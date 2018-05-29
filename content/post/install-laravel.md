---
title: "Masalah Saat Install Laravel"
slug: install-laravel
date: 2018-05-30T04:42:41+08:00
draft: false

type: post

tags:
    - laravel
    - coding
    - php

image: "/img/laravel/laravel.png"
description: ""
---

## Server tidak bisa dijalankan:

```bash
$ php artisan serve
PHP Warning:  require(/home/petanikode/tmp/mikroblog/vendor/autoload.php): failed to open stream: No such file or directory in /home/petanikode/tmp/mikroblog/artisan on line 18
PHP Fatal error:  require(): Failed opening required '/home/petanikode/tmp/mikroblog/vendor/autoload.php' (include_path='.:/usr/share/php') in /home/petanikode/tmp/mikroblog/artisan on line 18
```

Solusi:

Coba jalankan perintah:

```bash
composer install
```

## Versi PHP masih Versi Lama

Muncul masalah lagi, ternyata versi PHP yang saya gunakan masih versi lama:

```bash
$ composer install
Loading composer repositories with package information
Updating dependencies (including require-dev)
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - This package requires php ^7.1.3 but your PHP version (7.0.30) does not satisfy that requirement.
  Problem 2
    - laravel/framework v5.6.9 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.8 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.7 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.6 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.5 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.4 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.3 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.23 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.22 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.21 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.20 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.2 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.19 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.18 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.17 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.16 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.15 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.14 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.13 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.12 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.11 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.10 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.1 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework v5.6.0 requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - laravel/framework 5.6.x-dev requires php ^7.1.3 -> your PHP version (7.0.30) does not satisfy that requirement.
    - Installation request for laravel/framework 5.6.* -> satisfiable by laravel/framework[5.6.x-dev, v5.6.0, v5.6.1, v5.6.10, v5.6.11, v5.6.12, v5.6.13, v5.6.14, v5.6.15, v5.6.16, v5.6.17, v5.6.18, v5.6.19, v5.6.2, v5.6.20, v5.6.21, v5.6.22, v5.6.23, v5.6.3, v5.6.4, v5.6.5, v5.6.6, v5.6.7, v5.6.8, v5.6.9].
```

Solusi:

Upgrade versi PHP ke versi yang lebih baru, install melalui PPA.

```bash
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get install -y php7.2
```

Coba jalankan server lagi:

```bash
$ php artisan serve
PHP Warning:  require(/home/petanikode/tmp/mikroblog/vendor/autoload.php): failed to open stream: No such file or directory in /home/petanikode/tmp/mikroblog/artisan on line 18
PHP Fatal error:  require(): Failed opening required '/home/petanikode/tmp/mikroblog/vendor/autoload.php' (include_path='.:/usr/share/php') in /home/petanikode/tmp/mikroblog/artisan on line 18
```

Ternyat amasih error!

Coba jalankan `composer install` lagi.

```bash
$ composer install
Loading composer repositories with package information
Updating dependencies (including require-dev)
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - laravel/framework v5.6.9 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.8 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.7 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.6 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.5 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.4 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.3 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.23 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.22 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.21 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.20 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.2 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.19 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.18 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.17 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.16 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.15 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.14 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.13 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.12 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.11 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.10 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.1 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework v5.6.0 requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - laravel/framework 5.6.x-dev requires ext-mbstring * -> the requested PHP extension mbstring is missing from your system.
    - Installation request for laravel/framework 5.6.* -> satisfiable by laravel/framework[5.6.x-dev, v5.6.0, v5.6.1, v5.6.10, v5.6.11, v5.6.12, v5.6.13, v5.6.14, v5.6.15, v5.6.16, v5.6.17, v5.6.18, v5.6.19, v5.6.2, v5.6.20, v5.6.21, v5.6.22, v5.6.23, v5.6.3, v5.6.4, v5.6.5, v5.6.6, v5.6.7, v5.6.8, v5.6.9].

  To enable extensions, verify that they are enabled in your .ini files:
    - /etc/php/7.2/cli/php.ini
    - /etc/php/7.2/cli/conf.d/10-opcache.ini
    - /etc/php/7.2/cli/conf.d/10-pdo.ini
    - /etc/php/7.2/cli/conf.d/20-calendar.ini
    - /etc/php/7.2/cli/conf.d/20-ctype.ini
    - /etc/php/7.2/cli/conf.d/20-exif.ini
    - /etc/php/7.2/cli/conf.d/20-fileinfo.ini
    - /etc/php/7.2/cli/conf.d/20-ftp.ini
    - /etc/php/7.2/cli/conf.d/20-gettext.ini
    - /etc/php/7.2/cli/conf.d/20-iconv.ini
    - /etc/php/7.2/cli/conf.d/20-json.ini
    - /etc/php/7.2/cli/conf.d/20-phar.ini
    - /etc/php/7.2/cli/conf.d/20-posix.ini
    - /etc/php/7.2/cli/conf.d/20-readline.ini
    - /etc/php/7.2/cli/conf.d/20-shmop.ini
    - /etc/php/7.2/cli/conf.d/20-sockets.ini
    - /etc/php/7.2/cli/conf.d/20-sysvmsg.ini
    - /etc/php/7.2/cli/conf.d/20-sysvsem.ini
    - /etc/php/7.2/cli/conf.d/20-sysvshm.ini
    - /etc/php/7.2/cli/conf.d/20-tokenizer.ini
  You can also run `php --ini` inside terminal to see which files are used by PHP in CLI mode.
```

