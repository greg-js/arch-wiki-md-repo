**翻译状态：** 本文是英文页面 [Dropbox](/index.php/Dropbox "Dropbox") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-12-16，点击[这里](https://wiki.archlinux.org/index.php?title=Dropbox&diff=0&oldid=349226)可以查看翻译后英文页面的改动。

[Dropbox](https://www.dropbox.com) is a file sharing system that recently introduced a GNU/Linux client. Use it to transparently sync files across computers and architectures. Simply drop files into your `~/Dropbox` folder, and they will automatically sync to your centralized repository.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 AUR](#AUR)
    *   [1.2 手动安装](#.E6.89.8B.E5.8A.A8.E5.AE.89.E8.A3.85)
    *   [1.3 可选软件包](#.E5.8F.AF.E9.80.89.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [2 启动](#.E5.90.AF.E5.8A.A8)
    *   [2.1 自动启动 Dropbox](#.E8.87.AA.E5.8A.A8.E5.90.AF.E5.8A.A8_Dropbox)
    *   [2.2 作为 systemd 的服务启动](#.E4.BD.9C.E4.B8.BA_systemd_.E7.9A.84.E6.9C.8D.E5.8A.A1.E5.90.AF.E5.8A.A8)
        *   [2.2.1 Run as a daemon with systemd user](#Run_as_a_daemon_with_systemd_user)
*   [3 不安装 Dropbox 而访问文件](#.E4.B8.8D.E5.AE.89.E8.A3.85_Dropbox_.E8.80.8C.E8.AE.BF.E9.97.AE.E6.96.87.E4.BB.B6)
*   [4 Securing your Dropbox](#Securing_your_Dropbox)
    *   [4.1 Setup EncFS with Dropbox](#Setup_EncFS_with_Dropbox)
*   [5 Multiple Dropbox instances](#Multiple_Dropbox_instances)
*   [6 Dropbox on laptops](#Dropbox_on_laptops)
    *   [6.1 Using netctl](#Using_netctl)
    *   [6.2 Using NetworkManager](#Using_NetworkManager)
    *   [6.3 Using wicd](#Using_wicd)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Dropbox keeps saying Downloading files](#Dropbox_keeps_saying_Downloading_files)
    *   [7.2 Change the Dropbox location from the installation wizard](#Change_the_Dropbox_location_from_the_installation_wizard)
    *   [7.3 Context menu entries in file manager do not work](#Context_menu_entries_in_file_manager_do_not_work)
    *   [7.4 Connecting...](#Connecting...)
    *   [7.5 Dropbox does not start - "This is usually because of a permission error"](#Dropbox_does_not_start_-_.22This_is_usually_because_of_a_permission_error.22)
        *   [7.5.1 Check permissions](#Check_permissions)
        *   [7.5.2 Re-linking your account](#Re-linking_your_account)
        *   [7.5.3 Errors caused by running out of space](#Errors_caused_by_running_out_of_space)
        *   [7.5.4 Locale caused errors](#Locale_caused_errors)
        *   [7.5.5 Filesystem monitoring problem](#Filesystem_monitoring_problem)
    *   [7.6 代理设置](#.E4.BB.A3.E7.90.86.E8.AE.BE.E7.BD.AE)
    *   [7.7 不要让它自动升级](#.E4.B8.8D.E8.A6.81.E8.AE.A9.E5.AE.83.E8.87.AA.E5.8A.A8.E5.8D.87.E7.BA.A7)

## 安装

### AUR

您可以从 [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 安装 [dropbox](https://aur.archlinux.org/packages/dropbox/) 。或者, 也可以安装 [dropbox-experimental](https://aur.archlinux.org/packages/dropbox-experimental/)。

**Note:** 如果 PKGBUILD 已经过时，你可以在下载后更新它，或者在 [AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 页面标记其为过期。

1.  安装完毕，您就可以从程序菜单中的图标或者是在命令行中输入 `dropboxd` 启动 Dropbox。 您将会在系统托盘中看到程序的图标。
2.  Dropbox 也许会有弹窗提示（此程序非官网下载等等），你知道这个程序是从 AUR 下载安装的就好啦，然后你可以放心大胆的点击“Don't ask again”来忽视这个提示。
3.  然后会看到一个要求您输入账户信息的窗口，您可以输入已有账户或者是新建一个账户。
4.  再然后您会看到 Dropbox 的欢迎页面，此处将会有一个关于如何使用 Dropbox 的简短的介绍。
5.  点击 "Finish and go to My Dropbox"。

### 手动安装

以下的内容将介绍 [从命令行下手动安装 Dropbox](https://www.dropbox.com/install)。以 64 位系统为例，运行：

```
$ cd ~
$ wget -O - "[https://www.dropbox.com/download?plat=lnx.x86_64](https://www.dropbox.com/download?plat=lnx.x86_64)" | tar xzf -

```

然后，启动 Dropbox：

```
$ ~/.dropbox-dist/dropboxd

```

### 可选软件包

*   纯命令行界面，从 [AUR](/index.php/AUR "AUR") 安装 [dropbox-cli](https://aur.archlinux.org/packages/dropbox-cli/)。
*   GNOME 集成，从 [AUR](/index.php/AUR "AUR") 安装 [nautilus-dropbox](https://aur.archlinux.org/packages/nautilus-dropbox/)，此插件将会自动启动 Dropbox。
*   Nemo 集成，从 [AUR](/index.php/AUR "AUR") 安装 [nemo-dropbox-git](https://aur.archlinux.org/packages/nemo-dropbox-git/)。
*   [Thunar](/index.php/Thunar "Thunar") 集成, 从 [AUR](/index.php/AUR "AUR") 安装 [thunar-dropbox](https://aur.archlinux.org/packages/thunar-dropbox/)。
*   对于 [KDE](/index.php/KDE "KDE") 用户，也可以在 [AUR](/index.php/AUR "AUR") 中找到 KDE 下的应用：[kfilebox](https://aur.archlinux.org/packages/kfilebox/)。

## 启动

### 自动启动 Dropbox

对于 [KDE](/index.php/KDE "KDE") 用户来说，在注销用户或者是重启机器后，之前正在运行的程序将会自动重新启动。[Xfce](/index.php/Xfce "Xfce") 稍有不同，将 `dropbox.desktop` 放置在 {ic|~/.config/autostart}} 下，Dropbox 在下次启动时就会自动启动了。

如果这些都不能正常的工作，那您也可以将 `~/.dropbox-dist/dropboxd &` 添加到 `~/.xinitrc` 来让窗口管理器控制它的启动（也有可能在 `~/.config/openbox/autostart`,看你的设置了）。当然，您也可以将 Dropbox [作为服务启动](#Run_as_daemon_with_systemd).

### 作为 systemd 的服务启动

当前的 Dropbox 版本已经包含了 systemd 服务文件。默认的 systemd 服务文件并不能在系统托盘中显示软件的图标，但是依旧在后台默默的为您同步您的文件。如果您需要托盘图标支持，那么建立 `/etc/systemd/system/dropbox@.service` ，修改环境变量 `DISPLAY` 后替换默认的 systemd 服务文件：

 `/etc/systemd/system/dropbox@.service` 

```
.include /usr/lib/systemd/system/dropbox@.service
[Service]
Environment=DISPLAY=:0

```

最后，启动此服务，在登录时 Dropbox 将能够自动运行：

```
# systemctl enable dropbox@<user>

```

Note that you have to manually start Dropbox the first time after installation, so that it runs through the login and setup screen. Further, you need to uncheck the option **Start Dropbox on system startup** in order to prevent Dropbox from being started twice. The daemon can then be used subsequently.

#### Run as a daemon with systemd user

If you have followed the [systemd/User](/index.php/Systemd/User "Systemd/User") wiki page, you probably want to start dropbox only when you log in or launch your WM/DE. The solution in that case is to create a service in your home directory instead of using the sysadmin account:

 `$HOME/.config/systemd/user/dropbox@.service` 

```
[Unit]
Description=Dropbox as a systemd service
After=xorg.target

[Service]
ExecStart=/home/<user>/.dropbox-dist/dropboxd
ExecReload=/bin/kill -HUP $MAINPID
Environment=DISPLAY=%i

[Install]
WantedBy=default.target

```

Then you can start or enable it with:

```
$ systemctl --user {start|enable} dropbox@:0.service

```

That way you can easily start it in your main display (likely :0) or in another one, without having to hard code it.

**Note:** After a lot of trial and error I found that using `/usr/bin/dropboxd` didn't start the service and it didn't show any error either (even when running it directly from the terminal worked fine). I believe it has to do that starting it that way systemd doesn't know which user is actually running the daemon.

## 不安装 Dropbox 而访问文件

如果您仅需要基本的访问文件的功能，那么您可以访问 [https://www.dropbox.com/](https://www.dropbox.com/) 来上传或者是下载您的文件。此方法不需要安装 Dropbox 。

另外，您也可以尝试从 [AUR](/index.php/AUR "AUR") 安装 [droxi](https://aur.archlinux.org/packages/droxi/) ，此终端工具提供了类似于 GNU `ftp` 客户端的功能。

## Securing your Dropbox

If you want to store sensitive data in your Dropbox, you should encrypt it before. Syncing to Dropbox is encrypted, but all files are (for the time being) stored on the server unencrypted just as you put them in your Dropbox.

*   Dropbox works with [TrueCrypt](/index.php/TrueCrypt "TrueCrypt"), and after you initially uploaded the TrueCrypt volume to Dropbox, performance is quite okay, because Dropbox has a working binary diff.

*   Another possibility is to use [EncFS](/index.php/EncFS "EncFS"), which has the advantage that all files are encrypted separately, i.e. you do not have to determine in advance the size of the content you want to encrypt and your encrypted directory grows and shrinks while you add/delete/modify files in it. You can also mount an encrypted volume at startup using the `-S` option of `encfs` to avoid having to input the passphrase, but note that your encrypted files are not secure from someone who has direct access to your computer.

### Setup EncFS with Dropbox

Follow the Wiki instructions to install [EncFS](/index.php/EncFS "EncFS").

Assuming you have set your Dropbox directory as `~/Dropbox`:

Create a folder. Files you want synced to Dropbox will go in here.

```
$ mkdir ~/Private

```

Run the following and enter a password when asked:

```
$ encfs ~/Dropbox/Encrypted ~/Private

```

Your secure folder is ready for use; creating any file inside `~/Private` will automatically encrypt it into `~/Dropbox/Encrypted`, which will then be synced to your cloud storage.

To mount your EncFS folder on every boot, follow the instructions in the [EncFS](/index.php/EncFS#User_friendly_mounting "EncFS") wiki page.

**Tip:** Consider using the `ENCFS6_CONFIG` variable and moving the `.encfs6.xml` file to another location (like a USB stick), to help ensure that your encrypted data and the means to realistically decrypt it do not exist together online.

## Multiple Dropbox instances

If you need to separate or distinguish your data, personal and work usage for example, you can subscribe to Dropbox with different email addresses and have their directories synced by different Dropbox instances running on a single machine.

The basic principle and general how-to are described in the [Dropbox Wiki](http://www.dropboxwiki.com/Multiple_Instances_On_Unix).

To summarize, you can setup new or additional instances with:

```
mkdir /path/to/.dropbox-alt-1
HOME=/path/to/.dropbox-alt-1 /usr/bin/dropbox start -i

```

Once that is done, stop any Dropbox instance still running and start them like this:

```
HOME=/path/to/.dropbox-alt-1 /path/to/.dropbox-alt-1/.dropbox-dist/dropboxd
HOME=/path/to/.dropbox-alt-2 /path/to/.dropbox-alt-2/.dropbox-dist/dropboxd

```

Pay attention to use different `.../.dropbox-dist/dropboxd` binaries. Even when setting a custom HOME value, the `/opt/dropbox/dropbox` or `/opt/dropbox/dropboxd` wrappers allow only one instance and when started they will kill the one already running.

## Dropbox on laptops

Dropbox itself is pretty good at dealing with connectivity problems. If you have a laptop and roam between different network environments, Dropbox will have problems reconnecting if you do not restart it. **Try one of the methods described below first,** if for some reason the problem remains, you may try one of these hackish solutions: [[1]](https://bbs.archlinux.org/viewtopic.php?pid=790905), [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1012343#p1012343).

**Note:** When using any of these methods, you need to prevent Dropbox from doing a standard autostart by unchecking _Dropbox - Preferences - General - Start Dropbox on system startup_. This prevents Dropbox from creating the `~/.config/autostart/dropbox.desktop` file and thus from starting twice.

### Using netctl

For [netctl](/index.php/Netctl "Netctl"), use `ExecUpPost` and `ExecDownPre` respectively in every network profile you use, or for example in `/etc/netctl/interfaces/wlan0` to start Dropbox automatically whenever profile on `wlan0` is active. Add '|| true' to your command to make sure [netctl](/index.php/Netctl "Netctl") will bring up your profile, although Dropbox fails to start.

```
ExecUpPost="_any other code_; su -c 'DISPLAY=:0 /usr/bin/dropboxd &' _your_user_ || true"
ExecDownPre="_any other code_; killall dropbox"

```

Obviously, `_your_user_` has to be edited and `_any other code_;` can be omitted if you do not have any. The above will make sure that Dropbox is running only if there is a network profile active.

### Using NetworkManager

If you have connectivity problem with [NetworkManager](/index.php/NetworkManager "NetworkManager"), try using a [dispatcher script](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager"): [networkmanager-dispatcher-dropbox](https://aur.archlinux.org/packages/networkmanager-dispatcher-dropbox/) or [networkmanager-dispatcher-dropbox-systemd](https://aur.archlinux.org/packages/networkmanager-dispatcher-dropbox-systemd/).

### Using wicd

Create /etc/wicd/scripts/postconnect/dropbox:

```
#!/usr/bin/env bash
su -c 'DISPLAY=:0 /usr/bin/dbus-launch dropboxd &' your_username

```

or, if you use dropbox with systemd:

```
#!/usr/bin/env bash
systemctl restart dropbox@<user>

```

Create /etc/wicd/scripts/postdisconnect/dropbox:

```
#!/usr/bin/env bash
killall dropbox

```

or, if you use dropbox with systemd:

```
#!/usr/bin/env bash
systemctl stop dropbox@<user>

```

**Note:** If you use PCManFM as your file manager, Dropbox will use 'xdg-open' calls pcmanfm to open the Dropbox folder.However, without a dbus session, you can not use Trash in PCManFM. You should refer to [Dbus](/index.php/Dbus "Dbus") and [General troubleshooting#Session permissionsto](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") edit your ~/.xinitrc based on /etc/skel/.xinitrc to start a D-Bus session before your launch any other program in ~/.xinitrc. Do use 'dbus-launch dropboxd' instead of just 'dropboxd' in wicd postconnect script. otherwise pcmanfm launched by clicking dropbox icon can not use the Trash.

## Troubleshooting

### Dropbox keeps saying Downloading files

But in fact now files are synced with your box. This problem is likely to appear when your Dropbox folder is located on a NTFS partition whose mount path contains spaces, or permissions are not set for that partition. See more in the [[forums](https://bbs.archlinux.org/viewtopic.php?id=153368)]. To resolve the problem pay attention to your entry in `/etc/fstab`. Avoid spaces in the mount path and set write permissions with the "default_permissions" option:

```
UUID=01CD2ABB65E17DE0 /run/media/username/Windows ntfs-3g uid=username,gid=users,default_permissions 0 0

```

### Change the Dropbox location from the installation wizard

Some users experience the problem during setting-up Dropbox that they cannot select a Dropbox folder other than `/home/username/Dropbox`. In this case when the window for changing the path is shown , hit `Ctrl+l`, enter the location (e.g. /mnt/data/Dropbox) and click on the '"Choose" or "Open" button.

### Context menu entries in file manager do not work

Several file managers such as Thunar, GNOME Files or its fork Nemo come with extensions that provide context menu entries for files and folders inside your Dropbox. Most of them will result in a browser action such as opening the file or folder in dropbox.com or sharing the link. If you experience these entries not working, then it is likely you have not set the `$BROWSER` variable which Dropbox requires. See [Environment variables](/index.php/Environment_variables "Environment variables") for details.

### Connecting...

It may happen that Dropbox cannot connect successfully because it was loaded before an internet connection was established. This can happen on wireless connections, or fast loading machines on wired networks. The best solution to this problem, for wired and wireless connections, is [#Dropbox on laptops](#Dropbox_on_laptops) which will ensure that Dropbox is started only after the connection is established.

An alternative solution, for those not using netctl or NetworkManager, is to delay the startup of dropbox:

*   `cp ~/.config/autostart/dropbox.desktop ~/.config/autostart/dropbox-delayed.desktop`
*   Prevent dropbox from doing a standard autostart by unchecking Dropbox - Preferences - General - Start Dropbox on system startup. This removes `~/.config/autostart/dropbox.desktop`.
*   Edit `~/.config/autostart/dropbox-delayed.desktop` and replace `Exec=dropboxd` with `Exec=bash -c "sleep _timeout_ && dropboxd"`. Tweak the _timeout_ parameter, the value of `3` is a good start.

### Dropbox does not start - "This is usually because of a permission error"

#### Check permissions

Make sure that you own Dropbox's directories before running the application. This includes

*   `~/.dropbox` - Dropbox's configuration directory
*   `~/Dropbox` - Dropbox's download directory (default)

You can ensure this by changing their owner with `chown -R`.

This error could also be caused by `/var` being full.

#### Re-linking your account

[Dropbox's FAQ](https://www.dropbox.com/help/72) suggests that this error may be caused by misconfiguration and is fixed by (re)moving the current configuration folder

```
# mv ~/.dropbox ~/.dropbox.old

```

and restarting Dropbox.

#### Errors caused by running out of space

A common error that might happen is that there is no more available space on your `/tmp` and `/var` partitions. If this happens, Dropbox will crash on startup with the following error in its log:

```
Exception: Not a valid FileCache file

```

A detailed story of such an occurrence can be found in the [forums](https://bbs.archlinux.org/viewtopic.php?pid=973458). Make sure there is enough space available before launching Dropbox.

Another case is when the root partition is full:

```
OperationalError: database or disk is full

```

Check to see the available space on partitions with `df`.

#### Locale caused errors

Try starting `dropboxd` with this code:

```
LANG=$LOCALE
dropboxd

```

(You can also use a different value for LANG; it must be in the format "en_US.UTF-8") This helps when running from a Bash script or Bash shell where `/etc/rc.d/functions` has been loaded

#### Filesystem monitoring problem

If you have a lot of files to sync in your Dropbox folder, you might get the following error:

```
Unable to monitor filesystem
Please run: echo 100000 | sudo tee /proc/sys/fs/inotify/max_user_watches and restart Dropbox to correct the problem.

```

This can be fixed easily by adding

```
fs.inotify.max_user_watches = 100000

```

to `/etc/sysctl.d/99-sysctl.conf` and then reload the kernel parameters

```
# sysctl --system

```

### 代理设置

最简单的方法是在 Dropbox 的首选项页面设置代理。另外也可以设置为自动选择代理，它将会读取 http_proxy 的变量而使用合适的代理。

 `env http_proxy=http://your.proxy.here:port /usr/bin/dropboxd` 

或者

```
export http_proxy=http://your.proxy.here:port
/usr/bin/dropboxd

```

**Note:** Dropbox 仅支持此形式的 `http://your.proxy.here:port` 代理表示方法， 此表示方法不被支持 `your.proxy.here:port`（大部分程序都不支持此方法） 。

### 不要让它自动升级

```
rm -rf ~/.dropbox-dist
install -dm0 ~/.dropbox-dist

```