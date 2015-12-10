# Go

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Go](http://golang.org/) is a statically-typed language with syntax loosely derived from that of C, adding garbage collected memory management, type safety, some dynamic-typing capabilities, additional built-in types such as variable-length arrays and key-value maps, and a large standard library.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Test your installation](#Test_your_installation)
    *   [1.2 $GOPATH](#.24GOPATH)
    *   [1.3 Enable cross compilation for other platforms](#Enable_cross_compilation_for_other_platforms)
*   [2 See also](#See_also)

## Installation

There are two Go compilers nowadays, and they can be [installed](/index.php/Install "Install") from [official repositories](/index.php/Official_repositories "Official repositories"):

*   **gc**: common name for official set of compilers 8g(x86), 6g(amd64), 5g(arm), that can be [installed](/index.php/Install "Install") with [go](https://www.archlinux.org/packages/?name=go)
    *   fast compilation
*   **gccgo**: frontend for _gcc_, part of its compiler collection, can be [installed](/index.php/Install "Install") with [gcc-go](https://www.archlinux.org/packages/?name=gcc-go)
    *   goroutines becomes full flow
    *   small size of the binary
    *   better optimization

### Test your installation

Check that Go is installed correctly by building a simple program, as follows:

 `hello.go` 

```
package main

import "fmt"

func main() {
    fmt.Println("Hello, Arch!")
}

```

Then run it with the go tool:

 `$ go run hello.go` 

```
Hello, Arch!

```

Compilation with standard _gc_ compiler (same as `go build -compiler=gc test.go`):

```
$ go build test.go

```

Compilation with _gccgo_ (same as `go build -compiler=gccgo test.go`):

```
$ gccgo test.go -o test

```

### $GOPATH

Go dependencies, when used for example in `import` statements, are searched for in the `$GOPATH` variable, and then - in `$GOROOT` (_go_ installation directory, `/usr/lib/go` by default). If you expect to use external dependencies, not only basic from `$GOROOT`, you must specify workspace area in your `~/.bash_profile` (or equivalent):

```
export GOPATH=~/go

```

**Tip:** You can see all Go variables by running `go env`

Create that workspace:

```
$ mkdir -p ~/go/{bin,src}

```

`src` directory is used to store sources of the project, and `bin` for executables.

Also you can add path to `bin` directory in `$PATH` [environment variable](/index.php/Environment_variable "Environment variable") to run installed programs (written on Go language) anywhere (like, for example, `ls`):

```
export PATH="$PATH:$GOPATH/bin"

```

Note that we also add the `bin` subdirectory to the `$PATH` so we can run any executables that be required.

Run `go help gopath` for more information.

### Enable cross compilation for other platforms

The official package only supports Linux amd64, 386 and arm architectures. To support cross compilation for Darwin, FreeBSD and MS Windows, run the commands below.

```
 $ cd /usr/lib/go/src; for os in darwin freebsd windows; do for arch in amd64 386; do sudo GOROOT_BOOTSTRAP=/usr/lib/go GOOS=$os GOARCH=$arch ./make.bash --no-clean; done; done

```

**Note:** These commands will need to be run following each Go package update.

For more information, see [FS#30287](https://bugs.archlinux.org/task/30287).

## See also

*   [Official web-site of Go Programming Language](http://golang.org/)
*   [Wikipedia article](https://en.wikipedia.org/wiki/Go_(programming_language) "wikipedia:Go (programming language)")
*   [Examples with small descriptions](https://gobyexample.com/)
*   [Interactive Go training tour](http://tour.golang.org)
*   [IDEs and Plugins for Go](https://github.com/golang/go/wiki/IDEsAndTextEditorPlugins)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Go&oldid=410726](https://wiki.archlinux.org/index.php?title=Go&oldid=410726)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Programming languages](/index.php/Category:Programming_languages "Category:Programming languages")