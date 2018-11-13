## Contents

*   [1 Инсталация](#Инсталация)
*   [2 Интерграция в KDE](#Интерграция_в_KDE)
*   [3 Допълнителни настройки](#Допълнителни_настройки)
    *   [3.1 Microsoft fonts and Opera](#Microsoft_fonts_and_Opera)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Java на Arch64](#Java_на_Arch64)
    *   [4.2 Шрифтът е прекалено голям](#Шрифтът_е_прекалено_голям)
    *   [4.3 Бавно скролване на графични карти nVidia](#Бавно_скролване_на_графични_карти_nVidia)

## Инсталация

Opera бе преместна в [AUR](/index.php/AUR "AUR") пордаи проблеми с лиценза.

Можете да инсталирате последната стабилна версия на Opera с [yaourt](/index.php/Yaourt "Yaourt"):

```
$ yaourt -S opera

```

**Note:** x86_64 потребителите могат да опитат да инсталират Opera чрез инсталационния скрипт включен в tar.gz файла от [http://www.opera.com/browser/download/](http://www.opera.com/browser/download/), понеже пакета на Opera има някои lib32 dependensies, които x86_64 потребителите може да не желаят. Инсталирайте qt3 (pacman -S qt3) след това. Също така имайте в предвид, че тази инсталация няма да бъде следена от pacman, така че **се препоръчва само за напреднали потребители**.

## Интерграция в KDE

In recent versions of Opera there is a somewhat obscure option `-systemstyle` which will apply KDE style settings instead of plain QT. However, you should test yourself your KDE selected theme is not causing instabilities i.e., sudden browser crashes.

If dialogs don't work for you, make sure

```
 File Selector -> Dialog Toolkit = 0

```

in `opera:config` advanced options.

## Допълнителни настройки

*   За да махнете иконата от системната лента, пуснете Opera с опцията `-notrayicon`:

```
 $ opera -notrayicon

```

*   За да не се ползват файлови разширения за поща:

```
 $ opera -nomail

```

*   To make the menus look integrated with Qt, install your preferred Qt4 theme and apply it by using `qtconfig` (`/usr/bin/qtconfig`, installed as a dependency for the non-static Opera package).

*   To make Opera use [KDE](/index.php/KDE "KDE") icons, download a native skin such as [fixed window skin](http://my.opera.com/community/customize/skins/info/?id=8908)

*   To improve flash performance in Opera, issue this command before starting opera, or add it to `~/.bash_profile` (alternatively, `/etc/profile` to make the change system-wide):

```
 export OPERAPLUGINWRAPPER_PRIORITY=0

```

### Microsoft fonts and Opera

**Note:** Можете да настроите шрифтовете от *Tools -> Preferences -> Advanced -> Fonts*, шрифтове от qtconfig са с приоритед над шрифтовете на GNOME.

Ако [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) не е инсталиран преди да пуснете Opera за първи път, Opera ще използва тези шрифтове по подразбиране, независимо какво е посочено в настройките на GTK, [GNOME](/index.php/GNOME "GNOME") или KDE font management, т.н.

За да настроите Opera да ползва настройките от вашия font manager:

1\. Затворете всички иснтанции на Opera.

2\. Премахнете ttf-ms-fonts.

```
# pacman -R tts-ms-fonts

```

3\. `rm -rf ~/.opera`

**Warning:** Това е предназначено за *нови* инсталации на Opera, понеже премахването на този път и всичките му компоненти ще рестартира настройките на Opera, кеша, отметките, т.н.

4\. Пуснете Opera отново. Можете да реинсталира ttf-ms-fonts след това.

```
# pacman -S tts-ms-fonts

```

## Troubleshooting

### Java на Arch64

1\. Инсталирайте среда на Java:

```
# pacman -S openjdk

```

За версията със свободен код, или:

```
# pacman -S jre

```

За версията на Sun със затворен код.

2\. Добавете към`~/.bash_profile`, или `/etc/profile` за да запазите настройките за всички потребители:

```
# openjdk
export LD_LIBRARY_PATH=/usr/lib/jvm/java-6-openjdk/jre/lib/amd64/server/
# jre
export LD_LIBRARY_PATH=/opt/java/jre/lib/amd64/server/

```

Или пък, направете символична връзка към `libjvm.so`:

```
# openjdk
cd /usr/lib/jvm/java-6-openjdk/jre/lib/amd64
ln -s server/libjvm.so .
# jre
cd /opt/java/jre/lib/amd64
ln -s server/libjvm.so .

```

3\. Редактирайте пътят към Java в Opera: *Menu -> Tools -> Preferences -> Advanced -> Content -> Java Options*.

```
#openjdk
/usr/lib/jvm/java-6-openjdk/jre/lib/amd64/
#jre
/opt/java/jre/lib/amd64/

```

### Шрифтът е прекалено голям

Нагласяйки Opera да ползва определени DPI насила може да помогне (ненужно за Opera 10 и по-нови).

Вкарайте:

```
opera:config

```

в лентата за адреси и потърсете "dpi". Избере DPI настройката в полетп "Force DPI", и запазете настройката като цъкнете "Save".

### Бавно скролване на графични карти nVidia

Опитайте следната команда:

```
$ nvidia-settings -a InitialPixmapPlacement=2

```