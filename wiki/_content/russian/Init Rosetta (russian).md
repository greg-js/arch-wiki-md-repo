## Таблица взаимодействия с сервисами в Init и systemd

| Команда init | Команда systemd | Комментарий |
| rc.d {start |stop | restart...} daemon | systemctl {start | stop | restart...} daemon.service | Изменить состояние сервиса (демона). |
| rc.d list | systemctl list-unit-files --type=service | Список сервисов (демонов). |
| chkconfig daemon {on | off} | systemctl {enable | disable} daemon.service | Выключить или включить сервис (демон). |
| chkconfig daemon --add | systemctl daemon-reload | Используется при создании или изменении конфигурационных файлов/скриптов. |

## Таблица уровней запуска и их аналогов в systemd

| Уровнень запуска SysV | Systemd Target | Примечание |
| 0 | runlevel0.target, poweroff.target | Выключить систему. |
| 1, s, single | runlevel1.target, rescue.target | Однопользовательский уровень запуска. |
| 2, 4 | runlevel2.target, runlevel4.target, multi-user.target | Уровень запуска, определенный пользователем/специфичный для узла. По умолчанию соответствует уровню запуска 3. |
| 3 | runlevel3.target, multi-user.target | Многопользовательский режим без графики. Пользователи, как правило, входят с помощью множества консолей или через сеть. |
| 5 | runlevel5.target, graphical.target | Многопользовательский режим с графикой. Обычно эквивалентен запуску всех сервисов уровня 3 и графическому менеджеру входа. |
| 6 | runlevel6.target, reboot.target | Перезагрузка. |
| emergency | emergency.target | Аварийная оболочка. |