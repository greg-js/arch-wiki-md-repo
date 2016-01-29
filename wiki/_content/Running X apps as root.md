# Running X apps as root

By default, and for security reasons, root will be unable to connect to a non-root user's X server. There are multiple ways of allowing root to do so, if it is necessary.

## The most secure methods

The most secure methods are simple. They include:

*   kdesu (included with KDE)

```
$ kdesu _name-of-app_

```

*   gksu (included with GNOME)

```
$ gksu _name-of-app_

```

*   bashrun (in community)

```
$ bashrun --su _name-of-app_

```

*   [sudo](/index.php/Sudo "Sudo") (must be installed and properly configured with `visudo`)

```
$ sudo _name-of-app_

```

*   [sux](https://aur.archlinux.org/packages/sux/)<sup><small>AUR</small></sup> (wrapper around su which will transfer your X credentials)

```
$ sux root _name-of-app_

```

These are the preferred methods, because they automatically exit when the application exits, negating any security risks quite completely.

## Alternate methods

These methods will allow root to connect to a non-root user's X server, but present varying levels of security risks, especially if you run ssh. If you are behind a firewall, you may consider them to be safe enough for your requirements.

*   **Temporarily allow root access**

NaN

```
$ xhost +

```

will temporarily allow root, or _anyone_ to connect your X server. Likewise,

```
$ xhost -

```

will disallow this function afterward.

Some users also use:

```
$ xhost + localhost

```

(Your X server must be configured to listen to TCP connections for `xhost + localhost` to work).

*   **Permanently allow root access**

NaN

`session optional pam_xauth.so`

to `/etc/pam.d/su` and `/etc/pam.d/su-l`. Then switch to your root user using 'su' or 'su -'.

NaN

Add the following to `/etc/profile`

```
export XAUTHORITY=/home/non-root-usersname/.Xauthority

```

This will permanently allow root to connect to a non-root user's X server.

Or, merely specify a particular app:

```
export XAUTHORITY=/home/usersname/.Xauthority kwrite

```

(to allow root to access kwrite, for instance.)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Running_X_apps_as_root&oldid=387977](https://wiki.archlinux.org/index.php?title=Running_X_apps_as_root&oldid=387977)"