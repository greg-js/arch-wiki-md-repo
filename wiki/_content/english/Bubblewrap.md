[bubblewrap](https://github.com/projectatomic/bubblewrap) is a lightweight setuid sandbox application developed from [Flatpak](https://en.wikipedia.org/wiki/Flatpak "wikipedia:Flatpak") with a small installation footprint and minimal resource requirements. While the application package is named bubblewrap, the actual executable binary and manpage reference is *bwrap*. Notable features include support for cgroup/IPC/mount/network/PID/user [namespaces](https://en.wikipedia.org/wiki/Linux_namespaces "wikipedia:Linux namespaces") and [seccomp](https://en.wikipedia.org/wiki/Seccomp "wikipedia:Seccomp") filtering. Note that bubblewrap drops all [capabilities](/index.php/Capabilities "Capabilities") within a sandbox and that child tasks cannot gain greater privileges than its parent. Notable feature exclusions include the lack of explicit support for blacklisting/whitelisting file paths.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage examples](#Usage_examples)
    *   [3.1 Bash](#Bash)
    *   [3.2 dhcpcd](#dhcpcd)
    *   [3.3 Unbound](#Unbound)
    *   [3.4 Desktop](#Desktop)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Sandboxing X11](#Sandboxing_X11)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [bubblewrap](https://www.archlinux.org/packages/?name=bubblewrap) or [bubblewrap-git](https://aur.archlinux.org/packages/bubblewrap-git/).

**Note:** The user namespace configuration item `CONFIG_USER_NS` is not set in the stock Arch kernel per [FS#36969](https://bugs.archlinux.org/task/36969). This prevents the kernel from exposing user namespaces as a means to accomodate separate user information for separate virtualized services. An example would be running *syslog* in a namespace with a UID and GID different than that of the host system. The [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) package sets `CONFIG_USER_NS=y` and is a viable alternative to the stock kernel if the ability to create user namepaces as an unprivileged user is desired.

## Configuration

bubblewrap can be called directly from the command-line and/or within [shell scripts](https://github.com/projectatomic/bubblewrap/blob/master/demos/bubblewrap-shell.sh) as part of a [complex wrapper](https://github.com/projectatomic/bubblewrap/blob/master/demos/flatpak-run.sh). Unlike applications such as [Firejail](/index.php/Firejail "Firejail") which automatically set `/var` and `/etc` to read-only within the sandbox, bubblewrap makes no such operating assumptions. It is up to the user to determine which configuration options to pass in accordance to the application being sandboxed. bubblewrap does not automatically create user namespaces when running with setuid privileges and can accomodate typical environment variables including `$HOME` and `$USER`.

## Usage examples

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
bash: no job control in this shell
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
*   Create new [IPC](https://en.wikipedia.org/wiki/Inter-process_communication "wikipedia:Inter-process communication") and [control group](/index.php/Cgroups "Cgroups") namespaces
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

## Troubleshooting

### Sandboxing X11

Bind mounting the host X11 socket to an alternative X11 socket may not work:

```
--bind /tmp/.X11-unix/X0 /tmp/.X11-unix/X8 --setenv DISPLAY :8

```

A workaround is to bind mount the host X11 socket to the same socket within the sandbox:

```
--bind /tmp/.X11-unix/X0 /tmp/.X11-unix/X0 --setenv DISPLAY :0

```

## See also

*   [bubblewrap GitHub project page](https://github.com/projectatomic/bubblewrap)