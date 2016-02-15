| **Device** | **Status** | **Modules** |
| Video (GMA 500) | **Working** | gma500_gfx / fbdev |
| Ethernet | **Working** | atl1c |
| Wireless | **Working** | ath9k |
| Audio | **Working** | snd_hda_intel |
| Camera | **Working** | uvcvideo |
| Card Reader | **Working** |
| Function Keys | **Partially working** |

## Contents

*   [1 Installation](#Installation)
*   [2 Video](#Video)
*   [3 Sound](#Sound)
*   [4 Camera](#Camera)
*   [5 Hotkeys](#Hotkeys)
*   [6 Fan](#Fan)

## Installation

For an in-depth guide on the installation see the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide").

## Video

The GMA 500 in the 1101HAb works well with the gma500_gfx driver included in the kernel and the fbdev driver. Install the fbdev driver via pacman:

```
   # pacman -Syu xf86-video-fbdev

```

As of linux-2.6, the user can no longer control the backlight. This can be remedied by adding `acpi_osi=Linux` to the KERNEL line in your bootloader.

(TODO: Add xorg configuration how-to)

## Sound

In at least one instance, sound worked out of the box. Just unmute and adjust the Master mixer using something like alsamixer.

## Camera

The webcam makes use of the `uvcvideo` module, which is part of the kernel as of linux-2.6\. Just run:

```
   # modprobe uvcvideo

```

and then you can use mplayer to test the camera's video:

```
   $  mplayer tv:// -tv driver=v4l2:width=320:height=240:fps=200:device=/dev/video0 -nosound

```

To load the module on startup, youmay add the module name to the MODULES array in `/etc/rc.conf`

## Hotkeys

After a clean installation, some of the media keys will not work. The ones that do (Volume Up/Down/Mute and Wifi) work well, but the rest require some tweaking. Adding

```
   acpi_backlight=vendor acpi_osi=Linux

```

should be enough to get all of the keys (except Fn+F7) mapped to keycodes, which may then be mapped to actions via either something like `speckeysd` / `xbindkeys` or the user's desktop environment.

## Fan

This model have more temperature than it seems to be "normal". It seems that fan does not work properly. It reaches 69 Celsius degrees.