---
title: "Membuat Buku dengan Honkit"
slug: honkit
date: 2020-06-30T23:02:16+08:00
draft: false

type: post

tags:
    - buku

image: ""
description: "Cara saya memulai membuat proyek penulisan buku dengan Hokit"
---

Rencananya saya mau membuat ebook, tapi masih bingung dengan tools yang akan
digunakan.

Kalau gampangnya sih bisa pakai Ms. Writer, tapi saya kurang suka menulis
di aplikasi office. Saya lebih senang menulis di teks editor.

Mencoba cari-cari info di Google, saya menemukan Gitbook Toolchain,
tapi proyek ini sudah dihentikan. Ini mungkin model bisnis dari Gitbook sudah
berubah.

Sebagai alternatif, saya menemukan Honkit.

## Apa itu Honkit?

**Hon** diambil dari bahasa jepang, yang artinya buku. Sementara **kit** artinya
alat-alat atau peralatan. Jadi Honkit adalah peralatan untuk membuat buku.

Mengapa diambil dari bahasa jepang?

Soalnya pencetaus proyek ini adalah si [uzu](https://github.com/uzu). Dia adalah
software developer dari Jepang.

## Memulai Proyek Buku dengan Honkit

Oke, pertama yang harus dipersiapkan adalah:

- Nodejs dengan versi 10 ke atas
- Yarn atau npm (saya lebih prefer yarn)
- Honkit

Biklah, sekarang mari kita mulai membuat proyeknya. Buat saja folder baru lalu 
inisialisasi proyek nodejs di sana dengan yarn atau npm.

```bash
mkdir buku-honkit
cd buku-honkit
yarn init -y
```

Setelah itu, install Honkit:

```bash
yarn add honkit --dev
```

Setelah itu, inisialisasi proyek Honkit dengan perintah:

```bash
yarn run honkit init
```

Perintah ini akan membuat file `SUMMARY.md` dan `README.md`.

## Struktur Direktori

Biar rapi, saya akan menyimpan semua konten buku di dalam folder `src`.
Maka tinggal buat folder baru.

```bash
mkdir src
```

Di dalam folder `src` nantinya akan berisi file markdown dan images untuk 
konten bukunya.

Silahkan pindahkan file `SUMMARY.md` dan `README.md` ke dalam folder `src`.

```txt
├── node_modules
├── package.json
├── src
│   ├── chapter-1
│   │   ├── mengenal-honkit.md
│   │   └── README.md
│   ├── chapter-2
│   ├── images
│   ├── README.md
│   └── SUMMARY.md
└── yarn.lock
```

## Konfigurasi Buku

Berikutnya.. kita harus menambahkan konfigurasi pada file `book.json`.
File ini belum ada, kita harus membuatnya sendiri.

Berikut ini isinya:

```json
{
    "title": "Tutorial Honkit",
    "description": "Belajar membuat buku dengan Honkit",
    "author": "Ahmad Muhardian",
    "isbn": "00000000000000",
    "language": "id",
    "direction": "ltr",
    "root": "src",
    "pdf": {
        "fontFamily": "Lato",
        "fontSize": 16
    }
}
```

Pastikan mengisi field `root` dengan `src`, karena lokasi konten buku kita
berada di sana.

## Konfigurasi Proyek

Buka `package.json`, tambahkan field `scripts`:

```json {hl_lines=["6-11"]}
{
  "name": "budidaya-html",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "scripts": {
    "start": "honkit serve",
    "serve": "honkit serve",
    "build": "honkit build",
    "clean": "rm -rf _book/*"
  },
  "devDependencies": {
    "honkit": "^3.4.1"
  }
}
```

Tujuan dari pembuatan `scripts` ini agar perintah `honkit` bisa kita eksekusi
langsung dengan `yarn`.

Misalnya, mau menjalankan server. Tinggal ketik:

```bash
yarn serve
```

atau

```bash
yarn start
```

## Terakhir Tambahkan .gitignore

Karena nantinya proyek ini akan menggunakan Git, ada baiknya membuat file
`.gitignore` untuk mendaftarkan file-file yang tak perlu dicatat oleh Git.

Berikut ini isi `.gitignore` milik saya:

```txt
_book
node_modules
```

## Apa Selanjutnya?

Selanjutnya kita tinggal mulai nulis deh!

Tinggal otak-atik aja konten markdown yang ada di folder `src`