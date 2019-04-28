Related articles

*   [Fonts](/index.php/Fonts "Fonts")
*   [Font configuration](/index.php/Font_configuration "Font configuration")
*   [MS Fonts](/index.php/MS_Fonts "MS Fonts")
*   [X Logical Font Description](/index.php/X_Logical_Font_Description "X Logical Font Description")

Some users may find the default Java fonts or the display mode of fonts in Java applications to be unpleasant. Several methods to improve the font display in the Oracle Java Runtime Environment (JRE) are available. These methods may be used separately, but many users will find they achieve better results by combining them.

TrueType fonts appear to be the best supported format for use with Java.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Anti-aliasing](#Anti-aliasing)
    *   [1.1 Running an xsettings daemon](#Running_an_xsettings_daemon)
    *   [1.2 Overriding the automatically picked up settings](#Overriding_the_automatically_picked_up_settings)
    *   [1.3 OpenJDK patch](#OpenJDK_patch)
*   [2 Font selection](#Font_selection)
    *   [2.1 TrueType fonts](#TrueType_fonts)
    *   [2.2 Fixing Mojibake (For JRE8)](#Fixing_Mojibake_(For_JRE8))

## Anti-aliasing

[Anti-aliasing](https://en.wikipedia.org/wiki/Font_rasterization "wikipedia:Font rasterization") of fonts is available with Oracle Java 1.6 and OpenJDK on Linux.

### Running an xsettings daemon

Java tries to get the system defaults through xsettings. On [GNOME](/index.php/GNOME "GNOME") you don't have to do anything, `gnome-settings-daemon` is already running. Otherwise [xsettingsd](https://www.archlinux.org/packages/?name=xsettingsd) is a lightweight alternative.

### Overriding the automatically picked up settings

If you don't want to run an xsettings daemon, or the fonts still look ugly, there is also a system property to set anti-aliasing. To do this system-wide, add the following line to `/etc/environment`:

```
_JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=*setting'*

```

Where `*setting*` is one of the values:

| Setting | Description |
| `off`, `false`, `default` | No anti-aliasing |
| `on` | Full anti-aliasing |
| `gasp` | Use the font's built-in hinting instructions |
| `lcd`, `lcd_hrgb` | Anti-aliasing tuned for many popular LCD monitors |
| `lcd_hbgr`, `lcd_vrgb`, `lcd_vbgr` | Alternative LCD monitor setting |

The `gasp` and `lcd` settings work well in many instances.

To optionally to use GTK look and feel, add the following line instead:

```
_JAVA_OPTIONS='-Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel' 

```

**Note:**

*   The described Java options only work for applications that draw their GUI in Java, like Jdownloader, and not for applications which utilize Java as backend only, like Openoffice.org and Matlab.
*   **TrueType** fonts contain a **g**rid-fitting **a**nd **s**can-conversion **p**rocedure (*GASP*) table with the designer's recommendations for the font's display at different point sizes. Some sizes are recommended to be fully anti-aliased, others are to be hinted, and some are to be displayed as bitmaps. Combinations are sometimes used for certain point sizes.

Specify the variable on the command line before the executable to try the new configuration:

```
_JAVA_OPTIONS=*options* *executable* 

```

Re-login for the changes to take effect.

### OpenJDK patch

Even with anti-aliasing enforced through Java options, the resulting anti-aliasing may be inferior to native applications. This can be remedied with a patch to OpenJDK, available in the [AUR](/index.php/AUR "AUR"):

*   Patched **OpenJDK7** is available as [jre7-openjdk-infinality](https://aur.archlinux.org/packages/jre7-openjdk-infinality/) (<tt>--enable-infinality=yes</tt>)
*   Patched **OpenJDK8** is available as [jre8-openjdk-infinality](https://aur.archlinux.org/packages/jre8-openjdk-infinality/)

The patched version obtains the per-family FreeType rendering/loading flags from fontconfig instead of using OpenJDK heuristics. Although this is an [Infinality](/index.php/Infinality "Infinality") package, the patches themselves don't actually depend on [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/) since only vanilla [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) APIs are used.

## Font selection

### TrueType fonts

Some Java applications may specify use of a particular TrueType font; these applications must be made aware of the directory path to the desired font. TrueType fonts are installed in the directory `/usr/share/fonts/TTF`. Add the following line to `/etc/environment` to enable these fonts.

```
JAVA_FONTS=/usr/share/fonts/TTF

```

Relogin for the change to take effect.

### Fixing Mojibake (For JRE8)

Place font files under the directory below. Create the directory if it does not exist.

```
/usr/lib/jvm/java-8-openjdk/jre/lib/fonts/fallback/

```