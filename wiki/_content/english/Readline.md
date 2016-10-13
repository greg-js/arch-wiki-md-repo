**Readline** is a library by the [GNU Project](/index.php/GNU_Project "GNU Project"), used by [Bash](/index.php/Bash "Bash") and other CLI-interface programs to edit and interact with the command line. Before reading this page please refer to the library home [page](http://www.gnu.org/s/readline/) as only subtle configuration will be introduced here.

## Contents

*   [1 Editing mode](#Editing_mode)
*   [2 Fast word movement](#Fast_word_movement)
*   [3 History](#History)
*   [4 Faster completion](#Faster_completion)
*   [5 Macros](#Macros)
*   [6 Disabling control echo](#Disabling_control_echo)

## Editing mode

By default Readline uses Emacs style shortcuts for interacting with command line. However, vi style editing interface is also supported. Either way, rich sets of shortcut keys are provided for editing [without using the far-away cursor keys](/index.php/Keyboard_without_cursor_keys "Keyboard without cursor keys").

If you are a [vi](/index.php/Vi "Vi") or [vim](/index.php/Vim "Vim") user, you likely want to put the following line in your `~/.inputrc` to enable vi-like keybindings in all Readline based programs, including bash:

```
set editing-mode vi

```

If you don't want to set it globally above, you can set it for bash only by adding the following line in your `~/.bashrc`:

```
set -o vi

```

You may find either [vi](http://www.catonmat.net/download/bash-vi-editing-mode-cheat-sheet.pdf) or [emacs](http://www.catonmat.net/download/readline-emacs-editing-mode-cheat-sheet.pdf) cheat sheets useful.

## Fast word movement

[Xterm](/index.php/Xterm "Xterm") supports moving between words with `Ctrl+Left` and `Ctrl+Right` [by default](http://stackoverflow.com/a/7783928). To achieve this effect with other terminal emulators, find the correct [terminal codes](http://wiki.bash-hackers.org/scripting/terminalcodes), and bind them to `backward-word` and `forward-word` in `~/.inputrc`.

For example, for [urxvt](/index.php/Urxvt "Urxvt"):

 `~/.inputrc` 
```
"\eOd": backward-word
"\eOc": forward-word
```

## History

Usually, pressing the up arrow key will cause the last command to be shown regardless of the command that has been typed so far. However, users may find it more practical to list only past commands that match the current input.

For example, if the user has typed the following commands:

*   `ls /usr/src/linux-2.6.15-ARCH/kernel/power/Kconfig`
*   `who`
*   `mount`
*   `man mount`

In this situation, when typing `ls` and pressing the up arrow key, current input will be replaced with `man mount`, the last performed command. If the history search has been enabled, only past commands beginning with `ls` (the current input) will be shown, in this case `ls /usr/src/linux-2.6.15-ARCH/kernel/power/Kconfig`.

You can enable the history search mode by adding the following lines to `/etc/inputrc` or `~/.inputrc`:

```
"\e[A":history-search-backward
"\e[B":history-search-forward

```

If you are using vi mode, you can add the following lines to `~/.inputrc` (from [this post](https://bbs.archlinux.org/viewtopic.php?pid=428760#p428760)):

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

Alternatively, one can use reverse-search-history (incremental search) by pressing `Ctrl+R`, which does not search based on previous input but instead jumps backwards in the history buffer as commands are typed in a search term. Pressing `Ctrl+R` again during this mode will display the previous line in the buffer that matches the current search term, while pressing `Ctrl+G` (abort) will cancel the search and restore the current input line. So in order to search through all previous `mount` commands, press `Ctrl+R`, type 'mount' and keep pressing `Ctrl+R` until the desired line is found.

The forward equivalent to this mode is called forward-search-history and is bound to `Ctrl+S` by default. Beware that most terminals override `Ctrl+S` to suspend execution until `Ctrl+Q` is entered. (This is called XON/XOFF flow control). For activating forward-search-history, either disable flow control by issuing:

```
$ stty -ixon

```

or use a different key in `inputrc`. For example, to use `Alt+S` which is not bound by default:

```
"\es":forward-search-history

```

## Faster completion

When performing tab completion, a single tab attempts to partially complete the current word. If no partial completions are possible, a double tab shows all possible completions.

The double tab can be changed to a single tab by setting

 `~/.inputrc` 
```
set show-all-if-unmodified on

```

Or you can set it such that a single tab will perform both steps: partially complete the word *and* show all possible completions if it is still ambiguous:

 `~/.inputrc` 
```
set show-all-if-ambiguous on

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

Now type a line and press `Alt`+`W`. Readline will act as though `Ctrl+E` (end-of-line) had been pressed, appended with ' `# macro`'.

Use any of the existing keybindings within a readline macro, which can be quite useful to automate frequently used idioms. For example, this one makes `Ctrl+Alt+L` append "| less" to the line and run it (`Ctrl+M` is equivalent to `Enter`):

```
"\e\C-l":"\C-e | less\C-m"

```

The next one prefixes the line with 'yes |' when pressing `Ctrl+Alt+Y`, confirming any yes/no question the command might ask:

```
"\e\C-y":"\C-ayes | \C-m"

```

This example wraps the line in `su -c ''`, if `Alt+S` is pressed:

```
"\es":"\C-a su -c '\C-e'\C-m"

```

This example prefixes the line with `sudo` , if `Alt+S` is pressed. It's safer because it won't input the `Enter` key.

```
"\es":"\C-asudo \C-e"

```

As a last example, quickly send a command in the background with `Ctrl+Alt+B`, discarding all of its output:

```
"\e\C-b":"\C-e > /dev/null 2>&1 &\C-m"

```

## Disabling control echo

Due to an update to [readline](https://www.archlinux.org/packages/?name=readline), the terminal now echoes `^C` after `Ctrl+C` is pressed. For users who wish to disable this, simply add the following to `~/.inputrc`:

```
set echo-control-characters off

```