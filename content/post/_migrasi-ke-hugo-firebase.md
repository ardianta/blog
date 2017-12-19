+++
title = "Migrasi Lombokfoss ke Hugo dan Hosting di Firebase"
slug = "dns-cloudflare-firebase"
images = ["/2016/10/image.jpg"]
description = "Setting DNS Firebase di Cloudflare"
categories = ["category"]
tags = ["tag1", "tag2"]
draft = true
+++

Minggu ini saya melakukan migrasi blog saya Lombokfoss, karena nggak pernah diurus.

Rencananya saya mau pakai Hugo dan hostingya di Firebase, lalu untuk DNS
saya percayakan pada CloudFlare.

Saya baru pertama kali mencoba hosting di Firebase dan mengkonfigurasi
kustom domainnya.

Di CloudFlare saya set seperti ini:

![]()

Hampir satu minggu saya tunggu, tapi belum juga bisa.

Ternyata masalahanya cuma di pengaturan SSL Cloudflare saja.

Harus diset __"Full"__:

![Pengaturan SSL Cloudflare]()

Setelah beberapa menit, akhirnya bisa juga dibuka di https://www.lombokfoss.com/.

Kenapa bisa begitu ya?

Dugaan saya kemungkinan SSL Cloudflare bentrok dengan SSL Firebase. Sehingga harus diset __"Full"__.

![SSL Cloudflare](https://www.petanikode.com/img/cara-menambahkan-ssl-untuk-github-pages/cloudflare_ssl_modes.png)
