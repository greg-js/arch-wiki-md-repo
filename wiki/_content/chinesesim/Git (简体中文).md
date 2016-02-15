[Git](http://git-scm.com/) 是一个由 Linux 内核作者 Linus Torvalds 编写的版本控制系统（VCS），现在被用来维护 Linux 内核以及数以千计的其他项目，包括 Arch 的软件包管理器 [Pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")。

在官方网站可以获得一份完整的、包含参考与教程的 [文档](http://git-scm.com/documentation)。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 在 Git 命令行下启用彩色输出](#.E5.9C.A8_Git_.E5.91.BD.E4.BB.A4.E8.A1.8C.E4.B8.8B.E5.90.AF.E7.94.A8.E5.BD.A9.E8.89.B2.E8.BE.93.E5.87.BA)
    *   [2.2 解决 Git 在命令行下中文文件名显示为数字的问题](#.E8.A7.A3.E5.86.B3_Git_.E5.9C.A8.E5.91.BD.E4.BB.A4.E8.A1.8C.E4.B8.8B.E4.B8.AD.E6.96.87.E6.96.87.E4.BB.B6.E5.90.8D.E6.98.BE.E7.A4.BA.E4.B8.BA.E6.95.B0.E5.AD.97.E7.9A.84.E9.97.AE.E9.A2.98)
*   [3 基本用法](#.E5.9F.BA.E6.9C.AC.E7.94.A8.E6.B3.95)
    *   [3.1 克隆一个版本库](#.E5.85.8B.E9.9A.86.E4.B8.80.E4.B8.AA.E7.89.88.E6.9C.AC.E5.BA.93)
    *   [3.2 提交（commit）文件到版本库](#.E6.8F.90.E4.BA.A4.EF.BC.88commit.EF.BC.89.E6.96.87.E4.BB.B6.E5.88.B0.E7.89.88.E6.9C.AC.E5.BA.93)
    *   [3.3 将改动提交（push）到公共版本库](#.E5.B0.86.E6.94.B9.E5.8A.A8.E6.8F.90.E4.BA.A4.EF.BC.88push.EF.BC.89.E5.88.B0.E5.85.AC.E5.85.B1.E7.89.88.E6.9C.AC.E5.BA.93)
    *   [3.4 从服务器公共版本库下载修改](#.E4.BB.8E.E6.9C.8D.E5.8A.A1.E5.99.A8.E5.85.AC.E5.85.B1.E7.89.88.E6.9C.AC.E5.BA.93.E4.B8.8B.E8.BD.BD.E4.BF.AE.E6.94.B9)
    *   [3.5 查看历史记录](#.E6.9F.A5.E7.9C.8B.E5.8E.86.E5.8F.B2.E8.AE.B0.E5.BD.95)
    *   [3.6 处理合并（merge）](#.E5.A4.84.E7.90.86.E5.90.88.E5.B9.B6.EF.BC.88merge.EF.BC.89)
*   [4 使用分布式版本控制系统](#.E4.BD.BF.E7.94.A8.E5.88.86.E5.B8.83.E5.BC.8F.E7.89.88.E6.9C.AC.E6.8E.A7.E5.88.B6.E7.B3.BB.E7.BB.9F)
    *   [4.1 创建一个分支](#.E5.88.9B.E5.BB.BA.E4.B8.80.E4.B8.AA.E5.88.86.E6.94.AF)
    *   [4.2 A word on commits](#A_word_on_commits)
    *   [4.3 提交为检查点](#.E6.8F.90.E4.BA.A4.E4.B8.BA.E6.A3.80.E6.9F.A5.E7.82.B9)
    *   [4.4 编辑之前的提交](#.E7.BC.96.E8.BE.91.E4.B9.8B.E5.89.8D.E7.9A.84.E6.8F.90.E4.BA.A4)
    *   [4.5 插入、重新排序和更改历史记录](#.E6.8F.92.E5.85.A5.E3.80.81.E9.87.8D.E6.96.B0.E6.8E.92.E5.BA.8F.E5.92.8C.E6.9B.B4.E6.94.B9.E5.8E.86.E5.8F.B2.E8.AE.B0.E5.BD.95)
*   [5 Git提示符](#Git.E6.8F.90.E7.A4.BA.E7.AC.A6)
*   [6 传输协议](#.E4.BC.A0.E8.BE.93.E5.8D.8F.E8.AE.AE)
    *   [6.1 智能HTTP](#.E6.99.BA.E8.83.BDHTTP)
    *   [6.2 Git SSH](#Git_SSH)
        *   [6.2.1 特定非标准端口](#.E7.89.B9.E5.AE.9A.E9.9D.9E.E6.A0.87.E5.87.86.E7.AB.AF.E5.8F.A3)
    *   [6.3 Git守护进程](#Git.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
    *   [6.4 Git版本库权限](#Git.E7.89.88.E6.9C.AC.E5.BA.93.E6.9D.83.E9.99.90)
*   [7 参见](#.E5.8F.82.E8.A7.81)

## 安装

[git](https://www.archlinux.org/packages/?name=git) 可以通过 [Pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 从 [extra] 官方源安装。如果你希望搭配其它 VCS、邮件服务器或 Git 的图形界面使用 git，请注意安装时提示的可选依赖。

如果需要 Bash 命令补完（也即按下 `Tab` 来完成你正在键入的命令），请在`~/.bashrc`文件中添加如下内容：

 `source /usr/share/git/completion/git-completion.bash` 

你也可以安装 [bash-completion](https://www.archlinux.org/packages/?name=bash-completion) 来自动为 shell 提供命令补完。

如果你想使用 Git 内建的图形界面（例如 `gitk` 或者 `git gui`），你需要安装 [tk](https://www.archlinux.org/packages/?name=tk) 软件包，否则你会遇到一个隐晦的错误信息：

 `/usr/bin/gitk: line 3: exec: wish: not found.` 

## 配置

Git 从若干 INI 格式的配置文件中读取配置信息。在每一个 git 版本库中，`.git/config` 用于指定与该版本库有关的配置选项。在 `$HOME/.gitconfig` 中的用户 ("global") 的配置文件将被用作仓库配置的备用配置。你可以直接编辑配置文件，但是更推荐的方法是使用 git-config 工具。例如，

```
$ git config --global core.editor "nano -w"

```

会在 `~/.gitconfig` 文件的 `[core]` 部分中添加 `editor = nano -w`。

[git-config 工具的 man page](http://www.kernel.org/pub/software/scm/git/docs/git-config.html) 提供了完整的选项列表。

这是一些你可能用到的常见的配置：

```
$ git config --global user.name "Firstname Lastname"
$ git config --global user.email "your_email@youremail.com"

```

### 在 Git 命令行下启用彩色输出

配置 `color.ui` 选项可以令 Git 以彩色输出信息。

```
$ git config --global color.ui true

```

### 解决 Git 在命令行下中文文件名显示为数字的问题

```
$ git config --global core.quotepath false

```

## 基本用法

### 克隆一个版本库

以下命令可以将一个 Git 版本库克隆至本地目录的新文件夹中：

```
git clone <repo location> <dir>

```

如果留空 `<dir>` 字段，就会以 Git 版本库的名称命名新文件夹，例如：

```
git clone git@github.com:torvalds/linux.git

```

可以将 GitHub 上 Linux 内核的镜像克隆至名为「linux」的文件夹中。

### 提交（commit）文件到版本库

Git 的提交过程分为两步：

1.  添加新文件、修改现有的文件（均可通过 `git add <files>` 完成), 或者删除文件（通过 `git rm` 完成）。这些修改将被存入名叫 index 的文件中。
2.  使用 `git commit` 提交修改。

Git 提交时会打开文本编辑器，填写提交信息。你可以通过 `git config` 命令修改 `core.editor` 来选择编辑器。

此外，你也可以直接用 `git commit -m <message>` 命令在提交时填写提交信息，这样就不会打开编辑器。

其它有用的技巧：

`git commit -a` lets you commit changes you have made to files already under Git control without having to take the step of adding the changes to the index. You still have to add new files with git add.

`git commit -a` 命令可以跳过添加修改的部分，但是如果创建新文件依然需要 `git add`。

`git add -p` 命令可以提交修改文件的特定部分。如果你进行了许多修改而且希望将其分多次提交的话，这一选项非常有用。

### 将改动提交（push）到公共版本库

以下命令可以将修改提交至服务器（例如 Github）：

```
git push <server name> <branch>

```

添加 `-u` 参数可以将该服务器设为当前分支（branch）提交时的默认服务器。如果你是通过上文的方法克隆的版本库，默认服务器将是你克隆的来源（别名「origin」），默认分支将是 master。也就是说如果你按照上文的方法克隆的话，提交时只要执行 `git push` 即可。如果需要的话，可以令 Git 提交至多个服务器，不过这比较复杂。下文将讲解分支（branch）。

### 从服务器公共版本库下载修改

如果你在多台电脑上工作，并且需要将本地版本库与服务器更新，可以执行：

```
git pull <server name> <branch>

```

与 push 类似，server name 与 branch 都可以根据默认来，所以只需执行 `git pull`。

Git pull 实际上是如下两个命令的简写：

1.  `git fetch`，将服务器文件复制至本地，这一分支被称作「remote」也即它是远程服务器的镜像。
2.  `git merge`，将「remote」分支的文件与本地文件合并。如果你的本地提交记录与服务器的提交记录相同，就可以直接得到服务器的最新版本。如果你的提交记录与服务器的记录不符（例如在你最后一次提交之后别人进行了提交），两份提交记录将被合并。

It is not a bad idea to get into the practice of using these two commands instead of `git pull`. This way you can check to make sure that the server contains what you would expect before merging.

分步执行两个命令而非 `git pull` 并不是坏事，这样可以确保合并之前服务器的文件与你期望的相同。

### 查看历史记录

`git log` 命令可以显示当前分支的历史记录。注意每一次提交（commit）会以一个 SHA-1 标记区分，接下来是提交者、提交日期以及提交信息。更实用的命令：

```
git log --graph --oneline --decorate

```

可以显示与 TortoiseGit 的提交记录类似的窗口，这一窗口包含了如下内容：

*   每次提交的 SHA-1 标记的前七位（足以区分不同的提交）
*   `--graph` 选项可以显示从当前分支 fork 的分支数目（如果有的话）
*   `--oneline` 选项可以在一行内显示每次提交的信息
*   `--decorate` 选项可以显示所有的提交信息（包括分支与标签）

可以通过如下命令将这一命令以 `git graph` 的别名保存：

```
git config --global alias.graph 'log --graph --oneline --decorate'

```

现在执行 `git graph` 将等价于执行 `git log --graph --oneline --decorate`。

`git graph` 与 `git log` 命令也可以带 `--all` 的参数执行，这将显示所有的分支信息，而不止当前的分支。

也可以带 `--stat` 参数执行，它可以显示每次提交时哪些文件有修改、修改了多少行。

### 处理合并（merge）

当你执行 pull、进行复原操作，或者将一个分支与另一个进行合并时会需要处理合并。与其它 VCS 类似，当 Git 无法自动处理合并时，就需要使用者进行处理。

可以查看 Git Book 的[这一部分](http://git-scm.com/book/en/Git-Branching-Basic-Branching-and-Merging#Basic-Merge-Conflicts)讲解如何处理冲突合并。

如果你需要通过合并来还原的话，可以带 `--abort` 参数运行合并相关的命令，例如 `git merge --abort`，`git pull --abort`，`git rebase --abort`)。

## 使用分布式版本控制系统

The above commands only provide the basics. The real power and convenience in Git (and other distributed version control systems) come from leveraging its local commits and fast branching. A typical Git workflow looks like this:

1.  Create and check out a branch to add a feature.
2.  Make as many commits as you would like on that branch while developing that feature.
3.  Squash, rearrange, and edit your commits until you are satisfied with the commits enough to push them to the central server and make them public.
4.  Merge your branch back into the main branch.
5.  Delete your branch, if you desire.
6.  Push your changes to the central server.

### 创建一个分支

```
git branch <branch name>

```

can be used to create a branch that will branch off the current commit. After it has been created, you should switch to it using

```
git checkout <branch name>

```

A simpler method is to do both in one step with

```
git checkout -b <branch name>

```

To see a list of branches, and which branch is currently checked out, use

```
git branch

```

### A word on commits

Many of the following commands take commits as arguments. A commit can be identified by any of the following:

*   Its 40-digit SHA-1 hash (the first 7 digits are usually sufficient to identify it uniquely)
*   Any commit label such as a branch or tag name
*   The label `HEAD` always refers to the currently checked-out commit (usually the head of the branch, unless you used `git checkout` to jump back in history to an old commit)
*   Any of the above plus `~` to refer to previous commits. For example, `HEAD~` refers to one commit before `HEAD` and `HEAD~5` refers to five commits before `HEAD`.

### 提交为检查点

In Subversion and other older, centralized version control systems, commits are permanent - once you make them, they are there on the server for everyone to see. In Git, your commits are local and you can combine, rearrange, and edit them before pushing them to the server. This gives you more flexibility and lets you use commits as checkpoints. Commit early and commit often.

### 编辑之前的提交

```
git commit --amend

```

allows you to modify the previous commit. The contents of the index will be applied to it, allowing you to add more files or changes you forgot to put in. You can also use it to edit the commit message, if you would like.

### 插入、重新排序和更改历史记录

```
git rebase -i <commit>

```

will bring up a list of all commits between `<commit>` and the present, including `HEAD` but excluding `<commit>`. This command allows you rewrite history. To the left of each commit, a command is specified. Your options are as follows:

*   The "pick" command (the default) uses that commit in the rewritten history.
*   The "reword" command lets you change a commit message without changing the commit's contents.
*   The "edit" command will cause Git to pause during the history rewrite at this commit. You can then modify it with `git commit --amend` or insert new commits.
*   The "squash" command will cause a commit to be folded into the previous one. You will be prompted to enter a message for the combined commit.
*   The "fixup" command works like squash, but discards the message of the commit being squashed instead of prompting for a new message.
*   Commits can be erased from history by deleting them from the list of commits
*   Commits can be re-ordered by re-ordering them in the list. When you are done modifying the list, Git will prompt you to resolve any resulting merge problems (after doing so, continue rebasing with `git rebase --continue`)

When you are done modifying the list, Git will perform the desired actions. If Git stops at a commit (due to merge conflicts caused by re-ordering the commits or due to the "edit" command), use `git rebase --continue` to resume. You can always back out of the rebase operation with `git rebase --abort`.

**Warning:** Only use `git rebase -i` on local commits that have not yet been pushed to anybody else. Modifying commits that are on the central server will cause merge problems for obvious reasons.

**Note:** Vim makes these rebase operations very simple since lines can be cut and pasted with few keystrokes.

## Git提示符

The Git package comes with a prompt script. To enable the prompt addition you will need to source the git-prompt.sh script and add `$(__git_ps1 " (%s)")` to you PS1 variable.

*   Copy `/usr/share/git/completion/git-prompt.sh` to your home directory (e.g. `~/.git-prompt.sh`).
*   Add the following line to your .bashrc/.zshrc:

```
source ~/.git-prompt.sh

```

*   For Bash:

```
PS1='[\u@\h \W$(__git_ps1 " (%s)")]\$ '

```

**Note:** For information about coloring your bash prompt see [Color_Bash_Prompt](/index.php/Color_Bash_Prompt "Color Bash Prompt")

*   For zsh:

```
PS1='[%n@%m %c$(__git_ps1 " (%s)")]\$ '

```

The `%s` is replaced by the current branch name. The git information is displayed only if you are navigating in a git repository. You can enable extra information by setting and exporting certain variables to a non-empty value as shown in the following table:

<caption></caption>
| Variable | Information |
| GIT_PS1_SHOWDIRTYSTATE | ***** for unstaged and **+** for staged changes |
| GIT_PS1_SHOWSTASHSTATE | **$** if something is stashed |
| GIT_PS1_SHOWUNTRACKEDFILES | **%** if there are untracked files |

## 传输协议

### 智能HTTP

Since version 1.6.6 git is able to use the HTTP(S) protocol as efficiently as SSH or Git by utilizing the git-http-backend. Furthermore it is not only possible to clone or pull from repositories, but also to push into repositories over HTTP(S).

The setup for this is rather simple as all you need to have installed is the Apache web server (with mod_cgi, mod_alias, and mod_env enabled) and of course, git:

```
# pacman -S apache git

```

Once you have your basic setup up and running, add the following to your Apache's config usually located at `/etc/httpd/conf/httpd.conf`:

```
<Directory "/usr/lib/git-core*">
    Order allow,deny
    Allow from all
</Directory>

SetEnv GIT_PROJECT_ROOT /srv/git
SetEnv GIT_HTTP_EXPORT_ALL
ScriptAlias /git/ /usr/lib/git-core/git-http-backend/

```

The above example config assumes that your git repositories are located at `/srv/git` and that you want to access them via something like http(s)://your_address.tld/git/your_repo.git. Feel free to customize this to your needs.

**Note:** Of course you have to make sure that your Apache can read and write (if you want to enable push access) on your git repositories.

For more detailed documentation, visit the following links:

*   [http://progit.org/2010/03/04/smart-http.html](http://progit.org/2010/03/04/smart-http.html)
*   [https://www.kernel.org/pub/software/scm/git/docs/v1.7.10.1/git-http-backend.html](https://www.kernel.org/pub/software/scm/git/docs/v1.7.10.1/git-http-backend.html)

### Git SSH

You first need to have a public SSH key. For that follow the guide at [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys"). To set up SSH itself, you need to follow the [SSH](/index.php/SSH "SSH") guide. This assumes you have a public SSH key now and that your SSH is working. Open your SSH key in your favorite editor (default public key name is `~/.ssh/id_rsa.pub`), and copy its content (`Ctrl+c`). Now go to your user where you have made your Git repository, since we now need to allow that SSH key to log in on that user to access the Git repository. Open `~/.ssh/authorized_keys` in your favorite editor, and paste the contents of id_rsa.pub in it. Be sure it is all on one line! That is important! It should look somewhat like this:

**Warning:** Do not copy the line below! It is an example! It will not work if you use that line!

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAAAgQCboOH6AotCh4OcwJgsB4AtXzDo9Gzhl+BAHuEvnDRHNSYIURqGN4CrP+b5Bx/iLrRFOBv58TcZz1jyJ2PaGwT74kvVOe9JCCdgw4nSMBV44cy+6cTJiv6f1tw8pHRS2H6nHC9SCSAWkMX4rpiSQ0wkhjug+GtBWOXDaotIzrFwLw== username@hostname

```

Now you can checkout your Git repository this way (change where needed. Here it is using the git username and localhost):

```
git clone git@localhost:my_repository.git

```

You should now get an SSH yes/no question. Type `yes` followed by `Enter`. Then you should have your repository checked out. Because this is with SSH, you also do have commit rights now. For that look at [Git](/index.php/Git "Git") and [Super Quick Git Guide](/index.php/Super_Quick_Git_Guide "Super Quick Git Guide").

#### 特定非标准端口

Connecting on a port other than 22 can be configured on a per-host basis in `/etc/ssh/ssh_config` or `~/.ssh/config`. To set up ports for a repository, specify the path in `.git/config` using the port number `N` and the _absolute path_ `/PATH/TO/REPO`:

```
[ssh://user@example.org:N/PATH/TO/REPO](ssh://user@example.org:N/PATH/TO/REPO)

```

Typically the repository resides in the home directory of the user which allows you to use tilde-expansion. Thus to connect on port N=443,

```
url = git@example.org:repo.git

```

becomes:

```
url = [ssh://git@example.org:443/~git/repo.git](ssh://git@example.org:443/~git/repo.git)

```

### Git守护进程

**Note:** The git daemon only allows read access. For write access see [#Git SSH](#Git_SSH).

This will allow URLs like "git clone [git://localhost/my_repository.git](git://localhost/my_repository.git)".

Edit the configuration file for git-daemon `/etc/conf.d/git-daemon.conf` (GIT_REPO is a place with your git projects), then start git-daemon with root privileges:

```
# systemctl start git-daemon@

```

To run the git-daemon every time at boot, enable the service:

```
# systemctl enable git-daemon@

```

Clients can now simply use:

```
git clone [git://localhost/my_repository.git](git://localhost/my_repository.git)

```

### Git版本库权限

To restrict read/write access, you can simply use Unix rights, see [http://sitaramc.github.com/gitolite/doc/overkill.html](http://sitaramc.github.com/gitolite/doc/overkill.html)

For a fine-grained rights access, see [gitolite](/index.php/Gitolite "Gitolite") and [gitosis](/index.php/Gitosis "Gitosis")

## 参见

*   [http://book.git-scm.com/index.html](http://book.git-scm.com/index.html)
*   [http://gitref.org/](http://gitref.org/)
*   [http://www.kernel.org/pub/software/scm/git/docs/](http://www.kernel.org/pub/software/scm/git/docs/)
*   [http://help.github.com/](http://help.github.com/)