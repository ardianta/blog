---
title: "Partial Penghitung Kata pada Hugo"
slug: hugo-wordscounter
date: 2018-09-08T22:15:58+08:00
draft: false

type: post

tags:
    - hugo
    - blog

image: "/img/wordscounter/layout.png"
description: "Setiap menulis blog, Saya jarang memperhatikan
jumlah kata yang ditulis. Rencananya saya ingin menulis 1000+ kata
untuk setiap artikel."
---

Setiap menulis blog, Saya jarang memperhatikan
jumlah kata yang ditulis.

Rencananya saya ingin menulis 1000+ kata
untuk setiap artikel.

Karena itu, saya perlu bantuan penghitung
kata pada tulisa.

Saya menggunakan teks editor VS Code untuk
menulis. Kadang menggunakan VIM.

Di VS Code, saya tidak ingin menginstal ekstensi
untuk menghitung jumlah kata.

Karena di artikel yang ditulis terdapat
front-matter yang juga akan masuk hitungan.

Karena itu, solusinya membuat partial
penghitung kata.

Oke, ini dia partialnya:

![Partial Penghitung kata di Hugo](/img/wordscounter/partial.png)

Saya memberi nama `statusbar.html`,
karena akan ditampilkan pada bagian bawah.

Setelah itu, partial ini tinggal kita pakai
pada layout `single.html`.

![Menggunakan partial](/img/wordscounter/layout.png)

Hasilnya:

![Hasil partial](/img/wordscounter/output.png)

Mantap :+1:

Sekarang saya bisa tahu jumlah kata yang
ditulis.

{{< tweet 1037985999752593408 >}}