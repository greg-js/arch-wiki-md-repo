**Состояние перевода:** На этой странице представлен перевод статьи [Font configuration/Examples](/index.php/Font_configuration/Examples "Font configuration/Examples"). Дата последней синхронизации: 6 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Font_configuration/Examples&diff=0&oldid=424396).

Основная статья: [Настройка шрифтов](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%88%D1%80%D0%B8%D1%84%D1%82%D0%BE%D0%B2 "Настройка шрифтов").

Настройки могут варьироваться в значительной степени. Пожалуйста, приводите примеры настроек Fontconfig с объяснением того, что они делают.

## Contents

*   [1 Хинтованные шрифты](#.D0.A5.D0.B8.D0.BD.D1.82.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D1.8B.D0.B5_.D1.88.D1.80.D0.B8.D1.84.D1.82.D1.8B)
*   [2 Отключение хинтинга для *курсивных* или **жирных** шрифтов](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.85.D0.B8.D0.BD.D1.82.D0.B8.D0.BD.D0.B3.D0.B0_.D0.B4.D0.BB.D1.8F_.D0.BA.D1.83.D1.80.D1.81.D0.B8.D0.B2.D0.BD.D1.8B.D1.85_.D0.B8.D0.BB.D0.B8_.D0.B6.D0.B8.D1.80.D0.BD.D1.8B.D1.85_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2)
*   [3 Резкие шрифты](#.D0.A0.D0.B5.D0.B7.D0.BA.D0.B8.D0.B5_.D1.88.D1.80.D0.B8.D1.84.D1.82.D1.8B)
*   [4 Шрифты семейства Liberation](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B_.D1.81.D0.B5.D0.BC.D0.B5.D0.B9.D1.81.D1.82.D0.B2.D0.B0_Liberation)
*   [5 Включение сглаживания (anti-aliasing) только для больших шрифтов](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.B3.D0.BB.D0.B0.D0.B6.D0.B8.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.28anti-aliasing.29_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.B4.D0.BB.D1.8F_.D0.B1.D0.BE.D0.BB.D1.8C.D1.88.D0.B8.D1.85_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2)
*   [6 Шрифты Chrome OS](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B_Chrome_OS)
*   [7 Патченные пакеты](#.D0.9F.D0.B0.D1.82.D1.87.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
*   [8 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Хинтованные шрифты

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

## Отключение хинтинга для *курсивных* или **жирных** шрифтов

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

## Резкие шрифты

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

## Шрифты семейства Liberation

Для достижения единства шрифтов во всей системе все приложения должны быть настроены на использование псевдонимов serif, sans-serif и monospace, значения для которых должны быть выставлены в fontconfig. Шрифты Liberation были выбраны для того, чтобы придерживаться метрической совместимости со шрифтами MS Core.

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

## Включение сглаживания (anti-aliasing) только для больших шрифтов

Некоторые пользователи предпочитают более чёткое отображение, которого anti-aliasing не позволяет добиться:

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

## Шрифты Chrome OS

Веб-браузер и другие распространенные приложения используют шрифты ([псевдонимы шрифтов](/index.php/Fonts#Font_alias "Fonts")) `Serif`, `Sans-Serif` и `Monospace` по умолчанию. Процедура изменения шрифтов по умолчанию похожа на их замену. Например, чтобы использовать шрифты Chrome OS из пакета [ttf-chromeos-fonts](https://aur.archlinux.org/packages/ttf-chromeos-fonts/):

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

## Патченные пакеты

**Важно:** Пакеты AUR поддерживаются отдельно от приложений из [Официальных репозиториев](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8 "Официальные репозитории"). Вся графическая система может выйти из строя, если установленные пользователем основные графические библиотеки станут несовместимыми.

**Примечание:**

*   Как правило, необходима настройка.
*   Новое отображение шрифтов не начнется, пока не перезагрузите приложения.
*   Приложения которые [статически ссылаются](https://en.wikipedia.org/wiki/Static_library "wikipedia:Static library") на библиотеку, не будут использовать патчи принятые к системной библиотеке.

*   **freetype2-ubuntu** — Настройки шрифтов поставляемых с Ubuntu. [[1]](http://bazaar.launchpad.net/~ubuntu-branches/ubuntu/wily/fontconfig/wily/files/head:/debian/patches/) [[2]](http://bazaar.launchpad.net/~ubuntu-branches/ubuntu/wily/freetype/wily/files/head:/debian/patches-freetype/)

	[https://launchpad.net/ubuntu/+source/freetype](https://launchpad.net/ubuntu/+source/freetype) || [freetype2-ubuntu](https://aur.archlinux.org/packages/freetype2-ubuntu/) [fontconfig-ubuntu](https://aur.archlinux.org/packages/fontconfig-ubuntu/)

*   **[Infinality](/index.php/Infinality_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Infinality (Русский)")** — Файлы настроек шрифтов, патчи, и скрипты.

	[https://github.com/bohoomil/fontconfig-ultimate](https://github.com/bohoomil/fontconfig-ultimate) || [freetype2-infinality](https://aur.archlinux.org/packages/freetype2-infinality/) [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/)

Для восстановления непатченых пакетов, установите оригинальные пакеты [freetype2](https://www.archlinux.org/packages/?name=freetype2), [cairo](https://www.archlinux.org/packages/?name=cairo), и [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) в качестве зависимостей (используя флаг `--asdeps` при переустановки с помощью pacman). Включите [lib32-cairo](https://www.archlinux.org/packages/?name=lib32-cairo), [lib32-fontconfig](https://www.archlinux.org/packages/?name=lib32-fontconfig), и [lib32-freetype2](https://www.archlinux.org/packages/?name=lib32-freetype2) если вы также устанавливали 32-разрядные версии.

## Смотрите также

*   [Форум Gentoo (Англ.)](http://forums.gentoo.org/viewtopic-p-7273876.html#7273876)