---
title: "Cegah Ghost Spam di Google Analytic"
slug: ghost-spam
date: 2019-03-01T20:17:20+08:00
draft: false

type: post

tags:
    - tag

image: "/img/ga/filter.png"
description: "Entah ini disengaja atau tidak, laporan page dari web rmco.id masuk ke google analytic petanikode yang membuat saya bingung."
---

Pada tanggal 24 kemarin, trafik di petanikode tiba-tiba meningkat 2x lipat
dari biasanya.

![Ghost Spam Trafik](/img/ga/ghost-spam.png)

Apakah ini bagus?

Tentu saja tidak, karena trafiknya bersal dari spam.

Entah ini disengaja atau tidak, laporan page
dari web `rmco.id` masuk ke google analytic petanikode
yang membuat saya bingung.

Tapi untungnya saya menemukan solusinya di https://carloseo.com/removing-google-analytics-spam/

Langkah-langkah pencegahannya:

1. Masuk ke Admin -> Filter
2. Buat Filter Baru
3. Pilih Include
4. Masukan alamat domain di dalam filter patterrn
5. Simpan

![Filter Google Analytic](/img/ga/filter.png)

Maka laporan trafik yang akan masuk ke Google Analytic
hanya akan menampilkan dari domain `www.petanikode.com` saja.