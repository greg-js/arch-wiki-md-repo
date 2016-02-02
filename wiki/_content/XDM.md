# XDM

Related articles

*   [Display manager](/index.php/Display_manager "Display manager")

From [XDM manual page](http://www.xfree86.org/current/xdm.1.html):

	_Xdm manages a collection of X displays, which may be on the local host or remote servers. The design of xdm was guided by the needs of X terminals as well as The Open Group standard XDMCP, the X Display Manager Control Protocol. Xdm provides services similar to those provided by init, getty and login on character terminals: prompting for login name and password, authenticating the user, and running a "session."_

XDM provides a simple and straightforward graphical login prompt.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Defining the session](#Defining_the_session)
    *   [2.2 Theming](#Theming)
        *   [2.2.1 Background wallpaper](#Background_wallpaper)
        *   [2.2.2 Font](#Font)
        *   [2.2.3 Login dialog positioning](#Login_dialog_positioning)
        *   [2.2.4 Removing the logo](#Removing_the_logo)
    *   [2.3 Multiple X sessions & Login in the window](#Multiple_X_sessions_.26_Login_in_the_window)
    *   [2.4 Passwordless login](#Passwordless_login)

## Installation

[Install](/index.php/Install "Install") the [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm) package. Then [enable](/index.php/Enable "Enable") `xdm.service`.

If you would like to use an Arch Linux theme for XDM, you can optionally install the [xdm-archlinux](https://www.archlinux.org/packages/?name=xdm-archlinux) package. If installing the latter package, then do **not** enable `xdm.service`, but instead enable `xdm-archlinux.service`.

## Configuration

### Defining the session

Unlike many more modern [display managers](/index.php/Display_manager "Display manager") such as [GDM](/index.php/GDM "GDM") or [LightDM](/index.php/LightDM "LightDM"), XDM does not source available sessions from .desktop files located in the `/usr/share/xsessions` directory. As such, XDM does not have a 'session menu.' Instead, XDM will execute the `.xinitrc` file in the home directory. See [Xinitrc#Configuration](/index.php/Xinitrc#Configuration "Xinitrc") for details.

Ensure that the `.xinitrc` file in your home directory is executable. To do this use the following command:

```
$ chmod 744 ~/.xinitrc

```

### Theming

For the exact meanings of the options discussed below, see the manual page of xdm. The configuration file is located in `/etc/X11/xdm/Xresources`, notice that if you installed [xdm-archlinux](https://www.archlinux.org/packages/?name=xdm-archlinux) the configuration file will instead be located in `/etc/X11/archlinux/xdm/Xresources`.

#### Background wallpaper

You can use a program such as [qiv](https://www.archlinux.org/packages/?name=qiv) to set the background in XDM:

*   Install [qiv](https://www.archlinux.org/packages/?name=qiv)

*   Make a directory to store background images, e.g. `/root/backgrounds` or `/usr/local/share/backgrounds`

*   Place your images in the directory.

*   Edit `/etc/X11/xdm/Xsetup_0`. Change the `xconsole` command to:

```
 /usr/bin/qiv -zr /root/backgrounds/*

```

#### Font

*   Edit `/etc/X11/xdm/Xresources`. Add/replace the following defines:

```
 xlogin**greetFont:  -adobe-helvetica-bold-o-normal--20-**-**-**-**-**-iso8859-1
 xlogin**font:       -adobe-helvetica-medium-r-normal--14-**-**-**-**-**-iso8859-1
 xlogin**promptFont: -adobe-helvetica-bold-r-normal--14-**-**-**-**-**-iso8859-1
 xlogin**failFont:   -adobe-helvetica-bold-r-normal--14-**-**-**-**-**-iso8859-1

```

#### Login dialog positioning

This configuration will move the login dialog to the bottom right of the screen.

```
 xlogin*frameWidth: 1
 xlogin*innerFramesWidth: 1
 xlogin*logoPadding: 0
 xlogin*geometry:    300x175-0-0

```

#### Removing the logo

Comment out the logo defines:

```
 #xlogin*logoFileName: /usr/X11R6/lib/X11/xdm/pixmaps/xorg.xpm
 #xlogin*logoFileName: /usr/X11R6/lib/X11/xdm/pixmaps/xorg-bw.xpm

```

### Multiple X sessions & Login in the window

With the [Xdmcp](/index.php/Xdmcp "Xdmcp") enable, you can easily run multiple X sessions simultaneously on the same machine.

```
# X -query ip_xdmcp_server :2

```

This will launch the second session, in window you need [xorg-server-xephyr](https://www.archlinux.org/packages/?name=xorg-server-xephyr)

```
# Xephyr -query this_machine_ip :2

```

### Passwordless login

In order to enable passwordless login for XDM, add the line below to `/etc/X11/xdm/Xresources`:

```
xlogin*allowNullPasswd: true

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=XDM&oldid=414368](https://wiki.archlinux.org/index.php?title=XDM&oldid=414368)"