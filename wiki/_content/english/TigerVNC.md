Related articles

*   [x11vnc](/index.php/X11vnc "X11vnc")

[TigerVNC](http://tigervnc.org/) is an implementation of the [VNC](https://en.wikipedia.org/wiki/VNC "wikipedia:VNC") protocol. This article focuses on the server functionality.

## Contents

*   [1 Installation](#Installation)
*   [2 Running vncserver for virtual (headless) sessions](#Running_vncserver_for_virtual_.28headless.29_sessions)
    *   [2.1 Create environment, config, and password files](#Create_environment.2C_config.2C_and_password_files)
        *   [2.1.1 Edit the environment file](#Edit_the_environment_file)
        *   [2.1.2 Edit the optional config file](#Edit_the_optional_config_file)
    *   [2.2 Starting and stopping vncserver via systemd](#Starting_and_stopping_vncserver_via_systemd)
        *   [2.2.1 User mode](#User_mode)
        *   [2.2.2 System mode](#System_mode)
        *   [2.2.3 Multi-user mode](#Multi-user_mode)
*   [3 Running vncserver to directly control the local display](#Running_vncserver_to_directly_control_the_local_display)
    *   [3.1 Using tigervnc's x0vncserver](#Using_tigervnc.27s_x0vncserver)
        *   [3.1.1 Starting and stopping x0vncserver via systemd](#Starting_and_stopping_x0vncserver_via_systemd)
    *   [3.2 Using x11vnc](#Using_x11vnc)
*   [4 Connecting to vncserver](#Connecting_to_vncserver)
    *   [4.1 Passwordless authentication](#Passwordless_authentication)
    *   [4.2 Example GUI-based clients](#Example_GUI-based_clients)
*   [5 Accessing vncserver via SSH tunnels](#Accessing_vncserver_via_SSH_tunnels)
    *   [5.1 On the server](#On_the_server)
    *   [5.2 On the client](#On_the_client)
    *   [5.3 Connecting to a vncserver from Android devices over SSH](#Connecting_to_a_vncserver_from_Android_devices_over_SSH)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Connecting to an OSX system](#Connecting_to_an_OSX_system)
    *   [6.2 Connecting to non-X environments on a Raspberry Pi (Arch ARM)](#Connecting_to_non-X_environments_on_a_Raspberry_Pi_.28Arch_ARM.29)
    *   [6.3 Copying clipboard contents from the remote machine to the local](#Copying_clipboard_contents_from_the_remote_machine_to_the_local)
    *   [6.4 Fix for no mouse cursor](#Fix_for_no_mouse_cursor)
    *   [6.5 Recommended security settings](#Recommended_security_settings)
    *   [6.6 Toggling Fullscreen](#Toggling_Fullscreen)
    *   [6.7 Unable to type '<' character](#Unable_to_type_.27.3C.27_character)

## Installation

[Install](/index.php/Install "Install") the [tigervnc](https://www.archlinux.org/packages/?name=tigervnc) package.

**Note:** This packages provides the requisite vncserver, x0vncserver and also vncviewer.

Vncserver provides two major remote control abilities:

1.  Virtual (headless) server is similar to the standard X server, but has a virtual screen rather than a physical one. The virtual server runs completely *parallel* to the physical X server should one be running.
2.  Direct control of the local X session(s) which do run on the physical monitor.

## Running vncserver for virtual (headless) sessions

### Create environment, config, and password files

Vncserver will create its initial environment, config, and user password file the first time it is run. These will be stored in `~/.vnc` which will be created if not present.

 `$ vncserver` 
```
You will require a password to access your desktops.

Password:
Verify:

New 'mars:1 (facade)' desktop is mars:1

Creating default startup script /home/facade/.vnc/xstartup
Starting applications specified in /home/facade/.vnc/xstartup
Log file is /home/facade/.vnc/mars:1.log

```

Notice the :1 trailing the hostname. This is indicating the TCP port number on which the virtual vncserver is running. In this case, :1 is actually TCP port 5901 (5900+1). Running `vncserver` a second time will create a second instance running on the next highest, free port, i.e 5902 (5900+2) which shall end in :2 as above.

**Note:** Linux systems can have as many VNC servers as physical memory allows, all of which running in parallel to each other.

Shutdown the vncserver by using the -kill switch:

```
$ vncserver -kill :1

```

#### Edit the environment file

Vncserver sources `~/.vnc/xstartup` which functions like an [.xinitrc](/index.php/.xinitrc ".xinitrc") file. At a minimum, users should start a DE from this file. For more, see: [General recommendations#Desktop environments](/index.php/General_recommendations#Desktop_environments "General recommendations").

For example, starting lxqt:

 `~/.vnc/xstartup` 
```
#!/bin/sh
exec startlxqt

```

make sure `~/.vnc/xstartup` has a execute permission:

```
 chmod u+x ~/.vnc/xstartup

```

#### Edit the optional config file

With the release of tigervnc 1.60-1, support for parsing options in `~/.vnc/config` has been implemented which obviates the need to call `vncserver` with command line switches. The format is one option per line. An example is provided:

 `~/.vnc/config` 
```

## Supported server options to pass to vncserver upon invocation can be listed
## in this file. See the following manpages for more: vncserver(1) Xvnc(1).
## Several common ones are shown below. Uncomment and modify to your liking.
##
securitytypes=tlsvnc
desktop=sandbox
geometry=1200x700
dpi=96
localhost
alwaysshared

```

### Starting and stopping vncserver via systemd

Systemd can manage the vncserver via a service in one of two modes using either a user or system service. Both are presented below.

#### User mode

**Note:** In order to keep the vncserver alive when the user logs out (physically or via ssh), one must enable the linger option for loginctl like this: `# loginctl enable-linger username` Failure to do so will result in the vncserver getting killed when the user logs off the machine.

Start the service in usermode:

```
$ systemctl --user start vncserver@:1

```

Enable the service in usermode:

```
$ systemctl --user enable vncserver@:1

```

#### System mode

**Warning:** Do not run this service if your local area network is untrusted.

Create `/etc/systemd/system/vncserver@*:1*.service`, where `:1` is the `$DISPLAY` [environment variable](/index.php/Environment_variable "Environment variable").

Modify the service by defining the user (`User=`) to run the server, and the desired [Vncserver](/index.php/Vncserver "Vncserver") options (`usr/bin/vncserver %i -arg1 -arg2 -argn`).

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
ExecStartPre=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
ExecStart=/usr/bin/vncserver %i -geometry 1440x900 -alwaysshared -fg
ExecStop=/usr/bin/vncserver -kill %i

[Install]
WantedBy=multi-user.target

```

[Start](/index.php/Start "Start") `vncserver@*:1*.service` and optionally [enable](/index.php/Enable "Enable") it to run at boot time/shutdown.

#### Multi-user mode

One can use systemd socket activation in combination with [XDMCP](/index.php/XDMCP "XDMCP") to automatically spawn VNC servers for each user who attempts to login, so there is no need to set up one server/port per user. This setup uses the display manager to authenticate users and login, so there is no need for VNC passwords. The downside is that users cannot leave a session running on the server and reconnect to it later. To get this running, first set up [XDMCP](/index.php/XDMCP "XDMCP") and make sure the display manager is running. Then create:

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

If the VNC server is exposed to the internet, add the `-localhost` option to `Xvnc` in `xvnc@.service` and follow the instructions below about connecting over SSH (Note that the 'localhost' in `-query localhost` is not `-localhost`). Since we only select a user after connecting, the VNC server runs as user 'nobody' and uses xvnc directly instead of the 'vncserver' script, so any options in ~/.vnc are ignored. Optionally [autostart](/index.php/Autostart "Autostart") `vncconfig` so that the clipboard works (`vncconfig` exits immediately in non-VNC sessions). One way is to create:

 `/etc/X11/xinit/xinitrc.d/99-vncconfig.sh` 
```

#!/bin/sh
vncconfig -nowin &

```

## Running vncserver to directly control the local display

### Using tigervnc's x0vncserver

[tigervnc](https://www.archlinux.org/packages/?name=tigervnc) provides the x0vncserver binary which allows direct control over a physical X session. Invoke it like so:

```
$ x0vncserver -display :0 -passwordfile ~/.vnc/passwd

```

For more see

```
man x0vncserver

```

#### Starting and stopping x0vncserver via systemd

**Warning:** Do not run this service if your local area network is untrusted!

In order to have a VNC Server runnning x0vncserver, which is the easiest way for most users to quickly have remote access to the current desktop, you can create a systemd unit.

**Note:** This unit will only be useful if the user in the unit is currently running a X session.

Create `/etc/systemd/system/x0vncserver.service` and modify it defining the user to run the server, and the desired options.

 `/etc/systemd/system/x0vncserver.service` 
```

[Unit]
Description=Remote desktop service (VNC)
After=syslog.target network.target

[Service]
Type=forking
User=foo
ExecStart=/usr/bin/sh -c '/usr/bin/x0vncserver -display :0 -rfbport 5900 -passwordfile /home/foo/.vnc/passwd &'

[Install]
WantedBy=multi-user.target

```

### Using x11vnc

Another option is to use [x11vnc](https://www.archlinux.org/packages/?name=x11vnc) which has the advantage or disadvantage, depending on one's perspective, of requiring root to initiate the access. For more, see: [X11vnc](/index.php/X11vnc "X11vnc").

## Connecting to vncserver

**Warning:** It is ill-advised to connect insecurely to a vncserver outside of the LAN; readers are encouraged read the rest of this article in its entirety if use cases require connections outside of one's LAN. That being said, TigerVNC *is encrypted by default* unless it is specifically instructed otherwise by setting SecurityTypes to a non-secure option, although this lacks identity verification and will not prevent MITM attack during the connection setup. X509Vnc is the recommended option for a secure connection.

Any number of clients can connect to a vncserver. A simple example is given below where vncserver is running on 10.1.10.2 on port 5901 (:1) in shorthand notation:

```
$ vncviewer 10.1.10.2:1

```

### Passwordless authentication

The `-passwd` switch allows one to define the location of the server's `~/.vnc/passwd` file. It is expected that the user has access to this file on the server through [SSH](/index.php/SSH "SSH") or through physical access. In either case, place that file on the client's file system in a safe location, i.e. one that has read access ONLY to the expected user.

```
$ vncviewer -passwd /path/to/server-passwd-file

```

### Example GUI-based clients

*   [gtk-vnc](https://www.archlinux.org/packages/?name=gtk-vnc)
*   [krdc](https://www.archlinux.org/packages/?name=krdc)
*   [rdesktop](https://www.archlinux.org/packages/?name=rdesktop)
*   [vinagre](https://www.archlinux.org/packages/?name=vinagre)
*   [remmina](https://www.archlinux.org/packages/?name=remmina)
*   [vncviewer-jar](https://www.archlinux.org/packages/?name=vncviewer-jar)

TigerVNC's vncviewer also has a simple GUI when run without any parameters:

```
$ vncviewer

```

## Accessing vncserver via SSH tunnels

An advantage of SSH tunneling is one does not need to open up another port to the outside, since the traffic is literally tunneled through the SSH port which the user already has open to the WAN. It is highly recommended to use the `-localhost` switch when running vncserver with this method since this switch only allows connections *from the localhost* and by analogy, only by users physically ssh'ed and authenticated on the box.

**Note:** TigerVNC uses TLSVnc encryption by default, unless specifically instructed via the SecurityTypes parameter. Authentication and traffic is encrypted, but there is no identity verification. TigerVNC supports alternative encryption schemes such as X509Vnc that allows the client to verify the identity of the server. When the SecurityTypes on the server side is set to a non-secure option as high-priority (such as None, VncAuth, Plain, TLSNone, TLSPlain, X509None, X509Plain; which is ill-advised), it is not possible to use encryption. In that case, one can tunnel the VNC over SSH. When running vncviewer, it is a good idea to explicitly set SecurityTypes and not accept any unencrypted traffic.

### On the server

Below is an example invoking vncserver with the -localhost flag:

```
$ vncserver -geometry 1440x900 -alwaysshared -dpi 96 -localhost :1

```

Alternatively, simply add the "localhost" option as a single line in `~/.vnc/config`. Below is the example above in this format:

 `~/.vnc/config` 
```
## Supported server options to pass to vncserver upon invocation can be listed
## in this file. See the following manpages for more: vncserver(1) Xvnc(1).
## Several common ones are shown below. Uncomment and modify to your liking.
geometry=1200x700
alwaysshared
dpi=96
localhost
```

### On the client

With the server now only accepting connection from the localhost, connect to the box via ssh using X-forwarding and the -L switch to enable tunnels. For more on this feature, see the manpage for ssh itself. For example:

```
$ ssh -X 10.1.10.2 -L 5901:localhost:5901

```

This forwards the server port 5901 to the client box also on port 5901\. Note that one does not have to match the port numbers on the server and client. For example:

```
$ ssh -X 10.1.10.2 -L 8900:localhost:5901

```

This forwards the server port 5901 to the client box on port 8900\.

Once connected via SSH, leave that xterm or shell window open since it is acting as the secured tunnel to/from server. To connect via this encrypted tunnel, simply point the vncviewer to the client port on the localhost.

Using the matched ports on the server/client:

```
$ vncviewer localhost:5901

```

Using different ports on the server/client:

```
$ vncviewer localhost:8900

```

### Connecting to a vncserver from Android devices over SSH

To connect to a VNC Server over SSH using an Android device:

```
1\. SSH server running on the machine to connect to.
2\. VNC server running on the machine to connect to. (Run server with -localhost flag as mentioned above)
3\. SSH client on the Android device (ConnectBot is a popular choice and will be used in this guide as an example).
4\. VNC client on the Android device (androidVNC).
```

Consider some dynamic DNS service for targets that do not have static IP addresses.

In ConnectBot, type in the IP and connect to the desired machine. Tap the options key, select Port Forwards and add a new port:

```
Nickname: vnc
Type: Local
Source port: 5901
Destination: 127.0.0.1:5901
```

Save that.

In androidVNC:

```
Nickname: nickname
Password: the password used to set up the VNC server
Address: 127.0.0.1 (we are in local after connecting through SSH)
Port: 5901
```

Connect.

## Tips and tricks

### Connecting to an OSX system

See [https://help.ubuntu.com/community/AppleRemoteDesktop](https://help.ubuntu.com/community/AppleRemoteDesktop). Tested with Remmina.

### Connecting to non-X environments on a Raspberry Pi (Arch ARM)

Install [dispmanx_vnc](https://aur.archlinux.org/packages/dispmanx_vnc/) on the Arch ARM device. Frame rates are not very high but it provides a working VNC access.

### Copying clipboard contents from the remote machine to the local

If copying from the remote machine to the local machine does not work, run autocutsel on the server, as mentioned below [reference](https://bbs.archlinux.org/viewtopic.php?id=101243):

```
$ autocutsel -fork

```

Now press F8 to display the VNC menu popup, and select `Clipboard: local -> remote` option.

One can put the above command in `~/.vnc/xstartup` to have it run automatically when vncserver is started.

### Fix for no mouse cursor

If no mouse cursor is visible when using `x0vncserver`, start vncviewer as follows:

```
$ vncviewer DotWhenNoCursor=1 <server>

```

Or put `DotWhenNoCursor=1` in the tigervnc configuration file, which is at `~/.vnc/default.tigervnc` by default.

### Recommended security settings

**Note:** If using ssh tunnels (i.e. [#Accessing vncserver via SSH tunnels](#Accessing_vncserver_via_SSH_tunnels)), X509Vnc is not required since the encryption is handled by the sshd.

SecurityTypes controls the preferred security algorithms. The default in the current version 1.5.0 is "X509Plain,TLSPlain,X509Vnc,TLSVnc,X509None,TLSNone,VncAuth,None". A more secure alternative is "X509Vnc,TLSVnc", which will disable all unencrypted data traffic.

It is recommended to use X509Vnc, as TLSVnc lacks identity verification.

```
$ vncserver -x509key /path/to/key.pem -x509cert /path/to/cerm.pem -SecurityTypes X509Vnc :1

```

Issuing x509 certificates is beyond the scope of this guide. However, this is expected to be straightforward after the public launch of [Let's Encrypt](https://en.wikipedia.org/wiki/Let%27s_Encrypt "wikipedia:Let's Encrypt"). Alternatively, one can issue certificates using [OpenSSL](/index.php/OpenSSL "OpenSSL") and manually share the keys between server and client using email for instance.

### Toggling Fullscreen

This can be done through vncclient's Menu. By default, vncclient's Menu Key is F8.

### Unable to type '<' character

If pressing `<` on a remote client emits the `>` character, try remapping the incoming key [[1]](https://insaner.com/blog/2013/05.html#20130422063137):

```
$ x0vncserver -RemapKeys="0x3c->0x2c"

```