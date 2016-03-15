## Contents

*   [1 Передмова](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B4.D0.BC.D0.BE.D0.B2.D0.B0)
    *   [1.1 Вступ](#.D0.92.D1.81.D1.82.D1.83.D0.BF)
    *   [1.2 Ліцензія](#.D0.9B.D1.96.D1.86.D0.B5.D0.BD.D0.B7.D1.96.D1.8F)
    *   [1.3 ТІЛЬКИ БЕЗ ПАНІКИ!](#.D0.A2.D0.86.D0.9B.D0.AC.D0.9A.D0.98_.D0.91.D0.95.D0.97_.D0.9F.D0.90.D0.9D.D0.86.D0.9A.D0.98.21)
    *   [1.4 Шлях Arch](#.D0.A8.D0.BB.D1.8F.D1.85_Arch)
    *   [1.5 Про цю настанову](#.D0.9F.D1.80.D0.BE_.D1.86.D1.8E_.D0.BD.D0.B0.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D1.83)
*   [2 Частина I: Встановлення базової системи](#.D0.A7.D0.B0.D1.81.D1.82.D0.B8.D0.BD.D0.B0_I:_.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_.D0.B1.D0.B0.D0.B7.D0.BE.D0.B2.D0.BE.D1.97_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B8)
    *   [2.1 Крок 1: Отримання встановчого образу](#.D0.9A.D1.80.D0.BE.D0.BA_1:_.D0.9E.D1.82.D1.80.D0.B8.D0.BC.D0.B0.D0.BD.D0.BD.D1.8F_.D0.B2.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D1.87.D0.BE.D0.B3.D0.BE_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D1.83)
        *   [2.1.1 Встановлення з CD](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_.D0.B7_CD)
        *   [2.1.2 USB-флешка](#USB-.D1.84.D0.BB.D0.B5.D1.88.D0.BA.D0.B0)
    *   [2.2 Крок 2: Завантаження інсталятора Linux](#.D0.9A.D1.80.D0.BE.D0.BA_2:_.D0.97.D0.B0.D0.B2.D0.B0.D0.BD.D1.82.D0.B0.D0.B6.D0.B5.D0.BD.D0.BD.D1.8F_.D1.96.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D1.8F.D1.82.D0.BE.D1.80.D0.B0_Linux)
        *   [2.2.1 Зміна розкладки клавіатури](#.D0.97.D0.BC.D1.96.D0.BD.D0.B0_.D1.80.D0.BE.D0.B7.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D1.96.D0.B0.D1.82.D1.83.D1.80.D0.B8)
        *   [2.2.2 Документація](#.D0.94.D0.BE.D0.BA.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D0.B0.D1.86.D1.96.D1.8F)
    *   [2.3 Крок 3: Початок інсталяції](#.D0.9A.D1.80.D0.BE.D0.BA_3:_.D0.9F.D0.BE.D1.87.D0.B0.D1.82.D0.BE.D0.BA_.D1.96.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D1.8F.D1.86.D1.96.D1.97)
    *   [2.4 А: Вибір джерела для інсталяції](#.D0.90:_.D0.92.D0.B8.D0.B1.D1.96.D1.80_.D0.B4.D0.B6.D0.B5.D1.80.D0.B5.D0.BB.D0.B0_.D0.B4.D0.BB.D1.8F_.D1.96.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D1.8F.D1.86.D1.96.D1.97)
        *   [2.4.1 Конфігурування мережі (Netinstall)](#.D0.9A.D0.BE.D0.BD.D1.84.D1.96.D0.B3.D1.83.D1.80.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D0.BC.D0.B5.D1.80.D0.B5.D0.B6.D1.96_.28Netinstall.29)
            *   [2.4.1.1 (A)DSL Quickstart for the Live Environment (If you have a pure modem (or router in bridge mode) to connect to your ISP)](#.28A.29DSL_Quickstart_for_the_Live_Environment_.28If_you_have_a_pure_modem_.28or_router_in_bridge_mode.29_to_connect_to_your_ISP.29)
            *   [2.4.1.2 Wireless Quickstart For the Live Environment (If you need wireless connectivity during the installation process)](#Wireless_Quickstart_For_the_Live_Environment_.28If_you_need_wireless_connectivity_during_the_installation_process.29)
                *   [2.4.1.2.1 Does the Wireless Chipset require Firmware?](#Does_the_Wireless_Chipset_require_Firmware.3F)
    *   [2.5 Б: Налаштування годинника](#.D0.91:_.D0.9D.D0.B0.D0.BB.D0.B0.D1.88.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D0.B3.D0.BE.D0.B4.D0.B8.D0.BD.D0.BD.D0.B8.D0.BA.D0.B0)
    *   [2.6 В: Підготовка твердого диску](#.D0.92:_.D0.9F.D1.96.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0_.D1.82.D0.B2.D0.B5.D1.80.D0.B4.D0.BE.D0.B3.D0.BE_.D0.B4.D0.B8.D1.81.D0.BA.D1.83)
        *   [2.6.1 Розбивка твердих дисків](#.D0.A0.D0.BE.D0.B7.D0.B1.D0.B8.D0.B2.D0.BA.D0.B0_.D1.82.D0.B2.D0.B5.D1.80.D0.B4.D0.B8.D1.85_.D0.B4.D0.B8.D1.81.D0.BA.D1.96.D0.B2)
            *   [2.6.1.1 Інформація про розбивку](#.D0.86.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D1.96.D1.8F_.D0.BF.D1.80.D0.BE_.D1.80.D0.BE.D0.B7.D0.B1.D0.B8.D0.B2.D0.BA.D1.83)
            *   [2.6.1.2 Розділ підкачки (swap)](#.D0.A0.D0.BE.D0.B7.D0.B4.D1.96.D0.BB_.D0.BF.D1.96.D0.B4.D0.BA.D0.B0.D1.87.D0.BA.D0.B8_.28swap.29)
            *   [2.6.1.3 Схема розбивки](#.D0.A1.D1.85.D0.B5.D0.BC.D0.B0_.D1.80.D0.BE.D0.B7.D0.B1.D0.B8.D0.B2.D0.BA.D0.B8)
            *   [2.6.1.4 How big should my partitions be?](#How_big_should_my_partitions_be.3F)
            *   [2.6.1.5 Create Partition:cfdisk](#Create_Partition:cfdisk)
        *   [2.6.2 Налаштування точок монтування файлових систем](#.D0.9D.D0.B0.D0.BB.D0.B0.D1.88.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D1.82.D0.BE.D1.87.D0.BE.D0.BA_.D0.BC.D0.BE.D0.BD.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.B8.D1.85_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC)
            *   [2.6.2.1 Filesystem Types](#Filesystem_Types)
            *   [2.6.2.2 A note on Journaling](#A_note_on_Journaling)
    *   [2.7 D: Select Packages](#D:_Select_Packages)
    *   [2.8 E: Install Packages](#E:_Install_Packages)
    *   [2.9 F: Configure the System](#F:_Configure_the_System)
        *   [2.9.1 Can the installer handle this more automatically?](#Can_the_installer_handle_this_more_automatically.3F)
        *   [2.9.2 /etc/rc.conf](#.2Fetc.2Frc.conf)
            *   [2.9.2.1 LOCALIZATION section](#LOCALIZATION_section)
            *   [2.9.2.2 HARDWARE Section](#HARDWARE_Section)
            *   [2.9.2.3 NETWORKING Section](#NETWORKING_Section)
                *   [2.9.2.3.1 Example, using a dynamically assigned IP address (**DHCP**)](#Example.2C_using_a_dynamically_assigned_IP_address_.28DHCP.29)
                *   [2.9.2.3.2 Example, using a **static** IP address](#Example.2C_using_a_static_IP_address)
            *   [2.9.2.4 DAEMONS Section](#DAEMONS_Section)
                *   [2.9.2.4.1 About DAEMONS](#About_DAEMONS)
        *   [2.9.3 /etc/fstab](#.2Fetc.2Ffstab)
            *   [2.9.3.1 An example /etc/fstab](#An_example_.2Fetc.2Ffstab)
        *   [2.9.4 **/etc/mkinitcpio.conf**](#.2Fetc.2Fmkinitcpio.conf)
        *   [2.9.5 /etc/modprobe.d/modprobe.conf](#.2Fetc.2Fmodprobe.d.2Fmodprobe.conf)
        *   [2.9.6 /etc/resolv.conf (for Static IP)](#.2Fetc.2Fresolv.conf_.28for_Static_IP.29)
        *   [2.9.7 /etc/hosts](#.2Fetc.2Fhosts)
        *   [2.9.8 /etc/hosts.deny and /etc/hosts.allow](#.2Fetc.2Fhosts.deny_and_.2Fetc.2Fhosts.allow)
        *   [2.9.9 /etc/locale.gen](#.2Fetc.2Flocale.gen)
        *   [2.9.10 Pacman-Mirror](#Pacman-Mirror)
        *   [2.9.11 Root password](#Root_password)
    *   [2.10 Install and configure a bootloader](#Install_and_configure_a_bootloader)
        *   [2.10.1 For BIOS motherboards](#For_BIOS_motherboards)
            *   [2.10.1.1 Syslinux](#Syslinux)
            *   [2.10.1.2 GRUB](#GRUB)
        *   [2.10.2 For UEFI motherboards](#For_UEFI_motherboards)
            *   [2.10.2.1 Gummiboot](#Gummiboot)
            *   [2.10.2.2 GRUB](#GRUB_2)
    *   [2.11 Н: Перезавантаження](#.D0.9D:_.D0.9F.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.B2.D0.B0.D0.BD.D1.82.D0.B0.D0.B6.D0.B5.D0.BD.D0.BD.D1.8F)

## Передмова

##### Вступ

Вітаємо! Цей документ проведе вас через процес установки та налаштування [Arch Linux](/index.php/Arch_Linux "Arch Linux"), який є простий, гнучкий та легковажний дистрибутив GNU/Linux, <tt>UNIX</tt>-подібна операційна система для обізнаних користувачів.

*   Arch Linux потребує певного рівня углиблености знань про особливості його налаштування та про принципи роботи <tt>UNIX</tt>-подібних систем, тому в настанові надається додаткова роз’яснювальна інформація.
*   Ця інструкція призначена для нових користувачів Arch, але може використовуватися як довідкова та інформативна база.

**Особливості дистрибутиву Arch Linux:**

*   [Прості](/index.php/The_Arch_Way "The Arch Way") <tt>UNIX</tt>-подібний дизайн і філософія
*   Всі пакети зібрані для архітектур i686 та x86_64
*   [BSD-подібні](/index.php/Arch_boot_process "Arch boot process") сценарії завантаження, які включають централізований файл налаштувань
*   mkinitcpio: простий створювач initramfs
*   Пакетний менеджер [Pacman](/index.php/Pacman "Pacman"), легкий і швидкий, майже не потребує пам’яті
*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System") — схожа на ports система збирання пакетів, надає простий каркас для створення пакетів з сирцевого коду
*   Репозиторій [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") пропонує багато тисяч складених користувачами пакетів

##### Ліцензія

Arch Linux, pacman, документація та скрипти охороняються авторським правом (©2002-2007 by Judd Vinet, ©2007-2010 by Aaron Griffin) і ліцензовані під GNU General Public License Version 2.

##### ТІЛЬКИ БЕЗ ПАНІКИ!

Система Arch Linux збирається *користувачем* з командної оболонки за допомогою елементарних текстових команд. На відміну від непіддатливих структур інших дистрибутивів, тут немає ні пропонуємого оточення, ні заздалегідь обраної конфігурації. За допомогою командного рядка, *Ви* додаєте пакети з репозиторію за допомогою пакетного менеджера pacman і власноруч налаштуєте вашу систему через редагування текстових файлів аж доки ваша система не задовольнятиме вашим потребам. Також ви вручну створюватимете користувачів і керуватимете групами та правами користувачів. Цей метод дозволяє отримати максимум піддатливості, вибору і контролю можливостей вашої системою (*from the base up*).

Arch Linux — це дистрибутив для обізнаних користувачів GNU/Linux, що прагнуть зробити *все самостійно*.

##### Шлях Arch

***Принципи проектування Arch спрямовані на підтримання його простоти.***

"Простоту" системи у цьому контексті слід розуміти як "відсутність надмірних додатків, змін або ускладнень". По суті: елегантний, мінімалістичний підхід.

**Деякі думки щодо погляду на простоту:**

*   " Простота розглядається з технічної точки зору, а не з позиції зручності користувача. Краще бути технічно елегантним і заохочувати на пізнання, ніж бути легким у використанні, але абияким з технічного боку", — Аарон Ґрифін.
*   *Entia non sunt multiplicanda praeter necessitatem* або "Не слід множити сутності без необхідності", — принцип бритви Окама. Термін "бритва" посилається на процес обрізання непотрібних ускладнень для досягнення найпростішого пояснення, методу або теорії.
*   "Незвичайність [мого методу] полягає у простоті... Правильний розвиток завжди приводить до простоти", — Брюс Лі.

##### Про цю настанову

Хоча ця настанова охоплює більшість речей, які необхідні для встановлення та конфігурації Arch Linux, в ній неможливо розповісти про всі можливості та варіанти. [Вікі](/index.php/Main_page "Main page") Arch є прекрасним ресурсом; в разі виникнення питань спочатку пошукайте відповіді на ньому. IRC-канал (на freenode #archlinux) і [форум](https://bbs.archlinux.org/) допоможуть вам, якщо відповідь не вдалося знайти деінде.

**Note:** Чітке дотримання інструкцій необхідне для успішного встановлення та правильного налаштування Arch Linux, тому, *будь ласка*, читайте ретельно. Рекомендується прочитати кожну секцію повністю <u>перед</u> виконанням того, що там написано.

Оскільки дистрибутиви GNU/Linux є модульними за дизайном, ця настанова розділена на 4 основні частини:

**[Частина I: Встановлення базової системи](#.D0.A7.D0.B0.D1.81.D1.82.D0.B8.D0.BD.D0.B0_I:_.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_.D0.B1.D0.B0.D0.B7.D0.BE.D0.B2.D0.BE.D1.97_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B8)**

**[Частина II: Налаштування та оновлення базової системи](#Part_II:_Configure_.26_Update_the_New_Arch_Linux_base_system)**

**[Частина III: Встановлення X та налаштування ALSA](#Part_III:_Install_X_and_configure_ALSA)**

**[Частина IV: Встановлення та налаштування середовища стільниці](#Part_IV:_Installing_and_configuring_a_Desktop_Environment)**

## Частина I: Встановлення базової системи

### Крок 1: Отримання встановчого образу

Ви можете отримати офіційний образ [тут](https://archlinux.org/download/).

*   Образи Core та Netinstall містять лише найнеобхідніші пакети для встановлення **базової системи Arch Linux**. *Зауважте, що базова система не включає графічний інтерфейс користувача (GUI). Здебільшого образи містять з інструментів GNU (компілятор, асемблер, лінкер, бібліотеки, оболонку та утиліти), ядро Linux і кілька додаткових бібліотек та модулів.*
*   Образи Core придатні для встановлення як з CD, так і з Інтернету.
*   Образи Netinstall менші і не містять пакетів; все завантажуються скрізь Інтернет.
*   Образи isolinux можуть бути використані, якщо є проблеми з grub-версією. Більше нічим вони не відрізняються.
*   [Arch64 FAQ](/index.php/Arch64_FAQ "Arch64 FAQ") допоможе обрати між 32- і 64-бітною версіями.

#### Встановлення з CD

Запишіть .iso образ на CD за допомогою вашої улюбленої програми запису компакт-дисків і переходьте до [Кроку 2: Завантаження інсталятора Linux](#.D0.9A.D1.80.D0.BE.D0.BA_2:_.D0.97.D0.B0.D0.B2.D0.B0.D0.BD.D1.82.D0.B0.D0.B6.D0.B5.D0.BD.D0.BD.D1.8F_.D1.96.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D1.8F.D1.82.D0.BE.D1.80.D0.B0_Linux)

**Note:** Якість як компакт-дисків, так і пристроїв їх запису може сильно різнитись. Взагалі, для надійного запису рекомендується записувати диски на невеликій швидкості. Деякі користувачі рекомендують дуже низьку швидкість запису ***4x або 2x.*** Якщо ви стикаєтесь з проблемами під час встановлення, пов’язаними з компакт-диском, спробуйте записати диск на мінімальній швидкості, яка підтримується вашою системою.

#### USB-флешка

**Warning:** Всі файли на вашому USB-носії буде невідворотно знищено!

**<tt>UNIX</tt>-овий метод:**

Підключіть чисту флешку, визначте шлях до неї і запишіть образ .img за допомогою програми `/bin/dd`:

```
dd if=archlinux-2009.08-*{core|netinstall}*-*{i686|x86_64}*.img of=/dev/sd*x*

```

де `if=` — це шлях до файла образу і `of=` — це ваш USB-носій. Переконайтесь, що ім’я носія `/dev/sd**x**`, а не `/dev/sd**x1**`. Вам знадобиться USB-носій розміру, достатнього для запису образу, який на момент написання цієї настанови становить 381MB. Таким чином, вистачить пристрою на 512MB.

**Перевірка md5sum:**

Занотуйте кількість записів (блоків), які були прочитані та записані, і потім виконайте наступну перевірку:

```
dd if=/dev/sd*x* count=*кількість_блоків* status=noxfer | md5sum

```

Отримане значення md5sum повинне співпадати зі значенням md5sum образу, яке, в свою чергу, повинно дорівнювати значенню, записаному у файлі md5sums.txt з сайту, звідки ви отримали образ. Типовий запис і перевірка виглядають наступним чином:

```
$ [sudo] dd if=archlinux-2009.08-core-i686.img of=/dev/sdc
744973+0 records in
744973+0 records out
381426176 bytes (381 MB) copied, 106.611 s, 3.6 MB/s
$ [sudo] dd if=/dev/sdc count=744973 status=noxfer | md5sum
4850d533ddd343b80507543536258229  -
744973+0 records in
744973+0 records out

```

**Windows-метод:**

Завантажте програму Disk Imager за адресою [https://launchpad.net/win32-image-writer/+download](https://launchpad.net/win32-image-writer/+download). Вставте USB-носій. Запустіть Disk Imager і виберіть файл образу. Виберіть букву-ідентифікатор, яка відповідає USB-носію. Натисність на кнопку "Write".

Переходьте до [Кроку 2: Завантаження інсталятора Linux](#.D0.9A.D1.80.D0.BE.D0.BA_2:_.D0.97.D0.B0.D0.B2.D0.B0.D0.BD.D1.82.D0.B0.D0.B6.D0.B5.D0.BD.D0.BD.D1.8F_.D1.96.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D1.8F.D1.82.D0.BE.D1.80.D0.B0_Linux)

### Крок 2: Завантаження інсталятора Linux

Вставте компакт-диск або USB-носій з інсталяційним образом і завантажтеся з нього. Для цього вам, можливо, знадобиться змінити порядок завантаження у BIOS вашого комп’ютера таким чином, щоб носій з образом був першим у списку пристроїв, з яких відбувається завантаження. Для того, щоб зайти в меню налаштування BIOS, натисніть клавішу (зазвичай DEL, F1, F2, F11 або F12) після включення живлення комп’ютера (протягом фази BIOS POST (Power On Self-Test)).

**Tip:** Вимоги до пам’яті для базового встановлення:

*   Core : 128 MB RAM x86_64/i686 (вибрані всі пакети, з розділом підкачки (свопом))
*   Netinstall : 128 MB RAM x86_64/i686 (вибрані всі пакети, з розділом підкачки (свопом))

Після завантаження з носія повинне з’явитися головне меню. Оберіть бажаний варіант завантаження за допомогою клавіш зі стрілками і натисніть Enter.

Зазвичай найкращим вибором буде перший пункт меню, Boot Archlive. Проте якщо у вас є проблеми з libata/PATA, або у вас немає SATA (Serial ATA) приводів, оберіть пункт Boot Archlive [legacy IDE].

Для зміни опцій GRUB натисність **e**. Багато користувачів захочуть змінити роздільну здатність кадорового буфера (фреймбуфера) для кращого консольного виведення. Додайте

```
vga=773

```

до рядка опцій ядра для одержання роздільної здатності фреймбуфера 1024x768\. Натисність Enter для збереження змін. Коли закінчите, натисність **b** для завантаження системи з обраними параметрами.

Після завантаження системи з’явиться запрошення для входу. Увійдіть під іменем користувача *root*.

Якщо виникнуть проблеми при завантаженні з компакт-диска або інші проблеми з **обладнанням**, зверніться до сторінки [Installation Troubleshooting](/index.php?title=Installation_Troubleshooting&action=edit&redlink=1 "Installation Troubleshooting (page does not exist)").

#### Зміна розкладки клавіатури

Якщо у вас не US розкладка клавіатури, ви можете обрати вашу розкладку або шрифт у консолі за допомогою команди

```
# km

```

або використати команду loadkeys:

```
# loadkeys *layout*

```

(замініть *layout* вашою розкладкою клавіатури, наприклад "`fr`" або "`be-latin1`").

#### Документація

Офіційна настанова зі встановлення доступна прямо в live-системі! Щоб відкрити її, перейдіть до vc/2 (віртуальна консоль #2), натиснувши <ALT>+F2, і потім виконайте наступну команду:

```
# less /arch/docs/official_installation_guide_en

```

`less` дозволить вам пересуватися документом. Перейдіть до vc/1, натиснувши <ALT>+F1, для продовження встановлення.

Для отримання інформації з офіційної настанови передіть до vc/2 в будь-який момент процесу встановлення.

**Tip:** Зауважте, що офіційна настанова описує встановлення і налаштування базової системи. Після її встановлення рекомендується продовжити вивчення цього документа для отримання докладної інформації про подальше налаштування системи та інші пов’язані питання.

### Крок 3: Початок інсталяції

Від імені рута запустіть інсталяційний скрипт з vc/1:

```
# /arch/setup

```

### А: Вибір джерела для інсталяції

Після вікна з привітанням ви маєте вибрати джерело інсталяції. Виберіть відповідне джерело.

*   Якщо ви користуєтсь образом CORE, продовжіть роботу з пункту [Б: Налаштування годинника](#.D0.91:_.D0.9D.D0.B0.D0.BB.D0.B0.D1.88.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D0.B3.D0.BE.D0.B4.D0.B8.D0.BD.D0.BD.D0.B8.D0.BA.D0.B0).
*   Користувачам образу Netinstall інсталятор, при бажанні, допоможе завантажити драйвери Ethernet в ручному режимі. Udev досить ефективно завантажує необхідні модулі автоматично, тому скоріш за все нічого робити не треба. Ви можете перевірити це викликавши ifconfig -a з vc/3 (Select OK to continue.)

#### Конфігурування мережі (Netinstall)

Будуть показані доступні інтерфейси. Якщо виведено інтерфейс і HWaddr (**H**ard**W**are **addr**ess) значить потрібний модуль був успішно завантажений. Якщо цього не сталося, ви можете підключити їх з допомогою інсталятора або зробити це вручну з іншої віртуальної консолі.

Наступний екран запропонує *Select the interface, Probe,* or *Cancel*. Виберіть потрібний інтерфейс і продовжуйте далі.

Далі інсталятор запропонує запустити DHCP. Вибір варіанту *Так* запустить **dhcpcd**, щоб виявити доступний мережевий шлюз і запросити IP адресу. Вибравши *Ні* інсталятор запитає вас про статичну IP-адресу, мережеву маску, широкомовну адресу, мережевий шлюз, DNS, адресу HTTP та FTP проксі серверів. І нарешті інсталятор покаже введені вами дані для останньої перевірки.

##### (A)DSL Quickstart for the Live Environment (If you have a pure modem (or router in bridge mode) to connect to your ISP)

Switch to another virtual console (<Alt> + F2), login as root and invoke

```
# pppoe-setup

```

If everything is well configured in the end you can connect to your ISP with

```
# pppoe-start

```

Return to first virtual console with <ALT>+F1\. Continue with [B: Set Clock](#B:_Set_Clock)

##### Wireless Quickstart For the Live Environment (If you need wireless connectivity during the installation process)

The wireless drivers and utilities are now available to you in the live environment of the installation media. A good knowledge of your wireless hardware will be of key importance to successful configuration. Note that the following quickstart procedure *executed at this point in the installation* will initialize your wireless hardware for use *in the live environment*. These steps (or some other form of wireless management) must be repeated from the actual installed system after booting into it.

Also note that these steps are optional if wireless connectivity is unnecessary at this point in the installation; wireless functionality may always be established later.

The basic procedure will be:

*   Switch to a free virtual console, e.g.: <ALT>+F3
*   (Optional) Identify the wireless interface and driver module:

```
# lsmod | grep -i net

```

*   Ensure udev has loaded the driver, and that the driver has created a usable wireless kernel interface with `/usr/sbin/iwconfig`:

```
# iwconfig

```

Example output:

```
lo no wireless extensions.
eth0 no wireless extensions.
wlan0    unassociated  ESSID:""
         Mode:Managed  Channel=0  Access Point: Not-Associated   
         Bit Rate:0 kb/s   Tx-Power=20 dBm   Sensitivity=8/0  
         Retry limit:7   RTS thr:off   Fragment thr:off
         Power Management:off
         Link Quality:0  Signal level:0  Noise level:0
         Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
         Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

`wlan0` is the available wireless interface in the example.

*   Bring the interface up with `/sbin/ifconfig <interface> up`.

An example using the wlan0 interface:

```
# ifconfig wlan0 up

```

(Remember, your interface may be named something else, depending on your module (driver) and chipset: wlan0, eth1, etc.)

*   If the essid has been forgotten or is unknown, use `/sbin/iwlist <interface> scan` to scan for nearby networks.

```
# iwlist wlan0 scan

```

*   Specify the id of the chosen wireless network with iwconfig <interface> essid "<youressid>" key <your_wep_key> (give the essid (the 'network name') of the network in quotes).
*   An example using WEP and a hexadecimal key:

```
# iwconfig wlan0 essid "linksys" key 0241baf34c

```

*   An example using WEP and an ASCII passphrase:

```
# iwconfig wlan0 essid "linksys" key s:pass1

```

*   An example using an unsecured network:

```
# iwconfig wlan0 essid "linksys"

```

*   Request an IP address with `/sbin/dhcpcd <interface>` . e.g.:

```
# dhcpcd wlan0

```

*   Ensure you can route using `/bin/ping`:

```
# ping -c 3 www.google.com

```

Done.

*   For connecting to a network using WPA, consult the [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant") article, and continue below.

###### Does the Wireless Chipset require Firmware?

A small percentage of wireless chipsets also require firmware, in addition to a corresponding driver. If unsure, invoke `/usr/bin/dmesg` to query the kernel log for a firmware request from the wireless chipset:

```
# dmesg | grep firmware

```

Example output from an Intel chipset which requires and has requested firmware from the kernel at boot:

```
firmware: requesting iwlwifi-5000-1.ucode

```

If there is no output, it may be concluded that the system's wireless chipset does not require firmware.

**Note:** **Wireless chipset firmware packages (for cards which require them) are pre-installed under /lib/firmware in the live environment, (on CD/USB stick) *but must be explicitly installed to your actual system to provide wireless functionality after you reboot into it!* Package selection and installation is covered below. Ensure installation of both your wireless module and firmware during the package selection step! See [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") if you are unsure about the requirement of corresponding firmware installation for your particular chipset. This is a very common error.**

After the initial Arch installation is complete, you may wish to refer to [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") to ensure a permanent configuration solution for your installed system.

Return to vc/1 with <ALT>+F1\. Continue with [B: Set Clock](#B:_Set_Clock)

### Б: Налаштування годинника

*   UTC - виберіть UTC якщо на комп’ютері встановлені тільки <tt>UNIX</tt>-подібні операційна(і) система(и).

*   localtime - виберіть цей пункт при мультизавантаженні із Microsoft Windows OS.

### В: Підготовка твердого диску

**Warning:** Операції з партиціями твердого диску можуть знищити дані на ньому. Рекомендується бути надзвичайно обережним і зробити резервну копію важливих даних.

**Note:** Розбивка твердого диску, при бажанні, може бути виконана до початку встановлення Arch з допомогою [GParted](http://gparted.sourceforge.net/download.php) або інших подібних засобів. Якщо диск для встановлення системи уже підготовлений, можна продовжувати з пункту [Налаштування точок монтування файлових систем](#.D0.9D.D0.B0.D0.BB.D0.B0.D1.88.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D1.82.D0.BE.D1.87.D0.BE.D0.BA_.D0.BC.D0.BE.D0.BD.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.B8.D1.85_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC)

Перегляньте інформацію про диск(и), викликом команди `/sbin/fdisk`.

Відкрийте іншу віртуальну консоль та напишіть:

```
# fdisk -l

```

Отриману про диск(и) і партицію(ї) інформацію візьміть до уваги.

Поверніться назад до інсталяційного скрипта натиснувши <ALT>+F1

Виберіть перший пункт "Prepare Hard Drive".

*   1 варіант: Автоматична підготовка

Автоматично розбиває диск за такою конфігурацією:

*   *   ext2 /boot розділ із розміром за замовчуванням 32MB. *Ви можете змінити запропонований розмір.*
    *   Розділ swap з розміром за замовчуванням 256MB. *Ви також можете змінити це значення.*
    *   Окремі розділи кореневої файлової системи і файлової системи для домашньої директорії: / і /home. Можна задати значення їхніх розмірів. Підтримуються вибір файлових систем ext2, ext3, ext4, reiserfs, xfs, jfs, але обидва розділи будуть відформатовані в однаковій файловій системі (при використанні автоматичної підготовки).

Добре пам’ятайте, що автоматична підготовка стре весь твердий диск. Уважно читайте повідомлення інсталятора. Перевірте, що ви вибрали саме той твердий диск (якщо їх у вас кілька).

*   2 варіант: **(рекомендовано)** Ручна підготовка з використанням cfdisk

Найнадійніша і найбільш придатна для ваших потреб розбивка робиться саме цим варіантом.

*At this point, more advanced GNU/Linux users who are familiar and comfortable with manually partitioning may wish to skip down to **[D: Select Packages](#D:_Select_Packages)** below.*

**Note:** Для користувачів, які встановлюють Arch на USB-флешку написано окрему статтю "[Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key")".

#### Розбивка твердих дисків

##### Інформація про розбивку

Розбивка твердого диску полягає у створенні на ньому спеціальних областей (розділів), які функціонують як окремі диски зі своїми файловими системами. Розділи бувають:

1.  основні
2.  розширені
3.  логічні

**Основні** розділи можуть бути завантажувальними і їх може бути не більше чотирьох на диск чи на масив RAID. Якщо схема розбивки потребує більше, використовують **розширені** розділи, які містять у собі **логічні**.

Розширені розділи не використовуються самі по собі — це просто вмістилища для логічних розділів. Якщо потрібно, твердий диск може мати лише один розширений розділ, який, на своєму рівні абстракції, розбитий на логічні розділи.

При розбивці диску можна помітити схему нумерації. Основні розділи називаються sda1, sda2, sda3\. За ними розширений розділ sda4 і логічні розділи sda5, sd6 і т. д.

##### Розділ підкачки (swap)

Розділ підкачки — це місце на твердому диску, куди операційна система записує дані оперативної пам’яті, якщо вони не поміщаються або не придатні для зберігання на фізичному пристрої оперативної пам’яті.

Історично склалося правило, що розділ підкачки має бути удвічі більшим за ємність фізичної оперативної пам’яті. Пізніше розвиток комп’ютерної техніки призвів до збільшення обсягів пам’яті і це правило не завжди можна ефективно застосовувати. Загалом на машинах із розміром оперативної пам’яті до 512MB це правило найчастіше ще має сенс. Якщо на машині встановлено 1GB оперативної пам’яті чи більше, можна встановити розмір розділу підкачки рівним розміру оперативної пам’яті або не створювати його зовсім, тим більш, що пізніше (після завершення інсталяції) можна створити *файл* підкачки ([swap file](/index.php/HOW_TO:_Create_swap_file "HOW TO: Create swap file")). A 1 GB swap partition will be used in this example.

**Note:** Якщо ви будете використовувати технології suspend-to-disk чи hibernate, розділ підкачки повинен як мінімум бути рівним розміру фізичної оперативної пам’яті. Деякі користувачі Arch рекомендують задати розмір на 10–15% більший, щоб врахувати можливість появи на диску битих секторів.

##### Схема розбивки

Схеми розбивки диска досить різняться від одного користувача до іншого в залежності від його потреб і звичок. При мультизавантаженні Arch і Windows, може допомогти стаття [Windows and Arch Dual Boot](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot").

Часто в окремі файлові системи виокремлюють такі директорії:

**/** (корінь) *Коренева файлова система — єдина обов’язкова файлова система, перша в ієрархії, на яку монтуються решта. Всі файли і директорії операційної системи містить коренева директорія "/", навіть якщо вони розміщені на різних фізичних пристроях. Вміст кореневої файлової системи при потребі має адекватно завантажити і відновити працездатність системи. Тому певні директорії у / не є кандидатами на окремий розділ.*

**/boot** *Ця директорія містить ядро, образ ramdisk, завантажувальник, його конфігураційні файли, дані, які використовуються до того, як ядро почне виконувати програми простору користувача.*

**/home** *Дані користувачів, а також конфігураційні файли програм, специфічні для кожного окремого користувача.*

**/usr** *While root is the primary filesystem, /usr is the secondary hierarchy, for user data, containing the majority of (multi-)user utilities and applications. /usr is shareable, read-only data. This means that /usr shall be shareable between various hosts and must not be written to, except in the case of system update/upgrade. Any information that is host-specific or varies with time is stored elsewhere.*

**/tmp** *directory for programs that require temporary files such as '.lck' files, which can be used to prevent multiple instances of their respective program until a task is completed, at which point the '.lck' file will be removed. Programs must not assume that any files or directories in /tmp are preserved between invocations of the program and files and directories located under /tmp will typically be deleted whenever the system is booted.*

**/var** *contains variable data; spool directories and files, administrative and logging data, pacman's cache, the ABS tree, etc. /var exists in order to make it possible to mount /usr as read-only. Everything that historically went into /usr that is written to during system operation (as opposed to installation and software maintenance) must be under /var.*

**Warning:** Besides /boot, directories essential for booting are: '***/bin', '/dev', '/etc', '/lib', '/proc' and '/sbin'. Therefore, they must not reside on a separate partition from /.***

***There are several advantages for using discrete filesystems, rather than combining all into one partition***:

*   Security: Each filesystem may be configured in /etc/fstab as 'nosuid', 'nodev', 'noexec', 'readonly', etc.
*   Stability: A user, or malfunctioning program can completely fill a filesystem with garbage if they have write permissions for it. Critical programs, which reside on a different filesystem remain unaffected.
*   Speed: A filesystem which gets written to frequently may become somewhat fragmented. (An effective method of avoiding fragmentation is to ensure that each filesystem is never in danger of filling up completely.) Separate filesystems remain unaffected, and each can be defragmented separately as well.
*   Integrity: If one filesystem becomes corrupted, separate filesystems remain unaffected.
*   Versatility: Sharing data across several systems becomes more expedient when independent filesystems are used. Separate filesystem types may also be chosen based upon the nature of data and usage.

In this example, we shall use separate partitions for /, /var, /home, and a swap partition.

**Note:** /var contains many small files. This should be taken into consideration when choosing a filesystem type for it, (if creating its own separate partition).

##### How big should my partitions be?

This question is best answered based upon individual needs. You may wish to simply create **one partition for root and one partition for swap or only one root partition without swap** or refer to the following examples and consider these guidelines to provide a frame of reference:

*   The root filesystem (/) in the example will contain the /usr directory, which can become moderately large, depending upon how much software is installed. 15-20 GB should be sufficient for most users.

*   The /var filesystem will contain, among other data, the [ABS](/index.php/ABS "ABS") tree and the pacman cache. Keeping cached packages is useful and versatile; it provides the ability to downgrade packages if needed. /var tends to grow in size; the pacman cache can grow large over long periods of time, but can be safely cleared if needed. If you are using an SSD, you may wish to locate your /var on an HDD and keep the / and /home partitions on your SSD to avoid needless read/writes to the SSD. 6-8 Gigs on a desktop system should be sufficient for /var. Servers tend to have extremely large /var filesystems.

*   The /home filesystem is typically where user data, downloads, and multimedia reside. On a desktop system, /home is typically the largest filesystem on the drive by a large margin. Remember that if you chose to reinstall Arch, all the data on your /home partition will be untouched (so long as you have a separate /home partition).

*   An extra 25% of space added to each filesystem will provide a cushion for unforeseen occurrence, expansion, and serve as a preventive against fragmentation.

***From the guidelines above, the example system shall contain a ~15GB root (/) partition, ~7GB /var, 1GB swap, and a /home containing the remaining disk space.***

##### Create Partition:cfdisk

Start by creating the primary partition that will contain the **root**, (/) filesystem.

Choose **N**ew -> Primary and enter the desired size for root (/). Put the partition at the beginning of the disk.

Also choose the **T**ype by designating it as '83 Linux'. The created / partition shall appear as sda1 in our example.

Now create a primary partition for /var, designating it as **T**ype 83 Linux. The created /var partition shall appear as sda2

Next, create a partition for swap. Select an appropriate size and specify the **T**ype as 82 (Linux swap / Solaris). The created swap partition shall appear as sda3.

Lastly, create a partition for your /home directory. Choose another primary partition and set the desired size.

Likewise, select the **T**ype as 83 Linux. The created /home partition shall appear as sda4.

Example:

```
Name    Flags     Part Type    FS Type           [Label]         Size (MB)
-------------------------------------------------------------------------
sda1               Primary     Linux                             15440 #root
sda2               Primary     Linux                             6256  #/var
sda3               Primary     Linux swap / Solaris              1024  #swap
sda4               Primary     Linux                             140480 #/home

```

Choose **W**rite and type '**yes'**. Beware that this operation may destroy data on your disk. Choose **Q**uit to leave the partitioner. Choose Done to leave this menu and continue with "Set Filesystem Mountpoints".

**Note:** Since the latest developments of the Linux kernel which include the libata and PATA modules, all IDE, SATA and SCSI drives have adopted the sd*x* naming scheme. This is perfectly normal and should not be a concern.

#### Налаштування точок монтування файлових систем

First you will be asked for your swap partition. Choose the appropriate partition (sda3 in this example). You will be asked if you want to create a swap filesystem; select yes. Next, choose where to mount the / (root) directory (sda1 in the example). At this time, you will be asked to specify the filesystem type.

##### Filesystem Types

Again, a filesystem type is a very subjective matter which comes down to personal preference. Each has its own advantages, disadvantages, and unique idiosyncrasies. Here is a very brief overview of supported filesystems:

1\. **ext2** *Second Extended Filesystem*- Old, reliable GNU/Linux filesystem. Very stable, but *without journaling support*. May be inconvenient for root (/) and /home, due to very long fsck's. *An ext2 filesystem can easily be converted to ext3.* Generally regarded as a good choice for /boot/.

2\. **ext3** *Third Extended Filesystem*- Essentially the ext2 system, but with journaling support. ext3 is completely compatible with ext2\. *Extremely* stable, mature, and by far the most widely used, supported and developed GNU/Linux FS.

**High Performance Filesystems:**

3\. **ext4** *Fourth Extended Filesystem*- Backward compatible with ext2 and ext3, Introduces support for volumes with sizes up to 1 exabyte and files with sizes up to 16 terabyte. Increases the 32,000 subdirectory limit in ext3 to 64,000\. Offers online defragmentation ability.

**Note:** ext4 is a new filesystem and may have some bugs.

4\. **ReiserFS** (V3)- Hans Reiser's high-performance journaling FS uses a very interesting method of data throughput based on an unconventional and creative algorithm. ReiserFS is touted as very fast, especially when dealing with many small files. ReiserFS is fast at formatting, yet comparatively slow at mounting. Quite mature and stable. ReiserFS is not actively developed at this time (Reiser4 is the new Reiser filesystem). Generally regarded as a good choice for /var/.

5\. **JFS** - IBM's **J**ournaled **F**ile**S**ystem- The first filesystem to offer journaling. JFS had many years of use in the IBM AIX® OS before being ported to Linux. JFS currently uses the least CPU resources of any GNU/Linux filesystem. Very fast at formatting, mounting and fsck's, and very good all-around performance, especially in conjunction with the deadline I/O scheduler. (See [JFS](/index.php/JFS "JFS").) Not as widely supported as ext or ReiserFS, but very mature and stable.

6\. **XFS** - Another early journaling filesystem originally developed by Silicon Graphics for the IRIX OS and ported to Linux. XFS offers very fast throughput on large files and large filesystems. Very fast at formatting and mounting. Generally benchmarked as slower with many small files, in comparison to other filesystems. XFS is very mature and offers online defragmentation ability.

*   JFS and XFS filesystems cannot be *shrunk* by disk utilities (such as gparted or parted magic)

##### A note on Journaling

All above filesystems, except ext2, utilize [journaling](https://en.wikipedia.org/wiki/Journaling_file_system "wikipedia:Journaling file system"). Journaling file systems are fault-resilient file systems that use a journal to log changes before they are committed to the file system to avoid metadata corruption in the event of a crash. Note that not all journaling techniques are alike; specifically, only ext3 and ext4 offer *data-mode journaling*, (though, not by default), which journals *both* data *and* meta-data (but with a significant speed penalty). The others only offer *ordered-mode journaling*, which journals meta-data only. While all will return your filesystem to a valid state after recovering from a crash, *data-mode journaling* offers the greatest protection against file system corruption and data loss but can suffer from performance degradation, as all data is written twice (first to the journal, then to the disk). Depending upon how important your data is, this may be a consideration in choosing your filesystem type.

***Moving on...***

Choose and create the filesystem (format the partition) for / by selecting **yes**. You will now be prompted to add any additional partitions. In our example, sda2 and sda4 remain. For sda2, choose a filesystem type and mount it as /var. Finally, choose the filesystem type for sda4, and mount it as /home.

**Note:** If you have not created and do not need a separate /boot partition, you may safely ignore the warning that it does not exist.
Return to the main menu.

### D: Select Packages

*   Core ISO: Choose CD as source and select the appropriate CD drive if more than one exist on the installation machine.
*   Netinstall: Select an FTP/HTTP mirror. *Note that archlinux.org is throttled to 50KB/s*.
*   All packages during installation are from the [core] repository. They are further divided into **Base**, and **Base-devel**.
*   Package information and brief descriptions are available [here](https://www.archlinux.org/packages/?repo=Core&arch=i686&limit=all&sort=pkgname).

Package selection is split into two stages. First, select the package category:

**Note:** For expedience, all packages in **base** are selected by default. Use the space-bar to select and de-select packages.

*   **Base**: Packages from the [core] repo to provide the minimal base environment. *Always select it and only remove packages that will not be used.*
*   **Base-devel**: Extra tools from [core] such as **make**, and **automake**. *Most beginners should choose to install it, and will probably need it later.*
*   **Other packages**: Important choices include **wireless_tools**, **ndiswrapper** and **openssh**.

After category selection, you will be presented with the full lists of packages, allowing you to fine-tune your selections. Use the space bar to select and unselect.

**Note:** If you are going to require connection to a wireless network, install wireless_tools. If you plan to use WPA encryption, consider installing netcfg2, which will enable you to do so.

After selecting the needed packages, leave the selection screen and continue to the next step, Install Packages.

### E: Install Packages

Next, choose 'Install Packages'. You will be asked if you wish to keep the packages in the pacman cache. If you choose 'yes', you will have the flexibility to [downgrade](/index.php/Downgrade_packages "Downgrade packages") to previous package versions in the future, so this is recommended (you can always clear the cache in the future). The installer script will now install the selected packages, as well as the default Arch 2.6 kernel, to your system.

*   Netinstall: The [Pacman](/index.php/Pacman "Pacman") package manager will now download and install your selected packages. (See vc/5 for output, vc/1 to return to the installer)
*   Core image: The packages will be installed from the CD/USB stick.

### F: Configure the System

*Closely following and understanding these steps is of key importance to ensure a properly configured system.*

*   At this stage of the installation, you will configure the primary configuration files of your Arch Linux base system.

*   Previous versions of the installer included [hwdetect](/index.php/Hwdetect "Hwdetect") to gather information for your configuration. This has been deprecated, and **[udev](/index.php/Udev "Udev")** should handle most module loading automatically at boot.

Now you will be asked which text editor you want to use; choose [nano](/index.php/Nano "Nano"), [joe](http://joe-editor.sourceforge.net/) or [vi](/index.php/Vim "Vim"), (**nano** is generally considered easiest of the 3). You will be presented with a menu including the main configuration files for your system.

**Note:** *It is very important at this point to edit, or at least verify by opening, every configuration file.* The installer script relies on your input to create these files on your installation. A common error is to skip over these critical steps of configuration.

##### Can the installer handle this more automatically?

Hiding the process of system configuration is in direct opposition to ***[The Arch Way](/index.php/The_Arch_Way "The Arch Way")***. While it is true that recent versions of the kernel and hardware probing tools offer excellent hardware support and auto-configuration, Arch presents the user all pertinent configuration files during installation for the purposes of *transparency and system resource control*. By the time you have finished modifying these files to your specifications, you will have learned the simple method of manual Arch Linux system configuration and become more familiar with the base structure, leaving you better prepared to use and maintain your new installation productively.

***Moving on...***

#### /etc/rc.conf

Arch Linux uses the file `/etc/rc.conf` as the principal location for system configuration. This one file contains a wide range of configuration information, principally used at system startup. As its name directly implies, it also contains settings for and invokes the /etc/rc* files, and is, of course, sourced *by* these files.

##### LOCALIZATION section

*   **LOCALE**=: This sets your system locale, which will be used by all i18n-aware applications and utilities. You can get a list of the available locales by running `locale -a` from the command line. This setting's default is fine for US English users.
*   **HARDWARECLOCK**=: Specifies whether the hardware clock, which is synchronized on boot and on shutdown, stores **UTC** time, or **localtime**. UTC makes sense because it greatly simplifies changing timezones and daylight savings time. localtime is necessary if you dual boot with an operating system such as Windows, that only stores localtime to the hardware clock.
*   **USEDIRECTISA**=: Use direct I/O request instead of `/dev/rtc` for hwclock
*   **TIMEZONE**=: Specify your TIMEZONE. (All available zones are under `/usr/share/zoneinfo/`).
*   **KEYMAP**=: The available keymaps are in `/usr/share/kbd/keymaps`. Please note that this setting is only valid for your TTYs, not any graphical window managers or **X**.
*   **CONSOLEFONT**=: Available console fonts reside under `/usr/share/kbd/consolefonts/` if you must change. The default (blank) is safe.
*   **CONSOLEMAP**=: Defines the console map to load with the setfont program at boot. Possible maps are found in `/usr/share/kbd/consoletrans`, if needed. The default (blank) is safe.
*   **USECOLOR**=: Select "yes" if you have a color monitor and wish to have colors in your consoles.

```
LOCALE="en_US.utf8"
HARDWARECLOCK="localtime"
USEDIRECTISA="no"
TIMEZONE="US/Eastern"
KEYMAP="us"
CONSOLEFONT=
CONSOLEMAP=
USECOLOR="yes"

```

##### HARDWARE Section

*   **MOD_AUTOLOAD**=: Setting this to "yes" will use **udev** to automatically probe hardware and load the appropriate modules during boot, (convenient with the default modular kernel). Setting this to "no" will rely on the user's ability to specify this information manually, or compile their own custom kernel and modules, etc.
*   **MOD_BLACKLIST**=: This has become deprecated in favor of adding blacklisted modules directly to the **MODULES=** line below.
*   **MODULES**=: Specify additional MODULES if you know that an important module is missing. If your system has any floppy drives, add "floppy". If you will be using loopback filesystems, add "loop". Also specify any blacklisted modules by prefixing them with a bang (!). Udev will be forced NOT to load blacklisted modules. In the example, the IPv6 module as well as the annoying pcspeaker are blacklisted.

```
# Scan hardware and load required modules at boot
MOD_AUTOLOAD="yes"
# Module Blacklist - Deprecated
MOD_BLACKLIST=()
#
MODULES=(!net-pf-10 !snd_pcsp !pcspkr loop)

```

##### NETWORKING Section

*   **HOSTNAME**=:Set your HOSTNAME to your liking.
*   **eth0**=: 'Ethernet, card 0'. Adjust the interface IP address, netmask and broadcast address *if* you are using **static IP**. Set eth0="dhcp" if you want to use **DHCP**
*   **INTERFACES**=: Specify all interfaces here. Multiple interfaces should be separated with a space as in:

```
(eth0 wlan0)

```

*   **gateway**=: If you are using **static IP**, set the gateway address. If using **DHCP**, you can usually ignore this variable, though some users have reported the need to define it.
*   **ROUTES**=: If you are using static **IP**, remove the **!** in front of 'gateway'. If using **DHCP**, you can usually leave this variable commented out with the bang (!), but again, some users require the gateway and ROUTES defined. If you experience networking issues with pacman, for instance, you may want to return to these variables.

###### Example, using a dynamically assigned IP address (**DHCP**)

```
HOSTNAME="arch"
#eth0="eth0 192.168.0.2 netmask 255.255.255.0 broadcast 192.168.0.255"
eth0="dhcp"
INTERFACES=(eth0)
gateway="default gw 192.168.0.1"
ROUTES=(!gateway)

```

###### Example, using a **static** IP address

```
HOSTNAME="arch"
eth0="eth0 192.168.0.2 netmask 255.255.255.0 broadcast 192.168.0.255"
INTERFACES=(eth0)
gateway="default gw 192.168.0.1"
ROUTES=(gateway)

```

Modify `/etc/resolv.conf` to contain the DNS servers of choice. Example:

```
search my.isp.net.
nameserver 4.2.2.1
nameserver 4.2.2.2
nameserver 4.2.2.3

```

Various processes can overwrite the contents of `/etc/resolv.conf`. For example, by default Arch Linux uses the **dhcpcd** DHCP client, which will overwrite the file when it starts. [Various methods](/index.php/Resolv.conf "Resolv.conf") may be used to preserve the nameserver settings in `/etc/resolv.conf`. For example, dhcpcd's configurations file may be edited to prevent the dhcpcd daemon from overwriting the file. To do this, you will need to modify the `/etc/conf.d/dhcpcd` configuration:

```
# Arguments to be passed to the DHCP client daemon
# DHCPCD_ARGS="-q"
DHCPCD_ARGS="-C resolv.conf -q"

```

**Tip:** If using a non-standard MTU size (a.k.a. jumbo frames) is desired AND the installation machine hardware supports them, see the [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames") wiki article for further configuration.

##### DAEMONS Section

This array simply lists the names of those scripts contained in /etc/rc.d/ which are to be started during the boot process, and the order in which they start. Asynchronous initialization by backgrounding is also supported and useful for speeding up boot.

```
DAEMONS=(network @syslog-ng netfs @crond)

```

*   If a script name is prefixed with a bang (!), it is not executed.
*   If a script is prefixed with an "at" symbol (@), it shall be executed in the background; the startup sequence will not wait for successful completion of each daemon before continuing to the next. (Useful for speeding up system boot). Do not background daemons that are needed by other daemons. For example "mpd" depends on "network", therefore backgrounding network may cause mpd to break.
*   Edit this array whenever new system services are installed, if starting them automatically during boot is desired.

**Note:** This 'BSD-style' init, is the Arch way of handling what other distributions handle with various symlinks to an /etc/init.d directory.

###### About DAEMONS

The [daemons](/index.php/Daemons "Daemons") line need not be changed at this time, but it is useful to explain what daemons are, as they will be addressed later in this guide. A *daemon* is a program that runs in the background, waiting for events to occur and offering services. A good example is a webserver that waits for a request to deliver a page (e.g.:httpd) or an SSH server waiting for a user login (e.g.:sshd). While these are full-featured applications, there are also daemons whose work is not that visible. Examples are a daemon which writes messages into a log file (e.g. syslog, metalog), a daemon which lowers the CPU frequency if the system has nothing to do (e.g.:cpufreq), and a daemon which provides a graphical login (e.g.: gdm, kdm). All these programs can be added to the daemons line and will be started when the system boots. Useful daemons will be presented during this guide.

Historically, the term *daemon* was coined by the programmers of MIT's Project MAC. They took the name from *Maxwell's demon*, an imaginary being from a famous thought experiment that constantly works in the background, sorting molecules. <tt>UNIX</tt> systems inherited this terminology and created the backronym **d**isk **a**nd **e**xecution **mon**itor.

**Tip:** All Arch daemons reside under /etc/rc.d/

#### /etc/fstab

The **fstab** (for **f**ile **s**ystems **tab**le) is part of the system configuration listing all available disks and disk partitions, and indicating how they are to be initialized or otherwise integrated into the overall system's filesystem. The **/etc/fstab** file is most commonly used by the **mount** command. The mount command takes a filesystem on a device, and adds it to the main system hierarchy that you see when you use your system. **mount -a** is called from /etc/rc.sysinit, about 3/4 of the way through the boot process, and reads /etc/fstab to determine which options should be used when mounting the specified devices therein. If **noauto** is appended to a filesystem in /etc/fstab, **mount -a** will not mount it at boot.

##### An example /etc/fstab

```
# <file system>        <dir>        <type>        <options>                 <dump>    <pass>
none                   /dev/pts     devpts        defaults                       0         0
none                   /dev/shm     tmpfs         defaults                       0         0
#/dev/cdrom            /media/cdrom   auto        ro,user,noauto,unhide          0         0
#/dev/dvd              /media/dvd     auto        ro,user,noauto,unhide          0         0
#/dev/fd0              /media/fl      auto        user,noauto                    0         0
/dev/sda1                   /          jfs        defaults,noatime               0         1
/dev/sda2                   /var     reiserfs     defaults,noatime,notail        0         2
/dev/sda3                    swap     swap        defaults                       0         0
/dev/sda4                   /home      jfs        defaults,noatime               0         2

```

**Note:** The 'noatime' option disables writing read access times to the metadata of files and may safely be appended to / and /home regardless of your specified filesystem type for increased speed, performance, and power efficiency (see [here](http://kerneltrap.org/node/14148) for more). 'notail' disables the ReiserFS tailpacking feature, for added performance at the cost of slightly less efficient disk usage.

*   **<file system>**: describes the block device or remote filesystem to be mounted. For regular mounts, this field will contain a link to a block device node (as created by mknod which is called by udev at boot) for the device to be mounted; for instance, '/dev/cdrom' or '/dev/sda1'.

**Note:** If your system has more than one hard drive, the installer will default to using UUID rather than the sd*x* naming scheme, for consistent device mapping. Due to active developments in the kernel and also udev, the ordering in which drivers for storage controllers are loaded may change randomly, yielding an unbootable system/kernel panic. Nearly every motherboard has several controllers (onboard SATA, onboard IDE), and due to the aforementioned development updates, /dev/sda may become /dev/sdb on the next reboot. (See [this wiki article](/index.php/Persistent_block_device_naming "Persistent block device naming") for more information on persistent block device naming. )

*   **<dir>**: describes the mount point for the filesystem. For swap partitions, this field should be specified as 'swap'; (Swap partitions are not actually mounted.)

*   **<type>**: describes the type of the filesystem. The Linux kernel supports many filesystem types. (For the filesystems currently supported by the running kernel, see /proc/filesystems). An entry 'swap' denotes a file or partition to be used for swapping. An entry 'ignore' causes the line to be ignored. This is useful to show disk partitions which are currently unused.

*   **<options>**: describes the mount options associated with the filesystem. It is formatted as a comma separated list of options with no intervening spaces. It contains at least the type of mount plus any additional options appropriate to the filesystem type. For documentation on the available options for non-nfs file systems, see mount(8).

*   **<dump>**: used by the dump(8) command to determine which filesystems are to be dumped. dump is a backup utility. If the fifth field is not present, a value of zero is returned and dump will assume that the filesystem does not need to be backed up. *Note that dump is not installed by default.*

*   **<pass>**: used by the fsck(8) program to determine the order in which filesystem checks are done at boot time. The root filesystem should be specified with a <pass> of 1, and other filesystems should have a <pass> of 2 or 0\. Filesystems within a drive will be checked sequentially, but filesystems on different drives will be checked at the same time to utilize parallelism available in the hardware. If the sixth field is not present or zero, a value of zero is returned and fsck will assume that the filesystem does not need to be checked.

*   If you plan on using **hal** to automount media such as DVDs, you may wish to comment out the cdrom and dvd entries in preparation for **hal**, which will be installed later in this guide.

Expanded information available in the [Fstab](/index.php/Fstab "Fstab") wiki entry.

#### **[/etc/mkinitcpio](/index.php/Configuring_mkinitcpio "Configuring mkinitcpio").conf**

*Most users will not need to modify this file at this time, but please read the following explanatory information.*

This file allows further fine-tuning of the initial ram filesystem, or initramfs, (also historically referred to as the initial ramdisk or "initrd") for your system. The initramfs is a gzipped image that is read by the kernel during boot. The purpose of the initramfs is to bootstrap the system to the point where it can access the root filesystem. This means it has to load any modules that are required for devices like IDE, SCSI, or SATA drives (or USB/FW, if you are booting from a USB/FW drive). Once the initrramfs loads the proper modules, either manually or through udev, it passes control to the kernel and your boot continues. For this reason, the initramfs only needs to contain the modules necessary to access the root filesystem. It does not need to contain every module you would ever want to use. The majority of common kernel modules will be loaded later on by udev, during the init process.

**mkinitcpio** is the next generation of **initramfs creation**. It has many advantages over the old **mkinitrd** and **mkinitramfs** scripts.

*   It uses "glibc" and "busybox" to provide a small and lightweight base for early userspace.
*   It can use **udev** for hardware autodetection at runtime, thus prevents you from having tons of unnecessary modules loaded.
*   Its hook-based init script is easily extendable with custom hooks, which can easily be included in pacman packages without having to modifiy mkinitcpio itself.
*   It already supports **lvm2**, **dm-crypt** for both legacy and luks volumes, **raid**, **swsusp** and **suspend2** resuming and booting from **usb mass storage** devices.
*   Many features can be configured from the kernel command line without having to rebuild the image.
*   The **mkinitcpio** script makes it possible to include the image in a kernel, thus making a self-contained kernel image is possible.
*   Its flexibility makes recompiling a kernel unnecessary in many cases.

If using RAID or LVM on the root filesystem, the appropriate HOOKS must be configured. See the wiki pages for [RAID](/index.php/Installing_with_Software_RAID_or_LVM "Installing with Software RAID or LVM") and [/etc/mkinitcpio](/index.php/Configuring_mkinitcpio "Configuring mkinitcpio") for more info. If using a non-US keyboard. add the "`keymap`" hook to load your local keymap during boot. Add the "`usbinput`" hook if using a USB keyboard, e.g.:

```
HOOKS="base udev autodetect pata scsi sata filesystems keymap usbinput"

```

(Otherwise, if boot fails for some reason you will be asked to enter root's password for system maintenance but will be unable to do so.)

If you need support for booting from USB devices, FireWire devices, PCMCIA devices, NFS shares, software RAID arrays, LVM2 volumes, encrypted volumes, or DSDT support, configure your HOOKS accordingly.

If doing a CF or SD card install, you may need to add the `usbinput` HOOK for your system to boot properly.

*If you are using a US keyboard, and have no need for any of the above HOOKS, editing this configuration should be unnecessary at this point.*

**mkinitcpio** is an Arch innovation developed by Aaron Griffin and Tobias Powalowski with some help from the community.

#### /etc/modprobe.d/modprobe.conf

This file can be used to set special configuration options for the kernel modules. It is unnecessary to configure this file at this time.

#### /etc/resolv.conf (for Static IP)

The *resolver* is a set of routines in the C library that provide access to the Internet Domain Name System (DNS). One of the main functions of DNS is to translate domain names into IP addresses, to make the Web a friendlier place. The resolver configuration file, or /etc/resolv.conf, contains information that is read by the resolver routines the first time they are invoked by a process.

*   *If you are using DHCP, you may safely ignore this file, as by default, it will be dynamically created and destroyed by the dhcpcd daemon. You may change this default behavior if you wish. (See [Network](/index.php/Network#For_DHCP_IP "Network")]).*

If you use a static IP, set your DNS servers in /etc/resolv.conf (nameserver <ip-address>). You may have as many as you wish. An example, using OpenDNS:

```
nameserver 208.67.222.222
nameserver 208.67.220.220

```

If you are using a router, you will probably want to specify your DNS servers in the router itself, and merely point to it from your **/etc/resolv.conf**, using your router's IP (which is also your gateway from **/etc/rc.conf**), e.g.:

```
nameserver 192.168.1.1

```

If using **DHCP**, you may also specify your DNS servers in the router, or allow automatic assignment from your ISP, if your ISP is so equipped.

#### /etc/hosts

This file associates IP addresses with hostnames and aliases, one line per IP address. For each host a single line should be present with the following information:

```
<IP-address> <hostname> [aliases...]

```

Add your *hostname*, coinciding with the one specified in /etc/rc.conf, as an alias, so that it looks like this:

```
127.0.0.1   localhost.localdomain   localhost ***yourhostname***

```

**Note:** *This format, **including the 'localhost' and your actual host name**, is required for program compatibility! So, if you have named your computer "arch", then that line above should look like this:*
```
127.0.0.1   localhost.localdomain   localhost arch

```
Errors in this entry may cause poor network performance and/or certain programs to open very slowly, or not work at all. This is a very common error for beginners.

If you use a static IP, add another line using the syntax: <static-IP> <hostname.domainname.org> <hostname> e.g.:

```
192.168.1.100 ***yourhostname***.domain.org  ***yourhostname***

```

**Tip:** For convenience, you may also use /etc/hosts aliases for hosts on your network, and/or on the Web, e.g.:
```
64.233.169.103   www.google.com   g
192.168.1.90   media
192.168.1.88   data

```
The above example would allow you to access google simply by typing 'g' into your browser, and access to a media and data server on your network by name and without the need for typing out their respective IP addresses.

#### /etc/hosts.deny and /etc/hosts.allow

Modify these configurations according to your needs if you plan on using the [ssh](/index.php/SSH "SSH") daemon. The default configuration will reject all incoming connections, not only ssh connections. Edit your **/etc/hosts.allow** file and add the appropriate parameters:

*   let everyone connect to you

```
sshd: ALL

```

*   restrict it to a certain ip

```
sshd: 192.168.0.1

```

*   restrict it to your local LAN network (range 192.168.0.0 to 192.168.0.255)

```
sshd: 192.168.0.

```

*   OR restrict for an IP range

```
sshd: 10.0.0.0/255.255.255.0

```

If you do not plan on using the [ssh](/index.php/SSH "SSH") daemon, leave this file at the default, (empty), for added security.

#### /etc/locale.gen

The **/usr/sbin/locale-gen** command reads from **/etc/locale.gen** to generate specific locales. They can then be used by **glibc** and any other locale-aware program or library for rendering text, correctly displaying regional monetary values, time and date formats, alphabetic idiosyncrasies, and other locale-specific standards. The ability to setup a default locale is a great built-in privilege of using a <tt>UNIX</tt>-like operating system.

By default /etc/locale.gen is an empty file with commented documentation. Once edited, the file remains untouched. **locale-gen** runs on every **glibc** upgrade, generating all the locales specified in /etc/locale.gen.

Choose the locale(s) you need (remove the # in front of the lines you want), e.g.:

```
en_US ISO-8859-1
en_US.UTF-8	

```

The installer will now run the locale-gen script, which will generate the locales you specified. You may change your locale in the future by editing /etc/locale.gen and subsequently running 'locale-gen' as root.

**Note:** ***If you fail to choose your locale, this will lead to a "The current locale is invalid..." error. This is perhaps the most common mistake by new Arch users, and also leads to the most commonly asked questions on the forum.***

#### Pacman-Mirror

Choose a mirror repository for **pacman**.

*   *archlinux.org is throttled, limiting downloads to 50KB/s*

#### Root password

Finally, set a root password and make sure that you remember it later. Return to the main menu and continue with installing bootloader.

### Install and configure a bootloader

#### For BIOS motherboards

For BIOS systems, several boot loaders are available, see [Boot loaders](/index.php/Boot_loaders "Boot loaders") for a complete list. Choose one as per your convenience. Here, two of the possibilities are given as examples:

*   [Syslinux](/index.php/Syslinux "Syslinux") is (currently) limited to loading only files from the partition where it was installed. Its configuration file is considered to be easier to understand. An example configuration can be found in the [syslinux](/index.php/Syslinux#Examples "Syslinux") article.
*   [GRUB](/index.php/GRUB "GRUB") is more feature-rich and supports more complex scenarios. Its configuration file(s) is more similar to 'sh' scripting language, which may be difficult for beginners to manually write. It is recommended that they automatically generate one.

##### Syslinux

If you opted for a GUID partition table (GPT) for your hard drive earlier, you need to install the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package now for the installation of *syslinux* to work:

```
# pacman -S gptfdisk

```

Install the [syslinux](https://www.archlinux.org/packages/?name=syslinux) package and then use the `syslinux-install_update` script to automatically *install* the bootloader (`-i`), mark the partition *active* by setting the boot flag (`-a`), and install the *MBR* boot code (`-m`):

```
# pacman -S syslinux
# syslinux-install_update -iam

```

After installing Syslinux, configure `syslinux.cfg` to point to the right root partition. This step is vital. If it points to the wrong partition, Arch Linux will not boot. Change `/dev/sda3` to reflect your root partition (if you partitioned your drive as in [the example](#Prepare_the_storage_drive), your root partition is `/dev/sda1`).

 `# nano /boot/syslinux/syslinux.cfg` 
```
...
LABEL arch
        ...
        APPEND root=**/dev/sda3** rw
        ...
```

If adding [UUID](/index.php/UUID "UUID") rather than partition number the syntax is `APPEND root=UUID=*partition_uuid* rw`.

Do the same for the fallback entry.

For more information on configuring and using Syslinux, see [Syslinux](/index.php/Syslinux "Syslinux").

##### GRUB

Install the [grub](https://www.archlinux.org/packages/?name=grub) package and then run `grub-install` to install the bootloader:

```
# pacman -S grub
# grub-install --target=i386-pc --recheck **/dev/sda**

```

**Note:**

*   Change `/dev/sda` to reflect the drive you installed Arch on. Do not append a partition number (do not use `sda*X*`).
*   For GPT-partitioned drives on BIOS motherboards, you also need a "BIOS Boot Partition". See [GPT-specific instructions](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") in the GRUB page.
*   A sample `/boot/grub/grub.cfg` gets installed as part of the [grub](https://www.archlinux.org/packages/?name=grub) package, and subsequent `grub-*` commands may not over-write it. Ensure that your intended changes are in `grub.cfg`, rather than in `grub.cfg.new` or some such file.

While using a manually created `grub.cfg` is absolutely fine, it is recommended that beginners automatically generate one:

**Tip:** To automatically search for other operating systems on your computer, install [os-prober](https://www.archlinux.org/packages/?name=os-prober) (`pacman -S os-prober`) before running the next command.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

**Note:** It is possible that multiple redundant menu entries will be generated. See [GRUB#Redundant_menu_entries](/index.php/GRUB#Redundant_menu_entries "GRUB").

For more information on configuring and using GRUB, see [GRUB](/index.php/GRUB "GRUB").

#### For UEFI motherboards

For UEFI systems, several boot loaders are available, see [Boot loaders](/index.php/Boot_loaders "Boot loaders") for a complete list. Choose one as per your convenience. Here, two of the possibilities are given as examples:

*   [gummiboot](/index.php/Gummiboot "Gummiboot") is a minimal UEFI Boot Manager which provides a menu for [EFISTUB](/index.php/EFISTUB "EFISTUB") kernels and other UEFI applications.
*   [GRUB](/index.php/GRUB "GRUB") is a more complete bootloader, useful if you run into problems with Gummiboot.

No matter which one you choose, first install the [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) package, so you can manipulate your EFI System Partition after installation:

```
# pacman -S dosfstools

```

**Note:** For UEFI boot, the drive needs to be GPT-partitioned and an [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") (512 MiB or larger, gdisk type `EF00`, formatted with FAT32) must be present. In the following examples, this partition is assumed to be mounted at `/boot`. If you have followed this guide from the beginning, you have already done all of these.

##### Gummiboot

Install the [gummiboot](https://www.archlinux.org/packages/?name=gummiboot) package and run `gummiboot install` to install the bootloader to the EFI System Partition:

```
# pacman -S gummiboot
# gummiboot install

```

**Warning:** Gummiboot and the Linux Kernel will not automatically update if your EFI System Partition is not mounted at `/boot`.

You will need to manually create a configuration file to add an entry for Arch Linux to the gummiboot manager. Create `/boot/loader/entries/arch.conf` and add the following contents, replacing `/dev/sdaX` with your **root** partition, usually `/dev/sda2`:

 `# nano /boot/loader/entries/arch.conf` 
```
title          Arch Linux
linux          /vmlinuz-linux
initrd         /initramfs-linux.img
options        root=**/dev/sdaX** rw
```

For more information on configuring and using gummiboot, see [gummiboot](/index.php/Gummiboot "Gummiboot").

##### GRUB

Install the [grub](https://www.archlinux.org/packages/?name=grub) and [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) packages and run `grub-install` to install the bootloader:

```
# pacman -S grub efibootmgr
# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=arch_grub --recheck

```

Next, while using a manually created `grub.cfg` is absolutely fine, it is recommended that beginners automatically generate one:

**Tip:** To automatically search for other operating systems on your computer, install [os-prober](https://www.archlinux.org/packages/?name=os-prober) before running the next command. However *os-prober* is not known to properly detect UEFI OSes.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

For more information on configuring and using GRUB, see [GRUB](/index.php/GRUB "GRUB").

### Н: Перезавантаження

Ось Ви налаштували і встановили базову систему Arch Linux. Вийдіть з інсталяції і перезагрузіть ПК:

```
# reboot

```

(Переконайтесь у видаленні інсталяційного диску)