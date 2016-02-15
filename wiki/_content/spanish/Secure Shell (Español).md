**Estado de la traducción:** este artículo es una versión traducida de [Secure Shell](/index.php/Secure_Shell "Secure Shell"). Fecha de la última traducción/revisión: **2014-12-26**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Secure_Shell&diff=0&oldid=352767).

**S**ecure **Sh**ell o **SSH** es un protocolo de red que permite el intercambio de datos sobre un canal seguro entre dos computadoras. SSH usa técnicas de cifrado que hacen que la información que viaja por el medio de comunicación vaya de manera no legible y ninguna tercera persona pueda descubrir el usuario y contraseña de la conexión ni lo que se escribe durante toda la sesión. SSH usa criptografía de clave pública para autenticar el equipo remoto y permitir al mismo autenticar al usuario si es necesario.

SSH se suele utilizar para iniciar una sesión en una máquina remota, donde poder ejecutar órdenes, pero también permite la tunelización, el reenvío de puertos TCP de forma arbitraria y de conexiones X11; también se pueden realizar transferencias de archivos usando protocolos SFTP o SCP asociados.

Un servidor SSH, por defecto, escucha el puerto TCP 22\. Un programa cliente de SSH es utilizado, generalmente, para establecer conexiones a un demonio _sshd_ que acepta conexiones remotas. Ambos se encuentran comúnmente en los sistemas operativos más modernos, incluyendo Mac OS X, Linux, Solaris y OpenVMS. Existen versiones propietarias, freeware y open-source de varios niveles de complejidad y exhaustividad.

