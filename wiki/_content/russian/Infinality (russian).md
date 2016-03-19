**Состояние перевода:** На этой странице представлен перевод статьи [Infinality](/index.php/Infinality "Infinality"). Дата последней синхронизации: 27 декабря 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Infinality&diff=0&oldid=413518).

Набор патчей [Infinality](http://www.infinality.net/) стремится значительно улучшить отрисовку шрифтов freetype2, и добавляет несколько новых возможностей.

## Contents

*   [1 Особенности](#.D0.9E.D1.81.D0.BE.D0.B1.D0.B5.D0.BD.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [2.1 Infinality-bundle](#Infinality-bundle)
        *   [2.1.1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_2)
        *   [2.1.2 Рекомендуемые шрифты с ограниченными лицензиями](#.D0.A0.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D1.83.D0.B5.D0.BC.D1.8B.D0.B5_.D1.88.D1.80.D0.B8.D1.84.D1.82.D1.8B_.D1.81_.D0.BE.D0.B3.D1.80.D0.B0.D0.BD.D0.B8.D1.87.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC.D0.B8_.D0.BB.D0.B8.D1.86.D0.B5.D0.BD.D0.B7.D0.B8.D1.8F.D0.BC.D0.B8)
        *   [2.1.3 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
        *   [2.1.4 Больше шрифтов](#.D0.91.D0.BE.D0.BB.D1.8C.D1.88.D0.B5_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.BE.D0.B2)
        *   [2.1.5 Замены шрифта](#.D0.97.D0.B0.D0.BC.D0.B5.D0.BD.D1.8B_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.B0)
        *   [2.1.6 Подписи пакетов](#.D0.9F.D0.BE.D0.B4.D0.BF.D0.B8.D1.81.D0.B8_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
        *   [2.1.7 Обновление](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [2.2 Апстрим infinality](#.D0.90.D0.BF.D1.81.D1.82.D1.80.D0.B8.D0.BC_infinality)
*   [3 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 Spotify проблемы шрифта](#Spotify_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.B0)
    *   [3.2 Google Chrome проблемы](#Google_Chrome_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B)
    *   [3.3 Emacs](#Emacs)
    *   [3.4 GIMP](#GIMP)
    *   [3.5 Неправильно отображаются специальные языковые символы / глифы](#.D0.9D.D0.B5.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D1.8C.D0.BD.D0.BE_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D1.81.D0.BF.D0.B5.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.8F.D0.B7.D1.8B.D0.BA.D0.BE.D0.B2.D1.8B.D0.B5_.D1.81.D0.B8.D0.BC.D0.B2.D0.BE.D0.BB.D1.8B_.2F_.D0.B3.D0.BB.D0.B8.D1.84.D1.8B)
    *   [3.6 Браузеры Firefox/Chrome рендерят моноширный шрифт как пропорциональный](#.D0.91.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80.D1.8B_Firefox.2FChrome_.D1.80.D0.B5.D0.BD.D0.B4.D0.B5.D1.80.D1.8F.D1.82_.D0.BC.D0.BE.D0.BD.D0.BE.D1.88.D0.B8.D1.80.D0.BD.D1.8B.D0.B9_.D1.88.D1.80.D0.B8.D1.84.D1.82_.D0.BA.D0.B0.D0.BA_.D0.BF.D1.80.D0.BE.D0.BF.D0.BE.D1.80.D1.86.D0.B8.D0.BE.D0.BD.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9)
    *   [3.7 Общие проблемы со шрифтами](#.D0.9E.D0.B1.D1.89.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81.D0.BE_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.B0.D0.BC.D0.B8)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Особенности

Все настройки Infinality задаются во время выполнения с помощью переменных сред в `/etc/X11/xinit/xinitrc.d/xft-settings.sh`, и включают следующее:

*   **Emboldening Enhancement**: Отключение Y Emboldening, производит гораздо приятный результат на шрифты без утолщённых версий. Работает на родном TT Hinter и autohinter.
*   **Auto-Autohint**: Автоматически ставит autohint на шрифты, которые не содержат никаких инструкций TT.
*   **Autohint Enhancement**: Makes autohint snap horizontal stems to pixels. Gives a result that appears like a well-hinted truetype font, but is 100% patent-free (as far as I know).
*   **Customized FIR Filter**: Выберите свои собственные [значения фильтра](http://www.infinality.net/forum/viewtopic.php?f=2&t=19) во время выполнения. Работает на родном TT Hinter и autohinter.
*   **Stem Alignment**: Выравнивает растровые глифы оптимизированных границ пикселей. Работает на родном TT Hinter и autohinter.
*   **Pseudo Gamma Correction**: Глифы светлее и темнее, при заданном значении ниже данного размера. Работает на родном TT Hinter и autohinter.
*   **Embolden Thin Fonts**: Делает тонкие или лёгкие шрифты более заметными. Работает на autohinter.
*   **Force Slight Hinting**: Принудительно использовать slight hinting, даже когда программы запрашивают full hinting. Если вы используете local.conf, который я предоставляю (включенный в пакет fedora infinality-settings), то вы заметите улучшения отображения шрифтов.
*   **ChromeOS Style Sharpening**: Использует патч ChromeOS , чтобы сделать резче вид шрифтов. В настоящее время включено в набор патчей infinality.

Для подробностей смотрите [README](http://www.infinality.net/forum/viewtopic.php?f=2&t=18).

Ряд предустановок включено, и может быть использовано, путем установки переменной USE_STYLE в `/etc/X11/xinit/xinitrc.d/xft-settings.sh`.

**Примечание:** Файл `/etc/X11/xinit/xinitrc.d/infinality-settings.sh` часто меняет своё содержимое, в зависимости от версии. Все стили отображения, и перечисленные настройки параметров, смотрите [[в файле настроек с примерами и описанием](https://github.com/bohoomil/fontconfig-ultimate/blob/master/freetype/generic_settings/infinality-settings.sh)]. Можете скопировать его себе полностью, взяв за основу.

## Установка

### Infinality-bundle

**Infinality-bundle** представляет собой набор программного обеспечения, направленного на улучшение визуализации текста в Arch Linux.

В настоящее время, в комплект входят:

*   *freetype2-infinality-ultimate* - [freetype2](https://www.archlinux.org/packages/?name=freetype2) собранный с [Infinality](http://www.infinality.net/blog/) и дополнительными патчами.
*   *fontconfig-infinality-ultimate* - [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) оптимизированный для использования *freetype2-infinality-ultimate*, включая отдельные предустановки для свободных шрифтов (по умолчанию), шрифтов MS и коллекции пользовательских шрифтов.
*   *cairo-infinality-ultimate* - [cairo](https://www.archlinux.org/packages/?name=cairo) собранный с дополнительными и Ubuntu-патчами.

Все библиотеки собраны в чистом окружении среды Chroot, и доступны для обеих архитектур i686 и x86_64, включена поддержка multilib.

Для удобства пользователей доступен дополнительный репозиторий *infinality-bundle-fonts* предлагающий широкий выбор всех необходимых шрифтов, для создания и воспроизведения гипертекстовых документов. Все шрифты были отобраны и проверены вручную, чтобы гарантировать высокое качество их рендеринга, а также совместимость с проприетарными эквивалентами используемыми в сети и офисных приложениях. Все шрифты находятся в свободном доступе и распространяются по лицензиям GPL, OFL, Apache или подобными, не ограничивающими их использование.

Дополнительные действия после установки не требуется, однако Вы легко сможете настроить сборку под ваши нужды, если потребуется.

#### Установка

Установка состоит из добавления выбранных репозиториев в `pacman.conf` и [установки](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакетов из соответствующих групп или мета-пакетов. Не забудьте перезапустить сервер X после установки, чтобы увидеть изменения.

*   [infinality-bundle](/index.php/Unofficial_user_repositories#infinality-bundle "Unofficial user repositories") содержит базовые пакеты собранные в группе *infinality-bundle*.
*   [infinality-bundle-multilib](/index.php/Unofficial_user_repositories#infinality-bundle-multilib "Unofficial user repositories") репозиторий содержит дополнительные мультибиблиотечные библиотеки для архитектуры x86_64 собранные в группе *infinality-bundle-multilib*.
*   [infinality-bundle-fonts](/index.php/Unofficial_user_repositories#infinality-bundle-fonts "Unofficial user repositories") репозиторий содержит полную коллекцию бесплатных шрифтов в метапакетах *ibfonts-meta-base*, *ibfonts-meta-extended* и *ibfonts-meta-extended-lt*.

**Примечание:**

*   Не забудьте добавить ключ ID 962DDE58 в ваш pacman keyring. Для подробных инструкций как это сделать,смотрите [Добавление неофициальных ключей](/index.php/Pacman-key_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BE.D1.84.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D1.85_.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.B9 "Pacman-key (Русский)").
*   Когда pacman разрешает зависимости и получает конфликтующий пакет, например:
    ```
    resolving dependencies...
    looking for inter-conflicts...
    :: freetype2-infinality-ultimate and freetype2 are in conflict. Remove freetype2? [y/N]

    ```
    отвечайте `yes`.

#### Рекомендуемые шрифты с ограниченными лицензиями

Ниже приведен список шрифтов, которые распространяются по несвободным лицензиям и не могут быть включены в состав *infinality-bundle-fonts* как бинарные пакеты. Однако, вы можете установить их и использовать соблюдая некоторые условия, часть из них (исходные пакеты) можно найти в репозитории [AUR](/index.php/AUR "AUR"). Пожалуйста ознакомьтесь с лицензионным соглашением, прежде чем использовать шрифты!

*   [ttf-brill](https://aur.archlinux.org/packages/ttf-brill/)
*   [otf-neris](https://aur.archlinux.org/packages/otf-neris/)
*   [ttf-aller](https://aur.archlinux.org/packages/ttf-aller/)
*   [ttf-envy-code-r](https://aur.archlinux.org/packages/ttf-envy-code-r/)

#### Использование

Пользователи популярных окружений рабочего стола (GNOME, KDE, Xfce4, Cinnamon, LXDE) должны настроить параметры шрифта через их панели управления DE. В принципе, настройки должны дублировать те, что в файле настроек freetype2 (`/etc/X11/xinit/xinitrc.d/xft-settings.sh`):

```
Xft.antialias: 1
Xft.autohint: 0
Xft.dpi: 96
Xft.hinting: 1
Xft.hintstyle: hintfull
Xft.lcdfilter: lcddefault
Xft.rgba: rgb

```

Если панель управления вашего DE не позволяет установить любой из выше указанных пунктов, отрегулируйте только те, которые доступны. Помимо этих значений, можно настроить все переменные `INFINALITY_FT`. Пример:

```
# Делает шрифты темнее и толще при отрицательном значении. При положительном осветляет.
export INFINALITY_FT_BRIGHTNESS="-10"

# Не слишком острый, не слишком гладкий
export INFINALITY_FT_FILTER_PARAMS="16 20 28 20 16"

```

**Примечание:** Ваши настройки будут сохранены в файл`.pacsave` при обнавлении пакета infinality.

*   Можно пропустить установку *infinality-bundle-fonts* если вы хотите использовать пропиетарную коллекцию шрифтов Microsoft. Если это так, то вы должны активировать предустановки Fontconfig MS для обеспечения правильного выбора набора шрифтов. Сделайте это:

 `# fc-presets set` 
```
1) combi
2) free
3) ms
4) reset
5) quit
Enter your choice...

```

и выберите `3`.

Для большей информации, запустите `fc-presets help`.

*   Если вы предпочитаете использовать пользовательский набор шрифтов, есть предустановки `combi` которые позволяют регулировать соответствующие параметры fontconfig. При активации предустановки `combi`, содержание файла настроек (`/etc/fonts/conf.avail.infinality/combi`) может быть свободно изменено. Когда вы закончите, не забудьте создать резервную копию каталога 'combi'.

#### Больше шрифтов

Если вы хотите установить еще больше шрифтов, есть дополнительная коллекция *infinality-bundle-fonts-extra*. Выполните

```
$ pacman -Ss infinality-bundle-fonts-extra

```

чтобы получить список доступных пакетов.

**Совет:** Перед установкой любого стороннего шрифта либо из [официальных репозиториев](/index.php/Official_repositories "Official repositories") или [AUR](/index.php/AUR "AUR"), всегда проверяйте доступен ли он в коллекции *infinality-bundle-fonts*

**Важно:** **Не** пытайтесь установить все группы *infinality-bundle-fonts* или *infinality-bundle-fonts-extra*. Если вы не знаете наверняка, какие нужны шрифты из доступных там, вы только излишне загромоздите свой жесткий диск и снизите производительность кэша шрифтов. *ibfonts-meta-extended* должно хватить в большинстве, даже очень сложных случаях использования. Кроме того, несколько семейств шрифтов доступны в нескольких форматах (T1, TTF, OTF): попытка установить все пакеты шрифтов приведет к неразрешимым конфликтам пакетов. Если это так, то вы всегда должны использовать только **один** формат на семью

#### Замены шрифта

Если Вы хотите перезаписать набор замены стандартных шрифтов в `/etc/fonts/conf.d/37-repl-global-*preset*.conf` или добавить новые, используйте `/etc/fonts/conf.d/35-repl-custom.conf`. Вам понадобится продублировать шаблон (16 строк кода) для каждого семейства шрифтов, которые хотите заменить и подставить соответсвующие названия.

#### Подписи пакетов

Бывает пользователи сталкиваются с тем, что подпись не соответствует репозиторию. Частое обновление списка пакетов (`pacman -Syy`), решит проблему. Если не получается, удалите файлы infinality-bundle files из `/var/lib/pacman/sync` и снова обновите список пакетов.

**Примечание:** Можно отказаться от проверки подписи *SigLevel = Never* для каждого репозитория Infinality в вашем */etc/pacman.conf*. Например:
```
[infinality-bundle]
Server = [http://bohoomil.com/repo/$arch](http://bohoomil.com/repo/$arch)
SigLevel = Never

```

#### Обновление

*fontconfig-infinality-ultimate* часто обновляется, обычно каждые 3-4 недели, после ряда сообщений об незначительных ошибках, которые были исправлены. Каждое исправление появляется сразу в репозитории GitHub, и пользователи выбравшие [fontconfig-infinality-ultimate-git](https://aur.archlinux.org/packages/fontconfig-infinality-ultimate-git/) из AUR получат их раньше, т.е. когда пересоберут пакет.

**Примечание:**

*   *fontconfig-infinality-ultimate-git* пакет разработки доступен в репозитории [infinality-bundle]. Имейте в виду, что это не стабильный релиз, и может что-нибудь нарушить.
*   When **reporting bugs**, please report all code-related issues (incorrect rendering, fontconfig problems, etc.) at GitHub [Issues * bohoomil/fontconfig-ultimate](https://github.com/bohoomil/fontconfig-ultimate/issues) and Arch specific, including problems regarding maintenance, packaging and general questions, in dedicated threads at Arch Forums. Before filing a report, make sure that [infinality-bundle] packages were correctly installed and customized.

### Апстрим infinality

**Важно:** Infinality патчи предназначены для версии старше 2.4x freetype2\. Пользователям рекомендуется использовать [infinality-bundle](#Infinality-bundle) поддерживаемый *bohoomil*.

[freetype2-infinality](https://aur.archlinux.org/packages/freetype2-infinality/) Может быть установлен из [AUR](/index.php/AUR "AUR"). Если вы пользователь multilib, также установите [lib32-freetype2-infinality](https://aur.archlinux.org/packages/lib32-freetype2-infinality/) из AUR. AUR также содержит последний снимок разработки патча Infinality с freetype2 : [freetype2-infinality-git](https://aur.archlinux.org/packages/freetype2-infinality-git/) и [lib32-freetype2-infinality-git](https://aur.archlinux.org/packages/lib32-freetype2-infinality-git/).

Рекомендуется также установить [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/) для включения выбора готовых стилей замещения шрифта и настройки сглаживания, кроме настроек рендеринга самого движка. После этого, вы можете выбрать стиль шрифта (win7, winxp, osx, linux, ...) с помощью:

```
# fc-presets set

```

Соответствующие шрифты должны быть установлены.

**Примечание:**

*   Установите [grip-git](https://aur.archlinux.org/packages/grip-git/) из AUR, чтобы иметь предварительный просмотр шрифта в реальном времени.
*   `README` для [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/) говорит, что `/etc/fonts/local.conf` должен быть, либо не существует, или не имеет связанных настроек с infinality. `local.conf` является устаревшим и полностью заменен этой конфигурацией.

Для большей информации, смотрите пост на форуме: [http://www.infinality.net/forum/viewtopic.php?f=2&t=77#p794](http://www.infinality.net/forum/viewtopic.php?f=2&t=77#p794)

## Решение проблем

Смотрите также [Font configuration#Troubleshooting](/index.php/Font_configuration#Troubleshooting "Font configuration").

### Spotify проблемы шрифта

Если у вас проблемы рендеринга шрифтов с Spotify [[1](http://i.imgur.com/E51vt2b.jpg)], попробуйте следующие настройки шрифта:

```
USE_STYLE="2"
export INFINALITY_FT_FRINGE_FILTER_STRENGTH="50"
export INFINALITY_FT_USE_VARIOUS_TWEAKS="true"
export INFINALITY_FT_CHROMEOS_STYLE_SHARPENING_STRENGTH="20"
export INFINALITY_FT_GAMMA_CORRECTION="30 80"
export INFINALITY_FT_STEM_ALIGNMENT_STRENGTH="25"
export INFINALITY_FT_STEM_FITTING_STRENGTH="25"

```

### Google Chrome проблемы

Чтобы исправить проблемы с отображением в браузере Google Chrome описанные [в этом сообщении](https://bbs.archlinux.org/viewtopic.php?pid=1344172#p1344172), отредактируйте файл `/etc/fonts/fonts.conf` убрав знаки комментирования (удалите "!--" и "--"):

```
<!--match target="pattern">
<edit name="dpi" mode="assign">
<double>72</double>
</edit>
</match-->
```

### Emacs

Emacs users have reported issues with Noto Sans as the default sans-serif font. This will affect any font face that specifies "Sans Serif" as the font family including the variable-pitch face that is used in Emacs Info mode.

Noto Sans is a collection of many individual language specific font files. Emacs does not find the correct version when it tries to render the font and displays glyphs instead.

To get around the issue you need to either specify a different default Sans Serif font for all applications or modify the font family for any faces that specify "Sans Serif" within Emacs.

To change the default font for all applications place the following:

```
  <alias>
    <family>sans-serif</family>
    <prefer>
      <family>Liberation Sans</family>
    </prefer>
  </alias>

```

in either `/etc/fonts/conf.avail.infinality/35-repl-custom.conf` for global effect or `$XDG_CONFIG_HOME/fontconfig/fonts.conf` or `$XDG_CONFIG_HOME/fontconfig/conf.d/60-latin.conf` for a single user. For `combi` users, `60-latin-combi.conf` should be modified accordingly.

The default font can be any but Noto Sans.

To change the font in Emacs only:

If you prefer Noto Sans for other applications and just want to fix Emacs specifically then you can specify a new Font Family for the variable pitch face. This could be done via customize (M-x customize-face RET variable-pitch RET) or by placing the following code in `$HOME/.emacs` or `$HOME/emacs.d/init.el`.

```
(custom-set-faces
  '(variable-pitch ((t (:family "Liberation Sans")))))

```

Note that there may be other faces either in default Emacs or specified by themes that also use the default Sans Serif font and would have to be modified in the same way. Changing the system wide default to something like Liberation Sans is therefore a more universal fix.

### GIMP

Пользователи GIMP сообщили о проблемах с субпиксельным рендерингом текста в изображениях (смотрите для примера [эту тему](http://www.infinality.net/forum/viewtopic.php?f=2&t=229)). Лучший путь решения, - отключить субпиксельный рендеринг полностью в GIMP. Добавьте файл `/etc/gimp/2.0/fonts.conf` (или `~/.gimp-2.8/fonts.conf` для одного пользователя) со следующим содержанием:

 `/etc/gimp/2.0/fonts.conf` 
```
<fontconfig>
  <match target="font">
    <edit name="rgba" mode="assign">
      <const>none</const>
    </edit>
  </match>
</fontconfig>

```

### Неправильно отображаются специальные языковые символы / глифы

Неправильно отображаются специальные языковые символы при использовании стандартного шрифта.

Это обычно происходит с веб-сайтами (особенно блогами), использующими шаблоны CSS, которые используют веб-шрифты с отсутствием поддержки для расширенных латинских символов. Хотя это не является следствием использования этой сборки и должно исправляться администратором сайта. Эту проблему можно обойти созданием правила замены шрифтов в fontconfig'е. Если хотите использовать эту возможность, сперва активируйте замены `36-repl-missing-glyphs.conf`:

```
$ cd /etc/fonts/conf.d
$ ln -s ../conf.avail.infinality/36-repl-missing-glyphs.conf .

```

после чего отредактируйте файл согласно приведенному примеру.

**Примечание:** Шрифты, используемые по умолчанию для нелатинских сценариев указаны в `65-non-latin-*preset*.conf`(настройки по умолчанию).

Перезапись стандартных правил замен и добавление своих возможно с `35-repl-custom.conf`. Этот файл используется по умолчанию, так что все что потребуется это его редактирование.

### Браузеры Firefox/Chrome рендерят моноширный шрифт как пропорциональный

Вы можете проверить, какие шрифты использует браузер, выполнив `fc-match`. Если для `"monospace"` вы получаете пропорциональный шрифт Arial

```
# fc-match "monospace"
monospace: arial.ttf: "Arial" "Normal"

```

вам нужно запустить

```
 # fc-presets set

```

### Общие проблемы со шрифтами

Если Вы натолкнетесь на проблемы со шрифтами (например, какие-то глифы не отображаются в документах PDF, хотя семейство шрифтов было корректно установлено), начните поиск неисправностей выполнив команду:

```
# fc-cache -fr

```

Это полностью очистит кэш шрифтов и создаст его заново.

## Смотрите также

*   [Файл *infinality-settings.sh* с примерами и описанием (Англ.)](https://github.com/bohoomil/fontconfig-ultimate/blob/master/freetype/generic_settings/infinality-settings.sh)
*   [Домашняя страница (Англ.)](http://www.infinality.net/blog/infinality-freetype-patches/)
*   [Форум (Англ.)](http://www.infinality.net/forum/)
*   [Короткая статья о infinality (содержит скриншоты, Англ.)](http://www.webupd8.org/2013/06/better-font-rendering-in-linux-with.html)
*   [Infinality bundle и шрифты](http://bohoomil.com) - домашняя страничка сборки.
*   [fontconfig-ultimate](https://github.com/bohoomil/fontconfig-ultimate) - git-репозиторий, содержащий патчи, настройки и сборочные сценарии для всей коллекции *infinality-bundle+fonts* в отдельных бранчах.
*   [infinality-bundle: good looking fonts made (even) easier](https://bbs.archlinux.org/viewtopic.php?id=162098) - *infinality-bundle* support thread in the Arch Linux Forums
*   [infinality-bundle-fonts: a free multilingual font collection for Arch](https://bbs.archlinux.org/viewtopic.php?id=170976) - *infinality-bundle-fonts* support thread in the Arch Linux Forums