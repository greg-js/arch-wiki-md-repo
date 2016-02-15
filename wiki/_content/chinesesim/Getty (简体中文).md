通常从 `/etc/[inittab](/index.php/Inittab "Inittab")` 启动，允许用户从终端登录。

## Contents

*   [1 Agetty](#Agetty)
*   [2 Fgetty](#Fgetty)
*   [3 其他](#.E5.85.B6.E4.BB.96)
*   [4 参见](#.E5.8F.82.E8.A7.81)

## Agetty

[Agetty](/index.php/Agetty "Agetty") 是 [util-linux](https://www.archlinux.org/packages/?name=util-linux) 包的组成部分。

Agetty 在等待登录时更改 TTY 设置，这样换行就不会被翻译成 CR–LF。这可能会导致终端上显示的信息(例如由 [Init](/index.php/Init "Init") 启动的程序输出的信息) 产生"台阶效应"。

## Fgetty

[Fgetty](/index.php?title=Fgetty&action=edit&redlink=1 "Fgetty (page does not exist)"). 包：[fgetty](https://aur.archlinux.org/packages/fgetty/). 来自于 Mingetty，不会产生台阶效应。打过补丁的 [fgetty-pam](https://aur.archlinux.org/packages/fgetty-pam/) 现在是 PAM 支持(incl. SHA-2) 的依赖之一.

## 其他

*   **[Mingetty](/index.php?title=Mingetty&action=edit&redlink=1 "Mingetty (page does not exist)")** package: [mingetty](https://aur.archlinux.org/packages/mingetty/)
*   **[Qingy](/index.php/Qingy "Qingy")** package: [qingy](https://aur.archlinux.org/packages/qingy/)
*   **[Fbgetty](/index.php?title=Fbgetty&action=edit&redlink=1 "Fbgetty (page does not exist)")** package: [fbgetty](https://www.archlinux.org/packages/?name=fbgetty)
*   **[Ngetty](/index.php?title=Ngetty&action=edit&redlink=1 "Ngetty (page does not exist)")** AUR: [ngetty](https://aur.archlinux.org/packages/ngetty/)
*   **[Rungetty](/index.php?title=Rungetty&action=edit&redlink=1 "Rungetty (page does not exist)")** AUR: [rungetty](https://aur.archlinux.org/packages/rungetty/)
*   **[Mgetty](/index.php?title=Mgetty&action=edit&redlink=1 "Mgetty (page does not exist)")** AUR: [mgetty](https://aur.archlinux.org/packages/mgetty/)

## 参见

*   [Display manager (简体中文)](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")
*   [Disable Clearing of Boot Messages (简体中文)](/index.php?title=Disable_Clearing_of_Boot_Messages_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Disable Clearing of Boot Messages (简体中文) (page does not exist)")
*   [Automatic login to virtual console (简体中文)](/index.php?title=Automatic_login_to_virtual_console_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)&action=edit&redlink=1 "Automatic login to virtual console (简体中文) (page does not exist)")