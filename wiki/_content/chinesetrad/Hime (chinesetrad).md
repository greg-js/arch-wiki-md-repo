相關文章

*   [Arch Linux Localization (正體中文)](/index.php/Arch_Linux_Localization_(%E6%AD%A3%E9%AB%94%E4%B8%AD%E6%96%87) "Arch Linux Localization (正體中文)")

## Contents

*   [1 安裝](#.E5.AE.89.E8.A3.9D)
    *   [1.1 安裝其他輸入法表格](#.E5.AE.89.E8.A3.9D.E5.85.B6.E4.BB.96.E8.BC.B8.E5.85.A5.E6.B3.95.E8.A1.A8.E6.A0.BC)
*   [2 設定](#.E8.A8.AD.E5.AE.9A)
    *   [2.1 自動啟動](#.E8.87.AA.E5.8B.95.E5.95.9F.E5.8B.95)

## 安裝

只要用 [yaourt](/index.php/Yaourt "Yaourt") 可以簡單地安裝好 hime。

```
yaourt -S hime

```

### 安裝其他輸入法表格

待續

## 設定

### 自動啟動

設定 `~/.xprofile` 或者 `/etc/xprofile` (詳：[xprofile](/index.php/Xprofile "Xprofile"))或 `~/.xinitrc` (詳：[xinitrc](/index.php/Xinitrc "Xinitrc"))，來讓 hime 可以自動執行：

```
export LC_CTYPE=zh_TW.UTF-8
export XMODIFIERS=@im=hime
hime &

```