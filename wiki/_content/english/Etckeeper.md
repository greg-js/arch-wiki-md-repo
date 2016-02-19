[Etckeeper](http://etckeeper.branchable.com/) lets you keep `/etc` under version control.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 systemd](#systemd)
    *   [3.2 Cron](#Cron)
    *   [3.3 Incron](#Incron)
    *   [3.4 Automatic push to remote repo](#Automatic_push_to_remote_repo)
    *   [3.5 Wrapper script](#Wrapper_script)

## Installation

[Install](/index.php/Install "Install") the [etckeeper](https://www.archlinux.org/packages/?name=etckeeper) package.

## Configuration

The preferred version control system (default is [git](/index.php/Git "Git")) and other options are to be configured in `/etc/etckeeper/etckeeper.conf`.

Etckeeper supports using [pacman](/index.php/Pacman "Pacman") as a `LOWLEVEL_PACKAGE_MANAGER` and `HIGHLEVEL_PACKAGER_MANAGER` in `etckeeper.conf`.

## Usage

After configuration the repository for the `/etc` path has to be initialized:

```
# etckeeper init

```

As of *etckeeper* version 1.18.3-1, pre-install and post-install [pacman hooks](/index.php/Pacman#Hooks "Pacman") are executed automatically on package installation, update and removal. A manual [#Wrapper script](#Wrapper_script) is not required anymore.

To track other changes to the `/etc` path, you need to either commit changes manually (see the etckeeper(8) man page for commands) or use one of the stopgap solutions below.

### systemd

Service and timer units are included in the package. Simply [enable](/index.php/Systemd/Timers#Management "Systemd/Timers") `etckeeper.timer`.

See [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers") for more information and [Systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd") if you wish to edit the provided units.

### Cron

There is a cron script in the source distribution at `debian/cron.daily`. You can use this script to automatically commit changes on a schedule. To make it run daily, for example, make sure you have cron installed and enabled, then simply copy the script from the srcdir where you built etckeeper to `/etc/cron.daily` and make sure it is executable (e.g. `chmod +x /path/to/script`).

### Incron

As an alternative to the above, you could set up incron to automatically commit changes using etckeeper whenever a file in `/etc` is modified.

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

### Wrapper script

If you want to track changes of a frequently executed command (e.g. `*command*`), a simple wrapper script can help to automate it. For example, create:

 `/usr/local/bin/checketc.sh` 
```
#!/bin/bash

etckeeper pre-install
*command*
etckeeper post-install
```

and make it executable. Alternatively, you may call the Etckeeper commands via a bash alias or function, see [Bash#Aliases](/index.php/Bash#Aliases "Bash") for more information.

**Note:** Before Etckeeper version 1.18.3-1 such manual wrapper script was required for Pacman integration. Now the Pacman hooks perform the commands automatically.