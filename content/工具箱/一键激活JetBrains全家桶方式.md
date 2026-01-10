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
[跳转到您离开的地方（最后一个回复，帖子 802)](https://linux.do/t/topic/694120/802) [跳转到顶部](https://linux.do/t/topic/694120/1)

## 由 w461313128 发布于 2025 年 6月 2 日

[3A](https://linux.do/u/w461313128) [w461313128](https://linux.do/u/w461313128)

[2025 年 6月](https://linux.do/t/topic/694120?u=zyf "发布日期")

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

## Linux

- 复制命令到终端中执行即可
```
wget --no-check-certificate ckey.run -O ckey.run && bash ckey.run
```
- debug
```bash
wget --no-check-certificate ckey.run/debug -O ckey.run && bash ckey.run
```
- 取消激活
```bash
wget --no-check-certificate ckey.run/uninstall -O ckey.run && bash ckey.run
```

## Mac

- Mac好像是默认没有安装wget，所以用curl,如果你有wget，也可以直接用linux命令
```
curl -L -o ckey.run ckey.run && bash ckey.run
```
- debug
```bash
curl -L -o ckey.run ckey.run/debug && bash ckey.run
```
- 取消激活
```bash
curl -L ckey.run/uninstall -o ckey.run && bash ckey.run
```

## 如果需要自定义激活信息的前往激活网站ckey.run(CodeKey Run)

### idea2025.1.1.1激活图

[![image](https://linux.do/uploads/default/optimized/4X/0/8/5/085c87ec4db4773b30d220400192a25abba675a1_2_690x391.png)](https://linux.do/uploads/default/original/4X/0/8/5/085c87ec4db4773b30d220400192a25abba675a1.png "image")

### 正常模式运行

[![image](https://linux.do/uploads/default/optimized/4X/4/6/4/464c91bf98f49b993665f2571aa98a90a04d2cfb_2_307x500.png)](https://linux.do/uploads/default/original/4X/4/6/4/464c91bf98f49b993665f2571aa98a90a04d2cfb.png "image")

### debug模式运行

[![image](https://linux.do/uploads/default/optimized/4X/1/8/7/18709550a150d35431c9a3540af547809864f5fa_2_453x500.png)](https://linux.do/uploads/default/original/4X/1/8/7/18709550a150d35431c9a3540af547809864f5fa.png "image")

### Linux

[![image](https://linux.do/uploads/default/optimized/4X/b/b/f/bbf65d32daf7d697279d07de462d792cabbd709b_2_689x445.png)](https://linux.do/uploads/default/original/4X/b/b/f/bbf65d32daf7d697279d07de462d792cabbd709b.png "image")

### Mac

[![image](https://linux.do/uploads/default/optimized/4X/0/b/c/0bc91200c8e41b502368c013d7a9eeb0b8e9b943_2_666x500.png)](https://linux.do/uploads/default/original/4X/0/b/c/0bc91200c8e41b502368c013d7a9eeb0b8e9b943.png "image")

## 激活失败的情况

## Mac

- [mac系统如果之前有使用其它工具，导致激活失败的，需要彻底删除缓存、配置等文件](https://linux.do/t/topic/694120/148)

- [一键命令行方式激活JetBrains全家桶及插件](https://linux.do/t/topic/901854)
- [L 站福利及项目信息汇总【开发篇】（不定时更新）](https://linux.do/t/topic/539997)
- [分享一个jetrains全家桶的免费激活办法](https://linux.do/t/topic/812694/33)
- [手把手教你激活pycharm和插件到2048年](https://linux.do/t/topic/626335/75)
- [白嫖 jetbrains 被回收了，破解的是社区版的无法使用 js 该如何选择？](https://linux.do/t/topic/797096/13)