## Ekstensi yang dibutuhkan belum terinstall

Ok, dari pesan error tersebut, kita bisa ketahui ada bebeapa Ekstensi yang dibutuhkan oleh Laravel.
Namun, belum tersedia dan diaktifkan.

Solusi:

Install ekstensi mbstring

```bash
apt install php-mbstring
```

Jalankan lagi:

```bash
composer install
```

Masih Error:

```bash
$ composer install
Loading composer repositories with package information
Updating dependencies (including require-dev)
Your requirements could not be resolved to an installable set of packages.

  Problem 1
    - phpunit/phpunit 7.2.x-dev requires ext-dom * -> the requested PHP extension dom is missing from your system.
    - phpunit/phpunit 7.1.x-dev requires ext-dom * -> the requested PHP extension dom is missing from your system.
    - phpunit/phpunit 7.1.5 requires ext-dom * -> the requested PHP extension dom is missing from your system.
    - phpunit/phpunit 7.1.4 requires ext-dom * -> the requested PHP extension dom is missing from your system.
    - phpunit/phpunit 7.1.3 requires ext-dom * -> the requested PHP extension dom is missing from your system.
    - phpunit/phpunit 7.1.2 requires ext-dom * -> the requested PHP extension dom is missing from your system.
    - phpunit/phpunit 7.1.1 requires ext-dom * -> the requested PHP extension dom is missing from your system.
    - phpunit/phpunit 7.1.0 requires ext-dom * -> the requested PHP extension dom is missing from your system.
    - phpunit/phpunit 7.0.x-dev requires ext-dom * -> the requested PHP extension dom is missing from your system.
    - phpunit/phpunit 7.0.3 requires ext-dom * -> the requested PHP extension dom is missing from your system.
    - phpunit/phpunit 7.0.2 requires ext-dom * -> the requested PHP extension dom is missing from your system.
    - phpunit/phpunit 7.0.1 requires ext-dom * -> the requested PHP extension dom is missing from your system.
    - phpunit/phpunit 7.0.0 requires ext-dom * -> the requested PHP extension dom is missing from your system.
    - Installation request for phpunit/phpunit ^7.0 -> satisfiable by phpunit/phpunit[7.0.0, 7.0.1, 7.0.2, 7.0.3, 7.0.x-dev, 7.1.0, 7.1.1, 7.1.2, 7.1.3, 7.1.4, 7.1.5, 7.1.x-dev, 7.2.x-dev].

  To enable extensions, verify that they are enabled in your .ini files:
    - /etc/php/7.2/cli/php.ini
    - /etc/php/7.2/cli/conf.d/10-opcache.ini
    - /etc/php/7.2/cli/conf.d/10-pdo.ini
    - /etc/php/7.2/cli/conf.d/20-calendar.ini
    - /etc/php/7.2/cli/conf.d/20-ctype.ini
    - /etc/php/7.2/cli/conf.d/20-exif.ini
    - /etc/php/7.2/cli/conf.d/20-fileinfo.ini
    - /etc/php/7.2/cli/conf.d/20-ftp.ini
    - /etc/php/7.2/cli/conf.d/20-gettext.ini
    - /etc/php/7.2/cli/conf.d/20-iconv.ini
    - /etc/php/7.2/cli/conf.d/20-json.ini
    - /etc/php/7.2/cli/conf.d/20-mbstring.ini
    - /etc/php/7.2/cli/conf.d/20-phar.ini
    - /etc/php/7.2/cli/conf.d/20-posix.ini
    - /etc/php/7.2/cli/conf.d/20-readline.ini
    - /etc/php/7.2/cli/conf.d/20-shmop.ini
    - /etc/php/7.2/cli/conf.d/20-sockets.ini
    - /etc/php/7.2/cli/conf.d/20-sysvmsg.ini
    - /etc/php/7.2/cli/conf.d/20-sysvsem.ini
    - /etc/php/7.2/cli/conf.d/20-sysvshm.ini
    - /etc/php/7.2/cli/conf.d/20-tokenizer.ini
  You can also run `php --ini` inside terminal to see which files are used by PHP in CLI mode.
```

Kali ini errornya karena belum ada `ext-dom`.

Solusinya:

Install `ext-dom`:

```bash
apt intall php-xml
```

Coba lagi:

```bash
php artisan serve

# jika masih error coba
composer install
```

Jika masih error, coba install semua ekstensi yang dibutuhkan laravel 5.6:

- PHP >= 7.1.3
- OpenSSL PHP Extension
- PDO PHP Extension
- Mbstring PHP Extension
- Tokenizer PHP Extension
- XML PHP Extension
- Ctype PHP Extension
- JSON PHP Extension

```bash
sudo apt-get install php-common php-mbstring php-xml php-zip php-json php-mcrypt
```

Done!

Laravel bisa dijalankan...

![Laravel](/img/laravel/laravel.png)