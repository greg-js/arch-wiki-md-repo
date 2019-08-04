Related articles

*   [GnuPG](/index.php/GnuPG "GnuPG")

From [Wikipedia](https://en.wikipedia.org/wiki/Keybase "wikipedia:Keybase"):

	Keybase is a key directory that maps social media identities to encryption keys (including, but not limited to PGP keys) in a publicly auditable manner. Keybase also offers an encrypted chat and cloud storage system, called Keybase Chat and the Keybase filesystem respectively. Files placed in the public portion of the filesystem are served from a public endpoint, as well as locally from a filesystem mounted by the Keybase client. Keybase supports publicly connecting Twitter, GitHub, Facebook, Reddit, and Hacker News identities to encryption keys, along with Bitcoin and Zcash wallet addresses.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Signup / Login](#Signup_/_Login)
*   [3 GnuPG Keys](#GnuPG_Keys)
*   [4 Keybase Filesystem (KBFS)](#Keybase_Filesystem_(KBFS))
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Keybase GUI starts automatically](#Keybase_GUI_starts_automatically)
*   [6 See also](#See_also)

## Installation

Keybase is provided by the [keybase](https://www.archlinux.org/packages/?name=keybase) package. The KBFS filesystem and Keybase GUI can be additionally installed with the [kbfs](https://www.archlinux.org/packages/?name=kbfs) and [keybase-gui](https://www.archlinux.org/packages/?name=keybase-gui) packages. Alternatively, [keybase-bin](https://aur.archlinux.org/packages/keybase-bin/) is available on the AUR which includes everything in a single package. See also the [install instructions on keybase.io](https://keybase.io/docs/the_app/install_linux).

## Signup / Login

If you installed the GUI via [keybase-bin](https://aur.archlinux.org/packages/keybase-bin/), it will walk you through signup. These instructions are for the CLI-only [keybase](https://www.archlinux.org/packages/?name=keybase) package.

Keybase requires its service to be running so you can interact with it. First start the keybase service by starting the included systemd service as your user (enable this service to run on boot):

```
 $ systemctl start --user keybase

```

Or alternatively, run the keybase service manually:

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
$ keybase pgp gen

```

This will interactively generate a key pair and securely upload the keys.

## Keybase Filesystem (KBFS)

KBFS uses [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") to mount the remote cryptographic filesystem. It comes with the [keybase-bin](https://aur.archlinux.org/packages/keybase-bin/) package, or can be installed separately with [kbfs](https://www.archlinux.org/packages/?name=kbfs).

Keybase allows users to store up to 250 GB of files in a cloud storage called the Keybase filesystem. The filesystem is divided into three parts: public files, private files, and team files. The filesystem is mounted to `/keybase` by default if installed through [keybase-bin](https://aur.archlinux.org/packages/keybase-bin/).

To configure kbfs if installed via the [kbfs](https://www.archlinux.org/packages/?name=kbfs) package, first ensure the keybase service is running (see instructions above). Then configure the desired mountpoint for the KBFS:

```
 $ keybase config set mountdir /path/to/kbfs

```

Now the `kbfs` service can be started:

```
 $ systemctl start --user kbfs

```

Enable this service to have the kbfs mounted on boot.

All files under `/path/to/kbfs/public` are automatically signed by the client. All files under `/path/to/kbfs/private` are both encrypted and signed before being uploaded, making them end-to-end encrypted. See the [KBFS docs on keybase.io](https://keybase.io/docs/kbfs) for more information and usage instructions.

## Troubleshooting

### Keybase GUI starts automatically

By default, keybase-gui add a desktop entry in your [autostart](/index.php/XDG_Autostart "XDG Autostart"). To disable it:

 `keybase ctl autostart --disable` 

## See also

*   [Keybase Homepage](https://keybase.io/)
*   [Wikipedia:Keybase](https://en.wikipedia.org/wiki/Keybase "wikipedia:Keybase")
*   [Keybase Basics](https://keybase.io/docs/command_line)