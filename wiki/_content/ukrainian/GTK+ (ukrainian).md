Related articles

*   [Однаковий вигляд для QT та GTK застосунків](/index.php/Uniform_look_for_Qt_and_GTK_applications_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0) "Uniform look for Qt and GTK applications (Українська)")

GTK+, GIMP Toolkit, спочатку був зроблений для [GIMP](/index.php/GIMP "GIMP") але тепер дуже популярний інструментарій прив’язаний до багатьох мов.

## Contents

*   [1 Теми](#.D0.A2.D0.B5.D0.BC.D0.B8)
    *   [1.1 GTK+ 1.x](#GTK.2B_1.x)
    *   [1.2 GTK+ 2.x](#GTK.2B_2.x)
    *   [1.3 GTK+ та QT](#GTK.2B_.D1.82.D0.B0_QT)
*   [2 Налаштування](#.D0.9D.D0.B0.D0.BB.D0.B0.D1.88.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F)
    *   [2.1 Увімкнення налаштовуваних клавіш швидкого доступу](#.D0.A3.D0.B2.D1.96.D0.BC.D0.BA.D0.BD.D0.B5.D0.BD.D0.BD.D1.8F_.D0.BD.D0.B0.D0.BB.D0.B0.D1.88.D1.82.D0.BE.D0.B2.D1.83.D0.B2.D0.B0.D0.BD.D0.B8.D1.85_.D0.BA.D0.BB.D0.B0.D0.B2.D1.96.D1.88_.D1.88.D0.B2.D0.B8.D0.B4.D0.BA.D0.BE.D0.B3.D0.BE_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D1.83)
    *   [2.2 Прискорення меню GNOME](#.D0.9F.D1.80.D0.B8.D1.81.D0.BA.D0.BE.D1.80.D0.B5.D0.BD.D0.BD.D1.8F_.D0.BC.D0.B5.D0.BD.D1.8E_GNOME)
*   [3 Компіляція GTK+ програм](#.D0.9A.D0.BE.D0.BC.D0.BF.D1.96.D0.BB.D1.8F.D1.86.D1.96.D1.8F_GTK.2B_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC)
*   [4 Ресурси](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D0.B8)

## Теми

### GTK+ 1.x

Старі GTK+ 1 додатки (як xmms) спочатку не виглядяли дуже гарно. Це тому, що вони використовували бридкі теми за замовчуванням. Щоб їх змінити, вам потрібно:

1.  завантажити та встановити якусь гарну тему
2.  змінити тему

Деякі красиві теми є в [extra]. Щоб їх встановити:

```
# pacman -S gtk-smooth-engine

```

Щоб змінити тему можете використати gtk-theme-switch:

```
# pacman -S gtk-theme-switch

```

Запустіть його з командою 'switch'.

### GTK+ 2.x

Основні [Desktop environments](/index.php/Desktop_environment "Desktop environment") надають інструменти для налаштування GTK+ тем, значків, шрифтів та розмірів шрифту. Крім того, є інструменти такі як [lxappearance](https://www.archlinux.org/packages/?name=lxappearance), [gtk-chtheme](https://www.archlinux.org/packages/?name=gtk-chtheme), [gtk-theme-switch2](https://www.archlinux.org/packages/?name=gtk-theme-switch2) та [gtk2_prefs](https://www.archlinux.org/packages/?name=gtk2_prefs), що можуть бути використаними. [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) є DE незалежним інструментом налаштування з проекту LXDE, що не потребує інших частин LXDE. Встановіть один з наступних пакунків:

```
# pacman -S lxappearance

# pacman -S gtk-chtheme

# pacman -S gtk-theme-switch2

# pacman -S gtk2_prefs

```

Деякі теми GTK+ 2 рекомендовані до встановлення. Поширена тема *Clearlooks* входить до пакунку [gtk-engines](https://www.archlinux.org/packages/?name=gtk-engines):

```
# pacman -S gtk-engines

```

Інші теми знаходяться в [AUR](/index.php/AUR "AUR"):

*   [https://aur.archlinux.org/packages.php?O=0&K=gtk2-theme&do_Search=Go](https://aur.archlinux.org/packages.php?O=0&K=gtk2-theme&do_Search=Go)
*   [https://aur.archlinux.org/packages.php?O=0&K=gtk-theme&do_Search=Go](https://aur.archlinux.org/packages.php?O=0&K=gtk-theme&do_Search=Go)

Інакше GTK+ налаштунки можуть бути змінені шляхом редагування файлу `~/.gtkrc-2.0`. Список налаштувань GTK+ можна знайти в [бібліотеці GNOME](http://library.gnome.org/devel/gtk/stable/GtkSettings.html). Щоб вручну змінити GTK+ тему, значки, шрифти та їх розміри - додайте наступне до `~/.gtkrc-2.0`:

 `~/.gtkrc-2.0` 
```
gtk-icon-theme-name = "[ім’я-теми-значків]"
gtk-theme-name = "[ім’я-теми]"
gtk-font-name = "[ім’я-шрифту] [розмір]"
```

Наприклад:

 `~/.gtkrc-2.0` 
```
gtk-icon-theme-name = "Tango"
gtk-theme-name = "Murrine-Gray"
gtk-font-name = "DejaVu Sans 8"
```

**Note:** Приклад віще потребує пакунки [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu), [tango-icon-theme](https://aur.archlinux.org/packages/tango-icon-theme/), [gtk-engine-murrine](https://www.archlinux.org/packages/?name=gtk-engine-murrine) та [murrine-themes-collection](https://www.archlinux.org/packages/?name=murrine-themes-collection).

### GTK+ та QT

Якщо на робочому столі встановлено GTK+ та QT (KDE) додатки то помітно, що їхня зовнішність відрізняється. Якщо ви хочете зробити стилі GTK+ відповідними до QT будьласка прочитайте [Однаковий вигляд для QT та GTK застосунків](/index.php/Uniform_look_for_Qt_and_GTK_applications_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0) "Uniform look for Qt and GTK applications (Українська)").

## Налаштування

**Note:** Дивись [бібліотеку GNOME](http://library.gnome.org/devel/gtk/stable/GtkSettings.html) з повним списком параметрів конфігурації GTK.

Мета цього розділу полягає в зборі параметрів конфігурації GTK котрий може бути використаним наприклад в `~/.gtkrc-2.0`.

### Увімкнення налаштовуваних клавіш швидкого доступу

Налаштування клавіш швидкого доступу в GTK додатках (котрі називаються ще *прискорювачі* в GTK термінології) можна зробити за допомогою миші, навівши її над пунктом меню і натиснувши бажану комбінацію клавіш. Однак, ця функція вимкнена за замовчуванням. Щоб її увімкнути, встановіть

```
gtk-can-change-accels = 1

```

### Прискорення меню GNOME

Це налаштування відповідає за затримку між наведенням курсору миші на меню і його відкриття в GNOME. Змініть цей параметр на відповідний. Число в мілісекундах, наприклад, 250 буде чверть секунди.

```
gtk-menu-popup-delay = 0

```

## Компіляція GTK+ програм

Якщо GTK+ програми пишуться на C з нуля, необхідно додати CFLAGS для gcc (код був запозичений з Ubuntu форуму):

```
gcc -g -Wall `pkg-config --cflags --libs gtk+-2.0` -o base base.c

```

-g та -Wall параметри вже не є необхідними так як вони призначені тільки для більш детального налагоджувального виводу. Ви можете спробувати офіційний [Hello World приклад](http://library.gnome.org/devel/gtk-tutorial/stable/c39.html#SEC-HELLOWORLD) наданий gtk.org.

## Ресурси

*   [Офіційний GTK+ вебсайт (Англійська)](http://www.gtk.org/)
*   [Підручник для GTK+ 2 (Англійська)](http://library.gnome.org/devel/gtk-tutorial/stable/)
*   [Стаття в Вікіпедії про GTK+ (Англійська)](https://en.wikipedia.org/wiki/GTK%2B "wikipedia:GTK+")