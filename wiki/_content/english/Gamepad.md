Joysticks can be a bit of a hassle to get working in Linux. Not because they are poorly supported, but simply because you need to determine which modules to load to get your joystick working, and it's not always very obvious!

## Contents

*   [1 Joystick Input Systems](#Joystick_Input_Systems)
*   [2 Determining which modules you need](#Determining_which_modules_you_need)
    *   [2.1 Loading the modules for analogue devices](#Loading_the_modules_for_analogue_devices)
    *   [2.2 USB joysticks](#USB_joysticks)
*   [3 Testing Your Configuration](#Testing_Your_Configuration)
    *   [3.1 Joystick API](#Joystick_API)
    *   [3.2 evdev API](#evdev_API)
*   [4 Setting up deadzones and calibration](#Setting_up_deadzones_and_calibration)
    *   [4.1 Wine deadzones](#Wine_deadzones)
    *   [4.2 Xorg deadzones](#Xorg_deadzones)
    *   [4.3 Joystick API deadzones](#Joystick_API_deadzones)
    *   [4.4 evdev API deadzones](#evdev_API_deadzones)
    *   [4.5 Configuring curves and responsivness](#Configuring_curves_and_responsivness)
*   [5 Disable Joystick From Controlling Mouse](#Disable_Joystick_From_Controlling_Mouse)
*   [6 Using Joystick to send keystrokes](#Using_Joystick_to_send_keystrokes)
    *   [6.1 Xorg configuration example](#Xorg_configuration_example)
*   [7 Specific devices](#Specific_devices)
    *   [7.1 Dance pads](#Dance_pads)
    *   [7.2 Logitech Thunderpad Digital](#Logitech_Thunderpad_Digital)
    *   [7.3 Nintendo Gamecube Controller](#Nintendo_Gamecube_Controller)
    *   [7.4 PlayStation 3/4 controller](#PlayStation_3.2F4_controller)
        *   [7.4.1 Connecting via Bluetooth](#Connecting_via_Bluetooth)
    *   [7.5 Steam Controller](#Steam_Controller)
        *   [7.5.1 Wine](#Wine)
    *   [7.6 Xbox 360 controller](#Xbox_360_controller)
        *   [7.6.1 SteamOS xpad](#SteamOS_xpad)
        *   [7.6.2 xboxdrv](#xboxdrv)
            *   [7.6.2.1 Multiple controllers](#Multiple_controllers)
            *   [7.6.2.2 Mimic Xbox 360 controller with other controllers](#Mimic_Xbox_360_controller_with_other_controllers)
                *   [7.6.2.2.1 Logitech Dual Action](#Logitech_Dual_Action)
                *   [7.6.2.2.2 PlayStation 2 controller via USB adapter](#PlayStation_2_controller_via_USB_adapter)
                *   [7.6.2.2.3 PlayStation 3 controller via USB](#PlayStation_3_controller_via_USB)
                *   [7.6.2.2.4 PlayStation 3 controller via Bluetooth](#PlayStation_3_controller_via_Bluetooth)
                *   [7.6.2.2.5 PlayStation 4 controller](#PlayStation_4_controller)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Joystick moving mouse](#Joystick_moving_mouse)
    *   [8.2 Joystick not working in FNA/SDL based games](#Joystick_not_working_in_FNA.2FSDL_based_games)
    *   [8.3 Joystick not recognized by all programs](#Joystick_not_recognized_by_all_programs)
    *   [8.4 Steam Controller Not Pairing](#Steam_Controller_Not_Pairing)

## Joystick Input Systems

Linux actually has 2 different input systems for Joysticks. The original 'Joystick' interface and the newer 'evdev' based one.

`/dev/input/jsX` maps to the 'Joystick' API interface and `/dev/input/event*` maps to the 'evdev' ones (this also includes other input devices such as mice and keyboards). Symbolic links to those devices are also available in `/dev/input/by-id/` and `/dev/input/by-path/` where the legacy 'Joystick' API has names ending with `-joystick` while the 'evdev' have names ending with `-event-joystick`.

Most new games will default to the 'evdev' interface as it gives more detailed information about the buttons and axes available and also adds support for force feedback.

While SDL1.x defaults to 'evdev' interface you can force it to use the old 'Joystick' API by setting the environment variable `SDL_JOYSTICK_DEVICE=/dev/input/js0`. This can help many games such as X3\. SDL2.x supports only the new 'evdev' interface.

It's also worth mentioning that there is also a xorg driver `xf86-input-joystick`. It just allows you to control the mouse/keyboard in xorg using a joystick, for most people this will be undesirable. Disabling this behaviour is described below in [Disable Joystick From Controlling Mouse](#Disable_Joystick_From_Controlling_Mouse), in most cases you can just remove this package though.

## Determining which modules you need

Unless you're using very old joystick that uses gameport or proprietary USB protocol, you will need just the generic USB human interface device (HID) modules.

For an extensive overview of all joystick related modules in Linux, you will need access to the Linux kernel sources -- specifically the Documentation section. Unfortunately, pacman kernel packages do not include what we need. If you have the kernel sources downloaded, have a look at `Documentation/input/joystick.txt`. You can browse the kernel source tree at [kernel.org](https://kernel.org/) by clicking the "browse" (cgit - the git frontend) link for the kernel that you're using, then clicking the "tree" link near the top. Here's a link to the [documentation from the latest kernel](https://git.kernel.org/cgit/linux/kernel/git/stable/linux-stable.git/tree/Documentation/input/joystick.txt).

Some joysticks need specific modules, such as the Microsoft Sidewinder controllers (`sidewinder`), or the Logitech digital controllers (`adi`). Many older joysticks will work with the simple `analog` module. If your joystick is plugging in to a gameport provided by your soundcard, you will need your soundcard drivers loaded - however, some cards, like the Soundblaster Live, have a specific gameport driver (`emu10k1-gp`). Older ISA soundcards may need the `ns558` module, which is a standard gameport module.

As you can see, there are many different modules related to getting your joystick working in Linux, so I couldn't possibly cover everything here. Please have a look at the documentation mentioned above for details.

### Loading the modules for analogue devices

You need to load a module for your gameport (`ns558`, `emu10k1-gp`, `cs461x`, etc...), a module for your joystick (`analog`, `sidewinder`, `adi`, etc...), and finally the kernel joystick device driver (`joydev`). Add these to a new file in `/etc/modules-load.d/`, or simply modprobe them. The `gameport` module should load automatically, as this is a dependency of the other modules.

### USB joysticks

You need to get USB working, and then modprobe your joystick driver, which is `usbhid`, as well as `joydev`. If you use a usb mouse or keyboard, `usbhid` will be loaded already and you just have to load the `joydev` module.

## Testing Your Configuration

Once the modules are loaded, you should be able to find a new device: `/dev/input/js0` and a file ending with `-event-joystick` in `/dev/input/by-id` directory. You can simply `cat` those devices to see if the joystick works - move the stick around, press all the buttons - you should see mojibake printed when you move the sticks or press buttons.

Both interfaces are also supported in wine and reported as separate devices. You can test them with `wine control joy.cpl`.

**Tip:** Input devices by default have **input** group, for example [pcsx2](https://www.archlinux.org/packages/?name=pcsx2) have no access to gamepad without rights. Make sure your user in **input** group.

### Joystick API

There are a lot of applications that can test this old API, `jstest` from the [joyutils](https://www.archlinux.org/packages/?name=joyutils) package is the simplest one. If the output is unreadable because the line printed is too long you can also use graphical tools. KDE4 has a built in one in Input Devices panel in System Settings or [jstest-gtk-git](https://aur.archlinux.org/packages/jstest-gtk-git/) is an alternative.

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

Add a similar line into your `/etc/X11/xorg.conf.d/50-joystick.conf` before the `EndSection`:

```
Option "MapAxis1" "deadzone=1000"

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
SUBSYSTEM=="input", ATTRS{idVendor}=="054c", ATTRS{idProduct}=="c268", ACTION=="add", RUN+="/usr/bin/jscal.sh"

```

To get the idVendor and idProduct use `udevadm info --attribute-walk --name /dev/input/jsX`

Use the `/dev/input/by-id/*-joystick` device names in case you use multiple controllers.

### evdev API deadzones

Currently there is no standalone application that allows changing calibration for `evdev` API, but there is `G25manage` distributed together with VDrift game that can change the center deadzone.

The easiest way to get it is to go to VDrift [github](https://github.com/VDrift/vdrift/tree/master/tools/G25manage), download all files in the folder and build them using `make`.

After that, you should be able to see your device configuration by using:

```
$ ./G25manage --showcalibration /dev/input/by-id/usb-*-event-joystick

```

To change deadzones of any of the axes, you use the following command:

```
$ ./G25manage --evdev /dev/input/by-id/usb-*-event-joystick --axis 0 --deadzone 0

```

Use udev rules file to set them automatically when the controller is connected.

Note that inside the kernel, the value is called `flatness` and is set using the `EVIOCSABS` `ioctl`.

Default configuration will look like similar to this:

 `$ ./G25manage --showcalibration /dev/input/by-id/usb-Madcatz_Saitek_Pro_Flight_X-55_Rhino_Stick_G0000090-event-joystick` 
```
Supported Absolute axes:
   Absolute axis 0x00 (0) (X Axis) (min: 0, max: 65535, flatness: 4095 (=6.25%), fuzz: 255)
   Absolute axis 0x01 (1) (Y Axis) (min: 0, max: 65535, flatness: 4095 (=6.25%), fuzz: 255)
   Absolute axis 0x05 (5) (Z Rate Axis) (min: 0, max: 4095, flatness: 255 (=6.23%), fuzz: 15)
   Absolute axis 0x10 (16) (Hat zero, x axis) (min: -1, max: 1, flatness: 0 (=0.00%), fuzz: 0)
   Absolute axis 0x11 (17) (Hat zero, y axis) (min: -1, max: 1, flatness: 0 (=0.00%), fuzz: 0)
```

While a more reasonable setting would be achieved with something like this (repeat for other axes):

 `$ ./G25manage --evdev /dev/input/by-id/usb-Madcatz_Saitek_Pro_Flight_X-55_Rhino_Stick_G0000090-event-joystick --axis 0 --deadzone 512` 
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

## Disable Joystick From Controlling Mouse

If you want to play games with your controller, you might want to disable joystick control over mouse cursor. To do this, edit /etc/X11/xorg.conf.d/50-joystick.conf so that it looks like this:

 `/etc/X11/xorg.conf.d/50-joystick.conf ` 
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

First, make sure you have [xf86-input-joystick](https://www.archlinux.org/packages/?name=xf86-input-joystick) installed. Then, create `/etc/X11/xorg.conf.d/51-joystick.conf` like so:

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

### PlayStation 3/4 controller

The DualShock 3, DualShock 4 and Sixaxis controllers work out of the box when plugged in via USB (the PS button will need to be pushed to begin). They can also be used wirelessly via Bluetooth.

Steam properly recognizes it as a PS3 pad and Big Picture can be launched with the PS button. Big Picture and some games may act as if it was a 360 controller. Gamepad control over mouse is on by default. You may want to turn it off before playing games, see [#Joystick moving mouse](#Joystick_moving_mouse).

##### Connecting via Bluetooth

Install the [bluez-plugins](https://www.archlinux.org/packages/?name=bluez-plugins) and [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) packages, which includes the *sixaxis* plugin. Then [start](/index.php/Start "Start") `bluetooth.service`, plug the controller in via USB, and the plugin should program your PC's bluetooth address into the controller automatically.

You can now disconnect your controller. The next time you hit the PlayStation button it will connect without asking anything else.

Remember to disconnect the controller when you are done as the controller will stay on when connected and drain the battery.

### Steam Controller

The [steam](https://www.archlinux.org/packages/?name=steam) package (starting from version 1.0.0.51-1) will recognize the controller and provide keyboard/mouse/gamepad emulation while Steam is running. The in-game Steam overlay needs to be enabled and working in order for gamepad emulation to work. You may need to run `udevadm trigger` with root privileges or plug the dongle out and in again, if the controller doesn't work immediately after installing and running steam. If all else fails, try restarting the computer while the dongle is plugged in.

If you can't get the Steam Controller to work, see [#Steam Controller Not Pairing](#Steam_Controller_Not_Pairing).

Alternatively you can install [python-steamcontroller-git](https://aur.archlinux.org/packages/python-steamcontroller-git/) to have controller and mouse emulation without Steam.

On some desktop environments the on screen keyboard might freeze when trying to input text after two characters. This is a problem with focus and can be fixed by opening Window Manager, opening focus tab and unticking 'Automatically give focus to newly created windows'.

#### Wine

[python-steamcontroller-git](https://aur.archlinux.org/packages/python-steamcontroller-git/) can also be used to make the Steam Controller work for games running under Wine. You need to find and download the file `xbox360cemu.v.3.0.rar` (e.g. from here: [Download Link from 2shared](http://www.2shared.com/file/wcq8xuPf/xbox360cemuv30.html)). Then copy the files `dinput8.dll`, `xbox360cemu.ini`, `xinput1_3.dll` and `xinput_9_1_0.dll` to the directory that contains your game executable. Edit `xbox360cemu.ini` and only change the following values under `[PAD1]` to remap the Steam Controller correctly to a XBox Controller.

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

Now start python-steamcontroller in Xbox360 mode (`sc-xbox.py start`). You might also want to copy `XInputTest.exe` from `xbox360cemu.v.3.0.rar` to the same directory and run it with Wine in order to test if it works. However neither mouse nor keyboard emulation work with this method.

### Xbox 360 controller

Both the wired and wireless (with the *Xbox 360 Wireless Receiver for Windows*) controllers are supported by the `xpad` kernel module and should work without additional packages.

It has been reported that the default xpad driver has some issues with a few newer wired and wireless controllers, such as:

*   incorrect button mapping. ([discussion in Steam bugtracker](https://github.com/ValveSoftware/steam-for-linux/issues/95#issuecomment-14009081))
*   not-working sync. All four leds keep blinking, but controller works. ([discussion in Arch Forum](https://bbs.archlinux.org/viewtopic.php?id=156028))

If you experience such issues, you can use either [#SteamOS xpad](#SteamOS_xpad) or [#xboxdrv](#xboxdrv) instead of the default `xpad` driver.

If you wish to use the controller for controlling the mouse, or mapping buttons to keys, etc. you should use the [xf86-input-joystick](https://www.archlinux.org/packages/?name=xf86-input-joystick) package (configuration help can be found using `man joystick`). If the mouse locks itself in a corner, it might help changing the `MatchDevicePath` in `/etc/X11/xorg.conf.d/50-joystick.conf` from `/dev/input/event*` to `/dev/input/js*`.

**Tip:** If you use the [TLP](/index.php/TLP "TLP") power management tool, you may experience connection issues with your Microsoft wireless adapter (e.g. the indicator LED will go out after the adapter has been connected for a few seconds, and controller connection attempts fail). This is due to TLP's USB autosuspend functionality, and the solution is to add the Microsoft wireless adapter's device ID to this feature's blacklist (USB_BLACKLIST, check [TLP configuration](http://linrunner.de/en/tlp/docs/tlp-configuration.html#usb) for more details).

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

 `/etc/default/xboxdrv/` 
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

###### Logitech Dual Action

The Logitech Dual Action gamepad has a very similar mapping to the PS2 pad, but some buttons and triggers need to be swapped to mimic the Xbox controller.

```
 # xboxdrv --evdev /dev/input/event* \
   --evdev-absmap ABS_X=x1,ABS_Y=y1,ABS_RZ=x2,ABS_Z=y2,ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \
   --axismap -Y1=Y1,-Y2=Y2 \
   --evdev-keymap BTN_TRIGGER=x,BTN_TOP=y,BTN_THUMB=a,BTN_THUMB2=b,BTN_BASE3=back,BTN_BASE4=start,BTN_BASE=lt,BTN_BASE2=rt,BTN_TOP2=lb,BTN_PINKIE=rb,BTN_BASE5=tl,BTN_BASE6=tr \
   --mimic-xpad --silent

```

###### PlayStation 2 controller via USB adapter

To fix the button mapping of PS2 dual adapters and mimic the Xbox controller you can run the following command:

```
 # xboxdrv --evdev /dev/input/event* \
   --evdev-absmap ABS_X=x1,ABS_Y=y1,ABS_RZ=x2,ABS_Z=y2,ABS_HAT0X=dpad_x,ABS_HAT0Y=dpad_y \
   --axismap -Y1=Y1,-Y2=Y2 \
   --evdev-keymap   BTN_TOP=x,BTN_TRIGGER=y,BTN_THUMB2=a,BTN_THUMB=b,BTN_BASE3=back,BTN_BASE4=start,BTN_BASE=lb,BTN_BASE2=rb,BTN_TOP2=lt,BTN_PINKIE=rt,BTN_BASE5=tl,BTN_BASE6=tr \
   --mimic-xpad --silent

```

###### PlayStation 3 controller via USB

If you own a PS3 controller and can connect with USB, xboxdrv has the mappings built in. Just run the program (and detach the running driver) and it works!

```
# xboxdrv --silent --detach-kernel-driver

```

###### PlayStation 3 controller via Bluetooth

With your controller connected via Bluetooth, find the device address with `bluetoothctl`. Then create a new udev rule with the following content:

 `/etc/udev/rules.d/99-dualshock.rules`  `KERNEL=="event*", SUBSYSTEM=="input", ATTRS{uniq}=="<device_addr_you_got_on_pairing>", SYMLINK+="input/dualshock3"` 

The address must be in lowercase, like `06:9a:b4:c8:ef:8b`.

Now run xboxdrv over the new device:

```
$ xboxdrv --evdev /dev/input/dualshock3 --mimic-xpad

```

###### PlayStation 4 controller

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

## Troubleshooting

### Joystick moving mouse

Sometimes USB joystick can be recognized as HID mouse (only in X, it is still being installed as `/dev/input/js0` as well). Known issue is cursor being moved by the joystick, or escaping to en edge of a screen right after plugin. If your application can detect joystick by it self, you can remove xf86-input-joystick package.

More gentle solution is to [Disable Joystick From Controlling Mouse](#Disable_Joystick_From_Controlling_Mouse).

### Joystick not working in FNA/SDL based games

If you are using a generic non-widely used gamepad you may encounter issues getting the gamepad recognized in games based on SDL. Since [May the 14th 2015](https://github.com/flibitijibibo/FNA/commit/e55742cfe7e38b778a21ed8a12cb2f2081490d8d), FNA supports dropping a `gamecontrollerdb.txt` into the executable folder of the game, for example the [SDL_GameControllerDB](https://github.com/gabomdq/SDL_GameControllerDB).

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

### Steam Controller Not Pairing

If you want your system to be able to recognise Steam controller after hot swapping between wireless and wired connection, and also want system to recognise Steam controller if connected via micro-usb cable while wireless dongle is plugged in, you need to do instructions below. Otherwise, Steam controller will behave just as keyboard/mouse devise after hot swapping or unrecognised at all by steam and games.

If the Steam Controller will not pair wirelessly but works when wired make you may need to create the following udev rule, suggested by Valve[[1]](https://steamcommunity.com/app/353370/discussions/0/490123197956024380/).

 `/etc/udev/rules.d/99-steam-controller-perms.rules` 
```
# This rule is needed for basic functionality of the controller in Steam and keyboard/mouse emulation
SUBSYSTEM=="usb", ATTRS{idVendor}=="28de", MODE="0666"

# This rule is necessary for gamepad emulation
KERNEL=="uinput", MODE="0660", GROUP="steamcontroller", OPTIONS+="static_node=uinput"

# DualShock 4 wired
SUBSYSTEM=="usb", ATTRS{idVendor}=="054c", ATTRS{idProduct}=="05c4", MODE="0666"
# DualShock 4 wireless adapter
SUBSYSTEM=="usb", ATTRS{idVendor}=="054c", ATTRS{idProduct}=="0ba0", MODE="0666"
# DualShock 4 slim wired
SUBSYSTEM=="usb", ATTRS{idVendor}=="054c", ATTRS{idProduct}=="09cc", MODE="0666"

# Valve HID devices over USB hidraw
KERNEL=="hidraw*", ATTRS{idVendor}=="28de", MODE="0666"

# Valve HID devices over bluetooth hidraw
KERNEL=="hidraw*", KERNELS=="*28DE:*", MODE="0666"

# DualShock 4 over bluetooth hidraw
KERNEL=="hidraw*", KERNELS=="*054C:05C4*", MODE="0666"

# DualShock 4 Slim over bluetooth hidraw
KERNEL=="hidraw*", KERNELS=="*054C:09CC*", MODE="0666" 

```

Create a group of steam controller users.

```
# groupadd steamcontroller

```

And add your user to that group.

```
# gpasswd -a $USER steamcontroller

```