# KDE Packages (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

С выхода KDE SC 4.3, для каждого приложения существуют отдельные пакеты. В этой статье описываются понятия групп и мета-пакетов.

## Contents

*   [1 Терминология](#.D0.A2.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.BE.D0.BB.D0.BE.D0.B3.D0.B8.D1.8F)
*   [2 Использование групп пакетов](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B3.D1.80.D1.83.D0.BF.D0.BF_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [2.1 Зачем использовать группы?](#.D0.97.D0.B0.D1.87.D0.B5.D0.BC_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D1.8C_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D1.8B.3F)
        *   [2.1.1 Достоинства](#.D0.94.D0.BE.D1.81.D1.82.D0.BE.D0.B8.D0.BD.D1.81.D1.82.D0.B2.D0.B0)
        *   [2.1.2 Недостатки](#.D0.9D.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D0.B0.D1.82.D0.BA.D0.B8)
    *   [2.2 Для кого это?](#.D0.94.D0.BB.D1.8F_.D0.BA.D0.BE.D0.B3.D0.BE_.D1.8D.D1.82.D0.BE.3F)
*   [3 Using Meta-Packages](#Using_Meta-Packages)
    *   [3.1 Why use meta-packages?](#Why_use_meta-packages.3F)
        *   [3.1.1 Advantages](#Advantages)
        *   [3.1.2 Disadvantages](#Disadvantages)
    *   [3.2 Who is it for?](#Who_is_it_for.3F)
*   [4 Listing the member packages](#Listing_the_member_packages)

## Терминология

**Модуль (module)**

Исходный код KDE организован в несколько категорий, которые называются модулями. Например, kdebase, kdeutils и т.п. KDE выпускают один архив исходных кодов на каждый модуль. Подробно можно узнать здесь [Coordinator List](http://techbase.kde.org/Projects/Release_Team#Coordinator_List).

**Группа пакетов (package group)**

Группа пакетов - это группа пакетов :). [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") даёт возможность выбирать множество пакетов для установки или удаления с помощью групп.

**Мета-пакет (meta-package)**

Мета-пакет - это пустой пакет, который просто объединяет несколько пакетов с помощью зависимостей.

## Использование групп пакетов

Имеются группы для каждого модуля KDE, такие как **kdebase**, **kdeutils** и т.п. Установка группы пакетов установит все пакеты, принадлежащие группе на момент установки. К примеру, чтобы установить все пакеты, которые являются частью модуля **kdebase** или **kdeutils**, выполните:

```
# pacman -S kdebase kdeutils ...

```

Также существует группа **kde**, которая включает в себя все остальные. Установка данной группы поставит вам текущую версию KDE полностью:

```
# pacman -S kde

```

### Зачем использовать группы?

#### Достоинства

*   Использование групп позволяет легко устанавливать или удалять множество пакетов сразу. Одной командой можно установить все пакеты из модуля. Using groups makes it easier to install or remove a set of packages. This allows you to use a single command (like above) to install or remove all packages in a module.
*   Между группой и пакетами не существует жёсткой зависимости (hard dependency), т.е. не обязательно устанавливать все пакеты из группы, можно спокойно их удалять, не затрагивая остальные пакеты данного набора. There is no hard dependency between a group and its packages. This means that there is no reason to have all member packages in a group installed. You may freely remove member packages that belong to a group without touching other member packages of the same group.

#### Недостатки

*   [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") не установит пакеты, которые могут быть добавлены в группу после того, как вы её установите. Например, если в следующем релизе KDE SC изменится состав групп, новые пакеты из них не будут установлены, когда вы обновите систему и вам придётся устанавливать их вручную. Чтобы избежать этого, используйте мета-пакеты (следующий раздел). will not install any new packages that may be added to a group at a later date. For instance, if the next release of the KDE software compilation includes new applications in one of more modules, these new applications will not be automatically installed when you upgrade your system. You will have to manually install these new packages. To overcome this, use meta-packages (see next section).

### Для кого это?

Устанавливайте группы если вам нужны только некоторые модули KDE SC или вы выбрать только определённые пакеты, тогда вы можете удалить остальные. ТакInstall package groups if you only want some modules of the current KDE software compilation release. Groups are also useful for those users who only want to retain some packages from a group, while opting to remove the others.

## Using Meta-Packages

Just like groups, there are meta-packages for each KDE module, such as **kde-meta-kdebase**, **kde-meta-kdeutils** etc. Installing these meta-packages will install or upgrade all packages that belong to the module. If new applications are added to the module in a future release, they will automatically be installed when you upgrade your system. To install a specific module such as **kdebase** or **kdeutils** using meta-packages, use:

```
# pacman -S kde-meta-kdebase kde-meta-kdeutils ...

```

In addition to this, there is a **kde-meta** group that includes all these meta-packages. Installing the **kde-meta** group will install the entire KDE software compilation:

```
# pacman -S kde-meta

```

### Why use meta-packages?

#### Advantages

*   Like package groups, meta-packages make it easy to install and maintain a set of packages. This allows you to use a single command (like above) to install all packages in a module.
*   Use of meta-packages ensures that [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") will install any new member packages automatically when you upgrade your system. This emulates the behavior of the monolithic set of packages that were used before KDE SC 4.3.

#### Disadvantages

*   Meta-packages have a hard dependency on all the member packages that are part of it. This means that you cannot freely remove member packages that are part of a meta-package without removing the meta-package first. For example, if you installed **kde-meta-kdebase** and would now like to remove a member package such as, **kdebase-kwrite**, you will first need to remove the meta-package before removing the member package:

```
# pacman -R kde-meta-kdebase
# pacman -R kdebase-kwrite

```

Doing this will not remove other member packages in the **kde-meta-kdebase** meta-package, but it will also no longer automatically add new packages in that module (possibly from the next release) when you upgrade the system using pacman -Syu. You may re-install **kde-meta-kdebase** meta-package at any time to return to the monolithic package behavior.

If you installed the kde-meta package, you can remove all meta-packages at once by using:

```
# pacman -R kde-meta

```

This will only remove the meta-packages and not the actual member packages.

### Who is it for?

Use meta-packages if you desire to install the entire KDE software compilation or one or more of its modules in its entirety. This ensures a smooth upgrade path by automatically adding new split packages from subsequent releases.

## Listing the member packages

To get a complete list of KDE applications use

```
pacman -Sg kde

```

Get a list of all meta packages:

```
pacman -Sg kde-meta

```

Get a list of all KDE module groups:

```
for i in $(pacman -Sqg kde-meta); do echo ${i#kde-meta-};done

```

Get a list of all KDE packages and their module group:

```
for i in $(pacman -Sqg kde-meta); do pacman -Sg ${i#kde-meta-};done

```

You could also use the web interface at [archlinux.de](https://www.archlinux.de/?page=Packages;group=5) to browse package groups.

Retrieved from "[https://wiki.archlinux.org/index.php?title=KDE_Packages_(Русский)&oldid=414488](https://wiki.archlinux.org/index.php?title=KDE_Packages_(Русский)&oldid=414488)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Arch development (Русский)](/index.php/Category:Arch_development_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Arch development (Русский)")
*   [Desktop environments (Русский)](/index.php/Category:Desktop_environments_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Desktop environments (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")