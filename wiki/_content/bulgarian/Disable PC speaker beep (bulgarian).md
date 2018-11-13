## Contents

*   [1 Глобално](#Глобално)
*   [2 Локално](#Локално)
    *   [2.1 В X](#В_X)
    *   [2.2 В конзолата](#В_конзолата)
    *   [2.3 През ALSA](#През_ALSA)

# Глобално

*   Можете напълно да изключите модула на PC speaker при стартиране на Arch като добавите `!pcspkr` към `MODULES` в `/etc/rc.conf`:

```
MODULES=( ... !pcspkr ... )

```

*   Ако `lsmod | grep snd-pcsp` показва нещо, добавете `!snd-pcsp`:

```
MODULES=( ... !snd-pcsp ... )

```

В [тази](https://bbs.archlinux.org/viewtopic.php?pid=557665#p557665) тема, се препоръчва да се добавя и двете в `/etc/rc.conf`.

# Локално

## В X

```
$ xset -b

```

Можете да добавите командата в startup файл, като `~/.xinitrc`, за да се изключва всеки пък като пускате X.

## В конзолата

```
$ setterm -blength 0

```

Подобно, можете да го добавите в `~/.bashrc`.

*   Друг начин е да добавите в `~/.inputrc` следния ред:

```
set bell-style none

```

## През ALSA

*   Опитайте се да намалите до 0 PC Speaker:

```
$ amixer set 'PC Speaker' 0% mute

```

При някои звукови карти се нарича PC Beep:

```
$ amixer set 'PC Beep' 0% mute

```

Можете да позлвате `alsamixer` за GUI в конзолата:

```
$ alsamixer

```

Отидете до PC beep и натиснете бутона 'M' за да го заглушите напълно. Запомнете настройките в alsa:

```
# alsactl store

```

За да работи този метод, трябва да добавите **alsa** в списъка с daemon-и в */etc/rc.conf*