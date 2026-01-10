---
title: "新型真●一键激活JetBrains全家桶方式，不需要手动下载任何文件(懒人福利)！idea/win/linux/mac - 开发调优"
source: "https://linux.do/t/topic/694120"
author:
  - "[[LINUX DO]]"
published:
created: 2026-01-10
description: "Where possible begins."
tags:
  - "clippings"
---
## 先感谢论坛其他佬发布的激活方式以及激活工具

## 适配了Win、Linux、Mac

## 测试系统

- windows 10
- 乌班图Ubuntu 24.04.2 LTS
- MacOS Sequoia 15.2

## 使用方法

## Windows

- 按键盘Win + X，选择WindowsPowerShell(**管理员**)
- **复制** 命令到刚才打开的PS中运行(一定要复制，不要手输，容易错)
```
irm ckey.run|iex
```
- 会自动扫描安装的JetBrains系列软件，idea等等、稍等片刻即可激活完毕，激活码都不需要输入，全自动

### 如果想查看处理了哪些文件，可以使用debug命令,会输出相应的信息

```bash
irm ckey.run/debug|iex
```

### 查看脚本源代码,把后面的|iex去掉即可

```
irm ckey.run
```
- 取消激活
```bash
irm ckey.run/uninstall|iex
```

## 如果需要自定义激活信息的前往激活网站ckey.run(CodeKey Run)

### idea2025.1.1.1激活图

[![image](https://linux.do/uploads/default/optimized/4X/0/8/5/085c87ec4db4773b30d220400192a25abba675a1_2_690x391.png)](https://linux.do/uploads/default/original/4X/0/8/5/085c87ec4db4773b30d220400192a25abba675a1.png "image")

### 正常模式运行

[![image](https://linux.do/uploads/default/optimized/4X/4/6/4/464c91bf98f49b993665f2571aa98a90a04d2cfb_2_307x500.png)](https://linux.do/uploads/default/original/4X/4/6/4/464c91bf98f49b993665f2571aa98a90a04d2cfb.png "image")

### debug模式运行

[![image](https://linux.do/uploads/default/optimized/4X/1/8/7/18709550a150d35431c9a3540af547809864f5fa_2_453x500.png)](https://linux.do/uploads/default/original/4X/1/8/7/18709550a150d35431c9a3540af547809864f5fa.png "image")
