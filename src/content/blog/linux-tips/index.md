---
title: "Linux 记录"
description: "日常 Linux 解决方式记录"
date: "2025-06-09"
lastUpdateDate: "2025-06-09"
tags:
  - linux
---

## ffplay 测试摄像头

```shell
ffplay -f v4l2 -input_format mjpeg -framerate 30 -video_size 640x480 /dev/video0
```

## fio 测试硬盘随机读写速度

```shell
sudo apt install fio

sudo fio --name=random_read_test \
    --filename=/dev/sda \
    --size=10G \
    --rw=randread \
    --bs=64k \
    --direct=1 \
    --numjobs=1 \
    --iodepth=16 \
    --time_based \
    --runtime=30 \
    --ioengine=libaio \
    --group_reporting

sudo fio --name=random_write_test \
    --filename=/dev/sda \
    --size=10G \
    --rw=randwrite \
    --bs=64k \
    --direct=1 \
    --numjobs=1 \
    --iodepth=16 \
    --time_based \
    --runtime=30 \
    --ioengine=libaio \
    --group_reporting
```
