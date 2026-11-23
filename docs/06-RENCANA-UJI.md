# Rencana Uji — Neraca Warga

## 1. Prinsip

1. **Agen yang menguji, YAN yang memutuskan.** Semua uji otomatis dan sebagian besar uji manual dijalankan agen di lingkungannya sendiri. YAN menerima bukti berupa laporan, tangkapan layar, dan tanda ✓/✗ CI. YAN hanya menguji hal yang membutuhkan penilaian manusia: kebenaran konten, uji perangkat nyata, dan uji kelas.
2. Setiap fitur menghasilkan `docs/laporan/NW-xx-uji.md` (format §8).
3. Uji dilakukan pada **build yang sama** dengan yang diserahkan dalam ZIP.

## 2. Lingkungan dan matriks perangkat

| Kode | Perangkat/peramban | Penguji | Kapan |
| --- | --- | --- | --- |
| D1 | Chromium (Playwright), emulasi Moto G Power / 4G lambat | Agen | Setiap fitur |
| D2 | Chromium desktop 1366×768 dan 1024×768 (proyektor) | Agen | Setiap fitur |
| D3 | Firefox dan WebKit (Playwright) | Agen | NW-01, NW-08, NW-12 |
| D4 | HP Android kelas bawah milik siswa/YAN (Chrome terbaru) | YAN | v0.6, v1.0 |
| D5 | HP Android lama (Chrome ±2 tahun lalu) bila tersedia | YAN | v1.0 |
| D6 | Laptop sekolah + proyektor kelas | YAN | v0.8 (uji kelas) |
| D7 | iPhone (Safari) bila tersedia | YAN | v1.0 (opsional) |

Emulasi yang wajib dicoba agen: `prefers-reduced-motion: reduce`, `prefers-color-scheme: dark`, `forced-colors: active`, lebar 320 px, zoom 200%, mode luring.

## 3. Uji otomatis

| Kode | Pemeriksaan | Alat | Lulus bila |
| --- | --- | --- | --- |
| AU-01 | Validitas HTML semua halaman | `html-validate` | 0 galat |
| AU-02 | Kerangka konsisten, judul unik, tanpa gaya/skrip *inline* | `tests/periksa-kerangka.mjs` | 0 temuan |
| AU-03 | Skema dan aturan data | `tests/periksa-data.mjs` | 0 temuan |
| AU-04 | Kesetiaan teks modul | `tests/periksa-modul.mjs` | Semua kutipan `data-asal="modul"`/`"asal": "modul"` ditemukan |
| AU-05 | Halaman termuat tanpa galat konsol | Playwright | 22/22 halaman |
| AU-06 | Aksesibilitas otomatis | `@axe-core/playwright` | 0 pelanggaran *serious/critical* |
| AU-07 | Tidak ada gulir horizontal di 320 px | Playwright (`scrollWidth ≤ clientWidth`) | Semua halaman |
| AU-08 | Tidak ada permintaan ke luar situs sebelum interaksi | Playwright (pantau `request`) | 0 permintaan lintas asal saat memuat halaman |
| AU-09 | Daftar *precache* lengkap | `tests/periksa-sw.mjs` | Cocok 100% (mulai NW-12) |
| AU-10 | Anggaran kinerja (P2) | Lighthouse CI | Sesuai 04 §13 |

## 4. Skenario uji penerimaan

Format: **Diberikan** keadaan awal → **Ketika** tindakan → **Maka** hasil. Skenario bertanda 🤖 diotomasi dengan Playwright.

### 4.1 Global

- **UJ-G1** 🤖 Diberikan halaman mana pun → Ketika menekan `Tab` pertama kali lalu `Enter` → Maka fokus berada di `<h1>` halaman.
- **UJ-G2** 🤖 Diberikan layar sempit → Ketika membuka Menu lalu menekan `Esc` → Maka laci tertutup dan fokus kembali ke tombol Menu.
- **UJ-G3** 🤖 Diberikan stasiun 3 → Ketika memilih *Berikutnya* → Maka `uji.html` terbuka dan penanda menunjukkan "Stasiun 4 dari 6".
- **UJ-G4** 🤖 Diberikan tema sistem gelap → Ketika halaman dimuat → Maka token gelap terpakai tanpa kedip tema terang.
- **UJ-G5** 🤖 Diberikan progres tersimpan → Ketika memilih *Hapus data di perangkat ini* lalu *Hapus data* → Maka kunci `neraca-warga:v1` hilang dan Beranda menampilkan *Mulai Belajar*.
- **UJ-G6** 🤖 Diberikan `localStorage` diblokir → Ketika mengisi LKPD → Maka pesan "Jawaban tidak dapat disimpan…" muncul sekali dan fitur tetap berjalan.

