The **Logitech Marble Mouse** is a pointing device with four buttons and a trackball. It is also known as the **Trackman Marble**. The Marble Mouse is symmetrical, making it well-suited for use with either hand. [Picture](http://www.logitech.com/assets/21083/21083.png). Out-of-the box it does not scroll, but you can configure it to enable this.

## Contents

*   [1 Installation](#Installation)
*   [2 Basic function](#Basic_function)
*   [3 Configuration](#Configuration)
    *   [3.1 Buttons and trackball](#Buttons_and_trackball)
        *   [3.1.1 Assigning buttons](#Assigning_buttons)
        *   [3.1.2 "Both-large-buttons" combination-click](#.22Both-large-buttons.22_combination-click)
        *   [3.1.3 Scroll modifier](#Scroll_modifier)
    *   [3.2 Right-side or left-side](#Right-side_or_left-side)
    *   [3.3 System-wide or per-user](#System-wide_or_per-user)
    *   [3.4 Xorg input hotplugging](#Xorg_input_hotplugging)
    *   [3.5 Without Xorg hotplugging](#Without_Xorg_hotplugging)
*   [4 Sample configuration](#Sample_configuration)
    *   [4.1 Configuration file](#Configuration_file)
    *   [4.2 Restarting X](#Restarting_X)
*   [5 Minimal configuration](#Minimal_configuration)
    *   [5.1 Using evdev](#Using_evdev)
    *   [5.2 Using libinput](#Using_libinput)
*   [6 Additional tweaks](#Additional_tweaks)
    *   [6.1 Console (gpm)](#Console_.28gpm.29)
    *   [6.2 Chromium browser](#Chromium_browser)
    *   [6.3 Firefox browser](#Firefox_browser)
*   [7 See also](#See_also)

## Installation

No driver installation is required. Your system detects the Logitech Marble Mouse at system boot, or whenever it is "hot-plugged" into a booted system.

The Marble Mouse is treated like any regular mouse — you do not need to configure it. You will probably want to, however, in order to enable scrolling or customize button actions.

## Basic function

Hardware IDs for the Marble Mouse buttons remain constant, regardless of device configuration.

When no additional configuration is specified, buttons are mapped to these functions:

| ID     | Hardware Action     | Result                 |
| 1 | Large button left | normal click |
| 2 | Both large buttons | middle-click  † |
| 3 | Large button right | right-click |
| 4 | *(not a button)* | - |
| 5 | *(not a button)* | - |
| 6 | *(not a button)* | - |
| 7 | *(not a button)* | - |
| 8 | Small button left | browser back |
| 9 | Small button right | browser forward |

**Note:**

*   Both large buttons pressed simultaneously creates a **middle-click**.
*   †  The simultaneous click is enabled by a configuration directive. It requires `Emulate3buttons`.
*   Terms *middle-click* and *wheel-click* are used interchangeably in this document.
*   *Alternate-click* may be used instead of *right-click*. Typically, this pops up a context menu.
*   The result shown above occurs when no modifier key is pressed.
*   A different result may occur when a modifier key such as *Ctrl* is held while a button is clicked.

| ID     | Hardware Action     | Result                 |
| 4 | *Roll ball down* | move cursor down |
| 5 | *Roll ball up* | move cursor up |
| 6 | *Roll ball left* | move cursor left |
| 7 | *Roll ball right* | move cursor right |

**Note:**

*   Cursor motion occurs when no modifier is used.
*   A modifier used in conjunction with rolling motion may create an alternate result.
*   "Modifier" refers to a key (such as *Ctrl*) or button (as in *mouse button*) being held while the trackball is rolled.

**Note:** The Marble Mouse trackball can perform document scrolling, much like a wheel mouse. Scrolling occurs when the **[scroll mod­ifier](#Scroll_modifier)** is held down while the trackball is rolled. You must provide at least a **[minimal configuration](#Minimal_configuration)** to enable this feature.

Using the trackball in "wheel mode" can require some unusual gestures on the user's part. Using a wheel mouse, for example, you can resize the display font in your web browser using the  *Ctrl + wheel_roll*  gesture. With the trackball, this operation becomes  *Ctrl + hold_button + ball_roll*.

## Configuration

You may find it helpful to simply jump to the [sample configuration](#Sample_configuration) and try it.

The configuration sections contain information which may not be of interest to you. Most Arch users will be using a modern version of the X server which requires udev hot plugging.

**Note:** There is currently (as at May 2012) an issue with [Gnome 3 and middle click emulation](http://who-t.blogspot.com.au/2011/04/gnome-30-middle-mouse-button-emulation.html). See [#"Both-large-buttons" combination-click](#.22Both-large-buttons.22_combination-click) below.

Gnome 3 is used, for example, in Ubuntu 12.04.

### Buttons and trackball

After you locate the [sample configuration file](#Configuration_file) you may wish to alter it. You need only concern yourself with three or four setup lines.

#### Assigning buttons

You may want to assign new actions for button presses. This is done by setting positional parameters.

Values may be changed for buttons **1, 2, 3, 8,** and **9**. (Button **2** is simply a combination press of the two large buttons.) Do not alter parameters 4, 5, 6, or 7.

```
# This line makes the default button assignments.

Option "ButtonMapping" "1 2 3 4 5 6 7 8 9"

```

One obvious reason to assign different button actions is to accommodate left-handed placement:

```
# This line switches the left and right large buttons, and nothing else. For left-handed user.

Option "ButtonMapping" "3 2 1 4 5 6 7 8 9"

```

Another reason to reassign is when you do not like the "normal" assignments — especially the small buttons.

The line below changes the button **2** action to ***browser forward***. Parameter two (both-large-button click) is given value **9** for *browser forward*. The line below also reassigns both small buttons. We want them to emit ***middle-click***. (Either button may be clicked separately.) Parameters eight and nine are given values of **2** for *middle-click*.

```
# Three buttons are given new assignments. For right-handed user.

Option "ButtonMapping" "1 9 3 4 5 6 7 2 2"

```

Parameters are positioned in numeric order. Parameters you might modify are 1, 2, 3, 8, and 9\. Parameters 4, 5, 6, and 7 should be left alone; they correspond to trackball movements.

#### "Both-large-buttons" combination-click

As stated, button **2** is a simultaneous press of the two large buttons.

Experimentation shows, in the absence of a configuration directive, this action produces an indeterminate result. It appears to issue *some* command, but the result is inconsistent with my expectation of *middle-click.* The result seems dependent on whichever object is foremost. It is inconsistent regardless. You need to enable the combination-click:

```
# Emulate3Buttons refers to the act of pressing buttons A and D
# simultaneously to emulate a middle-click or wheel click.
Option "Emulate3Buttons" "true"

```

This is sufficient to enable the default mapping of button **2**, which is *wheel-click*.  See [minimal configuration](#Minimal_configuration).

As at May 2012, there is an issue with [Gnome 3 and middle click emulation](http://who-t.blogspot.com.au/2011/04/gnome-30-middle-mouse-button-emulation.html). Gnome 3 is used, for example, in Ubuntu 12.04\. Gnome 3 also sets the middle click property, and defaults to "false". Since Gnome does its settings **after** Xorg, the Gnome setting overrides the xorg setting, and emulation is disabled. The Gnome setting can be changed with this command:

```
gsettings set org.gnome.settings-daemon.peripherals.mouse middle-button-enabled true

```

You only need to do this once (per user) as Gnome remembers the settings between sessions. There is a [launchpad bug](https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-input-evdev/+bug/874237/comments/13) on the issue in case you are interested.

#### Scroll modifier

One huge limitation for the Marble Mouse is the lack of a scroll wheel or scroll ring. This limitation is overcome by assigning a *scroll modifier*: a mouse button which allows the trackball to scroll. When the scroll modifier is held, the trackball scrolls. Although a scroll modifier is *assigned* by default (see [basic function](#Basic_function)), the scroll modifier is **not enabled** by default. In addition to enabling the scroll modifier, you may *also* assign it to a different button.

**Note:** The scroll button has a "click" function in addition to its scroll function. The scroll modifier is a "press and hold" function separate from the "click" function. The best choice for scroll modifier is one of the small buttons. Unfortunately, standard "click" actions for those buttons are awkward. I recommend you reassign click actions for the small buttons.

The standard scroll setting defines the small button for scrolling — that is good, — but the same button has a default *"click"* action that is ***browser back***. A better choice is ***middle-click***. *Middle-click* corresponds to what you would expect from years of wheel mouse usage.

Putting complaints aside (these are addressed by reassigning small buttons), you specify a button to be the ***scroll modifier***:

```
Option "EmulateWheel" "true"
Option "EmulateWheelButton" "8"

# Button 8 is the small button on the left side, which works well for right-handed users.
# Button 9 is the small button on the right side, which works well for left-handed users.
# Button 2 cannot be assigned as the scroll modifier; AKA "EmulateWheelButton".

```

**Disable horizontal scrolling**

A particular configuration line enables horizontal scrolling. You disable horizontal scrolling by commenting that line out.

```
# A hash mark disables a configuration line.

# Option "XAxisMapping" "6 7"

```

I use both scrolling directions, but some may find this restriction helpful. You cannot disable vertical scrolling in a similar fashion — not that you would want to, anyway.

### Right-side or left-side

Previous sections explain how to modify your configuration file for either left or right placement.

*   On occasion, you may wish to switch between left-handed and right-handed usage.
*   I do this when I feel the early signs of repetitive strain injury.

To switch to the opposite placement, I manually edit my configuration file and [restart the X server.](#Restarting_X) Comments in the file remind me which lines to change. You could devise a script to make switching more automatic, if you wanted to.

*   With Arch Linux, I prefer a lightweight or non-existent desktop environment running the **[Openbox](/index.php/Openbox "Openbox")** window manager.

Other desktop environments may have widgets to simplify — or complicate, depending how you view it — switching between right and left. With Ubuntu 10.10, for example, you need only mark a box in the mouse control panel to effect a button switch. *(You must change the configuration file to get the correct scroll modifier assignment, however. Also, Ubuntu ignores large button assignments in the configuration file; the control panel makes them unnecessary.)*

### System-wide or per-user

**Note:** Section undergoing revision. Please jump to the sample configuration

If you want the configuration to be system wide, you can add this line to the InputDevice-Section.

```
Option "ButtonMapping" "1 8 3 2 9"

```

For a per-user-configuration you need to put this in your ~/.Xmodmap

```
pointer = 1 8 3 4 5 6 7 2 9 10 11 12 13

```

or this in your ~/.xinitrc.

```
xmodmap -e "pointer = 1 8 3 4 5 6 7 2 9 10 11 12 13"

```

### Xorg input hotplugging

**Note:** Section undergoing revision. Please jump to the sample configuration

Two expositions help you configure a trackball with buttons for click, middle-click, right-click, and scrolling. The first exposition uses [Xorg Input Hotplugging](/index.php/Xorg#Input_devices "Xorg"); the second does not. Edit them to suit your preferences.

Add this entry to your `/etc/X11/xorg.conf`:

```
Section "InputClass"
    Identifier   "Logitech Trackball"
    MatchProduct "Trackball"
    Option       "ButtonMapping"      "1 8 3 4 5 6 7 2 9"
    Option       "EmulateWheel"       "True"
    Option       "EmulateWheelButton" "9"
    Option       "XAxisMapping"       "6 7"
EndSection

```

To learn more about the used parameters you should read the apropriate section in the evdev man page.

### Without Xorg hotplugging

**Note:** Section undergoing revision. Please jump to the sample configuration

The mouse device entry in `/etc/X11/xorg.conf` should look like this:

```
Section "InputDevice"
    Identifier "Mouse0"
    Driver     "mouse"
    Option     "CorePointer"
    Option     "Device"             "/dev/input/mice"
    Option     "Protocol"           "ExplorerPS/2"
    Option     "Buttons"            "9"
    Option     "ZAxisMapping"       "4 5"
    Option     "XAxisMapping"       "6 7"
    Option     "EmulateWheelButton" "9"
    Option     "EmulateWheel"       "true"
EndSection

```

The `"Auto"` option for `"Protocol"` works fine, too. Of course you can use the name you prefer as the `Identifier`, as long as it is the same you use as `InputDevice` in the `Section "ServerLayout"` .

## Sample configuration

The sample configuration modifies and extends the [basic function](#Basic_function) of the Marble Mouse.

In this example, either of the two small buttons may be clicked to send a ***wheel-click***. Wheel-click means the same as "middle-click" here. In addition, one of the small buttons provides ***scrolling*** in conjunction with the trackball. Note that only *one* small button has the ability for scrolling, although both small buttons are able to *wheel-click.*

Finally, clicking both large buttons simultaneously sends the ***browser back*** event. There is no button to send *browser forward*.

| ID     | Hardware Action          | Result (this configuration)      | New assignment |
| 1 | Large button left | normal click | 1 |
| 2 | Both large buttons | browser back | 8 |
| 3 | Large button right | right-click | 3 |
| 8 | Small button left  † | wheel-click | 2 |
| 9 | Small button right  ‡       | wheel-click | 2 |

**Note:**

*   Both large buttons pressed simultaneously results in *browser back*.
*   Either small button, when clicked, results in *middle-click*.
*   †  This small button allows trackball scrolling when held down. It is the scroll modifier.
*   ‡  This button can be mapped for scrolling function instead. This button works better for left-side placement because it lies near the thumb of one's left-hand. Only one button can be assigned as the scroll modifier as far as I know.

### Configuration file

The following lines are appended to **`/etc/X11/xorg.conf.d/10-evdev.conf`**

**Note:** *Users of other Linux distributions may find the configuration file in another location. Ubuntu uses /usr/share/X11/xorg.conf.d/10-evdev.conf*

This example is set up for right-hand placement with horizontal scrolling disabled.

```
#       - - - Logitech Marble Mouse Settings - - -
#
#       The Logitech Marble Mouse buttons are mapped [A-D] from left to right: 
#       A (large); B (small) |  C (small); D (large). 
#
#       Preferred options for right-handed usage:
#       A = normal click [1]  
#       B = middle-click [2] 
#       C = middle-click [2] 
#       D = right-click [3]
#       Hold button B while rolling trackball to emulate wheel-scrolling. 
#
#       Preferred options for left-handed usage:
#       A = right-click [3]  
#       B = middle-click [2] 
#       C = middle-click [2]
#       D = normal click [1]
#       Hold button C while rolling trackball to emulate wheel-scrolling.
#       Pressing both large buttons simultaneously (b) produces a "back" action.

Section "InputClass"
        Identifier  "Marble Mouse"
        MatchProduct "Logitech USB Trackball"
        MatchIsPointer "on"
        MatchDevicePath "/dev/input/event*"
        Driver "evdev"

#       Physical button #s:     A b D - - - - B C    
#       Option "ButtonMapping" "1 8 3 4 5 6 7 2 2"   right-hand placement
#       Option "ButtonMapping" "3 8 1 4 5 6 7 2 2"   left-hand placement
#       b = A & D 
        Option "ButtonMapping" "1 8 3 4 5 6 7 2 2"

#       EmulateWheel: Use Marble Mouse trackball as mouse wheel 
#       Factory Default: 8; Use 9 for right side small button
        Option "EmulateWheel" "true"
        Option "EmulateWheelButton" "8"

#       EmulateWheelInertia: How far (in pixels) the pointer must move to
#       generate button press/release events in wheel emulation mode.
#       Factory Default: 50
        Option "EmulateWheelInertia" "10"

#       Axis Mapping: Enable vertical [ZAxis] and horizontal [XAxis] scrolling
        Option "ZAxisMapping" "4 5"
#       Option "XAxisMapping" "6 7"

#       Emulate3Buttons: Required to interpret simultaneous press of two large
#       buttons, A & D, as a seperate command, b.
#       Factory Default: true
        Option "Emulate3Buttons" "true"
EndSection

```

### Restarting X

Changes made to xorg configuration files do not take effect until the X session is restarted. To restart the X session, simply log out from your window manager and log back in.

Or, depending on what display manager you use, you can use one of the following commands:

Default Ubuntu (with LightDM) : `sudo restart lightdm`

Gnome (with GDM) : `sudo restart gdm`

KDE (with KDM) : `sudo restart kdm`

## Minimal configuration

### Using evdev

At times it can be useful to start with the absolute minimum and build from there. This is one facet of [The Arch Way](/index.php/The_Arch_Way "The Arch Way"). In this spirit, I decided to see how few lines I might use to create a usable Marble Mouse configuration.

You can omit *all* configuration lines and the Marble Mouse is still usable for basic pointing and clicking. However, it will not be able to scroll. The "both-large-button" simultaneous click produces indeterminate results — experimentation shows this.

Given that you are satisfied with [default button settings](#Basic_function) and you wish only to enable scrolling and the "both-large-button" click, you need these lines. The following lines are appended to **`/etc/X11/xorg.conf.d/10-evdev.conf`**.

```
Section "InputClass"
        Identifier  "Marble Mouse"
        MatchProduct "Logitech USB Trackball"
        Option "EmulateWheel" "true"
        Option "EmulateWheelButton" "8"
        Option "XAxisMapping" "6 7"
        Option "Emulate3Buttons" "true"
EndSection

```

### Using libinput

As of version 3.16 GDM/Gnome uses libinput. For the device to work as described in the above section you need to install [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) and instead append this to `/etc/X11/xorg.conf.d/10-libinput.conf`.

 `/etc/X11/xorg.conf.d/10-libinput.conf` 
```
Section "InputClass"
        Identifier      "Marble Mouse"
        MatchProduct    "Logitech USB Trackball"
        Driver          "libinput"
        Option          "ScrollMethod" "button"
        Option          "ScrollButton" "8"
	Option		"MiddleEmulation" "on"
EndSection

```

## Additional tweaks

### Console (gpm)

See [Console mouse support](/index.php/Console_mouse_support "Console mouse support") for details. Within the console you can use `gpm` with type option set to **imps2**. Edit **`/etc/conf.d/gpm`** such that:

```
GPM_ARGS="-m /dev/input/mice -t imps2"

```

This lets you use the large left button for selecting text and the right button to extend the selection. The small left button acts as a middle-click; it pastes the selection.

### Chromium browser

By default, Chromium treats a middle-click as a *paste* command. This choice stems from "Linux tradition", not the capricious whim of one developer. Like myself, you may prefer a ***Windows*** approach. I want the middle button(s) to initiate *automatic scrolling,* not *pasting*:

*   A browser extension **AutoScroll** allows middle-click to initiate automatic scrolling.
*   This extension is helpful for any Linux user with a wheel mouse, not just Marble Mouse users.
*   A middle-click initiates automatic scrolling when clicked on a blank area of a web page.

*   When you program both small buttons to emit middle-click, either button can initiate automatic scrolling. That is a click function.
*   When you program one of the small buttons to act as scroll modifier (mouse setup), you can manually scroll web pages **without** fixing the browser. That is a press‑and‑hold function. (I recommend installing AutoScroll even though it is not absolutely necessary for scrolling.)
*   After you assign the scroll modifier to one of the small buttons, the small buttons act a bit differently from one another. The difference is seen when you compare their "press‑and‑hold" behaviors.

Be sure to install ***AutoScroll***;  the similarly-named *Auto Scroll* extension implements a different feature.

This information also applies to the browser called **Google Chrome**.

### Firefox browser

Older versions of Firefox map horizontal-scrolling hardware to perform ***browser back*** and ***browser forward*** navigation.

This makes vertical scrolling using the trackball almost impossible.

The slightest horizontal motion triggers a URL redirection. To fix this:

*   Enter `about:config` in the location bar
*   Find the internal variable named `mousewheel.horizscroll.withnokey.action`. Set its value to **0**.
*   It may be useful to set `mousewheel.horizscroll.withnokey.numlines` to **1** as well.

## See also

*   Arch wiki documentation: [All Mouse Buttons Working](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working")
*   Arch wiki documentation: [Xorg#Configuration](/index.php/Xorg#Configuration "Xorg")
*   Marble mouse scroll wheel: [Replacement for SetPoint driver](http://simans.net/marble/)
*   Joe Shaw blog post: [Linux input ecosystem](http://joeshaw.org/2010/10/01/681/)
*   Ubuntu community: [Logitech Marble Mouse](https://help.ubuntu.com/community/Logitech_Marblemouse_USB)
*   Chrome web store: [AutoScroll extension](https://chrome.google.com/webstore/detail/occjjkgifpmdgodlplnacmkejpdionan)