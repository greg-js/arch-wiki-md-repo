[android_mpris_bridge-git](https://aur.archlinux.org/packages/android_mpris_bridge-git/) is available in the [AUR](/index.php/AUR "AUR"). It enables you to control (pause/play/change volume) media players which support the [MPRIS D-Bus interface](http://www.freedesktop.org/wiki/Specifications/mpris-spec/) (such as [vlc](https://www.archlinux.org/packages/?name=vlc) and [dragon](https://www.archlinux.org/packages/?name=dragon)) from your Android device.

## Running the application

If you are using [PulseAudio](/index.php/PulseAudio "PulseAudio"), append this line to /etc/pulse/default.pa in order to load it's dbus module at startup :

```
pactl load-module module-dbus-protocol

```

To automatically load the avahi daemon at startup run this command:

```
# systemctl enable avahi-daemon.service

```

After rebooting your system, run this command from a terminal:

```
$ mprisap-launch

```

Make sure your Android device and PC are both connected to the same wireless network.

On the Android device install the application apk from: [https://bitbucket.org/mderezynski/android_mpris_bridge/downloads](https://bitbucket.org/mderezynski/android_mpris_bridge/downloads)

And search for your MPRIS access point.