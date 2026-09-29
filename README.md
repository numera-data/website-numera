# Numera Data — Website Portofolio (Quarto + R)

Situs portofolio **Numera Data — Health Data Research & Analysis Consultant**: beranda, profil
tim, dan proyek (termasuk satu demo analisis survei kompleks dengan **R** yang dirender langsung).
Alamat situs: https://numera-data.github.io/website-numera

## Struktur

```
_quarto.yml                  ← judul situs, menu, tema, URL situs
index.qmd                    ← beranda (hero, statistik, layanan, proyek & tulisan terbaru)
tim.qmd                      ← halaman daftar tim (otomatis dari folder tim/)
tim/<nama>.qmd               ← profil tiap anggota (+ foto <nama>.svg/.jpg)
proyek.qmd                   ← galeri proyek (otomatis dari folder proyek/)
proyek/<slug>/index.qmd      ← satu studi kasus per folder (+ thumbnail)
_templates/tim.ejs           ← template kartu anggota tim
assets/light.scss, dark.scss ← warna brand mode terang/gelap
assets/custom.scss           ← gaya tambahan (hero, kartu, dsb.)
_freeze/                     ← hasil eksekusi kode yang disimpan (WAJIB di-commit)
DESCRIPTION                  ← daftar paket R yang dibutuhkan (dibaca GitHub Actions)
.github/workflows/publish.yml← deploy otomatis ke GitHub Pages
```

## Menjalankan di komputer sendiri

1. Pasang [Quarto](https://quarto.org/docs/get-started/) dan [R](https://cran.r-project.org/) (≥ 4.1; RStudio/Positron opsional).
2. Di konsol R: `install.packages(c("knitr", "rmarkdown", "dplyr", "tidyr", "ggplot2", "scales"))`
3. `quarto preview` → situs terbuka di browser dan otomatis ter-refresh saat file disimpan.

## Mengganti konten

| Ingin mengubah… | Edit file |
|---|---|
| Nama tim, menu, link sosial | `_quarto.yml` |
| Teks beranda & angka statistik | `index.qmd` |
| Anggota tim | salin `tim/falah.qmd` → ubah `title`, `subtitle` (peran), `description`, `image`, `categories` (skill), `order` (urutan) |
| Foto anggota | taruh `tim/<nama>.jpg` (rasio 1:1), lalu ubah `image:` |
| Proyek baru | salin satu folder di `proyek/`, ubah front matter; isi `author:` dengan nama anggota persis agar proyek muncul di profil mereka |
| Paket R baru untuk halaman berkode | tambahkan di bagian `Imports:` pada `DESCRIPTION` |
| Warna brand | `$primary` di `assets/light.scss` dan `assets/dark.scss` (diambil dari logo: #006FE4, #002C65, #009CF9) |
| Peta di beranda (slideshow) | ganti file di `assets/peta/` (PNG/JPG/SVG, rasio 4:3), lalu sesuaikan `src`, `alt`, dan `<figcaption>` di blok `map-slider` pada `index.qmd`. Tambah/kurangi peta dengan menyalin/menghapus satu blok `<figure>`. |
| Logo | `assets/logo.png` (mode terang), `assets/logo-dark.png` (mode gelap), `assets/favicon.png` |

## Deploy ke GitHub Pages

1. Buat repositori `website-numera` di organisasi GitHub `numera-data`, lalu push seluruh folder ini ke branch `main`
   — **termasuk folder `_freeze/`**.
2. Di repositori: **Settings → Pages → Build and deployment → Source: GitHub Actions**.
3. Setiap push ke `main` akan merender dan memublikasikan situs. Status bisa dilihat di tab **Actions**.
4. Situs akan tersedia di https://numera-data.github.io/website-numera (sudah diatur di `site-url`).

> **Tentang `_freeze/`**: halaman berkode R hanya dieksekusi ulang jika file `.qmd`-nya
> berubah. Jalankan `quarto render` secara lokal setelah mengubah halaman berkode, lalu commit
> perubahan di `_freeze/`. Workflow tetap memasang R dan paket di `DESCRIPTION` sebagai cadangan.

## Yang masih perlu dilengkapi

- [ ] Ganti 3 peta **draf** di `assets/peta/` dengan peta asli tim (hapus kata *draf* di keterangan).

- [ ] Link LinkedIn/GitHub pribadi tiap anggota (saat ini memakai email & GitHub tim).
- [ ] Temuan utama tiap proyek dan screenshot (mis. dashboard DBD, peta iklan rokok) bila boleh dipublikasikan.
- [ ] Pastikan domain `numera.org` dan alamat `falah@numera.org` benar-benar aktif.
