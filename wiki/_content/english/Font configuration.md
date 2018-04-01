Related articles

*   [Fonts](/index.php/Fonts "Fonts")
*   [Font configuration/Examples](/index.php/Font_configuration/Examples "Font configuration/Examples")
*   [Java Runtime Environment Fonts](/index.php/Java_Runtime_Environment_Fonts "Java Runtime Environment Fonts")
*   [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts")
*   [MS Fonts](/index.php/MS_Fonts "MS Fonts")
*   [X Logical Font Description](/index.php/X_Logical_Font_Description "X Logical Font Description")

[Fontconfig](http://www.freedesktop.org/wiki/Software/fontconfig/) is a library designed to provide a list of available [fonts](/index.php/Fonts "Fonts") to applications, and also for configuration for how fonts get rendered: see [Wikipedia:Fontconfig](https://en.wikipedia.org/wiki/Fontconfig "wikipedia:Fontconfig"). The FreeType library [freetype2](https://www.archlinux.org/packages/?name=freetype2) renders the fonts, based on this configuration.

Though Fontconfig is the standard in modern Linux, some applications rely on the original method of font selection and display, the [X Logical Font Description](/index.php/X_Logical_Font_Description "X Logical Font Description").

The font rendering packages on Arch Linux includes support for *freetype2* with the bytecode interpreter (BCI) enabled. For better font rendering, especially with an LCD monitor, see [#Fontconfig configuration](#Fontconfig_configuration) and [Font configuration/Examples](/index.php/Font_configuration/Examples "Font configuration/Examples").

## Contents

*   [1 Font paths](#Font_paths)
*   [2 Fontconfig configuration](#Fontconfig_configuration)
    *   [2.1 Presets](#Presets)
    *   [2.2 Anti-aliasing](#Anti-aliasing)
    *   [2.3 Hinting](#Hinting)
        *   [2.3.1 Byte-Code Interpreter (BCI)](#Byte-Code_Interpreter_.28BCI.29)
        *   [2.3.2 Autohinter](#Autohinter)
        *   [2.3.3 Hintstyle](#Hintstyle)
    *   [2.4 Pixel alignment](#Pixel_alignment)
    *   [2.5 Subpixel rendering](#Subpixel_rendering)
        *   [2.5.1 LCD filter](#LCD_filter)
        *   [2.5.2 Advanced LCD filter specification](#Advanced_LCD_filter_specification)
    *   [2.6 Disable auto-hinter for bold fonts](#Disable_auto-hinter_for_bold_fonts)
    *   [2.7 Replace or set default fonts](#Replace_or_set_default_fonts)
    *   [2.8 Whitelisting and blacklisting fonts](#Whitelisting_and_blacklisting_fonts)
    *   [2.9 Disable bitmap fonts](#Disable_bitmap_fonts)
    *   [2.10 Disable scaling of bitmap fonts](#Disable_scaling_of_bitmap_fonts)
    *   [2.11 Create bold and italic styles for incomplete fonts](#Create_bold_and_italic_styles_for_incomplete_fonts)
    *   [2.12 Change rule overriding](#Change_rule_overriding)
    *   [2.13 Query the current settings](#Query_the_current_settings)
*   [3 Applications without fontconfig support](#Applications_without_fontconfig_support)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Distorted fonts](#Distorted_fonts)
    *   [4.2 Calibri, Cambria, Monaco, etc. not rendering properly](#Calibri.2C_Cambria.2C_Monaco.2C_etc._not_rendering_properly)
    *   [4.3 Applications overriding hinting](#Applications_overriding_hinting)
    *   [4.4 Applications not picking up hinting from DE's settings](#Applications_not_picking_up_hinting_from_DE.27s_settings)
    *   [4.5 Incorrect hinting in GTK applications on non-Gnome systems](#Incorrect_hinting_in_GTK_applications_on_non-Gnome_systems)
    *   [4.6 Helvetica font problem in generated PDFs](#Helvetica_font_problem_in_generated_PDFs)
    *   [4.7 FreeType Breaking Bitmap Fonts](#FreeType_Breaking_Bitmap_Fonts)
*   [5 See also](#See_also)

## Font paths

For fonts to be known to applications, they must be cataloged for easy and quick access.

The font paths initially known to Fontconfig are: `/usr/share/fonts/`, `~/.local/share/fonts` (and `~/.fonts/`, now deprecated). Fontconfig will scan these directories recursively. For ease of organization and installation, it is recommended to use these font paths when [adding fonts](/index.php/Adding_fonts "Adding fonts").

To see a list of known Fontconfig fonts:

```
$ fc-list : file

```

See [fc-list(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fc-list.1) for more output formats.

Check for Xorg's known font paths by reviewing its log:

```
$ grep /fonts ~/.local/share/xorg/Xorg.0.log

```

**Tip:**

*   You can also check the list of [Xorg](/index.php/Xorg "Xorg")'s known font paths using the command `xset q`.
*   Use `/var/log/Xorg.0.log` if Xorg is run with root privileges.

Keep in mind that Xorg does not search recursively through the `/usr/share/fonts/` directory like Fontconfig does. To add a path, the full path must be used:

```
Section "Files"
    FontPath     "/usr/share/fonts/local/"
EndSection

```

If you want font paths to be set on a per-user basis, you can add and remove font paths from the default by adding the following line(s) to `~/.xinitrc`:

```
xset +fp /usr/share/fonts/local/           # Prepend a custom font path to Xorg's list of known font paths
xset -fp /usr/share/fonts/sucky_fonts/     # Remove the specified font path from Xorg's list of known font paths

```

To see a list of known Xorg fonts use `xlsfonts`, from the [xorg-xlsfonts](https://www.archlinux.org/packages/?name=xorg-xlsfonts) package.

## Fontconfig configuration

Fontconfig is documented in the [fonts-conf](http://www.freedesktop.org/software/fontconfig/fontconfig-user.html) man page.

Configuration can be done per-user through `$XDG_CONFIG_HOME/fontconfig/fonts.conf`, and globally with `/etc/fonts/local.conf`. The settings in the per-user configuration have precedence over the global configuration. Both these files use the same syntax.

**Note:** Configuration files and directories: `~/.fonts.conf/`, `~/.fonts.conf.d/` and `~/.fontconfig/*.cache-*` are deprecated since [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) 2.10.1 ([upstream commit](http://cgit.freedesktop.org/fontconfig/commit/?id=8c255fb185d5651b57380b0a9443001e8051b29d)) and will not be read by default in the future versions of the package. New paths are `$XDG_CONFIG_HOME/fontconfig/fonts.conf`, `$XDG_CONFIG_HOME/fontconfig/conf.d/NN-name.conf` and `$XDG_CACHE_HOME/fontconfig/*.cache-*` respectively. If using the second location, make sure the naming is valid (where `NN` is a two digit number like `00`, `10`, or `99`).

Fontconfig gathers all its configurations in a central file (`/etc/fonts/fonts.conf`). This file is replaced during fontconfig updates and should not be edited. Fontconfig-aware applications source this file to know available fonts and how they get rendered. This file is a conglomeration of rules from the global configuration (`/etc/fonts/local.conf`), the configured presets in `/etc/fonts/conf.d/`, and the user configuration file (`$XDG_CONFIG_HOME/fontconfig/fonts.conf`). `fc-cache` can be used to rebuild fontconfig's configuration, although changes will only be visible in newly launched applications.

**Note:** For some desktop environments (such as [GNOME](/index.php/GNOME "GNOME") and [KDE](/index.php/KDE "KDE")) using the *Font Control Panel* will automatically create or overwrite the user font configuration file. For these desktop environments, it is best to match your already defined font configurations to get the expected behavior.

Fontconfig configuration files use [XML](https://en.wikipedia.org/wiki/XML "wikipedia:XML") format and need these headers:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

  <!-- settings go here -->

</fontconfig>

```

The configuration examples in this article omit these tags.

### Presets

There are presets installed in the directory `/etc/fonts/conf.avail`. They can be enabled by creating [symbolic links](https://en.wikipedia.org/wiki/Symbolic_link "wikipedia:Symbolic link") to them, both per-user and globally, as described in `/etc/fonts/conf.d/README`. These presets will override matching settings in their respective configuration files.

For example, to enable sub-pixel RGB rendering globally:

```
# cd /etc/fonts/conf.d
# ln -s ../conf.avail/10-sub-pixel-rgb.conf

```

To do the same but instead for a per-user configuration:

```
$ mkdir $XDG_CONFIG_HOME/fontconfig/conf.d
$ ln -s /etc/fonts/conf.avail/10-sub-pixel-rgb.conf $XDG_CONFIG_HOME/fontconfig/conf.d

```

### Anti-aliasing

[Font rasterization](https://en.wikipedia.org/wiki/Font_rasterization "wikipedia:Font rasterization") converts vector font data to bitmap data so that it can be displayed. The result can appear jagged due to [aliasing](https://en.wikipedia.org/wiki/Aliasing "wikipedia:Aliasing"). The technique known as [anti-aliasing](https://en.wikipedia.org/wiki/Anti-aliasing "wikipedia:Anti-aliasing") can be used to increase the apparent resolution of font edges. Anti-aliasing is **enabled** by default. To disable it:

```
  <match target="font">
    <edit name="antialias" mode="assign">
      <bool>false</bool>
    </edit>
  </match>

```

**Note:** Some applications, like [GNOME](/index.php/GNOME "GNOME") may [override default anti-aliasing settings](#Troubleshooting).

### Hinting

[Font hinting](https://en.wikipedia.org/wiki/Font_hinting "wikipedia:Font hinting") (also known as instructing) is the use of mathematical instructions to adjust the display of an outline font so that it lines up with a rasterized grid (i.e. the pixel grid of the display). Its intended effect is to make fonts appear more crisp so that they are more readable. Fonts will line up correctly without hinting when displays have around 300 [DPI](https://en.wikipedia.org/wiki/Dots_per_inch "wikipedia:Dots per inch").

#### Byte-Code Interpreter (BCI)

Using BCI hinting, instructions in TrueType fonts are rendered according to FreeTypes's interpreter. BCI hinting works well with fonts with good hinting instructions. Hinting is **enabled** by default. To disable it:

```
  <match target="font">
    <edit name="hinting" mode="assign">
      <bool>false</bool>
    </edit>
  </match>

```

**Note:** You can switch BCI implementations by editing `/etc/profile.d/freetype2.sh` which includes a brief documentation. Possible values are `truetype:interpreter-version=35` (classic mode, emulates Windows 98; 2.6 default), `truetype:interpreter-version=38` ("Infinality" subpixel mode), `truetype:interpreter-version=40` (minimal subpixel mode; 2.7 default). Subpixel rendering should use a subpixel BCI. For details, see [[1]](https://www.freetype.org/freetype2/docs/subpixel-hinting.html).

#### Autohinter

The autohinter attempts to do automatic hinting and disregards any existing hinting information. Originally it was the default because TrueType2 fonts were patent-protected but now that these patents have expired there is very little reason to use it. It does work better with fonts that have broken or no hinting information but it will be strongly sub-optimal for fonts with good hinting information. Generally common fonts are of the later kind so autohinter will not be useful. Autohinter is **disabled** by default. To enable it:

```
  <match target="font">
    <edit name="autohint" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

```

#### Hintstyle

Hintstyle is the amount of font reshaping done to line up to the grid. Hinting values are: `hintnone`, `hintslight`, `hintmedium`, and `hintfull`. `hintslight` will make the font more fuzzy to line up to the grid but will be better in retaining font shape (see [[2]](https://www.freetype.org/freetype2/docs/text-rendering-general.html)), while `hintfull` will be a crisp font that aligns well to the pixel grid but will lose a greater amount of font shape. `hintslight` implicitly uses the autohinter in a vertical-only mode in favor of font-native information for non-CFF (*.otf*) fonts.

**`hintslight`** is the default setting. To change it:

```
  <match target="font">
    <edit name="hintstyle" mode="assign">
      <const>hintnone</const>
    </edit>
  </match>

```

**Note:** Some applications, like [GNOME](/index.php/GNOME "GNOME") may [override default hinting settings.](#Troubleshooting)

### Pixel alignment

Most monitors manufactured today use the Red, Green, Blue (RGB) specification. Fontconfig will need to know your monitor type to be able to display your fonts correctly. Monitors are either: **RGB** (most common), **BGR**, **V-RGB** (vertical), or **V-BGR**. A monitor test can be found [here](http://www.lagom.nl/lcd-test/subpixel.php).

```
  <match target="font">
    <edit name="rgba" mode="assign">
      <const>rgb</const>
    </edit>
  </match>

```

**Note:** Without subpixel rendering (see below), freetype will only care about the alignment (vertical or horizontal) of the subpixels. There is no difference between **RGB** and **BGR**, for example.

### Subpixel rendering

[Subpixel rendering](https://en.wikipedia.org/wiki/Subpixel_rendering "wikipedia:Subpixel rendering") is a technique to improve sharpness of font rendering by effectively tripling the horizontal (or vertical) resolution through the use of subpixels. On Windows machines, this technique is called "ClearType". Subpixel rendering is covered by Microsoft patents and **disabled** by default on Arch Linux. To enable it, you have to re-compile [freetype2](https://www.archlinux.org/packages/?name=freetype2) and define the `FT_CONFIG_OPTION_SUBPIXEL_RENDERING` macro, or use e.g. the AUR package [freetype2-cleartype](https://aur.archlinux.org/packages/freetype2-cleartype/).

To enable subpixel rendering, make sure that correct pixel alignment (see above) is configured.

#### LCD filter

When using subpixel rendering, you should enable the LCD filter, which is designed to reduce colour fringing. This is described under [LCD filtering](http://www.freetype.org/freetype2/docs/reference/ft2-lcd_filtering.html) in the FreeType 2 API reference. Different options are described under [FT_LcdFilter](http://www.freetype.org/freetype2/docs/reference/ft2-lcd_filtering.html#FT_LcdFilter), and are illustrated by this [LCD filter test](http://www.spasche.net/files/lcdfiltering/) page.

The `lcddefault` filter will work for most users. Other filters are available that can be used in special situations: `lcdlight`; a lighter filter ideal for fonts that look too bold or fuzzy, `lcdlegacy`, the original Cairo filter; and `lcdnone` to disable it entirely.

```
  <match target="font">
    <edit name="lcdfilter" mode="assign">
      <const>lcddefault</const>
    </edit>
  </match>

```

#### Advanced LCD filter specification

If the available built-in LCD filters are not satisfactory, it is possible to tweak the font rendering very specifically by building a custom freetype2 package and modifying the hardcoded filters. The [Arch Build System](/index.php/Arch_Build_System "Arch Build System") can be used to build and install packages from source.

First, refresh the freetype2 PKGBUILD as root:

```
# abs extra/freetype2

```

This example uses `/var/abs/build` as the build directory, substitute it according to your personal ABS setup. Download and extract the freetype2 package as a regular user:

```
$ cd /var/abs/build
$ cp -r ../extra/freetype2 .
$ cd freetype2
$ makepkg -o

```

Enable subpixel rendering by editing the file `src/freetype-VERSION/include/freetype/config/ftoption.h` and uncommenting the `FT_CONFIG_OPTION_SUBPIXEL_RENDERING` macro.

Then, edit the file `src/freetype-VERSION/src/base/ftlcdfil.c` and look up the definition of the constant `default_filter[5]`:

```
static const FT_Byte  default_filter[5] =
    { 0x10, 0x40, 0x70, 0x40, 0x10 };

```

This constant defines a low-pass filter applied to the rendered glyph. Modify it as needed. (reference: [freetype list discussion](https://lists.nongnu.org/archive/html/freetype/2006-09/msg00069.html)) Save the file, build and install the custom package:

```
$ makepkg -e
# pacman -Rd freetype2
# pacman -U freetype2-VERSION-ARCH.pkg.tar.xz

```

Reboot or restart X. The lcddefault filter should now render fonts differently.

### Disable auto-hinter for bold fonts

The auto-hinter uses sophisticated methods for font rendering, but often makes bold fonts too wide. Fortunately, a solution can be turning off the autohinter for bold fonts while leaving it on for the rest:

```
...
<match target="font">
    <test name="weight" compare="more">
        <const>medium</const>
    </test>
    <edit name="autohint" mode="assign">
        <bool>false</bool>
    </edit>
</match>
...

```

### Replace or set default fonts

The most reliable way to do this is to add an XML fragment similar to the one below. *Using the "binding" attribute will give you better results*, for example, in Firefox where you may not want to change properties of font being replaced. This will cause Ubuntu to be used in place of Georgia:

```
...
 <match target="pattern">
   <test qual="any" name="family"><string>georgia</string></test>
   <edit name="family" mode="assign" binding="same"><string>Ubuntu</string></edit>
 </match>
...

```

An alternate approach is to set the "preferred" font, but *this only works if the original font is not on the system*, in which case the one specified will be substituted:

```
...
<!-- Replace Helvetica with Bitstream Vera Sans Mono -->
<!-- Note, an alias for Helvetica should already exist in default conf files -->
<alias>
    <family>Helvetica</family>
    <prefer><family>Bitstream Vera Sans Mono</family></prefer>
    <default><family>fixed</family></default>
</alias>
...

```

### Whitelisting and blacklisting fonts

The element `<selectfont>` is used in conjunction with the `<acceptfont>` and `<rejectfont>` elements to selectively whitelist or blacklist fonts from the resolve list and match requests. The simplest and most typical use case it to reject one font that is needed to be installed, however is getting matched for a generic font query that is causing problems within application user interfaces.

First obtain the Family name as listed in the font itself:

 `$ fc-scan .fonts/lklug.ttf --format='%{family}
'`  `LKLUG` 

Then use that Family name in a `<rejectfont>` stanza:

```
<selectfont>
    <rejectfont>
        <pattern>
            <patelt name="family" >
                <string>LKLUG</string>
            </patelt>
        </pattern>
    </rejectfont>
</selectfont>

```

Typically when both elements are combined, `<rejectfont>` is first used on a more general matching glob to reject a large group (such as a whole directory), then `<acceptfont>` is used after it to whitelist individual fonts out of the larger blacklisted group.

```
<selectfont>
    <rejectfont>
        <glob>/usr/share/fonts/OTF/*</glob>
    </rejectfont>
    <acceptfont>
        <pattern>
            <patelt name="family" >
                <string>Monaco</string>
            </patelt>
        </pattern>
    </acceptfont>
</selectfont>

```

### Disable bitmap fonts

Bitmap fonts are sometimes used as fallbacks for missing fonts, which may cause text to be rendered pixelated or too large. Use the `70-no-bitmaps.conf` [preset](#Presets) to disable this behavior.

To disable embedded bitmap for all fonts:
 `~/.config/fontconfig/conf.d/20-no-embedded.conf` 
```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match target="font">
    <edit name="embeddedbitmap" mode="assign">
      <bool>false</bool>
    </edit>
  </match>
</fontconfig>

```

To disable embedded bitmap fonts for a specific font:

```
<match target="font">
  <test qual="any" name="family">
    <string>Monaco</string>
  </test>
  <edit name="embeddedbitmap">
    <bool>false</bool>
  </edit>
</match>

```

### Disable scaling of bitmap fonts

To disable scaling of bitmap fonts (which often makes them blurry), remove `/etc/fonts/conf.d/10-scale-bitmap-fonts.conf`.

### Create bold and italic styles for incomplete fonts

FreeType has the ability to automatically create *italic* and **bold** styles for fonts that do not have them, but only if explicitly required by the application. Given programs rarely send these requests, this section covers manually forcing generation of missing styles.

Start by editing `/usr/share/fonts/fonts.cache-1` as explained below. Store a copy of the modifications on another file, because a font update with `fc-cache` will overwrite `/usr/share/fonts/fonts.cache-1`.

Assuming the Dupree font is installed:

```
"dupree.ttf" 0 "Dupree:style=Regular:slant=0:weight=80:width=100:foundry=unknown:index=0:outline=True:*etc...*

```

Duplicate the line, change `style=Regular` to `style=Bold` or any other style. Also change `slant=0` to `slant=100` for italic, `weight=80` to `weight=200` for bold, or combine them for ***bold italic***:

```
"dupree.ttf" 0 "Dupree:style=Bold Italic:slant=100:weight=200:width=100:foundry=unknown:index=0:outline=True:*etc...*

```

Now add necessary modifications to `$XDG_CONFIG_HOME/fontconfig/fonts.conf`:

```
...
<match target="font">
    <test name="family" qual="any">
        <string>Dupree</string>
         <!-- other fonts here .... -->
     </test>
     <test name="weight" compare="more_eq"><int>140</int></test>
     <edit name="embolden" mode="assign"><bool>true</bool></edit>
</match>

<match target="font">
    <test name="family" qual="any">
        <string>Dupree</string>
        <!-- other fonts here .... -->
    </test>
    <test name="slant" compare="more_eq"><int>80</int></test>
    <edit name="matrix" mode="assign">
        <times>
            <name>matrix</name>
                <matrix>
                    <double>1</double><double>0.2</double>
                    <double>0</double><double>1</double>
                </matrix>
        </times>
    </edit>
</match>
...

```

**Tip:** Use the value 'embolden' for existing bold fonts in order to make them even bolder.

### Change rule overriding

Fontconfig processes files in `/etc/fonts/conf.d` in numerical order. This enables rules or files to override one another, but often confuses users about what file gets parsed last.

To guarantee that personal settings take precedence over any other rules, change their ordering:

```
# cd /etc/fonts/conf.d
# mv 50-user.conf 99-user.conf

```

This change seems however to be unnecessary for the most of the cases, because a user is given enough control by default to set up own font preferences, hinting and antialiasing properties, alias new fonts to generic font families, etc.

### Query the current settings

To find out what settings are in effect, use `fc-match --verbose`. eg.

 `$ fc-match --verbose Sans` 
```
family: "DejaVu Sans"(s)
hintstyle: 3(i)(s)
hinting: True(s)
...

```

Look up the meaning of the numbers at [http://www.freedesktop.org/software/fontconfig/fontconfig-user.html](http://www.freedesktop.org/software/fontconfig/fontconfig-user.html). Eg. 'hintstyle: 3' means 'hintfull'

## Applications without fontconfig support

Some applications like [URxvt](/index.php/URxvt "URxvt") and [Emacs](/index.php/Emacs "Emacs") will ignore fontconfig settings. You can work around this by using `~/.Xresources`, but it is as flexible as fontconfig. Example (see [#Fontconfig configuration](#Fontconfig_configuration) for explanations of the options):

 `~/.Xresources` 
```
Xft.autohint: 0
Xft.lcdfilter: lcddefault
Xft.hintstyle: hintslight
Xft.hinting: 1
Xft.antialias: 1
Xft.rgba: rgb

```

Make sure the settings are loaded properly when X starts with `xrdb -q` (see [Xresources](/index.php/Xresources "Xresources") for more information).

## Troubleshooting

### Distorted fonts

**Note:** 96 DPI is not a standard. You should use your monitor's actual DPI to get proper font rendering, especially when using subpixel rendering.

If fonts are still unexpectedly large or small, poorly proportioned or simply rendering poorly, fontconfig may be using the incorrect DPI.

Fontconfig should be able to detect DPI parameters as discovered by the Xorg server. You can check the automatically discovered DPI with `xdpyinfo` (provided by the [xorg-xdpyinfo](https://www.archlinux.org/packages/?name=xorg-xdpyinfo) package):

 `$ xdpyinfo | grep dots` 
```
  resolution:    102x102 dots per inch

```

If the DPI is detected incorrectly (usually due to an incorrect monitor [EDID](https://en.wikipedia.org/wiki/Extended_Display_Identification_Data "wikipedia:Extended Display Identification Data")), you can specify it manually in the Xorg configuration, see [Xorg#Display size and DPI](/index.php/Xorg#Display_size_and_DPI "Xorg"). This is the recommended solution, but it may not work with buggy drivers.

Fontconfig will default to the Xft.dpi variable if it is set. Xft.dpi is usually set by desktop environments (usually to Xorg's DPI setting) or manually in `~/.Xdefaults` or `~/.Xresources`. Use xrdb to query for the value:

 `$ xrdb -query | grep dpi` 
```
Xft.dpi:	102

```

Those still having problems can fall back to manually setting the DPI used by fontconfig:

```
...
<match target="pattern">
   <edit name="dpi" mode="assign"><double>102</double></edit>
</match>
...

```

### Calibri, Cambria, Monaco, etc. not rendering properly

Some scalable fonts have embedded bitmap versions which are rendered instead, mainly at smaller sizes. Using [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts") as replacements can improve the rendering in these cases.

You can also force using scalable fonts at all sizes by [disabling embedded bitmap](#Disable_bitmap_fonts), sacrificing some rendering quality.

### Applications overriding hinting

Some applications or desktop environments may override default fontconfig hinting and anti-aliasing settings. This may happen with [GNOME](/index.php/GNOME "GNOME") 3, for example while you are using Qt applications like [vlc](https://www.archlinux.org/packages/?name=vlc) or [smplayer](https://www.archlinux.org/packages/?name=smplayer). Use the specific configuration program for the application in such cases. For GNOME, try [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks).

### Applications not picking up hinting from DE's settings

For instance, under GNOME it sometimes happens that Firefox applies full hinting even when it's set to "none" in GNOME's settings, which results in sharp and widened fonts. In this case you would have to add hinting settings to your `fonts.conf` file:

```
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>	
<fontconfig>
 <match target="font">
  <edit mode="assign" name="hinting">
   <bool>false</bool>
  </edit>
 </match>
</fontconfig>

```

In this example, hinting is set to "grayscale".

### Incorrect hinting in GTK applications on non-Gnome systems

[GNOME](/index.php/GNOME "GNOME") uses the XSETTINGS system to configure font rendering. Outside of GNOME, GTK applications rely on fontconfig, but some fonts get the hinting wrong causing them to look too bold or too light.

A simple solution is using [xsettingsd-git](https://aur.archlinux.org/packages/xsettingsd-git/) to provide the configuration, for example:

 `~/.xsettingsd` 
```
Xft/Hinting 1
Xft/RGBA "rgb"
Xft/HintStyle "hintslight"
Xft/Antialias 1

```

Alternatively you could just write the font configuration as `Xft.*` directives in `~/.Xresources` without using a settings daemon.

### Helvetica font problem in generated PDFs

If the following command

```
fc-match helvetica

```

produces

```
helvR12-ISO8859-1.pcf.gz: "Helvetica" "Regular"

```

then the bitmap font provided by [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) is likely to be embedded into PDFs generated by "Print to File" or "Export" in various applications. The bitmap font was probably installed as a consequence of installing the whole [xorg](https://www.archlinux.org/groups/x86_64/xorg/) group (which is usually NOT recommended). To solve the pixelized font problem, you can uninstall the package. Install [gsfonts](https://www.archlinux.org/packages/?name=gsfonts) (Type 1) or [tex-gyre-fonts](https://www.archlinux.org/packages/?name=tex-gyre-fonts) (OpenType) for corresponding free subsitute of Helvetica (and other PostScript/PDF base fonts).

You may also experience similar problem when you open a PDF which requires Helvetica but does not have it embedded for viewing.

### FreeType Breaking Bitmap Fonts

Some users are reporting problems ([FS#52502](https://bugs.archlinux.org/task/52502)) with bitmap fonts having changed names after upgrading [freetype2](https://www.archlinux.org/packages/?name=freetype2) to version 2.7.1, creating havok in terminal emulators and several other programs such as [dwm](https://aur.archlinux.org/packages/dwm/) or [dmenu](https://www.archlinux.org/packages/?name=dmenu) by falling back to another (different) font. This was caused by the changes to the PCF font family format, which is described in their *release notes* [[4]](https://sourceforge.net/projects/freetype/files/freetype2/2.7.1/). Users transitioning from the old format might want to create a *font alias* to remedy the problems, like the solution which is described in [[5]](https://forum.manjaro.org/t/terminus-font-name-fix-after-freetype2-update-to-2-7-1-1/15530), given here too:

Assume we want to create an alias for [terminus-font](https://www.archlinux.org/packages/?name=terminus-font), which was renamed from `Terminus` to `xos4 Terminus` in the previously described [freetype2](https://www.archlinux.org/packages/?name=freetype2) update:

*   Create a configuration file in `/etc/fonts/conf.avail/` for the *font alias*:

 `/etc/fonts/conf.avail/33-TerminusPCFFont.conf` 
```
<?xml version="1.0"?>
 <!DOCTYPE fontconfig SYSTEM "fonts.dtd">
 <fontconfig>
     <alias>
         <family>Terminus</family>
         <prefer><family>xos4 Terminus</family></prefer>
         <default><family>fixed</family></default>
     </alias>
 </fontconfig>

```

*   Create a symbolic link towards it in the `/etc/fonts/conf.d` directory. In our example we would link as follows: `ln -s /etc/fonts/conf.avail/33-TerminusPCFFont.conf /etc/fonts/conf.d` to make the change permanent.

Everything should now work as it did before the update, the *font alias* should not be in effect, but make sure to either reload `.Xresources` or restart the display server first so the affected programs can use the alias.

## See also

*   [Fontconfig Users' Guide](http://www.freedesktop.org/software/fontconfig/fontconfig-user.html)
*   [Fonts in X11R6.8.2](http://www.x.org/X11R6.8.2/doc/fonts.html) - Official Xorg font information
*   [FreeType 2 overview](http://freetype.sourceforge.net/freetype2/)
*   [Gentoo font-rendering thread](https://forums.gentoo.org/viewtopic-t-723341.html)
*   [On slight hinting](http://www.freetype.org/freetype2/docs/text-rendering-general.html)