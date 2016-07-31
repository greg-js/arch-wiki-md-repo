**翻譯狀態：** 本文章是 [Libvirt](/index.php/Libvirt "Libvirt") 的翻譯版本。最近一次的翻譯時間：2016-03-10。點擊[本連結](https://wiki.archlinux.org/index.php?title=Libvirt&diff=0&oldid=413990)查看英文頁面之後的變更。

Libvirt 是一組軟體的匯集，提供了管理虛擬機器和其它虛擬化功能（如：儲存和虛擬網路等）的便利途徑。這些軟體主要包括：一個長期稳定的 API、一個守護程序（libvirtd）、一些命令列工具（如virsh、virt-install等）和一些GUI工具（如virt-manager等）。Libvirt 的主要目標是提供一個單一途徑以管理多種不同虛擬化方案以及虛擬化主機，包括：[KVM/QEMU](/index.php/QEMU "QEMU")，[Xen](/index.php/Xen "Xen")，[LXC](/index.php/LXC "LXC")，[OpenVZ](http://openvz.org) 或 [VirtualBox](/index.php/VirtualBox "VirtualBox") [hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors") （[詳見這裡](http://libvirt.org/drivers.html)）。

Libvirt 的一些主要功能如下：

*   **VM management（虛擬機器管理）**：如：開機、停止、暫停、保存、恢復和迁移等；多種不同類型裝置的熱插拔操作，包括硬碟、網路卡、記憶體、CPU等。
*   **Remote machine support（支援遠端連線）**：Libvirt 的所有功能都可以在執行著libvirt daemon的機器上執行，包括遠端機器。通過最簡便且無需額外配置的 SSH 協定，遠端連線可支援多種網路連線方式。
*   **Storage management（存儲管理）**：任何執行 libvirt 守護程序的主機都可以用于管理多種類型的的存儲：創建多種類型的鏡像檔（qcow2，qed，vmdk，raw，...），掛載 NFS 共用，枚舉現有 LVM 捲軸，新增新的 LVM 磁區，對裸磁碟裝置分割，掛載 iSCSI 共用，以及更多......
*   **Network interface management（網路介面管理）**：任何執行 libvirt 守護程序的主機都可以用于管理物理的和邏輯的網路介面，枚舉現有介面，配置（和創建）介面、橋接、VLAN、連接埠綁定。
*   **Virtual NAT and Route based networking（虛擬NAT 和基於路由的網路）**：任何執行libvirt 守護程序的主機都可以管理和創建虛擬網路。Libvirt 虛擬網路使用[iptables防火牆](/index.php/Iptables "Iptables")規則實現一个路由器，為虛擬機器提供到主機網路的透明存取。

## Contents

*   [1 安裝](#.E5.AE.89.E8.A3.9D)
    *   [1.1 伺服器端](#.E4.BC.BA.E6.9C.8D.E5.99.A8.E7.AB.AF)
    *   [1.2 用戶端](#.E7.94.A8.E6.88.B6.E7.AB.AF)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 設定授權](#.E8.A8.AD.E5.AE.9A.E6.8E.88.E6.AC.8A)
        *   [2.1.1 使用 polkit](#.E4.BD.BF.E7.94.A8_polkit)
        *   [2.1.2 基於檔案的權限授權](#.E5.9F.BA.E6.96.BC.E6.AA.94.E6.A1.88.E7.9A.84.E6.AC.8A.E9.99.90.E6.8E.88.E6.AC.8A)
    *   [2.2 守護程序](#.E5.AE.88.E8.AD.B7.E7.A8.8B.E5.BA.8F)
    *   [2.3 非加密的 TCP/IP sockets](#.E9.9D.9E.E5.8A.A0.E5.AF.86.E7.9A.84_TCP.2FIP_sockets)
*   [3 测试](#.E6.B5.8B.E8.AF.95)
*   [4 管理](#.E7.AE.A1.E7.90.86)
    *   [4.1 virsh](#virsh)
    *   [4.2 儲存pool](#.E5.84.B2.E5.AD.98pool)
        *   [4.2.1 用 virsh 新增存儲Pool](#.E7.94.A8_virsh_.E6.96.B0.E5.A2.9E.E5.AD.98.E5.84.B2Pool)
        *   [4.2.2 用 virt-manager 新增儲存Pool](#.E7.94.A8_virt-manager_.E6.96.B0.E5.A2.9E.E5.84.B2.E5.AD.98Pool)
    *   [4.3 存儲磁區](#.E5.AD.98.E5.84.B2.E7.A3.81.E5.8D.80)
        *   [4.3.1 用 virsh 新增磁區](#.E7.94.A8_virsh_.E6.96.B0.E5.A2.9E.E7.A3.81.E5.8D.80)
        *   [4.3.2 virt-manager 後備儲存類型的 bug](#virt-manager_.E5.BE.8C.E5.82.99.E5.84.B2.E5.AD.98.E9.A1.9E.E5.9E.8B.E7.9A.84_bug)
    *   [4.4 虛擬機](#.E8.99.9B.E6.93.AC.E6.A9.9F)
        *   [4.4.1 用 virt-install 新增虛擬機器](#.E7.94.A8_virt-install_.E6.96.B0.E5.A2.9E.E8.99.9B.E6.93.AC.E6.A9.9F.E5.99.A8)
        *   [4.4.2 用 virt-manager 新增虛擬機器](#.E7.94.A8_virt-manager_.E6.96.B0.E5.A2.9E.E8.99.9B.E6.93.AC.E6.A9.9F.E5.99.A8)
        *   [4.4.3 管理虛擬機](#.E7.AE.A1.E7.90.86.E8.99.9B.E6.93.AC.E6.A9.9F)
    *   [4.5 網路](#.E7.B6.B2.E8.B7.AF)
    *   [4.6 快照](#.E5.BF.AB.E7.85.A7)
        *   [4.6.1 新增快照](#.E6.96.B0.E5.A2.9E.E5.BF.AB.E7.85.A7)
    *   [4.7 其他管理操作](#.E5.85.B6.E4.BB.96.E7.AE.A1.E7.90.86.E6.93.8D.E4.BD.9C)
*   [5 Python 連接代碼](#Python_.E9.80.A3.E6.8E.A5.E4.BB.A3.E7.A2.BC)
*   [6 參閱](#.E5.8F.83.E9.96.B1)

## 安裝

基於守護程序/用戶端的架構的 libvirt 只需要安裝在需要實現虛擬化的機器上。當然，libvirt伺服器和libvirt用戶端可以是相同的物理機器。

### 伺服器端

[安裝](/index.php?title=%E5%AE%89%E8%A3%9D&action=edit&redlink=1 "安裝 (page does not exist)") [libvirt](https://www.archlinux.org/packages/?name=libvirt) 以及至少一個管理程式（hypervisor）：

*   截至 2015-02-01，啟動 `libvirtd` **必須**在系統上安裝 [qemu](https://www.archlinux.org/packages/?name=qemu)（参參見[FS#41888](https://bugs.archlinux.org/task/41888)）。好在， [libvirt 的 KVM/QEMU 驅動](http://libvirt.org/drvqemu.html) 是 *libvirt* 的，如果 [KVM 功能已啟用](/index.php/QEMU#Enabling_KVM "QEMU")，首選驅動則支援全虛擬化和硬體加速加速的用戶機。詳見 [QEMU](/index.php/QEMU "QEMU")。

*   其他虛擬機器後端，包括 [LXC](/index.php/LXC "LXC"), [Xen](/index.php/Xen "Xen") 和 [VirtualBox](/index.php/VirtualBox "VirtualBox")。請參見他們各自的安裝說明。

**注意:** [Libvirt 的 LXC 驅動](http://libvirt.org/drvlxc.html) 並不依賴 [lxc](https://www.archlinux.org/packages/?name=lxc) 提供的使用這空間工具，因此，如果計畫使用這個驅動並不需要安裝該工具。

**警告:** Libvirt 預設未支援 [Xen](/index.php/Xen "Xen")。需要用 [ABS](/index.php/ABS "ABS") 編輯 [libvirt](https://www.archlinux.org/packages/?name=libvirt) 的 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") ，去掉 `--without-xen` 選項後重新構建（built）libvirt。

其它虛擬機器管理式的列表见[这里](http://libvirt.org/drivers.html)。

對於網路連線，安裝這些包：

*   [ebtables](https://www.archlinux.org/packages/?name=ebtables) **和** [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) 用於 [預設的](http://wiki.libvirt.org/page/VirtualNetworking#The_default_configuration) NAT/DHCP網路
*   [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils) 用於橋接網路
*   [openbsd-netcat](https://www.archlinux.org/packages/?name=openbsd-netcat) 經由 [SSH](/index.php/SSH "SSH") 遠端管理

### 用戶端

用戶端是用於管理和存取虛擬機器的使用者界面。

*   *virsh* 用於管理和配置（域）的命令列程式；它包含在 [libvirt](https://www.archlinux.org/packages/?name=libvirt) 中。

虛擬機* [virt-manager](https://www.archlinux.org/packages/?name=virt-manager) 用於管理虛擬機的GUI。

*   [virtviewer](https://www.archlinux.org/packages/?name=virtviewer) 用於顯示並與虛擬化用戶機作業系統進行交互
*   [gnome-boxes](https://www.archlinux.org/packages/?name=gnome-boxes) 簡單的 GNOME 3 程式，存取遠端虛擬系統
*   [libvirt-sandbox](https://aur.archlinux.org/packages/libvirt-sandbox/) 應用程式沙箱工具包

相容 libvirt 的軟體列表見[[1]](http://libvirt.org/apps.html).

## 配置

對於***系統*** 級別的管理工作（如：全局配置和鏡像位置），libvirt 要求至少要[設定授權](#.E8.A8.AD.E5.AE.9A.E6.8E.88.E6.AC.8A)和[啟動守護程序](#.E5.AE.88.E8.AD.B7.E7.A8.8B.E5.BA.8F)。

**注意:** 對於使用者***工作階段*** 級別的管理任務，守護程序的安裝和設定*不是* 必須的。授權總是僅限本地，前台程式將啟動一个 **libvirtd** 守護程序的本地實例。

### 設定授權

來自 [libvirt：連線授權](http://libvirt.org/auth.html#ACL_server_config)：

	Libvirt daemon允許管理員分別為用戶端連線的每個網路 socket 選擇不同授權機制。這主要是通過 libvirt 守護程序的主設定檔 `/etc/libvirt/libvirtd.conf` 來實現的。每個 libvirt socket 可以有獨立的授權機制配置。目前的可選項有 `none`、`polkit` 和 `sasl`。

由于 [libvirt](https://www.archlinux.org/packages/?name=libvirt) 在安裝时將把 [polkit](https://www.archlinux.org/packages/?name=polkit) 作為依赖一並安裝，所以 [polkit](#.E4.BD.BF.E7.94.A8_polkit) 通常是 `unix_sock_auth` 參數的預設值（[來源](http://libvirt.org/auth.html#ACL_server_polkit)）。但[基於檔案的權限](#.E5.9F.BA.E6.96.BC.E6.AA.94.E6.A1.88.E7.9A.84.E6.AC.8A.E9.99.90.E6.8E.88.E6.AC.8A)仍然可用。

#### 使用 polkit

**注意:** 為了使 `polkit` 認證工作正常，應該重新啟動一次系統。

*libvirt* daemon在 polkit 策略設定檔（`/usr/share/polkit-1/actions/org.libvirt.unix.policy`）中提供了2種 [行為](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.A1.8C.E4.B8.BA "Polkit (简体中文)") 策略：

*   `org.libvirt.unix.manage` 面向完全的管理存取（讀寫模式的後台 socket），以及
*   `org.libvirt.unix.monitor` 面向僅监視查看存取（唯讀 socket）。

預設的面向讀寫模式後台 socket 的策略將請求認證為管理者。這類似於 [sudo](/index.php/Sudo "Sudo") 認證，但它並不要求用戶應用最終以 root 身分執行。預設策略下也仍然允許任何應用連線到唯讀 socket。

Arch Linux 預設 `wheel` 組的所有實驗者都是管理員身分：定義於 `/etc/polkit-1/rules.d/50-default.rules`（參閱[管理员标识](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.AE.A1.E7.90.86.E5.91.98.E6.A0.87.E8.AF.86 "Polkit (简体中文)")）。這樣就不必新增組和規則檔案。 **如果用户是 `wheel` 群組的成員**：只要連線到了讀寫模式 socket（例如通过 [virt-manager](https://www.archlinux.org/packages/?name=virt-manager)）就會被提示輸入該使用者的口令。

**注意:** 要求口令的提示由系統中的 [認證代理](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.AE.A4.E8.AF.81.E4.BB.A3.E7.90.86 "Polkit (简体中文)") 給出。文本控制台預設的認證代理是 `pkttyagent` 它可能因工作不正常而導致各種問題。

**提示:** 如果要配置無密碼認證，參考 [跳過密碼提示](/index.php/Polkit#Bypass_password_prompt "Polkit")。

從 libvirt 1.2.16 開始（提案見：[[2]](http://libvirt.org/git/?p=libvirt.git;a=commit;h=e94979e901517af9fdde358d7b7c92cc055dd50c)），`libvirt` 組的成員使用者預設可以無密碼存取讀寫模式 socket。最簡單的判斷方法就是看 libvirt 組是否存在並且使用者是否為該組成員。如果要把 kvm 組存取讀寫模式後台 socket 的認證策略改為免認證模式，可創建下面的檔案：

 `/etc/polkit-1/rules.d/50-libvirt.rules` 
```
/* Allow users in kvm group to manage the libvirt daemon without authentication（允許 kvm 組的使用者管理 libvirt 而無需認證）
*/
polkit.addRule(function(action, subject) {
    if (action.id == "org.libvirt.unix.manage" &&
        subject.isInGroup("kvm")) {
            return polkit.Result.YES;
    }
});

```

然後 [新增使用者](/index.php?title=Users_and_group&action=edit&redlink=1 "Users and group (page does not exist)") 到 `kvm` 組并重新登入。*kvm* 也可以是任何其它存在的組並且用戶是該組的成員（詳情請閱讀 [使用者和使用者群組](/index.php?title=%E4%BD%BF%E7%94%A8%E8%80%85%E5%92%8C%E4%BD%BF%E7%94%A8%E8%80%85%E7%BE%A4%E7%B5%84&action=edit&redlink=1 "使用者和使用者群組 (page does not exist)")）。

修改組之後別忘了重新登入才能生效。

#### 基於檔案的權限授權

為了給 *libvirt* 組使用者定義基於檔案的權限以管理虛擬機器，取消下列行的註釋：

 `/etc/libvirt/libvirtd.conf` 
```
#unix_sock_group = "libvirt"
#unix_sock_ro_perms = "0777"  # set to 0770 to deny non-group libvirt users
#unix_sock_rw_perms = "0770"
#auth_unix_ro = "none"
#auth_unix_rw = "none"

```

有些資料提到可以通過改變某些特定 libvirt 目錄的權限以簡化管理。需要記住的是：包更新時，這些變更會遺失。如要修改這些系統目錄的權限，需要 root 使用者權限。

### 守護程序

`libvirtd.service` 和 `virtlogd.service`2個服務都要 [啟動](/index.php/Systemd_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Systemd (正體中文)")。可以把 `libvirtd.service` 設定為 [啟用](/index.php/Enable "Enable")，這時系統將同時啟用 `virtlogd.service` 和 `virtlockd.socket` 両個服務 [單元](/index.php/Systemd_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Systemd (正體中文)")，因此後二者不必再設置為啟用。

### 非加密的 TCP/IP sockets

**警告:** 這種方法常用於在可信網路中快速連線遠端虛擬機做協助。這是***最不安全*** 的連線方式，應當*僅僅* 用於測試或用於安全、私密和可信的網路環境。這時 SASL 沒有啟用，所以所有的 TCP 通訊都是明文傳輸。在正式的應用場合應當*始終* 啟用SASL。

編輯 `/etc/libvirt/libvirtd.conf`：

 `/etc/libvirt/libvirtd.conf` 
```
listen_tls = 0
listen_tcp = 1
auth_tcp=none

```

It is also necessary to start the server in listening mode by editing `/etc/conf.d/libvirtd`:

 `/etc/conf.d/libvirtd`  `LIBVIRTD_ARGS="--listen"` 

## 测试

To test if libvirt is working properly on a *system* level:

```
$ virsh -c qemu:///system

```

To test if libvirt is working properly for a user-*session*:

```
$ virsh -c qemu:///session

```

## 管理

Libvirt management is done mostly with three tools: [virt-manager](https://www.archlinux.org/packages/?name=virt-manager) (GUI), `virsh`, and `guestfish` (which is part of [libguestfs](https://aur.archlinux.org/packages/libguestfs/)).

### virsh

The virsh program is for managing guest *domains* (virtual machines) and works well for scripting, virtualization administration. Though most virsh commands require root privileges to run due to the communication channels used to talk to the hypervisor, typical management, creation, and running of domains (like that done with VirtualBox) can be done as a regular user.

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

### 儲存pool

A pool is a location where storage *volumes* can be kept. What libvirt defines as *volumes* others may define as "virtual disks" or "virtual machine images". Pool locations may be a directory, a network filesystem, or partition (this includes a [LVM](/index.php/LVM "LVM")). Pools can be toggled active or inactive and allocated for space.

On the *system*-level, `/var/lib/libvirt/images/` will be activated by default; on a user-*session*, `virt-manager` creates `$HOME/VirtualMachines`.

Print active and inactive storage pools:

```
$ virsh pool-list --all

```

#### 用 virsh 新增存儲Pool

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

#### 用 virt-manager 新增儲存Pool

First, connect to a hypervisor (e.g. QEMU/KVM *system*, or user-*session*). Then, right-click on a connection and select *Details*; select the *Storage* tab, push the *+* button on the lower-left, and follow the wizard.

### 存儲磁區

Once the pool has been created, volumes can be created inside the pool. *If building a new domain (virtual machine), this step can be skipped as a volume can be created in the domain creation process.*

#### 用 virsh 新增磁區

Create volume, list volumes, resize, and delete:

```
$ virsh vol-create-as      *poolname* *volumename* 10GiB
$ virsh vol-list           *poolname*
$ virsh vol-resize  --pool *poolname* *volumename* 12GiB
$ virsh vol-delete  --pool *poolname* *volumename*
$ virsh vol-dumpxml --pool *poolname* *volumename*  # for details.

```

#### virt-manager 後備儲存類型的 bug

On newer versions of `virt-manager` you can now specify a backing store to use when creating a new disk. This is very useful, in that you can have new domains be based on base images saving you both time and disk space when provisioning new virtual systems. There is a bug ([https://bugzilla.redhat.com/show_bug.cgi?id=1235406](https://bugzilla.redhat.com/show_bug.cgi?id=1235406)) in the current version of `virt-manager` which causes `virt-manager` to choose the wrong type of the backing image in the case where the backing image is a `qcow2` type. In this case, it will errantly pick the backing type as `raw`. This will cause the new image to be unable to read from the backing store, and effectively remove the utility of having a backing store at all.

There is a workaround for this issue. `qemu-img` has long been able to do this operation directly. If you wish to have a backing store for your new domain before this bug is fixed, you may use the following command.

```
$ qemu-img create -f qcow2 -o backing_file=<path to backing image>,backing_fmt=qcow2 <disk name> <disk size>

```

Then you can use this image as the base for your new domain and it will use the backing store as a COW volume saving you time and disk space.

### 虛擬機

Virtual machines are called *domains*. If working from the command line, use `virsh` to list, create, pause, shutdown domains, etc. `virt-viewer` can be used to view domains started with `virsh`. Creation of domains is typically done either graphically with `virt-manager` or with `virt-install` (a command line program that is part of the [virt-manager](https://www.archlinux.org/packages/?name=virt-manager) package).

Creating a new domain typically involves using some installation media, such as an `.iso` from the storage pool or an optical drive.

Print active and inactive domains:

```
# virsh list --all

```

**Note:** [SELinux](/index.php/SELinux "SELinux") has a built-in exemption for libvirt that allows volumes in `/var/lib/libvirt/images/` to be accessed. If using SELinux and there are issues with the volumes, ensure that volumes are in that directory, or ensure that other storage pools are correctly labeled.

#### 用 virt-install 新增虛擬機器

For an extremely detailed domain (virtual machine) setup, it is easier to [#用 virt-manager 新增虛擬機器](#.E7.94.A8_virt-manager_.E6.96.B0.E5.A2.9E.E8.99.9B.E6.93.AC.E6.A9.9F.E5.99.A8). However, basics can easily be done with `virt-install` and still run quite well. Minimum specifications are `--name`, `--memory`, guest storage (`--disk`, `--filesystem`, or `--nodisks`), and an install method (generally an `.iso` or CD).

Arch Linux install (two GiB, raw format volume create; user-networking):

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

**Tip:** Run `osinfo-query --fields=name,version os` to get argument for `--os-variant`; this will help define some specifications for the domain. However, `--memory` and `--disk` will need to be entered; one can look within the appropriate `/usr/share/libosinfo/db/oses/*os*.xml` if needing these specifications. After installing, it will likely be preferable to install the [Spice Guest Tools](http://www.spice-space.org/download.html) that include the [VirtIO drivers](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Virtualization_Host_Configuration_and_Guest_Installation_Guide/form-Virtualization_Host_Configuration_and_Guest_Installation_Guide-Para_virtualized_drivers-Mounting_the_image_with_virt_manager.html). For a Windows VirtIO network driver there is also [virtio-win](https://aur.archlinux.org/packages/virtio-win/). These drivers are referenced by a `<model type='virtio' />` in the guest's `.xml` configuration section for the device. A bit more information can also be found on the [QEMU article](/index.php/QEMU#Preparing_a_Windows_guest "QEMU").

Import existing volume:

```
$ virt-install  \
  --name demo  \
  --memory 512 \
  --disk /home/user/VMs/mydisk.img \
  --import

```

#### 用 virt-manager 新增虛擬機器

首先，連線到虛擬機的Hypervisor（例如 QEMU/KVM *system* 或使用這 *session*，在“連線”上右鍵按一下並選擇 *新增*，然後跟隨 新增虛擬機器精靈 完成。

*   在**第五步**中打開**進階選項**並確認**虛擬化類型**设为 **KVM**（這通常是首選模式）。如果要求附加的硬體配置，選中**安裝前定制**選項。

#### 管理虛擬機

啟動虛擬機器：

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

### 網路

[此處](https://jamielinux.com/docs/libvirt-networking-handbook/)是有有關libvirt 網路的一个正宗的概述。

預設情況下，當 `libvird` 服務啟動後，即創建了一个名為 *default* 的 NAT 網橋与外部網路聯通（警告：參閱 [#"default" 網路的 bug](#.22default.22_.E7.B6.B2.E8.B7.AF.E7.9A.84_bug)）。對於其他的網路連線需求，可創建下列4種類型的網路讓虛擬機連線到網路：

*   bridge — 這是一個虛擬裝置，它通過一個物理介面直接共享網路資料。使用場合為：宿主機有 *靜態* 網路、虛擬機不需與其它虛擬機連接、虛擬機要佔用全部進出流量，並且虛擬機執行於*系統* 層級。有關如何在現有預設網橋時增加另一個網橋的方法，參閱 [網橋](/index.php?title=%E7%B6%B2%E6%A9%8B&action=edit&redlink=1 "網橋 (page does not exist)")。網橋創建後，需要將它指定到相應客戶機的 `.xml` 設定檔中。
*   network — 這是一個虛擬網路，它可以與其它虛擬機共用。使用場景为：宿主機有 *動態* 網路（例如：NetworkManager）或使用無線網路。
*   macvtap — 直接連線到宿主機的一個物理網路介面。
*   user — 本地網路，僅用於使用者 *工作階段*。

絕大多數用戶都可以通過 `virsh` 的各種可選項創建具有各種功能的網路，一般來說比通過 GUI 程式（像 `virt-manager` 等）更容易做到。也可以按 [#用 virt-install 新增虛擬機](#.E7.94.A8_virt-install_.E6.96.B0.E5.A2.9E.E8.99.9B.E6.93.AC.E6.A9.9F) 實現。

**注意:** libvirt 通過 [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) 處理 DHCP 和 DNS 請求，以啟動每個虛擬網路的不同實例。也會為特定的路由添加 iptables 規則並啟用 `ip_forward` 內核參數。

### 快照

Snapshots take the disk, memory, and device state of a domain at a point-of-time, and save it for future use. They have many uses, from saving a "clean" copy of an OS image to saving a domain's state before a potentially destructive operation. Snapshots are identified with a unique name.

Snapshots are saved within the volume itself and the volume must be the format: qcow2 or raw. Snapshots use deltas so they have the potentiality to not take much space.

#### 新增快照

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

## Python 連接代碼

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

## 參閱

*   [libvirt網站](http://libvirt.org/drvqemu.html)
*   [Red Hat 虛擬化部署和管理指南](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Virtualization_Deployment_and_Administration_Guide/index.html)