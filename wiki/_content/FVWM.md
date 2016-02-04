# FVWM

FVWM is a stable, powerful, efficient, and ICCCM-compliant multiple virtual desktop window manager for the X Window system. It requires some effort to learn to use it well, since it is almost entirely configured by editing configuration files with a text editor, but those who persist end up with a desktop environment that works exactly the way they want it to work. Although using FVWM does not require any knowlege of programming languages, it is possible to extend the power of FVWM with [M4](http://www.fvwm.org/documentation/manpages/stable/FvwmM4.php), [C](http://www.fvwm.org/documentation/manpages/stable/FvwmCpp.php), and [Perl](http://www.fvwm.org/documentation/manpages/stable/FvwmPerl.php) preprocessing. FVWM has a [Perl library](http://www.fvwm.org/documentation/perllib/) that makes creating FVWM modules in Perl possible and easy. Development is active, and support is excellent. And for those who wonder, FVWM means Feeble Virtual Window Manager.

## Contents

*   [1 Installing FVWM](#Installing_FVWM)
*   [2 Starting FVWM](#Starting_FVWM)
*   [3 Bringing Out its Power](#Bringing_Out_its_Power)
*   [4 References](#References)

## Installing FVWM

[Install](/index.php/Install "Install") the package [fvwm](https://www.archlinux.org/packages/?name=fvwm).

You can also install [fvwm-patched](https://aur.archlinux.org/packages/fvwm-patched/), or if you have archlinuxfr (see [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories")) added to your `/etc/pacman.conf` it can be installed with [pacman](/index.php/Pacman "Pacman") like a regular package.

## Starting FVWM

Select _FVWM_ from the session menu in a [display manager](/index.php/Display_manager "Display manager") of choice. Otherwise, add

```
exec fvwm

```

to your user's `.xinitrc`.

See [xinitrc](/index.php/Xinitrc "Xinitrc") for details, such as preserving the logind session.

## Bringing Out its Power

When you start FVWM for the first time, you will get something that looks very blank. When you left-click on the desktop, you will be able to select a very basic configuration for FVWM. Choose the modules you want and you are ready to get started. You will undoubtedly want to do more to create your desktop, so here are some tips:

*   Although it is outdated, the Zensites FVWM beginners guide[[1]](http://zensites.net/fvwm/guide/) helps to understand how FVWM functions and how to build **your** basic setup.

*   The Gentoo Linux Wiki has a useful guide on configuration.[[2]](https://web.archive.org/web/20130204050827/http://en.gentoo-wiki.com/wiki/FVWM/Configuration)

*   The FVWM homepage[[3]](http://fvwm.org/) includes documentation[[4]](http://fvwm.org/documentation/), a FAQ [[5]](http://fvwm.org/documentation/faq/), and links to a Wiki[[6]](https://web.archive.org/web/20140107042718/http://fvwmwiki.xteddy.org/)) and the FVWM forums[[7]](http://www.fvwmforums.org).

*   The best way to come up with the desktop you want is probably to check out the configurations in the FVWM forum[[8]](http://www.fvwmforums.org/phpBB3/viewforum.php?f=39) or at Box-Look.org,[[9]](http://www.box-look.org) choose one you like, install it, and modify it to taste.

*   As you work with what other people have done, you may find it helpful to look at the tips on configuration files by Thomas Adam, the most active FVWM developer.[[10]](http://www.fvwmforums.org/phpBB3/viewtopic.php?f=40&t=1505)

*   A page[[11]](http://web.archive.org/web/20070912061152/abdn.ac.uk/~u15dm4/fvwm/) in the [Internet Archive](http://archive.org/) is outdated, but seems to be the only significant online documentation for fvwm-patched.

*   FVWM-Crystal, which is also in the Arch repositories as package [fvwm-crystal](https://www.archlinux.org/packages/?name=fvwm-crystal), is an add-on that makes FVWM much easier to configure, although the easier configuration allows much less flexibility than direct editing of configuration files.

*   [XdgMenu](/index.php/XdgMenu "XdgMenu") is a useful utility for generating menus.

*   Fvwm plays well with [xcompmgr](/index.php/Xcompmgr "Xcompmgr") for simple compositing effects.

*   Useful applications are similar to those suggested for [Openbox](/index.php/Openbox "Openbox") or [Fluxbox](/index.php/Fluxbox "Fluxbox").

## References

1.  Zensites [FVWM beginners guide](http://zensites.net/fvwm/guide/).
2.  [FVWM Homepage](http://fvwm.org/).
3.  FVWM Homepage [documentation](http://fvwm.org/documentation/).
4.  FVWM Homepage [FAQ](http://fvwm.org/documentation/faq/).
5.  [FVWM Wiki](http://fvwmwiki.xteddy.org/).
6.  [FVWM Forums](http://www.fvwmforums.org).
7.  [Gentoo wiki about Fvwm](http://wiki.gentoo.org/wiki/FVWM).
8.  [Debian wiki about Fvwm](https://wiki.debian.org/Fvwm).
9.  [Ubuntu wiki about Fvwm](https://help.ubuntu.com/community/FVWM).
10.  [Configurations](http://www.fvwmforums.org/phpBB3/viewforum.php?f=39&sid=468469f95f9a2a90cd9d5a0819d26eec) in the FVWM forum.
11.  [Box-Look](http://www.box-look.org/).
12.  Thomas Adam on [common mistakes in configuration files](http://www.fvwmforums.org/phpBB3/viewtopic.php?f=40&t=1505).
13.  [Fvwm Patches](http://web.archive.org/web/20070912061152/abdn.ac.uk/~u15dm4/fvwm/) in the [Internet Archive](http://archive.org/).
14.  [An example of a Fvwm module written in Perl](http://petermblair.com/2009/02/my-first-fvwm-module/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=FVWM&oldid=413756](https://wiki.archlinux.org/index.php?title=FVWM&oldid=413756)"