Raspberry Pi - минималистичный компьютер построенный на архитектуре ARMv6.

**Обратите внимание:** Информация о поддержке архитектуры ARM приведена здесь: [http://archlinuxarm.org/](http://archlinuxarm.org/)

## Wayland

Wayland - новый оконный протокол для Linux. Использование Wayland требует изменения и переустановки части вашего системного программного обеспечения. Дополнительную информацию можно найти на домашней странице [Wayland](http://wayland.freedesktop.org/). Ниже рассмотрена установка и настройка Wayland на Raspberry PI.

## Установка

Установка минимальной конфигурации операционной системы Arch Linux на Raspberry PI рассмотрена [здесь](http://archlinuxarm.org/platforms/armv6/raspberry-pi#qt-platform_tabs-ui-tabs2).

Обязательно обновляем систему

```
$ pacman -Syu 

```

Устанавливаем Wayland (из extra) [wayland](https://www.archlinux.org/packages/?name=wayland)

```
$ pacman -S wayland

```