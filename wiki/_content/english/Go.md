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

There are two Go compilers nowadays, and they can be [installed](/index.php/Install "Install") from [official repositories](/index.php/Official_repositories "Official repositories"):

*   **go**: interface to the set of compilation tools that can be [installed](/index.php/Install "Install") with [go](https://www.archlinux.org/packages/?name=go)
    *   fast compilation
    *   official tools (go get, go doc, etc.)
    *   cross-compilation
*   **gccgo**: frontend for *gcc*, part of its compiler collection, can be [installed](/index.php/Install "Install") with [gcc-go](https://www.archlinux.org/packages/?name=gcc-go)
    *   goroutines becomes full flow
    *   small size of the binary (dynamic linking)

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

Compilation with standard *gc* compiler (same as `go build -compiler=gc hello.go`):

```
$ go build hello.go

```

Compilation with *gccgo* (same as `go build -compiler=gccgo hello.go`):

```
$ gccgo hello.go -o hello

```

### $GOPATH

Go dependencies, when used for example in `import` statements, are searched for in the `$GOPATH` variable, and then - in `$GOROOT` (*go* installation directory, `/usr/lib/go` by default). If you expect to use external dependencies, not only basic from `$GOROOT`, you must specify workspace area in your `~/.bash_profile` (or equivalent):

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

The official package only supports Linux amd64, 386 and arm architectures. To support cross compilation for Darwin, FreeBSD and MS Windows, follow along as below.

You can not build `/usr/lib/go/src` of itself, ie if you set `$GOROOT_BOOTSTRAP` to `/usr/lib/go` you will get a warning like this.

```
 $ cd /usr/lib/go/src
 $ GOROOT_BOOTSTRAP=/usr/lib/go GOOS=darwin GOARCH=amd64 ./make.bash --no-clean 
 ##### Building Go bootstrap tool.
 cmd/dist
 ERROR: $GOROOT_BOOTSTRAP must not be set to $GOROOT
 Set $GOROOT_BOOTSTRAP to a working Go tree >= Go 1.4.

```

To get around this, grab a source copy of Go from [https://golang.org/](https://golang.org/).

**Note:** Commands below will assume you extracted your download of Go to `~/downloads/go`.

Build your downloaded Go with your system GO.

```
 $ cd ~/downloads/go/src
 $ GOROOT_BOOTSTRAP=/usr/lib/go GOOS=linux GOARCH=amd64 ./make.bash --no-clean

```

You can now build your system Go using the downloaded Go as bootstrap with this command.

```
 $ cd /usr/lib/go/src; for os in darwin freebsd windows; do for arch in amd64 386; do sudo GOROOT_BOOTSTRAP="$HOME/downloads/go" GOOS=$os GOARCH=$arch ./make.bash --no-clean; done; done

```

**Note:** These commands will need to be run following each Go package update.

For more information, see [FS#30287](https://bugs.archlinux.org/task/30287).

## Troubleshooting

### Jetbrains Go Plugin

If you are using a Jetbrains IDE and the Go plugin cannot find your Go SDK path, you might be using an incompatible package. Remove the `gcc-go` package and replace it with `go`. If your GOPATH is set, the IDE should now be able to find your Go SDK at `/usr/lib/go`.

## See also

*   [Official web-site of Go Programming Language](http://golang.org/)
*   [Wikipedia article](https://en.wikipedia.org/wiki/Go_(programming_language) "wikipedia:Go (programming language)")
*   [Examples with small descriptions](https://gobyexample.com/)
*   [Interactive Go training tour](http://tour.golang.org)
*   [IDEs and Plugins for Go](https://github.com/golang/go/wiki/IDEsAndTextEditorPlugins)
*   [Go 1.5 Bootstrap Plan](https://docs.google.com/document/d/1OaatvGhEAq7VseQ9kkavxKNAfepWy2yhPUBs96FGV28/edit)