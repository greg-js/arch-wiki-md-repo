[Go](http://golang.org/) — язык программирования, главными особенностями которого является быстрая компиляции, сборка мусора и многопоточность.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Проверка установки](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [1.2 $GOPATH](#.24GOPATH)
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

Также с [go](https://www.archlinux.org/packages/?name=go) можно установить дополнительные инструменты разработчика [go-tools](https://www.archlinux.org/packages/?name=go-tools).

### Проверка установки

Для проверки работоспособности создайте простенькую программу:

 `test.go` 
```
package main

func main() {
    println("Привет, Арч!")
}

```

Запустите программу при помощи Go:

 `$ go run test.go` 
```
Привет, Арч!

```

Компиляция стандартным компилятором *gc* (аналог `go build -compiler=gc test.go`):

```
$ go build test.go

```

Компиляция с помощью *gccgo* (аналог `go build -compiler=gccgo test.go`):

```
$ gccgo test.go -o test

```

Компиляция с помощью *gccgo* и [*gold-линковщика*](/index.php/Gold_linker_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Gold linker (Русский)"):

```
$ gccgo test.go -fuse-ld=gold -o test

```

### $GOPATH

В языке Go поиск программ и их зависимостей (например, `import *пакет*`) сначала выполняется в каталогах, прописанных в переменную `$GOPATH`, а затем - в переменной `$GOROOT` (путь установки *go*, по умолчанию `/usr/lib/go`). Поэтому, чтобы использовать внешние зависимости, а не только базовые, что находятся в `$GOROOT`, нужно определить область рабочего пространства в вашем `~/.bash_profile` (или его эквиваленте):

```
$ export GOPATH=~/go

```

**Совет:** Для просмотра переменных Go выполните команду `go env`

Создадим также само рабочее пространство:

```
$ mkdir -p ~/go/{bin,src}

```

Каталог `src` предназначен для хранения исходников проектов, а `bin` - для размещения исполняемых файлов, которые получаются, например, при установке наших проектов (`go install пакет`) или получении и установки пакета из других источников (`go get github.com/*путь/к/пакету*`).

Для удобства можно также добавить в переменную окружения `$PATH` путь к каталогу `bin` нашего рабочего пространства, что позволит запускать установленные программы языка Go так же, как, к примеру, и стандартную для *linux* команду `ls`:

```
$ export PATH="$PATH:$GOPATH/bin"

```

Для получения дополнительной информации смотрите `go help gopath`.

## Динамические библиотеки

Компилятор Go собирает все зависимости программы в один бинарник, но начиная с версии 1.5 появилась возможность подключать библиотеки динамически. Для начала нужно скомпилировать стандартную библиотеку языка Go как динамическую:

```
$ go install -buildmode=shared std

```

теперь можно скомпилировать программу test.go с поддержкой динамических библиотек:

```
$ go build -linkshared -o test.go

```

чтобы программа могла запускатся и на других системах с ней нужно поставить также и стандартную динамическую библиотеку языка Go `libstd.so`, взять её можно по адресу `$(go env GOROOT)/pkg/$(go env GOOS)_$(go env GOARCH)_dynlink/libstd.so` Помимо наличия самой библиотеки нужно ещё установить переменную `LD_LIBRARY_PATH` которая укажет программе откуда брать динамческую библиотеку(на примере linux):

```
export LD_LIBRARY_PATH=$PWD

```

## Кросс-компиляция

**$GOARCH**

```
386               : x386
amd64             : AMD64
amd64p32          : AMD64 с 32-указателями
arm               : ARM
arm64             : ARM64
mips64            : MIPS64
mips64le          : MIPS64-LE

```

**$GOOS**

```
linux             : Linux
darwin            : iOS, MacOS X
windows           : Windows
freebsd           : FreeBSD
netbsd            : NetBSD
openbsd           : OpenBSD
dragonfly         : DragonFly BSD
plan9             : Plan 9
nacl              : Native Client
android           : Android

```

пример компиляции:

```
$ GOOS=windows GOARCH=amd64 go build -o test

```

## Оптимизация

Компилятор go по умолчанию компилирует пакет с отладочной информацией что существенно увеличивает размер исполняемого файла, чтобы этого избежать необходимо добавить флаг:

```
$ go build -ldflags '-s' test.go

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