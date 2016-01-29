# Pass

[pass](http://www.zx2c4.com/projects/password-store/) is a simple password manager for the command line. Passwords are stored inside gpg encrypted files in a simple directory tree structure. pass is a shell script that makes use of existing tools like [gnupg](https://www.archlinux.org/packages/?name=gnupg), [pwgen](https://www.archlinux.org/packages/?name=pwgen), [tree](https://www.archlinux.org/packages/?name=tree) and [git](https://www.archlinux.org/packages/?name=git).

## Contents

*   [1 Installation](#Installation)
*   [2 Basic usage](#Basic_usage)
*   [3 Migrating to pass](#Migrating_to_pass)
*   [4 GUI](#GUI)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [pass](https://www.archlinux.org/packages/?name=pass) package.

## Basic usage

**Note:** To be able to use pass, set up gnupg as described in [GnuPG#Basic keys management](/index.php/GnuPG#Basic_keys_management "GnuPG")

*   Initialize the password store

```
$ pass init <gpg-id or email>

```

*   Insert password, providing a descriptive hierarchical name

```
$ pass insert archlinux.org/wiki/username

```

*   Get a view of the password store

 `$ pass` 

```
Password Store
└── archlinux.org
    └── wiki
        └── username

```

*   Generate a new random password, where `<n>` is the desired password length as a number.

```
$ pass generate archlinux.org/wiki/username <n>

```

*   Retrieve password, enter the gpg passphrase at the prompt

```
$ pass archlinux.org/wiki/username

```

*   Users of Xorg with [xclip](https://www.archlinux.org/packages/?name=xclip) installed can retrieve the password directly onto the clipboard temporarily to paste into web forms via:

```
$ pass -c archlinux.org/wiki/username

```

**Note:** Users preferring the classical middle-click/paste can add the following to their respective ~/.shellrc for this behavior: `export PASSWORD_STORE_X_SELECTION=primary`

## Migrating to pass

There are multiple scripts listed on the [pass-project page](http://www.zx2c4.com/projects/password-store/) to import passwords from other programs

## GUI

There is now a stable release of [qtpass](https://aur.archlinux.org/packages/qtpass/) available on the AUR.

## See also

*   [A more comprehensive pass tutorial](http://blog.sanctum.geek.nz/linux-crypto-passwords/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pass&oldid=413133](https://wiki.archlinux.org/index.php?title=Pass&oldid=413133)"