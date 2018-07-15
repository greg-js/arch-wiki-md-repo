There are two popular ways of configuring a Linux terminal to work transparently over a wallpaper, without any borders, menu bars or toolbars. This is very popular among developers because of its practical and coolness factor. Example: using it to view source-code or to get an interactive process status of the system with htop. Something like conky, but not quite.

## Contents

*   [1 Using Tilda](#Using_Tilda)
*   [2 Setup by desktop environment](#Setup_by_desktop_environment)
    *   [2.1 Openbox, Compiz and alike](#Openbox.2C_Compiz_and_alike)
    *   [2.2 Gnome](#Gnome)
    *   [2.3 Xfce4](#Xfce4)

## Using Tilda

[Tilda](/index.php/Tilda "Tilda") is a highly customizable GTK based drop-down terminal emulator, inspired by terminals featured in games like Quake, Doom and Half-Life, where the terminal has no border and is hidden from the desktop till a keyboard shortcut is pressed. To achieve the desired look, edit the configuration as follows:

1.  Under the *General* tab, uncheck *Always on Top*.
2.  Under *Appearance* you can edit the height and width to your liking, but make sure you check *Enable Transparency* and make the *Level of Transparency* 100%.
3.  Under *Colors* tab, chose *Green on Black* or *Personalize*.
4.  Under *Scrolling* you select *Disabled*.

## Setup by desktop environment

### Openbox, Compiz and alike

With versatile window managers like [Openbox](/index.php/Openbox "Openbox") it is easy to create a terminal on the desktop. *Tilda* is highly configurable and might be your terminal of choice. Right-click on *Tilda* and configure the size to your needs, then set transparency to 100%, uncheck the option to start *Tilda* hidden.

Now you only have to set *Tilda* as "below" according to your window manager. For Compiz, this is done with the "Rules for Windows"-plugin, for Openbox, add to the "applications"-section of `rc.xml` the following lines:

```
<application name="tilda">
<layer>below</layer>
</application>

```

Et voila, you have a transparent terminal the size of your choice on your desktop, that will not appear in the tasklist and is permanently below.

### Gnome

It is proposed here to install the [devilspie](https://www.archlinux.org/packages/?name=devilspie) package which provides control over the placement and the behavior of the terminal window. It can be configured to detect windows as they are created, and match the window to a set of rules. If the window matches the rules, it can perform a series of actions on that window.

Follow the steps below to configure *devilspie* to catch the terminal emulator on the fly and setup its style as desired:

	1\. Create a *devilspie* configuration file: it has the extension *.ds* and is within the `~/.devilspie` folder. This is the default location for configuration.

 `~/.devilspie/DesktopConsole.ds` 
```
(if
(matches (window_name) "DesktopConsole_1")
(begin
(stick)
(below)
(undecorate)
(skip_pager)
(skip_tasklist)
(wintype "dock")
(geometry "+240+250")
(geometry "954×680")
)
)

```

For a complete list of options check the [list of options](http://foosel.org/linux/devilspie).

	2\. Open a gnome-terminal window go to *Edit > Profile > New*. Name it DesktopConsole_1.

Edit the Profile, to achieve our desired look we will need to edit the default configurations:

Under *General* tab, **uncheck** "Show menubar by default in new terminals".

Under *Colors* tab, **choose** "Green on Black" (choose whatever you like, i like this).

Under *Effects* tab, **choose** "Transparent background". Make sure the scroll is set to "None".

Under *Scrolling* tab, **select** "Disabled".

	3\. In this step we will setup devilspie and our custom terminal profile to load on bootup.

Go to *Systems > Preferences > Sessions*. Add a new session by using the `+` sign. The first one we will put, "devilspie", in both name and command. The second session we will put "gnome-terminal", under name and "gnome-terminal --window-with-profile=DesktopConsole_1 --title=DesktopConsole_1", under command. Here we are basically calling gnome-terminal with the custom profile we created earlier.

**Note:** if you have trouble with the window position you can specify the geometry in the command options here.

	4\. Logout/login and you should have your desired look.

You can customize more to fit your needs and style, have more than one terminal; I will leave it to your imagination.

### Xfce4

Using *wmctrl* this can be achieved with the default *xfce4-terminal's* command line options. The sample script below is rather self-explanatory...

```
#!/bin/bash
xfce4-terminal --hide-borders --hide-toolbar --hide-menubar --title=desktopconsole --geometry=130x44+0+0 &
sleep 5
wmctrl -r desktopconsole -b add,below,sticky
wmctrl -r desktopconsole -b add,skip_taskbar,skip_pager

```

**Note:** A more revised version of this script can be found here [https://bbs.archlinux.org/viewtopic.php?id=154094](https://bbs.archlinux.org/viewtopic.php?id=154094)

By naming the the terminal with *--title* one can easily identify it's window and add/remove properties through *wmctrl* accordingly. Setting the size and possition with the *--geometry* option follows this rule: (Width-in-characters)x(height-in-charactors)+x+y where x and y are the position in pixels offset from the upper-left corner of the display (which starts at +0+0). transparency and disabling the scrollbar can be set through the terminal's *preferences* menu under the *appearance* and *general* tabs. Once the user has the script customized to their needs or wants they can simply mark it as executable (or chmod a+x /path/to/script.sh) then add it to their startup under *Applications Menu > Settings > Session and Startup > Applications Autostart*.

**Note:** The previous was tested only on Xfce4 with Xfwm4 but a similar approach may work with other window managers. For a list on environments which wmctrl may work with visit [w:wmctrl](https://en.wikipedia.org/wiki/wmctrl "w:wmctrl")