**Состояние перевода:** На этой странице представлен перевод статьи [Wireshark](/index.php/Wireshark "Wireshark"). Дата последней синхронизации: 19 января 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Wireshark&diff=0&oldid=408501).

Wireshark (ранее Ethereal) - бесплатная программа-анализатор с открытым исходным кодом. Программа используется для анализа, перехвата (сниффинга) интернет пакетов.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Захват пакетов от обычного пользователя](#Захват_пакетов_от_обычного_пользователя)
    *   [2.1 Добавить пользователя в группу wireshark](#Добавить_пользователя_в_группу_wireshark)
    *   [2.2 Использование sudo](#Использование_sudo)
*   [3 Методы анализа захваченных пакетов](#Методы_анализа_захваченных_пакетов)
    *   [3.1 Фильтрация TCP пакетов](#Фильтрация_TCP_пакетов)
    *   [3.2 Фильтрация UDP пакетов](#Фильтрация_UDP_пакетов)
    *   [3.3 Фильтрование пакетов из специфичного IP-адреса](#Фильтрование_пакетов_из_специфичного_IP-адреса)

## Установка

Wireshark имеет несколько реализаций: GTK, CLI, Qt:

*   [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk)
*   [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli)
*   [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt)

## Захват пакетов от обычного пользователя

ArchLinux использует [метод из вики Wireshark](https://wiki.wireshark.org/CaptureSetup/CapturePrivileges#Other_Linux_based_systems_or_other_installation_methods) для разделения привилегий. Если установлен [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli), используйте скрипт для совместимости `/usr/bin/dumpcap`.

 `$ getcap /usr/bin/dumpcap`  `/usr/bin/dumpcap = cap_net_admin,cap_net_raw+eip` 

`/usr/bin/dumpcap` единственный процесс имеющий привилегии для перехвата пакетов.

**Важно:** `/usr/bin/dumpcap` должен быть запущен либо от суперпользователя, либо от группы wireshark.

Существуют несколько способов перехвата пакетов от обычного пользователя:

### Добавить пользователя в группу wireshark

Для использования wireshark без прав суперпользователя можно добавить пользователя в группу `wireshark`:

```
# gpasswd -a *username* wireshark

```

Если вы не хотите перезапускать текущую сессию, то используйте эту команду:

```
# newgrp wireshark

```

### Использование sudo

Также возможно использование [sudo](https://www.archlinux.org/packages/?name=sudo), чтобы временно использовать группу `wireshark`. Следующие строки позволят всем пользователям группы `wheel` запускать программы, используя GID wireshark:

 `%wheel ALL=(:wireshark) /usr/bin/wireshark, /usr/bin/tshark` 

Для запуска wireshark:

 `$ sudo -g wireshark wireshark` 

## Методы анализа захваченных пакетов

Wireshark поддерживает огромное количество методов анализа пакетов с помощью фильтров.

**Примечание:** Для более детального изучения синтаксиса, смотрите `man pcap-filter(7)`

### Фильтрация TCP пакетов

Если вы желаете просмотреть все текущие TCP пакеты, то введите `tcp` в строку "Filter".

### Фильтрация UDP пакетов

Если вы желаете просмотреть все текущие UDP пакеты, то введите `udp` в строку "Filter".

### Фильтрование пакетов из специфичного IP-адреса

*   Если вы желаете просмотреть весь текущий трафик исходящие из специфичного адреса, то используйте следующий фильтр: `ip.dst == *1.2.3.4*`.
*   Для просмотра входящего трафика, используя специфичный адрес: `ip.src == *1.2.3.4*`.
*   Для просмотра исходящего трафика: `ip.addr == *1.2.3.4*`.

Вместо `*1.2.3.4*` подставьте нужный вам ip-адрес.