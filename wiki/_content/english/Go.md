[Go](http://golang.org/) is a statically-typed language with syntax loosely derived from that of C, adding garbage collected memory management, type safety, some dynamic-typing capabilities, additional built-in types such as variable-length arrays and key-value maps, and a large standard library.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Test your installation](#Test_your_installation)
    *   [1.2 $GOPATH](#.24GOPATH)
    *   [1.3 Enable cross compilation for other platforms](#Enable_cross_compilation_for_other_platforms)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Jetbrains Go Plugin](#Jetbrains_Go_Plugin)
*   [3 See also](#See_also)

## Installation

The standard Go compiler is `go`, which can be installed from the [go](https://www.archlinux.org/packages/?name=go) package. The `go` command also include various tooling such as `go get`, `go doc`, etc. An alternative is [gcc-go](https://www.archlinux.org/packages/?name=gcc-go), which is a Go frontend for the GNU Compiler Collection (GCC). In some cases `gccgo` may do better optimisations. When in doubt: use `go`.

An additional package that most Go developers will want to install is `go-tools`. This will provide various commonly used tools which will make working with Go easier, such as `goimports`, `guru`, `gorename`, etc.

### Test your installation

You can check that Go is installed correctly by building a simple program, as follows:

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

Compilation with standard *gc* compiler (same as `go build -compiler=gc hello.go`):

```
$ go build hello.go

```

Compilation with *gccgo* (same as `go build -compiler=gccgo hello.go`):

```
$ gccgo hello.go -o hello

```

### $GOPATH

Go expects the source code to live inside `$GOPATH`, which is set to `~/go` by default.

**Tip:** You can see all Go variables by running `go env`

Create that workspace:

```
$ mkdir -p ~/go/src

```

The `~/go/src` directory is used to store the sources of the packages. When compiling Go will also create `bin` for executables and `pkg` to cache individual packages. You'll probably want to add `~/go/bin` to the `$PATH` [environment variable](/index.php/Environment_variable "Environment variable") to run installed Go:

```
export PATH="$PATH:$HOME/go/bin"

```

Run `go help gopath` for more information.

**Tip:** `$GOPATH` works like `$PATH` and can contain multiple entries, this can be useful to split out packages downloaded with `go get` and your own source code; e.g. `GOPATH=$HOME/go:$HOME/mygo`

### Enable cross compilation for other platforms

The [go](https://www.archlinux.org/packages/?name=go) package only supports Linux *amd64*, *i386*, and *arm*. However you may compile go from source and enable cross-compiling for additional architectures. The following paragraph will outline the basics steps do enable cross-compilation support for *Darwin*, *FreeBSD* and *MS Windows*.

Download a copy of the source code from the [official website](https://golang.org/) and extracts its content to e.g. `~/downloads/go`.

Build your downloaded Go with your system Go:

```
 $ cd ~/downloads/go/src
 $ GOROOT_BOOTSTRAP=/usr/lib/go GOOS=linux GOARCH=amd64 ./make.bash --no-clean

```

You can now build your system Go using the downloaded Go as bootstrap with the following command:

```
 $ cd /usr/lib/go/src; for os in darwin freebsd windows; do for arch in amd64 386; do sudo GOROOT_BOOTSTRAP="$HOME/downloads/go" GOOS=$os GOARCH=$arch ./make.bash --no-clean; done; done

```

**Note:** These commands will need to be run following each Go package update.

For more information, see [FS#30287](https://bugs.archlinux.org/task/30287).

## Troubleshooting

### Jetbrains Go Plugin

If you are using a Jetbrains IDE and the Go plugin cannot find your Go SDK path, you might be using an incompatible package. Remove the `gcc-go` package and replace it with `go`. If your `$GOPATH` is set, the IDE should now be able to find your Go SDK at `/usr/lib/go`.

## See also

*   [Official web-site of Go Programming Language](http://golang.org/)
*   [Wikipedia article](https://en.wikipedia.org/wiki/Go_(programming_language) "wikipedia:Go (programming language)")
*   [Examples with small descriptions](https://gobyexample.com/)
*   [Interactive Go training tour](http://tour.golang.org)
*   [IDEs and Plugins for Go](https://github.com/golang/go/wiki/IDEsAndTextEditorPlugins)