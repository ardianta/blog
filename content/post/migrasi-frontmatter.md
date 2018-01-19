---
title: "Migrasi Front-matter Hugo dengan sed"
slug: migrasi-frontmatter
date: 2018-01-19T20:05:09+08:00
draft: false

type: post

tags:
    - hugo
    - blog

image: "/img/sed/git-log.png"
description: "Cara saya modifikasi semua front-matter di artikel hugo dengan sed"
---

Saya berencana memperbaiki template dan front-matter Petanikode.
Ada 300 lebih artikelnya yang harus dimodifikasi.

Saya rasa ini cukup merepotkan, mengedit satu-persatu front-matter
setiap artikel. Apalagi jumlahnya cukup banyak.

Akhirnyta saya menemukan `sed` (Stream Editor). 

Berawal dari coba-coba dari [perintah ini](https://unix.stackexchange.com/questions/112023/how-can-i-replace-a-string-in-a-files), 
Front-matternya menjadi rusak. Untungnya menggunakan git, jadi masih bisa dikembalikan lagi.

Lalu biar mudah saya membuat *branch* baru bernama `theme-migration`.

```bash
git checkout -b theme-migration
```

Sekarang saya bebas memodifikasinya dengan `sed` tanpa harus takut rusak lagi.
Karena kalau rusak, kita bisa bikin lagi *branch* baru dari *branch* `master`.

Ini adalah log catatan di *branch* `theme-migration`:

![Git log](/img/sed/git-log.png)

Kebanyakan yang saya lakukan adalah menghapus dan mengubah agar
menjadi lebih sederhana.

Contoh:

Mengubah `src:` menjadi `image:`

```bash
sed -i -- 's/src:/image:/g' ./content/post/*
```

Tapi sebelum itu, saya coba-coba dulu melakukan print dengan perintah:

```bash
sed -n -- '/src:/p' ./content/post/*
```

Kalau sudah yakin bari menjalankan perintah yang atas.

Saya belum begitu paham dengan `sed` terutama pada *regex*.
Namun, bisa diperlajari pada [tutorialspoint](https://www.tutorialspoint.com/sed/index.htm).

Kedepannya, saya akan menggunakan *archetype* ini untuk postingan terbaru
di Petanikode:

```yaml
---
draft: true
date: {{ .Date }}
updated: {{ .Date }}
type: post

title: "{{ replace .TranslationBaseName "-" " " | title }}"
slug: {{ .BaseFileName }}

topik:
    - Python
    - Java
    - Javascript
    - PHP
    - HTML

kategori:
    - Pemrograman
    - Web
    - Desktop
    - Mobile
    - Jaringan
    - Game

image: "/img/"
thumbnail: "/img/"
description: "{{ replace .TranslationBaseName "-" " " | title }}"
---
```

Setelah selesai mengedit front-matter dengan `sed`, berikutnya melakukan *testing* 
dan *merge* ke *branch* `master`. Terakhir melakuan *deploy* dan beres! 😄