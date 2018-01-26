---
title: "Git Push, Lalu Tiba-tiba Matilampu!"
slug: git-push-matilampu
date: 2017-12-20T00:59:23+08:00
draft: false

tags:
    - Git

image: "img/git-matilampu/repo-rusak.png"
description: "Apa yang akan terjadi saat menjalankan perintah git push lalu
ditengah-tengah mati lampu?"
---

Apa yang akan terjadi saat menjalankan perintah `git push` lalu
ditengah-tengah mati lampu?

Jika pakai laptop nggak masalah, karena daya masih bisa
ngambil dari baterai.

Tapi yang pakai komputer?

atau yang laptopnya nggak bisa nyala tanpa cas?

Ini masalah!

Sebenarnya kejadian ini sudah pernah saya alami sebelumnya.

Repositori jadi rusak dan tidak bisa melakukan apa-apa.

![Repositori Git Rusak](/img/git-matilampu/repo-rusak.png)

Solusi "bodohnya" kita harus membuat repositori baru.

Hapus dulu database git yang sudah ada:

```bash
rm -rf .git
rm .gitignore
```

Lalu bikin lagi yang baru:

```bash
git init .
git add .
git commit -m "first commit"
```

Lalu untuk push ke github, kita pakai `--force`. Sebenarnya ini bahaya, karena
dapat menghapus semua log yang ada di repo github.

```bash
git push origin master --force
```

Maka semua revisi yang ada di Github akan ditindih dengan yang baru.

Lalu, karena repositori ini saya pakai untuk Hugo, maka
harus buat sub-modul lagi untuk deploy ke Github.

