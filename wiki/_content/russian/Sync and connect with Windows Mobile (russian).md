Эта страница является руководством по подключению вашего устройства Windows Mobile к Archlinux, после прочтения которого вы сможете подключать и синхронизировать ваше мобильное устройство так же, как и в Windows. Для достижения этой цели используется [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)")-приложение [synce-kde](https://aur.archlinux.org/packages/synce-kde/), но пользователи [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") и *box могут не беспокоиться: его [qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)")-зависимости очень маленькие.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Подключение к телефону](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA_.D1.82.D0.B5.D0.BB.D0.B5.D1.84.D0.BE.D0.BD.D1.83)
*   [3 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
*   [4 Other problems](#Other_problems)
*   [5 Work with PocketPC files from file manager](#Work_with_PocketPC_files_from_file_manager)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") следующие пакеты:

1.  [synce-odccm](https://aur.archlinux.org/packages/synce-odccm/)
2.  [synce-kde](https://aur.archlinux.org/packages/synce-kde/)
3.  [synce-sync-engine](https://www.archlinux.org/packages/?name=synce-sync-engine)

## Подключение к телефону

1.  Запустите *odccm*: `# odccm` 
2.  Запустите *sync-engine*. Вы можете использовать опцию `-d` для запуска в фоновом режиме в качестве [демона](/index.php/Daemons_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Daemons (Русский)")
3.  Запустите *synce-kpm*
4.  Подключите свой телефон

Теперь вы можете подключить и синхронизировать свой телефон через кабель. Перед синхронизацией вы должны создать "партнёрство" со своим телефоном, используя ActiveSync. Точно так же, как и в Windows.

## Решение проблем

Если ваше устройство не обнаруживается в *synce-kpm*, убедитесь, что в настройках синхронизации включена опция "ActiveSync", а не "Mass Storage Device" или подобная (Настройки - Подключения - USB подключения).

## Other problems

There is only one problem I have experienced with this. Sometimes it will stop working, and you will get an error report on your phone saying device.exe had a problem and was teminated. To fix this, simply go to USB-connection setting, choose "mass storage device" and select Ok, and then select "active sync" and again ok.

If the above did not work, you might have to quit/kill sync-engine and odccm, and restart them. Start odccm first. This seems to be necessary when sync-engine is stuck at " Authorization pending - waiting for password on device" You will get output if you start sync-engine without the -d option.

I think this problem arises after the phone has suspended, but I'm not quite sure what really causes it.

## Work with PocketPC files from file manager

There is a [SynCE FS](http://www.lvivier.info/SynceFS/) project, which is aimed to provide a possibility to work with winmobile device filesystem as a remote filesystem. It ts based on [SynCE](http://synce.sourceforge.net) and [Coda](http://www.coda.cs.cmu.edu/).

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [syncefs](https://aur.archlinux.org/packages/syncefs/). To use SynCE FS, you need a working SynCE installation.

At the first step you need to load `coda` [модуль ядра](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel modules (Русский)").

At the next step you need to start SynCE tools: `odccm` and `sync-engine`.

Finally you can mount your PocketPC filesystem with a command:

 `mount /mnt/synce` 

(Directory /mnt/synce is normally created during installation. If not - please create it manually.)

Now you can use your PocketPC filesystem from /mnt/synce directory.

**Tip:**

To mount PocketPC filesystem as ordinal user (non-root), you need to add the following to your fstab:

 `none /mnt/synce cefs rw,user,noauto,codadev=/dev/cfs0 0 0`