**翻译状态：** 本文是英文页面 [IRC_channel](/index.php/IRC_channel "IRC channel") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-06-27，点击[这里](https://wiki.archlinux.org/index.php?title=IRC_channel&diff=0&oldid=439070)可以查看翻译后英文页面的改动。

相关文章

*   [ArchWiki:IRC](/index.php/ArchWiki:IRC "ArchWiki:IRC")
*   [International communities](/index.php/International_communities "International communities")
*   [phrik](/index.php/Phrik "Phrik")

## Contents

*   [1 官方频道](#官方频道)
    *   [1.1 用户名注册](#用户名注册)
    *   [1.2 频道管理员](#频道管理员)
    *   [1.3 其它频道](#其它频道)
*   [2 中文频道](#中文频道)
    *   [2.1 中文社区频道的机器人](#中文社区频道的机器人)
        *   [2.1.1 桥接机器人（用于不同 IM 间转发消息）](#桥接机器人（用于不同_IM_间转发消息）)
        *   [2.1.2 HoroBot (IRC) / @yoitsuhorobot (Telegram)](#HoroBot_(IRC)_/_@yoitsuhorobot_(Telegram))
        *   [2.1.3 Lisa (XMPP)](#Lisa_(XMPP))
        *   [2.1.4 varia (IRC)](#varia_(IRC))
        *   [2.1.5 @wheeeel_todobot (Telegram)](#@wheeeel_todobot_(Telegram))
        *   [2.1.6 @SherlockHolo_bot (Telegram)](#@SherlockHolo_bot_(Telegram))
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

中文频道的入口和规则请参阅 [Code of conduct (简体中文)](/index.php/Code_of_conduct_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Code of conduct (简体中文)")

### 中文社区频道的机器人

#### 桥接机器人（用于不同 IM 间转发消息）

*   tg2arch、tg2offtopic、tg2game、tg2bot 用于 Telegram 和 IRC 间的相互转发。
*   xmppbot 和 offbot 用于 IRC 和 XMPP 间的相互转发。

形如 `[tg2arch][JohnSmith]` 的形式表示 Telegram 后昵称为 JohnSmith 的用户发送的消息。其他侧亦然。

在 IRC 侧可以使用的命令：

*   `\last` ：返回由 Telegram 用户回复 IRC 用户的最后一条消息。

#### HoroBot (IRC) / @yoitsuhorobot (Telegram)

作者： [FiveYellowMice](https://fiveyellowmice.com/)

源代码： [https://gitlab.com/FiveYellowMice/horobot2/tree/master](https://gitlab.com/FiveYellowMice/horobot2/tree/master)

A bot used to try to become Horo, but now it has evolved. 🤷

只在 #archlinux-cn-offtopic 可用。

*   在 IRC 上，可以通过 `horo/<command>` 或 `HoroBot: /<command>` 来使用
*   在 Telegram 上，可以通过 `/<command>@yoitsuhorobot` 来使用

下列均用 `/<command>` 表示对应的指令。

*   **/status** 返回一些状态信息，例如阈值和随机发送的 Emoji 列表。
*   **/poi** [text] 返回带有所输入的文本的图片。如果没有提供文本，则返回 "Poi!"
*   **/speak** 返回一句看起来像是胡言乱语的话。

这些操作会根据不同的条件不定期自动执行。

*   当群内在一段时间内发送了一定数量的消息后，会随机发送一些 Emoji。
    *   影响发送的参数有两个，阈值（threshold）和冷却速度（cooling_speed）。可以通过 `/set_<arguement>` 命令设置。 例如将阈值设置为 300： `/set_threshold 300`
    *   要改变随机发送的 Emojis 的列表，使用 `/add_emoji` 或 `/rem_emoji` 命令。例如添加 😋 到列表： `/add_emoji 😋`
    *   当然如果汝愿意的话 `/force_send` 可以现在就随机选择一种 Emoji 来发送。

#### Lisa (XMPP)

作者：[lilydjwg](https://github.com/lilydjwg)

Lisa 的命令主要分为 3 类

1.  [直接与 Lisa 对话](#直接对话命令)(需要用 ':' 分隔内容与 Lisa 的名字) 例如: `Lisa: 北京天气`
2.  [以 '!' 为前缀的命令](#带有前缀的命令) 例如: `!aqi 北京`
3.  [直接输入命令](#直接触发的命令)  例如: `割一下`

*   如果对话不是命令列表中的内容，那么会触发 Lisa 的对话功能
*   查询天气 `Lisa: XX天气` XX 为中文城市名称，例如 `Lisa: 北京天气`
*   讲笑话 `Lisa: 笑话` 讲一个冷笑话

*   帮助命令 `!help` 发送一个 LisaHelp 的链接： [https://github.com/ZWindL/LisaHelp/blob/master/README.md](https://github.com/ZWindL/LisaHelp/blob/master/README.md)
*   查询空气质量 `!aqi { cityname|zip code }` 查询相应城市的空气质量，其中 cityname 为地名，语种任选
*   查询维基百科 `!{lang}wiki <entry>` , lang 为语种的 ISO 639-1 语言代码（目前支持英文（"en"）、中文（"zh"）和日文（"ja"））。例如查询中文维基百科名为 Arch Linux 的条目： `!zhwiki Arch Linux` 会返回对应条目的导言部分和链接。
*   查询 arch wiki `!wiki entry` 查询 arch wiki 中相应的词条，只在 #archlinux-cn 频道响应此命令
*   查询 ip 归属地 `!ip ip_addr` 返回 ip_addr 所在的粗略地理位置, 暂不支持 ipv6
*   idea generator `!idea` 无参数返回一条 [ideaGenerator](http://www.matrix67.com/ideagen/) 的话语

直接触发的命令 （不建议在 #archlinux-cn 过分使用。）

*   fortune `lisalisa` 不需要参数 ，返回一条发人深省的内容
*   讲段子 `割一下` 从糗事百科抓取一条段子，每两次抓取之间有一定的冷却时间

自动触发的命令 ：

*   网站标题 当发送的消息含有链接时会自动解析网页并发送回标题或文件类型。
*   Arch Linux CN Teeworlds Server 上下线提醒 当有人连接（或断开连接）Arch Linux CN 的 Teeworlds Server 时会发送玩家的名称到 频道，只在 #arxhlinux-cn-offtopic 生效。

#### varia (IRC)

作者：[gauge](https://github.com/renormalizable) 源代码：[https://github.com/renormalizable/ircbot](https://github.com/renormalizable/ircbot)

在频道中发送 `'help` 可以获取 varia 的命令列表，发送 `'help 命令名称` 可以获取 这个命令的用法，例如：

```
`'help google
varia: <...> is mandatory, [...] is optional, (...) also accepts multiline input
varia: google: google (query) [#max number][+offset]` 

```

> 文档待补全 #flag

#### @wheeeel_todobot (Telegram)

作者：[VOID001 a.k.a Poi&YoshinoP](https://github.com/VOID001)

源代码：[https://github.com/VOID001/todobot](https://github.com/VOID001/todobot)

A TODOBot powered by archlinux and golang, made with love by VOID Shana(a.k.a VOID001).

支持下列命令：

*   **/todo** `/todo Task content##<enroll_count>,Task content##<enroll_count>...` 添加 TODO 任务，可以批量添加，通过英文逗号","分割。 并且支持设置该 TODO 的参与人数，设置方式为: `/todo blablabla##<count>`
*   **/ping** `/ping` 检查机器人的可用性并且会通过 ["一言" API](https://hitokoto.cn/api) 返回一个动漫名句
*   **/list** `/list ["done", "all"]` OR `/list` 默认列出当前群组内所有未完成的任务，可以通过增加参数 `all`,`done` 列出所有任务，和所有完成的任务 （目前没有分页所以在任务特别多的 Chat 里会刷不出来全部任务消息 QAQ)
*   **/done** `/done <TaskID>` OR `/done` OR `/donex<TaskID>` 完成任务，如果当前用户正在该群组内 `workon` 某一个任务，则该任务会被标记为完成。 如果用户没有在该群组内 `workon` 某一个任务，则会弹出 Reply Keyboard Button 即消息回复按钮，用户可以选择任务 ID 进行完成。也可以通过 `/done <TaskID>` 的形式直接完成某一个任务， 还可以点击 `/list` 中出现的 `/donex<TaskID>` 直接完成某一个任务。
*   **/track** `/track ["on", "off"]` 设置机器人跟踪状态，当你在群组中使用机器人时，默认会追踪你的 username & display name, 追踪的信息将可能被公开展示(如 ranklist, 统计信息等)。使用 `/track off` 即可关闭追踪， 并且将 username & display name 都设置为 "HIDDEN BY USER" ， 再次输入 `/track` 或者 `/track on` 即可开启追踪 （不过 userID 是必须记录的啦，不然波特就无法工作了呢）
*   **/workon** `/workon <TaskID>` 开启摸鱼保护模式，可以通过 `/workon <TaskID>` 或者点击 `/todo` 返回结果下面的按钮 (限 Telegram)对任务开启摸鱼保护模式，进入该模式之后， 如果用户出现在含有该 bot 的群里（包括发消息，发图片等行为）， bot 会对摸鱼行为进行提醒(如果任务为 "睡觉", "休息", "sleep" 则会提醒用户去休息)， 每 30s 提醒一次，并且每条消息都会被记录为一次 "摸鱼"，无论 bot 是否提醒用户。在用户完成该任务时， 会统计用户的工作时间，以及摸鱼次数，有效工作时间等信息，其中工作时间会发送到群组内， 有效工作时间和摸鱼次数则通过私聊的形式发送给用户 **使用本功能前请至少私聊过一次 BOT**
*   **/rank** `/rank [count]` OR `/rank` 显示完成任务的排行榜，范围为全部使用该bot的用户，在排行榜中将显示用户的 display name 和 完成任务数量， 摸鱼次数，如果用户关闭了 BOT 跟踪状态的话，则 display name 显示为 "HIDDEN BY USER"
*   **/help** `/help` 显示本帮助信息
*   **/del** `/del <TaskID,TaskID...>` 用于删除任务，用法为 `/del <TaskID>,<TaskID>...`
*   **/cancel** `/cancel` 用于取消显示在用户输入框下方的键盘，目前仅有此用途

#### @SherlockHolo_bot (Telegram)

作者：[Sherlock Holo (@Sherlock_Holo)](https://github.com/Sherlock-Holo)

支持下列命令：

*   **/arch** [repository] 搜索 Arch Linux 官方仓库中的软件包，可以添加 `[repository]` 参数选择从哪个仓库中搜索。
*   **/google** 通过 Google 搜索网络，返回第一条结果的链接。

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