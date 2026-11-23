# Desain & Interaksi — Neraca Warga

Dokumen ini menetapkan tampilan, tata letak, komponen, gerak, dan **katalog interaksi kecil**. Setiap komponen mencantumkan ID panduan *Modern Web Guidance* (MWG) yang wajib diambil agen sebelum membangunnya (lihat 04-SPESIFIKASI-TEKNIS §12 dan AGENTS.md).

## 1. Prinsip desain

1. **Konten dulu.** Siswa datang untuk belajar. Bingkai halaman kecil, tidak ada *pop-up* saat halaman dibuka, dan konten tidak bergeser ketika dibaca. (MWG: `content-first-noise-reduction`)
2. **Tenang tetapi hidup.** Selaras dengan prinsip *berkesadaran* dan *menggembirakan*: gerak singkat, lembut, dan selalu menjawab tindakan siswa. Tidak ada animasi yang berjalan sendiri lebih dari 5 detik tanpa tombol jeda. (MWG: `motion`)
3. **Seimbang.** Metafora neraca menyatukan identitas visual dan interaksi. Hak dan kewajiban selalu tampil sebagai pasangan.
4. **Inklusif dan aman.** Dapat dipakai dengan sentuhan, mouse, keyboard, dan pembaca layar. Tidak bergantung pada warna saja. Topik sensitif disajikan dengan hormat. (MWG: `accessibility`, `color`)
5. **Ringan dan tahan luring.** Ilustrasi SVG, satu keluarga huruf, tanpa pustaka pihak ketiga. (MWG: `performance`)

## 2. Identitas visual

### 2.1 Sistem warna bermakna

Warna mengikuti aturan tangan pada *ice breaking* modul: **tangan kanan = hak**, **tangan kiri = kewajiban**, **kedua tangan = keduanya**.

| Makna | Warna | Posisi tetap | Ikon pendamping (wajib, karena warna tidak boleh sendirian) |
| --- | --- | --- | --- |
| Hak | Biru | Kanan (piringan kanan neraca, tombol kanan) | Perisai (hak yang dilindungi) |
| Kewajiban | Jingga | Kiri (piringan kiri neraca, tombol kiri) | Tangan memberi |
| Keduanya / Seimbang (warna merek) | Toska | Tengah (tiang neraca, tombol tengah) | Neraca |

Biru dan jingga dipilih karena senada dengan palet modul cetak (biru tua dan jingga), sehingga situs terasa satu keluarga dengan modul. Posisi kiri/kanan untuk hak/kewajiban sengaja memakai properti fisik, tidak logis, karena terikat pada tangan (MWG `css`: "would I want this to flip in RTL?").

### 2.2 Token warna

Nilai kontras dihitung dengan rumus WCAG 2.x. Teks normal minimal 4,5:1; batas komponen UI minimal 3:1.

**Tema terang**

| Token | Nilai | Kontras pada kertas `#FBF8F3` | Catatan |
| --- | --- | --- | --- |
| `--warna-kertas` | `#FBF8F3` | — | Latar halaman (nuansa kertas) |
| `--warna-permukaan` | `#FFFFFF` | — | Kartu, dialog |
| `--warna-tinta` | `#1F2328` | 14,91 | Teks utama |
| `--warna-tinta-lembut` | `#57606A` | 6,03 | Teks sekunder |
| `--warna-garis` | `#7A838C` | 3,64 (3,85 pada putih) | Batas kolom isian, kartu interaktif |
| `--warna-garis-halus` | `#E4DED4` | dekoratif | Pemisah non-UI saja |
| `--warna-seimbang` | `#0E6B68` | 5,97 | Merek, tombol utama, "Keduanya"; teks putih 6,32 |
| `--warna-hak` | `#1F4FA3` | 7,33 | Teks putih 7,76 |
| `--warna-kewajiban` | `#A64B0A` | 5,46 | Teks putih 5,78 |
| `--warna-berhasil` | `#17763A` | 5,37 | Selalu dengan ikon centang |
| `--warna-bahaya` | `#B42318` | 6,21 | Selalu dengan ikon silang/peringatan |
| `--warna-peringatan` | `#8A5A00` | 5,59 | |
| `--warna-seimbang-muda` | `#E2F1EF` | latar | Teks toska di atasnya 5,44 |
| `--warna-hak-muda` | `#E7EEFB` | latar | Teks biru di atasnya 6,66 |
| `--warna-kewajiban-muda` | `#FCEFE3` | latar | Teks jingga di atasnya 5,12 |

**Tema gelap**

