# PROMPT_SKIN.md — Aturan Membuat Skin Controller APK DTX

Dokumen ini MANDIRI: AI yang hanya menerima dokumen ini + gambar referensi harus bisa membuat skin yang kompatibel
dengan Skin Engine APK DTX (pad sampler / drum pad / kendang elektronik). Tidak perlu membaca percakapan sebelumnya.
Bahasa dokumen: Indonesia. Jangan menebak fungsi APK di luar katalog di bawah.

## 1. Konsep
SKIN BUKAN wallpaper dan BUKAN sekadar tema. **SKIN = TAMPILAN + LAYOUT + CONTROLLER + AREA SENTUH + ID KONTROL.**
- `skin.svg` = tampilan + posisi + ID + hit area + state visual. **Tanpa logika** (tanpa JavaScript, `onclick`, event handler, audio).
- `skin.json` = daftar kontrol + mapping ke fungsi APK.
- APK = audio engine + fungsi + sentuhan. APK **mengikuti layout skin**, jangan memaksa layout bawaan APK ke gambar.

Contoh alur: gambar PAD → grup `pad-1` + `hit-pad-1` → APK membuat touch area di posisi itu → disentuh → memutar sample pad 1.

## 2. Input & Output
Input: 1 atau lebih gambar referensi. **Satu gambar = satu skin** (`skin-01`, `skin-02`, ...).
Output per skin (folder `skins/<id>/`):
```
skin.svg      skin.json      preview.svg
```
Struktur repository:
```
skins-repo/
├── README.md   index.json   PROMPT_SKIN.md
└── skins/<id>/{skin.svg, skin.json, preview.svg}
```
Repository TIDAK boleh berisi kode APK. `id` hanya `A-Z a-z 0-9 _ -` (maks 64).

## 3. Alur kerja (bertahap, tiap tahap menghasilkan file nyata + CHECKPOINT.md)
1. **Analisis**: per gambar — nama skin, rasio/ukuran, daftar pad, tombol, knob/slider, display, dekorasi, elemen tanpa fungsi APK, apakah 12/16 pad mungkin. Tulis `analysis/skin-XX.md`.
2. **Desain**: ukuran canvas, viewBox, koordinat pad/tombol/knob/display, ID, hit area. Layout **mengikuti gambar**.
3. **SVG** → validasi. 4. **skin.json** → validasi mapping. 5. **preview.svg** (skin + overlay hit area + label ID). 6. Daftarkan di `index.json` (sha256 + size).
Jangan mengklaim tahap selesai bila file belum dibuat/divalidasi. Jika berhenti, tulis `CHECKPOINT.md` (Project, Current Stage, Completed, Files Created, Reference Images, Skin Names, Detected Controls, Unsupported Controls, Important Decisions, Problems, Next Stage, Instructions for Next AI, Previous Stage). AI berikutnya membaca checkpoint dulu dan melanjutkan dari Next Stage tanpa mengulang. Jangan hapus hasil tahap lama.

## 4. Aturan skin.svg
### 4.1 Root (WAJIB semua atribut)
```xml
<svg xmlns="http://www.w3.org/2000/svg"
     data-skin-name="Nama Skin" data-skin-version="1.0" data-skin-author="Author"
     data-pad-min="12" data-pad-max="12"
     width="900" height="900" viewBox="0 0 900 900">
```
`viewBox` = koordinat utama (semua posisi memakai koordinat ini). Jangan membuat SVG khusus ukuran layar tertentu; APK menskalakan sendiri (FIT, skin tetap utuh).

### 4.2 Larangan (skin DITOLAK bila ada)
`<script>`, `<foreignObject>`, `<image>`, `<use>`, `<audio>`, `<video>`, `<iframe>`; atribut `on*`; `href`/`xlink:href`; URL `http(s)://` di atribut (kecuali `xmlns*`); aset eksternal; > 20.000 elemen; file > 4 MB; viewBox ≤ 0 atau > 100.000.
Hindari juga `<metadata>` (mis. c2pa), font eksternal.
Renderer APK = AndroidSVG: **tanpa `<filter>`**, `letter-spacing` diabaikan. Gradien, pattern, path, text, transform aman. Pakai font generik (`monospace`, `sans-serif`).

