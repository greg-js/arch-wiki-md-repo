[Mercurial](https://www.mercurial-scm.org/) (commonly referred to as **hg**) is a distributed version control system written in Python and is similar in many ways to [Git](/index.php/Git "Git"), [Bazaar](http://bazaar.canonical.com/) and [Darcs](/index.php/Darcs "Darcs").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Graphical front-ends](#Graphical_front-ends)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Dotfiles Repo](#Dotfiles_Repo)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [mercurial](https://www.archlinux.org/packages/?name=mercurial), available in the [Official repositories](/index.php/Official_repositories "Official repositories"). For the development version, install [mercurial-hg](https://aur.archlinux.org/packages/mercurial-hg/).

### Graphical front-ends

See also [Mercurial graphical user interfaces](https://www.mercurial-scm.org/wiki/OtherTools#Graphical_user_interfaces).

*   **EasyMercurial** — Simple user interface for the Mercurial distributed version control system.

	[https://easyhg.org/](https://easyhg.org/) || [easyhg](https://aur.archlinux.org/packages/easyhg/)

*   **hgk** — Tcl/Tk based tool to browse the history of a repository in a graphical way.

	[https://www.mercurial-scm.org/wiki/HgkExtension](https://www.mercurial-scm.org/wiki/HgkExtension) || [mercurial](https://www.archlinux.org/packages/?name=mercurial) + [tk](https://www.archlinux.org/packages/?name=tk)

*   **hgtui** — Textual user interface frontend for DSCM mercurial.

	[https://bitbucket.org/hgtui/hgtui](https://bitbucket.org/hgtui/hgtui) || [hgtui-hg](https://aur.archlinux.org/packages/hgtui-hg/)

*   **hgview** — Qt4 and text based Mercurial log navigator.

	[https://www.logilab.org/project/hgview/](https://www.logilab.org/project/hgview/) || [hgview](https://aur.archlinux.org/packages/hgview/)

*   **[TortoiseHg](https://en.wikipedia.org/wiki/TortoiseHg "wikipedia:TortoiseHg")** — Set of graphical tools and a Nautilus extension for the Mercurial distributed revision control system.

	[https://tortoisehg.bitbucket.io/](https://tortoisehg.bitbucket.io/) || [tortoisehg](https://aur.archlinux.org/packages/tortoisehg/)

## Configuration

At the minimum you should configure your username or mercurial will most likely give you an error when trying to commit. Do this by editing `~/.hgrc` and adding the following:

 `~/.hgrc` 
```
[ui]
username = John Smith <johnsmith@domain.tld>
```

To use the graphical browser **hgk** aka. **hg view**, add the following to `~/.hgrc` (see [forum thread](https://bbs.archlinux.org/viewtopic.php?id=31999)):

 `~/.hgrc` 
```
[extensions]
hgk=
```

You will need to install [tk](https://www.archlinux.org/packages/?name=tk) before running **hg view** to avoid the rather cryptic error message:

```
/usr/bin/env: wish: No such file or directory

```

To remove Mercurial warnings of unverified certificate fingerprints, add the following to `~/.hgrc` (see [Mercurial wiki](http://mercurial.selenic.com/wiki/CACertificates)):

 `~/.hgrc` 
```
[web]
cacerts = /etc/ssl/certs/ca-certificates.crt
```

If you are going to be working with large repositories, you may want to enable the *progress* extension by adding it to your `~/.hgrc` file:

 `~/.hgrc` 
```
[extensions]
progress =
```

This will show progress bars on longer operations after 3 seconds. If you would like the progress bar to show sooner, you can append the following to your configuration file:

 `~/.hgrc` 
```
[progress]
delay = 1.5
```

## Usage

All mercurial commands are initiated with the *hg* prefix. To see a list of some of the common commands, run

```
$ hg help

```

You can either work with a pre-existing repository (collection of code or files), or create your own to share.

To work with a pre-existing repository, you must clone it to a directory of your choice:

```
$ mkdir mercurial
$ cd mercurial
$ hg clone [http://hg.serpentine.com/tutorial/](http://hg.serpentine.com/tutorial/)

```

To create you own, change to the directory you wish to share and initiate a mercurial project

```
$ cd myfiles
$ hg init myfiles

```

### Dotfiles Repo

If you intend on creating a repo of all your `~/.` files, you simply initiate the project in your home folder:

```
$ hg init

```

It is then just a case of adding the specific files you wish to track:

```
$ hg add |file1 file2 file3

```

You can then create a `~/.hgignore` to ensure that only the files you wish to include in the repository are tracked by mercurial.

**Tip:** If you include: syntax: glob at the top of the `.hgignore` file, you can easily exclude groups of files from your repository.

## See also

*   [Mercurial: The Definitive Guide](http://hgbook.red-bean.com/read/)
*   [hginit.com](http://hginit.com/) - a tutorial by Joel Spolsky
*   [Mercurial Kick-Start](http://mercurial.aragost.com/kick-start/en/) one more tutorial by Aragost.
*   [Bitbucket](http://bitbucket.org) - free and commercial hosting of Mercurial repositories (all Mercurial repositories [will be removed](https://bitbucket.org/blog/sunsetting-mercurial-support-in-bitbucket) on 2020-06-01)