| Token | Nilai | Kontras pada kertas `#0F1720` | Catatan |
| --- | --- | --- | --- |
| `--warna-kertas` | `#0F1720` | — | |
| `--warna-permukaan` | `#17212B` | — | |
| `--warna-tinta` | `#E6EDF3` | 15,27 | |
| `--warna-tinta-lembut` | `#A8B3BF` | 8,48 | |
| `--warna-garis` | `#6E7A86` | 4,12 (3,72 pada permukaan) | |
| `--warna-garis-halus` | `#26323E` | dekoratif | |
| `--warna-seimbang` | `#5CC8C2` | 9,02 | Teks tombol `#0F1720` |
| `--warna-hak` | `#8DB5FF` | 8,75 | Teks tombol `#0F1720` |
| `--warna-kewajiban` | `#F6B26B` | 9,88 | Teks tombol `#0F1720` |
| `--warna-berhasil` | `#6FD08C` | 9,52 | |
| `--warna-bahaya` | `#FF8A80` | 7,90 | |
| `--warna-peringatan` | `#F2C35B` | 10,94 | |
| `--warna-seimbang-muda` | `#133332` | latar | |
| `--warna-hak-muda` | `#17263F` | latar | |
| `--warna-kewajiban-muda` | `#3A2614` | latar | |

Aturan penerapan:

- Deklarasikan `color-scheme: light dark` pada `:root` dan `<meta name="color-scheme" content="light dark">` di `<head>`. Token memakai `light-dark()` dengan cadangan sesuai panduan (MWG: `dark-mode`, `color`).
- Mode kontras tinggi Windows (*forced colors*): setiap kartu dan kolom isian **wajib** punya `border`, jangan hanya bayangan. Siapkan token cadangan kata kunci sistem (`CanvasText`, `ButtonText`, `Highlight`) di `@media (forced-colors: active)`.
- `accent-color: var(--warna-seimbang)` untuk kotak centang, radio, dan *slider* bawaan.
- `theme-color` dua nilai (terang `#FBF8F3`, gelap `#0F1720`) lewat `<meta name="theme-color" media="(prefers-color-scheme: …)">` (MWG: `browser-ui-theming`).

### 2.3 Tipografi

- **Huruf:** *Plus Jakarta Sans* (karya Tokotype, Jakarta; lisensi SIL OFL 1.1), versi variabel, di-*hosting* sendiri dalam format WOFF2 dengan *subset* Latin. Berat yang dipakai: 400, 600, 700, 800.
- **Cadangan:** `system-ui, "Segoe UI", Roboto, sans-serif` dengan `font-size-adjust` agar tinggi-x stabil saat huruf web dimuat (MWG: `visually-stable-font-fallbacks`).
- **Ukuran:** semua dalam `rem`, tanpa `px`. Akar dokumen **tidak** diberi `font-size` (MWG: `typography`, `respect-os-text-scale`).

| Token | Nilai | Pemakaian |
| --- | --- | --- |
| `--teks-kecil` | `0.875rem` | Keterangan, sumber |
| `--teks-isi` | `1rem` | Paragraf (tidak boleh lebih kecil) |
| `--teks-pengantar` | `1.125rem` | Paragraf pembuka |
| `--judul-3` | `clamp(1.125rem, 1rem + 0.5vw, 1.375rem)` | H3 |
| `--judul-2` | `clamp(1.375rem, 1.1rem + 1.2vw, 1.875rem)` | H2 |
| `--judul-1` | `clamp(1.75rem, 1.2rem + 2.6vw, 3rem)` | H1 |
| `--tampilan` | `clamp(2rem, 1.2rem + 4vw, 4rem)` | Judul Beranda |
| `--proyektor` | `clamp(2.5rem, 1rem + 6vw, 6rem)` | Mode Guru (timer, pernyataan) |

Rasio maksimum/minimum setiap `clamp()` ≤ 2,5 agar zoom 200% tetap berfungsi (MWG: `typography`).

- `line-height: 1.5` untuk isi, `1.2` untuk judul (tanpa satuan).
- Lebar teks maksimum `65ch`.
- `text-wrap: balance` hanya pada H1–H3 dan judul kartu; `text-wrap: pretty` hanya pada paragraf bacaan. Jangan pada `*` (MWG: `improve-text-layout-and-legibility`).
- Penekanan memakai **tebal**, bukan HURUF KAPITAL. Rata kiri, tanpa *justify*.

### 2.4 Ruang, sudut, bayangan

| Token | Nilai |
| --- | --- |
| `--ruang-1` … `--ruang-8` | `0.25rem`, `0.5rem`, `0.75rem`, `1rem`, `1.5rem`, `2rem`, `3rem`, `4rem` |
| `--sudut-kecil` / `--sudut` / `--sudut-besar` / `--sudut-pil` | `0.5rem` / `0.75rem` / `1.25rem` / `999px` |
| `--bayangan-1` | `0 1px 2px rgb(0 0 0 / 0.06), 0 2px 8px rgb(0 0 0 / 0.06)` |
| `--bayangan-2` (angkat saat *hover*/tekan) | `0 4px 16px rgb(0 0 0 / 0.12)` |

`corner-shape: squircle` boleh dipakai sebagai peningkatan progresif (MWG: `css` §9).

### 2.5 Logo dan ilustrasi

