[KDE Wallet Manager](http://utils.kde.org/projects/kwalletmanager/) is a tool to manage the passwords on your KDE Plasma system. By using the KWallet subsystem it not only allows you to keep your own secrets but also to access and manage the passwords of every application that integrates with KWallet.

## Contents

*   [1 Unlock KDE Wallet automatically on login](#Unlock_KDE_Wallet_automatically_on_login)
*   [2 Using the KDE Wallet to store ssh keys](#Using_the_KDE_Wallet_to_store_ssh_keys)
*   [3 KDE Wallet for Firefox](#KDE_Wallet_for_Firefox)
*   [4 KDE Wallet for Chromium](#KDE_Wallet_for_Chromium)
*   [5 See also](#See_also)

## Unlock KDE Wallet automatically on login

If your KWallet password is the same as your username password, you can unlock your wallet automatically on login.

For **Plasma 4**, install the [pam_kwallet-git](https://aur.archlinux.org/packages/pam_kwallet-git/).

Then edit `/etc/pam.d/kde` and add the two lines under their corresponding sections:

```
auth            optional        pam_kwallet.so kdehome=.kde4
session         optional        pam_kwallet.so
```
 `Example /etc/pam.d/kde` 
```
#%PAM-1.0
auth            include         system-login
auth            optional        pam_kwallet.so kdehome=.kde4 

account         include         system-login

password        include         system-login

session         include         system-login
session         optional        pam_kwallet.so
```

For **Plasma 5**, install [kwallet-pam](https://www.archlinux.org/packages/?name=kwallet-pam) package. Then edit your login manager pam file and add the two lines under their corresponding sections:

```
-auth            optional        pam_kwallet5.so
-session         optional        pam_kwallet5.so auto_start
```

For [LightDM](/index.php/LightDM "LightDM"), for example, edit lightdm and lightdm-greeter files:

 `Example /etc/pam.d/lightdm` 
```
#%PAM-1.0
auth            include         system-login
-auth            optional        pam_kwallet5.so

account         include         system-login

password        include         system-login

session         include         system-login
-session         optional        pam_kwallet5.so auto_start
```

For [SDDM](/index.php/SDDM "SDDM"), just edit the sddm file like this to get both kwallet4 and kwallet5 to auto-unlock:

 `Example /etc/pam.d/sddm` 
```
auth            include         system-login
auth            optional        pam_kwallet5.so
auth            optional        pam_kwallet.so kdehome=.kde4
account         include         system-login
password        include         system-login
session         include         system-login
session         optional        pam_kwallet5.so
session         optional        pam_kwallet.so
```

After restarting your wallet should unlock automatically if your user password is the same as your KWallet password and you use a login manager like KDM.

**Note:** Currently, pam_kwallet-git / kwallet-pam has at least two limitations: first, it's not compatible with [GnuPG](/index.php/GnuPG "GnuPG") keys, so KDE Wallet must use the standard blowfish encryption. Also, the wallet name must be "kdewallet" (that's the default name). If, for some reason, you create a new wallet, you need to use this name (so you will probably need to rename the old wallet too).

## Using the KDE Wallet to store ssh keys

First, make sure that you have an [SSH agent](/index.php/SSH_agent "SSH agent") running.

[Install](/index.php/Install "Install") the [ksshaskpass](https://www.archlinux.org/packages/?name=ksshaskpass) package.

**Note:** If you use KDE4 and run into problems due to ksshaskpass connecting to a [second instance of kwallet](https://bbs.archlinux.org/viewtopic.php?pid=1525004), try installing [ksshaskpass4](https://aur.archlinux.org/packages/ksshaskpass4/) instead.

Create an autostart file (KDE4: `~/.kde4/Autostart/ssh-add.sh`, KDE Plasma: `~/.config/autostart/ssh-add.sh`) with this content:

```
#!/bin/sh
ssh-add </dev/null

```

KDE Plasma no longer processes *.sh startup scripts in the autostart directory. There are two methods to fix this.

**Method #1: Move ssh-add.sh to the new autostart-scripts directory**

Instead of placing the file in `~/.config/autostart/ssh-add.sh`, place it in `~/.config/autostart-scripts/ssh-add.sh`.

**Method #2: Convert ssh-add.sh to a desktop file**

You can also create a startup .desktop file `~/.config/autostart/ssh-add.desktop`:

```
[Desktop Entry]
Exec=~/.config/autostart/ssh-add.sh
Icon=system-run
StartupNotify=true
Terminal=false
Type=Application

```

**Tip:** The above ssh-add.sh script will only add the default key `~/.ssh/id_rsa`. Assuming you have different SSH keys named `key1`, `key2`, `key3` in `~/.ssh/`, you may add them automatically on login by changing the above script to:
```
#!/bin/sh
ssh-add $HOME/.ssh/key1 $HOME/.ssh/key2 $HOME/.ssh/key3 </dev/null

```

If you created a desktop file for ssh-add above, reboot. If you created a sh file, make it executable and run it:

**Plasma 4**

```
$ chmod +x ~/.kde4/Autostart/ssh-add.sh
$ ~/.kde4/Autostart/ssh-add.sh

```

**Plasma 5**

```
$ chmod +x ~/.config/autostart-scripts/ssh-add.sh
$ ~/.config/autostart-scripts/ssh-add.sh

```

You also have to set the `SSH_ASKPASS` environment variable in your /etc/profile or ~/.bash_profile:

```
export SSH_ASKPASS="/usr/bin/ksshaskpass"

```

It will ask for your password and unlock your SSH keys. Upon restart your SSH keys should be unlocked once you give your kwallet password.

To add a new key and store the password with kwallet use the following command

```
$ ssh-add /path/to/new/key </dev/null

```

and append the key to the list of keys in `~/.kde4/Autostart/ssh-add.sh` as explained above to have it unlocked upon providing the kwallet password.

## KDE Wallet for Firefox

There is an addon to make Firefox store passwords with [KDE5 Wallet](https://addons.mozilla.org/addon/kde5-wallet-password-integrati/) or [KDE4 Wallet](https://addons.mozilla.org/addon/kde-wallet-password-integratio/).

## KDE Wallet for Chromium

Chromium has built in wallet integration. To enable it, run Chromium with the `--password-store=kwallet` or `--password-store=detect` argument.

## See also

*   [Unlocking KWallet with PAM](https://www.dennogumi.org/2014/04/unlocking-kwallet-with-pam/)