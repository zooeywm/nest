---
title: "Linux 问题及解决方法"
description: "工作中遇到过的 Linux 问题及解决方法"
date: "2025-06-05"
lastUpdateDate: "2025-06-05"
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