- **Logo:** neraca sederhana. Piringan kiri jingga (kewajiban), piringan kanan biru (hak), tiang dan lengan toska. *Wordmark* "Neraca Warga" dengan Plus Jakarta Sans 800. SVG dibuat dengan bagian bernama (`#lengan`, `#piring-kiri`, `#piring-kanan`) agar dapat dianimasikan.
- **Ilustrasi:** SVG datar buatan sendiri, maksimal 3 warna token + netral. Warna memakai `currentColor` atau variabel CSS agar ikut tema gelap. Ukuran ≤ 30 KB per berkas.
- **Tokoh:** siswa SMP berseragam putih–biru tua, beragam (berjilbab, berkacamata, warna kulit beragam), ekspresif tetapi tidak karikatural.
- **Larangan:** adegan kekerasan, darah, senjata, foto siswa nyata, logo/merek nyata, gambar Buku Siswa.
- **Adegan per stasiun:** Mulai (siswa mengangkat tangan kanan/kiri), Amati (kaca pembesar di atas grafik), Selidiki (meja diskusi dengan LKPD), Uji (kartu soal dan centang), Renungkan (siswa duduk tenang), Berkarya (poster kampanye). Empat kasus: HP dengan gelembung komentar, gerbang dua sekolah, persimpangan jalan dengan helm, bukit hutan dan mata air.
- Ilustrasi dekoratif diberi `aria-hidden="true"`. Ilustrasi informatif diberi `role="img"` dan `<title>` (MWG: `accessibility` §6).

### 2.6 Ikon

- Set **Lucide** (lisensi ISC; berkas lisensi disertakan) ditambah tiga ikon khusus: hak (perisai), kewajiban (tangan memberi), neraca.
- Teknik: **SVG sprite dengan `<use>`** (`assets/ikon/sprite.svg`) yang mewarisi `currentColor`. Mesin ikon berbasis *container style queries* tidak dipakai karena fiturnya masih *Newly available* (MWG: `icons`).
- Tombol yang hanya berisi ikon wajib punya nama aksesibel. Ikon dekoratif diberi `aria-hidden="true"`.

## 3. Tata letak dan responsif

- **Mobile-first.** Satu kolom di bawah ±48rem. Dua kolom (konten + samping) mulai ±64rem untuk Ruang Baca dan LKPD (samping: daftar langkah atau Peta Pasal mini).
- Wadah halaman `max-inline-size: 72rem`; kolom teks `65ch`.
- Komponen menyesuaikan diri lewat **container queries**, bukan *media query* lebar layar. *Media query* hanya untuk jenis input (`pointer: coarse`) dan preferensi pengguna (MWG: `form-factor-adaptation`).
- Kisi kartu: `grid-template-columns: repeat(auto-fill, minmax(min(100%, 16rem), 1fr))`.
- Target sentuh: minimal 24×24 px, dan **44×44 px** pada `pointer: coarse` (MWG: `form-factor-adaptation`).
- Tidak ada pengguliran horizontal pada lebar 320 px. Tabel lebar boleh bergulir di wadahnya sendiri (`role="region"`, `tabindex="0"`, nama aksesibel) atau berubah menjadi tumpukan (MWG: `responsive-table`).
- `viewport-fit=cover` + `env(safe-area-inset-*)` untuk bilah bawah. `scroll-padding-bottom` setinggi bilah agar elemen terfokus tidak tertutup.

## 4. Navigasi

| Bagian | Perilaku | MWG |
| --- | --- | --- |
| Kepala halaman | *Sticky*, satu baris, tinggi < 12% layar. Berisi logo, tautan Jalur, Ruang Baca, Glosarium, tombol Menu. Peningkatan: tersembunyi saat menggulir turun lewat *scroll-state query* (tanpa skrip cadangan; bila tidak didukung, kepala tetap tampil) | `content-first-noise-reduction`, `navbar` |
| Menu (layar sempit) | Laci samping memakai `<dialog>` + `showModal()`; berisi tautan semua halaman, Mode Guru, Tentang, sakelar tema, Hapus data | `navigation-drawer` |
| Penanda stasiun | "Stasiun 3 dari 6" + enam titik berlabel; titik aktif memakai bentuk berbeda, tidak hanya warna | `accessibility` |
| Bilah bawah (layar sempit) | Tombol *Sebelumnya* / *Berikutnya*; aman dari *safe area* | `form-factor-adaptation` |
| Tautan lewati | "Lewati ke konten utama", tautan pertama di halaman | `accessibility` §1 |
| Halaman aktif | `aria-current="page"` + garis bawah tebal | `navbar` |

## 5. Komponen

