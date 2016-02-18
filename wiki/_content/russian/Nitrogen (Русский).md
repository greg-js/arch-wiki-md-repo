[Nitrogen](http://projects.l3ib.org/nitrogen/) - это быстрый и легковесный менеджер обоев рабочего стола X Window System.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [2.1 Установка обоев](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.B1.D0.BE.D0.B5.D0.B2)
    *   [2.2 Сохранение обоев](#.D0.A1.D0.BE.D1.85.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D0.B1.D0.BE.D0.B5.D0.B2)

## Установка

Пакет [nitrogen](https://www.archlinux.org/packages/?name=nitrogen) доступен в [официальных репозиториях](/index.php/Official_Repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official Repositories (Русский)").

## Использование

Для справки выполните

```
$ nitrogen --help

```

Следующие примеры помогут вам освоиться.

### Установка обоев

Чтобы установить и показывать обои из определнного каталога рекурсивно, выполните:

```
$ nitrogen /path/to/image/directory/

```

Чтобы установить и показывать обои из определнного каталога *не* рекурсивно, выполните:

```
$ nitrogen --no-recurse /path/to/image/directory/

```

### Сохранение обоев

Чтобы выбранные обои устанавливались в последующих сессиях, добавьте в ваш стартовый файл (~/.xinitrc, ~/.config/openbox/autostart и др.):

```
nitrogen --restore &

```