**Estado de la traducción**
Este artículo es una traducción de [GEDA](/index.php/GEDA "GEDA"), revisada por última vez el **2018-11-02**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=GEDA&diff=0&oldid=552608) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

El proyecto gEDA ha producido y continúa trabajando en una suite de herramientas GPL y un kit de herramientas de automatización de diseño electrónico. Estas herramientas se utilizan para el diseño de circuitos eléctricos, captura esquemática, simulación, creación de prototipos y producción. Actualmente, el proyecto gEDA ofrece un conjunto maduro de aplicaciones de software gratuitas para el diseño electrónico, que incluyen captura esquemática, gestión de atributos, generación de listas de materiales (BOM), creación netlist a más de 20 formatos de netlist, simulación analógica y digital y diseño de placa de circuito impreso (PCB).

El proyecto gEDA se inició debido a la falta de herramientas EDA gratuitas para los sistemas POSIX con el principal propósito de avanzar en el estado del hardware libre o el hardware de código abierto. La suite se está desarrollando principalmente en la plataforma GNU/Linux con un cierto esfuerzo de desarrollo para asegurarse de que las herramientas se ejecuten también en otras plataformas.

(Fuente: [página web de gEDA](http://www.gpleda.org/))

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Primera PCB](#Primera_PCB)
    *   [2.1 Crear símbolo esquemático](#Crear_s.C3.ADmbolo_esquem.C3.A1tico)
        *   [2.1.1 Ruta de búsqueda esquemática](#Ruta_de_b.C3.BAsqueda_esquem.C3.A1tica)
    *   [2.2 Crear esquema](#Crear_esquema)
    *   [2.3 Crear y enrutar el PCB](#Crear_y_enrutar_el_PCB)

## Instalación

El paquete [geda-gaf](https://www.archlinux.org/packages/?name=geda-gaf) le instalará el editor de esquemas y el editor de atributos, el cual está disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). También podría ser necesario instalar [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) y [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) para obtener un correcto escalado de las fuentes.

La instalación de [pcb](https://www.archlinux.org/packages/?name=pcb) le dará el editor de PCB, disponible en [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

## Primera PCB

### Crear símbolo esquemático

Puede crear nuevos símbolos a medida que esté creando esquemas. Abra un archivo vacío con

```
$ gschem mysymbol.sym

```

y agregue pines con `ap` y atributos con `aa` . Consulte la [wiki de geda](http://wiki.geda-project.org/geda:master_attributes_list) para obtener más información. Una vez que haya terminado, no olvide traducir su símbolo a cero absoluto con `et` . Si no lo hace, su símbolo probablemente estará fuera de su ventana gráfica una vez que lo coloque en su esquema.

Guarde el símbolo con `fs` y verifíquelo con

```
$ gsymcheck -vv mysymbol.sym

```

#### Ruta de búsqueda esquemática

No olvide colocar su símbolo dentro de la ruta de búsqueda de gschem. También puede ser útil extender esta ruta a una carpeta en su propio proyecto creando un archivo llamado ` gafrc ` en la carpeta del proyecto con el siguiente contenido
```
(component-library "./symbols")

```

y luego copie todos los símbolos requeridos por el proyecto a una subcarpeta llamada "symbols".

### Crear esquema

Ejecute el editor de esquemas:

```
$ gschem

```

Véase también:

[FAQ](http://wiki.geda-project.org/geda:faq-gschem)

### Crear y enrutar el PCB

Una vez que haya alcanzado un punto en su esquema en el que desee comenzar a enrutar el PCB (puede hacerlo de forma iterativa), es el momento de crear un proyecto gsch2pcb. Agregue las siguientes líneas a un archivo recién creado, llamado `firstpcb.prj` :

```
schematics firstpcb.sch
empty-footprint nofootprint
output-name firstpcb

```

Este proyecto leerá de firstpcb.sch, ignorará cualquier parte que tenga una huella llamada 'nofootprint' y los archivos de salida comenzarán a ser:

*   El PCB: firstpcb.pcb
*   El netlist: firstpcb.net
*   Comandos del nombre de pin: firstpcb.cmd
*   ...

Si optó por un directorio de símbolos local, debe incluirlo aquí. También es probable que desee un directorio local de huella, de paso. Así que agregue estas líneas al archivo prj:

```
elements-dir footprints
elements-dir symbols

```

Ahora ejecute gsch2pcb con este archivo de proyecto:

```
$ gsch2pcb -f firstpcb.prj

```

gsch2pcb le dirá qué hacer a continuación o si hubo algún error.