| Komponen | Ketentuan utama | MWG |
| --- | --- | --- |
| Tombol | `<button>` untuk aksi, `<a>` untuk pindah halaman. Keadaan *hover*, tekan (`scale: 0.97`), fokus (`outline` 3px, `outline-offset` 3px) tampak berbeda. Tidak memakai `disabled` bila fokus harus tetap, gunakan `aria-disabled` | `natural-interactions`, `accessibility` |
| Kartu stasiun/kasus | Satu tautan tujuan; seluruh kartu dapat diketuk tanpa merusak semantik; status progres berupa teks + ikon | `card` |
| *Chip* pilihan | Kotak centang asli dalam `<label>` bergaya *chip* (`label:has(:checked)`), dikelompokkan `<fieldset>` + `<legend>` | `checkbox`, `forms` |
| Dialog | `<dialog>` + `showModal()`; tutup dengan `<form method="dialog">`; tanpa `role="dialog"`, tanpa *focus trap* buatan; `closedby="any"` sebagai peningkatan; cegah gulir latar dengan CSS panduan | `dialog`, `animate-to-from-top-layer`, `prevent-page-scroll-under-modal-dialog`, `light-dismiss-a-dialog` |
| Definisi istilah | Tombol istilah membuka `popover="auto"` via `popovertarget`; di layar sempit tampil sebagai lembar bawah, di layar lebar sebagai kartu tengah (tanpa *anchor positioning*). Berisi istilah, definisi, tautan ke glosarium | `interest-triggered-tooltips` (bagian *toggletip*), `content-first-noise-reduction` |
| Notifikasi (*toast*) | `popover="manual"`; hanya untuk lencana dan pembaruan versi; isinya juga tersedia di tempat lain; tidak muncul saat dialog modal terbuka | `persistent-toast-notifications` |
| Status simpan | Teks kecil "Tersimpan di perangkat ini" dalam satu `role="status"` per halaman, dengan *debounce* | `accessibility` §8 |
| Akordeon | `<details>`/`<summary>`, tanpa judul di dalam `summary`; eksklusif dengan atribut `name` sebagai peningkatan; animasi buka lewat `::details-content` sebagai peningkatan | `accordion`, `animate-to-intrinsic-sizes` |
| Bilah progres | `<progress>` bergaya kustom; label teks di dekatnya | `progress` |
| Cincin progres | Untuk timer dan ringkasan progres; `@property` sebagai peningkatan | `progress-ring` |
| *Slider* tebakan | `<input type="range">` asli dengan label dan nilai tampil | `slider` |
| Langkah LKPD | Daftar `<ol>` langkah + satu `<section>` aktif; fokus pindah ke judul langkah saat berganti | `html` §6, `accessibility` |
| Kolom isian | Label di atas; petunjuk di atas kolom dan dihubungkan `aria-describedby`; validasi muncul setelah interaksi (`:user-invalid`); `field-sizing: content` sebagai peningkatan dengan cadangan `rows="4"` | `forms`, `validate-input-after-interaction`, `form-fields-automatically-fit-contents`, `accessible-error-announcement` |
| Tabel | `<caption>`, `<th scope>`; tumpuk di layar sempit | `responsive-table`, `accessibility` |
| Grafik batang | HTML/CSS (bukan *canvas*), dalam `<figure>` + `<figcaption>` + tabel data alternatif di `<details>` | `accessibility` §6 |
| Tombol salin | Ikon berganti ke centang + gelembung "Disalin!" yang juga menjadi *live region*; tidak dinonaktifkan saat umpan balik | `copy-button` |
| Sakelar tema | Tiga status: Otomatis / Terang / Gelap; disimpan; tanpa kedip tema saat dimuat | `dark-mode-toggle` |
| Indikator progres baca | Bilah tipis di atas halaman Ruang Baca, dekoratif, hanya bila *scroll-driven animations* didukung | `scroll-progress-indicator` |

## 6. Gerak

### 6.1 Token

| Token | Nilai | Pemakaian |
| --- | --- | --- |
| `--durasi-cepat` | `120ms` | Warna, tekan tombol |
| `--durasi` | `200ms` | Muncul/hilang komponen |
| `--durasi-lambat` | `320ms` | Kartu permainan, dialog |
| `--durasi-grafik` | `600ms` | Batang grafik tumbuh |
| `--ease-keluar` | `cubic-bezier(0.2, 0.8, 0.2, 1)` | Umum |

Kurva pegas ditulis **langsung** di deklarasi, didahului cadangan kata kunci, dan **tidak** lewat variabel CSS (MWG: `natural-interactions`, `physics-based-easing`):

```css
.token-jatuh {
  animation: jatuh var(--durasi-lambat) ease-out both;
  animation: jatuh var(--durasi-lambat) linear(0, 0.45 15%, 1.08 35%, 0.97 55%, 1.01 75%, 1) both;
}
```

### 6.2 Aturan

