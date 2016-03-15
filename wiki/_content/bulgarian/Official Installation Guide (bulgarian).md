## Contents

*   [1 Увод](#.D0.A3.D0.B2.D0.BE.D0.B4)
    *   [1.1 Какво е Arch Linux?](#.D0.9A.D0.B0.D0.BA.D0.B2.D0.BE_.D0.B5_Arch_Linux.3F)
    *   [1.2 Лиценз](#.D0.9B.D0.B8.D1.86.D0.B5.D0.BD.D0.B7)
*   [2 Преди инсталацията](#.D0.9F.D1.80.D0.B5.D0.B4.D0.B8_.D0.B8.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D1.8F.D1.82.D0.B0)
    *   [2.1 Архитектури](#.D0.90.D1.80.D1.85.D0.B8.D1.82.D0.B5.D0.BA.D1.82.D1.83.D1.80.D0.B8)
    *   [2.2 Достъпни image файлове](#.D0.94.D0.BE.D1.81.D1.82.D1.8A.D0.BF.D0.BD.D0.B8_image_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.B5)
    *   [2.3 AIF, инсталационната програма](#AIF.2C_.D0.B8.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D0.B0.D1.82.D0.B0_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.B0)
    *   [2.4 Сдобиване с Arch Linux](#.D0.A1.D0.B4.D0.BE.D0.B1.D0.B8.D0.B2.D0.B0.D0.BD.D0.B5_.D1.81_Arch_Linux)
    *   [2.5 Подготвяне на инсталациони медии](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.B2.D1.8F.D0.BD.D0.B5_.D0.BD.D0.B0_.D0.B8.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.B8_.D0.BC.D0.B5.D0.B4.D0.B8.D0.B8)
*   [3 Arch Linux инсталация](#Arch_Linux_.D0.B8.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D1.8F)
    *   [3.1 Използване на инсталационната медия](#.D0.98.D0.B7.D0.BF.D0.BE.D0.BB.D0.B7.D0.B2.D0.B0.D0.BD.D0.B5_.D0.BD.D0.B0_.D0.B8.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D0.B0.D1.82.D0.B0_.D0.BC.D0.B5.D0.B4.D0.B8.D1.8F)
        *   [3.1.1 Преди-boot](#.D0.9F.D1.80.D0.B5.D0.B4.D0.B8-boot)
        *   [3.1.2 След-boot](#.D0.A1.D0.BB.D0.B5.D0.B4-boot)
    *   [3.2 Инсталиране](#.D0.98.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B8.D1.80.D0.B0.D0.BD.D0.B5)
        *   [3.2.1 Взаимодействаща инсталационна процедура](#.D0.92.D0.B7.D0.B0.D0.B8.D0.BC.D0.BE.D0.B4.D0.B5.D0.B9.D1.81.D1.82.D0.B2.D0.B0.D1.89.D0.B0_.D0.B8.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D0.B0_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D0.B4.D1.83.D1.80.D0.B0)
            *   [3.2.1.1 Избете Извор](#.D0.98.D0.B7.D0.B1.D0.B5.D1.82.D0.B5_.D0.98.D0.B7.D0.B2.D0.BE.D1.80)
                *   [3.2.1.1.1 CD-ROM или Друг Извор](#CD-ROM_.D0.B8.D0.BB.D0.B8_.D0.94.D1.80.D1.83.D0.B3_.D0.98.D0.B7.D0.B2.D0.BE.D1.80)
                *   [3.2.1.1.2 Мрежа(FTP/HTTP)](#.D0.9C.D1.80.D0.B5.D0.B6.D0.B0.28FTP.2FHTTP.29)
                    *   [3.2.1.1.2.1 Мрежови Настройки](#.D0.9C.D1.80.D0.B5.D0.B6.D0.BE.D0.B2.D0.B8_.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
                    *   [3.2.1.1.2.2 Избере Огледало](#.D0.98.D0.B7.D0.B1.D0.B5.D1.80.D0.B5_.D0.9E.D0.B3.D0.BB.D0.B5.D0.B4.D0.B0.D0.BB.D0.BE)
            *   [3.2.1.2 Нагласете Часовника](#.D0.9D.D0.B0.D0.B3.D0.BB.D0.B0.D1.81.D0.B5.D1.82.D0.B5_.D0.A7.D0.B0.D1.81.D0.BE.D0.B2.D0.BD.D0.B8.D0.BA.D0.B0)
            *   [3.2.1.3 Подгответе Твърдите Дискове](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.B2.D0.B5.D1.82.D0.B5_.D0.A2.D0.B2.D1.8A.D1.80.D0.B4.D0.B8.D1.82.D0.B5_.D0.94.D0.B8.D1.81.D0.BA.D0.BE.D0.B2.D0.B5)
                *   [3.2.1.3.1 Автоматична Подготовка](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.BD.D0.B0_.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0)
                *   [3.2.1.3.2 Ръчна Подготовка на Твърдия Диск](#.D0.A0.D1.8A.D1.87.D0.BD.D0.B0_.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BD.D0.B0_.D0.A2.D0.B2.D1.8A.D1.80.D0.B4.D0.B8.D1.8F_.D0.94.D0.B8.D1.81.D0.BA)
                *   [3.2.1.3.3 Ръчна настройка на блокови устройства, файлови системи, и точки за прикачване](#.D0.A0.D1.8A.D1.87.D0.BD.D0.B0_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BD.D0.B0_.D0.B1.D0.BB.D0.BE.D0.BA.D0.BE.D0.B2.D0.B8_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0.2C_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.B8_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B8.2C_.D0.B8_.D1.82.D0.BE.D1.87.D0.BA.D0.B8_.D0.B7.D0.B0_.D0.BF.D1.80.D0.B8.D0.BA.D0.B0.D1.87.D0.B2.D0.B0.D0.BD.D0.B5)
                *   [3.2.1.3.4 Rollbacks](#Rollbacks)
            *   [3.2.1.4 Избор на пакети](#.D0.98.D0.B7.D0.B1.D0.BE.D1.80_.D0.BD.D0.B0_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B8)
            *   [3.2.1.5 Инсталиране на пакети](#.D0.98.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B8.D1.80.D0.B0.D0.BD.D0.B5_.D0.BD.D0.B0_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B8)
            *   [3.2.1.6 Настройване на системата](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.B2.D0.B0.D0.BD.D0.B5_.D0.BD.D0.B0_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0.D1.82.D0.B0)
            *   [3.2.1.7 Install Bootloader](#Install_Bootloader)
            *   [3.2.1.8 Exit Install](#Exit_Install)
        *   [3.2.2 Automatic Installation Procedure](#Automatic_Installation_Procedure)
            *   [3.2.2.1 Config file syntax](#Config_file_syntax)
        *   [3.2.3 Customizing Installations](#Customizing_Installations)
*   [4 Новата Ви Система](#.D0.9D.D0.BE.D0.B2.D0.B0.D1.82.D0.B0_.D0.92.D0.B8_.D0.A1.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0)
*   [5 Допълнителна информация](#.D0.94.D0.BE.D0.BF.D1.8A.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D0.BD.D0.B0_.D0.B8.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8F)
    *   [5.1 Управление на пакети](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B0_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B8)
    *   [5.2 APPENDIX](#APPENDIX)

# Увод

## Какво е Arch Linux?

Arch Linux е независима, оптимизирана Линукс дистрибуция за i686 и x86-64,която е била оригинално базирана на идеи от CRUX. Arch е бърз, лек, гъвкав и семпъл.

Семплият дизайн го правят лесен за надграждане и превръщане в каквато система си пожелаете.

## Лиценз

Arch Linux и скриптовете са с авторско право

2002-2007 Judd Vinet

2007-2009 Aaron Griffin

и са лицензирани под GNU General Public License (GPL).

# Преди инсталацията

## Архитектури

ArchLinux е оптимизирана за i686 и x86-64 процесори и няма да тръгне на по-ниски x86 чипове (i386,i486,i586). Pentium II или AMD K6-2 процесор или по-добър е необходим Преди инсталирането на Arch Linux, трябва да решите чрез кой метод ще го инсталирате.

## Достъпни image файлове

Arch Linux предлага bootable image файлове за:

*   CD-rom устройства (ISO формат): работи на почти всички машини със CD-ROM устройство
*   USB диск images файлове(raw формат): работи на всички машини можещи да boot-ват от USB устройства.

Bootloader-а GRUB се използва, но за тези, които имат проблеми с GRUB и определени CD-rom устройства, се предлагат ISO изображения с ISOLINUX bootloader.
Има по два варианта за всяка инсталационна медия и се различават само по пакетите, които предлагат.

*   Image файловете "core" съдържат snapshot на пакетите от core.
    Тези image файлове са подходящи за потребители без Интернет или с бавна връзка.

*   Image файловете "net" почти не съдържат пакети, и използват мрежата за инсталация.
    Препоръчва се да ги ползвате понеже те съдържат най-новите версии на пакетите.

Можете да зададете на инсталационната програма да свали пакетите от Интернет (или някоя мрежа) използвайки изображенията, както и можете да използвате изображенията като среди за възтановяване на системата.
Изображенията работят като обикновена Arch Linux система.
Те са инсталация на Arch Linux на CD или USB изображение вместо на твърд диск.
Те съдържат целия пакет "base" , както и различни програми за настройки на мрежата и драйвъри.
Ако ви трябва нещо друго по време на инсталацияата, инсталирайте го чрез pacman.

## AIF, инсталационната програма

Arch Linux използва AIF (Arch Linux Installation Framework) за извършване на инсталацията.
Порграмата - написана в bash - съдържа библиотеки за различни функции (инсталиране на пакети, настройки на дискове и т.н.) и някои процедури, които използват тези библиотеки за да улеснят инстлационния процес както и други малки задачи (кратки процедури'). Тези процедури са включени по подразбиране:

*   interactive: Взаимодействаща инсталационна процедура, която задава въпроси, помага с инстлационния процес и настройките на системата като автоматично променя настройки на неща, които по-рано се задали (пример: мрежови настройки).
    В началото инсталирана системаще има само пакети от "base", които могат да бъдат настройвани заедно с програми и драйвъри да помагат да се свържете с Интернет.
    След като успешно се заредили системата, ще направите пълно системно обновление и ще инсталирате останалите пакети, които желаете. (под прякор `/arch/setup`)
*   automatic: Автоматизирана процедура, с мининални изисквания за интеракция от потребителя.
    Използва профили за настройките на системата.
    Вижте /usr/share/aif/examples/ за примерни профилни файлове. Примерите са за освнони настройки, но можете да ги редактирате по желание да включват допълнително пакети, и т.н.
*   base: основна инсталация, с малко интеракция от страна на потребителя.
    Останалите процедури ползват тази и НЕ СЕ препоръчва на потребителите да изберат този път.
*   partial-configure-network: излага настройките от взаимодействаща инсталационна процедура, за да помогнат в живата среда.
*   partial-disks: Прочита на дисковата подсистема или прави rollback.
*   partial-keymap: Променя клавиатурата/конзолните шрифтови настройки. (под прякор `km`)

Преимуществата на процедури като partial-keymap и partial-configure-network над директното използване на инструменти като loadkeys или ifconfig е, че когато използвате взаимодействащата процедура, ще имате възможност да запази настройките в конфигурационните файлове на системата.

Можете и да отидете по-дълбоко:

*   да създавате собствени процедури или презапишете части от други процедури
*   да създавате собствени библиотеки, за нови функции
*   да създавате собствени настройки за процедурите, които ги поддържат (пример automatic)

За повече информация вижте readme файла от AIF.

## Сдобиване с Arch Linux

*   Можете да свалите Arch Linux от огледалните адреси в страницата [download](https://www.archlinux.org/download/).

*   Също така, можете да закупите инсталационен CD отm Archux, OSDisc or LinuxCD и може да ви бъде изпратен навсякъде по света.

## Подготвяне на инсталациони медии

**CD-ROM**

*   Свалете iso/<release>/archlinux-XXX.iso

*   Свалете iso/<release>/sha1sums.txt

*   Потвърдете валидността на .iso image файла чрез sha1sum:

    sha1sum --check sha1sums.txt

    archlinux-XXX.iso: OK

*   Запишете ISO image файла на CD-R или CD-RW със софтуеър по ваш избор.

**USB**

*   Свалете iso/<release>/archlinux-XXX.img

*   Свалете iso/<release>/sha1sums.txt

*   Потвърдете валидността на .img image файла чрез sha1sum:

    sha1sum --check sha1sums.txt

    archlinux-XXX.img: OK

*   Запишете disk image файла на USB устройство с памет (флашка), използвайки dd или подобна програма подържаща raw-write:

    dd if=archlinux-XXX.img of=/dev/sdX

Бъдете сигурни, че използвате /dev/sdX а не /dev/sdX1\.
Тази команда ще изтрие безвъзвратно всичко от USB устройството, така че провете дали нямате запазена важна информация преди да започнете.

# Arch Linux инсталация

## Използване на инсталационната медия

### Преди-boot

Проверете дали вашият BIOS е нагласен да boot-ва от CD-ROM или USB устройства.
Рестартирайте компютъра с инсталационния CD на Arch Linux в CD-ROM устройството или с USB устройството вкарано в порта. След като инсталационната медия започне да boot-ва яе видите емблемата на Arch Linux и grub меню чакащо вашия избор.
Обикновено можете просто да натиснете Enter.
Ако Grub забие, най-вероятно имате проблем със CD-ROM устройството и се препоръчва да пробвате USB метода.

### След-boot

След като се зареди напълно, инсталационна програмата ще ви поиска логин. В горната част на екрана ще видите кратки инструкции..
Влезте като root. От тук нататък можете да ръчно да инсталирате Arch, както и да започнете самата инсталация

*   Ако предпочитате клавиатура различна от US или искате специфичен шрифт за конзолата, напишете `km` за да ги смените.
*   Ако по някаква причина ви трябва мрежови достъп преди да стартирате инсталационната програма, (интерактивната процедура ви дава възможност да настроите мрежата за NET инсталации)
    можете да напишете `aif -p partial-configure-network`

И за двете, настройките ще бъдат запомнени и могат да бъдат ползвани по желание по време на взаимодействащата инсталационна процедура.

Също така има логин име `arch`, което ви дава възможност да правите неща като непривилигерован потребител.
Повечето хора не използват тази функция.

Всичко нужно за инсталацията можете да намерите в /arch

## Инсталиране

Можете да изберете взаимодействащата или автоматичната процедура.
Вижте readme файла на AIF за повече информация.

### Взаимодействаща инсталационна процедура

Вкарайте `/arch/setup` (или `aif -p interactive`, което е същото) за да започнете.

След първоначлния екран и предупреждение ще се появи главното инсталационно меню. Можете да използвате стрелките Нагоре и Надолу за да се движите из менюто. Използвайте клавиша TAB за да избирате различните бутони и ENTER за да ги активирате. По време на инсталацията можете да видите какво се случва в седмата виртуална конзола като натиснете (ALT-F7). Изпозлвайте (ALT-F1) за да се върнете обратно към основната конзола. Може и да ползвате и други конзоли, ако ви потрябват.

#### Избете Извор

Първо трябва да изебере как ще иснталирате Arch Linux. Ако имате бърза Интернет връзка, се преопръчва NET инсталацията, която подсигурява получването на най-новите версии на пакетите (за разлика от остарелите от CD или USB). Ако пък сте избрали изображението NET, нямате много избор ;-).

##### CD-ROM или Друг Извор

Ако изберете CD-ROM или OTHER SOURCE ще можете да инсталирате само пакетите, които са на компакт дискта (а те вероятно са остарели) или пакети от медия, която сте прикачили ръчно (DVD, USB, т.н.) към файловата система. Преимущество е, че не се изисква Интернет връзка за този тип инсталация и съответно се препоръчва на хора с бавна Интернет връзка, както и на хора, които не искат да чакат да се свалят всичките инсталационни пакети.

##### Мрежа(FTP/HTTP)

###### Мрежови Настройки

Първата опция в Setup Network ви дава възможност да инсталирате и настроите мрежовата карта. Ако използвате безжична карта ще трябва да я настроите ръчно, в такъв случай тази част от инсталационната програма няма да ви помогне. Ще ви бъде предоставен списък с наличните мрежови устройства. Ако нито една ethernet карта не е налична, или тази която искате да ползвате я няма, или изберете OK и я заредете ръчно (probe), или превключете към друга конзола и ръчно заредете модула. Ако все още не можете да настроите мрежовата карта, проверете дали е сложена правилно в дънната платка и дали е поддържа от ядрото на Linux.

Когато правиния модул е зареден, и вашата мрежова карта се вижда в списъка, трябва да изберете ethernet устройството, което искате да конфигурирате и ще ви бъде дадена възможност да нагласите мрежата чрез DHCP. Ако мрежата ви не ползва DHCP, изберете NO и нагласете настройките ръчно. И при двата случая мрежата вече ще бъде конфигурирана след настройките.

###### Избере Огледало

Choose Mirror ви дава възможност да изберете предпочитаното огледало за свалянето на пакетите, които ще инсталирате. Препоръчва се да избере огледало максимално физически близко до вас за да постигнете максимални скорости на сваляне. По-нататък в инсталационния процес ще имате възможност да зададете избраното огледало по подразбиране за бъдещи инсталации на пакети.

**Note: ** ftp.archlinux.org is throttled to 50 KB/s.

Тези опции само се показват когато е избрана FTP инсталация. След подготовката, изберете Return to Main Menu.

#### Нагласете Часовника

Set Clock ви дава възможност да нагласите системния часовник. Първо трябва да изберете дали хардуерния часовник е нагласен на UTC или localtime. UTC се препоръчва, но ако имате друга операционна система инсталирана, която не може да ползва UTC нормално (като Windows), ще трябва да изберете localtime. След това ще трябва да изберете времевия пояс и ще можете да нагласите датата и часовника (можете да ползвате [NTP](http://www.ntp.org/) ако мрежата ви работи).

#### Подгответе Твърдите Дискове

Prepare Hard Drive ще ви заведе в подменю с две алтернативи да подготвите твърдия диск(ове) за инсталацията, както и опция за започване отначало в случай на грешка.

*   Auto-prepare ще настрои (и презапише) дяловете на диска автоматично. Създава /boot, swap, / и /home дялове и ви дава възможност да изберете размер и файлов тип на дяловете.
*   Ако искате повече контрол, можете ръчно да нагласите дяловете на твърдия диск и после ръчно да зададете пълна инсталация използвайки тези дялове. Също така, тук можете да ползвате неща като lvm и dm_crypt.
*   Rollback проверява кои файлови системи са били създадени чрез тези методи, разкачва споменатата файлова система и унищожава lvm и dm_crypt ако са били създадени от вас. Използвайте тази опция ако вя трябва undo/redo на определена схема. Ще бъдете подсетени за това ако забравите.

Бележки:

*   AIF can help you set up new dm_crypt and lvm volumes, but not (yet) softraid.
*   AIF currently does not help you creating volumegroups that span multiple physical volumes. (if you need this -unlikely- : use vgcreate)
*   AIF supports reusing filesystems, but only if it can find the blockdevice. If you want to reuse a filesystem that is on top of lvm/dm_crypt/softraid, you will need to bring up the volumes yourself.

##### Автоматична Подготовка

Auto-Prepare will automatically partition a hard drive of your choice into a /boot, swap, a root partition, and a /home and then create filesystems on all four. These partitions will also be automatically mounted in the proper place. To be exact, this option will create:

*   32 MB ext2 /boot partition
*   256 MB swap partition
*   7.5 GB root partition
*   /home partition with the remaining space

Ще трябва да модифицирате размерите според вашите изисквания, но /home винаги ще използва остатъка от свободното пространство. Можете да нагласите използваните файлови системи за /boot и за root и /home едновременно.

**АВТОМАТИЧНАТА ПОДГОТОВКА ЩЕ ИЗТРИЕ ВСИЧКАТА ИНФОРМАЦИЯ ОТ ИЗБРАНИЯ ТВЪРД ДИСК!**

##### Ръчна Подготовка на Твърдия Диск

Тук можете да изберете кой диск(ове) да разделите на дялове с прогрмата cfdisk, където свободно можете да настроите дяловете преди да ги запазите с [Write] и [Quit]. Дялът root е задължителен за да продължите инсталацията.

##### Ръчна настройка на блокови устройства, файлови системи, и точки за прикачване

Всички разпознати дялове са показани в това меню. Над тях можете да създадете нови файлови системи. Имайте впредвид три неща:

*   Всичко тук е само модел и ще бъде нагласено само след като потвърдите.
*   Не всички блокови устройства поддържат всички файлови системи (пример: не можете да сложите LVM обемна група на нещо друго освен на физически LVM). Инсталационната програма автоматично ще филтрира възможните файлови системи и дори автоматично ще извере една.
*   Някои файлови системи създават нови blockdevices. Така е при dm_crypt и lvm. Те ще се появят в модел и ще можете да ги използвате върху други файлови системи.
*   Когато ви попитат за (optional) настройки на mkfs tools, подайте аргументи, коите ще бъдат използвани като се създава mkfs. Пример, за да изключите journal на ext файлови системи:
    *   не правете: `^has_journal`
    *   а по-добре: `-O ^has_journal`

When filesystems setup is complete, select 'Done'. At this point a check will be run which will tell you any critical errors (such as no root filesystem) and/or give you some warnings which you may ignore (like no swap). If anything is found, you can go back to fix these issues, or continue at which point everything will be setup the way you asked.

For example, if you want a setup that uses LVM on top of dm_crypt, you would:

*   make sure that you have a 2 partitions: a small one for the unencrypted boot (about 100M) and one for the rest of the (encrypted) system. (do this in "Manually partition hard drives")
*   on your /dev/sdX1, make an ext2 filesystem with mountpoint /boot
*   on your /dev/sdX2, make a dm_crypt volume, with label sdX2crypt (or whatever you want)
*   /dev/mapper/sdX2crypt will appear. Put a LVM physical volume on this
*   /dev/mapper/sdX2crypt+ appears. This is the representation of the physical volume. Put a volumegroup on this, with label cryptpool (or whatever you want)
*   /dev/mapper/cryptpool appears. On this volumegroup you are able to put multiple logical volumes. Make 2:
    *   one with size 5G: label this cryptroot
    *   one with size 10G: label this crypthome
*   2 new volumes appear:
    *   /dev/mapper/cryptpool-cryptroot: on this blockdevice, you can put your root filesystem, with mountpoint /.
    *   /dev/mapper/cryptpool-crypthome is the blockdevice on which you can put the filesystem with mountpoint /home.
*   If you want swapspace, make a logical volume for swap and put a swap volume on it.
*   That's it! If you select 'done' it should process the model and create your disk setup the way you specified. The cool part is that you can pick relatively small values for your volumes to start with, and if you need more space later you can grow the logical volume and the filesystem on top of it.

##### Rollbacks

The rollback function will do everything necessary to "undo" changes you made in the 'Manually configure block devices, filesystems and mountpoints' or 'Autoprepare' step, to allow you completely redo your setup.

It will:

*   unmount filesystems from the target system
*   destroy/undo lvm and dm_crypt volumes.

It will not:

*   undo any partitioning
*   remove 'simple' filesystems such as ext3, xfs, swap etc.

The reason for this is simple: only things that might disturb subsequent hard disk preparations need to be undone.

#### Избор на пакети

Select Packages ви дава възможност да изберете кои пакети да инсталирате от компакт диск, USB или NET огледало. Можете да зададете цели групи от пакети от които ще инсталирате пакетите, и после да премахнете тези, които не ви трябват ор групите. Препоръчва се да инсталирате всички пакети от "base", но нищо друго за сега. Изключение са пакети, които са нужни за Интернет връзка.

След като сте избрали пакетите, излезте от менюто и отидете на следващата стъпка.

#### Инсталиране на пакети

Install Packages ще инсталира основните пакети, както и други пакети, които сте избрали в предишната стъпка на вашия твърд диск.

#### Настройване на системата

Configure System има няколко функции:

*   автоматично подготвя някои конфигурационни файлове (пример: menu.lst на grub, HOOKS на mkinitcpio.conf, настройки на клавиатурата в rc.conf, огледалата на pacman и пр.)
*   презарежда някои файлове за които сте се съгласили по-рано. (пример: мрежови настройки)
*   позволява ръчни настройки на конфигурационните файлове. Ще бъдете попитани кой редактор да използвате. Имате избор между nano, joe или vi
*   дава възможност за нагласяне на паролата за root.

**Конфигурационни файлове**

Това са основните конфигурационни файлове в Arch. Ако имате нужда от помощ за определен процес, прочетете съвпадаща страница от man или се обърнете към онлайн документацията. В много случаи Arch Linux [Wiki](https://wiki.archlinux.org/) и [forums](https://bbs.archlinux.org/) имат достатъчно информация относно темите.

*   /etc/rc.conf
*   [/etc/fstab](/index.php/Fstab "Fstab")
*   /etc/mkinitcpio.conf
*   /etc/modprobe.d/modprobe.conf
*   /etc/resolv.conf
*   /etc/hosts
*   /etc/hosts.deny
*   /etc/hosts.allow
*   /etc/locale.gen
*   /etc/pacman.d/mirrorlist
*   /etc/pacman.conf

**/etc/rc.conf**

Това е главния конфигурационен файл на Arch Linux. Там можете да настроите клавиатурата, времевия пояс, hostname, мрежата, daemon-ите както и кои модули да се зареждат при boot, профили и други.

**LOCALE:** Това настройва езикът на системата, който ще бъде използван от всички програми подържащи i18-. Вижте locale.gen отдолу за повече избори на настройки. По подразбиране, настройките са ориентиране за англоговорящи потребители.

**HARDWARECLOCK:** Или UTC ако часовникът в BIOS-а е настроен на UTC, или localtime ако часовника в BIOS-а е настроен на местното време. Ако имате Операционна Система, която не може да чете UTC време от BIOS-а правилно, като Windows, изберете localtime , иначе се предпочита UTC, което смомага за смяната на лятното/зимното време както и други малки подобрения.

**USEDIRECTISA:** Ако изберете "yes" ще настроите hwclock да използва I/O инструкции за достъп до часовника. иначе, hwclock ще се опита да изпозва устройството /dev/rtc , по подразбиране от драйвъра rtc. Опция "no" работи за лица, които не ползват ISA.

**TIMEZONE:** Specifies your time zone. Possible time zones are the relative path to a zoneinfo file starting from the directory /usr/share/zoneinfo. For example, a German timezone would be Europe/Berlin, which refers to the file /usr/share/zoneinfo/Europe/Berlin. If the exact timezone filename is unknown, worry about it later.

**KEYMAP:** Defines the keymap to load with the loadkeys program on bootup. Possible keymaps are found in /usr/share/kbd/keymaps. Please note that this setting is only valid for your TTYs, not any graphical window managers or X! Again, the default is fine for US users.

**CONSOLEFONT:** Defines the console font to load with the setfont program on bootup. Possible fonts are found in /usr/share/kbd/consolefonts.

**CONSOLEMAP:** Defines the console map to load with the setfont program on bootup. Possible maps are found in /usr/share/kbd/consoletrans. Set this to a map suitable for the appropriate locale (8859-1 for Latin1, for example) if using an UTF-8 locale above, and use programs that generate 8-bit output. If using X11 for everyday work, this may be skipped, as it only affects the output of Linux console applications.

**USECOLOR:** Enable (or disable) colorized status messages during boot-up.

**MOD_AUTOLOAD:** Ако е нагласено "yes", се позволява на udev да зарежда модули когато са нужни при зареждането. Ако е нагласено "no", няма да има такива разрешения.

**MODULES:** In this array you can list the names of modules you want to load during bootup without the need to bind them to a hardware device as in the modprobe.conf. Simply add the name of the module here, and put any options into modprobe.conf if need be. Prepending a module with a bang ('!') will blacklist the module, and not allow it to be loaded.

**USELVM:** Избере "yes" за екзекуция на vgchange по време на sysinit, активирайки групите LVM

**HOSTNAME:** Set this to the hostname of the machine, without the domain part. This is totally your choice, as long as you stick to letters, digits and a few common special characters like the dash.

**INTERFACES:** Here you define the settings for your networking interfaces. The default lines and the included comments explain the setup well enough. If you use DHCP, 'eth0="dhcp"' should work for you. If you do not use DHCP just keep in mind that the value of the variable (whose name must be equal to the name of the device which is supposed to be configured) equals the line which would be appended to the ifconfig command if you were to configure the device manually in the shell.

**ROUTES:** You can define your own static network routes with arbitrary names here. Look at the example for a default gateway to get the idea. Basically the quoted part is identical to what is passed to a manual route add command, therefore reading man route is recommended, or simply leave this alone.

**[/index.php/Network_Profiles NET_PROFILES]:** Enables certain network profiles at bootup. Network profiles provide a convenient way of managing multiple network configurations, and are intended to replace the standard INTERFACES/ROUTES setup that is still recommended for systems with only one network configuration. If your computer will be participating in various networks at various times (eg, a laptop) then you should take a look at the /etc/network-profiles/ directory to set up some profiles. There is a template file included there that can be used to create new profiles. This now requires the netcfg package.

**DAEMONS:** This array simply lists the names of those scripts contained in /etc/rc.d/ which are supposed to be started during the boot process. If a script name is prefixed with a bang (!), it is not executed. If a script is prefixed with an "at" symbol (@), then it will be executed in the background, ie. the startup sequence will not wait for successful completion before continuing. Usually you do not need to change the defaults to get a running system, but you are going to edit this array whenever you install system services like sshd, and want to start these automatically during bootup.

**[/etc/fstab](/index.php/Fstab "Fstab")**

Filesystem settings and mountpoints are configured here. The installer should have created the necessary entries. Ensure they are accurate and correct.

**/etc/mkinitcpio.conf**

This file allows you to fine-tune the initial ramdisk for your system. The ramdisk is a gzipped image that is read by the kernel during bootup. Its purpose is to bootstrap the system to the point where it can access the root filesystem. This means it has to load any modules that are required to "see" things like IDE, SCSI, or SATA drives (or USB/FW, if you are booting off a USB/FW drive). Once the ramdisk loads the proper modules, either manually or through udev, it passes control to the Arch system and your bootup continues. For this reason, the ramdisk only needs to contain the modules necessary to access the root filesystem. It does not need to contain every module you would ever want to use. The majority of your everyday modules will be loaded later on by udev, during the init process.

By default, mkinitcpio.conf is configured to autodetect all needed modules for IDE, SCSI, or SATA systems through so-called HOOKS. The installed should also have inserted hooks like crypt, lvm, keymap and usbinput if relevant. This means the default initrd should work for almost everybody. /etc/mkinitcpio.conf may be edited to remove the subsystem HOOKS (ie, IDE, SCSI, RAID, USB, etc) that are unneeded. The system may be customized even further by specifying the exact modules needed in the MODULES array and remove even more of the hooks, but proceed with caution.

If using RAID on the root filesystem, the RAID settings near the bottom must be configured. See the wiki pages for RAID and mkinitcpio for more info. If using a non-US keyboard, also add the 'keymap' hook, as well as the 'usbinput' hook if using a USB keyboard.

**/etc/modprobe.d/modprobe.conf**

This tells the kernel which modules to load for system devices and what options to set. For example, to have the kernel load the Realtek 8139 ethernet module when it starts the network (ie. tries to setup eth0), use this line:

```
alias eth0 8139too

```

Most people will not need to edit this file.

**/etc/resolv.conf**

Use this file to manually setup the preferred nameserver(s). It should basically look like this:

```
search domain.tld
nameserver 192.168.0.1
nameserver 192.168.0.2

```

Replace domain.tld and the ip addresses with your settings. The so-called search domain specifies the default domain that is appended to unqualified hostnames automatically. By setting this, a ping myhost will effectively become a ping myhost.domain.tld with the above values. These settings usually are not mighty important, though, and most people should leave them alone for now. If you use DHCP, this file will be replaced with the correct values automatically when networking is started, meaning you can and should happily ignore this file.

**/etc/hosts**

This is where you stick hostname/ip associations of computers on your network. If a hostname is not known to your DNS, you can add it here to allow proper resolving, or override DNS replies. You usually do not need to change anything here, but you might want to add the hostname and hostname + domain of the local machine to this file, resolving to the IP of your network interface. Some services, postfix for example, will bomb otherwise. If you do not know what you are doing, leave this file alone until you read man hosts.

**/etc/locale.gen**

This file contains a list of all supported locales and charsets available to you. When choosing a LOCALE in your /etc/rc.conf or when starting a program, it is required to uncomment the respective locale in this file, to make a "compiled" version available to the system, and run the locale-gen command as root to generate all uncommented locales and put them in their place afterwards. You should uncomment all locales you intend to use.

During the installation process, you do not need to run locale-gen manually, this will be taken care of automatically after saving your changes to this file. By default, all locales are enabled that would make sense by rc.conf's LOCALE= setting. To make your system work smoothly, you should edit this file and uncomment at least the one locale you are using in your rc.conf.

**/etc/pacman.d/mirrorlist**

This file contains a list of mirrors from which pacman will download packages for the official Arch Linux repositories. The mirrors are tried in the order in which they are listed. The $repo macro is automatically expanded by pacman depending on the repository (core, extra, community or testing).

If you are performing an FTP installation, the mirror you used to download the packages from will be added on top of the mirror list, in order to be used as the default mirror in your new Arch Linux system.

**/etc/pacman.conf**

Here you can customize pacman settings such as which repositories to use.

**Set Root Password**

At this step, you must set the root password for your system. Choose this password carefully, preferably as a mixture of alphanumeric and special characters, since this password allows you to modify critical parts of your system.

When you are done editing the configuration files choose Return to return to the main menu. The setup will regenerate the initial ramdisk to enable the changes you made in mkinitcpio.conf.

#### Install Bootloader

Install Bootloader will install a bootloader on your hard drive, either GRUB or NONE in case you have a bootloader already installed and want to use that one instead. If you choose to install GRUB, the setup script will want you to examine the appropriate configuration file to confirm the proper settings.

**/boot/grub/menu.lst**

You should check and modify this file to accommodate your boot setup if you want to use GRUB, otherwise you will have to modify your existing bootloader's configuration file. The installer will have pre-populated this file using UUID entries which you may have to change in the same cases you would need to change them in your fstab.

After checking your bootloader configuration for correctness, you will be prompted for a partition to install the loader to. Unless you are using yet another boot loader, you should install GRUB to the MBR of the installation disk, which is usually represented by the appropriate device name without a number suffix.

#### Exit Install

Exit the Installer, remove the media you used for the installation, type reboot at the command line and cross your fingers!

### Automatic Installation Procedure

With the automatic installation procedure, you can do scripted/automatic installations. See [#Aif_the_installation_tool 2.3 AIF, the installation tool] In /usr/share/aif/examples you will find example profiles which will need no or minimal editing in order to install a system:

*   generic-install-on-sda this file demonstrates some things you can do (adding custom packages, setting timezone, update config files etc) it sets up a simple installation (with a structure similar to what you get with Auto-prepare) on /dev/sda
*   fancy-install-on-sda very similar to generic-install-on-sda, but sets up a "filesystems on lvm on dm_crypt" system on /dev/sda

Invoke as `aif -p automatic -c /path/to/configfile` Obviously, do not forget to change the hard disk names unless you want to use /dev/sda.

#### Config file syntax

Config files will be sourced by the bash shell, so they need to be valid bash code.

**PARTITIONS:** Allows you to define partitions for your hard disk, separated by spaces.

*   first comes the device file for the hard disk
*   then for each partition you want: size in MiB (or '*' for all remaining space),filesystem type and optionally a '+' to toggle the bootable flag. separated by colons (':')

**BLOCKDATA:** In this multi-line variable you can describe for each partition you will have how it should be used. Study the examples to see how it works.

### Customizing Installations

You can also customize your installation experience by writing new procedures (possibly inheriting from current procedures) or config files for procedures that support it (eg automatic). You have all the aif libraries at your disposal and you can create new libraries. (see /usr/lib/aif) This is a moving target, so consult the AIF readme for more information.

# Новата Ви Система

Ако всичко е минало наред можете да рестартирате (провете че сте извалиди USB устройството / CD-ROM).

You will notice that in the early userspace (the part that comes after the bootloader) the hooks (as defined in mkinitcpio.conf) needed to get your root filesystem are run.
If you have lvm, it will run the lvm hook. If you use encryption, it will the keymap and encrypt hooks so you can enter your password to decrypt the volume.

Once the system is booted, login as root. By default the password is empty but in the interactive procedure you can change it.

# Допълнителна информация

## Управление на пакети

Pacman е менъджерът на пакети, който следи инсталирания софтуеър на системата. Има проста поддръжка за dependencies и използва gunzip tar формат. Някои прости задачи, които можете да зададете са обяснени по-долу. За пълна документация на pacman, посетете [Wiki](/index.php/Pacman "Pacman").

**Типични задачи:**

*   Подновяване на списъка с пакети

    # pacman --sync --refresh

    # pacman -Sy

This will retrieve a fresh master package list from the repositories defined in the /etc/pacman.conf file and decompress it into the database area.

*   Търсене на пакети в repositories

    # pacman --sync --search <regexp>

    # pacman -Ss <regexp>

Search each package in the sync databases for names or descriptions that match regexp.

*   Display specific not installed package info

    # pacman --sync --info foo

    # pacman -Si foo

Displays information on the not yet installed package foo (size, install date, build date, dependencies, conflicts, etc.)

*   Добавяне на пакет от

    # pacman --sync foo

    # pacman -S foo

Retrieve and install package foo, complete with all dependencies it requires. Before using any sync option, make sure you refreshed the package list.

*   List installed packages

    # pacman --query

    # pacman -Q

Показва списък с всички инсталирани пакети.

*   Проверка дали определен пакет е инсталиран

    # pacman --query foo

    # pacman -Q foo

This command will display the name and version of the foo package if it is installed, nothing otherwise.

*   Display specific package info

    # pacman --query --info foo

    # pacman -Qi foo

Displays information on the installed package foo (size, install date, build date, dependencies, conflicts, etc.)

*   Display list of files contained in package

    # pacman --query --list foo

    # pacman -Ql foo

Показва всички файлови към пакет foo.

*   Find out which package a specific file belongs to

    # pacman --query --owns /path/to/file

    # pacman -Qo /path/to/file

This query displays the name and version of the package which contains the file referenced by its full path as a parameter.

## APPENDIX

See [Official Arch Linux Install Guide Appendix](/index.php/Official_Arch_Linux_Install_Guide_Appendix "Official Arch Linux Install Guide Appendix") for some related unofficial documentation, new users may find useful.