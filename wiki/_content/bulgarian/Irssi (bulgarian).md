## Contents

*   [1 Увод](#Увод)
*   [2 Инсталация](#Инсталация)
*   [3 Настройки](#Настройки)
*   [4 Инсталиране на скриптове](#Инсталиране_на_скриптове)

## Увод

[irssi](http://www.irssi.org/) е модулиран, текстов (ncurses) клиент за IRC.

## Инсталация

```
# pacman -S irssi

```

## Настройки

*   Файлът с настройките се намира в ~/.irssi/config. Можете да стартирате irssi с друг конфигурационен файл по следния начин:

```
$ irssi --config=ФАЙЛ

```

## Инсталиране на скриптове

*   Долният пример инсталира скрипт за проверяване на правописа:

```
# pacman -S ispell
$ mkdir -p ~/.irssi/scripts/autorun
$ cd ~/.irssi/scripts
$ wget [http://scripts.irssi.org/scripts/spell.pl](http://scripts.irssi.org/scripts/spell.pl) .
# perl -MCPAN -e 'install Lingua::Ispell' 
$ irssi

```

*   Ако не искате да ползвате CPAN; [http://search.cpan.org/~jdporter/Lingua-Ispell-0.07/lib/Lingua/Ispell.pm](http://search.cpan.org/~jdporter/Lingua-Ispell-0.07/lib/Lingua/Ispell.pm)
*   В irssi

```
/script load spell.pl

```

*   Ако всичко е наред, трябва да изглежда така:

```
- - Irssi: Loaded script spell
/bind meta-s /_spellcheck

```

Трик: Alt + S проверява текущия ред за правописни грешки.

Ако искате скриптът да се стартира автоматично с пускането на irssi, направете символична връзка с autorun:

```
$ cd ~/.irssi/scripts/autorun
$ ln -s ../spell.pl .

```