1. Animasikan hanya `transform` (lebih disukai properti individual `translate`, `rotate`, `scale`) dan `opacity` (MWG: `motion`, `individual-transform-properties`).
2. Gerak spasial hanya aktif di dalam `@media (prefers-reduced-motion: no-preference)`. Perubahan warna dan opasitas boleh tetap ada. **Jangan** memakai `animation-duration: 0.01ms` global (MWG: `motion`).
3. Saat gerak dimatikan, elemen tetap berakhir di keadaan akhirnya. Kode yang menunggu `animationend` harus tetap melanjutkan bila `getAnimations()` kosong.
4. Tidak ada kedip lebih dari 3 kali per detik, dalam kondisi apa pun.
5. Animasi yang berjalan lebih dari 5 detik (napas STOP, timer) hanya mulai setelah diketuk dan selalu punya tombol jeda.
6. Masuk/keluar komponen memakai `@starting-style` + `transition-behavior: allow-discrete` (ditulis terpisah dari *shorthand*) + `overlay` untuk lapisan atas (MWG: `animate-element-entry-exit`, `animate-to-from-top-layer`).
7. Transisi antarhalaman memakai *cross-document view transitions*, hanya dalam `no-preference`; arah **maju** (ke stasiun berikutnya) bergeser ke kiri, **mundur** bergeser ke kanan (MWG: `cross-document-transitions`, `directional-navigation-transitions`, `consistent-cross-document-transitions`).

## 7. Suara dan getar

Versi 1.0 tidak memakai suara. Opsi suara (P2) bawaannya mati dan hanya untuk Mode Guru (bunyi lembut saat timer habis). Getar perangkat tidak dipakai.

## 8. Mode proyektor (Mode Guru)

- Tombol **Tampilan proyektor** menambah kelas `mode-proyektor` pada `<html>`. Huruf memakai `--proyektor`, kontras dinaikkan (teks `--warna-tinta` di atas `--warna-permukaan`), dan semua elemen dekoratif disembunyikan.
- Timer terbaca dari belakang kelas: angka minimal setinggi `--proyektor`.
- Dapat dikendalikan dengan keyboard: `Spasi` mulai/jeda timer, `→` segmen berikutnya, `←` segmen sebelumnya. Pintasan hanya aktif saat fokus tidak berada di kolom isian dan diumumkan di bantuan layar.

## 9. Cetak

`assets/css/cetak.css` dimuat dengan `media="print"` (MWG: `performance`: pisahkan CSS lewat atribut `media`).

- Sembunyikan navigasi, tombol, ilustrasi dekoratif, dan bilah.
- Ukuran isi 11–12 pt, A4, margin 2 cm, kepala cetak: "Neraca Warga · LKPD {n} · Kelompok …".
- **LKPD kosong:** teks kasus + pertanyaan + garis jawaban.
- **LKPD terisi (Ringkasan):** jawaban kelompok + pasal + upaya + evaluasi.
- Soal kuis tanpa kunci (versi siswa) dan dengan kunci (versi guru).
- Rubrik dalam tabel penuh.
- Hindari pemenggalan di tengah kartu/tabel (`break-inside: avoid`).

## 10. Katalog interaksi kecil

Kolom **Gerak berkurang** menjelaskan perilaku saat `prefers-reduced-motion: reduce`.

