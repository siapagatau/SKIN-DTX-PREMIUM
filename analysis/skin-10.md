# Analisis skin-10 — Yamaha DTX-Multi 12 Black Original Tall Pad

Varian Tall dari skin-08 (DTX hitam ORI, ref 824287.png / 824298.png). Warna, pad doff berbutir, body, panel, tombol (KIT hijau, kiri/kanan kuning, UTILITY putih), knob, LCD, lampu indikator, ID, mapping, dan fungsi IDENTIK dengan skin-08. 12 pad. Cara meninggikan sama dengan skin-09 (Tall dari skin-01).

Perubahan:
- Strip pad atas (pad 1-3): tinggi 61 -> 111 (+50).
- Strip pad bawah (pad 10-12): tinggi 64 -> 114 (+50).
- Pad besar (pad 4-9) ukuran tetap; barisnya turun +50 mengikuti strip atas.
- Panel bawah (LCD, tombol, knob, lampu indikator) turun +100; kanal vertikal, alur horizontal, dan body dipanjangkan.
- viewBox 900x900 -> 900x1000. layout: padZone "30 54 840 762", panelZone "30 816 840 130".
- Hit area pad 1-3 dan 10-12 ikut ditinggikan (tinggi 111 dan 114); hit area lain digeser. Tidak ada overlap, semua di dalam zona.
- Rect state aktif (garis kuning) dan garis tepi pad strip ikut ditinggikan (dicek semua 12 pad).
- Tanpa <filter>/<image>. Tinggi tambahan diatur lewat D1 (atas) dan D2 (bawah) di skrip pembuat; mudah diubah.
