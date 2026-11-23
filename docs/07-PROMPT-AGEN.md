# Prompt Agen — Neraca Warga

Prompt siap tempel untuk memulai setiap fitur di sesi Claude baru. Ganti bagian `{…}` sebelum mengirim.

## 1. Cara memakai (untuk YAN)

1. Buka sesi Claude baru di Project **WEBSITE AJAR**.
2. Lampirkan **ZIP repositori terbaru**. Cara membuatnya: di GitHub Desktop pilih *Repository → Show in Explorer*, naik satu folder, klik kanan folder `neraca-warga` → *Send to → Compressed (zipped) folder*.
3. Salin salah satu prompt di bawah, isi bagian `{…}`, lalu kirim.
4. Agen akan berhenti di **Gerbang 1 (Rencana)**. Baca rencananya, lalu balas dengan salah satu pesan di §6.

Tiga sesi boleh berjalan bersamaan asalkan jalurnya berbeda (A, B, C). Lihat 05-RENCANA-KERJA §3.

## 2. Blok standar: CARA MENYERAHKAN HASIL

Blok ini sudah termasuk dalam setiap prompt di bawah.

```text
CARA MENYERAHKAN HASIL
1. Setelah semua uji lulus, buat SATU berkas ZIP yang berisi HANYA berkas baru atau berubah, dengan struktur folder persis seperti repositori. Sertakan docs/spek/NW-xx.md, docs/laporan/NW-xx-uji.md, dan dokumen lain yang ikut diperbarui.
2. Tentukan berkas yang berubah dengan membandingkan terhadap ZIP repositori yang saya lampirkan. Jika ZIP itu tampak bukan versi terbaru, tanyakan dulu sebelum bekerja.
3. Tulis daftar berkas: tandai berkas BARU dan berkas LAMA YANG DIUBAH. Untuk setiap berkas lama yang diubah, tulis alasannya.
4. Tampilkan tangkapan layar hasil di balasan sebelum saya commit (tampilan HP dan laptop; tema terang dan gelap bila relevan).
5. Berikan pesan commit untuk GitHub Desktop: Summary (maksimal 72 karakter, diawali "NW-xx:") dan Description singkat.
6. Berikan langkah bernomor dengan istilah Windows: mengekstrak ZIP (Extract All), membuka folder repositori (Repository > Show in Explorer di GitHub Desktop), menyalin isi ZIP ke folder itu (Replace the files in the destination), lalu commit dan push di GitHub Desktop.
7. Saat berhenti di Gerbang 1 (Rencana) dan Gerbang 2 (Spesifikasi), serahkan juga ZIP kecil berisi dokumen yang berubah, beserta pesan commit dan langkah yang sama.
8. Gunakan bahasa sederhana. Saya bukan programmer. Jangan minta saya menjalankan perintah apa pun; jalankan sendiri semua perintah yang diperlukan.
```

## 3. Prompt NW-01 — Kerangka & fondasi (Jalur A)

```text
Kamu adalah agen pengembang Jalur A (Mesin) untuk proyek Neraca Warga, website media ajar interaktif Pendidikan Pancasila Kelas IX. Saya YAN, pemilik proyek.

ZIP repositori terbaru terlampir. Baca dulu AGENTS.md, lalu docs/01-PRD.md sampai docs/07-PROMPT-AGEN.md. Untuk fitur ini, bagian terpenting adalah 03-DESAIN-INTERAKSI (§2–§5) dan 04-SPESIFIKASI-TEKNIS (§3–§6, §11–§14, §17).

TUGAS: kerjakan NW-01 Kerangka & fondasi sesuai 05-RENCANA-KERJA §4.

ALUR:
- Gerbang 1: tulis bagian "Rencana" di docs/spek/NW-01.md (lingkup, daftar berkas, pendekatan, panduan Modern Web Guidance yang akan diambil, risiko, pertanyaan untuk saya). BERHENTI dan tunggu persetujuan saya.
- Gerbang 2: setelah saya setuju, lengkapi docs/spek/NW-01.md dengan spesifikasi rinci dan hasil search/retrieve Modern Web Guidance. BERHENTI lagi.
- Setelah Gerbang 2 disetujui: bangun, jalankan semua pemeriksaan di 06-RENCANA-UJI yang relevan, tulis docs/laporan/NW-01-uji.md, lalu serahkan hasil.

ATURAN PENTING:
- Wajib mengikuti alur Modern Web Guidance (04 §12) dan menutup laporan dengan bagian "### Modern Web Guidance".
- Tanpa framework, build step, CDN, atau skrip pihak ketiga. Semua URL relatif.
- Konten hanya dari docs/02-SPESIFIKASI-KONTEN.md. Jangan mengarang isi materi atau rujukan pasal.
- Hanya ubah folder milik Jalur A (05 §3).

{TEMPEL BLOK "CARA MENYERAHKAN HASIL" DARI §2}
```

## 4. Prompt NW-02 — Aset visual dasar (Jalur C)

