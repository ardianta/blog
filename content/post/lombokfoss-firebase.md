---
title: "Migrasi Lombokfoss ke Hugo dan Firebase"
slug: lombokfoss-firebase
date: 2017-11-06T23:44:45+08:00
draft: false

tags:
    - blog

image: "img/lombokfoss/ssl.png"
description: "Rencananya saya mau pakai Hugo dan hostingnya di Firebase, lalu untuk DNS saya masih percayakan pada CloudFlare."
---

Minggu ini saya melakukan migrasi blog saya [Lombokfoss](https://www.lombokfoss.com), karena nggak pernah diurus.

Rencananya saya mau pakai Hugo dan hostingnya di Firebase, lalu untuk DNS
saya masih percayakan pada CloudFlare.

Saya baru pertama kali mencoba hosting di Firebase dan mengkonfigurasi
kustom domainnya.

Di CloudFlare saya set seperti ini:

![Konfigurasi DNS Cloudflare](/img/lombokfoss/dns-cloudflare.png)

Hampir satu minggu saya tunggu, tapi belum juga bisa.

Ternyata masalahanya cuma di pengaturan SSL Cloudflare saja.

Harus diset __"Full"__:

![Pengaturan SSL Cloudflare](/img/lombokfoss/ssl.png)

Setelah beberapa menit, akhirnya bisa juga dibuka di https://www.lombokfoss.com/.

Kenapa bisa begitu ya?

Dugaan saya kemungkinan SSL Cloudflare bentrok dengan SSL Firebase. Sehingga harus diset __"Full"__. Tapi, sepertinya dugaan ini salah.

![SSL Cloudflare](https://www.petanikode.com/img/cara-menambahkan-ssl-untuk-github-pages/cloudflare_ssl_modes.png)

Ah yang penting sudah bisa sekarang.

Pekerjaan selanjutnya adalah membuat template.