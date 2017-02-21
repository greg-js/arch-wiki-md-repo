[DDE](http://www.deepin.org/?language=en) (Deepin Desktop Environment) is the default desktop environment originally created for the linux Deepin distribution.

## Contents

*   [1 Installation](#Installation)
*   [2 Launching Deepin Desktop Environment](#Launching_Deepin_Desktop_Environment)
    *   [2.1 Via a Display Manager](#Via_a_Display_Manager)
    *   [2.2 Using xinitrc](#Using_xinitrc)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Does not start](#Does_not_start)
    *   [3.2 No background after resuming from standby](#No_background_after_resuming_from_standby)
    *   [3.3 Open in terminal not work in deepin-file-manager](#Open_in_terminal_not_work_in_deepin-file-manager)
*   [4 Bug Reporting](#Bug_Reporting)

## Installation

To get a minimal desktop interface, you may start by [installing](/index.php/Installing "Installing") [deepin](https://www.archlinux.org/groups/x86_64/deepin/) group. This will pull all the basic components.

The [deepin-extra](https://www.archlinux.org/groups/x86_64/deepin-extra/) group contains some extra applications for a more complete desktop environment.

To be able to use the integrated network administration, the [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) package is required, and the `NetworkManager.service` must be [started and enabled](/index.php/Systemd#Using_units "Systemd").

## Launching Deepin Desktop Environment

### Via a Display Manager

To use the default DDE's lightdm greeter you have to modify the configuration file under the `[Seat:*]` section, to state:.

 `/etc/lightdm/lightdm.conf` 
```
[Seat:*]
...
greeter-session=lightdm-deepin-greeter
```

### Using xinitrc

*See the [xinitrc](/index.php/Xinitrc "Xinitrc") page for more information.*

 `~/.xinitrc` 
```
exec startdde

```

Execute `startx` or `xinit` to start DDE.

**Note:** If you want to start Xorg at boot, please read the [Start X at login](/index.php/Start_X_at_login "Start X at login") article.

## Troubleshooting

### Does not start

Type `startdde` in virtual console and see the output. If you see error with file mentioned `libgo.so.9` - ensure you have installed **the latest** [gcc-libs](https://www.archlinux.org/packages/?name=gcc-libs) package.

### No background after resuming from standby

Because of the way the NVIDIA driver stores its FBOs [[1]](https://devtalk.nvidia.com/default/topic/787748/linux/-nvidia340xx-archlinux64-gnome3-14-the-background-of-desktop-and-lockscreen-mess-after-resume-from-/post/4367179/#4367179), it happens that after resuming from standby the background suddenly disappears, leaving only a white screen with possibly some color noise on it. The bug appears to be fixed in GNOME upstream, but the Deepin desktop environment still has it.

A possible workaround would be restarting the window manager every time the computer resumes from suspension. A way to do that would be creating the following systemd service

 `/etc/systemd/system/resume@.service` 
```
[Unit]
Description=User resume actions
After=suspend.target

[Service]
User=%I
Type=simple
ExecStart=/usr/bin/deepin-wm-restart.sh

[Install]
WantedBy=suspend.target

```

That executes the following script

 `/usr/bin/deepin-wm-restart.sh` 
```
#!/bin/bash
export DISPLAY=:0
deepin-wm --replace

```

Once those two files are created in the correct directories, in order to enable the script it's sufficient to run these commands:

```
# chmod +x /usr/bin/deepin-wm-restart.sh
# systemctl enable resume@*user*
# systemctl start resume@*user* 

```

The first command makes the script you created executable, the second makes sure that the service always start at boot and the last one starts the service immediately so you can test the workaround without having to reboot the system.

### Open in terminal not work in deepin-file-manager

See [here](https://github.com/linuxdeepin/developer-center/issues/121). A solution for the moment:

```
# ln -s /usr/bin/deepin-terminal /usr/bin/x-terminal-emulator

```

## Bug Reporting

Any upstream or arch packaging related bugs should be reported [here](https://github.com/linuxdeepin/developer-center/issues). All deepin developers will see the bug reports and solve them as soon as possible.