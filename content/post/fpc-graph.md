---
title: "Unit graph untuk Free Pascal di Linux"
slug: fpc-graph
date: 2021-08-06T15:30:39+08:00
draft: false

type: post

tags:
    - Pascal

image: ""
description: ""

typora-root-url: ../../static
---

## Masalah:

Saat compile program pascal yang menggunakan unit `graph`, ia tidak bisa dan dapat persan error seperti ini:

```
program1.pas(2,10) Fatal: Can't find unit graph used by program1
```

Ini disebabkan karena unit `graph` belum terinstal di komputer. Saya menemukan diskusi untuk solusi masalah ini di forum: https://forum.lazarus.freepascal.org/index.php?topic=23777.0

## Solusi:

Cek unit Free Pascal yang terinstal di direktori `/usr/lib`.

![usr lib fpc unit](/img/fpc-graph/usr-lib-fpc-unit.png)

Dari sana kita bisa tahu library `graph` apa aja yang sudah terinstal. Pada gambar di atas ada `ggigraph` dan `ptcgraph`.

O ya, *Free Pascal Compiler* (FPC) akan mencari file `.o` dan `.ppu` saat kita melakukan compile dan di program kita menggunakan Unit di pascal.

Contoh:

```pascal
uses graph;
```

Maka FPC akan menjadi file `graph.ppu` dan `graph.o` di dalam folder library (`/usr/lib/fpc/units`).

> Alamat path library tergantung dari versi Free Pascal yang digunakan

Karena file `graph.ppu` dan `graph.o` tidak ada maka kita bisa gunakan alternatif seperti `ggigraph` dan `ptcgraph`.

Pada solusi yang saya coba, ternyata `ptcgraph` bisa menjadi pengganti `graph` di Linux.

Tapi untuk menggunakan unit `ptcgraph` kita harus menginstal unit pendukungnya terlebih dahulu.

```bash
sudo apt install fp-units-gfx fp-units-fcl
```

Setelah itu, pada kode program pascal kita bisa gunakan `prcgraph`.

![uses ptcgraph](/img/fpc-graph/uses-ptcgraph.png)

Selamat mencoba, semoga berhasil!