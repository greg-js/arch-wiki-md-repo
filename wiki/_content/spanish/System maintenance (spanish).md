Related articles

*   [General recommendations](/index.php/General_recommendations "General recommendations")

**Estado de la traducción:** este artículo es una versión traducida de [System maintenance](/index.php/System_maintenance "System maintenance"). Fecha de la última traducción/revisión: **2017-9-10**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=System_maintenance&diff=0&oldid=).

El mantenimiento regular del sistema es necesario para el correcto funcionamiento de Arch durante un período de tiempo. El mantenimiento oportuno es una práctica a la que muchos usuarios se acostumbran.

## Contents

*   [1 Compruebe si hay errores](#Compruebe_si_hay_errores)
    *   [1.1 Servicios systemd fallidos](#Servicios_systemd_fallidos)
    *   [1.2 Archivos de registro](#Archivos_de_registro)
*   [2 Copias de respaldo](#Copias_de_respaldo)
    *   [2.1 Archivos de configuración](#Archivos_de_configuraci.C3.B3n)
    *   [2.2 Lista de paquetes instalados](#Lista_de_paquetes_instalados)
    *   [2.3 Base de datos Pacman](#Base_de_datos_Pacman)
    *   [2.4 Encabezados LUKS](#Encabezados_LUKS)
    *   [2.5 Datos del sistema y del usuario](#Datos_del_sistema_y_del_usuario)
*   [3 Actualización del sistema](#Actualizaci.C3.B3n_del_sistema)
    *   [3.1 Leer antes de actualizar el sistema](#Leer_antes_de_actualizar_el_sistema)
    *   [3.2 Evite ciertos comandos de pacman](#Evite_ciertos_comandos_de_pacman)
    *   [3.3 Las actualizaciones parciales no son compatibles](#Las_actualizaciones_parciales_no_son_compatibles)
    *   [3.4 Actuar sobre las alertas durante una actualización](#Actuar_sobre_las_alertas_durante_una_actualizaci.C3.B3n)
    *   [3.5 Trate rápidamente con nuevos archivos de configuración](#Trate_r.C3.A1pidamente_con_nuevos_archivos_de_configuraci.C3.B3n)
    *   [3.6 Revertir actualizaciones fallidas](#Revertir_actualizaciones_fallidas)
*   [4 Utilice el gestor de paquetes para instalar el software](#Utilice_el_gestor_de_paquetes_para_instalar_el_software)
    *   [4.1 Elija los controladores de código abierto](#Elija_los_controladores_de_c.C3.B3digo_abierto)
    *   [4.2 Tenga cuidado con los paquetes no oficiales](#Tenga_cuidado_con_los_paquetes_no_oficiales)
    *   [4.3 Actualizar la lista de réplicas](#Actualizar_la_lista_de_r.C3.A9plicas)
*   [5 Limpiar los archivos del sistema](#Limpiar_los_archivos_del_sistema)
    *   [5.1 Caché del paquetes](#Cach.C3.A9_del_paquetes)
    *   [5.2 Paquetes no utilizados (huérfanos)](#Paquetes_no_utilizados_.28hu.C3.A9rfanos.29)
    *   [5.3 Archivos antiguos de configuración](#Archivos_antiguos_de_configuraci.C3.B3n)
    *   [5.4 Enlaces simbólicos rotos](#Enlaces_simb.C3.B3licos_rotos)
*   [6 Consejos y trucos](#Consejos_y_trucos)
    *   [6.1 Usar paquetes de software probados](#Usar_paquetes_de_software_probados)
    *   [6.2 Instalar el paquete linux-lts](#Instalar_el_paquete_linux-lts)
*   [7 Ver también](#Ver_tambi.C3.A9n)

## Compruebe si hay errores

### Servicios systemd fallidos

Compruebe si los servicios systemd han entrado en un estado fallido:

```
 $ systemctl --failed

```

Consulte [Systemd#Analyzing the system state](/index.php/Systemd#Analyzing_the_system_state "Systemd") para obtener más información.

### Archivos de registro

Busque errores en los archivos de registro ubicados en `/var/log`, así como errores de alta prioridad en la registro periódico systemd:

```
 # journalctl -p 3 -xb

```

Consulte [Systemd#Journal](/index.php/Systemd#Journal "Systemd") para obtener más información. Consulte [Xorg#Troubleshooting](/index.php/Xorg#Troubleshooting "Xorg") para obtener información sobre dónde y cómo [Xorg](/index.php/Xorg "Xorg") registra errores.

## Copias de respaldo

Cree copias de seguridad de datos importantes a intervalos regulares. Consulte [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") para encontrar muchas aplicaciones alternativas que pueden adaptarse mejor a su caso. Ver [Category:System recovery](/index.php/Category:System_recovery "Category:System recovery") para otros artículos de interés.

Las copias de seguridad pueden automatizarse con [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

### Archivos de configuración

Antes de editar cualquier archivo de configuración, cree una copia de seguridad para que pueda volver a una versión anterior en caso de problemas. Editores como [vim](/index.php/Vim "Vim") y [emacs](/index.php/Emacs "Emacs") pueden hacer esto automáticamente, así como herramientas como [etckeeper](/index.php/Etckeeper "Etckeeper") que mantienen el directorio `/etc` en un sistema de control de versiones (VCS); Vea el [dotfiles#Version control](/index.php/Dotfiles#Version_control "Dotfiles") para más información.

### Lista de paquetes instalados

Mantenga una lista de todos los paquetes instalados, de modo que si una re-instalación completa es inevitable, es más fácil volver a crear el entorno original.

Consulte los consejos de [Pacman tips#List of installed packages](/index.php/Pacman_tips#List_of_installed_packages "Pacman tips") para obtener más detalles.

### Base de datos Pacman

Consulte las sugerencias de [Pacman tips#Back-up the pacman database](/index.php/Pacman_tips#Back-up_the_pacman_database "Pacman tips").

### Encabezados LUKS

Puede tener sentido revisar y sincronizar periódicamente las copias de seguridad de encabezados de partición encriptada LUKS, especialmente si se han revocado frases de acceso. Véase [Dm-crypt/Device encryption#Backup and restore](/index.php/Dm-crypt/Device_encryption#Backup_and_restore "Dm-crypt/Device encryption").

### Datos del sistema y del usuario

Consulte Copia de seguridad del sistema [System backup](/index.php/System_backup "System backup").

## Actualización del sistema

Se recomienda realizar actualizaciones completas del sistema con regularidad a través de [Pacman#Upgrading packages](/index.php/Pacman#Upgrading_packages "Pacman"), para disfrutar de las últimas correcciones de errores y actualizaciones de seguridad, y también para evitar tener que lidiar con demasiadas actualizaciones de paquetes que requieren intervención manual de una sola vez. Cuando se solicita apoyo de la comunidad, generalmente se asumirá que el sistema está actualizado.

Asegúrese de tener un medio de instalación de Arch Linux en otro CD/USB "live" para que pueda rescatar fácilmente su sistema si hay algún problema después de actualizarlo. Si está ejecutando Arch en un entorno de producción o no puede permitirse el tiempo de inactividad por cualquier razón, pruebe primero los cambios en los archivos de configuración, así como las actualizaciones de los paquetes de software, en un sistema duplicado no crítico. Luego, si no surgen problemas, implemente los cambios en el sistema de producción.

Si el sistema tiene paquetes de [AUR](/index.php/AUR "AUR"), actualice cuidadosamente todos ellos.

*Pacman* es una potente herramienta de gestión de paquetes, pero no intenta manejar todos los casos posibles. Los usuarios deben ser vigilantes y asumir la responsabilidad de mantener su propio sistema.

### Leer antes de actualizar el sistema

Antes de actualizar, se espera que los usuarios visiten [Arch Linux home page](https://www.archlinux.org/) para ver las últimas noticias o, alternativamente, suscribirse al [RSS feed](https://www.archlinux.org/feeds/news/), las listas de correo [arch-announce mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) o seguir [@archlinux](https://twitter.com/archlinux) en Twitter. Cuando las actualizaciones requieren intervención del usuario fuera de lo común (más de lo que se puede manejar simplemente siguiendo las instrucciones dadas por *pacman*), se realizará una publicación de noticias apropiada.

Antes de actualizar un software fundamental (como el [kernel](/index.php/Kernel "Kernel"), [xorg](/index.php/Xorg "Xorg"), [systemd](/index.php/Systemd "Systemd") o [glibc](https://www.archlinux.org/packages/?name=glibc) ) a una nueva versión, revise el [forum](https://bbs.archlinux.org/) apropiado para ver si ha habido problemas informados.

Los usuarios también deben ser conscientes de que la actualización de paquetes puede plantear problemas **inesperados** que podrían requerir una intervención inmediata; por lo tanto, se desaconseja actualizar un sistema estable poco antes de que sea necesario para llevar a cabo una tarea importante. Es aconsejable antes de actualizar el sistema, esperar cuando se tenga tiempo suficiente para poder hacer frente a posibles problemas posteriores a la actualización.

### Evite ciertos comandos de pacman

Evite realizar [actualizaciones parciales](#Las_actualizaciones_parciales_no_son_compatibles). En otras palabras, nunca ejecute `pacman -Sy`; en su lugar, siempre use `pacman -Syu`.

Evite usar la opción `--force` con pacman, **especialmente** en comandos como `pacman -Syu --force` implica más de un paquete. La opción `--force` ignora los conflictos de archivos e incluso puede causar la pérdida de archivos cuando los archivos son reubicados entre diferentes paquetes. En un sistema correctamente mantenido, sólo se debe utilizar cuando se recomienda explícitamente por los desarrolladores de Arch (consulte [#Leer antes de actualizar el sistema](#Leer_antes_de_actualizar_el_sistema).

Evite usar la opción `-d` con pacman. `pacman -Rdd *package*` omite las verificaciones de dependencia durante la eliminación del paquete. Como resultado, un paquete que proporciona una dependencia crítica podría ser eliminado, resultando en una falla del sistema.

### Las actualizaciones parciales no son compatibles

Arch Linux es una distribución [rolling release](https://en.wikipedia.org/wiki/rolling_release "wikipedia:rolling release"). Esto significa que cuando las nuevas versiones de la [library](https://en.wikipedia.org/wiki/Library_(computing) "wikipedia:Library (computing)") se envían a los repositorios, los [developers](https://www.archlinux.org/people/developers/) y [Trusted Users](/index.php/Trusted_Users "Trusted Users") reconstruyen todos los paquetes de los repositorios que necesitan ser reconstruidos en contra de las bibliotecas. Por ejemplo, si dos paquetes dependen de la misma biblioteca, actualizar sólo un paquete también podría actualizar la biblioteca (como dependencia), lo que podría romper el otro paquete que depende de una versión anterior de la biblioteca.

Es por eso que las actualizaciones parciales **no son compatibles**. No utilice `pacman -Sy *package*` o cualquier equivalente, como `pacman -Sy` seguido de `pacman -S *package*`. Actualice **siempre** (con `pacman -Syu`) antes de instalar un paquete. Tenga mucho cuidado al usar `IgnorePkg` e `IgnoreGroup` por la misma razón. Si el sistema tiene paquetes instalados localmente (como paquetes [AUR](/index.php/AUR "AUR")), los usuarios tendrán que reconstruirlos cuando sus dependencias reciban una advertencia [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname") (bumps).

Si se ha creado un escenario de actualización parcial y se rompen los binarios porque no pueden encontrar las bibliotecas a las que están vinculadas, **no "solucione" el problema simplemente mediante enlaces simbólicos**. Las bibliotecas reciben advertencia [soname](https://en.wikipedia.org/wiki/soname "wikipedia:soname")(bumps) cuando **no son compatibles con versiones anteriores**. Simplemente el comando  `pacman -Syu` hacia un sistema espejo correctamente sincronizado solucionará el problema mientras el *pacman* no esté roto.

El scripts bash de chequeo*checkupdates*, incluido con el paquete pacman, proporcionan una forma segura de comprobar las actualizaciones de los paquetes instalados sin ejecutar una actualización del sistema al mismo tiempo.

### Actuar sobre las alertas durante una actualización

Al actualizar el sistema, asegúrese de prestar atención a los avisos de alerta proporcionados por [pacman](/index.php/Pacman "Pacman"). Si alguna acción adicional es requerida por el usuario, encárguese de ello cuidadosamente de inmediato. Si una alerta pacman es confusa, busque en los foros y las publicaciones recientes para obtener instrucciones más detalladas.

### Trate rápidamente con nuevos archivos de configuración

Cuando se invoca pacman, los archivos .`.pacnew` y `.pacsave` pueden crearse. Pacman proporciona aviso cuando esto sucede y los usuarios deben tratar con estos archivos con prontitud. Los usuarios son remitidos [Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files") wiki para obtener instrucciones detalladas.

Además, piense en otros archivos de configuración que puede haber copiado o creado. Si un paquete tiene una configuración de ejemplo que ha copiado en su directorio principal, compruebe si se ha creado un nuevo.

### Revertir actualizaciones fallidas

Si se espera que una actualización de paquete cause problemas, los empaquetadores se asegurarán de que pacman muestre un mensaje apropiado cuando se actualice el paquete. Si experimenta problemas después de una actualización, compruebe la salida de pacman consultando `/var/log/pacman.log`.

**Sugerencia:**  Puede utilizar un visor de registros como [wat-git](https://aur.archlinux.org/packages/wat-git/) para buscar en los registros de pacman.

En este punto, sólo después de asegurarse de que no hay información disponible a través de pacman, no hay noticias relativas en [https://www.archlinux.org/](https://www.archlinux.org/), y no hay posts del foro con respecto a la actualización, considere buscar ayuda en el [forum](https://bbs.archlinux.org), además de en los canales [IRC](/index.php/IRC "IRC"), o [downgrading](/index.php/Downgrading "Downgrading") el paquete ofensivo.

## Utilice el gestor de paquetes para instalar el software

[Pacman](/index.php/Pacman "Pacman") hace un trabajo mucho mejor que usted en el registro de archivos. Si instala las cosas manualmente, tarde o temprano *olvidará* lo que hizo, olvidará dónde instaló, instalará software conflictivo, lo instalará en ubicaciones incorrectas, etc.

*   Instale paquetes de los repositorios oficiales utilizando el método en la sección [Pacman#Installing packages](/index.php/Pacman#Installing_packages "Pacman").

*   Si el programa que desea no está disponible, compruebe si alguien ha creado un paquete en la [AUR](/index.php/AUR "AUR"). Siga el método en ese artículo para la instalación.

*   Por último, si el programa que desea no está en los repositorios oficiales o en el AUR, aprenda a [create a package](/index.php/Create_a_package "Create a package") para él.

Para limpiar los archivos instalados incorrectamente, vea [Pacman/Tips and tricks#Identify files not owned by any package](/index.php/Pacman/Tips_and_tricks#Identify_files_not_owned_by_any_package "Pacman/Tips and tricks").

### Elija los controladores de código abierto

Intente instalar siempre los controladores de código abierto antes de recurrir a controladores propietarios. La mayoría de las veces, los controladores de código abierto son más estables y fiables que los controladores propietarios. Los errores del controlador de código abierto se solucionan con más facilidad y rapidez. Mientras que los controladores propietarios pueden ofrecer más características y capacidades, todo ello en contra de la estabilidad. Para evitar este dilema, intente elegir los componentes de hardware conocidos por tener compatibilidad con el controlador de código abierto maduro con funciones completas. La información sobre el hardware con controladores Linux de código abierto está disponible en [linux-drivers.org](http://www.linux-drivers.org/).

### Tenga cuidado con los paquetes no oficiales

Use con precaución los paquetes de [AUR](/index.php/AUR "AUR") o un repositorio de usuarios no oficial [unofficial user repository](/index.php/Unofficial_user_repository "Unofficial user repository"). La mayoría son suministrados por usuarios regulares y por lo tanto pueden no tener los mismos estándares que los de los repositorios oficiales. Tenga cuidado con los [AUR helpers](/index.php/AUR_helpers "AUR helpers") que automatizan la instalación de paquetes de AUR. **Siempre** revise PKGBUILDs por precaución y signos de error o código malicioso antes de construir y / o instalar el paquete.

Para simplificar el mantenimiento, limite la cantidad de paquetes no oficiales usados. Hacer controles periódicos de los que están en uso real, y eliminar (o reemplazar con sus homólogos oficiales) cualquier otro. Consulte [pacman/Tips and tricks#Maintenance](/index.php/Pacman/Tips_and_tricks#Maintenance "Pacman/Tips and tricks") para comandos útiles.

### Actualizar la lista de réplicas

Actualice la lista de espejos de pacman, ya que la calidad de los espejos puede variar con el tiempo, y algunos podrían quedar sin conexión o su velocidad de descarga podría degradarse. Vea los [mirrors](/index.php/Mirrors "Mirrors") para más detalles.

## Limpiar los archivos del sistema

Al buscar archivos para eliminar, es importante encontrar los archivos que ocupan más espacio en disco. Los programas que ayudan con esto se encuentran en:

*   [List of applications#Disk usage display](/index.php/List_of_applications#Disk_usage_display "List of applications") Visualización del uso del disco .
*   [List of applications#Disk cleaning](/index.php/List_of_applications#Disk_cleaning "List of applications") Limpieza del disco .

### Caché del paquetes

Elimine archivos `.pkg` no deseados de `/var/cache/pacman/pkg/` para liberar espacio en disco.

Consulte [Pacman#Cleaning the package cache]] para obtener más información.

### Paquetes no utilizados (huérfanos)

Retire los paquetes no utilizados del sistema para liberar espacio en disco y simplificar el mantenimiento. Ver [Pacman/Tips and tricks#Removing unused packages (orphans)](/index.php/Pacman/Tips_and_tricks#Removing_unused_packages_.28orphans.29 "Pacman/Tips and tricks") para más detalles.

### Archivos antiguos de configuración

Los archivos de configuración antiguos pueden entrar en conflicto con las versiones de software más recientes o corromperse con el tiempo. Elimine las configuraciones innecesarias periódicamente, en particular en su carpeta de inicio y `~/.config`. Por razones similares, tenga cuidado al compartir carpetas de inicio entre instalaciones.

Busque las siguientes carpetas:

*   `~/.config/` -- donde las aplicaciones guardan su configuración
*   `~/.cache/` -- el caché de algunos programas puede crecer en tamaño
*   `~/.local/share/` -- los archivos antiguos pueden estar ahí

Consulte la ayuda [XDG Base Directory support](/index.php/XDG_Base_Directory_support "XDG Base Directory support") para obtener más información.

Para mantener el directorio personal limpio de archivos temporales creados en el lugar incorrecto, es una buena idea administrar una lista de archivos no deseados y eliminarlos regularmente, por ejemplo con [rmshit.py](https://github.com/lahwaacz/Scripts/blob/master/rmshit.py).

[rmlint](https://www.archlinux.org/packages/?name=rmlint) se puede usar para encontrar y opcionalmente eliminar archivos duplicados, archivos vacíos, directorios vacíos recursivos y enlaces simbólicos rotos.

### Enlaces simbólicos rotos

Los enlaces simbólicos viejos y rotos podrían estar todo de su sistema; usted debe eliminarlos. Ejemplos para lograr esto se pueden encontrar [here](https://unix.stackexchange.com/questions/34248/how-can-i-find-broken-symlinks) y [here](http://www.commandlinefu.com/commands/view/8260/find-broken-symlinks).

Para listar rápidamente todos los enlaces simbólicos rotos de su sistema, utilice:

```
 # find -xtype l -print

```

A continuación, inspeccionar y eliminar entradas innecesarias de esta lista.

## Consejos y trucos

Los siguientes consejos generalmente no son necesarios, pero ciertos usuarios pueden encontrarlos útiles.

### Usar paquetes de software probados

Los lanzamientos continuos de Arch pueden ser una bendición para los usuarios que quieran probar las últimas características y obtener actualizaciones de upstream tan pronto como sea posible, pero también pueden dificultar el mantenimiento del sistema. Para simplificar el mantenimiento y mejorar la estabilidad, intente evitar software de vanguardia e instale sólo software maduro y probado. Tales paquetes son menos propensos a recibir actualizaciones difíciles como cambios importantes de configuración o remociones de características. Preferir software que tiene una comunidad de desarrollo fuerte y activa, así como un número elevado de usuarios competentes, con el fin de simplificar el apoyo en caso de un problema.

Evite cualquier uso del repositorio de pruebas, incluso los paquetes individuales de las pruebas. Estos paquetes son experimentales y no son adecuados para un sistema estable. Del mismo modo, evitar los paquetes de desarrollo que se construyen directamente a partir de fuentes. Estos se encuentran generalmente en [AUR](/index.php/AUR "AUR"), con nombres como: "dev", "devel", "svn", "cvs", "git", etc.

### Instalar el paquete linux-lts

El paquete [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) es un paquete alternativo de kernel de Arch, y está disponible en el repositorio [core](/index.php/Core "Core"). Esta versión particular del kernel tiene soporte a largo plazo (LTS) desde upstream, incluyendo arreglos de seguridad y algunas funciones backports. Es útil si prefiere la estabilidad de las actualizaciones menos frecuentes del kernel o si desea un kernel de fallback en caso de que una nueva versión del kernel cause problemas.

Para que esté disponible como una opción de arranque, necesitará actualizar el archivo de configuración de su cargador de arranque [bootloader](/index.php/Bootloader "Bootloader") para usar el kernel LTS y el disco ram: `vmlinuz-linux-lts` y `initramfs-linux-lts.img`.

## Ver también

*   [Arch News Bash Script](https://bbs.archlinux.org/viewtopic.php?id=146850)