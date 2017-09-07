相关文章

*   [Emacs#Custom colors and theme](/index.php/Emacs#Custom_colors_and_theme "Emacs")
*   [nano#Syntax highlighting](/index.php/Nano#Syntax_highlighting "Nano")

**翻译状态：** 本文是英文页面 [Color_output_in_console](/index.php/Color_output_in_console "Color output in console") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-09-01，点击[这里](https://wiki.archlinux.org/index.php?title=Color_output_in_console&diff=0&oldid=448928)可以查看翻译后英文页面的改动。

This page was created to consolidate colorization of CLI outputs.

## Contents

*   [1 diff](#diff)
*   [2 grep](#grep)
*   [3 less](#less)
    *   [3.1 环境变量](#.E7.8E.AF.E5.A2.83.E5.8F.98.E9.87.8F)
    *   [3.2 Wrappers](#Wrappers)
    *   [3.3 读取标准输入时彩色化输出](#.E8.AF.BB.E5.8F.96.E6.A0.87.E5.87.86.E8.BE.93.E5.85.A5.E6.97.B6.E5.BD.A9.E8.89.B2.E5.8C.96.E8.BE.93.E5.87.BA)
*   [4 ls](#ls)
*   [5 man](#man)
    *   [5.1 使用 less](#.E4.BD.BF.E7.94.A8_less)
    *   [5.2 Using most](#Using_most)
    *   [5.3 Using X resources](#Using_X_resources)
        *   [5.3.1 xterm](#xterm)
        *   [5.3.2 rxvt-unicode](#rxvt-unicode)
*   [6 pacman](#pacman)
*   [7 Wrappers for other programs](#Wrappers_for_other_programs)
    *   [7.1 Universal wrappers with multiple preconfigured presets](#Universal_wrappers_with_multiple_preconfigured_presets)
    *   [7.2 Compilers](#Compilers)
    *   [7.3 Ping](#Ping)
    *   [7.4 Make](#Make)
    *   [7.5 Libraries](#Libraries)
*   [8 Shells](#Shells)
    *   [8.1 bash](#bash)
    *   [8.2 zsh](#zsh)
    *   [8.3 Fish](#Fish)
*   [9 Terminal emulators](#Terminal_emulators)
    *   [9.1 Virtual console](#Virtual_console)
        *   [9.1.1 Login screen](#Login_screen)
    *   [9.2 X window system](#X_window_system)
    *   [9.3 Display all 256 colors](#Display_all_256_colors)
    *   [9.4 Display tput escape codes](#Display_tput_escape_codes)
    *   [9.5 Enumerate supported colors](#Enumerate_supported_colors)
    *   [9.6 Enumerate terminal capabilities](#Enumerate_terminal_capabilities)
    *   [9.7 Color scheme scripts](#Color_scheme_scripts)
*   [10 See also](#See_also)

## diff

diffutils from version 3.4 includes the `--color` option ([GNU mailing list](https://lists.gnu.org/archive/html/info-gnu/2016-08/msg00004.html)).

```
$ alias diff 'diff --color=auto'

```

Alternatively, the following wrappers can be used:

*   **colordiff** — A Perl script wrapper for 'diff' that produces the same output but with pretty 'syntax' highlighting

	[http://www.colordiff.org/](http://www.colordiff.org/) || [colordiff](https://www.archlinux.org/packages/?name=colordiff)

*   **cwdiff** — A (w)diff wrapper to support directories and colorize the output

	[https://github.com/junghans/cwdiff](https://github.com/junghans/cwdiff) || [cwdiff](https://aur.archlinux.org/packages/cwdiff/), [cwdiff-git](https://aur.archlinux.org/packages/cwdiff-git/)

## grep

除了美观用途以外，**grep**的彩色化输出也对学习[regexp](https://en.wikipedia.org/wiki/regexp "wikipedia:regexp")和**grep**功能很有用。

请在您的shell配置文件添加以下内容以启用默认的彩色化输出，适用于[Bash](/index.php/Bash "Bash")：

```
~/.bashrc|2=alias grep='grep --color=auto'

```

如果要显示行数，添加"*-n*"参数即可.

您还可以直接设置**GREP_OPTIONS** [环境变量](/index.php/Environment_variables "Environment variables")，不过这有可能会影响到那些用到**grep** [[1]](http://brainstorm.ubuntu.com/idea/24141/)的脚本：

```
 export GREP_COLOR="1;32"

```

`GREP_COLORS`环境变量其实可以定义特定的搜索。

## less

### 环境变量

请在您的 shell 配置文件添加：

 `~/.bashrc` 
```
export LESS=-R
export LESS_TERMCAP_mb=$'\E[1;31m'
export LESS_TERMCAP_md=$'\E[1;36m'
export LESS_TERMCAP_me=$'\E[0m'
export LESS_TERMCAP_se=$'\E[0m'
export LESS_TERMCAP_so=$'\E[01;44;33m'
export LESS_TERMCAP_ue=$'\E[0m'
export LESS_TERMCAP_us=$'\E[1;32m'
```

值随您所愿修改，请参照：[ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors "wikipedia:ANSI escape code")。

**Note:** The `LESS_TERMCAL_*xx*` variables is currently undocumented in less(1), for a detailed explanation on these sequences, see this [answer](http://unix.stackexchange.com/questions/108699/documentation-on-less-termcap-variables/108840#108840).

### Wrappers

您可直接开启**less**内置的代码高亮。先[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") 软件包 [source-highlight](https://www.archlinux.org/packages/?name=source-highlight)，再在您的Shell配置文件里添加以下：

 `~/.bashrc` 
```
export LESSOPEN="| /usr/bin/source-highlight-esc.sh %s"
export LESS='-R '

```

经常使用命令行界面的用户可以安装[lesspipe](https://www.archlinux.org/packages/?name=lesspipe)。

用户可以使用以下 less 命令列出一个压缩包里的文件列表：

 `$ less *compressed_file*.tar.gz` 
```
==> use tar_file:contained_file to view a file in the archive
-rw------- *username*/*group*  695 2008-01-04 19:24 *compressed_file*/*content1*
-rw------- *username*/*group*   43 2007-11-07 11:17 *compressed_file*/*content2*
*compressed_file*.tar.gz (END)
```

`lesspipe`还被赋予`less`对文件而不仅是压缩包进行交互的能力，从而成为打开某一种文件的一个新工具（比如用来代替[python-html2text](https://www.archlinux.org/packages/?name=python-html2text)查看html文件。

安装完`lesspipe`后需重新登录以激活其功能，或者运行

```
source `/etc/profile.d/lesspipe.sh`

```

### 读取标准输入时彩色化输出

**Note:** 建议将这些 [环境变量](#Colored_output_through_environment_variables) 添加到 `~/.bashrc` or `~/.zshrc`. 因为本节完全基于: `export LESS=R` 写成

当你运行一个命令和使用管道连接 [标准输出](https://en.wikipedia.org/wiki/Standard_output "wikipedia:Standard output") (*stdout*) 到 *less* 作为分页视图 (e.g. `yaourt -Qe --date | less`), 你也许会发现输出不再是彩色化的. 这通常是因为该程序试图检测如果其 *stdout* 是交互式终端, 在这种情况下将输出彩色化文本,否则输出未着色文本. 当你想重定向 *stdout* 到一个文件中，这是一个很好的行为, e.g. `yaourt -Qe --date > pkglst-backup.txt`. 但是，当你想在 `less` 浏览输出时这将不是很好的行为.

一些程序提供禁用交互式 tty 检测的选项:

```
# dmesg --color=always | less

```

如果程序不提供任何类似选项，可以欺骗程序相信*stdout* 是交互式终端，有几种可行方式:

*   [stdoutisatty](https://github.com/lilydjwg/stdoutisatty) 是一个用c写成的小程序, 它可以调用 "fake interactive tty". 你可以通过 [AUR](/index.php/AUR "AUR"): [stdoutisatty](https://aur.archlinux.org/packages/stdoutisatty/)安装. 用法示例:

```
$ stdoutisatty yaourt -Qe --date | less

```

*   [unbuffer](http://expect.sourceforge.net/example/unbuffer.man.html) 是一个基于 *sh* 和 [Tcl](http://tcl.tk/) 的很好的 (手册比程序本身还要长), 古老的脚本. *unbuffer* 附带 [expect](https://www.archlinux.org/packages/?name=expect). 我们只需要这样使用:

```
$ unbuffer yaourt -Qe --date | less

```

[zpty](http://zsh.sourceforge.net/Doc/Release/Zsh-Modules.html#The-zsh_002fzpty-Module) 是 [zsh](/index.php/Zsh "Zsh") 的一个模块, 这里有一个来自 依云[[2]](http://lilydjwg.is-programmer.com/2011/6/29/using-zpty-module-of-zsh.27677.html) 的小函数, 将其放入 `~/.zshrc`:

 `~/.zshrc` 
```
zmodload zsh/zpty

pty() {
	zpty pty-${UID} ${1+$@}
	if [[ ! -t 1 ]];then
		setopt local_traps
		trap '' INT
	fi
	zpty -r pty-${UID}
	zpty -d pty-${UID}
}

ptyless() {
	pty $@ | less
}
```

用法:

```
$ ptyless *program*

```

通过管道转接到其它程序 (less in this example):

```
$ pty *program* | less

```

## ls

可以使用一个简单的命令别名启用彩色输出功能，`~/.bashrc`文件应该已经有一句从`/etc/skel/.bashrc`复制过来的指定别名命令：

```
alias ls='ls --color=auto'

```

以下步骤可以进一步改进`ls`的彩色输出功能，比如损坏的符号链接显示为红色，把以下内容添加到`~/.bashrc`，然后重新登录，或者把脚本source一下：

```
eval $(dircolors -b)

```

## man

对很多人来说，彩色手册页比黑白的更加易于大脑消化吸收。

有两种常用的实现man手册页彩色显示的方法：使用 `most` 或 `less` .

### 使用 less

You can set various `LESS_TERMCAP_***` environment variables to change how it highlights text. For example, `LESS_TERMCAP_md` is used for bold text and `LESS_TERMCAP_me` is used to reset to normal text formatting[[3]](http://boredzo.org/blog/archives/2016-08-15/colorized-man-pages-understood-and-customized).

In Bash, the escape sequences you can use are the same ones from [Bash/Prompt customization](/index.php/Bash/Prompt_customization "Bash/Prompt customization") and these variables can be defined in a function wrapping the `man` command:

 `~/.bashrc` 
```
man() {
    LESS_TERMCAP_md=$'\e[01;31m' \
    LESS_TERMCAP_me=$'\e[0m' \
    LESS_TERMCAP_se=$'\e[0m' \
    LESS_TERMCAP_so=$'\e[01;44;33m' \
    LESS_TERMCAP_ue=$'\e[0m' \
    LESS_TERMCAP_us=$'\e[01;32m' \
    command man "$@"
}

```

For [Fish](/index.php/Fish "Fish") you could accomplish this with:

 `~/.config/fish/config.fish` 
```
set -xU LESS_TERMCAP_md (printf "\e[01;31m")
set -xU LESS_TERMCAP_me (printf "\e[0m")
set -xU LESS_TERMCAP_se (printf "\e[0m")
set -xU LESS_TERMCAP_so (printf "\e[01;44;33m")
set -xU LESS_TERMCAP_ue (printf "\e[0m")
set -xU LESS_TERMCAP_us (printf "\e[01;32m")

```

Remember to source your config or restart your shell to make the changes take effect.

For a detailed explanation on these variables, see [this answer](http://unix.stackexchange.com/questions/108699/documentation-on-less-termcap-variables/108840#108840). [Bash/Prompt customization#Examples](/index.php/Bash/Prompt_customization#Examples "Bash/Prompt customization") has some (non-Bash-specific) examples of escape sequences that can be used.

### Using most

The basic function of 'most' is similar to `less` and `more`, but it has a smaller feature set. Configuring most to use colors is easier than using less, but additional configuration is necessary to make most behave like less.

用 [pacman](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 安装软件包 [most](https://www.archlinux.org/packages/?name=most).

编辑文件`/etc/man_db.conf`，去掉pager项的注释并修改为：

```
DEFINE     pager     most -s

```

然后测试一下：

```
$ man whatever_man_page

```

通过修改`~/.mostrc`（不存在的话请自行创建）或全局配置文件 `/etc/most.conf`。示例`~/.mostrc`:

```
% Color settings
color normal lightgray black
color status yellow blue
color underline yellow black
color overstrike brightblue black

```

以下示例配置使用类似`less`的快捷键：

```
% less-like keybindings
unsetkey "^K"
unsetkey "g"
unsetkey "G"
unsetkey ":"

setkey next_file ":n"
setkey find_file ":e"
setkey next_file ":p"
setkey toggle_options ":o"
setkey toggle_case ":c"
setkey delete_file ":d"
setkey exit ":q"

setkey bob "g"
setkey eob "G"
setkey down "e"
setkey down "E"
setkey down "j"
setkey down "^N"
setkey up "y"
setkey up "^Y"
setkey up "k"
setkey up "^P"
setkey up "^K"
setkey page_down "f"
setkey page_down "^F"
setkey page_up "b"
setkey page_up "^B"
setkey other_window "z"
setkey other_window "w"
setkey search_backward "?"
setkey bob "p"
setkey goto_mark "'"
setkey find_file "E"
setkey edit "v"

```

### Using X resources

A quick way to add color to manual pages viewed on [xterm](https://www.archlinux.org/packages/?name=xterm)/`uxterm` or [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) is to modify `~/.Xresources`.

#### xterm

```
*VT100.colorBDMode:     true
*VT100.colorBD:         red
*VT100.colorULMode:     true
*VT100.colorUL:         cyan

```

which *replaces* the decorations with the colors. Also add:

```
*VT100.veryBoldColors: 6

```

if you want colors and decorations (bold or underline) *at the same time*. See `man xterm` for a description of the `veryBoldColors` resource.

#### rxvt-unicode

```
URxvt.colorIT:      #87af5f
URxvt.colorBD:      #d7d7d7
URxvt.colorUL:      #87afd7

```

Run:

```
$ xrdb -load ~/.Xresources

```

Launch a new `xterm/uxterm` or `rxvt-unicode` and you should see colorful man pages.

This combination puts colors to **bold** and <u>underlined</u> words in `xterm/uxterm` or to **bold**, <u>underlined</u>, and *italicized* text in `rxvt-unicode`. You can play with different combinations of these attributes (see the [sources](http://pub.ligatura.org/fs/xfree86/xresources/xterm) of this item).

## pacman

[Pacman](/index.php/Pacman "Pacman") has a color option. Uncomment the `Color` line in `/etc/pacman.conf`.

## Wrappers for other programs

(most of them outdated but still functioning)

### Universal wrappers with multiple preconfigured presets

*   **rainbow** — Colorize commands output or STDIN using patterns.
    Presets: df, diff, env, host, ifconfig, java-stack-trace, jboss, jonas, md5sum, mvn2, mvn3, ping, tomcat, top, traceroute.

	[https://github.com/nicoulaj/rainbow](https://github.com/nicoulaj/rainbow) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **grc** — Yet another colouriser for beautifying your logfiles or output of commands.
    Presets: configure, cvs, df, diff, esperanto, gcc, irclog, ldap, log, mount, netstat, ping, proftpd, traceroute, wdiff.

	[https://github.com/pengwynn/grc](https://github.com/pengwynn/grc) || [grc](https://www.archlinux.org/packages/?name=grc)

*   **colorlogs** — Colorize commands output or STDIN using patterns.
    Presets: logs, git status, ant, maven.

	[https://github.com/memorius/colorlogs](https://github.com/memorius/colorlogs) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **cope** — A colourful wrapper for terminal programs.
    Presets: acpi, arp, cc, df, dprofpp, fdisk, free, g++, gcc, id, ifconfig, ls, lspci, lsusb, make, md5sum, mpc, netstat, nm, nmap, nocope, ping, pmap, ps, readelf, route, screen, sha1sum, sha224sum, sha256sum, sha384sum, sha512sum, shasum, socklist, stat, strace, tcpdump, tracepath, traceroute, w, wget, who, xrandr.

	[https://github.com/yogan/cope](https://github.com/yogan/cope) || [cope-git](https://aur.archlinux.org/packages/cope-git/)

*   **cw** — A non-intrusive real-time ANSI color wrapper for common unix-based commands.
    Presets: arp, arping, auth.log@, blockdev, cal, cksum, clock, configure, cpuinfo@, crontab@, cw-pipe, cw-test.cgi, date, df, diff, dig, dmesg, du, env, figlet, file, find, finger, free, fstab@, fuser, g++, gcc, group@, groups, hdparm, hexdump, host, hosts@, id, ifconfig, inittab@, iptables, last, lastlog, lsattr, lsmod, lsof, ltrace-color, make, md5sum, meminfo@, messages@, mount, mpg123, netstat, nfsstat, nmap, nslookup, objdump, passwd@, ping, pmap, pmap_dump, praliases, profile@, protocols@, ps, pstree, quota, quotastats, resolv.conf@, route, routel, sdiff, services@, showmount, smbstatus, stat, strace-color, sysctl, syslog, tar, tcpdump, tracepath, traceroute, umount, uname, uptime, users, vmstat, w, wc, whereis, who, xferlog.

	[http://cwrapper.sourceforge.net/](http://cwrapper.sourceforge.net/) || [cw](https://aur.archlinux.org/packages/cw/)

### Compilers

*   **colorgcc** — A Perl wrapper to colorize the output of compilers with warning/error messages matching the gcc output format

	[https://schlueters.de/colorgcc.html](https://schlueters.de/colorgcc.html) || [colorgcc](https://www.archlinux.org/packages/?name=colorgcc)

### Ping

*   **prettyping** — Add some great features to ping monitoring. A wrapper around the standard ping tool with the objective of making the output prettier, more colorful, more compact, and easier to read.

	[http://denilson.sa.nom.br/prettyping/](http://denilson.sa.nom.br/prettyping/) || [prettyping](https://aur.archlinux.org/packages/prettyping/)

### Make

*   **colormake** — A simple wrapper around make to make it's output more readable.

	[http://bre.klaki.net/programs/colormake/](http://bre.klaki.net/programs/colormake/) || [colormake](https://aur.archlinux.org/packages/colormake/), [colormake-git](https://aur.archlinux.org/packages/colormake-git/)

### Libraries

*   **ruby-rainbow** — Rainbow is extension to ruby's String class adding support for colorizing text on ANSI terminal

	[https://rubygems.org/gems/rainbow/](https://rubygems.org/gems/rainbow/) || [ruby-rainbow](https://www.archlinux.org/packages/?name=ruby-rainbow)

*   **python-blessings** — A thin, practical wrapper around terminal coloring, styling, and positioning

	[https://pypi.python.org/pypi/blessings](https://pypi.python.org/pypi/blessings) || [python-blessings](https://www.archlinux.org/packages/?name=python-blessings), [python2-blessings](https://www.archlinux.org/packages/?name=python2-blessings)

## Shells

### bash

See [Bash/Prompt customization#Colors](/index.php/Bash/Prompt_customization#Colors "Bash/Prompt customization").

### zsh

See [Zsh#Colors](/index.php/Zsh#Colors "Zsh").

### Fish

See [Fish#Web interface](/index.php/Fish#Web_interface "Fish").

## Terminal emulators

### Virtual console

The colors in the [Linux virtual console](https://en.wikipedia.org/wiki/Virtual_console "w:Virtual console")—see [console(4)](http://jlk.fjfi.cvut.cz/arch/manpages/man/console.4)—running on the framebuffer can be changed. This is done by writing the escape code `\\e]PXRRGGBB`, where `X` is the hexadecimal index of the color from 0-F, and `RRGGBB` is a traditional hexadecimal RGB code.

For example, to reuse existing colors defined in `~/.Xresources`, add the following to the shell initialization file (such as `~/.bashrc`):

```
if [ "$TERM" = "linux" ]; then
    _SEDCMD='s/.*\*color\([0-9]\{1,\}\).*#\([0-9a-fA-F]\{6\}\).*/\1 \2/p'
    for i in $(sed -n "$_SEDCMD" $HOME/.Xresources | awk '$1 < 16 {printf "\\e]P%X%s", $1, $2}'); do
        echo -en "$i"
    done
    clear
fi

```

#### Login screen

The below is a colored example of the virtual console login screen in `/etc/issue`. Create a backup of the original file with `mv /etc/issue /etc/issue.bak` as root, and create a new `/etc/issue`:

```
echo -e '\e[H\e[2J' > issue
echo -e '                                                            \e[1;30m| \e[34m\\s \\r' >> issue
echo -e '       \e[36;1m/\\\\                      \e[37m||     \e[36m| |                   \e[30m|' >> issue
echo -e '      \e[36m/  \\\\                     \e[37m||     \e[36m|     _               \e[30m| \e[32m\\t' >> issue
echo -e '     \e[1;36m/ \e[0;36m.. \e[1m\\\\   \e[37m//==\\\\\\\\ ||/= /==\\\\ ||/=\\\\  \e[36m| | |/ \\\\ |  | \\\\ /     \e[30m| \e[32m\\d' >> issue
echo -e '    \e[0;36m/ .  . \\\\  \e[37m||  || ||   |    ||  || \e[36m| | |  | |  |  X      \e[1;30m|' >> issue
echo -e '   \e[0;36m/  .  .  \\\\ \e[37m\\\\\\\\==/| ||   \\\\==/ ||  || \e[36m| | |  | \\\\_/| / \\\\     \e[1;30m| \e[31m\\U' >> issue
echo -e '  \e[0;36m/ ..    .. \\\\   \e[0;37mA simple, lightweight linux distribution.  \e[1;30m|' >> issue
echo -e ' \e[0;36m/_\x27        `_\\\\                                             \e[1;30m| \e[35m\\l \e[0mon \e[1;33m\
' >> issue
echo -e ' \e[0m' >> issue
echo -e * >> issue*

```

Save the file and make it executable with `chmod +x /etc/issue`.

See also:

*   [https://bbs.archlinux.org/viewtopic.php?pid=386429#p386429](https://bbs.archlinux.org/viewtopic.php?pid=386429#p386429)
*   [http://www.linuxfromscratch.org/blfs/view/svn/postlfs/logon.html](http://www.linuxfromscratch.org/blfs/view/svn/postlfs/logon.html)

### X window system

Most [Xorg](/index.php/Xorg "Xorg") terminals, including [xterm](/index.php/Xterm "Xterm") and [urxvt](/index.php/Urxvt "Urxvt"), support at least 16 basic colors. The colors 0-7 are the 'normal' colors. Colors 8-15 are their 'bright' counterparts, used for highlighting. These colors can be modified through [X resources](/index.php/X_resources "X resources"), or through specific terminal settings. For example:

 `~/.Xresources` 
```
! Black + DarkGrey
*color0:  #000000
*color8:  #555753
! DarkRed + Red
*color1:  #ff6565
*color9:  #ff8d8d
! DarkGreen + Green
*color2:  #93d44f
*color10: #c8e7a8
! DarkYellow + Yellow
*color3:  #eab93d
*color11: #ffc123
! DarkBlue + Blue
*color4:  #204a87
*color12: #3465a4
! DarkMagenta + Magenta
*color5:  #ce5c00
*color13: #f57900
!DarkCyan + Cyan (both not tango)
*color6:  #89b6e2
*color14: #46a4ff
! LightGrey + White
*color7:  #cccccc
*color15: #ffffff
```

**Warning:** Color resources such as `foreground` and `background` can be read by other applications (such as [emacs](https://www.gnu.org/software/emacs/manual/html_node/emacs/Table-of-Resources.html)). This can be avoided by specifiying the class name, for example `XTerm.foreground`.

See also:

*   [#Using X resources](#Using_X_resources) for how to color bold and underlined text automatically.
*   [Color Themes](https://web.archive.org/web/20090130061234/http://phraktured.net/terminal-colors/) - Extensive list of terminal color themes by Phraktured.
*   [Xcolors.net](http://xcolors.net/) List of user-contributed terminal color themes.
*   [Xcolors by dkeg](http://beta.andrewrcraig.us/index.php?page=xcolors)

*   [base16 color schemes](https://github.com/chriskempson/base16)

### Display all 256 colors

Prints all 256 colors across the screen.

```
$ (x=`tput op` y=`printf %76s`;for i in {0..256};do o=00$i;echo -e ${o:${#o}-3:3} `tput setaf $i;tput setab $i`${y// /=}$x;done)

```

### Display tput escape codes

Replace `tput op` with whatever tput you want to trace. `op` is the default foreground and background color.

```
$ ( strace -s5000 -e write tput op 2>&2 2>&1 ) | tee -a /dev/stderr | grep -o '"[^"]*"'

```

```
033[\033[1;34m"\33[39;49m"\033[00m

```

### Enumerate supported colors

The following command will let you discover all the terminals you have terminfo support for, and the number of colors each terminal supports. The possible values are: 8, 15, 16, 52, 64, 88 and 256.

```
$ for T in `find /usr/share/terminfo -type f -printf '%f '`;do echo "$T `tput -T $T colors`";done|sort -nk2

```

```
Eterm-88color 88
rxvt-88color 88
xterm+88color 88
xterm-88color 88
Eterm-256color 256
gnome-256color 256
konsole-256color 256
putty-256color 256
rxvt-256color 256
screen-256color 256
screen-256color-bce 256
screen-256color-bce-s 256
screen-256color-s 256
xterm+256color 256
xterm-256color 256

```

### Enumerate terminal capabilities

This command is useful to see what features that are supported by your terminal.

```
$ infocmp -1 | sed -nu 's/^[ \000\t]*//;s/[ \000\t]*$//;/[^ \t\000]\{1,\}/!d;/acsc/d;s/=.*,//p'|column -c80

```

```
bel	cuu	ich	kb2	kf15	kf3	kf44	kf59	mc0	rmso	smul
blink	cuu1	il	kbs	kf16	kf30	kf45	kf6	mc4	rmul	tbc
bold	cvvis	il1	kcbt	kf17	kf31	kf46	kf60	mc5	rs1	u6
cbt	dch	ind	kcub1	kf18	kf32	kf47	kf61	meml	rs2	u7
civis	dch1	indn	kcud1	kf19	kf33	kf48	kf62	memu	sc	u8
clear	dl	initc	kcuf1	kf2	kf34	kf49	kf63	op	setab	u9
cnorm	dl1	invis	kcuu1	kf20	kf35	kf5	kf7	rc	setaf	vpa

```

### Color scheme scripts

See [[4]](https://paste.xinu.at/m-dAiJ/) for scripts which display a chart of your current terminal scheme.

## See also

*   [lolcat clone in x64 assembly](https://gkbrk.com/2016/07/lolcat-clone-in-x64-assembly/)