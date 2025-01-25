---
title: "Fix: Kde Flicker Bug"
slug: fix-kde-flicker-bug
date: 2021-05-11T09:24:09+08:00
draft: false

type: post

tags:
    - KDE
    - Kubuntu
    - Linux
    - Problem Solved

image: ""
description: ""
typora-root-url: ../../static
---

## ⚠ Masalah:

Terjadi *flicker* atau layar berkedip saat resize window di Kubuntu 20.04.
Mungkin saja VGA Card yang digunakan laptop saya tidak mampu menghandle animasinya.

Video Demo:

{{< youtube nZ1BZ0LmYSM >}}

## ✅ Solusi:


Buka, **Settings**->**Display and Monitor**.
Lalu ubah settingan *compositor*. 

![compositor-settings](/img/fix-kde-flicker-bug/compositor-settings.png)

Saya gunakan **OpenGL 2.0** sebagai rendering backend. Entah mengapa, kalau
pakai yang lain terjadi *flicker*.