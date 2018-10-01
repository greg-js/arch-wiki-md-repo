## Contents

*   [1 GNOME是什麼?](#GNOME.E6.98.AF.E4.BB.80.E9.BA.BC.3F)
*   [2 如何安裝GNOME桌面](#.E5.A6.82.E4.BD.95.E5.AE.89.E8.A3.9DGNOME.E6.A1.8C.E9.9D.A2)
*   [3 GNOME Sessions](#GNOME_Sessions)
*   [4 啟動GNOME](#.E5.95.9F.E5.8B.95GNOME)
    *   [4.1 圖形化的（Graphically）](#.E5.9C.96.E5.BD.A2.E5.8C.96.E7.9A.84.EF.BC.88Graphically.EF.BC.89)
    *   [4.2 手動開啟](#.E6.89.8B.E5.8B.95.E9.96.8B.E5.95.9F)
    *   [4.3 在Wayland啟動GNOME應用程式](#.E5.9C.A8Wayland.E5.95.9F.E5.8B.95GNOME.E6.87.89.E7.94.A8.E7.A8.8B.E5.BC.8F)
*   [5 導覽解說](#.E5.B0.8E.E8.A6.BD.E8.A7.A3.E8.AA.AA)
    *   [5.1 常用的應用程式名](#.E5.B8.B8.E7.94.A8.E7.9A.84.E6.87.89.E7.94.A8.E7.A8.8B.E5.BC.8F.E5.90.8D)
*   [6 設定](#.E8.A8.AD.E5.AE.9A)
    *   [6.1 系統設定](#.E7.B3.BB.E7.B5.B1.E8.A8.AD.E5.AE.9A)
        *   [6.1.1 顏色](#.E9.A1.8F.E8.89.B2)
        *   [6.1.2 日期 & 時間](#.E6.97.A5.E6.9C.9F_.26_.E6.99.82.E9.96.93)
        *   [6.1.3 預設應用程式](#.E9.A0.90.E8.A8.AD.E6.87.89.E7.94.A8.E7.A8.8B.E5.BC.8F)
        *   [6.1.4 Mouse and touchpad](#Mouse_and_touchpad)
        *   [6.1.5 Network](#Network)
        *   [6.1.6 Online accounts](#Online_accounts)
        *   [6.1.7 Search](#Search)
    *   [6.2 Advanced settings](#Advanced_settings)
        *   [6.2.1 Appearance](#Appearance)
            *   [6.2.1.1 GTK+ themes and icon themes](#GTK.2B_themes_and_icon_themes)
                *   [6.2.1.1.1 Global dark theme](#Global_dark_theme)
            *   [6.2.1.2 Window manager themes](#Window_manager_themes)
                *   [6.2.1.2.1 Titlebar height](#Titlebar_height)
                *   [6.2.1.2.2 Titlebar button order](#Titlebar_button_order)
                *   [6.2.1.2.3 Hide titlebar when maximized](#Hide_titlebar_when_maximized)
            *   [6.2.1.3 GNOME Shell themes](#GNOME_Shell_themes)
        *   [6.2.2 Desktop](#Desktop)
            *   [6.2.2.1 Icons on the Desktop](#Icons_on_the_Desktop)
            *   [6.2.2.2 Lock screen and background](#Lock_screen_and_background)
        *   [6.2.3 Extensions](#Extensions)
        *   [6.2.4 Input methods](#Input_methods)
        *   [6.2.5 Fonts](#Fonts)
        *   [6.2.6 Startup applications](#Startup_applications)
        *   [6.2.7 Power](#Power)
            *   [6.2.7.1 Configure behaviour on lid switch close](#Configure_behaviour_on_lid_switch_close)
            *   [6.2.7.2 Change critical battery level action](#Change_critical_battery_level_action)
        *   [6.2.8 Sort applications into application (app) folders](#Sort_applications_into_application_.28app.29_folders)
*   [7 Tips and tricks](#Tips_and_tricks)
    *   [7.1 Keyboard](#Keyboard)
        *   [7.1.1 Turn on NumLock on login](#Turn_on_NumLock_on_login)
        *   [7.1.2 Hotkey alternatives](#Hotkey_alternatives)
        *   [7.1.3 Keyboard switch with command](#Keyboard_switch_with_command)
        *   [7.1.4 XkbOptions keyboard options](#XkbOptions_keyboard_options)
        *   [7.1.5 De-bind Windows key](#De-bind_Windows_key)
    *   [7.2 Disks](#Disks)
    *   [7.3 Hiding applications from the menu](#Hiding_applications_from_the_menu)
    *   [7.4 Screencast recording](#Screencast_recording)
    *   [7.5 Screenshot](#Screenshot)
    *   [7.6 Log out delay](#Log_out_delay)
    *   [7.7 Disable animations](#Disable_animations)
    *   [7.8 Retina (HiDPI) display support](#Retina_.28HiDPI.29_display_support)
    *   [7.9 Passwords and keys (PGP Keys)](#Passwords_and_keys_.28PGP_Keys.29)
    *   [7.10 Terminal](#Terminal)
        *   [7.10.1 Change default terminal size](#Change_default_terminal_size)
        *   [7.10.2 New terminals adopt current directory](#New_terminals_adopt_current_directory)
        *   [7.10.3 Pad the terminal](#Pad_the_terminal)
        *   [7.10.4 Disable blinking cursor](#Disable_blinking_cursor)
        *   [7.10.5 Disable confirmation window when closing Terminal](#Disable_confirmation_window_when_closing_Terminal)
    *   [7.11 Middle mouse button](#Middle_mouse_button)
    *   [7.12 Enable button and menu icons](#Enable_button_and_menu_icons)
    *   [7.13 Use custom colours and gradients for desktop background](#Use_custom_colours_and_gradients_for_desktop_background)
    *   [7.14 Transitioning backgrounds](#Transitioning_backgrounds)
    *   [7.15 Custom GNOME sessions](#Custom_GNOME_sessions)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Shell freezes](#Shell_freezes)
    *   [8.2 Incorrect application defaults](#Incorrect_application_defaults)
    *   [8.3 Tracker & Documents do not list any local files](#Tracker_.26_Documents_do_not_list_any_local_files)
    *   [8.4 Unable to add accounts in Empathy and GNOME Online Accounts](#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts)
    *   [8.5 Cannot change settings in dconf-editor](#Cannot_change_settings_in_dconf-editor)
    *   [8.6 When an extension breaks the shell](#When_an_extension_breaks_the_shell)
    *   [8.7 Extensions do not work after GNOME 3 update](#Extensions_do_not_work_after_GNOME_3_update)
    *   [8.8 Keyboard shortcut do not work with only conky running](#Keyboard_shortcut_do_not_work_with_only_conky_running)
    *   [8.9 Unable to apply stored configuration for monitors](#Unable_to_apply_stored_configuration_for_monitors)
    *   [8.10 Consistent cursor theme](#Consistent_cursor_theme)
    *   [8.11 Windows cannot be modified with Alt-Key + mouse-button](#Windows_cannot_be_modified_with_Alt-Key_.2B_mouse-button)
    *   [8.12 Slow loading of system icons/slow GDM login](#Slow_loading_of_system_icons.2Fslow_GDM_login)
    *   [8.13 Artifacts when maximizing windows](#Artifacts_when_maximizing_windows)
    *   [8.14 Tear-free video with Intel HD Graphics](#Tear-free_video_with_Intel_HD_Graphics)
    *   [8.15 Window opens behind other windows when using multiple monitors](#Window_opens_behind_other_windows_when_using_multiple_monitors)
    *   [8.16 Lock button fails to re-enable touchpad](#Lock_button_fails_to_re-enable_touchpad)
    *   [8.17 GNOME Shell keyboard sources menu not visible](#GNOME_Shell_keyboard_sources_menu_not_visible)
    *   [8.18 Mouse cursor missing](#Mouse_cursor_missing)
    *   [8.19 No restart button in session menu when screen is locked](#No_restart_button_in_session_menu_when_screen_is_locked)
    *   [8.20 PulseAudio system-wide causes delay in GNOME and GDM](#PulseAudio_system-wide_causes_delay_in_GNOME_and_GDM)
    *   [8.21 GNOME crashes when trying to reorder applications in the GNOME Shell Dash](#GNOME_crashes_when_trying_to_reorder_applications_in_the_GNOME_Shell_Dash)
*   [9 See also](#See_also)

## GNOME是什麼?

[GNOME](http://www.gnome.org/)專案提供了兩樣東西: GNOME桌面環境，一個設計給終使用者的直覺、引人注目的桌面環境。和GNOME開發平台, 一個用來開發可整合進桌面環境的極具擴展性的框架。

## 如何安裝GNOME桌面

在安裝GNOME之前，請先利用以下指令更新你的pacman:

```
# pacman -Syu 
# pacman -Syy

```

這會幫你略過當安裝gnome-media套件時，所需的依賴gstreamer0.10-gconf不存在未更新的系統中的問題。安裝gnome前更新的你系統是必需的。

利用下列指令安裝GNOME桌面:

```
# pacman -S gnome

```

另外，如果需要更多GNOME應用程式，包含檔案管理器,硬碟管理器,文字編輯器和一些遊戲，記得這些程式是以[gnome](https://www.archlinux.org/groups/x86_64/gnome/)為基礎的：

```
# pacman -S gnome-extra

```

這裡有一個套件組(metapackage)，包含了一個群組的組件。你可以選擇安裝這個群組全部的套件或是部分的套件。全部的套件都可以被安全的安裝，此安裝是被高度建議的。但以下是一些可能不被需要的套件的列表

*   **Epiphany** GNOME的網頁瀏覽器。假設你預定要使用其它的網頁瀏覽器，如Firefox。那這個套件就是不必要的。但是仍建議你使用這個被Firefox遮住光環但還是非常棒的瀏覽器。

*   **Evolution** 一個GNOME中用來管理個人資訊的套件(e-mail,行程，聯絡人資訊...等)。假如你想要使用其它的個人資訊管理套件，如Thunderbird，或是網頁版的個人資訊管理套件，如google或yahoo。那麼這個套件就不是必需的。

*   **gnome-backgrounds** 是由GNOME社群為你挑選的桌面布景集合。假設你有自己的桌面背景圖案。那麼這個套件就可以不用安裝。

*   **gnome-screensaver** GNOME桌面的螢幕保護程式集合。假如你不使用螢幕保護程式，那麼這個套件就可以不用安裝。

*   **gnome-themes** GNOME布景主題的集合。假如你要使用自己的布景主題。那麼這個套件就可以不用安裝。

*   **gnome2-user-docs** 和 **yelp** 是GNOME的幫助文件和幫助文件的讀取器。假如你不是個會讀取幫助文件，而是傾向於在Google上找尋幫助的話。那麼這個套件就可以不用安裝。

從GNOME 3開始，GNOME專案從新改寫以迎合現代使用者需求與當代科技。在GNOME中新增以下特色:

*   提供新的預設當代主題與字形
*   活動視窗提供一個快速存取你的視窗與應用程式
*   內建(整合式)訊息桌面服務
*   更多穩定提示系統與更多分離式panel
*   可快速搜尋活動
*   新的系統管理程式
*   ...更多特色請至[GNOME3](http://www.gnome3.org/)

## GNOME Sessions

GNOME有三個可用sessions，都使用GNOME Shell。

*   **GNOME** 是預設的、創新的排版。
*   **GNOME Classic** 是傳統的桌面排版類似GNOME 2的介面，使用預先載入, using pre-activated extensions and parameters.[[1]](http://worldofgnome.org/welcome-to-gnome-3-8-flintstones-mode/)因此它是個高度自訂性。
*   **GNOME on Wayland** 使用協定的GNOME Shell. 傳統的Xwindows應用程式也可透過Xwayland跑在這上面.

## 啟動GNOME

GNOME可以透過[display manager](/index.php/Display_manager "Display manager"), 或手動從終端機開啟. 對於最佳的桌面環境整合, 使用推薦 [GDM](/index.php/GDM "GDM") (the GNOME Display manager). 注意 [啟動](/index.php?title=%E5%95%9F%E5%8B%95&action=edit&redlink=1 "啟動 (page does not exist)") display manager (例如GDM) 代表 Xorg將以root權限啟動.

**Note:** 桌面鎖定功能是由GDM提供的. 如果GNOME不是透過GDM開啟的, 你需要其他的程式來達到桌面鎖定功能 - 看 [List of applications/Security#Screen lockers](/index.php/List_of_applications/Security#Screen_lockers "List of applications/Security").

### 圖形化的（Graphically）

選擇session: *GNOME*, *GNOME Classic* 或 *GNOME on Wayland* 從display manager's session選單.

### 手動開啟

*   對於標準GNOME session, 新增以下到 `~/.xinitrc` 檔案: `exec gnome-session`.
*   對於GNOME Classic session, 新增以下到 `~/.xinitrc` 檔案:
    ```
    export XDG_CURRENT_DESKTOP=GNOME-Classic:GNOME
    export GNOME_SHELL_SESSION_MODE=classic
    exec gnome-session --session=gnome-classic
    ```

修改完`~/.xinitrc` 後, GNOME 可以透過 `startx` 指令開啟 (see [xinitrc](/index.php/Xinitrc "Xinitrc") for additional details, such as preserving the logind session). 設定完 `~/.xinitrc` 後，它可被安排啟動X [Start X at login](/index.php/Start_X_at_login "Start X at login").

**Note:** GNOME on Wayland 需要 [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) package, 而且 **不能** 使用 *startx*與 `~/.xinitrc`開啟. 請使用 `gnome-session --session=gnome-wayland`. 更多資訊, 請看 [Wayland](/index.php/Wayland "Wayland").

### 在Wayland啟動GNOME應用程式

近期, 作為預設, GNOME 應用程式可透過 Xwayland跑於wayland上. 如要測試你的GNOME應用程式於wayland上相容性, 在terminal開啟應用程式並加上`env GDK_BACKEND='wayland,x11' <command>`於command前.

**Note:** 設定全域的Wayland環境, 藉由`env GDK_BACKEND=wayland gnome-session --session=gnome-wayland`指令, 可能無用 - *gnome-session* 將立即跳出. 請使用`export GDK_BACKEND='wayland,x11'` 在你的 bash 設定檔, 或使用 `env GDK_BACKEND='wayland,x11' gnome-session --session=gnome-wayland` 指令. 但總結來說, 這些設定非必要, 只要執行 `gnome-session` 以 `--session=gnome-wayland` 就足夠了. 沒有 `GDK_BACKEND` 環境變數, GNOME 應用程式必須 "Wayland aware" 以執行Wayland應用程式, 或者以Xwayland作為預設. 看更多 `GDK_BACKEND` 於 GNOME [Environment variables](https://developer.gnome.org/gtk3/stable/gtk-running.html).

請看多資訊於此頁面 [GNOME Applications under Wayland](https://wiki.gnome.org/Initiatives/Wayland/Applications/).

## 導覽解說

學習GNOME更多更有效率請看[GNOME Shell Cheat Sheet](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet); 其強調更多GNOME Shell 特色與快捷箭，包含任務選擇,鍵盤使用,視窗控制,面板,鳥瞰模式,與更多。 一些快捷鍵:

*   `Super` + `m`: 顯示訊息
*   `Super` + `a`: 顯示應用程式目錄
*   `Alt-` + `Tab`: 循環顯示當前活動中程式
*   `Alt-` + ``` (在 `Tab` 上的那個鍵 (US keyboard) ): 循環顯示使用程式之子視窗
*   `Alt` + `F2`, 然後按`r` 或 `restart`: 從新啟動有問題的圖形化界面.

### 常用的應用程式名

**Note:** 有些GNOME應用程式有換過名字於文件中，而且在對話窗中也換了，但執行期則否. 一些這類程式列在底下.

**Tip:** 搜尋一些程式的常用名稱在GNOME shell的搜尋欄中將會成功回傳結果. 例如, 搜尋 *nautilus* 將顯示 *Files*.

| 現在名 | 常用名 |
| [Files](/index.php/Files "Files") | Nautilus |
| [Web](/index.php/GNOME_Web "GNOME Web") | Epiphany |
| Videos | Totem |
| Main Menu | Alacarte |
| Document Viewer | Evince |
| Disk Usage Analyser | Baobab |
| Image Viewer | EoG (Eye of GNOME) |
| [Passwords and Keys](/index.php/GNOME_Keyring "GNOME Keyring") | Seahorse |

## 設定

GNOME 桌面以 configuration database backend (DConf) 來儲存系統與程式設定. 當軟體被安裝時，他的預設設定會載入資料庫. 基本設定會藉由GNOME系統設定面板 (*gnome-control-center*) 或每個應用程式的偏好設定來載入. 直接對DConf資料庫操作永遠可用 *gsettings*指令工具. 尤其，它可那些無圖形化設定工具進行設定。

GNOME設定以GNOME Settings Daemon來運行. 注意這個daemon可在GNOME session運行， 想執行GNOME 設定在非GNOME環境. 請執行 `nohup /usr/lib/gnome-settings-daemon/gnome-settings-daemon > /dev/null &` .

設定通常只涵蓋單一使用者，對於剩下的使用者，本篇並不提供建立多使用者系統樣板之教學。

### 系統設定

值得注意的控制面板設定

#### 顏色

daemon `colord` 讀取顯示器的 EDID並提取適合顏色. 大多數顏色設定以準確不須修改; 然而對於那些不準確的或舊型顯示器, color顏色設定會被放在`~/.local/share/icc/` 並被執行.

#### 日期 & 時間

如果系統有被設定 [Network Time Protocol daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon"), 它會效果很好.如果需要同步時間可透過手動設定從目錄.

顯示日期於視窗最頂欄, 執行:

```
$ gsettings set org.gnome.desktop.interface clock-show-date true

```

另外, 顯示週數在Shell Calender, 執行:

```
$ gsettings set org.gnome.shell.calendar show-weekdate true

```

#### 預設應用程式

安裝完gnome完之後可能發現一些錯置的預設應用程式，例如：*totem*開源播放器取代常見的[VLC](/index.php/VLC "VLC")，這些設定可以透過：*System*>*Details*>*Default applications*來修改。 其他的協定與方法可看[Default appliactions](/index.php?title=Default_appliactions&action=edit&redlink=1 "Default appliactions (page does not exist)")來設定。

#### Mouse and touchpad

To help reduce touchpad interference you may wish to implement the settings below:

*   Disable touchpad while typing
*   Disable scrolling
*   Disable tap-to-click

#### Network

[NetworkManager](/index.php/NetworkManager "NetworkManager") is the native tool of the GNOME project to control network settings from the shell. It is installed by default as a dependency for [tracker](https://www.archlinux.org/packages/?name=tracker) package, which is a part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group, and just needs to be [enabled](/index.php/NetworkManager#Enable_NetworkManager "NetworkManager").

While any other [network manager](/index.php/List_of_applications/Internet#Network_managers "List of applications/Internet") can be used as well, NetworkManager provides the full integration via the shell network settings and a status indicator applet [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) (not required for GNOME).

#### Online accounts

Backends for the GNOME messaging application [empathy](https://www.archlinux.org/packages/?name=empathy) as well as the GNOME Online Accounts section of the System Settings panel are provided in a separate group: [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/). See [#Unable to add accounts in Empathy and GNOME Online Accounts](#Unable_to_add_accounts_in_Empathy_and_GNOME_Online_Accounts). Some online accounts, such as [ownCloud](/index.php/OwnCloud "OwnCloud"), require [gvfs-goa](https://www.archlinux.org/packages/?name=gvfs-goa) to be installed for full functionality in GNOME applications such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") and GNOME Documents [[2]](https://wiki.gnome.org/ThreePointSeven/Features/Owncloud).

#### Search

The GNOME shell has a search that can be quickly accessed by pressing the `Super` key and starting to type. The [tracker](https://www.archlinux.org/packages/?name=tracker) package is installed by default as a part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group and provides an indexing application and metadata database. It can be configured with the *Search and Indexing* menu item; monitor status with *tracker-control*. It is started automatically by *gnome-session* when the user logs in. Indexing can be started manually with `tracker-control -s`. Search settings can also be configured in the *System Settings* panel.

The Tracker database can be queried using the *tracker-sparql* command. View its manual page [tracker-sparql(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tracker-sparql.1) for more information.

### Advanced settings

As noted above, many configuration options such as changing the [GTK+](/index.php/GTK%2B "GTK+") theme or the [window manager](/index.php/Window_manager "Window manager") theme are not exposed in the GNOME System Settings panel (*gnome-control-center*). Those users that want to configure these settings may wish to use the GNOME Tweak Tool ([gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool)), a convenient graphical tool which exposes many of these settings.

GNOME settings (which are stored in the DConf database) can also be configured using the [*dconf-editor*](https://developer.gnome.org/dconf/unstable/dconf-editor.html) (a graphical DConf configuration tool) or the [*gsettings*](https://developer.gnome.org/gio/stable/GSettings.html) command line tool. The GNOME Tweak Tool does not do anything else in the background of the GUI; note though that you will not find all settings described in the following sections in it.

#### Appearance

##### GTK+ themes and icon themes

To install a new theme or icon set, add the relevant `~/.local/share/themes` or `~/.local/share/icons` respectively (add to `/usr/share/` instead of `~/.local/share/` for the themes to be available systemwide.) They and other GUI settings can also be defined in `~/.config/gtk-3.0/settings.ini`:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-theme-name = Adwaita
# next option is applicable only if selected theme supports it
gtk-application-prefer-dark-theme = true
# set font name and dimension
gtk-font-name = Sans 10

```

Additional theme locations:

*   [DeviantArt](http://www.deviantart.com/browse/all/customization/skins/linuxutil/desktopenv/gnome/gtk3/).
*   [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=167).
*   [GTK3 themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gtk3&do_Search=Go).
*   [Cursor themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=xcursor&do_Search=Go&PP=50&SB=v&SO=d).
*   [Icon themes in the AUR](https://aur.archlinux.org/packages.php?O=0&K=icon-theme&do_Search=Go&PP=50&SB=v&SO=d).

Once installed, they can be selected using the GNOME Tweak Tool or GSettings - see below for GSettings commands:

For the GTK+ theme:

```
$ gsettings set org.gnome.desktop.interface gtk-theme *theme-name*

```

For the icon theme

```
$ gsettings set org.gnome.desktop.interface icon-theme *theme-name*

```

###### Global dark theme

GNOME will use the Adwaita light theme by default however a dark variant of this theme (called the Global Dark Theme) also exists and can be selected using the Tweak Tool or by editing the GTK+ 3 settings file - see [GTK+#Dark theme variant](/index.php/GTK%2B#Dark_theme_variant "GTK+"). Some applications such as Image Viewer (*eog*) use the dark theme by default. It should be noted that the Global Dark Theme only works with GTK+ 3 applications; some GTK+ 3 applications may only have partial support for the Global Dark theme. Qt and GTK+ 2 support for the Global Dark Theme may be added in the future.

##### Window manager themes

The window manager theme (the style of the window titlebars) can be set using the GNOME Tweak Tool or the following GSettings command:

```
$ gsettings set org.gnome.desktop.wm.preferences theme *theme-name*

```

###### Titlebar height

**Note:** As of GNOME 3.16, Mutter no longer uses Metacity themes. Instead, the titlebar decorations are themed using GTK+.

To change the titlebar height, create the following file, adjusting the padding as desired:

 `~/.config/gtk-3.0/gtk.css` 
```
.header-bar {
	padding-top: 3px;
	padding-bottom: 3px;
	font-size: 9px;
}

.header-bar .button {
	padding-top: 5px;
	padding-bottom: 5px;
}

```

###### Titlebar button order

To set the order for the GNOME window manager (Mutter, Metacity):

```
$ gsettings set org.gnome.desktop.wm.preferences button-layout ':minimize,maximize,close'

```

**Tip:** The colon indicates which side of the titlebar the window buttons will appear.

###### Hide titlebar when maximized

*   [Install](/index.php/Install "Install") [mutter-hide-legacy-decorations](https://aur.archlinux.org/packages/mutter-hide-legacy-decorations/). It changes a default setting in the window manager, so as to automatically hide the titlebar on legacy (non-headerbar) apps when they are maximized or tiled to the side.

*   [Install](/index.php/Install "Install") [maximus](https://aur.archlinux.org/packages/maximus/). To start the application, execute *maximus* from a terminal. When running, the daemon will automatically maximize windows. It will undecorate maximized windows and redecorate them when they are unmaximized. If you do not want all windows to start maximized, run `maximus -m` instead. Note that this will only work with windows decorated by the window manager; applications that use client-side decoration such as [GNOME Files](/index.php/GNOME_Files "GNOME Files") will not be undecorated when maximized.

##### GNOME Shell themes

The theme of GNOME Shell itself is configurable. To use a Shell theme, firstly ensure that you have the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package installed. Then enable the *User Themes* extension, either through GNOME Tweak Tool or through the [GNOME Shell Extensions](https://extensions.gnome.org) webpage. Shell themes can then be loaded and selected using the GNOME Tweak Tool.

There are a number of GNOME Shell themes available [in the AUR](https://aur.archlinux.org/packages.php?O=0&K=gnome-shell-theme&do_Search=Go&PP=50&SB=v&SO=d).

Shell themes can also be downloaded from [gnome-look.org](http://gnome-look.org/index.php?xcontentmode=191).

#### Desktop

Various Desktop settings can be applied.

##### Icons on the Desktop

See [GNOME Files#Desktop Icons](/index.php/GNOME_Files#Desktop_Icons "GNOME Files").

##### Lock screen and background

When setting the Desktop or Lock screen background, it is important to note that the Pictures tab will only display pictures located in `/home/*username*/Pictures` folder. If you wish to use a picture not located in this folder, use the commands indicated below.

For the desktop background:

```
$ gsettings set org.gnome.desktop.background picture-uri 'file:///path/to/my/picture.jpg'

```

For the lock screen background

```
$ gsettings set org.gnome.desktop.screensaver picture-uri 'file:///path/to/my/picture.jpg'

```

#### Extensions

**Note:** The GNOME Shell browser plugin which allows users to install extensions from [extensions.gnome.org](https://extensions.gnome.org) is not compatible with Chrome/Chromium versions 35 and over. Users wishing to install extensions from the webpage will have to use a compatible browser such as [Firefox](/index.php/Firefox "Firefox") or [GNOME Web](/index.php/GNOME_Web "GNOME Web").

GNOME Shell can be customized with extensions per user or system-wide.

The catalogue of extensions is available at [extensions.gnome.org](https://extensions.gnome.org). By a user they can be installed and activated in the browser by setting the switch in the top left of the screen to **ON** and clicking **Install** on the resulting dialog (if the extension in question is not installed). After installation it is shown in the [extensions.gnome.org/local/](https://extensions.gnome.org/local/) tab, which has to be visited as well to check for available updates. Installed extensions can also be enabled or disabled using [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool).

More information about GNOME shell extensions is available on the [GNOME Shell Extensions about page](https://extensions.gnome.org/about/).

[Installing](/index.php/Install "Install") extensions via a package makes them available for all users of the system and automates the update process.

The [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package provides a set of extensions maintained as part of the GNOME project (many of the included extensions are used by the GNOME Classic session).

Users who want a taskbar but do not wish to use the GNOME Classic session may want to enable the *Window list* extension (provided by the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package).

#### Input methods

GNOME has integrated support for input methods through [IBus](/index.php/IBus "IBus"), only [ibus](https://www.archlinux.org/packages/?name=ibus) and the wanted input method engine (e.g. [ibus-libpinyin](https://www.archlinux.org/packages/?name=ibus-libpinyin) for Intelligent Pinyin) needed to be installed, after installation the input method engine can be added as a keyboard layout in GNOME's Regional & Language Settings.

#### Fonts

**Tip:** If you set the *Scaling factor* to a value above 1.00, the Accessibility menu will be automatically enabled.

Fonts can be set for Window titles, Interface (applications), Documents and Monospace. See the Fonts tab in the Tweak Tool for the relevant options.

For hinting, RGBA will likely be desired as this fits most monitors types, and if fonts appear too blocked reduce hinting to *Slight* or *None*.

#### Startup applications

To start certain applications on login, copy the relevant `.desktop` file from `/usr/share/applications/` to `~/.config/autostart/`.

The same effect can be achieved using the Tweak Tool.

**Tip:** If the plus sign button in the Tweak Tool's Startup Applications section is unresponsive, try start the Tweak Tool from the terminal using the following command: `gnome-tweak-tool`. See the following [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1413631#p1413631).

**Note:** The *gnome-session-properties* dialog was removed as of GNOME 3.12\. It can be added back by [installing](/index.php/Install "Install") the [gnome-session-properties](https://aur.archlinux.org/packages/gnome-session-properties/) package.

#### Power

The basic power settings that may want to be altered (these example settings assume the user is using a laptop - change them as desired):

```
$ gsettings set org.gnome.settings-daemon.plugins.power button-power *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-timeout *3600*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type *hibernate*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-timeout *1800*
$ gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-battery-type *hibernate*
$ gsettings set org.gnome.desktop.lockdown disable-lock-screen *true*

```

To keep a monitor active on lid close:

```
$ gsettings set org.gnome.settings-daemon.plugins.xrandr default-monitors-setup do-nothing

```

##### Configure behaviour on lid switch close

The GNOME Tweak Tool, as of version 3.17.1, can optionally *inhibit* the *systemd* setting for the lid close ACPI event.[[3]](http://ftp.gnome.org/pub/GNOME/sources/gnome-tweak-tool/3.17/gnome-tweak-tool-3.17.1.news) To *inhibit* the setting, start the Tweak Tool and, under the power tab, check the *Don't suspend on lid close* option. This means that the system will do nothing on lid close instead of suspending - the default behaviour. Checking the setting creates `~/.config/autostart/ignore-lid-switch-tweak.desktop` which will autostart the Tweak Tool's inhibitor.

If you do not want the system to suspend or do nothing on lid close, you will need to ensure that the setting described above is **not** checked and then configure *systemd* with `HandleLidSwitch=*preferred_behaviour*` as described in [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management").

##### Change critical battery level action

The System Settings panel only allows the user to choose between *Suspend* or *Hibernate*. To choose another option such as *Do Nothing* open the `dconf-editor` and navigate to `org.gnome.settings-daemon.plugins.power`. Edit the `"critical-battery-action"` value to `"nothing"`.

#### Sort applications into application (app) folders

**Tip:** The [gnome-catgen](https://github.com/prurigro/gnome-catgen) ([gnome-catgen-git](https://aur.archlinux.org/packages/gnome-catgen-git/)) script allows you to manage folders through the creation of files in `~/.local/share/applications-categories` named after each category and containing a list of the desktop files belonging to apps you would like to have inside. Optionally, you can have it cycle through each app without a folder and input the desired category until you ctrl-c or run out of apps.

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

Applications can also be sorted by their category (specified in their *.desktop* file):

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ categories "['Office']"

```

If certain applications matching a category are not wanted in a certain folder, exclusions can be set:

```
$ gsettings set org.gnome.desktop.app-folders.folder:/org/gnome/desktop/app-folders/folders/Sundry/ excluded-apps "['libreoffice-draw.desktop']"

```

For further information, refer to the [app-folders schema](https://git.gnome.org/browse/gsettings-desktop-schemas/tree/schemas/org.gnome.desktop.app-folders.gschema.xml.in.in).

## Tips and tricks

Other GNOME system settings and tips.

### Keyboard

#### Turn on NumLock on login

Run the following command:

```
$ gsettings set org.gnome.settings-daemon.peripherals.keyboard numlock-state on

```

#### Hotkey alternatives

A lot of hotkeys can be changed via system settings menu. For example, to re-enable the show desktop keybinding:

*System settings* > *Keyboard* > *Shortcuts* > *Navigation* > *Hide all normal windows*

However, certain hotkeys cannot be changed directly via system settings. In order to change these keys, use *dconf-editor*. An example of particular note is the hotkey `Alt-` + ``` (the key above `Tab` on US keyboard layouts). In GNOME Shell it is pre-configured to cycle through windows of an application, however it is also a hotkey often used in the [Emacs](/index.php/Emacs "Emacs") editor. It can be changed by opening *dconf-editor* and modifying the *switch-group* key found in `org.gnome.desktop.wm.keybindings`.

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

#### Keyboard switch with command

To have keyboard shortcut **Alt** + **Shift** switch keyboards:

Open Gnome-Tweak-Tool (or Keyboard Settings, in GNOME 3.16) and set *Typing* > *Modifiers-only input sources* > *select Alt-shift*. For more information see also the forum [thread](https://bbs.archlinux.org/viewtopic.php?id=152127).

#### XkbOptions keyboard options

Using the **dconf-editor**, navigate to the key named `org.gnome.desktop.input-sources.xkb-options` and add desired XkbOptions (e.g. *caps:swapescape*) to the list.

See `/usr/share/X11/xkb/rules/xorg` for all XkbOptions and `/usr/share/X11/xkb/symbols/*` for the respective descriptions.

**Note:** To enable the `Ctrl+Alt+Backspace` combination to terminate Xorg, use the [gnome-tweak-tool](https://www.archlinux.org/packages/?name=gnome-tweak-tool). Within the **Tweak Tool**, navigate to *Typing > Key sequence to kill the X server* and select the option `Ctrl+Alt+Backspace` from the dropdown menu.

#### De-bind Windows key

By default, the 'Windows key' will open the GNOME Shell overview mode. You can unbind this key by running the command below

```
$ gsettings set org.gnome.mutter overlay-key 'Foo'

```

### Disks

GNOME provides a disk utility to manipulate storage drive settings. These are some of its features:

*   **Enable write cache** is a feature that most hard drives provide. Data is cached and allocated at chosen times to improve system performance. Not recommended unless the computer has a backup battery pack or is a laptop as data would be lost on power failure.

	*Settings* > *Drive Settings* > *Write Cache* > **On**

*   **Automatic Mount Options** can mount drives and partitions that are GPT based - will use default, recommended options.

**Warning:** This setting erases related [fstab](/index.php/Fstab "Fstab") entries

	*Partition Settings* > *Edit Mount Options* > *Automatic Mount Options* > **On**

### Hiding applications from the menu

**Tip:** Desktop entries can be hidden by editing the `.desktop` files themselves. See [Desktop entries#Hide desktop entries](/index.php/Desktop_entries#Hide_desktop_entries "Desktop entries").

Use the *Main Menu* application (provided by the [alacarte](https://www.archlinux.org/packages/?name=alacarte) package) to hide any applications you do not wish to show in the menu.

### Screencast recording

GNOME features built-in screencast recording with the **Ctrl** + **Shift** + **Alt** + **R** key combination. A red circle is displayed in the bottom right corner of the screen when the recording is in progress. After the recording is finished, a file named `Screencast from %d%u-%c.webm` is saved in the Videos directory. In order to use the screencast feature the gst plugins need to be installed.

### Screenshot

Default save directory:

```
$ gsettings set org.gnome.gnome-screenshot auto-save-directory file:///home/*USER*/Desktop

```

Check the *gnome-screenshot* manual page for more options.

### Log out delay

To eliminate the default 60 second delay when logging out:

```
$ gsettings set org.gnome.SessionManager logout-prompt false

```

### Disable animations

To disable Shell animations (such as "Show Applications" and the wave animation in the top left activities hot corner), run:

```
$ gsettings set org.gnome.desktop.interface enable-animations false

```

### Retina (HiDPI) display support

GNOME introduced HiDPI support in version 3.10\. If your display does not provide the correct screen size through EDID, this can lead to incorrectly scaled UI elements. As a workaround you can open *dconf-editor* and find the key `scaling-factor` in `org.gnome.desktop.interface`. Set it to `1` to get the standard scale.

Also see [HiDPI](/index.php/HiDPI "HiDPI").

### Passwords and keys (PGP Keys)

You can use the Passwords and Keys program (*seahorse*) to create a PGP key as it is a front end for [GnuPG](/index.php/GnuPG "GnuPG") and installs it as dependency. This may be useful in the future (for instance if to encrypt a file). Create a key as shown below (the process may take about 10 minutes):

*File* > *New* > *PGP Key* > *Name* > *Email* > *Defaults* > *Passphrase*.

### Terminal

#### Change default terminal size

The default size of a new terminal can be adjusted in the menu *Edit > Profile preferences* .

#### New terminals adopt current directory

By default new terminals open in the `$HOME` directory. To have new terminals adopt the current working directory: `source /etc/profile.d/vte.sh`. Add the command to the shell configuration to retain the behaviour. [[4]](http://unix.stackexchange.com/questions/93476/gnome-terminal-keep-track-of-directory-in-new-tab)

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

#### Disable blinking cursor

Since GNOME 3.8 and the migration to GSettings and DConf the key required to modify in order to disable the blinking cursor in the Terminal differs slightly in contrast to the old GConf key. To disable the blinking cursor in GNOME 3.8 and above use:

```
$ gsettings set org.gnome.desktop.interface cursor-blink false

```

To disable the blinking cursor in Terminal only use (make sure profile uid is correct one):

```
$ dconf write /org/gnome/terminal/legacy/profiles:/:b1dcc9dd-5262-4d8d-a863-c897e6d979b9/cursor-blink-mode "'off'"

```

Note that `gnome-settings-daemon`, from the package of the same name, must be running for this and other settings changes to take effect in GNOME applications - see [#Configuration](#Configuration).

#### Disable confirmation window when closing Terminal

The Terminal will always display a confirmation window when trying to close the window while one is logged in as root. To avoid this, execute the following:

```
$ gsettings set org.gnome.Terminal.Legacy.Settings confirm-close false

```

### Middle mouse button

By default, GNOME 3 disables middle mouse button emulation regardless of [Xorg](/index.php/Xorg "Xorg") settings (**Emulate3Buttons**). To enable middle mouse button emulation use:

```
$ gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true

```

### Enable button and menu icons

Since GTK+ 3.10, the GSettings key 'menus-have-icons' has been deprecated. Icons in buttons and menus can still be enabled by setting the following overrides:

```
$ gsettings set org.gnome.settings-daemon.plugins.xsettings overrides "{'Gtk/ButtonImages': <1>, 'Gtk/MenuImages': <1>}"

```

### Use custom colours and gradients for desktop background

To use custom colours and gradients for your desktop background, you will first need to set either a transparent picture or else a non-existent picture as your desktop background. For instance, the command below will set a non-existent picture as the background.

```
$ gsettings set org.gnome.desktop.background picture-uri none

```

At this point, the desktop background should be a flat colour - the default colour setting is for a deep blue.

For a different flat colour you need only change the primary colour setting:

```
$ gsettings set org.gnome.desktop.background primary-color <my color>

```

where <my color> is a hex value (such as *ffffff* for white).

For a colour gradient, you will also need to change secondary colour setting `org.gnome.desktop.background secondary-color` and select a shading type. For instance, if you want a horizontal gradient, execute the following:

```
$ gsettings set org.gnome.desktop.background color-shading-type horizontal

```

If you are using a transparent picture as your background, you can set the opacity by executing the following:

```
$ gsettings set org.gnome.desktop.background picture-opacity <value>

```

where value is a number between 1 and 100 (100 for maximum opacity).

### Transitioning backgrounds

GNOME can transition between different wallpapers at specific time intervals. This is done by creating an XML file specifying the pictures to be used and the time interval. For more information on creating such files, see the following [article](http://www.linuxjournal.com/content/create-custom-transitioning-background-your-gnome-228-desktop).

Alternatively, a number of tools are available to automate the process:

*   **mkwlppr** — This script creates XML files that can act as dynamic wallpapers for GNOME by referring to multiple wallpapers.

	[http://pastebin.com/019G2rCy](http://pastebin.com/019G2rCy) || see [mkwlppr](http://pastebin.com/019G2rCy)

*   **[Wallpapoz](/index.php/Wallpapoz "Wallpapoz")** — Wallpapoz is a tool that provides dynamic wallpapers for GNOME and Xfce desktops.

	[https://vajrasky.wordpress.com/](https://vajrasky.wordpress.com/) || [wallpapoz](https://aur.archlinux.org/packages/wallpapoz/)

*   **CreBS** — A Python/GTK application used to create and set desktop wallpaper slideshows for GNOME.

	[http://www.obfuscatepenguin.net/](http://www.obfuscatepenguin.net/) || [crebs](https://aur.archlinux.org/packages/crebs/)

For setting the XML file as the default background, see [#Lock screen and background](#Lock_screen_and_background).

### Custom GNOME sessions

It is possible to create custom GNOME sessions which use the GNOME session manager but start different sets of components ([Openbox](/index.php/Openbox "Openbox") with [tint2](/index.php/Tint2 "Tint2") instead of GNOME Shell for example).

Two files are required for a custom GNOME session: a session file in `/usr/share/gnome-session/sessions/` which defines the components to be started and a [desktop entry](/index.php/Desktop_entry "Desktop entry") in `/usr/share/xsessions` which is read by the [display manager](/index.php/Display_manager "Display manager"). An example session file is provided below:

 `/usr/share/gnome-session/sessions/gnome-openbox.session` 
```
[GNOME Session]
Name=GNOME Openbox
RequiredComponents=openbox;tint2;gnome-settings-daemon;

```

And an example desktop file:

 `/usr/share/xsessions/gnome-openbox.desktop` 
```
[Desktop Entry]
Name=GNOME Openbox
Exec=gnome-session --session=gnome-openbox

```

**Note:** GNOME Session calls upon the `.desktop` files of each of the components to be started. If a component you wish to start does not provide a `.desktop` file, you must create a suitable desktop entry in a directory such as `/usr/local/share/applications`.

## Troubleshooting

### Shell freezes

In the event of a Shell freeze (which might be caused by certain appearance tweaks, malfunctioning extensions or perhaps a lack of available memory) restarting the Shell by pressing `Alt` + `F2` and then entering **r** may not be possible.

In this case, try switching to another TTY (**Ctrl** + **Alt** + **F2**) and entering the following command: `pkill -HUP gnome-shell`. It may take a few seconds before the Shell successfully restarts. Restarting the shell in this fashion should not log the user out but it is a good idea to try and ensure that all work is saved anyway.

If this fails, the [Xorg](/index.php/Xorg "Xorg") server will need to be restarted either by: `pkill X` for console logins or: `systemctl restart gdm` for GDM logins. Bear in mind that restarting the Xorg server will log the user out so try to ensure that all work is saved before attempting this.

### Incorrect application defaults

When installing applications for the first time you may find that GNOME has the wrong application associated to a certain protocols - for instance, *easytag* becomes the folder handler instead of [GNOME Files](/index.php/GNOME_Files "GNOME Files").

For GNOME Files see the following page: [GNOME Files#Files is no longer the default file manager](/index.php/GNOME_Files#Files_is_no_longer_the_default_file_manager "GNOME Files").

For Document Viewer, run the following command:

```
$ xdg-mime default evince.desktop application/pdf

```

For other applications, default handler settings are detailed on the following page: [Default applications](/index.php/Default_applications "Default applications").

Optionally, you can [install](/index.php/Install "Install") [gnome-defaults-list](https://aur.archlinux.org/packages/gnome-defaults-list/). It will place your configuration file at `/etc/gnome/defaults.list`.

### Tracker & Documents do not list any local files

In order for Tracker (and, therefore, Documents) to detect your local files, they must be stored in an [XDG compliant directory](http://standards.freedesktop.org/basedir-spec/basedir-spec-latest.html) (such as 'Documents' or 'Music'). For more information, see [XDG user directories](/index.php/XDG_user_directories "XDG user directories").

You can also configure Tracker to recursively search inside specific directories such as your home directory. These settings can be made using `tracker-preferences`.

### Unable to add accounts in Empathy and GNOME Online Accounts

Empathy, the engine behind integrated messaging, GNOME Online Accounts, and all other system settings based on messaging accounts will not function correctly unless the [telepathy](https://www.archlinux.org/groups/x86_64/telepathy/) group of packages or at least one of the backends ([telepathy-gabble](https://www.archlinux.org/packages/?name=telepathy-gabble), or [telepathy-haze](https://www.archlinux.org/packages/?name=telepathy-haze), for example) is [installed](/index.php/Install "Install"). View descriptions of *telepathy* components on the [freedesktop.org telepathy wiki](http://telepathy.freedesktop.org/wiki/Components).

**Note:** [Avahi](/index.php/Avahi "Avahi") daemon is required for connecting with the People Nearby account, and also in order for some desktop extensions to work correctly like [Chat Status](https://extensions.gnome.org/extension/746/chat-status/)

### Cannot change settings in dconf-editor

When one cannot set settings in [dconf](https://www.archlinux.org/packages/?name=dconf), it is possible their dconf user settings are corrupt. In this case it is best to delete the user dconf files in `~/.config/dconf/user*` and set the settings in dconf-editor after.

### When an extension breaks the shell

When enabling shell extensions causes GNOME breakage, you should first remove the *user-theme* and *auto-move-windows* extensions from their installation directory.

The installation directory could be one of `~/.local/share/gnome‑shell/extensions`, `/usr/share/gnome‑shell/extensions` or `/usr/local/share/gnome‑shell/extensions`. Removing these two extension-containing folders may fix the breakage. Otherwise, isolate the problem extension with trial‑and‑error.

Removing or adding an extension-containing folder to the aforementioned directories removes or adds the corresponding extension to your system. Details on GNOME Shell extensions are available at the [GNOME web site.](https://live.gnome.org/GnomeShell/Extensions)

If you have trouble with uninstalling an extension via [extensions.gnome.org/local](https://extensions.gnome.org/local/), then probably they have been installed as system-wide extensions with the [gnome-shell-extensions](https://www.archlinux.org/packages/?name=gnome-shell-extensions) package. Removing the package again obviously affects all user accounts.

### Extensions do not work after GNOME 3 update

**Note:** Please bear in mind that whilst the methods below will allow you to **try** and activate an extension with an unsupported version of GNOME Shell, it is by no means a guarantee that the extension will work successfully. The most likely outcome of trying to activate such an extension is that GNOME Shell will crash and then restart.

Before trying the workarounds below, check if an update is available for the extension by visiting [extensions.gnome.org/local](https://extensions.gnome.org/local).

If there is no update for your current GNOME version yet, use the following command to disable version validation for extensions:

```
$ gsettings set org.gnome.shell disable-extension-version-validation true

```

Alternatively, you could modify the extension itself, changing the supported shell version to satisfy the version validation. See the method below.

Locate the folder where your extensions are installed. It might be `~/.local/share/gnome-shell/extensions` or `/usr/share/gnome-shell/extensions`.

Edit each occurrence of `metadata.json` which appears in each extension sub-folder.

| Insert: | `"shell-version": ["3.x"]` |
| Instead of (for example): | `"shell-version": ["3.4"]` |

`"3.x"` indicates the extension works with every shell version. If it breaks, you will know to change it back.

### Keyboard shortcut do not work with only conky running

The GNOME shell keyboard shortcuts like `Alt+F2`, `Alt+F1`, and the media key shortcuts do not work if conky is the only program running. However, if another application like *gedit* is running, then the keyboard shortcuts work.

Solution: edit `.conkyrc`

```
own_window yes
own_window_transparent yes
own_window_argb_visual yes
own_window_type dock
own_window_class Conky
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager

```

### Unable to apply stored configuration for monitors

If you encounter this message try to disable the *xrandr* `gnome-settings-daemon plugin`:

```
$ dconf write /org/gnome/settings-daemon/plugins/xrandr/active false

```

### Consistent cursor theme

See [Cursor themes#Desktop environments](/index.php/Cursor_themes#Desktop_environments "Cursor themes").

### Windows cannot be modified with Alt-Key + mouse-button

In GNOME 3.6 and above, the mouse button modifier (the key that allows you to drag a window from a location other than the titlebar) is the `Super` key instead of the `Alt` key which was used in the past. The change was made in response to the following [bug report](https://bugzilla.gnome.org/show_bug.cgi?id=607797).

To change the mouse button modifier back to the `Alt` key, execute the following:

```
$ gsettings set org.gnome.desktop.wm.preferences mouse-button-modifier '<Alt>'  

```

**Note:** It is not possible to change this with *System settings* > *Keyboard* > *Shortcuts*

### Slow loading of system icons/slow GDM login

Problems with the loading of system icons, such the ones in the title bar of Files, might be solved by executing the following command:

```
# gdk-pixbuf-query-loaders --update-cache

```

Running the aforementioned command may also fix repeated occurrences of the "Oh no! Something has gone wrong!" error screen and/or very slow loading and login with GDM as described in the following [forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1414157).

### Artifacts when maximizing windows

Maximizing windows may cause artifacts as of GNOME 3.12.0 - see the following [forum thread](https://bbs.archlinux.org/viewtopic.php?id=183617) and [bug report](https://bugzilla.gnome.org/show_bug.cgi?id=728385). A solution is detailed in the following section: [#Tear-free video with Intel HD Graphics](#Tear-free_video_with_Intel_HD_Graphics).

### Tear-free video with Intel HD Graphics

	DRI3

According to [this bug report](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c2), DRI3 includes the `buffer_age` extension that allows GNOME Shell's Mutter compositor to sync windows to vblank in an efficient way. [Enable](/index.php/Intel_graphics#Direct_Rendering_Infrastructure_3_.28DRI3.29 "Intel graphics") it in the Xorg driver. You can change `AccelMethod` to your preference in the configuration file created, but the line must be included when the file is created; otherwise, `gnome-session` will crash upon login in a non-Wayland session.

	Intel TearFree

Enabling the [Xorg Intel TearFree option](/index.php/Intel_graphics#Tear-free_video "Intel graphics") is a known workaround for tearing problems on Intel adapters. However, the way this option acts makes it redundant with the use of a compositor (it increases memory consumption and lowers performance, see [the original bug report's final comment](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c123)).

	Mutter tweaks

**Note:** This workaround has been [reported](https://bugzilla.gnome.org/show_bug.cgi?id=711028#c0) to have side effects and may not fix tearing in all cases.

GNOME Shell's Mutter compositor has a tweak known to address tearing problems (see [the original suggestion for this fix](https://bugzilla.gnome.org/show_bug.cgi?id=657071#c1) and its mention in [the Freedesktop bug report](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c59)). To enable this tweak, append the following line to `/etc/environment`: `CLUTTER_PAINT=disable-clipped-redraws:disable-culling`. Then restart the Xorg server.

### Window opens behind other windows when using multiple monitors

This is possibly a bug in GNOME Shell which causes new windows to open behind others. To fix this issue, one can run the following command:

```
$ gsettings set org.gnome.shell.overrides workspaces-only-on-primary false

```

### Lock button fails to re-enable touchpad

Some laptops have a touchpad lock button that disables the touchpad so that users can type without worrying about touching the touchpad. Currently, it appears that although GNOME can lock the touchpad by pressing this button, it cannot unlock it. If the touchpad gets locked you can run the following to unlock it:

```
$ xinput set-prop "SynPS/2 Synaptics TouchPad" "Device Enabled" 1

```

### GNOME Shell keyboard sources menu not visible

A menu showing the keyboard input sources (for example 'en' for an English keyboard layout) should be visible next to the status area containing icons for network, volume and power sources. If the keyboard sources menu is not visible, this is probably because you have configured your [Xorg](/index.php/Xorg "Xorg") keyboard layout in a way which GNOME does not recognise.

To ensure that the menu is visible, remove any Xorg keyboard configuration you might have created and set the keyboard locale using [localectl](/index.php/Keyboard_configuration_in_Xorg#Using_localectl "Keyboard configuration in Xorg").

Upon running the command and then logging out, you should find that the keyboard input sources menu is visible in GDM and in the GNOME Shell desktop. See [Input sources in GNOME](http://blogs.gnome.org/mclasen/2012/09/21/input-sources-in-gnome/) for more information.

### Mouse cursor missing

When using a separate [window manager](/index.php/Window_manager "Window manager") with *gnome-settings-daemon*, the mouse cursor may vanish. Run:

```
$ gsettings set org.gnome.settings-daemon.plugins.cursor active false

```

### No restart button in session menu when screen is locked

If [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") is installed, ensure that it is not running at startup, see [#Startup applications](#Startup_applications).

### PulseAudio system-wide causes delay in GNOME and GDM

If you are running [PulseAudio](/index.php/PulseAudio "PulseAudio") in system-wide mode, the PulseAudio 7.0 upgrade breaks [GDM](/index.php/GDM "GDM") and GNOME. See [this forum post](https://bbs.archlinux.org/viewtopic.php?id=203051) for more information.

### GNOME crashes when trying to reorder applications in the GNOME Shell Dash

The dash is the "toolbar" that appears, by default, [on the left](https://en.wikipedia.org/wiki/GNOME_Shell#Design_components "wikipedia:GNOME Shell") when you click Activities. Applications can be reordered in the dash by dragging and dropping. If this fails, and/or causes GNOME to crash, try [changing your icon theme](https://bbs.archlinux.org/viewtopic.php?id=171689).

## See also

*   [The Official Website of GNOME](http://www.gnome.org/)
*   [Extensions for GNOME-shell](https://extensions.gnome.org/)
*   [GNOME Shell Cheat Sheet](https://wiki.gnome.org/Projects/GnomeShell/CheatSheet), commands, keyboard shortcuts and other tips for using GNOME Shell.
*   Themes, icons, and backgrounds:
    *   [GNOME Art](http://art.gnome.org/)
    *   [GNOME Look](http://www.gnome-look.org/)
*   GTK/GNOME programs:
    *   [GNOME Files](http://www.gnomefiles.org/)
    *   [GNOME Project Listing](http://www.gnome.org/projects/)
*   [Customizing the GNOME Shell](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html)