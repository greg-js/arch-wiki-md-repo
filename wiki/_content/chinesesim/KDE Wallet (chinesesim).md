**翻译状态：** 本文是英文页面 [KDE Wallet](/index.php/KDE_Wallet "KDE Wallet") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-4-11，点击[这里](https://wiki.archlinux.org/index.php?title=KDE+Wallet&diff=0&oldid=568128)可以查看翻译后英文页面的改动。

[KDE Wallet Manager](http://utils.kde.org/projects/kwalletmanager/) 是一个用于管理 [KDE](/index.php/KDE "KDE") Plasma 上的密码的工具。KWallet子系统提供了访问和管理兼容KWallet的应用所保存的密码的功能，同时你也可以用它来保存你自己的密码。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 在登录时自动解锁 Kwallet](#在登录时自动解锁_Kwallet)
    *   [1.1 配置 display manager](#配置_display_manager)
*   [2 使用 KDE Wallet 存储 ssh key passphrases](#使用_KDE_Wallet_存储_ssh_key_passphrases)
*   [3 Firefox 上的 KDE Wallet 支持](#Firefox_上的_KDE_Wallet_支持)
*   [4 Chrome 和 Chromium 的 KDE Wallet 支持](#Chrome_和_Chromium_的_KDE_Wallet_支持)
*   [5 See also](#See_also)

## 在登录时自动解锁 Kwallet

**Note:**

*   [kwallet-pam](https://www.archlinux.org/packages/?name=kwallet-pam) 与 [GnuPG](/index.php/GnuPG "GnuPG") keys 不兼容，所以 KDE Wallet 必须使用 `blowfish` 加密方式。
*   所选择的 KWallet 密码必须与当前 [用户](/index.php/User "User") 的密码相同。
*   KWallet 在账户使用自动登录的时候不会自动解锁。
*   要自动解锁的 wallet 必须要命名为 `kdewallet` (这是默认的名字)。任何其他名字的 wallet 都不会自动解锁。
*   如果桌面环境用的是 [KDE](/index.php/KDE "KDE"), 建议关闭 KDE Wallet settings 里的 *Close when last application stops using it* 选项来防止 wallet 在每次被使用（比如获取[WiFi](/index.php/WiFi "WiFi")密码）之后被关闭。
*   可能需要先把默认创建的 wallet 删除——即删除所有已经储存的密码条目。
*   如果 kwallet Migration Assistant在每次登录之后都要求输入密码，请重命名或删除 `~/.kde4/share/apps/kwallet` 文件夹.

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [kwallet-pam](https://www.archlinux.org/packages/?name=kwallet-pam) 包来提供对 [PAM](/index.php/PAM "PAM") 的兼容模块。

选择性 [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [kwalletmanager](https://www.archlinux.org/packages/?name=kwalletmanager) 来使用 KWallet 管理工具。这个工具可以用于建立一个 `blowfish` 加密的KDE Wallet，同时提供了 *kcm-module* 没有提供的其他设置。

**Tip:** 替代选项是使用 KWalletManager 然后设置一个空的 Kwallet 密码, 这样就可以避免需要输入密码来解锁 wallet。只要在 *Change Password..* 的时候把两个框都留空就可以了。但是这样的话无法阻止对 wallet 的未授权访问。 因此非常建议打开 *Access Control* 里的 *Prompt when an application accesses a wallet* 选项来避免未授权访问。

### 配置 display manager

下面的几行必须存在于你使用的 Display Manager 的配置文件里：

```
auth            optional        pam_kwallet5.so
session         optional        pam_kwallet5.so auto_start
```

常见的 [display manager](/index.php/Display_manager "Display manager") 所需要修改的文件如下：

*   [SDDM](/index.php/SDDM "SDDM")：不需要进行修改，因为 `/etc/pam.d/sddm` 里已经写好了。
*   [GDM](/index.php/GDM "GDM")： 修改 `/etc/pam.d/gdm-password`。
*   [LightDM](/index.php/LightDM "LightDM")： 修改 `/etc/pam.d/lightdm` 和 `/etc/pam.d/lightdm-greeter`：

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

## 使用 KDE Wallet 存储 ssh key passphrases

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [ksshaskpass](https://www.archlinux.org/packages/?name=ksshaskpass)。

[创建](/index.php/Create "Create") 一个 [autostart script file](/index.php/KDE#Autostart "KDE") 并把它标记为 [executable](/index.php/Executable "Executable"):

 `~/.config/autostart-scripts/ssh-add.sh` 
```
#!/bin/sh
ssh-add </dev/null

```

**Tip:** 上面这个 ssh-add.sh 脚本只会添加默认的 `~/.ssh/id_rsa` key。如果你在 `~/.ssh/` 下有多个SSH key，假设分别是 `key1`, `key2`, `key3`，你需要像下面这样修改脚本来自动添加它们： `~/.config/autostart-scripts/ssh-add.sh` 
```
#!/bin/sh
ssh-add $HOME/.ssh/key1 $HOME/.ssh/key2 $HOME/.ssh/key3 </dev/null

```

你需要设置[环境变量](/index.php/Environment_variable "Environment variable") `SSH_ASKPASS` 为 `ksshaskpass`：

```
export SSH_ASKPASS="/usr/bin/ksshaskpass"

```

它会要你输入密码来解锁 SSH keys。在重启之后，输入kwallet密码之后 SSH keys 就会被解锁。

如果要添加一个新的 key 并把密码储存在 kwallet里，使用这个命令：

```
$ ssh-add */path/to/new/key* </dev/null

```

并把这个 key 按照上面所说的方法添加到 `~/.config/autostart-scripts/ssh-add.sh` 的 keys 列表里。

## Firefox 上的 KDE Wallet 支持

**Note:** Firefox 57 及更新版本上这个 addon 已经失效了。如果你还想用它，请使用 [firefox-esr52](https://aur.archlinux.org/packages/firefox-esr52/) (生命周期支持到 2018 八月)。

一个非官方的[Firefox](/index.php/Firefox "Firefox") addon [KDE5 Wallet](https://addons.mozilla.org/addon/kde5-wallet-password-integrati/) 提供集成支持。

## Chrome 和 Chromium 的 KDE Wallet 支持

Chrome/Chromium 内置了 wallet 支持。在运行 Chromium 的时候加上 `--password-store=kwallet` 或者 `--password-store=detect` 参数来启用它。如果需要永久启用这个参数，参考 [Chromium/Tips and tricks#Making flags persistent](/index.php/Chromium/Tips_and_tricks#Making_flags_persistent "Chromium/Tips and tricks")。(设置 CHROMIUM_USER_FLAGS 是无效的。)

## See also

*   [Unlocking KWallet with PAM](https://www.dennogumi.org/2014/04/unlocking-kwallet-with-pam/)