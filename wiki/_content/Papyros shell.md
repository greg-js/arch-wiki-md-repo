# Papyros shell

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Window manager](/index.php/Window_manager "Window manager")

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** Other distributions don't get a separate page on the Arch wiki. This page should be dedicated strictly to the desktop shell component. (Discuss in [Talk:Papyros shell#](https://wiki.archlinux.org/index.php/Talk:Papyros_shell))

**Papyros** is a desktop environment based on Google's Material Design guidelines, created in 2014\. The operating system, desktop shell, and material design framework is still in active development and is in a pre-alpha state.

## Installation

You can install Papyros shell using the [AUR](/index.php/AUR "AUR") package [papyros-shell](https://aur.archlinux.org/packages/papyros-shell/)<sup><small>AUR</small></sup> or [papyros-shell-git](https://aur.archlinux.org/packages/papyros-shell-git/)<sup><small>AUR</small></sup>.

Otherwise you can follow these instructions:

Add the following lines to your `/etc/pacman.conf` file, above the default repositories:

 `/etc/pacman.conf` 

```
[papyros]
SigLevel = Never
Server = [http://dash.papyros.io/repos/$repo/$arch](http://dash.papyros.io/repos/$repo/$arch)
```

Then run:

```
sudo pacman -Syu
sudo pacman -S papyros-shell

```

You can finally run the shell by:

```
papyros-session

```

## Other applications

For additional functionality, you may wish to install the following:

*   **liri-browser** — A Web Browser using the QML Material framework from the Papyros Project.

[https://github.com/liri-browser/liri-browser](https://github.com/liri-browser/liri-browser) || [liri-browser](https://aur.archlinux.org/packages/liri-browser/)<sup><small>AUR</small></sup>

*   **liri-player** — A Web player using the QML Material framework from the Papyros Project.

[https://github.com/pierremtb/liri-player](https://github.com/pierremtb/liri-player) || [liri-player-git](https://aur.archlinux.org/packages/liri-player-git/)<sup><small>AUR</small></sup>

*   **papyros-files** — The file manager for Papyros.

[https://github.com/papyros/files-app](https://github.com/papyros/files-app) || [papyros-files](https://aur.archlinux.org/packages/papyros-files/)<sup><small>AUR</small></sup>

*   **papyros-settings** — The file settings for Papyros.

[https://github.com/papyros/settings-app](https://github.com/papyros/settings-app) || [papyros-settings-git](https://aur.archlinux.org/packages/papyros-settings-git/)<sup><small>AUR</small></sup>

## See also

*   [Official homepage](http://papyros.io)
*   [Papyros development](https://github.com/papyros)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Papyros_shell&oldid=414364](https://wiki.archlinux.org/index.php?title=Papyros_shell&oldid=414364)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments")