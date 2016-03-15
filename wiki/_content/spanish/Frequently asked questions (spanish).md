Además de las preguntas tratadas más abajo, es posible que encuentre interesante la lectura de los artículos [The Arch Way (Español)](/index.php/The_Arch_Way_(Espa%C3%B1ol) "The Arch Way (Español)") y [Arch Linux (Español)](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)"). Ambos artículos contienen información muy útil sobre Arch Linux.

## Contents

*   [1 General](#General)
    *   [1.1 ¿Qué es Arch Linux??](#.C2.BFQu.C3.A9_es_Arch_Linux.3F.3F)
    *   [1.2 ¿Por qué puedo preferir usar Arch?](#.C2.BFPor_qu.C3.A9_puedo_preferir_usar_Arch.3F)
    *   [1.3 ¿Por qué podría no preferir usar Arch?](#.C2.BFPor_qu.C3.A9_podr.C3.ADa_no_preferir_usar_Arch.3F)
    *   [1.4 ¿En qué distribución se basa Arch?](#.C2.BFEn_qu.C3.A9_distribuci.C3.B3n_se_basa_Arch.3F)
    *   [1.5 ¿Qué arquitecturas soporta Arch?](#.C2.BFQu.C3.A9_arquitecturas_soporta_Arch.3F)
    *   [1.6 ¿Tiene Arch soporte para CPU ARM?](#.C2.BFTiene_Arch_soporte_para_CPU_ARM.3F)
    *   [1.7 Soy un completo principiante en GNU/Linux. ¿Debo usar Arch?](#Soy_un_completo_principiante_en_GNU.2FLinux._.C2.BFDebo_usar_Arch.3F)
    *   [1.8 Arch requiere mucho tiempo y esfuerzo para instalar y usar. Además, la comunidad sigue diciéndome: «lee la wiki» (o RTFM)](#Arch_requiere_mucho_tiempo_y_esfuerzo_para_instalar_y_usar._Adem.C3.A1s.2C_la_comunidad_sigue_dici.C3.A9ndome:_.C2.ABlee_la_wiki.C2.BB_.28o_RTFM.29)
    *   [1.9 ¿Arch está diseñado para ser utilizado como un servidor?, ¿un escritorio?, ¿una estación de trabajo?](#.C2.BFArch_est.C3.A1_dise.C3.B1ado_para_ser_utilizado_como_un_servidor.3F.2C_.C2.BFun_escritorio.3F.2C_.C2.BFuna_estaci.C3.B3n_de_trabajo.3F)
    *   [1.10 A mí me gusta Arch, excepto que el equipo de desarrollo debería implementar la *«funcionalidad X»*](#A_m.C3.AD_me_gusta_Arch.2C_excepto_que_el_equipo_de_desarrollo_deber.C3.ADa_implementar_la_.C2.ABfuncionalidad_X.C2.BB)
    *   [1.11 ¿Para cuándo la nueva versión disponible?](#.C2.BFPara_cu.C3.A1ndo_la_nueva_versi.C3.B3n_disponible.3F)
    *   [1.12 ¿Es Arch Linux una distribución estable? ¿Tiene problemas con frecuencia?](#.C2.BFEs_Arch_Linux_una_distribuci.C3.B3n_estable.3F_.C2.BFTiene_problemas_con_frecuencia.3F)
    *   [1.13 Arch necesita más prensa (es decir, publicidad)](#Arch_necesita_m.C3.A1s_prensa_.28es_decir.2C_publicidad.29)
    *   [1.14 Arch necesita más programadores](#Arch_necesita_m.C3.A1s_programadores)
    *   [1.15 ¿Por qué va mi internet tan lento en comparación con otros sistemas operativos?](#.C2.BFPor_qu.C3.A9_va_mi_internet_tan_lento_en_comparaci.C3.B3n_con_otros_sistemas_operativos.3F)
    *   [1.16 ¿Por qué Arch está usando toda mi RAM?](#.C2.BFPor_qu.C3.A9_Arch_est.C3.A1_usando_toda_mi_RAM.3F)
    *   [1.17 ¿De dónde vino todo mi espacio libre?](#.C2.BFDe_d.C3.B3nde_vino_todo_mi_espacio_libre.3F)
*   [2 Gestión de paquetes](#Gesti.C3.B3n_de_paquetes)
    *   [2.1 ¿En qué paquete está X?](#.C2.BFEn_qu.C3.A9_paquete_est.C3.A1_X.3F)
    *   [2.2 He encontrado un error con el paquete X. ¿Qué debo hacer?](#He_encontrado_un_error_con_el_paquete_X._.C2.BFQu.C3.A9_debo_hacer.3F)
    *   [2.3 Los paquetes que Arch deberían usar una única extensión. «.pkg.tar.gz» y «.pkg.tar.xz» son demasiado largos y/o confusos](#Los_paquetes_que_Arch_deber.C3.ADan_usar_una_.C3.BAnica_extensi.C3.B3n._.C2.AB.pkg.tar.gz.C2.BB_y_.C2.AB.pkg.tar.xz.C2.BB_son_demasiado_largos_y.2Fo_confusos)
    *   [2.4 Pacman necesita una biblioteca para que otras aplicaciones puedan acceder fácilmente a la información del paquete](#Pacman_necesita_una_biblioteca_para_que_otras_aplicaciones_puedan_acceder_f.C3.A1cilmente_a_la_informaci.C3.B3n_del_paquete)
    *   [2.5 ¿Por qué pacman no tiene un front-end gráfico (GUI) oficial?](#.C2.BFPor_qu.C3.A9_pacman_no_tiene_un_front-end_gr.C3.A1fico_.28GUI.29_oficial.3F)
    *   [2.6 Pacman necesita la *«característica X»*](#Pacman_necesita_la_.C2.ABcaracter.C3.ADstica_X.C2.BB)
    *   [2.7 ¿Cuál es la diferencia entre los distintos repositorios?](#.C2.BFCu.C3.A1l_es_la_diferencia_entre_los_distintos_repositorios.3F)
    *   [2.8 Acabo de instalar el paquete X. ¿Cómo empiezó?](#Acabo_de_instalar_el_paquete_X._.C2.BFC.C3.B3mo_empiez.C3.B3.3F)
    *   [2.9 ¿Por qué hay solo una única versión de cada biblioteca compartida en los repositorios oficiales?](#.C2.BFPor_qu.C3.A9_hay_solo_una_.C3.BAnica_versi.C3.B3n_de_cada_biblioteca_compartida_en_los_repositorios_oficiales.3F)
    *   [2.10 ¿Qué pasa si ejecuto «pacman -Syu» y hay una actualización de una biblioteca compartida, pero no para las aplicaciones que dependen de ella?](#.C2.BFQu.C3.A9_pasa_si_ejecuto_.C2.ABpacman_-Syu.C2.BB_y_hay_una_actualizaci.C3.B3n_de_una_biblioteca_compartida.2C_pero_no_para_las_aplicaciones_que_dependen_de_ella.3F)
    *   [2.11 ¿Es posible que haya una actualización del kernel principal, sin que se actualicen al mismo tiempo algunos de los paquetes de controladores?](#.C2.BFEs_posible_que_haya_una_actualizaci.C3.B3n_del_kernel_principal.2C_sin_que_se_actualicen_al_mismo_tiempo_algunos_de_los_paquetes_de_controladores.3F)
    *   [2.12 ¿Arch utiliza paquetes firmados?](#.C2.BFArch_utiliza_paquetes_firmados.3F)
    *   [2.13 ¿Qué hacer antes de actualizar?](#.C2.BFQu.C3.A9_hacer_antes_de_actualizar.3F)
*   [3 Instalación](#Instalaci.C3.B3n)
    *   [3.1 Arch necesita un instalador. Tal vez una instalación a través de GUI](#Arch_necesita_un_instalador._Tal_vez_una_instalaci.C3.B3n_a_trav.C3.A9s_de_GUI)
    *   [3.2 He instalado Arch, ¡y estoy en una shell! ¿Y ahora qué?](#He_instalado_Arch.2C_.C2.A1y_estoy_en_una_shell.21_.C2.BFY_ahora_qu.C3.A9.3F)
    *   [3.3 ¿Qué entorno de escritorio o gestor de ventanas debo usar?](#.C2.BFQu.C3.A9_entorno_de_escritorio_o_gestor_de_ventanas_debo_usar.3F)
    *   [3.4 ¿Qué hace único a Arch respecto de otras distribuciones «minimalistas»?](#.C2.BFQu.C3.A9_hace_.C3.BAnico_a_Arch_respecto_de_otras_distribuciones_.C2.ABminimalistas.C2.BB.3F)
*   [4 Otras](#Otras)
    *   [4.1 ¿Qué es AUR, de lo que tanto se habla?](#.C2.BFQu.C3.A9_es_AUR.2C_de_lo_que_tanto_se_habla.3F)
    *   [4.2 ¿Por qué aparece una pantalla verde cuando intento ver un vídeo?](#.C2.BFPor_qu.C3.A9_aparece_una_pantalla_verde_cuando_intento_ver_un_v.C3.ADdeo.3F)
    *   [4.3 La revisión ortográfica marca todo el texto ¡como incorrecto!](#La_revisi.C3.B3n_ortogr.C3.A1fica_marca_todo_el_texto_.C2.A1como_incorrecto.21)

## General

### ¿Qué es Arch Linux??

Consulte el artículo [Arch Linux (Español)](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)").

### ¿Por qué puedo preferir usar Arch?

Si, después de leer acerca de la filosofía [The Arch Way (Español)](/index.php/The_Arch_Way_(Espa%C3%B1ol) "The Arch Way (Español)"), desea abrazar el enfoque *«do-it-yourself»* («hágalo usted mismo») y quiere o desea una distribución GNU/Linux de propósito general, simple, elegante, altamente personalizable y vanguardista, quizás le pueda gustar Arch.

### ¿Por qué podría no preferir usar Arch?

Usted puede **no** querer usar Arch, si:

*   Después de la lectura de [The Arch Way (Español)](/index.php/The_Arch_Way_(Espa%C3%B1ol) "The Arch Way (Español)"), no está de acuerdo con su filosofía.
*   No tiene la capacidad/tiempo/ganas de usar una distribución GNU/Linux basada en *do-it-yourself* («hazlo tú mismo»).
*   Necesita compatibilidad con una arquitectura que no sea x86_64 o i686.
*   Tiene una postura firme sobre el uso de una distribución que solo proporcione software libre, según la definición de GNU.
*   Cree que un sistema operativo debería configurarse por sí solo, funcionar inmediatamente una vez instalado, e incluir por defecto un completo conjunto de software y entornos de escritorios en el soporte de instalación.
*   No desea una distribución GNU/Linux vanguardista y rolling release.
*   Está satisfecho con su actual sistema operativo.
*   Quiere un sistema operativo que se dirija a una base de usuarios diferente.
*   No está lo suficientemente loco para ejecutar un sistema operativo desarrollado por Allan.

### ¿En qué distribución se basa Arch?

Arch está desarrollada de forma independiente, construida desde cero, sin basarse en ninguna otra distribución GNU/Linux. Antes de crear Arch, Judd Vinet admiraba y utilizaba CRUX, una distribución genial y minimalista creada por Per Lidén. Originariamente inspirado por las ideas en común con CRUX, Arch fue construido desde cero, y luego Pacman fue codificado en C.

### ¿Qué arquitecturas soporta Arch?

Arch soporta las arquitecturas i686 y x86_64 (a veces llamado amd64) .

### ¿Tiene Arch soporte para CPU ARM?

No, pero el proyecto [Arch Linux ARM](http://archlinuxarm.org/) proporciona un puerto de Arch Linux para varias plataformas ARM.

### Soy un completo principiante en GNU/Linux. ¿Debo usar Arch?

Esta cuestión ha tenido mucho debate. Arch está dirigida más hacia usuarios avanzados de GNU/Linux, pero algunas personas sienten que Arch es un buen punto de partida para el principiante motivado. Si es un principiante y quiere usar Arch, tenga en cuanta únicamente que debe estar dispuesto a invertir un tiempo considerable en el aprendizaje de un nuevo sistema, así como aceptar el hecho de que Arch está diseñado fundamentalmente como una distribución DIY (*Do-It-Yourself*, Hágalo usted mismo). Es el usuario quien monta el sistema y controla en lo que se convertirá. Antes de pedir ayuda, haga su propia investigación independiente buscando en Google, indagando en el foro (y leyendo el resto de estas preguntas frecuentes) y buscando en la excelente documentación proporcionada por la wiki de Arch. *Hay una razón por la que estos recursos se ponen a disposición del usuario en primer lugar.* Son muchos los *voluntarios* que dedican miles de horas compilando esta información excelente.

Lectura recomendada: La [Guía para principiantes](/index.php/Beginners%27_Guide_(Espa%C3%B1ol) "Beginners' Guide (Español)") de Arch Linux.

### Arch requiere mucho tiempo y esfuerzo para instalar y usar. Además, la comunidad sigue diciéndome: «lee la wiki» (o [RTFM](https://en.wikipedia.org/wiki/es:RTFM "wikipedia:es:RTFM"))

Arch está diseñado y utilizado por y para una base de usuarios específicamente concreta. Tal vez no es la adecuada para usted. Consulte más [arriba](#Soy_un_completo_principiante_en_GNU.2FLinux._.C2.BFDebo_usar_Arch.3F).

### ¿Arch está diseñado para ser utilizado como un servidor?, ¿un escritorio?, ¿una estación de trabajo?

Arch no está diseñado para un tipo de uso particular. Más bien, está diseñado para un tipo particular de *usuario*. Arch está dirigido a usuarios competentes que disfrutan de su naturaleza do-it-yourself, y que además la aprovechan para moldear el sistema para satisfacer sus peculiares necesidades. Por lo tanto, moldeado según los propósitos del usuario, Arch se puede utilizar para virtualmente cualquier propósito. Muchos utilizan Arch tanto en los equipos de sobremesa como en estaciones de trabajo. Y por supuesto, archlinux.org se ejecuta en Arch.

### A mí me gusta Arch, excepto que el equipo de desarrollo debería implementar la *«funcionalidad X»*

Antes de seguir adelante, ¿leyó [The Arch Way (Español)](/index.php/The_Arch_Way_(Espa%C3%B1ol) "The Arch Way (Español)")? ¿Ha proporcionado la característica/solución? ¿Se ajusta a la filosofía de Arch sobre *minimalismo* y *exactitud de código* por encima de la comodidad? Involúcrese, contribuya con el código/solución a la comunidad. Si está bien considerado por el equipo de la comunidad y de desarrollo, tal vez sea integrado en Arch. La comunidad de Arch se nutre de la contribución y del intercambio del código y de las herramientas propias.

### ¿Para cuándo la nueva versión disponible?

Las versiones de Arch Linux no son más que una instantánea del repositorio [core], y se publican, por lo general, en la primera mitad de cada mes.

El modelo rolling release mantiene cada sistema Arch Linux actualizado y en la vanguardia mediante la ejecución de una única orden. Por esta razón, los lanzamientos no son importantes en Arch, porque se vuelven obsoletos tan pronto como el paquete ha sido actualizado. Si está buscando obtener la última versión de Arch Linux, no es necesario volver a instalarlo. Solo tiene que ejecutar la orden `pacman -Syu` y el sistema será el mismo que el que obtendría con una instalación completamente nueva. Por esta misma razón, las nuevas versiones de Linux Arch no suelen estar llenas de nuevas e interesantes características. Las características nuevas e interesantes son liberadas cuando sea necesario con los paquetes que se actualizan, y se pueden obtener inmediatamente con `pacman -Syu`.

### ¿Es Arch Linux una distribución estable? ¿Tiene problemas con frecuencia?

La respuesta corta es: Es en gran parte tan estable como *el usuario* la haga.

*Usted* ensambla su propio sistema Arch, sobre el entorno proporcionado por la base simple, y *usted* tiene el control de las actualizaciones del sistema. Obviamente, un sistema más grande, más complejo, que incorpora una multitud de paquetes personalizados, y una gran cantidad de herramientas y entornos de escritorio, sería más propenso a tener problemas de configuración debido a los cambios de los desarrolladores en las implementaciones de las aplicaciones, que uno más liviano, donde el sistema sería más simple. Arch está dirigido a usuarios capaces y proactivos. Competencias generales en UNIX y buenas prácticas en el mantenimiento y actualización del sistema también juegan un papel importante en la estabilidad del sistema. También cabe recordar que los paquetes de Arch vienen en su mayoría sin parches, por lo que la mayoría de los problemas de las aplicaciones son inherentes a los desarrolladores de las mismas.

Por lo tanto, *el usuario* es, en última instancia, el responsable de la estabilidad de su propio sistema rolling release. El usuario decide el momento de actualizar, e integra los cambios necesarios cuando se requiere. Si el usuario accede a la comunidad en busca de ayuda, a menudo se le presta de manera oportuna. La diferencia entre Arch y otras distribuciones, a este respecto, es que Arch es verdaderamente una distribución «do-it-yourself» ; las denuncias de ruptura son equivocadas e improductivas, cuando se debe a los cambios en las aplicaciones por los desarrolladores de las mismas, los cuales no son responsabilidad de los desarrolladores de Arch.

Vea el artículo [Enhance system stability](/index.php/Enhance_system_stability "Enhance system stability") para obtener consejos sobre cómo hacer que un sistema Arch Linux sea lo más estable posible.

### Arch necesita más prensa (es decir, publicidad)

Arch obtiene mucha publicidad tal como es. El objetivo de Arch Linux no es ser grande, sino más bien, proporcionar una distribución elegante, minimalista y vanguardista, centrada en la simplicidad y la corrección del código. Orgánicamente, el crecimiento sostenible se produce de forma natural entre los usuarios destinatarios.

### Arch necesita más programadores

Posiblemente sea así. ¡No dude en ofrecer su tiempo! Visite los [foros](https://bbs.archlinux.org), [canales IRC](/index.php/IRC_Channel "IRC Channel"), y [listas de correo](https://mailman.archlinux.org/mailman/listinfo/), y vea lo que hay pendiente por hacer. Comenzar a involucarse en el subforo de la *Community Contributions* es una buena manera de empezar.

### ¿Por qué va mi internet tan lento en comparación con otros sistemas operativos?

¿Está su red configurada correctamente? Eche un vistazo a [nombre del equipo](/index.php/Beginners%27_Guide_(Espa%C3%B1ol)#Nombre_del_equipo "Beginners' Guide (Español)") y [Configurar la red](/index.php/Beginners%27_Guide_(Espa%C3%B1ol)#Configurar_la_red "Beginners' Guide (Español)") de la Guía para Principiantes.

También tenga en cuenta que Arch Linux no viene con [traffic shaping](https://en.wikipedia.org/wiki/Traffic_shaping "wikipedia:Traffic shaping") habilitado. Por lo tanto, es posible que si un programa de alguna manera utiliza su conexión de Internet al máximo – sin importar si se trata de P2P o de conexiones de un clásico client-server – otras locales se encontrarán obstruidas, traduciéndose en retrasos graves y tiempos de espera. El auxilio puede venir instalando un [firewalls](/index.php/Firewalls "Firewalls") como Shorewall o Vuurmuur; también hay scripts estáticos para [iproute2](https://www.archlinux.org/packages/?name=iproute2) (como por ejemplo [este derivado](http://serendipity.ruwenzori.net/index.php/2008/06/01/modified-wondershaper-for-better-voip-qos) de Wondershaper), que realiza precisamente esta tarea.

### ¿Por qué Arch está usando toda mi RAM?

Fundamentalmente, una RAM no utilizada es una RAM desperdiciada.

Muchos usuarios han observado cómo el kernel de Linux maneja la memoria de manera diferente de como están acostumbrados. Dado que el acceso a los datos alojados en la RAM es mucho más rápido que desde una unidad de almacenamiento, el kernel guarda en la memoria los datos a los que se ha accedido recientemente. Los datos en caché solo se borran cuando el sistema comienza a quedarse sin memoria disponible y los nuevos datos necesitan ser cargados.

Quizás la causa más común de esta confusión es la orden `free`:

 `$ free -m` 
```
             total       used       free     shared    buffers     cached
Mem:          1009        741        267          0        104        359
-/+ buffers/cache:        278        731
Swap:         1537          0       1537
```

Es importante tener en cuenta que la línea `-/+ buffers/cache:` representa la cantidad de memoria que está realmente en «uso activo» y la cantidad de memoria «disponible», en lugar de la «no utilizada».

En el ejemplo anterior, un ordenador portátil con 1G de RAM total parece estar utilizando 741M de la misma, ¡con nada más que unos cuantos terminales en ralentí y un navegador web de código abierto!. Sin embargo, al examinar la línea descrita arriba, vemos que solo 278M de ella están en «uso activo», y de hecho, 731M están «disponibles» para los nuevos datos. Al parecer, 104M de la memoria «usada» contienen datos almacenados y 359M contienen datos almacenados en caché, los cuales pueden ser eliminados inmediatamente si es necesario. Solo 267M del total están verdaderamente «libres» de la carga de almacenamiento de datos.

¿El resultado final?. ¡Más prestaciones!

Consulte [este estupendo artículo](http://www.linuxjournal.com/article/2770) si se ha despertado su curiosidad. También hay un sitio web dedicado a despejar esta confusión: [http://www.linuxatemyram.com/](http://www.linuxatemyram.com/)

### ¿De dónde vino todo mi espacio libre?

La respuesta a esta pregunta depende de su sistema. Hay algunas [utilidades de disco](/index.php/Common_Applications#Disk_usage_display_programs "Common Applications") que pueden ayudarle a encontrar la respuesta.

## Gestión de paquetes

### ¿En qué paquete está X?

Puede averiguarlo con [pkgfile](/index.php/Pkgfile "Pkgfile").

Por ejemplo:

```
$ pkgfile *nombre_del_archivo*

```

### He encontrado un error con el paquete X. ¿Qué debo hacer?

En primer lugar, es necesario averiguar si el error es algo que el equipo de Arch puede arreglar. A veces no lo es (por ejemplo, los fallos de Firefox pueden ser responsabilidad del equipo de Mozilla), lo que se llama un error *upstream*. Si se trata de un problema de Arch, hay una serie de pasos que puede seguir:

1.  Busque en los foros para obtener información. Compruebe si alguien más lo ha notado.
2.  Publique un [bug report](/index.php/Reporting_bug_guidelines "Reporting bug guidelines") con información detallada en [https://bugs.archlinux.org](https://bugs.archlinux.org).
3.  Si lo considera oportuno, escriba un mensaje en el foro detallando el problema y el hecho de que ya lo ha informado. Esto ayudará a evitar que mucha gente avise del mismo error.

### Los paquetes que Arch deberían usar una única extensión. «.pkg.tar.gz» y «.pkg.tar.xz» son demasiado largos y/o confusos

Esto ha sido discutido en *Arch mailing list*. Algunos propusieron archivos con la extensión `.pac`. Por lo que se sabe actualmente, no existe un plan para cambiar la extensión de los paquetes. Como dijo Tobias Kieslich, uno de los desarrolladores de Arch: «*¡Un paquete **es** un tarball comprimido con* gzip *[xz]!. Y se puede abrir, investigar y manipular por cualquier aplicación que gestione los *.tar. Por otra parte, el mime-type es detectado automática y correctamente por la mayoría de las aplicaciones.*»

### Pacman necesita una biblioteca para que otras aplicaciones puedan acceder fácilmente a la información del paquete

Desde la versión 3.0.0, Pacman ha sido el front-end para libalpm, la biblioteca «Arch Linux Package Management». Esta biblioteca permite escribir otros front-ends alternativos (por ejemplo, un front-end gráfico).

### ¿Por qué pacman no tiene un front-end gráfico (GUI) oficial?

Por favor, lea [The Arch Way (Español)](/index.php/The_Arch_Way_(Espa%C3%B1ol) "The Arch Way (Español)") y [Arch Linux (Español)](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)"). Básicamente, la respuesta es que el equipo de desarrollo de Arch no proporcionará uno. Siéntase libre de utilizar el desarrollado por otros usuarios. Una lista selectiva puede encontrarse en [Pacman GUI Frontends](/index.php/Pacman_GUI_Frontends "Pacman GUI Frontends").

### Pacman necesita la *«característica X»*

Por favor, lea [The Arch Way (Español)](/index.php/The_Arch_Way_(Espa%C3%B1ol) "The Arch Way (Español)") y [Arch Linux (Español)](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)"). La filosofía de Arch es *«Keep It Simple»*. Si piensa que su idea tiene interés y no vulnera el principio de simplicidad, entonces puede optar por debatirla en el foro ([aquí](https://bbs.archlinux.org/)). También le recomendamos que compruebe [esto](https://bugs.archlinux.org); es un lugar para proponer peticiones de características si encuentra que es importante.

Sin embargo, la mejor manera de obtener una característica adicional a pacman o a Arch Linux es implementarla por si mismo. El parche o código puede o no ser admitido oficialmente, pero quizás otros apreciarán, probarán y contribuirán a su esfuerzo.

### ¿Cuál es la diferencia entre los distintos repositorios?

Consulte [Repositorios Oficiales](/index.php/Official_Repositories_(Espa%C3%B1ol) "Official Repositories (Español)").

### Acabo de instalar el paquete X. ¿Cómo empiezó?

Si está utilizando un entorno de escritorio como [KDE](/index.php/KDE "KDE") o [GNOME](/index.php/GNOME "GNOME"), el programa automáticamente debería aparecer en el menú. Si está tratando de ejecutar el programa desde un terminal y no sabe el nombre del archivo binario, utilice:

```
$ pacman -Qlq *nombre_del_paquete* | grep /usr/bin/

```

### ¿Por qué hay solo una única versión de cada biblioteca compartida en los repositorios oficiales?

Importantes distribuciones, como Debian, tienen diferentes versiones de bibliotecas compartidas incluidas en paquetes diferentes: `libfoo1`, `libfoo2`, `libfoo3` y así sucesivamente. De esta manera es posible tener aplicaciones compiladas con diferentes versiones de `libfoo` instaladas en el mismo sistema.

A diferencia de Debian, Arch es una distribución rolling-release de vanguardia. El rasgo más visible de una distribución de vanguardia es la disponibilidad de las últimas versiones de software en los repositorios, en el caso de una distribución como Arch, esto también significa que solo las últimas versiones de todos los paquetes están oficialmente soportadas. Si además añadimos soporte para software obsoleto, lo mantenedores de los paquetes tendrían que dedicar más tiempo asegurando que las nuevas versiones funcionan como se esperaba. Tan pronto como una nueva versión de una biblioteca compartida se hace disponible, los desarrolladores la añaden a los repositorios y recompilan los paquetes afectados para utilizar la nueva versión.

### ¿Qué pasa si ejecuto «pacman -Syu» y hay una actualización de una biblioteca compartida, pero no para las aplicaciones que dependen de ella?

Este escenario no debería ocurrir en absoluto. Suponiendo que una aplicación llamada `foobaz`, que está en uno de los repositorios oficiales, ha sido compilada con la biblioteca denominada `libbaz`, una actualización de `libbaz` conllevará una recompilación de foobaz, y pacman actualizará libbaz sin problemas. En caso contrario, si no se compila con éxito, el paquete `foobaz` tendrá una dependencia a una versión distinta (por ejemplo, *libbaz 1.5*), la cual se eliminó por pacman durante la actualización de `libbaz`, debido a un conflicto entre ambas.

Si `foobaz` es un paquete que se compiló e instaló desde AUR, debe tratar de recompilar `foobaz` con la nueva versión de `libbaz`. Si la compilación falla, informe del problema a los desarrolladores de `foobaz`.

### ¿Es posible que haya una actualización del kernel principal, sin que se actualicen al mismo tiempo algunos de los paquetes de controladores?

No, eso no es posible. Las principales actualizaciones del kernel (por ejemplo, *linux 3.5.0-1* a *linux 3.6.0-1*) siempre van acompañados de recompilaciones con todos los paquetes de controladores compatibles con el kernel. Por otro lado, si tiene un paquete de un controlador sin soporte oficial instalado en el sistema, como [catalyst](https://aur.archlinux.org/packages/catalyst/), y después de una actualización del kernel no recompila dicho controlador para el nuevo kernel, puede romperse el sistema. Los usuarios son responsables de actualizar los paquetes de controladores sin soporte que han instalado.

### ¿Arch utiliza paquetes firmados?

Si. La firma de paquetes en [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") se ha implementado desde la versión 4\. Véase [package signing](/index.php/Package_signing "Package signing") para obtener más información.

### ¿Qué hacer antes de actualizar?

En Arch Linux, es importante que, antes de actualizar, «compruebe las páginas principales de [las noticias de Arch](https://www.archlinux.org/), [las listas de anuncios](https://mailman.archlinux.org/mailman/listinfo/arch-announce/), y, opcionalmente, [el fórum](https://bbs.archlinux.org/) y [las listas de correos](https://mailman.archlinux.org/mailman/listinfo/), antes de oprimir la tecla *intro*.» Cualquier intrucción especial se publicarán en esos sitios.

## Instalación

### Arch necesita un instalador. Tal vez una instalación a través de GUI

Dado que la instalación no se produce con frecuencia (léase el resto de este artículo para saber más acerca de lo que significa *rolling release*), no es una alta prioridad para los desarrolladores o usuarios. La [Guía de instalación](/index.php/Installation_Guide_(Espa%C3%B1ol) "Installation Guide (Español)") y la [Guía para principiantes](/index.php/Beginners%27_Guide_(Espa%C3%B1ol) "Beginners' Guide (Español)") han sido completamente actualizadas para utilizar el método de línea de comandos. Si todavía está interesado en usar un instalador, considere el uso de [Archboot](/index.php/Archboot "Archboot").

### He instalado Arch, ¡y estoy en una shell! ¿Y ahora qué?

Véase la [Guía para principiantes](/index.php/Beginners%27_Guide_(Espa%C3%B1ol) "Beginners' Guide (Español)") de Arch Linux.

### ¿Qué entorno de escritorio o gestor de ventanas debo usar?

Ya que hay una gran variedad disponibles, use el que más se ajuste a sus necesidades. Véanse los artículos [Desktop Environment (Español)](/index.php/Desktop_Environment_(Espa%C3%B1ol) "Desktop Environment (Español)") y [Window Manager (Español)](/index.php/Window_Manager_(Espa%C3%B1ol) "Window Manager (Español)").

### ¿Qué hace único a Arch respecto de otras distribuciones «minimalistas»?

Algunas distribuciones pueden proporcionar métodos mínimos de instalación, que comparten algunas similitudes con el proceso de instalación de Arch. Sin embargo, algunos puntos deben tenerse en cuenta:

1.  Arch ha sido *diseñada fundamentalmente* como un entorno ligero, de base mínima, sobre la cual construir.
2.  El *único* camino para instalar Arch es compilando a partir de esta base mínima.
3.  El sistema base y toda la distribución asumen un enfoque de diseño K.I.S.S., lo que la hace especialmente adecuada para una determinada base de usuarios.
4.  La instalación de servicios y paquetes requiere participación manual, la configuración interactiva del usuario. A diferencia de otras distribuciones que automáticamente configuran los servicios y el comportamiento inicial, la filosofía de Arch pone énfasis en la competencia del usuario para controlar y manejar con responsabilidad el sistema.
5.  El empaquetado de Arch está diseñado para ser mínimo, y las dependencias entre paquetes son *opcionales*, no instalándose nunca automáticamente. Más bien, al usuario simplemente se le notifica de su existencia durante la instalación del paquete, lo que se traduce en un sistema más ligero.
6.  Arch ofrece una excelente y completa documentación, para ayudarle en el proceso de montaje del sistema.

## Otras

### ¿Qué es AUR, de lo que tanto se habla?

Véase [Arch User Repository#FAQ](/index.php/Arch_User_Repository#FAQ "Arch User Repository").

### ¿Por qué aparece una pantalla verde cuando intento ver un vídeo?

La profundidad del color está mal configurada. Es posible que tenga que ser 24 en lugar de 16, por ejemplo.

### La revisión ortográfica marca todo el texto ¡como incorrecto!

¿Ha istalado un diccionario [aspell](https://www.archlinux.org/packages/?name=aspell)? Utilice `pacman -Ss aspell` para ver los diccionarios disponibles que puede descargar.

Si instalando los archivos de diccionarios no resuelve el problema, lo más probable es que se trate de un problema con `enchant`. Compruebe si hay archivos de diccionarios conocidos:

 `$ aspell dicts` 
```
es
es_ES
...etc
```

Si el diccionario de la lengua correspondiente está en la lista, añádalo a `/usr/share/enchant/enchant.ordering`. En el ejemplo anterior, sería:

```
es_ES:aspell

```