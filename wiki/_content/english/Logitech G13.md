The Logitech G13 is a 25-key "advanced gameboard" from Logitech's Gaming series, with the intention of replacing the left half of your keyboard whilst gaming. It uses rubber dome keyswitches for the main 22-keys, mouse-like buttons for the two buttons around the joystick, a joystick (which can be pressed in), four Mode buttons, four option buttons, a menu button, and a backlight toggle. ([Official Site](http://gaming.logitech.com/en-us/product/g13-advanced-gameboard))

There are a couple options for drivers, but only one that appears to work well today:

*   Running the official [Logitech Gaming Software](http://support.logitech.com/software/gaming-software) under [Wine](/index.php/Wine "Wine"). Despite working fine, the software [has a Garbage rating](https://appdb.winehq.org/objectManager.php?sClass=application&iId=14748) on WineHQ, as it can't actually communicate with USB devices. (However, the reports available are quite old, and you may have better luck)
*   [g15daemon](https://www.archlinux.org/packages/?name=g15daemon), despite it's backend (libg15) claiming to support the G13, does not actually support the G13.
*   [linux-g13-driver](https://code.google.com/p/linux-g13-driver/), which can compile if you edit the Makefile (see [issue #16](https://code.google.com/p/linux-g13-driver/issues/detail?id=16)), and may work for you.
*   [g13](https://github.com/ecraven/g13) [g13-git](https://aur.archlinux.org/packages/g13-git/) is a user-space driver, which seems to work the best out of these.

## Contents

*   [1 g13](#g13)
    *   [1.1 Installation](#Installation)
    *   [1.2 Running](#Running)
    *   [1.3 Configuring](#Configuring)
    *   [1.4 Commands](#Commands)
    *   [1.5 Keys](#Keys)

## g13

### Installation

Install [g13-git](https://aur.archlinux.org/packages/g13-git/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

In order to run g13d as your user instead of root, download [91-g13.rules](https://github.com/ecraven/g13/blob/master/91-g13.rules), and put it in `/etc/udev/rules.d/`.

### Running

**Note:** The binary is named g13d, the binary g13 is from [gnupg](https://www.archlinux.org/packages/?name=gnupg).

After following the steps above, when you reboot and launch g13, you should receive an image with a "linux inside" logo, "G13", and the GNU logo.

If you receive the error `/dev/uinput doesn't grant write permissions`, running the command below should fix it, but only until you reboot.

 `# chmod a+rw /dev/uinput` 

### Configuring

g13 is configured via writing to /tmp/g13-0.

Ex, to set the display a purple colour:

 `$ echo "rgb 177 13 201" > /tmp/g13-0` 

g13 can also handle multiple commands at once:

 `$ echo -e "rgb 177 13 201\nbind G4 KEY_W" > /tmp/g13-0` 
**Tip:** g13 can handle multiple commands at once, and will ignore lines starting with `#`. You can use this to make files full of commands and run `cat file > /tmp/g13-0` when you're ready to play.

### Commands

*   `rgb <rrr> <ggg> <bbb>`, Set the backlight to an rgb colour, values are expressed in decimal from 0 to 255.

For example, to set the display green:

 `rgb 0 255 0` 

*   `bind <g13key> <actualkey>`, Binds a G13 key. All keys are bound to `a` by default.

For example, to setup WASD movement:

```
bind G4 KEY_W
bind G10 KEY_A
bind G11 KEY_S
bind G12 KEY_D
```

See below for how to configure this.

*   `mod <n>`, Sets the backlight status of M1, M2, M3, and MR.

<n> is a bitmask. To find the desired state compute the sum of 1 (M1), 2 (M2), 4 (M3) and 8 (MR). For example, to set M1, M3, and MR on, and turn M2 off (1+4+8=13):

 `mod 13` 

### Keys

 `Keys to map to (should be self explanatory)`  `KEY_0 KEY_1 KEY_2 KEY_3 KEY_4 KEY_5 KEY_6 KEY_7 KEY_8 KEY_9 KEY_A KEY_APOSTROPHE KEY_B KEY_BACKSLASH KEY_BACKSPACE KEY_C KEY_CAPSLOCK KEY_COMMA KEY_D KEY_DOT KEY_DOWN KEY_E KEY_ENTER KEY_EQUAL KEY_ESC KEY_F KEY_F1 KEY_F10 KEY_F2 KEY_F3 KEY_F4 KEY_F5 KEY_F6 KEY_F7 KEY_F8 KEY_F9 KEY_G KEY_GRAVE KEY_H KEY_I KEY_J KEY_K KEY_KP0 KEY_KP1 KEY_KP2 KEY_KP3 KEY_KP4 KEY_KP5 KEY_KP6 KEY_KP7 KEY_KP8 KEY_KP9 KEY_KPASTERISK KEY_KPDOT KEY_KPMINUS KEY_KPPLUS KEY_L KEY_LEFT KEY_LEFTALT KEY_LEFTBRACE KEY_LEFTCTRL KEY_LEFTSHIFT KEY_M KEY_MINUS KEY_N KEY_NUMLOCK KEY_O KEY_P KEY_Q KEY_R KEY_RIGHT KEY_RIGHTBRACE KEY_RIGHTSHIFT KEY_S KEY_SCROLLLOCK KEY_SEMICOLON KEY_SLASH KEY_SPACE KEY_T KEY_TAB KEY_U KEY_UP KEY_V KEY_W KEY_X KEY_Y KEY_Z`  `Keys to map`  `BD DOWN G1 G10 G11 G12 G13 G14 G15 G16 G17 G18 G19 G2 G20 G21 G22 G3 G4 G5 G6 G7 G8 G9 L1 L2 L3 L4 LEFT LIGHT LIGHT_STATE M1 M2 M3 MR TOP STICK_LEFT STICK_RIGHT STICK_UP STICK_DOWN` 

Since that can be less than explanatory, here's a diagram showing where the keys physically are on the device:

```
Keypad:
      ______________
     |  160x43 LCD  |
     |              |
      ‾‾‾‾‾‾‾‾‾‾‾‾‾‾
     BD L1 L2 L3 L4 LIGHT_STATE
        M1 M2 M3 MR
G1  G2  G3  G4  G5  G6  G7 
G8  G9  G10 G11 G12 G13 G14
   G15  G16 G17 G18  G19
       G10  G21  G22

Joystick:
 L            STICK_UP
 E  STICK_LEFT  TOP   STICK_RIGHT
 F           STICK_DOWN
 T
               DOWN

```

**Tip:** As a jumping off point, you can use [default.bind](https://github.com/zekesonxx/g13-profiles/blob/master/default.bind), which has the same bindings as the default profile when using the official software, along with a purple backlight.