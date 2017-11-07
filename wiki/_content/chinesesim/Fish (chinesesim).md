**翻译状态：** 本文是英文页面 [Fish](/index.php/Fish "Fish") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-11-07，点击[这里](https://wiki.archlinux.org/index.php?title=Fish&diff=0&oldid=494923)可以查看翻译后英文页面的改动。

**fish**, 是 "friendly interactive shell" 的缩写, 是一个"为交互式使用而创建，用户友好的 [命令行shell](/index.php/Command-line_shell "Command-line shell")". [[1]](http://fishshell.com/docs/current/index.html)

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 网页配置接口](#.E7.BD.91.E9.A1.B5.E9.85.8D.E7.BD.AE.E6.8E.A5.E5.8F.A3)
    *   [2.2 命令补全](#.E5.91.BD.E4.BB.A4.E8.A1.A5.E5.85.A8)
*   [3 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [3.1 历史记录](#.E5.8E.86.E5.8F.B2.E8.AE.B0.E5.BD.95)
*   [4 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [4.1 不要把fish设为默认shell](#.E4.B8.8D.E8.A6.81.E6.8A.8Afish.E8.AE.BE.E4.B8.BA.E9.BB.98.E8.AE.A4shell)
        *   [4.1.1 修改.bashrc来启动fish](#.E4.BF.AE.E6.94.B9.bashrc.E6.9D.A5.E5.90.AF.E5.8A.A8fish)
        *   [4.1.2 设为默认终端模拟器shell](#.E8.AE.BE.E4.B8.BA.E9.BB.98.E8.AE.A4.E7.BB.88.E7.AB.AF.E6.A8.A1.E6.8B.9F.E5.99.A8shell)
        *   [4.1.3 设为默认终端服用器shell](#.E8.AE.BE.E4.B8.BA.E9.BB.98.E8.AE.A4.E7.BB.88.E7.AB.AF.E6.9C.8D.E7.94.A8.E5.99.A8shell)
    *   [4.2 设为默认shell(不建议)](#.E8.AE.BE.E4.B8.BA.E9.BB.98.E8.AE.A4shell.28.E4.B8.8D.E5.BB.BA.E8.AE.AE.29)
    *   [4.3 关闭问候语](#.E5.85.B3.E9.97.AD.E9.97.AE.E5.80.99.E8.AF.AD)
    *   [4.4 配置su命令默认启动fish](#.E9.85.8D.E7.BD.AEsu.E5.91.BD.E4.BB.A4.E9.BB.98.E8.AE.A4.E5.90.AF.E5.8A.A8fish)
    *   [4.5 登录fish时自动开启X](#.E7.99.BB.E5.BD.95fish.E6.97.B6.E8.87.AA.E5.8A.A8.E5.BC.80.E5.90.AFX)
    *   [4.6 使用 liquidprompt](#.E4.BD.BF.E7.94.A8_liquidprompt)
    *   [4.7 在提示中增加git 状态](#.E5.9C.A8.E6.8F.90.E7.A4.BA.E4.B8.AD.E5.A2.9E.E5.8A.A0git_.E7.8A.B6.E6.80.81)
    *   [4.8 ssh-agent 问题](#ssh-agent_.E9.97.AE.E9.A2.98)
    *   [4.9 "command not found" 钩子](#.22command_not_found.22_.E9.92.A9.E5.AD.90)
    *   [4.10 从jobs中删除进程](#.E4.BB.8Ejobs.E4.B8.AD.E5.88.A0.E9.99.A4.E8.BF.9B.E7.A8.8B)
    *   [4.11 迅速设置别名](#.E8.BF.85.E9.80.9F.E8.AE.BE.E7.BD.AE.E5.88.AB.E5.90.8D)
*   [5 另请参阅](#.E5.8F.A6.E8.AF.B7.E5.8F.82.E9.98.85)

## 安装

从官方仓库安装 [fish](https://www.archlinux.org/packages/?name=fish)包 ，也可以从AUR安装开发版的[fish-git](https://aur.archlinux.org/packages/fish-git/)。

如果想把fish设为默认的 Shell，参照[Shell#Changing your default shell](/index.php/Shell#Changing_your_default_shell "Shell")；然而，这里更推荐你不要这么做，参见 [#不要把fish设为默认shell](#.E4.B8.8D.E8.A6.81.E6.8A.8Afish.E8.AE.BE.E4.B8.BA.E9.BB.98.E8.AE.A4shell)。

安装完之后，输入 `fish` 即可进入fish。

在fish中输入 `help` 即可自动打开浏览器，显示帮助文档。推荐用户至少阅读 "Syntax overview" 这一节的内容，因为fish的语法和其它shell的不太一样。

## 配置

fish的配置脚本保存在`~/.config/fish/config.fish`，这个文件就和 `.bashrc`一样。当启动终端时，fish会执行这个文件中的脚本。

### 网页配置接口

通过下面命令即可用浏览器打开fish的配置页面。

```
fish_config

```

在浏览器中可以交互式配置提示和颜色主题， 配置会保存到个人配置文件， 你也可以在浏览器中查看自己定义的函数和命令历史。

### 命令补全

fish可以通过解析man的数据，生成自动补全规则，这些自动补全规则保存于`~/.config/fish/generated_completions/`。可以运行下面命令更新自动补齐规则。

```
fish_update_completions

```

你也可以在 `~/.config/fish/completions/` 中定义自己的自动补全规则. `/usr/share/fish/completions/` 有更多的例子。

对Arch Linux来说， *pacman*, *pacman-key*, *makepkg*, *cower*, *pbget*, *pacmatic*这些命令的自动补全规则已经在fish中内置了----fish在不同的发行版中内置了不同的命令补全规则。fish的内存管理足够智能，不会因为命令补全产生负面影响。

## 故障排除

### 历史记录

Fish does not implement history substitution (e.g. `sudo !!`), and the fish developers have said that they [do not plan to](http://fishshell.com/docs/current/faq.html#faq-history). Still, this is an essential piece of many users' workflow. Reddit user, [crossroads1112](http://www.reddit.com/u/crossroads1112), created a function that regains some of the functionality of history substitution and with another syntax. The function is on [github](https://gist.github.com/crossroads1112/77badb2c3455e23b873b) and instructions are included as comments in it. There is a [forked version](https://gist.github.com/b-/981892a65837ab0a387e) that is closer to the original syntax and allows for `command !!` if you specify the command in the helper function.

Other alternatives to regaining the `command !!` syntax can be found on [Fish' github wiki](https://github.com/fish-shell/fish-shell/wiki/Bash-Style-History-Substitution-%28%21%21-and-%21%24%29). The examples here include e.g. the `bind_bang` function which expands `!!` to the latest command in the history (this will of course make it impossible to do to bangs in a row as they will expand). Another option is the command given on [this github issue](https://github.com/fish-shell/fish-shell/issues/288#issuecomment-158704275).

## 提示与技巧

### 不要把fish设为默认shell

在Arch中，很多shell脚本都是为[Bash](/index.php/Bash "Bash")而写的，并且与fish不兼容。这里不建议把fish设为默认shell，把bash设为默认shell可以使得那些为bash而写的脚本可以正常运行，确保系统环境正常初始化，环境变量正常配置。如果你把fish设为默认的shell，很可能会在启动shell时看到报错信息。

下面是一些技巧，能够使得即使不把fish设为默认shell，也能够在登录的时候自动进入fish。

#### 修改.bashrc来启动fish

把bash设为你的默认shell，只需要在你的bash配置文件[Bash#Configuration files](/index.php/Bash#Configuration_files "Bash")（一般是`.bashrc`）的最后一行加入 `exec fish`，即可在进入bash之后自动启动fish。这种做法使得Bash可以正常的运行 `/etc/profile` 和 `/etc/profile.d`下的配置。因为*fish*替代了bash 进程，退出 *fish*也会自动退出终端。和下一个方法相比，这种做法更通用，因为它能够同时在本地和SSH远程连接时运作。

**Tip:** 如果你想进入bash而不是fish，使用命令 `bash --norc`

#### 设为默认终端模拟器shell

另外一种自动启动fish的方法是专门针对终端模拟器设置默认解释器。对大多数终端模拟器来说，只需要`-e` 选项即可完成配置修改。以gnome终端模拟器为例，修改使用fish的命令如下：

```
gnome-terminal -e fish

```

LilyTerm等轻量级的终端模拟器，不支持通过命令设置默认的解释器，这时候可以通过环境变量的方式：

```
SHELL=/usr/bin/fish lilyterm

```

你也可以通过修改终端模拟器的配置文件来完成配置。

这样，当你打开终端模拟器的时候，就会自动的进入fish。

#### 设为默认终端服用器shell

如果要为tmux设置默认的shell，只需要把下面这句话放到 `~/.tmux.conf`:

```
set-option -g default-shell "/usr/bin/fish"

```

这样只要启动*tmux*，都会自动进入fish。

### 设为默认shell(不建议)

If you decide to set fish as your default shell, you may find that you no longer have very much in your path. You can add a section to your `~/.config/fish/config.fish` file that will set your path correctly on login. This is much like `.profile` or `.bash_profile` as it is only executed for login shells.

```
if status --is-login
        set PATH $PATH /usr/bin /sbin
end

```

**Note:** This route requires you to manually add various other environment variables, such as `$MOZ_PLUGIN_PATH`. It is a huge amount of work to get a seamless experience with fish as your default shell using this method. A better idea would be [#Not setting fish as default shell](#Not_setting_fish_as_default_shell).

### 关闭问候语

默认情况下，每次启动fish，fish都会打印问候语。你可以在fish的配置文件中增加 `set fish_greeting`以关闭它。

### 配置su命令默认启动fish

当你使用"su"用户切换到其他用户的时候，默认使用的shell是Bash，但是你可以在fish的配置文件中添加一个函数覆盖默认的"su"命令，使得你在使用"su"命令切换用户的时候会自动使用fish：

```
function su
    /bin/su --shell=/usr/bin/fish $argv
end

```

### 登录fish时自动开启X

把下面配置添加到 `~/.config/fish/config.fish`，即可在你登录tty1的时候自动启动X。

```
# Start X at login
if status --is-login
    if test -z "$DISPLAY" -a $XDG_VTNR = 1
        exec startx -- -keeptty
    end
end

```

### 使用 liquidprompt

[Liquidprompt](https://github.com/nojhan/liquidprompt) is a popular "full-featured & carefully designed adaptive prompt for Bash & Zsh" and has no plans to make it compatible with fish [[2]](https://github.com/nojhan/liquidprompt/pull/230). [This project](https://github.com/wesbarnett/fish-lp) implements it for fish.

### 在提示中增加git 状态

If you would like fish to display the branch and dirty status when you are in a git directory, you can add the following to your `~/.config/fish/config.fish`:

```
# fish git prompt
set __fish_git_prompt_showdirtystate 'yes'
set __fish_git_prompt_showstashstate 'yes'
set __fish_git_prompt_showupstream 'yes'
set __fish_git_prompt_color_branch yellow

# Status Chars
set __fish_git_prompt_char_dirtystate '⚡'
set __fish_git_prompt_char_stagedstate '→'
set __fish_git_prompt_char_stashstate '↩'
set __fish_git_prompt_char_upstream_ahead '↑'
set __fish_git_prompt_char_upstream_behind '↓'

function fish_prompt
        set last_status $status
        set_color $fish_color_cwd
        printf '%s' (prompt_pwd)
        set_color normal
        printf '%s ' (__fish_git_prompt)
       set_color normal
end

```

### ssh-agent 问题

在fish中，`eval (ssh-agent)`会因为变量的设置方式而报错。一个变通的方案是使用csh风格的选项`-c`：

```
 $ eval (ssh-agent -c)

```

### "command not found" 钩子

[pkgfile](/index.php/Pkgfile "Pkgfile") 包含了一个 "未找到命令"("command not found") 钩子，但你输入一个当前系统不存在的命令，pkgfile会自动从官方仓库中搜索哪个安装包有这个命令。只要你安装了[pkgfile](/index.php/Pkgfile "Pkgfile")，这个钩子就会自动启用。

### 从jobs中删除进程

当你退出*fish*的时候，所有后台进程也会终止。为了保持一个任务即使在fish退出了之后也继续运行，需要先输入`disown`命令，再退出。举例来说，在后台启动firefox，然后退出fish，但firefox在后台继续运行：

```
 $ firefox &
 $ disown
 $ exit

```

你会发现虽然你退出了fish，但firefox没有退出。请参阅disown(1)了解更多细节。

### 迅速设置别名

如果想要快速的设置一个持久化的别名（即使重启也不会失效），可以直接在fish下输入：

```
$ alias FooAliasName "foo"
$ funcsave FooAliasName

```

这种做法会把你的别名设为fish的终端函数。如果你想看所有的函数，或者是编辑它们，你可以使用`fish_config` ，然后在**Function**标签下进行配置。

## 另请参阅

*   [http://fishshell.com/](http://fishshell.com/) - fish主页
*   [http://fishshell.com/docs/current/index.html](http://fishshell.com/docs/current/index.html) - 文档
*   [http://hyperpolyglot.org/unix-shells](http://hyperpolyglot.org/unix-shells) - Shell 语法对照表