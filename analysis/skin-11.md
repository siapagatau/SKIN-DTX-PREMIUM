# Analisis skin-11 — Ashley DME-705 Tall Pad

Varian skin-02 (Ashley v3.1). Warna, body, panel, tombol, knob, LCD, lampu indikator, LED tab per pad, ID, mapping, dan fungsi IDENTIK. 9 pad.

Perubahan:
- Strip karet atas (pad 1-3): tinggi 80 -> 130 (+50). Titik cembung disusun ulang jadi 5 baris berselang-seling (sebelumnya 3 baris); gradasi silinder meregang mengikuti tinggi.
- Pad besar (pad 4-9) ukuran tetap; barisnya turun +50. Garis tembaga, tab LED, kanal, body, panel bawah (LCD, tombol, knob, lampu indikator) ikut turun +50.
- viewBox 1108x976 -> 1108x1026. layout: padZone "0 0 1108 780", panelZone "0 780 1108 246".
- Hit area pad 1-3 ditinggikan (101 -> 151), lainnya digeser +50. Tidak overlap, semua di dalam zona.
- Efek ketuk = Ashley v3.1 (garis tepi 3px solid #ffb27d inset + LED tab merah).
