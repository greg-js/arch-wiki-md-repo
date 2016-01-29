# Etckeeper

Etckeeper lets you keep `/etc` under version control.

## Contents

*   [1 Install](#Install)
*   [2 Configure](#Configure)
*   [3 Usage](#Usage)
    *   [3.1 systemd](#systemd)
    *   [3.2 Cron](#Cron)
    *   [3.3 Wrapper script](#Wrapper_script)
    *   [3.4 Incron](#Incron)
    *   [3.5 Automatic push to remote repo](#Automatic_push_to_remote_repo)

## Install

Etckeeper can be [installed](/index.php/Pacman "Pacman") with the [etckeeper](https://www.archlinux.org/packages/?name=etckeeper) package, available in the [official repositories](/index.php/Official_repositories "Official repositories").

## Configure

The main config file is `/etc/etckeeper/etckeeper.conf`. You can set things such as the VCS to use in this file.

Once you've set your preferred VCS (the default is git), you can initialize the /etc repository by running

```
# etckeeper init

```

## Usage

Etckeeper supports using pacman as a `LOWLEVEL_PACKAGE_MANAGER` in `etckeeper.conf`. Support for using pacman as a `HIGHLEVEL_PACKAGER_MANAGER` is not possible since pacman does not have hook capability, so you'll need to either commit changes manually or use one of the stopgap solutions below.

### systemd

Service and timer units are included in the package. Simply [enable](/index.php/Systemd/Timers#Management "Systemd/Timers") `etckeeper.timer`.

See [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") for more informations and [Systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd") if you wish to edit the provided units.

### Cron

There is a cron script in the source distribution at `debian/cron.daily`. You can use this script to automatically commit changes on a schedule. To make it run daily, for example, make sure you have cron installed and enabled, then simply copy the script from the srcdir where you built etckeeper to `/etc/cron.daily` and make sure it's executable (e.g. `chmod +x /path/to/script`).

### Wrapper script

In order to emulate the auto-commit functionality that etckeeper has on other systems, you could place a script such as the one below somewhere in your PATH, make it executable, and use it instead of `pacman -Syu` to update your system.

```
#!/bin/bash

etckeeper pre-install
pacman -Syu
etckeeper post-install

```

Alternatively you can add a quick alias to `~/.bashrc`:

```
alias pkg-update='sudo etckeeper pre-install && sudo pacman -Syu && sudo etckeeper post-install'

```

or a function where it is possible to specify the arguments for pacman or pacman wrapper:

```
Pacman () { sudo etckeeper pre-install && sudo pacman  "$@" && sudo etckeeper post-install; }

```

To use the function, just run pacman as usual with flags as needed, but with a capital "P". For example:

```
Pacman -Syu
Pacman -R foo

```

**Warning:** Do not name your wrapper script "pacman" and rely on it appearing earlier in the PATH than `/usr/bin/pacman`. One of the etckeeper pre-install hooks calls pacman without specifying its path, so your script will be invoked recursively without end.

### Incron

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Please expand this section with instructions on how to set up incron or link to a write-up. (Discuss in [Talk:Etckeeper#](https://wiki.archlinux.org/index.php/Talk:Etckeeper))

As an alternative to the above, you could set up incron to automatically commit changes using etckeeper whenever a file in /etc is modified.

### Automatic push to remote repo

**Warning:** Pushing your etckeeper repository to a publicly accessible remote repository can expose sensitive data such as password hashes or private keys. Proceed with caution.

Whilst having a local backup in `/etc/.git` is a good first step, etckeeper can automatically push your changes on each commit to a remote repository such as Github. Create an executable file `/etc/etckeeper/commit.d/40github-push`:

```
#!/bin/sh
set -e

if [ "$VCS" = git ] && [ -d .git ]; then
  cd /etc/
  git push origin master
fi

```

Change to `etc/.git` and add your remote Github repository:

```
# git remote add origin [https://github.com/user/repo.git](https://github.com/user/repo.git)

```

Now each time you run your wrapper script or alias from above, changes will be automatically commited to your Github repo.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Etckeeper&oldid=411988](https://wiki.archlinux.org/index.php?title=Etckeeper&oldid=411988)"