### 4.3 Konvensi ID (huruf kecil, tanda hubung)
| Elemen | ID | Keterangan |
|---|---|---|
| Pad ke-N | `pad-N`, `pad-N-normal`, `pad-N-active` | `pad-N` = `<g data-type="pad">` berisi dua grup state |
| Tombol | `btn-<nama>`, `btn-<nama>-normal`, `btn-<nama>-active` | `<g data-type="button">` |
| Hit area | `hit-<id kontrol>` | mis. `hit-pad-1`, `hit-btn-play`, `hit-vol-knob` |
| Knob | `vol-knob` (+ `vol-track`, `vol-handle`) | lihat 4.5 |
| Display | `slot-display` | lihat 4.6 |
| Dekorasi | `deco-<nama>` | `<g data-type="decorative">`, tanpa hit area |

State: `*-normal` tampil; `*-active` diberi `display="none"` (APK menampilkan saat ditekan). Pad & tombol wajib punya state normal DAN active (active hilang = hanya peringatan, tanpa efek tekan).

### 4.4 Hit area
- Berupa `<rect id="hit-..." x y width height fill="#000" fill-opacity="0"/>`, dikumpulkan di `<g id="layer-hit">` paling atas.
- Wajib: `x,y,width,height` ada, lebar/tinggi > 0, **seluruhnya di dalam viewBox**.
- Setiap pad, tombol, dan knob WAJIB punya hit area. Display & dekorasi tidak punya.
- Hindari hit area saling tumpuk (peringatan). Tombol kecil boleh digambar kecil; APK memperluas target sentuh hingga ~40dp, tapi jangan sampai menimpa kontrol lain.
- Pad ditrigger saat jari **turun**; tombol saat **tap**.

### 4.5 Knob / slider (rotary)
```xml
<g id="vol-knob" data-type="rotary" data-cx="97" data-cy="765"
   data-angle-min="-135" data-angle-max="135" data-value-default="0.78"> ... </g>
<path id="vol-track" .../>   <!-- jalur -->
<... id="vol-handle" .../>   <!-- penanda -->
```
`data-cx/data-cy` = pusat putar (WAJIB). APK menimpa rotasi: sudut = min + (max−min) × nilai, jadi `transform` awal hanya visual statis. Slider/knob wajib punya track dan handle. Saat ini satu-satunya fungsi rotary: `volume.kendang`. Slider lurus belum didukung engine: gambarkan sebagai dekorasi atau catat di unsupported.

### 4.6 Display (LCD)
`<g id="slot-display" data-type="display">` — **elemen `<rect>` pertama di dalamnya** = area LCD. APK menggambar teks dari template di skin.json di area itu (teks `<text>` contoh di SVG hanya visual statis). Tidak punya hit area.

### 4.7 Dekorasi
Tombol/label/logo/speaker/dll yang tidak punya fungsi APK → `deco-*`, tanpa hit area, dicatat di `unsupportedInReference`. **Jangan membuat tombol palsu.**

### 4.7b Lampu indikator pad (opsional)
Kotak/lampu yang harus menyala saat pad dipukul (mis. keypad 12 tombol DTX-Multi 12). Gambar lampu MATI di dasar (warna redup) dan lampu MENYALA sebagai `<g id="led-pad-N-on" display="none">`; **`<rect>` pertama di dalamnya = area lampu** (sertakan halo di dalamnya). Daftarkan di skin.json level atas:
```json
"indicators": [ { "id": "led-pad-1", "pad": 1, "on": "led-pad-1-on" } ]
```
Tanpa hit area, tanpa function. Pad N dipukul -> lampu N menyala lalu padam bertahap. Butuh APK Skin v3.3 (APK lama mengabaikannya).

### 4.8 Urutan layer yang disarankan
`layer-bg` → `layer-deco` → `layer-controls` (pad/tombol/knob/display) → `layer-hit` (paling atas).

