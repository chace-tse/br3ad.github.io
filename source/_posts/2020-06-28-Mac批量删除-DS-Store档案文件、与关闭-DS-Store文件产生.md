---
title: Mac批量删除.DS_Store档案文件、与关闭.DS_Store文件产生
date: 2020-06-28 00:29:23
tags:
- Mac
- MacBook Pro
- macOS Catalina
category:
- [Mac]
- [macOS]
---

1、打开终端，并执行以下命令行

**查找系统所有`.DS_Store`文件并删除**

```sh
sudo find / -name ".DS_Store" -depth -exec rm {} \;
```

2、输入电脑用户管理员密码，会开始进行删除，而这会需要一点时间，需要等一会。

3、彻底解决不让`.DS_Store`文件再产生，只需在终端执行以下命令，即可，若要将它开启时，只需改为false就可以

**禁用或启用自动生成**

**禁止`.DS_Store`生成：**
```sh
defaults write com.apple.desktopservices DSDontWriteNetworkStores true
```

**恢复`.DS_Store`生成：**
```sh
defaults delete com.apple.desktopservices DSDontWriteNetworkStores false

```

4、在项目中如何删除自动生成的`.DS_Store`文件？

如果项目中还没有生成`.DS_Store`文件，那么直接将`.DS_Store`加入到`.gitignore`文件就可以。
如果项目中已存在`.DS_Store`文件，需先从项目中将其删除，然后再将它加入到`.gitignore`文件。

**删除项目中所有的`.DS_Store`文件**

```sh
find . -name .DS_Store -print0 | xargs -0 git rm -f --ignore-unmatch
```

**将`.DS_Store`文件加入到`.gitignore`**

```sh
echo .DS_Store >> ~/.gitignore
```

## 参考链接

> [Mac OS X v10.4 and later: How to prevent .DS_Store file creation over network connections](https://support.apple.com/en-us/HT1629)
