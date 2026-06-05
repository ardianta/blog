---
title: "Fix: Git SSH di Windows tidak bisa push dan clone"
slug: fix-git-ssh-windows
date: 2026-06-05T15:07:00+08:00
draft: true

type: post

tags:
    - Git
    - SSH
    - Windows
    - Problem Solved

image: ""
description: "Cara mengatasi masalah koneksi SSH Git di sistem operasi Windows."
typora-root-url: ../../static
---

Masalah koneksi Git menggunakan SSH di Windows seringkali terjadi karena service `ssh-agent` yang belum berjalan secara otomatis atau konfigurasi key yang tidak terbaca dengan benar.

Berikut adalah langkah-langkah untuk mengatasinya.

## ⚠ Masalah:

Saat melakukan `git clone` atau `git push` menggunakan SSH di Windows, muncul error seperti:

```txt
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```
Atau `ssh-agent` tidak aktif:

```txt
Error connecting to agent: No such file or directory
```

## ✅ Solusi:

### 1. Aktifkan Service SSH Agent di Windows

Buka **PowerShell** sebagai Administrator, lalu jalankan perintah berikut untuk mengaktifkan dan menjalankan `ssh-agent`:

```powershell
# Mengatur startup type menjadi Automatic
Set-Service -Name ssh-agent -StartupType Automatic

# Menjalankan service ssh-agent
Start-Service ssh-agent
```

### 2. Tambahkan SSH Key ke Agent

Setelah agent aktif, tambahkan SSH key Anda (biasanya berada di `~/.ssh/id_rsa` atau `~/.ssh/id_ed25519`):

```bash
ssh-add ~/.ssh/id_ed25519
```

### 3. Konfigurasi File Config (Opsional)

Jika Anda memiliki beberapa akun (misal Github pribadi dan kantor), buat atau edit file config di `~/.ssh/config` dengan konfigurasi seperti berikut:

```text
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519
```

### 4. Tes Koneksi

Terakhir, lakukan tes koneksi ke platform Git Anda (misal GitHub):

```bash
ssh -T git@github.com
```

Jika berhasil, Anda akan melihat pesan sambutan seperti:
`Hi username! You've successfully authenticated, but GitHub does not provide shell access.`

### 5. Perbaiki masalah tidak bisa push dan clone

Sejauh ini SSH untuk git sudah terkonfigurasi dengan benar, tapi saat saya coba untuk push dan clone, saya masih mendapatkan error seperti berikut:

```txt
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
```

Ini disebabkan karena command ssh yang dipakai saat proses clone dan push adalah ssh bawaan dari git bash yang berada di `C:\Program Files\Git\usr\bin`.

Sementara ssh-agent di git bash belum terkonfigurasi dengan benar. Karena itu error ini muncul.

Cara memperbaikinya:

Kita mengubah ssh command yang dipakai saat git memproses clone dan push menggunakan OpenSSH.
Jadi tinggal jalankan command ini untuk mengubahnya:

```powershell
git config --global core.sshCommand C:/Windows/System32/OpenSSH/ssh.exe
```

Setelah itu coba lagi untuk clone dan push. Jika masih error, coba restart git bash atau restart komputer Anda.

Semoga bermanfaat!
