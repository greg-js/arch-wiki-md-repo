## Contents

*   [1 简介](#.E7.AE.80.E4.BB.8B)
*   [2 手动连接](#.E6.89.8B.E5.8A.A8.E8.BF.9E.E6.8E.A5)
*   [3 自动连接](#.E8.87.AA.E5.8A.A8.E8.BF.9E.E6.8E.A5)
*   [4 操作](#.E6.93.8D.E4.BD.9C)
*   [5 命令](#.E5.91.BD.E4.BB.A4)
*   [6 技巧](#.E6.8A.80.E5.B7.A7)
    *   [6.1 保存聊天记录](#.E4.BF.9D.E5.AD.98.E8.81.8A.E5.A4.A9.E8.AE.B0.E5.BD.95)
    *   [6.2 屏蔽进入/退出房间等提示](#.E5.B1.8F.E8.94.BD.E8.BF.9B.E5.85.A5.2F.E9.80.80.E5.87.BA.E6.88.BF.E9.97.B4.E7.AD.89.E6.8F.90.E7.A4.BA)
*   [7 更多内容](#.E6.9B.B4.E5.A4.9A.E5.86.85.E5.AE.B9)

## 简介

[Irssi](http://www.irssi.org/)是一个ncurse界面的控制台irc程序。

*   安装irssi

 `# pacman -S irssi` 

*   运行程序

 ` $ irssi` 

## 手动连接

*   连接服务器

```
/connect irc.freenode.net

```

*   加入頻道

```
/join #archlinux

```

## 自动连接

*   添加网络

```
/network add -nick YOURNICKNAME Freenode
/network add -nick YOURNICKNAME OFTC

```

*   添加服务器

```
/server add -auto -network Freenode irc.freenode.net
/server add -auto -network OFTC irc.oftc.net

```

*   添加想要自动加入的频道

```
/channel add -auto #archlinux Freenode
/channel add -auto #arch-cn OFTC

```

下次启动时，就会自动连接freenode和oftc，并分别加入其中的archlinux和arch-cn频道。使用Alt+数字键切换。

## 操作

*   使用Alt+数字键，可在不同频道间切换

```
`Alt`+`1`返回主界面
`Alt`+`2`返回#archlinux

```

## 命令

	/wc 

	離開頻道,返回主畫面

	/quit 

	退出

	/channel list 

	显示保存的频道

	/server list 

	显示保存的服务器

	/network list 

	显示保存的网络

## 技巧

### 保存聊天记录

```
/SET autolog ON
/SET autolog_path /var/log/irclogs/$tag/$0.log
/save

```

### 屏蔽进入/退出房间等提示

[_Disabling Join/Part messages in various Mac IRC clients_ by Clint Ecker](http://clintecker.com/disable-irc-msgs.html)

```
/ignore #archlinux QUITS JOINS
/ignore * QUITS PARTS NICKS JOINS
/save

```

## 更多内容

[_Advanced Irssi Usage_ by Sam Kleinman1](http://library.linode.com/communications/irc/advanced-irssi-print)