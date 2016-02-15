**dlua** - это привязка языка программирования [lua](http://www.lua.org/) к языку D, выпускается под лицензией [MIT License](/index.php/Licenses#MIT "Licenses").

## Contents

*   [1 Необходимые средства разработки](#.D0.9D.D0.B5.D0.BE.D0.B1.D1.85.D0.BE.D0.B4.D0.B8.D0.BC.D1.8B.D0.B5_.D1.81.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.B0_.D1.80.D0.B0.D0.B7.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.BA.D0.B8)
*   [2 Hello, World!](#Hello.2C_World.21)
*   [3 Примечание](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D0.B5)
*   [4 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

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

Теперь установим _dlua_:

```
# dsss net install luad

```

Если всё прошло успешно, то значит библиотека _dlua_ установлена корректно.

# Hello, World!

Lua - простой, лёгкий и удобный скриптовый язык. Главным его достоинством является то, что его очень просто внедрить в приложение и воспользоваться его преимуществами в полной мере.

А сейчас напишем небольшое приложение, которое будет использовать _lua_: будет выполняться скрипт, в котором будет использоваться функция, объявленная в нашей программе.

Но для сборки нашего примера нам понадобится утилита _rebuild_, которая является частью системы _D Shared Software System (DSSS)_.

Всё готово, теперь мы можем написать код.

Итак, создадим файл _hello.d_ следующего содержания (это основная часть нашей программы):

```
// проверка dlua
module test.dlua;

// используем привязку dlua
import dlua.all;

// нам нужна функция writefln() из стандартной библиотеки
import std.stdio;

/**
 * Функция testfunction() будет вызываться виртуальной
 * машиной языка Lua. Эта функция выводит фразу "Hello from D!"
 * в STDOUT.
 */
int testfunction(lua_State* L)
{
    writefln("Hello from D!");
    return 0;
}

/**
 * Функция main() инициализирует виртуальную машину Lua,
 * загружает стандартную библиотеку языка Lua, а также
 * регистрирует нашу функцию testfunction().
 */
void main()
{
    // создаём экземпляр виртуальной машины Lua
    lua_State* L = luaL_newstate();
    // загружаем стандартную библиотеку Lua
    luaL_openlibs(L);
    // регистрируем нашу функцию testfunction()
    lua_register(L, "testfunction", &testfunction);
    // запускаем скрипт hello.lua в нашей виртуальной машине
    luaL_dofile(L, "hello.lua");
    // освобождаем нашу виртуальную машину
    lua_close(L);
}

```

То, что делает код, ясно по интуитивно понятным комментариям.

Теперь напишем скрипт _hello.lua_, который будет выполняться нашей программой:

```
io.write("Hello from Lua!\n")
testfunction()
io.write("Hello from Lua again!\n")

```

Мы используем функцию _io.write()_ из стандартной библиотеки, а также функцию _testfunction()_, предоставленную нашей программой на языке D.

Теперь скомпилируем наш пример, здесь нам пригодится утилита _rebuild_ из пакета _dsss_:

```
$ rebuild hello.d -L-llua -L-ldl
gcc ./test.dlua.o ./dlua.all.o ./dlua.lua.o ./dlua.luaconf.o ./dlua.lauxlib.o ./dlua.lualib.o ./nmd_gcstats.o -o hello -m32 -Xlinker --start-group -lphobos -llua -ldl -Xlinker -L/usr/lib -Xlinker -L/usr/lib -lphobos -lpthread -lm

```

Всё! Осталось только порадоваться работе программы:

```
$ ./hello     
Hello from Lua!
Hello from D!
Hello from Lua again!

```

# Примечание

Данная статья написана пользователем [eveel](/index.php/User:Eveel "User:Eveel").

# Ссылки

*   [Вебсайт Lua](http://www.lua.org/)
*   [Язык программирования D](http://www.digitalmars.com/d/index.html)
*   [Проект dlua](http://code.google.com/p/dlua/)
*   [Проект D Shared Software System (DSSS)](http://dsource.org/projects/dsss)