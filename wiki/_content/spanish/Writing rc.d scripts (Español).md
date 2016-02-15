Como parte del inicio "estilo-BSD" de arch, los scripts del rc.d son usados para el inicio, detencion y reiniciacion de los [demonios](/index.php/Daemon "Daemon").

## Lineas de guia

*   Fuente `/etc/rc.conf`, `/etc/rc.d/functions`, y opcionalmente `/etc/conf.d/DAEMON_NAME`.
*   Los argumentos y opciones de los demenios deben ir en `/etc/conf.d/DAEMON_NAME`. Esta hecho para separar las configuraciones y mantener la consistencia.
*   Usar las funciones en `/etc/rc.d/functions` en vez de duplicar las funcionalidades.
*   Inclir al menos "start", "stop" y "restart" como argumentos en es script.
*   Hay algunas funcionalidades provistas por `/etc/rc.d/functions`:
    *   stat_busy "<message>": establece el estado _busy_(ocupado) como mensaje a mostrar (ej: Iniciando Demonio [OCUPADO])
    *   stat_done: establece el estado _done_ (hecho) (ej: Iniciando Demonio [HECHO])
    *   stat_fail: establece el estado _failed_ (e.g. Iniciando Demonio [FALLO])
    *   get_pid <program>: obtiene el PID del programa.
    *   ck_pidfile <PID-file> <program>: Chekea si el PID-file es aun valido para el programa (e.g. ck_pidfile /var/run/daemon.pid daemon || rm -f /var/run/daemon.pid)
    *   [add|rm]_daemon <program>: Agrega/remueve programas a los demonios activos (almacenados en `/run/daemons/`)

## Ejemplo

Lo siguiente es un ejemplo para _crond_. Revise en `/etc/rc.d`, encontrara variedad.

El archivo de configuración:

 `/etc/conf.d/crond`  `ARGS="-S -l info"` 

El script actual:

 `/etc/rc.d/crond` 

```
#!/bin/bash

. /etc/rc.conf
. /etc/rc.d/functions

DAEMON=crond
ARGS=

[ -r /etc/conf.d/$DAEMON ] && . /etc/conf.d/$DAEMON

PID=$(get_pid $DAEMON)

case "$1" in
 start)
   stat_busy "Starting $DAEMON"
   [ -z "$PID" ] && $DAEMON $ARGS &>/dev/null
   if [ $? = 0 ]; then
     add_daemon $DAEMON
     stat_done
   else
     stat_fail
     exit 1
   fi
   ;;
 stop)
   stat_busy "Stopping $DAEMON"
   [ -n "$PID" ] && kill $PID &>/dev/null
   if [ $? = 0 ]; then
     rm_daemon $DAEMON
     stat_done
   else
     stat_fail
     exit 1
   fi
   ;;
 restart)
   $0 stop
   sleep 1
   $0 start
   ;;
 *)
   echo "usage: $0 {start|stop|restart}"  
esac

```