选择喜欢的一种显示效果的配置，加入/etc/fonts/local.conf 的<fontconfig>......</fontconfig>之间

把下面的配置加入/etc/fonts/local.conf

```
<match target="font">
        <edit name="embeddedbitmap">
                <bool>true</bool>
        </edit>
</match>

```

例如

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<!-- /etc/fonts/local.conf file for local customizations -->
<fontconfig>
.
.
.
.
.
.
        <match target="font">
                <edit name="embeddedbitmap">
                        <bool>true</bool>
                </edit>
        </match>
.
.
.
.
.
.
</fontconfig>

```

## 一. Windows(R)-Like 显示效果的字体参考配置

1\. 安装 MS core fonts

```
pacman -S ttf-ms-fonts

```

2\. 加入配置

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

## 二. Anti-aliasing效果的字体参考配置

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