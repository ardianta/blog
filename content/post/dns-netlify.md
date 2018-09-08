---
title: "Error 520: Petanikode Down!"
slug: dns-netlify
date: 2018-09-04T18:05:05+08:00
draft: false

type: post

tags:
    - cloudflare
    - blog
    - netlify

image: "/img/dns-netlify/520.png"
description: "Beberapa hari ini saya sering mendapatkan laporan error 520 dari pengunjung Petanikode. Saya tidak tahu penyebabnya apa..."
---

Beberapa hari ini saya sering mendapatkan laporan **error 520**
dari pengunjung [Petanikode](https://www.petanikode.com/).

![Error pada petanikode](/img/dns-netlify/520.png)

Apakah mungkin karena trafiknya terlalu ramai?

Ataukah Netlify yang tidak mau akur dengan cloudflare?

Saya tidak tahu penyebabnya apa...

Namun, screenshot di atas menujukan kalau server tempat
Petanikode di-hosting telah down.

Sedangkan Cloudflare berusaha melayani request dengan
cache yang ada.

Hmmm....

## Apakah Bandwidth-nya habis?

Netlify memberikan kuota bandwidth sampai 100GB per bulan.
Kalau dilihat dari analytic Cloudflare...

![Analytic Cloudflare](/img/dns-netlify/bandwidth.jpg)

Kuota bandwidth yang dihabiskan Petanikode selama sehari
sekitar 500MB. Dalam sebulan, bisa mencapai 15GB.

Menurut saya ini bukan masalah pada bandwidth.

Mungkin saja Netlify dan Cloudflare tidak mau akur,
karena beberapa hari yang lalu saya pernah membaca
blog netlify yang memberikan alasan: ["Mengapa netlify tidak perlu pakai cloudflare"](https://www.netlify.com/blog/2017/03/28/why-you-dont-need-cloudflare-with-netlify/)

## Percobaan Melepas Cloudflare

Sebelum melepas cloudflare, saya akan coba dulu
di blog saya yang lain, yaitu [lombokfoss.com](https://www.lombokfoss.com).

Blog ini masih sepi pengunjung, jadi saya tidak
akan khwatir kalau down beberapa hari karena propagasi.

Saya langsung mengubah Nameserver di IDWebhost
agar mengarah ke Netlify.

![DNS IDwebhost](/img/dns-netlify/idwebhost.png)

Lalu beberapa menit kemudian, saya verifikiasi
konfigurasi DNS di Netlify.

...dan berhasil.

![Konfigurasi DNS Netlify](/img/dns-netlify/netlify.png)

Webnya masih mengudara hingga saat ini.
Tidak ada propagasi.