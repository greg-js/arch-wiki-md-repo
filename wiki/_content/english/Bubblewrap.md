Related articles

*   [Security](/index.php/Security "Security")
*   [Flatpak](/index.php/Flatpak "Flatpak")

[bubblewrap](https://github.com/projectatomic/bubblewrap) is a lightweight [setuid](https://en.wikipedia.org/wiki/Setuid "wikipedia:Setuid") sandbox application developed from [Flatpak](https://en.wikipedia.org/wiki/Flatpak "wikipedia:Flatpak") with a small installation footprint and minimal resource requirements. While the application package is named bubblewrap, the actual executable binary and manpage reference is *bwrap*. bubblewrap is expected to [anchor the sandbox mechanism](https://blog.torproject.org/blog/q-and-yawning-angel) of the [Tor Browser](https://www.torproject.org/projects/torbrowser.html) (Linux) in the future. Notable features include support for cgroup/IPC/mount/network/PID/user/UTS [namespaces](https://en.wikipedia.org/wiki/Linux_namespaces "wikipedia:Linux namespaces") and [seccomp](https://en.wikipedia.org/wiki/Seccomp "wikipedia:Seccomp") filtering. Note that bubblewrap drops all [capabilities](/index.php/Capabilities "Capabilities") within a sandbox and that child tasks cannot gain greater privileges than its parent. Notable feature exclusions include the lack of explicit support for blacklisting/whitelisting file paths.

**Warning:** Unlike when using a separate user and a separate log-in session, bubblewrap not only exposes security vulnerabilities in the kernel but also in the window compositor. Users should be aware that running untrustworthy code in bubblewrap is still not safe.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage examples](#Usage_examples)
    *   [3.1 No-op](#No-op)
    *   [3.2 Bash](#Bash)
    *   [3.3 dhcpcd](#dhcpcd)
    *   [3.4 Unbound](#Unbound)
    *   [3.5 Desktop](#Desktop)
    *   [3.6 MuPDF](#MuPDF)
    *   [3.7 p7zip](#p7zip)
    *   [3.8 Filesystem isolation](#Filesystem_isolation)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Using X11](#Using_X11)
    *   [4.2 Sandboxing X11](#Sandboxing_X11)
    *   [4.3 Opening URLs from wrapped applications](#Opening_URLs_from_wrapped_applications)
    *   [4.4 New Session](#New_Session)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [bubblewrap](https://www.archlinux.org/packages/?name=bubblewrap) or [bubblewrap-git](https://aur.archlinux.org/packages/bubblewrap-git/).

**Note:** For information about [user_namespaces(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/user_namespaces.7) support in Archlinux kernels see [Security#Sandboxing applications](/index.php/Security#Sandboxing_applications "Security").

## Configuration

bubblewrap can be called directly from the command-line and/or within [shell scripts](https://github.com/projectatomic/bubblewrap/blob/master/demos/bubblewrap-shell.sh) as part of a [complex wrapper](https://github.com/projectatomic/bubblewrap/blob/master/demos/flatpak-run.sh). Unlike applications such as [Firejail](/index.php/Firejail "Firejail") which automatically set `/var` and `/etc` to read-only within the sandbox, bubblewrap makes no such operating assumptions. It is up to the user to determine which configuration options to pass in accordance to the application being sandboxed. bubblewrap does not automatically create user namespaces when running with setuid privileges and can accomodate typical environment variables including `$HOME` and `$USER`.

## Usage examples

### No-op

A no-op bubblewrap invocation is as follows:

```
$ bwrap --dev-bind / / bash

```

This will spawn a bash process which should behave exactly as outside a sandbox. If a sandboxed program misbehaves, you may want to start from the above no-op invocation, and work your way towards a more secure configuration step-by-step.

### Bash

Create a simple [Bash](/index.php/Bash "Bash") sandbox:

*   Determine available kernel namespaces

```
$ ls /proc/self/ns 
cgroup  ipc  mnt  net  pid  user uts

```

**Note:** The presence of `user` indicates that the kernel has exposed support for user namespaces with `CONFIG_USER_NS=y`

*   Bind as read-only the entire host `/` directory to `/` in the sandbox
*   Create a new user namespace and set the [user ID](https://en.wikipedia.org/wiki/User_identifier "wikipedia:User identifier") to `256` and the [group ID](https://en.wikipedia.org/wiki/Group_identifier "wikipedia:Group identifier") to `512`

```
$ bwrap --ro-bind / / --unshare-user --uid 256 --gid 512 bash
bash-4.4$ id
uid=256 gid=512 groups=512,65534(nobody)
bash-4.4$ ls -l /usr/bin/bash
-rwxr-xr-x 1 nobody nobody 811752 2017-01-01 04:20 /usr/bin/bash

```

### dhcpcd

Create a simple [dhcpcd](/index.php/Dhcpcd "Dhcpcd") sandbox:

*   Determine available kernel namespaces

```
$ ls /proc/self/ns 
cgroup  ipc  mnt  net  pid  uts

```

**Note:** The absence of `user` indicates that the kernel has been built with `CONFIG_USER_NS=n` or is user namespace restricted.

*   Bind as read-write the entire host `/` directory to `/` in the sandbox
*   Mount a new devtmpfs filesystem to `/dev` in the sandbox
*   Create new [IPC](https://en.wikipedia.org/wiki/Inter-process_communication "wikipedia:Inter-process communication") and [control group](/index.php/Control_group "Control group") namespaces
*   Create a new UTS namespace and set `dhcpcd` as the hostname

```
# /usr/bin/bwrap --bind / / --dev /dev --unshare-ipc --unshare-cgroup --unshare-uts --hostname dhcpcd /usr/bin/dhcpcd -q -b

```

### Unbound

Create a more granular and complex [Unbound](/index.php/Unbound "Unbound") sandbox:

*   Bind as read-only the system `/usr` directory to `/usr` in the sandbox
*   Create a symbolic link from the system `/usr/lib` directory to `/lib64` in the sandbox
*   Bind as read-only the system `/etc` directory to `/etc` in the sandbox
*   Create empty `/var` and `/run` directories within the sandbox
*   Mount a new devtmpfs filesystem to `/dev` in the sandbox
*   Create new IPC and [PID](https://en.wikipedia.org/wiki/Process_identifier "wikipedia:Process identifier") and control group namespaces
*   Create a new UTS namespace and set `unbound` as the hostname

```
# /usr/bin/bwrap --ro-bind /usr /usr --symlink usr/lib /lib64 --ro-bind /etc /etc --dir /var --dir /run --dev /dev --unshare-ipc --unshare-pid --unshare-cgroup --unshare-uts --hostname unbound /usr/bin/unbound -d

```

**Tip:** See [systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd") to enable the bubblewrapping of systemd unit files including `unbound.service`

### Desktop

Leverage bubblewrap within [desktop entries](/index.php/Desktop_entries "Desktop entries"):

*   Bind as read-write the entire host `/` directory to `/` in the sandbox
*   Re-bind as read-only the `/var` and `/etc` directories in the sandbox
*   Mount a new devtmpfs filesystem to `/dev` in the sandbox
*   Create a tmpfs filesystem over the sandboxed `/run` directory
*   Disable network access by creating new network namespace

```
[Desktop Entry]
Name=nano Editor
Exec=bwrap --bind / / --dev /dev --tmpfs /run --unshare-net  st -e nano -o . %f
Type=Application
MimeType=text/plain;

```

**Note:** `--dev /dev` is required to write to `/dev/pty`

*   Example MuPDF desktop entry incorporating a `mupdf.sh` shell wrapper:

```
[Desktop Entry]
Name=MuPDF
Exec=mupdf.sh %f
Icon=application-pdf.svg
Type=Application
MimeType=application/pdf;application/x-pdf;

```

**Note:** Ensure that `mupdf.sh` is located within your executable PATH e.g. `PATH=$PATH:$HOME/bwrap`

### MuPDF

The power and flexibility of *bwrap* is best revealed when used to create an environment within a shell wrapper:

*   Bind as read-only the host `/usr/bin` directory to `/usr/bin` in the sandbox
*   Bind as read-only the host `/usr/lib` directory to `/usr/lib` in the sandbox
*   Create a symbolic link from the system `/usr/lib` directory to `/lib64` in the sandbox
*   Create a [tmpfs](/index.php/Tmpfs "Tmpfs") filesystem overlaying `/usr/lib/gcc` in the sandbox
    *   This effectively [blacklists](https://en.wikipedia.org/wiki/Blacklist_(computing) the contents of `/usr/lib/gcc` from appearing in the sandbox
*   Create a new tmpfs filesystem as the `$HOME` directory in the sandbox
*   Bind as read-only an `.Xauthority` file and *Documents* directory into the sandbox
    *   This effectively whitelists the `.Xauthority` file and *Documents* directory with recursion
*   Create a new tmpfs filesystem as the `/tmp` directory in the sandbox
*   Whitelist the [X11](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") socket by binding it into the sandbox as read-only
*   Clone and create private containers for all namespaces supported by the running kernel
    *   If the kernel does not support non-privileged user namespaces, skip its creation and continue
*   Do not place network components into a private namespace
    *   This allows for network access to follow URI hyperlinks

```
#!/bin/sh
#~/bwrap/mupdf.sh
(exec bwrap \
--ro-bind /usr/bin /usr/bin \
--ro-bind /usr/lib /usr/lib \
--symlink usr/lib /lib64 \
--tmpfs /usr/lib/gcc \
--tmpfs $HOME \
--ro-bind $HOME/.Xauthority $HOME/.Xauthority \
--ro-bind $HOME/Documents $HOME/Documents \
--tmpfs /tmp \
--ro-bind /tmp/.X11-unix/X0 /tmp/.X11-unix/X0 \
 --unshare-all \
--share-net \
/usr/bin/mupdf "$@")

```

**Tip:** Execute a shell wrapper substituting the existing executable with */usr/bin/sh* to debug and verify the contents and filesystem structure of the sandbox.

```
$ bwrap \
--ro-bind /usr/bin /usr/bin \
--ro-bind /usr/lib /usr/lib \
--symlink usr/lib /lib64 \
--tmpfs /usr/lib/gcc \
--tmpfs $HOME \
--ro-bind $HOME/.Xauthority $HOME/.Xauthority \
--ro-bind $HOME/Desktop $HOME/Desktop \
--tmpfs /tmp \
--ro-bind /tmp/.X11-unix/X0 /tmp/.X11-unix/X0 \
--unshare-all \
--share-net \
 /usr/bin/sh
bash-4.4$ ls -AF
.Xauthority  Documents/

```

Perhaps the most important rule to consider when building a bubblewrapped filesystem is that *commands are executed in the order they appear*. From the [MuPDF](http://mupdf.com/) example above:

*   A tmpfs system is created followed by the bind mounting of an `.Xauthority` file and a *Documents* directory:

```
--tmpfs $HOME \
--ro-bind $HOME/.Xauthority $HOME/.Xauthority \
--ro-bind $HOME/Documents $HOME/Documents \

```

```
bash-4.4$ ls -a
.  ..  .Xauthority  Desktop

```

*   A tmpfs filesystem is created after the bind mounting of `.Xauthority` and overlays it so that only the *Documents* directory is visible within the sandbox:

```
--ro-bind $HOME/.Xauthority $HOME/.Xauthority \
--tmpfs $HOME \
--ro-bind $HOME/Desktop $HOME/Desktop \

```

```
bash-4.4$ ls -a
.  ..  Desktop

```

### p7zip

Applications which have not yet been patched against [known vulnerabilities](https://web.nvd.nist.gov/view/vuln/detail?vulnId=CVE-2016-9296) constitute prime candidates for bubblewrapping:

*   Bind as read-only the host `/usr/bin/7za` executable path to the sandbox
*   Create a symbolic link from the system `/usr/lib` directory to `/lib64` in the sandbox
*   Blacklist the sandboxed contents of `/usr/lib/modules` and `/usr/lib/systemd` with tmpfs overlays
*   Mount a new devtmpfs filesystem to `/dev` in the sandbox
*   Bind as read-write the host `/sandbox` directory to the `/sandbox` directory in the sandbox
    *   *7za* will only run in the host `/sandbox` directory and/or its subdirectories when called from the shell wrapper
*   Create new cgroup/IPC/network/PID/UTS namespaces for the application and its processes
    *   If the kernel does not support non-privileged user namespaces, skip its creation and continue
    *   Creation of a new network namespace prevents the sandbox from obtaining network access
*   Add a custom or an arbitrary [hostname](/index.php/Hostname "Hostname") to the sandbox such as `p7zip`
*   Unset the `XAUTHORITY` [environment variable](/index.php/Environment_variable "Environment variable") to hide the location of the X11 connection cookie
    *   *7za* does not need to connect to an X11 display server to function properly
*   Start a new terminal session to prevent keyboard input from escaping the sandbox

```
#!/bin/sh
#~/bwrap/pz7ip.sh
(exec bwrap \
--ro-bind /usr/bin/7za /usr/bin/7za \
--symlink usr/lib /lib64 \
--tmpfs /usr/lib/modules \
--tmpfs /usr/lib/systemd \
--dev /dev \
--bind /sandbox /sandbox \
--unshare-all \
--hostname p7zip \
--unsetenv XAUTHORITY \
--new-session \
/usr/bin/7za "$@")

```

**Note:** */usr/bin/sh* and */usr/bin/ls* must reside in the executable path in order to traverse and verify the sandbox filesystem.

```
bwrap \
--ro-bind /usr/bin/7za /usr/bin/7za \
**--ro-bind /usr/bin/ls /usr/bin/ls \**
**--ro-bind /usr/bin/sh /usr/bin/sh \**
--symlink usr/lib /lib64 \
--tmpfs /usr/lib/modules \
--tmpfs /usr/lib/systemd \
--dev /dev \
--bind /sandbox /sandbox \
--unshare-all \
--hostname p7zip \
--unsetenv XAUTHORITY \
--new-session \
/usr/bin/sh
bash: no job control in this shell
bash-4.4$ ls -AF         
dev/  lib64@  usr/
bash-4.4$ ls -l /usr/lib/modules 
total 0
bash-4.4$ ls -l /usr/lib/systemd
total 0
bash-4.4$ ls -AF /dev
console  full  null  ptmx@  pts/  random  shm/  stderr@  stdin@  stdout@  tty  urandom  zero
bash-4.4$ ls -A /usr/bin
7za  ls  sh

```

### Filesystem isolation

**Warning:** It is the bubblewrap user’s responsibility to update the filesystem trees regularly.

To further hide the contents of the file system (such as those in `/var`, `/usr/bin` and `/usr/lib`) and to sandbox even the installation of software, pacman can be made to install Arch packages into isolated filesystem trees.

In order to use pacman for installing software into the filesystem trees, you will need to install [fakeroot](https://www.archlinux.org/packages/?name=fakeroot) and [fakechroot](https://www.archlinux.org/packages/?name=fakechroot).

Suppose you want to install the `xterm` package with pacman into an isolated filesystem tree. You should prepare your tree like this:

```
$ MYPACKAGE=xterm
$ mkdir -p ~/sandboxes/${MYPACKAGE}/files/var/lib/pacman
$ mkdir -p ~/sandboxes/${MYPACKAGE}/files/etc
$ cp /etc/pacman.conf ~/sandboxes/${MYPACKAGE}/files/etc/pacman.conf

```

You may want to edit `~/sandboxes/${MYPACKAGE}/files/etc/pacman.conf` and adjust the pacman configuration used:

*   Remove any undesired custom repositories and `IgnorePkg`, `IgnoreGroup`, `NoUpgrade` and `NoExtract` settings that are needed only for the host system.
*   You may need to remove the `CheckSpace` option so pacman will not complain about errors finding the root filesystem for checking disk space.

Then install the `base` group along with the needed fakeroot into the isolated filesystem tree:

```
$ fakechroot fakeroot pacman -Syu \
    --root ~/sandboxes/${MYPACKAGE}/files \
    --dbpath ~/sandboxes/${MYPACKAGE}/files/var/lib/pacman \
    --config ~/sandboxes/${MYPACKAGE}/files/etc/pacman.conf \
    base fakeroot

```

Since you will be repeatedly calling bubblewrap with the same options, make an alias:

```
$ alias bw-install='bwrap                        \
     --bind ~/sandboxes/${MYPACKAGE}/files/ /    \
     --ro-bind /etc/resolv.conf /etc/resolv.conf \
     --tmpfs /tmp                                \
     --proc /proc                                \
     --dev /dev                                  \
     --chdir /                                   '

```

You will need to set up the [locales](/index.php/Locale "Locale"):

```
$ nano -w ~/sandboxes/${MYPACKAGE}/files/etc/locale.gen
$ bw-install locale-gen

```

Then set up pacman’s keyring:

```
$ bw-install fakeroot pacman-key --init
$ bw-install fakeroot pacman-key --populate archlinux

```

Now you can install the desired `xterm` package.

```
$ bw-install fakeroot pacman -S ${MYPACKAGE}

```

If the pacman command fails here, try running the command for populating the keyring again.

Congratulations. You now have an isolated filesystem tree containing `xterm`. You can use `bw-install` again to upgrade your filesystem tree.

You can now run your software with bubblewrap. `*command*` should be `xterm` in this case.

```
$ bwrap                                          \
     --ro-bind ~/sandboxes/${MYPACKAGE}/files/ / \
     --ro-bind /etc/resolv.conf /etc/resolv.conf \
     --tmpfs /tmp                                \
     --proc /proc                                \
     --dev /dev                                  \
     --chdir /                                   \
     *command*

```

Note that some files can be shared between packages. You can hardlink to all files of an existing parent filesystem tree to reuse them in a new tree:

```
$ cp -al ~/sandboxes/${MYPARENTPACKAGE} ~/sandboxes/${MYPACKAGE}

```

Then proceed with the installation as usual by calling pacman from `bw-install fakechroot fakeroot pacman …`.

## Troubleshooting

### Using X11

Bind mounting the host X11 socket to an alternative X11 socket may not work:

```
--bind /tmp/.X11-unix/X0 /tmp/.X11-unix/X8 --setenv DISPLAY :8

```

A workaround is to bind mount the host X11 socket to the same socket within the sandbox:

```
--bind /tmp/.X11-unix/X0 /tmp/.X11-unix/X0 --setenv DISPLAY :0

```

### Sandboxing X11

While bwrap provides some very nice isolation for sandboxed application, there is an easy escape as long as access to the X11 socket is available. X11 does not include isolation between applications and is completely insecure. The only solution to this is to switch to a wayland compositor with no access to the Xserver from the sandbox.

There are however some workarounds that use xpra or xephyr to run in a new X11 environment. This would work with bwrap as well.

To test X11 isolation, run 'xinput test <id>' where <id> is your keyboard id which you can find with 'xinput list' When run without additional X11 isolation, this will show that any application with X11 access can capture keyboard input of any other application, which is basically what a keylogger would do.

### Opening URLs from wrapped applications

When a wrapped IRC or email client attempts to open a URL, it will usually attempt to launch a browser process, which will run within the same sandbox as the wrapped application. With a well-wrapped application, this will likely not work. The approach used by [Firejail](/index.php/Firejail "Firejail") is to [give wrapped applications all the privileges of the browser as well](https://github.com/netblue30/firejail/blob/b1479a3730a361221c271226cc56d0724ee109c4/etc/thunderbird.profile#L31-L33), however this implies a good amount of permission creep.

A better solution to this problem is to communicate opened URLs to outside the sandbox. This can be done using `snapd-xdg-open` as follows:

1.  Install [snapd-xdg-open-git](https://aur.archlinux.org/packages/snapd-xdg-open-git/)
2.  On your `bwrap` command line, add:

```
$ bwrap ... \
  --ro-bind /run/user/$UID/bus /run/user/$UID/bus \
  --ro-bind /usr/lib/snapd-xdg-open/xdg-open /usr/bin/xdg-open \
  --ro-bind /usr/lib/snapd-xdg-open/xdg-open /usr/bin/chromium \
  ...

```

The `/usr/bin/chromium` bind is only necessary for programs not using XDG conventions, such as Mozilla Thunderbird.

### New Session

There is a security issue with TIOCSTI, (CVE-2017-5226) which allows sandbox escape. To prevent this, bubblewrap has introduced the new option '--new-session' which calls setsid(). However this causes some behavioural issues that are hard to work with in some cases. For instance, it makes shell job control not work for the bwrap command.

It is recommended to use this if possible, but if not the developers recommend that the issue is neutralized in some other way, for instance using SECCOMP, which is what flatpak does: [https://github.com/flatpak/flatpak/commit/902fb713990a8f968ea4350c7c2a27ff46f1a6c4](https://github.com/flatpak/flatpak/commit/902fb713990a8f968ea4350c7c2a27ff46f1a6c4)

## See also

*   [bubblewrap GitHub project page](https://github.com/projectatomic/bubblewrap)
*   [The Linux Kernel Archives: SECure COMPuting with filters](https://www.kernel.org/doc/Documentation/prctl/seccomp_filter.txt)