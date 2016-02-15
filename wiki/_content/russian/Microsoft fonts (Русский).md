Эта статья объясняет, как установить шрифты TrueType Microsoft и эмулировать рендеринг шрифтов Windows.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Использование шрифтов с раздела Windows](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2_.D1.81_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B0_Windows)
    *   [1.2 Текущие пакеты](#.D0.A2.D0.B5.D0.BA.D1.83.D1.89.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
    *   [1.3 Устаревшие пакеты](#.D0.A3.D1.81.D1.82.D0.B0.D1.80.D0.B5.D0.B2.D1.88.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
*   [2 Полезные правила Fontconfig для шрифтов MS](#.D0.9F.D0.BE.D0.BB.D0.B5.D0.B7.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D0.B0_Fontconfig_.D0.B4.D0.BB.D1.8F_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2_MS)
*   [3 Windows 7](#Windows_7)
*   [4 Windows 8](#Windows_8)

## Установка

### Использование шрифтов с раздела Windows

Если есть примонтированный раздел с установленной Windows, можно использовать шрифты Windows, ссылаясь на них.

_Например, если раздел Windows C:\ смонтирован в `/windows`:_

```
# ln -s /windows/Windows/Fonts /usr/share/fonts/WindowsFonts

```

Затем, обновите кэш fontconfig:

```
# fc-cache

```

В качестве альтернативы, скопируйте шрифты Windows, в `/usr/share/fonts`:

```
# mkdir /usr/share/fonts/WindowsFonts
# cp /windows/Windows/Fonts/* /usr/share/fonts/WindowsFonts
# chmod 755 /usr/share/fonts/WindowsFonts/*

```

Затем, обновите кэш fontconfig:

```
# fc-cache

```

### Текущие пакеты

**Обратите внимание:** Этим пакетам **требуется доступ Windows 7/8/10 и/или Office 2007** установки или установочный носитель, для подробностей обратитесь к соответствующему [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

*   [ttf-office-2007-fonts](https://aur.archlinux.org/packages/ttf-office-2007-fonts/) — шрифты Office 2007 fonts
*   [ttf-win7-fonts](https://aur.archlinux.org/packages/ttf-win7-fonts/) — шрифты Windows 7
*   [ttf-ms-win8](https://aur.archlinux.org/packages/ttf-ms-win8/) — шрифты Windows 8.1
*   [ttf-ms-win10](https://aur.archlinux.org/packages/ttf-ms-win10/) — шрифты Windows 10

### Устаревшие пакеты

**Обратите внимание:** Шрифты, представленные этими пакетами устаревшие, им не хватает современных инструкций hinting и полных наборов символов. Рекомендуется использовать вышеуказанные пакеты.

[ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) содержит:

*   [Andalé Mono](https://en.wikipedia.org/wiki/Andal%C3%A9_Mono "wikipedia:Andalé Mono")
*   [Arial](https://en.wikipedia.org/wiki/Arial "wikipedia:Arial")
*   [Arial Black](https://en.wikipedia.org/wiki/Arial_Black "wikipedia:Arial Black")
*   [Comic Sans](https://en.wikipedia.org/wiki/Comic_Sans "wikipedia:Comic Sans")
*   [Courier New](https://en.wikipedia.org/wiki/Courier_New "wikipedia:Courier New")
*   [Georgia](https://en.wikipedia.org/wiki/Georgia_(typeface) "wikipedia:Georgia (typeface)")
*   [Impact](https://en.wikipedia.org/wiki/Impact_(typeface) "wikipedia:Impact (typeface)")
*   [Lucida Sans](https://en.wikipedia.org/wiki/Lucida_Sans "wikipedia:Lucida Sans")
*   [Lucida Console](https://en.wikipedia.org/wiki/Lucida_Console "wikipedia:Lucida Console")
*   [Microsoft Sans Serif](https://en.wikipedia.org/wiki/Microsoft_Sans_Serif "wikipedia:Microsoft Sans Serif")
*   ~~[Symbol](https://en.wikipedia.org/wiki/Symbol_(typeface) "wikipedia:Symbol (typeface)")~~
*   [Times New Roman](https://en.wikipedia.org/wiki/Times_New_Roman "wikipedia:Times New Roman")
*   [Trebuchet](https://en.wikipedia.org/wiki/Trebuchet_MS "wikipedia:Trebuchet MS")
*   [Verdana](https://en.wikipedia.org/wiki/Verdana "wikipedia:Verdana")
*   [Webdings](https://en.wikipedia.org/wiki/Webdings "wikipedia:Webdings")
*   [Wingdings](https://en.wikipedia.org/wiki/Wingdings "wikipedia:Wingdings")

**Важно:** Согласно [оригиналу Лицензионного соглашения конечного пользователя от Microsoft](http://web.archive.org/web/20020227054122/www.microsoft.com/typography/fontpack/eula.htm), в нём есть _некоторые_ правовые ограничения при использовании шрифтов.

Вы также можете получить [ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/) который, как вы и ожидали, содержит [Tahoma](https://en.wikipedia.org/wiki/ru:%D0%A2%D0%B0%D1%85%D0%BE%D0%BC%D0%B0 "wikipedia:ru:Тахома").

[ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/) содержит:

*   [Calibri](https://en.wikipedia.org/wiki/Calibri "wikipedia:Calibri")
*   [Cambria](https://en.wikipedia.org/wiki/Cambria_(typeface) "wikipedia:Cambria (typeface)")
*   [Candara](https://en.wikipedia.org/wiki/Candara "wikipedia:Candara")
*   [Consolas](https://en.wikipedia.org/wiki/Consolas "wikipedia:Consolas")
*   [Constantia](https://en.wikipedia.org/wiki/Constantia_(typeface) "wikipedia:Constantia (typeface)")
*   [Corbel](https://en.wikipedia.org/wiki/Corbel_(typeface) "wikipedia:Corbel (typeface)")

## Полезные правила Fontconfig для шрифтов MS

Часто сайты задают шрифты, используя общие имена (helvetica, courier, times или times new roman) правило в fontconfig заменит эти (некрасивые) свободные шрифты:

```
/etc/fonts/conf.d/30-metric-aliases-free.conf

```

чтобы в полной мере использовать шрифты MS, необходимо создать правило сопоставления этих общих имен, конкретному MS шрифту, содержащемуся из вышеуказанных пакетов:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
       <alias binding="same">
         <family>Helvetica</family>
         <accept>
         <family>Arial</family>
         </accept>
       </alias>
       <alias binding="same">
         <family>Times</family>
         <accept>
         <family>Times New Roman</family>
         </accept>
       </alias>
       <alias binding="same">
         <family>Courier</family>
         <accept>
         <family>Courier New</family>
         </accept>
       </alias>
</fontconfig>

```

Также полезно ассоциировать serif, sans-serif, monospace шрифты в вашем любимом браузере, с шрифтами MS.

## Windows 7

Воспользуйтесь [патченным Infinality пакетом freetype2](/index.php/Infinality_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Infinality (Русский)"), и используйте профиль Windows 7 в provided (условиях) `local.conf`.

## Windows 8

Пакет [ttf-ms-win8](https://aur.archlinux.org/packages/ttf-ms-win8/) до настоящего времени, предназначен в качестве замены [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/), [ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/) и [ttf-win7-fonts](https://aur.archlinux.org/packages/ttf-win7-fonts/).

Хотя он обеспечивает более новые версии шрифтов, он **не может автоматически загружать шрифты** по лицензионным соображениям.

**Обратите внимание:** Использование Microsoft шрифтов за пределами работы системы Windows запрещено EULA (хотя в некоторых странах Лицензионное соглашение является недействительным). Пожалуйста, примите во внимание лицензию Microsoft, прежде чем использовать шрифты.

Вы можете приобрести шрифты установленной и полностью обновленной системы Windows 8.1\. Любое издание _Windows 8.1 build **Windows 8.1 6.3.9600.17238**_ будет работать.

На установленной системе Windows 8.1 шрифты, как правило, находится в `[%WINDIR%](http://technet.microsoft.com/en-us/library/hh825266.aspx)\Fonts`, и файл лицензии `[%SYSTEM32%](http://technet.microsoft.com/en-us/library/hh825266.aspx)\license.rtf`.

Вам нужны файлы, перечисленные в массиве `source=()`. Поместите их в той же директории, что и этот файл [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), а затем запустите [makepkg](/index.php/Makepkg "Makepkg").

`makepkg --pkg ttf-ms-win8` сделает пакет основных шрифтов Windows 8.1 который охватывает даже больше, чем [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/).

Шрифты лучше всего рассматривать с [Infinality](/index.php/Infinality_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Infinality (Русский)"). Infinality предлагает большой рендеринг шрифтов и настроек.