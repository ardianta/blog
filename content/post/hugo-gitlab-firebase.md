---
title: "Deploy Hugo ke Firebase dengan Gitlab CI"
slug: hugo-gitlab-firebase
date: 2017-12-23T22:25:46+08:00
draft: false

tags:
    - hugo
    - gitlab
    - firebase

image: "/img/hugo/ci-gitlab.png"
description: "Cara yang saya gunakan untuk deploy Hugo ke Firebase melalui Gitlab CI"
---

Biasanya saya melakukan deploy dengan perintah `firebase deploy`.
Akan tetapi perintah ini sama persis seperti FTP.

Semua file akan di-upload ke Firebase. Hal ini akan membuat
kuota internet saya cepat habis 😄, resiko pakai paket data.

Lalu sebaiknya bagaimana?

Saya ingin mencoba _workflow_ pak Ariya. Beliau deploy
Hugo ke Firebase melalui Gitlab CI.

Gambarannya seperti ini:

![Workflow Hugo](/img/hugo/staticsite.png)

Sumber: [ariya.io](https://ariya.io/2017/05/static-site-with-hugo-and-firebase)

Lalu, pada repo Gitlab, saya menggunakan konfigurasi CI seperti ini:

```yaml
image: nohitme/hugo-firebase:0.31.1

before_script:
  - hugo version
  - firebase --version

hugo_firebase:
  stage: deploy
  only:
    - master
  except:
    - dev
  script:
    - rm -rf public
    - hugo --config config.production.toml
    - firebase deploy --token ${FIREBASE_TOKEN}
```

Saya menggunakan image docker dari [nohitme/hugo-firebase](https://hub.docker.com/r/nohitme/hugo-firebase/). Ukurannya cukup besar,
sekitar 76 MB. Karena image ini menggunakan Nodejs versi 9
dan Hugo versi terbaru (0.31.1).

Sebenarnya saya sudah coba beberapa _Image_. Tapi, tidak ada yang cocok.
Inilah image yang paling sederhana menurut saya.

`FIREBASE_TOKEN` dalam konfigurasi CI di atas adalah variabel 
_environtment_ yang kita tambahkan melalui __Settings->CI/DI->Secret Variables__.

Dengan menggunakan konfigurasi CI ini, waktu build-nya relatif lebih cepat.
Biasanya anatara 30 detik sampai 2 menit.

![Build CI Gitlab](/img/hugo/ci-gitlab.png)

Sekarang kita tinggal `git push` aja ke Gitlab untuk deploy ke Firebase.

Enak kaan!