FVWM是X窗口系统下非常强大的ICCCM-compliant多虚拟桌面窗口管理器. It requires some effort to learn to use it well, since it is almost entirely configured by editing configuration files with a text editor, but those who persist end up with a desktop environment that works exactly the way they want it to work. Although using FVWM does not require an knowlege of programming languages, it is possible to extend the power of FVWM with [M4](http://www.fvwm.org/documentation/manpages/stable/FvwmM4.php), [C](http://www.fvwm.org/documentation/manpages/stable/FvwmCpp.php), and [Perl](http://www.fvwm.org/documentation/manpages/stable/FvwmPerl.php) preprocessing. FVWM has a [Perl library](http://www.fvwm.org/documentation/perllib/) that makes creating FVWM modules in Perl possible and easy. Development is active, and support is excellent. And for those who wonder, FVWM means Feeble Virtual Window Manager.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装fvwm](#安装fvwm)
*   [2 启动 FVWM](#启动_FVWM)
*   [3 改进 FVWM](#改进_FVWM)
*   [4 参考](#参考)

## 安装fvwm

从 [官方软件仓库](/index.php/Official_repositories "Official repositories")中[安装](/index.php/Pacman "Pacman") 软件包 [fvwm](https://www.archlinux.org/packages/?name=fvwm)。

也可以从[AUR](/index.php/AUR "AUR")中安装[fvwm-patched](https://aur.archlinux.org/packages/fvwm-patched/).

## 启动 FVWM

fvwm会自动在kdm/gdm加入启动项, 如果没有, 在用户目录下的.xinitrc中手动加入

```
exec fvwm

```

也可以看看 [SLiM](/index.php/SLiM "SLiM") 教程, 关于在.xinitrc怎么配置多种窗口管理器.

详情参阅 [xinitrc](/index.php/Xinitrc "Xinitrc")。

## 改进 FVWM

When you start FVWM for the first time, you will get something that looks very blank. When you left-click on the desktop, you will be able to select a very basic configuration for FVWM. Choose the modules you want and you are ready to get started. You will undoubtedly want to do more to create your desktop, so here are some tips:

*   虽然它很过时，但是它对理解FVWM的工作原理和怎么样建立你自己的基本设置很有帮助. [FVWM beginners guide](http://www.zensites.net/fvwm/guide/)

*   The FVWM homepage[[1]](http://fvwm.org/) includes documentation[[2]](http://fvwm.org/documentation/), a FAQ [[3]](http://fvwm.org/documentation/faq/), and links to a Wiki[[4]](http://fvwmwiki.xteddy.org/)) and the FVWM forums[[5]](http://www.fvwmforums.org).

*   The best way to come up with the desktop you want is probably to check out the configurations in the FVWM forum[[6]](http://www.fvwmforums.org/phpBB3/viewforum.php?f=39&sid=468469f95f9a2a90cd9d5a0819d26eec) or at Box-Look.org,[[7]](http://www.box-look.org) choose one you like, install it, and modify it to taste.

*   As you work with what other people have done, you may find it helpful to look at the tips on configuration files by Thomas Adam, the most active FVWM developer.[[8]](http://www.fvwmforums.org/phpBB3/viewtopic.php?f=40&t=1505)

*   A page[[9]](http://web.archive.org/web/20070912061152/abdn.ac.uk/~u15dm4/fvwm/) in the [Internet Archive](http://archive.org/) is outdated, but seems to be the only significant online documentation for fvwm-patched.

*   FVWM-Crystal, which is also in the Arch repositories as package [fvwm-crystal](https://aur.archlinux.org/packages/fvwm-crystal/), is an add-on that makes FVWM much easier to configure, although the easier configuration allows much less flexibility than direct editing of configuration files.

*   [XdgMenu](/index.php/XdgMenu "XdgMenu") is a useful utility for generating menus.

*   Fvwm plays well with [xcompmgr](/index.php/Xcompmgr "Xcompmgr") for simple compositing effects.

*   Useful applications are similar to those suggested for [Openbox](/index.php/Openbox "Openbox") or [Fluxbox](/index.php/Fluxbox "Fluxbox").

## 参考

1.  Zensites [FVWM beginners guide](http://zensites.net/fvwm/guide/).
2.  [FVWM Homepage](http://fvwm.org/).
3.  FVWM Homepage [documentation](http://fvwm.org/documentation/).
4.  FVWM Homepage [FAQ](http://fvwm.org/documentation/faq/).
5.  [FVWM Wiki](http://fvwmwiki.xteddy.org/).
6.  [FVWM Forums](http://www.fvwmforums.org).
7.  [Configurations](http://www.fvwmforums.org/phpBB3/viewforum.php?f=39&sid=468469f95f9a2a90cd9d5a0819d26eec) in the FVWM forum.
8.  [Box-Look](http://www.box-look.org/).
9.  Thomas Adam on [common mistakes in configuration files](http://www.fvwmforums.org/phpBB3/viewtopic.php?f=40&t=1505).
10.  [Fvwm Patches](http://web.archive.org/web/20070912061152/abdn.ac.uk/~u15dm4/fvwm/) in the [Internet Archive](http://archive.org/).
11.  [An example of a Fvwm module written in Perl](http://petermblair.com/2009/02/my-first-fvwm-module/)