### 4.2 Mulai

- **UJ-M1** 🤖 Ketika memilih perasaan mana pun → Maka respons tampil dan **tidak ada perubahan** pada `localStorage`.
- **UJ-M2** 🤖 Diberikan permainan dimulai → Maka urutan tombol (kiri ke kanan) adalah Kewajiban, Keduanya, Hak.
- **UJ-M3** 🤖 Ketika menjawab 14 pernyataan hanya dengan keyboard → Maka skor akhir tampil, neraca dalam keadaan seimbang, dan lencana *Siap Belajar* didapat.
- **UJ-M4** 🤖 Ketika menjawab HK-04 dengan "Hak" → Maka umpan balik menyebut "Keduanya" dan Pasal 27 ayat (3).
- **UJ-M5** Diberikan gerak berkurang → Ketika menjawab → Maka kartu berganti tanpa meluncur dan token muncul tanpa jatuh.

### 4.3 Amati

- **UJ-A1** 🤖 Ketika tebakan 600 lalu *Lihat kenyataannya* → Maka pesan "Tebakanmu sangat dekat!…" muncul. Tebakan 300 → pesan "Kenyataannya lebih banyak…". Tebakan 900 → pesan "Tebakanmu lebih tinggi…".
- **UJ-A2** 🤖 Ketika halaman Amati dimuat → Maka tidak ada permintaan ke `youtube-nocookie.com` atau `ytimg.com` sampai tombol putar diketuk.
- **UJ-A3** 🤖 Diberikan luring → Maka tombol putar diganti pesan luring dan ringkasan video tetap terbaca.
- **UJ-A4** 🤖 Ketika memilih dua *chip* dan menulis tanggapan lalu memuat ulang → Maka pilihan dan teks pulih.

### 4.4 Ruang Baca dan glosarium

- **UJ-R1** 🤖 Ketika mengetik "hak" di pencarian glosarium → Maka hanya istilah yang mengandung "hak" yang tampil dan jumlahnya diumumkan sekali.
- **UJ-R2** 🤖 Ketika mengaktifkan istilah bertitik dengan `Enter` → Maka definisi tampil; `Esc` menutupnya dan fokus kembali ke istilah.
- **UJ-R3** 🤖 Pasangan Seimbang: keliru dua kali pada PS-1 → Maka petunjuk muncul; 7 pasangan tepat → pesan selesai.
- **UJ-R4** 🤖 Peta Pasal: mengetik "28J" → hanya Pasal 28J yang tampil; membukanya → dialog menampilkan "Kewajiban menghormati HAM orang lain…".
- **UJ-R5** 🤖 Siapa yang Menangani?: SM-06 dijawab "Peradilan Tata Usaha Negara" → umpan balik benar dengan alasan.
- **UJ-R6** 🤖 *Tandai sudah dibaca* pada 4 bagian → lencana *Penjelajah Pasal* didapat dan hub menunjukkan 4/4.

### 4.5 Selidiki (LKPD)

- **UJ-S1** 🤖 Diberikan `kasus-3.html` → Maka L2 menampilkan isian tambahan "Hak yang ingin dipenuhi siswa dan orang tua".
- **UJ-S2** 🤖 Ketika mengisi nama anggota di L0, mengisi L2, lalu memuat ulang → Maka L2 pulih dan **nama anggota kosong**; `localStorage` tidak memuat nama tersebut.
- **UJ-S3** 🤖 Ketika menekan *Butuh petunjuk?* tiga kali di L4 → Maka tiga petunjuk muncul berurutan dengan penghitung 1/3, 2/3, 3/3.
- **UJ-S4** 🤖 Ketika hanya satu upaya diisi lalu menekan *Lanjut* → Maka pesan minimal dua upaya muncul, terhubung dengan `aria-describedby`, dan fokus ke kolom yang bermasalah.
- **UJ-S5** 🤖 Ketika berpindah langkah → Maka fokus berada di judul langkah baru.
- **UJ-S6** 🤖 Ringkasan dicetak ke PDF (Playwright `page.pdf`) → Maka muat dalam A4, navigasi dan tombol tidak ikut tercetak.
- **UJ-S7** Tombol *Salin teks* → teks ringkasan masuk *clipboard* dan umpan balik "Disalin!" dibacakan.

### 4.6 Uji (kuis)

- **UJ-U1** 🤖 Menjawab sesuai kunci (C, A, D, B, C, A, D, B, A, C) → Maka nilai 100, TP 1 = 100, TP 2 = 100.
- **UJ-U2** 🤖 Menjawab benar hanya nomor 1–5 → Maka nilai 50, TP 1 = 100, TP 2 = 0, rekomendasi menampilkan bagian Ruang Baca 2 dan 4 tanpa duplikat.
- **UJ-U3** 🤖 Halaman hasil tidak memuat kata "KKTP" sebagai label capaian siswa.
- **UJ-U4** 🤖 Riwayat setelah 6 kali percobaan hanya menyimpan 5 entri terakhir.

