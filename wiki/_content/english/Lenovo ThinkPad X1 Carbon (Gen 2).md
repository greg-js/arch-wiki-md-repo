Related articles

*   [Lenovo ThinkPad X1 Carbon](/index.php/Lenovo_ThinkPad_X1_Carbon "Lenovo ThinkPad X1 Carbon")
*   [Lenovo ThinkPad X1 Carbon (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_3) "Lenovo ThinkPad X1 Carbon (Gen 3)")
*   [Lenovo ThinkPad X1 Carbon (Gen 4)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_4) "Lenovo ThinkPad X1 Carbon (Gen 4)")
*   [Lenovo ThinkPad X1 Carbon (Gen 5)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_5) "Lenovo ThinkPad X1 Carbon (Gen 5)")

**Tip:** A great resource for thinkpads is [http://www.thinkwiki.org/wiki/ThinkWiki](http://www.thinkwiki.org/wiki/ThinkWiki)

## Contents

*   [1 Model description](#Model_description)
    *   [1.1 Legacy-BIOS](#Legacy-BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 Hardware](#Hardware)
    *   [2.1 Power Management](#Power_Management)
    *   [2.2 Wake From Suspend](#Wake_From_Suspend)
    *   [2.3 Keyboard](#Keyboard)
        *   [2.3.1 Remapping keys using xmodmap](#Remapping_keys_using_xmodmap)
        *   [2.3.2 Remapping keys using xkb](#Remapping_keys_using_xkb)
            *   [2.3.2.1 Backtick (`) and Tilde (~)](#Backtick_.28.60.29_and_Tilde_.28.7E.29)
            *   [2.3.2.2 Home and End](#Home_and_End)
            *   [2.3.2.3 BackSpace and Delete](#BackSpace_and_Delete)
    *   [2.4 Trackpad](#Trackpad)
        *   [2.4.1 Lock-ups on click](#Lock-ups_on_click)
        *   [2.4.2 Tweaking trackpad behavior](#Tweaking_trackpad_behavior)
        *   [2.4.3 Touchpad not working after wake up from sleep](#Touchpad_not_working_after_wake_up_from_sleep)
    *   [2.5 Keyboard backlight](#Keyboard_backlight)
        *   [2.5.1 Automatically turn on backlight when typing](#Automatically_turn_on_backlight_when_typing)
    *   [2.6 Audio](#Audio)
    *   [2.7 Processor](#Processor)
*   [3 Add ALSA-Preamplifier](#Add_ALSA-Preamplifier)
    *   [3.1 Network](#Network)
        *   [3.1.1 Wired](#Wired)
        *   [3.1.2 Wireless](#Wireless)
    *   [3.2 Display](#Display)
        *   [3.2.1 Touchscreen](#Touchscreen)
        *   [3.2.2 GPU](#GPU)
        *   [3.2.3 HiDPI](#HiDPI)
        *   [3.2.4 Xbindkeys](#Xbindkeys)
    *   [3.3 KMS](#KMS)
    *   [3.4 Webcam](#Webcam)
    *   [3.5 Fingerprint Reader](#Fingerprint_Reader)
    *   [3.6 WWAN (Mobile broadband)](#WWAN_.28Mobile_broadband.29)
    *   [3.7 GPS](#GPS)
    *   [3.8 Bluetooth](#Bluetooth)
*   [4 Other hardware](#Other_hardware)
    *   [4.1 Docking](#Docking)
        *   [4.1.1 Audio](#Audio_2)
        *   [4.1.2 Video](#Video)
        *   [4.1.3 Other ports](#Other_ports)

## Model description

Lenovo ThinkPad X1 Carbon, Gen 2 (X1C). Comes without optical drive. There is also a touch version. Has UEFI BIOS with BIOS-legacy fallback mode.

To ensure you have this version, try running *dmidecode*:

```
# dmidecode -t system | grep Version
Version: ThinkPad X1 Carbon 2nd

```

**Tip:** A great resource for thinkpads is [http://www.thinkwiki.org/wiki/ThinkWiki](http://www.thinkwiki.org/wiki/ThinkWiki)

### Legacy-BIOS

### UEFI

Installing the system from an [Archboot](/index.php/Archboot "Archboot") device just works.

Alteratively, to manually install using `efibootmgr` (see [Unified Extensible Firmware Interface#efibootmgr](/index.php/Unified_Extensible_Firmware_Interface#efibootmgr "Unified Extensible Firmware Interface")), you can run this:

```
# efibootmgr -c -d /dev/sda -p 1 -l /EFI/arch_grub/grubx64.efi -L "Arch"

```

This assumes that you are using [GRUB](/index.php/GRUB "GRUB") with /dev/sda1 as your ESP. If you are using a different partition change the arguments to `-d` and `-p` arguments.

**Note:**

This may not work from the [Archiso](/index.php/Archiso "Archiso") image, in which case you will need to use the EFI shell built into the archiso image.

Reboot the computer and drop into the EFI shell at the menu, then run these commands:

```
> bcfg boot add 0 fs0:\EFI\arch_grub\grubx64.efi "Arch"

```

Make sure you are using the correct disk (`fs0`) and bootloader location (`\EFI\arch_grub\grubx64.efi`).

## Hardware

Almost everything works out of the box. Most of the hardware is based on the Intel Lynx Point reference design.

### Power Management

The [kernel module](/index.php/Kernel_module "Kernel module") `thinkpad_acpi` picks up most of the sensors. The kernel module `tp_smapi` is not currently supported. PCIe ASPM does not currently work.

[Udev](/index.php/Udev "Udev") does not not notify whenever battery discharges by 1%, but it does notify at 80%, 20%, 5%, 4% and 0%. To take advantage of this, see (Suspend On Low Battery [Laptop#hibernate on low battery level](/index.php/Laptop#hibernate_on_low_battery_level "Laptop"))

### Wake From Suspend

Wake from suspend can be buggy with earlier versions of the bios, see: [[1]](http://linux-thinkpad.10952.n7.nabble.com/Gen-2-Haswell-X1-Carbon-suspend-to-RAM-hang-td21039.html)

This can be solved by flashing the bios to a version >=1.13\. Look here for Lenovo's bios versions: [[2]](http://support.lenovo.com/en_GB/downloads/detail.page?DocID=DS039783)

A guide how to make a bootable BIOS key drive can be found here: [[3]](http://positon.org/lenovo-thinkpad-bios-update-with-linux-and-usb)

And some fairly old help from lenovo here: [[4]](http://www.thinkwiki.org/wiki/BIOS_Upgrade#Using_grub4dos_.28also_for_Linux.29)

If the function keys fail to wake after suspend, ensure you have a kernel version >=3.15.

If you build your own kernels, make sure to either enable TPM (Trusted Platform Module) drivers or disable the Security Chip in the BIOS.

### Keyboard

On kernel 3.14 and lower the adaptive panel at the top of the keyboard is locked to function mode.

From kernel 3.15, Home mode is also available which allows access to screen brightness and other controls.

If you wish to remap keys to get back to a sane keyboard layout, you can use either xmodmap or xkb. The difference is largely user preference.

#### Remapping keys using xmodmap

To get the tilde key back to a sane location on the keyboard you can use xmodmap [Xmodmap](/index.php/Xmodmap "Xmodmap") to remap Shift-Esc to '~'. Install [xorg-xmodmap](https://www.archlinux.org/packages/?name=xorg-xmodmap) and generate a custom key map:

```
$ xmodmap -pke > ~/.Xmodmap

```

Then edit your key map:

 `~/.Xmodmap` 
```
...
keycode   9 = Escape asciitilde Escape
...

```

Make sure xmodmap loads your new keymap on login:

 `~/.xinitrc` 
```
...
if [ -s ~/.Xmodmap ]; then
       xmodmap ~/.Xmodmap
fi
...

```

#### Remapping keys using xkb

##### Backtick (`) and Tilde (~)

To get the backtick/tilde back to a normal location, add the following definition for the Escape button:

 `/usr/share/X11/xkb/symbols/pc` 
```
key <ESC>  { [ grave, asciitilde ] };

```

##### Home and End

You may also wish to remap the 'Home' and 'End' button back to Caps Lock, or Escape. Change the lines for HOME and END as follows:

 `/usr/share/X11/xkb/symbols/pc` 
```
key <HOME> { [ Caps_Lock ] };
key  <END> { [ Caps_Lock ] };

```

or to make 'Home' and 'End' be Escape:

 `/usr/share/X11/xkb/symbols/pc` 
```
key <HOME> { [ Escape ] };
key  <END> { [ Escape ] };

```

##### BackSpace and Delete

If you find yourself accidentally hitting the delete key instead of backspace, you may wish to make both backspace and delete be 'BackSpace', while functioning as 'Delete' when you hold down shift:

 `/usr/share/X11/xkb/symbols/pc` 
```
key <BKSP> { [ BackSpace, Delete ] };
key <DELE> { [ BackSpace, Delete ] };

```

### Trackpad

To enable Trackpad support you need to install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

**Warning:** the above did the opposite for me. When both [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) and [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) are installed, the trackpoint (red thingy) uses libinput by default, so it doesn't cooperate with the trackpad (which by default is driven by synaptics), and as a result you can't scroll with middle button + trackpoint. Keeping only [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) got everything working.

#### Lock-ups on click

There are significant issues with the trackpad locking up on click. This is due to the trackpad operating in buggy PS/2 mode.

One alternative is to abandon the trackpad completely and use the trackpoint. Make sure xf86-input-synaptics is not installed - the trackpad will still register button one mouse clicks. Using xbindkeys [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") and [xdotool](https://www.archlinux.org/packages/?name=xdotool), right button clicks can be mapped to some other event. For example:

 `~/.xbindkeysrc` 
```
# Emit a right click on Alt + trackpad click
"xdotool click 3"
  Mod1 + b:1 + Release

```

#### Tweaking trackpad behavior

The behavior of the trackpad by default can be contrary to your expectations, particularly if you are coming from an OS X style trackpad. The following settings can help significantly:

 `/etc/X11/xorg.conf.d/99-x1carbon.conf` 
```
# Copy this to /etc/X11/xorg.conf.d/99-x1carbon.conf
 Section "InputClass"
     Identifier "X1 carbon stuff"
     MatchIsTouchpad "on"
     MatchDevicePath "/dev/input/event*"
     Driver "synaptics"

     # Enable two finger scrolling vertically, disable horizontally
     Option "VertTwoFingerScroll" "1"
     Option "HorizTwoFingerScroll" "0"

     # No scrolling along the edge
     Option "VertEdgeScroll" "0"
     Option "HorizEdgeScroll" "0"

     Option "LockedDrags" "0"
     Option "FingerPress" "1"

     # Turn off the blasted corners as buttons
     Option "RTCornerButton" "0"
     Option "RBCornerButton" "0"
     Option "LTCornerButton" "0"
     Option "LBCornerButton" "0"

     # Ignore "taps" and listen for "clicks"
     Option "TapButton1" "0"
     Option "TapButton2" "0"
     Option "TapButton3" "0"
     Option "ClickFinger1" "1" # Left click one finger
     Option "ClickFinger2" "3" # Right click two fingers
     Option "ClickFinger3" "0" # Three finger click disabled

     Option "TapAndDragGesture" "0"

     # No circular scrolling
     Option "CircularScrolling" "0"
 EndSection

```

If you are using gnome-shell, you may need to tell the settings app not to overwrite our changes:

```
gsettings set org.gnome.settings-daemon.plugins.mouse active false

```

#### Touchpad not working after wake up from sleep

See here: [Touchpad Synaptics#Touchpad does not work after resuming from hibernate/suspend](/index.php/Touchpad_Synaptics#Touchpad_does_not_work_after_resuming_from_hibernate.2Fsuspend "Touchpad Synaptics")

### Keyboard backlight

Works out of the box. there is a button on the soft keyboard to toggle it between off, low, and high brightness.

#### Automatically turn on backlight when typing

Using a c program that continuously checks for keyboard input, it is possible to activate the backlight for a certain time. The program source is as a follows

 `kbdbacklight.c` 
```
/* Original Author: Howard Chu <hyc@symas.com> 2013-01-15
 *
 * compile as "gcc -O2 -o kbdbacklight kbdbacklight.c" and run it in the background, or arrange to have it run at bootup.
 *
 * adapted by gabtub@gmail.com 2017-01-22
 * using https://gist.github.com/hadess/6847281
 * based on http://askubuntu.com/questions/383501/enable-the-keyboard-backlights-on-supported-lenovo-e-g-carbon-x1-with-command
 * original code found at  http://forum.notebookreview.com/threads/asus-keyboard-backlight-controller.703985/
 * sigterm catching done as shown in https://airtower.wordpress.com/2010/06/16/catch-sigterm-exit-gracefully/
 *
 * monitor keyboard activity and toggle keyboard backlight
 */
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <poll.h>
#include <unistd.h>
#include <signal.h>
#include <string.h>

static char dummybuf[8192];

/** @brief How many milliseconds before turning off kbd light */
#ifndef IDLE_MSEC
#define IDLE_MSEC	5000
#endif

#ifndef BRGHT_OFF
#define BRGHT_OFF	3
#endif
#ifndef BRGHT_MED
#define BRGHT_MED 67
#endif
#ifndef BRGHT_MAX
#define BRGHT_MAX 131
#endif

volatile sig_atomic_t running = 1;

void term(int signum)
{
    // sigterm == 15
    running = 0;
}

int main(int argc, char *argv[])
{
  struct sigaction action;
  struct pollfd pfd;
  int rc, blfd;
  int timeout, prev = -1;
  /* possible brightness levels for x1
   * - 3		off
   * - 67	medium
   * - 131	max
   */
  char bm[1];
  bm[0] = BRGHT_MED;

  memset(&action, 0, sizeof(struct sigaction));
  action.sa_handler = term;
  sigaction(SIGTERM, &action, NULL);

  // potentially needs
  // sudo modprobe -r ec_sys
  // sudo modprobe ec_sys write_support=1
  blfd = open("/sys/kernel/debug/ec/ec0/io", O_WRONLY);
  // needs the event bound to the keyboard
  // for Xorg ie find using
  //  cat /var/log/Xorg.0.log | grep "keyboard.*event"
  pfd.fd = open("/dev/input/event4", O_RDONLY);
  pfd.events = POLLIN;
  timeout = IDLE_MSEC;

  while (running) {
    rc = poll(&pfd, 1, timeout);
    if (rc) {
      /* got keyboard input, flush it all and
       * wait for the next event.
       */
      read(pfd.fd, dummybuf, sizeof(dummybuf));
      timeout = IDLE_MSEC;
      bm[0] = BRGHT_MED;
    } else {
      /* once we've gotten a timeout, turn off
       * kbd backlight and wait forever for
       * the next keypress
       */
      timeout = -1;
      bm[0] = BRGHT_OFF;
    }
    if (bm[0] == prev)
      continue;
    lseek(blfd, 13, SEEK_SET);
    write(blfd, bm, 1);
    prev = bm[0];
  }
  // clean up after sigterm
  bm[0] = BRGHT_OFF;
  lseek(blfd, 13, SEEK_SET);
  write(blfd, bm, 1);
}

```

This file can be compiled with:

```
 gcc -O2 -o kbdbacklight kbdbacklight.c

```

and must be executed as root. Furthermore, following kernel modules must be loaded for this to work:

```
 modprobe -r ec_sys
 modprobe ec_sys write_support=1

```

It would be possible to autostart this by creating a systemd service as follows:

*   Create a folder /usr/local/customscripts/kbdbacklight/
*   Save the compiled c program to /usr/local/customscripts/kbdbacklight/kbdbacklight
*   Create the following bash script in the same folder:

 `/usr/local/customscripts/kbdbacklight/kbdbacklight.sh` 
```
#!/bin/bash
# must be executed as root
modprobe -r ec_sys
modprobe ec_sys write_support=1
./kbdbacklight &
RETVAL=$?
PID=$!
[ $RETVAL -eq 0 ] && echo $PID > /usr/local/customscripts/kbdbacklight/pid

```

*   Create the following systemd service and place it in /etc/systemd/system/kbdbacklight.service

 `/etc/systemd/system/kbdbacklight.service` 
```
#!/bin/bash
[Unit]
Description=starts a daemon monitoring keyboard usage. will turn on keyboard backlight until no key is pressed for a TIMEOUT period
Requires=
After=

[Service]
Type=forking
User=root
WorkingDirectory=/usr/local/customscripts/kbdbacklight/
ExecStart=/usr/local/customscripts/kbdbacklight/kbdbacklight.sh &
PIDFile=/usr/local/customscripts/kbdbacklight/pid

[Install]
WantedBy=multi-user.target

```

*   activate the service with

```
 systemctl enable kbdbacklight
 systemctl start kbdbacklight

```

**Note:**

Specifiy the amount timeout for turning the backlight off again by adjusting the constant IDLE_MSEC in the c program. (and recompiling it again)

### Audio

Sound works out of the box. Uses the snd_hda_intel kernel module.

You may need to add default sound card options to the module.

In /etc/modprobe.d/alsa-base.conf include the following line:

options snd_hda_intel index=1

### Processor

See [Microcode#Enabling Intel microcode updates](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode") how to update to processor's microcode.

## Add ALSA-Preamplifier

It is a common problem on laptops running linux that the sound, even on maximum, is not loud enough. This can be fixed by adding an ALSA preamplifier. Install alsa-utils:

```
sudo pacman -S alsa-utils

```

Change the config in /etc/asound.conf to the following ( you might have to adjust the cardnumber):

```
# Set your DEFAULT device to the softvol plug-in
# NOT to a hardware card device
#
# The "!" means completely override the previous default
# Not just changing/adding to it.
pcm.!default {
  type plug
  slave.pcm "softvol"
}

# Configure softvol
pcm.softvol {
  type softvol

  # Send softvol's output to dmix
  slave {
    pcm "dmix"
    # If you wanted to you could send the output to a card directly
    # But in most cases it's better to send it to dmix and let
    # dmix handle where to send it. You can add a whole extra section
    # to configure dmix and where it sends output, but I'm
    # not covering that here.

    ## Use Card 0 Device 0 instead of dmix
    # pcm "hw:0,0"
    ## Use Card 2 Device 0 instead of dmix
    # pcm "hw:2,0"
  }

  # Add a control slider in your mixer interfaces
  # i.e. KMix and alsamixer
  control {
    name "Pre-Amp"
    card 0 #<CardNumberYouWantControlToShowOn> i.e. card 0 or card 2
  }

  # Minimum dB when slider is at 0%
  min_dB -5.0

  # Maximum DB when slider is at 100%
  max_dB 40.0

  # How many levels the slider should go through
  # i.e. how granular do you want your control to be
  resolution 12
}

```

Taken from [here](https://web.archive.org/web/20160316004932/http://blog.tpa.me.uk/2013/10/23/alsa-pre-amp-volume-boost-the-simple-explanation/). **WARNING:** It is possible to permanently damage your loudspeakers if you turn it up too much!

### Network

#### Wired

There is a small port on the right side for Ethernet. An adaptor is required. In case of loss of the adaptor, the part number is for ordering is 04X6435.

#### Wireless

Works out of the box. The module `iwlwifi` should be automatically loaded by [udev](/index.php/Udev "Udev").

 `$ lspci` 
```
Network controller: Intel Corporation Wireless 7260 (rev 83)

```

### Display

#### Touchscreen

Works out of the box as single touch. The hardware is multitouch, but current stable drivers only support left-click mouse emulation.

#### GPU

The video card installed is an integrated Intel Haswell GPU. See [intel](/index.php/Intel "Intel") for more info.

#### HiDPI

Since the display has such a high pixel density, you might encounter problems. See here: [HiDPI](/index.php/HiDPI "HiDPI")

#### Xbindkeys

For alternative window managers (Fluxbox, etc..), try installing [xbindkeys](/index.php/Xbindkeys "Xbindkeys") and adding the following to `~/.xbindkeysrc`

```
"xbacklight -dec 5"
  XF86MonBrightnessDown
"xbacklight -inc 5"
  XF86MonBrightnessUp

```

### KMS

Get [KMS](/index.php/KMS "KMS") working by adding i915 to the modules line

 `/etc/mkinitcpio.conf`  `MODULES="i915"` 

Then regenerate your [initramfs](/index.php/Initramfs "Initramfs"):

```
# mkinitcpio -p linux

```

### Webcam

Works out of the box.

### Fingerprint Reader

The fingerprint reader is a Validity Sensors model (138a:0017) also used on the Thinkpad X240 and T440\. ThinkFinger does NOT support this reader.

This fingerprint reader requires libfprint to be build from the current git ([https://github.com/ars3niy/fprint_vfs5011.git](https://github.com/ars3niy/fprint_vfs5011.git) ) as yet no stable fprint release supports it.

### WWAN (Mobile broadband)

The SIM-card must be inserted in the back of the laptop.

This is usually a Sierra Wireless EM7345\. It uses the cdc_mbim kernel module from kernel 3.14 forward. Since Gnome 3.14.1 it works with NetworkManager after installing modemmanager (after a reboot to catch the udev event).

### GPS

This is provided by the Sierra Wireless EM7345\. mbim_gpsd is required as well as a udev rule.

Untested

### Bluetooth

Works out of the box after enabling bluetooth.service.

## Other hardware

### Docking

This model comes with a OneLink dock port, next to the power adaptor. Out of the box, it is covered with a rubber cap that can be removed easily. Tested with OneLink Pro dock.

Since Kernel 4.12 the touchpad and mousenipple stops working when the notebook is disconnected from the Dockingstation. A temporary solution is to reload the mouse kernel module:

```
$ rmmod psmouse && modprobe psmouse

```

#### Audio

Audio works out of the box, but presents as a separate sound card.

#### Video

The dock has DisplayPort and DVI on the back, and either work, but only one at a time. Second external monitor can still be connected to the mini-DisplayPort directly on the laptop.

#### Other ports

All other ports on the dock work as expected.