| ID | Interaksi & tempat | Pemicu → respons | Aksesibilitas | Gerak berkurang | MWG | P |
| --- | --- | --- | --- | --- | --- | --- |
| IM-01 | **Umpan balik tombol** (semua tombol & kartu) | *Hover*: bayangan naik; tekan: `scale 0.97`; fokus: cincin `outline`. Kombinasi keadaan tetap terbedakan | Cincin fokus kontras ≥ 3:1; tidak bergantung *hover* | Tanpa `scale`; warna tetap | `natural-interactions` | P0 |
| IM-02 | **Neraca Beranda** | Ketuk/arahkan ke salah satu piringan → lengan miring ±6° ke arah itu lalu kembali seimbang dengan kurva pegas; label "Hak" atau "Kewajiban" muncul di bawah piringan | Tombol dengan nama "Miringkan ke hak" / "Miringkan ke kewajiban"; dapat dengan keyboard | Lengan tidak berputar; hanya label muncul | `physics-based-easing`, `individual-transform-properties` | P1 |
| IM-03 | **Cek Perasaan** (Mulai) | Pilih wajah → wajah membesar sedikit dengan pegas, respons muncul pelan di bawah | Grup radio asli; respons di `role="status"` | Tanpa membesar; respons langsung | `forms`, `physics-based-easing` | P0 |
| IM-04 | **Kartu Hak atau Kewajiban?** (Mulai) | Pilih tombol → kartu meluncur ke arah pilihan (kanan = hak, kiri = kewajiban, atas = keduanya), token jatuh ke piringan, kartu berikutnya masuk. Benar: ikon centang + warna; belum tepat: ikon info + penjelasan. Opsional (P2): geser kartu ke kanan/kiri dengan `touch-action: pan-y` | Tiga `<button>` selalu ada; hasil diumumkan lewat `role="status"`; fokus kembali ke kartu baru | Kartu berganti tanpa meluncur; token muncul tanpa jatuh | `animate-element-entry-exit`, `physics-based-easing` | P0 |
| IM-05 | **Neraca seimbang** (akhir permainan) | Setelah 14 kartu, lengan neraca bergoyang kecil lalu diam datar; teks "Seimbang!" | Ringkasan skor sebagai teks | Neraca langsung datar | `motion` | P0 |
| IM-06 | **Tebak dulu!** (Amati) | Geser *slider* → angka tebakan berubah langsung; tekan *Lihat kenyataannya* → batang 2025 tumbuh ke 641, garis tebakan tetap terlihat sebagai pembanding, pesan muncul | *Slider* asli berlabel; pesan di `role="status"`; tabel data alternatif | Batang langsung tampil penuh | `slider`, `motion` | P0 |
| IM-07 | **Batang tumbuh saat terlihat** (grafik JPPI & PISA) | Batang tumbuh dari 0 ketika grafik masuk layar | Nilai selalu tertulis di batang | Batang langsung penuh; peningkatan hanya bila `animation-timeline: view()` didukung | `scroll-entry-exit-effects` | P1 |
| IM-08 | **Fasad video** (Amati) | Ketuk gambar sampul (berkas lokal) → *iframe* `youtube-nocookie.com` dimuat dan siap diputar; fokus pindah ke *iframe* | Tombol "Putar video: …"; *iframe* ber-`title`; ringkasan teks di bawah | Tanpa transisi | `lazy-load-video-and-audio`, `privacy` | P0 |
| IM-09 | **Chip tanggapan** (Amati, LKPD) | Ketuk *chip* → ikon centang "muncul" dan warna berubah | Kotak centang asli dalam `fieldset` | Tanpa efek muncul | `checkbox` | P0 |
| IM-10 | **Kartu Masalah** (Ruang Baca 1) | Ketuk kartu → isi masalah terbuka di tempat dengan transisi tinggi; tombol "Selidiki kasusnya" muncul | Tombol `aria-expanded` atau `<details>`; isi tetap ada di DOM | Buka tanpa transisi | `accordion`, `animate-to-intrinsic-sizes` | P1 |
| IM-11 | **Pasangan Seimbang** (Ruang Baca 2) | Ketuk hak (terpilih, terangkat) → ketuk kewajiban. Tepat: kedua kartu menyatu, neraca mini tetap datar, "Seimbang!". Belum tepat: kartu bergoyang pelan, neraca mini miring sesaat. (P2: seret dengan *pointer capture* sebagai alternatif) | Semua kartu `<button>` dengan `aria-pressed`; hasil di `role="status"`; urutan fokus logis | Tanpa goyang/miring; hanya ikon + teks | `physics-based-easing`; P2: `drag-and-drop` (pola *pointer capture* & `Escape`) | P0 |
| IM-12 | **Peta Pasal** (Ruang Baca 3, LKPD) | Kotak 28A–28J + pasal lain; ketuk → dialog berisi pokok pengaturan dan jenis (hak/kewajiban/keduanya); kotak yang sudah dibuka diberi centang; kolom cari menyaring kotak secara langsung | `<search>` + label; dialog native; jumlah hasil diumumkan dengan *debounce* | Dialog muncul tanpa membesar | `dialog`, `html` (`<search>`), `accessibility` §8 | P0 |
| IM-13 | **Pohon Peradilan** (Ruang Baca 4) | Cabang dapat dibuka-tutup; garis cabang tergambar saat dibuka | `<details>` bersarang, tanpa judul di `summary` | Tanpa gambar garis bergerak | `accordion` | P1 |
| IM-14 | **Siapa yang Menangani?** (Ruang Baca 4) | Kartu situasi + pilihan lembaga; pilih → umpan balik + alasan; skor akhir | Grup tombol; hasil di `role="status"` | Tanpa transisi kartu | `animate-element-entry-exit` | P1 |
| IM-15 | **Istilah bertitik** (bacaan & kasus) | Ketuk istilah → lembar definisi muncul dari bawah (layar sempit) atau kartu tengah (layar lebar) | Tombol istilah; `popover="auto"`; `Esc` menutup; fokus kembali | Muncul tanpa geser | `interest-triggered-tooltips`, `content-first-noise-reduction` | P1 |
| IM-16 | **Langkah LKPD** (Selidiki) | Lanjut → langkah aktif berganti dengan geser pendek; daftar langkah mencentang langkah selesai; *Butuh petunjuk?* membuka satu petunjuk per ketukan dengan penghitung "Petunjuk 1/3" | Fokus ke judul langkah baru; petunjuk di `role="status"` | Berganti tanpa geser | `animate-element-entry-exit`, `html` §6 | P0 |
| IM-17 | **Penghitung upaya** (LKPD L6) | Setiap upaya ditambah → lencana "2 upaya ✓ minimal terpenuhi" berubah dari abu-abu ke toska | Teks berubah + ikon; diumumkan sekali saat syarat terpenuhi | Tanpa animasi warna | `forms` | P0 |
| IM-18 | **Status tersimpan** (LKPD, refleksi) | Setelah berhenti mengetik ±800 md → "Tersimpan di perangkat ini" muncul pelan lalu meredup | Satu `role="status"` per halaman, *debounce* | Tanpa memudar | `accessibility` §8 | P0 |
| IM-19 | **Umpan balik kuis** (Uji) | Pilih jawaban → opsi terkunci. Benar: centang memantul + semburan kecil 8 titik toska (≤ 600 md). Belum tepat: kartu bergoyang 2 kali (≤ 300 md), jawaban benar ditandai, pembahasan terbuka | Hasil + pembahasan dibacakan lewat `role="status"`; ikon + teks, bukan warna saja | Tanpa pantul, semburan, dan goyang | `motion`, `physics-based-easing` | P0 |
| IM-20 | **Hitung naik skor** (Uji) | Angka skor naik dari 0 ke nilai akhir (≤ 800 md), batang TP 1 & TP 2 terisi | Nilai akhir langsung tersedia sebagai teks bagi pembaca layar | Angka langsung tampil | `motion` | P1 |
| IM-21 | **Lencana didapat** (semua stasiun) | Saat syarat terpenuhi → notifikasi kecil dengan ikon lencana "muncul"; daftar lencana di Beranda | `popover="manual"`; teks juga tampil di Beranda; ditunda bila dialog terbuka | Muncul tanpa membesar | `persistent-toast-notifications` | P1 |
| IM-22 | **Napas STOP** (Renungkan) | Tekan *Mulai* → lingkaran membesar 4 dtk (Tarik napas), diam 2 dtk (Tahan), mengecil 6 dtk (Hembuskan), 3 siklus; tombol *Jeda* | Aba-aba teks besar berganti; tidak diumumkan berulang; tombol jeda tanpa `aria-pressed` bila label berganti | Lingkaran diam; hanya aba-aba teks dan hitung mundur | `motion` | P1 |
| IM-23 | **Catatan Tempel** (Renungkan) | Kartu bergaya kertas tempel sedikit miring (−1,5°); saat difokus menjadi lurus | Kolom berlabel; tombol salin | Tanpa rotasi | `copy-button` | P1 |
| IM-24 | **Tombol salin** (Berkarya, Ringkasan) | Ketuk → ikon salin berubah menjadi centang + gelembung "Disalin!" ±2 dtk | Gelembung sekaligus *live region*; tombol tidak dinonaktifkan | Gelembung memudar saja | `copy-button` | P1 |
| IM-25 | **Transisi stasiun** (antarhalaman jalur) | Maju: halaman lama bergeser ke kiri dan halaman baru masuk dari kanan; mundur sebaliknya; halaman lain memakai *cross-fade* | Judul halaman unik; fokus normal | Tanpa transisi (opt-in hanya di `no-preference`) | `cross-document-transitions`, `directional-navigation-transitions`, `consistent-cross-document-transitions` | P1 |
| IM-26 | **Timer kelas** (Mode Guru) | Cincin menghitung mundur; 1 menit terakhir berubah jingga + ikon jam; habis: cincin berdenyut lembut 2 kali (tanpa kedip) + teks "Waktu habis" | Diumumkan hanya pada 5 menit, 1 menit, dan habis | Tanpa denyut | `progress-ring`, `motion` | P1 |
| IM-27 | **Roda giliran** (Mode Guru) | Tekan *Acak* → empat kartu kelompok berputar urutan ±1,2 dtk lalu berhenti pada urutan presentasi | Urutan akhir tampil sebagai daftar bernomor dan diumumkan | Urutan langsung tampil | `motion` | P2 |

