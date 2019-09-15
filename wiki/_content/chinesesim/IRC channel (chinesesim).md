**翻译状态：** 本文是英文页面 [IRC_channel](/index.php/IRC_channel "IRC channel") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-06-27，点击[这里](https://wiki.archlinux.org/index.php?title=IRC_channel&diff=0&oldid=439070)可以查看翻译后英文页面的改动。

相关文章

*   [ArchWiki:IRC](/index.php/ArchWiki:IRC "ArchWiki:IRC")
*   [International communities](/index.php/International_communities "International communities")
*   [phrik](/index.php/Phrik "Phrik")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 官方频道](#官方频道)
    *   [1.1 用户名注册](#用户名注册)
    *   [1.2 频道管理员](#频道管理员)
    *   [1.3 其它频道](#其它频道)
*   [2 中文频道](#中文频道)
*   [3 其它语言的 IRC 频道](#其它语言的_IRC_频道)

## 官方频道

这篇条目介绍 Arch Linux 的[IRC](https://en.wikipedia.org/wiki/zh:IRC "wikipedia:zh:IRC") 主要支持频道 **#archlinux** , 主要的交流频道 **#archlinux-offtopic**.(都在 [Freenode](http://www.freenode.net/) 上)

**#archlinux**频道的主要话题是有关 Arch Linux 的支持和总体讨论。频道规则请查看[Code of conduct](/index.php/Code_of_conduct "Code of conduct") 和 [Code of conduct#IRC](/index.php/Code_of_conduct#IRC "Code of conduct")，常用的缩略语请参看[Arch terminology](/index.php/Arch_terminology "Arch terminology") 和 [IRC Jargon](http://leonardo.spidernet.net/Copernicus/831/mirc/tips5/jarg.html)。

你需要一个IRC客户端才能加入讨论频道。可用的IRC客户端列表请查看[List of applications/Internet#IRC clients](/index.php/List_of_applications/Internet#IRC_clients "List of applications/Internet") 和 [Wikipedia:Comparison of Internet Relay Chat clients](https://en.wikipedia.org/wiki/Comparison_of_Internet_Relay_Chat_clients 中可以使用 [[Irssi|irssi] 。

### 用户名注册

**#archlinux**和**archlinux-offtopic**当前的频道模式为`+r`和`+q $~a`。这意味着你必须通过`NickServ`的身份验证才能加入个别的频道，发送消息。做这个是为了过滤垃圾信息的骚扰。

需要使用NickServ注册，请参照[freenode FAQ](https://freenode.net/kb/answer/registration)，当连接上了*chat.freenode.net*使用`NickServ help`：

```
/query nickserv help register
/query nickserv help identify

```

如果你并没有进行用户注册和验证，你会被转到**#archlinux-unregisterd**频道。用`msg chanserv access #archlinux list`指令能得到可以帮助你的人的列表，或者加入#freenode频道，在那里提问。

**Note:**

*   如果`/query`在你的客户端不起作用，你可以试着用`/quote nickserv <command>`或`/msg nickserv <command>`。
*   有些客户端会在你通过NickServ验证之前就尝试自动加入频道， 你需要开启SASL来解决这个问题。查看你的IRC客户端文档或者在[SASL page](https://freenode.net/kb/answer/sasl)上寻找教程来实现它。

### 频道管理员

**Note:** Arch的管理员在**#archlinux**和**#archlinux-offtopic**都具有管理员身份。查看下面的列或者在freenode上用`/msg phrik listops`指令。

需要管理员的协助? 别犹豫,直接 `/query` 或者 `/msg` 吧. 截止到 2016/2/4 , 操作员有这些:

*   alad
*   amcrae
*   falconindy
*   gehidore / man
*   grawity
*   heftig
*   jelle
*   MrElendig / Mion
*   Namarrgon
*   pid1
*   tigrmesh / tigr
*   vodik
*   wonder / ioni

### 其它频道

The size of our community led to the creation of multiple IRC channels. To get a list of all channels on **[chat.freenode.net](ircs://chat.freenode.net)** that contain `archlinux` in their name, use the command `/query alis list *archlinux*`.

| Channel | Description |
| [#archlinux64](ircs://chat.freenode.net/archlinux64) | x86_64 specific discussion channel, mostly in English |
| [#archlinux-aur](ircs://chat.freenode.net/archlinux-aur) | [AUR](/index.php/AUR "AUR") general discussion |
| [#archlinux-aurweb](ircs://chat.freenode.net/archlinux-aurweb) | [aurweb](https://projects.archlinux.org/aurweb.git/) development discussion |
| [#archlinux-bugs](ircs://chat.freenode.net/archlinux-bugs) | Bug-centric discussion |
| [#archlinux-classroom](ircs://chat.freenode.net/archlinux-classroom) | A project that develops and hosts classes for the Arch Linux community. |
| [#archlinux-devops](ircs://chat.freenode.net/archlinux-devops) | Arch Linux internal infrastructure and devops discussions. |
| [#archlinux-multilib](ircs://chat.freenode.net/archlinux-multilib) | Arch Linux Multilib Project discussion and packaging |
| [#archlinux-newbie](ircs://chat.freenode.net/archlinux-newbie) | A space to learn, try new things, and ask for help without fear of ridicule. |
| [#archlinux-pacman](ircs://chat.freenode.net/archlinux-pacman) | [Pacman](/index.php/Pacman "Pacman") development and discussion |
| [#archlinux-projects](ircs://chat.freenode.net/archlinux-projects) | Projects development and discussion (mkinitcpio, abs, dbscripts, devtools, ...) |
| [#archlinux-reproducible](ircs://chat.freenode.net/archlinux-reproducible) | Discussion channel for achieving reproducible builds. |
| [#archlinux-security](ircs://chat.freenode.net/archlinux-security) | Discussion of security issues within Arch packages. |
| [#archlinux-testing](ircs://chat.freenode.net/archlinux-testing) | Discussion channel regarding the testing repositories. |
| [#archlinux-wiki](ircs://chat.freenode.net/archlinux-wiki) | Discussion about [ArchWiki](/index.php/ArchWiki "ArchWiki"), its articles and the [Arch Linux Forums](https://bbs.archlinux.org/). |
| [#archlinux-women](ircs://chat.freenode.net/archlinux-women) | Discussing gender and equality, mostly in English. |
| [#archlinux-proaudio](ircs://chat.freenode.net/archlinux-proaudio) | Discussion of [Arch Linux Pro Audio](/index.php/Professional_audio "Professional audio"). Users also in the unofficial #archaudio |

## 中文频道

中文频道的入口和规则请参阅 [#archlinux-cn readme](https://fars.ee/~readme.html).

## 其它语言的 IRC 频道

International discussions are available at the following channels, also located at the **[chat.freenode.net](ircs://chat.freenode.net)** IRC network, unless stated otherwise.

| Channel | Description |
| [#archlinux-za](ircs://chat.freenode.net/archlinux-za) | Discussion (Afrikaans, English) |
| [#archlinux-br](ircs://chat.freenode.net/archlinux-br) | Discussion (Brazilian) |
| [#archlinux-cn](ircs://chat.freenode.net/archlinux-cn) | Discussion (Chinese); also on **[irc.oftc.net#arch-cn](ircs://irc.oftc.net/arch-cn)** |
| [#archlinux-cr](ircs://chat.freenode.net/archlinux-cr) | Discussion (Costa Rica) |
| [#archlinux.cz](ircs://chat.freenode.net/archlinux.cz) | Discussion (Czech) |
| [#archlinux.dk](ircs://chat.freenode.net/archlinux.dk) | Discussion (Danish) |
| [#archlinux.fi](ircs://chat.freenode.net/archlinux.fi) | Discussion (Finnish) |
| [#archlinux-fr](ircs://chat.freenode.net/archlinux-fr) | Discussion (French) |
| [#archlinux-gaelic](ircs://chat.freenode.net/archlinux-gaelic) | Discussion (Gaelic) |
| [#archlinux.de](ircs://chat.freenode.net/archlinux.de) | Discussion (German) |
| [#archlinux-greece](ircs://chat.freenode.net/archlinux-greece) | Discussion (Greek) |
| [#archlinux-il](ircs://chat.freenode.net/archlinux-il) | Discussion (Hebrew) |
| [#archlinux.hu](ircs://chat.freenode.net/archlinux.hu) | Discussion (Hungarian) |
| [#archlinux-it](ircs://chat.freenode.net/archlinux-it) | Discussion (Italian); also on **[irc.azzurra.org#archlinux](irc://irc.azzurra.org/archlinux)** |
| [#archlinux-nordics](ircs://chat.freenode.net/archlinux-nordics) | Discussion (the nordics: Danish, Finnish, Norwegian and Swedish) |
| [#archlinux-kr](ircs://chat.freenode.net/archlinux-kr) | Discussion (Korean) |
| [#archlinux-ir](ircs://chat.freenode.net/archlinux-ir) | Discussion (Persian) |
| [#archlinux.org.pl](ircs://chat.freenode.net/archlinux.org.pl) | Discussion (Polish) |
| [#archlinux-pt](ircs://chat.freenode.net/archlinux-pt) | Discussion (Portuguese) |
| [#archlinux.ro](ircs://chat.freenode.net/archlinux.ro) | Discussion (Romanian) |
| [#archlinux-ru](ircs://chat.freenode.net/archlinux-ru) | Discussion (Russian); also on **[irc.mibbit.net#archlinux-ru](irc://irc.mibbit.net/archlinux-ru)** |
| [#archlinux-rs](ircs://chat.freenode.net/archlinux-rs) | Discussion (Serbian) |
| [#archlinux-es](ircs://chat.freenode.net/archlinux-es) | Discussion (Spanish) |
| [#archlinux.se](ircs://chat.freenode.net/archlinux.se) | Discussion (Swedish) |
| [#archlinux-tr](ircs://chat.freenode.net/archlinux-tr) | Discussion (Turkish) |
| [#archlinux-ve](ircs://chat.freenode.net/archlinux-ve) | Discussion (Venezuela) |
| [#archlinuxvn](ircs://chat.freenode.net/archlinuxvn) | Discussion (Vietnamese, Tiếng Việt) |