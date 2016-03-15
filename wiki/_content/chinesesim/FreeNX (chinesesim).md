*NX 是一项令人激动的远程控制技术。它提供了在高延迟、低带宽环境中 *<u>接近本地速度</u> *的应用程序响应链接。NX 的核心库由 [NoMachine](http://www.nomachine.com/) 在 GPL 授权下提供。**FreeNX** 是一个 NX 服务器和客户端组件的 GPL 实现。*

	— [FreeNX - 自由的 NX](http://freenx.berlios.de/)

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 设置](#.E8.AE.BE.E7.BD.AE)
    *   [2.1 服务器](#.E6.9C.8D.E5.8A.A1.E5.99.A8)
        *   [2.1.1 密钥](#.E5.AF.86.E9.92.A5)
        *   [2.1.2 启动服务器](#.E5.90.AF.E5.8A.A8.E6.9C.8D.E5.8A.A1.E5.99.A8)
    *   [2.2 客户端](#.E5.AE.A2.E6.88.B7.E7.AB.AF)
        *   [2.2.1 Arch Linux](#Arch_Linux)
        *   [2.2.2 Windows](#Windows)
        *   [2.2.3 配置](#.E9.85.8D.E7.BD.AE)
*   [3 运行](#.E8.BF.90.E8.A1.8C)
    *   [3.1 键盘快捷键](#.E9.94.AE.E7.9B.98.E5.BF.AB.E6.8D.B7.E9.94.AE)
    *   [3.2 退出全屏](#.E9.80.80.E5.87.BA.E5.85.A8.E5.B1.8F)
    *   [3.3 Tips on resume](#Tips_on_resume)
    *   [3.4 修复 DPI 设置](#.E4.BF.AE.E5.A4.8D_DPI_.E8.AE.BE.E7.BD.AE)
*   [4 在已有屏幕上使用 FreeNX](#.E5.9C.A8.E5.B7.B2.E6.9C.89.E5.B1.8F.E5.B9.95.E4.B8.8A.E4.BD.BF.E7.94.A8_FreeNX)
*   [5 设置非 KDE 或非 Gnome 桌面管理器](#.E8.AE.BE.E7.BD.AE.E9.9D.9E_KDE_.E6.88.96.E9.9D.9E_Gnome_.E6.A1.8C.E9.9D.A2.E7.AE.A1.E7.90.86.E5.99.A8)
    *   [5.1 Alternative fix](#Alternative_fix)
*   [6 问题](#.E9.97.AE.E9.A2.98)
    *   [6.1 调试问题](#.E8.B0.83.E8.AF.95.E9.97.AE.E9.A2.98)
    *   [6.2 验证 OK, 但连接失败](#.E9.AA.8C.E8.AF.81_OK.2C_.E4.BD.86.E8.BF.9E.E6.8E.A5.E5.A4.B1.E8.B4.A5)
    *   [6.3 按键改变](#.E6.8C.89.E9.94.AE.E6.94.B9.E5.8F.98)
    *   [6.4 Xorg 7](#Xorg_7)
    *   [6.5 密码错误 / 没有可用连接](#.E5.AF.86.E7.A0.81.E9.94.99.E8.AF.AF_.2F_.E6.B2.A1.E6.9C.89.E5.8F.AF.E7.94.A8.E8.BF.9E.E6.8E.A5)
        *   [6.5.1 在启动 session 时 NX 崩溃](#.E5.9C.A8.E5.90.AF.E5.8A.A8_session_.E6.97.B6_NX_.E5.B4.A9.E6.BA.83)
    *   [6.6 显示 NX 徽标之后黑屏](#.E6.98.BE.E7.A4.BA_NX_.E5.BE.BD.E6.A0.87.E4.B9.8B.E5.90.8E.E9.BB.91.E5.B1.8F)
    *   [6.7 GDM/XDM Session Menu Error with non-KDE or Gnome Desktop Managers (more common with non-Arch Linux users)](#GDM.2FXDM_Session_Menu_Error_with_non-KDE_or_Gnome_Desktop_Managers_.28more_common_with_non-Arch_Linux_users.29)
    *   [6.8 Cannot connect because command sessreg not found](#Cannot_connect_because_command_sessreg_not_found)

## 安装

包分为两部分：

*   freenx （服务器）
*   nxclient （客户端）

如果你打算用 freenx 来连接无头 PC，记得你得有一个配置好的 X 服务器，这样你应该就能安装任何与 [xorg](/index.php/Xorg "Xorg") 相关联的包了。

## 设置

### 服务器

自由（免费）的服务器在 'freenx' 包中。你必须安装 sshd 守护进程，并且让它正确运行：

```
# systemctl enable sshd

```

要使 freenx 的登录验证工作，sshd 必须正确配置。检查 /etc/ssh/sshd_config 中下列项：

```
RSAAuthentication yes
AllowUsers someuser nx

```

NX 的主配置文件位于:

```
/opt/NX/etc/node.conf

```
*如果你的 ssh 守护进程不是运行在默认的 22 端口，你需要取消注释并修改：* `SSHD_PORT=22` 
**Note:** As of OpenSSL 1.0.0, it is necessary to set proper md5sum command in `/opt/NX/etc/node.conf`: `COMMAND_MD5SUM="md5sum"` 

如果你在用 Gnome 或 KDE 桌面环境，你不需要编辑此文件，应为修改过的 MD5SUM 与默认配置在这种场合下能够工作。如果你在使用其它窗口管理器，比如 Fluxbox/Openbox 或 Xfce，你大概需要稍微修改这个文件（见下方）。

安装完 freenx 包，运行 `/opt/NX/bin/nxsetup --help` for an overview of the install and uninstall procedures.

**Note:** You should also install "xdialog" on the server or you will not see the "suspend/terminate" dialog when you try to close the window or hit "ctrl-alt-T": `pacman -S xdialog` 

#### 密钥

服务器需要用密钥来验证客户端。默认情况下，在安装时会产生一对随机密钥，一个是服务器的，另一个是客户端的。你需要给每一个想要连接的客户端（Windows 也好， linux 也好）复制一份客户端密钥。

客户端密钥能在这儿找到：

```
/opt/NX/home/nx/.ssh/client.id_dsa.key

```

Alternatively you can use the default key that is provided by NoMachine with all clients. In this case you do not need to copy a custom generated key to each client. To get the server to accept the default client keys run:

```
/opt/NX/bin/nxsetup --install --setup-nomachine-key

```

Recreation of random keys:

```
/opt/NX/bin/nxsetup --install

```

Transferring nx keys to another freenx server:

*   /opt/NX/home/nx/.ssh contains the key files

```
 -rw------- 1 nx root  697  9\. Okt 12:55 authorized_keys
 -rw------- 1 nx root  668  9\. Okt 11:48 client.id_dsa.key
 -rw------- 1 nx root  609  9\. Okt 12:55 server.id_dsa.pub.key

```

*   Save those files.
*   Add those files to your new server, they need the same permissions, names, group and directory!

```
 # cp authorized_keys client.id_dsa.key server.id_dsa.pub.key /opt/NX/home/nx/.ssh/
 # chmod 600 /opt/NX/home/nx/.ssh/*
 # chown nx /opt/NX/home/nx/.ssh/*
 # chgrp root /opt/NX/home/nx/.ssh/*

```

*   Recreate known_hosts file:

```
 # echo -n 127.0.0.1 > /opt/NX/home/nx/.ssh/known_hosts
 # cat /etc/ssh/ssh_host_rsa_key.pub >> /opt/NX/home/nx/.ssh/known_hosts
 # chmod 633 /opt/NX/home/nx/.ssh/known_hosts
 # chown nx /opt/NX/home/nx/.ssh/known_hosts
 # chgrp root /opt/NX/home/nx/.ssh/known_hosts

```

#### 启动服务器

Once installed the server is effectively running and ready to go, you do not have to do anything manually The only thing that must be running in order to connect is the sshd daemon. This is because the nxserver is actually started by logging into sshd as the special user 'nx'. This user has been set up to use the nxserver as its shell, much like a normal user has bash as the default shell.

You can specify the local addresses sshd should listen for by editing /etc/ssh/sshd_config and adding them in the following format:

```
ListenAddress host|IPv4_addr|IPv6_addr

```

The original ListenAddress in sshd_config is 0.0.0.0\. This listens to all addresses, however adding any address will take precedent to this and and accept connections from the new address only.

Restart the sshd daemon to put any changes to its configuration into effect:

```
# systemctl restart sshd

```

In actual fact, if you check the process list (`ps aux`) you may not see the nxserver running even though it is. This is because the nxserver is actually started by logging into sshd as the special user 'nx'. This user has been set up to use the nxserver as its shell, much like a normal user has bash as the default shell.

### 客户端

#### Arch Linux

Get the client from pacman:

```
pacman -S nxclient

```

#### Windows

Get the client from nomachine's homepage: [http://www.nomachine.com](http://www.nomachine.com)

Tip: Nomachine tends to remove old clients from their homepage, If your setup works with a client save it at a safe place ;)

#### 配置

As mentioned above, the client must contain the correct key to connect to the server. If you are using the custom keys generated during install, you need to copy the client key to the following locations:

*   Windows: `<yourinstalldironwindows>/share/keys/client.id_dsa.key`
*   Arch Linux: `/opt/NX/share/keys/client.id_dsa.key`

After moving the keys you may have use the nxclient GUI to import the new keys. From the configuration dialog press the 'Key...' button and import the new client key.

## 运行

After installing nxclient on Arch Linux, executables are available in /opt/NX/bin. At the first run of /opt/NX/bin/nxclient, the user will be led through a wizard.

### 键盘快捷键

```
CTR+ALT+F          Toggles full-screen mode. 
CTRL+ALT+T         Shows the terminate, suspend dialog.
CTRL+ALT+M         Maximizes of minimizes the window 
CTRL+ALT+Mouse     Drags the viewport, so you can view different portions 
                   of the desktop. 
CTRL+ALT+Arrows 
or                 Moves the viewport by an incremental amount of pixels. 
CTRL+ALT+Keypad 
CTRL+ALT+S         It will activate "screen-scraping" mode, so all the GetImage
                   originated by the clients will be forwarded to the real
                   display. This should make happy those who love taking
                   screenshots ;-). By pressing the sequence again, nxagent
                   will revert to the usual "fast" mode.
CTRL+ALT+E         lazy image encoding
CTRL+ALT+Shift+ESC Emergency-exit and kill-window

```

### 退出全屏

There is a magic-pixel in the top right corner of nearly every nx-application in fullscreenmode. Right-click the pixel and application-window gets iconified.

### Tips on resume

*   Resume is a bit experimental, crashes might appear after session has resumed. You have to find out which apps like resuming and which do not ;) .
*   Resuming between Linux and Windows sessions does not work. UPDATE: It appears that version 3.2.0-14 is able to resume Windows-suspended sessions.
*   If resume fails let it time out and don't use the cancel button, else sessions will stay open and consume RAM on server. To kill such sessions use the Session Admin program to kill them.

### 修复 DPI 设置

If you like to have the same font-sizes/dpi sizes on all your client session, set the X resource "Xft.dpi". For example putting the following line into a user's "~/.Xresources" makes her/his "desktop" a 100dpi. Xft.dpi: 100

## 在已有屏幕上使用 FreeNX

Usually, when connecting to a NX server, a new X session is created. Sometimes it might be useful, to connect to an existing X session, e.g. the root session. This is not possible with NX in default setup, but can be reached, using `tightvnc` and `x11vnc`. Do the following steps on the NX server system.

```
# pacman -S tightvnc x11vnc

```

x11vnc will serve the X session, we have to create a file `$HOME/.x11vncrc` to give x11vnc some options, e.g.:

```
display :0
shared
forever
localhost
rfbauth /home/USER/.x11vnc/passwd

```

Create the VNC password file:

```
$ mkdir $HOME/.x11vnc
$ x11vnc -storepasswd PASSWORD $HOME/.x11vnc/passwd
$ chmod 600 $HOME/.x11vnc/passwd

```

Create a shell script, which starts the x11vnc service, if not running and starts the vncviewer provided by the package tightvnc.

**Note:** The variable `$VNC_PORT` in the following script defines the X display, which is configured as `display :0` under `$HOME/.x11vncrc`, `590**0**` is the root session, if you want to use `display :1` use the port `590**1**` and so on

```
#!/bin/sh
VNC_VIEWER=vncviewer
VNC_SERVER=x11vnc
VNC_RESOLUTION=1024x786
VNC_PASSWD=/home/USER/.x11vnc/passwd
VNC_PORT=5900

if [ -z "$(pgrep ${VNC_SERVER})" ]; then
	echo $VNC_SERVER not running, starting...
	exec $VNC_SERVER &
	sleep 5
fi

exec $VNC_VIEWER -geometry $VNC_RESOLUTION -passwd $VNC_PASSWD localhost::$VNC_PORT

```

Save this script with a texteditor of your choice, e.g. under `$HOME/shell/nxvnc.sh`. Make it executable and create a symbolic link, e.g:

```
$ chmod +x $HOME/shell/nxvnc.sh
# ln -s /home/USER/shell/nxvnc.sh /usr/local/bin/nxvnc

```

At this point, you might want to test the current configuration: `$ /usr/local/bin/nxvnc`

If the x11vnc service and a vncviewer session is started, you configuration works well. You are now able to connect to the current X session using your NX client with following options:

```
Login, Password, Host, Port: your default entries
Desktop: Unix -> Custom
 - Settings:
   - Run the following command: /usr/local/bin/nxvnc
   - New virtual desktop
Display:
  - Fullscreen or Custom with you preferred resolution

```

You are able to connect to your current X session via NX client now.

	— [FreeNX to existing display (opensuse.org)](http://en.opensuse.org/SDB:FreeNX_to_existing_display)

## 设置非 KDE 或非 Gnome 桌面管理器

Before following anything in this part, make sure the server working setup and accepting connections. This section only deals with problems once NXClient has logged on.

It is quite simple (once the server is setup) to connect to Gnome and KDE sessions, however connecting to other window managers (fluxbox, xfce, whatever) is slightly different.

Choosing "custom" and using a command like startx of startfluxbox will either result in a blank screen after the !M logo or the Client to present an error complaining about lack of a X server. A way around this is open a session with the command "startx", and the another with the command to start your window-manager-of-choice.

If you do not want to do this, you can start X by [installing a login manager like SLIM or XDM](/index.php/Display_manager "Display manager"). I would recomend using SLiM because of it's small size.

(Authors note: This is how I got fluxbox, xfce and others to work on my arch installation- however, I have now removed slim from inittab and set the run level back to 3, and yet I can still login perfectly with NXClient. Possibly try this if you get your system working this way, if like me you have a low memory machine.)

#### Alternative fix

A simple fix without resorting to the above seems to involve a simple edit to the config file. This should work for fluxbox/openbox/xfce or any other window manager that uses the **.xinitrc** startup file in a call to **startx**.

Simply edit the config file (as root):

```
/opt/NX/etc/node.conf

```

and change

```
#USER_X_STARTUP_SCRIPT=.Xclients

```

to

```
USER_X_STARTUP_SCRIPT=.xinitrc

```

Remember to remove the # symbol from the start of the line.

Then in the client under configuration settings, choose **Custom** as the desktop, and click on settings:

*   In the first group select - **`Run the default X client Script on server`**
*   In the second group select - **`New virtual desktop`**

## 问题

### 调试问题

Edit the nxserver config file:

```
 vi /opt/NX/etc/node.conf

```

Change:

```
 #SESSION_LOG_CLEAN=1

```

to

```
 SESSION_LOG_CLEAN=0

```

Then you can look/debug the log files in:

```
 $HOME/.nx/T-C-<hostname>-<display>-<session-id>

```

For succesfull connections and:

```
 $HOME/.nx/F-C-<hostname>-<display>-<session-id>

```

For failed ones.

### 验证 OK, 但连接失败

If you are trying to startkde

```
 vi /opt/NX/etc/node.conf

```

And search for:

```
 COMMAND_START_KDE=startkde

```

Replace for:

```
 COMMAND_START_KDE=/usr/bin/startkde

```

### 按键改变

Change the key in GUI setup to new generated key.

### Xorg 7

Be aware that you have to remove the /usr/X11R6 directory, else strange things can happen.

### 密码错误 / 没有可用连接

*   If you have changed your ssh daemon to run on an alternate port, be sure to modify SSHD_PORT within /opt/NX/etc/node.conf.

*   If you get always wrong password or no connection after authentication was done and you are sure that you typed it correct, check that your server can connect to itself using localhost by ssh.

*   If you messed up your key files, create new ones or fix the old ones, it's probably caused by a wrong known_hosts file.

*   If you get wrong password or login, put **ENABLE_PASSDB_AUTHENTICATION="1"** in /opt/NX/etc/node.conf and add a user by

```
# /opt/NX/bin/nxserver --adduser [username]
# /opt/NX/bin/nxserver --passwd [username]

```

#### 在启动 session 时 NX 崩溃

If your NX Client shows the NX logo then disappears with a Connection Problem dialog afterwards.

Then it could be due to missing fonts. Mostly applies if you have installed Arch Linux base and then installed freenx after without the whole X11 set.

Solution until FreeNX Dependencies is fixed is to install xorg-fonts-misc on your NX Server (pacman -S xorg-fonts-misc) and your NX should work.

Note: This does not apply to freenx 0.6.1-3 and above, fix has been incorporated in it and following versions.

### 显示 NX 徽标之后黑屏

If you see the NX logo (!M) then a blank screen.

This problem can be solved by running a login manager- The problem is that X11 is not started, and it appears that "startx" or similar do not work from the freenx client. Follow these instructions to setup a login manager and load it at startup: [Display manager](/index.php/Display_manager "Display manager")

Blind: If this does not resolve your issues, be aware that freenx and bash_completion do not play well together. I only got things to work after removing bash_completion from the .bashrc.

### GDM/XDM Session Menu Error with non-KDE or Gnome Desktop Managers (more common with non-Arch Linux users)

Problem: A session menu comes up talking about "chooseSessionListWidget." A window manager never loads.

Fix :

Double check to see if ~/.xinitrc is executable.

```
 ls -la ~/ | grep .xinitrc

```

If the file is not executable, simply

```
 chmod +x ~/.xinitrc

```

Keep in mind this command should be executed along with pertinent instructions on this page about "Setting up non-KDE or Gnome desktop managers"

### Cannot connect because command sessreg not found

If you get the following error while connecting

```
 /opt/NX/bin/nxserver: line 941: sessreg: command not found
 NX> 280 Exiting on signal: 15

```

then you have to install the package xorg-server-utils.