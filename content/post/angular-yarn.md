---
title: "Menggunakan Yarn pada Angular CLI"
slug: angular-yarn
date: 2017-12-30T12:13:17+08:00
draft: false

type: post

tags:
    - Angular
    - Javascript
    - Nodejs
    - NPM
    - Yarn

image: "/img/angular/angular-yarn.png"
description: "Angular default-nya menggunakan NPM. Apabila ingin mengganti package manager
ke Yarn, cukup ketik perintah ini"
---

Angular default-nya menggunakan NPM. Apabila ingin mengganti package manager
ke Yarn, cukup ketik perintah ini:

```bash
ng set --global packageManager=yarn
```

Percobaan:

![Angular CLI dengan Yarn](/img/angular/angular-yarn.png)

Untuk mengembalikan ke NPM:

```bash
ng set --global packageManager=npm
```

__Kenapa Pakai Yarn?__

Menurut saya Yarn lebih cepat daripada NPM dan Yarn bisa digunakan Offline.

Sumber: https://medium.com/@beeman/using-yarn-with-angular-cli-db2e318e43c5
