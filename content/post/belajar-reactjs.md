---
title: "Langkah Awal: Belajar Reactjs"
slug: belajar-reactjs
date: 2017-12-29T04:24:49+08:00
draft: false

type: post

tags:
    - Reactjs
    - Javascript

image: "/img/react/reactjs-vscode.png"
description: "Langkah awal belajar React, ya pertama harus kenalan dulu dengan React-nya. Bagaimana sejarahnya? Kenapa harus menggunakan React? Bagaimana konsep React?"
---

Saya telat ikut kulgram Reactjs di [@lombokjs](https://t.me/lombokjs),
karena kehabisan kuota 😢.

Tapi tak masalah, di Telegram masih tersimpan arsipnya.

Langkah awal belajar React, ya pertama harus kenalan dulu 
dengan React-nya.

Bagaimana sejarahnya?

Kenapa harus menggunakan React?

Bagaimana konsep React?

Kira-kira itulah isi dari kulgram semalam yang nggak saya ikuti.

Tapi pagi ini, saya mau coba-coba langsung...

Coba nginstall aja, siapa tau mau belajar lebih lanjut.

## Memulai Project React

Saya akan menggunakan `yarn` dan `create-react-app` untuk memulai.

Pertama, kita install dulu `yarn`.

```bash
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update && sudo apt-get install yarn
```

Untuk sistem operasi yang lain cek di sini: https://yarnpkg.com/lang/en/docs/install/

Kenapa tidak pakai `npm`?

Karena merasa pakai `yarn` lebih kenceng 😄.

Habis install `yarn`, sekarang kita intall `create-react-app`.

```bash
sudo yarn global add create-react-app
```

Sebenarnya bisa langsung pakai CDN, tapi biar keren dikit kita pakai ini aja.

![Instalasi create-react-app](/img/react/instalasi-create-react.png)

Setelah itu, baru kita bisa baut project React.

Perintahnya:

```bash
create-react-app my-react-app
```

Habis itu, kita buka dengan teks editor andalan, yaitu VS Code:

```bash
code my-ract-app
```

![Buka project react dengan VS Code](/img/react/code-my-react.png)

...dan ini lah penampakannya:

![Buka project react dengan VS Code](/img/react/reactjs-vscode.png)

Terakhir, tinggal ketik perintah `yarn start` untuk _build_ dan menjalankan server.

![Start server react](/img/react/yarn-start.png)

Lalu, browser akan terbuka otomatis dan hasilnya:

![Start server react](/img/react/react-di-browser.png)

Mantap 😍...

## Akhir Kata

Kelihatannya menarik untuk dipelajari lebih dalam. Karena di Indonesia
juga banyak yang menggunakannya.

Mungkin nanti saya akan masukkan ke dalam _list_ untuk dipelajari di tahun depan (2018).