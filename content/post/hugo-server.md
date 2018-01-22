---
title: "Binding Server Hugo ke IP LAN"
slug: hugo-server
date: 2018-01-23T02:03:56+08:00
draft: false

type: post

tags:
    - Hugo

image: "/img/hugo-server/server-hugo.png"
description: "Cara menjalankan server hugo untuk di-binding dengan IP LAN"
---

Jadi ceritanya hari ini saya dapat *feedback* untuk revisi pekerjaan 
pembuatan template Hugo.

![Revisi Template](/img/hugo-server/revisi.jpg)

Kebanyakan masalahnya pada tata letak dan *responsive*.

Saya ingin mengetes langsung dengan HP. Sebenarnya bisa langsung dilakukan di
browser, tapi saya maunya langsung dari HP saja.

Kondisi topologi jraingan saya:

```
Modem Wifi --- Laptop
|
|
HP
```

Alamat IP laptop saya `192.168.1.104` bisa diakses melalui LAN.

Ketika mencoba mengakses alamat IP tersebut dari HP, yang muncul adalah
server Apache. Karena di Laptop saya sudah terpasang server Apache.

Namun, saya coba jalankan server Hugo dengan perintah berikut:

![Menjalankan Server Hugo](/img/hugo-server/server-hugo.png)

Malah tidak bisa diakses. Baik dari HP maupun lapop.

![Akses Server Hugo](/img/hugo-server/akses-server.jpg)

Ini karena parameter `-b` adalah untuk mengeset `BaseURL` saja.

Solusinya:

Kita harus bind IP `0.0.0.0` atau IP LAN komputernya.

```bash
hugo server --baseUrl=http://192.168.0.104/ --bind="0.0.0.0"
```

Selamat mencoba...