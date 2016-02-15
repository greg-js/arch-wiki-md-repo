_pkgstats_ отсылает список всех установленных пакетов, [модулей ядра](https://www.archlinux.org/news/pkgstats-now-collects-modules-usage/), архитектуру и используемые вами зеркала в проект Arch Linux. Эта информация анонимна и не может быть использована для вашей идентификации, однако, она помогает разработчикам Arch в распределении приоритености их задач.

## Установка

Вы можете установить [pkgstats](https://www.archlinux.org/packages/?name=pkgstats) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

## Использование

pkgstats настроен так, что выполняется автоматически каждую неделю с помощью [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

Вы можете запустить его вручную, выполнив команду `pkgstats`. Выполните `pkgstats -h` для отображения информации по использованию.

## Результаты

Посмотреть статистику можно здесь: [https://www.archlinux.de/?page=Statistics](https://www.archlinux.de/?page=Statistics).

Для дополнительной информации, смотрите официальное [обсуждение на форуме](https://bbs.archlinux.org/viewtopic.php?id=105431).