## 使用 wget 幫 Pacman 加速

*   首先，請先完整升級你的系統，並確定你有最新版本的 pacman :

```
pacman -Syu

```

*   確定你的系統內已經安裝好 wget :

```
pacman -S wget

```

*   現在讓我們來編輯 `/etc/pacman.conf` 這個設定檔。將下面一行加在 `[options]` 這一段下，或著取消 `XferCommand` 這一行的註解號 :

```
XferCommand = /usr/bin/wget -c --passive-ftp -c %u

```

*   如果一切都沒問題，儲存你剛作的修改後輸入下面這行指令來檢查 :

```
grep wget /etc/pacman.conf

```

	你應該得到如下的回覆 :

```
XferCommand = /usr/bin/wget -c --passive-ftp -c %u

```

*   現在起， pacman 將直接使用 wget 來下載所有的套件了。

如果你需要一個比 pacman 內建，功能更強大的 proxy 設定，這個技巧也非常有用。

你可以直接修改 wget 的設定檔，而不需要在每次執行 wget 時都需要在指令行下一堆選項參數。

wget 的設定檔是 /etc/wgetrc，但是這個設定檔對系統內的每個使用者都有效。如果你只想新設定只對某個特定的使用者起作用，請使用在 /etc/wgetrc 內提到的 $HOME/.wgetrc 這個檔案來儲存你的設定。