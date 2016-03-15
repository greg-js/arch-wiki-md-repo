## Contents

*   [1 Вступление](#.D0.92.D1.81.D1.82.D1.83.D0.BF.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [4 Темы](#.D0.A2.D0.B5.D0.BC.D1.8B)
*   [5 Создание собственных тем](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.BE.D0.B1.D1.81.D1.82.D0.B2.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D1.82.D0.B5.D0.BC)
*   [6 kdmrc](#kdmrc)
    *   [6.1 SessionsDirs](#SessionsDirs)
    *   [6.2 Перезапуск X сервера](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_X_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)

## Вступление

KDM (KDE Display Manager) это менеджер входа в систему для KDE. Он поддерживает различные темы оформления, автовход, выбор графического окружения для входа и т.д.

## Установка

*Смотрите [Display Manager (Русский)](/index.php/Display_Manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display Manager (Русский)").*

## Настройка

KDM можно настроить из программы ПАРАМЕТРЫ СИСТЕМЫ, запустив ее с привилегиями root:

*   в KDEMod программа автоматически запросит пароль
*   в KDE можно использовать kdesu:

```
$ `kdesu systemsettings`

```

## Темы

Темы оформления для Archlinux KDM можно установить так:

```
# pacman -S archlinux-themes-kdm

```

Огромное количество тем для KDM4 лежит здесь [http://kde-look.org/index.php?xcontentmode=41](http://kde-look.org/index.php?xcontentmode=41).

**Примечание:** Для установки тем оформления необходимо запускать ПАРАМЕТРЫ СИСТЕМЫ с привилегиями root.

## Создание собственных тем

Все шаблоны лежат в `/usr/share/apps/kdm/themes`.

Они имеют такой-же формат как и темы для GDM, документацию для которого можно найти здесь: [Detailed Description of Theme XML format](http://projects.gnome.org//gdm/docs/2.18/thememanual.html#descofthemeformat).

## kdmrc

Настройки KDM хранятся здесь `/usr/share/config/kdm/kdmrc`. Изначально этот файл содержит подробные комментарии о каждом пункте настроек.

### SessionsDirs

Эта переменная содержит список директорий, в которых находятся файлы сессий в формате `.desktop`, в порядке уменьшения приоритета. В Arch Linux некоторые [оконные менеджеры](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)") устанавливают свои файлы в `/etc/X11/sessions` или `/usr/share/xsessions`. Добавьте эти директории в `/usr/share/config/kdm/kdmrc` чтобы иметь возможность запускать их из KDM.

```
SessionsDirs=/usr/share/apps/kdm/sessions,/usr/share/config/kdm/sessions,/usr/share/apps/kdm/sessions,/etc/X11/sessions,/usr/share/xsessions

```

### Перезапуск X сервера

Чтобы разрешить пользователям перезапускать X сервер из KDM, отредактируйте kdmrc:

```
 [X-:*-Greeter]
 # [...]
 # Show the "Restart X Server"/"Close Connection" action in the greeter.
 # Default is true
 AllowClose=true

```

Эта настройка добавит в меню KDM пункт перезапуска X сервера. Так-же перезапуск можно вызвать сочетанием клавиш Alt-E.