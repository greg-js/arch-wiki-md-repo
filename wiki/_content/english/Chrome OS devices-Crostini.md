This article describes how to install Arch Linux on a Chromebook in a container (via Crostini), without needing to enable developer mode, allowing apps to run alongside other Chrome/Android apps.

	Advantages

*   Don't need to enable developer mode - Officially supported, leaves ChromeOS secure, no need to flash a BIOS etc.
*   Better battery life - Battery life of Chrome with the functionality of Linux.
*   Access to Android apps, play store etc.

	Disadvantages

*   No OpenGL support yet (24-11-2018)
*   No sound support yet (24-11-2018)

## Contents

*   [1 Introduction](#Introduction)
    *   [1.1 Enabling Linux support](#Enabling_Linux_support)
    *   [1.2 Replacing the default Debian Linux container with Arch Linux](#Replacing_the_default_Debian_Linux_container_with_Arch_Linux)
*   [2 Known issues](#Known_issues)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Network not working on Pixelbook](#Network_not_working_on_Pixelbook)
    *   [3.2 DNS resolution not working](#DNS_resolution_not_working)
    *   [3.3 App not opening in chrome OS (infinite spinner)](#App_not_opening_in_chrome_OS_(infinite_spinner))

## Introduction

### Enabling Linux support

Look for Linux under Settings and enable it. This installs a Debian Linux container that we will then replace with an Arch Linux container.

	*Settings > Linux > Enable*

Crostini is still rolling out to Chromebooks. If you don't see an option to enable Linux, you may need to switch to the beta or developer channel, if it has not rolled out to the stable channel for your laptop yet. This can be done via *Settings > About Chrome OS > Channel > Dev/Beta*.

### Replacing the default Debian Linux container with Arch Linux

The below instructions were taken from [https://www.reddit.com/r/Crostini/wiki/howto/run-arch-linux](https://www.reddit.com/r/Crostini/wiki/howto/run-arch-linux)

1\. Install an Arch linux container

Open a new terminal in Chrome (Alt + Shift + T). Then connect to terminal and create an arch linux container:

```
   vsh termina
   run_container.sh --container_name arch --user <gmail username> --lxd_image archlinux/current --lxd_remote [https://us.images.linuxcontainers.org/](https://us.images.linuxcontainers.org/)

```

The <gmail username> here is the same user you are logged in to your Chromebooks as, without the @gmail.com. eg. foobar@gmail.com will set --user foobar. Apps launched from the ChromeOS launcher run under this user.

2\. Replace the default Debian container with Arch Linux.

The default Debian container is named penguin. Renaming the "arch" container created above to it will cause chrome to launch Linux apps from the arch container.

```
   lxc stop arch
   lxc stop penguin
   lxc rename penguin debian
   lxc rename arch penguin

```

3\. Install Crostini container tools, Wayland for GUI apps, XWayland for X11 apps.

First open a console session the the Arch Linux container.

```
   lxc console penguin

```

I installed an AUR helper to install Crostini tools:

```
   $ pacman -S base-devel
   $ git clone [https://aur.archlinux.org/yay.git](https://aur.archlinux.org/yay.git)
   $ cd yay
   $ makepkg -si

```

Then used it to install Crostini container tools, and enable the userland service for GUI tools to work:

```
   $ sudo pacman -S wayland xwayland
   $ yay -S cros-container-guest-tools-git

```

At present (11-24-2018) xkeyboard-config 2.24 break the sommelier-x service. Workaround is to comment out two lines starting with "<i372>" and "<i374>" in /usr/share/X11/xkb/keycodes/evdev. Then enable and start the services.

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

## Known issues

Tested, working (2018-11-24)

*   Pycharm

Tested, not working (2018-11-24 - no hardware acceleration, audio)

*   Gnome (No OpenGL)
*   glxgears (No OpenGL)
*   Audacity (No recording devices)

## Troubleshooting

### Network not working on Pixelbook

[https://tedyin.com/posts/archlinux-on-pixelbook/](https://tedyin.com/posts/archlinux-on-pixelbook/) reports that the below setting needs to be set to get the network working on the pixelbook. Make sure to restart your container after you set it.

```
 lxc profile set default security.syscalls.blacklist "keyctl errno 38"

```

### DNS resolution not working

DNS resolution stopped working in the container after my install. To get it working again I had to create [/etc/resolv.conf](/index.php//etc/resolv.conf "/etc/resolv.conf").

### App not opening in chrome OS (infinite spinner)

I found that launching a console (lxc console penguin) session prevents apps from launching in Chrome OS. Launching results in an infinite spinner. In that case I have to stop and start the container to get the Chrome OS launcher working

```
  lxc stop penguin
  lxc start penguin

```

Instead of using an lxc console session, I use a regular Linux terminal GUI launched from ChomeOS that prevents this issue.