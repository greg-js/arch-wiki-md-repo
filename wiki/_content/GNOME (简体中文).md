# GNOME (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

相关文章

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [GTK+](/index.php/GTK%2B "GTK+")
*   [GDM](/index.php/GDM "GDM")
*   [GNOME Files](/index.php/GNOME_Files "GNOME Files")
*   [Gedit](/index.php/Gedit "Gedit")
*   [Epiphany](/index.php/Epiphany "Epiphany")
*   [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")

**翻译状态：** 本文是英文页面 [GNOME](/index.php/GNOME "GNOME") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-10-05，点击[这里](https://wiki.archlinux.org/index.php?title=GNOME&diff=0&oldid=400254)可以查看翻译后英文页面的改动。

GNOME (pronounced _gah-nohm_ or _nohm_)是一个简单易用的[桌面环境](/index.php/Desktop_environment_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Desktop environment (简体中文)") .它由[The GNOME Project](https://en.wikipedia.org/wiki/The_GNOME_Project "wikipedia:The GNOME Project") 设计并且完全自由和开源. GNOME是[GNU Project](https://en.wikipedia.org/wiki/GNU_Project "wikipedia:GNU Project")的一部分.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 附加的软件包](#.E9.99.84.E5.8A.A0.E7.9A.84.E8.BD.AF.E4.BB.B6.E5.8C.85)
*   [2 GNOME会话](#GNOME.E4.BC.9A.E8.AF.9D)
*   [3 运行 GNOME](#.E8.BF.90.E8.A1.8C_GNOME)
    *   [3.1 图形界面登录](#.E5.9B.BE.E5.BD.A2.E7.95.8C.E9.9D.A2.E7.99.BB.E5.BD.95)
    *   [3.2 Wayland 中的 GNOME 应用程序](#Wayland_.E4.B8.AD.E7.9A.84_GNOME_.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
*   [4 导览](#.E5.AF.BC.E8.A7.88)
    *   [4.1 重启 GNOME shell](#.E9.87.8D.E5.90.AF_GNOME_shell)
    *   [4.2 GNOME Shell 崩溃](#GNOME_Shell_.E5.B4.A9.E6.BA.83)
    *   [4.3 遗留名称](#.E9.81.97.E7.95.99.E5.90.8D.E7.A7.B0)
*   [5 配置](#.E9.85.8D.E7.BD.AE)
    *   [5.1 GNOME 系统设置](#GNOME_.E7.B3.BB.E7.BB.9F.E8.AE.BE.E7.BD.AE)
        *   [5.1.1 色彩设置](#.E8.89.B2.E5.BD.A9.E8.AE.BE.E7.BD.AE)
        *   [5.1.2 日期与时间](#.E6.97.A5.E6.9C.9F.E4.B8.8E.E6.97.B6.E9.97.B4)
        *   [5.1.3 默认应用程序](#.E9.BB.98.E8.AE.A4.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
        *   [5.1.4 鼠标和触摸板](#.E9.BC.A0.E6.A0.87.E5.92.8C.E8.A7.A6.E6.91.B8.E6.9D.BF)
        *   [5.1.5 网络](#.E7.BD.91.E7.BB.9C)
        *   [5.1.6 在线帐户](#.E5.9C.A8.E7.BA.BF.E5.B8.90.E6.88.B7)
        *   [5.1.7 搜索](#.E6.90.9C.E7.B4.A2)
    *   [5.2 高级设置](#.E9.AB.98.E7.BA.A7.E8.AE.BE.E7.BD.AE)
        *   [5.2.1 外观](#.E5.A4.96.E8.A7.82)
            *   [5.2.1.1 GTK+主题和图标主题](#GTK.2B.E4.B8.BB.E9.A2.98.E5.92.8C.E5.9B.BE.E6.A0.87.E4.B8.BB.E9.A2.98)
                *   [5.2.1.1.1 全局暗色主题](#.E5.85.A8.E5.B1.80.E6.9A.97.E8.89.B2.E4.B8.BB.E9.A2.98)
            *   [5.2.1.2 窗口管理器主题](#.E7.AA.97.E5.8F.A3.E7.AE.A1.E7.90.86.E5.99.A8.E4.B8.BB.E9.A2.98)
                *   [5.2.1.2.1 标题栏的高度](#.E6.A0.87.E9.A2.98.E6.A0.8F.E7.9A.84.E9.AB.98.E5.BA.A6)
                *   [5.2.1.2.2 标题栏按钮重新排序](#.E6.A0.87.E9.A2.98.E6.A0.8F.E6.8C.89.E9.92.AE.E9.87.8D.E6.96.B0.E6.8E.92.E5.BA.8F)
                *   [5.2.1.2.3 最大化时隐藏标题栏](#.E6.9C.80.E5.A4.A7.E5.8C.96.E6.97.B6.E9.9A.90.E8.97.8F.E6.A0.87.E9.A2.98.E6.A0.8F)
            *   [5.2.1.3 GNOME Shell主题](#GNOME_Shell.E4.B8.BB.E9.A2.98)
        *   [5.2.2 桌面](#.E6.A1.8C.E9.9D.A2)
            *   [5.2.2.1 桌面上的图标](#.E6.A1.8C.E9.9D.A2.E4.B8.8A.E7.9A.84.E5.9B.BE.E6.A0.87)
            *   [5.2.2.2 锁屏和背景](#.E9.94.81.E5.B1.8F.E5.92.8C.E8.83.8C.E6.99.AF)
        *   [5.2.3 扩展](#.E6.89.A9.E5.B1.95)
        *   [5.2.4 输入法](#.E8.BE.93.E5.85.A5.E6.B3.95)
        *   [5.2.5 字体](#.E5.AD.97.E4.BD.93)
        *   [5.2.6 启动应用程序](#.E5.90.AF.E5.8A.A8.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
        *   [5.2.7 电源](#.E7.94.B5.E6.BA.90)
            *   [5.2.7.1 Hibernate the computer when lid is closed](#Hibernate_the_computer_when_lid_is_closed)
            *   [5.2.7.2 Prevent Suspend-To-RAM (S3) when closing the lid](#Prevent_Suspend-To-RAM_.28S3.29_when_closing_the_lid)
            *   [5.2.7.3 Change critical battery level action](#Change_critical_battery_level_action)
        *   [5.2.8 Sort applications into application (app) folders](#Sort_applications_into_application_.28app.29_folders)
*   [6 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [6.1 键盘](#.E9.94.AE.E7.9B.98)
        *   [6.1.1 登陆打开NumLock键](#.E7.99.BB.E9.99.86.E6.89.93.E5.BC.80NumLock.E9.94.AE)
        *   [6.1.2 热键选择](#.E7.83.AD.E9.94.AE.E9.80.89.E6.8B.A9)
        *   [6.1.3 打开键盘开关命令](#.E6.89.93.E5.BC.80.E9.94.AE.E7.9B.98.E5.BC.80.E5.85.B3.E5.91.BD.E4.BB.A4)
        *   [6.1.4 XkbOptions键盘选项](#XkbOptions.E9.94.AE.E7.9B.98.E9.80.89.E9.A1.B9)
        *   [6.1.5 De-bind Windows key](#De-bind_Windows_key)
    *   [6.2 磁盘](#.E7.A3.81.E7.9B.98)
    *   [6.3 从菜单隐藏的应用程序](#.E4.BB.8E.E8.8F.9C.E5.8D.95.E9.9A.90.E8.97.8F.E7.9A.84.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F)
    *   [6.4 截屏记录](#.E6.88.AA.E5.B1.8F.E8.AE.B0.E5.BD.95)
    *   [6.5 截图](#.E6.88.AA.E5.9B.BE)
    *   [6.6 注销延迟](#.E6.B3.A8.E9.94.80.E5.BB.B6.E8.BF.9F)
    *   [6.7 禁用动画](#.E7.A6.81.E7.94.A8.E5.8A.A8.E7.94.BB)
    *   [6.8 Retina (HiDPI) display support](#Retina_.28HiDPI.29_display_support)
    *   [6.9 密码和密钥 (PGP Keys)](#.E5.AF.86.E7.A0.81.E5.92.8C.E5.AF.86.E9.92.A5_.28PGP_Keys.29)
    *   [6.10 终端](#.E7.BB.88.E7.AB.AF)
        *   [6.10.1 更改默认的终端大小](#.E6.9B.B4.E6.94.B9.E9.BB.98.E8.AE.A4.E7.9A.84.E7.BB.88.E7.AB.AF.E5.A4.A7.E5.B0.8F)
        *   [6.10.2 新终端采用当前目录](#.E6.96.B0.E7.BB.88.E7.AB.AF.E9.87.87.E7.94.A8.E5.BD.93.E5.89.8D.E7.9B.AE.E5.BD.95)
        *   [6.10.3 Pad the terminal](#Pad_the_terminal)
        *   [6.10.4 禁用光标闪烁](#.E7.A6.81.E7.94.A8.E5.85.89.E6.A0.87.E9.97.AA.E7.83.81)
        *   [6.10.5 关闭终端时，禁用确认窗口](#.E5.85.B3.E9.97.AD.E7.BB.88.E7.AB.AF.E6.97.B6.EF.BC.8C.E7.A6.81.E7.94.A8.E7.A1.AE.E8.AE.A4.E7.AA.97.E5.8F.A3)
    *   [6.11 鼠标中键](#.E9.BC.A0.E6.A0.87.E4.B8.AD.E9.94.AE)
    *   [6.12 启用按钮和菜单图标](#.E5.90.AF.E7.94.A8.E6.8C.89.E9.92.AE.E5.92.8C.E8.8F.9C.E5.8D.95.E5.9B.BE.E6.A0.87)
    *   [6.13 使用自定义的色彩和渐变色的桌面背景](#.E4.BD.BF.E7.94.A8.E8.87.AA.E5.AE.9A.E4.B9.89.E7.9A.84.E8.89.B2.E5.BD.A9.E5.92.8C.E6.B8.90.E5.8F.98.E8.89.B2.E7.9A.84.E6.A1.8C.E9.9D.A2.E8.83.8C.E6.99.AF)
    *   [6.14 gnome terminal透明](#gnome_terminal.E9.80.8F.E6.98.8E)
    *   [6.15 渐变背景](#.E6.B8.90.E5.8F.98.E8.83.8C.E6.99.AF)
    *   [6.16 GNOME Files](#GNOME_Files)
        *   [6.16.1 移除侧边栏计算机中的文件夹](#.E7.A7.BB.E9.99.A4.E4.BE.A7.E8.BE.B9.E6.A0.8F.E8.AE.A1.E7.AE.97.E6.9C.BA.E4.B8.AD.E7.9A.84.E6.96.87.E4.BB.B6.E5.A4.B9)
        *   [6.16.2 地址栏显示文本路径](#.E5.9C.B0.E5.9D.80.E6.A0.8F.E6.98.BE.E7.A4.BA.E6.96.87.E6.9C.AC.E8.B7.AF.E5.BE.84)
    *   [6.17 GNOME 面板](#GNOME_.E9.9D.A2.E6.9D.BF)
        *   [6.17.1 在时间栏显示日期](#.E5.9C.A8.E6.97.B6.E9.97.B4.E6.A0.8F.E6.98.BE.E7.A4.BA.E6.97.A5.E6.9C.9F)
        *   [6.17.2 隐藏顶部面板的图标](#.E9.9A.90.E8.97.8F.E9.A1.B6.E9.83.A8.E9.9D.A2.E6.9D.BF.E7.9A.84.E5.9B.BE.E6.A0.87)
        *   [6.17.3 去掉注销时的延迟](#.E5.8E.BB.E6.8E.89.E6.B3.A8.E9.94.80.E6.97.B6.E7.9A.84.E5.BB.B6.E8.BF.9F)
    *   [6.18 活动视图](#.E6.B4.BB.E5.8A.A8.E8.A7.86.E5.9B.BE)
        *   [6.18.1 从应用程序视图移除应用程序项目](#.E4.BB.8E.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E8.A7.86.E5.9B.BE.E7.A7.BB.E9.99.A4.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E9.A1.B9.E7.9B.AE)
        *   [6.18.2 怎样改变应用程序图标大小](#.E6.80.8E.E6.A0.B7.E6.94.B9.E5.8F.98.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E5.9B.BE.E6.A0.87.E5.A4.A7.E5.B0.8F)
        *   [6.18.3 禁止鼠标接触 hot corner（左上角）切换活动视图](#.E7.A6.81.E6.AD.A2.E9.BC.A0.E6.A0.87.E6.8E.A5.E8.A7.A6_hot_corner.EF.BC.88.E5.B7.A6.E4.B8.8A.E8.A7.92.EF.BC.89.E5.88.87.E6.8D.A2.E6.B4.BB.E5.8A.A8.E8.A7.86.E5.9B.BE)
    *   [6.19 标题栏](#.E6.A0.87.E9.A2.98.E6.A0.8F)
        *   [6.19.1 减少标题栏高度](#.E5.87.8F.E5.B0.91.E6.A0.87.E9.A2.98.E6.A0.8F.E9.AB.98.E5.BA.A6)
    *   [6.20 登录屏幕](#.E7.99.BB.E5.BD.95.E5.B1.8F.E5.B9.95)
        *   [6.20.1 登录管理器壁纸](#.E7.99.BB.E5.BD.95.E7.AE.A1.E7.90.86.E5.99.A8.E5.A3.81.E7.BA.B8)
        *   [6.20.2 登录界面大字体](#.E7.99.BB.E5.BD.95.E7.95.8C.E9.9D.A2.E5.A4.A7.E5.AD.97.E4.BD.93)
        *   [6.20.3 关闭声音](#.E5.85.B3.E9.97.AD.E5.A3.B0.E9.9F.B3)
        *   [6.20.4 按电源键启用交互界面](#.E6.8C.89.E7.94.B5.E6.BA.90.E9.94.AE.E5.90.AF.E7.94.A8.E4.BA.A4.E4.BA.92.E7.95.8C.E9.9D.A2)
        *   [6.20.5 改变 GDM 的键盘布局](#.E6.94.B9.E5.8F.98_GDM_.E7.9A.84.E9.94.AE.E7.9B.98.E5.B8.83.E5.B1.80)
        *   [6.20.6 gnome terminal透明](#gnome_terminal.E9.80.8F.E6.98.8E_2)
        *   [6.20.7 启用备用模式](#.E5.90.AF.E7.94.A8.E5.A4.87.E7.94.A8.E6.A8.A1.E5.BC.8F)
    *   [6.21 其他技巧](#.E5.85.B6.E4.BB.96.E6.8A.80.E5.B7.A7)
*   [7 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [7.1 Shell freezes](#Shell_freezes)
    *   [7.2 Incorrect application defaults](#Incorrect_application_defaults)
    *   [7.3 Tracker & Documents do not list any local files](#Tracker_.26_Documents_do_not_list_any_local_files)
    *   [7.4 Unable to add accounts in Empathy and GNOME Online Accounts](#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts)
    *   [7.5 Cannot change settings in dconf-editor](#Cannot_change_settings_in_dconf-editor)
    *   [7.6 When an extension breaks the shell](#When_an_extension_breaks_the_shell)
    *   [7.7 扩展在 GNOME 3 升级后不工作了](#.E6.89.A9.E5.B1.95.E5.9C.A8_GNOME_3_.E5.8D.87.E7.BA.A7.E5.90.8E.E4.B8.8D.E5.B7.A5.E4.BD.9C.E4.BA.86)
    *   [7.8 只有 conky 运行时键盘快捷方式不工作](#.E5.8F.AA.E6.9C.89_conky_.E8.BF.90.E8.A1.8C.E6.97.B6.E9.94.AE.E7.9B.98.E5.BF.AB.E6.8D.B7.E6.96.B9.E5.BC.8F.E4.B8.8D.E5.B7.A5.E4.BD.9C)
    *   [7.9 Unable to apply stored configuration for monitors](#Unable_to_apply_stored_configuration_for_monitors)
    *   [7.10 一致的光标主题](#.E4.B8.80.E8.87.B4.E7.9A.84.E5.85.89.E6.A0.87.E4.B8.BB.E9.A2.98)
    *   [7.11 Windows cannot be modified with Alt-Key + mouse-button](#Windows_cannot_be_modified_with_Alt-Key_.2B_mouse-button)
    *   [7.12 加载速度慢的系统图标/慢GDM登录](#.E5.8A.A0.E8.BD.BD.E9.80.9F.E5.BA.A6.E6.85.A2.E7.9A.84.E7.B3.BB.E7.BB.9F.E5.9B.BE.E6.A0.87.2F.E6.85.A2GDM.E7.99.BB.E5.BD.95)
    *   [7.13 Artifacts when maximizing windows](#Artifacts_when_maximizing_windows)
    *   [7.14 Tear-free video with Intel HD Graphics](#Tear-free_video_with_Intel_HD_Graphics)
    *   [7.15 Window opens behind other windows when using multiple monitors](#Window_opens_behind_other_windows_when_using_multiple_monitors)
    *   [7.16 锁定按钮无法重新启用触摸板](#.E9.94.81.E5.AE.9A.E6.8C.89.E9.92.AE.E6.97.A0.E6.B3.95.E9.87.8D.E6.96.B0.E5.90.AF.E7.94.A8.E8.A7.A6.E6.91.B8.E6.9D.BF)
    *   [7.17 密码不记得](#.E5.AF.86.E7.A0.81.E4.B8.8D.E8.AE.B0.E5.BE.97)
    *   [7.18 GNOME Shell键盘源菜单不可见](#GNOME_Shell.E9.94.AE.E7.9B.98.E6.BA.90.E8.8F.9C.E5.8D.95.E4.B8.8D.E5.8F.AF.E8.A7.81)
    *   [7.19 鼠标指针丢失](#.E9.BC.A0.E6.A0.87.E6.8C.87.E9.92.88.E4.B8.A2.E5.A4.B1)
    *   [7.20 在会话菜单中没有重启按钮时，屏幕被锁定](#.E5.9C.A8.E4.BC.9A.E8.AF.9D.E8.8F.9C.E5.8D.95.E4.B8.AD.E6.B2.A1.E6.9C.89.E9.87.8D.E5.90.AF.E6.8C.89.E9.92.AE.E6.97.B6.EF.BC.8C.E5.B1.8F.E5.B9.95.E8.A2.AB.E9.94.81.E5.AE.9A)
    *   [7.21 pulseaudio系统原因延误GNOME和GDM](#pulseaudio.E7.B3.BB.E7.BB.9F.E5.8E.9F.E5.9B.A0.E5.BB.B6.E8.AF.AFGNOME.E5.92.8CGDM)
    *   [7.22 GNOME 登录需要花很长的时间](#GNOME_.E7.99.BB.E5.BD.95.E9.9C.80.E8.A6.81.E8.8A.B1.E5.BE.88.E9.95.BF.E7.9A.84.E6.97.B6.E9.97.B4)
    *   [7.23 安装扩展导致 GNOME 停止工作](#.E5.AE.89.E8.A3.85.E6.89.A9.E5.B1.95.E5.AF.BC.E8.87.B4_GNOME_.E5.81.9C.E6.AD.A2.E5.B7.A5.E4.BD.9C)
    *   [7.24 GTK 2+ 应用程序显示段错误无法启动](#GTK_2.2B_.E5.BA.94.E7.94.A8.E7.A8.8B.E5.BA.8F.E6.98.BE.E7.A4.BA.E6.AE.B5.E9.94.99.E8.AF.AF.E6.97.A0.E6.B3.95.E5.90.AF.E5.8A.A8)
    *   [7.25 ATI Catalyst 驱动在使用 GNOME Shell 的时候遭遇到了毛刺和伪影](#ATI_Catalyst_.E9.A9.B1.E5.8A.A8.E5.9C.A8.E4.BD.BF.E7.94.A8_GNOME_Shell_.E7.9A.84.E6.97.B6.E5.80.99.E9.81.AD.E9.81.87.E5.88.B0.E4.BA.86.E6.AF.9B.E5.88.BA.E5.92.8C.E4.BC.AA.E5.BD.B1)
    *   [7.26 多台显示器和 dock 扩展](#.E5.A4.9A.E5.8F.B0.E6.98.BE.E7.A4.BA.E5.99.A8.E5.92.8C_dock_.E6.89.A9.E5.B1.95)
    *   [7.27 Empathy和其他程序没有环境音](#Empathy.E5.92.8C.E5.85.B6.E4.BB.96.E7.A8.8B.E5.BA.8F.E6.B2.A1.E6.9C.89.E7.8E.AF.E5.A2.83.E9.9F.B3)
    *   [7.28 通过 can-change-accels 编辑快捷键失败](#.E9.80.9A.E8.BF.87_can-change-accels_.E7.BC.96.E8.BE.91.E5.BF.AB.E6.8D.B7.E9.94.AE.E5.A4.B1.E8.B4.A5)
    *   [7.29 在备用模式右键点击面板停止响应](#.E5.9C.A8.E5.A4.87.E7.94.A8.E6.A8.A1.E5.BC.8F.E5.8F.B3.E9.94.AE.E7.82.B9.E5.87.BB.E9.9D.A2.E6.9D.BF.E5.81.9C.E6.AD.A2.E5.93.8D.E5.BA.94)
    *   [7.30 "显示桌面"快捷键无效](#.22.E6.98.BE.E7.A4.BA.E6.A1.8C.E9.9D.A2.22.E5.BF.AB.E6.8D.B7.E9.94.AE.E6.97.A0.E6.95.88)
    *   [7.31 GNOME Files 不启动](#GNOME_Files_.E4.B8.8D.E5.90.AF.E5.8A.A8)
    *   [7.32 不能保存显示器配置文件](#.E4.B8.8D.E8.83.BD.E4.BF.9D.E5.AD.98.E6.98.BE.E7.A4.BA.E5.99.A8.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
    *   [7.33 按触摸板锁定键不能重新启用触摸板](#.E6.8C.89.E8.A7.A6.E6.91.B8.E6.9D.BF.E9.94.81.E5.AE.9A.E9.94.AE.E4.B8.8D.E8.83.BD.E9.87.8D.E6.96.B0.E5.90.AF.E7.94.A8.E8.A7.A6.E6.91.B8.E6.9D.BF)
    *   [7.34 在 GNOME Files 里面 CTRL+V 粘贴路径而不是文件](#.E5.9C.A8_GNOME_Files_.E9.87.8C.E9.9D.A2_CTRL.2BV_.E7.B2.98.E8.B4.B4.E8.B7.AF.E5.BE.84.E8.80.8C.E4.B8.8D.E6.98.AF.E6.96.87.E4.BB.B6)
    *   [7.35 不能连接到加密 Wi-Fi](#.E4.B8.8D.E8.83.BD.E8.BF.9E.E6.8E.A5.E5.88.B0.E5.8A.A0.E5.AF.86_Wi-Fi)
    *   [7.36 “Mutter 命令 33 尚未定义。”](#.E2.80.9CMutter_.E5.91.BD.E4.BB.A4_33_.E5.B0.9A.E6.9C.AA.E5.AE.9A.E4.B9.89.E3.80.82.E2.80.9D)
    *   [7.37 “Mutter-dialig：终端命令未定义”](#.E2.80.9CMutter-dialig.EF.BC.9A.E7.BB.88.E7.AB.AF.E5.91.BD.E4.BB.A4.E6.9C.AA.E5.AE.9A.E4.B9.89.E2.80.9D)
    *   [7.38 Intel CPU 用户开机引导到 GDM 界面提示“oh no”](#Intel_CPU_.E7.94.A8.E6.88.B7.E5.BC.80.E6.9C.BA.E5.BC.95.E5.AF.BC.E5.88.B0_GDM_.E7.95.8C.E9.9D.A2.E6.8F.90.E7.A4.BA.E2.80.9Coh_no.E2.80.9D)
*   [8 外部链接](#.E5.A4.96.E9.83.A8.E9.93.BE.E6.8E.A5)

## 安装

以下两个软件包（组）均包含 GNOME 的组件：

**gnome** 包组包含基本桌面环境和软件，以提供标准的 GNOME 体验。

**gnome-extra** 包组包含剩余的可选工具，例如文本编辑器、压缩文件管理器、光盘烧录工具、邮件客户端、游戏、开发工具及其它非必需的软件。这些软件与 GNOME 桌面的集成很好。假如您不想安装 GNOME 全部的软件包，在安装它的时候注意看软件包描述（或者你可以先安装再删除他们）。

**Note:** _mutter_ acts as a composite manager for the desktop, employing hardware graphics acceleration to provide effects aimed at reducing screen clutter. The GNOME session manager automatically detects if your video driver is capable of running GNOME Shell and if not, falls back to software rendering using _llvmpipe_.

### 附加的软件包

上面提到的包组不包括这些包：

*   **[Boxes](https://en.wikipedia.org/wiki/GNOME_Boxes "wikipedia:GNOME Boxes")** — A simple user interface to access [libvirt](/index.php/Libvirt "Libvirt") virtual machines.

[https://wiki.gnome.org/Apps/Boxes](https://wiki.gnome.org/Apps/Boxes) || [gnome-boxes](https://www.archlinux.org/packages/?name=gnome-boxes)

*   **GNOME Initial Setup** — A simple, easy, and safe way to prepare a new system.

[https://github.com/GNOME/gnome-initial-setup](https://github.com/GNOME/gnome-initial-setup) || [gnome-initial-setup](https://www.archlinux.org/packages/?name=gnome-initial-setup)

*   **GNOME PackageKit** — Collection of graphical tools for PackageKit to be used in the GNOME desktop.

[https://github.com/GNOME/gnome-packagekit](https://github.com/GNOME/gnome-packagekit) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **[Nemiver](https://en.wikipedia.org/wiki/Nemiver "wikipedia:Nemiver")** — A C/C++ debugger.

[https://wiki.gnome.org/Apps/Nemiver](https://wiki.gnome.org/Apps/Nemiver) || [nemiver](https://www.archlinux.org/packages/?name=nemiver)

*   **[Software](https://en.wikipedia.org/wiki/GNOME_Software "wikipedia:GNOME Software")** — Lets you install and update applications and system extensions.

[https://wiki.gnome.org/Apps/Software/](https://wiki.gnome.org/Apps/Software/) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

## GNOME会话

GNOME 有三个可用的会话，都使用 GNOME Shell

*   **GNOME** 是默认会话, 有创新的布局
*   **GNOME Classic** 的桌面布局类似于传统的GNOME 2, using pre-activated extensions and parameters. [[1]](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/) Hence it is more a customized GNOME Shell than a truly distinct mode
*   **GNOME on Wayland** GNOME Shell 在新的Wayland协议上运行. 而传统的 X 应用程序在Xwayland上运行

## 运行 GNOME

GNOME可以通过 [显示管理器](/index.php/Display_manager_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Display manager (简体中文)")以图形方式启动,或者从控制台手动启动。 为优化桌面整合, 建议使用[GDM (简体中文)](/index.php/GDM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GDM (简体中文)") (GNOME显示管理器)。 注意 [启用](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BD.BF.E7.94.A8.E5.8D.95.E5.85.83 "Systemd (简体中文)") 一个显示管理器(例如GDM)意味着Xorg将会以root权限运行.

**注意:** 如果不使用 GDM，你将无法体验到对锁屏的原生支持，因此你不得不使用另一个屏幕锁来提供类似功能，参见[Xmonad (简体中文)#GNOME 3 and xmonad](/index.php/Xmonad_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#GNOME_3_and_xmonad "Xmonad (简体中文)").

### 图形界面登录

可以在登录管理器中选择 _GNOME',_ GNOME Classic _或_ GNOME on Wayland _作为登录选项。_

### Wayland 中的 GNOME 应用程序

根据当前的默认情况，GNOME 应用程序会利用 XWayland，以传统 X 应用程序的方式运行。若需在 Wayland 下测试 GNOME 应用，请以命令行方式运行程序，并加上以下前缀： `env GDK_BACKEND=wayland <command>`。

**Note:** 可以设置全局的 Wayland 环境，使用 `env GDK_BACKEND=wayland gnome-session --session=gnome-wayland`。 但是现在无法工作—— _gnome-session_ 会立即闪退.

请查看以下页面以了解开发进展： [GNOME Applications under Wayland](https://wiki.gnome.org/Initiatives/Wayland/Applications/).

## 导览

您可以阅读这篇文章： [GNOME Shell cheat sheet](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet) 以了解如何高效地使用 GNOME shell，它展示了 GNOME shell 的特色与使用快捷键。文章内容包括怎么切换任务，使用键盘，窗口控制，使用面板，预览模式等。 部分常用的快捷键：

*   `Super`： 进入预览模式
*   `Super` + `m`： 显示消息托盘
*   `Super` + `a`：显示应用程序菜单
*   `Alt` + `F2`：输入命令以快速启动应用
*   `Alt` + `F2`，然后输入 `r` 或 `restart`，再 `Enter`：重启 GNOME shell。这一条在你遇到 shell 图形界面错误时十分有用。

### 重启 GNOME shell

当修改过界面之后你可能需要重启 GNOME shell。你可以重新登陆，不过有一个简单快捷的方法。 按 `Alt` + `F2` 再输入 `r` 再 `Enter`

### GNOME Shell 崩溃

一些特定的微调或者经常性重启 Shell 会导致 shell 在将要重启的时候崩溃。这个时候你必须做好心理准备，然后强制注销。有一些修改，例如在_**GNOME Shell**_ 和 _**fallback mode,**_ 之间切换，不能简单地使用 r 重启；必须重登陆来应用这个效果。

丑话说在前面，在重启 shell 前请先把有用的文档保存（或者关闭）。虽然这不是必要的，因为窗口和文档在重启了 shell 之后应该还在。

### 遗留名称

**注意:** 一些GNOME程序在文档和关于对话框的名称已更改，但可执行文件的名称却没有。这样的应用程序在下面表格列出.

**提示:** 在搜索栏中搜索的应用程序的遗留名称将成功返回现在的应用程序，例如搜索_nautilus_将返回_Files_.

<table class="wikitable">

<tbody>

<tr>

<th>Current</th>

<th>Legacy</th>

</tr>

<tr>

<td>[Files](/index.php/Files "Files")</td>

<td>Nautilus</td>

</tr>

<tr>

<td>[Web](/index.php/GNOME_Web "GNOME Web")</td>

<td>Epiphany</td>

</tr>

<tr>

<td>Videos</td>

<td>Totem</td>

</tr>

<tr>

<td>Main Menu</td>

<td>Alacarte</td>

</tr>

<tr>

<td>Document Viewer</td>

<td>Evince</td>

</tr>

<tr>

<td>Disk Usage Analyser</td>

<td>Baobab</td>

</tr>

<tr>

<td>Image Viewer</td>

<td>EoG (Eye of GNOME)</td>

</tr>

<tr>

<td>[Passwords and Keys](/index.php/GNOME_Keyring "GNOME Keyring")</td>

<td>Seahorse</td>

</tr>

</tbody>

</table>

## 配置

GNOME 3 是重新设计的，但是像大多数大型软件项目一样，他是很多不同时间的部分组装起来的。他没有一个 **无所不包** 的配置工具。新的 _系统设置_ 比以前的控制面板有很大的改进。 _系统设置_ 组织得很好，但是你可能想要更深层次地改变外观。

以前你所熟悉的配置工具现在有的好用，有的不好用了。有些设置选项隐藏着，不太容易找到。许多设置将会，或已经迁移到了新的工具上。你需要了解应当去哪里寻找适当的设置项，才能更好地配置 GNOME 外观。

GNOME 桌面环境依赖于一个存储配置的数据库后端（DConf）来存储 GNOME 与 GNOME 应用的设置。安装桌面环境时，GNOME 提供一套默认的配置，而各类应用程序向数据库中添加它们自己的配置。

对用户来说，最基础而直观的配置方式莫过于使用 GNOME 系统设置面板（gnome-control-center），以及 GNOME 应用程序各自的首选项（preferences）面板。如果您愿意，直接在 DConf 数据库中进行修改与配置总是可行的，尤其是在某些设置选项没有暴露在用户界面的情况下，直接修改可以更改某些隐藏选项。

GNOME 的这些配置通常是用户间相互独立的。以下文字仅供单用户配置所用，并没有提及更改全局配置模板的方法。

### GNOME 系统设置

系统设置工具包括了一些最基础的 GNOME 环境配置选项。

#### 色彩设置

`colord` 守护进程读取显示器的 [EDID](https://zh.wikipedia.org/wiki/EDID)信息，并提取出合适的色彩配置内容。大多数情况下，自动色彩配置都是正确的，不需要额外设置；但是对于可能出现的偏差情况，例如使用较旧的显示器时，您可以将色彩配置文件放在 `~/.local/share/icc/` 下，并在设置面板里启用。

#### 日期与时间

如果系统已有配置好的 [NTP 守护进程](https://wiki.archlinux.org/index.php/Network_Time_Protocol_daemon_(简体中文))，它同样会对 GNOME 桌面环境起作用。如果需要，您也可以手动控制进行同步。

如需在顶栏显示日期，请运行：

```
$ gsettings set org.gnome.desktop.interface clock-show-date true

```

另外，如需在 shell 的日历中显示周数，请运行：

```
$ gsettings set org.gnome.shell.calendar show-weekdate true

```

当然，以上配置均可以在 `gnome-tweak-tool` 里完成。

#### 默认应用程序

Upon installing GNOME for the first time, you may find that the wrong applications are handling certain protocols. For example, _totem_ opens videos instead of a previously used [VLC](/index.php/VLC "VLC"). Some of the associations can be set from system settings via: _System_ > _Details_ > _Default applications_.

For other protocols and methods see [Default applications](/index.php/Default_applications "Default applications") for configuration.

#### 鼠标和触摸板

为了帮助减少触摸板的干扰，你可能希望实现以下设置：

*   禁用触摸板，打字时
*   禁用滚动
*   禁用点击

#### 网络

[NetworkManager](/index.php/NetworkManager "NetworkManager") is the native tool of the GNOME project to control network settings from the shell. It is installed by default as a dependency for [tracker](https://www.archlinux.org/packages/?name=tracker) package, which is a part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group, and just needs to be [enabled](/index.php/NetworkManager#Enable_NetworkManager "NetworkManager").

While any other [network manager](/index.php/List_of_applications/Internet#Network_managers "List of applications/Internet") can be used as well, NetworkManager provides the full integration via the shell network settings and a status indicator applet [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) (not required for GNOME).

#### 在线帐户

Backends for the GNOME messaging application [empathy](https://www.archlinux.org/packages/?name=empathy) as well as the GNOME Online Accounts section of the System Settings panel are provided in a separate group: [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). See [#Unable to add accounts in Empathy and GNOME Online Accounts](#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts). Some online accounts, such as [ownCloud](/index.php/OwnCloud "OwnCloud"), require [gvfs-goa](https://www.archlinux.org/packages/?name=gvfs-goa) to be installed for full functionality in GNOME applications such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") and GNOME Documents [[2]](https://wiki.gnome.org/ThreePointSeven/Features/Owncloud).

#### 搜索

The GNOME shell has a search that can be quickly accessed by pressing the `Super` key and starting to type. The [tracker](https://www.archlinux.org/packages/?name=tracker) package is installed by default as a part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group and provides an indexing application and metadata database. It can be configured with the _Search and Indexing_ menu item; monitor status with _tracker-control_. It is started automatically by _gnome-session_ when the user logs in. Indexing can be started manually with `tracker-control -s`. Search settings can also be configured in the _System Settings_ panel.

The Tracker database can be queried using the _tracker-sparql_ command. View its manual page `man tracker-sparql` for more information.

### 高级设置

#### 外观

##### GTK+主题和图标主题

除了以下所述的直接从底层修改主题的方法，您也可以使用 gnome-tweak-tool 工具进行修改。 安装一个新的主题和图标集，分别添加相关的`~/.local/share/themes` 或者 `~/.local/share/icons` respectively (add to `/usr/share/` instead of `~/.local/share/` for the themes to be available systemwide.) 他们和其他GUI设置也可以在 `~/.config/gtk-3.0/settings.ini`中定义:

 `~/.config/gtk-3.0/settings.ini` 

```
[Settings]
gtk-theme-name = Adwaita
# next option is applicable only if selected theme supports it
gtk-application-prefer-dark-theme = true
# set font name and dimension
gtk-font-name = Sans 10

```

其他主题的站点:

*   [DeviantArt](http://www.deviantart.com/browse/all/customization/skins/linuxutil/desktopenv/gnome/gtk3/).
*   [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=167).
*   [GTK3 themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gtk3&do_Search=Go).
*   [Cursor themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=xcursor&do_Search=Go&PP=50&SB=v&SO=d).
*   [Icon themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=icon-theme&do_Search=Go&PP=50&SB=v&SO=d).

一旦安装，就可以使用 GNOME Tweak Tool或GSettings -参阅下面的GSettings命令：

对于GTK+主题：

```
$ gsettings set org.gnome.desktop.interface gtk-theme _theme-name_

```

对于图标主题

```
$ gsettings set org.gnome.desktop.interface icon-theme _theme-name_

```

###### 全局暗色主题

GNOME will use the Adwaita light theme by default however a dark variant of this theme (called the Global Dark Theme) also exists and can be selected using the Tweak Tool or by editing the GTK+ 3 settings file - see [GTK+#Dark theme variant](/index.php/GTK%2B#Dark_theme_variant "GTK+"). Some applications such as Image Viewer (_eog_) use the dark theme by default. It should be noted that the Global Dark Theme only works with GTK+ 3 applications; some GTK+ 3 applications may only have partial support for the Global Dark theme. Qt and GTK+ 2 support for the Global Dark Theme may be added in the future.

##### 窗口管理器主题

The window manager theme (the style of the window titlebars) can be set using the GNOME Tweak Tool or the following GSettings command:

```
$ gsettings set org.gnome.desktop.wm.preferences theme _theme-name_

```

###### 标题栏的高度

**注意:** 在GNOME 3.16中，Mutter不再使用metacity主题。相反，标题栏的装饰主题使用GTK+。

改变标题栏的高度，创建以下文件，调整填充所需：

 `~/.config/gtk-3.0/gtk.css` 

```
.header-bar.default-decoration {
    padding-top: 3px;
    padding-bottom: 3px;
}

.header-bar.default-decoration .button.titlebutton {
    padding-top: 2px;
    padding-bottom: 2px;
}

```

标题栏的高度也可以通过选择一个较小的字体。默认情况下，字体设置为Cantarell Bold 11。您可能希望将字体设置为较小的，例如Sans Bold 10\. 你可以这样使用以下GSettings命令来完成：

```
$ gsettings set org.gnome.desktop.wm.preferences titlebar-font 'Sans Bold 10'

```

###### 标题栏按钮重新排序

设置 GNOME 窗口管理器顺序 (Mutter, Metacity):

```
$ gsettings set org.gnome.desktop.wm.preferences button-layout ':minimize,maximize,close'

```

**提示:** 冒号表示窗口标题栏的按钮会出现在哪一方

###### 最大化时隐藏标题栏

*   [Install](/index.php/Install "Install") [mutter-hide-legacy-decorations](https://aur.archlinux.org/packages/mutter-hide-legacy-decorations/)<sup><small>AUR</small></sup>. It changes a default setting in the window manager, so as to automatically hide the titlebar on legacy (non-headerbar) apps when they are maximized or tiled to the side.

*   [Install](/index.php/Install "Install") [maximus](https://aur.archlinux.org/packages/maximus/)<sup><small>AUR</small></sup>. To start the application, execute _maximus_ from a terminal. When running, the daemon will automatically maximize windows. It will undecorate maximized windows and redecorate them when they are unmaximized. If you do not want all windows to start maximized, run `maximus -m` instead. Note that this will only work with windows decorated by the window manager; applications that use client-side decoration such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") will not be undecorated when maximized.

##### GNOME Shell主题

The theme of GNOME Shell itself is configurable. To use a Shell theme, firstly ensure that you have the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package installed. Then enable the _User Themes_ extension, either through GNOME Tweak Tool or through the [GNOME Shell Extensions](https://extensions.gnome.org) webpage. Shell themes can then be loaded and selected using the GNOME Tweak Tool.

There are a number of GNOME Shell themes available [in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-theme&do_Search=Go&PP=50&SB=v&SO=d).

Shell themes can also be downloaded from [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=191).

#### 桌面

各种桌面设置可以应用。

##### 桌面上的图标

参阅 [GNOME Files#Desktop Icons](/index.php/GNOME_Files#Desktop_Icons "GNOME Files").

##### 锁屏和背景

When setting the Desktop or Lock screen background, it is important to note that the Pictures tab will only display pictures located in `/home/_username_/Pictures` folder. If you wish to use a picture not located in this folder, use the commands indicated below.

对于桌面背景：

```
$ gsettings set org.gnome.desktop.background picture-uri 'file:///path/to/my/picture.jpg'

```

对于锁屏背景

```
$ gsettings set org.gnome.desktop.screensaver picture-uri 'file:///path/to/my/picture.jpg'

```

#### 扩展

**注意:** 通过 The GNOME Shell browser plugin（即 [extensions.gnome.org](https://extensions.gnome.org)）安装扩展的方法暂时无法在 Chrome/Chromium 35 或更高的版本上进行。用户应当采用其它对网页安装更兼容的浏览器进行安装，如 [Firefox (简体中文)](/index.php/Firefox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Firefox (简体中文)") 或 [GNOME/Web](/index.php/GNOME/Web "GNOME/Web")。

GNOME Shell 可以使用第三方扩展来定制。这些扩展提供了一些额外的功能，如：提供一个可以一直显示的 Dock、更换 Shell 的主题，等等。

名为 [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) 的软件包提供了一组由 The GNOME Project 维护，被当做 GNOME 计划的一部分的扩展，其中许多扩展被用在了 GNOME Classic 会话环境中。（最新版本的扩展你可以用他的代码 snapshot）[列表在这里](https://www.archlinux.org/packages/?sort=&q=gnome-shell-extension&maintainer=&last_update=&flagged=&limit=50)

```
 $ pacman -Ss gnome-shell-extension

```

另外，有许多扩展被收集并托管在了[extensions.gnome.org](https://extensions.gnome.org) 上。你可以在浏览器中浏览扩展列表，并轻松地一键点击来安装、管理、启用扩展。你可以在 [这里](https://extensions.gnome.org/about/)找到有关插件的更多信息。

你也可以在 [AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-extension&do_Search=Go)里面找到一些有用的扩展。当然，它们大多也可以在 [extensions.gnome.org](https://extensions.gnome.org) 找到。一些值得一提的是：

*   [gnome-shell-extension-lockkeys-git](https://aur.archlinux.org/packages/gnome-shell-extension-lockkeys-git/)<sup><small>AUR</small></sup> 一个指示 NumLock/CapsLock 激活情况的扩展。
*   [gnome-shell-extension-weather-git](https://aur.archlinux.org/packages/gnome-shell-extension-weather-git/)<sup><small>AUR</small></sup> 一个可以显示天气通知的扩展。
*   [gnome-shell-extension-nohotcorner-git](https://aur.archlinux.org/packages/gnome-shell-extension-nohotcorner-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnome-shell-extension-nohotcorner-git)]</sup> 一个禁用“Hot Corner”功能的拓展。
*   [gnome-shell-extension-insensitive-message-tray-git](https://aur.archlinux.org/packages/gnome-shell-extension-insensitive-message-tray-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnome-shell-extension-insensitive-message-tray-git)]</sup> 使鼠标在屏幕底部激活信息托盘的行为变迟钝的拓展。
*   [Alternative Status Menu](https://extensions.gnome.org/extension/5/alternative-status-menu/) 让你的用户菜单里显示休眠和关机的扩展。

另外，想要在屏幕底部显示一个任务栏，但又不想使用 GNOME Classic 的用户可以考虑使用 Window list 扩展 (由 [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) 提供).

在安装完一个扩展之后可能需要[重启 GNOME shell](#.E9.87.8D.E5.90.AF_GNOME_shell) 。故障排除信息参照[安装扩展导致GNOME停止工作](#.E5.AE.89.E8.A3.85.E6.89.A9.E5.B1.95.E5.AF.BC.E8.87.B4GNOME.E5.81.9C.E6.AD.A2.E5.B7.A5.E4.BD.9C)。

#### 输入法

GNOME集成了的通过[IBus](/index.php/IBus "IBus")的输入法, 只有[ibus](https://www.archlinux.org/packages/?name=ibus)和添加想要的输入法引擎 (例如:[ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) for Intelligent Pinyin) 需要安装，安装后，输入法引擎可以加入GNOME的区域和语言设置键盘布局。

#### 字体

**Tip:** If you set the _Scaling factor_ to a value above 1.00, the Accessibility menu will be automatically enabled.

Fonts can be set for Window titles, Interface (applications), Documents and Monospace. See the Fonts tab in the Tweak Tool for the relevant options.

For hinting, RGBA will likely be desired as this fits most monitors types, and if fonts appear too blocked reduce hinting to _Slight_ or _None_.

#### 启动应用程序

要启动登录某些应用程序, copy the relevant `.desktop` file from `/usr/share/applications/` to `~/.config/autostart/`. 可以使用Tweak Tool.来达到同样的效果。

**Tip:** If the plus sign button in the Tweak Tool's Startup Applications section is unresponsive, try start the Tweak Tool from the terminal using the following command: `gnome-tweak-tool`. See the following [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1413631#p1413631).

**Note:** The _gnome-session-properties_ dialog was removed as of GNOME 3.12\. It can be added back by [installing](/index.php/Install "Install") the [gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/)<sup><small>AUR</small></sup> package.

#### 电源

The basic power settings that may want to be altered (these example settings assume the user is using a laptop - change them as desired):

```
$ gsettings set org.gnome.settings-daemon.plugins.power button-power _hibernate_
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-timeout _3600_
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type _hibernate_
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-timeout _1800_
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-type _hibernate_
$ gsettings set org.gnome.desktop.lockdown disable-lock-screen _true_

```

To keep a monitor active on lid close:

```
$ gsettings set org.gnome.settings-daemon.plugins.xrandr default-monitors-setup do-nothing

```

##### Hibernate the computer when lid is closed

This setting cannot be done directly in GNOME. First make sure that [hibernation](/index.php/Hibernation "Hibernation") is correctly set up. Then, configure _systemd_ with `HandleLidSwitch=hibernate` as described in [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management").

##### Prevent Suspend-To-RAM (S3) when closing the lid

This setting cannot be done directly in GNOME, so you have to configure _systemd_ with `HandleLidSwitch=ignore` as described in [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management").

##### Change critical battery level action

The System Settings panel only allows the user to choose between _Suspend_ or _Hibernate_. To choose another option such as _Do Nothing_ open the `dconf-editor` and navigate to `org.gnome.settings-daemon.plugins.power`. Edit the `"critical-battery-action"` value to `"nothing"`.

#### Sort applications into application (app) folders

**Tip:** The [gnome-catgen](https://github.com/prurigro/gnome-catgen) ([gnome-catgen-git](https://aur.archlinux.org/packages/gnome-catgen-git/)<sup><small>AUR</small></sup>) script allows you to manage folders through the creation of files in `~/.local/share/applications-categories` named after each category and containing a list of the desktop files belonging to apps you'd like to have inside. Optionally, you can have it cycle through each app without a folder and input the desired category until you ctrl-c or run out of apps.

In the **dconf-editor** navigate to `org.gnome.desktop.app-folders` and set the value of `folder-children` to an array of comma separated folder names:

```
['Utilities', 'Sundry']

```

Add applications using `gsettings`:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ apps "['alacarte.desktop', 'dconf-editor.desktop']"

```

This adds the applications `alacarte.desktop` and `dconf-editor.desktop` to the Sundry folder. This will also create the folder `org.gnome.desktop.app-folders.folders.Sundry`.

To name the folder (if it has no name that appears at the top of the applications):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ name "Sundry"

```

Applications can also be sorted by their category (specified in their _.desktop_ file):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ categories "['Office']"

```

If certain applications matching a category are not wanted in a certain folder, exclusions can be set:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ excluded-apps "['libreoffice-draw.desktop']"

```

For further information, refer to the [app-folders schema](https://git.gnome.org/browse/gsettings-desktop-schemas/tree/schemas/org.gnome.desktop.app-folders.gschema.xml.in.in).

## 提示与技巧

其他GNOME系统设置和提示。

### 键盘

#### 登陆打开NumLock键

运行以下命令：

```
$ gsettings set org.gnome.settings-daemon.peripherals.keyboard numlock-state on

```

#### 热键选择

很多的快捷键可以通过系统设置菜单中更改. 例如，重新启用“显示桌面快捷键：

_System settings_ > _Keyboard_ > _Shortcuts_ > _Navigation_ > _Hide all normal windows_

However, certain hotkeys cannot be changed directly via system settings. In order to change these keys, use _dconf-editor_. An example of particular note is the hotkey `Alt-` + ``` (the key above `Tab` on US keyboard layouts). In GNOME Shell it is pre-configured to cycle through windows of an application, however it is also a hotkey often used in the [Emacs](/index.php/Emacs "Emacs") editor. It can be changed by opening _dconf-editor_ and modifying the _switch-group_ key found in `org.gnome.desktop.wm.keybindings`.

It is possible to manually change the keys via an application's so-called **accel** map file. Where it is to be found is up to the application: For instance, Thunar's is at `~/.config/Thunar/accels.scm`, whereas Files's is located at `~/.config/nautilus/accels` and `~/.gnome2/accels/nautilus` on old release.

The file should contain a list of possible hotkeys, each unchanged line commented out with a leading ";" that has to be removed for a change to become active. For example to replace the hotkey used by Files to move files to the trash folder, change the line:

```
; (gtk_accel_path "<Actions>/DirViewActions/Trash" "<Primary>Delete")

```

to this:

```
(gtk_accel_path "<Actions>/DirViewActions/Trash" "Delete")

```

The file is regenerated regularly so do not comment the file. The uncommented line will stay but every comment you add will be lost.

#### 打开键盘开关命令

To have keyboard shortcut **Alt** + **Shift** switch keyboards:

Open Gnome-Tweak-Tool (or Keyboard Settings, in GNOME 3.16) and set _Typing_ > _Modifiers-only input sources_ > _select Alt-shift_. For more information see also the forum [thread](https://bbs.archlinux.org/viewtopic.php?id=152127).

#### XkbOptions键盘选项

Using the **dconf-editor**, navigate to the key named `org.gnome.desktop.input-sources.xkb-options` and add desired XkbOptions (e.g. _caps:swapescape_) to the list.

See `/usr/share/X11/xkb/rules/xorg` for all XkbOptions and `/usr/share/X11/xkb/symbols/*` for the respective descriptions.

**Note:** To enable the `Ctrl+Alt+Backspace` combination to terminate Xorg, use the [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool). Within the **Tweak Tool**, navigate to _Typing > Key sequence to kill the X server_ and select the option `Ctrl+Alt+Backspace` from the dropdown menu.

#### De-bind Windows key

默认情况下，“Windows键”将打开GNOMEshelly预览模式。 You can unbind this key by running the command below

```
$ gsettings set org.gnome.mutter overlay-key 'Foo'

```

### 磁盘

GNOME提供磁盘实用程序来操作的存储驱动器设置。这是它的一些特点：

*   **Enable write cache** is a feature that most hard drives provide. Data is cached and allocated at chosen times to improve system performance. Not recommended unless the computer has a backup battery pack or is a laptop as data would be lost on power failure.

_Settings_ > _Drive Settings_ > _Write Cache_ > **On**

*   **Automatic Mount Options** can mount drives and partitions that are GPT based - will use default, recommended options.

**Warning:** This setting erases related [fstab](/index.php/Fstab "Fstab") entries

_Partition Settings_ > _Edit Mount Options_ > _Automatic Mount Options_ > **On**

### 从菜单隐藏的应用程序

**Tip:** Desktop entries can be hidden by editing the `.desktop` files themselves. See [Desktop entries#Hide desktop entries](/index.php/Desktop_entries#Hide_desktop_entries "Desktop entries").

Use the _Main Menu_ application (provided by the [alacarte](https://www.archlinux.org/packages/?name=alacarte) package) to hide any applications you do not wish to show in the menu.

### 截屏记录

GNOME features built-in screencast recording with the **Ctrl** + **Shift** + **Alt** + **R** key combination. A red circle is displayed in the bottom right corner of the screen when the recording is in progress. After the recording is finished, a file named `Screencast from %d%u-%c.webm` is saved in the Videos directory. In order to use the screencast feature the gst plugins need to be installed.

### 截图

默认保存目录:

```
$ gsettings set org.gnome.gnome-screenshot auto-save-directory file:///home/_USER_/Desktop

```

Check the _gnome-screenshot_ manual page for more options.

### 注销延迟

去掉注销的确认和 60 秒的延迟： 这个对话框一般出现在你用状态菜单注销的时候。这个修改对于 关机 也生效。这个不是全局修改，只对使用该命令的用户生效。使用该命令立即生效。

```
$ gsettings set org.gnome.SessionManager logout-prompt false

```

### 禁用动画

To disable Shell animations (such as "Show Applications" and the wave animation in the top left activities hot corner), run:

```
$ gsettings set org.gnome.desktop.interface enable-animations false

```

### Retina (HiDPI) display support

GNOME introduced HiDPI support in version 3.10\. If your display does not provide the correct screen size through EDID, this can lead to incorrectly scaled UI elements. As a workaround you can open _dconf-editor_ and find the key `scaling-factor` in `org.gnome.desktop.interface`. Set it to `1` to get the standard scale.

Also see [HiDPI](/index.php/HiDPI "HiDPI").

### 密码和密钥 (PGP Keys)

You can use the Passwords and Keys program (_seahorse_) to create a PGP key as it is a front end for [GnuPG](/index.php/GnuPG "GnuPG") and installs it as dependency. This may be useful in the future (for instance if to encrypt a file). Create a key as shown below (the process may take about 10 minutes):

_File_ > _New_ > _PGP Key_ > _Name_ > _Email_ > _Defaults_ > _Passphrase_.

### 终端

#### 更改默认的终端大小

The default size of a new terminal can be adjusted in the menu _Edit > Profile preferences_ .

#### 新终端采用当前目录

By default new terminals open in the `$HOME` directory. To have new terminals adopt the current working directory: `source /etc/profile.d/vte.sh`. Add the command to the shell configuration to retain the behaviour.

#### Pad the terminal

To pad the terminal (create a small, invisible border between the window edges and the terminal contents) create the file below:

 `~/.config/gtk-3.0/gtk.css` 

```
VteTerminal,
TerminalScreen {
    padding: 10px 10px 10px 10px;
    -VteTerminal-inner-border: 10px 10px 10px 10px;
}
```

#### 禁用光标闪烁

Since GNOME 3.8 and the migration to GSettings and DConf the key required to modify in order to disable the blinking cursor in the Terminal differs slightly in contrast to the old GConf key. To disable the blinking cursor in GNOME 3.8 and above use:

```
$ gsettings set org.gnome.desktop.interface cursor-blink false

```

To disable the blinking cursor in Terminal only use (make sure profile uid is correct one):

```
$ dconf write /org/gnome/terminal/legacy/profiles:/:b1dcc9dd-5262-4d8d-a863-c897e6d979b9/cursor-blink-mode "'off'"

```

Note that `gnome-settings-daemon`, from the package of the same name, must be running for this and other settings changes to take effect in GNOME applications - see [GNOME#Configuration](/index.php/GNOME#Configuration "GNOME").

#### 关闭终端时，禁用确认窗口

试图关闭该窗口，而一个以root身份登录时，终端将始终显示一个确认窗口。为了避免这种情况，执行以下命令：

```
$ gsettings set org.gnome.Terminal.Legacy.Settings confirm-close false

```

### 鼠标中键

By default, GNOME 3 disables middle mouse button emulation regardless of [Xorg](/index.php/Xorg "Xorg") settings (**Emulate3Buttons**). To enable middle mouse button emulation use:

```
$ gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true

```

### 启用按钮和菜单图标

Since GTK+ 3.10, the GSettings key 'menus-have-icons' has been deprecated. Icons in buttons and menus can still be enabled by setting the following overrides:

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

### 使用自定义的色彩和渐变色的桌面背景

使用自定义颜色和渐变为您的桌面背景，您首先需要设置一个透明的图片或其他不存在的图片作为您的桌面背景。例如，下面的命令将设置一个不存在的图片为背景。

```
$ gsettings set org.gnome.desktop.background picture-uri none

```

在这一点上，桌面背景应该是一个平坦的颜色-默认的颜色设置为深蓝色。

对于不同的平面彩色你只需要改变的主要颜色设置：

```
$ gsettings set org.gnome.desktop.background primary-color <my color>

```

where <my color> is a hex value (such as _ffffff_ for white).

对于颜色渐变，你也需要改变次要颜色设置 `org.gnome.desktop.background secondary-color` 并选择一个阴影类型。举例来说，如果你想有一个horizontal gradient，执行以下命令：

```
$ gsettings set org.gnome.desktop.background color-shading-type horizontal

```

如果你是使用一个透明的图片作为你的背景，你可以通过执行以下设置的透明度：

```
$ gsettings set org.gnome.desktop.background picture-opacity <value>

```

数值在100和1之间（最大不透明度为100）。

### gnome terminal透明

可以在~/.bashrc里添加一段代码实现

```
~/.bashrc
if [ -n "$WINDOWID" ]; then
    TRANSPARENCY_HEX=$(printf 0x%x $((0xffffffff * 80 / 100)))
    xprop -id "$WINDOWID" -f _NET_WM_WINDOW_OPACITY 32c -set _NET_WM_WINDOW_OPACITY "$TRANSPARENCY_HEX"
fi

```

```

 **Template error:** are you trying to use the = sign? Visit [Help:Template#Escape template-breaking characters](/index.php/Help:Template#Escape_template-breaking_characters "Help:Template") for workarounds.

```

**Tip:** 80为透明度。

### 渐变背景

GNOME 可以在特定的时间间隔之间的使用不同的壁纸。 这是通过创建一个XML文件，指定要使用的图片和时间间隔完成的。有关创建这些文件的详细信息，请参阅下面的 [article](http://www.linuxjournal.com/content/create-custom-transitioning-background-your-gnome-228-desktop).

可替代地，一些工具可用自动化过程：

*   **mkwlppr** — This script creates XML files that can act as dynamic wallpapers for GNOME by referring to multiple wallpapers.

[http://pastebin.com/019G2rCy](http://pastebin.com/019G2rCy) || see [mkwlppr](http://pastebin.com/019G2rCy)

*   **[Wallpapoz](/index.php/Wallpapoz "Wallpapoz")** — Wallpapoz is a tool that provides dynamic wallpapers for GNOME and Xfce desktops.

[https://vajrasky.wordpress.com/](https://vajrasky.wordpress.com/) || [wallpapoz](https://aur.archlinux.org/packages/wallpapoz/)<sup><small>AUR</small></sup>

*   **CreBS** — A Python/GTK application used to create and set desktop wallpaper slideshows for GNOME.

[http://www.obfuscatepenguin.net/](http://www.obfuscatepenguin.net/) || [crebs](https://aur.archlinux.org/packages/crebs/)<sup><small>AUR</small></sup>

对于设置XML文件作为默认的背景，参阅 [#Lock screen and background](#Lock_screen_and_background).

### GNOME Files

GNOME Files，即 nautilus，为 GNOME 默认的文件管理器。

#### 移除侧边栏计算机中的文件夹

显示的文件夹在 `~/.config/user-dirs.dirs` 里配置，他可以被任何编辑器直接修改。运行 `xdg-user-dirs-update` 来应用修改。但是建议设置文件权限为只读。

#### 地址栏显示文本路径

标准的 Files 工具栏用按钮来显示路径。想要从**键盘**输入，你需要使它显示文本路径。按 `Ctrl` + `L` 就可以完成。

假如你想让它始终显示为文本路径，用 gsettings 如下所示。

```
$ gsettings set org.gnome.nautilus.preferences always-use-location-entry true

```

**注意:** 这样修改之后，你不能回到按钮路径。只有在设置为 **false** 的情况下，可以通过快捷键来使两种模式都可用。

### GNOME 面板

#### 在时间栏显示日期

默认 GNOME 在顶栏只显示星期和时间。可以通过下面的命令修改，修改立即生效。

```
# gsettings set org.gnome.shell.clock show-date true

```

#### 隐藏顶部面板的图标

在登录 GNOME 时，顶部面板可能会出现一些不需要的图标。通过编辑 GNOME 面板脚本来移除这些图标。

例如，要想移除 **universal access icon**。从 AREA_ORDER 行中移除 'a11y'，并注释掉 AREA_SHELL_IMPLEMENTATION 行中的 'a11y'。

修改

 `/usr/share/gnome-shell/js/ui/panel.js` 

```
const STANDARD_STATUS_AREA_ORDER = ['ally', 'keyboard', 'volume', 'network', 'bluetooth', 'battery', 'userMenu'];
const STANDARD_STATUS_AREA_SHELL_IMPLEMENTATION = {
    'a11y': imports.ui.status.accessibility.ATIndicator
    'volume': imports.ui.status.volume.Indicator,
    'battery': imports.ui.status.power.Indicator,
    'keyboard': imports.ui.status.keyboard.XKBIndicator,
    'userMenu': imports.ui.userMenu.UserMenuButton
};

```

为

 `/usr/share/gnome-shell/js/ui/panel.js` 

```
const STANDARD_STATUS_AREA_ORDER = ['keyboard', 'volume', 'network', 'bluetooth' 'battery', 'userMenu'];
const STANDARD_STATUS_AREA_SHELL_IMPLEMENTATION = {
    //'a11y': imports.ui.status.accessibility.ATIndicator
    'volume': imports.ui.status.volume.Indicator,
    'battery': imports.ui.status.power.Indicator,
    'keyboard': imports.ui.status.keyboard.XKBIndicator,
    'userMenu': imports.ui.userMenu.UserMenuButton
};

```

保存并重启 gnome-shell 查看结果。

1.  `Alt+F2`
2.  `r`
3.  `Enter`

#### 去掉注销时的延迟

按照下面的方法修改来去掉注销的确认和 60 秒的延迟。

这个对话框一般出现在你用状态菜单注销的时候。这个修改对于 _**关机**_ 也生效。这个不是全局修改，只对使用该命令的用户生效。使用该命令立即生效。

```
$ gsettings set org.gnome.SessionManager logout-prompt 'false'

```

### 活动视图

#### 从应用程序视图移除应用程序项目

GNOME 用 .desktop 文件来填充应用程序视图。这些纯文本文件位于**`/usr/share/applications`**。 GNOME Files 不把他们识别为纯文本文件，你不能直接在文件夹视图中编辑他们。使用终端显示或编辑它们

```
# ls /usr/share/applications
# nano /usr/share/applications/foo.desktop

```

要想系统全局修改，直接编辑**`/usr/share/applications`**中的文件。要想只对自己生效，把 _foo.desktop_ 复制到home文件夹：

```
$ cp /usr/share/applications/foo.desktop ~/.local/share/applications/

```

你可以按照你的想法编辑 .desktop 文件。

**注意:** 删除一个 .desktop 文件并不卸载软件，只是删除他的桌面特性（如文件关联，快捷键等）。

添加下列选项到 .desktop 文件来使 foo 不再显示在应用程序视图：

```
$ echo "NoDisplay=true" >> foo.desktop

```

#### 怎样改变应用程序图标大小

对于很多人来说，一个很怪异的事情就是 GNOME 3 的图标大小。当遇到一个小屏幕加很多程序的时候很痛苦。 很高兴这里有一个方法能改变这中情况，修改 GNOME shell 主题。

直接修改系统文件夹(别忘了备份)或者复制到你的用户文件夹。对于默认主题，修改**`/usr/share/gnome-shell/theme/gnome-shell.css`**

对于用户主题，修改**`/usr/share/themes/<UserTheme>/gnome-shell/gnome-shell.css`**

修改 _gnome-shell.css_ ，用下面的值替换。然后[#重启 GNOME shell](#.E9.87.8D.E5.90.AF_GNOME_shell)

 `gnome-shell.css` 

```
 .icon-grid {
     spacing: 18px;
     -shell-grid-item-size: 82px;
 }

 .icon-grid .overview-icon {
     icon-size: 48px;
 }

```

默认主题的小图标版在[AUR](https://aur.archlinux.org/packages.php?ID=51586)上提供。

#### 禁止鼠标接触 hot corner（左上角）切换活动视图

要禁用这一功能，编辑**`/usr/share/gnome-shell/js/ui/layout.js`**（Gnome 3.0.x中是_panel.js_）文件的这一段：

 `layout.js` 

```
 this._corner = new Clutter.Rectangle({ name: 'hot-corner',
                                       width: 1,
                                       height: 1,
                                       opacity: 0,
                                       reactive: true });icon-size: 48px;
 }

```

把_reactive_的值_true_修改为_false_，[#重启 GNOME shell](#.E9.87.8D.E5.90.AF_GNOME_shell)即可。

### 标题栏

#### 减少标题栏高度

```
# sed -i '/title_vertical_pad/s|value="[0-9]\{1,2\}"|value="0"|g' /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml

```

[重启 GNOME shell](#.E9.87.8D.E5.90.AF_GNOME_shell)，这会修改垂直间距从14到0，给你更时尚的外观。

想要恢复默认值，从[官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库")中[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [gnome-themes-standard](https://www.archlinux.org/packages/?name=gnome-themes-standard)

### 登录屏幕

#### 登录管理器壁纸

在会话变量被如上设置之后，你就可以发出命令检索或者设置 GDM 项目。

最简单的方法是使用配置编辑器图形界面：

```
$ dconf-editor

```

设置的位置和下面的命令行一样。

下面是用命令行检索和设置 GDM 壁纸。

```
$  GSETTINGS_BACKEND=dconf gsettings get org.gnome.desktop.background picture-uri
 $  GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.background picture-uri 'file:///usr/share/backgrounds/gnome/SundownDunes.jpg'

 $  GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.background picture-options 'zoom'
 ## Possible values: centered, none, scaled, spanned, stretched, wallpaper, zoom
```

**注意:** 你必须指定一个 "gdm" 有读权限的文件，GDM不能读你的home文件夹。

另外还有一种可以在图形界面改变主题 (gtk3, 图标和鼠标)、壁纸和其他细小的设置 GDM 登陆屏幕的方法，你可以从 AUR 安装 [gdm3setup](https://aur.archlinux.org/packages/gdm3setup/)<sup><small>AUR</small></sup>.

#### 登录界面大字体

这个修改用 scaling factor 放大你的登陆界面字体。就像在桌面上你使用辅助功能一样。

在做这个修改之前，你必须 [export GDM会话变量](#.E7.99.BB.E5.BD.95.E7.AE.A1.E7.90.86.E5.99.A8)。

```
$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.interface text-scaling-factor '1.25'

```

#### 关闭声音

这个调整让你在登录界面通过快捷键禁用声音反馈。你必须首先 [export GDM会话变量](#.E7.99.BB.E5.BD.95.E7.AE.A1.E7.90.86.E5.99.A8)。

```
$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.sound event-sounds 'false'

```

如果上面的调整不工作或者你无法 export GDM 会话变量，有一个比真正解决更容易的解决方法：在登陆时用键盘多媒体键静音或者降低音量。

#### 按电源键启用交互界面

默认安装设置电源键功能是休眠。_**关机**_或_**显示会话**_或许会更好一点。你必须首先 [export GDM会话变量](#.E7.99.BB.E5.BD.95.E7.AE.A1.E7.90.86.E5.99.A8)。

```
 $ GSETTINGS_BACKEND=dconf gsettings set org.gnome.settings-daemon.plugins.power button-power 'interactive'
 $ GSETTINGS_BACKEND=dconf gsettings set org.gnome.settings-daemon.plugins.power button-hibernate 'interactive'
 $ gsettings list-recursively org.gnome.settings-daemon.plugins.power

```

#### 改变 GDM 的键盘布局

由于 GDM 无视您的 GNOME 3 键盘设置，您得在 Xorg 配置文件中设置您的键盘布局。参阅此处： [Beginner's Guide.](/index.php/Beginners%27_guide#Non-US_keyboard "Beginners' guide")

#### gnome terminal透明

可以在~/.bashrc里添加一段代码实现

```
~/.bashrc
if [ -n "$WINDOWID" ]; then
    TRANSPARENCY_HEX=$(printf 0x%x $((0xffffffff * 80 / 100)))
    xprop -id "$WINDOWID" -f _NET_WM_WINDOW_OPACITY 32c -set _NET_WM_WINDOW_OPACITY "$TRANSPARENCY_HEX"
fi

```

```

 **Template error:** are you trying to use the = sign? Visit [Help:Template#Escape template-breaking characters](/index.php/Help:Template#Escape_template-breaking_characters "Help:Template") for workarounds.

```

**Tip:** 80为透明度。

#### 启用备用模式

如果 gnome-shell 不存在或您的显卡不支持混成特效的话，您的会话将自动以备用模式启动。

如果您想在安装了 gnome-shell 的情况下启用备用模式 (Fallback Mode) 的话，打开**系统设置**。打开**系统信息**>**图形**。把**强制使用备用模式**调为`开启`。

你也可以选择用_gsettings_命令来选择会话类型。

```
$ gsettings set org.gnome.desktop.session session-name 'gnome-fallback'

```

重新登录应用设置。禁用备用模式，用'gnome' 代替 'gnome-fallback'。

### 其他技巧

参见：[GNOME Tips (简体中文)](/index.php/GNOME_Tips_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GNOME Tips (简体中文)")。

## 故障排除

### Shell freezes

In the event of a Shell freeze (which might be caused by certain appearance tweaks, malfunctioning extensions or perhaps a lack of available memory) restarting the Shell by pressing `Alt` + `F2` and then entering **r** may not be possible.

In this case, try switching to another TTY (**Ctrl** + **Alt** + **F2**) and entering the following command: `pkill -HUP gnome-shell`. It may take a few seconds before the Shell successfully restarts. Restarting the shell in this fashion should not log the user out but it is a good idea to try and ensure that all work is saved anyway.

If this fails, the [Xorg](/index.php/Xorg "Xorg") server will need to be restarted either by: `pkill X` for console logins or: `systemctl restart gdm` for GDM logins. Bear in mind that restarting the Xorg server will log the user out so try to ensure that all work is saved before attempting this.

### Incorrect application defaults

When installing applications for the first time you may find that GNOME has the wrong application associated to a certain protocols - for instance, _easytag_ becomes the folder handler instead of [GNOME Files](/index.php/GNOME_Files "GNOME Files").

For GNOME Files see the following page: [GNOME Files#Files is no longer the default file manager](/index.php/GNOME_Files#Files_is_no_longer_the_default_file_manager "GNOME Files").

For Document Viewer, run the following command:

```
$ xdg-mime default evince.desktop application/pdf

```

For other applications, default handler settings are detailed on the following page: [Default applications](/index.php/Default_applications "Default applications").

Optionally, you can [install](/index.php/Install "Install") [gnome-defaults-list](https://aur.archlinux.org/packages/gnome-defaults-list/)<sup><small>AUR</small></sup>. It will place your configuration file at `/etc/gnome/defaults.list`.

### Tracker & Documents do not list any local files

In order for Tracker (and, therefore, Documents) to detect your local files, they must be stored in an [XDG compliant directory](http://standards.freedesktop.org/basedir-spec/basedir-spec-latest.html) (such as 'Documents' or 'Music'). For more information, see [Xdg user directories](/index.php/Xdg_user_directories "Xdg user directories").

You can also configure Tracker to recursively search inside specific directories such as your home directory. These settings can be made using `tracker-preferences`.

### Unable to add accounts in Empathy and GNOME Online Accounts

Empathy, the engine behind integrated messaging, GNOME Online Accounts, and all other system settings based on messaging accounts will not function correctly unless the [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) group of packages or at least one of the backends ([telepathy-gabble](https://www.archlinux.org/packages/?name=telepathy-gabble), or [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), for example) is [installed](/index.php/Install "Install"). View descriptions of _telepathy_ components on the [freedesktop.org telepathy wiki](http://telepathy.freedesktop.org/wiki/Components).

**Note:** [Avahi](/index.php/Avahi "Avahi") daemon is required for connecting with the People Nearby account, and also in order for some desktop extensions to work correctly like [Chat Status](https://extensions.gnome.org/extension/746/chat-status/)

### Cannot change settings in dconf-editor

When one cannot set settings in [dconf](https://www.archlinux.org/packages/?name=dconf), it is possible their dconf user settings are corrupt. In this case it is best to delete the user dconf files in `~/.config/dconf/user*` and set the settings in dconf-editor after.

### When an extension breaks the shell

When enabling shell extensions causes GNOME breakage, you should first remove the _user-theme_ and _auto-move-windows_ extensions from their installation directory.

The installation directory could be one of `~/.local/share/gnome‑shell/extensions`, `/usr/share/gnome‑shell/extensions` or `/usr/local/share/gnome‑shell/extensions`. Removing these two extension-containing folders may fix the breakage. Otherwise, isolate the problem extension with trial‑and‑error.

Removing or adding an extension-containing folder to the aforementioned directories removes or adds the corresponding extension to your system. Details on GNOME Shell extensions are available at the [GNOME web site.](https://live.gnome.org/GnomeShell/Extensions)

If you have trouble with uninstalling an extension via [extensions.gnome.org/local](https://extensions.gnome.org/local/), then probably they have been installed as system-wide extensions with the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package. Removing the package again obviously affects all user accounts.

### 扩展在 GNOME 3 升级后不工作了

**Note:** Please bear in mind that whilst the methods below will allow you to **try** and activate an extension with an unsupported version of GNOME Shell, it is by no means a guarantee that the extension will work successfully. The most likely outcome of trying to activate such an extension is that GNOME Shell will crash and then restart.

Before trying the workarounds below, check if an update is available for the extension by visiting [extensions.gnome.org/local](https://extensions.gnome.org/local).

If there is no update for your current GNOME version yet, use the following command to disable version validation for extensions:

```
$ gsettings set org.gnome.shell disable-extension-version-validation true

```

Alternatively, you could modify the extension itself, changing the supported shell version to satisfy the version validation. See the method below.

找到扩展的安装目录，可能是 `~/.local/share/gnome-shell/extensions` 或 `/usr/share/gnome-shell/extensions`.

编辑扩展子文件夹中的每一个 **`metadata.json`**

<table border="0">

<tbody>

<tr>

<td>Insert:</td>

<td>`"shell-version": ["3.x"]`</td>

</tr>

<tr>

<td>Instead of (for example):</td>

<td>`"shell-version": ["3.4"]`</td>

</tr>

</tbody>

</table>

`"3.x"` 是最好的选择，这个表示扩展能在所有 _**3.x**_ GNOME Shell版本下工作。

### 只有 conky 运行时键盘快捷方式不工作

gnome-shell 键盘快捷方式(如 Alt+F2,Alt+F1 和多媒体键快捷方式)当只有 conky 运行时不会工作。然而如果另一个程序(例如 gedit)在运行，键盘快捷方式就可以工作了。

解决方式：编辑 .conkyrc

```
own_window yes
own_window_transparent yes
own_window_argb_visual yes
own_window_type dock
own_window_class Conky
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

### Unable to apply stored configuration for monitors

If you encounter this message try to disable the _xrandr_ `gnome-settings-daemon plugin`:

```
$ dconf write /org/gnome/settings-daemon/plugins/xrandr/active false

```

### 一致的光标主题

See [Cursor themes#Desktop environments](/index.php/Cursor_themes#Desktop_environments "Cursor themes").

### Windows cannot be modified with Alt-Key + mouse-button

In GNOME 3.6 and above, the mouse button modifier (the key that allows you to drag a window from a location other than the titlebar) is the `Super` key instead of the `Alt` key which was used in the past. The change was made in response to the following [bug report](https://bugzilla.gnome.org/show_bug.cgi?id=607797).

To change the mouse button modifier back to the `Alt` key, execute the following:

```
$ gsettings set org.gnome.desktop.wm.preferences mouse-button-modifier '<Alt>'  

```

**Note:** It is not possible to change this with _System settings_ > _Keyboard_ > _Shortcuts_

### 加载速度慢的系统图标/慢GDM登录

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** As per [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1565891#p1565891), it's probably the fact that on [gdk-pixbuf2](https://www.archlinux.org/packages/?name=gdk-pixbuf2) post install `gdk-pixbuf-query-loaders --update-cache` is run which fixes the issue, not the re-installation of the package per se. (Discuss in [Talk:GNOME (简体中文)#](https://wiki.archlinux.org/index.php/Talk:GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)))

Problems with the loading of system icons, such the ones in the title bar of Files, might be solved by [installing](/index.php/Pacman#Installing_specific_packages "Pacman") (or re-installing) the [gdk-pixbuf2](https://www.archlinux.org/packages/?name=gdk-pixbuf2) package.

Re-installing the aforementioned package may also fix repeated occurrences of the "Oh no! Something has gone wrong!" error screen and/or very slow loading and login with GDM as described in the following [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1414157).

### Artifacts when maximizing windows

Maximizing windows may cause artifacts as of GNOME 3.12.0 - see the following [forum thread](https://bbs.archlinux.org/viewtopic.php?id=183617) and [bug report](https://bugzilla.gnome.org/show_bug.cgi?id=728385). A solution is detailed in the following section: [#Tear-free video with Intel HD Graphics](#Tear-free_video_with_Intel_HD_Graphics).

### Tear-free video with Intel HD Graphics

Intel TearFree

Enabling the [Xorg Intel TearFree option](/index.php/Intel_Graphics#Tear-free_video "Intel Graphics") is a known workaround for tearing problems on Intel adapters. However, the way this option acts makes it redundant with the use of a compositor (it increases memory consumption and lowers performance, see [the original bug report's final comment](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c123)).

DRI3

According to [this bug report](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c2), DRI3 includes the `buffer_age` extension that allows GNOME Shell's Mutter compositor to sync windows to vblank in an efficient way. DRI3 support is not compiled in to the mesa package, so you have to recompile [mesa](https://www.archlinux.org/packages/?name=mesa) with `--enable-dri3` in the `./configure` flags (see [ABS](/index.php/ABS "ABS")). Then enable it in the Xorg driver:

 `/etc/X11/xorg.conf.d/20-intel.conf` 

```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "DRI"    "3"
EndSection
```

Mutter tweaks

**Note:** This workaround has been [reported](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c0) to have side effects and may not fix tearing in all cases.

GNOME Shell's Mutter compositor has a tweak known to address tearing problems (see [the original suggestion for this fix](https://bugzilla.gnome.org/show_bug.cgi?id=657071#c1) and its mention in [the Freedesktop bug report](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c59)). To enable this tweak, append the following line to `/etc/environment`: `CLUTTER_PAINT=disable-clipped-redraws:disable-culling`. Then restart the Xorg server.

### Window opens behind other windows when using multiple monitors

This is possibly a bug in GNOME Shell which causes new windows to open behind others. To fix this issue, one can run the following command:

```
$ gsettings set org.gnome.shell.overrides workspaces-only-on-primary false

```

### 锁定按钮无法重新启用触摸板

Some laptops have a touchpad lock button that disables the touchpad so that users can type without worrying about touching the touchpad. Currently, it appears that although GNOME can lock the touchpad by pressing this button, it cannot unlock it. If the touchpad gets locked you can run the following to unlock it:

```
$ xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 1

```

### 密码不记得

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:GNOME (简体中文)#](https://wiki.archlinux.org/index.php/Talk:GNOME_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)))

如果每次登录时都会有一个密码提示，你发现密码不保存，你可能需要创建/设置默认密钥环。

Ensure that the [seahorse](https://www.archlinux.org/packages/?name=seahorse) package is installed, open it ("Passwords and Keys" in system settings) and select _View_ > _By Keyring_ If there is no keyring in the left column (it will be marked with a lock icon), go to _File_ > _New_ > _Password Keyring_ and give it a name. You will be asked to enter a password. If you do not give the keyring a password it will be unlocked automatically, even when using autologin, but passwords will not be stored securely. Finally, right-click on the keyring you just created and select "Set as default".

### GNOME Shell键盘源菜单不可见

A menu showing the keyboard input sources (for example 'en' for an English keyboard layout) should be visible next to the status area containing icons for network, volume and power sources. If the keyboard sources menu is not visible, this is probably because you have configured your [Xorg](/index.php/Xorg "Xorg") keyboard layout in a way which GNOME does not recognise.

To ensure that the menu is visible, remove any Xorg keyboard configuration you might have created and set the keyboard locale using [localectl](/index.php/Keyboard_configuration_in_Xorg#Using_localectl "Keyboard configuration in Xorg").

Upon running the command and then logging out, you should find that the keyboard input sources menu is visible in GDM and in the GNOME Shell desktop. See [Input sources in GNOME](http://blogs.gnome.org/mclasen/2012/09/21/input-sources-in-gnome/) for more information.

### 鼠标指针丢失

When using a separate [window manager](/index.php/Window_manager "Window manager") with _gnome-settings-daemon_, the mouse cursor may vanish. Run:

```
$ gsettings set org.gnome.settings-daemon.plugins.cursor active false

```

### 在会话菜单中没有重启按钮时，屏幕被锁定

If [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") is installed, ensure that it is not running at startup, see [GNOME#Startup applications](/index.php/GNOME#Startup_applications "GNOME").

### pulseaudio系统原因延误GNOME和GDM

If you are running [PulseAudio](/index.php/PulseAudio "PulseAudio") in system-wide mode, the PulseAudio 7.0 upgrade breaks [GDM](/index.php/GDM "GDM") and GNOME. See [this forum post](https://bbs.archlinux.org/viewtopic.php?id=203051) for more information.

### GNOME 登录需要花很长的时间

用**paprefs**察看你是否启用_PulseAudio Network_ 。只要有任何音频设置启用了，在启动后gnome挂起大约一分钟。

一个方案是新建一个用户，用新建的用户登录。另一个方案是移动`~/.gconf`, `~/.gconfd` 和 `~/.config/dconf`文件夹到别的地方。重登录看问题是否还在。

如果不再延迟，一个个尝试你的设置，看看是哪个导致的错误。

### 安装扩展导致 GNOME 停止工作

如果安装这些扩展导致 GNOME 停止工作，那您必须首先将 _user-theme_ 和 _auto-move-windows_扩展从它们的安装文件夹中移除。

安装目录可能是`~/.local/share/gnome‑shell/extensions`,`/usr/share/gnome‑shell/extensions` 或 `/usr/local/share/gnome‑shell/extensions`中的一个。删除这两个扩展文件夹可能解决问题。如果不能，逐个扩展尝试。

移除或添加扩展到这些文件夹会将它们从系统移除或安装。更多有关GNOME Shell扩展的信息可以在[这里](https://live.gnome.org/GnomeShell/Extensions) 找到。

### GTK 2+ 应用程序显示段错误无法启动

此错误往往在安装了**oxygen-gtk**的情况下发生。这个主题与 GNOME 3 或 GTK 3 的某一设置冲突，当它被设置成 GTK 2 主题时，GTK 2 程序会出现类似下面的段错误：

```
(firefox-bin:14345): GLib-GObject-WARNING **: invalid (NULL) pointer instance

(firefox-bin:14345): GLib-GObject-CRITICAL **: g_signal_connect_data: assertion `G_TYPE_CHECK_INSTANCE (instance)' failed

(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_default_colormap: assertion `GDK_IS_SCREEN (screen)' failed

(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_colormap_get_visual: assertion `GDK_IS_COLORMAP (colormap)' failed

(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_default_colormap: assertion `GDK_IS_SCREEN (screen)' failed

(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_root_window: assertion `GDK_IS_SCREEN (screen)' failed

(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_screen_get_root_window: assertion `GDK_IS_SCREEN (screen)' failed

(firefox-bin:14345): Gdk-CRITICAL **: IA__gdk_window_new: assertion `GDK_IS_WINDOW (parent)' failed
Segmentation fault

```

目前的"解决方法"是把**oxygen-gtk**从系统中完全**移除**并为您的应用程序设置另一个主题。

### ATI Catalyst 驱动在使用 GNOME Shell 的时候遭遇到了毛刺和伪影

目前不推荐使用 Catalyst 运行 GNOME Shell。开源的 ATI 驱动（xf86-video-ati）似乎是能正确地运行 GNOME 3 混成桌面。

**注意:** 有望在 Catalyst 11.9 中修复。参见 [http://ati.cchtml.com/show_bug.cgi?id=99](http://ati.cchtml.com/show_bug.cgi?id=99)

### 多台显示器和 dock 扩展

如果你有多台显示器，并且用 Nvidia Twinview 配置，你的 dock 扩展可能会夹在显示器的中间。编辑扩展的源文件来重定位 dock。

编辑 **/usr/share/gnome-shell/extensions/dock@gnome-shell-extensions.gnome.org/extension.js** ，在代码中找到这行：

```
this.actor.set_position(primary.width-this._item_size-this._spacing-2, (primary.height-height)/2);

```

第一个参数是dock的X方向位置，从2改成15，dock在我的主显示器上到了正确的位置。你可以尝试几个X，Y的值来让他到合理位置。

```
this.actor.set_position(primary.width-this._item_size-this._spacing-15, (primary.height-height)/2);

```

### Empathy和其他程序没有环境音

如果你正在使用 [OSS](/index.php/OSS "OSS"), 你需要安装[AUR上的](https://aur.archlinux.org/packages.php?ID=31163) **libcanberra-oss**。

必须安装**sound-theme-freedesktop**包以获取默认环境声：

```
 # pacman -S sound-theme-freedesktop

```

### 通过 can-change-accels 编辑快捷键失败

也可以通过 accel map 手动设置快捷键。在哪里找到这些文件取决于应用软件，例如，Thuner 在`~/.config/Thunar/accels.scm`，GNOME Files 在 `~/.gnome2/accels/nautilus`。文件含有一系列快捷键，还未更改的快捷键用 ";" 注释，去掉注释以启用。

### 在备用模式右键点击面板停止响应

打开 gconf-editor 找到/apps/metacity/general/mouse_button_modifier，面板和 applets 也在使用快捷键 (<Alt>, <Super> 等)。

### "显示桌面"快捷键无效

GNOME 开发者认为他是一个 bug (察看 [https://bugzilla.gnome.org/show_bug.cgi?id=643609](https://bugzilla.gnome.org/show_bug.cgi?id=643609) )，因为最小化被抛弃了。定义 ALT+STRG+D 为下列设置：

```
系统设置 --> 键盘 --> 快捷键 --> 导航 --> 隐藏所有正常窗口

```

### GNOME Files 不启动

打开 gnome-tweak-tool -> File Manager -> Have file manager handle the desktop -> Off

### 不能保存显示器配置文件

如果你遇到这样的问题，尝试禁用 xrandr gnome-settings-daemon 插件：

```
dconf write /org/gnome/settings-daemon/plugins/xrandr/active false 

```

### 按触摸板锁定键不能重新启用触摸板

有一些笔记本有触摸板锁定键，这样你可以在打字的时候禁用他，不用担心碰到触摸板。但是GNOME可以正确地锁定他，却不能启用。如果触摸板已经被禁用，按下面操作解锁：

1.  按 ALT+F2 , 输入 gnome-terminal，回车
2.  输入以下命令

```
xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 1

```

### 在 GNOME Files 里面 CTRL+V 粘贴路径而不是文件

如果你被这个问题困扰，编辑 _~/.gnome2/accels/nautilus_你可以发现两个 CTRL+V :

```
(gtk_accel_path "<Actions>/DirViewActions/Paste" "<Control>v")
...
(gtk_accel_path "<Actions>/ClipboardActions/Paste" "<Control>v")

```

问题在于第二项，删除他可以好过一阵子，我可能还要再去修改他。另一个方法是修改快捷键。

### 不能连接到加密 Wi-Fi

如果你可以看到 wifi 连接,但是点击加密网络却不能打开输入密码对话,你可能需要安装 network-manager-applet。察看[Gnome NetworkManager setup](/index.php/NetworkManager#GNOME "NetworkManager").

### “Mutter 命令 33 尚未定义。”

当你使用 print screen 截屏的时候，出现“Mutter 命令 33 尚未定义。”。mutter 还用着 metacity 的配置文件。

```
$ sudo pacman -S metacity

```

### “Mutter-dialig：终端命令未定义”

```
$ gconftool-2 --type=string --set "/desktop/gnome/applications/terminal/exec" "gnome-terminal"

```

### Intel CPU 用户开机引导到 GDM 界面提示“oh no”

因为英特尔微码升级方式变更，导致部分新装用户在使用gnome桌面的时候可能会遇到这样的问题：在安装完 gnome 桌面后重启，结果 gdm 不能正常显示，白色背景上提示“oh no something……”和一个“logout”的按钮。 针对此问题，解决办法如下： 安装 Intel 的微码包 intel-ucode（AMD 的微码位于 linux-firmware，属于 base 软件组，所以 AMD 的 CPU 不会遇到此问题），然后执行 grub-mkconfig 重新生成 grub.cfg 文件。对于使用其它引导器的用户可以查看此页面：[Microcode](/index.php/Microcode "Microcode")。

## 外部链接

*   [官方网站](http://www.gnome.org/)
*   主题, 图标, 背景:
    *   [GNOME Art](http://art.gnome.org/)
    *   [GNOME Look](http://www.gnome-look.org/)
*   GTK/GNOME 程序:
    *   [GNOME Files](http://www.gnomefiles.org/)
    *   [GNOME Project Listing](http://www.gnome.org/projects/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=GNOME_(简体中文)&oldid=412762](https://wiki.archlinux.org/index.php?title=GNOME_(简体中文)&oldid=412762)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Desktop environments (简体中文)](/index.php/Category:Desktop_environments_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Desktop environments (简体中文)")