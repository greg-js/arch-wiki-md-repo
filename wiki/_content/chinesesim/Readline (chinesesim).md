**Readline** is a library by the [GNU Project](/index.php/GNU_Project "GNU Project"), used by [Bash](/index.php/Bash "Bash") and other CLI-interface programs to edit and interact with the command line. Before reading this page please refer to the library home [page](http://www.gnu.org/s/readline/) as only subtle configuration will be introduced here.

## Contents

*   [1 Command-line editing](#Command-line_editing)
*   [2 历史](#.E5.8E.86.E5.8F.B2)
    *   [2.1 History search](#History_search)
        *   [2.1.1 Avoid duplicates](#Avoid_duplicates)
        *   [2.1.2 Avoid whitespaces](#Avoid_whitespaces)
*   [3 Macros](#Macros)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Disabling control echo](#Disabling_control_echo)

## Command-line editing

By default Readline uses Emacs style shortcuts for interacting with command line. However, vi style editing interface is also supported. If you are a [vi](/index.php/Vi "Vi") or vim user, you may want to put the following line to your `~/.inputrc` to enable vi-like keybindings:

```
set -o vi

```

You may find either [vi](http://www.catonmat.net/download/bash-vi-editing-mode-cheat-sheet.pdf) or [emacs](http://www.catonmat.net/download/readline-emacs-editing-mode-cheat-sheet.pdf) cheat sheets useful.

## 历史

通常，无论你输入了什么，按向上箭头就会出现上一次输入的命令。然而，许多用户觉得只显示以刚刚输入的内容为开头的命令更为实际。

例如，假设输入了以下命令：

*   `ls /usr/src/linux-2.6.15-ARCH/kernel/power/Kconfig`
*   `who`
*   `mount`
*   `man mount`

通常，当输入 `ls` 并按向上箭头，你的输入就会被替换为 `man mount`。如果你使用了搜索历史功能，那么只有过去以 `ls`（当前输入的）开头的命令会被显示，在这里就是 `ls /usr/src/linux-2.6.15-ARCH/kernel/power/Kconfig`。

把以下内容加入到 `/etc/inputrc` 或者 `~/.inputrc`可以启动这个模式：

```
"\e[A":history-search-backward
"\e[B":history-search-forward

```

如果你在使用 vi 模式，添加下面几行到 `~/.inputrc` (来自 [这个帖子](https://bbs.archlinux.org/viewtopic.php?pid=428760#p428760)):

```
set editing-mode vi
$if mode=vi
set keymap vi-command
# these are for vi-command mode
"\e[A": history-search-backward
"\e[B": history-search-forward
set keymap vi-insert
# these are for vi-insert mode
"\e[A": history-search-backward
"\e[B": history-search-forward
$endif

```

If you chose to add these lines to `~/.inputrc`, it is recommended that you also add the following line at the beginning of this file to avoid strange things like [this](https://bbs.archlinux.org/viewtopic.php?id=112537):

```
$include /etc/inputrc

```

Alternatively, one can use reverse-search-history (incremental search) by pressing `Ctrl`+`R`, which does not search based on previous input but instead jumps backwards in the history buffer as commands are typed in a search term. Pressing `Ctrl`+`R` again during this mode will display the previous line in the buffer that matches the current search term, while pressing `Ctrl`+`G` (abort) will cancel the search and restore the current input line. So in order to search through all previous `mount` commands, press `Ctrl`+`R`, type 'mount' and keep pressing `Ctrl`+`R` until the desired line is found.

The forward equivalent to this mode is called forward-search-history and is bound to `Ctrl`+`S` by default. Beware that most terminals override `Ctrl`+`S` to suspend execution until `Ctrl`+`Q` is entered. (This is called XON/XOFF flow control). For activating forward-search-history, either disable flow control by issuing:

```
$ stty -ixon

```

or use a different key in `inputrc`. For example, to use `Alt`+`S` which is not bound by default:

```
"\es":forward-search-history

```

### History search

#### Avoid duplicates

If you repeat the same command several times, they will all be appended in your history. To prevent this, add to your `~/.bashrc`:

```
export HISTCONTROL=ignoredups

```

#### Avoid whitespaces

To disable logging blank commands add this to your `~/.bashrc`:

```
export HISTCONTROL=ignorespace

```

If your `~/.bashrc` already contains

```
export HISTCONTROL=ignoredups

```

replace it with

```
export HISTCONTROL=ignoreboth

```

## Macros

Readline also supports binding keys to keyboard macros. For simple example, run this command in Bash:

```
bind '"\ew":"\C-e # macro"'

```

or add the part within single quotes to inputrc:

```
"\ew":"\C-e # macro"

```

Now type a line and press `Alt`+`W`. Readline will act as though `Ctrl`+`E` (end-of-line) had been pressed, appended with ' `# macro`'.

Use any of the existing keybindings within a readline macro, which can be quite useful to automate frequently used idioms. For example, this one makes `Ctrl`+`Alt`+`L` append "| less" to the line and run it (`Ctrl`+`M` is equivalent to `Enter`:

```
"\e\C-l":"\C-e | less\C-m"

```

The next one prefixes the line with 'yes |' when pressing `Ctrl`+`Alt`+`Y`, confirming any yes/no question the command might ask:

```
"\e\C-y":"\C-ayes | \C-m"

```

This example wraps the line in `su -c ''`, if `Alt`+`S` is pressed:

```
"\es":"\C-a su -c '\C-e'\C-m"

```

As a last example, quickly send a command in the background with `Ctrl`+`Alt`+`B`, discarding all of its output:

```
"\e\C-b":"\C-e > /dev/null 2>&1 &\C-m"

```

## Tips and tricks

### Disabling control echo

Due to an update to [readline](https://www.archlinux.org/packages/?name=readline), the terminal now echoes `^C` after `Ctrl`+`C` is pressed. For users who wish to disable this, simply add the following to `~/.inputrc`:

```
set echo-control-characters off

```