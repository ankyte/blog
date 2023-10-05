---
author: Ankit Sahu
pubDatetime: 2022-10-03T00:00:00Z
title: Install snort on Kali
postSlug: install-snort-on-kali
featured: true
draft: false
tags:
  - linux
  - snort
  - kali
description: Snort is no longer available in Kali repositories Here are the steps to install snort on Kali
---

## Table of contents

> snort is no longer available in Kali repositories
> Here are the steps to install snort on Kali

## Backup kali's sources.list

```
mv /etc/apt/sources.list /etc/apt/sources.list.bak
```

## Remove updates

```
find /var/lib/apt/lists -type f -exec rm {} \;
```

## Change sources.list content

```
sudo nano /etc/apt/sources.list
```

Paste content given below

```bash
deb http://archive.ubuntu.com/ubuntu/ focal main restricted universe multiverse<br>
deb-src http://archive.ubuntu.com/ubuntu/ focal main restricted universe multiverse<br>

deb http://archive.ubuntu.com/ubuntu/ focal-updates main restricted universe multiverse<br>
deb-src http://archive.ubuntu.com/ubuntu/ focal-updates main restricted universe multiverse<br>

deb http://archive.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse<br>
deb-src http://archive.ubuntu.com/ubuntu/ focal-security main restricted universe multiverse<br>

deb http://archive.ubuntu.com/ubuntu/ focal-backports main restricted universe multiverse<br>
deb-src http://archive.ubuntu.com/ubuntu/ focal-backports main restricted universe multiverse<br>

deb http://archive.canonical.com/ubuntu focal partner<br>
deb-src http://archive.canonical.com/ubuntu focal partner<br>
```

If you are using kali as a virtual machine then paste this instead
As core Ubuntu repositories do not have the ARM repositories in them

```bash
deb [arch=arm64] http://ports.ubuntu.com/ubuntu-ports focal main restricted universe multiverse<br>
deb [arch=arm64] http://ports.ubuntu.com/ubuntu-ports focal-updates main restricted universe multiverse<br>
deb [arch=arm64] http://ports.ubuntu.com/ubuntu-ports focal-security main restricted universe multiverse<br>

deb [arch=i386,amd64] http://us.archive.ubuntu.com/ubuntu/ focal main restricted universe multiverse<br>
deb [arch=i386,amd64] http://us.archive.ubuntu.com/ubuntu/ focal-updates main restricted universe multiverse<br>
deb [arch=i386,amd64] http://security.ubuntu.com/ubuntu focal-security main restricted universe multiverse<br>
```

## Add the specified public keys

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 3B4FE6ACC0B21F32
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 871920D1991BC93C
```

## Update

```bash
sudo apt update
```

## Now install snort

```bash
sudo apt install snort
```
