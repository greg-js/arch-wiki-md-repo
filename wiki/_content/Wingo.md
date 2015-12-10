# Wingo

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Wingo is a fully featured true hybrid window manager that supports per-monitor workspaces, and neither the floating or tiling modes are after thoughts. This allows one to have tiling on one workspace while floating on the other. Wingo can be scripted with its own command language, is completely themeable, and supports user defined hooks. Wingo is written in Go and has no runtime dependencies.

The development version can be installed from the [wingo-git](https://aur.archlinux.org/packages/wingo-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/wingo-git)]</sup> package.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Run Wingo](#Run_Wingo)
    *   [3.1 Without a login manager](#Without_a_login_manager)
    *   [3.2 With a login manager](#With_a_login_manager)
*   [4 See also](#See_also)

## Installation

Wingo can be [installed](/index.php/Installed "Installed") from the [wingo-git](https://aur.archlinux.org/packages/wingo-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/wingo-git)]</sup>.

## Configuration

After installing Wingo the configuration files needs to be created with the `wingo --write-config` command.

## Run Wingo

### Without a login manager

To run wingo without a login manager, simply add `exec wingo` to the startup script of your choice (e.g. ~/.xinitrc.)

See [xinitrc](/index.php/Xinitrc "Xinitrc") for details, such as preserving the logind session.

You can also start wingo as preferred user without even logging in. See [Start X at login](/index.php/Start_X_at_login "Start X at login").

### With a login manager

To start wingo from a login manager, see [this article](/index.php/Display_manager "Display manager").

## See also

*   [Wingo on Github](https://github.com/BurntSushi/wingo) – Project repository
*   [Screenshots](https://github.com/BurntSushi/wingo/wiki/Screenshots) – Screenshots
*   [Bug reports](https://github.com/BurntSushi/wingo/issues?state=open) – Report a bug

Retrieved from "[https://wiki.archlinux.org/index.php?title=Wingo&oldid=392825](https://wiki.archlinux.org/index.php?title=Wingo&oldid=392825)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Stacking WMs](/index.php/Category:Stacking_WMs "Category:Stacking WMs")
*   [Tiling WMs](/index.php/Category:Tiling_WMs "Category:Tiling WMs")
*   [Dynamic WMs](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs")