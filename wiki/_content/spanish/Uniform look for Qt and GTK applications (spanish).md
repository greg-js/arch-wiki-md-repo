Artículos relacionados

*   [GTK+](/index.php/GTK%2B_(Espa%C3%B1ol) "GTK+ (Español)")
*   [Qt](/index.php/Qt "Qt")

Los programas basados en [Qt](https://en.wikipedia.org/wiki/Qt_(toolkit) y [GTK+](/index.php/GTK%2B_(Espa%C3%B1ol) "GTK+ (Español)") utilizan diferentes conjuntos de "widgets" para conformar sus interfaces gráficas de usuario. Cada uno presenta entre otras cosas, diferentes temas, estilos y juegos de íconos por defecto, así que su "aspecto y tacto" difieren significativamente. Este artículo le ayudará a conseguir que tanto sus aplicaciones Qt como las GTK+ sean parecidas para lograr una experiencia de escritorio más uniforme e "integrada".

*"Qt (pronunciado "cute" en inglés) es un marco de trabajo para desarrollo de aplicaciones multiplataforma, ampliamente usado para el desarrollo de programas con interfaz gráfica (en cuyo caso se le conoce como un conjunto de "widgets"), aunque también es utilizado para desarrollar programas no gráficos tales como herramientas de consola y servidores."*

*   **Tema** - Colección de un estilo, un tema de íconos y un tema de colores.
*   **Estilo** - Disposición gráfica; aspecto.
*   **Tema de íconos** - Conjunto de íconos globales.
*   **Tema de color** - Conjunto de colores globales que se utilizan en conjunción con el estilo.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Estilos](#Estilos)
    *   [1.1 QtCurve](#QtCurve)
    *   [1.2 Otros](#Otros)
*   [2 Motores de tema](#Motores_de_tema)
    *   [2.1 Motor GTK-Qt](#Motor_GTK-Qt)
    *   [2.2 MetaTheme](#MetaTheme)
*   [3 Otros trucos](#Otros_trucos)
    *   [3.1 Diálogos de archivo en KDE para las aplicaciones GTK2](#Diálogos_de_archivo_en_KDE_para_las_aplicaciones_GTK2)
*   [4 Resolución de problemas](#Resolución_de_problemas)
    *   [4.1 ¿Cómo establezco los estilos para cada sistema?](#¿Cómo_establezco_los_estilos_para_cada_sistema?)
        *   [4.1.1 Estilos KDE3 y Qt3](#Estilos_KDE3_y_Qt3)
        *   [4.1.2 Estilos Qt4](#Estilos_Qt4)
        *   [4.1.3 Estilos GTK2](#Estilos_GTK2)
        *   [4.1.4 Estilos GTK1](#Estilos_GTK1)
    *   [4.2 Temas que no funcionan con aplicaciones GTK](#Temas_que_no_funcionan_con_aplicaciones_GTK)

# Estilos

Están disponibles conjuntos de "widgets" con el propósito de integración, con implementaciones escritas tanto para Qt como para GTK+, en todas sus versiones principales. Con éstas, puede tener un aspecto único para todas sus aplicaciones independientemente del marco de trabajo en que hayan sido escritas.

## QtCurve

Está disponible para *qt4* (kde4), *qt3* (kde3), *gtk2*, y *gtk1* en el repositorio **[community]**, este estilo, que es altamente configurable, es el más popular de todos. Tiene muchos controles para las diferentes opciones, abarcando desde la apariencia de los botones hasta la forma de las barras de desplazamiento. Puede instalarlos todos.

```
pacman -S qtcurve-gtk1 qtcurve-gtk2 qtcurve-kde3 qtcurve-kde4

```

Para cambiar al estilo de la versión 3 de Qt en KDE versión 3:

```
Centro de control (kcontrol) --> Apariencia y temas --> Estilo --> Estilo de Widgets = QtCurve

```

Para cambiar al estilo de la versión 2 de GTK+ en KDE versión 3:

```
pacman -S gtk-chtheme

```

Ejecútelo y será capaz de elegir su opción. También puede cambiar los tipos. Tenga en cuenta por favor que cualquier aplicación abierta debe ser reiniciada para poder ver los cambios. Alternativamente, puede hacer lo mismo con un motor, como se verá más adelante.

## Otros

Conjuntos similares de estilo so aquellos que se parecen enrete sí - escritos tanto para Qt como para GTK+ - aunque no necesariamente por los mismos desarrolladores. Puede que tenga que hacer algunos ajustes menores para hacer que se parezcan al máximo. A continuación tiene una lista de ellos:

*   klearlooks (qt3); clearlooks (gtk2)

# Motores de tema

Se puede considerar un motor de tema como en una fina capa API que traduce temas (salvo los íconos) entre un o mas sistemas. Estos motores añaden algún código extra en el proceso y es indiscutible que este tipo de solución no es tan elegante y óptima como la de usar estilos nativos.

## Motor GTK-Qt

Este es para utilizar aplicaciones GTK+ en el entorno KDE, lo que básicamente significa que es para KDE. Aplica toda la configuración Qt (estilos, tipos, pero no los íconos) a las aplicaciones GTK+ y utiliza directamente los plugins de estilo. Haga el favor de tener en cuenta que con algunos estilos Qt se producen algunos problemas de renderizado.

```
pacman -S gtk-qt-engine

```

Puede acceder a él desde:

```
Centro de control (kcontrol) --> Apariencia y temas --> Estilos GTK y tipos

```

Si quisiera quitarlo por completo incluyendo cualquier recuerdo de él, tendría que borrar los siguientes archivos:

*   ~/.gtkrc2.0-kde
*   ~/.kde/env/gtk-qt-engine.rc.sh
*   ~/gtk-qt-engine.rc

## MetaTheme

El motor metatheme esta diseñado como una fina capa entre los sistemas de "widgets", creando un API unificado mediante el cual cada motor de tema puede dibujar. El resultado es que cada aplicación utiliza el mismo ćodigo para el dibujo, haciendo que la apariencia sea la misma entre las diferentes aplicaciones. Este motor esta capacitado para trabajar con los sistemas de GTK2, Qt/KDE, y Java.

```
pacman -S metatheme

```

Para instalarlo..

```
metatheme-install

```

Para la configuración...

```
mt-config

```

Para desinstalarlo...

```
metatheme-install -u

```

# Otros trucos

## Diálogos de archivo en KDE para las aplicaciones GTK2

KGtk es un guión de tipo "wrapper" que utiliza LD_PRELOAD para forzar a las aplicaciones GTK" a utilizar los diálogos de archivo de KDE. Si utiliza KDE y prefiere sus diálogos de archivo frente a los de GTK, puede instalar entonces kgtk desde AUR. Una vez instalado puede ejecuta las aplicaciones GTK2 con kgtk-wrapper de 2 maneras (utilizando gimp en los ejemplos).

Llamando directamente a kgtk-wrapper y ytilizando el binario GTK2 como argumento

```
/usr/local/bin/kgtk-wrapper gimp

```

O bien

Creando un enlace simbólico de kgtk utilizando el nombre del binario GTK2\. Puede entonces ejecutar /usr/local/bin/gimp cuando quiera ejecutar gimp con diálogos KDE.

```
ln -s /usr/local/bin/kgtk-wrapper /usr/local/bin/gimp
/usr/local/bin/gimp

```

# Resolución de problemas

## ¿Cómo establezco los estilos para cada sistema?

Puede utilizar los siguientes métodos para cambiar el tema en cada entorno.

#### Estilos KDE3 y Qt3

*   Centro de control (kcontrol) --> Apariencia y temas --> Estilo --> Estilo de widgets
*   kde-config --style [nombre del estilo]
*   /opt/qt/bin/qtconfig

#### Estilos Qt4

*   /usr/bin/qtconfig

#### Estilos GTK2

*   gtk-chtheme
*   gtk2_prefs
*   switch2 (paquete gtk-theme-switch2)

#### Estilos GTK1

*   switch (paquete gtk-theme-switch)

## Temas que no funcionan con aplicaciones GTK

Si el estilo o el motor de temas que estableció no está apareciendo en sus aplicaciones GTK puede ser que por alguna razón no se estén cargando sus archivos de configuración. Puede saber dónde espera su sistema encontrar estos archivos haciendo lo siguiente...

```
export | grep gtk

```

Normalmente los archivos esperados deberían ser ~/.gtkrc para GTK1, ~/.gtkrc2.0 o ~/.gtkrc2.0-kde para GTK2

Versiones más recientes gtk-qt-engine utilizan ~/.gtkrc2.0-kde y establecen la variable export en ~/.kde/env/gtk-qt-engine.rc.sh Si quitó recientemente gtk-qt-engine y está intentando establecer un tema GTK debe quitar entonces ~/.kde/env/gtk-qt-engine.rc.sh y reiniciar. Haciendo esto se asegurará de que GTK busque su configuración en el fichero estándar ~/.gtkrc2.0 en vez de en ~/.gtkrc2.0-kde