---
title: "Cara Deploy Hugo dari Gitlab ke Surge"
slug: hugo-gitlab-surge
date: 2018-01-13T17:59:45+08:00
draft: false

type: post

tags:
    - Hugo
    - Blog
    - Gitlab
    - Surge

image: "/img/hugo/ci-gitlab.png"
description: "Cara deploy hugo dari Gitlab CI ke Surge"
---

Saya punya project pembuatan template untuk web company profile.
Sewaktu ingin memperlihatkan demo, saya menggunakan layanan hosting Surge.
Karen sangat mudah sekali.

Cukup dengan mengetik perintah:

```
surge ./public
```

Website suda di-deploy ke Surge.

Namun, tiap kali deploy, kita akan upload semua file `public` ke surge.
Ini saya rasa kurang bagus, karena koneksi internet saya sangat terbatas
(lambat dan kuota tinggal sedikit hahaha 😄).

Karena itu, saya memanfaatkan Gitlab CI:

Worflownya menjadi begini:

```bash
Developer --> Gitlab --> Surge <-- Client
```

Berikut ini skrip `.gitlab.yml` yang saya gunakan:

```yaml
image: node:8-alpine

before_script:
    - npm install -g surge
    - npm install --save-dev hugo-bin@0.18.0
    - node --version
    - surge --version
    - $(npm bin)/hugo version

surge_deploy:
  only:
    - master
  script:
    - rm -rf public
    - $(npm bin)/hugo
    - surge --project ./public/ --token $SURGE_TOKEN
```

Karena image docker yang saya gunakan berbasis `node:8-alpine`.
Saya menggunakan modul nodejs bernama `hugo-bin`, modul ini adalah wrapper dari Hugo
yang bisa diinstal melalui `npm`. Sebenarnya bisa juga diinstal manual dari wget.

Lalu setelah itu menginstall `surge` dan melakukan build.

Kita membutuhkan token surge. Token ini bisa dibuat dengan perintah:

```bash
surge token
```

Setelah itu, kita buat dua variabel env di Secret Varable Gitlab:

1. `SURGE_LOGIN` berisi alamat email yang digunakan pada surge 
2. `SURGE_TOKEN` berisi kode token

Udah itu aja...

Selanjutnya kita tinggal melakukan push ke branch `master`, maka
si CI milik Gitlab akan otomatis melakukan deploy ke Surge.