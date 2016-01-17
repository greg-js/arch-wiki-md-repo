# xdg-open (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

Ссылки по теме

*   [Default applications](/index.php/Default_applications "Default applications")
*   [Переменные окружения](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5_%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F "Переменные окружения")

**xdg-open** это независимый инструмент для настройки использования пользовательских приложений по умолчанию. Многие приложения вызывают внутреннюю команду `xdg-open`.

В [средах рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)") (например, [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)"), [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)"), или [Xfce](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xfce (Русский)")), _xdg-open_ просто передает аргументы файл-открывалке окружения рабочего стола (_gvfs-open_, _kde-open_, или _exo-open_ соответственно), а это значит, что ассоциации остаются за средой рабочего стола. Если среда рабочего стола не будет обнаружена (например, при использовании только [оконного менеджера](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)"), такого как [Openbox](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Openbox (Русский)")), _xdg-open_ будет использовать собственные конфигурационные файлы.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
    *   [2.1 Установка браузера по умолчанию](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B1.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80.D0.B0_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [2.2 perl-file-mimeinfo](#perl-file-mimeinfo)
*   [3 Аналоги](#.D0.90.D0.BD.D0.B0.D0.BB.D0.BE.D0.B3.D0.B8)
    *   [3.1 замена xdg-open](#.D0.B7.D0.B0.D0.BC.D0.B5.D0.BD.D0.B0_xdg-open)
    *   [3.2 mailcap](#mailcap)
    *   [3.3 mimetype](#mimetype)
    *   [3.4 Переменные окружения](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)

## Установка

_xdg-open_ является частью пакета [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils), доступного в [официальных репозиториях](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D1%85_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%8F%D1%85 "Официальных репозиториях"). _xdg-open_ используется только в пользовательской сессии рабочего стола и не следует запускать с правами администратора.

Если вы планируете запускать xdg-open без окружения рабочего стола, рекомендуется также установить [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) или [xdg-utils-mimeo](https://aur.archlinux.org/packages/xdg-utils-mimeo/)<sup><small>AUR</small></sup>, либо [mimeo](https://aur.archlinux.org/packages/mimeo/)<sup><small>AUR</small></sup> из [AUR](/index.php/AUR "AUR") как более быструю альтернативу.

## Конфигурация

_xdg-open_ использует файл конфигурации, упомянутый в [Default Applications](/index.php/Default_applications#Using_MIME_types_and_desktop_entries "Default applications"). Вы можете редактировать этот файл, используя комманду _xdg-mime_. Чтобы **узнать** mime-тип требуемого существующего файла, наберите `xdg-mime query **filetype** _file.ext_`. И наоборот, чтобы узнать какой [ярлык приложения](/index.php/Desktop_entries "Desktop entries") соответствует mime-типу, запустите `xdg-mime query **default** _mime/type_`. К общим типам относятся: `inode/directory` (файловый менеджер), `image/jpeg` (просмотрщик JPEG изображений), `application/pdf` (PDF просмотрщик).

Чтобы **изменить** ассоциированное приложение, выполните `xdg-mime **default** _application.desktop_ _mime/type_`. Например для установки [Thunar](/index.php/Thunar_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Thunar (Русский)") в качестве файлового менеджера по умолчанию, запустите:

```
$ xdg-mime default Thunar.desktop inode/directory

```

Можно задать сразу несколько mime-типов для связи с одним приложением. Следующий пример позволит сделать [Emacs](/index.php/Emacs "Emacs") вызываемым для всех возможных текстовых файлов:

```
$ xdg-mime default emacs.desktop $(grep '^text/*' /usr/share/mime/types)

```

### Установка браузера по умолчанию

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**Правильность информации, представленной в этой статье или разделе, оспаривается**

**Причина:** Для браузеров имеется много различных MIME-типов (обсуждение: [Talk:Xdg-open (Русский)#](https://wiki.archlinux.org/index.php/Talk:Xdg-open_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

Чтобы установить стандартное приложение, открывающее `http(s)://` ссылки (замените `_browser.desktop_`. на предпочитаемый вами браузер _.desktop_, например, `firefox.desktop` или `chromium.desktop`):

```
$ xdg-mime default _browser.desktop_ x-scheme-handler/http
$ xdg-mime default _browser.desktop_ x-scheme-handler/https

```

Для .html файлов:

```
$ xdg-mime default _browser.desktop_ text/html

```

Другой способ:

```
$ xdg-settings set default-web-browser _browser_.desktop

```

Чтобы проверить изменения, попробуйте зайти по адресу через _xdg-open_:

```
$ xdg-open [https://archlinux.org](https://archlinux.org)

```

### perl-file-mimeinfo

_xdg-open_ использует [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) в качестве запасного варианта ("generic") если не обнаружена [среда рабочего стола](/index.php/%D0%A1%D1%80%D0%B5%D0%B4%D0%B0_%D1%80%D0%B0%D0%B1%D0%BE%D1%87%D0%B5%D0%B3%D0%BE_%D1%81%D1%82%D0%BE%D0%BB%D0%B0 "Среда рабочего стола"). Он может быть вызван непосредственно:

```
$ mimeopen -d /path/to/file

```

Будет задан вопрос, какое приложение использовать при открытии `/path/to/file`:

```
Please choose a default application for files of type text/plain
       1) notepad  (wine-extension-txt)
       2) Leafpad  (leafpad)
       3) OpenOffice.org Writer  (writer)
       4) gVim  (gvim)
       5) Other...

```

Выбранное приложение будет обработчиком по умолчанию для данного типа файлов. Mimeopen устанавливается в `/usr/bin/perlbin/vendor/mimetype`.

## Аналоги

### замена xdg-open

<table class="wikitable">

<tbody>

<tr>

<th>Название пакета</th>

<th>Метод</th>

<th>Основан на</th>

<th>Файл конфигурации</th>

</tr>

<tr>

<td>[busking-git](https://aur.archlinux.org/packages/busking-git/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/busking-git)]</sup></td>

<td>Регулярные выражения</td>

<td>[perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo)</td>

<td>пользовательский</td>

</tr>

<tr>

<td>[linopen](https://aur.archlinux.org/packages/linopen/)<sup><small>AUR</small></sup></td>

<td>[file](https://www.archlinux.org/packages/?name=file)</td>

<td>пользовательский</td>

</tr>

<tr>

<td>[mimeo](https://aur.archlinux.org/packages/mimeo/)<sup><small>AUR</small></sup></td>

<td>MIME-типы, регулярные выражения</td>

<td>[file](https://www.archlinux.org/packages/?name=file)</td>

<td>`mimeapps.list`, `defaults.list`; пользовательский необязателен</td>

</tr>

<tr>

<td>[mimi-git](https://aur.archlinux.org/packages/mimi-git/)<sup><small>AUR</small></sup></td>

<td>[file](https://www.archlinux.org/packages/?name=file)</td>

<td>пользовательский</td>

</tr>

<tr>

<td>[ease](https://aur.archlinux.org/packages/ease/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ease)]</sup></td>

<td>MIME-типы, названия файлов, регулярные выражения</td>

<td>база данных SQLite или [file](https://www.archlinux.org/packages/?name=file), [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) и др.</td>

<td>база данных SQLite или `mimeapps.list`</td>

</tr>

<tr>

<td>[ayr](https://aur.archlinux.org/packages/ayr/)<sup><small>AUR</small></sup></td>

<td>MIME-типы, названия файлов, регулярные выражения</td>

<td>[file](https://www.archlinux.org/packages/?name=file) либо [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) и др.</td>

<td>`mimeapps.list`, `defaults.list`</td>

</tr>

<tr>

<td>[sx-open](https://aur.archlinux.org/packages/sx-open/)<sup><small>AUR</small></sup><sup>[[ссылка недействительна](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): сохранено в [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/sx-open)]</sup></td>

<td>Регулярные выражения</td>

<td>[file](https://www.archlinux.org/packages/?name=file), регулярные выражения bash</td>

<td>пользовательский</td>

</tr>

</tbody>

</table>

**Обратите внимание:** Вышеуказанные аналоги могут символически ссылаться на каталог `xdg-open` до `/usr/bin` в [переменной $PATH](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5_%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F "Переменные окружения") (например, `ln -s /usr/bin/sx-open /usr/local/bin/xdg-open`). Однако, некоторые приложения могут быть жестко привязаны к `/usr/bin/xdg-open`. В таком случае установите пакет [xdg-utils-no-open](https://aur.archlinux.org/packages/xdg-utils-no-open/)<sup><small>AUR</small></sup> и скопируйте с заменой в `/usr/bin/xdg-open`

### mailcap

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**Эта статья или раздел нуждается в расширении**

**Причина:** При использовании [run-mailcap](https://aur.archlinux.org/packages/run-mailcap/)<sup><small>AUR</small></sup> совместно с _xdg-open_ может возникнуть зацикливание, в результате которого обе утилиты будут вызывать друг друга. [[1]](http://cgit.freedesktop.org/xdg/xdg-utils/tree/scripts/xdg-open.in#n266) It should then clearly not be combined with the below file to prevent endless loops (обсуждение: [Talk:Xdg-open (Русский)#](https://wiki.archlinux.org/index.php/Talk:Xdg-open_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

Формат файла_.mailcap_ используется программами работы с электронной почтой, такими как [mutt](https://www.archlinux.org/packages/?name=mutt) и [sylpheed](https://www.archlinux.org/packages/?name=sylpheed). Чтобы они использовали возможности _xdg-open_, отредактируйте `~/.mailcap`:

 `~/.mailcap` 

```
*/*; xdg-open "%s

```

### mimetype

_mimetype_ в пакете [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo) может показать некоторую mimetype-связанную информацию о файле.

Например:

```
$ mimetype file.ext

```

выведет mime-тип этого файла,

```
$ mimetype -d file.extension

```

выведет описание этого mime-типа.

Если утилите _xdg-open_ не удается обнаружить [среду рабочего стола](/index.php/Desktop_environment_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Desktop environment (Русский)"), то она будет выполнять комманду `file -i`, использующую для определения mime-типа только содержимое файла, в результате чего некоторые типы файлов определяются неправильно. При наличии _mimetype_ _xdg-open_ будет использовать его для лучшего результата определения, т.к. _mimetype_ использует информацию [общей базе данных](http://standards.freedesktop.org/shared-mime-info-spec/shared-mime-info-spec-0.18.html) mime info.

### Переменные окружения

Некоторые переменные окружения, такие как `BROWSER`, `DE` и `DESKTOP_SESSION`, изменят поведение по умолчанию _xdg-open_. См. [Переменные окружения](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5_%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F "Переменные окружения") для получения дополнительной информации.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Xdg-open_(Русский)&oldid=415693](https://wiki.archlinux.org/index.php?title=Xdg-open_(Русский)&oldid=415693)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Desktop environments (Русский)](/index.php/Category:Desktop_environments_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Desktop environments (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")