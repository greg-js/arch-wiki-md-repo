Related articles

*   [Bash](/index.php/Bash "Bash")
*   [Environment variables](/index.php/Environment_variables "Environment variables")
*   [Git#Git prompt](/index.php/Git#Git_prompt "Git")

Bash has several prompts which can be customized to increase productivity, aesthetic appeal, and nerd cred.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Prompts](#Prompts)
*   [2 Techniques](#Techniques)
    *   [2.1 Bash escape sequences](#Bash_escape_sequences)
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

## Prompts

Bash has four prompts that can be customized:

*   `PS1` is the primary prompt which is displayed before each command, thus it is the one most people customize.
*   `PS2` is the secondary prompt displayed when a command needs more input (e.g. a multi-line command).
*   `PS3` is not very commonly used. It is the prompt displayed for Bash's `select` built-in which displays interactive menus. Unlike the other prompts, it does not expand [Bash escape sequences](#Bash_escape_sequences). Usually you would customize it in the script where the `select` is used rather than in your `.bashrc`.
*   `PS4` is also not commonly used. It is displayed when debugging bash scripts to indicate levels of indirection. The first character is repeated to indicate deeper levels.

All of the prompts are customized by setting the corresponding variable to the desired string (usually in `~/.bashrc`), for example

```
PS2='> '

```

## Techniques

While one can simply set their prompt to a plain string, there are a variety of techniques for making the prompt more dynamic and useful.

### Bash escape sequences

When printing the prompt string, Bash looks for certain backslash-escaped characters and will expand them into special strings. For example, `\u` is expanded into the current username and `\A` is expanded to the current time. So a PS1 of `'\A \u $ '` would be printed like `17:35 *username* $` .

Check the "PROMPTING" section of the Bash man page for a complete list of escape sequences.

### Terminfo escape sequences

Aside from the escape characters recognized by Bash, most terminals recognize special escape sequences that affect the terminal itself rather than printing characters. For example they might change the color of subsequent printed characters, move the cursor to an arbitrary location, or clear the screen. These escape sequences can be somewhat illegible and can vary from terminal to terminal, so they are documented in the terminfo database. To see what capabilities your terminal supports, run

```
$ infocmp

```

The capability names (the part before the =) can be looked up in [terminfo(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/terminfo.5) for a description of what they do. For example, `setaf` sets the foreground color of whatever text is printed after it. To get the escape code for a capability, you can use the `tput` command. For example

```
$ tput setaf 2

```

prints the escape sequence to set the foreground color to green.

**Note:** If tput commands are failing for you, ensure that you have set the correct `TERM` value for your shell. For example, if you have set `xterm` instead of `xterm-256color`, `tput setaf` will only work with color numbers 0-7.

To practically incorporate these capabilities into your prompt, you can use Bash's command substitution and string interpolation. For example

```
GREEN="\[$(tput setaf 2)\]"
RESET="\[$(tput sgr0)\]"

PS1="${GREEN}my prompt${RESET}> "
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

 `PS1="$(awk '/MemFree/{print $2}' /proc/meminfo) prompt > "` 
```
53718 prompt >
53718 prompt >
53718 prompt >
```

But this doesn't work; the amount of memory shown is the same every time! This is because the command is run once, when PS1 is first set, and never again. The trick is to simply prevent the substitution either by escaping the `$` or by defining it in single quotes—either way it will be substituted when the prompt is actually displayed:

```
PS1="\$(awk '/MemFree/{print \$2}' /proc/meminfo) prompt > "
# or
PS1='$(awk "/MemFree/{print \$2}" /proc/meminfo) prompt > '

```

To prevent long commands from making your PS1 huge, you can define functions:

```
free_mem()
{
    awk '/MemFree/{print $2}' /proc/meminfo
}

PS1='$(free_mem) prompt > '
```

**Note:** You can use terminfo/ANSI escape sequences inside substituted functions but **not** Bash escapes. In particular `\[ \]` won't work for surrounding non-printable characters. Instead you can use the octal escapes `\001` and `\002` (e.g. using `printf` or `echo -e`).

### PROMPT_COMMAND

If the `PROMPT_COMMAND` variable is set, it will be evaluated right before PS1 is displayed. This can be used to achieve quite powerful effects. For example it can reassign PS1 based on some condition, or perform some operation on your Bash history every time you run a command.

**Warning:** PROMPT_COMMAND generally should not be used to print characters directly to the prompt. Characters printed outside of PS1 are not counted by Bash, which will cause it to incorrectly place the cursor and clear characters. Either use PROMPT_COMMAND to set PS1 or look at [embedding commands](#Embedding_commands).

### Escapes between command input and output

You can affect your input text in Bash by not resetting the text properties at the end of your PS1\. For example, inserting `tput blink` at the end of your PS1 will make your typed commands blink. However this effect will also continue through the command's output since the text properties are not reset when you hit Enter.

In order to insert escape sequences after you type a command but before the output is displayed, you can trap Bash's DEBUG signal, which is sent right before each command is executed:

```
$ trap 'tput sgr0' DEBUG

```

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
PS1="\$? > "
# or
PS1='$? > '

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
PS1='$(exitstatus) > '
```

:) > true
:) > false
D: >

### Positioning the cursor

It is possible to move the cursor around the screen inside of PS1 to make different parts of the prompt appear in different locations. However, to ensure that Bash positions the cursor and output in the right position, you must move the cursor back to the original position after you are done printing elsewhere. This can be done using the tput capabilities `sc` and `rc` to save and restore the cursor position. The general pattern for a prompt that moves the cursor is

```
PS1="\[$(tput sc; *cursor-moving code*) *positioned prompt stuff* $(tput rc)\] *normal prompt stuff*"

```

where the entire block of repositioned prompt is wrapped in `\[ \]` to prevent Bash from counting it as part of the regular prompt.

#### Right-justified text

The simplest way to print text on the right side of the screen is to use printf

```
rightprompt()
{
    printf "%*s" $COLUMNS "right prompt"
}

PS1='\[$(tput sc; rightprompt; tput rc)\]left prompt > '
```

left prompt > right prompt

This creates a right-justified variable-sized field `%*s` and sets its size to the current number of columns of the terminal `$COLUMNS`.

#### Arbitrary positioning

The `cup` capability moves the cursor to a specific position on the screen, for example `tput cup 20 5` moves the cursor to line 20, column 5 (where 0 0 is the top left corner). `cuu`, `cud`, `cuf`, and `cub` (up, down, forward, back) move the cursor relative to its current position. For example `tput cuf 10` moves the cursor 10 characters to the right. You can use the `LINES` and `COLUMNS` variables in the arguments to move the cursor relative to the bottom and right edges. For example, to move 10 lines and 5 columns away from the bottom right corner:

```
$ tput cup $((LINES - 11)) $((COLUMNS - 6))

```

### Customizing the terminal window title

The terminal window title can be customized in much the same way as the prompt: by printing escape sequences in the shell. Thus it is common for users to include window title customizations in their prompt. Although this is technically a feature of xterm, many modern terminals support it. The escape sequence to use is `**ESC**]2;*new title***BEL**` where `**ESC**` and `**BEL**` are the escape and bell characters. Using [#Bash escape sequences](#Bash_escape_sequences), changing the title in your prompt looks like

```
PS1='\[\e]2;*new title*\a\]prompt > '

```

Of course your window title string can include output from [embedding commands](#Embedding_commands) or variables such as `$PWD`, so that the title changes with each command.

## See also

*   Community examples and screenshots in the Forum thread: [What's your PS1?](https://bbs.archlinux.org/viewtopic.php?id=50885) (only accessible if logged in)
*   [Gentoo's `/etc/bash/bashrc`](https://gitweb.gentoo.org/repo/gentoo.git/tree/app-shells/bash/files/bashrc). See also [gentoo-bashrc](https://aur.archlinux.org/packages/gentoo-bashrc/).
*   [tput(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tput.1)
    *   [tput reference on bash-hackers.org](http://wiki.bash-hackers.org/scripting/terminalcodes)
    *   [Colours and Cursor Movement With tput](http://tldp.org/HOWTO/Bash-Prompt-HOWTO/x405.html)
*   [Bash Prompt HOWTO](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html)
*   [Giles Orr's collection of sample prompts](http://gilesorr.com/bashprompt/prompts/index.html)
*   [Bash tips: Colors and formatting](http://misc.flogisoft.com/bash/tip_colors_and_formatting)
*   [Liquid Prompt — a useful adaptive prompt for Bash & zsh](https://github.com/nojhan/liquidprompt)
*   [Bash POWER PROMPT](https://www.askapache.com/linux/bash-power-prompt/)
*   [Wikipedia:ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code "wikipedia:ANSI escape code")
*   [GNU Bash manual: Controlling the Prompt](https://www.gnu.org/software/bash/manual/html_node/Controlling-the-Prompt.html)