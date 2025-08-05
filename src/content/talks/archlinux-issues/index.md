---
title: "Arch Linux 问题及解决方法"
description: "日常遇到过的 Arch Linux 问题及解决方法"
date: "2025-02-12"
lastUpdateDate: "2025-04-16"
tags:
  - linux
---

## Hyprland 启动失败

```log
terminate called after throwing an instance of 'std::runtime_error'
what():  wlr_backend_autocreate() failed!
pcilib: Error reading /sys/bus/pci/devices/0000:00:08.3/label: Operation not permitted
terminate called recursively
Aborted (core dumped)
```

修复方式：`pacman -S polkit`

## Hyprland 休眠后无法恢复现场

在 `/etc/mkinitcpio.conf` `HOOKS` 中，将 `resume` 添加到 `udev` 后面

## clash-meta 授权问题

`sudo /usr/bin/setcap 'cap_net_admin,cap_net_bind_service=+ep' /usr/bin/clash-meta`
更好做法是[添加 pacman hook](https://github.com/zooeywm/dotfiles/blob/main/root/etc/pacman.d/hooks/clash-meta.hook)

## OBS 无法录屏和虚拟摄像头

录屏需要：`pipewire-v4l2`
虚拟摄像头：`v4l2loopback-dkms`

## nvim MarkdownPreview 错误：Cannot find module 'tslib'

<https://github.com/iamcco/markdown-preview.nvim/issues/188#issuecomment-841356921>

    `z ~/.local/share/LazyVim/lazy/markdown-preview.nvim/app && npm install`

## Clash 跟 ssh 22 端口冲突：

    在 clash 订阅配置中添加 `- DST-PORT,22,DIRECT`.

## bluetoothctl: No default controller available

```zsh
bluetooth hci0: Direct firmware load for mediatek/BT_RAM_CODE_MT7961_1a_2_hdr.bin failed with error -2
```

因为我使用了 AUR 的`linux-firmware-git`, 安装官方的 `linux-firmware` 即可解决问题。

## 火狐浏览器或 zen-browser dpi 配置

<https://support.mozilla.org/zh-CN/questions/1378420>

调整 about:config 中的 layout.css.devPixelsPerPx

## waydorid 报错：waydroid session start RuntimeError: Command failed: % /usr/lib/waydroid/data/scripts/waydroid-net.sh start

原因是 53 端口被占用，dnsmasq 监听了 0.0.0.0:53
解决方式：修改 /etc/dnsmasq.conf，设置 `listen-address=127.0.0.1` 以及 `bind-interfaces` 然后 sudo systemctl restart dnsmasq 即可

## nvim markdown-preview 无响应

https://github.com/iamcco/markdown-preview.nvim/issues/424#issuecomment-1033083561

## nftables 打开防火墙

编辑 `/etc/nftables.conf`

添加 `tcp dport 3240 accept`

并执行 `sudo nft -f /etc/nftables.conf`

## systemd-nspawn 容器突然提示某些目录找不到

看看有没有 /proc/sys/fs/binfmt_misc/qemu-aarch64 这样的文件，如果没有，说明 qemu-user-static-binfmt 没有正确安装。

重装一遍 sudo pacman -S qemu-user-static-binfmt
