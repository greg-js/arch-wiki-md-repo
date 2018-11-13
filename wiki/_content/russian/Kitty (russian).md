[Kitty](https://sw.kovidgoyal.net/kitty/index.html) - это программируемый эмулятор терминала на основе OpenGL. Kitty поддерживает тайлинг, truecolor, лигатуры и расширения для работы с клавиатурой и рендеринга изображений.

## Contents

*   [1 Установка](#Установка)
*   [2 Configuration](#Configuration)
*   [3 Использование](#Использование)
    *   [3.1 Kittens](#Kittens)
*   [4 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [kitty](https://www.archlinux.org/packages/?name=kitty).

## Configuration

Kitty настраивается через файл конфигурации `~/.config/kitty/kitty.conf`. Доступные опции можно посмотреть по [ссылке](https://sw.kovidgoyal.net/kitty/conf.html). В конце страницы можно посмотреть полный конфигурационный файл, используемый по умолчанию.

## Использование

После установки вы можете запустить kitty командой:

```
$ kitty

```

### Kittens

Kitty имеет фреймворк для создания подпрограмм, называемыми kittens. Некоторые из них:

```
$ kitty +kitten icat image.jpeg             # показать изображение в терминале (требуется imagemagick)
$ kitty +kitten diff file1 file2            # показать diff двух файлов
$ kitty +kitten clipboard                   # этот kitten позволяет работать с буфером обмена даже через ssh

```

## Смотрите также

*   [GitHub repository](https://github.com/kovidgoyal/kitty)