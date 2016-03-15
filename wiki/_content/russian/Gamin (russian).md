[Gamin](https://en.wikipedia.org/wiki/Gamin "wikipedia:Gamin") - система постоянного отслеживания изменений файлов и директорий. Реализует [FAM](/index.php/FAM "FAM") спецификацию и поддерживает [inotify](https://en.wikipedia.org/wiki/inotify "wikipedia:inotify"). Более новый и активно поддерживаемый проект, совместимый с FAM и заменяющий его в большинстве случаев. Является проектом [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)"), но при этом не имеет с ним зависимостей.

## Установка

Если FAM установлен, сперва [отключите](/index.php/Disable "Disable") `fam.service`; затем удалите пакет [fam](https://aur.archlinux.org/packages/fam/), игнорируя все зависимости:

```
# pacman -Rdd fam
# pacman -S [gamin](https://www.archlinux.org/packages/?name=gamin)

```

## Ссылки

*   [Gamin project page](https://people.gnome.org/~veillard/gamin/)