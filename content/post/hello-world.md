---
title: "Hello World! Tulisan Pertama di Blog Hugo"
slug: hello-world
date: 2017-01-24T14:35:02+08:00
draft: false

type: post

tags:
    - Blog
    - Hugo

image: "/img/2018/goal-2018.png"
description: "Tulisan pertama saya di blog baru"
---

Hello World!

ini adalah tulisan pertama di blog ini. Baru saja saya membuat blog
dengan Hugo. Sekarang lagi dikembangkan dengan tema [Hugo Bootstrap v4 Blog](https://github.com/alanorth/hugo-theme-bootstrap4-blog).

Saya memilih Hugo, karena rasanya lebih mudah dari pada Jekyll dan Octopress.
Meskipun saya belum mengerti bahasa pemrograman Go.

Deploy saya lakukan ke _Github Pages_ dengan dua repositori terpisah. Pertama,
repositori [ardianta-pargo](https://github.com/ardianta/ardianta-pargo) untuk
menyimpan konten, kemudian repositori [ardianta.github.io](https://github.com/ardianta/ardianta.github.io)
untuk menyimpan halaman publik hasil _render_ dari Hugo.

Saya menggunakan skrip dari [dokumentasi Hugo](https://gohugo.io/tutorials/github-pages-blog/) untuk melakukan deploy.
Karena saya tidak menggunakan _Continous Integration_ (CI). Jadi setiap
mau deploy harus eksekusi skrip tersebut. Berikut ini skripnya.

```bash
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
hugo # if using a theme, replace by `hugo -t <yourtheme>`

# Go To Public folder
cd public
# Add changes to git.
git add -A

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back
cd ..

```

Sepertinya template atau tema yang saya gunakan ini terlihat masih berantakan.
Mungkin nanti, saya akan perbaiki.
