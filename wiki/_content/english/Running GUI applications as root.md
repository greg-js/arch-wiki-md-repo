**Warning:** All of the following methods have security implications that users should be aware of. As put by Emmanuele Bassi, a GNOME developer: "*there are no *real*, substantiated, technological reasons why anybody should run a GUI application as root. By running GUI applications as an admin user you're literally running millions of lines of code that have not been audited properly to run under elevated privileges; you're also running code that will touch files inside your $HOME and may change their ownership on the file system; connect, via IPC, to even more running code, etc. You're opening up a massive, gaping security hole [...].*"[[1]](https://bugzilla.gnome.org//show_bug.cgi?id=772875#c5)

Avoid running graphical applications as [root](/index.php/Root_user "Root user") if possible, see [#Circumvent running graphical apps as root](#Circumvent_running_graphical_apps_as_root).

## Contents

*   [1 Circumvent running graphical apps as root](#Circumvent_running_graphical_apps_as_root)
    *   [1.1 sudoedit](#sudoedit)
    *   [1.2 GVFS](#GVFS)
*   [2 Xorg](#Xorg)
    *   [2.1 Punctual methods](#Punctual_methods)
    *   [2.2 Alternate methods](#Alternate_methods)
        *   [2.2.1 Xhost](#Xhost)
        *   [2.2.2 Permanently allow root access](#Permanently_allow_root_access)
*   [3 Wayland](#Wayland)
    *   [3.1 Using xhost](#Using_xhost)

## Circumvent running graphical apps as root

### sudoedit

To edit files as root, use [sudoedit](/index.php/Sudoedit "Sudoedit").

### GVFS

Access to privileged files and directories is possible through [GVFS](/index.php/GVFS "GVFS") by specifying the `admin` [backend](https://wiki.gnome.org/Projects/gvfs/backends) in the URI scheme[[2]](https://bugzilla.redhat.com/show_bug.cgi?id=1274451#c27)[[3]](https://bugzilla.gnome.org//show_bug.cgi?id=772875#c2), e.g.:

```
$ nautilus admin:///root/

```

or

```
$ gedit admin:///etc/fstab

```

**Tip:** This can also be done from the application location bar/file selector: e.g. in [nautilus](https://www.archlinux.org/packages/?name=nautilus) or [gedit](https://www.archlinux.org/packages/?name=gedit), type `Ctrl+l` and then prepend the `admin://` scheme to the resource path. The same effect can be attained via the [Other locations](https://wiki.gnome.org/Apps/Files?action=AttachFile&do=get&target=network.png) server address bar.

## Xorg

By default, and for security reasons, root will be unable to connect to a non-root user's [X server](/index.php/X_server "X server"). There are multiple ways of allowing root to do so however, if necessary.

The proper, recommended way to run GUI apps under X with elevated privileges is to create a [Polkit](/index.php/Polkit "Polkit") policy, as shown in [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=999328#p999328). This should however "*only be used for legacy programs*", as [pkexec(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pkexec.1) reminds. Applications should rather "*defer the privileged operations to an auditable, self-contained,* minimal *piece of code that gets executed after doing a privilege escalation, and gets dropped when not needed*"[[4]](https://bugzilla.gnome.org//show_bug.cgi?id=772875#c5). This may be the object of a bug report to the upstream project.

### Punctual methods

Those methods wrap the application in an elevation framework and drop the acquired privileges once it exits:

*   [kdesu](https://www.archlinux.org/packages/?name=kdesu), [kdesu(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/kdesu.1)

```
$ kdesu *application*

```

*   [sudo](/index.php/Sudo "Sudo") (must be [properly configured](/index.php/Sudo#Configuration "Sudo"))

```
$ sudo *application*

```

*   [sux](https://aur.archlinux.org/packages/sux/) (wrapper around su which will transfer your X credentials)

```
$ sux root *application*

```

### Alternate methods

These methods will allow root to connect to a non-root user's X server, but present varying levels of security risks, especially if you run ssh. If you are behind a firewall, you may consider them to be safe enough for your requirements.

#### Xhost

[Xhost](/index.php/Xhost "Xhost") can be used to temporarily allow root access.

#### Permanently allow root access

	**Method 1**: Add the line

```
session         optional        pam_xauth.so

```

to `/etc/pam.d/su` and `/etc/pam.d/su-l`. Then switch to your root user using 'su' or 'su -'.

	**Method 2**: Globally in `/etc/profile`

Add the following line to `/etc/profile`:

```
export XAUTHORITY=/home/non-root-usersname/.Xauthority

```

This will permanently allow root to connect to a non-root user's X server.

Or, merely specify a particular app:

```
export XAUTHORITY=/home/usersname/.Xauthority kwrite

```

(to allow root to access kwrite, for instance.)

## Wayland

Trying to run a graphical application as root via [su](/index.php/Su "Su"), [sudo](/index.php/Sudo "Sudo") or [pkexec](/index.php/Polkit "Polkit") in a Wayland session (e.g. [GParted](/index.php/GParted "GParted") or [Gedit](/index.php/Gedit "Gedit")), will fail with an error similar to this:

```
$ sudo gedit
No protocol specified
Unable to init server: Could not connect: Connection refused

(gedit:2349): Gtk-WARNING **: cannot open display: :0

```

Before Wayland, running GUI applications with elevated privileges could be properly implemented by creating a [Polkit](/index.php/Polkit "Polkit") policy, or more dangerously done by running the command in a terminal by prepending the command with `sudo`; but under (X)Wayland this does not work anymore as the default has been made to only allow the user who started the X server to connect clients to it (see the [bug report](https://bugzilla.redhat.com/show_bug.cgi?id=1266771) and [the](https://cgit.freedesktop.org/xorg/xserver/commit/?id=c4534a3) [upstream](https://cgit.freedesktop.org/xorg/xserver/commit/?id=4b4b908) [commits](https://cgit.freedesktop.org/xorg/xserver/commit/?id=76636ac) it refers to).

Avoid running graphical applications as root if possible, see [#Circumvent running graphical apps as root](#Circumvent_running_graphical_apps_as_root).

A more versatile though more insecure workaround allows any graphical application to be run as root [#Using xhost](#Using_xhost).

### Using xhost

A more versatile —though much less secure— workaround is to use [xhost](/index.php/Xhost "Xhost") to temporarily allow the root user to access the local user's X session[[5]](https://bugzilla.redhat.com/show_bug.cgi?id=1274451#c64). To do so, execute the following command as the current (unprivileged) user:

```
$ xhost si:localuser:root

```

To remove this access after the application has been closed:

```
$ xhost -si:localuser:root

```