### 4.7 Renungkan dan Berkarya

- **UJ-N1** 🤖 Ketika halaman dimuat → Maka lingkaran napas diam; setelah *Mulai*, fase berganti 4 dtk → 2 dtk → 6 dtk; *Jeda* menghentikan hitungan.
- **UJ-N2** 🤖 Diberikan gerak berkurang → Maka lingkaran tidak berubah ukuran; aba-aba dan hitung mundur tetap berjalan.
- **UJ-N3** 🤖 Refleksi a–d terisi lalu dimuat ulang → isian pulih; lencana *Perenung Bijak* didapat.
- **UJ-K1** 🤖 Tombol salin BD-1 → *clipboard* berisi teks BD-1 persis dan tombol tetap dapat difokus.

### 4.8 Mode Guru

- **UJ-T1** 🤖 Daftar segmen menampilkan durasi 15, 10, 5, 25, 35, 10, 20 menit (total 120).
- **UJ-T2** 🤖 Pada tampilan proyektor, `Spasi` memulai/menjeda timer, `→` pindah ke segmen berikutnya; pintasan tidak aktif ketika fokus di kolom isian.
- **UJ-T3** 🤖 Kalkulator nilai TP menghasilkan:

| Kasus | Benar 1–5 | Benar 6–10 | Ind. 1 | Ind. 2 | Ind. 3 | Nilai TP 1 → kategori | Nilai TP 2 → kategori | Pengayaan? |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| A | 4 | 5 | 3 | 3 | 4 | 78 → sudah mencapai | 100 → pengayaan/tantangan | Ya |
| B | 3 | 2 | 2 | 1 | 2 | 53 (52,5 dibulatkan ke atas) → remedial bagian yang diperlukan | 43 → remedial bagian yang diperlukan | Tidak |
| C | 1 | 2 | 1 | 1 | 1 | 22 → remedial seluruh bagian | 35 → remedial seluruh bagian | Tidak |
| D | 3 | 3 | 3 | 3 | 3 | 65 → remedial bagian yang diperlukan | 65 → remedial bagian yang diperlukan | Tidak |
| E | 4 | 4 | 2 | 1 | 4 | 66 (65,83) → sudah mencapai | 87 (86,67) → pengayaan/tantangan | Ya |
| F | 1 | 0 | 4 | 3 | 1 | 43 (42,5 dibulatkan ke atas) → remedial bagian yang diperlukan | 8 → remedial seluruh bagian | Tidak |
| G | 5 | 3 | 4 | 4 | 1 | 100 → pengayaan/tantangan | 48 → remedial bagian yang diperlukan | Tidak (TP 2 belum tercapai) |

- **UJ-T4** 🤖 Setelah memakai kalkulator dan memuat ulang → tidak ada data kalkulator di `localStorage`.
- **UJ-T5** 🤖 Rambu jawaban hanya menampilkan butir berstatus `disetujui`.
- **UJ-T6** Cetak LKPD kosong 1–4 dan soal (tanpa kunci/dengan kunci) rapi di A4.

### 4.9 PWA dan luring

- **UJ-P1** 🤖 Setelah satu kunjungan ke Beranda, mode luring → semua 22 halaman dapat dibuka dari *cache*.
- **UJ-P2** 🤖 Halaman yang belum pernah di-*cache* saat luring → `offline.html` tampil.
- **UJ-P3** 🤖 Versi SW dinaikkan → notifikasi "Versi baru tersedia" muncul; *Muat ulang* memuat versi baru.
- **UJ-P4** Di Android (D4), tombol *Pasang di perangkat* muncul dan aplikasi terpasang; di peramban tanpa dukungan, tombol tidak tampil.

### 4.10 Privasi

- **UJ-V1** 🤖 Selama alur lengkap (Mulai → Berkarya), daftar kunci `localStorage` hanya `neraca-warga:v1`, dan isinya tidak memuat nama yang diketik di L0.
- **UJ-V2** 🤖 Tidak ada cookie yang dibuat (`document.cookie === ""`).
- **UJ-V3** 🤖 CSP aktif: menyuntikkan `<script>` *inline* lewat konsol di halaman uji gagal dieksekusi (pelanggaran CSP tercatat).

## 5. Uji aksesibilitas manual (agen, setiap fitur)

