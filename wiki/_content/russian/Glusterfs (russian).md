**Состояние перевода:** На этой странице представлен перевод статьи [Glusterfs](/index.php/Glusterfs "Glusterfs"). Дата последней синхронизации: 24 июля 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Glusterfs&diff=0&oldid=482799).

[Glusterfs](https://www.gluster.org/) - это масштабируемая сетевая [файловая система.](/index.php/File_systems_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "File systems (Русский)").

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [glusterfs](https://www.archlinux.org/packages/?name=glusterfs).

## Настройка

Glusterfs можно настроить для работы во многих различных конфигурациях в зависимости от потребностей, включая распределенные и реплицированные. В приведенном ниже примере создается реплицируемый сервер с двумя узлами, каждый из которых имеет узлы gluster1 и gluster2, каждый из которых имеет два диска, один из которых содержит ОС sda, а другой - совместно используемый glusterfs sdb. Если не указано, что все настройки выполняются на gluster1

*   [Запустите/включите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5/%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Запустите/включите") демон gluster `glusterd.service` на обоих серверах.

*   Подключитесь к серверам

```
 # gluster peer probe gluster2

```

*   Разметка и форматирование диска glusterfs на обоих серверах
    *   Upstream советует создать один раздел и отформатировать его как xfs

*   На обоих серверах автомонтируйте диски, [добавив](/index.php/%D0%94%D0%BE%D0%B1%D0%B0%D0%B2%D1%8C%D1%82%D0%B5 "Добавьте") `/etc/fstab`, чтобы включить следующую строку, где `/dev/sd*XY*` является подходящим устройством (например, `/dev/sdb1`).

 `/etc/fstab`  `/dev/sd*XY* /export/sd*XY* xfs defaults 0 0` 

*   На обоих серверах [смонтируйте](/index.php/%D0%A1%D0%BC%D0%BE%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B9%D1%82%D0%B5 "Смонтируйте") диски. Затем создайте "brick":

```
 # mkdir -p /export/sd*XY*/brick

```

*   Включите репликацию на основном сервере

```
 # gluster volume create gv0 replica 2 gluster1.mydomain.net:/export/sdb1/brick gluster2.mydomain.net:/export/sdb1/brick

```

*   Убедитесь, что том создан правильно

```
 # gluster volume info

```

*   Запустите том

```
 # gluster volume start gv0

```

## Смотрите также

*   [Официальное руководство по установке glusterfs](http://gluster.readthedocs.io/en/latest/Install-Guide/Overview/)
*   [Блог, посвященный настройке Glusterfs на Arch Linux](https://blog.bastelfreak.de/2016/05/short-tip-setup-glusterfs-share-on-arch-linux/)