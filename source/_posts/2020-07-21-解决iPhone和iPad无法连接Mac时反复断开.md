---
title: 解决iPhone和iPad用USB连接Mac时反复中断的问题
date: 2020-07-21 23:55:50
tag:
- Mac
- MacBook Pro
- Terminal
- macOS Catalina
category:
- [Mac]
- [macOS]
---

## 问题

**iPhone或iPad使用USB线连接Mac时，会出现反复中断的问题**

## 原因

- USB线损坏
- 不是apple官方原装USB线

## 使用`Terminal`解决

**1、打开`Terminal`，键入以下命令行：**

```sh
$ sudo defaults write com.apple.usbd NoiPadNotifications \ -bool YES
```

**2、使用`Terminal`杀掉USB进程**

敲入以下命令行：

```sh
$ sudo killall -STOP -c usbd
```

## 通过活动监控器（Activity Monitor）强制退出`USBD`进程

> 打开**活动监控器（Activity Monitor）** > 选择**视图(View)** -> 选择所有进程（`All Processes`）-> 搜索`usbd` -> 双击 -> 退出（Quit）-> **强制退出（Force Quit）**

## 参考连接

> [iPhone 7 won't charge from my MacBook Pro](https://apple.stackexchange.com/questions/298573/iphone-7-wont-charge-from-my-macbook-pro)
