---
title: "Clone Commit Terakhir dari Repository Git"
slug: git-clone-depth
date: 2017-12-26T04:13:15+08:00
draft: false

tags:
    - Git

image: "/img/git/clone/clone-repo-petanikode.png"
description: "Cara Clone Commit Terakhir dari Rpositori"
---

Banyangkan ada `12283192311` commit yang sudah dilakukan pada repository.
Lalu kita ingin clone ke lokal.

Berapa besar file yang akan di-download?

Pastinya cukup besar.

Nah, bagaimana caranya clone hanya commit terakhir saja?

Cukup dengan perintah ini:

```bash
git clone --depth=1 <remote_repo_url>
```

Referensi:

- https://git-scm.com/docs/git-clone
- https://stackoverflow.com/a/1210012/2658551


Contoh:

Ada `1221` commit yang sudah dibuat pada repository ini:

![Repository PetaniKode](/img/git/clone/repo-petanikode.png)

Lalu tinggal di-clone aja dengan perintah tadi.

![Clone Repository PetaniKode](/img/git/clone/clone-repo-petanikode.png)
