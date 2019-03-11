相關文章

*   [Backup programs](/index.php/Backup_programs "Backup programs")

## 安裝

[dropbox](https://aur.archlinux.org/packages/dropbox/) 可以從 [AUR](/index.php/Arch_User_Repository "Arch User Repository") 安裝，你也可以選擇安裝 [dropbox-experimental](https://aur.archlinux.org/packages/dropbox-experimental/)。

安裝方式可以參考如下指令：

```
# sudo yaourt -S dropbox

```

1.  安裝完後你可以從應用程式選單啟動，或是藉由終端機執行指令 `dropbox`，客戶端程式的圖示會出現在系統匣中。
2.  啟動後會彈出一個視窗，可以選擇登入已有帳號或是建立新的帳號。
3.  接著你可以看到一個歡迎訊息以及一段簡短的使用教學。
4.  按下 Finish 完成。

如果你是 [KDE](/index.php/KDE "KDE") 使用者，那麼接下來不需要多餘的動作了，因為 KDE 會在登出時自動儲存運行中的應用程式，並會在登入時自動啟動。

### 可選套件

*   如果你想要使用終端機的指令介面，可以從 [AUR](/index.php/Arch_User_Repository "Arch User Repository") 安裝 [dropbox-cli](https://aur.archlinux.org/packages/dropbox-cli/)。
*   如果想與 Nautilus 結合，可以從 AUR 安裝 [nautilus-dropbox](https://aur.archlinux.org/packages/nautilus-dropbox/)。此套件會自動啟動 Dropbox。
*   如果想與 [Thunar](/index.php/Thunar "Thunar") 結合，從 AUR 安裝 [thunar-dropbox](https://aur.archlinux.org/packages/thunar-dropbox/)。
*   而 [KDE](/index.php/KDE "KDE") 的使用者，則在 AUR 中有 KDE 的客戶端 [kfilebox](https://aur.archlinux.org/packages/kfilebox/)。

### 自動啟動 Dropbox

你可以藉由添加 `dropboxd` 至 `~/.xinitrc`（或 `autostart`，根據你的設定）來自動啟動 Dropbox。或者你也可以添加至 [Daemon](/index.php/Daemon "Daemon") 中。