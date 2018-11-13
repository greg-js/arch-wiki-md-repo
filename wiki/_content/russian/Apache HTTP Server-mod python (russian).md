## Contents

*   [1 Введение](#Введение)
*   [2 Установка](#Установка)
    *   [2.1 Модуль Apache: Mod_python](#Модуль_Apache:_Mod_python)
        *   [2.1.1 Установка пакета](#Установка_пакета)
        *   [2.1.2 Настройка Apache](#Настройка_Apache)
        *   [2.1.3 Проверка Mod_python](#Проверка_Mod_python)
*   [3 См. также](#См._также)

## Введение

Mod_python - это модуль [Apache](/index.php/Apache "Apache"), который встраивает интерпретатор [Python](/index.php/Python_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Python (Русский)") на сервер. Используя mod_python можно написать веб-приложения на Python во много раз быстрее, чем в традиционных CGI и, кроме того, иметь доступ к дополнительным функциям, таким как способность сохранять соединения с базой данных и другие данные и иметь доступ к внутреннему Apache. Более подробное описание функций mod_python доступно в данной [статье](http://www.onlamp.com/pub/a/python/2003/10/02/mod_python.html) O'Reilly.

## Установка

### Модуль Apache: Mod_python

Этот документ описывает, как настроить и протестировать Apache модуль Mod_python на Arch Linux.

#### Установка пакета

1.  Pacman-Sy mod_python

#### Настройка Apache

```
   * Добавьте эту строку в `/etc/httpd/conf/httpd.conf`:
LoadModule python_module modules/mod_python.so

```

```
   * Перезапустите Apache
# httpd -k restart

```

```
   * Убедитесь, что Apache запускается без ошибок

```

#### Проверка Mod_python

```
   * Добавьте этот блок в `/etc/httpd/conf/httpd.conf`:

```

<Directory /home/www/html>

```
   AddHandler mod_python .py
   PythonHandler mod_python.publisher 
   PythonDebug On 
</Directory>

```

```
   * Создать файл `/home/www/html/` с именем `mptest.py` и добавить в него:

```

```
from mod_python import apache
def handler(req):
    req.content_type = 'text/plain'
    req.send_http_header()
    req.write("Hello World!")
    return apache.OK

```

```
   * Перезапустите Apache
# sudo apachectl restart

```

```
   * Убедитесь, что Apache запускается без ошибок

```

```
   * Перейдите на `[http://yoursite.com/mphandler.py/handler](http://yoursite.com/mphandler.py/handler)`, и убедитесь, что на сайте написано:
Hello World!

```

В конфигурации написанной выше, вы можете также указать любой ваш адрес, заканчивающийся на .pу в тестовом каталоге. Например, Вы можете указать адрес `/foobar.py` и он будет управляться из mptest.py.

## См. также

*   [Gentoo Wiki Mod_Python](http://gentoo-wiki.com/Apache_Modules_mod_python)
*   [mod_python Tutorial](http://webpython.codepoint.net/mod_python)
*   [http://www.modpython.org/](http://www.modpython.org/)
*   [mod_python manual](http://www.modpython.org/live/current/doc-html/)