# Analisis skin-02 — Ashley DME-705 Percussion Pad

Referensi: 808647.jpg (layout, 910x804) + 808649.jpg (branding Ashley DME-705). Nama produk memakai ASHLEY, bukan Lekato.

- Canvas/viewBox: 0 0 910 804 (koordinat piksel gambar referensi).
- Pad: 9 (3 strip karet atas = pad-1..3, 6 pad besar = pad-4..9). Tidak ada bukti 12/16 pad, jadi dipakai 9 saja (min=9, max=9).
- Panel: tombol CLICK, KIT, REC, SETUP, ▲, ▼, OK, SELECT, −, +, power, knob volume kiri (vol-knob), knob besar kanan, LCD oranye.
- Dekorasi tanpa fungsi: logo ASHLEY, label DME-705 Percussion Pad, LED TRIGGER/FOOTSWITCH, tab LCD (HOME/WAVE/LOOP/EFFECT/ADV).
- Warna garis pad mengikuti foto Ashley (oranye-merah), body lebih hitam.

Mapping tombol: CLICK=music.toggle, KIT=preset.menu, REC=record.toggle, SETUP=padSettings.open, ▲=preset.prev, ▼=preset.next, OK=sound.set, SELECT=file.load, −=music.seekBack, +=music.seekForward, power=skin.pick, knob besar (tap)=music.panel.
Fungsi tanpa kontrol: file.export, theme.open, screenrecord.toggle.

v1.5 (2026-10-09): skin.json display lines=4, template ["","KIT","P{preset:000}",""] agar teks LCD tidak kebesaran. SVG tidak berubah selain versi.

v1.6 (2026-10-09): naik versi saja (SVG/preview/skin.json); tidak ada perubahan tampilan.

v1.7 (2026-10-10): font polos diganti lettering outline (path dari Carlito/DejaVu Bold, tanpa <text>, tanpa font eksternal): ASHLEY gradien perak + bayangan bertingkat, "DME-705" gradien tembaga miring + "Percussion Pad" italic dengan tracking, TRIGGER/FOOTSWITCH krem-tembaga, label tombol bold dengan efek timbul putih, tab LCD bold. slot-display: rect pertama = jendela teks 96x46 di pusat LCD (427,729), rect kedua = LCD 118x94. Template 2 baris ["KIT","P{preset:000}"], lines=2.

