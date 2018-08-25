**[DPMS](https://en.wikipedia.org/wiki/VESA_Display_Power_Management_Signaling "wikipedia:VESA Display Power Management Signaling")** (Display Power Management Signaling) enables power saving behaviour of monitors when the computer is not in use. The time of inactivity before the monitor enters into a given saving power level, standby, suspend or off, can be set as described in [DPMSSetTimeouts(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/DPMSSetTimeouts.3). Note that some monitors make no difference between various DPMS modes.

## Contents

*   [1 Setting up DPMS in X](#Setting_up_DPMS_in_X)
*   [2 Disabling DPMS](#Disabling_DPMS)
*   [3 Modifying DPMS and screensaver settings using xset](#Modifying_DPMS_and_screensaver_settings_using_xset)
*   [4 DPMS interaction in a Linux console with setterm](#DPMS_interaction_in_a_Linux_console_with_setterm)
    *   [4.1 Prevent screen from turning off](#Prevent_screen_from_turning_off)
    *   [4.2 Pipe the output to a cat to see the escapes](#Pipe_the_output_to_a_cat_to_see_the_escapes)
    *   [4.3 Pipe the escapes to any tty (with write/append perms) to modify that terminal](#Pipe_the_escapes_to_any_tty_.28with_write.2Fappend_perms.29_to_modify_that_terminal)
        *   [4.3.1 Bash loop to set ttys 0-256](#Bash_loop_to_set_ttys_0-256)
*   [5 See also](#See_also)

## Setting up DPMS in X

**Note:** As of Xorg 1.8 DPMS is auto detected and enabled if ACPI is also enabled at kernel runtime.

Add the following to a file in `/etc/X11/xorg.conf.d/` in the `Monitor` section:

```
Option "DPMS" "true"

```

Add the following to the `ServerLayout` section, change the times (in minutes) as necessary:

```
Option "StandbyTime" "10"
Option "SuspendTime" "20"
Option "OffTime" "30"

```

**Note:** If the `"OffTime"` option does not work, use screen blanking instead, which will keep the monitor turned on with a black image. Alternatively, change `"blanktime"` to `"0"` to disable screen blanking
```
Option         "BlankTime" "30"

```

An example file `/etc/X11/xorg.conf.d/10-monitor.conf` could look like this.

```
Section "Monitor"
    Identifier "LVDS0"
    Option "DPMS" "false"
EndSection

Section "ServerLayout"
    Identifier "ServerLayout0"
    Option "StandbyTime" "0"
    Option "SuspendTime" "0"
    Option "OffTime"     "0"
    Option "BlankTime"   "0"
EndSection

```

## Disabling DPMS

Since DPMS is enable by default in many scenarios, explicit action must be taken to disable it. To complete disable DPMS, add the following to a file in `/etc/X11/xorg.conf.d/10-monitor.conf`:

```
Section "Extensions"
    Option      "DPMS" "Disable"
EndSection

```

## Modifying DPMS and screensaver settings using xset

It is possible to turn off your monitor using the *xset* tool which is provided by [installing](/index.php/Installing "Installing") the [xorg-xset](https://www.archlinux.org/packages/?name=xorg-xset) package.

Example commands:

| Command | Description |
| xset s off | Disable screen saver blanking |
| xset s 3600 3600 | Change blank time to 1 hour |
| xset -dpms | Turn off DPMS |
| xset s off -dpms | Disable DPMS and prevent screen from blanking |
| xset dpms force off | Turn off screen immediately |
| xset dpms force standby | Standby screen |
| xset dpms force suspend | Suspend screen |

To query the current settings:

 `$ xset q` 
```
...
Screen Saver:
  prefer blanking:  yes    allow exposures:  yes
  timeout:  600    cycle:  600
DPMS (Energy Star):
  Standby: 600    Suspend: 600    Off: 600
  DPMS is Enabled
  Monitor is On

```

See [xset(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xset.1) for all available commands.

**Note:**

*   [XScreenSaver](/index.php/XScreenSaver "XScreenSaver") and [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager) use their own DPMS settings and override *xset* configuration. See [XScreenSaver#DPMS and blanking settings](/index.php/XScreenSaver#DPMS_and_blanking_settings "XScreenSaver") and [Xfce#Display blanking](/index.php/Xfce#Display_blanking "Xfce") for more information.
*   If using the command manually in a shell you may need to prefix it with `sleep 1;` for it to work correctly, for example `sleep 1; xset dpms force off`
*   `xset dpms 0 0 0`, which sets all the DPMS timeouts to zero, could be a better way to "disable" DPMS, since the effect of `-dpms` would be reverted when, for example, turning off the screen with `xset dpms force off`.
*   If using `xset` in [xinitrc](/index.php/Xinitrc "Xinitrc") does not work, specify settings within a file in `/etc/X11/xorg.conf.d/`. See [#Setting up DPMS in X](#Setting_up_DPMS_in_X) for details.

## DPMS interaction in a Linux console with setterm

The *setterm* utility issues terminal recognized escape codes to alter the terminal. Essentially it just writes/echos the terminal sequences to the current terminal device, whether that be in screen, a remote ssh terminal, console mode, serial consoles, etc.

setterm Syntax: (0 disables)

```
setterm -blank [0-60|force|poke]
setterm -powersave [on|vsync|hsync|powerdown|off]
setterm -powerdown [0-60]

```

**Note:** If you haven't already read the brief DPMS article linked to below, please skim it to understand how DPMS can be used in the console the same as in X.

### Prevent screen from turning off

You can run this command:

```
$ setterm -blank 0 -powerdown 0

```

Alternatively you can disable console blanking permanently using the following command:

```
# echo -ne "\033[9;0]" >> /etc/issue

```

Changing 0 (after the semicolon) to e.g. 3, will keep the screen on for 3 minutes, before entering standby mode.

### Pipe the output to a cat to see the escapes

```
$ setterm -powerdown 2>&1 | exec cat -v 2>&1 | sed "s/\\^\\[/\\\\033/g"

```

### Pipe the escapes to any tty (with write/append perms) to modify that terminal

```
$ setterm -powerdown 0 >> /dev/tty3

```

**Note:** `>>` is used instead of `>`. For permission issues using *sudo* in a script or something, you can use the **tee** program to append the output of setterm to the tty device, which tty's let appending sometimes but not writing.

#### Bash loop to set ttys 0-256

```
$ for i in {0..256}; do setterm -powerdown 0 >> /dev/tty$i; done; unset i;

```

## See also

*   [PC Monitor DPMS specification explanation](https://web.archive.org/web/20180129095655/http://webpages.charter.net/dperr/dpms.htm)
*   [DPMS control in X](http://ptspts.blogspot.be/2009/10/screen-blanking-dpms-screen-saver.html)