From [the official website](https://www.passwordstore.org/):

	*Password management should be simple and follow Unix philosophy. With pass, each password lives inside of a gpg encrypted file whose filename is the title of the website or resource that requires the password. These encrypted files may be organized into meaningful folder hierarchies, copied from computer to computer, and, in general, manipulated using standard command line file management utilities.*

pass is a simple password manager for the command line. Pass is a shell script that makes use of existing tools like [gnupg](https://www.archlinux.org/packages/?name=gnupg), [tree](https://www.archlinux.org/packages/?name=tree) and [git](https://www.archlinux.org/packages/?name=git).

## Contents

*   [1 Installation](#Installation)
*   [2 Basic usage](#Basic_usage)
*   [3 Migrating to pass](#Migrating_to_pass)
*   [4 Extensions](#Extensions)
*   [5 Advanced usage](#Advanced_usage)
*   [6 Multiple pass Contexts (e.g. Teaming)](#Multiple_pass_Contexts_.28e.g._Teaming.29)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [pass](https://www.archlinux.org/packages/?name=pass) package.

**Tip:** An optional [Qt](/index.php/Qt "Qt") GUI is available via the [qtpass](https://www.archlinux.org/packages/?name=qtpass) package.

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

To get a view of the password store do the following. Note the example output which shows the hiearchy we just created.

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

## Extensions

Since version 1.7, pass supports extensions developed by the community. These extensions extend the features of pass with the support of new commands.

*   [pass-tomb](https://github.com/roddhjav/pass-tomb) ([pass-tomb](https://aur.archlinux.org/packages/pass-tomb/))

Manage the whole tree of your password store encrypted inside a [tomb](https://aur.archlinux.org/packages/tomb/).

*   [pass-otp](https://github.com/tadfisher/pass-otp) ([pass-otp](https://aur.archlinux.org/packages/pass-otp/))

Support for one-time-password (OTP) tokens.

*   [pass-import](https://github.com/roddhjav/pass-import) ([pass-import](https://aur.archlinux.org/packages/pass-import/))

A generic importer tool from other password managers.

*   [pass-update](https://github.com/roddhjav/pass-update) ([pass-update](https://aur.archlinux.org/packages/pass-update/))

An easy flow for updating passwords.

## Advanced usage

[Environment variables](/index.php/Environment_variables "Environment variables") can be used to alter where *pass* looks to do store and git operations via

```
PASSWORD_STORE_DIR=/path/to/store
PASSWORD_STORE_GIT=/path/to/store

```

For more information on how this can be used to support multiple pass repositories see [this link](https://lists.zx2c4.com/pipermail/password-store/2016-November/002463.html).

## Multiple pass Contexts (e.g. Teaming)

One can use aliases to set up different pass contexts, which helps when collaborating with different teams. We've gotten this working in bash as follows:

Add aliases to your `*~/.bashrc*`:

```
 alias passred="PASSWORD_STORE_DIR=~/.pass/red PASSWORD_STORE_GIT=~/.pass/red pass"
 alias passblue="PASSWORD_STORE_DIR=~/.pass/blue PASSWORD_STORE_GIT=~/.pass/blue pass"

```

Add these for bash-completion to your `*~/.bash_completion*` and make sure [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) is installed:

```
 source /usr/share/bash-completion/completions/pass
 _passred(){
     PASSWORD_STORE_DIR=~/.pass/red/ _pass
 }
 complete -o filenames -o nospace -F _passred passred
 _passblue(){
     PASSWORD_STORE_DIR=~/.pass/blue/ _pass
 }
 complete -o filenames -o nospace -F _passblue passblue

```

Now you can initialize into `*~/.pass/red*` and `*~/.pass/blue*` and have two pass contexts with the `*passred*` and `*passblue*` aliases. You can generalize this further into as many contexts as you like.

## See also

*   [A more comprehensive pass tutorial](http://blog.sanctum.geek.nz/linux-crypto-passwords/)