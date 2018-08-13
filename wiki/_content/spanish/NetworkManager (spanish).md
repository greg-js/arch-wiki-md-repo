Artículos relacionados

*   [Network Configuration (Español)](/index.php/Network_Configuration_(Espa%C3%B1ol) "Network Configuration (Español)")
*   [Wireless Setup (Español)](/index.php/Wireless_Setup_(Espa%C3%B1ol) "Wireless Setup (Español)")
*   [Netctl (Español)](/index.php/Netctl_(Espa%C3%B1ol) "Netctl (Español)")
*   [Wicd (Español)](/index.php/Wicd_(Espa%C3%B1ol) "Wicd (Español)")

[NetworkManager](http://projects.gnome.org/NetworkManager/) es un programa que proporciona a los sistemas la detección y configuración automática para conectarse a la red. Las funcionalidades de NetworkManager son útiles tanto para redes inalámbricas como por cable. Para las redes inalámbricas, NetworkManager prefiere las redes conocidas y tiene la capacidad de cambiar a la red más confiable. NetworkManager permite que las aplicaciones puedan cambiar de modalidad en línea y fuera de línea. NetworkManager da preferencia a las conexiones por cable antes que a las inalámbricas, tiene soporte para conexiones por módem y para ciertos tipos de VPN. NetworkManager fue originariamente desarrollado por Red Hat y ahora es respaldado por el proyecto [GNOME](/index.php/GNOME "GNOME").

## Contents

*   [1 Intalación base](#Intalaci.C3.B3n_base)
    *   [1.1 Soporte VPN](#Soporte_VPN)
*   [2 Interfaces gráficas](#Interfaces_gr.C3.A1ficas)
    *   [2.1 GNOME](#GNOME)
    *   [2.2 KDE](#KDE)
    *   [2.3 XFCE](#XFCE)
    *   [2.4 Openbox](#Openbox)
    *   [2.5 Otros escritorios y gestores de ventanas](#Otros_escritorios_y_gestores_de_ventanas)
    *   [2.6 Desde la línea de órdenes](#Desde_la_l.C3.ADnea_de_.C3.B3rdenes)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Activar NetworkManager](#Activar_NetworkManager)
        *   [3.1.1 Evitar advertencias](#Evitar_advertencias)
    *   [3.2 Activar NetworkManager Wait Online](#Activar_NetworkManager_Wait_Online)
    *   [3.3 Configurar permisos PolicyKit](#Configurar_permisos_PolicyKit)
    *   [3.4 Servicios de red con NetworkManager dispatcher](#Servicios_de_red_con_NetworkManager_dispatcher)
        *   [3.4.1 Evitar el tiempo de espera de tres segundos](#Evitar_el_tiempo_de_espera_de_tres_segundos)
        *   [3.4.2 Iniciar OpenNTPD](#Iniciar_OpenNTPD)
        *   [3.4.3 Montar carpeta remota con sshfs](#Montar_carpeta_remota_con_sshfs)
        *   [3.4.4 Usar dispatcher para conectarse a VPN despues de establecer una conexión de red](#Usar_dispatcher_para_conectarse_a_VPN_despues_de_establecer_una_conexi.C3.B3n_de_red)
    *   [3.5 Configuración del proxy](#Configuraci.C3.B3n_del_proxy)
*   [4 Comprobación](#Comprobaci.C3.B3n)
*   [5 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [5.1 Al usar nm-applet, las conexiones a redes wifi no solicitan contraseña y se desconectan](#Al_usar_nm-applet.2C_las_conexiones_a_redes_wifi_no_solicitan_contrase.C3.B1a_y_se_desconectan)
    *   [5.2 Problemas con el tráfico de datos a través del canal PPTP](#Problemas_con_el_tr.C3.A1fico_de_datos_a_trav.C3.A9s_del_canal_PPTP)
    *   [5.3 Desactivada la gestión de red](#Desactivada_la_gesti.C3.B3n_de_red)
    *   [5.4 Personalizar resolv.conf](#Personalizar_resolv.conf)
    *   [5.5 Problemas con DHCP](#Problemas_con_DHCP)
    *   [5.6 Problemas con hostname (*«nombre del equipo»*)](#Problemas_con_hostname_.28.C2.ABnombre_del_equipo.C2.BB.29)
        *   [5.6.1 Opción 1: modificar keyfil en NetworkManager.conf](#Opci.C3.B3n_1:_modificar_keyfil_en_NetworkManager.conf)
        *   [5.6.2 Opción 2: configurar dhclient para poner el nombre del equipo en el servidor DHCP](#Opci.C3.B3n_2:_configurar_dhclient_para_poner_el_nombre_del_equipo_en_el_servidor_DHCP)
        *   [5.6.3 Opción 3: configurar NetworkManager para utilizar dhcpcd](#Opci.C3.B3n_3:_configurar_NetworkManager_para_utilizar_dhcpcd)
    *   [5.7 Falta la ruta predeterminada](#Falta_la_ruta_predeterminada)
    *   [5.8 Modem 3G no detectado](#Modem_3G_no_detectado)
    *   [5.9 Desconexión de WLAN en portátiles](#Desconexi.C3.B3n_de_WLAN_en_port.C3.A1tiles)
    *   [5.10 Ajustes de la IP estática restaurando a DHCP](#Ajustes_de_la_IP_est.C3.A1tica_restaurando_a_DHCP)
    *   [5.11 No se pueden editar las conexiones como usuario normal](#No_se_pueden_editar_las_conexiones_como_usuario_normal)
    *   [5.12 Eliminar una red oculta](#Eliminar_una_red_oculta)
    *   [5.13 VPN no funciona en Gnome](#VPN_no_funciona_en_Gnome)
*   [6 Consejos y trucos](#Consejos_y_trucos)
    *   [6.1 Compartir la conexión a Internet a través de Wi-Fi](#Compartir_la_conexi.C3.B3n_a_Internet_a_trav.C3.A9s_de_Wi-Fi)
        *   [6.1.1 Ad-hoc](#Ad-hoc)
        *   [6.1.2 Real AP](#Real_AP)
    *   [6.2 Comprobar la activación de la red en el interior de un proceso cron o script](#Comprobar_la_activaci.C3.B3n_de_la_red_en_el_interior_de_un_proceso_cron_o_script)
    *   [6.3 Desbloquear automáticamente keyring después del login](#Desbloquear_autom.C3.A1ticamente_keyring_despu.C3.A9s_del_login)
        *   [6.3.1 GNOME](#GNOME_2)
        *   [6.3.2 KDE](#KDE_2)
        *   [6.3.3 SLiM login manager](#SLiM_login_manager)
    *   [6.4 Ignorar dispositivos específicos](#Ignorar_dispositivos_espec.C3.ADficos)
    *   [6.5 Conectar más rápido](#Conectar_m.C3.A1s_r.C3.A1pido)
        *   [6.5.1 Deshabilitar IPv6](#Deshabilitar_IPv6)
        *   [6.5.2 Acelerar DHCP mediante la desactivación de ARP sondeando DHCPCD](#Acelerar_DHCP_mediante_la_desactivaci.C3.B3n_de_ARP_sondeando_DHCPCD)
        *   [6.5.3 Usar servidores OpenDNS](#Usar_servidores_OpenDNS)
    *   [6.6 Activar el almacenamiento en caché de DNS](#Activar_el_almacenamiento_en_cach.C3.A9_de_DNS)

## Intalación base

NetworkManager se puede [instalar](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") con el paquete [networkmanager](https://www.archlinux.org/packages/?name=networkmanager), disponible en los [repositorios oficiales](/index.php/Official_repositories "Official repositories").

### Soporte VPN

Network Manager tiene soporte para las redes VPN mediante un sistema basado en plug-ins. Si necesita asistencia técnica VPN a través del gestor de la red hay que instalar uno de los siguientes paquetes de los [repositorios oficiales](/index.php/Official_repositories "Official repositories"):

*   [networkmanager-openconnect](https://www.archlinux.org/packages/?name=networkmanager-openconnect)
*   [networkmanager-openvpn](https://www.archlinux.org/packages/?name=networkmanager-openvpn)
*   [networkmanager-pptp](https://www.archlinux.org/packages/?name=networkmanager-pptp)
*   [networkmanager-vpnc](https://www.archlinux.org/packages/?name=networkmanager-vpnc)

## Interfaces gráficas

Para configurar y acceder fácilmente a NetworkManager la mayoría de los usuarios desearán instalar un applet. Esta GUI normalmente se ubica en la bandeja del sistema (o área de notificación) y permite la selección de red y la configuración de NetworkManager. Existen distintos tipos de applets para los diferentes tipos de entornos de escritorio.

### GNOME

El applet de GNOME [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) (anteriormente gnome-network-manager) es lo suficientemente ligero y funciona en todos los entornos.

Si desea guardar los datos de autentificación (Wireless/DSL) y activar la configuración global de las conexiones, es decir, «disponible para todos los usuarios» instale y configure [GNOME Keyring](/index.php/GNOME_Keyring "GNOME Keyring").

### KDE

El frontend de Plasma de Network Manager es un widget disponible en los repositorios oficiales como el paquete [kdeplasma-applets-plasma-nm](https://www.archlinux.org/packages/?name=kdeplasma-applets-plasma-nm). El anterior frontend de Plasma KNetworkManager también está disponible como paquete [kdeplasma-applets-networkmanagement](https://aur.archlinux.org/packages/kdeplasma-applets-networkmanagement/) desde aur.

Si tiene instalado tanto el widget Plasma como `nm-applet` y no desea iniciar `nm-applet` cuando usa KDE, añada la siguiente línea a `/etc/xdg/autostart/nm-applet.desktop`:

```
NotShowIn=KDE

```

Véase [Userbase page](http://userbase.kde.org/NetworkManagement) para obtener más información.

### XFCE

El paquete [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) no tendrá ningún problema en XFCE, pero para ver las notificaciones, *incluidos los mensajes de error*, necesitará `nm-applet`, una específica implementación de Freedesktop (consulte [Proyecto Galapago](http://www.galago-project.org/specs/notification/0.9/index.html)) para mostrar las notificaciones. Para activar las notificaciones, instale [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd), un paquete que proporciona una implementación de la especificación.

Sin un demonio de notificación, `nm-applet` generará los siguientes errores en stdout/stderr:

```
(nm-applet:24209): libnotify-WARNING **: Failed to connect to proxy
** (nm-applet:24209): WARNING **: get_all_cb: couldn't retrieve
system settings properties: (25) Launch helper exited with unknown
return code 1.
** (nm-applet:24209): WARNING **: fetch_connections_done: error
fetching connections: (25) Launch helper exited with unknown return
code 1.
** (nm-applet:24209): WARNING **: Failed to register as an agent:
(25) Launch helper exited with unknown return code 1

```

`nm-applet` funciona normalmente, pero sin notificaciones.

Si nm-applet no le pide la contraseña cuando se conecta a las nuevas redes wifi, e inmediatamente después se desconecta, es probable que tenga que instalar [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring).

### Openbox

Para que NetworkManager funcione correctamente en Openbox, el applet de GNOME requiere el demonio de notificación [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd), por la misma razón que en XFCE, y el paquete [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme) para poder mostrar el applet en la bandeja del sistema.

Si desea guardar los datos de autentificación (Wireless/DSL) instale y configure [gnome-keyring](/index.php/Gnome-keyring "Gnome-keyring").

`nm-applet` instala el archivo autostart en `/etc/xdg/autostart/nm-applet.desktop`. Si tiene problemas con él (por ejemplo, `nm-applet` se inicia dos veces o no se inicia en absoluto), consulte [[Openbox#autostart] o [[1]](https://bbs.archlinux.org/viewtopic.php?pid=993738) para conocer la solución.

### Otros escritorios y gestores de ventanas

En todos los demás casos, se recomienda usar el applet de GNOME. Deberá asegurarse que tiene instalado el paquete [gnome-icon-theme](https://www.archlinux.org/packages/?name=gnome-icon-theme) para poder ver el applet.

Para guardar información confidencial sobre las conexiones instale y configure [gnome-keyring](/index.php/Gnome-keyring "Gnome-keyring").

Para ejecutar `nm-applet` en un entorno sin una bandeja de sistema, puede utilizar [trayer](https://www.archlinux.org/packages/?name=trayer) o [stalonetray](https://www.archlinux.org/packages/?name=stalonetray). Por ejemplo, puede agregar un script como este a su propia ruta:

 `nmgui` 
```
 #!/bin/sh
 nm-applet    > /dev/null 2>/dev/null &
 stalonetray  > /dev/null 2>/dev/null
 killall nm-applet

```

Al cerrar la ventana de stalonetray, cierra `nm-applet` también, así que no consume memoria extra una vez que haya terminado con la configuración de red.

### Desde la línea de órdenes

La paquete [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) contiene [nmcli](http://manpages.ubuntu.com/manpages/maverick/man1/nmcli.1.html) desde la versión 0.8.1.

## Configuración

NetworkManager requiere algunos pasos adicionales para ser capaz de ejecutarse correctamente.

Antes de comenzar, compruebe que `/etc/hosts` está configurado correctamente. Si ya ha intentado conectarse antes de realizar este paso, NetworkManager puede haberlo modificado. He aquí un ejemplo de línea hostname en `/etc/hosts`:

 `/etc/hosts` 
```
127.0.0.1 localhost
::1       localhost

```

En caso de tener nss-myhostname apagado, la línea sería:

 `/etc/hosts` 
```
127.0.0.1 my-laptop localhost
::1       my-laptop localhost

```

**Nota:** Puede ser una buena idea usar `systemctl --type=service` para asegurarse que ningún otro servicio está en ejecución para configurar la red. La existencia de varios servicios de gestión de redes entrarán en conflicto.

### Activar NetworkManager

Una vez que el demonio NetworkManager se ha iniciado, se conectará automáticamente a cualesquiera «conexiones del sistema» disponibles que estén configuradas. Las «conexiones del usuario» o las conexiones no configuradas necesitarán `nmcli` o un applet para la configuración y la conexión.

Puede activar NetworkManager para que se inicie en el arranque con la siguiente orden:

 `# systemctl enable NetworkManager` 

Puede iniciar el demonio NetworkManager inmediatamente con la siguiente orden:

 `# systemctl start NetworkManager` 

#### Evitar advertencias

NetworkManager imprimirá, probablemente sin sentido, [advertencias (Bug#34971)](https://bugs.archlinux.org/task/34971) para el registro del sistema, cuando [NetworkManager-dispatcher.service](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") y [ModemManager.service](https://www.archlinux.org/packages/?name=modemmanager) no estén activados. Para mantener el registro limpio y suprimir estos mensajes, active ambos servicios, incluso si no son requeridos por el entorno:

 `# systemctl enable NetworkManager-dispatcher.service && systemctl enable ModemManager.service`  `# systemctl start NetworkManager-dispatcher.service && systemctl start ModemManager.service` 

### Activar NetworkManager Wait Online

Si tiene servicios que pueden fallar si se inician antes de que se abra la red, tiene que usar `NetworkManager-wait-online.service` además del servicio de NetworkManager. Esto, sin embargo, casi nunca es necesario, ya que la mayoría de los demonios de red se ponen en marcha correctamente, incluso si la red no se ha configurado todavía.

Puede activar NetworkManager Wait Online en el arranque con la siguiente orden:

 `# systemctl enable NetworkManager-wait-online` 

En algunos casos, el servicio puede que no se inicie con éxito en el arranque:

```
 NetworkManager-wait-online.service: main process exited, code=exited, status=1/FAILURE
 Failed to start Network Manager Wait Online
 Unit NetworkManger-wait-online.service entered failed state
 Starting Network.
 Reached target Network.

```

Esto se debe a la configuración del tiempo de espera en `/usr/lib/systemd/system/NetworkManager-wait-online.service` que es corto. Cambie el tiempo de espera predeterminado de 30 a un valor más alto.

### Configurar permisos PolicyKit

Véase [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") para la creación de una sesión de trabajo.

Con una sesión de trabajo, tiene varias opciones para la concesión de los privilegios necesarios para NetworkManager:

*Opción 1.* Ejecute un agente de autenticación [PolicyKit](/index.php/PolicyKit "PolicyKit") cuando se conecte, como `/usr/lib/polkit-gnome/polkit-gnome-authentication-agent-1` (es parte del paquete [polkit-gnome](https://www.archlinux.org/packages/?name=polkit-gnome)). Se le pedirá la contraseña cada vez que agregue o quite una conexión de red.

*Opción 2.* Añada su usuario al grupo `wheel`. No tendrá que introducir su contraseña, pero necesitará garantizar los permisos particulares a los usuarios tales como la capacidad de usar [sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)") sin introducir la contraseña de root.

*Opción 3.* Añádase al grupo `network` y cree el siguiente archivo

 `/etc/polkit-1/rules.d/50-org.freedesktop.NetworkManager.rules` 
```
polkit.addRule(function(action, subject) {
  if (action.id.indexOf("org.freedesktop.NetworkManager.") == 0 && subject.isInGroup("network")) {
    return polkit.Result.YES;
  }
});
```

Todos los usuarios del grupo `network` podrán añadir y eliminar redes sin contraseña. Esto no funcionará bajo systemd si no se tiene una sesión activa con [systemd-logind](/index.php/Systemd#Using_systemd-logind "Systemd").

### Servicios de red con NetworkManager dispatcher

Hay algunos servicios de red que no se desean ejecutar hasta que NetworkManager crea la interfaz. Algunos ejemplos son [OpenNTPD](/index.php/OpenNTPD "OpenNTPD") y diversos tipos de montajes de sistemas de archivos de red (por ejemplo, **netfs**). NetworkManager tiene la capacidad de iniciar estos servicios cuando se conecta a una red y detenerlos cuando se desconecta. Para utilizar esta característica necesita iniciar/activar el [servicio](/index.php/Daemon "Daemon") NetworkManager-dispatcher:

Una vez que la función está activa, se pueden añadir los scripts apropiados a la carpeta `/etc/NetworkManager/dispatcher.d`. Estos scripts necesitan los permisos de ejecución del usuario. Por seguridad, es una buena práctica que sean propiedad de **root:root** y con permisos de escritura únicamente por el propietario.

Los scripts se ejecutan en orden alfabético durante la fase de conexión, y en orden alfabético inverso durante la fase de desconexión. Reciben dos argumentos: el nombre de la interfaz (por ejemplo, *eth0*) y el estado (*up* o *down* para las interfaces y vpn-up o vpn-down para las conexiones vpn). A fin de garantizar el orden en que vayan surgiendo, es común el uso de caracteres numéricos puestos como prefijos delante del nombre del script (por ejemplo, `10_portmap` o `30_netfs` (que asegura que el mapeador de puertos se levante antes de que se intente montar NFS).

**Advertencia:**

*   Por razones de seguridad, debe desactivar el acceso de escritura para el grupo y otro. Por ejemplo, utilice el filtro 755\. En otro caso, puede ser denegada la ejecución del script con el mensaje de error: «nm-dispatcher.action: Script could not be executed: writable by group or other, or set-UID» en `/var/log/messages.log`.
*   Si se conecta a redes extranjeras o públicas, debe estar al tanto de cuáles son los servicios que están empezando y qué servidores se espera que estén disponibles para ellos al conectarse. Podría crear un agujero de seguridad al iniciar los servicios equivocados mientras está conectado a una red pública.

#### Evitar el tiempo de espera de tres segundos

Si lo anterior funciona, entonces esta sección no es relevante. Sin embargo, existe un problema general en relación con la ejecución del script dispatcher que se demora más de tres segundos antes de ser ejecutado. NetworkManager usa un tiempo de espera interna de 3 segundos (véase [Bugtracker](https://bugzilla.redhat.com/show_bug.cgi?id=982734) para más información) y automáticamente termina los scripts que tardan más de 3 segundos al acabar. En estos casos, el archivo de servicio dispatcher, ubicado en `/usr/lib/systemd/system/NetworkManager-dispatcher.service`, tiene que ser modificado para permanecer activo después de arrancar. Cree el archivo de servicio `/etc/systemd/system/NetworkManager-dispatcher.service` con el siguiente contenido:

```
.include /usr/lib/systemd/system/NetworkManager-dispatcher.service
[Service]
RemainAfterExit=yes

```

A continuación, active el script `NetworkManager-dispatcher` modificado.

#### Iniciar OpenNTPD

El siguiente ejemplo de script inicia el demonio OpenNTPD cuando una interfaz se conecta. Guarde el archivo como `/etc/NetworkManager/dispatcher.d/20_openntpd` y hágalo ejecutable.

```
#!/bin/sh
interface=$1 status=$2
case $status in
  up)
    systemctl start openntpd
    ;;
  down)
    if ! nm-tool | awk '/State:/{print $2}' | grep -qs ^connected; then
      systemctl stop openntpd
    fi
    ;;
esac
}}

```

#### Montar carpeta remota con sshfs

Dado que el script viene ejecutado en un entorno muy restrictivo, es necesario exportar la variable `SSH_AUTH_SOCK` para poder conectarse al propio agente SSH. Hay diferentes maneras para lograr esto, vea [este enlace](https://bbs.archlinux.org/viewtopic.php?pid=1042030#p1042030) para más información. El siguiente ejemplo funciona con [gnome-keyring](/index.php/Gnome-keyring "Gnome-keyring"), y le pedirá la contraseña si no está desbloqueada ya. En caso de que NetworkManager se conecte automáticamente al iniciar sesión, es probable gnome-keyring aún no se haya iniciado, de modo que la exportación fallará (de ahí que entre en modo de espera). Conocer la `UUID` necesaria para comprobar que coincide se puede encontrar con la orden `nmcli con status` o `nmcli con list`.

```
#!/bin/sh
USER='username'
REMOTE='user@host:/remote/path'
LOCAL='/local/path'

interface=$1 status=$2
if [ "$CONNECTION_UUID" = "*uuid*" ]; then
  case $status in
    up)
      export SSH_AUTH_SOCK=$(find /tmp -maxdepth 1 -type s -user "$USER" -name 'ssh')
      su "$USER" -c "sshfs $REMOTE $LOCAL"
      ;;
    down)
      fusermount -u "$LOCAL"
      ;;
  esac
fi

```

#### Usar dispatcher para conectarse a VPN despues de establecer una conexión de red

En este ejemplo, conectaremos automáticamente a una conexión VPN, previamente definida en NetworkManager, después de conectarse a una red Wi-Fi específica. Lo primero que hay que hacer es crear el script dispatcher que define el comportamiento a realizar después de conectarse a la red.

	1\. Cree el script dispatcher:

 `/etc/NetworkManager/dispatcher.d/vpn-up` 
```
#!/bin/sh
VPN_NAME="name of VPN connection defined in NetworkManager"
ESSID="wifi network ESSID (not connection name)"

interface=$1 status=$2
case $status in
  up|vpn-down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      nmcli con up id "$VPN_NAME"
    fi
    ;;
  down)
    if iwgetid | grep -qs ":\"$ESSID\""; then
      if nmcli con status id "$VPN_NAME" | grep -qs activated; then
        nmcli con down id "$VPN_NAME"
      fi
    fi
    ;;
esac

```

Recuerde que debe hacerlo ejecutable con `chmod +x` y establecer la conexión VPN a disposición de todos los usuarios.

Intentando conectar usando esta configuración, se producirá un error y NetworkManager mostrará un mensaje de 'no valid VPN secrets', debido al [método para guardar secretos de VPN](http://projects.gnome.org/NetworkManager/developers/migrating-to-09/secrets-flags.html) que nos lleva al paso 2:

	2\. Edite el archivo de configuración de la conexión VPN para señalar a NetworkManager como el almacen de los parámetros confidenciales propios en vez incluirlo en el depósito de claves [que será inaccesible para el usuario root](https://bugzilla.redhat.com/show_bug.cgi?id=710552): abra `/etc/NetworkManager/system-connections/<name of your VPN connection>` y modifique `password-flags` y `secret-flags` de `1` a `0`.

Otra forma es poner directamente la contraseña en el archivo de configuración añadiendo la sección `vpn-secrets`:

```
 [vpn]
 ....
 password-flags=0

 [vpn-secrets]
 password=your_password

```

**Nota:** Ahora es necesario volver a editar la configuración de la conexión de NetworkManager y volver a introducir las contraseñas/secretos de VPN.

### Configuración del proxy

NetworkManager no gestona directamente la configuración del proxy, pero si está usando GNOME, puede usar [proxydriver](http://marin.jb.free.fr/proxydriver/), el cual se encarga de configurar el proxy utilizando la información de NetworkManager. Puede encontrar el paquete [proxydriver](https://aur.archlinux.org/packages/proxydriver/) en [AUR](/index.php/AUR "AUR").

Para que proxydriver pueda cambiar la configuración del proxy, tendrá que ejecutar la siguiente orden, como parte del proceso de inicio de GNOME (Sistema -> Preferencias -> Aplicaciones de inicio):

```
xhost +si:localuser:your_username

```

Consulte: [Proxy settings](/index.php/Proxy_settings "Proxy settings")

## Comprobación

Los applets de NetworkManager están diseñados para cargarse al iniciar sesión, por lo que no debería ser objeto de configuración adicional para la mayoría de los casos. Si ya ha desactivado la configuración de red existente y ha desconectado la red, ahora puede comprobar si NetworkManager funciona. El primer paso es [iniciar](/index.php/Daemon "Daemon") el demonio *networkmanager*.

Algunos applets proveen un archivo `.desktop` para que el applet de NetworkManager se puede cargar a través del menú de la aplicación. Si no lo hace, tendrá que descubrir la orden para iniciarlo o reiniciar sesión otra vez para iniciar el applet. Una vez que el applet se inicia, es probable que comience a interrogar y ordenar conexiones de red, para después autoconfigurarse con un servidor DHCP.

Para iniciar el applet de GNOME en los gestores de ventanas no compatibles con xdg como [Awesome](/index.php/Awesome "Awesome"):

```
nm-applet --sm-disable &

```

Para las direcciones IP estáticas, tendrá que configurar NetworkManager para que las identifique. El proceso suele implicar pulsar con el botón secundario del ratón en el applet y seleccionar un menú similar a 'Editar las conexiones'.

## Solución de problemas

Algunas soluciones para los problemas más comunes.

### Al usar nm-applet, las conexiones a redes wifi no solicitan contraseña y se desconectan

Esto ocurre cuando no hay instalado ningún paquete keyring. Una solución fácil es instalar [gnome-keyring](https://www.archlinux.org/packages/?name=gnome-keyring).

### Problemas con el tráfico de datos a través del canal PPTP

Puede suceder que el login a la conexión PPTP se haga de manera correcta, y vea que la interfaz ppp0 tiene una IP VPN exacta, y, sin embargo, no puede hacer ping a ninguna IP remota. Ello es debido a la falta del soporte MPPE (Microsoft Point-to-Point Encryption) que se encuentra en el paquete pppd de Arch. Se recomienda probar primero con el paquete estándar [ppp](https://www.archlinux.org/packages/?name=ppp) de Arch que podría funcionar como es debido.

Para resolver el problema será suficiente instalar [ppp-mppe](https://aur.archlinux.org/packages/ppp-mppe/) desde [AUR](/index.php/AUR "AUR").

### Desactivada la gestión de red

A veces, cuando NetworkManager se apaga, el archivo del PID (estado) no se retira y recibirá el mensaje de «Network management disabled». Si esto sucede, tendrá que quitarlo manualmente:

```
# rm /var/lib/NetworkManager/NetworkManager.state

```

Si esto sucede en el arranque, se puede añadir una acción al archivo `/etc/rc.local` para que lo retire en el arranque:

```
nmpid=/var/lib/NetworkManager/NetworkManager.state
[ -f $nmpid ] && rm $nmpid
```

### Personalizar resolv.conf

Véase la página principal: [resolv.conf](/index.php/Resolv.conf "Resolv.conf"). También asegúrese de que NetworkManager utiliza [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) y no [dhclient](https://www.archlinux.org/packages/?name=dhclient). Si desea utilizar [dhclient](https://www.archlinux.org/packages/?name=dhclient), puede probar el paquete [networkmanager-dispatch-resolv](https://aur.archlinux.org/packages/networkmanager-dispatch-resolv/) disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

### Problemas con DHCP

Si tiene problemas para obtener una dirección IP mediante DHCP, intenta agregar lo que sigue al archivo `/etc/dhclient`:

```
 interface "eth0" {
   send dhcp-client-identifier 01:aa:bb:cc:dd:ee:ff;
 }

```

Donde `aa:bb:cc:dd:ee:ff` es la dirección MAC del NIC (la tarjeta de red). La dirección MAC se puede encontrar utilizando la orden `ip link show eth0` proporcionada por el paquete [iproute2](https://www.archlinux.org/packages/?name=iproute2).

Con algunos routers, resultará imposible conectarse correctamente, a menos que comente la línea:

```
require dhcp_server_identifier

```

en `/etc/dhcpcd.conf` (advierta que este archivo es un archivo distinto de `dhcpd.conf`). Esto no debería causar problemas a menos que tenga varios servidores DHCP en la red (no habitual); consulte [esta página](http://technet.microsoft.com/en-us/library/cc977442.aspx) para obtener más información.

### Problemas con hostname (*«nombre del equipo»*)

Dependerá de los plugins utilizados por NetworkManager, los cuales determinarán si el nombre del equipo se envía o no a un router para conectarse. El plugin genérico «keyfil» no envía, por defecto, el nombre del equipo en la configuración.

#### Opción 1: modificar keyfil en NetworkManager.conf

Para hacer que transmita el nombre del equipo, agregue lo siguiente al archivo:

 `/etc/NetworkManager/NetworkManager.conf` 
```
[keyfile]
hostname=*su_nombre-del-equipo*
```

Las opciones en `[keyfile]` se aplicarán a las conexiones de red en la ruta predeterminada `/etc/NetworkManager/system-connections`.

#### Opción 2: configurar dhclient para poner el nombre del equipo en el servidor DHCP

Otra opción es configurar el cliente DHCP, que NetworkManager iniciará automáticamente, para que envíe el nombre del equipo. NetworkManager utiliza [dhclient](https://www.archlinux.org/packages/?name=dhclient) si está instalado y, en su defecto, recurre a [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd). Para hacer que *dhclient* envíe el nombre del equipo hay que establecer una opción non-default, que permita que *dhcpcd* envíe el nombre del equipo por defecto.

*   En primer lugar, compruebe qué cliente DHCP está utilizando (*dhclient* en este ejemplo):

 `# journalctl -b | egrep "dhclient|dhcpcd"` 
```
...
Nov 17 21:03:20 zenbook dhclient[2949]: Nov 17 21:03:20 zenbook dhclient[2949]: Bound to *:546
Nov 17 21:03:20 zenbook dhclient[2949]: Listening on Socket/wlan0
Nov 17 21:03:20 zenbook dhclient[2949]: Sending on   Socket/wlan0
Nov 17 21:03:20 zenbook dhclient[2949]: XMT: Info-Request on wlan0, interval 1020ms.
Nov 17 21:03:20 zenbook dhclient[2949]: RCV: Reply message on wlan0 from fe80::126f:3fff:fe0c:2dc.

```

*   Copie el archivo de configuración de referencia `/usr/share/dhclient/dhclient.conf.example` a `/etc/dhclient.conf`:

```
# cp /usr/share/dhclient/dhclient.conf.example /etc/dhclient.conf

```

*   Echa un vistazo al archivo -realmente solo nos interesa una línea y que dhclient utiliza por defecto (de hecho, es la opción que utiliza si el archivo no existe)- para conocer otras opciones. La línea importante es esta:

 `/etc/dhclient.conf`  `send host-name = pick-first-value(gethostname(), "ISC-dhclient");` 

*   Fuerce una reactualización de las direcciones IP, y, a continuación, debería ver el nombre de su equipo en el servidor DHCP.

#### Opción 3: configurar NetworkManager para utilizar dhcpcd

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) y dígale a NetworkManager que lo utilice:

 `/etc/NetworkManager/NetworkManager.conf`  `dhcp=dhcpcd` 

Después [reinicie](/index.php/Systemd#Using_units "Systemd") `NetworkManager.service`.

### Falta la ruta predeterminada

Si con un sistema de KDE4, no se creó ninguna ruta por defecto a la hora de establecer conexiones inalámbricas con NetworkManager, en general se puede resolver modificando la configuración de la ruta de la conexión inalámbrica para eliminar la selección por defecto «Use only for resources on this connection».

### Modem 3G no detectado

Si NetworkManager (desde v0.7.999) no detecta el módem 3G, pero todavía se puede conectar usando [wvdial](/index.php/Wvdial "Wvdial"), pruebe a instalar el paquete [modemmanager](https://www.archlinux.org/packages/?name=modemmanager) y reinicie el demonio NetworkManager con `networkmanager rc.d restart`. También puede ser necesario volver a conectar o reiniciar el módem. Esta utilidad proporciona soporte para el hardware no incluido por defecto en la base de datos de NetworkManager.

### Desconexión de WLAN en portátiles

A veces, NetworkManager no funciona cuando se deshabilita el adaptador WiFi con el interruptor del portátil y se trata de activar de nuevo después. Esto suele ser debido a un problema con `rfkill`:

```
$ watch -n1 rfkill list all

```

para comprobar si el controlador informa `rfkill` sobre el estado del adaptador inalámbrico. Si un identificador permanece bloqueado después de conectar el adaptador se puede tratar de desbloquearlo de forma manual con la orden siguiente (donde X es el número del identificador proporcionado por la salida de la orden anterior):

```
# rfkill event unblock X

```

### Ajustes de la IP estática restaurando a DHCP

Debido a un error aún no solucionado, al cambiar las conexiones por defecto para la IP estática, `nm-applet` no guarda correctamente el cambio de configuración y vuelve a DHCP automático.

Para solucionar este problema hay que editar la conexión por defecto (por ejemplo, «Auto eth0») en `nm-applet`, cambiar el nombre de la conexión (por ejemplo, «mi eth0»), desactivar la casilla «Disponible para todos los usuarios», modificar la configuración de IP estáticas como se desee, y pulsar en **Aplicar**. Esto guardará la nueva conexión con el nombre dado.

A continuación, tendrá que asegurarse que la conexión por defecto no se conecte automáticamente. Para ello, ejecute `nm-connection-editor` (*no* como root). En el editor de conexión, modifique la conexión por defecto (por ejemplo, «Auto eth0») y desmarque la opción «Conectar automáticamente». Pulse **Aplicar** y cierre el editor de conexión.

### No se pueden editar las conexiones como usuario normal

Véase [#Set_up_PolicyKit_permissions](#Set_up_PolicyKit_permissions).

### Eliminar una red oculta

Obviamente, una red oculta no se muestra en la lista de selección de la GUI Wireless, por lo que no puede ser eliminada desde la interfaz gráfica de usuario. Puede eliminarla usando la siguiente orden:

```
# rm /etc/NetworkManager/system-connections/[SSID]

```

Dicha orden funciona para cualquier otra conexión.

### VPN no funciona en Gnome

Al configurar openconnect o conexiones vpnc en NetworkManager mientras usa Gnome, a veces puede no ver el cuadro de diálogo emergente, apareciendo el siguiente error en /var/log/errors.log:

```
localhost NetworkManager[399]: <error> [1361719690.10506] [nm-vpn-connection.c:1405] get_secrets_cb(): Failed to request VPN secrets #3: (6) No agents were available for this request.

```

Esto es causado por el Applet NM de Gnome esperando scripts de dialogos para pasar a /usr/lib/gnome-shell, cuando los paquetes de NetworkManager se colocan en /usr/lib/networkmanager. Como un arreglo «temporal» (este error ha sido tratado por un tiempo), hagan el enlace siguiente(s):

```
# Para OpenConnect
ln -s /usr/lib/networkmanager/nm-openconnect-auth-dialog /usr/lib/gnome-shell/ 

```

```
# Para VPNC (es decir, Cisco VPN)
ln -s /usr/lib/networkmanager/nm-vpnc-auth-dialog /usr/lib/gnome-shell/

```

Esto puede ser necesario hacerlo para cualquier otro plugin VPN NM también, pero estos son los dos más comunes.

## Consejos y trucos

### Compartir la conexión a Internet a través de Wi-Fi

Puede compartir su conexión a Internet (por ejemplo: 3G o por cable) con unos pocos clics utilizando nm. Necesitará el apoyo de una tarjeta wifi (las tarjetas basadas en Atheros AR9xx o, al menos, AR5xx son probablemente la mejor opción).

#### Ad-hoc

*   [Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el paquete [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) para ser capaz de compartir la conexión.
*   Un archivo dnsmasq.conf personalizado puede interferir con nm (aunque esta afirmación no se ha verificado).
*   Clicar sobre nm-applet → Crear red inalámbrica nueva.
*   Siga el asistente (asegúrese de usar una contraseña de 5 o 13 caracteres de extensión, otras longitudes fallarán).
*   Los ajustes se guardarán para la próxima vez que los necesite.

#### Real AP

El soporte para la modalidad de infraestructura (necesaria por los teléfonos Andoid, que no son compatibles con ad-hoc intencionadamente) no está apoyado actualmente por NetworkManager, pero está en desarrollo activo ...

Véase: [http://fedoraproject.org/wiki/Features/RealHotspot](http://fedoraproject.org/wiki/Features/RealHotspot)

### Comprobar la activación de la red en el interior de un proceso cron o script

Algunos tareas de cron requieren de la red para poder funcionar. Es posible que desee evitar la ejecución de estos trabajos cuando la red no funciona. Para ello, agregue un **if** de prueba para las consultas de redes con `nm-tool` de NetworkManager y compruebe el estado de las redes. La prueba tiene éxito si se muestra aquí cualquier interfaz activa, y fallida si no lo están. Esto es conveniente para los ordenadores portátiles que pueden tener conexión cableada, conexión inalámbrica, o podrían estar fuera de red.

```
if [ `nm-tool|grep State|cut -f2 -d' '` == "connected" ]; then
       #Whatever you want to do if the network is online
else
       #Whatever you want to do if the network is offline - note, this and the else above are optional
fi

```

Es útil para un script `cron.hourly` que ejecuta `fpupdate` para la actualización del escáner de firmas del antivirus F-Prot, por ejemplo. Otra forma de ser útil, con una pequeña modificación, podría ser diferenciar entre redes que utilizan diferentes partes de la salida `nm-tool`, por ejemplo, en cuanto que la red inalámbrica activa se indica con un asterisco, es posible, con la utilización de *grep*, cambiar el nombre de la red orientando la busqueda de *grep* a la red del asterisco.

### Desbloquear automáticamente keyring después del login

#### GNOME

1.  Haga clic con el botón derecho en el icono `nm-applet` del panel y seleccione *«Configuración de la red»* y abra la pestaña *«Inalámbrica»*.
2.  Seleccione la conexión que desee y haga clic en el botón *«Configuración»*.
3.  Marque las casillas *«Conectar automáticamente»* y *«Disponible para todos los usuarios»*.

Cierre la sesión y vuelva a entrar para completar el proceso.

**Nota:** El siguiente método es anticuado y puede no funcionar en todos los equipos.

*   En `/etc/pam.d/gdm` (o el demonio correspondiente en `/etc/pam.d`), añada la siguiente línea al final de los bloques «auth» y «session», para el caso de que no existan:

```
 auth            optional        pam_gnome_keyring.so
 session         optional        pam_gnome_keyring.so  auto_start

```

*   En `/etc/pam.d/passwd`, use la siguiente línea para el bloque del «password»:

```
 password    optional    pam_gnome_keyring.so

```

	La próxima vez que inicie sesión, debería preguntarle si desea que la contraseña se desbloquee automáticamente al iniciar sesión.

#### KDE

**Nota:** Consulte [http://live.gnome.org/GnomeKeyring/Pam](http://live.gnome.org/GnomeKeyring/Pam) para mayor información, y si se utiliza KDE con KDM, es posible usar [pam-keyring-tool](https://aur.archlinux.org/packages/pam-keyring-tool/) disponible desde [AUR](/index.php/AUR "AUR").

Coloque un script como el siguiente en `~/.kde4/Autostart`:

```
 #!/bin/sh
 echo PASSWORD | /usr/bin/pam-keyring-tool --unlock --keyring=default -s

```

Un script similar debe funcionar también con Openbox, LXDE, etc.

#### SLiM login manager

Véase [SLiM#SLiM and Gnome Keyring](/index.php/SLiM#SLiM_and_Gnome_Keyring "SLiM").

### Ignorar dispositivos específicos

A veces se puede desear que NetworkManager ignore algunos dispositivos específicos y no trate de configurar las direcciones y las rutas para ellos.

Puede ignorar los dispositivos por la dirección MAC mediante la siguiente configuración en `/etc/NetworkManager/NetworkManager.conf` :

```
[keyfile]
unmanaged-devices=mac:00:22:68:1c:59:b1;mac:00:1E:65:30:D1:C4

```

Después de poner esto [reinicie](/index.php/Daemon_(Espa%C3%B1ol) "Daemon (Español)") NetworkManager, y con ello debería ser capaz de configurar las interfaces de NetworkManager sin alterar lo que ha establecido.

### Conectar más rápido

#### Deshabilitar IPv6

Las conexiones lentas o reconexiones a la red pueden ser debidas a las consultas superfluas de NetworkManager a las IPv6\. Si no hay soporte para IPv6 en la red local, la conexión a una red puede tardar más de lo normal, mientras que NetworkManager intenta establecer una conexión IPv6 con resultado final de «time out». La solución es desactivar IPv6 en NetworkManager lo que hará que la conexión de red sea más rápida. Esto tiene que hacerse una sola vez para cada red a la cual se conecte.

*   Haga clic en el icono del estado de la red.
*   Haga clic en «Configuración de la red».
*   Vaya a la pestaña «Cableada» o «Inalámbrica», según corresponda.
*   Seleccione el nombre de la red.
*   Haga clic en «Configuración».
*   Vaya a «Ajustes de IPv6».
*   En el botón desplegable «Método», elija la opción «Ignorar».
*   Haga clic en «Guardar».

#### Acelerar DHCP mediante la desactivación de ARP sondeando DHCPCD

`dhcpcd` contiene una implementación de una recomendación de la norma DHCP ([RFC2131 sección 2.2](http://www.ietf.org/rfc/rfc2131.txt)) para comprobar a través de ARP si la dirección IP asignada realmente no está en uso. Puede parecer innecesario en una red doméstica, pero puede ahorrar alrededor de 5 segundos en cada conexión añadiendo la siguiente línea a `/etc/dhcpcd.conf`:

```
noarp

```

Esto equivale a lanzar `dhcpcd` con el flag `--noarp`, lo cual desactiva el sondeo a ARP, acelerando las conexiones con DHCP.

#### Usar servidores OpenDNS

Cree el archivo `/etc/resolv.conf.opendns` con los nombres de los servidores:

```
nameserver 208.67.222.222
nameserver 208.67.220.220

```

o utilizar los servidores DNS de Google, porque la gente ha estado recibiendo anuncios por los servidores de OpenDNS últimamente:

```
nameserver 8.8.8.8
nameserver 8.8.4.4

```

Y, de este modo, tiene el dispatcher que reemplaza los servidores DHCP descubiertos con los de OpenDNS:

 `/etc/NetworkManager/dispatcher.d/dns-servers-opendns` 
```
#!/bin/bash
# Use OpenDNS servers over DHCP discovered servers

cp -f /etc/resolv.conf.opendns /etc/resolv.conf
```

Haga el script ejecutable:

```
# chmod +x /etc/NetworkManager/dispatcher.d/dns-servers-opendns

```

### Activar el almacenamiento en caché de DNS

Las peticiones de DNS se puede acelerar si almacenamos en caché las solicitudes anteriores a nivel local para su posterior consulta. NetworkManager tiene un plugin para activar la caché DNS utilizando dnsmasq, pero no está activado en la configuración predeterminada. Es, sin embargo, fácil de activar siguiente las instrucciones de abajo.

Comience [instalando](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq). Después, edite el archivo `/etc/NetworkManager/NetworkManager.conf` y, seguidamente, añada la línea siguiente debajo de la sección `[main]`:

```
dns=dnsmasq

```

Ahora solo queda reiniciar NetworkManager o reiniciar el sistema. NetworkManager iniciará automáticamente dnsmasq y añadirá 127.0.0.1 al archivo `/etc/resolv.conf`. Los servidores DNS reales pueden ser encontrados en `/var/run/NetworkManager/dnsmasq.conf`. Puede verificar que dnsmasq está siendo utilizado buscando DNS dos veces con dig y comprobando el servidor y los tiempos de consulta.