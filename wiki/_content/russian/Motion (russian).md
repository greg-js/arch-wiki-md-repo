Ссылки по теме

*   [Настройка веб-камеры](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D0%B2%D0%B5%D0%B1-%D0%BA%D0%B0%D0%BC%D0%B5%D1%80%D1%8B "Настройка веб-камеры")

**Состояние перевода:** На этой странице представлен перевод статьи [Motion](/index.php/Motion "Motion"). Дата последней синхронизации: 15 октября 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Motion&diff=0&oldid=586124).

[Motion](https://motion-project.github.io/) — программа, которая следит за видеосигналом с камер. Она способна замечать изменение значительной части изображения, что позволяет выявлять движение.

## Установка

Установите пакет [motion](https://www.archlinux.org/packages/?name=motion).

## Настройка

Motion можно запустить с параметром `-c` , который определяет конкретный файл настроек (как это происходит в случае с программой [motionEye](https://github.com/ccrisan/motioneye/wiki)).

Если вы не указали `-c` или указанный файл не существует, Motion начнёт искать конфигурационный файл с именем 'motion.conf' в следующем порядке:

1.  Текущий каталог, из которого Motion был запущен
2.  Каталог '.motion' в домашней директории текущего пользователя (переменная окружения `$HOME`), например, `~/.motion/motion.conf`
3.  `/etc/motion/`

Файл настроек по умолчанию (`/etc/motion/motion.conf`) хорошо документирован, поэтому очень легко найти требуемые варианты настроек и способ их задания (например `rotate 90`).

Motion по умолчанию использует порт `8080` (+1 для каждой подключённой камеры), а доступ к веб-серверу и видеопотокам камер ограничен только локальными подключениями.