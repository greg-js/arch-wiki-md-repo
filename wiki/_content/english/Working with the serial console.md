Configure your Arch Linux machine so you can connect to it via the serial console port (com port). This will enable you to administer the machine even if it has no keyboard, mouse, monitor, or network attached to it (a headless server).

As of Arch Linux 2007.x, installation of Arch Linux is possible via the serial console as well.

A basic environment for this scenario is two machines connected using a serial cable (9-pin connector cable). The administering machine can be any Unix/Linux or Windows machine with a terminal emulator program (PuTTY or Minicom, for example).

The configuration instructions below will enable GRUB menu selection, boot messages, and terminal forwarding to the serial console.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Configure console access on the target machine](#Configure_console_access_on_the_target_machine)
        *   [1.1.1 GRUB2 and systemd](#GRUB2_and_systemd)
            *   [1.1.1.1 Without GRUB2, systemd only](#Without_GRUB2.2C_systemd_only)
        *   [1.1.2 GRUB v1 and No systemd](#GRUB_v1_and_No_systemd)
*   [2 Making Connections](#Making_Connections)
    *   [2.1 Connect using a terminal emulator program](#Connect_using_a_terminal_emulator_program)
        *   [2.1.1 Command line](#Command_line)
            *   [2.1.1.1 dterm](#dterm)
            *   [2.1.1.2 Minicom](#Minicom)
            *   [2.1.1.3 picocom](#picocom)
            *   [2.1.1.4 Screen](#Screen)
            *   [2.1.1.5 Serialclient](#Serialclient)
        *   [2.1.2 And, for Windows](#And.2C_for_Windows)
        *   [2.1.3 Graphical front-ends](#Graphical_front-ends)
*   [3 Installing Arch Linux using the serial console](#Installing_Arch_Linux_using_the_serial_console)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Ctrl-C and Minicom](#Ctrl-C_and_Minicom)
    *   [4.2 Resizing a terminal](#Resizing_a_terminal)

## Configuration

### Configure console access on the target machine

#### GRUB2 and systemd

If you configure the serial console in GRUB2 systemd will create a getty listener on the same serial device as GRUB2 by default. So, this is the only configuration needed for Arch running with systemd. To make grub enable the serial console, open `/etc/default/grub` in an editor. Change the `GRUB_CMDLINE_DEFAULT` line to start the console on `/dev/ttyS0`. Note in the example below, we set two consoles up; one on tty0 and one on the serial port.

```
GRUB_CMDLINE_LINUX_DEFAULT="console=tty0 console=ttyS0,38400n8"

```

Now we need to tell grub where is the console and what command to start in order to enable the serial console (Note as above for Linux kernel, one can append multiple input/output terminals in grub e.g. GRUB_TERMINAL="console serial" would enable both display and serial):

```
## Serial console
GRUB_TERMINAL=serial
GRUB_SERIAL_COMMAND="serial --speed=38400 --unit=0 --word=8 --parity=no --stop=1"

```

Rebuild the grub.cfg file with following command:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

After a reboot, getty will be listening on `/dev/ttyS0`, expecting 38400 baud, 8 data bits, no parity and one stop bit. When Arch boots, systemd will automatically start a getty session to listen on the same device with the same settings.

##### Without GRUB2, systemd only

Ignore this entire section if you have configured GRUB2 to listen on the serial interface. If you do not want GRUB2 to listen on the serial device, but only want getty listening after boot then follow these steps.

To start getty listening on `/dev/ttyS0` use systemctl:

```
# systemctl start getty@ttyS0.service

```

You can check to see the speed(s) getty is using with systemctl, but should be 38400 8N1:

```
# systemctl status serial-getty@ttyS0.service

```

To have getty listening on `/dev/ttyS0` every boot, enable the service for that specific port:

```
# systemctl enable serial-getty@ttyS0.service

```

Now, after a reboot, getty will be listening on device `/dev/ttyS0` expecting 38400 baud, 8 data bits, no parity and one stop bit-times.

#### GRUB v1 and No systemd

Edit the GRUB config file `/boot/grub/menu.lst` and add these lines to the general area of the configuration:

```
serial --unit=0 --speed=9600
terminal --timeout=5 serial console

```

Add suitable console parameters (e.g. change the serial device name or baud rate if required) at the end of your current kernel line:

```
console=tty0 console=ttyS0,9600

```

For example, the kernel line should look something like this after modification:

```
kernel /vmlinuz-linux root=/dev/md0 ro md=0,/dev/sda3,/dev/sdb3 vga=773 console=tty0 console=ttyS0,9600

```

**Note:** When the `terminal --timeout=5 serial console` line is added to your menu.lst grub configuration, your boot sequence will now show a series of "Press any key to continue" messages. If no key is pressed, the boot menu will appear on whichever (serial or console) appears first in the 'terminal' configuration line. The lines will look like this upon boot:

`Press any key to continue.
Press any key to continue.
Press any key to continue.
Press any key to continue.
Press any key to continue.
Press any key to continue.
Press any key to continue.`

Next, we have to edit `/etc/inittab` and add a new agetty line below the existing ones:

```
c0:2345:respawn:/sbin/agetty 9600 ttyS0 linux

```

Edit `/etc/securetty` and add an entry for the the serial console, *below the existing entries*:

```
ttyS0

```

Reboot.

**Note:** In all of the steps above, ttyS1 can also be used in case your machine has more than one serial port.

## Making Connections

### Connect using a terminal emulator program

**Note:** Before making a connection, it is recommended to add your user to the `uucp` group. Otherwise you will need root's permission to make a connection:
```
# gpasswd -a *username* uucp

```
See [Users and groups#User groups](/index.php/Users_and_groups#User_groups "Users and groups") for details.

Perform these steps on the machine used to connect the remote console.

#### Command line

##### dterm

[dterm](https://aur.archlinux.org/packages/dterm/) is a tiny serial communication program. If you invoke it without parameters, it will connect to `/dev/ttyS0` at 9600 baud by default. The following example connect to `/dev/ttyS0` at 115200 baud, with 8 data bits, no parity bit and 1 stop bit-times:

```
$ dterm 115200 8 n 1

```

See its homepage[[1]](http://www.knossos.net.nz/resources/free-software/dterm/) for more examples.

##### Minicom

[minicom](https://www.archlinux.org/packages/?name=minicom) can be obtained from the official repositories. Start Minicom in setup mode:

```
$ minicom -s

```

Using the textual navigation menu, change the serial port settings to the following:

```
Serial Device: /dev/ttyS0
Bps/Par/Bits: 9600 8N1

```

Press Enter to exit the menus (pressing Esc will not save changes). Remove the modem Init and Reset strings, as we are not connecting to a modem. To do this, under the `Modem and Dialing` menu, delete the Init and Reset strings. Optionally save the configuration by choosing `save setup as dfl` from the main menu. Restart minicom with the serial cable connected to the target machine. To end the session, press `Ctrl+A` followed by `Ctrl+X`.

##### picocom

[picocom](https://www.archlinux.org/packages/?name=picocom) is a tiny dumb-terminal emulation program that is very like minicom, but instead of *mini*, it is *pico*. The following example connect to `ttyS0` at 9600 bps:

```
$ picocom -b 9600 /dev/ttyS0

```

**Note:** if the backspace key won't work properly try out this option: '--omap delbs'

See its manual for detailed usage.

##### Screen

[screen](https://www.archlinux.org/packages/?name=screen) is able to connect to a serial port. It will connect at 9600 baud by default:

```
$ screen /dev/ttyS0

```

A different baud rate (e.g. 115200) may be specified on the commmand line.

```
screen /dev/ttyS0 115200

```

##### Serialclient

Serialclient[[2]](https://github.com/flagos/serialclient) is a CLI client for serial connection written in ruby. Install it with the following:

```
# pacman -S ruby
# gem install serialclient

```

Then, you can use like this:

```
$ serialclient -p /dev/ttyS0

```

#### And, for Windows

On Windows machines, connect to the serial port using programs like PuTTY[[3]](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) or Terminalbpp[[4]](https://sites.google.com/site/terminalbpp/).

#### Graphical front-ends

[gtkterm](https://aur.archlinux.org/packages/gtkterm/) provides a graphical interface to the task, with most abilities provided by [vte](https://www.archlinux.org/packages/?name=vte).

[cutecom](https://aur.archlinux.org/packages/cutecom/) is another gui enabled serial monitor.

[putty](https://www.archlinux.org/packages/?name=putty) is also available for Linux.

[moserial](https://aur.archlinux.org/packages/moserial/) is a gtk-based serial terminal, primarily intended for technical users and hardware hackers who need to communicate with embedded systems, test equipment, and serial consoles.

## Installing Arch Linux using the serial console

**Note:** The Arch Linux monthly release(i.e. the installation CD)'s boot loader has been configured[[5]](https://projects.archlinux.org/archiso.git/tree/configs/releng/syslinux/archiso_head.cfg#n1) to listen on 0 port(`ttyS0`/COM1) at 38400 bps, with 8 data bits, no parity bit and 1 stop bit-times.

1.  Connect to the target machine using the method described above.
2.  Boot the target machine using the Arch Linux installation CD.
3.  When the bootloader appears, select *Boot Arch Linux (<arch>)* and press `Tab` to edit
4.  Append `console=ttyS0,38400` and press `Enter`.
5.  Now systemd should detect ttyS0 and spawn a serial getty on it. Login as `root` and start the installation as usual.

**Note:** After setup is complete, the console settings will not be saved on the target machine; in order to avoid having to connect a keyboard and monitor, configure console access on the target machine before rebooting.

**Note:** While a port speed of 9600 is used in most of the examples in this document, working with higher values is recommended (List of available speeds is displayed in Minicom by pressing 'Ctrl-A' and then 'P')

## Troubleshooting

### Ctrl-C and Minicom

If you are having trouble sending a Control-C command through minicom you need to switch off hardware flow control in the device settings (minicom -s), which then enables the break.

### Resizing a terminal

Unlike ssh, serial connection does not have a mechanism to transfer something like `SIGWINCH` when a terminal is resized. This will cause weird problem with some full-screen programs (e.g. `less`) when you resized your terminal emulator's window.

Resize the terminal via `stty` is a workaround:

```
$ stty rows *lines* cols *columns*

```

However the above one requires you to manually input the proper geometry. The following examples should simplify the work.

1\. There is a less-known utility called `resize`, which is shipped with [xterm](https://www.archlinux.org/packages/?name=xterm), can solve this problem. Invoke it without parameter after you resize the terminal emulator's window:

```
$ resize

```

2\. In the case that you do not want to install xterm, it is possible to do the same work via a simple shell function. Put the following function into your zshrc, invoke it without parameter after you resize the terminal emulator's window:

```
rsz() {
	if [[ -t 0 && $# -eq 0 ]];then
		local IFS='[;' escape geometry x y
		print -n '\e7\e[r\e[999;999H\e[6n\e8'
		read -sd R escape geometry
		x=${geometry##*;} y=${geometry%%;*}
		if [[ ${COLUMNS} -eq ${x} && ${LINES} -eq ${y} ]];then
			print "${TERM} ${x}x${y}"
		else
			print "${COLUMNS}x${LINES} -> ${x}x${y}"
			stty cols ${x} rows ${y}
		fi
	else
		[[ -n ${commands[repo-elephant]} ]] && repo-elephant || print 'Usage: rsz'  ## Easter egg here :)
	fi
}
```