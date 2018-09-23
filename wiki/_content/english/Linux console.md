Related articles

*   [/Keyboard configuration](/index.php/Linux_console/Keyboard_configuration "Linux console/Keyboard configuration")
*   [Screen capture#Virtual console](/index.php/Screen_capture#Virtual_console "Screen capture")
*   [Color output in console](/index.php/Color_output_in_console "Color output in console")
*   [getty](/index.php/Getty "Getty")

According to [Wikipedia](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console"):

	The **Linux console** is a system console internal to the [Linux kernel](/index.php/Linux_kernel "Linux kernel"). The Linux console provides a way for the kernel and other processes to send text output to the user, and to receive text input from the user. The user typically enters text with a computer keyboard and reads the output text on a computer monitor. The Linux kernel supports virtual consoles - consoles that are logically separate, but which access the same physical keyboard and display.

This article describes the basics of the Linux console and how to configure the font display. Keyboard configuration is described in the [/Keyboard configuration](/index.php/Linux_console/Keyboard_configuration "Linux console/Keyboard configuration") subpage.

## Contents

*   [1 Implementation](#Implementation)
    *   [1.1 Virtual consoles](#Virtual_consoles)
    *   [1.2 Text mode](#Text_mode)
    *   [1.3 Framebuffer console](#Framebuffer_console)
*   [2 Keyboard shortcuts](#Keyboard_shortcuts)
*   [3 Fonts](#Fonts)
    *   [3.1 Preview and temporary changes](#Preview_and_temporary_changes)
    *   [3.2 Persistent configuration](#Persistent_configuration)
*   [4 See also](#See_also)

## Implementation

The console, unlike most services that interact directly with users, is implemented in the kernel. This contrasts with terminal emulation software, such as [Xterm](/index.php/Xterm "Xterm"), which is implemented in user space as a normal application. The console has always been part of released Linux kernels, but has undergone changes in its history, most notably the transition to using the [framebuffer](https://en.wikipedia.org/wiki/Linux_framebuffer "wikipedia:Linux framebuffer") and support for [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode").

Despite many improvements in the console, its full backward compatibility with legacy hardware means it is limited compared to a graphical terminal emulator.

### Virtual consoles

The console is presented to the user as a series of [virtual consoles](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console"). These give the impression that several independent terminals are running concurrently; each virtual console can be logged in with different users, run its own shell and have its own font settings. The virtual consoles each use a device `/dev/ttyX`, and you can switch between them by pressing `Alt+Fx` (where x is equal to the virtual console number, beginning with 1). The device `/dev/console` is automatically mapped to the active virtual console.

See also [chvt(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chvt.1), [openvt(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/openvt.1) and [deallocvt(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/deallocvt.1).

### Text mode

Since Linux originally began as a kernel for PC hardware, the console was developed using standard IBM [CGA/EGA/VGA](https://en.wikipedia.org/wiki/VGA "wikipedia:VGA") graphics, which all PCs supported at the time. The graphics operated in VGA text mode, which provides a simple 80x25 character display with 16 colours. This legacy mode is similar the capabilities of dedicated text terminals, such as the [DEC VT100](https://en.wikipedia.org/wiki/VT100 "wikipedia:VT100") series. It is still possible to boot in text mode if the system hardware supports it, but almost all modern distributions (including Arch Linux) use the framebuffer console instead.

### Framebuffer console

As Linux was ported to other non-PC architectures, a better solution was required, since other architectures do not use VGA-compatible graphics adapters, and may not support text modes at all. The framebuffer console was implemented to provide a standard console across all platforms, and so presents the same VGA-style interface regardless of the underlying graphics hardware. As such, the Linux console is not a terminal emulator, but a terminal in its own right. It uses the terminal type `linux`, and is largely compatible with VT100.

## Keyboard shortcuts

| Keyboard Shortcut | Description |
| `Ctrl+Alt+Del` | Reboots Computer (specified by the symlink `/usr/lib/systemd/system/ctrl-alt-del.target`) |
| `Alt+F1`, `F2`, `F3`, ... | Switch to *n*-th virtual console |
| `Alt+ ←` | Switch to previous virtual console |
| `Alt+ →` | Switch to next virtual console |
| `Scroll Lock` | When Scroll Lock is activated, input/output is locked |
| `Shift+PgUp`/`PgDown` | Scrolls console buffer up/down |
| `Ctrl+c` | Kills current task |
| `Ctrl+d` | Inserts an EOF |
| `Ctrl+z` | Pauses current Task |

See also [console_codes(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/console_codes.4).

## Fonts

**Note:** This section is about the [Linux console](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console"). For alternative console solutions offering more features (full Unicode fonts, modern graphics adapters etc.), see [fbterm](/index.php/Fbterm "Fbterm"), [KMSCON](/index.php/KMSCON "KMSCON") or similar projects.

By default, the [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") uses the kernel built-in font with a [CP437](https://en.wikipedia.org/wiki/CP437 "wikipedia:CP437") character set, but this can be easily changed.

The [Linux console](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console") uses UTF-8 encoding by default, but because the standard VGA-compatible framebuffer is used, a console font is limited to either a standard 256, or 512 glyphs. If the font has more than 256 glyphs, the number of colours is reduced from 16 to 8\. In order to assign correct symbol to be displayed to the given Unicode value, a special translation map, often called *unimap*, is needed. Nowadays most of the console fonts have the *unimap* built-in; historically, it had to be loaded separately.

The [kbd](https://www.archlinux.org/packages/?name=kbd) package provides tools to change virtual console font and font mapping. Available fonts are saved in the `/usr/share/kbd/consolefonts/` directory, those ending with *.psfu* or *.psfu.gz* have a Unicode translation map built-in.

Keymaps, the connection between the key pressed and the character used by the computer, are found in the subdirectories of `/usr/share/kbd/keymaps/`, see [/Keyboard configuration](/index.php/Linux_console/Keyboard_configuration "Linux console/Keyboard configuration") for details.

**Note:** Replacing the font can cause issues with programs that expect a standard VGA-style font, such as those using line drawing graphics.

**Tip:** For European based languages written in Latin/Greek letters you can use `eurlatgr` font, it includes a broad range of Latin/Greek letter variations as well as special characters [[2]](https://lists.altlinux.org/pipermail/kbd/2014-February/000439.html).

### Preview and temporary changes

**Tip:** An organized library of images for previewing is available: [Linux console fonts screenshots](http://alexandre.deverteuil.net/pages/consolefonts/).

```
$ showconsolefont

```

shows a table of glyphs or letters of a font.

`setfont` temporarily change the font if passed a font name (in `/usr/share/kbd/consolefonts/`) such as

```
$ setfont lat2-16 -m 8859-2

```

So to have a **small 8x8** font, with that font installed like seen below, use e.g.:

```
$ setfont -h8 /usr/share/kbd/consolefonts/drdos8x8.psfu.gz

```

Font names are case-sensitive. With no parameter, `setfont` returns the console to the default font.

**Tip:** All font changing commands can be typed in "blind".

**Note:** *setfont* only works on the console currently being used. Any other consoles, active or inactive, remain unaffected.

### Persistent configuration

The `FONT` variable in `/etc/vconsole.conf` is used to set the font at boot, persistently for all consoles. See [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) for details.

For displaying characters such as *Č, ž, đ, š* or *Ł, ę, ą, ś* using the font `lat2-16.psfu.gz`:

 `/etc/vconsole.conf` 
```
...
FONT=lat2-16
FONT_MAP=8859-2
```

It means that second part of ISO/IEC 8859 characters are used with size 16\. You can change font size using other values (e.g. `lat2-08`). For the regions determined by 8859 specification, look at the [Wikipedia:ISO/IEC 8859#The parts of ISO/IEC 8859](https://en.wikipedia.org/wiki/ISO/IEC_8859#The_parts_of_ISO.2FIEC_8859 "wikipedia:ISO/IEC 8859").

To use the specified font in early userspace, use the `consolefont` hook in `/etc/mkinitcpio.conf`. See [Mkinitcpio#HOOKS](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") for more information.

If the fonts seems to not change on boot, or change only temporarily, it is most likely that they got reset when graphics driver was initialized and console was switched to framebuffer. To avoid this, load your graphics driver earlier. See for example [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting"), [[3]](https://bbs.archlinux.org/viewtopic.php?id=145765) or other ways to setup your framebuffer before `/etc/vconsole.conf` is applied.

## See also

*   [General troubleshooting#Scrollback](/index.php/General_troubleshooting#Scrollback "General troubleshooting")
*   [The TTY demystified – Linus Åkesson](https://www.linusakesson.net/programming/tty/)