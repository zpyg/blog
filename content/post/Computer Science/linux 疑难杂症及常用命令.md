---
title: "Linux 疑难杂症及常用命令"
description: ""
date: 2022-07-17T12:23:45+08:00
categories:
  - Computer Science
tags: []
---


## garuda

> /etc/garuda/garuda-update/config
```conf
SKIP_MIRRORLIST=1
```

## archlinux pacman & AUR

### Wechat and QQ

enable 32bit

deepin-wine-qq
com.qq.weixin.deepin

### 一个或多个 PGP 签名无法校验！

#### 方式一：导入 GPG keys

```bash
gpg (--keyserver <keyserver>) --recv-keys <key>
```

#### 方式二：跳过校验

```bash
makepkg --skippgpcheck
```

## system

### ntfs3

```
λ sudo mount -t ntfs3 /dev/sdb1 /media/data
mount: /media/data: 文件系统类型错误、选项错误、/dev/sdb1 上有坏超级块、缺少代码页或帮助程序或其他错误.
dmesg(1) may have more information after failed mount system call.

[  314.779326] ntfs3: sdb1: volume is dirty and "force" flag is not set!
```

```bash
sudo ntfsfix -d /dev/sdb1
sudo mount -t ntfs3 /dev/sdb1 /mnt/Data
```

## users

```bash
id <username>
```

