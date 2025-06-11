---
title: "[Solved] Incompatible Java Version and Gradle Version di Project Android"
slug: fix-incompatible-java-gradle
date: 2025-06-02T15:30:39+08:00
draft: false

type: post

tags:
    - Problem Solved
    - Java
    - Android

image: ""
description: "Your build is currently configured to use incompatible Java 21.0.6 and Gradle 6.1.1. Cannot sync the project."

typora-root-url: ../../static
---

Kalau sering proyekan android, masalah incompatibility ini akan sering ditemui.
Tiap-tiap project menggunakan konfigurasi yang berbeda. Versi Java dan Gradlenya juga beda-beda.
Ini kadang membuat frustrasi di awal kita setup project.

## Masalah:

```txt
Your build is currently configured to use incompatible Java 21.0.6 and Gradle 6.1.1. Cannot sync the project.

We recommend upgrading to Gradle version 8.12.

The minimum compatible Gradle version is 8.5.

The maximum compatible Gradle JVM version is 13.

Possible solutions:
 - Upgrade to Gradle 8.12 and re-sync
 - Upgrade to Gradle 8.5 and re-sync
```

## Solusi:

Cek Gradle compatibility di:

- https://docs.gradle.org/current/userguide/compatibility.html

Pastikan Versi Java yang digunakan di Android Studio kompatible dengan versi gradle yang digunakan di dalam project.

Cara mengatur versi Java dan Gradle, bisa dari setingan android studio dan juga Project Structure.

Referensi:

- https://stackoverflow.com/questions/79049863/android-studio-ladybug-your-build-is-currently-configured-to-use-incompatible-j

Selamat mencoba, semoga berhasil!