**gtkD** - это объектно-ориентированная приязка библиотеки [GTK+](http://www.gtk.org/) к языку D, выпускается под лицензией [LGPL](/index.php/Licenses#LGPL "Licenses").

## Contents

*   [1 Необходимые средства разработки](#.D0.9D.D0.B5.D0.BE.D0.B1.D1.85.D0.BE.D0.B4.D0.B8.D0.BC.D1.8B.D0.B5_.D1.81.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.B0_.D1.80.D0.B0.D0.B7.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.BA.D0.B8)
*   [2 Проверка работоспособности](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.BE.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
*   [3 Программирование с использованием gtkD](#.D0.9F.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_gtkD)
*   [4 Примечание](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D0.B5)
*   [5 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

# Необходимые средства разработки

Нам понадобится компилятор *dmd* от Digital Mars, а также *D Shared Software System (DSSS)*, чтобы установить *dlua* и собрать нашу программу.

Установим компилятор *dmd*:

```
# wget [https://aur.archlinux.org/packages/dmd/dmd/PKGBUILD](https://aur.archlinux.org/packages/dmd/dmd/PKGBUILD)
# makepkg -i

```

А также систему сборки *DSSS*:

```
# wget [https://aur.archlinux.org/packages/dsss/dsss/PKGBUILD](https://aur.archlinux.org/packages/dsss/dsss/PKGBUILD)
# makepkg -i

```

Теперь установим *gtkD*:

```
# dsss net install gtkd

```

Если всё прошло успешно, то значит библиотека *gtkD* установлена корректно.

# Проверка работоспособности

В комплекте с gtkD идёт программа *GtkDTests*. Запустите её:

```
$ GtkDTests

```

Если через некоторое время появится окно с заголовком *GtkD tests*, а внутри будут разделённые вкладками демонстрации элементов управления *GTK+ 2.0*, то это значит, что всё в порядке.

# Программирование с использованием gtkD

Библиотека gtkD очень облегчает процесс разработки на языке D. Это доказывается на примере программы *Hello World*.

Код напишем на D с использованием *gtkD*, а собирать будем при помощи программы *compd*, которая идёт в комплекте с пакетом *dool-svn*.

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

Код написан, теперь нужно его скомпилировать. Для этого создадим в папке с файлом, содержащим наш код (пусть файл зовётся *hello.d*), ещё один файл, *build.compd*, в котором будут указаны правила сборки для программы *compd*:

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

Теперь соберём нашу программу *Hello World*:

```
$ compd

```

При правильно настроенных компонентах (*dmd*, *dool*, *gtkD*, etc), получим примерно следующий вывод:

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

Итак, теперь если запустить файл *hello-gtkd*, то появится диалоговое окно с надписью *Hello World*.

# Примечание

Данная статья написана пользователем [eveel](/index.php/User:Eveel "User:Eveel").

# Ссылки

*   [Вебсайт GTK+](http://www.gtk.org/)
*   [Язык программирования D](http://www.digitalmars.com/d/index.html)
*   [Проект gtkD](http://www.dsource.org/projects/dui)
*   [Проект dool](http://svn.dsource.org/projects/dool/)