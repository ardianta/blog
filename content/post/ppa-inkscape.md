---
title: "Install Inkscape Terbaru dari PPA Resmi"
slug: ppa-inkscape
date: 2018-02-06T16:29:16+08:00
draft: false

type: post

tags:
    - Inkscape
    - Linux

image: "/img/inkscape/ppa-inkscape.png"
description: "Saya menggunakan Inkscape 0.91, kadang sering stuck saat melakukan dragging dengan tombol spasi dan mouse."
---

Saya menggunakan Inkscape 0.91, kadang sering *stuck*
saat melakukan *dragging* dengan tombol spasi dan mouse.

Mungkin saja di versi 0.92 sudah diperbaiki. Oya, versi
0.91 ini dirilis pada tahun 2015, sedangkan 0.92 pada
tahun 2017.

Saya ingin upgrade ke 0.92, namun belum tersedia
di repositori resmi.

Akhirnya menemukan PPA ini:

```bash
sudo add-apt-repository ppa:inkscape.dev/stable
sudo apt-get update
```

Dan sekarang saya sudah bisa install Inkscape 0.92, yay!

![PPA Inkscape](/img/inkscape/ppa-inkscape.png)

Sumber: https://code.launchpad.net/~inkscape.dev/+archive/ubuntu/stable