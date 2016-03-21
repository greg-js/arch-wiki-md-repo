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

**Note:** To be able to use pass, set up [GnuPG](/index.php/GnuPG "GnuPG").

To initialize the password store:

```
$ pass init *<gpg-id or email>*

```

To create a new password, first provide a descriptive hierarchical name. In this example, this is *archlinux.org/wiki/username*.

```
$ pass insert archlinux.org/wiki/username

```

To get a view of the password store do the following. Not the example output which shows the hiearchy we just created.

 `$ pass` 
```
Password Store
└── archlinux.org
    └── wiki
        └── username

```

To generate a new random password for the above example, do the following, where `*n*` is the desired password length as a number:

```
$ pass generate archlinux.org/wiki/username *n*

```

To retreive a password, enter the gpg passphrase at the following prompt, again using the same hierarchical example name from above:

```
$ pass archlinux.org/wiki/username

```

Users of Xorg with [xclip](https://www.archlinux.org/packages/?name=xclip) installed can retrieve the password directly onto the clipboard temporarily (*e.g.,* to paste into web forms). To do so, do the following (again with the same example hierarchical name from above):

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