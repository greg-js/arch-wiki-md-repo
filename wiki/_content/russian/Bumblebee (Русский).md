**Примечание:** пожалуйста сообщите об ошибках на [Bumblebee-Project](https://github.com/Bumblebee-Project/Bumblebee)'s GitHub как описано в [Wiki](https://github.com/Bumblebee-Project/Bumblebee/wiki/Reporting-Issues).

_Bumblebee это решение, позволяющее задействовать гибридную графику с Nvidia Optimus. Основатель проекта Martin Juhl_

## Contents

*   [1 О Bumblebee](#.D0.9E_Bumblebee)
    *   [1.1 Как это работает](#.D0.9A.D0.B0.D0.BA_.D1.8D.D1.82.D0.BE_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82)
*   [2 Сведения об установке](#.D0.A1.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BE.D0.B1_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B5)
    *   [2.1 Использование драйвера Nvidia](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0_Nvidia)
    *   [2.2 Использование драйвера Nouveau](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80.D0.B0_Nouveau)
*   [3 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [3.1 Загрузка модулей ядра](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9_.D1.8F.D0.B4.D1.80.D0.B0)
        *   [3.1.1 Использование Nvidia](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Nvidia)
        *   [3.1.2 Nouveau](#Nouveau)
    *   [3.2 Установка X Server](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_X_Server)
    *   [3.3 Разрешить использование Bumblebee](#.D0.A0.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B8.D1.82.D1.8C_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Bumblebee)
    *   [3.4 Запуск демона Bumblebee](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B4.D0.B5.D0.BC.D0.BE.D0.BD.D0.B0_Bumblebee)
*   [4 Тестирование Bumblebee](#.D0.A2.D0.B5.D1.81.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Bumblebee)
*   [5 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
    *   [5.1 Compression and VGL Transport](#Compression_and_VGL_Transport)
    *   [5.2 Server Behavior Configuration](#Server_Behavior_Configuration)
*   [6 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [7 Управление питанием](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B8.D1.82.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC)
    *   [7.1 Небольшое примечание относительно удаления функции](#.D0.9D.D0.B5.D0.B1.D0.BE.D0.BB.D1.8C.D1.88.D0.BE.D0.B5_.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BE.D1.82.D0.BD.D0.BE.D1.81.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE_.D1.83.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D1.84.D1.83.D0.BD.D0.BA.D1.86.D0.B8.D0.B8)
    *   [7.2 Включение управления питанием](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D0.B8.D1.82.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC)
*   [8 Поиск неисправностей](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_.D0.BD.D0.B5.D0.B8.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BD.D0.BE.D1.81.D1.82.D0.B5.D0.B9)
    *   [8.1 VirtualGL не находит дисплей](#VirtualGL_.D0.BD.D0.B5_.D0.BD.D0.B0.D1.85.D0.BE.D0.B4.D0.B8.D1.82_.D0.B4.D0.B8.D1.81.D0.BF.D0.BB.D0.B5.D0.B9)
*   [9 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## О Bumblebee

[Optimus](http://www.nvidia.com/object/optimus_technology.html) реализует [технологию гибридной графики](http://hybrid-graphics-linux.tuxfamily.org/index.php?title=Hybrid_graphics) без аппаратного multiplexer. Интегрированная карта GPU берёт на себя управление, когда ноутбук работает от батареи, так лучше для энергосбережения. Дискретную карту следует использовать, когда вы запускаете требовательные приложения.

Bumblebee это программное решение, базирующееся на VirtualGL и драйверах ядра, позволяющее использовать дискретный GPU, не имеющий физического подключения к экрану.

### Как это работает

Bumblebee пытается подражать поведению Optimus; использует дискретный GPU для рендеринга когда это необходимо, и отключает питание дискретного GPU когда он не используется. Нынешние релизы поддерживают только рендеринг, управление питанием в процессе разработки.

Дискретная видеокарта Nvidia использует отдельный X сервер, присоединенный к "виртуальному" дисплею (дисплей сконфигурирован, но не используется). Второй сервер вызывается с помощью VirtualGL, как будто это удаленный X сервер. Это означает, что вам необходимо проделать несколько шагов по установке драйверов ядра, дополнительного X сервера и демона.

## Сведения об установке

Пакет AUR [bumblebee](https://aur.archlinux.org/packages.php?K=bumblebee&SeB=x) является стабильной версией и использует проприетарный драйвер Nvidia по умолчанию.

Также имеется версия git ([bumblebee-git](https://aur.archlinux.org/packages.php?K=bumblebee-git&SeB=x)) , которая может использовать любой драйвер: Nvidia или Nouveau. It is a checkout of the develop branch of the GitHub repository.

Для использование 32-битных приложений на 64-битной системе вам следует задействовать [lib32-virtualgl](https://aur.archlinux.org/packages.php?K=lib32-virtualgl&SeB=x) вместе с другими специфичными приложениями 32-битных библиотек.

**Примечание:** Если вы установили bumblebee из репозитория GitHub, используя установщик, запустите деинсталлятор прежде чем устанавливать пакет из AUR

Версии>= 2.3 работают с демоном старта /останова X сервера, но не будут контролировать питание карты по умолчанию.

### Использование драйвера Nvidia

Если вы установили git версию bumblebee, вы должны установить дополнительные пакеты, чтобы запустить его с драйвером Nvidia

*   [nvidia-utils-bumblebee](https://aur.archlinux.org/packages.php?K=nvidia-utils-bumblebee&SeB=x) содержит бинарный пакет Nvidia, который не будет конфликтовать с [libgl](https://www.archlinux.org/packages/?name=libgl)
*   [lib32-nvidia-utils-bumblebee](https://aur.archlinux.org/packages.php?K=lib32-nvidia-utils-bumblebee&SeB=x) содержит 32-битный бинарный пакет Nvidia, не вызывающий конфликтов с [libgl](https://www.archlinux.org/packages/?name=libgl)

### Использование драйвера Nouveau

Для использования драйвера [Nouveau](https://wiki.archlinux.org/index.php/Nouveau) вы должны инсталлировать git версию Bumblebee и некоторые дополнительные пакеты:

*   [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) экспериментальный 3D драйвер
*   [nouveau-dri](https://www.archlinux.org/packages/?name=nouveau-dri) классический Mesa DRI + Gallium3D drivers
*   [mesa](https://www.archlinux.org/packages/?name=mesa) библиотеки Mesa 3-D

Чтобы это работало:

`# pacman -S xf86-video-nouveau nouveau-dri mesa`

## Установка

Для того, чтобы Bumblebee мог функционировать на вашем компьютере, вам необходимо настроить второй X сервер, загрузить нужные модули ядра и запустить демон bumblebee. Большая часть этого делается автоматически при установке.

### Загрузка модулей ядра

#### Использование Nvidia

Для того, чтобы Bumblebee использовал проприетарные модули Nvidia, вам нужно сначала выгрузить модуль ядра Nouveau. Для этого запустите в терминале:

`# rmmod nouveau`

Добавьте в /etc/modprobe.d/modprobe.conf строки, выключающие Nouveau при загрузке:

/etc/modprobe.d/modprobe.conf

 `blacklist nouveau` 

Теперь загрузите модуль Nvidia:

`# modprobe nvidia`

Если вы хотите, чтобы модуль был загружен при старте, добавьте Nvidia в секцию MODULES в ваш файл /etc/rc.conf:

```
MODULES=(... nvidia ...)

```

#### Nouveau

Убедитесь, что драйвер Nouveau не добавлен в blacklist в файле /etc/modprobe.d/. Модуль ядра Nouveau загрузится по умолчанию.

### Установка X Server

При инсталляци должны быть распознаны ваши графические карты и их PCI BusID. Если вы заметили предупреждения относительно этого во время установки, следуйте указаниям ниже.

После установки файл /etc/bumblebee/xorg.conf.DRIVER будет содержать минимальную конфигурацию устройств (где DRIVER может бытьnouveau или nvidia). В этот файл вам нужно вписать индивидуальный адрес PCI шины вашей карты. Чтобы получить его, введите в терминале:

`$ lspci -d10de: -nn | grep '030[02]'`

 `01:00.0 VGA compatible controller [0300]: nVidia Corporation GT218 [GeForce 310M] [10de:0a75] (rev a2)` 

Обратите внимание на PCI адрес карты (01:00.0 в примере) и отредактируйте строку в /etc/bumblebee/xorg.conf.DRIVER с указанной опцией BusID в секции Device:

/etc/bumblebee/xorg.conf.DRIVER

```
...
Section "Device"
...
    BusID          "PCI:01:00:0"
...
EndSection
...

```

**Примечание:** вам нужно заменить любые точки (.) на двоеточие (:) чтобы X сервер воспринял ваш BusID

Если вы используете драйвер Nvidia, взгляните на секцию "Files" и проверьте, чтобы путь к модулю был правильным:

/etc/bumblebee/xorg.conf.nvidia

```
...
Section "Files"
    ModulePath "/usr/lib/nvidia-bumblebee,/usr/lib/xorg/modules"
EndSection
...

```

### Разрешить использование Bumblebee

Разрешение на использование optirun даётся всем пользователям группы 'bumblebee', так что добавьте себя (и других пользователей, которым нужен bumblebee) в эту группу:

`# usermod -a -G bumblebee <user>`

где<user> имя пользователя, который будет добавлен. Затем выйдите из системы, чтобы изменения вступили в силу.

### Запуск демона Bumblebee

Bumblebee запускает демон для старта вторичного X сервера и управляет некоторыми привилегированными функциями, для его запуска просто скомандуйте:

`# systemctl start bumblebeed.service`

Чтобы старт происходил при загрузке системы выполните:

```
# systemctl enable bumblebeed.service

```

Для отключения автозапуска выполните:

```
# systemctl disable bumblebeed.service 

```

Чтобы увидеть состояние демона, скомандуйте:

```
# systemctl status bumblebeed.service

```

## Тестирование Bumblebee

Вы можете протестировать Bumblebee командой:

`$ optirun glxgears`

Если это сработает, вы в состоянии управлять картой.

**Примечание:**вам будет нужен пакет [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) для запуска glxgears. This is not a benchmarking test, only indicates that the dedicated GPU is rendering.

## Конфигурация

Вы можете исправить некоторые переменные в файле/etc/bumblebee/bumblebee.conf. По умолчанию он выглядит так:

/etc/bumblebee/bumblebee.conf

```
STOP_SERVICE_ON_EXIT=N
X_SERVER_TIMEOUT=10
VGL_DISPLAY=:8
DRIVER=nvidia
X_CONFFILE=
BUMBLEBEE_GROUP=bumblebee
ENABLE_POWER_MANAGEMENT=N
VGL_COMPRESS=proxy
ECO_MODE=N
FALLBACK_START=N

```

### Compression and VGL Transport

Compression and transport regards how the frames are compressed in the server side (bumblebee X server), then transported to the client side (main X server) and uncompressed to be displayed in the application window. It mostly will affect performance in the GPU/GPU usage, as the transport is unlimited in bandwidth. Compressed methods (such as jpeg) will load the CPU the most but will load GPU the minimum necessary; uncompressed methods loads the most on GPU and the CPU will have the minimum load possible.

**Note:** CPU frequency scaling will affect directly on render performance

вы можете испробовать разные методы сжатия, добавив аргумент -c к команде optirun и посмотреть, какая подходит вам больше:

`$ optirun -c <compress-method> /opt/VirtualGL/bin/glxspheres`

 `Bumblebee будет передавать кадры с помощью: <compress-method>` 

где <compress-method>может бытьjpeg, xv, proxy, rgbилиyuv. Тогда вы сможете заменить одну из переменных VGL_COMPRESS в /etc/bumblebee/bumblebee.conf, используемых по умолчанию.

**Примечание:** методы proxy и xv показывают низкую частоту кадров, но в некоторых приложениях работают лучше.

### Server Behavior Configuration

Есть три переменные для управления optirun

```
STOP_SERVICE_ON_EXIT
X_SERVER_TIMEOUT
FALLBACK_START

```

X сервер стартует не сразу, если вы обратились к ним впервые. Старт должен происходить за секунду или около того, если время последующих вызовов слишком большое, установите STOP_SERVICE_ON_EXITвN и Bumblebee X сервер не будет остановлен, когда последний optirun отключен.

X_SERVER_TIMEOUT управляет временем ожидания X сервера. Если X серверу требуется время для запуска, вы можете уувеличить значение параметра, в противном случае запуск сервера может не произойти.

If you want the application to start in the integrated GPU if the X server is not available, set FALLBACK_START to Y. This will print the same message when the server is not available but will not fail to launch the program.

## Использование

Для запуска приложений, использующих графическую карту:

`$ optirun [опции] <приложение> [параметры приложения]`

Для просмотра списка опций optirun запустите:

`$ optirun --help`

Если вам нужно запустить 32-битное приложение на 64-битной системе, вы можете установить пакет библиотек 'lib32'.

## Управление питанием

**Внимание:** Эта функция была удалена до тех пор, пока не будет найдено полное и безопасное решение. Однако есть несколько способов, включенных в bumblebee>=2.4.0. Для получения подробной информации смотрите [здесь](https://github.com/Bumblebee-Project/Bumblebee/wiki/ACPI-Removed)

Целью управления питанием является отключение дискретной видео карты, когда вы не используете ресурсоёмкие приложения и её активацию, когда это необходимо. Сейчас вы можете переключать карты вручную, автоматическое переключение не работает по умолчанию.

### Небольшое примечание относительно удаления функции

Управление питанием временно недоступно, поскольку Bumblebee допускает ошибки при работе с ACPI. Вот некоторые из побочных эффектов:

*   - "FATAL: Error inserting nvidia (.../nvidia.ko): Нет такого устройства " ошибка при загрузке модуля nvidia
*   - Зависания во время загрузки, выключения или сна
*   - Приложение может изменить настройки BIOS
*   - Другие операционные системы больше не определяют графическую карту

В следующих версиях управление питанием может быть восстановлено.

Один из разработчиков говорит следующее об управлении питанием bumblebee:

**Lekensteyn**

> Okay, let's assume a building with dirty windows. You'd like to see more sun and therefore asks a worker to hire someone to get that job done. The worker has never learnt how to clean a dirty window properly, but guess that a rock might be the right way to do it. He asks a kid to try cleaning the window with a rock. Now, different things may happen:
> 
> 1.  the window gets scratched and it even gets more darky
> 2.  the window breaks and the sun can shine
> 
> In the first case, it has gotten worse. That's the "Module not found" horror and suspend/lock-up issues. In the second case, you won't guess that something is wrong because you achieved your goal: the sunshine is better. Anyway, the right solution is obviously cleaning the window with a cloth but not before the window is repaired, which is our current task.

The ACPI call methods are rocks and "you" is you. The kid is just a messenger, the acpi_call module. That worker is the Bumblebee developer team.

### Включение управления питанием

Начиная с версии 2.4.0 Bumblebee позволяет работать с ACP при помощи модуляacpi_call. Вы можете использовать пакет [acpi_call-git](https://aur.archlinux.org/packages.php?K=acpi_call-git&SeB=x).

**Внимание:** указанные выше проблемы всё ещё могут происходить, хотя этот метод более безопасен, если вы уверены, что хотите включить управление питанием, ниже показано, как это сделать.

Сначала отредактируйте /etc/bumblebee/bumblebee.confи установитеSTOP_SERVICE_ON_EXITсY, так X сервер будет остановлен, когда optirun не работает.

/etc/bumblebee/bumblebee.conf

```
...
STOP_SERVICE_ON_EXIT=Y
...

```

Теперь вы можете создать два файла (/etc/bumblebee/cardonи/etc/bumblebee/cardoff), содержащих настройки включения и отключения видео карты. Каждая строка должна содержать установку, комментарии не допускаются. Запишите ваши установки по одной на строку, кроме них не должно быть ничего, иначе это может привести к ошибкам:

/etc/bumblebee/cardon

```
\_SB.PCI0.RP00.VGA._DSM {0x01,0x02} 0x03 0x04 {0x1,0x0,0x0,0x3}
\_SB.PCI0.RP00.VGA._PS0

```

**Примечание:** the file must end in a newline, otherwise the last line is omitted

**Внимание:** Указанные установки весьма приблизительны и могут не работать на вашей машине. Вы можете найти больше [здесь](http://hybrid-graphics-linux.tuxfamily.org/index.php?title=ACPI_calls) (непроверено и ненадёжно).

Наконец, включите управление питанием, отредактировав /etc/bumblebee/bumblebee.conf:

/etc/bumblebee/bumblebee.conf

```
...
ENABLE_POWER_MANAGEMENT=Y
...

```

Вы можете рестартовать демон или перезагрузиться для того, чтобы настройки вступили в силу.

## Поиск неисправностей

Это пример поиска неисправностей, если проблема останется, сообщите об ошибках [здесь](https://github.com/Bumblebee-Project/Bumblebee).

### VirtualGL не находит дисплей

Если вы видите сообщение, похожее на это

```
[VGL] ERROR: Could not open display :XX

```

значит вторичный X сервер не работает или не запускается. Для поиска ошибок посмотрите файл /var/log/Xorg.XX.log , где 'XX' это номер дисплея, используемого bumblebee, также обратите внимание на сообщения в /var/log/bumblebee.log.

Вот кое-что, что вы можете попробовать сделать:

*   Проверьте загружен ли модуль nvidia командой "lspci -k"
*   Проверьте файл /etc/bumblebee/xorg.conf.nvidia и посмотрите соответствует ли значение опции "BusID" вашей PCI шине.
*   Проверьте опцию "ConnectedMonitor" в "DFP-0"или"CRT-0" (или "DFP,CRT"). Это должно быть верно для различных ноутбуков с "LVDS"
*   Попробуйте установить опцию _X_SERVER_TIMEOUT_ в более высокое значение, если X сервер запускается, но далеко не сразу становится доступен.

## Смотрите также

*   [Bumblebee Project repository](https://github.com/Bumblebee-Project/Bumblebee)