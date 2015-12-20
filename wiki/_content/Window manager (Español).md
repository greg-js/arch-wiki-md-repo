# Window manager (Español)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Artículos relacionados

*   [Desktop environment (Español)](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)")
*   [Display manager (Español)](/index.php/Display_manager_(Espa%C3%B1ol) "Display manager (Español)")
*   [Xorg (Español)](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)")
*   [xinitrc (Español)](/index.php/Xinitrc_(Espa%C3%B1ol) "Xinitrc (Español)")
*   [Start X at login (Español)](/index.php/Start_X_at_login_(Espa%C3%B1ol) "Start X at login (Español)")

Un [gestor de ventanas](https://en.wikipedia.org/wiki/es:Gestor_de_ventanas "wikipedia:es:Gestor de ventanas") (siglas en inglés WM) es un componente del sistema que proporciona al usuario una interfaz gráfica del propio sistema (GUI). Muchos usuarios prefieren instalar un [entorno de escritorio](/index.php/Desktop_Environment_(Espa%C3%B1ol) "Desktop Environment (Español)") (siglas en inglés DE), que proporciona una interfaz gráfica de usuario completa, incluyendo iconos, ventanas, barras de herramientas, fondos de pantalla y widgets de escritorio.

## Contents

*   [1 X Window System](#X_Window_System)
*   [2 Window managers (gestores de ventanas)](#Window_managers_.28gestores_de_ventanas.29)
    *   [2.1 Tipos](#Tipos)
*   [3 Listado de gestores de ventanas](#Listado_de_gestores_de_ventanas)
    *   [3.1 Stacking WMs (Gestores de Ventanas Superpuestas)](#Stacking_WMs_.28Gestores_de_Ventanas_Superpuestas.29)
    *   [3.2 Tiling window managers (Gestores de Ventanas tipo Mosaico)](#Tiling_window_managers_.28Gestores_de_Ventanas_tipo_Mosaico.29)
    *   [3.3 Dynamic window managers (Gestores de Ventanas Dinámicas)](#Dynamic_window_managers_.28Gestores_de_Ventanas_Din.C3.A1micas.29)
*   [4 Enlaces externos](#Enlaces_externos)

## X Window System

El [sistema de ventanas X](https://en.wikipedia.org/wiki/es:X_Window_System "wikipedia:es:X Window System") proporciona la base para una interfaz gráfica de usuario. Antes de instalar un gestor de ventanas, es necesaria la instalación previa de un servidor X funcional. Consulte [Xorg](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") para obtener información detallada.

_X proporciona el marco básico, o primigenio, para la construcción de estos entornos GUI: permite dibujar y mover ventanas en la pantalla e interactuar con el ratón y el teclado. X no proporciona la interfaz de usuario —otros programas clientes individuales conocidos como gestores de ventanas proporcionan dicha interfaz—. En consecuencia, el estilo visual de los entornos que corren en X ​​varía mucho; diferentes tipos de programas pueden presentar interfaces radicalmente diferentes. X está construido como una capa de abstracción adicional (a modo de aplicación) que emerge después del kernel del sistema operativo._

El usuario tiene la libertad de configurar su entorno gráfico de muchas maneras.

## Window managers (gestores de ventanas)

Los gestores de ventanas (WMs) son clientes de X que proporcionan la interacción del usuario con el sistema a través de una ventana. El gestor de ventanas controla la apariencia de una aplicación y cómo se gestiona: el borde, barra de título, el tamaño y la capacidad de cambiar el tamaño de una ventana son manejadas por los gestores de ventanas. Muchos gestores de ventanas proporcionan otras funcionalidades, tales como lugares para pegar [dockapps](http://dockapps.windowmaker.org/), como [Window Maker](/index.php/Window_Maker "Window Maker"), un menú para iniciar programas, menús para configurar el WM y otras cosas útiles. [Fluxbox](/index.php/Fluxbox "Fluxbox"), por ejemplo, tiene la capacidad de abrir "pestañas" para las ventanas.

Los gestores de ventanas generalmente no proporcionan _extras_, como los iconos del escritorio, que son comúnmente vistos en los [entornos de escritorio](/index.php/Desktop_environment "Desktop environment") (aunque es posible añadir iconos en un WM con otro programa).

Debido a la falta de _extras_, los WMs son mucho más ligeros en cuanto al uso de recursos del sistema.

### Tipos

*   **Stacking** (conocidos como flotantes) son gestores de ventanas que proporcionan un símil del escritorio tradicional utilizado en los sistemas operativos comerciales como Windows y OS X. Gestionan las ventanas como pedazos de papel en un escritorio, y pueden ser apilados uno sobre el otro.
*   **Tiling** son gestores de ventanas tipo "mosaico" donde las ventanas no se superponen. Por lo general, hacen un uso muy extenso de atajos de teclado y tienen menos dependencia (o no del todo) en el ratón. La gestión de las ventanas en forma de mosaicos puede ser configurada manualmente, aunque ofrecen diseños predefinidos, o combinar ambos.
*   **Dynamic** son gestores de ventanas que permiten alternar dinámicamente el diseño de la ventanas entre mosaicos o flotantes.

*   [Category:Stacking WMs](/index.php/Category:Stacking_WMs "Category:Stacking WMs")
*   [Category:Tiling WMs](/index.php/Category:Tiling_WMs "Category:Tiling WMs")
*   [Category:Dynamic WMs](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs")

Consulte [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers") y [Wikipedia:Comparison of X window managers](https://en.wikipedia.org/wiki/Comparison_of_X_window_managers "wikipedia:Comparison of X window managers") para comparar window managers.

## Listado de gestores de ventanas

### Stacking WMs (Gestores de Ventanas Superpuestas)

*   **[2bwm](/index.php/2bwm "2bwm")** — 2bwm es un rápido gestor de ventanas flotante, con la particularidad de tener 2 bordes, escritos con la biblioteca XCB y derivado de mcwm escrito por Michael Cardell. En 2bwm todo es accesible desde el teclado, aunque se puede utilizar un dispositivo de señalización para mover, cambiar el tamaño y subir/bajar. El nombre ha cambiado recientemente de mcwm-beast a 2bwm.

[https://github.com/venam/2bwm](https://github.com/venam/2bwm) || [2bwm](https://aur.archlinux.org/packages/2bwm/)<sup><small>AUR</small></sup>

*   **aewm** — aewm es un gestor de ventanas moderno y minimalista para X11\. Se controla completamente con el ratón, pero no contiene ninguna interfaz de usuario visible aparte de los marcos de ventanas. El conjunto de comandos es algo así como vi: diseñado en la noche de los tiempos (1997) para exprimir la velocidad de las máquinas con poca memoria, poco intuitivos y totalmente hostil para el nuevo usuario, pero rápido y elegante a su manera.

[http://www.red-bean.com/decklin/aewm/](http://www.red-bean.com/decklin/aewm/) || [aewm](https://aur.archlinux.org/packages/aewm/)<sup><small>AUR</small></sup>

*   **[AfterStep](https://en.wikipedia.org/wiki/AfterStep "wikipedia:AfterStep")** — AfterStep es un gestor de ventanas para el sistema de ventanas X de Unix. Originalmente basado en la apariencia de la interfaz de NeXTStep, que proporciona a los usuarios un escritorio consistente, limpio y elegante. El objetivo del desarrollo AfterStep es proporcionar una flexibilidad de configuración del escritorio, la mejora estética y el uso eficiente de los recursos del sistema.

[http://www.afterstep.org/](http://www.afterstep.org/) || [afterstep](https://aur.archlinux.org/packages/afterstep/)<sup><small>AUR</small></sup>

*   **[Blackbox](https://en.wikipedia.org/wiki/Blackbox "wikipedia:Blackbox")** — Blackbox es un gestor rápido y ligero para el sistema de ventanas X, sin todas esas dependencias de bibliotecas molestas. Blackbox está construido con C++ y contiene código completamente original (a pesar de que la aplicación de gráficos es similar a la de WindowMaker).

[http://blackboxwm.sourceforge.net/](http://blackboxwm.sourceforge.net/) || [blackbox](https://www.archlinux.org/packages/?name=blackbox)

*   **[Compiz](/index.php/Compiz "Compiz")** — Compiz es un gestor de composición OpenGL que utiliza GLX_EXT_texture_from_pixma para la unión de nivel superior de ventanas a los objetos de textura. Cuenta con un flexible sistema plug-in y está diseñado para funcionar bien en la mayoría del hardware de gráficos.

[http://www.compiz.org/](http://www.compiz.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=compiz)</small>

*   **[Enlightenment](/index.php/Enlightenment "Enlightenment")** — Enlightenment no es solo un gestor de ventanas para Linux/X11 y otros, sino también todo un conjunto de bibliotecas que le permitirán crear interfaces de usuario atractivas con mucho menos trabajo respecto a herramientas tradicionales, por no hablar de que es un clásico entre los gestores de ventanas.

[http://www.enlightenment.org/](http://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[evilwm](/index.php/Evilwm "Evilwm")** — Un gestor de ventanas minimalista para el sistema de ventanas X. 'Minimalista' aquí no significa que sea demasiado desnudo para ser útil, solo significa que omite muchas de las cosas que hacen que otros gestores de ventanas sean más _usables_.

[http://www.6809.org.uk/evilwm/](http://www.6809.org.uk/evilwm/) || [evilwm](https://aur.archlinux.org/packages/evilwm/)<sup><small>AUR</small></sup>

*   **[Fluxbox](/index.php/Fluxbox "Fluxbox")** — Fluxbox es un gestor de ventanas para X que se basó en el código de Blackbox 0.61.1\. Es muy ligero en cuanto a recursos y fácil de manejar, pero, no obstante, lleno de características para hacer una experiencia de escritorio fácil y muy rápido. Está construido usando C++ y liberado bajo la licencia MIT.

[http://www.fluxbox.org/](http://www.fluxbox.org/) || [fluxbox](https://www.archlinux.org/packages/?name=fluxbox)

*   **[Flwm](https://en.wikipedia.org/wiki/FLWM "wikipedia:FLWM")** — Flwm es un intento de combinar las mejores ideas observadas en varios gestores de ventanas. La influencia principal y base del código es de wm2, por Chris Cannam .

[http://flwm.sourceforge.net/](http://flwm.sourceforge.net/) || [flwm](https://aur.archlinux.org/packages/flwm/)<sup><small>AUR</small></sup>

*   **[FVWM](/index.php/FVWM "FVWM")** — FVWM es un gestor de ventanas extremadamente potente, compatible con ICCM, escritorio virtual múltiple, para el sistema X Window. El desarrollo está activo y el apoyo es excelente.

[http://www.fvwm.org/](http://www.fvwm.org/) || [fvwm](https://www.archlinux.org/packages/?name=fvwm)

*   **Goomwwm** — Goomwwm es un gestor de ventanas X11 implementado en C como un proyecto de software cleanroom. Maneja las ventanas con un diseño flotante mínimo, mientras que proporciona flexibilidad con el teclado para controlar el cambio de ventanas, tamaño, movimiento, marcado y disposición en mosaico. También es rápido, ligero, modular, cuenta con Xinerama y, siempre que sea posible, compatible con EWMH.

[http://aerosuidae.net/goomwwm/](http://aerosuidae.net/goomwwm/) || [goomwwm](https://aur.archlinux.org/packages/goomwwm/)<sup><small>AUR</small></sup>

*   **[Hackedbox](https://en.wikipedia.org/wiki/Hackedbox "wikipedia:Hackedbox")** — Hackedbox es una versión simplificada de Blackbox. La barra de herramientas se ha eliminado. El objetivo de Hackedbox es hacer que el gestor sea un pequeño "conjunto de características", sin excesos. No hay planes de agregar cualquier funcionalidad, solo correcciones de errores y mejoras en la velocidad siempre que sea posible.

[http://scrudgeware.org/projects/Hackedbox/](http://scrudgeware.org/projects/Hackedbox/) || [hackedbox](https://aur.archlinux.org/packages/hackedbox/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/hackedbox)]</sup>

*   **[IceWM](/index.php/IceWM "IceWM")** — IceWM es un gestor de ventanas para el sistema X Window. El objetivo de IceWM es la velocidad, la simplicidad y facilitar el trabajo del usuario.

[http://www.icewm.org/](http://www.icewm.org/) || [icewm](https://www.archlinux.org/packages/?name=icewm)

*   **[JWM](/index.php/JWM "JWM")** — JWM es un gestor de ventanas para el sistema de ventanas X11\. JWM está escrito en C y solo utiliza un mínimo de Xlib.

[http://joewing.net/programs/jwm/](http://joewing.net/programs/jwm/) || [jwm](https://www.archlinux.org/packages/?name=jwm)

*   **Karmen** — Karmen es un gestor de ventanas para X, escrito por Johan Veenhuizen. Está diseñado para "funcionar". No hay ningún archivo de configuración y ninguna dependencia de otras bibliotecas que no sean Xlib. El modelo de selección de entrada es click-to-focus. Karmen tiene por objetivo ser compatible con ICCCM y EWMH.

[http://karmen.sourceforge.net/](http://karmen.sourceforge.net/) || [karmen](https://aur.archlinux.org/packages/karmen/)<sup><small>AUR</small></sup>

*   **[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")** — KWin, el gestor de ventanas estándar de KDE en KDE 4.0, viene con la primera versión del soporte integrado para la composición, por lo que es también un gestor de composición. Esto permite a KWin proporcionar efectos gráficos avanzados, similar a Compiz, mientras que también proporciona todas las características de las versiones anteriores de KDE (como muy buena integración con el resto de KDE, configuración avanzada, prevención del enfoque, un gestor de ventanas bien testado y con un robusto manejo de las aplicaciones/herramientas con comportamiento anómalo, etc).

[http://techbase.kde.org/Projects/KWin](http://techbase.kde.org/Projects/KWin) || [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)<sup><small>AUR</small></sup>

*   **lwm** — lwm es un gestor de ventanas para X que trata de mantenerse fuera de lo común. No hay iconos, ni barras de botones, ni soporte para iconos, ni menú principal, nada de nada: si quiere todo eso, tendrá que optar por otros programas que se lo proporcionen. No hay ninguna opción de configurabilidad: un gestor de ventanas diferente, si tiene un sistema operativo con poco espacio de disco y escasa memoria física.

[http://www.jfc.org.uk/software/lwm.html](http://www.jfc.org.uk/software/lwm.html) || [lwm](https://www.archlinux.org/packages/?name=lwm)

*   **[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")** — Esta no es la página de inicio de Metacity. No hay página de inicio Metacity. Por esta misma razón no hay logo llamativo: Metacity se esfuerza por ser silencioso, pequeño, estable, para seguir con su propio trabajo, y no distraer al usuario.

[http://blogs.gnome.org/metacity/](http://blogs.gnome.org/metacity/) || [metacity](https://www.archlinux.org/packages/?name=metacity)

*   **[Mutter](https://en.wikipedia.org/wiki/Mutter_(window_manager) "wikipedia:Mutter (window manager)")** — Gestor de composición y de ventanas para GNOME, basado en Clutter, utiliza OpenGL.

[http://git.gnome.org/browse/mutter/](http://git.gnome.org/browse/mutter/) || [mutter](https://www.archlinux.org/packages/?name=mutter)

*   **[Openbox](/index.php/Openbox "Openbox")** — Openbox es un gestor de ventanas altamente configurable, de última generación, con un extenso soporte de estándares. El estilo visual *box es bien conocido por su apariencia minimalista. Openbox utiliza el estilo *box para proporcionar un mayor número de opciones para los desarrolladores de temas en comparación con las anteriores implementaciones *box. La documentación de los temas describe toda la gama de opciones disponibles en los temas de Openbox.

[http://openbox.org/wiki/Main_Page](http://openbox.org/wiki/Main_Page) || [openbox](https://www.archlinux.org/packages/?name=openbox)

*   **[pawm](/index.php/Pawm "Pawm")** — pawm es un gestor de ventanas para el sistema X Window. No es un "escritorio" y, por tanto, no ofrece un enorme número de opciones inútiles, solo las aplicaciones necesarias para ejecutar los programas X y, al mismo tiempo, tiene una interfaz amigable y fácil de usar.

[http://www.pleyades.net/pawm/](http://www.pleyades.net/pawm/) || [pawm](https://www.archlinux.org/packages/?name=pawm)

*   **[pekwm](/index.php/Pekwm "Pekwm")** — pekwm es un gestor de ventanas que alguna vez se basó en el gestor de ventanas aewm + +, pero ha evolucionado lo suficiente como para que no se parezca a aewm + + en absoluto. Tiene un gran conjunto de características ampliadas, incluyendo agrupamiento de ventanas (similar a Ion, PWM, o Fluxbox), auto-propiedades, Xinerama, keygrabber que soporta la gestión keychains, y mucho más.

[http://www.pekwm.org/projects/pekwm](http://www.pekwm.org/projects/pekwm) || [pekwm](https://www.archlinux.org/packages/?name=pekwm)

*   **[Sawfish](/index.php/Sawfish "Sawfish")** — Sawfish es un gestor de ventanas extensible mediante un lenguaje de scripting basado en Lisp. Su política es mínima en comparación con la mayoría de los gestores de ventanas. Su objetivo es simplemente gestionar ventanas de la manera más flexible posible y atractiva. Todas las funciones de alto nivel del WM se implementan en Lisp para futuras ampliaciones o correcciones.

[http://sawfish.wikia.com/wiki/Main_Page](http://sawfish.wikia.com/wiki/Main_Page) || [sawfish](https://aur.archlinux.org/packages/sawfish/)<sup><small>AUR</small></sup>

*   **TinyWM** — TinyWM es un gestor de ventanas pequeño que se ha creado como un ejercicio de minimalismo. También es quizás útil para el aprendizaje de algunos de los conceptos básicos en la creación de un gestor de ventanas. Está compuesto tan solo alrededor de 50 líneas de C. También hay una versión de Python que utiliza python-xlib.

[http://incise.org/tinywm.html](http://incise.org/tinywm.html) || [tinywm](https://aur.archlinux.org/packages/tinywm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/tinywm)]</sup>

*   **[twm](/index.php/Twm "Twm")** — twm es un gestor de ventanas para el sistema X Window. Proporciona barra de títulos, ventanas redimensionables, varias formas de gestión a través de iconos, funciones de macro definidas por el usuario, click-to-type y permite personalizar el comportamiento del ratón, atajos de teclado y menú.

[http://cgit.freedesktop.org/xorg/app/twm/](http://cgit.freedesktop.org/xorg/app/twm/) || [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm)

*   **WindowLab** — WindowLab es un gestor de ventanas pequeño y simple de diseño novedoso. Características orientadas del puntero del ratón para hacer clic para centrarse, pero no para levantar el centro, un mecanismo para redimensionar el tamaño de las ventanas, lo que le permite cambiar uno o más bordes de las ventanas en una sola acción, y una innovadora barra de menú que comparte la misma parte de la pantalla con la barra de tareas. Las barras de título de las ventanas no pueden ir por encima del borde de la pantalla, lo que limita el puntero del ratón, que puede llegar a hacer que incluso coincidir la barra de tareas y menús, para que sean más fáciles de seleccionar..

[http://nickgravgaard.com/windowlab/](http://nickgravgaard.com/windowlab/) || [windowlab](https://www.archlinux.org/packages/?name=windowlab)

*   **[Window Maker](/index.php/Window_Maker "Window Maker")** — Window Maker es un gestor de ventanas X11 originalmente diseñado para proporcionar apoyo para la integración del entorno de escritorio GNUstep. Reproduce lo más posible el aspecto elegante y la interfaz de usuario de NEXTSTEP. Es rápido, rico en características, fácil de configurar y de usar. También es software libre, con aportes realizados por programadores de todo el mundo.

[http://windowmaker.org/](http://windowmaker.org/) || [windowmaker](https://www.archlinux.org/packages/?name=windowmaker)

*   **WM2** — wm2 es un gestor de ventanas para X. Proporciona un estilo inusual de decoración de las ventanas, y tiene poca funcionalidad como para que el usuario se sienta cómodo con el gestor de ventanas. wm2 no es configurable, excepto mediante la edición del código fuente y volverlo a compilar, y realmente está pensado para personas que no quieren que su particular gestor de ventanas sea demasiado amigable.

[http://www.all-day-breakfast.com/wm2/](http://www.all-day-breakfast.com/wm2/) || [wm2](https://aur.archlinux.org/packages/wm2/)<sup><small>AUR</small></sup>

*   **Xfwm** — El gestor de ventanas Xfce gestiona la colocación de las ventanas de aplicación en la pantalla, ofrece hermosas decoraciones de ventana, administra las áreas de trabajo o escritorios virtuales y, de forma nativa, soporta el modo multipantalla. Proporciona su propio gestor de composición (de la extensión X.Org Composite) para las transparencias y sombras. El gestor de ventanas Xfce también incluye un editor de atajos de teclado para los comandos especificados por los usuarios y manipulaciones básicas de Windows y proporciona un cuadro de diálogo de preferencias para ajustes avanzados.

[http://www.xfce.org/projects/xfwm4/](http://www.xfce.org/projects/xfwm4/) || [xfwm4](https://www.archlinux.org/packages/?name=xfwm4)

### Tiling window managers (Gestores de Ventanas tipo Mosaico)

*   **dswm** — dswm (Deep Space Window Manager) es una rama de [Stumpwm](/index.php/Stumpwm "Stumpwm")

[https://github.com/dss-project/dswm](https://github.com/dss-project/dswm) || [dswm](https://aur.archlinux.org/packages/dswm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dswm)]</sup>

*   **[Herbstluftwm](/index.php/Herbstluftwm "Herbstluftwm")** — herbstluftwm es un tiling window manager para X11 usando Xlib y Glib. El diseño se basa en frames que se dividen en subframes que pueden ser separados de nuevo o se pueden llenar con ventanas (similar a i3/musca). Etiquetas (o áreas de trabajo o escritorios virtuales) se pueden añadir/quitar en tiempo real. Cada etiqueta contiene un diseño propio. Exactamente una etiqueta se visualiza en cada monitor. Las etiquetas son independientes del monitor (similar a xmonad). Herbstclient se configura en tiempo de ejecución a través de llamadas IPC . De modo que el archivo de configuración es sólo un script que se ejecuta en el arranque. (Similar a wmii/musca)

[http://wwwcip.cs.fau.de/~re06huxa/herbstluftwm](http://wwwcip.cs.fau.de/~re06huxa/herbstluftwm) || [herbstluftwm-git](https://aur.archlinux.org/packages/herbstluftwm-git/)<sup><small>AUR</small></sup>

*   **[Ion3](/index.php/Ion3 "Ion3")** — Ion es un tiling window manager X11 diseñado pensando en el teclado de los usuarios. Fue uno de los primeros de la "nueva ola" de los entornos de ventanas de mosaico (el otro es larswm, con un enfoque muy diferente) y desde entonces ha dado lugar a toda una categoría de tiling window manager para X11 - ninguno de los cuales realmente logran reproducir el espíritu y la funcionalidad de Ion. Utiliza Lua como intérprete integrado que se encarga de toda la configuración.

[http://tuomov.iki.fi/software](http://tuomov.iki.fi/software) || [ion3](https://aur.archlinux.org/packages/ion3/)<sup><small>AUR</small></sup>

*   **[Notion](/index.php/Notion "Notion")** — Notion es un gestor de ventanas con pestañas para el sistema de ventanas X que utiliza 'cuadros' o fichas (a modo mosaico) y 'ventanas con pestañas'.
    *   Tiling: se divide la pantalla con ventanas no sobrepuestas, a modo de "mosaico". Cada ventana ocupa un cuadrado del mosaico, y se puede maximizar a toda la pantalla.
    *   Tabbing: un cuadro o ficha puede contener varias ventanas - que serán 'pestañas' repartidas a modo de cartas.
    *   Static: muchos gestores de ventanas con funcionalidad tilling son "dinámicos", en el sentido de que se redimensionan y se mueven automáticamente los cuadros dentro del mosaico cada vez que las ventanas aparecen y desaparecen. Nocion, por el contrario, no cambia automáticamente el mosaico.

Nocion es un fork de Ion3.

[http://notion.sf.net/](http://notion.sf.net/) || [notion](https://www.archlinux.org/packages/?name=notion)

*   **[Ratpoison](/index.php/Ratpoison "Ratpoison")** — Ratpoison es un administrador de ventanas simple, sin excesos, sin elementos gráficos de lujo, sin decoración en las ventanas, y no hay dependencias parásitas. Es en gran parte el modelo de "GNU Screen" que ha hecho maravillas en el mercado del terminal virtual. Ratpoison está configurado con un simple archivo de texto. La barra de información en ratpoison es algo diferente, ya que se muestra sólo cuando sea necesario. Sirve como un lanzador de aplicaciones, así como una barra de notificación. Ratpoison no incluye una bandeja del sistema .

[http://www.nongnu.org/ratpoison/](http://www.nongnu.org/ratpoison/) || [ratpoison](https://www.archlinux.org/packages/?name=ratpoison)

*   **[Stumpwm](/index.php/Stumpwm "Stumpwm")** — Stumpwm es un gestor de ventanas de mosaico para X11, escrito totalmente en Common Lisp, y orientado al uso del teclado. Stumpwm intenta ser lo mínimo adaptable visualmente. Stumpwm tiene varios hooks para ajustar las configuraciones personales y variables para modificar, y se puede reconfigurar y volver a cargar mientras está funcionando. No hay decoración de las ventanas, ni de los iconos, ni de los botones y no tienen bandeja de sistema. Su barra de información se puede configurar para que se muestre siempre o sólo cuando es necesario.

[http://www.nongnu.org/stumpwm/](http://www.nongnu.org/stumpwm/) || [stumpwm-git](https://aur.archlinux.org/packages/stumpwm-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/stumpwm-git)]</sup>

*   **[subtle](/index.php/Subtle "Subtle")** — subtle es un gestor de ventana tiling manual con un enfoque bastante poco común en esta categoría: por defecto, no hay aplicación de diseño típico, las ventanas se colocan en un punto (de anclaje) en una cuadrícula personalizada. El usuario puede cambiar el anclaje de cada ventana, ya sea directamente o por juego con reglas definidas por las etiquetas en la configuración. Cuenta con área de trabajo y las etiquetas de marcado automático del cliente, ratón y teclado de control, así como una barra de estado extensible.

[http://subforge.org/projects/subtle](http://subforge.org/projects/subtle) || [subtle](https://aur.archlinux.org/packages/subtle/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/subtle)]</sup>

*   **[WMFS](/index.php/WMFS "WMFS")** — WMFS (Window Manager From Scratch) es un tiling window manager para X de peso ligero y altamente configurable. Puede ser configurado con un archivo de configuración, soporta los caracteres Xft (FreeType) y es con compatible con la EWMH (Extended Window Manager Hints), especificaciones para las extensiones Xinerama y Xrandr, extendidas al gestor de ventanas. WMFS se puede gestionar con comandos de ViWMFS (basados en Vi​​).

[https://github.com/xorg62/wmfs](https://github.com/xorg62/wmfs) || [wmfs](https://aur.archlinux.org/packages/wmfs/)<sup><small>AUR</small></sup>

*   **[WMFS2](/index.php/WMFS2 "WMFS2")** — WMFS2 es un sucesor incompatible de WMFS. Es aún más minimalista y trae algunas cosas nuevas.

[https://github.com/xorg62/wmfs](https://github.com/xorg62/wmfs) || [wmfs2-git](https://aur.archlinux.org/packages/wmfs2-git/)<sup><small>AUR</small></sup>

### Dynamic window managers (Gestores de Ventanas Dinámicas)

*   **[awesome](/index.php/Awesome "Awesome")** — awesome es altamente configurable, el marco de la próxima generación de gestor de ventanas para X. Es muy rápido, extensible y liberado bajo la licencia GNU GPLv2\. Configurado en Lua, tiene una bandeja del sistema, barra de información, y el lanzador construido adentro. Hay extensiones disponibles escritas en Lua. Utiliza de forma impresionante XCB en oposición a Xlib, que puede dar como resultado un aumento de velocidad. Impresionantes también el uso de otras características, como una rápida sustitución del daemon para notificacioines, un menú del botón derecho similar a la de los gestores de ventanas *box y muchas otras cosas.

[http://awesome.naquadah.org/](http://awesome.naquadah.org/) || [awesome](https://www.archlinux.org/packages/?name=awesome)

*   **[catwm](/index.php/Catwm "Catwm")** — catwm es un gestor de ventanas pequeño, incluso más sencillo que dwm, escrito en C. La configuración se realiza modificando el archivo config.h y recompilándolo después.

[https://github.com/pyknite/catwm](https://github.com/pyknite/catwm) || [catwm-git](https://aur.archlinux.org/packages/catwm-git/)<sup><small>AUR</small></sup>

*   **[dwm](/index.php/Dwm "Dwm")** — dwm es un gestor de ventanas dinámico para X. Maneja las ventanas en estilos mosaicos y flotantes. Todos los diseños se pueden aplicar de forma dinámica, para la optimización del entorno con la aplicación en uso y para la tarea a ejecutar. No incluye una aplicación de bandeja del sistema ni lanzadores automáticos, aunque el menu se integra bien con él, ya que son del mismo autor. No tiene un archivo de configuración de texto. La configuración se realiza en su totalidad por la modificación del código fuente en C, y debe volver a compilarse y reiniciarse cada vez que se cambie. El tamaño del programa ya se encuentra en el límite de la línea autoimpuesta, restringiendo aún más el desarrollo.

[http://dwm.suckless.org/](http://dwm.suckless.org/) || [dwm](https://www.archlinux.org/packages/?name=dwm)

*   **[echinus](/index.php/Echinus "Echinus")** — gestor de ventanas tiling y de ventanas flotantes simple y ligero para X11\. Comenzó como un fork de dwm con una configuración más fácil, pero con el tiempo equino se convirtió en un gestor de ventanas completo con soporte EWMH. Cuenta con un panel EWMH-compatible/barra de tareas, llamado [ourico](https://aur.archlinux.org/packages/ourico/)<sup><small>AUR</small></sup>

[http://plhk.ru/echinus](http://plhk.ru/echinus) || [echinus](https://aur.archlinux.org/packages/echinus/)<sup><small>AUR</small></sup>

*   **euclid-wm** — euclid-wm es un simple y ligero gestor ventanas flotantes para X11, con soporte para minimizar ventanas. Un archivo de configuración de texto controla las asignaciones de teclas y ajustes. Comenzó como un fork dwm con una configuración más fácil, y se convirtió en un completo gestor de ventanas con el apoyo EWMH. Cuenta con un panel EWMH-compatible/barra de tareas llamado [ourico](https://aur.archlinux.org/packages/ourico/)<sup><small>AUR</small></sup>.

[http://euclid-wm.sourceforge.net/index.php](http://euclid-wm.sourceforge.net/index.php) || [euclid-wm](https://aur.archlinux.org/packages/euclid-wm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/euclid-wm)]</sup>

*   **[i3](/index.php/I3 "I3")** — i3 es un gestor de ventanas de tipo mosaico, escrito completamente desde cero. i3 se creó porque wmii, el gestor de ventanas del que procedía, no proporcionaba algunas características útiles (compatibilidad multi-monitor, por ejemplo) contenía algunos errores, poco progreso en su desarrollo y no era fácil mejorarlo en absoluto (al carecer por completo de comentarios y/o documentación del código fuente). Diferencias notables de i3 son las áreas de soporte multi-monitor y la distribución del árbol. Para la velocidad de la interfaz de Plan 9 wmii no está implementada

[http://i3wm.org/](http://i3wm.org/) || [i3-wm](https://www.archlinux.org/packages/?name=i3-wm)

*   **[monsterwm](/index.php/Monsterwm "Monsterwm")** — es un mínimo, ligero, pequeño pero dinámico gestor de ventanas de tipo mosaico. Se procura mantener lo más pequeño posible. En la actualidad menos de 700 líneas con el archivo de configuración incluido. Proporciona un conjunto de cuatro modos de diseño diferentes (pila vertical, pila inferior, rejilla y monóculo/pantalla completa) por defecto, y tiene compatibilidad con el modo flotante. También cuenta con soporte multi-monitor. Cada monitor y escritorio virtual tiene sus propias propiedades, no afectados por las configuraciones de los otros monitores o escritorios. La configuración se realiza en su totalidad por la modificación del código fuente en C, que se debe volver a compilar y reiniciar cada vez que se cambie. Hay muchos parches disponibles apoyados por los desarrolladores, en forma de ramas git diferentes .

[https://github.com/c00kiemon5ter/monsterwm](https://github.com/c00kiemon5ter/monsterwm) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=monsterwm)</small>

*   **[Musca](/index.php/Musca "Musca")** — Un gestor de ventanas dinámico y sencillo para X, con características de ratpoison y dwm. Musca funciona como un gestor de ventanas tiling por defecto. El usuario determina cómo la pantalla se divide en cuadros que no se superponen, sin restricciones en el diseño. Las ventanas de aplicación siempre llenan el marco asignado, con la excepción de las ventanas transitorias y cuadros de diálogo emergentes que flotan por encima de su aplicación principal con el tamaño apropiado. Una vez visible, las aplicaciones no cambian a menos que se haga manualmente.

[http://aerosuidae.net/musca.html](http://aerosuidae.net/musca.html) || [musca](https://aur.archlinux.org/packages/musca/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/musca)]</sup>

*   **[snapwm](/index.php/Snapwm "Snapwm")** — es un pequeño y ligero gestor de ventana dinámico y de mosaico basado en catwm y dminiwm. Las ventanas se incorporan en la barra de estado con espacios de trabajo seleccionables y cinco modos (vertical, horizontal cuadrícula, pantalla completa, y apilado). Tiene otras características, como los colores de estado, pertag, attachaside, un archivo rc recargable, soporte de transparencia, integración del menú y más.

[https://github.com/moetunes/Nextwm](https://github.com/moetunes/Nextwm) || [snapwm-git](https://aur.archlinux.org/packages/snapwm-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/snapwm-git)]</sup>

*   **[spectrwm](/index.php/Spectrwm "Spectrwm")** — Spectrwm es un pequeño y dinámico gestor de ventanas de tipo mosaico para X11, inspirado en gran parte por xmonad y dwm. Trata de mantenerse reducido a la mínima expresión para que el valioso espacio de la pantalla se puede utilizar para cosas mucho más importantes. Tiene ajuste predefinidos y se configura con un archivo de texto. Fue escrito por los hackers para los hackers y apunta a ser pequeño, compacto y rápido. Tiene una barra de estado integrada alimentada desde un script definido por el usuario.

[https://opensource.conformal.com/wiki/spectrwm](https://opensource.conformal.com/wiki/spectrwm) || [spectrwm](https://www.archlinux.org/packages/?name=spectrwm)

*   **[Qtile](/index.php/Qtile "Qtile")** — Qtile es un gestor de ventanas de tipo mosaico, con todas las funciones hackeables, escrito en Python. Qtile is simple, sencillo y extensible. Es fácil escribir sus propios diseños, widgets y órdenes incorporadas. Está escrito y configurado completamente en Python, lo que significa que puede aprovechar toda la potencia y flexibilidad de dicho lenguaje para que se ajuste a sus necesidades.

[https://github.com/qtile/qtile](https://github.com/qtile/qtile) || [qtile-git](https://aur.archlinux.org/packages/qtile-git/)<sup><small>AUR</small></sup>

*   **[Wingo](/index.php/Wingo "Wingo")** — Wingo es un completo gestor de ventanas, un verdadero híbrido que soporta espacios de trabajo por monitores, y no se encuadra ni en los modos flotantes ni en los modos mosaicos. Esto permite que se pueda desarrollar una modalidad mosaica en un área de trabajo mientras desarrolla otra modalidad flotante en otro espacio de trabajo. Wingo puede ser escrito con un lenguaje órdenes propio, es completamente configurable en los temas, y apoya los hooks definidos por el usuario. Wingo está escrito en Go y no tiene dependencias en runtime.

[https://github.com/BurntSushi/wingo](https://github.com/BurntSushi/wingo) || [wingo-git](https://aur.archlinux.org/packages/wingo-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/wingo-git)]</sup>

*   **[wmii](/index.php/Wmii "Wmii")** — wmii es un gestor pequeño, de ventanas dinámicas para X11\. Admite secuencias de comandos (scripts), tiene una interfaz de sistema de archivos 9P y soporta la gestión de ventanas a modo "clásico" o "mosaico" (Acme-like) . Su objetivo es mantener un código base pequeño y limpio (leible, mejorable y precioso) . La configuración por defecto es en bash y [rc (la shell Plan 9)](http://rc.cat-v.org), pero existen programas escritos en Ruby, y cualquier programa que pueda trabajar con el texto puede configurarlo. Cuenta con una barra de estado y el lanzador incorporado, y también una bandeja de sistema opcional (`witray`).

[http://wmii.suckless.org/](http://wmii.suckless.org/) || [wmii](https://www.archlinux.org/packages/?name=wmii)

*   **[xmonad](/index.php/Xmonad "Xmonad")** — xmonad es un gestor de ventanas dinámico de tipo mosaico para X11 que se escribe y se configura en Haskell. En un WM normal, se pasa mucho tiempo buscando y alineando las ventanas. xmonad facilita el trabajo, mediante la automatización de ésto. Para todos los cambios que se realicen en la configuración, xmonad debe volver a compilarse, por lo que el compilador Haskell (más de 100 MB), debe estar instalado. Una gran biblioteca llamada [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) ofrece muchas características adicionales

[http://xmonad.org/](http://xmonad.org/) || [xmonad](https://www.archlinux.org/packages/?name=xmonad)

## Enlaces externos

*   [http://www.gilesorr.com/wm/](http://www.gilesorr.com/wm/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Window_manager_(Español)&oldid=412835](https://wiki.archlinux.org/index.php?title=Window_manager_(Español)&oldid=412835)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Window managers (Español)](/index.php/Category:Window_managers_(Espa%C3%B1ol) "Category:Window managers (Español)")