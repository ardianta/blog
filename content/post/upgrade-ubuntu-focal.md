---
title: "Masalah saat Upgrade ke Ubuntu 20.04 (Focal)"
slug: upgrade-ubuntu-focal
date: 2020-07-06T18:04:46+08:00
draft: false

type: post

tags:
    - tag

image: ""
description: "Error dan masalah yang saya temukan saat upgrade Kubuntu 18.04 ke
Kubuntu 20.04"
---

Hari ini saya melakukan upgrade Ubuntu 18.04 ke 20.04, sebenarnya versi ini
masih belum stabil. Menurut pengumuman resminya, nanti tanggl 6 agustus
akan dirilis versi stabilnya.

Tapi, saya malah **nekat upgrade**.. karena ingin mencoba fitur-fitur baru
yang ada di sana.

Hasilnya:

Mengecewakan!

Karena saya dapat beberapa masalah.. huh! :triumph:

## 1. Dolphin Tidak Bisa buka File

Setelah selesai upgrade, saya langsung membuka file manager Dolphin, akan
tetapi dapat pesan error.

```txt
 Error loading '/usr/lib/qt/plugins/kf5/kio/file.so'
```

✅ Solusi:

Menjalankan Dolphin dengen `debus-launch`:

```bash
dbus-launch dolphin
```

Referensi: [Forum Manjaro](https://forum.manjaro.org/t/unable-to-create-io-slave-klauncher-said-error-loading-usr-lib-qt-plugins-kf5-kio-file-so/25866/2)

## 2. Wifi Tidak Mau Connect

Setelah Restart.. WiFi gak bisa connect. Tombol *connect* gak bisa ditekan,
gak ada muncul loading progress. Parah!

Beberapa upaya yang saya lakukan:

- Gunakan USB Wifi (❌ gagal karena gak terdetek)
- Gunakan LAN untuk konek ke Modem (❌ gagal, gak tahu kenapa)
- Gunakan Modem USB untuk konek internet (✅ Berhasil)

![Jaringan Internet](/img/upgrade-ubuntu-focal/net.png)

Oke, sekarang saya sudah terhubung dengan internet.
Berikutnya, saya harus mencari tahu solusi dari masalah ini.

Pertama, saya coba update dan upgrade dulu:

```bash
sudo apt update && sudo apt upgrade
```

Upgrade gagal karena:

```bash
dian@petanikode~/b/ardianta> sudo apt upgrade 
E: dpkg was interrupted, you must manually run 'sudo dpkg --configure -a' to correct the problem.
```

Mari kita perbaiki dulu, dengan mengetik `sudo dpkg --configure -a`.

![configure dpkg](/img/upgrade-ubuntu-focal/configure-dpkg.png)

Lama juga nunggunya..

Pada proses ini saya memperhatikan, beberapa paket memang belum selesai
dikonfigursi dan juga beberapa paket membutuhkan koneksi internet untuk
konfigurasi.

![Configure paket](/img/upgrade-ubuntu-focal/configure-paket.png)

Setelah semua konfigurasi selesai, saya mencoba lagi melakukan update dan upgrade.

Hasilnya, masalah teratasi..

✅ Solusi:

1. Cara cara agar bisa terhubung dengan intenret;
2. Jalankan perintah `sudo dpkg --configure` 
3. Lakukan update dan upgrade

Jika solusi ini masih belum mempan, coba install driver WiFi-nya.

## 3. Audio Tidak ada Suara

Volume suara tidak bisa diperbesar atau dikecilkan kerena:

"No input or output devices found"

![Audio error](/img/upgrade-ubuntu-focal/audio.webp)

Artinya, sound card gagal dibaca..


✅ Solusi:

Solusinya sama seperti masalah nomer 2, yakni harus melakukan:

1. Cara cara agar bisa terhubung dengan intenret;
2. Jalankan perintah `sudo dpkg --configure` 
3. Lakukan update dan upgrade

## Akhir Kata..

Lain kali mungkin saya akan berhati-hati, karena versi yang belum stabil itu
rentan dengan bugs.

![Ubuntu 20.04](/img/upgrade-ubuntu-focal/ubuntu-20-04.webp)

Okeh, semoga Ubuntu 20.04 lancar di laptopku.