(Source: [Wikipedia:es:Secure Shell](https://en.wikipedia.org/wiki/es:Secure_Shell "wikipedia:es:Secure Shell"))

## Contents

*   [1 OpenSSH](#OpenSSH)
    *   [1.1 Instalando OpenSSH](#Instalando_OpenSSH)
    *   [1.2 Configurando SSH](#Configurando_SSH)
        *   [1.2.1 Cliente](#Cliente)
        *   [1.2.2 Demonio (daemon)](#Demonio_.28daemon.29)
        *   [1.2.3 VirtualBox](#VirtualBox)
    *   [1.3 Gestión del Demonio SSHD](#Gesti.C3.B3n_del_Demonio_SSHD)
    *   [1.4 Conectándose al servidor](#Conect.C3.A1ndose_al_servidor)
    *   [1.5 Protección de SSH](#Protecci.C3.B3n_de_SSH)
        *   [1.5.1 Protección contra ataques de fuerza bruta](#Protecci.C3.B3n_contra_ataques_de_fuerza_bruta)
        *   [1.5.2 Limitar el inicio de sesión como root](#Limitar_el_inicio_de_sesi.C3.B3n_como_root)
            *   [1.5.2.1 Denegar](#Denegar)
            *   [1.5.2.2 Restringir](#Restringir)
*   [2 Otros servidores y clientes SSH](#Otros_servidores_y_clientes_SSH)
    *   [2.1 Dropbear](#Dropbear)
    *   [2.2 SSH alternativa: Mobile Shell - responsive, survives disconnects](#SSH_alternativa:_Mobile_Shell_-_responsive.2C_survives_disconnects)
*   [3 Trucos y sugerencias](#Trucos_y_sugerencias)
    *   [3.1 Túneles SOCKS cifrados](#T.C3.BAneles_SOCKS_cifrados)
        *   [3.1.1 Paso 1: Iniciar la conexión](#Paso_1:_Iniciar_la_conexi.C3.B3n)
        *   [3.1.2 Paso 2: Configurar tu navegador (u otros programas)](#Paso_2:_Configurar_tu_navegador_.28u_otros_programas.29)
    *   [3.2 Redireccionar X11](#Redireccionar_X11)
        *   [3.2.1 Configuración](#Configuraci.C3.B3n)
        *   [3.2.2 Utilización](#Utilizaci.C3.B3n)
    *   [3.3 Redireccionar otros puertos](#Redireccionar_otros_puertos)
    *   [3.4 Multiplexación](#Multiplexaci.C3.B3n)
    *   [3.5 Acelerando SSH](#Acelerando_SSH)
    *   [3.6 Montando un Sistema de archivos Remoto con SSHFS](#Montando_un_Sistema_de_archivos_Remoto_con_SSHFS)
    *   [3.7 Mantener la sesión activa](#Mantener_la_sesi.C3.B3n_activa)
    *   [3.8 Guardar los datos de conexión en la configuración de SSH](#Guardar_los_datos_de_conexi.C3.B3n_en_la_configuraci.C3.B3n_de_SSH)
    *   [3.9 Autossh - reiniciar automáticamente las sesiones y túnes de SSH](#Autossh_-_reiniciar_autom.C3.A1ticamente_las_sesiones_y_t.C3.BAnes_de_SSH)
        *   [3.9.1 Ejecutar Autossh automáticamente en el arranque mediante systemd](#Ejecutar_Autossh_autom.C3.A1ticamente_en_el_arranque_mediante_systemd)
*   [4 Cambiar el número de puerto de SSH con la activación del socket (sshd.socket)](#Cambiar_el_n.C3.BAmero_de_puerto_de_SSH_con_la_activaci.C3.B3n_del_socket_.28sshd.socket.29)
*   [5 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [5.1 Lista de comprobación](#Lista_de_comprobaci.C3.B3n)
        *   [5.1.1 Limpiar claves desactualizadas (opcional)](#Limpiar_claves_desactualizadas_.28opcional.29)
        *   [5.1.2 Recomendaciones](#Recomendaciones)
    *   [5.2 La conexión SSH queda colgada después de apagar/reiniciar](#La_conexi.C3.B3n_SSH_queda_colgada_despu.C3.A9s_de_apagar.2Freiniciar)
    *   [5.3 Conexión denegada o problemas con timeout](#Conexi.C3.B3n_denegada_o_problemas_con_timeout)
        *   [5.3.1 ¿Está su router haciendo reenvío de puertos?](#.C2.BFEst.C3.A1_su_router_haciendo_reenv.C3.ADo_de_puertos.3F)
        *   [5.3.2 ¿Está SSH corriendo y escuchando?](#.C2.BFEst.C3.A1_SSH_corriendo_y_escuchando.3F)
        *   [5.3.3 ¿Existen reglas de firewall que bloqueen la conexión?](#.C2.BFExisten_reglas_de_firewall_que_bloqueen_la_conexi.C3.B3n.3F)
        *   [5.3.4 ¿Está el tráfico llegando a su ordenador?](#.C2.BFEst.C3.A1_el_tr.C3.A1fico_llegando_a_su_ordenador.3F)
        *   [5.3.5 ¿Su ISP o un tercero está bloqueando el puerto por defecto?](#.C2.BFSu_ISP_o_un_tercero_est.C3.A1_bloqueando_el_puerto_por_defecto.3F)
            *   [5.3.5.1 Diagnóstico con Wireshark](#Diagn.C3.B3stico_con_Wireshark)
            *   [5.3.5.2 Posible solución](#Posible_soluci.C3.B3n)
        *   [5.3.6 Leer del socket fallido: connection reset by peer](#Leer_del_socket_fallido:_connection_reset_by_peer)
    *   [5.4 «[your shell]: No such file or directory» / ssh_exchange_identification problem](#.C2.AB.5Byour_shell.5D:_No_such_file_or_directory.C2.BB_.2F_ssh_exchange_identification_problem)
    *   [5.5 Mensaje de error «Terminal unknown» o «Error opening terminal»](#Mensaje_de_error_.C2.ABTerminal_unknown.C2.BB_o_.C2.ABError_opening_terminal.C2.BB)
        *   [5.5.1 Solución estableciendo la variable $TERM](#Soluci.C3.B3n_estableciendo_la_variable_.24TERM)
        *   [5.5.2 Solución usando el archivo terminfo](#Soluci.C3.B3n_usando_el_archivo_terminfo)
*   [6 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## OpenSSH

OpenSSH (OpenBSD Secure Shell) es un conjunto de programas de computadora que proveen una sesión de comunicación encriptada en una red informática que utiliza el protocolo SSH. Fue creado como una alternativa de código abierto al software propietario ofrecido por SSH Communications Security. OpenSSH es desarrollado como parte del proyecto OpenBSD, que está a cargo de Theo de Raadt.

OpenSSH es confundido a veces con OpenSSL por la similitud de nombre, sin embargo, los proyectos tienen objetivos distintos y están desarrollados por equipos diferentes.

### Instalando OpenSSH

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [openssh](https://www.archlinux.org/packages/?name=openssh) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

### Configurando SSH

#### Cliente

El archivo de configuración del cliente SSH se puede encontrar y editar en `/etc/ssh/ssh_config` o `~/.ssh/config`.

Ya no es necesario establecer explícitamente el `Protocol 2`, comentado en el archivo de configuración por defecto. Eso significa que el `Protocol 1` no será utilizado a menos que esté explícitamente activado (fuente: [http://www.openssh.org/txt/release-5.4](http://www.openssh.org/txt/release-5.4)).

#### Demonio (daemon)

El archivo de configuración del demonio SSH se puede encontrar y editar en `/etc/ssh/ssh**d**_config`.

Para permitir el acceso sólo a algunos usuarios añadir esta línea:

```
AllowUsers    user1 user2

```

Para permitir el acceso sólo a algunos grupos:

```
AllowGroups group1 group2

```

Para deshabilitar el acceso a root por SSH, cambie la línea PermitRootLogin así:

```
PermitRootLogin no

```

Para agregar un agradable mensaje de bienvenida edite el archivo `/etc/issue` y cambie la línea Banner para que luzca así:

```
Banner /etc/issue

```

**Sugerencia:**

*   Es posible que desee cambiar el puerto por defecto de 22 a cualquier puerto superior (ver [seguridad por oscuridad](https://en.wikipedia.org/wiki/es:Seguridad_por_oscuridad "wikipedia:es:Seguridad por oscuridad")). A pesar de que el puerto ssh que está siendo ejecutado puede ser detectado utilizando un port-scanner o escáner de puertos como [nmap](https://www.archlinux.org/packages/?name=nmap), cambiarlo reducirá el número de entradas en el log causados por intentos de autentificación automáticos. Para ayudar a seleccionar un puerto, revise la [lista de números de puerto TCP y UDP](https://en.wikipedia.org/wiki/es:Anexo:N%C3%BAmeros_de_puerto "wikipedia:es:Anexo:Números de puerto"). También puede encontrar información de los puertos a nivel local en `/etc/services`. Seleccione un puerto alternativo que **no** esté ya asignado a un servicio común para evitar conflictos.
*   Desactivar completamente los inicios de sesión con la contraseña aumentará en gran medida el nivel seguridad, consulte [Secure Shell#Force public key authentication](/index.php/Secure_Shell#Force_public_key_authentication "Secure Shell") para más información.

#### VirtualBox

Para comunicarse entre huésped y anfitrión de VirtualBox, el puerto del servidor debe ser reenviado en Settings > Network. Al conectarse desde el cliente/anfitrión, conecte a la dirección IP de la máquina del cliente/anfitrión, en oposición a la conexión de la otra máquina. Esto es porque la conexión se realizará a través de un adaptador virtual.

### Gestión del Demonio SSHD

El demonio SSH viene con diferentes archivos de unidades systemd.

Puede iniciar el demonio de forma inmediata y/o activarlo para que se inicie la próxima vez que arranque el equipo, como se describe en [Systemd (Español)#Usar las unidades](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)"):

```
# systemctl start sshd.service
# systemctl enable sshd.service

```

**Advertencia:** Systemd inicia los procesos de manera asíncrona. Si se amarra el demonio SSH a una dirección IP específica `ListenAddress 192.168.1.100` puede ser que no cargue al arranque porque por defecto el archivo sshd.service no depende de que se hayan habilitado las interfaces de red. Cuando se amarre a una dirección IP, es necesario agregar `After=network.target` a un archivo personalizado de sshd.service. Ver [Systemd (Español)#Modificar los archivos de unidad suministrados](/index.php/Systemd_(Espa%C3%B1ol)#Modificar_los_archivos_de_unidad_suministrados "Systemd (Español)").

Opcionalmente, al servicio utilizado anteriormente da soporte para activar el socket mediante el demonio SSH, de forma que el demonio se active de forma automática al recibir la primera conexión:

```
# systemctl start sshd.socket
# systemctl enable sshd.socket

```

Si usa un puerto diferente al 22, debe definir «ListenStream» en el archivo correspondiente. Copie `/lib/systemd/system/sshd.socket` a `/etc/systemd/system/sshd.socket` para evitar que su archivo de systemd se sobresciba al actualizar el sistema. En `/etc/systemd/system/sshd.socket` cambie el puerto apropiado en «ListenStream» .

**Advertencia:** Al usar sshd.socket se inhabilita la opción `ListenAddress`, así que al usar el sshd.socket incluido permitirá conexiones desde cualquier dirección. Para lograr el efecto de definir `ListenAddress`, debe crear un archivo personalizado y modificar ListenStream (ej. `ListenStream=192.168.1.100:22` es equivalente a `ListenAddress 192.168.1.100`). Además debes agregar `FreeBind=true` bajo `[Socket]` o de lo contrario definir una dirección IP tendra el mismo efecto de definir `ListenAddress`: el socket no iniciara si la red no está lista.

**Sugerencia:** Cuando se utiliza la activación del socket, ni `sshd.socket` ni `sshd.service` permiten supervisar los intentos de conexión en el registro, pero si lo puede ver al ejecutar `# journalctl /usr/bin/sshd`.

### Conectándose al servidor

Para conectarse a un servidor, ejecuta:

```
$ ssh -p port user@server-address

```

### Protección de SSH

Permitir el acceso remoto al sistema a través de SSH es bueno para fines administrativos, pero puede representar una amenaza para la seguridad de su servidor. A menudo es el blanco de ataques de fuerza bruta, por lo que el acceso SSH necesita ser limitado adecuadamente para evitar que terceros accedan a su servidor.

*   Utilice nombres de cuenta y contraseñas no estándar .
*   Permita solo conexiones SSH entrantes desde ubicaciones de confianza.
*   Utilice [fail2ban](/index.php/Fail2ban "Fail2ban") o [sshguard](/index.php/Sshguard "Sshguard") para controlar los ataques de fuerza bruta, y banear las IP que se correspondan con las de los ataques de fuerza bruta.

#### Protección contra ataques de fuerza bruta

El concepto de [ataques de fuerza bruta](https://en.wikipedia.org/wiki/es:Ataque_de_fuerza_bruta "wikipedia:es:Ataque de fuerza bruta") es simple: es un mecanismo por el que alguien trata continuamente de iniciar sesión en una página web o un servidor para acceder a un prompt como SSH utilizando un elevado número de combinaciones de nombre de usuario y contraseña aleatorios. Se puede proteger de los ataques de fuerza bruta mediante un script automatizado que bloquea a cualquiera que esté tratando de usar la fuerza bruta en su camino, por ejemplo [fail2ban](/index.php/Fail2ban "Fail2ban") o [sshguard](/index.php/Sshguard "Sshguard").

Por otro lado, los ataques de fuerza bruta se pueden hacer inviable exigiendo la autenticación de la clave pública, añadiendo el siguiente ajuste a `sshd_config`:

```
PasswordAuthentication no

```

Antes de efectuar este ajuste, asegúrese de que todas las cuentas que requieren acceso SSH, tienen configurada la autenticación de la clave pública en los correspondientes archivos `authorized_keys`.

#### Limitar el inicio de sesión como root

En general, se considera una mala práctica permitir que el usuario root inicie sesión sin restricciones a través de SSH. Hay dos métodos por los cuales el acceso de root a SSH puede ser restringido para mayor seguridad.

##### Denegar

Sudo proporciona los derechos de root de forma selectiva para las acciones que requieran de estos derechos, sin necesidad de autenticarse con la cuenta de root. Esto permite el bloqueo de la cuenta root para acceder a través de SSH y funciona como una medida de seguridad frente a los potenciales ataques de fuerza bruta, ya que ahora un atacante debe adivinar, además del nombre de la cuenta, la contraseña.

SSH se puede configurar para negar las conexiones remotas con el usuario root, editando la sección «Authentication» en `/etc/ssh/sshd_config`. Basta con cambiar `#PermitRootLogin yes` a `no` y descomentar la línea:

 `/etc/ssh/sshd_config` 

```
PermitRootLogin no
...

```

A continuación, reiniciar el demonio de SSH:

```
 # systemctl restart sshd

```

Ahora va a ser incapaz de conectarse por SSH como root, pero todavía será capaz de iniciar sesión con su usuario normal y utilizar [su (Español)](/index.php/Su_(Espa%C3%B1ol) "Su (Español)") o [sudo (Español)](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)") para hacer la administración del sistema.

##### Restringir

Algunas tareas automatizadas realizadas a distancia, como copia de seguridad de todo el sistema, requieren el acceso de root completo. Para permitir que esto se haga de una manera segura, en lugar de desactivar el inicio de sessión de root a través de SSH, es posible permitir las conexiones de root solo para ciertas órdenes seleccionadas. Esto se puede lograr editando `~root/.ssh/authorized_keys`, y anteponiendo la clave deseada, por ejemplo, como sigue:

```
command="/usr/lib/rsync/rrsync -ro /" ssh-rsa …

```

Esto permitirá cualquier inicio de sesión con esta clave específica, solo para ejecutar la orden especificada entre las comillas.

El aumento de la superficie de ataque creado por exponer el nombre de usuario root al iniciar la sesión, se puede compensar añadiendo lo siguiente a `sshd_config`:

```
PermitRootLogin forced-commands-only

```

Este ajuste no solo restringirá las órdenes que puede ejecutar root a través de SSH, sino que también desactiva el uso de contraseñas, forzando el uso de la autenticación de la clave pública para la cuenta root.

Hay una alternativa un poco menos restrictiva, que permitirá ejecutar cualquier orden por root, pero hace los ataques de fuerza bruta no factibles mediante la exigencia de la autenticación de la clave pública. Para esta opción, establezca:

```
PermitRootLogin without-password

```

## Otros servidores y clientes SSH

Aparte de OpenSSH, hay otros muchos [clientes](https://en.wikipedia.org/wiki/Comparison_of_SSH_clients "wikipedia:Comparison of SSH clients") y [servidores](https://en.wikipedia.org/wiki/Comparison_of_SSH_servers "wikipedia:Comparison of SSH servers") SSH disponibles.

### Dropbear

[Dropbear](https://en.wikipedia.org/wiki/Dropbear_(software) "wikipedia:Dropbear (software)") es un cliente SSH-2 y un servidor. El paquete [dropbear](https://www.archlinux.org/packages/?name=dropbear) está disponible en [AUR](/index.php/Arch_User_Repository_(Espa%C3%B1ol) "Arch User Repository (Español)").

El cliente ssh en línea de órdenes se llama dbclient.

### SSH alternativa: Mobile Shell - responsive, survives disconnects

Del [sitio web](http://mosh.mit.edu/) de Mosh:

Aplicación de terminal remoto que permite la itinerancia, soporta conectividad intermitente y proporciona echo local inteligente y la edición de línea de keystrokes del usuario. Mosh es un reemplazo para SSH. Es más robusto y sensible, sobre todo a través de Wi-Fi, móvil y enlaces de larga distancia.

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") [mosh](https://www.archlinux.org/packages/?name=mosh) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)") o la última revisión [mosh-git](https://aur.archlinux.org/packages/mosh-git/) desde [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)").

## Trucos y sugerencias

### Túneles SOCKS cifrados

Este tipo de conexión es muy útil para usuarios de equipos portátiles conectados a varias conexiones inalámbricas no seguras. Lo único que necesitas es un servidor SSH corriendo en algún lugar seguro, como tu casa o tu trabajo. Puede ser útil usar un servicio de DNS dinámico como [DynDNS](http://www.dyndns.org/) para no tener que recordar la dirección IP a la que desea conectarse.

#### Paso 1: Iniciar la conexión

Lo único que tienes que hacer es ejecutar este comando en tu terminal favorita para iniciar la conexión:

```
$ ssh -ND 4711 _user_@_host_

```

donde `_user_` es tu nombre de usuario en el servidor SSH que se está ejecutando en el `_host_`. Preguntará por tu contraseña, y luego ¡estarás conectado! El parámetro `N` desactiva el prompt interactivo, y el `D` especifica el puerto local en el cual escuchar (puedes elegir el numero de puerto que quieras). El parámetro `T` desactiva la asignación pseudo-tty.

Le puede interesar añadir el parámetro _verbose_ (`-v`), ya que la salida le permite comprobar que está realmente conectado.

#### Paso 2: Configurar tu navegador (u otros programas)

El paso anterior es inútil si no configura el navegador web (u otros programas) para su uso con el túnel que acaba de crear. Debido a que la versión actual de SSH soporta SOCKS4 y SOCKS5, se puede usar cualquiera de ellos.

*   Para Firefox: _Editar → Preferencias → Avanzadas → Red → Conexión → Configuración_:

	Marca la casilla _"Configuración manual de proxy"_ , y escribe `localhost` en el campo _"servidor SOCKS"_ , y luego escribe tu número de puerto en el siguiente campo de texto (`4711` en el siguiente ejemplo).

Firefox no hace automáticamente las peticiones DNS a través del túnel socks. Este potencial problema de privacidad puede ser mitigado por los siguientes pasos:

1.  Escriba «about:config» en la barra de navegación de Firefox.
2.  Busque por «network.proxy.socks_remote_dns»
3.  Ajuste el valor a «true».
4.  Reinicie el navegador.

*   Para Chromium: Se pueden setear las configuraciones de SOCKS como variables de entorno o como opciones en línea de comandos. Es recomendable agregar una de las siguientes funciones a `.bashrc`:

```
function secure_chromium() {
    port=4711
    export SOCKS_SERVER=localhost:$port
    export SOCKS_VERSION=5
    chromium &
    exit
}

```

o

```
function secure_chromium {
    port=4343
    chromium --proxy-server="socks://localhost:$port" &
    exit
}

```

Ahora solo queda abrir una terminal y escribir:

```
$ secure_chromium

```

Listo. ¡Disfruta tu túnel seguro!

### Redireccionar X11

_X11 forwarding_ es un mecanismo que permite a las interfaces gráficas de los programas de X11, que se ejecutan en un sistema remoto, mostrarse en una máquina cliente local. Para reenviar X11 al equipo remoto, este no necesita tener un sistema completo X11 instalado, sin embargo, necesita, al menos, tener _xauth_ instalado. _xauth_ es una utilidad que mantiene las configuraciones de `Xauthority` utilizadas por el servidor y el cliente para la autenticación de la sesión de X11 ([fuente](http://xmodulo.com/2012/11/how-to-enable-x11-forwarding-using-ssh.html)).

**Advertencia:** Redirigir X11 tiene importantes implicaciones de seguridad que aconsejan la lectura de, al menos, las secciones pertinentes de `ssh`, `sshd_config` y `ssh_config` de las páginas del manual. Vea también [esta breve nota](https://security.stackexchange.com/questions/14815/security-concerns-with-x11-forwarding).

#### Configuración

En el sistema remoto:

*   [instale](/index.php/Pacman_(Espa%C3%B1ol)#Instalar_paquetes_espec.C3.ADficos "Pacman (Español)") [xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth) y [xorg-xhost](https://www.archlinux.org/packages/?name=xorg-xhost) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)")
*   en `/etc/ssh/ssh**d**_config`:
    *   verifique que las opciones `AllowTcpForwarding` y `X11UseLocalhost` están ajustadas a _yes_, y que `X11DisplayOffset` está ajustado a _10_ (esos son los valores por defecto si no se han cambiado, ver `man sshd_config`)
    *   ajuste `X11Forwarding` a _yes_
*   a continuación, [reinicie](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") el [demonio _sshd_](#Gesti.C3.B3n_del_Demonio_SSHD).

En el sistema cliente, active la opción `ForwardX11`, bien especificando el parámetro `-X` en la línea de órdenes para las conexiones ocasionales, bien ajustando `ForwardX11` a _yes_ en el [archivo de configuración del cliente de openSSH](#Cliente).

**Sugerencia:** Puede activar la opción `ForwardX11Trusted` (`-Y` en la línea de órdenes) si la interfaz gráfica está llegando mal o recibe errores; esto evitará que las redirecciones de X11 vengan sujetas a los controles de la [extensión de SEGURIDAD de X11](http://www.x.org/wiki/Development/Documentation/Security/). Asegúrese de haber entendido [la advertencia](#Redireccionar_X11) del comienzo de esta sección, si lo hace.

#### Utilización

[Inicie sesión en el equipo remoto](#Conect.C3.A1ndose_al_servidor) como de costumbre, especificando el parámetro `-X` si _ForwardX11_ no se ha activado en el archivo de configuración del cliente:

```
$ ssh -X _user@host_

```

Si recibe errores tratando de ejecutar aplicaciones gráficas, pruebe _ForwardX11Trusted_ en su lugar:

```
$ ssh -Y _user@host_

```

Ahora puede iniciar cualquier programa X en el servidor remoto, la salida será enviada a su sesión local:

```
$ xclock

```

Si recibe errores como «Cannot open display», pruebe la siguiente orden como usuario no root:

```
$ xhost +

```

La orden anterior permitirá a cualquiera transmitir aplicaciones X11\. Para limitar el reenvío a un tipo de equipo particular:

```
$ xhost +hostname

```

donde hostname es el nombre del equipo en particular al que desea remitirse. Ver `man xhost` para más detalles.

Tenga cuidado con algunas aplicaciones, ya que hacen un chequeo para ejecutar una instancia en la máquina local. [Firefox](/index.php/Firefox "Firefox") es un ejemplo: o bien cierre la instancia de Firefox en ejecución o utilice el siguiente parámetro de inicio para poner en marcha una instancia remota en el equipo local:

```
$ firefox -no-remote

```

Si recibe «X11 forwarding request failed on channel 0» cuando se conecta (y el archivo `/var/log/errors.log` del servidor muestra «Failed to allocate internet-domain X11 display socket»), asegúrese de que el paquete [xorg-xauth](https://www.archlinux.org/packages/?name=xorg-xauth) está instalado. Si su instalación no funciona, pruebe cualquiera de los dos opciones siguientes:

*   active la opción `AddressFamily any` en `ssh**d**_config` en el _server_, o
*   ajuste la opción `AddressFamily` en `ssh**d**_config` en el _server_ a inet.

Si establece «inet» puede arreglar los problemas con los clientes de Ubuntu en IPv4.

Para ejecutar aplicaciones X como otro usuario en el servidor SSH, necesita la línea de autenticación `xauth add` tomada desde `xauth list` de la sesión SSH del usuario conectado.

### Redireccionar otros puertos

Además del soporte integrado de SSH para redirigir X11, dicho soporte se puede usar también para asegurar el canal de cualquier conexión TCP, mediante su redirección local o remota.

El reenvío local abre un puerto en la máquina local, a la que se redirigirán las conexiones para el equipo remoto y de ahí a un destino determinado. Muy a menudo, el destino de reenvío será el mismo que el del equipo remoto, proporcionando así un shell seguro y, por ejemplo, una conexión VNC segura, a la misma máquina. El reenvío local se lleva a cabo por medio del parámetro `-L` y la especificación de reenvío se acompaña en forma de `<tunnel port>:<destination address>:<destination port>`.

Así:

```
$ ssh -L 1000:mail.google.com:25 192.168.0.100

```

utilizará SSH para iniciar sesión y abrir un shell en 192.168.0.100, y también creará un túnel desde el puerto TCP 1000 de la máquina local a mail.google.com en el puerto 25\. Una vez establecidas, las conexiones a localhost:1000 conectarán al puerto SMTP de Gmail. Para Google, parecerá que dichas conexiones (aunque no necesariamente los datos transmitidos por la conexión) se originaron en 192.168.0.100, y tales datos estarán seguros entre el equipo local y 192.168.0.100, pero no una vez en 192.168.0.100, a menos que se tomen otras medidas.

Del mismo modo:

```
$ ssh -L 2000:192.168.0.100:6001 192.168.0.100

```

permitirá conexiones a localhost:2000 que se enviarán de forma transparente al equipo remoto en el puerto 6001\. El ejemplo anterior es útil para conexiones VNC mediante la utilidad de vncserver —parte del paquete tightvnc— que, aunque muy útil, es explícita acerca de su falta de seguridad.

El reenvío remoto permite al equipo remoto conectarse a un equipo de forma arbitraria a través del túnel SSH y la máquina local, proporcionando un cambio funcional de redirecciones locales, y es útil para situaciones en las que, por ejemplo, el equipo remoto ha limitado conectividad debido a los cortafuegos. Se activa con el parámetro `-R` y utiliza la especificación de reenvío en forma de `<tunnel port>:<destination address>:<destination port>`.

Así:

```
$ ssh -R 3000:irc.freenode.net:6667 192.168.0.200

```

abrirá una shell en 192.168.0.200, y las conexiones desde 192.168.0.200 a sí mismo en el puerto 3000 (hablando en terminología remota, localhost:3000) serán enviadas a través del túnel de la máquina local y luego a irc.freenode.net en el puerto 6667, por lo tanto, en este ejemplo, lo que permite es el uso de programas de IRC en el equipo remoto, incluso si el puerto 6667 esté bloqueado por él, como es lo normal.

Tanto el reenvío local como el remoto se pueden utilizar para ofrecer una «puerta de enlace» segura, lo que permite que otros equipos se aprovechen de un túnel SSH, sin ejecutar SSH o el demonio SSH, proporcionando una dirección de enlace para el inicio del túnel como parte de la especificación de reenvío, por ejemplo `<tunnel address>:<tunnel port>:<destination address>:<destination port>`. La especificación `<tunnel address>` puede ser cualquier dirección de la máquina en el inicio del túnel, `localhost`, (o en blanco) `*`, que, respectivamente, permiten conexiones a través de la dirección indicada, a través de la interfaz loopback, o a través de cualquier interfaz. De forma predeterminada, el reenvío se limita a las conexiones desde la máquina en el «principio» del túnel, es decir, la especificación `<tunnel address>` viene asignada a `localhost`. El reenvío local no requiere ninguna configuración adicional, sin embargo, el reenvío remoto está limitado por la configuración del demonio SSH del servidor remoto. Vea la opción `GatewayPorts` en `sshd_config(5)` para más información.

### Multiplexación

El demonio SSH normalmente escucha en el puerto 22\. Sin embargo, es una práctica común para muchos puntos de acceso público a Internet bloquear todo el tráfico que no pase por los puertos HTTP/S normales (80 y 443, respectivamente), por lo que, efectivamente, bloquean las conexiones SSH. La solución inmediata para esto es tener listado adicionalmente`sshd` en uno de los puertos de la lista blanca:

 `/etc/ssh/sshd_config` 

```
Port 22
Port 443

```

Sin embargo, es probable que el puerto 443 ya esté en uso por un servidor web que sirve contenidos HTTPS, en cuyo caso es posible utilizar un multiplexor, como [sslh](https://www.archlinux.org/packages/?name=sslh), que escucha en el puerto multiplexado y puede inteligentemente reenviar paquetes a muchos servicios.

### Acelerando SSH

Se puede hacer que todas las sesiones al mismo equipo utilicen una conexión única, lo que acelerará enormemente los inicios de sesión posteriores, añadiendo estas líneas bajo el equipo (host) adecuado en `/etc/ssh/ssh_config`:

```
Host examplehost.com
  ControlMaster auto
  ControlPersist yes
  ControlPath ~/.ssh/socket-%r@%h:%p

```

Vea la página del manual `ssh_config(5)` para obtener una descripción completa de estas opciones.

Otra opción para mejorar la velocidad es habilitar la compresión con el sufijo `-C`. Una solución permanente es agregar esta línea debajo del host correcto en `/etc/ssh/ssh_config`:

```
Compression yes

```

**Advertencia:** `man ssh` establece que «_La compresión es deseable en las líneas de módem y otras conexiones lentas, pero ralentizará las cosas en redes rápidas_». Este consejo podría ser contraproducente en función de su configuración de red.

El tiempo de inicio de sesión puede ser acortado usando el sufijo `-4`,que saltea la búsqueda IPv6\. Esto puede hacerse permanente añadiendo esta línea bajo el host correcto en `/etc/ssh/ssh_config`:

```
AddressFamily inet

```

Cambiar los algoritmos de cifrado usados por SSH para demandar menos cpu puede mejorar la velocidad. En este sentido, las mejores opciones son arcfour y blowfish-cbc.

**Advertencia:** Por favor, no haga esto a menos que sepa lo que está haciendo; arcfour tiene una serie de debilidades conocidas.

Para utilizar sistemas de cifrado alternativos, ejecute SSH con el parámetro `-c`:

```
$ ssh -c arcfour,blowfish-cbc user@server-address

```

Para usar el cifrado permanentemente, añada esta línea bajo el equipo adecuado en `/etc/ssh/ssh_config`:

```
Ciphers arcfour,blowfish-cbc

```

### Montando un Sistema de archivos Remoto con SSHFS

Por favor, consulte el artículo [Sshfs](/index.php/Sshfs_(Espa%C3%B1ol) "Sshfs (Español)") para utilizar sshfs a fin de montar un sistema remoto —accesible a través de SSH— en una carpeta local, de modo que sea capaz de hacer cualquier operación en los archivos montados con cualquier herramienta (copiar, renombrar, editar con vim, etc.). Utilizar sshfs en lugar de shfs es, en general, preferible, como una nueva versión de shfs, ya que esta última no ha sido liberada desde 2004.

### Mantener la sesión activa

Tu sesion ssh sera automáticamente desconectada si ésta se encuentra inactiva. Para mantener activa la conexión agrega esto a `~/.ssh/config` o a `/etc/ssh/ssh_config` en el cliente.

```
ServerAliveInterval 120

```

Esto enviará la señal «keep alive» al servidor cada 120 segundos.

Por el contrario, para mantener activas las conexiones entrantes, puede establecer:

```
ClientAliveInterval 120

```

(o algún otro número mayor que 0) en el archivo `/etc/ssh/sshd_config` del servidor.

### Guardar los datos de conexión en la configuración de SSH

Cada vez que desee conectarse a un servidor ssh, por lo general, tiene que escribir, al menos, su dirección y el nombre de usuario. Para ahorrarse tener que reescribirlo, puede guardar los datos de los servidores a los que se conecta regularmente, utilizando el archivo personal `~/.ssh/config` o el global del sistema `/etc/ssh/ssh_config`, como se muestra en el siguiente ejemplo:

 `~/.ssh/config` 

```
Host myserver
    HostName 123.123.123.123
    Port 12345
    User bob
Host other_server
    HostName test.something.org
    User alice
    CheckHostIP no
    Cipher blowfish

```

Ahora solo queda conectarse al servidor utilizando el nombre especificado:

```
$ ssh myserver

```

Para ver una lista completa de las opciones posibles, eche un vistazo a la página del manual de ssh_config en el sistema o a la [ssh_config documentación](http://www.openbsd.org/cgi-bin/man.cgi?query=ssh_config) en el sitio web oficial.

### Autossh - reiniciar automáticamente las sesiones y túnes de SSH

Cuando una sesión o túnel no pueden mantenerse activos, por ejemplo debido a las malas condiciones de la red que provoca desconexiones del cliente, puede utilizar [Autossh](http://www.harding.motd.ca/autossh/) para reiniciar automáticamente. Autossh se puede instalar desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Ejemplos de uso:

```
$ autossh -M 0 -o "ServerAliveInterval 45" -o "ServerAliveCountMax 2" username@example.com

```

Combinado con [sshfs](/index.php/Sshfs "Sshfs"):

```
$ sshfs -o reconnect,compression=yes,transform_symlinks,ServerAliveInterval=45,ServerAliveCountMax=2,ssh_command='autossh -M 0' username@example.com: /mnt/example 

```

Conexión a través de un conjunto SOCKS-proxy por [Proxy_settings](/index.php/Proxy_settings_(Espa%C3%B1ol) "Proxy settings (Español)"):

```
$ autossh -M 0 -o "ServerAliveInterval 45" -o "ServerAliveCountMax 2" -NCD 8080 username@example.com 

```

Con el opción `-f`, autossh puede hacer que se ejecute como un proceso en segundo plano. Ejecutarlo de esta manera, sin embargo, significa que la frase de contraseña no se podrá introducir de forma interactiva.

La sesión finalizará una vez que se escribe `exit` en la sesión, o el proceso autossh recibe una señal SIGTERM, SIGINT of SIGKILL.

#### Ejecutar Autossh automáticamente en el arranque mediante systemd

Si desea iniciar automáticamente autossh, ahora es fácil conseguirlo haciendo que systemd maneje esto. Por ejemplo, puede crear un archivo de unidad systemd como este:

```
[Unit]
Description=AutoSSH service for port 2222
After=network.target

[Service]
Environment="AUTOSSH_GATETIME=0"
ExecStart=/usr/bin/autossh -M 0 -NL 2222:localhost:2222 -o TCPKeepAlive=yes foo@bar.com

[Install]
WantedBy=multi-user.target

```

Aquí `AUTOSSH_GATETIME=0` es una variable de entorno que especifica cuánto tiempo ssh debe estar activo antes de que autossh considere la conexión exitosa, ponerlo a 0 hace que autossh ignore el primer fallo de ejecución de ssh. Esto puede ser útil cuando se ejecuta autossh en el arranque. Otras variables de entorno están disponibles en la página del manual. Por supuesto, se puede hacer esta unidad más compleja si es necesario (consulte la documentación de systemd para más detalles), y, obviamente, puede utilizar sus propias opciones para autossh, pero tenga en cuenta que el parámetro `-f` implica `AUTOSSH_GATETIME=0` quen no funciona con systemd.

Luego coloque esto en, por ejemplo, /etc/systemd/system/autossh.service. Posteriormente, puede activar sus túneles autossh con, por ejemplo:

```
$ systemctl start autossh

```

(o como llame al archivo de servicios)

Si esto funciona bien para su caso, puede hacer esto permanente ejecutando:

```
$ systemctl enable autossh

```

Eso hace que autossh se inicie automáticamente en el arranque.

También es fácil mantener varios procesos autossh, para mantener activos varios túneles. Solo tiene que crear varios archivos .service con diferentes nombres.

## Cambiar el número de puerto de SSH con la activación del socket (sshd.socket)

Cree el archivo `/etc/systemd/system/sshd.socket.d/port.conf` con:

```
[Socket]
# Desactivar puerto por defecto
ListenStream=
# Establecer nuevo puerto
ListenStream=12345

```

systemd escuchará automáticamente en el nuevo puerto después de su recarga:

```
systemctl daemon-reload

```

## Solución de problemas

### Lista de comprobación

Esta es una primera aproximación a la solución de problemas con una lista de comprobación. Se recomienda revisar estos puntos antes de mirar más lejos:

1\. La carpeta `~/.ssh` del cliente y del servidor y su contenido deben ser accesibles por sus usuarios:

```
  $ chmod 700 /home/USER/.ssh
  $ chmod 600 /home/USER/.ssh/*

```

2\. Compruebe que todos los archivos de la carpeta `~/.ssh` del cliente y del servidor son propiedad de sus usuario:

```
  $ chown -R USER: ~/.ssh

```

3\. Compruebe que, por ejemplo, la clave pública `id_rsa.pub` del cliente está en el archivo `authorized_keys` del servidor .

4\. Compruebe que no se limitó el acceso a SSH a través de `AllowUsers` en `/etc/ssh/sshd_config` (separadas por espacios).

#### Limpiar claves desactualizadas (opcional)

5\. Elimine claves antiguas/no válidas del archivo `/.ssh/authorized_keys` del servidor.

6\. Elimine claves antiguas/no válidas privadas y públicas dentro de la carpeta `~/.ssh` de los clientes.

#### Recomendaciones

7\. Mantenga el menor número de claves posibles del archivo `~/.ssh/authorized_keys` del cliente en el servidor.

### La conexión SSH queda colgada después de apagar/reiniciar

La conexión SSH se bloquea después de apagar o reiniciar si systemd detiene la conexión de red antes que sshd. Para solucionar este problema, comente y cambie la declaración `After`:

 `/usr/lib/systemd/system/systemd-user-sessions.service` 

```
#After=remote-fs.target
After=network.target
```

### Conexión denegada o problemas con timeout

#### ¿Está su router haciendo reenvío de puertos?

SALTAR ESTE PASO SI NO ESTÁ DETRÁS DE UNA NAT DE MÓDEM/ROUTER (por ejemplo, un VPS o en otro caso un equipo con direcciones públicas). La mayoría de los hogares y pequeñas empresas tendrán un módem/router con NAT.

Lo primero es asegurarse de que el router sabe que reenvía cualquier conexión ssh entrante a su máquina. Su IP externa es dada a usted por su proveedor de Internet, y se asocia con cualquier petición que sale de su router. Por lo tanto, el router tiene que saber que cualquier conexión ssh entrante a su IP externa necesita ser reenviada a su máquina donde se ejecuta sshd.

Encuentre su dirección de red interna.

```
ip a

```

Encuentre la interfaz de su dispositivo y busque el campo inet. Luego acceda a la interfaz web de configuración del router, utilizando la IP del router (encontrará esto en la web). Informe a su router para redirigirlo a su IP inet. Vaya a [[1]](http://portforward.com/) para más instrucciones sobre cómo hacerlo para su router en particular.

#### ¿Está SSH corriendo y escuchando?

```
$ ss -tnlp

```

Si la orden anterior no muestra que el puerto SSH está abierto, SSH no se está ejecutando. Compruebe `/var/log/messages` para conocer errores, etc.

#### ¿Existen reglas de firewall que bloqueen la conexión?

[Iptables](/index.php/Iptables_(Espa%C3%B1ol) "Iptables (Español)") puede bloquear conexiones en el puerto `22`. Compruebe esto con:

 `# iptables -nvL` 

y busque las posibles reglas que bloqueen paquetes en la cadena `INPUT`. Entonces, si es necesario, desbloquee el puerto con una orden como:

```
# iptables -I INPUT 1 -p tcp --dport 22 -j ACCEPT

```

Para obtener más ayuda sobre cómo para configurar cortafuegos, consulte [Firewalls (Español)](/index.php/Firewalls_(Espa%C3%B1ol) "Firewalls (Español)").

#### ¿Está el tráfico llegando a su ordenador?

Realice un vuelco de la información del tráfico sobre el equipo que está teniendo problemas con:

```
# tcpdump -lnn -i any port ssh and tcp-syn

```

Esto debería mostrar alguna información básica, y luego espere a que todo el tráfico que debería producirse se muestre. Pruebe su conexión ahora. Si no ve ninguna salida cuando se intenta conectar, entonces algo fuera de su ordenador está bloqueando el tráfico (por ejemplo, cortafuegos físicos, NAT del router, etc.).

#### ¿Su ISP o un tercero está bloqueando el puerto por defecto?

**Nota:** Pruebe este paso si **sabe** que no está ejecutando ningún cortafuegos y sabe que ha configurado el router para DMZ o ha redirigido el puerto a su equipo y aún no funciona. Aquí encontrará los pasos de diagnóstico y una posible solución.

En algunos casos, su proveedor de Internet podría bloquear el puerto predeterminado (puerto 22 SSH), así que lo que está intentando (apertura de puertos, endurecimiento del apilamiento, defensa contra ataques de saturación, etc.) es estéril. Para confirmar esto, cree un servidor en todas las interfaces (0.0.0.0) y conéctese de forma remota.

Si recibe un mensaje de error similar a este:

```
ssh: connect to host www.inet.hr port 22: Connection refused

```

Eso significa que el puerto **no** está bloqueado por el ISP, pero el servidor no ejecuta SSH en ese puerto (vea [seguridad por oscuridad](https://en.wikipedia.org/wiki/es:Seguridad_por_oscuridad "wikipedia:es:Seguridad por oscuridad")).

Sin embargo, si se recibe un mensaje de error similar a este:

```
ssh: connect to host 111.222.333.444 port 22: Operation timed out 

```

Eso significa que algo está rechazando el tráfico TCP en el puerto 22\. Básicamente ese puerto está siendo vigilado, ya sea por el cortafuegos o por la intervención de terceras partes (como un ISP que bloquea y/o rechaza el tráfico entrante en el puerto 22). Si se sabe que no está ejecutando ningún cortafuegos en su ordenador, y está seguro que ningún Gremlins están creciendo en su router y switches, entonces, el ISP está bloqueando el tráfico.

Para hacer doble verificación, puede ejecutar Wireshark en el servidor y escuchar el tráfico en el puerto 22\. Dado que Wireshark es una utilidad que esnifa paquetes de dos niveles, y TCP/UDP tiene 3 niveles y así sucesivamente (ver [pila de red de IP](https://en.wikipedia.org/wiki/es:Familia_de_protocolos_de_Internet "wikipedia:es:Familia de protocolos de Internet")), si no recibe nada mientras se conecta de forma remota, lo más probable es que un tercero esté bloqueando el tráfico en ese puerto para su servidor.

##### Diagnóstico con Wireshark

[Instale](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") Wireshark con el paquete [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) disponible en los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

Y luego ejecútelo utilizando,

```
tshark -f "tcp port 22" -i NET_IF

```

donde NET_IF es la interfaz de red para una conexión WAN (ver `ip a` para comprobar). Si no se está recibiendo ningún paquete al intentar conectarse de forma remota, puede estar muy seguro de que su ISP está bloqueando el tráfico entrante en el puerto 22.

##### Posible solución

La solución es utilizar algún otro puerto que el ISP no esté bloqueando. Abra el archivo `/etc/ssh/sshd_config` y configúrelo para utilizar diferentes puertos. Por ejemplo, añada:

```
Port 22
Port 1234

```

Asegúrese también de que otras líneas de configuración del «puerto» en el archivo están comentadas. Solo comentar «Port 22» y poner «Port 1234» no va a resolver el problema, porque entonces sshd solo escuchará el puerto 1234\. Utilice ambas líneas para ejecutar el servidor SSH en ambos puertos.

Reinicie el servidor `systemctl restart sshd.service` y todo estará listo. Todavía tiene que configurar su cliente(s) para poder usar el otro puerto, en lugar del puerto predeterminado. Existen numerosas soluciones a ese problema, pero nosotros cubrimos dos de ellas aquí.

#### Leer del socket fallido: connection reset by peer

Las versiones recientes de openssh a veces fallan con el mensaje de error anterior, debido a un error que implica la criptografía de curva elíptica. En este caso, añada la siguiente línea a `~/.ssh/config`:

```
HostKeyAlgorithms ssh-rsa-cert-v01@openssh.com,ssh-dss-cert-v01@openssh.com,ssh-rsa-cert-v00@openssh.com,ssh-dss-cert-v00@openssh.com,ecdsa-sha2-nistp256,ecdsa-sha2-nistp384,ecdsa-sha2-nistp521,ssh-rsa,ssh-dss

```

Con openssh 5.9, la solución anterior no funciona. En su lugar, ponga las siguientes líneas en `~/.ssh/config`:

```
Ciphers aes128-ctr,aes192-ctr,aes256-ctr,aes128-cbc,3des-cbc 
MACs hmac-md5,hmac-sha1,hmac-ripemd160

```

Ver también [discussion](http://www.gossamer-threads.com/lists/openssh/dev/51339) en el foro openssh bug.

### «[your shell]: No such file or directory» / ssh_exchange_identification problem

Una posible causa de esto es la necesidad de ciertos clientes SSH de encontrar una ruta absoluta (una devuelta por `whereis -b [your shell]`, por instancia) en `$SHELL`, incluso si el binario de la shell se encuentra en una de las entradas `$PATH`.

### Mensaje de error «Terminal unknown» o «Error opening terminal»

Con ssh es posible recibir errores como «Terminal unknown» después de iniciar sesión. Iniciar aplicaciones ncurses como nano fallan con el mensaje «Error opening terminal». Hay dos métodos para solucionar este problema, uno rápido, mediante la variable $TERM, y otro más detallado usando el archivo terminfo.

#### Solución estableciendo la variable $TERM

Después de conectar con el servidor remoto establezca la variable $TERM para «xterm» con la siguiente orden:

`TERM=xterm`

Este método es una solución provisional y debe ser utilizado en servidores ssh al que se conecta raramente, ya que puede tener efectos secundarios no deseados. También tiene que repetir la orden después de cada conexión, o bien configurando ~.bashrc .

#### Solución usando el archivo terminfo

Una solución con más dedicación consiste en transferir el archivo terminfo del terminal en el equipo cliente al servidor ssh. En este ejemplo explicamos cómo configurar el archivo terminfo para el terminal «rxvt-unicode-256color». Cree el directorio que contendrá los archivos terminfo en el servidor ssh, mientras se está conectado al servidor, con la orden:

`mkdir -p ~/.terminfo/r/`

Ahora copie el archivo terminfo de su terminal en el nuevo directorio. Reemplace `rxvt-unicode-256color` con el terminal de su cliente en la siguiente orden y `ssh-server` con el usuario y dirección del servidor correspondiente.

`$ scp /usr/share/terminfo/r/_rxvt-unicode-256color_ ssh-server:~/.terminfo/r/`

Después de salir y entrar en el servidor ssh el problema debe haber sido corregido.

## Véase también

*   [A Cure for the Common SSH Login Attack](http://www.soloport.com/iptables.html)
*   [Defending against brute force ssh attacks](http://www.la-samhna.de/library/brutessh.html)
*   [OpenSSH key management, Part 1](http://www.ibm.com/developerworks/library/l-keyc/index.html) and [Part 2](http://www.ibm.com/developerworks/library/l-keyc2) on IBM developerWorks