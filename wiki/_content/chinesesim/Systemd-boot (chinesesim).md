**翻译状态：** 本文是英文页面 [Systemd-boot](/index.php/Systemd-boot "Systemd-boot") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-01-18，点击[这里](https://wiki.archlinux.org/index.php?title=Systemd-boot&diff=0&oldid=412593)可以查看翻译后英文页面的改动。

**systemd-boot** (以前被称为**gummiboot**) 是可以执行 EFI 镜像文件的简单 UEFI 启动管理器。启动的内容可以通过一个配置(glob)或者屏幕菜单选择。[systemd](https://www.archlinux.org/packages/?name=systemd) 从版本 220-2 开始包含此组件。

配置很简单，但是只能启动 EFI 可执行程序，例如 Linux 内核 [EFISTUB](/index.php/EFISTUB "EFISTUB"), UEFI Shell, GRUB, Windows Boot Manager等。

**Warning:** systemd-boot 提供了引导EFISTUB内核的简单接口，如果你在启动EFISTUB内核时遇到了困难(例如[FS#33745](https://bugs.archlinux.org/task/33745)), 你应该使用像[GRUB](/index.php/GRUB "GRUB"), [Syslinux](/index.php/Syslinux "Syslinux") 或 [ELILO](/index.php/Boot_loaders#ELILO "Boot loaders")这样的不使用EFISTUB的启动管理器.

**Note:** 本文用 `$esp` 表示[EFI 系统分区](/index.php/EFI_System_Partition "EFI System Partition")，也就是 ESP 的挂载位置。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 在UEFI 引导下安装](#.E5.9C.A8UEFI_.E5.BC.95.E5.AF.BC.E4.B8.8B.E5.AE.89.E8.A3.85)
    *   [1.2 在传统启动下安装](#.E5.9C.A8.E4.BC.A0.E7.BB.9F.E5.90.AF.E5.8A.A8.E4.B8.8B.E5.AE.89.E8.A3.85)
    *   [1.3 更新](#.E6.9B.B4.E6.96.B0)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 基本配置](#.E5.9F.BA.E6.9C.AC.E9.85.8D.E7.BD.AE)
    *   [2.2 增加启动选项](#.E5.A2.9E.E5.8A.A0.E5.90.AF.E5.8A.A8.E9.80.89.E9.A1.B9)
        *   [2.2.1 一般的安装选项](#.E4.B8.80.E8.88.AC.E7.9A.84.E5.AE.89.E8.A3.85.E9.80.89.E9.A1.B9)
        *   [2.2.2 根分区在LVM 逻辑卷上时](#.E6.A0.B9.E5.88.86.E5.8C.BA.E5.9C.A8LVM_.E9.80.BB.E8.BE.91.E5.8D.B7.E4.B8.8A.E6.97.B6)
        *   [2.2.3 加密的根分区](#.E5.8A.A0.E5.AF.86.E7.9A.84.E6.A0.B9.E5.88.86.E5.8C.BA)
        *   [2.2.4 根分区是btrfs子卷](#.E6.A0.B9.E5.88.86.E5.8C.BA.E6.98.AFbtrfs.E5.AD.90.E5.8D.B7)
        *   [2.2.5 EFI Shells 或其他 EFI 应用程序](#EFI_Shells_.E6.88.96.E5.85.B6.E4.BB.96_EFI_.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [2.3 对休眠的支持](#.E5.AF.B9.E4.BC.91.E7.9C.A0.E7.9A.84.E6.94.AF.E6.8C.81)
*   [3 启动选单中的按键操作](#.E5.90.AF.E5.8A.A8.E9.80.89.E5.8D.95.E4.B8.AD.E7.9A.84.E6.8C.89.E9.94.AE.E6.93.8D.E4.BD.9C)
*   [4 排除问题](#.E6.8E.92.E9.99.A4.E9.97.AE.E9.A2.98)
    *   [4.1 通过efibootmgr手动添加启动选项](#.E9.80.9A.E8.BF.87efibootmgr.E6.89.8B.E5.8A.A8.E6.B7.BB.E5.8A.A0.E5.90.AF.E5.8A.A8.E9.80.89.E9.A1.B9)
    *   [4.2 在Windows升级后不能看到启动菜单](#.E5.9C.A8Windows.E5.8D.87.E7.BA.A7.E5.90.8E.E4.B8.8D.E8.83.BD.E7.9C.8B.E5.88.B0.E5.90.AF.E5.8A.A8.E8.8F.9C.E5.8D.95)
*   [5 参阅](#.E5.8F.82.E9.98.85)

## 安装

### 在UEFI 引导下安装

1.  确认启动方式是 UEFI 模式
2.  验证[可以正确访问 EFI 变量](/index.php/Unified_Extensible_Firmware_Interface#Requirements_for_UEFI_variable_support "Unified Extensible Firmware Interface")
3.  EFI 系统分区正确挂载，而且内核和 initramfs 已经被复制到 ESP。 systemd-boot 无法从其它分区加载 EFI 程序。 建议将 ESP 挂载到 `/boot`. 如果希望 ESP 和 /boot 分离，请查看后面的 [#更新](#.E6.9B.B4.E6.96.B0)部分。
4.  执行下面命令将 systemd-boot 程序复制到 EFI 系统分区并将 systemd-boot 安装成EFI启动管理器的默认的 EFI 程序。

```
# bootctl --path=*$esp* install

```

### 在传统启动下安装

**Warning:** 这不是建议的方法!

如果你以传统方式(MBR)启动电脑,或许能成功安装,不过需要在安装之后像你的固件提供如何启动systemd-boot的相关信息,为此你需要:

*   一个EFI Shell;
*   或是你的UEFI 固件设置中提供了更改启动选项的界面.

**Note:** 例如某些 Dell Latitude 计算机上,UEFI固件设置界面提供了设置EFI启动所需的工具,而EFI Shell 无法修改那些设置.

如果能这样做的话,进入你的 EFI Shell 或是 UEFI 固件设置,修改你的默认EFI启动加载器为 `$esp/EFI/systemd/systemd-bootx64.efi` (在i686架构上是 `systemd-bootia32.efi`).

### 更新

systemd-boot (bootctl(1), systemd-efi-boot-generator(8)) 假定你的 EFI 系统分区 挂载在 `/boot`. 和 *gummiboot* 不同,Systemd-boot的升级需要用户手动进行:

```
# bootctl update  

```

如果 EFI 系统分区不在 `/boot`, 需要加入 `--path=` 参数来指定. 例如:

```
# bootctl --path=/boot/$esp update

```

## 配置

### 基本配置

基本设置保存在`$esp/loader/loader.conf`,有三个选项: The basic configuration is kept in `$esp/loader/loader.conf`, with three possible configuration options:

*   `default` –默认加载的配置文件 (不含 `.conf` 后缀); 可以使用通配符 `arch-*`

*   `timeout` –启动选单的超时时间,如果不设置的话,启动选单只有在你按住Space键时才显示.

*   `editor` -是否允许用户编辑内核参数. `1` (默认值) 是允许, `0` 是阻止. 因为用户可以通过 `init=/bin/bash` 来绕过root密码并获得root权限,建议设置成`0`.

下面是一个样例:

 `$esp/loader/loader.conf` 
```
default  arch
timeout  4
editor   0

```

你也可以在启动选单中改变默认值和超时时间,所做的改动会保存到efivars中.

### 增加启动选项

**Note:** 如果存在的话,bootctl 会自动为 "**Windows Boot Manager (Windows 启动管理器)**" (`\EFI\Microsoft\Boot\Bootmgfw.efi`), "**EFI Shell**" (`\shellx64.efi`) 和 "**EFI Default Loader**" (`\EFI\Boot\bootx64.efi`)增加启动选项. 但并不会为其他EFI应用程序创建启动选项,所以需要进行进一步设置. 如果你是和Windows 组成双重启动,建议禁用 [Windows 中的"快速启动"](/index.php/Dual_boot_with_Windows#Fast_Start-Up "Dual boot with Windows") 选项.

**Tip:** 你能用 `blkid -s PARTUUID -o value /dev/sdxY` 找到某个分区的PARTUUID, 'x' 和 'Y' 分别是磁盘和分区编号.稍后可能需要这些信息.

bootctl 会在 `$esp/loader/entries/*.conf` 搜索启动选项– 一个文件中只能包含一个启动选项,下面是参数列表:

*   `title` – **必须选项.** 系统的名称.

*   `version` – 内核版本,只在有多个`title` 时需要.

*   `machine-id` – 通过 `/etc/machine-id`用于区分不同设备的名称, 只在有多个`title` 和 `version` 时需要.

*   `efi` – 要启动的EFI应用程序的位置,以 (`$esp`) 为相对路径,; 例如 `/vmlinuz-linux`. **需要此选项或是 `linux` (参阅下文) 的一项.**

*   `options` – 传递给EFI应用程序的参数,可选.但如果你要启动linux,至少需要 `initrd=*efipath*` 和 `root=*dev*`选项.

要启动linux,你还可以指定 `linux *path-to-vmlinuz*` 和 `initrd *path-to-initramfs*`;这会自动转换成 `efi *path*` 和 `options initrd=*path*` – 这个语法只是为了方便,在功能上并没有区别.

#### 一般的安装选项

这是一个根分区既不在LVM逻辑卷又没有加密时的配置选项:

 `$esp/loader/entries/arch.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660 rw
```

注意这个例子中用PARTUUID(或是PARTLABEL)来标识一个GPT分区(和UUID/LABEL不同,它标识一个文件系统).使用因为PARTUUID/PARTLABEL是因为它不像UUID/LABEL会在格式化时改变,也不像 /dev/sd* 会在某些时候交换.在某些无文件系统分区(或是不支持卷标的LUKS 加密卷)上也能工作.

#### 根分区在LVM 逻辑卷上时

**Warning:** 如果没有一个在LVM卷组外的`/boot`分区,不要用 Systemd-boot .

这是一个根分区在[LVM](/index.php/LVM "LVM")逻辑卷上时的样例:

 `$esp/loader/entries/arch-lvm.conf` 
```
title          Arch Linux (LVM)
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=/dev/mapper/<VolumeGroup-LogicalVolume> rw
```

用实际的逻辑卷组和逻辑卷名替换 `<VolumeGroup-LogicalVolume>` (例如 `root=/dev/mapper/volgroup00-lvolroot`). 也可以使用UUID:

```
....
options  root=UUID=<UUID identifier> rw

```

#### 加密的根分区

这是一个加密的根分区 ([例如通过DM-Crypt / LUKS](/index.php/Dm-crypt "Dm-crypt"))的样例:

 `$esp/loader/entries/arch-encrypted.conf` 
```
title Arch Linux Encrypted
linux /vmlinuz-linux
initrd /initramfs-linux.img
options cryptdevice=UUID=<UUID>:<mapped-name> root=/dev/mapper/<mapped-name> quiet rw
```

这个例子中用了UUID; PARTUUID 应该也可以使用, 如果你愿意,也可以用UUID替换/dev/段. 参阅 [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration").

你也可以加入类似于 `\EFI\arch\grub.efi`的EFI应用程序.

#### 根分区是btrfs子卷

如果用[btrfs](/index.php/Btrfs "Btrfs")子卷作为根分区,记得加入 `rootflags=subvol=<root 子卷名称>`到`options`选项中,在这个例子中,根分区挂载在名称为'ROOT'的btrfs子卷中 (例如 `mount -o subvol=ROOT /dev/sdxY /mnt`):

 `$esp/loader/entries/arch-btrfs-subvol.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=PARTUUID=14420948-2cea-4de7-b042-40f67c618660 rw rootflags=subvol=ROOT
```

如果做不到这一点的话,会出现这样的错误消息: `ERROR: Root device mounted successfully, but /sbin/init does not exist.`

#### EFI Shells 或其他 EFI 应用程序

你可以像这样加载EFI Shell或其他EFI应用程序:

 `$esp/loader/entries/uefi-shell-v1-x86_64.conf` 
```
title  UEFI Shell x86_64 v1
efi    /EFI/shellx64_v1.efi
```
 `$esp/loader/entries/uefi-shell-v2-x86_64.conf` 
```
title  UEFI Shell x86_64 v2
efi    /EFI/shellx64_v2.efi
```

### 对休眠的支持

参阅 [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## 启动选单中的按键操作

启动选单中支持的按键操作有:

*   `Up/Down` - 选择选项
*   `Enter` - 加载所选的选项
*   `d` - 设置默认的启动选项 (会保存在 EFI 变量中)
*   `-/T` - 增加超时时间 (会保存在 EFI 变量中)
*   `+/t` - 减少超时时间 (会保存在 EFI 变量中)
*   `e` - 编辑内核参数,如果 `editor` 选项设置为`0`,则没有任何作用.
*   `v` - 显示版本信息
*   `Q` - 退出
*   `P` - 显示目前的配置
*   `h/?` - 帮助

这些热键可以在启动管理器时直接指定启动哪一个选项

*   `l` - Linux
*   `w` - Windows
*   `a` - OS X
*   `s` - EFI Shell
*   `1-9` -选项的编号

## 排除问题

### 通过efibootmgr手动添加启动选项

如果运行`bootctl install` 命令失败,你可以通过 [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr)手动增加选项:

```
# efibootmgr -c -d /dev/sdX -p Y -l /EFI/systemd/systemd-bootx64.efi -L "Linux Boot Manager"

```

用[EFI 系统分区](/index.php/UEFI#EFI_System_Partition "UEFI")的设备名称替换`/dev/sdXY`.

### 在Windows升级后不能看到启动菜单

例如你升级Windows 后直接启动了Windows而不是选择启动菜单:

*   确定UEFI固件设置中的"安全启动"(Secure Boot) 和 [Windows 中的"快速启动"](/index.php/Dual_boot_with_Windows#Fast_Start-Up "Dual boot with Windows") 选项没有启用.
*   确定UEFI固件设置的启动顺序中Linux Boot Manager 先于 Windows Boot Manager.

**Note:** Windows 8.x+,和 Windows 10,可能会覆盖你在UEFI固件设置中设置的启动顺序并把自己设置成第一启动选项. 所以你应该知道如何修改"一次性启动选项".

你可以通过组策略和一个批处理文件(".bat")来阻止Windows更改启动设置,在Windows上这样做:

1.  以管理员身份打开命令提示符,运行 `bcdedit /enum firmware`
2.  寻找描述中带有"linux"的启动选项,例如 "Linux Boot Manager"
3.  复制带大括号的描述符, 例如 `{31d0d5f4-22ad-11e5-b30b-806e6f6e6963}`
4.  创建一个批处理文件 (例如 `bootorder.bat`) ,包含下列的内容: `bcdedit /set {fwbootmgr} DEFAULT {*这里是你在第三步中获得的描述符*}` (例如 `bcdedit /set {fwbootmgr} DEFAULT {31d0d5f4-22ad-11e5-b30b-806e6f6e6963}`).
5.  运行 *gpedit (组策略对象编辑器)* 在 *本地计算机策略 > 计算机设置 > Windows 设置 > 脚本(启动/关机)*中,选择"启动,会打开一个名为"启动选项:的对话框.
6.  添加第四步中创建的批处理文件到"脚本"列表中.

或者让Windows 启动管理器加载systemd-boot的EFI应用程序,要这样做的话在Windows上以管理员身份运行:

```
bcdedit /set {bootmgr} path \EFI\systemd\systemd-bootx64.efi

```

## 参阅

*   [http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/)