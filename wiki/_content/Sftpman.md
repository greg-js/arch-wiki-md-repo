# Sftpman

You can use sftpman (an [sshfs](/index.php/Sshfs "Sshfs") helper) to mount a remote system - accessible via [SSH](/index.php/SSH "SSH") - to a local folder.

sftpman offers both a command-line tool (_sftpman_) and a GTK frontend (_sftpman-gtk_, see [screenshot](https://github.com/spantaleev/sftpman-gtk/raw/master/sftpman-gui.png)), each packaged separately.

With sftpman, you first setup (define) your remote filesystems and then you mount/unmount them easily (with one click/command).

## Contents

*   [1 Prerequisite](#Prerequisite)
*   [2 Installation](#Installation)
*   [3 Defining filesystems](#Defining_filesystems)
    *   [3.1 Mounting/Unmounting](#Mounting.2FUnmounting)
    *   [3.2 Removing defined filesystems](#Removing_defined_filesystems)
    *   [3.3 Learning more](#Learning_more)
    *   [3.4 Troubleshooting](#Troubleshooting)
*   [4 Other Resources](#Other_Resources)
*   [5 See also](#See_also)

## Prerequisite

In order to use _sftpman_ or it's GTK frontend _sftpman-gtk_, you'll first need to have a working [sshfs](/index.php/Sshfs "Sshfs") setup.

[sshfs](/index.php/Sshfs "Sshfs") and fuse are installed as dependencies, so you may just need to add _fuse_ to your module-list in `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` to auto-load at boot.

## Installation

The [sftpman](https://aur.archlinux.org/packages/sftpman/)<sup><small>AUR</small></sup> and [sftpman-gtk](https://aur.archlinux.org/packages/sftpman-gtk/)<sup><small>AUR</small></sup> packages are available in the [AUR](/index.php/AUR "AUR").

_sftpman_ provides the base library and the command-line application _sftpman_.

_sftpman-gtk_ provides the _sftpman-gtk_ application, a GTK frontend to _sftpman_.

## Defining filesystems

Each filesystem managed by sftpman needs to have a unique name/id which will be used when managing the system and also in its mount path. A system with an id of _my-machine_ will be mounted locally to _/mnt/sshfs/my-machine_.

Authentication with the remote filesystem during mounting can be performed using passwords or [SSH keys](/index.php/SSH_keys "SSH keys").

To define a new remote filesystem with password-based authentication using the command-line tool, do:

```
# sftpman setup --id "my-machine" --host "HOSTNAME_OR_IP" --user "USERNAME" \
--mount_point "/REMOTE_PATH" --auth_method=password

```

Or the equivalent in case you want to use authentication with SSH Keys (recommended):

```
# sftpman setup --id "my-machine" --host "HOSTNAME_OR_IP" --user "USERNAME" \
--mount_point "/REMOTE_PATH" --auth_method=publickey --ssh_key "PATH_TO_PRIVATE_KEY"

```

The above setup is the minimum you need to specify to define a new filesystem that sftpman can mount. Depending on your environment, you may need to use some more options (like _--port_, which defaults to 22). To see a full list of available options do:

```
# sftpman help

```

You can also use the GTK frontend to define new filesystems more easily.

### Mounting/Unmounting

Once you've defined several filesystems, you can mount them by using their ids.

To mount:

```
# sftpman mount my-machine

```

which mounts the filesystem to _/mnt/sshfs/my-machine_

To unmount:

```
# sftpman unmount my-machine

```

**Note:** In order for the GUI application to be able to ask you for a password when mounting, you'll need to install some form of an ssh askpass tool. See: [SSH keys#Using ssh-agent and x11-ssh-askpass](/index.php/SSH_keys#Using_ssh-agent_and_x11-ssh-askpass "SSH keys")

### Removing defined filesystems

To remove a defined filesystem from sftpman's list do:

```
# sftpman rm machine-id

```

### Learning more

To see a list of more commands and options that _sftpman_ supports, consult the help:

```
# sftpman help

```

### Troubleshooting

_sftpman_ can perform some basic checks on the environment, which may catch some potential problems:

```
# sftpman preflight_check

```

If the GUI application does not ask you for a password while mounting (when using password-based authentication or for password-protected ssh keys), you will need to install an ssh askpass tool, see [#Mounting/Unmounting](#Mounting.2FUnmounting).

**Note:** If mounting a filesystem fails, sftpman will give you the full _sshfs_ command and its output. You can then use that command and run it manually (possibly after adding some more debug options to it, so you would see some more output).

When doing authentication using keys, start small and make sure SSHing actually works by trying it manually, before trying to use sshfs. Some common problems can be solved by consulting [Using SSH Keys#Troubleshooting](/index.php/Using_SSH_Keys#Troubleshooting "Using SSH Keys").

Also see [Sshfs#Troubleshooting](/index.php/Sshfs#Troubleshooting "Sshfs").

## Other Resources

[sftpman](https://github.com/spantaleev/sftpman) - sftpman (source code, issue tracker) at github

[sftpman-gtk](https://github.com/spantaleev/sftpman-gtk) - sftpman-gtk (source code, issue tracker) at github

[PKGBUILDs](https://github.com/spantaleev/PKGBUILDs) - Package files (source code, issue tracker) for _sftpman_ and _sftpman-gtk_ at github

## See also

*   [SSH](/index.php/SSH "SSH")
*   [sshfs](/index.php/Sshfs "Sshfs")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sftpman&oldid=377038](https://wiki.archlinux.org/index.php?title=Sftpman&oldid=377038)"