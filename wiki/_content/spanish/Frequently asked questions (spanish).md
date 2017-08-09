**Estado de la traducción:** este artículo es una versión traducida de [Frequently asked questions](/index.php/Frequently_asked_questions "Frequently asked questions"). Fecha de la última traducción/revisión: **2016-04-03**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Frequently_asked_questions&diff=0&oldid=426982).

Además de las preguntas tratadas más abajo, es posible que encuentre interesante la lectura de los artículos [The Arch Way (Español)](/index.php/The_Arch_Way_(Espa%C3%B1ol) "The Arch Way (Español)") y [Arch Linux (Español)](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)"). Ambos artículos contienen información muy útil sobre Arch Linux.

## Contents

*   [1 General](#General)
    *   [1.1 ¿Qué es Arch Linux?](#.C2.BFQu.C3.A9_es_Arch_Linux.3F)
    *   [1.2 ¿Por qué podría no preferir usar Arch?](#.C2.BFPor_qu.C3.A9_podr.C3.ADa_no_preferir_usar_Arch.3F)
    *   [1.3 ¿Qué arquitecturas soporta Arch?](#.C2.BFQu.C3.A9_arquitecturas_soporta_Arch.3F)
    *   [1.4 ¿Tiene Arch soporte para CPU ARM?](#.C2.BFTiene_Arch_soporte_para_CPU_ARM.3F)
    *   [1.5 Soy un completo principiante en GNU/Linux. ¿Debo usar Arch?](#Soy_un_completo_principiante_en_GNU.2FLinux._.C2.BFDebo_usar_Arch.3F)
    *   [1.6 ¿Arch está diseñado para ser utilizado como un servidor?, ¿un escritorio?, ¿una estación de trabajo?](#.C2.BFArch_est.C3.A1_dise.C3.B1ado_para_ser_utilizado_como_un_servidor.3F.2C_.C2.BFun_escritorio.3F.2C_.C2.BFuna_estaci.C3.B3n_de_trabajo.3F)
    *   [1.7 A mí me gusta Arch, excepto que el equipo de desarrollo debería implementar la *«funcionalidad X»*](#A_m.C3.AD_me_gusta_Arch.2C_excepto_que_el_equipo_de_desarrollo_deber.C3.ADa_implementar_la_.C2.ABfuncionalidad_X.C2.BB)
    *   [1.8 ¿Para cuándo la nueva versión disponible?](#.C2.BFPara_cu.C3.A1ndo_la_nueva_versi.C3.B3n_disponible.3F)
    *   [1.9 ¿Es Arch Linux una distribución estable? ¿Tiene problemas con frecuencia?](#.C2.BFEs_Arch_Linux_una_distribuci.C3.B3n_estable.3F_.C2.BFTiene_problemas_con_frecuencia.3F)
    *   [1.10 Arch necesita más prensa (es decir, publicidad)](#Arch_necesita_m.C3.A1s_prensa_.28es_decir.2C_publicidad.29)
    *   [1.11 Arch necesita más programadores](#Arch_necesita_m.C3.A1s_programadores)
    *   [1.12 ¿Por qué va mi internet tan lento en comparación con otros sistemas operativos?](#.C2.BFPor_qu.C3.A9_va_mi_internet_tan_lento_en_comparaci.C3.B3n_con_otros_sistemas_operativos.3F)
    *   [1.13 ¿Por qué Arch está usando toda mi RAM?](#.C2.BFPor_qu.C3.A9_Arch_est.C3.A1_usando_toda_mi_RAM.3F)
    *   [1.14 ¿De dónde vino todo mi espacio libre?](#.C2.BFDe_d.C3.B3nde_vino_todo_mi_espacio_libre.3F)
*   [2 Gestión de paquetes](#Gesti.C3.B3n_de_paquetes)
    *   [2.1 ¿En qué paquete está X?](#.C2.BFEn_qu.C3.A9_paquete_est.C3.A1_X.3F)
    *   [2.2 He encontrado un error con el paquete X. ¿Qué debo hacer?](#He_encontrado_un_error_con_el_paquete_X._.C2.BFQu.C3.A9_debo_hacer.3F)
    *   [2.3 Los paquetes que Arch deberían usar una única extensión. «.pkg.tar.gz» y «.pkg.tar.xz» son demasiado largos y/o confusos](#Los_paquetes_que_Arch_deber.C3.ADan_usar_una_.C3.BAnica_extensi.C3.B3n._.C2.AB.pkg.tar.gz.C2.BB_y_.C2.AB.pkg.tar.xz.C2.BB_son_demasiado_largos_y.2Fo_confusos)
    *   [2.4 Pacman necesita una biblioteca para que otras aplicaciones puedan acceder fácilmente a la información del paquete](#Pacman_necesita_una_biblioteca_para_que_otras_aplicaciones_puedan_acceder_f.C3.A1cilmente_a_la_informaci.C3.B3n_del_paquete)
    *   [2.5 Pacman necesita la *«característica X»*](#Pacman_necesita_la_.C2.ABcaracter.C3.ADstica_X.C2.BB)
    *   [2.6 ¿Cuál es la diferencia entre los distintos repositorios?](#.C2.BFCu.C3.A1l_es_la_diferencia_entre_los_distintos_repositorios.3F)
    *   [2.7 Acabo de instalar el paquete X. ¿Cómo empiezo?](#Acabo_de_instalar_el_paquete_X._.C2.BFC.C3.B3mo_empiezo.3F)
    *   [2.8 ¿Por qué hay solo una única versión de cada biblioteca compartida en los repositorios oficiales?](#.C2.BFPor_qu.C3.A9_hay_solo_una_.C3.BAnica_versi.C3.B3n_de_cada_biblioteca_compartida_en_los_repositorios_oficiales.3F)
    *   [2.9 ¿Qué pasa si ejecuto una actualización completa del sistema y hay una actualización de una biblioteca compartida, pero no para las aplicaciones que dependen de ella?](#.C2.BFQu.C3.A9_pasa_si_ejecuto_una_actualizaci.C3.B3n_completa_del_sistema_y_hay_una_actualizaci.C3.B3n_de_una_biblioteca_compartida.2C_pero_no_para_las_aplicaciones_que_dependen_de_ella.3F)
    *   [2.10 ¿Es posible que haya una actualización del kernel principal, sin que se actualicen al mismo tiempo algunos de los paquetes de controladores?](#.C2.BFEs_posible_que_haya_una_actualizaci.C3.B3n_del_kernel_principal.2C_sin_que_se_actualicen_al_mismo_tiempo_algunos_de_los_paquetes_de_controladores.3F)
    *   [2.11 ¿Arch utiliza paquetes firmados?](#.C2.BFArch_utiliza_paquetes_firmados.3F)
    *   [2.12 ¿Qué hacer antes de actualizar?](#.C2.BFQu.C3.A9_hacer_antes_de_actualizar.3F)
    *   [2.13 Un paquete de actualización fue liberado, pero pacman dice que el sistema está al día](#Un_paquete_de_actualizaci.C3.B3n_fue_liberado.2C_pero_pacman_dice_que_el_sistema_est.C3.A1_al_d.C3.ADa)
*   [3 Instalación](#Instalaci.C3.B3n)
    *   [3.1 Arch necesita un instalador. ¿Tal vez una instalación a través de GUI?](#Arch_necesita_un_instalador._.C2.BFTal_vez_una_instalaci.C3.B3n_a_trav.C3.A9s_de_GUI.3F)
    *   [3.2 He instalado Arch, ¡y estoy en una shell! ¿Y ahora qué?](#He_instalado_Arch.2C_.C2.A1y_estoy_en_una_shell.21_.C2.BFY_ahora_qu.C3.A9.3F)
    *   [3.3 ¿Qué entorno de escritorio o gestor de ventanas debo usar?](#.C2.BFQu.C3.A9_entorno_de_escritorio_o_gestor_de_ventanas_debo_usar.3F)
    *   [3.4 ¿Qué hace único a Arch respecto de otras distribuciones «minimalistas»?](#.C2.BFQu.C3.A9_hace_.C3.BAnico_a_Arch_respecto_de_otras_distribuciones_.C2.ABminimalistas.C2.BB.3F)
*   [4 64-bit](#64-bit)
    *   [4.1 ¿Cómo puedo saber si mi procesador es compatible con x86_64?](#.C2.BFC.C3.B3mo_puedo_saber_si_mi_procesador_es_compatible_con_x86_64.3F)
    *   [4.2 ¿Voy a tener todos los paquetes en mi Arch de 32 bits?](#.C2.BFVoy_a_tener_todos_los_paquetes_en_mi_Arch_de_32_bits.3F)
    *   [4.3 ¿Por qué 64 bits?](#.C2.BFPor_qu.C3.A9_64_bits.3F)
    *   [4.4 ¿Puedo construir paquetes de 32 bits para i686 dentro de Arch de 64-bit?](#.C2.BFPuedo_construir_paquetes_de_32_bits_para_i686_dentro_de_Arch_de_64-bit.3F)
    *   [4.5 ¿Puedo cambiar de i686 a x86_64 sin reinstalar?](#.C2.BFPuedo_cambiar_de_i686_a_x86_64_sin_reinstalar.3F)

## General

### ¿Qué es Arch Linux?

Consulte el artículo [Arch Linux (Español)](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)").

### ¿Por qué podría no preferir usar Arch?

Usted puede **no** querer usar Arch, si:

*   No tiene la capacidad/tiempo/ganas de usar una distribución GNU/Linux basada en *do-it-yourself* («hazlo tú mismo»).
*   Necesita compatibilidad con una arquitectura que no sea x86_64.
*   Tiene una postura firme sobre el uso de una distribución que solo proporcione software libre, según la definición de GNU.
*   Cree que un sistema operativo debería configurarse por sí solo y funcionar una vez instalado, incluyendo por defecto un completo conjunto de software y entornos de escritorios en el soporte de instalación.
*   No desea una distribución GNU/Linux rolling release («lanzamiento continuo»).
*   Está satisfecho con su sistema operativo actual.

### ¿Qué arquitecturas soporta Arch?

Arch sólo soporta x86_64 (a veces llamado amd64). El soporte para i686 será descartado y eliminado por completo en noviembre del 2017 [[1]](https://www.archlinux.org/news/phasing-out-i686-support/). Si todavía está ejecutando un sistema de 32-bit puede estar interesado en leer [¿Cómo puedo saber si mi procesador es compatible con x86_64?](#.C2.BFC.C3.B3mo_puedo_saber_si_mi_procesador_es_compatible_con_x86_64.3F)

### ¿Tiene Arch soporte para CPU ARM?

No, pero el proyecto [Arch Linux ARM](http://archlinuxarm.org/) proporciona un puerto de Arch Linux para varias plataformas ARM.

### Soy un completo principiante en GNU/Linux. ¿Debo usar Arch?

Si es un principiante y quiere usar Arch, tenga en cuanta únicamente que debe estar dispuesto a invertir un tiempo considerable en el aprendizaje de un nuevo sistema, así como aceptar el hecho de que Arch está diseñado fundamentalmente como una distribución DIY (*Do-It-Yourself*, Hágalo usted mismo). Es el usuario quien monta el sistema y controla en lo que se convertirá.

Antes de pedir ayuda, haga su propia investigación independiente buscando en Google, indagando en el foro (y leyendo el resto de estas preguntas frecuentes) y buscando en la excelente documentación proporcionada por la wiki de Arch. *Hay una razón por la que estos recursos se ponen a disposición del usuario en primer lugar.* Son muchos los *voluntarios* que dedican miles de horas compilando esta excelente información.

Véase también [Arch terminology#RTFM](/index.php/Arch_terminology#RTFM "Arch terminology") y la [Beginners' guide (Español)](/index.php/Beginners%27_guide_(Espa%C3%B1ol) "Beginners' guide (Español)").

### ¿Arch está diseñado para ser utilizado como un servidor?, ¿un escritorio?, ¿una estación de trabajo?

Arch no está diseñado para un tipo de uso particular. Más bien, está diseñado para un tipo particular de *usuario*. Arch está dirigido a usuarios competentes que disfrutan de su naturaleza do-it-yourself, y que además la aprovechan para moldear el sistema y satisfacer sus necesidades. Por lo tanto, moldeado según los propósitos del usuario, Arch se puede utilizar prácticamente para cualquier propósito. Muchos utilizan Arch tanto en equipos de sobremesa como en estaciones de trabajo. Y por supuesto, archlinux.org se ejecuta en Arch.

### A mí me gusta Arch, excepto que el equipo de desarrollo debería implementar la *«funcionalidad X»*

Involúcrese, contribuya con el código/solución a la comunidad. Si está bien considerado por el equipo de la comunidad y de desarrollo, tal vez sea integrado en Arch. La comunidad de Arch se nutre de la contribución y del intercambio de códigos y de herramientas.

### ¿Para cuándo la nueva versión disponible?

Los lanzamientos de Arch Linux son simplemente un entorno live para la instalación o el rescate, que incluyen el grupo [base](https://www.archlinux.org/groups/x86_64/base/) y unos pocos [paquetes adicionales](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both). Las versiones se liberan, por lo general, en la primera mitad de cada mes.

### ¿Es Arch Linux una distribución estable? ¿Tiene problemas con frecuencia?

Es *el usuario*, en última instancia, el responsable de la estabilidad de su propio sistema rolling release. El usuario decide el momento de actualizar, e integra los cambios necesarios cuando se requiere. Si el usuario accede a la comunidad en busca de ayuda, a menudo se le presta de manera oportuna. La diferencia entre Arch y otras distribuciones es que Arch es verdaderamente una distribución «do-it-yourself» ; las denuncias de ruptura son equivocadas e improductivas, cuando se debe a los cambios hechos a las aplicaciones por los desarrolladores de las mismas, sin ser responsabilidad del equipo que desarrolla Arch.

Vea el artículo [System maintenance](/index.php/System_maintenance "System maintenance") para obtener consejos sobre cómo hacer que un sistema Arch Linux sea lo más estable posible.

### Arch necesita más prensa (es decir, publicidad)

Arch obtiene mucha publicidad tal como es. El objetivo de Arch Linux no es ser grande, sino más bien, orgánicamente, el crecimiento sostenible se produce de forma natural entre los usuarios destinatarios.

### Arch necesita más programadores

Posiblemente sea así. ¡No dude en ofrecer su tiempo! Visite los [foros](https://bbs.archlinux.org), [canales IRC](/index.php/IRC_channel "IRC channel") y [listas de correo](https://mailman.archlinux.org/mailman/listinfo/), y vea lo que hay pendiente por hacer. Comenzar a involucarse en el subforo de la *Community Contributions* es una buena manera de empezar.

### ¿Por qué va mi internet tan lento en comparación con otros sistemas operativos?

¿Está su red configurada correctamente? Eche un vistazo a [nombre del equipo](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Nombre_del_equipo "Beginners' guide (Español)") y [Configurar la red](/index.php/Beginners%27_guide_(Espa%C3%B1ol)#Configurar_la_red "Beginners' guide (Español)") de la Guía para principiantes.

También tenga en cuenta que Arch Linux no viene con [traffic shaping](https://en.wikipedia.org/wiki/Traffic_shaping "wikipedia:Traffic shaping") habilitado. Por lo tanto, es posible que si un programa, de alguna manera, utiliza su conexión de Internet al máximo –sin importar si se trata de P2P o de conexiones de un clásico client-server– otras conexiones locales se encontrarán obstruidas, traduciéndose en retrasos graves y tiempos de espera. El auxilio puede venir instalando un [firewalls](/index.php/Firewalls "Firewalls") como Shorewall o Vuurmuur; también hay scripts estáticos para [iproute2](https://www.archlinux.org/packages/?name=iproute2) (como por ejemplo [este derivado](http://serendipity.ruwenzori.net/index.php/2008/06/01/modified-wondershaper-for-better-voip-qos) de Wondershaper), que realiza precisamente esta tarea.

### ¿Por qué Arch está usando toda mi RAM?

Fundamentalmente, una RAM no utilizada es una RAM desperdiciada.

Muchos usuarios han observado cómo el kernel de Linux maneja la memoria de manera diferente de como están acostumbrados. Dado que el acceso a los datos alojados en la RAM es mucho más rápido que desde una unidad de almacenamiento, el kernel guarda en la memoria los datos a los que se ha accedido recientemente. Los datos en caché solo se borran cuando el sistema comienza a quedarse sin memoria disponible y los nuevos datos necesitan ser cargados.

Quizás la causa más común de esta confusión es la orden `free`:

 `$ free -h` 
```
              total        used        free      shared  buff/cache   available
Mem:           2.8G        1.1G        283M        224M        1.4G        1.2G
Swap:          3.0G        881M        2.1G

```

Es importante distinguir entre memoria «free» y «available». En el ejemplo anterior, un portátil con 2,8G de memoria RAM total parece estar utilizando la mayor parte de ella, y solo disponer de 283M de memoria libre. Sin embargo, 1,4G de la misma está en «buff/cache». Todavía hay 1,2G disponibles para iniciar nuevas aplicaciones, sin tener que acudir a la memoria swap. Vea `man free(1)` para obtener más detalles. ¿El resultado de todo esto? ¡Más rendimiento!

Consulte [este maravilloso artículo](http://www.linuxjournal.com/article/2770) ¡si su curiosidad se ha despertado! También hay un sitio web dedicado a aclarar esta confusión: [http://www.linuxatemyram.com/](http://www.linuxatemyram.com/)

### ¿De dónde vino todo mi espacio libre?

La respuesta a esta pregunta depende de su sistema. Hay algunas [utilidades de discoque](/index.php/Common_Applications#Disk_usage_display_programs "Common Applications") pueden ayudarle a encontrar la respuesta.

## Gestión de paquetes

### ¿En qué paquete está X?

Puede averiguarlo con [pkgfile](/index.php/Pkgfile "Pkgfile").

Por ejemplo:

```
$ pkgfile *nombre_del_archivo*

```

### He encontrado un error con el paquete X. ¿Qué debo hacer?

En primer lugar, es necesario averiguar si el error es algo que el equipo de Arch puede arreglar. A veces no lo es (por ejemplo, los fallos de Firefox pueden ser responsabilidad del equipo de Mozilla), lo que se llama un error *upstream*. Si se trata de un problema de Arch, hay una serie de pasos que puede seguir:

1.  busque en los foros para obtener información. Compruebe si alguien más lo ha notado;
2.  publique un [bug report](/index.php/Reporting_bug_guidelines "Reporting bug guidelines") con información detallada en [https://bugs.archlinux.org](https://bugs.archlinux.org);
3.  si lo considera oportuno, escriba un mensaje en el foro detallando el problema y el hecho de que ya lo ha informado. Esto ayudará a evitar que mucha gente avise del mismo error.

### Los paquetes que Arch deberían usar una única extensión. «.pkg.tar.gz» y «.pkg.tar.xz» son demasiado largos y/o confusos

Esto ha sido discutido en *Arch mailing list*. Algunos propusieron archivos con la extensión `.pac`. Por lo que se sabe actualmente, no existe un plan para cambiar la extensión de los paquetes. Como dijo Tobias Kieslich, uno de los desarrolladores de Arch: «*¡Un paquete **es** un tarball comprimido con* gzip *[xz]!. Y se puede abrir, investigar y manipular por cualquier aplicación que gestione los *.tar. Por otra parte, el mime-type es detectado automática y correctamente por la mayoría de las aplicaciones.*»

### Pacman necesita una biblioteca para que otras aplicaciones puedan acceder fácilmente a la información del paquete

Desde la versión 3.0.0, pacman ha sido el front-end para libalpm, la biblioteca «Arch Linux Package Management». Esta biblioteca permite escribir otros front-ends alternativos (por ejemplo, un front-end gráfico).

### Pacman necesita la *«característica X»*

Si piensa que su idea tiene interés, entonces puede optar por debatirla en [pacman-dev](https://lists.archlinux.org//listinfo/pacman-dev/). También le recomendamos que compruebe [https://bugs.archlinux.org](https://bugs.archlinux.org) por si encuentra peticiones de características similares.

Sin embargo, la mejor manera de obtener una característica adicional a pacman o a Arch Linux es implementarla por si mismo. El parche o código puede o no ser admitido oficialmente, pero quizás otros apreciarán, probarán y contribuirán a su esfuerzo.

### ¿Cuál es la diferencia entre los distintos repositorios?

Consulte [Repositorios Oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

### Acabo de instalar el paquete X. ¿Cómo empiezo?

Si está utilizando un entorno de escritorio como [KDE](/index.php/KDE "KDE") o [GNOME](/index.php/GNOME "GNOME"), el programa automáticamente debería aparecer en el menú. Si está tratando de ejecutar el programa desde un terminal y no sabe el nombre del archivo binario, utilice:

```
$ pacman -Qlq *nombre_del_paquete* | grep /usr/bin/

```

### ¿Por qué hay solo una única versión de cada biblioteca compartida en los repositorios oficiales?

Importantes distribuciones, como Debian, tienen diferentes versiones de bibliotecas compartidas incluidas en paquetes diferentes: `libfoo1`, `libfoo2`, `libfoo3` y así sucesivamente. De esta manera es posible tener aplicaciones compiladas con diferentes versiones de `libfoo` instaladas en el mismo sistema.

En el caso de una distribución como Arch, solo las últimas versiones estables de paquetes tienen soporte oficial. Si retiramos el soporte para software obsoleto, lo mantenedores de los paquetes tendrán más tiempo para dedicar a las nuevas versiones asegurando así que las mismas funcionen como se espera de ellas. Tan pronto como una nueva versión de una biblioteca compartida se hace disponible, los desarrolladores la añaden a los repositorios y recompilan los paquetes afectados para utilizar la nueva versión.

### ¿Qué pasa si ejecuto una actualización completa del sistema y hay una actualización de una biblioteca compartida, pero no para las aplicaciones que dependen de ella?

Este escenario no debería ocurrir en absoluto. Suponiendo que una aplicación llamada `foobaz`, que está en uno de los repositorios oficiales, ha sido compilada con la biblioteca denominada `libbaz`, una actualización de `libbaz` conllevará una recompilación de foobaz, y pacman actualizará libbaz sin problemas. En caso contrario, si no se compila con éxito, el paquete `foobaz` tendrá una dependencia a una versión distinta (por ejemplo, *libbaz 1.5*), la cual se habría eliminado por pacman durante la actualización de `libbaz`, debido a un conflicto entre ambas.

Si `foobaz` es un paquete que se compiló e instaló desde AUR, debe tratar de recompilar `foobaz` con la nueva versión de `libbaz`. Si la compilación falla, informe del problema a los desarrolladores de `foobaz`.

### ¿Es posible que haya una actualización del kernel principal, sin que se actualicen al mismo tiempo algunos de los paquetes de controladores?

No, eso no es posible. Las principales actualizaciones del kernel (por ejemplo, *linux 3.5.0-1* a *linux 3.6.0-1*) siempre van acompañados de recompilaciones con todos los paquetes de controladores compatibles con el kernel. Por otro lado, si tiene un paquete de un controlador sin soporte oficial instalado en el sistema, como [catalyst](https://aur.archlinux.org/packages/catalyst/), y después de una actualización del kernel no recompila dicho controlador para el nuevo kernel, puede romperse el sistema. Los usuarios son responsables de actualizar los paquetes de controladores sin soporte que han instalado.

### ¿Arch utiliza paquetes firmados?

Si. La firma de paquetes en [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") se ha implementado desde la versión 4\. Véase [package signing](/index.php/Package_signing "Package signing") para obtener más información.

### ¿Qué hacer antes de actualizar?

En Arch Linux, es importante que, antes de actualizar, «compruebe las páginas principales de [las noticias de Arch](https://www.archlinux.org/), [las listas de anuncios](https://mailman.archlinux.org/mailman/listinfo/arch-announce/), y, opcionalmente, [el fórum](https://bbs.archlinux.org/) y [las listas de correos](https://mailman.archlinux.org/mailman/listinfo/), antes de oprimir la tecla *intro*.» Cualquier intrucción especial se publicará en esos sitios.

### Un paquete de actualización fue liberado, pero pacman dice que el sistema está al día

Los servidores de réplicas de *pacman* no se sincronizan inmediatamente. Puede tomar más de 24 horas antes de una actualización está disponible para usted. Las únicas opciones son que sea paciente o utilizar otro servidor de réplica. [MirrorStatus](https://www.archlinux.org/mirrors/status/) puede ayudar a identificar un servidor de réplica actualizado.

## Instalación

### Arch necesita un instalador. ¿Tal vez una instalación a través de GUI?

Dado que la instalación no se produce con frecuencia (léase el resto de este artículo para saber más acerca de lo que significa *rolling release*), no es una alta prioridad para los desarrolladores o usuarios. La [Guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)") y la [Guía para principiantes](/index.php/Beginners%27_guide_(Espa%C3%B1ol) "Beginners' guide (Español)") han sido completamente actualizadas para utilizar el método de línea de órdenes. Si todavía está interesado en usar un instalador, considere el uso de [Archboot](/index.php/Archboot "Archboot").

### He instalado Arch, ¡y estoy en una shell! ¿Y ahora qué?

Véase la [Guía para principiantes](/index.php/Beginners%27_guide_(Espa%C3%B1ol) "Beginners' guide (Español)") de Arch Linux.

### ¿Qué entorno de escritorio o gestor de ventanas debo usar?

Ya que hay una gran variedad disponibles, use el que más se ajuste a sus necesidades. Véanse los artículos [Desktop environment (Español)](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") y [Window manager (Español)](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)").

### ¿Qué hace único a Arch respecto de otras distribuciones «minimalistas»?

Vea [Arch compared to other distributions (Español)](/index.php/Arch_compared_to_other_distributions_(Espa%C3%B1ol) "Arch compared to other distributions (Español)").

## 64-bit

### ¿Cómo puedo saber si mi procesador es compatible con x86_64?

Si su procesador es compatible con [x86_64](https://en.wikipedia.org/wiki/es:X86-64 "wikipedia:es:X86-64"), tendrá el flag `lm` en `/proc/cpuinfo`. Por ejemplo,

```
$ grep -w lm /proc/cpuinfo

```

Bajo Windows, utilizando el software gratuito [CPU-Z](http://www.cpuid.com/cpuz.php) para ayudarle a determinar si su CPU es compatible con 64-bit. Las CPU con instrucciones para AMD de «MD64» o solución de «EM64T» para Intel, deberían ser compatibles con las versiones x86_64 y sus paquetes binarios.

### ¿Voy a tener todos los paquetes en mi Arch de 32 bits?

La mayoría de los paquetes oficiales tienen versiones de 64 bits, aunque puede que tenga que habilitar el repositorio [multilib](/index.php/Multilib "Multilib") para ejecutar algunos programas de 32 bits. [Package Differences](https://www.archlinux.org/packages/differences/) enumera los pocos casos en los que paquetes de multilib difieren de las versiones nativas de 32 bits.

La única excepción son los paquetes de [AUR](/index.php/AUR "AUR") que solo tienen enumerado `'i686'`, pero incluso entonces pueden trabajar para 64 bits también. Basta añadir `'x86_64'` al [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

Como último recurso, siempre puede [instalar un sistema de 32-bit dentro del sistema de 64-bit](/index.php/Install_bundled_32-bit_system_in_64-bit_system "Install bundled 32-bit system in 64-bit system").

### ¿Por qué 64 bits?

Es más rápido en la mayoría de los casos, y como razón adicional también inherentemente más seguro debido a la naturaleza de [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization") en combinación con [Position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") y [NX Bit](https://en.wikipedia.org/wiki/NX_Bit "wikipedia:NX Bit") que no está disponible en el kernel de stock i686 debido a la deshabilitación de PAE. Si el equipo tiene más de 4 GB de RAM, solamente un sistema operativo de 64 bits será capaz de utilizarlo en su totalidad.

Los programadores también tienden cada vez más a preocuparse menos de 32 bits ("legacy") y tratarlo como «nuevas» CPU de x86 que soportan normalmente extensiones de 64-bit.

Hay muchas más razones que podríamos enumerar aquí para decirle que evite los 32 bits, razones relativas al kernel, al espacio de usuario y a los programas individuales que simplemente hacen mejor opción los 64 bits de momento.

### ¿Puedo construir paquetes de 32 bits para i686 dentro de Arch de 64-bit?

Sí. Puede utilizar el repositorio [multilib](/index.php/Multilib "Multilib") con un [makepkg config](/index.php/Makepkg#Build_32-bit_packages_on_a_64-bit_system "Makepkg") o [instalar un sistema de 32-bit dentro del sistema de 64-bit](/index.php/Install_bundled_32-bit_system_in_64-bit_system "Install bundled 32-bit system in 64-bit system").

### ¿Puedo cambiar de i686 a x86_64 sin reinstalar?

No. Todos los paquetes deben volver a ser instalados en la nueva arquitectura y realizar los cambios de configuración que sean necesarios. Sin embargo, no es necesario volver a particionar o formatear unidades de disco duro durante la instalación, por lo que es posible migrar todos los datos antiguos. Un hilo del foro ha sido creado [aquí](https://bbs.archlinux.org/viewtopic.php?id=64485) que describe las medidas adoptadas para migrar una instalación desde 32 a 64 bits sin perder ninguna configuración/ajustes/datos utilizando un gran disco duro externo.

Sin embargo, también puede iniciar el sistema con la ISO de instalación de 64 bits, montar el disco, hacer copia de seguridad de todo lo que puede desee mantener que no sea un binario de 32 bits (por ejemplo: `/home` & `/etc`), e instalar.

También es posible que desee leer acerca de [migrating between architectures](/index.php/Migrating_between_architectures "Migrating between architectures").