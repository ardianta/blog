---
title: "Agar Hugo tidak melakukan HTTP Request saat Offline"
slug: hugo-offline
date: 2018-03-18T00:37:25+08:00
draft: false

type: post

tags:
    - blog
    - hugo

image: ""
description: ""
---

Saya menggunakan shortcode *twitter* dan *instagram* di dalam postingan.
Setiap kali mau render, pasti akan melakukan HTTP Request ke API twitter dan instagram.

Sehingga, apabila kita render saat dalam keadaan offline, maka akan menghasilkan
error seperti ini:

![Error Call GetJSON](/img/hugo/error-getjson.png)

Cara mencegahnya:

Kita cukup mengisi alamat `baseurl` dengan `localhost`:

```toml
baseurl = "http://localhost"
```

Maka Hugo tidak akan melakukan HTTP Request lagi. 😜