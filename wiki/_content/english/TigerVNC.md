Related articles

*   [x11vnc](/index.php/X11vnc "X11vnc")

[TigerVNC](http://tigervnc.org/) is an implementation of the [Virtual Network Computing](https://en.wikipedia.org/wiki/Virtual_Network_Computing "wikipedia:Virtual Network Computing") (VNC) protocol. This article focuses on the server functionality.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Running vncserver for virtual (headless) sessions](#Running_vncserver_for_virtual_(headless)_sessions)
    *   [2.1 Create password, startup and config files](#Create_password,_startup_and_config_files)
        *   [2.1.1 Edit the startup script](#Edit_the_startup_script)
        *   [2.1.2 Edit the optional config file](#Edit_the_optional_config_file)
    *   [2.2 Starting and stopping vncserver via systemd](#Starting_and_stopping_vncserver_via_systemd)
        *   [2.2.1 User mode](#User_mode)
        *   [2.2.2 System mode](#System_mode)
        *   [2.2.3 On demand multi-user mode](#On_demand_multi-user_mode)
*   [3 Running x0vncserver to directly control the local display](#Running_x0vncserver_to_directly_control_the_local_display)
    *   [3.1 Starting x0vncserver via xprofile](#Starting_x0vncserver_via_xprofile)
    *   [3.2 Starting and stopping x0vncserver via systemd](#Starting_and_stopping_x0vncserver_via_systemd)
*   [4 Connecting to vncserver](#Connecting_to_vncserver)
    *   [4.1 Passwordless authentication](#Passwordless_authentication)
    *   [4.2 Example GUI-based clients](#Example_GUI-based_clients)
*   [5 Accessing vncserver via SSH tunnels](#Accessing_vncserver_via_SSH_tunnels)
    *   [5.1 On the server](#On_the_server)
    *   [5.2 On the client](#On_the_client)
    *   [5.3 Connecting to a vncserver from Android devices over SSH](#Connecting_to_a_vncserver_from_Android_devices_over_SSH)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Connecting to an OSX system](#Connecting_to_an_OSX_system)
    *   [6.2 Connecting to non-X environments on a Raspberry Pi (Arch ARM)](#Connecting_to_non-X_environments_on_a_Raspberry_Pi_(Arch_ARM))
    *   [6.3 Recommended security settings](#Recommended_security_settings)
    *   [6.4 Starting X (startx) with vncserver](#Starting_X_(startx)_with_vncserver)
    *   [6.5 Toggling Fullscreen](#Toggling_Fullscreen)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Unable to type '<' character](#Unable_to_type_'<'_character)
    *   [7.2 Black rectangle instead of window](#Black_rectangle_instead_of_window)
    *   [7.3 No mouse cursor](#No_mouse_cursor)
    *   [7.4 Copying clipboard content from the remote machine](#Copying_clipboard_content_from_the_remote_machine)
    *   [7.5 "Authentication is required to create a color managed device" dialog when launching GNOME 3](#"Authentication_is_required_to_create_a_color_managed_device"_dialog_when_launching_GNOME_3)
*   [8 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [tigervnc](https://www.archlinux.org/packages/?name=tigervnc) package.

Two VNC servers are available with TigerVNC:

1.  *Xvnc* is the default and recommended server for TigerVNC. It is both a VNC server and an X server with a virtual framebuffer. This means it is similar to the standard X server but has a virtual screen rather than a physical one. The virtual server runs in parallel with the physical X server should one be running. *vncserver* is a wrapper script which eases the starting of *Xvnc*. See [#Running vncserver for virtual (headless) sessions](#Running_vncserver_for_virtual_(headless)_sessions) for more information.
2.  *x0vncserver* provides direct control of the local X session(s) which are running on the physical monitor. It continuously polls the X display which is a simple but inefficient implementation. See [#Running x0vncserver to directly control the local display](#Running_x0vncserver_to_directly_control_the_local_display) for more information.

TigerVNC also provides *vncviewer* which is a client viewer for VNC.

## Running vncserver for virtual (headless) sessions

### Create password, startup and config files

The first time *vncserver* is run, it creates its initial environment, config, and user password file. These will be stored in `~/.vnc` which will be created if not present. See [vncserver(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vncserver.1) for the complete manual.

 `$ vncserver` 
```
You will require a password to access your desktops.

Password:
Verify:

New 'mycomputer:1 (theusername)' desktop is mycomputer:1

Creating default startup script /home/theusername/.vnc/xstartup
Starting applications specified in /home/theusername/.vnc/xstartup
Log file is /home/theusername/.vnc/mycomputer:1.log

```

Note the `:1` trailing the hostname in the output messages of the script. This indicates the TCP port number on which the virtual VNC server is running. In this case, `:1` is actually TCP port 5901 (5900+1). Running `vncserver` a second time will create a second instance running on the next highest, free port, i.e 5902 (5900+2) which shall end in `:2` as above.

**Note:** Linux systems can have as many VNC servers as memory allows, all of which will be running in parallel to each other.

To shutdown the just created VNC server, use the `-kill` switch:

```
$ vncserver -kill :1

```

If at any stage one needs to change the previously defined password, the *vncpasswd* tool can be called:

```
$ vncpasswd

```

See [vncpasswd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vncpasswd.1) for more information.

#### Edit the startup script

The `~/.vnc/xstartup` script is sourced by *vncserver* for creating the virtual X session and it must be adapted to one's needs. It functions like an [.xinitrc](/index.php/.xinitrc ".xinitrc") file. In this script, users are expected to start a [Desktop environment](/index.php/Desktop_environment "Desktop environment"), see: [General recommendations#Desktop environments](/index.php/General_recommendations#Desktop_environments "General recommendations").

For example, to start [Xfce](/index.php/Xfce "Xfce"), the following script can be used:

 `~/.vnc/xstartup` 
```
#!/bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
exec startxfce4
```

**Note:** The instruction `unset DBUS_SESSION_BUS_ADDRESS` clears the variable and forces `startxfce4` to initiate a new bus for the VNC session. If [D-Bus](/index.php/D-Bus "D-Bus") fails to start, try using `exec dbus-launch startxfce4` instead to launch the bus manually, note that this latter way of starting *D-Bus* is deprecated.

To start [GNOME](/index.php/GNOME "GNOME"), replace `exec startxfce4` by `exec dbus-launch gnome-session` in the example above.

To start [Cinnamon](/index.php/Cinnamon "Cinnamon"), replace `exec startxfce4` by `exec dbus-launch cinnamon-session` in the example above.

Make sure `~/.vnc/xstartup` has a execute permission.

#### Edit the optional config file

*vncserver* supports parsing parameters through the command line, or in the file `~/.vnc/config`. The format of the config file is one option per line, option names are case-insensitive and commenting with `#` is supported. The parameters can be either *vncserver* specific or can be parameters that are passed to *Xvnc*, see [vncserver(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vncserver.1) or [Xvnc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xvnc.1) for the full list of available options.

An example is provided below:

 `~/.vnc/config` 
```
securitytypes=tlsvnc
desktop=sandbox
geometry=1200x700
dpi=96
localhost
alwaysshared
```

### Starting and stopping vncserver via systemd

*Systemd* can manage the vncserver by either running it in system or in user mode. Both ways are presented below.

#### User mode

The user mode is the most straightforward way to run the VNC server as a service. [Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `vncserver@:1.service` in [Systemd/User](/index.php/Systemd/User "Systemd/User") mode, i.e. with the `--user` parameter. The `:1` option can be replaced by another display number, it is the increment over 5900 the VNC server listens to. In the previous example, one connects to the server through port 5901.

**Note:** The vncserver will get killed when the user logs off the machine, see [Systemd/User#Automatic start-up of systemd user instances](/index.php/Systemd/User#Automatic_start-up_of_systemd_user_instances "Systemd/User") for related configuration.

#### System mode

Create `/etc/systemd/system/vncserver@*:1*.service`. As in user mode above, `:1` is the port increment over 5900 to which the VNC server will be listening for connections (e.g `vncserver@:5.service` means the server will be listening to port 5905). Edit the service unit by defining the user (`User=`) to run the server, and the desired *vncserver* options.

 `/etc/systemd/system/vncserver@*:1*.service` 
```
[Unit]
Description=Remote desktop service (VNC)
After=syslog.target network.target

[Service]
Type=simple
User=foo
PAMName=login
PIDFile=/home/%u/.vnc/%H%i.pid
ExecStartPre=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
ExecStart=/usr/bin/vncserver %i -geometry 1440x900 -alwaysshared -fg
ExecStop=/usr/bin/vncserver -kill %i

[Install]
WantedBy=multi-user.target
```

[Start](/index.php/Start "Start") `vncserver@*:1*.service` and optionally [enable](/index.php/Enable "Enable") it to run at boot time/shutdown.

#### On demand multi-user mode

One can use *systemd* socket activation in combination with [XDMCP](/index.php/XDMCP "XDMCP") to automatically spawn VNC servers for each user who attempts to login, so there is no need to set up one server/port per user. This setup uses the display manager to authenticate users and login, so there is no need for VNC passwords. The downside is that users cannot leave a session running on the server and reconnect to it later.

To get this running, first set up [XDMCP](/index.php/XDMCP "XDMCP") and make sure the display manager is running. Then create:

 `/etc/systemd/system/xvnc.socket` 
```
[Unit]
Description=XVNC Server

[Socket]
ListenStream=5900
Accept=yes

[Install]
WantedBy=sockets.target
```
 `/etc/systemd/system/xvnc@.service` 
```
[Unit]
Description=XVNC Per-Connection Daemon

[Service]
ExecStart=-/usr/bin/Xvnc -inetd -query localhost -geometry 1920x1080 -once -SecurityTypes=None
User=nobody
StandardInput=socket
StandardError=syslog
```

Use systemctl to [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `xvnc.socket`. Now any number of users can get unique desktops by connecting to port 5900.

If the VNC server is exposed to the internet, add the `-localhost` option to `Xvnc` in `xvnc@.service` (note that `-query localhost` and `-localhost` are different switches) and follow [#Accessing vncserver via SSH tunnels](#Accessing_vncserver_via_SSH_tunnels). Since we only select a user after connecting, the VNC server runs as user *nobody* and uses `Xvnc` directly instead of the `vncserver` script, so any options in `~/.vnc` are ignored. Optionally, [autostart](/index.php/Autostart "Autostart") *vncconfig* so that the clipboard works (*vncconfig* exits immediately in non-VNC sessions). One way is to create:

 `/etc/X11/xinit/xinitrc.d/99-vncconfig.sh` 
```
#!/bin/sh
vncconfig -nowin &
```

## Running x0vncserver to directly control the local display

As mentioned in [#Installation](#Installation), the *tigervnc* package also provides the x0vncserver binary which allows direct control over a physical X session. After defining a session password using the *vncpasswd* tool, invoke the server like so:

```
$ x0vncserver -rfbauth ~/.vnc/passwd

```

For more information, see [x0vncserver(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/x0vncserver.1).

**Note:** *x0vncserver* is an inefficient VNC server which continuously polls any X display, allowing it to be controlled via VNC. It is intended mainly as a demonstration of a simple VNC server. [x11vnc](/index.php/X11vnc "X11vnc") is an alternative more advanced VNC server which also provides direct control of the current X session.

### Starting x0vncserver via xprofile

A simple way to start *x0vncserver* is adding a line in one of the [xprofile](/index.php/Xprofile "Xprofile") files such as:

 `~/.xprofile` 
```
...
x0vncserver -rfbauth ~/.vnc/passwd &
```

### Starting and stopping x0vncserver via systemd

In order to have a VNC Server running *x0vncserver*, which is the easiest way for most users to quickly have remote access to the current desktop, create a systemd unit as follows replacing the user and the options with the desired ones:

 `~/.config/systemd/user/x0vncserver.service` 
```
[Unit]
Description=Remote desktop service (VNC)

[Service]
Type=simple
# wait for Xorg started by ${USER}
ExecStartPre=/bin/sh -c 'while ! pgrep -U "$USER" Xorg; do sleep 2; done'
ExecStart=/usr/bin/x0vncserver -rfbauth %h/.vnc/passwd
# or login with your username & password
#ExecStart=/usr/bin/x0vncserver -PAMService=login -PlainUsers=${USER} -SecurityTypes=TLSPlain

[Install]
WantedBy=default.target
```

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") the service `x0vncserver.service` in [Systemd/User](/index.php/Systemd/User "Systemd/User") mode, i.e. with the `--user` parameter.

## Connecting to vncserver

**Warning:** The default's TigerVNC security method is not secure, it lacks identity verification and will not prevent man-in-the-middle attack during the connection setup. Make sure you understand the security settings of your server and do not connect insecurely to a vncserver outside of a trusted LAN.

**Note:** By default, TigerVNC uses the *TLSVnc* authentication/encryption method unless specifically instructed via the `SecurityTypes` parameter. With *TLSVnc*, there is standard VNC authentication and traffic is encrypted with GNUTLS but the identity of the server is not verified. TigerVNC supports alternative security schemes such as *X509Vnc* that combines standard VNC authentication with GNUTLS encryption and server identification, this is the recommended mode for a secure connection. When `SecurityTypes` on the server is set to a non-encrypted option as high-priority (such as *None*, *VncAuth*, *Plain*, *TLSNone*, *TLSPlain*, *X509None*, *X509Plain*); which is ill-advised, then it is not possible to use encryption. When running *vncviewer*, it is safer to explicitly set `SecurityTypes` and not accept any unencrypted traffic. Any other mode is to be used only when [#Accessing vncserver via SSH tunnels](#Accessing_vncserver_via_SSH_tunnels).

Any number of clients can connect to a vncserver. A simple example is given below where vncserver is running on 10.1.10.2 port 5901, or :1 in shorthand notation:

```
$ vncviewer 10.1.10.2:1

```

### Passwordless authentication

The `-passwd` switch allows one to define the location of the server's `~/.vnc/passwd` file. It is expected that the user has access to this file on the server through [SSH](/index.php/SSH "SSH") or through physical access. In either case, place that file on the client's file system in a safe location, i.e. one that has read access ONLY to the expected user.

```
$ vncviewer -passwd */path/to/server-passwd-file*

```

The password can also be provided directly.

**Note:** The password below is not secured; anyone who can run `ps` on the machine will see it.

```
$ vncviewer -passwd <(echo MYPASSWORD | vncpasswd -f)

```

### Example GUI-based clients

*   [gtk-vnc](https://www.archlinux.org/packages/?name=gtk-vnc)
*   [krdc](https://www.archlinux.org/packages/?name=krdc)
*   [vinagre](https://www.archlinux.org/packages/?name=vinagre)
*   [remmina](/index.php/Remmina "Remmina")
*   [virt-viewer](https://www.archlinux.org/packages/?name=virt-viewer)
*   [vncviewer-jar](https://aur.archlinux.org/packages/vncviewer-jar/)

TigerVNC's vncviewer also has a simple GUI when run without any parameters:

```
$ vncviewer

```

## Accessing vncserver via SSH tunnels

For servers offering SSH connection, an advantage of this method is that it is not necessary to open any other port than the already opened SSH port to the outside, since the VNC traffic is tunneled through the SSH port.

### On the server

On the server side, *vncserver* or *x0vncserver* must be run.

When running *vncserver*, it is recommended to use the `-localhost` switch way since it allows connections from the localhost only and by analogy, only from users ssh'ed and authenticated on the box. For example run a command such as:

```
$ vncserver -geometry 1440x900 -alwaysshared -dpi 96 **-localhost** :1

```

For *x0vncserver*, this `-localhost` switch is not available but a workaround is to use the `-HostsFile` option and create the below file that will be provided as a parameter:

 `~/.vnc/hostsfile` 
```
+127.0.0.1
+::1
-
```

It will only accept connection from localhost in IPv4 or IPv6 address standard.

The corresponding command is:

```
$ x0vncserver -HostsFile ~/.vnc/hostsfile -SecurityTypes none

```

### On the client

The VNC server has been setup on the remote machine to only accept local connections. Now, the client must open a secure shell with the remote machine (10.1.10.2 in this example) and create a tunnel from the client port, for instance 9901, to the remote server 5901 port. For more details on this feature, see [OpenSSH#Forwarding other ports](/index.php/OpenSSH#Forwarding_other_ports "OpenSSH") and [ssh(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ssh.1).

```
$ ssh 10.1.10.2 -L 9901:localhost:5901

```

Once connected via SSH, leave this shell window open since it is acting as the secured tunnel with the server. Alternatively, directly run SSH in the background using the `-f` option. On the client side, to connect via this encrypted tunnel, point the *vncviewer* to the forwarded client port on the localhost.

```
$ vncviewer localhost:9901

```

What happens in practice is that the vncviewer connects locally to port 9901 which is tunneled to the server's localhost port 5901\. The connection is established to the right port within the secure shell.

**Tip:** It is possible, with a one-liner, to keep the port forwarding active during the connection and close it right after: `$ ssh -fL 9901:localhost:5901 10.1.10.2 sleep 10; vncviewer localhost:9901` What it does is that the `-f` switch will make ssh go in the background, it will still be alive executing `sleep 10`. vncviewer is then executed and ssh remains open in the background as long as vncviewer makes use of the tunnel. ssh will close once the tunnel is dropped which is the wanted behavior.

### Connecting to a vncserver from Android devices over SSH

To connect to a VNC server over SSH using an Android device as a client, consider having the following setup:

1.  SSH running on the server
2.  vncserver running on server (with `-localhost` flag for security)
3.  SSH client on the Android device: *ConnectBot* is a popular choice and will be used in this guide as an example
4.  VNC client on the Android device: *androidVNC* used here

In *ConnectBot*, connect to the desired machine. Tap the options key, select *Port Forwards* and add a port:

```
Type: Local
Source port: 5901
Destination: 127.0.0.1:5901

```

In *androidVNC* connect to the VNC port, this is the local address following the SSH connection:

```
Password: the vncserver password
Address: 127.0.0.1
Port: 5901

```

## Tips and tricks

### Connecting to an OSX system

See [https://help.ubuntu.com/community/AppleRemoteDesktop](https://help.ubuntu.com/community/AppleRemoteDesktop). Tested with Remmina.

### Connecting to non-X environments on a Raspberry Pi (Arch ARM)

Install [dispmanx_vnc](https://aur.archlinux.org/packages/dispmanx_vnc/) on the Arch ARM device. Frame rates are not very high but it provides a working VNC access.

### Recommended security settings

If not [#Accessing vncserver via SSH tunnels](#Accessing_vncserver_via_SSH_tunnels) where the identification and the encryption are handled via SSH, it is recommended to use *X509Vnc*, as *TLSVnc* lacks identity verification.

```
$ vncserver -x509key */path/to/key.pem* -x509cert */path/to/cert.pem* -SecurityTypes X509Vnc :1

```

Issuing x509 certificates is beyond the scope of this guide. However, [Let's Encrypt](https://en.wikipedia.org/wiki/Let%27s_Encrypt "wikipedia:Let's Encrypt") provides an easy way to do so. Alternatively, one can issue certificates using [OpenSSL](/index.php/OpenSSL "OpenSSL"), share the public key with the client and specify it with the `-X509CA` parameter. An example is given below the server is running on 10.1.10.2:

```
$ vncviewer 10.1.10.2 -X509CA */path/to/cert.pem*

```

### Starting X (startx) with vncserver

Users invoking `startx` to load the DE, should note that the default `~/.vnc/xstartup` will launch an X session with `twm` as the desktop ignoring the setting at the end of `~/.vnc/xstartup`. Instead of specifying the desktop at the end of `~/.vnc/xstartup`, `source` `.xinitrc` (with full path).

### Toggling Fullscreen

This can be done through vnc client's Menu. By default, vnc client's Menu Key is F8.

## Troubleshooting

### Unable to type '<' character

If pressing `<` on a remote client emits the `>` character, try remapping the incoming key [[1]](https://insaner.com/blog/2013/05.html#20130422063137):

```
$ x0vncserver -RemapKeys="0x3c->0x2c"

```

### Black rectangle instead of window

Most probably this is due to the application strictly requiring the composite Xorg extension. For example webkit based app: midori, psi-plus, etc.

Restart vncserver in this case using something like following:

```
 vncserver -geometry ... -depth 24 :1 +extension Composite

```

It looks like Composite extension in VNC will work only with 24bit depth.

### No mouse cursor

If no mouse cursor is visible when using `x0vncserver`, start vncviewer as follows:

```
$ vncviewer DotWhenNoCursor=1 <server>

```

Or put `DotWhenNoCursor=1` in the tigervnc configuration file, which is at `~/.vnc/default.tigervnc` by default.

### Copying clipboard content from the remote machine

If copying from the remote machine to the local machine does not work, run `autocutsel` on the server, as mentioned in [[2]](https://bbs.archlinux.org/viewtopic.php?id=101243):

```
$ autocutsel -fork

```

Now press F8 to display the VNC menu popup, and select `Clipboard: local -> remote` option.

One can put the above command in `~/.vnc/xstartup` to have it run automatically when vncserver is started.

### "Authentication is required to create a color managed device" dialog when launching GNOME 3

A workaround is to create a "vnc" group and add the gdm user and any other users using vnc to that group. Modify `/etc/polkit-1/rules.d/gnome-vnc.rules` with the following[[3]](https://github.com/TurboVNC/turbovnc/issues/47):

```
   polkit.addRule(function(action, subject) {
      if ((action.id == "org.freedesktop.color-manager.create-device" ||
           action.id == "org.freedesktop.color-manager.create-profile" ||
           action.id == "org.freedesktop.color-manager.delete-device" ||
           action.id == "org.freedesktop.color-manager.delete-profile" ||
           action.id == "org.freedesktop.color-manager.modify-device" ||
           action.id == "org.freedesktop.color-manager.modify-profile") &&
          subject.isInGroup("vnc")) {
         return polkit.Result.YES;
      }
   });

```

## See also

*   [https://github.com/TigerVNC/tigervnc](https://github.com/TigerVNC/tigervnc)