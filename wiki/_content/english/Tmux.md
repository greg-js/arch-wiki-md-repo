[Tmux](http://tmux.github.io/) is a "terminal multiplexer: it enables a number of terminals (or windows), each running a separate program, to be created, accessed, and controlled from a single screen. tmux may be detached from a screen and continue running in the background, then later reattached."

Tmux is a BSD-licensed alternative to [GNU Screen](/index.php/GNU_Screen "GNU Screen"). Although similar, there are many differences between the programs, as noted on the [tmux FAQ page](https://raw.githubusercontent.com/tmux/tmux/master/FAQ).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Key bindings](#Key_bindings)
        *   [2.1.1 Copy Mode](#Copy_Mode)
    *   [2.2 Browsing URLs](#Browsing_URLs)
    *   [2.3 Setting the correct term](#Setting_the_correct_term)
        *   [2.3.1 256 colors](#256_colors)
        *   [2.3.2 24-bit color](#24-bit_color)
        *   [2.3.3 xterm-keys](#xterm-keys)
    *   [2.4 Other Settings](#Other_Settings)
    *   [2.5 Autostart with systemd](#Autostart_with_systemd)
*   [3 Session initialization](#Session_initialization)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Scrolling issues](#Scrolling_issues)
    *   [4.2 Mouse scrolling](#Mouse_scrolling)
    *   [4.3 Terminal emulator does not support UTF-8 mouse events](#Terminal_emulator_does_not_support_UTF-8_mouse_events)
    *   [4.4 Shift+F6 not working in Midnight Commander](#Shift.2BF6_not_working_in_Midnight_Commander)
*   [5 X clipboard integration](#X_clipboard_integration)
    *   [5.1 Urxvt middle click](#Urxvt_middle_click)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Start tmux with default session layout](#Start_tmux_with_default_session_layout)
        *   [6.1.1 Get the default layout values](#Get_the_default_layout_values)
        *   [6.1.2 Define the default tmux layout](#Define_the_default_tmux_layout)
        *   [6.1.3 Autostart tmux with default tmux layout](#Autostart_tmux_with_default_tmux_layout)
        *   [6.1.4 Alternate approach for default session](#Alternate_approach_for_default_session)
    *   [6.2 Start tmux in urxvt](#Start_tmux_in_urxvt)
    *   [6.3 Start tmux on every shell login](#Start_tmux_on_every_shell_login)
        *   [6.3.1 Bash](#Bash)
    *   [6.4 Start a non-login shell](#Start_a_non-login_shell)
    *   [6.5 Use tmux windows like tabs](#Use_tmux_windows_like_tabs)
    *   [6.6 Clients simultaneously interacting with various windows of a session](#Clients_simultaneously_interacting_with_various_windows_of_a_session)
    *   [6.7 Correct the TERM variable according to terminal type](#Correct_the_TERM_variable_according_to_terminal_type)
    *   [6.8 Reload an updated configuration without restarting tmux](#Reload_an_updated_configuration_without_restarting_tmux)
    *   [6.9 Template script to run program in new session resp. attach to existing one](#Template_script_to_run_program_in_new_session_resp._attach_to_existing_one)
    *   [6.10 Terminal emulator window titles](#Terminal_emulator_window_titles)
    *   [6.11 Automatic layouting](#Automatic_layouting)
    *   [6.12 Vim friendly configuration](#Vim_friendly_configuration)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [tmux](https://www.archlinux.org/packages/?name=tmux) package. Optionally, install [tmux-bash-completion](https://aur.archlinux.org/packages/tmux-bash-completion/) to provide bash completion functions for tmux.

## Configuration

A user-specific configuration file should be located at `~/.tmux.conf`, while a global configuration file should be located at `/etc/tmux.conf`.

### Key bindings

By default, command key bindings are prefixed by `Ctrl-b`. For example, to vertically split a window type `Ctrl-b+%`.

After splitting a window into multiple panes, a pane can be resized by the hitting prefix key (e.g. `Ctrl-b`) and, while continuing to hold Ctrl, press Left/Right/Up/Down. Swapping panes is achieved in the same manner, but by hitting *o* instead of a directional key.

**Tip:** To mimic [screen](/index.php/Screen "Screen") key bindings copy `/usr/share/tmux/screen-keys.conf` to either of the configuration locations.

Key bindings may be changed with the bind and unbind commands in `tmux.conf`. For example, the default prefix binding of `Ctrl-b` can be changed to `Ctrl-a` by adding the following commands in your configuration file:

```
unbind C-b
set -g prefix C-a
bind C-a send-prefix

```

**Tip:** Quote special characters to use them as prefix. You may also use `Alt` (called Meta) instead of `Ctrl`. For example: `set -g prefix m-'\'`

Additional ways to move between windows include the following:

```
Ctrl-b l (Move to the previously selected window)
Ctrl-b w (List all windows / window numbers)
Ctrl-b <window number> (Move to the specified window number, the default bindings are from 0 – 9)
Ctrl-b q  (Show pane numbers, when the numbers show up type the key to goto that pane)

```

Tmux has a find-window option & key binding to ease navigation of many windows:

```
Ctrl-b f <window name> (Search for window name)
Ctrl-b w (Select from interactive list of windows)

```

#### Copy Mode

A tmux window may be in one of several modes. The default permits direct access to the terminal attached to the window; the other is copy mode. Once in copy mode you can navigate the buffer including scrolling the history. Use vi or emacs-style key bindings in copy mode. The default is emacs, unless VISUAL or EDITOR contains ‘vi’

To enter copy mode do the following:

```
Ctrl-b [

```

You can navigate the buffer as you would in your default editor.

To quit copy mode, use one of the following keybindings:

vi mode:

```
q

```

emacs mode:

```
Esc

```

### Browsing URLs

To browse URLs inside tmux you must have [urlview](https://aur.archlinux.org/packages/urlview/) installed and configured.

Inside a new terminal:

```
bind-key u capture-pane \; save-buffer /tmp/tmux-buffer \; run-shell "$TERMINAL -e urlview /tmp/tmux-buffer"

```

Or inside a new tmux window (no new terminal needed):

```
bind-key u capture-pane \; save-buffer /tmp/tmux-buffer \; new-window -n "urlview" '$SHELL -c "urlview < /tmp/tmux-buffer"'

```

### Setting the correct term

#### 256 colors

If you are using a 256 colour terminal, you will need to set the correct term in tmux. As of [tmux 2.1](https://raw.githubusercontent.com/tmux/tmux/master/CHANGES), this is now *tmux*, or *tmux-256color*. You can do this in `tmux.conf`:

```
set -g default-terminal "tmux-256color" 

```

Other, older alternatives, include *screen*, or *screen-256color*:

```
set -g default-terminal "screen-256color"

```

Also, if tmux messes up, you can force tmux to assume that the terminal support 256 colors, by adding this in your .bashrc:

```
alias tmux="tmux -2"

```

#### 24-bit color

Tmux supports 24-bit color as of version 2.2 ([[1]](https://github.com/tmux/tmux/commit/427b8204268af5548d09b830e101c59daa095df9)). If your terminal supports 24-bit color (see this [gist](https://gist.github.com/XVilka/8346728)), add your terminal to the `terminal-overrides` setting. For example, if you use [Termite](/index.php/Termite "Termite"), you would add:

```
set -ga terminal-overrides ",xterm-termite:Tc"

```

For other terminals, replace `xterm-termite` with the relevant terminal type (stored in `$TERM`). See the tmux(1) man page for details about the `Tc` terminfo extension.

#### xterm-keys

To enable xterm-keys in your `tmux.conf`, you have to add the following line

```
set-option -g xterm-keys on

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

To limit the scrollback buffer to 10000 lines:

```
set -g history-limit 10000

```

Terminal emulator settings can be overridden with

```
set -ga terminal-overrides ',xterm*:smcup@:rmcup@'
set -ga terminal-override ',rxvt-uni*:XT:Ms=\E]52;%p1%s;%p2%s\007'

```

Mouse can be toggled with

```
bind-key m set-option -g mouse on \; display 'Mouse: ON'
bind-key M set-option -g mouse off \; display 'Mouse: OFF'

```

### Autostart with systemd

There are some notable advantages to starting a tmux server at startup. Notably, when you start a new tmux session, having the service already running reduces any delays in the startup.

Furthermore, any customization attached to your tmux session will be retained and your tmux session can be made to persist even if you have never logged in, if you have some reason to do that (like a heavily scripted tmux configuration or shared user tmux sessions).

The service below starts *tmux* for the specified user (i.e. start with `tmux@*username*.service`):

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

Alternatively, you can place this file within your [systemd/User](/index.php/Systemd/User "Systemd/User") directory (without `User=%I`), for example `~/.config/systemd/user/tmux.service`. This way the tmux service will start when you log in, unless you also enable [systemd/User#Automatic start-up of systemd user instances](/index.php/Systemd/User#Automatic_start-up_of_systemd_user_instances "Systemd/User").

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

If you have issues scrolling with Shift-Page Up/Down in your terminal, the following will remove the smcup and rmcup capabilities for any term that reports itself as anything beginning with `xterm`:

```
set -ga terminal-overrides ',xterm*:smcup@:rmcup@'

```

This tricks the terminal emulator into thinking Tmux is a full screen application like pico or mutt[[2]](http://superuser.com/questions/310251/use-terminal-scrollbar-with-tmux), which will make the scrollback be recorded properly. Beware however, it will get a bit messed up when switching between windows/panes. Consider using Tmux's native scrollback instead.

### Mouse scrolling

**Note:** This interferes with selection buffer copying and pasting. To copy/paste to/from the selection buffer hold the shift key.

If you want to scroll with your mouse wheel, ensure mode-mouse is on in .tmux.conf

```
set -g mouse on

```

You can set scroll History with:

```
set -g history-limit 30000

```

For mouse wheel scrolling as from tmux 2.1 try adding one or both of these to ~/.tmux.conf

```
   bind -T root WheelUpPane   if-shell -F -t = "#{alternate_on}" "send-keys -M" "select-pane -t =; copy-mode -e; send-keys -M"
   bind -T root WheelDownPane if-shell -F -t = "#{alternate_on}" "send-keys -M" "select-pane -t =; send-keys -M"

```

Though the above will only scroll one line at a time, add this solution to scroll an entire page instead

```
   bind -t vi-copy    WheelUpPane   page-up
   bind -t vi-copy    WheelDownPane page-down
   bind -t emacs-copy WheelUpPane   page-up
   bind -t emacs-copy WheelDownPane page-down

```

### Terminal emulator does not support UTF-8 mouse events

When the terminal emulator does not support the UTF-8 mouse events and the `mouse on` tmux option is set, left-clicking inside the terminal window might paste strings like `[M#` or `[Ma` into the promt.

To solve this issue set:

```
set -g mouse-utf8 off

```

### Shift+F6 not working in Midnight Commander

See [Midnight Commander#Broken shortcuts](/index.php/Midnight_Commander#Broken_shortcuts "Midnight Commander").

## X clipboard integration

**Tip:** The tmux plugin [tmux-yank](https://github.com/tmux-plugins/tmux-yank) provides similar functionality.

It is possible to copy tmux selection to X clipboard (and to X primary/secondary selection) and in reverse direction. The following tmux config file snippet effectively integrates X clipboard/selection with the current tmux selection using the program [xsel](https://www.archlinux.org/packages/?name=xsel):

```
# Emacs style
bind-key -T copy-mode y send-keys -X copy-pipe "xsel -i -p && xsel -o -p | xsel -i -b"
bind-key C-y run "xsel -o | tmux load-buffer - ; tmux paste-buffer"

```

```
# Vim style
bind-key -T copy-mode-vi y send-keys -X copy-pipe "xsel -i -p && xsel -o -p | xsel -i -b"
bind-key p run "xsel -o | tmux load-buffer - ; tmux paste-buffer"

```

[xclip](https://www.archlinux.org/packages/?name=xclip) could also be used for that purpose, unlike xsel it works better on printing raw bitstream that doesn't fit the current locale. Nevertheless, it is neater to use `xsel` instead of `xclip`, because xclip does not close STDOUT after it has read from tmux's buffer. As such, tmux doesn't know that the copy task has completed, and continues to wait for xclip's termination, thereby rendering tmux unresponsive. A workaround is to redirect `STDOUT` of `xclip` to `/dev/null`, like in the following:

```
# Vim style
bind-key -T copy-mode-vi y send-keys -X copy-pipe "xclip -i -sel clip > /dev/null"
bind-key p run "xclip -o -sel clip | tmux load-buffer - ; tmux paste-buffer"

```

### Urxvt middle click

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

Next, you want to tell tmux about the new function and enable mouse support (if you haven't already):

 `~/.tmux.conf` 
```
...
set-option -ga terminal-override ',rxvt-uni*:XT:Ms=\E]52;%p1%s;%p2%s\007'
set -g mouse on
...

```

That's it. Be sure to end all instances of tmux before trying the new MiddleClick functionality.

While in tmux, Shift+MiddleMouseClick will paste the clipboard selection while just MiddleMouseClick will paste your tmux buffer. Outside of tmux, just use MiddleMouseClick to paste your tmux buffer and your standard Ctrl-c to copy.

## Tips and tricks

### Start tmux with default session layout

To setup your default Tmux session layout, you install [tmuxinator](https://aur.archlinux.org/packages/tmuxinator/) from [AUR](/index.php/AUR "AUR"). Test your installation with

```
tmuxinator doctor

```

#### Get the default layout values

Start Tmux as usual and configure your windows and panes layout as you like. When finished, get the current layout values by executing (while you are still within the current Tmux session)

```
tmux list-windows

```

The output may look like this (two windows with 3 panes and 2 panes layout)

```
0: default* (3 panes) [274x83] [layout 20a0,274x83,0,0{137x83,0,0,3,136x83,138,0[136x41,138,0,5,136x41,138,42,6]}] @2 (active)
1: remote- (2 panes) [274x83] [layout e3d3,274x83,0,0[274x41,0,0,4,274x41,0,42,7]] @3                                         

```

The Interesting part you need to copy for later use begins after **[layout...** and excludes **... ] @2 (active)**. For the first window layout you need to copy e.g. **20a0,274x83,0,0{137x83,0,0,3,136x83,138,0[136x41,138,0,5,136x41,138,42,6]}**

#### Define the default tmux layout

Knowing this, you can exit the current tmux session. Following this, you create your default Tmux session layout by editing Tmuxinator's config file (Don't copy the example, get your layout values as described above)

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

The example defines two windows named "default" and "remote". With your determined layout values. For each pane you have to use at least one `-` line. Within the first window panes you start the commandline "clear" in pane one, "vim" in pane two and "clear && emacs -nw" executes two commands in pane three on each Tmux start. The second window layout has two panes without defining any start commmands.

Test the new default layout with (yes, it is "mux"):

```
mux default

```

#### Autostart tmux with default tmux layout

If you like to start your terminal session with your default Tmux session layout edit

 `~/.bashrc` 
```
 if [ -z "$TMUX" ]; then
   mux default          
 fi                     

```

#### Alternate approach for default session

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

### Start tmux on every shell login

#### Bash

For bash, simply add the following line of bash code to your .bashrc before your aliases; the code for other shells is very similar:

 `~/.bashrc` 
```
# If not running interactively, do not do anything
[[ $- != *i* ]] && return
[[ -z "$TMUX" ]] && exec tmux

```

**Note:** This snippet ensures that tmux is not launched inside of itself (something tmux usually already checks for anyway). tmux sets $TMUX to the socket it is using whenever it runs, so if $TMUX isn't set or is length 0, we know we aren't already running tmux.

Add the following snippet to start only one session (unless you start some manually), on login, try attach at first, only create a session if no tmux is running.

```
# TMUX
if which tmux >/dev/null 2>&1; then
    #if not inside a tmux session, and if no session is started, start a new session
    test -z "$TMUX" && (tmux attach || tmux new-session)
fi

```

The following snippet does the same thing, but also checks tmux is installed before trying to launch it. It also tries to reattach you to an existing tmux session at logout, so that you can shut down every tmux session quickly from the same terminal at logout.

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

### Start a non-login shell

Tmux starts a [login shell](http://unix.stackexchange.com/questions/38175) [by default](http://comments.gmane.org/gmane.comp.terminal-emulators.tmux.user/5997), which may result in multiple negative side effects:

*   Users of [fortune](https://en.wikipedia.org/wiki/fortune_(Unix) may notice that quotes are printed when creating a new panel.
*   The configuration files for login shells such as `~/.profile` are interpreted each time a new panel is created, so commands intended to be run on session initialization (e.g. setting audio level) are executed.

To disable this behaviour, add to `~/.tmux.conf`:

```
set -g default-command "${SHELL}"

```

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

An alternative taken from [[3]](http://comments.gmane.org/gmane.comp.terminal-emulators.tmux.user/2632) is to put the following ~/.bashrc:

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

### Correct the TERM variable according to terminal type

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

### Reload an updated configuration without restarting tmux

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

For `set-titles-string`, `#T` will display `user@host:~` and change accordingly as you connect to different hosts.

### Automatic layouting

When creating new splits or destroying older ones the currently selected layout isn't applied. To fix that, add following binds which will apply the currently selected layout to new or remaining panes:

```
bind-key -n M-c kill-pane \; select-layout
bind-key -n M-n split-window \; select-layout

```

### Vim friendly configuration

See [[4]](https://gist.github.com/anonymous/6bebae3eb9f7b972e6f0) for a configuration friendly to [vim](/index.php/Vim "Vim") users.

## See also

*   [BBS topic](https://bbs.archlinux.org/viewtopic.php?id=84157&p=1)
*   [Screen and tmux feature comparison](http://www.dayid.org/os/notes/tm.html)
*   [powerline](https://github.com/Lokaltog/powerline), a dynamic statusbar for tmux
*   [Plugins for tmux](https://github.com/tmux-plugins)

**Tutorials**

*   [Practical Tmux](http://mutelight.org/articles/practical-tmux)
*   [Tmux FAQ (OpenBSD)](http://www.openbsd.org/faq/faq7.html#tmux)
*   [man page (OpenBSD)](http://www.openbsd.org/cgi-bin/man.cgi?query=tmux)
*   [Tmux tutorial Part 1](http://blog.hawkhost.com/2010/06/28/tmux-the-terminal-multiplexer/) and [Part 2](http://blog.hawkhost.com/2010/07/02/tmux-%E2%80%93-the-terminal-multiplexer-part-2)