---
title: "linux 配置分享"
description: "Archlinux 配置分享"
date: "2024-04-03"
tags:
  - linux
---

## 分发版选择

我选择使用 Arch Linux，使用 Arch Linux 的优点可以用一句话概括：“简单、轻量、完全掌控”。

## 安装指引

安装文档里有详细介绍，这里不再赘述：https://wiki.archlinux.org/title/installation_guide

可参照我一个朋友的安装步骤, 比较适合新手: [Arch 安装.md](https://github.com/TD-Sky/notebook/blob/main/Arch/%E5%AE%89%E8%A3%85.md)

磁盘分为两个分区：一个2G [uefi](https://wiki.archlinux.org/title/Unified_Extensible_Firmware_Interface)

剩下的是 root 分区，使用 [lvm2](https://wiki.archlinux.org/title/Install_Arch_Linux_on_LVM) 和 [gpt](https://wiki.archlinux.org/title/Partitioning#GUID_Partition_Table)。

## 系统管理

1. 经常运行 `systemctl --failed` 并且修复。
2. tty 字体太小的话 - https://wiki.archlinux.org/title/HiDPI#Linux_console_(tty)
3. 配置：见我的 [dotfiles](https://github.com/zooeywm/dotfiles)
