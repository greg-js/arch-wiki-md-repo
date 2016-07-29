[Blueman](https://github.com/blueman-project/blueman) is a full featured Bluetooth manager written in [GTK+](/index.php/GTK%2B "GTK+"). See the project page on [Github](https://github.com/blueman-project/blueman).

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Autostarting](#Autostarting)
    *   [2.2 Permissions](#Permissions)
    *   [2.3 Mounting Bluetooth devices](#Mounting_Bluetooth_devices)
    *   [2.4 Blueman and PulseAudio](#Blueman_and_PulseAudio)
*   [3 Configuration](#Configuration)
    *   [3.1 Disable auto power-on](#Disable_auto_power-on)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Blueman applet does not start](#Blueman_applet_does_not_start)
    *   [4.2 No adapters detected](#No_adapters_detected)
    *   [4.3 Can't receive files](#Can.27t_receive_files)
*   [5 See also](#See_also)

## Installation

Install either [blueman](https://www.archlinux.org/packages/?name=blueman) or [blueman-git](https://aur.archlinux.org/packages/blueman-git/) (the development version).

Be sure to enable the [Bluetooth](/index.php/Bluetooth "Bluetooth") daemon and start Blueman with `blueman-applet`. A graphical settings panel can be launched with `blueman-manager`.

## Usage

### Autostarting

The following autostart file should have been created: `/etc/xdg/autostart/blueman.desktop`. This means that Blueman should be autostarted with most desktop environments without manual intervention. See the article for your desktop environment or window manager as well as the [Autostarting](/index.php/Autostarting "Autostarting") article for further information on autostarting.

### Permissions

To receive files remember to right click on the *Blueman tray icon > Local Services > Transfer > File Receiving (Object Push)* and tick the *Accept files from trusted devices* box.

To be able to manage devices, you might need to add your user to the `lp` group, else you might receive the following error when connecting to a device: `DBusFailedError: No such file or directory`. This is because the user needs to be authorized to communicate with the bluetooth daemon via [D-Bus](/index.php/D-Bus "D-Bus") - the `lp` group is specified in `/etc/dbus-1/system.d/bluetooth.conf`. For information on adding a user to a group, see [Users and groups#Other examples of user management](/index.php/Users_and_groups#Other_examples_of_user_management "Users and groups").

### Mounting Bluetooth devices

The instructions below describe a method for using different file managers with Blueman. The examples in this section focus on [Thunar](/index.php/Thunar "Thunar"). If you are using a different file manager, substitute *thunar* with the name of the file manager you are using.

 `obex_thunar.sh` 
```
#!/bin/bash
fusermount -u ~/bluetooth
obexfs -b $1 ~/bluetooth
thunar ~/bluetooth

```

Now you will need to move the script to an appropriate location (e.g., `/usr/local/bin`). After that, mark it as executable:

```
# chmod +x /usr/local/bin/obex_thunar.sh

```

The last step is to change the line in *Blueman tray icon > Local Services > Transfer > Advanced* to `obex_thunar.sh %d`.

**Tip:** If you do not want to create a script, you could just replace this command: `nautilus --browse obex://` with this one: `thunar obex://` in *Local Services > Transfer > Advanced*

### Blueman and PulseAudio

Users who want to use [PulseAudio](/index.php/PulseAudio "PulseAudio") with a Bluetooth headset, in addition to [installing](/index.php/Install "Install") [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth), may want to activate the PulseAudio plugin of Blueman. This automatically loads PulseAudio Bluetooth module after audio device is connected and plays all audio through the Bluetooth headset. For more information see [Bluetooth headset](/index.php/Bluetooth_headset "Bluetooth headset")

## Configuration

Configuration is done through [dconf](https://www.archlinux.org/packages/?name=dconf) (or gsettings or [dconf-editor](https://www.archlinux.org/packages/?name=dconf-editor)).

### Disable auto power-on

Blueman automatically enables Bluetooth adapter () when certain events (on boot, laptop lid is opened, ...) occur. This can be disabled with the `auto-power-on` in `org.blueman.plugins.powermanager`:

```
$ gsettings set org.blueman.plugins.powermanager auto-power-on false

```

## Troubleshooting

### Blueman applet does not start

If blueman-applet fails to start, try removing the entire `/var/lib/bluetooth` directory and restarting the machine (or just the dbus and bluetooth services).

```
# rm -rf /var/lib/bluetooth
$ systemctl reboot

```

If you see a notification saying `Incoming file over Bluetooth` then this means that the device isn't marked as trusted. Mark it as trusted and try sending the file again.

### No adapters detected

If your Bluetooth applet or manager doesn't show or detect any Bluetooth adapter, you might be missing [rfkill](https://www.archlinux.org/packages/?name=rfkill). Restart might be required.

### Can't receive files

If you can't send or receive files and you encounter a python-dbus-exception error similar or exactly like `process org.bluez.obex exited with status 1` then it is advised to start the obexd-service manually from `/usr/lib/bluetooth/obexd` and see if that helps. Since the default permissions assume 755 it is possible to start the daemon from a user-account and/or create an autostarter.

Should the error persist or another occur then try using [obexftp](https://www.archlinux.org/packages/?name=obexftp) for file transfers instead, see [Bluetooth#ObexFTP transfers](/index.php/Bluetooth#ObexFTP_transfers "Bluetooth").

## See also

*   [Blueman development](https://github.com/blueman-project/blueman), on GitHub