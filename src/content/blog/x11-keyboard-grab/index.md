---
title: "X11 抓取键盘"
description: "X11 抓取键盘踩坑及解决方式"
date: "2025-03-31"
lastUpdateDate: "2025-03-31"
tags:
  - qt
  - x11
---

## 问题

我遇到的问题可以用以下几个链接概括：

[x11 - Unable to move window after XGrabKeyboard](https://stackoverflow.com/questions/14555703/x11-unable-to-move-window-after-xgrabkeyboard)

[Redirect Keyboard input with XGrabKey or XGrabKeyboard](https://stackoverflow.com/questions/23430995/redirect-keyboard-input-with-xgrabkey-or-xgrabkeyboard)

一句话概括就是`XGrabKey`只要有其他客户端 Grab 过你要 Grab 的键位，就会失败，经过经验证明这是大概率失败的，而 `XGrabKeyboard` 也会影响**鼠标拖动窗口**和**调整窗口大小**以上问题均没有解决方案。

## 解决方式

经过一番摸索，我发现 xcb 会在鼠标**进入标题栏**，**抵达窗口边框**和**移出窗口**时触发 `XCB_LEAVE_NOTIFY`，在**离开标题栏**和**进入窗口**时触发 `XCB_ENTER_NOTIFY`，于是在进入的时候调用 XGrabKeyboard,离开的时候调用 XUnGrabKeyboard 即可