## 11. Wireframe teks (urutan blok di layar sempit)

### 11.1 Beranda (`index.html`)

1. Kepala halaman.
2. *Hero*: judul "Neraca Warga", tagline *Seimbangkan hak dan kewajibanmu*, subjudul "Pendidikan Pancasila Kelas IX · Tantangan Pemenuhan Hak dan Kewajiban Warga Negara", **Neraca interaktif (IM-02)**, tombol utama *Mulai Belajar* / *Lanjutkan: {stasiun}*.
3. **Jalur Belajar**: enam kartu stasiun (nomor, nama, satu kalimat, ilustrasi kecil, status).
4. Kartu **Ruang Baca** (progres 0–4 bagian) dan **Glosarium**.
5. Pilihan peran: *Saya siswa* (gulir ke Jalur) · *Saya guru* (ke `guru.html`).
6. Lencana (bila ada).
7. Kotak privasi singkat + *Hapus data di perangkat ini* + *Pasang di perangkat* (bila didukung).
8. Kaki halaman: Tentang, versi, lisensi.

Layar lebar: *hero* dua kolom (teks kiri, neraca kanan); Jalur Belajar 3 × 2.

### 11.2 Stasiun (pola umum)

Kepala → penanda stasiun → judul + *chip* prinsip → pengantar → blok kegiatan → kotak *Butuh bantuan?* (stasiun tertentu) → tombol *Berikutnya* → bilah bawah.

