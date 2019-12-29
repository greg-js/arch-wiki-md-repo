**翻译状态：** 本文是英文页面 [Password_Recovery](/index.php/Password_Recovery "Password Recovery") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-11-22，点击[这里](https://wiki.archlinux.org/index.php?title=Password_Recovery&diff=0&oldid=554070)可以查看翻译后英文页面的改动。

本指南介绍如何恢复遗忘的 root 密码。有好几种方法能完成此任务。

**Warning:** 攻击者都可以使用上述方法修改系统，要保证系统安全，请限制物理上的访问，或者使用全[磁盘加密](/index.php/Disk_encryption "Disk encryption")。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 使用LiveCD](#使用LiveCD)
    *   [1.1 Change Root](#Change_Root)
*   [2 使用GRUB调用Bash](#使用GRUB调用Bash)
*   [3 参阅](#参阅)

## 使用LiveCD

通过LiveCD可以使用好几种方法：chroot并且使用`passwd`命令或者擦除密码域条目。任何Linux的LiveCD都可以使用，只是chroot时它必须匹配已经安装的架构类型。这里仅介绍 chroot 方式，因为这个方法更不容易出错。

### Change Root

1.  启动LiveCD, [mount](/index.php/Mount "Mount") 根文件系统.
2.  然后通过下列命令重置密码：

```
`passwd --root 根文件系统挂载点 用户名` 

```

1.  卸载根文件系统。
2.  重启，记下你的密码。

## 使用GRUB调用Bash

1.  选择适当的启动条目并且按下 **e** 来编辑这一行。
2.  选择内核行再次按下 **e**来编辑。
3.  在这行末尾添加 `init=/bin/bash` 。
4.  按下 **Ctrl + X** 重启 (改动只是暂时的)。重启后你将看到bash提示符。
5.  你的根文件系统应该只读挂载，所以再次以read/write挂载它： `mount -n -o remount,rw /` 
6.  使用`passwd`创建一个新的管理员密码。
7.  通过 `reboot -f` 重启，不要再次忘记你的密码。

**Note:** 使用此法时有的键盘不能被初始系统正确加载，你可能不能在bash提示符后输入任何东西。如果出现这种情况，你不得不使用其他方法。

## 参阅

*   [this guide](http://www.howtoforge.com/how-to-reset-a-forgotten-root-password-with-knoppix-p2) for an example.