Artículos relacionados

*   [Network Configuration (Español)](/index.php/Network_Configuration_(Espa%C3%B1ol) "Network Configuration (Español)")
*   [Wireless Setup (Español)](/index.php/Wireless_Setup_(Espa%C3%B1ol) "Wireless Setup (Español)")
*   [Netctl (Español)](/index.php/Netctl_(Espa%C3%B1ol) "Netctl (Español)")
*   [NetworkManager (Español)](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)")

[Wicd](http://www.wicd.net/) es un gestor de conexiones de red que puede manejar interfaces inalámbricas y cableadas, de forma similar y alternativa a [NetworkManager](/index.php/NetworkManager_(Espa%C3%B1ol) "NetworkManager (Español)"). Wicd está escrito en [Python](/index.php/Python "Python") y [GTK+](/index.php/GTK%2B "GTK+"), por lo que necesita de la instalación de un menor número de dependencias repecto de otros gestores de red. Alternativamente, está disponible una versión de Wicd para [KDE](/index.php/KDE "KDE"), escrito en [Qt](/index.php/Qt "Qt"), desde el repositorio [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"). Wicd también se puede ejecutar desde el terminal en una interfaz diseñada con las bibliotecas curses, que no requiere una sesión de servidor X, ni área de notificación (véase [#Ejecutar Wicd](#Ejecutar_Wicd)).

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
    *   [1.1 Paquete base](#Paquete_base)
    *   [1.2 Cliente GTK+](#Cliente_GTK.2B)
    *   [1.3 Cliente KDE](#Cliente_KDE)
    *   [1.4 Notificaciones](#Notificaciones)
    *   [1.5 Alternativa](#Alternativa)
*   [2 Para empezar](#Para_empezar)
    *   [2.1 Configuración inicial](#Configuraci.C3.B3n_inicial)
    *   [2.2 Ejecutar Wicd en un entorno de escritorio](#Ejecutar_Wicd_en_un_entorno_de_escritorio)
    *   [2.3 Ejecutar Wicd en modo texto](#Ejecutar_Wicd_en_modo_texto)
    *   [2.4 Inicio automático](#Inicio_autom.C3.A1tico)
    *   [2.5 Scripts](#Scripts)
        *   [2.5.1 Detener los ataques de ARP spoofing](#Detener_los_ataques_de_ARP_spoofing)
        *   [2.5.2 Cambiar la dirección MAC con macchanger](#Cambiar_la_direcci.C3.B3n_MAC_con_macchanger)
*   [3 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [3.1 Fallo importando pynotify, notificaciones desactivadas](#Fallo_importando_pynotify.2C_notificaciones_desactivadas)
    *   [3.2 Mensaje de error de conexión con Dbus](#Mensaje_de_error_de_conexi.C3.B3n_con_Dbus)
    *   [3.3 Problemas después de actualizar el paquete](#Problemas_despu.C3.A9s_de_actualizar_el_paquete)
    *   [3.4 Algunas notas sobre front-end gráficos para sudo](#Algunas_notas_sobre_front-end_gr.C3.A1ficos_para_sudo)
    *   [3.5 Configurar wicd para trabajar con eduroam](#Configurar_wicd_para_trabajar_con_eduroam)
    *   [3.6 Dos procesos wicd-client (y eventualmente dos iconos en la bandeja del sistema)](#Dos_procesos_wicd-client_.28y_eventualmente_dos_iconos_en_la_bandeja_del_sistema.29)
    *   [3.7 Contraseña incorrecta usando PEAP con TKIP/MSCHAPV2](#Contrase.C3.B1a_incorrecta_usando_PEAP_con_TKIP.2FMSCHAPV2)
    *   [3.8 Wicd no puede obtener una dirección IP de WLAN](#Wicd_no_puede_obtener_una_direcci.C3.B3n_IP_de_WLAN)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Instalación

### Paquete base

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") [wicd](https://www.archlinux.org/packages/?name=wicd), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Incluye todo lo necesario para ejecutar el demonio wicd, el cliente `wicd-cli` y la interfaz de terminal `wicd-curses`.

### Cliente GTK+

Para una interfaz GTK+, instale [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk), disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)"). Incluye todo lo necesario para ejecutar la interfaz GTK de wicd y el archivo de inicio automático para que el icono aparezca en la bandeja del sistema.

### Cliente KDE

Para una interfaz KDE, instale [wicd-kde](https://aur.archlinux.org/packages/wicd-kde/), disponible en el repositorio [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

### Notificaciones

Para activar las notificaciones visuales sobre el estado de la red, es necesario instalar [notification-daemon](https://www.archlinux.org/packages/?name=notification-daemon).

Si no está usando [GNOME](/index.php/GNOME "GNOME"), instale [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd), en lugar de notification-daemon, ya que demanda muchos paquetes GNOME innecesarios.

### Alternativa

Los script de compilación de [wicd-bzr](https://aur.archlinux.org/packages/wicd-bzr/) están disponibles en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)"), en los que se basa la última rama de desarrollo. Si necesita una versión alternativa o simplemente quiere crear su propio paquete, puede construirlo fácilmente usando [ABS](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)").

## Para empezar

### Configuración inicial

Wicd provee un demonio que debe ser iniciado.

**Advertencia:** La ejecución de varios gestores de red *a voluntad* simultáneamente causarán problemas, por lo que es importante *desactivar los demás demonios de gestión de red*.

En primer lugar, detenga todos los demonios de red que estén en ejecución (como netctl, dhcpcd, NetworkManager).

Desactive los servicios de gestión red existentes, `netctl`, `dhcpcd`, y `networkmanager`. Remítase a [Systemd (Español)#Usar las unidades](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)").

**Nota:** Puede que tenga que detener y desactivar el demonio **network**, en lugar de **netctl**, que es el servicio que actualmente reemplaza a **network**. Si no está seguro, pruebe a desactivar ambos.

Inicie el [demonio](/index.php/Daemon_(Espa%C3%B1ol) "Daemon (Español)") **wicd** de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)") y active el servicio para que arranque al inicio del sistema.

Agregue su cuenta al grupo **users**:

```
# gpasswd -a NOMBREDEUSUARIO users

```

**Nota:** El grupo Unix que permite a dbus acceder a **wicd**, está sujeto a cambios, y puede ser diferente de *network*. Compruebe qué grupo viene indicado en la policy presente en `/etc/dbus-1/system.d/wicd.conf`, y añada su propio usuario a dicho grupo.

Si ha agregado el usuario a un grupo nuevo, reinicie sesión de usuario.

### Ejecutar Wicd en un entorno de escritorio

Si ha instalado el paquete [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk) y entrado en el entorno de escritorio, abra un terminal virtual para ejecutar una de las siguientes órdenes:

*   Para iniciar Wicd como un servicio del sistema, ejecute:

```
$ systemctl start wicd.service

```

*   Para cargar Wicd, ejecute:

```
$ wicd-client

```

*   Para forzar que se inicie minimizado en el área de notificación, ejecute:

```
$ wicd-client --tray

```

*   Si su entorno de escritorio no tiene un área de notificación, o si no quiere que wicd se muestre como un icono en la bandeja del sistema, ejecute:

```
$ wicd-client -n

```

### Ejecutar Wicd en modo texto

Si no instaló [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk), entonces puede usar wicd-cli o wicd-curses:

```
$ wicd-curses

```

**Nota:** Wicd no le pide una clave de acceso para el prompt. Para utilizar conexiones cifradas (WPA/WEP), y ampliar la red a la que poder conectarse, haga clic en **Advanced** en las opciones de red y escriba la información necesaria.

### Inicio automático

El paquete [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk) pone un archivo en `/etc/xdg/autostart/wicd-tray.desktop`, para iniciar automáticamente `wicd-client` al iniciar sesión en el DE/WM. Si es así, es suficiente con activar el servicio del sistema wicd:

```
$ systemctl enable wicd.service

```

Si `/etc/xdg/autostart/wicd-tray.desktop` no existe, puede añadir **wicd-client** para que al arrancar el DE/WM la aplicación se inicie al conectarse a la sesión.

**Nota:** Si **wicd-client** es añadido al inicio de DE/WM cuando `/etc/xdg/autostart/wicd-tray.desktop` existe, tendrá un problema por que tendrá dos `wicd-client` corriendo simultáneamente.

### Scripts

Wicd tiene la capacidad de ejecutar scripts durante todas las etapas del proceso de conexión (post/pre conectar/desconectar). Basta con colocar un script dentro de la carpeta de la etapa pertinente en `/etc/wicd/scripts/` y hacerlo ejecutable.

Los scripts son capaces de recibir tres parámetros, a saber:

```
$1 - el tipo de conexión (inalámbrica/por cable).
$2 - el ESSID (nombre de red).
$3 - el BSSID (dirección MAC de la puerta de enlace).

```

#### Detener los ataques de ARP spoofing

El siguiente script se puede utilizar para establecer un ARP estático, para detener los ataques [ARP spoofing](https://en.wikipedia.org/wiki/es:ARP_Spoofing "wikipedia:es:ARP Spoofing"). Basta con cambiar los valores dentro de la declaración para que coincida con los de las redes a las que desea permitir entradas para ARP estáticas.

```
#!/bin/bash
#Set the parameters passed to this script to meaningful variable names.
connection_type="$1"
essid="$2"
bssid="$3"

if [ "${connection_type}" == "wireless" ]; then

       #Change below to match your networks.
       case "$essid" in
               YOUR-NETWORK-NAME-ESSID)
                       sudo arp -s 192.168.0.1 00:11:22:33:44:55
                       ;;
               Netgear01923)
                       sudo arp -s 192.168.0.1 10:11:20:33:40:50
                       ;;
               ANOTHER-ESSID)
                       sudo arp -s 192.168.0.1 11:33:55:77:99:00
                       ;;
               *)
                       echo "Static ARP not set. No network defined."
                       ;;
       esac
fi

```

#### Cambiar la dirección MAC con macchanger

Véase el [artículo relacionado](/index.php/MAC_address_spoofing#systemd_.2B_macchanger_.2B_dhcpcd_.28no_NetworkManager.29 "MAC address spoofing").

El siguiente script se puede utilizar para cambiar la dirección MAC de las interfaces de red.

Para cambiar la MAC cada vez que se conecta a una red, coloque el script en el directorio `/etc/wicd/scripts/preconnect/`

Eche un vistazo a `macchanger --help` para ajustar la orden macchanger a sus necesidades.

```
#!/usr/bin/env bash

connection_type="$1"

if [[ "${connection_type}" == "wireless" ]]; then
    ip link set wlan0 down
    macchanger -A wlan0
    ip link set wlan0 up
elif [[ "${connection_type}" == "wired" ]]; then
    ip link set eth0 down
    macchanger -A eth0
    ip link set eth0 up
fi

```

## Solución de problemas

Véase [Network configuration#Troubleshooting](/index.php/Network_configuration#Troubleshooting "Network configuration") para la solución de los problemas sobre las conexiones por cable y [Wireless network configuration#Troubleshooting](/index.php/Wireless_network_configuration#Troubleshooting "Wireless network configuration") para la solución de problemas de las conexiones inalámbricas. Esta sección solo se refiere a los problemas específicos de *wicd*.

### Fallo importando pynotify, notificaciones desactivadas

Para el caso de que el paquete [python2-notify](https://www.archlinux.org/packages/?name=python2-notify) no se instale automáticamente. Puede [instalarlo](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

### Mensaje de error de conexión con Dbus

Si wicd de repente deja de funcionar y emite mensajes haciendo responsable a dbus, es muy probable que tenga que quitar wicd completamente, incluso con todos sus archivos de configuración, y volver a instalarlo desde cero:

```
pacman -R wicd
rm -Rf /etc/wicd /var/log/wicd /etc/dbus-1/system.d/wicd*
pacman -S wicd

```

Compruebe este enlace para conocer más detalles: [https://bbs.archlinux.org/viewtopic.php?pid=577141#p577141](https://bbs.archlinux.org/viewtopic.php?pid=577141#p577141)

Puede encontrar que wicd-client devuelve mensajes de error de conexión relativos a dbus («Could not connect to wicd's D-Bus interface») cuando wicd no está funcionando a causa de un problema con un archivo de configuración. Aparentemente, en ocasiones una cuenta vacía se agrega a /etc/wicd/wired-settings.conf, en cuyo caso solo tiene que eliminar los corchetes:

```
[] 

```

y reiniciar wicd.

Si lo anterior no funciona, podría intentar [esto](https://bbs.archlinux.org/viewtopic.php?pid=1268721).

### Problemas después de actualizar el paquete

A veces wicd client no se carga después de una actualización del paquete debido a errores de dbus.

Una posible solución consiste en eliminar los archivos de configuración ubicados en el directorio `/etc/wicd/`.

```
# systemctl stop wicd
# rm /etc/wicd/*.conf
# systemctl start wicd

```

### Algunas notas sobre front-end gráficos para sudo

Si recibe un error acerca de que wicd falla al no encontrar un programa gráfico con sudo, instale uno como [gksu](https://aur.archlinux.org/packages/gksu/), [ktsuss](https://aur.archlinux.org/packages/ktsuss/), o [kdebase-runtime](https://aur.archlinux.org/packages/kdebase-runtime/), ejecutando la orden oportuna:

```
$ ktsuss wicd-client -n

```

```
$ gksudo wicd-client -n

```

```
$ kdesu wicd-client -n

```

### Configurar wicd para trabajar con eduroam

**Nota:** Se aconseje probar primero el paquete [wicd-eduroam](https://aur.archlinux.org/packages/wicd-eduroam/) de AUR. Aparecerá en wicd la opción para «eduroam». Si no funciona, intente lo que sigue.

Este perfil solo funcionará para las instituciones eduroam que utilizan el protocolo TTLS, pero no funcionará para el caso que venga usado el protocolo PEAP (puede encontrar un perfil PEAP aquí: [Eduroam wicd](http://csclub.uwaterloo.ca/~mtahmed/article/eduroam_wicd)).

Cree el archivo `/etc/wicd/encryption/templates/ttls-80211`, y guarde lo siguiente:

 `/etc/wicd/encryption/templates/ttls-80211` 
```
name = TTLS for Wireless
author = Alexander Clouter
version = 1
require anon_identity *Anonymous_Username identity *Identity password *Password 
optional ca_cert *Path_to_CA_Cert cert_subject *Certificate_Subject
-----
ctrl_interface=/var/run/wpa_supplicant
network={
       ssid="$_ESSID"
       scan_ssid=$_SCAN

       key_mgmt=WPA-EAP
       eap=TTLS

       ca_cert="$_CA_CERT"
       subject_match="$_CERT_SUBJECT"

       phase2="auth=MSCHAPv2 auth=PAP"

       anonymous_identity="$_ANON_IDENTITY"
       identity="$_IDENTITY"
       password="$_PASSWORD"
}

```

Abra un terminal:

```
# echo ttls-80211 >> /etc/wicd/encryption/templates/active

```

Abra wicd, elija TTLS para Wi-Fi en las propiedades de eduroam e introduzca los valores adecuados para su conexión. El formato del subject match debe mostrar algo así: «/CN=server.example.com».

NB. Este ajuste funciona en algunos caso comentando `subject_match`, aunque no es seguro, pero podría servir para conectase.

### Dos procesos wicd-client (y eventualmente dos iconos en la bandeja del sistema)

Consulte la nota en [#Ejecutar Wicd en modo texto](#Ejecutar_Wicd_en_modo_texto) sobre el archivo autostart en `/etc/xdg/autostart`, consulte el post del foro y envíe los errores a algunos de los [siguientes enlaces](#V.C3.A9ase_tambi.C3.A9n) proporcionados. Resumidamente, si `/etc/xdg/autostart/wicd-tray.desktop` existe, elimínelo. Solo es necesario el servicio `wicd` activado en el sistema.

### Contraseña incorrecta usando PEAP con TKIP/MSCHAPV2

La plantilla de conexión PEAP con TKIP/MSCHAPV2 requiere que el usuario introduzca la ruta a un certificado CA, además de introducir el nombre de usuario y contraseña. Sin embargo, esto puede causar problemas, dando como resultado que wicd notifique un mensaje de error de una contraseña incorrecta [*](https://bbs.archlinux.org/viewtopic.php?pid=990385). Una posible solución es el uso de PEAP con GTC en lugar de TKIP/MSCHAPV2 que no requiere para conectar la ruta al certificado CA.

### Wicd no puede obtener una dirección IP de WLAN

Esto podría ser causado al estar ejecutándose dhcpcd junto con wicd como servicio systemd. Una solución sería la de detener/desactivar **dhcpcd**.

## Véase también

*   [Nota sobre las interfaces en el sitio oficial](http://www.wicd.net/download.php)
*   [Discusión en el Foro](https://bbs.archlinux.org/viewtopic.php?id=114803) acerca de las dos instancias de wicd-client y `/etc/xdg/autostart`
*   [Informe de errores sobre el mencionado comportamiento de /etc/xdg/autostart y wicd-client](https://bugs.archlinux.org/task/22423)