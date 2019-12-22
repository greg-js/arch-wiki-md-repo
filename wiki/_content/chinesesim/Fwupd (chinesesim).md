Related articles

*   [Secure Boot](/index.php/Secure_Boot "Secure Boot")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

**翻译状态：** 本文是英文页面 [Fwupd](/index.php/Fwupd "Fwupd") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-12-06，点击[这里](https://wiki.archlinux.org/index.php?title=Fwupd&diff=0&oldid=558138)可以查看翻译后英文页面的改动。

**fwupd** 是帮助你在 Linux 下更新固件的小工具，支持但不限于 UEFI/BIOS 固件。

支持的设备列表请查看 [这里](https://fwupd.org/lvfs/devicelist) 更多厂商支持计划请查看 [链接](https://fwupd.org/vendorlist)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 使用](#使用)
*   [3 更新 UEFI/BIOS 固件](#更新_UEFI/BIOS_固件)
    *   [3.1 安全启动](#安全启动)
        *   [3.1.1 用自己的密钥](#用自己的密钥)

## 安装

[安装](/index.php/Install "Install") [fwupd](https://www.archlinux.org/packages/?name=fwupd).

更新 UEFI/BIOS 固件请查看 [#更新 UEFI/BIOS 固件](#更新_UEFI/BIOS_固件)

## 使用

获得可用设备列表

```
$ fwupdmgr get-devices

```

**Note:** 列表中的部分设备可能不能使用该工具更新，*例如* Intel 核心显卡

刷新可用更新元数据

```
$ fwupdmgr refresh

```

检查哪些设备有可用更新

```
$ fwupdmgr get-updates

```

安装可用更新

```
$ fwupdmgr update

```

**Note:** 部分更新可能需要 sudo/root 权限

## 更新 UEFI/BIOS 固件

**Warning:** UEFI 固件更新可能会损坏你的引导器安装配置，所以更新完成后你可能需要重新安装你的引导器。如果你的系统只能在重启后安装 BIOS 更新，那么你需要准备一个包含 Arch 的 U 盘用于在更新完成后重新安装修复引导器。

1.  确保你使用 UEFI 模式启动系统；
2.  检查 [你的 EFI 变量可以获取](/index.php/Unified_Extensible_Firmware_Interface#Requirements_for_UEFI_variable_support "Unified Extensible Firmware Interface")；
3.  挂载你的 [EFI system partition](/index.php/EFI_system_partition "EFI system partition") (ESP) properly. `*esp*` 分区已经挂载。

### 安全启动

在 [Secure Boot](/index.php/Secure_Boot "Secure Boot") 开启的系统下，fwupd 使用 [shim](/index.php/Secure_Boot#shim "Secure Boot") 来引导 fwupd EFI 文件。 使用前请确保正确安装 shim

#### 用自己的密钥

**Note:** 下面的描述是基于fwupd未来版本的操作方式，参见 [[1]](https://github.com/hughsie/fwupd/issues/669).

或者,你需要手动签名uefi执行文件进行升级 ,此文件位于 `/usr/lib/fwupd/efi/fwupdx64.efi`. 签过名的uefi执行文件在 `/usr/lib/fwupd/efi/fwupdx64.efi.signed`. 使用 [sbsigntools](https://www.archlinux.org/packages/?name=sbsigntools), 运行:

```
# sbsign --key <keyfile> --cert <certfile> /usr/lib/fwupd/efi/fwupdx64.efi

```

可完成签名

为了使安装或者升级时自动签名，使用 [Pacman hook](/index.php/Pacman_hook "Pacman hook")：

 `/etc/pacman.d/hooks/sign-fwupd-secureboot.hook` 
```
[Trigger]
Operation = Install
Operation = Upgrade
Type = File
Target = usr/lib/fwupd/efi/fwupdx64.efi

[Action]
When = PostTransaction
Exec = /usr/bin/sbsign --key <keyfile> --cert <certfile> /usr/lib/fwupd/efi/fwupdx64.efi
Depends = sbsigntools
```

注意需要确保 `<keyfile>` 和 `<certfile>` 符合密钥的路径.

最后,你需要更改`/etc/fwupd/uefi.conf` 文件，将 `RequireShimForSecureBoot` 更改为 `RequireShimForSecureBoot=false`.