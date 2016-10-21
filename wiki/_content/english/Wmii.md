[wmii](http://wmii.suckless.org/) (window manager improved 2) is a dynamic window manager for X11\. It supports classic and dynamic window management with extended keyboard, mouse, and filesystem based remote control. It replaces the workspace paradigm with a new tagging approach.

The following tips are intended to help the user get started with wmii. While wmii can be configured in almost any language, this article will focus on using the **wmiirc** configuration file, which is simply a shell script. Please see the [ruby-wmii](/index.php/Ruby-wmii "Ruby-wmii") article to see how to configure wmii in ruby.

Please note that wmii does not appear to be in active development, so any bugs encountered are likely to stay.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting wmii](#Starting_wmii)
*   [3 Configuration](#Configuration)
    *   [3.1 Configuration Variables](#Configuration_Variables)
    *   [3.2 Window Colors](#Window_Colors)
*   [4 Usage](#Usage)
    *   [4.1 Layouts](#Layouts)
        *   [4.1.1 Floating layout](#Floating_layout)
    *   [4.2 Views and Tagging](#Views_and_Tagging)
*   [5 WMII filesystem](#WMII_filesystem)
*   [6 Tips and tricks](#Tips_and_tricks)
    *   [6.1 Weechat Highlight Notification](#Weechat_Highlight_Notification)
    *   [6.2 Mod4 on an old Thinkpad](#Mod4_on_an_old_Thinkpad)
    *   [6.3 Nice fonts](#Nice_fonts)
    *   [6.4 Keyboard layouts](#Keyboard_layouts)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [wmii](https://www.archlinux.org/packages/?name=wmii) package.

The source can be found on [the project's Google Code page](https://code.google.com/p/wmii/) and is also [mirrored on GitHub](https://github.com/sunaku/wmii).

## Starting wmii

Select *wmii* from the menu in a [display manager](/index.php/Display_manager "Display manager") of choice.

Alternatively, to start wmii with *startx*, edit your `~/.xinitrc` file, adding the following:

 `~/.xinitrc` 
```
 exec wmii

```

To allow for starting wmii without logging off or killing the X session, add the following to `~/.xinitrc`:

 `~/.xinitrc` 
```
 until wmii; do
   true
 done

```

Upon your first login, you will be greeted with the wmii welcome message, which also includes a short tutorial on wmii. Completing this tutorial will give you a good idea of how wmii works.

**Tip:** If the welcome message does not appear, install [xorg-xmessage](https://www.archlinux.org/packages/?name=xorg-xmessage). Then you can read the welcome message by pressing `$MODKEY-a` and selecting 'welcome'.

## Configuration

The easiest way to start configuring wmii, is to copy the default wmiirc file to your home directory and changing it to your needs. For version 3.9,

```
mkdir ~/.wmii
cp /etc/wmii/wmiirc ~/.wmii/

```

Or just create ~/.wmii/wmiirc_local if you want only basic customization such as fonts, colors etc.

For earlier versions,

```
mkdir ~/.wmii/wmii-$VERSION
cp /etc/wmii/wmiirc ~/.wmii/wmii-$VERSION/

```

By editing this file, you can change things such as color, background, modkey, etc. Keep in mind that wmiirc uses tabbed indentation in case your editor of choice is configured to only produce spaces. Mixing the two indenting styles may cause unexpected behavior.

### Configuration Variables

```
# Configuration Variables
MODKEY=Mod1
UP=k
DOWN=j
LEFT=h
RIGHT=l

```

Change Mod1 to Mod4 if you want to use Windows key instead of Alt. You can also change h, j, k, l, if you like.

### Window Colors

```
# Colors tuples: "<text> <background> <border>"
WMII_NORMCOLORS='#ffffff #000000 #ffffff'
WMII_FOCUSCOLORS='#ffffff #5c0000 #ffffff'

```

```
WMII_BACKGROUND='#333333'
WMII_FONT='fixed'

```

Colors of unselected window are in NORMCOLORS variable. Colors of selected window are in FOCUSCOLOR variable. You can change the background color (if you use transparent terminal) with the WMII_BACKGROUND variable.

## Usage

If you are not familiar with tiling WMs, it's not really easy to begin with it. You must learn a few basic hotkeys to launch programs and place or resize windows. It is a good idea to write the basic hotkeys on paper and stick these on your monitor until you memorize them. By default, the "Mod" key is Alt. Some default hotkeys are :

```
   * Mod+Enter -> Terminal
   * Mod+p -> wimenu : a menu appears, just type the beginning of the name of the application 
     to open it.
   * Mod+d -> default layout : windows are divided on screen
   * Mod+s -> stacked layout : the selected window take all the screen, we just see the title 
     bar of the others.
   * Mod+j -> select the window below
   * Mod+k -> select the window above
   * Shift+Mod+j -> move the window down
   * Shift+Mod+k -> move the window up
   * Mod+a -> Actions menu : choose "quit" to quit

```

N.B. For commonly used programs you can make use of *history.progs*, Mod+p and up/down arrow keys to select previous entries.

By default, only one column is used by the desktop (i.e. the entire screen). It's possible to use several columns with h and l :

```
   * Mod+Shift+h : move the selected window left
   * Mod+Shift+l : move the selected window right
   * Mod+h : select the column on the left
   * Mod+l : select the column on the right 

```

Columns are created automatically, with your placements of the windows. You can make them bigger or smaller, clicking beetween two columns.

### Layouts

You begin in "default" layout : all windows take the same space. You can make them bigger or smaller by clicking in the little square in the title bar of a window.

```
   * "default" layout (Mod+d) : all windows take the same space.
   * "stacked" layout (Mod+s) : the selected window takes the entire column, but you can see 
      the title bar of other windows.
   * "maximum" layout (Mod+m) : the selected window takes the entire column, you do not see 
      other windows.
   * "fullscreen" layout (Mod+f) : the selected window takes runs in full screen.

```

#### Floating layout

You can place your windows like a classic window manager. It's called floating layout. It's useful for some applications, like the Gimp, mplayer, vlc etc.

```
   * Mod+Shift+Space : Move selected window in floating layout.
   * Mod+Space : switch between floating layout and normal layout. 

```

In the floating layout, we can select a window with Mod+j and Mod+k. We can change dimensions of the window, by dragging, like in any other window manager. But we can use hotkeys for that as well :

```
   * Mod+Left click : move window
   * Mod+Right click : change dimensions of the window (you can use it in other layouts too)

```

### Views and Tagging

Tagging in wmii is very similar to the concept of virtual desktops in other window managers. However, tagging is slightly more powerful because it makes it very easy to group windows in multiple ways concurrently. This is made possible by the fact that WMII easily allows each window to have multiple tags. This allows you to group applications for specific use cases and easily switch between them without having to tear down your previous environment by sending applications to another "Desktop".

By default, when you first start up wmii you will see the word 'nil' in the lower left corner. You are at the 'nil' view. The first application you start (such as a terminal: Mod+Enter) will automatically be tagged with a "1" and you will be automatically switched to view "1". Views can be navigated or changed with built in keybindings:

```
   * Mod+Shift+2 : tag selected window to view "2"
   * Mod+2 : this switches you to view "2" where you can see all windows tagged with "2"

```

It's the same thing for all numbers, from 0 to 9\. But you can also use names :

```
   * Mod+t : views menu : you can select a tag with right and left keys, or type the name 
     of the tag (or just a part of the name, if it was created).

   * Mod+Shift+t : this retags the currently selected window with whatever you type into 
     the menu.

   * N.B If using plan9port a *history.tags* file is generated in .wmii-*/. You can use 
     up/down arrow keys to recall previous entries for simple re-tagging/window viewing.

```

You can tag windows with multiple views by using a '+' between the tag names :

```
   * Mod+Shift+t foo+bar+2 : this tags the currently selected window to the views "foo",
     "bar" and "2".

```

You can remove a single tag from multi-tagged windows by selecting the one you wish to remove and using Mod+Shift+t, -tag *name/number* ie Urxvt is multi-tagged on views 1 2 3 and 4, if you jumped to 3 and typed exit, all instances of urxvt will be terminated, using Mod+Shift+t, -3 will only remove that single view.

Tags can be set for specific applications in the wmiirc configuration file.

```
# Tagging Rules
wmiir write /tagrules <<!
/Firefox.*/ -> ~+2
/Gimp.*/ -> ~+3
/.*/ -> sel
/.*/ -> 1
!

```

With the above tag rules, firefox starts in floating mode (~) on view "2". Gimp starts in floating mode on view "3".

**Note:** Applications need to spawn an X-window in order to be automatically assigned tags. Therefore, in order to launch your terminal based programs you will need to prepend something like *urxvt -e <program>* if want to make use of this feature.

## WMII filesystem

WMII's filesystem is based on the [9P protocol](http://9p.cat-v.org). Every element (windows, statusbar, ...) is represented as a file. This makes several cool things possible. For example you can display the song you're currently listening to in the statusbar (for example with MPD and MPC).

**Note:** This filesystem is not permanent and you have to set up everything again after reboot. To make your changes "permanent" simply write the right commands into your wmiirc.

You can access the filesystem with the *wmiir* command. For instance, you can list the root directory with *wmiir ls /*

```
client/
colrules
ctl
event
keys
lbar/
rbar/
tag/
tagrules

```

You can use *wmiir read* to look into files: *wmiir read /tag/sel/index*

```
# ~ 1280 785
~ 0x160000d 731 394 486 332 xterm:XTerm:~
# 1 0 1280
1 0x800003 0 785 opera:Opera:Editing Wmii - Preview - ArchWiki - Opera

```

So this is the info for the **sel**ected (current) tag. As you can see, I've got one floating xterm and Opera running on this tag. The first number in this output indicates the column of the window. ~ is the floating column and 1 ist (obviously) the first column. The second column is the XServer-ID for the client. The next columns are the coordinates and the size of the window. The last column ist the titlebar of the window.

You can create new files with *wmiir create*:

```
echo Arch is best | wmiir create /rbar/arch

```

Now you should see "Arch is best" in your statusbar

"wmiir create" reads from STDIN. So you can pipe any information you like into your statusbar. "wmiir write" works in a similar fashion but doesn't create new files.

**Note:** Note for /rbar and /lbar:The elements in those status bars are in alphabetical order.

You can remove files with rm or remove

If you like to have a program on several tags you can use:

```
echo "3+5+8" | wmiir write /client/0x800003/tags

```

Now my Opera window appears on Tags 3,5 and 8.

But there are easier ways to accomplish this ;) Just type MOD+shift+t and enter "3+5+8" and you get the same result for the currently selected client.

**Note:** There's also the possibility to mount WMII's filesystem. Have a look at the [official documentation](http://wmii.suckless.org/9p).

## Tips and tricks

### Weechat Highlight Notification

If you use weechat and want to know when you have been messaged without always having to look at the weechat window, you can use the *launcher.pl* script to send a notice to the bar. To get this working, you will need to create a script that sends your desired notice. Here is very simple example:

```
#!/bin/bash
echo :: NEW MESSAGE :: | wmiir create /lbar/alert
sleep 8
wmiir remove /lbar/alert

```

Then start weechat and load the script.

```
/perl load launcher.pl

```

Then type the following command into weechat:

```
/set plugins.var.perl.launcher.signal.weechat_pv = "/path/to/yourscript"

```

If you are experiencing the "/rbar/alert File not Found" error inside the weechat buffer and its messing up your layout you can try the following fix:

```
/set plugins.var.perl.launcher.signal.weechat_pv = "/path/to/yourscript >/dev/null 2>&"

```

Now, :: NEW MESSAGE :: will appear in the left corner of your bar whenever you have a message highlight. Make sure to place *launcher.pl* the perl/autoload directory so that it starts when weechat starts.

### Mod4 on an old Thinkpad

Although Wmii defaults to Mod1, using Mod4 reduces conflicts in keybindings with many terminal applications. There is a snag for old Thinkpad users, however. They do not have a Mod4 key. To get one, another key has to be assigned to it using xmodmap. To do it, make an *.Xmodmap* file in your home directory and add this to it:

```
keycode 64 = Super_L
add Mod4 = Super_L
remove Mod1 = Super_L

```

You will need to replace 64 with whatever *xev* tells you is the keycode of the key you want to replace. In the above example, I replace left Alt (and use right alt for applications).

### Nice fonts

Wmii now supports Xft, just prefix font name with 'xft'. For instance:

```
export WMII_FONT='xft:Sans-9'

```

### Keyboard layouts

You'd probably like to have its own keyboard layout for each window. However, most of such applications requires system tray while witray is only available in the [development version of wmii](https://aur.archlinux.org/packages.php?ID=3497). [xxkb](https://www.archlinux.org/packages/?q=xxkb) package helps to solve the problem. It has no UI by default. You only need to configure layouts in xorg.conf. Create /etc/X11/xorg.conf.d/20-keyboard.conf and put something like this into it:

```
Section "InputClass"
    Identifier      "Keyboard Defaults"
    MatchIsKeyboard "yes"
    Option          "XkbModel"      "pc101"
    Option          "XkbLayout"     "us,ru"
    Option          "XkbOptions"    "grp:ctrl_shift_toggle,compose:prsc"
EndSection

```

Replace layout, options and model to fit your needs. Add

```
xxkb &

```

into your wmiirc and it just works. [xkblayout-state](https://aur.archlinux.org/packages/xkblayout-state/) can be used to put layout indicator into the status line:

```
status() {
    echo -n label $(xkblayout-state print "%s") '|' $(date +"%a %b %d %H:%M")
}

```

## See also

*   [wmii Website](https://code.google.com/p/wmii/) -- the official website of wmii
*   [dmenu](/index.php/Dmenu "Dmenu") -- a simple application launcher which binds well with dwm and wmii
*   [user guide](http://wmii.googlecode.com/hg/doc/wmii.pdf) -- latest wmii guide (pdf)
*   [The wmii thread](https://bbs.archlinux.org/viewtopic.php?id=22592)
*   [wmii colour themes](https://sites.google.com/site/blijvend/home-1/notes/wmiicolor)
*   [ruby-wmii](http://eigenclass.org/hiki.rb?wmii+ruby) -- Ruby configuration and scripting for wmii 3.1
*   [sunaku's wmiirc](https://github.com/sunaku/wmiirc) -- Ruby configuration and scripting for wmii 3.9+ and wmii-hg
*   [Ben's wmiirc](http://pastebin.com/Xyn0mEjr) -- Simple wmiirc with extra widgets (vol, mpd, mail, clock) and other modifications
*   mailing list is dev@suckless.org, see official website
*   IRC channel is #wmii on the OFTC IRC network