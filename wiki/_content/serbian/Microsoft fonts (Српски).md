| **Summary**  |
| Installing TrueType web-core (Microsoft) fonts and emulating Windows' font rendering |
| **Legal** |
| According to [original Microsoft's End User License Agreement](http://web.archive.org/web/20020227054122/www.microsoft.com/typography/fontpack/eula.htm), there are *some* legal limitations when using the fonts. |
| **Related** |
| [Fonts](/index.php/Fonts "Fonts"): Information on adding fonts and font recommendations |
| [Font Configuration](/index.php/Font_Configuration "Font Configuration"): Font setup and beautification |
| [Java Fonts - Sun JRE](/index.php/Java_Fonts_-_Sun_JRE "Java Fonts - Sun JRE"): Fonts specific to Sun's Java machine |

## Contents

*   [1 Sadržani Fontovi](#Sadr.C5.BEani_Fontovi)
*   [2 Upustvo](#Upustvo)
    *   [2.1 Instalacija iz riznice](#Instalacija_iz_riznice)
    *   [2.2 Ručno instaliranje](#Ru.C4.8Dno_instaliranje)
*   [3 Sharp fonts resembling Windows](#Sharp_fonts_resembling_Windows)

## Sadržani Fontovi

Sadržani fontovi u ttf-ms-fonts : Andale Mono, Arial, Arial Black, Comic, Courier New, Georgia, Impact, Lucida Sans, Lucida Console, Microsoft Sans Serif, Symbol, Tahoma, Times New Roman, Trebuchet, Verdana, Webdings and Wingdings.

## Upustvo

Trenutno poželjan način je da se instalira iz [extra] riznice. I ručni način je opisan za one koji žele ručno da instaliraju.

### Instalacija iz riznice

Pokrenite sledeću komandu da instalirate font:

```
# pacman -S ttf-ms-fonts

```

### Ručno instaliranje

Preuzeti fontove sa [freshmeat.net](http://freshmeat.net/projects/msfonts/).

Zatim instalirati:

```
$ tar xvf webcore-fonts-3.0.tar.gz
$ mkdir -p ~/.fonts/ms
$ cp webcore-fonts/fonts/* ~/.fonts/ms
$ cd ~/.fonts/ms
$ ttmkfdir >fonts.scale
$ mkfontdir
$ fc-cache -v

```

## Sharp fonts resembling Windows

Kompletan vodič kako da MS fontove podesite da budu kao na XP-u možete naći ovde [http://www.sharpfonts.co.cc/](http://www.sharpfonts.co.cc/). ukratko, instalirajte fontove kako je opisao autor, sa njegovim xml fajlom.