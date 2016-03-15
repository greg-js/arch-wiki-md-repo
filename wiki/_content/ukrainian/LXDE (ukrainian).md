LXDE є відкритим середовищем робочого столу, розробленого під ліцензією GPL для Unix та інших POSIX-сумісних платформ, таких як Linux. Ця стаття розповідає про встановлення, конфігурацію та різні помилки.

З [LXDE.org | Легке середовище робочого столу X11 (LXDE)](http://lxde.org/):

	*The "Lightweight X11 Desktop Environment" is an extremely fast-performing and energy-saving desktop environment. Maintained by an international community of developers, it comes with a beautiful interface, multi-language support, standard keyboard short cuts and additional features like tabbed file browsing. LXDE uses less CPU and less RAM than other environments. It is especially designed for cloud computers with low hardware specifications, such as, netbooks, mobile devices (e.g. MIDs) or older computers.*

## Contents

*   [1 Встановлення](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F)
*   [2 Запуск робочого столу](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.80.D0.BE.D0.B1.D0.BE.D1.87.D0.BE.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D1.83)
    *   [2.1 Менеджер сесій](#.D0.9C.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80_.D1.81.D0.B5.D1.81.D1.96.D0.B9)
    *   [2.2 Консоль](#.D0.9A.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C)
*   [3 Рецепти і підказки](#.D0.A0.D0.B5.D1.86.D0.B5.D0.BF.D1.82.D0.B8_.D1.96_.D0.BF.D1.96.D0.B4.D0.BA.D0.B0.D0.B7.D0.BA.D0.B8)
    *   [3.1 Редагування меню програм](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.B3.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D0.BC.D0.B5.D0.BD.D1.8E_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC)
    *   [3.2 Автомонтування](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.BE.D0.BD.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F)
    *   [3.3 Автостарт програм](#.D0.90.D0.B2.D1.82.D0.BE.D1.81.D1.82.D0.B0.D1.80.D1.82_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC)
    *   [3.4 Прив’язки](#.D0.9F.D1.80.D0.B8.D0.B2.E2.80.99.D1.8F.D0.B7.D0.BA.D0.B8)
    *   [3.5 Курсори](#.D0.9A.D1.83.D1.80.D1.81.D0.BE.D1.80.D0.B8)
        *   [3.5.1 Власна тека іконок в $HOME](#.D0.92.D0.BB.D0.B0.D1.81.D0.BD.D0.B0_.D1.82.D0.B5.D0.BA.D0.B0_.D1.96.D0.BA.D0.BE.D0.BD.D0.BE.D0.BA_.D0.B2_.24HOME)
    *   [3.6 Час цифрового годинника](#.D0.A7.D0.B0.D1.81_.D1.86.D0.B8.D1.84.D1.80.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D0.B3.D0.BE.D0.B4.D0.B8.D0.BD.D0.BD.D0.B8.D0.BA.D0.B0)
    *   [3.7 Налаштування шрифтів](#.D0.9D.D0.B0.D0.BB.D0.B0.D1.88.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D1.88.D1.80.D0.B8.D1.84.D1.82.D1.96.D0.B2)
    *   [3.8 Розкладка клавіатури](#.D0.A0.D0.BE.D0.B7.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B0.D0.B2.D1.96.D0.B0.D1.82.D1.83.D1.80.D0.B8)
        *   [3.8.1 Додавання “Переключателя розкладки клавіатури” до панелі](#.D0.94.D0.BE.D0.B4.D0.B0.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.E2.80.9C.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B0.D1.82.D0.B5.D0.BB.D1.8F_.D1.80.D0.BE.D0.B7.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D1.96.D0.B0.D1.82.D1.83.D1.80.D0.B8.E2.80.9D_.D0.B4.D0.BE_.D0.BF.D0.B0.D0.BD.D0.B5.D0.BB.D1.96)
    *   [3.9 Gnome-screensaver в LXDE](#Gnome-screensaver_.D0.B2_LXDE)
    *   [3.10 Іконки lxpanel’і](#.D0.86.D0.BA.D0.BE.D0.BD.D0.BA.D0.B8_lxpanel.E2.80.99.D1.96)
    *   [3.11 LXDM](#LXDM)
        *   [3.11.1 Автовхід](#.D0.90.D0.B2.D1.82.D0.BE.D0.B2.D1.85.D1.96.D0.B4)
    *   [3.12 PCManFM](#PCManFM)
    *   [3.13 Заміна менеджера вікон](#.D0.97.D0.B0.D0.BC.D1.96.D0.BD.D0.B0_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0_.D0.B2.D1.96.D0.BA.D0.BE.D0.BD)
    *   [3.14 Опції засинання і сплячки](#.D0.9E.D0.BF.D1.86.D1.96.D1.97_.D0.B7.D0.B0.D1.81.D0.B8.D0.BD.D0.B0.D0.BD.D0.BD.D1.8F_.D1.96_.D1.81.D0.BF.D0.BB.D1.8F.D1.87.D0.BA.D0.B8)
    *   [3.15 Виключення і перезапуск з LXDE](#.D0.92.D0.B8.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.BD.D1.8F_.D1.96_.D0.BF.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B7_LXDE)
*   [4 Помилки](#.D0.9F.D0.BE.D0.BC.D0.B8.D0.BB.D0.BA.D0.B8)
    *   [4.1 Управління ключами SSH](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D1.96.D0.BD.D0.BD.D1.8F_.D0.BA.D0.BB.D1.8E.D1.87.D0.B0.D0.BC.D0.B8_SSH)
    *   [4.2 GTK+ Warnings with lxsession 0.4.1](#GTK.2B_Warnings_with_lxsession_0.4.1)
    *   [4.3 LXsession Full](#LXsession_Full)
*   [5 Ресурси](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D0.B8)

## Встановлення

LXDE є дуже модулярним, тому Ви можете вибрати будь-які пакунки. До списку необхідних пакунків для встановлення LXDE входять: [lxde-common](https://www.archlinux.org/packages/?name=lxde-common), [lxsession](https://www.archlinux.org/packages/?name=lxsession), [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils), і менеджер вікон.

Ви можете встановити всюо групу LXDE за допомогою команди:

```
# pacman -S lxde

```

Ця команда встановить наступні пакунки:

*   [gpicview](https://www.archlinux.org/packages/?name=gpicview): Легкий переглядач малюнків
*   [lxappearance](https://www.archlinux.org/packages/?name=lxappearance): Утиліта для налаштування тем, іконок і шрифтів для GTK+ програм
*   [lxde-common](https://www.archlinux.org/packages/?name=lxde-common): Налаштування по замовчуванню для інтегрування різних компонент LXDE
*   [lxde-icon-theme](https://www.archlinux.org/packages/?name=lxde-icon-theme): Тема іконок для LXDE
*   [lxlauncher](https://www.archlinux.org/packages/?name=lxlauncher): Пускач програм для програм, в основному для нетбуків
*   [lxmenu-data](https://www.archlinux.org/packages/?name=lxmenu-data): Збірка файлів, що адаптують специфікацію меню freedesktop.org
*   [lxpanel](https://www.archlinux.org/packages/?name=lxpanel): Панель робочого столу для LXDE
*   [lxrandr](https://www.archlinux.org/packages/?name=lxrandr): Віконний менеджер
*   [lxtask](https://www.archlinux.org/packages/?name=lxtask): Легкий менеджер завдань
*   [lxterminal](https://www.archlinux.org/packages/?name=lxterminal): Легкий емулятор терміналу
*   [menu-cache](https://www.archlinux.org/packages/?name=menu-cache): Демон, що автоматично генерує меню для LXDE
*   [openbox](https://www.archlinux.org/packages/?name=openbox): Легкий стандартний, з широким спектром налаштувань, віконний менеджер, що типово використовується з LXDE
*   [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm): Стандартний менеджер файлів для LXDE, який також виконує функцію інтеграції робочого столу

Після завершення встановлення скопіюйте три файли до ~/.config/openbox , так як в підказці pacman. Покладіть menu.xml, rc.xml і autostart.sh в ~/.config/openbox. Їх можна знайти в /etc/xdg/openbox:

```
cp /etc/xdg/openbox/menu.xml /etc/xdg/openbox/rc.xml /etc/xdg/openbox/autostart.sh ~/.config/openbox

```

Можливо Вам потрібно встановити [Gamin](/index.php/Gamin "Gamin"), знаряддя для моніторингу файлів і тек, як заміну [FAM](/index.php/FAM "FAM"). Він працює разом з програмами і не потребує демону, так як це є у випадку fam. Якщо Ви вже маєте встановлений fam, видаліть його спочатку з стрічки DAEMONS в `/etc/rc.conf` і зупиніть демон, а тоді встановіть gamin:

```
# pacman -S gamin

```

Можливо Ви захочете встановити деякі [легкі аплікації](/index.php/Lightweight_Applications "Lightweight Applications"), що типово використовуються з LXDE:

```
# pacman -S leafpad xarchiver obconf epdfview

```

Врахуйте, що деякі пакунки LXDE є експериментальні і Вам потрібно встановлювати їх зі сховища [AUR](/index.php/AUR "AUR").

## Запуск робочого столу

Є багато способів запустити робочий стіл LXDE.

### Менеджер сесій

Якщо Ви використовуєте [екранний менеджер](/index.php/Display_manager "Display manager") як [GDM](/index.php/GDM "GDM"), [KDM](/index.php/KDM "KDM") або [SLiM](/index.php/SLiM "SLiM"), тоді просто переключіть сесію на LXDE. Перегляньте сторінки вікі цих менеджерів для інструкції.

### Консоль

Існує кілька способів запуску робочого столу з консолі.

Щоб використати **startx**, Вам потрібно визначити LXDE у Вашому файлі `~/.xinitrc`:

```
exec startlxde

```

Щоб запустити LXDE з командної стрічки без `~/.xinitrc`:

```
$ xinit /usr/bin/startlxde

```

Якщо ж `~/.xinitrc` вже існує, то цей спосіб не спрацює.

Якщо Ви бажаєте запустити **startx** автоматично при завантаженні, тоді загляньте до допомоги по [Запуск X при завантаженні](/index.php/Start_X_at_login#Starting_X_as_preferred_user_without_logging_in "Start X at login").

Для інших завдань Вам потрібно впевнитися, що dbus запущений як демон.

## Рецепти і підказки

### Редагування меню програм

Меню програм працює, використовуючи файли `.desktop`, які розміщені в `/usr/share/applications`. Багато середовищ робочих столів запускають програми, що переписують ці настройки і дозволяють редагувати меню. LXDE ще не створило свого редактора меню, однак Ви можете самі вручну підлаштувати його. Можна теж використати редактор меню з AUR - [lxmed](https://aur.archlinux.org/packages/lxmed/)

Щоб додати або налаштувати пункт меню, створіть файл або символьне посилання на файл `.desktop` в `/usr/share/applications`. Прочитайте [специфікацію робочого столу](http://standards.freedesktop.org/desktop-entry-spec/latest/) на freedesktop.org про структуру файлів `.desktop`.

Щоб видалити пункти з меню, замість вилучати файли `.desktop`, можна відредагувати файл і додати наступну стрічку до файлу:

```
NoDisplay=true.

```

Якщо є багато файлів, то можна це автоматизувати за допомогою простих команд:

```
cd /usr/share/applications
for i in program1.desktop program2.desktop ...; do cp /usr/share/applications/$i \
/home/user/.local/share/applications/; echo "NoDisplay=true" >> \
/home/user/.local/share/applications/$i; done

```

Це спрацює для всіх програм за винятком програм з KDE. Для них потрібно залогуватися до самого KDE і з під нього використати редактор меню KDE. Для кожного пункту меню, який Ви не бажаєте бачити, потрібно зазначити опцію 'Show only in KDE'. Якщо ж додавання NoDisplay=True не спрацьовує, то Ви можете додати ShowOnlyIn=XFCE.

### Автомонтування

[PCManFM#Volume_handling](/index.php/PCManFM#Volume_handling "PCManFM")

### Автостарт програм

	Файли .desktop

Для початку Вам потрібно зробити символьне посилання від файлу запуску програми `.desktop` в `/usr/share/applications/` до `~/.config/autostart/`. Наприклад, для запуску програми lxterminal автоматично під час запуску робочого середовища:

```
$ ln -s /usr/share/applications/lxterminal.desktop ~/.config/autostart/

```

Після того як файл `.desktop` додано, Ви можете керувати автозапуском за допомогою графічної утиліти [lxsession-edit](https://aur.archlinux.org/packages/lxsession-edit/).

	Файл autostart

Наступний метод полягає у використанні файлу `~/.config/lxsession/LXDE/autostart`. Цей файл не є shell-скриптом, однак в кожній стрічці вказана команда для запуску, якщо ж команда починається з символу @, то тоді вона буде перезапущена у випадку краху. Наприклад, для запуску lxterminal і leafpad автоматично при запуску сесії:

 `~/.config/lxsession/LXDE/autostart` 
```
@lxterminal
@leafpad

```

**Note:** Команди **не повинні** закінчуватися символом & .

Також існує глобальний файл автозапуску в `/etc/xdg/lxsession/LXDE/autostart`. Якщо в системі присутні обидва файли (глобальний і користувацький), тоді буде запущено вміст обох файлів.

### Прив’язки

Мишка і привязки клавіш (наприклад скорочення клавіатури) здійснюється за допомогою Openbox і описано детально [тут](http://openbox.org/wiki/Help:Bindings). Користувачі LXDE повинні використати ці інструкції для редагування файлу ~/.config/openbox/lxde-rc.xml

Для редагування привязок клавіш можна використати GUI [obkey](https://aur.archlinux.org/packages/obkey/), доступне в AUR. Типовий файл для редагування obkey є rc.xml, але ви можете використати його для редагування конфігурації LXDE наступним чином:

```
$ obkey ~/.config/openbox/lxde-rc.xml

```

Більше інформації про obkey можна знайти [тут](http://code.google.com/p/obkey/).

### Курсори

The latest [lxappearance2-git](https://aur.archlinux.org/packages/lxappearance2-git/) in [AUR](/index.php/AUR "AUR") provides functionality to change cursor themes. If you do not want to install newer, experimental lxappearance2, you'll have to define your cursor in your `~/.Xdefaults` file. See [configuring cursor themes](/index.php/X11_Cursors#Configuring_Cursor_Themes "X11 Cursors").

A basic way is to add the cursor to the default theme. First you will need to make the directory:

```
# mkdir /usr/share/icons/default

```

Then you can specify to add to the icon theme the cursor. This will use the [xcursor-bluecurve](https://www.archlinux.org/packages/?name=xcursor-bluecurve) pointer theme:

 `/usr/share/icons/default/index.theme` 
```
[icon theme]
Inherits=Bluecurve
```

#### Власна тека іконок в $HOME

На даний момент PCmanFM ще не підтримує цю функцію:

[https://bbs.archlinux.org/viewtopic.php?pid=851397#p851397](https://bbs.archlinux.org/viewtopic.php?pid=851397#p851397)

### Час цифрового годинника

Ви можете клацнути правою кнопкою миші на годиннику на панелі і налаштувати відображення часу. Наприклад, для відображення стандартного часуу форматі HH:MM:SS:

```
%I:%M

```

У вигляді YYYY/MM/DD HH:MM:SS :

```
%Y/%m/%d %H:%M:%S

```

Дивіться допомогу на `strftime (3)`, щоб дізнатися більше про параметри.

### Налаштування шрифтів

Для налаштування шрифтів можна використати [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) і встановити основний шрифт. Для інших шрифтів використайте гномівський Центр контролю:

```
# pacman -S gnome-control-center

```

Після встановлення шрифтів можна вилучити програму, оскільки зміни залишаться.

### Розкладка клавіатури

1 спосіб: Додайте в /etc/xdg/lxsession/LXDE/autostart наступну стрічку перед @lxpanel --profile LXDE:

```
@setxkbmap -option grp:switch,grp:alt_shift_toggle,grp_led:scroll us,uk

```

або ~/.config/lxsession/LXDE/autostart (для кожного користувача):

```
setxkbmap -option grp:switch,grp:alt_shift_toggle,grp_led:scroll us,uk

```

2 спосіб: Створіть файл /etc/xdg/autostart/setxkmap.desktop з таким змістом:

```
[Desktop Entry]
Version=1.0
Encoding=UTF-8
Name=Fix keyboard settings
Exec=setxkbmap -rules xorg -layout "us,uk" -variant "," -option "grp:alt_shift_toggle"
Terminal=false
Type=Application 

```

3 спосіб: Відредагуйте файл ~/.Xkbmap для поточного користувача або файл /etc/X11/Xkbmap для всієї системи додаючи наступну стрічку:

```
-option grp:alt_shift_toggle,grp_led:scroll us,uk

```

4 спосіб: Додайте наступну стрічку до /etc/X11/xinit/xinitrc або ~/.xinitrc:

```
setxkbmap -option grp:alt_shift_toggle,grp_led:scroll us,uk

```

5 спосіб: Встановіть [fbxkb](http://fbxkb.sourceforge.net/) або qxkb з [AUR](/index.php/AUR "AUR")

6 спосіб: [Xorg#Switching_Between_Keyboard_Layouts](/index.php/Xorg#Switching_Between_Keyboard_Layouts "Xorg")

#### Додавання “Переключателя розкладки клавіатури” до панелі

1.  Клікніть правою клавішою на Вашій панелі
2.  Виберіть “Додати / Видалити компоненти панелі”
3.  Виберіть “Додати”
4.  Виберіть “Переключатель розкладки клавіатури”

### Gnome-screensaver в LXDE

Встановіть потрібні пакунки:

```
pacman -S gnome-screensaver gnome-session

```

Створіть простий запускач для сесії Гнома, щоб запустити зберігач екрану. Для цьго створіть файл `~/.config/autostart/gnome-session.desktop` з таким змістом:

```
[Desktop Entry]
Exec=/usr/bin/gnome-session

```

Тепер вийдіть з сесії і ввійдіть знову. Зберігач екрану повинен бути запущений.

### Іконки lxpanel’і

Типові іконки, що використовуються в lxpanel, зберігаються в `/usr/share/pixmaps`. Будь-які іконки, які Ви бажаєте використати, теж потрібно зберегти в тому місці.

Ви можете змінити типові іконки для програм, зробивши наступні кроки:

1.  Зберегти нову іконку в /usr/share/pixmaps
2.  Використати текстовий редактор і відкрити файл `.desktop` програми, де б Ви хотіли змінити іконку, в `/usr/share/applications`.
3.  Змінити

```
Icon=/default/icon/.png

```

на

```
Icon=/name/of/new/icon/added/to/pixmaps/.png

```

### LXDM

LXDE має власний експериментальний менеджер входу на базі GTK+, який називається LXDM. Щоб встановити LXDM виконайте наступне:

```
# sudo pacman -S lxdm

```

Тоді змініть наступну стрічку у файлі `/etc/inittab`:

```
x:5:respawn:/usr/sbin/lxdm >& /dev/null

```

#### Автовхід

Відредагуйте файл `/etc/lxdm/lxdm.conf`:

```
[base]
autologin=Назва_користувача

```

### PCManFM

[Сторінка вікі PCManFM](/index.php/PCManFM "PCManFM")

Для того щоб використовувати Смітник, монтувати диски, моніторувати зміни на диску Вам потрібно встановити підтримку gvfs:

```
pacman -S polkit-gnome gvfs

```

polkit-gnome забезпечує автентифікацію і тому його потрібно запустити при вході:

```
mkdir -p ~/.config/autostart
cp /etc/xdg/autostart/polkit-gnome-authentication-agent-1.desktop ~/.config/autostart

```

Файл запуску polkit-gnome-authentication-agent-1.desktop на даний момент не працює добре на деяких робочих столах. Якщо появляться якісь проблеми запуску, тоді приберіть цю стрічку в ньому:

```
OnlyShowIn=GNOME;XFCE;

```

[PCManFM @ LXDE wiki](http://wiki.lxde.org/en/PCManFM_build_and_setup_guide#Setup_Runtime_Environment_Correctly)

### Заміна менеджера вікон

[Openbox](/index.php/Openbox "Openbox"), the default window manager of LXDE, can be easily replaced by other window managers, such as fvwm, icewm, dwm, metacity, compiz ...etc.

LXDE will attempt to use window manager from the user lxsession configuration file `~/.config/lxsession/LXDE/desktop.conf`. If it does not exist, it will then attempt to use the global configuration file `/etc/xdg/lxsession/LXDE/desktop.conf`.

Replace the openbox-lxde command with the window manager of your choice:

```
[Session]
window_manager=openbox-lxde

```

For metacity:

```
window_manager=metacity

```

For compiz:

```
window_manager=compiz ccp --indirect-rendering

```

### Опції засинання і сплячки

Щоб працювали опціїї Виключення, Перезавантаження, Сплячки та Засинання, потрібно мати запущений dbus. Вам також потрібн встановити [pm-utils](/index.php/Pm-utils "Pm-utils") та upower.

```
#pacman -S pm-utils upower

```

Тоді додайте свого користувача до групи power:

```
# gpasswd -a <КОРИСТУВАЧ> power

```

Переконайтесь, що Ви сконфігурували `~/.xinitrc` так як сказано в [Запуск робочого столу](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.80.D0.BE.D0.B1.D0.BE.D1.87.D0.BE.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D1.83):

```
exec startlxde

```

### Виключення і перезапуск з LXDE

Щоб мати можливість виключати, перезавантажувати і входити в режим сну з меню виходу, потрібно переконатися, що dbus і HAL запущений, а тоді додайте Вашого користувача до групи power:

```
# gpasswd -a <USERNAME> power

```

## Помилки

### Управління ключами SSH

Управління ключами ssh можна здійснити за допомогою keychain. Дивіться статтю [використання keychain](/index.php/Using_SSH_Keys#Using_keychain "Using SSH Keys") для більшої інформації.

### GTK+ Warnings with lxsession 0.4.1

When starting GTK+2 programs you get the following message:

```
GTK+ icon them is not properly set

This usually means you don't have an XSETTINGS manager running. Desktop environment like GNOME or XFCE automatically execute
their XSETTING managers like gnome-settings-daemon or xfce-mcs-manager.

```

This is caused by the migration of lxde-settings-daemon config files into lxsession. If you made customizations to these config files, you are in need of merging those config files:

*   /usr/share/lxde/config
*   ~/.config/lxde/config

into

*   etc/xdg/lxsession/LXDE/desktop.conf
*   ~/.config/lxsession/LXDE/desktop.conf

Alternatively, you can use lxappearance from the community repository to fix this.

### LXsession Full

There are some bugs in lxsession related to session management. lxsession-lite is a version of lxsession which does not have the session management capability. The stability of lxsession-lite is better than lxsession, however it can not save and restore sessions. Thus it is recommended to use lxsession-lite till the problems in lxsession are fixed.

## Ресурси

*   [LXDE wiki entry related to Arch Linux](http://wiki.lxde.org/en/ArchLinux)
*   [LXDE Project (Sourceforge)](http://lxde.sourceforge.net)
*   [LXDE Forum](http://forum.lxde.org)
*   [The Latest lx* Packages](https://sourceforge.net/project/showfiles.php?group_id=180858)
*   [PCMan File Manager](https://sourceforge.net/project/showfiles.php?group_id=156956)