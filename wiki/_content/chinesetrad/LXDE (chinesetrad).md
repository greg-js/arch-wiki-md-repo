LXDE（**L**ightweight **X**11 **D**esktop **E**nviorment）是由台灣數名自由軟體開發者發展的羽量級桌面環境，LXDE的設計理念包括輕巧、實用、低相依性。

## 安裝

LXDE的設計是十分模組化的，你可以選擇你需要的套件自行安裝，一個最小的LXDE安裝需求包括：

*   [lxde-common](https://www.archlinux.org/packages/?name=lxde-common)
*   [lxsession](https://www.archlinux.org/packages/?name=lxsession)
*   [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils)
*   一個視窗管理員（Window Manager）

你也可以直接安裝[lxde](https://www.archlinux.org/groups/x86_64/lxde/)套件組︰

```
# pacman -S lxde

```

此套件組會自動安裝以下套件：

*   gpicview
*   lxappearance
*   lxde-common
*   lxde-icon-theme
*   lxlauncher
*   lxmenu-data
*   lxpanel
*   lxrandr
*   lxsession-lite
*   lxtask
*   lxterminal
*   menu-cache
*   openbox
*   pcmanfm

此外，你也需要安裝[Gamin](/index.php/Gamin "Gamin")，Gamin是一個監控檔案和目錄的工具，他不像fam需要以daemon的方式存在，如果你已經有裝了fam，請在/etc/rc.conf中將他從DAEMON中移除，關閉它然後安裝gamin：

```
# pacman -S gamin

```

你可能也會想要安裝以下輕量級的套件：

```
# pacman -S leafpad xarchiver obconf epdfview

```

## 啟動桌面環境

啟動LXDE桌面環境的方式有數種，如果你使用如[SLiM](/index.php/SLiM "SLiM")、[GDM](/index.php/GDM "GDM")和[KDM](/index.php/KDM "KDM")之類的登入管理員，請選擇Session為LXDE然後登入，如果你想從終端機介面啟動LXDE，請參閱以下指示。

如果你想使用**startx**，在你的~/.xinitrc加上：

```
# exec startlxde

```

如果你不想要使用~/.xinitrc，你可以直接在terminal上輸入（若~/.xinitrc已存在此方法無效）：

```
# xinit /usr/bin/startlxde

```

如果你想要在開機時自動執行startx，請參閱[Start X at Boot](/index.php/Start_X_at_Boot "Start X at Boot")。