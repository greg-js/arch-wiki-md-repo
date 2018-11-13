**Estado de la traducción**
Este artículo es una traducción de [Mono](/index.php/Mono "Mono"), revisada por última vez el **2018-11-08**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Mono&diff=0&oldid=552396) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

De [Wikipedia](https://en.wikipedia.org/wiki/es:Proyecto_Mono "wikipedia:es:Proyecto Mono"):

	Mono es el nombre de un proyecto de código abierto iniciado por Ximian respaldado por Microsoft y actualmente impulsado por Novell (tras la adquisición de Ximian) para crear un grupo de herramientas libres, basadas en GNU/Linux y compatibles con .NET según lo especificado por el ECMA.

## Contents

*   [1 Instalación](#Instalación)
*   [2 Ejecutando aplicaciones Mono](#Ejecutando_aplicaciones_Mono)
*   [3 Probar Mono](#Probar_Mono)
*   [4 Desarrollo](#Desarrollo)
*   [5 Solución de problemas](#Solución_de_problemas)
    *   [5.1 Recibo un error "cannot execute "ruta/a/tu/binario" file name has not been set."](#Recibo_un_error_"cannot_execute_"ruta/a/tu/binario"_file_name_has_not_been_set.")
    *   [5.2 Recibo un error cuando intento ejecutar los binarios de Mono directamente: "cannot execute binary file"](#Recibo_un_error_cuando_intento_ejecutar_los_binarios_de_Mono_directamente:_"cannot_execute_binary_file")
    *   [5.3 Recibo un error de handshake TLS (o un error basado en un sistema de certificados similar)](#Recibo_un_error_de_handshake_TLS_(o_un_error_basado_en_un_sistema_de_certificados_similar))
    *   [5.4 Recibo un error al compilar fsharp: "System.TypeInitializationException: The type initializer for 'System.Console' threw an exception"](#Recibo_un_error_al_compilar_fsharp:_"System.TypeInitializationException:_The_type_initializer_for_'System.Console'_threw_an_exception")
*   [6 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [mono](https://www.archlinux.org/packages/?name=mono).

Si necesita soporte de VisualBasic.Net, debe [instalar](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el intérprete de VisualBasic.Net con el paquete [mono-basic](https://aur.archlinux.org/packages/mono-basic/).

MonoDevelop recurre a [xterm](/index.php/Xterm "Xterm") cuando ejecuta su proyecto. Podría instalarlo cuando esté escribiendo una aplicación de consola.

## Ejecutando aplicaciones Mono

Puede ejecutar los binarios de Mono recurriendo a `mono` manualmente:

```
$ mono programsname.exe

```

También puede ejecutar los binarios de Mono directamente, al igual que los binarios nativos:

```
$ chmod 755 exefile.exe
$ ./exefile.exe

```

## Probar Mono

Cree un archivo nuevo:

 `test.cs` 
```
using System;

public class Test {
 public static void Main(string[] args) {
  Console.WriteLine("Hello World!");
 }
}

```

Después ejecute:

```
$ mcs test.cs
$ mono test.exe
Hello world!

```

## Desarrollo

Empezar a desarrollar en Mono/C# es muy fácil. Solo [instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el [MonoDevelop IDE](http://monodevelop.com/) con el paquete [monodevelop-stable](https://aur.archlinux.org/packages/monodevelop-stable/) o [monodevelop-git](https://aur.archlinux.org/packages/monodevelop-git/). Alternativamente, puede instalar el IDE [rider](https://aur.archlinux.org/packages/rider/).

Si desea el navegador de documentación API y algunas herramientas de testeo y desarrollo, instale [mono-tools](https://www.archlinux.org/packages/?name=mono-tools).

## Solución de problemas

### Recibo un error "cannot execute "ruta/a/tu/binario" file name has not been set."

Puede instalar [xterm](/index.php/Xterm "Xterm"), ya que MonoDevelop inicia [xterm](/index.php/Xterm "Xterm") cuando presiona ejecutar. Esto podría ser una posible dependencia.

### Recibo un error cuando intento ejecutar los binarios de Mono directamente: "cannot execute binary file"

El controlador [binfmt_misc](https://en.wikipedia.org/wiki/Binfmt_misc "wikipedia:Binfmt misc") para Mono aún no se ha configurado, como se explica en detalle en la [página web del proyecto Mono](http://www.mono-project.com/Guide:Running_Mono_Applications#Registering_.exe_as_non-native_binaries_.28Linux_only.29).

Para solucionar esto, [reinicie](/index.php/Daemon_(Espa%C3%B1ol) "Daemon (Español)") el servicio `systemd-binfmt`.

### Recibo un error de handshake TLS (o un error basado en un sistema de certificados similar)

Intente `mozroots --import --ask-remove`, el cual debería actualizar los certificados de mono. `mozroots` es parte del paquete mono.

### Recibo un error al compilar fsharp: "System.TypeInitializationException: The type initializer for 'System.Console' threw an exception"

Este es un error reciente en mcs que se utiliza para compilar fsharp. Una solución es usar `export TERM=xterm`, como se detalla aquí [[1]](https://github.com/mono/mono/issues/6752)

## Véase también

*   [Página web oficial de Mono](http://www.mono-project.com)
*   [Manual de Mono](http://mono-project.com/Monkeyguide)
*   [La referencia API de Mono](http://go-mono.org/docs)
*   [ECMA-334: Especificación del lenguaje C#](http://www.ecma-international.org/publications/standards/ECMA-334.HTM)
*   [ECMA-335: Common Language Infrastructure (CLI)](http://www.ecma-international.org/publications/standards/ECMA-335.HTM)
*   [Instrucciones para ejecutar aplicaciones Mono](http://www.mono-project.com/Guide:Running_Mono_Applications)