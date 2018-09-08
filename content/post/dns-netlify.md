---
title: "Error 520: Petanikode Down!"
slug: dns-netlify
date: 2018-09-04T18:05:05+08:00
draft: true

type: post

tags:
    - tag

image: ""
description: ""
---

Beberapa hari ini saya sering mendapatkan laporan **error 520**
dari pengunjung [Petanikode](https://www.petanikode.com/).

![Error pada petanikode](/img/dns-netlify/520.png)

Apakah mungkin karena trafiknya terlalu ramai?

Ataukah Netlify yang tidak mau akur dengan cloudflare?

Saya tidak tahu penyebabnya apa...

Namun, screenshot di atas menujukan kalau server tempat
Petanikode dihosting telah down.

Sedangkan Cloudflare berusaha melayani request dengan
cache yang ada.

Hmmm....

## Apakah Bandwidth-nya habis?

Netlify memberikan kuota bandwidth sampai 100GB per bulan.
Kalau dilihat dari analytic Cloudflare...

![Analytic Cloudflare]()

Kuota bandwidth yang dihabiskan Petanikode selama sehari
sekitar 500MB. Dalam sebulan, bisa mencapai 15GB.

Menurut saya ini bukan masalah pada bandwidth.

Mungkin saja Netlify dan Cloudflare tidak mau akur,
karena beberapa hari yang lalu saya pernah membaca
blog netlify yang mengungkapkan: "Mengapa netlify
tidak perlu pakai cloudflare"

## Percobaan Melepas Cloudflare

Sebelum melepas cloudflare, saya akan coba dulu
di blog saya yang lain, yaitu [lombokfoss.com](https://www.lombokfoss.com).

Blog ini masih sepi pengunjung, jadi saya tidak
akan khwatir kalau down beberapa hari karena propagasi.

Saya langsung mengubah Nameserver di IDWebhost
agar mengarah ke Netlify.

![DNS IDwebhost]()

Lalu beberapa menit kemudian, saya verifikiasi
konfigurasi DNS di Netlify.

...dan berhasil.

![Konfigurasi DNS Netlify]()

Webnya masih mengudara hingga saat ini.
Tidak ada propagasi.