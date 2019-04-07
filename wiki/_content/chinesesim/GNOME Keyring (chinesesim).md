**翻译状态：** 本文是英文页面 [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-01-31，点击[这里](https://wiki.archlinux.org/index.php?title=GNOME+Keyring&diff=0&oldid=565099)可以查看翻译后英文页面的改动。

[GNOME Keyring](https://wiki.gnome.org/Projects/GnomeKeyring) is "a collection of components in GNOME that store secrets, passwords, keys, certificates and make them available to applications."

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 用GUI管理](#用GUI管理)
*   [3 在GNOME外部使用钥匙环](#在GNOME外部使用钥匙环)
    *   [3.1 没有可视化管理软件的情况下](#没有可视化管理软件的情况下)
        *   [3.1.1 自动登陆](#自动登陆)
        *   [3.1.2 控制台登陆](#控制台登陆)
            *   [3.1.2.1 用PAM的方法](#用PAM的方法)
            *   [3.1.2.2 用xinitrc的方法](#用xinitrc的方法)
    *   [3.2 有可视化管理软件的情况下](#有可视化管理软件的情况下)
*   [4 SSH钥匙](#SSH钥匙)
    *   [4.1 Start SSH and Secrets components of keyring daemon](#Start_SSH_and_Secrets_components_of_keyring_daemon)
    *   [4.2 禁止钥匙环的守护进程组件](#禁止钥匙环的守护进程组件)
*   [5 提示与小技巧](#提示与小技巧)
    *   [5.1 软件中的插件](#软件中的插件)
    *   [5.2 去除密码](#去除密码)
    *   [5.3 Git的插件](#Git的插件)
    *   [5.4 GnuPG的插件](#GnuPG的插件)
*   [6 故障排除](#故障排除)
    *   [6.1 密码没被记住](#密码没被记住)
    *   [6.2 重置钥匙环](#重置钥匙环)
*   [7 参见](#参见)

## 安装

如果使用的是GNOME, [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) 作为 [gnome](https://www.archlinux.org/groups/x86_64/gnome/) 组的一个包自动安装。在其他情况下，请[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring) 包。安装[libsecret](https://www.archlinux.org/packages/?name=libsecret)来让应用程序使用 keyrings。不推荐安装[libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring)，除非有一些应用程序一定要用它。

与GNOME keyring相关的其他工具包括：

*   **secret-tool** — 通过命令行访问GNOME keyring (以及其他任何实现了[DBus Secret Service API](http://standards.freedesktop.org/secret-service/)的服务) 。

	[https://wiki.gnome.org/Projects/Libsecret](https://wiki.gnome.org/Projects/Libsecret) || [libsecret](https://www.archlinux.org/packages/?name=libsecret)

*   **gnome-keyring-query** — 提供一个用于从GNOME Keyring的密码库查询密码的命令行工具， 但是用的是不推荐的[libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring)包。

	|| [gnome-keyring-query](https://aur.archlinux.org/packages/gnome-keyring-query/)

*   **gkeyring** — 从命令行查询密码，用的是不推荐的[libgnome-keyring](https://www.archlinux.org/packages/?name=libgnome-keyring)包。

	[https://github.com/kparal/gkeyring](https://github.com/kparal/gkeyring) || [gkeyring](https://aur.archlinux.org/packages/gkeyring/), [gkeyring-git](https://aur.archlinux.org/packages/gkeyring-git/)

## 用GUI管理

你可以通过Seahorse来管理GNOME Keyring的内容。[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [seahorse](https://www.archlinux.org/packages/?name=seahorse) 包。

留空或者更改GNOME keyring的密码是允许的。在seahorse里，在 "View" 下拉菜单里，选择 "By Keyring"。在Passwords标签页里，右键单击 "Passwords: login" 然后选择 "Change password." 输入旧密码然后留空新密码，你会收到警告说正在使用未加密的储存方式，如果确定请点击"Use Unsafe Storage."

## 在GNOME外部使用钥匙环

### 没有可视化管理软件的情况下

#### 自动登陆

If you are using automatic login, then you can disable the keyring manager by setting a blank password on the login keyring.

**Note:** The passwords are stored unencrypted in this case.

#### 控制台登陆

When using console-based login, the keyring daemon can be started by either [PAM](/index.php/PAM "PAM") or [xinitrc](/index.php/Xinitrc "Xinitrc"). PAM can also unlock the keyring automatically at login.

##### 用PAM的方法

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

##### 用xinitrc的方法

Start the gnome-keyring-daemon from [xinitrc](/index.php/Xinitrc "Xinitrc"):

 `~/.xinitrc` 
```
eval $(/usr/bin/gnome-keyring-daemon --start --components=pkcs11,secrets,ssh)
export SSH_AUTH_SOCK

```

See [Xfce#SSH agents](/index.php/Xfce#SSH_agents "Xfce") for use in Xfce.

If using [i3](/index.php/I3 "I3") and ssh is not showing the password prompt, giving the following error:

```
sign_and_send_pubkey: signing failed: agent refused operation
Permission denied (publickey).

```

then you need to add the DISPLAY environment variable to dbus-daemon via the .xinitrc:

 `~/.xinitrc` 
```
dbus-update-activation-environment --systemd DISPLAY
eval $(/usr/bin/gnome-keyring-daemon --start --components=pkcs11,secrets,ssh)
export SSH_AUTH_SOCK

...
exec i3

```

**Note:** If you use a different location for `~/.Xauthority` (`XAUTHORITY`) then you will have to also include this environment variable in the aforementioned `dbus-update-activation-environment` command.

### 有可视化管理软件的情况下

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

## SSH钥匙

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

### 禁止钥匙环的守护进程组件

If you wish to run an alternative SSH agent (e.g. [ssh-agent](/index.php/SSH_keys#ssh-agent "SSH keys") or [gpg-agent](/index.php/GnuPG#gpg-agent "GnuPG"), you need to disable the `ssh` component of GNOME Keyring. To do so in an account-local way, copy `/etc/xdg/autostart/gnome-keyring-ssh.desktop` to `~/.config/autostart` and then append the line `Hidden=true` to the copied file. Then log out.

**Note:** In case you use [GNOME](/index.php/GNOME "GNOME") 3.24 or older on [Wayland](/index.php/Wayland "Wayland"), gnome-shell will overwrite `SSH_AUTH_SOCK` to point to gnome-keyring regardless if it is running or not. To prevent this, you need to set the environment variable GSM_SKIP_SSH_AGENT_WORKAROUND before gnome-shell is started. One way to do this is to add the line `GSM_SKIP_SSH_AGENT_WORKAROUND DEFAULT=1` to `~/.pam_environment`.

## 提示与小技巧

### 软件中的插件

*   [Firefox](/index.php/Firefox#KDE.2FGNOME_integration "Firefox")

### 去除密码

```
gnome-keyring-daemon -r -d

```

This command starts gnome-keyring-daemon, shutting down previously running instances.

### Git的插件

The GNOME keyring is useful in conjuction with [Git](/index.php/Git "Git") when you are pushing over HTTPS.

[Install](/index.php/Install "Install") the [libsecret](https://www.archlinux.org/packages/?name=libsecret) package.

Set Git up to use the helper:

```
$ git config --global credential.helper /usr/lib/git-core/git-credential-libsecret

```

Next time you do a *git push*, you are asked to unlock your keyring, if not unlocked already.

### GnuPG的插件

Several applications which use GnuPG require a `pinentry-program` to be set. Set the following to use Gnome 3 pinentry for Gnome Keyring to manage passphrase prompts.

 `~/.gnupg/gpg-agent.conf` 
```
pinentry-program /usr/bin/pinentry-gnome3

```

Another option is to [force loopback for GPG](/index.php/GnuPG#Unattended_passphrase "GnuPG") which should allow the passphrase to be entered in the application.

## 故障排除

### 密码没被记住

如果你每次登陆的时候都收到密码提示框，并且你发现你的密码没有被自动保持你可能需要创建或设置一个默认钥匙环

确保 [seahorse](https://www.archlinux.org/packages/?name=seahorse) 包已经 [安装](/index.php/%E5%AE%89%E8%A3%85 "安装")了, 打开它 (系统设置中的"密码和密钥") 并且选中“视图” > “根据钥匙环”。 如果在左边的一竖排中没看到钥匙环 (一个锁一样的图标)， 打开“文件” > “新建” > “密码钥匙环”，然后取一个名字，你可能会被要求输入一个密码。如果你没有给钥匙环密码，钥匙环将会自动解锁，即使使用自动登陆，密码也不会被安全保存。最后，右键你创建的钥匙环并选择“设为默认”。

### 重置钥匙环

If you get the error "The password you use to login to your computer no longer matches that of your login keyring", you can simply reset your gnome keyring.

Remove "login.keyring" and "user.keystore" from */home/{username}/.local/share/keyrings/*. After removing the files, simply log out and log in again. Obviously, this will remove your saved keys.

## 参见

*   [GNOME wiki](https://wiki.gnome.org/action/show/Projects/GnomeKeyring)