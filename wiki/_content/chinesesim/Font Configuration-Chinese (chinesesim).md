全局修改字体配置，修改`/etc/fonts/local.conf`, 配置用户字体，修改`$XDG_CONFIG_HOME/fontconfig/fonts.conf`.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Android显示效果的字体参考配置](#Android®显示效果的字体参考配置)
    *   [1.1 安装字体](#安装字体)
    *   [1.2 添加配置文件](#添加配置文件)
*   [2 Windows显示效果的字体参考配置](#Windows®显示效果的字体参考配置)
    *   [2.1 安装 MS core fonts](#安装_MS_core_fonts)
    *   [2.2 加入配置](#加入配置)
*   [3 Anti-aliasing效果的字体参考配置](#Anti-aliasing效果的字体参考配置)

## Android显示效果的字体参考配置

### 安装字体

```
pacman -S ttf-roboto noto-fonts noto-fonts-cjk adobe-source-han-sans-cn-fonts adobe-source-han-serif-cn-fonts ttf-dejavu

```

### 添加配置文件

```
~/.config/fontconfig/fonts.conf
or
/etc/fonts/local.conf
```

```

<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <its:rules xmlns:its="http://www.w3.org/2005/11/its" version="1.0">
    <its:translateRule
      translate="no"
      selector="/fontconfig/*[not(self::description)]"
    />
  </its:rules>

  <description>Android Font Config</description>

  <!-- Font directory list -->

  <dir>/usr/share/fonts</dir>
  <dir>/usr/local/share/fonts</dir>
  <dir prefix="xdg">fonts</dir>
  <!-- the following element will be removed in the future -->
  <dir>~/.fonts</dir>

  <!-- 关闭内嵌点阵字体 -->
  <match target="font">
    <edit name="embeddedbitmap" mode="assign">
      <bool>false</bool>
    </edit>
  </match>

  <!-- 英文默认字体使用 Roboto 和 Noto Serif ,终端使用 DejaVu Sans Mono. -->
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

  <!-- 中文默认字体使用思源黑体和思源宋体,不使用　Noto Sans CJK SC 是因为这个字体会在特定情况下显示片假字. -->
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

  <!-- Windows & Linux Chinese fonts. -->
  <!-- 把所有常见的中文字体映射到思源黑体和思源宋体，这样当这些字体未安装时会使用思源黑体和思源宋体.
解决特定程序指定使用某字体，并且在字体不存在情况下不会使用fallback字体导致中文显示不正常的情况. -->
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

  <!-- Load local system customization file -->
  <include ignore_missing="yes">conf.d</include>

  <!-- Font cache directory list -->

  <cachedir>/var/cache/fontconfig</cachedir>
  <cachedir prefix="xdg">fontconfig</cachedir>
  <!-- the following element will be removed in the future -->
  <cachedir>~/.fontconfig</cachedir>

  <config>
    <!-- Rescan configuration every 30 seconds when FcFontSetList is called -->
    <rescan>
      <int>30</int>
    </rescan>
  </config>
</fontconfig>

```

## Windows显示效果的字体参考配置

### 安装 MS core fonts

```
pacman -S ttf-ms-fonts

```

### 加入配置

```

       <match target="font">
                <edit name="autohint">
                        <bool>false</bool>
                </edit>
                <edit name="hinting">
                        <bool>true</bool>
                </edit>
                <edit name="antialias">
                        <bool>true</bool>
                </edit>
        </match>

<!--
 Synthetic emboldening for fonts that do not have bold face available
 -->

	<match target="font">
		<!-- check to see if the font is just regular -->
		<test name="weight" compare="less_eq">
			<const>medium</const>
		</test>
		<!-- check to see if the pattern requests bold -->
		<test target="pattern" name="weight" compare="more">
			<const>medium</const>
		</test>
		<!--
		  set the embolden flag
		  needed for applications using cairo, e.g. gucharmap, gedit, ...
		-->
		<edit name="embolden" mode="assign">
			<bool>true</bool>
		</edit>
		<!--
		 set weight to bold
		 needed for applications using Xft directly, e.g. Firefox, ...
		-->
		<edit name="weight" mode="assign">
			<const>bold</const>
		</edit>
	</match>

	<match target="font">
                <test target="pattern" name="lang" compare="contains">
                        <string>zh</string>
                        <string>ja</string>
                        <string>ko</string>
                </test>
                <edit name="spacing">
                        <const>proportional</const>
                </edit>
                <edit name="globaladvance">
                	<bool>false</bool>
                </edit>
        </match>

	<match target="pattern">
		<test name="family">
			<string>SimSun</string>
			<string>SimSun-18030</string>
			<string>AR PL ShanHeiSun Uni</string>
			<string>AR PL New Sung</string>
			<string>MingLiU</string>
			<string>PMingLiU</string>
		</test>
		<edit binding="strong" mode="prepend" name="family">
			<string>Tahoma</string>
			<string>Arial</string>
			<string>Verdana</string>
			<string>DejaVu Sans</string>
			<string>Bitstream Vera Sans</string>
		</edit>
	</match>

	<match target="font">
		<test name="family" qual="any">
			<string>AR PL ShanHeiSun Uni</string>
			<string>AR PL New Sung</string>
			<string>SimSun</string>
			<string>NSimSun</string>
			<string>MingLiu</string>
			<string>PMingLiu</string>
		</test>
		<test name="pixelsize" compare="less_eq">
			<double>12</double>
		</test>
		<edit name="pixelsize" mode="assign">
			<double>12</double>
		</edit>
	</match>

	<match target="font" >
 		<test compare="eq" name="family" qual="any" >
			<string>宋体</string>
			<string>新宋体</string>
			<string>SimSun</string>
			<string>NSimSun</string>
			<string>宋体-18030</string>
			<string>新宋体-18030</string>
			<string>SimSun-18030</string>
			<string>NSimSun-18030</string>
			<string>AR PL ShanHeiSun Uni</string>
			<string>AR PL New Sung</string>
			<string>MingLiU</string>
			<string>PMingLiU</string>
  		</test>
		<test compare="less_eq" name="pixelsize" >
			<double>16</double>
		</test>
		<edit mode="assign" name="hinting" >
		  	<bool>true</bool>
		</edit>
		<edit mode="assign" name="autohint" >
		  	<bool>false</bool>
		</edit>
                <edit name="antialias">
                        <bool>false</bool>
                </edit>
		<edit mode="assign" name="hintstyle" >
		  	<const>hintslight</const>
		</edit>
	</match>

        <match target="font">
                <test name="family">
                        <string>Andale Mono</string>
                        <string>Arial</string>
                        <string>Comic Sans MS</string>
                        <string>Georgia</string>
                        <string>Impact</string>
                        <string>Trebuchet MS</string>
                        <string>Verdana</string>
                        <string>Courier New</string>
                        <string>Times New Roman</string>
                        <string>Tahoma</string>
                        <string>Webdings</string>
                        <string>Albany AMT</string>
                        <string>Thorndale AMT</string>
                        <string>Cumberland AMT</string>
                        <string>Andale Sans</string>
                        <string>Andy MT</string>
                        <string>Bell MT</string>
                        <string>Monotype Sorts</string>
                </test>
		<test name="pixelsize" compare="less_eq">
				<double>16</double>
		</test>
                <edit name="autohint">
                        <bool>false</bool>
                </edit>
                <edit name="antialias">
                        <bool>false</bool>
                </edit>
	</match>

	<alias>
		<family>serif</family>
		<prefer>
			<family>Times New Roman</family>
			<family>Thorndale AMT</family>
			<family>Nimbus Roman No9 L</family>
			<family>DejaVu Serif</family>
			<family>Bitstream Vera Serif</family>
			<family>Luxi Serif</family>
			<family>Likhan</family>
			<family>FreeSerif</family>
			<family>Times</family>
			<family>SimSun</family>
			<family>SimSun-18030</family>
			<family>MingLiU</family>
			<family>WenQuanYi Bitmap Song</family>
			<family>AR PL ShanHeiSun Uni</family>
			<family>AR PL New Sung</family>
			<family>FZSongTi</family>
			<family>FZMingTiB</family>
			<family>AR PL SungtiL GB</family>
			<family>AR PL Mingti2L Big5</family>
			<family>Kochi Mincho</family>
			<family>UnBatang</family>
			<family>Baekmuk Batang</family>
			<family>HanyiSong</family>
			<family>ZYSong18030</family>
		</prefer>
	</alias>
	<alias>
		<family>sans-serif</family>
		<prefer>
			<family>Arial</family>
			<family>Albany AMT</family>
			<family>Nimbus Sans L</family>
			<family>Verdana</family>
			<family>DejaVu Sans</family>
			<family>Bitstream Vera Sans</family>
			<family>Luxi Sans</family>
			<family>FreeSans</family>
			<family>Helvetica</family>
			<family>SimSun</family>
			<family>SimSun-18030</family>
			<family>MingLiU</family>
			<family>WenQuanYi Bitmap Song</family>
			<family>AR PL ShanHeiSun Uni</family>
			<family>AR PL New Sung</family>
			<family>FZSongTi</family>
			<family>FZMingTiB</family>
			<family>AR PL SungtiL GB</family>
			<family>AR PL Mingti2L Big5</family>
			<family>Kochi Gothic</family>
			<family>UnDotum</family>
			<family>Baekmuk Gulim</family>
			<family>Baekmuk Dotum</family>
		</prefer>
	</alias>
	<alias>
		<family>monospace</family>
		<prefer>
			<family>Courier New</family>
			<family>Cumberland AMT</family>
			<family>Nimbus Mono L</family>
			<family>Andale Mono</family>
			<family>DejaVu Sans Mono</family>
			<family>Bitstream Vera Sans Mono</family>
			<family>Luxi Mono</family>
			<family>FreeMono</family>
			<family>NSimSun</family>
			<family>NSimSun-18030</family>
			<family>PMingLiU</family>
			<family>WenQuanYi Bitmap Song</family>
			<family>AR PL ShanHeiSun Uni</family>
			<family>AR PL New Sung</family>
			<family>FZSongTi</family>
			<family>FZMingTiB</family>
			<family>AR PL SungtiL GB</family>
			<family>AR PL Mingti2L Big5</family>
			<family>Kochi Gothic</family>
			<family>UnDotum</family>
			<family>Baekmuk Gulim</family>
			<family>Baekmuk Dotum</family>
			<family>HanyiSong</family>
			<family>ZYSong18030</family>
		</prefer>
	</alias>

```

## Anti-aliasing效果的字体参考配置

```

       <match target="font">
                <edit name="autohint">
                        <bool>true</bool>
                </edit>
                <edit name="hintstyle">
                        <const>hintfull</const>
                </edit>
                <edit name="antialias">
                        <bool>true</bool>
                </edit>
        </match>

	<match target="font">
		<!-- check to see if the font is just regular -->
		<test name="weight" compare="less_eq">
			<const>medium</const>
		</test>
		<!-- check to see if the pattern requests bold -->
		<test target="pattern" name="weight" compare="more">
			<const>medium</const>
		</test>
		<!--
		  set the embolden flag
		  needed for applications using cairo, e.g. gucharmap, gedit, ...
		-->
		<edit name="embolden" mode="assign">
			<bool>true</bool>
		</edit>
		<!--
		 set weight to bold
		 needed for applications using Xft directly, e.g. Firefox, ...
		-->
		<edit name="weight" mode="assign">
			<const>bold</const>
		</edit>
	</match>

	<match target="font">
                <test target="pattern" name="lang" compare="contains">
                        <string>zh</string>
                        <string>ja</string>
                        <string>ko</string>
                </test>
                <edit name="spacing">
                        <const>proportional</const>
                </edit>
                <edit name="globaladvance">
                	<bool>false</bool>
                </edit>
        </match>

	<match target="pattern">
		<test name="family">
			<string>SimSun</string>
			<string>SimSun-18030</string>
			<string>AR PL ShanHeiSun Uni</string>
			<string>AR PL New Sung</string>
			<string>MingLiU</string>
			<string>PMingLiU</string>
		</test>
		<edit binding="strong" mode="prepend" name="family">
			<string>Tahoma</string>
			<string>Arial</string>
			<string>Verdana</string>
			<string>DejaVu Sans</string>
			<string>Bitstream Vera Sans</string>
		</edit>
	</match>

	<match target="font">
		<test name="family" qual="any">
			<string>AR PL ShanHeiSun Uni</string>
			<string>AR PL New Sung</string>
			<string>SimSun</string>
			<string>NSimSun</string>
			<string>MingLiu</string>
			<string>PMingLiu</string>
		</test>
		<test name="pixelsize" compare="less_eq">
			<double>12</double>
		</test>
		<edit name="pixelsize" mode="assign">
			<double>12</double>
		</edit>
	</match>

	<match target="font" >
 	       <test compare="eq" name="family" qual="any" >
			<string>宋体</string>
			<string>新宋体</string>
			<string>SimSun</string>
			<string>NSimSun</string>
			<string>宋体-18030</string>
			<string>新宋体-18030</string>
			<string>SimSun-18030</string>
			<string>NSimSun-18030</string>
			<string>AR PL ShanHeiSun Uni</string>
			<string>AR PL New Sung</string>
			<string>MingLiU</string>
			<string>PMingLiU</string>
  		</test>
		<test compare="less_eq" name="pixelsize" >
			<double>16</double>
		</test>
		<edit mode="assign" name="hinting" >
		  	<bool>true</bool>
		</edit>
		<edit mode="assign" name="autohint" >
		  	<bool>false</bool>
		</edit>
                <edit name="antialias">
                        <bool>false</bool>
                </edit>
		<edit mode="assign" name="hintstyle" >
		  	<const>hintslight</const>
		</edit>
	</match>

	<alias>
		<family>serif</family>
		<prefer>
			<family>Nimbus Roman No9 L</family>
			<family>Thorndale AMT</family>
			<family>DejaVu Serif</family>
			<family>Bitstream Vera Serif</family>
			<family>Times New Roman</family>
			<family>Luxi Serif</family>
			<family>Likhan</family>
			<family>FreeSerif</family>
			<family>Times</family>
			<family>SimSun</family>
			<family>SimSun-18030</family>
			<family>MingLiU</family>
			<family>WenQuanYi Bitmap Song</family>
			<family>AR PL ShanHeiSun Uni</family>
			<family>AR PL New Sung</family>
			<family>FZSongTi</family>
			<family>FZMingTiB</family>
			<family>AR PL SungtiL GB</family>
			<family>AR PL Mingti2L Big5</family>
			<family>Kochi Mincho</family>
			<family>UnBatang</family>
			<family>Baekmuk Batang</family>
			<family>HanyiSong</family>
			<family>ZYSong18030</family>
		</prefer>
	</alias>
	<alias>
		<family>sans-serif</family>
		<prefer>
			<family>DejaVu Sans</family>
			<family>Bitstream Vera Sans</family>
			<family>Luxi Sans</family>
			<family>Arial</family>
			<family>Verdana</family>
			<family>Albany AMT</family>
			<family>Nimbus Sans L</family>
			<family>FreeSans</family>
			<family>Helvetica</family>
			<family>SimSun</family>
			<family>SimSun-18030</family>
			<family>MingLiU</family>
			<family>WenQuanYi Bitmap Song</family>
			<family>AR PL ShanHeiSun Uni</family>
			<family>AR PL New Sung</family>
			<family>FZSongTi</family>
			<family>FZMingTiB</family>
			<family>AR PL SungtiL GB</family>
			<family>AR PL Mingti2L Big5</family>
			<family>Kochi Gothic</family>
			<family>UnDotum</family>
			<family>Baekmuk Gulim</family>
			<family>Baekmuk Dotum</family>
		</prefer>
	</alias>
	<alias>
		<family>monospace</family>
		<prefer>
			<family>DejaVu Sans Mono</family>
			<family>Bitstream Vera Sans Mono</family>
			<family>Luxi Mono</family>
			<family>Courier New</family>
			<family>Cumberland AMT</family>
			<family>Nimbus Mono L</family>
			<family>Andale Mono</family>
			<family>FreeMono</family>
			<family>NSimSun</family>
			<family>NSimSun-18030</family>
			<family>PMingLiU</family>
			<family>WenQuanYi Bitmap Song</family>
			<family>AR PL ShanHeiSun Uni</family>
			<family>AR PL New Sung</family>
			<family>FZSongTi</family>
			<family>FZMingTiB</family>
			<family>AR PL SungtiL GB</family>
			<family>AR PL Mingti2L Big5</family>
			<family>Kochi Gothic</family>
			<family>UnDotum</family>
			<family>Baekmuk Gulim</family>
			<family>Baekmuk Dotum</family>
			<family>HanyiSong</family>
			<family>ZYSong18030</family>
		</prefer>
	</alias>

```