v1.8 (2026-10-10): restyle mengikuti foto asli 808648.jpg (1108x976, skala 0.8213 ke viewBox 910x804): panel hitam, bezel LCD hitam rounded, LCD oranye jenuh 368..545 x 672..775, tombol mint (#eef7f0->#cfe5d9), knob hitam + cincin krom, tombol power krem, LED putih (117/138/160/182), garis pad 2.6px tembaga gelap. Semua ID, hit area, layout, jendela teks LCD tetap.

v1.9 (2026-10-10): penyempurnaan lanjutan terhadap foto 808648.jpg — lihat CHECKPOINT untuk daftar posisi kontrol yang bergeser (power, knob kecil, knob besar, tombol -/+). Hit area tetap di dalam panelZone dan tidak saling tumpuk.

v2.0 (2026-10-10): DIBUAT ULANG dari nol berdasarkan foto 808648.jpg (1108x976). viewBox baru 0 0 1108 976 = koordinat piksel foto 1:1 (bukan lagi 910x804). 9 pad (3 strip karet bertitik + 6 pad arang, garis tembaga tipis + tab krem), pita abu atas, plat hitam, LED trigger putih, tombol mint (KIT/▲/▼ lebih putih), knob kecil + titik tick, knob besar bercincin krom, tombol -/+ berbentuk panah, LCD oranye dengan tab HOME bercoklat. Teks memakai <text> generik (sans-serif/monospace), tanpa path outline. Semua ID, mapping fungsi, dan jumlah kontrol sama dengan v1.9; hanya koordinat berubah. layout: padZone 0 0 1108 722, panelZone 0 722 1108 254. slot-display: rect pertama = jendela teks 110x50 di tengah LCD, rect kedua = LCD. Tanpa overlap hit area, semua hit di dalam zonanya. Belum diuji di APK.

v2.1 (2026-10-10): revisi pad + lapisan body (ref 808648.jpg). Pad: garis tembaga 3px bersegmen dengan celah di persimpangan dan tab perunggu, bingkai bersudut membulat, strip karet berbentuk silinder dengan titik cembung 3 baris berselang-seling, pad arang dengan sorot tepi bawah. Body bawah: pita abu terang (#626260->#3a3a3a) dengan garis sorot atas, sisi kiri/kanan abu miring, bibir cekungan abu gelap, cekungan panel hitam, sehingga tiap lapisan terpisah jelas. Kontrol/ID/mapping tidak berubah; posisi pad bergeser 1-2 px mengikuti ukuran foto.

v2.2 (2026-10-10): body bawah disesuaikan ulang dengan foto 808648.jpg. Sisi kiri/kanan = badan abu gelap polos (bukan gradasi terang); ujung pita miring simetris (x0->48 kiri, x1108->1058 kanan); dinding cekungan hitam miring melebar ke bawah (kiri 47->28, kanan 1058->1090) dengan garis tepi terang + strip abu gelap di kanan; panel cekungan hitam; pita atas lebih gelap/rata. Knob volume kecil diperkecil sedikit agar label "-" terlihat. ID/mapping/hit area tidak berubah.

v2.3 (2026-10-10): sisi kanan body dicerminkan dari sisi kiri (badan abu polos, ujung pita 1108->1060, dinding cekungan hitam 1061->1080, panel 1038->1062); garis terang dan strip abu tambahan di kanan dihapus. ID/mapping/hit area tidak berubah.

v2.4 (2026-10-10): tanda ® di samping logo ASHLEY dihapus. Lainnya tidak berubah.

v2.5 (2026-10-10): perbaikan animasi ketuk + lampu indikator, mengikuti gaya skin LED (skin-01). Pad: state aktif kini menyala terang (gradasi oranye-emas, cahaya radial di tengah, kilap atas, garis tepi krem 4-5px, dua garis dalam); strip karet 1-3 ikut menyala dan titik-titiknya berpendar. Lampu: 9 lampu bulat di blok TRIGGER/FOOTSWITCH (baris atas 5 lampu = pad 1-5, baris bawah 4 lampu = pad 6-9); mati = coklat redup, menyala = `led-pad-N-on` (halo + inti putih-emas) lewat `indicators` di skin.json. Butuh APK Skin v3.3. Layout/ID/hit area/mapping tidak berubah. Belum diuji di APK.

v2.6 (2026-10-10): pad diperbaiki mengikuti foto close-up 814829.jpg (warna/profil diukur dari piksel). Pad besar: permukaan abu netral #3a3939 -> #454641 (lebih terang ke bawah) + bayangan horizontal halus (kiri terang, kanan gelap), anyaman sangat halus (pattern 4x4, noise ~1.6 seperti foto), bevel: garis terang tipis di kiri, garis terang 3px di bawah + bayangan gelap di bawahnya, tepi kanan gelap, sudut r=6, kanal gelap di sekeliling pad (statis di layer-bg). Strip karet: silinder dengan profil dari foto (atas gelap kecoklatan, sorot di ~60% tinggi, bawah gelap + tepi hitam), ujung kanan 12px lebih pendek dengan bayangan ujung silinder (hit area tetap), titik cembung lebih kecil (r2.8) dengan bayangan kiri-bawah + sorot kanan-atas. Garis tembaga: gaya tabung (halo coklat 9px, tepi #a85a38, tengah #e9a07e, inti #f6cdb3), tab krem-tan bergradasi. Efek ketuk (v2.5) dan lampu indikator tidak berubah selain ujung kanan strip aktif mengikuti bentuk baru. ID/mapping/hit area/layout tidak berubah. Belum diuji di APK.

v2.7 (2026-10-10): efek ketuk pad DISEDERHANAKAN mengikuti skin Ashley versi LED. Pad aktif tidak lagi oranye penuh: tampilan sama dengan normal, hanya sedikit lebih terang (overlay putih 10%) + garis tepi tembaga tipis. Tab krem di bawah tiap pad (9 buah) kini jadi LED: redup (tan) saat normal, menyala merah-oranye + halo saat pad diketuk (digambar di dalam pad-N-normal / pad-N-active, jadi bekerja di semua versi APK). Lampu indikator blok TRIGGER/FOOTSWITCH (led-pad-N-on + "indicators") dihapus; kini dekorasi statis. Tidak butuh APK Skin v3.3 lagi. ID/mapping/hit area/layout tidak berubah.

v2.7 revisi: warna LED menyala diubah jadi merah murni (#ff6b6b -> #e00d0d, halo #ff1a1a).

v2.8 (2026-10-10): semua pad disejajarkan dalam satu grid. Strip karet atas dan pad besar kini punya x dan lebar sama per kolom (x=16.5/381.5/746.5, lebar 342, sebelumnya strip 332-342 dan pad 342-347 dengan x berbeda). Area gelap (cekungan) di sekeliling pad, tab LED, garis tembaga horizontal, dan pemisah vertikal (x=370/735) ikut dirapikan simetris. Hit area strip disesuaikan, tidak tumpang tindih. ID/mapping/layout tidak berubah.

v2.9 (2026-10-10): perbaikan lampu. (1) LED tab di bawah tiap pad dulu berada di luar hit area pad sehingga tidak tergambar saat diketuk (versi LED yang jalan menaruh LED di dalam hit area); hit-pad-1..9 diperpanjang sampai mencakup LED + halo (strip y5..106, baris 1 y107..416, baris 2 y417..728, kolom diperlebar 5px ke kiri). layout padZone 0 0 1108 730 / panelZone 0 730 1108 246 agar semua hit di dalam zona. (2) 9 lampu indikator body (TRIGGER/FOOTSWITCH, led-pad-N-on + "indicators" di skin.json) dikembalikan, kini menyala merah (butuh APK Skin v3.3). LED tab di pad tidak butuh v3.3. ID/mapping/fungsi tidak berubah.

v3.0 (2026-10-19): tekstur pad kotak (pad-4..9) diganti pattern butiran diagonal p-grain (4x4, garis diagonal gelap 0.08 + terang 0.04), sama seperti pad skin DTX terbaru (skin-08), dengan warna tetap Ashley (g-pad #3a3939..#454641). Pattern anyaman lama p-weave (opasitas 0.008/0.016, hampir tak terlihat dan pecah saat screenshot) tidak lagi dipakai di pad kotak. Strip pad-1..3, bevel, LED, ID/hit area/mapping/layout tidak berubah.

v3.0 revisi (2026-10-19): permukaan pad kotak (pad-4..9) dibuat FLAT: gradasi g-pad (#3a3939->#454641) diganti warna solid #3f3f3c dan overlay bayangan g-pad-sh dihapus, karena gradasi tipis menimbulkan garis/banding pindah warna di screenshot. Tekstur p-grain, bevel, LED tetap.

v3.0 revisi 2 (2026-10-19): garis terang pinggir pad kotak (sorot atas, kiri, bawah) dihapus atas permintaan; garis gelap tepi tetap.

v3.0 revisi 3 (2026-10-19): penghapusan garis terang pinggir pad dibatalkan; garis terang atas/kiri/bawah dikembalikan seperti semula. Pad tetap flat + tekstur p-grain.

v3.1 (2026-10-26): ujung kanan strip pad-1..3 disamakan dengan ujung kiri (tanpa bayangan gelap, sorot tipis cermin; strip 2/3 tanpa scale non-1). Garis tepi state aktif pad-1..9 = 3px solid #ffb27d inset 1.5 (gaya DTX, warna tembaga terang), LED tab di bawah pad tidak tertabrak dan tetap menyala merah. ID/hit area/mapping/layout tidak berubah.
