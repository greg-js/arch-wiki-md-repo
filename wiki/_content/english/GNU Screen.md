[GNU Screen](http://www.gnu.org/s/screen/) is a wrapper that allows separation between the text program and the shell from which it was launched. This allows the user to, for example, start a text program in a terminal in X, kill X, and continue to interact with the program.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Common Commands](#Common_Commands)
    *   [2.2 Command Prompt Commands](#Command_Prompt_Commands)
    *   [2.3 Named sessions](#Named_sessions)
    *   [2.4 Autostart with systemd](#Autostart_with_systemd)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Change the escape key](#Change_the_escape_key)
    *   [3.2 Start at window 1](#Start_at_window_1)
    *   [3.3 Nested Screen Sessions](#Nested_Screen_Sessions)
    *   [3.4 Use 256 colors](#Use_256_colors)
    *   [3.5 Informative statusbar](#Informative_statusbar)
    *   [3.6 Turn welcome message off](#Turn_welcome_message_off)
    *   [3.7 Turn your hardstatus line into a dynamic urxvt|xterm|aterm window title](#Turn_your_hardstatus_line_into_a_dynamic_urxvt.7Cxterm.7Caterm_window_title)
    *   [3.8 Use X scrolling mechanism](#Use_X_scrolling_mechanism)
    *   [3.9 Attach an existing running program to screen](#Attach_an_existing_running_program_to_screen)
    *   [3.10 Setting a different bash prompt while in screen](#Setting_a_different_bash_prompt_while_in_screen)
    *   [3.11 Turn off visual bell](#Turn_off_visual_bell)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Fix Midnight Commander hard hang when starting in screen](#Fix_Midnight_Commander_hard_hang_when_starting_in_screen)
    *   [4.2 Fix for residual editor text](#Fix_for_residual_editor_text)
    *   [4.3 Fix for Name column in windowlist only show "bash"](#Fix_for_Name_column_in_windowlist_only_show_.22bash.22)
*   [5 See also](#See_also)

## Installation

GNU Screen can be [installed](/index.php/Pacman "Pacman") using the [screen](https://www.archlinux.org/packages/?name=screen) package found in the [official repositories](/index.php/Official_repositories "Official repositories").

## Usage

Commands are entered pressing `ctrl+a` and then the key binding.

### Common Commands

*   `ctrl+a` `?` Displays commands and its defaults (VERY important)
*   `ctrl+a` `:` Enter to the command prompt of screen
*   `ctrl+a` `"` Window list
*   `ctrl+a` `0` opens window 0
*   `ctrl+a` `A` Rename the current window
*   `ctrl+a` `a` Sends `ctrl+a` to the current window
*   `ctrl+a` `c` Create a new window (with shell)
*   `ctrl+a` `S` Split current region into two regions
*   `ctrl+a` `tab` Switch the input focus to the next region
*   `ctrl+a` `ctrl+a` Toggle between current and previous region
*   `ctrl+a` `Esc` Enter Copy Mode (use enter to select a range of text)
*   `ctrl+a` `]` Paste text
*   `ctrl+a` `Q` Close all regions but the current one
*   `ctrl+a` `X` Close the current region
*   `ctrl+a` `d` Detach from the current screen session, and leave it running. Use `screen -r` to resume

### Command Prompt Commands

*   `ctrl+a` `:quit` Closes all windows and closes screen session
*   `ctrl+a` `:source ~/.screenrc` Reloads screenrc configuration file (can alternatively use /etc/screenrc)

### Named sessions

To create a named session, run screen with the following command:

```
$ screen -S *session_name*

```

To (re)name an existing a session, run the following command while screen is running:

`ctrl+a` `:sessionname *session_name*`

To print a list of *pid.tty.host* strings identifying your screen sessions:

```
$ screen -list

```

To attach to a named screen session, run this command:

```
$ screen -x *session_name*

```

or

```
$ screen -r *session_name*

```

### Autostart with systemd

This service autostarts screen for the specified user (e.g. `systemctl enable screen@florian`). Running this as a system unit is important, because [systemd --user](/index.php/Systemd/User "Systemd/User") instance is not guaranteed to be running and will be killed when the last session for given user is closed.

 `/etc/systemd/system/screen@.service` 
```
[Unit]
Description=screen
After=network.target

[Service]
Type=simple
User=%i
ExecStart=/usr/bin/screen -DmS autoscreen
ExecStop=/usr/bin/screen -S autoscreen -X quit

[Install]
WantedBy=multi-user.target

```

## Tips and tricks

### Change the escape key

The escape key can be changed with the `escape` option in `~/.screenrc`. For example:

 `escape ``` 

sets the escape key to ``` and

 `escape ^^^` 

sets it to `ctrl+^`.

### Start at window 1

By default, the first screen window is 0\. If you'd rather never have a window 0 and start instead with 1, add the following lines on your configuration:

 `~/.screenrc` 
```
bind c screen 1
bind ^c screen 1
bind 0 select 10                                                            
screen 1

```

### Nested Screen Sessions

It is possible to get stuck in a nested screen session. A common scenario: you start an ssh session from within a screen session. Within the ssh session, you start screen. By default, the outer screen session that was launched first responds to `ctrl+a` commands. To send a command to the inner screen session, use `ctrl+a` `a`, followed by your command. For example:

*   `ctrl+a` `a` `d` Detaches the inner screen session.
*   `ctrl+a` `a` `K` Kills the inner screen session.

### Use 256 colors

By default, screen uses an 8-color terminal emulator. To enable more colors, you need to be using a terminal that supports them and set the correct [term](http://aperiodic.net/screen/commands:term) value. This will use [terminfo](https://en.wikipedia.org/wiki/Terminfo "wikipedia:Terminfo") to describe how the [ANSI escape codes](https://en.wikipedia.org/wiki/ANSI_escape_code "wikipedia:ANSI escape code") will be interpreted. An entry in the terminfo database structure must exist, [ncurses](https://www.archlinux.org/packages/?name=ncurses) provides many common descriptions stored under `/usr/share/terminfo/`.

First try the generic value:

 `~/.screenrc` 
```
term screen-256color

```

If that does not work, try setting it based on the used terminal. When using [xterm](/index.php/Xterm "Xterm")-based terminal:

 `~/.screenrc` 
```
term xterm-256color

```

When using [rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode"):

 `~/.screenrc` 
```
term rxvt-unicode-256color

```

**Note:** `/usr/share/terminfo/r/rxvt-unicode-256color` is provided by [rxvt-unicode-terminfo](https://www.archlinux.org/packages/?name=rxvt-unicode-terminfo), which is installed as a dependency of [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode). However, if you log into a server via [SSH](/index.php/SSH "SSH") and run *screen* there, this terminfo file might not be available on the server. In this case it is recommended to copy `/usr/share/terminfo/r/rxvt-unicode-256color` on the server, it can be saved in `~/.terminfo`.

As a last resort, try setting [termcapinfo](http://aperiodic.net/screen/commands:termcapinfo) instead:

 `~/.screenrc` 
```
attrcolor b ".I"    # allow bold colors - necessary for some reason
termcapinfo xterm 'Co#256:AB=\E[48;5;%dm:AF=\E[38;5;%dm'   # tell screen how to set colors. AB = background, AF=foreground
defbce on    # use current bg color for erased chars

```

### Informative statusbar

The default statusbar may be a little lacking. You may find this one more helpful:

 `~/.screenrc` 
```
hardstatus off
hardstatus alwayslastline
hardstatus string '%{= kG}[ %{G}%H %{g}][%= %{= kw}%?%-Lw%?%{r}(%{W}%n*%f%t%?(%u)%?%{r})%{w}%?%+Lw%?%?%= %{g}][%{B} %m-%d %{W} %c %{g}]'

```

Another possibility, taken from [frodfrog's blog](http://www.fordfrog.com/2012/09/02/71/) is:

 `~/.screenrc` 
```
hardstatus alwayslastline '%{= G}[ %{G}%H %{g}][%= %{= w}%?%-Lw%?%{= R}%n*%f %t%?%{= R}(%u)%?%{= w}%+Lw%?%= %{= g}][ %{y}Load: %l %{g}][%{B}%Y-%m-%d %{W}%c:%s %{g}]'

```

### Turn welcome message off

 `~/.screenrc` 
```
startup_message off

```

### Turn your hardstatus line into a dynamic urxvt|xterm|aterm window title

This one is pretty simple; just switch your current `hardstatus` line into a `caption` line with notification, and edit accordingly:

 `~/.screenrc` 
```
backtick 1 5 5 true
termcapinfo rxvt* 'hs:ts=\E]2;:fs=\007:ds=\E]2;\007'
hardstatus string "screen (%n: %t)"
caption string "%{= kw}%Y-%m-%d;%c %{= kw}%-Lw%{= kG}%{+b}[%n %t]%{-b}%{= kw}%+Lw%1`"
caption always

```

This will give you something like `screen (0 bash)` in the title of your terminal emulator. The caption supplies the date, current time, and colorizes your screen window collection.

### Use X scrolling mechanism

The scroll buffer of GNU Screen can be accessed with `ctrl+a` `[`. However, this is very inconvenient. To use the scroll bar of e.g. xterm or konsole, add the following line:

 `~/.screenrc` 
```
termcapinfo xterm* ti@:te@

```

### Attach an existing running program to screen

If you started a program outside screen, but now you would like it to be inside, you can use **reptyr** to reparent the process from it's current tty to one inside screen.

[Install](/index.php/Install "Install") the package [reptyr](https://www.archlinux.org/packages/?name=reptyr) from the [official repositories](/index.php/Official_repositories "Official repositories").

Get the PID of the process (you can use `ps ax` for that). Now just enter the PID as argument to reptyr inside a screen window.

 `$ reptyr *<pid>*` 

### Setting a different bash prompt while in screen

If you want a different bash prompt when in a screen session, add the following to your .bashrc:

```
if [ -z $STY ]
then
        PS1="YOUR REGULAR PROMPT"
else  
        PS1="YOUR SCREEN PROMPT"
fi

```

[[1]](http://serverfault.com/questions/257975/how-to-check-if-im-in-screen-session)

### Turn off visual bell

With this setting, screen will not make an ugly screen flash instead of a bell sound.

 `~/.screenrc` 
```
vbell off

```

## Troubleshooting

### Fix Midnight Commander hard hang when starting in screen

In some cases (need deeper inspection) [old gpm bug](https://bugzilla.redhat.com/show_bug.cgi?id=168076) gets alive. So, then you try to run mc inside screen, you get a frozen screen window. Try to kill gpm daemon before starting mc and/or disable it in `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`.

### Fix for residual editor text

When you open a text editor like nano in screen and then close it, the text may stay visible in your terminal. To fix this, put the following:

 `~/.screenrc` 
```
altscreen on

```

### Fix for Name column in windowlist only show "bash"

add following to ~/.screenrc

 `~/.screenrc`  `windowlist string "%4n %h%=%f"` 

## See also

*   [MacOSX Hints - Automatically using screen in your shell](http://www.macosxhints.com/article.php?story=20021114055617124)
*   [Gentoo Wiki - Tutorial for screen](http://wiki.gentoo.org/wiki/Screen)
*   [Arch Forums - Regarding 256 color issue with urxvt](https://bbs.archlinux.org/viewtopic.php?id=50647)
*   [Arch Forums - .screenrc configs with screenshots](https://bbs.archlinux.org/viewtopic.php?id=55618)
*   [Ratpoison - A window manager based on gnu screen](/index.php/Ratpoison "Ratpoison")
*   [Xpra - An utility to detach/reattach X programs, in a way similar as screen does for command line based programs](/index.php/Xpra "Xpra")