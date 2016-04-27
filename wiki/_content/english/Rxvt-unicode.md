[rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html) is a customizable [terminal emulator](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator") forked from [rxvt](https://en.wikipedia.org/wiki/Rxvt "wikipedia:Rxvt"). Features of rxvt-unicode include international language support through [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode"), the ability to display multiple font types and support for [Perl](https://en.wikipedia.org/wiki/Perl "wikipedia:Perl") extensions.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Xresources](#Xresources)
    *   [2.2 Scrollback position](#Scrollback_position)
    *   [2.3 Scrollback buffer in secondary screen](#Scrollback_buffer_in_secondary_screen)
    *   [2.4 Font declaration methods](#Font_declaration_methods)
    *   [2.5 Font spacing](#Font_spacing)
    *   [2.6 Colors](#Colors)
*   [3 Cut and paste](#Cut_and_paste)
*   [4 Perl extensions](#Perl_extensions)
    *   [4.1 Clickable URLs](#Clickable_URLs)
    *   [4.2 Yankable URLs (no mouse)](#Yankable_URLs_.28no_mouse.29)
    *   [4.3 Simple tabs](#Simple_tabs)
    *   [4.4 Fullscreen](#Fullscreen)
    *   [4.5 Changing font size on the fly](#Changing_font_size_on_the_fly)
    *   [4.6 Disabling Perl extensions](#Disabling_Perl_extensions)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Transparency not working after upgrade to v9.09](#Transparency_not_working_after_upgrade_to_v9.09)
    *   [5.2 Remote hosts](#Remote_hosts)
    *   [5.3 Using rxvt-unicode as gmrun terminal](#Using_rxvt-unicode_as_gmrun_terminal)
    *   [5.4 My numerical keypad acts weird and generates differing output? (e.g. in vim)](#My_numerical_keypad_acts_weird_and_generates_differing_output.3F_.28e.g._in_vim.29)
    *   [5.5 Key combinations do not work](#Key_combinations_do_not_work)
    *   [5.6 Slow performance when drawing glyphs](#Slow_performance_when_drawing_glyphs)
    *   [5.7 Very long lines cause slowdown](#Very_long_lines_cause_slowdown)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) package.

## Configuration

See [urxvt(1)](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod) and [urxvt(7)](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod) for available settings and values.

### Xresources

Rxvt-unicode is controlled by command-line arguments or [Xresources](/index.php/Xresources "Xresources"). Command-line arguments override, and take precedence over resource settings See the [X resources](/index.php/X_resources "X resources") article for details.

`urxvt --help` prints all available *rxvt* resources to standard error. The man page has full explanations of each resource.

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

When you scroll a pager in a *secondary screen* (e.g. `less` without the `**-X**` option), it may be a good idea to disable the scrollback buffer to be able to scroll in the pager *itself*, instead of the terminal's buffer: this is default and unchangeable behaviour in konsole and vte-based terminals.

In urxvt, to disable the scrollback buffer for the *secondary screen*:

```
URxvt.secondaryScreen: 1
URxvt.secondaryScroll: 0

```

The above configuration works as expected except when scrolling with a mouse wheel. When you scroll a pager in the *secondary screen* with the mouse wheel - and there has been something in the scrollback buffer, instead of the pager itself - the scrollback buffer will be scrolled by the mouse wheel. To solve this issue, it is necessary to introduce a new option into rxvt-unicode [[1]](https://bbs.archlinux.org/viewtopic.php?id=132150). A patched rxvt-unicode is available in AUR as [rxvt-unicode-better-wheel-scrolling](https://aur.archlinux.org/packages/rxvt-unicode-better-wheel-scrolling/). After installing it, add the following to the configuration file:

```
URxvt.secondaryWheel: 1

```

**Note:** Avoid using this option with the [urxvt-vtwheel](https://aur.archlinux.org/packages/urxvt-vtwheel/) perl extension, as it will conflict.

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

### Font spacing

By default the distance between characters can feel too wide. The spacing can be reduced by one pixel as such:

 `~/.Xresources` 
```
URxvt.letterSpace: -1

```

There is some debate [[2]](http://lists.schmorp.de/pipermail/rxvt-unicode/2007q4/000511.html)[[3]](http://lists.schmorp.de/pipermail/rxvt-unicode/2007q4/000512.html) over how *urxvt* calculates character widths. [rxvt-unicode-patched](https://aur.archlinux.org/packages/rxvt-unicode-patched/) changes this calculation, usually resulting in tighter character spacing.

### Colors

By default, rxvt-unicode is compiled with color support. In addition to the default foreground and background colors, rxvt can display up to 256 colors (plus high-intensity bold/blinking/underlined and any mix of these).

It is also possible to specify the color values of foreground, background, cursorColor, cursorColor2, colorBD, colorUL as a number 0-15, as a convenient shorthand to reference the color name of color0-color15\. See [#Xresources](#Xresources) for details.

**Note:** By default `urxvt` uses the same colors as [Xterm](/index.php/Xterm "Xterm"), except one. Add `URxvt.color12: rgb:5c/5c/ff` to Xresources to change this.

## Cut and paste

Rxvt-unicode uses cut buffers which are loaded into the current `PRIMARY` selection by default. See [Selecting and pasting text](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod#THE_SELECTION_SELECTING_AND_PASTING_) for details.

**Note:** Text can be selected to `CLIPBOARD` with the `selection-to-clipboard` [perl extension](#Perl_extensions) available since [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) 9.20.

See also [Clipboard#List of clipboard managers](/index.php/Clipboard#List_of_clipboard_managers "Clipboard")

## Perl extensions

We can enable URxvt perl extensions by including the following line:

```
 URxvt.perl-ext-common: extension_name_1,extension_name_2,...

```

Please take note that there **should not** be any spacing between extension names.

### Clickable URLs

You can make URLs in the terminal clickable using the matcher extension. For example, to open links in the default web browser with the left mouse button, add the following to `.Xresources`:

```
URxvt.perl-ext-common: default,matcher
URxvt.url-launcher: /usr/bin/xdg-open
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

### Fullscreen

You can install the [AUR](/index.php/AUR "AUR") package [urxvt-fullscreen](https://aur.archlinux.org/packages/urxvt-fullscreen/), and then set a key binding to put urxvt fullscreen.

 `~/.Xresources` 
```
...
URxvt.perl-ext-common: ...,fullscreen,...
URxvt.keysym.F11: perl:fullscreen:switch
...

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

## Troubleshooting

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

However, using the *xmodmap* program ([xorg-xmodmap](https://www.archlinux.org/packages/?name=xorg-xmodmap)), you can re-map your number pad keys back.

1\. Check the keycode that your numerical keypad (numpad) generates using `xev` program.

*   Start the `xev` program
*   Press your number pad keys and look for *... keycode xxx ...* in `xev`'s output. For example, numpad 1 in my keyboard is also "End" key, that have a '**keycode 87'**.

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

### Key combinations do not work

See [Get Alt key to work in terminal](http://vim.wikia.com/wiki/Get_Alt_key_to_work_in_terminal?useskin=monobook).

### Slow performance when drawing glyphs

Some programs like alsamixer and xprop do not perform well with some graphics drivers and in consequence redraw very slowly. The option "skipBuiltinGlyphs" for `~/.Xresources` or the command line option `-sbg` may fix this. One possible solution is to add the following to `~/.Xresources`:

```
URxvt*skipBuiltinGlyphs:    true

```

### Very long lines cause slowdown

The `matcher` plugin may be the culprit here. It must match a regex against a line every time the line updates, and if you have a large `saveLines` value this can exacerbate the problem by allowing a very large maximum line length.

There are some simple workarounds:

*   Reduce `saveLines`
*   Disable the `matcher` plugin

If neither of those are palatable options, you can compromise by disabling URL matching past a certain cutoff point:

1.  Copy `/usr/lib/urxvt/perl/matcher` to `~/.urxvt/ext/` (creating the directory if necessary)
2.  Edit `~/.urxvt/ext/matcher`, and find the `my ($self, $row) = @_;` line in the `on_line_update` sub. It should be line 270.
3.  After that line, insert the line `return () if $row < -100;`. This disables URL matching on any line that starts more than 100 rows behind the top of the terminal.

## See also

*   [rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html) - Official site
*   [Source Code](http://cvs.schmorp.de/rxvt-unicode/) - Browseable CVS
*   [rxvt-unicode FAQ](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod) - Official FAQ
*   [rxvt-unicode Reference](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod) - Official manual page
*   [urxvtperl](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/src/urxvt.pm) - Official Perl extension reference