# AGENTS.md — Aturan kerja agen untuk Neraca Warga

Neraca Warga adalah website media ajar interaktif Pendidikan Pancasila Kelas IX, subbab *Tantangan Pemenuhan Hak dan Kewajiban Warga Negara*. Pemilik proyek: **YAN** (I Wayan Gede Griyawana). Situs statis, di-*hosting* di GitHub Pages.

## 1. Urutan membaca

1. `AGENTS.md` (berkas ini)
2. `docs/01-PRD.md`: apa dan mengapa
3. `docs/02-SPESIFIKASI-KONTEN.md`: **satu-satunya sumber konten**
4. `docs/03-DESAIN-INTERAKSI.md`: tampilan, komponen, katalog interaksi kecil (IM-xx)
5. `docs/04-SPESIFIKASI-TEKNIS.md`: arsitektur, data, kebijakan peramban, alur Modern Web Guidance
6. `docs/05-RENCANA-KERJA.md`: fitur NW-xx, gerbang, jalur paralel, kriteria terima
7. `docs/06-RENCANA-UJI.md`: uji otomatis, skenario, format laporan
8. `docs/spek/NW-xx.md` dan `docs/laporan/`: hasil kerja fitur sebelumnya

## 2. Aturan mutlak

1. **Bahasa.** Antarmuka situs dan dokumen berbahasa Indonesia. Laporan kepada YAN memakai bahasa sederhana.
2. **YAN bukan programmer.** Jangan pernah meminta YAN menjalankan perintah, membuka terminal, atau menyunting kode. Agen menjalankan sendiri semua perintah. YAN hanya memakai GitHub Desktop (Windows) dan antarmuka web GitHub.
3. **Konten.** Semua isi materi berasal dari `docs/02-SPESIFIKASI-KONTEN.md`. Teks `[MODUL]` disalin persis dan elemennya diberi `data-asal="modul"`. Jangan mengarang materi, data, kutipan, atau contoh baru. Bila butuh teks baru, tandai `[DRAF]` dan laporkan.
4. **Rujukan pasal.** Hanya YAN yang memutuskan penambahan atau perubahan rujukan pasal. Rujukan di luar modul berstatus `draf` dan tidak tampil sebelum disetujui.
5. **Modern Web Guidance wajib** untuk setiap pekerjaan HTML/CSS/JS sisi klien: *search* → *retrieve* → terapkan → ungkapkan di bagian `### Modern Web Guidance` pada laporan (04 §12).
6. **Kebijakan peramban.** Fungsi inti hanya memakai fitur *Baseline Widely available*. Fitur lebih baru hanya sebagai peningkatan progresif dengan cadangan (04 §11).
7. **Tanpa** *framework*, *build step*, CDN, pustaka *runtime*, analitik, cookie, atau skrip pihak ketiga. Polifil Popover hanya dari `assets/vendor/` dan dimuat bersyarat.
8. **URL relatif** di semua tempat (situs berada di subjalur `/neraca-warga/`).
9. **Privasi.** Jangan pernah menyimpan nama siswa/anggota kelompok, kelas, pilihan Cek Perasaan, atau masukan kalkulator nilai. Data lain hanya di `localStorage` kunci `neraca-warga:v1`.
10. **Aksesibilitas.** Target WCAG 2.2 AA: elemen asli lebih dulu, fokus terlihat, keyboard penuh, target sentuh 44 px di layar sentuh, tidak bergantung pada warna, satu *live region* per halaman.
11. **Gerak.** Gerak spasial hanya di `prefers-reduced-motion: no-preference`. Tidak ada animasi otomatis > 5 detik tanpa tombol jeda. Tidak ada kedip > 3 kali per detik.
12. **Keamanan.** Patuhi CSP di templat (04 §4): tanpa `<style>`, atribut `style`, skrip *inline*, atau `onclick`. Teks dari siswa hanya lewat `textContent`.
13. **Kepemilikan folder.** Ubah hanya folder milik jalurmu (05 §3). Temuan di folder jalur lain dicatat, tidak diperbaiki sendiri.
14. **Keselamatan konten.** Tanpa gambar kekerasan atau foto siswa. Jangan meminta siswa menulis pengalaman pribadi sebagai korban. Kotak *Butuh bantuan?* tetap ada di halaman yang ditentukan.

## 3. Alur kerja per fitur

Gerbang 1 (Rencana) → berhenti → Gerbang 2 (Spesifikasi) → berhenti → Bangun → Uji → Serah terima. Rincian di `docs/05-RENCANA-KERJA.md` §1. Jangan melompati gerbang kecuali YAN mengizinkan secara tertulis.

## 4. *Definition of Done*

Lihat `docs/05-RENCANA-KERJA.md` §6. Ringkasnya: kriteria terima terpenuhi, CI hijau, uji keyboard/gerak berkurang/tema gelap/320 px dilakukan, tanpa konten atau pasal baru yang belum disetujui, dokumen diperbarui, dan laporan memuat bagian Modern Web Guidance.

## 5. Perintah yang dijalankan agen (bukan YAN)

```bash
npm ci                                   # pasang alat uji
npm run periksa                          # html-validate + kerangka + data + konten (+ sw)
npx playwright test                      # uji asap, skenario, axe
npx -y modern-web-guidance@latest search "<kueri>" --skill-version 2026_11_16-268fb9ea
npx -y modern-web-guidance@latest retrieve "<id>"
```

Untuk melihat situs secara lokal, jalankan server statis apa pun dari akar repositori. Jangan memasang alat global di komputer YAN.

## 6. Cara menyerahkan hasil

1. Setelah semua uji lulus, buat **satu ZIP** yang berisi **hanya berkas baru atau berubah**, dengan struktur folder persis seperti repositori. Sertakan `docs/spek/NW-xx.md`, `docs/laporan/NW-xx-uji.md`, dan dokumen lain yang ikut diperbarui.
2. Tentukan berkas yang berubah dengan membandingkan terhadap ZIP repositori yang dilampirkan YAN. Jika ZIP tampak bukan versi terbaru, **tanyakan dulu** sebelum bekerja.
3. Tulis daftar berkas: tandai **baru** dan **lama yang diubah**. Untuk setiap berkas lama yang diubah, sebutkan alasannya.
4. Tampilkan **tangkapan layar** hasil di balasan sebelum YAN meng-*commit* (HP dan laptop; terang dan gelap bila relevan).
5. Berikan **pesan commit** untuk GitHub Desktop: *Summary* ≤ 72 karakter diawali `NW-xx:` dan *Description* singkat.
6. Berikan **langkah bernomor** berbahasa sederhana dengan istilah Windows: *Extract All*, *Repository → Show in Explorer*, salin isi ZIP (*Replace the files in the destination*), lalu *Commit to main* dan *Push origin*.
7. Saat berhenti di **Gerbang 1** dan **Gerbang 2**, serahkan juga ZIP kecil berisi dokumen yang berubah, beserta pesan *commit* dan langkah yang sama.
8. Bila GitHub Actions gagal setelah *push*, YAN akan menempelkan pesannya. Perbaiki dan serahkan ulang dengan cara yang sama.
