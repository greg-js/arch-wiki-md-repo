一共有三种办法，可以给内核传递参数，用于控制其行为方式：

1.  在编译内核时（这个最根本，会决定后面两种方法）
2.  内核启动时(通常是在一个启动管理器里设置).
3.  在运行时 (通过修改在 `/proc` 和 `/sys`中的文件).

本页面主要是讲第二种方法。

## Contents

*   [1 配置](#.E9.85.8D.E7.BD.AE)
    *   [1.1 Syslinux](#Syslinux)
    *   [1.2 GRUB](#GRUB)
    *   [1.3 GRUB Legacy](#GRUB_Legacy)
    *   [1.4 LILO](#LILO)
*   [2 常见参数列表](#.E5.B8.B8.E8.A7.81.E5.8F.82.E6.95.B0.E5.88.97.E8.A1.A8)
*   [3 更多信息](#.E6.9B.B4.E5.A4.9A.E4.BF.A1.E6.81.AF)

## 配置

内核参数可以在启动时临时修改，也可以永久性写到启动管理器的配置文件中，永远起作用。

下面示例：把参数`quiet` 和 `splash` 加到启动管理器 [Syslinux](/index.php/Syslinux "Syslinux"), [GRUB](/index.php/GRUB "GRUB"), [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") 和 [LILO](/index.php/LILO "LILO")中.

#### Syslinux

*   当出现启动选择菜单的时候，按 `Tab` 进入修改模式:

	 `> .linux ../vmlinuz-linux root=/dev/sda3 ro initrd=../initramfs-linux.img _quiet splash_` 

	Press `Enter` to boot with these parameters.

*   To make the change persistent after reboot, edit `/boot/syslinux/syslinux.cfg` and add them to the `APPEND` line:

	 `APPEND root=/dev/sda3 ro _quiet splash_` 

更多详情请见[Syslinux](/index.php/Syslinux "Syslinux") 。

#### GRUB

*   Press `e` when the menu shows up and add them on the `linux` line:

	 `linux   /boot/vmlinuz-linux root=UUID=978e3e81-8048-4ae1-8a06-aa727458e8ff ro  _quiet splash_` 

	Press `b` to boot with these parameters.

*   To make the change persistent after reboot, while you _could_ manually edit `/boot/grub/grub.cfg` with the exact line from above, for beginners it's recommended to:

	Edit `/etc/default/grub` and append your kernel options to the `GRUB_CMDLINE_LINUX_DEFAULT` line:

	 `GRUB_CMDLINE_LINUX_DEFAULT="_quiet splash_"` 

	And then automatically re-generate the `grub.cfg` file with:

	 `# grub-mkconfig -o /boot/grub/grub.cfg` 

For more information on configuring GRUB, see the [GRUB](/index.php/GRUB "GRUB") article.

#### GRUB Legacy

*   Press `e` when the menu shows up and add them on the `kernel` line:

	 `kernel /boot/vmlinuz-linux root=/dev/sda3 ro _quiet splash_` 

	Press `b` to boot with these parameters.

*   To make the change persistent after reboot, edit `/boot/grub/menu.lst` and add them to the `kernel` line, exactly like above.

For more information on configuring GRUB Legacy, see the [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") article.

#### LILO

*   Add them to `/etc/lilo.conf`:

```
image=/boot/vmlinuz-linux
        ...
        _quiet splash_
```

For more information on configuring LILO, see the [LILO](/index.php/LILO "LILO") article.

## 常见参数列表

**Note:** Not all of the listed options are always available. Most are associated with subsystems and work only if the kernel is configured with those subsystems built in. They also depend on the presence of the hardware they are associated with.

| [SysVinit](/index.php/SysVinit "SysVinit")（即将过时） | [systemd](/index.php/Systemd "Systemd") | 描述 |
| `3` | `systemd.unit=multi-user` | 不启动x（可进入后启动） |
| `1` | `systemd.unit=rescue` | 进入根用户模式(root). |
| `nomodeset` | `nomodeset` | 关闭内核显示模式设置功能. |
| `loglevel=3` | `loglevel=3` | Removes "misaligned reg" and "unknown connector type" messages during boot with the [Nouveau](/index.php/Nouveau "Nouveau") driver. See [this](https://bbs.archlinux.org/viewtopic.php?id=137509) topic. |
| -- | `init=/usr/lib/systemd/systemd` | 使用[systemd](/index.php/Systemd#Installation "Systemd") 替代 SysVinit 启动. |
| `init=/bin/sh rw` | `init=/bin/sh rw` | 进入超级终端模式，一般用于急救 |

All of these parameters are case-sensitive.

For a complete list of all known options, please see the [kernel documentation](https://www.kernel.org/doc/Documentation/kernel-parameters.txt).

## 更多信息

*   [sysctl](/index.php/Sysctl "Sysctl")
*   [List of kernel parameters with further explanation and grouped by similar options](http://files.kroah.com/lkn/lkn_pdf/ch09.pdf)