[Crostini](https://chromium.googlesource.com/chromiumos/docs/+/master/containers_and_vms.md) is Google's umbrella term for making Linux application support easy to use and integrating well with Chrome OS.

This article describes how to install Arch Linux on a Chromebook in a container (via Crostini), without needing to enable developer mode, allowing apps to run alongside other Chrome/Android apps.

Highlights:

*   Officially supported, don't need to enable developer mode - leaves ChromeOS secure, no need to flash a BIOS etc.
*   Better battery life - Battery life of Chrome with the functionality of Linux.
*   Access to Android apps, play store etc.
*   Audio & OpenGL are supported, but microphone and USB devices are still in progress.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduction](#Introduction)
    *   [1.1 Enabling Linux support](#Enabling_Linux_support)
    *   [1.2 Replacing the default Debian Linux container with Arch Linux](#Replacing_the_default_Debian_Linux_container_with_Arch_Linux)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Network not working on Pixelbook](#Network_not_working_on_Pixelbook)
    *   [2.2 DNS resolution not working](#DNS_resolution_not_working)
    *   [2.3 App not opening in chrome OS (infinite spinner)](#App_not_opening_in_chrome_OS_(infinite_spinner))
    *   [2.4 Audio playback](#Audio_playback)
    *   [2.5 Video playback](#Video_playback)
    *   [2.6 GPU acceleration](#GPU_acceleration)
    *   [2.7 Fullscreen video, games and mouse capture don't work correctly](#Fullscreen_video,_games_and_mouse_capture_don't_work_correctly)
    *   [2.8 SystemD status showed as degraded](#SystemD_status_showed_as_degraded)
*   [3 Useful links](#Useful_links)

## Introduction

### Enabling Linux support

Look for Linux under Settings and enable it. This installs a Debian Linux container that we will then replace with an Arch Linux container.

	*Settings > Linux > Enable*

Crostini is still rolling out to Chromebooks. If you don't see an option to enable Linux, you may need to switch to the beta or developer channel, if it has not rolled out to the stable channel for your laptop yet. This can be done via *Settings > About Chrome OS > Channel > Dev/Beta*.

### Replacing the default Debian Linux container with Arch Linux

The below instructions were taken from [https://www.reddit.com/r/Crostini/wiki/howto/run-arch-linux](https://www.reddit.com/r/Crostini/wiki/howto/run-arch-linux)

1\. Install an Arch linux container

Open a new terminal in Chrome (Ctrl + Alt + T). Then connect to terminal and create an arch linux container:

```
vsh termina
run_container.sh --container_name arch --user <gmail username> --lxd_image archlinux/current --lxd_remote [https://us.images.linuxcontainers.org/](https://us.images.linuxcontainers.org/)

```

The <gmail username> here is the same user you are logged in to your Chromebooks as, without the @gmail.com and dots. eg. foo.bar@gmail.com will set --user foobar. Apps launched from the ChromeOS launcher run under this user.

2\. Replace the default Debian container with Arch Linux.

The default Debian container is named penguin. Renaming the "arch" container created above to it will cause chrome to launch Linux apps from the arch container.

```
lxc stop arch
lxc stop penguin
lxc rename penguin debian
lxc rename arch penguin

```

3\. Set password for gmail username

By default the gmail user has no password set. Use lxc exec to set a password:

```
lxc exec penguin -- bash

```

You also might want to add [sudo](/index.php/Sudo "Sudo") and add the user to sudoers.

4\. Install Crostini container tools, Wayland for GUI apps, XWayland for X11 apps.

First open a console session the the Arch Linux container.

```
lxc console penguin

```

[Install](/index.php/Install "Install") the [cros-container-guest-tools-git](https://aur.archlinux.org/packages/cros-container-guest-tools-git/) package. Additionally install [wayland](https://www.archlinux.org/packages/?name=wayland) and [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) to be able to use GUI tools. Then enable and start the services.

```
$ systemctl --user enable sommelier@0      # For Wayland GUI apps
$ systemctl --user enable sommelier-x@0    # For X11 GUI apps
$ systemctl --user start sommelier@0      # For Wayland GUI apps
$ systemctl --user start sommelier-x@0    # For X11 GUI apps

```

Make sure these services are running successfully by running:

```
$ systemctl --user status sommelier@0
$ systemctl --user status sommelier-x@0

```

Now, when apps are installed in Arch Linux, they will automatically show up and can be launched from ChromeOS. Note that while GUI apps work, rendering is still software, with no OpenGL support yet.

## Troubleshooting

### Network not working on Pixelbook

[https://tedyin.com/posts/archlinux-on-pixelbook/](https://tedyin.com/posts/archlinux-on-pixelbook/) reports that the below setting needs to be set to get the network working on the pixelbook. Make sure to restart your container after you set it.

```
lxc profile set default security.syscalls.blacklist "keyctl errno 38"

```

### DNS resolution not working

DNS resolution stopped working in the container after my install. To get it working again I had to create [/etc/resolv.conf](/index.php//etc/resolv.conf "/etc/resolv.conf").

As of Jan 2019, my container wasn't able to resolve ".org" DNS, I had to modify [nsswitch.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nsswitch.conf.5) (only the hosts line).

```
 hosts: files dns

```

### App not opening in chrome OS (infinite spinner)

I found that launching a console (lxc console penguin) session prevents apps from launching in Chrome OS. Launching results in an infinite spinner. In that case I have to stop and start the container to get the Chrome OS launcher working

```
lxc stop penguin
lxc start penguin

```

Instead of using an lxc console session, I use a regular Linux terminal GUI launched from ChomeOS that prevents this issue.

### Audio playback

Crostini support audio playback starting Chrome OS 74\. With [cros-container-guest-tools-git](https://aur.archlinux.org/packages/cros-container-guest-tools-git/) installed both ALSA and PulseAudio playback should work out-of-the-box. Audio input is not supported as of 08/21/2019.

### Video playback

[mpv](/index.php/Mpv "Mpv") can play videos using software rendering without any addition configuration, however this is CPU consuming and laggy experience for modern video codecs like H265\. For hardware accelerated playback GPU acceleration is required. Take into account, that GPU acceleration for Crostini is based on [Virgil 3D GPU project](https://virgil3d.github.io/), so no real GPU device pass-though is performed and hardware-specific APIs like VA-API or VPDAU are not available. However OpenGL acceleration can be used, i.e. this is example of `mpv.conf` config for [mpv] media player which enabled accelerated video and audio playback on Google Pixelbook starting Chrome OS 77:

```
vo=gpu
ao=alsa
```

### GPU acceleration

Make sure GPU acceleration is enabled for Crostini using chrome://flags/#crostini-gpu-support flag. On Google Pixelbook GPU acceleration works with Arch out-of-the-box starting Chrome OS 77:

 `$ glxinfo -B` 
```
name of display: :0
display: :0  screen: 0
direct rendering: Yes
Extended renderer info (GLX_MESA_query_renderer):
    Vendor: Red Hat (0x1af4)
    Device: virgl (0x1010)
    Version: 19.1.4
--> Accelerated: yes <--
    Video memory: 0MB
    Unified memory: no
    Preferred profile: core (0x1)
    Max core profile version: 4.3
    Max compat profile version: 3.1
    Max GLES1 profile version: 1.1
    Max GLES[23] profile version: 3.2
OpenGL vendor string: Red Hat
OpenGL renderer string: virgl
OpenGL core profile version string: 4.3 (Core Profile) Mesa 19.1.4
OpenGL core profile shading language version string: 4.30
OpenGL core profile context flags: (none)
OpenGL core profile profile mask: core profile

OpenGL version string: 3.1 Mesa 19.1.4
OpenGL shading language version string: 1.40
OpenGL context flags: (none)

OpenGL ES profile version string: OpenGL ES 3.2 Mesa 19.1.4
OpenGL ES profile shading language version string: OpenGL ES GLSL ES 3.20
```

### Fullscreen video, games and mouse capture don't work correctly

Currently Crostini doesn't allow linux apps to be completely fullscreen and mouse capture doesn't work correctly. So playing most Steam games is infeasable.

### SystemD status showed as degraded

Issue is caused by systemd-udev-trigger.service unit, which fails due to missing write access to the /sys. It is safe to mask it:

```
sudo systemctl mask systemd-udev-trigger.service

```

and restart the Linux subsystem. After restart

```
systemctl status

```

should report **State: running**.

## Useful links

1.  [Running Custom Containers Under Chrome OS](https://chromium.googlesource.com/chromiumos/docs/+/master/containers_and_vms.md)
2.  [How to install Arch Linux with Jupyter Notebook](https://www.reddit.com/r/Crostini/wiki/howto/run-arch-linux)
3.  [Powerline Web Fonts for Chromebook](https://github.com/wernight/powerline-web-fonts)
4.  [Pixelbook Setup](https://gist.github.com/cassiozen/93da03b91c8dae7c990e58e3e6b90615)
5.  [/r/Crostini](https://www.reddit.com/r/Crostini/)