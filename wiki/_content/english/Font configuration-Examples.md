See [Font configuration](/index.php/Font_configuration "Font configuration") for the main article.

Configurations can vary to a degree. Please post Fontconfig configurations with an explanation for why they were done.

## Contents

*   [1 Hinted fonts](#Hinted_fonts)
*   [2 No hinting for italic or bold](#No_hinting_for_italic_or_bold)
*   [3 Enable anti-aliasing only for bigger fonts](#Enable_anti-aliasing_only_for_bigger_fonts)
*   [4 Disable bold font](#Disable_bold_font)
*   [5 Disable ligatures for monospaced fonts](#Disable_ligatures_for_monospaced_fonts)
*   [6 Default fonts](#Default_fonts)
    *   [6.1 Japanese](#Japanese)
    *   [6.2 Chinese](#Chinese)
*   [7 See also](#See_also)

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

## No hinting for italic or bold

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

## Disable ligatures for monospaced fonts

This prevents letter combinations like "ffi" from being squashed into a single-width character in some monospaced fonts. The whole `<match>` block needs to be duplicated to include extra fonts.

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <description>Disable ligatures for monospaced fonts to avoid ff, fi, ffi, etc. becoming only one character wide</description>

  <match target="font">
    <test name="family" compare="eq" ignore-blanks="true">
      <string>Nimbus Mono PS</string>
    </test>
    <edit name="fontfeatures" mode="append">
      <string>liga off</string>
      <string>dlig off</string>
    </edit>
  </match>
</fontconfig>

```

You can test the effectiveness of this with the following command:

```
$ echo -e "| worksheet |
| buffering |
| difficult |
| finishing |
| different |
| efficient |" | pango-view --font="Nimbus Mono PS" /dev/stdin

```

Some programs (such as Firefox) do not support the `fontfeatures` tag, so for those replacing the font with another is the only option. See [Font configuration#Replace or set default fonts](/index.php/Font_configuration#Replace_or_set_default_fonts "Font configuration") for details.

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

## See also

*   [Gentoo forums](http://forums.gentoo.org/viewtopic-p-7273876.html#7273876)