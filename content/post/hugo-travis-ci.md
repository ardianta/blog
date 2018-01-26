---
title: "Sekarang Blog ini Menggunakan Travis CI"
slug: hugo-travis-ci
date: 2017-12-24T06:05:11+08:00
draft: false

tags:
    - Hugo
    - Blog
    - Travis
    - CI

image: "/img/travis/travis-ci.png"
description: "Workflow ngeblog saya berubah. Sekarang sudah dibantu Travis CI untuk build dan deploy"
---

Blog ini di-hosting di Github pada repositori ini: https://github.com/ardianta/ardianta.github.io.

Setiap kali saya ingin _deploy_, saya harus melakukan _push_
ke sana.

Tapi sekarang sudah tidak lagi, karena sudah
dibantu sama Travis CI. yay! 😄

Travis CI ini bertugas untuk melakuakn build dan 
deploy.

Adapun skrip yang saya gunakan adalah sebagai berikut:

File `deploy-ci.sh`

```bash
#!/bin/bash

set -e

DEPLOY_REPO="https://${DEPLOY_BLOG_TOKEN}@github.com/ardianta/ardianta.github.io.git"

function main {
    clean
    get_current_site
    build_site
    deploy
}

function clean { 
	echo "cleaning public folder"
	if [ -d "public" ]; then rm -rf public; fi 
}

function get_current_site { 
	echo "getting latest site"
	git clone --depth 1 $DEPLOY_REPO public 
}

function build_site { 
	echo "building site..."
	hugo --config config.production.toml
}

function deploy {
	echo "deploying changes"

	if [ -z "$TRAVIS_PULL_REQUEST" ]; then
	    echo "except don't publish site for pull requests"
	    exit 0
	fi  

	if [ "$TRAVIS_BRANCH" != "master" ]; then
	    echo "except we should only publish the master branch. stopping here"
	    exit 0
	fi

	cd public
	git config --global user.name "Travis CI"
    git config --global user.email ardianta_pargo@yahoo.co.id
	git add -A
	git status
	git commit -m "Travis build $TRAVIS_BUILD_NUMBER auto-pushed to github"
	git push $DEPLOY_REPO master:master
}


main
```

Kita membutuhkan token personal Github untuk mengisi `DEPLOY_BLOG_TOKEN`
agar skrip di atas bisa melakukan _push_ ke repositori.

Token ini bisa kita dapatkan di __Akun->Settings->Developer settings->Personal access tokens__
(https://github.com/settings/tokens).

Token yang sudah dibuat, bisa ditambahkan di pengaturan Travis (https://travis-ci.org/).

Sementara untuk konfigurasi CI Travis-nya:

File: `.travis.yml`

```yaml
language: generic
os: linux

sudo: required
dist: trusty
group: deprecated-2017Q4


install:
  - wget -O /tmp/hugo.deb https://github.com/gohugoio/hugo/releases/download/v0.31.1/hugo_0.31.1_Linux-64bit.deb
  - sudo dpkg -i /tmp/hugo.deb
  - rm -rf public || exit 0

script:
  - hugo version
  - chmod +x deploy-ci.sh
  - ./deploy-ci.sh
```

Dengan begini saya tinggal melakukan push saja ke repositori ini:
https://github.com/ardianta/blog lalu Travis CI akan melakukan build
dan melakukan push [ke sini](https://github.com/ardianta/ardianta.github.io).

Ini screenshot saat si Travis CI melakukan Build.

![Travis CI Build Hugo to Github](/img/travis/travis-ci.png)

Kadang kalau tidak ada yang di-push, build akan gagal. Tapi itu tidak masalah,
karena belum ada update terbaru yang harus di-push.

![History Build Travis](/img/travis/build.png)

Sekarang bisa sedikit hemat kuota, karena tidak nge-push ke dua 
repositori sekaligus. 😄

Terima kasih Travis CI.