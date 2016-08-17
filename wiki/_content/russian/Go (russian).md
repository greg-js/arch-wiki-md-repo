[Go](http://golang.org/) — язык программирования, главными особенностями которого является быстрая компиляции, сборка мусора и многопоточность.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Проверка установки](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [1.2 Настройка базового рабочего окружения](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B1.D0.B0.D0.B7.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
*   [2 Динамические библиотеки](#.D0.94.D0.B8.D0.BD.D0.B0.D0.BC.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.B1.D0.B8.D0.B1.D0.BB.D0.B8.D0.BE.D1.82.D0.B5.D0.BA.D0.B8)
*   [3 Кросс-компиляция](#.D0.9A.D1.80.D0.BE.D1.81.D1.81-.D0.BA.D0.BE.D0.BC.D0.BF.D0.B8.D0.BB.D1.8F.D1.86.D0.B8.D1.8F)
*   [4 Оптимизация](#.D0.9E.D0.BF.D1.82.D0.B8.D0.BC.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

На сегодняшний день существует два компилятора Go и оба доступны в [официальном репозитории](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"):

*   **gc**: общее название для официального набора компиляторов 8g(x86), 6g(amd64), 5g(arm), с версии 1.5 заменяются на один единственный go tool compile, [устанавливается](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") с пакетом [go](https://www.archlinux.org/packages/?name=go)

	+ быстрая компиляция

*   **gccgo**: фронтэнд для *gcc*, входит в состав его коллекции компиляторов, [устанавливается](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") с пакетом [gcc-go](https://www.archlinux.org/packages/?name=gcc-go)

	+ малый размер двоичного файла

	+ хорошая оптимизация

	‒ goroutines здесь полновесные потоки(проблема решается использованием [*gold-линковщика*](/index.php/Gold_linker_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Gold linker (Русский)") ([*info*](http://blog.golang.org/gccgo-in-gcc-471))

Также вместе с [go](https://www.archlinux.org/packages/?name=go) можно установить пакет [go-tools](https://www.archlinux.org/packages/?name=go-tools) который включает в себя документацию(*godoc*) и дополнительные инструменты разработчика.

### Проверка установки

Для проверки работоспособности создайте простенькую программу:

 `test.go` 
```
package main

func main() {
    println("Привет, Арч!")
}

```

Запуск программы с помощью интерпретатора:

 `$ go run test.go` 
```
Привет, Арч!

```

Компиляция стандартным компилятором *gc*:

```
$ go build test.go

```

аналогичен

```
$ go build -compiler=gc test.go

```

Компиляция с помощью *gccgo*:

```
$ gccgo test.go -o test

```

аналогичен

```
$ go build -compiler=gccgo test.go

```

Компиляция с помощью *gccgo* и [*gold-линковщика*](/index.php/Gold_linker_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Gold linker (Русский)"):

```
$ gccgo test.go -fuse-ld=gold -o test

```

### Настройка базового рабочего окружения

Для комфортной работы необходимо настроить как минимум две переменные: `$GOBIN` и `$GOPATH`.

В языке Go поиск программ и их зависимостей (например, `import "*пакет*"`), сначала выполняется в каталогах, прописанных в переменную `$GOPATH`, а затем - в переменной `$GOROOT` (путь установки *go*, по умолчанию `/usr/lib/go`). Поэтому, чтобы использовать внешние зависимости, а не только базовые из `$GOROOT`, нужно определить область рабочего пространства:

```
$ export GOPATH=$HOME/go

```

**Совет:** Для просмотра переменных Go используйте команду `go env`

теперь создадим само рабочее пространство:

```
$ mkdir -p $GOPATH/src

```

каталог `src` предназначен для хранения исходных текстов проектов.

Чтобы иметь возможность легко устанавливать пакеты с разных источников, таких например как [https://github.com](https://github.com) ( команда `go get github.com/*путь/к/пакету*`) или же непосредственно из своего проекта (команда `go install пакет`), необходимо задать переменную окружения `$GOBIN`:

```
$ export GOBIN=$GOPATH/bin
$ mkdir $GOBIN

```

`$GOBIN` можно также добавить в переменную окружения `$PATH` что позволит запускать установленные программы так же, как и стандартные системные утилиты:

```
$ export PATH="$PATH:$GOBIN"

```

**Совет:** Для удобства переменные `$GOBIN` и `$GOPATH` можно поместить в ваш `~/.bash_profile` (или его эквивалент)

**Совет:** Для получения дополнительной информации смотрите `go help gopath`

## Динамические библиотеки

Компилятор Go собирает все зависимости программы в один исполняемый файл, но начиная с версии Go 1.5 появилась возможность использовать динамические библиотеки.

Для подключения *всей стандартной библиотеки языка Go* нужно сначала скомпилировать её как динамическую:

```
# go install -buildmode=shared std

```

скомпилированная библиотека станет доступна по адресу: `$(go env GOROOT)/pkg/$(go env GOOS)_$(go env GOARCH)_dynlink/libstd.so`

**Примечание:** После каждого обновления версии языка Go данную библиотек также следует пересобрать

теперь можно скомпилировать программу test.go с поддержкой динамических библиотек:

```
$ go build -linkshared -o test

```

Если необходимо скомпилировать пакет как отдельную библиотеку, выполните:

```
$ go install -buildmode=shared -linkshared

```

после чего собранную библиотеку можно найти в папке `$GOPATH/pkg/$(go env GOOS)_$(go env GOARCH)_dynlink`.

Пользовательскую динамическую библиотеку в системе можно использовать если:

*   поместить её в каталог который используются системой для стандартного расположения динамических библиотек, в Арче это `/usr/lib/`
*   прописать путь до библиотеки в файле `/etc/ld.so.conf`, после чего обновить кеш командой `ldconfig`
*   использовать специальную переменную среды `$LD_LIBRARY_PATH`:

```
$ export LD_LIBRARY_PATH="/путь/к/каталогу/с/пользовательскими/динамическими/библиотеками"

```

если такая переменная уже существует, то:

```
$ export LD_LIBRARY_PATH="/путь/к/каталогу/с/пользовательскими/динамическими/библиотеками:${LD_LIBRARY_PATH}"

```

## Кросс-компиляция

**$GOOS и $GOARCH**

```
darwin     386
darwin     amd64
darwin     arm
darwin     arm64
dragonfly  amd64
freebsd    386
freebsd    amd64
freebsd    arm
linux      386
linux      amd64
linux      arm
linux      arm64
linux      ppc64
linux      ppc64le
linux      mips64
linux      mips64le
linux      s390x
netbsd     386
netbsd     amd64
netbsd     arm
openbsd    386
openbsd    amd64
openbsd    arm
plan9      386
plan9      amd64
plan9      arm
solaris    amd64
windows    386
windows    amd64

```

пример компиляции:

```
$ GOOS=windows GOARCH=amd64 go build -o test

```

## Оптимизация

Компилятор [go](https://www.archlinux.org/packages/?name=go) по умолчанию собирает пакет с дополнительной информацией которая влияет только на отладку и анализ полученного файла.

Чтобы этого избежать можно использовать ключ *-ldflags* с флагами отвечающими за отключения отладочной информации (*-w*) и сгенерированной таблицей символов (*-s*):

```
$ go build -ldflags '-w -s' test.go

```

## Смотрите также

*   [Официальный веб-сайт языка Go (en)](http://golang.org/)
*   [Интерактивный тур обучения Go (en)](http://tour.golang.org)
*   [Статья в Википедии](https://en.wikipedia.org/wiki/ru:Go "wikipedia:ru:Go")
*   [Русская группа в G+](https://groups.google.com/forum/#!forum/golang-ru)
*   [Хаб на Habrahabr про Go](http://habrahabr.ru/hub/go/)
*   [Веб-ресурс посвящённый Go](http://4gophers.com/)
*   [Примеры с кратким описанием](http://gobyexample.ru/)
*   [Awesome Go](http://awesome-go.com/)
*   [IDE и плагины для Go](https://github.com/golang/go/wiki/IDEsAndTextEditorPlugins)
*   [Руководство по созданию пакетов для AUR программ написанных на языке Go](/index.php/Go_package_guidelines "Go package guidelines")