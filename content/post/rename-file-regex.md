---
title: "Rename Banyak File dengan Regex"
slug: rename-file-regex
date: 2021-04-01T12:32:40+08:00
draft: false

type: post

tags:
    - tag

image: ""
description: "Cara rename banyak file dengan Regex di Linux"

typora-root-url: ../../static
---

Di Linux, kita bisa rename banyak file dengan Regex.

Program yang digunakan adalah:

- `rename`
- `prename`

Install dulu program rename:

```bash
sudo apt install rename
```

Note: sebenarnya program `rename` ada yang dari `util-linux` dan `File::Rename` (Perl),
kita akan pakai yang dari Perl.. karena dia support regex.

Coba baca issue ini:

- https://askubuntu.com/a/1024963
- https://askubuntu.com/a/956020

Jika kamu menggunakan fedora, bisa pakai `prename`.

Install dengan perintah:

```bash
sudo dnf install prename
```

Setelah itu masuk ke folder tempat semua file berada, lalu jalankan 
perintah rename dengan regex.

```bash
rename -n 's/<regex untuk search file>/<regex untuk replace>/' *.ext
```

Opsi `-n` akan memberikan output dari hasil rename, ini berguna
untuk coba-coba regex-nya sebelum di rename.

Simbol `s/` para regex berarti kita akan melakukan subtitusi atau replace.

Contoh:

list file sebagai berikut:

```txt
[Anime] Black Clover BD - 01.mkv
[Anime] Black Clover BD - 02.mkv
[Anime] Black Clover BD - 03.mkv
[Anime] Black Clover BD - 04.mkv
[Anime] Black Clover BD - 05.mkv
```

Kita ingin rename menjadi seperti ini:

```txt
Black Clover - 01.mkv
Black Clover - 02.mkv
Black Clover - 03.mkv
Black Clover - 04.mkv
Black Clover - 05.mkv
```

Maka perintahnya:

```bash
rename -n 's/(\[w+]) (Black Clover) BD - (\d.)/$2 - $3' *.mkv
```

Penjelasan tentang regex-nya bisa dicek di [regexr.com/5prb7](https://regexr.com/5prb7).

Hasil outputnya:

```txt
rename([Anime] Black Clover BD - 01.mkv, Black Clover - 01.mkv)
rename([Anime] Black Clover BD - 02.mkv, Black Clover - 02.mkv)
rename([Anime] Black Clover BD - 03.mkv, Black Clover - 03.mkv)
rename([Anime] Black Clover BD - 04.mkv, Black Clover - 04.mkv)
rename([Anime] Black Clover BD - 05.mkv, Black Clover - 05.mkv)
```

Jika sudah yakin, opsi `-n` bisa dihapus untuk melakukan rename.

```bash
rename 's/(\[w+]) (Black Clover) BD - (\d)/$2 - $3' *.mkv
```

Selamat mencoba.