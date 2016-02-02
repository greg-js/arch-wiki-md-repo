# Papyros shell

**Papyros** is a desktop environment based on Google's Material Design guidelines, created in 2014\. The operating system, desktop shell, and material design framework is still in active development and is in a pre-alpha state.

## Installation

You can install Papyros shell using the [AUR](/index.php/AUR "AUR") package [papyros-shell](https://aur.archlinux.org/packages/papyros-shell/) or [papyros-shell-git](https://aur.archlinux.org/packages/papyros-shell-git/).

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

	[https://github.com/liri-browser/liri-browser](https://github.com/liri-browser/liri-browser) || [liri-browser](https://aur.archlinux.org/packages/liri-browser/)

*   **liri-player** — A Web player using the QML Material framework from the Papyros Project.

	[https://github.com/pierremtb/liri-player](https://github.com/pierremtb/liri-player) || [liri-player-git](https://aur.archlinux.org/packages/liri-player-git/)

*   **papyros-files** — The file manager for Papyros.

	[https://github.com/papyros/files-app](https://github.com/papyros/files-app) || [papyros-files](https://www.archlinux.org/packages/?name=papyros-files)

*   **papyros-settings** — The file settings for Papyros.

	[https://github.com/papyros/settings-app](https://github.com/papyros/settings-app) || [papyros-settings-git](https://aur.archlinux.org/packages/papyros-settings-git/)

## See also

*   [Official homepage](http://papyros.io)
*   [Papyros development](https://github.com/papyros)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Papyros_shell&oldid=418353](https://wiki.archlinux.org/index.php?title=Papyros_shell&oldid=418353)"