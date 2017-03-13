This article provides ideas how to keep two systems (folders) in sync across devices. This is a challenging problem, especially if both devices are used concurrently and files may be in conflict.

## Contents

*   [1 Unison](#Unison)
    *   [1.1 Prerequisites](#Prerequisites)
    *   [1.2 Configuration example](#Configuration_example)
    *   [1.3 Limitations](#Limitations)
*   [2 rsync](#rsync)
*   [3 Syncthing](#Syncthing)
*   [4 Other](#Other)

## Unison

[Unison](http://www.cis.upenn.edu/~bcpierce/unison/). [Screenshot](http://caml.inria.fr/about/successes-images/unison.jpg).

Unision allows you to do a sync in both directions. The great feature of Unison is that it provides you with a GUI that can assist you in resolving conflicts when synchronizing files.

### Prerequisites

You need to have the same version of unison installed on both machines as well as SSH.

### Configuration example

Consider user Joe that has two systems, Alpha and Beta.

The example below shows you the following useful Unison configuration file instructions:

*   Define the two `root` folders to sync;
*   Using the `follow` instruction to follow symbolic links;
*   Including a `common` set of file ignores.

**~/.unison/alpha.prf**

```
root = /home/joe
root = ssh://beta//home/joe
follow = Path school
include common

```

**~/.unison/beta.prf**

```
root = /home/joe
root = ssh://alpha//home/hugo
follow = Path school
include common

```

**~/.unison/common**

```
ignore = Regex .*(cache|Cache|te?mp|history|thumbnails).*
ignore = Name sylpheed.log*
ignore = Name unison.log
ignore = Name .ICEauthority
ignore = Name .Xauthority

```

You can call unison from the command line, for example:

```
alias unisync="unison-gtk2 beta -contactquietly -logfile /dev/null"

```

### Limitations

You can also use this tool with NFS shares instead of SSH, but you may find that it is slower. The advantage of using SSH is that the local unison asks the remote unison process to check for updates, rather than trying to do it locally using NFS (which requires additional network traffic).

If you are using a ssh port different from the default (22), for example 1022, use this line in your prf file:

```
sshargs = -p 1022

```

If you are using symbolic links and want to synchronize your files on a vfat system (usb key for example), unison will not accept them and generate errors. As a solution, you can tell unison not to synchronize links (`links` option). However, if this is not an option for you, you can find them on your system with:

```
find ~/folder -type l

```

Unison is very sensitive and requires the **exact same versions** on [client and server](https://groups.yahoo.com/neo/groups/unison-users/conversations/topics/11439%7Cboth). Also, unison **must** be compiled against the same OCaml version on all peers too. Making it highly unfeasible for a heterogeneous network.

## rsync

See [rsync](/index.php/Rsync "Rsync").

## Syncthing

See [syncthing](/index.php/Syncthing "Syncthing").

## Other

Consider Dropbox, Owncloud or Nextcloud.