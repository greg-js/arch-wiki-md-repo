Ссылки по теме

*   [iptables (Русский)](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [nftables](/index.php/Nftables "Nftables"). Дата последней синхронизации: 13 декабря 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Nftables&diff=0&oldid=591624).

[nftables](https://netfilter.org/projects/nftables/) — проект netfilter, целью которого ставится замена существующего набора межсетевых экранов {ip,ip6,arp,eb}tables. Была разработана новая система фильтрации пакетов, добавлена пользовательская утилита ntf, а также создан слой совместимости с {ip,ip6}tables. nftables использует набор хуков, систему отслеживания соединений, систему очередей и подсистему логирования netfilter.

nftables состоит из трёх основных частей: низкоуровневая реализация в составе ядра, библиотека libnl и пользовательский интерфейс nftables. Ядро занимается выполнением правил во время работы межсетевого экрана; для настройки правил в ядро добавлен интерфейс [netlink](https://en.wikipedia.org/wiki/Netlink "wikipedia:Netlink"). Библиотека libnl содержит низкоуровневые функции для взаимодействия с ядром, а в качестве пользовательского интерфейса nftables используется утилита nft.

Подробную информацию о nftables можно найти на [вики-странице](https://wiki.nftables.org/wiki-nftables/index.php/Main_Page) проекта.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Использование](#Использование)
*   [3 Настройка](#Настройка)
    *   [3.1 Таблицы](#Таблицы)
        *   [3.1.1 Создание таблицы](#Создание_таблицы)
        *   [3.1.2 Просмотр таблиц](#Просмотр_таблиц)
        *   [3.1.3 Просмотр цепочек и правил](#Просмотр_цепочек_и_правил)
        *   [3.1.4 Удаление таблицы](#Удаление_таблицы)
        *   [3.1.5 Стирание таблицы](#Стирание_таблицы)
    *   [3.2 Цепочки](#Цепочки)
        *   [3.2.1 Создание цепочки](#Создание_цепочки)
            *   [3.2.1.1 Обычная цепочка](#Обычная_цепочка)
            *   [3.2.1.2 Базовая цепочка](#Базовая_цепочка)
        *   [3.2.2 Просмотр правил](#Просмотр_правил)
        *   [3.2.3 Изменение цепочки](#Изменение_цепочки)
        *   [3.2.4 Удаление цепочки](#Удаление_цепочки)
        *   [3.2.5 Стереть правила из цепочки](#Стереть_правила_из_цепочки)
    *   [3.3 Правила](#Правила)
        *   [3.3.1 Добавление правила](#Добавление_правила)
            *   [3.3.1.1 Выражения](#Выражения)
        *   [3.3.2 Удаление](#Удаление)
    *   [3.4 Полная перезагрузка правил](#Полная_перезагрузка_правил)
*   [4 Примеры](#Примеры)
    *   [4.1 Рабочая станция](#Рабочая_станция)
    *   [4.2 Сервер](#Сервер)
    *   [4.3 Ограничение скорости передачи](#Ограничение_скорости_передачи)
    *   [4.4 Переход](#Переход)
    *   [4.5 Несколько сетевых интерфейсов с разными правилами](#Несколько_сетевых_интерфейсов_с_разными_правилами)
    *   [4.6 Маскарадинг](#Маскарадинг)
    *   [4.7 NAT с пробросом портов](#NAT_с_пробросом_портов)
*   [5 Советы и рекомендации](#Советы_и_рекомендации)
    *   [5.1 Настройка простого сетевого экрана](#Настройка_простого_сетевого_экрана)
        *   [5.1.1 Одиночная машина](#Одиночная_машина)
    *   [5.2 Предотвращение атак перебором](#Предотвращение_атак_перебором)
*   [6 Решение проблем](#Решение_проблем)
    *   [6.1 Работа с Docker](#Работа_с_Docker)
*   [7 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [nftables](https://www.archlinux.org/packages/?name=nftables) из официальных репозиториев или git-версию [nftables-git](https://aur.archlinux.org/packages/nftables-git/) из AUR.

**Совет:** Большинство [интерфейсов](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Интерфейс "Iptables (Русский)") iptables не имеет прямой или косвенной поддержки nftables, хотя возможность для этого существует [[2]](https://www.spinics.net/lists/netfilter/msg58215.html). [firewalld](/index.php/Firewalld "Firewalld") — единственный графический интерфейс со встроенной поддержкой обеих версий утилит межсетевого экрана, как iptables, так и nftables [[3]](https://firewalld.org/2018/07/nftables-backend).

## Использование

В *nftables* есть определённые различия между временными правилами, созданными в командной строке, и постоянными, загруженными из файла или сохранёнными в файл. Файл настроек по умолчанию — `/etc/nftables.conf`. Он уже содержит простую IPv4/IPv6 таблицу правил "inet filter".

Чтобы его использовать, [запустите/включите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5/%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Запустите/включите") службу `nftables.service`.

Узнать набор действующих правил можно командой

```
# nft list ruleset

```

**Примечание:** Возможно, придётся создать файл `/etc/modules-load.d/nftables.conf` со списком всех относящихся к nftables модулей. Это необходимо для корректной работы службы systemd. Список модулей можно узнать командой
```
$ grep -Eo '^nf\w+' /proc/modules

```

Если этого не сделать, то скорее всего вы столкнётесь с ошибкой `Error: Could not process rule: No such file or directory`.

## Настройка

Утилита *nft* выполняет обработку правил перед передачей их ядру. Правила объединяются в цепочки, которые, в свою очередь, входят в состав таблиц. В следующих разделах описано создание и модифицирование этих структур.

Все выполняемые ниже изменения — временные. Чтобы их зафиксировать, сохраните созданный набор правил в файл `/etc/nftables.conf`, который будет загружаться службой `nftables.service`:

```
# nft -s list ruleset > /etc/nftables.conf

```

**Примечание:** Команда `nft list` не выводит определения переменных. Если в файле `/etc/nftables.conf` есть какие-либо переменные, то в выводе команды вы их не увидите — все переменные будут заменены на значения.

Прочитать правила из файла можно с помощью флага `-f`/`--file`

```
# nft -f *имя-файла*

```

Обратите внимание, что уже загруженные правила не будут при этом автоматически стёрты.

В руководстве [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8) можно найти полный список команд.

### Таблицы

Таблицы содержат [#Цепочки](#Цепочки). В отличие от iptables, в nftables отсутствуют встроенные таблицы. Количество и название таблиц определяется пользователем. Однако каждая таблица имеет только одно семейство адресов и применяется к пакетам только этой семьи. Таблицы могут относиться к одному из пяти семейств.

| семейство nftables | утилита iptables |
| ip | iptables |
| ip6 | ip6tables |
| inet | iptables and ip6tables |
| arp | arptables |
| bridge | ebtables |

`ip` - семейство по умолчанию; используется, если параметр семейства не был указан.

Семейство `inet` используется для создания общих для протоколов IPv4 и IPv6 правил, что позволяет унифицировать семейства `ip` и `ip6` и упростить создание правил.

Описание остальных семейств адресов вы найдёте в руководстве [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8#ADDRESS_FAMILIES).

В командах ниже параметр `*семейство*` будет указываться не всегда; если его нет, то подразумевается семейство `ip`.

#### Создание таблицы

Добавить новую таблицу:

```
# nft add table *семейство* *таблица*

```

#### Просмотр таблиц

Вывести список таблиц:

```
# nft list tables

```

#### Просмотр цепочек и правил

Вывести цепочки и правила выбранной таблицы:

```
# nft list table *семейство* *таблица*

```

Например, чтобы вывести на экран правила таблицы `filter` семейства `inet`, выполните команду:

```
# nft list table inet filter

```

#### Удаление таблицы

Чтобы удалить таблицу, выполните:

```
# nft delete table *семейство* *таблица*

```

Удалить можно только пустую таблицу без цепочек.

#### Стирание таблицы

Стереть все правила таблицы:

```
# nft flush table *семейство* *таблица*

```

### Цепочки

Цепочка содержит [#Правила](#Правила). В отличие от iptables, в nftables отсутствуют встроенные цепочки. Соответственно, если опрелённые типы или хуки фреймворка netfilter не задействованы ни в одном правиле nftables, то проходящие через эти цепочки пакеты обрабатываться не будут.

Есть два типа цепочек. *Базовая* цепочка является точкой входа для пакетов из сетевого стека, если указан хук. *Обычная* цепочка может использоваться в качестве цели перехода (jump).

В командах ниже параметр `*семейство*` будет указываться не всегда; если его нет, то подразумевается семейство `ip`.

#### Создание цепочки

##### Обычная цепочка

Добавить обычную цепочку `*цепочка*` в таблицу `*таблица*`:

```
# nft add chain *семейство* *таблица* *цепочка*

```

Например, чтобы добавить обычную цепочку `tcpchain` к таблице `filter` семейства адресов `inet`, выполните:

```
# nft add chain inet filter tcpchain

```

##### Базовая цепочка

Чтобы добавить базовую цепочку, укажите хук и значение приоритета:

```
# nft add chain *семейство* *таблица* *цепочка* '{ type *тип* hook *хук* priority *приоритет* ; }'

```

`*тип*` может принимать значения `filter`, `route` или `nat`.

Для семейств адресов IPv4/IPv6/Inet `*хук*` может принимать значения `prerouting`, `input`, `forward`, `output` или `postrouting`. Описание других возможных хуков вы найдёте в руководстве [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8#ADDRESS_FAMILIES).

Параметр `*приоритет*` задаётся названием приоритета или его значением (подробнее см. [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8#CHAINS)). Цепочки с более низкими значениями обрабатываются раньше. Значение приоритета может быть отрицательным [[4]](https://wiki.nftables.org/wiki-nftables/index.php/Configuring_chains#Base_chain_types).

Например, добавим базовую цепочку для фильтрации входящих пакетов:

```
# nft add chain inet filter input '{ type filter hook input priority 0; }'

```

Если заменить команду `add` на `create` в любом из правил выше, то цепочка тоже будет создана, но при этом вы получите сообщение об ошибке, если цепочка с таким названием уже существует.

#### Просмотр правил

Следующая команда выводит на экран все правила в цепочке:

```
# nft list chain *семейство* *таблица* *цепочка*

```

Например, следующая команда выведет правила цепочки `output` таблицы `filter` семейства `inet`:

```
# nft list chain inet filter output

```

#### Изменение цепочки

Для редактирования цепочки укажите её название и правила, которые нужно изменить:

```
# nft chain *семейство таблица цепочка* '{ [ type *тип* hook *хук* device *устройство* priority *приоритет* ; policy *политика* ; ] }'

```

Например, для изменения политики обработки входящих пакетов цепочки исходной таблицы с `accept` на `drop` выполните команду:

```
# nft chain inet filter input '{ policy drop ; }'

```

#### Удаление цепочки

Удалить цепочку:

```
# nft delete chain *семейство* *таблица* *цепочка*

```

Цепочка должна быть пустой (не содержать правил) и не должна быть целью перехода из другой цепочки.

#### Стереть правила из цепочки

Чтобы стереть все правила цепочки, выполните:

```
# nft flush chain *семейство* *таблица* *цепочка*

```

### Правила

Правила конструируются из выражений (expressions) и операторов (statements) и содержатся внутри цепочек.

#### Добавление правила

**Совет:** Утилита *iptables-translate* поможет преобразовать правила [iptables](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)") в формат nftables.

Чтобы добавить правило в цепочку, выполните:

```
# nft add rule *семейство* *таблица* *цепочка* handle *маркер* *оператор*

```

Правило будет прикреплено после `*маркер*`, который можно не указывать. Если маркер (handle) не задать, то правило добавится в конец цепочки.

Чтобы добавить правило перед определённой позицией, выполните

```
# nft insert rule *семейство* *таблица* *цепочка* handle *маркер* *оператор*

```

Если `*маркер*` не указан, то правило добавится в начало цепочки.

##### Выражения

Обычно `*оператор*` включает несколько выражений для сравнений и вынесения решения. Решениями могут быть `accept`, `drop`, `queue`, `continue`, `return`, `jump *цепочка*` и `goto *цепочка*`. Возможны и другие операторы помимо решений, подробнее смотрите [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8).

В nftables доступен ряд выражений, по большей части совпадающий с аналогичными в iptables. Наиболее важное отличие заключается в том, что здесь нет обобщённых или неявных параметров. Обобщённый параметр (generic match) обычно доступен для всех правил, например, параметры `--protocol` или `--source`. Неявные правила (implicit matches) относятся к конкретному протоколу, как параметр `--sport` для пакетов TCP.

Ниже представлен неполный список возможных параметров:

*   meta (метасущности, напр. интерфейсы)
*   icmp (протокол ICMP)
*   icmpv6 (протокол ICMPv6)
*   ip (протокол IP)
*   ip6 (протокол IPv6)
*   tcp (протокол TCP)
*   udp (протокол UDP)
*   sctp (протокол SCTP)
*   ct (отслеживание соединений)

Ниже приведён неполный список аргументов для параметров (подробнее см. [nft(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nft.8)):

```
meta:
  oif <интерфейс-отправитель НОМЕР>
  iif <интерфейс-получатель НОМЕР>
  oifname <интерфейс-отправитель ИМЯ>
  iifname <интерфейс-получатель ИМЯ>

  (параметры oif и iif принимаю строковые значения, которые конвертируются в номер)
  (параметры oifname и iifname более гибкие, но они медленнее из-за необходимости работать со строками-именами)

icmp:
  type <тип icmp>

icmpv6:
  type <тип icmpv6>

ip:
  protocol <протокол>
  daddr <адрес получателя>
  saddr <адрес отправителя>

ip6:
  daddr <адрес получателя>
  saddr <адрес отправителя>

tcp:
  dport <порт получателя>
  sport <порт отправителя>

udp:
  dport <порт получателя>
  sport <порт отправителя>

sctp:
  dport <порт получателя>
  sport <порт отправителя>

ct:
  state <new | established | related | invalid>

```

#### Удаление

Отдельные правила могут быть удалены только с помощью маркера. Команда `nft --handle list` выведет список маркеров.

Ниже приведён пример правила с маркером и команда для его удаления. Аргумент `--numeric` позволяет выводить IP-адреса в численном виде.

 `# nft --handle --numeric list chain inet filter input` 
```
table inet fltrTable {
     chain input {
          type filter hook input priority 0;
          ip saddr 127.0.0.1 accept # handle 10
     }
}

```

```
# nft delete rule inet fltrTable input handle 10

```

Стирание всех цепочек таблицы выполняется командой `nft flush table`. Отдельные цепочки могут быть стёрты командами `nft flush chain` или `nft delete rule`.

```
# nft flush table foo
# nft flush chain foo bar
# nft delete rule ip6 foo bar

```

Первая команда стирает все цепочки в ip-таблице `foo`. Вторая - цепочку `bar` в ip-таблице `foo`. Третья удаляет все правила в цепочке `bar` в ip6-таблице `foo`.

### Полная перезагрузка правил

Создать файл для новых правил:

```
# echo "flush ruleset" > /tmp/nftables 

```

Сбросить дамп правил в новый файл:

```
# nft -s list ruleset >> /tmp/nftables

```

Теперь можно редактировать файл `/tmp/nftables`, создавая и изменяя правила. Применить изменения можно командой:

```
# nft -f /tmp/nftables

```

## Примеры

### Рабочая станция

 `/etc/nftables.conf` 
```
flush ruleset

table inet filter {
	chain input {
		type filter hook input priority 0; policy drop;

		iif lo accept comment "Accept any localhost traffic"
		ct state invalid drop comment "Drop invalid connections"
		ct state established,related accept comment "Accept traffic originated from us"

		ip6 nexthdr icmpv6 icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report } accept comment "Accept ICMPv6"
		ip protocol icmp icmp type { destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem } accept comment "Accept ICMP"
		ip protocol igmp accept comment "Accept IGMP"

		udp dport mdns ip6 daddr ff02::fb accept comment "Accept mDNS"
		udp dport mdns ip daddr 224.0.0.251 accept comment "Accept mDNS"

		udp sport 1900 udp dport >= 1024 ip6 saddr { fd00::/8, fe80::/10 } meta pkttype unicast limit rate 4/second burst 20 packets accept comment "Accept UPnP IGD port mapping reply"
		udp sport 1900 udp dport >= 1024 ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } meta pkttype unicast limit rate 4/second burst 20 packets accept comment "Accept UPnP IGD port mapping reply"

		udp sport netbios-ns udp dport >= 1024 meta pkttype unicast ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept Samba Workgroup browsing replies"
		udp sport netbios-ns udp dport >= 1024 meta pkttype unicast ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept Samba Workgroup browsing replies"

		counter comment "Count any other traffic"
	}

	chain forward {
		type filter hook forward priority 0; policy drop;
	}

	chain output {
		type filter hook output priority 0; policy accept;
	}

}

```

### Сервер

 `/etc/nftables.conf` 
```
flush ruleset

table inet filter {
	chain input {
		type filter hook input priority 0; policy drop;

		iif lo accept comment "Accept any localhost traffic"
		ct state invalid drop comment "Drop invalid connections"
		ct state established,related accept comment "Accept traffic originated from us"

		ip6 nexthdr icmpv6 icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report } accept comment "Accept ICMPv6"
		ip protocol icmp icmp type { destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem } accept comment "Accept ICMP"
		ip protocol igmp accept comment "Accept IGMP"

		udp dport mdns ip6 daddr ff02::fb accept comment "Accept mDNS"
		udp dport mdns ip daddr 224.0.0.251 accept comment "Accept mDNS"

		tcp dport ssh accept comment "Accept SSH on port 22"

		tcp dport { http, https, 8008, 8080 } accept comment "Accept HTTP (ports 80, 443, 8008, 8080)"

		meta l4proto { tcp, udp } th dport 2049 ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept NFS"
		meta l4proto { tcp, udp } th dport 2049 ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept NFS"

		udp dport netbios-ns ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept NetBIOS Name Service (nmbd)"
		udp dport netbios-ns ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept NetBIOS Name Service (nmbd)"
		udp dport netbios-dgm ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept NetBIOS Datagram Service (nmbd)"
		udp dport netbios-dgm ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept NetBIOS Datagram Service (nmbd)"
		tcp dport netbios-ssn ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept NetBIOS Session Service (smbd)"
		tcp dport netbios-ssn ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept NetBIOS Session Service (smbd)"
		tcp dport microsoft-ds ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept Microsoft Directory Service (smbd)"
		tcp dport microsoft-ds ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept Microsoft Directory Service (smbd)"

		udp sport bootpc udp dport bootps ip saddr 0.0.0.0 ip daddr 255.255.255.255 accept comment "Accept DHCPDISCOVER (for DHCP-Proxy)"
		udp sport { bootpc, 4011 } udp dport { bootps, 4011 } ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept PXE"
		udp dport tftp ip6 saddr { fd00::/8, fe80::/10 } accept comment "Accept TFTP"
		udp dport tftp ip saddr { 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16, 169.254.0.0/16 } accept comment "Accept TFTP"

	}

	chain forward {
		type filter hook forward priority 0; policy drop;
	}

	chain output {
		type filter hook output priority 0; policy accept;
	}

}

```

### Ограничение скорости передачи

```
table inet filter {
	chain input {
		type filter hook input priority 0; policy drop;

		iif lo accept comment "Accept any localhost traffic"
		ct state invalid drop comment "Drop invalid connections"

		ip protocol icmp icmp type echo-request limit rate over 10/second burst 4 packets drop comment "No ping floods"
		ip6 nexthdr icmpv6 icmpv6 type echo-request limit rate over 10/second burst 4 packets drop comment "No ping floods"

		ct state established,related accept comment "Accept traffic originated from us"

		ip6 nexthdr icmpv6 icmpv6 type { destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report } accept comment "Accept ICMPv6"
		ip protocol icmp icmp type { destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem } accept comment "Accept ICMP"
		ip protocol igmp accept comment "Accept IGMP"

		tcp dport ssh ct state new limit rate 15/minute accept comment "Avoid brute force on SSH"

	}

}

```

### Переход

Если вы используете переходы (jumps), то целевая цепочка должна быть описана до перехода. Иначе будет получена ошибка `Error: Could not process rule: No such file or directory`.

```
table inet filter {
    chain web {
        tcp dport http accept
        tcp dport 8080 accept
    }
    chain input {
        type filter hook input priority 0;
        ip saddr 10.0.2.0/24 jump web
        drop
    }
}

```

### Несколько сетевых интерфейсов с разными правилами

Если у вашей системы несколько сетевых интерфейсов и вы хотите использовать для них разные наборы правил, то создайте фильтрующую цепочку-диспетчер, а после неё опишите цепочки для сетевых интерфейсов. Например, пусть ваша машина выступает в качестве домашнего маршрутизатора и вы желаете запустить веб-сервер, доступный по локальной сети (интерфейс `enp3s0`), но не из публичного интернета (интерфейс `enp2s0`). Создайте таблицу вроде этой:

```
table inet filter {
  chain input { # эта цепочка выступает в качестве диспетчера
    type filter hook input priority 0;

    iif lo accept # всегда разрешайте доступ к петевому интерфейсу
    iifname enp2s0 jump input_enp2s0
    iifname enp3s0 jump input_enp3s0

    reject with icmp type port-unreachable # отклонить трафик от остальных интерфейсов
  }
  chain input_enp2s0 { # правила для публичного интерфейса
    ct state {established,related} accept
    ct state invalid drop
    udp dport bootpc accept
    tcp dport bootpc accept
    reject with icmp type port-unreachable # весь остальной трафик
  }
  chain input_enp3s0 { # правила для веб-сервера на LAN-интерфейсе
    ct state {established,related} accept
    ct state invalid drop
    udp dport bootpc accept
    tcp dport bootpc accept
    tcp port http accept
    tcp port https accept
    reject with icmp type port-unreachable # весь остальной трафик
  }
  chain ouput { # все исходящие пакеты - разрешены
    type filter hook output priority 0;
    accept
  }
}

```

Можно поступить иначе - задать только одну строку `iifname`, например для интерфейса веб-сервера, а правила для остальных интерфейсов вместо диспетчеризации описать в одном месте.

### Маскарадинг

В nftables есть специальное ключевое слово `masquerade`, "позволяющее автоматически изменять адрес источника на адрес интерфейса-отправителя" [[5]](https://wiki.nftables.org/wiki-nftables/index.php/Performing_Network_Address_Translation_%28NAT%29#Masquerading). Это особенно удобно в ситуациях, когда IP-адрес интерфейса непредсказуем или нестабилен — например, исходящий интерфейс маршрутизатора, подключённого к нескольким интернет-провайдерам. [Маскарадинг](https://en.wikipedia.org/wiki/ru:%D0%9C%D0%B0%D1%81%D0%BA%D0%B0%D1%80%D0%B0%D0%B4%D0%B8%D0%BD%D0%B3 "wikipedia:ru:Маскарадинг") позволяет не переписывать правила межсетевого экрана для трансляции сетевых адресов (NAT) при каждом изменении IP-адреса интерфейса.

Правила работы маскарадинга:

*   опция `masquerading` в ядре Linux должна быть включена (в стандартном ядре она включена по умолчанию); в противном случае задайте параметр ядра `CONFIG_NFT_MASQ=m`.
*   ключевое слово `masquerade` может использоваться только в цепочке типа `nat`.
*   masquerading является подвидом [SNAT](https://en.wikipedia.org/wiki/Network_Address_Translation#SNAT "wikipedia:Network Address Translation"), поэтому работает только исходящих интерфейсов.

Пример правил межсетевого экрана для машины с двумя интерфейсами, локальным `enp3s0` и публичным `enp2s0`:

```
table inet nat {
  chain prerouting {
    type nat hook prerouting priority -100;
  }
  chain postrouting {
    type nat hook postrouting priority 100;
    oifname "enp2s0" masquerade
  }
}

```

Поскольку таблица выше относится к типу `inet`, то маскарадингу подвергаются пакеты и IPv4, и IPv6\. Чтобы ограничить маскарадинг только IPv4-пакетами (т.к. у IPv6 большое пространство адресов и NAT не требуется) либо добавьте выражение `meta nfproto ipv4` перед `oifname "enp2s0" masquerade`, либо измените тип таблицы на `ip`.

### NAT с пробросом портов

Ниже приведён пример проброса портов 22 и 80 на адрес `*ip-адрес_получателя*`. Необходимо предварительно с помощью [sysctl](/index.php/Sysctl "Sysctl") установить параметры `net.ipv4.ip_forward` и `net.ipv4.conf.*wan_интерфейс*.forwarding` на `1`.

```
table ip nat {
  chain prerouting {
    type nat hook prerouting priority -100;

    tcp dport { ssh, http } dnat to *ip-адрес_получателя*
  }

  chain postrouting {
    type nat hook postrouting priority 100;

    ip daddr *ip-адрес_получателя* masquerade
  }
}
</nowiki>
```

## Советы и рекомендации

### Настройка простого сетевого экрана

Дополнительную информацию можно найти в статье [Simple stateful firewall](/index.php/Simple_stateful_firewall_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Simple stateful firewall (Русский)").

#### Одиночная машина

Сотрите текущий набор правил:

```
# nft flush ruleset

```

Добавьте таблицу:

```
# nft add table inet filter

```

Добавьте базовые цепочки input, forward и output. Политики для входящих и пересылаемых пакетов должна быть drop. Политика для исходящих пакетов — accept.

```
# nft add chain inet filter input '{ type filter hook input priority 0 ; policy drop ; }'
# nft add chain inet filter forward '{ type filter hook forward priority 0 ; policy drop ; }'
# nft add chain inet filter output '{ type filter hook output priority 0 ; policy accept ; }'

```

Добавьте две обычные цепочки, которые будут обрабатывать пакеты протоколов TCP и UDP:

```
# nft add chain inet filter TCP
# nft add chain inet filter UDP

```

Разрешите related и established трафик:

```
# nft add rule inet filter input ct state related,established accept

```

Разрешите трафик на петлевой интерфейс:

```
# nft add rule inet filter input iif lo accept

```

Заблокируйте invalid трафик:

```
# nft add rule inet filter input ct state invalid drop

```

Разрешите пакеты ICMP и IGMP:

```
# nft add rule inet filter input ip6 nexthdr icmpv6 icmpv6 type '{ destination-unreachable, packet-too-big, time-exceeded, parameter-problem, mld-listener-query, mld-listener-report, mld-listener-reduction, nd-router-solicit, nd-router-advert, nd-neighbor-solicit, nd-neighbor-advert, ind-neighbor-solicit, ind-neighbor-advert, mld2-listener-report }' accept
# nft add rule inet filter input ip protocol icmp icmp type '{ destination-unreachable, router-solicitation, router-advertisement, time-exceeded, parameter-problem }' accept
# nft add rule inet filter input ip protocol igmp accept

```

Новый UDP-трафик будет передаваться цепочке UDP:

```
# nft add rule inet filter input ip protocol udp ct state new jump UDP

```

Новый TCP-трафик будет передаваться цепочке TCP:

```
# nft add rule inet filter input 'ip protocol tcp tcp flags & (fin|syn|rst|ack) == syn ct state new jump TCP'

```

Заблокировать весь трафик, который не обрабатывается другими правилами:

```
# nft add rule inet filter input ip protocol udp reject
# nft add rule inet filter input ip protocol tcp reject with tcp reset
# nft add rule inet filter input counter reject with icmp type prot-unreachable

```

В этом месте необходимо выбрать, какие порты будут оставаться открытыми для входящих соединений, обрабатываемых цепочками TCP и UDP. Например, открыть соединения для веб-сервера:

```
# nft add rule inet filter TCP tcp dport 80 accept

```

Разрешить HTTPS-соединения для веб-сервера на порте 443:

```
# nft add rule inet filter TCP tcp dport 443 accept

```

Разрешить SSH-трафик на порт 22:

```
# nft add rule inet filter TCP tcp dport 22 accept

```

Разрешить входящие DNS-запросы:

```
# nft add rule inet filter TCP tcp dport 53 accept
# nft add rule inet filter UDP udp dport 53 accept

```

В конце не забудьте сохранить набор правил, чтобы они стали постоянными.

### Предотвращение атак перебором

[Sshguard](/index.php/Sshguard "Sshguard") может обнаруживать атаки перебором и модифицировать сетевые экраны, временно помещая IP-адреса в чёрный список. Описание настройки nftables для работы с sshguard можно найти в статье [Sshguard#nftables](/index.php/Sshguard#nftables "Sshguard").

## Решение проблем

### Работа с Docker

*nftables* может создавать помехи сетевой работе контейнеров [Docker](/index.php/Docker_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Docker (Русский)") (возможно, и другим средствам виртуализации тоже). В частности, политика `drop` цепочки `forward` блокирует пакеты, источником которых является docker. Если вы не хотите удалять эту цепочку, то сделайте следующее:

1.  [Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [iptables-nft](https://www.archlinux.org/packages/?name=iptables-nft); он содержит iptables-совместимый интерфейс nftables, который docker сможет использовать.
2.  Модифицируйте цепочку `forward` таблицы `inet`:

    ```
    chain forward {
      type filter hook forward priority security; policy drop
      mark 1 accept

    ```

3.  Добавьте цепочку DOCKER-USER в таблицу `ip filter`, чтобы помечать (mark) пакеты docker:

    ```
    table ip filter {
      chain DOCKER-USER {
        mark set 1
      }
    }

    ```

Теперь сгенерированные контейнером docker пакеты будут маркироваться и пересылаться дальше, поскольку docker уже их отфильтровал (цепочка `forward` в docker использует политику `drop`).

## Смотрите также

*   [netfilter nftables](https://wiki.nftables.org/) — документация от разработчиков проекта netfilter
*   [debian:nftables](https://wiki.debian.org/nftables "debian:nftables") — статья на Debian-wiki
*   [gentoo:nftables](https://wiki.gentoo.org/wiki/nftables "gentoo:nftables") — статья на Gentoo-wiki
*   [First release of nftables](https://lwn.net/Articles/324251/) — выход nftables (2009)
*   [nftables quick howto](https://home.regit.org/netfilter-en/nftables-quick-howto/) — советы и подсказки
*   [The return of nftables](https://lwn.net/Articles/564095/) — обновление nftables (2013)
*   [What comes after "iptables"?](https://developers.redhat.com/blog/2016/10/28/what-comes-after-iptables-its-successor-of-course-nftables/) — nftables со временем заменит iptables