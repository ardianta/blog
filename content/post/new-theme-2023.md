---
title: "New Hugo Theme 2023: Template Baru untuk Web Personal Saya"
slug: new-theme-2023
date: 2023-05-16T14:05:05+08:00
draft: false

type: post

tags:
    - Hugo

image: "/img/new-theme-2023/before-after.avif"
description: "Sebenarnya sudah lama saya ingin ganti template web personal. Tapi nggak kunjung-kunjung dikerjakan. Malah keasikan ngerjain project yang lain, hehe."

typora-root-url: ../../static
typora-copy-images-to: ../../static/img/new-theme-2023/
---

Sebenarnya sudah lama saya ingin ganti template web personal.
Tapi nggak kunjung-kunjung dikerjakan. Malah keasikan ngerjain project yang lain, hehe.

Kemarin (15/05/2023), saya mulai develop tema baru.

```bash
hugo new theme ardianta
```

Untuk sementara, nama theme-nya adalah `ardianta`. Mungkin nanti kalau sudah jadi akan saya ubah
dan submit ke website Hugo.

## Desain Theme

Sebelum mulai bikin theme, saya sudah menyiapkan desainnya bakal seperti apa.
Desain saya buat di Figma. Namun, waktu saya coding saya tidak mengikuti 100% dari desain.

Desain ini cuma jadi patokan saja untuk layout dan style. Tidak harus 100% pixel perfect hehe.

![Desain Theme di Figma](/img/new-theme-2023/desain-theme-di-figma.avif)

Desain temanya sudah saya buat cukup lama, cuma kemarin dilakukan improvement lagi. Seperti menambahkan section dan mengganti font.

## Typography

Untuk typography, saya mengandalkan plugin Prose dari Tailwind. Font yang digunakan adalah [Jost](https://fonts.google.com/specimen/Jost).
Saya tertarik menggunakan font ini karena terinspirasi dari [theme Doks](https://github.com/h-enk/doks).

![Web Doks](/img/new-theme-2023/web-doks.avif)

Font Jost terlihat tegas tapi fun. Tegas tapi informal. Saya suka melihatnya, apalagi kalau di pakai di artikel.

..dan sepertinya jika dipakai di UI, font ini juga terlihat bagus.

## Coding Logs..

Catatan-catatan yang dilakukan saat coding:

### Hari Pertama (15 Mei 2023)

Hari ini saya menghabiskan waktu sekitar 4 jam lebih buat coding *(slicing)* halaman home atau landing page.
Saya menggunakan TailwindCSS, tapi untuk awal saya pakai Tailwind dari CDN. Bukan tailwind yang di-build dari Hugo,
seperti di Tutorial yang pernah saya share: [Menggunakan Tailwind untuk Membuat Tema Hugo](https://www.petanikode.com/hugo-tailwind/).

Pertimbangan menggunakan TailwindCSS di awal agar bisa langsung fokus slicing, bukan setup-setup Tailwind.

Untuk saat ini hasil codingnya:

![Hasil Coding landing page](/img/new-theme-2023/halaman-landing.avif)

Mantap, sudah cukup terlihat bagus.

### Hari Pertama (16 Mei 2023)

Di Hari ke-2, saya melanjutkan mengerjakan template untuk halaman-halaman esensial seperti:

- Halaman Artikel
- Halaman List Artikel
- Halaman untuk Regular Page

Hasilnya:

![Halaman Artikel](/img/new-theme-2023/halaman-artikel.avif)

Ada beberapa partial yang ditambahkan:

1. Partial Pagination
2. Partial Disqus

## Perbandingan Before dan After

Sebelumnya theme saya buat pakai Bootstrap, sekarang pakai Tailwind.
Berikut ini perbandingan desainnya.

![Before vs After](/img/new-theme-2023/before-after.avif)

Yang sebelah kanan jelas terlihat lebih bagus dan profesional. 😁

## Apa Selanjutnya?

Bisa dibilang template ini sudah selesai 70% dan sepertinya sudah bisa dipakai.
Sisanya saya tinggal buat template untuk halaman-halaman lainnya seperti halaman Project,
Taxonomy, Search, Contact, dll.