**翻译状态：** 本文是英文页面 [IRC_channel](/index.php/IRC_channel "IRC channel") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-05-19，点击[这里](https://wiki.archlinux.org/index.php?title=IRC_channel&diff=0&oldid=435539)可以查看翻译后英文页面的改动。

**Warning:** [频道的统计信息在这](https://theos.kyriasis.com/~kyrias/stats/archlinux.html). 如果不想被记录在统计中的话,请和 [demize](/index.php/User:Kyrias "User:Kyrias") 联系.

这篇条目介绍 Arch Linux 的主要支持 [IRC](https://en.wikipedia.org/wiki/zh:IRC "wikipedia:zh:IRC") 频道 **#archlinux** , 主要交流频道 **#archlinux-offtopic**.(都在 [Freenode](http://www.freenode.net/) 上)

[IRC channels](/index.php/IRC_channels_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "IRC channels (简体中文)") 有其它官方,非官方和本地化频道的列表.

## Contents

*   [1 加入频道](#.E5.8A.A0.E5.85.A5.E9.A2.91.E9.81.93)
*   [2 #archlinux - Arch Linux 官方支持频道](#.23archlinux_-_Arch_Linux_.E5.AE.98.E6.96.B9.E6.94.AF.E6.8C.81.E9.A2.91.E9.81.93)
    *   [2.1 #archlinux 规则](#.23archlinux_.E8.A7.84.E5.88.99)
    *   [2.2 #archlinux 频道指引](#.23archlinux_.E9.A2.91.E9.81.93.E6.8C.87.E5.BC.95)
    *   [2.3 #archlinux 操作员](#.23archlinux_.E6.93.8D.E4.BD.9C.E5.91.98)
*   [3 #archlinux-offtopic](#.23archlinux-offtopic)
    *   [3.1 #archlinux-offtopic 规则](#.23archlinux-offtopic_.E8.A7.84.E5.88.99)
    *   [3.2 #archlinux-offtopic 操作员](#.23archlinux-offtopic_.E6.93.8D.E4.BD.9C.E5.91.98)
*   [4 一般信息](#.E4.B8.80.E8.88.AC.E4.BF.A1.E6.81.AF)
    *   [4.1 缩略语和行话](#.E7.BC.A9.E7.95.A5.E8.AF.AD.E5.92.8C.E8.A1.8C.E8.AF.9D)

## 加入频道

你需要一个 IRC 客户端来加入频道, [List of applications/Internet#IRC clients](/index.php/List_of_applications/Internet#IRC_clients "List of applications/Internet") 和 [Wikipedia:Comparison of Internet Relay Chat clients](https://en.wikipedia.org/wiki/Comparison_of_Internet_Relay_Chat_clients "wikipedia:Comparison of Internet Relay Chat clients") 有各种客户端的列表.为了减少垃圾信息骚扰,**#archlinux** 和 **#archlinux-offtopic** 现在只允许注册用户加入. [https://freenode.net/kb/answer/registration](https://freenode.net/kb/answer/registration) 这里] 有通过 NickServ 注册的文档.如果你不注册,你会被邀请到 #archlinux-unregistered,输入 `/msg chanserv access #archlinux list` 获得 **#archlinux** 频道的成员列表.

有些客户端会在你与 NickServ 验证之前尝试加入频道,你可以通过 SASL 来解决这一问题.查找你的 IRC 客户端的文档或者 [Freenode 上的文档来了解如何设置 SASL](https://freenode.net/kb/answer/sasl).

大多数 IRC 客户端使用下面这些命令即可连接到服务器并通过 NickServ 完成验证:

```
/connect chat.freenode.net
/msg NickServ IDENTIFY `nick` `password`
/join #archlinux

```

## #archlinux - Arch Linux 官方支持频道

这是获得 Arch Linux 支持和进行一般讨论的主要频道。

现在这个频道的状态是 {ic|+q $~a}} ,也就是只允许注册用户加入. 当你连接到 chat.freenode.net 以后,可以通过这两个命令获得通过 NickServ 完成验证的详细信息:

```
/query nickserv help register
/query nickserv help identify

```

如果你的客户端不支持 `/query`,可以尝试其它命令,例如 `/quote nickserv <command>` 或者 `/msg nickserv <command>`.

### #archlinux 规则

*   **首先遵守下列规则**

	[Freenode 网络政策](https://freenode.net/policies)

	[Freenode 频道指引](https://freenode.net/changuide)

	[#archlinux 频道指引](#.23archlinux_.E9.A2.91.E9.81.93.E6.8C.87.E5.BC.95)

*   **用户和机器人**
    *   如果你想添加一个机器人,在你这么做*之前*先和操作员联系.
    *   不允许自动回复.
*   **机器人相关**
    *   'phrik!~archbot@archlinux/bot/phrik' 是频道内唯一的机器人.
    *   尽量减少机器人的使用频率,记住如果不需要把消息输出到频道的话,你可以使用 `/query phrik` 和机器人私聊.
    *   不要利用机器人发送垃圾信息.
*   **宣传**
    *   不要这么做,除非操作员允许你这样做.
*   **内容和链接**
    *   频道的主要话题是 Arch Linux 的支持和一般讨论.
    *   也可以讨论关于硬件和软件的一般问题(前提是不会干扰正常的讨论)
    *   如果遇到没有提及的情况,操作员会去处理.

### #archlinux 频道指引

1.  频道里的主要语言是英语,如果你需要以其它语言获得帮助,[[IRC_channels_(简体中文)#本地化 IRC 频道|]] 有各种本地化频道的列表.
2.  加入频道以后先通过 `/topic` 读一下频道的 topic,topic 一般情况下包括了部分重要的信息.
3.  别想[挑起纷争](https://en.wikipedia.org/wiki/Flaming_(Internet)#Flame_war "wikipedia:Flaming (Internet)"),遇到这种情况(包括破坏和扰乱分子)应该联系[[##archlinux 操作员|]].
4.  不要刷屏,超过三行的消息请考虑使用 pastebin `program &> program-output.txt` 和 Pastebin 客户端可以简化这一操作.
5.  别滥用机器人 phrik ,想尝试某个命令或者获得命令帮助请用私聊(`/query`或 `/msg`.例如 `/query phrik help <command>`).
6.  不用问谁在或是在用和你一样的软件,直接提问就好.
7.  [在提报 bug 前先看看这个](http://www.co.kerr.tx.us/it/howtoreport.html), 如果你知道[如何巧妙的提问](http://www.catb.org/~esr/faqs/smart-questions.html),你的问题应该更容易得到回答.
8.  别依赖帮助,自己去寻找它.重复提问前先等等,大多数问题都是由其他*用户*回答的,例如你.
9.  也别害羞,如果遇到你能回答的问题，请试着给予解答,只有更多的志愿者参与回答这个频道才能蓬勃发展.
10.  你若要神助，先自助吧。记得 [在 Wiki 上搜索](/index.php/Special:Search "Special:Search"),[在论坛上搜索](https://bbs.archlinux.org/search.php),阅读 [手册页](/index.php/Man_page "Man page"),或是在 Google 上搜索,这些方法能帮助你更快的得到答案,或许也可以教会你其他的东西.
11.  如果有其他人询问关于你的问题的更多信息,记得最好总是回复他/他/它.
12.  做一个好的例子,每位用户的行为都会影响整个频道.别忘了保持你的谦逊,友好和礼貌.

### #archlinux 操作员

需要操作员的协助? 别犹豫,直接 `/query` 或者 `/msg` 吧. 截止到 2016/2/4 , 操作员有这些:

*   brain0
*   falconindy
*   grawity
*   heftig
*   jelle
*   MrElendig / Mion
*   Namarrgon
*   pid1
*   tigrmesh / tigr
*   vodik
*   wonder / ioni

## #archlinux-offtopic

### #archlinux-offtopic 规则

*   **首先遵守下列规则**

	[Freenode 网络政策](https://freenode.net/policies)

	[Freenode 频道指引](https://freenode.net/changuide)

	[#archlinux 频道指引](#.23archlinux_.E9.A2.91.E9.81.93.E6.8C.87.E5.BC.95)

*   操作员可以根据自己的意愿移除其他人,所以别犯傻.但是如果你受到了不公正的对待,提出来.

### #archlinux-offtopic 操作员

1.  archlinux 的操作员也是 #archlinux-offtopic 的操作员,[上面有列表](#.23archlinux_.E6.93.8D.E4.BD.9C.E5.91.98) ,或者通过 `/msg phrik listops` 也可以获得.

## 一般信息

### 缩略语和行话

	RTFM 

	Read The Fine Manual,读读那手册

	RTFW 

	Read The Fine Wiki,读读 wiki

	RTFB 

	Read The Fine BBS,读读论坛

	RTFN 

	Read The Fine News,读读新闻

	[{core,extra,testing, ...}] 

	通常代表某个[软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)"). 例如: "nvidia drivers are in [extra]"

	AUR 

	Arch User Community Repository,AUR (Arch 用户软件仓库)

	ABS 

	Arch Build System

	ltt 

	less than three -> '<3' -> 'love'

	TU 

	Trusted User

	BBS 

	Bulletin Board System -> 'forum' ,论坛

	AFAIK 

	As Far As I Know,据我所知......

	IIRC 

	If I Recall Correctly,如果我想的对的话

	IMO 

	In My Opinion,在我看来

	FTW 

	For The Win

	FTL 

	For The Loss

	nvm 

	never mind / forget it,别介意.

	ymmv 

	your mileage may vary

	+b / B& 

	Ban / Banned ,被封禁