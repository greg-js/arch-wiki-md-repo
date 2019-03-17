相关文章

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Secure Boot](/index.php/Secure_Boot "Secure Boot")
*   [Unified Extensible Firmware Interface (简体中文)](/index.php/Unified_Extensible_Firmware_Interface_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Unified Extensible Firmware Interface (简体中文)")

**翻译状态：** 本文是英文页面 [Systemd-boot](/index.php/Systemd-boot "Systemd-boot") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-03-16，点击[这里](https://wiki.archlinux.org/index.php?title=Systemd-boot&diff=0&oldid=567880)可以查看翻译后英文页面的改动。

**systemd-boot** (以前被称为**gummiboot**) 是可以执行 EFI 镜像文件的简单 UEFI 启动管理器。启动的内容可以通过一个配置(glob)或者屏幕菜单选择。Arch 默认安装的 [systemd](https://www.archlinux.org/packages/?name=systemd) 提供了这个功能。

配置很简单，但是只能启动 EFI 可执行程序，例如 Linux 内核 [EFISTUB](/index.php/EFISTUB "EFISTUB"), UEFI Shell, GRUB, Windows Boot Manager等。

**Note:** 本文用 `$esp` 表示[EFI 系统分区](/index.php/EFI_system_partition "EFI system partition")，也就是 ESP 的挂载位置。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
    *   [1.1 安装 EFI 启动管理器](#安装_EFI_启动管理器)
    *   [1.2 更新 EFI 启动管理器](#更新_EFI_启动管理器)
        *   [1.2.1 手动更新](#手动更新)
        *   [1.2.2 自动更新](#自动更新)
*   [2 配置](#配置)
    *   [2.1 基本配置](#基本配置)
    *   [2.2 增加启动选项](#增加启动选项)
        *   [2.2.1 一般的安装选项](#一般的安装选项)
        *   [2.2.2 根分区在LVM 逻辑卷上时](#根分区在LVM_逻辑卷上时)
        *   [2.2.3 加密的根分区](#加密的根分区)
        *   [2.2.4 根分区是btrfs子卷](#根分区是btrfs子卷)
        *   [2.2.5 EFI Shells 或其他 EFI 应用程序](#EFI_Shells_或其他_EFI_应用程序)
    *   [2.3 对休眠的支持](#对休眠的支持)
*   [3 启动选单中的按键操作](#启动选单中的按键操作)
*   [4 排除问题](#排除问题)
    *   [4.1 在传统启动下安装](#在传统启动下安装)
    *   [4.2 通过efibootmgr手动添加启动选项](#通过efibootmgr手动添加启动选项)
    *   [4.3 在Windows升级后不能看到启动菜单](#在Windows升级后不能看到启动菜单)
*   [5 参阅](#参阅)

## 安装

### 安装 EFI 启动管理器

要安装 *systemd-boot* EFI 启动管理器，首先确保启动方式是 UEFI 模式，可以访问 [UEFI 变量](/index.php/Unified_Extensible_Firmware_Interface#UEFI_variables "Unified Extensible Firmware Interface")。用 `efivar --list` 命令进行检查。

*systemd-boot* 仅可以从[ESP](/index.php/EFI_system_partition "EFI system partition") 分区加载 [EFISTUB](/index.php/EFISTUB "EFISTUB") 内核。要持续更新内核，建议将 ESP 挂载到 `/boot`. 如果没将 ESP 挂载到 `/boot`,需要手动将内核和 initramfs 复制到 ESP. 详情请参考 [EFI system partition#Alternative mount points](/index.php/EFI_system_partition#Alternative_mount_points "EFI system partition") .

下面的例子中会用 `$esp` 代替 EFI 系统分区的实际位置，例如 `/boot`。

ESP 挂载到 `*esp*` 后，使用 [bootctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bootctl.1) 将 *systemd-boot* 安装到 EFI 系统分区：

```
# bootctl --path=*esp* install

```

在 x64 架构的系统上，两个完全一样的二进制文件 `*esp*/EFI/systemd/systemd-bootx64.efi` 和 `*esp*/EFI/BOOT/BOOTX64.EFI` 会被复制到 ESP. 然后将 *systemd-boot* 设置为 EFI 启动管理器的默认 EFI 程序(默认启动项)。

### 更新 EFI 启动管理器

每当 *systemd-boot* 有新版本时，用户都需要更新启动管理器。

#### 手动更新

更新 *systemd-boot* 需要使用 *bootctl*。如果没指定 `path`，会按顺序检查 `/efi`, `/boot` 和 `/boot/efi`。

```
# bootctl update

```

可以用 `path` 指定具体位置：

```
# bootctl --path=*esp* update

```

**Note:** This is also the command to use when migrating from *gummiboot*, before removing that package. If that package has already been removed, however, run `bootctl --path=*esp* install`.

#### 自动更新

The package [systemd-boot-pacman-hook](https://aur.archlinux.org/packages/systemd-boot-pacman-hook/) provides a [Pacman hook](/index.php/Pacman_hook "Pacman hook") to automate the update process. [Installing](/index.php/Install "Install") the package will add a hook which will be executed every time the [systemd](https://www.archlinux.org/packages/?name=systemd) package is upgraded. Alternatively, to replicate what the *systemd-boot-pacman-hook* package does without installing it, place the following pacman hook in the `/etc/pacman.d/hooks/` directory:

 `/etc/pacman.d/hooks/100-systemd-boot.hook` 
```
[Trigger]
Type = Package
Operation = Upgrade
Target = systemd

[Action]
Description = Updating systemd-boot
When = PostTransaction
Exec = /usr/bin/bootctl update
```

## 配置

### 基本配置

基本设置保存在`$esp/loader/loader.conf`,有三个选项: The basic configuration is kept in `$esp/loader/loader.conf`, with three possible configuration options:

*   `default` –默认加载的配置文件 (不含 `.conf` 后缀); 可以使用通配符 `arch-*`

*   `timeout` –启动选单的超时时间,如果不设置的话,启动选单只有在按键时才显示.

*   `editor` -是否允许用户编辑内核参数. `1` (默认值) 是允许, `0` 是阻止. 因为用户可以通过 `init=/bin/bash` 来绕过root密码并获得root权限,建议设置成`0`.

下面是一个样例:

 `esp/loader/loader.conf` 
```
default  arch
timeout  4
console-mode max
editor   no

```

你也可以在启动选单中改变默认值和超时时间,所做的改动会保存到efivars中.

**Tip:** `/usr/share/systemd/bootctl`包含参考示例文件.

### 增加启动选项

**Note:** 如果存在的话,bootctl 会自动为 "**Windows Boot Manager (Windows 启动管理器)**" (`\EFI\Microsoft\Boot\Bootmgfw.efi`), "**EFI Shell**" (`\shellx64.efi`) 和 "**EFI Default Loader**" (`\EFI\Boot\bootx64.efi`)增加启动选项. 但并不会为其他EFI应用程序创建启动选项,所以需要进行进一步设置. 如果你是和Windows 组成双重启动,建议禁用 [Windows 中的"快速启动"](/index.php/Dual_boot_with_Windows#Fast_Start-Up "Dual boot with Windows") 选项.

如果需要 Intel [microcode](/index.php/Microcode "Microcode")，不要忘了修改 `initrd`。

**Tip:** 你能用 `blkid -s PARTUUID -o value /dev/sdxY` 找到某个分区的PARTUUID, 'x' 和 'Y' 分别是磁盘和分区编号.稍后可能需要这些信息.

bootctl 会在 `$esp/loader/entries/*.conf` 搜索启动选项– 一个文件中只能包含一个启动选项,下面是参数列表:

*   `title` – **必须选项.** 系统的名称.

*   `version` – 内核版本,只在有多个`title` 时需要.

*   `machine-id` – 通过 `/etc/machine-id`用于区分不同设备的名称, 只在有多个`title` 和 `version` 时需要.

*   `efi` – 要启动的EFI应用程序的位置,以 (`$esp`) 为相对路径,; 例如 `/vmlinuz-linux`. **需要此选项或是 `linux` (参阅下文) 的一项.**

*   `options` – 传递给 EFI 应用程序或内核启动的参数,可选.但如果你要启动linux,至少需要 `initrd=*efipath*` 和 `root=*dev*`选项.

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

**Tip:** `/usr/share/systemd/bootctl` 提供了参考示例文件.

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

如果使用 LVM，cryptdevice 行应该类似于：

 `*esp*/loader/entries/arch-encrypted-lvm.conf` 
```
title Arch Linux Encrypted LVM
linux /vmlinuz-linux
initrd /initramfs-linux.img
options cryptdevice=UUID=<UUID>:MyVolGroup root=/dev/mapper/MyVolGroup-MyVolRoot quiet rw
```

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

### 在传统启动下安装

**Warning:** 这不是建议的方法!

如果你以传统方式(MBR)启动电脑,或许能成功安装,不过需要在安装之后像你的固件提供如何启动systemd-boot的相关信息,为此你需要:

*   一个EFI Shell;
*   或是你的UEFI 固件设置中提供了更改启动选项的界面.

**Note:** 例如某些 Dell Latitude 计算机上,UEFI固件设置界面提供了设置EFI启动所需的工具,而EFI Shell 无法修改那些设置.

如果能这样做的话,进入你的 EFI Shell 或是 UEFI 固件设置,修改你的默认EFI启动加载器为 `$esp/EFI/systemd/systemd-bootx64.efi` (在i686架构上是 `systemd-bootia32.efi`).

### 通过efibootmgr手动添加启动选项

如果运行`bootctl install` 命令失败,你可以通过 [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr)手动增加选项:

```
# efibootmgr -c -d /dev/sdX -p Y -l /EFI/systemd/systemd-bootx64.efi -L "Linux Boot Manager"

```

用[EFI 系统分区](/index.php/UEFI#EFI_System_Partition "UEFI")的设备名称替换`/dev/sdXY`.

### 在Windows升级后不能看到启动菜单

参阅[Windows 修改了启动顺序](/index.php/Unified_Extensible_Firmware_Interface_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Unified Extensible Firmware Interface (简体中文)")。

## 参阅

*   [http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/](http://www.freedesktop.org/wiki/Software/systemd/systemd-boot/)