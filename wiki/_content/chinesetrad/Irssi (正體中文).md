## Contents

*   [1 簡介](#.E7.B0.A1.E4.BB.8B)
*   [2 安裝](#.E5.AE.89.E8.A3.9D)
*   [3 設定](#.E8.A8.AD.E5.AE.9A)
*   [4 安裝腳本](#.E5.AE.89.E8.A3.9D.E8.85.B3.E6.9C.AC)
*   [5 使用簡例](#.E4.BD.BF.E7.94.A8.E7.B0.A1.E4.BE.8B)
*   [6 其他資料](#.E5.85.B6.E4.BB.96.E8.B3.87.E6.96.99)

## 簡介

[irssi](http://www.irssi.org/) 是一個可模組化，基於文字模式(ncurses)的IRC客戶端。 更詳細的內容,可參考[Wikipedia:Irssi](http://zh.wikipedia.org/zh-hk/Irssi)

## 安裝

*   用root的身分:

```
# pacman -S irssi

```

## 設定

*   編輯 ~/.irssi/config 。 如果你想使用指定的設定檔來執行 irssi ,可以這樣:

```
$ irssi --config=FILE

```

*   有時侯,部分文字可能會出現亂碼，你可以在irssi下執行下列指令,以設定正確的文字編碼。

```
/set recode_autodetect_utf8 ON 
/set recode_fallback CP1252
/save

```

## 安裝腳本

*   以下是安裝文字拚寫檢查腳本
*   開啟終端程式

```
# pacman -S ispell
$ mkdir -p ~/.irssi/scripts/autorun
$ cd ~/.irssi/scripts
$ wget [http://scripts.irssi.org/scripts/spell.pl](http://scripts.irssi.org/scripts/spell.pl) .
# perl -MCPAN -e 'install Lingua::Ispell' ** # make sure your are root**
$ irssi

```

*   如果你不想使用CPAN; [http://search.cpan.org/~jdporter/Lingua-Ispell-0.07/lib/Lingua/Ispell.pm](http://search.cpan.org/~jdporter/Lingua-Ispell-0.07/lib/Lingua/Ispell.pm)
*   在irssi下執行

```
/script load spell.pl

```

*   如果執行成功,會顯示如下資訊:

```
- - Irssi: Loaded script spell
/bind meta-s /_spellcheck

```

提示: Alt + s 會檢查你輸入的文字拚法是否有錯.

如果你想腳本自動載入irssi,可以在~/.irssi/scripts/autorun建立連結

```
$ cd ~/.irssi/scripts/autorun
$ ln -s ../spell.pl .

```

## 使用簡例

*   連接到位於irc.freenode.net的#archlinux頻道
*   開啟終端

```
$ irssi

```

*   連接到irc.freenode.net

```
/connect irc.freenode.net

```

*   加入頻道

```
/join #archlinux

```

*   於不同頻道切換,以下是返回主畫面irc.freenode.net

`Alt`+`1`

*   顯示第一個頻道,剛才加入的#archlinux

`Alt`+`2`

*   離開頻道,返回主畫面

```
/wc

```

*   結束irssi

```
/quit

```

# 其他資料

*   [irssi 簡單教學](http://hsian-studio.blogspot.com/2009/03/irssi.html)
*   [用 screen + irssi 上 irc 之鄉民版教學 (含Q&A)](http://lzy-blah.blogspot.com/2007/08/screen-irssi-irc-q.html)
*   [slzzp指導 irssi 相關細節](http://notexist.wordpress.com/2006/08/23/slzzp%E6%8C%87%E5%B0%8E-irssi-%E7%9B%B8%E9%97%9C%E7%B4%B0%E7%AF%80/)
*   [設定 Irssi (英文網頁)](http://linuxtidbits.wordpress.com/2008/01/09/setting-up-irssi/)