[SpaceFM](https://ignorantguru.github.io/spacefm/) (a fork of [PCManFM](/index.php/PCManFM "PCManFM")) is a lightweight, highly configurable, desktop-independent multi-panel tabbed file and desktop manager. It features a built-in virtual file system, a [udev](/index.php/Udev "Udev")-based device manager, a customisable menu system, and [Bash](/index.php/Bash "Bash") integration.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 File searches](#File_searches)
    *   [2.2 Desktop management](#Desktop_management)
    *   [2.3 Mounting remote hosts](#Mounting_remote_hosts)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Open archive in app instead of extracting](#Open_archive_in_app_instead_of_extracting)
    *   [3.2 Show custom context menu command only on files/folders](#Show_custom_context_menu_command_only_on_files.2Ffolders)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Columns are not resizeable](#Columns_are_not_resizeable)
    *   [4.2 Segmentation faults](#Segmentation_faults)

## Installation

[Install](/index.php/Install "Install") the [spacefm](https://aur.archlinux.org/packages/spacefm/) package.

Or you can use [spacefm-gtk2](https://aur.archlinux.org/packages/spacefm-gtk2/) package if you need a GTK+ 2 version.

## Usage

See the [User's Manual](https://ignorantguru.github.io/spacefm/spacefm-manual-en.html).

### File searches

SpaceFM provides a built-in file search feature similar to [catfish](https://www.archlinux.org/packages/?name=catfish):

```
$ spacefm -f

```

### Desktop management

SpaceFM includes a lightweight desktop manager. [[1]](https://ignorantguru.github.io/spacefm/spacefm-manual-en.html#invocation-desktopmanager). It replaces the desktop menu, adds desktop icons, and sets the wallpaper.

To restore the native window manager menu, open `Desktop preferences`

```
$ spacefm --desktop-pref

```

and enable the `Right click shows WM menu` option in the `Desktop` tab. Consider adding the above command to a keybind and/or the native desktop menu for easy access.

To run SpaceFM as a [daemon](/index.php/Daemon "Daemon") without it managing the desktop [[2]](https://ignorantguru.github.io/spacefm/spacefm-manual-en.html#invocation-daemonmode), use:

```
$ spacefm -d

```

How SpaceFM may be autostarted as a daemon process or to manage the desktop for a standalone [window manager](/index.php/Window_manager "Window manager") will depend on the window manager itself. Should a window manager not provide an autostart file, edit [xinitrc](/index.php/Xinitrc "Xinitrc") or [xprofile](/index.php/Xprofile "Xprofile").

### Mounting remote hosts

SpaceFM supports mounting remote hosts via [udevil](/index.php/Udisks#devmon "Udisks"). To add a remote host, add the access URL into the URL bar. A terminal window should pop up showing the mounting process which is useful for error tracing.

An overview of the supported remote hosts is available in the [udevil help](https://ignorantguru.github.io/udevil/udevil--help.html). For example to mount a remote FTP server:

```
ftp://user:pass@sys.domain/share

```

## Tips and tricks

### Open archive in app instead of extracting

By default, SpaceFM is configured to extract an archive when double clicking on it. If you instead want to open it with your default archive manager such as [file-roller](https://www.archlinux.org/packages/?name=file-roller), then select an archive, right-click for context menu, and then: Open / Archive default / Open With App

### Show custom context menu command only on files/folders

If you have a custom context menu command that should be only shown on selection of files or folders, then add the following rules to `Menu Item Properties -> Context`:

```
MIME Type equals true
File Is Dir equals true
File Is Text equals true

```

## Troubleshooting

### Columns are not resizeable

This should only happen on the first start of SpaceFM (GTK+ 2 version). [[3]](https://github.com/IgnorantGuru/spacefm/issues/382)

### Segmentation faults

If SpaceFM crashes with errors such as:

```
localhost kernel: [245086.687050] spacefm[30684]: segfault at 3e8000003e8 ip 00007fc95c586866 sp 00007fffb1dc9cc0 error 4 in libgtk-x11-2.0.so.0.2400.24[7fc95c446000+435000]

```

SpaceFM uses many different GUI elements, and is thus suspectible to a malfunctioning theme (especially in GTK+ 3). Try a different theme such as Raleigh (default theme). To do so for SpaceFM only, in GTK+ 2:

```
GTK2_RC_FILES=/usr/share/themes/Raleigh/gtk-2.0/gtkrc spacefm

```

See [[4]](https://ignorantguru.github.io/spacefm/spacefm-manual-en.html#invocation-gtkthemes) for details.