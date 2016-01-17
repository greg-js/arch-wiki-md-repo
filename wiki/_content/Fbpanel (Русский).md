# Fbpanel (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

Fbpanel - лёгковесная, гибко настраиваемая панель для рабочего стола.  
Страницы проекта:  
[GitHub](https://github.com/aanatoly/fbpanel)  
[SourceForge](http://fbpanel.sourceforge.net/)

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 wincmd plugin](#wincmd_plugin)
*   [3 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)

## Установка

Установите [fbpanel](https://www.archlinux.org/packages/?name=fbpanel).

## Настройка

Выполните от пользователя:

```
$fbpanel

```

Возможно, что [fbpanel](https://www.archlinux.org/packages/?name=fbpanel) выдаст ошибку, ссылаясь на невозможность открытия `/home/user/.config/fbpanel/default`  
Ничего страшного здесь нет, достаточно создать дефолтный файл конфигурации:

```
$mkdir ~/.config/fbpanel
$cp /usr/share/fbpanel/default ~/.config/fbpanel

```

### wincmd plugin

Плагин по умолчанию включён, но может не корректно отображать значки, которые не сможет найти. В этом случае укажите путь к иконкам:

```
Plugin {
  type = wincmd
  config {
      image = ~/images/my_image.png
      tooltip = Left click to iconify all windows. Middle click to shade them.
  }
}

```

**Совет:** Вы можете использовать изображения в качестве значков.

`/usr/share/fbpanel/images/` в таком случае необходимо скопировать в домашнюю директорию пользователя:

```
$mkdir ~/images
$cp -R /usr/share/fbpanel/images/ ~/images 

```

## Решение проблем

В случае получения следующего сообщения при запуске:

```
volume: can't open /dev/mixer
fbpanel: cant't start plugin volume

```

Закоментируйте следующие строки в файле конфигурации:

```
Plugin {
   type = volume
}

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Fbpanel_(Русский)&oldid=415778](https://wiki.archlinux.org/index.php?title=Fbpanel_(Русский)&oldid=415778)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Application launchers (Русский)](/index.php/Category:Application_launchers_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Application launchers (Русский)")
*   [Eye candy (Русский)](/index.php/Category:Eye_candy_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Eye candy (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")
*   [Status monitoring and notification (Русский)](/index.php/Category:Status_monitoring_and_notification_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Status monitoring and notification (Русский)")