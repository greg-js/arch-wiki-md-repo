There are two official Linux versions of Skype available:

*   The new Skype for Linux (version 5.x, currently in beta): see [#Skype for Linux](#Skype_for_Linux)

	It is basically the web version in a wrapper. Group video chat is not yet working.

*   The old Skype (version 4.x, final release in June 2014): see [#Legacy Skype](#Legacy_Skype)

	Legacy Skype does not support calling to some newer clients.[[1]](https://blogs.skype.com/news/2016/07/13/skype-for-linux-alpha-and-calling-on-chrome-and-chromebooks/) **Should have stopped working on 1 July 2017**[[2]](http://www.omgubuntu.co.uk/2017/06/skype-4-3-linux-stop-working-july-2017) but is still working as of 5 July 2017.

Alternatively, you can use the web version at [web.skype.com](https://web.skype.com/). It has working voice and video chat (at least on Chromium/Chrome and Firefox), but group video chat is not yet working.

## Contents

*   [1 Skype for Linux](#Skype_for_Linux)
*   [2 Legacy Skype](#Legacy_Skype)
    *   [2.1 Installation](#Installation)
    *   [2.2 Skype sound](#Skype_sound)
    *   [2.3 Restricting Skype access](#Restricting_Skype_access)
        *   [2.3.1 systemd-nspawn](#systemd-nspawn)
        *   [2.3.2 Docker](#Docker)
        *   [2.3.3 Use Skype with special user](#Use_Skype_with_special_user)
            *   [2.3.3.1 Access Pulseaudio controls when using Skype as a different user](#Access_Pulseaudio_controls_when_using_Skype_as_a_different_user)
            *   [2.3.3.2 Open URLs in your user's browser](#Open_URLs_in_your_user.27s_browser)
            *   [2.3.3.3 Access received files](#Access_received_files)
        *   [2.3.4 AppArmor](#AppArmor)
        *   [2.3.5 TOMOYO](#TOMOYO)
    *   [2.4 Troubleshooting](#Troubleshooting)
        *   [2.4.1 GUI does not match GTK Theme](#GUI_does_not_match_GTK_Theme)
        *   [2.4.2 Test call fails](#Test_call_fails)
        *   [2.4.3 No video with GSPCA webcams](#No_video_with_GSPCA_webcams)
        *   [2.4.4 No video with Compiz](#No_video_with_Compiz)
        *   [2.4.5 Skype does not use a GTK+ theme, even though other Qt apps do](#Skype_does_not_use_a_GTK.2B_theme.2C_even_though_other_Qt_apps_do)
        *   [2.4.6 No incoming video stream](#No_incoming_video_stream)
        *   [2.4.7 Monster/low-octave "growling" distortion over mic](#Monster.2Flow-octave_.22growling.22_distortion_over_mic)
        *   [2.4.8 Crackling/noisy sound (mainly using 64-bit OS)](#Crackling.2Fnoisy_sound_.28mainly_using_64-bit_OS.29)
            *   [2.4.8.1 Solution 1](#Solution_1)
            *   [2.4.8.2 Solution 2](#Solution_2)
        *   [2.4.9 Skype sounds stops media player or other sound sources](#Skype_sounds_stops_media_player_or_other_sound_sources)
        *   [2.4.10 You are already signed in on this computer](#You_are_already_signed_in_on_this_computer)
        *   [2.4.11 Empty white screen window](#Empty_white_screen_window)
        *   [2.4.12 Skype doesn't output any sound after upgrading PulseAudio](#Skype_doesn.27t_output_any_sound_after_upgrading_PulseAudio)
*   [3 Skype plugin for Pidgin](#Skype_plugin_for_Pidgin)

## Skype for Linux

There is a new *Skype for Linux Beta*, which is basically the web version at [web.skype.com](https://web.skype.com/) in a wrapper. It has working text, (group) voice, and video chat (group video chat is not yet working).

[Install](/index.php/Install "Install") it with the [skypeforlinux](https://aur.archlinux.org/packages/skypeforlinux/) or [skypeforlinux-bin](https://aur.archlinux.org/packages/skypeforlinux-bin/) package.

## Legacy Skype

### Installation

[Install](/index.php/Install "Install") the [skype](https://aur.archlinux.org/packages/skype/) package.

Running Skype is just as easy. Type `skype` into a terminal or double-click the Skype icon on your desktop or in your DE's application menu.

### Skype sound

Skype requires [PulseAudio](/index.php/PulseAudio "PulseAudio") for voice communication and does not support plain [ALSA](/index.php/ALSA "ALSA").

Alternatively, if you do not want to use PulseAudio, you can follow [ALSA#PulseAudio compatibility](/index.php/ALSA#PulseAudio_compatibility "ALSA")

### Restricting Skype access

There are a couple of reasons you might want to restrict Skype's access to your computer:

*   The skype binary is disguised against decompiling, so nobody is (still) able to reproduce what it really does.
*   It produces encrypted traffic even when you are not actively using Skype.

See [[3]](http://www1.cs.columbia.edu/~salman/skype/index.html) for more information.

Restrictions can be implemented in a number of ways, with varying ease and security. It is possible to run Skype in a container, run it as a separate user, or use the [Mandatory Access Control](https://en.wikipedia.org/wiki/Mandatory_access_control "wikipedia:Mandatory access control") functionality available in the Linux kernel.

#### systemd-nspawn

**Warning:** systemd-nspawn provides the most straightforward way to run an application in a separate environment, however it is [not considered](https://www.freedesktop.org/software/systemd/man/systemd-nspawn.html) to provide a fully secure setup.

The following script will create a container in `/mnt/stor/vm/skype` and run Skype from there on each subsequent run. Fetching the default pacman config is necessary for 64-bit systems with multilib enabled, but be careful in case you have custom repositories enabled. Note that sound and video may be broken with this method.

```
 #!/bin/bash
 set -e
 DEST=/mnt/stor/vm/skype
 if [ ! -d "$DEST" ];then
     sudo mkdir -p "$DEST/var/lib/pacman/";
     sudo mkdir -p "$DEST/etc/"
     sudo curl https://projects.archlinux.org/svntogit/packages.git/plain/trunk/pacman.conf.i686?h=packages/pacman -o "$DEST/etc/pacman.conf"
     echo sudo skype | sudo pacman --arch i686 --root "$DEST" --cachedir /var/cache/pacman/pkg --config "$DEST/etc/pacman.conf" -Sy - --noconfirm
     sudo systemd-nspawn -D "$DEST" groupadd skype
     sudo systemd-nspawn -D "$DEST" useradd -g skype skype
     sudo mkdir -p $DEST/home/skype/.config/pulse
     sudo cp ~/.config/pulse/cookie $DEST/home/skype/.config/pulse/
     sudo cp ~/.Xauthority $DEST/home/skype/
     sudo chmod 755 -R $DEST/home/skype/
     sudo chown -R 1000:1000 $DEST/home/skype/
 fi
 sudo systemd-nspawn -D "$DEST" --bind=/tmp/.X11-unix --share-system sudo -u skype env DISPLAY=:0 PULSE_SERVER=desktop skype

```

#### Docker

**Warning:** Running Docker has its own set of security implications and caveats. Read the main Docker article for more information.

Install [Docker](/index.php/Docker "Docker") and feel free to [explore Docker Hub](https://hub.docker.com/search/?q=skype&page=1&isAutomated=0&isOfficial=0&pullCount=0&starCount=0) for Skype images prepared by users.

A tried and tested image is [sameersbn/skype](https://github.com/sameersbn/docker-skype) (hosted on Github). It uses X11 and [PulseAudio](/index.php/PulseAudio "PulseAudio") unix domain sockets on the host to enable audio/video support in Skype. A wrapper script mounts the X11 and Pulseaudio sockets inside the container. The X11 socket allows for the user interface to display on the host, while Pulseaudio socket allows for the audio output to be rendered on the host. `/dev/video0` is also mounted.

Container has access to `~/.Skype` and `~/Downloads` directories on your host system. Wrapper scripts are installed into `/usr/local/bin`.

For installation use [upstream instructions](https://github.com/sameersbn/docker-skype/blob/master/README.md).

#### Use Skype with special user

**Warning:** As of version 1.16, Xorg runs as a regular user. This means a special user has no access to X. The following approach only works when enabling root for Xorg; see [Xorg#Rootless Xorg (v1.16)](/index.php/Xorg#Rootless_Xorg_.28v1.16.29 "Xorg").

A special user can be used for running Skype within one's normal environment. Permissions will have to be set to ensure your home directory is not readable by the special Skype user (see [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes")).

An AUR package, [skype-secure](https://aur.archlinux.org/packages/skype-secure/) exists that will run skype as a separate user ("_skype") cleanly. It is heavily based on the information in this section.

Create a new group for the skype user:

```
# groupadd skype

```

Then we have to add the new user:

```
# useradd -m -g skype -G audio,video -s /bin/bash skype

```

**Note:** Maybe you need to add "skype" user to "pulse-access" and "pulse-rt" groups. But it works fine with "audio" and "skype" groups only.

Now add the following line to `/home/skype/.bashrc`:

```
export DISPLAY=":0.0"

```

At last we define the alias (e.g. in `~/.bashrc`):

```
alias skype='xhost +local: && su skype -c skype'

```

Now we can start Skype as the newly created user simply by running `skype` from the command line and entering the password of the user skype.

If you are tired of typing in the skype user's password every time, make sure you installed the [sudo](/index.php/Sudo "Sudo") package, run `visudo` then add this line at the bottom:

```
%wheel ALL=(skype) NOPASSWD: /usr/bin/skype

```

And use this alias to launch skype:

```
alias skype='xhost +local: && sudo -u skype /usr/bin/skype'

```

**Note:** If you forget the `xhost` command, Skype may fail with a "No protocol specified" error on stdout.

I noticed that the newly created user is able to read some of the files in my home directory because the permissions were a+r, so I changed them manually to a-r u+r and changed umask from 022 to 066.

In order to restrict user "skype" accessing your external drive mounted in `/media/data` for instance, make sure first that "skype" does not belong to group "users" (if you used the default group "skype", everything should be fine), then change the accesses on the mount point:

```
# chown :users /media/data
# chmod o-rwx /media/data

```

This way, it is ensured that only the owner (normally "root") and "users" can access the specified directory tree while the others, including "skype", will be forbidden.

##### Access Pulseaudio controls when using Skype as a different user

Audio will not be functional since the special skype user can't connect to the PulseAudio daemon owned by the user which has started the desktop session. However, a socket can be exposed for the new user to connect to the PulseAudio daemon. See [PulseAudio/Examples#Allowing multiple users to use PulseAudio at the same time](/index.php/PulseAudio/Examples#Allowing_multiple_users_to_use_PulseAudio_at_the_same_time "PulseAudio/Examples") for more information.

##### Open URLs in your user's browser

When one clicks URL in chat window, skype execute [xdg-open](/index.php/Xdg-open "Xdg-open") to handle it. By default `xdg-open` uses default web browser for skype user environment. In order to open links in your user's browser perform next setup.

**Note:**

*   [Sudo](/index.php/Sudo "Sudo") should be installed and properly configured.
*   Current example uses [firefox](/index.php/Firefox "Firefox") as preferred browser.
*   Do not forget to adjust *your_user* to proper value.

Log in as skype user:

```
$ sudo -u skype -i

```

Create local preferences dir:

```
$ mkdir -p ~/.local/share/applications

```

Create `/home/skype/.local/share/applications/firefox-sudo.desktop` file:

```
[Desktop Entry]
Name=Firefox
Exec=/home/skype/firefox-wrapper %u
Terminal=false
Type=Application
Categories=Network;WebBrowser;

```

Set `firefox-sudo.desktop` to manage HTTP and HTTPS URLs:

```
$ xdg-mime default firefox-sudo.desktop x-scheme-handler/http
$ xdg-mime default firefox-sudo.desktop x-scheme-handler/https

```

(Optionally) add FTP handler:

```
$ xdg-mime default firefox-sudo.desktop x-scheme-handler/ftp

```

Create `/home/skype/firefox-wrapper` script (adjust *your_user*):

```
#!/bin/bash
DISPLAY=:0.0 HOME=/home/*your_user* sudo -u *your_user* /usr/lib/firefox/firefox -new-tab $1

```

Make it executable:

```
$ chmod +x ~/firefox-wrapper

```

Now as root user open `/etc/sudoers`:

```
# visudo

```

And add permission for skype user to exec user's browser (adjust *your_user*):

```
skype ALL=(*your_user*) NOPASSWD: /usr/lib/firefox/firefox -new-tab http*, /usr/lib/firefox/firefox -new-tab ftp*

```

##### Access received files

By default `skype` stores received files with 600 permissions (only owner can access them). One may use [incron](https://www.archlinux.org/packages/?name=incron) to perform automatic permission fix upon downloading.

**Note:** This example assumes that you configure skype to save received files into `/home/skype/downloads`

Make skype home dir and download dir accessible:

```
# chmod 755 /home/skype /home/skype/downloads

```

[Install](/index.php/Install "Install") incron with the [incron](https://www.archlinux.org/packages/?name=incron) package, and enable and start `incrond` [using systemd](/index.php/Systemd#Using_units "Systemd"). Open incrontab for root user:

```
# incrontab -e

```

Add incron job:

```
/home/skype/downloads IN_CREATE chmod 644 $@/$#

```

Save changes and exit incrontab editor.

To test incron in action just enter skype download dir and create test file:

```
# cd /home/skype/downloads
# install -m 600 /dev/null test.txt
# ls -l test.txt

```

File permissions should be 644 or -rw-r--r--

(Optionally) link skype download dir into your home dir:

```
$ ln -s /home/skype/downloads ~/skype_files

```

#### AppArmor

See the [AppArmor](/index.php/AppArmor "AppArmor") page for how to set up AppArmor.

The userland tools for AppArmor come with a collection of example profiles. Skype is amongst them. Copy this to the directory where AppArmor profiles are stored.

```
# cp -ip /usr/share/apparmor/extra-profiles/usr.bin.skype /etc/apparmor.d/

```

For whatever reason, the profile is not complete. You may wish to modify it further. Here is an example for Skype 4:

```
#include <tunables/global>

/usr/bin/skype {
  #include <abstractions/audio>
  #include <abstractions/consoles>
  #include <abstractions/dbus-session>
  #include <abstractions/gnome>
  #include <abstractions/kde>
  #include <abstractions/nameservice>
  #include <abstractions/video>

  # Executables
  /usr/bin/skype ixmr,
  /usr/lib{,32}/skype/skype ixmr,
  /usr/bin/xdg-open PUxmr,
  /usr/bin/kde4-config PUxmr,

  # Configuration files
  owner @{HOME}/.Skype/ rw,
  owner @{HOME}/.Skype/** krw,
  owner @{HOME}/.config/Skype/ rw,
  owner @{HOME}/.config/Skype/** krw,

  # Downloads/uploads directory
  owner @{HOME}/Public/ rw,
  owner @{HOME}/Public/** krw,

  # Libraries
  /usr/lib{,32}/libv4l/v4l2convert.so mr,
  /usr/share/skype/lib/libQtWebKit.so.4 mr,

  # Shared data
  /usr/share/skype/ r,
  /usr/share/skype/** r,

  # Devices
  /dev/ r,
  /dev/video[0-9]* mrw,

  # System information
  /etc/machine-id r,
  @{PROC}/sys/kernel/{ostype,osrelease} r,
  @{PROC}/sys/vm/overcommit_memory r,
  @{PROC}/[0-9]*/net/arp r,
  owner @{PROC}/[0-9]*/cmdline r,
  owner @{PROC}/[0-9]*/status r,
  owner @{PROC}/[0-9]*/task/ r,
  owner @{PROC}/[0-9]*/task/[0-9]*/stat r,
  owner @{PROC}/[0-9]*/fd/ r,
  /sys/devices/system/cpu/ r,
  /sys/devices/system/cpu/cpu[0-9]*/cpufreq/scaling_{cur_freq,max_freq} r,
  /sys/devices/pci*/*/usb[0-9]*/*/*/modalias r,
  /sys/devices/pci*/*/usb[0-9]*/*/*/video4linux/video[0-9]*/dev r,
  /sys/devices/pci*/*/usb[0-9]*/*/{idVendor,idProduct,speed} r,

  # This probably should go to appropriate abstractions
  /etc/asound.conf r,
  owner @{HOME}/.config/fontconfig/fonts.conf r,
  owner @{HOME}/.config/gtk-3.0/bookmarks r,
  owner @{HOME}/.config/oxygen-gtk/argb-apps.conf rw,
  owner @{HOME}/.config/pulse/cookie krw,
  owner @{HOME}/.icons/** r,
  owner @{HOME}/.kde4/share/config/kdeglobals krw,
  owner @{HOME}/.kde4/share/config/gtkrc-2.0 r,
  owner @{HOME}/.kde4/share/config/oxygenrc r,
  /usr/share/icons/*/index.theme kr,
  /usr/share/nvidia/nvidia-application-profiles-*-rc r,

  # Denials
  deny owner @{HOME}/.mozilla/ r,
  deny owner @{HOME}/.mozilla/** r,
  deny /sys/devices/virtual/dmi/** r,
}
```

**Note:** This example assumes that Skype is configured to save received files into `~/Public`. Feel free to change it to any folder you like.

To use the profile, first be sure `securityfs` is mounted,

```
# mount -t securityfs securityfs /sys/kernel/security

```

Load the profile by the command,

```
# apparmor_parser -r /etc/apparmor.d/usr.bin.skype

```

Now you can run Skype restricted but as your own user. Denials are logged in `messages.log`.

#### TOMOYO

Please note that this section describes using TOMOYO 2.5\. See [TOMOYO Linux#TOMOYO Linux 2.x](/index.php/TOMOYO_Linux#TOMOYO_Linux_2.x "TOMOYO Linux") for installation.

**Note:** Do not forget to populate first the `/etc/tomoyo` directory running: `/usr/lib/tomoyo/init_policy`

*   Open `/etc/tomoyo/exception_policy.conf` file and add these lines:

```
path_group SKYPE_DIRS /home/\*/.Skype/
path_group SKYPE_DIRS /home/\*/.Skype/\{\*\}/
path_group SKYPE_DIRS /home/\*/.config/Skype/\{\*\}/
path_group SKYPE_DIRS /usr/share/skype/\{\*\}/
path_group SKYPE_DIRS /tmp/skype-\*/
path_group SKYPE_DIRS /tmp/skype-\*/\{\*\}/
path_group SKYPE_DIRS /home/\*/Downloads/tmp/\{\*\}/
path_group SKYPE_FILES /home/\*/.Skype/\{\*\}/\*
path_group SKYPE_FILES /home/\*/.config/Skype/\{\*\}/\*
path_group SKYPE_FILES /usr/share/skype/\{\*\}/\*
path_group SKYPE_FILES /home/\*/.Skype/\*
path_group SKYPE_FILES /home/\*/.config/Skype/\*
path_group SKYPE_FILES /usr/share/skype/\*
path_group SKYPE_FILES /tmp/skype-\*/\{\*\}/\*
path_group SKYPE_FILES /home/\*/Downloads/tmp/\{\*\}/\*
path_group SKYPE_FILES /home/\*/Downloads/tmp/\*
path_group ICONS_DIRS /usr/share/icons/\{\*\}/
path_group ICONS_FILES /usr/share/icons/\{\*\}/\*
path_group ICONS_FILES /usr/share/icons/\*
initialize_domain /usr/bin/skype from any
initialize_domain /usr/lib32/skype/skype from any
```

Note that `/home/*/Downloads/tmp` folders are the only folders to which Skype will be able to save received files and from which it will be able to send all files.

*   Then open `/etc/tomoyo/domain_policy.conf` and add the following lines:

```
<kernel> /usr/bin/skype
use_profile 3
use_group 0

misc env \*
file read /bin/bash
file read /usr/bin/bash
file read/write /dev/tty
file read /usr/lib/locale/locale-archive
file read /usr/lib/gconv/gconv-modules
file read /usr/bin/skype
file read /usr/lib32/skype/skype
file execute /usr/lib32/skype/skype exec.realpath="/usr/lib32/skype/skype" exec.argv[0]="/usr/lib32/skype/skype"

<kernel> /usr/lib32/skype/skype
use_profile 3
use_group 0

file append /dev/snd/pcm\*
file chmod /home/\*/.Skype/ 0700
file create /home/\*/.cache/fontconfig/\* 0600-0666
file create /tmp/qtsingleapp-\*-lockfile 0600-0666
file create @SKYPE_FILES 0600-0666
file create /dev/shm/pulse-shm-\* 0700-0777
file execute /usr/bin/firefox
file execute /usr/bin/gnome-open
file execute /usr/bin/notify-send
file execute /usr/bin/opera
file execute /usr/bin/xdg-open
file ioctl /dev/snd/\* 0-0xFFFFFFFFFFFFFFFF
file ioctl /dev/video0 0-0xFFFFFFFFFFFFFFFF
file ioctl anon_inode:inotify 0x541B
file ioctl socket:[family=1:type=2:protocol=0] 0x8910
file ioctl socket:[family=1:type=2:protocol=0] 0x8933
file ioctl socket:[family=2:type=1:protocol=6] 0x541B
file ioctl socket:[family=2:type=2:protocol=17] 0x541B
file ioctl socket:[family=2:type=2:protocol=17] 0x8912
file ioctl socket:[family=2:type=2:protocol=17] 0x8927
file ioctl socket:[family=2:type=2:protocol=17] 0x8B01
file ioctl socket:[family=2:type=2:protocol=17] 0x8B1B
file ioctl socket:[family=2:type=2:protocol=17] 0x8B15
file ioctl socket:[family=2:type=2:protocol=17] 0x8B05
file link/rename /home/\*/.cache/fontconfig/\* /home/\*/.cache/fontconfig/\*
file mkdir /home/\*/.cache/fontconfig/\* 0600
file mkdir @SKYPE_DIRS 0700-0777
file mksock /tmp/qtsingleapp-\* 0755
file read /dev/urandom
file read/write/unlink/truncate /dev/shm/pulse-shm-\*
file read /etc/fonts/conf.avail/\*.conf
file read /etc/fonts/conf.d/\*.conf
file read /etc/fonts/fonts.conf
file read /etc/group
file read /etc/host.conf
file read /etc/hosts
file read /etc/machine-id
file read /etc/nsswitch.conf
file read /etc/resolv.conf
file read /home/\*/.ICEauthority
file read /home/\*/.XCompose
file read /home/\*/.Xauthority
file read /home/\*/.Xdefaults
file read /home/\*/.fontconfig/\*
file read /home/\*/.config/fontconfig/\*
file read /home/\*/.config/pulse/cookie
file read /usr/lib/locale/locale-archive
file read /usr/lib32/gconv/UTF-16.so
file read /usr/lib32/gconv/gconv-modules
file read /usr/lib32/libv4l/v4l2convert.so
file read /usr/lib32/libv4l/plugins/libv4l-mplane.so
file read /usr/lib32/pulseaudio/libpulsecommon-5.0.so
file read /usr/lib32/qt/plugins/bearer/libq\*bearer.so
file read /usr/lib32/qt/plugins/iconengines/libqsvgicon.so
file read /usr/lib32/qt/plugins/imageformats/libq\*.so
file read /usr/lib32/qt/plugins/inputmethods/libqimsw-multi.so
file read /usr/lib32/skype/skype
file read /usr/share/X11/locale/\*/Compose
file read /usr/share/X11/locale/\*/XLC_LOCALE
file read /usr/share/X11/locale/compose.dir
file read /usr/share/X11/locale/locale.alias
file read /usr/share/X11/locale/locale.dir
file read /usr/share/alsa/alsa.conf
file read /usr/share/alsa/cards/\*.conf
file read /usr/share/alsa/pcm/\*.conf
file read /usr/share/fonts/\*/\*/\*
file read /usr/share/locale/\*/LC_MESSAGES/\*.mo
file read /usr/share/ca-certificates/mozilla/\*.crt
file read /var/cache/fontconfig/\*.cache-4
file read @ICONS_FILES
file read proc:/sys/vm/overcommit_memory
file read /sys/devices/\*/\*/\*/\*/\*/modalias
file read /sys/devices/\*/\*/\*/\*/\*/video4linux/video0/dev
file read /sys/devices/\*/\*/\*/\*/idProduct
file read /sys/devices/\*/\*/\*/\*/idVendor
file read /sys/devices/\*/\*/\*/\*/speed
file read /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq
file read /sys/devices/system/cpu/cpu0/cpufreq/scaling_max_freq
file read /sys/devices/system/cpu/online
file read/write /dev/snd/\*
file read/write /dev/video0
file read/write/truncate /home/\*/.config/Trolltech.conf
file read/write/unlink /home/\*/.cache/fontconfig/\*
file read/write/unlink /tmp/qtsingleapp-\*
file read/write/unlink/truncate @SKYPE_FILES
file rename @SKYPE_DIRS @SKYPE_DIRS
file rename @SKYPE_FILES @SKYPE_FILES
file rmdir @SKYPE_DIRS
misc env \*
network inet dgram bind 0.0.0.0 0-65535
network inet dgram bind 127.0.0.1 0
network inet dgram bind/send 0.0.0.0-255.255.255.255 0-65535
network inet stream bind/listen 0.0.0.0 0-65535
network inet stream connect 0.0.0.0-255.255.255.255 0-65535
network unix stream bind/listen/connect /tmp/qtsingleapp-\*
network unix stream connect /tmp/.ICE-unix/\*
network unix stream connect /var/run/dbus/system_bus_socket
network unix stream connect /var/run/nscd/socket
network unix stream connect \000/tmp/.ICE-unix/\*
network unix stream connect \000/tmp/.X11-unix/X0
network unix stream connect \000/tmp/dbus-\*
network unix stream connect /run/user/1000/pulse/native

<kernel> /usr/lib32/skype/skype /usr/bin/xdg-open
use_profile 0
use_group 0

<kernel> /usr/lib32/skype/skype /usr/bin/gnome-open
use_profile 0
use_group 0

<kernel> /usr/lib32/skype/skype /usr/bin/notify-send
use_profile 0
use_group 0
```

*   After finishing editing reload TOMOYO config files by executing these commands:

```
# tomoyo-loadpolicy -df < /etc/tomoyo/domain_policy.conf
# tomoyo-loadpolicy -ef < /etc/tomoyo/exception_policy.conf
```

Skype is now sandboxed.

Please note that this config is generated on 64-bit Arch system, and some of your ioctls and library paths may differ from mentioned above. So in order to fine-tune TOMOYO config for your Skype [start](/index.php/Start "Start") `tomoyo-auditd.service`.

Then go to `/var/log/tomoyo` folder and start watching `reject_003.log`:

```
$ tail -f reject_003.log

```

The output of this command will show you rejected actions for Skype, so you will be able to add them to `domain_policy.conf` file if needed.

See [[4]](http://tomoyo.sourceforge.jp/2.5/index.html.en) for a detailed guide to TOMOYO configuration.

### Troubleshooting

#### GUI does not match GTK Theme

See [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") for information about theming Qt based applications like [VirtualBox](/index.php/VirtualBox "VirtualBox") or Skype. Also, you may need to install the [lib32-gtk-engines](https://aur.archlinux.org/packages/lib32-gtk-engines/) package.

#### Test call fails

Call to Echo Test Service can fail with error "call failed" when the user profiles are usually corrupt. Solution is to remove the profile and file and re-add your account in Skype as seen in Ubuntu Forums.

```
 # rm ~/.Skype/ -rf

```

#### No video with GSPCA webcams

Firstly, remove the Skype configuration directory. Otherwise preloading V4L libraries (see below) will not help, because old settings will override preloaded libraries. Note that all personal account settings will be lost.

```
rm -rf ~/.Skype

```

For i686, install [v4l-utils](https://www.archlinux.org/packages/?name=v4l-utils), userspace tools and conversion library for Video 4 Linux, and run Skype with

```
LD_PRELOAD=/usr/lib/libv4l/v4l1compat.so skype

```

to start Skype with v4l1 compatibility.

For x86_64, install [lib32-v4l-utils](https://www.archlinux.org/packages/?name=lib32-v4l-utils) from [multilib] repository and run Skype with

```
LD_PRELOAD=/usr/lib32/libv4l/v4l1compat.so skype

```

To make it running from DE menus and independent of Skype updates, you can add alias (e.g. in `~/.bashrc`):

```
alias skype='LD_PRELOAD=/usr/*libxx*/libv4l/v4l1compat.so skype'

```

where *libxx* should be edited as appropriate.

#### No video with Compiz

Try launching Skype setting an environment variable like this:

```
$ XLIB_SKIP_ARGB_VISUALS=1 skype

```

#### Skype does not use a GTK+ theme, even though other Qt apps do

Recent versions of Skype allow you to change the theme via the Options menu. However, selecting the GTK+ option may not work properly. This is probably because you do not have a 32-bit theme engine installed. Try to find the engine your theme uses in the multilib repository or the [AUR](/index.php/AUR "AUR"). If you have no idea which engine your theme is using, the easiest fix is to install [lib32-gtk-engines](https://aur.archlinux.org/packages/lib32-gtk-engines/). This does however contain quite a lot of packages, so the best would be to find and install only the needed package.

**Note:** You may not have to install [lib32-gtk-engines](https://aur.archlinux.org/packages/lib32-gtk-engines/). First try if the following steps work for you if you only install *lib32-gtk2* and a GTK+2 theme respectively. See also the [forums](https://bbs.archlinux.org/viewtopic.php?pid=1200975#p1200975).

Once installed, it will still not work unless you have a 32-bit version of GConf installed. You could build and install [lib32-gconf](https://www.archlinux.org/packages/?name=lib32-gconf) if desired, but there is an easier workaround. First, create or edit `~/.gtkrc-2.0` so that it contains the following line:

```
$ gtk-theme-name = "*My theme*"

```

Replace *My theme by* the name of your theme, but leave the quotes. Second, run Skype like this:

```
$ export GTK2_RC_FILES="/etc/gtk-2.0/gtkrc:$HOME/.gtkrc-2.0"
$ skype

```

The GTK+ theme should now appear correctly. You can make this permanent either by running Skype from a script containing the above 2 lines, or by exporting GTK2_RC_FILES in `~/.xprofile` or `~/.xinitrc`, depending on how you start X.

If you cannot change the theme in the Options menu, run Skype using the following command:

```
$ /usr/bin/skype --disable-cleanlooks -style GTK

```

If you wish menus within desktop environments to load Skype with a GTK+ theme by default then modify the 'Exec' line of `/usr/share/applications/skype.desktop` so that it reads:

```
$ Exec=/usr/bin/skype --disable-cleanlooks -style GTK

```

Similarly if you have set Skype to autostart then modify `~/.config/autostart/skype.desktop` in the same way.

#### No incoming video stream

If skype shows a black square for the video preview, but something else (like `xawtv -c /dev/video0`) shows video correctly, you might need to start Skype with:

```
export XLIB_SKIP_ARGB_VISUALS=1 && skype

```

Another possible workaround is to preload *v4l1compat.so*:

```
LD_PRELOAD=/usr/lib/libv4l/v4l1compat.so skype

```

A further alternative is:

```
cd /usr/lib/lib32/libv4l &&  LD_PRELOAD=v4l1compat.so skype;

```

#### Monster/low-octave "growling" distortion over mic

Some users with newer kernels are experiencing a monster-like growling distortion of their sound stream on the other end of Skype. This can be fixed by creating a dummy ALSA device or by removing `~/.Skype/shared.xml`. See [https://bbs.archlinux.org/viewtopic.php?pid=819500#p819500](https://bbs.archlinux.org/viewtopic.php?pid=819500#p819500) for more information.

#### Crackling/noisy sound (mainly using 64-bit OS)

##### Solution 1

With root privileges, edit the `/usr/bin/skype` script to add the `PULSE_LATENCY_MSEC` variable, changing this line:

```
exec "$LIBDIR/skype/skype" "$@"

```

to this:

```
PULSE_LATENCY_MSEC=60 exec "$LIBDIR/skype/skype" "$@"

```

##### Solution 2

Edit `/etc/pulse/default.pa` and change the following line

```
load-module module-udev-detect

```

to

```
load-module module-udev-detect tsched=0

```

See also: [PulseAudio/Troubleshooting#Glitches, skips or crackling](/index.php/PulseAudio/Troubleshooting#Glitches.2C_skips_or_crackling "PulseAudio/Troubleshooting").

#### Skype sounds stops media player or other sound sources

You can try commenting out the following modules in `/etc/pulse/default.pa`

```
#load-module module-role-cork

```

Finally you have to restart pulseaudio:

```
$ pulseaudio --kill
$ pulseaudio --start

```

If restarting does not solve the sound problem try to log out and log in again.

If that does not help, you can try changing flat-volumes to no in `/etc/pulse/daemon.conf`.

```
flat-volumes = no

```

If that still does not work, you can manually unload the module:

```
$ pactl unload-module module-role-cork

```

#### You are already signed in on this computer

If Skype is closed without the dc.lock file being deleted, it will fail to log back in.

To fix this, close Skype and run:

```
$ rm ~/.Skype/shared_dynco/dc.lock

```

#### Empty white screen window

If you get a white empty window when launching skype, try to autologin like this instead:

```
$ echo *username* *password* | skype --pipelogin

```

#### Skype doesn't output any sound after upgrading PulseAudio

Currently, Skype doesn't work PulseAudio 9.0 `enable-memfd` option, you have to make sure it's disabled in `/etc/pulse/daemon.conf`.

## Skype plugin for Pidgin

See [Pidgin#Skype plugin](/index.php/Pidgin#Skype_plugin "Pidgin").