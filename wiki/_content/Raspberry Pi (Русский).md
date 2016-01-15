# Raspberry Pi (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

Raspberry Pi - минималистичный компьютер построенный на архитектуре ARMv6.

**Обратите внимание:** За поддержкой архитектуры ARM обращаться сюда [http://archlinuxarm.org/](http://archlinuxarm.org/)

## Wayland

Wayland - новый оконный протокол для Линукса. Использование Wayland требует изменения и переустановки части вашего системного программного обеспечения. Дополнительную информацию смотреть на домашней странице [Wayland](http://wayland.freedesktop.org/). Ниже будем рассматривать установку и настройку Wayland на микрокомпьютере Raspberry PI.

## Установка

Установку минимальной конфигурации операционной системы Arch Linux на Raspberry PI смотреть [здесь](http://archlinuxarm.org/platforms/armv6/raspberry-pi#qt-platform_tabs-ui-tabs2). Обязательно обновляем систему

```
$ pacman -Syu 

```

Установка Wayland делаем из extra [wayland](https://www.archlinux.org/packages/?name=wayland)

```
$ pacman -S wayland

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Raspberry_Pi_(Русский)&oldid=415143](https://wiki.archlinux.org/index.php?title=Raspberry_Pi_(Русский)&oldid=415143)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [ARM architecture (Русский)](/index.php/Category:ARM_architecture_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:ARM architecture (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")