Tutorialnya ada di sini: [Cara Hosting Hugo di Github](https://www.petanikode.com/hugo-hosting-github/)

Setelah itu, coba tes deploy lagi.

Pasti bisa!

Berikut ini log perintah yang saya ketik di terminal:

```bash
petanikode@imajinasi ~/ardianta-pargo $ rm -rf .git
petanikode@imajinasi ~/ardianta-pargo $ git status 
fatal: Not a git repository (or any parent up to mount point /home)
Stopping at filesystem boundary (GIT_DISCOVERY_ACROSS_FILESYSTEM not set).
petanikode@imajinasi ~/ardianta-pargo $ git init .
Initialized empty Git repository in /home/petanikode/ardianta-pargo/.git/
petanikode@imajinasi ~/ardianta-pargo $ rm -R public/
petanikode@imajinasi ~/ardianta-pargo $ git add .
petanikode@imajinasi ~/ardianta-pargo $ git commit -m "first commit"
[master (root-commit) e5cb7d3] first commit
 54 files changed, 14823 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 .gitmodules
 create mode 100644 archetypes/default.md
 create mode 100644 config.toml
 create mode 100644 content/about.md
 create mode 100644 content/post/_ilmu-2017.md
 create mode 100644 content/post/_migrasi-ke-hugo-firebase.md
 create mode 100644 content/post/ekstensi-hugofy.md
 create mode 100644 content/post/hello-world.md
 create mode 100644 content/post/hp-cooling-fan.md
 create mode 100644 content/post/lombokdev-meetup-3.md
 create mode 100644 content/post/tema-baru-hugo.md
 create mode 100644 content/project.md
 create mode 100755 deploy.sh
 create mode 100644 static/README.md
 create mode 100644 static/img/ardianta-logo.svg
 create mode 100644 static/img/hugofy/error-server.png
 create mode 100644 static/img/hugofy/install-hugofy.png
 create mode 100644 static/img/hugofy/perintah-hugofy.png
 create mode 100644 static/img/tema-baru/index.png
 create mode 100644 static/img/tema-baru/single.png
 create mode 100644 themes/ardianta/LICENSE.md
 create mode 100644 themes/ardianta/archetypes/default.md
 create mode 100644 themes/ardianta/layouts/404.html
 create mode 100644 themes/ardianta/layouts/_default/list.html
 create mode 100644 themes/ardianta/layouts/_default/single.html
 create mode 100644 themes/ardianta/layouts/index.html
 create mode 100644 themes/ardianta/layouts/partials/disqus.html
 create mode 100644 themes/ardianta/layouts/partials/footer.html
 create mode 100644 themes/ardianta/layouts/partials/head.html
 create mode 100644 themes/ardianta/layouts/partials/header.html
 create mode 100644 themes/ardianta/static/css/bootstrap-grid.css
 create mode 100644 themes/ardianta/static/css/bootstrap-grid.css.map
 create mode 100644 themes/ardianta/static/css/bootstrap-grid.min.css
 create mode 100644 themes/ardianta/static/css/bootstrap-grid.min.css.map
 create mode 100644 themes/ardianta/static/css/bootstrap-reboot.css
 create mode 100644 themes/ardianta/static/css/bootstrap-reboot.css.map
 create mode 100644 themes/ardianta/static/css/bootstrap-reboot.min.css
 create mode 100644 themes/ardianta/static/css/bootstrap-reboot.min.css.map
 create mode 100644 themes/ardianta/static/css/bootstrap.css
 create mode 100644 themes/ardianta/static/css/bootstrap.css.map
 create mode 100644 themes/ardianta/static/css/bootstrap.min.css
 create mode 100644 themes/ardianta/static/css/bootstrap.min.css.map
 create mode 100644 themes/ardianta/static/css/prism.css
 create mode 100644 themes/ardianta/static/css/style.css
 create mode 100644 themes/ardianta/static/img/ardianta.jpg
 create mode 100644 themes/ardianta/static/js/bootstrap.js
 create mode 100644 themes/ardianta/static/js/bootstrap.min.js
 create mode 100644 themes/ardianta/static/js/jquery-3.2.1.slim.min.js
 create mode 100644 themes/ardianta/static/js/lazysizes.min.js
 create mode 100644 themes/ardianta/static/js/popper.min.js
 create mode 100644 themes/ardianta/static/js/prism.js
 create mode 100644 themes/ardianta/static/js/twemoji.min.js
 create mode 100644 themes/ardianta/theme.toml
petanikode@imajinasi ~/ardianta-pargo $ git status 
On branch master
nothing to commit, working directory clean
petanikode@imajinasi ~/ardianta-pargo $ git remote add origin git@github.com:ardianta/blog.git
petanikode@imajinasi ~/ardianta-pargo $ git remote -v
origin	git@github.com:ardianta/blog.git (fetch)
origin	git@github.com:ardianta/blog.git (push)
petanikode@imajinasi ~/ardianta-pargo $ git push origin master --force
Counting objects: 72, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (65/65), done.
Writing objects: 100% (72/72), 450.71 KiB | 0 bytes/s, done.
Total 72 (delta 7), reused 0 (delta 0)
remote: Resolving deltas: 100% (7/7), done.
To git@github.com:ardianta/blog.git
 + eaff54b...e5cb7d3 master -> master (forced update)
petanikode@imajinasi ~/ardianta-pargo $ git submodule add -b master git@github.com:ardianta/ardianta.github.io.git public
Cloning into 'public'...
remote: Counting objects: 634, done.
remote: Compressing objects: 100% (111/111), done.
remote: Total 634 (delta 113), reused 168 (delta 64), pack-reused 415
Receiving objects: 100% (634/634), 1.20 MiB | 465.00 KiB/s, done.
Resolving deltas: 100% (303/303), done.
Checking connectivity... done.
petanikode@imajinasi ~/ardianta-pargo $ hugo
Started building sites ...
ERROR 2017/12/20 00:55:27 Page's Now is deprecated and will be removed in Hugo 0.27. Use now (the template func).
Built site for language en:
0 of 2 drafts rendered
0 future content
0 expired content
7 regular pages created
8 other pages created
0 non-page files copied
0 paginator pages created
0 tags created
0 categories created
total in 11 ms
petanikode@imajinasi ~/ardianta-pargo $ cd public/
petanikode@imajinasi ~/ardianta-pargo/public $ git add .
petanikode@imajinasi ~/ardianta-pargo/public $ git commit -m "deploy setelah kerusakan"
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
petanikode@imajinasi ~/ardianta-pargo/public $ git push origin master 
Everything up-to-date
petanikode@imajinasi ~/ardianta-pargo/public $ cd ..
petanikode@imajinasi ~/ardianta-pargo $ ./deploy.sh 
Deploying updates to GitHub...
Started building sites ...
ERROR 2017/12/20 00:56:11 Page's Now is deprecated and will be removed in Hugo 0.27. Use now (the template func).
Built site for language en:
0 of 2 drafts rendered
0 future content
0 expired content
7 regular pages created
8 other pages created
0 non-page files copied
0 paginator pages created
0 categories created
0 tags created
total in 13 ms
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
Everything up-to-date
petanikode@imajinasi ~/ardianta-pargo $ ./deploy.sh 
Deploying updates to GitHub...
Started building sites ...
ERROR 2017/12/20 00:56:42 Page's Now is deprecated and will be removed in Hugo 0.27. Use now (the template func).
Built site for language en:
0 of 2 drafts rendered
0 future content
0 expired content
7 regular pages created
8 other pages created
0 non-page files copied
0 paginator pages created
0 tags created
0 categories created
total in 13 ms
[master 241711f] rebuilding http://ardianta.github.io Wed Dec 20 00:56:42 WITA 2017
 1 file changed, 2 insertions(+)
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (5/5), 468 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
To git@github.com:ardianta/ardianta.github.io.git
   99a9edb..241711f  master -> master
petanikode@imajinasi ~/ardianta-pargo $
```

Untungnya repositori ini bukan project besar. Jadi tak masalah Git-nya mengulang dari awal.

Sebenarnya ada cara lain, yaitu dengan clone ulang yang sudah ada.

Akan tentapi, ada banyak perubahan yang sudah dilakukan.

Capek juga ulang lagi... 😄