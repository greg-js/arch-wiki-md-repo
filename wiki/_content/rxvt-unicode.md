# rxvt-unicode

[rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html) is a highly customizable [terminal emulator](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator") forked from [rxvt](https://en.wikipedia.org/wiki/Rxvt "wikipedia:Rxvt"). Commonly known as `urxvt`, rxvt-unicode can be [daemonized](/index.php/Daemon "Daemon") to run clients within a single [process](https://en.wikipedia.org/wiki/Process_(computing) "wikipedia:Process (computing)") in order to minimize the use of system resources. Developed by Marc Lehmann, some of the more outstanding features of rxvt-unicode include international language support through [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode"), the ability to display multiple font types and support for [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl") extensions.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Creating ~/.Xresources](#Creating_.7E.2F.Xresources)
    *   [2.2 True transparency](#True_transparency)
    *   [2.3 Native transparency](#Native_transparency)
    *   [2.4 Scrollbar](#Scrollbar)
    *   [2.5 Scrollback position](#Scrollback_position)
    *   [2.6 Scrollback buffer in secondary screen](#Scrollback_buffer_in_secondary_screen)
    *   [2.7 Font declaration methods](#Font_declaration_methods)
    *   [2.8 Set icon](#Set_icon)
    *   [2.9 Set as login shell](#Set_as_login_shell)
    *   [2.10 Use urxvt as application launcher](#Use_urxvt_as_application_launcher)
    *   [2.11 Font spacing](#Font_spacing)
*   [3 Perl extensions](#Perl_extensions)
    *   [3.1 Clickable URLs](#Clickable_URLs)
    *   [3.2 Yankable URLs (no mouse)](#Yankable_URLs_.28no_mouse.29)
    *   [3.3 Simple tabs](#Simple_tabs)
    *   [3.4 Advanced tab management](#Advanced_tab_management)
    *   [3.5 Fullscreen](#Fullscreen)
    *   [3.6 Scrollwheel support](#Scrollwheel_support)
    *   [3.7 Changing font size on the fly](#Changing_font_size_on_the_fly)
    *   [3.8 Disabling Perl extensions](#Disabling_Perl_extensions)
*   [4 Colors](#Colors)
    *   [4.1 Xterm-like colors](#Xterm-like_colors)
*   [5 Improving performance](#Improving_performance)
    *   [5.1 Daemon-client](#Daemon-client)
        *   [5.1.1 Xinitrc](#Xinitrc)
        *   [5.1.2 systemd](#systemd)
*   [6 Cut and paste](#Cut_and_paste)
    *   [6.1 Default key bindings](#Default_key_bindings)
    *   [6.2 Custom key bindings](#Custom_key_bindings)
    *   [6.3 Clipboard management](#Clipboard_management)
    *   [6.4 Automatic script management](#Automatic_script_management)
*   [7 Improved Kuake-like behavior in Openbox](#Improved_Kuake-like_behavior_in_Openbox)
    *   [7.1 Scriptlets](#Scriptlets)
    *   [7.2 urxvtq with tabbing](#urxvtq_with_tabbing)
        *   [7.2.1 Tab control](#Tab_control)
    *   [7.3 Openbox configuration](#Openbox_configuration)
    *   [7.4 Further configuration](#Further_configuration)
    *   [7.5 Related scripts](#Related_scripts)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 ~/.Xresources is not being sourced](#.7E.2F.Xresources_is_not_being_sourced)
    *   [8.2 Transparency not working after upgrade to v9.09](#Transparency_not_working_after_upgrade_to_v9.09)
    *   [8.3 Remote hosts](#Remote_hosts)
    *   [8.4 Using rxvt-unicode as gmrun terminal](#Using_rxvt-unicode_as_gmrun_terminal)
    *   [8.5 My numerical keypad acts weird and generates differing output? (e.g. in vim)](#My_numerical_keypad_acts_weird_and_generates_differing_output.3F_.28e.g._in_vim.29)
    *   [8.6 Pseudo-tty](#Pseudo-tty)
    *   [8.7 Key combinations do not work](#Key_combinations_do_not_work)
    *   [8.8 Slow performance when drawing glyphs](#Slow_performance_when_drawing_glyphs)
*   [9 External resources](#External_resources)

## Installation

[rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) is available in the [official repositories](/index.php/Official_repositories "Official repositories") and includes 256 color support.

[rxvt-unicode-patched](https://aur.archlinux.org/packages/rxvt-unicode-patched/) is available in the [AUR](/index.php/AUR "AUR") and includes a fix for the font width bug.

## Configuration

See the [rxvt-unicode reference page](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod) for the complete list of available setting and values.

### Creating ~/.Xresources

The look, feel, and function of rxvt-unicode is controlled by command-line arguments and/or [X resources](/index.php/X_resources "X resources"). X resources can be set using `~/.Xresources` and _xrdb_ ([xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb)), see the [X resources](/index.php/X_resources "X resources") article for details.

Append commented list of all _rxvt_ resources to your `~/.Xresources` file:

```
 urxvt --help 2>&1| sed -n '/:  /s/^ */! URxvt*/gp' >> ~/.Xresources

```

Or for a commented list + helpful descriptions:

 `TERM=rxvt-unicode-256color command man -Pcat urxvt | sed -n '/depth: b/,/^BA/p'|sed '$d'|sed '/^       [a-z]/s/^ */^/g'|sed -e :a -e 'N;s/\n/@@/g;ta;P;D'|sed 's,\^\([^@]\+\)@*[\t ]*\([^\^]\+\),! \2\n! URxvt*\1\n\n,g'|sed 's,@@\(  \+\),\n\1,g'|sed 's,@*$,,g'|sed '/^[^!]/d'|tr -d "'\`" >> ~/.Xresources` 

**Note:** Command-line arguments override, and take precedence over resource settings

### True transparency

To use true transparency, you need to be using a [window manager](/index.php/Window_manager "Window manager") that supports compositing or a separate compositor.

From the command-line:

```
$ urxvt -depth 32 -bg rgba:3f00/3f00/3f00/dddd

```

Using the configuration file:

 `~/.Xresources` 

```
URxvt.depth: 32
URxvt.background: rgba:1111/1111/1111/dddd

```

or

 `~/.Xresources` 

```
URxvt.depth: 32
URxvt.background: [95]#000000

```

where '95' is the opacity level in percentage and '#000000' is the background color.

To use a color i.e. #302351 with the rgba:rrrr/gggg/bbbb/aaaa syntax it would be rgba:3000/2300/5100/ee00\. "ee00" (the alpha value) to make it nicely transparent.

**Note:** To make these settings universal for all forms of URxvt, you may add a wildcard. For example, `URxvt.depth` would become `URxvt*.depth`.

### Native transparency

If there is no need for true transparency, or if compositing uses too many resources on your system, you can get transparency working in the following way:

 `~/.Xresources` 

```
! Xresources file

URxvt*inheritPixmap: true
URxvt*.transparent: true
! URxvt*.shading: 0 to 99 darkens, 101 to 200 lightens
URxvt*.shading: 110

```

Using the URxvt*background setting exemplified above instead of URxvt*.shading will also work.

**Note:** Avoid using shading if you have a `URxvt.tintColor` set. Use a different `tintColor` instead.

### Scrollbar

The look of the scrollbar can be chosen through this entry in `~/.Xresources`:

```
! scrollbar style - rxvt (default), plain (most compact), next, or xterm
URxvt.scrollstyle: rxvt

```

The scrollbar can also be completely deactivated like so:

```
URxvt.scrollBar: false

```

### Scrollback position

By default, when shell output appears the scrollback view will automatically jump to the bottom of the buffer to display new output. If in cases where you want to see previous output (e.g., compiler messages), set the following options in `~/.Xresources`:

```
! do not scroll with output
URxvt*scrollTtyOutput: false

! scroll in relation to buffer (with mouse scroll or Shift+Page Up)
URxvt*scrollWithBuffer: true

! scroll back to the bottom on keypress
URxvt*scrollTtyKeypress: true

```

### Scrollback buffer in secondary screen

When you scroll a pager in a _secondary screen_(e.g. `less` without the `**-X**` option), it may be a good idea to disable the scrollback buffer to be able to scroll in the pager _itself_, instead of the terminal's buffer: this is default and unchangeable behaviour in konsole and vte-based terminals. In urxvt, to disable the scrollback buffer for the _secondary screen_:

```
URxvt.secondaryScreen: 1
URxvt.secondaryScroll: 0

```

The above configuration works as expected except when scrolling with a mouse wheel. When you scroll a pager in the _secondary screen_ with the mouse wheel - and there has been something in the scrollback buffer, instead of the pager itself - the scrollback buffer will be scrolled by the mouse wheel. To solve this issue, it is necessary to introduce a new option into rxvt-unicode[[1]](https://bbs.archlinux.org/viewtopic.php?id=132150). A patched rxvt-unicode is available in AUR as [rxvt-unicode-better-wheel-scrolling](https://aur.archlinux.org/packages/rxvt-unicode-better-wheel-scrolling/). After installing it, add the following to the configuration file:

```
URxvt.secondaryWheel: 1

```

**Note:** Please do not use this option with the [vtwheel](#Scrollwheel_support) perl extension, it will mess up.

### Font declaration methods

```
URxvt.font: 9x15

```

is the same as:

```
URxvt.font: -misc-fixed-medium-r-normal--15-140-75-75-c-90-iso8859-1

```

And, for the same font in bold:

```
URxvt.font: 9x15bold

```

is the same as:

```
URxvt.font: -misc-fixed-bold-r-normal--15-140-75-75-c-90-iso8859-1

```

The complete list of short names for X core fonts can be found in `/usr/share/fonts/misc/fonts.alias` (there is also some fonts.alias files in some of the other subdirectories of `/usr/share/fonts/`, but as they are packaged separately from the actual fonts, they may list fonts you do not actually have installed). It is worth noting that these short aliases select for ISO-8859-1 versions of the fonts rather than ISO-10646-1 (Unicode) versions, and 75 DPI rather than 100 DPI versions, so you are probably better off avoiding them and choosing fonts by their full long names instead.

**Note:** The above paragraph is only for bitmap fonts. Other fonts can be used through Xft using the following format:

```
URxvt.font: xft:monaco:size=10

```

Or

```
URxvt.font: xft:monaco:bold:size=10

```

**Note:**

*   If there is a hyphen(-) in an Xft font name, it must be escaped with backslash(\) twice. It's different from the usage of urxvt -fn option and the result that fc-list returns, where backslash present only once
*   You will see a new font only after restart X

A nice method for testing out fonts in a live terminal before committing to the config is by printing escape codes in the terminal, for example:

```
$ printf '\e]710;%s\007' "xft:Terminus:pixelsize=12"

```

### Set icon

**Note:** Because of a bug report[FS#34862](https://bugs.archlinux.org/task/34862) complaining that the rxvt-unicode package had too many dependencies, you must now install the AUR package [rxvt-unicode-pixbuf](https://aur.archlinux.org/packages/rxvt-unicode-pixbuf/) in order to use the icon option.

By default URxvt does not feature a taskbar icon. However, this can be easily changed by adding the following line to `~/.Xresources` and pointing to the desired icon:

```
URxvt.iconFile:    /usr/share/icons/Clarity/scalable/apps/terminal.svg

```

### Set as login shell

This will cause the shell to be started as a login shell, like the option `-ls`.

```
URxvt*loginShell: true

```

### Use urxvt as application launcher

urxvt can be used as a lightweight alternative to application launchers such as [gmrun](https://www.archlinux.org/packages/?name=gmrun). Run urxvt with the following configuration to imitate look and behaviour of an application launcher or assign the command to a custom alias:

```
$ urxvt -geometry 80x3 -name 'bashrun' -e sh -c "/bin/bash -i -t"

```

### Font spacing

By default the distance between characters can feel too wide. It's controlled by this entry:

 `~/.Xresources` 

```
URxvt.letterSpace: -1

```

Here `-1` decreases the spacing by one pixel, but can be adjusted as needed.

## Perl extensions

We can enable URxvt perl extensions by including the following line:

```
 URxvt.perl-ext-common: extension_name_1,extension_name_2,...

```

Please take note that there **should not** be any spacing between extension names.

### Clickable URLs

You can make URLs in the terminal clickable using the matcher extension. For example, to open links in [Firefox](/index.php/Firefox "Firefox") add the following to `.Xresources`:

```
URxvt.perl-ext-common: default,matcher
URxvt.url-launcher: /usr/bin/firefox
URxvt.matcher.button: 1

```

Since rxvt-unicode 9.14, it's also possible to use matcher to open and list recent (currently limited to 10) URLs via keyboard:

```
URxvt.keysym.C-Delete: perl:matcher:last
URxvt.keysym.M-Delete: perl:matcher:list

```

Matching links can be colored with a chosen foreground or background [color](#Colors), for example blue:

```
URxvt.matcher.rend.0: Uline Bold fg5

```

Alternatively, use `colorUL` for a #RRGGBB color. This will however color all underlined text, instead of only link matches:

```
URxvt.colorUL: #4682B4

```

### Yankable URLs (no mouse)

In addition, you can select and open URLs in your web browser without using the mouse. Install the [urxvt-perls](https://www.archlinux.org/packages/?name=urxvt-perls) package from the [official repositories](/index.php/Official_repositories "Official repositories") and adjust your `.Xresources` as necessary. An example is shown below:

```
URxvt.perl-ext: default,url-select
URxvt.keysym.M-u: perl:url-select:select_next
URxvt.url-select.launcher: /usr/bin/xdg-open
URxvt.url-select.underline: true

```

**Note:** This extension replaces the Clickable URLs extension mentioned above, so `matcher` can be removed from the `URxvt.perl-ext` list.

**Key commands:**

| Key | Description |
| Alt+u | Enter selection mode. The last URL on your screen will be selected. You can repeat `Alt+u` to select the next upward URL. |
| k | Select next upward URL |
| j | Select next downward URL |
| Return | Open selected URL in browser and quit selection mode |
| o | Open selected URL in browser without quitting selection mode |
| y | Copy (yank) selected URL and quit selection mode |
| Esc | Cancel URL selection mode |

### Simple tabs

To add tabs to urxvt, add the following to your `~/.Xresources`:

```
URxvt.perl-ext-common: ...,tabbed,...

```

To control tabs use:

| Key | Description |
| Shift+Down | New tab |
| Shift+Left | Go to left tab |
| Shift+Right | Go to right tab |
| Ctrl+Left | Move tab to the left |
| Ctrl+Right | Move tab to the right |
| Ctrl+d | Close tab |

You can change the colors of tabs with the following:

```
URxvt.tabbed.tabbar-fg: 2
URxvt.tabbed.tabbar-bg: 0
URxvt.tabbed.tab-fg: 3
URxvt.tabbed.tab-bg: 0

```

### Advanced tab management

Install the [urxvt-tabbedex](https://aur.archlinux.org/packages/urxvt-tabbedex/) package from [AUR](/index.php/AUR "AUR"), then add the `tabbedex` value to the `URxvt.perl-ext-common` X resource in your `~/.Xresources`:

```
URxvt.perl-ext-common: ...,tabbedex,...

```

**Note:** If you have previously used the `tabbed` Perl extension and have defined the `tabbed` value for the `URxvt.perl-ext-common` X resource, please remove the `tabbed` value first to avoid conflict with `tabbedex`.

By default, the "[NEW]" button (which is rarely used and usable only with the mouse) is disabled with tabbedex. You can reenable this feature by setting the `new-button` to yes.

```
URxvt.tabbed.new-button: true

```

Tabs can be named with `Shift+ ↑` (`Enter` to confirm, `Escape` to cancel).

To automatically hide the tabs bar when only one tab is present, enable the following resource:

```
URxvt.tabbed.autohide: true

```

To prevent the last tab from closing Urxvt, enable the following resource:

```
URxvt.tabbed.reopen-on-close: yes

```

To start a new tab or cycle through tabs, use the following user commands: `tabbedex:(new|next|prev)_tab`. Example of mappings:

```
URxvt.keysym.Control-t: perl:tabbedex:new_tab
URxvt.keysym.Control-Tab: perl:tabbedex:next_tab
URxvt.keysym.Control-Shift-Tab: perl:tabbedex:prev_tab

```

To define your own key bindings to rename a tab or move a tab to the right or to the left, use the following commands: `tabbedex:move_tab_(left|right)` and `tabbedex:rename_tab`. Example of mappings:

```
URxvt.keysym.Control-Shift-Left: perl:tabbedex:move_tab_left
URxvt.keysym.Control-Shift-Right: perl:tabbedex:move_tab_right
URxvt.keysym.Control-Shift-R: perl:tabbedex:rename_tab

```

**Note:** Redefining the keys used for the user commands will not disable the default mappings, you have to set the X resource `no-tabbedex-keys` for that. However, currently it is not included in [urxvt-tabbedex](https://aur.archlinux.org/packages/urxvt-tabbedex/) package. Consider using [urxvt-tabbedex-git](https://aur.archlinux.org/packages/urxvt-tabbedex-git/) package instead:

```
URxvt.tabbed.no-tabbedex-keys: true

```

### Fullscreen

You can install the [AUR](/index.php/AUR "AUR") package [urxvt-fullscreen](https://aur.archlinux.org/packages/urxvt-fullscreen/), and then set a key binding to put urxvt fullscreen.

 `~/.Xresources` 

```
...
URxvt.perl-ext-common: ...,fullscreen,...
URxvt.keysym.F11: perl:fullscreen:switch
...

```

### Scrollwheel support

Install [urxvt-vtwheel](https://aur.archlinux.org/packages/urxvt-vtwheel/) from the [AUR](/index.php/AUR "AUR") and add it to your Perl extensions within `~/.Xresources`:

```
 URxvt.perl-ext-common:  ...,vtwheel,...

```

### Changing font size on the fly

Install [urxvt-resize-font-git](https://aur.archlinux.org/packages/urxvt-resize-font-git/) from the [AUR](/index.php/AUR "AUR"), add it to your Perl extensions within `~/.Xresources`

```
 URxvt.perl-ext-common:  ...,resize-font,...

```

and add some key bindings, for example like this:

```
 URxvt.resize-font.smaller: C-Down
 URxvt.resize-font.bigger: C-Up

```

For the Ctrl+Shift bindings to work, a default binding needs to be disabled (see discussion [here](http://wilmer.gaa.st/blog/archives/36-rxvt-unicode-and-ISO-14755-mode.html)):

```
 URxvt.iso14755: false
 URxvt.iso14755_52: false

```

### Disabling Perl extensions

If you do not use the Perl extension features, you can improve the security and speed by disabling Perl extensions completely.

```
URxvt.perl-ext:
URxvt.perl-ext-common:

```

**Note:** If you use multiple Perl extension features, you can list them in succession, comma-separated: `URxvt.perl-ext-common:default,matcher,tabbed.`

## Colors

By default, rxvt-unicode is compiled with color support. In addition to the default foreground and background colors, rxvt can display up to 256 colors (plus high-intensity bold/blinking/underlined and any mix of these). The look, feel, and function of rxvt-unicode is controlled by command-line arguments called X resources.

A sample `~/.Xresources` for an urxvt terminal with default colors but white fonts on a black background would be written as follow:

 `~/.Xresources` 

```
! Background color
URxvt*background: black

! Font color
URxvt*foreground: white

! Other colors
URxvt*color0: black
URxvt*color1: red3
URxvt*color2: green3
URxvt*color3: yellow3
URxvt*color4: blue2
URxvt*color5: magenta3
URxvt*color6: cyan3
URxvt*color7: gray90
URxvt*color8: grey50
URxvt*color9: red
URxvt*color10: green
URxvt*color11: yellow
URxvt*color12: blue
URxvt*color13: magenta
URxvt*color14: cyan
URxvt*color15: white
```

It is also possible to specify the color values of foreground, background, cursorColor, cursorColor2, colorBD, colorUL as a number 0-15, as a convenient shorthand to reference the color name of color0-color15\. See [#Creating ~/.Xresources](#Creating_.7E.2F.Xresources) to create a commented `~/.Xresources` file for `urxvt`

### Xterm-like colors

By default `urxvt` uses the same colors as `xterm` use except one. Add the following line at the end of your `~/.Xresources` for xterm-like colors:

 `~/.Xresources` 

```
...
URxvt*color12: rgb:5c/5c/ff
```

then merge it contents with your current X resources configuration with:

```
xrdb -merge ~/.Xresources

```

and finally restart `urxvt`.

## Improving performance

*   Avoid the use of Xft fonts. If Xft fonts must be used, append `:antialias=false` to the setting value.[[2]](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod#Can_I_speed_up_Xft_rendering_somehow)
*   Build rxvt-unicode with disabled support for unnecessary features, `--disable-xft` and `--disable-unicode3` in particular.
*   Limit the number of `saveLines` (option `-sl`) in the scrollback buffer to reduce memory usage. [[4]](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod#Isn_t_rxvt_unicode_supposed_to_be_sm)
    *   Use tmux for scrollback buffer and set saveLines to 0
*   [Disable perl](#Disabling_Perl_extensions)
*   Consider running `urxvtd` as a daemon accepting connections from `urxvtc` clients.

### Daemon-client

#### Xinitrc

See the _Examples_ section in `man urxvtd`. This is the preferred option.

#### systemd

**Note:** Regular users cannot execute systemctl power commands (reboot, poweroff, etc) when logged in to a urxvt client/daemon setup which is started through systemd, as the client is not part of the [session](/index.php/Session "Session"). For this reason starting urxvt through systemd is discouraged.

System service:

 `/etc/systemd/system/urxvtd@.service` 

```
[Unit]
Description=RXVT-Unicode Daemon

[Service]
User=%i
ExecStart=/usr/bin/urxvtd -q -o

[Install]
WantedBy=multi-user.target

```

Pass the username when [starting the service](/index.php/Systemd#Using_units "Systemd"):

```
urxvtd@_username_.service

```

For a [systemd/User](/index.php/Systemd/User "Systemd/User") service, place the following unit files in `~/.config/systemd/user`:

 `urxvtd.service` 

```
[Unit]
Description=Urxvt Terminal Daemon
Requires=urxvtd.socket

[Service]
ExecStart=/usr/bin/urxvtd -o -q
Environment=RXVT_SOCKET=%t/urxvtd-%H

[Install]
WantedBy=_MyTarget_.target

```

 `urxvtd.socket` 

```
[Unit]
Description=urxvt daemon (socket activation)
Documentation=man:urxvtd(1) man:urxvt(1)

[Socket]
ListenStream=%t/urxvtd-%H

[Install]
WantedBy=sockets.target

```

## Cut and paste

**Note:** With the use of a terminal multiplexer, urxvt (or any terminal emulator) `CLIPBOARD` integration will not be effective, since it will not be possible to select all of the desired text in a straightforward fashion or at all, in some cases (e.g., when the active multiplexed terminal is changed to another one and then back to the original one, and one selects text beyond what is visible, which causes text from the other terminal to be displayed). Obviously this is due to the fact that the terminal emulator lacks the ability to distinguish between multiplexed terminals. Therefore, it would be effectively redundant for one who always uses a terminal multiplexer capable of maintaining a scrollback buffer and integrating with `CLIPBOARD` (e.g. [tmux](/index.php/Tmux "Tmux") with [customized key bindings](/index.php/Tmux#Key_bindings "Tmux")) to integrate `CLIPBOARD` with urxvt.

For users unfamiliar with [Xorg](/index.php/Xorg "Xorg") data transfer methods, the exchange of information to and from rxvt-unicode can become a burden. Suffice to say that rxvt-unicode uses cut buffers which are typically loaded into the current `PRIMARY` selection by default. [[5]](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod#THE_SELECTION_SELECTING_AND_PASTING_) Users are urged to review [Wikipedia:X Window selection](https://en.wikipedia.org/wiki/X_Window_selection "wikipedia:X Window selection") for additional information.

### Default key bindings

Default X key bindings will still work for copying and pasting. After selecting the text Ctrl+Insert or Ctrl+Alt+C can be used to copy and Shift+Insert or Ctrl+Alt+V to paste.

### Custom key bindings

To enable copy/paste using Ctrl+Shift+c/Ctrl+Shift+v, or similar, you will need to edit your .Xresources. First add the extension:

```
URxvt.perl-ext-common: default,clipboard

```

Then disable iso14755:

```
URxvt.iso14755: False

```

And bind the keys:

```
URxvt.keysym.Shift-Control-C: perl:clipboard:copy
URxvt.keysym.Shift-Control-V: perl:clipboard:paste

```

If using xsel (which is the default), use:

```
URxvt.clipboard.copycmd:  xsel -ib
URxvt.clipboard.pastecmd: xsel -ob

```

These two settings can be changed for other clipboard managers such as xclip.

### Clipboard management

See [Clipboard#List of clipboard managers](/index.php/Clipboard#List_of_clipboard_managers "Clipboard")

### Automatic script management

**Note:** Since version 9.20, [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) comes with a new `selection-to-clipboard` extension that supersedes the scripts below. Enable it like any other extension.

Skottish[[6]](https://bbs.archlinux.org/viewtopic.php?pid=506845#p506845) created a Perl script to automatically copy any selection in rxvt-unicode to the X clipboard. Save the following as `/usr/lib/urxvt/perl/clipboard`:

```
#! /usr/bin/perl

sub on_sel_grab {
    my $query=quotemeta $_[0]->selection;
    $query=~ s/\n/\\n/g;
    $query=~ s/\r/\\r/g;
    system( "echo -en " . $query . " | xsel -i -b -p" );
}

```

Xyne has also created his own variation of Skottish's script named [urxvt-clipboard](https://aur.archlinux.org/packages/urxvt-clipboard/) which is available in the [AUR](/index.php/AUR "AUR") that allows the user to paste the selection with `Ctrl+V` instead of only with a middle mouse click:

```
#! /usr/bin/perl

sub on_sel_grab
{
  my $query = $_[0]->selection;
  open (my $pipe,'|-','xsel -ib') or die;
  print $pipe $query;
  close $pipe;
  open (my $pipe,'|-','xsel -ip') or die;
  print $pipe $query;
  close $pipe;
}

```

It also requires [xsel](https://www.archlinux.org/packages/?name=xsel) and needs to be enabled in the `*perl-ext-common` or `*perl-ext` field in `~/.Xresources`. For example:

```
URxvt.perl-ext-common: default,clipboard

```

The [AUR](/index.php/AUR "AUR") package [urxvt-perls-git](https://aur.archlinux.org/packages/urxvt-perls-git/) is another option one can use. [urxvt-perls-git](https://aur.archlinux.org/packages/urxvt-perls-git/) includes the same functionality as [urxvt-clipboard](https://aur.archlinux.org/packages/urxvt-clipboard/), in addition to the keyboard-select and url-select Perl extensions.

## Improved Kuake-like behavior in Openbox

This was originally posted on the forum by Xyne [[7]](https://bbs.archlinux.org/viewtopic.php?pid=550380), and it relies on the [xdotool](https://www.archlinux.org/packages/?name=xdotool) found in the [official repositories](/index.php/Official_repositories "Official repositories").

### Scriptlets

Save this scriptlet from the `urxvtc` man page somewhere on your system as `urxvtc` (e.g., in `~/.config/openbox`):

```
#!/bin/sh

urxvtc "$@"
if [ $? -eq 2 ]; then
   urxvtd -q -o -f
   urxvtc "$@"
fi

```

and save this one as `urxvtq`:

```
#!/bin/bash

wid=$(xdotool search --classname urxvtq)
if [ -z "$wid" ]; then
  /path/to/urxvtc -name urxvtq -geometry 80x28
  wid=$(xdotool search --classname urxvtq | head -1)
  xdotool windowfocus "$wid"
  xdotool key Control_L+l
else
  if [ -z "$(xdotool search --onlyvisible --classname urxvtq 2>/dev/null)" ]; then
    xdotool windowmap "$wid"
    xdotool windowfocus "$wid"
  else
    xdotool windowunmap "$wid"
  fi
fi

```

A previous version of [xdotool](https://www.archlinux.org/packages/?name=xdotool) introduced a bug which disabled recognition of visible windows and thus led some users to use the following scriptlet in place of the previous one. This is no longer necessary as of [xdotool](https://www.archlinux.org/packages/?name=xdotool) >= 1.20100416.2809, but it has been left here for future reference.'

```
#!/bin/bash

wid=$(xprop -name urxvtq | grep 'WM_COMMAND' | awk -F ',' '{print $3}' | awk -F '"' '{print $2}')
if [ -z "$wid" ]; then
  /path/to/urxvtc -name urxvtq -geometry 200x28
  wid=$(xprop -name urxvtq | grep 'WM_COMMAND' | awk -F ',' '{print $3}' | awk -F '"' '{print $2}')
  xdotool windowfocus "$wid"
  xdotool key Control_L+l
else
  if [ -z "$(xprop -id "$wid" | grep 'window state: Normal' 2>/dev/null)" ]; then
    xdotool windowmap "$wid"
    xdotool windowfocus "$wid"
  else
    xdotool windowunmap "$wid"
  fi
fi

```

Make sure that you change `/path/to/urxvtc` to the actual path to the `urxvtc` scriptlet that you saved above. We will be using `urxvtc` to launch both regular instances of `urxvt` and the kuake-like instance.

### urxvtq with tabbing

If you want to have tabs in your kuake-like `urxvtc` (here called `urxvtq`) just replace the third line in your `urxvtq`:

```
wid=$(xdotool search --name urxvtq)

```

with:

```
wid=$(xdotool search --name urxvtq | grep -m 1 "" )

```

To activate tab support, you can either replace the fifth line of your `urxvtq`:

```
/path/to/urxvtc -name urxvtq -geometry 80x28

```

with:

```
/path/to/urxvtc -name urxvtq -pe tabbed -geometry 80x28

```

or replace this line of your `~/.Xresources` file:

```
URxvt.perl-ext-common: default,matcher

```

with

```
URxvt.perl-ext-common: default,matcher,tabbed

```

#### Tab control

| Key | Description |
| Shift+Left | Switch to the tab left of the current one |
| Shift+Right | Switch to the tab right of the current one |
| Shift+Down | Create a new tab |

You can also use your mouse to switch the tabs by clicking the wished one and create a new tab by clicking on _[NEW].\\_

To close a tab just enter `exit` like you would to normally close a terminal.

### Openbox configuration

Now add the following lines to the `<applications>` section of `~/.config/openbox/rc.xml`:

```
<application name="urxvtq">
   <decor>no</decor>
   <position force="yes">
     <x>center</x>
     <y>0</y>
   </position>
   <desktop>all</desktop>
   <layer>above</layer>
   <skip_pager>yes</skip_pager>
   <skip_taskbar>yes</skip_taskbar>
   <maximized>Horizontal</maximized>
</application>
```

and add these lines to the `<keyboard>` section:

```
<keybind key="W-t">
  <action name="Execute">
    <command>/path/to/urxvtc</command>
  </action>
</keybind>
<keybind key="W-grave">
  <action name="Execute">
    <execute>/path/to/urxvtq</execute>
  </action>
</keybind>
```

Here too you need to change the `/path/to/*` lines to point to the scripts that you saved above. Save the file and then reconfigure Openbox. You should now be able to launch regular instances of urxvt with `Super+T`, and toggle the kuake-like console with `Super+**`**` (the grave key also known as the backtick).

### Further configuration

The advantage of this configuration over the urxvt kuake Perl script is that Openbox provides more keybinding options such as modifier keys. The kuake script hijacks an entire physical key regardless of any modifier combination. Review the [Openbox bindings documentation](http://openbox.org/wiki/Help:Bindings) for the full range or possibilities.

The [Openbox per-app settings](http://openbox.org/wiki/Help:Applications) can be used to further configure the behavior of the kuake-like console (e.g. screen position, layer, etc.). You may need to change the "geometry" parameter in the `urxvtq` scriptlet to adjust the height of the console.

### Related scripts

*   hbekel has posted a generalized version of the `urxvtq` [here](https://bbs.archlinux.org/viewtopic.php?pid=550380#p550380) which can be used to toggle any application using [xdotool](https://www.archlinux.org/packages/?name=xdotool).
*   [http://www.jukie.net/~bart/blog/20070503013555](http://www.jukie.net/~bart/blog/20070503013555) - A script for opening URLs with your keyboard instead of mouse with urxvt.

## Troubleshooting

### ~/.Xresources is not being sourced

In some cases where _urxvt_ does not acknowledge `~/.Xresources`, you may need to add `xrdb -merge ~/.Xresources` to your `~/.xinitrc` file. See [X resources](/index.php/X_resources "X resources") for more information.

### Transparency not working after upgrade to v9.09

The rxvt-unicode developers removed compatibility code for a lot of non standard wallpaper setters with this update. Using a non compatible wallpaper setter will break transparency support. Recommended wallpaper setters:

*   [feh](/index.php/Feh "Feh")
*   hsetroot
*   esetroot

To make true transparency work, make sure to comment URxvt.tintColor and URxvt.inheritPixmap.

### Remote hosts

If you are logging into a remote host, you may encounter problems when running text-mode programs under rxvt-unicode. This can be fixed by installing [rxvt-unicode-terminfo](https://www.archlinux.org/packages/?name=rxvt-unicode-terminfo) on the remote host or by copying `/usr/share/terminfo/r/rxvt-unicode` from your local machine to your host at `~/.terminfo/r/rxvt-unicode`; same for rxvt-unicode-256color.

Some remote systems do not change title automatically unless you specify TERM=xterm. To fix the issue add this line to .bashrc on the remote machine:

```
PROMPT_COMMAND='echo -ne "\033]0;${USER}@${HOSTNAME}:${PWD}\007"'

```

### Using rxvt-unicode as gmrun terminal

Unlike some other terminals, urxvt expects the arguments to `-e` to be given separately, rather than grouped together with quotes. This causes trouble with gmrun, which assumes the opposite behavior. This can be worked around by putting an "eval" in front of gmrun's "Terminal" variable in `.gmrunrc`:

```
Terminal = eval urxvt
TermExec = ${Terminal} -e

```

(gmrun uses `/bin/sh` to execute commands, so the "eval" is understood here.) The "eval" has the side-effect of "breaking up" the argument to `-e` in the same way that `$@` does in [Bash](/index.php/Bash "Bash"), making the command intelligible to urxvt.

### My numerical keypad acts weird and generates differing output? (e.g. in vim)

Some Debian GNU/Linux users seem to have this problem, although no specific details were reported so far. It is possible that this is caused by the wrong TERM setting, although the details of whether and how this can happen are unknown, as TERM=rxvt should offer a compatible keymap. See the answer to the previous question, and please report if that helped.

However, using the _xmodmap_ program ([xorg-xmodmap](https://www.archlinux.org/packages/?name=xorg-xmodmap)), you can re-map your number pad keys back.

1\. Check the keycode that your numerical keypad (numpad) generates using `xev` program.

*   Start the `xev` program
*   Press your number pad keys and look for _... keycode xxx ..._ in `xev`'s output. For example, numpad 1 in my keyboard is also "End" key, that have a '**keycode 87'**.

2\. Create or modify your xmodmap file, usually `~/.Xmodmap`, with the content representing your keycode.

Example of xmodmap file with number pad keycode:

```
keycode 63 = KP_Multiply
keycode 79 = Home KP_7
keycode 80 = Up KP_8
keycode 81 = Prior KP_9
keycode 82 = KP_Subtract
keycode 83 = Left KP_4
keycode 84 = KP_5
keycode 85 = Right KP_6
keycode 86 = KP_Add
keycode 87 = End KP_1
keycode 88 = Down KP_2
keycode 89 = Next KP_3
keycode 90 = Insert KP_0
keycode 91 = Delete KP_Decimal
keycode 112 = Prior
keycode 117 = Next
```

3\. Load your xmodmap file at X session start-up.

For example, in `~/.xinitrc` file add:

```
...
xmodmap ~/.Xmodmap
...

```

### Pseudo-tty

The following error is likely caused by `/dev/pts` having been mounted with the wrong options.

```
urxvt: cannot initialize pseudo-tty, aborting.

```

Remove `/dev/pts` from `/etc/fstab` and fix the current mount options with:

```
sudo mount -o remount,gid=5,mode=620 /dev/pts

```

See also [[8]](https://mailman.archlinux.org/pipermail/arch-dev-public/2013-August/025332.html), [FS#36548](https://bugs.archlinux.org/task/36548), and [[9]](https://bbs.archlinux.org/viewtopic.php?pid=1318127).

### Key combinations do not work

See [Get Alt key to work in terminal](http://vim.wikia.com/wiki/Get_Alt_key_to_work_in_terminal?useskin=monobook).

### Slow performance when drawing glyphs

Some programs like alsamixer and xprop do not perform well with some graphics drivers and in consequence redraw very slowly. The option "skipBuiltinGlyphs" for `~/.Xresources` or the command line option `-sbg` may fix this. One possible solution is to add the following to `~/.Xresources`:

```
URxvt*skipBuiltinGlyphs:    true

```

## External resources

*   [rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html) - Official site
*   [Source Code](http://cvs.schmorp.de/rxvt-unicode/) - Browseable CVS
*   [rxvt-unicode FAQ](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod) - Official FAQ
*   [rxvt-unicode Reference](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod) - Official manual page
*   [urxvtperl](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/src/urxvt.pm) - Official Perl extension reference

Retrieved from "[https://wiki.archlinux.org/index.php?title=Rxvt-unicode&oldid=412689](https://wiki.archlinux.org/index.php?title=Rxvt-unicode&oldid=412689)"