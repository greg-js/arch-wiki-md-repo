# Color Bash Prompt

You can add colors and additional information to the [Bash](/index.php/Bash "Bash")'s prompt (PS1) to increase productivity and make the prompt stand out.

This article shows how to _customize the personal prompt of a regular user_.

## Contents

*   [1 Prompts](#Prompts)
*   [2 Techniques](#Techniques)
    *   [2.1 Bash escape sequences](#Bash_escape_sequences)
    *   [2.2 Terminfo escape sequences](#Terminfo_escape_sequences)
    *   [2.3 ANSI escape sequences](#ANSI_escape_sequences)
    *   [2.4 Embedding commands](#Embedding_commands)
    *   [2.5 PROMPT_COMMAND](#PROMPT_COMMAND)
    *   [2.6 Escapes between command input and output](#Escapes_between_command_input_and_output)
*   [3 Basic prompts](#Basic_prompts)
    *   [3.1 Regular user](#Regular_user)
    *   [3.2 Root](#Root)
*   [4 Professional prompts](#Professional_prompts)
    *   [4.1 Regular user](#Regular_user_2)
    *   [4.2 Root](#Root_2)
*   [5 Ultimate prompts](#Ultimate_prompts)
    *   [5.1 Load/Mem Status for 256colors](#Load.2FMem_Status_for_256colors)
    *   [5.2 List of colors for prompt and Bash](#List_of_colors_for_prompt_and_Bash)
    *   [5.3 Positioning the cursor](#Positioning_the_cursor)
    *   [5.4 Return value visualisation](#Return_value_visualisation)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Random quotations at logon](#Random_quotations_at_logon)
    *   [6.2 Colors overview](#Colors_overview)
    *   [6.3 Colorized git prompt](#Colorized_git_prompt)
*   [7 See also](#See_also)

## Prompts

Bash has four prompts that can be customized:

*   `PS1` is the primary prompt which is displayed before each command, thus it is the one most people customize.
*   `PS2` is the secondary prompt displayed when a command needs more input (e.g. a multi-line command).
*   `PS3` is not very commonly used. It is the prompt displayed for Bash's `select` built-in which displays interactive menus. Unlike the other prompts, it does not expand [Bash escape sequences](#Bash_escape_sequences). Usually you would customize it in the script where the `select` is used rather than in your `.bashrc`.
*   `PS4` is also not commonly used. It is displayed when debugging bash scripts to indicate levels of indirection. The first character is repeated to indicate deeper levels.

All of the prompts are customized by setting the corresponding variable to the desired string (usually in `~/.bashrc`), for example

```
export PS2='> '

```

## Techniques

While one can simply set their prompt to a plain string, there are a variety of techniques for making the prompt more dynamic and useful.

### Bash escape sequences

When printing the prompt string, Bash looks for certain backslash-escaped characters and will expand them into special strings. For example, `\u` is expanded into the current username and `\A` is expanded to the current time. So a PS1 of `'\A \u $ '` would be printed like `17:35 _username_ $` .

Check the "PROMPTING" section of the Bash man page for a complete list of escape sequences.

### Terminfo escape sequences

Aside from the escape characters recognized by Bash, most terminals recognize special escape sequences that affect the terminal itself rather than printing characters. For example they might change the color of subsequent printed characters, move the cursor to an arbitrary location, or clear the screen. These escape sequences can be somewhat illegible and can vary from terminal to terminal, so they are documented in the terminfo database. To see what capabilities your terminal supports, run

```
$ infocmp $TERM

```

The capability names (the part before the =) can be looked up in the terminfo man page for a description of what they do. For example, `setaf` sets the foreground color of whatever text is printed after it. To get the escape code for a capability, you can use the `tput` command. For example

```
$ tput setaf 2

```

prints the escape sequence to set the foreground color to green.

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

**Warning:** PROMPT_COMMAND generally should not be used to print characters directly to the prompt. Bash keeps track of the size of PS1 so that it can correctly move the cursor and clear characters; it does not count characters printed outside of PS1\. This can cause strange behavior and overwritten text. Either use PROMPT_COMMAND to set PS1 or look at [embedding commands](#Embedding_commands).

### Escapes between command input and output

You can affect your input text in Bash by not resetting the text properties at the end of your PS1\. For example, inserting `tput blink` at the end of your PS1 will make your typed commands blink. However this effect will also continue through the command's output since the text properties are not reset when you hit Enter.

In order to insert escape sequences after you type a command but before the output is displayed, you can trap Bash's DEBUG signal, which is sent right before each command is executed:

 `~/.bashrc`  `trap 'tput sgr0' DEBUG` 

## Basic prompts

The following settings are useful for distinguishing the root prompt from non-root users.

### Regular user

A green prompt for _regular users_:

[chiri@zetsubou ~]$ _

 `~/.bashrc` 

```
#PS1='[\u@\h \W]\$ '  # Default
PS1='\[\e[1;32m\][\u@\h \W]\$\[\e[0m\] '
```

### Root

A red prompt for _root_ (copy from `/etc/skel/`, if not already):

[root@zetsubou ~]# _

 `/root/.bashrc` 

```
#PS1='[\u@\h \W]\$ '  # Default
PS1='\[\e[1;31m\][\u@\h \W]\$\[\e[0m\] '
```

**Note:** Also copy `.bash_profile` from `/etc/skel/` to `/root/`, to make sure that your colours persist in su shells.

## Professional prompts

The following settings provides more professional prompts.

### Regular user

A green/blue prompt for _regular users_:

chiri ~/docs $ echo "sample output text"
sample output text
chiri ~/docs $ _

 `PS1='\[\e[0;32m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[1;32m\]\$\[\e[m\] \[\e[1;37m\]'` 

This will give a very pleasing, colorful prompt and theme for the console with bright white text.

The string above contains color-set escape sequences (start coloring: `\[\e[_color_\]`, end coloring: `\[\e[m\]`) and information placeholders:

*   **\u** - Username. The original prompt also has **\h**, which prints the host name.
*   **\w** - Current absolute path. Use **\W** for current relative path.
*   **\$** - The prompt character (eg. `#` for root, `$` for regular users).
*   **\[** and **\]** - These tags should be placed around color codes so bash knows how to properly place the cursor.

The last color-set sequence, `\[\e[1;37m\]`, is not closed, so the remaining text (everything typed into the terminal, program output and so on) will be in that (bright white) color. It may be desirable to change this color, or to delete the last escape sequence in order to leave the actual output in unaltered color.

### Root

A red/blue prompt for _root_:

root ~/docs # echo "sample output text"
sample output text
root ~/docs # _

 `PS1='\[\e[0;31m\]\u\[\e[m\] \[\e[1;34m\]\w\[\e[m\] \[\e[0;31m\]\$ \[\e[m\]\[\e[0;32m\]'` 

This will give you a red designation and green console text.

## Ultimate prompts

### Load/Mem Status for 256colors

This is not even pushing the limits. Other than using `sed` to parse the memory and load average (using the `-u` option for non-buffering), and the builtin _history_ to save your history to your `HISTFILE` after every command, which you may find incredibly useful when dealing with crashing shells or subshells, this is essentially just making BASH print variables it already knows, making this extremely fast compared to prompts with non-builtin commands.

This prompt is from AskApache.com's [BASH Power Prompt article](http://www.askapache.com/linux-unix/bash-power-prompt.html), which goes into greater detail. It is especially helpful for those wanting to understand 256 color terminals, ncurses, termcap, and terminfo.

This is for **256 color terminals**, which is where the `\033[38;5;22m` terminal escapes come from.

```
802/1024MB      1.28 1.20 1.13 3/94 18563
[5416:17880 0:70] 05:35:50 Wed Apr 21 [srot@host.sqpt.net:/dev/pts/0 +1] ~

(1:70)$ _
```

```
PROMPT_COMMAND='history -a;echo -en "\033[m\033[38;5;2m"$(( $(sed -nu "s/MemFree:[\t ]\+\([0-9]\+\) kB/\1/p" /proc/meminfo)/1024))"\033[38;5;22m/"$(($(sed -nu "s/MemTotal:[\t ]\+\([0-9]\+\) kB/\1/Ip" /proc/meminfo)/1024 ))MB"\t\033[m\033[38;5;55m$(< /proc/loadavg)\033[m"'
PS1='\[\e[m\n\e[1;30m\][$$:$PPID \j:\!\[\e[1;30m\]]\[\e[0;36m\] \T \d \[\e[1;30m\][\[\e[1;34m\]\u@\H\[\e[1;30m\]:\[\e[0;37m\]${SSH_TTY} \[\e[0;32m\]+${SHLVL}\[\e[1;30m\]] \[\e[1;37m\]\w\[\e[0;37m\] \n($SHLVL:\!)\$ '
```

### List of colors for prompt and Bash

Add this to your Bash file(s) to define colors for prompt and commands:

```
txtblk='\e[0;30m' # Black - Regular
txtred='\e[0;31m' # Red
txtgrn='\e[0;32m' # Green
txtylw='\e[0;33m' # Yellow
txtblu='\e[0;34m' # Blue
txtpur='\e[0;35m' # Purple
txtcyn='\e[0;36m' # Cyan
txtwht='\e[0;37m' # White
bldblk='\e[1;30m' # Black - Bold
bldred='\e[1;31m' # Red
bldgrn='\e[1;32m' # Green
bldylw='\e[1;33m' # Yellow
bldblu='\e[1;34m' # Blue
bldpur='\e[1;35m' # Purple
bldcyn='\e[1;36m' # Cyan
bldwht='\e[1;37m' # White
unkblk='\e[4;30m' # Black - Underline
undred='\e[4;31m' # Red
undgrn='\e[4;32m' # Green
undylw='\e[4;33m' # Yellow
undblu='\e[4;34m' # Blue
undpur='\e[4;35m' # Purple
undcyn='\e[4;36m' # Cyan
undwht='\e[4;37m' # White
bakblk='\e[40m'   # Black - Background
bakred='\e[41m'   # Red
bakgrn='\e[42m'   # Green
bakylw='\e[43m'   # Yellow
bakblu='\e[44m'   # Blue
bakpur='\e[45m'   # Purple
bakcyn='\e[46m'   # Cyan
bakwht='\e[47m'   # White
txtrst='\e[0m'    # Text Reset
```

Or if you prefer color names you will know how to spell without a special decoder ring and want high intensity colors:

```
# Reset
Color_Off='\e[0m'       # Text Reset

# Regular Colors
Black='\e[0;30m'        # Black
Red='\e[0;31m'          # Red
Green='\e[0;32m'        # Green
Yellow='\e[0;33m'       # Yellow
Blue='\e[0;34m'         # Blue
Purple='\e[0;35m'       # Purple
Cyan='\e[0;36m'         # Cyan
White='\e[0;37m'        # White

# Bold
BBlack='\e[1;30m'       # Black
BRed='\e[1;31m'         # Red
BGreen='\e[1;32m'       # Green
BYellow='\e[1;33m'      # Yellow
BBlue='\e[1;34m'        # Blue
BPurple='\e[1;35m'      # Purple
BCyan='\e[1;36m'        # Cyan
BWhite='\e[1;37m'       # White

# Underline
UBlack='\e[4;30m'       # Black
URed='\e[4;31m'         # Red
UGreen='\e[4;32m'       # Green
UYellow='\e[4;33m'      # Yellow
UBlue='\e[4;34m'        # Blue
UPurple='\e[4;35m'      # Purple
UCyan='\e[4;36m'        # Cyan
UWhite='\e[4;37m'       # White

# Background
On_Black='\e[40m'       # Black
On_Red='\e[41m'         # Red
On_Green='\e[42m'       # Green
On_Yellow='\e[43m'      # Yellow
On_Blue='\e[44m'        # Blue
On_Purple='\e[45m'      # Purple
On_Cyan='\e[46m'        # Cyan
On_White='\e[47m'       # White

# High Intensity
IBlack='\e[0;90m'       # Black
IRed='\e[0;91m'         # Red
IGreen='\e[0;92m'       # Green
IYellow='\e[0;93m'      # Yellow
IBlue='\e[0;94m'        # Blue
IPurple='\e[0;95m'      # Purple
ICyan='\e[0;96m'        # Cyan
IWhite='\e[0;97m'       # White

# Bold High Intensity
BIBlack='\e[1;90m'      # Black
BIRed='\e[1;91m'        # Red
BIGreen='\e[1;92m'      # Green
BIYellow='\e[1;93m'     # Yellow
BIBlue='\e[1;94m'       # Blue
BIPurple='\e[1;95m'     # Purple
BICyan='\e[1;96m'       # Cyan
BIWhite='\e[1;97m'      # White

# High Intensity backgrounds
On_IBlack='\e[0;100m'   # Black
On_IRed='\e[0;101m'     # Red
On_IGreen='\e[0;102m'   # Green
On_IYellow='\e[0;103m'  # Yellow
On_IBlue='\e[0;104m'    # Blue
On_IPurple='\e[0;105m'  # Purple
On_ICyan='\e[0;106m'    # Cyan
On_IWhite='\e[0;107m'   # White

```

To use in commands from your shell environment:

$ echo -e "${txtblu}test"
test
$ echo -e "${bldblu}test"
**test**
$ echo -e "${undblu}test"
**test**
$ echo -e "${bakblu}test"
**test**
$ _

 `PS1="\[$txtblu\]foo\[$txtred\] bar\[$txtrst\] baz : "` 

Double quotes enable `$color` variable expansion and the `\[ \]` escapes around them make them not count as character positions and the cursor position is not wrong.

**Note:** If experiencing premature line wrapping when entering commands, then missing escapes (`\[ \]`) is most likely the reason.

### Positioning the cursor

The following sequence sets the cursor position:

 `\[\033[<row>;<column>f\]` 

The current cursor position can be saved using:

 `\[\033[s\]` 

To restore a position, use the following sequence:

 `\[\033[u\]` 

The following example uses these sequences to display the time in the upper right corner:

 `PS1=">\[\033[s\]\[\033[1;\$((COLUMNS-5))f\]\$(date +%H:%M)\[\033[u\]"` 

The environment variable `COLUMNS` contains the number of columns of the terminal. The above example substracts _5_ from its value in order to justify the five-character wide output of `date` at the right border.

### Return value visualisation

Use the following prompt to see the return value of last command:

0 ;) : true
0 ;) : false
1 ;( :

```
#return value visualisation
PS1="\$? \$(if [[ \$? == 0 ]]; then echo \"\[\033[0;32m\];)\"; else echo \"\[\033[0;31m\];(\"; fi)\[\033[00m\] : "
```

_Zero_ is a green smiley and _non-zero_ a red one. So your prompt will smile if the last operation was successful.

But you will probably want to include the username and hostname as well, like this:

0 ;) andy@alba ~ $ true
0 ;) andy@alba ~ $ false
1 ;( andy@alba ~ $ _

```
#return value visualisation
PS1="\[\033[01;37m\]\$? \$(if [[ \$? == 0 ]]; then echo \"\[\033[01;32m\];)\"; else echo \"\[\033[01;31m\];(\"; fi) $(if [[ ${EUID} == 0 ]]; then echo '\[\033[01;31m\]\h'; else echo '\[\033[01;32m\]\u@\h'; fi)\[\033[01;34m\] \w \$\[\033[00m\] "
```

Or, if you want, you can build your prompt using the ✓ unicode symbol for a _zero_ status and the ✗ unicode symbol for a _nonzero_ status:

0 ✓ andy@alba ~ $ true
0 ✓ andy@alba ~ $ false
1 ✗ andy@alba ~ $ I\ will\ try\ to\ type\ a\ wrong\ command...
bash: I will try to type a wrong command...: command not found
127 ✗ andy@alba ~ $ _

```
#return value visualisation
PS1="\[\033[01;37m\]\$? \$(if [[ \$? == 0 ]]; then echo \"\[\033[01;32m\]\342\234\223\"; else echo \"\[\033[01;31m\]\342\234\227\"; fi) $(if [[ ${EUID} == 0 ]]; then echo '\[\033[01;31m\]\h'; else echo '\[\033[01;32m\]\u@\h'; fi)\[\033[01;34m\] \w \$\[\033[00m\] "
```

Alternatively, this can be made more [readable](http://stackoverflow.com/a/22362727/1821548) with `PROMPT_COMMAND`:

```
set_prompt () {
    Last_Command=$? # Must come first!
    Blue='\[\e[01;34m\]'
    White='\[\e[01;37m\]'
    Red='\[\e[01;31m\]'
    Green='\[\e[01;32m\]'
    Reset='\[\e[00m\]'
    FancyX='\342\234\227'
    Checkmark='\342\234\223'

    # Add a bright white exit status for the last command
    PS1="$White\$? "
    # If it was successful, print a green check mark. Otherwise, print
    # a red X.
    if [[ $Last_Command == 0 ]]; then
        PS1+="$Green$Checkmark "
    else
        PS1+="$Red$FancyX "
    fi
    # If root, just print the host in red. Otherwise, print the current user
    # and host in green.
    if [[ $EUID == 0 ]]; then
        PS1+="$Red\\h "
    else
        PS1+="$Green\\u@\\h "
    fi
    # Print the working directory and prompt marker in blue, and reset
    # the text color to the default.
    PS1+="$Blue\\w \\\$$Reset "
}
PROMPT_COMMAND='set_prompt'
```

Here is an alternative that only includes the error status, if _non-zero_:

```
PROMPT_COMMAND='es=$?; [[ $es -eq 0 ]] && unset error || error=$(echo -e "\e[1;41m $es \e[40m")'
PS1="${error} ${PS1}"
```

## Tips and tricks

### Random quotations at logon

For a brown [Fortune](/index.php/Fortune "Fortune") prompt, add:

 `~/.bashrc` 

```
[[ "$PS1" ]] && echo -e "\e[00;33m$(/usr/bin/fortune)\e[00m"

```

### Colors overview

The page at [http://ascii-table.com/ansi-escape-sequences.php](http://ascii-table.com/ansi-escape-sequences.php) describes the various available color escapes. The following Bash function displays a table with ready-to-copy escape codes.

 `~/.bashrc` 

```
colors() {
	local fgc bgc vals seq0

	printf "Color escapes are %s\n" '\e[${value};...;${value}m'
	printf "Values 30..37 are \e[33mforeground colors\e[m\n"
	printf "Values 40..47 are \e[43mbackground colors\e[m\n"
	printf "Value  1 gives a  \e[1mbold-faced look\e[m\n\n"

	# foreground colors
	for fgc in {30..37}; do
		# background colors
		for bgc in {40..47}; do
			fgc=${fgc#37} # white
			bgc=${bgc#40} # black

			vals="${fgc:+$fgc;}${bgc}"
			vals=${vals%%;}

			seq0="${vals:+\e[${vals}m}"
			printf "  %-9s" "${seq0:-(default)}"
			printf " ${seq0}TEXT\e[m"
			printf " \e[${vals:+${vals+$vals;}}1mBOLD\e[m"
		done
		echo; echo
	done
}

```

### Colorized git prompt

Source `/usr/share/git/completion/git-prompt.sh` for your shell:

 `~/.bashrc` 

```
source /usr/share/git/completion/git-prompt.sh

```

and use `__git_ps1` inside `PS1` or `PROMPT_COMMAND`. See [Don't Reinvent the Wheel](http://ithaca.arpinum.org/2013/01/02/git-prompt.html) for details.

## See also

*   Community examples and screenshots in the Forum thread: [What's your PS1?](https://bbs.archlinux.org/viewtopic.php?id=50885)
*   The original _not modified_ Gentoo's `/etc/bash.bashrc` file can be found [here](http://www.jeremysands.com/archlinux/gentoo-bashrc-2008.0). See also [gentoo-bashrc](https://aur.archlinux.org/packages/gentoo-bashrc/).
*   tput(1)
    *   [tput reference on bash-hackers.org](http://wiki.bash-hackers.org/scripting/terminalcodes)
    *   [Colours and Cursor Movement With tput](http://tldp.org/HOWTO/Bash-Prompt-HOWTO/x405.html)
*   [Nice Xresources color schemes collection](http://xcolors.net/)
*   [Bash Prompt HOWTO](http://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html)
*   [Giles Orr's collection of sample prompts](http://gilesorr.com/bashprompt/prompts/index.html)
*   [Bash tips: Colors and formatting](http://misc.flogisoft.com/bash/tip_colors_and_formatting)
*   [Liquid Prompt — a useful adaptive prompt for Bash & zsh](https://github.com/nojhan/liquidprompt)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Color_Bash_Prompt&oldid=419091](https://wiki.archlinux.org/index.php?title=Color_Bash_Prompt&oldid=419091)"