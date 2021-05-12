---
title: "Fix: Tombol Meta/Windows tidak Membuka Menu di KDE"
slug: fix-kde-menu-meta
date: 2021-05-11T07:20:47+08:00
draft: false

type: post

tags:
    - Kubuntu
    - Linux
    - KDE

image: ""
description: ""

typora-root-url: ../../static
---

## ⚠ Masalah:

Tombol Meta atau Windows tidak berfungsi untuk membuka menu launcher di KDE. Saat ini saya pakai Kubuntu 20.04 dengan KDE Plasma 5.

## ✅ Solusi:

Buka **Global Shortcut**, bisa dari *System Settings* atau juga menu launcher.

Kemudian, masuk ke menu **Plasma**, lalu tambahkan `Alt`+`F1` sebagai
key shortcut untuk **Activate Application Menu Widget**.

![kde global shortcut](/img/fix-kde-menu-meta/kde-global-shortcut.png)

Jika belum bisa, coba klik kanan pada **Menu launcher** lalu pilih **Configure Application Menu**.

![configure-application-menu](/img/fix-kde-menu-meta/configure-application-menu.png)

Setelah itu, tambahkan `Alt`+`F1` sebagai shortcut untuk membuka menu tersebut.

![application menu shortcut](/img/fix-kde-menu-meta/application-menu-shortcut.png)