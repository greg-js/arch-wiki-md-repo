Related articles

*   [TigerVNC](/index.php/TigerVNC "TigerVNC")

[x11vnc](https://en.wikipedia.org/wiki/x11vnc "wikipedia:x11vnc") is a VNC server, it allows one to view remotely and interact with real X displays (i.e. a display corresponding to a physical monitor, keyboard, and mouse) with any VNC viewer. While it is not developed any longer by its original author Karl Runge, *LibVNC* and the GitHub community have taken over the development.

*x11vnc* does not create an extra display (or X desktop) for remote control. Instead, it shows in real time the existing X11 display, unlike *Xvnc*, part of [TigerVNC](/index.php/TigerVNC "TigerVNC"), which is an alternatives VNC server available in the [official repositories](/index.php/Official_repositories "Official repositories").

Also note that x11vnc is not shipped with a client viewer. Any VNC viewer should do the job and be compatible with the x11vnc server while not necessarily using all its functionalities. TigerVNC's *vncviewer* is a recommended client.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Setting up x11vnc](#Setting_up_x11vnc)
    *   [1.1 Installation](#Installation)
    *   [1.2 Starting](#Starting)
        *   [1.2.1 Setting X authority](#Setting_X_authority)
            *   [1.2.1.1 Start X](#Start_X)
            *   [1.2.1.2 Running from xinetd](#Running_from_xinetd)
            *   [1.2.1.3 GDM](#GDM)
            *   [1.2.1.4 Lightdm](#Lightdm)
            *   [1.2.1.5 LXDM](#LXDM)
            *   [1.2.1.6 SDDM](#SDDM)
            *   [1.2.1.7 SLIM](#SLIM)
    *   [1.3 Setting a password](#Setting_a_password)
    *   [1.4 Running constantly](#Running_constantly)
    *   [1.5 Accessing](#Accessing)
*   [2 SSH Tunnel](#SSH_Tunnel)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Screensaver problem](#Screensaver_problem)
    *   [3.2 IPv6 port different from IPv4 port](#IPv6_port_different_from_IPv4_port)
*   [4 See also](#See_also)

## Setting up x11vnc

### Installation

Install [x11vnc](https://www.archlinux.org/packages/?name=x11vnc) from the official repositories.

### Starting

First, start X either by *startx* or through a [display manager](/index.php/Display_manager "Display manager"). You may need to set up X to [run headless](/index.php/Headless_With_X "Headless With X") too.

Then, run the following command, all available options are explained in [x11vnc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/x11vnc.1).

```
$ x11vnc -display :0

```

Another option is to place the x11vnc command line in a script which is called at login, for example:

```
x11vnc -wait 50 -noxdamage -passwd PASSWORD -display :0 -forever -o /var/log/x11vnc.log -bg

```

**Note:** The password "PASSWORD" above is not secured; anyone who can run `ps` on the machine will see it. Also note that `/var/log/x11vnc.log` needs to be created manually and its ownership needs to match that of the user who will run it.

#### Setting X authority

You may set an X authority file for the VNC server. This is accomplished by using the `-auth` argument followed by the appropriate file, which will depend on how your X server was started. Generally, assigning an X authority file requires running *x11vnc* as root.

##### Start X

```
$ x11vnc -display :0 -auth ~/.Xauthority

```

If that fails, you may have to run instead (as root):

```
# x11vnc -display :0 -auth /home/*user*/.Xauthority

```

Where *user* is the username of the user who is running the X server.

##### Running from xinetd

X11vnc can be run using a xinetd service, which only starts X11vnc once a user connects.

Create an xinetd service entry for x11vnc, for example:

 `/etc/xinetd/x11vnc` 
```
service x11vncservice
{
       port            = 5900
       type            = UNLISTED
       socket_type     = stream
       protocol        = tcp
       wait            = no
       user            = root
       server          = /usr/bin/x11vnc
       server_args     = -inetd -o /var/log/x11vnc.log -noxdamage -display :0 -auth guess
       disable         = no
}

```

After reloading `xinetd.service`, X11vnc will start once a client connects to port 5900.

##### GDM

**Note:** Newer GDM packages ship with Xwayland as the default display server backend. The following instructions, however, only apply when using Xorg (else `.Xauthority` is not created, and *x11vnc* fails to start). You are therefore advised to uncomment `#WaylandEnable=false` setting in `/etc/gdm/custom.conf` in order to proceed.

```
# x11vnc -display :0 -auth /var/lib/gdm/:0.Xauth

```

Newer versions of GDM uses /run/user. Example for user 120 (gdm), used for login screen.

```
# x11vnc -display :0 -auth /run/user/120/gdm/Xauthority

```

or see [Troubleshooting](#Troubleshooting) section below

##### Lightdm

```
# x11vnc -display :0 -auth /var/run/lightdm/root/\:0

```

##### LXDM

```
# x11vnc -display :0 -auth /var/run/lxdm/lxdm-\:0.auth

```

##### SDDM

SDDM uses an unpredictable UUID for the auth file [[1]](https://github.com/sddm/sddm/issues/622) therefore one needs to:

```
# x11vnc -display :0 -auth $(find /var/run/sddm/ -type f)

```

Embedding this into a systemd .service file will require a trick to evaluate the find command as shown here [[2]](https://gist.github.com/nickjacob/9909574).

##### SLIM

```
# x11vnc -display :0 -auth /var/run/slim.auth

```

**Warning:** This will set up VNC with NO PASSWORD. This means that ANYBODY who has access to the network the computer is on CAN SEE YOUR XSERVER. It is a fairly simple matter to tunnel your VNC connection through SSH to avoid this. Or, simply set a password, as described below.

**Note:** The password will only encrypt the login process itself. The transmission is still unencrypted[[3]](http://security.web.cern.ch/security/ssh/encrypt_vnc.htm).

### Setting a password

Running:

```
$ x11vnc -usepw

```

uses the password found in `~/.vnc/passwd`, where the password is obscured with a fixed key in a VNC compatible format, or alternatively in `~/.vnc/passwdfile`, where the first line of the file contains the password. If none of these files can be located, it prompts the user for a password which is saved in `~/.vnc/passwd` and is used right away.

The VNC viewer should then prompt for a password when connecting.

### Running constantly

By default, x11vnc will accept the first VNC session and shutdown when the session disconnects. In order to avoid that, start x11vnc with either the `-many` or the `-forever` argument, like this:

```
$ x11vnc -many -display :0

```

It is also possible to use the following command :

```
$ x11vnc --loop

```

this will restart the server once the session is finished

### Accessing

Get a VNC client on another computer, and type in the IP address of the computer running x11vnc. Hit connect, and you should be set.

If you are attempting to access a VNC server / computer (running x11vnc) from outside of its network then you will need to ensure that it has port 5900 forwarded.

## SSH Tunnel

You need to have [SSH](/index.php/SSH "SSH") installed and configured.

Use the `-localhost` flag with x11vnc for it to bind to the local interface. Once that is done, you can use SSH to tunnel the port; then, connect to VNC through SSH.

Simple example (from [http://www.karlrunge.com/x11vnc/index.html#tunnelling](http://www.karlrunge.com/x11vnc/index.html#tunnelling) ):

```
$ ssh -t -L 5900:localhost:5900 remote_host 'x11vnc -localhost -display :0'

```

(You will likely have to provide passwords/passphrases to login from your current location into your remote_host Unix account; we assume you have a login account on remote_host and it is running the SSH server)

And then in another terminal window on your current machine run the command:

```
$ vncviewer -PreferredEncoding=ZRLE localhost:0

```

## Troubleshooting

1\. You can check your ip address and make sure port 5900 is forwarded by visiting [this](http://www.realvnc.com/cgi-bin/nettest.cgi) website.

2\. Tested only on [GNOME](/index.php/GNOME "GNOME") + [GDM](/index.php/GDM "GDM")

If you cannot start the tunnel, and get error like XOpenDisplay(":0") failed, Check if you have a `~/.Xauthority` directory. If that does not exist, You can create one easily (Actually a symlink to actual one) by running command given below as normal user NOT ROOT OR USING [Sudo](/index.php/Sudo "Sudo") as below:

```
$ ln -sv $(dirname $(xauth info | awk '/Authority file/{print $3}')) ~/.Xauthority

```

then try above [tunneling](#SSH_Tunnel) example and it should work fine. Further if you want this to be automatically done each time [Xorg](/index.php/Xorg "Xorg") is restarted, create the [xprofile](/index.php/Xprofile "Xprofile") file & make is executable as below

```
$ ln -sf $(dirname $(xauth info | awk '/Authority file/{print $3}')) ~/.Xauthority

```

3. **GNOME 3** and **x11vnc**

If you are using GNOME 3 and x11vnc and you get the following errors

```
*** XOpenDisplay failed (:0) 

*** x11vnc was unable to open the X DISPLAY: ":0", it cannot continue.

```

Try running x11vnc like

```
$ x11vnc -noxdamage -many -display :0 -auth /var/run/gdm/$(sudo ls /var/run/gdm | grep $(whoami))/database -forever -bg

```

Please update if this works / not works for any other [display manager](/index.php/Display_manager "Display manager") or [desktop environment](/index.php/Desktop_environment "Desktop environment").

### Screensaver problem

If screensaver starts every 1-2 second, start x11vnc with `-nodpms` key.

### IPv6 port different from IPv4 port

The default behavior for the command:

```
$ x11vnc -display :0 -rfbport 5908

```

is for the server to listen to TCP port 5908 and TCP6 port 59**00**. For the server to listen to the same TCP6 port, also use the `-rfbportv6` option to force the IPv6 listening port. For example:

```
$ x11vnc -display :0 -rfbport 5908 -rfbportv6 5908

```

## See also

*   [original author site](http://www.karlrunge.com/x11vnc/)
*   [https://github.com/LibVNC/x11vnc](https://github.com/LibVNC/x11vnc)
*   [Wikipedia:x11vnc](https://en.wikipedia.org/wiki/x11vnc "wikipedia:x11vnc")