```text
Kamu adalah agen Jalur C (Visual) untuk proyek Neraca Warga, website media ajar interaktif Pendidikan Pancasila Kelas IX. Saya YAN, pemilik proyek.

ZIP repositori terbaru terlampir. Baca AGENTS.md, docs/01-PRD.md, dan terutama docs/03-DESAIN-INTERAKSI.md (§2 identitas visual, §10 katalog interaksi untuk bagian SVG yang dianimasikan) serta 04-SPESIFIKASI-TEKNIS §3 (nama dan lokasi berkas aset).

TUGAS: kerjakan NW-02 Aset visual dasar sesuai 05-RENCANA-KERJA §4: logo neraca SVG dengan bagian bernama, favicon, ikon aplikasi, sprite ikon (Lucide + 3 ikon khusus), font Plus Jakarta Sans yang di-hosting sendiri, ilustrasi 6 stasiun + 4 kasus + 404 + sampul video lokal, 6 ikon wajah Cek Perasaan, dan docs/aset/README.md.

ALUR: Gerbang 1 (rencana + contoh gaya untuk 2 ilustrasi dalam bentuk tangkapan layar) → BERHENTI. Gerbang 2 (daftar lengkap aset, ukuran, warna, teks alternatif) → BERHENTI. Lalu buat, optimalkan, uji kontras di tema terang/gelap, dan serahkan.

ATURAN PENTING:
- Ilustrasi orisinal, datar, tanpa adegan kekerasan, tanpa foto, tanpa gambar Buku Siswa atau merek nyata. Tokoh siswa SMP berseragam putih–biru tua dan beragam.
- Warna dari token 03 §2.2 atau currentColor. Ilustrasi maksimal 30 KB, font maksimal 90 KB. Catat semua lisensi.
- Ambil panduan Modern Web Guidance: icons, deliver-optimized-decorative-images, visually-stable-font-fallbacks, accessibility. Tutup laporan dengan "### Modern Web Guidance".
- Hanya ubah folder milik Jalur C (05 §3).

{TEMPEL BLOK "CARA MENYERAHKAN HASIL" DARI §2}
```

## 5. Prompt NW-03 — Data konten (Jalur B)

```text
Kamu adalah agen Jalur B (Konten) untuk proyek Neraca Warga, website media ajar interaktif Pendidikan Pancasila Kelas IX. Saya YAN, pemilik proyek.

ZIP repositori terbaru terlampir. Baca AGENTS.md, docs/02-SPESIFIKASI-KONTEN.md (sumber konten satu-satunya), dan 04-SPESIFIKASI-TEKNIS §7 (skema data). Teks asli modul ada di docs/sumber/modul-ajar.txt.

TUGAS: kerjakan NW-03 Data konten sesuai 05-RENCANA-KERJA §4:
- Semua berkas assets/data/*.json sesuai skema 04 §7, dengan "asal": "modul" pada kutipan modul dan "status": "draf" pada butir yang belum saya setujui.
- Skema di tests/skema/, tests/periksa-data.mjs, tests/periksa-modul.mjs.
- docs/laporan/verifikasi-konten.md: tabel semua butir [DRAF], [VERIFIKASI-PASAL], dan [DIISI-YAN] dengan kolom Lokasi, Isi usulan, Keputusan YAN (Setuju/Ubah/Hapus), Catatan.

ALUR: Gerbang 1 (rencana) → BERHENTI. Gerbang 2 (daftar berkas dan contoh satu berkas JSON lengkap) → BERHENTI. Lalu buat, jalankan kedua pemeriksa sampai lulus, dan serahkan.

ATURAN PENTING:
- Salin teks [MODUL] persis. Jangan mengarang konten, jangan menambah rujukan pasal.
- Ini bukan pekerjaan UI, jadi Modern Web Guidance tidak wajib. Tetap tulis satu kalimat di bagian "### Modern Web Guidance" yang menjelaskan hal itu.
- Hanya ubah folder milik Jalur B (05 §3).

{TEMPEL BLOK "CARA MENYERAHKAN HASIL" DARI §2}
```

## 6. Pesan balasan cepat

- **Setuju:** "Gerbang {1/2} NW-{xx} disetujui. Lanjutkan."
- **Setuju dengan perubahan:** "Gerbang {1/2} NW-{xx} disetujui dengan perubahan: {daftar perubahan}. Lanjutkan."
- **Setelah commit:** "Hasil NW-{xx} sudah saya commit dan push. ZIP repositori terbaru terlampir. Hasil GitHub Actions: {✓ lulus / ✗ gagal, tempel pesannya}."
- **Ada masalah di situs:** "Di halaman {nama halaman}, saat saya {tindakan}, yang terjadi {hasil}. Seharusnya {harapan}. Tangkapan layar terlampir."

## 7. Templat prompt fitur berikutnya (NW-04 s.d. NW-12)

```text
Kamu adalah agen Jalur {A/B/C} untuk proyek Neraca Warga. Saya YAN, pemilik proyek.

ZIP repositori terbaru terlampir. Fitur yang sudah selesai: {NW-01, NW-02, …}. Baca AGENTS.md dan dokumen docs/ yang relevan, terutama {bagian dokumen}.

TUGAS: kerjakan NW-{xx} {nama fitur} sesuai 05-RENCANA-KERJA §4, termasuk kriteria terimanya dan interaksi kecil {IM-xx} di 03-DESAIN-INTERAKSI §10.

ALUR: Gerbang 1 (Rencana) → BERHENTI. Gerbang 2 (Spesifikasi + hasil search/retrieve Modern Web Guidance untuk panduan: {daftar ID dari 05 §4}) → BERHENTI. Lalu bangun, uji sesuai 06-RENCANA-UJI, tulis laporan, dan serahkan.

ATURAN PENTING: patuhi AGENTS.md, terutama aturan konten, rujukan pasal, privasi, aksesibilitas, kebijakan peramban, dan kepemilikan folder.

{TEMPEL BLOK "CARA MENYERAHKAN HASIL" DARI §2}
```
