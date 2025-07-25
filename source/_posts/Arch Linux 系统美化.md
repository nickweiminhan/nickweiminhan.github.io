---
layout:     post
title:      "2025-03-11-Arch Linux 系统美化"
subtitle:   "Arch Linux 系统美化"
date:       2025-03-11 21:00:06
author:     "Nickwei"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - 随笔
---







本文讲述如何配置以让 KDE 桌面环境看起来更加拥有美感。 原则：美化不应该付出大量的时间折腾，既没有实际用处，也没有意义。花最少的时间完成性价比最高的美化始终是第一原则。

> 在 KDE 相关软件更新前后，出现过第三方主题不稳定/卡顿的问题，再次强调不要美化魔改的太过，这会添加更多的不确定性，让你的桌面稳定性下降。

## 01. 壁纸

在桌面右键，选择`配置桌面`。在新出现的窗口中右下角选择`添加图片`可以选择你想要的图片。其中`位置`一项选择’缩放，保持比例’，`背景`一项选择’模糊’。这样你就可以拥有一个成比例，且边缘带有高斯模糊的漂亮的桌面壁纸。

## 02. 系统主题

使用一个高质量的系统主题可以直线提升系统的美观程度。*系统设置* > *外观* > *全局主题* > *获取新的全局主题* ，搜索主题 layan，进行设置即可。 顺便说一句，这个主题的作者 vinceliuice 是一位中国大佬，是一位设计师，他设计的主题以及图标的质量都很高，你可以去他的[主页](https://www.pling.com/u/vinceliuice/)为他打分和点赞。

> 如果切换主题后，windows 键不能呼出菜单，可在左下角右键，配置程序启动器，在键盘快捷键中重新设置`windows+F1`键，windows 键会显示为 Meta 键。

## 03. 窗口装饰

在 *系统设置* > *外观* > *窗口装饰* 中，获取新窗口装饰，搜索 layan，并应用即可。

## 04. 系统图标

如果主题中的图标不能满足你，那么可以选择一些自定义的图标。*系统设置* > *外观* > *图标* > *获取新图标主题* ，搜索图标名 Tela-icon-theme，进行安装设置即可。

## 05. SDDM 主题

你应该注意得到，输入密码时默认的登录界面是很丑的，这里也可以替换掉。*系统设置* > *开机和关机* > *登录屏幕(SDDM)* > *获取新登录屏幕* ，搜索 SDDM 主题 layan 并设置即可。

## 06. 欢迎屏幕（splashscreen）

可以对在登录界面后的欢迎屏幕进行美化。 *系统设置* > *外观* > *欢迎屏幕* > *获取新欢迎屏幕* ，搜索 miku 进行设置即可。这个`Snowy Night Miku`是我们搜索到的最好看的二刺猿属性的初始界面了。另外，还有一个大佬做了一些二次元主题的欢迎屏幕，但是质量一般，这里是他的[主页](https://www.pling.com/u/thevladsoft/)。

## 07. 桌面插件

在任务栏空白处右键，选择编辑面板，添加部件。

- Netspeed widget 网速组件，这个很实用
- todolist 任务组件

然后把你经常使用的软件固定在任务栏即可。

KDE Plasma 5.22.1 更新后，需要额外安装 ksysguard 才能确保桌面插件的正常运行。[相关资料](https://github.com/dfaust/plasma-applet-netspeed-widget/issues/28)

## 08. 混成器

*系统设置* > *显示和监控* > *混成器* 开启混成器

## 09. 终端样式设置

打开 konsole， *设置* > *编辑当前方案* > *外观* ，选择`Red-Black` 应用确认即可。

## 10. Kvantum Manager

主题配合 Kvantum Manager 可以达到更好的效果。

```
sudo pacman -S kvantum

BASH
```

在[这里](https://www.pling.com/p/1325246/)下载 Layan 的 Kvantum 主题，并解压。打开 Kvantum Manager,选择主题并安装，接下来在`Change/Delete Theme`中选择 Layan,Use this theme。最后在系统设置，外观中的应用程序风格中选择 kvantum 即可。

> 如果透明的效果没有显示，确保 KDE 的全局缩放比例为整数倍。或者尝试切换混成器中 openGL 的设置。

## 11. GRUB 主题

[官方文档](https://wiki.archlinux.org/title/GRUB/Tips_and_tricks#Theme)

在[pling](https://www.pling.com/browse/cat/109/order/latest/)选择下载你想要的 GRUB 主题，比如这个[二刺螈主题](https://www.pling.com/p/1526503/)。接下来 `cd` 进解压出来的文件夹，打开 konsole 输入

```
sudo cp -r . /usr/share/grub/themes/Nino

BASH
```

以将主题放置在系统的 GRUB 默认文件夹内。 接着编辑 `/etc/default/grub` 文件，找到 `#GRUB_THEME=` 一行，将前面的注释去掉，并指向主题的 `theme.txt` 文件。即

```
#GRUB_THEME=
GRUB_THEME="/usr/share/grub/themes/Nino/theme.txt" #修改后

BASH
```

然后再在终端输入

```
sudo grub-mkconfig -o /boot/grub/grub.cfg

BASH
```

更新 GRUB ，并重启即可。

## 12. 开机动画

[Plymouth](https://fedoraproject.org/wiki/Releases/FeatureBetterStartup) 是一个来自于 Fedora 社区的提供美化启动图形界面的功能的项目，如有需要，可以参考[官方文档](https://wiki.archlinux.org/title/Plymouth_(简体中文))进行配置。不建议新手在此项配置上花费太多时间。







