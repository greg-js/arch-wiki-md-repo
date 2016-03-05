En un sistema operativo, el reloj (*«clock»*) está determinado por cuatro partes: el valor del horario, la hora estándar, la zona horaria y el horario de verano (-DST- **D**aylight **S**aving **T**ime, si corresponde). En este artículo se explica qué son y cómo leer/configurar los mismos. Para *mantener* la hora del sistema ajustada mediante la red consulte [Network Time Protocol daemon](/index.php/Network_Time_Protocol_daemon_(Espa%C3%B1ol) "Network Time Protocol daemon (Español)").

## Contents

*   [1 Reloj del hardware y reloj del sistema](#Reloj_del_hardware_y_reloj_del_sistema)
    *   [1.1 Leer el reloj](#Leer_el_reloj)
    *   [1.2 Ajustar el reloj](#Ajustar_el_reloj)
    *   [1.3 Reloj RTC (Reloj en Tiempo Real)](#Reloj_RTC_.28Reloj_en_Tiempo_Real.29)
*   [2 Hora estándar](#Hora_est.C3.A1ndar)
    *   [2.1 UTC en Windows](#UTC_en_Windows)
*   [3 Huso horario](#Huso_horario)
*   [4 Desviación del horario](#Desviaci.C3.B3n_del_horario)
*   [5 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [5.1 El reloj muestra un valor que no es ni UTC ni hora local](#El_reloj_muestra_un_valor_que_no_es_ni_UTC_ni_hora_local)
*   [6 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Reloj del hardware y reloj del sistema

Un ordenador tiene dos relojes que deben tenerse en cuenta: el «reloj del hardware/ordenador» y el «reloj del sistema/software».

**El reloj del hardware** (también conocido como el Reloj en Tiempo Real ([RTC](https://en.wikipedia.org/wiki/es:Reloj_en_tiempo_real "wikipedia:es:Reloj en tiempo real")) o reloj CMOS) guarda los valores de: año, mes, día, hora, minuto y segundos. No tiene la capacidad de guardar el horario estándar (localtime o UTC), ni si DST (horario de verano) se utiliza.

**El reloj del sistema** (también conocido como reloj del software) realiza un seguimiento de: Hora, Zona horaria y DTS (el horario de verano, si procede). Ello es calculado por el kernel de Linux por el número de segundos transcurridos desde la medianoche del 1 de enero 1970, UTC. El valor inicial del reloj del sistema se establece a partir del reloj del hardware, en función de lo establecido en el archivo `/etc/adjtime`. Una vez completado el arranque, el reloj del sistema se configura independientemente del reloj del hardware. El kernel de Linux sigue los ajustes del reloj del sistema para integrar las interrupciones del temporizador.

### Leer el reloj

Para comprobar la hora actual del hardware y la hora del reloj del sistema, respectivamente (la hora del reloj del hardware se interpreta como hora local incluso si el reloj del hardware se ajusta en UTC):

```
$ timedatectl status

```

### Ajustar el reloj

Para ajustar el reloj del sistema directamente:

```
# timedatectl set-time "2012-10-30 18:17:16"

```

### Reloj RTC (Reloj en Tiempo Real)

El comportamiento normal de la mayoría de los sistemas operativos es el siguiente:

*   En el momento del arranque del ordenador el sistema operativo establece el horario del reloj del sistema desde el reloj de hardware.
*   Durante el funcionamiento del ordenador, se mantiene la hora exacta del reloj del sistema con un demonio [NTP](/index.php/Network_Time_Protocol_daemon_(Espa%C3%B1ol) "Network Time Protocol daemon (Español)").
*   En el momento de apagarse el ordenador, se ajusta el horario del reloj del hardware desde el reloj del sistema.

## Hora estándar

**Note:** [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") utilizará UTC para el reloj del hardware por defecto.

Hay dos estándares de tiempo: **localtime** y **C**oordinated **U**niversal **T**ime (**UTC**). La hora local (*«localtime»*) estándar depende de la actual *zona horaria*, mientras que UTC es el horario *mundial* estándar y es independiente de los valores de la zona horaria. Aunque conceptualmente diferentes, UTC es también conocido como GMT (Greenwich Mean Time).

El estándar utilizado por el reloj de hardware (reloj CMOS, la hora que aparece en la BIOS) se define por el sistema operativo. De manera predeterminada, Windows utiliza localtime, Mac OS utiliza UTC y varios sistemas operativos como UNIX. Un sistema operativo que utiliza el estándar UTC, por lo general, considera que el horario CMOS (el reloj del hardware) usa el horario UTC (GMT, hora de Greenwich) y lo reajusta, para que al configurarse la hora del sistema en el arranque esta coincida con la zona horaria.

Al usar Linux, es beneficioso tener el reloj del hardware configurado para usar el estándar UTC y que el resto de los sistemas operativos coexistentes en el ordenador estén al corriente de esta circunstancia. Definir el reloj del hardware como UTC en Linux significa que el cambio del horario de verano se produce automáticamente. Si se utiliza el estándar localtime, el reloj del sistema no cambiará la hora para ajustarse a DST, por que asume que otro sistema operativo se encargará de realizar el cambio horario de verano (esto es así siempre y cuando ningún demonio NTP está en funcionamiento).

Se puede configurar el horario estándar del reloj del hardware a través de la línea de órdenes. Para comprobar qué uso horario ha establecido la instalación Arch Linux, escriba:

```
$ timedatectl status | grep local

```

El reloj del hardware se puede consultar y ajustar con la orden `timedatectl`. Para cambiar el horario estándar del reloj del hardware para usar localtime:

```
# timedatectl set-local-rtc 1

```

Y para configurarlo para usar UTC:

```
# timedatectl set-local-rtc 0

```

Tenga en cuenta que, si el reloj del hardware está configurado en modo localtime, tratar con el horario de verano puede ser caótico. Si el horario de verano cambia cuando el ordenador está apagado, la hora estará mal en el próximo arranque ([aquí hay más información sobre ello](http://www.cl.cam.ac.uk/~mgk25/mswish/ut-rtc.html)). Los kernel actuales establecen la hora del sistema desde el RTC directamente en el arranque, asumiendo que RTC está configurado conforme a UTC. Esto significa que si el RTC está ajustado en hora local, entonces la hora del sistema, en un primer momento, vedrá mal establecida en cada arranque y, luego, corregida poco después. Esta es la causa de ciertos errores (ir hacia atrás en el tiempo no es buen consejo).

Las órdenes de arriba generarán el archivo `/etc/adjtime` automáticamente, sin que sea necesaria configuración adicional.

Durante el inicio del kernel, en el momento en que el controlador RTC está cargado, el reloj del sistema se configurará desde el reloj del hardware. Si esto ocurre o no, dependerá de la plataforma del hardware, la versión del kernel y las opciones de compilación del kernel. Si ocurre, en este punto de la secuencia de inicio, el sistema operativo presupone que la hora del reloj del hardware usa el estándar UTC y establece el valor de `/proc/sys/class/rtcN/hctosys` (N=0,1,2,..) en 1\. Más tarde, el reloj del sistema se ajusta de nuevo desde el reloj de hardware en systemd, dependiendo de los valores en `/etc/adjtime` . Por lo tanto, con el reloj de hardware en localtime puede provocar un comportamiento inesperado durante la secuencia de inicio, por ejemplo la hora del sistema volviendo hacia atrás, lo cual es siempre una mala idea.

**Nota:** El uso de `timedatectl` requiere un dbus activo. Por lo tanto, puede que no sea posible utilizar esta orden en un entorno chroot (por ejemplo, durante la instalación). En estos casos, se puede volver a la orden hwclock.

### UTC en Windows

Una razón por la que los usuarios a menudo establecen RTC en localtime es para un [arranque dual con Windows](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot") ([que utiliza localtime](http://blogs.msdn.com/b/oldnewthing/archive/2004/09/02/224672.aspx)). Sin embargo, Windows puede hacer frente a RTC estando en UTC con un simple [ajuste del registro](#UTC_en_Windows). Es recomendable configurar Windows para que use UTC, en lugar de configurar Linux para que use localtime. Si configura Windows para que use UTC, recuerde también desactivar la función de Windows *«Internet Time Update»*, para que Windows no interfiera en el reloj del hardware, tratando de sincronizarlo con el horario de Internet. En su lugar considere usar [NTP](/index.php/Network_Time_Protocol_daemon_(Espa%C3%B1ol) "Network Time Protocol daemon (Español)") para modificar RTC y sincronizarlo con el horario de internet.

Utilice `regedit`, y añada un valor `DWORD` con el parámetro hexadecimal `1` en el registro:

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation\RealTimeIsUniversal

```

Como alternativa, puede crear un archivo `*.reg` (en el escritorio) con el siguiente contenido y haga doble clic sobre él para importarlo al registro:

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation]
     "RealTimeIsUniversal"=dword:00000001

```

Windows XP y Windows Vista SP1 están habilitados para establecer el horario estándar usando UTC y activarse de la misma manera. Sin embargo, se produce un error después de reanudar desde el modo de suspensión/hibernación que hace que recoloque en *localtime* el reloj. Para estos sistemas operativos se recomienda usar *localtime*.

En el caso de que Windows intente actualizar el reloj siguiendo los cambios de DTS, permítalo. Dejará el reloj en UTC como se esperaba, corrigiendo solamente la hora visualizada.

La hora del reloj del hardware y del reloj del sistema puede ser necesario [actualizarlas](#Set_clock) después de ajustar este valor.

Si está teniendo problemas con el desfase del horario, pruebe reinstalando `tzdata` y luego establecer su zona horaria de nuevo.

```
# pacman -S tzdata
# timedatectl set-timezone Europa/Madrid

```

Es lógico [desactivar](http://www.addictivetips.com/windows-tips/disable-time-synchronization-in-windows-7/) la sincronización horaria en Windows, de lo contrario se hará un lío el reloj del equipo.

## Huso horario

Puede comprobar el [Huso horario](https://en.wikipedia.org/wiki/es:Huso_horario "wikipedia:es:Huso horario") que rige en su equipo con:

```
$ timedatectl status

```

Puede listar las áreas disponibles con:

```
$ timedatectl list-timezones

```

Puede cambiar el uso horario con:

```
# timedatectl set-timezone <Zone>/<SubZone>

```

He aquí un ejemplo:

```
# timedatectl set-timezone Canada/Eastern

```

Esto creará un enlace simbólico `/etc/localtime` que apunta a un archivo de información de zonas en `/usr/share/zoneinfo/`. En caso de que decida crear el enlace manualmente, tenga en cuenta que debe ser un enlace relativo, no absoluto, como se especifica en archlinux(7).

Véase `man 1 timedatectl`, `man 5 localtime`, y `man 7 archlinux` para más detalles.

**Nota:** Si el archivo de configuración `/etc/timezone` anterior a la instalación de systemd todavía está presente en su sistema, puede eliminarlo de forma segura, puesto que ya no se utilizará.

## Desviación del horario

Cada reloj tiene un valor que difiere del *horario actual* (la mejor representación sigue siendo el [Tiempo Atómico Internacional](https://en.wikipedia.org/wiki/es:Tiempo_At%C3%B3mico_Internacional "wikipedia:es:Tiempo Atómico Internacional")); no hay reloj perfecto. Un reloj electrónico basado en cuarzo mantiene un horaro imperfecto, pero mantiene una inexactitud constante. Esta base de «inexactitud» es lo que se conoce como «tiempo sesgado» o «tiempo de desviación».

Cuando el reloj del hardware está configurado con `hwclock`, la aplicación calcula un valor de desviación nuevo en segundos por día. El valor de desviación se calcula mediante la diferencia entre el nuevo valor y el valor del reloj del hardware justo antes del ajuste, teniendo en cuenta para fijar el nuevo valor, el valor de desviación anterior y la última vez que se ajustó el reloj del hardware. El nuevo valor de la desviación y el momento en que se ajustó el reloj, se registran en el archivo `/etc/adjtime`, sobreescribiendo los valores anteriores. El reloj del hardware, por lo tanto, se ajusta, para que sirva de referencia a la desviación, cuando se ejecuta la orden `hwclock --adjust`, lo cual ocurre también en el apagado, pero solo si el demonio `hwclock` está habilitado (por lo tanto, para sistemas que utilizan systemd , esto no sucede).

**Nota:** Si el reloj del ordenador se ha ajustado de nuevo en menos de 24 horas desde el anterior ajuste, la desviación no se recalcula, al considerar `hwclock` que el período de tiempo transcurrido es demasiado corto como para calcular la derivación con precisión.

Si el reloj de hardware mantiene pérdidas o incrementos de tiempo grandes, es posible que se haya registrado una deriva inválida (pero esto solo es aplicable si el demonio hwclock se está ejecutando). Esto puede suceder si se ha ajustado la hora del reloj del hardware incorrectamente o el [horario estándar](#Hora_est.C3.A1ndar) no está sincronizado con una instalación de Windows o Mac OS. El valor de desviación se puede quitar, eliminando el archivo `/etc/adjtime`, y, después, ajustando correctamente el reloj del hardware y la hora del reloj del sistema, y verificando si el [horario estándar](#Hora_est.C3.A1ndar) es correcto.

**Nota:** Para los que utilizan systemd, pero desean hacer uso del valor de desviación guardado en `/etc/adjtime` (es decir, si tal vez no quieren usar NTP), tienen que ejecutar `hwclock --adjust` de manera regular, quizás mediante la creación de una tarea cron.

El reloj del software es muy preciso, pero, como la mayoría de los relojes, no es totalmente preciso y se desvía también. Aunque rara vez, el reloj del sistema puede perder precisión si el kernel omite las interrupciones. Hay algunas herramientas para mejorar la precisión del rejoj del software:

*   [NTP](/index.php/Network_Time_Protocol_daemon_(Espa%C3%B1ol) "Network Time Protocol daemon (Español)") puede sincronizar el reloj del software de un sistema GNU/Linux con servidores de hora de internet utilizando el protocolo de tiempo de red ([*«Network Time Protocol»*](https://en.wikipedia.org/wiki/es:Network_Time_Protocol "wikipedia:es:Network Time Protocol")). NTP también puede ajustar la frecuencia de interrupción y el número de pasos por segundo para reducir la deriva del reloj del sistema. La ejecución de NTP también hará que el reloj del hardware está resincronizado cada 11 minutos.
*   [adjtimex](https://aur.archlinux.org/packages/adjtimex/) en [AUR](/index.php/Arch_User_Repository "Arch User Repository") puede interpretar las variaciones de tiempo del kernel como frecuencias de interrupción, para ayudar a mejorar la deriva del horario del reloj del sistema.

## Solución de problemas

### El reloj muestra un valor que no es ni UTC ni hora local

Esto podría ser causado por varias razones. Por ejemplo, si el reloj de hardware está funcionando con la hora local, pero `timedatectl` está ajustado para asumir que está en UTC, el resultado sería que al estar configurada la zona horaria conforme a UTC, la hora vendría corregida dos veces, ofreciendo valores incorrectos tanto para la hora local como para UTC.

Para forzar al reloj a que adopte la hora correcta, y para pasar también el horario UTC correcto al reloj del hardware, siga estos pasos:

*   Instale [NTP](/index.php/NTP "NTP") (no es necesario activarlo como un servicio).
*   Establezca el [huso horario](#Huso_horario) correctamente.
*   Ejecute `ntpd -qg` para sincronizar manualmente el reloj con la red, omitiendo las desviaciones grandes entre UTC local y UTC de red.
*   Ejecute `hwclock --systohc` para pasar el horario UTC actual del software al reloj del clock.

## Véase también

*   [Linux Tips - Linux, Clocks, and Time](http://www.linuxsa.org.au/tips/time.html)
*   [Sources for Time Zone and Daylight Saving Time Data](http://www.twinsun.com/tz/tz-link.htm) for [tzdata](https://www.archlinux.org/packages/?name=tzdata)
*   [Time Scales](http://www.ucolick.org/~sla/leapsecs/timescales.html)
*   [Wikipedia:Time](https://en.wikipedia.org/wiki/Time "wikipedia:Time")