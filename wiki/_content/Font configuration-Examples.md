# Font configuration/Examples

See [Font configuration](/index.php/Font_configuration "Font configuration") for the main article.

Configurations can vary to a degree. Please post Fontconfig configurations with an explanation for why they were done.

## Contents

*   [1 Hinted fonts](#Hinted_fonts)
*   [2 No hinting for _italic_ or **bold**](#No_hinting_for_italic_or_bold)
*   [3 Sharp fonts](#Sharp_fonts)
*   [4 Liberation fonts](#Liberation_fonts)
*   [5 Enable anti-aliasing only for bigger fonts](#Enable_anti-aliasing_only_for_bigger_fonts)
*   [6 Chrome OS fonts](#Chrome_OS_fonts)
*   [7 Patched packages](#Patched_packages)
*   [8 See also](#See_also)

## Hinted fonts

 `$XDG_CONFIG_HOME/fontconfig/fonts.conf` 

```
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
<fontconfig>
	<match target="font">
		<edit mode="assign" name="antialias">
			<bool>true</bool>
		</edit>
		<edit mode="assign" name="embeddedbitmap">
			<bool>false</bool>
		</edit>
		<edit mode="assign" name="hinting">
			<bool>true</bool>
		</edit>
		<edit mode="assign" name="hintstyle">
			<const>hintslight</const>
		</edit>
		<edit mode="assign" name="lcdfilter">
			<const>lcddefault</const>
		</edit>
		<edit mode="assign" name="rgba">
			<const>rgb</const>
		</edit>
	</match>
</fontconfig>

```

## No hinting for _italic_ or **bold**

```
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
<fontconfig>
  <match target="font" >
    <edit mode="assign" name="autohint">  <bool>true</bool></edit>
    <edit mode="assign" name="hinting">	  <bool>false</bool></edit>
    <edit mode="assign" name="lcdfilter"> <const>lcddefault</const></edit>
    <edit mode="assign" name="hintstyle"> <const>hintslight</const></edit>
    <edit mode="assign" name="antialias"> <bool>true</bool></edit>
    <edit mode="assign" name="rgba">      <const>rgb</const></edit>
  </match>

  <match target="font">
    <test name="pixelsize" qual="any" compare="more"><double>15</double></test>
    <edit mode="assign" name="lcdfilter"><const>lcdlight</const></edit>
    <edit mode="assign" name="hintstyle"><const>hintnone</const></edit>
  </match>

  <match target="font">
    <test name="weight" compare="more"><const>medium</const></test>
    <edit mode="assign" name="hintstyle"><const>hintnone</const></edit>
    <edit mode="assign" name="lcdfilter"><const>lcdlight</const></edit>
  </match>

  <match target="font">
    <test name="slant"  compare="not_eq"><double>0</double></test>
    <edit mode="assign" name="hintstyle"><const>hintnone</const></edit>
    <edit mode="assign" name="lcdfilter"><const>lcdlight</const></edit>
  </match>

</fontconfig>

```

## Sharp fonts

```
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match target="font">
    <edit name="antialias" mode="assign"><bool>true</bool></edit>
    <edit name="hinting" mode="assign"><bool>true</bool></edit>
    <edit name="hintstyle" mode="assign"><const>hintfull</const></edit>
    <edit name="lcdfilter" mode="assign"><const>lcddefault</const></edit>
    <edit name="rgba" mode="assign"><const>rgb</const></edit>
  </match>
</fontconfig>

```

## Liberation fonts

For font consistency, all applications should be set to use the serif, sans-serif, and monospace aliases, which are mapped to particular fonts by fontconfig. The Liberation fonts were chosen to follow metric-compatibility of the MS Core fonts.

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
    <match target="font">
        <edit mode="assign" name="antialias"><bool>true</bool></edit>
        <edit mode="assign" name="autohint"><bool>false</bool></edit>
        <edit mode="assign" name="embeddedbitmap"><bool>false</bool></edit>
        <edit mode="assign" name="hinting"><bool>true</bool></edit>
        <edit mode="assign" name="hintstyle"><const>hintslight</const></edit>
        <edit mode="assign" name="lcdfilter"><const>lcddefault</const></edit>
        <edit mode="assign" name="rgba"><const>rgb</const></edit>
    </match>

    <match target="pattern">
        <test qual="any" name="family"><string>serif</string></test>
        <edit name="family" mode="assign" binding="same"><string>Liberation Serif</string></edit>
    </match>
    <match target="pattern">
        <test qual="any" name="family"><string>sans-serif</string></test>
        <edit name="family" mode="assign" binding="same"><string>Liberation Sans</string></edit>
    </match>
    <match target="pattern">
        <test qual="any" name="family"><string>monospace</string></test>
        <edit name="family" mode="assign" binding="same"><string>Liberation Mono</string></edit>
    </match>

    <match target="pattern">
        <edit name="dpi" mode="assign"><double>96</double></edit>
    </match>
</fontconfig>
```

## Enable anti-aliasing only for bigger fonts

Some users prefer the sharper rendering that anti-aliasing does not offer:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match target="font">
    <edit name="antialias" mode="assign">
      <bool>false</bool>
    </edit>
  </match>

  <match target="font" >
    <test name="size" qual="any" compare="more">
      <double>12</double>
    </test>
    <edit name="antialias" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

  <match target="font" >
    <test name="pixelsize" qual="any" compare="more">
      <double>16</double>
    </test>
    <edit name="antialias" mode="assign">
      <bool>true</bool>
    </edit>
  </match>
</fontconfig>

```

## Chrome OS fonts

Web browser and another common applications use `Serif`, `Sans-Serif` and `Monospace` as default fonts ([Fonts#Font alias](/index.php/Fonts#Font_alias "Fonts")). The procedure to change default fonts is similar to replace them. For example, to use Chrome OS fonts [ttf-chromeos-fonts](https://aur.archlinux.org/packages/ttf-chromeos-fonts/)<sup><small>AUR</small></sup>:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <!-- Set preferred serif, sans serif, and monospace fonts. -->
  <alias>
    <family>serif</family>
    <prefer><family>Tinos</family></prefer>
  </alias>
  <alias>
    <family>sans-serif</family>
    <prefer><family>Arimo</family></prefer>
  </alias>
  <alias>
    <family>sans</family>
    <prefer><family>Arimo</family></prefer>
  </alias>
  <alias>
    <family>monospace</family>
    <prefer><family>Cousine</family></prefer>
  </alias>
</fontconfig>

```

## Patched packages

**Warning:** AUR packages are maintained separately from applications in the [official repositories](/index.php/Official_repositories "Official repositories"). The whole graphical system can become inoperable, if the user-installed core graphical libraries become incompatible.

**Note:**

*   Configuration is usually necessary.
*   The new font rendering will not be available until applications restart.
*   Applications which [statically link](https://en.wikipedia.org/wiki/Static_library "wikipedia:Static library") to a library will not be affected by the system library, or patches applied to it.

*   **freetype2-ubuntu** — Font configuration shipped with Ubuntu. [[1]](http://bazaar.launchpad.net/~ubuntu-branches/ubuntu/wily/fontconfig/wily/files/head:/debian/patches/) [[2]](http://bazaar.launchpad.net/~ubuntu-branches/ubuntu/wily/freetype/wily/files/head:/debian/patches-freetype/)

	[https://launchpad.net/ubuntu/+source/freetype](https://launchpad.net/ubuntu/+source/freetype) || [freetype2-ubuntu](https://aur.archlinux.org/packages/freetype2-ubuntu/)<sup><small>AUR</small></sup> [fontconfig-ubuntu](https://aur.archlinux.org/packages/fontconfig-ubuntu/)<sup><small>AUR</small></sup>

*   **[Infinality](/index.php/Infinality "Infinality")** — Font configuration files, patches, and scripts.

	[https://github.com/bohoomil/fontconfig-ultimate](https://github.com/bohoomil/fontconfig-ultimate) || [freetype2-infinality](https://aur.archlinux.org/packages/freetype2-infinality/)<sup><small>AUR</small></sup> [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/)<sup><small>AUR</small></sup>

To restore the original packages, reinstall [freetype2](https://www.archlinux.org/packages/?name=freetype2), [cairo](https://www.archlinux.org/packages/?name=cairo), and [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) as dependencies (use the `--asdeps` flag with pacman when reinstalling). Include [lib32-cairo](https://www.archlinux.org/packages/?name=lib32-cairo), [lib32-fontconfig](https://www.archlinux.org/packages/?name=lib32-fontconfig), and [lib32-freetype2](https://www.archlinux.org/packages/?name=lib32-freetype2) if you also installed 32-bit versions.

## See also

*   [Gentoo forums](http://forums.gentoo.org/viewtopic-p-7273876.html#7273876)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Font_configuration/Examples&oldid=412420](https://wiki.archlinux.org/index.php?title=Font_configuration/Examples&oldid=412420)"