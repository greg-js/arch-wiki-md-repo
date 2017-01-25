Some users may find the default Java fonts or the display mode of fonts in Java applications to be unpleasant. Several methods to improve the font display in the Oracle Java Runtime Environment (JRE) are available. These methods may be used separately, but many users will find they achieve better results by combining them.

TrueType fonts appear to be the best supported format for use with Java.

## Contents

*   [1 Anti-aliasing](#Anti-aliasing)
    *   [1.1 Basic settings](#Basic_settings)
    *   [1.2 Font hinting](#Font_hinting)
    *   [1.3 OpenJDK patch](#OpenJDK_patch)
*   [2 Font selection](#Font_selection)
    *   [2.1 TrueType fonts](#TrueType_fonts)
    *   [2.2 Fixing Mojibake (For JRE8)](#Fixing_Mojibake_.28For_JRE8.29)

## Anti-aliasing

### Basic settings

[Anti-aliasing](https://en.wikipedia.org/wiki/Font_rasterization "wikipedia:Font rasterization") of fonts is available with Oracle Java 1.6 and OpenJDK on Linux. To do this system-wide, add the following line to `/etc/environment`:

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
_JAVA_OPTIONS=*options* *exectuable* 

```

Re-login for the changes to take effect.

### Font hinting

Some java applications are subject to system font hinting changes. Consider choosing one of the following environment variables before launching a java app:

```
export FT2_SUBPIXEL_HINTING=0  # Classic mode
export FT2_SUBPIXEL_HINTING=1  # Infinality mode
export FT2_SUBPIXEL_HINTING=2  # Default mode

```

For example, the value of <tt>0</tt> makes freetype use non-bold fonts (at least for some apps).

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