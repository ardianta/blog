---
title: "Serius Nih! Cloudflare tidak Melakukan Propagasi"
slug: cloudflare-propagasi
date: 2017-12-24T18:31:41+08:00
draft: false

tags:
    - DNS
    - Cloudflare

image: "/img/dns/domain-netlify.png"
description: "Propagasi bertujuan untuk mengumumkan alamat IP baru ke semua jaringan internet. Propagasi biasanya membutuhkan waktu 24 jam sampai bahkan 1 minggu."
---

Biasanya kalau kita ganti server hosting, lalu alamat IP domain
diganti dengan server yang baru, maka membutuhkan masa propagasi.

Propagasi bertujuan untuk mengumumkan alamat IP baru ke semua jaringan internet.
Propagasi biasanya membutuhkan waktu 24 jam sampai bahkan 1 minggu.

Pengalaman kemarin, saya pindah-pindah server hosting dari Blogger
ke Gitlab, dari Gitlab ke Github.

Propagasinya lama dan domain belum bisa diakses sampai masa propagasi selesai. 
Kira-kira 2--3 hari baru bisa selesai.

Tapi kali ini, tidak ada propagasi.

Saya memindahkan hosting dari Github ke Netlify. Lalu mengubah pengaturan DNS 
di Cloudflare.

![DNS Netlify di Cloudflare](/img/dns/dns-netlify.png)

Tapi di Netlify masih tanda seru, kenapa ya?

![DNS di Netlify](/img/dns/domain-netlify.png)

Meskipun begitu, domainnya tetap mengarah ke Netlify.

Saya coba-coba melakukan beberapa perubahan. Lalu, 
melakukan deploy ke Netlify.

Hasilnya: bernar, website yang dipakai sekarang dari Netlify.

Wih! ini artinya tidak perlu propagasi donk 😮.

Cloudflare sendiri sudah menerbitkan blog yang
berjudul [Never Deal With DNS Propagation Again](https://blog.cloudflare.com/never-deal-with-dns-propagation-again/).

Tapi dulu pas migrasi dari Gitlab ke Github, butuh waktu propagasi.

Saya jadi bingung?