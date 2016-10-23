**翻译状态：** 本文是英文页面 [Libvirt](/index.php/Libvirt "Libvirt") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-10-21，点击[这里](https://wiki.archlinux.org/index.php?title=Libvirt&diff=0&oldid=454633)可以查看翻译后英文页面的改动。

Libvirt 是一组软件的汇集，提供了管理虚拟机和其它虚拟化功能（如：存储和网络接口等）的便利途径。这些软件包括：一个长期稳定的 C 语言 API、一个守护进程（libvirtd）和一个命令行工具（virsh）。Libvirt 的主要目标是提供一个单一途径以管理多种不同虚拟化方案以及虚拟化主机，包括：[KVM/QEMU](/index.php/QEMU "QEMU")，[Xen](/index.php/Xen "Xen")，[LXC](/index.php/LXC "LXC")，[OpenVZ](http://openvz.org) 或 [VirtualBox](/index.php/VirtualBox "VirtualBox") [hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors") （[详见这里](http://libvirt.org/drivers.html)）。

Libvirt 的一些主要功能如下：

*   **VM management（虚拟机管理）**：各种虚拟机生命周期的操作，如：启动、停止、暂停、保存、恢复和迁移等；多种不同类型设备的热插拔操作，包括磁盘、网络接口、内存、CPU等。
*   **Remote machine support（支持远程连接）**：Libvirt 的所有功能都可以在运行着 libvirt 守护进程的机器上执行，包括远程机器。通过最简便且无需额外配置的 SSH 协议，远程连接可支持多种网络连接方式。
*   **Storage management（存储管理）**：任何运行 libvirt 守护进程的主机都可以用于管理多种类型的存储：创建多种类型的文件镜像（qcow2，vmdk，raw，...），挂载 NFS 共享，枚举现有 LVM 卷组，创建新的 LVM 卷组和逻辑卷，对裸磁盘设备分区，挂载 iSCSI 共享，以及更多......
*   **Network interface management（网络接口管理）**：任何运行 libvirt 守护进程的主机都可以用于管理物理的和逻辑的网络接口，枚举现有接口，配置（和创建）接口、桥接、VLAN、端口绑定。
*   **Virtual NAT and Route based networking（虚拟 NAT 和基于路由的网络）**：任何运行 libvirt 守护进程的主机都可以管理和创建虚拟网络。Libvirt 虚拟网络使用防火墙规则实现一个路由器，为虚拟机提供到主机网络的透明访问。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 服务端](#.E6.9C.8D.E5.8A.A1.E7.AB.AF)
    *   [1.2 客户端](#.E5.AE.A2.E6.88.B7.E7.AB.AF)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 设置授权](#.E8.AE.BE.E7.BD.AE.E6.8E.88.E6.9D.83)
        *   [2.1.1 使用 polkit](#.E4.BD.BF.E7.94.A8_polkit)
        *   [2.1.2 基于文件的权限授权](#.E5.9F.BA.E4.BA.8E.E6.96.87.E4.BB.B6.E7.9A.84.E6.9D.83.E9.99.90.E6.8E.88.E6.9D.83)
    *   [2.2 守护进程](#.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
    *   [2.3 非加密的 TCP/IP sockets](#.E9.9D.9E.E5.8A.A0.E5.AF.86.E7.9A.84_TCP.2FIP_sockets)
    *   [2.4 用主机名访问虚拟机](#.E7.94.A8.E4.B8.BB.E6.9C.BA.E5.90.8D.E8.AE.BF.E9.97.AE.E8.99.9A.E6.8B.9F.E6.9C.BA)
*   [3 测试](#.E6.B5.8B.E8.AF.95)
*   [4 管理](#.E7.AE.A1.E7.90.86)
    *   [4.1 virsh](#virsh)
    *   [4.2 存储池](#.E5.AD.98.E5.82.A8.E6.B1.A0)
        *   [4.2.1 用 virsh 新建存储池](#.E7.94.A8_virsh_.E6.96.B0.E5.BB.BA.E5.AD.98.E5.82.A8.E6.B1.A0)
        *   [4.2.2 用 virt-manager 新建存储池](#.E7.94.A8_virt-manager_.E6.96.B0.E5.BB.BA.E5.AD.98.E5.82.A8.E6.B1.A0)
    *   [4.3 存储卷](#.E5.AD.98.E5.82.A8.E5.8D.B7)
        *   [4.3.1 用 virsh 新建卷](#.E7.94.A8_virsh_.E6.96.B0.E5.BB.BA.E5.8D.B7)
        *   [4.3.2 virt-manager 后备存储类型的 bug](#virt-manager_.E5.90.8E.E5.A4.87.E5.AD.98.E5.82.A8.E7.B1.BB.E5.9E.8B.E7.9A.84_bug)
    *   [4.4 虚拟机](#.E8.99.9A.E6.8B.9F.E6.9C.BA)
        *   [4.4.1 用 virt-install 新建虚拟机](#.E7.94.A8_virt-install_.E6.96.B0.E5.BB.BA.E8.99.9A.E6.8B.9F.E6.9C.BA)
        *   [4.4.2 用 virt-manager 新建虚拟机](#.E7.94.A8_virt-manager_.E6.96.B0.E5.BB.BA.E8.99.9A.E6.8B.9F.E6.9C.BA)
        *   [4.4.3 管理虚拟机](#.E7.AE.A1.E7.90.86.E8.99.9A.E6.8B.9F.E6.9C.BA)
    *   [4.5 网络](#.E7.BD.91.E7.BB.9C)
    *   [4.6 快照](#.E5.BF.AB.E7.85.A7)
        *   [4.6.1 创建快照](#.E5.88.9B.E5.BB.BA.E5.BF.AB.E7.85.A7)
    *   [4.7 其他管理操作](#.E5.85.B6.E4.BB.96.E7.AE.A1.E7.90.86.E6.93.8D.E4.BD.9C)
*   [5 Python 连接代码](#Python_.E8.BF.9E.E6.8E.A5.E4.BB.A3.E7.A0.81)
*   [6 UEFI 支持](#UEFI_.E6.94.AF.E6.8C.81)
    *   [6.1 OVMF - QEMU workaround](#OVMF_-_QEMU_workaround)
*   [7 PulseAudio](#PulseAudio)
*   [8 参阅](#.E5.8F.82.E9.98.85)

## 安装

基于守护进程/客户端的架构的 libvirt 只需要安装在需要要实现虚拟化的机器上。注意，服务器和客户端可以是相同的物理机器。

### 服务端

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [libvirt](https://www.archlinux.org/packages/?name=libvirt) 以及至少一个管理程序（hypervisor）：

*   [libvirt 的 KVM/QEMU 驱动](http://libvirt.org/drvqemu.html) 是 *libvirt* 的首选驱动，如果 [KVM 功能已启用](/index.php/QEMU#Enabling_KVM "QEMU")，则支持全虚拟化和硬件加速的客户机。详见 [QEMU](/index.php/QEMU "QEMU")。

*   其他[受支持的管理程序](http://libvirt.org/drivers.html)，包括 [LXC](/index.php/LXC "LXC")、[VirtualBox](/index.php/VirtualBox "VirtualBox") 和 [Xen](/index.php/Xen "Xen")。请参见它们各自的安装说明。
    *   [Libvirt 的 LXC 驱动](http://libvirt.org/drvlxc.html) 并不依赖 [lxc](https://www.archlinux.org/packages/?name=lxc) 提供的用户空间工具。因此，即便需要使用这个驱动也并不是必须安装该工具。
    *   Libvirt 能支持 [Xen](/index.php/Xen "Xen")，但默认未内建支持。需要用 [ABS](/index.php/ABS "ABS") 编辑 [libvirt](https://www.archlinux.org/packages/?name=libvirt) 的 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") ，去掉 `--without-xen` 选项后重新构建（built）libvirt。由于 VirtualBox 尚未正式支持 Xen，所以应当用 `--without-vbox` 选项替换前述选项。

对于网络连接，安装这些包：

*   [ebtables](https://www.archlinux.org/packages/?name=ebtables) **和** [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) 用于 [默认的](http://wiki.libvirt.org/page/VirtualNetworking#The_default_configuration) NAT/DHCP网络
*   [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils) 用于桥接网络
*   [openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat) 通过 [SSH](/index.php/SSH "SSH") 远程管理

### 客户端

客户端是用于管理和访问虚拟机的用户界面。

*   *virsh* 用于管理和配置虚拟机（域）的命令行程序；它包含在 [libvirt](https://www.archlinux.org/packages/?name=libvirt) 中。
*   [virt-manager](https://www.archlinux.org/packages/?name=virt-manager) 用于管理虚拟机的图形用户界面。
*   [virtviewer](https://www.archlinux.org/packages/?name=virtviewer) 轻量级界面，用于显示并与虚拟化客户机操作系统进行交互
*   [gnome-boxes](https://www.archlinux.org/packages/?name=gnome-boxes) 简单的 GNOME 3 程序，访问远程虚拟系统
*   [virt-manager-qt5](https://aur.archlinux.org/packages/virt-manager-qt5/)
*   [libvirt-sandbox](https://aur.archlinux.org/packages/libvirt-sandbox/) 应用程序沙箱工具包

兼容 libvirt 的软件列表见 [这里](http://libvirt.org/apps.html).

## 配置

对于***系统*** 级别的管理任务（如：全局配置和镜像*卷* 位置），libvirt 要求至少要[设置授权](#.E8.AE.BE.E7.BD.AE.E6.8E.88.E6.9D.83)和[启动守护进程](#.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)。

**注意:** 对于用户***会话*** 级别的管理任务，守护进程的安装和设置*不是* 必须的。授权总是仅限本地，前台程序将启动一个 **libvirtd** 守护进程的本地实例。

### 设置授权

来自 [libvirt：连接授权](http://libvirt.org/auth.html#ACL_server_config)：

	Libvirt 守护进程允许管理员分别为客户端连接的每个网络 socket 选择不同授权机制。这主要是通过 libvirt 守护进程的主配置文件 `/etc/libvirt/libvirtd.conf` 来实现的。每个 libvirt socket 可以有独立的授权机制配置。目前的可选项有 `none`、`polkit` 和 `sasl`。

由于 [libvirt](https://www.archlinux.org/packages/?name=libvirt) 在安装时将把 [polkit](https://www.archlinux.org/packages/?name=polkit) 作为依赖一并安装，所以 [polkit](#.E4.BD.BF.E7.94.A8_polkit) 通常是 `unix_sock_auth` 参数的默认值（[来源](http://libvirt.org/auth.html#ACL_server_polkit)）。但[基于文件的权限](#.E5.9F.BA.E4.BA.8E.E6.96.87.E4.BB.B6.E7.9A.84.E6.9D.83.E9.99.90.E6.8E.88.E6.9D.83)仍然可用。

#### 使用 polkit

**注意:** 为使 `polkit` 认证工作正常，应该重启一次系统。

*libvirt* 守护进程在 polkit 策略配置文件（`/usr/share/polkit-1/actions/org.libvirt.unix.policy`）中提供了两种 [操作](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E6.93.8D.E4.BD.9C "Polkit (简体中文)")策略：

*   `org.libvirt.unix.manage` 面向完全的管理访问（读写模式后台 socket），以及
*   `org.libvirt.unix.monitor` 面向仅监视察看访问（只读 socket）。

默认的面向读写模式后台 socket 的策略将请求认证为管理员。这点类似于 [sudo](/index.php/Sudo_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Sudo (简体中文)") 认证，但它并不要求客户应用最终以 root 身份运行。默认策略下也仍然允许任何应用连接到只读 socket。

Arch Linux 默认 `wheel` 组的所有用户都是管理员身份：定义于 `/etc/polkit-1/rules.d/50-default.rules`（参阅[管理员身份认证](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.AE.A1.E7.90.86.E5.91.98.E8.BA.AB.E4.BB.BD.E8.AE.A4.E8.AF.81 "Polkit (简体中文)")）。这样就不必新建组和规则文件。 **如果用户是 `wheel` 组的成员**：只要连接到了读写模式 socket（例如通过 [virt-manager](https://www.archlinux.org/packages/?name=virt-manager)）就会被提示输入该用户的口令。

**注意:** 要求口令的提示由系统中的[认证代理](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.BA.AB.E4.BB.BD.E8.AE.A4.E8.AF.81.E7.BB.84.E4.BB.B6 "Polkit (简体中文)")给出。文本控制台默认的认证代理是 `pkttyagent` 它可能因工作不正常而导致各种问题。

**提示:** 如果要配置无口令认证，参阅[跳过口令提示](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.B7.B3.E8.BF.87.E5.8F.A3.E4.BB.A4.E6.8F.90.E7.A4.BA "Polkit (简体中文)")。

从 libvirt 1.2.16 版开始（提案见：[[1]](http://libvirt.org/git/?p=libvirt.git;a=commit;h=e94979e901517af9fdde358d7b7c92cc055dd50c)），`libvirt` 组的成员用户默认可以无口令访问读写模式 socket。最简单的判断方法就是看 libvirt 组是否存在并且用户是否该组成员。如果要把 kvm 组访问读写模式后台 socket 的认证策略改为免认证模式，可创建下面的文件：

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

然后[添加用户](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.85.B6.E5.AE.83.E7.94.A8.E6.88.B7.E7.AE.A1.E7.90.86.E7.A4.BA.E4.BE.8B "Users and groups (简体中文)")到 `kvm` 组并重新登录。*kvm* 也可以是任何其它存在的组并且用户是该组成员（详阅[用户和用户组](/index.php/%E7%94%A8%E6%88%B7%E5%92%8C%E7%94%A8%E6%88%B7%E7%BB%84 "用户和用户组")）。

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

`libvirtd.service` 和 `virtlogd.service`这两个服务单元都要[启动](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)")。可以把 `libvirtd.service` 设置为[启用](/index.php/Enable "Enable")，这时系统将同时启用 `virtlogd.service` 和 `virtlockd.socket` 两个服务[单元](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)")，因此后二者不必再设置为**启用**。

### 非加密的 TCP/IP sockets

**警告:** 这种方法常用于在可信网络中快速连接远程虚拟机做协助。这是***最不安全*** 的连接方式，应当*仅仅* 用于测试或用于安全、私密和可信的网络环境。这时 SASL 没有启用，所以所有的 TCP 通讯都是明文传输。在正式的应用场合应当*始终* 启用 SASL。

编辑 `/etc/libvirt/libvirtd.conf`：

 `/etc/libvirt/libvirtd.conf` 
```
listen_tls = 0
listen_tcp = 1
auth_tcp=none

```

It is also necessary to start the server in listening mode by editing `/etc/conf.d/libvirtd`:

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

绝大部分的 libvirt 管理可以通过三个工具实现：[virt-manager](https://www.archlinux.org/packages/?name=virt-manager)（图形界面）、`virsh` 和 `guestfish`（它是 [libguestfs](https://aur.archlinux.org/packages/libguestfs/) 的一部分）。

### virsh

Visrsh 用于管理客户*域*（即 虚拟机），在脚本式虚拟化管理环境中工作良好。Though most virsh commands require root privileges to run due to the communication channels used to talk to the hypervisor, typical management, creation, and running of domains (like that done with VirtualBox) can be done as a regular user.

Virsh includes an interactive terminal that can be entered if no commands are passed (options are allowed though): `virsh`. The interactive terminal has support for tab completion.

From the command line:

```
$ virsh [option] <command> [argument]...

```

From the interactive terminal:

```
virsh # <command> [argument]...

```

Help is available:

```
$ virsh help [option*] or [group-keyword*]

```

### 存储池

A pool is a location where storage *volumes* can be kept. What libvirt defines as *volumes* others may define as "virtual disks" or "virtual machine images". Pool locations may be a directory, a network filesystem, or partition (this includes a [LVM](/index.php/LVM "LVM")). Pools can be toggled active or inactive and allocated for space.

On the *system*-level, `/var/lib/libvirt/images/` will be activated by default; on a user-*session*, `virt-manager` creates `$HOME/VirtualMachines`.

Print active and inactive storage pools:

```
$ virsh pool-list --all

```

#### 用 virsh 新建存储池

If wanted to *add* a storage pool, here are examples of the command form, adding a directory, and adding a LVM volume:

```
$ virsh pool-define-as name type [source-host] [source-path] [source-dev] [source-name] [<target>] [--source-format format]
$ virsh pool-define-as *poolname* dir - - - - /home/*username*/.local/libvirt/images
$ virsh pool-define-as *poolname* fs - -  */dev/vg0/images* - *mntpoint*

```

The above command defines the information for the pool, to build it:

```
$ virsh pool-build     *poolname*
$ virsh pool-start     *poolname*
$ virsh pool-autostart *poolname*

```

To remove it:

```
$ virsh pool-undefine  *poolname*

```

**Tip:** For LVM storage pools:

*   It is a good practice to dedicate a volume group to the storage pool only.
*   Choose a LVM volume group that differs from the pool name, otherwise when the storage pool is deleted the LVM group will be too.

#### 用 virt-manager 新建存储池

First, connect to a hypervisor (e.g. QEMU/KVM *system*, or user-*session*). Then, right-click on a connection and select *Details*; select the *Storage* tab, push the *+* button on the lower-left, and follow the wizard.

### 存储卷

Once the pool has been created, volumes can be created inside the pool. *If building a new domain (virtual machine), this step can be skipped as a volume can be created in the domain creation process.*

#### 用 virsh 新建卷

Create volume, list volumes, resize, and delete:

```
$ virsh vol-create-as      *poolname* *volumename* 10GiB --format aw|bochs|raw|qcow|qcow2|vmdk
$ virsh vol-upload  --pool *poolname* *volumename* *volumepath*
$ virsh vol-list           *poolname*
$ virsh vol-resize  --pool *poolname* *volumename* 12GiB
$ virsh vol-delete  --pool *poolname* *volumename*
$ virsh vol-dumpxml --pool *poolname* *volumename*  # for details.

```

#### virt-manager 后备存储类型的 bug

On newer versions of `virt-manager` you can now specify a backing store to use when creating a new disk. This is very useful, in that you can have new domains be based on base images saving you both time and disk space when provisioning new virtual systems. There is a bug ([https://bugzilla.redhat.com/show_bug.cgi?id=1235406](https://bugzilla.redhat.com/show_bug.cgi?id=1235406)) in the current version of `virt-manager` which causes `virt-manager` to choose the wrong type of the backing image in the case where the backing image is a `qcow2` type. In this case, it will errantly pick the backing type as `raw`. This will cause the new image to be unable to read from the backing store, and effectively remove the utility of having a backing store at all.

There is a workaround for this issue. `qemu-img` has long been able to do this operation directly. If you wish to have a backing store for your new domain before this bug is fixed, you may use the following command.

```
$ qemu-img create -f qcow2 -o backing_file=<path to backing image>,backing_fmt=qcow2 <disk name> <disk size>

```

Then you can use this image as the base for your new domain and it will use the backing store as a COW volume saving you time and disk space.

### 虚拟机

虚拟机被称作“域”。 If working from the command line, use `virsh` to list, create, pause, shutdown domains, etc. `virt-viewer` can be used to view domains started with `virsh`. Creation of domains is typically done either graphically with `virt-manager` or with `virt-install` (a command line program installed as part of the [virt-install](https://www.archlinux.org/packages/?name=virt-install) package).

Creating a new domain typically involves using some installation media, such as an `.iso` from the storage pool or an optical drive.

Print active and inactive domains:

```
# virsh list --all

```

**Note:** [SELinux](/index.php/SELinux "SELinux") has a built-in exemption for libvirt that allows volumes in `/var/lib/libvirt/images/` to be accessed. If using SELinux and there are issues with the volumes, ensure that volumes are in that directory, or ensure that other storage pools are correctly labeled.

#### 用 virt-install 新建虚拟机

For an extremely detailed domain (virtual machine) setup, it is easier to [#用 virt-manager 新建虚拟机](#.E7.94.A8_virt-manager_.E6.96.B0.E5.BB.BA.E8.99.9A.E6.8B.9F.E6.9C.BA). However, basics can easily be done with `virt-install` and still run quite well. Minimum specifications are `--name`, `--memory`, guest storage (`--disk`, `--filesystem`, or `--nodisks`), and an install method (generally an `.iso` or CD).See `man virt-install` for more details and information about unlisted options.

Arch Linux install (two GiB, qcow2 format volume create; user-networking):

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

Fedora testing (Xen hypervisor, non-default pool, do not originally view):

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

**Tip:** Run `osinfo-query --fields=name,short-id,version os` to get argument for `--os-variant`; this will help define some specifications for the domain. However, `--memory` and `--disk` will need to be entered; one can look within the appropriate `/usr/share/libosinfo/db/oses/*os*.xml` if needing these specifications. After installing, it will likely be preferable to install the [Spice Guest Tools](http://www.spice-space.org/download.html) that include the [VirtIO drivers](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Virtualization_Host_Configuration_and_Guest_Installation_Guide/form-Virtualization_Host_Configuration_and_Guest_Installation_Guide-Para_virtualized_drivers-Mounting_the_image_with_virt_manager.html). For a Windows VirtIO network driver there is also [virtio-win](https://aur.archlinux.org/packages/virtio-win/). These drivers are referenced by a `<model type='virtio' />` in the guest's `.xml` configuration section for the device. A bit more information can also be found on the [QEMU article](/index.php/QEMU#Preparing_a_Windows_guest "QEMU").

Import existing volume:

```
$ virt-install  \
  --name demo  \
  --memory 512 \
  --disk /home/user/VMs/mydisk.img \
  --import

```

#### 用 virt-manager 新建虚拟机

首先，连接到虚拟机超级管理器（例如 QEMU/KVM *system* 或用户 *session*，在连接上右击并选择 *新建*，然后跟随向导完成。

*   在**第四步**中取消选中**立即分配全部虚拟磁盘空间**会加快创建过程并节省实际虚拟磁盘空间占用；**然而**，这将导致将来花费额外的磁盘整理时间。
*   在**第五步**中打开**高级选项**并确认**虚拟化类型**设为 **kvm**（这通常是首选模式）。如果要求附加的硬件配置，选中**安装前定制**选项。

#### 管理虚拟机

启动虚拟机：

```
$ virsh start *domain*
$ virt-viewer --connect qemu:///session *domain*

```

Gracefully attempt to shutdown a domain; force off a domain:

```
$ virsh shutdown *domain*
$ virsh destroy  *domain*

```

Autostart domain on libvirtd start:

```
$ virsh autostart *domain*
$ virsh autostart *domain* --disable

```

Shutdown domain on host shutdown:

	Running domains can be automatically suspended/shutdown at host shutdown using the `libvirt-guests.service` systemd service. This same service will resume/startup the suspended/shutdown domain automatically at host startup. Read `/etc/conf.d/libvirt-guests` for service options.

Edit a domain's XML configuration:

```
$ virsh edit *domain*

```

**Note:** Virtual Machines started directly by QEMU are not managable by libvirt tools.

### 网络

[这里](https://jamielinux.com/docs/libvirt-networking-handbook/)是有关 libvirt 网络的一个正宗的概述。

默认情况下，当 `libvirtd` 服务启动后，即创建了一个名为 *default* 的 NAT 网桥与外部网络联通（警告：参阅 [#"default" 网络的 bug](#.22default.22_.E7.BD.91.E7.BB.9C.E7.9A.84_bug)）。对于其他的网络连接需求，可创建下列四种类型的网络以连接到虚拟机：

*   bridge — 这是一个虚拟设备，它通过一个物理接口直接共享数据。使用场景为：宿主机有 *静态* 网络、虚拟机不需与其它虚拟机连接、虚拟机要占用全部进出流量，并且虚拟机运行于 *系统* 层级。有关如何在现有默认网桥时增加另一个网桥的方法，请参阅 [网桥](/index.php/%E7%BD%91%E6%A1%A5 "网桥")。网桥创建后，需要将它指定到相应客户机的 `.xml` 配置文件中。
*   network — 这是一个虚拟网络，它可以与其它虚拟机共用。使用场景为：宿主机有 *动态* 网络（例如：NetworkManager）或使用无线网络。
*   macvtap — 直接连接到宿主机的一个物理网络接口。
*   user — 本地网络，仅用于用户 *会话*。

绝大多数用户都可以通过 `virsh` 的各种可选项创建具有各种功能的网络，一般来说比通过 GUI 程序（像 `virt-manager` 之类）更容易做到。也可以按 [#用 virt-install 新建虚拟机](#.E7.94.A8_virt-install_.E6.96.B0.E5.BB.BA.E8.99.9A.E6.8B.9F.E6.9C.BA) 所述实现。

**注意:** libvirt 通过 [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) 处理 DHCP 和 DNS 请求，以启动每个虚拟网络的不同实例。也会为特定的路由添加 iptables 规则并启用 `ip_forward` 内核参数。This also means that having dnsmasq running on the host system is not necessary to support libvirt requirements (and could interfere with libvirt dnsmasq instances).

### 快照

Snapshots take the disk, memory, and device state of a domain at a point-of-time, and save it for future use. They have many uses, from saving a "clean" copy of an OS image to saving a domain's state before a potentially destructive operation. Snapshots are identified with a unique name.

Snapshots are saved within the volume itself and the volume must be the format: qcow2 or raw. Snapshots use deltas so they have the potentiality to not take much space.

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

Connect to non-default hypervisor:

```
$ virsh --connect xen:///
virsh # uri
xen:///

```

Connect to the QEMU hypervisor over SSH; and the same with logging:

```
$ virsh --connect qemu+ssh://*username*@*host*/system
$ LIBVIRT_DEBUG=1 virsh --connect qemu+ssh://*username*@*host*/system

```

Connect a graphic console over SSH:

```
$ virt-viewer  --connect qemu+ssh://*username*@*host*/system *domain*
$ virt-manager --connect qemu+ssh://*username*@*host*/system *domain*

```

**Note:** If you are having problems connecting to a remote RHEL server (or anything other than Arch, really), try the two workarounds mentioned in [FS#30748](https://bugs.archlinux.org/task/30748) and [FS#22068](https://bugs.archlinux.org/task/22068).

Connect to the VirtualBox hypervisor (*VirtualBox support in libvirt is not stable yet and may cause libvirtd to crash*):

```
$ virsh --connect vbox:///system

```

Network configurations:

```
$ virsh -c qemu:///system net-list --all
$ virsh -c qemu:///system net-dumpxml default

```

## Python 连接代码

The [libvirt-python](https://www.archlinux.org/packages/?name=libvirt-python) package provides a [python2](https://www.archlinux.org/packages/?name=python2) API in `/usr/lib/python2.7/site-packages/libvirt.py`.

General examples are given in `/usr/share/doc/libvirt-python-*your_libvirt_version*/examples/`

Unofficial example using [qemu](https://www.archlinux.org/packages/?name=qemu) and [openssh](https://www.archlinux.org/packages/?name=openssh):

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

Libvirt can suport UEFI virtual machines through QEMU and [OVMF](https://github.com/tianocore/edk2).

Currently this is possible in Arch Linux through a workaround. [This ovmf packaging bug](https://bugs.archlinux.org/index.php?do=details&action=details.addvote&task_id=47101) needs to be resolved for this to work out of the box or with minimal configuration of `/etc/libvirt/qemu.conf`.

### OVMF - QEMU workaround

*   Build [ovmf](https://www.archlinux.org/packages/?name=ovmf) from the [ABS](/index.php/ABS "ABS") with `makepkg`.
*   Copy the `OVMF_CODE.fd` and `OVMF_VARS.fd` files either for 64 or 32 bit to the default qemu location.

 `/etc/libvirt/qemu.conf` 
```
#nvram = [
#   "/usr/share/OVMF/OVMF_CODE.fd:/usr/share/OVMF/OVMF_VARS.fd",
#   "/usr/share/OVMF/OVMF_CODE.secboot.fd:/usr/share/OVMF/OVMF_VARS.fd",
#   "/usr/share/AAVMF/AAVMF_CODE.fd:/usr/share/AAVMF/AAVMF_VARS.fd"
#]

```

```
# mkdir /usr/share/OVMF
# cp src/edk2/Build/OvmfX64/RELEASE_GCC49/FV/OVMF_CODE.fd src/edk2/Build/OvmfX64/RELEASE_GCC49/FV/OVMF_VARS.fd /usr/share/OVMF/ 

```

*   Restart `libvirtd`

```
 # systemctl stop libvirtd
 # systemctl start libvirtd

```

Now you are ready to create a uefi virtual machine. Create a new virtual machine through [virt-manager](https://www.archlinux.org/packages/?name=virt-manager). When you get to the final page of the 'New VM' wizard, do the following:

*   Click 'Customize before install', then select 'Finish'
*   On the 'Overview' screen, Change the 'Firmware' field to select the 'UEFI x86_64' option.
*   Click 'Begin Installation'
*   The boot screen you'll see should use linuxefi commands to boot the installer, and you should be able to run efibootmgr inside that system, to verify that you're running an UEFI OS.

For more information about this, refer to [this fedora wiki page](https://fedoraproject.org/wiki/Using_UEFI_with_QEMU).

## PulseAudio

The PulseAudio daemon normally runs under your regular user account, and will only accept connections from the same user. This can be a problem if QEMU is being run as root through [libvirt](/index.php/Libvirt "Libvirt"). To run QEMU as a regular user, edit `/etc/libvirt/qemu.conf` and set the `user` option to your username.

```
user = "dave"

```

You will also need to tell QEMU to use the PulseAudio backend and identify the server to connect to. Add the following section to your domain configuration using `virsh edit`.

```
 <qemu:commandline>
   <qemu:env name='QEMU_AUDIO_DRV' value='pa'/>
   <qemu:env name='QEMU_PA_SERVER' value='/run/user/1000/pulse/native'/>
 </qemu:commandline>

```

`1000` is your user id. Change it if necessary.

## 参阅

*   [libvirt 网站](http://libvirt.org/drvqemu.html)
*   [Red Hat 虚拟化部署和管理指南](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Virtualization_Deployment_and_Administration_Guide/index.html)
*   [Red Hat 虚拟化调优指南](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Virtualization_Tuning_and_Optimization_Guide/index.html)
*   [Slackware KVM and libvirt](http://docs.slackware.com/howtos:general_admin:kvm_libvirt)
*   [IBM KVM](http://www-01.ibm.com/support/knowledgecenter/linuxonibm/liaat/liaatkvm.htm)
*   [libvirt 网络手册](https://jamielinux.com/docs/libvirt-networking-handbook/)