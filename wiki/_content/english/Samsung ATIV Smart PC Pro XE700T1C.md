<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 System Specification](#System_Specification)
*   [2 Installation](#Installation)
*   [3 Network](#Network)
    *   [3.1 Wireless](#Wireless)
    *   [3.2 Bluetooth](#Bluetooth)
*   [4 Buttons](#Buttons)
*   [5 Graphics](#Graphics)
*   [6 TouchScreen](#TouchScreen)
    *   [6.1 Screen Rotation](#Screen_Rotation)
        *   [6.1.1 Rotate on button press (Gnome)](#Rotate_on_button_press_(Gnome))
        *   [6.1.2 Rotate on button press (i3)](#Rotate_on_button_press_(i3))
    *   [6.2 Multitouch](#Multitouch)
*   [7 Sound](#Sound)
*   [8 Webcam](#Webcam)
*   [9 Accessories](#Accessories)
    *   [9.1 Dock](#Dock)
    *   [9.2 Keyboard](#Keyboard)
    *   [9.3 Stylus](#Stylus)

## System Specification

*   CPU: Intel® Core™ i5 3317U (1.7 GHz, 3 MB, caché L3), Intel HM76
*   Memory: 4GB DDR3 System Memory at 1600MHz
*   Hard-Drive: 128GB Solid-state Drive
*   Screen: 11.6" LCD (1920x1080)
*   Integrated Graphics: Intel® HD Graphics 4000
*   Touchscreen: Atmel maXTouch Digitizer (10 points)
*   Accelerometer: STMicroelectronics 6-Axis Accelerometer/Magnetometer ([LSM303DLH](/index.php/STMicroelectronics_LSM303DLH_Accelerometer/Magenetometer "STMicroelectronics LSM303DLH Accelerometer/Magenetometer"))
*   WiFi: Intel® Centrino® Advanced-N 6235 802.11abg/n
*   Bluetooth: Bluetooth 3.0
*   USB: USB 3.0

## Installation

Press the power and volume key down a few seconds. To Navigate the BIOS, the home, button is escape, the lock button is enter, the volume rocker buttons are up and down and the volume rocker buttons and the lock button pressed simultaneously are left and right. Also you can navigating throught touch and access to the boot menu. From here it's your classic Arch install.

([Installation guide](/index.php/Installation_guide "Installation guide"))

## Network

### Wireless

No issues.

### Bluetooth

Works fine too.

[Enable](/index.php/Enable "Enable") `bluetooth.service`.

## Buttons

Everything works well.

## Graphics

The [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver works well with no need for an configuration.

The brightness you need to add acpi_backlight=video in the kernel params [Backlight#Kernel command-line options](/index.php/Backlight#Kernel_command-line_options "Backlight")

## TouchScreen

The touch screen works out of the box with [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) and the pen works almost perfectly with [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom).

In order to get the pen button to emulate a right click, go into the Wacom settings in System Preferences.

The touch screen will be recognized as a finger input by many applications, such as Gnome Files or chromium by default and will result in dragging causing the page to scroll, rather than selecting text or objects.

To use scroll fingers with Firefox you can add:

```
$ echo export MOZ_USE_XINPUT2=1 | sudo tee /etc/profile.d/firefox-scroll.sh

```

### Screen Rotation

#### Rotate on button press (Gnome)

You can use the button that the tablet has to lock or unlock he rotation. Also gnome has and option in the config menu (Up corner right)-

#### Rotate on button press (i3)

You can use the rotation lock button on i3 to rotate the screen by making a [bash](/index.php/Bash "Bash") script that runs when the button is pressed. Below is a script I use to do so. The script has a secondary outside file that holds a boolean that tells whether or not the screen is rotated. Make sure to replace */directory/* in the code with wherever one desires to place the secondary file.

```
#!/bin/bash
#Script to rotate the screen when evoked

#check a file and pass to a variable to see if the screen is already rotated
rotated=$(< */directory/*rotation.txt)

#if statement to rotate the screen the opposite way
if [ $rotated -eq 0 ];then
        xrandr --output eDP1 --rotate normal
        xsetwacom set "Wacom ISDv4 EC Pen stylus" rotate none
        xinput set-prop "pointer:Atmel Atmel maXTouch Digitizer" --type=float "Coordinate Transformation Matrix" 0 0 0 0 0 0 0 0 0
        echo 1 > */directory/*rotation.txt
else
        xrandr --output eDP1 --rotate right
        xsetwacom set "Wacom ISDv4 EC Pen stylus" rotate cw
        xinput set-prop "pointer:Atmel Atmel maXTouch Digitizer" --type=float "Coordinate Transformation Matrix" 0 1 0 -1 0 1 0 0 1
        echo 0 > */directory/*rotation.txt
fi
```

### Multitouch

Multitouch works fine out the box. For example you can manipulate the images on Eye of Gnome (Gnome Image Viewer)

## Sound

After installing [GNOME](/index.php/GNOME "GNOME"), the sound works without any extras. The rocker buttons on the side also work without any problems.

## Webcam

The frontal camera doesn't work yet. But the other camera works fine with Cheese (if you are using Gnome)

## Accessories

### Dock

Not tested yet.

### Keyboard

The tablet has a USB port so you can put a keyboard or a combo keyboard. With Bluetooth no testes yet.

### Stylus

If you have installed the Wacom driver, the stylus works fine.

I use [xournal](https://aur.archlinux.org/packages/xournal/) for writing notes, and found enabling, "Use XInput", "Eraser Tip" and "Pressure sensitivity", as well as setting "Button 3 Mapping" to "Eraser" gave the best, and expected results.