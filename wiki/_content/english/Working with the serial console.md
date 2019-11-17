An Arch Linux machine can be configured for connections via the serial console port, which enables administration of a machine even if it has no keyboard, mouse, monitor, or network attached to it.

Installation of Arch Linux is possible via the serial console as well.

A basic environment for this scenario is two machines connected using a serial cable (9-pin connector cable). The administering machine can be any Unix/Linux or Windows machine with a terminal emulator program (PuTTY or Minicom, for example).

The configuration instructions below will enable boot loader menu selection, boot messages, and terminal forwarding to the serial console.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configure console access on the target machine](#Configure_console_access_on_the_target_machine)
    *   [1.1 Boot loader](#Boot_loader)
        *   [1.1.1 GRUB](#GRUB)
        *   [1.1.2 GRUB Legacy](#GRUB_Legacy)
        *   [1.1.3 rEFInd](#rEFInd)
        *   [1.1.4 Syslinux](#Syslinux)
    *   [1.2 Kernel](#Kernel)
    *   [1.3 getty](#getty)
*   [2 Making Connections](#Making_Connections)
    *   [2.1 Connect using a terminal emulator program](#Connect_using_a_terminal_emulator_program)
        *   [2.1.1 Command line](#Command_line)
            *   [2.1.1.1 dterm](#dterm)
            *   [2.1.1.2 Minicom](#Minicom)
            *   [2.1.1.3 picocom](#picocom)
            *   [2.1.1.4 Screen](#Screen)
            *   [2.1.1.5 Serialclient](#Serialclient)
        *   [2.1.2 And, for Windows](#And,_for_Windows)
        *   [2.1.3 Graphical front-ends](#Graphical_front-ends)
*   [3 Installing Arch Linux using the serial console](#Installing_Arch_Linux_using_the_serial_console)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Ctrl-C and Minicom](#Ctrl-C_and_Minicom)
    *   [4.2 Resizing a terminal](#Resizing_a_terminal)

## Configure console access on the target machine

### Boot loader

#### GRUB

When using [GRUB](/index.php/GRUB "GRUB") with a generated `grub.cfg`, edit `/etc/default/grub` and enable serial input and output support:

 `/etc/default/grub` 
```
...
GRUB_TERMINAL_INPUT="console serial"
...
GRUB_TERMINAL_OUTPUT="gfxterm serial"
...
```

Next add the `GRUB_SERIAL_COMMAND` variable and set the options for the serial connection. For COM1 (`/dev/ttyS0`) with baud rate of 115200 bit/s:

 `/etc/default/grub` 
```
...
GRUB_SERIAL_COMMAND="serial --unit=0 --speed=115200"
```

Read GRUB's manual on [Using GRUB via a serial line](https://www.gnu.org/software/grub/manual/grub/grub.html#Serial-terminal) and the [serial command](https://www.gnu.org/software/grub/manual/grub/grub.html#serial) for detailed explanation of the available options.

#### GRUB Legacy

Edit the [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") configuration file `/boot/grub/menu.lst` and add these lines to the general area of the configuration:

```
serial --unit=0 --speed=9600
terminal --timeout=5 serial console

```

**Note:** When the `terminal --timeout=5 serial console` line is added to your `menu.lst`, your boot sequence will now show a series of `Press any key to continue` messages. If no key is pressed, the boot menu will appear on whichever (serial or console) appears first in the `terminal` configuration line.

#### rEFInd

[rEFInd](/index.php/REFInd "REFInd") supports serial console only in text mode. Edit `refind.conf` and uncomment `textonly`.

#### Syslinux

To enable serial console in [Syslinux](/index.php/Syslinux "Syslinux"), edit `syslinux.cfg` and add `SERIAL` as the first directive in the configuration file.

For COM1 (`/dev/ttyS0`) with baud rate of 115200 bit/s:

```
SERIAL 0 115200

```

The serial parameters are hardcoded to 8 bits, no parity and 1 stop bit.[[1]](https://wiki.syslinux.org/wiki/index.php/SYSLINUX#SERIAL_port_.5Bbaudrate_.5Bflowcontrol.5D.5D). Read [Syslinux Wiki:Config#SERIAL](https://wiki.syslinux.org/wiki/index.php?title=Config#SERIAL) for the directive's options.

### Kernel

Kernel's output can be sent to serial console by setting the `console=` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). The last specified `console=` will be set as `/dev/console`.

```
console=tty0 console=ttyS0,115200

```

See [https://www.kernel.org/doc/Documentation/admin-guide/serial-console.rst](https://www.kernel.org/doc/Documentation/admin-guide/serial-console.rst).

### getty

At boot, [systemd-getty-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-getty-generator.8) will start a [getty](/index.php/Getty "Getty") instance for each console specified in the kernel command line.

If you have not configured `console=` in kernel command line [start](/index.php/Start "Start") `serial-getty@*device*.service`. For `/dev/ttyS0` (COM1) that would be `serial-getty@ttyS0.service`. [Enable](/index.php/Enable "Enable") the service to start it at boot.

Unless specified otherwise in the kernel command line, getty will be expecting 38400 bit/s baud rate, 8 data bits, no parity and one stop bit-times.

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

See its homepage[[2]](http://www.knossos.net.nz/resources/free-software/dterm/) for more examples.

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

[GNU Screen](/index.php/GNU_Screen "GNU Screen") is able to connect to a serial port. It will connect at 9600 baud by default:

```
$ screen /dev/ttyS0

```

A different baud rate (e.g. 115200) may be specified on the command line.

```
screen /dev/ttyS0 115200

```

To end the session, press `Ctrl+a` followed by `K`. Alternatively, press `Ctrl+a`, type `:quit` and confirm it by pressing `Enter`.

##### Serialclient

Serialclient[[3]](https://github.com/flagos/serialclient) is a CLI client for serial connection written in ruby. Install it with the following:

```
# pacman -S ruby
# gem install serialclient

```

Then, you can use like this:

```
$ serialclient -p /dev/ttyS0

```

#### And, for Windows

On Windows machines, connect to the serial port using programs like PuTTY[[4]](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) or Terminalbpp[[5]](https://sites.google.com/site/terminalbpp/).

#### Graphical front-ends

[cutecom](https://aur.archlinux.org/packages/cutecom/) is another gui enabled serial monitor.

[putty](https://www.archlinux.org/packages/?name=putty) is also available for Linux.

[moserial](https://www.archlinux.org/packages/?name=moserial) is a gtk-based serial terminal, primarily intended for technical users and hardware hackers who need to communicate with embedded systems, test equipment, and serial consoles.

## Installing Arch Linux using the serial console

**Note:** The Arch Linux monthly release(i.e. the installation CD)'s boot loader has been configured[[6]](https://projects.archlinux.org/archiso.git/tree/configs/releng/syslinux/archiso_head.cfg#n1) to listen on 0 port(`ttyS0`/COM1) at 38400 bps, with 8 data bits, no parity bit and 1 stop bit-times.

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

Unlike ssh, serial connections do not have a mechanism to transfer something like `SIGWINCH` when a terminal is resized. This can cause weird problems with some full-screen programs (e.g. `less`) when you resize your terminal emulator's window.

Resizing the terminal via `stty` is a workaround:

```
$ stty rows *lines* cols *columns*

```

However, this requires you to manually input the proper geometry. The following methods should be simpler.

1\. There is a lesser-known utility called `resize`, shipped with [xterm](https://www.archlinux.org/packages/?name=xterm), that can solve this problem. Invoke it without parameters after you resize the terminal emulator's window:

```
$ resize

```

2\. If you don't want to install xterm, it is possible to do the same work via a shell function. Put the following function into your zshrc and invoke it without parameters after resizing the terminal emulator's window:

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