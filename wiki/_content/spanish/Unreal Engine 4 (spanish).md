Unreal Engine 4 es la ultima versión de el motor de videojuegos de PC, consolas, dispositivos móviles y de realidad virtual creado por la compañía Epic Games

El contenido de este articulo fue originalmente escrito en [Esta Página](https://wiki.unrealengine.com/Building_On_Linux) y adaptado específicamente para ArchLinux

* * *

## Contents

*   [1 Requisitos Mínimos](#Requisitos_M.C3.ADnimos)
*   [2 Instalación](#Instalaci.C3.B3n)
    *   [2.1 Registro](#Registro)
    *   [2.2 Desde AUR](#Desde_AUR)
    *   [2.3 Compilar desde el Código Fuente](#Compilar_desde_el_C.C3.B3digo_Fuente)
        *   [2.3.1 Satisfacer Dependencias](#Satisfacer_Dependencias)
        *   [2.3.2 Obtener el código fuente](#Obtener_el_c.C3.B3digo_fuente)
        *   [2.3.3 Preparar para la compilacion](#Preparar_para_la_compilacion)
        *   [2.3.4 Compilar el código fuente](#Compilar_el_c.C3.B3digo_fuente)
    *   [2.4 Ejecutar Unreal Engine 4](#Ejecutar_Unreal_Engine_4)
    *   [2.5 Problemas Comunes](#Problemas_Comunes)
        *   [2.5.1 Errores de compilación](#Errores_de_compilaci.C3.B3n)
            *   [2.5.1.1 No se encuentra el archivo "ConvexHull2D.h"](#No_se_encuentra_el_archivo_.22ConvexHull2D.h.22)
        *   [2.5.2 Problemas de Compilación](#Problemas_de_Compilaci.C3.B3n)

## Requisitos Mínimos

PC o Mac

CPU: Intel o AMD 2.5 GHz 4 nucleos o superior **64 Bits**

GPU: NVIDIA GeForce GTX 470 o AMD Radeon 6870 HD series

RAM: 8 GB

## Instalación

### Registro

* * *

Primero necesita registrarse en la pagina de [Epic Games](https://www.unrealengine.com)y asociar su cuenta de GitHub a su cuenta de Epic Games

### Desde AUR

* * *

Unreal Engine 4 esta disponible en [AUR](/index.php/AUR "AUR") como [unreal-engine](https://aur.archlinux.org/packages/unreal-engine/) se necesitan aproximadamente 100 GB para la compilación, una vez compilado ocupara aproximadamente 22 GB y el código fuente descargado es de aproxidamamente 7 GB.

La compilación tardara varias horas.

Como el repositorio es privado usted puede [Establecer una clave SSH](https://help.github.com/articles/generating-an-ssh-key/) para que su cuenta de GitHub se use para descargar el código fuente

### Compilar desde el Código Fuente

* * *

#### Satisfacer Dependencias

Instale [clang35](https://aur.archlinux.org/packages/clang35/), [mono](https://www.archlinux.org/packages/?name=mono), [dos2unix](https://www.archlinux.org/packages/?name=dos2unix) and [cmake](https://www.archlinux.org/packages/?name=cmake).

En algunas ocasiones sera necesario re compilar clang o obtener un paquete pre compilado de clang que no use `ld.gold`:

Si instaló clang35 desde los repositorios haga lo siguiente:

```
$ mkdir ~/bin/ && cd ~/bin/ && ln -s /bin/ld.bfd ./ld.gold

```

Después modifique el archivo [.bashrc](/index.php/.bashrc ".bashrc") y agregue la linea siguiente:

```
export PATH=$HOME/bin:$PATH

```

A continuación cierre todas las terminales abiertas para aplicar los cambios

* * *

#### Obtener el código fuente

Descargue el código fuente de Unreal Engine 4 usando el siguiente comando

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

Para compilar el código fuente ejecute el siguiente comando:

```
$ make UE4Editor UE4Game UnrealPak CrashReportClient ShaderCompileWorker UnrealLightmass

```

Este proceso tomara bastante tiempo, dependerá de la capacidad de procesamiento de su Ordenador

* * *

### Ejecutar Unreal Engine 4

Para ejecutar Unreal ENgine 4 solo inserte los siguientes comandos en una terminal:

```
$cd Engine/Binaries/Linux

```

Si compiló con UE4Editor:

```
$./UE4Editor 

```

Si compilo con UE4Editor-Linux-Debug:

```
$./UE4Editor-Linux-Debug

```

### Problemas Comunes

* * *

#### Errores de compilación

##### No se encuentra el archivo "ConvexHull2D.h"

Modifique el archivo `SubUVAnimation.cpp` ubicado en `/Engine/Source/Runtime/Private/Particles` sobrescriba la linea:

```
#include "ConvexHull2D.h"

```

por esta:

```
#include "ConvexHull2d.h"

```

#### Problemas de Compilación

Si surgen problemas al momento de compilar el editor puede intentar compilarlo usando el Perfil "Debug"

```
$ make UE4Editor-Linux-Debug

```