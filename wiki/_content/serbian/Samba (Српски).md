| **Кратак преглед**  |
| Инсталација, конфигурисање и решавање проблема Samba протокола |
| **Слично** |
| [NFS](/index.php/NFS "NFS") |
| [Samba Domain Controller](/index.php/Samba_Domain_Controller "Samba Domain Controller") |

**Samba** је реимплементација SMB/CIFS мрежног протокола, који олакшава дељење фајлова и штампача међу Linux и Windows системима као алтернатива за [NFS](/index.php/NFS "NFS"). Неки корисници кажу да се Samba лако конфигурише и да је рад веома једноставан. Али, многи корисници наиђу на проблеме са његовим комплексним и неинтуитивним механизмом. Препорука је да се корисници држе следећих упутстава.

## Contents

*   [1 Инсталација](#.D0.98.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D1.98.D0.B0)
*   [2 Конфигурација](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.98.D0.B0)
    *   [2.1 smb.conf](#smb.conf)
    *   [2.2 Покретање и аутоматизација daemona](#.D0.9F.D0.BE.D0.BA.D1.80.D0.B5.D1.82.D0.B0.D1.9A.D0.B5_.D0.B8_.D0.B0.D1.83.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.98.D0.B0_daemona)
    *   [2.3 SWAT: Samba веб административна алатка](#SWAT:_Samba_.D0.B2.D0.B5.D0.B1_.D0.B0.D0.B4.D0.BC.D0.B8.D0.BD.D0.B8.D1.81.D1.82.D1.80.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D0.B0_.D0.B0.D0.BB.D0.B0.D1.82.D0.BA.D0.B0)
    *   [2.4 Додавање корисника](#.D0.94.D0.BE.D0.B4.D0.B0.D0.B2.D0.B0.D1.9A.D0.B5_.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D0.BD.D0.B8.D0.BA.D0.B0)
*   [3 Приступ дељеним фајловима](#.D0.9F.D1.80.D0.B8.D1.81.D1.82.D1.83.D0.BF_.D0.B4.D0.B5.D1.99.D0.B5.D0.BD.D0.B8.D0.BC_.D1.84.D0.B0.D1.98.D0.BB.D0.BE.D0.B2.D0.B8.D0.BC.D0.B0)
    *   [3.1 Приступ Samba дељеним фолдерима из Gnome окружења](#.D0.9F.D1.80.D0.B8.D1.81.D1.82.D1.83.D0.BF_Samba_.D0.B4.D0.B5.D1.99.D0.B5.D0.BD.D0.B8.D0.BC_.D1.84.D0.BE.D0.BB.D0.B4.D0.B5.D1.80.D0.B8.D0.BC.D0.B0_.D0.B8.D0.B7_Gnome_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D1.9A.D0.B0)
    *   [3.2 Приступ дељеним фајловима из другог графичког окружења](#.D0.9F.D1.80.D0.B8.D1.81.D1.82.D1.83.D0.BF_.D0.B4.D0.B5.D1.99.D0.B5.D0.BD.D0.B8.D0.BC_.D1.84.D0.B0.D1.98.D0.BB.D0.BE.D0.B2.D0.B8.D0.BC.D0.B0_.D0.B8.D0.B7_.D0.B4.D1.80.D1.83.D0.B3.D0.BE.D0.B3_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.BA.D0.BE.D0.B3_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D1.9A.D0.B0)
    *   [3.3 Приступ Samba дељеном фајлу из шкољке](#.D0.9F.D1.80.D0.B8.D1.81.D1.82.D1.83.D0.BF_Samba_.D0.B4.D0.B5.D1.99.D0.B5.D0.BD.D0.BE.D0.BC_.D1.84.D0.B0.D1.98.D0.BB.D1.83_.D0.B8.D0.B7_.D1.88.D0.BA.D0.BE.D1.99.D0.BA.D0.B5)
        *   [3.3.1 Аутоматско монтирањеAutomatic](#.D0.90.D1.83.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D1.81.D0.BA.D0.BE_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.B0.D1.9A.D0.B5Automatic)
            *   [3.3.1.1 smbnetfs](#smbnetfs)
            *   [3.3.1.2 fusesmb](#fusesmb)
            *   [3.3.1.3 Autofs](#Autofs)
        *   [3.3.2 Ручно монтирање](#.D0.A0.D1.83.D1.87.D0.BD.D0.BE_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.B0.D1.9A.D0.B5)
            *   [3.3.2.1 Додавање дељеног фолдера у fstab](#.D0.94.D0.BE.D0.B4.D0.B0.D0.B2.D0.B0.D1.9A.D0.B5_.D0.B4.D0.B5.D1.99.D0.B5.D0.BD.D0.BE.D0.B3_.D1.84.D0.BE.D0.BB.D0.B4.D0.B5.D1.80.D0.B0_.D1.83_fstab)
            *   [3.3.2.2 Дозвољавање корисницима да монтирају](#.D0.94.D0.BE.D0.B7.D0.B2.D0.BE.D1.99.D0.B0.D0.B2.D0.B0.D1.9A.D0.B5_.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D0.BD.D0.B8.D1.86.D0.B8.D0.BC.D0.B0_.D0.B4.D0.B0_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.B0.D1.98.D1.83)
*   [4 Савети и трикови](#.D0.A1.D0.B0.D0.B2.D0.B5.D1.82.D0.B8_.D0.B8_.D1.82.D1.80.D0.B8.D0.BA.D0.BE.D0.B2.D0.B8)
    *   [4.1 Дељење фајлова у локалној мрежи без корисничког имена и лозинке](#.D0.94.D0.B5.D1.99.D0.B5.D1.9A.D0.B5_.D1.84.D0.B0.D1.98.D0.BB.D0.BE.D0.B2.D0.B0_.D1.83_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D0.BD.D0.BE.D1.98_.D0.BC.D1.80.D0.B5.D0.B6.D0.B8_.D0.B1.D0.B5.D0.B7_.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D0.BD.D0.B8.D1.87.D0.BA.D0.BE.D0.B3_.D0.B8.D0.BC.D0.B5.D0.BD.D0.B0_.D0.B8_.D0.BB.D0.BE.D0.B7.D0.B8.D0.BD.D0.BA.D0.B5)
        *   [4.1.1 Опција 1 - Форсирање гост веза](#.D0.9E.D0.BF.D1.86.D0.B8.D1.98.D0.B0_1_-_.D0.A4.D0.BE.D1.80.D1.81.D0.B8.D1.80.D0.B0.D1.9A.D0.B5_.D0.B3.D0.BE.D1.81.D1.82_.D0.B2.D0.B5.D0.B7.D0.B0)
        *   [4.1.2 Опција 2 - Дозволити готи и корисник везе](#.D0.9E.D0.BF.D1.86.D0.B8.D1.98.D0.B0_2_-_.D0.94.D0.BE.D0.B7.D0.B2.D0.BE.D0.BB.D0.B8.D1.82.D0.B8_.D0.B3.D0.BE.D1.82.D0.B8_.D0.B8_.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D0.BD.D0.B8.D0.BA_.D0.B2.D0.B5.D0.B7.D0.B5)
    *   [4.2 Једноставан конфигурациони фајл](#.D0.88.D0.B5.D0.B4.D0.BD.D0.BE.D1.81.D1.82.D0.B0.D0.B2.D0.B0.D0.BD_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.B8_.D1.84.D0.B0.D1.98.D0.BB)
    *   [4.3 Откривање мрежних дељених фолдера](#.D0.9E.D1.82.D0.BA.D1.80.D0.B8.D0.B2.D0.B0.D1.9A.D0.B5_.D0.BC.D1.80.D0.B5.D0.B6.D0.BD.D0.B8.D1.85_.D0.B4.D0.B5.D1.99.D0.B5.D0.BD.D0.B8.D1.85_.D1.84.D0.BE.D0.BB.D0.B4.D0.B5.D1.80.D0.B0)
    *   [4.4 Удаљена контрола Windows рачунара](#.D0.A3.D0.B4.D0.B0.D1.99.D0.B5.D0.BD.D0.B0_.D0.BA.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D0.B0_Windows_.D1.80.D0.B0.D1.87.D1.83.D0.BD.D0.B0.D1.80.D0.B0)
*   [5 Решавање проблема](#.D0.A0.D0.B5.D1.88.D0.B0.D0.B2.D0.B0.D1.9A.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0)
    *   [5.1 Проблем са приступом фолдеру који је заштићен лозинком из Windows система](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC_.D1.81.D0.B0_.D0.BF.D1.80.D0.B8.D1.81.D1.82.D1.83.D0.BF.D0.BE.D0.BC_.D1.84.D0.BE.D0.BB.D0.B4.D0.B5.D1.80.D1.83_.D0.BA.D0.BE.D1.98.D0.B8_.D1.98.D0.B5_.D0.B7.D0.B0.D1.88.D1.82.D0.B8.D1.9B.D0.B5.D0.BD_.D0.BB.D0.BE.D0.B7.D0.B8.D0.BD.D0.BA.D0.BE.D0.BC_.D0.B8.D0.B7_Windows_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0)
    *   [5.2 Дијалог прозору треба доста времена да се појави](#.D0.94.D0.B8.D1.98.D0.B0.D0.BB.D0.BE.D0.B3_.D0.BF.D1.80.D0.BE.D0.B7.D0.BE.D1.80.D1.83_.D1.82.D1.80.D0.B5.D0.B1.D0.B0_.D0.B4.D0.BE.D1.81.D1.82.D0.B0_.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.B0_.D0.B4.D0.B0_.D1.81.D0.B5_.D0.BF.D0.BE.D1.98.D0.B0.D0.B2.D0.B8)
    *   [5.3 Промене у Samba верзији 3.4.0](#.D0.9F.D1.80.D0.BE.D0.BC.D0.B5.D0.BD.D0.B5_.D1.83_Samba_.D0.B2.D0.B5.D1.80.D0.B7.D0.B8.D1.98.D0.B8_3.4.0)
    *   [5.4 Грешка: Вредност превелика за дефинисани тип податка](#.D0.93.D1.80.D0.B5.D1.88.D0.BA.D0.B0:_.D0.92.D1.80.D0.B5.D0.B4.D0.BD.D0.BE.D1.81.D1.82_.D0.BF.D1.80.D0.B5.D0.B2.D0.B5.D0.BB.D0.B8.D0.BA.D0.B0_.D0.B7.D0.B0_.D0.B4.D0.B5.D1.84.D0.B8.D0.BD.D0.B8.D1.81.D0.B0.D0.BD.D0.B8_.D1.82.D0.B8.D0.BF_.D0.BF.D0.BE.D0.B4.D0.B0.D1.82.D0.BA.D0.B0)
    *   [5.5 Морам да ресетујем samba протокола да би моји дељени фолдери видели остали](#.D0.9C.D0.BE.D1.80.D0.B0.D0.BC_.D0.B4.D0.B0_.D1.80.D0.B5.D1.81.D0.B5.D1.82.D1.83.D1.98.D0.B5.D0.BC_samba_.D0.BF.D1.80.D0.BE.D1.82.D0.BE.D0.BA.D0.BE.D0.BB.D0.B0_.D0.B4.D0.B0_.D0.B1.D0.B8_.D0.BC.D0.BE.D1.98.D0.B8_.D0.B4.D0.B5.D1.99.D0.B5.D0.BD.D0.B8_.D1.84.D0.BE.D0.BB.D0.B4.D0.B5.D1.80.D0.B8_.D0.B2.D0.B8.D0.B4.D0.B5.D0.BB.D0.B8_.D0.BE.D1.81.D1.82.D0.B0.D0.BB.D0.B8)
*   [6 Ресурси](#.D0.A0.D0.B5.D1.81.D1.83.D1.80.D1.81.D0.B8)

## Инсталација

Инсталација само _client_ програма је сувишна за ститеме који не деле фајлове, само приступају дељеним фајловима:

```
# pacman -S smbclient

```

Да би дељене фајлове учинили доступним, потребно је инсталирати Samba _server_ пакет (који ће такође инсталирати и smbclient):

```
# pacman -S samba

```

Daemon је инсталиран са сервереом и мора се покренути да би Samba радила. Samba користи [FAM](/index.php/FAM "FAM") за надгледанје промена у фајл систему, а може да користи и [Gamin](/index.php/Gamin "Gamin"), али Gamin је скоро у потпуности замењен FAM, углваном зато што је FAM лоше одржаван и генерално инфериоран, непопуларан избор.

Gamin се инсталира на следеђи начин:

```
# pacman -S gamin

```

## Конфигурација

`/etc/samba/smb.conf` фајл мора се креирати пре него што се daemon покрене. Кад је подешен, корисници могу да се одлуче за коришћење напредних конфигурационих интерфејса као што је SWAT.

### smb.conf

Као root, копирати подразумевану Samba конфигурацију у `/etc/samba/smb.conf`:

```
# cp /etc/samba/smb.conf.default /etc/samba/smb.conf

```

Отворити `smb.conf` у изменити конфигурациони фајл да одговара нашим потребама. Подразумевани фајл прави дељење за сваки home директоријум сваког корисника. Такође креира и дељење за штампаче.

Више информација о доступним опцијама може се наћи у `man smb.conf`

### Покретање и аутоматизација daemona

Ако се користи FAM, потребно је покренути `fam` [daemon](/index.php/Daemon "Daemon") пре `samba`. Gamin не захтева daemon пошто се аутоматски покреће кад је то неопходно.

Без ресетовања, FAM и Samba могу се поркенути следећим командама:

```
# /etc/rc.d/fam start
# /etc/rc.d/samba start

```

Додати `fam` и `samba` у DAEMONS линију `[rc.conf](/index.php/Rc.conf "Rc.conf")` фајла за аутоматско поркетање daemona приликом бутовања.

### SWAT: Samba веб административна алатка

[SWAT](http://samba.xsec.it/samba/docs/man/Samba-HOWTO-Collection/SWAT.html) је способност Samba сервиса. Главни извршни фајл се зове swat и покреће га eXtended InterNET Daemon, [xinetd](https://en.wikipedia.org/wiki/xinetd "wikipedia:xinetd").

Постоји много различитих мишљења о корисности SWAT алата. Колико год неко покушавао да направи савшени конфигурациони алат, он остаје објекат личног укуса. SWAT је алат који дозвољава веб засновану конфигурацију Samba сервиса. Поседује чаробњака који помаже у брзом конфигурисању Samba сервиса, има помоћ за сваки `smb.conf` параметар, пружа надгледање тренутног стања информација о вези, и дозвоњава MS Windows мрежно управљање лозинкама. [[1]](http://samba.xsec.it/samba/docs/man/Samba-HOWTO-Collection/SWAT.html)

**Note:** Ако имате проблема са овим упутствима, може се користити и [Webmin](/index.php/Webmin "Webmin") алат, и лако учитати SWAT модул овде.

**Warning:** Пре коришћења SWAT алата, SWAT ће у потпуности заменити `smb.conf` са потпуно оптимизованим фајлом који има уклоњене коментаре, и неподразумевана подешавања ће бити уписана.

Да би користили SWAT, прво треба инсталирати xinetd:

```
# pacman -S xinetd

```

Треба изменити `/etc/xinetd.d/swat` коришћењем неког од текстуалних едитора. Да би се омогућио SWAT, треба променити `disable = yes` линију у `disable = no`.

```
service swat
{
        type                    = UNLISTED
        protocol                = tcp
        port                    = 901
        socket_type             = stream
        wait                    = no
        user                    = root
        server                  = /usr/sbin/swat
        log_on_success          += HOST DURATION
        log_on_failure          += HOST
        disable                 = no
}

```

Алтернатива је додавање уноса за swat у `/etc/services` и изоствављање прве три линије конфигурације. Ако је xinetd компајлиран са tcp_wrappers подршком (то је подразумевано код Arch-a), потребно је изменити `/etc/hosts.allow` додавањем следећие линије:

```
swat:127.0.0.1

```

Покретање xinetd daemoa:

```
# /etc/rc.d/xinetd start

```

Веб интерфејсу се може приступити преко порта 901,

```
[http://localhost:901/](http://localhost:901/)

```

### Додавање корисника

Да би се пријавили на Samba дељени фајл морамо додати корисника:

```
# smbpasswd -a <user>

```

Корисник већ мора имати налог на серверу. Ако корисник не постоји стићи ће следећа порука упозорења:

```
Failed to modify password entry for user "<user>"

```

Може се додати нови корисник у Linux хост командом [adduser](/index.php/User_Management#adduser "User Management"). Овај чланак не покрива додавање корисника у Windows системе.

**Note:** smbpasswd се не користи од [Samba version 3.4.0](/index.php/Samba#Changes_in_Samba_version_3.4.0 "Samba")

## Приступ дељеним фајловима

Дељеним ресурсима са других рачунара на локалној мрежи може се приступити и монтирати локано коришћењем корисничког интерфејса (GUI) или конзонлог приступа (CLI). Графички приступ је ограничен. Нека десктоп окружења имају начине олакшавањна приступа дељеним ресурсима. Тачније, већина десктоп окружења и управљача прозора имају неки свој метод.

Постоје два дела дељења приступа. Први је основни механизам фајл система, а други је интерфејс који дозвољава кориснику да изабере дељене ресурсе. Нека окружења први део уграђен у себе.

Како користите KDE, постоји могућност претраге Samba дељених фолдера/фајлова. Нису потребни додатни пакети. (Али, за GUI у KDE системским подешавањима потребно је инсталирати kdenetwork-filesharing пакет из [extra] репозиторијума. Други програм је SMB4K.) Ако, ипак, планирате да делите у Gnome окружењу или из шкољке, потребно је инсталирати додатне пакете.

### Приступ Samba дељеним фолдерима из Gnome окружења

За Gnome, постоји Nautilus. Да би приступили дељеним фајловима преко Nautilusа, неопходно је инсталирати gvfs-smb пакет:

```
# pacman -S gvfs-smb

```

За Nautilus/Dolphin/Konqueror прозоре, притиснути `Ctrl`+`L` или ићи у "Go" мени и изабрати "Location..." -- обе акције ће дозволити да упишете у "Go to:" празно. Унети:

```
smb://servername/share

```

**Note:** Ако немате име сервера у `/etc/hosts`, треба користити IP адресу сервера уместо servername.

Други Gnome претраживач је програм Gnomba.

### Приступ дељеним фајловима из другог графичког окружења

Постоји доста корисних програма, али неопходно је имати пакете направљене за њих. Ово се може урадити коришћењем Arch package build system. Добра ствар је што не захтевају одређено окружење да би се инсталирали, и зато доносе мање пртљага.

LinNeighborhood је неспецифичан кад су у питању десктоп окружење и управњач прозора. То је једноставан генерички X-заснован претраживач локалне мреже. Није леп, али је ефективан.

Други могући програми укључују pyneighborhood и RUmba, као и xffm-samba додатак за Xffm.

### Приступ Samba дељеном фајлу из шкољке

Дељеним фолдерима може се приступити коришћењем аутоматском монтера или коришћењем [manual method](#Manual_share_mounting).

#### Аутоматско монтирањеAutomatic

Постоји неколико алтернатива за лако претраживање дељених фолдера.

##### smbnetfs

1\. Инталирати [smbnetfs](https://www.archlinux.org/packages/?name=smbnetfs):

```
# pacman -S smbnetfs

```

2\. Додати следећу линију у `/etc/fuse.conf`:

```
user_allow_other

```

3\. Учитати `fuse` кернел модул:

```
# modprobe fuse

```

4\. Покренути `smbnetfs` [daemon](/index.php/Daemon "Daemon"):

```
# /etc/rc.d/smbnetfs start

```

Ако је неопходна конфигурација правилно истражена, тврди се да су сви дељени фолдери у мрежи аутоматски монтирани у `/mnt/smbnet`.

Додати следеће у `/etc/rc.conf` за приступ дељеним фолдерима при бутовању:

```
MODULES=(... **fuse** ...)
DAEMONS=(... **smbnetfs** ...)

```

Ако су корисничко име и лозинка неопходни за приступ неким фолдерима, потребно је изменити `/etc/smbnetfs/.smb/smbnetfs.conf` уклањањем коментара који почињу са "auth" и подесити их за своје потребе:

```
auth			"hostname" "username" "password"

```

Онда, можда је неопходно променити дозволе на `/etc/smbnetfs/.smb/smbnetfs.conf` и свим осталим фајловима које smbnetfs укључује да би радило нормално:

```
# chmod 600 /etc/smbnetfs/.smb/smbnetfs.conf

```

##### fusesmb

**Note:** Пошто `smbclient 3.2.X` не функционише са `fusesmb`, вратити се на старију верзију ако је неопходно. Погледати [relevant forum topic](https://bbs.archlinux.org/viewtopic.php?id=58434) за више информација.

1\. Инсталирати [fusesmb](https://aur.archlinux.org/packages/fusesmb/) пакет из [AUR](/index.php/AUR "AUR") репозиторијума.

2\. Креирати тачку монтирања:

```
# mkdir /mnt/fusesmb

```

3\. Учитати `fuse` модул:

```
# modprobe fuse

```

4\. Монтирати дељени фолдер:

```
# fusesmb -o allow_other /mnt/fusesmb

```

За монтирање приликом бутовања, додати команду изнад у `/etc/rc.local` и додати `fuse` модул у `/etc/rc.conf`:

```
MODULES=(... **fuse** ...)

```

##### Autofs

Погледати [Autofs](/index.php/Autofs "Autofs") за информације о кернел-заснованом аутомонтеру за Linux.

#### Ручно монтирање

1\. Користити smbclient за претраживање из шкољке. Да би излистали јавне дељене фолдере на серверу користимо команду:

```
$ smbclient -L <hostname> -U%

```

2\. Креирање тачке монтирања:

```
# mkdir /mnt/MOUNTPOINT

```

3\. Монтирамо дељени фолдер коришћењем `mount.cifs`. Држите до знања да неће све опције бити потребне и пожељне, као што је `password`:

```
# mount -t cifs //_SERVER_/_SHARENAME_ _MOUNTPOINT_ -o user=_USERNAME_,password=_PASSWORD_,workgroup=_WORKGROUP_,ip=_SERVERIP_

```

	`SERVER`

	Име Windows система

	`SHARENAME`

	Дељени директоријум

	`MOUNTPOINT`

	Локални директоријум у којем је монтиран дељени фолдер

	`-o [options]`

	Спецификација опција за `mount.cifs`

	`user`

	Корисничко име које се користило за монтирање

	`password`

	Лозинка дељеног директоријума

	`workgroup`

	Користи се за спецификацију радне групе

	`ip`

	IP адреса сервера -- ако систем није у могућности да нађе Windows рачунар на основу имена (DNS, WINS, hosts унос, итд.)

**Note:** Суздржати се од коришћења (**/**) карактера. Коришћење `//SERVER/SHARENAME**/**` неће радити.

4\. Демонтирање се врши на следећи начин:

```
# umount /mnt/MOUNTPOINT

```

##### Додавање дељеног фолдера у `fstab`

Додати следеће у `/etc/[fstab](/index.php/Fstab "Fstab")` за лако монтирање:

```
//SERVER/SHARENAME /mnt/MOUNTPOINT cifs noauto,noatime,username=USER,password=PASSWORD,workgroup=WORKGROUP 0 0

```

`noauto` опција онемогућава аутоматско монтирање приликом бутовања система и `noatime` повећава перформансе прескакањем inode времена приступа.

После додавања претходне линије, синтакса за монтирање фајлова постаје једноставнија:

```
# mount /mnt/MOUNTPOINT

```

Ако се Samba дељени фолдер додаје у `fstab`, `netfs` daemon треба додати у `[rc.conf](/index.php/Rc.conf "Rc.conf")`, негде после [network](/index.php/Network "Network") daemonа. `netfs` daemon ће монтирати мрежне партиције приликом бутовања и, најважније, демонтирати мрежне партиције при гашењу. Чак и коришћење `noauto` опције у `fstab`, `netfs` daemon се треба користити. Без тога било који мрежни дељени фолдер који је монтиран приликом гашења ће изазвати да `network` daemon чека да веза истекне, и тако повећати време гашења рачунара.

##### Дозвољавање корисницима да монтирају

Пре омогућавања приступа командама за монтирање, `fstab` се мора изменити. Додати `users` опцију за сваки унос у `/etc/fstab`:

```
//SERVER/SHARENAME /path/to/SHAREMOUNT cifs **users**,noauto,noatime,username=USER,password=PASSWORD,workgroup=WORKGROUP 0 0

```

**Note:** Опција је `user**s**` (з множини). За друге фајл системе, ова опција је углавном _user_; без "**s**".

Ово ће дозволити корисницима да монтирају док год постоји тачка монтирања у директоријуму који _контролише_ корисник; нпр. корисников home директоријум. Да би дозволили корисницима да монтирају и демонтирају без тачака монтирања које они не поседују користи се [#smbnetfs](#smbnetfs), или се додељују [sudo](/index.php/Sudo "Sudo") привилегије.

## Савети и трикови

### Дељење фајлова у локалној мрежи без корисничког имена и лозинке

#### Опција 1 - Форсирање гост веза

Изменити `/etc/samba/smb.conf` и изменити следећу линију:

```
security = user

```

з

```
security = share

```

#### Опција 2 - Дозволити готи и корисник везе

Изменити `/etc/samba/smb.conf` и додати следећу линију:

```
map to guest = Bad User

```

после ове линије

```
security = user

```

Ако желите да ограничите дељене податке на специфични интерфејс заменити:

```
;   interfaces = 192.168.12.2/24 192.168.13.2/24

```

са:

```
interfaces = lo eth0
bind interfaces only = true

```

(мењање eth0 у локалну мрежу са којом желите да делите.)

Ако желите да измените налог који приступа дељеним фолдерима изменити следеће линије:

```
;   guest account = nobody

```

Последњи корак је креирање директоријума (за дозволу уписа користити променљиву = yes):

```
[Public Share]
path = /path/to/public/share
available = yes
browsable = yes
public = yes
writable = no

```

### Једноставан конфигурациони фајл

```
[global]
workgroup = WORKGROUP
server string = Samba Server
netbios name = PC_NAME
security = share
; the line below is important! If you have permission issues make
; sure the user here is the same as the user of the folder you
; want to share
guest account = mark
username map = /etc/samba/smbusers
name resolve order = hosts wins bcast
wins support = no

[public]
comment = Public Share
path = /path/to/public/share
available = yes
browsable = yes
public = yes
writable = no

```

### Откривање мрежних дељених фолдера

Ако ништа ије познато о другим системима на локалној мрежи, и аутоматски алат као што је [#smbnetfs](#smbnetfs) није доступан, следеће методе дозвољавају ручно истраживање дељених фолдера.

1\. Прво, инсталирати [nmap](https://www.archlinux.org/packages/?name=nmap) и [smbclient](https://www.archlinux.org/packages/?name=smbclient) користећи [pacman](/index.php/Pacman "Pacman"):

```
# pacman -S nmap smbclient

```

2\. `nmap` проверава који су портови отворени:

```
# nmap -p 139 -sT 192.168.1.*

```

У овом случају, претраживање 192.168.1.* IP адресног опсега и порта 139, резултује:

```
$ nmap -sT 192.168.1.*

```

```
Starting nmap 3.78 ( [http://www.insecure.org/nmap/](http://www.insecure.org/nmap/) ) at 2005-02-15 11:45 PHT
Interesting ports on 192.168.1.1:
(The 1661 ports scanned but not shown below are in state: closed)
PORT     STATE SERVICE
**139/tcp  open  netbios-ssn**
5000/tcp open  UPnP

Interesting ports on 192.168.1.5:
(The 1662 ports scanned but not shown below are in state: closed)
PORT     STATE SERVICE
6000/tcp open  X11

Nmap run completed -- 256 IP addresses (2 hosts up) scanned in 7.255 seconds

```

Први резултат је други систем; други је клијент са ког је претраживање обављено.

3\. Сад кад су системи са отвореним портом 139 откривени, користимо `nmblookup` да проверимо NetBIOS имена:

```
$ nmblookup -A 192.168.1.1

```

```
Looking up status of 192.168.1.1
        PUTER           <00> -         B <ACTIVE>
        HOMENET         <00> - <GROUP> B <ACTIVE>
        PUTER           <03> -         B <ACTIVE>
        **PUTER           <20> -         B <ACTIVE>**
        HOMENET         <1e> - <GROUP> B <ACTIVE>
        USERNAME        <03> -         B <ACTIVE>
        HOMENET         <1d> -         B <ACTIVE>
        MSBROWSE        <01> - <GROUP> B <ACTIVE>

```

Без обзира на излаз, потражити **<20>**, који показује хоста са отвореним услугама.

4\. Користити `smbclient` да излистамо услуге дељене на _PUTER_. Ако тражи лозинку, пристиском на тастер ентер би требало да се прикаже следећа листа:

```
$ smbclient -L \\PUTER

```

```
Sharename       Type      Comment
---------       ----      -------
MY_MUSIC        Disk
SHAREDDOCS      Disk
PRINTER$        Disk
PRINTER         Printer
IPC$            IPC       Remote Inter Process Communication

Server               Comment
---------            -------
PUTER

Workgroup            Master
---------            -------
HOMENET               PUTER

```

Ово приказује који фолдери су дељени и који се могу монтирати локално. Погледати: [#Accessing Samba shares](#Accessing_Samba_shares)

### Удаљена контрола Windows рачунара

Samba нуди групу алата за комуникацију са Windows системима. Ови алати могу бити корисни у случају да не можете да приступите Windows рачунару коришћењем удаљеног радног окружења, као што је приказано у неким примерима.

Послати команду за гашење са коментаром:

```
$ net rpc shutdown -C "comment" -I IPADDRESS -U USERNAME%PASSWORD

```

Ако преферирате принудно гашење уместо тога промените -C са коментаром на једно -f. За ресетовање додати -r, праћено -C или -f.

Заустављање и покретање услуге:

```
$ net rpc service stop SERVICENAME -I IPADDRESS -U USERNAME%PASSWORD

```

Да видимо све могуће net rpc команде:

```
$ net rpc

```

## Решавање проблема

### Проблем са приступом фолдеру који је заштићен лозинком из Windows система

Ако имате проблема са приступом фолдеру који је заштићен лозинком из Windows система, пробајте да додате ово у `/etc/samba/smb.conf`:[[2]](http://blogs.computerworld.com/networking_nightmare_ii_adding_linux)

Обратите пажњи да ово додате у ваш **локални** smb.conf, не на smb.conf сервера

```
[global]
# lanman fix
client lanman auth = yes
client ntlmv2 auth = no

```

### Дијалог прозору треба доста времена да се појави

Имао сам проблем да је дијалог прозору потребно око 30 секунди да се појави при покушају да се повежем на Windows XP/Windows 7 систем. Анализирањем error.log на серверу приметио сам следеће:

```
[2009/11/11 06:20:12,  0] printing/print_cups.c:cups_connect(103)
Unable to connect to CUPS server localhost:631 - Interrupted system call

```

Пошто немам штампач на серверу, додао сам следеће у глобални део конфигурације:

```
load printers = no
printing = bsd
disable spoolss = yes
printcap name = /dev/null

```

### Промене у Samba верзији 3.4.0

[Веће промене у Samba 3.4.0](http://www.samba.org/samba/history/samba-3.4.0.html) укључују:

Подразумевана passdb грешка је промењена на 'tdbsam'! То прекида постојећа подешавања која користе 'smbpasswd' грешку без експлицитне декларације!

Ако желите да се држите 'smbpasswd' грешке пробајте да промените ово у `/etc/samba/smb.conf`:

```
passdb backend = smbpasswd

```

или конвертујте ваше smbpasswd уносе коришћењем:

```
sudo pdbedit -i smbpasswd -e tdbsam

```

### Грешка: Вредност превелика за дефинисани тип податка

Са неким апликацијама можете добити ову грешку кад покушате да отворите монтирани фајл у smbfs/cifs:

```
 Value too large for defined data type

```

Решење[[3]](https://bugs.launchpad.net/ubuntu/+bug/479266/comments/5) је додати ову опцију у ваше smbfs/cifs опције за монтирање (у /etc/fstab на пример):

```
 ,nounix,noserverino

```

_Ради на Arch Linux систему закључно са датумом (2009-12-02)_

### Морам да ресетујем samba протокола да би моји дељени фолдери видели остали

Ако приликом покретања рачунара, samba дељеним фолдерима не може приступити, проверити следеће:

*   Уверите се да нисте заборавили да додате samba daemon у DAEMONS одељак /etc/rc.conf фајла (после 'network' daemona)
*   _network_ услуга није покренута у позадити (са префиксом @ ). Уклањање '@' испред 'network' може да среди овај проблем. Ресетовати рачунар да проверите.

## Ресурси

*   [Samba официјални сајт](http://www.samba.org/)
*   [Samba: представљање](http://www.samba.org/samba/docs/SambaIntro.html)