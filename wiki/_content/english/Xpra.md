From the [Xpra website](http://xpra.org/):

Xpra is '[GNU Screen](/index.php/GNU_Screen "GNU Screen") for X': it allows you to run X programs, usually on a remote host, direct their display to your local machine, and then to disconnect from these programs and reconnect from the same or another machine, without losing any state. It gives you remote access to individual applications.

*   Xpra is "rootless" or "seamless": programs you run under it show up on your desktop as regular programs, managed by your regular window manager.
*   Sessions can be accessed over SSH, or password protected over plain TCP sockets.
*   Xpra is usable over reasonably slow links and does its best to adapt to changing network bandwidth limits. (see also adaptive JPEG mode)
*   Xpra is open-source (GPLv2+), multi-platform and multi-language, with current clients written in Python and Java.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Use](#Use)
    *   [2.1 run application "single shot"](#run_application_"single_shot")
    *   [2.2 run applications in a persistent xpra server on the remote host](#run_applications_in_a_persistent_xpra_server_on_the_remote_host)
    *   [2.3 run whole desktop environment](#run_whole_desktop_environment)
    *   [2.4 shadow remote desktop](#shadow_remote_desktop)
    *   [2.5 as xorg sandbox](#as_xorg_sandbox)
    *   [2.6 more](#more)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Start at boot](#Start_at_boot)
        *   [3.1.1 Server](#Server)
        *   [3.1.2 Client](#Client)
            *   [3.1.2.1 Method 1: .xinitrc](#Method_1:_.xinitrc)
            *   [3.1.2.2 Method 2: systemd user session](#Method_2:_systemd_user_session)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Error: Only console users are allowed to run the X server](#Error:_Only_console_users_are_allowed_to_run_the_X_server)
    *   [4.2 Error: failed to connect to display :100](#Error:_failed_to_connect_to_display_:100)
    *   [4.3 Problem: Fonts are rendered in wrong sizes or clicks will not register after resizing a window](#Problem:_Fonts_are_rendered_in_wrong_sizes_or_clicks_will_not_register_after_resizing_a_window)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the package [xpra](https://www.archlinux.org/packages/?name=xpra) or [xpra-svn](https://aur.archlinux.org/packages/xpra-svn/), on the server and the clients.

**Tip:** If you intend to run Xpra locally under a existing Xorg session with graphic drivers such as `nvidia` or `ATi` you will need to modify the default xpra config. Xpra fetches `-configdir` from `xorg-server-xvfb` which will be `/etc/X11/xorg.conf.d`, therefore you need to change this by following the three bottom steps of [1333056#p1333056](https://bbs.archlinux.org/viewtopic.php?pid=1333056#p1333056) in order to run xpra locally.

## Use

### run application "single shot"

To run an application remotely over ssh without starting an xpra server on the host it's running on in advance, you can simply use this command on your client machine:

 `$ xpra start ssh:user@host --exit-with-children --start-child="command"` 

Where "command" is the command you would start on the remote hosts shell. This will start xpra remotely and shuts down the xpra server when the command exits.

### run applications in a persistent xpra server on the remote host

If you want to have a persistent server on the remote machine, you can start an xpra server on the machine where you want to run the applications (we are using display number **7** here):

 `$ xpra start :7` 

Now you can start an application, e.g. firefox:

 `$ DISPLAY=:7 firefox` 

Or, if you want to start a screen session and execute the programs from there to be able to close the console:

```
$ DISPLAY=:7 screen
[screen starts]
$ firefox
```

Note that if you start `screen` like this you don't have to specify the display number when executing programs. They will be running on the xpra display automatically.

After running these commands, you don't see any windows yet. To actually see the applications on your display, you have to connect to the xpra server. If you are connecting to an xpra display on the same machine, start the xpra client like this:

 `$ xpra attach :7` 

Or, if you are connecting to a remote machine over ssh:

 `$ xpra attach ssh:user@example.com:7` 

After starting the client, any programs running on the remote server display are displayed on your local screen. To detach, type `ctrl-c` or use the command:

 `$ xpra detach ssh:user@example.com:7` 

Programs continue to run on the server and you can reattach again later.

You can stop the server with:

 `$ xpra stop :7` 

on the machine where the server is running, or remotely:

 `$ xpra stop ssh:user@example.com:7` 

### run whole desktop environment

To run whole desktop (on the server side):

 `$ xpra start-desktop :7 --start-child=xfce4-session --exit-with-children` 

where:

*   `:7` is a number of xorg DISPLAY session
*   `--start-child=xfce4-session` run xfce4 session as child on xpra server
*   `--exit-with-children` mean that server will be closed after session logout (children exit)

To attach it (on the server side):

 `$ xpra attach :7` 

To attach it (on the client side):

 `$ xpra attach ssh:user@example.com:7` 

To detach press ctrl+c on terminal or run:

 `$ xpra detach :7` 
**Tip:** Screen resolution can be changed with [xrandr](/index.php/Xrandr "Xrandr").

### shadow remote desktop

To clone:

*   display must be auth by this same user as ssh login to
*   display must be shown on remote screen

To shadow desktop run this on the client side:

 `$ xpra shadow ssh:DISPLAY_user@example.com:DISPLAY_number` 

### as xorg sandbox

Sandox can be achieved with [firejail](/index.php/Firejail "Firejail"):

*   for application sandbox (change `eth0` to your interface name or to `none`):

 `$ firejail --x11=xpra --net=eth0 firefox` 

*   xpra attach, etc:

 `$ firejail --net=eth0 xpra [...]` 
**Note:** `--net=eth0` creates a separate namespace for the network. This is necessary to hide all xorg or system sockets from xpra, otherwise a sandbox is most likely ineffective ([issue-54#153757284](https://github.com/netblue30/firejail/issues/57#issuecomment-153757284)).

### more

For a complete manual, check `man xpra`.

## Tips and tricks

### Start at boot

#### Server

It is possible to start the xpra server at boot using a [systemd](/index.php/Systemd "Systemd") unit.

Create the unit file:

 `/etc/systemd/system/xpra@.service` 
```
[Unit]
Description=xpra display

[Service]
Type=simple
User=%i
EnvironmentFile=/etc/conf.d/xpra
ExecStart=/usr/bin/xpra --no-daemon start ${%i}

[Install]
WantedBy=multi-user.target

```

Now create the configuration, adding a line for each username you want to have an xpra display:

 `/etc/conf.d/xpra` 
```
myusername=:7

```

[Enable the service](/index.php/Daemons "Daemons") for each username that owns a display. In this example, the service would be `xpra@myusername.service`.

#### Client

**Note:** If the client is a remote machine, first of all use SSH keys to be able to connect to the server without typing a password. Read [SSH keys](/index.php/SSH_keys "SSH keys") for more details.

##### Method 1: .xinitrc

Add to your `~/.xinitrc` file the line necessary to start the connection, adding an **&** at the end of the line.

Make sure to add such line **before** the `exec` line.

For example, on a remote client it could be:

 `~/.xinitrc` 
```
xpra attach ssh:user@example.com:7 &

```

##### Method 2: systemd user session

Configure your session to use **systemd user session**. Read [Systemd/User](/index.php/Systemd/User "Systemd/User") for details.

**Note:** Make sure you understand the difference between **systemd user session** services, and regular **systemd** services. Again, read the [Systemd/User](/index.php/Systemd/User "Systemd/User") for details.

Create the following service unit:

 `$HOME/.config/systemd/user/xpra-client@.service` 
```
[Unit]
Description=xpra client

[Service]
Type=simple
EnvironmentFile=%h/.config/conf/xpra_client
ExecStart=/usr/bin/xpra attach %i $OPTS

[Install]
WantedBy=default.target

```

Create the configuration file, using the options you want:

 `$HOME/.config/conf/xpra_client` 
```
OPTS=--encoding=jpeg --quality=90

```

The service name would be in the format of `xpra-client@*ssh:username@hostname**:<display number>***.service`.

Example:

 `xpra-client@ssh:myuser@example.com:7.service` 

[Enable that service](/index.php/Daemons "Daemons"), and remember to use the `--user` flag on `systemctl`.

## Troubleshooting

### Error: Only console users are allowed to run the X server

If the execution fails with this error message in the log file you need to make the following changes:

Create the file /etc/X11/Xwrapper.config with the content

 `/etc/X11/Xwrapper.config` 
```
allowed_users=anybody

```

### Error: failed to connect to display :100

Sometimes this errors are produced:

 `/run/user/1000/xpra/:100.log` 
```
(EE) Fatal server error:
(EE) parse_vt_settings: Cannot open /dev/tty0 (Permission denied)
(EE) Server terminated with error (1). Closing log file.

```

To solve it is necessary run with `--xvfb=/usr/bin/Xorg`. Example:

 `xpra start ssh://$USER@$SERVER/100 --start-child=/usr/bin/terminator --xvfb=/usr/bin/Xorg` 

### Problem: Fonts are rendered in wrong sizes or clicks will not register after resizing a window

Try to install the [xf86-video-dummy-xpra-patch](https://aur.archlinux.org/packages/xf86-video-dummy-xpra-patch/) package, if you encounter problems with font rendering or missed clicks after resizing a remote window. It contains the xf86-video-dummy driver with patches from the xpra team, that are meant to help with these problems.

**Tip:** If font rendering is either too big or too small, try experimenting with the --dpi setting of xpra. The default is --dpi 96\. Bigger values mean larger font rendering, lower values make font rendering smaller.

For the patches and further information see:

*   [xpra wiki article about the Xdummy driver](https://xpra.org/trac/wiki/Xdummy)
*   [xpra wiki article about dpi settings](https://xpra.org/trac/wiki/DPI)

## See also

*   [Xpra website](http://xpra.org/)