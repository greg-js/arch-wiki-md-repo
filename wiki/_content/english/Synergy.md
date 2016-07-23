[Synergy](http://synergy-project.org/) lets you easily share a single mouse and keyboard between multiple computers (even with different operating systems) without the need for special hardware. It is intended for users with multiple computers on their desk since each system uses its own monitor(s).

Redirecting the mouse and keyboard is as simple as moving the mouse off the edge of your screen. Synergy also merges the clipboards of all the systems into one, allowing cut-and-paste between systems. Furthermore, it synchronizes screen savers so they all start and stop together and, if screen locking is enabled, only one screen requires a password to unlock them all.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Arch Linux](#Arch_Linux)
    *   [1.2 Windows and OS X](#Windows_and_OS_X)
*   [2 Pre-configuration](#Pre-configuration)
    *   [2.1 Arch Linux](#Arch_Linux_2)
        *   [2.1.1 Enable Encryption](#Enable_Encryption)
*   [3 Server configuration](#Server_configuration)
    *   [3.1 Arch Linux](#Arch_Linux_3)
        *   [3.1.1 Use Encryption](#Use_Encryption)
    *   [3.2 Windows](#Windows)
    *   [3.3 OS X](#OS_X)
    *   [3.4 Configuration examples](#Configuration_examples)
*   [4 Clients configuration](#Clients_configuration)
    *   [4.1 Arch Linux](#Arch_Linux_4)
        *   [4.1.1 Use Encryption](#Use_Encryption_2)
        *   [4.1.2 Autostart](#Autostart)
    *   [4.2 Windows](#Windows_2)
    *   [4.3 OS X](#OS_X_2)
*   [5 Known Issues](#Known_Issues)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Keyboard AltGr](#Keyboard_AltGr)
    *   [6.2 Keyboard repeat](#Keyboard_repeat)
    *   [6.3 Keyboard mapping](#Keyboard_mapping)
    *   [6.4 No Cursor in Gnome3](#No_Cursor_in_Gnome3)
    *   [6.5 Client is returning "failed to verify server certificate fingerprint"](#Client_is_returning_.22failed_to_verify_server_certificate_fingerprint.22)
*   [7 External Links](#External_Links)

## Installation

### Arch Linux

You can [install](/index.php/Install "Install") the [synergy](https://www.archlinux.org/packages/?name=synergy) package.

### Windows and OS X

[Download](http://synergy-project.org/download/) and run the newest installer from the official website.

## Pre-configuration

First determine the IP addresses and [host names](/index.php/Network_configuration#Set_the_hostname "Network configuration") for each machine and make sure each has a correct hosts file.

*   Arch Linux - `/etc/hosts`
*   Windows - `C:\WINDOWS\system32\drivers\etc\hosts`
*   OS X - [How to Add Hosts to Local Hosts File](http://support.apple.com/kb/TA27291).

 `/etc/hosts` 
```
10.10.66.1        archserver.localdomain       archserver
10.10.66.100      archleft.localdomain         archleft
10.10.66.105      archright.localdomain        archright
```

**Note:** Check that the clients can reach the server.

### Arch Linux

#### Enable Encryption

Synergy version 1.7 replaced their own transport encryption with SSL.

To install the SSL plugin, copy or symlink it to the plugins directory, which is `~/.synergy/plugins` by default.

```
$ mkdir -p ~/.synergy/plugins
$ ln -s /usr/lib/synergy/libns.so ~/.synergy/plugins/libns.so

```

## Server configuration

In synergy, the computer with keyboard and mouse you want to share is called server. See [Synergy Configuration File Format](http://synergy-project.org/wiki/Text_Config) for a detailed description of all available sections and options.

### Arch Linux

The configuration file for Arch Linux is `/etc/synergy.conf`. If it does not exist, create it using `/etc/synergy.conf.example`, whose comments should give you enough information for a basic configuration; if you need further reference, read the guide mentioned above.

**Tip:** You may also use [quicksynergy](https://aur.archlinux.org/packages/quicksynergy/) from the [AUR](/index.php/AUR "AUR") which provide a GUI to simplify the configuration process.

**Tip:** Make sure the server port is not blocked. By default, synergy uses port 24800.

If you experience problems and you wish to run the server in the foreground, you can run the following command instead:

```
# synergys -f

```

The synergy server process needs to attach to your user's X session, which means it needs to run as your user. [Enable](/index.php/Enable "Enable") `synergys@mary` as the appropriate user (replacing 'mary' with your username).

**Tip:** You can enable `synergys@mary.socket` to start the server when a client tries to connect instead. This is useful when the service can't connect to an X server on boot.

#### Use Encryption

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
# synergys --enable-crypto

```

*   Starting with systemd:

 ` /usr/lib/systemd/system/synergys@.service` 
```
[Unit]
Description=Synergy Server Daemon
After=network.target

[Service]
User=%i
ExecStart=/usr/bin/synergys --no-daemon --config /etc/synergy.conf --enable-crypto
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

To start the service for your user:

```
# systemctl start synergys@mary

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

### OS X

OS X has a similar configuration as Unix: check [the official documentation](http://synergy-project.org/wiki/Developer) for more information.

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

#### Use Encryption

If you use the synergy command line client, copy the file containing the fingerprint **`~/.synergy/SSL/Fingerprints/Local.txt`** from the server into the clients home directory **`~/.synergy/SSL/Fingerprints/TrustedServers.txt`**. To start the synergy command line client with encryption, type:

```
$ synergyc --enable-crypto

```

**Note:** There is an open issue with the GUI client of synergy (see [https://github.com/symless/synergy/issues/4737](https://github.com/symless/synergy/issues/4737)). The dialog to prompt for confirmation of the server's fingerprint, only pops up if the logging level is set to INFO, DEBUG or DEBUG2.

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

*   Otherwise, if you are using a [display manager](/index.php/Display_manager "Display manager") (kdm, gdm, [SLiM](/index.php/SLiM "SLiM"), ...), or a stand-alone [window manager](/index.php/Window_manager "Window manager") (Openbox, ...), you could exploit its start-up script and add the following:

```
synergyc server-host-name

```

For example, using *kdm* you should edit `/usr/share/config/kdm/Xsetup`.

*   To start the Synergy client with systemd, create a service file, **/etc/systemd/system/synergyc@.service** and optionally a config file, **/etc/conf.d/synergyc.conf**

 ` /etc/systemd/system/synergyc@.service` 
```
[Unit]
Description=Synergy Client Daemon
After=network.target

[Service]
EnvironmentFile=/etc/conf.d/synergyc.conf
ExecStart=/usr/bin/synergyc --no-daemon --debug ${DEBUGLEVEL:-INFO} ${SERVERALIAS}
User=%i

[Install]
WantedBy=multi-user.target
```
 `/etc/conf.d/synergyc.conf` 
```
DEBUGLEVEL=WARNING
SERVERALIAS=server-name
```

To start the service for your user,

```
# systemctl start synergyc@mary

```

Automatically starting Synergy is also documented in its [official reference page](https://github.com/symless/synergy/wiki/Startup).

### Windows

After installation, open the Synergy program, select the option *Client (use another computer's keyboard and mouse)* and type the host name of the server computer in the text box, then click *Start* to start the client.

**Note:** You can use the tray icon to stop the client.

If you want to start the Synergy client every time Windows starts, you have to launch the program **as an administrator**, then go to *Edit -> Services* and select *Install* in the *Client* section.

If you want to start the client from the command-line, here is a Windows command you can place in a `.bat` file or just run from `cmd.exe`. This points to a configuration file in `C:\synergy.sgc` and runs in the background like a service.

 `START /MIN /D"C:\Program Files\Synergy+\bin" synergys.exe -d ERROR -n m6300 -c C:\synergy.sgc -a 10.66.66.2:24800` 

### OS X

Locate the synergyc program in the synergyc folder and drag it onto the terminal window: the full path will appear in the terminal. Now append the host name of the server, so that the complete command will look like this:

 `/path/to/synergyc/synergyc server-host-name` 

Then press `Enter`.

## Known Issues

If Arch is being used as a client in a Synergy installation, the server may not be able to wake the client monitor. There are some workarounds, such as executing the following via [SSH](/index.php/SSH "SSH"), if ACPI is enabled (see: [Modifying DPMS and ScreenSaver settings with xset](/index.php/Display_Power_Management_Signaling#Modifying_DPMS_and_screensaver_settings_using_xset "Display Power Management Signaling")):

 `# xset dpms force on` 

## Troubleshooting

The official documentation has a [FAQ](http://synergy-project.org/wiki/Synergy_FAQ) and also a [troubleshooting page](https://github.com/symless/synergy/wiki/User-Guide#Troubleshooting).

### Keyboard AltGr

If you encounter problems with AltGr add

```
altgr = alt

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

### No Cursor in Gnome3

When Gnome 3 doesn't detect a mouse, it will default to touchscreen mode and hide the cursor. To enable run:

```
# dconf write /org/gnome/settings-daemon/plugins/cursor/active false

```

This can be added to an init script or systemd unit:

```
 ExecStartPost=dconf write /org/gnome/settings-daemon/plugins/cursor/active false

```

### Client is returning "failed to verify server certificate fingerprint"

You need to copy the content of server's "~/.synergy/SSL/Fingerprints/Local.txt" into client's "~/.synergy/SSL/Fingerprints/TrustedServers.txt".

## External Links

*   Synergy website: [http://synergy-project.org](http://synergy-project.org)
*   Official documentation: [http://synergy-project.org/wiki/User_Guide](http://synergy-project.org/wiki/User_Guide)