---
title: "Eksperimen Membuat Template Blogger dengan Bootstrap 4"
slug: template-blogger
date: 2018-01-25T20:30:53+08:00
draft: false

type: post

tags:
    - Blog
    - Bootstrap

image: "/img/template-blogger/cheatsheet.png"
description: "Membuat template blog sepertinya lebih sulit daripada membuat template Hugo. Karena dokumentasi template blogger sangat minim."
---

Tadi malam saya coba eksperimen membuat template blogger dengan
Bootstrap 4. Saya membuat blog baru (https://bs4blogger.blogspot.com)
untuk eksperimen ini.

Membuat template blog sepertinya lebih sulit daripada membuat
template Hugo. Karena dokumentasi template blogger sangat minim.

Berikut ini link dokumentasi yang bisa digunakan:

- [Pengenalan konsep dasar template blogger](https://support.google.com/blogger/answer/46888)
- [Penjelasan tentang CSS di Template](https://support.google.com/blogger/answer/46871)
- [Penjelasan tentang kode widget](https://support.google.com/blogger/answer/46995)
- [Variabel data di template](https://support.google.com/blogger/answer/47270)

Saya juga menggunakan semacam *cheatsheet* untuk mempermudah
dalam mengetahui isi dari variabel data.

![Cheatsheet template blogger](/img/template-blogger/cheatsheet.png)

## Kendala

Setelah berjam-jam, saya mendapat kendala pada *layout*.
Karena blogger juga menyisipkan class-class aneh di templatenya.

Hal ini membuat saya kesulitan membuat template.

Rencananya saya mau buat layout yang berbeda untuk halaman
home dan halaman artikel. Tapi susah juga, karena template Blogger
menggunakan komponen section (`<b:section >`) yang membatasi
kebebasan saya.

...dan juga penjelasan atau dokumentasi tentang komponen-komponen
itu sangat minim.

## Akhir kata...

Blogger sepertinya produk yang tidak mendapatkan
perhatian lebih. Di saat produk-produk Google yang lain 
sudah di-upgrade ke teknologi baru. 
Blogger malah dibiarkan oleh Google.
Padalah penggunanya cukup banyak.

Mungkin saja profit-nya kurang 😄...