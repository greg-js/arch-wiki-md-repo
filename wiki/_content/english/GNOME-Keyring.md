[GNOME Keyring](https://wiki.gnome.org/Projects/GnomeKeyring) is "a collection of components in GNOME that store secrets, passwords, keys, certificates and make them available to applications."

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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
    *   [4.1 Start SSH and Secrets components of keyring daemon](#Start_SSH_and_Secrets_components_of_keyring_daemon)
    *   [4.2 Disable keyring daemon components](#Disable_keyring_daemon_components)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Integration with applications](#Integration_with_applications)
    *   [5.2 Flushing passphrases](#Flushing_passphrases)
    *   [5.3 Git integration](#Git_integration)
    *   [5.4 GnuPG integration](#GnuPG_integration)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Passwords are not remembered](#Passwords_are_not_remembered)
    *   [6.2 Resetting the keyring](#Resetting_the_keyring)
*   [7 See also](#See_also)

## Installation

When using GNOME, [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) is installed automatically as a part of the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group. Otherwise [install](/index.php/Install "Install") the [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) package. Install [libsecret](https://www.archlinux.org/packages/?name=libsecret) to allow applications to use your keyrings. [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring) is deprecated, however, some applications may require it.

Extra utilities related to GNOME keyring include:

*   **secret-tool** — Access the GNOME keyring (and any other service implementing the [DBus Secret Service API](https://specifications.freedesktop.org/secret-service/)) from the command line.

	[https://wiki.gnome.org/Projects/Libsecret](https://wiki.gnome.org/Projects/Libsecret) || [libsecret](https://www.archlinux.org/packages/?name=libsecret)

*   **gnome-keyring-query** — Provides a simple command-line tool for querying passwords from the password store of the GNOME Keyring. (uses the deprecated [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring))

	|| [gnome-keyring-query](https://aur.archlinux.org/packages/gnome-keyring-query/)

*   **gkeyring** — Query passwords from the command line. (uses the deprecated [libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring))

	[https://github.com/kparal/gkeyring](https://github.com/kparal/gkeyring) || [gkeyring](https://aur.archlinux.org/packages/gkeyring/), [gkeyring-git](https://aur.archlinux.org/packages/gkeyring-git/)

## Manage using GUI

You can manage the contents of GNOME Keyring using Seahorse. [Install](/index.php/Install "Install") it with the package [seahorse](https://www.archlinux.org/packages/?name=seahorse).

It is possible to leave the GNOME keyring password blank or change it. In seahorse, in the "View" drop-down menu, select "By Keyring". On the Passwords tab, right click on "Passwords: login" and pick "Change password." Enter the old password and leave empty the new password. You will be warned about using unencrypted storage; continue by pushing "Use Unsafe Storage."

## Using the keyring outside GNOME

### Without a display manager

#### Automatic login

If you are using automatic login, then you can disable the keyring manager by setting a blank password on the login keyring.

**Note:** The passwords are stored unencrypted in this case.

#### Console login

When using console-based login, the keyring daemon can be started by either [PAM](/index.php/PAM "PAM") or [xinitrc](/index.php/Xinitrc "Xinitrc"). PAM can also unlock the keyring automatically at login.

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
session    optional     pam_gnome_keyring.so auto_start
```

For [SDDM](/index.php/SDDM "SDDM"), edit instead the configuration file `/etc/pam.d/sddm`.

Next, for [GDM](/index.php/GDM "GDM"), add `password optional pam_gnome_keyring.so` to the end of `/etc/pam.d/passwd`.

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

*   [GDM](/index.php/GDM "GDM")
*   [LightDM](/index.php/LightDM "LightDM")
*   [LXDM](/index.php/LXDM "LXDM")
*   [SDDM](/index.php/SDDM "SDDM")

For GDM and LightDM, note the keyring [must be](https://wiki.gnome.org/Projects/GnomeKeyring/Pam) named *login* to be automatically unlocked.

To enable the keyring for applications run through the terminal, such as SSH, add the following to your `~/.bash_profile`, `~/.zshenv`, or similar:

 `~/.bash_profile` 
```
if [ -n "$DESKTOP_SESSION" ];then
    eval $(gnome-keyring-daemon --start)
    export SSH_AUTH_SOCK
fi
```
 `~/.config/fish/config.fish` 
```
if test -n "$DESKTOP_SESSION"
    set (gnome-keyring-daemon --start | string split "=")
end
```

## SSH keys

To add your SSH key:

```
$ ssh-add ~/.ssh/id_rsa
Enter passphrase for /home/mith/.ssh/id_rsa:

```

To list automatically loaded keys:

```
$ ssh-add -L

```

To disable all keys:

```
$ ssh-add -D

```

Now when you connect to a server, the key will be found and a dialog will popup asking you for the passphrase. It has an option to automatically unlock the key when you log in. If you check this, you will not need to enter your passphrase again!

Alternatively, to permanently save the a passphrase in the keyring, use ssh-askpass from package [seahorse](https://www.archlinux.org/packages/?name=seahorse):

```
/usr/lib/seahorse/ssh-askpass my_key

```

**Note:** You have to have the corresponding `.pub` file in the same directory as the private key (`~/.ssh/id_rsa.pub` in the example). Also, make sure that the public key is the file name of the private key plus `.pub` (for example, `my_key.pub`).

### Start SSH and Secrets components of keyring daemon

If you are starting Gnome Keyring with a display manager or the Pam method described above and you are NOT using Gnome, Unity or Mate as your desktop you may find that the SSH and Secrets components are not being started automatically. You can fix this by copying the desktop files gnome-keyring-ssh.desktop and gnome-keyring-secrets.desktop from /etc/xdg/autostart/ to ~/.config/autostart/ and deleting the OnlyShowIn line.

```
$ cp /etc/xdg/autostart/{gnome-keyring-secrets.desktop,gnome-keyring-ssh.desktop} ~/.config/autostart/
$ sed -i '/^OnlyShowIn.*$/d' ~/.config/autostart/gnome-keyring-secrets.desktop
$ sed -i '/^OnlyShowIn.*$/d' ~/.config/autostart/gnome-keyring-ssh.desktop

```

### Disable keyring daemon components

If you wish to run an alternative SSH agent (e.g. [ssh-agent](/index.php/SSH_keys#ssh-agent "SSH keys") or [gpg-agent](/index.php/GnuPG#gpg-agent "GnuPG")), you need to disable the `ssh` component of GNOME Keyring. To do so in an account-local way, copy `/etc/xdg/autostart/gnome-keyring-ssh.desktop` to `~/.config/autostart/` and then append the line `Hidden=true` to the copied file. Then log out.

**Note:** In case you use [GNOME](/index.php/GNOME "GNOME") 3.24 or older on [Wayland](/index.php/Wayland "Wayland"), gnome-shell will overwrite `SSH_AUTH_SOCK` to point to gnome-keyring regardless if it is running or not. To prevent this, you need to set the environment variable GSM_SKIP_SSH_AGENT_WORKAROUND before gnome-shell is started. One way to do this is to add the line `GSM_SKIP_SSH_AGENT_WORKAROUND DEFAULT=1` to `~/.pam_environment`.

## Tips and tricks

### Integration with applications

*   [Firefox](/index.php/Firefox#KDE.2FGNOME_integration "Firefox")

### Flushing passphrases

```
gnome-keyring-daemon -r -d

```

This command starts gnome-keyring-daemon, shutting down previously running instances.

### Git integration

The GNOME keyring is useful in conjuction with [Git](/index.php/Git "Git") when you are pushing over HTTPS.

[Install](/index.php/Install "Install") the [libsecret](https://www.archlinux.org/packages/?name=libsecret) package.

Set Git up to use the helper:

```
$ git config --global credential.helper /usr/lib/git-core/git-credential-libsecret

```

Next time you do a *git push*, you are asked to unlock your keyring, if not unlocked already.

### GnuPG integration

Several applications which use GnuPG require a `pinentry-program` to be set. Set the following to use Gnome 3 pinentry for Gnome Keyring to manage passphrase prompts.

 `~/.gnupg/gpg-agent.conf` 
```
pinentry-program /usr/bin/pinentry-gnome3

```

Another option is to [force loopback for GPG](/index.php/GnuPG#Unattended_passphrase "GnuPG") which should allow the passphrase to be entered in the application.

## Troubleshooting

### Passwords are not remembered

If you get a password prompt every time you login, and you find that passwords are not saved, you might need to create/set a default keyring.

Ensure that the [seahorse](https://www.archlinux.org/packages/?name=seahorse) package is [installed](/index.php/Install "Install"), open it ("Passwords and Keys" in system settings) and select *View* > *By Keyring*. If there is no keyring in the left column (it will be marked with a lock icon), go to *File* > *New* > *Password Keyring* and give it a name. You will be asked to enter a password. If you do not give the keyring a password it will be unlocked automatically, even when using autologin, but passwords will not be stored securely. Finally, right-click on the keyring you just created and select "Set as default".

### Resetting the keyring

If you get the error "The password you use to login to your computer no longer matches that of your login keyring", you can simply reset your gnome keyring.

Remove "login.keyring" and "user.keystore" from */home/{username}/.local/share/keyrings/*. After removing the files, simply log out and log in again. Obviously, this will remove your saved keys.

## See also

*   [GNOME wiki](https://wiki.gnome.org/action/show/Projects/GnomeKeyring)