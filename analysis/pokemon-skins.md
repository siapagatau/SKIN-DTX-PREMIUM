# Analisis skin event Pokémon (7 skin)

Dasar: skin-10 (Yamaha DTX-Multi 12 Black Original Tall Pad). Layout, ID, hit area, skin.json (controls/mapping/indikator/layout), LCD, knob, dan body hitam IDENTIK. 12 pad. Dibangun oleh `tools/build_pokemon_skins.py` (ada di proyek APK).

Yang berubah per skin:
- Pad (strip + besar), kanal antar pad, bibir pad, state aktif: rona abu-biru diganti warna Pokémon dengan shading asli dipertahankan (pad aktif = lebih terang + garis tepi 3px warna kontras).
- Tombol KIT (btn-preset-menu) dan highlight state-tekan tombol = warna aksen; tombol kiri/kanan (seek) = warna samping; lampu keypad 12 tombol = warna lampu; garis tepi panel = turunan warna pad. LCD tetap hijau lime (keterbacaan).
- Stiker: Pokémon (Dream World, vektor path murni) di pad-5, dengan garis putih die-cut + bayangan tipis. `deco-sticker-pokemon` (normal) dan `deco-sticker-pokemon-active` (aktif), tanpa hit area. Tanpa <image>/<use>/<filter>.

| skin_id | pad | garis aktif | stiker |
|---|---|---|---|
| pokemon-pikachu | kuning emas #f2c230 | merah #e53935 | Pikachu |
| pokemon-bulbasaur | tosca-hijau #4fb89a | kuning #ffe14d | Bulbasaur |
| pokemon-charmander | oranye #f08a32 | krem #fff0a0 | Charmander |
| pokemon-squirtle | biru #4aa6dc | kuning #ffd23f | Squirtle |
| pokemon-psyduck | kuning pastel #f4d86a | biru #2f9be0 | Psyduck |
| pokemon-snorlax | biru-tosca #4b8f98 | krem #f6e7b8 | Snorlax |
| pokemon-mewtwo | lavender #b79ae0 | ungu #6a2fd0 | Mewtwo |

Event (events/events.json): 1 event = 1 skin (klien hanya mendukung satu skin_id per event), 5 misi per event memakai tipe yang dikenal klien; target naik dari Pikachu (paling ringan) ke Mewtwo (paling berat). Skin event tidak tampil di tab Skin sampai diklaim (EventProgressManager.isEventSkin).
Tidak ada preview.svg (sama seperti skin event sebelumnya; skin event tersembunyi dari katalog bebas).
