**Estado de la traducción**
Este artículo es una traducción de [Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers"), revisada por última vez el **2018-11-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Systemd/Timers&diff=0&oldid=556635) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")
*   [systemd/User (Español)](/index.php/Systemd/User_(Espa%C3%B1ol) "Systemd/User (Español)")
*   [systemd FAQ (Español)](/index.php/Systemd_FAQ_(Espa%C3%B1ol) "Systemd FAQ (Español)")
*   [cron](/index.php/Cron "Cron")

Los temporizadores son archivos de unidad de [systemd (Español)](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") cuyo nombre termina en `.timer` que controlan archivos `.service` o eventos. Los temporizadores se pueden usar como una alternativa a [cron](/index.php/Cron "Cron") (lea [#Como un reemplazo de cron](#Como_un_reemplazo_de_cron)). Los temporizadores tienen soporte incorporado para ejecutar eventos basados en el calendario, eventos de tiempo monotónicos y se pueden ejecutar de forma asíncrona.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Unidades de temporizador](#Unidades_de_temporizador)
*   [2 Unidad de servicio](#Unidad_de_servicio)
*   [3 Gestión](#Gestión)
*   [4 Ejemplos](#Ejemplos)
    *   [4.1 Temporizador monotónico](#Temporizador_monotónico)
    *   [4.2 Temporizador en tiempo real](#Temporizador_en_tiempo_real)
*   [5 Unidades .timer transitorias](#Unidades_.timer_transitorias)
*   [6 Como un reemplazo de cron](#Como_un_reemplazo_de_cron)
    *   [6.1 Beneficios](#Beneficios)
    *   [6.2 Advertencias](#Advertencias)
    *   [6.3 MAILTO](#MAILTO)
    *   [6.4 Utilizar un crontab](#Utilizar_un_crontab)
*   [7 Véase también](#Véase_también)

## Unidades de temporizador

Los temporizadores son archivos de unidades de *systemd* terminados en un sufijo `.timer`. Los temporizadores son como cualquier otro [arcivo de configuración de unidad](/index.php/Systemd_(Espa%C3%B1ol)#Escribir_archivos_de_unidad "Systemd (Español)") y se cargan desde las mismas rutas, pero incluyen una sección `[Timer]` que define cuándo y cómo se activa el temporizador. Los temporizadores se definen como uno de estos dos tipos:

*   **Temporizadores en tiempo real** (también conocido como «wallclock timers») se activan con un evento del calendario, de la misma manera que lo hacen los cronjobs. La opción `OnCalendar=` se utiliza para definirlos.
*   **Temporizadores monotónicos** se activan después de un intervalo de tiempo condicionado a un punto de inicio variable. Se detienen si el equipo está temporalmente suspendido o apagado. Hay varios temporizadores monotónicos diferentes, pero todos tienen la forma: `On*Type*Sec=`. Los temporizadores monotónicos comunes incluyen `OnBootSec` y `OnActiveSec`.

Para obtener una explicación completa de las opciones del temporizador, consulte [systemd.timer(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.timer.5). La sintaxis de los argumentos para los eventos del calendario y los intervalos de tiempo se definen en [systemd.time(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.time.7).

## Unidad de servicio

Para cada archivo `.timer`, existe un archivo `.service` coincidente (por ejemplo, `foo.timer` y `foo.service`). El archivo `.timer` activa y controla el archivo `.service`. El archivo `.service` no requiere una sección `[Install]` ya que son las unidades de *temporizador* las que se activan. Si es necesario, es posible controlar una unidad con un nombre diferente usando la opción `Unit=` en la sección `[Timer]` del archivo temporizador.

## Gestión

Para usar una unidad *temporizador* [active](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") e [inicie](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") la misma como cualquier otra unidad (recuerde agregar el sufijo `.timer`). Para ver todos los temporizadores iniciados, ejecute:

 `$ systemctl list-timers` 
```
NEXT                          LEFT        LAST                          PASSED     UNIT                         ACTIVATES
Thu 2014-07-10 19:37:03 CEST  11h left    Wed 2014-07-09 19:37:03 CEST  12h ago    systemd-tmpfiles-clean.timer systemd-tmpfiles-clean.service
Fri 2014-07-11 00:00:00 CEST  15h left    Thu 2014-07-10 00:00:13 CEST  8h ago     logrotate.timer              logrotate.service

```

**Nota:**

*   Para enumerar todos los temporizadores (incluido inactivos), use `systemctl list-timers --all`.
*   El estado de un servicio iniciado por un temporizador probablemente aparecerá inactivo a menos que se esté activando en ese momento.
*   Si un temporizador se desincroniza, puede ayudar eliminar su archivo `stamp-*` en `/var/lib/systemd/timers` (o `~/.local/share/systemd/` en caso de temporizadores de usuario). Estos son archivos de longitud cero que marcan la última vez que se ejecutó cada temporizador. Si se eliminan, se reconstruirán en el próximo inicio de su temporizador.

## Ejemplos

Un archivo de unidad de servicio se puede programar con un temporizador listo para usar. Los siguientes ejemplos programan que el servicio, `foo.service`, se ejecutará con el temporizador correspondiente llamado `foo.timer`.

### Temporizador monotónico

Un temporizador que se iniciará 15 minutos después del arranque y nuevamente cada semana mientras el sistema se está ejecutando.

 `/etc/systemd/system/foo.timer` 
```
[Unit]
Description=Run foo weekly and on boot

[Timer]
OnBootSec=15min
OnUnitActiveSec=1w 

[Install]
WantedBy=timers.target

```

### Temporizador en tiempo real

Un temporizador que comienza una vez a la semana (a las 12:00 AM del lunes). Cuando se activa, activa el servicio inmediatamente si se perdió la última hora de inicio (opción `Persistent=true`), por ejemplo, debido a que el sistema estaba apagado:

 `/etc/systemd/system/foo.timer` 
```
[Unit]
Description=Run foo weekly

[Timer]
OnCalendar=weekly
Persistent=true

[Install]
WantedBy=timers.target
```

Cuando se requieren fechas y horas más específicas, los eventos de `OnCalendar` utilizan el siguiente formato:

```
`DayOfWeek Year-Month-Day Hour:Minute:Second`

```

es decir:

```
`DíadelaSemana Año-Mes-Día Hora:Minuto:Segundo`

```

Se puede usar un asterisco para especificar cualquier valor y se pueden usar comas para listar posibles valores. Dos valores separados por `..` indica un rango contiguo.

En el ejemplo siguiente, el servicio se ejecuta los primeros cuatro días de cada mes a las 12:00 PM, pero *solo* si ese día es lunes o martes.

```
OnCalendar=Mon,Tue *-*-01..04 12:00:00

```

Para ejecutar un servicio el primer sábado de cada mes, use:

```
OnCalendar=Sat *-*-1..7 18:00:00

```

Al usar `DayOfWeek`, se debe especificar, al menos, un día de la semana. Si quiere algo para ejecutar todos los días a las 4 AM, utilice:

```
 OnCalendar=*-*-* 4:00:00

```

Para ejecutar un servicio en diferentes momentos, `OnCalendar` puede especificarse más de una vez. En el siguiente ejemplo, el servicio se ejecuta a las 22:30 los días entre fines de semana y a las 20:00 los fines de semana.

```
 OnCalendar=Mon..Fri 22:30
 OnCalendar=Sat,Sun 20:00

```

Dispone de más información en [systemd.time(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.time.7).

**Sugerencia:**

*   `OnCalendar` se puede probar para verificar su funcionamiento y para calcular la próxima vez en que se producirá la condición suspensiva para el caso de que se utilice una unidad de temporizador con `calendar` de la utilidad *systemd-analyse*. Por ejemplo, se puede usar `systemd-analyze calendar weekly` o `systemd-analyze calendar "Mon,Tue *-*-01..04 12:00:00"`.
*   La orden `faketime` es especialmente útil para probar varios escenarios con la orden anterior; viene con el paquete [libfaketime](https://www.archlinux.org/packages/?name=libfaketime).
*   Expresiones de eventos especiales como `daily` y `weekly` hacen referencia a *horas de inicio específicas* y, por lo tanto, cualquier temporizador que comparta dichos eventos de calendario se iniciará simultáneamente. Los temporizadores que comparten eventos de inicio pueden provocar un rendimiento deficiente del sistema si los servicios de los temporizadores compiten por los recursos del sistema. La opción `RandomizedDelaySec` en la sección `[Timer]` evita este problema al alternar aleatoriamente la hora de inicio de cada temporizador. Vea [systemd.timer(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.timer.5).

## Unidades .timer transitorias

Se puede utilizar `systemd-run` para crear unidades `.timer` transitorias. Es decir, se puede configurar una orden para que se ejecute a una hora específica sin tener un archivo de servicio. Por ejemplo, la siguiente orden muestra un archivo después de 30 segundos:

```
# systemd-run --on-active=30 /bin/touch /tmp/foo

```

También se puede especificar un archivo de servicio preexistente que no tiene un archivo de temporizador. Por ejemplo, lo siguiente inicia la unidad systemd llamada `*someunit*.service` después de que hayan transcurrido 12 horas y media:

```
# systemd-run --on-active="12h 30m" --unit *someunit*.service

```

Véase [systemd-run(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-run.1) para más información y ejemplos.

## Como un reemplazo de cron

Aunque [cron](/index.php/Cron "Cron") es posiblemente el planificador de trabajos más conocido, los temporizadores de *systemd* pueden ser una alternativa.

### Beneficios

Los principales beneficios de usar temporizadores provienen del hecho de que cada trabajo tiene su propio servicio *systemd*. Algunos de estos beneficios son:

*   Los trabajos pueden iniciarse fácilmente independientemente de sus temporizadores. Esto simplifica la depuración de errores.
*   Cada trabajo puede configurarse para ejecutarse en un entorno específico (consulte [systemd.exec(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.exec.5)).
*   Los trabajos se pueden adjuntar a [grupos de control](/index.php/Cgroups "Cgroups").
*   Los trabajos se pueden configurar para que dependan de otras unidades de *systemd*.
*   Los trabajos se registran en el journal de *systemd* para una fácil depuración de errores.

### Advertencias

Algunas cosas que son fáciles de hacer con cron son difíciles de hacer solo con unidades de temporizador:

*   Creación: para configurar un trabajo temporizado con *systemd* necesita crear dos archivos y ejecutar órdenes `systemctl`, en comparación con crontab que basta con agregar una sola línea.
*   Correos electrónicos: no hay un equivalente incorporado a `MAILTO` de cron para enviar correos electrónicos en el caso de que falle el trabajo. Consulte la siguiente sección para ver un ejemplo de cómo configurar una funcionalidad similar utilizando `OnFailure=`.

### MAILTO

Puede configurar systemd para enviar un correo electrónico cuando falla una unidad. Cron envía un correo a `MAILTO` si el trabajo da una salida [stdout o stderr](https://en.wikipedia.org/wiki/es:Entrada_est%C3%A1ndar "wikipedia:es:Entrada estándar"), aunque muchos trabajos se pueden configurar para generar solo un error. Primero, necesita dos archivos: un ejecutable para enviar el correo y un *.service* para iniciar el ejecutable. Para este ejemplo, el ejecutable es solo un script de intérprete de órdenes que usa `sendmail`:

 `/usr/local/bin/systemd-email` 
```
#!/bin/bash

/usr/bin/sendmail -t <<ERRMAIL
To: $1
From: systemd <root@$HOSTNAME>
Subject: $2
Content-Transfer-Encoding: 8bit
Content-Type: text/plain; charset=UTF-8

$(systemctl status --full "$2")
ERRMAIL
```

Cualquiera que sea el ejecutable que utilice, probablemente debería tomar, al menos, dos argumentos, como lo hace este script de intérprete de órdenes: la dirección a la que enviar el correo y el archivo de la unidad para obtener el estado (de no entregado). El *.service* que creamos pasará estos argumentos:

 `/etc/systemd/system/status-email-*user*@.service` 
```
[Unit]
Description=status email for %i to *user*

[Service]
Type=oneshot
ExecStart=/usr/local/bin/systemd-email *address* %i
User=nobody
Group=systemd-journal
```

Donde `*user*` es el usuario que recibe el correo electrónico y `*address*` es la dirección de correo electrónico de ese usuario. Aunque el receptor esté codificado, el archivo de unidad sobre el que se informa se pasa como un parámetro de instancia, por lo que este servicio puede enviar correo electrónico para muchas otras unidades. En este punto, puede [iniciar](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") `status-email-*user*@dbus.service` para verificar que puede recibir los correos electrónicos.

Luego simplemente [edite](/index.php/Systemd_(Espa%C3%B1ol)#Modificar_los_archivos_de_unidad_suministrados "Systemd (Español)") el servicio para el que desea correos electrónicos y agregue `OnFailure=status-email-*user*@%n.service` a la sección `[Unit]`. `%n` pasa el nombre de la unidad a la plantilla.

**Nota:**

*   Si configura la seguridad SSMTP de acuerdo con [SSMTP#Security](/index.php/SSMTP#Security "SSMTP"), el usuario `nobody` no tendrá acceso a `/etc/ssmtp/ssmtp.conf`, y la orden `systemctl start status-email-*user*@dbus.service` fallará. Una solución para ello es usar `root` como User en la unidad `status-email-*user*@.service`.
*   Si intenta utilizar `mail -s somelogs *address*` en su script de correo electrónico, `mail` se bifurcará y systemd interrumpirá el proceso de correo cuando vea su script salir. Haga que el correo no se bifurque con `mail -Ssendwait -s somelogs *address*`.

### Utilizar un crontab

Se pueden solucionar varias de las advertencias descritas arriba mediante la instalación de un paquete que pase un crontab tradicional para configurar los temporizadores. [systemd-cron-next](https://aur.archlinux.org/packages/systemd-cron-next/) y [systemd-cron](https://aur.archlinux.org/packages/systemd-cron/) son dos de estos paquetes. Estos pueden proporcionar la característica `MAILTO` que falta.

Además, al igual que con crontabs, se puede obtener una vista unificada de todos los trabajos programados con `systemctl`. Véase [#Gestión](#Gestión).

## Véase también

*   [systemd.timer(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.timer.5)
*   [Página wiki del Proyecto Fedora](https://fedoraproject.org/wiki/Features/SystemdCalendarTimers) sobre los temporizadores basados en el calendario de *systemd*
*   [Sección de la wiki de Gentoo](https://wiki.gentoo.org/wiki/Systemd#Timer_services) sobre los servicios temporizadores de *systemd*
*   **systemd-cron-next** — herramienta para generar temporizadores/servicios desde archivos crontab y anacrontab

	[https://github.com/systemd-cron/systemd-cron-next](https://github.com/systemd-cron/systemd-cron-next) || [systemd-cron-next](https://aur.archlinux.org/packages/systemd-cron-next/)

*   **systemd-cron** — proporciona unidades systemd para ejecutar scripts de cron; utilizando *systemd-crontab-generator* para convertir crontabs

	[https://github.com/systemd-cron/systemd-cron](https://github.com/systemd-cron/systemd-cron) || [systemd-cron](https://aur.archlinux.org/packages/systemd-cron/)