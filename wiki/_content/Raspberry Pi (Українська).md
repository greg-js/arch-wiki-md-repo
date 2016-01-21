# Raspberry Pi (Українська)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

З [Wikipedia](https://en.wikipedia.org/wiki/Raspberry_Pi "wikipedia:Raspberry Pi"):

"_Raspberry Pi - це одноплатний комп'ютер, розроблений британським фондом Raspberry Pi Foundation. Його головне призначення — стимулювати навчання базовим комп'ютерним наукам у школах._"

Оригінальні моделі, випущені в 2012, базувалися на процесорі Broadcom SoC BCM2835 ([ARM11 architecture](https://en.wikipedia.org/wiki/ARM11 "wikipedia:ARM11")). Модель Raspberry Pi 2, випущена в 2015, продавалася з процесором BCM2836 SoC (4-ядерному [ARM Cortex-A7 architecture](https://en.wikipedia.org/wiki/ARM_Cortex-A7 "wikipedia:ARM Cortex-A7")).

## Contents

*   [1 Передмова](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B4.D0.BC.D0.BE.D0.B2.D0.B0)
*   [2 Системна архітектура](#.D0.A1.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D0.B0_.D0.B0.D1.80.D1.85.D1.96.D1.82.D0.B5.D0.BA.D1.82.D1.83.D1.80.D0.B0)
*   [3 Продуктивність SD-карти](#.D0.9F.D1.80.D0.BE.D0.B4.D1.83.D0.BA.D1.82.D0.B8.D0.B2.D0.BD.D1.96.D1.81.D1.82.D1.8C_SD-.D0.BA.D0.B0.D1.80.D1.82.D0.B8)
    *   [3.1 Включення перевірки fsck під час запуску](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.BD.D1.8F_.D0.BF.D0.B5.D1.80.D0.B5.D0.B2.D1.96.D1.80.D0.BA.D0.B8_fsck_.D0.BF.D1.96.D0.B4_.D1.87.D0.B0.D1.81_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D1.83)
*   [4 Встановлення Arch Linux ARM](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_Arch_Linux_ARM)
*   [5 Мережа](#.D0.9C.D0.B5.D1.80.D0.B5.D0.B6.D0.B0)
    *   [5.1 Налаштування WLAN без ethernet](#.D0.9D.D0.B0.D0.BB.D0.B0.D1.88.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_WLAN_.D0.B1.D0.B5.D0.B7_ethernet)
*   [6 Аудіо](#.D0.90.D1.83.D0.B4.D1.96.D0.BE)
    *   [6.1 Застереження щодо HDMI аудіо](#.D0.97.D0.B0.D1.81.D1.82.D0.B5.D1.80.D0.B5.D0.B6.D0.B5.D0.BD.D0.BD.D1.8F_.D1.89.D0.BE.D0.B4.D0.BE_HDMI_.D0.B0.D1.83.D0.B4.D1.96.D0.BE)
*   [7 Відео](#.D0.92.D1.96.D0.B4.D0.B5.D0.BE)
    *   [7.1 HDMI / аналоговий вихід TV-Out](#HDMI_.2F_.D0.B0.D0.BD.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2.D0.B8.D0.B9_.D0.B2.D0.B8.D1.85.D1.96.D0.B4_TV-Out)
    *   [7.2 Застереження щодо аналогового виводу TV-Out](#.D0.97.D0.B0.D1.81.D1.82.D0.B5.D1.80.D0.B5.D0.B6.D0.B5.D0.BD.D0.BD.D1.8F_.D1.89.D0.BE.D0.B4.D0.BE_.D0.B0.D0.BD.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D0.B2.D0.B8.D0.B2.D0.BE.D0.B4.D1.83_TV-Out)
    *   [7.3 Драйвер X.org](#.D0.94.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80_X.org)
*   [8 Сенсори на платі](#.D0.A1.D0.B5.D0.BD.D1.81.D0.BE.D1.80.D0.B8_.D0.BD.D0.B0_.D0.BF.D0.BB.D0.B0.D1.82.D1.96)
    *   [8.1 Температура](#.D0.A2.D0.B5.D0.BC.D0.BF.D0.B5.D1.80.D0.B0.D1.82.D1.83.D1.80.D0.B0)
    *   [8.2 Напруга](#.D0.9D.D0.B0.D0.BF.D1.80.D1.83.D0.B3.D0.B0)
    *   [8.3 Легкий пакет для моніторингу](#.D0.9B.D0.B5.D0.B3.D0.BA.D0.B8.D0.B9_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82_.D0.B4.D0.BB.D1.8F_.D0.BC.D0.BE.D0.BD.D1.96.D1.82.D0.BE.D1.80.D0.B8.D0.BD.D0.B3.D1.83)
*   [9 Розгін процесора](#.D0.A0.D0.BE.D0.B7.D0.B3.D1.96.D0.BD_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D0.BE.D1.80.D0.B0)
*   [10 Серійна консоль](#.D0.A1.D0.B5.D1.80.D1.96.D0.B9.D0.BD.D0.B0_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C)
*   [11 Модуль камери для Raspberry Pi](#.D0.9C.D0.BE.D0.B4.D1.83.D0.BB.D1.8C_.D0.BA.D0.B0.D0.BC.D0.B5.D1.80.D0.B8_.D0.B4.D0.BB.D1.8F_Raspberry_Pi)
*   [12 Апаратний генератор випадкових чисел](#.D0.90.D0.BF.D0.B0.D1.80.D0.B0.D1.82.D0.BD.D0.B8.D0.B9_.D0.B3.D0.B5.D0.BD.D0.B5.D1.80.D0.B0.D1.82.D0.BE.D1.80_.D0.B2.D0.B8.D0.BF.D0.B0.D0.B4.D0.BA.D0.BE.D0.B2.D0.B8.D1.85_.D1.87.D0.B8.D1.81.D0.B5.D0.BB)
*   [13 GPIO](#GPIO)
    *   [13.1 SPI](#SPI)
    *   [13.2 Python](#Python)
*   [14 I2C](#I2C)
*   [15 Дивіться також](#.D0.94.D0.B8.D0.B2.D1.96.D1.82.D1.8C.D1.81.D1.8F_.D1.82.D0.B0.D0.BA.D0.BE.D0.B6)

## Передмова

Ця стаття не є путівником по встановленню і припускає, що читач уже має встановлену систему Arch. Початківцям бажано прочитати [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide"), де описано початкові завдання, як створення користувачів, керування системою, етс.

**Note:** Підтримка для архітектури ARM представлена на сторінці [http://archlinuxarm.org](http://archlinuxarm.org), а не через повідомлення на офіційному форумі Arch Linux. Будь-які повідомлення, які стосуються специфічних проблем, пов'язаних з ARM, будуть закриті в зв'язку з [Arch Linux distribution support ONLY](/index.php/Forum_etiquette#Arch_Linux_distribution_support_ONLY "Forum etiquette") policy.

## Системна архітектура

Raspberry Pi базується на ARM, а тому потребує виконувальних файлів, які зібрані для цієї архітектури. Ці файли можна знайти сторінці проекту [Arch Linux ARM project](http://archlinuxarm.org/about), який містить порти Arch Linux для пристроїв на базі ARM. Ці пристрої мають свою спільноту і форум на їхній сторінці. Офіційний форум Archlinux _не_ підтримує специфічні проблеми ARM. З впровадженням Raspberry Pi 2 пакунки тепер залежать від відповідної архітектури:

*   ARMv6 (BCM2835): Raspberry Pi Model A, A+, B, B+, Zero
*   ARMv7 (BCM2836): Raspberry Pi 2 (базується на моделі B+)

## Продуктивність SD-карти

Швидкість реагування системи, особливо під час операцій, пов'язаних з інтенсивним використання диску, таких як оновлення системи, можуть дуже залежати від низької якості/повільності пристроїв SD-карт. Це проявляється як [часті, часто довгі паузи](http://archlinuxarm.org/forum/viewtopic.php?f=64&t=9467), коли pacman записує файли до файлової системи. Паузи не спричинені заповненням шини RPi або RPi2, а, швидше за все, слабою пропускною здатністю повільної SD (або мікро SD) карти. Більше про це дивіться [Benchmarking#Flash media](/index.php/Benchmarking#Flash_media "Benchmarking").

Продуктивність і швидкість реагування системи в цілому можна поліпшити шляхом внесення змін в конфігурацію системи. Більше про це дивіться [Maximizing performance](/index.php/Maximizing_performance "Maximizing performance") та [SSD#Tips for minimizing disk reads/writes](/index.php/SSD#Tips_for_minimizing_disk_reads.2Fwrites "SSD").

### Включення перевірки fsck під час запуску

Скористайтесь з порад [fsck#Boot time checking](/index.php/Fsck#Boot_time_checking "Fsck"). Пам'ятайте, що параметри ядра вказуються у файлі `/boot/cmdline.txt`.

## Встановлення Arch Linux ARM

Дивіться [документацію по Arch Linux ARM Pi](http://archlinuxarm.org/platforms/armv6/raspberry-pi) або [документацію по Arch Linux ARM Pi2](http://archlinuxarm.org/platforms/armv7/broadcom/raspberry-pi-2).

## Мережа

Типова інсталяція Archlinux містить вже готові налаштування мережі в dhcp режимі за допомогою [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"), яке дозволяє доступ до офіційного встановлення через [Secure Shell](/index.php/Secure_Shell "Secure Shell"). Пароль користувача root є "root" і його потрібно негайно змінити і, за бажанням, налаштувати [SSH keys](/index.php/SSH_keys "SSH keys").

### Налаштування WLAN без ethernet

Користувачі, які бажають налаштувати безпровідну мережу, повинні використати демон безпровідної мережі, такий як [WPA supplicant](/index.php/WPA_supplicant "WPA supplicant"). Використайте [wireless section](/index.php/Beginners%27_guide#Wireless "Beginners' guide") Путівника початківця для додаткової інформації.

## Аудіо

Пакунок [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) має поставити потрібні програми для використання звуку. Типову гучність можна підлаштувати, використовуючи `alsamixer`.

**Приклад:** Переконайтесь, що єдине джерело звуку "PCM" не заглушене (позначено як `MM` коли заглушене, натисніть `M` щоб включити).

Виберіть джерело аудіо для виводу:

```
$ amixer cset numid=3 _x_

```

Тут `_x_` може приймати такі значення:

*   0 для Авто
*   1 для аналогового виводу
*   2 для HDMI

### Застереження щодо HDMI аудіо

Деякі програми вимагають налаштування файлу `/boot/config.txt` для форсування виводу звуку через HDMI:

```
hdmi_drive=2

```

## Відео

### HDMI / аналоговий вихід TV-Out

В типовій конфігурації Raspberry Pi використовує HDMI відео, якщо під'єднано [HDMI](https://en.wikipedia.org/wiki/HDMI "wikipedia:HDMI") монітор. В протилежному випадку для виводу відео використовується аналоговий вихід TV-Out (також відомий як композитний вихід або RCA)

Щоб перемикатися між HDMI та аналоговим TV-Out використовуйте програму

```
/opt/vc/bin/tvservice

```

Використовуйте параметр _-s_ для перевірки статусу виводу; параметр _-o_ виключить дисплей і параметр _-p_ включить вихід HDMI з вибраними налаштуваннями.

Підлаштування можливо знадобиться для виправлення властивого пересканування/недосканування і легко досягається правкою файлу `boot/config.txt`, в якому налаштовується багато параметрів. Для корекції просто відкоментуйте відповідні стрічки і налаштуйте згідно інструкції в коментарях:

```
# uncomment the following to adjust overscan. Use positive numbers if console
# goes off screen, and negative if there is too much border
#overscan_left=16
overscan_right=8
overscan_top=-16
overscan_bottom=-16

```

Користувачам, які бажають використовувати аналогове відео, потрібно глянути на [цей](https://raw.github.com/Evilpaul/RPi-config/master/config.txt) файл конфігурації, який містить опції для не-NTSC виводів.

Потрібне перезавантаження для впровадження змін.

### Застереження щодо аналогового виводу TV-Out

Починаючи з Raspberry Pi 1 модель B+ і Raspberry Pi 2 модель B, сокет композитного відео був вилучений і замінений композитним сигналом через 3.5мм гніздо відео/аудіо. Деякі кабелі RCA не мають стандарту Raspberry Pi, в цьому випадку під'єднайте червоний або білий контакти для виводу відео.[[1]](http://www.raspberrypi-spy.co.uk/2014/07/raspberry-pi-model-b-3-5mm-audiovideo-jack/)

### Драйвер X.org

Драйвер X.org для Raspberry Pi може бути [встановлений](/index.php/Installed "Installed") за допомогою пакунку _xf86-video-fbdev_ або _xf86-video-fbturbo-git_.

## Сенсори на платі

### Температура

Знімати дані з сенсора температури можна за допомогою утиліти в пакунку _raspberrypi-firmware-tools_. RPi пропонує сенсор на BCM2835 SoC (CPU/GPU):

 `$ /opt/vc/bin/vcgencmd measure_temp`  `temp=49.8'C` 

Альтернативно, можна прочитати з файлової системи:

 `$ cat /sys/class/thermal/thermal_zone0/temp`  `49768` 

Для зрозумілого виводу:

 `$ awk '{printf "%3.1f°C\n", $1/1000}' /sys/class/thermal/thermal_zone0/temp`  `54.1°C` 

### Напруга

За чотирма різними напругами можна спостерігати за допомогою `/opt/vc/bin/vcgencmd`:

```
$ /opt/vc/bin/vcgencmd measure_volts _<id>_

```

Де `_<id>_` це:

*   core для напруги на ядрі
*   sdram_c для напруги на ядрі sdram
*   sdram_i для напруги I/O sdram
*   sdram_p для напруги PHY sdram

### Легкий пакет для моніторингу

[monitorix](https://aur.archlinux.org/packages/monitorix/)<sup><small>AUR</small></sup> має специфічну підтримку для RPi з версії 3.2.0\. Знімки екрану доступні [тут](http://www.monitorix.org/screenshots.html).

## Розгін процесора

RPi можна розігнати, редагуючи файл `/boot/config.txt`, наприклад:

```
arm_freq=800
arm_freq_min=100
core_freq=300
core_freq_min=75
sdram_freq=400
over_voltage=0

```

Стрічки з `*_min` визначають мінімальну частоту, що використовуватиметься даною компонентою. Коли система не завантажена, частоти знижуються до мінімального значення. Перегляньте статтю [Розгін](http://elinux.org/RPiconfig#Overclocking) на elinux щодо додаткових опцій та прикладів.

Потрібно перевантажити систему для впровадження нових налаштувань.

Налаштування розгону для годинника CPU застосовуються, коли регулятор підкручує CPU, тобто під навантаженням. Для отримання даних щодо поточної частоти CPU:

```
$ cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq

```

Прочитайте [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") для більшої інформації щодо регуляторів.

**Приклад:** Наступний скрипт покаже всі частоти, що встановлені на RPi:

```
#/bin/bash
for src in arm core h264 isp v3d uart pwm emmc pixel vec hdmi dpi ; do
    echo -e "$src:\t$(/opt/vc/bin/vcgencmd  measure_clock $src)"
done

```

## Серійна консоль

Відредагуйте файл `/boot/cmdline.txt`, змініть `loglevel` на `5` для перегляду повідомлень при завантаженні:

```
loglevel=5

```

Якщо типова швидкість 115200 не працює правильно, спробуйте змінити її на 38400:

```
console=ttyAMA0,38400 kgdboc=ttyAMA0,38400

```

Запустіть сервіс getty на Pi

```
# systemctl start getty@ttyAMA0

```

Ввімкніть під час завантаження

```
# systemctl enable getty@ttyAMA0.service

```

Створення властивого сервісного посилання:

```
# ln -s /usr/lib/systemd/system/serial-getty@.service /etc/systemd/system/getty.target.wants/serial-getty@ttyAMA0.service

```

З'єднайтесь з комп'ютера:

```
# screen /dev/ttyUSB0 38400

```

## Модуль камери для Raspberry Pi

Команди для модуля камери включені як частина пакунку _raspberrypi-firmware-tools_, який встановлено з основною системою.

```
$ /opt/vc/bin/raspistill
$ /opt/vc/bin/raspivid

```

Додайте до файлу `/boot/config.txt`:

```
gpu_mem=128
start_file=start_x.elf
fixup_file=fixup_x.dat

```

Можна теж додати

```
disable_camera_led=1

```

Наступні стрічки є типовою помилкою:

```
mmal: mmal_vc_component_enable: failed to enable component: ENOSPC
mmal: camera component couldn't be enabled
mmal: main: Failed to create camera component
mmal: Failed to run camera app. Please check for firmware updates

```

яку можна виправити, налаштовуючи ці значення у файлі `/boot/config.txt`:

```
cma_lwm=
cma_hwm=
cma_offline_start=

```

Іншу типову помилку:

```
mmal: mmal_vc_component_create: failed to create component 'vc.ril.camera' (1:ENOMEM)
mmal: mmal_component_create_core: could not create component 'vc.ril.camera' (1)
mmal: Failed to create camera component
mmal: main: Failed to create camera component
mmal: Only 64M of gpu_mem is configured. Try running "sudo raspi-config" and ensure that "memory_split" has a value of 128 or greater

```

можна виправити, додаючи наступну стрічку до файлу `/etc/modprobe.d/blacklist.conf`:

```
blacklist i2c_bcm2708

```

Щоб використовувати стандартні програми (такі, що використовують `/dev/video0`), потрібно завантажити драйвер V4L2\. Це можна зробити автоматично під час завантаження, створивши файл автозавантаження:

 `/etc/modules-load.d/rpi-camera.conf`  `bcm2835-v4l2` 

## Апаратний генератор випадкових чисел

Хоч Arch Linux ARM для Raspberry Pi має налаштований модуль `bcm2708-rng` для завантаження (дивіться [це](http://archlinuxarm.org/forum/viewtopic.php?f=31&t=4993#p27708)), однак потрібно встановити _rng-tools_ і повідомити Апаратний Демон Ентропії RNG (_rngd_), в якому місці знаходиться апаратний генератор випадкових чисел.

Це можна зробити редагуванням файлу `/etc/conf.d/rngd`:

```
RNGD_OPTS="-o /dev/random -r /dev/hwrng"

```

і вмикаючи і [запускаючи](/index.php/Start "Start") сервіс _rngd_.

Якщо в системі запущено [haveged](/index.php/Haveged "Haveged"), то його потрібно зупинити і вимкнути, оскільки він може гризтися з _rngd_.

Ці зміни забезпечують передачу даних з апаратного генератора випадкових чисел до пула ентропії ядра в `/dev/random`. Для перевірки доступної ентропії запустіть:

```
# cat /proc/sys/kernel/random/entropy_avail

```

Число повинно бути біля 3000, тоді як перед налаштуванням _rngd_ воно повинно бути близьке до 1000.

## GPIO

### SPI

Для ввімкнення пристроїв `/dev/spidev*` закоментуйте наступну стрічку:

 `/boot/config.txt`  `device_tree_param=spi=on` 

### Python

Для використання пінів GPIO з Python, використайте бібліотеку [RPi.GPIO](https://pypi.python.org/pypi/RPi.GPIO). Встановіть або [python-raspberry-gpio](https://aur.archlinux.org/packages/python-raspberry-gpio/)<sup><small>AUR</small></sup> або [python2-raspberry-gpio](https://aur.archlinux.org/packages/python2-raspberry-gpio/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/python2-raspberry-gpio)]</sup> з [AUR](/index.php/AUR "AUR").

## I2C

Встановіть пакунки _i2c-tools_ та _lm_sensors_.

Ввімкніть підтримку i2c, додаючи стрічку до `/boot/config.txt`:

```
 dtparam=i2c_arm=on

```

Налаштуйте модулі `i2c-dev` і `i2c-bcm2708` (якщо вони не є в чорному списку для камери), щоб завантажувалися на старті:

 `/etc/modules-load.d/raspberrypi.conf` 

```
i2c-dev
i2c-bcm2708
```

Перевантажте Raspberry Pi і запустіть наступну команду для отримання адреси пристрою:

```
 i2cdetect -y 0

```

Тепер потрібно повідомити Linux про можливість використання пристрою. Замініть адрес пристрою адресою, знайденою в попередньому кроці, додаючи префікс '0x' (наприклад 0x48) і виберіть назву пристрою:

```
 echo <назва пристрою> <адреса пристрою> >/sys/class/i2c-adapter/i2c-0/new_device

```

Перевірте командою dmesg, чи появився новий пристрій:

```
 i2c-0: new_device: Instantiated device ds1621 at 0x48

```

І, остаточно, отримайте вивід з сенсора:

```
 sensors

```

## Дивіться також

*   [RPi Config](http://elinux.org/RPiconfig) - Excellent source of info relating to under-the-hood tweaks.
*   [RPi vcgencmd usage](http://elinux.org/RPI_vcgencmd_usage) - Overview of firmware command vcgencmd.
*   [Arch Linux ARM on Raspberry PI](http://archpi.dabase.com/) - A FAQ style site with hints and tips for running Arch Linux on the RPi
*   [[2]](https://github.com/phortx/Raspberry-Pi-Setup-Guide) - A really opionionated guide how to setup a RPi with Arch Linux

Retrieved from "[https://wiki.archlinux.org/index.php?title=Raspberry_Pi_(Українська)&oldid=415974](https://wiki.archlinux.org/index.php?title=Raspberry_Pi_(Українська)&oldid=415974)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ARM architecture (Українська)](/index.php/Category:ARM_architecture_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0) "Category:ARM architecture (Українська)")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")