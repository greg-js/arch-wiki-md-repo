# Papyros shell

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

NaN

*   **liri-player** — A Web player using the QML Material framework from the Papyros Project.

NaN

*   **papyros-files** — The file manager for Papyros.

NaN

*   **papyros-settings** — The file settings for Papyros.

NaN

## See also

*   [Official homepage](http://papyros.io)
*   [Papyros development](https://github.com/papyros)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Papyros_shell&oldid=418353](https://wiki.archlinux.org/index.php?title=Papyros_shell&oldid=418353)"