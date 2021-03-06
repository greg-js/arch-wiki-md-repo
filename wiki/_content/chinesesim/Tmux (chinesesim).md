相关文章

*   [dtach](/index.php/Dtach "Dtach")
*   [GNU Screen](/index.php/GNU_Screen "GNU Screen")

**翻译状态：** 本文是英文页面 [Tmux](/index.php/Tmux "Tmux") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-10-24，点击[这里](https://wiki.archlinux.org/index.php?title=Tmux&diff=0&oldid=492457)可以查看翻译后英文页面的改动。

[tmux](http://tmux.github.io/) 是一个终端复用器: 可以激活多个终端或窗口, 在每个终端都可以单独访问，每一个终端都可以访问，运行和控制各自的程序.tmux类似于screen，可以关闭窗口将程序放在后台运行，需要的时候再重新连接。

Tmux 与基于 ISC 协议发布的 [GNU Screen](/index.php/Screen_Tips "Screen Tips") 类似，这个[tmux FAQ 页面](https://raw.githubusercontent.com/tmux/tmux/master/FAQ)包含两者的区别。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 快捷键前缀](#快捷键前缀)
        *   [2.1.1 复制模式](#复制模式)
    *   [2.2 打开URL](#打开URL)
    *   [2.3 正确设置 term](#正确设置_term)
    *   [2.4 其他设置](#其他设置)
    *   [2.5 用systemd后台自启tmux](#用systemd后台自启tmux)
*   [3 会话初始化](#会话初始化)
*   [4 提示和小技巧](#提示和小技巧)
    *   [4.1 启动时使用默认布局](#启动时使用默认布局)
        *   [4.1.1 获取默认布局参数](#获取默认布局参数)
        *   [4.1.2 定义默认布局](#定义默认布局)
        *   [4.1.3 自动使用默认布局启动tmux](#自动使用默认布局启动tmux)
        *   [4.1.4 默认会话的替代实现方式](#默认会话的替代实现方式)
    *   [4.2 Start tmux in urxvt](#Start_tmux_in_urxvt)
    *   [4.3 启动shell时自动启动tmux](#启动shell时自动启动tmux)
        *   [4.3.1 Bash](#Bash)
    *   [4.4 启动non-login shell](#启动non-login_shell)
    *   [4.5 像标签一样使用窗口](#像标签一样使用窗口)
    *   [4.6 Clients simultaneously interacting with various windows of a session](#Clients_simultaneously_interacting_with_various_windows_of_a_session)
    *   [4.7 根据终端类型自动更正TERM环境变量](#根据终端类型自动更正TERM环境变量)
    *   [4.8 不用重启tmux就能加载新的配置](#不用重启tmux就能加载新的配置)
    *   [4.9 样例代码:attach已启动的会话而不是新开一个](#样例代码:attach已启动的会话而不是新开一个)
    *   [4.10 标题栏自动更改](#标题栏自动更改)
    *   [4.11 自动布局](#自动布局)
    *   [4.12 使用类似Vim的快捷键设置](#使用类似Vim的快捷键设置)
*   [5 常见问题与解答](#常见问题与解答)
    *   [5.1 滚动问题](#滚动问题)
    *   [5.2 Shift+F6 not working in Midnight Commander](#Shift+F6_not_working_in_Midnight_Commander)
*   [6 ICCCM Selection Integration](#ICCCM_Selection_Integration)
    *   [6.1 Urxvt MiddleClick Solution](#Urxvt_MiddleClick_Solution)
*   [7 外部链接](#外部链接)

## 安装

从[官方源](/index.php/Official_repositories "Official repositories")[安装](/index.php/Pacman "Pacman")软件包[tmux](https://www.archlinux.org/packages/?name=tmux)。可选安装[tmux-bash-completion](https://aur.archlinux.org/packages/tmux-bash-completion/)为tmux提供了bash补全功能。

## 配置

用户私人配置文件在`~/.tmux.conf`, 全局配置文件在 `/etc/tmux.conf`。

### 快捷键前缀

<caption>*前缀为* `Ctrl-b`</caption>
| 按键 | 动作 |
| c | 创建一个新窗口 |
| n | 切换至下一窗口 |
| p | 切换到上一个窗口 |
| " | 水平分割窗口 |
| % | 垂直分割窗口 |
| , | 重新命名当前窗口 |
| o | 移动至下一个面板 |

默认绑定的前缀按键为Ctrl-b. 比如说垂直分割窗口的快捷键就是 `Ctrl-b %`。

使用多个面板分割窗口后, 先按前缀快捷键(比如说：`Ctrl-b`)然后按住Ctrl键就可以使用方向键调整面板大小。 如果要交换面板也是采用同样的方式，只是按键由方向键换成“O“键。

快捷键前缀可以用`tmux.conf`中的bind和unbind命令修改。比如你可以在配置文件中增加下面命令,把前缀`Ctrl-b`改成`Ctrl-a`：

```
unbind C-b
set -g prefix C-a
bind C-a send-prefix

```

**提示：** 使用特殊字符作为前缀，你必须使用`Alt`键(Meta键)代替`Ctrl`键。例如：`set -g prefix m-'\'`

。

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

#### 复制模式

一个tmux窗口可能处于几个模式中的一个。默认模式允许直接访问连接到窗口的终端；另一种是复制模式。一旦在复制模式下，你可以在缓冲区包括滚动历史。vi或emacs风格的按键方式绑定在复制模式中，默认是emacs,除非编辑器包含"vi"。

使用下列快捷键可以进入滚动模式:

```
Ctrl-b [

```

可以在默认编辑器的缓冲区中进行浏览。 离开复制模式，使用下面的按键： vi模式

```
 q

```

emacs模式

```
 Esc

```

### 打开URL

你需要安装 [urlview](https://aur.archlinux.org/packages/urlview/)来打开URL 另外需要配置如下：

打开一个新的终端:

```
bind-key u capture-pane \; save-buffer /tmp/tmux-buffer \; run-shell "$TERMINAL -e urlview /tmp/tmux-buffer"

```

或者直接在tmux的一个新窗口 (不需要新终端):

```
bind-key u capture-pane \; save-buffer /tmp/tmux-buffer \; new-window -n "urlview" '$SHELL -c "urlview < /tmp/tmux-buffer"'

```

### 正确设置 term

如果使用的是 256 色的终端，必须在 tmux 的配置文件 `tmux.conf` 中将终端设置为 `tmux` 或 `tmux-256color`:

```
 set -g default-terminal "tmux-256color"  

```

或在 `.bashrc` 中添加:

```
# for tmux: export 256color
[ -n "$TMUX" ] && export TERM=screen-256color

```

如果你在 `tmux.conf` 启用xterm-keys, 那你需要构建一个新的终端信息来声明新的退出命令，否则程序无法获取退出方式。用 `tic` 编译下列信息，你可以使用 "xterm-screen-256color" 来作为你的TERM:

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

### 其他设置

设置最多回滚的行数

```
set -g history-limit 10000

```

### 用systemd后台自启tmux

开机自启tmux有诸多好处，当tmux服务在后台运行时,启动一个tmux会话能减少许多延时。

此外，即使你没有登录，对tmux会话的任何定制都将保留，tmux会话也将会被持久化。这对于那些有重度tmux配置（启动慢）或者共享tmux会话的人来说特别有用。

下面这个systemd service配置可作为参考 (启动 `tmux@*username*.service`):

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

**提示：** 可以通过 `WorkingDirectory=*custom_path*` 设置工作路径.

把这个文件放在 [systemd/User](/index.php/Systemd/User "Systemd/User") 目录下,如 `~/.config/systemd/user/tmux.service`. 这样tmux service 就会在你登录时自动启动.

## 会话初始化

可以通过修改配置文件`~/.tmux.conf`来使得tmux在初始化一个session的时候自动新建窗口, 比如:

```
new  -n WindowName Command
neww -n WindowName Command
neww -n WindowName Command

```

如果想在tmux启动session的时候自动分割窗口, 只需要把相应分割命令加在你想分割的窗口的neww命令之下, 如下:

```
new  -s SessionName -n WindowName Command
neww -n foo/bar foo
# 在这之下添加分割窗口命令
splitw -v -p 50 -t 0 bar
selectw -t 1 
selectp -t 0

```

这将启动两个窗口, 第二个窗口会被命名为foo/bar并且会被垂直对半分割, 其中窗格foo会在窗格bar的上面,光标会在第二个窗口(foo/bar)上面的窗格(foo)

{{注意|除非你在你得配置文件`.conf`中特别指定, 否则会话(session), window(窗口),panes(窗格)的序号都是从0开始算起.}

想要管理多个会话, 需要在你的配置文件中用source命令分别执行相应会话的配置文件

```
# initialize sessions
bind F source-file ~/.tmux/foo
bind B source-file ~/.tmux/bar

```

## 提示和小技巧

### 启动时使用默认布局

Session managers like tmuxinator and [tmuxp](/index.php/Tmuxp "Tmuxp") make it easy to manage common session configurations.

For tmuxinator, install [tmuxinator](https://aur.archlinux.org/packages/tmuxinator/) from [AUR](/index.php/AUR "AUR"). Test your installation with

```
tmuxinator doctor

```

#### 获取默认布局参数

Start tmux as usual and configure your windows and panes layout as you like. When finished, get the current layout values by executing (while you are still within the current tmux session)

```
tmux list-windows

```

The output may look like this (two windows with 3 panes and 2 panes layout)

```
0: default* (3 panes) [274x83] [layout 20a0,274x83,0,0{137x83,0,0,3,136x83,138,0[136x41,138,0,5,136x41,138,42,6]}] @2 (active)
1: remote- (2 panes) [274x83] [layout e3d3,274x83,0,0[274x41,0,0,4,274x41,0,42,7]] @3                                         

```

The Interesting part you need to copy for later use begins after **[layout...** and excludes **... ] @2 (active)**. For the first window layout you need to copy e.g. **20a0,274x83,0,0{137x83,0,0,3,136x83,138,0[136x41,138,0,5,136x41,138,42,6]}**

#### 定义默认布局

Knowing this, you can exit the current tmux session. Following this, you create your default tmux session layout by editing tmuxinator's config file (Don't copy the example, get your layout values as described above)

 `~/.tmuxinator/default.yml` 
```
name: default
root: ~/
windows:
  - default:
      layout: 20a0,274x83,0,0{137x83,0,0,3,136x83,138,0[136x41,138,0,5,136x41,138,42,6]}
      panes:
        - clear
        - vim
        - clear && emacs -nw
  - remote:
      layout: 24ab,274x83,0,0{137x83,0,0,3,136x83,138,0,4}
      panes:
        - 
        - 

```

The example defines two windows named "default" and "remote". With your determined layout values. For each pane you have to use at least one `-` line. Within the first window panes you start the commandline "clear" in pane one, "vim" in pane two and "clear && emacs -nw" executes two commands in pane three on each tmux start. The second window layout has two panes without defining any start commmands.

Test the new default layout with (yes, it is "mux"):

```
mux default

```

#### 自动使用默认布局启动tmux

如果想在启动终端的时候直接进入tmux, 并且使用默认布局, 可以设置

 `~/.bashrc` 
```
 if [ -z "$TMUX" ]; then
   mux default          
 fi                     

```

#### 默认会话的替代实现方式

Instead of using the above method, one can just write a bash script that when run, will create the default session and attach to it. Then you can execute it from a terminal to get the pre-designed configuration in that terminal

```
#!/bin/bash
tmux new-session -d -n WindowName Command
tmux new-window -n NewWindowName
tmux split-window -v
tmux selectp -t 1
tmux split-window -h
tmux selectw -t 1
tmux -2 attach-session -d

```

### Start tmux in urxvt

Use this command to start urxvt with a started tmux session. I use this with the exec command from my .ratpoisonrc file.

 `urxvt -e bash -c "tmux -q has-session && exec tmux attach-session -d || exec tmux new-session -n$USER -s$USER@$HOSTNAME"` 

### 启动shell时自动启动tmux

#### Bash

对bash用户, 只需要将下面命令添加到自己家目录下的.bashrc, 要注意这句命令需要在alias配置之前.对其它shell的配置也是类似的

 `~/.bashrc` 
```
# If not running interactively, do not do anything
[[ $- != *i* ]] && return
[[ -z "$TMUX" ]] && exec tmux

```

**注意:** 这些代码确保tmux不会在tmux中启动(tmux嵌套于tmux中). tmux 通过设置环境变量$TMUX 来设置tmux启动所用的socket, 如果$TMUX不存在,或者长度为0那么就可以知道当前没有运行tmux.

下面的配置会尝试只启动一个会话, 当你登录时, 如果之前启动过会话, 那么它会直接attach, 而不是新开一个. 想要新开一个session要么是因为之前没有会话, 要么是你手动启动一个新的会话.

```
# TMUX
if which tmux >/dev/null 2>&1; then
    #if not inside a tmux session, and if no session is started, start a new session
    test -z "$TMUX" && (tmux attach || tmux new-session)
fi

```

下面的配置实现的功能相似, 但是他会在启动tmux之前先检查一下tmux是否已经安装. 它也会在你登出之前帮你重新连接上未关闭的session, 这样可以让你手动关闭会话并保存相应的工作,避免数据丢失,进程异常中断.

```
# TMUX
if which tmux >/dev/null 2>&1; then
    # if no session is started, start a new session
    test -z ${TMUX} && tmux

    # when quitting tmux, try to attach
    while test -z ${TMUX}; do
        tmux attach || break
    done
fi

```

另外一种配置, 一样可以实现自动连接已存在的会话,否则会新开一个:

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

### 启动non-login shell

Tmux starts a [login shell](http://unix.stackexchange.com/questions/38175) [by default](http://comments.gmane.org/gmane.comp.terminal-emulators.tmux.user/5997), which may result in multiple negative side effects:

*   Users of [fortune](https://en.wikipedia.org/wiki/fortune_(Unix) may notice that quotes are printed when creating a new panel.
*   The configuration files for login shells such as `~/.profile` are interpreted each time a new panel is created, so commands intended to be run on session initialization (e.g. setting audio level) are executed.

To disable this behaviour, add to `~/.tmux.conf`:

```
set -g default-command "${SHELL}"

```

### 像标签一样使用窗口

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
        # Session id is date and time to prevent conflict
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

An alternative taken from [[1]](http://comments.gmane.org/gmane.comp.terminal-emulators.tmux.user/2632) is to put the following ~/.bashrc:

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

### 根据终端类型自动更正TERM环境变量

Instead of [setting a fixed TERM variable in tmux](#Setting_the_correct_term), it is possible to set the proper TERM (either `screen` or `screen-256color`) according to the type of your terminal emulator:

 `~/.tmux.conf` 
```
## set the default TERM
set -g default-terminal screen

## update the TERM variable of terminal emulator when creating a new session or attaching a existing session
set -g update-environment 'DISPLAY SSH_ASKPASS SSH_AGENT_PID SSH_CONNECTION WINDOWID XAUTHORITY TERM'
## determine if we should enable 256-colour support
if "[[ ${TERM} =~ 256color || ${TERM} == fbterm ]]" 'set -g default-terminal screen-256color'

```
 `~/.zshrc` 
```
## workaround for handling TERM variable in multiple tmux sessions properly from [http://sourceforge.net/p/tmux/mailman/message/32751663/](http://sourceforge.net/p/tmux/mailman/message/32751663/) by Nicholas Marriott
if [[ -n ${TMUX} && -n ${commands[tmux]} ]];then
        case $(tmux showenv TERM 2>/dev/null) in
                *256color) ;&
                TERM=fbterm)
                        TERM=screen-256color ;;
                *)
                        TERM=screen
        esac
fi
```

### 不用重启tmux就能加载新的配置

如果对tmux的配置文件`~/.tmux.conf`做了修改, 默认情况下tmux是不会自动重新加载的, 除非关闭所有正在运行的tmux会话. 如果不想关闭会话而手动加载tmux的配置文件, 可以在命令行下输入:

```
tmux source-file <path>

```

也可以在配置文件 `~/.tmux.conf` 中加入下面配置(这样下次输入 ctrl+b r就可以加载新的配置文件了):

```
bind r source-file <path>

```

还有一种做法是输入前缀+冒号(ctrl+b :),然后输入如下命令:

```
source .tmux.conf

```

### 样例代码:attach已启动的会话而不是新开一个

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

### 标题栏自动更改

If you SSH into a host in a tmux window, you'll notice the window title of your terminal emulator remains to be `user@localhost` rather than `user@server`. To allow the title bar to adapt to whatever host you connect to, set the following in `~/.tmux.conf`

```
set -g set-titles on
set -g set-titles-string "#T"

```

For `set-titles-string`, `#T` will display `user@host:~` and change accordingly as you connect to different hosts.

### 自动布局

When creating new splits or destroying older ones the currently selected layout isn't applied. To fix that, add following binds which will apply the currently selected layout to new or remaining panes:

```
bind-key -n M-c kill-pane \; select-layout
bind-key -n M-n split-window \; select-layout

```

### 使用类似Vim的快捷键设置

See [[2]](https://gist.github.com/anonymous/6bebae3eb9f7b972e6f0) for a configuration friendly to [vim](/index.php/Vim "Vim") users.

With tmux 2.4 change:

```
bind -t vi-copy 'v' begin-selection
bind -t vi-copy 'y' copy-selection
bind -t vi-copy 'Space' halfpage-down
bind -t vi-copy 'Bspace' halfpage-up

```

to:

```
bind-key -T copy-mode-vi 'v' send -X begin-selection
bind-key -T copy-mode-vi 'y' send -X copy-selection
bind-key -T copy-mode-vi 'Space' send -X halfpage-down
bind-key -T copy-mode-vi 'Bspace' send -X halfpage-up

```

## 常见问题与解答

### 滚动问题

如果你在终端中使用Shift-PageUp/Shift-PageDown 翻页有问题,把下面加到配置文件中试试:

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