| **Summary**  |
| Сховище Пакунків Користувачів є сховищем [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")’ів, що надіслані користувачами і які доповнюють програми з [офіційних сховищ](/index.php/Official_repositories "Official repositories"). Ця стаття описує процес збирання *непідтримуваних* пакунків з AUR. |
| **Огляд** |
| Packages in Arch Linux are built using [makepkg](/index.php/Makepkg "Makepkg") and a custom build script for each package (known as a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")). Once packaged, software can be installed and managed with [pacman](/index.php/Pacman "Pacman"). PKGBUILDs for software in the [official repositories](/index.php/Official_repositories "Official repositories") are available from the [ABS](/index.php/Arch_Build_System "Arch Build System") tree; thousands more are available from the (unsupported) [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). |
| **Подібне** |
| [AUR helpers](/index.php/AUR_helpers "AUR helpers") |
| [AUR Trusted User Guidelines](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") |
| **Ресурси** |
| [Веб-сторінка AUR](https://aur.archlinux.org) |
| [Список розсилки AUR](https://www.archlinux.org/mailman/listinfo/aur-general) |

Arch User Repository (AUR) — це сховище пакунків, кероване спільнотою Arch. Воно містить описи пакунків (так звані PKGBUILD), що полегшують зібрання пакета з джерела ([makepkg](/index.php/Makepkg "Makepkg")) та його встановлення ([pacman](/index.php/Pacman "Pacman")). Метою AUR є організація й розповсюдження нових пакунків, створених користувачами, а також надання доступу до популярних пакунків через сховища [[community]](#.5Bcommunity.5D). Ця стаття пояснює, як використовувати AUR.

Чимало пакунків, що отримують місце в офіційних сховищах, створюються в AUR. Завдяки AUR користувачі можуть внести свій вклад у розвиток пакунку за рахунок супроводу PKGBUILD й пов’язаних файлів. Спільнота AUR має можливість проголосувати за пакунок у цьому сховищі чи проти нього; пакунок, за який проголосувало достатньо користувачів, потрапляє до сховища [community], що доступний прямо через [pacman](/index.php/Pacman "Pacman") чи [abs](/index.php/ABS "ABS").

## Contents

*   [1 З чого почати](#.D0.97_.D1.87.D0.BE.D0.B3.D0.BE_.D0.BF.D0.BE.D1.87.D0.B0.D1.82.D0.B8)
*   [2 Історія](#.D0.86.D1.81.D1.82.D0.BE.D1.80.D1.96.D1.8F)
*   [3 Пошук](#.D0.9F.D0.BE.D1.88.D1.83.D0.BA)
*   [4 Встановлення пакунків](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_.D0.BF.D0.B0.D0.BA.D1.83.D0.BD.D0.BA.D1.96.D0.B2)
    *   [4.1 Підготовка](#.D0.9F.D1.96.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [4.2 Отримання файлів для збирання](#.D0.9E.D1.82.D1.80.D0.B8.D0.BC.D0.B0.D0.BD.D0.BD.D1.8F_.D1.84.D0.B0.D0.B9.D0.BB.D1.96.D0.B2_.D0.B4.D0.BB.D1.8F_.D0.B7.D0.B1.D0.B8.D1.80.D0.B0.D0.BD.D0.BD.D1.8F)
    *   [4.3 Збирання пакунка](#.D0.97.D0.B1.D0.B8.D1.80.D0.B0.D0.BD.D0.BD.D1.8F_.D0.BF.D0.B0.D0.BA.D1.83.D0.BD.D0.BA.D0.B0)
    *   [4.4 Встановлення пакунка](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_.D0.BF.D0.B0.D0.BA.D1.83.D0.BD.D0.BA.D0.B0)
*   [5 Зворотній зв’язок](#.D0.97.D0.B2.D0.BE.D1.80.D0.BE.D1.82.D0.BD.D1.96.D0.B9_.D0.B7.D0.B2.E2.80.99.D1.8F.D0.B7.D0.BE.D0.BA)
*   [6 Обмін пакунками](#.D0.9E.D0.B1.D0.BC.D1.96.D0.BD_.D0.BF.D0.B0.D0.BA.D1.83.D0.BD.D0.BA.D0.B0.D0.BC.D0.B8)
    *   [6.1 Надсилання пакунків](#.D0.9D.D0.B0.D0.B4.D1.81.D0.B8.D0.BB.D0.B0.D0.BD.D0.BD.D1.8F_.D0.BF.D0.B0.D0.BA.D1.83.D0.BD.D0.BA.D1.96.D0.B2)
    *   [6.2 Підтримка пакунків](#.D0.9F.D1.96.D0.B4.D1.82.D1.80.D0.B8.D0.BC.D0.BA.D0.B0_.D0.BF.D0.B0.D0.BA.D1.83.D0.BD.D0.BA.D1.96.D0.B2)
    *   [6.3 Інші запити](#.D0.86.D0.BD.D1.88.D1.96_.D0.B7.D0.B0.D0.BF.D0.B8.D1.82.D0.B8)
*   [7 Сховище [community]](#.D0.A1.D1.85.D0.BE.D0.B2.D0.B8.D1.89.D0.B5_.5Bcommunity.5D)
*   [8 Сховище Git](#.D0.A1.D1.85.D0.BE.D0.B2.D0.B8.D1.89.D0.B5_Git)
*   [9 FAQ](#FAQ)
    *   [9.1 What is the AUR?](#What_is_the_AUR.3F)
    *   [9.2 What kind of packages are permitted on the AUR?](#What_kind_of_packages_are_permitted_on_the_AUR.3F)
    *   [9.3 What is a TU?](#What_is_a_TU.3F)
    *   [9.4 What's the difference between the Arch User Repository and [community]?](#What.27s_the_difference_between_the_Arch_User_Repository_and_.5Bcommunity.5D.3F)
    *   [9.5 How many votes does it take to get a PKGBUILD into [community]?](#How_many_votes_does_it_take_to_get_a_PKGBUILD_into_.5Bcommunity.5D.3F)
    *   [9.6 How do I make a PKGBUILD?](#How_do_I_make_a_PKGBUILD.3F)
    *   [9.7 I'm trying to do pacman -S foo; it isn't working but I know it's in [community]](#I.27m_trying_to_do_pacman_-S_foo.3B_it_isn.27t_working_but_I_know_it.27s_in_.5Bcommunity.5D)
    *   [9.8 Foo in AUR is outdated; what do I do?](#Foo_in_AUR_is_outdated.3B_what_do_I_do.3F)
    *   [9.9 I have a PKGBUILD I would like to submit; can someone check it to see if there are any errors?](#I_have_a_PKGBUILD_I_would_like_to_submit.3B_can_someone_check_it_to_see_if_there_are_any_errors.3F)
    *   [9.10 Foo in AUR doesn't compile when I do makepkg; what should I do?](#Foo_in_AUR_doesn.27t_compile_when_I_do_makepkg.3B_what_should_I_do.3F)
    *   [9.11 How can I speed up repeated build processes?](#How_can_I_speed_up_repeated_build_processes.3F)
    *   [9.12 How do I access unsupported packages?](#How_do_I_access_unsupported_packages.3F)
    *   [9.13 How can I upload to AUR without using the web interface?](#How_can_I_upload_to_AUR_without_using_the_web_interface.3F)

## З чого почати

Знайти і звантажити PKGBUILD можна через [веб-інтерфейс AUR](https://aur.archlinux.org). PKGBUILD слід зібрати в пакунок (за допомогою [makepkg](/index.php/Makepkg "Makepkg")), який потім встановлюється за допомогою pacman.

*   Встановіть [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) (`pacman -S base-devel`). Члени цієї групи не вказані в PKGBUILD; [очікується](https://bbs.archlinux.org/viewtopic.php?pid=632355), що вони вже встановлені, без них чимало пакунків із AUR зібрати не вдасться.
*   Далі в цій статті подана детальніша інформація зі встановлення пакунків із AUR.
*   Час від часу відвідуйте [веб-інтерфейс AUR](https://aur.archlinux.org) і оновлюйте необхідні пакунки. За цією адресою також надано статистику й список свіжих оновлень пакунків.
*   [#FAQ](#FAQ) відповідає на найпоширеніші питання.
*   Оптимізуйте `/etc/makepkg.conf` відповідно до можливостей процесора. Помітне пришвидшення компіляції пакунків на багатоядерних процесорах унаслідок модифікації змінної MAKEFLAGS. За специфічні відносно обладнання оптимізації GCC відповідає змінна CFLAGS. Детальніше про це розповідається в [makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf").

## Історія

Наступні дані подано тільки задля історичної цінності. Їм на зміну прийшов AUR і зараз до них доступу вже немає.

Спочатку було `ftp://ftp.archlinux.org/incoming`, куди бажаючі могли вивантажити свій PKGBUILD, потрібні супровідні файли і створений пакунок на сервер. Пакунок і відповідні файли залишалися там, поки [Управляючий пакунками](/index.php/Package_Maintainer "Package Maintainer") не побачить його і займеться ним.

Пізніше народилася ідея Сховища Довірених Користувачів. Певним користувачам спільноти дозволено розміщувати свої сховища і давати іншим можливість користатися ними. На цьому розбудувався AUR, для більшої доступності і гнучкості. Фактично розробники пакунків з AUR можуть подавати на отримання звання TUs (Довірені Користувачі).

## Пошук

Веб-інтерфейс AUR знаходиться [тут](https://aur.archlinux.org/). Опис інтерфейсу для використання AUR зі скрипта знаходиться [тут](https://aur.archlinux.org/rpc.php).

За запитом надаються імена й описи пакунків через порівняння MySQL LIKE. Це дозволяє здійснювати ширший пошук (наприклад, спробуйте 'tool%like%grep' замість 'tool like grep'). Опис, що містить '%', слід шукати з '\%' у цьому місці.

## Встановлення пакунків

Встановлення пакунків з AUR є відносно простим процесом. Фактично:

1.  Отримати tar-архів, що містить PKGBUILD та інші потрібні файли
2.  Розпакувати архів (бажано в теку, що призначена суто для створення пакунків з AUR)
3.  Запустити **makepkg** в теці, де збережені файли (запуск "makepkg -s" автоматично встановить залежності за допомогою pacman)
4.  Встановити вихідний файл пакунку за допомогою **pacman**:

```
# pacman -U /шлях/до/пакунку.tar.xz

```

[AUR-помічники](/index.php/AUR_helpers "AUR helpers") дають простий доступ до AUR. Вони відрізняються своїми функціями, але в основному вони можуть шукати, отримувати, створювати та встановлювати з PKGBUILD-ів, знайдених в AUR. Всі ці скрипти теж можна знайти в AUR.

**Note:** Немає і ніколи не було *офіційного* способу встановлення пакунків з AUR. Всі користувачі повинні ознайомитися з процесом створення.

Нижче подано конкретний приклад встановлення пакунку з назвою "foo".

### Підготовка

Спочатку впевніться, чи встановлені всі необхідні пакунки. Групи пакунків "base-devel" повинно вистачити; вона містить *make* та інші утиліти для компіляції з джерельних файлів.

**Warning:** Для пакунків з AUR вважається, що група "base-devel" вже встановлена, і не міститься в списку залежностей, навіть якщо пакунок не вдасться зібрати без неї. Тому впевніться, що ця група пакунків встановлена пере тим як нарікати, що пакунок не збирається.

```
# pacman -S base-devel

```

Далі виберіть відповідну теку для збирання пакунку. Тека для збирання - це просто тека, де пакунок буде створений або "зібраний" і це може бути будь-яка тека. Прикладом загальновживаних тек є:

```
~/builds

```

або, якщо ви використовуєте ABS ([Система Збирання Арча](/index.php/Arch_Build_System "Arch Build System")):

```
/var/abs/local

```

Щоб отримати більше інформації про ABS прочитайте статтю [Система Збирання Арча](/index.php/Arch_Build_System "Arch Build System"). У прикладі використовується тека `~/builds` як тека для збирання.

### Отримання файлів для збирання

Спочатку знайдіть пакунок в AUR. Це можна зробити за допомогою пошуку на [Домашній сторінці AUR](https://aur.archlinux.org/). Натискання на назві програми в списку переносить до сторінки з інформацією про пакунок. Прочитайте опис, щоб знати точно, чи цей пакунок вам потрібно, перевірте коли пакунок був оновлений, і прочитайте коментарі.

Завантажте потрібні файли для збирання. На сторінці інформації про пакунок натисніть на посилання "Архів" в лівому нижньому кутку в кінці опису пакунка. Цей файл потрібно зберегти в теці збирання, або скопіювати в цю теку після звантаження. В цьому прикладі цей файл названо "foo.tar.gz" (стандартний формат це *назва_пакунка*.tar.gz).

### Збирання пакунка

Розпакуйте завантажений файл архіву. Для цього змініть теку на теку збирання, якщо ви ще не в ній, та розпакуйте файли для збирання до неї.

```
$ cd ~/builds
$ tar -xvzf foo.tar.gz

```

Ця операція повинна створити нову теку з назвою "foo" в теці збирання.

**Warning:** **Уважно перевірте всі файли.** `cd` до щойно створеної теки і уважно перевірте файл `PKGBUILD` та решту файлів `.install` на предмет небажаних команд. Файли `PKGBUILD`ів - це bash-скрипти, що містять функції, які запускаються через `makepkg`: ці функції можуть містити *будь-які* команди або синтаксис bash’у, тому цілком правдоподібно `PKGBUILD` може містити небезпечні команди по злобі або невігластву з боку автора. Оскільки `makepkg` використовує fakeroot (і ніколи не повинен запускатися з правами суперкористувача), тому є певний рівень захисту, однак ви не повинні ніколи на це розраховувати. Якщо ви сумніваєтесь, не збирайте цей пакунок та шукайте допомоги на форумах або списку розсилки.

```
$ cd foo
$ nano PKGBUILD
$ nano foo.install

```

Створення пакунка. Після того як ви вручну перевірили цілісність файлів, запустіть [makepkg](/index.php/Makepkg "Makepkg") як звичайний користувач в теці збирання.

```
$ makepkg -s

```

Перемикач `-s` використовує [sudo](/index.php/Sudo "Sudo") для встановлення всіх потрібних залежностей. Якщо ви не бажаєте використовувати sudo, тоді вручну встановіть всі необхідні пакунки-залежності перед збиранням і запускайте тоді команду вище вже без перемикача `-s`.

### Встановлення пакунка

Встановіть пакунок за допомогою pacman. Створений файл пакунка повинен мати таку назву:

```
<*назва програми*>-<*номер версії програми*>-<*номер перегляду пакунка*>-<*архітектура*>.pkg.tar.xz

```

Цей пакунок можна встановити за допомогою команди pacman'а "upgrade" (оновити):

```
# pacman -U foo-0.1-1-i686.pkg.tar.xz   

```

Ці вручну встановлені пакунки називаються сторонніми пакунками - пакунками, що не походять з жоного сховища, які використовує pacman. Для отримання списку сторонніх пакунків запустіть команду:

```
$ pacman -Qm 

```

**Note:** Наведений вище приклад є тільки коротким підсумком процесу створення пакунка. Завітайте на сторінки [makepkg](/index.php/Makepkg "Makepkg") та [ABS](/index.php/ABS "ABS"), де міститься більш детальніша інформація, і які рекомендуються для перегляду всім (особливо для новачків.

## Зворотній зв’язок

На [Веб-сторінці AUR](https://aur.archlinux.org) для користувачів існує можливіть залишати коментарі та відгуки щодо покращення пакунка для власника PKGBUILD’а. Уникайте вставляти патчі або PKGBUILD’и в коментарях: вони швидко стають застарілими та тільки забирають багато місця. Замість цього відсилайте ці файли електронною поштою до власника пакунка, або ж використайте [pastebin](/index.php/Pastebin_Clients "Pastebin Clients").

Найпростішим способом виразити своє ставлення до пакунка для **всіх** користувачів Arch’а є відкрити веб-сторінку AUR і **проголосувати** за улюблені пакунки. Всі пакунки можуть бути адаптованими TU-користувачами для включення їх в сховище [community], тому кількість голосів, відданих за пакунок, може стати вагомим аргументом в цьому процесі; тому в інтересах кожного проголосувати!

## Обмін пакунками

Користувачі є найбільш цінними для AUR, яке б не реалізувало свій потенціал без їхньої підтримки, ангажованості і внеску. Тривалість життя AUR-пакунку напряму залежить від користувача. Користувач може поділитися своїм пакунком наступним чином.

Користувачі можуть **поділитися** своїм PKGBUILD’ом використовуючи Сховище Пакунків Користувачів Arch’а (AUR). Сховище не містить жодного бінарного пакунка, але дозволяє користувачам вивантажувати PKGBUILD’и, які, в свою чергу, інші користувачі можуть завантажити. Ці PKGBUILD’и неофіційні і не були повністю перевірені, тому їх використовують на свій власний страх та ризик.

### Надсилання пакунків

Після логування на веб-сторінці AUR користувач може [вислати](https://aur.archlinux.org/pkgsubmit.php) архівовану (`.tar.gz`) теку, що містить файли пакунка. Тека всередині архіву повинна містити [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), файли `.install`, поправки, етс. (**без жодних** бінарних файлів). Приклад такої теки можна побачити, заглянувши в теку `/var/abs`, якщо встановлена [Система Збирання Arch'а](/index.php/Arch_Build_System "Arch Build System").

Архів можна створити за допомогою команди:

```
$ makepkg --source 

```

Зауважте, що це є архів tar і gz; наприклад, якщо ви надсилаєте пакунок з назвою *libfoo*, після створення архіву він повинен мати подібний вигляд:

```
# Список вмісту архіву.
$ tar tf libfoo-0.1-1.src.tar.gz
libfoo/
libfoo/PKGBUILD
libfoo/libfoo.install

```

Готуючи пакунок для AUR, дотримуйтесь наступних правил:

*   Перевірте [базу пакунків](https://www.archlinux.org/packages/) щодо подібних пакунків. Якщо пакунок вже існує, **не** надсилайте пакунка. Якщо поточний пакунок застарілий або не має потрібних можливостей, тоді [повідомте про ваду](https://bugs.archlinux.org/).
*   Перевірте AUR на наявність подібного пакунка. Якщо пакунок вже підтримується, зміни можна надіслати як коментар для власника. Якщо ж не підтримується, тоді пакунок можна привласнити і оновлювати. Не створюйте дублікатів пакунка.
*   Уважно перевірте файл для надсилання. Усі, хто надсилає пакунки, повинні прочитати та дотримуватися [Стандартів Збирання Arch'а](/index.php/Arch_packaging_standards "Arch packaging standards"). Це необхідно для нормального функціонування і загального успіху AUR. Пам’ятайте, що Ви не заробите бонусів та повагу інших користувачів, що витратять час з поганим PKGBUILD’ом.
*   Пакунки, що містять бінарні файли або погано написані, можуть бути видалені без попередження.
*   Якщо ви не впевнені щодо пакунка (або процесом збирання/надсилання), надішліть PKGBUILD до [Списку Розсилки AUR](https://mailman.archlinux.org/mailman/listinfo/) або до [дошки повідомлень AUR](https://bbs.archlinux.org/viewforum.php?id=4) на форумі для публічної рецензії перед надсиланням пакунка до AUR.
*   Впевніться, що пакунок дійсно потрібний. Чи ще хто-небуть буде використовувати цей пакунок? Якщо більше ніж кілька людей визнають, що пакунок потрібний, тоді його вартує надіслати до AUR.
*   Отримайте трохи досвіду перед надсиланням пакунка. Зберіть кілька пакунків, щоб вивчити сам процес збирання, і тільки тоді надсилайте.
*   Якщо ви надсилаєте `package.tar.gz` з файлом з назвою '`package`', ви отримаєте помилку : 'Не можу змінити теку `/home/aur/unsupported/package/package`'. Щоб це вирішити, перейменуйте '`package`' на щось інше, наприклад, '`package.rc`'. Тоді встановиться в теку `pkg` яку можете перейменувати назад на '`package`'.

Обов’язково прочитайте [Стандарти Збирання Arch'а#Надсилання пакунків в Aur](/index.php/Arch_packaging_standards#Submitting_Packages_to_the_AUR "Arch packaging standards").

### Підтримка пакунків

*   Якщо ви підтримуєте якийсь пакунок і бажаєте оновити PKGBUILD для вашого пакунка, тоді просто надішліть його ще раз.
*   Перевірте відгуки та коментарі від інших користувачів і намагайтесь врахувати запропоновані поправки; вважайте це процесом навчання!
*   Не забувайте про пакунки, що ви надіслали! Підтримувати пакунок - це робота власника, підтримувати та оновлювати PKGBUILD.
*   Якщо ви не бажаєте продовжувати підтримувати пакунок з певних причин, `зречіться` пакунка, використовуючи веб-інтерфейс AUR, та/або надсилаючи повідомлення до Списку Розсилки AUR.

### Інші запити

*   Запит про зречення пакунка та запит на видалення треба спрямовувати до списку розсилки aur-general до TU та до інших користувачів, як вирішують проблему.
*   **Додайте назву пакунка та посилання на сторінку AUR пакунка**, бажано з виноскою [1].
*   Запит на зречення пакунку буде втілений два тижні після того, як поточний власник пакунку не відповів на електронного листа.
*   **Злиття пакунків зреалізовано**, користувачі все ще повинні надіслати пакунок з новою назвою і можливо коментарі зі старої версії і голосування в списку розсилки
*   Запит на вилучення вимагає наступної інформації:
    *   Назва пакунка та посилання на сторінку AUR пакунка
    *   Причина вилучення, хочаб кілька слів
        **Примітка:** Коментарі до пакунка не завжди дають розуміння причини видалення. Тому як тільки TU зреагує, єдиним місцем, де можна буде отримати інформацію про причини вилучення, буде тільки список розсилки aur-general.
    *   Додайте додаткові деталі, наприклад, що даний пакунок вже реалізований іншим пакунком, якщо ви самі є власником цього пакунка, він перейменований і інший власник погоджується, етс.

Запит на вилучення може бути відхилений, в такому випадку вам запропонують зректися пакунка, щоб хтось інший став його власником.

## Сховище [community]

Сховище [community], яке підтримується [Довіреними Користувачами](/index.php/Trusted_Users "Trusted Users"), містить найбільш популярні пакунки з AUR. Це сховище підключене по замовчуванню `/etc/pacman.conf`. Якщо [community] не підключене або вилучене, тоді його можна включити, відкоментовуючи або додаючи ці дві стрічки:

 `/etc/pacman.conf` 
```
...
[community]
Include = /etc/pacman.d/mirrorlist
...

```

Сховище [community], на відміну від AUR, містить бінарні пакунки, які можна встановити безпосередньо з [pacman](/index.php/Pacman "Pacman"), а файли для збирання цих пакунків можна отримати за допомогою [ABS](/index.php/Arch_Build_System "Arch Build System"). Деякі з цих пакунків можуть переміщувати до сховищ [core] або [extra], якщо розробники вирішать, що ці пакунки є необхідні для системи.

Користувачі також можуть отримати доступ до файлів збирання пакунків з [community], редагуючи файл `/etc/abs.conf` і включаючи сховище [community] в списку `REPOS`.

## Сховище Git

Сховище Git з AUR підтримується через Thomas Dziedzic, і яке теж містить історію пакунків. Сховище оновлюється як мінімум раз в день. Щоб отримати копію сховища (кілька сотень MБ):

```
$ git clone [git://pkgbuild.com/aur-mirror.git](git://pkgbuild.com/aur-mirror.git)

```

[Веб-інтерфейс](http://pkgbuild.com/git/aur-mirror.git/), [Читай_мене](http://pkgbuild.com/~td123/readme), [Гілка форуму](https://bbs.archlinux.org/viewtopic.php?id=113099)

## FAQ

### What is the AUR?

The AUR (Arch User Repository) is a place where the Arch Linux community can upload [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") of applications, libraries, etc., and share them with the entire community. Fellow users can then vote for their favorites to be moved into the [community] repository to be shared with Arch Linux users in binary form.

### What kind of packages are permitted on the AUR?

The packages on the AUR are merely "build scripts", i.e recipes to build binaries for pacman. For most cases, everything is permitted, as long as you are in compliance with the licensing terms of the software. For other cases, where it is mentioned that "you may not link" to downloads, i.e contents that are not redistributable, you may only use the file name itself as the source. This means and requires users to already have the restricted source in the build directory prior to building the package. Piracy is frowned upon, so "warez" is absolutely not permitted. When in doubt, ask.

### What is a TU?

A [TU (Trusted User)](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") is a person who is chosen to oversee AUR and the [community] repository. They're the ones who maintain popular PKGBUILDs in [community], and overall keep the AUR running.

### What's the difference between the Arch User Repository and [community]?

The Arch User Repository is where all PKGBUILDs that users submit are stored, and must be built manually with [makepkg](/index.php/Makepkg "Makepkg"). When PKGBUILDs receive enough votes, they are moved into the [community] repository, where the TUs maintain binary packages that can be installed with [pacman](/index.php/Pacman "Pacman").

### How many votes does it take to get a PKGBUILD into [community]?

Usually, at least 10 votes are required for something to move into [community]. However, if a TU wants to support a package, it will often be found in the repository.

### How do I make a PKGBUILD?

The best resource is [Creating packages](/index.php/Creating_packages "Creating packages"). Remember to look in AUR before creating the PKGBUILD as to not duplicate efforts.

### I'm trying to do `pacman -S foo`; it isn't working but I know it's in [community]

You probably haven't enabled [community] in your `/etc/pacman.conf`. Just uncomment the relevant lines. If [community] is enabled in your `/etc/pacman.conf` try running `pacman -S -y` first to synchronize the pkgcache before trying your package again.

### Foo in AUR is outdated; what do I do?

For starters, you can flag packages out-of-date. If it stays out-of-date for an extended period of time, the best thing to do is email the maintainer. If there is no response from the maintainer after two weeks, you could send mail to the aur-general mailing list to have a TU orphan the PKGBUILD if you're willing to maintain it yourself.

### I have a PKGBUILD I would like to submit; can someone check it to see if there are any errors?

If you would like to have your PKGBUILD critiqued, post it on the aur-general mailing list to get feedback from the TUs and fellow AUR members. You could also get help from the [IRC channel](/index.php/ArchChannel "ArchChannel"), #archlinux on irc.freenode.net. You can also use [namcap](/index.php/Namcap "Namcap") to check your PKGBUILD and the resulting package for errors.

### Foo in AUR doesn't compile when I do `makepkg`; what should I do?

You are probably missing something trivial.

1.  Run `pacman -Syyu` before compiling anything with `makepkg` as the problem may be that your system is not up-to-date.
2.  Ensure you have both "base" and "base-devel" groups installed.
3.  Try using the "`-s`" option with `makepkg` to check and install all the dependencies needed before starting the build process.

Be sure to first read the PKGBUILD and the comments on the AUR page of the package in question. The reason might not be trivial after all. Custom CFLAGS, LDFLAGS and MAKEFLAGS can cause failures. It's also possible that the PKGBUILD is broken for everyone. If you cannot figure it out on your own, just report it to the maintainer e.g. by posting the errors you are getting in the comments on the AUR page.

### How can I speed up repeated build processes?

If you frequently compile code that uses gcc - say, a git or SVN package - you may find [ccache](/index.php/Ccache "Ccache"), short for "compiler cache", useful.

### How do I access unsupported packages?

See [#Installing packages](#Installing_packages)

### How can I upload to AUR without using the web interface?

You can use *aurploader* ([python3-aur](https://aur.archlinux.org/packages/python3-aur/)), [aurup](https://aur.archlinux.org/packages/aurup/) or [burp](https://www.archlinux.org/packages/?name=burp) -- these are command-line programs.