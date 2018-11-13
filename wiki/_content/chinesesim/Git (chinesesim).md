**翻译状态：** 本文是英文页面 [Git](/index.php/Git "Git") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-08-31，点击[这里](https://wiki.archlinux.org/index.php?title=Git&diff=0&oldid=536424)可以查看翻译后英文页面的改动。

相关文章

*   [Bisecting bugs with Git](/index.php/Bisecting_bugs_with_Git "Bisecting bugs with Git")
*   [Gitweb](/index.php/Gitweb "Gitweb")
*   [Cgit](/index.php/Cgit "Cgit")
*   [HTTP tunneling#Tunneling Git](/index.php/HTTP_tunneling#Tunneling_Git "HTTP tunneling")
*   [Subversion (简体中文)](/index.php/Subversion_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Subversion (简体中文)")
*   [Concurrent Versions System](/index.php/Concurrent_Versions_System "Concurrent Versions System")

> I've met people who thought that git is a front-end to GitHub. They were wrong, git is a front-end to the AUR.
> — [Linus T.](https://public-inbox.org/git/#didyoureallythinklinuswouldsaythat)

[Git](https://en.wikipedia.org/wiki/Git_(software) 是一个由 Linux 内核作者 Linus Torvalds 编写的版本控制系统（VCS），现在被用来维护 [AUR](/index.php/AUR "AUR") 软件包以及数以千计的其他项目，其中包括 Linux 内核。

## Contents

*   [1 安装](#安装)
    *   [1.1 图形化前端](#图形化前端)
*   [2 配置](#配置)
*   [3 基本用法](#基本用法)
    *   [3.1 获取一个 Git 仓库](#获取一个_Git_仓库)
    *   [3.2 记录更改](#记录更改)
        *   [3.2.1 暂存 (stage) 更改](#暂存_(stage)_更改)
        *   [3.2.2 提交 (commit) 更改](#提交_(commit)_更改)
        *   [3.2.3 选择修订版本](#选择修订版本)
        *   [3.2.4 查看更改](#查看更改)
    *   [3.3 撤销修改](#撤销修改)
    *   [3.4 分支 (branch)](#分支_(branch))
    *   [3.5 多人合作](#多人合作)
        *   [3.5.1 合并请求 (pull requests)](#合并请求_(pull_requests))
        *   [3.5.2 使用远程仓库 (remote)](#使用远程仓库_(remote))
        *   [3.5.3 向某个仓库推送 (push) 修改](#向某个仓库推送_(push)_修改)
        *   [3.5.4 处理合并 (merge)](#处理合并_(merge))
    *   [3.6 历史记录和版本记录](#历史记录和版本记录)
        *   [3.6.1 在历史记录中搜索](#在历史记录中搜索)
        *   [3.6.2 使用标签 (tag)](#使用标签_(tag))
        *   [3.6.3 重新组织 commit](#重新组织_commit)
*   [4 提示与技巧](#提示与技巧)
    *   [4.1 使用 git-config](#使用_git-config)
    *   [4.2 保持良好的礼仪](#保持良好的礼仪)
    *   [4.3 加快身份验证](#加快身份验证)
    *   [4.4 默认通讯协议](#默认通讯协议)
    *   [4.5 Bash 自动补全](#Bash_自动补全)
    *   [4.6 Git 提示符](#Git_提示符)
    *   [4.7 可视化显示](#可视化显示)
    *   [4.8 关于提交 (commit) 的小提示](#关于提交_(commit)_的小提示)
    *   [4.9 对提交 (commit) 签名](#对提交_(commit)_签名)
    *   [4.10 在非主分支上工作](#在非主分支上工作)
    *   [4.11 直接将补丁发送至邮件列表](#直接将补丁发送至邮件列表)
    *   [4.12 远程库很大时的注意事项](#远程库很大时的注意事项)
        *   [4.12.1 最简单的方式：接收整个仓库](#最简单的方式：接收整个仓库)
        *   [4.12.2 部分接收](#部分接收)
        *   [4.12.3 获取其他分支](#获取其他分支)
        *   [4.12.4 未来可能出现的其他方案](#未来可能出现的其他方案)
*   [5 Git 服务器](#Git_服务器)
    *   [5.1 SSH 协议](#SSH_协议)
    *   [5.2 Smart HTTP 协议](#Smart_HTTP_协议)
    *   [5.3 Git 协议](#Git_协议)
    *   [5.4 设置访问权限](#设置访问权限)
*   [6 参考资料](#参考资料)

## 安装

[安装](/index.php/Install "Install") [git](https://www.archlinux.org/packages/?name=git) 软件包。要使用开发版本，请安装 [git-git](https://aur.archlinux.org/packages/git-git/) 软件包。当使用 *git svn*、*git gui* 和 *gitk* 等工具时请检查可选依赖项是否安装。

### 图形化前端

参考 [git GUI Clients](https://git-scm.com/download/gui/linux)。

*   **Giggle** — 用于 git 的 GTK+ 前端。

	[https://wiki.gnome.org/Apps/giggle/](https://wiki.gnome.org/Apps/giggle/) || [giggle](https://www.archlinux.org/packages/?name=giggle)

*   **Git Cola** — 用 Python 编写的丝滑而强大的 git 图形前端。

	[https://git-cola.github.io/](https://git-cola.github.io/) || [git-cola](https://aur.archlinux.org/packages/git-cola/)

*   **Git Extensions** — 允许用户不使用命令行就可以完成 git 各项操作的图形前端。

	[https://gitextensions.github.io/](https://gitextensions.github.io/) || [gitextensions](https://aur.archlinux.org/packages/gitextensions/)

*   **gitg** — 用于查看 git 仓库的 GNOME GUI 客户端。

	[https://wiki.gnome.org/Apps/Gitg](https://wiki.gnome.org/Apps/Gitg) || [gitg](https://www.archlinux.org/packages/?name=gitg)

*   **git-gui** — Tcl/Tk 库编写的可移植 git 图形前端。

	[https://git-scm.com/docs/git-gui](https://git-scm.com/docs/git-gui) || [git](https://www.archlinux.org/packages/?name=git) + [tk](https://www.archlinux.org/packages/?name=tk)

**注意:** 要打开 *git-gui* 的拼写检查功能，请安装 [aspell](https://www.archlinux.org/packages/?name=aspell)，同时还需要与 `LC_MESSAGES` [环境变量](/index.php/Environment_variables_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Environment variables (简体中文)") 相对应的字典文件。参阅 [FS#28181](https://bugs.archlinux.org/task/28181) 和 [aspell (简体中文)](/index.php/Aspell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Aspell (简体中文)")。

*   **gitk** — Tcl/Tk 库编写的 Git 仓库查看器。

	[https://git-scm.com/docs/gitk](https://git-scm.com/docs/gitk) || [git](https://www.archlinux.org/packages/?name=git) + [tk](https://www.archlinux.org/packages/?name=tk)

*   **QGit** — 可图形化地按照不同开发分支显示修订历史记录、查阅补丁内容、查看被修改文件的 Git GUI 查看器。

	[https://github.com/tibirna/qgit](https://github.com/tibirna/qgit) || [qgit](https://www.archlinux.org/packages/?name=qgit)

*   **[RabbitVCS](https://en.wikipedia.org/wiki/RabbitVCS "wikipedia:RabbitVCS")** — 一组图形化工具，用于轻松、直接地访问您使用的版本控制系统。

	[http://rabbitvcs.org/](http://rabbitvcs.org/) || [rabbitvcs](https://aur.archlinux.org/packages/rabbitvcs/)

*   **Tig** — 基于 ncurses 的 git 字符模式前端。

	[https://jonas.github.io/tig/](https://jonas.github.io/tig/) || [tig](https://www.archlinux.org/packages/?name=tig)

*   **ungit** — 在不牺牲 git 各种功能的情况下使其变得更加友好。

	[https://github.com/FredrikNoren/ungit](https://github.com/FredrikNoren/ungit) || [nodejs-ungit](https://aur.archlinux.org/packages/nodejs-ungit/)

## 配置

你至少需要设置好姓名和邮箱之后才能开始使用 Git：

```
$ git config --global user.name  "*John Doe*"
$ git config --global user.email "*johndoe@example.com*"

```

参阅 [起步 - 初次运行 Git 前的配置](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%88%9D%E6%AC%A1%E8%BF%90%E8%A1%8C-Git-%E5%89%8D%E7%9A%84%E9%85%8D%E7%BD%AE)。

更多设置选项可参阅 [#提示与技巧](#提示与技巧)。

## 基本用法

一个 Git 版本库包含在一个名为 `.git` 的目录内，该目录包含了修订历史以及其他元数据。版本库所跟踪的目录（默认为父目录）称为工作目录。在工作树进行的更改在被提交 (commit) 前需要先暂存 (stage) 起来。Git 还可以让你恢复以前提交的工作树文件。

参阅 [起步 - Git 基础](https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-Git-%E5%9F%BA%E7%A1%80)。

### 获取一个 Git 仓库

*   初始化一个版本库

	`git init`，参阅 [git-init(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-init.1)

*   克隆 (clone) 一个现有的版本库

	`git clone *repository*`，参阅 [git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1)

### 记录更改

Git 管理的项目存在一个暂存区 (staging area)，即 git 目录中的 `index` 文件，其中保存了即将包含在你下一次提交中的文件更改。要将某个修改过的文件记录下来，首先需要将修改后的文件添加到 index（暂存它），然后用 `git commit` 命令将当前的 index 保存为一次新的提交。

#### 暂存 (stage) 更改

*   将工作树中的文件更改添加至 index

	`git add *pathspec*`，参阅 [git-add(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-add.1)

*   移除 index 中记录的文件更改

	`git reset *pathspec*`，参阅 [git-reset(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-reset.1)

*   显示即将提交的更改、未暂存的更改以及未被 git 跟踪的文件

	`git status`，参阅 [git-status(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-status.1)

可以用 `.gitignore` 文件来让 git 忽略某些未跟踪的文件，请参阅 [gitignore(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gitignore.5)。

Git 不会跟踪文件移动。合并时的文件移动检测仅基于内容的相似性。`git mv` 命令仅仅是为了方便，它相当于：

```
$ mv -i foo bar
$ git reset -- foo
$ git add bar

```

#### 提交 (commit) 更改

`git commit` 命令将暂存区的更改保存至版本库，参阅 [git-commit(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-commit.1)。

*   `-m` – 后面跟上提交消息作为参数直接提交，而不是打开默认的文本编辑器来写提交信息后再提交
*   `-a` – 自动暂存已更改或已删除的文件（不会添加未跟踪的文件）
*   `--amend` – 重做上次提交，用于修改提交消息或修改提交的文件

**提示：** 建议经常性的提交小更改，并附上有意义的提交信息。

#### 选择修订版本

Git 提供了多种方式来指定修订版本，参阅 [gitrevisions(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gitrevisions.7) 和 [选择修订版本](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E9%80%89%E6%8B%A9%E4%BF%AE%E8%AE%A2%E7%89%88%E6%9C%AC)。

许多 Git 命令需要用修订版本作为参数。一次提交记录可以用下列任何一种方式表示：

*   某次提交的 SHA-1 哈希值（前7位通常足以唯一标识它）
*   任意提交时的标签，如分支名称或 tag 名称
*   标签 `HEAD` 总是指向当前 check out 的提交（通常是分支的头部，除非你使用 *git checkout* 跳回到历史记录中的旧提交）
*   以上任意一种表示方式加上 `~` 都可以表示之前的提交。例如，`HEAD~` 指向 `HEAD` 的前一次提交，`HEAD~5` 指向 `HEAD` 5 次前的提交。

#### 查看更改

查看不同提交间的修改处：

```
$ git diff HEAD HEAD~3

```

或者查看暂存区和工作树之间的不同：

```
$ git diff

```

查看修改历史（其中 "*-N*" 指定最近的 n 次修改）：

```
$ git log -p *(-N)*

```

### 撤销修改

*   `git reset` - 重置当前 HEAD 指针到指定状态，参阅 [git-reset(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-reset.1)

*   `git checkout` - 恢复工作树中的文件，参阅 [git-checkout(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-checkout.1)

### 分支 (branch)

Bug 修复和新功能通常在不同分支里测试。当一切就绪时它们就可以合并至默认（主）分支。

创建一个分支，其名称准确地反映了其目的：

```
$ git branch *help-section-addition*

```

列出已存在的分支：

```
$ git branch

```

切换分支：

```
$ git checkout *branch*

```

新建分支并切换至该分支：

```
$ git checkout -b *branch*

```

将一个分支合并回主分支：

```
$ git checkout master
$ git merge *branch*

```

如果不存在冲突的话，所有更改将被合并。否则 Git 将显示一条错误信息，并通过给工作树中的文件加注释来记录冲突。添加的注释可以用 `git diff` 显示。要解决冲突，必须编辑文件，删除注释，并提交最终版本。请参阅下面的 [#处理合并 (merge)](#处理合并_(merge))。

当一个分支使用完毕，可以这样删除：

```
$ git branch -d *branch*

```

### 多人合作

一个典型的 Git 工作流像这样：

1.  创建一个新仓库或克隆一个远程仓库。
2.  新建一个分支用于修改文件，然后提交这些修改。
3.  将多次提交合并在一起，这样更便于组织项目或更好地理解。
4.  把提交的分支合并回主分支。
5.  （可选）将更改推送至远程服务器。

#### 合并请求 (pull requests)

在做出并提交更改后，贡献者可以请求原作者合并更改。这被称为 *合并请求 (pull request)*。

如果用 pull：

```
$ git pull *location* master

```

*pull* 命令相当于 *fetch* 和 *merge* 命令的结合。如果存在冲突（比如原作者在同一时间段内在相同位置做了更改），那就有必要手动解决冲突。

另一种方式是，原作者可以选择想要合并的更改。通过使用 *fetch* 命令（以及带有特殊 `FETCH_HEAD` 标记的 *log* 命令），可以在决定如何处理合并请求 (pull request) 前查看该请求的内容：

```
$ git fetch *location* master
$ git log -p HEAD..FETCH_HEAD
$ git merge *location* master

```

#### 使用远程仓库 (remote)

远程 (remote) 是和本地相关联的远程仓库的别名。其实就是创建一个 *label* 来定义一个位置。这些 label 用于标识经常访问的仓库。

添加一个远程仓库：

```
$ git remote add *label* *location*

```

获取远程库里的内容：

```
$ git fetch *label*

```

显示本地主分支与远程主分支之间的差异：

```
$ git log -p master..*label*/master

```

查看当前仓库相关联的远程仓库：

```
$ git remote -v

```

当设置的远程仓库是本仓库的 fork 来源（项目的领导者），这个远程仓库会被定义为 *upstream*（上游）。

#### 向某个仓库推送 (push) 修改

从原作者处获得推送修改的权限之后，使用以下命令推送修改：

```
$ git push *location* *branch*

```

当使用 *git clone* 获得这个仓库后，git 会把仓库的原始地址记录在名为 `origin` 的变量中。

所以一次 *典型的* 推送可以这样做：

```
$ git push origin master

```

如果使用了 `-u` (`--set-upstream-to`) 选项，地址将会被记录下来，下次只要使用 `git push` 就可以了。

#### 处理合并 (merge)

可以查看 Git Book 的 [遇到冲突时的分支合并](https://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E6%96%B0%E5%BB%BA%E4%B8%8E%E5%90%88%E5%B9%B6#遇到冲突时的分支合并) 部分了解如何处理合并冲突。合并操作通常是可逆的，如果想返回合并前，可以使用 `--abort` 命令（比如 `git merge --abort` 或 `git pull --abort`）。

### 历史记录和版本记录

#### 在历史记录中搜索

`git log` 命令可以显示历史记录信息，其中包含每次提交的校验和、作者、日期，以及简略信息。*校验和* 就是一次提交对象的 "对象名称"，通常是一个 40 位的 SHA-1 哈希值。

对于具有较长信息的历史记录（其中 "*checksum*" 可以截取前几位，只要它是唯一的）：

```
$ git show (*checksum*)

```

在被跟踪的文件中搜索 *pattern*：

```
$ git grep *pattern*

```

在 `.c` 和 `.h` 文件中搜索：

```
$ git grep *pattern* -- '*.[ch]'

```

#### 使用标签 (tag)

给某次提交打标签来标记这个版本：

```
$ git tag 2.14 *checksum*

```

*Tag* 通常是用于 [发布/标记版本](https://www.drupal.org/node/1066342) 的，但它可以是任何字符串。通常使用带注释的标签，因为它们会被添加到 Git 数据库中。

标记当前的提交：

```
$ git tag -a 2.14 -m "Version 2.14"

```

列出标签：

```
$ git tag -l

```

删除某个标签：

```
$ git tag -d 2.08

```

更新远程库中的标签：

```
$ git push --tags

```

#### 重新组织 commit

在提交合并请求之前，可能需要合并/重新组织 commit。这是通过 *git rebase*（变基）`--interactive`完成的：

```
$ git rebase -i *checksum*

```

然后会打开文本编辑器，其中包含指定范围内所有提交的摘要；这种情况下会包括最新提交 (`HEAD`)，但不包括 `*checksum*` 表示的那次 commit。也可以使用数字来标记，例如用 `HEAD~3`，这会把最后三次提交变基：

```
pick d146cc7 Mountpoint test.
pick 4f47712 Explain -o option in readme.
pick 8a4d479 Rename documentation.

```

修改第一栏中的动作可以决定如何执行变基操作。可选的动作有：

*   `pick` — 原样保留每次提交（默认）。
*   `edit` — 编辑文件和/或 commit 信息。
*   `reword` — 编辑 commit 信息。
*   `squash` — 合并/折叠到先前的提交中。
*   `fixup` — 合并/折叠到先前的提交中并丢弃它们的信息。

提交会被重新排序或从历史记录中擦除（所以要非常小心）。编辑文件后，Git 将执行指定的操作；如果提示有合并问题待解决，请解决它们并使用 `git rebase --continue` 来继续，或使用 `git rebase --abort` 命令来取消操作。

**注意:** 合并多次提交的操作只能应用于本地提交，它会导致其他人共享的存储库出现问题。

## 提示与技巧

### 使用 git-config

Git 从 4 个 ini 类型的配置文件里读取配置：

*   `/etc/gitconfig` 是应用于整个系统的默认配置文件
*   `~/.gitconfig` 和 `~/.config/git/config` （自 1.7.12 起）是应用于特定用户的配置文件
*   `.git/config` 是应用于特定仓库的配置文件

这些文件可以直接编辑，但是更常用的方法是使用 *git config*，下面是一些示范。

列出当前已配置的变量：

```
$ git config {--local,--global,--system} --list

```

将默认文本编辑器从 [vim](/index.php/Vim "Vim") 改成 [nano](/index.php/Nano "Nano")：

```
$ git config --global core.editor "nano -w"

```

设置默认的推送 (push) 行为：

```
$ git config --global push.default simple

```

设置不同的 *git difftool* 工具（默认是 *meld*）：

```
$ git config --global diff.tool vimdiff

```

更多信息请参阅 [git-config(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-config.1) 和 [配置 Git](https://git-scm.com/book/zh/v2/%E8%87%AA%E5%AE%9A%E4%B9%89-Git-%E9%85%8D%E7%BD%AE-Git)。

### 保持良好的礼仪

*   当你想为一个现有的项目贡献时，请先阅读并理解这个项目的许可，因为它可能会过度限制你更改代码的权力。有些许可会在代码的所有权方面引起争议。
*   理解这个项目的社区，以及你可以融入其中的程度。要了解项目的主要方向，可以阅读所有文档甚至是代码库的 [log](#历史记录和版本记录)。
*   当发起一个合并请求，或者提交一个补丁时，保证它是小改动并且有完善的文档；这将有助于项目维护者理解你的改动，并决定是否合并这些改动或是让你再改一下。
*   如果贡献被拒绝，不要气馁，毕竟这是他们的项目。如果它很重要，请尽可能清楚和耐心地讨论这次贡献的理由，最终可能通过这种方法解决问题。

### 加快身份验证

每次向 Git 服务器推送时都要认证身份,你可能会想要避免这种麻烦。

*   如果你是用 SSH 密钥来认证的，请使用 [SSH agents](/index.php/SSH_keys_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#SSH_agents "SSH keys (简体中文)")。参阅 [Secure Shell (简体中文)#加速 SSH](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#加速_SSH "Secure Shell (简体中文)") 和 [Secure Shell (简体中文)#保持在线](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#保持在线 "Secure Shell (简体中文)")。
*   如果你是用账号和密码来认证的，在服务器支持 SSH 的情况下请切换至 [SSH keys](/index.php/SSH_keys_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SSH keys (简体中文)")， 否则请尝试 [git-credential-cache](https://git-scm.com/docs/git-credential-cache) 或 [git-credential-store](https://git-scm.com/docs/git-credential-store)。

### 默认通讯协议

如果你正在使用一个上述那种复用的 SSH 连接，让 Git 使用 SSH 可能比使用 HTTPS 更快。同时，一些服务器（比如 AUR）只允许通过 SSH 推送更改。例如，像下面这样配置可以使得 Git 通过 SSH 访问 AUR 上的任何仓库。

 `~/.gitconfig` 
```
[url "ssh://aur@aur.archlinux.org/"]
	insteadOf = https://aur.archlinux.org/
	insteadOf = http://aur.archlinux.org/
	insteadOf = git://aur.archlinux.org/

```

### Bash 自动补全

要启用 Bash 的自动补全，请在 [Bash 启动文件](/index.php/Bash#Configuration_files "Bash") 里用 source 加载 `/usr/share/git/completion/git-completion.bash` 文件。或者也可以安装 [bash-completion](https://www.archlinux.org/packages/?name=bash-completion)。

### Git 提示符

Git 包带有一个提示符脚本。要启用它，请用 source 加载 `/usr/share/git/completion/git-prompt.sh` 脚本，然后使用 `%s` 参数设置一个自定义 shell 提示符：

*   [Bash](/index.php/Bash "Bash") 用户： `PS1='[\u@\h \W$(__git_ps1 " (%s)")]\$ '`
*   [zsh](/index.php/Zsh "Zsh") 用户： `setopt PROMPT_SUBST ; PS1='[%n@%m %c$(__git_ps1 " (%s)")]\$ '`

要自动完成这项工作，请参阅 [Command-line shell#Configuration files](/index.php/Command-line_shell#Configuration_files "Command-line shell")。

当切换至一个 Git 仓库所在目录时，shell 提示符会变成所在分支名称。也可以配置提示符来显示其他信息：

<caption></caption>
| Shell variable | Information |
| GIT_PS1_SHOWDIRTYSTATE | 已暂存 (staged) 显示 **+**，未暂存 (unstaged) 显示 *****。 |
| GIT_PS1_SHOWSTASHSTATE | 已储藏 (stashed) 显示 **$**。 |
| GIT_PS1_SHOWUNTRACKEDFILES | 有未跟踪文件时显示 **%**。 |
| GIT_PS1_SHOWUPSTREAM | **<,>,<>** 分别表示落后于上游、领先于上游、偏离上游。 |

`GIT_PS1_SHOWUPSTREAM` 需要设置为 `auto` 才能使更改生效。

**注意:** 如果发生了 `$(__git_ps1)` 返回 `((unknown))` 的情况，是因为有一个 `.git` 文件夹在你当前的文件夹里面，但却不包含任何存储库，因此 Git 不认识它。这有可能发生在你把 `~/.git/config` 误认为是 Git 的配置文件而不是 `~/.gitconfig`。

你也可以使用来自 [AUR](/index.php/AUR "AUR") 的自定义 git shell 提示符软件包，例如 [bash-git-prompt](https://aur.archlinux.org/packages/bash-git-prompt/) 或 [gittify](https://aur.archlinux.org/packages/gittify/)。

### 可视化显示

要了解已经完成了多少工作：

```
$ git diff --stat

```

带有 fork 显示的 *git log*：

```
$ git log --graph --oneline --decorate

```

给图形化的 *git log* 做一个别名（使用 *git graph* 即可显示经过修饰的 log）：

```
$ git config --global alias.graph 'log --graph --oneline --decorate'

```

### 关于提交 (commit) 的小提示

重置为以前的提交（非常危险，这将会擦除所有内容并改写为特定提交）：

```
$ git reset --hard HEAD^

```

如果远程仓库的地址发生变化，可以这样更新它的位置：

```
$ git remote set-url origin git@*address*:*user*/*repo*.git

```

自动附加签名行到提交（将某个 姓名-电邮 签名添加到提交中，某些项目会要求这样做）：

```
$ git commit -s

```

自动附加签名到补丁（使用 `git format-patch *commit*` 时生效）：

```
$ git config --local format.signoff true

```

提交已更改文件的特定部分。如果有大量更改时，最好拆分成多个提交，这种情况下这个命令通常很有用：

```
$ git add -p

```

### 对提交 (commit) 签名

Git 允许使用 [GnuPG](/index.php/GnuPG_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GnuPG (简体中文)") 对提交和标签进行签名，请参见 [签署工作](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E7%AD%BE%E7%BD%B2%E5%B7%A5%E4%BD%9C)。

**注意:** 如果是借助 [pinentry](https://www.archlinux.org/packages/?name=pinentry) 来进行 GPG 签名，请确保 `export GPG_TTY=$(tty)`（或者使用 pinentry-tty），否则当 GPG 处于锁定状态时签名这一步会失败（因为它无法在 shell 提示符里询问 pin 码）。

配置 Git 使它自动对提交进行签名：

```
$ git config --global commit.gpgSign true

```

### 在非主分支上工作

偶尔项目维护人员会要求你在其他分支上完成工作。这些分支通常被称为 `devel` 或 `testing`。首先要克隆存储库。

要进入不是主分支的分支（*git clone* 只会显示主分支，但其他分支其实也是存在的，用 `git branch -a` 可以显示出来）：

```
$ git checkout -b *branch* origin/*branch*

```

然后就可以像平常一样编辑文件，但是要使得整个仓库都保持同步，下面这两个命令都要用：

```
$ git pull --all
$ git push --all

```

### 直接将补丁发送至邮件列表

如果你想直接将补丁发送至一个邮件列表，需要安装以下软件包：[perl-authen-sasl](https://www.archlinux.org/packages/?name=perl-authen-sasl)，[perl-net-smtp-ssl](https://www.archlinux.org/packages/?name=perl-net-smtp-ssl) 和 [perl-mime-tools](https://www.archlinux.org/packages/?name=perl-mime-tools)。

确保你已经配置了用户名和邮件地址，可参阅 [#配置](#配置)。

配置你的邮箱设置：

```
$ git config --global sendemail.smtpserver *smtp.example.com*
$ git config --global sendemail.smtpserverport *587*
$ git config --global sendemail.smtpencryption *tls*
$ git config --global sendemail.smtpuser *foobar@example.com*

```

现在你应该可以将补丁发送至某个邮件列表了（可参阅[OpenEmbedded:How to submit a patch to OpenEmbedded#Sending patches](http://www.openembedded.org/wiki/How_to_submit_a_patch_to_OpenEmbedded#Sending_patches)）：

```
$ git add *filename*
$ git commit -s
$ git send-email --to=*openembedded-core@lists.openembedded.org* --confirm=always -M -1

```

### 远程库很大时的注意事项

当远程库很大时该怎么办？请参考这一节。其中的示例来自于 linux kernel。

#### 最简单的方式：接收整个仓库

你可以这样接收整个仓库：

```
$ git clone [git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git](git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git)

```

下载时间会很长，而且 "git clone" 无法断点续传（截止至 2018 年 8 月），还会占用很多硬盘空间。

可以用这个命令更新仓库

```
$ git pull

```

#### 部分接收

也许你想把本地仓库的大小限制得小一点，比如只保留 v4.14 以后的代码来分离出一个 bug，那么可以这么做：

```
$ git clone --shallow-exclude v4.13   [git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git](git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git) # 这样就只会下载 v4.14 及以后的文件，v4.13 以前的不会下载。

```

也许你只需要最新的仓库快照，忽略所有的历史记录。（如果有压缩包提供且足够使用，那就下载压缩包，获取 git 仓库快照开销要大一点。）可以这样做：

```
$ git clone --depth 1 [git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git](git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git)

```

之后也可以这样获取历史提交记录：

```
$ git fetch --tags --shallow-exclude v4.1 # 获取 v4.1 之后的提交记录
$ git fetch --tags --shallow-since 2016-01-01

```

如果没有 `--tags`，那么就接收不到 tags。

#### 获取其他分支

在上面的示例中，你本地的仓库仅跟踪主线内核，即“最近开发完成”的内核。假设你想获取最近的 “LTS” 版内核，比如最新的 4.14 分支，可以这么做：

```
$ git remote set-branches --add origin linux-4.17.y
$ git fetch
$ git branch --track linux-4.17.y origin/linux-4.17.y

```

最后一行不是必须的，但你应该需要执行它。 （要获取你需要的那个分支的具体名称，没有什么通用的方法，或许可以靠 web 页面的 "ref" 链接来猜测）

如果需要 linux-4.17.y 的快照，这样做：

```
$ git checkout -b linux-4.17.y

```

或者这样做，将它解压到其他目录里：

```
$ mkdir /foo/bar/src-4.17; cd /foo/bar/src-4.17
$ git clone --no-local --depth 1 -b linux-4.17.y  ../linux-stable

```

然后像平常一样，执行 `git pull` 来更新你的快照。

#### 未来可能出现的其他方案

Git 虚拟文件系统 (Git Virtual Filesystem, GVFS) 由微软开发，允许在不克隆仓库至本地的情况下使用 git 仓库。（参阅 [this Microsoft blog](https://blogs.msdn.microsoft.com/bharry/2017/05/24/the-largest-git-repo-on-the-planet/) 或 [Wikipedia artcile](https://en.wikipedia.org/wiki/Git_Virtual_File_System "wikipedia:Git Virtual File System")。）这个功能在 Linux 暂不可用。

无论如何这个功能暂不适用于上述示例中的 Linux 内核仓库。

## Git 服务器

这一节讲述如何配置使用不同的协议连接到存储库。

### SSH 协议

要使用 SSH 协议，首先要准备一个 SSH 公钥，可以按照 [SSH keys (简体中文)](/index.php/SSH_keys_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SSH keys (简体中文)") 的指导来完成。要配置一个 SSH 服务器，请遵循 [Secure Shell (简体中文)](/index.php/Secure_Shell_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Secure Shell (简体中文)") 的指导。

当 SSH 生成了密钥之后，将 `~/.ssh/id_rsa.pub` 文件的内容粘贴至服务器上的 `~/.ssh/authorized_keys` 文件里（一行一个，同一个公钥确保在同一行）。现在 Git 仓库可以通过 SSH 来访问：

```
$ git clone *user*@*foobar.com*:*my_repository*.git

```

现在，如果你的 SSH 客户端的 `StrictHostKeyChecking` 选项设为了 `ask`（默认），你应该会收到来自 SSH 的问题，要你回答 yes/no。输入 `yes` 然后回车，你的仓库就能被取出。同时，由于通过 SSH 协议访问，你现在应该有提交权限。

要把一个已存在的仓库改成使用 SSH 访问，需要重新定义一下远程地址：

```
$ git remote set-url origin git@localhost:*my_repository*.git

```

要从非 22 端口连接，可以在每台主机的 `/etc/ssh/ssh_config` 或 `~/.ssh/config` 里配置。要为某个本地仓库设置端口（示例中用的 443 端口）：

 `.git/config` 
```
[remote "origin"]
    url = ssh://*user*@*foobar*.com:443/~*my_repository*/repo.git
```

你可以通过只允许用户执行 push 和 pull 操作来进一步提高 SSH 账户的安全性。这是通过将该账户的默认登录 shell 换成 git-shell 来实现的。在 [配置服务器](https://git-scm.com/book/zh/v2/%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%B8%8A%E7%9A%84-Git-%E9%85%8D%E7%BD%AE%E6%9C%8D%E5%8A%A1%E5%99%A8) 中对此有所描述。

### Smart HTTP 协议

通过使用 git-http 后端，Git 可以像使用 SSH 协议或 Git 协议一样高效地使用 HTTP(S) 协议。此外，它不仅可以从仓库中克隆或拉取更改，还可以通过 HTTP(S) 推送更改。

这个设置相当简单，因为你只需要安装 Apache Web 服务器（[apache](https://www.archlinux.org/packages/?name=apache)，启用 `mod_cgi`、`mod_alias` 和 `mod_env`），当然还要安装 [git](https://www.archlinux.org/packages/?name=git)。

当你正在进行基本设置时，请将以下内容添加到 Apache 配置文件中，该配置文件通常位于：

 `/etc/httpd/conf/httpd.conf` 
```
<Directory "/usr/lib/git-core*">
    Require all granted
</Directory>

SetEnv GIT_PROJECT_ROOT /srv/git
SetEnv GIT_HTTP_EXPORT_ALL
ScriptAlias /git/ /usr/lib/git-core/git-http-backend/

```

这里假设你的 Git 仓库位于 `/srv/git`，并且你想用类似 `http(s)://your_address.tld/git/your_repo.git` 的方式来访问它们。

**注意:** 请确保 Apache 对你的仓库有读写权限。

如果需要更多详细文档，请访问：

*   [https://git-scm.com/book/en/v2/Git-on-the-Server-Smart-HTTP](https://git-scm.com/book/en/v2/Git-on-the-Server-Smart-HTTP)
*   [https://git-scm.com/docs/git-http-backend](https://git-scm.com/docs/git-http-backend)

### Git 协议

**注意:** Git 协议没有加密或认证机制，且只允许读取。

[Start 并且 enable](/index.php/Start "Start") `git-daemon.socket` 这个 systemd 单元。

守护程序会带有以下选项启动：

```
ExecStart=-/usr/lib/git-core/git-daemon --inetd --export-all --base-path=/srv/git

```

位于 `/srv/git/` 目录下的仓库会被守护程序识别。客户端能以类似这样的方式连接：

```
$ git clone git://*location*/*repository*.git

```

### 设置访问权限

要限制读取和/或写入权限，可以使用常规 Unix 权限控制。更多信息请参考 [when gitolite is overkill](https://github.com/sitaramc/gitolite/blob/d74e58b5de8c78bddd29b009ba2d606f7fcb4f2d/doc/overkill.mkd)。

如果需要更加精细的访问控制，请参考 [gitolite](/index.php/Gitolite "Gitolite") 和 [gitosis](/index.php/Gitosis "Gitosis")。

## 参考资料

*   Git 手册页：[git(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git.1)
*   [Pro Git book](https://git-scm.com/book/en/)
*   来自 GitHub 的 [Git Reference](https://git.github.io/git-reference/)
*   [Git workflow: Forks, remotes, and pull requests](http://nathanhoad.net/git-workflow-forks-remotes-and-pull-requests)
*   [VideoLAN wiki article](https://wiki.videolan.org/Git)
*   [A comparison of protocols GitHubGist](https://gist.github.com/grawity/4392747)
*   [How to GitHub](https://gun.io/blog/how-to-github-fork-branch-and-pull-request)