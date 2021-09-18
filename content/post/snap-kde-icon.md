---
title: "Fix: Ikon Aplikasi yang diinstal dengan Snap tidak Tampil"
slug: snap-kde-icon
date: 2021-09-18T19:59:51+08:00
draft: false

type: post

tags:
  - Linux
  - Snap

image: "/img/snap-kde-icon/file-script-autorun.png"
description: "Aplikasi yang diinstal dengan snap tidak memiliki ikon di menu launcher. Gimana cara perbaikinya?"

typora-root-url: ../../static
typora-copy-images-to: ../../static/img/snap-kde-icon/
---

Awalnya saya mengira ini masalah di KDE, tapi ternyata bukan.

Setiap kali saya instal aplikasi dengan `snap`, ikon-nya pasti tidak ada di menu launcher.

Ini membuat saya kesal, dan tidak ingin menggunakan snap.

Mengapa bisa begini?

Apakah snap tidak mendukung KDE?

Tapi jika saya install dari Discover  (Manajer aplikasi bawaan KDE), aplikasi yang bersumber dari snap bisa terinstal dengan benar.

Tapi kenapa saat saya menggunakan command line, ikon aplikasinya tidak tampil di menu? 

Setelah googling, akrhinya saya ketemua akar masalahnya.

## Masalah:

Ikon aplikasi yang diinstal dengan `snap` tidak tampil di menu launcher, karena shell yang saya gunakan mungkin tidak bisa mengeksekusi script untuk integrasi dengan environment desktop.

O ya, dalam kasus ini saya menggunakan Fish Shell.

Seharusnya default sehll di Linux adalah Bash, tapi saya sudah menggantinya dengan Fish Sehll, karena merasa lebih nyaman menggunakan Shell ini.

Ternyata ini yang menjadi penyebab ikon aplikasi tidak ditambahkan di menu launcher.

Uh dasar Fish Shell..

## Solusi:

Solusi dari masalah ini adalah dengan menambahkan alamat path aplikasi snap pada environment variabel `XDG_DATA_DIRS`.

Coba lihat gimana isi variabel ini sekarang dengan perintah echo:

```bash
dian@petanikode~> echo $XDG_DATA_DIRS
/usr/share/plasma:/home/dian/.local/share/flatpak/exports/share:/var/lib/flatpak/exports/share:/usr/local/share:/usr/share
```

Keliatan di sini, tidak ada alamat path yang menuju ke folder ikon untuk aplikasi snap.

Untuk memperbaikinya, kita bisa tambahkan alamat path dengan membuat custom script.

Buat file baru di dalam `/home/username/.config/plasma-workspace/env/` dengan nama `snap-apps-dekstop-integration.sh` kemudian isi dengan kode ini:

```bash
export XDG_DATA_DIRS="$XDG_DATA_DIRS:/var/lib/snapd/desktop/"
```

Intinya, pada script ini kita menambahkan alamat path aplikasi snap.

![file script autorun](/img/snap-kde-icon/file-script-autorun.png)

File script yang ada di dalam folder `plasma-workspace/env` akan otomatis dieksekusi saat komputer baru nyala.

Karena itu, silahkan restart untuk melihat perubahannya.

Semoga berhasil.