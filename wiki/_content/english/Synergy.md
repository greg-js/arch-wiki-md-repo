[Synergy](http://synergy-project.org/) lets you easily share a single mouse and keyboard between multiple computers (even with different operating systems) without the need for special hardware. It is intended for users with multiple computers on their desk since each system uses its own monitor(s).

Redirecting the mouse and keyboard is as simple as moving the mouse off the edge of your screen. Synergy also merges the clipboards of all the systems into one, allowing cut-and-paste between systems. Furthermore, it synchronizes screen savers so they all start and stop together and, if screen locking is enabled, only one screen requires a password to unlock them all.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Arch Linux](#Arch_Linux)
    *   [1.2 Windows and macOS](#Windows_and_macOS)
*   [2 Pre-configuration](#Pre-configuration)
*   [3 Server configuration](#Server_configuration)
    *   [3.1 Arch Linux](#Arch_Linux_2)
        *   [3.1.1 Use encryption](#Use_encryption)
    *   [3.2 Windows](#Windows)
    *   [3.3 macOS](#macOS)
    *   [3.4 Configuration examples](#Configuration_examples)
*   [4 Clients configuration](#Clients_configuration)
    *   [4.1 Arch Linux](#Arch_Linux_3)
        *   [4.1.1 Use encryption](#Use_encryption_2)
        *   [4.1.2 Autostart](#Autostart)
    *   [4.2 Windows](#Windows_2)
    *   [4.3 macOS](#macOS_2)
*   [5 Known issues](#Known_issues)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Keyboard AltGr](#Keyboard_AltGr)
    *   [6.2 Keyboard repeat](#Keyboard_repeat)
    *   [6.3 Keyboard mapping](#Keyboard_mapping)
    *   [6.4 No cursor in Gnome](#No_cursor_in_Gnome)
    *   [6.5 Client is returning "failed to verify server certificate fingerprint"](#Client_is_returning_.22failed_to_verify_server_certificate_fingerprint.22)
    *   [6.6 Scroll Lock LED does not light](#Scroll_Lock_LED_does_not_light)
    *   [6.7 Additional mouse buttons do not work in client](#Additional_mouse_buttons_do_not_work_in_client)
*   [7 External links](#External_links)

## Installation

### Arch Linux

You can [install](/index.php/Install "Install") the [synergy](https://www.archlinux.org/packages/?name=synergy) package.

### Windows and macOS

[Download](https://symless.com/synergy/) and run the newest installer from the official website. The official version is paid, although you may compile and run your own builds for free using [sources on GitHub](https://github.com/symless/synergy-core).

## Pre-configuration

First determine the IP addresses and [host names](/index.php/Network_configuration#Set_the_hostname "Network configuration") for each machine and make sure each has a correct hosts file.

*   Arch Linux - `/etc/hosts`
*   Windows - `C:\WINDOWS\system32\drivers\etc\hosts`
*   macOS - [How to Add Hosts to Local Hosts File](http://support.apple.com/kb/TA27291).

 `/etc/hosts` 
```
10.10.66.1        archserver.localdomain       archserver
10.10.66.100      archleft.localdomain         archleft
10.10.66.105      archright.localdomain        archright
```

**Note:** Check that the clients can reach the server.

## Server configuration

In synergy, the computer with keyboard and mouse you want to share is called server. See [Synergy Configuration File Format](https://github.com/symless/synergy-core/wiki/Text-Config) for a detailed description of all available sections and options.

### Arch Linux

The configuration file for Arch Linux is `/etc/synergy.conf`. If it does not exist, create it using `/etc/synergy.conf.example`, whose comments should give you enough information for a basic configuration; if you need further reference, read the guide mentioned above.

**Tip:** You may also use [quicksynergy](https://aur.archlinux.org/packages/quicksynergy/) from the [AUR](/index.php/AUR "AUR") which provide a GUI to simplify the configuration process.

**Tip:** Make sure the server port is not blocked. By default, synergy uses port 24800.

If you experience problems and you wish to run the server in the foreground, you can run the following command instead:

```
# synergys -f

```

The synergy server process needs to attach to your user's X session, which means it needs to run as your user. [Enable](/index.php/Enable "Enable") `synergys.service` with `--user` option.

**Tip:** You can enable `synergys.socket` to start the server when a client tries to connect instead. This is useful when the service can't connect to an X server on boot.

#### Use encryption

To generate a certificate and fingerprint for the server to use.

```
$ mkdir -p ~/.synergy/SSL/Fingerprints
$ openssl req -x509 -nodes -days 365 -subj /CN=Synergy -newkey rsa:1024 -keyout ~/.synergy/SSL/Synergy.pem -out ~/.synergy/SSL/Synergy.pem
$ openssl x509 -fingerprint -sha1 -noout -in ~/.synergy/SSL/Synergy.pem > ~/.synergy/SSL/Fingerprints/Local.txt
$ sed -e "s/.*=//" -i ~/.synergy/SSL/Fingerprints/Local.txt

```

To activate the SSL plugin, add the `--enable-crypto` option.

*   Starting from the command line:

```
$ synergys --enable-crypto

```

*   Starting with systemd:

```
$ systemctl --user start synergys

```

### Windows

1.  Open the Synergy program
2.  Select the option *Server (share this computer's mouse and keyboard)*
3.  Select *Configure interactively*
4.  Click the *Configure Server...* button
5.  This opens a window in which you can add screens depending on how many computers/screens you have: just drag the screen icon in the top-right corner to the screens area, and double-click it to edit its settings
6.  Click *OK* to close the screens window when you are ready, then click on *Start* to start the server

On Windows, configuration is saved by default in a `synergy.sgc` file, but its name and location can of course be changed at pleasure.

If you want to start the Synergy server everytime Windows starts, you have to launch the program **as administrator**, then go to *Edit -> Services* and select *Install* in the *Server* section; note that at the following reboot Synergy will indeed automatically start, but the tray icon will not display automatically (at least for version 1.4.2 beta on Windows 7). To uninstall the service, do the same thing but obviously select *Uninstall*.

If you want to start the server from the command-line, here is a Windows command you can place in a `.bat` file or just run from `cmd.exe`:

```
C:\Program Files\Synergy+\bin\synergys.exe  -f --debug ERROR --name left --log c:\windows\synergy.log -c C:/windows/synergy.sgc --address 10.66.66.2:24800

```

### macOS

macOS has a similar configuration as Unix: check [the official documentation](https://github.com/symless/synergy-core/wiki/Developer) for more information.

### Configuration examples

This is an example for a basic 3-computers setup:

 `/etc/synergy.conf` 
```
section: screens
	server-fire:
	archright-fire:
	archleft-fire:
end

section: links
	archleft-fire:
		right = server-fire
	server-fire:
		right = archright-fire
		left = archleft-fire
	archright-fire:
		left = server-fire
end

```

This should be the example bundled with the Arch Linux package:

 `/etc/synergy.conf` 
```
section: screens
        # three hosts named:  moe, larry, and curly
        moe:
        larry:
        curly:
end

section: links
        # larry is to the right of moe and curly is above moe
        moe:
                right = larry
                up    = curly

        # moe is to the left of larry and curly is above larry.
        # note that curly is above both moe and larry and moe
        # and larry have a symmetric connection (they're in
        # opposite directions of each other).
        larry:
                left  = moe
                up    = curly

        # larry is below curly.  if you move up from moe and then
        # down, you'll end up on larry.
        curly:
                down  = larry
end

section: aliases
        # curly is also known as shemp
        curly:
                shemp
end
```

The following is a more customized example:

 `synergy.sgc` 
```
section: screens
	leftpc:
		halfDuplexCapsLock = false
		halfDuplexNumLock = false
		halfDuplexScrollLock = false
		xtestIsXineramaUnaware = false
		switchCorners = none +top-left +top-right +bottom-left +bottom-right 
		switchCornerSize = 0
	rightpc:
		halfDuplexCapsLock = false
		halfDuplexNumLock = false
		halfDuplexScrollLock = false
		xtestIsXineramaUnaware = false
		switchCorners = none +top-left +top-right +bottom-left +bottom-right 
		switchCornerSize = 0
end

section: aliases
leftpc:
10.66.66.2
rightpc:
10.66.66.1
end

section: links
	leftpc:
		right = rightpc
	rightpc:
		left = leftpc
end

section: options
	heartbeat = 1000
	relativeMouseMoves = false
	screenSaverSync = false
	win32KeepForeground = false
	switchCorners = none +top-left +top-right +bottom-left +bottom-right 
	switchCornerSize = 4
end
```

## Clients configuration

**Note:** This assumes a server has been set up and configured **properly**. Make sure the server is already configured to accept the client(s) before continuing.

**Tip:** You don't need to setup a client on the host server as the server includes one.

### Arch Linux

In a console window, type:

```
$ synergyc server-host-name

```

Or, to run synergy in the foreground:

```
$ synergyc -f server-host-name

```

Here, `server-host-name` is the host name of the server.

#### Use encryption

If you use the synergy command line client, copy the file containing the fingerprint <a class="mw-selflink selflink">`~/.synergy/SSL/Fingerprints/Local.txt`</a> from the server into the clients home directory <a class="mw-selflink selflink">`~/.synergy/SSL/Fingerprints/TrustedServers.txt`</a>. To start the synergy command line client with encryption, type:

```
$ synergyc --enable-crypto

```

**Note:** There is an open issue with the GUI client of synergy (see [https://github.com/symless/synergy-core/issues/4737](https://github.com/symless/synergy-core/issues/4737)). The dialog to prompt for confirmation of the server's fingerprint, only pops up if the logging level is set to INFO, DEBUG or DEBUG2.

#### Autostart

There exist several ways to automatically start the Synergy client, and they are actually the same that can be used for every other application.

**Note:** In all of the following examples, you always have to substitute `server-host-name` with the real server host name.

*   You can add the next line to your [`~/.xinitrc`](/index.php/Xinitrc "Xinitrc"):

 `~/.xinitrc` 
```
...

#replace server-host-name with the real name
synergyc server-host-name

```

The following is an alternative:

 `~/.xinitrc` 
```
XINIT_CMD='/usr/bin/synergyc -d FATAL -n galileo-fire 10.66.66.2:24800'
/usr/bin/pgrep -lxf "$XINIT_CMD" || ( ( $XINIT_CMD ) & )

```

*   Otherwise, if you are using a [display manager](/index.php/Display_manager "Display manager") ([GDM](/index.php/GDM "GDM"), [SDDM](/index.php/SDDM "SDDM"), ...), or a stand-alone [window manager](/index.php/Window_manager "Window manager") (Openbox, ...), you could exploit its start-up script and add the following:

```
synergyc server-host-name

```

*   To start the Synergy client with systemd, create a service file:

 `~/.config/systemd/user/synergyc.service` 
```
[Unit]
Description=Synergy Client Daemon
After=network.target

[Service]
ExecStart=/usr/bin/synergyc --no-daemon *server-name*
Restart=always
RestartSec=3

[Install]
WantedBy=default.target
```

To start the service for your user:

```
$ systemctl --user start synergyc

```

To start the service at login for your user:

```
$ systemctl --user enable synergyc

```

Automatically starting Synergy is also documented in its [official reference page](https://github.com/symless/synergy-core/wiki/Startup).

### Windows

After installation, open the Synergy program, select the option *Client (use another computer's keyboard and mouse)* and type the host name of the server computer in the text box, then click *Start* to start the client.

**Note:** You can use the tray icon to stop the client.

If you want to start the Synergy client every time Windows starts, you have to launch the program **as an administrator**, then go to *Edit -> Services* and select *Install* in the *Client* section.

If you want to start the client from the command-line, here is a Windows command you can place in a `.bat` file or just run from `cmd.exe`. This points to a configuration file in `C:\synergy.sgc` and runs in the background like a service.

 `START /MIN /D"C:\Program Files\Synergy+\bin" synergys.exe -d ERROR -n m6300 -c C:\synergy.sgc -a 10.66.66.2:24800` 

### macOS

Locate the synergyc program in the synergyc folder and drag it onto the terminal window: the full path will appear in the terminal. Now append the host name of the server, so that the complete command will look like this:

 `/path/to/synergyc/synergyc server-host-name` 

Then press `Enter`.

## Known issues

If Arch is being used as a client in a Synergy installation, the server may not be able to wake the client monitor. There are some workarounds, such as executing the following via [SSH](/index.php/SSH "SSH"), if ACPI is enabled (see: [Modifying DPMS and ScreenSaver settings with xset](/index.php/Display_Power_Management_Signaling#Modifying_DPMS_and_screensaver_settings_using_xset "Display Power Management Signaling")):

 `# xset dpms force on` 

## Troubleshooting

The official documentation has a [FAQ](https://github.com/symless/synergy-core/wiki/User-FAQ) and also a [troubleshooting page](https://github.com/symless/synergy-core/wiki/User-Guide#Troubleshooting).

### Keyboard AltGr

If you encounter problems with AltGr add

```
altgr = alt       #1.8.2
altgr = shift     #v1.8.3 and higher

```

on the screen/client section in /etc/synergys.conf.

### Keyboard repeat

If you experience problems with your keyboard repeat on the client machine (Linux host), simply type:

 `# /usr/bin/xset r on` 

in any console.

### Keyboard mapping

If you experience problems with the keyboard mapping when using the server's keyboard in a client window (e.g a terminal) then re-setting the X key map after starting synergyc may help. The following command sets the keymap to its current value:

```
# setxkbmap $(setxkbmap -query | grep "^layout:" | awk -F ": *" '{print $2}')

```

### No cursor in Gnome

When [GNOME](/index.php/GNOME "GNOME") doesn't detect a mouse, it will default to touchscreen mode and hide the cursor. To enable run:

```
# dconf write /org/gnome/settings-daemon/plugins/cursor/active false

```

This can be added to an init script or systemd unit:

```
 ExecStartPost=dconf write /org/gnome/settings-daemon/plugins/cursor/active false

```

### Client is returning "failed to verify server certificate fingerprint"

You need to copy the content of server's "~/.synergy/SSL/Fingerprints/Local.txt" into client's "~/.synergy/SSL/Fingerprints/TrustedServers.txt".

### Scroll Lock LED does not light

When using Scroll Lock to lock to a client (or to enter relative mouse move mode), you may run into an issue with your keyboard's Scroll Lock LED not lighting. This can be solved by binding the `Scroll_Lock` key to an empty modifier key.

First, find an empty modifier. In this case, mod3 is available:

```
 $ xmodmap
 xmodmap:  up to 4 keys per modifier, (keycodes in parentheses):

 shift       Shift_L (0x32),  Shift_R (0x3e)
 lock        Caps_Lock (0x42)
 control     Control_L (0x25),  Control_R (0x69)
 mod1        Alt_L (0x40),  Alt_R (0x6c),  Meta_L (0xcd)
 mod2        Num_Lock (0x4d)
 mod3
 mod4        Super_L (0x85),  Super_R (0x86),  Super_L (0xce),  Hyper_L (0xcf)
 mod5        ISO_Level3_Shift (0x5c),  Mode_switch (0xcb)

```

Then, add the new mapping.

```
 $ xmodmap -e 'add mod3 = Scroll_Lock'
 $ "echo "add mod3 = Scroll_Lock" >> ~/.Xmodmap

```

See [Xmodmap#Activating the custom table](/index.php/Xmodmap#Activating_the_custom_table "Xmodmap") to have `~/.Xmodmap` loaded on login.

After making this change, test the LED and screen locking. If you find that you need to press Scroll Lock twice to lock screens, enable `halfDuplexScrollLock` on all screens in `section: screens`.

### Additional mouse buttons do not work in client

If you find that additional mouse buttons (i.e. Mouse4/Mouse5) do not translate to a client, try adding the following to `section: options`:

```
 mousebutton(6) = mousebutton(4)
 mousebutton(7) = mousebutton(5)

```

This will re-map the mouse keys to the proper number. If that does not fix the problem, remove the configuration, stop Synergy, and start it in the foreground with debug logging enabled:

```
 $ synergys -f -d DEBUG1

```

Then, move your cursor to the screen of the client with the issue. Click the non-functioning keys, and watch for log entries like this:

```
 [2017-09-30T14:56:45] DEBUG1: onMouseDown id=6
 ...
 [2017-09-30T14:56:46] DEBUG1: onMouseUp id=6

```

The `id=...` part will have the right number to use in `mousebutton(...)`

## External links

*   Synergy website: [https://symless.com/synergy/](https://symless.com/synergy/)
*   Official documentation: [https://github.com/symless/synergy-core/wiki/User-Guide](https://github.com/symless/synergy-core/wiki/User-Guide)