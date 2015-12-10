# Default applications

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Window manager](/index.php/Window_manager "Window manager")

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** [File managers](#File_managers) and [Gnome Control Center](#Gnome_Control_Center) are only front-ends to the [Desktop entries method](#MIME_types_and_desktop_entries), similarly to [gnome-defaults-list](#gnome-defaults-list) and following. The layout should be more logical. (Discuss in [Talk:Default applications#](https://wiki.archlinux.org/index.php/Talk:Default_applications))

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** `org.freedesktop.FileManager1` [D-Bus](/index.php/D-Bus "D-Bus") service may mess with the default file manager, e.g. when using [Firefox](/index.php/Firefox "Firefox"). (Discuss in [Talk:Default applications#](https://wiki.archlinux.org/index.php/Talk:Default_applications))

Default applications can be set for use with particular file types (e.g. the [Firefox](/index.php/Firefox "Firefox") web browser for `HTML` files). Where undertaken, files may be opened and/or edited with the desired application much faster and more conveniently. There are also numerous methods to configure default applications in Linux. This page will explain the most common methods: File Managers, MIME types, and environment variables.

## Contents

*   [1 MIME types and desktop entries](#MIME_types_and_desktop_entries)
    *   [1.1 File managers](#File_managers)
    *   [1.2 Gnome Control Center](#Gnome_Control_Center)
    *   [1.3 gnome-defaults-list](#gnome-defaults-list)
    *   [1.4 xdg-open](#xdg-open)
    *   [1.5 Custom file associations](#Custom_file_associations)
    *   [1.6 Maintaining settings for multiple desktop environments](#Maintaining_settings_for_multiple_desktop_environments)
*   [2 Using environment variables](#Using_environment_variables)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Applications do not appear in the Open With... context menu (of a file manager)](#Applications_do_not_appear_in_the_Open_With..._context_menu_.28of_a_file_manager.29)

## MIME types and desktop entries

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Lacks clarity, content tacked on (Discuss in [Talk:Default applications#](https://wiki.archlinux.org/index.php/Talk:Default_applications))

The modern method to start applications is using [Desktop entries](/index.php/Desktop_entries "Desktop entries"). This way, programs can advertise which kind of files (to be exact: what MIME-types) they can open. For instance, `gimp.desktop` states `MimeType=image/bmp;image/gif;...`.

[freedesktop.org](http://www.freedesktop.org/wiki) recommends how to specify default (preferred) applications for MIME-types in their [Association between MIME types and applications](http://standards.freedesktop.org/mime-apps-spec/mime-apps-spec-1.0.html) standard. This involves writing into files called `mimeapps.list` which are looked up in the following order of paths:

<table class="wikitable">

<tbody>

<tr>

<th>Path</th>

<th>Usage</th>

</tr>

<tr>

<td>`$HOME/.config/$desktop-mimeapps.list`</td>

<td>user overrides, desktop-specific</td>

</tr>

<tr>

<td>`$HOME/.config/mimeapps.list`</td>

<td>user overrides</td>

</tr>

<tr>

<td>`/etc/xdg/$desktop-mimeapps.list`</td>

<td>sysadmin and vendor overrides, desktop-specific</td>

</tr>

<tr>

<td>`/etc/xdg/mimeapps.list`</td>

<td>sysadmin and vendor overrides</td>

</tr>

<tr>

<td>`$HOME/.local/share/applications/$desktop-mimeapps.list`</td>

<td>for compatibility but now deprecated, desktop-specific</td>

</tr>

<tr>

<td>`$HOME/.local/share/applications/mimeapps.list`</td>

<td>for compatibility but now deprecated</td>

</tr>

<tr>

<td>`/usr/local/share/applications/$desktop-mimeapps.list` and  
`/usr/share/applications/$desktop-mimeapps.list`</td>

<td>distribution-provided defaults, desktop-specific</td>

</tr>

<tr>

<td>`/usr/local/share/applications/mimeapps.list` and  
`/usr/share/applications/mimeapps.list`</td>

<td>distribution-provided defaults</td>

</tr>

</tbody>

</table>

In this table, `$VARS` are environment variables and `$desktop` is the name of the current desktop (in lowercase), for example `kde`, `gnome`, `xfce`, etc.

The default application for a given MIME-type is specified by writing into the group `[Default Applications]` in the `mimeapps.list` file. In the following example, application `default1.desktop` (if it is installed) will be used for `mimetype1`, and otherwise `default2.desktop` (if it is installed and `default1.desktop` is not):

```
[Default Applications]
mimetype1=default1.desktop;default2.desktop

```

The applications are written as a semicolon-separated list of [desktop file IDs](http://standards.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html#desktop-file-id).

In the absence of such an entry, the next `mimeapps.list` in the path hierarchy will be checked. Once all levels have been checked, if no entry could be found, then programs can pick any of the _.desktop_ files associated with the MIME-type, taking into account added and removed associations as per these other groups which may be specified in `mimeapps.list` files:

```
[Added Associations]
mimetype1=foo1.desktop;foo2.desktop;foo3.desktop
mimetype2=foo4.desktop
[Removed Associations]
mimetype1=foo5.desktop

```

The `[Added Associations]` group defines additional associations of applications with MIME-types, as if the _.desktop_ file was listing this MIME-type in the first place. The `[Removed Associations]` group removes associations of applications with MIME-types, as if the _.desktop_ file was **not** listing this MIME-type in the first place. The entries in `[Default Applications]` should also be considered to add an association between application and MIME-type in the same manner.

**Note:**

*   Arch Linux itself does not provide any system-wide preferences for associations, but other distributions and specific desktop environments may do so via `mimeapps.list` or the older but deprecated `defaults.list` files.
*   As the standards for setting default applications have been recently changed, not all programs will comply with them yet. Indeed, the programs provided by freedesktop.org's [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) package do not fully follow their own standards!
*   Your choice of desktop environment, or none, will also affect how your default applications are stored.
*   When the program `update-desktop-database` is run (usually as root during the (un)installation of a package), it updates files called `mimeinfo.cache` in the `/usr/local/share/applications` and `/usr/share/applications` directories. These files keep track of which MIME-types are associated with which _.desktop_ files overall. This file should not be edited by the user.

### File managers

Most file managers will allow for specific applications to be set as the defaults for various file types. New defaults may also be set at any time. For example, to set a default application using [thunar](https://www.archlinux.org/packages/?name=thunar), the native file manager for [Xfce](/index.php/Xfce "Xfce"):

*   `right-click` the file-type desired
*   Select `Open with another application`
*   Select the desired application
*   Ensure that the `Use as default for this kind of file` check-box is ticked
*   Click the `Open` button.

The general process will be very similar for most other popular file managers, including [PCManFM](/index.php/PCManFM "PCManFM") and [spacefm](https://www.archlinux.org/packages/?name=spacefm).

### Gnome Control Center

If it is installed, run `gnome-control-center`, open `System` > `Details` > `Default Applications`.

### gnome-defaults-list

[gnome-defaults-list](https://aur.archlinux.org/packages/gnome-defaults-list/)<sup><small>AUR</small></sup> is available from the [AUR](/index.php/AUR "AUR"), and contains a list of file-types and programs specific to the GNOME desktop. The list is installed to `/etc/gnome/defaults.list`.

Open this file with a text editor. Here you can replace a given application with the name of the program of your choice. For example, the media-player `totem` can be replaced with another, such as `vlc`. Save the file to `~/.local/share/applications/defaults.list`.

### xdg-open

[xdg-open](/index.php/Xdg-open "Xdg-open") is a desktop-independent tool for starting default applications. Many applications invoke the `xdg-open` command internally. xdg-open uses xdg-mime to query `~/.local/share/applications/mimeapps.list` (among other things; if you use a mainstream DE like GNOME, KDE or LXDE, xdg-open might try using their specific tools before xdg-mime) to find the MIME type of the file that is to be opened and the default application associated with that MIME type.

See [xdg-open](/index.php/Xdg-open "Xdg-open") for more information.

### Custom file associations

The following method creates a custom mime type and file association manually. This is useful if your desktop does not have a mime type/file association editor installed. In this example, a fictional multimedia application 'foobar' will be associated with all `*.foo` files. This will only affect the current user.

First, create the file `~/.local/share/mime/packages/application-x-foobar.xml`:

```
$ mkdir -p ~/.local/share/mime/packages
$ cd ~/.local/share/mime/packages
$ touch application-x-foobar.xml

```

Then edit `~/.local/share/mime/packages/application-x-foobar.xml` and add this text:

```
<?xml version="1.0" encoding="UTF-8"?>
<mime-info xmlns="http://www.freedesktop.org/standards/shared-mime-info">
    <mime-type type="application/x-foobar">
        <comment>foo file</comment>
        <icon name="application-x-foobar"/>
        <glob-deleteall/>
        <glob pattern="*.foo"/>
    </mime-type>
</mime-info>

```

Note that you can use any icon, including one for another application.

Next, edit or create the file `~/.local/share/applications/foobar.desktop` to contain something like:

```
[Desktop Entry]
Name=Foobar
Exec=/usr/bin/foobar
MimeType=application/x-foobar
Icon=foobar
Terminal=false
Type=Application
Categories=AudioVideo;Player;Video;
Comment=

```

Note that Categories should be set appropriately for the application type (in this example, a multimedia app).

Now update the applications and mime database with:

```
$ update-desktop-database ~/.local/share/applications
$ update-mime-database    ~/.local/share/mime

```

Programs that use mime types, such as file managers, should now open `*.foo` files with foobar. (You may need to restart your file manager to see the change.)

### Maintaining settings for multiple desktop environments

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** This should be either expanded on (particularly referencing `NoDisplay`, or merged to [Desktop entries](/index.php/Desktop_entries "Desktop entries") (Discuss in [Talk:Default applications#](https://wiki.archlinux.org/index.php/Talk:Default_applications))

The `OnlyShowIn` field of a .desktop file may be useful; see [this page](http://standards.freedesktop.org/menu-spec/latest/).

## Using environment variables

Most non-graphical programs use [Environment variables](/index.php/Environment_variables "Environment variables"), such as `EDITOR` or `BROWSER`. These can be set in your terminal's autostart file (e.g. `~/.bashrc`):

 `~/.bashrc` 

```
export EDITOR="nano"
export BROWSER="firefox"

```

## Troubleshooting

### Applications do not appear in the Open With... context menu (of a file manager)

Sometimes, a certain application will not appear in the right-click _Open With..._ dialog. To fix this problem, locate the `.desktop` file in `/usr/share/applications`, edit it as root, and add `%U` to the end of the `Exec=` line. For example, Kile currently has this problem; you need to edit `/usr/share/applications/kde4/kile.desktop` and change the line reading `Exec=kile` to read `Exec=kile %U`. Also, please file a bug against the upstream project if you notice this problem.

You may also have to edit the `MimeType` list in the `.desktop` file if you install extensions that allow an application to handle additional MIME types.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Default_applications&oldid=401269](https://wiki.archlinux.org/index.php?title=Default_applications&oldid=401269)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments")