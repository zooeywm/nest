---
title: "rclone 配置"
description: "rclone 配置"
date: "2024-04-14"
lastUpdateDate: "2025-02-13"
tags:
  - linux
  - file-manage
---

## rclone

> 详见 <https://rclone.org/docs/>

## 配置 GoogleDrive

请按照指示完成 Google Drive 配置： <https://rclone.org/drive/#making-your-own-client-id>

## 配置 OneDrive 组织

参照：<https://rclone.org/webdav>，使用 sharepoint 和 webdav，请注意，需要对密码进行加密。

## 用法

在使用了 `Mount`，`Sync`，`Copy` 以及 `BiSync` 模式之后，我最终选择了使用 `BiSync` 模式，因为 `Mount` 是基于 `FUSE` 的，当其守护进程结束之后，本地数据都会被抹除。`Copy` 模式不能删除远程文件。`Sync` 是单向操作，所以我选择了双向操作的 `BiSync`

```zsh
rclone bisync GoogleDrive: ~/Documents/rclone/GoogleDrive --create-empty-src-dirs --compare size,modtime,checksum --slow-hash-sync-only --resilient -MvP --drive-skip-gdocs --fix-case
```
