[Humble Bundle](https://humblebundle.com) is a digital distributor of commercial video games, that stocks many titles with Linux support.

## Contents

*   [1 Purchase](#Purchase)
*   [2 Installation](#Installation)
    *   [2.1 Using AUR packages](#Using_AUR_packages)
        *   [2.1.1 Providing the game archive](#Providing_the_game_archive)
    *   [2.2 Manual installation](#Manual_installation)

## Purchase

There are two purchasing methods:

*   *Humble Indie Bundles* – time-limited promotions where a collection of games can be bought at a price determined by the purchaser.
*   *Humble Store* – traditional (fixed-price, single-game) purchases, usually via a widget on the game developer's website.

Both give you the exact same versions of the games, and in both cases the game ends up in your personal game library on the Humble Bundle website, from where you can download it.

## Installation

Many of the games offered on the platform have Linux versions, often provided in the form of a `.deb` package for Debian/Ubuntu, and a `.tar.gz` archive or `.sh` self-extracting archive for "generic" Linux distributions.

In some cases, you can just extract the `.tar.gz` or `.sh` somewhere on your Arch Linux system and run the game executable in the extracted folder. But in many other cases, additional installation steps are required to make the game run error-free.

### Using AUR packages

[AUR](/index.php/AUR "AUR") packages for Humble Bundle games take care of all the steps required to make each game run on Arch Linux.

These AUR package typically include the suffix `-hib` in their name.

#### Providing the game archive

Of course you have to provide your purchased game archive to the AUR package, so that it can install it. There are a few ways to achieve this:

*   **Manually copy/symlink the archive:**

	Manually download the game archive from your Humble Bundle library. Then copy or symlink the game archive to the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") folder. (You can look at the `source` array in the PKGBUILD to see which exact archive file it expects.

*   **Register a download agent:**

	Most AUR packages for Humble Bundle games helpfully mark the game archive using the custom `hib://` URI protocol. You can specify a handler for this protocol in the configuration file `/etc/makepkg.conf`, by adding a line to the `DLAGENTS` array right at the top of the file. You only need to do this once. The process for placing game archives into PKGBUILD directories will then be automated.

*   ***DLAGENT that finds the manually downloaded archive:***

	If you use the following DLAGENT, you can simply download your Humble Bundle archives to somewhere in your `~/downloads`, and AUR packages will automatically find and symlink it:

	 `'hib::/usr/bin/sh -c find\ \$HOME/Downloads\ -name\ \$(basename\ %u)\ -exec\ ln\ -s\ \\\{\\\}\ %o\ \\\;\ -quit'` 

*   ***DLAGENT that automatically downloads the archive:***

	If you have the [hib-dlagent](https://aur.archlinux.org/packages/hib-dlagent/) program installed, you can use the following DLAGENT to have it automatically download the game archive from your Humble Bundle library on demand:

	 `'hib::/usr/bin/hib-dlagent -u USER-EMAIL -o %o %u'` 

	It will ask you for your password each time. If complete automation is desired, you can hard-code the password using the `-p` parameter, but for security reason you probably shouldn't do this in the global `/etc/makepkg.conf` which all user accounts can read, but rather create the file `~/.makepkg.conf` and add it there as such:

	 `DLAGENTS+=('hib::/usr/bin/hib-dlagent -u USER-EMAIL -p PASSWORD -o %o %u')` 

### Manual installation

Manually getting a Humble Bundle game to run on Arch Linux, after extracting it, typically involves:

*   **Installing dependencies**:

	The games tend to assume that all dependencies which are part of a standard Ubuntu system, are installed.

	Remember that if the game only has a 32bit binary, you have to install the `lib32-` versions of all dependencies on a 64bit system.

*   **Removing bundled libraries that cause problems**:

	Some dependencies *are* bundled with the games, usually in a subfolder called `lib` or `lib32` or `lib64`. Unfortunately, some of these cause problems on Arch Linux, in which case you'll have to delete the troublemakers from that subfolder, so that the game will use the version of the library from `/usr/lib*`) instead. (Of course you'll then have to install the Arch Linux package which provides the library.)

If you're unsure, ask on the [forum](https://bbs.archlinux.org/viewforum.php?id=32) for help.