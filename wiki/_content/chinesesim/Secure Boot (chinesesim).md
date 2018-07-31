Related articles

*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

关于在 Linux 中 Secure Boot 的概述请参考文章 [Rodsbooks' Secure Boot](http://www.rodsbooks.com/efi-bootloaders/secureboot.html).

## 使用经过签名的boot loader

### Booting archiso

本节的重点在于如何在 Arch Linux 中设置安全启动。本节暂时仅介绍在开启 Secure Boot 模式的情况下启动 archiso 的步骤。因为 EFI 程序 `PreLoader.efi` 和 `HashTool.efi` 已经添加到 archiso 中，所以在开启 Secure Boot 模式的情况下启动 archiso 是可行的，将会显示一条 "Failed to Start loader...I will now execute HashTool". 的消息。要使用 HashTool 来注册 `loader.efi` 和 `vmlinuz.efi` 的 hash 值，执行如下步骤：

*   选择 `OK`
*   在 HashTool 主菜单先选择 `Enroll Hash`，再选择 `\loader.efi`，然后点击 `Yes` 确认。再选择 `Enroll Hash` 和 `archiso`，进入 archiso 目录，然后选择 `vmlinuz-efi` 并且点击 `Yes` 确认，最后点击 `Exit` 返回启动设备选择菜单。
*   在启动设备选择菜单选择 `Arch Linux archiso x86_64 UEFI CD`。

archiso 启动后会自动以 root 登陆，并且出现 shell 提示符。使用以下命令检查 archiso 是否以 Secure Boot 模式启动：

```
$ od -An -t u1 /sys/firmware/efi/efivars/SecureBoot-XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX

```

XXXX 部分因不同机器而各不相同。可以使用 tab 补全来获取帮助或者列出 EFI 变量。

如果以 Secure Boot 模式启动，命令会返回以 **1** 结尾的五个整数，例如：

```
6  0  0  0  1

```

此外，另一种方法是执行：

```
$ bootctl status

```