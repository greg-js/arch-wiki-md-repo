[KDE Wallet Manager](http://utils.kde.org/projects/kwalletmanager/) is a tool to manage passwords on the [KDE](/index.php/KDE "KDE") Plasma system. By using the KWallet subsystem it not only allows you to keep your own secrets but also to access and manage the passwords of every application that integrates with KWallet.

## Contents

*   [1 Unlock KDE Wallet automatically on login](#Unlock_KDE_Wallet_automatically_on_login)
    *   [1.1 Configure Display Manager](#Configure_Display_Manager)
*   [2 Using the KDE Wallet to store ssh key passhprases](#Using_the_KDE_Wallet_to_store_ssh_key_passhprases)
*   [3 KDE Wallet for Firefox](#KDE_Wallet_for_Firefox)
*   [4 KDE Wallet for Chrome and Chromium](#KDE_Wallet_for_Chrome_and_Chromium)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Inotify folder watch limit](#Inotify_folder_watch_limit)
*   [6 See also](#See_also)

## Unlock KDE Wallet automatically on login

**Note:**

*   The chosen KWallet password must be the same as the current [user](/index.php/User "User") password.
*   [kwallet-pam](https://www.archlinux.org/packages/?name=kwallet-pam) is not compatible with [GnuPG](/index.php/GnuPG "GnuPG") keys, the KDE Wallet must use the standard `blowfish` encryption.
*   The wallet must be named `kdewallet` (default name). It doesn't unlock any other wallet(s).

[Install](/index.php/Install "Install") [kwallet-pam](https://www.archlinux.org/packages/?name=kwallet-pam) for the [PAM](/index.php/PAM "PAM") compatible module.

### Configure Display Manager

The following lines must be present under their corresponding sections:

```
auth            optional        pam_kwallet5.so
session         optional        pam_kwallet5.so auto_start
```

It may be needed to edit the [Display Manager](/index.php/Display_Manager "Display Manager") configuration:

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

## Using the KDE Wallet to store ssh key passhprases

**Note:** A [SSH agent](/index.php/SSH_agent "SSH agent") should be up and running.

[Install](/index.php/Install "Install") [ksshaskpass](https://www.archlinux.org/packages/?name=ksshaskpass) package.

[Create](/index.php/Create "Create") an [autostart script file](/index.php/KDE#Autostarting_applications "KDE") and mark it as [executable](/index.php/Executable "Executable"):

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

You also have to set the `SSH_ASKPASS` [environment variable](/index.php/Environment_variable "Environment variable"), see [Environment variables#Defining variables](/index.php/Environment_variables#Defining_variables "Environment variables"). E.g.:

```
export SSH_ASKPASS="/usr/bin/ksshaskpass"

```

It will ask for your password and unlock your SSH keys. Upon restart your SSH keys should be unlocked once you give your kwallet password.

To add a new key and store the password with kwallet use the following command

```
$ ssh-add /path/to/new/key </dev/null

```

and append the key to the list of keys in `~/.config/autostart-scripts/ssh-add.sh` as explained above to have it unlocked upon providing the kwallet password.

## KDE Wallet for Firefox

**Note:** As of Firefox 57 this addon is not supported anymore. Use Firefox ESR if wanting to use this addon.

There is an unofficial [Firefox](/index.php/Firefox "Firefox") addon for [KDE5 Wallet](https://addons.mozilla.org/addon/kde5-wallet-password-integrati/) integration.

## KDE Wallet for Chrome and Chromium

Chrome/Chromium has built in wallet integration. To enable it, run Chromium with the `--password-store=kwallet` or `--password-store=detect` argument. To make the change persistent, see [Chromium/Tips and tricks#Making flags persistent](/index.php/Chromium/Tips_and_tricks#Making_flags_persistent "Chromium/Tips and tricks"). (Setting CHROMIUM_USER_FLAGS will not work.)

## Troubleshooting

### Inotify folder watch limit

If you get the following error:

```
KDE Baloo Filewatch service reached the inotify folder watch limit. File changes may be ignored.

```

Then you will need to increase the inotify folder watch limit:

```
# echo 524288 > /proc/sys/fs/inotify/max_user_watches

```

To make changes permanent, create a `40-max-user-watches.conf` file:

 `/etc/sysctl.d/40-max-user-watches.conf`  `fs.inotify.max_user_watches=524288` 

## See also

*   [Unlocking KWallet with PAM](https://www.dennogumi.org/2014/04/unlocking-kwallet-with-pam/)