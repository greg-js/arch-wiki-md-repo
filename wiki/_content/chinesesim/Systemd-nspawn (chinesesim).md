**翻译状态：** 本文是英文页面 [Systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-09-23，点击[这里](https://wiki.archlinux.org/index.php?title=Systemd-nspawn&diff=0&oldid=576931)可以查看翻译后英文页面的改动。

Related articles

*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [Lxc-systemd](/index.php/Lxc-systemd "Lxc-systemd")
*   [systemd (简体中文)](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")
*   [systemd-networkd (简体中文)](/index.php/Systemd-networkd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd-networkd (简体中文)")
*   [Docker (简体中文)](/index.php/Docker_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Docker (简体中文)")

*systemd-nspawn* 就像是 [chroot](/index.php/Chroot "Chroot") 命令, 但是是 *吃了类固醇的chroot（chroot on steroids）*.

*systemd-nspawn* 可用于在一个轻量命名空间容器中运行命令或操作系统。它比 [chroot](/index.php/Chroot "Chroot") 更强大在于它完全虚拟化了文件系统层次结构、进程树、各种 IPC 子系统以及主机和域名。

*systemd-nspawn* 将容器中各种内核接口的访问限制为只读，像是 `/sys`, `/proc/sys` 和 `/sys/fs/selinux`。 网络接口和系统时钟或许不能从容器内更改，不能创建设备节点。主机系统也无法重新启动，并且可能无法从容器内加载内核模块。

这种机制不同于 [Lxc-systemd](/index.php/Lxc-systemd "Lxc-systemd") 或 [Libvirt](/index.php/Libvirt "Libvirt")-lxc，它是一种更容易去配置的工具。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 用例](#用例)
    *   [2.1 在容器中创建和启动最小 Arch Linux 发行版](#在容器中创建和启动最小_Arch_Linux_发行版)
    *   [2.2 创建 Debian 或 Ubuntu 环境](#创建_Debian_或_Ubuntu_环境)
    *   [2.3 创建专有用户（无特权容器）](#创建专有用户（无特权容器）)
    *   [2.4 在启动时启用容器](#在启动时启用容器)
    *   [2.5 编译与测试包](#编译与测试包)
*   [3 管理](#管理)
    *   [3.1 machinectl](#machinectl)
    *   [3.2 systemd 工具链](#systemd_工具链)
    *   [3.3 资源控制](#资源控制)
*   [4 提示和技巧](#提示和技巧)
    *   [4.1 使用 X 环境](#使用_X_环境)
        *   [4.1.1 避免使用 xhost](#避免使用_xhost)
    *   [4.2 运行 Firefox](#运行_Firefox)
    *   [4.3 访问主机文件系统](#访问主机文件系统)
    *   [4.4 配置网络](#配置网络)
        *   [4.4.1 nsswitch.conf](#nsswitch.conf)
        *   [4.4.2 使用主机网络](#使用主机网络)
        *   [4.4.3 虚拟以太网接口](#虚拟以太网接口)
        *   [4.4.4 使用网络桥接](#使用网络桥接)
    *   [4.5 Run on a non-systemd system](#Run_on_a_non-systemd_system)
    *   [4.6 Specify per-container settings](#Specify_per-container_settings)
    *   [4.7 Use Btrfs subvolume as container root](#Use_Btrfs_subvolume_as_container_root)
    *   [4.8 Use temporary Btrfs snapshot of container](#Use_temporary_Btrfs_snapshot_of_container)
    *   [4.9 Run docker in systemd-nspawn](#Run_docker_in_systemd-nspawn)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Root login fails](#Root_login_fails)
    *   [5.2 Unable to upgrade some packages on the container](#Unable_to_upgrade_some_packages_on_the_container)
    *   [5.3 execv(...) failed: Permission denied](#execv(...)_failed:_Permission_denied)
    *   [5.4 Reboot not working](#Reboot_not_working)
    *   [5.5 Mounting a NFS share inside the container](#Mounting_a_NFS_share_inside_the_container)
*   [6 See also](#See_also)

## 安装

*systemd-nspawn* 是被打包进 [systemd](https://www.archlinux.org/packages/?name=systemd) 包的一部分。

## 用例

### 在容器中创建和启动最小 Arch Linux 发行版

首先安装 [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts).

然后，创建一个目录来保存容器。在这个用例中我们将使用 `~/MyContainer`。

接下来，我们使用 pacstrap 在容器中安装一个基本的arch系统。我们至少需要安装[base](https://www.archlinux.org/packages/?name=base) 包组.

```
# pacstrap -i -c ~/MyContainer base [additional pkgs/groups]

```

**Tip:** `-i` 选项将**避免**自动确认包的选择。由于不需要在容器中安装 Linux 内核，因此可以从包列表选择中删除它以节省空间。详情见 [Pacman#Usage](/index.php/Pacman#Usage "Pacman")。

**Note:** [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) 包被 [linux](https://www.archlinux.org/packages/?name=linux) 依赖，它被包含在 [base](https://www.archlinux.org/packages/?name=base) 包组中并且不是运行容器的关键，会导致 `systemd-tmpfiles-setup.service` 在 `systemd-nspawn` 的引导过程中会出现一些问题。在建立容器时安装 [base](https://www.archlinux.org/packages/?name=base) 组但排除掉 [linux](https://www.archlinux.org/packages/?name=linux) 包以及他的依赖是有可能的，用 `pacstrap -i -c ~/MyContainer base --ignore linux [additional pkgs/groups]`。`--ignore` 标志将会非常简单的传达给 [pacman](https://www.archlinux.org/packages/?name=pacman)。详情见 [FS#46591](https://bugs.archlinux.org/task/46591)。

安装完成后，引导至容器中：

```
# systemd-nspawn -b -D ~/MyContainer

```

参数 `-b` 将会启动这个容器（比如：以 PID=1 运行 `systemd`）, 而不是仅仅启动一个 shell, 而参数 `-D` 指定成为容器根目录的目录。

容器启动后，以"root"身份登录，没有密码。

可以在容器内运行 `poweroff` 来关闭容器。在主机端，容器可以通过 [machinectl](#machinectl) 工具进行控制。

**Note:** 要从容器内终止 *session*，请按住 `Ctrl` 并快速地按 `]` 三下。非美国键盘用户应该使用 `%` 而不是 `]`。

### 创建 Debian 或 Ubuntu 环境

安装 [debootstrap](https://www.archlinux.org/packages/?name=debootstrap) 和 [debian-archive-keyring](https://www.archlinux.org/packages/?name=debian-archive-keyring) 与 [ubuntu-keyring](https://www.archlinux.org/packages/?name=ubuntu-keyring) 中的一个或两个（当然要安装你想要的发行版的keyrings）。

**Note:** *systemd-nspawn* 要求容器中的操作系统以 PID 1 运行systemd，并且*systemd-nspawn* 要安装在容器中。这意味着 15.04 之前的 Ubuntu 并不能开箱即用，并且需要额外的配置才能从upstart转换成systemd。还需要确保在容器中安装 `systemd-container` 包。

在这里很容易设置 Debian 或 Ubuntu 环境：

```
# cd /var/lib/machines
# debootstrap --include=systemd-container --components=main,universe <codename> myContainer <repository-url>

```

对于 Debian，有效的代码名称要么是滚动式名称像是 "stable" 或 "testing"，要么是发行名称如 "stretch" 或 "sid"， 对于 Ubuntu，应使用"xenial"或者"zesty"等代码名称。 代码名称的完整列表位于 `/usr/share/debootstrap/scripts` 中。对于 Debian 镜像，"仓库链接" 可以是 `[http://deb.debian.org/debian/](http://deb.debian.org/debian/)`。 对于 Ubuntu 镜像, "仓库链接" 可以是 `[http://archive.ubuntu.com/ubuntu/](http://archive.ubuntu.com/ubuntu/)`。

与 Arch 不同，Debian 和 Ubuntu 不会让您在首次登录时无密码登录。为了设置root密码登录，要不使用"-b"参数并设置密码：

```
# systemd-nspawn -D myContainer
# passwd
# logout

```

如果上述不起作用。可以启动容器，改用以下命令：

```
# systemd-nspawn -b -D myContainer  #Starts the container
# machinectl shell root@myContainer /bin/bash  #Get a root bash shell
# passwd
# logout

```

### 创建专有用户（无特权容器）

*systemd-nspawn* 支持非特权容器，尽管容器需要以 root 身份引导启动。

**Note:** 此功能需要 [user_namespaces(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/user_namespaces.7)，更多信息请参阅 [Linux Containers#Enable support to run unprivileged containers (optional)](/index.php/Linux_Containers#Enable_support_to_run_unprivileged_containers_(optional) "Linux Containers")

最简单的方法是让 *systemd-nspawn* 来决定一切：

```
# systemd-nspawn -UD myContainer
# passwd
# logout
# systemd-nspawn -bUD myContainer

```

在这里 *systemd-nspawn* 将确认目录的所有者是否已经被使用，如果没有，将使用这个作为基数的大于它的65536个ID。另一方面，如果 UID/GID 正在使用，它将从 524288 - 1878982656 中随机选择 65536 个未使用的范围，并使用它们。

**Note:**

*   所选范围的基数始终为 65536 的倍数。
*   如果内核支持用户命名空间，那么 `-U` 和 `--private-users=pick` 是相同的。`--private-users=pick` 还意味着 `--private-users-chown`，更多细节请参阅[systemd-nspawn(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-nspawn.1)。

您还可以手动指定容器的 UID/GID：

```
# systemd-nspawn -D myContainer --private-users=1354956800:65536 --private-users-chown
# passwd
# logout
# systemd-nspawn -bUD myContainer

```

你仍然可以使用 `--private-users=1354956800:65536` 配合 `--private-users-chown` 来启动容器，但这是徒增麻烦罢了, 让 `-U` 在分配 ID 后处理它。

### 在启动时启用容器

当您频繁地使用容器时，您可能会希望能够在在启动时启用它。

首先 [enable](/index.php/Enable "Enable") 这个 `machines.target`，然后启用 `systemd-nspawn@*myContainer*.service`，其中 `myContainer` 是在 `/var/lib/machines` 中的容器。

**Tip:** 要自定义容器的启动，请编辑 `/etc/systemd/nspawn/*myContainer*.nspawn`。有关所有选项，请参阅 [systemd.nspawn(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.nspawn.5)。

### 编译与测试包

请参阅 [Creating packages for other distributions](/index.php/Creating_packages_for_other_distributions "Creating packages for other distributions") 寻找更多用例.

## 管理

### machinectl

**Note:** *machinectl* 工具要求在容器中安装 [systemd](/index.php/Systemd "Systemd") 和 [dbus](https://www.archlinux.org/packages/?name=dbus) 。有关详细讨论，请参阅 [[1]](https://github.com/systemd/systemd/issues/685)。

管理容器基本上使用 `machinectl` 命令。有关详细信息，请参阅 [machinectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/machinectl.1) 。

用例：

在正在运行的容器内生成一个新的 shell：

```
$ machinectl login *MyContainer*

```

显示有关容器的详细信息：

```
$ machinectl status *MyContainer*

```

重新启动容器：

```
$ machinectl reboot *MyContainer*

```

容器关机：

```
$ machinectl poweroff *MyContainer*

```

**Tip:** 可以使用 *systemctl* `poweroff` 和 `reboot` 命令从容器会话中执行关机和重新启动操作。

下载镜像：

```
# machinectl pull-tar *URL* *name*

```

### systemd 工具链

大部分核心的 systemd 工具链已更新为对容器有效。工具们通常提供了 `-M, --machine=` 选项并把容器名称作为参数。 用例：

查看特定容器的 journal 日志：

```
$ journalctl -M *MyContainer*

```

显示控制组的内容：

```
$ systemd-cgls -M *MyContainer*

```

查看容器的启动时间：

```
$ systemd-analyze -M *MyContainer*

```

查看资源使用情况的概况：

```
$ systemd-cgtop

```

### 资源控制

您可以使用控制组来使用 `systemctl set-property` 实现对容器的限制和资源管理，请参阅 [systemd.resource-control(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.resource-control.5)。例如，您可能希望限制内存量或 CPU 使用率。要将容器的内存消耗限制为 2 GiB：

```
# systemctl set-property systemd-nspawn@*myContainer*.service MemoryMax=2G

```

或者将 CPU 时间使用率限制为大约相当于 2 个内核：

```
# systemctl set-property systemd-nspawn@*myContainer*.service CPUQuota=200%

```

这将在 `/etc/systemd/system.control/systemd-nspawn@*myContainer*.service.d/` 中创建常驻文件}。

根据文档，`MemoryHigh` 是控制内存消耗的首选方法，但也不会像 `MemoryMax` 那样进行强制限制。您可以使用这两个选项将 `MemoryMax` 作为您最后的一道防线。还要考虑到如果您不会限制容器可以“看到”的 CPU 数量，但通过限制容器相对于总 CPU 时间的最大时间，也可以获得类似的结果。

**Tip:** 如果不希望在重新启动后保留此更改，则可以传递选项 `--runtime` 使更改成为临时性的。您可以使用 `systemd-cgtop` 检查其结果。

## 提示和技巧

### 使用 X 环境

详情见 [Xhost](/index.php/Xhost "Xhost") 和 [Change root#Run graphical applications from chroot](/index.php/Change_root#Run_graphical_applications_from_chroot "Change root").

您需要设置您容器会话中 `DISPLAY` 以连接到外部 X 服务器。

X 在 `/tmp` 文件夹中存储一些必要的文件。为了使容器能显示任何内容，它需要访问这些文件。为此，当启动容器时，请追加 `--bind-ro=/tmp/.X11-unix` 选项。

**Note:** 从 systemd 版本 235 开始, `/tmp/.X11-unix` 的内容 [必须以只读方式装入](https://github.com/systemd/systemd/issues/7093)，否则它们将从文件系统中消失。只读挂载标志不会阻止在套接字上使用 `connect()`。如果你还绑定了`/run/user/1000` 那么你有可能希望显式绑定 `/run/user/1000/bus` 为只读，以防止 dbus 套接字被删除。

#### 避免使用 xhost

`xhost` 仅提供对 X 服务器相当粗糙的访问权限。更细节的访问控制可通过`$XAUTHORITY` 文件。遗憾的是, 仅使 `$XAUTHORITY` 文件在容器中可被访问无法执行工作: 您的 `$XAUTHORITY` 文件只特定于您的主机，但是容器是另一台主机。根据 [stackoverflow](https://stackoverflow.com/a/25280523) 下面这个技巧可以让你的X服务器接受来自于你容器中的X 应用的 `$XAUTHORITY` 文件：

```
$ XAUTH=/tmp/container_xauth
$ xauth nextract - "$DISPLAY" | sed -e 's/^..../ffff/' | xauth -f "$XAUTH" nmerge -
$ sudo systemd-nspawn -D myContainer --bind=/tmp/.X11-unix --bind="$XAUTH" \
                      -E DISPLAY="$DISPLAY" -E XAUTHORITY="$XAUTH" --as-pid2 /usr/bin/xeyes

```

上面第二行将连接组设定为 "FamilyWild"，值 `65535`，这会使输入匹配你的每一个显示。 更多信息请参考 [Xsecurity(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xsecurity.7) 。

### 运行 Firefox

请见 [Firefox tweaks](/index.php/Firefox_tweaks#Run_Firefox_inside_an_nspawn_container "Firefox tweaks").

### 访问主机文件系统

请见 `--bind` 和 `--bind-ro` 于 [systemd-nspawn(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-nspawn.1).

如果主机和容器都是 Arch Linux，则例如，可以共享 pacman 缓存：

```
# systemd-nspawn --bind=/var/cache/pacman/pkg

```

或许你还可以使用文件来进行指定的先于容器的绑定：

 `/etc/systemd/nspawn/*my-container*.nspawn` 
```
[Files]
Bind=/var/cache/pacman/pkg

```

详情见 [#Specify per-container settings](#Specify_per-container_settings).

### 配置网络

对于最简单的设置，允许传出连接到互联网，你可以使用 [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") 进行网络管理和 DHCP ，并且针对DNS你可以使用 [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") 。 这里假设您已经使用 `-n` 启动 `systemd-nspawn` 来创建指向主机的虚拟以太网链接。

您还可以通过添加 DNS 服务器的 IP 地址来手动 [编辑](/index.php/Textedit "Textedit") 你容器的 `/etc/resolv.conf`，而不是使用 [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved")。

请注意，规范的 [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") 主机和容器的 .network 文件来自于https://github.com/systemd/systemd/tree/master/network 。

更多详细的例子请参阅 [systemd-networkd#Usage with containers](/index.php/Systemd-networkd#Usage_with_containers "Systemd-networkd") 。

#### nsswitch.conf

为了能从主机更容易的的连接到容器中，你可以为容器名开启本地DNS解析。向 `/etc/nsswitch.conf` 文件中 `hosts:` 部分添加 `mymachines`。比如：

 `/etc/nsswitch.conf`  `hosts: files mymachines dns myhostname` 

然后，任何DNS寻找主机中主机名 `foo` 时，将会先参看 `/etc/hosts`，然后时本地容器的名字，再是上游DNS等等。

#### 使用主机网络

为了关闭容器的私有网络，利用 `machinectl start MyContainer` 启动时，请往 `/etc/systemd/nspawn` 目录（如有必要请自行创建目录）下的 `MyContainer.nspawn` 文件中添加下文：

 `/etc/systemd/nspawn/MyContainer.nspawn` 
```
[Network]
VirtualEthernet=no

```

在 `MyContainer.nspawn` 文件中参数集将会覆盖掉 `systemd-nspawn@.service` 的默认设置，然后重新启动的容器将会使用主机的网络。

#### 虚拟以太网接口

如果一个容器是用 `systemd-nspawn ... -n` 启动的，systemd 将会自动在主机和容器上各创建一个虚拟网络接口，并用虚拟以太网线路连接起来。

如果容器的名字是 `foo`，那么主机上的虚拟网络接口的名字会是 `ve-foo`。容器里的虚拟网络接口名一直是 `host0`。

当检查到接口带有 `ip link`，接口名显示时将会带有一个后缀，像是 `ve-foo@if2` 和 `host0@if9`。`@ifN` 实际上并不是接口名字的一部分，相反的，`ip link` 带有这个信息以指示虚拟以太网线缆所连接的另一端的“插槽”。

举个例子，一个主机的虚拟以太网接口显示为 `ve-foo@if2`，它将连接到容器 `foo`，其内部的第二个网络接口 -- 当你在容器内运行 `ip link` 序号为 2 的那一个。相同的，在容器内，名字为 `host0@if9` 的接口将会连接到主机的第9个接口。

**Note:** 如果你使用防火墙，你的虚拟接口的流量可能会被阻挡。你必须开启必要的规则来通过你的防火墙。

#### 使用网络桥接

如果你在主机系统上配置过一个网桥，以便将IP地址分配给容器，使其就像是本地网络中的一个物理机一样（比如，请看 [systemd-networkd#DHCP with two distinct IP](/index.php/Systemd-networkd#DHCP_with_two_distinct_IP "Systemd-networkd") 或 [systemd-networkd#Static IP network](/index.php/Systemd-networkd#Static_IP_network "Systemd-networkd")），你可以通过选项 `--network-bridge=*br0*` 使 systemd-nspawn 来使用它。

### Run on a non-systemd system

See [Init#systemd-nspawn](/index.php/Init#systemd-nspawn "Init").

### Specify per-container settings

To specify per-container settings and not overrides for all (e.g. bind a directory to only one container), the *.nspawn* files can be used. See [systemd.nspawn(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.nspawn.5) for details.

### Use Btrfs subvolume as container root

To use a [Btrfs subvolume](/index.php/Btrfs#Subvolumes "Btrfs") as a template for the container's root, use the `--template` flag. This takes a snapshot of the subvolume and populates the root directory for the container with it.

**Note:** If the template path specified is not the root of a subvolume, the **entire** tree is copied. This will be very time consuming.

For example, to use a snapshot located at `/.snapshots/403/snapshot`:

```
# systemd-nspawn --template=/.snapshots/403/snapshots -b -D *my-container*

```

where `*my-container*` is the name of the directory that will be created for the container. After powering off, the newly created subvolume is retained.

### Use temporary Btrfs snapshot of container

One can use the `--ephemeral` or `-x` flag to create a temporary btrfs snapshot of the container and use it as the container root. Any changes made while booted in the container will be lost. For example:

```
# systemd-nspawn -D *my-container* -xb

```

where *my-container* is the directory of an **existing** container or system. For example, if `/` is a btrfs subvolume one could create an ephemeral container of the currently running host system by doing:

```
# systemd-nspawn -D / -xb 

```

After powering off the container, the btrfs subvolume that was created is immediately removed.

### Run docker in systemd-nspawn

[Docker](/index.php/Docker "Docker") requires `rw` permission of `/sys/fs/cgroup` to run its containers, which is mounted read-only by `systemd-nspawn` by default due to cgroup namespace. However, it is possible to run Docker in a systemd-nspawn container by bind-mounting `/sys/fs/cgroup` from host os and enabling necessary capabilities and permissions.

**Note:** The following steps are essentially sharing the cgroup namespace to the container, giving kernel keyring permissions and making it a privileged container, which is likely to increase the attack surface and decrease security level. You should always evaluate the actual benefits by doing so before following the steps.

First, cgroup namespace should be disabled by `systemctl edit systemd-nspawn@myContainer`

 `systemctl edit systemd-nspawn@myContainer` 
```
[Service]
Environment=SYSTEMD_NSPAWN_USE_CGNS=0

```

Then, edit `/etc/systemd/nspawn/myContainer.nspawn` (create if absent) and add the following configurations.

 `/etc/systemd/nspawn/myContainer.nspawn` 
```
[Exec]
Capability=all
SystemCallFilter=add_key keyctl

[Files]
Bind=/sys/fs/cgroup

```

This grants all capabilities to the container, whitelists two system calls `add_key` and `keyctl` (related to kernel keyring and required by Docker), and bind-mounts `/sys/fs/cgroup` from host to the container. After editing these files, you need to poweroff and restart your container for them to take effect.

**Note:** You might need to load the `overlay` module on the host before starting Docker inside the systemd-nspawn to use the `overlay2` storage driver (default storage driver of Docker) properly. Failure to load the driver will cause Docker to choose the inefficient driver `vfs` which copies everything for every layer of Docker containers. Consult [Kernel modules#Automatic module loading with systemd](/index.php/Kernel_modules#Automatic_module_loading_with_systemd "Kernel modules") on how to load the module automatically.

## Troubleshooting

### Root login fails

If you get the following error when you try to login (i.e. using `machinectl login <name>`):

```
arch-nspawn login: root
Login incorrect

```

And `journalctl` shows:

```
pam_securetty(login:auth): access denied: tty 'pts/0' is not secure !

```

Add `pts/0` to the list of terminal names in `/etc/securetty` on the **container** filesystem, see [[2]](http://unix.stackexchange.com/questions/41840/effect-of-entries-in-etc-securetty/41939#41939). You can also opt to delete `/etc/securetty` on the **container** to allow root to login to any tty, see [[3]](https://github.com/systemd/systemd/issues/852).

### Unable to upgrade some packages on the container

It can sometimes be impossible to upgrade some packages on the container, [filesystem](https://www.archlinux.org/packages/?name=filesystem) being a perfect example. The issue is due to `/sys` being mounted as Read Only. The workaround is to remount the directory in Read Write when running `mount -o remount,rw -t sysfs sysfs /sys`, do the upgrade then reboot the container.

### execv(...) failed: Permission denied

When trying to boot the container via `systemd-nspawn -bD */path/to/container*` (or executing something in the container), and the following error comes up:

```
execv(/usr/lib/systemd/systemd, /lib/systemd/systemd, /sbin/init) failed: Permission denied

```

even though the permissions of the files in question (i.e. `/lib/systemd/systemd`) are correct, this can be the result of having mounted the file system on which the container is stored as non-root user. For example, if you mount your disk manually with an entry in [fstab](/index.php/Fstab "Fstab") that has the options `noauto,user,...`, *systemd-nspawn* will not allow executing the files even if they are owned by root.

### Reboot not working

When trying to reboot the container via machinectl or within the container, the container does not reboot.

Workaround: edit `/usr/lib/systemd/system/systemd-nspawn@.service` and remove `--keep-unit`

Reference: [https://github.com/systemd/systemd/issues/2809](https://github.com/systemd/systemd/issues/2809)

### Mounting a NFS share inside the container

Not possible at this time (June 2019).

## See also

*   [Automatic console login](/index.php/Getty#Nspawn_console "Getty")
*   [machinectl man page](http://www.freedesktop.org/software/systemd/man/machinectl.html)
*   [systemd-nspawn man page](http://www.freedesktop.org/software/systemd/man/systemd-nspawn.html)
*   [Creating containers with systemd-nspawn](http://lwn.net/Articles/572957/)
*   [Presentation by Lennart Pottering on systemd-nspawn](https://www.youtube.com/results?search_query=systemd-nspawn&aq=f)
*   [Running Firefox in a systemd-nspawn container](http://dabase.com/e/12009/)