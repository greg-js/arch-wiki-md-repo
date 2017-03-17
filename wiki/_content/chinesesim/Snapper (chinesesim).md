**翻译状态：** 本文是英文页面 [Snapper](/index.php/Snapper "Snapper") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-03-15，点击[这里](https://wiki.archlinux.org/index.php?title=Snapper&diff=0&oldid=470749)可以查看翻译后英文页面的改动。

[Snapper](http://snapper.io) 是一个由 openSUSE 的 Arvin Schnell 开发的工具，用于管理 [Btrfs](/index.php/Btrfs "Btrfs") 子卷和 [LVM](/index.php/LVM "LVM") 精简配置(thin-provisioned)卷。它可以创建和比较快照，在快照间回滚，并支持自动按时间序列创建快照。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 建立一个新的配置](#.E5.BB.BA.E7.AB.8B.E4.B8.80.E4.B8.AA.E6.96.B0.E7.9A.84.E9.85.8D.E7.BD.AE)
*   [3 创建快照](#.E5.88.9B.E5.BB.BA.E5.BF.AB.E7.85.A7)
    *   [3.1 自动按时创建快照](#.E8.87.AA.E5.8A.A8.E6.8C.89.E6.97.B6.E5.88.9B.E5.BB.BA.E5.BF.AB.E7.85.A7)
        *   [3.1.1 启用/停用](#.E5.90.AF.E7.94.A8.2F.E5.81.9C.E7.94.A8)
        *   [3.1.2 设置快照限制](#.E8.AE.BE.E7.BD.AE.E5.BF.AB.E7.85.A7.E9.99.90.E5.88.B6)
        *   [3.1.3 更改创建和清理频率](#.E6.9B.B4.E6.94.B9.E5.88.9B.E5.BB.BA.E5.92.8C.E6.B8.85.E7.90.86.E9.A2.91.E7.8E.87)
    *   [3.2 手动创建快照](#.E6.89.8B.E5.8A.A8.E5.88.9B.E5.BB.BA.E5.BF.AB.E7.85.A7)
        *   [3.2.1 简单快照](#.E7.AE.80.E5.8D.95.E5.BF.AB.E7.85.A7)
        *   [3.2.2 Pre/post 快照](#Pre.2Fpost_.E5.BF.AB.E7.85.A7)
    *   [3.3 启动时快照](#.E5.90.AF.E5.8A.A8.E6.97.B6.E5.BF.AB.E7.85.A7)
*   [4 列出快照](#.E5.88.97.E5.87.BA.E5.BF.AB.E7.85.A7)
*   [5 列出配置](#.E5.88.97.E5.87.BA.E9.85.8D.E7.BD.AE)
*   [6 删除快照](#.E5.88.A0.E9.99.A4.E5.BF.AB.E7.85.A7)
*   [7 允许非 root 用户访问](#.E5.85.81.E8.AE.B8.E9.9D.9E_root_.E7.94.A8.E6.88.B7.E8.AE.BF.E9.97.AE)
*   [8 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [8.1 日志](#.E6.97.A5.E5.BF.97)
    *   [8.2 IO 错误](#IO_.E9.94.99.E8.AF.AF)
*   [9 相关资源](#.E7.9B.B8.E5.85.B3.E8.B5.84.E6.BA.90)

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") [snapper](https://www.archlinux.org/packages/?name=snapper) 包。或者安装开发版本 [snapper-git](https://aur.archlinux.org/packages/snapper-git/)。

此外，还可以安装 GUI 前端 [snapper-gui-git](https://aur.archlinux.org/packages/snapper-gui-git/)。

## 建立一个新的配置

在为 btrfs 子卷建立一个 snapper 配置前，这个子卷必须已经存在。否则，你应该在建立 snapper 配置前[创建](/index.php/Btrfs_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.88.9B.E5.BB.BA.E5.AD.90.E5.8D.B7 "Btrfs (简体中文)")它。

要为位置为 `*/path/to/subvolume*` 的 btrfs 子卷创建一个新的 snapper 配置文件，并命名为 `*config*`：

```
# snapper -c *config* create-config */path/to/subvolume*

```

这将会：

*   根据 `/etc/snapper/config-templates` 处的默认配置模板创建一个配置文件 `/etc/snapper/configs/*config*`。
*   在 `*/path/to/subvolume*/.snapshots` 处创建一个子卷，用于存储未来该配置文件产生的子卷。子卷的路经将会是 `*/path/to/subvolume*/.snapshots/*#*/snapshot`，`*#*` 是子卷序号。
*   将 `*config*` 加入到 `/etc/conf.d/snapper` 的 `SNAPPER_CONFIGS` 中。

例如，要为挂载在 `/` 的子卷创建一个配置文件：

```
# snapper -c root create-config /

```

此时，配置文件已经激活。如果你的 [cron](/index.php/Cron "Cron") 守护进程已经运行， snapper 将会使用 [#自动按时创建快照](#.E8.87.AA.E5.8A.A8.E6.8C.89.E6.97.B6.E5.88.9B.E5.BB.BA.E5.BF.AB.E7.85.A7)。否则，你需要使用 systemd 单元文件和定时器。参阅 [#启用/停用](#.E5.90.AF.E7.94.A8.2F.E5.81.9C.E7.94.A8)。

参阅 `snapper-configs` 的 [man page (简体中文)](/index.php/Man_page_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Man page (简体中文)")。

## 创建快照

### 自动按时创建快照

一个快照时间线(timeline)由可配置数目的每小时/日/月/年快照组成。当自动按时创建启用时，默认每小时创建一个快照。每天由时间线清理算法清理多余快照。

#### 启用/停用

如果你拥有一个 [cron](/index.php/Cron "Cron") 守护进程，该特性应该已经自动启用。要停用，编译你想禁用该特性的子卷对应配置文件为：

 `TIMELINE_CREATE="no"` 

如果你没有 [cron](/index.php/Cron "Cron") 守护进程，你可以使用提供的 systemd 单元文件。[Start](/index.php/Start "Start") 并 [enable](/index.php/Enable "Enable") `snapper-timeline.timer` 来启用自动按时创建快照。另外，[start](/index.php/Start "Start") 并 [enable](/index.php/Enable "Enable") `snapper-cleanup.timer` 来定期清理老旧快照。

#### 设置快照限制

默认配置将保留 10 个每小时快照，10 个每日快照，10 个每月快照和 10 个每年快照。你可以在配置文件中更改这些限制，特别是在繁忙的子卷，例如 `/` 上。参阅 [#Preventing slowdowns](#Preventing_slowdowns)。

这是一份名为 `*config*` 的配置文件的示例片段，它将保留 5 个每小时快照，7 个每日快照，不保留每月和每年快照：

 `/etc/snapper/configs/*config*` 
```
TIMELINE_MIN_AGE="1800"
TIMELINE_LIMIT_HOURLY="5"
TIMELINE_LIMIT_DAILY="7"
TIMELINE_LIMIT_WEEKLY="0"
TIMELINE_LIMIT_MONTHLY="0"
TIMELINE_LIMIT_YEARLY="0"
```

#### 更改创建和清理频率

如果你使用提供的 systemd 定时器，你可以 [修改](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BF.AE.E6.94.B9.E7.8E.B0.E5.AD.98.E5.8D.95.E5.85.83.E6.96.87.E4.BB.B6 "Systemd (简体中文)") 它们来更改创建和清理频率。

例如，编辑 `snapper-timeline.timer`，加入下列配置来设定快照频率为间隔五分钟，而不是一小时：

```
[Timer]
OnCalendar=*:0/5

```

**注意:** 配置项 `TIMELINE_LIMIT_HOURLY` 在上述示例中，其含义将会变为表示保留多少个每5分钟快照。

在编辑 `snapper-cleanup.timer` 来每小时运行清理，而不是每天的时候, 你需要更改 `OnUnitActiveSec`。 加入:

```
[Timer]
OnUnitActiveSec=1h

```

参阅 [Systemd (简体中文)/定时器](/index.php?title=Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/%E5%AE%9A%E6%97%B6%E5%99%A8&action=edit&redlink=1 "Systemd (简体中文)/定时器 (page does not exist)") 和 [Systemd#Drop-in_files](/index.php/Systemd#Drop-in_files "Systemd").

### 手动创建快照

#### 简单快照

默认情况下 snapper 创建 'simple *类型的快照，它们与其他快照没有特别关系。*

要为一个子卷创建快照：

```
 # snapper -c *config* create --description *desc*

```

以上命令没有对应的清理算法，因此该快照将会一直存储直到 [删除](#Delete_a_snapshot) 它。

要设置一个清理算法，在 `create` 后使用 `-c` 选项，并在 `number`，`timeline`，`pre` 或 `post` 中选择一个参数。 `number` 使 snapper 定期清理超出配置文件中设置的数量限制的快照。例如，要创建一个使用 `number` 清理算法的快照：

```
 # snapper -c *config* create -c number

```

参阅 [#自动按时创建快照](#.E8.87.AA.E5.8A.A8.E6.8C.89.E6.97.B6.E5.88.9B.E5.BB.BA.E5.BF.AB.E7.85.A7) 查看 `timeline` 是如何工作的。参阅 [#Pre/post 快照](#Pre.2Fpost_.E5.BF.AB.E7.85.A7) 查看 `pre` `post` 如何工作。

#### Pre/post 快照

除了 *simple* 快照以外，你还可以创建 *pre/post* 快照，*pre* 快照永远有一个对应的 *post* 快照。配对的目的是可以在系统更改前后创建快照。

要创建一个 *pre/post* 快照对，先创建一个 *pre* 快照：

```
 # snapper -c *config* create -t pre -p

```

记下输出的快照序号，它将会在创建 post 快照时使用。

然后执行一个系统更改（例如：安装一个新程序，更新系统，等等）

现在创建 *post* 快照：

```
 # snapper -c *config* create -t post --pre-number *N*

```

`*N*` 是对应的 *pre* 快照的序号。

An alternative method is to use the `--command` flag for `create`, which wraps a command with pre/post snapshots: 另一种方法是在 `create` 时使用 `--command` 选项，将会在 pre/post 快照间执行一个命令：

```
 # snapper -c *config* create --command *cmd*

```

`*cmd*` 是你希望在 pre/post 快照间执行的命令。

参阅 [Snapper#Wrapping pacman transactions in snapshots](/index.php/Snapper#Wrapping_pacman_transactions_in_snapshots "Snapper").

### 启动时快照

要让 snapper 为 `root` 配置文件创建一个快照，启用 `snapper-boot.timer`。

## 列出快照

要列出名为 *config* 的配置文件对应的快照:

```
 # snapper -c *config* list

```

## 列出配置

列出所有你已经创建的配置:

```
 # snapper list-configs

```

## 删除快照

要删除序号为 `*N*` 的快照:

```
 # snapper -c *config* delete *N*

```

可以一次删除多个快照。例如，要删除 root 配置文件的 65 和 70 号快照：

```
 # snapper -c root delete 65 70

```

**注意:** 删除 pre 快照时, 你应该总是删除对应的 post 快照。反之亦然。

## 允许非 root 用户访问

所有配置文件都是由 root 用户创建的，默认情况下，也只有 root 用户可以查看并访问它们。

要让指定用户可以列出某一配置文件的快照，修改 `/etc/snapper/configs/*config*` 中的 `ALLOW_USERS` 项。现在你应该可以以普通用户权限运行 `snapper -c *config*list`

最后，如果你想允许某一用户浏览 `.snapshots` 目录，但是该目录的拥有者必须为 root。因此，你应该修改包括该用户的组为组拥有者，以 `users` 为例：

```
# chmod a+rx .snapshots
# chown :users .snapshots

```

## 疑难解答

### 日志

Snapper 将所有活动写入到 `/var/log/snapper.log` 中 —— 在你认为出错时，首先检查该文件。

当你遇到关于每小时/每日/每周快照的问题时，最常见的原因是由于 cronie 服务（或者你使用的其他 cron 守护进程）没有运行。

### IO 错误

如果你在试图创建快照时遇到 'IO Error'，请确认你试图创建快照的子卷对应的 [.snapshots](https://bbs.archlinux.org/viewtopic.php?id=164404) 目录是一个子卷。

另一个可能的原因是 .snapshots 目录的拥有者不是 root。你会在在 `/var/log/snapper.log` 中找到 `Btrfs.cc(openInfosDir):219 - .snapshots must have owner root`。

## 相关资源

*   [Snapper homepage](http://snapper.io/)
*   [openSUSE Snapper portal](https://en.opensuse.org/Portal:Snapper)
*   [Btrfs homepage](https://btrfs.wiki.kernel.org/index.php/Main_Page)
*   [Linux.com: Snapper: SUSE's Ultimate Btrfs Snapshot Manager](https://www.linux.com/news/enterprise/systems-management/878490-snapper-suses-ultimate-btrfs-snapshot-manager/)