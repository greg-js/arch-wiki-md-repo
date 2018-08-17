Related articles

*   [SSH](/index.php/SSH "SSH")
*   [SSHFS](/index.php/SSHFS "SSHFS")

You can use sftpman (an [SSHFS](/index.php/SSHFS "SSHFS") helper) to mount a remote system - accessible via [SSH](/index.php/SSH "SSH") - to a local folder.

sftpman offers both a command-line tool (*sftpman*) and a GTK frontend (*sftpman-gtk*, see [screenshot](https://github.com/spantaleev/sftpman-gtk/raw/master/sftpman-gui.png)), each packaged separately.

With sftpman, you first setup (define) your remote filesystems and then you mount/unmount them easily (with one click/command).

## Contents

*   [1 Prerequisite](#Prerequisite)
*   [2 Installation](#Installation)
*   [3 Defining filesystems](#Defining_filesystems)
    *   [3.1 Mounting/Unmounting](#Mounting.2FUnmounting)
    *   [3.2 Removing defined filesystems](#Removing_defined_filesystems)
    *   [3.3 Learning more](#Learning_more)
*   [4 Troubleshooting](#Troubleshooting)

## Prerequisite

In order to use *sftpman* or it's GTK frontend *sftpman-gtk*, you'll first need to have a working [SSHFS](/index.php/SSHFS "SSHFS") setup.

## Installation

The [sftpman](https://aur.archlinux.org/packages/sftpman/) and [sftpman-gtk](https://aur.archlinux.org/packages/sftpman-gtk/) packages are available in the [AUR](/index.php/AUR "AUR").

*sftpman* provides the base library and the command-line application *sftpman*.

*sftpman-gtk* provides the *sftpman-gtk* application, a GTK frontend to *sftpman*.

## Defining filesystems

Each filesystem managed by sftpman needs to have a unique name/id which will be used when managing the system and also in its mount path. A system with an id of *my-machine* will be mounted locally to */mnt/sshfs/my-machine*.

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

The above setup is the minimum you need to specify to define a new filesystem that sftpman can mount. Depending on your environment, you may need to use some more options (like *--port*, which defaults to 22). To see a full list of available options do:

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

which mounts the filesystem to */mnt/sshfs/my-machine*

To unmount:

```
# sftpman unmount my-machine

```

**Note:** In order for the GUI application to be able to ask you for a password when mounting, you'll need to install some form of an ssh askpass tool. See [SSH keys#x11-ssh-askpass](/index.php/SSH_keys#x11-ssh-askpass "SSH keys").

### Removing defined filesystems

To remove a defined filesystem from sftpman's list do:

```
# sftpman rm machine-id

```

### Learning more

To see a list of more commands and options that *sftpman* supports, consult the help:

```
# sftpman help

```

## Troubleshooting

*sftpman* can perform some basic checks on the environment, which may catch some potential problems:

```
# sftpman preflight_check

```

If the GUI application does not ask you for a password while mounting (when using password-based authentication or for password-protected ssh keys), you will need to install an ssh askpass tool, see [#Mounting/Unmounting](#Mounting.2FUnmounting).

**Note:** If mounting a filesystem fails, sftpman will give you the full *sshfs* command and its output. You can then use that command and run it manually (possibly after adding some more debug options to it, so you would see some more output).

When doing authentication using keys, start small and make sure SSHing actually works by trying it manually, before trying to use sshfs. Some common problems can be solved by consulting [Using SSH Keys#Troubleshooting](/index.php/Using_SSH_Keys#Troubleshooting "Using SSH Keys").

Also see [SSHFS#Troubleshooting](/index.php/SSHFS#Troubleshooting "SSHFS").