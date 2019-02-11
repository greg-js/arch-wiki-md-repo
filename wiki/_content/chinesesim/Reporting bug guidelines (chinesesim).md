**翻译状态：** 本文是英文页面 [Reporting_bug_guidelines](/index.php/Reporting_bug_guidelines "Reporting bug guidelines") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-07-13，点击[这里](https://wiki.archlinux.org/index.php?title=Reporting_bug_guidelines&diff=0&oldid=433639)可以查看翻译后英文页面的改动。

Related articles

*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")
*   [Step-by-step debugging guide](/index.php/Step-by-step_debugging_guide "Step-by-step debugging guide")
*   [Debug - Getting Traces](/index.php/Debug_-_Getting_Traces "Debug - Getting Traces")

在 [Arch Linux 问题跟踪系统](https://bugs.archlinux.org/) 报告问题是 [帮助社区](/index.php/Getting_involved_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Getting involved (简体中文)") 的一种方式。然而，质量不高的问题报告却会起反作用，浪费开发者的时间。此文档将像那些愿意帮助社区的人给出有效报告问题和解决问题的指南。

参见 Simon Tatham 的 [如何有效的报告问题](http://www.chiark.greenend.org.uk/~sgtatham/bugs.html)。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 开始之前](#开始之前)
    *   [1.1 查找重复问题](#查找重复问题)
    *   [1.2 上游还是 Arch?](#上游还是_Arch?)
    *   [1.3 Bug 或者 Feature?](#Bug_或者_Feature?)
        *   [1.3.1 有些不该提交 Bug 报告的原因](#有些不该提交_Bug_报告的原因)
        *   [1.3.2 有些不是 Feature 的原因](#有些不是_Feature_的原因)
    *   [1.4 收集有用的信息](#收集有用的信息)
*   [2 新建一个 Bug 报告](#新建一个_Bug_报告)
    *   [2.1 创建账户](#创建账户)
    *   [2.2 各个项目](#各个项目)
    *   [2.3 摘要](#摘要)
    *   [2.4 严重性](#严重性)
    *   [2.5 包括相关信息](#包括相关信息)
*   [3 追踪 Bug](#追踪_Bug)
    *   [3.1 投票与监视](#投票与监视)
    *   [3.2 回答追加的问题](#回答追加的问题)
    *   [3.3 软件新版本发布时更新问题报告](#软件新版本发布时更新问题报告)
    *   [3.4 关闭已经解决的问题](#关闭已经解决的问题)
    *   [3.5 问题的状态](#问题的状态)

## 开始之前

准备详细规范的问题报告并不难，但是需要报告者付出精力。 **报告前的工作才是最重要的。** 不幸的是，很少有人花时间做好这个工作。

下面的步骤将指导您准备问题报告。

### 查找重复问题

当你遇到问题或要求一个新功能是，极有可能有人也遇到了同样的问题，产生同样的想法。一个问题报告可能已经存在。这时，不要创建重复问题，请[跟踪原有问题](#追踪_Bug)。

全面查找已有信息，包括：

*   [Arch Linux 论坛](https://bbs.archlinux.org/): 论坛通常是用户寻求帮助和分享解决方案的第一处。就算当时问题可能没有解决，各位用户追加的信息和讨论能帮助你找到正确的方向。

*   [Arch Linux Bugtracker](https://bugs.archlinux.org/) （Arch Linux Bug 回报系统）: 也许你的问题已经由其他的用户提交给了开发者。重复的问题不仅没有帮助并且会被直接关闭。试着搜索**[最近关闭的 Bug 报告](https://bugs.archlinux.org/index.php?string=&project=1&status%5B%5D=closed&closedfrom=-1+week)** 和其它正在进行中的报告。记得在高级选项中选择“搜索详细信息”和“搜索评论”，因为可能标题不一定含有你搜索的信息。

*   [Google](http://www.google.com) 或者你喜欢的搜索引擎: 试着搜索程序名称，版本和相关的错误消息（如果有的话）。

*   **上游** 论坛,邮件列表和 Bug 回报系统: 如果 Arch Linux 不是造成 Bug 的原因，这个 Bug 应该提交到上游（而不是 Arch Linux）。试着搜索最近关闭的 Bug 报告和其它正在进行中的报告，你所遇到的 Bug 可能已经在上游被修复了。

*   **其它发行版的论坛**: 自由软件社区很宏大，有想法的不只有 Archer ! 考虑一下搜索其它发行版的论坛，例如 [Gentoo Forums](http://forums.gentoo.org/), [FedoraForum.org](http://forums.fedoraforum.org/), 和 [Ubuntu Forums](http://ubuntuforums.org/)。

### 上游还是 Arch?

Arch Linux 是一个 GNU/Linux *发行版* . Arch 开发者们和 Trusted User 们负责从各处编译,打包并分发软件.**上游**意味着*来源* – 就是 Arch Linux 所分发的软件的来源.例如 FireFox 浏览器是由 Mozilla 开发的.

**如果 Arch 不是造成 Bug 的主要原因,把 Bug 报告提交到 Arch 开发者并不能解决问题.**

通过向上游提交 Bug 报告,你不只帮助到了 Arch Linux 用户和开发者,同时也是在帮助自由软件社区的其他用户们.这样其它发行版的用户也能从中获得解决方案.

如果你从上游获得了相关的信息,也许可以把它们发送到 Arch Linux Bugtracker ,这样 Arch 开发者和用户们便能从中了解一些信息.

所以 Arch Linux 负责什么?

*   [Arch Linux 计划](https://projects.archlinux.org/): [pacman](/index.php/Pacman "Pacman"), [AUR](/index.php/AUR "AUR"), [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"), Arch Linux 网站. 不知道这个包是不是 Arch 的项目? 查找项目信息 (`pacman -Qi *package_name*` 或者通过网站) 并从中寻找上游网址 .

*   **打包**: 打包包含从上游获取源代码,用相关的选项编译,确认它能在 Arch 上正确安装与运行等环节. Arch 的 打包环节不包含增加新功能或是修复 Bug ,这些是上游开发者的工作.

如果某个 Bug/Feature 不是 Arch 的原因,请把它提交给上游.另参阅 [有些不是 Bug 的原因](#有些不是_Bug_的原因).

### Bug 或者 Feature?

	bug

	某些该工作的地方没有按开发者的预期工作.

	feature

	something which software does or would do if somebody coded it.

#### 有些不该提交 Bug 报告的原因

*   你想要一个还没有的功能（这是功能请求）。
*   已经提交给上游的 Bug
*   上游已经修复但是 Arch 还没更新软件包。
*   **某个软件包过期了**，这种情况请使用 [Arch Linux 网站上的](https://archlinux.org/packages/) **标记这个包已过期** 按钮.
*   某个软件包没使用来自其它发行版或其它社区的补丁,**补丁应该提交到上游**.
*   某个软件包中的 **非核心功能** 没有启用.这种情况应该提交功能请求.
*   某个软件包没有包含 [freedesktop](http://www.freedesktop.org) 相关文件,例如 **.desktop 文件** 或是 **图标**.只有在上游提供了这些文件但软件包中没有使用的情况下才是个 Bug .如果该上游没有提供这些文件,那么应该向上游提交功能请求.

#### 有些不是 Feature 的原因

*   这是个 Bug ......
*   **某个软件包过期了**，这种情况请使用 [Arch Linux 网站上的](https://archlinux.org/packages/) **标记这个包已过期** 按钮.
*   某个软件包没使用来自其它发行版或其它社区的补丁,**补丁应该提交到上游**.

### 收集有用的信息

这是一个关于你的 Bug 报告中应该包含的信息的列表:

*   **软件包的具体版本**,类似于"最新的","今天的","[Extra]中的"这样的描述毫无意义.

*   软件包所使用的库 (可以在 PKGBUILD 中的 *depends* 中找到 ),它们可能和问题相关.如果你不知道确切的信息,那就等别人来问......

*   如果遇到了硬件问题,记得提供你的内核版本.偶尔还需要你的硬件品牌相关的信息.

*   这个功能 **是否有正常工作一次** .如果有的话,提出来什么时间停止工作的.

*   Indicate your **hardware brand** when you are having hardware related problems

*   如果有的话,提供其它 **相关的日志** 这些信息可能会帮助找到问题所在:
    *   [Systemd 日志](/index.php/Systemd_journal "Systemd journal").如果使用[syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng), `/var/log/messages` 包含内核和硬件相关问题的信息.
    *   `/var/log/Xorg.0.log` , `/var/log/Xorg.2.log` 或其他 Xorg 日志包含显示相关的问题的信息.
    *   通过 **verbose** 或是 **debug** 模式在终端运行你的程序并收集其输出 (如果有的话,请参阅你的程序提供的文档) . 对于母语不是英语的用户,你也许需要在终端中设置相应的环境变量 (例如`export LC_ALL="C"`) 以使程序以英文输出.这样更多的人便可以读懂它.例如在终端下以 `--verbose` 选项运行 *foobar*:

```
$ export LC_ALL="C"
$ foobar --verbose

```

这样改变环境变量只对当前终端生效.

如果你要提供大量的文本,例如 dmesg 的输出或是 Xorg 日志,最好把它们保存到文件中并随着 Bug 报告提供. **但是请保证提供的文件和 Bug 相关**.

*   **复现 Bug 的方法**.这很重要,因为这样可以帮助其他人测试 Bug 是否修复和寻找潜在的修复方案.

*   **堆栈跟踪** .包含程序调用过程的列表,这可以帮助定位问题的位置(特别是那些导致程序崩溃的问题).[Debug - Getting Traces#Getting the trace](/index.php/Debug_-_Getting_Traces#Getting_the_trace "Debug - Getting Traces") 包含了使用[gdb](https://www.archlinux.org/packages/?name=gdb) (The GNU Debugger) 生成堆栈跟踪的详细信息.

## 新建一个 Bug 报告

在你收集到需要的信息并且确定是个 Bug 或者功能请求以后,你就可以提交 Bug 报告或者功能请求了.

### 创建账户

首先在 [Arch 的 Bug 回报系统](https://bugs.archlinux.org/) 上注册一个账户,像 Wiki 和论坛一样简单.

只有在你跟踪的 Bug 更新以后才会收到邮件提醒,因此你不必担心收件箱会爆炸 :-)

### 各个项目

在你觉得某个 Bug 或功能请求确实和 Arch 相关以后,你应该将其放置在正确的项目里.在创建报告时从左侧选择一个正确的项目:

*   **Arch Linux** - *testing*, *core*, 或 *extra* 中的软件包的问题. 也包含 Arch Linux 的文档,网站(除了 AUR) 和安全问题.

*   **Arch User Repository (AUR)** - AUR 网站代码和服务器相关.记住并不包含访问AUR中软件包的第三方程序.

*   **Community Packages** - *community* 中的软件包 . 这并不包含 *unsupported* (AUR) 中的软件包.

*   **Pacman** - [pacman](/index.php/Pacman "Pacman") 和它关联的官方脚本和工具,例如makepkg 和 abs ,但并不包含 [AUR helpers](/index.php/AUR_helpers "AUR helpers") 这一类社区开发的软件 .

*   **Release Engineering** - 所有和发行相关的问题 (iso等......)

对于 AUR 上软件包的问题,请使用 AUR 网站上的评论功能提交给 AUR 上该软件包的维护者.

### 摘要

请编写一个简洁且有描述性的摘要,下面是一些建议:

*   **不要写成** "*pkgname* is broken after the last update" 这样的,这不光没描述性而且没人知道 Arch 中的 "after last update" 是啥时候.
*   用方括号表示软件包名称,例如 "**[*pkgname*]** 3.0.5-1 breaks copy-paste feature" .合理的命名可以帮助开发者搜索和排列报告.
*   别太长,因为太长的内容会在列表中被截断.

### 严重性

选择一个*严重性等级*不会帮助更快的修复 Bug .这只是让关键的问题易于搜索和被开发者标记.

Here is a general usage of severities: 常见的严重等级有这几种:

*   **Critical**(严重),导致系统崩溃或启动失败,可能影响到其他用户的问题.或是对外服务的安全漏洞.
*   **High**(高) - 程序的主要功能不工作,或是不那么严重的安全问题等等.
*   **Medium**(中等) - 程序的非主要功能不工作,不遵循 UNIX 规范等等.
*   **Low**(低) - 程序的可选功能(插件或是编译时选项)不工作.
*   **Very Low**(很低) - 翻译或是文档错误,偶尔会是功能请求.

### 包括相关信息

这也许是 Bug 报告中最困难的一个阶段,前面的[收集有用的信息](#收集有用的信息)一节应该包含了需要的信息;如果不知道要提供什么的话,记得"多多益善".

参见 Simon Tatham 的 [如何有效的报告问题](http://www.chiark.greenend.org.uk/~sgtatham/bugs.html)。

不过开发者可能会要求你提供更多信息,幸运的是在交谈过几次以后你应该会知道该提供哪些信息了.

短小的信息可以包含在你的报告里,长的信息请使用附件功能随附在报告里.

## 追踪 Bug

**不要认为你提交完 Bug 报告就结束了**! 开发者和其他用户可能会询问你细节或是提供一些方法.没有持续的反馈会让 Bug 报告有始无终,同时也会惹恼用户和开发者们.

### 投票与监视

你可以为同样影响到你的 Bug **vote** (投票).投票会让开发者察觉有多少人受到了这个 Bug 的影响.但是如果你遇到了同样的问题,提交相关的信息是比投票更快的解决方法.

**Watching** (监视/跟踪) 一个 Bug 很重要,你会收到关于你跟踪的 Bug 的进展的邮件.如果你提交了一个报告,请确保选中了 "Notify me whenever this task changes" (在 Task 改变时通知我) 选项.

### 回答追加的问题

其它人花时间阅读报告并尝试帮助你修复问题,你也应该尽所能向其他人提供你能做到的帮助.收不到回应不仅可能会让你的 Bug 难以修复,还会让帮助你的人失去信心.

**如果其他人需要更多信息,请尝试提供给他们.也请你尝试一下可能的解决方案。**.

开发者会关闭那些有新回复而提交 Bug 的人超过几周或是一个月没有回复的 Bug 报告。

### 软件新版本发布时更新问题报告

有时某个 Bug 已经在新版本中修复，遇到这种情况的话记得在 Bug 报告中提出来然后提交一个关闭请求.

### 关闭已经解决的问题

有些时候用户可能自己解决了自己遇到的 Bug ,遇到这种情况的话记得在 Bug 报告中提出来,**附上解决方案的参考链接**,然后提交一个关闭请求.

### 问题的状态

一个 Bug 可能有下面这些状态:

*   **Unconfirmed**(未确认) - 这是默认状态,表示还没人确认或是复现这个 Bug.

*   **New**(新的/已确认) - 表示这个 Bug 已经确认,但还没关联到相关软件的负责人.通常是因为还没确认哪个软件引发的 Bug 的缘故.

*   **Assigned**(已分配) - 这个 Bug 已经分配到与之关联的开发者.不过这不意味着只有这个开发者会帮忙解决这个 Bug .这只是表示开发者会 关注这个Bug,例如检查任何的修补,发表解决方案和在需要时关闭 Bug 报告.所以不要直接和这个被分配的开发者联系......

*   **Researching**(研究中) - 有人正在寻求解决方案. 这通常表示这个 Bug 可能呢个需要更多经验丰富的用户帮忙解决.

*   **Waiting on Response**(等待回复) 和 **Requires testing**(需要测试) - 有人提供了更多信息或是提供了一个可能的解决方法,但是需要反馈.**Watching** (监视/跟踪) 一个 Bug 很重要,因为你可能会被开发者要求提供更详细的信息.

*   **A task closure has been requested**(已提交关闭请求) - 这不是最终状态,但你也许会发现某些 Bug 报告是这样的状态.和它关联的开发者会决定是否关闭它.

*   **Closed**(已关闭) - 可能因为这不是个 Bug [有些不该提交 Bug 报告的原因](#有些不该提交_Bug_报告的原因) 或者已经被解决.

像开发者和 TU 这样的人负责管理和更新各个 Bug 的状态.