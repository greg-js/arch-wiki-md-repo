[Opera](http://www.opera.com) es una suite de Internet muy completa, desarrollada por **Opera Software ASA**, una compañía IT Noruega. Es un software **propietario** con algunos componentes de código abierto. Está disponible tanto para GNU/Linux, OS X y Windows y está presente en 45 idiomas. También posee versiones para celulares y tablets. Su motor de renderizado se llama **Presto**, es de código cerrado y soporta los estándares Web. Existe una versión en desarrollo con las últimas características del navegador llamada [Opera Next](http://www.opera.com/browser/next)].

## Contents

*   [1 Características](#Caracter.C3.ADsticas)
    *   [1.1 ¿Porque debería usar Opera?](#.C2.BFPorque_deber.C3.ADa_usar_Opera.3F)
    *   [1.2 ¿Porque no debería usar Opera?](#.C2.BFPorque_no_deber.C3.ADa_usar_Opera.3F)
*   [2 Instalación](#Instalaci.C3.B3n)
*   [3 Plugins (conectores)](#Plugins_.28conectores.29)
    *   [3.1 Flash Player](#Flash_Player)
        *   [3.1.1 Mejorar el rendimiento de Flash](#Mejorar_el_rendimiento_de_Flash)
    *   [3.2 WebM](#WebM)
*   [4 Algunos ajustes del Editor de Opciones](#Algunos_ajustes_del_Editor_de_Opciones)
    *   [4.1 Desactivar plugins (conectores) para mejorar el rendimiento](#Desactivar_plugins_.28conectores.29_para_mejorar_el_rendimiento)
    *   [4.2 Quitar icono en la bandeja del sistema](#Quitar_icono_en_la_bandeja_del_sistema)
    *   [4.3 Desactivar funciones](#Desactivar_funciones)
        *   [4.3.1 Desactivar cliente de correo](#Desactivar_cliente_de_correo)
        *   [4.3.2 Desactivar cliente Bitorrent](#Desactivar_cliente_Bitorrent)
    *   [4.4 Desactivar selección de texto](#Desactivar_selecci.C3.B3n_de_texto)
*   [5 Interfaz](#Interfaz)
    *   [5.1 Corregir estilo de la barra de título en KDE](#Corregir_estilo_de_la_barra_de_t.C3.ADtulo_en_KDE)
    *   [5.2 Fuentes de Microsoft y Opera](#Fuentes_de_Microsoft_y_Opera)
*   [6 Desplazamiento (scroll)](#Desplazamiento_.28scroll.29)
    *   [6.1 Activar desplazamiento suave](#Activar_desplazamiento_suave)
    *   [6.2 Solucionar desplazamiento lento en tarjetas nVidia](#Solucionar_desplazamiento_lento_en_tarjetas_nVidia)
    *   [6.3 Desplazarse al arrastrar el ratón](#Desplazarse_al_arrastrar_el_rat.C3.B3n)

## Características

*   Opera Mail : Cliente de correo electrónico integrado.
*   Opera Turbo: Comprime las páginas Web en los servidores de Opera Software ASA antes de ser descargadas. Esto permite ahorrar ancho de banda, ideal para conexiones lentas.
*   Opera Link: Sincroniza en la nube los marcadores, historial, acceso rápido, motores de búsqueda, contraseñas, etc. Requiere una cuenta Opera.
*   Opera Unite: Permite compartir contenidos y servicios desde su equipo.
*   Speed Dial (Acceso rápido): Muestra miniaturas con acceso a sus Web favoritas. Puede personalizarse y permite añadir extensiones.
*   Navegación con gestos del ratón. Se pueden usar al mantener pulsado el botón derecho del ratón.
*   Cliente BitTorrent incorporado.
*   Notas.
*   Administrar motores de búsqueda para personalizar búsquedas con palabras clave.
*   Opera Dragonfly: Para el desarrollo de páginas Web.
*   Extensiones, para aumentar la funcionalidad del navegador.
*   Widgets: aplicaciones desarrolladas por usuarios que funcionan de forma independientemente al navegador.
*   Acoplar pestañas: Crear grupos de pestañas, arrastrando una sobre otra.
*   Vista previa en pestañas al pasar el cursor sobre ellas.
*   Protección anti-fraude.
*   Lector de noticias, con soporte a RSS y Atom.
*   Cliente de chat IRC y soporte ftp.
*   Identificador: Administra las contraseñas y permite iniciar sesión en Webs con múltiples usuarios.
*   Administrador de descargas.
*   Administrador de marcadores.
*   Guardar y administrar sesiones.
*   Bloqueo de contenido: Permite eliminar la publicidad e imágenes del sitio visitado.
*   Corrector ortográfico.
*   Editar opciones por sitio: guardar la configuración de las cookies, las ventanas emergentes, el comportamiento de java, la identificación del navegador, entre otras cosas.
*   Personalizar aspecto: cambiar el color de la interfaz y personalizar barras y botones.
*   Papelera de pestañas cerradas.
*   Panel lateral para acceder a las funciones del navegador.
*   Navegación privada por pestañas y ventanas.

### ¿Porque debería usar Opera?

*   Es rápido y liviano.
*   Cumple con los estándares.
*   Es muy personalizable.
*   Fuera de la caja provee navegación web con gestos del mouse y ad-blocking, cliente de mail, cliente bittorrent y cliente IRC ¡todo en uno! Entre otras cosas...
*   Tiene un toque profesional: **no software inflado, no escapes de memoria, no congelamientos, no desplomes**.

### ¿Porque no debería usar Opera?

*   No es [Libre](http://www.gnu.org/philosophy/free-sw.html). Es [software propietario](http://en.wikipedia.org/wiki/Proprietary_software).
*   Si usted es usuario de GNOME o de algun window manager basado en GTK+, requiere cargar bibliotecas adicionales, ya que Opera es una aplicación [Qt](http://en.wikipedia.org/wiki/Qt_(toolkit)). Sin embargo, a partir de la versión 10.50 esto cambia, puesto que se utilizaran las librerías del sistema X11 y dependiendo del tipo de librería gráfica, Opera intentará cargarla para su integración con el sistema del usuario (Gnome/GTK+ y KDE4/Qt4).
*   Algunas paginas web no se mostrarán de forma correcta porque esas paginas no siguen los estándares de la web (Opera se apega a los estándares).

## Instalación

El paquete [opera](https://www.archlinux.org/packages/?name=opera) se puede descargar desde los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)").

```
$ pacman -S opera

```

## Plugins (conectores)

Opera usa los plugins basados en Mozilla; vea [Browser Plugins (Español)](/index.php/Browser_Plugins_(Espa%C3%B1ol) "Browser Plugins (Español)") para más información. Los plugins que usa el navegador están especificados en: Menú Opera -> Configuración -> Opciones -> Avanzado -> Contenidos -> Opciones de conectores.

### Flash Player

Puede descargar el paquete [flashplugin](https://www.archlinux.org/packages/?name=flashplugin) desde los [repositorios oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)").

#### Mejorar el rendimiento de Flash

Para mejorar el rendimiento del plugin (Flash) en Opera, escriba este comando antes de iniciar el navegador o agréguelo a **~/.bashrc** (alternativamente a **/etc/profile**, para que el cambio afecte todos los usuarios):

```
OPERAPLUGINWRAPPER_PRIORITY=0
OPERA_KEEP_BLOCKED_PLUGIN=1

```

También, este comando le puede ayudar a solucionar problemas de Flash en algunos entornos gráficos:

```
GDK_NATIVE_WINDOWS=1

```

### WebM

Opera permite visualizar vídeos insertados en formato [WebM](http://www.webmproject.org), con HTML5\. Para que funcione, debe tener instalado [Gstreamer](/index.php/Gstreamer "Gstreamer") “**base**” y “**good**”.

```
$ pacman -S gstreamer0.10-base gstreamer0.10-plugins-base gstreamer0.10-good gstreamer0.10-plugins-good

```

Si ya los tiene instalados y no puede ver vídeos WebM, pruebe reinstalándolos.

## Algunos ajustes del Editor de Opciones

Pude modificar el comportamiento del navegador accediendo al [Editor de Opciones](http://www.opera.com/browser/tutorials/personalize/behavior) de Opera, escribiendo **opera:config** en la barra de direcciones.

### Desactivar plugins (conectores) para mejorar el rendimiento

La ejecución de elementos Flash en algunos los sitios puede disminuir la fluidez en la experiencia de navegación y aumentar el consumo de CPU. Opera ofrece la posibilidad de **deshabilitar los conectores externos, y activarlos haciendo click sobre ellos**. También se mostrará un **icono en la barra de direcciones para activar todos los plugins** de la página visitada. Lamentablemente, esta opción no posee “lista blanca” para añadir excepciones. Nótese que dicha característica viene por defecto al habilitar [Opera Turbo](http://www.opera.com/browser/turbo). Para desactivar los plugins, marque la casilla “Enable On Demand Plugin” en la sección UserPrefs en opera:config. Escriba en su barra de direcciones:

```
opera:config#UserPrefs|EnableOnDemandPlugin

```

Además, sitios como YouTube, ofrecen la posibilidad de [visualizar vídeos usando HTML5 (WebM)](http://www.youtube.com/html5), reemplazando Flash (característica en fase de prueba).

### Quitar icono en la bandeja del sistema

Para iniciar Opera sin el icono en la bandeja del sistema, desmarque la casilla “Show Tray Icon” en la sección UserPrefs en opera:config. Escriba en su barra de direcciones:

```
opera:config#UserPrefs | ShowTrayIcon

```

También puede hacerlo añadiendo la opción "-notrayicon" al lanzador de la aplicación:

```
$ opera -notrayicon

```

### Desactivar funciones

Una manera de aumentar el rendimiento de las aplicaciones es deshabilitar características o servicios no deseados.

#### Desactivar cliente de correo

Pude deshabilitar el cliente interno de correo, desmarcando la casilla “Show E-mail Client” en la sección UserPrefs en opera:config. Escriba en su barra de direcciones:

```
opera:config#UserPrefs|ShowE-mailClient

```

Otra forma de hacerlo es añadiendo la opción “-nomail” al lanzador de la aplicación.

```
$ opera -nomail

```

#### Desactivar cliente Bitorrent

Para ello, desmarque la casilla “Enable” en la sección BiTorrent en opera:config. Escriba en su barra de direcciones:

```
opera:config#BitTorrent|Enable

```

### Desactivar selección de texto

Es posible deshabilitar la selección de texto. Sin embargo, la selección de texto a través de Javascript seguirá funcionando. Escriba en su barra de direcciones y marque la casilla:

```
opera:config#System|DisableTextSelect

```

## Interfaz

*   Para hacer que los menús tengan aspecto integrado con Qt o tengan la apariencia que usted desee, instalar el tema preferido Qt4 y aplicarlo mediante el uso de **qtconfig**.
*   Puede añadir los botones que quiera en la interfaz de usuario, arrastrándolos desde: Menú Opera -> Apariencia -> Botones.

### Corregir estilo de la barra de título en KDE

En KDE, si la barra de título no tiene un estilo uniforme a la zona de pestañas, puedes conseguir una apariencia homogénea haciendo lo siguiente:

1.  Vaya a **Preferencias del sistema** -> **Apariencia del espacio de trabajo** -> **Configuración de decoración...** -> **Situaciones específicas de la ventana**.
2.  Haga click en **Añadir** y rellene con la siguiente información:
3.  En “Coincidir con la propiedad de la ventana”, elija “**Nombre de la clase de ventana**”. En “Expresión regular con la que coincidir”, escriba **Opera**. Marque la casilla “Estilo de fondo” y escoja: “**Gradiente radial**”.
4.  Acepte los cambios e inicie Opera para ver los resultados en la interfaz.

### Fuentes de Microsoft y Opera

Habiendo instalado el paquete [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) antes de usar Opera, el navegador usará por defecto las fuentes de Microsoft, posiblemente contrastando con las opciones especificadas por su configuración de fuentes (ya sea GNOME, KDE u otro). Para hacer que Opera use las fuentes predilectas de su sistema:

1.  Cierre Opera
2.  Elimine el paquete [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/).
3.  Mueva la carpeta de perfiles: **mv -i ~/.opera ~/.opera.bak** (Nota: Esta carpeta contiene sus marcadores y preferencias).
4.  Inicie Opera y verifique que la configuración de las fuentes está bien aplicada.
5.  Puede restaurar sus marcadores y configuración, copiando los ficheros de **~/.opera.bak** a **~/.opera**, exceptuando al fichero operaprefs.ini.
6.  Ahora pude reinstalar el paquete [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) si es que desea.

También, tome en cuenta que todas las fuentes son configurables a través de Herramientas -> Preferencias -> Avanzado -> Fuentes, y que fuentes especificadas por **qtconfig** toman precedencia sobre opciones de su entorno gráfico.

## Desplazamiento (scroll)

### Activar desplazamiento suave

1.  Vaya a: Menú Opera -> Configuración -> Opciones -> Avanzado -> Navegación.
2.  Marque: **Desplazamiento suave**.

### Solucionar desplazamiento lento en tarjetas nVidia

Intente, ejecutando el siguiente comando:

```
$ nvidia-settings -a InitialPixmapPlacement=2

```

### Desplazarse al arrastrar el ratón

También puede desplazarse por una página haciendo click y arrastrando el ratón por el sitio. Es muy útil si usted tiene una pantalla táctil. Para activar esta característica, marque la casilla “ Scrolls Pan” en la sección UserPrefs en opera:config. Escriba en su barra de direcciones:

```
opera:config#UserPrefs|ScrollIsPan

```