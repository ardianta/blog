---
title: "Install Docker"
slug: install-docker
date: 2017-12-30T17:41:27+08:00
draft: true

type: post

tags:
    - tag

meta:
    image: ""
    keyword: ""
    description: ""
---

```bash
 sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

Update:

```bash
sudo apt-get update
```


Install packages to allow apt to use a repository over HTTPS:

```bash
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```

Add Docker’s official GPG key:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
Verify that you now have the key with the fingerprint 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88,by searching for the last 8 characters of the fingerprint.

```bash
$ sudo apt-key fingerprint 0EBFCD88

pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22
```

```bash
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   xenial \
   stable"
```

N.B: `xenial` untuk Linux Mint 18 (Ubuntu Xenial)


```bash
sudo apt-get update
```

Install Docker CE:

```bash
sudo apt-get install docker-ce
```



https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#install-docker-ce-1