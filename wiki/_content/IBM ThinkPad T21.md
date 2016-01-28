# IBM ThinkPad T21

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Works with no known issues. Tested on 2008.03 and 2008.06\.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 CPU Frequency Scaling](#CPU_Frequency_Scaling)
    *   [1.2 Hotkeys](#Hotkeys)
        *   [1.2.1 External VGA](#External_VGA)
    *   [1.3 Xorg](#Xorg)
*   [2 See also](#See_also)

## Configuration

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:IBM ThinkPad T21#](https://wiki.archlinux.org/index.php/Talk:IBM_ThinkPad_T21))

### CPU Frequency Scaling

Install [cpudyn](https://aur.archlinux.org/packages.php?ID=43483) from the AUR.

Add speedstep_lib, speedstep_smi, and cpufreq_userspace to MODULES array in /etc/[rc.conf](/index.php/Rc.conf "Rc.conf").

```
MODULES=(... **speedstep_lib speedstep_smi cpufreq_userspace** ...)

```

Add cpudyn to DAEMONS array in /etc/rc.conf

```
DAEMONS=(... **cpudyn** ...)

```

### Hotkeys

They work better after loading the thinkpad-acpi module, to assign the generated keycodes to their supposed functions. You may also want to install tpb (ThinkPad Buttons) if you still have trouble.

#### External VGA

For whatever reason, external VGA output (for an external monitor) was disabled. This was fixed by doing this:

```
# echo 1 > /proc/acpi/video/VID/DOS 

```

### Xorg

Works with driver xf86-video-savage. However, to achieve DRI (and thus OpenGL acceleration), you will have to use 16-bit color. The 8 MB of VRAM with the Savage GPU isn't enough to support 24 bit color, OpenGL, and 1024x768\. You must either drop color depth or resolution.

Here is the mentioned file, for those who do not have a working configuration yet:

```
# /etc/X11/xorg.conf (xorg X Window System server configuration file)  

Section "ServerLayout" 
       Identifier     "X.org Configured" 
       Screen      0  "Screen0" 0 0 
       InputDevice    "Mouse0" "CorePointer" 
       InputDevice    "Keyboard0" "CoreKeyboard" 
EndSection 
Section "Files" 
       RgbPath      "/usr/share/X11/rgb" 
       ModulePath   "/usr/lib/xorg/modules" 
       FontPath     "/usr/share/fonts/misc" 
       FontPath     "/usr/share/fonts/100dpi:unscaled" 
       FontPath     "/usr/share/fonts/75dpi:unscaled" 
       FontPath     "/usr/share/fonts/TTF" 
       FontPath     "/usr/share/fonts/Type1" 
EndSection 
Section "Module" 
       Load  "glx" 
       Load  "extmod" 
       Load  "xtrap" 
       Load  "record" 
       Load  "GLcore" 
       Load  "dbe" 
       Load  "dri" 
       Load  "freetype" 
EndSection 
Section "InputDevice" 
       Identifier  "Keyboard0" 
       Driver      "kbd" 
EndSection 
Section "InputDevice" 
       Identifier  "Mouse0" 
       Driver      "mouse" 
       Option      "Protocol" "auto" 
       Option      "Device" "/dev/input/mice" 
       Option      "ZAxisMapping" "4 5 6 7" 
       ###To enable third trackpoint scrolling button
       Option      "EmulateWheel" "true"
       Option      "EmulateWheelButton" "2"
EndSection 
Section "Monitor" 
       Identifier   "Monitor0" 
       VendorName   "Monitor Vendor" 
       ModelName    "Monitor Model" 
EndSection 
Section "Device" 
       ### Available Driver options are:- 
       ### Values: <i>: integer, <f>: float, <bool>: "True"/"False", 
       ### <string>: "String", <freq>: "<f> Hz/kHz/MHz" 
       ### [arg]: arg optional 
       #Option     "NoAccel"                   # [<bool>] 
       #Option     "AccelMethod"               # <str> 
       #Option     "HWCursor"                  # [<bool>] 
       #Option     "SWCursor"                  # [<bool>] 
       #Option     "ShadowFB"                  # [<bool>] 
       #Option     "Rotate"                    # [<str>] 
       #Option     "UseBIOS"                   # [<bool>] 
       #Option     "LCDClock"                  # <freq> 
       #Option     "ShadowStatus"              # [<bool>] 
       #Option     "CrtOnly"                   # [<bool>] 
       #Option     "TvOn"                      # [<bool>] 
       #Option     "PAL"                       # [<bool>] 
       #Option     "ForceInit"                 # [<bool>] 
       #Option     "Overlay"                   # [<str>] 
       #Option     "TransparencyKey"           # [<str>] 
       #Option     "ForceInit"                 # [<bool>] 
       #Option     "DisableXVMC"               # [<bool>] 
       #Option     "DisableTile"               # [<bool>] 
       #Option     "DisableCOB"                # [<bool>] 
       #Option     "BCIforXv"                  # [<bool>] 
       #Option     "DVI"                       # [<bool>] 
       #Option     "IgnoreEDID"                # [<bool>] 
       #Option     "BusType"                   # [<str>] 
       #Option     "DmaType"                   # [<str>] 
       #Option     "DmaMode"                   # [<str>] 
       #Option     "AGPMode"                   # <i> 
       #Option     "AGPSize"                   # <i> 
       #Option     "DRI"                       # [<bool>] 
       Identifier  "Card0" 
       Driver      "savage" 
       VendorName  "S3 Inc." 
       BoardName   "86C270-294 Savage/IX-MV" 
       BusID       "PCI:1:0:0" 
EndSection 
Section "Screen" 
       Identifier "Screen0" 
       Device     "Card0" 
       Monitor    "Monitor0" 
       DefaultDepth 16 
       SubSection "Display" 
               Viewport   0 0 
               Depth     1 
       EndSubSection 
       SubSection "Display" 
               Viewport   0 0 
               Depth     4 
       EndSubSection 
       SubSection "Display" 
               Viewport   0 0 
               Depth     8 
       EndSubSection 
       SubSection "Display" 
               Viewport   0 0 
               Depth     15 
       EndSubSection 
       SubSection "Display" 
               Viewport   0 0 
               Depth     16 
       EndSubSection 
       SubSection "Display" 
               Viewport   0 0 
               Depth     24 
       EndSubSection 
EndSection

```

## See also

*   [Thinkwiki](http://www.thinkwiki.org/wiki/Category:T21)

Retrieved from "[https://wiki.archlinux.org/index.php?title=IBM_ThinkPad_T21&oldid=383141](https://wiki.archlinux.org/index.php?title=IBM_ThinkPad_T21&oldid=383141)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [IBM](/index.php/Category:IBM "Category:IBM")

Hidden category:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")