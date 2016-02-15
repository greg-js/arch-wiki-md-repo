Репозиторий _multilib_ позволяет запускать и собирать 32-битные приложения в 64-битной версии Arch Linux. Он содержит пакеты с 32-битными версиями библиотек, которые используются для запуска 32-битных программ. Эти библиотеки располагаются в каталоге `/usr/lib32`.

## Contents

*   [1 Структура каталогов](#.D0.A1.D1.82.D1.80.D1.83.D0.BA.D1.82.D1.83.D1.80.D0.B0_.D0.BA.D0.B0.D1.82.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2)
*   [2 Включение](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5)
*   [3 Отключение](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Структура каталогов

При использовании _multilib_ на 64-битной версии Arch Linux поддерживается структура каталогов, аналогичная структуре, принятой в Debian: 32-битные версии библиотек размещаются в `/usr/lib32`, а обычные для системы 64-битные — в `/usr/lib`.

## Включение

Для использования репозитория [multilib](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#multilib "Official repositories (Русский)") раскомментируйте секцию `[multilib]` в файле `/etc/pacman.conf` (обе строки):

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

Затем обновите список пакетов и выполните полное обновление системы, набрав `pacman -Syu`.

**Обратите внимание:** Arch Linux не поддерживает частичное обновление, поэтому параметр `-u` необходим.

## Отключение

Чтобы восстановить чистую 64-битную систему, выполните следующую команду, которая удалит все пакеты из _multilib_:

```
# pacman -R $(paclist multilib | cut -f1 -d' ')

```

**Обратите внимание:** Если при этом возникнут конфликты с [gcc-libs](https://www.archlinux.org/packages/?name=gcc-libs), установите заново 64-битные версии gcc-libs и всех пакетов в [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), выполнив следующую команду:

```
# pacman -S gcc-libs base-devel

```

и снова попытайтесь удалить все пакеты _multilib_.

Закомментируйте секцию `[multilib]` в `/etc/pacman.conf`:

```
#[multilib]
#Include = /etc/pacman.d/mirrorlist

```

Затем обновите список пакетов и выполните полное обновление системы, набрав `pacman -Syu`.

## Смотрите также

*   [Multilib Project](/index.php/64-bit_FAQ_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D0.B9_Multilib "64-bit FAQ (Русский)")
*   [arch-multilib](//mailman.archlinux.org/mailman/listinfo/arch-multilib) список рассылки