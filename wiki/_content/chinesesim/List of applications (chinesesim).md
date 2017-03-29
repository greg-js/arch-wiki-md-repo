**翻译状态：** 本文是英文页面 [List_of_applications](/index.php/List_of_applications "List of applications") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-02-20，点击[这里](https://wiki.archlinux.org/index.php?title=List_of_applications&diff=0&oldid=396023)可以查看翻译后英文页面的改动。

**[常用程序](/index.php/List_of_Applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications (简体中文)")**

* * *

[互联网](/index.php/List_of_Applications/Internet_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Internet (简体中文)") – [多媒体](/index.php/List_of_Applications/Multimedia_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Multimedia (简体中文)") – [工具](/index.php/List_of_Applications/Utilities_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Utilities (简体中文)") – [文档](/index.php/List_of_Applications/Documents_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Documents (简体中文)") – [安全](/index.php/List_of_Applications/Security_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Security (简体中文)") – [科学](/index.php/List_of_Applications/Science_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Science (简体中文)") – [其它](/index.php/List_of_Applications/Other_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "List of Applications/Other (简体中文)")

本文按照不同分类列出常用的应用程序，是寻找软件包的索引。许多段落分成终端和图形应用程序。

**Tip:**

*   本页面主要目的是为了在各种类别中更容易搜索。通过上面列表中的链接可以在各自的页面中查看子分类。
*   您可能想要[安装](/index.php/Pacman "Pacman")软件包 [pkgstats](https://www.archlinux.org/packages/?name=pkgstats), 此软件提供了一个 cron 任务，定期向 Arch Linux 开发者发送您的操作系统上安装的软件包以及您的系统架构和使用的镜像信息，以便开发者安排任务的优先级，让发行版变得更好。发送的信息都是匿名的，不会泄露您的个人信息。您可以在[统计信息页面](https://www.archlinux.de/?page=Statistics)查看收集到的信息。详见 [此论坛帖子](https://bbs.archlinux.org/viewtopic.php?id=105431)。
*   Daemon packages usually include the relevant systemd unit file to [start](/index.php/Start "Start"); some packages even include different ones. After installation `pacman -Qql *package* | grep -Fe .service -e .socket` can be used to check and find the relevant one.

**注意:** "Console" 中的应用程序可能会有图形前端，但其官方版本并不自带图形前端。

## Contents

*   [1 互联网](#.E4.BA.92.E8.81.94.E7.BD.91)
    *   [1.1 网络管理](#.E7.BD.91.E7.BB.9C.E7.AE.A1.E7.90.86)
    *   [1.2 网络浏览器](#.E7.BD.91.E7.BB.9C.E6.B5.8F.E8.A7.88.E5.99.A8)
        *   [1.2.1 终端](#.E7.BB.88.E7.AB.AF)
        *   [1.2.2 图形界面](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2)
            *   [1.2.2.1 基于 Gecko](#.E5.9F.BA.E4.BA.8E_Gecko)
                *   [1.2.2.1.1 Firefox forks](#Firefox_forks)
            *   [1.2.2.2 Blink-based](#Blink-based)
            *   [1.2.2.3 Webkit-based](#Webkit-based)
            *   [1.2.2.4 其它](#.E5.85.B6.E5.AE.83)
    *   [1.3 下载](#.E4.B8.8B.E8.BD.BD)
        *   [1.3.1 FTP](#FTP)
            *   [1.3.1.1 FTP 客户端](#FTP_.E5.AE.A2.E6.88.B7.E7.AB.AF)
            *   [1.3.1.2 FTP 服务器](#FTP_.E6.9C.8D.E5.8A.A1.E5.99.A8)
        *   [1.3.2 BitTorrent 客户端](#BitTorrent_.E5.AE.A2.E6.88.B7.E7.AB.AF)
            *   [1.3.2.1 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C)
                *   [1.3.2.1.1 命令行后端](#.E5.91.BD.E4.BB.A4.E8.A1.8C.E5.90.8E.E7.AB.AF)
                *   [1.3.2.1.2 纯命令行界面](#.E7.BA.AF.E5.91.BD.E4.BB.A4.E8.A1.8C.E7.95.8C.E9.9D.A2)
            *   [1.3.2.2 图形环境](#.E5.9B.BE.E5.BD.A2.E7.8E.AF.E5.A2.83)
                *   [1.3.2.2.1 libtorrent-rasterbar 后端](#libtorrent-rasterbar_.E5.90.8E.E7.AB.AF)
                *   [1.3.2.2.2 libktorrent 后端](#libktorrent_.E5.90.8E.E7.AB.AF)
                *   [1.3.2.2.3 其它](#.E5.85.B6.E5.AE.83_2)
        *   [1.3.3 电驴](#.E7.94.B5.E9.A9.B4)
        *   [1.3.4 Gnutella](#Gnutella)
    *   [1.4 通讯](#.E9.80.9A.E8.AE.AF)
        *   [1.4.1 邮件客户端](#.E9.82.AE.E4.BB.B6.E5.AE.A2.E6.88.B7.E7.AB.AF)
            *   [1.4.1.1 终端](#.E7.BB.88.E7.AB.AF_2)
            *   [1.4.1.2 图形界面](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2_2)
        *   [1.4.2 即时聊天](#.E5.8D.B3.E6.97.B6.E8.81.8A.E5.A4.A9)
            *   [1.4.2.1 多协议客户端](#.E5.A4.9A.E5.8D.8F.E8.AE.AE.E5.AE.A2.E6.88.B7.E7.AB.AF)
                *   [1.4.2.1.1 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C_2)
                *   [1.4.2.1.2 图形环境](#.E5.9B.BE.E5.BD.A2.E7.8E.AF.E5.A2.83_2)
        *   [1.4.3 IRC 客户端](#IRC_.E5.AE.A2.E6.88.B7.E7.AB.AF)
            *   [1.4.3.1 终端](#.E7.BB.88.E7.AB.AF_3)
            *   [1.4.3.2 图形界面](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2_3)
            *   [1.4.3.3 XMPP (Jabber)](#XMPP_.28Jabber.29)
                *   [1.4.3.3.1 命令行客户端](#.E5.91.BD.E4.BB.A4.E8.A1.8C.E5.AE.A2.E6.88.B7.E7.AB.AF)
                *   [1.4.3.3.2 图形界面客户端](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2.E5.AE.A2.E6.88.B7.E7.AB.AF)
                *   [1.4.3.3.3 服务器](#.E6.9C.8D.E5.8A.A1.E5.99.A8)
            *   [1.4.3.4 多协议客户端](#.E5.A4.9A.E5.8D.8F.E8.AE.AE.E5.AE.A2.E6.88.B7.E7.AB.AF_2)
                *   [1.4.3.4.1 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C_3)
                *   [1.4.3.4.2 图形界面](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2_4)
        *   [1.4.4 局域网聊天](#.E5.B1.80.E5.9F.9F.E7.BD.91.E8.81.8A.E5.A4.A9)
        *   [1.4.5 软件式电话](#.E8.BD.AF.E4.BB.B6.E5.BC.8F.E7.94.B5.E8.AF.9D)
            *   [1.4.5.1 客户端](#.E5.AE.A2.E6.88.B7.E7.AB.AF)
                *   [1.4.5.1.1 SIP](#SIP)
                *   [1.4.5.1.2 IAX2](#IAX2)
                *   [1.4.5.1.3 Skype](#Skype)
                *   [1.4.5.1.4 其它](#.E5.85.B6.E5.AE.83_3)
                *   [1.4.5.1.5 多协议](#.E5.A4.9A.E5.8D.8F.E8.AE.AE)
            *   [1.4.5.2 实用工具](#.E5.AE.9E.E7.94.A8.E5.B7.A5.E5.85.B7)
    *   [1.5 新闻，RSS 与博客](#.E6.96.B0.E9.97.BB.EF.BC.8CRSS_.E4.B8.8E.E5.8D.9A.E5.AE.A2)
        *   [1.5.1 新闻抓取](#.E6.96.B0.E9.97.BB.E6.8A.93.E5.8F.96)
            *   [1.5.1.1 终端](#.E7.BB.88.E7.AB.AF_4)
            *   [1.5.1.2 图形界面](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2_5)
        *   [1.5.2 播客客户端](#.E6.92.AD.E5.AE.A2.E5.AE.A2.E6.88.B7.E7.AB.AF)
        *   [1.5.3 Usenet 新闻播报与新闻抓取](#Usenet_.E6.96.B0.E9.97.BB.E6.92.AD.E6.8A.A5.E4.B8.8E.E6.96.B0.E9.97.BB.E6.8A.93.E5.8F.96)
        *   [1.5.4 博客软件](#.E5.8D.9A.E5.AE.A2.E8.BD.AF.E4.BB.B6)
        *   [1.5.5 微博客户端](#.E5.BE.AE.E5.8D.9A.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [1.6 网络剪贴板](#.E7.BD.91.E7.BB.9C.E5.89.AA.E8.B4.B4.E6.9D.BF)
    *   [1.7 比特币](#.E6.AF.94.E7.89.B9.E5.B8.81)
    *   [1.8 Surveying](#Surveying)
*   [2 多媒体](#.E5.A4.9A.E5.AA.92.E4.BD.93)
    *   [2.1 解码器](#.E8.A7.A3.E7.A0.81.E5.99.A8)
    *   [2.2 图像](#.E5.9B.BE.E5.83.8F)
        *   [2.2.1 图像查看](#.E5.9B.BE.E5.83.8F.E6.9F.A5.E7.9C.8B)
            *   [2.2.1.1 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C_4)
            *   [2.2.1.2 图形环境](#.E5.9B.BE.E5.BD.A2.E7.8E.AF.E5.A2.83_3)
        *   [2.2.2 图形和图像处理](#.E5.9B.BE.E5.BD.A2.E5.92.8C.E5.9B.BE.E5.83.8F.E5.A4.84.E7.90.86)
            *   [2.2.2.1 位图编辑器](#.E4.BD.8D.E5.9B.BE.E7.BC.96.E8.BE.91.E5.99.A8)
            *   [2.2.2.2 矢量图处理 - 绘画](#.E7.9F.A2.E9.87.8F.E5.9B.BE.E5.A4.84.E7.90.86_-_.E7.BB.98.E7.94.BB)
            *   [2.2.2.3 矢量图处理 - CAD](#.E7.9F.A2.E9.87.8F.E5.9B.BE.E5.A4.84.E7.90.86_-_CAD)
            *   [2.2.2.4 三维建模与渲染](#.E4.B8.89.E7.BB.B4.E5.BB.BA.E6.A8.A1.E4.B8.8E.E6.B8.B2.E6.9F.93)
        *   [2.2.3 截取屏幕](#.E6.88.AA.E5.8F.96.E5.B1.8F.E5.B9.95)
    *   [2.3 音频](#.E9.9F.B3.E9.A2.91)
        *   [2.3.1 音频系统](#.E9.9F.B3.E9.A2.91.E7.B3.BB.E7.BB.9F)
        *   [2.3.2 音频播放器](#.E9.9F.B3.E9.A2.91.E6.92.AD.E6.94.BE.E5.99.A8)
            *   [2.3.2.1 音乐播放器守护进程和客户端 (Client)](#.E9.9F.B3.E4.B9.90.E6.92.AD.E6.94.BE.E5.99.A8.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E5.92.8C.E5.AE.A2.E6.88.B7.E7.AB.AF_.28Client.29)
            *   [2.3.2.2 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C_5)
            *   [2.3.2.3 图形环境](#.E5.9B.BE.E5.BD.A2.E7.8E.AF.E5.A2.83_4)
        *   [2.3.3 音响管理](#.E9.9F.B3.E5.93.8D.E7.AE.A1.E7.90.86)
        *   [2.3.4 提取 CD](#.E6.8F.90.E5.8F.96_CD)
        *   [2.3.5 可视化](#.E5.8F.AF.E8.A7.86.E5.8C.96)
        *   [2.3.6 音频标签编辑器](#.E9.9F.B3.E9.A2.91.E6.A0.87.E7.AD.BE.E7.BC.96.E8.BE.91.E5.99.A8)
        *   [2.3.7 声音编辑](#.E5.A3.B0.E9.9F.B3.E7.BC.96.E8.BE.91)
    *   [2.4 手机管家](#.E6.89.8B.E6.9C.BA.E7.AE.A1.E5.AE.B6)
    *   [2.5 视频](#.E8.A7.86.E9.A2.91)
        *   [2.5.1 视频播放器](#.E8.A7.86.E9.A2.91.E6.92.AD.E6.94.BE.E5.99.A8)
            *   [2.5.1.1 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C_6)
            *   [2.5.1.2 图形化界面](#.E5.9B.BE.E5.BD.A2.E5.8C.96.E7.95.8C.E9.9D.A2)
        *   [2.5.2 DVD 提取](#DVD_.E6.8F.90.E5.8F.96)
        *   [2.5.3 视频编辑器](#.E8.A7.86.E9.A2.91.E7.BC.96.E8.BE.91.E5.99.A8)
            *   [2.5.3.1 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C_7)
            *   [2.5.3.2 图形界面](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2_6)
        *   [2.5.4 录屏](#.E5.BD.95.E5.B1.8F)
    *   [2.6 Optical media burning](#Optical_media_burning)
    *   [2.7 Podcasts](#Podcasts)
    *   [2.8 Collection managers](#Collection_managers)
    *   [2.9 Lyrics fetchers](#Lyrics_fetchers)
*   [3 工具](#.E5.B7.A5.E5.85.B7)
    *   [3.1 分区工具](#.E5.88.86.E5.8C.BA.E5.B7.A5.E5.85.B7)
    *   [3.2 挂载](#.E6.8C.82.E8.BD.BD)
        *   [3.2.1 Udisks](#Udisks)
    *   [3.3 基本 Shell 命令](#.E5.9F.BA.E6.9C.AC_Shell_.E5.91.BD.E4.BB.A4)
    *   [3.4 集成式开发环境](#.E9.9B.86.E6.88.90.E5.BC.8F.E5.BC.80.E5.8F.91.E7.8E.AF.E5.A2.83)
    *   [3.5 虚拟终端](#.E8.99.9A.E6.8B.9F.E7.BB.88.E7.AB.AF)
        *   [3.5.1 基于 VTE](#.E5.9F.BA.E4.BA.8E_VTE)
        *   [3.5.2 KMS-based](#KMS-based)
        *   [3.5.3 framebuffer-based](#framebuffer-based)
    *   [3.6 文件](#.E6.96.87.E4.BB.B6)
        *   [3.6.1 文件管理器](#.E6.96.87.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8)
            *   [3.6.1.1 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C_8)
            *   [3.6.1.2 图形环境](#.E5.9B.BE.E5.BD.A2.E7.8E.AF.E5.A2.83_5)
        *   [3.6.2 桌面搜索引擎](#.E6.A1.8C.E9.9D.A2.E6.90.9C.E7.B4.A2.E5.BC.95.E6.93.8E)
        *   [3.6.3 压缩与解压](#.E5.8E.8B.E7.BC.A9.E4.B8.8E.E8.A7.A3.E5.8E.8B)
            *   [3.6.3.1 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C_9)
            *   [3.6.3.2 图形环境](#.E5.9B.BE.E5.BD.A2.E7.8E.AF.E5.A2.83_6)
        *   [3.6.4 文件合并及比较](#.E6.96.87.E4.BB.B6.E5.90.88.E5.B9.B6.E5.8F.8A.E6.AF.94.E8.BE.83)
        *   [3.6.5 批量命名](#.E6.89.B9.E9.87.8F.E5.91.BD.E5.90.8D)
    *   [3.7 磁盘清理](#.E7.A3.81.E7.9B.98.E6.B8.85.E7.90.86)
    *   [3.8 磁盘使用情况分析](#.E7.A3.81.E7.9B.98.E4.BD.BF.E7.94.A8.E6.83.85.E5.86.B5.E5.88.86.E6.9E.90)
    *   [3.9 时钟同步](#.E6.97.B6.E9.92.9F.E5.90.8C.E6.AD.A5)
    *   [3.10 系统监视器](#.E7.B3.BB.E7.BB.9F.E7.9B.91.E8.A7.86.E5.99.A8)
    *   [3.11 系统信息检测](#.E7.B3.BB.E7.BB.9F.E4.BF.A1.E6.81.AF.E6.A3.80.E6.B5.8B)
        *   [3.11.1 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C_10)
        *   [3.11.2 图形环境](#.E5.9B.BE.E5.BD.A2.E7.8E.AF.E5.A2.83_7)
    *   [3.12 键盘布局切换](#.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80.E5.88.87.E6.8D.A2)
    *   [3.13 电源管理](#.E7.94.B5.E6.BA.90.E7.AE.A1.E7.90.86)
    *   [3.14 剪贴板管理](#.E5.89.AA.E8.B4.B4.E6.9D.BF.E7.AE.A1.E7.90.86)
    *   [3.15 壁纸设置](#.E5.A3.81.E7.BA.B8.E8.AE.BE.E7.BD.AE)
    *   [3.16 软件包管理](#.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.AE.A1.E7.90.86)
    *   [3.17 输入法](#.E8.BE.93.E5.85.A5.E6.B3.95)
    *   [3.18 Trash management](#Trash_management)
    *   [3.19 File synchronization](#File_synchronization)
    *   [3.20 Finders](#Finders)
*   [4 文档](#.E6.96.87.E6.A1.A3)
    *   [4.1 办公软件套装](#.E5.8A.9E.E5.85.AC.E8.BD.AF.E4.BB.B6.E5.A5.97.E8.A3.85)
    *   [4.2 字处理器](#.E5.AD.97.E5.A4.84.E7.90.86.E5.99.A8)
    *   [4.3 文档标记语言](#.E6.96.87.E6.A1.A3.E6.A0.87.E8.AE.B0.E8.AF.AD.E8.A8.80)
    *   [4.4 表格](#.E8.A1.A8.E6.A0.BC)
    *   [4.5 学术文档](#.E5.AD.A6.E6.9C.AF.E6.96.87.E6.A1.A3)
    *   [4.6 翻译与本土化](#.E7.BF.BB.E8.AF.91.E4.B8.8E.E6.9C.AC.E5.9C.9F.E5.8C.96)
    *   [4.7 文本编辑器](#.E6.96.87.E6.9C.AC.E7.BC.96.E8.BE.91.E5.99.A8)
        *   [4.7.1 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C_11)
            *   [4.7.1.1 Vi 类文本编辑器](#Vi_.E7.B1.BB.E6.96.87.E6.9C.AC.E7.BC.96.E8.BE.91.E5.99.A8)
        *   [4.7.2 图形环境](#.E5.9B.BE.E5.BD.A2.E7.8E.AF.E5.A2.83_8)
            *   [4.7.2.1 协同式文本编辑器](#.E5.8D.8F.E5.90.8C.E5.BC.8F.E6.96.87.E6.9C.AC.E7.BC.96.E8.BE.91.E5.99.A8)
    *   [4.8 阅读与浏览](#.E9.98.85.E8.AF.BB.E4.B8.8E.E6.B5.8F.E8.A7.88)
        *   [4.8.1 电子书阅读](#.E7.94.B5.E5.AD.90.E4.B9.A6.E9.98.85.E8.AF.BB)
            *   [4.8.1.1 书架](#.E4.B9.A6.E6.9E.B6)
        *   [4.8.2 PDF 和 DjVu](#PDF_.E5.92.8C_DjVu)
            *   [4.8.2.1 终端](#.E7.BB.88.E7.AB.AF_5)
            *   [4.8.2.2 图形化界面](#.E5.9B.BE.E5.BD.A2.E5.8C.96.E7.95.8C.E9.9D.A2_2)
        *   [4.8.3 虚拟分页器](#.E8.99.9A.E6.8B.9F.E5.88.86.E9.A1.B5.E5.99.A8)
        *   [4.8.4 CHM](#CHM)
        *   [4.8.5 漫画](#.E6.BC.AB.E7.94.BB)
    *   [4.9 扫描](#.E6.89.AB.E6.8F.8F)
    *   [4.10 OCR](#OCR)
        *   [4.10.1 引擎](#.E5.BC.95.E6.93.8E)
        *   [4.10.2 布局分析与用户界面](#.E5.B8.83.E5.B1.80.E5.88.86.E6.9E.90.E4.B8.8E.E7.94.A8.E6.88.B7.E7.95.8C.E9.9D.A2)
    *   [4.11 笔记](#.E7.AC.94.E8.AE.B0)
        *   [4.11.1 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C_12)
        *   [4.11.2 图形环境](#.E5.9B.BE.E5.BD.A2.E7.8E.AF.E5.A2.83_9)
    *   [4.12 Mind-mapping tools](#Mind-mapping_tools)
    *   [4.13 字符选择器](#.E5.AD.97.E7.AC.A6.E9.80.89.E6.8B.A9.E5.99.A8)
    *   [4.14 Stylus notes taking](#Stylus_notes_taking)
    *   [4.15 参考书目管理](#.E5.8F.82.E8.80.83.E4.B9.A6.E7.9B.AE.E7.AE.A1.E7.90.86)
*   [5 安全](#.E5.AE.89.E5.85.A8)
    *   [5.1 防火墙](#.E9.98.B2.E7.81.AB.E5.A2.99)
    *   [5.2 网络安全](#.E7.BD.91.E7.BB.9C.E5.AE.89.E5.85.A8)
    *   [5.3 威胁与漏洞探测](#.E5.A8.81.E8.83.81.E4.B8.8E.E6.BC.8F.E6.B4.9E.E6.8E.A2.E6.B5.8B)
    *   [5.4 文件安全](#.E6.96.87.E4.BB.B6.E5.AE.89.E5.85.A8)
        *   [5.4.1 反恶意软件](#.E5.8F.8D.E6.81.B6.E6.84.8F.E8.BD.AF.E4.BB.B6)
    *   [5.5 备份](#.E5.A4.87.E4.BB.BD)
    *   [5.6 锁屏](#.E9.94.81.E5.B1.8F)
    *   [5.7 Hash 校验](#Hash_.E6.A0.A1.E9.AA.8C)
    *   [5.8 加密，签名与信息隐藏](#.E5.8A.A0.E5.AF.86.EF.BC.8C.E7.AD.BE.E5.90.8D.E4.B8.8E.E4.BF.A1.E6.81.AF.E9.9A.90.E8.97.8F)
    *   [5.9 密码管理](#.E5.AF.86.E7.A0.81.E7.AE.A1.E7.90.86)
*   [6 科学](#.E7.A7.91.E5.AD.A6)
    *   [6.1 学术文档](#.E5.AD.A6.E6.9C.AF.E6.96.87.E6.A1.A3_2)
    *   [6.2 数学](#.E6.95.B0.E5.AD.A6)
        *   [6.2.1 计算器](#.E8.AE.A1.E7.AE.97.E5.99.A8)
        *   [6.2.2 计算机代数系统](#.E8.AE.A1.E7.AE.97.E6.9C.BA.E4.BB.A3.E6.95.B0.E7.B3.BB.E7.BB.9F)
        *   [6.2.3 科学与工程计算](#.E7.A7.91.E5.AD.A6.E4.B8.8E.E5.B7.A5.E7.A8.8B.E8.AE.A1.E7.AE.97)
        *   [6.2.4 统计](#.E7.BB.9F.E8.AE.A1)
        *   [6.2.5 数据评估](#.E6.95.B0.E6.8D.AE.E8.AF.84.E4.BC.B0)
    *   [6.3 化学与生物学](#.E5.8C.96.E5.AD.A6.E4.B8.8E.E7.94.9F.E7.89.A9.E5.AD.A6)
        *   [6.3.1 计算生物学和生物信息学](#.E8.AE.A1.E7.AE.97.E7.94.9F.E7.89.A9.E5.AD.A6.E5.92.8C.E7.94.9F.E7.89.A9.E4.BF.A1.E6.81.AF.E5.AD.A6)
        *   [6.3.2 分子学](#.E5.88.86.E5.AD.90.E5.AD.A6)
            *   [6.3.2.1 查看器](#.E6.9F.A5.E7.9C.8B.E5.99.A8)
            *   [6.3.2.2 Drawing](#Drawing)
            *   [6.3.2.3 Modeling](#Modeling)
        *   [6.3.3 Periodic table](#Periodic_table)
        *   [6.3.4 Biochemistry](#Biochemistry)
        *   [6.3.5 Image manipulation](#Image_manipulation)
    *   [6.4 天文学](#.E5.A4.A9.E6.96.87.E5.AD.A6)
    *   [6.5 物理学](#.E7.89.A9.E7.90.86.E5.AD.A6)
        *   [6.5.1 电子学](#.E7.94.B5.E5.AD.90.E5.AD.A6)
        *   [6.5.2 物理系统模拟器](#.E7.89.A9.E7.90.86.E7.B3.BB.E7.BB.9F.E6.A8.A1.E6.8B.9F.E5.99.A8)
        *   [6.5.3 单位转换](#.E5.8D.95.E4.BD.8D.E8.BD.AC.E6.8D.A2)
*   [7 其它](#.E5.85.B6.E5.AE.83_4)
    *   [7.1 工作环境](#.E5.B7.A5.E4.BD.9C.E7.8E.AF.E5.A2.83)
        *   [7.1.1 开机动画](#.E5.BC.80.E6.9C.BA.E5.8A.A8.E7.94.BB)
        *   [7.1.2 命令行](#.E5.91.BD.E4.BB.A4.E8.A1.8C_13)
        *   [7.1.3 Terminal multiplexers](#Terminal_multiplexers)
        *   [7.1.4 Desktop environments](#Desktop_environments)
        *   [7.1.5 Window managers](#Window_managers)
            *   [7.1.5.1 Console](#Console)
            *   [7.1.5.2 Graphical](#Graphical)
        *   [7.1.6 Window tilers](#Window_tilers)
        *   [7.1.7 Virtual desktop pagers](#Virtual_desktop_pagers)
        *   [7.1.8 Support applications](#Support_applications)
            *   [7.1.8.1 Login managers](#Login_managers)
            *   [7.1.8.2 Composite managers](#Composite_managers)
            *   [7.1.8.3 Taskbars / panels / docks](#Taskbars_.2F_panels_.2F_docks)
            *   [7.1.8.4 Application launchers](#Application_launchers)
            *   [7.1.8.5 Logout dialogue](#Logout_dialogue)
        *   [7.1.9 Accessibility](#Accessibility)
            *   [7.1.9.1 Screen reading](#Screen_reading)
            *   [7.1.9.2 Speech recognition](#Speech_recognition)
    *   [7.2 Finance](#Finance)
    *   [7.3 Flashcards](#Flashcards)
    *   [7.4 Time management](#Time_management)
        *   [7.4.1 Console](#Console_2)
        *   [7.4.2 Graphical](#Graphical_2)
    *   [7.5 Emulators](#Emulators)
        *   [7.5.1 Consoles](#Consoles)
        *   [7.5.2 Other](#Other)
    *   [7.6 Amateur radio](#Amateur_radio)
*   [8 参见](#.E5.8F.82.E8.A7.81)

## 互联网

**Note:** For possibly more up to date selection of applications, try checking the [AUR 'network' category](https://aur.archlinux.org/packages.php?O=0&K=&do_Search=Go&detail=1&C=13&SeB=nd&SB=n&SO=a&PP=50)

### 网络管理

### 网络浏览器

See also [Wikipedia:Comparison of web browsers](https://en.wikipedia.org/wiki/Comparison_of_web_browsers "wikipedia:Comparison of web browsers").

#### 终端

*   **[ELinks](https://en.wikipedia.org/wiki/ELinks "wikipedia:ELinks")** — Advanced and well-established feature-rich text mode web browser (Links fork, barely supported since 2009).

	[http://elinks.or.cz/](http://elinks.or.cz/) || [elinks](https://www.archlinux.org/packages/?name=elinks)

*   **[Links](https://en.wikipedia.org/wiki/Links_(web_browser) "wikipedia:Links (web browser)")** — Text WWW browser. Includes a console version [links] similar to Lynx, and a graphical X-window/framebuffer version [links -g] (must be compiled in, Arch has both) with CSS, image rendering, pull-down menus.

	[http://links.twibright.com/](http://links.twibright.com/) || [links](https://www.archlinux.org/packages/?name=links)

*   **[Lynx](https://en.wikipedia.org/wiki/Lynx_(web_browser) "wikipedia:Lynx (web browser)")** — Text browser for the World Wide Web.

	[http://lynx.isc.org](http://lynx.isc.org) || [lynx](https://www.archlinux.org/packages/?name=lynx)

*   **retawq** — Interactive, multi-threaded network client (web browser) for text terminals.

	[http://retawq.sourceforge.net/](http://retawq.sourceforge.net/) || [retawq](https://aur.archlinux.org/packages/retawq/)

*   **[w3m](https://en.wikipedia.org/wiki/W3m "wikipedia:W3m")** — Pager/text-based web browser. It has vim-like keybindings, and is able to display images. It has javascript support too.

	[http://w3m.sourceforge.net/](http://w3m.sourceforge.net/) || [w3m](https://www.archlinux.org/packages/?name=w3m)

#### 图形界面

##### 基于 Gecko

可见 [Wikipedia:Gecko (software)](https://en.wikipedia.org/wiki/Gecko_(software) "wikipedia:Gecko (software)").

*   **[Firefox](/index.php/Firefox "Firefox")** — Extensible browser from Mozilla based on Gecko with fast rendering.

	[https://mozilla.com/firefox](https://mozilla.com/firefox) || [firefox](https://www.archlinux.org/packages/?name=firefox)

*   **Seamonkey** — Continuation of the Mozilla Internet Suite.

	[http://www.seamonkey-project.org/](http://www.seamonkey-project.org/) || [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)

*   **[Conkeror](https://en.wikipedia.org/wiki/Conkeror "wikipedia:Conkeror")** — Keyboard-based browser modeled after [Emacs](/index.php/Emacs "Emacs") using [XULRunner](https://en.wikipedia.org/wiki/XULRunner "wikipedia:XULRunner"). Customizable via JavaScript.

	[http://repo.or.cz/w/conkeror.git/](http://repo.or.cz/w/conkeror.git/) || [conkeror-git](https://aur.archlinux.org/packages/conkeror-git/)

###### Firefox forks

**警告:** 以下浏览器是火狐的第三方版本，请直接向它们各自的创建者寻求支持。

*   **[Iceweasel](https://en.wikipedia.org/wiki/Mozilla_Corporation_software_rebranded_by_the_Debian_project#IceWeasel "wikipedia:Mozilla Corporation software rebranded by the Debian project")** — Fork of Firefox developed by Debian Linux. The main difference is that it does not include any trademarked Mozilla artwork. See [[1]](http://web.glandium.org/blog/?p=97) for more information on Iceweasel's existence.

	[https://wiki.debian.org/Iceweasel](https://wiki.debian.org/Iceweasel) || [iceweasel](https://aur.archlinux.org/packages/iceweasel/)

*   **[GNU IceCat](https://en.wikipedia.org/wiki/GNU_IceCat "wikipedia:GNU IceCat")** — 通过 GNU Project 分发的 Web 浏览器, 去掉了非自由的组件，并且附加上了隐私扩展。发行周期与 Mozilla Firefox 相比可能会推迟。

	[https://www.gnu.org/software/gnuzilla/](https://www.gnu.org/software/gnuzilla/) || [icecat](https://aur.archlinux.org/packages/icecat/)

*   **[Pale Moon](https://en.wikipedia.org/wiki/Pale_Moon_(web_browser) "wikipedia:Pale Moon (web browser)")** — 基于 Firefox 的分支, using a Firefox 3+ interface through selective use of add-ons. Firefox 扩展可能不兼容. [[2]](https://addons.palemoon.org/firefox/incompatible/) Compiled for SSE2, with disabled optional code and no support for newer Firefox features such as cache2, e10s, and OTMC.

	[http://www.palemoon.org/](http://www.palemoon.org/) || [palemoon-bin](https://aur.archlinux.org/packages/palemoon-bin/)

##### Blink-based

See also [Wikipedia:Blink (layout engine)](https://en.wikipedia.org/wiki/Blink_(layout_engine) "wikipedia:Blink (layout engine)").

*   **[Chromium](/index.php/Chromium "Chromium")** — Web browser developed by Google, the open source project behind Google Chrome.

	[http://www.chromium.org/](http://www.chromium.org/) || [chromium](https://www.archlinux.org/packages/?name=chromium)

*   **[Opera](/index.php/Opera "Opera")** — Highly customizable browser with focuses on an adherence to web rendering standards.

	[http://opera.com](http://opera.com) || [opera](https://www.archlinux.org/packages/?name=opera)

##### Webkit-based

参考 [Wikipedia:Webkit](https://en.wikipedia.org/wiki/Webkit "wikipedia:Webkit").

*   **[Arora](https://en.wikipedia.org/wiki/Arora_(browser) "wikipedia:Arora (browser)")** — 使用 QtWebKit 建立的跨平台 Web 浏览器. 2012年1月停止开发。

	[https://code.google.com/p/arora/](https://code.google.com/p/arora/) || [arora](https://aur.archlinux.org/packages/arora/)

*   **[dwb](/index.php/Dwb "Dwb")** — Lightweight, highly customizable web browser based on the WebKit engine with *vi*-like shortcuts and tiling layouts. As of October 2014 *dwb* is [unmaintained](https://bitbucket.org/portix/dwb/pull-request/22/several-cleanups-to-increase-portability/diff#comment-3217936).

	[http://portix.bitbucket.org/dwb/](http://portix.bitbucket.org/dwb/) || [dwb](https://aur.archlinux.org/packages/dwb/)

*   **[GNOME Web](/index.php/GNOME_Web "GNOME Web")** — Browser which uses the WebKitGTK+ rendering engine, part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

	[https://wiki.gnome.org/Apps/Web/](https://wiki.gnome.org/Apps/Web/) || [epiphany](https://www.archlinux.org/packages/?name=epiphany)

*   **[Jumanji](/index.php/Jumanji "Jumanji")** — 高度定制且功能强大的Web浏览器。

	[http://pwmt.org/projects/jumanji](http://pwmt.org/projects/jumanji) || [jumanji](https://aur.archlinux.org/packages/jumanji/)

*   **[Luakit](/index.php/Luakit "Luakit")** — Highly configurable, micro-browser framework based on the WebKit engine and the GTK+ toolkit. It is very fast, extensible by Lua and licensed under the GNU GPLv3 license.

	[http://mason-larobina.github.com/luakit/](http://mason-larobina.github.com/luakit/) || [luakit](https://aur.archlinux.org/packages/luakit/)

*   **Maxthon** — A browser that combines a minimal design with sophisticated technology to make the web faster, safer, and easier.

	[http://www.maxthon.cn/](http://www.maxthon.cn/) || [maxthon-browser](https://aur.archlinux.org/packages/maxthon-browser/)

*   **[Midori](https://en.wikipedia.org/wiki/Midori_(web_browser) "wikipedia:Midori (web browser)")** — Lightweight web browser based on GTK+ and WebKit.

	[http://midori-browser.org/](http://midori-browser.org/) || [midori](https://www.archlinux.org/packages/?name=midori)

*   **Otter-browser** — Browser aiming to recreate classic Opera (12.x) UI using Qt5.

	[http://otter-browser.org/](http://otter-browser.org/) || [otter-browser](https://aur.archlinux.org/packages/otter-browser/)

*   **[QupZilla](https://en.wikipedia.org/wiki/QupZilla "wikipedia:QupZilla")** — New and very fast open source browser based on WebKit core, written in Qt framework.

	[http://www.qupzilla.com](http://www.qupzilla.com) || [qupzilla](https://www.archlinux.org/packages/?name=qupzilla)

*   **[qutebrowser](/index.php/Qutebrowser "Qutebrowser")** — A keyboard-driven, vim-like browser based on PyQt5 and QtWebKit.

	[https://github.com/The-Compiler/qutebrowser](https://github.com/The-Compiler/qutebrowser) || [qutebrowser](https://www.archlinux.org/packages/?name=qutebrowser)

*   **[Rekonq](https://en.wikipedia.org/wiki/Rekonq "wikipedia:Rekonq")** — WebKit-based web browser for KDE.

	[http://rekonq.kde.org/](http://rekonq.kde.org/) || [rekonq](https://aur.archlinux.org/packages/rekonq/)

*   **Sb** — Very lightweight WebKit-based browser that uses keybindings to perform most things the URL bar would usually do.

	[https://github.com/mutantturkey/sb/](https://github.com/mutantturkey/sb/) || [sb-git](https://aur.archlinux.org/packages/sb-git/)

*   **SlimBoat** — Fast, free secure and powerful web browser based on QtWebkit.

	[http://www.slimboat.com/](http://www.slimboat.com/) || [slimboat](https://aur.archlinux.org/packages/slimboat/)

*   **Surf** — Lightweight WebKit-based browser, which follows the [suckless ideology](http://suckless.org/philosophy) (basically, the browser itself is a single C source file).

	[http://surf.suckless.org](http://surf.suckless.org) || [surf](https://www.archlinux.org/packages/?name=surf)

*   **[Uzbl](https://en.wikipedia.org/wiki/Uzbl "wikipedia:Uzbl")** — Group of web interface tools which adhere to the Unix philosophy.

	[http://uzbl.org/](http://uzbl.org/) || [uzbl-browser](https://www.archlinux.org/packages/?name=uzbl-browser)

*   **vimb** — Fast and lightweight vim like web browser based on the webkit web browser engine and the GTK toolkit.

	[https://fanglingsu.github.io/vimb/](https://fanglingsu.github.io/vimb/) || [vimb](https://aur.archlinux.org/packages/vimb/)

*   **[Vimprobable](/index.php/Vimprobable "Vimprobable")** — Browser that behaves like the Vimperator plugin available for Mozilla Firefox. It is based on the WebKit engine and uses the GTK+ bindings.

	[http://sourceforge.net/apps/trac/vimprobable/](http://sourceforge.net/apps/trac/vimprobable/) || [vimprobable-git](https://aur.archlinux.org/packages/vimprobable-git/)

*   **[Xombrero](https://en.wikipedia.org/wiki/Xombrero "wikipedia:Xombrero") (formerly known as *xxxterm*)** — Webkit minimalist web browser with sophisticated security features designed-in, BSD style.

	[https://opensource.conformal.com/wiki/xombrero](https://opensource.conformal.com/wiki/xombrero) || [xombrero-git](https://aur.archlinux.org/packages/xombrero-git/)

##### 其它

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — 基于 Qt 和 KHTML 的web浏览器, [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/)的一部分.

	[http://konqueror.org/](http://konqueror.org/) || [kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror)

*   **[Abaco](https://en.wikipedia.org/wiki/Abaco_(web_browser) "wikipedia:Abaco (web browser)")** — Multi-page graphical web browser for the Plan 9 OS.

	[http://lab-fgb.com/abaco/](http://lab-fgb.com/abaco/) || [abaco](https://aur.archlinux.org/packages/abaco/)

*   **[Conkeror](https://en.wikipedia.org/wiki/Conkeror "wikipedia:Conkeror")** — Highly programmable web browser, with Emacs-like keybindings, based on Mozilla's XULRunner.

	[http://conkeror.org/](http://conkeror.org/) || [conkeror-git](https://aur.archlinux.org/packages/conkeror-git/)

*   **[Dillo](https://en.wikipedia.org/wiki/Dillo "wikipedia:Dillo")** — Small, fast graphical web browser built on [FLTK](https://en.wikipedia.org/wiki/Fltk "wikipedia:Fltk").

	[http://dillo.org/](http://dillo.org/) || [dillo](https://www.archlinux.org/packages/?name=dillo)

*   **[NetSurf](https://en.wikipedia.org/wiki/NetSurf "wikipedia:NetSurf")** — 用 C 语言写的次轻量级浏览器, 注意它对 JavaScript 欠缺支持，和使用它自己的渲染引擎快速的渲染。

	[http://netsurf-browser.org](http://netsurf-browser.org) || [netsurf](https://www.archlinux.org/packages/?name=netsurf)

### 下载

#### FTP

##### FTP 客户端

See also [Wikipedia:Comparison of FTP client software](https://en.wikipedia.org/wiki/Comparison_of_FTP_client_software "wikipedia:Comparison of FTP client software").

*   **[CurlFtpFS](/index.php/CurlFtpFS "CurlFtpFS")** — Filesystem for accessing FTP hosts; based on FUSE and libcurl.

	[http://curlftpfs.sourceforge.net/](http://curlftpfs.sourceforge.net/) || [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs)

*   **FatRat** — Download manager with support for HTTP, FTP, SFTP, BitTorrent, RapidShare and more.

	[http://fatrat.dolezel.info/](http://fatrat.dolezel.info/) || [fatrat-git](https://aur.archlinux.org/packages/fatrat-git/)

*   **[FileZilla](https://en.wikipedia.org/wiki/FileZilla "wikipedia:FileZilla")** — 快速可靠的 FTP, FTPS and SFTP 客户端.

	[http://filezilla-project.org/](http://filezilla-project.org/) || [filezilla](https://www.archlinux.org/packages/?name=filezilla)

*   **[fuseftp](/index.php/FtpFs#Fuseftp "FtpFs")** — FTP filesystem written in Perl, using [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace").

	[http://freshmeat.net/projects/fuseftp/](http://freshmeat.net/projects/fuseftp/) || [fuseftp](https://aur.archlinux.org/packages/fuseftp/)

*   **[gFTP](https://en.wikipedia.org/wiki/gFTP "wikipedia:gFTP")** — Multithreaded FTP client for Linux.

	[http://gftp.seul.org/](http://gftp.seul.org/) || [gftp](https://www.archlinux.org/packages/?name=gftp)

*   **[LFTP](https://en.wikipedia.org/wiki/Lftp "wikipedia:Lftp")** — Sophisticated command-line FTP client.

	[http://lftp.yar.ru/](http://lftp.yar.ru/) || [lftp](https://www.archlinux.org/packages/?name=lftp)

*   **LftpFS** — Read-only filesystem based on lftp (also supports HTTP, FISH, SFTP, HTTPS, FTPS and proxies).

	[http://lftpfs.sourceforge.net/](http://lftpfs.sourceforge.net/) || [lftpfs](https://aur.archlinux.org/packages/lftpfs/)

*   **[tnftp](https://en.wikipedia.org/wiki/tnftp "wikipedia:tnftp")** — FTP client with several advanced features for [NetBSD](https://en.wikipedia.org/wiki/NetBSD "wikipedia:NetBSD").

	[http://freecode.com/projects/tnftp](http://freecode.com/projects/tnftp) || [tnftp](https://www.archlinux.org/packages/?name=tnftp)

一些像 Dolphin, [GNOME Files](/index.php/GNOME_Files "GNOME Files") 和 [Thunar](/index.php/Thunar "Thunar") 这样的文件管理器也提供FTP功能.

##### FTP 服务器

*   **bftpd** — 小巧, 易配置的 FTP 服务器

	[http://bftpd.sourceforge.net/](http://bftpd.sourceforge.net/) || [bftpd](https://www.archlinux.org/packages/?name=bftpd)

*   **[proFTPd](/index.php/Proftpd "Proftpd")** — 一个安全的可配置的 FTP 服务器

	[http://www.proftpd.org/](http://www.proftpd.org/) || [proftpd](https://aur.archlinux.org/packages/proftpd/)

*   **[Pure-FTPd](/index.php/Pure-FTPd "Pure-FTPd")** — Free (BSD-licensed), secure, production-quality and standard-compliant FTP server.

	[http://www.pureftpd.org/project/pure-ftpd](http://www.pureftpd.org/project/pure-ftpd) || [pure-ftpd](https://aur.archlinux.org/packages/pure-ftpd/)

*   **[vsftpd](/index.php/Vsftpd "Vsftpd")** — 适用于 类UNIX 系统的，轻量级的，标准的，安全的 FTP 服务器。

	[https://security.appspot.com/vsftpd.html](https://security.appspot.com/vsftpd.html) || [vsftpd](https://www.archlinux.org/packages/?name=vsftpd)

#### BitTorrent 客户端

参见 [Wikipedia:Comparison of BitTorrent clients](https://en.wikipedia.org/wiki/Comparison_of_BitTorrent_clients "wikipedia:Comparison of BitTorrent clients").

##### 命令行

###### 命令行后端

虽说可以在命令行上用，但均有可选的图形前端。

*   **[aria2](/index.php/Aria2 "Aria2")** — 轻量级的下载工具，支持 HTTP(S), FTP, BitTorrent (DHT, PEX, MSE/PE)协议以及元链接。能够以守护进程运行，通过 JSON-RPC & XML-RPC 接口管理

	[http://aria2.sourceforge.net/](http://aria2.sourceforge.net/) || [aria2](https://www.archlinux.org/packages/?name=aria2)

*   **[btpd](/index.php/Btpd "Btpd")** — 简单，命令行界面，守护进程，同时也有 web 和 GTK+ 界面。

	[http://github.com/btpd/btpd](http://github.com/btpd/btpd) || [btpd](https://aur.archlinux.org/packages/btpd/)

*   **[MLDonkey](https://en.wikipedia.org/wiki/MLDonkey "wikipedia:MLDonkey")** — 支持 BitTorrent 的多协议 P2P 客户端

	[http://mldonkey.sourceforge.net/](http://mldonkey.sourceforge.net/) || [mldonkey](https://www.archlinux.org/packages/?name=mldonkey)

*   **[Transmission](https://en.wikipedia.org/wiki/Transmission_(BitTorrent_client) "wikipedia:Transmission (BitTorrent client)")** — 简单易用的BitTorrent 客户端，拥有守护程序版本, TK+, Qt 图形用户界面, 网页和命令行前端

	[http://www.transmissionbt.com/](http://www.transmissionbt.com/) || [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli)

###### 纯命令行界面

*   **[rTorrent](/index.php/RTorrent "RTorrent")** — 简单的轻量级 BitTorrent 客户端

	[http://libtorrent.rakshasa.no/](http://libtorrent.rakshasa.no/) || [rtorrent](https://www.archlinux.org/packages/?name=rtorrent)

##### 图形环境

###### libtorrent-rasterbar 后端

*   **[Deluge](/index.php/Deluge "Deluge")** — 用户友好的 BitTorrent 客户端，用Python和PyGTK编写

	[http://deluge-torrent.org/](http://deluge-torrent.org/) || [deluge](https://www.archlinux.org/packages/?name=deluge)

*   **FatRat** — 基于 Qt 和 C++ 的下载器，支持 HTTP, FTP, SFTP. BT, rapidshare 以及更多。

	[http://fatrat.dolezel.info/](http://fatrat.dolezel.info/) || [fatrat](https://aur.archlinux.org/packages/fatrat/)

*   **[qBittorrent](https://en.wikipedia.org/wiki/qBittorrent "wikipedia:qBittorrent")** — 一个和 µtorrent 相类似的开源 （GPLv2)BitTorrent 客户端。

	[http://qbittorrent.sourceforge.net/](http://qbittorrent.sourceforge.net/) || [qbittorrent](https://www.archlinux.org/packages/?name=qbittorrent)

*   **[Tribler](https://en.wikipedia.org/wiki/Tribler "wikipedia:Tribler")** — 第四代文件共享系统 BT 客户端。

	[http://www.tribler.org](http://www.tribler.org) || [tribler](https://aur.archlinux.org/packages/tribler/)

###### libktorrent 后端

*   **[KGet](https://en.wikipedia.org/wiki/KGet "wikipedia:KGet")** — 一个支持 HTTP(S). FTP 和 BitTorrent 的 KDE 下载管理器.

	[http://www.kde.org/applications/internet/kget/](http://www.kde.org/applications/internet/kget/) || [kdenetwork-kget](https://www.archlinux.org/packages/?name=kdenetwork-kget)

*   **[KTorrent](https://en.wikipedia.org/wiki/KTorrent "wikipedia:KTorrent")** — 一个 KDE 下的多功能 BitTorrent 客户端.

	[http://ktorrent.org/](http://ktorrent.org/) || [ktorrent](https://www.archlinux.org/packages/?name=ktorrent)

###### 其它

*   **QTorrent** — 一个用PyQt写的BT客户端.

	[http://thegraveyard.org/qtorrent.php](http://thegraveyard.org/qtorrent.php) || [qtorrent](https://aur.archlinux.org/packages/qtorrent/)

*   **Tixati** — BitTorrent 协议，P2P 客户端。P

	[http://www.tixati.com](http://www.tixati.com) || [tixati](https://aur.archlinux.org/packages/tixati/)

*   **[Transmission](https://en.wikipedia.org/wiki/Transmission_(BitTorrent_client) "wikipedia:Transmission (BitTorrent client)")** — 简单易用的 BitTorrent 客户端，拥有守护程序版本, 拥有 GTK+, Qt 图形用户界面, 网页和命令行前端

	[http://transmissionbt.com/](http://transmissionbt.com/) || [transmission-gtk](https://www.archlinux.org/packages/?name=transmission-gtk) [transmission-qt](https://www.archlinux.org/packages/?name=transmission-qt)

*   **[Vuze](https://en.wikipedia.org/wiki/Vuze "wikipedia:Vuze")** — 功能强大的 BitTorrent 客户端，用 Java 编写（以前是 Azureus）.

	[https://www.vuze.com/](https://www.vuze.com/) || [vuze](https://aur.archlinux.org/packages/vuze/)

#### 电驴

eDonkey仍然是第二大p2p网络 (参见 [Internet Study 2008/2009](http://www.ipoque.com/en/resources/internet-studies)).

*   **[aMule](/index.php/AMule "AMule")** — 著名的有守护进程的eDonkey/Kad 客户端，拥有GTK+,网页和命令行前端

	[http://www.amule.org/](http://www.amule.org/) || [amule](https://www.archlinux.org/packages/?name=amule)

*   **[MlDonkey](/index.php?title=MlDonkey&action=edit&redlink=1 "MlDonkey (page does not exist)")** — A multi-network P2P client.

	[http://mldonkey.sourceforge.net/](http://mldonkey.sourceforge.net/) || [mldonkey](https://www.archlinux.org/packages/?name=mldonkey)

*   **[Neoloader](/index.php?title=Neoloader&action=edit&redlink=1 "Neoloader (page does not exist)")** — Privacy using NeoKads mash routing.

	[http://http://neoloader.com/](http://http://neoloader.com/) || [neoloader](https://aur.archlinux.org/packages/neoloader/)

*   **KaMule** — kde下的aMule图形前端.

	[http://kde-apps.org/content/show.php?content=150270](http://kde-apps.org/content/show.php?content=150270) || [kamule](https://aur.archlinux.org/packages/kamule/)

#### Gnutella

*   **[Sharelin](https://en.wikipedia.org/wiki/Sharelin "wikipedia:Sharelin")** — Gnutella2 only client with a web UI.

	[http://sourceforge.net/apps/mediawiki/sharelin](http://sourceforge.net/apps/mediawiki/sharelin) || [sharelin](https://aur.archlinux.org/packages/sharelin/)

### 通讯

#### 邮件客户端

See also [Wikipedia:Comparison of e-mail clients](https://en.wikipedia.org/wiki/Comparison_of_e-mail_clients "wikipedia:Comparison of e-mail clients").

##### 终端

*   **alot** — An experimental terminal MUA based on [notmuch mail](http://notmuchmail.org/). It is written in python using the [urwid](http://urwid.org/) toolkit.

	[https://github.com/pazz/alot](https://github.com/pazz/alot) || [alot](https://aur.archlinux.org/packages/alot/) [alot-git](https://aur.archlinux.org/packages/alot-git/)

*   **[Alpine](/index.php/Alpine "Alpine")** — Fast, easy-to-use and Apache-licensed email client based on [Pine](https://en.wikipedia.org/wiki/Pine_(email_client) "wikipedia:Pine (email client)").

	[https://washington.edu/alpine](https://washington.edu/alpine) || [re-alpine](https://aur.archlinux.org/packages/re-alpine/) [alpine](https://aur.archlinux.org/packages/alpine/)

*   **[Gnus](https://en.wikipedia.org/wiki/Gnus "wikipedia:Gnus")** — Email, NNTP and RSS client for Emacs.

	[http://gnus.org/](http://gnus.org/) || [emacs-gnus-git](https://aur.archlinux.org/packages/emacs-gnus-git/)

*   **S-nail** — a mail processing system with a command syntax reminiscent of *ed* with lines replaced by messages. Provides the functionality of [mailx](https://en.wikipedia.org/wiki/mailx "wikipedia:mailx") and much more.

	[http://sourceforge.net/projects/s-nail/](http://sourceforge.net/projects/s-nail/) || [s-nail](https://www.archlinux.org/packages/?name=s-nail)

*   **mu/mu4e** — Email indexer (mu) and client for emacs (mu4e). Xapian based for fast searches.

	[http://www.djcbsoftware.nl/code/mu/mu4e.html](http://www.djcbsoftware.nl/code/mu/mu4e.html) || [mu](https://aur.archlinux.org/packages/mu/)

*   **[Mutt](/index.php/Mutt "Mutt")** — Small but very powerful text-based mail client.

	[http://www.mutt.org/](http://www.mutt.org/) || [mutt](https://www.archlinux.org/packages/?name=mutt)

*   **Nmh** — A modular mail handling system.

	[http://www.nongnu.org/nmh/](http://www.nongnu.org/nmh/) || [nmh](https://aur.archlinux.org/packages/nmh/) [nmh-git](https://aur.archlinux.org/packages/nmh-git/)

*   **[notmuch](/index.php/Notmuch "Notmuch")** — A fast mail indexer built on top of *xapian*.

	[http://notmuchmail.org/](http://notmuchmail.org/) || [notmuch](https://www.archlinux.org/packages/?name=notmuch) [notmuch-vim](https://www.archlinux.org/packages/?name=notmuch-vim) [notmuch-mutt](https://www.archlinux.org/packages/?name=notmuch-mutt)

*   **[Sup](/index.php/Sup "Sup")** — CLI mail client with very fast searching, tagging, threading and GMail like operation.

	[http://supmua.org/](http://supmua.org/) || [sup](https://aur.archlinux.org/packages/sup/)

*   **Wanderlust** — Email client and news reader for Emacs.

	[http://www.gohome.org/wl/](http://www.gohome.org/wl/) || [wanderlust](https://www.archlinux.org/packages/?name=wanderlust)

##### 图形界面

*   **[Balsa](/index.php/Balsa "Balsa")** — Simple and light email client that is part of the Gnome project.

	[http://pawsa.fedorapeople.org/balsa/](http://pawsa.fedorapeople.org/balsa/) || [balsa](https://www.archlinux.org/packages/?name=balsa)

*   **[Claws Mail](https://en.wikipedia.org/wiki/Claws_Mail "wikipedia:Claws Mail")** — Lightweight GTK-based email client and news reader.

	[http://claws-mail.org/](http://claws-mail.org/) || [claws-mail](https://www.archlinux.org/packages/?name=claws-mail)

*   **[Evolution](/index.php/Evolution "Evolution")** — Mature and feature-rich e-mail client used in GNOME by default. Part of [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

	[http://projects.gnome.org/evolution/](http://projects.gnome.org/evolution/) || [evolution](https://www.archlinux.org/packages/?name=evolution)

*   **Geary** — Simple desktop mail client built in [Vala](https://en.wikipedia.org/wiki/Vala_(programming_language) "wikipedia:Vala (programming language)").

	[https://wiki.gnome.org/Apps/Geary](https://wiki.gnome.org/Apps/Geary) || [geary](https://www.archlinux.org/packages/?name=geary)

*   **[Kmail](https://en.wikipedia.org/wiki/Kmail "wikipedia:Kmail")** — Mature and feature-rich email client. Part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[http://kde.org/applications/internet/kmail/](http://kde.org/applications/internet/kmail/) || [kdepim-kmail](https://www.archlinux.org/packages/?name=kdepim-kmail)

*   **Manitou Mail** — Database-driven email system.

	[http://www.manitou-mail.org/](http://www.manitou-mail.org/) || [manitou-mdx](https://aur.archlinux.org/packages/manitou-mdx/) [manitou-ui](https://aur.archlinux.org/packages/manitou-ui/)

*   **Roundcubemail** — Browser-based multilingual IMAP client with a native application-like user interface.

	[http://roundcube.net/](http://roundcube.net/) || [roundcubemail](https://www.archlinux.org/packages/?name=roundcubemail)

*   **[Sylpheed](https://en.wikipedia.org/wiki/Sylpheed "wikipedia:Sylpheed")** — Lightweight and user-friendly GTK+ email client.

	[http://sylpheed.sraoss.jp/en/](http://sylpheed.sraoss.jp/en/) || [sylpheed](https://www.archlinux.org/packages/?name=sylpheed)

*   **[Thunderbird](/index.php/Thunderbird "Thunderbird")** — Feature-rich email client from Mozilla written in GTK+.

	[http://www.mozilla.org/thunderbird/](http://www.mozilla.org/thunderbird/) || [thunderbird](https://www.archlinux.org/packages/?name=thunderbird)

*   **Trojitá** — Qt IMAP email client. Only supports one IMAP account.

	[http://trojita.flaska.net/](http://trojita.flaska.net/) || [trojita](https://www.archlinux.org/packages/?name=trojita)

#### 即时聊天

See also [Wikipedia:Comparison_of_instant_messaging_clients](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients "wikipedia:Comparison of instant messaging clients").

##### 多协议客户端

See also [Wikipedia:Comparison of instant messaging clients#Multiprotocol_clients](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients#Multiprotocol_clients "wikipedia:Comparison of instant messaging clients").

**Note:** All messengers, that support several networks by means of direct connections to them, belong to this section.

列在这里的许多客户端(包括 Pidgin 及其衍生版本)都是通过[libpurple](https://en.wikipedia.org/wiki/libpurple "wikipedia:libpurple")来支持多种及时通讯网络的。这些网络的类型非常多, 但是这些客户端(像任何多协议客户端)通常只有限或不支持每个网络特别的特征。

###### 命令行

*   **BarnOwl** — 一个使用ncurses library的聊天客户端，支持Zephyr, AIM, Jabber, IRC, 和 Twitter协议.

	[http://barnowl.mit.edu/](http://barnowl.mit.edu/) || [barnowl](https://aur.archlinux.org/packages/barnowl/)

*   **[Bitlbee](/index.php/Bitlbee "Bitlbee")** — 一个IRC客户端并且提供了其他流行聊天网络的入口支持(XMPP, MSN, Yahoo, AIM, ICQ and Twitter).

	[http://bitlbee.org/](http://bitlbee.org/) || [bitlbee](https://www.archlinux.org/packages/?name=bitlbee)

*   **[CenterIM](https://en.wikipedia.org/wiki/Centericq "wikipedia:Centericq")** — CenterICQ的复刻软件, 文字模式菜单和窗口驱动的IM界面.

	[http://centerim.org/](http://centerim.org/) || [centerim](https://www.archlinux.org/packages/?name=centerim)

*   **Finch** — 一个使用ncurses library的聊天客户端，使用libpurple并支持其所有的协议.

	[http://developer.pidgin.im/wiki/Using%20Finch](http://developer.pidgin.im/wiki/Using%20Finch) || [finch](https://www.archlinux.org/packages/?name=finch)

*   **[naim](https://en.wikipedia.org/wiki/naim_(software) "wikipedia:naim (software)")** — 一个使用ncurses library的聊天客户端，支持AOL, ICQ, IRC 和the Lily CMC.

	[http://naim.n.ml.org/](http://naim.n.ml.org/) || [naim](https://www.archlinux.org/packages/?name=naim)

###### 图形环境

*   **Carrier** — Pidgin的复刻版，轻微加强的图形界面 (以前叫funpidgin).

	[http://funpidgin.sourceforge.net/](http://funpidgin.sourceforge.net/) || [carrier](https://aur.archlinux.org/packages/carrier/)

*   **[Emesene](https://en.wikipedia.org/wiki/Emesene "wikipedia:Emesene")** — 一个Windows Live Messenger的PyGtk即时通讯客户端, 同样兼容Jabber, Facebook 和 Google Talk.

	[http://emesene.org/](http://emesene.org/) || [emesene](https://aur.archlinux.org/packages/emesene/)

*   **[Empathy](https://en.wikipedia.org/wiki/Empathy_(software) 框架.

	[http://live.gnome.org/Empathy](http://live.gnome.org/Empathy) || [empathy](https://www.archlinux.org/packages/?name=empathy)

*   **Galaxium Messenger** — 专为GNOME桌面设计的通讯软件.

	[https://code.google.com/p/galaxium/](https://code.google.com/p/galaxium/) || [galaxium](https://aur.archlinux.org/packages/galaxium/)

*   **[Instantbird](https://en.wikipedia.org/wiki/Instantbird "wikipedia:Instantbird")** — 使用Mozilla's XUL 和 libpurple的多协议客户端.

	[http://instantbird.com/](http://instantbird.com/) || [instantbird](https://aur.archlinux.org/packages/instantbird/)

*   **[Kopete](https://en.wikipedia.org/wiki/Kopete "wikipedia:Kopete")** — 一个用户友好型即时通讯客户端，支持AIM, ICQ, Windows Live Messenger, Yahoo, Jabber, Gadu-Gadu, Novell GroupWise Messenger, 和其他IM网络.

	[http://kopete.kde.org/](http://kopete.kde.org/) || [kdenetwork-kopete](https://www.archlinux.org/packages/?name=kdenetwork-kopete)

*   **[Telepathy](/index.php/KDE#KDE_Telepathy "KDE")** — 一个KDE 即时通讯客户端，使用[Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) "wikipedia:Telepathy (software)")框架.作为Kopete的替代品而生.

	[http://community.kde.org/Real-Time_Communication_and_Collaboration/](http://community.kde.org/Real-Time_Communication_and_Collaboration/) || [kde-telepathy-meta](https://www.archlinux.org/packages/?name=kde-telepathy-meta)

*   **Licq** — UNIX即时通讯客户端,支持多种协议(ICQ, MSN and Jabber).

	[http://www.licq.org](http://www.licq.org) || [licq](https://www.archlinux.org/packages/?name=licq)

*   **[Pidgin](/index.php/Pidgin "Pidgin")** — 一个多协议即时通讯客户端.

	[http://pidgin.im/](http://pidgin.im/) || [pidgin](https://www.archlinux.org/packages/?name=pidgin)

*   **Pidgin Light** — Pidgin的轻量级版本, 不支持 gstreamer, tcl, tk, xscreensaver

	[http://pidgin.im/](http://pidgin.im/) || [pidgin-light](https://aur.archlinux.org/packages/pidgin-light/)

*   **qutIM** — 一个简单的用户友好型即时通讯客户端，支持ICQ, Jabber, Mail.Ru, IRC 和 VKontakte messaging.

	[http://qutim.org/](http://qutim.org/) || [qutim](https://aur.archlinux.org/packages/qutim/)

#### IRC 客户端

See also [Wikipedia:Comparison of Internet_Relay_Chat_clients](https://en.wikipedia.org/wiki/Comparison_of_Internet_Relay_Chat_clients "wikipedia:Comparison of Internet Relay Chat clients").

**Note:** Most web browsers and many IM clients also support IRC.

###### 终端

*   **[BitchX](https://en.wikipedia.org/wiki/BitchX "wikipedia:BitchX")** — Console-based IRC client developed from the popular [ircII](https://en.wikipedia.org/wiki/ircII "wikipedia:ircII").

	[http://www.bitchx.org/](http://www.bitchx.org/) || [bitchx-git](https://aur.archlinux.org/packages/bitchx-git/)

*   **ERC** — Powerful, modular, and extensible IRC client for [Emacs](/index.php/Emacs "Emacs").

	[http://savannah.gnu.org/projects/erc/](http://savannah.gnu.org/projects/erc/) || [erc-git](https://aur.archlinux.org/packages/erc-git/)

*   **[ii](https://en.wikipedia.org/wiki/Ii_(IRC_client) "wikipedia:Ii (IRC client)")** — Featherweight IRC client, literally `tail -f` the conversation and `echo` back your replies to a file.

	[http://tools.suckless.org/ii](http://tools.suckless.org/ii) || [ii](https://aur.archlinux.org/packages/ii/)

*   **Ircfs** — File system interface to IRC written in [Limbo](http://limbo.cat-v.org).

	[http://www.ueber.net/code/r/ircfs](http://www.ueber.net/code/r/ircfs) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=ircfs)</small>

*   **[Irssi](/index.php/Irssi "Irssi")** — Highly-configurable ncurses-based IRC client.

	[http://irssi.org/](http://irssi.org/) || [irssi](https://www.archlinux.org/packages/?name=irssi)

*   **ScrollZ** — Advanced IRC client based on [ircII](https://en.wikipedia.org/wiki/ircII "wikipedia:ircII").

	[http://www.scrollz.info/](http://www.scrollz.info/) || [scrollz](https://aur.archlinux.org/packages/scrollz/)

*   **sic** — Extremely simple IRC client, similar to [ii](https://en.wikipedia.org/wiki/Ii_(IRC_client) "wikipedia:Ii (IRC client)").

	[http://tools.suckless.org/sic](http://tools.suckless.org/sic) || [sic](https://aur.archlinux.org/packages/sic/)

*   **[WeeChat](https://en.wikipedia.org/wiki/WeeChat "wikipedia:WeeChat")** — Modular, lightweight ncurses-based IRC client.

	[http://weechat.org/](http://weechat.org/) || [weechat](https://www.archlinux.org/packages/?name=weechat)

###### 图形界面

*   **HexChat** — 基于Xchat，支持Linux和Windows。

	[http://hexchat.github.io/](http://hexchat.github.io/) || [hexchat](https://www.archlinux.org/packages/?name=hexchat)

*   **[Konversation](https://en.wikipedia.org/wiki/Konversation "wikipedia:Konversation")** — KDE桌面的IRC客户端。

	[http://konversation.kde.org/](http://konversation.kde.org/) || [konversation](https://www.archlinux.org/packages/?name=konversation)

*   **[KVIrc](https://en.wikipedia.org/wiki/KVIrc "wikipedia:KVIrc")** — 基于QT且能够更外主题外观的IRC客户端。

	[http://kvirc.net/](http://kvirc.net/) || [kvirc](https://www.archlinux.org/packages/?name=kvirc)

*   **Loqui** — 依赖少，基于GTK的IRC客户端。 [GNet](https://live.gnome.org/GNetLibrary)

	[https://launchpad.net/loqui](https://launchpad.net/loqui) || [loqui](https://aur.archlinux.org/packages/loqui/)

*   **LostIRC** — 简单的基于GTK+的IRC客户端，具有Tab补全功能，支持多服务器和日志记录等。

	[http://lostirc.sourceforge.net](http://lostirc.sourceforge.net) || [lostirc](https://aur.archlinux.org/packages/lostirc/)

*   **pcw** — [ii](http://tools.suckless.org/ii)的图形前端， 可以为每一个通信开启一个终端。

	[https://bitbucket.org/emg/pcw](https://bitbucket.org/emg/pcw) || [pcw-hg](https://aur.archlinux.org/packages/pcw-hg/)

*   **Polari** — Gnome项目中的简洁IRC客户端。

	[https://wiki.gnome.org/Apps/Polari/](https://wiki.gnome.org/Apps/Polari/) || [polari](https://www.archlinux.org/packages/?name=polari)

*   **[Quassel](https://en.wikipedia.org/wiki/Quassel_IRC "wikipedia:Quassel IRC")** — 现代的跨平台分布式IRC客户端。

	[http://quassel-irc.org/](http://quassel-irc.org/) || [quassel-core](https://www.archlinux.org/packages/?name=quassel-core) [quassel-client](https://www.archlinux.org/packages/?name=quassel-client)

*   **[Smuxi](https://en.wikipedia.org/wiki/Smuxi "wikipedia:Smuxi")** — 跨平台的IRC客户端 ，灵感来自于[Irssi](/index.php/Irssi "Irssi")。

	[http://smuxi.org/](http://smuxi.org/) || [smuxi](https://www.archlinux.org/packages/?name=smuxi)

##### XMPP (Jabber)

See also [Wikipedia:XMPP](https://en.wikipedia.org/wiki/XMPP "wikipedia:XMPP") and [Wikipedia:Comparison of instant messaging clients#XMPP-related features](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients#XMPP-related_features "wikipedia:Comparison of instant messaging clients").

###### 命令行客户端

*   **Freetalk** — Console-based Jabber client.

	[https://gnu.org/s/freetalk/](https://gnu.org/s/freetalk/) || [freetalk](https://www.archlinux.org/packages/?name=freetalk)

*   **jabber.el** — Minimal Jabber client for [Emacs](/index.php/Emacs "Emacs").

	[http://emacs-jabber.sourceforge.net/](http://emacs-jabber.sourceforge.net/) || [emacs-jabber](https://aur.archlinux.org/packages/emacs-jabber/)

*   **[MCabber](https://en.wikipedia.org/wiki/MCabber "wikipedia:MCabber")** — Small Jabber console client, includes features: SSL, PGP, MUC, OTR, and UTF8.

	[http://mcabber.com/](http://mcabber.com/) || [mcabber](https://www.archlinux.org/packages/?name=mcabber)

*   **Profanity** — A console based Jabber client inspired by Irssi.

	[http://www.profanity.im/](http://www.profanity.im/) || [profanity](https://www.archlinux.org/packages/?name=profanity)

###### 图形界面客户端

*   **[Gajim](https://en.wikipedia.org/wiki/Gajim "wikipedia:Gajim")** — Jabber client written in PyGTK.

	[https://gajim.org/](https://gajim.org/) || [gajim](https://www.archlinux.org/packages/?name=gajim)

*   **Jabbim** — Jabber client written in PyQt.

	[http://www.jabbim.com/](http://www.jabbim.com/) || [jabbim-svn](https://aur.archlinux.org/packages/jabbim-svn/)

*   **[Psi](https://en.wikipedia.org/wiki/Psi_(instant_messaging_client) "wikipedia:Psi (instant messaging client)")** — Qt-based Jabber client which supports video conferencing (since version 0.13).

	[http://psi-im.org/](http://psi-im.org/) || [psi](https://www.archlinux.org/packages/?name=psi) [psimedia](https://aur.archlinux.org/packages/psimedia/)

*   **Psi+** — Enhanced version of the Psi Jabber client with many new [features](http://psi-plus.com/wiki/en:features#differences_between_psi_beta_version_and_the_official_psi_015-dev_version).

	[https://code.google.com/p/psi-dev/](https://code.google.com/p/psi-dev/) || [psi-plus-git](https://aur.archlinux.org/packages/psi-plus-git/)

*   **[Tkabber](https://en.wikipedia.org/wiki/Tkabber "wikipedia:Tkabber")** — Easy to hack feature-rich XMPP client by the author of the ejabberd XMPP server.

	[http://tkabber.jabber.ru/](http://tkabber.jabber.ru/) || [tkabber](https://www.archlinux.org/packages/?name=tkabber)

###### 服务器

See also [Wikipedia:Comparison of XMPP server software](https://en.wikipedia.org/wiki/Comparison_of_XMPP_server_software "wikipedia:Comparison of XMPP server software").

*   **[Prosody](/index.php/Prosody "Prosody")** — An XMPP server written in the [Lua](http://www.lua.org/) programming language. Prosody is designed to be lightweight and highly extensible. It is licensed under a permissive [MIT license](http://prosody.im/source/mit).

	[http://prosody.im/](http://prosody.im/) || [prosody](https://www.archlinux.org/packages/?name=prosody)

*   **Ejabberd** — Jabber server written in Erlang

	[http://www.ejabberd.im/](http://www.ejabberd.im/) || [ejabberd](https://www.archlinux.org/packages/?name=ejabberd)

*   **[Jabberd2](/index.php/Jabberd2 "Jabberd2")** — An XMPP server written in the C language and licensed under the GNU General Public License. It was inspired by jabberd14.

	[http://jabberd2.org](http://jabberd2.org) || [jabberd2](https://aur.archlinux.org/packages/jabberd2/)

*   **Openfire** — An XMPP IM multiplatform server written in Java

	[http://www.igniterealtime.org/projects/openfire/](http://www.igniterealtime.org/projects/openfire/) || [openfire](https://www.archlinux.org/packages/?name=openfire)

##### 多协议客户端

见 [Wikipedia:Comparison of instant messaging clients](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients "wikipedia:Comparison of instant messaging clients").

**Note:** All messengers, that support several networks by means of direct connections to them, belong to this section.

Many clients listed here (including Pidgin and all its forks) support multiple IM networks via [libpurple](https://en.wikipedia.org/wiki/libpurple "wikipedia:libpurple"). The number of networks supported by these clients is very large but they (like any multiprotocol clients) usually have very limited or no support for network-specific features.

###### 命令行

*   **BarnOwl** — Ncurses-based chat client with support for the Zephyr, AIM, Jabber, IRC, and Twitter protocols.

	[http://barnowl.mit.edu/](http://barnowl.mit.edu/) || [barnowl](https://aur.archlinux.org/packages/barnowl/)

*   **[Bitlbee](/index.php/Bitlbee "Bitlbee")** — IRC client that provides a gateway to popular chat networks (XMPP, MSN, Yahoo, AIM, ICQ and Twitter).

	[http://bitlbee.org/](http://bitlbee.org/) || [bitlbee](https://www.archlinux.org/packages/?name=bitlbee)

*   **[CenterIM](https://en.wikipedia.org/wiki/Centericq "wikipedia:Centericq")** — Fork of CenterICQ, a text mode menu- and window-driven IM interface.

	[http://centerim.org/](http://centerim.org/) || [centerim](https://www.archlinux.org/packages/?name=centerim)

*   **[Finch](/index.php/Pidgin "Pidgin")** — Ncurses-based chat client that uses libpurple and supports all its protocols.

	[http://developer.pidgin.im/wiki/Using%20Finch](http://developer.pidgin.im/wiki/Using%20Finch) || [finch](https://www.archlinux.org/packages/?name=finch)

*   **[naim](https://en.wikipedia.org/wiki/naim_(software) "wikipedia:naim (software)")** — Ncurses chat client with support for AOL, ICQ, IRC and the Lily CMC.

	[http://naim.n.ml.org/](http://naim.n.ml.org/) || [naim](https://www.archlinux.org/packages/?name=naim)

*   **pork** — Programmable, ncurses-based AIM and IRC client that mostly looks and feels like ircII.

	[http://dev.ojnk.net/](http://dev.ojnk.net/) || [pork](https://www.archlinux.org/packages/?name=pork)

*   **[Tox](/index.php/Tox "Tox")** — Tox is a distributed, secure messenger with audio and video chat capabilities.

	[https://tox.chat/](https://tox.chat/) || [tox-git](https://aur.archlinux.org/packages/tox-git/)

###### 图形界面

*   **Carrier** — Pidgin fork providing minor GUI enhancements (formerly FunPidgin).

	[http://funpidgin.sourceforge.net/](http://funpidgin.sourceforge.net/) || [carrier](https://aur.archlinux.org/packages/carrier/)

*   **[Emesene](https://en.wikipedia.org/wiki/Emesene "wikipedia:Emesene")** — PyGTK instant messenger for the Windows Live Messenger network, also compatible with Jabber, Facebook and Google Talk.

	[http://emesene.org/](http://emesene.org/) || [emesene](https://aur.archlinux.org/packages/emesene/)

*   **[Empathy](https://en.wikipedia.org/wiki/Empathy_(software) framework.

	[http://live.gnome.org/Empathy](http://live.gnome.org/Empathy) || [empathy](https://www.archlinux.org/packages/?name=empathy)

*   **Galaxium Messenger** — Messenger application designed for the GNOME desktop.

	[https://code.google.com/p/galaxium/](https://code.google.com/p/galaxium/) || [galaxium](https://aur.archlinux.org/packages/galaxium/)

*   **[Instantbird](https://en.wikipedia.org/wiki/Instantbird "wikipedia:Instantbird")** — Multi-protocol chat client using Mozilla's XUL and libpurple.

	[http://instantbird.com/](http://instantbird.com/) || [instantbird](https://aur.archlinux.org/packages/instantbird/)

*   **[Kopete](https://en.wikipedia.org/wiki/Kopete "wikipedia:Kopete")** — User-friendly IM supporting AIM, ICQ, Windows Live Messenger, Yahoo, Jabber, Gadu-Gadu, Novell GroupWise Messenger, and other IM networks. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

	[http://kopete.kde.org/](http://kopete.kde.org/) || [kdenetwork-kopete](https://www.archlinux.org/packages/?name=kdenetwork-kopete)

*   **[KDE Telepathy](/index.php/KDE#KDE_Telepathy "KDE")** — KDE instant messaging client using the [Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) framework. Meant as a replacement for Kopete.

	[http://community.kde.org/Real-Time_Communication_and_Collaboration/](http://community.kde.org/Real-Time_Communication_and_Collaboration/) || [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta)

*   **Licq** — Instant messaging client for UNIX supporting multiple protocols (currently ICQ, MSN and Jabber).

	[http://www.licq.org](http://www.licq.org) || [licq](https://www.archlinux.org/packages/?name=licq)

*   **Mikutter** — An open-source Twitter client using [GTK+](/index.php/GTK%2B "GTK+") and Ruby.

	[http://mikutter.hachune.net/](http://mikutter.hachune.net/) || [mikutter](https://aur.archlinux.org/packages/mikutter/) [mikutter-git](https://aur.archlinux.org/packages/mikutter-git/)

*   **[Pidgin](/index.php/Pidgin "Pidgin")** — Multi-protocol instant messaging client.

	[http://pidgin.im/](http://pidgin.im/) || [pidgin](https://www.archlinux.org/packages/?name=pidgin) [pidgin-light](https://aur.archlinux.org/packages/pidgin-light/)

*   **qutIM** — Simple and user-friendly IM supporting ICQ, Jabber, Mail.Ru, IRC and VKontakte messaging.

	[http://qutim.org/](http://qutim.org/) || [qutim-stable](https://aur.archlinux.org/packages/qutim-stable/)

#### 局域网聊天

See also: [Comparison of LAN messengers](https://en.wikipedia.org/wiki/Comparison_of_LAN_messengers "wikipedia:Comparison of LAN messengers").

*   **iptux** — Lan communication software, compatible with IP Messenger.

	[https://github.com/iptux-src/iptux](https://github.com/iptux-src/iptux) || [iptux](https://aur.archlinux.org/packages/iptux/)

#### 软件式电话

See also [Wikipedia:Comparison of VoIP software](https://en.wikipedia.org/wiki/Comparison_of_VoIP_software "wikipedia:Comparison of VoIP software") and [Wikipedia:List of SIP software](https://en.wikipedia.org/wiki/List_of_SIP_software "wikipedia:List of SIP software").

##### 客户端

**Note:** Some [IM clients](#Instant_messaging) also offer voice and video communication

###### SIP

*   **[Blink](https://en.wikipedia.org/wiki/Blink_(software) "wikipedia:Blink (software)")** — State of the art, easy to use SIP client.

	[http://www.icanblink.com/](http://www.icanblink.com/) || [blink-darcs](https://aur.archlinux.org/packages/blink-darcs/)

*   **[Ekiga](https://en.wikipedia.org/wiki/Ekiga "wikipedia:Ekiga")** — VoIP and video conferencing application with full SIP and H.323 support (formerly known as GNOME Meeting).

	[http://www.ekiga.org/](http://www.ekiga.org/) || [ekiga](https://www.archlinux.org/packages/?name=ekiga)

*   **[Empathy](https://en.wikipedia.org/wiki/Empathy_(software) "wikipedia:Empathy (software)")** — GNOME instant messenger client using the Telepathy framework with SIP support (using the Sofia-SIP library).

	[https://live.gnome.org/Empathy](https://live.gnome.org/Empathy) || [empathy](https://www.archlinux.org/packages/?name=empathy)

*   **[Jitsi](https://en.wikipedia.org/wiki/Jitsi "wikipedia:Jitsi")** — Audio/video SIP VoIP phone and instant messenger written in Java (formerly SIP-Communicator).

	[https://jitsi.org/](https://jitsi.org/) || [jitsi](https://aur.archlinux.org/packages/jitsi/)

*   **[KPhone](https://en.wikipedia.org/wiki/KPhone "wikipedia:KPhone")** — Qt SIP User Agent with voice, video and text messaging support.

	[http://sourceforge.net/projects/kphone/](http://sourceforge.net/projects/kphone/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=kphone)</small>

*   **[Linphone](https://en.wikipedia.org/wiki/Linphone "wikipedia:Linphone")** — VoIP phone application that allows you to to communicate freely with people over the internet, with voice, video, and text instant messaging.

	[http://www.linphone.org/](http://www.linphone.org/) || [linphone](https://www.archlinux.org/packages/?name=linphone)

*   **Minisip** — SIP User Agent with focus on security (supports TLS, end-to-end security, SRTP, MIKEY (DH, PSK, PKE)).

	[http://www.minisip.org/](http://www.minisip.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=minisip)</small>

*   **[QuteCom](https://en.wikipedia.org/wiki/QuteCom "wikipedia:QuteCom")** — Softphone which allows you to make free PC to PC video and voice calls, and to integrate all your IM contacts in one place (formerly Wengo Phone).

	[http://trac.qutecom.org/](http://trac.qutecom.org/) || [qutecom](https://aur.archlinux.org/packages/qutecom/)

*   **[Twinkle](https://en.wikipedia.org/wiki/Twinkle_(software) "wikipedia:Twinkle (software)")** — Qt softphone for VoIP and IM communication using SIP.

	[http://www.twinklephone.com/](http://www.twinklephone.com/) || [twinkle](https://aur.archlinux.org/packages/twinkle/)

*   **[X-Lite](https://en.wikipedia.org/wiki/X-Lite "wikipedia:X-Lite")** — Proprietary freeware VoIP soft phone that uses SIP.

	[http://www.counterpath.net/x-lite](http://www.counterpath.net/x-lite) || [xlite_bin](https://aur.archlinux.org/packages/xlite_bin/)

*   **[Zfone](https://en.wikipedia.org/wiki/Zfone "wikipedia:Zfone")** — Softphone application for secure voice communication over the Internet (VoIP), using the ZRTP protocol.

	[http://zfoneproject.com/](http://zfoneproject.com/) || [zfone](https://aur.archlinux.org/packages/zfone/)

###### IAX2

*   **Kiax** — Qt-based IAX/2 Softphone.

	[http://www.forschung-direkt.eu/projects/kiax2/](http://www.forschung-direkt.eu/projects/kiax2/) || [kiax](https://aur.archlinux.org/packages/kiax/)

###### Skype

*   **[Skype](/index.php/Skype "Skype")** — Popular but proprietary application for high-quality voice communication.

	[http://www.skype.com/](http://www.skype.com/) || [skype](https://aur.archlinux.org/packages/skype/)

###### 其它

*   **Hangups** — A third-party instant messaging client for Google Hangouts

	[https://github.com/tdryer/hangups](https://github.com/tdryer/hangups) || [hangups-git](https://aur.archlinux.org/packages/hangups-git/)

*   **[Mumble](https://en.wikipedia.org/wiki/Mumble_(software) "wikipedia:Mumble (software)")** — Voice chat application similar to TeamSpeak.

	[http://mumble.sourceforge.net/](http://mumble.sourceforge.net/) || [mumble](https://www.archlinux.org/packages/?name=mumble)

*   **[TeamSpeak](/index.php/TeamSpeak "TeamSpeak")** — Proprietary VoIP application with gamers as its target audience.

	[http://www.teamspeak.com/](http://www.teamspeak.com/) || [teamspeak3](https://www.archlinux.org/packages/?name=teamspeak3)

*   **Webex** — Proprietary conferencing software.

	[http://www.webex.com/](http://www.webex.com/) || [webex](https://aur.archlinux.org/packages/webex/)

###### 多协议

*   **[SFLPhone](https://en.wikipedia.org/wiki/SFLphone "wikipedia:SFLphone")** — Open-source SIP/IAX2 compatible softphone with PulseAudio support.

	[http://sflphone.org/](http://sflphone.org/) || [sflphone](https://aur.archlinux.org/packages/sflphone/)

##### 实用工具

*   **Gladstone** — Educational ITU-T G.729 compliant codec with a GStreamer plugin.

	[https://gitorious.org/gladstone](https://gitorious.org/gladstone) || [gladstone-drizztbsd-git](https://aur.archlinux.org/packages/gladstone-drizztbsd-git/)

*   **SIPp** — Open source test tool and traffic generator for the SIP protocol.

	[http://sipp.sourceforge.net/](http://sipp.sourceforge.net/) || [sipp](https://aur.archlinux.org/packages/sipp/)

*   **Sipsak** — Small command-line tool for developers and administrators of SIP applications.

	[http://sipsak.org/](http://sipsak.org/) || [sipsak](https://aur.archlinux.org/packages/sipsak/)

### 新闻，RSS 与博客

See also [Wikipedia:Comparison of feed aggregators](https://en.wikipedia.org/wiki/Comparison_of_feed_aggregators "wikipedia:Comparison of feed aggregators").

#### 新闻抓取

See also [Wikipedia:Comparison of feed aggregators](https://en.wikipedia.org/wiki/Comparison_of_feed_aggregators "wikipedia:Comparison of feed aggregators").

##### 终端

*   **[Canto](https://en.wikipedia.org/wiki/Canto_(news_aggregator) "wikipedia:Canto (news aggregator)")** — Ncurses RSS aggregator.

	[http://codezen.org/canto/](http://codezen.org/canto/) || [canto-next-git](https://aur.archlinux.org/packages/canto-next-git/)

*   **[Gnus](https://en.wikipedia.org/wiki/Gnus "wikipedia:Gnus")** — Email, NNTP and RSS client for Emacs.

	[http://gnus.org/](http://gnus.org/) || [emacs-gnus-git](https://aur.archlinux.org/packages/emacs-gnus-git/)

*   **Newsbeuter** — Ncurses RSS aggregator with layout and keybinding similar to the [Mutt](/index.php/Mutt "Mutt") email client.

	[http://newsbeuter.org](http://newsbeuter.org) || [newsbeuter](https://www.archlinux.org/packages/?name=newsbeuter)

*   **Rawdog** — "RSS Aggregator Without Delusions Of Grandeur" that parses RSS/CDF/Atom feeds into a static HTML page of articles in chronological order.

	[http://offog.org/code/rawdog.html](http://offog.org/code/rawdog.html) || [rawdog](https://www.archlinux.org/packages/?name=rawdog)

*   **Snownews** — Text mode RSS news reader.

	[http://kiza.kcore.de/software/snownews/](http://kiza.kcore.de/software/snownews/) || [snownews](https://www.archlinux.org/packages/?name=snownews)

##### 图形界面

*   **[Akregator](https://en.wikipedia.org/wiki/Kontact#News_Feed_Aggregator "wikipedia:Kontact")** — News aggregator for KDE, part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[http://kde.org/applications/internet/akregator/](http://kde.org/applications/internet/akregator/) || [kdepim-akregator](https://www.archlinux.org/packages/?name=kdepim-akregator)

*   **Blam** — Simple newsreader for GNOME written in C Sharp.

	[https://git.gnome.org/browse/blam](https://git.gnome.org/browse/blam) || [blam](https://aur.archlinux.org/packages/blam/)

*   **[BlogBridge](https://en.wikipedia.org/wiki/BlogBridge "wikipedia:BlogBridge")** — Excellent Java-based aggregator, which gives users the option to synchronize their feeds across multiple computers. Though according to the official website, project is not being supported any more.

	[http://blogbridge.com](http://blogbridge.com) || [blogbridge](https://aur.archlinux.org/packages/blogbridge/)

*   **[Liferea](https://en.wikipedia.org/wiki/Liferea "wikipedia:Liferea")** — GTK+ news aggregator for online news feeds and weblogs.

	[http://liferea.sourceforge.net](http://liferea.sourceforge.net) || [liferea](https://www.archlinux.org/packages/?name=liferea)

*   **RSS Guard** — Very tiny RSS and ATOM news reader developed using Qt framework.

	[https://bitbucket.org/skunkos/rssguard](https://bitbucket.org/skunkos/rssguard) || [rssguard](https://aur.archlinux.org/packages/rssguard/)

*   **[RSSOwl](https://en.wikipedia.org/wiki/RSSOwl "wikipedia:RSSOwl")** — Powerful aggregator for RSS and Atom feeds, written in Java using Eclipse Rich Client Platform and SWT as a widget toolkit.

	[http://boreal.rssowl.org](http://boreal.rssowl.org) || [rssowl](https://aur.archlinux.org/packages/rssowl/)

*   **[Thunderbird](/index.php/Thunderbird "Thunderbird")** — Email client from Mozilla which also functions as a pretty nice news aggregator.

	[http://www.mozilla.org/thunderbird/](http://www.mozilla.org/thunderbird/) || [thunderbird](https://www.archlinux.org/packages/?name=thunderbird)

*   **Tickr (formerly News)** — GTK-based RSS Reader that displays feeds as a smooth scrolling line on your Desktop, as known from TV stations.

	[http://newsrssticker.com/](http://newsrssticker.com/) || [tickr](https://aur.archlinux.org/packages/tickr/)

*   **Urssus** — Cross platform GUI news aggregator.

	[https://code.google.com/p/urssus/](https://code.google.com/p/urssus/) || [urssus](https://aur.archlinux.org/packages/urssus/)

*   **QuiteRSS** — RSS/Atom feed reader written on Qt/С++.

	[http://quiterss.org/](http://quiterss.org/) || [quiterss](https://aur.archlinux.org/packages/quiterss/)

#### 播客客户端

#### Usenet 新闻播报与新闻抓取

Some [email clients](#Email_clients) also support NNTP. This section mainly lists NNTP-only client.

See also: [Wikipedia:List of Usenet newsreaders](https://en.wikipedia.org/wiki/List_of_Usenet_newsreaders "wikipedia:List of Usenet newsreaders"), [Wikipedia:Comparison of Usenet newsreaders](https://en.wikipedia.org/wiki/Comparison_of_Usenet_newsreaders "wikipedia:Comparison of Usenet newsreaders").

*   **lottanzb** — A *SABnzbd+* (Usenet binary downloader) GUI front-end written in PyGTK

	[http://www.lottanzb.org/](http://www.lottanzb.org/) || [lottanzb](https://aur.archlinux.org/packages/lottanzb/)

*   **nn** — Alternative more user-friendly(curses-based) Usenet newsreader for UNIX.

	[http://www.nndev.org/](http://www.nndev.org/) || [nn](https://aur.archlinux.org/packages/nn/)

*   **[NZBGet](/index.php/NZBGet "NZBGet")** — CLI Utility to grab Usenet binary file using .nzb files.

	[http://nzbget.sourceforge.net/](http://nzbget.sourceforge.net/) || [nzbget](https://www.archlinux.org/packages/?name=nzbget)

*   **[pan](https://en.wikipedia.org/wiki/Pan_(newsreader) "wikipedia:Pan (newsreader)")** — A GTK2 Usenet newsreader that's good at both text and binaries.

	[http://pan.rebelbase.com/](http://pan.rebelbase.com/) || [pan](https://www.archlinux.org/packages/?name=pan)

*   **[slrn](https://en.wikipedia.org/wiki/slrn "wikipedia:slrn")** — An open source text-based news client.

	[http://www.slrn.org/](http://www.slrn.org/) || [slrn](https://www.archlinux.org/packages/?name=slrn)

*   **[tin](https://en.wikipedia.org/wiki/Tin_(newsreader) "wikipedia:Tin (newsreader)")** — A cross-platform threaded NNTP and spool based UseNet newsreader.

	[http://tin.org/](http://tin.org/) || [tin](https://aur.archlinux.org/packages/tin/)

*   **trn** — A text-based Threaded Usenet newsreader.

	[http://trn.sourceforge.net/](http://trn.sourceforge.net/) || [trn](https://aur.archlinux.org/packages/trn/)

*   **[XPN](https://en.wikipedia.org/wiki/XPN_(newsreader) "wikipedia:XPN (newsreader)")** — A graphical newsreader use PyGTK.

	[http://xpn.altervista.org/index-en.html](http://xpn.altervista.org/index-en.html) || [xpn](https://aur.archlinux.org/packages/xpn/)

*   **xrn** — Usenet newsreader for X Window System.

	[http://www.mit.edu/people/jik/software/xrn.html](http://www.mit.edu/people/jik/software/xrn.html) || [xrn](https://aur.archlinux.org/packages/xrn/)

#### 博客软件

See also [Wikipedia:Blog software](https://en.wikipedia.org/wiki/Blog_software "wikipedia:Blog software") and [Wikipedia:List of content management systems](https://en.wikipedia.org/wiki/List_of_content_management_systems "wikipedia:List of content management systems").

*   **[Drupal](/index.php/Drupal "Drupal")** — An open source content management platform powering millions of websites and applications. It is built, used, and supported by an active and diverse community of people around the world.

	[http://drupal.org/](http://drupal.org/) || [drupal](https://www.archlinux.org/packages/?name=drupal)

*   **[Ghost](/index.php/Ghost "Ghost")** — Blogging platform written in JavaScript and distributed under the MIT License, designed to simplify the process of online publishing for individual bloggers as well as online publications.

	[https://ghost.org/](https://ghost.org/) || [ghost](https://aur.archlinux.org/packages/ghost/)

*   **Hexo** — A fast, simple & powerful blog framework, powered by Node.js.

	[http://hexo.io](http://hexo.io) || [nodejs-hexo](https://aur.archlinux.org/packages/nodejs-hexo/)

*   **[Jekyll](/index.php/Jekyll "Jekyll")** — A static blog engine, written in Ruby, which supports Markdown, textile and other formats.

	[http://jekyllrb.com/](http://jekyllrb.com/) || [ruby-jekyll](https://aur.archlinux.org/packages/ruby-jekyll/)

*   **Nanoblogger** — A small weblog engine written in Bash for the command line. It uses common UNIX tools such as cat, grep, and sed to create static HTML content. It is not mantained anymore.

	[http://nanoblogger.sourceforge.net/](http://nanoblogger.sourceforge.net/) || [nanoblogger](https://www.archlinux.org/packages/?name=nanoblogger)

*   **Pelican** — A static site generator, powered by Python.

	[http://docs.getpelican.com/en/3.5.0/](http://docs.getpelican.com/en/3.5.0/) || [pelican](https://www.archlinux.org/packages/?name=pelican)

*   **[Wordpress](/index.php/Wordpress "Wordpress")** — An easy to setup and administer FLOSS content management system featuring a strong and vibrant community with thousands of plugins and themes.

	[http://wordpress.org/](http://wordpress.org/) || [wordpress](https://www.archlinux.org/packages/?name=wordpress)

#### 微博客户端

See also [Wikipedia:List of Twitter services and applications](https://en.wikipedia.org/wiki/List_of_Twitter_services_and_applications "wikipedia:List of Twitter services and applications").

*   **wecase** — A Sina Weibo Client Focusing on Linux.

	[https://github.com/WeCase/WeCase](https://github.com/WeCase/WeCase) || [wecase](https://aur.archlinux.org/packages/wecase/)

*   **Birdie** — A beautiful Twitter client for GNU/Linux, currently [under active development](http://www.birdieapp.eu/2014/10/26/birdie-2-status.html).

	[http://birdieapp.github.io/](http://birdieapp.github.io/) || [birdie](https://aur.archlinux.org/packages/birdie/)

*   **Choqok** — Microblogging client for KDE that supports Twitter.com, Pump.io, GNU social and opendesktop.org services.

	[http://choqok.gnufolks.org/](http://choqok.gnufolks.org/) || [choqok](https://www.archlinux.org/packages/?name=choqok)

*   **Corebird** — Native Gtk+ Twitter client for the Linux desktop.

	[http://corebird.baedert.org/](http://corebird.baedert.org/) || [corebird-git](https://aur.archlinux.org/packages/corebird-git/)

*   **[Gwibber](https://en.wikipedia.org/wiki/Gwibber "wikipedia:Gwibber")** — GTK-based microblogging client with support for Facebook, Identi.ca, Twitter, Flickr, Foursquare, Sina and Sohu.

	[http://gwibber.com/](http://gwibber.com/) || [gwibber](https://aur.archlinux.org/packages/gwibber/)

*   **[Hotot](https://en.wikipedia.org/wiki/Hotot_(program) "wikipedia:Hotot (program)")** — Lightweight and open source microblogging client with support for Twitter and Identi.ca and integration with various image sharing services and URL shorteners [(discontinued)](http://hotot.org/).

	[http://hotot.org](http://hotot.org) || [hotot](https://aur.archlinux.org/packages/hotot/)

*   **Pino** — Simple and fast client for Twitter and Identi.ca written in [Vala](https://en.wikipedia.org/wiki/Vala_(programming_language) "wikipedia:Vala (programming language)").

	[http://pino-app.appspot.com/](http://pino-app.appspot.com/) || [pino](https://aur.archlinux.org/packages/pino/)

*   **Polly** — Linux Twitter client designed for multiple columns of multiple accounts.

	[https://launchpad.net/polly/](https://launchpad.net/polly/) || [polly](https://aur.archlinux.org/packages/polly/)

*   **Qwit** — Cross-platform client for Twitter using the Qt toolkit.

	[http://code.google.com/p/qwit/](http://code.google.com/p/qwit/) || [qwit](https://aur.archlinux.org/packages/qwit/)

*   **ttytter** — Easily scriptable twitter client written in Perl.

	[http://www.floodgap.com/software/ttytter/](http://www.floodgap.com/software/ttytter/) || [ttytter](https://aur.archlinux.org/packages/ttytter/)

*   **Turpial** — Multi-interface Twitter client written in Python.

	[http://turpial.org.ve/](http://turpial.org.ve/) || [turpial-git](https://aur.archlinux.org/packages/turpial-git/)

*   **tyrs** — Simple client for Twitter and Identi.ca supporting virtually all its features with nice console UI (unmaintained).

	[http://tyrs.nicosphere.net/](http://tyrs.nicosphere.net/)  || [tyrs](https://aur.archlinux.org/packages/tyrs/)

*   **turses** — Twitter client for the console based off [tyrs](https://aur.archlinux.org/packages/tyrs/) with major improvements.

	[http://turses.rtfd.org/](http://turses.rtfd.org/) || [turses](https://aur.archlinux.org/packages/turses/)

### 网络剪贴板

『网络剪贴板』经常被用来上传必要的信息，以方便用户在 IRC 频道向他人求助。目前『网络剪贴板』服务均支持文本 (e.g. [sprunge.org](http://sprunge.us/), [pastie.org](http://pastie.org/), [codepad.org](http://codepad.org/)) 和图片 (e.g. [imgur.com](http://imgur.com/), [picpaste.com](http://picpaste.com/))『网络剪贴板』客户端大多允许您直接通过 CLI 上传，无需依靠网络浏览器。

**Tip:** 可直接用 curl 上传 sprunge 网站： `<command> | curl -F 'sprunge=<-' http://sprunge.us` [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh/wiki)（一个用来配置 [Zsh (简体中文)](/index.php/Zsh_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Zsh (简体中文)") 的工具）也提供了一个 [sprunge 插件](https://github.com/robbyrussell/oh-my-zsh/wiki/Usage-of-the-%22sprunge%22-command)。

*   **Elmer** — 和 wgetpaste 和 curlpaste 相似，但用 Perl 写成且可调用 wget 或 curl，网站： [codepad.org](http://codepad.org/), [rafb.me](http://rafb.me/), [sprunge.us](http://sprunge.us/), [ompldr.org](http://ompldr.org/).

	[https://github.com/sudokode/elmer](https://github.com/sudokode/elmer) || [elmer](https://aur.archlinux.org/packages/elmer/)

*   **Fb-client** — [paste.xinu.at](http://paste.xinu.at/) 专用客户端。

	[http://paste.xinu.at](http://paste.xinu.at) || [fb-client](https://www.archlinux.org/packages/?name=fb-client)=

*   **Gist** — [gist.github.com](https://gist.github.com/) 专用命令行界面客户端。

	[http://github.com/defunkt/gist](http://github.com/defunkt/gist) || [gist](https://www.archlinux.org/packages/?name=gist)

*   **Haste** — 用 Haskell 写成的独特客户端. 网站： [hpaste.org](http://hpaste.org/), [paste2.org](http://paste2.org/), [pastebin.com](http://pastebin.com/) and others.

	[http://hackage.haskell.org/package/haste](http://hackage.haskell.org/package/haste) || [ruby-haste](https://aur.archlinux.org/packages/ruby-haste/) [ruby-haste-git](https://aur.archlinux.org/packages/ruby-haste-git/)

*   **Hg-paste** — 网站： [dpaste.com](http://dpaste.com/) and [dpaste.org](http://dpaste.org/).

	[http://bitbucket.org/sjl/hg-paste](http://bitbucket.org/sjl/hg-paste) || [hg-paste](https://aur.archlinux.org/packages/hg-paste/)

*   **imgur** — 可上传图片到 [imgur.com](http://imgur.com) 的客户端。

	[http://imgur.com/apps](http://imgur.com/apps) || [imgur](https://aur.archlinux.org/packages/imgur/)

*   **Ix** — [ix.io](http://ix.io) 专用客户端。

	[http://ix.io](http://ix.io) || [ix](https://aur.archlinux.org/packages/ix/)

*   **Npaste-client** — [npaste.de](http://npaste.de/) 专用客户端。

	[http://npaste.de](http://npaste.de) || [npaste-client](https://aur.archlinux.org/packages/npaste-client/)

*   **Pastebinit** — 相当小巧的 Python 脚本，网站： [pastie.org](http://pastie.org/), [paste.kde.org](http://paste.kde.org/), [paste.debian.net](http://paste.debian.net/), [paste.ubuntu.com](http://paste.ubuntu.com/) 以及其他 (可用 `pastebinit -l` 来查询).

	[http://launchpad.net/pastebinit](http://launchpad.net/pastebinit) || [pastebinit](https://www.archlinux.org/packages/?name=pastebinit)

*   **Uppity** — 有姿态的客户端。

	[https://github.com/Kiwi/Uppity](https://github.com/Kiwi/Uppity) || [uppity-git](https://aur.archlinux.org/packages/uppity-git/)

*   **Vim-gist** — Vim 插件，针对 [gist.github.com](https://gist.github.com/).

	[http://www.vim.org/scripts/script.php?script_id=2423](http://www.vim.org/scripts/script.php?script_id=2423) || [vim-gist](https://aur.archlinux.org/packages/vim-gist/)

*   **Vim-paster** — Vim 插件，用 curl 自动上传到某服务器端

	[http://eugeneciurana.com/site.php?page=tools](http://eugeneciurana.com/site.php?page=tools) || [vim-paster](https://aur.archlinux.org/packages/vim-paster/)

*   **Wgetpaste** — Bash 脚本，能自动上传到以下『网络剪贴板』网站： [pastebin.ca](http://pastebin.ca/), [codepad.org](http://codepad.org/), [dpaste.com](http://dpaste.com/) 和 [pastebin.osuosl.org](http://pastebin.osuosl.org/).

	[http://wgetpaste.zlin.dk/](http://wgetpaste.zlin.dk/) || [wgetpaste](https://www.archlinux.org/packages/?name=wgetpaste)

### 比特币

更多信息参见: [Bitcoin](/index.php/Bitcoin "Bitcoin").

*   **Armory** — 一个带有很多特性的比特币客户端, 例如对多种钱包的支持，导入keys和备份.

	[https://github.com/etotheipi/BitcoinArmory](https://github.com/etotheipi/BitcoinArmory) || [armory-git](https://aur.archlinux.org/packages/armory-git/)

*   **[Bitcoin](/index.php/Bitcoin "Bitcoin")** — 一种管理 p2p 现金比特币的正式工具.

	[http://bitcoin.org/](http://bitcoin.org/) || [bitcoin-daemon](https://www.archlinux.org/packages/?name=bitcoin-daemon) [bitcoin-qt](https://www.archlinux.org/packages/?name=bitcoin-qt)

*   **Electrum** — An easy to use Bitcoin client.

	[http://electrum.org/](http://electrum.org/) || [electrum](https://www.archlinux.org/packages/?name=electrum)

*   **MultiBit** — A lightweight Bitcoin desktop client powered by the BitCoinJ library.

	[https://multibit.org/](https://multibit.org/) || [multibit](https://www.archlinux.org/packages/?name=multibit)

### Surveying

*   **[LimeSurvey](https://en.wikipedia.org/wiki/LimeSurvey "wikipedia:LimeSurvey")** — An open source on-line survey application. As a web server-based software it enables users to develop and publish on-line surveys, and collect responses, with no programming.

	[https://www.limesurvey.org/](https://www.limesurvey.org/) || [limesurvey](https://aur.archlinux.org/packages/limesurvey/)

## 多媒体

### 解码器

See the main article: [Codecs](/index.php/Codecs "Codecs").

### 图像

#### 图像查看

See also [Wikipedia:Comparison of image viewers](https://en.wikipedia.org/wiki/Comparison_of_image_viewers "wikipedia:Comparison of image viewers").

##### 命令行

*   **fbi** — Image viewer for the linux framebuffer console.

	[https://www.kraxel.org/blog/linux/fbida/](https://www.kraxel.org/blog/linux/fbida/) || [fbida](https://www.archlinux.org/packages/?name=fbida)

*   **fbv** — framebuffer 图像查看器

	[http://s-tech.elsat.net.pl/fbv/](http://s-tech.elsat.net.pl/fbv/) || [fbv](https://www.archlinux.org/packages/?name=fbv)

*   **fim** — 基于fbi的，可定制的，支持脚本Frambuffer图像查看器

	[http://www.autistici.org/dezperado/](http://www.autistici.org/dezperado/) || [fim](https://aur.archlinux.org/packages/fim/)

*   **jfbview** — Framebuffer PDF and image viewer based on Imlib2\. Features include Vim-like controls, rotation and zoom, zoom-to-fit, and fast multi-threaded rendering.

	[http://seasonofcode.com/pages/jfbview.html](http://seasonofcode.com/pages/jfbview.html) || [jfbview](https://aur.archlinux.org/packages/jfbview/)

##### 图形环境

*   **[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")** — Image viewing and cataloging program, which is a part of the GNOME desktop environment.

	[http://projects.gnome.org/eog/](http://projects.gnome.org/eog/) || [eog](https://www.archlinux.org/packages/?name=eog)

*   **QIV** — 小巧快速的 gdk/Imlib 图像查看器

	[http://spiegl.de/qiv/](http://spiegl.de/qiv/) || [qiv](https://www.archlinux.org/packages/?name=qiv)

*   **Viewnior** — Minimalistic GTK2 viewer featuring support for flip, rotate, animations and configurable mouse actions

	[https://xsisqox.github.com/Viewnior/about.html](https://xsisqox.github.com/Viewnior/about.html) || [viewnior](https://www.archlinux.org/packages/?name=viewnior)

*   **Eye of MATE** — Simple graphics viewer for the MATE desktop.

	[https://github.com/mate-desktop/eom](https://github.com/mate-desktop/eom) || [eom](https://www.archlinux.org/packages/?name=eom)

*   **[Feh](/index.php/Feh "Feh")** — 使用imlib2的轻量级图像查看器

	[http://linuxbrit.co.uk/feh/](http://linuxbrit.co.uk/feh/) || [feh](https://www.archlinux.org/packages/?name=feh)

*   **meh** — meh is a small, simple, super fast image viewer using raw XLib.

	[http://www.johnhawthorn.com/meh/](http://www.johnhawthorn.com/meh/) || [meh](https://aur.archlinux.org/packages/meh/)

```
**GalaPix** — 基于OpenGL的图像查看器，提供同时显示图像集并形成缩略图的功能

```

	[http://code.google.com/p/galapix/](http://code.google.com/p/galapix/) || [galapix](https://aur.archlinux.org/packages/galapix/)

*   **[Geeqie](https://en.wikipedia.org/wiki/Geeqie "wikipedia:Geeqie")** — Image browser and viewer (fork of GQview) that adds additional functionality such as support for RAW files.

	[http://geeqie.sourceforge.net/](http://geeqie.sourceforge.net/) || [geeqie](https://www.archlinux.org/packages/?name=geeqie)

*   **Gimmage** — Gtkmm image viewer.

	[http://gimmage.berlios.de/](http://gimmage.berlios.de/) || [gimmage](https://www.archlinux.org/packages/?name=gimmage)

*   **GPicView** — Simple and fast image viewer for X, which is part of the [LXDE](/index.php/LXDE "LXDE") desktop.

	[http://lxde.sourceforge.net/gpicview/](http://lxde.sourceforge.net/gpicview/) || [gpicview](https://www.archlinux.org/packages/?name=gpicview)

*   **[GQview](https://en.wikipedia.org/wiki/GQview "wikipedia:GQview")** — Image browser that features single click access to view images and move around the directory tree

	[http://gqview.sourceforge.net/](http://gqview.sourceforge.net/) || [gqview-devel](https://aur.archlinux.org/packages/gqview-devel/)

*   **[gThumb](https://en.wikipedia.org/wiki/GThumb "wikipedia:GThumb")** — Image viewer for the GNOME desktop.

	[https://live.gnome.org/gthumb](https://live.gnome.org/gthumb) || [gthumb](https://www.archlinux.org/packages/?name=gthumb)

*   **[Gwenview](https://en.wikipedia.org/wiki/Gwenview "wikipedia:Gwenview")** — Fast and easy to use image viewer for the KDE desktop.

	[http://gwenview.sourceforge.net/](http://gwenview.sourceforge.net/) || [gwenview](https://www.archlinux.org/packages/?name=gwenview)

*   **Mirage** — PyGTK image viewer featuring support for crop and resize, custom actions and a thumbnail panel.

	[http://mirageiv.berlios.de](http://mirageiv.berlios.de) || [mirage](https://www.archlinux.org/packages/?name=mirage)

*   **nomacs** — Free (GPLv3) Qt image viewer for many operating systems. It is feature-rich but starts fast and can be configured to show additional widgets or only the image.

	[http://www.nomacs.org/](http://www.nomacs.org/) || [nomacs](https://www.archlinux.org/packages/?name=nomacs)

*   **Phototonic** — Fast and functional image viewer and organizer (Qt).

	[https://github.com/oferkv/phototonic](https://github.com/oferkv/phototonic) || [phototonic](https://aur.archlinux.org/packages/phototonic/)

*   **PhotoQt** — Fast and highly configurable image viewer with a simple and nice interface.

	[http://photoqt.org/](http://photoqt.org/) || [photoqt](https://aur.archlinux.org/packages/photoqt/)

*   **[Picasa](https://en.wikipedia.org/wiki/Picasa "wikipedia:Picasa")** — Image organizer and viewer from Google that has editing capabilities and integration with the photo-sharing website.

	[http://picasa.google.com/](http://picasa.google.com/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=picasa)</small>

*   **Quick Image Viewer** — Very small and fast image viewer based on GTK+ and imlib2.

	[http://spiegl.de/qiv/](http://spiegl.de/qiv/) || [qiv](https://www.archlinux.org/packages/?name=qiv)

*   **Ristretto** — Xfce 桌面环境下快速的轻量级图像查看器

	[http://goodies.xfce.org/projects/applications/ristretto](http://goodies.xfce.org/projects/applications/ristretto) || [ristretto](https://www.archlinux.org/packages/?name=ristretto)

*   **Shotwell** — A digital photo organizer designed for the GNOME desktop environment

	[https://wiki.gnome.org/Apps/Shotwell](https://wiki.gnome.org/Apps/Shotwell) || [shotwell](https://www.archlinux.org/packages/?name=shotwell)

*   **[Simple Viewer GL](/index.php?title=Simple_Viewer_GL&action=edit&redlink=1 "Simple Viewer GL (page does not exist)")** — Simple image viewer using OpenGL, it has few dependencies.

	[simpleviewergl-git](https://aur.archlinux.org/packages/simpleviewergl-git/) || [simpleviewergl-git](https://aur.archlinux.org/packages/simpleviewergl-git/)

*   **SXIV** — 简单的 X 图像查看器; works well with tiling window managers, uses imlib2

	[https://github.com/muennich/sxiv](https://github.com/muennich/sxiv) || [sxiv](https://www.archlinux.org/packages/?name=sxiv)

*   **[Viewnior](https://en.wikipedia.org/wiki/Viewnior "wikipedia:Viewnior")** — Minimalistic GTK+ image viewer featuring support for flipping, rotating, animations and configurable mouse actions.

	[http://xsisqox.github.com/Viewnior/](http://xsisqox.github.com/Viewnior/) || [viewnior](https://www.archlinux.org/packages/?name=viewnior)

*   **Xloadimage** — 经典的 X 图像查看器

	[http://web.archive.org/web/19981207030422/http://world.std.com/~jimf/xloadimage.html](http://web.archive.org/web/19981207030422/http://world.std.com/~jimf/xloadimage.html) || [xloadimage](https://www.archlinux.org/packages/?name=xloadimage)

*   **XnView MP** — 高效的图像查看，浏览，转换器

	[http://www.xnview.com/en/index.html](http://www.xnview.com/en/index.html) || [xnviewmp](https://aur.archlinux.org/packages/xnviewmp/)

*   **[xv](https://en.wikipedia.org/wiki/Xv_(software) "wikipedia:Xv (software)")** — Shareware program written by John Bradley to display and modify digital images under the X Window System.

	[http://www.trilon.com/xv/](http://www.trilon.com/xv/) || [xv](https://aur.archlinux.org/packages/xv/)

#### 图形和图像处理

##### 位图编辑器

*   **[GIMP](https://en.wikipedia.org/wiki/GIMP "wikipedia:GIMP")** — GIMP 是 [GNU](/index.php/GNU "GNU") Image Manipulation Program（GNU图像处理程序）的缩写。成立于20世纪90年代中期的GIMP是一个与 Adobe Photoshop 相似的图像编辑套件。Arch Linux 软件仓库拥有数量众多的GIMP插件和辅助工具。可以使用如下命令来搜索它们：

```
pacman -Ss gimp

```

还有数量众多的软件包在 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")。您也许会有兴趣阅读 [CMYK support in The GIMP](/index.php/CMYK_support_in_The_GIMP "CMYK support in The GIMP")

	[http://www.gimp.org/](http://www.gimp.org/) || [gimp](https://www.archlinux.org/packages/?name=gimp)

*   **KolourPaint** — KDE 下免费、快速的图像编辑器，与Windows 7系统之前微软画图软件相似，但是添加了一些如支持透明度等的新特征

	[http://kolourpaint.org](http://kolourpaint.org) || [kdegraphics-kolourpaint](https://www.archlinux.org/packages/?name=kdegraphics-kolourpaint)

*   **mtPaint** — 致力于创建色彩索引的调色板图像以及像素画的图像编辑器

	[http://mtpaint.sourceforge.net/](http://mtpaint.sourceforge.net/) || [mtpaint](https://www.archlinux.org/packages/?name=mtpaint)

*   **darktable** — 具有完整的照片工作流程并且擅长于RAW格式处理的软件

	[http://www.darktable.org//](http://www.darktable.org//) || [darktable](https://www.archlinux.org/packages/?name=darktable)

*   **MyPaint** — 数码绘画者的自由图像工具

	[http://mypaint.intilinux.com](http://mypaint.intilinux.com) || [mypaint](https://www.archlinux.org/packages/?name=mypaint)

*   **Krita (瑞典语言版本中称为crayon)** — 基于KDE平台和Koffice库创建的数字绘画设计软件

	[http://krita.org/](http://krita.org/) || [calligra-krita](https://www.archlinux.org/packages/?name=calligra-krita)

*   **Nathive** — “没用的图像编辑器”（"the usable image editor"）, 一个基于Gnome设计，具有圆滑的学习曲线，着眼于实用性的图像编辑软件

	[http://www.nathive.org/](http://www.nathive.org/) || [nathive](https://aur.archlinux.org/packages/nathive/)

*   **[ImageMagick](https://en.wikipedia.org/wiki/ImageMagick "wikipedia:ImageMagick")** — ImageMagick 是一个命令行图像处理程序。 它因为其支持超过100多种格式的精确格式转换而知名。它的API使得它非常易于融入脚本之中，而且它也被用作很多软件的后台处理器——比如创建MediaWiki的图片缩略图。

	[http://www.imagemagick.org/script/index.php](http://www.imagemagick.org/script/index.php) || [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)

*   **[GraphicsMagick](https://en.wikipedia.org/wiki/GraphicsMagick "wikipedia:GraphicsMagick")** — GraphicsMagick 于2002年基于ImageMagick的设计创建，继承了它的API和命令行稳定性。 而且它还支持多核CPU以增强性能，因为如此它被许多大型机构网站（如Flickr、etsy等）使用。

	[http://www.graphicsmagick.org/](http://www.graphicsmagick.org/) || [graphicsmagick](https://www.archlinux.org/packages/?name=graphicsmagick)

*   **[Shotwell](https://en.wikipedia.org/wiki/Shotwell_(software) "wikipedia:Shotwell (software)")** — Shotwell是一个图片管理软件。他只有简单的图像处理功能，比如：旋转、裁剪、色彩矫正和红眼移除等。它可以直接从数码相机中导入照片并且导出到设计媒体网站。

	[http://yorba.org/shotwell/](http://yorba.org/shotwell/) || [shotwell](https://www.archlinux.org/packages/?name=shotwell)

*   **[digiKam](https://en.wikipedia.org/wiki/digiKam "wikipedia:digiKam")** — digiKam是一个基于KDE的图像/照片管理器。借助插件架构，它内置了大量的图像处理功能。digiKam声称自己比其他很多的图像处理工具拥有更多的图像处理功能，包括RAW格式图像的导入和处理。

	[http://www.digikam.org/](http://www.digikam.org/) || [digikam](https://www.archlinux.org/packages/?name=digikam)

##### 矢量图处理 - 绘画

*   **[Inkscape](https://en.wikipedia.org/wiki/Inkscape "wikipedia:Inkscape")** — 一个开源的矢量图编辑器，功能类似于Illustrator、CorelDraw以及Xara X。它使用W3C标准可放大矢量图格式（SVG）。Inkscape支持众多的高级SVG功能（如标记、克隆、Alpha通道混合等）。并且具有一套认真设计的基于工作流程的界面。它可以很方便地编辑节点，执行复杂的路径操作，描绘位图等等等等。其开发者以其社区维护的开发方法致力于维护一个正在发展中的用户与开发者社区。

	[http://inkscape.org/](http://inkscape.org/) || [inkscape](https://www.archlinux.org/packages/?name=inkscape)

*   **Xara** — 一个高级矢量图软件。

	[http://www.xaraxtreme.org/](http://www.xaraxtreme.org/) || [xaralx](https://aur.archlinux.org/packages/xaralx/)

*   **Dia** — 一个基于GTK+的创意软件。

	[http://live.gnome.org/Dia](http://live.gnome.org/Dia) || [dia](https://www.archlinux.org/packages/?name=dia)

##### 矢量图处理 - CAD

See also [Wikipedia:List of computer-aided design editors](https://en.wikipedia.org/wiki/List_of_computer-aided_design_editors "wikipedia:List of computer-aided design editors").

*   **[BRL-CAD](https://en.wikipedia.org/wiki/BRL-CAD "wikipedia:BRL-CAD")** — Constructive solid geometry (CSG) solid modeling computer-aided design (CAD) system that includes an interactive geometry editor, ray tracing support for graphics rendering and geometric analysis, computer network distributed framebuffer support, scripting, image-processing and signal-processing tools.

	[http://brlcad.org/](http://brlcad.org/) || [brlcad](https://aur.archlinux.org/packages/brlcad/)

*   **DraftSight** — 专业级免费CAD软件。DraftSight让专业CAD用户、学生和教育工作者能够创建、编辑和查看DWG文件。 DraftSight适用于Windows®、Mac®和Linux环境。

	[http://www.3ds.com/cn/products/draftsight/download-draftsight](http://www.3ds.com/cn/products/draftsight/download-draftsight) || [Draftsight](https://aur.archlinux.org/packages/Draftsight/)

*   **[FreeCAD](https://en.wikipedia.org/wiki/FreeCAD "wikipedia:FreeCAD")** — CAD/CAE program, based on OpenCascade, Qt and Python with features such as macro recording, workbenches and the ability to run as server.

	[http://sourceforge.net/projects/free-cad/](http://sourceforge.net/projects/free-cad/) || [freecad](https://www.archlinux.org/packages/?name=freecad)

*   **LeoCAD** — CAD program for creating virtual LEGO models. It has an easy to use interface and currently includes over 6000 different pieces created by the LDraw community.

	[http://leocad.org](http://leocad.org) || [leocad](https://aur.archlinux.org/packages/leocad/)

*   **[LibreCAD](https://en.wikipedia.org/wiki/LibreCAD "wikipedia:LibreCAD")** — Powerful 2D CAD application based on Qt. It has been forked from QCad Community Edition.

	[http://www.librecad.org/](http://www.librecad.org/) || [librecad](https://www.archlinux.org/packages/?name=librecad)

*   **[OpenSCAD](https://en.wikipedia.org/wiki/OpenSCAD "wikipedia:OpenSCAD")** — Open source 2D/3D CAD using programmers approach.

	[http://www.openscad.org](http://www.openscad.org) || [openscad](https://www.archlinux.org/packages/?name=openscad) [openscad-git](https://aur.archlinux.org/packages/openscad-git/)

*   **[QCAD](https://en.wikipedia.org/wiki/QCad "wikipedia:QCad")** — Powerful 2D CAD application that began in 1999\. QCaD includes DFX standard file format and supports HPGL format.

	[http://www.qcad.org/](http://www.qcad.org/) || [qcad](https://www.archlinux.org/packages/?name=qcad)

*   **[VariCAD](https://en.wikipedia.org/wiki/VariCAD "wikipedia:VariCAD")** — 3D/2D CAD and mechanical engineering application which provides support for parameters and geometric constraints, tools for shells, pipelines, sheet metal unbending and crash tests, assembly support, mechanical part and symbol libraries, calculations, bills of materials, and more.

	[http://www.varicad.com/en/home/](http://www.varicad.com/en/home/) || [varicad](https://aur.archlinux.org/packages/varicad/)

##### 三维建模与渲染

See also [Wikipedia:Comparison of 3D computer graphics software](https://en.wikipedia.org/wiki/Comparison_of_3D_computer_graphics_software "wikipedia:Comparison of 3D computer graphics software").

*   **[Art of Illusion](https://en.wikipedia.org/wiki/Art_of_Illusion "wikipedia:Art of Illusion")** — 3D modeling and rendering studio written in Java.

	[http://www.artofillusion.org/](http://www.artofillusion.org/) || [aoi](https://aur.archlinux.org/packages/aoi/)

*   **[MakeHuman™](https://en.wikipedia.org/wiki/MakeHuman "wikipedia:MakeHuman")** — Parametrical modeling program for creating human bodies.

	[http://www.makehuman.org/](http://www.makehuman.org/) || [makehuman](https://aur.archlinux.org/packages/makehuman/)

*   **[POV-Ray](https://en.wikipedia.org/wiki/POV-Ray "wikipedia:POV-Ray")** — Script-based raytracer for creating 3D graphics.

	[http://www.povray.org/](http://www.povray.org/) || [povray](https://www.archlinux.org/packages/?name=povray)

*   **[Wings 3D](https://en.wikipedia.org/wiki/Wings3d "wikipedia:Wings3d")** — Advanced subdivision modeler that is both powerful and easy to use.

	[http://www.wings3d.com/](http://www.wings3d.com/) || [wings3d](https://www.archlinux.org/packages/?name=wings3d)

*   **Blender** — 一个全能的三维在图形创意工具。功能包括三维建模、材质设计、三维动画、后期合成等等功能。同时它也有大量的附加不定和工具扩展它的功能。[Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

另外可见:

*   *   [Blender homepage](http://www.blender.org/)
    *   [Blender Wiki](http://wiki.blender.org/index.php/Main_Page)
    *   [Blender walkthrough on wikibooks](http://en.wikibooks.org/wiki/Blender_3D)

	[http://www.blender.org/](http://www.blender.org/) || [blender](https://www.archlinux.org/packages/?name=blender)

#### 截取屏幕

See also: [Taking a screenshot](/index.php/Taking_a_screenshot "Taking a screenshot").

### 音频

#### 音频系统

See also [Wikipedia:Sound server](https://en.wikipedia.org/wiki/Sound_server "wikipedia:Sound server").

See the main article: [Sound system](/index.php/Sound_system "Sound system").

*   **wineasio** — Provides an ASIO to JACK driver for *wine*. ASIO is the most common Windows low-latency driver, so is commonly used in audio workstation programs.

	[http://sourceforge.net/projects/wineasio/](http://sourceforge.net/projects/wineasio/) || [wineasio](https://aur.archlinux.org/packages/wineasio/)

#### 音频播放器

See also [Wikipedia:Comparison of audio player software](https://en.wikipedia.org/wiki/Comparison_of_audio_player_software "wikipedia:Comparison of audio player software").

##### 音乐播放器守护进程和客户端 (Client)

*   **[Music Player Daemon](/index.php/Music_Player_Daemon "Music Player Daemon")** — 轻量、可伸缩音乐播放器，C/S结构，MPD 作为一个守护程序运行于后台， 管理播放列表和音乐数据库

	[http://mpd.wikia.com/wiki/Music_Player_Daemon_Wiki](http://mpd.wikia.com/wiki/Music_Player_Daemon_Wiki) || [mpd](https://www.archlinux.org/packages/?name=mpd)

*   [MPD客户端程序清单](/index.php/Music_Player_Daemon#Clients "Music Player Daemon")
*   **[XMMS2](https://en.wikipedia.org/wiki/XMMS2 "wikipedia:XMMS2")** — Complete rewrite of the popular music player.

	[https://xmms2.org](https://xmms2.org) || [xmms2](https://www.archlinux.org/packages/?name=xmms2)

##### 命令行

*   **[cmus](/index.php/Cmus "Cmus")** — Very feature-rich ncurses-based music player.

	[http://cmus.github.io/](http://cmus.github.io/) || [cmus](https://www.archlinux.org/packages/?name=cmus)

*   **Cplay** — Curses front-end for various audio players (ogg123, mpg123, mpg321, splay, madplay, and mikmod, xmp, and sox).

	[http://directory.fsf.org/wiki/Cplay](http://directory.fsf.org/wiki/Cplay) || [cplay](https://aur.archlinux.org/packages/cplay/)

*   **Herrie** — Minimalistic console-based music player with native AudioScrobbler support.

	[http://herrie.info/](http://herrie.info/) || [herrie](https://aur.archlinux.org/packages/herrie/)

*   **[MOC](/index.php/Moc "Moc")** — Ncurses console audio player with support for the MP3, OGG, and WAV formats.

	[http://moc.daper.net/](http://moc.daper.net/) || [moc](https://www.archlinux.org/packages/?name=moc)

*   **MPFC** — Gstreamer-based audio player with curses interface.

	[http://code.google.com/p/mpfc/](http://code.google.com/p/mpfc/) || [mpfc](https://aur.archlinux.org/packages/mpfc/)

*   **[mpg123](https://en.wikipedia.org/wiki/Mpg123 "wikipedia:Mpg123")** — Fast free MP3 console audio player for Linux, FreeBSD, Solaris, HP-UX and nearly all other UNIX systems (also decodes MP1 and MP2 files).

	[http://www.mpg123.org/](http://www.mpg123.org/) || [mpg123](https://www.archlinux.org/packages/?name=mpg123)

*   **[pianobar](/index.php/Pianobar "Pianobar")** — Console-based frontend for Pandora.

	[http://6xq.net/projects/pianobar/](http://6xq.net/projects/pianobar/) || [pianobar](https://www.archlinux.org/packages/?name=pianobar)

*   **PyTone** — Advanced music jukebox with a console interface.

	[http://www.luga.de/pytone/](http://www.luga.de/pytone/) || [pytone](https://aur.archlinux.org/packages/pytone/)

*   **shell-fm** — Console-based player for the streams provided by [last.fm](http://www.last.fm/).

	[https://github.com/jkramer/shell-fm/](https://github.com/jkramer/shell-fm/) || [shell-fm](https://aur.archlinux.org/packages/shell-fm/)

*   **[VLC](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")** — Highly portable multimedia player with ncurses interface module, and multimedia framework capable of reading most audio and video formats as well as DVDs, Audio CDs, VCDs, and various streaming protocols.

	[https://www.videolan.org/vlc/](https://www.videolan.org/vlc/) || [vlc](https://www.archlinux.org/packages/?name=vlc)

*   **whistle** — a curses-based commandline audio player.

	[https://github.com/ap0calypse/whistle/](https://github.com/ap0calypse/whistle/) || [whistle-git](https://aur.archlinux.org/packages/whistle-git/)

##### 图形环境

*   **[Amarok](/index.php/Amarok "Amarok")** — Mature Qt-based player known for its plethora of features.

	[http://amarok.kde.org/](http://amarok.kde.org/) || [amarok](https://www.archlinux.org/packages/?name=amarok)

*   **[aTunes](https://en.wikipedia.org/wiki/aTunes "wikipedia:aTunes")** — Audio player written in Java.

	[http://www.atunes.org/](http://www.atunes.org/) || [atunes](https://aur.archlinux.org/packages/atunes/)

*   **[Audacious](/index.php/Audacious "Audacious")** — [Winamp](https://en.wikipedia.org/wiki/Winamp "wikipedia:Winamp") clone like Beep and old XMMS versions.

	[http://audacious-media-player.org/](http://audacious-media-player.org/) || [audacious](https://www.archlinux.org/packages/?name=audacious)

*   **[Banshee](https://en.wikipedia.org/wiki/Banshee_(media_player) "wikipedia:Banshee (media player)")** — [iTunes](https://en.wikipedia.org/wiki/iTunes "wikipedia:iTunes") clone, built with GTK+ and [Mono](/index.php/Mono "Mono"), feature-rich and more actively developed.

	[http://banshee.fm/](http://banshee.fm/) || [banshee](https://aur.archlinux.org/packages/banshee/)

*   **[Clementine](https://en.wikipedia.org/wiki/Clementine_(software) "wikipedia:Clementine (software)")** — Amarok 1.4 clone, ported to Qt 4.

	[http://www.clementine-player.org/](http://www.clementine-player.org/) || [clementine](https://www.archlinux.org/packages/?name=clementine)

*   **Cuberok** — Music player and collection manager with a lightweight interface.

	[http://code.google.com/p/cuberok/](http://code.google.com/p/cuberok/) || [cuberok](https://aur.archlinux.org/packages/cuberok/)

*   **DeaDBeeF** — Light and fast music player with many features, no GNOME or KDE dependencies, supports console-only, as well as a GTK+ GUI, comes with many plugins, and has a metadata editor.

	[http://deadbeef.sourceforge.net/](http://deadbeef.sourceforge.net/) || [deadbeef](https://www.archlinux.org/packages/?name=deadbeef)

*   **[Exaile](/index.php/Exaile "Exaile")** — GTK+ clone of Amarok.

	[http://www.exaile.org/](http://www.exaile.org/) || [exaile](https://aur.archlinux.org/packages/exaile/)

*   **gmusicbrowser** — Open-source jukebox for large collections of MP3/OGG/FLAC files.

	[http://gmusicbrowser.org/](http://gmusicbrowser.org/) || [gmusicbrowser](https://aur.archlinux.org/packages/gmusicbrowser/)

*   **GNOME Music** — Music is the new GNOME music playing application. It aims to combine an elegant and immersive browsing experience with simple and straightforward controls.

	[https://wiki.gnome.org/Apps/Music](https://wiki.gnome.org/Apps/Music) || [gnome-music](https://www.archlinux.org/packages/?name=gnome-music)

*   **Goggles Music Manager** — Music collection manager and player that automatically categorizes your music, supports gapless playback, features easy tag editing, and internet radio support. Uses the [Fox toolkit](https://en.wikipedia.org/wiki/Fox_toolkit "wikipedia:Fox toolkit").

	[http://gogglesmm.github.io/](http://gogglesmm.github.io/) || [gogglesmm](https://www.archlinux.org/packages/?name=gogglesmm)

*   **Guayadeque** — Full featured media player that can easily manage large collections and uses the GStreamer media framework.

	[http://guayadeque.org/](http://guayadeque.org/) || [guayadeque](https://aur.archlinux.org/packages/guayadeque/)

*   **[JuK](https://en.wikipedia.org/wiki/JuK "wikipedia:JuK")** — JuK is an audio jukebox application, supporting collections of MP3, Ogg Vorbis, and FLAC audio files.

	[https://www.kde.org/applications/multimedia/juk/](https://www.kde.org/applications/multimedia/juk/) || [kdemultimedia-juk](https://www.archlinux.org/packages/?name=kdemultimedia-juk)

*   **Listen** — Listen is a Music player and management for GNOME written in python.

	[https://launchpad.net/listen](https://launchpad.net/listen) || [listen](https://aur.archlinux.org/packages/listen/)

*   **LXMusic** — A minimalist xmms2-based music player.

	[http://wiki.lxde.org/en/LXMusic](http://wiki.lxde.org/en/LXMusic) || [lxmusic](https://www.archlinux.org/packages/?name=lxmusic)

*   **Miam-player** — Cross-platform open source music player.

	[http://miam-player.org/](http://miam-player.org/) || [miam-player](https://aur.archlinux.org/packages/miam-player/)

*   **[Nightingale](https://en.wikipedia.org/wiki/Nightingale_(software) "wikipedia:Nightingale (software)")** — Open source clone of iTunes-based on [Songbird](https://en.wikipedia.org/wiki/Songbird_(software) "wikipedia:Songbird (software)"), that uses Mozilla technologies and the GStreamer framework.

	[http://getnightingale.com/](http://getnightingale.com/) || [nightingale](https://aur.archlinux.org/packages/nightingale/)

*   **Noise** — Simple, fast, and good looking music player.

	[https://launchpad.net/noise](https://launchpad.net/noise) || [noise](https://www.archlinux.org/packages/?name=noise)

*   **Nuvola Player** — Integrated Google Music, Grooveshark, 8tracks and Hype Machine player.

	[http://nuvolaplayer.fenryxo.cz/](http://nuvolaplayer.fenryxo.cz/) || [nuvolaplayer](https://aur.archlinux.org/packages/nuvolaplayer/)

*   **Potamus** — Lightweight, intuitive GTK+ audio player with an emphasis on high audio quality.

	[http://offog.org/code/potamus.html](http://offog.org/code/potamus.html) || [potamus](https://aur.archlinux.org/packages/potamus/)

*   **Pragha** — GTK+ music manager. (fork of the Consonance Music Manager)

	[https://pragha-music-player.github.io/](https://pragha-music-player.github.io/) || [pragha](https://www.archlinux.org/packages/?name=pragha)

*   **Qmmp** — Qt-based multimedia player with a user interface that is similar to Winamp or XMMS.

	[http://qmmp.ylsoftware.com/](http://qmmp.ylsoftware.com/) || [qmmp](https://www.archlinux.org/packages/?name=qmmp)

*   **[Quod Libet](https://en.wikipedia.org/wiki/Quod_Libet_(software) "wikipedia:Quod Libet (software)")** — Audio player written with PyGTK and GStreamer with support for regular expressions in playlists.

	[http://code.google.com/p/quodlibet/](http://code.google.com/p/quodlibet/) || [quodlibet](https://www.archlinux.org/packages/?name=quodlibet)

*   **[Rhythmbox](https://en.wikipedia.org/wiki/Rhythmbox "wikipedia:Rhythmbox")** — GTK+ clone of iTunes, used by default in GNOME.

	[http://projects.gnome.org/rhythmbox/](http://projects.gnome.org/rhythmbox/) || [rhythmbox](https://www.archlinux.org/packages/?name=rhythmbox)

*   **[Spotify](/index.php/Spotify "Spotify")** — Proprietary music streaming service. It supports local playback and streaming from Spotify's vast library (requires a free account).

	[http://www.spotify.com/](http://www.spotify.com/) || [spotify](https://aur.archlinux.org/packages/spotify/)

*   **[SpotCommander](/index.php/SpotCommander "SpotCommander")** — A remote control for Spotify, optimized for mobile devices. It works on any device with a modern browser, and it's free and open source.

	[http://olejon.github.io/spotcommander/](http://olejon.github.io/spotcommander/) || [spotcommander](https://aur.archlinux.org/packages/spotcommander/)

*   **Tomahawk** — Music player application written in C++/Qt. It decouples the name of the song from the source it was shared from - and fulfills the request using all of your available sources.

	[http://www.tomahawk-player.org/](http://www.tomahawk-player.org/) || [tomahawk](https://aur.archlinux.org/packages/tomahawk/)

*   **[VLC](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")** — Highly portable multimedia player and multimedia framework capable of reading most audio and video formats as well as DVDs, Audio CDs, VCDs, and various streaming protocols.

	[https://www.videolan.org/vlc/](https://www.videolan.org/vlc/) || [vlc](https://www.archlinux.org/packages/?name=vlc)

*   **[XMMS](https://en.wikipedia.org/wiki/XMMS "wikipedia:XMMS")** — Skinnable GTK+ standalone media player similar to Winamp.

	[http://legacy.xmms2.org/](http://legacy.xmms2.org/) || [xmms](https://aur.archlinux.org/packages/xmms/)

#### 音响管理

*   **GVolWheel** — An audio mixer which lets you control the volume through a tray icon.

	[http://sourceforge.net/projects/gvolwheel/](http://sourceforge.net/projects/gvolwheel/) || [gvolwheel](https://aur.archlinux.org/packages/gvolwheel/)

*   **GVTray** — A master volume mixer for the system tray.

	[http://code.google.com/p/gtk-tray-utils/](http://code.google.com/p/gtk-tray-utils/) || [gvtray](https://aur.archlinux.org/packages/gvtray/)

*   **pa-applet** — PulseAudio system tray applet with volume bar.

	[https://github.com/fernandotcl/pa-applet](https://github.com/fernandotcl/pa-applet) || [pa-applet-git](https://aur.archlinux.org/packages/pa-applet-git/)

*   **PNMixer** — A fork of Obmixer. It has many new features such as ALSA channel selection, connect/disconnect detection, shortcuts, etc.

	[https://github.com/nicklan/pnmixer/wiki](https://github.com/nicklan/pnmixer/wiki) || [pnmixer](https://aur.archlinux.org/packages/pnmixer/)

*   **Volctl** — Per-application volume control for GNU/Linux desktops.

	[https://buzz.github.io/volctl/](https://buzz.github.io/volctl/) || [volctl](https://aur.archlinux.org/packages/volctl/)

*   **Volnoti** — Volnoti is a lightweight volume notification daemon for GNU/Linux and other POSIX operating systems.

	[https://github.com/davidbrazdil/volnoti](https://github.com/davidbrazdil/volnoti) || [volnoti](https://aur.archlinux.org/packages/volnoti/)

*   **Volti** — A GTK application for controlling audio volume from system tray with an internal mixer and support for multimedia keys that uses only ALSA.

	[http://code.google.com/p/volti/](http://code.google.com/p/volti/) || [volti](https://aur.archlinux.org/packages/volti/)

*   **VolumeIcon** — Another volume control for your system tray with channel selection, themes and an external mixer.

	[http://softwarebakery.com/maato/volumeicon.html](http://softwarebakery.com/maato/volumeicon.html) || [volumeicon](https://www.archlinux.org/packages/?name=volumeicon)

*   **VolWheel** — A little application which lets you control the sound volume easily through a tray icon you can scroll on.

	[http://oliwer.net/b/volwheel.html](http://oliwer.net/b/volwheel.html) || [volwheel](https://www.archlinux.org/packages/?name=volwheel)

#### 提取 CD

See [Optical disc drive#CD](/index.php/Optical_disc_drive#CD "Optical disc drive").

#### 可视化

*   **[ProjectM](https://en.wikipedia.org/wiki/MilkDrop "wikipedia:MilkDrop")** — Music visualizer which uses 3D accelerated iterative image-based rendering.

	[http://projectm.sourceforge.net/](http://projectm.sourceforge.net/) || [projectm](https://www.archlinux.org/packages/?name=projectm)

*   **[VSXu](https://en.wikipedia.org/wiki/VSXu "wikipedia:VSXu")** — Free to use program that lets you create and perform real-time audio visual presets.

	[http://www.vsxu.com/](http://www.vsxu.com/) || [vsxu](https://aur.archlinux.org/packages/vsxu/)

#### 音频标签编辑器

*   **Audio Tag Tool** — Tool to edit tags in MP3 and Ogg Vorbis files.

	[http://tagtool.sourceforge.net/](http://tagtool.sourceforge.net/) || [tagtool](https://aur.archlinux.org/packages/tagtool/)

*   **Cowbell** — Elegant music organizer that supports many audio formats including MP3, Ogg/FLAC, and MusePack.

	[http://more-cowbell.org/](http://more-cowbell.org/) || [cowbell](https://aur.archlinux.org/packages/cowbell/)

*   **[EasyTag](https://en.wikipedia.org/wiki/EasyTag "wikipedia:EasyTag")** — Utility for viewing, editing and writing ID3 tags of your MP3 files.

	[http://easytag.sourceforge.net/](http://easytag.sourceforge.net/) || [easytag](https://www.archlinux.org/packages/?name=easytag)

*   **[Ex Falso](https://en.wikipedia.org/wiki/Ex_Falso_(software) "wikipedia:Ex Falso (software)")** — Cross-platform free and open source audio tag editor and library organizer.

	[http://code.google.com/p/quodlibet/](http://code.google.com/p/quodlibet/) || [exfalso](https://aur.archlinux.org/packages/exfalso/)

*   **ID3 Mass Tagger** — Command-line utility to edit ID3 1.x and 2.x tags.

	[http://squell.github.io/id3/](http://squell.github.io/id3/) || [id3](https://www.archlinux.org/packages/?name=id3)

*   **Kid3** — MP3, Ogg/Vorbis, FLAC, MPC, MP4/AAC, MP2, Speex, TrueAudio, WavPack, WMA, WAV and AIFF files tag editor.

	[http://kid3.sourceforge.net/](http://kid3.sourceforge.net/) || [kid3](https://www.archlinux.org/packages/?name=kid3)

*   **MP3Info** — MP3 technical info viewer and ID3 1.x tag editor.

	[http://ibiblio.org/mp3info/](http://ibiblio.org/mp3info/) || [mp3info](https://www.archlinux.org/packages/?name=mp3info)

*   **[MusicBrainz Picard](https://en.wikipedia.org/wiki/MusicBrainz_Picard "wikipedia:MusicBrainz Picard")** — Cross-platform audio tag editor written in Python (the official MusicBrainz tagger).

	[http://musicbrainz.org/doc/MusicBrainz_Picard](http://musicbrainz.org/doc/MusicBrainz_Picard) || [picard](https://www.archlinux.org/packages/?name=picard)

*   **[Puddletag](https://en.wikipedia.org/wiki/Puddletag "wikipedia:Puddletag")** — Replacement for the famous MP3tag for Windows.

	[http://puddletag.sourceforge.net/](http://puddletag.sourceforge.net/) || [puddletag](https://www.archlinux.org/packages/?name=puddletag)

*   **taffy** — Simple command-line tag editor for many audio formats.

	[http://github.com/jangler/taffy](http://github.com/jangler/taffy) || [taffy](https://aur.archlinux.org/packages/taffy/)

*   **Qoobar** — Universal QT-based audio tagger (specialized for classical music)

	[http://qoobar.sourceforge.net/en/index.htm](http://qoobar.sourceforge.net/en/index.htm) || [qoobar](https://aur.archlinux.org/packages/qoobar/)

#### 声音编辑

*   **[Ardour](https://en.wikipedia.org/wiki/Ardour_(software) "wikipedia:Ardour (software)")** — Multichannel hard disk recorder and digital audio workstation.

	[http://ardour.org/](http://ardour.org/) || [ardour](https://www.archlinux.org/packages/?name=ardour)

*   **[Audacity](https://en.wikipedia.org/wiki/Audacity_(audio_editor) "wikipedia:Audacity (audio editor)")** — Program that lets you manipulate digital audio waveforms.

	[http://audacity.sourceforge.net/](http://audacity.sourceforge.net/) || [audacity](https://www.archlinux.org/packages/?name=audacity)

*   **GNOME Sound Recorder** — The Sound Recorder application enables you to record and play .flac, .ogg (OGG audio, or .oga), and .wav sound files.

	[https://git.gnome.org/browse/gnome-sound-recorder](https://git.gnome.org/browse/gnome-sound-recorder) || [gnome-sound-recorder](https://www.archlinux.org/packages/?name=gnome-sound-recorder)

*   **[Jokosher](https://en.wikipedia.org/wiki/Jokosher "wikipedia:Jokosher")** — Non-linear multi-track digital audio editor that is being developed in Python, using the GTK+ interface and GStreamer as an audio back-end.

	[https://launchpad.net/jokosher/](https://launchpad.net/jokosher/) || [jokosher](https://aur.archlinux.org/packages/jokosher/)

*   **KWave** — KDE的声音编辑器

	[http://kwave.sourceforge.net/](http://kwave.sourceforge.net/) || [kwave](https://www.archlinux.org/packages/?name=kwave)

*   **easytag** — 查看和编辑多种音频格式的 tag

	[http://easytag.sourceforge.net/](http://easytag.sourceforge.net/) || [easytag](https://www.archlinux.org/packages/?name=easytag)

*   **[LMMS](/index.php/LMMS "LMMS")** — The Linux MultiMedia Studio. Free cross-platform software which allows you to produce music with your computer.

	[http://lmms.sourceforge.net/](http://lmms.sourceforge.net/) || [lmms](https://www.archlinux.org/packages/?name=lmms)

*   **[Qtractor](https://en.wikipedia.org/wiki/Qtractor "wikipedia:Qtractor")** — Qt-based hard disk recorder and digital audio workstation application that aims to provide digital audio workstation software simple enough for the average home user, and yet powerful enough for the professional user.

	[http://qtractor.sourceforge.net/qtractor-index.html](http://qtractor.sourceforge.net/qtractor-index.html) || [qtractor](https://www.archlinux.org/packages/?name=qtractor)

*   **[Rosegarden](https://en.wikipedia.org/wiki/Rosegarden "wikipedia:Rosegarden")** — Digital audio workstation program developed with ALSA and Qt that acts as an audio and MIDI sequencer, scorewriter and musical composition and editing tool.

	[http://www.rosegardenmusic.com/](http://www.rosegardenmusic.com/) || [rosegarden](https://www.archlinux.org/packages/?name=rosegarden)

*   **XCFA** — Tool to extract the contens of audio CDs and convert them to various formats.

	[http://www.xcfa.tuxfamily.org/](http://www.xcfa.tuxfamily.org/) || [xcfa](https://aur.archlinux.org/packages/xcfa/)

### 手机管家

*   **moto4lin** — 基于P2K平台，用于摩托罗拉手机文件系统的浏览和编辑器

	[http://moto4lin.sourceforge.net/](http://moto4lin.sourceforge.net/) || [moto4lin](https://aur.archlinux.org/packages/moto4lin/)

*   **GNOME Phone Manager** — Control your mobile phone from your GNOME desktop.

	[https://wiki.gnome.org/PhoneManager](https://wiki.gnome.org/PhoneManager) || [gnome-phone-manager](https://www.archlinux.org/packages/?name=gnome-phone-manager)

*   **KDE Connect** — A project that aims to communicate all your devices.

	[http://community.kde.org/KDEConnect](http://community.kde.org/KDEConnect) || [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect)

*   **Moto4Lin** — File manager and seem editor for Motorola P2K phones (like C380/C650).

	[http://sourceforge.net/projects/moto4lin/](http://sourceforge.net/projects/moto4lin/) || [moto4lin](https://aur.archlinux.org/packages/moto4lin/)

### 视频

#### 视频播放器

See also [Wikipedia:Comparison of video player software](https://en.wikipedia.org/wiki/Comparison_of_video_player_software "wikipedia:Comparison of video player software").

##### 命令行

*   **[MPlayer](/index.php/MPlayer "MPlayer")** — Video player that supports a complete and versatile array of video and audio formats.

	[http://www.mplayerhq.hu/design7/news.html](http://www.mplayerhq.hu/design7/news.html) || [mplayer](https://www.archlinux.org/packages/?name=mplayer) (See also a very similar fork: [mplayer2](https://aur.archlinux.org/packages/mplayer2/))

*   **[mpv](/index.php/Mpv "Mpv")** — Movie player based on MPlayer and mplayer2.

	[http://mpv.io](http://mpv.io) || [mpv](https://www.archlinux.org/packages/?name=mpv) [mpv-git](https://aur.archlinux.org/packages/mpv-git/)

*   **[xine-ui](https://en.wikipedia.org/wiki/xine "wikipedia:xine")** — Free multimedia player.

	[http://www.xine-project.org](http://www.xine-project.org) || [xine-ui](https://www.archlinux.org/packages/?name=xine-ui)

*   **[VLC ncurses](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")** — Command-line version of the famous video player that can play smoothly high definition videos in the TTY.

	[https://www.videolan.org/vlc/](https://www.videolan.org/vlc/) || [vlc-nogui](https://aur.archlinux.org/packages/vlc-nogui/)

##### 图形化界面

See also: [MPlayer frontends](/index.php/MPlayer#Frontends.2FGUIs "MPlayer"), [mpv](/index.php/Mpv "Mpv").

*   **bomi** — Powerful and easy to use multimedia player (mpv backend) (Qt 5).

	[https://bomi-player.github.io/](https://bomi-player.github.io/) || [bomi](https://aur.archlinux.org/packages/bomi/) (previously [cmplayer](https://aur.archlinux.org/packages/cmplayer/)), [bomi-git](https://aur.archlinux.org/packages/bomi-git/)

*   **[Dragon Player](https://en.wikipedia.org/wiki/Kdemultimedia#Dragon_Player "wikipedia:Kdemultimedia")** — Simple video player for KDE. Part of the [kdemultimedia](https://www.archlinux.org/groups/x86_64/kdemultimedia/) group.

	[http://www.kde.org/applications/multimedia/dragonplayer/](http://www.kde.org/applications/multimedia/dragonplayer/) || [kdemultimedia-dragonplayer](https://www.archlinux.org/packages/?name=kdemultimedia-dragonplayer)

*   **[Kaffeine](https://en.wikipedia.org/wiki/Kaffeine "wikipedia:Kaffeine")** — Very versatile KDE media player that, by default, utilizes Xine as its backend and has excellent support of digital TV (DVB).

	[http://kaffeine.kde.org/](http://kaffeine.kde.org/) || [kaffeine](https://www.archlinux.org/packages/?name=kaffeine)

*   **Parole** — Modern media player based on the GStreamer framework.

	[http://goodies.xfce.org/projects/applications/parole/](http://goodies.xfce.org/projects/applications/parole/) || [parole](https://www.archlinux.org/packages/?name=parole)

*   **Rage** — Video and audio player written with Enlightenment Foundation Libraries with some extra bells and whistles.

	[http://www.enlightenment.org/p.php?p=about/rage](http://www.enlightenment.org/p.php?p=about/rage) || [rage](https://aur.archlinux.org/packages/rage/)

*   **Snappy** — Powerful media player with a minimalistic interface.

	[https://wiki.gnome.org/Apps/Snappy](https://wiki.gnome.org/Apps/Snappy) || [snappy-player](https://www.archlinux.org/packages/?name=snappy-player)

*   **[Totem](https://en.wikipedia.org/wiki/Totem_(software) "wikipedia:Totem (software)")** — Media player (audio and video) for the GNOME desktop that uses GStreamer. Part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

	[http://projects.gnome.org/totem/](http://projects.gnome.org/totem/) || [totem](https://www.archlinux.org/packages/?name=totem)

*   **[VLC media player](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")** — Middleweight video player with support for a wide variety of audio and video formats.

	[https://www.videolan.org/vlc/](https://www.videolan.org/vlc/) || [vlc](https://www.archlinux.org/packages/?name=vlc)

*   **Whaaw! Media Player** — Lightweight GStreamer-based audio and video player that can serve as a good alternative to Totem for those who do not like all of those GNOME dependencies.

	[http://home.gna.org/whaawmp/](http://home.gna.org/whaawmp/) || [whaawmp](https://aur.archlinux.org/packages/whaawmp/)

*   **Xnoise** — GTK+ and GStreamer-based media player for both audio and video with "a slick GUI, great speed and lots of features." (development ceased)

	[http://www.xnoise-media-player.com/](http://www.xnoise-media-player.com/) || [xnoise](https://www.archlinux.org/packages/?name=xnoise)

#### DVD 提取

See [Optical disc drive#DVD ripping](/index.php/Optical_disc_drive#DVD_ripping "Optical disc drive").

#### 视频编辑器

参见 [Wikipedia:Comparison of video editing software](https://en.wikipedia.org/wiki/Comparison_of_video_editing_software "wikipedia:Comparison of video editing software").

##### 命令行

*   **[Avidemux](https://en.wikipedia.org/wiki/Avidemux "wikipedia:Avidemux")** — 免费，天生为简易剪切、过滤和转码而生。

	[http://fixounet.free.fr/avidemux/](http://fixounet.free.fr/avidemux/) || [avidemux-cli](https://www.archlinux.org/packages/?name=avidemux-cli)

*   **[HandBrake-CLI](/index.php/Optical_disc_drive#DVD_ripping "Optical disc drive")** — Simple yet powerful video transcoder ideal for batch mkv/x264 ripping.

	[http://handbrake.fr/](http://handbrake.fr/) || [handbrake-cli](https://www.archlinux.org/packages/?name=handbrake-cli)

##### 图形界面

*   **[Avidemux](https://en.wikipedia.org/wiki/Avidemux "wikipedia:Avidemux")** — F免费，天生为简易剪切、过滤和转码而生。

	[http://fixounet.free.fr/avidemux/](http://fixounet.free.fr/avidemux/) || [avidemux-gtk](https://www.archlinux.org/packages/?name=avidemux-gtk) [avidemux-qt](https://www.archlinux.org/packages/?name=avidemux-qt)

*   **[Cinelerra (Community Version)](https://en.wikipedia.org/wiki/Cinelerra "wikipedia:Cinelerra")** — 专业级别，能够编辑或合成视频的环境。

	[http://cinelerra-cv.org/](http://cinelerra-cv.org/) || [cinelerra-cv](https://www.archlinux.org/packages/?name=cinelerra-cv)

*   **[HandBrake](/index.php/Optical_disc_drive#DVD_ripping "Optical disc drive")** — Simple yet powerful video transcoder ideal for batch mkv/x264 ripping. GTK+ version.

	[http://handbrake.fr/](http://handbrake.fr/) || [handbrake](https://www.archlinux.org/packages/?name=handbrake)

*   **[Kdenlive](https://en.wikipedia.org/wiki/Kdenlive "wikipedia:Kdenlive")** — 非线性，基本是专业人士用的。

	[http://kdenlive.org/](http://kdenlive.org/) || [kdenlive](https://www.archlinux.org/packages/?name=kdenlive)

*   **[Lightworks](https://en.wikipedia.org/wiki/Lightworks "wikipedia:Lightworks")** — 非线性，专业级别，支持广泛编码。

	[http://www.lwks.com/](http://www.lwks.com/) || [lwks](https://aur.archlinux.org/packages/lwks/)

*   **[LiVES](https://en.wikipedia.org/wiki/LiVES "wikipedia:LiVES")** — VJ (live performance) 平台。

	[http://lives.sourceforge.net/](http://lives.sourceforge.net/) || [lives](https://aur.archlinux.org/packages/lives/)

*   **Open Movie Editor** — 制作电影用，比较好上手。

	[http://www.openmovieeditor.org/](http://www.openmovieeditor.org/) || [openmovieeditor](https://aur.archlinux.org/packages/openmovieeditor/)

*   **[Open Shot](https://en.wikipedia.org/wiki/OpenShot_Video_Editor "wikipedia:OpenShot Video Editor")** — 非线性，基于 MLT 框架。

	[http://www.openshotvideo.com/](http://www.openshotvideo.com/) || [openshot](https://www.archlinux.org/packages/?name=openshot)

*   **[PiTiVi](https://en.wikipedia.org/wiki/Pitivi "wikipedia:Pitivi")** — GNOME 专用。

	[http://www.pitivi.org/](http://www.pitivi.org/) || [pitivi](https://www.archlinux.org/packages/?name=pitivi)

*   **Transmageddon** — Python 写成的简易软件。只要是 GStreamer 支持的编码，都可以转码。

	[http://www.linuxrising.org/](http://www.linuxrising.org/) || [transmageddon](https://www.archlinux.org/packages/?name=transmageddon)

#### 录屏

See also [Wikipedia:Comparison of screencasting software](https://en.wikipedia.org/wiki/Comparison_of_screencasting_software "wikipedia:Comparison of screencasting software").

Screencast utilities allow you to create a video of your desktop or individual windows.

*   **byzanz** — Simple screencast tool that produces GIF animations.

	[http://blogs.gnome.org/otte/2009/08/30/byzanz-0-2-0/](http://blogs.gnome.org/otte/2009/08/30/byzanz-0-2-0/) || [byzanz-git](https://aur.archlinux.org/packages/byzanz-git/)

*   **glc** — Screencast tool that can capture the sound and video from OpenGL applications, such as games, where regular X11 screencast tools produce choppy results.

	[https://github.com/nullkey/glc](https://github.com/nullkey/glc) || [glc](https://aur.archlinux.org/packages/glc/)

*   **Istanbul** — Simple desktop session recorder that produces ogg videos.

	[https://live.gnome.org/Istanbul](https://live.gnome.org/Istanbul) || [istanbul](https://aur.archlinux.org/packages/istanbul/)

*   **Kazam** — Screencasting program with design in mind.

	[https://launchpad.net/kazam](https://launchpad.net/kazam) || [kazam-bzr](https://aur.archlinux.org/packages/kazam-bzr/)

*   **[RecordMyDesktop](https://en.wikipedia.org/wiki/RecordMyDesktop "wikipedia:RecordMyDesktop")** — An easy to use utility that records your desktop into the ogg format with a CLI, Qt or GTK+ interface.

	[http://recordmydesktop.sourceforge.net/](http://recordmydesktop.sourceforge.net/) || [recordmydesktop](https://www.archlinux.org/packages/?name=recordmydesktop) [gtk-recordmydesktop](https://www.archlinux.org/packages/?name=gtk-recordmydesktop) [qt-recordmydesktop](https://www.archlinux.org/packages/?name=qt-recordmydesktop)

*   **simplescreenrecorder** — A feature-rich screen recorder written in C++/Qt4 that supports X11 and OpenGL.

	[http://www.maartenbaert.be/simplescreenrecorder/](http://www.maartenbaert.be/simplescreenrecorder/) || [simplescreenrecorder](https://www.archlinux.org/packages/?name=simplescreenrecorder)

*   **vokoscreen** — Simple screencast tool, GUI ffmpeg.

	[http://www.kohaupt-online.de/hp](http://www.kohaupt-online.de/hp) || [vokoscreen](https://aur.archlinux.org/packages/vokoscreen/)

*   **[XVidCap](https://en.wikipedia.org/wiki/XVidCap "wikipedia:XVidCap")** — Application used for recording a screencast or digital recording of an X Window System screen output with an audio narration.

	[http://xvidcap.sourceforge.net/](http://xvidcap.sourceforge.net/) || [xvidcap](https://aur.archlinux.org/packages/xvidcap/)

### Optical media burning

See [Optical disc drive#Burning CD/DVD/BD with a GUI](/index.php/Optical_disc_drive#Burning_CD.2FDVD.2FBD_with_a_GUI "Optical disc drive").

### Podcasts

see [Podcast clients](/index.php/List_of_applications/Internet#Podcast_clients "List of applications/Internet")

### Collection managers

*   **[Beets](/index.php/Beets "Beets")** — Music library organizer, tagger and more.

	[http://beets.radbox.org/](http://beets.radbox.org/) || [beets](https://www.archlinux.org/packages/?name=beets)

*   **Demlo** — Batch music tagger, encoder, renamer and more.

	[http://ambrevar.bitbucket.org/demlo/](http://ambrevar.bitbucket.org/demlo/) || [demlo](https://aur.archlinux.org/packages/demlo/)

*   **[GCstar](https://en.wikipedia.org/wiki/GCstar "wikipedia:GCstar")** — GNOME application for organizing various collections (board games, comic books, movies, stamps, etc.).

	[http://www.gcstar.org/](http://www.gcstar.org/) || [gcstar](https://www.archlinux.org/packages/?name=gcstar)

*   **[Tellico](https://en.wikipedia.org/wiki/Tellico "wikipedia:Tellico")** — KDE application for organizing various collections (books, video, music, coins, etc.).

	[http://tellico-project.org/](http://tellico-project.org/) || [tellico](https://www.archlinux.org/packages/?name=tellico)

*   **[Kodi](/index.php/Kodi "Kodi")** — Application for organizing various collections and automatically retrieving info about them (video, music, photos).

	[http://kodi.tv/](http://kodi.tv/) || [kodi](https://www.archlinux.org/packages/?name=kodi)

### Lyrics fetchers

*   **clyrics** — An extensible lyrics fetcher, with daemon support for cmus and mocp.

	[http://beets.radbox.org/](http://beets.radbox.org/) || [clyrics](https://aur.archlinux.org/packages/clyrics/)

## 工具

### 分区工具

参阅 [Partitioning#Partitioning tools](/index.php/Partitioning#Partitioning_tools "Partitioning").

### 挂载

*   **9mount** — Mount 9p filesystems.

	[http://sqweek.net/code/9mount/](http://sqweek.net/code/9mount/) || [9mount](https://aur.archlinux.org/packages/9mount/)

*   **cryptmount** — Mount an encrypted file system as a regular user.

	[http://cryptmount.sourceforge.net/](http://cryptmount.sourceforge.net/) || [cryptmount](https://aur.archlinux.org/packages/cryptmount/)

*   **ldm** — A lightweight daemon that mounts drives automagically using *udev*

	[https://github.com/LemonBoy/ldm](https://github.com/LemonBoy/ldm) || [ldm](https://aur.archlinux.org/packages/ldm/)

*   **pmount** — Mount *source* as a regular user to an automatically created destination `/media/*source_name*`.

	[http://pmount.alioth.debian.org/](http://pmount.alioth.debian.org/) || [pmount](https://aur.archlinux.org/packages/pmount/)

*   **pmount-safe-removal** — Mount removable devices as regular user with safe removal

	[http://mywaytoarch.tumblr.com/post/13111098534/pmount-safe-removal-of-usb-device](http://mywaytoarch.tumblr.com/post/13111098534/pmount-safe-removal-of-usb-device) || [pmount-safe-removal](https://aur.archlinux.org/packages/pmount-safe-removal/)

*   **udevil** — Mounts removable devices as a regular user, show device info, and monitor device changes. Only depends on *udev* and glib.

	[http://ignorantguru.github.io/udevil](http://ignorantguru.github.io/udevil) || [udevil](https://www.archlinux.org/packages/?name=udevil)

*   **ws** — Mount Windows network shares ([CIFS](https://en.wikipedia.org/wiki/Server_Message_Block "wikipedia:Server Message Block") and [VFS](https://en.wikipedia.org/wiki/Virtual_file_system "wikipedia:Virtual file system")).

	[http://winshares.sourceforge.net/](http://winshares.sourceforge.net/) || [ws](https://aur.archlinux.org/packages/ws/)

#### Udisks

*   **bashmount** — A bash script to mount and manage removable media as a regular user with udisks.

	[https://github.com/jamielinux/bashmount](https://github.com/jamielinux/bashmount) || [bashmount](https://aur.archlinux.org/packages/bashmount/)

*   **udiskie** — Automatic disk mounting service using *udisks*

	[https://pypi.python.org/pypi/udiskie](https://pypi.python.org/pypi/udiskie) || [udiskie](https://www.archlinux.org/packages/?name=udiskie)

*   **udisks_functions** — Bash functions and aliases for *udisks2*

	[https://bbs.archlinux.org/viewtopic.php?id=109307](https://bbs.archlinux.org/viewtopic.php?id=109307) || [udisks_functions](https://aur.archlinux.org/packages/udisks_functions/)

*   **udisksvm** — GUI *udisks* wrapper for removable media

	[https://bbs.archlinux.org/viewtopic.php?id=112397](https://bbs.archlinux.org/viewtopic.php?id=112397) || [udisksvm](https://aur.archlinux.org/packages/udisksvm/)

### 基本 Shell 命令

*   **[Core utilities](/index.php/Core_utilities "Core utilities")** — The basic file, shell and text manipulation utilities of the GNU operating system

	[http://www.gnu.org/software/coreutils](http://www.gnu.org/software/coreutils) || [coreutils](https://www.archlinux.org/packages/?name=coreutils)

### 集成式开发环境

See also [Wikipedia:Comparison of integrated development environments](https://en.wikipedia.org/wiki/Comparison_of_integrated_development_environments "wikipedia:Comparison of integrated development environments").

*   **[Anjuta](/index.php/Anjuta "Anjuta")** — Versatile IDE with project management, an application wizard, an interactive debugger, a source editor, version control support and many more tools.

	[http://www.anjuta.org/](http://www.anjuta.org/) || [anjuta](https://www.archlinux.org/packages/?name=anjuta)

*   **[Aptana Studio](https://en.wikipedia.org/wiki/Aptana#Aptana_Studio "wikipedia:Aptana")** — IDE based on Eclipse, but geared towards web development, with support for HTML, CSS, Javascript, Ruby on Rails, PHP, Adobe AIR and others.

	[http://www.aptana.org/](http://www.aptana.org/) || [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)

*   **[Bluefish](https://en.wikipedia.org/wiki/Bluefish_(text_editor) "wikipedia:Bluefish (text editor)")** — GTK+ editor/IDE with an MDI interface, syntax highlighting and support for Python plugins.

	[http://bluefish.openoffice.nl/](http://bluefish.openoffice.nl/) || [bluefish](https://www.archlinux.org/packages/?name=bluefish)

*   **[BlueGriffon](https://en.wikipedia.org/wiki/BlueGriffon "wikipedia:BlueGriffon")** — A WYSIWYG content editor for the World Wide Web. Powered by Gecko, the rendering engine of [Firefox](/index.php/Firefox "Firefox"), it can edit Web pages in conformance to Web Standards. It runs on Mac OS X, Windows and Linux.

	[http://bluegriffon.org/](http://bluegriffon.org/) || [bluegriffon](https://www.archlinux.org/packages/?name=bluegriffon)

*   **[Bluej](https://en.wikipedia.org/wiki/Bluej "wikipedia:Bluej")** — Fully featured Java IDE used mainly for educational and beginner purposes.

	[http://bluej.org/](http://bluej.org/) || [bluej](https://aur.archlinux.org/packages/bluej/)

*   **[Brackets](https://en.wikipedia.org/wiki/Brackets_(text_editor) "wikipedia:Brackets (text editor)")** — A free open-source editor written in HTML, CSS, and Javascript with a primary focus on Web Development. It was created by Adobe Systems, licensed under the MIT License, and is currently maintained on GitHub.

	[http://brackets.io/](http://brackets.io/) || [brackets](https://aur.archlinux.org/packages/brackets/)

*   **[Code::Blocks](https://en.wikipedia.org/wiki/Code::Blocks "wikipedia:Code::Blocks")** — Open source and cross-platform C/C++ IDE.

	[http://www.codeblocks.org/](http://www.codeblocks.org/) || [codeblocks](https://www.archlinux.org/packages/?name=codeblocks)

*   **[Cloud9](https://en.wikipedia.org/wiki/Cloud9_IDE "wikipedia:Cloud9 IDE")** — State-of-the-art IDE that runs in your browser and lives in the cloud, allowing you to run, debug and deploy applications from anywhere, anytime.

	[https://c9.io/](https://c9.io/) || [cloud9](https://aur.archlinux.org/packages/cloud9/)

*   **[Eclipse](/index.php/Eclipse "Eclipse")** — Open source community project, which aims to provide a universal development platform.

	[http://eclipse.org/](http://eclipse.org/) || [eclipse](https://www.archlinux.org/packages/?name=eclipse)

*   **[Editra](https://en.wikipedia.org/wiki/Editra "wikipedia:Editra")** — Multi-platform text editor with an implementation that focuses on creating an easy to use interface and features that aid in code development.

	[http://www.editra.org](http://www.editra.org) || [editra-svn](https://aur.archlinux.org/packages/editra-svn/)

*   **[Eric](https://en.wikipedia.org/wiki/Eric_Python_IDE "wikipedia:Eric Python IDE")** — Full-featured Python 3.x and Ruby IDE in PyQt4.

	[http://eric-ide.python-projects.org/](http://eric-ide.python-projects.org/) || [eric](https://www.archlinux.org/packages/?name=eric) [eric4](https://aur.archlinux.org/packages/eric4/)

*   **[Gambas](/index.php/Gambas "Gambas")** — Free development environment based on a Basic interpreter with object extensions.

	[http://gambas.sourceforge.net/en/main.html](http://gambas.sourceforge.net/en/main.html) || [gambas3-ide](https://www.archlinux.org/packages/?name=gambas3-ide)

*   **[Geany](https://en.wikipedia.org/wiki/Geany "wikipedia:Geany")** — Text editor using the GTK+ toolkit with basic features of an integrated development environment.

	[https://geany.org](https://geany.org) || [geany](https://www.archlinux.org/packages/?name=geany)

*   **IEP** — Cross-platform Python IDE focused on interactivity and introspection, which makes it very suitable for scientific computing.

	[http://iep-project.org/](http://iep-project.org/) || [iep](https://aur.archlinux.org/packages/iep/)

*   **[IntelliJ IDEA](https://en.wikipedia.org/wiki/IntelliJ_IDEA "wikipedia:IntelliJ IDEA")** — IDE for Java, Groovy and other programming languages with advanced refactoring features.

	[http://www.jetbrains.com/idea/](http://www.jetbrains.com/idea/) || [intellij-idea-community-edition](https://www.archlinux.org/packages/?name=intellij-idea-community-edition)

*   **[KDevelop](https://en.wikipedia.org/wiki/KDevelop "wikipedia:KDevelop")** — Feature-full, plugin extensible IDE for C/C++ and other programming languages.

	[http://kdevelop.org/](http://kdevelop.org/) || [kdevelop](https://www.archlinux.org/packages/?name=kdevelop)

*   **[Komodo Edit](https://en.wikipedia.org/wiki/Komodo_Edit "wikipedia:Komodo Edit")** — A free, multi-language editor.

	[http://www.activestate.com/komodo-edit](http://www.activestate.com/komodo-edit) || [komodo-edit](https://aur.archlinux.org/packages/komodo-edit/)

*   **[Lazarus](https://en.wikipedia.org/wiki/Lazarus_(IDE) "wikipedia:Lazarus (IDE)")** — Cross-platform IDE for Object Pascal.

	[http://lazarus.freepascal.org/](http://lazarus.freepascal.org/) || [lazarus](https://www.archlinux.org/packages/?name=lazarus)

*   **LiteIDE** — A simple, open source, cross-platform Go IDE.

	[https://github.com/visualfc/liteide](https://github.com/visualfc/liteide) || [liteide](https://www.archlinux.org/packages/?name=liteide)

*   **MonkeyStudio** — Monkey Studio (MkS) is a cross platform IDE written in C++/Qt 4\. Syntax highlighting for more than 22 programming languages.

	[http://monkeystudio.org/](http://monkeystudio.org/) || [monkeystudio](https://aur.archlinux.org/packages/monkeystudio/)

*   **[MonoDevelop](https://en.wikipedia.org/wiki/MonoDevelop "wikipedia:MonoDevelop")** — Cross-platform IDE targeted for the Mono and .NET frameworks.

	[http://monodevelop.com/](http://monodevelop.com/) || [monodevelop](https://www.archlinux.org/packages/?name=monodevelop)

*   **MPLAB** — IDE for Microchip PIC and dsPIC development

	[http://www.microchip.com/mplabx](http://www.microchip.com/mplabx) || [microchip-mplabx-bin](https://aur.archlinux.org/packages/microchip-mplabx-bin/)

*   **[NetBeans](/index.php/Netbeans "Netbeans")** — Integrated development environment (IDE) for developing with Java, JavaScript, PHP, Python, Ruby, Groovy, C, C++, Scala, Clojure, and other languages.

	[http://netbeans.org/](http://netbeans.org/) || [netbeans](https://www.archlinux.org/packages/?name=netbeans)

*   **[Ninja-IDE](https://en.wikipedia.org/wiki/Ninja-IDE "wikipedia:Ninja-IDE")** — from the recursive acronym: "Ninja-IDE Is Not Just Another IDE", is a cross-platform integrated development environment (IDE); runs on Linux/X11, Mac OS X and Windows OSs. Used, for example, for Python development

	[http://ninja-ide.org/](http://ninja-ide.org/) || [ninja-ide](https://www.archlinux.org/packages/?name=ninja-ide)

*   **[Phpstorm](https://en.wikipedia.org/wiki/PhpStorm "wikipedia:PhpStorm")** — JetBrains PhpStorm is a commercial, cross-platform IDE for PHP built on JetBrains' IntelliJ IDEA platform, providing an editor for PHP, HTML and JavaScript with on-the-fly code analysis, error prevention and automated refactorings for PHP and JavaScript code.

	[https://www.jetbrains.com/phpstorm/](https://www.jetbrains.com/phpstorm/) || [phpstorm](https://aur.archlinux.org/packages/phpstorm/) [phpstorm-eap](https://aur.archlinux.org/packages/phpstorm-eap/)

*   **[PyCharm](https://en.wikipedia.org/wiki/PyCharm "wikipedia:PyCharm")** — IDE used for programming in Python with support for code analysis, debugging, unit testing, version control and web development with Django.

	[http://www.jetbrains.com/pycharm/](http://www.jetbrains.com/pycharm/) || [pycharm-community](https://aur.archlinux.org/packages/pycharm-community/)

*   **[QDevelop](https://en.wikipedia.org/wiki/QDevelop "wikipedia:QDevelop")** — Free and cross-platform IDE for Qt.

	[http://biord-software.org/qdevelop/](http://biord-software.org/qdevelop/) || [qdevelop-svn](https://aur.archlinux.org/packages/qdevelop-svn/)

*   **[Qt Creator](https://en.wikipedia.org/wiki/Qt_Creator "wikipedia:Qt Creator")** — Lightweight, cross-platform C++ integrated development environment with a focus on Qt.

	[http://qt-project.org/downloads#qt-creator](http://qt-project.org/downloads#qt-creator) || [qtcreator](https://www.archlinux.org/packages/?name=qtcreator)

*   **[Scratch](https://en.wikipedia.org/wiki/Scratch "wikipedia:Scratch")** — A multimedia authoring tool for educational and entertainment purposes, such as creating interactive projects and simple sprite-based games. It is used primarly by unskilled users (such as children) as an entry to [event-driven programming](https://en.wikipedia.org/wiki/Event-driven_programming "wikipedia:Event-driven programming"). *Scratch* is free software under GPL v2 and [Scratch Source Code License](http://wiki.scratch.mit.edu/wiki/Scratch_Source_Code_License).

	[http://scratch.mit.edu](http://scratch.mit.edu) || [scratch](https://www.archlinux.org/packages/?name=scratch)

*   **Spyder** — Scientific PYthon Development EnviRonment providing MATLAB-like features.

	[http://code.google.com/p/spyderlib/](http://code.google.com/p/spyderlib/) || [spyder](https://www.archlinux.org/packages/?name=spyder)

### 虚拟终端

参见 [Wikipedia:List of terminal emulators](https://en.wikipedia.org/wiki/List_of_terminal_emulators "wikipedia:List of terminal emulators").

资深用户爱用虚拟终端，也难怪会有那么多 X11 虚拟终端冒出来了。大多虚拟终端在模拟 Xterm, Xterm 又向 VT102 看齐，最后 VT102 更是在模仿打字机，所以您应该品读 [Wikipedia article](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator") 和 [other sources](https://google.com/search?q=linux+terminal+emulators) 以把握个大概。

*   **Eterm** — 取代 Xterm 且为 [Enlightenment](/index.php/Enlightenment "Enlightenment") 而打造。

	[http://eterm.org](http://eterm.org) || [eterm](https://aur.archlinux.org/packages/eterm/)

*   **[KMSCON](/index.php/KMSCON "KMSCON")** — 基于 linux kernel mode setting (KMS).

	[https://github.com/dvdhrm/kmscon](https://github.com/dvdhrm/kmscon) || [kmscon](https://www.archlinux.org/packages/?name=kmscon)

*   **[Konsole](https://en.wikipedia.org/wiki/Konsole "wikipedia:Konsole")** — [KDE](/index.php/KDE "KDE") 专用。

	[http://kde.org/applications/system/konsole/](http://kde.org/applications/system/konsole/) || [kdebase-konsole](https://www.archlinux.org/packages/?name=kdebase-konsole)

*   **[Mrxvt](https://en.wikipedia.org/wiki/mrxvt "wikipedia:mrxvt")** — 基于 rxvt, 支持 Tabs.

	[http://materm.sourceforge.net/wiki/pmwiki.php](http://materm.sourceforge.net/wiki/pmwiki.php) || [mrxvt](https://aur.archlinux.org/packages/mrxvt/)

*   **QTerminal** — 基于 Qt, 轻量。

	[https://github.com/qterminal/qterminal](https://github.com/qterminal/qterminal) || [qterminal-git](https://aur.archlinux.org/packages/qterminal-git/)

*   **[rxvt](https://en.wikipedia.org/wiki/Rxvt "wikipedia:Rxvt")** — 公认已取代 Xterm 的虚拟终端。

	[http://rxvt.sourceforge.net/](http://rxvt.sourceforge.net/) || [rxvt](https://aur.archlinux.org/packages/rxvt/)

*   **[st](/index.php/St "St")** — 简单，在Ｘ下可用。

	[http://st.suckless.org](http://st.suckless.org) || [st](https://www.archlinux.org/packages/?name=st)

*   **Terminal** — 支持多窗口，滚动缓冲以及众多理想功能，从属 GNUstep.

	[http://gap.nongnu.org/terminal/index.html](http://gap.nongnu.org/terminal/index.html) || [gnustep-terminal](https://aur.archlinux.org/packages/gnustep-terminal/)

*   **[terminator](/index.php/Terminator "Terminator")** — 支持多 Panels.

	[http://gnometerminator.blogspot.it/](http://gnometerminator.blogspot.it/) || [terminator](https://www.archlinux.org/packages/?name=terminator)

*   **Terminology** — Enlightenment 项目专用，有众多金光闪闪的功能：文件缩略图，多媒体播放器。

	[http://enlightenment.org/p.php?p=about/terminology](http://enlightenment.org/p.php?p=about/terminology) || [terminology](https://www.archlinux.org/packages/?name=terminology)

*   **[Tilda](https://en.wikipedia.org/wiki/Tilda_(software) "wikipedia:Tilda (software)")** — 受众多 FPS 游戏，如 Quake, Doom 和半条命，启发而诞生。

	[http://sourceforge.net/projects/tilda/files/](http://sourceforge.net/projects/tilda/files/) || [tilda](https://www.archlinux.org/packages/?name=tilda)

*   **[urxvt](/index.php/Urxvt "Urxvt")** — 基于 Perl, rxvt, 高度可扩展，支持 Unicode, 多 Tab, 访问 URL, Quake 风格的下拉式，伪・透明。

	[http://software.schmorp.de/pkg/rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode) || [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode)

*   **[xterm](/index.php/Xterm "Xterm")** — Ｘ最简单的虚拟终端了，它还为不能在窗口系统下直接用的程序，提供了兼容于 DEC VT102 和 Tektronix 4014 的终端。

	[http://invisible-island.net/xterm/](http://invisible-island.net/xterm/) || [xterm](https://www.archlinux.org/packages/?name=xterm)

*   **[Yakuake](https://en.wikipedia.org/wiki/Yakuake "wikipedia:Yakuake")** — 基于 Konsole, 下拉式，Quake 风格。

	[http://yakuake.kde.org/](http://yakuake.kde.org/) || [yakuake](https://www.archlinux.org/packages/?name=yakuake)

#### 基于 VTE

[VTE](http://developer.gnome.org/vte/unstable/) (Virtual Terminal Emulator) 最早是由 GNOME 开发并广泛使用的虚拟终端，它还派生了众多大大小小的分支。

*   **evilvte** — 很轻量，可定制性强，支持 Tabs, 自动隐藏，换编码。

	[http://calno.com/evilvte/](http://calno.com/evilvte/) || [evilvte](https://aur.archlinux.org/packages/evilvte/)

*   **[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")** — [GNOME](/index.php/GNOME "GNOME") 专用，支持 Unicode, 不支持透明。

	[https://wiki.gnome.org/Apps/Terminal](https://wiki.gnome.org/Apps/Terminal) || [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)

*   **[Guake](/index.php/Guake "Guake")** — GNOME 桌面的，下拉式的。

	[http://guake.org/](http://guake.org/) || [guake](https://www.archlinux.org/packages/?name=guake)

*   **Terra** — 基于 GTK+3.0, 同一个窗口上可以分割成众多小窗口。

	[https://github.com/ozcanesen/terra-terminal](https://github.com/ozcanesen/terra-terminal) || [terra](https://aur.archlinux.org/packages/terra/)

*   **[LilyTerm](/index.php/LilyTerm "LilyTerm")** — 很轻量。

	[http://lilyterm.luna.com.tw/](http://lilyterm.luna.com.tw/) || [lilyterm](https://www.archlinux.org/packages/?name=lilyterm)

*   **LXTerminal** — [LXDE](/index.php/LXDE "LXDE") 组件之一，也可单独安装。

	[http://wiki.lxde.org/en/LXTerminal](http://wiki.lxde.org/en/LXTerminal) || [lxterminal](https://www.archlinux.org/packages/?name=lxterminal)

*   **MATE terminal** — [Wikipedia:GNOME terminal](https://en.wikipedia.org/wiki/GNOME_terminal "wikipedia:GNOME terminal") 在 [MATE](/index.php/MATE "MATE") 桌面上的 Fork.

	[http://www.mate-desktop.org/](http://www.mate-desktop.org/) || [mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal)

*   **ROXTerm** — 有 Tab 机制。

	[http://roxterm.sourceforge.net/](http://roxterm.sourceforge.net/) || [roxterm](https://www.archlinux.org/packages/?name=roxterm)

*   **sakura** — 基于 GTK+ 和 VTE.

	[http://www.pleyades.net/david/projects/sakura](http://www.pleyades.net/david/projects/sakura) || [sakura](https://www.archlinux.org/packages/?name=sakura)

*   **Stjerm** — 基于 GTK+, 下拉式，提供简约的界面，内存占用少，与合成窗口管理器有很好的互动，比如 Compiz.

	[https://code.google.com/p/stjerm-terminal-emulator/](https://code.google.com/p/stjerm-terminal-emulator/) || [stjerm-git](https://aur.archlinux.org/packages/stjerm-git/)

*   **[Terminal](https://en.wikipedia.org/wiki/Terminal_(Xfce) "wikipedia:Terminal (Xfce)")** — [Xfce](/index.php/Xfce "Xfce") 桌面专用虚拟终端，支持颜色提示符，Tab 机制。

	[http://docs.xfce.org/apps/terminal/start](http://docs.xfce.org/apps/terminal/start) || [xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal)

*   **Termit** — 简单，基于 VTE, 支持 Tabs, 书签，编码转换。

	[https://wiki.github.com/nonstop/termit/](https://wiki.github.com/nonstop/termit/) || [termit](https://aur.archlinux.org/packages/termit/)

*   **[Termite](/index.php/Termite "Termite")** — 适合命令行控，转为平铺式窗口管理器打造，还有 Tab 机制。

	[https://github.com/thestinger/termite](https://github.com/thestinger/termite) || [termite](https://www.archlinux.org/packages/?name=termite)

#### KMS-based

The following terminal emulators are based on the [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") that could be invoked without X.

*   **[KMSCON](/index.php/KMSCON "KMSCON")** — A KMS/DRM-based system console(getty) with an integrated terminal emulator for Linux operating systems.

	[https://github.com/dvdhrm/kmscon](https://github.com/dvdhrm/kmscon) || [kmscon](https://www.archlinux.org/packages/?name=kmscon)

#### framebuffer-based

In GNU/Linux world, the [framebuffer](https://en.wikipedia.org/wiki/Framebuffer "wikipedia:Framebuffer") could be refered to a virtual device in the Linux kernel (**fbdev**) or the virtual framebuffer system for X (**xvfb**). This section mainly lists the terminal emulators that based on the in-kernel virtual device, i.e. **fbdev**.

*   **[fbterm](/index.php/Fbterm "Fbterm")** — A fast framebuffer-based terminal emulator with many amazing features. Development stopped.

	[http://code.google.com/p/fbterm/](http://code.google.com/p/fbterm/) || [fbterm](https://www.archlinux.org/packages/?name=fbterm)

*   **yaft** — A simple terminal emulator for living without X, with UCS2 glyphs, wallpaper and 256color support.

	[https://github.com/uobikiemukot/yaft](https://github.com/uobikiemukot/yaft) || [yaft](https://aur.archlinux.org/packages/yaft/)

### 文件

#### 文件管理器

See also [Wikipedia:Comparison of file managers](https://en.wikipedia.org/wiki/Comparison_of_file_managers "wikipedia:Comparison of file managers").

##### 命令行

*   **[Midnight Commander](https://en.wikipedia.org/wiki/Midnight_commander "wikipedia:Midnight commander")** — 终端双面板文件管理器

	[http://www.midnight-commander.org](http://www.midnight-commander.org) || [mc](https://www.archlinux.org/packages/?name=mc)

*   **pilot** — [Alpine](/index.php/Alpine "Alpine")的文件管理器

	[http://www.washington.edu/alpine](http://www.washington.edu/alpine) || [alpine](https://aur.archlinux.org/packages/alpine/)

*   **[Ranger](/index.php/Ranger "Ranger")** — vi风格快捷键,可定制,特性丰富

	[http://nongnu.org/ranger](http://nongnu.org/ranger) || [ranger](https://www.archlinux.org/packages/?name=ranger)

*   **[Vifm](/index.php/Vifm "Vifm")** — 基于ncurses的双面板文件管理器,vi风格快捷键

	[http://vifm.sourceforge.net/](http://vifm.sourceforge.net/) || [vifm](https://www.archlinux.org/packages/?name=vifm)

##### 图形环境

*   **Dolphin** — KDE 4的默认文件管理器

	[http://dolphin.kde.org/](http://dolphin.kde.org/) || [kdebase-dolphin](https://www.archlinux.org/packages/?name=kdebase-dolphin)

*   **emelFM2** — 双面板文件管理器

	[http://emelfm2.net/](http://emelfm2.net/) || [emelfm2](https://www.archlinux.org/packages/?name=emelfm2)

*   **Konqueror** — KDE环境下的文件管理器

	[http://www.konqueror.org/](http://www.konqueror.org/) || [kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror)

*   **Krusader** — KDE环境下的高级双面板(commander风格)文件管理器

	[http://www.krusader.org/](http://www.krusader.org/) || [krusader](https://www.archlinux.org/packages/?name=krusader)

*   **[GNOME Files](/index.php/GNOME_Files "GNOME Files")** — Gnome默认文件管理器,重量级,可扩展、支持自定义脚本

	[http://projects.gnome.org/nautilus/](http://projects.gnome.org/nautilus/) || [nautilus](https://www.archlinux.org/packages/?name=nautilus)

*   **[PCManFM](/index.php/PCManFM "PCManFM")** — 轻量级文件管理器,支持标签,可以管理桌面背景(可选)

	[http://pcmanfm.sourceforge.net/](http://pcmanfm.sourceforge.net/) || [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm)

*   **qtfm** — 小型轻量级文件管理器,完全基于Qt

	[http://www.qtfm.org/](http://www.qtfm.org/) || [qtfm](https://www.archlinux.org/packages/?name=qtfm)

*   **ROX-Filer** — 小型快速文件管理器,可以管理桌面背景和面板(可选)

	[http://rox.sourceforge.net](http://rox.sourceforge.net) || [rox](https://www.archlinux.org/packages/?name=rox)

*   **Sunflower** — 小型,高度可定制的双面板文件管理器,支持插件

	[http://code.google.com/p/sunflower-fm/](http://code.google.com/p/sunflower-fm/) || [sunflower](https://aur.archlinux.org/packages/sunflower/)

*   **[Thunar](/index.php/Thunar "Thunar")** — 可以作为daemon运行,启动和加载目录速度很快.可以配置自定义动作

	[http://thunar.xfce.org/index.html](http://thunar.xfce.org/index.html) || [thunar](https://www.archlinux.org/packages/?name=thunar)

*   **tuxcmd** — 双面板文件管理器，Total Commander风格，已停止开发

	[http://tuxcmd.sourceforge.net/description.php](http://tuxcmd.sourceforge.net/description.php) || [tuxcmd](https://www.archlinux.org/packages/?name=tuxcmd)

*   **Xfe** — X环境下的类似视窗操作系统的Explorer或Commander的管理器

	[http://roland65.free.fr/xfe/index.php/](http://roland65.free.fr/xfe/index.php/) || [xfe](https://www.archlinux.org/packages/?name=xfe)

#### 桌面搜索引擎

See also [Wikipedia:List of search engines#Desktop search engines](https://en.wikipedia.org/wiki/List_of_search_engines#Desktop_search_engines "wikipedia:List of search engines").

*   **Catfish** — 万能文件搜索工具

	[https://launchpad.net/catfish-search](https://launchpad.net/catfish-search) || [catfish](https://www.archlinux.org/packages/?name=catfish)

*   **Docfetcher** — 基于 Java, 开源，桌面搜索

	[http://docfetcher.sourceforge.net](http://docfetcher.sourceforge.net) || [docfetcher](https://aur.archlinux.org/packages/docfetcher/)

*   **Gnome Search Tool** — Gnome 首席搜索工具

	[http://gnome.org](http://gnome.org) || [gnome-search-tool](https://www.archlinux.org/packages/?name=gnome-search-tool)

*   **Gnome Search Tool No Nautilus** — 去除了 [GNOME Files](/index.php/GNOME_Files "GNOME Files") 和 *gnome-desktop* 的 *gnome-search-tool*

	|| [gnome-search-tool-no-nautilus](https://aur.archlinux.org/packages/gnome-search-tool-no-nautilus/)

*   **Pinot** — 个性化元搜索

	[http://code.google.com/p/pinot-search/](http://code.google.com/p/pinot-search/) || [pinot](https://www.archlinux.org/packages/?name=pinot)

*   **Recoll** — 基于 Xapian 后端的全文本搜索

	[http://www.lesbonscomptes.com/recoll/](http://www.lesbonscomptes.com/recoll/) || [recoll](https://www.archlinux.org/packages/?name=recoll)

*   **Searchmonkey** — 强大的 GUI 搜索工具，支持正则表达式

	[http://searchmonkey.sourceforge.net/](http://searchmonkey.sourceforge.net/) || [searchmonkey](https://aur.archlinux.org/packages/searchmonkey/)

*   **[Strigi](https://en.wikipedia.org/wiki/Strigi "wikipedia:Strigi")** — 爬虫，Qt GUI，快速

	[http://strigi.sourceforge.net/](http://strigi.sourceforge.net/) || [strigi](https://www.archlinux.org/packages/?name=strigi)

*   **[Tracker](https://en.wikipedia.org/wiki/MetaTracker_(software) "wikipedia:MetaTracker (software)")** — 一体化索引，搜索工具，元数据

	[http://projects.gnome.org/tracker/index.html](http://projects.gnome.org/tracker/index.html) || [tracker](https://www.archlinux.org/packages/?name=tracker)

#### 压缩与解压

See also [Wikipedia:Comparison of file archivers](https://en.wikipedia.org/wiki/Comparison_of_file_archivers "wikipedia:Comparison of file archivers").

##### 命令行

*   **atool** — 管理多种压缩文件的脚本.

	[http://www.nongnu.org/atool/](http://www.nongnu.org/atool/) || [atool](https://www.archlinux.org/packages/?name=atool)

*   **[p7zip](/index.php/P7zip "P7zip")** — 终端下的7zip的POSIX系统移植版本.

	[http://p7zip.sourceforge.net/](http://p7zip.sourceforge.net/) || [p7zip](https://www.archlinux.org/packages/?name=p7zip)

##### 图形环境

*   **Ark** — KDE环境下的压缩文件管理器.

	[http://kde.org/applications/utilities/ark/](http://kde.org/applications/utilities/ark/) || [kdeutils-ark](https://www.archlinux.org/packages/?name=kdeutils-ark)

*   **File Roller** — Gnome环境下的默认压缩文件管理器.

	[http://fileroller.sourceforge.net/](http://fileroller.sourceforge.net/) || [file-roller](https://www.archlinux.org/packages/?name=file-roller)

*   **Peazip** — 一个开源的文件及压缩文件管理器

	[http://www.peazip.org/peazip-linux.html](http://www.peazip.org/peazip-linux.html) || [peazip](https://aur.archlinux.org/packages/peazip/)

*   **Squeeze** — 终端工具的次轻量级的前端.

	[http://squeeze.xfce.org/](http://squeeze.xfce.org/) || [squeeze](https://aur.archlinux.org/packages/squeeze/)

*   **Xarchive** — 多种工具的GTK+ 2前端.

	[http://xarchive.sourceforge.net/](http://xarchive.sourceforge.net/) || [xarchive](https://aur.archlinux.org/packages/xarchive/)

*   **Xarchiver** — 独立的轻量级桌面压缩文件管理器.

	[http://xarchiver.sourceforge.net/](http://xarchiver.sourceforge.net/) || [xarchiver](https://www.archlinux.org/packages/?name=xarchiver)

*   **[p7zip](/index.php/P7zip "P7zip")** — 终端下的7zip的POSIX系统移植版本.包括7zFM图形界面.

	[http://p7zip.sourceforge.net/](http://p7zip.sourceforge.net/) || [p7zip](https://www.archlinux.org/packages/?name=p7zip)

#### 文件合并及比较

See also [Wikipedia:Comparison of file comparison tools](https://en.wikipedia.org/wiki/Comparison_of_file_comparison_tools "wikipedia:Comparison of file comparison tools").

*   **colordiff** — 相当于 diff, 但自带语法高亮。

	[http://www.colordiff.org/](http://www.colordiff.org/) || [colordiff](https://www.archlinux.org/packages/?name=colordiff)

*   **Diffuse** — 简单小巧的文本合并工具，由 Python 编写成

	[http://diffuse.sourceforge.net/](http://diffuse.sourceforge.net/) || [diffuse](https://www.archlinux.org/packages/?name=diffuse)

*   **KDiff3** — KDE 文件及目录的比较及合并工具

	[http://kdiff3.sourceforge.net/](http://kdiff3.sourceforge.net/) || [kdiff3](https://www.archlinux.org/packages/?name=kdiff3)

*   **[Kompare](https://en.wikipedia.org/wiki/Kompare "wikipedia:Kompare")** — 在源文件之间 Diff/Patch 的前端，支持众多比较格式，还允许大量显示格式的选项

	[http://kde.org/applications/development/kompare](http://kde.org/applications/development/kompare) || [kdesdk-kompare](https://www.archlinux.org/packages/?name=kdesdk-kompare)

*   **[Meld](https://en.wikipedia.org/wiki/Meld_(software) "wikipedia:Meld (software)")** — 可视化比较及合并工具，适用于文件，目录和版本控制项目

	[http://meld.sourceforge.net](http://meld.sourceforge.net) || [meld](https://www.archlinux.org/packages/?name=meld)

*   **xxdiff** — 专注于文件或目录之间差异的图形化浏览器

	[http://furius.ca/xxdiff/](http://furius.ca/xxdiff/) || [xxdiff](https://aur.archlinux.org/packages/xxdiff/)

[Vim](/index.php/Vim "Vim") 和 [Emacs](/index.php/Emacs "Emacs") 均通过 [vimdiff](/index.php/Vim#Merging_files_.28vimdiff.29 "Vim") 和 `ediff` 提供了合并功能。

#### 批量命名

### 磁盘清理

### 磁盘使用情况分析

*   **ncdu** — 简单的，使用ncurses的磁盘使用情况分析工具器.

	[http://dev.yorhel.nl/ncdu](http://dev.yorhel.nl/ncdu) || [ncdu](https://www.archlinux.org/packages/?name=ncdu)

*   **gt5** — diff 风格的 du 浏览器

	[http://gt5.sourceforge.net](http://gt5.sourceforge.net) || [gt5](https://aur.archlinux.org/packages/gt5/)

*   **Baobab** — 一个C/gtk+的Gnome环境的磁盘分析程序.

	[http://www.marzocca.net/linux/baobab](http://www.marzocca.net/linux/baobab) || [baobab](https://www.archlinux.org/packages/?name=baobab)

*   **Filelight** — 显示可互动的图像，用环状的饼图可视化磁盘使用情况.

	[http://www.methylblue.com/filelight](http://www.methylblue.com/filelight) || [filelight](https://www.archlinux.org/packages/?name=filelight)

*   **gdmap** — 根据文件夹或文件的大小绘制由一系列矩形组成的图像.

	[http://gdmap.sourceforge.net/](http://gdmap.sourceforge.net/) || [gdmap](https://www.archlinux.org/packages/?name=gdmap)

### 时钟同步

### 系统监视器

*   **adesklet SystemMonitor** — [adesklets](https://en.wikipedia.org/wiki/Adesklets "wikipedia:Adesklets") 的一系列模块系统监视器。

	[http://adesklets.sourceforge.net/desklets.html](http://adesklets.sourceforge.net/desklets.html) || [adesklet-systemmonitor](https://aur.archlinux.org/packages/adesklet-systemmonitor/)

*   **[Conky](/index.php/Conky "Conky")** — 轻量、可定制的系统监视器。

	[http://conky.sourceforge.net/](http://conky.sourceforge.net/) || [conky](https://www.archlinux.org/packages/?name=conky)

*   **dstat** — 万能的资源统计工具。

	[http://dag.wieers.com/home-made/dstat/](http://dag.wieers.com/home-made/dstat/) || [dstat](https://www.archlinux.org/packages/?name=dstat)

*   **[GKrellM](https://en.wikipedia.org/wiki/GKrellM "wikipedia:GKrellM")** — 既简单，又灵活的系统监视器，由 GTK+ 编写成，可集成大量插件。

	[http://members.dslextreme.com/users/billw/gkrellm/gkrellm.html](http://members.dslextreme.com/users/billw/gkrellm/gkrellm.html) || [gkrellm](https://www.archlinux.org/packages/?name=gkrellm)

*   **gnome-system-monitor** — [GNOME (简体中文)](/index.php/GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME (简体中文)") 的系统监视器。

	[https://help.gnome.org/users/gnome-system-monitor/](https://help.gnome.org/users/gnome-system-monitor/) || [gnome-system-monitor](https://www.archlinux.org/packages/?name=gnome-system-monitor)

*   **[htop](https://en.wikipedia.org/wiki/Htop "wikipedia:Htop")** — 简易的交互式进程查看器。

	[http://htop.sourceforge.net/](http://htop.sourceforge.net/) || [htop](https://www.archlinux.org/packages/?name=htop)

*   **[KSysGuard](https://en.wikipedia.org/wiki/KDE_System_Guard 专用的任务管理器、性能监视器。

	[http://userbase.kde.org/KSysGuard/](http://userbase.kde.org/KSysGuard/) || [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)

*   **linux process explorer** — Linux 的图像化任务管理器。

	[http://sourceforge.net/projects/procexp/](http://sourceforge.net/projects/procexp/) || [procexp](https://aur.archlinux.org/packages/procexp/)

*   **LXTask** — [LXDE (简体中文)](/index.php/LXDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LXDE (简体中文)") 的轻量任务管理器。

	[http://wiki.lxde.org/en/LXTask](http://wiki.lxde.org/en/LXTask) || [lxtask](https://www.archlinux.org/packages/?name=lxtask)

*   **[Trayfreq](/index.php/Trayfreq "Trayfreq")** — 一个轻量的电池监视器、CPU 计数器。

	[http://trayfreq.sourceforge.net](http://trayfreq.sourceforge.net) || [trayfreq](https://aur.archlinux.org/packages/trayfreq/)

### 系统信息检测

#### 命令行

*   **alsi** — Arch Linux 一个系统信息工具，它甚至可适用于其它 Linux 发行版，连编辑脚本都不需要。

	[http://trizenx.blogspot.ro/2012/08/alsi.html](http://trizenx.blogspot.ro/2012/08/alsi.html) || [alsi](https://aur.archlinux.org/packages/alsi/)

*   **archey** — 基于 Python 3 的简单脚本，能显示 Arch Logo 及若干基本系统信息。

	[https://github.com/djmelik/archey](https://github.com/djmelik/archey) || [archey](https://aur.archlinux.org/packages/archey/)

*   **archey2** — 基于 Python 2 的简单脚本，能显示 Arch Logo 及若干基本系统信息。

	[https://github.com/djmelik/archey](https://github.com/djmelik/archey) || [archey2](https://aur.archlinux.org/packages/archey2/)

*   **archey3-git** — 又一个能显示 Arch Logo 及若干基本系统信息的 Python 脚本

	[http://www.generictestdomain.net/archey3/](http://www.generictestdomain.net/archey3/) || [archey3-git](https://aur.archlinux.org/packages/archey3-git/)

*   **Dmidecode** — 能基于 SMBIOS/DMI 标准报告储存于您系统 BIOS 中的硬件信息。

	[http://www.nongnu.org/dmidecode/](http://www.nongnu.org/dmidecode/) || [dmidecode](https://www.archlinux.org/packages/?name=dmidecode)

#### 图形环境

*   **CPU-G** — 显示您硬件若干有用信息的工具，和 Windows 下的 CPU-Z 很相似。

	[http://cpug.sourceforge.net/](http://cpug.sourceforge.net/) || [cpu-g](https://aur.archlinux.org/packages/cpu-g/)

*   **hardinfo** — 显示您硬件和操作系统若干有用信息的工具，和 Windows 下的设备管理器很相似。

	[http://hardinfo.berlios.de/HomePage](http://hardinfo.berlios.de/HomePage) || [hardinfo](https://www.archlinux.org/packages/?name=hardinfo)

*   **i-Nex** — 一个收集并显示所有硬件参数的工具，采用了和 Windows 工具 CPU-Z 很相似的界面。

	[http://i-nex.linux.pl/](http://i-nex.linux.pl/) || [i-nex](https://aur.archlinux.org/packages/i-nex/)

*   **lshw-gtk** — 一个提供很详细的硬件信息的小工具，同时具备了 CLI 和 GTK 界面。

	[http://ezix.org/project/wiki/HardwareLiSter](http://ezix.org/project/wiki/HardwareLiSter) || [lshw-gtk](https://aur.archlinux.org/packages/lshw-gtk/)

### 键盘布局切换

*   **fbxkb** — A NETWM compliant keyboard indicator and switcher. It shows a flag of current keyboard in a systray area and allows you to switch to another one.

	[http://fbxkb.sourceforge.net/](http://fbxkb.sourceforge.net/) || [fbxkb](https://aur.archlinux.org/packages/fbxkb/)

*   **xxkb** — A lightweight keyboard layout indicator and switcher.

	[http://sourceforge.net/projects/xxkb/](http://sourceforge.net/projects/xxkb/) || [xxkb](https://www.archlinux.org/packages/?name=xxkb)

*   **qxkb** — A keyboard switcher written in Qt.

	[http://code.google.com/p/qxkb/](http://code.google.com/p/qxkb/) || [qxkb](https://aur.archlinux.org/packages/qxkb/)

*   **[X Neural Switcher](https://en.wikipedia.org/wiki/X_Neural_Switcher "wikipedia:X Neural Switcher")** — A text analyser, it detects the language of the input and corrects the keyboard layout if needed.

	[http://www.xneur.ru/](http://www.xneur.ru/) || [xneur](https://aur.archlinux.org/packages/xneur/), [gxneur](https://aur.archlinux.org/packages/gxneur/) (GUI)

### 电源管理

见 [Power saving#Packages](/index.php/Power_saving#Packages "Power saving").

### 剪贴板管理

### 壁纸设置

### 软件包管理

*   **Aurnotify** — 提示你最喜爱的来自AUR的软件的新动态.

	[http://adesklets.sourceforge.net/desklets.html](http://adesklets.sourceforge.net/desklets.html) || [aurnotify](https://aur.archlinux.org/packages/aurnotify/)

*   **Pkgtools** — 一个Arch Linux软件管理的脚本合集. 包含 **pkgfile** – 命令来查找哪个包含了某个文件

	[https://github.com/Daenyth/pkgtools](https://github.com/Daenyth/pkgtools) || [pkgtools](https://aur.archlinux.org/packages/pkgtools/)

*   **[Yaourt](/index.php/Yaourt "Yaourt")** — 一个pacman前端，有更多特性和对aur的支持.

	[http://www.archlinux.fr/yaourt-en/](http://www.archlinux.fr/yaourt-en/) || [yaourt](https://aur.archlinux.org/packages/yaourt/)

参考阅读[AUR helpers](/index.php/AUR_helpers "AUR helpers").

### 输入法

参见 [Wikipedia:Input method](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method").

*   **[Fcitx (简体中文)](/index.php/Fcitx_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fcitx (简体中文)")** — 可扩展，超灵活的输入工具。

	[http://fcitx-im.org](http://fcitx-im.org) || [fcitx](https://www.archlinux.org/packages/?name=fcitx)

*   **Hime** — 基于 GTK2/GTK3 的输入平台。

	[http://hime-ime.github.io/](http://hime-ime.github.io/) || [hime-git](https://aur.archlinux.org/packages/hime-git/)

*   **[IBus (简体中文)](/index.php/IBus_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "IBus (简体中文)")** — Linux 新一代输入 BUS.

	[http://ibus.googlecode.com](http://ibus.googlecode.com) || [ibus](https://www.archlinux.org/packages/?name=ibus)

*   **[Rime IME](/index.php/Rime_IME "Rime IME")** — Rime 输入引擎。

	[http://code.google.com/p/rimeime/](http://code.google.com/p/rimeime/) || [ibus-rime](https://www.archlinux.org/packages/?name=ibus-rime) or [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime)

*   **[UIM](/index.php/UIM "UIM")** — 多语言输入库。

	[http://code.google.com/p/uim/](http://code.google.com/p/uim/) || [uim](https://www.archlinux.org/packages/?name=uim)

### Trash management

*   **trash-cli** — A command-line interface implementing FreeDesktop.org's Trash specification.

	[http://github.com/andreafrancia/trash-cli](http://github.com/andreafrancia/trash-cli) || [trash-cli](https://www.archlinux.org/packages/?name=trash-cli)

### File synchronization

*   **[rsync](/index.php/Rsync "Rsync")** — An incremental transfer and synchronization program.

	[http://rsync.samba.org](http://rsync.samba.org) || [rsync](https://www.archlinux.org/packages/?name=rsync)

*   **[Syncthing](/index.php/Syncthing "Syncthing")** — Open, trustworthy and decentralized cloud synchronization service.

	[https://syncthing.net](https://syncthing.net) || [syncthing](https://www.archlinux.org/packages/?name=syncthing)

*   **[Unison](/index.php/Unison "Unison")** — Bidirectional sync. It keeps track of changes like a VCS.

	[http://www.cis.upenn.edu/~bcpierce/unison](http://www.cis.upenn.edu/~bcpierce/unison) || [unison](https://www.archlinux.org/packages/?name=unison)

### Finders

*   **fuzzy-find** — Fuzzy completion for finding files.

	[https://github.com/silentbicycle/ff](https://github.com/silentbicycle/ff) || [ff-git](https://aur.archlinux.org/packages/ff-git/)

*   **fzf** — General-purpose command-line fuzzy finder.

	[https://github.com/junegunn/fzf](https://github.com/junegunn/fzf) || [fzf](https://www.archlinux.org/packages/?name=fzf)

*   **rmlint** — Tool to quickly find (and optionally remove) duplicate files and other lint

	[https://rmlint.readthedocs.org/en/latest/](https://rmlint.readthedocs.org/en/latest/) || [rmlint](https://www.archlinux.org/packages/?name=rmlint)

## 文档

### 办公软件套装

See also [Wikipedia:Comparison of office suites](https://en.wikipedia.org/wiki/Comparison_of_office_suites "wikipedia:Comparison of office suites").

*   **[Calligra](https://en.wikipedia.org/wiki/Calligra_Suite "wikipedia:Calligra Suite")** — [KDE](/index.php/KDE "KDE") 办公软件套装，即 KOffice 的活跃分支。它提供了 OpenOffice 大多功能，又有智能手机和平板的版本。

	[http://www.calligra-suite.org/](http://www.calligra-suite.org/) || [calligra](https://www.archlinux.org/packages/?name=calligra)

*   **[Kingsoft Office](https://en.wikipedia.org/wiki/Kingsoft_Office "wikipedia:Kingsoft Office")** — 专有，又名 WPS.

	[http://www.kingsoftstore.com/](http://www.kingsoftstore.com/) || [wps-office](https://aur.archlinux.org/packages/wps-office/)

*   **[LibreOffice](/index.php/LibreOffice "LibreOffice")** — OpenOffice 的超活跃分支之一。

	[https://www.libreoffice.org/](https://www.libreoffice.org/) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) 或 [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh)

*   **[OpenOffice](/index.php/OpenOffice "OpenOffice")** — 开源的办公软件，集成了字处理，表格，幻灯片，图像，数据库以及更多的软件，采用 Apache 许可证。

	[http://www.openoffice.org/](http://www.openoffice.org/) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **[Siag Office](https://en.wikipedia.org/wiki/Siag_Office "wikipedia:Siag Office")** — 极度轻量，有字处理、表格、文本编辑器、文件管理器和预览器。

	[http://siag.nu/](http://siag.nu/) || [siag-office](https://aur.archlinux.org/packages/siag-office/)

*   **[SoftMaker Office](https://en.wikipedia.org/wiki/SoftMaker_Office "wikipedia:SoftMaker Office")** — 完全，稳定，轻快，兼容微软办公格式，有字处理，表格，幻灯片。

	[http://www.freeoffice.com/](http://www.freeoffice.com/) || [freeoffice](https://aur.archlinux.org/packages/freeoffice/)

### 字处理器

See also [Wikipedia:Comparison of word processors](https://en.wikipedia.org/wiki/Comparison_of_word_processors "wikipedia:Comparison of word processors").

*   **[Abiword](/index.php/Abiword "Abiword")** — 全功能的字处理器。

	[http://www.abisource.com/](http://www.abisource.com/) || [abiword](https://www.archlinux.org/packages/?name=abiword)

*   **[BlueGriffon](https://en.wikipedia.org/wiki/BlueGriffon "wikipedia:BlueGriffon")** — WYSIWYG content editor for the World Wide Web.

	[http://www.bluegriffon.com/](http://www.bluegriffon.com/) || [bluegriffon](https://www.archlinux.org/packages/?name=bluegriffon)

*   **[Calligra Words](https://en.wikipedia.org/wiki/Calligra_Words "wikipedia:Calligra Words")** — Powerful word processor included in the Calligra Suite.

	[http://www.calligra.org/words/](http://www.calligra.org/words/) || [calligra-words](https://www.archlinux.org/packages/?name=calligra-words)

*   **gLabels** — program for creating labels and business cards.

	[http://glabels.org/](http://glabels.org/) || [glabels](https://www.archlinux.org/packages/?name=glabels)

*   **[LibreOffice Writer](/index.php/LibreOffice "LibreOffice")** — Full-featured word processor included in the LibreOffice suite.

	[https://www.libreoffice.org/discover/writer](https://www.libreoffice.org/discover/writer) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still)

*   **[OpenOffice Writer](/index.php/OpenOffice "OpenOffice")** — Full-featured word processor included in the OpenOffice suite.

	[http://www.openoffice.org/](http://www.openoffice.org/) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **Pathetic Writer** — X-based rich text processor included in Siag Office.

	[http://siag.nu/pw/](http://siag.nu/pw/) || [siag-office](https://aur.archlinux.org/packages/siag-office/)

*   **[Scribus](https://en.wikipedia.org/wiki/Scribus "wikipedia:Scribus")** — 桌面出版程序。

	[http://www.scribus.net/canvas/Scribus](http://www.scribus.net/canvas/Scribus) || [scribus](https://www.archlinux.org/packages/?name=scribus)

*   **[Ted](https://en.wikipedia.org/wiki/Ted_(word_processor) "wikipedia:Ted (word processor)")** — Easy to use GTK+-based rich text processor (with footnote support).

	[http://www.nllgg.nl/Ted/](http://www.nllgg.nl/Ted/) || [ted](https://aur.archlinux.org/packages/ted/)

### 文档标记语言

See also [Wikipedia:Comparison of document markup languages](https://en.wikipedia.org/wiki/Comparison_of_document_markup_languages "wikipedia:Comparison of document markup languages").

*   **[asciidoc](https://en.wikipedia.org/wiki/AsciiDoc "wikipedia:AsciiDoc")** — Human-readable text document format. Used by Arch for generating *pacman* 's man pages[[3]](https://www.archlinux.org/pacman/pacman.8.html).

	[http://asciidoc.org/](http://asciidoc.org/) || [asciidoc](https://www.archlinux.org/packages/?name=asciidoc)

*   **Asciidoctor** — An asciidoc implementation written in Ruby, with many extra features.

	[http://asciidoctor.org/](http://asciidoctor.org/) || [ruby-asciidoctor](https://aur.archlinux.org/packages/ruby-asciidoctor/)

*   **[Markdown](https://en.wikipedia.org/wiki/Markdown "wikipedia:Markdown")** — Text-to-HTML conversion tool that allows you to write using a simple plain text format.

	[http://daringfireball.net/projects/markdown](http://daringfireball.net/projects/markdown) || [markdown](https://www.archlinux.org/packages/?name=markdown)

*   **Pandoc** — Swiss-army knife for converting one markup format into another (supports Markdown).

	[http://johnmacfarlane.net/pandoc](http://johnmacfarlane.net/pandoc) || [haskell-pandoc](https://www.archlinux.org/packages/?name=haskell-pandoc) [pandoc-static](https://aur.archlinux.org/packages/pandoc-static/)
**Tip:** Both *pandoc* packages have large build-time dependencies that require significant hard disk space. Alternatively, you can download the *pandoc-static* binary directly from the Parabola GNU Linux repo ([64-bit](https://repo.parabolagnulinux.org/pcr/os/x86_64/), [32-bit](https://repo.parabolagnulinux.org/pcr/os/i686/)), or install *haskell-pandoc* from the binary [haskell-core](/index.php/Unofficial_user_repositories#haskell-core "Unofficial user repositories") repository, which however also has massive dependencies size. It is [recommended against](/index.php/Haskell#cabal-install "Haskell") to use [cabal-install](https://www.archlinux.org/packages/?name=cabal-install) as the primary source of installation of Haskell packages even though it may appear more straightforward.

*   **[Sphinx](https://en.wikipedia.org/wiki/Sphinx_(documentation_generator) "wikipedia:Sphinx (documentation generator)")** — A documentation generation system using [reStructuredText](https://en.wikipedia.org/wiki/ReStructuredText "wikipedia:ReStructuredText") to generate output in multiple formats (primary documentation system for the Python project).

	[http://sphinx-doc.org](http://sphinx-doc.org) || [python-sphinx](https://www.archlinux.org/packages/?name=python-sphinx)

*   **[txt2tags](https://en.wikipedia.org/wiki/Txt2tags "wikipedia:Txt2tags")** — Dead-simple, KISS-compliant lightweight, human-readable markup language to produce rich format content out of plain text files.

	[http://txt2tags.sourceforge.net](http://txt2tags.sourceforge.net) || [txt2tags](https://www.archlinux.org/packages/?name=txt2tags)

### 表格

See also [Wikipedia:Comparison of spreadsheet software](https://en.wikipedia.org/wiki/Comparison_of_spreadsheet_software "wikipedia:Comparison of spreadsheet software").

*   **[Calligra Sheets](https://en.wikipedia.org/wiki/Calligra_Sheets "wikipedia:Calligra Sheets")** — Powerful spreadsheet application included in the Calligra Suite

	[http://www.calligra.org/sheets/](http://www.calligra.org/sheets/) || [calligra-sheets](https://www.archlinux.org/packages/?name=calligra-sheets)

*   **[Gnumeric](/index.php/Gnumeric "Gnumeric")** — Spreadsheet program that is part of the GNOME desktop.

	[http://www.gnumeric.org/](http://www.gnumeric.org/) || [gnumeric](https://www.archlinux.org/packages/?name=gnumeric)

*   **[LibreOffice Calc](/index.php/LibreOffice "LibreOffice")** — Full-featured spreadsheet application included in the LibreOffice suite.

	[https://www.libreoffice.org/discover/calc/](https://www.libreoffice.org/discover/calc/) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still)

*   **[OpenOffice Calc](/index.php/OpenOffice "OpenOffice")** — Full-featured spreadsheet application included in the OpenOffice suite.

	[http://openoffice.org/product/calc](http://openoffice.org/product/calc) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **Pyspread** — Pyspread is a non-traditional spreadsheet application that is based on and written in the programming language Python.

	[http://manns.github.io/pyspread/index.html](http://manns.github.io/pyspread/index.html) || [pyspread](https://aur.archlinux.org/packages/pyspread/)

*   **Siag** — Spreadsheet application based on the X Window System and the Scheme programming language included in Siag Office.

	[http://siag.nu/siag/](http://siag.nu/siag/) || [siag-office](https://aur.archlinux.org/packages/siag-office/)

### 学术文档

With [LaTeX](/index.php/LaTeX "LaTeX"), creation of any scientific document, article, journal, etc. is made commonplace.

See also [Wikipedia:Comparison of TeX editors](https://en.wikipedia.org/wiki/Comparison_of_TeX_editors "wikipedia:Comparison of TeX editors") and [the LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX/Installation#Editors).

*   **[AUCTeX](https://en.wikipedia.org/wiki/AUCTEX "wikipedia:AUCTEX")** — Extensible package for writing and formatting TeX files in Emacs.

	[https://www.gnu.org/software/auctex/](https://www.gnu.org/software/auctex/) || [auctex](https://www.archlinux.org/packages/?name=auctex)

*   **[Gummi](https://en.wikipedia.org/wiki/Gummi_(software) "wikipedia:Gummi (software)")** — Lightweight TeX/LaTeX GTK+-based editor.

	[http://gummi.midnightcoding.org/](http://gummi.midnightcoding.org/) || [gummi](https://www.archlinux.org/packages/?name=gummi)

*   **[Kile](https://en.wikipedia.org/wiki/Kile "wikipedia:Kile")** — User-friendly TeX/LaTeX editor for the KDE desktop with many features.

	[http://kile.sourceforge.net/](http://kile.sourceforge.net/) || [kile](https://www.archlinux.org/packages/?name=kile)

*   **[LyX](https://en.wikipedia.org/wiki/LyX "wikipedia:LyX")** — Document processor that encourages an approach to writing based on the structure of your documents (WYSIWYM) and not simply their appearance (WYSIWYG).

	[http://www.lyx.org/](http://www.lyx.org/) || [lyx](https://www.archlinux.org/packages/?name=lyx)

*   **[TeXmacs](https://en.wikipedia.org/wiki/GNU_TeXmacs "wikipedia:GNU TeXmacs")** — WYSIWYW editing platform with special features for scientists.

	[http://www.texmacs.org/](http://www.texmacs.org/) || [texmacs](https://www.archlinux.org/packages/?name=texmacs)

*   **[Texmaker](https://en.wikipedia.org/wiki/Texmaker "wikipedia:Texmaker")** — Cross-platform, light and easy-to-use LaTeX IDE.

	[http://www.xm1math.net/texmaker/index.html](http://www.xm1math.net/texmaker/index.html) || [texmaker](https://www.archlinux.org/packages/?name=texmaker)

*   **Winefish** — Editor for experienced LaTeX users with support for UTF-8, syntax highlight, auto-completion and auto-text.

	[http://winefish.berlios.de/](http://winefish.berlios.de/) || [winefish](https://aur.archlinux.org/packages/winefish/)

### 翻译与本土化

*   **[Apertium](https://en.wikipedia.org/wiki/Apertium "wikipedia:Apertium")** — Free and open source rule-based machine translation platform with available language data. It supports the following formats: HTML, Microsoft Office 2007 XML, OpenDocument, TMX, MediaWiki and others.

	[http://apertium.org/](http://apertium.org/) || [apertium](https://aur.archlinux.org/packages/apertium/)

*   **[Gtranslator](https://en.wikipedia.org/wiki/Gtranslator "wikipedia:Gtranslator")** — Enhanced gettext po file editor for the GNOME. It handles all forms of gettext po files and includes very useful features.

	[https://projects.gnome.org/gtranslator/](https://projects.gnome.org/gtranslator/) || [gtranslator](https://www.archlinux.org/packages/?name=gtranslator)

*   **[Lokalize](https://en.wikipedia.org/wiki/Lokalize "wikipedia:Lokalize")** — Standard [KDE](/index.php/KDE "KDE") tool for software translation. It includes basic editing of PO files, support for glossary, translation memory, project managing, etc. It belongs to [kdesdk](https://www.archlinux.org/groups/x86_64/kdesdk/)

	[http://userbase.kde.org/Lokalize](http://userbase.kde.org/Lokalize) || [lokalize](https://www.archlinux.org/packages/?name=lokalize)

*   **[Moses](https://en.wikipedia.org/wiki/Moses_(machine_translation) "wikipedia:Moses (machine translation)")** — Statistical machine translation tool (language data not included).

	[http://statmt.org/moses](http://statmt.org/moses) || [moses-git](https://aur.archlinux.org/packages/moses-git/)

*   **[OmegaT](https://en.wikipedia.org/wiki/OmegaT "wikipedia:OmegaT")** — General translator's tool which contains a lot of translation memory features and can give suggestions from Google Translate. It supports the following formats: HTML, Microsoft Office 2007 XML, OpenDocument, XLIFF/Okapi, MediaWiki, plain text, TMX and others.

	[http://omegat.org](http://omegat.org) || [omegat](https://aur.archlinux.org/packages/omegat/)

*   **[Poedit](https://en.wikipedia.org/wiki/Poedit "wikipedia:Poedit")** — 基于gettext/po-based的简单翻译工具。

	[http://poedit.net](http://poedit.net) || [poedit](https://www.archlinux.org/packages/?name=poedit)

*   **Pology** — Set of Python tools for dealing with gettext/po-files.

	[http://techbase.kde.org/Localization/Tools/Pology](http://techbase.kde.org/Localization/Tools/Pology) || [pology](https://aur.archlinux.org/packages/pology/)

*   **[Virtaal](https://en.wikipedia.org/wiki/Virtaal and others.

	[http://translate.sourceforge.net/wiki/virtaal](http://translate.sourceforge.net/wiki/virtaal) || [virtaal](https://aur.archlinux.org/packages/virtaal/)

### 文本编辑器

参见 [Wikipedia:Comparison of text editors](https://en.wikipedia.org/wiki/Comparison_of_text_editors "wikipedia:Comparison of text editors").

一些轻量级 [集成开发式环境](/index.php/List_of_applications/Utilities#Integrated_development_environments "List of applications/Utilities") 也能拿来当文本编辑器用用。

#### 命令行

*   **e3** — 无依赖，又小巧，由汇编语言编写而成。

	[http://sites.google.com/site/e3editor/](http://sites.google.com/site/e3editor/) || [e3](https://www.archlinux.org/packages/?name=e3)

*   **dex** — 轻量简单，支持 ctags 及匹配编译错误。

	[https://github.com/tihirvon/dex](https://github.com/tihirvon/dex) || [dex-editor-git](https://aur.archlinux.org/packages/dex-editor-git/)

*   **[Emacs-nox](/index.php/Emacs "Emacs")** — 可扩展、高度定制、自助编辑并实时显示，不支持 X11.

	[http://www.gnu.org/software/emacs/emacs.html](http://www.gnu.org/software/emacs/emacs.html) || [emacs-nox](https://www.archlinux.org/packages/?name=emacs-nox)

*   **[JED](https://en.wikipedia.org/wiki/JED_(text_editor) "wikipedia:JED (text editor)")** — 基于 [S-Lang library](https://en.wikipedia.org/wiki/S-Lang_(programming_library) "wikipedia:S-Lang (programming library)"), 同时包括命令行版 jed 和 X-windows 版 xjed.

	[http://jedsoft.org/jed/](http://jedsoft.org/jed/) || [jed](https://aur.archlinux.org/packages/jed/)

*   **[Joe](/index.php/Joe "Joe") (Joe's Own Editor)** — 基于终端，为简单易用而生。

	[http://joe-editor.sourceforge.net/](http://joe-editor.sourceforge.net/) || [joe](https://www.archlinux.org/packages/?name=joe)

*   **[mcedit](https://en.wikipedia.org/wiki/Midnight_Commander "wikipedia:Midnight Commander")** — Midnight Commander 文件管理器自带的编辑器。

	[http://www.ibiblio.org/mc/](http://www.ibiblio.org/mc/) || [mc](https://www.archlinux.org/packages/?name=mc)

*   **[MicroEmacs](https://en.wikipedia.org/wiki/MicroEMACS "wikipedia:MicroEMACS")** — 基于 Ncurses, 同时包括命令行版 me -n 和 X-windows 版 me.

	[http://www.jasspa.com/](http://www.jasspa.com/) || [jasspa-me](https://aur.archlinux.org/packages/jasspa-me/)

*   **[mg](https://en.wikipedia.org/wiki/mg_(editor) "wikipedia:mg (editor)")** — 又小又快的绿色 Emacs 类编辑器。

	[http://homepage.boetes.org/software/mg](http://homepage.boetes.org/software/mg) || [mg](https://www.archlinux.org/packages/?name=mg)

*   **[Nano](/index.php/Nano "Nano")** — 基于 pico, 自带虚拟键盘。

	[http://nano-editor.org/](http://nano-editor.org/) || [nano](https://www.archlinux.org/packages/?name=nano)

*   **Ne** — 键绑定遵循 Windows 风格。

	[http://ne.di.unimi.it/](http://ne.di.unimi.it/) || [ne](https://aur.archlinux.org/packages/ne/)

*   **[Zile](https://en.wikipedia.org/wiki/Zile_(editor) "wikipedia:Zile (editor)")** — 又一种轻量的 Emacs 类编辑器

	[https://gnu.org/s/zile/](https://gnu.org/s/zile/) || [zile](https://www.archlinux.org/packages/?name=zile)

##### [Vi](/index.php/Vi "Vi") 类文本编辑器

*   **[Vi](/index.php/Vi "Vi")** — 最原始的 ex/vi 类编辑器。

	[http://ex-vi.sourceforge.net/](http://ex-vi.sourceforge.net/) || [vi](https://www.archlinux.org/packages/?name=vi)

*   **[Vim](/index.php/Vim "Vim") (Vi IMproved)** — 在 Unix 之道上追求登峰造极的高级 vi 类编辑器，集众多功能之大成。

	[http://www.vim.org/](http://www.vim.org/) || [vim](https://www.archlinux.org/packages/?name=vim)

*   **[Neovim](/index.php/Neovim "Neovim")** — 二十一世纪的现代 Vi 类编辑器。

	[http://neovim.org/](http://neovim.org/) || [neovim-git](https://aur.archlinux.org/packages/neovim-git/)

#### 图形环境

*   **[Acme](https://en.wikipedia.org/wiki/Acme_(text_editor) "wikipedia:Acme (text editor)")** — 极简且灵活的编程环境，由 Rob Pike 为 Plan 9 操作系统开发而成。

	[http://acme.cat-v.org](http://acme.cat-v.org) || [plan9port](https://www.archlinux.org/packages/?name=plan9port)

*   **[Atom](https://en.wikipedia.org/wiki/Atom_(text_editor) "wikipedia:Atom (text editor)")** — 由 GitHub 开发，支持由 Node.js 写成的插件和 Git 版本控制。

	[https://atom.io/](https://atom.io/) || [atom-editor](https://aur.archlinux.org/packages/atom-editor/)

*   **[Beaver](/index.php/Beaver "Beaver")** — GTK+, 天生就高度模块化，轻量化，现代化。

	[http://beaver-editor.sourceforge.net/](http://beaver-editor.sourceforge.net/) || [beaver](https://www.archlinux.org/packages/?name=beaver)

*   **Edile** — 基于单文件，PyGTK 代码与脚本的编辑器。

	[https://code.google.com/p/edile/](https://code.google.com/p/edile/) || [edile](https://aur.archlinux.org/packages/edile/)

*   **[Gedit](https://en.wikipedia.org/wiki/Gedit "wikipedia:Gedit")** — GNOME 自带的 GTK+ 编辑器，支持语法高亮，自动缩进，对齐括号等等，还提供了众多扩展以加强功能。

	[http://projects.gnome.org/gedit/](http://projects.gnome.org/gedit/) || [gedit](https://www.archlinux.org/packages/?name=gedit)

*   **[GNU Emacs](/index.php/Emacs "Emacs")** — 虽以高难度闻名，但其成千上百的技巧与扩展却不是盖的。

	[https://gnu.org/s/emacs](https://gnu.org/s/emacs) || [emacs](https://www.archlinux.org/packages/?name=emacs)

*   **[gVim](/index.php/GVim "GVim")** — Vim 的图形用户界面

	[http://www.vim.org/](http://www.vim.org/) || [gvim](https://www.archlinux.org/packages/?name=gvim)

*   **Jedit** — 程序员专用，由 Java 编写而成。

	[http://www.jedit.org/](http://www.jedit.org/) || [jedit](https://www.archlinux.org/packages/?name=jedit)

*   **[JuffEd](https://en.wikipedia.org/wiki/JuffEd "wikipedia:JuffEd")** — 支持多标签与语法高亮，由 Qt 编写而成。

	[http://juffed.com/en/index.html](http://juffed.com/en/index.html) || [juffed](https://aur.archlinux.org/packages/juffed/)

*   **[Kate](https://en.wikipedia.org/wiki/Kate_(text_editor) "wikipedia:Kate (text editor)")** — 功能全面、程序员专用的编辑器，出自 KDE, 还能当 MDI 和文件管理器用。

	[http://kate-editor.org/](http://kate-editor.org/) || [kdesdk-kate](https://www.archlinux.org/packages/?name=kdesdk-kate)

*   **[KWrite](https://en.wikipedia.org/wiki/KWrite "wikipedia:KWrite")** — KDE 自带的轻量文本编辑器，编辑器部件继承自 Kate。

	[http://kde.org/applications/utilities/kwrite/](http://kde.org/applications/utilities/kwrite/) || [kdebase-kwrite](https://www.archlinux.org/packages/?name=kdebase-kwrite)

*   **[Leafpad](https://en.wikipedia.org/wiki/Leafpad "wikipedia:Leafpad")** — 移植到 GTK+ 上的 Notepad, 致力于简单。

	[http://tarot.freeshell.org/leafpad/](http://tarot.freeshell.org/leafpad/) || [leafpad](https://www.archlinux.org/packages/?name=leafpad)

*   **Medit** — 编程专用。

	[http://mooedit.sourceforge.net/](http://mooedit.sourceforge.net/) || [medit](https://www.archlinux.org/packages/?name=medit)

*   **[Mousepad](https://en.wikipedia.org/wiki/Xfce#Leafpad "wikipedia:Xfce")** — Xfce 桌面环境自带的文本编辑器

	[http://www.xfce.org/](http://www.xfce.org/) || [mousepad](https://www.archlinux.org/packages/?name=mousepad)

*   **[Nedit](https://en.wikipedia.org/wiki/NEdit "wikipedia:NEdit")** — [lesstif](https://www.archlinux.org/packages/?name=lesstif) 桌面环境自带的文本编辑器。

	[http://www.nedit.org/](http://www.nedit.org/) || [nedit](https://www.archlinux.org/packages/?name=nedit)

*   **[Pluma](/index.php/MATE "MATE")** — MATE 桌面环境自带的文本编辑器。

	[http://mate-desktop.org](http://mate-desktop.org) || [pluma](https://www.archlinux.org/packages/?name=pluma)

*   **[PyRoom](https://en.wikipedia.org/wiki/PyRoom "wikipedia:PyRoom")** — 致力于专心致志的 PyGTK 文本编辑器，又克隆自鲜为人知的 WriteRoom 。

	[http://pyroom.org/](http://pyroom.org/) || [pyroom](https://aur.archlinux.org/packages/pyroom/)

*   **QSciTE** — Qt 版本的 SciTE.

	[http://code.google.com/p/qscite/](http://code.google.com/p/qscite/) || [qscite](https://aur.archlinux.org/packages/qscite/)

*   **QXmlEdit** — 简单可用的 Qt XML 编辑器，XSD 查看器。

	[http://code.google.com/p/qxmledit/](http://code.google.com/p/qxmledit/) || [qxmledit](https://aur.archlinux.org/packages/qxmledit/)

*   **[Sam](https://en.wikipedia.org/wiki/Sam_(text_editor) "wikipedia:Sam (text editor)")** — 极简主义，同时包含图形用户界面，一门强大的命令行语言，远程编辑功能，由 Eob Pike 开发而成。

	[http://sam.cat-v.org](http://sam.cat-v.org) || [plan9port](https://www.archlinux.org/packages/?name=plan9port) or [9base](https://www.archlinux.org/packages/?name=9base)

*   **[SciTE](https://en.wikipedia.org/wiki/SciTE "wikipedia:SciTE")** — 常用来编译及运行程序。

	[http://scintilla.org/SciTE.html](http://scintilla.org/SciTE.html) || [scite](https://www.archlinux.org/packages/?name=scite)

*   **Scribes** — 终极，最小，即简单与强悍的合体。

	[http://scribes.sourceforge.net](http://scribes.sourceforge.net) || [scribes](https://www.archlinux.org/packages/?name=scribes)

*   **[Sublime Text 2](https://en.wikipedia.org/wiki/Sublime_Text "wikipedia:Sublime Text")** — 闭源，由 C++ 和 Python 编写而成，集成众多高级功能插件之大成，却难得地一直保持轻量流畅的高水准。

	[http://sublimetext.com](http://sublimetext.com) || [sublime-text](https://aur.archlinux.org/packages/sublime-text/)

*   **Tea** — 基于 Qt, 编辑富文本用。

	[http://tea-editor.sourceforge.net/](http://tea-editor.sourceforge.net/) || [tea](https://www.archlinux.org/packages/?name=tea)

*   **XEdit** — Simple text editor for the X Window System.

	[http://www.x.org/wiki/](http://www.x.org/wiki/) || [xorg-xedit](https://www.archlinux.org/packages/?name=xorg-xedit)

##### 协同式文本编辑器

*   **Gobby** — 支持在同一界面编辑多文档，多人聊天。

	[http://gobby.0x539.de](http://gobby.0x539.de) || [gobby](https://www.archlinux.org/packages/?name=gobby)

### 阅读与浏览

#### 电子书阅读

**Note:** Some [PDF and DjVu viewers](#PDF_and_DjVu) also support other e-book formats.

*   **[Calibre](https://en.wikipedia.org/wiki/Calibre_(software) "wikipedia:Calibre (software)")** — E-book library management application that can also convert between different formats and sync with a variety of e-book readers. Supported formats include CBZ, CBR, CBC, CHM, DJVU, EPUB, FictionBook, HTML, HTMLZ, LIT, LRF, Mobipocket, ODT, PDF, PRC, PDB, PML, RB, RTF, SNB, TCR, TXT and TXTZ.

	[http://calibre-ebook.com/](http://calibre-ebook.com/) || [calibre](https://www.archlinux.org/packages/?name=calibre)

*   **Cool Reader** — E-book viewer with many supported formats such as EPUB (non-DRM), FictionBook, TXT, RTF, HTML, CHM and TCR.

	[http://crengine.sourceforge.net/](http://crengine.sourceforge.net/) || [coolreader](https://aur.archlinux.org/packages/coolreader/)

*   **epub** — 使用Python和Curses的控制台EPUB阅读器。

	[https://pypi.python.org/pypi/epub](https://pypi.python.org/pypi/epub) || [python-epub](https://aur.archlinux.org/packages/python-epub/)

*   **[FBReader](https://en.wikipedia.org/wiki/FBReader "wikipedia:FBReader")** — E-book viewer with many supported formats such as EPUB, FictionBook, HTML, plucker, PalmDoc, zTxt, TCR, CHM, RTF, OEB, Mobipocket (non-DRM) and TXT.

	[http://fbreader.org/](http://fbreader.org/) || [fbreader](https://www.archlinux.org/packages/?name=fbreader)

*   **pPub** — 简单的EPUB阅读器使用 Python、 GTK3 和 WebKit。

	[https://github.com/sakisds/pPub](https://github.com/sakisds/pPub) || [ppub](https://aur.archlinux.org/packages/ppub/)

*   **[Sigil](https://en.wikipedia.org/wiki/Sigil_(application) "wikipedia:Sigil (application)")** — WYSIWYG ebook editor.

	[http://sigil-ebook.com/](http://sigil-ebook.com/) || [sigil](https://www.archlinux.org/packages/?name=sigil)

##### 书架

for more collection apps, see also [Multimedia#Collection managers](/index.php/Multimedia#Collection_managers "Multimedia")

*   **Alexandria** — GNOME application to help manage your book collection.

	[http://alexandria.rubyforge.org/](http://alexandria.rubyforge.org/) || [alexandria](https://aur.archlinux.org/packages/alexandria/)

*   **[Koha](https://en.wikipedia.org/wiki/Koha_(software) "wikipedia:Koha (software)")** — Open source Integrated Library System (ILS), used world-wide by public, school and special libraries.

	[http://koha-community.org/](http://koha-community.org/) || [koha](https://aur.archlinux.org/packages/koha/)

#### PDF 和 DjVu

**Note:** [PDF forms](https://en.wikipedia.org/wiki/Portable_Document_Format#Interactive_elements "wikipedia:Portable Document Format") support:

*   [acroread](https://aur.archlinux.org/packages/acroread/) is able to save both AcroForms and XFA forms into PDF files.
*   Poppler-based readers such as [evince](https://www.archlinux.org/packages/?name=evince) and [kdegraphics-okular](https://www.archlinux.org/packages/?name=kdegraphics-okular) support AcroForms, but not full XFA forms. [[4]](https://bugs.freedesktop.org/show_bug.cgi?id=18935) [[5]](https://bugs.launchpad.net/ubuntu/+source/poppler/+bug/321720)

See also [Wikipedia:List of PDF software](https://en.wikipedia.org/wiki/List_of_PDF_software "wikipedia:List of PDF software") and [Wikipedia:DjVu](https://en.wikipedia.org/wiki/DjVu "wikipedia:DjVu").

##### 终端

*   **fbpdf** — Small framebuffer PDF and DjVu viewer based off of MuPDF, with [Vim](/index.php/Vim "Vim") keybindings and written in C

	[http://repo.or.cz/w/fbpdf.git](http://repo.or.cz/w/fbpdf.git) || [fbpdf-git](https://aur.archlinux.org/packages/fbpdf-git/)

*   **jfbview** — Framebuffer PDF and image viewer. Features include Vim-like controls, zoom-to-fit, a TOC (outline) view, fast multi-threaded rendering and asynchronous pre-caching. Originally a fork of *fbpdf* called *jfbpdf*, now completely rewritten.

	[http://seasonofcode.com/pages/jfbview.html](http://seasonofcode.com/pages/jfbview.html) || [jfbview](https://aur.archlinux.org/packages/jfbview/)

##### 图形化界面

**Note:** Some [web browsers](/index.php/List_of_applications/Internet#Web_browsers "List of applications/Internet") have support for displaying PDF files, either built-in or via plugin.

*   **acroread** — A PDF file viewer offered by Adobe (closed source).

	[http://www.adobe.com/products/reader.html](http://www.adobe.com/products/reader.html) || [acroread](https://aur.archlinux.org/packages/acroread/)

*   **apvlv** — Lightweight PDF/DjVu/UMD/TXT viewer with [Vim](/index.php/Vim "Vim") keybindings.

	[http://naihe2010.github.com/apvlv/](http://naihe2010.github.com/apvlv/) || [apvlv](https://www.archlinux.org/packages/?name=apvlv)

*   **Atril** — Simple multi-page document viewer for MATE.

	[https://github.com/mate-desktop/atril](https://github.com/mate-desktop/atril) || [atril](https://www.archlinux.org/packages/?name=atril)

*   **ePDFView** — Free lightweight PDF document viewer using the Poppler and GTK+ libraries. Development stopped.

	[http://freecode.com/projects/epdfview](http://freecode.com/projects/epdfview) || [epdfview](https://www.archlinux.org/packages/?name=epdfview)

*   **[Evince](https://en.wikipedia.org/wiki/Evince "wikipedia:Evince")** — Document viewer for multiple document formats. Supports PDF, PostScript, DjVu, TIFF and DVI.

	[https://wiki.gnome.org/Apps/Evince](https://wiki.gnome.org/Apps/Evince) || [evince](https://www.archlinux.org/packages/?name=evince)

*   **[Foxit Reader](https://en.wikipedia.org/wiki/Foxit_Reader "wikipedia:Foxit Reader")** — Small, fast (compared to Acrobat) PDF viewer. (closed source)

	[http://www.foxitsoftware.com/pdf/desklinux/](http://www.foxitsoftware.com/pdf/desklinux/) || [foxitreader](https://aur.archlinux.org/packages/foxitreader/)

*   **gv** — Graphical user interface for the Ghostscript interpreter that allows to view and navigate through PostScript and PDF documents.

	[http://www.gnu.org/software/gv/](http://www.gnu.org/software/gv/) || [gv](https://www.archlinux.org/packages/?name=gv)

*   **[llpp](/index.php/Llpp "Llpp")** — Very fast PDF reader based off of MuPDF, that supports continuous page scrolling, bookmarking, and text search through the whole document.

	[http://repo.or.cz/w/llpp.git](http://repo.or.cz/w/llpp.git) || [llpp](https://aur.archlinux.org/packages/llpp/)

*   **[MuPDF](https://en.wikipedia.org/wiki/MuPDF "wikipedia:MuPDF")** — Very fast PDF and XPS viewer and toolkit written in portable C. Features CJK font support.

	[http://mupdf.com](http://mupdf.com) || [mupdf](https://www.archlinux.org/packages/?name=mupdf)

*   **[Okular](https://en.wikipedia.org/wiki/Okular "wikipedia:Okular")** — Universal PDF viewer for KDE.

	[http://okular.kde.org/](http://okular.kde.org/) || [kdegraphics-okular](https://www.archlinux.org/packages/?name=kdegraphics-okular)

*   **PdfMod** — You can reorder, rotate, and remove pages, export images from a document, edit the title, subject, author, and keywords, and combine documents via drag and drop.

	[https://wiki.gnome.org/Apps/PdfMod](https://wiki.gnome.org/Apps/PdfMod) || [pdfmod](https://www.archlinux.org/packages/?name=pdfmod)

*   **PDF Studio** — All-in-one PDF editor similar to Adobe Acrobat (proprietary).

	[http://www.qoppa.com/pdfstudio/](http://www.qoppa.com/pdfstudio/) || [pdfstudio](https://aur.archlinux.org/packages/pdfstudio/)

*   **qpdfview** — Tabbed document viewer. It uses Poppler for PDF support, libspectre for PS support, DjVuLibre for DjVu support, CUPS for printing support and the Qt toolkit for its interface.

	[https://launchpad.net/qpdfview](https://launchpad.net/qpdfview) || [qpdfview](https://aur.archlinux.org/packages/qpdfview/)

*   **[Xournal](https://en.wikipedia.org/wiki/Xournal "wikipedia:Xournal")** — Pdf viewer/note taking application.

	[http://xournal.sourceforge.net/](http://xournal.sourceforge.net/) || [xournal](https://www.archlinux.org/packages/?name=xournal)

*   **[Xpdf](https://en.wikipedia.org/wiki/Xpdf "wikipedia:Xpdf")** — Viewer that can decode LZW and read encrypted PDFs.

	[http://www.foolabs.com/xpdf/](http://www.foolabs.com/xpdf/) || [xpdf](https://www.archlinux.org/packages/?name=xpdf)

*   **[zathura](https://en.wikipedia.org/wiki/Zathura_(document_viewer) "wikipedia:Zathura (document viewer)")** — Highly customizable and functional PDF/DjVu/PostScript/ComicBook viewer (plugin based).

	[http://pwmt.org/projects/zathura/](http://pwmt.org/projects/zathura/) || [zathura](https://www.archlinux.org/packages/?name=zathura) [zathura-pdf-mupdf](https://www.archlinux.org/packages/?name=zathura-pdf-mupdf) [zathura-djvu](https://www.archlinux.org/packages/?name=zathura-djvu)

#### 虚拟分页器

See also [Wikipedia:Terminal pager](https://en.wikipedia.org/wiki/Terminal_pager "wikipedia:Terminal pager").

*   [more](https://en.wikipedia.org/wiki/More_(command) — A simple and feature-light pager. It is a part of the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package.
*   **[less](/index.php/Core_utilities#less "Core utilities")** — A program similar to more, but with support for both forward and backward scrolling, as well as partial loading of files.

	[http://www.gnu.org/software/less](http://www.gnu.org/software/less) || [less](https://www.archlinux.org/packages/?name=less)

*   **less-mouse** — less with mouse scrolling support. It is present in the AUR as [less-mouse](https://aur.archlinux.org/packages/less-mouse/).
*   **[most](https://en.wikipedia.org/wiki/Most_(Unix) "wikipedia:Most (Unix)")** — A pager with support for multiple windows, left and right scrolling, and built-in colour support

	[http://www.jedsoft.org/most/](http://www.jedsoft.org/most/) || [most](https://www.archlinux.org/packages/?name=most)

*   **mcview** — A pager with mouse and colour support. It is bundled with midnight commander.

	[http://www.midnight-commander.org](http://www.midnight-commander.org) || [mc](https://www.archlinux.org/packages/?name=mc)

*   **vimpager** — A script that turns vim into a pager. As a result, you get various vim features such as colour schemes, mouse support, split screens, etc.

	[https://github.com/rkitover/vimpager](https://github.com/rkitover/vimpager) || [vimpager](https://www.archlinux.org/packages/?name=vimpager)

#### CHM

See also [Wikipedia:Microsoft Compiled HTML Help](https://en.wikipedia.org/wiki/Microsoft_Compiled_HTML_Help "wikipedia:Microsoft Compiled HTML Help").

*   **ChmSee** — CHM viewer based on xulrunner.

	[https://code.google.com/p/chmsee/](https://code.google.com/p/chmsee/) || [chmsee](https://aur.archlinux.org/packages/chmsee/)

*   **Kchmviewer** — Qt-based CHM viewer that uses chmlib and borrows some ideas from xchm. It does not depend on [KDE](/index.php/KDE "KDE"), but it can be compiled to integrate with it.

	[http://www.ulduzsoft.com/kchmviewer/](http://www.ulduzsoft.com/kchmviewer/) || [kchmviewer](https://www.archlinux.org/packages/?name=kchmviewer)

*   **[xCHM](https://en.wikipedia.org/wiki/xCHM "wikipedia:xCHM")** — 轻量级 CHM 查看器中，基于 chmlib。

	[http://xchm.sf.net/](http://xchm.sf.net/) || [xchm](https://www.archlinux.org/packages/?name=xchm)

#### 漫画

*   **[Comix](https://en.wikipedia.org/wiki/Comix_(software) "wikipedia:Comix (software)")** — GTK2 image viewer specifically designed to handle comic book archives. Also includes library manager. It's development was stopped in 2009 and moved to MComix.

	[http://comix.sourceforge.net/](http://comix.sourceforge.net/) || [comix](https://aur.archlinux.org/packages/comix/)

*   **[MComix](https://en.wikipedia.org/wiki/MComix "wikipedia:MComix")** — GTK2 image viewer specifically designed to handle comic book archives (fork of Comix). Also includes library manager.

	[http://sourceforge.net/projects/mcomix/](http://sourceforge.net/projects/mcomix/) || [mcomix](https://www.archlinux.org/packages/?name=mcomix)

*   **QComicBook** — Lightweight comic book viewer written in C++ and Qt4.

	[http://qcomicbook.org/](http://qcomicbook.org/) || [qcomicbook](https://aur.archlinux.org/packages/qcomicbook/)

*   **YACReader** — Comic book viewer written in C++ and Qt5\. Comes with YACReaderLibrary for managing comics.

	[http://yacreader.com/](http://yacreader.com/) || [yacreader](https://aur.archlinux.org/packages/yacreader/)

### 扫描

See [SANE#Install a frontend](/index.php/SANE#Install_a_frontend "SANE").

### OCR

See also [Wikipedia:Comparison of optical character recognition software](https://en.wikipedia.org/wiki/Comparison_of_optical_character_recognition_software "wikipedia:Comparison of optical character recognition software").

#### 引擎

*   **CuneiForm** — Command line OCR system originally developed and open sourced by Cognitive technologies. Supported languages: eng, ger, fra, rus, swe, spa, ita, ruseng, ukr, srp, hrv, pol, dan, por, dut, cze, rum, hun, bul, slo, lav, lit, est, tur.

	[https://launchpad.net/cuneiform-linux](https://launchpad.net/cuneiform-linux) || [cuneiform](https://www.archlinux.org/packages/?name=cuneiform)

*   **GOCR/JOCR** — OCR engine which also supports barcode recognition.

	[http://jocr.sourceforge.net/](http://jocr.sourceforge.net/) || [gocr](https://www.archlinux.org/packages/?name=gocr)

*   **Ocrad** — OCR program based on a feature extraction method.

	[http://www.gnu.org/software/ocrad/](http://www.gnu.org/software/ocrad/) || [ocrad](https://www.archlinux.org/packages/?name=ocrad)

*   **Tesseract** — Accurate open source OCR engine. Package splitted, you need install some datafiles for each language ([tesseract-data-eng](https://www.archlinux.org/packages/?name=tesseract-data-eng) for example).

	[http://code.google.com/p/tesseract-ocr/](http://code.google.com/p/tesseract-ocr/) || [tesseract](https://www.archlinux.org/packages/?name=tesseract)

#### 布局分析与用户界面

*   **gImageReader** — Graphical GTK frontend to Tesseract.

	[http://gimagereader.sourceforge.net/](http://gimagereader.sourceforge.net/) || [gimagereader](https://aur.archlinux.org/packages/gimagereader/)

*   **gscan2pdf** — Scans, runs an OCR engine, minor post-processing, creates a document.

	[http://gscan2pdf.sourceforge.net/](http://gscan2pdf.sourceforge.net/) || [gscan2pdf](https://aur.archlinux.org/packages/gscan2pdf/)

*   **OCRFeeder** — Python GUI for Gnome which performs document analysis and rendition, and can use either CuneiForm, GOCR, Ocrad or Tesseract as OCR engines. It can import from PDF or image files, and export to HTML or OpenDocument.

	[https://wiki.gnome.org/Apps/OCRFeeder](https://wiki.gnome.org/Apps/OCRFeeder) || [ocrfeeder](https://www.archlinux.org/packages/?name=ocrfeeder)

*   **OCRopy** — OCR *platform*, modules exist for document layout analysis, OCR engines (it can use Tesseract or its own engine), natural language modeling, etc.

	[https://github.com/tmbdev/ocropy](https://github.com/tmbdev/ocropy) || [ocropy](https://aur.archlinux.org/packages/ocropy/)

*   **[YAGF](/index.php/YAGF "YAGF")** — Graphical interface for the CuneiForm text recognition program on the Linux platform.

	[http://symmetrica.net/cuneiform-linux/yagf-en.html](http://symmetrica.net/cuneiform-linux/yagf-en.html) || [yagf](https://www.archlinux.org/packages/?name=yagf)

### 笔记

参见 [Wikipedia:Comparison of notetaking software](https://en.wikipedia.org/wiki/Comparison_of_notetaking_software "wikipedia:Comparison of notetaking software").

#### 命令行

*   **hnb** — 当场处理众多类型数据（地址，待做清单，点子和书评等等）的程序。

	[http://hnb.sourceforge.net/](http://hnb.sourceforge.net/) || [hnb](https://aur.archlinux.org/packages/hnb/)

*   **pynote** — 通过命令行整理笔记。通过可读的 JSON 文件来储存笔记，还提供了版本控制。

	[https://pypi.python.org/pypi/pynote](https://pypi.python.org/pypi/pynote) || [pynote](https://aur.archlinux.org/packages/pynote/)

#### 图形环境

*   **[BasKet](https://en.wikipedia.org/wiki/BasKet_Note_Pads "wikipedia:BasKet Note Pads")** — 能够整理，分享和撰写笔记的应用程序。它支持不少玩意，就像待做清单，链接，图片以及其它等等，就像剪贴本一样。

	[http://basket.kde.org/](http://basket.kde.org/) || [basket](https://www.archlinux.org/packages/?name=basket)

*   **Cherrytree** — 阶层式笔记本程序，支持富文本，语法高亮，以 XML 或数据库文件储存数据。

	[http://giuspen.com/cherrytree/](http://giuspen.com/cherrytree/) || [cherrytree](https://www.archlinux.org/packages/?name=cherrytree)

*   **[Gnote](https://en.wikipedia.org/wiki/Gnote "wikipedia:Gnote")** — 迁移 Tomboy 到 C++ 的一种尝试。

	[http://live.gnome.org/Gnote](http://live.gnome.org/Gnote) || [gnote](https://www.archlinux.org/packages/?name=gnote)

*   **KeepNote** — 支持富文本，跨平台的 GTK+ 笔记应用程序

	[http://keepnote.org](http://keepnote.org) || [keepnote](https://www.archlinux.org/packages/?name=keepnote)

*   **[KJots](https://en.wikipedia.org/wiki/KJots "wikipedia:KJots")** — 手动处理纷杂笔记的小程序，从属 [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/) 。

	[http://www.kde.org/applications/utilities/kjots/](http://www.kde.org/applications/utilities/kjots/) || [kjots](https://www.archlinux.org/packages/?name=kjots)

*   **NoteCase** — 阶层式笔记的绿色软件，由 C++ 及 GTK+ 编写成。

	[notecase](https://aur.archlinux.org/packages/notecase/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[org-mode](https://en.wikipedia.org/wiki/org-mode "wikipedia:org-mode")** — [Emacs](/index.php/Emacs "Emacs") 特有的笔记模式，专于项目的计划及编写。

	[http://orgmode.org](http://orgmode.org) || [emacs-org-mode](https://aur.archlinux.org/packages/emacs-org-mode/)

*   **nixnote** — evernote的第三方开源程序（以前名叫nevernote）

	[http://www.sourceforge.net/projects/nevernote](http://www.sourceforge.net/projects/nevernote) || [nixnote_beta](https://aur.archlinux.org/packages/nixnote_beta/)

*   **[Tomboy](https://en.wikipedia.org/wiki/Tomboy_(software) "wikipedia:Tomboy (software)")** — Linux 和 Unix 上的桌面笔记程序，可以 wiki 形式连接众多笔记。

	[http://projects.gnome.org/tomboy/](http://projects.gnome.org/tomboy/) || [tomboy](https://www.archlinux.org/packages/?name=tomboy)

*   **wiznote** — 基于开源，跨平台和云的笔记程序

	[http://www.wiznote.com/](http://www.wiznote.com/) || [wiznote](https://www.archlinux.org/packages/?name=wiznote)

*   **[zim](/index.php/Zim "Zim")** — 所见即所得的文本编辑器，剑指桌面端的维基概念。

	[http://zim-wiki.org/](http://zim-wiki.org/) || [zim](https://www.archlinux.org/packages/?name=zim)

*   **znotes** — A lightweight crossplatform application for notes managment with simple interface, use qt4 libraries.

	[http://znotes.sourceforge.net/](http://znotes.sourceforge.net/) || [znotes](https://aur.archlinux.org/packages/znotes/)

### Mind-mapping tools

*   **FreeMind** — Premier free mind-mapping software written in Java.

	[http://freemind.sourceforge.net](http://freemind.sourceforge.net) || [freemind](https://www.archlinux.org/packages/?name=freemind)

*   **Freeplane** — Free and open source software application that supports thinking, sharing information and getting things done at work, in school and at home. The software can be used for mind mapping and analyzing the information contained in mind maps.

	[http://freeplane.sourceforge.net](http://freeplane.sourceforge.net) || [freeplane](https://aur.archlinux.org/packages/freeplane/)

*   **Semantik** — A mind-mapping application for KDE.

	[https://ita1024.github.io/semantik/](https://ita1024.github.io/semantik/) || [semantik](https://aur.archlinux.org/packages/semantik/)

*   **TreeSheets** — The ultimate replacement for spreadsheets, mind mappers, outliners, PIMs, text editors and small databases.

	[http://strlen.com/treesheets/](http://strlen.com/treesheets/) || [treesheets-git](https://aur.archlinux.org/packages/treesheets-git/)

*   **View Your Mind** — Tool to generate and manipulate maps which show your thoughts. Such maps can help you to improve your creativity and effectivity. You can use them for time management, to organize tasks, to get an overview over complex contexts, to sort your ideas etc.

	[http://www.insilmaril.de/vym/](http://www.insilmaril.de/vym/) || [vym](https://www.archlinux.org/packages/?name=vym)

*   **Visual Understanding Environment** — Open Source project focused on creating flexible tools for managing and integrating digital resources in support of teaching, learning and research.

	[http://vue.tufts.edu](http://vue.tufts.edu) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **XMind** — Brainstorming and mind mapping application. It provides a rich set of different visualization styles, and allows sharing of created mind maps via their website.

	[http://www.xmind.net](http://www.xmind.net) || [xmind](https://www.archlinux.org/packages/?name=xmind)

### 字符选择器

*   **GNOME Characters** — Character map application for GNOME

	[https://wiki.gnome.org/Design/Apps/CharacterMap](https://wiki.gnome.org/Design/Apps/CharacterMap) || [gnome-characters](https://www.archlinux.org/packages/?name=gnome-characters)

*   **gucharmap** — A GTK+ 3 Character Selector, distributed with GNOME desktop.

	[https://wiki.gnome.org/Apps/Gucharmap](https://wiki.gnome.org/Apps/Gucharmap) || [gucharmap](https://www.archlinux.org/packages/?name=gucharmap)

*   **kdeutils-kcharselect** — A tool to select special characters from all installed fonts and copy them into the clipboard. Distributed with KDE.

	[http://utils.kde.org/projects/kcharselect/](http://utils.kde.org/projects/kcharselect/) || [kcharselect](https://www.archlinux.org/packages/?name=kcharselect)

### Stylus notes taking

*   **Write** — a word processor for hand writing.

	[http://www.styluslabs.com/](http://www.styluslabs.com/) || [write_stylus](https://aur.archlinux.org/packages/write_stylus/)

*   **Gournal** — note-taking application written for usage on Tablet-PC, written in perl.

	[http://www.adebenham.com/old-stuff/gournal/](http://www.adebenham.com/old-stuff/gournal/) || [gournal](https://aur.archlinux.org/packages/gournal/)

*   **Xournal** — an application for notetaking, sketching, keeping a journal using a stylus.

	[http://xournal.sourceforge.net/](http://xournal.sourceforge.net/) || [xournal](https://www.archlinux.org/packages/?name=xournal)

### 参考书目管理

参见 [Wikipedia:Comparison of reference management software](https://en.wikipedia.org/wiki/Comparison_of_reference_management_software "wikipedia:Comparison of reference management software").

*   **Bibus** — 一个可以直接在OpenOffice.org/LibreOffice中插入引用并生成文献索引的书目数据库.

	[http://bibus-biblio.sourceforge.net](http://bibus-biblio.sourceforge.net) || [bibus](https://aur.archlinux.org/packages/bibus/)

*   **DocEar** — Docear 是一个学术文献套件, 用于搜索，组织和创造的学术文献, 建立在思维导图软件 Freeplane 和 文件参考管理软件JabRef上.

	[https://www.docear.org](https://www.docear.org) || [docear](https://aur.archlinux.org/packages/docear/)

*   **JabRef** — BibTeX的GUI前端, 由Java写成.

	[http://jabref.sourceforge.net](http://jabref.sourceforge.net) || [jabref](https://aur.archlinux.org/packages/jabref/)

*   **Zotero** — Zotero 单机版. 是一个免费的，易于使用的工具来帮助您收集，整理，引用和共享研究资源.

	[http://www.zotero.org](http://www.zotero.org) || [zotero](https://aur.archlinux.org/packages/zotero/)

## 安全

For detailed guides, see the main ArchWiki page, [Security](/index.php/Security "Security").

### 防火墙

See the main article: [Firewalls](/index.php/Firewalls "Firewalls").

See also [Wikipedia:Comparison of firewalls](https://en.wikipedia.org/wiki/Comparison_of_firewalls "wikipedia:Comparison of firewalls").

### 网络安全

*   **[Arpwatch](https://en.wikipedia.org/wiki/Arpwatch "wikipedia:Arpwatch")** — Tool that monitors ethernet activity and keeps a database of Ethernet/IP address pairings.

	[http://ee.lbl.gov/](http://ee.lbl.gov/) || [arpwatch](https://www.archlinux.org/packages/?name=arpwatch)

*   **Bro** — Powerful network analysis framework that is much different from the typical IDS you may know.

	[https://www.bro.org/](https://www.bro.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **EtherApe** — Graphical network monitor for Unix modeled after etherman. Featuring link layer, IP and TCP modes, it displays network activity graphically. Hosts and links change in size with traffic. Color coded protocols display.

	[http://etherape.sourceforge.net/](http://etherape.sourceforge.net/) || [etherape](https://www.archlinux.org/packages/?name=etherape)

*   **[Honeyd](/index.php/Honeyd "Honeyd")** — Tool that allows the user to set up and run multiple virtual hosts on a computer network.

	[http://www.honeyd.org/](http://www.honeyd.org/) || [honeyd](https://aur.archlinux.org/packages/honeyd/)

*   **IPTraf** — Console-based network monitoring utility.

	[https://fedorahosted.org/iptraf-ng/](https://fedorahosted.org/iptraf-ng/) || [iptraf-ng](https://www.archlinux.org/packages/?name=iptraf-ng)

*   **Kismet** — 802.11 layer2 wireless network detector, sniffer, and intrusion detection system.

	[http://www.kismetwireless.net/](http://www.kismetwireless.net/) || [kismet](https://www.archlinux.org/packages/?name=kismet)

*   **Nemesis** — Command-line network packet crafting and injection utility.

	[http://nemesis.sourceforge.net/](http://nemesis.sourceforge.net/) || [nemesis](https://www.archlinux.org/packages/?name=nemesis)

*   **[Nmap](/index.php/Nmap "Nmap")** — Security scanner used to discover hosts and services on a computer network, thus creating a "map" of the network.

	[http://nmap.org/](http://nmap.org/) || [nmap](https://www.archlinux.org/packages/?name=nmap)

*   **[Ntop](/index.php/Ntop "Ntop")** — Network probe that shows network usage in a way similar to what top does for processes.

	[http://www.ntop.org/](http://www.ntop.org/) || [ntop](https://www.archlinux.org/packages/?name=ntop)

*   **[Snort](/index.php/Snort "Snort")** — Network intrusion prevention and detection system.

	[http://www.snort.org/](http://www.snort.org/) || [snort](https://aur.archlinux.org/packages/snort/)

*   **[Sshguard](/index.php/Sshguard "Sshguard")** — Daemon that protects SSH and other services against brute-force attacts, similar to Fail2ban.

	[http://www.sshguard.net/](http://www.sshguard.net/) || [sshguard](https://www.archlinux.org/packages/?name=sshguard)

*   **[Suricata](/index.php/Suricata "Suricata")** — High performance Network IDS, IPS and Network Security Monitoring engine.

	[http://suricata-ids.org/](http://suricata-ids.org/) || [suricata](https://aur.archlinux.org/packages/suricata/)

*   **[Tcpdump](https://en.wikipedia.org/wiki/tcpdump "wikipedia:tcpdump")** — Common console-based packet analyzer that allows the user to intercept and display TCP/IP and other packets being transmitted or received over a network.

	[http://www.tcpdump.org/](http://www.tcpdump.org/) || [tcpdump](https://www.archlinux.org/packages/?name=tcpdump)

*   **[vnStat](/index.php/VnStat "VnStat")** — Console-based network traffic monitor that keeps a log of network traffic for the selected interfaces.

	[http://humdi.net/vnstat/](http://humdi.net/vnstat/) || [vnstat](https://www.archlinux.org/packages/?name=vnstat)

*   **[Wireshark](/index.php/Wireshark "Wireshark")** — Network protocol analyzer that lets you capture and interactively browse the traffic running on a computer network.

	[http://www.wireshark.org/](http://www.wireshark.org/) || [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk)

### 威胁与漏洞探测

*   **AFICK** — Security tool that allows to monitor the changes on your files systems, and so can detect intrusions.

	[http://afick.sourceforge.net/](http://afick.sourceforge.net/) || [afick](https://aur.archlinux.org/packages/afick/)

*   **Lynis** — Security and system auditing tool to harden Unix/Linux systems.

	[https://cisofy.com/lynis/](https://cisofy.com/lynis/) || [lynis](https://www.archlinux.org/packages/?name=lynis)

*   **[Metasploit Framework](/index.php/Metasploit_Framework "Metasploit Framework")** — An advanced open-source platform for developing, testing, and using exploit code.

	[http://www.metasploit.com/](http://www.metasploit.com/) || [metasploit](https://www.archlinux.org/packages/?name=metasploit)

*   **[Nessus](/index.php/Nessus "Nessus")** — Comprehensive vulnerability scanning program.

	[http://www.nessus.org/products/nessus](http://www.nessus.org/products/nessus) || [nessus](https://aur.archlinux.org/packages/nessus/)

*   **[OpenVAS](/index.php/OpenVAS "OpenVAS")** — Framework of several services and tools offering a comprehensive and powerful vulnerability scanning and vulnerability management solution. FOSS Nessus fork.

	[http://www.openvas.org/](http://www.openvas.org/) || [openvas](https://www.archlinux.org/groups/x86_64/openvas/)

*   **Osiris** — Tool for monitoring system integrity and changes across a network.

	[https://launchpad.net/osiris](https://launchpad.net/osiris) || [osiris](https://www.archlinux.org/packages/?name=osiris)

*   **OSSEC** — Open Source Host-based Intrusion Detection System that performs log analysis, file integrity checking, policy monitoring, rootkit detection, real-time alerting and active response.

	[http://www.ossec.net/](http://www.ossec.net/) || [ossec-agent](https://aur.archlinux.org/packages/ossec-agent/) [ossec-local](https://aur.archlinux.org/packages/ossec-local/) [ossec-server](https://aur.archlinux.org/packages/ossec-server/)

*   **Samhain** — Host-based intrusion detection system (HIDS) provides file integrity checking and log file monitoring/analysis, as well as rootkit detection, port monitoring, detection of rogue SUID executables, and hidden processes.

	[http://www.la-samhna.de/samhain/index.html](http://www.la-samhna.de/samhain/index.html) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **Tiger** — Security tool that can be use both as a security audit and intrusion detection system.

	[http://www.nongnu.org/tiger/](http://www.nongnu.org/tiger/) || [tiger](https://aur.archlinux.org/packages/tiger/)

*   **[Tripwire](https://en.wikipedia.org/wiki/Open_Source_Tripwire "wikipedia:Open Source Tripwire")** — Intrusion detection system.

	[http://tripwire.sourceforge.net/](http://tripwire.sourceforge.net/) || [tripwire](https://aur.archlinux.org/packages/tripwire/)

### 文件安全

*   **[AIDE](/index.php/AIDE "AIDE")** — File and directory integrity checker.

	[http://aide.sourceforge.net/](http://aide.sourceforge.net/) || [aide](https://www.archlinux.org/packages/?name=aide)

*   **Logcheck** — Simple utility which is designed to allow a system administrator to view the logfiles which are produced upon hosts under their control.

	[https://logcheck.alioth.debian.org/](https://logcheck.alioth.debian.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Logwatch](/index.php/Logwatch "Logwatch")** — Customizable log analysis system.

	[http://sourceforge.net/projects/logwatch/](http://sourceforge.net/projects/logwatch/) || [logwatch](https://www.archlinux.org/packages/?name=logwatch)

*   **OpenDLP** — OpenDLP is a free and open source, agent- and agentless-based, centrally-managed, massively distributable data loss prevention tool.

	[https://code.google.com/p/opendlp/](https://code.google.com/p/opendlp/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **Swatch** — Utility that can monitor just about any type of log.

	[http://swatch.sourceforge.net/](http://swatch.sourceforge.net/) || [swatch](https://aur.archlinux.org/packages/swatch/)

#### 反恶意软件

*   **chkrootkit** — Locally checks for signs of a rootkit.

	[http://www.chkrootkit.org/](http://www.chkrootkit.org/) || [chkrootkit](https://aur.archlinux.org/packages/chkrootkit/)

*   **[ClamAV](/index.php/ClamAV "ClamAV")** — Open source antivirus engine for detecting trojans, viruses, malware & other malicious threats.

	[http://www.clamav.net/](http://www.clamav.net/) || [clamav](https://www.archlinux.org/packages/?name=clamav)

*   **Linux Malware Detect** — Malware scanner designed around the threats faced in shared hosted environments.

	[https://www.rfxn.com/projects/linux-malware-detect/](https://www.rfxn.com/projects/linux-malware-detect/) || [maldet](https://aur.archlinux.org/packages/maldet/)

*   **Rootkit Hunter** — Checks machines for the presence of rootkits and other unwanted tools.

	[http://rkhunter.sourceforge.net/](http://rkhunter.sourceforge.net/) || [rkhunter](https://www.archlinux.org/packages/?name=rkhunter)

### 备份

See the main article: [Backup programs](/index.php/Backup_programs "Backup programs").

See also [Wikipedia:Comparison of backup software](https://en.wikipedia.org/wiki/Comparison_of_backup_software "wikipedia:Comparison of backup software").

### 锁屏

**Warning:** Only *sflock*, *physlock*, *Cinnamon Screensaver*, *MATE Screensaver* and *GNOME Screensaver* are able to block tty access.

*   **Cinnamon Screensaver** — Screen locker for the Cinnamon desktop.

	[https://github.com/linuxmint/cinnamon-screensaver](https://github.com/linuxmint/cinnamon-screensaver) || [cinnamon-screensaver](https://www.archlinux.org/packages/?name=cinnamon-screensaver)

*   **GNOME Screensaver** — Screen locker for the GNOME Flashback desktop.

	[https://wiki.gnome.org/Projects/GnomeScreensaver](https://wiki.gnome.org/Projects/GnomeScreensaver) || [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver)

*   **i3lock** — A simple screen locker. Provides user feedback, uses PAM authentication, supports DPMS. The background can be set to an image or solid color.

	[http://i3wm.org/i3lock/](http://i3wm.org/i3lock/) || [i3lock](https://www.archlinux.org/packages/?name=i3lock)

*   **i3lock-blur** — Fork of *i3lock* which can use your desktop with the blur effect applied as a background.

	[http://github.com/karulont/i3lock-blur](http://github.com/karulont/i3lock-blur) || [i3lock-blur](https://aur.archlinux.org/packages/i3lock-blur/)

*   **i3lock-wrapper** — A simple wrapper around *i3lock* which sets up a blurred screenshot of the desktop as a background image.

	[https://github.com/ashinkarov/i3-extras](https://github.com/ashinkarov/i3-extras) || [i3lock-wrapper](https://aur.archlinux.org/packages/i3lock-wrapper/)

*   **Light-locker** — A simple locker (forked from *gnome-screensaver*) that aims to have simple, sane, secure defaults and be well integrated with the desktop while not carrying any desktop-specific dependencies. It relies on [LightDM](/index.php/LightDM "LightDM") for locking and unlocking your session via ConsoleKit/UPower or *logind/systemd*

	[https://github.com/the-cavalry/light-locker](https://github.com/the-cavalry/light-locker) || [light-locker](https://www.archlinux.org/packages/?name=light-locker)

*   **MATE Screensaver** — Screensaver and locker for MATE Desktop Environment.

	[https://github.com/mate-desktop/mate-screensaver](https://github.com/mate-desktop/mate-screensaver) || [mate-screensaver](https://www.archlinux.org/packages/?name=mate-screensaver)

*   **physlock** — Screen and console locker.

	[https://github.com/muennich/physlock](https://github.com/muennich/physlock) || [physlock](https://aur.archlinux.org/packages/physlock/)

*   **sflock** — Simple screen locker utility for X, based on slock. Provides a very basic user feedback.

	[https://github.com/benruijl/sflock](https://github.com/benruijl/sflock) || [sflock-git](https://aur.archlinux.org/packages/sflock-git/)

*   **slock** — Very simple and lightweight X screen locker. Offers only a black background when locked, there are no animations or text fields.

	[http://tools.suckless.org/slock](http://tools.suckless.org/slock) || [slock](https://www.archlinux.org/packages/?name=slock)

*   **sxlock** — Fork of sflock with a few enhancements. Provides basic user feedback, uses PAM authentication, supports DPMS and RandR. Supports `sxlock.service` to lock the screen on suspend/hibernation. See the [README](https://github.com/lahwaacz/sxlock/blob/master/README.md) for more information.

	[https://github.com/lahwaacz/sxlock](https://github.com/lahwaacz/sxlock) || [sxlock-git](https://aur.archlinux.org/packages/sxlock-git/)

*   **vlock** — TTY locker. A mirror of the [original vlock](https://lists.archlinux.org/pipermail/aur-general/2013-July/024662.html) is available at [github](https://github.com/WorMzy/vlock).

	[http://www.kbd-project.org](http://www.kbd-project.org) || [kbd](https://www.archlinux.org/packages/?name=kbd)

*   **xlockmore** — Simple X11 screen lock with PAM support.

	[http://www.tux.org/~bagleyd/xlockmore.html](http://www.tux.org/~bagleyd/xlockmore.html) || [xlockmore](https://www.archlinux.org/packages/?name=xlockmore)

*   **[XScreenSaver](/index.php/XScreenSaver "XScreenSaver")** — Screen saver and locker for the X Window System.

	[http://www.jwz.org/xscreensaver/](http://www.jwz.org/xscreensaver/) || [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver)

*   **XSecureLock** — X11 screen lock utility designed with the primary goal of security.

	[https://github.com/google/xsecurelock](https://github.com/google/xsecurelock) || [xsecurelock-git](https://aur.archlinux.org/packages/xsecurelock-git/)

### Hash 校验

*   **GtkHash** — 生成摘记，计算校验的 GTK+ 工具

	[http://gtkhash.sourceforge.net/](http://gtkhash.sourceforge.net/) || [gtkhash](https://aur.archlinux.org/packages/gtkhash/)

*   **hashdeep** — 可对多文件计算 Hash, 生成摘记，跨平台的工具。

	[http://md5deep.sourceforge.net/](http://md5deep.sourceforge.net/) || [hashdeep](https://aur.archlinux.org/packages/hashdeep/)

*   **Parano** — 用于生成、编辑和校验 MD5 和 SFV 文件的 GNOME 前端

	[http://parano.berlios.de/](http://parano.berlios.de/) || [parano](https://aur.archlinux.org/packages/parano/)

*   **RHash** — Hash 校验工具，支持 SFV, CRC 等等，支持众多算法

	[http://rhash.anz.ru/](http://rhash.anz.ru/) || [rhash](https://www.archlinux.org/packages/?name=rhash)

*   **Quick Hash GUI** — 可在文本或硬盘递归地快速进行 Hash 的 GUI 工具

	[http://sourceforge.net/projects/quickhash/](http://sourceforge.net/projects/quickhash/) || [quickhash](https://aur.archlinux.org/packages/quickhash/)

*   **RHash** — Utility for verifying hash sums (SFV, CRC, etc). Supports lots of algorithms.

	[http://rhash.anz.ru/](http://rhash.anz.ru/) || [rhash](https://www.archlinux.org/packages/?name=rhash)

*   **MassHash** — A set of file hashing tools (both CLI and GTK+ GUI) written in Python. Supported algorithms include MD5, SHA-1, SHA-224, SHA-256, SHA-384, SHA-512.

	[http://jdleicher.github.io/MassHash/](http://jdleicher.github.io/MassHash/) || [masshash](https://aur.archlinux.org/packages/masshash/)

### 加密，签名与信息隐藏

*   **ccrypt** — A command-line utility for encrypting and decrypting files and streams.

	[http://ccrypt.sourceforge.net/](http://ccrypt.sourceforge.net/) || [ccrypt](https://www.archlinux.org/packages/?name=ccrypt)

*   **[GnuPG](/index.php/GnuPG "GnuPG")** — The GNU project's complete and free implementation of the OpenPGP standard as defined by RFC4880\. Free and Open Source replacement of PGP, mostly used for digital signing of packages.

	[http://gnupg.org/](http://gnupg.org/) || [gnupg](https://www.archlinux.org/packages/?name=gnupg)

*   **gzsteg** — A utiltiy that can hide data in gzip compressed files

	[http://www.nic.funet.fi/pub/crypt/steganography/](http://www.nic.funet.fi/pub/crypt/steganography/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=gzsteg)</small>

*   **silenteye** — A steganography application written in C++, use Qt4 library.

	[http://www.silenteye.org/](http://www.silenteye.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=silenteye)</small>

*   **snow** — Steganography program for concealing messages in text files

	[http://www.darkside.com.au/snow/](http://www.darkside.com.au/snow/) || [snow](https://aur.archlinux.org/packages/snow/)

*   **steghide** — A steganography utility that is able to hide data in various kinds of image and audio files.

	[http://steghide.sourceforge.net](http://steghide.sourceforge.net) || [steghide](https://www.archlinux.org/packages/?name=steghide)

*   **stegparty** — A steganography utility hides text by typoing text existing text files.

	[https://github.com/countrygeek/stegparty](https://github.com/countrygeek/stegparty) || [stegparty](https://aur.archlinux.org/packages/stegparty/)

### 密码管理

*   **Console Password Manager** — Curses based password manager using PGP-encryption.

	[http://github.com/comotion/cpm](http://github.com/comotion/cpm) || [cpm](https://aur.archlinux.org/packages/cpm/)

*   **Figaro's Password Manager 2** — GTK2 port of [Figaro's Password Manager](http://fpm.sourceforge.net/) with some new enhancements.

	[http://als.regnet.cz/fpm2/](http://als.regnet.cz/fpm2/) || [fpm2](https://aur.archlinux.org/packages/fpm2/)

*   **GPass** — Password manegement software for GNOME2 desktop.

	[http://projects.netlab.jp/gpass/](http://projects.netlab.jp/gpass/) || [gpass](https://aur.archlinux.org/packages/gpass/)

*   **GPassword Manager** — Simple, lightweight and cross-platform utility for managing and accessing passwords.

	[http://sourceforge.net/projects/gpasswordman/](http://sourceforge.net/projects/gpasswordman/) || [gpasswordman](https://aur.archlinux.org/packages/gpasswordman/)

*   **Gtkpass** — Gtkpass is a GTK and Libkpass-based password manager for KeePass 1.x databases.

	[https://sourceforge.net/projects/gtkpass/](https://sourceforge.net/projects/gtkpass/) || [gtkpass](https://aur.archlinux.org/packages/gtkpass/)

*   **Ked Password Manager** — A password manager that helps to manage large numbers of passwords.

	[http://kedpm.sourceforge.net](http://kedpm.sourceforge.net) || [kedpm](https://aur.archlinux.org/packages/kedpm/)

*   **[KeePass Password Safe](/index.php/KeePass "KeePass")** — Free open source Mono-based password manager, which helps you to manage your passwords in a secure way.

	[http://keepass.info/](http://keepass.info/) || [keepass](https://www.archlinux.org/packages/?name=keepass)

*   **KeePassC** — KeePassC is a curses-based password manager compatible to KeePass v.1.x and KeePassX.

	[https://raymontag.github.com/keepassc](https://raymontag.github.com/keepassc) || [keepassc](https://aur.archlinux.org/packages/keepassc/)

*   **KeePassX** — Free and open source Qt-based password manager (uses KeePass 1.x databases for storage).

	[http://www.keepassx.org/](http://www.keepassx.org/) || [keepassx](https://www.archlinux.org/packages/?name=keepassx)

*   **MyPasswords** — What you need for managing your passwords, including the passwords of your online accounts, bank accounts and ... with the corresponding URLs.

	[http://sourceforge.net/projects/mypasswords7/](http://sourceforge.net/projects/mypasswords7/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **MyPasswordSafe** — Easy-to-use QT based password manager, compatible with Password Safe files (and therefore pwsafe).

	[http://www.semanticgap.com/myps/](http://www.semanticgap.com/myps/) || [mypasswordsafe](https://aur.archlinux.org/packages/mypasswordsafe/)

*   **Pasaffe** — Easy to use password manager for Gnome with a Password Safe 3.0 compatible database.

	[https://launchpad.net/pasaffe](https://launchpad.net/pasaffe) || [pasaffe](https://aur.archlinux.org/packages/pasaffe/)

*   **[pass](/index.php/Pass "Pass")** — Simple console based password manager

	[http://www.passwordstore.org/](http://www.passwordstore.org/) || [pass](https://www.archlinux.org/packages/?name=pass)

*   **Password Gorilla** — A cross-platform password manager.

	[https://github.com/zdia/gorilla/wiki/](https://github.com/zdia/gorilla/wiki/) || [password-gorilla](https://aur.archlinux.org/packages/password-gorilla/) [gorilla](https://aur.archlinux.org/packages/gorilla/)

*   **Password Safe** — Simple and secure password manager.

	[http://passwordsafe.sourceforge.net/](http://passwordsafe.sourceforge.net/) || [passwordsafe](https://aur.archlinux.org/packages/passwordsafe/)

*   **pwsafe** — Unix commandline program that manages encrypted password databases.

	[http://nsd.dyndns.org/pwsafe/](http://nsd.dyndns.org/pwsafe/) || [pwsafe](https://www.archlinux.org/packages/?name=pwsafe)

*   **QPass** — Easy to use password manager with built-in password generator.

	[http://qpass.sourceforge.net](http://qpass.sourceforge.net) || [qpass](https://aur.archlinux.org/packages/qpass/)

*   **Revelation** — Password manager for the GNOME desktop.

	[http://revelation.olasagasti.info/](http://revelation.olasagasti.info/) || [revelation](https://aur.archlinux.org/packages/revelation/)

*   **Seahorse** — GNOME application for managing encryption keys and passwords in the GnomeKeyring.

	[https://wiki.gnome.org/Apps/Seahorse](https://wiki.gnome.org/Apps/Seahorse) || [seahorse](https://www.archlinux.org/packages/?name=seahorse)

*   **Universal Password Manager** — Allows you to store usernames, passwords, URLs and generic notes in an encrypted database protected by one master password.

	[http://upm.sourceforge.net/](http://upm.sourceforge.net/) || [upm](https://aur.archlinux.org/packages/upm/)

## 科学

**Note:** 查看[AUR 'science' category](https://aur.archlinux.org/packages.php?O=0&do_Search=Go&detail=1&C=15&SeB=nd&SB=v&SO=d&PP=50)，有可能获得较新的Applications/Science列表

### 学术文档

参见主条目 [List of applications/Documents#Scientific documents](/index.php/List_of_applications/Documents#Scientific_documents "List of applications/Documents").

### 数学

#### 计算器

参见 [Wikipedia:Comparison of software calculators](https://en.wikipedia.org/wiki/Comparison_of_software_calculators "wikipedia:Comparison of software calculators").

*   **[bc](https://en.wikipedia.org/wiki/bc_programming_language "wikipedia:bc programming language")** — 任意精度的计算语言。

	[http://www.gnu.org/software/bc/](http://www.gnu.org/software/bc/) || [bc](https://www.archlinux.org/packages/?name=bc)

*   **calc** — 任意精确度的文字模式计算器。

	[http://www.isthe.com/chongo/tech/comp/calc/](http://www.isthe.com/chongo/tech/comp/calc/) || [calc](https://www.archlinux.org/packages/?name=calc)

*   **Extcalc** — 基于Qt的科学计算器。

	[http://extcalc-linux.sourceforge.net/](http://extcalc-linux.sourceforge.net/) || [extcalc](https://aur.archlinux.org/packages/extcalc/)

*   **galculator** — 基于GTK+的科学计算器。

	[http://galculator.sourceforge.net/](http://galculator.sourceforge.net/) || [galculator](https://www.archlinux.org/packages/?name=galculator) [galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)

*   **[GCalctool](https://en.wikipedia.org/wiki/GCalctool "wikipedia:GCalctool")** — Gnome内建的科学计算器 (GTK2 version).

	[http://www.gnome.org](http://www.gnome.org) || [gcalctool-oldgui](https://aur.archlinux.org/packages/gcalctool-oldgui/)

*   **[GNOME Calculator](https://en.wikipedia.org/wiki/GCalctool "wikipedia:GCalctool")** — Gnome内建的科学计算器 (new GTK3 version)。

	[http://www.gnome.org](http://www.gnome.org) || [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)

*   **KAlgebra** — 包含于KDE EDU 的计算器及图表制作工具。

	[http://www.kde.org/applications/education/kalgebra/](http://www.kde.org/applications/education/kalgebra/) || [kdeedu-kalgebra](https://www.archlinux.org/packages/?name=kdeedu-kalgebra)

*   **[KCalc](https://en.wikipedia.org/wiki/KCalc "wikipedia:KCalc")** — KDE内建的科学计算器。

	[http://kde.org/applications/utilities/kcalc/](http://kde.org/applications/utilities/kcalc/) || [kdeutils-kcalc](https://www.archlinux.org/packages/?name=kdeutils-kcalc)

*   **Qalculate** — 具备容错输入，常数识别及单位运算的计算器和方程求解器。

	[http://qalculate.sourceforge.net/](http://qalculate.sourceforge.net/) || [libqalculate](https://www.archlinux.org/packages/?name=libqalculate)

*   **SpeedCrunch** — 速度快，高精度，功能强大的跨平台的计算器。

	[http://speedcrunch.org](http://speedcrunch.org) || [speedcrunch](https://www.archlinux.org/packages/?name=speedcrunch)

*   **[xcalc](https://en.wikipedia.org/wiki/xcalc "wikipedia:xcalc")** — 用于X的科学计算器，包含代数和逆波兰表示法(reverse polish notation)模式。

	[http://xorg.freedesktop.org/](http://xorg.freedesktop.org/) || [xorg-xcalc](https://www.archlinux.org/packages/?name=xorg-xcalc)

#### 计算机代数系统

参见 [Wikipedia:Comparison of computer algebra systems](https://en.wikipedia.org/wiki/Comparison_of_computer_algebra_systems "wikipedia:Comparison of computer algebra systems").

*   **[AXIOM](https://en.wikipedia.org/wiki/Axiom_(computer_algebra_system) "wikipedia:Axiom (computer algebra system)")** — FriCAS:衍生自强大的AXIOM-CAS

	[http://fricas.sourceforge.net](http://fricas.sourceforge.net) || [fricas](https://aur.archlinux.org/packages/fricas/)

*   **[Fermat](https://en.wikipedia.org/wiki/Fermat_(computer_algebra_system) "wikipedia:Fermat (computer algebra system)")** — 计算机代数系统，可处理任意精度整数和分数运算，多元多项式，符号运算，多项式环上的矩阵运算，图形及其它类型数值运算。

	[http://home.bway.net/lewis/](http://home.bway.net/lewis/) || [fermat](https://aur.archlinux.org/packages/fermat/)

*   **[GAP](https://en.wikipedia.org/wiki/GAP_(computer_algebra_system) "wikipedia:GAP (computer algebra system)")** — 计算机离散代数系统，特别擅于计算群论（computational group theory）。

	[http://www.gap-system.org](http://www.gap-system.org) || [gap-math](https://aur.archlinux.org/packages/gap-math/)

*   **[Maple](/index.php/Maple "Maple")** — 著名的商业CAS。常用於教学。

	[http://www.maplesoft.com/products/maple/](http://www.maplesoft.com/products/maple/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=maple)</small>

*   **[Mathics](/index.php/Mathics "Mathics")** — 一款自由的CAS软件，用于符号运算，使用[Python](/index.php/Python "Python")作为其主要编程语言; 致力于Mathematica语法和函数兼容; 该程序依赖Sympy完成主要的计算，且可通过Sage使用可选的高级功能。

	[http://www.mathics.org/](http://www.mathics.org/) || [mathics](https://aur.archlinux.org/packages/mathics/)

*   **[Mathomatic](https://en.wikipedia.org/wiki/Mathomatic "wikipedia:Mathomatic")** — 用C语言编写的通用计算机代数系统。

	[http://www.mathomatic.org/](http://www.mathomatic.org/) || [mathomatic](https://www.archlinux.org/packages/?name=mathomatic)

*   **[Maxima](https://en.wikipedia.org/wiki/Maxima_(software) "wikipedia:Maxima (software)")** — 类似[Maple](https://en.wikipedia.org/wiki/Maple_(software) "wikipedia:Maple (software)")/[Mathematica](https://en.wikipedia.org/wiki/Wolfram_Mathematica "wikipedia:Wolfram Mathematica")的程序，拥有基于wxWidgets的图形前端。

	[http://maxima.sourceforge.net/](http://maxima.sourceforge.net/) || [maxima](https://www.archlinux.org/packages/?name=maxima) [wxmaxima](https://www.archlinux.org/packages/?name=wxmaxima)

*   **[PARI/GP](https://en.wikipedia.org/wiki/PARI/GP "wikipedia:PARI/GP")** — 为快速计算数论设计的计算机代数系统。

	[http://pari.math.u-bordeaux.fr/](http://pari.math.u-bordeaux.fr/) || [pari](https://www.archlinux.org/packages/?name=pari)

*   **[Xcas](https://en.wikipedia.org/wiki/Xcas "wikipedia:Xcas")** — Giac的用戶界面。（Giac是一个自由，基础的计算机代数系统）

	[http://www-fourier.ujf-grenoble.fr/~parisse/giac.html](http://www-fourier.ujf-grenoble.fr/~parisse/giac.html) || [xcas](https://www.archlinux.org/packages/?name=xcas)

*   **[Sympy](https://en.wikipedia.org/wiki/SymPy "wikipedia:SymPy")** — 支持符号计算的Python函式库(以x,y等名称作运算工具，这是mathemetica有而scipy欠缺的功能)，可求出不定积分(indefinite integral)和导数。显示结果的方式有：ascii art、python expression、Latex，或透过matplotlib绘图。

	[http://www.sympy.org/en/index.html](http://www.sympy.org/en/index.html) || [python-sympy](https://www.archlinux.org/packages/?name=python-sympy)

#### 科学与工程计算

参见 [Wikipedia:Comparison of numerical analysis software](https://en.wikipedia.org/wiki/Comparison_of_numerical_analysis_software "wikipedia:Comparison of numerical analysis software").

*   **EngLab** — 使用类C语法的交叉编译数学平台。

	[http://englab.bugfest.net](http://englab.bugfest.net) || [englab](https://aur.archlinux.org/packages/englab/)

*   **[Euler](https://en.wikipedia.org/wiki/Euler_(software) "wikipedia:Euler (software)")** — 为高等数学计算，如微积分，优化和统计，以及通过Maxima实现的符号运算设计的数值计算程序。

	[http://euler.sourceforge.net](http://euler.sourceforge.net) || [euler](https://aur.archlinux.org/packages/euler/)

*   **[FreeMat](https://en.wikipedia.org/wiki/FreeMat "wikipedia:FreeMat")** — 类[Matlab](/index.php/Matlab "Matlab")程序，支持相当数量的Matlab函数，同时拥有编程友好(codeless)的C, C++, Fortran语言接口，以及对分布式并行算法开发和3D可视化功能的支持。

	[http://freemat.sourceforge.net/](http://freemat.sourceforge.net/) || [freemat](https://www.archlinux.org/packages/?name=freemat)

*   **[GNU Radio](/index.php/GNU_Radio "GNU Radio")** — 软件开发套件，提供信号处理模块以协助开发程序。

	[http://www.gnuradio.org/redmine/projects/gnuradio/wiki](http://www.gnuradio.org/redmine/projects/gnuradio/wiki) || [gnuradio](https://www.archlinux.org/packages/?name=gnuradio)

*   **[Octave](/index.php/Octave "Octave")** — 类[Matlab](/index.php/Matlab "Matlab")编程语言和接口，用于数值计算。

	[http://www.gnu.org/software/octave/](http://www.gnu.org/software/octave/) || [octave](https://www.archlinux.org/packages/?name=octave)

*   **[PyLab](https://en.wikipedia.org/wiki/matplotlib "wikipedia:matplotlib")** — Python模块集合（pyplot, numpy等），用于科学计算

	[http://www.scipy.org/PyLab](http://www.scipy.org/PyLab) || [python2-matplotlib](https://www.archlinux.org/packages/?name=python2-matplotlib)

*   **[Sage](/index.php/Sage "Sage")** — 数学软件系统，使用大量已有开源软件包整合出一个通用的Python接口，可作为Magma, Maple, Mathematica 和 Matlab的替代品。

	[http://www.sagemath.org](http://www.sagemath.org) || [sage-mathematics](https://www.archlinux.org/packages/?name=sage-mathematics)

*   **[Scilab](https://en.wikipedia.org/wiki/Scilab "wikipedia:Scilab")** — Matlab替代品，用于数值计算，语法和Matlab不相同，但是可以很容易从Matlab语法转换。

	[http://www.scilab.org/](http://www.scilab.org/) || [scilab](https://aur.archlinux.org/packages/scilab/)

#### 统计

参见 [Wikipedia:Comparison of statistical packages](https://en.wikipedia.org/wiki/Comparison_of_statistical_packages "wikipedia:Comparison of statistical packages")。

*   **[JAGS](https://en.wikipedia.org/wiki/Just_another_Gibbs_sampler "wikipedia:Just another Gibbs sampler") (Just another Gibbs sampler)** — 跨平台程序，用于基于马尔可夫链蒙特卡尔理论(Markov Chain Monte Carlo) (MCMC) 模拟的贝塞叶分层模型(Bayesian hierachical models) 分析。

	[http://mcmc-jags.sourceforge.net/](http://mcmc-jags.sourceforge.net/) || [jags](https://aur.archlinux.org/packages/jags/)

*   **[Python Data Analysis Library (pandas)](https://en.wikipedia.org/wiki/Pandas_(software) "wikipedia:Pandas (software)")** — 基于Python语言的高性能，易用的数据结构和数据分析工具。

	[http://pandas.pydata.org/](http://pandas.pydata.org/) || [python2-pandas-git](https://aur.archlinux.org/packages/python2-pandas-git/)

*   **[PSPP](https://en.wikipedia.org/wiki/PSPP "wikipedia:PSPP")** — 自由的SPSS实现。

	[http://www.gnu.org/software/pspp/](http://www.gnu.org/software/pspp/) || [pspp](https://aur.archlinux.org/packages/pspp/)

*   **[R](/index.php/R "R")** — 用于统计计算及图形处理的软件环境。

	[http://cran.r-project.org/](http://cran.r-project.org/) || [r](https://www.archlinux.org/packages/?name=r)

*   **[RKWard](https://en.wikipedia.org/wiki/RKWard "wikipedia:RKWard")** — 统计语言R的前端。

	[http://rkward.sourceforge.net/](http://rkward.sourceforge.net/) || [rkward](https://aur.archlinux.org/packages/rkward/)

*   **[RStudio](https://en.wikipedia.org/wiki/RStudio "wikipedia:RStudio")** — 为R构建的基于Qt的强大的产品级IDE 。

	[http://www.rstudio.com/](http://www.rstudio.com/) || [rstudio-desktop-bin](https://aur.archlinux.org/packages/rstudio-desktop-bin/)

#### 数据评估

参见 [Wikipedia:List of information graphics software](https://en.wikipedia.org/wiki/List_of_information_graphics_software "wikipedia:List of information graphics software")。

*   **Extrema** — 数据图像化及分析工具。

	[http://sourceforge.net/projects/extrema](http://sourceforge.net/projects/extrema) || [extrema](https://aur.archlinux.org/packages/extrema/)

*   **[Fityk](https://en.wikipedia.org/wiki/Fityk "wikipedia:Fityk")** — 曲线拟合和数据分析工具，主要用于以钟形函数(bell-shaped function)拟合到实验数据。

	[http://fityk.nieto.pl/](http://fityk.nieto.pl/) || [fityk](https://aur.archlinux.org/packages/fityk/)

*   **[Gnuplot](https://en.wikipedia.org/wiki/gnuplot "wikipedia:gnuplot")** — 命令行驱动的可以绘制2D和3D函数，数据和数据拟合(data fits)的软件。

	[http://www.gnuplot.info/](http://www.gnuplot.info/) || [gnuplot](https://www.archlinux.org/packages/?name=gnuplot)

*   **[Grace](https://en.wikipedia.org/wiki/Grace_(plotting_tool) "wikipedia:Grace (plotting tool)")** — WYSIWYG(所见即所得)2D图表绘制工具。

	[http://plasma-gate.weizmann.ac.il/Grace/](http://plasma-gate.weizmann.ac.il/Grace/) || [grace](https://www.archlinux.org/packages/?name=grace) [qtgrace](https://aur.archlinux.org/packages/qtgrace/) [gracegtk](https://aur.archlinux.org/packages/gracegtk/)

*   **[LabPlot](https://en.wikipedia.org/wiki/LabPlot "wikipedia:LabPlot")** — 类似SciDAVis的自由软件，可以用于数据分析和数据可视化应用。

	[http://labplot.sourceforge.net/](http://labplot.sourceforge.net/) || [labplot2](https://aur.archlinux.org/packages/labplot2/)

*   **[QtiPlot](https://en.wikipedia.org/wiki/QtiPlot "wikipedia:QtiPlot")** — 类似私有软件[Origin](https://en.wikipedia.org/wiki/Origin_(software) "wikipedia:Origin (software)")和[SigmaPlot](https://en.wikipedia.org/wiki/SigmaPlot "wikipedia:SigmaPlot")的跨平台软件，可用于互动式图表绘制和数据分析。

	[http://www.qtiplot.com/](http://www.qtiplot.com/) || [qtiplot](https://www.archlinux.org/packages/?name=qtiplot)

*   **[ROOT](https://en.wikipedia.org/wiki/ROOT "wikipedia:ROOT")** — CERN研发的数据分析软件和函数库(原用于微观物理学)。

	[http://root.cern.ch/drupal/](http://root.cern.ch/drupal/) || [root](https://aur.archlinux.org/packages/root/)

*   **[SciDAVis](https://en.wikipedia.org/wiki/SciDAVis "wikipedia:SciDAVis")** — QtiPlot的派生软件，以提供更好的文档支持和友好用户介面为目标。

	[http://scidavis.sourceforge.net/](http://scidavis.sourceforge.net/) || [scidavis](https://aur.archlinux.org/packages/scidavis/)

参见 [List of applications#Spreadsheets](/index.php/List_of_applications#Spreadsheets "List of applications")

### 化学与生物学

#### 计算生物学和生物信息学

参见 [Wikipedia:List of open source bioinformatics software](https://en.wikipedia.org/wiki/List_of_open_source_bioinformatics_software "wikipedia:List of open source bioinformatics software").

*   **[BALL](https://en.wikipedia.org/wiki/BALL "wikipedia:BALL") (Biochemical Algorithms Library)** — 基于C++构建的应用框架，提供一种可扩展的数据结构和类集合，用于分子力学，先进的溶剂化方法(advanced solvation methods), 蛋白质结构的对比和分析，文件的导入/导出，以及可视化。

	[http://www.ball-project.org/](http://www.ball-project.org/) || [ball](https://aur.archlinux.org/packages/ball/)

*   **[BioJava](https://en.wikipedia.org/wiki/BioJava "wikipedia:BioJava")** — Java工具集， 用于计算生物学和生物信息学。

	[http://biojava.org/wiki/Main_Page](http://biojava.org/wiki/Main_Page) || [biojava](https://aur.archlinux.org/packages/biojava/)

*   **[Biopython](https://en.wikipedia.org/wiki/Biopython "wikipedia:Biopython")** — Python包，包含用于计算生物学和生物信息学的工具。

	[http://biopython.org/wiki/Biopython](http://biopython.org/wiki/Biopython) || [python-biopython](https://www.archlinux.org/packages/?name=python-biopython) [python2-biopython](https://www.archlinux.org/packages/?name=python2-biopython)

*   **[EMBOSS](https://en.wikipedia.org/wiki/EMBOSS "wikipedia:EMBOSS") (European Molecular Biology Open Software Suite)** — 用于分析的开源软件包，由分子生物学和生物信息学用户社区需求驱动。

	[http://emboss.sourceforge.net/](http://emboss.sourceforge.net/) || [emboss](https://aur.archlinux.org/packages/emboss/)

*   **[MEGA](https://en.wikipedia.org/wiki/MEGA,_Molecular_Evolutionary_Genetics_Analysis "wikipedia:MEGA, Molecular Evolutionary Genetics Analysis") (Molecular Evolutionary Genetics Analysis)** — 集成化工具，用于指导自动和手动序列比对，推导进化树，最小化基于网络的数据库，分子演化速率估计，推导祖序列(ancestral sequence), 以及对进化假说的验证。

	[http://www.megasoftware.net/](http://www.megasoftware.net/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[MUMmer](https://en.wikipedia.org/wiki/MUMmer "wikipedia:MUMmer")** — 生物信息学软件系统，用于基于后缀树(suffix trees)的序列比对。

	[http://mummer.sourceforge.net/](http://mummer.sourceforge.net/) || [mummer](https://aur.archlinux.org/packages/mummer/)

*   **[UGENE](https://en.wikipedia.org/wiki/UGENE "wikipedia:UGENE")** — 集成了大量的知名生物学工具和算法并同时提供图形和字符界面的应用程序。

	[http://ugene.unipro.ru/](http://ugene.unipro.ru/) || [ugene](https://aur.archlinux.org/packages/ugene/)

#### 分子学

##### 查看器

参见 [Wikipedia:List of molecular graphics systems](https://en.wikipedia.org/wiki/List_of_molecular_graphics_systems "wikipedia:List of molecular graphics systems").

*   **[Avogadro](https://en.wikipedia.org/wiki/Avogadro_(software) "wikipedia:Avogadro (software)")** — 3D分子结构编辑器，查看器和仿真器(同时支持从[Protein Data Bank](https://en.wikipedia.org/wiki/Protein_Data_Bank "wikipedia:Protein Data Bank")下载数据)。

	[http://avogadro.openmolecules.net/wiki/Main_Page](http://avogadro.openmolecules.net/wiki/Main_Page) || [avogadro](https://aur.archlinux.org/packages/avogadro/)

*   **BALLView** — 可单独使用的分子建模和可视化应用，是[BALL](https://en.wikipedia.org/wiki/BALL "wikipedia:BALL")框架的一部分。

	[http://www.ballview.org/](http://www.ballview.org/) || [ball](https://aur.archlinux.org/packages/ball/)

*   **[Ghemical](https://en.wikipedia.org/wiki/Ghemical "wikipedia:Ghemical")** — 计算化学软件包，用于分子结构的编辑，查看和仿真。

	[http://bioinformatics.org/ghemical/ghemical/index.html](http://bioinformatics.org/ghemical/ghemical/index.html) || [ghemical](https://aur.archlinux.org/packages/ghemical/)

*   **[PyMOL](https://en.wikipedia.org/wiki/PyMOL "wikipedia:PyMOL")** — 开源分子可视化系统，可以生成高质量的低分子和生物高分子(例如蛋白质)的图像。

	[http://pymol.org](http://pymol.org) || [pymol](https://www.archlinux.org/packages/?name=pymol)

*   **[RasMol](https://en.wikipedia.org/wiki/RasMol "wikipedia:RasMol")** — 用于描述和探索生物高分子结构的计算机分子图形可视化程序。

	[http://www.rasmol.org/](http://www.rasmol.org/) || [rasmol](https://aur.archlinux.org/packages/rasmol/)

##### Drawing

*   **[BKChem](https://en.wikipedia.org/wiki/BKchem "wikipedia:BKchem")** — Practical and goodlooking skeletal formula molecule drawing program.

	[http://bkchem.zirael.org/](http://bkchem.zirael.org/) || [bkchem](https://aur.archlinux.org/packages/bkchem/)

*   **[Chemtool](https://en.wikipedia.org/wiki/Chemtool "wikipedia:Chemtool")** — GTK+-based program for drawing chemical structural formulas.

	[http://ruby.chemie.uni-freiburg.de/~martin/chemtool/chemtool.html](http://ruby.chemie.uni-freiburg.de/~martin/chemtool/chemtool.html) || [chemtool](https://www.archlinux.org/packages/?name=chemtool)

*   **EasyChem** — Simple skeletal formula molecule drawing program with a focus on producing press-quality figures.

	[http://easychem.sourceforge.net/](http://easychem.sourceforge.net/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=easychem)</small>

*   **[Gabedit](https://en.wikipedia.org/wiki/Gabedit "wikipedia:Gabedit")** — Graphical user interface to computational chemistry packages like [GAMESS](https://en.wikipedia.org/wiki/GAMESS_(US) "wikipedia:GAMESS (US)"), [Gaussian](https://en.wikipedia.org/wiki/Gaussian_(software) "wikipedia:Gaussian (software)"), [MOLCAS](https://en.wikipedia.org/wiki/MOLCAS "wikipedia:MOLCAS"), [MOLPRO](https://en.wikipedia.org/wiki/MOLPRO "wikipedia:MOLPRO"), [MPQC](https://en.wikipedia.org/wiki/MPQC "wikipedia:MPQC"), [OpenMopac](https://en.wikipedia.org/wiki/MOPAC "wikipedia:MOPAC"), [Firefly](https://en.wikipedia.org/wiki/PC_GAMESS "wikipedia:PC GAMESS") (previously PC GAMESS) and [Q-Chem](https://en.wikipedia.org/wiki/Q-Chem "wikipedia:Q-Chem").

	[http://gabedit.sourceforge.net/](http://gabedit.sourceforge.net/) || [gabedit](https://aur.archlinux.org/packages/gabedit/)

*   **[XDrawChem](https://en.wikipedia.org/wiki/XDrawChem "wikipedia:XDrawChem")** — Extensive skeletal formula molecule drawing program (includes spectroscopy prediction).

	[http://xdrawchem.sourceforge.net/](http://xdrawchem.sourceforge.net/) || [xdrawchem](https://aur.archlinux.org/packages/xdrawchem/)

##### Modeling

*   **[GROMACS](https://en.wikipedia.org/wiki/GROMACS "wikipedia:GROMACS") (GROningen MAchine for Chemical Simulations)** — Versatile package to perform molecular dynamics, i.e. simulate the Newtonian equations of motion for systems with hundreds to millions of particles.

	[http://www.gromacs.org](http://www.gromacs.org) || [gromacs](https://aur.archlinux.org/packages/gromacs/)

*   **[Quantum ESPRESSO](https://en.wikipedia.org/wiki/Quantum_ESPRESSO "wikipedia:Quantum ESPRESSO")** — Integrated suite of applications for electronic-structure calculations and materials modeling at nanoscale. It is based on density-functional theory, plane waves, and pseudopotentials (both norm-conserving and ultrasoft).

	[http://www.quantum-espresso.org/](http://www.quantum-espresso.org/) || [quantum-espresso](https://aur.archlinux.org/packages/quantum-espresso/)

#### Periodic table

*   **gElemental** — Periodic table of the elements with additional information.

	[http://freshmeat.net/projects/gelemental](http://freshmeat.net/projects/gelemental) || [gelemental](https://aur.archlinux.org/packages/gelemental/)

*   **[Kalzium](https://en.wikipedia.org/wiki/Kalzium "wikipedia:Kalzium")** — Periodic table of the elements with molecule editor and equation solver from the [KDE](/index.php/KDE "KDE") desktop.

	[http://edu.kde.org/kalzium/](http://edu.kde.org/kalzium/) || [kdeedu-kalzium](https://www.archlinux.org/packages/?name=kdeedu-kalzium)

#### Biochemistry

*   **[Bioclipse](https://en.wikipedia.org/wiki/Bioclipse "wikipedia:Bioclipse")** — Java-based visual platform for biochemistry that uses the Eclipse Rich Client Platform (RCP).

	[http://www.bioclipse.net/](http://www.bioclipse.net/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=bioclipse)</small>

#### Image manipulation

*   **[ImageJ](https://en.wikipedia.org/wiki/ImageJ "wikipedia:ImageJ")** — Java-based image processing and analysing program that provides extensibility via plugins and macros. It is widely used in microscopy (e.g. for cell counting).

	[http://rsb.info.nih.gov/ij](http://rsb.info.nih.gov/ij) || [imagej](https://aur.archlinux.org/packages/imagej/)

*   **[Fiji](https://en.wikipedia.org/wiki/FIJI_(software) "wikipedia:FIJI (software)")** — ImageJ distribution (and soon ImageJ2) with a lot of plugins organized into a coherent menu structure.

	[http://fiji.sc](http://fiji.sc) || [fiji-binary](https://aur.archlinux.org/packages/fiji-binary/)

### 天文学

*   **Stellarium** — 開源的虛擬天文館軟體，可以用3D方式模擬真實的天空.

	[http://www.stellarium.org/](http://www.stellarium.org/) || [stellarium](https://www.archlinux.org/packages/?name=stellarium)

*   **KStars** — KKDE天文館軟體.

	[http://edu.kde.org/kstars/](http://edu.kde.org/kstars/) || [kdeedu-kstars](https://www.archlinux.org/packages/?name=kdeedu-kstars)

*   **Celestia** — 以OpenGL開發的3D天文軟件。讓使用者以第一身穿梭於三維宇宙空間。

	[http://www.shatters.net/celestia/](http://www.shatters.net/celestia/) || [celestia](https://www.archlinux.org/packages/?name=celestia)

### 物理学

#### 电子学

See also [Wikipedia:Comparison of EDA software](https://en.wikipedia.org/wiki/Comparison_of_EDA_software "wikipedia:Comparison of EDA software").

#### 物理系统模拟器

*   **[Code_Aster](https://en.wikipedia.org/wiki/Code_Aster "wikipedia:Code Aster")** — 用於土木及结构工程，作有限元分析和模拟的结构力学。

	[http://www.code-aster.org/V2/spip.php?rubrique2](http://www.code-aster.org/V2/spip.php?rubrique2) || [aster](https://aur.archlinux.org/packages/aster/)

*   **[Step](https://en.wikipedia.org/wiki/Step_(software) "wikipedia:Step (software)")** — 包含在KDE的二维物理模拟引擎。

	[http://edu.kde.org/step/](http://edu.kde.org/step/) || [kdeedu-step](https://www.archlinux.org/packages/?name=kdeedu-step)

*   **[SWMM](https://en.wikipedia.org/wiki/SWMM "wikipedia:SWMM")** — 雨水管理模型。

	[http://www.epa.gov/](http://www.epa.gov/) || [swmm5-git](https://aur.archlinux.org/packages/swmm5-git/)

#### 单位转换

*   **ConvertAll** — Unit conversion application that allows one to combine units in any way (e.g. inches per decade), even if it does not make sense.

	[http://convertall.bellz.org/](http://convertall.bellz.org/) || [convertall](https://aur.archlinux.org/packages/convertall/)

*   **Gonvert** — Conversion utility that allows conversion between many units like CGS, Ancient, Imperial with many categories like length, mass, numbers, etc.

	[http://www.unihedron.com/projects/gonvert/](http://www.unihedron.com/projects/gonvert/) || [gonvert](https://aur.archlinux.org/packages/gonvert/)

*   **[Units](https://en.wikipedia.org/wiki/GNU_Units "wikipedia:GNU Units")** — Command-line unit converter and calculator that can handle multiplicative scale changes, nonlinear conversions such as Fahrenheit to Celsius or wire gauge and others.

	[http://www.gnu.org/s/units/](http://www.gnu.org/s/units/) || [units](https://www.archlinux.org/packages/?name=units)

**翻译状态：** 本文是英文页面 [List_of_applications](/index.php/List_of_applications "List of applications") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-02-20，点击[这里](https://wiki.archlinux.org/index.php?title=List_of_applications&diff=0&oldid=417274)可以查看翻译后英文页面的改动。

## 其它

### 工作环境

初始安装的Arch系统使用Bash作为Shell但不包含任何图形环境,因此用户能够自行选择.大多数使用者使用X11窗口管理器或桌面环境,但还是有人喜欢使用命令行工作.

#### 开机动画

参见 [Wikipedia:Bootsplash](https://en.wikipedia.org/wiki/Bootsplash "wikipedia:Bootsplash").

*   **[Fbsplash](/index.php/Fbsplash "Fbsplash")** — Gentoo开机动画程序

	[http://wiki.gentoo.org/wiki/Fbsplash](http://wiki.gentoo.org/wiki/Fbsplash) || [fbsplash](https://aur.archlinux.org/packages/fbsplash/)

*   **[Plymouth](/index.php/Plymouth "Plymouth")** — Fedora新开机动画程序,取代了Red Hat 的开机动画

	[http://www.freedesktop.org/wiki/Software/Plymouth/](http://www.freedesktop.org/wiki/Software/Plymouth/) || [plymouth](https://aur.archlinux.org/packages/plymouth/)

*   **[Splashy](/index.php/Splashy "Splashy")** — 另一个取代Bootsplash的开机动画程序

	[https://alioth.debian.org/projects/splashy/](https://alioth.debian.org/projects/splashy/) || [splashy-full](https://aur.archlinux.org/packages/splashy-full/)

#### 命令行

详见[Command-line shell](/index.php/Command-line_shell "Command-line shell").

参见[Wikipedia:Comparison of command shells](https://en.wikipedia.org/wiki/Comparison_of_command_shells "wikipedia:Comparison of command shells").

#### Terminal multiplexers

*   **abduco** — Tool for session attach and detach support which allows a process to run independently from its controlling terminal.

	[http://www.brain-dump.org/projects/abduco/](http://www.brain-dump.org/projects/abduco/) || [abduco](https://www.archlinux.org/packages/?name=abduco)

*   **dtach** — Program that emulates the detach feature of [screen](/index.php/Screen "Screen").

	[http://dtach.sourceforge.net/](http://dtach.sourceforge.net/) || [dtach](https://www.archlinux.org/packages/?name=dtach)

*   **[GNU Screen](/index.php/GNU_Screen "GNU Screen")** — Full-screen window manager that multiplexes a physical terminal.

	[https://gnu.org/s/screen/](https://gnu.org/s/screen/) || [screen](https://www.archlinux.org/packages/?name=screen)

*   **[tmux](/index.php/Tmux "Tmux")** — BSD licensed terminal multiplexer.

	[http://tmux.github.io/](http://tmux.github.io/) || [tmux](https://www.archlinux.org/packages/?name=tmux)

*   **[byobu](https://en.wikipedia.org/wiki/Byobu_(software) "wikipedia:Byobu (software)")** — An GPLv3 licensed addon for tmux or screen. It requires a terminal multiplexer installed.

	[http://byobu.co/](http://byobu.co/) || [byobu](https://aur.archlinux.org/packages/byobu/)

#### Desktop environments

See the main article: [Desktop environment#List of desktop environments](/index.php/Desktop_environment#List_of_desktop_environments "Desktop environment").

See also [Wikipedia:Comparison of X Window System desktop environments](https://en.wikipedia.org/wiki/Comparison_of_X_Window_System_desktop_environments "wikipedia:Comparison of X Window System desktop environments").

#### Window managers

##### Console

See also [#Terminal multiplexers](#Terminal_multiplexers), which offer some of the functions of window managers for the console.

*   **dvtm** — [dwm](/index.php/Dwm "Dwm")-style window manager in the console.

	[http://brain-dump.org/projects/dvtm/](http://brain-dump.org/projects/dvtm/) || [dvtm](https://www.archlinux.org/packages/?name=dvtm)

*   **twin** — Text-mode window manager.

	[http://sourceforge.net/projects/twin/](http://sourceforge.net/projects/twin/) || [twin](https://www.archlinux.org/packages/?name=twin)

##### Graphical

See the main article: [Window manager#List of window managers](/index.php/Window_manager#List_of_window_managers "Window manager").

See also [Wikipedia:Comparison of X window managers](https://en.wikipedia.org/wiki/Comparison_of_X_window_managers "wikipedia:Comparison of X window managers").

#### Window tilers

*   **PyTyle3** — An automatic tiler that is compatible with Openbox Multihead with faster action and lower memory footprint.

	[https://github.com/BurntSushi/pytyle3](https://github.com/BurntSushi/pytyle3) || [pytyle3-git](https://aur.archlinux.org/packages/pytyle3-git/)

*   **PyWO** — Allows you to easily organize windows on the desktop using keyboard shortcuts.

	[https://code.google.com/p/pywo/](https://code.google.com/p/pywo/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **QuickTile** — Lightweight standalone alternative to Compiz Grid plugin.

	[http://ssokolow.com/quicktile/](http://ssokolow.com/quicktile/) || [quicktile-git](https://aur.archlinux.org/packages/quicktile-git/)

*   **stiler** — A simple python script to convert any wm to tiling wm.

	[https://bbs.archlinux.org/viewtopic.php?id=64100](https://bbs.archlinux.org/viewtopic.php?id=64100) || [stiler-grid-git](https://aur.archlinux.org/packages/stiler-grid-git/) [stiler](https://aur.archlinux.org/packages/stiler/)

*   **[Tile-windows](/index.php/Tile-windows "Tile-windows")** — Tool for tiling windows horizontally or vertically.

	[http://www.sourcefiles.org/Utilities/Miscellaneous/tile_0.7.4.tar.gz.shtml](http://www.sourcefiles.org/Utilities/Miscellaneous/tile_0.7.4.tar.gz.shtml) || [tile-windows](https://aur.archlinux.org/packages/tile-windows/)

*   **whaw** — Window manager independent window layout tool.

	[http://repetae.net/computer/whaw/](http://repetae.net/computer/whaw/) || [whaw](https://aur.archlinux.org/packages/whaw/)

*   **wumwum** — The Window Manager manager. It can turn emwh compliant window managers into a tiling window manager while retaining all initial functionalities.

	[http://wumwum.sourceforge.net/](http://wumwum.sourceforge.net/) || [wumwum](https://aur.archlinux.org/packages/wumwum/)

#### Virtual desktop pagers

See also [Wikipedia:Pager (GUI)](https://en.wikipedia.org/wiki/Pager_(GUI) "wikipedia:Pager (GUI)").

*   **bbpager** — Dockable pager for [blackbox](/index.php/Blackbox "Blackbox") and other window managers.

	[http://bbtools.sourceforge.net/download.php?file=6](http://bbtools.sourceforge.net/download.php?file=6) || [bbpager](https://www.archlinux.org/packages/?name=bbpager)

*   **fbpager** — Virtual desktop pager for fluxbox.

	[http://www.fluxbox.org/fbpager](http://www.fluxbox.org/fbpager) || [fbpager-git](https://aur.archlinux.org/packages/fbpager-git/)

*   **IPager** — A configurable pager with transparency, originally developed for Fluxbox.

	[http://useperl.ru/ipager/index.en.html](http://useperl.ru/ipager/index.en.html) || [ipager](https://aur.archlinux.org/packages/ipager/)

*   **Neap** — An non-intrusive and light pager that runs in the notification area of your panel.

	[http://code.google.com/p/neap/](http://code.google.com/p/neap/) || [neap](https://aur.archlinux.org/packages/neap/)

*   **Netwmpager** — A NetWM/EWMH compatible pager.

	[http://sourceforge.net/projects/sf-xpaint/files/netwmpager/](http://sourceforge.net/projects/sf-xpaint/files/netwmpager/) || [netwmpager](https://aur.archlinux.org/packages/netwmpager/)

*   **obpager** — Pager for [Openbox](/index.php/Openbox "Openbox") writen in C++.

	[http://obpager.sourceforge.net/](http://obpager.sourceforge.net/) || [obpager](https://aur.archlinux.org/packages/obpager/)

*   **Pager** — A highly configurable pager compatible with Openbox Multihead.

	[https://github.com/BurntSushi/pager-multihead](https://github.com/BurntSushi/pager-multihead) || [pager-multihead-git](https://aur.archlinux.org/packages/pager-multihead-git/)

#### Support applications

##### Login managers

See the main article: [Display manager#List of display managers](/index.php/Display_manager#List_of_display_managers "Display manager").

##### Composite managers

See the main article: [Xorg#List of composite managers](/index.php/Xorg#List_of_composite_managers "Xorg").

##### Taskbars / panels / docks

*   **[Avant Window Navigator](/index.php/Avant_Window_Navigator "Avant Window Navigator")** — Lightweight dock which sits at the bottom of the screen.

	[http://launchpad.net/awn](http://launchpad.net/awn) || [avant-window-navigator](https://aur.archlinux.org/packages/avant-window-navigator/)

*   **[Bmpanel](/index.php/Bmpanel "Bmpanel")** — Lightweight, NETWM compliant panel.

	[http://code.google.com/p/bmpanel2/](http://code.google.com/p/bmpanel2/) || [bmpanel](https://aur.archlinux.org/packages/bmpanel/)

*   **[Cairo-Dock](/index.php/Cairo-Dock "Cairo-Dock")** — Highly customizable dock and launcher application.

	[http://www.glx-dock.org/](http://www.glx-dock.org/) || [cairo-dock](https://www.archlinux.org/packages/?name=cairo-dock)

*   **Daisy** — KDE Plasma widget which acts as a dock.

	[http://cdlszm.org/](http://cdlszm.org/) || [kdeplasma-applets-daisy](https://aur.archlinux.org/packages/kdeplasma-applets-daisy/)

*   **Docker** — Docking application which acts as a system tray.

	[http://icculus.org/openbox/2/docker/](http://icculus.org/openbox/2/docker/) || [docker-tray](https://aur.archlinux.org/packages/docker-tray/)

*   **[Docky](https://en.wikipedia.org/wiki/Docky "wikipedia:Docky")** — Full fledged dock application that makes opening common applications and managing windows easier and quicker.

	[http://wiki.go-docky.com/](http://wiki.go-docky.com/) || [docky](https://www.archlinux.org/packages/?name=docky)

*   **[fbpanel](/index.php/Fbpanel "Fbpanel")** — Lightweight, NETWM compliant desktop panel.

	[http://fbpanel.sourceforge.net/](http://fbpanel.sourceforge.net/) || [fbpanel](https://www.archlinux.org/packages/?name=fbpanel)

*   **[GNOME Panel](https://en.wikipedia.org/wiki/GNOME_Panel "wikipedia:GNOME Panel")** — Panel included in the [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") desktop.

	[https://wiki.gnome.org/Projects/GnomePanel](https://wiki.gnome.org/Projects/GnomePanel) || [gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel)

*   **KoolDock** — KDE3 docker with great effects that tries to resemble the OS X dock.

	[http://sourceforge.net/projects/kooldock](http://sourceforge.net/projects/kooldock) || [kooldock-svn](https://aur.archlinux.org/packages/kooldock-svn/)

*   **LXPanel** — Lightweight X11 desktop panel and part of the LXDE desktop.

	[http://lxde.org/lxpanel](http://lxde.org/lxpanel) || [lxpanel](https://www.archlinux.org/packages/?name=lxpanel)

*   **MATE Panel** — Panel included in the [MATE](/index.php/MATE "MATE") desktop.

	[https://github.com/mate-desktop/mate-panel/](https://github.com/mate-desktop/mate-panel/) || [mate-panel](https://www.archlinux.org/packages/?name=mate-panel)

*   **PerlPanel** — The ideal accompaniment to a light-weight Window Manager such as OpenBox, or a desktop-drawing program like iDesk.

	[http://savannah.nongnu.org/projects/perlpanel](http://savannah.nongnu.org/projects/perlpanel) || [perlpanel](https://aur.archlinux.org/packages/perlpanel/)

*   **plank** — Elegant, simple, clean dock from [pantheon](/index.php/Pantheon "Pantheon") desktop environment.

	[https://launchpad.net/plank](https://launchpad.net/plank) || [plank](https://www.archlinux.org/packages/?name=plank)

*   **[PyPanel](/index.php/PyPanel "PyPanel")** — Lightweight panel/taskbar written in Python and C.

	[http://pypanel.sourceforge.net/](http://pypanel.sourceforge.net/) || [pypanel](https://www.archlinux.org/packages/?name=pypanel)

*   **qtpanel** — Project to create useful and beautiful panel in Qt.

	[https://gitorious.org/qtpanel/qtpanel](https://gitorious.org/qtpanel/qtpanel) || [qtpanel-git](https://aur.archlinux.org/packages/qtpanel-git/)

*   **[Stalonetray](/index.php/Stalonetray "Stalonetray")** — Stand-alone system tray.

	[http://stalonetray.sourceforge.net/](http://stalonetray.sourceforge.net/) || [stalonetray](https://www.archlinux.org/packages/?name=stalonetray)

*   **[Tint2](/index.php/Tint2 "Tint2")** — Simple panel/taskbar developed specifically for Openbox.

	[http://code.google.com/p/tint2/](http://code.google.com/p/tint2/) || [tint2](https://www.archlinux.org/packages/?name=tint2)

*   **Trayer** — Lightweight GTK+-based systray.

	[https://gna.org/projects/fvwm-crystal/](https://gna.org/projects/fvwm-crystal/) || [trayer](https://www.archlinux.org/packages/?name=trayer)

*   **wbar** — Quick launch bar developed with speed in mind.

	[http://freecode.com/projects/wbar/](http://freecode.com/projects/wbar/) || [wbar](https://www.archlinux.org/packages/?name=wbar)

*   **Xfce Panel** — Panel included in the [Xfce](/index.php/Xfce "Xfce") desktop.

	[http://docs.xfce.org/xfce/xfce4-panel/start](http://docs.xfce.org/xfce/xfce4-panel/start) || [xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel)

##### Application launchers

See also [Wikipedia:Comparison of desktop application launchers](https://en.wikipedia.org/wiki/Comparison_of_desktop_application_launchers "wikipedia:Comparison of desktop application launchers").

*   **ADeskBar** — Easy, simple and unobtrusive application launcher for Openbox.

	[http://adeskbar.tuxfamily.org/](http://adeskbar.tuxfamily.org/) || [adeskbar](https://aur.archlinux.org/packages/adeskbar/)

*   **Albert** — An application launcher inspired by Alfred.

	[https://github.com/manuelschneid3r/albert](https://github.com/manuelschneid3r/albert) || [albert](https://aur.archlinux.org/packages/albert/)

*   **Ayr** — Manages menus of application launchers, either executables or desktop files. Also opens files and URLs with launchers, desktop files, or applications associated by name or mimetype. Uses dmenu to manage its menus.

	[http://appstogo.mcfadzean.org.uk/linux.html#ayr](http://appstogo.mcfadzean.org.uk/linux.html#ayr) || [ayr](https://aur.archlinux.org/packages/ayr/)

*   **Bashrun2** — Provides a different, barebones approach to a run dialog, using a specialized Bash session within a small xterm window.

	[http://henning-bekel.de/bashrun2/](http://henning-bekel.de/bashrun2/) || [bashrun2](https://aur.archlinux.org/packages/bashrun2/)

*   **[dmenu](/index.php/Dmenu "Dmenu")** — Fast and lightweight dynamic menu for X which is also useful as an application launcher.

	[http://tools.suckless.org/dmenu/](http://tools.suckless.org/dmenu/) || [dmenu](https://www.archlinux.org/packages/?name=dmenu)

*   **dmenu-extended** — An extension to *dmenu* for quickly opening files and folders.

	[https://github.com/markjones112358/dmenu-extended](https://github.com/markjones112358/dmenu-extended) || [dmenu-extended](https://aur.archlinux.org/packages/dmenu-extended/)

*   **dmenu-launch** — Simple *dmenu*-based application launcher. Launches binaries and XDG shortcuts.

	[https://github.com/Wintervenom/Scripts/blob/master/file/launch/dmenu-launch](https://github.com/Wintervenom/Scripts/blob/master/file/launch/dmenu-launch) || [dmenu-launch](https://aur.archlinux.org/packages/dmenu-launch/)

*   **dswitcher** — *dmenu*-based window switcher that works regardless of workspace or minimization.

	[https://github.com/Antithesisx/dswitcher](https://github.com/Antithesisx/dswitcher) || [dswitcher-git](https://aur.archlinux.org/packages/dswitcher-git/)

*   **Fehlstart** — Small GTK+-based application launcher.

	[https://gitorious.org/fehlstart](https://gitorious.org/fehlstart) || [fehlstart-git](https://aur.archlinux.org/packages/fehlstart-git/)

*   **[Gmrun](/index.php/Gmrun "Gmrun")** — Lightweight GTK+-based application launcher, with the ability to run programs inside a terminal and other handy features.

	[http://sourceforge.net/projects/gmrun/](http://sourceforge.net/projects/gmrun/) || [gmrun](https://www.archlinux.org/packages/?name=gmrun)

*   **[GNOME Do](https://en.wikipedia.org/wiki/GNOME_Do with many plugins, originally developed for the GNOME desktop.

	[http://do.cooperteam.net/](http://do.cooperteam.net/) || [gnome-do](https://www.archlinux.org/packages/?name=gnome-do)

*   **j4-dmenu-desktop** — Very fast dmenu application launcher.

	[https://github.com/enkore/j4-dmenu-desktop](https://github.com/enkore/j4-dmenu-desktop) || [j4-dmenu-desktop](https://aur.archlinux.org/packages/j4-dmenu-desktop/)

*   **Kupfer** — Convenient command and access tool for the GNOME desktop that can launch applications, open documents and access different types of objects and act on them.

	[https://wiki.gnome.org/Apps/Kupfer](https://wiki.gnome.org/Apps/Kupfer) || [kupfer](https://aur.archlinux.org/packages/kupfer/)

*   **[Launchy](https://en.wikipedia.org/wiki/Launchy "wikipedia:Launchy")** — Very popular cross-platform application launcher with a plugin-based system used to provide extra functionality.

	[http://www.launchy.net/](http://www.launchy.net/) || [launchy](https://www.archlinux.org/packages/?name=launchy)

*   **Lighthouse** — A simple scriptable popup dialog to run on X.

	[https://github.com/emgram769/lighthouse](https://github.com/emgram769/lighthouse) || [lighthouse-git](https://aur.archlinux.org/packages/lighthouse-git/)

*   **rofi** — A popup window switcher roughly based on superswitcher, requiring only xlib and pango.

	[http://davedavenport.github.io/rofi/](http://davedavenport.github.io/rofi/) || [rofi](https://www.archlinux.org/packages/?name=rofi)

*   **slingshot** — An application launcher has a clear look, part of [pantheon](/index.php/Pantheon "Pantheon") desktop environment.

	[https://launchpad.net/slingshot](https://launchpad.net/slingshot) || [slingshot-launcher](https://aur.archlinux.org/packages/slingshot-launcher/)

*   **Synapse** — Synapse is a semantic launcher written in Vala that you can use to start applications as well as find and access relevant documents and files by making use of the Zeitgeist engine.

	[https://launchpad.net/synapse-project](https://launchpad.net/synapse-project) || [synapse](https://www.archlinux.org/packages/?name=synapse)

*   **Whippet** — A launcher and xdg-open replacement for control freaks. Opens files and URLs with applications associated by name and/or mimetype. Applications and associations may be customized using an SQLite database. Uses dmenu to manage its menus.

	[http://appstogo.mcfadzean.org.uk/linux.html#whippet](http://appstogo.mcfadzean.org.uk/linux.html#whippet) || [whippet](https://aur.archlinux.org/packages/whippet/)

*   **xboomx** — Light *dmenu* wrapper that reorders commands based on popularity, written in Python.

	[https://bitbucket.org/dehun/xboomx](https://bitbucket.org/dehun/xboomx) || [xboomx](https://aur.archlinux.org/packages/xboomx/)

*   **xfce4-appfinder** — An eazy-to-use application launcher from Xfce.

	[http://docs.xfce.org/xfce/xfce4-appfinder/start](http://docs.xfce.org/xfce/xfce4-appfinder/start) || [xfce4-appfinder](https://www.archlinux.org/packages/?name=xfce4-appfinder)

*   **Yeganesh** — Light *dmenu* wrapper that reorders commands based on popularity, written in Haskell.

	[http://dmwit.com/yeganesh](http://dmwit.com/yeganesh) || [yeganesh](https://aur.archlinux.org/packages/yeganesh/)

##### Logout dialogue

A few simple shutdown managers are available:

*   **exitx** — A logout dialog for Openbox that uses [Sudo](/index.php/Sudo "Sudo").

	[http://www.linuxsir.com/bbs/lastpostinthread350740.html](http://www.linuxsir.com/bbs/lastpostinthread350740.html) || [exitx](https://aur.archlinux.org/packages/exitx/)

*   **exitx-polkit** — A GTK logout dialog for Openbox with PolicyKit support.

	[https://github.com/z0id/exitx-polkit](https://github.com/z0id/exitx-polkit) || [exitx-polkit-git](https://aur.archlinux.org/packages/exitx-polkit-git/)

*   **exitx-systemd** — A GTK logout dialog for Openbox with systemd support.

	[https://github.com/z0id/exitx-systemd](https://github.com/z0id/exitx-systemd) || [exitx-systemd-git](https://aur.archlinux.org/packages/exitx-systemd-git/)

*   **oblogout** — A graphical logout script for [Openbox](/index.php/Openbox "Openbox") that may be used with other WMs.

	[https://launchpad.net/oblogout](https://launchpad.net/oblogout) || [oblogout](https://www.archlinux.org/packages/?name=oblogout)

*   **obshutdown** — A great GTK/Cairo based shutdown manager for Openbox and other window managers.

	[https://github.com/panjandrum/obshutdown](https://github.com/panjandrum/obshutdown) || [obshutdown](https://aur.archlinux.org/packages/obshutdown/)

#### Accessibility

##### Screen reading

*   **Orca** — Screen reader for individuals who are blind or visually impaired

	[http://www.gnome.org/projects/orca](http://www.gnome.org/projects/orca) || [orca](https://www.archlinux.org/packages/?name=orca)

*   **[Simple Orca Plugin System](/index.php/Simple_Orca_Plugin_System "Simple Orca Plugin System")** — Plug-in extension for the Orca screen reader

	[https://stormdragon.tk/orca-plugins/index.php](https://stormdragon.tk/orca-plugins/index.php) || [simpleorcapluginsystem-git](https://aur.archlinux.org/packages/simpleorcapluginsystem-git/)

##### Speech recognition

See the main article [Speech recognition](/index.php/Speech_recognition "Speech recognition") for applications.

### Finance

See also [Wikipedia:Comparison of accounting software](https://en.wikipedia.org/wiki/Comparison_of_accounting_software "wikipedia:Comparison of accounting software").

*   **esniper** — Simple, lightweight tool for [sniping](https://en.wikipedia.org/wiki/Auction_sniping "wikipedia:Auction sniping") eBay auctions.

	[http://esniper.sourceforge.net/](http://esniper.sourceforge.net/) || [esniper](https://aur.archlinux.org/packages/esniper/)

*   **[GnuCash](https://en.wikipedia.org/wiki/GnuCash "wikipedia:GnuCash")** — Financial application that implements a double-entry book-keeping system with features for small business accounting.

	[http://www.gnucash.org/](http://www.gnucash.org/) || [gnucash](https://www.archlinux.org/packages/?name=gnucash)

*   **[Grisbi](https://en.wikipedia.org/wiki/Grisbi "wikipedia:Grisbi")** — Personal finance system which manages third party, expenditure and receipt categories, as well as budgetary lines, financial years, and other information that makes it suitable for associations.

	[http://www.grisbi.org/](http://www.grisbi.org/) || [grisbi](https://aur.archlinux.org/packages/grisbi/)

*   **[HomeBank](https://en.wikipedia.org/wiki/HomeBank "wikipedia:HomeBank")** — Easy to use finance manager that can analyse your personal finance in detail using powerful filtering tools and graphs.

	[http://homebank.free.fr/](http://homebank.free.fr/) || [homebank](https://www.archlinux.org/packages/?name=homebank)

*   **[KMyMoney](https://en.wikipedia.org/wiki/KMyMoney "wikipedia:KMyMoney")** — Personal finance manager that operates in a similar way to [Microsoft Money](https://en.wikipedia.org/wiki/Microsoft_Money "wikipedia:Microsoft Money"). It supports different account types, categorisation of expenses and incomes, reconciliation of bank accounts and import/export to the “QIF” file format.

	[http://kmymoney2.sourceforge.net/index-home.html](http://kmymoney2.sourceforge.net/index-home.html) || [kmymoney](https://www.archlinux.org/packages/?name=kmymoney)

*   **Ledger** — Ledger is a powerful, double-entry accounting system that is accessed from the UNIX command-line.

	[http://ledger-cli.org/](http://ledger-cli.org/) || [ledger](https://aur.archlinux.org/packages/ledger/)

*   **Moneychanger** — An intuitive QT/C++ system tray client for *Open-Transactions*

	[https://github.com/Open-Transactions/Moneychanger](https://github.com/Open-Transactions/Moneychanger) || [moneychanger-git](https://aur.archlinux.org/packages/moneychanger-git/)

*   **Manager Accounting** — Manager is free accounting software for small business.

	[http://www.manager.io/](http://www.manager.io/) || [manager-accounting](https://aur.archlinux.org/packages/manager-accounting/)

*   **Money Manager EX** — An easy-to-use personal finance suite

	[http://www.moneymanagerex.org/](http://www.moneymanagerex.org/) || [moneymanagerex](https://www.archlinux.org/packages/?name=moneymanagerex)

*   **Skrooge** — Personal finances manager for the KDE desktop.

	[http://skrooge.org/](http://skrooge.org/) || [skrooge](https://www.archlinux.org/packages/?name=skrooge)

*   **openerp** — Open source erp system purely in python.

	[http://openerp.com/](http://openerp.com/) || [openerp](https://aur.archlinux.org/packages/openerp/)

*   **Open-Transactions** — A financial cryptography library used for issuing currencies, stock, paying dividends, creating asset accounts, sending/receiving digital cash, trading on markets and escrow.

	[https://github.com/Open-Transactions/Open-Transactions](https://github.com/Open-Transactions/Open-Transactions) || [open-transactions-git](https://aur.archlinux.org/packages/open-transactions-git/)

### Flashcards

*   **[Anki](/index.php/Anki "Anki")** — Anki is a program which makes remembering things easy.

	[http://ankisrs.net/](http://ankisrs.net/) || [anki](https://www.archlinux.org/packages/?name=anki)

*   **iGNUit** — Memorization aid based on the Leitner flashcard system.

	[http://homepages.ihug.co.nz/~trmusson/programs.html#ignuit](http://homepages.ihug.co.nz/~trmusson/programs.html#ignuit) || [ignuit](https://aur.archlinux.org/packages/ignuit/)

*   **[Mnemosyne](/index.php/Mnemosyne "Mnemosyne")** — Free flash-card tool which optimizes your learning process.

	[http://mnemosyne-proj.org/](http://mnemosyne-proj.org/) || [mnemosyne](https://aur.archlinux.org/packages/mnemosyne/)

### Time management

#### Console

*   **Calcurse** — Text-based ncurses calendar and scheduling system.

	[http://calcurse.org/](http://calcurse.org/) || [calcurse](https://www.archlinux.org/packages/?name=calcurse)

*   **Doneyet** — Ncurses-based hierarchical To-do list manager written in C++.

	[https://github.com/gtaubman/doneyet](https://github.com/gtaubman/doneyet) || [doneyet](https://aur.archlinux.org/packages/doneyet/)

*   **Pal** — Very lightweight calendar with both interactive and non-interactive interfaces.

	[http://palcal.sourceforge.net/](http://palcal.sourceforge.net/) || [pal](https://aur.archlinux.org/packages/pal/)

*   **[Remind](/index.php/Remind "Remind")** — Highly sophisticated text-based calendaring and notification system.

	[http://roaringpenguin.com/products/remind](http://roaringpenguin.com/products/remind) || [remind](https://www.archlinux.org/packages/?name=remind)

*   **[Taskwarrior](https://en.wikipedia.org/wiki/Taskwarrior "wikipedia:Taskwarrior")** — Command-line To-do list application with support for lua customization and more.

	[http://taskwarrior.org/](http://taskwarrior.org/) || [task](https://www.archlinux.org/packages/?name=task)

*   **Todo.txt** — Small command-line To-do manager.

	[http://ginatrapani.github.com/todo.txt-cli/](http://ginatrapani.github.com/todo.txt-cli/) || [todotxt](https://aur.archlinux.org/packages/todotxt/)

*   **TuDu** — Ncurses-based hierarchical To-do list manager with vim-like keybindings.

	[http://code.meskio.net/tudu/](http://code.meskio.net/tudu/) || [tudu](https://aur.archlinux.org/packages/tudu/)

*   **When** — Simple personal calendar program.

	[http://lightandmatter.com/when/when.html](http://lightandmatter.com/when/when.html) || [when](https://www.archlinux.org/packages/?name=when)

*   **Wyrd** — Text-based front-end to Remind, a calendar and alarm program used on UNIX and Linux computers.

	[http://pessimization.com/software/wyrd/](http://pessimization.com/software/wyrd/) || [wyrd](https://aur.archlinux.org/packages/wyrd/)

*   **mail2rem** — Small script for importing *.ics calendars from Maildir to Remind calendar.

	[https://github.com/esovetkin/mail2rem](https://github.com/esovetkin/mail2rem) || [mail2rem-git](https://aur.archlinux.org/packages/mail2rem-git/)

*   **DevTodo** — Is a small command line application for maintaining lists of tasks.

	[http://swapoff.org/devtodo1.html](http://swapoff.org/devtodo1.html) || [devtodo](https://aur.archlinux.org/packages/devtodo/)

#### Graphical

*   **Calendar** — Calendar application for GNOME.

	[https://wiki.gnome.org/Apps/Calendar](https://wiki.gnome.org/Apps/Calendar) || [gnome-calendar](https://www.archlinux.org/packages/?name=gnome-calendar)

*   **Day Planner** — Program designed to help you easily plan and manage your time. It can manage appointments, birthdays and more.

	[http://www.day-planner.org/](http://www.day-planner.org/) || [dayplanner](https://aur.archlinux.org/packages/dayplanner/)

*   **etm (Event and Task Manager)** — Simple application with a "Getting Things Done!" approach to handling events, tasks, activities, reminders and projects.

	[http://duke.edu/~dgraham/ETM/](http://duke.edu/~dgraham/ETM/) || [etm](https://aur.archlinux.org/packages/etm/)

*   **Glista** — Simple GTK+ To-do list manager with notes support.

	[http://arr.gr/glista/](http://arr.gr/glista/) || [glista](https://aur.archlinux.org/packages/glista/)

*   **GTG (Getting Things GNOME!)** — Personal tasks and To-do list items organizer for the GNOME desktop.

	[http://gtgnome.net/](http://gtgnome.net/) || [gtg](https://aur.archlinux.org/packages/gtg/)

*   **Hamster** — Time tracking application that helps you to keep track on how much time you have spent during the day on activities you choose to track.

	[http://projecthamster.wordpress.com/](http://projecthamster.wordpress.com/) || [hamster-time-tracker](https://www.archlinux.org/packages/?name=hamster-time-tracker)

*   **[KOrganizer](https://en.wikipedia.org/wiki/Kontact#Organizer "wikipedia:Kontact")** — Calendar and scheduling program, part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[http://www.kde.org/applications/office/korganizer/](http://www.kde.org/applications/office/korganizer/) || [korganizer](https://www.archlinux.org/packages/?name=korganizer)

*   **[Lightning](https://en.wikipedia.org/wiki/Lightning_(software) "wikipedia:Lightning (software)")** — Extension to Mozilla Thunderbird that provides calendar and task support.

	[http://www.mozilla.org/projects/calendar/lightning/](http://www.mozilla.org/projects/calendar/lightning/) || [lightning](https://aur.archlinux.org/packages/lightning/)

*   **Orage** — GTK+ calendar and task manager often seen integrated with Xfce.

	[http://www.xfce.org/projects](http://www.xfce.org/projects) || [orage](https://www.archlinux.org/packages/?name=orage)

*   **Osmo** — GTK+ personal organizer, which includes calendar, tasks manager and address book modules.

	[http://clayo.org/osmo/](http://clayo.org/osmo/) || [osmo](https://www.archlinux.org/packages/?name=osmo)

*   **Outspline** — Extensible outliner with advanced time management features, supporting events with complex recurrence schemes.

	[https://kynikos.github.io/outspline/](https://kynikos.github.io/outspline/) || [outspline](https://aur.archlinux.org/packages/outspline/)

*   **QTodoTxt** — A cross-platform UI client for `todo.txt` files (see [project's page](http://todotxt.com/))

	[https://github.com/mNantern/QTodoTxt](https://github.com/mNantern/QTodoTxt) || [qtodotxt](https://aur.archlinux.org/packages/qtodotxt/) [qtodotxt-git](https://aur.archlinux.org/packages/qtodotxt-git/)

*   **Rachota** — Portable time tracker for personal projects.

	[http://rachota.sourceforge.net/](http://rachota.sourceforge.net/) || [rachota](https://aur.archlinux.org/packages/rachota/)

*   **Task Coach** — Simple open source To-do manager to manage personal tasks and To-do lists.

	[http://taskcoach.org](http://taskcoach.org) || [taskcoach](https://aur.archlinux.org/packages/taskcoach/)

*   **[Tasque](https://en.wikipedia.org/wiki/Tasque_(software) "wikipedia:Tasque (software)")** — Easy quick task management app written in C Sharp.

	[https://wiki.gnome.org/Apps/Tasque](https://wiki.gnome.org/Apps/Tasque) || [tasque](https://www.archlinux.org/packages/?name=tasque)

*   **Tider** — Lightweight time tracking application (GTK+)

	[http://pusto.org/en/tider/](http://pusto.org/en/tider/) || [tider-git](https://aur.archlinux.org/packages/tider-git/)

*   **TkRemind** — Sophisticated calendar and alarm program.

	[http://www.roaringpenguin.com/products/remind](http://www.roaringpenguin.com/products/remind) || [remind](https://www.archlinux.org/packages/?name=remind)

*   **wxRemind** — Python text and graphical frontend to Remind.

	[http://duke.edu/~dgraham/wxRemind/](http://duke.edu/~dgraham/wxRemind/) || [wxremind](https://aur.archlinux.org/packages/wxremind/)

### Emulators

An emulator is a program which serves to replicate the functions of another platform or system so as to allow applications and games to be run in environments they were not programmed for.

**Note:** For possibly more up to date selection of emulators, try checking the [AUR 'emulators' category](https://aur.archlinux.org/packages.php?O=0&K=&do_Search=Go&detail=1&L=0&C=5&SeB=nd&SB=n&SO=a&PP=25)

**Warning:** Owning a high-level emulator is not illegal, but distribution of any type of copyrighted ROMs and unauthorized emulation (without written permission of the copyright holder allowing the user to do so) are **illegal**. Consequently, Arch Linux does not distribute this copyrighted content, including game ROMs and ripped console BIOSs. You are fully responsible for whatever usage of the emulators obtained from the [official repositories](/index.php/Official_repositories "Official repositories") or the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") you make, as well as any legal repercussion that result. Arch Linux bears no responsibility at all.

#### Consoles

See also [Wikipedia:List of video game console emulators](https://en.wikipedia.org/wiki/List_of_video_game_console_emulators "wikipedia:List of video game console emulators").

*   **Citra** — Nintendo 3DS emulator.

	[http://citra-emu.org/](http://citra-emu.org/) || [citra-git](https://aur.archlinux.org/packages/citra-git/)

*   **DeSmuME** — Nintendo DS emulator.

	[http://desmume.org/](http://desmume.org/) || [desmume](https://www.archlinux.org/packages/?name=desmume)

*   **[Dolphin](/index.php/Dolphin_emulator "Dolphin emulator")** — Very capable GameCube and Wii emulator.

	[http://dolphin-emu.org/](http://dolphin-emu.org/) || [dolphin-emu](https://www.archlinux.org/packages/?name=dolphin-emu)

*   **epsxe** — Emulator for the PlayStation video game console for x86-based PC hardware.

	[http://www.epsxe.com/](http://www.epsxe.com/) || [epsxe](https://aur.archlinux.org/packages/epsxe/)

*   **fakenes** — NES (Nintendo Famicom) emulator.

	[http://fakenes.sourceforge.net/](http://fakenes.sourceforge.net/) || [fakenes](https://aur.archlinux.org/packages/fakenes/)

*   **FCEUX** — NTSC and PAL 8 bit Nintendo/Famicom emulator that is an evolution of the original FCE Ultra emulator. It is accurate, compatible and actively maintained.

	[http://fceux.com/](http://fceux.com/) || [fceux](https://www.archlinux.org/packages/?name=fceux)

*   **Gens2** — Emulator for Sega Genesis, Sega CD and 32X that is written in assembly language and no longer actively developed.

*   activate OpenGL, set video resolution per custom to 1024x600 for streched full-screen or 800x600 for non-streched;
*   use "Normal" renderer, I couldn't find a visible advantage with the other ones.

	[http://www.gens.me/](http://www.gens.me/) || [gens](https://www.archlinux.org/packages/?name=gens)

*   **Gens-GS** — Gens2, rewritten in C++, combining features from various Gens forks.

	[http://segaretro.org/Gens/GS](http://segaretro.org/Gens/GS) || [gens-gs](https://www.archlinux.org/packages/?name=gens-gs)

*   **gngeo** — Command-line NeoGeo emulator.

	[http://gngeo.googlecode.com](http://gngeo.googlecode.com) || [gngeo](https://aur.archlinux.org/packages/gngeo/)

*   **higan** — Multisystem emulator focusing on accuracy, supporting SNES, NES, GB, GBC, GBA.

	[http://code.google.com/p/higan/](http://code.google.com/p/higan/) || [higan](https://www.archlinux.org/packages/?name=higan)

*   **mednafen** — Command line driven multi system emulator.

	[http://mednafen.sourceforge.net/](http://mednafen.sourceforge.net/) || [mednafen](https://www.archlinux.org/packages/?name=mednafen)

*   **Mupen64Plus** — Highly compatible Nintendo 64 emulator with plugin system.

	[http://code.google.com/p/mupen64plus/](http://code.google.com/p/mupen64plus/) || [mupen64plus](https://www.archlinux.org/packages/?name=mupen64plus) or a graphical front-end, such as [m64py](https://aur.archlinux.org/packages/m64py/) or [cutemupen](https://aur.archlinux.org/packages/cutemupen/).

*   **pSX** — A not plugin-based PlayStation emulator with fairly high compatibility.

	[http://psxemulator.gazaxian.com/](http://psxemulator.gazaxian.com/) || [psx](https://aur.archlinux.org/packages/psx/)

*   **PCSXR** — PlayStation emulator; Debian fork of the abandoned original PCSX

	[http://pcsxr.codeplex.com/](http://pcsxr.codeplex.com/) || [pcsxr](https://www.archlinux.org/packages/?name=pcsxr)

*   **PCSX2** — PlayStation 2 emulator. It is still being maintained and developed. It requires BIOS files.

	[http://www.pcsx2.net/](http://www.pcsx2.net/) || [pcsx2](https://www.archlinux.org/packages/?name=pcsx2)

*   **snes-9x** — Portable, freeware Super Nintendo Entertainment System (SNES) emulator.

	[http://www.snes9x.com/](http://www.snes9x.com/) || [snes9x](https://www.archlinux.org/packages/?name=snes9x)

*   **[Visual Boy Advance](/index.php/Visual_Boy_Advance "Visual Boy Advance")** — Game Boy emulator with Game Boy Advance, Game Boy Color, and Super Game Boy support.

	[http://vba.ngemu.com/](http://vba.ngemu.com/) || [vbam-gtk](https://www.archlinux.org/packages/?name=vbam-gtk)

*   **ZSNES** — Highly compatible Super Nintendo emulator.

	[http://www.zsnes.com/](http://www.zsnes.com/) || [zsnes](https://www.archlinux.org/packages/?name=zsnes)

#### Other

*   **DOSBox** — Open-source DOS emulator which primarily focuses on running DOS Games.

	[http://www.dosbox.com/](http://www.dosbox.com/) || [dosbox](https://www.archlinux.org/packages/?name=dosbox)

*   **DOSEmu** — Open-source DOS emulator.

	[http://www.dosemu.org/](http://www.dosemu.org/) || [dosemu](https://www.archlinux.org/packages/?name=dosemu)

*   **MAME** — Multiple Arcade Machine Emulator.

	[http://mamedev.org/](http://mamedev.org/) || [sdlmame](https://www.archlinux.org/packages/?name=sdlmame)

*   **ResidualVM** — Cross-platform 3D game interpreter which allows you to play LucasArts' Lua-based 3D adventures.

	[http://residualvm.org/](http://residualvm.org/) || [residualvm](https://aur.archlinux.org/packages/residualvm/)

*   **[RetroArch](/index.php/RetroArch "RetroArch")** — Frontend to libretro (emulation library, using modified versions of existing emulators as plugins).

	[http://www.libretro.com/](http://www.libretro.com/) || [retroarch](https://www.archlinux.org/packages/?name=retroarch)

*   **ScummVM** — Virtual machine for old school adventures.

	[http://www.scummvm.org/](http://www.scummvm.org/) || [scummvm](https://www.archlinux.org/packages/?name=scummvm)

*   **X Neko Project II** — PC-9801 emulator.

	[http://www.asahi-net.or.jp/~aw9k-nnk/np2/](http://www.asahi-net.or.jp/~aw9k-nnk/np2/) || [xnp2](https://aur.archlinux.org/packages/xnp2/)

### Amateur radio

See the main article: [Amateur radio#Software list](/index.php/Amateur_radio#Software_list "Amateur radio").

See also [Wikipedia:List of software-defined radios](https://en.wikipedia.org/wiki/List_of_software-defined_radios "wikipedia:List of software-defined radios").

## 参见

*   [终端中的应用列表，包含截图和评论](http://kmandla.wordpress.com/software/)
*   [Arch Linux Forums / LnF Awards 2011](https://bbs.archlinux.org/viewtopic.php?id=111878) - 2011 年度最佳轻量程序。
*   [Arch Linux Forums / LnF Awards 2012](https://bbs.archlinux.org/viewtopic.php?id=138281) - 2012 年度最佳轻量程序。
*   [Survey: Vote for the most popular apps of 2013-2014](https://bbs.archlinux.org/viewtopic.php?id=174764)
*   [http://sourceforge.net/](http://sourceforge.net/) 开源软件
*   [http://www.oschina.net/](http://www.oschina.net/) 开源中国社区
*   [http://linuxappfinder.com/](http://linuxappfinder.com/)
*   [http://www.linuxlinks.com/](http://www.linuxlinks.com/)
*   [Wikipedia:List of open source software packages](https://en.wikipedia.org/wiki/List_of_open_source_software_packages "wikipedia:List of open source software packages")
*   [http://linuxappfinder.com/alternatives](http://linuxappfinder.com/alternatives) - Windows 和 OS X 软件的替代品
*   [http://alternativeto.net/](http://alternativeto.net/) - 寻找流行的程序的替代品
*   [http://www.linuxalt.com/](http://www.linuxalt.com/) - Windows 软件对应的 Linux 软件
*   [http://lin-app.com/](http://lin-app.com/) - 广大程序与 Linux 游戏的在线信息库
*   [http://www.osalt.com/](http://www.osalt.com/)