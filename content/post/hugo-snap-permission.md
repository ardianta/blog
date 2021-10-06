---
title: "Fix: Hugo Snap Permission Denied"
slug: hugo-snap-permission
date: 2021-10-06T12:44:06+08:00
draft: false

type: post

tags:
    - Hugo

image: "/img/hugo-snap-permission/hugo-server-permission-denied.png"
description: "Cara perbaiki file permission denied pada hugo yang diinstall dengan snap"

typora-root-url: ../../static
typora-copy-images-to: ../../static/img/hugo-snap-permission/

---

Hugo yang saya install dengan `snap` ternyata tidak bisa bekerja dengan normal.

## Masalah:

Saat menjalankan `hugo server` saya mendapatkan error berikut:

![hugo server permission denied](/img/hugo-snap-permission/hugo-server-permission-denied.png)

Awalnya saya mengira karena hak akses file di proyek yang saya jalankan belum benar.

Saya sudah coba ubah dengan `chmod`, tapi tidak ada hasilnya. Tetap saja permission denied.

Saya juga sudah coba menjalankannya dengan `sudo`, tapi tidak ada hasil juga.

## Solusi:

Setelah googling, saya menemukan jawaban. Ternyata memang hugo yang terinstall dengan `snap` belum bisa mengakses file yang berada di storage eksternal seperti hardisk dan flashdisk.

Agar bisa mengaksesnya, kita harus menghubungkannya dengan perintah:

```bash
sudo snap connect hugo:removable-media
```

Dengan begitu, `hugo` bisa mengakses file yang berada di removable media.