## 5. Katalog fungsi RESMI (hanya ini yang boleh di skin.json)
| function | Tipe kontrol | Keterangan |
|---|---|---|
| `sample.play` | pad | params `{"pad": N}`, N = nomor pad |
| `music.toggle` | button | play/stop lagu |
| `music.panel` | button | tampil/sembunyi panel volume & musik ASLI APK (tanpa dialog baru) |
| `music.seekBack` / `music.seekForward` | button | mundur / maju 5 detik |
| `preset.prev` / `preset.next` | button | ganti preset |
| `preset.menu` | button | tampil/sembunyi panel preset ASLI APK (tanpa dialog baru) |
| `file.load` | button | muat file |
| `file.export` | button | ekspor |
| `padSettings.open` | button | dialog pengaturan pad |
| `sound.set` | button | SET SUARA untuk pad terakhir yang diketuk |
| `theme.open` | button | tema warna |
| `skin.pick` | button | dialog pemilih skin |
| `record.toggle` | button | rekam audio |
| `screenrecord.toggle` | button | rekam layar |
| `volume.kendang` | rotary | volume 0..1 (APK memetakan ke 0..1,5) |
| `display.preset` | display | template teks, mis. `["KIT","P{preset:000}"]` |

Function di luar katalog -> skin DITOLAK.

**Prinsip Skin v2: tidak ada menu/tombol tambahan di luar skin.** Fungsi APK yang ingin bisa dipakai pengguna HARUS diberi kontrol di gambar skin (tombol apa pun, tidak harus bertuliskan fungsinya). Fungsi yang tidak diberi kontrol = tidak bisa diakses di skin itu. Tombol TIDAK wajib punya grup `-active`/`-normal`: bila tidak ada, aplikasi memberi highlight putih transparan saat ditekan. Tombol tetap WAJIB punya `hit-<id>` (rect transparan) di `layer-hit`.

