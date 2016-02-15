From [GnomeKeyring](https://live.gnome.org/GnomeKeyring/):

	_GNOME Keyring is a collection of components in GNOME that store secrets, passwords, keys, certificates and make them available to applications._

**Note:** As of July 10, 2015, GNOME Keyring does not handle ECDSA[[1]](https://bugzilla.gnome.org/show_bug.cgi?id=641082) and Ed25519[[2]](https://bugzilla.gnome.org/show_bug.cgi?id=723274) keys. You can turn to other [SSH agents](/index.php/SSH_keys#SSH_agents "SSH keys") if you need support for those.

## Contents

*   [1 Installation](#Installation)
*   [2 Manage using GUI](#Manage_using_GUI)
*   [3 Using the keyring outside GNOME](#Using_the_keyring_outside_GNOME)
    *   [3.1 Without a display manager](#Without_a_display_manager)
        *   [3.1.1 Automatic login](#Automatic_login)
        *   [3.1.2 Console login](#Console_login)
            *   [3.1.2.1 PAM method](#PAM_method)
            *   [3.1.2.2 xinitrc method](#xinitrc_method)
    *   [3.2 With a display manager](#With_a_display_manager)
*   [4 SSH keys](#SSH_keys)
    *   [4.1 Disable keyring daemon SSH component](#Disable_keyring_daemon_SSH_component)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Integration with applications](#Integration_with_applications)
    *   [5.2 Flushing passphrases](#Flushing_passphrases)
    *   [5.3 GNOME Keyring and Git](#GNOME_Keyring_and_Git)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Passwords are not remembered](#Passwords_are_not_remembered)

## Installation

When using GNOME, [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) is installed automatically as a part of the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group. Otherwise install [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) from the [official repositories](/index.php/Official_repositories "Official repositories").

Extra utilities:

*   **secret-tool** — Access the GNOME keyring (and any other service implementing the [DBus Secret Service API](http://standards.freedesktop.org/secret-service/)) from the command line.

	[https://wiki.gnome.org/Projects/Libsecret](https://wiki.gnome.org/Projects/Libsecret) || [libsecret](https://www.archlinux.org/packages/?name=libsecret)

*   **gnome-keyring-query** — Provides a simple command-line tool for querying passwords from the password store of the GNOME Keyring.

	[http://www.gentoo-wiki.info/HOWTO_Use_gnome-keyring_to_store_SSH_passphrases](http://www.gentoo-wiki.info/HOWTO_Use_gnome-keyring_to_store_SSH_passphrases) || [gnome-keyring-query](https://aur.archlinux.org/packages/gnome-keyring-query/)

*   **gkeyring** — Query passwords from the command line, the [Git](/index.php/Git "Git") version can list all passwords without needing to know name or id of the item

	[https://github.com/kparal/gkeyring](https://github.com/kparal/gkeyring) || [gkeyring](https://aur.archlinux.org/packages/gkeyring/), [gkeyring-git](https://aur.archlinux.org/packages/gkeyring-git/)

## Manage using GUI

You can manage the contents of GNOME Keyring using Seahorse. Install it with the package [seahorse](https://www.archlinux.org/packages/?name=seahorse) from the official repositories.

It is possible to leave the GNOME keyring password blank or change it. In seahorse, in the "View" drop-down menu, select "By Keyring". On the Passwords tab, right click on "Passwords: login" and pick "Change password." Enter the old password and leave empty the new password. You will be warned about using unencrypted storage; continue by pushing "Use Unsafe Storage."

## Using the keyring outside GNOME

### Without a display manager

#### Automatic login

If you are using automatic login, then you can disable the keyring manager by setting a blank password on the login keyring.

**Note:** The passwords are stored unencrypted in this case.

#### Console login

When using console-based login, the keyring daemon can be started by either [PAM](https://en.wikipedia.org/wiki/Pluggable_authentication_module "wikipedia:Pluggable authentication module") or [xinitrc](/index.php/Xinitrc "Xinitrc"). PAM can also unlock the keyring automatically at login.

##### PAM method

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

**Note:**

*   To use automatic unlocking, the same password for the user account and the keyring have to be set.
*   You will still need the code in `~/.xinitrc` below in order to export the environment variables required.

##### xinitrc method

Start the gnome-keyring-daemon from [xinitrc](/index.php/Xinitrc "Xinitrc"):

 `~/.xinitrc` 

```
eval $(/usr/bin/gnome-keyring-daemon --start --components=pkcs11,secrets,ssh)
export SSH_AUTH_SOCK

```

See [Xfce#SSH agents](/index.php/Xfce#SSH_agents "Xfce") for use in Xfce.

### With a display manager

When using a display manager, the keyring works out of the box for most cases. The following display managers automatically unlock the keyring once you log in:

*   GNOME's login manager [gdm](https://www.archlinux.org/packages/?name=gdm)
*   Slim [slim](https://www.archlinux.org/packages/?name=slim)
*   LightDM [lightdm](https://www.archlinux.org/packages/?name=lightdm)

**Note:** You may need to install [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring)

For KDM, see [KDM#KDM and Gnome-keyring](/index.php/KDM#KDM_and_Gnome-keyring "KDM").

For SDDM, follow the KDM guidelines, but modify `/etc/pam.d/sddm` instead of `/etc/pam.d/kde`.

To enable the keyring for applications run through the terminal, such as SSH, add the following to your `~/.bash_profile`, `~/.zshenv`, or similar:

 `~/.zshenv` 

```
if [ -n "$DESKTOP_SESSION" ];then
    eval $(gnome-keyring-daemon --start)
    export SSH_AUTH_SOCK
fi
```

**Note:** The GNOME Keyring Daemon no longer exposes `GNOME_KEYRING_PID`. See [commit](https://mail.gnome.org/archives/commits-list/2014-March/msg03864.html).

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

### Disable keyring daemon SSH component

In case if you run your own version of the SSH agent (e.g. [ssh-agent](/index.php/SSH_keys#ssh-agent "SSH keys")), you need to disable the SSH component in GNOME keyring daemon:

```
 ln -sf /dev/null /etc/xdg/autostart/gnome-keyring-ssh.desktop

```

Then you need to logout to make the effect.

## Tips and tricks

### Integration with applications

*   [Firefox#GNOME Keyring integration](/index.php/Firefox#GNOME_Keyring_integration "Firefox")

### Flushing passphrases

```
gnome-keyring-daemon -r -d

```

This command starts gnome-keyring-daemon, shutting down previously running instances.

### GNOME Keyring and Git

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

## Troubleshooting

### Passwords are not remembered

If you get a password prompt every time you login, and you find that passwords are not saved, you might need to create/set a default keyring.

Ensure that the [seahorse](https://www.archlinux.org/packages/?name=seahorse) package is installed, open it ("Passwords and Keys" in system settings) and select _View_ > _By Keyring_ If there is no keyring in the left column (it will be marked with a lock icon), go to _File_ > _New_ > _Password Keyring_ and give it a name. You will be asked to enter a password. If you do not give the keyring a password it will be unlocked automatically, even when using autologin, but passwords will not be stored securely. Finally, right-click on the keyring you just created and select "Set as default".