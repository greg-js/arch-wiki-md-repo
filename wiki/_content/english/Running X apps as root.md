By default, and for security reasons, root will be unable to connect to a non-root user's [X server](/index.php/X_server "X server"). There are multiple ways of allowing root to do so however, if necessary.

**Warning:** All of the following methods have security implications that users should be aware of. Running GUI applications as root allows to execute a lot of code which is not audited properly for running under elevated priviledges. This may be a huge security hole.

The proper, recommended way to run GUI apps under X with elevated privileges is to create a [Polkit](/index.php/Polkit "Polkit") policy, as shown in [this forum post](https://bbs.archlinux.org/viewtopic.php?pid=999328#p999328). This should however "*only be used for legacy programs*", as [pkexec(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pkexec.1) reminds. Applications should rather "*defer the privileged operations to an auditable, self-contained,* minimal *piece of code that gets executed after doing a privilege escalation, and gets dropped when not needed*"[[1]](https://bugzilla.gnome.org//show_bug.cgi?id=772875#c5). This may be the object of a bug report to the upstream project.

## Contents

*   [1 Punctual methods](#Punctual_methods)
*   [2 Alternate methods](#Alternate_methods)
    *   [2.1 Temporarily allow root access](#Temporarily_allow_root_access)
    *   [2.2 Permanently allow root access](#Permanently_allow_root_access)
*   [3 Wayland](#Wayland)

## Punctual methods

Those methods wrap the application in an elevation framework and drop the acquired privileges once it exits:

*   [kdesu](https://www.archlinux.org/packages/?name=kdesu)

```
$ kdesu *name-of-app*

```

See also [Sudo#kdesu](/index.php/Sudo#kdesu "Sudo").

*   [gksu](/index.php/Sudo#gksu "Sudo")

**Warning:** *gksu* has been deprecated since 2011[[2]](https://bugzilla.gnome.org//show_bug.cgi?id=772875#c5), and has not seen any update since 2014[[3]](https://www.archlinux.org/packages/?name=gksu).

```
$ gksu *name-of-app*

```

See also [Sudo#gksu](/index.php/Sudo#gksu "Sudo").

*   [bashrun](https://www.archlinux.org/packages/?name=bashrun) (in community)

```
$ bashrun --su *name-of-app*

```

*   [sudo](/index.php/Sudo "Sudo") (must be installed and properly configured with `visudo`)

```
$ sudo *name-of-app*

```

*   [sux](https://aur.archlinux.org/packages/sux/) (wrapper around su which will transfer your X credentials)

```
$ sux root *name-of-app*

```

## Alternate methods

These methods will allow root to connect to a non-root user's X server, but present varying levels of security risks, especially if you run ssh. If you are behind a firewall, you may consider them to be safe enough for your requirements.

### Temporarily allow root access

See [Xhost](/index.php/Xhost "Xhost").

### Permanently allow root access

	**Method 1**: Add the line

`session optional pam_xauth.so`

to `/etc/pam.d/su` and `/etc/pam.d/su-l`. Then switch to your root user using 'su' or 'su -'.

	**Method 2**: Globally in `/etc/profile`

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

## Wayland

If you are running wayland, you'll find that the fallback X server won't work when running programs as root. Try running `xhost +local:` first.