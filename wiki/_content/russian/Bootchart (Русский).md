**Состояние перевода:** На этой странице представлен перевод статьи [Bootchart](/index.php/Bootchart "Bootchart"). Дата последней синхронизации: 29 февраля 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Bootchart&diff=0&oldid=419232).

**Примечание:** Bootchart является частью systemd. Эта статья описывает bootchart до того, как пакет стал непосредственной частью systemd.

[Bootchart](https://meego.gitorious.org/meego-developer-tools/bootchart) это ручная утилита используемая для анализа и ускорения загрузки компьютера. Утилита содержит в себе bootchartd демона, который записывает и создаёт изображение. (на основе записей)

## Contents

*   [1 Установка Bootchart](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_Bootchart)
*   [2 Запуск Bootchart](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Bootchart)
    *   [2.1 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [3 Генерирование изображения](#.D0.93.D0.B5.D0.BD.D0.B5.D1.80.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B8.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
*   [4 Bootchart2](#Bootchart2)
*   [5 Полезные ссылки](#.D0.9F.D0.BE.D0.BB.D0.B5.D0.B7.D0.BD.D1.8B.D0.B5_.D1.81.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Установка Bootchart

Пакет [bootchart](https://www.archlinux.org/packages/?name=bootchart) находится в репозитории extra.

## Запуск Bootchart

Для использования bootchart или для установки в качестве демона при загрузки системы самостоятельно добавьте скрипт для запуска. (*`rc.sysinit`*)

**Примечание:** Если вы самостоятельно добавили демона для запуска, то Вам также придётся останавливать работу вручную.

### Настройка

Это в основном копирование настроек загрузчика `init=/usr/bin/bootchartd`.Детальнее [Kernel parameters (Русский)](/index.php/Kernel_parameters_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel parameters (Русский)"). Bootchart прекращает свою работу при логине в систему. (Терминал, [экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер"))

## Генерирование изображения

Для генерации изображения используйте:

```
bootchart-render

```

в каталоге, где Вы имеете права на запись. Это команда создаёт `bootchart.png` изображение, как не сложно догадаться, в формате png. На изображении будет графически показано время загрузки процесса и т.д.

**Примечание:** Вам понадобится установленный и настроенный Java runtime пакет, прежде чем вы сможете использовать `bootchart-render`.

## Bootchart2

**Примечание:** Альтернативой Bootchart является [bootchart2](https://github.com/mmeeks/bootchart). Bootchart2 использует python, вместо JVM, и требует: pygtk, git и busybox. Смотрите GRUB и GRUB2 для конфигурации.

Bootchart2 **/etc/bootchartd.conf**

```
EXIT_PROC="kdm_greet xterm konsole gnome-terminal metacity mutter compiz ldm icewm-session enlightenment"

```

Строка выше может быть скорректирована, или оставлена пустой.

Bootchart2 также может быть использован с [E4rat (Русский)](/index.php/E4rat_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "E4rat (Русский)").

## Полезные ссылки

*   [Bootchart home page](http://www.bootchart.org/)