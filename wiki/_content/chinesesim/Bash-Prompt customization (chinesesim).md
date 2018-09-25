相关文章

*   [Environment variables](/index.php/Environment_variables "Environment variables")
*   [Bash](/index.php/Bash "Bash")

**翻译状态：** 本文是英文页面 [Color_Bash_Prompt](/index.php/Color_Bash_Prompt "Color Bash Prompt") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-03-17，点击[这里](https://wiki.archlinux.org/index.php?title=Color_Bash_Prompt&diff=0&oldid=420530)可以查看翻译后英文页面的改动。

这是一个设置[Bash](/index.php/Bash "Bash")提示符（PS1）色彩以及自定义的参考版本，它可以帮助你在命令行更有效率。您可以添加更多的信息给你的提示符，或者你可以简单地设置的色彩来使提示符中色彩斑斓。

## Contents

*   [1 提示符　](#.E6.8F.90.E7.A4.BA.E7.AC.A6)
*   [2 技巧](#.E6.8A.80.E5.B7.A7)
    *   [2.1 Bash 转义字符](#Bash_.E8.BD.AC.E4.B9.89.E5.AD.97.E7.AC.A6)
    *   [2.2 Terminfo escape sequences](#Terminfo_escape_sequences)
    *   [2.3 ANSI escape sequences](#ANSI_escape_sequences)
    *   [2.4 Embedding commands](#Embedding_commands)
    *   [2.5 PROMPT_COMMAND](#PROMPT_COMMAND)
    *   [2.6 Escapes between command input and output](#Escapes_between_command_input_and_output)
    *   [2.7 Customizing root prompts](#Customizing_root_prompts)
*   [3 Examples](#Examples)
    *   [3.1 Colors](#Colors)
    *   [3.2 Common capabilities](#Common_capabilities)
    *   [3.3 Visualizing exit codes](#Visualizing_exit_codes)
    *   [3.4 Positioning the cursor](#Positioning_the_cursor)
        *   [3.4.1 Right-justified text](#Right-justified_text)
        *   [3.4.2 Arbitrary positioning](#Arbitrary_positioning)
    *   [3.5 Customizing the terminal window title](#Customizing_the_terminal_window_title)
*   [4 See also](#See_also)

## 提示符　

Bash 有四个可以定制的提示符:

*   `PS1` 是在每个命令前都显示的主要提示符，大部分用户都是定制这个值。
*   `PS2` 命令需要输入时的第二提示符(比如多行命令).
*   `PS3` 不常用，Bash　的内置 `select` 显示交互菜单时使用. 和其它提示符不一样，它不扩展 [Bash escape sequences](#ANSI_escape_sequences). 通常在使用包含 `select` 的脚本时会需要定制此提示符。
*   `PS4` 也不常用，在调试　bash 脚本时显示缩进级别。第一个字符的重复次数表示缩进级别。

所有提示符都可以通过设置变量到需要的数值进行定义(通常在 `~/.bashrc`), 例如：

```
export PS2='> '

```

## 技巧

虽然提示符可以简单的设置成固定值，下面技巧可以让提示符更动态和有用。

### Bash 转义字符

输出提示符时，Bash 会查找一些反斜杠开头的字符，然后转义成特殊字符。例如 `\u` 扩增为当前用户名 `\A` 扩展为当前时间. 所以如果设置 PS1 为 `'\A \u $ '`，将会输入 `17:35 *username* $` .

Bash 手册页面的 "PROMPTING" 段落有完整的转义字符列表。

### Terminfo escape sequences

Aside from the escape characters recognized by Bash, most terminals recognize special escape sequences that affect the terminal itself rather than printing characters. For example they might change the color of subsequent printed characters, move the cursor to an arbitrary location, or clear the screen. These escape sequences can be somewhat illegible and can vary from terminal to terminal, so they are documented in the terminfo database. To see what capabilities your terminal supports, run

```
$ infocmp

```

The capability names (the part before the =) can be looked up in the terminfo man page for a description of what they do. For example, `setaf` sets the foreground color of whatever text is printed after it. To get the escape code for a capability, you can use the `tput` command. For example

```
$ tput setaf 2

```

prints the escape sequence to set the foreground color to green.

**Note:** If tput commands are failing for you, ensure that you have set the correct `TERM` value for your shell. For example, if you have set `xterm` instead of `xterm-256color`, `tput setaf` will only work with color numbers 0-7.

To practically incorporate these capabilities into your prompt, you can use Bash's command substitution and string interpolation. For example

 `~/.bashrc` 
```
GREEN="\[$(tput setaf 2)\]"
RESET="\[$(tput sgr0)\]"

export PS1="${GREEN}my prompt${RESET}> "
```

my prompt>

**Note:** Wrapping the tput output in `\[ \]` is recommended by the Bash man page. This helps Bash ignore non-printable characters so that it correctly calculates the size of the prompt.

### ANSI escape sequences

Unfortunately, valid ANSI escape sequences may be missing from your terminal's terminfo database. This is especially common with escape sequences for newer features such as 256 color support. In that case you cannot use tput, you must input the escape sequence manually.

See [Wikipedia:ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code "wikipedia:ANSI escape code") for examples of escape sequences. Every escape sequence starts with a literal escape character, which you can input using the Bash escape sequence `\e`. So for example,`\e[48;5;209m` sets the background to a peachy color (if you have 256 color support) and `\e[2;2H` moves the cursor near the top-left corner of the screen.

In cases where Bash escape sequences are not supported (such as PS3) you can get a literal escape character using Bash's printf builtin:

```
ESC=$(printf "\e")
PEACH="$ESC[48;5;209m"

```

### Embedding commands

If you want to add the output of some command to your prompt, you might be tempted to use command substitution. For example, to add the amount of free memory to your prompt you might try:

 `export PS1="$(awk '/MemFree/{print $2}' /proc/meminfo) prompt > "` 
```
53718 prompt >
53718 prompt >
53718 prompt >
```

But this doesn't work; the amount of memory shown is the same every time! This is because the command is run once, when PS1 is first set, and never again. The trick is to simply prevent the substitution either by escaping the `$` or by defining it in single quotes—either way it will be substituted when the prompt is actually displayed:

```
export PS1="\$(awk '/MemFree/{print \$2}' /proc/meminfo) prompt > "
# or
export PS1='$(awk "/MemFree/{print \$2}" /proc/meminfo) prompt > '

```

To prevent long commands from making your PS1 huge, you can define functions:

```
free_mem()
{
    awk '/MemFree/{print $2}' /proc/meminfo
}

export PS1='$(free_mem) prompt > '
```

**Note:** You can use terminfo/ANSI escape sequences inside substituted functions but **not** Bash escapes. In particular `\[ \]` won't work for surrounding non-printable characters. Instead you can use the octal escapes `\001` and `\002` (e.g. using `printf` or `echo -e`).

### PROMPT_COMMAND

If the `PROMPT_COMMAND` variable is set, it will be evaluated right before PS1 is displayed. This can be used to achieve quite powerful effects. For example it can reassign PS1 based on some condition, or perform some operation on your Bash history every time you run a command.

**Warning:** PROMPT_COMMAND generally should not be used to print characters directly to the prompt. Characters printed outside of PS1 are not counted by Bash, which will cause it to incorrectly place the cursor and clear characters. Either use PROMPT_COMMAND to set PS1 or look at [embedding commands](#Embedding_commands).

### Escapes between command input and output

You can affect your input text in Bash by not resetting the text properties at the end of your PS1\. For example, inserting `tput blink` at the end of your PS1 will make your typed commands blink. However this effect will also continue through the command's output since the text properties are not reset when you hit Enter.

In order to insert escape sequences after you type a command but before the output is displayed, you can trap Bash's DEBUG signal, which is sent right before each command is executed:

 `~/.bashrc`  `trap 'tput sgr0' DEBUG` 

### Customizing root prompts

To ensure that you know when you are running as root, you can customize your root prompt to make it clearly stand out (perhaps blinking red?). This is done by customize the Bash prompt as usual but in root's home directory, `/root`. Start off by copying the skeleton files `/etc/skel/.bash_profile` and `/etc/skel/.bashrc` to `/root`, then edit `/root/.bashrc` as desired.

## Examples

### Colors

**Tip:** `infocmp` shows the number of colors `tput` works with, for example `colors#8`.

To see the full range of colors your terminal supports, you can use a simple loop with tput (change `setab` to `setaf` for text foregrounds):

```
for C in {0..255}; do
    tput setab $C
    echo -n "$C "
done
tput sgr0
echo
```

If that does not work (and you cannot fix it by setting the [correct TERM value](#Terminfo_escape_sequences)), you can test the different manual escape sequences:

```
# standard colors
for C in {40..47}; do
    echo -en "\e[${C}m$C "
done
# high intensity colors
for C in {100..107}; do
    echo -en "\e[${C}m$C "
done
# 256 colors
for C in {16..255}; do
    echo -en "\e[48;5;${C}m$C "
done
echo -e "\e(B\e[m"

```

To change the manual escapes from background to foreground, the standard color range is `30..37`, the high intensity range is `90..97`, and the 48 should be changed to 38 for 256 colors.

### Common capabilities

The following [terminfo capabilities](#Terminfo_escape_sequences) are useful for prompt customization and are supported by many terminals. **#1** and **#2** are placeholders for numeric arguments.

| Capability | Escape sequence | Description |
| Text attributes |
| blink | \E[5m | blinking text on |
| bold | \E[1m | bold text on |
| dim | \E[2m | dim text on |
| rev | \E[7m | reverse video on (switch text/background colors) |
| sitm | \E[3m | italic text on |
| ritm | \E[23m | italic text off |
| smso | \E[7m | highlighted text on |
| rmso | \E[27m | highlighted text off |
| smul | \E[4m | underlined text on |
| rmul | \E[24m | underlined text off |
| setab **#1** | \E[4**#1**m | set background color **#1** (0-7) |
| setaf **#1** | \E[3**#1**m | set text color **#1** (0-7) |
| sgr0 | \E(B\E[m | reset text attributes |
| Cursor movement |
| sc | \E7 | save cursor position |
| rc | \E8 | restore saved cursor position |
| clear | \E[H\E[2J | clear screen and move cursor to top left |
| cuu **#1** | \E[**#1**A | move cursor up **#1** rows |
| cud **#1** | \E[**#1**B | move cursor down **#1** rows |
| cuf **#1** | \E[**#1**C | move cursor right **#1** columns |
| cub **#1** | \E[**#1**D | move cursor left **#1** columns |
| home | \E[H | move cursor to top left |
| hpa **#1** | \E[**#1**G | move cursor to column **#1** |
| vpa **#1** | \E[**#1**d | move cursor to row **#1**, first column |
| cup **#1** **#2** | \E[**#1**;**#2**H | move cursor to row **#1**, column **#2** |
| Removing characters |
| dch **#1** | \E**#1**P | remove **#1** characters (like backspacing) |
| dl **#1** | \E**#1**M | remove **#1** lines |
| ech **#1** | \E**#1**X | clear **#1** characters (without moving cursor) |
| ed | \E[J | clear to bottom of screen |
| el | \E[K | clear to end of line |
| el1 | \E[1K | clear to beginning of line |

### Visualizing exit codes

Using the same trick from [embedding commands](#Embedding_commands) you can delay the interpolation of special Bash variables like `$?`. So the following prompt shows the exit code of the previous command:

```
export PS1="\$? > "
# or
export PS1='$? > '

```

0 > true
0 > false
1 >

This can be made more interesting using conditionals and functions:

```
exitstatus()
{
    if [[ $? == 0 ]]; then
        echo ':)'
    else
        echo 'D:'
    fi
}
export PS1='$(exitstatus) > '
```

:) > true
:) > false
D: >

### Positioning the cursor

It is possible to move the cursor around the screen inside of PS1 to make different parts of the prompt appear in different locations. However, to ensure that Bash positions the cursor and output in the right position, you must move the cursor back to the original position after you are done printing elsewhere. This can be done using the tput capabilities `sc` and `rc` to save and restore the cursor position. The general pattern for a prompt that moves the cursor is

```
export PS1="\[$(tput sc; *cursor-moving code*) *positioned prompt stuff* $(tput rc)\] *normal prompt stuff*"

```

where the entire block of repositioned prompt is wrapped in `\[ \]` to prevent Bash from counting it as part of the regular prompt.

#### Right-justified text

The simplest way to print text on the right side of the screen is to use printf

```
rightprompt()
{
    printf "%*s" $COLUMNS "right prompt"
}

export PS1='\[$(tput sc; rightprompt; tput rc)\]left prompt > '
```

left prompt > right prompt

This creates a right-justified variable-sized field `%*s` and sets its size to the current number of columns of the terminal `$COLUMNS`.

#### Arbitrary positioning

The `cup` capability moves the cursor to a specific position on the screen, for example `tput cup 20 5` moves the cursor to line 20, column 5 (where 0 0 is the top left corner). `cuu`, `cud`, `cuf`, and `cub` (up, down, forward, back) move the cursor relative to its current position. For example `tput cuf 10` moves the cursor 10 characters to the right. You can use the `LINES` and `COLUMNS` variables in the arguments to move the cursor relative to the bottom and right edges. For example, to move 10 lines and 5 columns away from the bottom right corner:

```
$ tput cup $((LINES - 11)) $((COLUMNS - 6))

```

### Customizing the terminal window title

The terminal window title can be customized in much the same way as the prompt: by printing escape sequences in the shell. Thus it is common for users to include window title customizations in their prompt. Although this is technically a feature of xterm, many modern terminals support it. The escape sequence to use is `**ESC**]2;*new title***BEL**` where `**ESC**` and `**BEL**` are the escape and bell characters. Using [Bash escape sequences](#ANSI_escape_sequences), changing the title in your prompt looks like

```
export PS1='\[\e]2;*new title*\a\]prompt > '

```

Of course your window title string can include output from [embedding commands](#Embedding_commands) or variables such as `$PWD`, so that the title changes with each command.

## See also

*   Community examples and screenshots in the Forum thread: [What's your PS1?](https://bbs.archlinux.org/viewtopic.php?id=50885)
*   [Gentoo's `/etc/bash/bashrc`](https://gitweb.gentoo.org/repo/gentoo.git/tree/app-shells/bash/files/bashrc). See also [gentoo-bashrc](https://aur.archlinux.org/packages/gentoo-bashrc/).
*   tput(1)
    *   [tput reference on bash-hackers.org](http://wiki.bash-hackers.org/scripting/terminalcodes)
    *   [Colours and Cursor Movement With tput](http://tldp.org/HOWTO/Bash-Prompt-HOWTO/x405.html)
*   [Nice Xresources color schemes collection](http://xcolors.net/)
*   [Bash Prompt HOWTO](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html)
*   [Giles Orr's collection of sample prompts](http://gilesorr.com/bashprompt/prompts/index.html)
*   [Bash tips: Colors and formatting](http://misc.flogisoft.com/bash/tip_colors_and_formatting)
*   [Liquid Prompt — a useful adaptive prompt for Bash & zsh](https://github.com/nojhan/liquidprompt)
*   [Bash POWER PROMPT](http://www.askapache.com/linux-unix/bash-power-prompt.html)
*   [Wikipedia:ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code "wikipedia:ANSI escape code")