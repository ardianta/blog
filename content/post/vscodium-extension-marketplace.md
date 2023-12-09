---
title: "Cara Mengubah Extension Marketplace pada VS Codium, Biar Bisa pakai Extension dari Microsoft"
slug: vscodium-extension-marketplace
date: 2023-12-09T09:02:56+08:00
draft: false

type: post

tags:
    - VS Code
    - VScodium
    - Text Editor
    - Coding

image: "/img/vscodium-extension-marketplace/vscodium-vscode-marketplace.png"
description: "VSCodium secara default menggunakan extension dari open-vsx.org, lalu gimana cara menggantinya agar menggunakan Visual Studio Marketplace dari Microsoft?"

typora-root-url: ../../static
typora-copy-images-to: ../../static/img/vscodium-extension-marketplace/
---

VSCodium adalah versi VS Code yang dikelola oleh komunitas.
Bukan dikelola oleh tim Microsoft.

Jadi extension buatan Microsoft tidak berlaku di sini.

Mengapa?

Ya, mungkin karena komunitas menganggap:

Binary VS Code yang dikeluarkan oleh Microsoft mengandung analityc (telemetry)
yang mengirim data secara diam-diam ke Microsoft.

Telementry ini berpotensi melakukan spy-spy hehe.

VS Codium menggunakan extension dari [open-vsx.org](https://open-vsx.org/),
sedangkan VS Code menggunakan ekstension dari [Visual Studio Marketplace](https://marketplace.visualstudio.com/VSCode).

Ada beberapa extension yang saya butuhkan tidak tersedia di `open-vsx`,
karena itu.. saya mau ganti aja ke Visual Studio Marketplace.

Caranya gimana?

Oke silahkan ikuti ini:

## Untuk Pengguna Linux

Masuk ke folder `/home/<user>/.config/VSCodium/`, lalu buat file baru di sana dengan nama
`product.json` dan isi dengan kode berikut:

```json
{
  "nameShort": "Visual Studio Code",
  "nameLong": "Visual Studio Code",
  "extensionsGallery": {
    "serviceUrl": "https://marketplace.visualstudio.com/_apis/public/gallery",
    "cacheUrl": "https://vscode.blob.core.windows.net/gallery/index",
    "itemUrl": "https://marketplace.visualstudio.com/items"
  }
}
```

![File product.json](/img/vscodium-extension-marketplace/vscodium-product-json.avif)

Setelah itu, buka ulang VS Codium dan cobalah untuk mencari extension yang dibuat oleh Microsoft.

![File product.json](/img/vscodium-extension-marketplace/vscodium-vscode-marketplace.png)

## Untuk Pengguna Mac

Buat kamu yang menggunakan MacOS, silahkan masuk ke `$HOME/Application Support/VSCodium`, lalu di sana buat
file baru dengan nama `product.json` dengan isi seperti ini: [^1]

```json
{
  "nameShort": "Visual Studio Code",
  "nameLong": "Visual Studio Code",
  "extensionsGallery": {
    "serviceUrl": "https://marketplace.visualstudio.com/_apis/public/gallery",
    "cacheUrl": "https://vscode.blob.core.windows.net/gallery/index",
    "itemUrl": "https://marketplace.visualstudio.com/items"
  }
}
```

Setelah itu, buka ulang VS Codium dan cobalah untuk mencari extension yang kamu inginkan dari
Visual Studio Marketplace.


[^1]: [Use VSCodium with Microsoft's proprietary marketplace](https://www.flypenguin.de/2023/02/26/use-vscodium-with-microsofts-proprietary-marketplace/)