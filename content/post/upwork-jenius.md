---
title: "Set-up Pembayaran Upwork ke Jenius"
slug: upwork-jenius
date: 2021-07-26T22:13:12+08:00
draft: false

type: post

tags:
    - Upwork
    - Jenius
    - Freelance

image: ""
description: "Cara setup Rekening Jenius atau Bank BTPN untuk pencairan dana di Upwork"

typora-root-url: ../../static
---

Sebelumnya, saya menggunakan Mandiri, tapi entah mengapa tidak berhasil dikirim. Saya lupa, apakah dulu pernah menghentikan menggunakan pembayaran ke mandiri atau bukan, yang jelas saat ini berberapa dolar yang saya hasilkan di Upwork masih nyangkut di sana hehe.

Saya berencana menggantinya ke Jenius, karena bisa saya pantau secara digital. Sebelumnya di Mandiri, saya cuma bisa cek lewat ATM kalau ada dolar masuk.

Tapi..

Masalahanya, saya lupa jawaban Security Question akun Upwork saya :cry:

Saya sudah mencoba jawab beberapa kali dengan jawaban yang saya ingat, tapi gagal terus. Parahh…

Namun, untunglah ada cara lain.

Yakni menggunakan Authenticator dan SMS OTP, sehingga akhirnya saya bisa mengubah metode pembayaran ke Bank BTPN atau Jenius.

## SWIFT Code bank BTPN Apa?

Saya menemukannya di tweet:

{{< tweet 963318837885026309 >}}

Awalnya saya coba menggunakan kode `SUNIIDJA`, tapi nama bank yang keluar malah lain. Bukan Bank BTPN.

Akhirnya, meyakinkan diri untuk menggunakan `BTPNIDJA` dan hasilnya:

![swift-code](/img/upwork-jenius/swift-code.png)

Kita juga bisa melihat berapa kurs dolar dan fee yang akan dipotong, jika menggunakan bank ini.

![kurs-dan-fee](/img/upwork-jenius/kurs-dan-fee.png)

## Mengisi Account Holder Bank Information

Berikutnya, kita akan diminta beberapa informasi penting tentang pemegang akun atau rekening.

![info-rekening](/img/upwork-jenius/info-rekening.png)

Silahkan masukan nomer rekening Jeniusmu. Nah untuk bank Code, coba cari di Google pasti ada. Dalam kasus ini, bank kode untuk BTPN/Jenius adalah `213`.

Lalu 4 angka kode terakhir kode cabang, dapat dari mana?

Saya dapat dari:

{{< tweet 1261863279476928517 >}}

Nah, di sana kode cabang adalah `2130101` kita ambil 4 angka terakhir untuk diisi di Upwork. Jadinya `0101` .

Selanjutnya tinggal isi data pribadi seperti nama, alamat, email, no telepon, dan jangan lupa untuk centang *“I attest that I am the owner and have..”*.

Berikutnya kita akan perlihatkan, rangkuman dari data yang diinputkan. Pastikan tidak ada yang salah, terutama nomer rekeneing. Silahkan recheck dengan teliti.