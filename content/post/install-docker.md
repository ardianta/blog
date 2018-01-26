---
title: "Install Docker di Linux Mint 18"
slug: install-docker
date: 2017-12-30T17:41:27+08:00
draft: false

type: post

tags:
    - Docker
    - Linux
    - Mint

image: "/img/docker/versi-docker.png"
description: "Cara Install Docker di Linux Mint 18"
---


Pertama lakukan update:

```bash
sudo apt-get update
```

Berikutnya install paket-paket yang dibutuhkan:

```bash
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```

Tamhakan GPG Key resmi Docker:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
Versifikasi fingerprint `9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88`

```bash
sudo apt-key fingerprint 0EBFCD88
```

outputnya:

```bash
pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22
```

Tambahkan almat repository Docker untuk Ubuntu xenial,
karena Linux Mint 18 setara dengan Ubuntu Xenial:

```bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   xenial \
   stable"
```

Setelah itu lakukan update:

```bash
sudo apt-get update
```

Terakhir, tinggal install Docker:

```bash
sudo apt-get install docker-ce
```

Setelah itu, coba cek dengan perintah `docker --version`.

![Versi Docker](/img/docker/versi-docker.png)


Referensi: [docs.docker.com](https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#install-docker-ce-1)