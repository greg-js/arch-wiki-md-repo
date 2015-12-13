# Reporting bug guidelines (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**本页面或部分需要翻译，部分内容可能已经与英文文章脱节。如果您希望贡献翻译，请访问[简体中文翻译组](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")。**

**附注:** please use the first argument of the template to provide more detailed indications.

在 [Arch Linux 问题跟踪系统](https://bugs.archlinux.org/) 报告问题是 [帮助社区](/index.php/Getting_Involved_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Getting Involved (简体中文)") 的一种方式。然而，质量不高的问题报告却会起反作用，浪费开发者的时间。此文档将像那些愿意帮助社区的人给出有效报告问题和解决问题的指南。

参见 Simon Tatham 的 [如何有效的报告问题](http://www.chiark.greenend.org.uk/~sgtatham/bugs.html)。

## Contents

*   [1 报告前](#.E6.8A.A5.E5.91.8A.E5.89.8D)
    *   [1.1 查找重复问题](#.E6.9F.A5.E6.89.BE.E9.87.8D.E5.A4.8D.E9.97.AE.E9.A2.98)
    *   [1.2 上游还是 Arch?](#.E4.B8.8A.E6.B8.B8.E8.BF.98.E6.98.AF_Arch.3F)
    *   [1.3 问题还是新功能?](#.E9.97.AE.E9.A2.98.E8.BF.98.E6.98.AF.E6.96.B0.E5.8A.9F.E8.83.BD.3F)
        *   [1.3.1 不是问题的原因](#.E4.B8.8D.E6.98.AF.E9.97.AE.E9.A2.98.E7.9A.84.E5.8E.9F.E5.9B.A0)
        *   [1.3.2 不是新功能的原因](#.E4.B8.8D.E6.98.AF.E6.96.B0.E5.8A.9F.E8.83.BD.E7.9A.84.E5.8E.9F.E5.9B.A0)
    *   [1.4 收集有用信息](#.E6.94.B6.E9.9B.86.E6.9C.89.E7.94.A8.E4.BF.A1.E6.81.AF)
*   [2 新开一个问题](#.E6.96.B0.E5.BC.80.E4.B8.80.E4.B8.AA.E9.97.AE.E9.A2.98)
    *   [2.1 创建账户](#.E5.88.9B.E5.BB.BA.E8.B4.A6.E6.88.B7)
    *   [2.2 项目和分类](#.E9.A1.B9.E7.9B.AE.E5.92.8C.E5.88.86.E7.B1.BB)
    *   [2.3 总结](#.E6.80.BB.E7.BB.93)
    *   [2.4 严重性](#.E4.B8.A5.E9.87.8D.E6.80.A7)
    *   [2.5 加入相关信息](#.E5.8A.A0.E5.85.A5.E7.9B.B8.E5.85.B3.E4.BF.A1.E6.81.AF)
*   [3 跟踪一个问题](#.E8.B7.9F.E8.B8.AA.E4.B8.80.E4.B8.AA.E9.97.AE.E9.A2.98)
    *   [3.1 投票和监视](#.E6.8A.95.E7.A5.A8.E5.92.8C.E7.9B.91.E8.A7.86)
    *   [3.2 回答更多问题](#.E5.9B.9E.E7.AD.94.E6.9B.B4.E5.A4.9A.E9.97.AE.E9.A2.98)
    *   [3.3 软件新版本发布时更新问题报告](#.E8.BD.AF.E4.BB.B6.E6.96.B0.E7.89.88.E6.9C.AC.E5.8F.91.E5.B8.83.E6.97.B6.E6.9B.B4.E6.96.B0.E9.97.AE.E9.A2.98.E6.8A.A5.E5.91.8A)
    *   [3.4 若解决则关闭](#.E8.8B.A5.E8.A7.A3.E5.86.B3.E5.88.99.E5.85.B3.E9.97.AD)
    *   [3.5 问题的状态](#.E9.97.AE.E9.A2.98.E7.9A.84.E7.8A.B6.E6.80.81)
*   [4 消灭问题日](#.E6.B6.88.E7.81.AD.E9.97.AE.E9.A2.98.E6.97.A5)

## 报告前

准备详细规范的问题报告并不难，但是需要报告者付出精力。 **报告前的工作才是最重要的。** 不幸的是，很少有人花时间做好这个工作。

下面的步骤将指导您准备问题报告。

### 查找重复问题

当你遇到问题或要求一个新功能是，极有可能有人也遇到了同样的问题，产生同样的想法。一个问题报告可能已经存在。这时，不要创建重复问题，请跟踪原有问题。

全面查找已有信息，包括：

*   [Arch Linux 论坛](https://bbs.archlinux.org/): The forums are often the first stop for users looking for help or sharing ideas. While a solution may not yet exist, additional background information and discussion can steer you in the right direction.

*   [Arch Linux 问题跟踪系统](https://bugs.archlinux.org/): Your problem may have already been reported to Arch Linux developers. Duplicate bug reports are unhelpful and promptly closed. Search both **[recently closed bugs](https://bugs.archlinux.org/index.php?string=&project=1&status%5B%5D=closed&closedfrom=-1+week)** as well as open reports. Remember to mark 'search details' and/or 'search comments' under Advanced, the bug title may not contain the text you're searching for.

*   [Google](http://www.google.com) or your favorite search engine: Search using the program's name, version, and a relevant part of the error message, if any.

*   **上游** 论坛、邮件列表和问题跟踪系统: If Arch Linux is not responsible for a bug, it should be reported upstream rather than the Arch Linux Bugtracker. Search both recently closed bugs as well as open reports. Bugs may have already been fixed in the program's development version.

*   **其他发行版的论坛**: The free software community is vast; Archers are not the only users with ideas! Consider searching the [Gentoo Forums](http://forums.gentoo.org/), [FedoraForum.org](http://forums.fedoraforum.org/), and [Ubuntu Forums](http://ubuntuforums.org/), for example.

### 上游还是 Arch?

Arch Linux is a GNU/Linux _distribution_. Arch developers and Trusted Users are responsible for compiling, packaging, and distributing software from a wide range of sources. **Upstream** refers to these _sources_ – the original authors or maintainers of software that is distributed in Arch Linux. For example, the popular Firefox web browser is developed by the Mozilla Project.

**If Arch is not responsible for a bug, the problem will not be solved by reporting the bug to Arch developers.** Responsibility for a bug is said to lie upstream when it is not caused through the distribution's porting and integration efforts.

By reporting bugs upstream, you will not only help Archers and Arch developers, but you will also help other people in the free software community as the solution will trickle down to all distributions.

Once you have reported a bug upstream or have found other relevant information from upstream, it might be helpful to post this in the Arch bug tracker, so both Arch developers and users are made aware of it.

So what is Arch Linux responsible for?

*   **Arch Linux Projects**: pacman, AUR, initscripts, Arch Websites. If you have a doubt about if the project belongs to Arch or not, display the package information (pacman -Qi foobar_package or using the website) and look at the URL.

*   **Packaging**: Packaging basically consists of fetching the source code from upstream, compiling it with relevant options, making sure that it will be correctly installed on an Arch system, and checking that the main functionality works. Packaging at Arch does not consist of adding new functionality or patches for existing bugs; this is the job of the upstream developer.

If a bug/feature is not under Arch's responsibility, report it upstream. See also [Reasons for not being a bug](/index.php/Reporting_bug_guidelines#Reasons_for_not_being_a_bug "Reporting bug guidelines").

### 问题还是新功能?

*   **问题** 是一个应该工作却未正常工作的内容。
*   **新功能** 是指有人编程之后会工作的内容。

#### 不是问题的原因

*   Something you would like a piece of software to do, which is not implemented by the upstream developers. In short : **a new feature**.
*   A bug already reported upstream.
*   A bug already fixed upstream but not in Arch because the package is not up-to-date.
*   **A package which is not-up-to-date**. Use the **Flag Package Out-of-Date** feature on [Arch's packages website](https://archlinux.org/packages/).
*   A package which does not use Fedora, Ubuntu or some other community patch. **Patches should be submitted _upstream_**.
*   A package where **non essential function** X or function Y is not activated. This is a feature request.
*   A package which does not include a **.desktop file** or **icons** or other [freedesktop](http://www.freedesktop.org) stuff. This is not a bug if such files are not included in the source tarball, and this must be requested as a feature request _upstream_. If such files are provided by _upstream_ but not used in the package then this is a bug.

#### 不是新功能的原因

*   When it is a bug ...
*   When it is not under Arch responsibility to implement the feature, ie an **upstream feature**.
*   A package is not up-to-date. Use the **Flag Package Out-of-Date** feature on [Arch's packages website](https://archlinux.org/packages/).
*   A package which does not use Fedora, Ubuntu or some other community patch. **Patches should be submitted _upstream_**.

### 收集有用信息

Here is a list of useful information that should be mentioned in your bug report :

*   **Version of the package** being used. **Always specify package version** Saying "the latest" , "todays" , or "the package in extra" have absolutely no meaning. Especially if the bug is not about to get fixed right away.

*   Version of the main libraries used by the package (available in the _depends_ variable in the PKGBUILD), when they are involved in the problem. If you do not know exactly what information to provide then wait for a bug hunter to ask you for it ...

*   Version of the kernel used if you are having hardware related problems.

*   Indicate whether or not **the functionality worked at one time or not**. If so indicate since when it stopped working.

*   Indicate your **hardware brand** when you are having hardware related problems

*   Add **relevant log information** when any is available. This can be obtained in the following places depending on the problem :
    *   /var/log/messages for kernel and hardware related issues.
    *   /var/log/Xorg.0.log or /var/log/Xorg.2.log or any Xorg like log files if video related problems (nvidia, ati, xorg ...)
    *   Run your program in a **console** and use **verbose** and/or **debug** mode if available (see your program documentation), and copy the output in a file. When running an application in a terminal make sure relevant information will be displayed in **english** so that many people can understand it. This can be done by using _export LC_ALL="c"_. Example with a software named _foobar_ from which you would like to have relevant information at runtime and provided that foobar has a --verbose option :

```
someone@somecomputer # export LC_ALL="C"
someone@somecomputer # foobar --verbose

```

This will affect only the current terminal and will stop taking effect when the terminal is closed.

If you have to paste a lot of text, like the output of dmesg, or a Xorg log, is it preferred to save it as a file on your computer and attach it to your bug report. Attaching a file rather than using a pastebin to present relevant information is preferable in general due to the fact that pastebined content may suffer by expired links or any other potential problems. **Attaching a file guarantees the provided information will always be available.**

*   **Indicate how to reproduce the bug**. This is very important, it will help people test the bug and potential patches on their own computer.

*   **The stack trace**. It is a list of calls made by the program during its execution, and helps in finding part of the program where the bug is located, especially if bug involves the program crashing. You can obtain a stack trace using gdb (The GNU Debugger) by running the program with "gdb name_of_program" and then typing "run" at the gdb prompt. When the program crashes, type "bt" at the gdb prompt to obtain the stack trace and then "quit" to exit gdb.

## 新开一个问题

When you are sure it is a bug or a feature and you gathered all useful information, then you are ready to open a bug report or feature request.

### 创建账户

You have to create an account on [Arch's bug tracker system](https://bugs.archlinux.org/). This is as easy as creating an account on a wiki or a forum and there is nothing particular to mention here. Do not be afraid of giving the email address you currently use : it will be hidden and you will receive mails only for bugs you follow.

### 项目和分类

Once you have determined your feature or bug is related to Arch and not an upstream issue, you will need to file your problem in the correct place (watch the project name in the drop down list to the left of 'Switch' button in top left corner of bug report creation page.):

*   **Arch Linux** - for packages in _testing_, _core_, or _extra_. It is also a place for documentation, websites (except AUR), and security issues.

*   **Arch User Repository (AUR)** - for the AUR website code and server issues. This does not include third party apps used to access the AUR or packages in _unsupported_.

*   **Community Packages** - for packages in _community_. It is not a place for packages in _unsupported_.

*   **Pacman** - for _pacman_ and the official scripts and tools associated with it. This includes things like makepkg and abs. It does not include community developed packages such as yaourt.

*   **Release Engineering** - intended for all release related issues (isos, installer, etc)

There is no place for reporting problems with packages in _unsupported_. The AUR provides a way to add comments to a package in _unsupported_. You should use this to report bugs to the package maintainer.

### 总结

Please write a concise and descriptive Summary.

Here is a list of recommendations:

*   **Do not** name your report "_pkgname_ is broken after the last update" - it is non-descriptive and "after last update" has no meaning in Arch.
*   Start the Summary with package name enclosed in square brackets, e.g. "**[_pkgname_]** 3.0.5-1 breaks copy-paste feature". By naming reports this way you make it much easier for developers to sort reports by package names.
*   Do not write too much text in the Summary. Excessive text will not be visible in reports list.

### 严重性

Choosing a _critical_ severity will not help to solve the bug faster. It will only make truly critical problems less visible and probably make the developer assigned to your bug a bit less open to fixing it.

Here is a general usage of severities :

*   **Critical**- System crash, severe boot failure that is likely to affect more than just you, or an exploitable security issue in either a core or outward-facing service package.
*   **High**- The main functionality of the application does not work, less critical security issues, etc.
*   **Medium**- A non-essential functionality does not work, UNIX standards not respected, etc.
*   **Low**- An optional functionality (plugin or compilation activated) does not work.
*   **Very Low**- Translation or documentation mistake. Something that really does not matter much but should be noticed for a future release.

### 加入相关信息

This is maybe one of the most difficult parts of bug reporting. You have to choose from the chapter [Gather useful information](/index.php/Reporting_bug_guidelines#Gather_useful_information "Reporting bug guidelines") which information you will add to your bug report. This will depend on which your problem is. If you do not know what the relevant pieces of information are, do not be shy : **it is better to give more information than needed than not enough**.

A good tutorial on reporting bugs can be found at [[1]](http://www.chiark.greenend.org.uk/~sgtatham/bugs.html)

However, developers or bug hunters will ask you for more information if needed. Fortunately after a few bug reports you will know what information should be given.

Short information can be inlined in your bug report, whereas **long information (logs, screenshots ...) should be attached**.

## 跟踪一个问题

**Do not think the work is done once you have reported a bug**!

Developers or other users will probably ask you for more details and give you some potential fixes to try. Without continued feedback, bugs cannot be closed and the end result is both angry users and developers.

### 投票和监视

You can **vote** for your favorite bugs. The number of votes indicates to the developers how many people are impacted by the bug. However, this is not a very effective way of getting the bug solved. Much more important would be posting any additional information you know about the bug if you were not the original reporter.

**Watching** a bug is important- you will receive an email when new comments are added or the bug status has changed. If you opened a bug verify that the _"Notify me whenever this task changes"_ checkbox is activated in order to receive such emails.

### 回答更多问题

People will take the time to look at your bug report and will try to help you. You need to continue to help them resolve your bug. Not answering to their questions will keep your bug unresolved and likely hamper enthusiasm to fix it.

**Please take the time to give people more information if requested and try the solutions proposed**.

Developers or bug hunters will close your bug if you do not answer questions after a few weeks or a month.

### 软件新版本发布时更新问题报告

Sometimes a bug is related to a given package version and is fixed in a new version. If this is the case then indicate it in the bug report comments and request a closure.

### 若解决则关闭

Sometimes people report a bug but do not notify when they have solved it on their own, leaving people searching for a solution that has already been found. Please request a closure if you found a solution and give the solution in the bug report comments.

### 问题的状态

During its life a bug goes through several states :

*   **Unconfirmed** : This is the default state. You have just reported it and nobody managed to reproduce the problem or confirmed that it is actually a bug.

*   **New** : The bug is confirmed but it has not been assigned to the developer responsible for the related software. It is usually the case when more investigation is needed to determine which software is responsible for the bug.

*   **Assigned** : The bug has been assigned to a developer responsible for the software involved in the bug. It does not mean that the developer will be the one who will fix the bug. It does not even mean that the developer will work on a solution. It just means that the developer will take care of the life cycle of the bug, including reviewing patches if any, releasing a fix and closing the bug when required. There is no point in contacting a developer directly to have a bug fixed more quickly, he/she will certainly not like it ...

*   **Researching** : Somebody is looking for a solution. This status is **rarely used at Arch** and it is better this way. The _researching_ status could make people believe they do not need to get interested in the bug report. But usually we need more than one person to fix a bug : having several experienced people on a bug helps a lot.

*   **Waiting on customer** and **Requires testing** : The one who reported a bug is asked to provide more information or to try a proposed solution, but he/she did not give a feedback yet. Those status are **rarely used at Arch** and should be used more often. However it is important that you **watch the bug** (see the [voting and watching section](/index.php/Reporting_bug_guidelines#Voting_and_Watching "Reporting bug guidelines")) as developers or bug hunters usually ask questions in the comments.

*   **A task closure has been requested** : this is not exactly a status, but you may find some bug reports with such a notification. This indicates that somebody requested a closure for the bug. A reason is added to the request most of the time. It is upon the assignee developer to decided whether he/she will accept the closure or not.

*   **Closed** : Either this is not a valid bug (see [Reasons for not being a bug](/index.php/Reporting_bug_guidelines#Reasons_for_not_being_a_bug "Reporting bug guidelines")) or a solution has been found and released.

Some people (developers, TUs ...) are responsible for dispatching the bugs and change their status.

## 消灭问题日

[Bug Squashing Day](/index.php/Bug_Squashing_Day "Bug Squashing Day")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Reporting_bug_guidelines_(简体中文)&oldid=411888](https://wiki.archlinux.org/index.php?title=Reporting_bug_guidelines_(简体中文)&oldid=411888)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [简体中文](/index.php/Category:%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87 "Category:简体中文")
*   [Arch development (简体中文)](/index.php/Category:Arch_development_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Arch development (简体中文)")