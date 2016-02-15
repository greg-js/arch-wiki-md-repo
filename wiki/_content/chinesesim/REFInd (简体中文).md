**翻译状态：** 本文是英文页面 [rEFInd](/index.php/REFInd "REFInd") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-06-01，点击[这里](https://wiki.archlinux.org/index.php?title=rEFInd&diff=0&oldid=315512)可以查看翻译后英文页面的改动。

rEFInd 是一个 [UEFI](/index.php/Unified_Extensible_Firmware_Interface_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Unified Extensible Firmware Interface (简体中文)") 启动管理器。它是 [rEFIt](http://refit.sourceforge.net/) （不再维护）的一个分支并且针对非 Mac 硬件修复了若干问题。它被设计为平台无关，可启动多个操作系统。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 手动安装](#.E6.89.8B.E5.8A.A8.E5.AE.89.E8.A3.85)
    *   [2.1 自定义菜单项](#.E8.87.AA.E5.AE.9A.E4.B9.89.E8.8F.9C.E5.8D.95.E9.A1.B9)
*   [3 在已有的 Windows UEFI 安装中使用 rEFIND](#.E5.9C.A8.E5.B7.B2.E6.9C.89.E7.9A.84_Windows_UEFI_.E5.AE.89.E8.A3.85.E4.B8.AD.E4.BD.BF.E7.94.A8_rEFIND)
*   [4 更新 rEFInd](#.E6.9B.B4.E6.96.B0_rEFInd)
    *   [4.1 Systemd 自动化](#Systemd_.E8.87.AA.E5.8A.A8.E5.8C.96)
*   [5 Apple Macs](#Apple_Macs)
*   [6 VirtualBox](#VirtualBox)
*   [7 参见](#.E5.8F.82.E8.A7.81)

## 安装

从[官方软件源](/index.php/Official_repositories "Official repositories")安装 [refind-efi](https://www.archlinux.org/packages/?name=refind-efi)。然后运行

```
# refind-install

```

此操作会检测您的内核和 [ESP](/index.php/UEFI#EFI_System_Partition "UEFI") 分区，复制需要的文件，创建默认配置文件并将 rEFInd 设置为默认的 UEFI 启动项

## 手动安装

**Tip:** rEFInd 能够以多种方式启动 Linux。参见 [The rEFInd Boot Manager: Methods of Booting Linux](http://www.rodsbooks.com/refind/linux.html)。本节将阐述使用 [EFISTUB](/index.php/EFISTUB "EFISTUB") 的过程。

**Note:** 对于 32 位 EFI，请将 **x64** 替换为 **ia32**。

如果 `refind-install` 脚本没有正常工作，您可以手动设置 rEFInd。

1.  在 ESP 中创建一个目录来存放 rEFInd 的文件。此处假定您的 ESP 分区被挂载到 `/boot/efi` 并且您希望将 rEFInd 存放在 `/boot/efi/EFI/refind`。
2.  将可执行文件、配置文件和资源文件复制到 ESP

    ```
    # cp /usr/share/refind/refind_x64.efi /boot/efi/EFI/refind/refind_x64.efi
    # cp /usr/share/refind/refind.conf-sample /boot/efi/EFI/refind/refind.conf
    # cp -r /usr/share/refind/{icons,fonts,drivers_x64} /boot/efi/EFI/refind/

    ```

3.  编辑刚才复制的配置文件。该文件有详细的注释。默认情况下，rEFInd 会在您的驱动器中寻找 EFISTUB 内核，所以您可能不需要做任何更改就能启动。
4.  如果需要定制内核引导选项，复制示例配置文件到你的内核的目录。编辑该文件并为您的根分区输入正确的 `PARTUUID` 和 `rootfstype` （可以使用 `blkid` 和 `lsblk -f`）.

    ```
    # cp /usr/share/refind/refind_linux.conf-sample /boot/refind_linux.conf

    ```

    **Tip:** `refind_linux.conf` 的每一行都会被显示为一个子菜单项。按下 + 、 Insert 或 F2 来展开子菜单.

5.  使用 `efibootmgr` 创建一条 UEFI 启动项（更改 X 、Y 使其指向您的 ESP 分区）。 参见 `efibootmgr` 的 man 手册.

    ```
    # efibootmgr -c -d /dev/sdX -p Y -l /EFI/refind/refind_x64.efi -L "rEFInd"

    ```

**Tip:** 在 rEFInd 中按下 F10 将会保存屏幕截图到 ESP 分区的根目录

### 自定义菜单项

您可以使用 `refind.conf` 中的小节手动创建启动条目。 确保 `scanfor` 包括 `manual` 否则条目将不会出现。

 `refind.conf` 

```
menuentry "Arch Linux" {
        icon     /EFI/refind/icons/os_arch.icns
        volume   1:
        loader   /boot/vmlinuz-linux
        initrd   /boot/initramfs-linux.img
        options  "root=PARTUUID=3518bb68-d01e-45c9-b973-0b5d918aae96 rw rootfstype=ext4"
}

```

## 在已有的 Windows UEFI 安装中使用 rEFIND

**Note:** 在页面 [Windows and Arch Dual Boot (简体中文)](/index.php/Windows_and_Arch_Dual_Boot_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Windows and Arch Dual Boot (简体中文)") 中查看通常的注意事项。

rEFInd 兼容 UEFI Windows 安装时创建的 EFI 系统分区，因此没有必要创建或格式化另一个 FAT32 分区。只需挂载 Windows 的 ESP 并像往常一样安装 rEFInd。默认情况下，rEFInd 的自动检测功能应该识别任何现有的 Windows 引导程序。

## 更新 rEFInd

Pacman 只更新在 `/usr/share/refind` 中的文件，不会将新文件复制到 ESP。 如果 `refind-install` 成功安装了 rEFInd，则可以再次运行以更新文件。 新的配置文件会被复制为 `refind.conf-sample` ——就像 `.pacdiff` —— 你可以选择改变合并到你的配置文件。 否则，您可以重复上文的步骤，复制新的文件。

### Systemd 自动化

如果需要自动复制 rEFInd 文件和更新 NVRAM（如果需要），可以使用下面的脚本。

**Note:** 如果您想更改 rEFInd 的安装目录，在脚本中修改 $refind_dir。

 `/usr/lib/systemd/scripts/refind_name_patchv2` 

```
#!/usr/bin/env bash
## COPYRIGHT 2013 : MARK E. LEE (BLUERIDER) : mlee24@binghamton.edu; mark@markelee.com

## LOG
## 1/17/2013 : Version 2 of refind_name_patch is released
##           : Supports long subdirectory location for refind
##           : Updates nvram when needed
##           : 10% speed boost
## 7/15/2013 : Changed arch to match 32-bit (ia32) and 64-bit (x64) naming scheme
##           : Changed directory copying in update-efi-dir to copy tools and drivers directories explicitly
##           : Changed efibootmgr writing code to be more concise and added (-w) to write the entry as per dusktreader's excellent guide : https://docs.google.com/document/d/1pvgm3BprpXoadsQi38FxqMOCUZhcSqFhZ26FZBkmn9I/edit
##           : Function to check if NVRAM boot entry was already listed was fixed to use awk and an if then clause
##           : ref_bin_escape was modified from : ref_bin_escape=${ref_bin//\//\\\\} to remove extra backslashes (error does not show up when using cmdline)
## 7/29/2013 : Changed location of tools,drivers, and binary directory to match capricious upstream move to /usr/share/refind

function main () {  ## main insertion function
  declare -r refind_dir="/boot/efi/EFI/refind"; ## set the refind directory
  arch=$(uname -m | awk -F'_' '{if ($1 == "x86") {print "x"$2} else if ($1 == "i686") {print "ia32"}}') &&  ## get bit architecture
  update-efi-dir;  ## updates or creates the refind directory
  update-efi-nvram;  ## updates nvram if needed
}

function update-efi-dir () {  ## setup the refind directory
  if [ ! -d $refind_dir ]; then  ## check if refind directory exists
    echo "Couldn't find $refind_dir";
    mkdir $refind_dir &&  ## make the refind directory if needed
    echo "Made $refind_dir";
  fi;
  if [ "$arch" ]; then  ## check if anything was stored in $arch
    cp -r /usr/share/refind/{refind_$arch.efi,keys,images,icons,fonts,docs,{tools,drivers}_$arch} $refind_dir/  && ## update the bins and dirs
    echo "Updated binaries and directory files for refind at $refind_dir";
   else
    echo "Failed to detect an x86 architecture";
    exit;
  fi;
}

function update-efi-nvram () { ## update the nvram with efibootmgr
  declare -r ref_bin=${refind_dir/\/boot\/efi}/refind_$arch.efi;  ## get path of refind binary (without /boot/efi)
  declare -r ref_bin_escape=${ref_bin//\//\\};  ## insert escape characters into $ref_bin
  [ "$(efibootmgr -v | awk "/${ref_bin_escape//\\/\\\\}/")" ] && ( ## check if boot entry is in nvram \
    echo "Found boot entry, no need to update nvram";
    ) || ( ## if boot entry is not in nvram; add it
    declare -r esp=$(mount -l | awk '/ESP/ {print $1}') &&  ## get ESP partition
    efibootmgr -cgw -d ${esp:0:8} -p ${esp:8} -L "rEFInd" -l $ref_bin_escape && ## update nvram
    echo "
    Updated nvram with entry rEFInd to boot $ref_bin
    Did not copy configuration files, please move refind.conf to $refind_dir/";
    )
}
main;  ## run the main insertion function

```

 `/usr/lib/systemd/system/refind_update.path` 

```
[Unit]
Description=Update rEFInd bootloader files

[Path]
PathChanged=/usr/share/refind/refind_<arch>.efi
Unit=refind_update.service

[Install]
WantedBy=multi-user.target

```

 `/usr/lib/systemd/system/refind_update.service` 

```
[Unit]
Description=Update rEFInd directories, binaries, and nvram

[Service]
Type=oneshot
ExecStart=/usr/bin/bash /usr/lib/systemd/scripts/refind_name_patchv2
RemainAfterExit=no

```

运行以下命令以激活这个 systemd path 单元：

```
# systemctl enable refind_update.path

```

## Apple Macs

[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)") 上的 [mactel-boot](https://aur.archlinux.org/packages/mactel-boot/) 是 "bless" 工具的实验性替代品。如果它不能正常工作， 在 OS X 中使用 "bless" 来将 rEFInd 设置为默认启动项。假设您的 UEFISYS 分区挂载到 `/mnt/efi`。

```
$ sudo bless --setBoot --folder /mnt/efi/EFI/refind --file /mnt/efi/EFI/refind/refind_x64.efi

```

## VirtualBox

参见 [VirtualBox#Using Arch under Virtualbox EFI mode](/index.php/VirtualBox#Using_Arch_under_Virtualbox_EFI_mode "VirtualBox").

## 参见

*   [The rEFInd Boot Manager](http://www.rodsbooks.com/refind/) by Roderick W. Smith.