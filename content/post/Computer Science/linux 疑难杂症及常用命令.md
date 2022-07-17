---
title: "Linux 疑难杂症及常用命令"
description: ""
date: 2022-07-17T12:23:45+08:00
categories:
  - Computer Science
tags: []
---


## archlinux pacman & AUR

### 一个或多个 PGP 签名无法校验！

#### 方式一：导入 GPG keys

```bash
gpg (--keyserver <keyserver>) --recv-keys <key>
```

#### 方式二：跳过校验

```bash
makepkg --skippgpcheck
```
