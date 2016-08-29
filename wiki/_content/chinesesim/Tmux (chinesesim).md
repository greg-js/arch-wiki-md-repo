**翻译状态：** 本文是英文页面 [Tmux](/index.php/Tmux "Tmux") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-6-29，点击[这里](https://wiki.archlinux.org/index.php?title=Tmux&diff=0&oldid=321396)可以查看翻译后英文页面的改动。

[Tmux](http://tmux.github.io/) 是一个终端复用器: 可以激活多个终端或窗口, 在每个终端都可以单独访问，每一个终端都可以访问，运行和控制各自的程序.tmux类似于screen，可以关闭窗口将程序放在后台运行，需要的时候再重新连接。 Tmux是于基于BSD协议发布的 [GNU Screen](/index.php/Screen_Tips "Screen Tips"). 虽然两者类似，但是还是有不同的地方，详情点击 [tmux FAQ page](https://raw.githubusercontent.com/tmux/tmux/master/FAQ)。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 快捷键前缀](#.E5.BF.AB.E6.8D.B7.E9.94.AE.E5.89.8D.E7.BC.80)
        *   [2.1.1 滚动](#.E6.BB.9A.E5.8A.A8)
    *   [2.2 Browsing URL's](#Browsing_URL.27s)
    *   [2.3 Setting the correct term](#Setting_the_correct_term)
    *   [2.4 Other Settings](#Other_Settings)
    *   [2.5 Autostart with systemd](#Autostart_with_systemd)
*   [3 Session initialization](#Session_initialization)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Scrolling issues](#Scrolling_issues)
    *   [4.2 Shift+F6 not working in Midnight Commander](#Shift.2BF6_not_working_in_Midnight_Commander)
*   [5 ICCCM Selection Integration](#ICCCM_Selection_Integration)
    *   [5.1 Urxvt MiddleClick Solution](#Urxvt_MiddleClick_Solution)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Start tmux in urxvt](#Start_tmux_in_urxvt)
    *   [6.2 Start tmux on every shell login](#Start_tmux_on_every_shell_login)
    *   [6.3 Use tmux windows like tabs](#Use_tmux_windows_like_tabs)
    *   [6.4 Clients simultaneously interacting with various windows of a session](#Clients_simultaneously_interacting_with_various_windows_of_a_session)
    *   [6.5 Changing the configuration with tmux started](#Changing_the_configuration_with_tmux_started)
    *   [6.6 Template script to run program in new session resp. attach to existing one](#Template_script_to_run_program_in_new_session_resp._attach_to_existing_one)
    *   [6.7 Terminal emulator window titles](#Terminal_emulator_window_titles)
    *   [6.8 Automatic layouting](#Automatic_layouting)
    *   [6.9 vim friendly configuration](#vim_friendly_configuration)
*   [7 外部链接](#.E5.A4.96.E9.83.A8.E9.93.BE.E6.8E.A5)

## 安装

从[官方源](/index.php/Official_repositories "Official repositories")[安装](/index.php/Pacman "Pacman")软件包[tmux](https://www.archlinux.org/packages/?name=tmux)。

## 配置

用户私人配置文件在`~/.tmux.conf`, 全局配置文件在 `/etc/tmux.conf`，范例配置文件在`/usr/share/tmux/`。

### 快捷键前缀

<caption>*前缀为* `Ctrl-b`</caption>
| 按键 | 动作 |
| c | 创建一个新窗口 |
| n | 切换至下一窗口 |
| p | 切换到上一个窗口 |
| " | 水平分割窗口 |
| % | 垂直分割窗口 |
| , | 重新命令当前窗口 |
| o | 移动至下一个面板 |

默认绑定的前缀按键为Ctrl-b. 比如说垂直分割窗口的快捷键就是 `Ctrl-b %`。

使用多个面板分割窗口后, 先按前缀快捷键(比如说：`Ctrl-b`)然后按住Ctrl键就可以使用方向键调整面板大小。 如果要交换面板也是采用同样的方式，只是按键由方向键换成“O“键。

**Tip:** 如果想要模仿screen的快捷键前缀配置, 可以把 `/usr/share/tmux/screen-keys.conf` 拷贝到上述提到的任一配置文件位置.

快捷键前缀可能会随着`tmux.conf`中的bind和unbind命令而改变. 比如你可以通过在配置文件中增加下面命令,把前缀从(i.e. `Ctrl-b`) 改成 `Ctrl-a` :

```
unbind C-b
set -g prefix C-a
bind C-a send-prefix

```

其他几种在窗口间移动的快捷键:

```
Ctrl-b l (回到上一个选定的窗口)
Ctrl-b w (显示所有的窗口和窗口序号)
Ctrl-b <window number> (移动到指定序号的窗口, 默认序号是 0 – 9)
Ctrl-b q  (显示当前面板号时, 输入指定的面板号可跳转.)

```

如果你打开10个以上的面板怎么办? tmux有寻找窗口的选项和快捷键.

```
Ctrl-b f <window name> (寻找指定名字的窗口)
Ctrl-b w (从交互式列表中选择窗口)

```

#### 滚动

使用下列快捷键可以进入滚动模式:

```
Ctrl-b [

```

这会使你进入滚动模式,然后你可以使用上下键或翻页键进行滚动,翻页.

```
Ctrl-b PageUp

```

这个快捷键会使你立即进入滚动模式,并向上翻页.

### Browsing URL's

To browse URL's inside tmux you must have [urlview](https://aur.archlinux.org/packages/urlview/) installed and configured.

Inside a new terminal:

```
bind-key u capture-pane \; save-buffer /tmp/tmux-buffer \; run-shell "$TERMINAL -e urlview /tmp/tmux-buffer"

```

Or inside a new tmux window (no new terminal needed):

```
bind-key u capture-pane \; save-buffer /tmp/tmux-buffer \; new-window -n "urlview" '$SHELL -c "urlview < /tmp/tmux-buffer"'

```

### Setting the correct term

If you are using a 256 colour terminal, you will need to set the correct term in tmux. You can do this in either the `tmux.conf`:

```
set -g default-terminal "screen-256color" 

```

or in your `.bashrc` with a test like:

```
# for tmux: export 256color
[ -n "$TMUX" ] && export TERM=screen-256color

```

If you enable xterm-keys in your `tmux.conf`, then you need to build a custom terminfo to declare the new escape codes or applications will not know about them. Compile the following with `tic` and you can use "xterm-screen-256color" as your TERM:

```
# A screen- based TERMINFO that declares the escape sequences
# enabled by the tmux config "set-window-option -g xterm-keys".
#
# Prefix the name with xterm- since some applications inspect
# the TERM *name* in addition to the terminal capabilities advertised.
xterm-screen-256color|GNU Screen with 256 colors bce and tmux xterm-keys,

# As of Nov'11, the below keys are picked up by
# .../tmux/blob/master/trunk/xterm-keys.c:
	kDC=\E[3;2~, kEND=\E[1;2F, kHOM=\E[1;2H,
	kIC=\E[2;2~, kLFT=\E[1;2D, kNXT=\E[6;2~, kPRV=\E[5;2~,
	kRIT=\E[1;2C,

# Change this to screen-256color if the terminal you run tmux in
# doesn't support bce:
	use=screen-256color-bce,

```

### Other Settings

Set scrollback to 10000 lines with

```
set -g history-limit 10000

```

### Autostart with systemd

There are some notable advantages to starting a tmux server at startup. Notably, when you start a new tmux session, having the service already running reduces any delays in the startup.

Furthermore, any customization attached to your tmux session will be retained and your tmux session can be made to persist even if you have never logged in, if you have some reason to do that (like a heavily scripted tmux configuration or shared user tmux sessions).

The service below starts tmux for the specified user (i.e. start with `tmux@*username*.service`):

 `/etc/systemd/system/tmux@.service` 
```
[Unit]
Description=Start tmux in detached session

[Service]
Type=forking
User=%I
ExecStart=/usr/bin/tmux new-session -s %u -d
ExecStop=/usr/bin/tmux kill-session -t %u

[Install]
WantedBy=multi-user.target

```

**Tip:** You may want to add `WorkingDirectory=*custom_path*` to customize working directory.

Alternatively, you can place this file within your [systemd/User](/index.php/Systemd/User "Systemd/User") directory, for example `~/.config/systemd/user/tmux.service`. This way the tmux service will start when you log in.

## Session initialization

You can have tmux open a session with preloaded windows by including those details in your `~/.tmux.conf`:

```
new  -n WindowName Command
neww -n WindowName Command
neww -n WindowName Command

```

To start a session with split windows (multiple panes), include the splitw command below the neww you would like to split; thus:

```
new  -s SessionName -n WindowName Command
neww -n foo/bar foo
splitw -v -p 50 -t 0 bar
selectw -t 1 
selectp -t 0

```

would open 2 windows, the second of which would be named foo/bar and would be split vertically in half (50%) with foo running above bar. Focus would be in window 2 (foo/bar), top pane (foo).

**Note:** Numbering for sessions, windows and panes starts at zero, unless you have specified a base-index of 1 in your `.conf`

To manage multiple sessions, source separate session files from your conf file:

```
# initialize sessions
bind F source-file ~/.tmux/foo
bind B source-file ~/.tmux/bar

```

## Troubleshooting

### Scrolling issues

If you have issues scrolling with Shift-PageUp/Shift-PageDown in your terminal, try this:

```
set -g terminal-overrides 'xterm*:smcup@:rmcup@'

```

### Shift+F6 not working in Midnight Commander

If the `Shift+F6` key combination is not working with either `TERM=screen` or `TERM=screen-256color`, then from inside tmux, run this command:

```
infocmp > screen (or screen-256color)

```

Open the file in a text editor, and add the following to the bottom of that file:

```
kf16=\E[29~,

```

Then compile the file with `tic`. The keys should be working now.

## ICCCM Selection Integration

It is possible to copy a tmux paste buffer to an ICCCM selection, and vice-versa, by defining a shell command which interfaces tmux with an X11 selection interface. The following tmux config file snippet effectively integrates `CLIPBOARD` with the current tmux paste buffer using xclip:

 `~/.tmux.conf` 
```
...
##CLIPBOARD selection integration
##Requires prefix key before the command key
#Copy tmux paste buffer to CLIPBOARD
bind C-c run "tmux save-buffer - | xclip -i -selection clipboard"
#Copy CLIPBOARD to tmux paste buffer and paste tmux paste buffer
bind C-v run "tmux set-buffer -- \"$(xclip -o -selection clipboard)\"; tmux paste-buffer"

```

As alternative you can use `xsel`:

 `~/.tmux.conf` 
```
...
##CLIPBOARD selection integration
##Requires prefix key before the command key
#Copy tmux paste buffer to CLIPBOARD
bind C-c run "tmux show-buffer | xsel -i -b"
#Copy CLIPBOARD to tmux paste buffer and paste tmux paste buffer
bind C-v run "tmux set-buffer -- \"$(xsel -o -b)\"; tmux paste-buffer"

```

It seems `xclip` does not close `STDOUT` after it has read from `tmux`'s buffer. As such, `tmux` doesn't know that the copy task has completed, and continues to /await `xclip`'s termination, thereby rendering the window manager unresponsive. To work around this, you can execute the command via `run-shell -b` instead of `run`, you can redirect `STDOUT` of `xclip` to `/dev/null`, or you can use an alternative command like `xsel`.

### Urxvt MiddleClick Solution

**Note:** To use this, you need to enable mouse support

There is an unofficial perl extension (mentioned in the official [FAQ](http://sourceforge.net/p/tmux/tmux-code/ci/master/tree/FAQ)) to enable copying/pasting in and out of urxvt with tmux via Middle Mouse Clicking.

First, you will need to download the perl script and place it into urxvts perl lib:

```
wget [http://anti.teamidiot.de/static/nei/*/Code/urxvt/osc-xterm-clipboard](http://anti.teamidiot.de/static/nei/*/Code/urxvt/osc-xterm-clipboard)
mv osc-xterm-clipboard /usr/lib/urxvt/perl/
```

You will also need to enable that perl script in your .Xdefaults:

 `~/.Xdefaults` 
```
...
*URxvt.perl-ext-common:		osc-xterm-clipboard
...

```

Next, you want to tell tmux about the new function and enable mouse support (if you haven't already). The third option is optional, to enable scrolling and selecting inside panes with your mouse:

 `~/.tmux.conf` 
```
...
set-option -ga terminal-override ',rxvt-uni*:XT:Ms=\E]52;%p1%s;%p2%s\007'
set-window-option -g mode-mouse on
set-option -g mouse-select-pane on
...

```

That's it. Be sure to end all instances of tmux before trying the new MiddleClick functionality.

While in tmux, Shift+MiddleMouseClick will paste the clipboard selection while just MiddleMouseClick will paste your tmux buffer. Outside of tmux, just use MiddleMouseClick to paste your tmux buffer and your standard Ctrl-c to copy.

**Note:** The current tmux version 1.8-1 has a bug where it sometimes might not be possible to paste tmux buffer between different panes of tmux. This behaviour is fixed in the git-version (2013.10.15)

## Tips and tricks

### Start tmux in urxvt

Use this command to start urxvt with a started tmux session. I use this with the exec command from my .ratpoisonrc file.

 `urxvt -e bash -c "tmux -q has-session && exec tmux attach-session -d || exec tmux new-session -n$USER -s$USER@$HOSTNAME"` 

### Start tmux on every shell login

Simply add the following line of bash code to your .bashrc before your aliases; the code for other shells is very similar:

 `[[ -z "$TMUX" ]] && exec tmux`  `~/.bashrc` 
```
# If not running interactively, do not do anything
[[ $- != *i* ]] && return
[[ -z "$TMUX" ]] && exec tmux

```

**Note:** This snippet ensures that tmux is not launched inside of itself (something tmux usually already checks for anyway). tmux sets $TMUX to the socket it is using whenever it runs, so if $TMUX isn't set or is length 0, we know we aren't already running tmux.

And this snippet start only one session(unless you start some manually), on login, try attach at first, only create a session if no tmux is running.

```
# TMUX
if which tmux 2>&1 >/dev/null; then
    #if not inside a tmux session, and if no session is started, start a new session
    test -z "$TMUX" && (tmux attach || tmux new-session)
fi

```

This snippet does the same thing, but also checks tmux is installed before trying to launch it. It also tries to reattach you to an existing tmux session at logout, so that you can shut down every tmux session quickly from the same terminal at logout.

```
# TMUX
if which tmux 2>&1 >/dev/null; then
    # if no session is started, start a new session
    test -z ${TMUX} && tmux

    # when quitting tmux, try to attach
    while test -z ${TMUX}; do
        tmux attach || break
    done
fi

```

Another possibility is to try to attach to existing deattached session or start a new session:

```
if [[ -z "$TMUX" ]] ;then
    ID="`tmux ls | grep -vm1 attached | cut -d: -f1`" # get the id of a deattached session
    if [[ -z "$ID" ]] ;then # if not available create a new one
        tmux new-session
    else
        tmux attach-session -t "$ID" # if available attach to it
    fi
fi

```

**Note:** Instead of using the bashrc file, you can launch tmux when you start your terminal emulator. (i. e. urxvt -e tmux)

### Use tmux windows like tabs

The following settings added to `~/.tmux.conf` allow to use tmux windows like tabs, such as those provided by the reference of these hotkeys — [urxvt's tabbing extensions](/index.php/Rxvt-unicode#urxvtq_with_tabbing "Rxvt-unicode"). An advantage thereof is that these virtual “tabs” are independent of the terminal emulator.

```
#urxvt tab like window switching (-n: no prior escape seq)
bind -n S-down new-window
bind -n S-left prev
bind -n S-right next
bind -n C-left swap-window -t -1
bind -n C-right swap-window -t +1

```

Of course, those should not overlap with other applications' hotkeys, such as the terminal's. Given that they substitute terminal tabbing that might as well be deactivated, though.

It can also come handy to supplement the EOT hotkey `Ctrl+d` with one for tmux's detach:

```
bind-key -n C-j detach

```

### Clients simultaneously interacting with various windows of a session

In [Practical Tmux](http://mutelight.org/articles/practical-tmux), Brandur Leach writes:

	Screen and tmux's behaviour for when multiple clients are attached to one session differs slightly. In Screen, each client can be connected to the session but view different windows within it, but in tmux, all clients connected to one session must view the same window.

	This problem can be solved in tmux by spawning two separate sessions and synchronizing the second one to the windows of the first, then pointing a second new session to the first.

The script “`tmx`” below implements this — the version here is slightly modified to execute “`tmux new-window`” if “1” is its second parameter. Invoked as `tmx <base session name> [1]` it launches the base session if necessary. Otherwise a new “client” session linked to the base, optionally add a new window and attach, setting it to kill itself once it turns “zombie”.

 `tmx` 
```
#!/bin/bash

#
# Modified TMUX start script from:
#     http://forums.gentoo.org/viewtopic-t-836006-start-0.html
#
# Store it to `~/bin/tmx` and issue `chmod +x`.
#

# Works because bash automatically trims by assigning to variables and by 
# passing arguments
trim() { echo $1; }

if [[ -z "$1" ]]; then
    echo "Specify session name as the first argument"
    exit
fi

# Only because I often issue `ls` to this script by accident
if [[ "$1" == "ls" ]]; then
    tmux ls
    exit
fi

base_session="$1"
# This actually works without the trim() on all systems except OSX
tmux_nb=$(trim `tmux ls | grep "^$base_session" | wc -l`)
if [[ "$tmux_nb" == "0" ]]; then
    echo "Launching tmux base session $base_session ..."
    tmux new-session -s $base_session
else
    # Make sure we are not already in a tmux session
    if [[ -z "$TMUX" ]]; then
        echo "Launching copy of base session $base_session ..."
        # Session is is date and time to prevent conflict
        session_id=`date +%Y%m%d%H%M%S`
        # Create a new session (without attaching it) and link to base session 
        # to share windows
        tmux new-session -d -t $base_session -s $session_id
        if [[ "$2" == "1" ]]; then
		# Create a new window in that session
		tmux new-window
	fi
        # Attach to the new session & kill it once orphaned
	tmux attach-session -t $session_id \; set-option destroy-unattached
    fi
fi

```

A useful setting for this is

```
setw -g aggressive-resize on

```

added to `~/.tmux.conf`. It causes tmux to resize a window based on the smallest client actually viewing it, not on the smallest one attached to the entire session.

An alternative taken from [[1]](http://sourceforge.net/mailarchive/forum.php?thread_name=CAPBqLKEC0MAFR%2BWUYqCuyd%3DKB47HK8CFSuAf%3Dd%3DW2H3F4fpMZw%40mail.gmail.com&forum_name=tmux-users) is to put the following ~/.bashrc:

 `.bashrc` 
```
function rsc() {
  CLIENTID=$1.`date +%S`
  tmux new-session -d -t $1 -s $CLIENTID \; set-option destroy-unattached \; attach-session -t $CLIENTID
}

function mksc() {
  tmux new-session -d -s $1
  rsc $1
}

```

Citing the author:

	"mksc foo" creates a always detached permanent client named "foo". It also calls "rsc foo" to create a client to newly created session. "rsc foo" creates a new client grouped by "foo" name. It has destroy-unattached turned on so when I leave it, it kills client.

	Therefore, when my computer looses network connectivity, all "foo.something" clients are killed while "foo" remains. I can then call "rsc foo" to continue work from where I stopped.

### Changing the configuration with tmux started

By default tmux reads `~/.tmux.conf` only if it was not already running. To have tmux load a configuration file afterwards, execute:

```
tmux source-file <path>

```

This can be added to `~/.tmux.conf` as e. g.:

```
bind r source-file <path>

```

You can also do ^: and type :

```
source .tmux.conf

```

### Template script to run program in new session resp. attach to existing one

This script checks for a program presumed to have been started by a previous run of itself. Unless found it creates a new tmux session and attaches to a window named after and running the program. If however the program was found it merely attaches to the session and selects the window.

```
#!/bin/bash

PID=$(pidof $1)

if [ -z "$PID" ]; then
    tmux new-session -d -s main ;
    tmux new-window -t main -n $1 "$*" ;
fi
    tmux attach-session -d -t main ;
    tmux select-window -t $1 ;
exit 0

```

A derived version to run *irssi* with the *nicklist* plugin can be found on [its ArchWiki page](/index.php/Irssi#irssi_with_nicklist_in_tmux "Irssi").

### Terminal emulator window titles

If you SSH into a host in a tmux window, you'll notice the window title of your terminal emulator remains to be `user@localhost` rather than `user@server`. To allow the title bar to adapt to whatever host you connect to, set the following in `~/.tmux.conf`

```
set -g set-titles on
set -g set-titles-string "#T"

```

For `set-titles-string`, `#T` will display `user@host:~` and change accordingly as you connect to different hosts. You can also set many more options here.

### Automatic layouting

When creating new splits or destroying older ones the currently selected layout isn't applied. To fix that, add following binds which will apply the currently selected layout to new or remaining panes:

```
bind-key -n M-c kill-pane \; select-layout
bind-key -n M-n split-window \; select-layout

```

### vim friendly configuration

This is a configuration meant to be friendly to whoever uses vim

```
#Prefix is Ctrl-a
set -g prefix C-a
bind C-a send-prefix
unbind C-b

set -sg escape-time 1
set -g base-index 1
setw -g pane-base-index 1

#Mouse works as expected
setw -g mode-mouse on
set -g mouse-select-pane on
set -g mouse-resize-pane on
set -g mouse-select-window on

setw -g monitor-activity on
set -g visual-activity on

set -g mode-keys vi
set -g history-limit 10000

# y and p as in vim
bind Escape copy-mode
unbind p
bind p paste-buffer
bind -t vi-copy 'v' begin-selection
bind -t vi-copy 'y' copy-selection
bind -t vi-copy 'Space' halfpage-down
bind -t vi-copy 'Bspace' halfpage-up

# extra commands for interacting with the ICCCM clipboard
bind C-c run "tmux save-buffer - | xclip -i -sel clipboard"
bind C-v run "tmux set-buffer \"$(xclip -o -sel clipboard)\"; tmux paste-buffer"

# easy-to-remember split pane commands
bind | split-window -h
bind - split-window -v
unbind '"'
unbind %

# moving between panes with vim movement keys
bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R

# moving between windows with vim movement keys
bind -r C-h select-window -t :-
bind -r C-l select-window -t :+

# resize panes with vim movement keys
bind -r H resize-pane -L 5
bind -r J resize-pane -D 5
bind -r K resize-pane -U 5
bind -r L resize-pane -R 5

```

## 外部链接

*   [Practical Tmux](http://mutelight.org/articles/practical-tmux) by Brandur Leach, providing a number of configuration tips
*   [Tmux tutorial](http://www.openbsd.org/faq/faq7.html#tmux) section from the OpenBSD FAQ
*   [OpenBSD Reference Manual for tmux](http://www.openbsd.org/cgi-bin/man.cgi?query=tmux)
*   [Screen and tmux feature comparison](http://www.dayid.org/os/notes/tm.html) page by Dayid Alan
*   [Tmux tutorial Part 1](http://blog.hawkhost.com/2010/06/28/tmux-the-terminal-multiplexer/) & [Part 2](http://blog.hawkhost.com/2010/07/02/tmux-%E2%80%93-the-terminal-multiplexer-part-2) blog posts on Hawk Host
*   [tmux.conf](https://github.com/kooothor/.dotfiles/blob/master/tmux.conf) example with CPU bar and shortcut to search man pages and display them vertically
*   [powerline](https://github.com/Lokaltog/powerline) provides a powerful, dynamic statusbar configuration for tmux

**Forum threads**

*   2009-11-06 - Arch Linux - [Anyone loving Tmux in place of Screen? Info/Tips etc. URLs I've found](https://bbs.archlinux.org/viewtopic.php?id=84157&p=1)