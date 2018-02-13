Related articles

*   [GnuPG](/index.php/GnuPG "GnuPG")

From [Wikipedia](https://en.wikipedia.org/wiki/Keybase "wikipedia:Keybase"):

	Keybase is a key directory that maps social media identities to encryption keys (including, but not limited to PGP keys) in a publicly auditable manner. Keybase also offers an encrypted chat and cloud storage system, called Keybase Chat and the Keybase filesystem respectively. Files placed in the public portion of the filesystem are served from a public endpoint, as well as locally from a filesystem mounted by the Keybase client. Keybase supports publicly connecting Twitter, GitHub, Facebook, Reddit, and Hacker News identities to encryption keys, along with Bitcoin and Zcash wallet addresses.

## Contents

*   [1 Installation](#Installation)
*   [2 Signup / Login](#Signup_.2F_Login)
*   [3 GnuPG Keys](#GnuPG_Keys)
*   [4 Keybase Filesystem (KBFS)](#Keybase_Filesystem_.28KBFS.29)
*   [5 See also](#See_also)

## Installation

Keybase is provided by the [keybase](https://www.archlinux.org/packages/?name=keybase) package, however this does not yet include the GUI or the KBFS filesystem. If you want the GUI and KBFS filesystem install [keybase-bin](https://aur.archlinux.org/packages/keybase-bin/).

After installing or updating, run:

```
$ run_keybase

```

## Signup / Login

**Note:** The signup and login commands will fail with keybase-1.0.41 because the `keybase.service` does not ship with the package (see [#56831](https://bugs.archlinux.org/task/56831)). Run the following command in another terminal:
```
$ keybase service

```

To signup for a Keybase account use, and follow the on-screen prompts:

```
$ keybase signup

```

If you already have a Keybase account you can login with:

```
$ keybase login <keybase_username>

```

## GnuPG Keys

During the interactive signup if you already have any GnuPG key pairs on your keyring, Keybase will ask if you wish to use one of them. If you do not have a key pair, you can generate one with:

```
$ keybase gpg gen

```

This will interactively generate a key pair and securely upload the keys.

## Keybase Filesystem (KBFS)

KBFS uses [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") to mount the remote cryptographic filesystem via the [systemd](/index.php/Systemd "Systemd") unit `keybase.mount`.

Keybase allows users to store up to 10 GB of files in a cloud storage called the Keybase filesystem. The filesystem is divided into three parts: public files, private files, and team files. The filesystem is mounted to `/keybase`.

All files under `/keybase/public` are automatically signed by the client. All files under `/keybase/private` are both encrypted and signed before being uploaded, making them end-to-end encrypted.

## See also

*   [Keybase Homepage](https://keybase.io/)
*   [Wikipedia:Keybase](https://en.wikipedia.org/wiki/Keybase "wikipedia:Keybase")
*   [Keybase Basics](https://keybase.io/docs/command_line)