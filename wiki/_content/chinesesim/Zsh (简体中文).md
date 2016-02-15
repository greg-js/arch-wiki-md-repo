**翻译状态：** 本文是英文页面 [Zsh](/index.php/Zsh "Zsh") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-01-17，点击[这里](https://wiki.archlinux.org/index.php?title=Zsh&diff=0&oldid=386240)可以查看翻译后英文页面的改动。

[Zsh](http://zsh.sourceforge.net/Intro/intro_1.html) 是一款功能强大终端（shell）软件，既可以作为一个交互式终端，也可以作为一个脚本解释器。它在兼容 [Bash](/index.php/Bash "Bash") 的同时 (默认不兼容，除非设置成 `emulate sh`) 还有提供了很多改进，例如：

*   更高效
*   更好的自动补全
*   更好的文件名展开（通配符展开）
*   更好的数组处理
*   可定制性高

Zsh [常见问题解答](http://zsh.sourceforge.net/FAQ/zshfaq01.html#l4) 中提供了更多使用 Zsh 的理由。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.1 初始化配置文件](#.E5.88.9D.E5.A7.8B.E5.8C.96.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
    *   [1.2 将 Zsh 作为默认终端](#.E5.B0.86_Zsh_.E4.BD.9C.E4.B8.BA.E9.BB.98.E8.AE.A4.E7.BB.88.E7.AB.AF)
*   [2 配置文件介绍](#.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6.E4.BB.8B.E7.BB.8D)
    *   [2.1 全局配置文件](#.E5.85.A8.E5.B1.80.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
*   [3 配置 Zsh](#.E9.85.8D.E7.BD.AE_Zsh)
    *   [3.1 简单的 .zshrc](#.E7.AE.80.E5.8D.95.E7.9A.84_.zshrc)
    *   [3.2 配置 $PATH](#.E9.85.8D.E7.BD.AE_.24PATH)
    *   [3.3 命令补全](#.E5.91.BD.E4.BB.A4.E8.A1.A5.E5.85.A8)
    *   [3.4 "command not found" 钩子](#.22command_not_found.22_.E9.92.A9.E5.AD.90)
    *   [3.5 消除历史记录中的重复条目](#.E6.B6.88.E9.99.A4.E5.8E.86.E5.8F.B2.E8.AE.B0.E5.BD.95.E4.B8.AD.E7.9A.84.E9.87.8D.E5.A4.8D.E6.9D.A1.E7.9B.AE)
    *   [3.6 ttyctl 命令](#ttyctl_.E5.91.BD.E4.BB.A4)
    *   [3.7 快捷键绑定](#.E5.BF.AB.E6.8D.B7.E9.94.AE.E7.BB.91.E5.AE.9A)
        *   [3.7.1 ncurses 应用的快捷键绑定](#ncurses_.E5.BA.94.E7.94.A8.E7.9A.84.E5.BF.AB.E6.8D.B7.E9.94.AE.E7.BB.91.E5.AE.9A)
        *   [3.7.2 另一种方法](#.E5.8F.A6.E4.B8.80.E7.A7.8D.E6.96.B9.E6.B3.95)
        *   [3.7.3 文件管理器的快捷键绑定](#.E6.96.87.E4.BB.B6.E7.AE.A1.E7.90.86.E5.99.A8.E7.9A.84.E5.BF.AB.E6.8D.B7.E9.94.AE.E7.BB.91.E5.AE.9A)
    *   [3.8 查找历史记录](#.E6.9F.A5.E6.89.BE.E5.8E.86.E5.8F.B2.E8.AE.B0.E5.BD.95)
    *   [3.9 命令提示符](#.E5.91.BD.E4.BB.A4.E6.8F.90.E7.A4.BA.E7.AC.A6)
    *   [3.10 自定义命令提示符](#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.91.BD.E4.BB.A4.E6.8F.90.E7.A4.BA.E7.AC.A6)
        *   [3.10.1 彩色](#.E5.BD.A9.E8.89.B2)
        *   [3.10.2 示例](#.E7.A4.BA.E4.BE.8B)
    *   [3.11 目录栈（dirstack）](#.E7.9B.AE.E5.BD.95.E6.A0.88.EF.BC.88dirstack.EF.BC.89)
    *   [3.12 帮助命令](#.E5.B8.AE.E5.8A.A9.E5.91.BD.E4.BB.A4)
    *   [3.13 仿 Fish 命令高亮](#.E4.BB.BF_Fish_.E5.91.BD.E4.BB.A4.E9.AB.98.E4.BA.AE)
    *   [3.14 .zshrc 样例](#.zshrc_.E6.A0.B7.E4.BE.8B)
    *   [3.15 配置框架](#.E9.85.8D.E7.BD.AE.E6.A1.86.E6.9E.B6)
    *   [3.16 自启动程序](#.E8.87.AA.E5.90.AF.E5.8A.A8.E7.A8.8B.E5.BA.8F)
    *   [3.17 刷新自动补全](#.E5.88.B7.E6.96.B0.E8.87.AA.E5.8A.A8.E8.A1.A5.E5.85.A8)
*   [4 卸载](#.E5.8D.B8.E8.BD.BD)
*   [5 另请参见](#.E5.8F.A6.E8.AF.B7.E5.8F.82.E8.A7.81)

## 安装

在开始安装之前，你或许想查看一下自己目前使用的终端是什么：

```
$ echo $SHELL

```

[zsh](https://www.archlinux.org/packages/?name=zsh) 在[官方维护仓库](/index.php/Official_repositories "Official repositories")中，可以和其他类似软件一样[安装](/index.php/Pacman "Pacman")。如果希望使用额外的补全功能，可以安装 [zsh-completions](https://www.archlinux.org/packages/?name=zsh-completions) 软件包。

### 初始化配置文件

可以运行下面的命令来检查 Zsh 是否被正确得安装：

```
$ zsh

```

运行后你将会看到 _新用户向导（zsh-newuser-install）_，它可以帮助你完成一些最基本的配置。如果你想跳过它，可以按 `q` 键退出。如果你没有看见它，你可以手动打开 _新用户向导_：

```
$ zsh /usr/share/zsh/functions/Newuser/zsh-newuser-install -f

```

### 将 Zsh 作为默认终端

另请参见 [更改你的默认终端](/index.php/Command-line_shell#Changing_your_default_shell "Command-line shell")

**小贴士:** 如果你要替换 [bash](https://www.archlinux.org/packages/?name=bash)，你也许想转移 `~/.bashrc` 中的某些配置到 `~/.zshrc` (例如：命令提示符和[别名](/index.php/Bash#Aliases "Bash"))，以及转移 `~/.bash_profile` 中的配置到 `~/.zprofile` (例如：[启动 X Window System 的代码](/index.php/Xinitrc#Autostart_X_at_login "Xinitrc"))。

## 配置文件介绍

当 Zsh 启动时，它会按照顺序依次读取下面的配置文件：

	`/etc/zsh/zshenv`

	该文件应该包含用来设置[PATH 环境变量](#Configuring_.24PATH)以及其他一些[环境变量](/index.php/Environment_variables "Environment variables")的命令；不应该包含那些可以产生输出结果或者假设终端已经附着到 tty 上的命令。

	`~/.zshenv`

	该文件和 `/etc/zsh/zshenv` 相似，但是它是针对每个用户而言的。一般来说是用来设置一些有用的环境变量。

	`/etc/zsh/zprofile`

	这是一个全局的配置文件，在用户登录的时候加载。一般是用来在登录的时候执行一些命令。请注意，在 Arch Linux 里该文件默认包含[一行配置](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/zprofile?h=packages/zsh)，用来加载 `/etc/profile` 文件，详见 [#全局配置文件](#.E5.85.A8.E5.B1.80.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)。

	`/etc/profile`

	在登录时，该文件应该被所有和伯克利（Bourne）终端相兼容的终端加载：它在登录的的时候会加载应用相关的配置（`/etc/profile.d/*.sh`）。注意在 Arch Linux 里，Zsh 会默认加载该文件。

	`~/.zprofile`

	该文件一般用来在登录的时候自动执行一些用户脚本。

	`/etc/zsh/zshrc`

	当 Zsh 被作为交互式终端的时候，会加载这样一个全局配置文件。

	`~/.zshrc`

	当 Zsh 被作为交互式终端的时候，会加载这样一个用户配置文件。

	`/etc/zsh/zlogin`

	在登录完毕后加载的一个全局配置文件。

	`~/.zlogin`

	和 `/etc/zsh/zlogin` 相似，但是它是针对每个用户而言的。

	`/etc/zsh/zlogout`

	在注销的时候被加载的一个全局配置文件。

	`~/.zlogout`

	和 `/etc/zsh/zlogout` 相似，但是它是针对每个用户而言的.

**注意:**

*   在 Arch 源中的 [zsh](https://www.archlinux.org/packages/?name=zsh) 所使用的文件路径和 Zsh 的 mam 手册中默认的不同（详见 [#全局配置文件](#.E5.85.A8.E5.B1.80.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)）
*   `/etc/profile` 不是 Zsh 常规启动配置文件的一部分，但是 Arch 源中的 [zsh](https://www.archlinux.org/packages/?name=zsh) 会在 `/etc/zsh/zprofile` 里面加载它。用户应该注意 `/etc/profile` 里面设置的 `$PATH` 环境变量会覆盖掉 `~/.zshenv` 里面配置的任何 `$PATH`。为了防止这一点，请在 `~/.zshrc` 当中设置 `$PATH`（不推荐替换掉 `/etc/zsh/zprofile` 里面的[默认配置](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/zprofile?h=packages/zsh)，因为这样会破坏其他提供了 `/etc/profile.d` 的软件包和 Zsh 的联动关系）

### 全局配置文件

有时候你可能想提供一些所有 Zsh 用户共享的配置。在帮助手册 zsh(1) 提到的一些全局配置文件（例如 `/etc/zshrc`）的路径，在 Arch Linux 里是有一些不同的，因为 it has been compiled with flags specifically to target[[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/zsh#n34) `/etc/zsh/` instead.

所以，Arch 源中 [zsh](https://www.archlinux.org/packages/?name=zsh) 的全局配置文件会使用 `/etc/zsh/zshrc` 而不是 `/etc/zshrc`。类似的还有 `/etc/zsh/zshenv`、`/etc/zsh/zlogin` 和 `/etc/zsh/zlogout`。注意这些文件不是默认就被创建好的，你可以根据需要来创建它们。

唯一的例外是 `zprofile`，请使用 `/etc/profile`

## 配置 Zsh

尽管 Zsh 基本不需要怎么配置就能满足大多数用户的需求，但是因为其中包含太多的可定制选项，导致配置 Zsh 可能会比较耗时。

### 简单的 .zshrc

下面是一个简单的 `.zshrc` 配置文件，它提供一个配置 Zsh 的生动的例子。你可以将下面的配置保存为文件 `.zshrc` 来使用它。

 `~/.zshrc` 

```
autoload -U compinit promptinit
compinit
promptinit

# 设置 walters 主题的默认命令行提示符
prompt walters
```

**小贴士:** 你可以执行命令 `source ~/.zshrc` 来生效修改的配置，而不需要重新登录

### 配置 $PATH

将下面的配置放到 `~/.zshenv` 中：

 `~/.zshenv` 

```
typeset -U path
path=(~/bin /other/things/in/path $path[@])
```

另请参见 [《A User's Guide to the Z-Shell（Z-Shell 用户指南）》](http://zsh.sourceforge.net/Guide/zshguide02.html#l24) 和 [#Configuration files](#Configuration_files) 中的相关内容。

### 命令补全

也许 Zsh 最引人注目的特性就是它先进的自动补全功能。在 `~/.zshrc` 最后加入下面的配置，开启自动补全：

 `~/.zshrc` 

```
autoload -U compinit
compinit

```

上面的补全配置包括 ssh/scp/sftp 命令中的主机名（host name）补全。但是要让这个特性正常工作，你需要防止 `~/.ssh/known_hosts` 中的主机名被散列化（hash）。

**警告:** 主机名去散列化可能会导致本机成为 [跳跃式攻击（"Island-hopping" attacks）](http://blog.rootshell.be/2010/11/03/bruteforcing-ssh-known_hosts-files/)的跳板。如果你希望 Zsh 自动补全主机名，你可以注释掉 `/etc/ssh/ssh_config` 当中的这行配置，或者设置为 `no`： `/etc/ssh/ssh_config`  `#HashKnownHosts yes` 

你可以将原来的 `~/.ssh/known_hosts` 移动到别的地方，之后 ssh 创建的 `~/.ssh/known_hosts` 文件就不会散列化主机名（但是之前信任的主机如果需要，还得重新导入进来）。具体请参考 ssh 的 README 文件中[散列化主机名](http://nms.lcs.mit.edu/projects/ssh/README.hashed-hosts)的相关内容。

添加下面的配置可以启动使用方向键控制的自动补全：

 `~/.zshrc`  `zstyle ':completion:*' menu select` 

	_按两次 tab 键启动菜单_

添加下面的配置可以启动命令行别名的自动补全：

 `~/.zshrc`  `setopt completealiases` 

### "command not found" 钩子

另请参见 [Pkgfile#Command not found](/index.php/Pkgfile#Command_not_found "Pkgfile")。

### 消除历史记录中的重复条目

 `~/.zshrc`  `setopt HIST_IGNORE_DUPS` 

假如目前的历史记录中已经有重复条目，可以运行下面的命令清除

```
$ sort -t ";" -k 2 -u ~/.zsh_history | sort -o ~/.zsh_history

```

### ttyctl 命令

[[2]](http://zsh.sourceforge.net/Doc/Release/Shell-Builtin-Commands.html#index-tty_002c-freezing) 描述了 Zsh 中的 `ttyctl` 命令。它可以用来锁定/解锁（freeze/unfreeze）终端。许多程序会修改终端的状态并且在异常退出的时候不会还原初始状态。下面的配置可以避免手动重置终端。

 `~/.zshrc`  `ttyctl -f` 

### 快捷键绑定

Zsh 使用自带的 zle 代替 readline，并且不会读取 `/etc/inputrc` 或者 `~/.inputrc`。 Zle 有 [emacs](/index.php/Emacs "Emacs") 和 [vi](/index.php/Vi "Vi") 两个模式，默认情况下它根据环境变量 `$EDITOR` 来决定使用哪一个模式，如果为空默认为 emacs 模式。使用 `bindkey -e` 或者 `bindkey -v` 来手动指定模式。 另请参见 [zshwiki: bindkeys](http://zshwiki.org/home/zle/bindkeys).

#### ncurses 应用的快捷键绑定

（译者注：ncurses 是一个字符界面下的 GUI 框架）如果直接将 ncurses 应用绑定到某个快捷键，那么它会失去交互性。可以使用变量 `BUFFER` 来解决这个问题。下面的例子是使用 `Alt+\` 来打开 ncmpcpp：

 `~/.zshrc` 

```
ncmpcppShow() { BUFFER="ncmpcpp"; zle accept-line; }
zle -N ncmpcppShow
bindkey '^[\' ncmpcppShow
```

#### 另一种方法

该方法会在启动应用之前，将你的输入保存在一行当中。

 `~/.zshrc` 

```
ncmpcppShow() { ncmpcpp <$TTY; zle redisplay; }
zle -N ncmpcppShow
bindkey '^[\' ncmpcppShow
```

#### 文件管理器的快捷键绑定

图形化文件管理器中使用快捷键可能很实用（译者注：你也可以在 Zsh 中自定义快捷键达到这样的效果）。第一个使用 `Alt+Left` 让用户撤销最近的 cd 操作，第二个使用 `Alt+Up` 让用户进入上层目录。这两个快捷键同时也会显示目录中的内容。

 `~/.zshrc` 

```
cdUndoKey() {
  popd      > /dev/null
  zle       reset-prompt
  echo
  ls
  echo
}

cdParentKey() {
  pushd .. > /dev/null
  zle      reset-prompt
  echo
  ls
  echo
}

zle -N                 cdParentKey
zle -N                 cdUndoKey
bindkey '^[[1;3A'      cdParentKey
bindkey '^[[1;3D'      cdUndoKey

```

### 查找历史记录

 `~/.zshrc` 

```
[[ -n "${key[PageUp]}"   ]]  && bindkey  "${key[PageUp]}"    history-beginning-search-backward
[[ -n "${key[PageDown]}" ]]  && bindkey  "${key[PageDown]}"  history-beginning-search-forward

```

使用这段配置会只显示以当前命令开头的历史记录。

### 命令提示符

这是一种 Zsh 中简单快速设置彩色提示符的方法。首先确保 `.zshrc` 中配置了自动加载提示符。具体配置如下：

 `~/.zshrc` 

```
autoload -U promptinit
promptinit

```

然后你可以运行下面的命令查看可用的提示符：

```
$ prompt -l

```

使用下面命令来启动其中一种提示符，例如启动 "walters" 提示符：

```
$ prompt walters

```

使用下面的命令查看所有可用的主题：

```
$ prompt -p

```

### 自定义命令提示符

对于那些不满足默认提示符的用户，Zsh 提供了自定义提示符的方法。除了普通终端会提供的靠左的提示符外，Zsh 还提供了靠右的提示符。通过配置 `PROMPT=` 来设置。

可以参考 [Prompt Expansion](http://zsh.sourceforge.net/Doc/Release/Prompt-Expansion.html) 来获得所有可用的 prompt variables 和 conditional substrings。

#### 彩色

Zsh 设置彩色提示符的方法和 [Bash](/index.php/Color_Bash_Prompt "Color Bash Prompt") 不同。 在 `.zshrc` 中 `PROMPT=` 前面添加 `autoload -U colors && colors` 来启用彩色提示符。通常你需要将这些配置放在 `%{ [...] %}` 里面确保光标不移动。

`$fg[color]` 会设置文本的颜色（红，绿，蓝，等等。默认是和之前的文本颜色保持一致）

| 命令 | 描述 |
| `%F{color} [...] %f` | 和前面介绍的 $fg 是一样的，但是更简洁。还可以在 F 前面添加数字。 |
| `$fg_no_bold[color]` | 设置文本为非粗体同时设定文本颜色 |
| `$fg_bold[color]` | 设置文本为粗体同时设定文本颜色 |
| `$reset_color` | 重置文本颜色（改为默认颜色）。不会重置粗体设定。使用 `%b` 来重置粗体设定。可以使用 `%f` 来简化配置。 |
| `%K{color} [...] %k` | 设置背景颜色。和非粗体文本颜色一样。任何单一数字前缀会设置背景为黑色。 |

| Possible color values |
| 黑 `black` or `0` | 红 `red` or `1` |
| 绿 `green` or `2` | 黄 `yellow` or `3` |
| 蓝 `blue` or `4` | 紫 `magenta` or `5` |
| 青 `cyan` or `6` | 白 `white` or `7` |

**注意:** 粗体文本不一定会和普通文本使用同一种颜色。例如, `$fg['yellow']` 会使用暗一点的黄色, 而 `$fg_bold['yellow']` 可能会使用亮一点的黄色。（译者注：具体是由你的终端模拟器配置决定的）

#### 示例

左右双边的提示符：

```
PROMPT="%{$fg[red]%}%n%{$reset_color%}@%{$fg[blue]%}%m %{$fg[yellow]%}%1~ %{$reset_color%}%#"
RPROMPT="[%{$fg[yellow]%}%?%{$reset_color%}]"

```

效果如下（忽略颜色）：

```
username@host ~ %                                                         [0]

```

### 目录栈（dirstack）

Zsh 可以配置 DIRSTACK 相关变量来加速 cd 访问常用目录。在你的配置文件中添加下面的配置：

 `.zshrc` 

```
DIRSTACKFILE="$HOME/.cache/zsh/dirs"
if [[ -f $DIRSTACKFILE ]] && [[ $#dirstack -eq 0 ]]; then
  dirstack=( ${(f)"$(< $DIRSTACKFILE)"} )
  [[ -d $dirstack[1] ]] && cd $dirstack[1]
fi
chpwd() {
  print -l $PWD ${(u)dirstack} >$DIRSTACKFILE
}

DIRSTACKSIZE=20

setopt autopushd pushdsilent pushdtohome

## Remove duplicate entries
setopt pushdignoredups

## This reverts the +/- operators.
setopt pushdminus

```

现在你可以使用

```
dirs -v

```

来打印目录栈（dirstack）。使用 `cd -<NUM>` 来跳转到以前访问过的目录。你还可以在连字符后面使用自动补全，非常方便。

### 帮助命令

和 [bash](/index.php/Bash "Bash") 不同的是 _zsh_ 没有内置的 `help` 命令，要想在 zsh 中使用 `help`，可以添加下面的配置：

```
autoload -U run-help
autoload run-help-git
autoload run-help-svn
autoload run-help-svk
unalias run-help
alias help=run-help
```

### 仿 Fish 命令高亮

（译者注：Fish 是一款比较新的终端软件）[Fish](/index.php/Fish "Fish") 提供了非常强大的命令高亮。如果你希望在 zsh 中使用类似的功能，你可以从官方仓库里安装 [zsh-syntax-highlighting](https://www.archlinux.org/packages/?name=zsh-syntax-highlighting)，然后添加下面的配置到你的 zshrc 中：

```
source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

```

### .zshrc 样例

*   官方仓库里来自 [http://grml.org/zsh](http://grml.org/zsh) 的软件包 [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) 中包含了很多 Zsh 的配置技巧
*   [http://github.com/MrElendig/dotfiles-alice/blob/master/.zshrc](http://github.com/MrElendig/dotfiles-alice/blob/master/.zshrc) 包含一些动态提示符和终端窗口标题等基本配置
*   [https://github.com/slashbeast/things/blob/master/configs/DOTzshrc](https://github.com/slashbeast/things/blob/master/configs/DOTzshrc) 拥有很多特性的 zsh 配置，注意阅读它的注释。值得注目的特性：关机、重启和睡眠的用户确认交互函数，命令提示符内支持 GIT（没有使用 vcsinfo），菜单使用 tab 补全，打印当前执行的命令到终端窗口的标题上，等等。

### 配置框架

*   [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) 是一个著名的，社区驱动的框架，它拥有很多有用的函数，helpers，插件，主题，可以用来简化复杂的 Zsh 配置。
*   [Prezto - Instantly Awesome Zsh](https://github.com/sorin-ionescu/prezto)（可以通过 [prezto-git](https://aur.archlinux.org/packages/prezto-git/) 获取） 它是一个模块化的 Zsh 配置框架，里面有很多顺手的默认配置、别名、函数、自动补全和命令提示符主题。
*   [Antigen](https://github.com/zsh-users/antigen) (可以通过 [antigen-git](https://aur.archlinux.org/packages/antigen-git/) 获取) 这个一个 zsh 插件管理器，受到 oh-my-zsh 和 vundle 的启发

### 自启动程序

**注意:** `$ZDOTDIR` 默认指向 `$HOME`

Zsh 经常执行 `/etc/zsh/zshenv` 和 `$ZDOTDIR/.zshenv`，所以不要让他们变得很臃肿。

如果是一个登录了的终端，会加载 `/etc/profile` 然后加载 `$ZDOTDIR/.zprofile`。然后如果是交互式模式，会继续加载 `/etc/zsh/zshrc` 接着加载 `$ZDOTDIR/.zshrc` 。最后如果还是登录了的终端，`/etc/zsh/zlogin` 和 `$ZDOTDIR/.zlogin` 也会被加载。

另请参见 `man zsh` 的 _STARTUP/SHUTDOWN FILES_ 章节。

### 刷新自动补全

一般来说，compinit 不会自动在 $PATH 里面查找新的可执行文件。例如当你安装了一个新的软件包，/usr/bin 里的新文件不会立即自动添加到自动补全当中。所以你需要执行下面的命令来将它们添加进自动补全：

```
$ rehash

```

这个 'rehash' 可以被放到你的 `zshrc` 来自动执行

 `~/.zshrc`  `zstyle ':completion:*' rehash true` 
**注意:** 这个技巧在 Oh My Zsh [[3]](https://github.com/robbyrussell/oh-my-zsh/issues/3440) 的一次 PR 中被发现

## 卸载

在卸载 [zsh](https://www.archlinux.org/packages/?name=zsh) 之前请先更换默认终端。

**警告:** 如果不遵循下面的步骤可能会导致用户无法访问任何终端

运行下面的命令：

```
$ chsh -s /bin/bash _user_

```

每一个使用 _zsh_ 作为默认终端的用户都需要执行一遍条命令。当完成之后就可以把 [zsh](https://www.archlinux.org/packages/?name=zsh) 软件包删除了。

当然你也也可以以 root 身份修改 `/etc/passwd` 文件，来批量更改用户的默认终端。

**警告:** 强留建议使用 `vipw` 来修改 `/etc/passwd`，因为它可以帮助你消灭格式错误

例如将下面的配置中的 /bin/zsh

```
_username_:x:1000:1000:_Full Name_,,,:/home/_username_:/bin/zsh

```

改成 /bin/bash

```
_username_:x:1000:1000:_Full Name_,,,:/home/_username_:/bin/bash

```

## 另请参见

*   [A User's Guide to ZSH](http://zsh.sourceforge.net/Guide/zshguide.html)
*   [The Z Shell Manual](http://zsh.sourceforge.net/Doc/Release/index-frame.html) (different format available [here](http://zsh.sourceforge.net/Doc/))
*   [Zsh FAQ](http://zsh.sourceforge.net/FAQ/zshfaq01.html)
*   [zsh-lovers(1)](http://grml.org/zsh/zsh-lovers.html) (this is also available as [zsh-lovers](https://www.archlinux.org/packages/?name=zsh-lovers) in offical repository)
*   [Zsh Wiki](http://zshwiki.org/home/)
*   [Gentoo Wiki: Zsh/HOWTO](https://wiki.gentoo.org/wiki/Zsh/HOWTO)
*   [Bash2Zsh Reference Card](http://www.bash2zsh.com/zsh_refcard/refcard.pdf)