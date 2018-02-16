---
title: "Isengin Web Python dan dapat akses Shell Linux Gratis!"
slug: shell-web-python
date: 2018-02-16T07:15:15+08:00
draft: false

type: post

tags:
    - Python
    - Linux

image: "/img/python/web-python-interaktif.png"
description: "Di website Python, terdapat shell python yang bisa kita gunakan untuk ujicaoba kode python. Lalu, bagaimana kalau kita akses shell seperti bash dan zsh dari sana?"
---

Karena habis gentayangan di beberapa cloud workspace 
seperti c9.io, codenvy, dan glitch saya tiba-tiba
kepikiran untuk mengakses shell dari web Python.

Di website Python, terdapat shell python yang
bisa kita gunakan untuk ujicaoba kode python.

Lalu, bagaimana kalau...

Kita akses shell seperti `bash` atau `zsh` di sana?

Ya, itu bisa.

Caranya:

Pertama saya coba-coba dulu menjalankan
perintah Linux dengan mengimpor modul `os`.

Di dalam modul `os`, terdapat fungsi untuk menjalankan
perintah Linux, yaitu: `system()`.

```python
import os

os.system('ls')
os.system('pwd')
os.system('ls -la /')
```

Outputnya kira-kira begini:

![Python interaktif di website python](/img/python/web-python-interaktif.png)

Melihat output dari perintah-peritah itu,
saya jadi semakin penasaran...

Bagaimana kalau kita buka `bash` atau `zsh`?

Ya, tinggal eksekusi saja perintah buat buka 
`bash` dan `zsh`.

```python
from os import system

system('bash')
```

dan...

Boom!

Kita dapat akses shell Linux.

Sekarang kita mau ngapain?

Oke, mari kita coba cek ada apa saja di sini.

![GCC dan Ruby di website Python](/img/python/c-ruby.png)

Woh! ada `gcc`, `g++`, dan juga `ruby`.

Kalau `git` ada tidak?

![Git di webstite Python](/img/python/git.png)

Tentu saja ada.

Oya, shell ini terhubung dengan internet.
Coba saja kita clone repository dari Github
atau coba download sesuatu dengan `wget` dan `curl`.

![Wget dari shell di Web Python](/img/python/wget.png)