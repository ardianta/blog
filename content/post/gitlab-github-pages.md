---
title: "Experimen Deploy Hugo dari Gitlab CI ke Github Pages"
slug: gitlab-github-pages
date: 2018-01-01T09:39:08+08:00
draft: false

type: post

tags:
    - Hugo
    - Github
    - Gitlab
    - CI

image: "/img/gitlab-github/token-github.png"
description: "Bagaimana cara deploy Hugo dari Gitlab ke Github Pages?"
---

Di awal tahun baru, sepertinya pegawai [Travis CI](/blog/hugo-travis-ci/) sedang liburan.
Hal ini munkin menyebabkan gangguan build di Travis CI. 
Akibanya lama menunggu Queue build-nya.

Sebagai alternatif, saya menggunakan CI milik Gitlab.

Ini adalah isi file `.gitlab-ci.yml` di [repo blog saya](https://github.com/ardianta/blog):

```yaml
image: andthensome/alpine-hugo-git-bash:0.31.2

before_script:
  - hugo version

github_pages:
  script:
  - rm -rf public
  - git clone --depth 1 https://ardianta:$GITHUB_ACCESS_TOKEN@github.com/ardianta/ardianta.github.io.git public
  - hugo --config config.production.toml
  - cd public
  - git config user.email "<your git email>"
  - git config --global user.name "<your git name>"
  - git add -A
  - git commit -m "Build from $CI_SERVER_NAME $CI_PIPELINE_ID"
  - git push
  artifacts:
    paths:
    - public
  only:
  - master
```

Saya menggunakan image docker [andthensome/alpine-hugo-git-bash](https://hub.docker.com/r/andthensome/alpine-hugo-git-bash/tags/),
karena membutuhkan perintah `hugo` dan `git` saat melakukan build.
Selain itu, image ini ukurannya relatif kecil yaitu 44MB.

Perintah `hugo` untuk me-render dari source code, lalu `git` untuk melakukan clone 
dan push ke github pages.

Variabel env untuk `$GITHUB_ACCESS_TOKEN` bisa kita isi di __Settings->CI/DI->Secret Variables__.

![Secret Variabel Github](/img/gitlab-github/token-github.png)

Nilai dari variabel ini adalah personal token dari Github, yang sudah dibuat di
[Settings->Tokens](https://github.com/settings/tokens).

Percobaan build...

![Build CI Gitlab](/img/gitlab-github/build-ci-gitlab.png)

Sukses 🌮

Ini hasilnya di repo Github Pages:

![Github Pages Blog Ardianta](/img/gitlab-github/github-pages.png)

Berikutnya saya ingin agar repo di Github sinkron dengan Gitlab.
Tapi saat masih belum tahu caranya.

Ya sudah, biarkan saja begini 😄.