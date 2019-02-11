[KDE Wallet Manager](http://utils.kde.org/projects/kwalletmanager/) is a tool to manage passwords on the [KDE](/index.php/KDE "KDE") Plasma system. By using the KWallet subsystem it not only allows you to keep your own secrets but also to access and manage the passwords of every application that integrates with KWallet.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Unlock KDE Wallet automatically on login](#Unlock_KDE_Wallet_automatically_on_login)
    *   [1.1 Configure display manager](#Configure_display_manager)
*   [2 Using the KDE Wallet to store ssh key passphrases](#Using_the_KDE_Wallet_to_store_ssh_key_passphrases)
*   [3 KDE Wallet for Firefox](#KDE_Wallet_for_Firefox)
*   [4 KDE Wallet for Chrome and Chromium](#KDE_Wallet_for_Chrome_and_Chromium)
*   [5 See also](#See_also)

## Unlock KDE Wallet automatically on login

**Note:**

*   [kwallet-pam](https://www.archlinux.org/packages/?name=kwallet-pam) is not compatible with [GnuPG](/index.php/GnuPG "GnuPG") keys, the KDE Wallet must use the standard `blowfish` encryption.
*   The chosen KWallet password must be the same as the current [user](/index.php/User "User") password.
*   The wallet cannot be unlocked when using autologin.
*   The wallet must be named `kdewallet` (default name). It does not unlock any other wallet(s).
*   If using [KDE](/index.php/KDE "KDE"), one may want to disable *Close when last application stops using it* in KDE Wallet settings to prevent the wallet from being closed after each usage ([WiFi](/index.php/WiFi "WiFi")-passphrase unlock, etc.).
*   It may be needed to remove the default created wallet first, thus removing all stored entries.
*   If the kwallet Migration Assistant asks for a password after every login, rename or delete the `~/.kde4/share/apps/kwallet` folder.

[Install](/index.php/Install "Install") [kwallet-pam](https://www.archlinux.org/packages/?name=kwallet-pam) for the [PAM](/index.php/PAM "PAM") compatible module.

Optional [install](/index.php/Install "Install") [kwalletmanager](https://www.archlinux.org/packages/?name=kwalletmanager) for the wallet management tool. This tool can be used to create a KDE Wallet with `blowfish` encryption and more settings not provided by the *kcm-module*.

### Configure display manager

The following lines must be present under their corresponding sections:

```
auth            optional        pam_kwallet5.so
session         optional        pam_kwallet5.so auto_start
```

It may be needed to edit the [display manager](/index.php/Display_manager "Display manager") configuration:

*   For [SDDM](/index.php/SDDM "SDDM") no further edits should be needed because the lines are already present in `/etc/pam.d/sddm`.
*   For [GDM](/index.php/GDM "GDM") edit `/etc/pam.d/gdm-password` accordingly.
*   For [LightDM](/index.php/LightDM "LightDM") edit `/etc/pam.d/lightdm` and `/etc/pam.d/lightdm-greeter` files:

 `/etc/pam.d/lightdm` 
```
#%PAM-1.0
auth            include         system-login
**auth            optional        pam_kwallet5.so**

account         include         system-login

password        include         system-login

session         include         system-login
**session         optional        pam_kwallet5.so auto_start**
```

## Using the KDE Wallet to store ssh key passphrases

**Note:** A [SSH agent](/index.php/SSH_agent "SSH agent") should be up and running.

[Install](/index.php/Install "Install") [ksshaskpass](https://www.archlinux.org/packages/?name=ksshaskpass) package.

[Create](/index.php/Create "Create") an [autostart script file](/index.php/KDE#Autostart "KDE") and mark it as [executable](/index.php/Executable "Executable"):

 `~/.config/autostart-scripts/ssh-add.sh` 
```
#!/bin/sh
ssh-add </dev/null

```

**Tip:** The above ssh-add.sh script will only add the default key `~/.ssh/id_rsa`. Assuming you have different SSH keys named `key1`, `key2`, `key3` in `~/.ssh/`, you may add them automatically on login by changing the above script to: `~/.config/autostart-scripts/ssh-add.sh` 
```
#!/bin/sh
ssh-add $HOME/.ssh/key1 $HOME/.ssh/key2 $HOME/.ssh/key3 </dev/null

```

You also have to set the `SSH_ASKPASS` [environment variable](/index.php/Environment_variable "Environment variable") to `ksshaskpass`.

It will ask for your password and unlock your SSH keys. Upon restart your SSH keys should be unlocked once you give your kwallet password.

To add a new key and store the password with kwallet use the following command

```
$ ssh-add /path/to/new/key </dev/null

```

and append the key to the list of keys in `~/.config/autostart-scripts/ssh-add.sh` as explained above to have it unlocked upon providing the kwallet password.

## KDE Wallet for Firefox

**Note:** As of Firefox 57 this addon is not supported anymore. Use [firefox-esr52](https://aur.archlinux.org/packages/firefox-esr52/) (supported until August 2018) if wanting to use this addon.

There is an unofficial [Firefox](/index.php/Firefox "Firefox") addon for [KDE5 Wallet](https://addons.mozilla.org/addon/kde5-wallet-password-integrati/) integration.

## KDE Wallet for Chrome and Chromium

Chrome/Chromium has built in wallet integration. To enable it, run Chromium with the `--password-store=kwallet` or `--password-store=detect` argument. To make the change persistent, see [Chromium/Tips and tricks#Making flags persistent](/index.php/Chromium/Tips_and_tricks#Making_flags_persistent "Chromium/Tips and tricks"). (Setting CHROMIUM_USER_FLAGS will not work.)

## See also

*   [Unlocking KWallet with PAM](https://www.dennogumi.org/2014/04/unlocking-kwallet-with-pam/)