---
title: "Konfigurasi Image Typora untuk Hugo"
slug: typora-hugo
date: 2021-08-25T15:08:15+08:00
draft: false

type: post

tags:
  - Typora
  - Hugo

image: "/img/typora-hugo/konfigurasi-typora-image.png"
description: "Cara konfigurasi Image di Typora untuk menulis konten Hugo. Sehingga kamu bisa lebih produktif."

typora-root-url: ../../static
typora-copy-images-to: ../../static/img/typora-hugo/
---

Sudah lama saya menulis konten di Hugo dengan Typora dan menikmati fitur yang disediakan oleh Typora.

Salah satu fitur yang saya sukai adalah bisa drag & drop gambar ke dalam artikel dan Typora akan otomatis melakukan copy ke folder yang kita tentukan.

Bahkan bisa juga otomatis melakukan upload ke layanan yang kita inginkan, misalnya seperti AWS S3 atau Firebase Storage.

Namun, yang akan saya bahas kali ini adalah gimana cara konfigurasi Typora untuk copy image ke folder `static` dan bisa ditampilkan di Teks Editor Typora maupun di website Hugo.

Mari kita mulai..

## Konfigurasi Front-matter di Archetype

Berikut ini konfigurasi `archetypes/post.md` milik saya.

```yaml
---
title: "{{ replace .TranslationBaseName "-" " " | title }}"
slug: {{ .BaseFileName }}
date: {{ .Date }}
draft: true

type: post

tags:
    - tag

image: ""
description: ""

typora-root-url: ../../static
typora-copy-images-to: ../../static/img/{{ .Name }}/
---
```

Coba perhatikan dua atribut terakhir di *archetype* ini!

```yaml
typora-root-url: ../../static
typora-copy-images-to: ../../static/img/{{ .Name }}/
```

Ini adalah atribut yang dibutuhkan Typora.

- `typora-root-url` adalah root URL untuk file statis yang akan digunakan oleh Typora.
- `typora-copy-images-to` adalah path yang akan digunakan oleh typora untuk melakukan copy otomatis saat kita melakukan drag & drop gambar.

Perlu di ketahui, arti dari `../../` adalah dua folder di atasnya. Karena file konten yang sedang dibuka berada di dalam folder `content/post/` sementara file statis berada di `static/` maka kita perlu naik dua level untuk mengakses folder tersebut.

Jika kamu menggunakan [page bundle](https://gohugo.io/content-management/page-bundles/), beda lagi konfigurasinya.

Mungkin akan seperti ini:

```yaml
typora-root-url: ./
typora-copy-images-to: ./
```

Ini karena page bundle menyimpan gambar di satu folder dengan file page kontenya.

Saya sendiri tidak menggunakan page bundle, karena tidak ingin mencampurkan konten dengan gambar, biar tidak berantakan hehe.

Tapi ya, preferensi orang.. beda-beda.

Ikuti saja yang mana paling nyaman menurutmu.

Kemudian setelah ini diapain?

Selanjutnya:

## Konfigurasi Image di Typora

Buka menu **File** > **Preferences** > **Image**, kemudian atur seperti ini:

![konfigurasi typora image](/img/typora-hugo/konfigurasi-typora-image.png)

Untuk centang **Apply above rules to online image** boleh juga dicentang, jika ingin menerapkan aturan ini pada gambar yang di copy dari internet.

Note:

Untuk yang menggunakan page bundle, tidak perlu menambahkan `img`, langsung saja tulis lokasi path-nya seperti ini:

```bash
./${filename}
```

Oke..

Setelah itu, kita bisa mencoba.

## Percobaan

Coba buat konten `post` baru di Hugo, kemudian buka dengan Typora.

Lalu, drag & drop gambar ke sana.

Maka akan muncul:

![craete folder](/img/typora-hugo/craete-folder.png)

Kita diminta untuk membuat folder baru, karena target folder yang kita tentukan di `typora-copy-image-to` belum ada.

Langsung saja klik **Create Folder**, maka gambar akan ditambahkan ke artikel seperti ini.

![typora inserted image](/img/typora-hugo/typora-inserted-image.png)

## Akhir Kata..

Nah, begitulah cara saya mengkonfigurasi Typora untuk menulis konten pada Hugo.

Typora memang memudahkan pekerjaan saya dalam menulis konten.

Selamat mencoba!