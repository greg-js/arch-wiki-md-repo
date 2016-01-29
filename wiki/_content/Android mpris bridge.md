# Android mpris bridge

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Android mpris bridge#](https://wiki.archlinux.org/index.php/Talk:Android_mpris_bridge))

[android_mpris_bridge-git](https://aur.archlinux.org/packages/android_mpris_bridge-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/android_mpris_bridge-git)]</sup> is available in the [AUR](/index.php/AUR "AUR"). It enables you to control (pause/play/change volume) media players which support the [MPRIS D-Bus interface](http://www.freedesktop.org/wiki/Specifications/mpris-spec/) (such as [vlc](https://www.archlinux.org/packages/?name=vlc) and [dragon](https://www.archlinux.org/packages/?name=dragon)) from your Android device.

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Android_mpris_bridge&oldid=416176](https://wiki.archlinux.org/index.php?title=Android_mpris_bridge&oldid=416176)"