### 11.3 Mulai (`mulai.html`)

Cek Perasaan → Hak atau Kewajiban? (kartu besar di tengah, tiga tombol di bawah: Kewajiban | Keduanya | Hak; neraca di atas kartu; penghitung 1/14) → Tujuan belajar ramah siswa → Pertanyaan pemantik (catatan keselamatan di atas) → Berikutnya: Amati.

### 11.4 Amati (`amati.html`)

Grafik JPPI dengan *slider* tebakan → pertanyaan lanjutan → Video (fasad) + ringkasan → Rujukan Gambar 2.9 → Tanggapan awal (dua `fieldset` *chip* + kolom teks) → Data PISA (grafik + catatan) → Berikutnya: Selidiki.

### 11.5 Ruang Baca — contoh `baca-ham.html`

Bilah progres baca → judul bagian → teks → perbandingan dua kolom → kutipan UU 39/1999 (`figure` + `blockquote`) → **Peta Pasal** (cari + kotak) → paragraf pasal di luar Bab XA → *Tandai sudah dibaca* → navigasi bagian sebelumnya/berikutnya. Layar lebar: daftar isi bagian di samping.

### 11.6 Selidiki — `kasus-n.html`

Judul LKPD + tema → daftar langkah (horizontal bergulir di layar sempit, vertikal di samping pada layar lebar) → langkah aktif (judul, pertanyaan, kolom, *Butuh petunjuk?*, tautan Ruang Baca terkait) → *Sebelumnya / Lanjut* → status tersimpan → (opsional) timer diskusi. Ringkasan: dokumen siap cetak + *Cetak/Simpan PDF* + *Salin teks*.

### 11.7 Uji (`uji.html`)

Pengantar + catatan latihan → bilah progres soal → kartu soal (nomor, pertanyaan, 4 opsi sebagai tombol besar) → pembahasan → *Soal berikutnya* → Hasil (skor, batang TP 1 & TP 2, pesan, rekomendasi, *Ulangi kuis*).

### 11.8 Renungkan (`renungkan.html`)

Simpulan → Napas STOP → Refleksi a–d → Catatan Tempel (e) → *Salin refleksi* / *Cetak*.

### 11.9 Berkarya (`berkarya.html`)

Tugas + tiga pilihan bentuk (kartu pilihan) → kriteria (tabel rubrik) → bank data & pasal (kartu dengan tombol salin) → ceklis rencana → (opsional) tautan pengayaan.

### 11.10 Mode Guru (`guru.html`, `guru-penilaian.html`)

`guru.html`: tombol *Tampilan proyektor* → daftar segmen alur (aktif disorot) → timer besar → panel segmen aktif (misalnya *ice breaking* proyektor, pemantik, pembagian kelompok) → roda giliran (P2).
`guru-penilaian.html`: tab/bagian Rubrik Sikap · Rubrik Keterampilan · Kalkulator Nilai TP · Rambu Jawaban LKPD · Cetak (LKPD kosong 1–4, soal post-test).

## 12. Keadaan khusus

| Keadaan | Tampilan |
| --- | --- |
| Pertama kali (belum ada progres) | Beranda menampilkan *Mulai Belajar*; kartu stasiun berstatus *Belum mulai* |
| Luring | Pita kecil non-modal "Kamu sedang luring…"; video menampilkan pesan luring + ringkasan |
| Penyimpanan tidak tersedia (mode privat/penuh) | Pesan sekali per halaman: "Jawaban tidak dapat disimpan di perangkat ini. Salin jawabanmu agar tidak hilang." Semua fitur tetap jalan di memori |
| JavaScript mati | Teks bacaan dan kasus tetap terbaca; widget menampilkan pesan cadangan (`nw-*:not(:defined)`) |
| Versi baru tersedia | Notifikasi "Versi baru tersedia · Muat ulang" |
| Data dihapus | Pesan konfirmasi; progres kembali kosong |
| Halaman tidak ada | `404.html` dengan ilustrasi neraca miring dan tombol ke Beranda |

## 13. Daftar periksa desain (*Definition of Done* visual)

- [ ] Semua pasangan teks/latar ≥ 4,5:1; batas UI ≥ 3:1 (tema terang & gelap)
- [ ] Hak/kewajiban/keduanya selalu disertai ikon dan teks
- [ ] Tidak ada pengguliran horizontal di 320 px; zoom 200% tanpa kehilangan konten
- [ ] Target sentuh ≥ 44 px pada layar sentuh
- [ ] Mode *forced colors*: batas kartu dan fokus tetap terlihat
- [ ] Semua gerak spasial hilang di `prefers-reduced-motion: reduce`, keadaan akhir tetap benar
- [ ] Tidak ada animasi otomatis > 5 dtk tanpa tombol jeda; tidak ada kedip > 3/dtk
- [ ] Ilustrasi ≤ 30 KB, dekoratif diberi `aria-hidden`
- [ ] Gaya cetak LKPD dan ringkasan rapi di A4
