Ссылки по теме

*   [Install bundled 32-bit system in Arch64](/index.php/Install_bundled_32-bit_system_in_Arch64 "Install bundled 32-bit system in Arch64")

Репозиторий *multilib* позволяет запускать и собирать 32-битные приложения в 64-битной версии Arch Linux. Он содержит пакеты с 32-битными версиями библиотек, которые используются для запуска 32-битных программ. Эти библиотеки располагаются в каталоге `/usr/lib32`.

## Contents

*   [1 Структура каталогов](#Структура_каталогов)
*   [2 Включение](#Включение)
*   [3 Отключение](#Отключение)
*   [4 Смотрите также](#Смотрите_также)

## Структура каталогов

При использовании *multilib* на 64-битной версии Arch Linux поддерживается структура каталогов, аналогичная структуре, принятой в Debian: 32-битные версии библиотек размещаются в `/usr/lib32`, а обычные для системы 64-битные — в `/usr/lib`.

## Включение

Для использования репозитория [multilib](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#multilib "Official repositories (Русский)") раскомментируйте секцию `[multilib]` в файле `/etc/pacman.conf` (обе строки):

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

Затем обновите список пакетов и выполните полное обновление системы, набрав `pacman -Syu`.

**Примечание:** Arch Linux не поддерживает частичное обновление, поэтому параметр `-u` необходим.

## Отключение

Чтобы восстановить чистую 64-битную систему, выполните следующую команду, которая удалит все пакеты из *multilib*:

```
# pacman -R $(paclist multilib | cut -f1 -d' ')

```

**Примечание:** Если при этом возникнут конфликты с [gcc-libs](https://www.archlinux.org/packages/?name=gcc-libs), установите заново 64-битные версии gcc-libs и всех пакетов в [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), выполнив следующую команду:
```
# pacman -S gcc-libs base-devel

```

и снова попытайтесь удалить все пакеты *multilib*.

Закомментируйте секцию `[multilib]` в `/etc/pacman.conf`:

```
#[multilib]
#Include = /etc/pacman.d/mirrorlist

```

Затем обновите список пакетов и выполните полное обновление системы, набрав `pacman -Syu`.

## Смотрите также

*   [arch-multilib](//mailman.archlinux.org/mailman/listinfo/arch-multilib) список рассылки