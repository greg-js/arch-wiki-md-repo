# GNOME Keyring

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From [GnomeKeyring](https://live.gnome.org/GnomeKeyring/):

_GNOME Keyring is a collection of components in GNOME that store secrets, passwords, keys, certificates and make them available to applications._

**Note:** As of July 10, 2015, GNOME Keyring does not handle ECDSA[[1]](https://bugzilla.gnome.org/show_bug.cgi?id=641082) and Ed25519[[2]](https://bugzilla.gnome.org/show_bug.cgi?id=723274) keys. You can turn to other [SSH agents](/index.php/SSH_keys#SSH_agents "SSH keys") if you need support for those.

## Contents

*   [1 Installation](#Installation)
*   [2 Manage using GUI](#Manage_using_GUI)
*   [3 Use without GNOME, and without a display manager](#Use_without_GNOME.2C_and_without_a_display_manager)
    *   [3.1 Automatic login](#Automatic_login)
    *   [3.2 Console login](#Console_login)
        *   [3.2.1 PAM method](#PAM_method)
        *   [3.2.2 xinitrc method](#xinitrc_method)
*   [4 Use without GNOME, but with a display manager](#Use_without_GNOME.2C_but_with_a_display_manager)
*   [5 Disable keyring daemon](#Disable_keyring_daemon)
*   [6 SSH keys](#SSH_keys)
*   [7 Integration with applications](#Integration_with_applications)
*   [8 Flushing passphrases](#Flushing_passphrases)
*   [9 GNOME Keyring and Git](#GNOME_Keyring_and_Git)
*   [10 Useful tools](#Useful_tools)

## Installation

When using GNOME, [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) is installed automatically as a part of the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group. Otherwise install [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Manage using GUI

You can manage the contents of GNOME Keyring using Seahorse. Install it with the package [seahorse](https://www.archlinux.org/packages/?name=seahorse) from the official repositories.

It is possible to leave the GNOME keyring password blank or change it. In seahorse, in the "View" drop-down menu, select "By Keyring". On the Passwords tab, right click on "Passwords: login" and pick "Change password." Enter the old password and leave empty the new password. You will be warned about using unencrypted storage; continue by pushing "Use Unsafe Storage."

## Use without GNOME, and without a display manager

### Automatic login

If you are using automatic login, then you can disable the keyring manager by setting a blank password on the login keyring.

**Note:** The passwords are stored unencrypted in this case.

### Console login

When using console-based login, the keyring daemon can be started by either [PAM](https://en.wikipedia.org/wiki/Pluggable_authentication_module "wikipedia:Pluggable authentication module") or [xinitrc](/index.php/Xinitrc "Xinitrc"). PAM can also unlock the keyring automatically at login.

#### PAM method

Start the gnome-keyring-daemon from `/etc/pam.d/login`:

Add `auth optional pam_gnome_keyring.so` at the end of the `auth` section and `session optional pam_gnome_keyring.so auto_start` at the end of the `session` section.

 `/etc/pam.d/login` 

```
#%PAM-1.0

 auth       required     pam_securetty.so
 auth       requisite    pam_nologin.so
 auth       include      system-local-login
 auth       optional     pam_gnome_keyring.so
 account    include      system-local-login
 session    include      system-local-login
 session    optional     pam_gnome_keyring.so        auto_start
```

Next, add `password optional pam_gnome_keyring.so` to the end of `/etc/pam.d/passwd`.

 `/etc/pam.d/passwd` 

```
#%PAM-1.0

 #password	required	pam_cracklib.so difok=2 minlen=8 dcredit=2 ocredit=2 retry=3
 #password	required	pam_unix.so sha512 shadow use_authtok
 password	required	pam_unix.so sha512 shadow nullok
 password	optional	pam_gnome_keyring.so
```

**Note:** To use automatic unlocking, the same password for the user account and the keyring have to be set.

**Note:** You will still need the code in `~/.xinitrc` below in order to export the environment variables required.

#### xinitrc method

Start the gnome-keyring-daemon from [xinitrc](/index.php/Xinitrc "Xinitrc"):

 `~/.xinitrc` 

```
eval $(/usr/bin/gnome-keyring-daemon --start --components=pkcs11,secrets,ssh)
export SSH_AUTH_SOCK

```

See [Xfce#SSH agents](/index.php/Xfce#SSH_agents "Xfce") for use in Xfce.

## Use without GNOME, but with a display manager

When using a display manager, the keyring works out of the box for most cases. The following display managers automatically unlock the keyring once you log in:

*   GNOME's login manager [gdm](https://www.archlinux.org/packages/?name=gdm)
*   Slim [slim](https://www.archlinux.org/packages/?name=slim)
*   LightDM [lightdm](https://www.archlinux.org/packages/?name=lightdm)

**Note:** You may need to install [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring)

For KDM, see [KDM#KDM and Gnome-keyring](/index.php/KDM#KDM_and_Gnome-keyring "KDM").

To enable the keyring for applications run through the terminal, such as SSH, add the following to your `~/.bash_profile`, `~/.zshenv`, or similar:

 `~/.zshenv` 

```
if [ -n "$DESKTOP_SESSION" ];then
    eval $(gnome-keyring-daemon --start)
    export SSH_AUTH_SOCK
fi
```

**Note:** The GNOME Keyring Daemon no longer exposes `GNOME_KEYRING_PID`. See [commit](https://mail.gnome.org/archives/commits-list/2014-March/msg03864.html).

## Disable keyring daemon

In case if you run your own version of the SSH agent (e.g. [ssh-agent](/index.php/SSH_keys#ssh-agent "SSH keys")), you need to disable the SSH component in GNOME keyring daemon:

```
 ln -sf /dev/null /etc/xdg/autostart/gnome-keyring-ssh.desktop

```

Then you need to logout to make the effect.

## SSH keys

To add your SSH key:

```
$ ssh-add ~/.ssh/id_dsa
Enter passphrase for /home/mith/.ssh/id_dsa:

```

To list automatically loaded keys:

```
$ ssh-add -L

```

To disable all keys;

```
$ ssh-add -D

```

Now when you connect to a server, the key will be found and a dialog will popup asking you for the passphrase. It has an option to automatically unlock the key when you log in. If you check this, you will not need to enter your passphrase again!

Alternatively, to permanently save the a passphrase in the keyring, use seahorse-ssh-askpass from package [seahorse](https://www.archlinux.org/packages/?name=seahorse):

```
/usr/lib/seahorse/seahorse-ssh-askpass my_key

```

**Note:** You have to have a have the corresponding `.pub` file in the same directory as the private key (`~/.ssh/id_dsa.pub` in the example). Also, make sure that the public key is the file name of the private key plus `.pub` (for example, `my_key.pub`).

## Integration with applications

*   [Firefox#GNOME Keyring integration](/index.php/Firefox#GNOME_Keyring_integration "Firefox")

## Flushing passphrases

```
gnome-keyring-daemon -r -d

```

This command starts gnome-keyring-daemon, shutting down previously running instances.

## GNOME Keyring and Git

The GNOME keyring is useful in conjuction with [Git](/index.php/Git "Git") when you are pushing over HTTPS.

First install the package [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring) from the [official repositories](/index.php/Official_repositories "Official repositories").

Next compile the helper:

```
$ cd /usr/share/git/credential/gnome-keyring
# make

```

Set Git up to use the helper:

```
$ git config --global credential.helper /usr/lib/git-core/git-credential-gnome-keyring

```

Next time you do a _git push_, you are asked to unlock your keyring, if not unlocked already.

## Useful tools

`secret-tool` (in the [libsecret](https://www.archlinux.org/packages/?name=libsecret) package) can access the GNOME keyring (and any other service implementing the [DBus Secret Service API](http://standards.freedesktop.org/secret-service/)) from the command line.

[gnome-keyring-query](https://aur.archlinux.org/packages/gnome-keyring-query/)<sup><small>AUR</small></sup> from the AUR provides a simple command-line tool for querying passwords from the password store of the GNOME Keyring.

[gkeyring](https://aur.archlinux.org/packages/gkeyring/)<sup><small>AUR</small></sup> also allows querying passwords from the command-line.

Unlike the three options above, [gkeyring-git](https://aur.archlinux.org/packages/gkeyring-git/)<sup><small>AUR</small></sup> allows listing of all passwords, without having to know the id or name of the item.

Retrieved from "[https://wiki.archlinux.org/index.php?title=GNOME_Keyring&oldid=401616](https://wiki.archlinux.org/index.php?title=GNOME_Keyring&oldid=401616)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [GNOME](/index.php/Category:GNOME "Category:GNOME")