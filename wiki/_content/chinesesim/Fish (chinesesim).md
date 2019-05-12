**翻译状态：** 本文是英文页面 [Fish](/index.php/Fish "Fish") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-05-09，点击[这里](https://wiki.archlinux.org/index.php?title=Fish&diff=0&oldid=567009)可以查看翻译后英文页面的改动。

[fish](https://fishshell.com)是“***f**riendly **i**nteractive **sh**ell*”的缩写，是一个“交互式的、对用户友好的 [命令行shell](/index.php/Command-line_shell "Command-line shell")”。

*fish*被有意设计成不完全与[POSIX](https://en.wikipedia.org/wiki/POSIX "wikipedia:POSIX")兼容。fish的作者们认为POSIX中存在一些缺陷和矛盾，并通过fish简化的或不同的语法解决这些问题。因此，即使简单的POSIX兼容的脚本也可能需要较多的修改，甚至完全重写，才能在fish中运行。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 把fish集成到系统中](#把fish集成到系统中)
    *   [2.1 把fish设为默认shell](#把fish设为默认shell)
    *   [2.2 只把fish设为交互式shell](#只把fish设为交互式shell)
        *   [2.2.1 通过.bashrc启动fish](#通过.bashrc启动fish)
        *   [2.2.2 使用终端模拟器的选项](#使用终端模拟器的选项)
        *   [2.2.3 使用终端复用器的选项](#使用终端复用器的选项)
*   [3 配置](#配置)
    *   [3.1 网页界面](#网页界面)
    *   [3.2 命令补全](#命令补全)
*   [4 提示与技巧](#提示与技巧)
    *   [4.1 命令替换](#命令替换)
    *   [4.2 串联命令](#串联命令)
    *   [4.3 关闭问候语](#关闭问候语)
    *   [4.4 配置su命令默认启动fish](#配置su命令默认启动fish)
    *   [4.5 登录fish时自动开启X](#登录fish时自动开启X)
    *   [4.6 使用 liquidprompt](#使用_liquidprompt)
    *   [4.7 在提示中增加git状态](#在提示中增加git状态)
    *   [4.8 在SSH中用彩色显示主机名](#在SSH中用彩色显示主机名)
    *   [4.9 ssh-agent 问题](#ssh-agent_问题)
    *   [4.10 "command not found" 钩子](#"command_not_found"_钩子)
    *   [4.11 从jobs中删除进程](#从jobs中删除进程)
    *   [4.12 设置别名](#设置别名)
*   [5 另请参阅](#另请参阅)

## 安装

安装[fish](https://www.archlinux.org/packages/?name=fish)软件包。也可以从AUR安装开发版的[fish-git](https://aur.archlinux.org/packages/fish-git/)。

安装完成后，输入`fish`即可进入fish shell。

要查看帮助文档，在fish中输入`help`。文档将会在浏览器中打开。建议用户至少读完文档中“Syntax overview”这一节内容，因为fish的语法和其他shell的不太一样。

## 把fish集成到系统中

需要考虑的是：是把fish设置为默认shell，也就是用户登录时直接进入的shell，还是通过当前的默认shell启动fish，并只在交互模式下使用fish。这里，我们假设当前的默认shell是[Bash](/index.php/Bash_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Bash (简体中文)")。

*   把fish设为**默认shell**：这种方式需要用户对fish的运行机制及其脚本语言有些基本的了解。用户需要把当前的初始化脚本和环境变量移动到fish的环境中。[#把fish设为默认shell](#把fish设为默认shell)中有具体的步骤。

*   只把fish用作**交互式shell**：这种方法“破坏性”较小。Bash会照常运行所有的初始化脚本，并在此基础上启动fish。[#只把fish设为交互式shell](#只把fish设为交互式shell)中有具体的步骤。

### 把fish设为默认shell

如果你决定把fish设为默认的shell，首先你需要将你的用户的shell改为`/usr/bin/fish`。参照[Command-line shell#Changing your default shell](/index.php/Command-line_shell#Changing_your_default_shell "Command-line shell")中的步骤。

下一步是把Bash的几个初始化脚本中现有的操作和配置写成fish的格式。这些脚本分别是`/etc/profile`、`~/.bash_profile`、`/etc/bash.bashrc`和`~/.bashrc`。

需要特别关注的是，在登录到fish中后，你需要尽快检查、调整环境变量`$PATH`的内容。在fish中，`$PATH`是一个*全局环境变量*，即它的作用范围包含所有函数，它在重启时会被清除，以及它对fish的所有子进程都是可见的（是一个*环境变量*）。向`$PATH`添加长期使用的路径的推荐的方法，是将他们赋给`fish_user_paths`这个全局变量。这个变量的内容重启时不会丢失，并会被自动添加到`$PATH`中。比如，

```
$ set -U fish_user_paths */第一个/路径* */第二个/路径* */第三个/路径*

```

这三个路径就会一直保持在`$PATH`中。这种方式比较简单，因为不需要修改配置文件。

### 只把fish设为交互式shell

如果不将fish设为默认shell，就能照常运行Bash的初始化脚本。这能够保证用户当前的环境变量不受影响并且在fish中也能使用，因为fish是作为Bash的子进程运行的。下面是几种只把fish设为交互式shell的方法。

#### 通过.bashrc启动fish

保持默认shell为Bash不变，然后添加一行`exec fish`到合适的[Bash配置文件](/index.php/Bash#Configuration_files "Bash")中，比如`.bashrc`。在这种方法中，Bash会正常执行`/etc/profile`和`/etc/profile.d`中的所有配置文件。相对于之后几种方法，这种是最通用的，因为这种方法在本机计算机和SSH远程计算机上都能使用。

**Tip:**

*   在这种配置下，要使用Bash而不是接着启动fish，需要使用`bash --norc`，以防止Bash加载`~/.bashrc`并执行`exec fish`。
*   要让类似于`bash -c 'echo test'`中的命令在Bash中执行而不是启动fish，你可以将`exec fish`换为`if [ -z "$BASH_EXECUTION_STRING" ]; then exec fish; fi`。

#### 使用终端模拟器的选项

另一种方法是在启动终端模拟器时通过添加命令行选项来启动fish。对于大部分的终端，这个选项是 `-e`。比如，要打开gnome-terminal并运行fish，可以将gnome-terminal的快捷方式改为：

```
gnome-terminal -e fish

```

对于不支持设置shell的终端模拟器，比如[lilyterm-git](https://aur.archlinux.org/packages/lilyterm-git/)，则需要这样：

```
SHELL=/usr/bin/fish lilyterm

```

另外，有些终端可以在设置或配置文件中将fish设为默认shell。

#### 使用终端复用器的选项

要将fish设为[tmux](/index.php/Tmux "Tmux")启动的默认shell，在`~/.tmux.conf`中加入这行：

```
set-option -g default-shell "/usr/bin/fish"

```

当*tmux*启动时，就会自动进入fish。

## 配置

fish的配置脚本保存在`~/.config/fish/config.fish`。这个文件与 `.bashrc`相似，当每次启动时，fish会执行这个文件中的命令。需要注意的是，如果需要设置长期保留的变量，应该将这个变量设为一个*全局变量*，而不是将它定义在这些配置脚本中。

用户定义的函数保存在`~/.config/fish/functions`中，文件名为`*函数名*.fish`。

### 网页界面

通过下面命令即可用浏览器打开fish的配置页面。

```
fish_config

```

在浏览器中可以交互式配置fish的配色、提示符、函数、变量、历史记录和快捷键。

### 命令补全

fish可以通过解析man的数据生成自动补全规则。这些自动补全规则保存于`~/.config/fish/generated_completions/`。可以运行下面的命令更新自动补齐规则。

```
fish_update_completions

```

你也可以在`~/.config/fish/completions/`中定义自己的自动补全规则。`/usr/share/fish/completions/`中有更多的例子。

对Arch Linux来说， *pacman*, *pacman-key*, *makepkg*, *cower*, *pbget*, *pacmatic*这些命令的自动补全规则已经在fish中内置了——fish在不同的发行版中内置了不同的命令补全规则。fish的内存管理足够智能，不会因为命令补全产生负面影响。

## 提示与技巧

### 命令替换

*fish*不包含Bash式的历史记录替换功能（如`sudo !!`）。fish的开发者在[fish faq](http://fishshell.com/docs/current/faq.html#faq-history)中建议使用交互式的方式调用历史记录：`上`方向键可回顾整条命令，而`Alt+上`会回顾命令的单个参数。

不过，[fish wiki](https://github.com/fish-shell/fish-shell/wiki/Bash-Style-Command-Substitution-and-Chaining-(!!-!$-&&-%7C%7C))中介绍了一些在fish中使用历史替换的办法。这种方法提供的历史替换并不完整，但可用的有`!!`（替换上一条命令）和`!$`（替换上一条命令的最后一个参数）。

### 串联命令

从3.0版本以后，fish不再提供串联命令符号`&&`和`!!`。在fish中，推荐使用`; and`和`; or`实现相似的效果。根据[fish wiki](https://github.com/fish-shell/fish-shell/wiki/Bash-Style-Command-Substitution-and-Chaining-(!!-!$-&&-%7C%7C)#getting--and-)中的步骤，可以通过设置快捷键自动将`&&`和`!!`替换为`; and`和`; or`。

### 关闭问候语

默认情况下，每次启动fish，fish都会打印问候语。要关闭问候语，可以在fish中运行：

```
set -U fish_greeting

```

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

[Liquidprompt](https://github.com/nojhan/liquidprompt)是一个“用于Bash和Zsh的全功能的、经过仔细设计的、自适应的提示符”，但它目前没有计划兼容fish[[1]](https://github.com/nojhan/liquidprompt/pull/230)。 [这个项目](https://github.com/wesbarnett/fish-lp)提供了一种用于fish的实现。

### 在提示中增加git状态

当你处在一个git目录中时，如果你想在fish的提示符中显示分支和修改的相关信息，可以仿照以下的例子编写`fish_prompt`函数：

 `~/.config/fish/functions/fish_prompt.fish` 
```
function fish_prompt
  set -l last_status $status

  if not set -q __fish_git_prompt_show_informative_status
    set -g __fish_git_prompt_show_informative_status 1
  end
  if not set -q __fish_git_prompt_color_branch
    set -g __fish_git_prompt_color_branch brmagenta
  end
  if not set -q __fish_git_prompt_showupstream
    set -g __fish_git_prompt_showupstream "informative"
  end
  if not set -q __fish_git_prompt_showdirtystate
    set -g __fish_git_prompt_showdirtystate "yes"
  end
  if not set -q __fish_git_prompt_color_stagedstate
    set -g __fish_git_prompt_color_stagedstate yellow
  end
  if not set -q __fish_git_prompt_color_invalidstate
    set -g __fish_git_prompt_color_invalidstate red
  end
  if not set -q __fish_git_prompt_color_cleanstate
    set -g __fish_git_prompt_color_cleanstate brgreen
  end

  printf '%s%s %s%s%s%s ' (set_color $fish_color_host) (prompt_hostname) (set_color $fish_color_cwd) (prompt_pwd) (set_color normal) (__fish_git_prompt)

  if not test $last_status -eq 0
    set_color $fish_color_error
  end
  echo -n '$ '
  set_color normal
end

```

然而，fish已经抛弃了这种方式，参见[fish-shell git](https://github.com/fish-shell/fish-shell/blob/master/share/functions/__fish_git_prompt.fish)。作为替代，fish现在内置了[Informative Git Prompt](http://mariuszs.github.io/blog/2013/informative_git_prompt.html)。该功能可以通过fish_config启用。

### 在SSH中用彩色显示主机名

如果需要在通过SSH登录到fish时用不同的颜色标记提示符中的主机名，请将以下内容添加到函数`fish_prompt`中，或者添加到fish的配置文件中。这里以红色为例：

 `~/.config/fish/functions/fish_prompt.fish` 
```
...
if set -q SSH_TTY
  set -g fish_color_host brred
end
...
```

### ssh-agent 问题

在fish中，`eval (ssh-agent)`会因为变量的设置方式而报错。一个变通的方案是使用csh风格的选项`-c`：

```
 $ eval (ssh-agent -c)

```

### "command not found" 钩子

[pkgfile](/index.php/Pkgfile "Pkgfile") 包含了一个 "未找到命令"("command not found") 钩子，但你输入一个当前系统不存在的命令，pkgfile会自动从官方仓库中搜索哪个安装包有这个命令。只要你安装了[pkgfile](/index.php/Pkgfile "Pkgfile")，这个钩子就会自动启用。

### 从jobs中删除进程

当退出*fish*的时候，所有后台进程也会终止。为了保持一个任务即使在fish退出了之后也继续运行，需要先输入`disown`命令，再退出。举例来说，在后台启动firefox，然后退出fish，但firefox在后台继续运行：

```
 $ firefox &
 $ disown
 $ exit

```

你会发现虽然你退出了fish，但firefox没有退出。请参阅disown(1)了解更多细节。

### 设置别名

如果想要快速的设置一个持久化的别名（即使重启也不会失效），可以直接在fish下输入：

```
$ alias FooAliasName "foo"
$ funcsave FooAliasName

```

这样会把你的别名作为fish中的函数。如果你想查看或者编辑所有的函数可以使用`fish_config`，然后在**Function**标签下进行配置。

## 另请参阅

*   [http://fishshell.com/](http://fishshell.com/) - fish主页
*   [http://fishshell.com/docs/current/index.html](http://fishshell.com/docs/current/index.html) - 文档
*   [http://hyperpolyglot.org/unix-shells](http://hyperpolyglot.org/unix-shells) - Shell 语法对照表