Joysticks can be a bit of a hassle to get working in Linux. Not because they are poorly supported, but simply because you need to determine which modules to load to get your joystick working, and it's not always very obvious!

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Joystick input systems](#Joystick_input_systems)
*   [2 Determining which modules you need](#Determining_which_modules_you_need)
    *   [2.1 Loading the modules for analogue devices](#Loading_the_modules_for_analogue_devices)
    *   [2.2 USB joysticks](#USB_joysticks)
        *   [2.2.1 Troubleshooting](#Troubleshooting)
*   [3 Testing your configuration](#Testing_your_configuration)
    *   [3.1 Joystick API](#Joystick_API)
    *   [3.2 evdev API](#evdev_API)
*   [4 Setting up deadzones and calibration](#Setting_up_deadzones_and_calibration)
    *   [4.1 Wine deadzones](#Wine_deadzones)
    *   [4.2 Xorg deadzones](#Xorg_deadzones)
    *   [4.3 Joystick API deadzones](#Joystick_API_deadzones)
    *   [4.4 evdev API deadzones](#evdev_API_deadzones)
    *   [4.5 Configuring curves and responsivness](#Configuring_curves_and_responsivness)
*   [5 Disable joystick from controlling mouse](#Disable_joystick_from_controlling_mouse)
*   [6 Using Joystick to send keystrokes](#Using_Joystick_to_send_keystrokes)
    *   [6.1 Xorg configuration example](#Xorg_configuration_example)
*   [7 Specific devices](#Specific_devices)
    *   [7.1 Dance pads](#Dance_pads)
    *   [7.2 Logitech Thunderpad Digital](#Logitech_Thunderpad_Digital)
    *   [7.3 Nintendo Gamecube Controller](#Nintendo_Gamecube_Controller)
    *   [7.4 Nintendo Switch Pro Controller and Joy-Cons](#Nintendo_Switch_Pro_Controller_and_Joy-Cons)
        *   [7.4.1 Kernel Nintendo HID Driver](#Kernel_Nintendo_HID_Driver)
            *   [7.4.1.1 joycond Userspace Daemon](#joycond_Userspace_Daemon)
            *   [7.4.1.2 Using hid-nintendo with Steam Games](#Using_hid-nintendo_with_Steam_Games)
            *   [7.4.1.3 Using hid-nintendo with SDL2 Games](#Using_hid-nintendo_with_SDL2_Games)
        *   [7.4.2 Dolphin (Gamecube Controller Emulation)](#Dolphin_(Gamecube_Controller_Emulation))
        *   [7.4.3 Steam](#Steam)
    *   [7.5 PlayStation 3/4 controller](#PlayStation_3/4_controller)
        *   [7.5.1 Connecting via Bluetooth](#Connecting_via_Bluetooth)
        *   [7.5.2 Using Playstation 3 controllers with Steam](#Using_Playstation_3_controllers_with_Steam)
        *   [7.5.3 Using generic/clone controllers](#Using_generic/clone_controllers)
    *   [7.6 iPEGA-9017s and other Bluetooth gamepads](#iPEGA-9017s_and_other_Bluetooth_gamepads)
        *   [7.6.1 iPEGA-9068 and 9087](#iPEGA-9068_and_9087)
    *   [7.7 Steam Controller](#Steam_Controller)
        *   [7.7.1 Wine](#Wine)
    *   [7.8 Xbox 360 controller](#Xbox_360_controller)
        *   [7.8.1 SteamOS xpad](#SteamOS_xpad)
        *   [7.8.2 xboxdrv](#xboxdrv)
            *   [7.8.2.1 Multiple controllers](#Multiple_controllers)
            *   [7.8.2.2 Mimic Xbox 360 controller with other controllers](#Mimic_Xbox_360_controller_with_other_controllers)
        *   [7.8.3 Using generic/clone controllers](#Using_generic/clone_controllers_2)
    *   [7.9 Xbox Wireless Controller / Xbox One Wireless Controller](#Xbox_Wireless_Controller_/_Xbox_One_Wireless_Controller)
        *   [7.9.1 Connect Xbox Wireless Controller with usb cable](#Connect_Xbox_Wireless_Controller_with_usb_cable)
        *   [7.9.2 Connect Xbox Wireless Controller with Bluetooth](#Connect_Xbox_Wireless_Controller_with_Bluetooth)
            *   [7.9.2.1 xpadneo](#xpadneo)
        *   [7.9.3 Connect Xbox Wireless Controller with Microsoft Xbox Wireless Adapter](#Connect_Xbox_Wireless_Controller_with_Microsoft_Xbox_Wireless_Adapter)
            *   [7.9.3.1 xow](#xow)
    *   [7.10 Logitech Dual Action](#Logitech_Dual_Action)
    *   [7.11 PlayStation 2 controller via USB adapter](#PlayStation_2_controller_via_USB_adapter)
    *   [7.12 PlayStation 3 controller via USB](#PlayStation_3_controller_via_USB)
    *   [7.13 PlayStation 3 controller via Bluetooth](#PlayStation_3_controller_via_Bluetooth)
    *   [7.14 PlayStation 4 controller](#PlayStation_4_controller)
        *   [7.14.1 Button mapping](#Button_mapping)
        *   [7.14.2 Fix Motion control conflict (gamepad won't work on somes apps)](#Fix_Motion_control_conflict_(gamepad_won't_work_on_somes_apps))
        *   [7.14.3 Disable touchpad acting as mouse](#Disable_touchpad_acting_as_mouse)
*   [8 Troubleshooting](#Troubleshooting_2)
    *   [8.1 Joystick moving mouse](#Joystick_moving_mouse)
    *   [8.2 Joystick not working in FNA/SDL based games](#Joystick_not_working_in_FNA/SDL_based_games)
    *   [8.3 Joystick not recognized by all programs](#Joystick_not_recognized_by_all_programs)
    *   [8.4 Steam Controller not pairing](#Steam_Controller_not_pairing)
    *   [8.5 Steam Controller makes a game crash or not recognized](#Steam_Controller_makes_a_game_crash_or_not_recognized)

## Joystick input systems

Linux has two different input systems for Joysticks – the original Joystick interface and the newer evdev-based interface.

`/dev/input/jsX` maps to the Joystick API interface and `/dev/input/event*` maps to the evdev ones (this also includes other input devices such as mice and keyboards). Symbolic links to those devices are also available in `/dev/input/by-id/` and `/dev/input/by-path/` where the legacy Joystick API has names ending with `-joystick` while the evdev have names ending with `-event-joystick`.

Most new games will default to the evdev interface as it gives more detailed information about the buttons and axes available and also adds support for force feedback.

While SDL1 defaults to evdev interface you can force it to use the old Joystick API by setting the environment variable `SDL_JOYSTICK_DEVICE=/dev/input/js0`. This can help many games such as X3\. SDL2 supports only the new evdev interface.

## Determining which modules you need

Unless you're using very old joystick that uses gameport or proprietary USB protocol, you will need just the generic USB human interface device (HID) modules.

For an extensive overview of all joystick related modules in Linux, you will need access to the Linux kernel sources -- specifically the Documentation section. Unfortunately, pacman kernel packages do not include what we need. If you have the kernel sources downloaded, have a look at `Documentation/input/joydev/`. You can browse the kernel source tree at [kernel.org](https://kernel.org/) by clicking the "browse" (cgit - the git frontend) link for the kernel that you're using, then clicking the "tree" link near the top. Here's a link to the [documentation from the latest kernel](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/tree/Documentation/input/joydev/joystick.rst).

Some joysticks need specific modules, such as the Microsoft Sidewinder controllers (`sidewinder`), or the Logitech digital controllers (`adi`). Many older joysticks will work with the simple `analog` module. If your joystick is plugging in to a gameport provided by your soundcard, you will need your soundcard drivers loaded - however, some cards, like the Soundblaster Live, have a specific gameport driver (`emu10k1-gp`). Older ISA soundcards may need the `ns558` module, which is a standard gameport module.

As you can see, there are many different modules related to getting your joystick working in Linux, so I couldn't possibly cover everything here. Please have a look at the documentation mentioned above for details.

### Loading the modules for analogue devices

You need to load a module for your gameport (`ns558`, `emu10k1-gp`, `cs461x`, etc...), a module for your joystick (`analog`, `sidewinder`, `adi`, etc...), and finally the kernel joystick device driver (`joydev`). Add these to a new file in `/etc/modules-load.d/`, or simply modprobe them. The `gameport` module should load automatically, as this is a dependency of the other modules.

### USB joysticks

You need to get USB working, and then modprobe your joystick driver, which is `usbhid`, as well as `joydev`. If you use a usb mouse or keyboard, `usbhid` will be loaded already and you just have to load the `joydev` module.

#### Troubleshooting

If your Xbox 360 joystick is connected with the Play&Charge USB cable it will show up in `lsusb` but it will not show up as an input device in `/dev/input/js*`, see note below.

## Testing your configuration

Once the modules are loaded, you should be able to find a new device: `/dev/input/js0` and a file ending with `-event-joystick` in `/dev/input/by-id` directory. You can simply `cat` those devices to see if the joystick works - move the stick around, press all the buttons - you should see mojibake printed when you move the sticks or press buttons.

Both interfaces are also supported in wine and reported as separate devices. You can test them with `wine control joy.cpl`.

**Tip:** Input devices by default have **input** group; for example, [pcsx2](https://www.archlinux.org/packages/?name=pcsx2) have no access to gamepad without rights. Make sure your user is in the **input** group.

### Joystick API

There are a lot of applications that can test this old API, `jstest` from the [joyutils](https://www.archlinux.org/packages/?name=joyutils) package is the simplest one. If the output is unreadable because the line printed is too long you can also use graphical tools. Plasma has a built in one in Input Devices panel in System Settings or [jstest-gtk-git](https://aur.archlinux.org/packages/jstest-gtk-git/) is an alternative.

Use of `jstest` is fairly simple, you just run `jstest /dev/input/js0` and it will print a line with state of all the axes (normalised to {-32767,32767}) and buttons.

After you start `jstest-gtk`, it will just show you a list of joysticks available, you just need to select one and press Properties.

### evdev API

The new 'evdev' API can be tested using the SDL2 joystick test application or using `evtest` from community repository. Install [sdl2-jstest-git](https://aur.archlinux.org/packages/sdl2-jstest-git/) and then run `sdl2-jstest --test 0`. Use `sdl2-jstest --list` to get IDs of other controllers if you have multiple ones connected.

To test force feedback on the device, use `fftest` from `linuxconsole` package:

```
$ fftest /dev/input/by-id/usb-*event-joystick

```

## Setting up deadzones and calibration

If you want to set up the deadzones (or remove them completely) of your analog input you have to do it separately for the xorg (for mouse and keyboard emulation), Joystick API and evdev API.

### Wine deadzones

Add the following registry entry and set it to a string from 0 to 10000 (affects all axes):

```
HKEY_CURRENT_USER\Software\Wine\DirectInput\DefaultDeadZone

```

Source: [UsefulRegistryKeys](http://wiki.winehq.org/UsefulRegistryKeys)

### Xorg deadzones

Add a similar line to `/etc/X11/xorg.conf.d/51-joystick.conf` (create if it doesn't exist):

 `/etc/X11/xorg.conf.d/51-joystick.conf` 
```
Section "InputClass"
    Option "MapAxis1" "deadzone=1000"
EndSection

```

1000 is the default value, but you can set anything between 0 and 30 000\. To get the axis number see the "Testing Your Configuration" section of this article. If you already have an option with a specific axis just type in the `deadzone=value` at the end of the parameter separated by a space.

### Joystick API deadzones

The easiest way is using `jstest-gtk` from [jstest-gtk-git](https://aur.archlinux.org/packages/jstest-gtk-git/). Select the controller you want to edit, then click the Calibration button at the bottom of the dialog (**don't** click Start Calibration there). You can then set the CenterMin and CenterMax values (which control the center deadzone), RangeMin and RangeMax which control the end of throw deadzones. Note that the calibration settings are applied when the application opens the device, so you need to restart your game or test application to see updated calibration settings.

After you set the deadzones use `jscal` to dump the new values into a shell script:

```
$ jscal -p /dev/input/jsX > jscal.sh # replace X with your joystick's number 
$ chmod +x jscal.sh

```

Now you need to make a [udev](/index.php/Udev "Udev") rule (for example `/etc/udev/rules.d and name it 85-jscal.rules`) so the script will automatically run when you connect the controller:

```
SUBSYSTEM=="input", ATTRS{idVendor}=="054c", ATTRS{idProduct}=="c268", ACTION=="add", RUN+="/usr/bin/bash /usr/bin/jscal.sh"

```

To get the idVendor and idProduct use `udevadm info --attribute-walk --name /dev/input/jsX`

Use the `/dev/input/by-id/*-joystick` device names in case you use multiple controllers.

### evdev API deadzones

The `evdev-joystick` tool from the [linuxconsole](https://www.archlinux.org/packages/?name=linuxconsole) package can be used to view and change deadzones and calibration for `evdev` API devices.

To view your device configuration:

```
$ evdev-joystick --showcal /dev/input/by-id/usb-*-event-joystick

```

To change the deadzone for a particular axis, use a command like:

```
$ evdev-joystick --evdev /dev/input/by-id/usb-*-event-joystick --axis 0 --deadzone 0

```

To set the same deadzone for all axes at once, omit the "--axis 0" option.

Use udev rules file to set them automatically when the controller is connected.

Note that inside the kernel, the value is called `flatness` and is set using the `EVIOCSABS` `ioctl`.

Default configuration will look like similar to this:

 `$ evdev-joystick --showcal /dev/input/by-id/usb-Madcatz_Saitek_Pro_Flight_X-55_Rhino_Stick_G0000090-event-joystick` 
```
Supported Absolute axes:
   Absolute axis 0x00 (0) (X Axis) (min: 0, max: 65535, flatness: 4095 (=6.25%), fuzz: 255)
   Absolute axis 0x01 (1) (Y Axis) (min: 0, max: 65535, flatness: 4095 (=6.25%), fuzz: 255)
   Absolute axis 0x05 (5) (Z Rate Axis) (min: 0, max: 4095, flatness: 255 (=6.23%), fuzz: 15)
   Absolute axis 0x10 (16) (Hat zero, x axis) (min: -1, max: 1, flatness: 0 (=0.00%), fuzz: 0)
   Absolute axis 0x11 (17) (Hat zero, y axis) (min: -1, max: 1, flatness: 0 (=0.00%), fuzz: 0)
```

While a more reasonable setting would be achieved with something like this (repeat for other axes):

 `$ evdev-joystick --evdev /dev/input/by-id/usb-Madcatz_Saitek_Pro_Flight_X-55_Rhino_Stick_G0000090-event-joystick --axis 0 --deadzone 512` 
```
Event device file: /dev/input/by-id/usb-Madcatz_Saitek_Pro_Flight_X-55_Rhino_Stick_G0000090-event-joystick
 Axis index to deal with: 0
 New dead zone value: 512
 Trying to set axis 0 deadzone to: 512
   Absolute axis 0x00 (0) (X Axis) Setting deadzone value to : 512
 (min: 0, max: 65535, flatness: 512 (=0.78%), fuzz: 255)
```

### Configuring curves and responsivness

In case your game requires just limited amount of buttons or has good support for multiple controllers, you may have good results with using `xboxdrv` to change response curves of the joystick.

Below are the setups I use for Saitek X-55 HOTAS:

```
$ xboxdrv --evdev /dev/input/by-id/usb-Madcatz_Saitek_Pro_Flight_X-55_Rhino_Throttle_G0000021-event-joystick \
  --evdev-no-grab --evdev-absmap 'ABS_#40=x1,ABS_#41=y1,ABS_X=x2,ABS_Y=y2' --device-name 'Hat and throttle' \
  --ui-axismap 'x2^cal:-32000:0:32000=,y2^cal:-32000:0:32000=' --silent

```

this maps the EV_ABS event with id of 40 and 41 (use xboxdrv with --evdev-debug to see the events registered), which is the normally inaccessible "mouse pointer" on the throttle, to first gamepad joystick and throttles to second joystick, it also clamps the top and lower ranges as they not always register fully.

A bit more interesting is the setup for the stick:

```
$ xboxdrv --evdev /dev/input/by-id/usb-Madcatz_Saitek_Pro_Flight_X-55_Rhino_Stick_G0000090-event-joystick \
  --evdev-no-grab --evdev-absmap 'ABS_X=x1' --evdev-absmap 'ABS_Y=y1' --device-name 'Joystick' \
  --ui-axismap 'x1^cal:-32537:-455:32561=,x1^dead:-900:700:1=,x1^resp:-32768:-21845:-2000:0:2000:21485:32767=' \
  --ui-axismap 'y1^cal:-32539:-177:32532=,y1^dead:-700:2500:1=,y1^resp:-32768:-21845:-2000:0:2000:21485:32767=' \
  --evdev-absmap 'ABS_RZ=x2' --ui-axismap 'x2^cal:-32000:-100:32000,x2^dead:-1500:1000:1=,x2^resp:-32768:-21845:-2000:0:2000:21485:32767=' \
  --silent

```

this maps the 3 joystick axes to gamepad axes and changes the calibration (min value, centre value, max value), dead zones (negative side, positive side, flag to turn smoothing) and finally change of response curve to a more flat one in the middle.

You can also modify the responsiveness by setting the 'sen' (sensitivity). Setting it to value of 0 will give you a linear sensitivity, value of -1 will give very insensitive axis while value of 1 will give very sensitive axis. You can use intermediate values to make it less or more sensitive. Internally xboxdrv uses a quadratic formula to calculate the resulting value, so this setting gives a more smooth result than 'resp' shown above.

Nice thing about xboxdrv is that it exports resulting device as both old Joystick API and new style evdev API so it should be compatible with basically any application.

## Disable joystick from controlling mouse

If you want to play games with your controller, you might want to disable joystick control over mouse cursor. To do this, edit `/etc/X11/xorg.conf.d/51-joystick.conf` (create if it doesn't exists) so that it looks like this:

 `/etc/X11/xorg.conf.d/51-joystick.conf ` 
```
Section "InputClass"
        Identifier "joystick catchall"
        MatchIsJoystick "on"
        MatchDevicePath "/dev/input/event*"
        Driver "joystick"
        Option "StartKeysEnabled" "False"       #Disable mouse
        Option "StartMouseEnabled" "False"      #support
EndSection
```

## Using Joystick to send keystrokes

A couple joystick to keystroke programs exist like [qjoypad](https://aur.archlinux.org/packages/qjoypad/) or [antimicro](https://aur.archlinux.org/packages/antimicro/), all work well without the need for X.org configuration.

### Xorg configuration example

This is a good solution for systems where restarting Xorg is a rare event because it is a static configuration loaded only on X startup. The example runs on a [Kodi](/index.php/Kodi "Kodi") media PC, controlled with a Logitech Cordless RumblePad 2\. Due to a problem with the d-pad (a.k.a. "hat") being recognized as another axis, [Joy2key](/index.php/Joy2key "Joy2key") was used as a workaround. Since upgrade to Kodi version 11.0 and joy2key 1.6.3-1, this setup no longer worked and the following was created for letting Xorg handle joystick events.

First, [install](/index.php/Install "Install") the [xf86-input-joystick](https://aur.archlinux.org/packages/xf86-input-joystick/) package. Then, create `/etc/X11/xorg.conf.d/51-joystick.conf` like so:

```
 Section "InputClass"
  Identifier "Joystick hat mapping"
  Option "StartKeysEnabled" "True"
  #MatchIsJoystick "on"
  Option "MapAxis5" "keylow=113 keyhigh=114"
  Option "MapAxis6" "keylow=111 keyhigh=116"
 EndSection

```

**Note:** The `MatchIsJoystick "on"` line does not seem to be required for the setup to work, but you may want to uncomment it.

## Specific devices

While most joysticks, especially USB based ones should just work, some may require (or give better results) if you use alternative drivers. If it doesn't work the first time, do not give up, and read those docs thoroughly!

### Dance pads

Most dance pads should work. However some pads, especially those used from a video game console via an adapter, have a tendency to map the directional buttons as axis buttons. This prevents hitting left-right or up-down simultaneously. This behavior can be fixed for devices recognized by xpad via a module option:

```
 # modprobe -r xpad
 # modprobe xpad dpad_to_buttons=1

```

If that did not work, you can try [axisfix-git](https://aur.archlinux.org/packages/axisfix-git/) or patching the `joydev` kernel module ([https://github.com/adiel-mittmann/dancepad](https://github.com/adiel-mittmann/dancepad)).

### Logitech Thunderpad Digital

Logitech Thunderpad Digital won't show all the buttons if you use the `analog` module. Use the device specific `adi` module for this controller.

### Nintendo Gamecube Controller

Dolphin Emulator has a [page on their wiki](https://wiki.dolphin-emu.org/index.php?title=How_to_use_the_Official_GameCube_Controller_Adapter_for_Wii_U_in_Dolphin) that explains how to use the official Nintendo USB adapter with a Gamecube controller. This configuration also works with the Mayflash Controller Adapter if the switch is set to "Wii U".

By default, the controller will register with [udev](/index.php/Udev "Udev"), but will only be readable by the root user. You can fix this by adding a udev device rule, like the below.

 `/etc/udev/rules.d/51-gcadapter.rules`  `SUBSYSTEM=="usb", ENV{DEVTYPE}=="usb_device", ATTRS{idVendor}=="057e", ATTRS{idProduct}=="0337", MODE="0666"` 

This only matches the USB device with the specified vendor and product IDs, which match those of the official USB adapter. It sets the permissions of the device file to 0666 so that programs that aren't running as root can read the device's input.

udev can be reloaded with the new configuration by executing

```
 # udevadm control --reload-rules

```

### Nintendo Switch Pro Controller and Joy-Cons

#### Kernel Nintendo HID Driver

The hid-nintendo kernel HID driver is currently in review on the linux-input mailing list. It is likely to be mainlined for the kernel 5.5 release. The most recent version of the changeset is currently being maintained in this[[1]](https://github.com/DanielOgorchock/linux) git repository. The driver provides support for rumble, battery level, and control of the player and home LEDs. It supports the Nintendo Switch Pro Controller over both USB and bluetooth in addition to the joy-cons.

##### joycond Userspace Daemon

The hid-nintendo kernel driver does not handle the combination of two joy-cons into one virtual input device. That functionality has been left up to userspace. [joycond-git](https://aur.archlinux.org/packages/joycond-git/) is a userspace daemon that combines two kernel joy-con evdev devices into one virtual input device using uinput. An application can use two joy-cons as if they are a single controller. When the daemon is active, switch controllers will be placed in a pseudo pairing mode, and the LEDs will start flashing. Holding the triggers can be used to pair controllers and make them usable. To pair two joy-cons together, press one trigger on each joy-con.

##### Using hid-nintendo with Steam Games

The hid-nintendo driver currently conflicts with steam using hidraw to implement its own pro controller driver. If you wish to use the Steam implementation, the hid-nintendo driver can be blacklisted. Alternatively if you want to use hid-nintendo with a Steam game directly, Steam can be started without access to hidraw using firejail:

```
 $ firejail --noprofile --blacklist=/sys/class/hidraw/ steam

```

##### Using hid-nintendo with SDL2 Games

To add a mapping for the joy-cons or the pro controller to an SDL2 game, [controllermap](https://aur.archlinux.org/packages/controllermap/) can be run in the game's directory of games which have their own gamecontrollerdb.txt file.

Alternatively, the mappings can be added to an environment variable:

 `~/.bashrc` 
```
# hid-nintendo SDL2 mappings
export SDL_GAMECONTROLLERCONFIG="050000007e0500000920000001800000,Nintendo Switch Pro Controller,platform:Linux,a:b0,b:b1,x:b3,y:b2,back:b9,guide:b11,start:b10,leftstick:b12,rightstick:b13,leftshoulder:b5,rightshoulder:b6,dpup:b14,dpdown:b15,dpleft:b16,dpright:b17,leftx:a0,lefty:a1,rightx:a2,righty:a3,lefttrigger:b7,righttrigger:b8,
030000007e0500000920000011810000,Nintendo Switch Pro Controller,platform:Linux,a:b0,b:b1,x:b3,y:b2,back:b9,guide:b11,start:b10,leftstick:b12,rightstick:b13,leftshoulder:b5,rightshoulder:b6,dpup:b14,dpdown:b15,dpleft:b16,dpright:b17,leftx:a0,lefty:a1,rightx:a2,righty:a3,lefttrigger:b7,righttrigger:b8,
060000007e0500000620000000000000,Nintendo Switch Combined Joy-Cons,platform:Linux,a:b0,b:b1,x:b3,y:b2,back:b9,guide:b11,start:b10,leftstick:b12,rightstick:b13,leftshoulder:b5,rightshoulder:b6,dpup:b14,dpdown:b15,dpleft:b16,dpright:b17,leftx:a0,lefty:a1,rightx:a2,righty:a3,lefttrigger:b7,righttrigger:b8,
"
```

#### Dolphin (Gamecube Controller Emulation)

Shinyquagsire23 made a git repo called "HID Joy-Con Whispering"[[2]](https://github.com/shinyquagsire23/HID-Joy-Con-Whispering), which contains a userspace driver for the Joy Cons and the Switch Pro Controller over USB. Currently, it does not support rumble or gyroscope. For rumble support, see the hid-nintendo kernel driver section above.

After running make, load the uinput module:

```
 # modprobe uinput

```

Then to activate the driver:

```
 # ./uinputdriver > /dev/null

```

Over on Dolphin's controller configuration menu, there should be an entry for evdev/0/joycon (not Nintendo Switch Pro Controller). Select it, and you should now be able to configure the controls.

#### Steam

While the controller works for native Linux games, this controller isn't detected by Steam. To fix this, we'll need to add a line to 70-steam-controller.rules.

 `/lib/udev/rules.d/70-steam-controller.rules` 
```
# NS PRO Controller USB
KERNEL=="hidraw*", ATTRS{idVendor}=="20d6", ATTRS{idProduct}=="a711", MODE="0660", TAG+="uaccess"
```

udev can be reloaded with the new configuration by executing

```
 # udevadm control --reload-rules

```

### PlayStation 3/4 controller

The DualShock 3, DualShock 4 and Sixaxis controllers work out of the box when plugged in via USB (the PS button will need to be pushed to begin). They can also be used wirelessly via Bluetooth.

Steam properly recognizes it as a PS3 pad and Big Picture can be launched with the PS button. Big Picture and some games may act as if it was a 360 controller. Gamepad control over mouse is on by default. You may want to turn it off before playing games, see [#Joystick moving mouse](#Joystick_moving_mouse).

##### Connecting via Bluetooth

Install the [bluez](https://www.archlinux.org/packages/?name=bluez), [bluez-plugins](https://www.archlinux.org/packages/?name=bluez-plugins), and [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) packages, which includes the *sixaxis* plugin. Then [start](/index.php/Start "Start") the [bluetooth](/index.php/Bluetooth "Bluetooth") service and ensure bluetooth is powered on. If using *bluetoothctl* start it in a terminal and then plug the controller in via USB. You should be prompted to trust the controller in bluetoothctl. A graphical bluetooth front-end may program your PC's bluetooth address into the controller automatically. Hit the PlayStation button and check that the controller works while plugged in.

You can now disconnect your controller. The next time you hit the PlayStation button it will connect without asking anything else.

Alternatively, on a PS4 controller you can hold the share button and the PlayStation button simultaneously (for a few seconds) to put the gamepad in pairing mode, and pair as you would normally.

GNOME's Settings also provides a graphical interface to pair sixaxis controllers when connected by wire.

Remember to disconnect the controller when you are done as the controller will stay on when connected and drain the battery.

**Note:** If the controller does not connect, make sure the bluetooth interface is turned on and the controllers have been trusted. (See [Bluetooth](/index.php/Bluetooth "Bluetooth"))

##### Using Playstation 3 controllers with Steam

For Steam to recognize your controllers, it needs to be able to read their device file. The [steam](https://www.archlinux.org/packages/?name=steam) package sets up udev rules for lots of controllers, but not the PlayStation 3 controller (aka. DualShock 3 controller). You can add the rules yourself:

 `/etc/udev/rules.d/99-dualshock-3.rules` 
```
# DualShock 3 controller, Bluetooth
KERNEL=="hidraw*", KERNELS=="*054C:0268*", MODE="0660", TAG+="uaccess"

# DualShock 3 controller, USB
KERNEL=="hidraw*", ATTRS{idVendor}=="054c", ATTRS{idProduct}=="0268", MODE="0660", TAG+="uaccess"
```

Make sure your user is in the "input" group:

`usermod -aG input yourusername`

Reboot your system. Steam should now detect your PlayStation 3 controller.

##### Using generic/clone controllers

Using generic/clone Dualshock controllers is possible, however there is an issue that may require to install a patched package. The default Bluetooth protocol stack doesn't detect some of the clone controllers. The [bluez-ps3](https://aur.archlinux.org/packages/bluez-ps3/) package is a version patched to be able to detect them.

### iPEGA-9017s and other Bluetooth gamepads

If you want to use one of the widely available bluetooth gamepads, such as iPEGA-9017s designed mostly for Android and iOS devices you would need [xboxdrv](https://aur.archlinux.org/packages/xboxdrv/), [bluez](https://www.archlinux.org/packages/?name=bluez), [bluez-plugins](https://www.archlinux.org/packages/?name=bluez-plugins), and [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils). You should connect it in gamepad mode (if there are different modes, choose the gamepad one). Technically it's ready to be used, but in most cases games would not recognize it, and you would have to map it individually for all application. The best way to simplify it and make it work with all applications is to mimic Microsoft X360 controller with [xboxdrv](https://aur.archlinux.org/packages/xboxdrv/). Once connected you can create a udev rule to give it a persistent name, that would come in handy when setting it up.

 `/etc/udev/rules.d/99-btjoy.rules` 
```
#Create a symlink to appropriate /dev/input/eventX at /dev/btjoy
ACTION=="add", SUBSYSTEM=="input", ATTRS{name}=="Bluetooth Gamepad", ATTRS{uniq}=="00:17:02:01:ae:2a", SYMLINK+="btjoy"
```

Replace "Bluetooth Gampad" with your device name and "00:17:02:01:ae:2a" with your device's address.

Next, create a configuration for [xboxdrv](https://aur.archlinux.org/packages/xboxdrv/) somewhere, for example:

 `~/.config/xboxdrv/ipega.conf` 
```
#iPEGA PG-9017S Config 

[xboxdrv]
evdev-debug = true
evdev-grab = true
rumble = false
mimic-xpad = true

[evdev-absmap]
ABS_HAT0X = dpad_x
ABS_HAT0Y = dpad_y

ABS_X = X1
ABS_Y = Y1

ABS_Z  = X2
ABS_RZ = Y2

[axismap]
-Y1 = Y1
-Y2 = Y2

[evdev-keymap]
BTN_EAST=a
BTN_C=b
BTN_NORTH=y
BTN_SOUTH=x
BTN_TR2=start
BTN_TL2=back
BTN_Z=rt
BTN_WEST=lt

BTN_MODE = guide
```

Refer to the xboxdrv man to see all the options.

Now when you have the config and your device is connected you can start the [xboxdrv](https://aur.archlinux.org/packages/xboxdrv/) like so:

`sudo xboxdrv --evdev /dev/btjoy --config .config/xboxdrv/ipega.conf`

Your games will now work with bluetooth gamepad as long as xboxdrv is running.

#### iPEGA-9068 and 9087

For this model, use the same procedures as above, but with the configs:

 `~/.config/xboxdrv/ipega.conf` 
```
#iPEGA PG-9068 and PG-9087 Config 

[xboxdrv]
evdev-debug = true
evdev-grab = true
rumble = false
mimic-xpad = true

[evdev-absmap]
ABS_HAT0X = dpad_x
ABS_HAT0Y = dpad_y

ABS_X = X1
ABS_Y = Y1

ABS_Z  = X2
ABS_RZ = Y2

[axismap]
-Y1 = Y1
-Y2 = Y2

[evdev-keymap]
BTN_A=a
BTN_B=b
BTN_Y=y
BTN_X=x
BTN_TR=rb
BTN_TL=lb
BTN_TR2=rt
BTN_TL2=lt
BTN_THUMBL=tl
BTN_THUMBR=tr
BTN_START=start
BTN_SELECT=back

BTN_MODE = guide
```

### Steam Controller

**Note:** Kernel 4.18 [provides a kernel driver](https://lkml.org/lkml/2018/4/16/380) for wired/wireless use of the steam controller as a controller input device without [Steam](/index.php/Steam "Steam").

The [Steam](/index.php/Steam "Steam") client will recognize the controller and provide keyboard/mouse/gamepad emulation while Steam is running. The in-game Steam overlay needs to be enabled and working in order for gamepad emulation to work. You may need to run `udevadm trigger` with root privileges or plug the dongle out and in again, if the controller doesn't work immediately after installing and running Steam. If all else fails, try restarting the computer while the dongle is plugged in.

For Steam client to be able to emulate other gamepads in games, you will need to follow this [post](https://steamcommunity.com/app/353370/discussions/2/1735465524711324558/) from Valve. Note that name of the file with udev rules may be different, for example `/usr/lib/udev/rules.d/70-steam-input.rules`. A reboot may be required after making changes.

If you can't get the Steam Controller to work, see [#Steam Controller not pairing](#Steam_Controller_not_pairing).

Alternatively you can install [python-steamcontroller-git](https://aur.archlinux.org/packages/python-steamcontroller-git/) to have controller and mouse emulation without Steam or [sc-controller](https://aur.archlinux.org/packages/sc-controller/) for a versatile graphical configuration tool simillar to what is provided by the Steam client.

On some desktop environments the on-screen keyboard might freeze when trying to input text after one or two characters. This is a problem with window focus. Check the settings for your [window manager](/index.php/Window_manager "Window manager") to see if it is possible to have focus follow the mouse or automatically focus new windows. Preventing the keyboard from receiving focus will fix the issue in [Awesome](/index.php/Awesome "Awesome"), see [Awesome#Steam Keyboard](/index.php/Awesome#Steam_Keyboard "Awesome").

**Note:** If you do not use the [Steam runtime](/index.php/Steam_runtime "Steam runtime"), you might actually need to disable the overlay for the controller to work in certain games (Rocket Wars, Rocket League, Binding of Isaac, etc.). Right click on a game in your library, select "Properties", and uncheck "Enable Steam Overlay".

#### Wine

[python-steamcontroller-git](https://aur.archlinux.org/packages/python-steamcontroller-git/) can also be used to make the Steam Controller work for games running under Wine. You need to find and download the application `xbox360cemu.v.3.0` (e.g. from [here](https://github.com/jacobmischka/ds4-in-wine/tree/master/xbox360cemu.v.3.0)). Then copy the files `dinput8.dll`, `xbox360cemu.ini`, `xinput1_3.dll` and `xinput_9_1_0.dll` to the directory that contains your game executable. Edit `xbox360cemu.ini` and only change the following values under `[PAD1]` to remap the Steam Controller correctly to a XBox controller.

 `xbox360cemu.ini` 
```
Right Analog X=4
Right Analog Y=-5
A=1
B=2
X=3
Y=4
Back=7
Start=8
Left Thumb=10
Right Thumb=11
Left Trigger=a3
Right Trigger=a6
```

Now start python-steamcontroller in Xbox360 mode (`sc-xbox.py start`). You might also want to copy `XInputTest.exe` from `xbox360cemu.v.3.0` to the same directory and run it with Wine in order to test if the mappings work correctly. However neither mouse nor keyboard emulation work with this method.

Alternatively you can use [sc-controller](https://aur.archlinux.org/packages/sc-controller/) for a similar graphical setup as Steam's own configurator. As of writing, it's a bit buggy here and there but offers an easy click and go way of configuring the controller.

### Xbox 360 controller

Both the wired and wireless (with the *Xbox 360 Wireless Receiver for Windows*) controllers are supported by the `xpad` kernel module and should work without additional packages. (Note that using a wireless Xbox360 controller with the Play&Charge USB cable will not work. The cable is for recharging only and does not transmit any input data over the wire.)

It has been reported that the default xpad driver has some issues with a few newer wired and wireless controllers, such as:

*   incorrect button mapping. ([discussion in Steam bugtracker](https://github.com/ValveSoftware/steam-for-linux/issues/95#issuecomment-14009081))
*   not-working sync. All four LEDs keep blinking, but controller works. ([discussion in Arch Forum](https://bbs.archlinux.org/viewtopic.php?id=156028))

If you experience such issues, you can use either [#SteamOS xpad](#SteamOS_xpad) or [#xboxdrv](#xboxdrv) instead of the default `xpad` driver.

If you wish to use the controller for controlling the mouse, or mapping buttons to keys, etc. you should use the [xf86-input-joystick](https://aur.archlinux.org/packages/xf86-input-joystick/) package (configuration help can be found using joystick(4)). If the mouse locks itself in a corner, it might help changing the `MatchDevicePath` in `/etc/X11/xorg.conf.d/50-joystick.conf` from `/dev/input/event*` to `/dev/input/js*`.

**Tip:** If you use the [TLP](/index.php/TLP "TLP") power management tool, you may experience connection issues with your Microsoft wireless adapter (e.g. the indicator LED will go out after the adapter has been connected for a few seconds, and controller connection attempts fail). This is due to TLP's USB autosuspend functionality, and the solution is to add the Microsoft wireless adapter's device ID to this feature's blacklist (USB_BLACKLIST, check [TLP configuration](http://linrunner.de/en/tlp/docs/tlp-configuration.html#usb) for more details).

In order to connect via Bluetooth using KDE, add the following [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `bluetooth.disable_ertm=1`.

#### SteamOS xpad

If you have issues with the default `xpad` kernel module, you can install the SteamOS version. There is still a known issue with compatibility between wireless Xbox360 controllers and games made in GameMaker Studio. If you encounter this problem, the only known workaround is to use xboxdrv. YoYo Games has refused to acknowledge this as a bug with their product and it is unlikely to ever be fixed.

First make sure you have [DKMS](/index.php/DKMS "DKMS") installed and running, then install the modified kernel module [steamos-xpad-dkms](https://aur.archlinux.org/packages/steamos-xpad-dkms/). During the installation you'll see that new xpad kernel module is strapped to your current kernel:

```
Creating symlink /var/lib/dkms/steamos-xpad-dkms/0.1/source ->
                 /usr/src/steamos-xpad-dkms-0.1

DKMS: add completed.

Kernel preparation unnecessary for this kernel.  Skipping...

Building module:
cleaning build area....
make KERNELRELEASE=3.12.8-1-ARCH KVERSION=3.12.8-1-ARCH....
cleaning build area....

```

Then unload the old xpad module and load new one:

```
# rmmod xpad
# modprobe steamos-xpad

```

Or just restart your computer.

#### xboxdrv

xboxdrv is an alternative to `xpad` which provides more functionality and might work better with certain controllers. It works in userspace and can be launched as system service.

Install it with the [xboxdrv](https://aur.archlinux.org/packages/xboxdrv/) package. Then [start](/index.php/Start "Start")/[enable](/index.php/Enable "Enable") `xboxdrv.service`.

If you have issues with the controller being recognized but not working in steam games or working but with incorrect mappings, it may be required to modify you config as such:

 `/etc/default/xboxdrv` 
```
[xboxdrv]
silent = true
device-name = "Xbox 360 Wireless Receiver"
mimic-xpad = true
deadzone = 4000

[xboxdrv-daemon]
dbus = disabled
```

Then [restart](/index.php/Restart "Restart") `xboxdrv.service`.

##### Multiple controllers

xboxdrv supports a multitude of controllers, but they need to be set up in `/etc/default/xboxdrv`. For each extra controller, add an `next-controller = true` line. For example, when using 4 controllers, add it 3 times:

```
 [xboxdrv]
 silent = true
 next-controller = true
 next-controller = true
 next-controller = true
 [xboxdrv-daemon]
 dbus = disabled

```

Then [restart](/index.php/Restart "Restart") `xboxdrv.service`.

##### Mimic Xbox 360 controller with other controllers

xboxdrv can be used to make any controller register as an Xbox 360 controller with the `--mimic-xpad` switch. This may be desirable for games that support Xbox 360 controllers out of the box, but have trouble detecting or working with other gamepads.

First, you need to find out what each button and axis on the controller is called. You can use [evtest](https://www.archlinux.org/packages/?name=evtest) for this. Run `evtest` and select the device event ID number (`/dev/input/event*`) that corresponds to your controller. Press the buttons on the controller and move the axes to read the names of each button and axis.

Here is an example of the output:

```

Event: time 1380985017.964843, type 4 (EV_MSC), code 4 (MSC_SCAN), value 90003
Event: time 1380985017.964843, type 1 (EV_KEY), code 290 (BTN_THUMB2), value 1
Event: time 1380985017.964843, -------------- SYN_REPORT ------------
Event: time 1380985018.076843, type 4 (EV_MSC), code 4 (MSC_SCAN), value 90003
Event: time 1380985018.076843, type 1 (EV_KEY), code 290 (BTN_THUMB2), value 0
Event: time 1380985018.076843, -------------- SYN_REPORT ------------
Event: time 1380985018.460841, type 4 (EV_MSC), code 4 (MSC_SCAN), value 90002
Event: time 1380985018.460841, type 1 (EV_KEY), code 289 (BTN_THUMB), value 1
Event: time 1380985018.460841, -------------- SYN_REPORT ------------
Event: time 1380985018.572835, type 4 (EV_MSC), code 4 (MSC_SCAN), value 90002
Event: time 1380985018.572835, type 1 (EV_KEY), code 289 (BTN_THUMB), value 0
Event: time 1380985018.572835, -------------- SYN_REPORT ------------
Event: time 1380985019.980824, type 4 (EV_MSC), code 4 (MSC_SCAN), value 90006
Event: time 1380985019.980824, type 1 (EV_KEY), code 293 (BTN_PINKIE), value 1
Event: time 1380985019.980824, -------------- SYN_REPORT ------------
Event: time 1380985020.092835, type 4 (EV_MSC), code 4 (MSC_SCAN), value 90006
Event: time 1380985020.092835, type 1 (EV_KEY), code 293 (BTN_PINKIE), value 0
Event: time 1380985020.092835, -------------- SYN_REPORT ------------
Event: time 1380985023.596806, type 3 (EV_ABS), code 3 (ABS_RX), value 18
Event: time 1380985023.596806, -------------- SYN_REPORT ------------
Event: time 1380985023.612811, type 3 (EV_ABS), code 3 (ABS_RX), value 0
Event: time 1380985023.612811, -------------- SYN_REPORT ------------
Event: time 1380985023.708768, type 3 (EV_ABS), code 3 (ABS_RX), value 14
Event: time 1380985023.708768, -------------- SYN_REPORT ------------
Event: time 1380985023.724772, type 3 (EV_ABS), code 3 (ABS_RX), value 128
Event: time 1380985023.724772, -------------- SYN_REPORT ------------

```

In this case, `BTN_THUMB`, `BTN_THUMB2` and `BTN_PINKIE` are buttons and `ABS_RX` is the X axis of the right analogue stick. You can now mimic an Xbox 360 controller with the following command:

```
$ xboxdrv --evdev /dev/input/event* --evdev-absmap ABS_RX=X2 --evdev-keymap BTN_THUMB2=a,BTN_THUMB=b,BTN_PINKIE=rt --mimic-xpad

```

The above example is incomplete. It only maps one axis and 3 buttons for demonstration purposes. Use `xboxdrv --help-button` to see the names of the Xbox controller buttons and axes and bind them accordingly by expanding the command above. Axes mappings should go after `--evdev-absmap` and button mappings follow `--evdev-keymap` (comma separated list; no spaces).

By default, xboxdrv outputs all events to the terminal. You can use this to test that the mappings are correct. Append the `--silent` option to keep it quiet.

#### Using generic/clone controllers

Some clone gamepads might require a specific initialization sequence in order to work ([Super User answer](https://superuser.com/a/1380235/303390)). For that you should run the following python script with sudo:

```
#!/usr/bin/env python3

import usb.core

dev = usb.core.find(idVendor=0x045e, idProduct=0x028e)

if dev is None:
    raise ValueError('Device not found')
else:
    dev.ctrl_transfer(0xc1, 0x01, 0x0100, 0x00, 0x14) 

```

### Xbox Wireless Controller / Xbox One Wireless Controller

#### Connect Xbox Wireless Controller with usb cable

This is supported by the kernel and should work without additional packages.

#### Connect Xbox Wireless Controller with Bluetooth

You will probably have to disable Enhanced Retransmission Mode (ERTM) to make it work.

Use either:

```
# echo 1 > /sys/module/bluetooth/parameters/disable_ertm

```

Or add this file to your module configuration:

 `/etc/modprobe.d/xbox_bt.conf`  `options bluetooth disable_ertm=1` 

##### xpadneo

A relatively new driver which does (yet) support only the Xbox One S controller via Bluetooth is called [xpadneo](https://github.com/atar-axis/xpadneo/). In exchange for supporting just one controller so far, it enables one to read out the correct battery level, supports rumble (even the one on the trigger buttons - L2/R2), corrects the (sometimes wrong) button mapping and more.

Installation is done using DKMS: [xpadneo-dkms-git](https://aur.archlinux.org/packages/xpadneo-dkms-git/)

#### Connect Xbox Wireless Controller with Microsoft Xbox Wireless Adapter

##### xow

[xow](https://github.com/medusalix/xow) is a project that allows connection with a wireless dongle. It is currently in very early stages of development. It can be installed via [xow-git](https://aur.archlinux.org/packages/xow-git/)

### Logitech Dual Action

The Logitech Dual Action gamepad has a very similar mapping to the PS2 pad, but some buttons and triggers need to be swapped to mimic the Xbox controller.

```
 # xboxdrv --evdev /dev/input/event* \
   --evdev-absmap ABS_X=x1,ABS_Y=y1,ABS_RZ=x2,ABS_Z=y2,ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \
   --axismap -Y1=Y1,-Y2=Y2 \
   --evdev-keymap BTN_TRIGGER=x,BTN_TOP=y,BTN_THUMB=a,BTN_THUMB2=b,BTN_BASE3=back,BTN_BASE4=start,BTN_BASE=lt,BTN_BASE2=rt,BTN_TOP2=lb,BTN_PINKIE=rb,BTN_BASE5=tl,BTN_BASE6=tr \
   --mimic-xpad --silent

```

### PlayStation 2 controller via USB adapter

To fix the button mapping of PS2 dual adapters and mimic the Xbox controller you can run the following command:

```
 # xboxdrv --evdev /dev/input/event* \
   --evdev-absmap ABS_X=x1,ABS_Y=y1,ABS_RZ=x2,ABS_Z=y2,ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \
   --axismap -Y1=Y1,-Y2=Y2 \
   --evdev-keymap   BTN_TOP=x,BTN_TRIGGER=y,BTN_THUMB2=a,BTN_THUMB=b,BTN_BASE3=back,BTN_BASE4=start,BTN_BASE=lb,BTN_BASE2=rb,BTN_TOP2=lt,BTN_PINKIE=rt,BTN_BASE5=tl,BTN_BASE6=tr \
   --mimic-xpad --silent

```

### PlayStation 3 controller via USB

If you own a PS3 controller and can connect with USB, xboxdrv has the mappings built in. Just run the program (and detach the running driver) and it works!

```
# xboxdrv --silent --detach-kernel-driver

```

There are some games which might also need the `--mimic-xpad` option, additionally.

### PlayStation 3 controller via Bluetooth

With your controller connected via Bluetooth, find the device address with `bluetoothctl`. Then create a new udev rule with the following content:

 `/etc/udev/rules.d/99-dualshock.rules`  `KERNEL=="event*", SUBSYSTEM=="input", ATTRS{uniq}=="<device_addr_you_got_on_pairing>", SYMLINK+="input/dualshock3"` 

The address must be in lowercase, like `06:9a:b4:c8:ef:8b`.

Now run xboxdrv over the new device:

```
$ xboxdrv --evdev /dev/input/dualshock3 --mimic-xpad

```

### PlayStation 4 controller

#### Button mapping

To fix the button mapping of PS4 controller you can use the following command with xboxdrv (or try with the [ds4drv](https://github.com/chrippa/ds4drv) program):

```
 # xboxdrv \
   --evdev /dev/input/by-id/usb-Sony_Computer_Entertainment_Wireless_Controller-event-joystick\
   --evdev-absmap ABS_X=x1,ABS_Y=y1                 \
   --evdev-absmap ABS_Z=x2,ABS_RZ=y2                \
   --evdev-absmap ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \
   --evdev-keymap BTN_A=x,BTN_B=a                   \
   --evdev-keymap BTN_C=b,BTN_X=y                   \
   --evdev-keymap BTN_Y=lb,BTN_Z=rb                 \
   --evdev-keymap BTN_TL=lt,BTN_TR=rt               \
   --evdev-keymap BTN_SELECT=tl,BTN_START=tr        \
   --evdev-keymap BTN_TL2=back,BTN_TR2=start        \
   --evdev-keymap BTN_MODE=guide                    \
   --axismap -y1=y1,-y2=y2                          \
   --mimic-xpad                                     \
   --silent

```

#### Fix Motion control conflict (gamepad won't work on somes apps)

Dualshock 4 V1 and V2 are both like 3 devices, touchpad, motion control, and joypad.

With somes softwares like Parsec and Shadow cloud gaming streaming apps, motion control is in conflict with joypad, you can disable touchpad and motion control by adding the following udev rule :

 `/etc/udev/rules.d/51-disable-DS3-and-DS4-motion-controls.rules` 
```
SUBSYSTEM=="input", ATTRS{name}=="*Controller Motion Sensors", RUN+="/bin/rm %E{DEVNAME}", ENV{ID_INPUT_JOYSTICK}=""
SUBSYSTEM=="input", ATTRS{name}=="*Controller Touchpad", RUN+="/bin/rm %E{DEVNAME}", ENV{ID_INPUT_JOYSTICK}=""
```

This should work in USB and Bluetooth mode. (If you want use bluetooth mode, press "home" button and "share" button together, white led of gamepad should blink very quickly, then add wireless controller with your bluetooth manager (bluez, gnome-bluetooth...)

#### Disable touchpad acting as mouse

This fixes conflicts with games that actually use touchpad as part of the gamepad, such as Rise of the Tomb Raider.

`sudo vim /etc/X11/xorg.conf.d/30ds4.conf`

And then paste the following and restart X11:

```
Section "InputClass"
       Identifier   "ds4-touchpad"
       Driver       "libinput"
       MatchProduct "Sony Interactive Entertainment Wireless Controller Touchpad"
       Option       "Ignore" "True"
EndSection

```

## Troubleshooting

### Joystick moving mouse

Sometimes USB joystick can be recognized as HID mouse (only in X, it is still being installed as `/dev/input/js0` as well). Known issue is cursor being moved by the joystick, or escaping to en edge of a screen right after plugin. If your application can detect joystick by it self, you can remove the [xf86-input-joystick](https://aur.archlinux.org/packages/xf86-input-joystick/) package.

A more gentle solution is described in [#Disable joystick from controlling mouse](#Disable_joystick_from_controlling_mouse).

### Joystick not working in FNA/SDL based games

If you are using a generic non-widely used gamepad you may encounter issues getting the gamepad recognized in games based on SDL. Since [14 May 2015](https://github.com/flibitijibibo/FNA/commit/e55742cfe7e38b778a21ed8a12cb2f2081490d8d), FNA supports dropping a `gamecontrollerdb.txt` into the executable folder of the game, for example the [SDL_GameControllerDB](https://github.com/gabomdq/SDL_GameControllerDB).

As an alternative and for older versions of FNA or for SDL you can generate a mapping yourself by downloading the SDL source code via [http://libsdl.org/](http://libsdl.org/), navigating to `/test/`, compile the `controllermap.c` program (alternatively install [controllermap](https://aur.archlinux.org/packages/controllermap/)) and run the test. After completing the controllermap test, a guid will be generated that you can put in the `SDL_GAMECONTROLLERCONFIG` environment variable which will then be picked up by SDL/FNA games. For example:

```
 $ export SDL_GAMECONTROLLERCONFIG="030000008f0e00000300000010010000,GreenAsia Inc. USB Joystick ,platform:Linux,x:b3,a:b2,b:b1,y:b0,back:b8,start:b9,dpleft:h0.8,dpdown:h0.0,dpdown:h0.4,dpright:h0.0,dpright:h0.2,dpup:h0.0,dpup:h0.1,leftshoulder:h0.0,leftshoulder:b6,lefttrigger:b4,rightshoulder:b7,righttrigger:b5,leftstick:b10,rightstick:b11,leftx:a0,lefty:a1,rightx:a3,righty:a2,"

```

### Joystick not recognized by all programs

Some software, Steam for example, will only recognize the first joystick it encounters. Due to a bug in the driver for Microsoft wireless periphery devices this can in fact be the bluetooth dongle. If you find you have a `/dev/input/js*` and `/dev/input/event*` belonging to you keyboard's bluetooth transceiver you can get automatically get rid of it by creating according udev rules. Create a `/`:

 `/etc/udev/rules.d/99-btcleanup.rules` 
```
ACTION=="add", KERNEL=="js[0-9]*", SUBSYSTEM=="input", KERNELS=="...", ATTRS{bInterfaceSubClass}=="00", ATTRS{bInterfaceProtocol}=="00", ATTRS{bInterfaceNumber}=="02", RUN+="/usr/bin/rm /dev/input/js%n"
ACTION=="add", KERNEL=="event*", SUBSYSTEM=="input", KERNELS=="...", ATTRS{bInterfaceSubClass}=="00", ATTRS{bInterfaceProtocol}=="00", ATTRS{bInterfaceNumber}=="02", RUN+="/usr/bin/rm /dev/input/event%n"

```

Correct the `KERNELS=="..."` to match your device. The correct value can be found by running

```
# udevadm info -an /dev/input/js0

```

Assuming the device in question is `/dev/input/js0`. After you placed the rule reload the rules with

```
# udevadm control --reload

```

Then replug the device making you trouble. The joystick and event devices should be gone, although their number will still be reserved. But the files are out of the way.

### Steam Controller not pairing

There are some unknown cases where the packaged udev rule for the Steam controller does not work ([FS#47330](https://bugs.archlinux.org/task/47330)). The most reliable workaround is to make the controller world readable. Copy the rule `/usr/lib/udev/rules.d/70-steam-controller.rules` to `/etc/udev/rules.d` with a later prioritiy and change anything that says `MODE="0660"` to `MODE="066**6**"` e.g.

 `/etc/udev/rules.d/99-steam-controller-perms.rules` 
```
...
SUBSYSTEM=="usb", ATTRS{idVendor}=="28de", MODE="0666"
...

```

You may have to reboot in order for the change to take effect.

### Steam Controller makes a game crash or not recognized

If your Steam Controller is working well in Steam Big Picture mode, but not recognized by a game or the game starts crashing when you plug in the controller, this may be because of the native driver that has been added to the Linux kernel 4.18\. Try to unload it, restart Steam and replug the controller.

The module name of the driver is *hid_steam*, so to unload it you may perform:

```
# sudo rmmod hid_steam

```