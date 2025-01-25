---
title: "[Solved] Nginx 502 Error: Cuma gara-gara console.err()"
slug: nginx-502-error
date: 2025-01-25T15:08:35+08:00
draft: false

type: post

tags:
    - tag

image: "/img/nginx-502-error/git-diff-caused-502-error.png"
description: "Error 502 di server Nginx, ternyata disebabkan oleh hal sepele."
---

Kemarin terjadi masalah di project yang sedang saya handle.
User tidak bisa upload file ke backend dan dapat respon:

```txt
502 Bad Gateway
```

Ini adalah respon error dari Nginx. Seharian saya debug konfigurasi Nginx,
mengubah beberapa hal seperti ukuran buffer untuk proxy dan ukuran maksimal
upload file yang dibolehkan untuk di-upload. Tapi tetap tidak bisa. 
Tetap saja respon servernya *502 Bad Gateway*.

Di server, saya menjalankan service backend API di port `4000`. Ini adalah
service yang akan menghandle file upload. Saya tidak mencurigai masalahnya ada
di service ini. Karena memang error-nya di sisi Nginx.

Tapi ternyata saya salah..

Setelah inspect logs Nginx, saya nemu sebuah clue. Katanya di logs itu:

```txt
[error] *407 upstream prematurely closed connection while reading response header from upstream
```

Saya kurang paham maksud errornya. Tapi di sini dapat saya duga, kalau ada masalah di `upstream`, yakni service yang berjalan di port `4000`.

Selain itu, Error di Nginx juga ngasi tau.. kalau itu "Bad Gateway" yang artinya ada masalah di reverse proxy servicenya.

Setelah ku coba cek endpoint untuk upload file di service `4000`, berulah ketemu sumber masalahnya.
Ternyata di sana saya menggunakan `console.err`.

```js
console.err("Error:", err);
```

Hahaha, setelah seharian menghabiskan waktu buat debug Nginx. Ternyata di sini masalah utamanya.
Bangkeeeeee!!!!

![Bangkeeeee](https://i.giphy.com/4qx6IRdg26uZ3MTtRn.webp)

Di sana yang benar seharusnya:

```js
console.err("Error:", err);
```

Bukan:

```js
console.err("Error:", err);
```

Anehnya, mengapa Nodejs meleawatkan ini. Mengapa sewaktu menjalankan servernya tidak menampilkan error, kalau itu sintaks yang salah.

Ahh iya, aku lupa aktifin eslint dan Nodejs gak peduli dengan sintaks error seperti ini.
Oh iya, project ini juga menggunakan babel, mungkin babel juga nggak ngecek sintaksnya saat proses build.

Project ini adalah project warisan dari orang India.
Kodenya berantakan, kalau ubah-ubah sesuastu biasanya akan menyebabkan error lainnya.
Jadi mesti hati-hati.

![Git diff solved 502 error](/img/nginx-502-error/git-diff-caused-502-error.png)

Sekarang sudah tidak lagi dapat Error 502, dan upload file sudah work kembali.