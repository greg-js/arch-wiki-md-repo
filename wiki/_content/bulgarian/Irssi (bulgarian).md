## Contents

*   [1 Увод](#.D0.A3.D0.B2.D0.BE.D0.B4)
*   [2 Инсталация](#.D0.98.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D1.8F)
*   [3 Настройки](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
*   [4 Инсталиране на скриптове](#.D0.98.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B8.D1.80.D0.B0.D0.BD.D0.B5_.D0.BD.D0.B0_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.BE.D0.B2.D0.B5)

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