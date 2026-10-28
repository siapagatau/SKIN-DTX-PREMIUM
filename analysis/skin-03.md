# Analisis skin-03 — Yamaha DTX-Multi 12 White Carbon

Referensi: 810756.jpg (tekstur stiker carbon fiber) + 810785.png (DTX-Multi 12 dengan pad distiker karbon). Varian dari skin-01.

- Canvas/viewBox: 0 0 900 900 (sama dengan skin-01). Layout, ID, hit area, dan skin.json identik dengan skin-01 -> kompatibel penuh dengan APK.
- Pad: 12 (padMin = padMax = 12). Pad 13–16 tidak didukung.
- Perubahan visual:
  1. Pad: dasar gelap + pattern `p-carbon` (twill, tile 12x9 mengikuti 810787.jpg: blok tegak terang-atas, bergeser turun-kanan; tanpa filter) + kilau `g-carbon-sheen`. State aktif tetap menyala (pad-on + outline kuning).
  2. Body: putih (#efeff0), panel bawah gradien putih-abu muda; celah antar pad abu-abu sedang (agak gelap).
  3. Teks/penanda di panel yang tadinya terang (MIN/VOLUME/MAX, jalur knob, DEC/INC, bracket) dibuat gelap agar terbaca di body putih. Housing LCD, logo, dan knob tetap hitam.
- Pemetaan fungsi sama dengan skin-01; `preset.menu` memakai `apkStatus: existing` (sesuai skin-02).
  4. Pad 5 (tengah atas): stiker Apple putih (hasil trace 810801.png jadi path vektor, tinggi ±170 unit, dipusatkan di pad). Dekorasi saja (`deco-apple-sticker` di state normal, `deco-apple-sticker-active` di state aktif), tanpa hit area, tidak mengubah fungsi pad 5.
  5. Pad 9 (kanan tengah): stiker logo TK (Tukang Kendang) putih, hasil trace 792990.png jadi path vektor (emblem lingkaran+TK, tanpa teks tagline), tinggi ±180 unit, dipusatkan di pad. Dekorasi saja (`deco-tk-sticker` normal, `deco-tk-sticker-active` aktif), tanpa hit area. Versi skin-03 jadi 1.1.
  6. Pad 4 (kiri atas-tengah): stiker logo DHEHAN Jenggot (sound system), hasil trace 811493.jpg jadi path vektor: latar bulat hitam (`ellipse`), cincin + headphone + teks DHEHAN emas (gradien `g-dhehan-gold`), teks JENGGOT abu. Lebar ±230 unit, dipusatkan di pad (166.5, 259). Dekorasi saja (`deco-dhehan-sticker` normal, `deco-dhehan-sticker-active` aktif), tanpa hit area. Versi skin-03 jadi 1.2.
  7. Pad 7 (kiri bawah-tengah): stiker logo Santuy Code (identitas pemilik), hasil trace 811507.png jadi path vektor putih (garis awan + teks "Santuy Code", tanpa latar hijau; lubang huruf lewat fill-rule evenodd), lebar ±225 unit, dipusatkan di pad (166.5, 516.5). Dekorasi saja (`deco-santuy-sticker` normal, `deco-santuy-sticker-active` aktif), tanpa hit area. Versi skin-03 jadi 1.4.
  8. Pad 6 (kanan atas-tengah): stiker clover (daun empat) hijau, hasil trace 811531.jpg jadi path vektor, lebar ±203 unit, dipusatkan di pad (733.5, 259). Celah/garis tengah daun hanya diisi putih di dalam siluet daun (tidak keluar ke batang/tepi), plus stroke putih ±4 unit mengelilingi clover agar terlihat di pad gelap. Skala 0.92. Dekorasi saja (`deco-clover-sticker` normal, `deco-clover-sticker-active` aktif), tanpa hit area. Versi skin-03 jadi 1.5.
