[KDE Wallet Manager](http://utils.kde.org/projects/kwalletmanager/) 是一个用于管理 KDE Plasma 上密码的工具。它将用于在 KDE 上访问和管理你的密码

## Contents

*   [1 在登录时自动解锁 Kwallet](#.E5.9C.A8.E7.99.BB.E5.BD.95.E6.97.B6.E8.87.AA.E5.8A.A8.E8.A7.A3.E9.94.81_Kwallet)
*   [2 Using the KDE Wallet to store ssh keys](#Using_the_KDE_Wallet_to_store_ssh_keys)
*   [3 KDE Wallet for Firefox](#KDE_Wallet_for_Firefox)
*   [4 KDE Wallet for Chrome and Chromium](#KDE_Wallet_for_Chrome_and_Chromium)
*   [5 See also](#See_also)

## 在登录时自动解锁 Kwallet

如果您的 KWallet 密码与您的用户名密码相同，您可以在登录时自动解锁您的 KWallet。

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [kwallet-pam](https://www.archlinux.org/packages/?name=kwallet-pam) 包， 然后编辑您的登录管理器 pam (通常为于 `/etc/pam.d` ) 文件，并在其相应部分下添加:

```
auth            optional        pam_kwallet5.so
session         optional        pam_kwallet5.so auto_start
```

在 [LightDM](/index.php/LightDM "LightDM"), 修改 `/etc/pam.d/lightdm` 和 `/etc/pam.d/lightdm-greeter` 文件:

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

在 [SDDM](/index.php/SDDM "SDDM"), 只需编辑 `/etc/pam.d/sddm` 就可以让 Kwllet5 在登录后自动解锁:

 `/etc/pam.d/sddm` 
```
auth            include         system-login
**auth            optional        pam_kwallet5.so**
account         include         system-login
password        include         system-login
session         include         system-login
**session         optional        pam_kwallet5.so auto_start**
```

重新启动后，如果您的用户密码与 KWallet 密码相同，您的 KWallet 将自动解锁。

**Note:** Currently, kwallet-pam has at least two limitations: first, it's not compatible with [GnuPG](/index.php/GnuPG "GnuPG") keys, so KDE Wallet must use the standard blowfish encryption. Also, the wallet name must be "kdewallet" (that's the default name). If, for some reason, you create a new wallet, you need to use this name (so you will probably need to rename the old wallet too).

## Using the KDE Wallet to store ssh keys

First, make sure that you have an [SSH agent](/index.php/SSH_agent "SSH agent") running.

[Install](/index.php/Install "Install") the [ksshaskpass](https://www.archlinux.org/packages/?name=ksshaskpass) package.

[Create](/index.php/Create "Create") an autostart file and mark it executable with [chmod](/index.php/Chmod "Chmod"):

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

You also have to set the `SSH_ASKPASS` environment variable in your /etc/profile or ~/.bash_profile:

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

There is an addon to make Firefox store passwords with [KDE5 Wallet](https://addons.mozilla.org/addon/kde5-wallet-password-integrati/).

## KDE Wallet for Chrome and Chromium

Chrome/Chromium has built in wallet integration. To enable it, run Chromium with the `--password-store=kwallet` or `--password-store=detect` argument. To make the change persistent, see [Chromium/Tips and tricks#Making_flags_persistent](/index.php/Chromium/Tips_and_tricks#Making_flags_persistent "Chromium/Tips and tricks"). (Setting CHROMIUM_USER_FLAGS will not work.)

## See also

*   [Unlocking KWallet with PAM](https://www.dennogumi.org/2014/04/unlocking-kwallet-with-pam/)