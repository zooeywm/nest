---
title: "Linux 问题及解决方法"
description: "工作中遇到过的 Linux 问题及解决方法"
date: "2025-06-05"
lastUpdateDate: "2025-06-24"
tags:
  - linux
---

## 5.4.18 内核 缺少 usbip

> https://github.com/dorssel/usbipd-win/issues/251

```bash
sudo apt install linux-tools-5.4.18-85-generic hwdata
sudo update-alternatives --install /usr/local/bin/usbip usbip $(command -v ls /usr/lib/linux-tools/*/usbip | tail -n1) 20
# usbipd 同理
```

## usbip 客户端 detach 有几率卡死，让这个设备无法被重定向

不调用客户端的 detach，改为只调用服务端的 unbind 即可

## 用户输错密码被锁定

进入 root shell

```shell
faillock --user <用户名> --reset
```

## Ubuntu: openssl version mismatch built against 30000020 you have 30400000


```shell
sudo apt-get remove openssh-server openssh-client --purge -y
sudo mv /etc/ld.so.cache /etc/ld.so.cache_bak
sudo apt install openssh-server
```

## Usbip 走 tcp 转发手柄设备不能正常使用的问题

经过排查，原因是手柄驱动源码里定义了 20ms 的 timeout，而我们写的 tcp 转发是默认有缓存的，要为转发客户端设置 NoDelay 选项。
