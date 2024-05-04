---
title: "Hal-hal yang baru saya ketahui setelah Belajar Ulang C dan C++"
slug: belajar-c-lagi
date: 2024-05-02T01:16:47+08:00
draft: true

type: post

tags:
    - tag

image: ""
description: ""

typora-root-url: ../../static
typora-copy-images-to: ../../static/img/belajar-c-lagi/
---

Saya belajar C dan C++ waktu kuliah dulu. Mulai saat semester 3, saya belajar otodidak kedua bahasa ini.
Ya, maklum di kampus soalnya nggak diajarin.

Tujuan belajar C dan C++ waktu itu, ingin paham gimana cara coding game atau game programming.
Sampai saya ulang-ulang dan menghafal sintaks untuk coding SDL di C dan C++. Haha, sekarang sih udah lupa.

Tapi saat ini, saya sudah paham Game Programming dan pernah membuat game 2D dan 3D pakai Unity
dan bahasa C#. Yaa.. pakai Game Engine, jadi lebih mudah.

Sekarang saya coba belajar lagi C dan C++, buat refresh ingatan dan juga mau update konten
[tutorial C](https://www.petanikode.com/tutorial/c) dan [C++ di petani Kode](https://www.petanikode.com/tutorial/cpp), hehe.

Oke, jadi ini hal-hal baru yang saya temukan:

## 1. Di C ternyata tidak ada true dan false

Ya, benar di C belum ada kata kunci `true` dan `false` untuk tipe
data *boolean*.

Tapi ini bisa diakali dengan integer `0` dan `1` untuk menggantikan
`true` dan `false`.

Ada juga yang membuat macro-nya seperti ini:

```c
#define true 1
#define false 0
```

Kalau ga mau buat sendiri, ada juga macro dari header `<stdbool.h>`.

Tapi sekarang di versi `C23`, kata kunci `true` dan `false` sudah
ditambahkan secara default di bahasa C.

## 2. Ternyata di Struct bisa simpan Fungsi

Penasaran dengan OOP di C, akhirnya saya mencari tahu.
Coba bertanya di ChatGPT tapi jawabannya kurang memuaskan.

Lalu saya nemu buku Extreme C di PackPub dan membacanya.
Ternyata OOP bisa dilakukan di C, tapi dengan cara yang berbeda.

Salah satu caranya, kita bisa simpan fungsi di dalam Struct.

Hah! emang bisa?

Ya bisa donk.

Kalau di C, yang disimpan adalah pointer yang mengarah ke fungsinya.
Sedangkan kalau di C++ udah bisa secara langsung.. tanpa harus pakai pointer.

Contoh di C:

```c
struct Player
{
    char* name;
    int hp;
    void (*doAttack)();
};

void doAttack(){ ... }
```

Contoh di C++:

```cpp
struct Player {
    string name;
    int hp;
    void attack(){
        // ...
    }
}
```

## 3. Cara pakai Makefile

Dulu saya cuma belajar C dan C++ cuma sampai fungsi dan OOP.
Belum sampai membuat project dan menggunakan library secara modular, 
jadi kurang tau cara pakai Makefile.

Tapi saat ini sudah paham berkat tutorial dari: https://makefiletutorial.com/

Selain itu, saya juga sempat nyoba [conan](https://conan.io/) untuk package manager C++.

## 4. Konsep Preprocessor dan Macro

Dulu saya sulit memahami konsep ini. Tapi setelah coba belajar Rust,
saya nemu kembali konsep Macro.

Tapi karena saya sudah belajar SASS dan CSS. 
Konsep ini akhirnya bisa saya pahami. Kurang lebih, preprocessor di C
sama seperti preprocessor pada SASS. 11 12 dah!

Preprocessor itu adalah proses yang dilakukan sebelum kode
program diproses oleh compiler. Dengan begitu kita bisa buat Macro
menggunakan direktif yang ada. Direktif ini untuk ngasih tau ke preprocessor..
apa yang harus dilakukan.

## 5. Sejarah LLVM

Saya tahu dua compiler yang sering sering dipakai untuk coding C/C++
adalah [GCC](https://gcc.gnu.org/) dan [LLVM](http://llvm.org/). Tapi belum tahu sejarah mengapa LLVM dibuat.

Setelah belajar ulang, ternyata si LLVM awalnya dibuat oleh Apple untuk
compile Objective-C. Lalu ditambahkan juga support untuk compile C.

Sementara GCC, ya udah tahu si dari project GNU. Namun, yang baru
saya tahu yang LLVM ini. Sering dengar, tapi ga tau asal-usulnya.

## 6. Pakai Namespace, Bukan Class

Ternyata ada yaa programmer yang ga mau pakai class. Dia cuma ngandelin namespace doang.

Saya panggil dia sepuh, karena skill coding C++ dan openGL-nya luar biasa jago.
Dalam salah satu live stream-nya dia mengatakan: *"Don't use fucking class, I use namespace instead"*

<!-- {{< youtube "" >}} -->

Hahaha, tapi ini pilihan aja sih. Bebas mau pakai yang mana dan tergantung kasus yang dihadapi.
Kalau bisa prosedural ya pakai aja prosedural, gak perlu dipaksakan OOP. Karena bahasa C++ kan multi paradigma.

Jadi, dari video live stream ini, saya baru tahu.. ternyata bikin logic di dalam namespace tanpa class juga bisa.