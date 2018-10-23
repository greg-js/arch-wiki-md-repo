[Ratpoison](http://www.nongnu.org/ratpoison/) is a tiling [window manager](/index.php/Window_manager "Window manager") written in C that allows the user to manage applications without a mouse. The user interface is inspired by [GNU Screen](/index.php/GNU_Screen "GNU Screen").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Using ratpoison](#Using_ratpoison)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Java Swing Applications](#Java_Swing_Applications)
    *   [4.2 Multiple workspaces](#Multiple_workspaces)
    *   [4.3 Urxvt and xterm](#Urxvt_and_xterm)
        *   [4.3.1 Install a Patched URxvt](#Install_a_Patched_URxvt)
        *   [4.3.2 Adjust the Border](#Adjust_the_Border)
    *   [4.4 Launch on startup](#Launch_on_startup)
    *   [4.5 Wallpaper and transparency](#Wallpaper_and_transparency)
*   [5 Useful keybindings](#Useful_keybindings)
*   [6 Focus follows mouse](#Focus_follows_mouse)
*   [7 Ratpoison and display managers](#Ratpoison_and_display_managers)
*   [8 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [ratpoison](https://www.archlinux.org/packages/?name=ratpoison) package.

## Configuration

To use ratpoison as your window manager, you have to create/edit the file `~/.xinitrc`.

Example .xinitrc:

```
# The black/white grid as background doesn't suit my taste.
xsetroot -solid black &
# Ratpoison is compatible with xcompmgr! now you can have real transparency
xcompmgr -c -f -D 5 &
#fire up ratpoison!
exec /usr/bin/ratpoison

```

## Using ratpoison

After X11 starts up you will see a black screen and a little textbox on the upper right of it that says "Welcome to Ratpoison". Now type `Ctrl+t` and then `?` to get a list of keybindings. If you are used to GNU screen, you will feel at home very soon.

You are able to define custom keystrokes and even override existing ones in `~/.ratpoisonrc`

Example:

```
# Overriding CTRL+t 'c' to start aterm instead of xterm
bind c exec aterm

bind f exec firefox

```

So, if you type `Ctrl+t` and then `f`, ratpoison will fire up Firefox.

`Ctrl+t` is the default escape key, the key used to trigger ratpoison commands. To change the mapping of the escape key to the Windows key, use the following line in your `~/.ratpoisonrc`:

```
# Setting the escape key to the Windows key
escape Super_L

```

Here is another .ratpoisonrc i'm using on my computers:

```
exec xsetroot -cursor_name left_ptr
startup_message off

escape C-z

# Make a screenshot
alias sshot exec import -window root ~/screenshot-$(date +%F).jpg
definekey top M-C-Print sshot

#virtual desks
gnewbg one
gnewbg two

definekey top M-l exec ratpoison -c "select -" -c "gprev" -c "next"
definekey top M-h exec ratpoison -c "select -" -c "gnext" -c "next"

#switch between windows
definekey top M-j next
definekey top M-k prev

#apps
unbind c
bind c exec urxvt -tr
#bind c exec aterm

bind g exec gftp
bind f exec firefox

```

## Tips and tricks

### Java Swing Applications

Java Swing GUI applications assume tiling window managers, and don't go to fullscreen properly with the default ratpoison configuration. However, there is a way to "trick" the Java swing window into thinking it's in a tiling window manager and getting it to go to fullscreen correctly.

First, install the <tt>wmname</tt> package. Then add this line to your <tt>.ratpoisonrc</tt>:

 `~/.ratpoisonrc` 
```
exec wmname LG3D

```

Voila! Java Swing applications should properly fullscreen now.

### Multiple workspaces

By default, ratpoison only has one workspace, but using a script called rpws (installed by default) you can have more.

Just edit your .ratpoisonrc, and add:

 `~/.ratpoisonrc` 
```
exec /usr/bin/rpws init 6 -k

```

That creates 6 workspaces. By default, you can access to them by using `Alt+F1` to access the first, `Alt+F2` to access the second, etc.

You can also add binds to them, like this:

```
bind C-1 exec rpws 1
bind C-2 exec rpws 2
...

```

That allows to access them with `Ctrl+t` `Ctrl+1` (assuming `Ctrl+t` as your escape key)

### Urxvt and xterm

Urxvt and xterm, as they are installed by default, send resize hints to the window manager. This works in most tiling window managers, but not in ratpoison. The end result is that URxvt/xterm resizes itself in multiples of the font size, rather than resizing to the whole screen, and chances that there are unfilled gaps are high. There are two solutions to this problem, documented below.

#### Install a Patched URxvt

If you use URxvt, the [rxvt-unicode-fontspacing-noinc-vteclear-secondarywheel](https://aur.archlinux.org/packages/rxvt-unicode-fontspacing-noinc-vteclear-secondarywheel/) package, among other improvements, sends no resize hints to the window manager. If you install this version of URxvt rather than the default, URxvt will resize properly within ratpoison.

#### Adjust the Border

We can use the xterm/urxvt option internalBorder and set the border of ratpoison to 0.

A trial and error process must be done to find the exact number of internalBorder for each combination of resolution and font size. (the border of ratpoison must be set to 0 before doing the tests) The term command line option -b can be used to test for the correct number and then can be saved on the following files.

 `~/.Xresources` 
```
urxvt*internalBorder: 8 #change urxvt to xterm if necessary. Using the font terminus in urxvt at 14px size, 8 is the correct number here.

```
 `~/.ratpoisonrc` 
```
set border 0

```

If a combination cannot be found, you could try changing the font size and the font family also. (that changes the required border number)

### Launch on startup

Examples for launching programs when ratpoison starts. File `~/.ratpoisonrc` is executed by ratpoison on startup.

 `Launch urxvt with a tmux session` 
```
exec urxvt -e bash -c "tmux -q has-session && exec tmux attach-session -d || exec tmux new-session -n$USER -s$USER@$HOSTNAME"

```
 `Launch optimized chromium` 
```
exec bash -c 'pidof chromium &>/dev/null || exec /usr/bin/chromium --disk-cache-dir=~/tmp/cache'

```

### Wallpaper and transparency

Example for setting transparency using [xcompmgr](/index.php/Xcompmgr "Xcompmgr") and nitrogen. First start nitrogen and set the desired wallpaper. Then use this in your `~/.ratpoisonrc`

 `Wallpaper and transparency` 
```
exec xcompmgr -c -f -D 5 &
exec nitrogen --restore

```

## Useful keybindings

| `Ctrl+t` `!` <*Program Name*> Start any program |
| `Ctrl+t` `?` Show key bindings |
| `Ctrl+t` `c` Start an X terminal |
| `Ctrl+t` `n` Switch to next window |
| `Ctrl+t` `p` Switch to previous window |
| `Ctrl+t` `1`-`9` Switch to windows 1-9 |
| `Ctrl+t` `k` Close the current window |
| `Ctrl+t` `Shift+k` XKill the current application |
| `Ctrl+t` `s`,`Shift+s` Split the current frame into two vertical,horizontal ones |
| `Ctrl+t` `Tab`, `←`, `↑`, `→`, `↓` Switch to the next, left. top, right, bottom frame. |
| `Ctrl+t` `Shift+q` Make the current frame the only one |
| `Ctrl+t` `:` Execute a ratpoison command |

## Focus follows mouse

`sloppy.c` is a build script for [ratpoison](https://www.archlinux.org/packages/?name=ratpoison) and can be found in `/usr/share/ratpoison/`. To enable focus follows mouse for `ratpoison`, run the following:

```
# cd /usr/share/ratpoison/
# gcc -o sloppy sloppy.c -lX11
# ./sloppy

```

To autostart focus follows mouse, add the following to `~/.ratpoisonrc`:

```
exec /usr/share/ratpoison/sloppy

```

## Ratpoison and display managers

Many [display managers](/index.php/Display_manager "Display manager") (e.g., [LightDM](/index.php/LightDM "LightDM")) source the available sessions from `/usr/share/xsessions/` and most window managers and desktop environments create .desktop files there. However ratpoison instead creates a `ratpoison.desktop` file in `/etc/X11/sessions/`. To allow display managers to find ratpoison one may need to copy the ratpoison.desktop file from `/etc/X11/sessions/ratpoison.desktop` to `/usr/share/xsessions/ratpoison.desktop`. If the `/usr/share/xsessions` directory does not exist, create it as root.

## See also

*   [The Ratpoison wiki](http://ratpoison.wxcvbn.org/)
*   [X11 Keys in Ratpoison](http://stumpwm.svkt.org/cgi-bin/ratpoison.pl?action=browse;id=keys)
*   [Ratpoison config sample](http://www.ormiret.com/?q=node/11)
*   [Share your Ratpoison (experience) forum thread](https://bbs.archlinux.org/viewtopic.php?id=68622)
*   [Collection of scripts for the Ratpoison window manager](https://github.com/jbaber/ratpoison_scripts)
*   [Stumpwm - a successor to Ratpoison written in Common lisp](http://www.nongnu.org/stumpwm/)