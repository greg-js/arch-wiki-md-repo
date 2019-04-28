<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 下载链接：](#下载链接：)
*   [2 主要特性](#主要特性)
*   [3 XX-Net不是匿名工具](#XX-Net不是匿名工具)
*   [4 平台支持情况](#平台支持情况)
*   [5 链接](#链接)
*   [6 使用方法](#使用方法)
*   [7 感谢](#感谢)
*   [8 如何帮助项目](#如何帮助项目)
*   [9 附图](#附图)
*   [10 集成XX-Net的项目](#集成XX-Net的项目)

## 下载链接：

最新发布： [https://github.com/XX-net/XX-Net/releases/latest](https://github.com/XX-net/XX-Net/releases/latest)

版本历史和说明： [https://github.com/XX-net/XX-Net/releases](https://github.com/XX-net/XX-Net/releases)

## 主要特性

*   大量改良过的GoAgent 稳定快速
*   Web界面，傻瓜易用
*   内置了公共 appid，便新手
*   自动导入证书，减少大量手动工作
*   可设置开机启动
*   支持自动升级，保留辛苦找到的ip资源

## XX-Net不是匿名工具

详情请看：[https://github.com/XX-net/XX-Net/wiki/Anonymous-and-Security](https://github.com/XX-net/XX-Net/wiki/Anonymous-and-Security)

## 平台支持情况

*   Windows XP （需要 tcpip.sys 补丁, 比如用 tcp-z）
*   Win7/8/10
*   Ubuntu （不显示系统托盘）
*   Debian （debian 8 php_proxy无法工作）
*   Mac OS X(10.7; 10.8; 10.9; 10.10)
*   ArchLinux(aur仓库：yaourt -S xx-net)

## 链接

*   [https://github.com/XX-net/XX-Net/wiki](https://github.com/XX-net/XX-Net/wiki) 使用指南
*   [https://github.com/XX-net/XX-Net/issues](https://github.com/XX-net/XX-Net/issues) 问题报告
*   [https://groups.google.com/forum/#!forum/xx-net](https://groups.google.com/forum/#!forum/xx-net) 讨论群
*   Email:xxnet.dev at gmail.com

## 使用方法

	AUR 仓库收录

`yaourt -S xx-net`

*   [https://github.com/XX-net/XX-Net/wiki/中文文档](https://github.com/XX-net/XX-Net/wiki/中文文档) 中文文档
*   [https://github.com/XX-net/XX-Net/wiki/English-Home-Page](https://github.com/XX-net/XX-Net/wiki/English-Home-Page) English
*   [https://github.com/XX-net/XX-Net/wiki/Persian-home-page](https://github.com/XX-net/XX-Net/wiki/Persian-home-page) Persian

安装xx-net需要有judy依赖。judy在安装时需要automake，autoconfig，但并未作为依赖由pacman安装，需要手动下载。

如需要自动启动，可按照github中wiki所说安装supervisor，同时xx-net的安装时产生supervisor的配置文件和服务文件，但该服务名称为supervisord，位于/usr/lib/systemdsystem/supervisord.service

## 感谢

*   GoAgent
*   GoGoTest
*   goagentfindip
*   checkgoogleip

## 如何帮助项目

[如何帮助项目](https://github.com/XX-net/XX-Net/wiki/How-to-contribute)

## 附图

## 集成XX-Net的项目

*   ChromeGAE 主页：[http://www.ccav1.com/chromegae](http://www.ccav1.com/chromegae) 集成Google Chrome和XX-Net的自动翻墙浏览器 维护人：Yanu
*   plusburg 主页：[https://github.com/Plusburg/Plusburg](https://github.com/Plusburg/Plusburg) 集成XX-Net的启动光盘镜像
*   appifed-xx-net [https://github.com/binarydist/appified-xx-net](https://github.com/binarydist/appified-xx-net) Mac OSX 环境下，变成一个标准的app