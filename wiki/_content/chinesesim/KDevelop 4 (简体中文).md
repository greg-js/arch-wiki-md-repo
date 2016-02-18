*"[KDevelop](http://kdevelop.org/) is a free, open source IDE (Integrated Development Environment) for MS Windows, Mac OS X, Linux, Solaris and FreeBSD. It is a feature-full, plugin extensible IDE for C/C++ and other programming languages. It is based on KDevPlatform, and the [KDE](/index.php/KDE "KDE") and [Qt](/index.php/Qt "Qt") libraries and is under development since 1998."*

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 添加额外的插件](#.E6.B7.BB.E5.8A.A0.E9.A2.9D.E5.A4.96.E7.9A.84.E6.8F.92.E4.BB.B6)
    *   [2.1 首先：安装依赖](#.E9.A6.96.E5.85.88.EF.BC.9A.E5.AE.89.E8.A3.85.E4.BE.9D.E8.B5.96)
    *   [2.2 PHP](#PHP)
    *   [2.3 其它插件](#.E5.85.B6.E5.AE.83.E6.8F.92.E4.BB.B6)
*   [3 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [3.1 KDevCMakeManager](#KDevCMakeManager)
*   [4 可用插件列表](#.E5.8F.AF.E7.94.A8.E6.8F.92.E4.BB.B6.E5.88.97.E8.A1.A8)

## 安装

从[official repositories](/index.php/Official_repositories "Official repositories")中[安装](/index.php/Pacman "Pacman") [kdevelop](https://www.archlinux.org/packages/?name=kdevelop)。

## 添加额外的插件

### 首先：安装依赖

KDevelop 解析器在官方源中，[kdevelop-pg-qt](https://www.archlinux.org/packages/?name=kdevelop-pg-qt)是你需要安装的额外插件。如果这个插件没有安装，该软件是不能编译的。

### PHP

能够从官方源中安装 PHP 插件，该插件提供自动完成和其它一些 PHP特定的功能。

安装好后重启KDevelop 4，你能使用 PHP 插件的功能，包括自动完成 PHP 功能和你的项目功能还有类。

### 其它插件

```
[AUR](/index.php/AUR "AUR"): [kdevelop-extra-plugins](https://aur.archlinux.org/packages/?O=0&C=0&SeB=nd&K=kdevelop-&outdated=&SB=n&SO=a&PP=50&do_Search=Go)在 AUR 中安装。

```

## 故障排除

### KDevCMakeManager

如果你得到这样的一个错误信息，项目管理插件不能加载 ("Could not load project management plugin KDevCMakeManager.")。请确信你的[cmake](https://www.archlinux.org/packages/?name=cmake)已经安装。

## 可用插件列表

As of June 18 2009, the following plugins are available from KDE's svn repository.

*   automake
*   bazaar
*   check
*   controlflowgraph
*   cppunit
*   csharp
*   ctest
*   duchainviewer
*   java
*   metrics
*   oldgdb
*   php
*   php-docs
*   python
*   qmake
*   qtdesigner
*   ruby
*   sloc
*   teamwork
*   xdebug

**Warning:** As of June 17 2009, do not install the php-docs plugin because it causes the php plugin to stop working.