# Libetc

**Note:** libetc is unmaintained upstream. You can use rewritefs instead.

This is for those who are tired of having a messy $HOME folder cluttered with loads of dotfiles/dotfolders.

libetc is a LD_PRELOAD-able shared library that intercepts file operations: if a program tries to open a dotfile in $HOME, it is redirected to $XDG_CONFIG_HOME, [as defined by freedesktop](http://standards.freedesktop.org/basedir-spec/basedir-spec-0.6.html).

When an application tries to acces $HOME/.foobar, the call is redirected to XDG_CONFIG_HOME/foobar

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Exceptions](#Exceptions)
*   [4 Homepage](#Homepage)

## Installation

[libetc](https://aur.archlinux.org/packages/libetc/)<sup><small>AUR</small></sup> is available in the [AUR](/index.php/AUR "AUR"), so use your favorite method to install it.

## Configuration

_I use bash, but this should work for other shells too._

Open ~/.bashrc and add :

```
export XDG_CONFIG_HOME=/anywhere/you/want 
export LD_PRELOAD=libetc.so.0
export LIBETC_BLACKLIST=/bin/cp:/bin/ln:/bin/ls:/bin/mv:/bin/rm:/usr/bin/find

```

XDG_CONFIG_HOME defaults to ~/.config if unset. Applications in LIBETC_BLACKLIST will access dotfiles the regular way.

At that point, you might want to have every dotfile/dotfolder that was previously in your $HOME in $XDG_CONFIG_HOME and strip out the dot in their name. If you don't, new files will be created in $XDG_CONFIG_HOME and/or "File not found" errors will appear. Read "Exceptions" below.

Then source your .bashrc :

```
source ~/.bashrc

```

## Exceptions

Those files need to be in your $HOME, but you can link them into $XDG_CONFIG_HOME if you need to.

*   .bashrc
*   .bash_history
*   .bash_profile

(feel free to add more if you find some)

## Homepage

Be sure to read the README there : [http://ordiluc.net/fs/libetc](http://ordiluc.net/fs/libetc)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Libetc&oldid=375772](https://wiki.archlinux.org/index.php?title=Libetc&oldid=375772)"