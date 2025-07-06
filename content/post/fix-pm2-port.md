---
title: "[Solved] PM2 Port Already in Use terosss!!"
slug: fix-pm2-port
date: 2025-06-16T20:58:28+08:00
draft: false

type: post

tags:
    - Problem Solved
    - Nodejs
    - Expressjs
    - PM2

image: ""
description: "Berminggu-minggu saya debug project ini, tapi belum solve-solve. Tapi akhirnya solve juga setelah banyak tanya di Gemini."
---

Berminggu-minggu saya debug project ini, tapi belum solve-solve.
Tapi akhirnya solve juga setelah banyak tanya di Gemini.

## Masalah:

Saat run project ini dengan nodemon, aman-aman saja. Tapi saat running menggunakan `pm2`,
malah error. Oya, di sini saya menggunakan file `ecosystem.config.js` untuk konfigurasi `pm2` di project ini.

Jadi saat saya menjalankan dengan perintah ini:

```bash
pm2 start ecosystem.config.js --env production
```
Malah error seperti ini:

```bash
8|api      | 2025-06-15 16:32 +00:00:     at process.processImmediate (node:internal/timers:485:21)
8|api      | 2025-06-15 16:32 +00:00:     at process.callbackTrampoline (node:internal/async_hooks:130:17) {
8|api      | 2025-06-15 16:32 +00:00:   code: 'EADDRINUSE',
8|api      | 2025-06-15 16:32 +00:00:   errno: -98,
8|api      | 2025-06-15 16:32 +00:00:   syscall: 'listen',
8|api      | 2025-06-15 16:32 +00:00:   address: '::',
8|api      | 2025-06-15 16:32 +00:00:   port: 4000
8|api      | 2025-06-15 16:32 +00:00: }
```

What the hell!?

Tidak ada port yang berjalan di port `4000`. 
Saya sudah periksa semua dengan perintah-perintah linux seperti `lsof`, `netstat`, dll.

Hmmmm... 🤔

Kalau saya jalankan project ini tanpa file `ecosystem.config.js`, bisa aja sih jalan.

```bash
pm2 start src/server.js
```

Tapi ini akan menyulitkan saya, karena harus nambahin argumen lagi diperintah itu agar saat nanti saya
deploy bisa auto restart, logs-nya ada tanggalnya, dan mesti menggunakan environment `production`.

Akhirnya nemu solusi setelah diskusi panjang dengan Gemini.

## Solusi:

### Penyebab masalahnya

Ternyata di konfigurasi project ini ada port yang sama. Yakni port untuk jalanin server expressjs-nya
dan juga port untuk jalankan server Websocket-nya.

Begini bentuk konfigurasinya:

```js
const port = process.env.PORT || 4000;
const socketPort = process.env.PORT || 4001;
```
Lihatlah di sana ada `process.env.PORT`, ini diambil dari file `.env`.
Kalau tidak ada di file `.env` maka nilainya akan otomatis mengginakan yang sebelah,
yakni `4000` dan `4001`.

Karena ada nilai `PORT` di file `.env`. Akhirnya kedua variabel tersebut
akan menggunakan nilai `4000` baik untuk variabel `port` dan `socketPort`.
Sehingga ini mengakibatkan bentrok saat dijalankan oleh PM2.

Jadi...

### Solusinya:

Kita harus bedakan port untuk server express dan websocket.
Jadi saya ubah aja seperti ini:

```js
const port = process.env.PORT || 4000;
const socketPort = process.env.SOCKET_PORT || 4001;
```

Di file `.env` tinggal buat variabel baru dengan nama `SOCKET_PORT`.

Dagh! selesai.