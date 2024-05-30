---
title: "[Solved] Error Push file besar ke Github"
slug: git-lfs
date: 2024-05-30T12:26:40+08:00
draft: false

type: post

tags:
    - tag

image: "/img/git-lfs/git-lfs.avif"
description: "Di sebuah repository private, ada file besar berupa arsip rar. Ukurannya lebih dari 100MB. Ketika saya melakukan push ke Github, ini akan tertolak otomatis oleh Github."
---

Di sebuah repository private, ada file besar berupa arsip rar.
Ukurannya lebih dari 100MB.

Ketika saya melakukan push ke Github, ini akan tertolak otomatis oleh Github
karena mencapai batas maksimal ukuran file yang sudah ditetapkan.

```txt
GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
```

![Error push file besar ke github](/img/git-lfs/git-lfs.avif)

Saya mau hapus file tersebut, tetapi sudah terlanjur masuk ke commit.

Lalu gimana donk?

Akhirnya saya nemu Git LFS (Large Filesystem), 
dari jawaban Stackoverflow ini: https://stackoverflow.com/a/65498452.

Langsung saja saya coba install di Fedora dengan perintah:

```bash
curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.rpm.sh | sudo bash
```

Install dengan dnf:

```bash
sudo dnf install git-lfs
```

Git LFS sendiri merupakan ekstensi tambahan dari Git. Jadi, kita perlu mengintalnya dulu
agar bisa menggunakannya di dalam git.

Nah, setelah terinstal.. kita tinggal init di repo dengan cara seperti ini.

```bash
git lfs install
```

Setelah itu, lakukan migrasi file besarnya dengan cara:

```bash
git lfs migrate import --include="path/to/file"
```

Contoh:

Di kasus repo saya, karena file `.rar` jadi perintahnya seperti ini:

```bash
git lfs migrate import --include="*.rar"
```

Ini artinya saya akan membuat semua file arsip rar akan di handle dengan git LFS.

..dan akhirnya saya coba lakukan push ke Github lagi, hasilnya bisa.

Mantap!