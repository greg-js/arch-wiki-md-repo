**Estado de la traducción**
Este artículo es una traducción de [Frequently asked questions](/index.php/Frequently_asked_questions "Frequently asked questions"), revisada por última vez el **2018-11-10**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Frequently_asked_questions&diff=0&oldid=547713) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Terminología en Arch](/index.php/Arch_Terminology_(Espa%C3%B1ol) "Arch Terminology (Español)")
*   [Preguntas frecuentes Arch User Repository](/index.php/Arch_User_Repository_(Espa%C3%B1ol)#FAQ "Arch User Repository (Español)")
*   [Solución de problemas](/index.php/General_troubleshooting_(Espa%C3%B1ol) "General troubleshooting (Español)")

## Contents

*   [1 General](#General)
    *   [1.1 ¿Qué es Arch Linux?](#¿Qué_es_Arch_Linux?)
    *   [1.2 ¿Por qué podría preferir no usar Arch?](#¿Por_qué_podría_preferir_no_usar_Arch?)
    *   [1.3 ¿Qué arquitecturas soporta Arch?](#¿Qué_arquitecturas_soporta_Arch?)
    *   [1.4 ¿Sigue Arch el estándar de jerarquía del sistema de archivos de la Fundación Linux (FHS)?](#¿Sigue_Arch_el_estándar_de_jerarquía_del_sistema_de_archivos_de_la_Fundación_Linux_(FHS)?)
    *   [1.5 Soy un completo principiante en GNU/Linux. ¿Debo usar Arch?](#Soy_un_completo_principiante_en_GNU/Linux._¿Debo_usar_Arch?)
    *   [1.6 ¿Arch está diseñado para ser utilizado como un servidor?, ¿un escritorio?, ¿una estación de trabajo](#¿Arch_está_diseñado_para_ser_utilizado_como_un_servidor?,_¿un_escritorio?,_¿una_estación_de_trabajo)
    *   [1.7 A mí me gusta Arch, excepto que el equipo de desarrollo debería implementar la *«funcionalidad X»*](#A_mí_me_gusta_Arch,_excepto_que_el_equipo_de_desarrollo_debería_implementar_la_«funcionalidad_X»)
    *   [1.8 ¿Para cuándo la nueva versión disponible?](#¿Para_cuándo_la_nueva_versión_disponible?)
    *   [1.9 ¿Es Arch Linux una distribución estable? ¿Tiene problemas con frecuencia?](#¿Es_Arch_Linux_una_distribución_estable?_¿Tiene_problemas_con_frecuencia?)
    *   [1.10 Arch necesita más prensa (es decir, publicidad)](#Arch_necesita_más_prensa_(es_decir,_publicidad))
    *   [1.11 Arch necesita más programadores](#Arch_necesita_más_programadores)
    *   [1.12 ¿Por qué va mi internet tan lento en comparación con otros sistemas operativos?](#¿Por_qué_va_mi_internet_tan_lento_en_comparación_con_otros_sistemas_operativos?)
    *   [1.13 ¿Por qué Arch está usando toda mi RAM?](#¿Por_qué_Arch_está_usando_toda_mi_RAM?)
    *   [1.14 ¿De dónde vino todo mi espacio libre?](#¿De_dónde_vino_todo_mi_espacio_libre?)
*   [2 Administración de paquetes](#Administración_de_paquetes)
    *   [2.1 He encontrado un error con el paquete X. ¿Qué debo hacer?](#He_encontrado_un_error_con_el_paquete_X._¿Qué_debo_hacer?)
    *   [2.2 Los paquetes que Arch deberían usar una única extensión. «.pkg.tar.gz» y «.pkg.tar.xz» son demasiado largos y/o confusos](#Los_paquetes_que_Arch_deberían_usar_una_única_extensión._«.pkg.tar.gz»_y_«.pkg.tar.xz»_son_demasiado_largos_y/o_confusos)
    *   [2.3 Pacman necesita una biblioteca para que otras aplicaciones puedan acceder fácilmente a la información del paquete](#Pacman_necesita_una_biblioteca_para_que_otras_aplicaciones_puedan_acceder_fácilmente_a_la_información_del_paquete)
    *   [2.4 Pacman necesita la *«característica X»*](#Pacman_necesita_la_«característica_X»)
    *   [2.5 Acabo de instalar el paquete X. ¿Cómo empiezo?](#Acabo_de_instalar_el_paquete_X._¿Cómo_empiezo?)
    *   [2.6 ¿Por qué hay solo una única versión de cada biblioteca compartida en los repositorios oficiales?](#¿Por_qué_hay_solo_una_única_versión_de_cada_biblioteca_compartida_en_los_repositorios_oficiales?)
    *   [2.7 ¿Qué pasa si ejecuto una actualización completa del sistema y hay una actualización de una biblioteca compartida, pero no para las aplicaciones que dependen de ella?](#¿Qué_pasa_si_ejecuto_una_actualización_completa_del_sistema_y_hay_una_actualización_de_una_biblioteca_compartida,_pero_no_para_las_aplicaciones_que_dependen_de_ella?)
    *   [2.8 ¿Es posible que haya una actualización del kernel principal, sin que se actualicen al mismo tiempo algunos de los paquetes de controladores?](#¿Es_posible_que_haya_una_actualización_del_kernel_principal,_sin_que_se_actualicen_al_mismo_tiempo_algunos_de_los_paquetes_de_controladores?)
    *   [2.9 ¿Qué hacer antes de actualizar?](#¿Qué_hacer_antes_de_actualizar?)
    *   [2.10 Un paquete de actualización fue liberado, pero pacman dice que el sistema está al día](#Un_paquete_de_actualización_fue_liberado,_pero_pacman_dice_que_el_sistema_está_al_día)
    *   [2.11 El proyecto *X* ha lanzado una nueva versión. ¿Cuánto tiempo demorará el paquete Arch para actualizar a esa nueva versión?](#El_proyecto_X_ha_lanzado_una_nueva_versión._¿Cuánto_tiempo_demorará_el_paquete_Arch_para_actualizar_a_esa_nueva_versión?)
    *   [2.12 Si necesito una versión anterior de una biblioteca instalada, ¿puedo simplemente enlazar a la versión más nueva?](#Si_necesito_una_versión_anterior_de_una_biblioteca_instalada,_¿puedo_simplemente_enlazar_a_la_versión_más_nueva?)
*   [3 Instalación](#Instalación)
    *   [3.1 Arch necesita un instalador. ¿Tal vez una instalación a través de GUI?](#Arch_necesita_un_instalador._¿Tal_vez_una_instalación_a_través_de_GUI?)
    *   [3.2 He instalado Arch, ¡y estoy en una shell! ¿Y ahora qué?](#He_instalado_Arch,_¡y_estoy_en_una_shell!_¿Y_ahora_qué?)
    *   [3.3 ¿Qué entorno de escritorio o gestor de ventanas debo usar?](#¿Qué_entorno_de_escritorio_o_gestor_de_ventanas_debo_usar?)
    *   [3.4 ¿Qué hace único a Arch respecto de otras distribuciones «minimalistas»?](#¿Qué_hace_único_a_Arch_respecto_de_otras_distribuciones_«minimalistas»?)
*   [4 64 bits](#64_bits)
    *   [4.1 ¿Cómo puedo saber si mi procesador es compatible con x86_64?](#¿Cómo_puedo_saber_si_mi_procesador_es_compatible_con_x86_64?)
    *   [4.2 ¿Por qué 64 bits?](#¿Por_qué_64_bits?)

## General

### ¿Qué es Arch Linux?

Véase el artículo [Arch Linux](/index.php/Arch_Linux_(Espa%C3%B1ol) "Arch Linux (Español)").

### ¿Por qué podría preferir no usar Arch?

Es posible que **no** desee usar Arch, si:

*   No tiene la habilidad/tiempo/ganas de usar una distribución GNU/Linux basada en *«hazlo tú mismo»*.
*   Necesita compatibilidad para una arquitectura que no sea x86_64.
*   Adopta una postura firme sobre el uso de una distribución que solo proporcione software libre, según la definición de GNU.
*   Cree que un sistema operativo debería configurarse por sí solo y funcionar una vez instalado, incluyendo por defecto un completo conjunto de software y entornos de escritorios en la instalación.
*   No quiere una distribución GNU/Linux de lanzamiento continuo.
*   Está satisfecho con su sistema operativo actual.

### ¿Qué arquitecturas soporta Arch?

Arch sólo soporta la arquitectura x86_64 (a veces llamado amd64). El soporte para i686 fue eliminado en noviembre de 2017 [[1]](https://www.archlinux.org/news/phasing-out-i686-support/).

Hay ports *no oficiales* para las arquitecturas i686 [[2]](https://archlinux32.org/) y [ARM](https://en.wikipedia.org/wiki/es:Arquitectura_ARM "wikipedia:es:Arquitectura ARM") [[3]](http://archlinuxarm.org/), cada uno con sus propios canales de la comunidad [[4]](http://ix.io/73w/irc)

### ¿Sigue Arch el estándar de jerarquía del sistema de archivos de la Fundación Linux (FHS)?

Arch Linux sigue la *jerarquía del sistema de archivos* para sistemas operativos que usan el administrador de servicios [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"). Véase [file-hierarchy(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file-hierarchy.7) para obtener una explicación de cada directorio junto con sus designaciones. En particular, `/bin`, `/sbin`, y `/usr/sbin` son enlaces simbólicos a `/usr/bin`, y `/lib` junto a `/lib64` son enlaces simbólicos a `/usr/lib`.

### Soy un completo principiante en GNU/Linux. ¿Debo usar Arch?

Si es un principiante y quiere usar Arch, tenga en cuanta únicamente que debe estar dispuesto a invertir un tiempo considerable en el aprendizaje de un nuevo sistema, así como aceptar el hecho de que Arch está diseñado fundamentalmente como una distribución 'hazlo tú mismo'. Es el usuario quien monta el sistema y controla en lo que se convertirá.

Antes de pedir ayuda, haga su propia investigación independiente buscando en Google, indagando en el foro (y leyendo el resto de estas preguntas frecuentes) y buscando en la excelente documentación proporcionada por la wiki de Arch. *Hay una razón por la que estos recursos se ponen a disposición del usuario en primer lugar.* Son muchos los *voluntarios* que dedican miles de horas compilando esta excelente información.

Véase también [Arch terminology#RTFM](/index.php/Arch_terminology#RTFM "Arch terminology") y la [guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)").

### ¿Arch está diseñado para ser utilizado como un servidor?, ¿un escritorio?, ¿una estación de trabajo

Arch no está diseñado para un tipo de uso particular. Más bien, está diseñado para un tipo particular de *usuario*. Arch está dirigido a usuarios competentes que disfrutan de su naturaleza 'hazlo tú mismo', y que además la aprovechan para moldear el sistema y satisfacer sus necesidades. Por lo tanto, moldeado según los propósitos del usuario, Arch se puede utilizar prácticamente para cualquier propósito. Muchos utilizan Arch tanto en equipos de sobremesa como en estaciones de trabajo. Y por supuesto, archlinux.org se ejecuta en Arch.

### A mí me gusta Arch, excepto que el equipo de desarrollo debería implementar la *«funcionalidad X»*

Involúcrese, contribuya con el código/solución a la comunidad. Si está bien considerado por el equipo de la comunidad y de desarrollo, tal vez sea integrado en Arch. La comunidad de Arch se nutre de la contribución y del intercambio de códigos y de herramientas.

### ¿Para cuándo la nueva versión disponible?

Los lanzamientos de Arch Linux son simplemente un entorno live para la instalación o el rescate, que incluyen el grupo [base](https://www.archlinux.org/groups/x86_64/base/) y unos pocos [paquetes adicionales](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both). Las versiones se liberan, por lo general, en la primera mitad de cada mes.

### ¿Es Arch Linux una distribución estable? ¿Tiene problemas con frecuencia?

Es *el usuario* el responsable en última instancia de la estabilidad de su propio sistema de lanzamiento continuo. El usuario decide el momento de actualizar, e integra los cambios necesarios cuando se requiere. Si el usuario accede a la comunidad en busca de ayuda, a menudo se le presta de manera oportuna. La diferencia entre Arch y otras distribuciones es que Arch es verdaderamente una distribución «do-it-yourself» ; las denuncias de ruptura son equivocadas e improductivas, cuando se debe a los cambios hechos a las aplicaciones por los desarrolladores de las mismas, sin ser responsabilidad del equipo que desarrolla Arch.

Véase el artículo [mantenimiento del sistema](/index.php/System_maintenance_(Espa%C3%B1ol) "System maintenance (Español)") para obtener consejos sobre cómo hacer que un sistema Arch Linux sea lo más estable posible.

### Arch necesita más prensa (es decir, publicidad)

Arch obtiene mucha publicidad tal como es. El objetivo de Arch Linux no es ser grande, sino más bien, orgánicamente, el crecimiento sostenible se produce de forma natural entre los usuarios destinatarios.

### Arch necesita más programadores

Posiblemente sea así. ¡No dude en ofrecer su tiempo! Visite los [foros](https://bbs.archlinux.org), [canales IRC](/index.php/IRC_channel "IRC channel") y [listas de correo](https://mailman.archlinux.org/mailman/listinfo/), y vea lo que hay pendiente por hacer. Comenzar a involucarse en el subforo de la *Community Contributions* es una buena manera de empezar.

### ¿Por qué va mi internet tan lento en comparación con otros sistemas operativos?

¿Está su red configurada correctamente? Véase el artículo sobre la [configuración de red](/index.php/Network_configuration_(Espa%C3%B1ol) "Network configuration (Español)").

También tenga en cuenta que Arch Linux no viene con [traffic shaping](https://en.wikipedia.org/wiki/Traffic_shaping como *Shorewall* o *Vuurmuur*; también hay scripts estáticos para [iproute2](https://www.archlinux.org/packages/?name=iproute2) (como por ejemplo [este derivado](http://serendipity.ruwenzori.net/index.php/2008/06/01/modified-wondershaper-for-better-voip-qos) de *Wondershaper*), que realiza precisamente esta tarea.

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

Es importante distinguir entre memoria «free» y «available». En el ejemplo anterior, un portátil con 2,8G de memoria RAM total parece estar utilizando la mayor parte de ella, y solo disponer de 283M de memoria libre. Sin embargo, 1,4G de la misma está en «buff/cache». Todavía hay 1,2G disponibles para iniciar nuevas aplicaciones, sin tener que acudir al espacio de intercambio. Véase `man free(1)` para obtener más detalles. ¿El resultado de todo esto? ¡Más rendimiento!

Véase [este maravilloso artículo](http://www.linuxjournal.com/article/2770) si ha despertado su curiosidad. También hay un sitio web dedicado a aclarar esta confusión: [http://www.linuxatemyram.com/](http://www.linuxatemyram.com/)

### ¿De dónde vino todo mi espacio libre?

La respuesta a esta pregunta depende de su sistema. Hay algunas [utilidades de disco](/index.php/List_of_applications_(Espa%C3%B1ol)#Programas_de_visualización_sobre_la_utilización_del_disco "List of applications (Español)") que pueden ayudarle a encontrar la respuesta.

## Administración de paquetes

Véase las páginas [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)"), [pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks_(Espa%C3%B1ol) "Pacman/Tips and tricks (Español)") y [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") para obtener más respuestas.

### He encontrado un error con el paquete X. ¿Qué debo hacer?

En primer lugar, es necesario averiguar si el error es algo que el equipo de Arch puede arreglar. A veces no lo es (por ejemplo, los fallos de Firefox pueden ser responsabilidad del equipo de Mozilla), lo que se llama un error *upstream*. Si se trata de un problema de Arch, hay una serie de pasos que puede seguir:

1.  busque en los foros para obtener información. Compruebe si alguien más lo ha notado;
2.  publique un [bug report](/index.php/Reporting_bug_guidelines "Reporting bug guidelines") con información detallada en [https://bugs.archlinux.org](https://bugs.archlinux.org);
3.  si lo considera oportuno, escriba un mensaje en el foro detallando el problema y el hecho de que ya lo ha informado. Esto ayudará a evitar que mucha gente avise del mismo error.

### Los paquetes que Arch deberían usar una única extensión. «.pkg.tar.gz» y «.pkg.tar.xz» son demasiado largos y/o confusos

Esto ha sido discutido en *Arch mailing list*. Algunos propusieron archivos con la extensión `.pac`. Por lo que se sabe actualmente, no existe un plan para cambiar la extensión de los paquetes. Como dijo Tobias Kieslich, uno de los desarrolladores de Arch: «*¡Un paquete **es** un tarball comprimido con* gzip *[xz]!. Y se puede abrir, investigar y manipular por cualquier aplicación que gestione los *.tar. Por otra parte, el mime-type es detectado automática y correctamente por la mayoría de las aplicaciones.*»

### Pacman necesita una biblioteca para que otras aplicaciones puedan acceder fácilmente a la información del paquete

pacman es el front-end para [libalpm](https://www.archlinux.org/pacman/libalpm.3.html), la biblioteca «Arch Linux Package Management». Esta biblioteca permite escribir otros front-ends alternativos, como un front-end gráfico.

### Pacman necesita la *«característica X»*

Si piensa que su idea tiene interés, entonces puede optar por debatirla en [pacman-dev](https://lists.archlinux.org//listinfo/pacman-dev/). También le recomendamos que compruebe [https://bugs.archlinux.org](https://bugs.archlinux.org) por si encuentra peticiones de características similares.

Sin embargo, la mejor manera de obtener una característica adicional a pacman o a Arch Linux es implementarla por si mismo. El parche o código puede o no ser admitido oficialmente, pero quizás otros apreciarán, probarán y contribuirán a su esfuerzo.

### Acabo de instalar el paquete X. ¿Cómo empiezo?

Si está utilizando un entorno de escritorio como [KDE](/index.php/KDE "KDE") o [GNOME](/index.php/GNOME_(Espa%C3%B1ol) "GNOME (Español)"), el programa automáticamente debería aparecer en el menú. Si está tratando de ejecutar el programa desde un terminal y no sabe el nombre del archivo binario, utilice:

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

### ¿Qué hacer antes de actualizar?

Siga la sección [actualización del sistema](/index.php/System_maintenance_(Espa%C3%B1ol)#Actualizaci.C3.B3n_del_sistema "System maintenance (Español)").

### Un paquete de actualización fue liberado, pero pacman dice que el sistema está al día

Los servidores de réplicas de *pacman* no se sincronizan inmediatamente. Puede tomar más de 24 horas antes de una actualización está disponible para usted. Las únicas opciones son que sea paciente o utilizar otro servidor de réplica. [MirrorStatus](https://www.archlinux.org/mirrors/status/) puede ayudar a identificar un servidor de réplica actualizado.

### El proyecto *X* ha lanzado una nueva versión. ¿Cuánto tiempo demorará el paquete Arch para actualizar a esa nueva versión?

Las actualizaciones del paquete se lanzarán cuando estén listas. La cantidad específica de tiempo puede ser tan breve como unas pocas horas después de que se libere una actualización menor de corrección de errores, hasta varias semanas después de la actualización de un gran grupo de paquetes. La cantidad de tiempo desde la nueva versión hasta que Arch libera un nuevo paquete depende de los paquetes específicos y la disponibilidad de los mantenedores del paquete. Además, algunos paquetes pasan algún tiempo en el repositorio [testing](/index.php/Testing "Testing"), por lo que esto puede prolongar el tiempo antes de que se actualice un paquete. Los [mantenedores](/index.php/Package_maintainer "Package maintainer") intentan trabajar lo más rápido posible para llevar actualizaciones estables a los repositorios. Si encuentra un paquete en los repositorios oficiales que está desactualizado, vaya al [sitio web del paquete](https://www.archlinux.org/packages/) y márquelo.

### Si necesito una versión anterior de una biblioteca instalada, ¿puedo simplemente enlazar a la versión más nueva?

Si tiene suerte, podría funcionar, por un tiempo. En cualquier caso, no es una solución adecuada, porque:

*   Las bibliotecas no cambian las versiones al azar - es probable que la API/ABI haya cambiado (posiblemente con bits eliminados), y es solo una cuestión de suerte si esos cambios afectan al uso.
*   El enlace simbólico no será rastreado por un administrador de paquetes. Los principiantes que intenten modificar de forma inmediata los archivos de la biblioteca del sistema, corren el mayor riesgo de realizar un cambio no deseado que no pueden diagnosticar/corregir, que el administrador de paquetes ayuda a evitar.
*   Una pequeña alternativa al volcado del archivo de biblioteca antiguo en el sistema de archivos, sin seguimiento, se olvidará, y no se detectarán/corregirán posibles errores de seguridad.

En su lugar, utilice/escriba por ejemplo un [paquete de compatibilidad](https://aur.archlinux.org/packages/?SeB=n&K=compat), que proporcione la versión de la biblioteca requerida.

## Instalación

### Arch necesita un instalador. ¿Tal vez una instalación a través de GUI?

Dado que la instalación no se produce con frecuencia (léase el resto de este artículo para saber más acerca de lo que significa *lanzamiento continuo*), no es una alta prioridad para los desarrolladores o usuarios. La [guía de instalación](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)") ha sido completamente actualizada para utilizar el método de línea de comandos.

### He instalado Arch, ¡y estoy en una shell! ¿Y ahora qué?

Véase las [recomendaciones generales](/index.php/General_recommendations_(Espa%C3%B1ol) "General recommendations (Español)").

### ¿Qué entorno de escritorio o gestor de ventanas debo usar?

Ya que hay una gran variedad disponibles, use el que más se ajuste a sus necesidades. Véase los artículos [Desktop environment (Español)](/index.php/Desktop_environment_(Espa%C3%B1ol) "Desktop environment (Español)") y [Window manager (Español)](/index.php/Window_manager_(Espa%C3%B1ol) "Window manager (Español)").

### ¿Qué hace único a Arch respecto de otras distribuciones «minimalistas»?

Véase [Arch compared to other distributions (Español)](/index.php/Arch_compared_to_other_distributions_(Espa%C3%B1ol) "Arch compared to other distributions (Español)").

## 64 bits

### ¿Cómo puedo saber si mi procesador es compatible con x86_64?

Si su procesador es compatible con [x86_64](https://en.wikipedia.org/wiki/es:X86-64 "wikipedia:es:X86-64"), tendrá el flag `lm` ([long mode](https://en.wikipedia.org/wiki/Long_mode "wikipedia:Long mode")) en `/proc/cpuinfo`. Por ejemplo,

```
$ grep -w lm /proc/cpuinfo

```

Bajo Windows, utilizando el software gratuito [CPU-Z](http://www.cpuid.com/cpuz.php) para ayudarle a determinar si su CPU es compatible con 64-bit. Las CPU con instrucciones para AMD de «MD64» o solución de «EM64T» para Intel, deberían ser compatibles con las versiones x86_64 y sus paquetes binarios.

### ¿Por qué 64 bits?

Es más rápido en la mayoría de los casos, y como razón adicional también inherentemente más seguro debido a la naturaleza de [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization") en combinación con [Position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") y [NX Bit](https://en.wikipedia.org/wiki/NX_Bit "wikipedia:NX Bit") que no está disponible en el kernel de stock i686 debido a la deshabilitación de PAE. Si el equipo tiene más de 4 GB de RAM, solamente un sistema operativo de 64 bits será capaz de utilizarlo en su totalidad.

Los programadores también tienden cada vez más a preocuparse menos de 32 bits ("legacy") y tratarlo como «nuevas» CPU de x86 que soportan normalmente extensiones de 64-bit.

Hay muchas más razones que podríamos enumerar aquí para decirle que evite los 32 bits, razones relativas al kernel, al espacio de usuario y a los programas individuales que simplemente hacen mejor opción los 64 bits de momento.