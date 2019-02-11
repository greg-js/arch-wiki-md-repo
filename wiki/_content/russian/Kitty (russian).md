**Состояние перевода:** На этой странице представлен перевод статьи [Kitty](/index.php/Kitty "Kitty"). Дата последней синхронизации: 18 ноября 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Kitty&diff=0&oldid=558439).

[Kitty](https://sw.kovidgoyal.net/kitty/index.html) — это программируемый эмулятор терминала на основе OpenGL. Kitty поддерживает мозаичный режим (тайлинг), TrueColor, лигатуры и расширения для работы с клавиатурой и рендеринга изображений.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Использование](#Использование)
    *   [2.1 Kittens](#Kittens)
*   [3 Настройка](#Настройка)
*   [4 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [kitty](https://www.archlinux.org/packages/?name=kitty).

## Использование

Новые вкладки и окна можно создавать и изменять с помощью различных сочетаний клавиш, начинающихся с `ctrl+shift`. Разметки (layouts) можно переключать с помощью `ctrl+shift+l`, также они могут быть сохранены и восстановлены.

Режим *full keyboard mode* позволяет различать неоднозначные сочетания клавиш, например, `ctrl+i` vs `tab`. Более того, новые эффекты текста (например, волнистое подчёркивание) также доступны для приложений, поддерживающих их.

### Kittens

В kitty есть фреймворк для создания подпрограмм, называемых [kittens](https://sw.kovidgoyal.net/kitty/#kittens). Некоторые из них:

```
$ kitty +kitten icat image.jpeg             # показать изображение в терминале (требуется imagemagick)
$ kitty +kitten diff file1 file2            # показать diff двух файлов
$ kitty +kitten clipboard                   # этот kitten позволяет работать с буфером обмена даже через ssh

```

## Настройка

Kitty настраивается через файл конфигурации `~/.config/kitty/kitty.conf`, где можно изменить параметры шрифтов, цветов, курсоров и поведения скролла. Доступные опции можно посмотреть на [официальном сайте](https://sw.kovidgoyal.net/kitty/conf.html), где также доступен полный [конфигурационный файл](https://sw.kovidgoyal.net/kitty/conf.html#sample-kitty-conf), используемый по умолчанию.

## Смотрите также

*   [Репозиторий на GitHub](https://github.com/kovidgoyal/kitty)