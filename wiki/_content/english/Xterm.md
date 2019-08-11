**xterm** is the standard [terminal emulator](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator") for the [X Window System](/index.php/X_Window_System "X Window System"). It is highly configurable and has many useful and some unusual features.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Resource file settings](#Resource_file_settings)
        *   [2.1.1 TERM Environmental Variable](#TERM_Environmental_Variable)
        *   [2.1.2 UTF-8](#UTF-8)
        *   [2.1.3 Make 'Alt' key behave as on other terminal emulators](#Make_'Alt'_key_behave_as_on_other_terminal_emulators)
        *   [2.1.4 Fix the backspace key](#Fix_the_backspace_key)
        *   [2.1.5 Key binding](#Key_binding)
    *   [2.2 Scrolling](#Scrolling)
        *   [2.2.1 Scrollbar](#Scrollbar)
    *   [2.3 Menus](#Menus)
        *   [2.3.1 Main Options menu](#Main_Options_menu)
        *   [2.3.2 VT Options menu](#VT_Options_menu)
        *   [2.3.3 VT Fonts menu](#VT_Fonts_menu)
        *   [2.3.4 Tek Options menu](#Tek_Options_menu)
    *   [2.4 Copy and paste](#Copy_and_paste)
        *   [2.4.1 PRIMARY or CLIPBOARD](#PRIMARY_or_CLIPBOARD)
        *   [2.4.2 PRIMARY and CLIPBOARD](#PRIMARY_and_CLIPBOARD)
        *   [2.4.3 Selecting text](#Selecting_text)
*   [3 Colors](#Colors)
*   [4 Fonts](#Fonts)
    *   [4.1 Default fonts](#Default_fonts)
    *   [4.2 Bold and underlined fonts](#Bold_and_underlined_fonts)
    *   [4.3 CJK Fonts](#CJK_Fonts)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Automatic transparency](#Automatic_transparency)
    *   [5.2 Enable bell urgency](#Enable_bell_urgency)
    *   [5.3 Font tips](#Font_tips)
        *   [5.3.1 Use color in place of bold and italics](#Use_color_in_place_of_bold_and_italics)
        *   [5.3.2 Adjust line spacing](#Adjust_line_spacing)
    *   [5.4 Tek 4014 demonstration](#Tek_4014_demonstration)
    *   [5.5 Protect against X11 input snooping](#Protect_against_X11_input_snooping)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Flickering on scroll](#Flickering_on_scroll)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [xterm](https://www.archlinux.org/packages/?name=xterm) package.

## Configuration

### Resource file settings

There are several options you can set in your [X resources](/index.php/X_resources "X resources") files that may make this terminal emulator much nicer to use. See [xterm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xterm.1)for a complete list.

#### TERM Environmental Variable

Allow xterm to report the TERM variable correctly. **Do not** set the TERM variable from your *~/.bashrc* or *~/.bash_profile* or similar file. The terminal itself should report the correct TERM to the system so that the proper *terminfo* file will be used. Two usable terminfo names are *xterm* and *xterm-256color*. To set the name, use the resource

```
XTerm.termName: xterm-256color

```

You can check the result within xterm using either of these commands:

```
$ echo $TERM
$ tset -q

```

#### UTF-8

Ensure that your [locale](/index.php/Locale "Locale") is set up for UTF-8\. If you do not use UTF-8, you may need to force xterm to more strictly follow your locale by setting

```
XTerm.vt100.locale: true

```

#### Make 'Alt' key behave as on other terminal emulators

The default `Alt` key behavior in xterm is a modifier to send eight bit input characters e.g. to insert `æ` by pressing `Alt+f`. To make `Alt` instead send a `^[` (escape) key (as in gnome-terminal and konsole), set

```
XTerm.vt100.metaSendsEscape: true

```

#### Fix the backspace key

On Arch Linux, xterm sends `^H` key when backspace is pressed. This breaks the `Ctrl+H` key combination on [Emacs](/index.php/Emacs "Emacs"). The workaround is to send `^?` when backspace is pressed by setting the resources

```
XTerm.vt100.backarrowKey: false
XTerm.ttyModes: erase ^?

```

#### Key binding

xterm defines a whole suite of "actions" for manipulating the terminal e.g. `copy-selection()`, `hard-reset()`, `scroll-back()`, etc. These actions can be mapped to mouse/key combinations using the `translations` resource. For example, you can map `Ctrl+M` and `Ctrl+R` to maximize/restore the window:

```
XTerm.vt100.translations: #override 
\
    Ctrl <Key>M: maximize() 
\
    Ctrl <Key>R: restore()

```

`#override` indicates that these bindings should override any existing ones (you almost always want this for custom key bindings). Each binding must be separated by the escape sequence `
`. If you want to insert a literal newline, it also needs to be escaped (hence `
\`). See the **KEY BINDINGS** section of [xterm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xterm.1)for the full list of actions and many examples.

**Tip:** You can also have separate sets of keybindings that you switch between. See the `keymap()` action in the man page.

### Scrolling

As new lines are written to the bottom of the xterm window, older lines disappear from the top. To scroll up and down through the off-screen lines one can use the mouse wheel, the key combinations `Shift+PageUp` and `Shift+PageDown`, or the scrollbar.

By default, 1024 lines are saved. You can change the number of saved lines with the `saveLines` resource,

```
XTerm.vt100.saveLines: 4096

```

Other X resources that affect scrolling are `jumpScroll`, `multiScroll`, and `fastScroll` (all under `XTerm.vt100`, see [xterm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xterm.1)). To scroll inside an [#alternate screen](#VT_Options_menu), set `alternateScroll` to `true`.

#### Scrollbar

The scrollbar is not shown by default. It can be enabled and its appearance tweaked through resource settings (note the differing capitalization of "scrollbar"!)

```
XTerm.vt100.scrollBar: true
XTerm.vt100.scrollbar.width: 8

```

See [xterm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xterm.1)for other scrollbar resources.

The scrollbar operates differently from what you may be accustomed to using.

*   To scroll down:

	– Click on the scrollbar with the left mouse button, or

	– Click on the scrollbar below the thumb with the middle mouse button.

*   To scroll up:

	– Click on the scrollbar with the right mouse button, or

	– Click on the scrollbar above the thumb with the middle mouse button.

*   To position text, moving in either direction:

	– Grab the thumb and use "click-and-drag" with the middle mouse button.

### Menus

[xterm](https://www.archlinux.org/packages/?name=xterm) is compiled with the *toolbar,* or *menubar,* disabled. The menus are still available as *popups* when you press `Ctrl+MouseButton` within the xterm window. The actions invoked by the menu items can often be accomplished using command line options or by setting resource values.

**Tip:** If the popup menu windows show only as small boxes, it is probably because you have a line similar to this, `XTerm*geometry: 80x32`, in your resources file. This *does* start xterm in an 80 column by 32 row main window, but it also forces the menu windows to be 80 pixels by 32 pixels! This is why you should fully specify the resource: `XTerm.vt100.geometry: 80x32` 

Some of the menu options are discussed below.

#### Main Options menu

***Ctrl + LeftMouse***

*   `Secure Keyboard` attempts to ensure only the xterm window, and no other application, receives your keystrokes. The display changes to reverse video when it is invoked. If the display is not in reverse video, the *Secure Keyboard* mode is not in effect. Please read the "SECURITY" section of the xterm man page for this option's limitations.

*   `Allow SendEvents` allows other processes to send keypress and mouse events to the xterm window. Because of the security risk, do not enable this unless you are very sure you know what you are doing.

*   `Log to File` – The log file will be named `Xterm.log.hostname.yyyy.mm.dd.hh.mm.ss.XXXXXX`. This file will contain all the printed output *and all cursor movements.* Logging may be a security risk.

*   The six `Send *** Signal` menu items are not often useful, except when your keyboard fails. `HUP`, `TERM` and `KILL` will close the xterm window. `KILL` should be avoided, as it does not allow any cleanup code to run.

*   The `Quit` menu item will also close the xterm window – it is the same as sending a `HUP` signal. Most users will use the keyboard combination `Ctrl+d` or will type `exit` to close an xterm instance.

#### VT Options menu

***Ctrl + MiddleMouse***

*   `Select to Clipboard` – Normally, selected text is stored in PRIMARY, to be pasted with `Shift+Insert` or by using the middle mouse button. By toggling this option to *on,* selected text will use CLIPBOARD, allowing you to paste the text selected in an xterm window into a GUI application using `Ctrl+v`. The corresponding resource is `XTerm.vt100.selectToClipboard`.

*   `Show Alternate Screen` – When you use an a terminal application such as *vim,* or *less,* the alternate screen is opened. The main VT window, now hidden, remains in memory. You can view this main window, but not issue any commands in it, by toggling this menu option. You are able to select and copy text from this main window.

**Tip:** Suspending the process running in the Alternate Screen and then resuming it provides more functionality than using `Show Alternate Screen`. With a *bash* shell, pressing `Ctrl+z` suspends the process; issuing the command `fg` then resumes it.

*   `Show Tek Window` and `Switch to Tek Mode` – The [Tektronix 4014](https://en.wikipedia.org/wiki/Tektronix_4010 "wikipedia:Tektronix 4010") was a graphics terminal from the 1970s used for CAD and plotting applications. The command line program `graph`, from [plotutils](https://www.archlinux.org/packages/?name=plotutils), and the application [gnuplot](https://www.archlinux.org/packages/?name=gnuplot) can be made to use xterm's Tek emulation; most people will prefer more modern display options for charting data. See the [#Tek 4014 demonstration](#Tek_4014_demonstration), below.

#### VT Fonts menu

***Ctrl + RightMouse***

*   When using XLFD fonts, the first seven menu items will change the font face and the font size used in the current xterm window. If you are using an Xft font, only the font size will change, the font face will not change with the different selections, .

**Tip:** `Unreadable` and `Tiny` are useful if you wish to keep an eye on a process but do not want to devote a large amount of screen space to the terminal window. An example use might be a lengthy compilation process when you only want to see that the operation completes.

*   `Selection`, when using XLFD font names, allows you to switch to the font name stored in the PRIMARY selection (or CLIPBOARD).

#### Tek Options menu

From the **Tek Window,** ***Ctrl + MiddleMouse***

The first section's options allow you to change the Tek window font size. The second set of options are used to move the focus between the Tek emulation window and the main, or *VT,* window and to close or hide the Tek window.

### Copy and paste

First, highlighting text using the mouse in an xterm (or alternatively another application) will select the text to copy, then clicking the mouse middle-button will paste that highlighted text. Also the key combination `Shift+Insert` will paste highlighted text, but only within an xterm.

#### PRIMARY or CLIPBOARD

By default, xterm, and many other applications running under X, copy highlighted text into a buffer called the [PRIMARY](/index.php/Clipboard "Clipboard") selection. The PRIMARY selection is short-lived; the text is immediately replaced by a new PRIMARY selection as soon as another piece of text is highlighted. Some applications will allow you to paste PRIMARY selections by using the middle-mouse, but not `Shift+Insert`, and some other applications may not allow pasting from PRIMARY entirely.

There is another buffer used for copied text called the CLIPBOARD selection. The text in the CLIPBOARD is long-lived, remaining available until a user actively overwrites it. Applications that use `Ctrl+c` and `Ctrl+x` for text copying and cutting operations, and `Ctrl+v` for pasting, are using the CLIPBOARD.

The fleeting nature of the PRIMARY selection, where copied text is lost as soon as another selection is highlighted, annoys some users. xterm allows the user to switch between the use of PRIMARY and CLIPBOARD using `Select to Clipboard` on the [#VT Options menu](#VT_Options_menu) or with the `XTerm.vt100.selectToClipboard` resource.

#### PRIMARY and CLIPBOARD

With the above setting you can select if you want to use PRIMARY or CLIPBOARD, but you can also hack it to add the selection to both. Just override the [#Key binding](#Key_binding) for releasing the left mouse button:

**Warning:** As of xterm-336, this method no longer works reliably - see [https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=901249#35](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=901249#35)

```
<Btn1Up>: select-end(PRIMARY, CLIPBOARD, CUT_BUFFER0)

```

You can add [#Key bindings](#Key_binding) similar to other terminals' copy/paste behavior (such as gnome terminal):

```
Ctrl Shift <Key>C: copy-selection(CLIPBOARD) 
\
Ctrl Shift <Key>V: insert-selection(CLIPBOARD)

```

#### Selecting text

The new user usually discovers that text may be selected using a "click-and-drag" with the left mouse button. Double-clicking will select a word, where a word is defined as consecutive alphabetic characters plus the underscore, or the Basic Regular Expression (BRE) `[A-Za-z_]`. Triple-clicking selects a line, with a "tab" character usually copied as multiple "space" characters.

Another way of selecting text, especially useful when copying more than one full screen, is:

1.  Left-click at the start of the intended selection.
2.  Scroll to where the end of the selection is visible.
3.  Right-click at the end of the selection.

You do not have to be precise immediately with the right-click – any highlighted selection may be extended or shortened by using a right-click.

You can clear any selected text by left-clicking once, anywhere within the xterm window.

When a character-based application runs inside xterm, it is allowed to receive mouse events. This may be a problem if the program can not communicate with the X11 clipboard. In order to pass these events to the underlying xterm, they must be accompanied by the `Shift` key. For example, in [links](https://www.archlinux.org/packages/?name=links) (not `xlinks -g`), one can mouse-click on URLs and menu items, but not select or paste with a middle button. To do copy-paste, press the `Shift` key and then perform mouse clicks (the key needs to be pressed only during the click, so there is no need to hold it when dragging mouse to select, for instance, a text block).

## Colors

xterm defaults to black text, the *foreground* color, on a white *background.* The foreground and background colors can be reversed by setting the resource

```
XTerm.vt100.reverseVideo: true

```

Alternatively, you can directly change the foreground and background colors (as well as the first sixteen terminal colors) using resources:

```
XTerm.vt100.foreground: white
XTerm.vt100.background: black
XTerm.vt100.color0: rgb:28/28/28
! ...
XTerm.vt100.color15: rgb:e4/e4/e4

```

**Note:** Colors for applications that use the X libraries may be specified in many different ways.

Some colors can be specified by assigned names. If [emacs](https://www.archlinux.org/packages/?name=emacs) or [vim](https://www.archlinux.org/packages/?name=vim) has been installed, you can examine `/usr/share/emacs/*/etc/rgb.txt` or `/usr/share/vim/*/rgb.txt` to view the list of color names with their decimal RGB values. Colors may also be specified using hexadecimal RGB values with the format `rgb:RR/GG/BB`, or the older and not encouraged syntax `#RRGGBB`.

The color `PapayaWhip` is the same as `rgb:ff/ef/d5`, which is the same as `#ffefd5`.

See [X(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/X.7) from [xorg-docs](https://www.archlinux.org/packages/?name=xorg-docs), for a more complete description of color syntax.

Many suggestions for color schemes can be viewed in the forum thread, [Terminal Colour Scheme Screenshots](https://bbs.archlinux.org/viewtopic.php?id=51818&p=1).

**Tip:** Many people specify colors in their X resources files without specifying an application class or application instance:
```
*foreground: rgb:b2/b2/b2
*background: rgb:08/08/08

```
The above example sets the foreground and background color values for all *Xlib* applications (xclock, xfontsel, and others) that use these resources. This is a nice, easy way to achieve a unified color scheme.

## Fonts

### Default fonts

xterm's default font is the bitmap font named by the [X Logical Font Description](/index.php/X_Logical_Font_Description "X Logical Font Description") alias `fixed`, often resolving to

```
-misc-fixed-medium-r-semicondensed--13-120-75-75-c-60-iso8859-?

```

This font, also aliased to the name `6x13`, has remakably wide coverage for unicode glyphs. The default "TrueType" font is the 14‑point font matched by the name `mono`. The *FreeType* font that will be used can be found with this command:

```
$ fc-match mono

```

Fonts can be specified in your resources, depending on whether the font is TrueType or not:

```
XTerm.vt100.faceName: Liberation Mono:size=10:antialias=false
XTerm.vt100.font: 7x13

```

To test, you can also set the font on the command line: `-fa` for `faceName`, `-fn` for `font`. If you set both kinds of fonts, you can alternate between the two by toggling `TrueType Fonts` from the [#VT Fonts menu](#VT_Fonts_menu). You can also choose the default with the following resource

```
! start with TrueType fonts disabled
XTerm.vt100.renderFont: false

```

### Bold and underlined fonts

Italic fonts are shown as underlined characters when using XLFD names in xterm. TrueType fonts should use an oblique typeface.

If you do not specify a bold font at the command line, `-fb`, or through the `XTerm.vt100.boldFont` resource, xterm will attempt to find a bold font matching the normal font. If a matching font is not found, the bold font will be created by "overstriking" the normal font.

### CJK Fonts

Many fonts do not contain glyphs for the double width Chinese, Japanese and Korean languages. Other terminal emulators such as [urxvt](/index.php/Urxvt "Urxvt") may be better suited if you frequently work with these languages.

Using bitmapped XLFD fonts with CJK has many pitfalls in xterm. It is much easier to use TrueType fonts for CJK display, using the `faceNameDoublesize` resource. This example uses *DejaVu Sans Mono* as the normal font and *WenQuanYi WenQuanYi Bitmap Song* as the double width font:

```
XTerm.vt100.faceName: DejaVu Sans Mono:style=Book:antialias=false
XTerm.vt100.faceNameDoublesize: WenQuanYi WenQuanYi Bitmap Song
XTerm.vt100.faceSize: 8

```

## Tips and tricks

### Automatic transparency

Install the package [transset-df](https://www.archlinux.org/packages/?name=transset-df) and a [composite manager](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager") such as [Xcompmgr](/index.php/Xcompmgr "Xcompmgr"). Then add the following line to your `~/.bashrc`:

```
[ -n "$XTERM_VERSION" ] && transset-df --id "$WINDOWID" >/dev/null

```

Now, each time you launch a shell in an xterm and a composite manager is running, the xterm window will be transparent. The test in front of `transset-df` keeps transet from executing if `XTERM_VERSION` is not defined. Note that your terminal will not be transparent if you launch a program other than a shell this way. It is probably possible to work around this if you want the functionality.

Also see [Per-application transparency](/index.php/Per-application_transparency "Per-application transparency").

### Enable bell urgency

To make the bell character notify the window manager of urgency, set:

```
XTerm.vt100.bellIsUrgent: true

```

### Font tips

#### Use color in place of bold and italics

When using small font sizes, bold or italic characters may be difficult to read. One solution is to turn off bolding and underlining or italics and use color instead. This example does just that:

```
! disable bold font faces, instead make text light blue.
XTerm.vt100.colorBDMode: true
XTerm.vt100.colorBD: rgb:82/a4/d3
! disable underlined text, instead make it white.
XTerm.vt100.colorULMode: true
XTerm.vt100.colorUL: rgb:e4/e4/e4
! similarly use colorIT for italics

```

See [#Colors](#Colors) for formatting information.

#### Adjust line spacing

Lines of text can sometimes be too close together, or they may appear to be too widely spaced. For one example, using *DejaVu Sans Mono,* the low underscore glyph may butt against CJK glyphs or the cursor block in the line below. Line spacing, called *leading* by typographers, can be adjusted with the following resource, for example to widen the spacing:

```
XTerm.scaleHeight: 1.01

```

Valid values for range from `0.9` to `1.5`, with `1.0` being the default.

### Tek 4014 demonstration

If you have [plotutils](https://www.archlinux.org/packages/?name=plotutils) installed, you can use xterm's Tektronix 4014 emulation to view some of the plotutils package's test files. Open the Tek window from the [#VT Options menu](#VT_Options_menu) menu item `Switch to Tek Mode` or start a new xterm instance using this command:

```
$ xterm -t -tn tek4014

```

Your PS1 prompt will not render correctly, if it appears at all. In the new window, enter the command,

```
cat /usr/share/tek2plot/dmerc.tek

```

A world map will appear in the Tek window. You can also view other `*.tek` files from that same directory. To close the Tek window, one can use the xterm menus.

### Protect against X11 input snooping

It can be inconvenient to activate **Secure Keyboard** mode from the [#Main Options menu](#Main_Options_menu). You can instead invoke the `secure()` action with a [#Key binding](#Key_binding):

```
Ctrl Alt <Key>S: secure()

```

## Troubleshooting

### Flickering on scroll

**Warning:** Double buffering may cause non-bitmap fonts to render incorrectly.

Rebuild xterm using [ABS](/index.php/ABS "ABS") and include the `--enable-double-buffer` flag:

```
./configure --prefix=/usr \
     ...
     --with-utempter \
     --enable-double-buffer

```

See [Xterm modifications](https://bbs.archlinux.org/viewtopic.php?id=146023) for details.

## See also

*   [Hidden gems of Xterm](http://lukas.zapletalovi.com/2013/07/hidden-gems-of-xterm.html)
*   [Commented XTerm resources](http://www.in-ulm.de/~mascheck/X11/XTerm)
*   [XTerm introduction and TrueType fonts configuration](http://www.futurile.net/2016/06/14/xterm-setup-and-truetype-font-configuration/)