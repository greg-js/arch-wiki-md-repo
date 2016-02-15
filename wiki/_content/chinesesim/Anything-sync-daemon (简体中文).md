**翻译状态：** 本文是英文页面 [Anything-sync-daemon](/index.php/Anything-sync-daemon "Anything-sync-daemon") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-06-28，点击[这里](https://wiki.archlinux.org/index.php?title=Anything-sync-daemon&diff=0&oldid=264000)可以查看翻译后英文页面的改动。

[Anything-sync-daemon](https://aur.archlinux.org/packages/Anything-sync-daemon/) (asd) 是一个小型的、用以将特定目录移至 tmpfs 并定期同步回硬盘（HDD/SSD）的伪守护进程。其原理为通过 symlinking 与 rsync 同步两处的文件。ASD 的一项主要目的为创造完全透明的用户体验。

## Contents

*   [1 Asd or Psd?](#Asd_or_Psd.3F)
*   [2 ASD 的优势](#ASD_.E7.9A.84.E4.BC.98.E5.8A.BF)
*   [3 安装与设置](#.E5.AE.89.E8.A3.85.E4.B8.8E.E8.AE.BE.E7.BD.AE)
    *   [3.1 编辑 /etc/asd.conf](#.E7.BC.96.E8.BE.91_.2Fetc.2Fasd.conf)
    *   [3.2 使用](#.E4.BD.BF.E7.94.A8)
        *   [3.2.1 Systemd](#Systemd)
    *   [3.3 Debug 模式](#Debug_.E6.A8.A1.E5.BC.8F)
    *   [3.4 （可选）自定义更新周期](#.EF.BC.88.E5.8F.AF.E9.80.89.EF.BC.89.E8.87.AA.E5.AE.9A.E4.B9.89.E6.9B.B4.E6.96.B0.E5.91.A8.E6.9C.9F)
*   [4 帮助](#.E5.B8.AE.E5.8A.A9)

## Asd or Psd?

**注意:** 如果你只想同步浏览器的 profile，我们建议不要使用 ASD，而是使用专门为此设计的、可以检查浏览器运行状况的 [PSD](/index.php/Profile-sync-daemon "Profile-sync-daemon")。ASD 并不会做这些检查，在某些情况下，浏览器 profile 的数据可能丢失。

## ASD 的优势

使用这一守护进程的优势在于两方面：

1.  降低硬盘负荷；
2.  速度

当目标目录被移至 tmpfs 之后，相应的读写操作也将从硬盘转移到内存，因而可以减少硬盘读写，同时提升运行速度与响应速度。内存的访问时间以纳秒计，而硬盘则是以毫秒计，这中间差了六个数量级，或者说，内存比硬盘快出一百万倍。

## 安装与设置

[Anything-sync-daemon](https://aur.archlinux.org/packages/Anything-sync-daemon/) 可以从 [AUR](/index.php/Arch_User_Repository "Arch User Repository") 下载。安装方法与其它包一样。

### 编辑 /etc/asd.conf

配置文件在随软件包安装的 `/etc/asd.conf`。要启动 ASD，至少需要指定需要同步的目标目录。

例如：

```
WHATTOSYNC=('/var/lib/monitorix' '/srv/http' '/foo/bar')

```

你可以修改你的发行版的 tmpfs 的位置。需要修改的话，取消 `VOLATILE` 行的注释。需要注意的是，对于 Arch Linux 来说，`/dev/shm` 的默认地址可以正常运行。运行诸如 Bleachbit 这样的程序时，请仔细阅读它的警告，因为它非常喜欢删除 /tmp 中储存的文件，这也是为什么 `/dev/shm` 更理想的原因。

你可以修改 tmpfs 中文件链接的权限。为了保护用户的隐私，默认权限是 `700`。

### 使用

除了 debug 以外，不要直接调用 `/usr/bin/anything-sync-daemon`。当守护进程启动时回自动进行第一次同步。如果你的系统中装有 [Cron](/index.php/Cron "Cron") 的话，它可以每隔一小时调用它同步、更新文件。最后，当停止 ASD 时，它会进行最后一次同步。

#### Systemd

请使用附带的守护进程文件管理 ASD（`/usr/lib/systemd/system/asd.service`）：

```
# systemctl [option] asd.service

```

可用的选项包括：

```
start  启动守护进程；创造 symlink 并且管理 tmpfs 中的目标目录。
stop  关闭进程；移除 symlink 并将 tmpfs 中的文件写回硬盘。
enable  启动时自动运行。
disable  禁止自动运行。

```

### Debug 模式

使用 debug 选项可以告诉用户，基于 `/etc/asd.conf` 的设定，ASD 会做哪些工作。可以像这样运行：

```
$ anything-sync-daemon debug

```

### （可选）自定义更新周期

**注意:** 这一步是可选的， **asd** 可以自己每小时更新。

如果使用者希望提高同步频率的话，可以执行如下命令，在 crontab 中添加一行配置，让 cron 调用 ASD 的 _sync_ 功能：

```
# crontab -e

```

例如希望每十分钟同步一次的话：

```
 */10 * * * *     /usr/bin/anything-sync-daemon resync &> /dev/null

```

## 帮助

请至 [讨论贴](https://bbs.archlinux.org/viewtopic.php?id=139141) 发表评论或提问。