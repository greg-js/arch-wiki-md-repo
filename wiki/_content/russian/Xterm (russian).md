**Состояние перевода:** На этой странице представлен перевод статьи [Xterm](/index.php/Xterm "Xterm"). Дата последней синхронизации: 12 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Xterm&diff=0&oldid=425206).

**xterm** это стандартный [эмулятор терминала](https://en.wikipedia.org/wiki/%D0%AD%D0%BC%D1%83%D0%BB%D1%8F%D1%82%D0%BE%D1%80_%D1%82%D0%B5%D1%80%D0%BC%D0%B8%D0%BD%D0%B0%D0%BB%D0%B0 "wikipedia:Эмулятор терминала") для [системы окон X](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)"). Он широко настраиваемый и имеет много полезных и необычных черт.

## Contents

*   [1 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [1.1 Настройка файла ресурсов](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.D1.80.D0.B5.D1.81.D1.83.D1.80.D1.81.D0.BE.D0.B2)
        *   [1.1.1 Переменная окружения TERM](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D0.B0.D1.8F_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_TERM)
        *   [1.1.2 UTF-8](#UTF-8)
        *   [1.1.3 Исправление клавиши 'Alt'](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.27Alt.27)
    *   [1.2 Прокрутка](#.D0.9F.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B0)
        *   [1.2.1 Полоса прокрутки](#.D0.9F.D0.BE.D0.BB.D0.BE.D1.81.D0.B0_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B8)
    *   [1.3 Меню](#.D0.9C.D0.B5.D0.BD.D1.8E)
        *   [1.3.1 Главные опции меню](#.D0.93.D0.BB.D0.B0.D0.B2.D0.BD.D1.8B.D0.B5_.D0.BE.D0.BF.D1.86.D0.B8.D0.B8_.D0.BC.D0.B5.D0.BD.D1.8E)
        *   [1.3.2 Опции меню VT](#.D0.9E.D0.BF.D1.86.D0.B8.D0.B8_.D0.BC.D0.B5.D0.BD.D1.8E_VT)
        *   [1.3.3 Шрифты меню VT](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B_.D0.BC.D0.B5.D0.BD.D1.8E_VT)
        *   [1.3.4 Опции меню Tek](#.D0.9E.D0.BF.D1.86.D0.B8.D0.B8_.D0.BC.D0.B5.D0.BD.D1.8E_Tek)
    *   [1.4 Копирование и вставка](#.D0.9A.D0.BE.D0.BF.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B8_.D0.B2.D1.81.D1.82.D0.B0.D0.B2.D0.BA.D0.B0)
        *   [1.4.1 PRIMARY или CLIPBOARD](#PRIMARY_.D0.B8.D0.BB.D0.B8_CLIPBOARD)
        *   [1.4.2 PRIMARY и CLIPBOARD](#PRIMARY_.D0.B8_CLIPBOARD)
        *   [1.4.3 Выбор текста](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D1.82.D0.B5.D0.BA.D1.81.D1.82.D0.B0)
*   [2 Цвета](#.D0.A6.D0.B2.D0.B5.D1.82.D0.B0)
*   [3 Шрифты](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B)
    *   [3.1 Стандартные шрифты](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82.D0.BD.D1.8B.D0.B5_.D1.88.D1.80.D0.B8.D1.84.D1.82.D1.8B)
    *   [3.2 Жирные и подчеркнутые шрифты](#.D0.96.D0.B8.D1.80.D0.BD.D1.8B.D0.B5_.D0.B8_.D0.BF.D0.BE.D0.B4.D1.87.D0.B5.D1.80.D0.BA.D0.BD.D1.83.D1.82.D1.8B.D0.B5_.D1.88.D1.80.D0.B8.D1.84.D1.82.D1.8B)
    *   [3.3 Шрифты CJK](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B_CJK)
*   [4 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [4.1 Автоматическая прозрачность](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B0.D1.8F_.D0.BF.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
    *   [4.2 Enable bell urgency](#Enable_bell_urgency)
    *   [4.3 Советы по шрифтам](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.BF.D0.BE_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.B0.D0.BC)
        *   [4.3.1 Используйте цвета вместо жирного и курсивного](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B9.D1.82.D0.B5_.D1.86.D0.B2.D0.B5.D1.82.D0.B0_.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.BE_.D0.B6.D0.B8.D1.80.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B8_.D0.BA.D1.83.D1.80.D1.81.D0.B8.D0.B2.D0.BD.D0.BE.D0.B3.D0.BE)
        *   [4.3.2 Отрегулируйте расстояние между строками](#.D0.9E.D1.82.D1.80.D0.B5.D0.B3.D1.83.D0.BB.D0.B8.D1.80.D1.83.D0.B9.D1.82.D0.B5_.D1.80.D0.B0.D1.81.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.B8.D0.B5_.D0.BC.D0.B5.D0.B6.D0.B4.D1.83_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B0.D0.BC.D0.B8)
    *   [4.4 Удалите чёрную границу](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B8.D1.82.D0.B5_.D1.87.D1.91.D1.80.D0.BD.D1.83.D1.8E_.D0.B3.D1.80.D0.B0.D0.BD.D0.B8.D1.86.D1.83)
    *   [4.5 Демонстрация Tek 4014](#.D0.94.D0.B5.D0.BC.D0.BE.D0.BD.D1.81.D1.82.D1.80.D0.B0.D1.86.D0.B8.D1.8F_Tek_4014)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 Мерцание при прокрутке](#.D0.9C.D0.B5.D1.80.D1.86.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B5)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Настройка

### Настройка файла ресурсов

Есть несколько опций, которые вы можете задать в файле [Ресурсы Х](/index.php/%D0%A0%D0%B5%D1%81%D1%83%D1%80%D1%81%D1%8B_%D0%A5 "Ресурсы Х"), они помогут сделать этот эмулятор терминала гораздо проще в использовании. Смотрите полный список `man xterm`.

#### Переменная окружения TERM

Allow xterm to report the **TERM** variable correctly. **Do not** set the TERM variable from your *~/.bashrc* or *~/.bash_profile* or similar file. The terminal itself should report the correct TERM to the system so that the proper *terminfo* file will be used. Two usable terminfo files are *xterm,* and *xterm-256color.*

Without setting TERM explicitly, xterm should report `$TERM` as `xterm`. You can check this from within xterm using either of these commands:

```
$ echo $TERM
$ tset -q

```

When TERM is not set explicitly, color schemes for some programs, such as *vim,* may not appear until a key is pressed or some other input occurs. This can be remedied with this resource setting:

```
xterm*termName: xterm-256color

```

#### UTF-8

Make certain your locale settings are correct for UTF-8\. Adding the following line to your resource file will then make xterm interpret all incoming data as UTF-8 encoded:

```
XTerm*locale: true

```

#### Исправление клавиши 'Alt'

If you use the `Alt` key for keyboard shortcuts, you will need this in your resource file:

```
XTerm*metaSendsEscape: true

```

### Прокрутка

As new lines are written to the bottom of the xterm window, older lines disappear from the top. To scroll up and down through the off-screen lines one can use the mouse wheel, the key combinations `Shift+PageUp` and `Shift+PageDown`, or the scrollbar.

By default, 1024 lines are saved. You can change the number of saved lines with the `saveLines` resource,

```
Xterm*saveLines: 4096

```

Other X resources that affect scrolling are `jumpScroll`, set to `true` by default, and `multiScroll` and `fastScroll`, both of which default to `false`. To scroll inside an [alternate screen](#.D0.9E.D0.BF.D1.86.D0.B8.D0.B8_.D0.BC.D0.B5.D0.BD.D1.8E_VT), set `alternateScroll` to `true`.

#### Полоса прокрутки

The scrollbar is not shown by default. It can be made visible by a menu selection, by command line options, or by setting resource values. It can be made to appear to the left or right of the window and its visual appearance can be modified through resource settings.

The scrollbar operates differently from what you may be accustomed to using.

*   To scroll down:

	– Click on the scrollbar with the left mouse button.

	– Click on the scrollbar below the *thumb* with the middle mouse button.

*   To scroll up:

	– Click on the scrollbar with the right mouse button.

	– Click on the scrollbar above the *thumb* with the middle mouse button.

*   To position text, moving in either direction:

	– Grab the *thumb* and use "click-and-drag" with the middle mouse button.

### Меню

The Archlinux version of xterm is compiled with the *toolbar,* or *menubar,* disabled. The menus are still available as *popups* when you press `Ctrl+MouseButton` within the xterm window. The actions invoked by the menu items can often be accomplished using command line options or by setting resource values.

**Совет:** If the popup menu windows show only as small boxes, it is probably because you have a line similar to this, `xterm*geometry: 80x32`, in your resources file. This *does* start xterm in an 80 column by 32 row main window, but it also forces the menu windows to be 80 pixels by 32 pixels! Replace the incorrect line with this: `xterm*VT100.geometry: 80x32` 

Some of the menu options are discussed below.

#### Главные опции меню

***Ctrl + LeftMouse***

*   `Secure Keyboard` attempts to ensure only the xterm window, and no other application, receives your keystrokes. The display changes to reverse video when it is invoked. If the display is not in reverse video, the *Secure Keyboard* mode is not in effect. Please read the "SECURITY" section of the xterm man page for this option's limitations.

*   `Allow SendEvents` allows other processes to send keypress and mouse events to the xterm window. Because of the security risk, do not enable this unless you are very sure you know what you are doing.

*   `Log to File` – The log file will be named `Xterm.log.hostname.yyyy.mm.dd.hh.mm.ss.XXXXXX`. This file will contain all the printed output *and all cursor movements.* Logging may be a security risk.

*   The six `Send *** Signal` menu items are not often useful, except when your keyboard fails. `HUP`, `TERM` and `KILL` will close the xterm window. `KILL` should be avoided, as it does not allow any cleanup code to run.

*   The `Quit` menu item will also close the xterm window – it is the same as sending a `HUP` signal. Most users will use the keyboard combination `Ctrl+d` or will type `exit` to close an xterm instance.

#### Опции меню VT

***Ctrl + MiddleMouse***

*   `Select to Clipboard` – Normally, selected text is stored in PRIMARY, to be pasted with `Shift+Insert` or by using the middle mouse button. By toggling this option to *on,* selected text will use CLIPBOARD, allowing you to paste the text selected in an xterm window into a GUI application using `Ctrl+v`. The corresponding XTerm resource is `selectToClipboard`.

*   `Show Alternate Screen` – When you use an a terminal application such as *vim,* or *less,* the alternate screen is opened. The main VT window, now hidden, remains in memory. You can view this main window, but not issue any commands in it, by toggling this menu option. You are able to select and copy text from this main window.

**Совет:** Suspending the process running in the Alternate Screen and then resuming it provides more functionality than using `Show Alternate Screen`. With a *bash* shell, pressing `Ctrl+z` suspends the process; issuing the command `fg` then resumes it.

*   `Show Tek Window` and `Switch to Tek Mode` – The [Tektronix 4014](https://en.wikipedia.org/wiki/Tektronix_4010 "wikipedia:Tektronix 4010") was a graphics terminal from the 1970s used for CAD and plotting applications. The command line program `graph`, from [plotutils](https://www.archlinux.org/packages/?name=plotutils), and the application [gnuplot](https://www.archlinux.org/packages/?name=gnuplot) can be made to use xterm's Tek emulation; most people will prefer more modern display options for charting data. See the [#Tek 4014 demonstration](#Tek_4014_demonstration), below.

#### Шрифты меню VT

***Ctrl + RightMouse***

*   When using XLFD fonts, the first seven menu items will change the font face and the font size used in the current xterm window. If you are using an Xft font, only the font size will change, the font face will not change with the different selections, .

**Совет:** `Unreadable` and `Tiny` are useful if you wish to keep an eye on a process but do not want to devote a large amount of screen space to the terminal window. An example use might be a lengthy compilation process when you only want to see that the operation completes.

*   `Selection`, when using XLFD font names, allows you to switch to the font name stored in the PRIMARY selection (or CLIPBOARD).

#### Опции меню Tek

From the **Tek Window,** ***Ctrl + MiddleMouse***

The first section's options allow you to change the Tek window font size. The second set of options are used to move the focus between the Tek emulation window and the main, or *VT,* window and to close or hide the Tek window.

### Копирование и вставка

First, highlighting text using the mouse in an xterm (or alternatively another application) will select the text to copy, then clicking the mouse middle-button will paste that highlighted text. Also the key combination `Shift+Insert` will paste highlighted text, but only within an xterm.

#### PRIMARY или CLIPBOARD

By default, xterm, and many other applications running under X, copy highlighted text into a buffer called the PRIMARY selection. The PRIMARY selection is short-lived; the text is immediately replaced by a new PRIMARY selection as soon as another piece of text is highlighted. Some applications will allow you to paste PRIMARY selections by using the middle-mouse, but not `Shift+Insert`, and some other applications may not allow pasting from PRIMARY entirely.

There is another buffer used for copied text called the CLIPBOARD selection. The text in the CLIPBOARD is long-lived, remaining available until a user actively overwrites it. Applications that use `Ctrl+c` and `Ctrl+x` for text copying and cutting operations, and `Ctrl+v` for pasting, are using the CLIPBOARD.

The fleeting nature of the PRIMARY selection, where copied text is lost as soon as another selection is highlighted, annoys some users. Xterm allows the user to switch between the use of PRIMARY and CLIPBOARD using `Select to Clipboard` on the [#VT Options menu](#VT_Options_menu) or with the `selectToClipboard` resource.

#### PRIMARY и CLIPBOARD

With the above setting you can select if you want to use PRIMARY or CLIPBOARD, but to use both you need a 'hack'. For example, put this in your .Xresources:

```
XTerm*VT100.translations: #override <Btn1Up>: select-end(PRIMARY, CLIPBOARD, CUT_BUFFER0)

```

#### Выбор текста

The new user usually discovers that text may be selected using a "click-and-drag" with the left mouse button. Double-clicking will select a word, where a word is defined as consecutive alphabetic characters plus the underscore, or the Basic Regular Expression (BRE) `[A-Za-z_]`. Triple-clicking selects a line, with a "tab" character usually copied as multiple "space" characters.

Another way of selecting text, especially useful when copying more than one full screen, is:

1.  Left-click at the start of the intended selection.
2.  Scroll to where the end of the selection is visible.
3.  Right-click at the end of the selection.

You do not have to be precise immediately with the right-click – any highlighted selection may be extended or shortened by using a right-click.

You can clear any selected text by left-clicking once, anywhere within the xterm window.

## Цвета

Xterm defaults to black text, the *foreground* color, on a white *background.* The foreground and background colors can be reversed using the [Опции меню VT](#.D0.9E.D0.BF.D1.86.D0.B8.D0.B8_.D0.BC.D0.B5.D0.BD.D1.8E_VT) or with the `-rv` command line option.

```
$ xterm -rv

```

Alternatively, the same thing can be accomplished with the following [Параметры ресурсов X](/index.php/%D0%A0%D0%B5%D1%81%D1%83%D1%80%D1%81%D1%8B_%D0%A5 "Ресурсы Х") (do not forget to [reread the new resource afterwards](/index.php/X_resources#Parsing_.Xresources "X resources")!):

```
XTerm*reverseVideo: on

```

Xterm's foreground color (the text color) and the background color may be set from the command line, using the options `-fg` and `-bg` respectively.

```
xterm -fg PapayaWhip -bg "rgb:00/00/80"

```

The first sixteen terminal colors, as well as the foreground and background colors, may be set from an [Ресурсы Х](/index.php/%D0%A0%D0%B5%D1%81%D1%83%D1%80%D1%81%D1%8B_%D0%A5 "Ресурсы Х") file:

```
XTerm*foreground: rgb:b2/b2/b2
XTerm*background: rgb:08/08/08
XTerm*color0: rgb:28/28/28

! ...Lines omitted...

XTerm*color15: rgb:e4/e4/e4
```

**Примечание:** Colors for applications that use the X libraries may be specified in many different ways.

Some colors can be specified by assigned names. If [emacs](https://www.archlinux.org/packages/?name=emacs) or [vim](https://www.archlinux.org/packages/?name=vim) has been installed, you can examine `/usr/share/emacs/*/etc/rgb.txt` or `/usr/share/vim/*/rgb.txt` to view the list of color names with their decimal RGB values. Colors may also be specified using hexadecimal RGB values with the format `rgb:RR/GG/BB`, or the older and not encouraged syntax `#RRGGBB`.

The color `PapayaWhip` is the same as `rgb:ff/ef/d5`, which is the same as `#ffefd5`.

See **man(7) X,** from [xorg-docs](https://www.archlinux.org/packages/?name=xorg-docs), for a more complete description of color syntax.

Many suggestions for color schemes can be viewed in the forum thread, [Terminal Colour Scheme Screenshots](https://bbs.archlinux.org/viewtopic.php?id=51818&p=1).

**Совет:** Many people specify colors in their X resources files without specifying an application class or application instance:
```
*foreground: rgb:b2/b2/b2
*background: rgb:08/08/08
```
The above example sets the foreground and background color values for all *Xlib* applications (xclock, xfontsel, and others) that use these resources. This is a nice, easy way to achieve a unified color scheme.

## Шрифты

### Стандартные шрифты

Xterm's default font is the bitmap font named by the [X Logical Font Description](/index.php/X_Logical_Font_Description "X Logical Font Description") alias `fixed`, often resolving to

```
-misc-fixed-medium-r-semicondensed--13-120-75-75-c-60-iso8859-?

```

This font, also aliased to the name `6x13`, has remakably wide coverage for unicode glyphs. The default "TrueType" font is the 14‑point font matched by the name `mono`. The *FreeType* font that will be used can be found with this command:

```
$ fc-match mono

```

Fonts can be specified from the command line, with the options `-fn` for bitmap font names and `-fa` for Xft names. The example below allows you to alternate between the two fonts by toggling `TrueType Fonts` from the [#VT Fonts menu](#VT_Fonts_menu).

 `$ xterm -fn 7x13 -fa "Liberation Mono:size=10:antialias=false"` 

For a more permanent change, the default fonts may be set in an [Ресурсы Х](/index.php/%D0%A0%D0%B5%D1%81%D1%83%D1%80%D1%81%D1%8B_%D0%A5 "Ресурсы Х") file:

```
xterm*faceName: Liberation Mono:size=10:antialias=false
xterm*font: 7x13
```

**Примечание:** There is a long-standing bug in xterm that prevents the command line option `-fn` working correctly when `faceName` has been set in a resource file. One solution is to set the resource `renderFont` to `false` on the command line.
```
$ xterm -fn 8x13                             # If this command does not set the font,
$ xterm -fn 8x13 -xrm "*renderFont:false"    # set the 'renderFont' resource to 'false'.
```
Perhaps easier, you can just toggle `TrueType Fonts` from the [#VT Fonts menu](#VT_Fonts_menu) in the terminal window.

### Жирные и подчеркнутые шрифты

Italic fonts are shown as underlined characters when using XLFD names in xterm. TrueType fonts should use an oblique typeface.

If you do not specify a bold font at the command line, `-fb`, or through the `boldFont` resource, xterm will attempt to find a bold font matching the normal font. If a matching font is not found, the bold font will be created by "overstriking" the normal font.

### Шрифты CJK

Many fonts do not contain glyphs for the double width Chinese, Japanese and Korean languages. Other terminal emulators such as [urxvt](/index.php/Urxvt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Urxvt (Русский)") may be better suited if you frequently work with these languages.

Using bitmapped XLFD fonts with CJK has many pitfalls in xterm. It is much easier to use TrueType fonts for CJK display, using the `faceNameDoublesize` resource. This example uses *DejaVu Sans Mono* as the normal font and *WenQuanYi Bitmap Song* as the double width font:

```
xterm*faceName: DejaVu Sans Mono:style=Book:antialias=false
xterm*faceNameDoublesize: WenQuanYi Bitmap Song
xterm*faceSize: 8
```

## Советы и хитрости

### Автоматическая прозрачность

Install the package [transset-df](https://www.archlinux.org/packages/?name=transset-df) and a [Композитный менеджер окон](https://en.wikipedia.org/wiki/%D0%9A%D0%BE%D0%BC%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80_%D0%BE%D0%BA%D0%BE%D0%BD "wikipedia:Композитный менеджер окон") such as [Xcompmgr](/index.php/Xcompmgr "Xcompmgr"). Then add the following line to your `~/.bashrc`:

```
[ -n "$XTERM_VERSION" ] && transset-df -a >/dev/null

```

Now, each time you launch a shell in an xterm and a composite manager is running, the xterm window will be transparent. The test in front of `transset-df` keeps transet from executing if `XTERM_VERSION` is not defined. Note that your terminal will not be transparent if you launch a program other than a shell this way. It is probably possible to work around this if you want the functionality.

Also see [Per-application transparency](/index.php/Per-application_transparency "Per-application transparency").

### Enable bell urgency

Add the following line to your `~/.Xresources` file:

```
xterm*bellIsUrgent: true

```

### Советы по шрифтам

#### Используйте цвета вместо жирного и курсивного

When using small font sizes, bold or italic characters may be difficult to read. One solution is to turn off bolding and underlining or italics and use color instead. This example does just that:

```
! Forbid bold font faces; bold type is light blue.
XTerm*colorBDMode: true
XTerm*colorBD: rgb:82/a4/d3
! Do not underscore text, underlined text is white.
XTerm*colorULMode: true
XTerm*colorUL: rgb:e4/e4/e4
```

#### Отрегулируйте расстояние между строками

Lines of text can sometimes be too close together, or they may appear to be too widely spaced. For one example, using *DejaVu Sans Mono,* the low underscore glyph may butt against CJK glyphs or the cursor block in the line below. Line spacing, called *leading* by typographers, can be adjusted using the `scaleHeight` resource. Here, the line spacing is widened:

```
XTerm*scaleHeight: 1.01

```

Valid values for `scaleHeight` range from `0.9` to `1.5`, with `1.0` being the default.

### Удалите чёрную границу

Xterm has a black border in some cases, you can disable this by adding the following line to your `~/.Xresources` file.

```
xterm*borderWidth: 0

```

### Демонстрация Tek 4014

If you have [plotutils](https://www.archlinux.org/packages/?name=plotutils) installed, you can use xterm's Tektronix 4014 emulation to view some of the plotutils package's test files. Open the Tek window from the [#VT Options menu](#VT_Options_menu) menu item `Switch to Tek Mode` or start a new xterm instance using this command:

```
$ xterm -t -tn tek4014

```

Your PS1 prompt will not render correctly, if it appears at all. In the new window, enter the command,

```
cat /usr/share/tek2plot/dmerc.tek

```

A world map will appear in the Tek window. You can also view other `*.tek` files from that same directory. To close the Tek window, one can use the xterm menus.

## Решение проблем

### Мерцание при прокрутке

**Важно:** Double buffering may cause non-bitmap fonts to render incorrectly.

Rebuild xterm using [ABS](/index.php/ABS "ABS") and include the `--enable-double-buffer` flag:

```
./configure --prefix=/usr \
     ...
     --with-utempter \
     --enable-double-buffer

```

See [Xterm modifications](https://bbs.archlinux.org/viewtopic.php?id=146023) for details.

## Смотрите также

*   [Hidden gems of Xterm](http://lukas.zapletalovi.com/2013/07/hidden-gems-of-xterm.html)
*   [Commented XTerm resources](http://www.in-ulm.de/~mascheck/X11/XTerm)