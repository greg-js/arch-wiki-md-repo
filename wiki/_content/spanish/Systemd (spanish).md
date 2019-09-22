**Estado de la traducción**
Este artículo es una traducción de [Systemd](/index.php/Systemd "Systemd"), revisada por última vez el **2018-12-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Systemd&diff=0&oldid=555139) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [systemd/User (Español)](/index.php/Systemd/User_(Espa%C3%B1ol) "Systemd/User (Español)")
*   [systemd/Timers (Español)](/index.php/Systemd/Timers_(Espa%C3%B1ol) "Systemd/Timers (Español)")
*   [systemd FAQ (Español)](/index.php/Systemd_FAQ_(Espa%C3%B1ol) "Systemd FAQ (Español)")
*   [init](/index.php/Init "Init")
*   [Daemons (Español)](/index.php/Daemons_(Espa%C3%B1ol) "Daemons (Español)")
*   [udev (Español)](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)")
*   [Improving performance/Boot process (Español)](/index.php/Improving_performance/Boot_process_(Espa%C3%B1ol) "Improving performance/Boot process (Español)")
*   [Allow users to shutdown (Español)](/index.php/Allow_users_to_shutdown_(Espa%C3%B1ol) "Allow users to shutdown (Español)")

De la [página web del proyecto](http://freedesktop.org/wiki/Software/systemd):

	*systemd* es un conjunto de bloques básicos de compilación para un sistema Linux. Proporciona un gestor de sistemas y servicios que se ejecuta como PID 1 e inicia el resto del sistema. systemd proporciona una notable capacidad de paralelización, utiliza la activación de socket y [D-Bus](/index.php/D-Bus "D-Bus") para iniciar los servicios, permite el inicio de demonios bajo demanda, realiza un seguimiento de los procesos con el uso de los [grupos de control](/index.php/Cgroups "Cgroups") de Linux, mantiene los puntos montaje y servicios de montaje automático e implementa un elaborado sistema de gestión de dependencias basado en un control lógico de los servicios. systemd es compatible con los scripts de inicialización de SysV y LSB y funciona como un reemplazo de sysvinit. Otras partes incluyen un demonio de registro, utilidades para controlar la configuración básica del sistema, tales como el nombre del equipo, la fecha, la configuración regional, la lista de usuarios registrados y contenedores y máquinas virtuales en ejecución, cuentas del sistema, directorios y configuraciones de tiempo de ejecución y demonios para gestionar una configuración de red simple, sincronización horaria de la red, reenvío de registros y resolución de nombres.

**Nota:** para una explicación detallada del motivo por el cual Arch cambió a *systemd*, consulte esta [publicación del foro](https://bbs.archlinux.org/viewtopic.php?pid=1149530#p1149530).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Utilización básica de systemctl](#Utilización_básica_de_systemctl)
    *   [1.1 Analizar el estado del sistema](#Analizar_el_estado_del_sistema)
    *   [1.2 Utilizar las unidades](#Utilizar_las_unidades)
    *   [1.3 Gestionar la energía](#Gestionar_la_energía)
*   [2 Escribir archivos de unidad](#Escribir_archivos_de_unidad)
    *   [2.1 Manejar las dependencias](#Manejar_las_dependencias)
    *   [2.2 Tipos de servicios](#Tipos_de_servicios)
    *   [2.3 Modificar los archivos de unidad suministrados](#Modificar_los_archivos_de_unidad_suministrados)
        *   [2.3.1 Reemplazar los archivos de unidad](#Reemplazar_los_archivos_de_unidad)
        *   [2.3.2 Archivos insertados](#Archivos_insertados)
        *   [2.3.3 Volver a la versión del proveedor](#Volver_a_la_versión_del_proveedor)
        *   [2.3.4 Ejemplos](#Ejemplos)
*   [3 Targets](#Targets)
    *   [3.1 Conocer los targets presentes](#Conocer_los_targets_presentes)
    *   [3.2 Crear un target personalizado](#Crear_un_target_personalizado)
    *   [3.3 Correlación entre los niveles de ejecución de SysV y los targets de systemd](#Correlación_entre_los_niveles_de_ejecución_de_SysV_y_los_targets_de_systemd)
    *   [3.4 Cambiar el target vigente](#Cambiar_el_target_vigente)
    *   [3.5 Cambiar el target predeterminado para arrancar](#Cambiar_el_target_predeterminado_para_arrancar)
    *   [3.6 Orden de los target por defecto](#Orden_de_los_target_por_defecto)
*   [4 Archivos temporales](#Archivos_temporales)
*   [5 Temporizadores](#Temporizadores)
*   [6 Montaje](#Montaje)
    *   [6.1 Montaje automático de particiones GPT](#Montaje_automático_de_particiones_GPT)
*   [7 Consejos y trucos](#Consejos_y_trucos)
    *   [7.1 Ejecutar servicios después de que la conexión de red esté activa](#Ejecutar_servicios_después_de_que_la_conexión_de_red_esté_activa)
    *   [7.2 Activar las unidades instaladas por defecto](#Activar_las_unidades_instaladas_por_defecto)
    *   [7.3 Entornos seguros para probar aplicaciones](#Entornos_seguros_para_probar_aplicaciones)
*   [8 Solución de problemas](#Solución_de_problemas)
    *   [8.1 Investigar errores de systemd](#Investigar_errores_de_systemd)
    *   [8.2 Diagnosticar problemas de arranque](#Diagnosticar_problemas_de_arranque)
    *   [8.3 Diagnosticar un servicio](#Diagnosticar_un_servicio)
    *   [8.4 Apagar/reiniciar se hace terriblemente largo](#Apagar/reiniciar_se_hace_terriblemente_largo)
    *   [8.5 Los procesos de corta duración parecen no registrar ninguna salida](#Los_procesos_de_corta_duración_parecen_no_registrar_ninguna_salida)
    *   [8.6 El tiempo de arranque aumenta con el tiempo](#El_tiempo_de_arranque_aumenta_con_el_tiempo)
    *   [8.7 systemd-tmpfiles-setup.service no se inicia en el arranque](#systemd-tmpfiles-setup.service_no_se_inicia_en_el_arranque)
    *   [8.8 La versión de systemd impresa en el arranque no es la misma que la versión del paquete instalado](#La_versión_de_systemd_impresa_en_el_arranque_no_es_la_misma_que_la_versión_del_paquete_instalado)
    *   [8.9 Desactivar el modo de emergencia en la máquina remota](#Desactivar_el_modo_de_emergencia_en_la_máquina_remota)
*   [9 Véase también](#Véase_también)

## Utilización básica de systemctl

La principal orden usada para conocer y controlar *systemd* es *systemctl*. Algunos de los posibles usos son el examen del estado del sistema y la gestión del sistema o de los servicios. Consulte [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) para conocer más detalles.

**Sugerencia:**

*   puede utilizar las siguientes órdenes *systemctl* con el parámetro `-H *usario*@*host*` para controlar una instancia de systemd en una máquina remota. Esto utilizará [SSH](/index.php/OpenSSH_(Espa%C3%B1ol) "OpenSSH (Español)") para conectarse a la instancia *systemd* remota;
*   lo usuarios de [Plasma](/index.php/Plasma "Plasma") pueden instalar [systemd-kcm](https://aur.archlinux.org/packages/systemd-kcm/) como una interfaz gráfica para *systemctl*. Después de instalar el módulo se agregará a *Administración del sistema*.

### Analizar el estado del sistema

Para mostrar el **estado del sistema** utilice:

```
$ systemctl status

```

Para **listar unidades en ejecución**:

```
$ systemctl

```

o:

```
$ systemctl list-units

```

Para **listar unidades que han fallado**:

```
$ systemctl --failed

```

Los archivos de las unidades disponibles se pueden ver en `/usr/lib/systemd/system/` y `/etc/systemd/system/` (este último tiene prioridad). Puede ver un **listado de las unidades instaladas** con:

```
$ systemctl list-unit-files

```

### Utilizar las unidades

Las unidades pueden ser, por ejemplo, services (*.service*), mount points (*.mount*), devices (*.device*) o sockets (*.socket*).

Cuando se usa *systemctl*, por lo general, tiene que especificar el nombre completo de la unidad, incluyendo el sufijo, por ejemplo, `sshd.socket`. Sin embargo, hay unos pocos atajos cuando se especifica la unidad en las siguientes órdenes *systemctl*:

*   Si no se especifica el sufijo, systemctl asumirá que es *.service*. Por ejemplo, `netcfg` y `netcfg.service` se consideran equivalentes.
*   Los puntos de montaje se traducirán automáticamente en la correspondiente unidad *.mount*. Por ejemplo, si especifica `/home` será equivalente a `home.mount`.
*   Similar a los puntos de montaje, los dispositivos se traducen automáticamente en la correspondiente unidad *.device*, por lo tanto, la especificación `/dev/sda2` es equivalente a `dev-sda2.device`.

Véase [systemd.unit(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5) para más detalles.

**Nota:** algunos nombres de unidades contienen un signo `@` (por ejemplo, `name@*string*.service`): esto significa que son [instancias](http://0pointer.de/blog/projects/instances.html) de una unidad *plantilla*, cuyo nombre de archivo real no contiene la parte `*string* `(por ejemplo, `name@.service` ). `*string*` se denomina al *identificador de instancia*, y es similar a un argumento que se pasa a la unidad que sirve de plantilla cuando es llamada con el orden *systemctl*: en el archivo de unidad se sustituirá el especificador `%i`.

Para ser más precisos, *antes* de probar inicializar una instancia de unidad de plantilla `name@.suffix`, *systemd* buscará una unidad con el nombre del archivo `name@string.suffix` exacto, aunque por convención, tal «conflicto» ocurre raramente, es decir, la mayoría de los archivos de unidades que contienen un signo `@` son plantillas. Además, si se llama a una unidad de plantilla sin un identificador de instancia, simplemente fallará, ya que el especificador `%i` no puede ser sustituido.

**Sugerencia:** la mayoría de las siguientes órdenes también funcionan si se especifican varias unidades, vea [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) para más información.

**Activa** una unidad de inmediato:

```
# systemctl start *unidad*

```

**Detiene** una unidad de inmediato:

```
# systemctl stop *unidad*

```

**Reinicia** la unidad:

```
# systemctl restart *unidad*

```

Hace que una unidad **recargue** su configuración:

```
# systemctl reload *unidad*

```

Muestra el **estado** de una unidad, incluso si se está ejecutando o no:

```
$ systemctl status *unidad*

```

**Comprueba** si la unidad ya está activada o no:

```
$ systemctl is-enabled *unidad*

```

**Activa** una unidad para inicarse en el **arranque**:

```
# systemctl enable *unidad*

```

**Activa** una unidad para inicarse en el **arranque** y lo **inicia** inmediatamente:

```
# systemctl enable --now *unidad*

```

**Desactiva** el inicio automático durante el arranque:

```
# systemctl disable *unidad*

```

**Enmascara** una unidad para que sea imposible iniciarla (tanto de forma manual como de dependencia, lo que hace que el enmascaramiento sea peligroso):

```
# systemctl mask *unidad*

```

**Desenmascara** una unidad:

```
# systemctl unmask *unidad*

```

Muestre la **página del manual** asociada a una unidad (esto debe ser compatible con el archivo de la unidad):

```
 $ systemctl help *unidad*

```

**Recarga** la configuración de *systemd*, buscando **unidades nuevas o modificadas**:

**Nota:** esto no le pide a las unidades modificadas que vuelvan a cargar sus propias configuraciones. Vea el ejemplo `reload` de arriba.

```
# systemctl daemon-reload

```

### Gestionar la energía

[polkit](/index.php/Polkit "Polkit") es necesario para gestionar la energía. Si se encuentra en una sesión local de *systemd-logind* y ninguna otra sesión está activa, las órdenes siguientes funcionarán sin requerir privilegios de root. Si no es así (por ejemplo, debido a que otro usuario ha iniciado otra sesión tty), *systemd* automáticamente le requerirá la contraseña de root.

Apagado y reinicio del sistema:

```
$ systemctl reboot

```

Apagado del sistema:

```
$ systemctl poweroff

```

Suspensión del sistema:

```
$ systemctl suspend

```

Poner el sistema en hibernación:

```
$ systemctl hibernate

```

Poner el sistema en estado de reposo híbrido —*«hybrid-sleep»* — (o suspensión combinada —*«suspend-to-both»*—):

```
$ systemctl hybrid-sleep

```

## Escribir archivos de unidad

La sintaxis de los [archivos de unidad](http://www.freedesktop.org/software/systemd/man/systemd.unit.html) de *systemd* está inspirada en los archivos *.desktop* de la Especificación de Entrada del Escritorio XDG que a su vez están inspirados en los archivos *.ini* de Microsoft Windows. Los archivos de unidad se cargan desde varias ubicaciones (para ver la lista completa, ejecute `systemctl show --property=UnitPath`), pero los principales son (enumerados desde la prioridad más baja a la más alta):

*   `/usr/lib/systemd/system/`: unidades proporcionadas por los paquetes instalados.
*   `/etc/systemd/system/`: unidades instaladas por el administrador del sistema.

**Nota:**

*   Las rutas de carga son completamente diferentes cuando se ejecuta *systemd* en [momdo usuario](/index.php/Systemd/User#How_it_works "Systemd/User").
*   Los nombres de las unidades del sistema solo pueden contener caracteres alfanuméricos ASCII, guiones bajos y puntos. Todos los demás caracteres deben reemplazarse por escapes «\x2d» de estilo C, o emplear su semántica predefinida ('@','-'). Consulte [systemd.unit(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.unit.5) y [systemd-escape(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-escape.1) para obtener más información.

Mire las unidades instaladas por sus paquetes para obtener ejemplos, así como la [[sección de ejemplo anotada](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Examples) de [systemd.service(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.service.5).

**Sugerencia:** Los comentarios precedidos con `#`, también se pueden usar en archivos de unidad, pero solo en líneas nuevas. No utilice los comentarios al final de la línea después de los parámetros de *systemd* o la unidad no se activará.

### Manejar las dependencias

Con *systemd* las dependencias pueden ser resueltas diseñando la unidad correctamente. El caso más típico es que la unidad *A* requiere la unidad *B* para poder funcionar, por lo que esta última debe iniciarse antes que *A*. En ese caso, agregue `Requires=B` y `After=B` a la sección `[Unit]` de `A`. Si la dependencia es opcional agregue, en su lugar, `Wants=B` y `After=B`. Tenga en cuenta que `Wants=` y `Requires=` no incluyen `After=`, lo que significa que si `After=` no esté especificado, las dos unidades se iniciarán en paralelo.

Las dependencias se colocan normalmente en los archivos .service y no en los [#Targets](#Targets). Por ejemplo, `network.target` es llamado por cualquiera que sea el servicio que configure las interfaces de red, por lo tanto, la solicitud que hace después la propia unidad personalizada es suficiente, ya que `network.target` se inicia de todos modos.

### Tipos de servicios

Existen diferentes tipos de arranque a tener en cuenta cuando se escribe un archivo de servicio personalizado. Esto se configura mediante el parámetro `Type=` en la sección `[Service]`.

*   `Type=simple` (por defecto): *systemd* considera que el servicio debe iniciarse inmediatamente. El proceso no debe romperse. No utilice este tipo si otros servicios tienen que ser llamados por ese servicio, a menos que no sea activado por el socket.
*   `Type=forking`: *systemd* considera que el servicio debe ser iniciado antes que el proceso se rompa y el antecesor se haya terminado. Para los demonios clásicos use este tipo a menos que sepa que no es necesario, ya que la mayoría de los demonios usan doble bifurcación para indicar que están listos. Debe especificar también `PIDFile=` para que *systemd* puede realizar un seguimiento del proceso principal.
*   `Type=oneshot`: esto es útil para los scripts que hacen un solo trabajo y luego concluyen. Es posible que desee también establecer `RemainAfterExit=yes` de modo que *systemd* sigue considerando el servicio como activo después de que el proceso haya terminado.
*   `Type=notify`: igual que `Type=simple`, pero con la condición de que el demonio va a enviar una señal a *systemd* cuando esté listo. Esto requiere del código específico proporcionado por `libsystemd-daemon.so`.
*   `Type=dbus`: el servicio se considera listo cuando el `BusName` especificado aparece en el [bus](https://en.wikipedia.org/wiki/es:Bus_(inform%C3%A1tica) del sistema [DBus](https://en.wikipedia.org/wiki/es:D-Bus "wikipedia:es:D-Bus").
*   `Type=idle`: *systemd* retrasará la ejecución del binario del servicio hasta que se envíen todos los trabajos. Un comportamiento por cierto muy similar a `Type=simple`.

Consulte la página del manual [systemd.service(5)](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Type=) para obtener una explicación más detallada de los valores `Type`.

### Modificar los archivos de unidad suministrados

Para evitar conflictos con pacman, los archivos de unidad proporcionados por los paquetes no deben editarse directamente. Hay dos formas seguras de modificar una unidad sin tocar el archivo original: crear un nuevo archivo de unidad que [sobrescriba la unidad original](#Reemplazar_los_archivos_de_unidad) o crear [fragmentos para insertarlos](#Archivos_insertados) que se aplican sobre la unidad original. Para ambos métodos, debe volver a cargar la unidad posteriormente para que los cambios surtan efectos. Esto se puede hacer editando la unidad con `systemctl edit` (que recarga la unidad automáticamente) o recargando todas las unidades con:

```
# systemctl daemon-reload

```

**Sugerencia:**

*   Puede usar *systemd-delta* para ver qué archivos de la unidad se han sobrescrito o ampliado y qué se ha cambiado exactamente.
*   Utilice `systemctl cat *unidad*` para ver el contenido de un archivo de unidad y todos los fragmentos insertados asociados.

#### Reemplazar los archivos de unidad

Para reemplazar el archivo de unidad `/usr/lib/systemd/system/*unit*`, cree el archivo `/etc/systemd/system/*unit*` y *reactive* la unidad para actualizar los enlaces simbólicos:

```
# systemctl reenable *unidad*

```

Alternativamente, ejecute:

```
# systemctl edit --full *unidad*

```

Esto abre `/etc/systemd/system/*unit*` en su editor (copiando la versión instalada si aún no existe) y la vuelve a cargar automáticamente cuando termina de editar.

**Nota:** las unidades de reemplazo seguirán usándose incluso si pacman actualiza las unidades originales en el futuro. Este método hace que el mantenimiento del sistema sea más difícil y, por lo tanto, se prefiere el siguiente enfoque.

#### Archivos insertados

Para crear fragmentos de archivos para insertar en el archivo de unidad `/usr/lib/systemd/system/*unit*`, cree el directorio `/etc/systemd/system/*unit*.d/` y coloque los archivos *.conf* allí para sobrescribir o agregar nuevas opciones. *systemd* analizará y aplicará estos archivos con preferencia a la unidad original.

La forma más fácil de hacer esto es ejecutar:

```
# systemctl edit *unidad*

```

Esto abre el archivo `/etc/systemd/system/*unit*.d/override.conf` en su editor de texto (creándolo si es necesario) y vuelve a cargar automáticamente la unidad cuando haya terminado de editarla.

**Nota:** no todas las claves se pueden anular con archivos de inserción. Por ejemplo, para cambiar `Conflicts=` [es necesario](https://lists.freedesktop.org/archives/systemd-devel/2017-June/038976.html) un archivo de reemplazo.

#### Volver a la versión del proveedor

Para revertir cualquier cambio en una unidad realizada utilizando `systemctl edit`, ejecute:

```
# systemctl revert *unidad*

```

#### Ejemplos

Por ejemplo, si simplemente desea agregar una dependencia adicional a una unidad, puede crear el siguiente archivo:

 `/etc/systemd/system/*unit*.d/customdependency.conf` 
```
[Unit]
Requires=*dependencia nueva*
After=*dependencia nueva*
```

Otro ejemplo, para reemplazar la directiva `ExecStart` para una unidad que no sea del tipo `oneshot`, cree el siguiente archivo:

 `/etc/systemd/system/*unit*.d/customexec.conf` 
```
[Service]
ExecStart=
ExecStart=*orden nueva*
```

Observe como `ExecStart` debe quedar límpio antes de volver a reasignarse [[1]](https://bugzilla.redhat.com/show_bug.cgi?id=756787#c9). Lo mismo se aplica a cada elemento que se puede especificar varias veces, por ejemplo `OnCalendar` para los temporizadores.

Un ejemplo más para reiniciar automáticamente un servicio:

 `/etc/systemd/system/*unit*.d/restart.conf` 
```
[Service]
Restart=always
RestartSec=30
```

## Targets

*systemd* utiliza *targets* (*«objetivos»*) que sirven a un propósito similar a los [runlevels](https://en.wikipedia.org/wiki/es:Nivel_de_ejecuci%C3%B3n "wikipedia:es:Nivel de ejecución") (*«niveles de ejecución»*), pero que tienen un comportamiento un poco diferente. Cada *target* se nomina, en lugar de numerarse, y está destinado a servir a un propósito específico con la posibilidad de realizar más de una acción al mismo tiempo. Algunos *targets* son activados heredando todos los servicios de otro *target* e implementando servicios adicionales. Como hay *targets* de *systemd* que imitan los runlevels de SystemVinit, es, por tanto, posible pasar de un *target* a otro utilizando la orden `telinit RUNLEVEL`.

### Conocer los targets presentes

La siguiente orden debe ser utilizada bajo *systemd*, en lugar de `runlevel`:

```
$ systemctl list-units --type=target

```

### Crear un target personalizado

Los niveles de ejecución (*«runlevels»*) que tenían un significado definido bajo sysvinit (es decir, 0, 1, 3, 5 y 6), tienen una correlación de 1:1 con un específico *target* de systemd. Desafortunadamente, no hay una buena manera de hacer lo mismo para los niveles de ejecución definidos por el usuario como son el 2 y el 4\. Si se hace uso de estos últimos, se sugiere dar un nuevo nombre al *target* de *systemd* como `/etc/systemd/system/*su target*` que tome como base uno de los runlevels existentes (vea `/usr/lib/systemd/system/graphical.target` como ejemplo), cree un directorio `/etc/systemd/system/*su target*.wants`, y haga un enlace a los servicios adicionales de `/usr/lib/systemd/system/` que desea activar.

### Correlación entre los niveles de ejecución de SysV y los targets de systemd

| Nivel de ejecución de SysV | Target de systemd | Notas |
| 0 | runlevel0.target, poweroff.target | Detiene el sistema. |
| 1, s, single | runlevel1.target, rescue.target | Modalidad de usuario único. |
| 2, 4 | runlevel2.target, runlevel4.target, multi-user.target | Definidos por el usuario/específico del sistio. Preconfigurados a 3. |
| 3 | runlevel3.target, multi-user.target | Multiusuario, no gráfica. Los usuarios, por lo general, pueden acceder a través de múltiples consolas o a través de la red. |
| 5 | runlevel5.target, graphical.target | Multiusuario, gráfica. Por lo general, tiene todos los servicios del nivel de ejecución 3, además de un inicio de sesión gráfica. |
| 6 | runlevel6.target, reboot.target | Reinicia el sistema. |
| emergency | emergency.target | Consola de emergencia. |

### Cambiar el target vigente

En *systemd* los targets quedan expuestos a través de «target units». Se pueden cambiar de esta manera:

```
# systemctl isolate graphical.target

```

Esto solo cambiará el target actual, y no tendrá ningún efecto sobre el siguiente arranque. Esto es equivalente a las órdenes `telinit 3` o `telinit 5` en Sysvinit.

### Cambiar el target predeterminado para arrancar

El target estándar es `default.target`, que es un enlace simbólico para `graphical.target`. Este se corresponde con el antiguo nivel de ejecución 5\.

Para verificar el target actual con *systemctl*, ejecute:

```
$ systemctl get-default

```

Para cambiar el target predeterminado para arrancar, cambie el enlace simbólico `default.target`. Con *systemctl*:

 `# systemctl set-default multi-user.target` 
```
Removed /etc/systemd/system/default.target.
Created symlink /etc/systemd/system/default.target -> /usr/lib/systemd/system/graphical.target.
```

Como alternativa, agregue uno de los siguientes [parámetros del kernel](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)") a su cargador de arranque:

*   `systemd.unit=multi-user.target` (que corresponde aproximadamente al anterior nivel de ejecución 3),
*   `systemd.unit=rescue.target` (que corresponde aproximadamente al anterior nivel de ejecución 1).

### Orden de los target por defecto

Systemd elige el `default.target` de acuerdo con el siguiente orden:

1.  El parámetro del kernel se muestra arriba
2.  Enlace simbólico de `/etc/systemd/system/default.target`
3.  Enlace simbólico de `/usr/lib/systemd/system/default.target`

## Archivos temporales

«*systemd-tmpfiles* crea, elimina y limpia archivos y directorios volátiles y temporales.» Lee los archivos de configuración en `/etc/tmpfiles.d/` y `/usr/lib/tmpfiles.d/` para descubrir qué acciones realizar. Los archivos de configuración del primer directorio tienen prioridad sobre los del último directorio.

Los archivos de configuración son proveídos normalmente junto con los archivos de servicio, y reciben su nombre en el estilo `/usr/lib/tmpfiles.d/*programa*.conf`. Por ejemplo, el demonio [Samba](/index.php/Samba "Samba") espera que el directorio `/run/samba` exista para obtener los permisos adecuados. Por tanto, el paquete [samba](https://www.archlinux.org/packages/?name=samba) viene con esta configuración:

 `/usr/lib/tmpfiles.d/samba.conf`  `D /run/samba 0755 root root` 

Los archivos de configuración también pueden ser usados para escribir en el arranque valores en ciertos archivos. Por ejemplo, si usa `/etc/rc.local` para dehabilitar la reactivación del sistema (*«wakeup»*) a través de dispositivos USB con la orden `echo USBE > /proc/acpi/wakeup`, se puede utilizar, en su lugar, el siguiente tmpfile:

 `/etc/tmpfiles.d/disable-usb-wake.conf` 
```
#    Path                  Mode UID  GID  Age Argument
w    /proc/acpi/wakeup     -    -    -    -   USBE
```

Consulte las páginas de los manuales [systemd-tmpfiles(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-tmpfiles.8) y [tmpfiles.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tmpfiles.d.5) para obtener más detalles.

**Nota:** este método puede no funcionar ajustando las opciones en `/sys` desde el momento en que el servicio `systemd-tmpfiles-setup` puede ejecutarse antes de que los módulos de los dispositivos adecuados se carguen. En este caso, se puede comprobar si el módulo tiene un parámetro para la opción que desea ajustar con `modinfo *modulo*` y establecer esta opción con un [archivo de configuraición en /etc/modprobe.d](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). De lo contrario, tendrá que escribir una [regla udev](/index.php/Udev#About_udev_rules "Udev") para establecer el atributo apropiado tan pronto como el dispositivo lo reclame.

## Temporizadores

Un temporizador es un archivo de configuración de unidad cuyo nombre termina en *.timer* y codifica información sobre un temporizador controlado y supervisado por *systemd*, para la activación basada en plazos de tiempo. Consulte [systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers").

**Nota:** los temporizadores pueden reemplazar la funcionalidad de [cron](/index.php/Cron "Cron") en gran medida. Consulte [systemd/Timers#As a cron replacement](/index.php/Systemd/Timers#As_a_cron_replacement "Systemd/Timers").

## Montaje

*systemd* se encarga de montar las particiones y los sistemas de archivos especificados en `/etc/fstab`. El script [systemd-fstab-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-fstab-generator.8) traduce todas las entradas presentes en `/etc/fstab` en unidades de systemd, esto se realiza en el momento del arranque y cada vez que se vuelve a cargar la configuración del gestor del sistema.

*systemd* extiende las habituales capacidades de [fstab](/index.php/Fstab "Fstab") y ofrece opciones de montaje adicionales. Esto afecta a las dependencias de la unidad de montaje; por ejemplo, se puede garantizar que un montaje se realice solo una vez que la red esté activa o solo cuando se monte otra partición. La lista completa de las opciones de montaje específicas de *systemd*, que generalmente llevan el prefijo `x-systemd.`, se detalla en [systemd.mount(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.mount.5#FSTAB).

En [fstab#Automount with systemd](/index.php/Fstab#Automount_with_systemd "Fstab") se proporciona un ejemplo de estas opciones de montaje en el contexto del *automontaje*, pensando en aquellos recursos que se deben montar tan solo cuando se les requiere en lugar de automáticamente en el momento del arranque.

### Montaje automático de particiones GPT

En un disco particionado con [GPT](/index.php/Partitioning_(Espa%C3%B1ol)#GUID_Partition_Table "Partitioning (Español)"), el script [systemd-gpt-auto-generator(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-gpt-auto-generator.8) montará particiones siguiendo la [especificación de particiones detectables](https://www.freedesktop.org/wiki/Specifications/DiscoverablePartitionsSpec/) , por lo tanto, las mismas se pueden omitir de `fstab`.

El montaje automático de una partición se puede desactivar cambiando el [tipo GUID](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") de la partición o configurando el atributo 63 "do not automount" para la partición en cuestión, véase [gdisk#Prevent GPT partition automounting](/index.php/Gdisk#Prevent_GPT_partition_automounting "Gdisk").

## Consejos y trucos

### Ejecutar servicios después de que la conexión de red esté activa

Para demorar la ejecución de un servicio hasta depués de que la red esté funcionando, incluya las siguientes dependencias en el archivo *.service*:

 `/etc/systemd/system/*foo*.service` 
```
[Unit]
...
**Wants=network-online.target**
**After=network-online.target**
...
```

El servicio de espera de red de la particular aplicación que gestiona la conexión la red también debe activarse para que `network-online.target` refleje adecuadamente el estado de la red.

*   Para los que usan [NetworkManager](/index.php/NetworkManager "NetworkManager"), [active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") `NetworkManager-wait-online.service`.
*   Si se usa [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"), `systemd-networkd-wait-online.service` se activa automáticamente de forma predeterminada cada vez que `systemd-networkd.service` está activado; compruebe que este es el caso con `systemctl is-enabled systemd-networkd-wait-online.service`, lo cual hará que no se necesite ninguna otra acción.

Para obtener explicaciones más detalladas, consulte: [ejecutar servicios después de que la red esté activa](https://www.freedesktop.org/wiki/Software/systemd/NetworkTarget/) en la wiki de systemd.

### Activar las unidades instaladas por defecto

Arch Linux se entrega con `/usr/lib/systemd/system-preset/99-default.preset` que contiene `disable *`. Esto hace que *systemctl preset* desactive todas las unidades de forma predeterminada, de modo que cuando se instala un nuevo paquete, el usuario debe activar la unidad manualmente.

Si este comportamiento no es deseado, simplemente cree un enlace simbólico de `/etc/systemd/system-preset/99-default.preset` a `/dev/null` para anular el archivo de configuración . Esto hará que *systemctl preset* active todas las unidades que se instalan, independientemente del tipo de unidad, a menos que se especifique otra cosa en otro archivo ubicado en uno de los directorios de configuración de *systemctl preset*. Las unidades de usuario no se verán afectadas. Vea [systemd.preset(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.preset.5) para más información.

**Nota:** activar todas las unidades por defecto puede causar problemas con los paquetes que contienen dos o más unidades mutuamente excluyentes. *systemctl preset* está diseñado para ser utilizado por distribuciones o administradores de sistemas. En el caso de que dos unidades en conflicto estén activadas, debe especificarse explícitamente cuál de ellas se debe desactivar en un archivo de configuración preestablecido, como se especifica en la página del manual de `systemd.preset`.

### Entornos seguros para probar aplicaciones

Un archivo de unidad se puede crear como un sandbox para aislar aplicaciones y sus procesos dentro de un entorno virtual reforzado. systemd aprovecha los [espacio de nombres](https://en.wikipedia.org/wiki/es:Espacio_de_nombres "wikipedia:es:Espacio de nombres"), las listas blancas/negras basadas en [Capabilities](/index.php/Capabilities "Capabilities") y los [grupos de control](/index.php/Cgroups "Cgroups") para contener procesos a través de una extensa [configuración de entornos de ejecución](https://www.freedesktop.org/software/systemd/man/systemd.exec.html).

El aprovisionamiento de un archivo de unidad systemd existente con la aplicación sandboxing, generalmente requiere de pruebas de ensayo y error acompañadas del uso generoso de [strace](https://www.archlinux.org/packages/?name=strace), [stderr](https://en.wikipedia.org/wiki/Standard_streams#Standard_error_.28stderr.29 "wikipedia:Standard streams"), registro de errores de [journalctl](https://www.freedesktop.org/software/systemd/man/journalctl.html) y de salida de recursos. Es posible que desee buscar primero en la documentación anterior los test ya realizados a partir de los cuales realizar la pruebas.

Algunos ejemplos sobre cómo se puede implementar el sandboxing con systemd:

*   `CapabilityBoundingSet` define un conjunto en lista blanca de capacidades permitidas, pero también se puede usar para incluir en una lista negra una capacidad específica para una unidad.
    *   La capacidad `CAP_SYS_ADM`, por ejemplo, que debería ser uno de los [objetivos de un sandbox seguro](https://lwn.net/Articles/486306/): `CapabilityBoundingSet=~ CAP_SYS_ADM`

## Solución de problemas

### Investigar errores de systemd

Como ejemplo, vamos a investigar un error con el servicio `systemd-modules-load`:

**1.** Vamos a determinar los servicios de *systemd* que fallan al inicio:

 `$ systemctl --state=failed`  `systemd-modules-load.service   loaded **failed failed**  Load Kernel Modules` 

Otra forma es ver los mensajes en vivo del registro de *systemd*:

```
$ journalctl -fp err

```

**2.** Encontramos un problema con el servicio `systemd-modules-load`. Indaguemos un poco más:

 `$ systemctl status systemd-modules-load` 
```
systemd-modules-load.service - Load Kernel Modules
   Loaded: loaded (/usr/lib/systemd/system/systemd-modules-load.service; static)
   Active: **failed** (Result: exit-code) since So 2013-08-25 11:48:13 CEST; 32s ago
     Docs: man:systemd-modules-load.service(8).
           man:modules-load.d(5)
  Process: **15630** ExecStart=/usr/lib/systemd/systemd-modules-load (**code=exited, status=1/FAILURE**)
```

Si el `Process ID` no está en la lista, simplemente reinicie el servicio fallido con `systemctl restart systemd-modules-load`

**3.** Ahora tenemos el identificador del proceso (PID) para investigar este error en profundidad. Escribimos la siguiente orden con el `Process ID` (en este caso: 15630):

 `$ journalctl _PID=15630` 
```
-- Logs begin at Sa 2013-05-25 10:31:12 CEST, end at So 2013-08-25 11:51:17 CEST. --
Aug 25 11:48:13 mypc systemd-modules-load[15630]: **Failed to find module 'blacklist usblp'**
Aug 25 11:48:13 mypc systemd-modules-load[15630]: **Failed to find module 'install usblp /bin/false'**
```

**4.** Vemos que algunos de los ajustes del módulo del kernel tienen valores erróneos. Por lo tanto, echemos un vistazo a estos valores en `/etc/modules-load.d/`:

 `$ ls -Al /etc/modules-load.d/` 
```
...
-rw-r--r--   1 root root    79  1\. Dez 2012  blacklist.conf
-rw-r--r--   1 root root     1  2\. Mär 14:30 encrypt.conf
-rw-r--r--   1 root root     3  5\. Dez 2012  printing.conf
-rw-r--r--   1 root root     6 14\. Jul 11:01 realtek.conf
-rw-r--r--   1 root root    65  2\. Jun 23:01 virtualbox.conf
...

```

**5.** El mensaje del error `Failed to find module 'blacklist usblp'` puede estar relacionado con un mal ajuste de `blacklist.conf`. Podemos desactivarlo insertando un signo **#** delante de cada opción que hemos descubierto que falla por medio del paso 3:

 `/etc/modules-load.d/blacklist.conf` 
```
**#** blacklist usblp
**#** install usblp /bin/false

```

**6.** Ahora, intente iniciar `systemd-modules-load`:

```
$ systemctl start systemd-modules-load.service

```

Si ha tenido éxito, no debe mostrarse ningún prompt. Si ve algún error, volveremos al paso 3 y utilizaremos el nuevo PID para solucionar los errores que aparecen en la izquierda.

Si todo está bien, se puede verificar que el servicio se ha iniciado satisfactoriamente con:

 `$ systemctl status systemd-modules-load` 
```
systemd-modules-load.service - Load Kernel Modules
   Loaded: **loaded** (/usr/lib/systemd/system/systemd-modules-load.service; static)
   Active: **active (exited)** since So 2013-08-25 12:22:31 CEST; 34s ago
     Docs: man:systemd-modules-load.service(8)
           man:modules-load.d(5)
 Process: 19005 ExecStart=/usr/lib/systemd/systemd-modules-load (code=exited, status=0/SUCCESS)
Aug 25 12:22:31 mypc systemd[1]: **Started Load Kernel Modules**.
```

### Diagnosticar problemas de arranque

*systemd* tiene varias opciones para diagnosticar problemas con el proceso de arranque. Consulte [boot debugging](/index.php/Boot_debugging "Boot debugging") para obtener instrucciones y opciones más generales para capturar mensajes de inicio antes de que *systemd* se haga cargo del [proceso de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)"). Véase también ña [documentación de depuración de errores de systemd](http://freedesktop.org/wiki/Software/systemd/Debugging/).

### Diagnosticar un servicio

Si algún servicio *systemd* se comporta mal o si desea obtener más información sobre lo que está sucediendo, configure la [variable de entorno](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") `SYSTEMD_LOG_LEVEL` a `debug`. Por ejemplo, para ejecutar el demonio *systemd-networkd* en modo de depuración de errores:

Agregue un [fragmento de archivo](#Archivos_insertados) para el servicio agregando las dos líneas siguientes:

```
[Service]
Environment=SYSTEMD_LOG_LEVEL=debug

```

O, de igual modo, establezca la variable de entorno manualmente:

```
# SYSTEMD_LOG_LEVEL=debug /lib/systemd/systemd-networkd

```

luego [reinicie](#Utilizar_las_unidades) *systemd-networkd* y observe jopurnal para el servicio con la opción `-f`/`--follow`.

### Apagar/reiniciar se hace terriblemente largo

Si el proceso de apagado tarda un tiempo muy largo (o parece congelarse), lo más probable es que un servicio no existente tenga la culpa. *systemd* espera un tiempo para iniciar cada servicio antes de tratar de acabar con él. Para averiguar si este es su caso, consulte [este artículo](http://freedesktop.org/wiki/Software/systemd/Debugging/#shutdowncompleteseventually).

### Los procesos de corta duración parecen no registrar ninguna salida

Si `systemctl -u foounit.service` no muestra ninguna salida para un servicio de breve duración, compruebe el PID. Por ejemplo, si `systemd-modules-load.service` falla, y `systemctl status systemd-modules-load` muestra que es seguido con PID 123, entonces es posible ver la salida de journal para dicho PID, por ejemplo `journalctl -b _PID=123`. Los campos con metadatos para journal, como `_SYSTEMD_UNIT` y `_COMM`, se recogen en modo asíncrono y se basan en la carpeta `/proc` para el proceso existente. La reparación de este proceso requiere la reparación del kernel para proporcionar estos datos por medio de una conexión socket, de forma similar a `SCM_CREDENTIALS`. En resumen, es un [bug](https://github.com/systemd/systemd/issues/2913). Tenga en cuenta que los servicios que fallan de inmediato pueden no imprimir nada en journal según el diseño de systemd.

### El tiempo de arranque aumenta con el tiempo

Después de usar `systemd-analyze` varios usuarios advirtieron que su tiempo de arranque había aumentado significativamente en comparación con lo que solía ser. Después de usar `systemd-analyze blame` se informa que [NetworkManager (Español)](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)") toma un tiempo inusualmente grande para comenzar.

El problema para algunos usuarios se debe a que `/var/log/journal` es demasiado grande. Esto puede tener otros impactos en el rendimiento, como para `systemctl status` o `journalctl`. Como tal, la solución es eliminar todos los archivos dentro de la carpeta (lo ideal sería hacer una copia de seguridad en algún lugar, al menos temporalmente) y luego establecer un límite de tamaño del archivo journal como se describe en [#Límite del tamaño de journal](#Límite_del_tamaño_de_journal).

### systemd-tmpfiles-setup.service no se inicia en el arranque

A partir de systemd 219, `/usr/lib/tmpfiles.d/systemd.conf` especifica los atributos de [ACL](https://en.wikipedia.org/wiki/es:Lista_de_control_de_acceso "wikipedia:es:Lista de control de acceso") para los directorios en `/var/log/journal` y, por lo tanto, requiere que el soporte de ACL sea activado para el sistema de archivos en el que reside journal.

Véase [Access Control Lists#Enabling ACL](/index.php/Access_Control_Lists#Enabling_ACL "Access Control Lists") para obtener instrucciones sobre cómo activar la ACL en el sistema de archivos que aloja `/var/log/journal`.

### La versión de systemd impresa en el arranque no es la misma que la versión del paquete instalado

Debe [regenerar initramfs](/index.php/Mkinitcpio_(Espa%C3%B1ol)#Creación_de_la_imagen_y_activación "Mkinitcpio (Español)") y las versiones deberían coincidir.

**Sugerencia:** se puede usar un hook de pacman para regenerar automáticamente initramfs cada vez que se actualice [systemd](https://www.archlinux.org/packages/?name=systemd). Vea [este hilo del foro](https://bbs.archlinux.org/viewtopic.php?id=215411) y [Pacman (Español)#Hooks](/index.php/Pacman_(Espa%C3%B1ol)#Hooks "Pacman (Español)").

### Desactivar el modo de emergencia en la máquina remota

Es posible que desee desactivar el modo de emergencia en una máquina remota, por ejemplo, una máquina virtual alojada en Azure o Google Cloud. Esto se debe a que, si se activa el modo de emergencia, la máquina no podrá conectarse a la red.

```
# systemctl mask emergency.service
# systemctl mask emergency.target

```

## Véase también

*   [Wikipedia article](https://en.wikipedia.org/wiki/systemd "wikipedia:systemd")
*   [systemd Official web site](https://www.freedesktop.org/wiki/Software/systemd)
    *   [systemd optimizations](https://www.freedesktop.org/wiki/Software/systemd/Optimizations)
    *   [systemd FAQ](https://www.freedesktop.org/wiki/Software/systemd/FrequentlyAskedQuestions)
    *   [systemd Tips and tricks](https://www.freedesktop.org/wiki/Software/systemd/TipsAndTricks)
*   [Manual pages](https://www.freedesktop.org/software/systemd/man/)
*   Otras distribuciones
    *   [Gentoo Wiki systemd page](https://wiki.gentoo.org/wiki/Systemd)
    *   [Fedora Project - About systemd](https://fedoraproject.org/wiki/Systemd)
    *   [Fedora Project - How to debug systemd problems](https://fedoraproject.org/wiki/How_to_debug_Systemd_problems)
    *   [Fedora Project - SysVinit to systemd cheatsheet](https://fedoraproject.org/wiki/SysVinit_to_Systemd_Cheatsheet)
    *   [Debian Wiki systemd page](https://wiki.debian.org/systemd "debian:systemd")
*   [Lennart's blog story](http://0pointer.de/blog/projects/systemd.html), [update 1](http://0pointer.de/blog/projects/systemd-update.html), [update 2](http://0pointer.de/blog/projects/systemd-update-2.html), [update 3](http://0pointer.de/blog/projects/systemd-update-3.html), [summary](http://0pointer.de/blog/projects/why.html)
*   [systemd for Administrators (PDF)](http://0pointer.de/public/systemd-ebook-psankar.pdf)
*   [How To Use Systemctl to Manage Systemd Services and Units](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units)
*   [Session management with systemd-logind](https://dvdhrm.wordpress.com/2013/08/24/session-management-on-linux/)
*   [Emacs Syntax highlighting for Systemd files](/index.php/Emacs#Syntax_highlighting_for_systemd_Files "Emacs")
*   [Two](http://www.h-online.com/open/features/Control-Centre-The-systemd-Linux-init-system-1565543.html) [part](http://www.h-online.com/open/features/Booting-up-Tools-and-tips-for-systemd-1570630.html) introductory article in *The H Open* magazine.