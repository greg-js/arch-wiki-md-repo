**gtkD** - это объектно-ориентированная приязка библиотеки [GTK+](http://www.gtk.org/) к языку D, выпускается под лицензией [LGPL](/index.php/Licenses#LGPL "Licenses").

## Contents

*   [1 Необходимые средства разработки](#.D0.9D.D0.B5.D0.BE.D0.B1.D1.85.D0.BE.D0.B4.D0.B8.D0.BC.D1.8B.D0.B5_.D1.81.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.B0_.D1.80.D0.B0.D0.B7.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.BA.D0.B8)
*   [2 Проверка работоспособности](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.BE.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
*   [3 Программирование с использованием gtkD](#.D0.9F.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_gtkD)
*   [4 Примечание](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D0.B5)
*   [5 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

# Необходимые средства разработки

Нам понадобится компилятор _dmd_ от Digital Mars, а также _D Shared Software System (DSSS)_, чтобы установить _dlua_ и собрать нашу программу.

Установим компилятор _dmd_:

```
# wget [https://aur.archlinux.org/packages/dmd/dmd/PKGBUILD](https://aur.archlinux.org/packages/dmd/dmd/PKGBUILD)
# makepkg -i

```

А также систему сборки _DSSS_:

```
# wget [https://aur.archlinux.org/packages/dsss/dsss/PKGBUILD](https://aur.archlinux.org/packages/dsss/dsss/PKGBUILD)
# makepkg -i

```

Теперь установим _gtkD_:

```
# dsss net install gtkd

```

Если всё прошло успешно, то значит библиотека _gtkD_ установлена корректно.

# Проверка работоспособности

В комплекте с gtkD идёт программа _GtkDTests_. Запустите её:

```
$ GtkDTests

```

Если через некоторое время появится окно с заголовком _GtkD tests_, а внутри будут разделённые вкладками демонстрации элементов управления _GTK+ 2.0_, то это значит, что всё в порядке.

# Программирование с использованием gtkD

Библиотека gtkD очень облегчает процесс разработки на языке D. Это доказывается на примере программы _Hello World_.

Код напишем на D с использованием _gtkD_, а собирать будем при помощи программы _compd_, которая идёт в комплекте с пакетом _dool-svn_.

```
// Hello World на gtkD
module test.gtkd;

// импортируем привязки gtkD
import gtk.MainWindow;
import gtk.Label;
import gtk.GtkD;

import std.stdio;

/**
 * Класс HelloGtkD, наследник MainWindow из gtkD.
 * Реализует диалоговое окно с надписью "Hello World".
 */
class HelloGtkD: MainWindow
{
    this()
    {
        super("GtkD");
        setBorderWidth(40);
        add(new Label("Hello World"));
        showAll();
    }
}

/**
 * Функция main(), инициализирует GTK, создаёт и отображает наше
 * диалоговое окно.
 */
void main(char [][]args)
{
    Gtk.init(args);
    new HelloGtkD();
    Gtk.main();
}

```

Код написан, теперь нужно его скомпилировать. Для этого создадим в папке с файлом, содержащим наш код (пусть файл зовётся _hello.d_), ещё один файл, _build.compd_, в котором будут указаны правила сборки для программы _compd_:

```
# исходная папка
.
# результирующий исполняемый файл
-o hello-gtkd
# компилировать промежуточный объектный файл
-c
# местонахождение заголовочных файлов библиотеки gtkD
-I /usr/include/d
# библиотека phobos компилятора dmd
-l phobos
# библиотека gtkD
-l gtkd
# библиотека линковщика dl
-l dl

```

Теперь соберём нашу программу _Hello World_:

```
$ compd

```

При правильно настроенных компонентах (_dmd_, _dool_, _gtkD_, etc), получим примерно следующий вывод:

```
arg[0]=compd
arg[1]=.
arg[2]=-o
arg[3]=hello-gtkd
arg[4]=-c
arg[5]=-I
arg[6]=/usr/include/d
arg[7]=-l
arg[8]=phobos
arg[9]=-l
arg[10]=gtkd
arg[11]=-l
arg[12]=dl

ExecutorSync.execute=
dmd ./hello.d   -odobj  -op  -I/usr/include/d   -c  -I/home/eveel/dmd/src/phobos

ExecutorSync.execute=
gcc  obj/./hello.o -o hello-gtkd -m32     -lphobos -lgtkd -ldl   -m32 -lphobos -lpthread -lm

```

Итак, теперь если запустить файл _hello-gtkd_, то появится диалоговое окно с надписью _Hello World_.

# Примечание

Данная статья написана пользователем [eveel](/index.php/User:Eveel "User:Eveel").

# Ссылки

*   [Вебсайт GTK+](http://www.gtk.org/)
*   [Язык программирования D](http://www.digitalmars.com/d/index.html)
*   [Проект gtkD](http://www.dsource.org/projects/dui)
*   [Проект dool](http://svn.dsource.org/projects/dool/)