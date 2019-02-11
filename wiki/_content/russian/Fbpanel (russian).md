Fbpanel - лёгковесная, гибко настраиваемая панель для рабочего стола.
Страницы проекта:
[GitHub](https://github.com/aanatoly/fbpanel)
[SourceForge](http://fbpanel.sourceforge.net/)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 wincmd plugin](#wincmd_plugin)
*   [3 Решение проблем](#Решение_проблем)

## Установка

Установите [fbpanel](https://aur.archlinux.org/packages/fbpanel/).

## Настройка

Выполните от пользователя:

```
$fbpanel

```

Возможно, что [fbpanel](https://aur.archlinux.org/packages/fbpanel/) выдаст ошибку, ссылаясь на невозможность открытия `/home/user/.config/fbpanel/default`
Ничего страшного здесь нет, достаточно создать дефолтный файл конфигурации:

```
$mkdir ~/.config/fbpanel
$cp /usr/share/fbpanel/default ~/.config/fbpanel

```

### wincmd plugin

Плагин по умолчанию включён, но может не корректно отображать значки, которые не сможет найти. В этом случае укажите путь к иконкам:

```
Plugin {
  type = wincmd
  config {
      image = ~/images/my_image.png
      tooltip = Left click to iconify all windows. Middle click to shade them.
  }
}

```

**Совет:** Вы можете использовать изображения в качестве значков.

`/usr/share/fbpanel/images/` в таком случае необходимо скопировать в домашнюю директорию пользователя:

```
$mkdir ~/images
$cp -R /usr/share/fbpanel/images/ ~/images 

```

## Решение проблем

В случае получения следующего сообщения при запуске:

```
volume: can't open /dev/mixer
fbpanel: cant't start plugin volume

```

Закоментируйте следующие строки в файле конфигурации:

```
Plugin {
   type = volume
}

```