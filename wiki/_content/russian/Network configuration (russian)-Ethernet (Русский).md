**Состояние перевода:** На этой странице представлен перевод статьи [Network configuration/Ethernet](/index.php/Network_configuration/Ethernet "Network configuration/Ethernet"). Дата последней синхронизации: 16 января 2020\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Network_configuration/Ethernet&diff=0&oldid=594422).

В данной статье описывается настройка [Ethernet](https://en.wikipedia.org/wiki/ru:Ethernet "wikipedia:ru:Ethernet"), общие вопросы о настройке сети описываются в статье [Настройка сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8 "Настройка сети").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Драйвер устройства](#Драйвер_устройства)
    *   [1.1 Проверка состояния](#Проверка_состояния)
    *   [1.2 Загрузка модуля](#Загрузка_модуля)
*   [2 Советы и рекомендации](#Советы_и_рекомендации)
    *   [2.1 ifplugd для ноутбуков](#ifplugd_для_ноутбуков)
*   [3 Решение проблем](#Решение_проблем)
    *   [3.1 Смена компьютера при использовании кабельного модема](#Смена_компьютера_при_использовании_кабельного_модема)
    *   [3.2 Явное уведомление о перегруженности](#Явное_уведомление_о_перегруженности)
    *   [3.3 Realtek: нет соединения / проблема WOL](#Realtek:_нет_соединения_/_проблема_WOL)
        *   [3.3.1 Включение сетевого интерфейса в Linux](#Включение_сетевого_интерфейса_в_Linux)
        *   [3.3.2 Откат/замена драйвера для Windows](#Откат/замена_драйвера_для_Windows)
        *   [3.3.3 Включение WOL в драйвере для Windows](#Включение_WOL_в_драйвере_для_Windows)
        *   [3.3.4 Обновление драйвера Realtek для Linux](#Обновление_драйвера_Realtek_для_Linux)
        *   [3.3.5 Включение LAN Boot ROM в BIOS/CMOS](#Включение_LAN_Boot_ROM_в_BIOS/CMOS)
    *   [3.4 Для чипсетов Atheros отсутствует интерфейс](#Для_чипсетов_Atheros_отсутствует_интерфейс)
    *   [3.5 Broadcom BCM57780](#Broadcom_BCM57780)
    *   [3.6 Realtek RTL8111/8168B](#Realtek_RTL8111/8168B)
    *   [3.7 Материнская плата Gigabyte с интерфейсом Realtek 8111/8168/8411](#Материнская_плата_Gigabyte_с_интерфейсом_Realtek_8111/8168/8411)

## Драйвер устройства

### Проверка состояния

Диспетчер устройств [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") должен определить вашу [сетевую плату](https://en.wikipedia.org/wiki/ru:%D0%A1%D0%B5%D1%82%D0%B5%D0%B2%D0%B0%D1%8F_%D0%BF%D0%BB%D0%B0%D1%82%D0%B0 "wikipedia:ru:Сетевая плата") и автоматически загрузить необходимый [модуль ядра](/index.php/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D0%B8_%D1%8F%D0%B4%D1%80%D0%B0 "Модули ядра") при старте системы. Найдите пункт "Ethernet controller" (или похожий) в выводе команды `lspci -v`. Там должна быть информация о том, какой модуль ядра содержит драйвер для вашей сетевой платы. Например:

 `$ lspci -v` 
```
02:00.0 Ethernet controller: Attansic Technology Corp. L1 Gigabit Ethernet Adapter (rev b0)
 	...
 	Kernel driver in use: atl1
 	Kernel modules: atl1

```

Затем проверьте, был ли загружен драйвер, при помощи команды `dmesg | grep *имя-модуля*`. Например:

```
$ dmesg | grep atl1
    ...
    atl1 0000:02:00.0: eth0 link is up 100 Mbps full duplex

```

Пропустите следующий раздел, если драйвер был успешно загружен. В противном случае необходимо узнать, какой модуль требуется для вашей конкретной модели.

### Загрузка модуля

Найдите в интернете необходимый для вашего чипсета модуль/драйвер. Когда вы узнаете, какой модуль необходимо использовать, попробуйте [загрузить его вручную](/index.php/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D0%B8_%D1%8F%D0%B4%D1%80%D0%B0#Управление_модулями_вручную "Модули ядра"). Если вы увидите сообщение об ошибке, говорящее, что модуль не найден, возможно, драйвер не включён в состав ядра Arch. Вы можете осуществить поиск имени модуля в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

Если *udev* не определяет и не загружает нужный модуль автоматически во время старта системы, обратитесь к разделу [Модули ядра#Автоматическое управление модулями](/index.php/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D0%B8_%D1%8F%D0%B4%D1%80%D0%B0#Автоматическое_управление_модулями "Модули ядра").

## Советы и рекомендации

### ifplugd для ноутбуков

**Совет:** [dhcpcd](/index.php/Dhcpcd "Dhcpcd") предоставляет ту же возможность "из коробки"

[ifplugd](https://www.archlinux.org/packages/?name=ifplugd) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") - это демон, который автоматически настроит ваше устройство Ethernet при подключении кабеля и удалит конфигурацию при его отключении. Это полезно для ноутбуков со встроенными сетевыми адаптерами, поскольку интерфейс будет настроен лишь при реальном подключении кабеля. Другой вариант использования - когда вам необходимо лишь перезапустить сеть, но не компьютер, без необходимости делать это в оболочке.

По умолчанию ifplugd настроен на работу с устройством `eth0`. Эта и другие настройки, такие как время задержки, можно изменить в файле `/etc/ifplugd/ifplugd.conf`.

**Примечание:** Пакет [netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)") содержит службу `netctl-ifplugd@.service`, в ином случае можно воспользоваться `ifplugd@.service` из пакета [ifplugd](https://www.archlinux.org/packages/?name=ifplugd). К примеру, [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") `ifplugd@eth0.service`.

## Решение проблем

### Смена компьютера при использовании кабельного модема

Некоторые провайдеры кабельных интернет-услуг (например, videotron) настраивают кабельный модем на работу только с одним клиентом-компьютером по MAC-адресу его сетевого интерфейса. Как только модем запомнит MAC-адрес первого подключенного компьютера или оборудования, он ни при каких обстоятельствах не будет отвечать на запросы, идущие с других MAC-адресов. Таким образом, если вы поменяете один компьютер на другой (или поставите маршрутизатор), новый компьютер (или маршрутизатор) не будет работать с кабельным модемом, поскольку он имеет MAC-адрес, отличный от предыдущего. Для сброса кабельного модема с тем, чтобы он стал работать с новым компьютером, необходимо выключить питание кабельного модема и включить его опять. Как только он перезагрузится и подключится к сети (загорятся соответствующие индикаторы), перезагрузите вновь подключенный компьютер, чтобы он выполнил запрос DHCP, или вручную заставьте его запросить новый адрес DHCP.

Если это не поможет, необходимо скопировать MAC-адрес изначальной машины. См. также [Подмена MAC-адреса](/index.php/%D0%9F%D0%BE%D0%B4%D0%BC%D0%B5%D0%BD%D0%B0_MAC-%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0 "Подмена MAC-адреса").

### Явное уведомление о перегруженности

Явное уведомление о перегруженности ([Explicit Congestion Notification](https://en.wikipedia.org/wiki/ru:Explicit_Congestion_Notification "wikipedia:ru:Explicit Congestion Notification"), ECN) может стать причиной проблем с передачей информации на старых/плохих маршрутизаторах. Для [systemd 239](https://github.com/systemd/systemd/issues/9748) это касается как входящего, так и исходящего трафика.

Чтобы включать ECN только по требованию входящих соединений (безопасно, настройка ядра по-умолчанию), выполните:

```
# sysctl net.ipv4.tcp_ecn=2

```

Для полного отключения ECN (например, чтобы проверить, действительно ли причина возникших проблем в ECN):

```
# sysctl net.ipv4.tcp_ecn=0

```

Подробную информацию можно получить в [документации ядра](https://www.kernel.org/doc/Documentation/networking/ip-sysctl.txt).

### Realtek: нет соединения / проблема WOL

Пользователи с сетевыми платами, основанными на Realtek 8168 8169 8101 8111(C) (отдельными/встроенными) могут заметить проблему, что карта, кажется, отключена во время загрузки системы, и лампочка-индикатор не горит. Такое часто встречается на машинах с двумя операционными системами, на которых также установлена Windows. Похоже, что причиной являются обычные официальные драйверы Realtek (датирующие все после мая 2007 г.) под Windows. Эти новые драйверы отключают функцию Wake-On-LAN, отключая сетевую плату при завершении работы Windows, и она остается выключенной до следующей загрузки Windows. Вы сможете заметить это, если индикатор подключения не горит, пока не будет загружена Windows; во время ее завершения работы индикатор выключается. В нормальном состоянии лампочка всегда должна гореть, пока система работает, даже во время POST. Эта проблема также затрагивает другие операционные системы, не имеющие новейших драйверов (например, Live CD). Есть несколько способов решения этой проблемы.

#### Включение сетевого интерфейса в Linux

Включите сетевой интерфейс, следуя инструкциям в статье [Network configuration#Включение и отключение сетевых интерфейсов](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Включение_и_отключение_сетевых_интерфейсов "Network configuration (Русский)").

#### Откат/замена драйвера для Windows

Вы можете откатить ваш драйвер сетевой платы в Windows на тот, который предоставляет Microsoft (если это возможно), или откатить/установить официальный драйвер Realtek, имеющий дату выпуска ранее мая 2007 г. (может найтись на компакт-диске, идущем в комплекте с вашим аппаратным обеспечением).

#### Включение WOL в драйвере для Windows

Наверное, самое лучшее и быстрое решение - изменить эту настройку в драйвере Windows. Тогда это затронет всю систему, в том числе Arch (а также live CD и другие операционные системы). В менеджере устройств Windows найдите ваш сетевой адаптер Realtek и сделайте на нем двойной щелчок мыши. Во вкладке "Дополнительно" измените значение "Wake-on-LAN после завершения работы" (Wake-on-LAN after shutdown) на "Включено".

В Windows XP (пример):

```
Кликните правой кнопкой мыши на "Мой компьютер" и зайдите в "Свойства"
--> Вкладка "Аппаратное обеспечение" (Hardware)
  --> Менеджер устройств
    --> Сетевые адаптеры
      --> "двойной клик" на Realtek ...
        --> Вкладка "Дополнительно"
          --> Wake-On-Lan после завершения работы
            --> Включено

```

**Примечание:** В новых драйверах Realtek для Windows (протестировано на *Realtek 8111/8169 LAN Driver v5.708.1030.2008*, датированном 2009/01/22, от GIGABYTE) доступ к этой опции может быть немного иным, например, *Shutdown Wake-On-LAN --> Включено*. Похоже, что ее переключение в значение `Отключено` не дает эффекта (вы увидите, что индикатор соединения по-прежнему выключается при завершении работы Windows). Довольно грязный обходной путь - загрузиться в Windows и просто перезагрузить (reset) систему (плохой restart/shutdown), что не даст драйверу Windows никаких шансов отключить LAN. Лампочка будет по-прежнему гореть, а адаптер LAN останется доступен после POST до тех пор, пока вы опять не запустите Windows и правильно завершите его работу

#### Обновление драйвера Realtek для Linux

Новые драйвера для интерфейсов Realtek можно найти на их сайте (не протестировано, но также должно решать проблему).

#### Включение LAN Boot ROM в BIOS/CMOS

Похоже, что установка *Интегрированная периферия (Integrated Peripherals) --> Встроенный (Onboard) LAN Boot ROM --> Включено* в BIOS/CMOS возобновляет работу чипа Realtek LAN при загрузке системы, несмотря на то, что драйвер Windows делает обратное при завершении работы ОС.

**Примечание:** Этот способ был несколько раз протестирован на материнской плате GIGABYTE GA-G31M-ES2L с BIOS версии F8, выпущенным 2009/02/05

### Для чипсетов Atheros отсутствует интерфейс

Пользователи некоторых чипов Atheros ethernet сообщают, что они не работают "из коробки" (с установочного носителя февраля 2014 г.). Помогает установка пакета [backports-patched](https://aur.archlinux.org/packages/backports-patched/) из AUR.

### Broadcom BCM57780

Этот чипсет Broadcom иногда работает плохо, если не указать порядок загрузки модулей. Необходимые модули — `broadcom` и `tg3`, и загружаться они должны именно в таком порядке.

Если в вашем компьютере используется этот чипсет, сделайте следующее:

*   Найдите вашу сетевую плату в выводе *lspci*:

 `$ lspci | grep Ethernet` 
```
02:00.0 Ethernet controller: Broadcom Corporation NetLink BCM57780 Gigabit Ethernet PCIe (rev 01)

```

*   Если Ethernet-соединение не функционирует, отключите кабель и выполните команды:

```
# modprobe -r tg3
# modprobe broadcom
# modprobe tg3

```

*   Подключите обратно сетевой кабель и проверьте работу модуля:

```
$ dmesg | grep tg3

```

*   Если это решило проблему, сделайте изменения постоянными, добавив модули `broadcom` и `tg3` (в этом порядке) в массив `MODULES`:

 `/etc/mkinitcpio.conf` 
```
MODULES=(.. broadcom tg3 ..)

```

*   Пересоберите initramfs:

```
# mkinitcpio -p linux

```

*   В качестве альтернативы можно создать файл `/etc/modprobe.d/broadcom.conf` со следующим содержимым:

```
softdep tg3 pre: broadcom

```

**Примечание:** Этот способ может помочь и для других чипсетов, например, BCM57760

### Realtek RTL8111/8168B

 `# lspci | grep Ethernet` 
```
03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 02)

```

За распознавание и работу этого сетевого интерфейса отвечает модуль `r8169`, однако некоторые ревизии данного драйвера работают с ошибками — происходит постоянное включение/выключение устройства. Для решения проблемы можно установить модуль [r8168](https://www.archlinux.org/packages/?name=r8168). Если [r8168](https://www.archlinux.org/packages/?name=r8168) не загружается автоматически менеджером [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)"), то нужно [запретить загрузку](/index.php/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D0%B8_%D1%8F%D0%B4%D1%80%D0%B0#Запрет_загрузки "Модули ядра") модуля `r8169`. Подробнее загрузка модулей описана в статье [Модули ядра#Автоматическое управление модулями](/index.php/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D0%B8_%D1%8F%D0%B4%D1%80%D0%B0#Автоматическое_управление_модулями "Модули ядра").

Ещё одной проблемой некоторых ревизий драйвера этого адаптера является плохая поддержка IPv6\. В случае зависания страниц и низкой скорости подключения может помочь [отключение функциональности IPv6](/index.php/IPv6_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Отключение_функциональности "IPv6 (Русский)").

### Материнская плата Gigabyte с интерфейсом Realtek 8111/8168/8411

При загрузке с выключенным (настройка по умолчанию) [IOMMU](https://en.wikipedia.org/wiki/ru:IOMMU "wikipedia:ru:IOMMU") могут возникнуть проблемы с сетевым интерфейсом на материнских платах Gigabyte (например, *Gigabyte GA-990FXA-UD3*). Сетевое подключение будет неустойчивым, с малой пропускной способностью или отсутствовать вовсе. Сказанное в равной мере касается как встроенных интерфейсов, так и внешних сетевых плат на шине PCI, поскольку настройки IOMMU влияют на все сетевые интерфейсы материнской платы. Если [включить](/index.php/PCI_passthrough_via_OVMF#Setting_up_IOMMU "PCI passthrough via OVMF") IOMMU и загрузиться с установочного устройства, то на секунду появится сообщение об ошибке AMD I-10/xhci, после чего загрузка продолжится обычным образом. В результате сетевой интерфейс будет функционировать нормально (даже с модулем `r8169`).

Если добавить [параметр ядра](/index.php/Kernel_parameters_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel parameters (Русский)") `iommu=soft`, то при загрузке сообщение об ошибке будет подавляться.