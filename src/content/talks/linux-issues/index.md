---
title: "Linux 问题及解决方法"
description: "工作中遇到过的 Linux 问题及解决方法"
date: "2025-06-05"
lastUpdateDate: "2025-06-05"
tags:
  - linux
---

## 5.4.18 内核 缺少 usbip

```bash
sudo apt install linux-tools-5.4.18-85-generic hwdata
sudo update-alternatives --install /usr/local/bin/usbip usbip $(command -v ls /usr/lib/linux-tools/*/usbip | tail -n1) 20
# usbipd 同理
```
