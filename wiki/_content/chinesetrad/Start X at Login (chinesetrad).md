相關文章

*   [systemd 使用者子頁面 (英)](/index.php/Systemd/User "Systemd/User")
*   [自動登入虛擬終端機 (英)](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console")
*   [顯示管理員](/index.php/Display_Manager_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Display Manager (正體中文)")
*   [無聲開機 (英)](/index.php/Silent_boot "Silent boot")
*   [Xinitrc (英)](/index.php/Xinitrc "Xinitrc")

**翻譯狀態：** 本文章是 [Start_X_at_Login](/index.php/Start_X_at_Login "Start X at Login") 的翻譯版本。最近一次的翻譯時間：2014-01-22。點擊[本連結](https://wiki.archlinux.org/index.php?title=Start_X_at_Login&diff=0&oldid=294001)查看英文頁面之後的變更。

這篇文章將解釋如何使 [X 伺服器](/index.php/X_server "X server")在登入虛擬終端機後自動啟動。利用 *startx* 指令可以達到目的，並使用 [xinitrc](/index.php/Xinitrc "Xinitrc") 調整該指令的行為，例如選擇要啟動什麼[視窗管理員](/index.php/Window_manager "Window manager")。一種替代方案是使用[顯示管理員](/index.php/Display_manager_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Display manager (正體中文)")，它會自動啟動 X 並提供圖形登入畫面。

## Shell 設定檔案

**註記:** 這種方式會在登入的 tty 上執行 X，以維持登入階段。

*   如果使用 [Bash](/index.php/Bash "Bash")，將以下內容加到 `~/.bash_profile` 的尾端。若這個檔案不存在，就複製 `/etc/skel/.bash_profile` 這個範例檔。
    如果使用 [Zsh](/index.php/Zsh "Zsh")，則改加到 `~/.zprofile`。

```
[[ -z $DISPLAY && $XDG_VTNR -eq 1 ]] && exec startx

```

**註記:**

*   您可以更改 `-eq 1` 這個比較式；比如說希望在數個虛擬終端 (VT) 上使用圖形登入，就改成 `-le 3` (vt1 到 vt3)。
*   X 必須在用來登入的 tty 上執行，才能保存 logind 作業階段。這是由預設的 `/etc/X11/xinit/xserverrc` 處理。

*   如果使用 [Fish](/index.php/Fish "Fish")，將以下內容加到 `~/.config/fish/config.fish` 的尾端。

```
# Start X at login
if status --is-login
    if test -z "$DISPLAY" -a $XDG_VTNR = 1
        exec startx
    end
end

```

## 提示與技巧

*   這個方式可以和[自動登入虛擬終端機](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console")結合。如果要這麼做，您需要為 autologin systemd 服務設定正確的相依性，確認dbus 在 `~/.xinitrc` 被讀取前已經啟動，接著才讓 pulseaudio 啟動 (參閱 [BBS#155416](https://bbs.archlinux.org/viewtopic.php?id=155416))
*   如果您希望結束 X 階段後能夠維持登入狀態，將 `exec` 移除。
*   若要將 X 作業階段的輸出重新導向到檔案，可建立[別名](/index.php/Alias "Alias")：

	 `alias startx='startx &> ~/.xlog'`