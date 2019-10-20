**Estado de la traducción**
Este artículo es una traducción de [System maintenance](/index.php/System_maintenance "System maintenance"), revisada por última vez el **2019-10-14**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=System_maintenance&diff=0&oldid=585320) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [General recommendations (Español)](/index.php/General_recommendations_(Espa%C3%B1ol) "General recommendations (Español)")

Para el correcto funcionamiento de Arch durante un cierto periodo de tiempo es necesario el mantenimiento regular del sistema. El mantenimiento oportuno es una práctica a la que muchos usuarios se acostumbran.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Comprobar si hay errores](#Comprobar_si_hay_errores)
    *   [1.1 Servicios systemd fallidos](#Servicios_systemd_fallidos)
    *   [1.2 Archivos de registro](#Archivos_de_registro)
*   [2 Realizar copias de respaldo](#Realizar_copias_de_respaldo)
    *   [2.1 Archivos de configuración](#Archivos_de_configuración)
    *   [2.2 Lista de paquetes instalados](#Lista_de_paquetes_instalados)
    *   [2.3 Base de datos de pacman](#Base_de_datos_de_pacman)
    *   [2.4 Encabezados LUKS](#Encabezados_LUKS)
    *   [2.5 Datos del sistema y del usuario](#Datos_del_sistema_y_del_usuario)
*   [3 Actualizar el sistema](#Actualizar_el_sistema)
    *   [3.1 Leer antes de actualizar el sistema](#Leer_antes_de_actualizar_el_sistema)
    *   [3.2 Evitar ciertas órdenes de pacman](#Evitar_ciertas_órdenes_de_pacman)
    *   [3.3 Las actualizaciones parciales no son compatibles](#Las_actualizaciones_parciales_no_son_compatibles)
    *   [3.4 Avisos sobre las alertas durante una actualización](#Avisos_sobre_las_alertas_durante_una_actualización)
    *   [3.5 Atender con diligencia los nuevos archivos de configuración](#Atender_con_diligencia_los_nuevos_archivos_de_configuración)
    *   [3.6 Revertir actualizaciones rotas](#Revertir_actualizaciones_rotas)
    *   [3.7 Verificar paquetes huérfanos y descartados](#Verificar_paquetes_huérfanos_y_descartados)
*   [4 Utilizar el gestor de paquetes para instalar software](#Utilizar_el_gestor_de_paquetes_para_instalar_software)
    *   [4.1 Elegir controladores de código abierto](#Elegir_controladores_de_código_abierto)
    *   [4.2 Tenga cuidado con los paquetes no oficiales](#Tenga_cuidado_con_los_paquetes_no_oficiales)
    *   [4.3 Actualizar la lista de servidores de réplicas](#Actualizar_la_lista_de_servidores_de_réplicas)
*   [5 Limpiar archivos del sistema](#Limpiar_archivos_del_sistema)
    *   [5.1 Caché de paquetes](#Caché_de_paquetes)
    *   [5.2 Paquetes no utilizados (huérfanos)](#Paquetes_no_utilizados_(huérfanos))
    *   [5.3 Archivos de configuración antiguos](#Archivos_de_configuración_antiguos)
    *   [5.4 Enlaces simbólicos rotos](#Enlaces_simbólicos_rotos)
*   [6 Consejos y trucos](#Consejos_y_trucos)
    *   [6.1 Usar paquetes de software probado](#Usar_paquetes_de_software_probado)
    *   [6.2 Instalar el paquete linux-lts](#Instalar_el_paquete_linux-lts)
*   [7 Véase también](#Véase_también)

## Comprobar si hay errores

### Servicios systemd fallidos

Compruebe si los servicios systemd se encuentran en un estado fallido:

```
 $ systemctl --failed

```

Consulte [Systemd (Español)#Analizar el estado del sistema](/index.php/Systemd_(Espa%C3%B1ol)#Analizar_el_estado_del_sistema "Systemd (Español)") para obtener más información.

### Archivos de registro

Busque errores en los archivos de registro ubicados en `/var/log`, así como errores de alta prioridad en el journal de systemd:

```
 # journalctl -p 3 -xb

```

Consulte [Systemd (Español)/Journal (Español)](/index.php/Systemd_(Espa%C3%B1ol)/Journal_(Espa%C3%B1ol) "Systemd (Español)/Journal (Español)") para obtener más información. Consulte [Xorg (Español)#Solución de problemas](/index.php/Xorg_(Espa%C3%B1ol)#Solución_de_problemas "Xorg (Español)") para obtener información sobre dónde y cómo [Xorg (Español)](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)") registra errores.

## Realizar copias de respaldo

Cree copias de seguridad de datos importantes a intervalos regulares. Consulte [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") para encontrar muchas aplicaciones alternativas que pueden adaptarse mejor a su caso. Consulte [Category:System recovery (Español)](/index.php/Category:System_recovery_(Espa%C3%B1ol) "Category:System recovery (Español)") para otros artículos de interés.

Las copias de seguridad pueden automatizarse con [systemd (Español)/Timers (Español)](/index.php/Systemd_(Espa%C3%B1ol)/Timers_(Espa%C3%B1ol) "Systemd (Español)/Timers (Español)").

### Archivos de configuración

Antes de editar cualquier archivo de configuración, cree una copia de seguridad para que pueda volver a una versión anterior en caso de problemas. Editores como [vim (Español)](/index.php/Vim_(Espa%C3%B1ol) "Vim (Español)") y [emacs (Español)](/index.php/Emacs_(Espa%C3%B1ol) "Emacs (Español)") pueden hacer esto automáticamente, así como herramientas como [etckeeper (Español)](/index.php/Etckeeper_(Espa%C3%B1ol) "Etckeeper (Español)") que mantienen el directorio `/etc` en un sistema de control de versiones (VCS); vea el artículo [dotfiles#Tracking dotfiles directly with Git](/index.php/Dotfiles#Tracking_dotfiles_directly_with_Git "Dotfiles") para más información.

### Lista de paquetes instalados

Mantenga una lista de todos los paquetes instalados, de modo que si una re-instalación completa es inevitable, sea más fácil volver a crear el entorno original.

Consulte los consejos de [pacman (Español)/Tips and tricks (Español)#Lista de paquetes instalados](/index.php/Pacman_(Espa%C3%B1ol)/Tips_and_tricks_(Espa%C3%B1ol)#Lista_de_paquetes_instalados "Pacman (Español)/Tips and tricks (Español)") para obtener más detalles.

### Base de datos de pacman

Consulte las sugerencias de [pacman (Español)/Tips and tricks (Español)#Copia de seguridad de la base de datos de pacman](/index.php/Pacman_(Espa%C3%B1ol)/Tips_and_tricks_(Espa%C3%B1ol)#Copia_de_seguridad_de_la_base_de_datos_de_pacman "Pacman (Español)/Tips and tricks (Español)").

### Encabezados LUKS

Puede tener sentido revisar y sincronizar periódicamente las copias de seguridad de encabezados de partición encriptada LUKS, especialmente si se han revocado frases de acceso. Véase [dm-crypt (Español)/Device encryption (Español)#Copia de seguridad y restauración](/index.php/Dm-crypt_(Espa%C3%B1ol)/Device_encryption_(Espa%C3%B1ol)#Copia_de_seguridad_y_restauración "Dm-crypt (Español)/Device encryption (Español)").

### Datos del sistema y del usuario

Consulte [System backup (Español)](/index.php/System_backup_(Espa%C3%B1ol) "System backup (Español)").

## Actualizar el sistema

Se recomienda realizar actualizaciones completas del sistema con regularidad como se indica en [Pacman (Español)#Actualizar paquetes](/index.php/Pacman_(Espa%C3%B1ol)#Actualizar_paquetes "Pacman (Español)"), para disfrutar de las últimas correcciones de errores y actualizaciones de seguridad, y también para evitar tener que lidiar con demasiadas actualizaciones de paquetes que requieren intervención manual de una sola vez. Cuando se solicita apoyo de la comunidad, generalmente se asumirá que el sistema está actualizado.

Asegúrese de tener un medio de instalación de Arch Linux en otro CD/USB «live» para que pueda rescatar fácilmente su sistema si hay algún problema después de actualizarlo. Si está ejecutando Arch en un entorno de producción o no puede permitirse estar un tiempo inactivo por cualquier razón, pruebe primero los cambios en los archivos de configuración, así como las actualizaciones de los paquetes de software, en un sistema duplicado no crítico. Luego, si no surgen problemas, implemente los cambios en el sistema de producción.

Si el sistema tiene paquetes de [AUR (Español)](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"), actualice cuidadosamente todos ellos.

*Pacman* es una potente herramienta de gestión de paquetes, pero no intenta manejar todos los casos posibles. Los usuarios deben ser vigilantes y asumir la responsabilidad de mantener su propio sistema.

### Leer antes de actualizar el sistema

Antes de actualizar, se espera que los usuarios visiten la [página principal de Arch Linux](https://www.archlinux.org/) para ver las últimas noticias o, alternativamente, suscríbase al [RSS feed](https://www.archlinux.org/feeds/news/), las [listas de correo de arch-announce](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) o seguir [@archlinux](https://twitter.com/archlinux) en Twitter. Cuando las actualizaciones requieren intervención del usuario fuera de lo común (más de lo que se puede manejar simplemente siguiendo las instrucciones dadas por *pacman*), se realizará una publicación de noticias apropiada.

Antes de actualizar un software fundamental (como el [Kernel (Español)](/index.php/Kernel_(Espa%C3%B1ol) "Kernel (Español)"), [xorg (Español)](/index.php/Xorg_(Espa%C3%B1ol) "Xorg (Español)"), [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") o [glibc](https://www.archlinux.org/packages/?name=glibc)) a una nueva versión, revise el [forum](https://bbs.archlinux.org/) apropiado para ver si ha habido problemas informados.

Los usuarios también deben ser conscientes de que la actualización de paquetes puede plantear problemas **inesperados** que podrían requerir una intervención inmediata; por lo tanto, se desaconseja actualizar un sistema estable poco antes de que sea necesario para llevar a cabo una tarea importante. Es aconsejable antes de actualizar el sistema, esperar cuando se tenga tiempo suficiente para poder hacer frente a posibles problemas posteriores a la actualización.

### Evitar ciertas órdenes de pacman

Evite realizar [actualizaciones parciales](#Las_actualizaciones_parciales_no_son_compatibles). En otras palabras, nunca ejecute `pacman -Sy`; en su lugar, siempre use `pacman -Syu`.

En general, evite usar la opción `--overwrite` con pacman. La opción `--overwrite` toma un argumento que contiene un [glob](https://en.wikipedia.org/wiki/glob_(programming) "wikipedia:glob (programming)").Cuando se utiliza, pacman omitirá las comprobaciones de conflictos de archivos para archivos que coincidan con el glob. En un sistema mantenido adecuadamente, solo debe usarse cuando los desarrolladores de Arch lo recomienden explícitamente. Consulte la sección [#Leer antes de actualizar el sistema](#Leer_antes_de_actualizar_el_sistema).

Evite usar la opción `-d` con pacman. `pacman -Rdd *paquete*` omite las verificaciones de dependencia durante la eliminación del paquete. Como resultado, un paquete que proporciona una dependencia crítica podría ser eliminado, resultando en una falla del sistema.

### Las actualizaciones parciales no son compatibles

Arch Linux es una distribución [rolling release](https://en.wikipedia.org/wiki/es:Liberaci%C3%B3n_continua reconstruyen todos los paquetes de los repositorios que necesitan ser reconstruidos con esas bibliotecas. Por ejemplo, si dos paquetes dependen de la misma biblioteca, actualizar solo un paquete también podría actualizar la biblioteca (como dependencia), lo que podría romper el otro paquete que depende de una versión anterior de la biblioteca.

Es por eso que las actualizaciones parciales **no son compatibles**. No utilice `pacman -Sy *paquete*` o cualquier equivalente, como `pacman -Sy` seguido de `pacman -S *paquete*`. Actualice **siempre** (con `pacman -Syu`) antes de instalar un paquete. Tenga mucho cuidado al usar `IgnorePkg` e `IgnoreGroup` por la misma razón. Si el sistema tiene paquetes instalados localmente (como paquetes [AUR (Español)](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)")), los usuarios tendrán que reconstruirlos cuando sus dependencias reciban una advertencia [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") (bumps).

Si se ha creado un escenario de actualización parcial y se rompen los binarios porque no pueden encontrar las bibliotecas a las que están vinculadas, **no «solucione» el problema simplemente mediante enlaces simbólicos**. Las bibliotecas reciben advertencias [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname")(bumps) cuando **no son compatibles con versiones anteriores**. Simplemente la orden `pacman -Syu` conectada a un servidor de réplica correctamente sincronizado, solucionará el problema mientras *pacman* no esté roto.

El script de bash *checkupdates*, incluido con el paquete [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib), proporciona una forma segura de comprobar las actualizaciones de los paquetes instalados sin ejecutar una actualización del sistema al mismo tiempo.

### Avisos sobre las alertas durante una actualización

Al actualizar el sistema, asegúrese de prestar atención a los avisos de alerta proporcionados por [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)"). Si es requerida alguna acción adicional al usuario, encárguese de ello cuidadosamente de inmediato. Si una alerta pacman es confusa, busque en los foros y las publicaciones recientes para obtener instrucciones más detalladas.

### Atender con diligencia los nuevos archivos de configuración

Cuando se invoca pacman, pueden crearse archivos `.pacnew` y `.pacsave`. Pacman proporciona avisos cuando esto sucede y los usuarios deben tratar estos archivos con prontitud. Los usuarios son remitidos a la página de la wiki [Pacman (Español)/Pacnew and Pacsave (Español)](/index.php/Pacman_(Espa%C3%B1ol)/Pacnew_and_Pacsave_(Espa%C3%B1ol) "Pacman (Español)/Pacnew and Pacsave (Español)") para obtener instrucciones detalladas.

Además, piense en otros archivos de configuración que puede haber copiado o creado. Si un paquete tiene una configuración de ejemplo que ha copiado en su directorio principal, compruebe si se ha creado un nuevo.

### Revertir actualizaciones rotas

Si se espera/conoce que una actualización de paquete cause problemas, los empaquetadores se asegurarán de que pacman muestre un mensaje apropiado cuando se actualice el paquete. Si experimenta problemas después de una actualización, compruebe la salida de pacman consultando `/var/log/pacman.log`.

**Sugerencia:** puede utilizar un visor de registros como [wat-git](https://aur.archlinux.org/packages/wat-git/) para buscar en los registros de pacman.

En este punto, solo después de asegurarse de que no hay información disponible a través de pacman, no hay noticias relativas en [https://www.archlinux.org/](https://www.archlinux.org/), y no hay posts del foro con respecto a la actualización, considere buscar ayuda en el [forum](https://bbs.archlinux.org), además de en los canales [Arch IRC channels (Español)](/index.php/Arch_IRC_channels_(Espa%C3%B1ol) "Arch IRC channels (Español)"), o [Downgrading packages (Español)](/index.php/Downgrading_packages_(Espa%C3%B1ol) "Downgrading packages (Español)") el paquete ofensivo.

### Verificar paquetes huérfanos y descartados

Después de una actualización, es posible que pueda tener paquetes que ya no sean necesarios o que ya no estén en los repositorios oficiales

Utilice `pacman -Qtd` para verificar los paquetes que se instalaron como una dependencia, de modo que ningún otro paquete dependa de ellos ahora. Si todavía se necesita un paquete huérfano, se recomienda cambiar el motivo de instalación a explícito. En otro caso, si el paquete ya no es necesario, se puede eliminar.

Además, es posible que algunos paquetes ya no estén en los repositorios remotos, pero aún pueden estar en su sistema local. Para enumerar todos los paquetes foráneos, utilice `pacman -Qm`. Tenga en cuenta que esta lista incluirá paquetes que se hayan instalado manualmente (por ejemplo, desde [AUR (Español)](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)")). Para excluir paquetes que están (todavía) disponibles en AUR, use la herramienta [ancient-packages](https://aur.archlinux.org/packages/ancient-packages/).

## Utilizar el gestor de paquetes para instalar software

[Pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") hace un trabajo mucho mejor que usted en el registro de archivos. Si instala las cosas manualmente, tarde o temprano *olvidará* lo que hizo, olvidará dónde instaló, instalará software conflictivo, lo instalará en ubicaciones incorrectas, etc.

*   Instale paquetes de los repositorios oficiales utilizando el método de la sección [Pacman (Español)#Instalar paquetes](/index.php/Pacman_(Espa%C3%B1ol)#Instalar_paquetes "Pacman (Español)").

*   Si el programa que desea no está disponible, compruebe si alguien ha creado un paquete en la [AUR (Español)](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"). Siga el método en ese artículo para la instalación.

*   Por último, si el programa que desea no está en los repositorios oficiales o en AUR, aprenda a [crear un paquete](/index.php/Creating_packages_(Espa%C3%B1ol) "Creating packages (Español)") para ello.

Para limpiar los archivos instalados incorrectamente, vea [Pacman (Español)/Tips and tricks (Español)#Identificar archivos que no pertenecen a ningún paquete](/index.php/Pacman_(Espa%C3%B1ol)/Tips_and_tricks_(Espa%C3%B1ol)#Identificar_archivos_que_no_pertenecen_a_ningún_paquete "Pacman (Español)/Tips and tricks (Español)").

### Elegir controladores de código abierto

Intente instalar siempre los controladores de código abierto antes de recurrir a controladores propietarios. La mayoría de las veces, los controladores de código abierto son más estables y fiables que los controladores propietarios. Los errores del controlador de código abierto se solucionan con más facilidad y rapidez. Mientras que los controladores propietarios pueden ofrecer más características y capacidades, todo ello en contra de la estabilidad. Para evitar este dilema, intente elegir los componentes de hardware conocidos por tener compatibilidad con el controlador de código abierto maduro con funciones completas.

### Tenga cuidado con los paquetes no oficiales

Use con precaución los paquetes de [AUR (Español)](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") o un [repositorio de usuarios no oficial](/index.php/Unofficial_user_repository "Unofficial user repository"). La mayoría son suministrados por usuarios normales y por lo tanto pueden no tener los mismos estándares que los de los repositorios oficiales. Tenga cuidado con los [AUR helpers (Español)](/index.php/AUR_helpers_(Espa%C3%B1ol) "AUR helpers (Español)") que automatizan la instalación de paquetes de AUR. **Siempre** revise los PKGBUILDs por precaución y para encontrar signos de error o código malicioso antes de construir y/o instalar el paquete.

Para simplificar el mantenimiento, limite la cantidad de paquetes no oficiales usados. Hacer controles periódicos de los que están en uso real, y eliminar (o reemplazar con sus homólogos oficiales) cualquier otro. Consulte [pacman (Español)/Tips and tricks (Español)#Mantenimiento](/index.php/Pacman_(Espa%C3%B1ol)/Tips_and_tricks_(Espa%C3%B1ol)#Mantenimiento "Pacman (Español)/Tips and tricks (Español)") para órdenes útiles.

### Actualizar la lista de servidores de réplicas

Actualice la lista de servidores de réplicas de pacman, ya que la calidad de los espejos puede variar con el tiempo, y algunos podrían quedar sin conexión o su velocidad de descarga podría degradarse.

Consulte [mirrors (Español)](/index.php/Mirrors_(Espa%C3%B1ol) "Mirrors (Español)") para más detalles.

## Limpiar archivos del sistema

Al buscar archivos para eliminar, es importante encontrar los archivos que ocupan más espacio en disco. Los programas que ayudan con esto se encuentran en:

*   [List of applications#Disk usage display](/index.php/List_of_applications#Disk_usage_display "List of applications") (visualizar utilización del disco).
*   [List of applications#Disk cleaning](/index.php/List_of_applications#Disk_cleaning "List of applications") (limpiar el disco).

### Caché de paquetes

Elimine archivos `.pkg` no deseados de `/var/cache/pacman/pkg/` para liberar espacio en disco.

Consulte [Pacman (Español)#Limpiar la memoria caché de los paquetes](/index.php/Pacman_(Espa%C3%B1ol)#Limpiar_la_memoria_caché_de_los_paquetes "Pacman (Español)") para obtener más información.

### Paquetes no utilizados (huérfanos)

Retire los paquetes no utilizados del sistema para liberar espacio en disco y simplificar el mantenimiento.

Consulte [Pacman (Español)/Tips and tricks (Español)#Eliminación de paquetes no utilizados (huérfanos)](/index.php/Pacman_(Espa%C3%B1ol)/Tips_and_tricks_(Espa%C3%B1ol)#Eliminación_de_paquetes_no_utilizados_(huérfanos) "Pacman (Español)/Tips and tricks (Español)") para más detalles.

### Archivos de configuración antiguos

Los archivos de configuración antiguos pueden entrar en conflicto con las versiones de software más recientes o corromperse con el tiempo. Elimine las configuraciones innecesarias periódicamente, en particular en su carpeta de inicio y `~/.config`. Por razones similares, tenga cuidado al compartir carpetas de inicio entre instalaciones.

Busque las siguientes carpetas:

*   `~/.config/` -- donde las aplicaciones guardan su configuración
*   `~/.cache/` -- el caché de algunos programas puede crecer en tamaño
*   `~/.local/share/` -- los archivos antiguos pueden estar ahí

Consulte la ayuda [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support") para obtener más información.

Para mantener el directorio personal limpio de archivos temporales creados en el lugar incorrecto, es una buena idea administrar una lista de archivos no deseados y eliminarlos regularmente, por ejemplo con [rmshit.py](https://github.com/lahwaacz/Scripts/blob/master/rmshit.py).

[rmlint](https://www.archlinux.org/packages/?name=rmlint) se puede usar para encontrar y opcionalmente eliminar archivos duplicados, archivos vacíos, directorios vacíos recursivos y enlaces simbólicos rotos.

### Enlaces simbólicos rotos

Es posible que haya enlaces simbólicos viejos y rotos en su sistema; debería eliminarlos. Ejemplos para lograr esto se pueden encontrar [aquí](https://unix.stackexchange.com/questions/34248/how-can-i-find-broken-symlinks) y [aquí](http://www.commandlinefu.com/commands/view/8260/find-broken-symlinks).

Para listar rápidamente todos los enlaces simbólicos rotos de su sistema, utilice:

```
 # find -xtype l -print

```

A continuación, inspeccione y elimine las entradas innecesarias de dicha lista.

## Consejos y trucos

Los siguientes consejos generalmente no son necesarios, pero ciertos usuarios pueden encontrarlos útiles.

### Usar paquetes de software probado

Los lanzamientos continuos de Arch pueden ser una bendición para los usuarios que quieran probar las últimas características y obtener actualizaciones de upstream tan pronto como sea posible, pero también pueden dificultar el mantenimiento del sistema. Para simplificar el mantenimiento y mejorar la estabilidad, intente evitar software de vanguardia e instale solo software maduro y probado. Tales paquetes son menos propensos a recibir actualizaciones difíciles como cambios importantes de configuración o remociones de características. Preferir software que tiene una comunidad de desarrollo fuerte y activa, así como un número elevado de usuarios competentes, con el fin de simplificar el apoyo en caso de un problema.

Evite cualquier uso del repositorio de pruebas, incluso los paquetes individuales de las pruebas. Estos paquetes son experimentales y no son adecuados para un sistema estable. Del mismo modo, evitar los paquetes de desarrollo que se construyen directamente a partir de fuentes. Estos se encuentran generalmente en [AUR (Español)](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"), con nombres como: «dev», «devel», «svn», «cvs», «git», etc.

### Instalar el paquete linux-lts

El paquete [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) es un paquete alternativo de kernel de Arch, y está disponible en el repositorio [core](/index.php/Core "Core"). Esta versión particular del kernel tiene soporte a largo plazo (LTS) desde upstream, incluyendo arreglos de seguridad y algunas funciones backports. Es útil si prefiere la estabilidad de las actualizaciones menos frecuentes del kernel o si desea un kernel de fallback en caso de que una nueva versión del kernel cause problemas.

Para que esté disponible como una opción de arranque, necesitará actualizar el archivo de configuración de su [cargador de arranque](/index.php/Bootloader "Bootloader") para usar el kernel LTS y el disco ram: `vmlinuz-linux-lts` y `initramfs-linux-lts.img`.

## Véase también

*   [Arch News Bash Script](https://bbs.archlinux.org/viewtopic.php?id=146850)