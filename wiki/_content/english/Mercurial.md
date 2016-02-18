[Mercurial](http://mercurial.selenic.com/) (commonly referred to as **hg**) is a distributed version control system written in Python and is similar in many ways to [Git](/index.php/Git "Git"), [Bazaar](http://bazaar.canonical.com/) and [Darcs](/index.php/Darcs "Darcs").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Dotfiles Repo](#Dotfiles_Repo)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [mercurial](https://www.archlinux.org/packages/?name=mercurial), available in the [Official repositories](/index.php/Official_repositories "Official repositories").

## Configuration

At the minimum you should configure your username or mercurial will most likely give you an error when trying to commit. Do this by editing `~/.hgrc` and adding the following:

 `~/.hgrc` 
```
[ui]
username = John Smith
```

To use the graphical browser **hgk** aka. **hg view**, add the following to `~/.hgrc` (see [forum thread](https://bbs.archlinux.org/viewtopic.php?id=31999)):

 `~/.hgrc` 
```
[extensions]
hgk=
```

You will need to install [tk](https://www.archlinux.org/packages/?name=tk) before running **hg view** to avoid the rather cryptic error message:

 `/usr/bin/env: wish: No such file or directory` 

To remove Mercurial warnings of unverified certificate fingerprints, add the following to `~/.hgrc` (see [Mercurial wiki](http://mercurial.selenic.com/wiki/CACertificates)):

 `~/.hgrc` 
```
[web]
cacerts = /etc/ssl/certs/ca-certificates.crt
```

If you are going to be working with large repositories (e.g. [ttf-google-fonts-hg](https://aur.archlinux.org/packages/ttf-google-fonts-hg/)), you may want to enable the *progress* extension by adding it to your `~/.hgrc` file:

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

 `$ hg help` 

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

 `$ hg init` 

It is then just a case of adding the specific files you wish to track:

 `$ hg add ` 

You can then create a `~/.hgignore` to ensure that only the files you wish to include in the repository are tracked by mercurial.

**Tip:** If you include: syntax: glob at the top of the `.hgignore` file, you can easily exclude groups of files from your repository.

## See also

*   [Mercurial: The Definitive Guide](http://hgbook.red-bean.com/read/)
*   [hginit.com](http://hginit.com/) - a tutorial by Joel Spolsky
*   [Mercurial Kick-Start](http://mercurial.aragost.com/kick-start/en/) one more tutorial by Aragost.
*   [Bitbucket](http://bitbucket.org) - free and commercial hosting of mercurial repositories
*   [Intuxication](http://mercurial.intuxication.org/) - free mercurial hosting