# Volnoti

[Volnoti](https://github.com/davidbrazdil/volnoti) is, according to its own GitHub page,

	"_A lightweight volume notification daemon for GNU/Linux and other POSIX operating systems. It is based on GTK+ and D-Bus and should work with any sensible window manager. The original aim was to create a volume notification daemon for lightweight window managers like LXDE or XMonad. It is known to work with a wide range of WMs, including GNOME, KDE, Xfce, LXDE, XMonad, i3 and many others._"

Volnoti can be useful to check volume changes if you are running a lightweight window manager like [Openbox](/index.php/Openbox "Openbox"), which doesn't usually come with a notification daemon, especially in combination with your laptop/keyboard's special keys.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage and configuration](#Usage_and_configuration)
    *   [2.1 Starting Volnoti](#Starting_Volnoti)
    *   [2.2 Configuration with Xbindkeys](#Configuration_with_Xbindkeys)

## Installation

Install the [volnoti](https://aur.archlinux.org/packages/volnoti/) package from [AUR](/index.php/AUR "AUR").

## Usage and configuration

### Starting Volnoti

To start the daemon, run the command

```
$ volnoti

```

Volnoti will run in background. In order to have Volnoti run automatically when your window manager starts, add the command to your WM's autostart file (e.g. `~/.config/openbox/autostart` if you're using Openbox). Check the program is running by typing in your terminal emulator

```
$ volnoti-show 20

```

A semi-transparent square should appear at the centre of your screen, showing a volume of 25%. Now you should configure Volnoti to display a notification each time your volume is changed.

### Configuration with Xbindkeys

The configuration below will use Volnoti, [Alsa](/index.php/Alsa "Alsa") and [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") to show the volume changes while pressing the hotkeys; this example will assume Xbindkeys has already been install and configured as described in its page.

Open `~./xbindkeysrc` in a text editor and add these lines before the string `# End of xbindkeys configuration`:

```
# Increase volume
"amixer set Master 5%+ && amixer get Master | egrep -o "([0-9]+)%" | egrep -o "[0-9]+" | xargs -0 volnoti-show"
   XF86AudioRaiseVolume

# Decrease volume
"amixer set Master 5%- && amixer get Master | egrep -o "([0-9]+)%" | egrep -o "[0-9]+" | xargs -0 volnoti-show"
   XF86AudioLowerVolume

# Toggle volume
"amixer set Master toggle; if [[ -n $(amixer get Master | grep 'Mono:' | grep -o "\[off\]") ]] ; then volnoti-show -m -v; else amixer get Master | egrep -o "([0-9]+)%" | egrep -o "[0-9]+" | xargs -0 volnoti-show; fi"
   XF86AudioMute

```

The first two commands will increase or lower the volume when the corresponding special keys are pressed, reading the new volume level and sending it as an argument to `volnoti-show`; the third one will toggle the volume and display Volnoti's corresponding notification (according to whether the volume was muted or unmuted).

Now you can restart Xbindkeys with `kill -1 $(pidof xbindkeys)` (or reboot your PC, after making sure both Volnoti and Xbindkeys are in your autostart file) and test your configuration.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Volnoti&oldid=416980](https://wiki.archlinux.org/index.php?title=Volnoti&oldid=416980)"