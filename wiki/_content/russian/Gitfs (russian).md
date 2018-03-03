**Состояние перевода:** На этой странице представлен перевод статьи [Gitfs](/index.php/Gitfs "Gitfs"). Дата последней синхронизации: 21 августа 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Gitfs&diff=0&oldid=447200).

From [gitfs](https://www.presslabs.org/gitfs/docs/):

	gitfs is a FUSE file system that fully integrates with git. You can mount a remote repository’s branch locally, and any subsequent changes made to the files will be automatically committed to the remote.

	You can mount any repository, and all the changes you make will be automatically converted into commits. gitfs will also expose the history of the branch you’re currently working on by simulating snapshots of every commit.

	gitfs is useful in places where you want to keep track of all your files, but at the same time you don’t have the possibility of organizing everything into commits yourself. A FUSE file system for git repositories, with local cache.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Write access to /var/lib/gitfs](#Write_access_to_.2Fvar.2Flib.2Fgitfs)
    *   [3.2 Write access to pygit2](#Write_access_to_pygit2)
    *   [3.3 Options for use with ssh key](#Options_for_use_with_ssh_key)

## Installation

[Install](/index.php/Install "Install") [gitfs](https://aur.archlinux.org/packages/gitfs/).

## Usage

gitfs enables to mount a remote git repository as a [FUSE](/index.php/Fuse "Fuse") filesystem, for example:

```
$ gitfs http://your.repository.org/repository.git */mount/directory*

```

See its documentation for [options](https://www.presslabs.org/gitfs/docs/arguments/).

## Troubleshooting

### Write access to /var/lib/gitfs

`/var/lib/gitfs` needs to exist and is not automatically created. Also, if you want to mount gitfs as a regular user, make sure to make it writable for that user:

```
sudo mkdir /var/lib/gitfs
sudo chown username:users /var/lib/gitfs

```

### Write access to pygit2

On first run gitfs tries to do some self-introspection which fails, if you run it as a regular user. To remedy this, run it once as root. You do not need to actually mount anything. It is enough to show the help message as root:

```
sudo gitfs -h

```

### Options for use with ssh key

Gitfs (and pygit2 on which it relies) seems to be under heavy development and options change. Although [the official docs](https://www.presslabs.org/gitfs/docs/arguments/) state that the option `-o key=` can be used to change the key, it turns out that version 0.4.1-1 from AUR requires the use of `-o ssh_key=`. Note that gitfs will not ask for a passphrase, if the key is passphrase protected. It simply returns with the error:

```
_pygit2.GitError: Failed to authenticate SSH session: Callback returned error

```

It is recommended to create a separate key for this by issuing:

```
ssh-keygen
/home/user/.ssh/gitfs_rsa
<empty passphrase>
<empty passphrase again>

```