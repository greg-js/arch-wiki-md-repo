### Определение типа файлов по расширениям

Применение пользовательских mime может сделать работу в среде более комфортной. Некоторые mime типы или, иначе, расширения файла могут быть неизвестны системе, но это можно исправить.
XFCE и Gnome имеют возможность определения пользовательских типов по расширению файла, назначения ему значка и действий по умолчанию.

## Пример - файлы плейлиста проигрывателя xine

Xine создаёт файлы плейлиста в структурированном текстовом формате с расширением .tox.
Mime-тип плейлиста система опознает как «текст», а при попытке просмотра файла в Thunar (Nautilus) он будет открыт в текстовом редакторе оболочки по умолчанию. При привязке плейлиста средствами файлового менеджера к проигрывателю xine все обычные текстовые файлы Thunar (Nautilus) будет пытаться открыть с помощью Xine.
Во избежание подобного и необходимо определить пользовательский mime тип. Тем самым мы объявляем оболочке, что файлы с расширением tox не являются текстовыми, а для их открытия используется специальное приложение.

Для начала необходимо создать файл user-tox.xml следующего содержания

```
<?xml version="1.0"?>
 <mime-info xmlns="[http://www.freedesktop.org/standards/shared-mime-info](http://www.freedesktop.org/standards/shared-mime-info)">
  <mime-type type="video/video">
   <comment>Toxine Playlist</comment>
   <glob pattern="*.tox"/>
  </mime-type>
 </mime-info>

```

В данном случае для файлов, имеющих расширение «tox», мы определили mime тип "video/video". Значок для типа будет взят системой из папки "mimetypes" из используемого вами набора иконок (например из "/usr/share/icons/Rodent/scalable/mimetypes"). В данном случае мы используем стандартную иконку video.svg.

* * *

<small>В некоторых случаях необходимо определение полностью пользовательского типа (что позволит избежать конфликтов в системе), создав совершенно новый тип и подтип, тогда строка объявления может принять вид:</small>

<small>
```
<mime-type type="users/toxine">

```

Этому пользовательскому mime-типу "users/toxine" будет сопоставлена иконка users-toxine.svg и т.п. Естественно, иконка должна присутствовать в используемом наборе, иначе будет установлена используемая по умолчанию для неизвестных типов файлов.
Достаточно сделать ссылку на понравившуюся из используемого набора.В случае type="users/toxine" например

</small>
```
<small>ln -Ts video.svg  users-toxine.svg</small>

```

* * *

Настало время добавить наш mime тип для расширения «tox» в систему. В консоли, в директории со вновь созданным файлом user-tox.xml выполняем следующую команду:

```
xdg-mime install user-tox.xml

```

Теперь система знает, что файлы с расширением «tox» являются новым типом. Осталось научить открывать их с помощью xine.

*   в консоли, выполнив

```
echo "video/video=xine.desktop" >> ~/.local/share/applications/defaults.list 

```

и после перезапуска оконного менеждера файлы плейлиста обретут свою иконку и будут открываться в xine.
<small><tt>если вы определяли другой тип, соответственно замените video/video на свой!</tt></small>

*   Можно просто перезагрузить Х, а при клике на изменившуюся иконку плейлиста Thunar (Nautilus) сам запросит программу для открытия типа "Toxine Playlist". Вам останется только указать xine в качестве таковой.

* * *

Подобным образом можно настроить различные ассоциации файлов по расширениям с приложениями, полностью определять и переопределять пользовательские типы и иконки.

* * *