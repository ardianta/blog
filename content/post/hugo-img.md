---
title: "Tips Hugo: Agar Gambar Tampil di Preview Markdown VS Code"
slug: hugo-img
date: 2020-01-19T23:02:17+08:00
draft: false

type: post

tags:
    - hugo
    - blog

image: "/img/hugo/img/markdown-preview.png"
description: "Saya biasanya menulis blog dengan VS Code. Tapi saat menggunakan fitur preview markdown di VS Code, gambar tidak mau tampil."
---

Saya biasanya menulis blog dengan VS Code.
Tapi saat menggunakan fitur preview markdown
di VS Code, gambar tidak mau tampil.

Ini karena alamat path gambar pada Hugo
menggunakan `static/img/`.

Sementara pada markdown harus ditulis seperti ini:

```markdown
![Teks Caption](/img/nama-gambar.jpg)
```

Karena nanti saat di-render akan menggunakan alamat itu.
Tapi untuk VS Code, alamat ini tidak ditemukan.

Lalu bagaimana caranya agar VS Code juga bisa baca
alamat gambar dari Hugo?

Caranya kita bisa buat simbolik link pada
root direktori hugo. Bisa menggunakan perintah ini:

```bash
ln -s static/img img
```

Dan hasilnya...

![Preview markdown pada VS Code](/img/hugo/img/markdown-preview.png)