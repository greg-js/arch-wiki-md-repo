Vncserver es un demonio de visualización remota que permite a usuarios situados a distancia realizar distintas funciones, incluyendo:

1.  Sesiones de X virtuales (sin cabeza) y totalmente en _paralelo_ que se ejecutan en segundo plano (es decir, no en el monitor físico, sino virtualmente) en una máquina. Todas las aplicaciones que se ejecutan en el servidor pueden seguir funcionando, incluso cuando el usuario se desconecta.
2.  Control directo de la sesión(s) local X (es decir, X se ejecuta en el monitor físico).

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Ejecutar vncserver para sesiones (sin cabeza) virtuales](#Ejecutar_vncserver_para_sesiones_.28sin_cabeza.29_virtuales)
    *   [2.1 Ajustes iniciales](#Ajustes_iniciales)
        *   [2.1.1 Crear archivos de entorno y contraseña](#Crear_archivos_de_entorno_y_contrase.C3.B1a)
        *   [2.1.2 Editar el archivo xstartup](#Editar_el_archivo_xstartup)
        *   [2.1.3 Permisos](#Permisos)
    *   [2.2 Iniciar el servidor](#Iniciar_el_servidor)
*   [3 Ejecutar vncserver para controlar directamente la pantalla local](#Ejecutar_vncserver_para_controlar_directamente_la_pantalla_local)
    *   [3.1 Usar x0vncserver de tigervnc](#Usar_x0vncserver_de_tigervnc)
    *   [3.2 Usar x11vnc](#Usar_x11vnc)
*   [4 Conectar a vncserver](#Conectar_a_vncserver)
    *   [4.1 Autenticación sin contraseña](#Autenticaci.C3.B3n_sin_contrase.C3.B1a)
    *   [4.2 Ejemplo de clientes basados en interfaz gráfica](#Ejemplo_de_clientes_basados_en_interfaz_gr.C3.A1fica)
*   [5 Asegurar vncserver por túneles SSH](#Asegurar_vncserver_por_t.C3.BAneles_SSH)
    *   [5.1 En el servidor](#En_el_servidor)
    *   [5.2 En el cliente](#En_el_cliente)
    *   [5.3 Conectar a un vncserver desde dispositivos Android a través de SSH](#Conectar_a_un_vncserver_desde_dispositivos_Android_a_trav.C3.A9s_de_SSH)
*   [6 Consejos y trucos](#Consejos_y_trucos)
    *   [6.1 Iniciar y detener vncserver en el arranque y apagado a través de systemd](#Iniciar_y_detener_vncserver_en_el_arranque_y_apagado_a_trav.C3.A9s_de_systemd)
    *   [6.2 Copiar contenidos del portapapeles desde la máquina remota a la local](#Copiar_contenidos_del_portapapeles_desde_la_m.C3.A1quina_remota_a_la_local)
    *   [6.3 Arreglo cuando no hay ningún cursor del ratón](#Arreglo_cuando_no_hay_ning.C3.BAn_cursor_del_rat.C3.B3n)
    *   [6.4 Conectar a un sistema OS X](#Conectar_a_un_sistema_OS_X)

## Instalación

Vncserver es proporcionado por [tigervnc](https://www.archlinux.org/packages/?name=tigervnc) y también por [tightvnc](https://aur.archlinux.org/packages/tightvnc/) desde [AUR](/index.php/AUR "AUR").

## Ejecutar vncserver para sesiones (sin cabeza) virtuales

### Ajustes iniciales

#### Crear archivos de entorno y contraseña

Vncserver creará el archivo del entorno inicial y el archivo de la contraseña del usuario la primera vez que se ejecute:

 `$ vncserver` 

```
You will require a password to access your desktops.

Password:
Verify:

New 'mars:1 (facade)' desktop is mars:1

Creating default startup script /home/facade/.vnc/xstartup
Starting applications specified in /home/facade/.vnc/xstartup
Log file is /home/facade/.vnc/mars:1.log

```

El puerto predeterminado en el que vncserver se ejecuta es: 1, que corresponde al puerto TCP en el que el servidor se está ejecutando (donde 5900 + n = número de puerto). En este caso, se está ejecutando en 5900 + 1 = 5901\. Ejecutar vncserver por segunda vez creará una segunda instancia que se ejecuta en el siguiente puerto más alto, libre, es decir: 2 o 5902.

**Nota:** Los sistemas Linux pueden tener tantos vncserver como memoria física lo permitan —todos ellos se ejecuta en paralelo entre sí—.

Apague vncserver usando el parámetro -kill:

```
$ vncserver -kill :1

```

#### Editar el archivo xstartup

El archivo fuente de Vncserver es `~/.vnc/xstartup` que funciona como un archivo [.xinitrc](/index.php/.xinitrc ".xinitrc"). Como mínimo, los usuarios deben definir un entorno de escritorio para empezar, si se desea un entorno gráfico. Por ejemplo, para iniciar xfce4:

```
#!/bin/sh
export XKL_XMODMAP_DISABLE=1
exec startxfce4

```

**Nota:** La línea `XKL_XMODMAP_DISABLE` es conocida por corregir los problemas asociados con las pulsaciones del teclado «scrambled» al escribir en las terminales bajo algún entorno de escritorio virtualizado.

#### Permisos

Es una buena práctica asegurar `~/.vnc` al igual que `~/.ssh`, aunque esto no es un requisito. Ejecute lo siguiente para hacerlo:

```
$ chmod 700 ~/.vnc

```

### Iniciar el servidor

Vncserver ofrece flexibilidad mediante la utilización de parámetros. El ejemplo siguiente inicia un vncserver con una resolución específica, lo que permite a múltiples usuarios ver/controlar de forma simultánea, y establece el dpi en el servidor virtual a 96:

```
$ vncserver -geometry 1440x900 -alwaysshared -dpi 96 :1

```

**Nota:** No se necesita usar una resolución de monitor estándar para vncserver; 1440x900 puede ser reemplazado con algo diferente como 1792x1008, 740x480, etc.

Para obtener una lista completa de opciones, pase el parámetro -help a vncserver.

```
$ vncserver -help

```

## Ejecutar vncserver para controlar directamente la pantalla local

### Usar x0vncserver de tigervnc

TigerVNC ofrece el binario x0vncserver que tiene una funcionalidad similar a x11vnc por ejemplo,

```
$ x0vncserver -display :0 -passwordfile ~/.vnc/passwd

```

Para más información, véase

```
man x0vncserver

```

### Usar x11vnc

Otra opción es utilizar el paquete [x11vnc](https://www.archlinux.org/packages/?name=x11vnc). Esto tiene la ventaja o desventaja, dependiendo de su perspectiva, de que requiere root para iniciar el acceso. Para más información, véase [X11vnc](/index.php/X11vnc "X11vnc").

## Conectar a vncserver

Cualquier número de cliente se puede conectar a un vncserver. Un ejemplo sencillo se muestra abajo donde vncserver está ejecutandose en 10.1.10.2 en el puerto 5901 (:1) en notación abreviada:

```
$ vncviewer 10.1.10.2:1

```

### Autenticación sin contraseña

El parámetro `-passwd` permite definir la ubicación del archivo `~/.vnc/passwd` en el servidor. Se espera que el usuario tenga acceso a este archivo en el servidor a través de [SSH](/index.php/Secure_Shell "Secure Shell"). En cualquier caso, coloque ese archivo en el sistema de archivos del cliente en un lugar seguro, es decir, que tenga acceso de lectura SOLO para el usuario cliente.

```
$ vncviewer -passwd /ruta/al/archivo-passwd-del-servidor

```

### Ejemplo de clientes basados en interfaz gráfica

*   [gtk-vnc](https://www.archlinux.org/packages/?name=gtk-vnc)
*   [kdenetwork-krdc](https://www.archlinux.org/packages/?name=kdenetwork-krdc)
*   [rdesktop](https://www.archlinux.org/packages/?name=rdesktop)
*   [vinagre](https://www.archlinux.org/packages/?name=vinagre)
*   [remmina](https://www.archlinux.org/packages/?name=remmina)
*   [vncviewer-jar](https://www.archlinux.org/packages/?name=vncviewer-jar)

## Asegurar vncserver por túneles SSH

### En el servidor

Si se que quiere acceso a vncserver desde fuera de la protección de una LAN, debe preocuparse por las contraseñas en texto plano y el tráfico sin cifrar desde/hacia el cliente y el servidor. Vncserver es fácilmente asegurable por túneles SSH. Además, no se necesita abrir otro puerto hacia el exterior usando este método, ya que el tráfico se canaliza literalmente a través del puerto SSH que el usuario ya tiene abierto en la WAN. Se recomienda utilizar el parámetro -localhost al ejecutar vncserver en este escenario. Este parámetro solo permite conexiones _desde el localhost_ —y, por analogía, solo los usuarios físicamente autenticados y asegurados en el entorno—.

```
$ vncserver -geometry 1440x900 -alwaysshared -dpi 96 -localhost :1

```

### En el cliente

Con el servidor funcionando, ahora solo basta aceptar la conexión del equipo local, y conectarse al entorno a través de ssh usando la opción -L para activar los túneles. Por ejemplo:

```
$ ssh IP_DE_LA_MÁQUINA_DE_DESTINO -L 8900:localhost:5901

```

Esto redirecciona el puerto 5901 del servidor al escenario del cliente en el pueto 8900\. Una vez conectado a través de SSH, deje abierto el termina xterm o la ventana de la shell; ello actuará como un túnel seguro a/desde el servidor. Para conectar a través de VNC, abra un segundo terminal xterm y no se conecte a la dirección IP remota, sino al localhost del cliente, utilizando así la canalización de seguridad:

```
$ vncviewer localhost::8900

```

Desde la página de manual de ssh: _-L [bind_address:] port:host:hostport_

_Esto especifica que el puerto dado en el equipo (cliente) local se rediccionará al equipo y al puerto dado en el lado remoto. Esto funciona mediante la asignación de un socket para escuchar al puerto en el lado local, opcionalmente unido al bind_address especificado. Cada vez que se realiza una conexión a este puerto, la conexión se envía a través del canal seguro, y se realiza una conexión al hostport de puerto del equipo desde la máquina remota. Las redirecciones de puertos también se pueden especificar en el archivo de configuración. Las direcciones IPv6 se pueden especificar con una sintaxis alternativa:_

_[bind_address/] port/host/ hostport o encerrando la dirección entre corchetes._ _Solo el superusuario puede redireccionar puertos privilegiados. Por defecto, el puerto local está condicionado a la configuración de los puertos de la puerta de enlace. Sin embargo, un bind_address explícito se puede utilizar para obligar a realizar la conexión a una dirección específica. El bind_address de ``localhost'' indica que el puerto de escucha está disponible para uso local solamente, mientras que una dirección vacía o `*' indica que el puerto debe estar disponible en todas las interfaces._

### Conectar a un vncserver desde dispositivos Android a través de SSH

Para conectarse a un vncserver sobre SSH usando un dispositivo Android:

```
1\. Ejecutar el servidor SSH en la máquina para conectarse.
2\. Ejecutar vncserver en la máquina para conectarse. (ejecutar el servidor con el parámetro -localhost como se mencionó arriba)
3\. Cliente SSH en el dispositivo Android (ConnectBot es una opción popular y será utilizada en esta guía como ejemplo).
4\. Cliente VNC en el dispositivo Android (androidVNC).
```

Considere la posibilidad de utilizar algún servicio de DNS dinámico para objetivos que no tienen direcciones IP estáticas.

En ConnectBot, escriba la IP y conéctese a la máquina deseada. Pulse la tecla Opciones, seleccione Redireccionar Puertos y añada un nuevo puerto:

```
Nickname: vnc
Type: Local
Source port: 5901
Destination: 127.0.0.1:5901
```

Guarde esto.

En androidVNC:

```
Nickname: apodo
Password: la contraseña utilizada para configurar vncserver
Address: 127.0.0.1 (estamos en local después de la conexión a través de SSH)
Port: 5901
```

Conectar.

## Consejos y trucos

### Iniciar y detener vncserver en el arranque y apagado a través de systemd

Cree `/etc/systemd/system/vncserver@:1.service` y modifíquelo definiendo el usuario para ejecutar el servidor. Utilice esto con systemd para gestionarlo.

 `/etc/systemd/system/vncserver@:1.service` 

```
# Archivo de unidad de servicio de vncserver
#
# 1\. Copiar este archivo a /etc/systemd/system/vncserver@:<display>.service
# 2\. Edite User=
#   ("User=foo")
# 3\. Edite y ajuste adecuadamente los parámetros de vncserver
#   ("/usr/bin/vncserver %i -arg1 -arg2 -argn")
# 4\. Ejecute `systemctl daemon-reload`
# 5\. Ejecute `systemctl enable vncserver@:<display>.service`
#
# NO EJECUTAR ESTE SERVICIO si su red de área local no es de confianza
#
# Lea la página wiki para más información sobre seguridad
# https://wiki.archlinux.org/index.php/Vncserver

[Unit]
Description=Servicio de escritorio remoto (VNC)
After=syslog.target network.target

[Service]
Type=simple
User=
PAMName=login

# Limpiar los archivos existentes en el entorno /tmp/.X11-unix
ExecStartPre=/bin/sh -c '/usr/bin/vncserver -kill %i > /dev/null 2>&1 || :'
ExecStart=/usr/bin/vncserver -geometry 1440x900 -fg -alwaysshared -dpi 100 %i
ExecStop=/usr/bin/vncserver -kill %i

[Install]
WantedBy=multi-user.target

```

Cambie las opciones en _ExecStart_, pero mantenga el parámetro -fg para permitir funcionalidades.

### Copiar contenidos del portapapeles desde la máquina remota a la local

Si la copia de la máquina remota a la máquina local no funciona, ejecute autocutsel en el servidor, como se menciona a continuación [[referencia](https://bbs.archlinux.org/viewtopic.php?id=101243)]:

```
$ autocutsel -fork

```

Ahora presione F8 para mostrar el menú emergente de VNC y seleccione la opción `Clipboard: local -> remote`.

Se puede poner la orden anterior en `~/.vnc/xstartup` para que se ejecute automáticamente al arrancar vncserver.

### Arreglo cuando no hay ningún cursor del ratón

Si no hay ningún cursor del ratón visible cuando se utiliza `x0vncserver`, inicie vncviewer de la siguiente manera:

```
$ vncviewer DotWhenNoCursor=1 <server>

```

O ponga `DotWhenNoCursor=1` en el archivo de configuración, que se encuentra en `~/.vnc/default.tigervnc` por defecto.

### Conectar a un sistema OS X

Véase [https://help.ubuntu.com/community/AppleRemoteDesktop](https://help.ubuntu.com/community/AppleRemoteDesktop). Probado con Remmina.