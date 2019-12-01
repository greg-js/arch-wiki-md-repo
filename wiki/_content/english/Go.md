Related articles

*   [Go package guidelines](/index.php/Go_package_guidelines "Go package guidelines")

[Go](http://golang.org/) is a statically-typed language with syntax loosely derived from that of [C](/index.php/C "C"), adding garbage collected memory management, type safety, some dynamic-typing capabilities, additional built-in types such as variable-length arrays and key-value maps, and a large standard library.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Test your installation](#Test_your_installation)
    *   [1.2 $GOPATH](#$GOPATH)
    *   [1.3 Cross compiling to other platforms](#Cross_compiling_to_other_platforms)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Jetbrains Go Plugin](#Jetbrains_Go_Plugin)
*   [3 See also](#See_also)

## Installation

The standard Go compiler is `go`, which can be installed from the [go](https://www.archlinux.org/packages/?name=go) package. The `go` command also include various tooling such as `go get`, `go doc`, etc. An alternative is [gcc-go](https://www.archlinux.org/packages/?name=gcc-go), which is a Go frontend for the [GNU Compiler Collection](/index.php/GNU_Compiler_Collection "GNU Compiler Collection") (GCC). In some cases `gccgo` may do better optimisations. When in doubt: use `go`.

An additional package that most Go developers will want to install is [go-tools](https://www.archlinux.org/packages/?name=go-tools). This will provide various commonly used tools which will make working with Go easier, such as `goimports`, `guru`, `gorename`, etc.

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

### Cross compiling to other platforms

The `go` command can natively cross-compile to [a number of platforms](https://golang.org/doc/install/source#introduction).

If [cgo](https://golang.org/cmd/cgo/) is not required for your build, then simply specify the target OS and architecture as env vars to `go build`:

```
$ GOOS=linux GOARCH=arm64 go build .

```

See [the official documentation](https://golang.org/doc/install/source#environment) for the valid combinations of `$GOOS` and `$GOARCH`.

On the other hand, if [cgo](https://golang.org/cmd/cgo/) is required for your build, you have to provide the path to your `C/C++` cross-compilers, via the `$CC/$CXX` env vars.

Say you want to cross-compile for `$GOOS=linux` and `$GOARCH=arm64`.

You need first to install the [aarch64-linux-gnu-gcc](https://www.archlinux.org/packages/?name=aarch64-linux-gnu-gcc) cross-compiler.

Here is a sample program that requires `cgo`, so that we can test the cross-compilation process:

```
$ cat > hello.go <<EOF
package main

// #include <stdio.h>
// void hello() {  puts("Hello, Arch!"); }
import "C"

func main() { C.hello() }
EOF

```

Then, you can cross-compile it like this:

```
$ GOOS=linux GOARCH=arm64 CGO_ENABLED=1 CC=/usr/bin/aarch64-linux-gnu-gcc go build hello.go

```

You can check that the architecture of the generated binary is actually `aarch64`:

```
$ file hello
hello: ELF 64-bit LSB executable, ARM aarch64, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux-aarch64.so.1, BuildID[sha1]=b1d92ae8840a019f36cc2aee4606b6ae4a581bf1, for GNU/Linux 3.7.0, not stripped

```

If you copy `hello` to a suitable host, you can test-run it:

```
[alarm@rpi3 ~]$ uname -a
Linux alarm 5.3.8-1-ARCH #1 SMP Tue Oct 29 19:31:23 MDT 2019 aarch64 GNU/Linux
[alarm@arpi3 ~]$ ./hello
Hello, Arch!

```

## Troubleshooting

### Jetbrains Go Plugin

If you are using a Jetbrains IDE and the Go plugin cannot find your Go SDK path, you might be using an incompatible package. Remove the `gcc-go` package and replace it with `go`. If your `$GOPATH` is set, the IDE should now be able to find your Go SDK at `/usr/lib/go`.

## See also

*   [Official website](http://golang.org/)
*   [Wikipedia article](https://en.wikipedia.org/wiki/Go_(programming_language) "wikipedia:Go (programming language)")
*   [Examples with small descriptions](https://gobyexample.com/)
*   [Interactive Go training tour](http://tour.golang.org)
*   [Go cross compilation](https://rakyll.org/cross-compilation/)
*   [IDEs and Plugins for Go](https://github.com/golang/go/wiki/IDEsAndTextEditorPlugins)