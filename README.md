# DTX Skins Repository

Repository skin controller untuk APK DTX. **Terpisah dari kode APK** (tidak ada kode APK di sini).

## Struktur
```
skins-repo/
├── README.md
├── index.json          <- katalog; dibaca APK
├── PROMPT_SKIN.md      <- aturan untuk AI pembuat skin
└── skins/<id>/
    ├── skin.svg        <- tampilan + layout + ID + hit area
    ├── skin.json       <- mapping fungsi
    └── preview.svg
```

## Alur APK
`config/skin-repo.json (indexUrl)` → `index.json` → `skin.json` + `skin.svg` → cache di perangkat → Skin Engine.
APK memverifikasi `sha256` dan `size` tiap file sebelum menyimpan. Skin terunduh tetap bisa dipakai offline.

## Menambah skin baru (tanpa update APK)
1. Buat folder `skins/<id>/` berisi `skin.svg`, `skin.json`, `preview.svg`.
2. Tambahkan entri di `index.json` (id, name, version, author, padMin, padMax, path, files + sha256 + size).
3. Commit & push. Setiap file yang berubah wajib diperbarui sha256/size-nya (`sha256sum`, `stat -c %s`).

`id` hanya huruf/angka/`_`/`-`. `path` harus berakhiran `/`, tanpa `..`.

## Mengisi indexUrl di APK
Isi `config/skin-repo.json` (dan salinannya di `app/src/main/assets/config/`) dengan URL raw `index.json`, mis.
`https://raw.githubusercontent.com/<user>/<repo>/main/index.json` (harus `https://`).
