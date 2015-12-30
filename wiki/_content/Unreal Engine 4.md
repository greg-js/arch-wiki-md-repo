# Unreal Engine 4

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Unreal Engine 4 es la ultima versión de el motor de videojuegos de PC y consolas creado por la compañía Epic Games

El contenido de este articulo fue originalmente escrito en [Esta Página](https://wiki.unrealengine.com/Building_On_Linux) y adaptado específicamente para ArchLinux

* * *

## Contents

*   [1 Requisitos Mínimos](#Requisitos_M.C3.ADnimos)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 Desde AUR](#Desde_AUR)
    *   [2.2 Compilar desde el Código Fuente](#Compilar_desde_el_C.C3.B3digo_Fuente)
        *   [2.2.1 Satisfacer Dependencias](#Satisfacer_Dependencias)
        *   [2.2.2 Obtener el código fuente](#Obtener_el_c.C3.B3digo_fuente)
        *   [2.2.3 Preparar para la compilacion](#Preparar_para_la_compilacion)
        *   [2.2.4 Compilar el código fuente](#Compilar_el_c.C3.B3digo_fuente)
    *   [2.3 Ejecutar Unreal Engine 4](#Ejecutar_Unreal_Engine_4)
    *   [2.4 Problemas Comunes](#Problemas_Comunes)
        *   [2.4.1 Problemas de Compilacion](#Problemas_de_Compilacion)

## Requisitos Mínimos

PC o Mac

CPU: Intel o AMD 2.5 GHz 4 nucleos o superior **64 Bits**

GPU: NVIDIA GeForce GTX 470 o AMD Radeon 6870 HD series

RAM: 8 GB

* * *

## Instalación

### Desde AUR

Para instalar desde AUR solo introduzca este comando en una terminal.

```
$ yaourt -S UE4

```

Este comando instalara únicamente los **Binarios**.

### Compilar desde el Código Fuente

* * *

#### Satisfacer Dependencias

```
$ sudo pacman -S clang35 mono dos2unix cmake

```

En algunas ocasiones sera necesario re compilar clang o obtener un paquete pre compilado de clang que no use id.gold Si usó el comando anterior puede hacer lo siguiente

```
$ mkdir ~/bin/ && cd ~/bin/ && ln -s /bin/ld.bfd ./ld.gold

```

Después modifique el archivo .bashrc (generalmente oculto en /home) y agregue la linea siguiente:

```
export PATH=$HOME/bin:$PATH

```

A continuación cierre todas las terminales abiertas para aplicar los cambios

* * *

#### Obtener el código fuente

Primero necesita registrarse en la pagina de [Epic Games](https://www.unrealengine.com)y asociar su cuenta de GitHub a su cuenta de Epic Games

Después descargue el código fuente de Unreal Engine 4 usando el siguiente comando

```
$ git clone -b release [https://github.com/EpicGames/UnrealEngine.git](https://github.com/EpicGames/UnrealEngine.git)

```

* * *

#### Preparar para la compilacion

```
$ cd UnrealEngine
$ ./Setup.sh
$ ./GenerateProjectFiles.sh

```

Estos scripts descargaran ciertas dependencias de un tamaño aproximado de 3.5 GB

* * *

#### Compilar el código fuente

Para compilar el código fuente ejecute los siguientes comandos:

```
$ make UE4Editor UE4Game UnrealPak CrashReportClient ShaderCompileWorker UnrealLightmass
$ make -j1 ShaderCompileWorker

```

Este proceso tomara bastante tiempo, dependerá de la capacidad de procesamiento de su Ordenador

* * *

### Ejecutar Unreal Engine 4

```
$cd Engine/Binaries/Linux
$./UE4Editor

```

### Problemas Comunes

* * *

#### Problemas de Compilacion

Si surgen problemas al momento de compilar el editor puede intentar compilarlo usando el Perfil "Debug"

```
$ make UE4Editor-Linux-Debug

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Unreal_Engine_4&oldid=413804](https://wiki.archlinux.org/index.php?title=Unreal_Engine_4&oldid=413804)"