---
title: "Percepat Scroll Zoom Figma di Firefox"
slug: figma-scroll-firefox
date: 2021-02-05T23:58:58+08:00
draft: false

type: post

tags:
    - tag

image: ""
description: "Cara mempercepat Zoom in dan Zoom out Figma di Firefox"
typora-root-url: ../../static
---

Hari ini saya banyak menghabiskan waktu di Figma, mulai dari belajar 
desain UI/UX hingga belajar menggunakan Figma untuk kebutuhan sehari-hari.

Tapi ada masalah kecil yang saya alami saat membuka Figma di Firefox.

Apa itu?

Zoom in dan zoom out Figma di Firefox terasa lambat.
Tidak seperti di Chrome.

Tapi tentang, saya sudah ketemu solusinya:

1. Buka `about:config` di address bar
2. Lalu cari `mousewheel.with_control.delta_multiplier_y`
3. Ubah nilainya dari `100` menjadi `500`

![setting-mousewheel-firefox](/img/figma-scroll-firefox/setting-mousewheel-firefox.png)

Sekarang saat kita mengekan tombol Ctrl+Scroll mouse, maka kecepatannya akan bertambah cepat.

Jika ingin lebih cepat lagi, naikin aja nilai `delta_multipier_y` jadi lebih tinggi.

Solusi ini saya dapatkan dari forum https://spectrum.chat/figma/feature-requests/zooming-speed-with-ctrl-mouse-scroll-on-firefox-differs-from-googles-chrome~250fac37-73e9-4319-b38a-297bf4db5843