[Go](http://golang.org/) es un lenguaje de tipo estático con sintaxis derivada de C, agregando gestión de memoria, recolector de basura, seguridad de tipos, algunas capacidades de escritura dinámica, tipos incorporados adicionales tales como matrices de longitud variable y mapas de valores clave y una gran biblioteca estándar.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Probar instalación](#Probar_instalaci.C3.B3n)
    *   [1.2 $GOPATH](#.24GOPATH)
    *   [1.3 Habilitar la compilación cruzada para otras plataformas](#Habilitar_la_compilaci.C3.B3n_cruzada_para_otras_plataformas)
*   [2 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [2.1 Complemento para Jetbrains](#Complemento_para_Jetbrains)
*   [3 Ver también](#Ver_tambi.C3.A9n)

## Instalación

Actualmente, hay dos compiladores para Go, y se pueden instalar desde los repositorios oficiales:

*   **go**: Interfaz con el conjunto de herramientas de compilación que pueden instalarse con el paquete [go](https://www.archlinux.org/packages/?name=go)
    *   Compilación rápida
    *   Herramientas oficiales (go get, go doc, etc.)
    *   Compilación cruzada
*   **gccgo**: frontend para *gcc*, parte de su colección compiladora, puede instalarse con [gcc-go](https://www.archlinux.org/packages/?name=gcc-go)
    *   Goroutines se convierte en pleno flujo
    *   Tamaño pequeño del binario (enlazamiento dinámico)

### Probar instalación

Para verificar si Go está instalado correctamente, se puede escribir un simple programa a modo de prueba, como el siguiente:

 `hello.go` 
```
package main

import "fmt"

func main() {
    fmt.Println("Hola, Arch!")
}

```

Luego, ejecutar con `go`:

 `$ go run hello.go` 
```
Hola, Arch!

```

Compilación con el compilador estándar *gc* (mismo que `go build -compiler=gc hello.go`):

```
$ go build hello.go

```

Compilación con *gccgo* (mismo que `go build -compiler=gccgo hello.go`):

```
$ gccgo hello.go -o hello

```

### $GOPATH

Las dependencias de Go, cuando se usan, por ej. en las declaraciones `import`, se buscan en la variable `$GOPATH`, y luego - en `$GOROOT` (en el directorio de instalación, `/usr/lib/go` por defecto). Si se desea usar dependencias externas, no únicamente las que están en `$GOROOT`, se debe especificar el área de trabajo en `~/.bash_profile` (o su equivalente):

```
export GOPATH=~/go

```

**Sugerencia:** Se pueden ver todas las variable de Go ejecutando `go env`

Crear el espacio de trabajo:

```
$ mkdir -p ~/go/{bin,src}

```

`src` el directorio se usa para guardar los archivos de código fuente, y `bin` para los ejecutarlos.

También se puede agregar la ruta a el directorio `bin` en `$PATH` para ejecutar programas instalados (escritos en el lenguaje de programación Go) donde sea (como, por ejemplo, `ls`):

```
export PATH="$PATH:$GOPATH/bin"

```

Notese que también se añadió el subdirectorio `bin` a la variable `$PATH` así se podrá ejecutar cualquier programa instalado requerido.

Ejecute `go help gopath` para más información.

### Habilitar la compilación cruzada para otras plataformas

El paquete oficial sólo admite arquitecturas de Linux amd64, 386 y arm. Para admitir la compilación cruzada de Darwin, FreeBSD y MS Windows, siga lo siguiente.

No se puede construir `/usr/lib/go/src` por sí sólo, por ej. si se configura `$GOROOT_BOOTSTRAP` a `/usr/lib/go` se obtendrá una advertencia como esta:

```
 $ cd /usr/lib/go/src
 $ GOROOT_BOOTSTRAP=/usr/lib/go GOOS=darwin GOARCH=amd64 ./make.bash --no-clean 
 ##### Building Go bootstrap tool.
 cmd/dist
 ERROR: $GOROOT_BOOTSTRAP must not be set to $GOROOT
 Set $GOROOT_BOOTSTRAP to a working Go tree >= Go 1.4.

```

Para evitar eso, consiga una copia de Go desde [https://golang.org/](https://golang.org/).

**Nota:** Los comandos siguientes asumirán que extrajo la descarga de Go a `~/downloads/go`.

Construye tu versión descargada de Go.

```
 $ cd ~/downloads/go/src
 $ GOROOT_BOOTSTRAP=/usr/lib/go GOOS=linux GOARCH=amd64 ./make.bash --no-clean

```

Ahora puede construir su sistema. Utilice el comando de arranque.

```
 $ cd /usr/lib/go/src; for os in darwin freebsd windows; do for arch in amd64 386; do sudo GOROOT_BOOTSTRAP="$HOME/downloads/go" GOOS=$os GOARCH=$arch ./make.bash --no-clean; done; done

```

**Nota:** Estos comandos tendrán que ejecutarse después de cada actualización del paquete Go.

Para más información, ver [FS#30287](https://bugs.archlinux.org/task/30287).

## Solución de problemas

### Complemento para Jetbrains

Si estás usando el entorno de desarrollo de Jetbrains y el complemento de Go no puede encontrar la ruta hacia el SDK, podrías estar usando un paquete incompatible. Remueve el paquete `gcc-go` y reemplazalo con `go`. Si la ruta GOPATH esta configurada, el IDE debería ser capaz de buscar el SDK de Go en `/usr/lib/go`.

## Ver también

*   [Sitio web oficial del lenguaje de programación Go](http://golang.org/)
*   [Artículo de wikipedia](https://en.wikipedia.org/wiki/Go_(lenguaje_de_programaci%C3%B3n) "wikipedia:Go (lenguaje de programación)")
*   [Ejemplos con pequeñas descripciones](https://gobyexample.com/)
*   [tour interactivo de entrenamiento Go](http://tour.golang.org)
*   [Entornos de desarrollo integrado y complementos para Go](https://github.com/golang/go/wiki/IDEsAndTextEditorPlugins)
*   [Go 1.5 Bootstrap Plan](https://docs.google.com/document/d/1OaatvGhEAq7VseQ9kkavxKNAfepWy2yhPUBs96FGV28/edit)