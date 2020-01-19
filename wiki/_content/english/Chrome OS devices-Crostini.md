[Crostini](https://chromium.googlesource.com/chromiumos/docs/+/master/containers_and_vms.md) is Google's umbrella term for making Linux application support easy to use and integrating well with Chrome OS.

This article describes how to install Arch Linux on a Chromebook in a container (via Crostini), without needing to enable developer mode, allowing apps to run alongside other Chrome/Android apps.

Highlights:

*   Officially supported, don't need to enable developer mode - leaves ChromeOS secure, no need to flash a BIOS etc.
*   Better battery life - Battery life of Chrome with the functionality of Linux.
*   Audio & OpenGL are supported, but microphone and USB devices are still in progress.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduction](#Introduction)
    *   [1.1 Enabling Linux support](#Enabling_Linux_support)
    *   [1.2 Replacing the default Debian Linux container with Arch Linux](#Replacing_the_default_Debian_Linux_container_with_Arch_Linux)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 No network in container](#No_network_in_container)
    *   [2.2 App not opening in chrome OS (infinite spinner)](#App_not_opening_in_chrome_OS_(infinite_spinner))
    *   [2.3 Audio playback](#Audio_playback)
    *   [2.4 Video playback](#Video_playback)
    *   [2.5 GPU acceleration](#GPU_acceleration)
    *   [2.6 Fullscreen video, games and mouse capture](#Fullscreen_video,_games_and_mouse_capture)
*   [3 Useful links](#Useful_links)

## Introduction

### Enabling Linux support

Look for Linux under Settings and enable it. This installs a Debian Linux container that we will then replace with an Arch Linux container.

	*Settings > Linux > Enable*

Crostini is still rolling out to Chromebooks. If you don't see an option to enable Linux, you may need to switch to the beta or developer channel, if it has not rolled out to the stable channel for your laptop yet. This can be done via *Settings > About Chrome OS > Channel > Dev/Beta*.

### Replacing the default Debian Linux container with Arch Linux

The below instructions based on [https://www.reddit.com/r/Crostini/wiki/howto/run-arch-linux](https://www.reddit.com/r/Crostini/wiki/howto/run-arch-linux)

0\. Delete the Debian container (optional)

If you have no use for Debian anymore, you can save some storage space by destroying and recreating the termina vm (this is the easiest way to do it, simply destroying the container with `lxc destroy penguin` will leave the space unusable). Beware this will also delete any other containers you may have under termina.

```
vmc destroy termina
vmc start termina

```

1\. Install an Arch linux container

Open a new terminal in Chrome (Ctrl + Alt + T). Then connect to terminal and create an arch linux container:

```
vmc container termina arch [https://us.images.linuxcontainers.org](https://us.images.linuxcontainers.org) archlinux/current

```

Following error will be shown after completion:

[Template:"Error: routine at frontends/vmc.rs:403 `container setup user(vm name,user id hash,container name,username)` failed: timeout while waiting for signal"](/index.php?title=Template:%22Error:_routine_at_frontends/vmc.rs:403_%60container_setup_user(vm_name,user_id_hash,container_name,username)%60_failed:_timeout_while_waiting_for_signal%22&action=edit&redlink=1 "Template:"Error: routine at frontends/vmc.rs:403 `container setup user(vm name,user id hash,container name,username)` failed: timeout while waiting for signal" (page does not exist)")

This is expected behavior, proceed with following steps.

2\. Connect to termina vm and check if arch container is present (it may a few minutes to show on the list):

```
vsh termina
lxc list

```

3\. launch a bash shell on the arch container:

```
lxc exec arch -- bash

```

4\. Set password for the default user based on your gmail username on the container. By default the gmail user has no password set so we need to set it:

```
passwd $(grep 1000:1000 /etc/passwd|cut -d':' -f1)

```

You also might want to add [sudo](/index.php/Sudo "Sudo") and add the user to the wheel group.

```
pacman -S sudo
visudo

```

Uncomment this line:

```
# %wheel ALL=(ALL) ALL

```

Add your user to the wheel group to allow sudo commands

```
usermod -aG wheel $(grep 1000:1000 /etc/passwd|cut -d':' -f1)

```

Leave the container:

```
exit

```

5\. Login to the container using regular user account you just configured:

```
lxc console arch

```

6\. Verify networking in the container. Command

```
ip -4 a show dev eth0

```

should return non-empty output with assigned ip address. If it is not empty, please proceed to step 7, otherwise you are facing the issue described in [#No network in container](#No_network_in_container) troubleshooting section - follow the instructions listed there to address the issue.

7\. Install Crostini container tools, Wayland for GUI apps, XWayland for X11 apps.

[Install](/index.php/Install "Install") the [cros-container-guest-tools-git](https://aur.archlinux.org/packages/cros-container-guest-tools-git/) package. Additionally install [wayland](https://www.archlinux.org/packages/?name=wayland) and [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) to be able to use GUI tools.

8\. Enable and start the services (for Wayland GUI, X11 GUI, Wayland GUI low density and X11 GUI low density accordingly):

```
$ systemctl --user enable sommelier@0
$ systemctl --user enable sommelier-x@0
$ systemctl --user start sommelier@1
$ systemctl --user start sommelier-x@1

```

Make sure these services are running successfully by running:

```
systemctl --user status sommelier@0
systemctl --user status sommelier@1
systemctl --user status sommelier-x@0
systemctl --user status sommelier-x@1

```

Now, when apps are installed in Arch Linux, they will automatically show up and can be launched from ChromeOS.

9\. Replace the default Debian container with Arch Linux.

Exit from the container shell back to the termina shell pressing **<ctrl>+a q** (or just close existing and open new termina shell as shown in step 2). The default Debian container is named penguin. Renaming the "arch" container created above to it will cause chrome to launch Linux apps from the arch container. Skip the third line if you have already removed the Debian container.

```
lxc stop --force arch
lxc stop --force penguin
lxc rename penguin debian
lxc rename arch penguin
lxc start penguin

```

10\. Restart the Linux subsystem to apply the changes. After restart inside container shell

```
systemctl --failed
systemctl --user --failed

```

should both report **0 loaded units listed** and

```
ip -4 a show dev eth0

```

should report ip address assigned for container

## Troubleshooting

### No network in container

As was reported by multiple sources, systemd-networkd and systemd-resolved services in systemd-244.1 are not working properly for unprivileged LXC containers, which ends up in missing network connectivity inside the Crostini container. Proposed solution is completely disable systemd-networkd/systemd-resolved and perform network configuration by [dhclient](/index.php/Dhclient "Dhclient") service instead:

```
sudo dhcpcd eth0
sudo pacman -S dhclient
sudo systemctl disable systemd-networkd
sudo systemctl disable systemd-resolved
sudo unlink /etc/resolv.conf
sudo touch /etc/resolv.conf
sudo systemctl enable dhclient@eth0
sudo systemctl start dhclient@eth0

```

[NetworkManager](/index.php/NetworkManager "NetworkManager") and [dhcpcd](/index.php/Dhcpcd "Dhcpcd") also can be used to address the issue if you prefer them over the proposed solution.

### App not opening in chrome OS (infinite spinner)

I found that launching a console (lxc console penguin) session prevents apps from launching in Chrome OS. Launching results in an infinite spinner. In that case I have to stop and start the container to get the Chrome OS launcher working

```
lxc stop penguin
lxc start penguin

```

Instead of using an lxc console session, I use a regular Linux terminal GUI launched from ChromeOS that prevents this issue.

### Audio playback

Crostini support audio playback starting Chrome OS 74\. With [cros-container-guest-tools-git](https://aur.archlinux.org/packages/cros-container-guest-tools-git/) installed both ALSA and PulseAudio playback should work out-of-the-box. Audio input is not supported as of 08/21/2019.

### Video playback

[mpv](/index.php/Mpv "Mpv") can play videos using software rendering without any addition configuration, however this is CPU consuming and laggy experience for modern video codecs like H265\. For hardware accelerated playback GPU acceleration is required. Take into account, that GPU acceleration for Crostini is based on [Virgil 3D GPU project](https://virgil3d.github.io/), so no real GPU device pass-though is performed and hardware-specific APIs like VA-API or VPDAU are not available. However OpenGL acceleration can be used, i.e. this is example of mpv.conf config for [mpv] media player which enabled accelerated video and audio playback on Google Pixelbook starting Chrome OS 77:

```
vo=gpu
ao=alsa
```

### GPU acceleration

On Google Pixelbook GPU acceleration works with Arch out-of-the-box starting Chrome OS 77\. Also no flags need to be enabled on recent released of ChromeOS:

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

### Fullscreen video, games and mouse capture

Currently Crostini has limited support for mouse capture starting with Chrome OS 79 (Currently in the Dev channel). You must enable the flag chrome://flags/#exo-pointer-lock to get mouse capture. The closed issue relating to mouse capture is [https://bugs.chromium.org/p/chromium/issues/detail?id=927521](https://bugs.chromium.org/p/chromium/issues/detail?id=927521)

## Useful links

1.  [Running Custom Containers Under Chrome OS](https://chromium.googlesource.com/chromiumos/docs/+/master/containers_and_vms.md)
2.  [/r/Crostini](https://www.reddit.com/r/Crostini/)
3.  [Powerline Web Fonts for Chromebook](https://github.com/wernight/powerline-web-fonts)