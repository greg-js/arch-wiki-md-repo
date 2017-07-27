**Состояние перевода:** На этой странице представлен перевод статьи [OpenAFS](/index.php/OpenAFS "OpenAFS"). Дата последней синхронизации: 24 июля 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=OpenAFS&diff=0&oldid=482800).

AFS - это продукт распределенной файловой системы, впервые внедренный в Университете Карнеги-Меллона и поддерживаемый и разработанный как продукт корпорации Transarc (теперь IBM Pittsburgh Labs). Он предлагает архитектуру клиент-сервер для совместного использования файлов и репликации контента только для чтения, обеспечивая независимость от местоположения, масштабируемость, безопасность и прозрачные возможности миграции. AFS доступен для широкого спектра гетерогенных систем, включая UNIX, Linux, MacOS X и Microsoft Windows.

IBM разветвила источник продукта AFS и сделала копию источника, доступного для развития и поддержки сообщества. Они назвали выпуск OpenAFS.

На этой странице описывается только клиентская сторона.

## Contents

*   [1 Установка клиента](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0)
*   [2 Устранение неполадок](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BF.D0.BE.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA)
    *   [2.1 aklog: a pioctl failed while obtaining tokens for cell ...](#aklog:_a_pioctl_failed_while_obtaining_tokens_for_cell_...)
*   [3 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка клиента

Установите клиент openafs с пакетами [openafs](https://aur.archlinux.org/packages/openafs/) и [openafs-modules](https://aur.archlinux.org/packages/openafs-modules/).

Отредактируйте `/etc/openafs/ThisCell` и поместите ячейку по умолчанию. Вы можете проверить ячейки в `/etc/openafs/CellServDB`.

[Запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `openafs-client`.

## Устранение неполадок

### aklog: a pioctl failed while obtaining tokens for cell ...

Возможно, ваш afs-клиент не работает. Запустите его, как описано в [#Установка клиента](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D0.B0).

## Смотрите также

*   Официальный сайт [https://www.openafs.org/](https://www.openafs.org/)