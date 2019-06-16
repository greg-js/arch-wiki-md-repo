From [the official website](https://www.passwordstore.org/):

	Password management should be simple and follow Unix philosophy. With pass, each password lives inside of a gpg encrypted file whose filename is the title of the website or resource that requires the password. These encrypted files may be organized into meaningful folder hierarchies, copied from computer to computer, and, in general, manipulated using standard command line file management utilities.

pass is a simple password manager for the command line. Pass is a shell script that makes use of existing tools like [GnuPG](/index.php/GnuPG "GnuPG"), [tree](https://www.archlinux.org/packages/?name=tree) and [Git](/index.php/Git "Git").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Basic usage](#Basic_usage)
*   [3 Migrating to pass](#Migrating_to_pass)
*   [4 Extensions](#Extensions)
*   [5 Advanced usage](#Advanced_usage)
*   [6 Multiple pass Contexts (e.g. Teaming)](#Multiple_pass_Contexts_(e.g._Teaming))
*   [7 Git integration](#Git_integration)
    *   [7.1 Git helper usage](#Git_helper_usage)
        *   [7.1.1 git Configuration](#git_Configuration)
        *   [7.1.2 Mapping File](#Mapping_File)
        *   [7.1.3 Password Store Layout](#Password_Store_Layout)
    *   [7.2 Central git server for Pass in combination with GnuPG(SSH example)](#Central_git_server_for_Pass_in_combination_with_GnuPG(SSH_example))
        *   [7.2.1 Install a bare Git repository for Pass on the server](#Install_a_bare_Git_repository_for_Pass_on_the_server)
        *   [7.2.2 Import authorized public SSH keys](#Import_authorized_public_SSH_keys)
        *   [7.2.3 On the client](#On_the_client)
*   [8 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [pass](https://www.archlinux.org/packages/?name=pass) package.

An optional [Qt](/index.php/Qt "Qt") GUI is available via the [qtpass](https://www.archlinux.org/packages/?name=qtpass) package.

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

pass comes with a dmenu wrapper to enable easy searching/copying. To use it, install the optional dependency [dmenu](https://www.archlinux.org/packages/?name=dmenu) and run:

```
$ passmenu

```

Then selecting an entry will copy its password to the clipboard. See [dmenu(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dmenu.1) for customization options such as case-insensitivity. You may want to set this to a systemwide keybinding in order to easily access passwords from any application.

**Note:** If using passmenu causes the current window to [lose focus](/index.php/Dmenu#Current_window_loses_focus "Dmenu"), downgrade dmenu to 4.8

## Migrating to pass

There are multiple scripts listed on the [pass-project page](http://www.zx2c4.com/projects/password-store/) to import passwords from other programs

## Extensions

Since version 1.7, pass supports extensions developed by the community. These extensions extend the features of pass with the support of new commands.

*   [pass-tomb](https://github.com/roddhjav/pass-tomb) ([pass-tomb](https://aur.archlinux.org/packages/pass-tomb/))

Manage the whole tree of your password store encrypted inside a [tomb](/index.php/Tomb "Tomb").

*   [pass-otp](https://github.com/tadfisher/pass-otp) ([pass-otp](https://www.archlinux.org/packages/?name=pass-otp))

Support for one-time-password (OTP) tokens.

*   [pass-import](https://github.com/roddhjav/pass-import) ([pass-import](https://aur.archlinux.org/packages/pass-import/))

A generic importer tool from other password managers.

*   [pass-update](https://github.com/roddhjav/pass-update) ([pass-update](https://aur.archlinux.org/packages/pass-update/))

An easy flow for updating passwords.

*   [pass-audit](https://github.com/roddhjav/pass-audit) ([pass-audit](https://aur.archlinux.org/packages/pass-audit/))

An extension for auditing a password repository.

## Advanced usage

[Environment variables](/index.php/Environment_variables "Environment variables") can be used to alter where *pass* looks to do store and git operations via:

```
PASSWORD_STORE_DIR=/path/to/store

```

For more information on how this can be used to support multiple pass repositories see [this link](https://lists.zx2c4.com/pipermail/password-store/2016-November/002463.html).

## Multiple pass Contexts (e.g. Teaming)

One can use aliases to set up different pass contexts, which helps when collaborating with different teams. We have gotten this working in bash as follows:

Add aliases to your `*~/.bashrc*`:

```
 alias passred="PASSWORD_STORE_DIR=~/.pass/red pass"
 alias passblue="PASSWORD_STORE_DIR=~/.pass/blue pass"

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

## Git integration

### Git helper usage

You can use `pass` as a credentials helper for `git`. [Install](/index.php/Install "Install") the [pass-git-helper](https://aur.archlinux.org/packages/pass-git-helper/) or [pass-git-helper-git](https://aur.archlinux.org/packages/pass-git-helper-git/) package. Detail are described in the [github README file](https://github.com/languitar/pass-git-helper).

#### `git` Configuration

Install `pass-git-helper` as a git credentials helper by calling:

```
git config --global credential.helper /usr/bin/pass-git-helper

```

#### Mapping File

Create the file `~/.config/pass-git-helper/git-pass-mapping.ini`. It is used to map git remote hosts to your `pass` database. The format is something like this:

```
[github.com]
target=dev/github

[*.fooo-bar.*]
target=dev/fooo-bar
```

You can use wildcards in the host part, as shown in the example.

#### Password Store Layout

As usual with pass, the helper assumes that the password is contained in the first line of the passwordstore entry. Additionally, if a second line is present, this line is interpreted as the username.

For this to work, you have to use `pass insert --multiline` to create a multi line password store entry.

### Central git server for Pass in combination with GnuPG(SSH example)

You are able to setup a password management system by setting up a central git server for Pass. This allows you to synchronize your central password repository through multiple client environments.

#### Install a bare Git repository for Pass on the server

On the server run `git init --bare ~/.password-store` to create a bare repository you can push to.

#### Import authorized public SSH keys

See [SSH keys#Copying the public key to the remote server](/index.php/SSH_keys#Copying_the_public_key_to_the_remote_server "SSH keys")

#### On the client

This section assumes you have configured GnuPG and have a key pair to encrypt passwords. On your local client ensure you have a local password store on the client, then enable management of local changes through Git, add your remote Git repository, and push your local Pass history.

```
# Create local password store
pass init <gpg key id>
# Enable management of local changes through Git
pass git init
# Add the the remote git repository as 'origin'
pass git remote add origin user@server:~/.password-store
# Push your local Pass history
pass git push -u --all
```

Now you can use the standard Git commands, prefixed by `pass`. For example: `pass git push`, or `pass git pull`. Pass will automatically create commits when you use it to modify your password store.

## See also

*   [A more comprehensive pass tutorial](http://blog.sanctum.geek.nz/linux-crypto-passwords/)
*   [Pass home page](https://www.passwordstore.org/)
*   [List of Compatible clients and possibilities for migration to Pass](https://www.passwordstore.org/#other)