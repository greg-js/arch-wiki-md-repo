See [Font configuration](/index.php/Font_configuration "Font configuration") for the main article.

Configurations can vary to a degree. Please post Fontconfig configurations with an explanation for why they were done.

## Contents

*   [1 Hinted fonts](#Hinted_fonts)
*   [2 No hinting for *italic* or **bold**](#No_hinting_for_italic_or_bold)
*   [3 Sharp fonts](#Sharp_fonts)
*   [4 Enable anti-aliasing only for bigger fonts](#Enable_anti-aliasing_only_for_bigger_fonts)
*   [5 Disable bold font](#Disable_bold_font)
*   [6 Default fonts](#Default_fonts)
    *   [6.1 Japanese](#Japanese)
    *   [6.2 Chinese](#Chinese)
*   [7 Patched packages](#Patched_packages)
*   [8 Infinality-like font substitution](#Infinality-like_font_substitution)
*   [9 See also](#See_also)

## Hinted fonts

 `~/.config/fontconfig/fonts.conf` 
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

## No hinting for *italic* or **bold**

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
    <edit name="hintstyle" mode="assign"><const>hintfull</const></edit>   <!-- try hintmedium if it looks bad -->
    <edit name="lcdfilter" mode="assign"><const>lcddefault</const></edit>
    <edit name="rgba" mode="assign"><const>rgb</const></edit>             <!-- set to match your display -->
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

## Disable bold font

For when a font does not present itself well in bold and you can't disable bold fonts in the application ([st](/index.php/St "St") for example).

```
...
<match target="pattern">
    <test qual="any" name="family">
        <string>Envy Code R</string>
    </test>
    <test name="weight" compare="more">
        <const>medium</const>
    </test>
    <edit name="weight" mode="assign" binding="same">
        <const>medium</const>
    </edit>
</match>
...

```

## Default fonts

For font consistency, all applications should be set to use the serif, sans-serif, and monospace aliases, which are mapped to particular fonts by fontconfig. See [Metric-compatible fonts](/index.php/Metric-compatible_fonts "Metric-compatible fonts") for options and examples.

### Japanese

Example fonts.conf which also specifies a default font for the Japanese locale (ja_JP) and keeps western style fonts for Latin letters.

```
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
<fontconfig>

<!-- Default font (no fc-match pattern) -->
 <match>
  <edit mode="prepend" name="family">
   <string>Noto Sans</string>
  </edit>
 </match>

<!-- Default font for the ja_JP locale (no fc-match pattern) -->
 <match>
  <test compare="contains" name="lang">
   <string>ja</string>
  </test>
  <edit mode="prepend" name="family">
   <string>Noto Sans CJK JP</string>
  </edit>
 </match>

<!-- Default sans-serif font -->
 <match target="pattern">
   <test qual="any" name="family"><string>sans-serif</string></test>
   <!--<test qual="any" name="lang"><string>ja</string></test>-->
   <edit name="family" mode="prepend" binding="same"><string>Noto Sans</string>  </edit>
 </match>

<!-- Default serif fonts -->
 <match target="pattern">
   <test qual="any" name="family"><string>serif</string></test>
   <edit name="family" mode="prepend" binding="same"><string>Noto Serif</string>  </edit>
   <edit name="family" mode="append" binding="same"><string>IPAPMincho</string>  </edit>
   <edit name="family" mode="append" binding="same"><string>HanaMinA</string>  </edit>
 </match>

<!-- Default monospace fonts -->
 <match target="pattern">
   <test qual="any" name="family"><string>monospace</string></test>
   <edit name="family" mode="prepend" binding="same"><string>Inconsolatazi4</string></edit>
   <edit name="family" mode="append" binding="same"><string>IPAGothic</string></edit>
 </match>

<!-- Fallback fonts preference order -->
 <alias>
  <family>sans-serif</family>
  <prefer>
   <family>Noto Sans</family>
   <family>Open Sans</family>
   <family>Droid Sans</family>
   <family>Ubuntu</family>
   <family>Roboto</family>
   <family>NotoSansCJK</family>
   <family>Source Han Sans JP</family>
   <family>IPAPGothic</family>
   <family>VL PGothic</family>
   <family>Koruri</family>
  </prefer>
 </alias>
 <alias>
  <family>serif</family>
  <prefer>
   <family>Noto Serif</family>
   <family>Droid Serif</family>
   <family>Roboto Slab</family>
   <family>IPAPMincho</family>
  </prefer>
 </alias>
 <alias>
  <family>monospace</family>
  <prefer>
   <family>Inconsolatazi4</family>
   <family>Ubuntu Mono</family>
   <family>Droid Sans Mono</family>
   <family>Roboto Mono</family>
   <family>IPAGothic</family>
  </prefer>
 </alias>

 <dir>~/.fonts</dir>
</fontconfig>

```

### Chinese

```
~/.config/fontconfig/fonts.conf
or
/etc/fonts/local.conf
```

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

	<match target="font">
		<edit name="embeddedbitmap" mode="assign">
			<bool>false</bool>
		</edit>
	</match>

	<match>
		<test qual="any" name="family">
			<string>serif</string>
		</test>
		<edit name="family" mode="prepend" binding="strong">
			<string>Noto Serif</string>
		</edit>
	</match>
	<match target="pattern">
		<test qual="any" name="family">
			<string>sans-serif</string>
		</test>
		<edit name="family" mode="prepend" binding="strong">
			<string>Roboto</string>
		</edit>
	</match>
	<match target="pattern">
		<test qual="any" name="family">
			<string>monospace</string>
		</test>
		<edit name="family" mode="prepend" binding="strong">
			<string>DejaVu Sans Mono</string>
		</edit>
	</match>

	<match>
		<test name="lang" compare="contains">
			<string>zh</string>
		</test>
		<test name="family">
			<string>serif</string>
		</test>
		<edit name="family" mode="prepend">
			<string>Source Han Serif CN</string>
		</edit>
	</match>
	<match>
		<test name="lang" compare="contains">
			<string>zh</string>
		</test>
		<test name="family">
			<string>sans-serif</string>
		</test>
		<edit name="family" mode="prepend">
			<string>Source Han Sans CN</string>
		</edit>
	</match>
	<match>
		<test name="lang" compare="contains">
			<string>zh</string>
		</test>
		<test name="family">
			<string>monospace</string>
		</test>
		<edit name="family" mode="prepend">
			<string>Noto Sans Mono CJK SC</string>
		</edit>
	</match>

<!--Windows & Linux Chinese fonts. -->
	<match target="pattern">
		<test qual="any" name="family">
			<string>WenQuanYi Zen Hei</string>
		</test>
		<edit name="family" mode="assign" binding="same">
			<string>Source Han Sans CN</string>
		</edit>
	</match>
	<match target="pattern">
                <test qual="any" name="family">
                        <string>WenQuanYi Micro Hei</string>
                </test>
                <edit name="family" mode="assign" binding="same">
                        <string>Source Han Sans CN</string>
                </edit>
	</match>
        <match target="pattern">
                <test qual="any" name="family">
                        <string>WenQuanYi Micro Hei Light</string>
                </test>
                <edit name="family" mode="assign" binding="same">
                        <string>Source Han Sans CN</string>
                </edit>
        </match>
	<match target="pattern">
                <test qual="any" name="family">
                        <string>Microsoft YaHei</string>
                </test>
                <edit name="family" mode="assign" binding="same">
                        <string>Source Han Sans CN</string>
                </edit>
        </match>
        <match target="pattern">
                <test qual="any" name="family">
                        <string>SimHei</string>
                </test>
                <edit name="family" mode="assign" binding="same">
                        <string>Source Han Sans CN</string>
                </edit>
        </match>
        <match target="pattern">
                <test qual="any" name="family">
                        <string>SimSun</string>
                </test>
                <edit name="family" mode="assign" binding="same">
                        <string>Source Han Serif CN</string>
                </edit>
        </match>
        <match target="pattern">
                <test qual="any" name="family">
                        <string>SimSun-18030</string>
                </test>
                <edit name="family" mode="assign" binding="same">
                        <string>Source Han Serif CN</string>
                </edit>
        </match>
</fontconfig>

```

## Patched packages

**Warning:** AUR packages are maintained separately from applications in the [official repositories](/index.php/Official_repositories "Official repositories"). The whole graphical system can become inoperable, if the user-installed core graphical libraries become incompatible.

**Note:**

*   Configuration is usually necessary.
*   The new font rendering will not be available until applications restart.
*   Applications which [statically link](https://en.wikipedia.org/wiki/Static_library "wikipedia:Static library") to a library will not be affected by the system library, or patches applied to it.

*   **freetype2-ubuntu** — Font configuration shipped with Ubuntu. [[1]](http://bazaar.launchpad.net/~ubuntu-branches/ubuntu/wily/fontconfig/wily/files/head:/debian/patches/) [[2]](http://bazaar.launchpad.net/~ubuntu-branches/ubuntu/wily/freetype/wily/files/head:/debian/patches-freetype/)

	[https://launchpad.net/ubuntu/+source/freetype](https://launchpad.net/ubuntu/+source/freetype) || [freetype2-ubuntu](https://aur.archlinux.org/packages/freetype2-ubuntu/) [fontconfig-ubuntu](https://aur.archlinux.org/packages/fontconfig-ubuntu/)

To restore the original packages, reinstall [freetype2](https://www.archlinux.org/packages/?name=freetype2), [cairo](https://www.archlinux.org/packages/?name=cairo), and [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) as dependencies (use the `--asdeps` flag with pacman when reinstalling). Include [lib32-cairo](https://www.archlinux.org/packages/?name=lib32-cairo), [lib32-fontconfig](https://www.archlinux.org/packages/?name=lib32-fontconfig), and [lib32-freetype2](https://www.archlinux.org/packages/?name=lib32-freetype2) if you also installed 32-bit versions.

## Infinality-like font substitution

For user provided fontconfig [substitutions](/index.php/Fonts#Font_alias "Fonts") replicating those offered with the [bundle](https://github.com/bohoomil/fontconfig-ultimate) install either [fonts-meta-extended-lt](https://aur.archlinux.org/packages/fonts-meta-extended-lt/) (light version) or [fonts-meta-extended](https://aur.archlinux.org/packages/fonts-meta-extended/) (complete version) and [enable](/index.php/Font_configuration#Presets "Font configuration") the provided `30-infinality-aliases.conf` preset.

## See also

*   [Gentoo forums](http://forums.gentoo.org/viewtopic-p-7273876.html#7273876)
*   [Thoroughly explained configuration that changes default fonts and sets fallback fonts for emoji and traditional Chinese characters](https://github.com/meribold/dotfiles/tree/master/home/config/fontconfig)