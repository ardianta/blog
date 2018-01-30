---
title: "Masalah Saat Upgrade Linux Mint 18"
slug: upgrade-lm-18
date: 2018-01-31T04:18:56+08:00
draft: false

type: post

tags:
    - Linux

image: "/img/upgrade/error-shutter.png"
description: "Hari ini saya pergi ke tempat Wifi.id dan melakukan upgrade Linux Mint. Akan tetapi dapat sedikit masalah dengan `mysql-server"
---

Kemarin saya pergi ke tempat Wifi.id dan melakukan upgrade Linux Mint.
Akan tetapi dapat sedikit masalah dengan `mysql-server`.

Entah mengapa ini bisa terjadi...

Sebenarnya ini yang membuat saya malas upgrade Linux. 
Kadang sering terjadi error karena ada beberapa bugs yang 
belum diperbaiki.

Namun, untungnya sudah *solved* dengan solusi dari https://askubuntu.com/a/762432/235594.

Berikut ini log Terminal saya:

```bash
petanikode@imajinasi ~ $ apt install shutter 
[sudo] password for petanikode: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
shutter is already the newest version (0.93.1-1ubuntu1).
0 upgraded, 0 newly installed, 0 to remove and 21 not upgraded.
2 not fully installed or removed.
After this operation, 0 B of additional disk space will be used.
Do you want to continue? [Y/n] y
Setting up mysql-server-5.7 (5.7.21-0ubuntu0.16.04.1) ...
insserv: warning: current start runlevel(s) (empty) of script `mysql' overrides LSB defaults (2 3 4 5).
insserv: warning: current stop runlevel(s) (0 1 2 3 4 5 6) of script `mysql' overrides LSB defaults (0 1 6).
mysql_upgrade: Got error: 2002: Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2) while connecting to the MySQL server
Upgrade process encountered error and will not continue.
mysql_upgrade failed with exit status 11
dpkg: error processing package mysql-server-5.7 (--configure):
 subprocess installed post-installation script returned error exit status 1
dpkg: dependency problems prevent configuration of mysql-server:
 mysql-server depends on mysql-server-5.7; however:
  Package mysql-server-5.7 is not configured yet.

dpkg: error processing package mysql-server (--configure):
 dependency problems - leaving unconfigured
Errors were encountered while processing:
 mysql-server-5.7
 mysql-server
E: Sub-process /usr/bin/dpkg returned an error code (1)
petanikode@imajinasi ~ $ apt remove mysql
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package mysql
petanikode@imajinasi ~ $ apt remove mysql-server
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages will be REMOVED:
  mysql-server
0 upgraded, 0 newly installed, 1 to remove and 21 not upgraded.
2 not fully installed or removed.
After this operation, 166 kB disk space will be freed.
Do you want to continue? [Y/n] n
Abort.
petanikode@imajinasi ~ $ apt install mysql-server --resintall
E: Command line option --resintall is not understood in combination with the other options
petanikode@imajinasi ~ $ apt install mysql-server
mysql-server           mysql-server-5.7       mysql-server-core-5.7
petanikode@imajinasi ~ $ apt install mysql-server
mysql-server           mysql-server-5.7       mysql-server-core-5.7
petanikode@imajinasi ~ $ apt install mysql-server
Reading package lists... Done
Building dependency tree       
Reading state information... Done
mysql-server is already the newest version (5.7.21-0ubuntu0.16.04.1).
0 upgraded, 0 newly installed, 0 to remove and 21 not upgraded.
2 not fully installed or removed.
After this operation, 0 B of additional disk space will be used.
Do you want to continue? [Y/n] y
Setting up mysql-server-5.7 (5.7.21-0ubuntu0.16.04.1) ...
insserv: warning: current start runlevel(s) (empty) of script `mysql' overrides LSB defaults (2 3 4 5).
insserv: warning: current stop runlevel(s) (0 1 2 3 4 5 6) of script `mysql' overrides LSB defaults (0 1 6).
mysql_upgrade: Got error: 2002: Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2) while connecting to the MySQL server
Upgrade process encountered error and will not continue.
mysql_upgrade failed with exit status 11
dpkg: error processing package mysql-server-5.7 (--configure):
 subprocess installed post-installation script returned error exit status 1
dpkg: dependency problems prevent configuration of mysql-server:
 mysql-server depends on mysql-server-5.7; however:
  Package mysql-server-5.7 is not configured yet.

dpkg: error processing package mysql-server (--configure):
 dependency problems - leaving unconfigured
Errors were encountered while processing:
 mysql-server-5.7
 mysql-server
E: Sub-process /usr/bin/dpkg returned an error code (1)
petanikode@imajinasi ~ $ sudo service mysql start 
petanikode@imajinasi ~ $ apt install mysql-server
Reading package lists... Done
Building dependency tree       
Reading state information... Done
mysql-server is already the newest version (5.7.21-0ubuntu0.16.04.1).
0 upgraded, 0 newly installed, 0 to remove and 21 not upgraded.
2 not fully installed or removed.
After this operation, 0 B of additional disk space will be used.
Do you want to continue? [Y/n] y
Setting up mysql-server-5.7 (5.7.21-0ubuntu0.16.04.1) ...
insserv: warning: current start runlevel(s) (empty) of script `mysql' overrides LSB defaults (2 3 4 5).
insserv: warning: current stop runlevel(s) (0 1 2 3 4 5 6) of script `mysql' overrides LSB defaults (0 1 6).
mysql_upgrade: Got error: 2002: Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2) while connecting to the MySQL server
Upgrade process encountered error and will not continue.
mysql_upgrade failed with exit status 11
dpkg: error processing package mysql-server-5.7 (--configure):
 subprocess installed post-installation script returned error exit status 1
dpkg: dependency problems prevent configuration of mysql-server:
 mysql-server depends on mysql-server-5.7; however:
  Package mysql-server-5.7 is not configured yet.

dpkg: error processing package mysql-server (--configure):
 dependency problems - leaving unconfigured
Errors were encountered while processing:
 mysql-server-5.7
 mysql-server
E: Sub-process /usr/bin/dpkg returned an error code (1)
petanikode@imajinasi ~ $ sudo apt dist-upgrade 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
Calculating upgrade... Done
The following packages were automatically installed and are no longer required:
  libllvm4.0 libllvm4.0:i386
Use 'sudo apt autoremove' to remove them.
The following NEW packages will be installed:
  libllvm5.0 libllvm5.0:i386
The following packages will be upgraded:
  hhvm libegl1-mesa libegl1-mesa:i386 libgbm1 libgbm1:i386 libgl1-mesa-dev
  libgl1-mesa-dri:i386 libgl1-mesa-dri libgl1-mesa-glx libgl1-mesa-glx:i386
  libglapi-mesa:i386 libglapi-mesa libgles2-mesa libwayland-egl1-mesa
  libwayland-egl1-mesa:i386 libxatracker2 linux-firmware mesa-common-dev
  ndiswrapper ndiswrapper-dkms ndiswrapper-utils-1.9
21 upgraded, 2 newly installed, 0 to remove and 0 not upgraded.
2 not fully installed or removed.
Need to get 106 MB of archives.
After this operation, 155 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu xenial-updates/main i386 libllvm5.0 i386 1:5.0-3~16.04.1 [15,0 MB]
Get:2 https://dl.hhvm.com/ubuntu xenial/main amd64 hhvm amd64 3.24.1-1~xenial [17,5 MB]
Get:3 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libllvm5.0 amd64 1:5.0-3~16.04.1 [13,5 MB]
Get:4 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libgl1-mesa-dev amd64 17.2.4-0ubuntu1~16.04.4 [4.452 B]
Get:5 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 mesa-common-dev amd64 17.2.4-0ubuntu1~16.04.4 [520 kB]
Get:6 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libgl1-mesa-glx amd64 17.2.4-0ubuntu1~16.04.4 [130 kB]
Get:7 http://archive.ubuntu.com/ubuntu xenial-updates/main i386 libgl1-mesa-glx i386 17.2.4-0ubuntu1~16.04.4 [138 kB]
Get:8 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libgles2-mesa amd64 17.2.4-0ubuntu1~16.04.4 [13,4 kB]
Get:9 http://archive.ubuntu.com/ubuntu xenial-updates/main i386 libglapi-mesa i386 17.2.4-0ubuntu1~16.04.4 [23,0 kB]
Get:10 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libglapi-mesa amd64 17.2.4-0ubuntu1~16.04.4 [22,4 kB]
Get:11 http://archive.ubuntu.com/ubuntu xenial-updates/main i386 libgbm1 i386 17.2.4-0ubuntu1~16.04.4 [26,4 kB]
Get:12 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libgbm1 amd64 17.2.4-0ubuntu1~16.04.4 [24,6 kB]
Get:13 http://archive.ubuntu.com/ubuntu xenial-updates/main i386 libgl1-mesa-dri i386 17.2.4-0ubuntu1~16.04.4 [6.256 kB]
Get:14 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libgl1-mesa-dri amd64 17.2.4-0ubuntu1~16.04.4 [5.782 kB]
Get:15 http://archive.ubuntu.com/ubuntu xenial-updates/main i386 libegl1-mesa i386 17.2.4-0ubuntu1~16.04.4 [92,2 kB]
Get:16 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libegl1-mesa amd64 17.2.4-0ubuntu1~16.04.4 [84,5 kB]
Get:17 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libwayland-egl1-mesa amd64 17.2.4-0ubuntu1~16.04.4 [5.874 B]
Get:18 http://archive.ubuntu.com/ubuntu xenial-updates/main i386 libwayland-egl1-mesa i386 17.2.4-0ubuntu1~16.04.4 [5.964 B]
Get:19 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 libxatracker2 amd64 17.2.4-0ubuntu1~16.04.4 [1.103 kB]
Get:20 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 linux-firmware all 1.157.15 [45,5 MB]
Get:21 http://archive.ubuntu.com/ubuntu xenial-updates/universe amd64 ndiswrapper amd64 1.60-3~ubuntu16.04.2 [20,4 kB]
Get:22 http://archive.ubuntu.com/ubuntu xenial-updates/universe amd64 ndiswrapper-dkms all 1.60-3~ubuntu16.04.2 [140 kB]
Get:23 http://archive.ubuntu.com/ubuntu xenial-updates/universe amd64 ndiswrapper-utils-1.9 all 1.60-3~ubuntu16.04.2 [1.740 B]
Fetched 106 MB in 1min 14s (1.422 kB/s)                                        
Selecting previously unselected package libllvm5.0:i386.
(Reading database ... 551823 files and directories currently installed.)
Preparing to unpack .../libllvm5.0_1%3a5.0-3~16.04.1_i386.deb ...
Unpacking libllvm5.0:i386 (1:5.0-3~16.04.1) ...
Selecting previously unselected package libllvm5.0:amd64.
Preparing to unpack .../libllvm5.0_1%3a5.0-3~16.04.1_amd64.deb ...
Unpacking libllvm5.0:amd64 (1:5.0-3~16.04.1) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...
Setting up libllvm5.0:amd64 (1:5.0-3~16.04.1) ...
Setting up libllvm5.0:i386 (1:5.0-3~16.04.1) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...
(Reading database ... 551832 files and directories currently installed.)
Preparing to unpack .../libgl1-mesa-dev_17.2.4-0ubuntu1~16.04.4_amd64.deb ...
Unpacking libgl1-mesa-dev:amd64 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../mesa-common-dev_17.2.4-0ubuntu1~16.04.4_amd64.deb ...
Unpacking mesa-common-dev:amd64 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../libgl1-mesa-glx_17.2.4-0ubuntu1~16.04.4_i386.deb ...
De-configuring libgl1-mesa-glx:amd64 (17.0.7-0ubuntu0.16.04.2) ...
Unpacking libgl1-mesa-glx:i386 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../libgl1-mesa-glx_17.2.4-0ubuntu1~16.04.4_amd64.deb ...
Unpacking libgl1-mesa-glx:amd64 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../libgles2-mesa_17.2.4-0ubuntu1~16.04.4_amd64.deb ...
Unpacking libgles2-mesa:amd64 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../libglapi-mesa_17.2.4-0ubuntu1~16.04.4_amd64.deb ...
De-configuring libglapi-mesa:i386 (17.0.7-0ubuntu0.16.04.2) ...
Unpacking libglapi-mesa:amd64 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../libglapi-mesa_17.2.4-0ubuntu1~16.04.4_i386.deb ...
Unpacking libglapi-mesa:i386 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../libgbm1_17.2.4-0ubuntu1~16.04.4_amd64.deb ...
De-configuring libgbm1:i386 (17.0.7-0ubuntu0.16.04.2) ...
Unpacking libgbm1:amd64 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../libgbm1_17.2.4-0ubuntu1~16.04.4_i386.deb ...
Unpacking libgbm1:i386 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../libgl1-mesa-dri_17.2.4-0ubuntu1~16.04.4_amd64.deb ...
De-configuring libgl1-mesa-dri:i386 (17.0.7-0ubuntu0.16.04.2) ...
Unpacking libgl1-mesa-dri:amd64 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../libgl1-mesa-dri_17.2.4-0ubuntu1~16.04.4_i386.deb ...
Unpacking libgl1-mesa-dri:i386 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../libegl1-mesa_17.2.4-0ubuntu1~16.04.4_amd64.deb ...
De-configuring libegl1-mesa:i386 (17.0.7-0ubuntu0.16.04.2) ...
Unpacking libegl1-mesa:amd64 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../libegl1-mesa_17.2.4-0ubuntu1~16.04.4_i386.deb ...
Unpacking libegl1-mesa:i386 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../libwayland-egl1-mesa_17.2.4-0ubuntu1~16.04.4_i386.deb ...
De-configuring libwayland-egl1-mesa:amd64 (17.0.7-0ubuntu0.16.04.2) ...
Unpacking libwayland-egl1-mesa:i386 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../libwayland-egl1-mesa_17.2.4-0ubuntu1~16.04.4_amd64.deb ...
Unpacking libwayland-egl1-mesa:amd64 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...
Setting up libgbm1:amd64 (17.2.4-0ubuntu1~16.04.4) ...
Setting up libgbm1:i386 (17.2.4-0ubuntu1~16.04.4) ...
Setting up libglapi-mesa:amd64 (17.2.4-0ubuntu1~16.04.4) ...
Setting up libglapi-mesa:i386 (17.2.4-0ubuntu1~16.04.4) ...
Setting up libgl1-mesa-dri:amd64 (17.2.4-0ubuntu1~16.04.4) ...
Installing new version of config file /etc/drirc ...
Setting up libgl1-mesa-dri:i386 (17.2.4-0ubuntu1~16.04.4) ...
Setting up libegl1-mesa:amd64 (17.2.4-0ubuntu1~16.04.4) ...
Setting up libegl1-mesa:i386 (17.2.4-0ubuntu1~16.04.4) ...
Setting up libwayland-egl1-mesa:amd64 (17.2.4-0ubuntu1~16.04.4) ...
Setting up libwayland-egl1-mesa:i386 (17.2.4-0ubuntu1~16.04.4) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...
(Reading database ... 551848 files and directories currently installed.)
Preparing to unpack .../hhvm_3.24.1-1~xenial_amd64.deb ...
[ ok ] Stopping hhvm (via systemctl): hhvm.service.
********************************************************************
* HHVM is being removed. You can remove it from your webserver with:
* 
* $ sudo /usr/share/hhvm/uninstall_fastcgi.sh
* $ sudo /etc/init.d/nginx restart
* $ sudo /etc/init.d/apache restart
********************************************************************
Unpacking hhvm (3.24.1-1~xenial) over (3.24.0-1~xenial) ...
Preparing to unpack .../libxatracker2_17.2.4-0ubuntu1~16.04.4_amd64.deb ...
Unpacking libxatracker2:amd64 (17.2.4-0ubuntu1~16.04.4) over (17.0.7-0ubuntu0.16.04.2) ...
Preparing to unpack .../linux-firmware_1.157.15_all.deb ...
Unpacking linux-firmware (1.157.15) over (1.157.13) ...
Preparing to unpack .../ndiswrapper_1.60-3~ubuntu16.04.2_amd64.deb ...
Unpacking ndiswrapper (1.60-3~ubuntu16.04.2) over (1.60-3~ubuntu16.04.1) ...
Preparing to unpack .../ndiswrapper-dkms_1.60-3~ubuntu16.04.2_all.deb ...

-------- Uninstall Beginning --------
Module:  ndiswrapper
Version: 1.60
Kernel:  4.4.0-31-generic (x86_64)
-------------------------------------

Status: Before uninstall, this module version was ACTIVE on this kernel.

ndiswrapper.ko:
 - Uninstallation
   - Deleting from: /lib/modules/4.4.0-31-generic/updates/
 - Original module
   - No original module was found for this module on this kernel.
   - Use the dkms install command to reinstall any previous module version.

depmod.........

DKMS: uninstall completed.

-------- Uninstall Beginning --------
Module:  ndiswrapper
Version: 1.60
Kernel:  4.8.0-53-generic (x86_64)
-------------------------------------

Status: Before uninstall, this module version was ACTIVE on this kernel.

ndiswrapper.ko:
 - Uninstallation
   - Deleting from: /lib/modules/4.8.0-53-generic/updates/
 - Original module
   - No original module was found for this module on this kernel.
   - Use the dkms install command to reinstall any previous module version.

depmod..........

DKMS: uninstall completed.

------------------------------
Deleting module version: 1.60
completely from the DKMS tree.
------------------------------
Done.
Unpacking ndiswrapper-dkms (1.60-3~ubuntu16.04.2) over (1.60-3~ubuntu16.04.1) ...
Preparing to unpack .../ndiswrapper-utils-1.9_1.60-3~ubuntu16.04.2_all.deb ...
Unpacking ndiswrapper-utils-1.9 (1.60-3~ubuntu16.04.2) over (1.60-3~ubuntu16.04.1) ...
Processing triggers for systemd (229-4ubuntu21) ...
Processing triggers for ureadahead (0.100.0-19) ...
ureadahead will be reprofiled on next reboot
Processing triggers for libc-bin (2.23-0ubuntu10) ...
Processing triggers for man-db (2.7.5-1) ...
Setting up mysql-server-5.7 (5.7.21-0ubuntu0.16.04.1) ...
insserv: warning: current start runlevel(s) (empty) of script `mysql' overrides LSB defaults (2 3 4 5).
insserv: warning: current stop runlevel(s) (0 1 2 3 4 5 6) of script `mysql' overrides LSB defaults (0 1 6).
mysql_upgrade: Got error: 2002: Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2) while connecting to the MySQL server
Upgrade process encountered error and will not continue.
mysql_upgrade failed with exit status 11
dpkg: error processing package mysql-server-5.7 (--configure):
 subprocess installed post-installation script returned error exit status 1
dpkg: dependency problems prevent configuration of mysql-server:
 mysql-server depends on mysql-server-5.7; however:
  Package mysql-server-5.7 is not configured yet.

dpkg: error processing package mysql-server (--configure):
 dependency problems - leaving unconfigured
Setting up mesa-common-dev:amd64 (17.2.4-0ubuntu1~16.04.4) ...
Setting up libgl1-mesa-glx:amd64 (17.2.4-0ubuntu1~16.04.4) ...
Setting up libgl1-mesa-glx:i386 (17.2.4-0ubuntu1~16.04.4) ...
Setting up libgl1-mesa-dev:amd64 (17.2.4-0ubuntu1~16.04.4) ...
Setting up libgles2-mesa:amd64 (17.2.4-0ubuntu1~16.04.4) ...
Setting up hhvm (3.24.1-1~xenial) ...
********************************************************************
* HHVM is installed.
*
* Running PHP web scripts with HHVM is done by having your
* webserver talk to HHVM over FastCGI. Install nginx or Apache,
* and then:
* $ sudo /usr/share/hhvm/install_fastcgi.sh
* $ sudo /etc/init.d/hhvm restart
* (if using nginx)  $ sudo /etc/init.d/nginx restart
* (if using apache) $ sudo /etc/init.d/apache restart
*
* Detailed FastCGI directions are online at:
* https://github.com/facebook/hhvm/wiki/FastCGI
*
* If you're using HHVM to run web scripts, you probably want it
* to start at boot:
* $ sudo update-rc.d hhvm defaults
*
* Running command-line scripts with HHVM requires no special setup:
* $ hhvm whatever.php
*
* You can use HHVM for /usr/bin/php even if you have php-cli
* installed:
* $ sudo /usr/bin/update-alternatives \
*    --install /usr/bin/php php /usr/bin/hhvm 60
********************************************************************
Setting up libxatracker2:amd64 (17.2.4-0ubuntu1~16.04.4) ...
Setting up linux-firmware (1.157.15) ...
update-initramfs: Generating /boot/initrd.img-4.8.0-53-generic
Warning: No support for locale: en_US.utf8
update-initramfs: Generating /boot/initrd.img-4.4.0-31-generic
Warning: No support for locale: en_US.utf8
update-initramfs: Generating /boot/initrd.img-4.4.0-21-generic
Warning: No support for locale: en_US.utf8
Setting up ndiswrapper (1.60-3~ubuntu16.04.2) ...
Setting up ndiswrapper-dkms (1.60-3~ubuntu16.04.2) ...
Loading new ndiswrapper-1.60 DKMS files...
Building only for 4.8.0-53-generic
Building initial module for 4.8.0-53-generic
Done.

ndiswrapper:
Running module version sanity check.
 - Original module
   - No original module exists within this kernel
 - Installation
   - Installing to /lib/modules/4.8.0-53-generic/updates/

depmod........

DKMS: install completed.
Setting up ndiswrapper-utils-1.9 (1.60-3~ubuntu16.04.2) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...
Processing triggers for shim-signed (1.32~16.04.1+0.9+1474479173.6c180c6-1ubuntu1) ...
Secure Boot not enabled on this system.
Errors were encountered while processing:
 mysql-server-5.7
 mysql-server
E: Sub-process /usr/bin/dpkg returned an error code (1)
petanikode@imajinasi ~ $ apt install mysql-server-
mysql-server-5.7       mysql-server-core-5.7  
petanikode@imajinasi ~ $ apt install mysql-server-
mysql-server-5.7       mysql-server-core-5.7  
petanikode@imajinasi ~ $ apt install mysql-server-5.7 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
mysql-server-5.7 is already the newest version (5.7.21-0ubuntu0.16.04.1).
The following packages were automatically installed and are no longer required:
  libllvm4.0 libllvm4.0:i386
Use 'sudo apt autoremove' to remove them.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
2 not fully installed or removed.
After this operation, 0 B of additional disk space will be used.
Do you want to continue? [Y/n] y
Setting up mysql-server-5.7 (5.7.21-0ubuntu0.16.04.1) ...
insserv: warning: current start runlevel(s) (empty) of script `mysql' overrides LSB defaults (2 3 4 5).
insserv: warning: current stop runlevel(s) (0 1 2 3 4 5 6) of script `mysql' overrides LSB defaults (0 1 6).
mysql_upgrade: Got error: 2002: Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2) while connecting to the MySQL server
Upgrade process encountered error and will not continue.
mysql_upgrade failed with exit status 11
dpkg: error processing package mysql-server-5.7 (--configure):
 subprocess installed post-installation script returned error exit status 1
dpkg: dependency problems prevent configuration of mysql-server:
 mysql-server depends on mysql-server-5.7; however:
  Package mysql-server-5.7 is not configured yet.

dpkg: error processing package mysql-server (--configure):
 dependency problems - leaving unconfigured
Errors were encountered while processing:
 mysql-server-5.7
 mysql-server
E: Sub-process /usr/bin/dpkg returned an error code (1)
petanikode@imajinasi ~ $ apt -f install
apt
Usage: apt command [options]
       apt help command [options]

Commands:
  add-repository   - Add entries to apt sources.list
  autoclean        - Erase old downloaded archive files
  autoremove       - Remove automatically all unused packages
  build            - Build binary or source packages from sources
  build-dep        - Configure build-dependencies for source packages
  changelog        - View a package's changelog
  check            - Verify that there are no broken dependencies
  clean            - Erase downloaded archive files
  contains         - List packages containing a file
  content          - List files contained in a package
  deb              - Install a .deb package
  depends          - Show raw dependency information for a package
  dist-upgrade     - Upgrade the system by removing/installing/upgrading packages
  download         - Download the .deb file for a package
  edit-sources     - Edit /etc/apt/sources.list with your preferred text editor
  dselect-upgrade  - Follow dselect selections
  full-upgrade     - Same as 'dist-upgrade'
  held             - List all held packages
  help             - Show help for a command
  hold             - Hold a package
  install          - Install/upgrade packages
  list             - List packages based on package names
  policy           - Show policy settings
  purge            - Remove packages and their configuration files
  recommends       - List missing recommended packages for a particular package
  rdepends         - Show reverse dependency information for a package
  reinstall        - Download and (possibly) reinstall a currently installed package
  remove           - Remove packages
  search           - Search for a package by name and/or expression
  show             - Display detailed information about a package
  showhold         - Same as 'held'
  source           - Download source archives
  sources          - Same as 'edit-sources'
  unhold           - Unhold a package
  update           - Download lists of new/upgradable packages
  upgrade          - Perform a safe upgrade
  version          - Show the installed version of a package

petanikode@imajinasi ~ $ sudo apt install -f
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libllvm4.0 libllvm4.0:i386
Use 'sudo apt autoremove' to remove them.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
2 not fully installed or removed.
After this operation, 0 B of additional disk space will be used.
Setting up mysql-server-5.7 (5.7.21-0ubuntu0.16.04.1) ...
insserv: warning: current start runlevel(s) (empty) of script `mysql' overrides LSB defaults (2 3 4 5).
insserv: warning: current stop runlevel(s) (0 1 2 3 4 5 6) of script `mysql' overrides LSB defaults (0 1 6).
mysql_upgrade: Got error: 2002: Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2) while connecting to the MySQL server
Upgrade process encountered error and will not continue.
mysql_upgrade failed with exit status 11
dpkg: error processing package mysql-server-5.7 (--configure):
 subprocess installed post-installation script returned error exit status 1
dpkg: dependency problems prevent configuration of mysql-server:
 mysql-server depends on mysql-server-5.7; however:
  Package mysql-server-5.7 is not configured yet.

dpkg: error processing package mysql-server (--configure):
 dependency problems - leaving unconfigured
Errors were encountered while processing:
 mysql-server-5.7
 mysql-server
E: Sub-process /usr/bin/dpkg returned an error code (1)
petanikode@imajinasi ~ $ sudo mysql -u root -p
Enter password: 
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2)
petanikode@imajinasi ~ $ sudo service mysql status
● mysql.service - MySQL Community Server
   Loaded: loaded (/lib/systemd/system/mysql.service; disabled; vendor preset: e
   Active: inactive (dead)

Jan 31 04:02:43 imajinasi systemd[1]: Started MySQL Community Server.
Jan 31 04:02:49 imajinasi systemd[1]: Stopping MySQL Community Server...
Jan 31 04:02:50 imajinasi systemd[1]: Stopped MySQL Community Server.
Jan 31 04:02:51 imajinasi systemd[1]: Stopped MySQL Community Server.
Jan 31 04:06:28 imajinasi systemd[1]: Stopped MySQL Community Server.
Jan 31 04:06:31 imajinasi systemd[1]: Stopped MySQL Community Server.
Jan 31 04:09:08 imajinasi systemd[1]: Stopped MySQL Community Server.
Jan 31 04:09:11 imajinasi systemd[1]: Stopped MySQL Community Server.
Jan 31 04:09:27 imajinasi systemd[1]: Stopped MySQL Community Server.
Jan 31 04:09:28 imajinasi systemd[1]: Stopped MySQL Community Server.
petanikode@imajinasi ~ $ sudo service mysql start
petanikode@imajinasi ~ $ sudo service mysql status
● mysql.service - MySQL Community Server
   Loaded: loaded (/lib/systemd/system/mysql.service; disabled; vendor preset: e
   Active: active (running) since Wed 2018-01-31 04:11:00 WITA; 1s ago
  Process: 5307 ExecStartPost=/usr/share/mysql/mysql-systemd-start post (code=ex
  Process: 5298 ExecStartPre=/usr/share/mysql/mysql-systemd-start pre (code=exit
 Main PID: 5306 (mysqld)
    Tasks: 28
   Memory: 135.3M
      CPU: 251ms
   CGroup: /system.slice/mysql.service
           └─5306 /usr/sbin/mysqld

Jan 31 04:10:59 imajinasi systemd[1]: Starting MySQL Community Server...
Jan 31 04:11:00 imajinasi systemd[1]: Started MySQL Community Server.
petanikode@imajinasi ~ $ sudo mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 3
Server version: 5.7.21-0ubuntu0.16.04.1 (Ubuntu)

Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> ^DBye
petanikode@imajinasi ~ $ sudo apt install -f
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libllvm4.0 libllvm4.0:i386
Use 'sudo apt autoremove' to remove them.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
2 not fully installed or removed.
After this operation, 0 B of additional disk space will be used.
Setting up mysql-server-5.7 (5.7.21-0ubuntu0.16.04.1) ...
insserv: warning: current start runlevel(s) (empty) of script `mysql' overrides LSB defaults (2 3 4 5).
insserv: warning: current stop runlevel(s) (0 1 2 3 4 5 6) of script `mysql' overrides LSB defaults (0 1 6).
mysql_upgrade: Got error: 2002: Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2) while connecting to the MySQL server
Upgrade process encountered error and will not continue.
mysql_upgrade failed with exit status 11
dpkg: error processing package mysql-server-5.7 (--configure):
 subprocess installed post-installation script returned error exit status 1
dpkg: dependency problems prevent configuration of mysql-server:
 mysql-server depends on mysql-server-5.7; however:
  Package mysql-server-5.7 is not configured yet.

dpkg: error processing package mysql-server (--configure):
 dependency problems - leaving unconfigured
Errors were encountered while processing:
 mysql-server-5.7
 mysql-server
E: Sub-process /usr/bin/dpkg returned an error code (1)
petanikode@imajinasi ~ $ sudo service mysql status
● mysql.service - MySQL Community Server
   Loaded: loaded (/lib/systemd/system/mysql.service; disabled; vendor preset: e
   Active: inactive (dead)

Jan 31 04:06:31 imajinasi systemd[1]: Stopped MySQL Community Server.
Jan 31 04:09:08 imajinasi systemd[1]: Stopped MySQL Community Server.
Jan 31 04:09:11 imajinasi systemd[1]: Stopped MySQL Community Server.
Jan 31 04:09:27 imajinasi systemd[1]: Stopped MySQL Community Server.
Jan 31 04:09:28 imajinasi systemd[1]: Stopped MySQL Community Server.
Jan 31 04:10:59 imajinasi systemd[1]: Starting MySQL Community Server...
Jan 31 04:11:00 imajinasi systemd[1]: Started MySQL Community Server.
Jan 31 04:11:17 imajinasi systemd[1]: Stopping MySQL Community Server...
Jan 31 04:11:19 imajinasi systemd[1]: Stopped MySQL Community Server.
Jan 31 04:11:20 imajinasi systemd[1]: Stopped MySQL Community Server.
petanikode@imajinasi ~ $ apt clean
petanikode@imajinasi ~ $ sudo apt install -f
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libllvm4.0 libllvm4.0:i386
Use 'sudo apt autoremove' to remove them.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
2 not fully installed or removed.
After this operation, 0 B of additional disk space will be used.
Setting up mysql-server-5.7 (5.7.21-0ubuntu0.16.04.1) ...
insserv: warning: current start runlevel(s) (empty) of script `mysql' overrides LSB defaults (2 3 4 5).
insserv: warning: current stop runlevel(s) (0 1 2 3 4 5 6) of script `mysql' overrides LSB defaults (0 1 6).
mysql_upgrade: Got error: 2002: Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (2) while connecting to the MySQL server
Upgrade process encountered error and will not continue.
mysql_upgrade failed with exit status 11
dpkg: error processing package mysql-server-5.7 (--configure):
 subprocess installed post-installation script returned error exit status 1
dpkg: dependency problems prevent configuration of mysql-server:
 mysql-server depends on mysql-server-5.7; however:
  Package mysql-server-5.7 is not configured yet.

dpkg: error processing package mysql-server (--configure):
 dependency problems - leaving unconfigured
Errors were encountered while processing:
 mysql-server-5.7
 mysql-server
E: Sub-process /usr/bin/dpkg returned an error code (1)
petanikode@imajinasi ~ $ sudo mv /etc/mysql/my.cnf /etc/mysql/my.cnf.bak
petanikode@imajinasi ~ $ sudo rm -r /etc/mysql/mysql.conf.d/
petanikode@imajinasi ~ $ sudo find / -name my.cnf
find: ‘/run/user/1000/gvfs’: Permission denied
/etc/alternatives/my.cnf

^C
petanikode@imajinasi ~ $ sudo mv /etc/mysql/debian.cnf /etc/mysql/debian.cnf.bakpetanikode@imajinasi ~ $ sudo apt purge mysql-server mysql-server-5.7 mysql-server-core-5.7
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libevent-core-2.0-5 libllvm4.0 libllvm4.0:i386
Use 'sudo apt autoremove' to remove them.
The following packages will be REMOVED:
  mysql-server* mysql-server-5.7* mysql-server-core-5.7*
0 upgraded, 0 newly installed, 3 to remove and 0 not upgraded.
2 not fully installed or removed.
After this operation, 94,7 MB disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database ... 551865 files and directories currently installed.)
Removing mysql-server (5.7.21-0ubuntu0.16.04.1) ...
Removing mysql-server-5.7 (5.7.21-0ubuntu0.16.04.1) ...
update-alternatives: using /etc/mysql/my.cnf.fallback to provide /etc/mysql/my.cnf (my.cnf) in auto mode
Purging configuration files for mysql-server-5.7 (5.7.21-0ubuntu0.16.04.1) ...
Removing mysql-server-core-5.7 (5.7.21-0ubuntu0.16.04.1) ...
Processing triggers for man-db (2.7.5-1) ...
petanikode@imajinasi ~ $ sudo apt install mysql-server
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libllvm4.0 libllvm4.0:i386
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  mysql-server-5.7 mysql-server-core-5.7
Suggested packages:
  mailx tinyca
Recommended packages:
  libhtml-template-perl
The following NEW packages will be installed:
  mysql-server mysql-server-5.7 mysql-server-core-5.7
0 upgraded, 3 newly installed, 0 to remove and 0 not upgraded.
Need to get 10,5 MB of archives.
After this operation, 94,7 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 mysql-server-core-5.7 amd64 5.7.21-0ubuntu0.16.04.1 [7.809 kB]
Get:2 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 mysql-server-5.7 amd64 5.7.21-0ubuntu0.16.04.1 [2.724 kB]
Get:3 http://archive.ubuntu.com/ubuntu xenial-updates/main amd64 mysql-server all 5.7.21-0ubuntu0.16.04.1 [10,2 kB]
Fetched 10,5 MB in 10s (1.047 kB/s)                                            
Preconfiguring packages ...
Selecting previously unselected package mysql-server-core-5.7.
(Reading database ... 551678 files and directories currently installed.)
Preparing to unpack .../mysql-server-core-5.7_5.7.21-0ubuntu0.16.04.1_amd64.deb ...
Unpacking mysql-server-core-5.7 (5.7.21-0ubuntu0.16.04.1) ...
Selecting previously unselected package mysql-server-5.7.
Preparing to unpack .../mysql-server-5.7_5.7.21-0ubuntu0.16.04.1_amd64.deb ...
Unpacking mysql-server-5.7 (5.7.21-0ubuntu0.16.04.1) ...
Selecting previously unselected package mysql-server.
Preparing to unpack .../mysql-server_5.7.21-0ubuntu0.16.04.1_all.deb ...
Unpacking mysql-server (5.7.21-0ubuntu0.16.04.1) ...
Processing triggers for man-db (2.7.5-1) ...
Processing triggers for systemd (229-4ubuntu21) ...
Processing triggers for ureadahead (0.100.0-19) ...
Setting up mysql-server-core-5.7 (5.7.21-0ubuntu0.16.04.1) ...
Setting up mysql-server-5.7 (5.7.21-0ubuntu0.16.04.1) ...
update-alternatives: using /etc/mysql/mysql.cnf to provide /etc/mysql/my.cnf (my.cnf) in auto mode
Renaming removed key_buffer and myisam-recover options (if present)
Checking if update is needed.
Checking server version.
Running queries to upgrade MySQL server.
Checking system database.
mysql.columns_priv                                 OK
mysql.db                                           OK
mysql.engine_cost                                  OK
mysql.event                                        OK
mysql.func                                         OK
mysql.general_log                                  OK
mysql.gtid_executed                                OK
mysql.help_category                                OK
mysql.help_keyword                                 OK
mysql.help_relation                                OK
mysql.help_topic                                   OK
mysql.innodb_index_stats                           OK
mysql.innodb_table_stats                           OK
mysql.ndb_binlog_index                             OK
mysql.plugin                                       OK
mysql.proc                                         OK
mysql.procs_priv                                   OK
mysql.proxies_priv                                 OK
mysql.server_cost                                  OK
mysql.servers                                      OK
mysql.slave_master_info                            OK
mysql.slave_relay_log_info                         OK
mysql.slave_worker_info                            OK
mysql.slow_log                                     OK
mysql.tables_priv                                  OK
mysql.time_zone                                    OK
mysql.time_zone_leap_second                        OK
mysql.time_zone_name                               OK
mysql.time_zone_transition                         OK
mysql.time_zone_transition_type                    OK
mysql.user                                         OK
The sys schema is already up to date (version 1.5.1).
Checking databases.
blog_php.artikel                                   OK
blog_php.user                                      OK
ci_jamkrida.agen                                   OK
ci_jamkrida.ci_sessions                            OK
ci_jamkrida.direksi                                OK
ci_jamkrida.log                                    OK
ci_jamkrida.pesan                                  OK
ci_jamkrida.t_transaksi                            OK
ci_jamkrida.user                                   OK
contoh_graf.jalan                                  OK
contoh_graf.kota                                   OK
cuitter.status                                     OK
cuitter.user                                       OK
dinkop.kegiatan                                    OK
dinkop.pegawai                                     OK
dinkop.program                                     OK
dinkop.spp                                         OK
dinkop.user                                        OK
dlmobi.users                                       OK
epk.bantuan_sosial                                 OK
epk.groups                                         OK
epk.kelompok_tani                                  OK
epk.komoditas                                      OK
epk.login_attempts                                 OK
epk.perkembangan                                   OK
epk.ref_bantuan                                    OK
epk.ref_desa                                       OK
epk.ref_kabupaten                                  OK
epk.ref_kecamatan                                  OK
epk.ref_kegiatan                                   OK
epk.ref_pejabat                                    OK
epk.ref_sumberdana                                 OK
epk.users                                          OK
epk.users_groups                                   OK
epoknak.bansos                                     OK
epoknak.bantuan_bangunan                           OK
epoknak.bantuan_sapras                             OK
epoknak.bantuan_ternak                             OK
epoknak.desa                                       OK
epoknak.kabupaten                                  OK
epoknak.kategori                                   OK
epoknak.kecamatan                                  OK
epoknak.kegiatan                                   OK
epoknak.penjabat                                   OK
epoknak.perkembangan                               OK
epoknak.poktan                                     OK
epoknak.sumberdana                                 OK
epoknak.tahun                                      OK
epoknak.user                                       OK
epoknak_dev.ban_alat_mesin                         OK
epoknak_dev.ban_bangunan                           OK
epoknak_dev.ban_pakan                              OK
epoknak_dev.ban_sosial                             OK
epoknak_dev.ban_ternak                             OK
epoknak_dev.groups                                 OK
epoknak_dev.kelompok_tani                          OK
epoknak_dev.login_attempts                         OK
epoknak_dev.perkembangan                           OK
epoknak_dev.ref_bantuan                            OK
epoknak_dev.ref_desa                               OK
epoknak_dev.ref_jenis_kegiatan                     OK
epoknak_dev.ref_kabupaten                          OK
epoknak_dev.ref_kecamatan                          OK
epoknak_dev.ref_pejabat                            OK
epoknak_dev.ref_sumber_dana                        OK
epoknak_dev.user                                   OK
epoknak_dev.users                                  OK
epoknak_dev.users_groups                           OK
lab_petanikode.kelas                               OK
lab_petanikode.learning                            OK
lab_petanikode.migrations                          OK
lab_petanikode.modul                               OK
lab_petanikode.password_resets                     OK
lab_petanikode.users                               OK
larablog.migrations                                OK
larablog.password_resets                           OK
larablog.posts                                     OK
larablog.users                                     OK
lokasi.desa                                        OK
lokasi.kabupaten                                   OK
lokasi.kecamatan                                   OK
mahasiswa.matakul                                  OK
my_php_project.phinxlog                            OK
my_php_project.users                               OK
pendaftaran_siswa.calon_siswa                      OK
perpustakaan.buku                                  OK
pesbuk.auth_tokens                                 OK
pesbuk.users                                       OK
phpmyadmin.pma__bookmark                           OK
phpmyadmin.pma__central_columns                    OK
phpmyadmin.pma__column_info                        OK
phpmyadmin.pma__designer_settings                  OK
phpmyadmin.pma__export_templates                   OK
phpmyadmin.pma__favorite                           OK
phpmyadmin.pma__history                            OK
phpmyadmin.pma__navigationhiding                   OK
phpmyadmin.pma__pdf_pages                          OK
phpmyadmin.pma__recent                             OK
phpmyadmin.pma__relation                           OK
phpmyadmin.pma__savedsearches                      OK
phpmyadmin.pma__table_coords                       OK
phpmyadmin.pma__table_info                         OK
phpmyadmin.pma__table_uiprefs                      OK
phpmyadmin.pma__tracking                           OK
phpmyadmin.pma__userconfig                         OK
phpmyadmin.pma__usergroups                         OK
phpmyadmin.pma__users                              OK
praktikumblog.artikel                              OK
praktikumblog.menu                                 OK
praktikumblog.user                                 OK
ruwi.jalan                                         OK
ruwi.lokasi                                        OK
ruwi.phinxlog                                      OK
ruwi.users                                         OK
si_budaya_sasak.tabel_admin                        OK
si_budaya_sasak.tabel_informasi                    OK
si_budaya_sasak.tabel_media                        OK
sys.sys_config                                     OK
tangsi_jaya_kom.admin                              OK
tangsi_jaya_kom.produk                             OK
tangsi_jaya_kom.setting                            OK
tokobuku.api_users                                 OK
tokobuku.books                                     OK
ujian.mahasiswa                                    OK
web_a1.tbl_mahasiswa                               OK
web_a1.user                                        OK
Upgrade process completed successfully.
Checking if update is needed.
Setting up mysql-server (5.7.21-0ubuntu0.16.04.1) ...
Processing triggers for systemd (229-4ubuntu21) ...
Processing triggers for ureadahead (0.100.0-19) ...
petanikode@imajinasi ~ $ sudo service mysql status
● mysql.service - MySQL Community Server
   Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: en
   Active: active (running) since Wed 2018-01-31 04:16:21 WITA; 15s ago
 Main PID: 8541 (mysqld)
   CGroup: /system.slice/mysql.service
           └─8541 /usr/sbin/mysqld

Jan 31 04:16:20 imajinasi systemd[1]: Starting MySQL Community Server...
Jan 31 04:16:21 imajinasi systemd[1]: Started MySQL Community Server.
petanikode@imajinasi ~ $ mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 4
Server version: 5.7.21-0ubuntu0.16.04.1 (Ubuntu)

Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| blog_php           |
+--------------------+
29 rows in set (0,00 sec)

mysql> ^DBye
petanikode@imajinasi ~ $ 
```

Setelah ini selesai...

Sekarang masalahnya pada Shutter!

Ia tidak mau mengabil screenshot. 😔

![Error Shutter](/img/upgrade/error-shutter.png)

**Update:**

Solved, tarnyata harus melakukan setting terlebih dahlulu.


![Error Shutter](/img/upgrade/shutter-setting.png)

<!-- 
Laporan bugs: https://bugs.launchpad.net/shutter/+bug/1746347
 -->