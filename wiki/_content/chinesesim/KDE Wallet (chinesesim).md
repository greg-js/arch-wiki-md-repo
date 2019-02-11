**翻译状态：** 本文是英文页面 [KDE Wallet](/index.php/KDE_Wallet "KDE Wallet") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-18，点击[这里](https://wiki.archlinux.org/index.php?title=KDE+Wallet&diff=0&oldid=492606)可以查看翻译后英文页面的改动。

[KDE Wallet Manager](http://utils.kde.org/projects/kwalletmanager/) 是一个用于管理 KDE Plasma 上密码的工具。它将用于在 KDE 上访问和管理你的密码

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 在登录时自动解锁 Kwallet](#在登录时自动解锁_Kwallet)
*   [2 使用 KDE Wallet 存储 ssh keys](#使用_KDE_Wallet_存储_ssh_keys)
*   [3 KDE Wallet for Firefox](#KDE_Wallet_for_Firefox)
*   [4 KDE Wallet for Chrome and Chromium](#KDE_Wallet_for_Chrome_and_Chromium)
*   [5 See also](#See_also)

## 在登录时自动解锁 Kwallet

如果您的 KWallet 密码与您的用户名密码相同，您可以在登录时自动解锁您的 KWallet。

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [kwallet-pam](https://www.archlinux.org/packages/?name=kwallet-pam) 包，

如果没有使用 [SDDM](/index.php/SDDM "SDDM") 登陆管理器，需要编辑您的登录管理器 pam (通常位于 `/etc/pam.d` ) 文件，并在其相应部分下添加:

```
auth            optional        pam_kwallet5.so
session         optional        pam_kwallet5.so auto_start
```

例如 [LightDM](/index.php/LightDM "LightDM") 需要修改 `/etc/pam.d/lightdm` 和 `/etc/pam.d/lightdm-greeter` 文件:

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

如果是 [GDM](/index.php/GDM "GDM"),编辑`/etc/pam.d/gdm-password`。重新启动后，如果您的用户密码与 KWallet 密码相同，您的 KWallet 将自动解锁。

**Note:** Currently, kwallet-pam has at least two limitations: first, it's not compatible with [GnuPG](/index.php/GnuPG "GnuPG") keys, so KDE Wallet must use the standard blowfish encryption. Also, the wallet name must be "kdewallet" (that's the default name). If, for some reason, you create a new wallet, you need to use this name (so you will probably need to rename the old wallet too).

## 使用 KDE Wallet 存储 ssh keys

首先, 你要确保你正在运行一个 [SSH agent](/index.php/SSH_agent "SSH agent")

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

There is an addon to make Firefox store passwords with [KDE5 Wallet](https://addons.mozilla.org/addon/kde5-wallet-password-integrati/).

## KDE Wallet for Chrome and Chromium

Chrome/Chromium has built in wallet integration. To enable it, run Chromium with the `--password-store=kwallet` or `--password-store=detect` argument. To make the change persistent, see [Chromium/Tips and tricks#Making flags persistent](/index.php/Chromium/Tips_and_tricks#Making_flags_persistent "Chromium/Tips and tricks"). (Setting CHROMIUM_USER_FLAGS will not work.)

## See also

*   [Unlocking KWallet with PAM](https://www.dennogumi.org/2014/04/unlocking-kwallet-with-pam/)