## 6. Aturan skin.json
```json
{
  "schemaVersion": 1,
  "name": "Nama Skin", "version": "1.0", "author": "Author",
  "svg": "skin.svg",
  "viewBox": "0 0 900 900",
  "padSupport": { "min": 12, "max": 12 },
  "controls": [
    { "id": "pad-1", "type": "pad", "index": 1, "hit": "hit-pad-1",
      "states": { "normal": "pad-1-normal", "active": "pad-1-active" }, "trigger": "down" },
    { "id": "btn-play", "type": "button", "hit": "hit-btn-play",
      "states": { "normal": "btn-play-normal", "active": "btn-play-active" }, "trigger": "tap" },
    { "id": "vol-knob", "type": "rotary", "hit": "hit-vol-knob", "track": "vol-track", "handle": "vol-handle",
      "angleMin": -135, "angleMax": 135, "valueRange": [0, 1], "defaultValue": 0.78 },
    { "id": "slot-display", "type": "display", "lines": 2 }
  ],
  "mapping": {
    "pad-1": { "function": "sample.play", "params": { "pad": 1 }, "apkStatus": "existing" },
    "btn-play": { "function": "music.toggle", "apkStatus": "existing" },
    "vol-knob": { "function": "volume.kendang", "apkStatus": "existing" },
    "slot-display": { "function": "display.preset", "template": ["KIT", "P{preset:000}"], "apkStatus": "wrap-existing" }
  },
  "unsupportedInReference": [
    { "id": "deco-midi", "kind": "decorative", "label": "MIDI", "reason": "Tombol hardware tanpa padanan fungsi di APK" }
  ]
}
```
Aturan: tipe valid `pad | button | rotary | display`; `trigger` `down|tap`; setiap kontrol WAJIB punya entri `mapping` dengan `function` dari katalog yang cocok dengan tipenya; `params.pad` = `index`; tiap `id`/`hit`/state harus ada di SVG; tidak ada ID ganda; `svg` hanya nama file biasa (tanpa `/`, `\`, `..`). `apkStatus`: pakai `existing` untuk fungsi katalog (jangan menciptakan `new`). Daftar semua elemen tak berfungsi di `unsupportedInReference` (`id`/`function`, `kind`, `label`, `reason`).
Jika atribut SVG dan skin.json berbeda untuk padMin/padMax/nama/versi, APK mengutamakan **atribut SVG** — samakan keduanya.

## 6A. Layout skin di layar (skin.json "layout") — SELURUH skin di-STRETCH
APK menggambar skin sebagai SATU gambar yang di-stretch memenuhi area layar (skala X dan Y boleh berbeda), tanpa area kosong
dan tanpa pemisahan bagian: pad, panel, tombol, semuanya diperlakukan sama, desain asli tidak diubah.
```json
"layout": { "padZone": "30 54 840 662", "panelZone": "30 716 840 130" }
```
- **padZone** = persegi yang membungkus SEMUA pad. **panelZone** = persegi berisi LCD, tombol, knob (semua kontrol non-pad).
  Gabungan keduanya = bagian skin yang ditampilkan (tepi kosong viewBox di luarnya dibuang).
- User bisa menyembunyikan panel: saat itu hanya padZone yang di-stretch memenuhi layar dan kontrol panel tidak tampil.
  Karena itu panel sebaiknya di BAWAH pad dan hit area tiap kontrol harus di dalam zonanya (validator memberi peringatan bila tidak).
- Bila `layout` dihilangkan: padZone = gabungan hit pad + 2 unit; panelZone = dari tepi bawah padZone sampai kontrol non-pad terbawah + 30 unit.
- Karena di-stretch, bentuk bulat (knob, tombol) tampil agak lonjong di layar yang sangat lebar. Rancang elemen panel agar tetap enak dilihat
  bila melebar; knob tetap berputar dengan benar.

## 7. Mode 12 / 16 pad
- Jumlah pad dibaca dari `data-pad-min`, `data-pad-max` dan keberadaan `pad-1..pad-N` (tidak di-hardcode). Nomor harus berurutan 1..N, N ≤ 16, dan padMin ≤ N ≤ padMax.
- Skin 12 saja: `min=12 max=12`, pad-1..pad-12. Opsi 16 dinonaktifkan dengan pesan "Pengaturan tambahan pad tidak didukung untuk skin ini."
- Skin 12–16: `min=12 max=16`, ada pad-1..pad-16. Pad 13–16 adalah grup terpisah (`pad-13..16` + `hit-pad-13..16`) dan **tampilan 12 pad harus tetap utuh** tanpa keempatnya (APK tidak menggambar dan tidak menerima sentuhan pad 13+ di mode 12).
- Bila gambar referensi tidak jelas bisa 16 pad, jangan memaksa: pakai 12 saja dan catat alasannya.

## 8. Checklist sebelum menyerahkan skin
**Visual**: layout/posisi/ukuran mengikuti gambar; tidak ada elemen di luar canvas; tidak ada overlap tak sengaja; terlihat sebagai controller.
**SVG**: valid XML; root 6 atribut lengkap; viewBox benar; tanpa script/onclick/aset eksternal/`<image>`/`<use>`/`<metadata>`; semua pad & tombol punya ID, hit area, state normal+active; knob punya `data-cx/cy`, track, handle; display punya `rect` pertama.
**skin.json**: JSON valid; semua kontrol punya mapping dari katalog; unsupported tercatat; padSupport sama dengan atribut SVG.
**Repo**: ada `skin.svg`, `skin.json`, `preview.svg`; `index.json` diperbarui (sha256 + size SEMUA file yang berubah); tidak ada kode APK.

## 9. Entri index.json
```json
{ "id": "skin-02", "name": "Nama", "version": "1.0", "author": "Author",
  "padMin": 12, "padMax": 12, "path": "skins/skin-02/",
  "files": { "skin.json": {"sha256": "...", "size": 0},
             "skin.svg":  {"sha256": "...", "size": 0},
             "preview.svg": {"sha256": "...", "size": 0} } }
```
`path` berakhiran `/`, tanpa `..`. Hitung dengan `sha256sum` dan `stat -c %s` SETELAH file final. APK memverifikasi keduanya; salah satu tidak cocok = unduhan ditolak. Menambah skin cukup upload folder + perbarui `index.json` (tanpa update APK). Skin yang sudah diunduh tetap bisa dipakai offline; skin rusak otomatis diganti skin default.

## 10. Hal yang TIDAK boleh
Membuat fungsi/ID palsu; menaruh logika di SVG; mengubah katalog fungsi; menghapus hasil tahap sebelumnya; menyatakan selesai tanpa file nyata; menggabungkan kode APK ke repository skin.
