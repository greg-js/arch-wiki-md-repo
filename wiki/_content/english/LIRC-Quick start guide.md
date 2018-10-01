Related articles

*   [LIRC](/index.php/LIRC "LIRC")

Step-by-step [LIRC](/index.php/LIRC "LIRC") setup guide for USB (MCE [Media Center Edition]) IR receiver with universal remote control.

**This is a quick-start guide only.** Please refer to man pages of the commands and files used and online documentation for in-depth help.

## Contents

*   [1 Prerequisites](#Prerequisites)
*   [2 Setup](#Setup)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Keypresses are not detected](#Keypresses_are_not_detected)
    *   [3.2 Repeated keypress events](#Repeated_keypress_events)
*   [4 Final configuration](#Final_configuration)
*   [5 Final testing](#Final_testing)

## Prerequisites

*   Get a USB IR receiver, preferably an MCE model which is almost always supported out-of-the-box.
*   Re-purpose an old universal remote control you have lying around the house.

## Setup

1.  Connect the USB IR receiver.
2.  Ensure there are fully charged batteries in your remote control.
3.  Get some kind of output/response from the remote using `mode2`: `# mode2` Point the remote control at the IR receiver and press some buttons. This will attempt to autodetect the correct input device using the default "devinput" driver. However, this might not work without manual configuration of protocols.
4.  If no button presses are detected for most keys, change IR protocols. If you get no response to the remote control buttons you want to use, you likely need to enable different protocols: `# ir-keytable -p <protocol> -p <protocol> ...` Look at the output of `ir-keytable` (as well as `cat /sys/class/rc/rc0/protocols`). When you have problems, run `ir-keytable -p all` as [root](/index.php/Root_user "Root user").
5.  If no button presses are detected for most keys, try different universal remote control device modes. You may also need to try different universal remote control device modes (TV, DVD, Audio, etc., buttons) in order to detect button presses when you're getting started. (You could possibly reprogram the universal remote's modes, but that would likely be a long trial-and-error process to find a setting that works.)
6.  After reconfiguring IR protocols and remote control device mode, retest: `# mode2` Point the remote control at the IR receiver and press some buttons. If button presses for most keys are not detected repeat the prior two steps until they are (or just run `ir-keytable -p all` as [root](/index.php/Root_user "Root user")).
7.  If you have narrowed down what protocols you need to support for your remote control, set them: `# ir-keytable -p sony -p rc-5` Otherwise, you can just use all protocols: `# ir-keytable -p all` 
8.  Determine the correct device for your IR receiver. Use either the default "devinput" driver or the older "default" driver:
    ```
    $ mode2 --driver devinput --list-devices
    $ mode2 --driver default --list-devices
    $ ir-keytable

    ```

9.  Use the device found for your USB IR receiver, e.g., `/dev/input/event11`: `# mode2 --driver devinput --device /dev/input/event11` or just try: `# mode2 --driver devinput --device auto` See if button presses are detected.
10.  If required, edit `/etc/lirc/lirc_options.conf`, e.g., if you're using the driver "default" instead of "devinput".
11.  Test your remote to see if scancodes are printed: `# ir-keytable -t` See if button presses are detected.
12.  Create a modified systemd `lircd.service` file which loads the correct protocols: `# cp /usr/lib/systemd/system/lircd.service /etc/systemd/system/` Edit `/etc/systemd/system/lircd.service`. At the end of the `[Service]` section add the following line: `ExecStartPost=/usr/bin/ir-keytable -p <protocol> -p <protocol>` where each "<protocol>" string is replaced by the protocol(s) you need (or just use `/usr/bin/ir-keytable -p all`).
13.  [Start](/index.php/Start "Start") the lirc daemon, `lircd.service`, so you can record keypresses in order to write an lircd configuration file for your remote control.
14.  Use irrecord to record keypress scancodes. Run: `# irrecord` to save/record the keystrokes to be used for your application. Follow `irrecord`'s instructions.
15.  Install the recorded lircd configuration file:
    ```
    # mv *device_name*.lircd.conf /etc/lirc/lircd.conf.d/
    # chown root:root /etc/lirc/lircd.conf.d/*device_name*.lircd.conf
    ```

16.  Move `devinput.lircd.conf` to `devinput.lircd.dist` to disable it, because you're not using an IR keyboard and/or mouse, just the IR receiver: `# mv /etc/lirc/lircd.conf.d/devinput.lircd.conf /etc/lirc/lircd.conf.d/devinput.lircd.dist` 
17.  [Restart](/index.php/Restart "Restart") `lircd.service` so you use the newly created lircd configuration file.
18.  Test to make sure the keys you recorded are correctly detected, that is, the correct key symbol is output for each button you press: `$ irw` See if the correct key symbols are reported, and if repeated signals are properly rejected.

## Troubleshooting

### Keypresses are not detected

Follow [#Setup](#Setup).

### Repeated keypress events

If you're having keypress repeating problems (each button press is echoed multiple times), examine the output of `irw`. The second column value is the repeat count. This will increment when repeated signals are detected. Each decoded button press with its count reset to "00" is reported as a separate button press event by lircd.

To fix this problem, generally the "gap" parameter sampled by `irrecord` in the `*device_name*.lircd.conf` file should be adjusted, often to a much larger value (e.g., from 44968 up to 113975).

After editing/adjusting any lircd configuration file, be sure to restart lircd (as shown above).

## Final configuration

Write an lircrc file for your end user application. This file is used by all client programs built with lirc support that attach to lircd to read IR control events. Edit `~/.lircrc` to issue commands to the program to be controlled. Test this configuration by running:

```
$ ircat *prog*

```

to see if the correct "config" strings for program `*prog*` are being output when you press all the buttons you wish to use. Note: If `~/.lircrc` isn't read by your application or just doesn't work, an alternate default location is `~/.config/lircrc`.

## Final testing

Finally, run your end user application and test remote control button presses to control it. If it works, you're done! If not, review and repeat the above sections as necessary to get each configuration step working before proceeding to the next step or section.