Related articles

*   [PCI passthrough via OVMF](/index.php/PCI_passthrough_via_OVMF "PCI passthrough via OVMF")
*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")

**翻译状态：** 本文是英文页面 [Libvirt](/index.php/Libvirt "Libvirt") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-07-10，点击[这里](https://wiki.archlinux.org/index.php?title=Libvirt&diff=0&oldid=528864)可以查看翻译后英文页面的改动。

Libvirt 是一组软件的汇集，提供了管理虚拟机和其它虚拟化功能（如：存储和网络接口等）的便利途径。这些软件包括：一个长期稳定的 C 语言 API、一个守护进程（libvirtd）和一个命令行工具（virsh）。Libvirt 的主要目标是提供一个单一途径以管理多种不同虚拟化方案以及虚拟化主机，包括：[KVM/QEMU](/index.php/QEMU "QEMU")，[Xen](/index.php/Xen "Xen")，[LXC](/index.php/LXC "LXC")，[OpenVZ](http://openvz.org) 或 [VirtualBox](/index.php/VirtualBox "VirtualBox") [hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors") （[详见这里](http://libvirt.org/drivers.html)）。

Libvirt 的一些主要功能如下：

*   **VM management（虚拟机管理）**：各种虚拟机生命周期的操作，如：启动、停止、暂停、保存、恢复和迁移等；多种不同类型设备的热插拔操作，包括磁盘、网络接口、内存、CPU等。
*   **Remote machine support（支持远程连接）**：Libvirt 的所有功能都可以在运行着 libvirt 守护进程的机器上执行，包括远程机器。通过最简便且无需额外配置的 SSH 协议，远程连接可支持多种网络连接方式。
*   **Storage management（存储管理）**：任何运行 libvirt 守护进程的主机都可以用于管理多种类型的存储：创建多种类型的文件镜像（qcow2，vmdk，raw，...），挂载 NFS 共享，枚举现有 LVM 卷组，创建新的 LVM 卷组和逻辑卷，对裸磁盘设备分区，挂载 iSCSI 共享，以及更多......
*   **Network interface management（网络接口管理）**：任何运行 libvirt 守护进程的主机都可以用于管理物理的和逻辑的网络接口，枚举现有接口，配置（和创建）接口、桥接、VLAN、端口绑定。
*   **Virtual NAT and Route based networking（虚拟 NAT 和基于路由的网络）**：任何运行 libvirt 守护进程的主机都可以管理和创建虚拟网络。Libvirt 虚拟网络使用防火墙规则实现一个路由器，为虚拟机提供到主机网络的透明访问。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
    *   [1.1 服务端](#服务端)
    *   [1.2 客户端](#客户端)
*   [2 配置](#配置)
    *   [2.1 设置授权](#设置授权)
        *   [2.1.1 使用 polkit](#使用_polkit)
        *   [2.1.2 基于文件的权限授权](#基于文件的权限授权)
    *   [2.2 守护进程](#守护进程)
    *   [2.3 非加密的 TCP/IP sockets](#非加密的_TCP/IP_sockets)
    *   [2.4 用主机名访问虚拟机](#用主机名访问虚拟机)
*   [3 测试](#测试)
*   [4 管理](#管理)
    *   [4.1 virsh](#virsh)
    *   [4.2 存储池](#存储池)
        *   [4.2.1 用 virsh 新建存储池](#用_virsh_新建存储池)
        *   [4.2.2 用 virt-manager 新建存储池](#用_virt-manager_新建存储池)
    *   [4.3 存储卷](#存储卷)
        *   [4.3.1 用 virsh 新建卷](#用_virsh_新建卷)
        *   [4.3.2 virt-manager 后备存储类型的 bug](#virt-manager_后备存储类型的_bug)
    *   [4.4 域](#域)
        *   [4.4.1 用 virt-install 新建域](#用_virt-install_新建域)
        *   [4.4.2 用 virt-manager 新建域](#用_virt-manager_新建域)
        *   [4.4.3 管理域](#管理域)
    *   [4.5 网络](#网络)
        *   [4.5.1 IPv6](#IPv6)
    *   [4.6 快照](#快照)
        *   [4.6.1 创建快照](#创建快照)
    *   [4.7 其他管理操作](#其他管理操作)
*   [5 Python 连接代码](#Python_连接代码)
*   [6 UEFI 支持](#UEFI_支持)
*   [7 PulseAudio](#PulseAudio)
*   [8 参阅](#参阅)

## 安装

基于守护进程/客户端的架构的 libvirt 只需要安装在需要要实现虚拟化的机器上。注意，服务器和客户端可以是相同的物理机器。

### 服务端

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [libvirt](https://www.archlinux.org/packages/?name=libvirt) 以及至少一个虚拟运行环境（hypervisor）：

*   [libvirt 的 KVM/QEMU 驱动](http://libvirt.org/drvqemu.html) 是 *libvirt* 的首选驱动，如果 KVM 功能已 [启用](/index.php/QEMU_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#启用_KVM "QEMU (简体中文)")，则支持全虚拟化和硬件加速的客户机。详见 [QEMU](/index.php/QEMU_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "QEMU (简体中文)")。

*   其他[受支持的虚拟运行环境](http://libvirt.org/drivers.html)，包括 [LXC](/index.php/LXC "LXC")、[VirtualBox](/index.php/VirtualBox "VirtualBox") 和 [Xen](/index.php/Xen "Xen")。请参见它们各自的安装说明。
    *   [Libvirt 的 LXC 驱动](http://libvirt.org/drvlxc.html) 并不依赖 [lxc](https://www.archlinux.org/packages/?name=lxc) 提供的用户空间工具。因此，即便需要使用这个驱动也并不是必须安装该工具。
    *   Libvirt 能支持 [Xen](/index.php/Xen "Xen")，但默认未内建支持。需要用 [ABS](/index.php/ABS "ABS") 编辑 [libvirt](https://www.archlinux.org/packages/?name=libvirt) 的 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") ，去掉 `--without-xen` 选项后重新构建（built）libvirt。由于 VirtualBox 尚未正式支持 Xen，所以应当用 `--without-vbox` 选项替换前述选项。

对于网络连接，安装这些包：

*   [ebtables](https://www.archlinux.org/packages/?name=ebtables) **和** [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) 用于 [默认的](http://wiki.libvirt.org/page/VirtualNetworking#The_default_configuration) NAT/DHCP网络
*   [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils) 用于桥接网络
*   [openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat) 通过 [SSH](/index.php/SSH "SSH") 远程管理

### 客户端

客户端是用于管理和访问虚拟机的用户界面。

*   **virsh** — *virsh* 是用于管理和配置域（虚拟机）的命令行程序。

	[https://libvirt.org/](https://libvirt.org/) || [libvirt](https://www.archlinux.org/packages/?name=libvirt)

*   **[GNOME Boxes](https://en.wikipedia.org/wiki/GNOME_Boxes "wikipedia:GNOME Boxes")** — 简单的 GNOME 3 程序，可以访问远程虚拟系统。

	[https://wiki.gnome.org/Apps/Boxes](https://wiki.gnome.org/Apps/Boxes) || [gnome-boxes](https://www.archlinux.org/packages/?name=gnome-boxes)

*   **Libvirt Sandbox** — 应用程序沙箱工具包。

	[https://sandbox.libvirt.org/](https://sandbox.libvirt.org/) || [libvirt-sandbox](https://aur.archlinux.org/packages/libvirt-sandbox/)

*   **Remote Viewer** — 简单的远程访问工具。

	[https://virt-manager.org/](https://virt-manager.org/) || [virt-viewer](https://www.archlinux.org/packages/?name=virt-viewer)

*   **Qt VirtManager** — 管理虚拟机的Qt程序。

	[https://github.com/F1ash/qt-virt-manager](https://github.com/F1ash/qt-virt-manager) || [qt-virt-manager](https://aur.archlinux.org/packages/qt-virt-manager/)

*   **[Virtual Machine Manager](https://en.wikipedia.org/wiki/Virtual_Machine_Manager "wikipedia:Virtual Machine Manager")** — 使用libvirt对KVM，Xen，LXC进行管理的图形化工具。

	[https://virt-manager.org/](https://virt-manager.org/) || [virt-manager](https://www.archlinux.org/packages/?name=virt-manager)

兼容 libvirt 的软件列表见 [这里](http://libvirt.org/apps.html).

## 配置

对于***系统*** 级别的管理任务（如：全局配置和镜像*卷* 位置），libvirt 要求至少要[设置授权](#设置授权)和[启动守护进程](#守护进程)。

**注意:** 对于用户***会话*** 级别的管理任务，守护进程的安装和设置*不是* 必须的。授权总是仅限本地，前台程序将启动一个 **libvirtd** 守护进程的本地实例。

### 设置授权

来自 [libvirt：连接授权](http://libvirt.org/auth.html#ACL_server_config)：

	Libvirt 守护进程允许管理员分别为客户端连接的每个网络 socket 选择不同授权机制。这主要是通过 libvirt 守护进程的主配置文件 `/etc/libvirt/libvirtd.conf` 来实现的。每个 libvirt socket 可以有独立的授权机制配置。目前的可选项有 `none`、`polkit` 和 `sasl`。

由于 [libvirt](https://www.archlinux.org/packages/?name=libvirt) 在安装时将把 [polkit](https://www.archlinux.org/packages/?name=polkit) 作为依赖一并安装，所以 [polkit](#使用_polkit) 通常是 `unix_sock_auth` 参数的默认值（[来源](http://libvirt.org/auth.html#ACL_server_polkit)）。但[基于文件的权限](#基于文件的权限授权)仍然可用。

#### 使用 polkit

**注意:** 为使 `polkit` 认证工作正常，应该重启一次系统。

*libvirt* 守护进程在 polkit 策略配置文件（`/usr/share/polkit-1/actions/org.libvirt.unix.policy`）中提供了两种**策略**（参阅：[Polkit (简体中文)#操作](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#操作 "Polkit (简体中文)")）：

*   `org.libvirt.unix.manage` 面向完全的管理访问（读写模式后台 socket），以及
*   `org.libvirt.unix.monitor` 面向仅监视察看访问（只读 socket）。

默认的面向读写模式后台 socket 的策略将请求认证为管理员。这点类似于 [sudo](/index.php/Sudo_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Sudo (简体中文)") 认证，但它并不要求客户应用最终以 root 身份运行。默认策略下也仍然允许任何应用连接到只读 socket。

Arch Linux 默认 `wheel` 组的所有用户都是管理员身份：定义于 `/etc/polkit-1/rules.d/50-default.rules`（参阅：[Polkit (简体中文)#管理员身份认证](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#管理员身份认证 "Polkit (简体中文)")）。这样就不必新建组和规则文件。 **如果用户是 `wheel` 组的成员**：只要连接到了读写模式 socket（例如通过 [virt-manager](https://www.archlinux.org/packages/?name=virt-manager)）就会被提示输入该用户的口令。

**注意:** 要求口令的提示由系统中的认证代理给出（参阅：[Polkit (简体中文)#身份认证组件](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#身份认证组件 "Polkit (简体中文)")）。文本控制台默认的认证代理是 `pkttyagent` 它可能因工作不正常而导致各种问题。

**提示：** 如果要配置无口令认证，参阅 [Polkit (简体中文)#跳过口令提示](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#跳过口令提示 "Polkit (简体中文)")。

从 libvirt 1.2.16 版开始（提案见：[[1]](http://libvirt.org/git/?p=libvirt.git;a=commit;h=e94979e901517af9fdde358d7b7c92cc055dd50c)），`libvirt` 组的成员用户默认可以无口令访问读写模式 socket。最简单的判断方法就是看 libvirt 组是否存在并且用户是否该组成员。 你可能想要修改授权以读写模式访问socket的组，例如，你想授权`kvm`组，可创建下面的文件：

 `/etc/polkit-1/rules.d/50-libvirt.rules` 
```
/* Allow users in kvm group to manage the libvirt daemon without authentication（允许 kvm 组的用户管理 libvirt 而无需认证）
*/
polkit.addRule(function(action, subject) {
    if (action.id == "org.libvirt.unix.manage" &&
        subject.isInGroup("kvm")) {
            return polkit.Result.YES;
    }
});

```

然后[添加用户](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#其它用户管理示例 "Users and groups (简体中文)")到 `kvm` 组并重新登录。*kvm* 也可以是任何其它存在的组并且用户是该组成员（详阅[用户和用户组](/index.php/%E7%94%A8%E6%88%B7%E5%92%8C%E7%94%A8%E6%88%B7%E7%BB%84 "用户和用户组")）。

修改组之后不要忘记重新登录才能生效。

#### 基于文件的权限授权

为了给 *libvirt* 组用户定义基于文件的权限以管理虚拟机，取消下列行的注释：

 `/etc/libvirt/libvirtd.conf` 
```
#unix_sock_group = "libvirt"
#unix_sock_ro_perms = "0777"  # set to 0770 to deny non-group libvirt users
#unix_sock_rw_perms = "0770"
#auth_unix_ro = "none"
#auth_unix_rw = "none"

```

有些资料提到可以通过改变某些特定 libvirt 目录的权限以简化管理。需要记住的是：包更新时，这些变更会丢失。如要修改这些系统目录的权限，需要 root 用户权限。

### 守护进程

`libvirtd.service` 和 `virtlogd.service`这两个服务单元都要[启动](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#使用单元 "Systemd (简体中文)")。可以把 `libvirtd.service` 设置为[启用](/index.php/Enable "Enable")，这时系统将同时启用 `virtlogd.service` 和 `virtlockd.socket` 两个服务[单元](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#使用单元 "Systemd (简体中文)")，因此后二者不必再设置为**启用**。

### 非加密的 TCP/IP sockets

**警告:** 这种方法常用于在可信网络中快速连接远程域做协助。这是***最不安全*** 的连接方式，应当*仅仅* 用于测试或用于安全、私密和可信的网络环境。这时 SASL 没有启用，所以所有的 TCP 通讯都是明文传输。在正式的应用场合应当*始终* 启用 SASL。

编辑 `/etc/libvirt/libvirtd.conf`：

 `/etc/libvirt/libvirtd.conf` 
```
listen_tls = 0
listen_tcp = 1
auth_tcp="none"

```

同时需要编辑`/etc/conf.d/libvirtd`以在监听模式下启动服务：

 `/etc/conf.d/libvirtd`  `LIBVIRTD_ARGS="--listen"` 

### 用主机名访问虚拟机

在非隔离的、桥接的网络中从宿主机访问客户机，可以通过启用 [libvirt](https://www.archlinux.org/packages/?name=libvirt) 提供的 `libvirt` NSS 模块实现。

编辑 `/etc/nsswitch.conf`：

 `/etc/nsswitch.conf` 
```
hosts: files libvirt dns myhostname

```

**注意:** `ping` 和 `ssh` 这类命令用于虚拟机主机名可以正常工作，但 `host` 和 `nslookup` 这类命令可能会失败或产生非预期结果，因后者依赖 DNS 。应改用 `getent hosts <vm-hostname>` 命令。

## 测试

测试 libvirt 在*系统*级工作是否正常：

```
$ virsh -c qemu:///system

```

测试 libvirt 在用户*会话*级工作是否正常：

```
$ virsh -c qemu:///session

```

## 管理

绝大部分的 libvirt 管理可以通过三个工具实现：[virt-manager](https://www.archlinux.org/packages/?name=virt-manager)（图形界面）、`virsh` 和 `guestfish`（它是 [libguestfs](https://www.archlinux.org/packages/?name=libguestfs) 的一部分）。

### virsh

Visrsh 用于管理客户*域*（虚拟机），在脚本式虚拟化管理环境中工作良好。由于需要通过通讯管道与虚拟运行环境通讯，绝大部分 virsh 命令需要管理员权限。尽管如此，一些典型的管理操作如域的创建、运行等也可以像VirtualBox 那样以普通用户身份执行。

Virsh 允许带命令行选项执行。如果不带则进入其内置的交互式终端：`virsh`。交互式终端支持 tab 键命令补全。

从命令行执行：

```
$ virsh [可选项] <命令> [参数]...

```

在交互式终端里运行：

```
virsh # <命令> [参数]...

```

帮助也是可用的：

```
$ virsh help [option*] or [group-keyword*]

```

### 存储池

存储池是指保存*卷*的位置。Libvirt 中*卷*的定义相当于其他系统中*虚拟磁盘*或*虚拟机镜像*的概念。存储池应该是一个目录、一个网络文件系统或一个分区（此处包括 [LVM](/index.php/LVM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LVM (简体中文)")）。存储池可以在活动与不活动之间切换，可以为其分配存储空间。

在*系统*级别，默认被激活的存储池是 `/var/lib/libvirt/images/`；在用户*会话*级别，`virt-manager` 将存储池创建在 `$HOME/VirtualMachines` 目录。

列出活动和不活动的存储池的命令：

```
$ virsh pool-list --all

```

#### 用 virsh 新建存储池

以下示例为*添加*存储池、目录和 LVM 卷的方法：

```
$ virsh pool-define-as name type [source-host] [source-path] [source-dev] [source-name] [<target>] [--source-format format]
$ virsh pool-define-as *poolname* dir - - - - /home/*username*/.local/libvirt/images
$ virsh pool-define-as *poolname* fs - -  */dev/vg0/images* - *mntpoint*

```

上述示例仅仅定义了存储池的信息，下面创建它：

```
$ virsh pool-build     *poolname*
$ virsh pool-start     *poolname*
$ virsh pool-autostart *poolname*

```

删除它的命令：

```
$ virsh pool-undefine  *poolname*

```

**提示：** 对于 LVM 存储池而言：

*   最佳实践是仅把一个卷组分配给一个存储池。
*   请为存储池选择一个与 LVM 卷组不同的名字。否则当存储池被删除时，该卷组也将被删除。

#### 用 virt-manager 新建存储池

首先，连接到虚拟运行环境（例如QEMU/KVM的系统/用户会话）。然后，右键点击一个**连接**（例如**QEMU/KVM**）选择**详情**，切换到**存储**选项卡，点击左下角的**+**，按照向导操作。

### 存储卷

存储池被创建之后，就可以在存储池中创建存储卷。如果你想新建一个域（虚拟机），那么这一步可以跳过，因为这一步可以在创建域的过程中完成。

#### 用 virsh 新建卷

新建卷，列出卷，变更卷大小，删除卷：

```
$ virsh vol-create-as      *poolname* *volumename* 10GiB --format aw|bochs|raw|qcow|qcow2|vmdk
$ virsh vol-upload  --pool *poolname* *volumename* *volumepath*
$ virsh vol-list           *poolname*
$ virsh vol-resize  --pool *poolname* *volumename* 12GiB
$ virsh vol-delete  --pool *poolname* *volumename*
$ virsh vol-dumpxml --pool *poolname* *volumename*  # for details.

```

#### virt-manager 后备存储类型的 bug

在较新版本的`virt-manager`中，你可以在创建新磁盘的时候选择一个后备存储（backing store）。这个功能很实用，它可以在你创建新域的时候选择基础镜像，从而节省你的时间和磁盘空间。目前的`virt-manager`有一个bug([https://bugzilla.redhat.com/show_bug.cgi?id=1235406)，导致](https://bugzilla.redhat.com/show_bug.cgi?id=1235406)，导致)`qcow2`格式的后备存储被错误的当做`raw`格式。这会让虚拟机无法读取后备存储，从而使这个功能完全失效。 这里有一个临时的解决办法。`qemu-img`长期以来都可以直接实现这个功能。如果你想在这个bug修复之前为新域创建一个后备存储，你可以使用下面的命令。

```
$ qemu-img create -f qcow2 -o backing_file=<path to backing image>,backing_fmt=qcow2 <disk name> <disk size>

```

之后你就可以以此镜像为基础创建新域，后备存储将被用作一个CoW（**C**opy **o**n **W**rite，写时复制）卷，节省你的时间和磁盘空间。

### 域

虚拟机被称作**“域”**。如果你想在命令行下操作，使用`virsh`列出，创建，暂停，关闭……域。`virt-viewer`可以用来查看使用`virsh`启动的域。域的创建通常以图形化的`virt-manager`或者命令行下的`virt-install`（一个命令行工具，是[virt-install](https://www.archlinux.org/packages/?name=virt-install)包的一部分）完成。 创建新域通常需要安装媒介，例如存储池中的`iso`文件或是直接从光驱安装。

列出活动的和不活动的域：

```
# virsh list --all

```

**注意:** [SELinux](/index.php/SELinux "SELinux")有内置策略使在`/var/lib/libvirt/images/`中的卷可以被访问。如果你使用SELinux并且在卷方面有问题，确保卷位于该目录，其他存储池标记正常。

#### 用 virt-install 新建域

对于很详细的域（虚拟机）配置，可以[#用 virt-manager 新建域](#用_virt-manager_新建域)更简单地完成。但是，基础配置同样可以用`virt-install`完成并且同样运行顺利。至少要配置`--name`, `--memory`, 存储(`--disk`, `--filesystem`,或`--nodisks`),和安装方法（通常来说是`.iso`文件或CD）。查看[virt-install(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/virt-install.1)得到未列出的选项和更多的详情。

Arch Linux（两个虚拟CPU，1 GiB内存，qcow2，用户网络）:

```
$ virt-install  \
  --name arch-linux_testing \
  --memory 1024             \ 
  --vcpus=2,maxvcpus=4      \
  --cpu host                \
  --cdrom $HOME/Downloads/arch-linux_install.iso \
  --disk size=2,format=raw  \
  --network user            \
  --virt-type kvm

```

Fedora testing (Xen, 非默认池,无默认控制台):

```
$ virt-install  \
  --connect xen:///     \
  --name fedora-testing \
  --memory 2048         \
  --vcpus=2             \
  --cpu=host            \
  --cdrom /tmp/fedora20_x84-64.iso      \
  --os-type=linux --os-variant=fedora20 \
  --disk pool=testing,size=4            \
  --network bridge=br0                  \
  --graphics=vnc                        \
  --noautoconsole
$ virt-viewer --connect xen:/// fedora-testing

```

Windows:

```
$ virt-install \
  --name=windows7           \
  --memory 2048             \
  --cdrom /dev/sr0          \
  --os-variant=win7         \
  --disk /mnt/storage/domains/windows7.qcow2,size=20GiB \
  --network network=vm-net  \
  --graphics spice

```

**提示：** 运行`osinfo-query --fields=name,short-id,version os`来获得`--os-variant`的参数，这可以帮助定制域的一些规格。然而`--memory`和`--disk`是必须被输入的。如果需要查看这些规格，可以看看`/usr/share/libosinfo/db/oses/*os*.xml`（译注：此处可能已过时）。在安装后，推荐安装[Spice Guest Tools](http://www.spice-space.org/download.html)，其中包括[VirtIO驱动](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Virtualization_Host_Configuration_and_Guest_Installation_Guide/form-Virtualization_Host_Configuration_and_Guest_Installation_Guide-Para_virtualized_drivers-Mounting_the_image_with_virt_manager.html)。Windows的VirtIO网络驱动可以在[virtio-win](https://aur.archlinux.org/packages/virtio-win/)得到。要使用VirtIO，需要在虚拟机`.xml`配置中使用`<model type='virtio' />`更多的信息可以参考[QEMU](/index.php/QEMU#Preparing_a_Windows_guest "QEMU")页面.

导入现有的卷：

```
$ virt-install  \
  --name demo  \
  --memory 512 \
  --disk /home/user/VMs/mydisk.img \
  --import

```

#### 用 virt-manager 新建域

首先，连接到虚拟运行环境（例如 QEMU/KVM *system* 或用户 *session*，在连接上右击并选择 *新建*，然后跟随向导完成。

*   在**第四步**中取消选中**立即分配全部虚拟磁盘空间**会加快创建过程并节省实际虚拟磁盘空间占用；**然而**，这将导致将来花费额外的磁盘整理时间。
*   在**第五步**中打开**高级选项**并确认**虚拟化类型**设为 **kvm**（这通常是首选模式）。如果要求附加的硬件配置，选中**安装前定制**选项。

#### 管理域

启动域：

```
$ virsh start *domain*
$ virt-viewer --connect qemu:///session *domain*

```

正常关闭域；强制关闭域:

```
$ virsh shutdown *domain*
$ virsh destroy  *domain*

```

在libvirtd启动时自动启动域:

```
$ virsh autostart *domain*
$ virsh autostart *domain* --disable

```

在宿主机关闭时自动关闭域:

	使用`libvirt-guests.service`Systemd服务，运行中的域可以在宿主机关闭时自动挂起/关闭。同时这个服务还可以让挂起/休眠的域在宿主机启动的时候自动恢复。查看`/etc/conf.d/libvirt-guests`并设置相关选项。

编辑一个域的XML配置：

```
$ virsh edit *domain*

```

**注意:** 直接被QEMU启动的虚拟机不被libvirt管理。

### 网络

[这里](https://jamielinux.com/docs/libvirt-networking-handbook/)是有关 libvirt 网络的一个正宗的概述。

默认情况下，当 `libvirtd` 服务启动后，即创建了一个名为 *default* 的 NAT 网桥与外部网络联通（仅 IPv4）。对于其他的网络连接需求，可创建下列四种类型的网络以连接到虚拟机：

*   bridge — 这是一个虚拟设备，它通过一个物理接口直接共享数据。使用场景为：宿主机有 *静态* 网络、不需与其它域连接、要占用全部进出流量，并且域运行于 *系统* 层级。有关如何在现有默认网桥时增加另一个网桥的方法，请参阅 [网桥](/index.php/%E7%BD%91%E6%A1%A5 "网桥")。网桥创建后，需要将它指定到相应客户机的 `.xml` 配置文件中。
*   network — 这是一个虚拟网络，它可以与其它虚拟机共用。使用场景为：宿主机有 *动态* 网络（例如：NetworkManager）或使用无线网络。
*   macvtap — 直接连接到宿主机的一个物理网络接口。
*   user — 本地网络，仅用于用户 *会话*。

绝大多数用户都可以通过 `virsh` 的各种可选项创建具有各种功能的网络，一般来说比通过 GUI 程序（像 `virt-manager` 之类）更容易做到。也可以按 [#用 virt-install 新建域](#用_virt-install_新建域) 所述实现。

**注意:** libvirt 通过 [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) 处理 DHCP 和 DNS 请求，以启动每个虚拟网络的不同实例。也会为特定的路由添加 iptables 规则并启用 `ip_forward` 内核参数。这也意味着宿主机上已运行的dnsmasq并不是libvirt所必须的（并可能干扰到libvirt的dnsmasq实例）。

#### IPv6

当通过任何配置工具试图添加IPv6地址时，你可能会遇到这样的错误：

```
Check the host setup: enabling IPv6 forwarding with RA routes without accept_ra set to 2 is likely to cause routes loss. Interfaces to look at: *eth0*

```

要修复这个问题，创建如下的文件（将`eth0`改为你的物理接口的名称），并且重新启动系统。

 `/etc/sysctl.d/libvirt-bridge.conf`  `net.ipv6.conf.eth0.accept_ra = 2` 

### 快照

快照保存某一时刻域的磁盘、内存和设备状态以供将来使用。快照有很多用处，例如在进行可能的破坏性操作时保存一份干净的域状态。快照使用唯一名称进行标识。

快照保存在卷之中，卷必须为qcow2或raw格式。快照使用增量存储，所以并不会占用很多空间。

#### 创建快照

Once a snapshot is taken it is saved as a new block device and the original snapshot is taken offline. Snapshots can be chosen from and also merged into another (even without shutting down the domain).

Print a running domain's volumes (running domains can be printed with `virsh list`):

 `# virsh domblklist *domain*` 
```
 Target     Source
 ------------------------------------------------
 vda        /vms/domain.img

```

To see a volume's physical properties:

 `# qemu-img info /vms/domain.img` 
```
 image: /vms/domain.img
 file format: qcow2
 virtual size: 50G (53687091200 bytes)
 disk size: 2.1G
 cluster_size: 65536

```

Create a disk-only snapshot (the option `--atomic` will prevent the volume from being modified if snapshot creation fails):

```
# virsh snapshot-create-as *domain* snapshot1 --disk-only --atomic

```

List snapshots:

 `# virsh snapshot-list *domain*` 
```
 Name                 Creation Time             State
 ------------------------------------------------------------
 snapshot1           2012-10-21 17:12:57 -0700 disk-snapshot

```

One can they copy the original image with `cp --sparse=true` or `rsync -S` and then merge the the original back into snapshot:

```
# virsh blockpull --domain *domain* --path /vms/*domain*.snapshot1

```

`domain.snapshot1` becomes a new volume. After this is done the original volume (`domain.img` and snapshot metadata can be deleted. The `virsh blockcommit` would work opposite to `blockpull` but it seems to be currently under development (including `snapshot-revert feature`, scheduled to be released sometime next year.

### 其他管理操作

连接到非默认的虚拟运行环境：

```
$ virsh --connect xen:///
virsh # uri
xen:///

```

通过SSH连接到QEMU虚拟运行环境，并且以相同方式登录：

```
$ virsh --connect qemu+ssh://*username*@*host*/system
$ LIBVIRT_DEBUG=1 virsh --connect qemu+ssh://*username*@*host*/system

```

通过SSH连接到一个图形控制台：

```
$ virt-viewer  --connect qemu+ssh://*username*@*host*/system *domain*
$ virt-manager --connect qemu+ssh://*username*@*host*/system *domain*

```

**注意:** 如果你在连接RHEL服务器（或其他不是Arch的服务器）时出现问题，尝试这两个解决方案：[FS#30748](https://bugs.archlinux.org/task/30748)[FS#22068](https://bugs.archlinux.org/task/22068).

连接到VirtualBox（libvirt对VirtualBox的支持尚不稳定，可能会导致libvirtd崩溃）:

```
$ virsh --connect vbox:///system

```

网络配置:

```
$ virsh -c qemu:///system net-list --all
$ virsh -c qemu:///system net-dumpxml default

```

## Python 连接代码

[libvirt-python](https://www.archlinux.org/packages/?name=libvirt-python)软件包提供了一个[python2](https://www.archlinux.org/packages/?name=python2)API，位于`/usr/lib/python2.7/site-packages/libvirt.py`。

一般的例子在`/usr/share/doc/libvirt-python-*your_libvirt_version*/examples/`给出。

一个[qemu](https://www.archlinux.org/packages/?name=qemu)和[openssh](https://www.archlinux.org/packages/?name=openssh)的例子（非官方）:

```
#! /usr/bin/env python2
# -*- coding: utf-8 -*-
import socket
import sys
import libvirt
if (__name__ == "__main__"):
   conn = libvirt.open("qemu+ssh://xxx/system")
   print "Trying to find node on xxx"
   domains = conn.listDomainsID()
   for domainID in domains:
       domConnect = conn.lookupByID(domainID)
       if domConnect.name() == 'xxx-node':
           print "Found shared node on xxx with ID " + str(domainID)
           domServ = domConnect
           break

```

## UEFI 支持

Libvirt 可以通过 qemu 和 [OVMF](https://github.com/tianocore/edk2) 来支持 UEFI 虚拟机。 安装 [ovmf](https://www.archlinux.org/packages/?name=ovmf) 。 添加下面的内容到 `/etc/libvirt/qemu.conf` 。

 `/etc/libvirt/qemu.conf` 
```
nvram = [
    "/usr/share/ovmf/x64/OVMF_CODE.fd:/usr/share/ovmf/x64/OVMF_VARS.fd"
]

```

*   重启 `libvirtd`

现在你可以创建一个 UEFI 虚拟机了。 你可以通过 [virt-manager](https://www.archlinux.org/packages/?name=virt-manager) 来创建。当你进行到向导的最后一步时：

*   勾选**在安装前自定义配置**，之后点击**完成**。
*   在**概况**屏幕, 将固件改为'UEFI x86_64'。
*   点击**开始安装**
*   在启动屏幕，你需要使用linuxefi命令来启动安装程序，并且你需要在系统中运行efibootmgr验证确实运行在UEFI模式下。

参考[fedora wiki](https://fedoraproject.org/wiki/Using_UEFI_with_QEMU)获得更多信息。

## PulseAudio

PulseAudio守护进程通常在你的普通用户下运行，并且只接受来自相同用户的连接。然而libvirt默认使用root运行QEMU。为了让QEMU在普通用户下运行，编辑`/etc/libvirt/qemu.conf`并将`user`设置为你的用户名。

```
user = "dave"

```

你同样需要告诉QEMU使用PulseAudio后端并识别要连接的服务器，首先将QEMU命名空间添加到你的域。 编辑域的`.xml`文件（使用`virsh edit domain`），将`domain type`行改为：

```
<domain type='kvm' xmlns:qemu='[http://libvirt.org/schemas/domain/qemu/1.0'](http://libvirt.org/schemas/domain/qemu/1.0')>

```

并且加入如下的配置（在最后一个`</devices>`之后，`</domain>`之前）：

```
 <qemu:commandline>
   <qemu:env name='QEMU_AUDIO_DRV' value='pa'/>
   <qemu:env name='QEMU_PA_SERVER' value='/run/user/1000/pulse/native'/>
 </qemu:commandline>

```

`1000`是你的用户ID，如果必要的话改为你的用户ID。

## 参阅

*   [libvirt 网站](http://libvirt.org/drvqemu.html)
*   [Red Hat 虚拟化部署和管理指南](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Virtualization_Deployment_and_Administration_Guide/index.html)
*   [Red Hat 虚拟化调优指南](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Virtualization_Tuning_and_Optimization_Guide/index.html)
*   [Slackware KVM and libvirt](http://docs.slackware.com/howtos:general_admin:kvm_libvirt)
*   [IBM KVM](http://www-01.ibm.com/support/knowledgecenter/linuxonibm/liaat/liaatkvm.htm)
*   [libvirt 网络手册](https://jamielinux.com/docs/libvirt-networking-handbook/)