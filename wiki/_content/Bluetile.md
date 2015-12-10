# Bluetile

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Bluetile is a tiling window manager designed to integrate with the [GNOME](/index.php/GNOME "GNOME") [desktop environment](/index.php/Desktop_environment "Desktop environment"). Why choose Bluetile? Because none of the other tiling [window managers](/index.php/Window_managers "Window managers") were built with the thought in mind that time is the most limited resource among the majority of users. It is good if you can configure a software in every respect. It is better if you do not have to.

The Bluetile project is really just another [xmonad](/index.php/Xmonad "Xmonad") configuration. A configuration that focuses on making the tiling paradigm easily accessible to users coming from traditional window managers.

You can create pretty much the same effect with a standard xmonad installation, but this project exists to provide an easy installation path with zero configuration and without having to read (as much) background information.

## Contents

*   [1 Installation](#Installation)
*   [2 Running Bluetile](#Running_Bluetile)
    *   [2.1 At start-up](#At_start-up)
    *   [2.2 Another approach](#Another_approach)
*   [3 Known issues](#Known_issues)
    *   [3.1 X11-1.4.6.1](#X11-1.4.6.1)
*   [4 See also](#See_also)

## Installation

1\. [Install](/index.php/Pacman "Pacman") the following packages from the [official repositories](/index.php/Official_repositories "Official repositories"): [ghc](https://www.archlinux.org/packages/?name=ghc) [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) [gtk2hs-buildtools](https://www.archlinux.org/packages/?name=gtk2hs-buildtools) [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib).

2\. Update cabal:

```
# cabal update

```

3\. Install bluetile:

```
# cabal install bluetile

```

**Note:** See [Known issues](#Known_issues) section if you get any compile errors.

## Running Bluetile

After you have installed Bluetile, test it:

```
$ ~/.cabal/bin/bluetile

```

### At start-up

If you wish to have bluetile launch automatically after logging in, you must set the correct PATH evironment label and then add _bluetile_ to your start-up applications.

1\. Edit `~/.bashrc` and add the following line to the end:

```
export PATH=~/.cabal/bin:$PATH

```

2\. Next launch `gnome-session-properties`:

```
$ gnome-session-properties

```

3\. You will be presented with a list of your start-up applcations.

```
Click: "Add"
In the name field enter: Bluetile Window Manager
In the command field enter: bluetile
The comment field is optional.

```

Thats it, happy tiling!

### Another approach

You can also edit `~/.gnomerc` and set the `WINDOW_MANAGER` variable with:

```
export WINDOW_MANAGER=/home/user/.cabal/bin/bluetile

```

With this, [GNOME](/index.php/GNOME "GNOME") will automatically use Bluetile instead of Metacity.

**Note:** With this method there is no need to add bluetile to your `gnome-session-properties`.

## Known issues

### X11-1.4.6.1

If you see an error that looks like this:

```
hsc2hs: Graphics/X11/Xlib/Extras.hsc: hGetContents: invalid argument (Invalid 
or incomplete multibyte or wide character) 
cabal: Error: some packages failed to install: 
X11-1.4.6.1 failed during the building phase. The exception was: 
ExitFailure 1 

```

Follow this procedure to fix this problem:

```
# pacman -S libticonv
$ cd ~/.cabal/packages/hackage.haskell.org/X11/1.4.6.1/
$ tar xzf X11-1.4.6.1.tar.gz && cd X11-1.4.6.1/Graphics/X11/Xlib
$ <Extras.hsc iconv -f ISO-8859-1 -t UTF8 >fix
$ mv fix Extras.hsc
$ cd ../../../
# cabal install

```

Once that is finished:

```
# cabal install bluetile

```

## See also

[http://bluetile.org/](http://bluetile.org/) - Project home page

[http://www.haskell.org/haskellwiki/Bluetile](http://www.haskell.org/haskellwiki/Bluetile) - Wiki

Retrieved from "[https://wiki.archlinux.org/index.php?title=Bluetile&oldid=375977](https://wiki.archlinux.org/index.php?title=Bluetile&oldid=375977)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Tiling WMs](/index.php/Category:Tiling_WMs "Category:Tiling WMs")