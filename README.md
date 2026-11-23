# Neraca Warga

**Media ajar interaktif Pendidikan Pancasila Kelas IX**
Bab 2 Hak dan Kewajiban Warga Negara · Subbab D *Tantangan Pemenuhan Hak dan Kewajiban Warga Negara*

> *Seimbangkan hak dan kewajibanmu.*

Neraca Warga menghidupkan modul ajar menjadi website interaktif dengan enam stasiun belajar (Mulai, Amati, Selidiki, Uji, Renungkan, Berkarya), Ruang Baca, Glosarium, dan Mode Guru. Situs ini ringan, bisa dipakai tanpa internet setelah kunjungan pertama, tanpa akun, dan tanpa pelacakan.

## Status

**Gerbang 0: paket dokumen perencanaan.** Kode situs belum dibuat. Pembangunan dimulai dari fitur NW-01 (lihat `docs/05-RENCANA-KERJA.md`).

## Isi paket

| Berkas | Isi |
| --- | --- |
| `docs/01-PRD.md` | Tujuan, pengguna, keselarasan dengan modul, kebutuhan, ruang lingkup, **keputusan yang perlu dijawab YAN** (§14) |
| `docs/02-SPESIFIKASI-KONTEN.md` | Seluruh isi situs per halaman, dengan tanda asal (modul/draf/perlu verifikasi) |
| `docs/03-DESAIN-INTERAKSI.md` | Warna, huruf, tata letak, komponen, katalog 27 interaksi kecil, wireframe teks |
| `docs/04-SPESIFIKASI-TEKNIS.md` | Arsitektur, struktur berkas, skema data, luring, kebijakan peramban, alur *Modern Web Guidance* |
| `docs/05-RENCANA-KERJA.md` | Fitur NW-01 s.d. NW-12, gerbang persetujuan, tiga jalur paralel, kriteria terima |
| `docs/06-RENCANA-UJI.md` | Uji otomatis, skenario uji, uji kelas, format laporan |
| `docs/07-PROMPT-AGEN.md` | Prompt siap tempel untuk memulai setiap fitur |
| `docs/sumber/` | Modul ajar asli (PDF) dan teksnya untuk pemeriksaan otomatis |
| `AGENTS.md`, `CLAUDE.md` | Aturan kerja untuk agen pengembang |

## Langkah memasukkan paket ini ke GitHub (GitHub Desktop, Windows)

1. Klik kanan berkas ZIP paket ini → **Extract All…** → **Extract**.
2. Buka **GitHub Desktop** → **File → New repository…**
   - *Name*: `neraca-warga`
   - *Description*: `Media ajar interaktif Pendidikan Pancasila Kelas IX`
   - *Local path*: pilih folder tempat kamu menyimpan proyek
   - **Jangan** centang *Initialize this repository with a README*; *Git ignore* dan *License*: **None**
   - Klik **Create repository**.
3. Di GitHub Desktop pilih **Repository → Show in Explorer**. Salin **seluruh isi** folder hasil ekstrak (README.md, AGENTS.md, CLAUDE.md, folder `docs`) ke folder yang terbuka.
4. Kembali ke GitHub Desktop. Di kolom *Summary* tulis `Gerbang 0: paket dokumen perencanaan Neraca Warga`, lalu klik **Commit to main**.
5. Klik **Publish repository**. Hapus centang **Keep this code private** (GitHub Pages gratis membutuhkan repositori publik), lalu klik **Publish repository**.
6. GitHub Pages **belum** perlu diaktifkan. Langkahnya ada di `docs/04-SPESIFIKASI-TEKNIS.md` §16 dan dilakukan setelah NW-01 selesai.

> Catatan: karena repositori publik, isi `docs/sumber/` (PDF modul) juga dapat dilihat orang lain. Jika tidak menginginkannya, jangan salin folder `docs/sumber` sebelum *commit*.

## Memulai pembangunan

1. Jawab keputusan terbuka di `docs/01-PRD.md` §14 (cukup tulis jawaban di sesi Claude berikutnya).
2. Buka `docs/07-PROMPT-AGEN.md`, salin prompt **NW-01**, lampirkan ZIP repositori terbaru, lalu kirim ke sesi Claude baru.
3. Bila ingin bekerja paralel, jalankan juga prompt **NW-02** (visual) dan **NW-03** (konten) di sesi lain.

## Kredit

- Penyusun modul dan pengembang media: I Wayan Gede Griyawana.
- Sumber utama: Modul Ajar Pendidikan Pancasila Kelas IX *Tantangan Pemenuhan Hak dan Kewajiban Warga Negara* dan Buku Siswa Pendidikan Pancasila untuk SMP/MTs Kelas IX (Prahara dkk., 2023).
- Praktik web mengikuti [Modern Web Guidance](https://github.com/GoogleChrome/modern-web-guidance).
- Rencana lisensi: kode MIT; teks dan ilustrasi CC BY-NC-SA 4.0; font SIL OFL 1.1; ikon Lucide ISC (menunggu keputusan YAN, PRD K-10).
