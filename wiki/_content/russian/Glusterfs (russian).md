Ссылки по теме

*   [Ceph](/index.php/Ceph "Ceph")

**Состояние перевода:** На этой странице представлен перевод статьи [Glusterfs](/index.php/Glusterfs "Glusterfs"). Дата последней синхронизации: 6 октября 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Glusterfs&diff=0&oldid=568751).

[Glusterfs](https://www.gluster.org/) — масштабируемая сетевая [файловая система](/index.php/%D0%A4%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D0%B0%D1%8F_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0 "Файловая система").

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [glusterfs](https://www.archlinux.org/packages/?name=glusterfs).

## Настройка

Glusterfs можно настроить для работы во многих различных конфигурациях в зависимости от потребностей, включая распределённые и реплицированные. В приведённом ниже примере создаётся реплицируемый сервер с двумя узлами, каждый из которых (gluster1 и gluster2) имеет два диска, один из которых содержит ОС (`sda`), а другой — совместно используемый glusterfs (`sdb`). Если не указано иного, все настройки выполняются на gluster1:

*   [Запустите/включите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5/%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Запустите/включите") службу `glusterd.service` на обоих серверах.
*   Соедините сервера:

```
 # gluster peer probe gluster2

```

*   Разметьте и отформатируйте диск glusterfs на обоих серверах
    *   Upstream советует создать один раздел и отформатировать его в XFS
*   На обоих серверах автоматически смонтируйте диски, [добавив](/index.php/%D0%94%D0%BE%D0%B1%D0%B0%D0%B2%D1%8C%D1%82%D0%B5 "Добавьте") следующую строку в `/etc/fstab`, где `/dev/sd*XY*` — подходящее устройство (например, `/dev/sdb1`).

 `/etc/fstab`  `/dev/sd*XY* /export/sd*XY* xfs defaults 0 0` 

*   [Смонтируйте](/index.php/%D0%A1%D0%BC%D0%BE%D0%BD%D1%82%D0%B8%D1%80%D1%83%D0%B9%D1%82%D0%B5 "Смонтируйте") диски на обоих серверах. Затем создайте *brick*:

```
 # mkdir -p /export/sd*XY*/brick

```

*   Включите репликацию на основном сервере:

```
 # gluster volume create gv0 replica 2 gluster1.mydomain.net:/export/sdb1/brick gluster2.mydomain.net:/export/sdb1/brick

```

*   Убедитесь, что том создан правильно:

```
 # gluster volume info

```

*   Запустите том:

```
 # gluster volume start gv0

```

*   Смонтируйте том:

```
 # mkdir -p /mnt/glusterClientMount
 # mount -t glusterfs gluster1:/gv0 /mnt/glusterClientMount

```

## Смотрите также

*   [Официальное руководство по установке glusterfs](https://docs.gluster.org/en/latest/Install-Guide/Overview/)
*   [Блог о настройке Glusterfs на Arch Linux](https://blog.bastelfreak.de/2016/05/short-tip-setup-glusterfs-share-on-arch-linux/)