- [ ] Seluruh alur fitur bisa diselesaikan hanya dengan keyboard; urutan fokus logis; fokus tidak terjebak.
- [ ] Cincin fokus terlihat jelas di tema terang dan gelap.
- [ ] Pembaca layar (NVDA + Firefox atau TalkBack + Chrome): nama, peran, dan keadaan kontrol terbaca; pengumuman hasil tidak berulang.
- [ ] Zoom 200% dan lebar 320 px: tidak ada konten terpotong.
- [ ] *Forced colors*: kartu, tombol, kolom, dan fokus tetap terlihat.
- [ ] Gerak berkurang: tidak ada gerak spasial; keadaan akhir benar.
- [ ] Tidak ada informasi yang hanya disampaikan lewat warna.
- [ ] Target sentuh ≥ 44 px pada emulasi layar sentuh.

## 6. Verifikasi konten oleh YAN

1. Agen jalur B menyiapkan `docs/laporan/verifikasi-konten.md`: tabel butir `[DRAF]`, `[VERIFIKASI-PASAL]`, dan `[DIISI-YAN]` dengan kolom *Lokasi*, *Isi usulan*, *Keputusan YAN* (Setuju / Ubah / Hapus), dan *Catatan*.
2. YAN mengisi keputusan, termasuk **ringkasan video** dan identitas di halaman Tentang.
3. Agen menerapkan keputusan dan mengubah status butir menjadi `disetujui`.
4. Sebelum rilis v1.0, YAN memeriksa Checklist Keselarasan (02 §14) langsung di situs (bukan di dokumen).

## 7. Uji coba kelas terbatas (kepraktisan)

- **Waktu:** setelah v0.8, satu sesi 40–80 menit.
- **Peserta:** 5–10 siswa kelas IX dengan perangkat beragam, ditambah satu guru atau YAN sebagai pengamat.
- **Tugas:** Mulai → Amati → satu LKPD berkelompok → Uji → Renungkan.
- **Amati dan catat:** waktu menyelesaikan LKPD, hambatan teknis, bagian yang membingungkan, interaksi yang paling disukai.
- **Angket respons siswa** `[DRAF]` (skala 1 = sangat tidak setuju … 4 = sangat setuju):
  1. Tampilan situs ini menarik.
  2. Tulisan di situs ini mudah dibaca.
  3. Aku tahu apa yang harus kulakukan di setiap halaman.
  4. Permainan dan kuis membantuku memahami hak dan kewajiban.
  5. Petunjuk LKPD membantuku menganalisis kasus.
  6. Situs ini berjalan lancar di perangkatku.
  7. Umpan balik setelah menjawab membantuku belajar.
  8. Aku merasa nyaman belajar topik perundungan dengan situs ini.
  9. Aku ingin memakai situs seperti ini lagi.
  10. Aku bisa menjelaskan mengapa hak dan kewajiban harus seimbang.
- **Analisis:** rata-rata per butir dan keseluruhan. Target keseluruhan ≥ 3,0. Butir dengan rata-rata < 2,5 menjadi prioritas perbaikan di NW-12.
- **Etika:** tanpa nama pada angket; siswa boleh tidak ikut; tidak ada pertanyaan tentang pengalaman pribadi perundungan.

## 8. Format laporan uji (`docs/laporan/NW-xx-uji.md`)

```markdown
# Laporan Uji NW-xx — {nama fitur}
Tanggal: … · Versi: … · Penguji: agen jalur …

## Ringkasan
Lulus/Tidak lulus, satu paragraf dalam bahasa sederhana.

## Hasil otomatis
| Kode | Hasil | Catatan |
(AU-01 … AU-08 yang relevan)

## Skenario penerimaan
| Kode | Hasil | Bukti (nama berkas tangkapan layar) |

## Uji manual aksesibilitas
Ceklis §5 dengan catatan.

## Masalah yang ditemukan
| No | Uraian | Tingkat | Status |

## Modern Web Guidance
- **`id-panduan`**: pilihan penting dan jebakan yang dicegah ("kutipan pendek aturan").
```

## 9. Kriteria lulus rilis 1.0

- [ ] Semua AU-01 s.d. AU-09 lulus; AU-10 ≥ 90 untuk halaman kunci.
- [ ] Semua skenario UJ bertanda 🤖 lulus di Chromium; UJ-G1–G3, UJ-S2, UJ-U1 juga lulus di Firefox dan WebKit.
- [ ] Uji perangkat D4 dan D6 lulus tanpa hambatan berat.
- [ ] Uji kelas: rata-rata angket ≥ 3,0; ≥ 80% siswa menyelesaikan satu LKPD tanpa bantuan teknis.
- [ ] Semua butir verifikasi konten diputuskan YAN; Checklist Keselarasan lengkap.
- [ ] YAN menyetujui rilis di `docs/laporan/rilis-1.0.md`.
