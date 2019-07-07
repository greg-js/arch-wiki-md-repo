Artículos relacionados

*   [Samba](/index.php/Samba_(Espa%C3%B1ol) "Samba (Español)")
*   [Samba/Controlador del dominio de Active Directory](/index.php/Samba/Active_Directory_domain_controller "Samba/Active Directory domain controller")
*   [SOGo](/index.php/SOGo "SOGo")

De [Wikipedia](https://en.wikipedia.org/wiki/es:Active_Directory "wikipedia:es:Active Directory"):

	Active Directory (AD) o Directorio Activo son los términos que utiliza Microsoft para referirse a su implementación de [servicio de directorio](https://en.wikipedia.org/wiki/es:Servicio_de_directorio "wikipedia:es:Servicio de directorio") en una red distribuida de computadores.

Este artículo describe cómo integrar el sistema Arch Linux con un dominio de red Window utilizando [Samba](/index.php/Samba_(Espa%C3%B1ol) "Samba (Español)").

Antes de continuar tiene que existir un dominio de Active Directory y tener un usuario con los permisos apropiados en el dominio para: listar usuarios y añadir cuentas en el ordenador (Unirse al dominio).

Este documento no tiene la intención de hacer una guía completa de Active Directory o Samba. Consulte en la sección de recursos para información adicional.

El servidor Active Directory es una localización central para la administración de la red y seguridad. Es el responsable de autentificar y autorizar todos los usuarios y ordenadores a través de la red de dominio de Window asignando y forzando políticas de seguridad para todos los ordenadores en una red e instalar o actualizar software en la red de ordenadores. Por ejemplo, cuando un usuario inicia sesión en un ordenador que es parte de un dominio Window su Active Directory es el que verifica la contraseña y especifíca si es un administrador del sistema o un usuario normal. Los ordenadores servidores en los cuales se está ejecutando el Active Directory son llamados controladores de dominio.

Active Directory utiliza las versiones dos y tres del [protocolo ligero de acceso a directorios (LDAP)](https://en.wikipedia.org/wiki/es:Protocolo_Ligero_de_Acceso_a_Directorios "wikipedia:es:Protocolo Ligero de Acceso a Directorios"), una versión de Microsoft de [Kerberos](/index.php/Kerberos "Kerberos") y DNS.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Terminología](#Terminología)
*   [2 Configuración de Active Directory](#Configuración_de_Active_Directory)
    *   [2.1 Consideraciones GPO](#Consideraciones_GPO)
*   [3 Configuración del anfitrión Linux](#Configuración_del_anfitrión_Linux)
    *   [3.1 Instalación](#Instalación)
    *   [3.2 Actualizar DNS](#Actualizar_DNS)
    *   [3.3 Configurar NTP](#Configurar_NTP)
    *   [3.4 Kerberos](#Kerberos)
        *   [3.4.1 Crear un ticket de Kerberos](#Crear_un_ticket_de_Kerberos)
        *   [3.4.2 Validar el ticket](#Validar_el_ticket)
    *   [3.5 pam_winbind.conf](#pam_winbind.conf)
    *   [3.6 Samba](#Samba)
    *   [3.7 Unirse al dominio](#Unirse_al_dominio)
*   [4 Iniciar y comprobar servicios](#Iniciar_y_comprobar_servicios)
    *   [4.1 Iniciar Samba](#Iniciar_Samba)
    *   [4.2 Comprobar Winbind](#Comprobar_Winbind)
    *   [4.3 Comprobar nsswitch](#Comprobar_nsswitch)
    *   [4.4 Comprobar comandos de Samba](#Comprobar_comandos_de_Samba)
*   [5 Configurar PAM](#Configurar_PAM)
    *   [5.1 system-auth](#system-auth)
        *   [5.1.1 Sección "auth"](#Sección_"auth")
        *   [5.1.2 Sección "account"](#Sección_"account")
        *   [5.1.3 Sección "password"](#Sección_"password")
        *   [5.1.4 Sección "session"](#Sección_"session")
    *   [5.2 passwd](#passwd)
        *   [5.2.1 Sección "password"](#Sección_"password"_2)
    *   [5.3 Comprobar inicio de sesión](#Comprobar_inicio_de_sesión)
*   [6 Configurar recursos compartidos](#Configurar_recursos_compartidos)
*   [7 Añadir un ordenador al archivo keytab y activar ssh kerberizado sin contraseña al ordenador](#Añadir_un_ordenador_al_archivo_keytab_y_activar_ssh_kerberizado_sin_contraseña_al_ordenador)
    *   [7.1 Crear un archivo keytab del ordenador](#Crear_un_archivo_keytab_del_ordenador)
    *   [7.2 Activar la autentificación keytab](#Activar_la_autentificación_keytab)
    *   [7.3 Preparar sshd en el servidor](#Preparar_sshd_en_el_servidor)
    *   [7.4 Añadir las opciones necesarias en el cliente](#Añadir_las_opciones_necesarias_en_el_cliente)
    *   [7.5 Comprobar la ejecución](#Comprobar_la_ejecución)
    *   [7.6 Ajuste preciso para un manejo completo de kerberos sin contraseña.](#Ajuste_preciso_para_un_manejo_completo_de_kerberos_sin_contraseña.)
*   [8 Generating user Keytabs which are accepted by AD](#Generating_user_Keytabs_which_are_accepted_by_AD)
    *   [8.1 Nice to know](#Nice_to_know)
*   [9 See also](#See_also)
    *   [9.1 Commercial Solutions](#Commercial_Solutions)

## Terminología

Si no está familiarizado con la terminología de Active Directory aquí tiene algunas palabras que son de ayuda conocer.

*   **Dominio** : El nombre usado para agrupar ordenadores y cuentas.
*   **SID** : Casa ordenador que se une al dominio como miembro tiene que tener un único SID o identificador del sistema.
*   **SMB** : Servidor de mensajes en bloque (Server Message Block).
*   **NETBIOS**: Protocolo de nombres de red (Network naming protocol) utilizado como alternativa a DNS. Más antiguo pero todavía utilizado en la red de Window.
*   **WINS**: Servicio de información de nombres de Windows (Windows Information Naming Service). Utilizado para resolver nombres Netbios a hosts Windows.
*   **Winbind**: Protocolo de autentificación de Windows.

## Configuración de Active Directory

Esta sección funciona con las configuraciones por defecto en Windows Server 2012 R2.

### Consideraciones GPO

La firma digital esta activada por defecto en Windows Server y tiene que estar activada en los niveles cliente y servidor. Para ciertas versiones de Samba los clientes Linux pueden experimentar problemas conectando al dominio y/o a recursos compartidos. Se recomienda que añada los siguientes parámetros a su archivo `smb.conf`:

```
client signing = auto 
server signing = auto

```

Si esto no lo soluciona puede desactivar *Firmar digitalmente las comunicaciones (Siempre)* en las directivas de grupo AD (Active Directory). En su editor de directivas de grupo AD localice:

En *Directivas locales > Directivas de seguridad > Servidor de red Microsoft > Firmar digitalmente las comunicaciones (Siempre)* activar *Definir esta directiva* y utilice el botón de selección *desactivar*.

Si utiliza Windows Server 2008 R2 necesita modificar esto en *GPO para directivas de controlador de dominio por defecto > Ajustes del ordenador > Directivas > Ajustes de Windows > Ajustes de Seguridad > Directivas locales > Opciones de seguridad > Cliente de red Microsoft: Firmar digitalmente las comunicaciones (Siempre)*.

Por favor tenga en cuenta que desactivando esta GPO (Objeto directiva de grupo) afecta a la seguridad de todos los miembros del dominio.

## Configuración del anfitrión Linux

Los siguientes pasos son para comenzar a configurar el anfitrión. Necesitará root o acceso sudo para completar estos pasos.

### Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") los siguientes paquetes:

*   [samba](https://www.archlinux.org/packages/?name=samba), vea también [Samba](/index.php/Samba_(Espa%C3%B1ol) "Samba (Español)")
*   [pam-krb5](https://www.archlinux.org/packages/?name=pam-krb5)
*   [ntp](https://www.archlinux.org/packages/?name=ntp) or [openntpd](https://www.archlinux.org/packages/?name=openntpd), vea también [NTPd](/index.php/Network_Time_Protocol_daemon_(Espa%C3%B1ol) "Network Time Protocol daemon (Español)") o [OpenNTPD](/index.php/OpenNTPD "OpenNTPD")

### Actualizar DNS

Active Directory es muy dependiente de DNS. Necesitará actualizar `/etc/resolv.conf` para utilizar uno o más controladores de dominio de Active Directory:

 `/etc/resolv.conf` 
```
nombreServidor <IP1>
nombreServidor <IP2>

```

Reemplaze <IP1> y <IP2> con unas direcciones IP válidas para los servidores de AD. Si su dominio de AD no permite reenvio de DNS o recursión puede necesitar añadir resolutores adicionales.

**Nota:** Si su maquina tiene un arranque dual Windows y Linux debe de utilizar un nombre DNS y un nombre netbios diferente para la configuración Linux si ambos sistemas operativos son miembros del mismo dominio.

### Configurar NTP

Lea [Sincronización del reloj](/index.php/System_time_(Espa%C3%B1ol)#Sincronización_del_reloj "System time (Español)") para configurar el servicio NTP.

En la configuración del servidor NTP utilice la dirección IP del los servidores AD que normalmente ejecutan NTP como servicio. Otra manera es utilizar otros servidores NTP conocidos proporcionados por la sincronización de los servidores de Active directory a la misma capa.

Asegúrese que el servicio está configurado para sincronizar la hora automáticamente bastante pronto en el inicio.

### Kerberos

Supongamos que su AD se llama ejemplo.com y que su AD está controlado por dos controladores de dominio, el primario y el secundario que se llaman PDC (Primary Domain Controler) y BDC, pdc.ejemplo.com y bdc.ejemplo.com respectivamente. Las direcciones IP serán 192.168.1.2 y 192.168.1.3 en este ejemplo. Tenga en cuenta la sintaxis, las mayúsculas son muy importantes aquí.

 `/etc/krb5.conf` 
```
[libdefaults]
        default_realm 	= 	EJEMPLO.COM
	clockskew 	= 	300
	ticket_lifetime	=	1d
        forwardable     =       true
        proxiable       =       true
        dns_lookup_realm =      true
        dns_lookup_kdc  =       true

[realms]
	EJEMPLO.COM = {
		kdc 	= 	PDC.EJEMPLO.COM
                admin_server = PDC.EJEMPLO.COM
		default_domain = EJEMPLO.COM
	}

[domain_realm]
        .kerberos.server = EJEMPLO.COM
	.ejemplo.com = EJEMPLO.COM
	ejemplo.com = EJEMPLO.COM
	ejemplo	= EJEMPLO.COM

[appdefaults]
	pam = {
	ticket_lifetime 	= 1d
	renew_lifetime 		= 1d
	forwardable 		= true
	proxiable 		= false
	retain_after_close 	= false
	minimum_uid 		= 0
	debug 			= false
	}

[logging]
	default 		= FILE:/var/log/krb5libs.log
	kdc 			= FILE:/var/log/kdc.log
        admin_server            = FILE:/var/log/kadmind.log

```

**Nota:** Heimdal 1.3.1 encriptación DES en desuso que se requiere para la autentificación antes del Windows Server 2008\. Probablemente tendrá que añadir `allow_weak_crypto = true` a la sección `[libdefaults]`.

#### Crear un ticket de Kerberos

**Nota:** Las claves y los comandos son específicos para cada usuario: sudo debe ser root, por tanto su cuenta no elevada puede conectarse a un usuario de AD diferente con una clave separada. Si solo tiene un dominio no es necesario escribir @EJEMPLO.COM

Ahora puede buscar los controladores del dominio de AD y pedir a un ticket a kerberos (**las mayúsculas son necesarias**):

 `kinit administrator@EJEMPLO.COM` 

Puede utilizar cualquier usuario que tenga permisos como Administrador de Dominio.

#### Validar el ticket

Ejecute **klist** para verificar que recibiste el token. Debe de ver algo similar a:

 `# klist` 
```
 Ticket cache: FILE:/tmp/krb5cc_0
 Default principal: administrator@EJEMPLO.COM

 Valid starting    Expires           Service principal 
 02/04/12 21:27:47 02/05/12 07:27:42 krbtgt/EJEMPLO.COM@EJEMPLO.COM
         renew until 02/05/12 21:27:47

```

### pam_winbind.conf

Si recibe errores de estado diciendo que el archivo /etc/security/pam_winbind.conf no se encuentra cree el archivo y añada lo siguiente:

 `/etc/security/pam_winbind.conf` 
```
[global]
  debug = no
  debug_state = no
  try_first_pass = yes
  krb5_auth = yes
  krb5_ccache_type = FILE
  cached_login = yes
  silent = no
  mkhomedir = yes

```

Con estos ajustes winbind creará fichas de usuario sobre la marcha (krb5_ccache_type = FILE) en el inicio de sesión y los mantiene. Puede verificar esto ejecutando simplemente klist en una consola después de iniciar sesión con un usuario de AD pero sin necesidad de ejecutar kinit. Puede necesitar permisos adicionales en /etc/krb5.keytab por ejemplo 640 en vez de 600 para hacer que funcione (vea este ejemplo [FS#52621](https://bugs.archlinux.org/task/52621)).

### Samba

Samba es un programa de software libre que re-implementa el protocolo de red SMB/CIFS. También incluye utilidades para las máquinas Linux para actuar como servidores de red Windows y clientes.

**Nota:** La configuración puede variar bastante dependiendo de como se despliegue el entorno Windows. Prepárese para problemas e investigación

En esta sección nos centraremos primero en hacer que la autentificación funcione editando primero la sección 'Global'. Más tarde volveremos atrás y añadiremos comparticiones.

 `/etc/samba/smb.conf` 
```
[Global]
  netbios name = MYARCHLINUX
  workgroup = EJEMPLO
  realm = EJEMPLO.COM
  server string = %h ArchLinux Host
  security = ads
  encrypt passwords = yes
  password server = pdc.ejemplo.com
  client signing = auto
  server signing = auto

  idmap config * : backend = tdb
  idmap config * : range = 10000-20000

  winbind use default domain = Yes
  winbind enum users = Yes
  winbind enum groups = Yes
  winbind nested groups = Yes
  winbind separator = +
  winbind refresh tickets = yes
  winbind offline logon = yes
  winbind cache time = 300

  template shell = /bin/bash
  template homedir = /home/%D/%U

  preferred master = no
  dns proxy = no
  wins server = pdc.ejemplo.com
  wins proxy = no

  inherit acls = Yes
  map acl inherit = Yes
  acl group control = yes

  load printers = no
  debug level = 3
  use sendfile = no

```

### Unirse al dominio

Necesita una cuenta de AD con permisos de administrados para hacer esto. Supongamos que la cuenta se llama Administrador. El comando es 'net ads join'.

 `# net ads join -U Administrador` 
```
Administrador's password: xxx
Using short domain name -- EJEMPLO
Joined 'MYARCHLINUX' to realm 'EJEMPLO.COM'

```

## Iniciar y comprobar servicios

### Iniciar Samba

¡Milagrosamente no habrá reiniciado aún! Bien. Si esta en una sesión X quitela, de esta forma podrá probar iniciar sesión en otra consola mientras que esté aún con la sesión iniciada.

Active e inicie los demonios individuales de Samba `smbd.service`, `nmbd.service`, y `winbindd.service`.

**Nota:** En [samba](https://www.archlinux.org/packages/?name=samba) 4.8.0-1, los demonios unitarios de Samba se han renombrado a `smbd.service`, `nmbd.service`, y `winbindd.service` a `smb.service`, `nmb.service`, y `winbind.service`.

Lo siguiente que necesitará es modificar la configuración NSSwitch que es la que le dice a Linux como obtener la información de varias fuentes y en qué orden. En este caso dependemos del Active Directory como fuentes adicionales para Usuarios, Grupos, y Hosts.

 `/etc/nsswitch.conf` 
```
 passwd:            files winbind
 shadow:            files winbind
 group:             files winbind 

 hosts:             files dns wins

```

### Comprobar Winbind

Vamos a comprobar si winbind es capaz de listar el AD. El siguiente comando debe de devolver una lista de usuarios de AD:

 `# wbinfo -u` 
```
administrator
guest
krbtgt
test.user

```

*   Note que creamos un usuario de Active Directory llamado 'test.user' en el controlador de dominio.

Podemos hacer lo mismo para grupos de AD:

 `# wbinfo -g` 
```
domain computers
domain controllers
schema admins
enterprise admins
cert publishers
domain admins
domain users
domain guests
group policy creator owners
ras and ias servers
allowed rodc password replication group
denied rodc password replication group
read-only domain controllers
enterprise read-only domain controllers
dnsadmins
dnsupdateproxy

```

### Comprobar nsswitch

Para asegurarse que su host es capaz de listar el domino para usuarios y grupos podemos comprobar los ajustes nsswitch utilizando el comando 'getent'.

Si los usuarios de su Controlador de Dominio no se ven pruebe añadir las siguiente línea a su archivo smb.conf:

 `/etc/samba/smb.conf` 
```
winbind trusted domains only = no

```

La siguiente salida muestra como se ve una instalación de ArchLinux:

 `# getent passwd` 
```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/bin/false
daemon:x:2:2:daemon:/sbin:/bin/false
mail:x:8:12:mail:/var/spool/mail:/bin/false
ftp:x:14:11:ftp:/srv/ftp:/bin/false
http:x:33:33:http:/srv/http:/bin/false
nobody:x:99:99:nobody:/:/bin/false
dbus:x:81:81:System message bus:/:/bin/false
ntp:x:87:87:Network Time Protocol:/var/empty:/bin/false
avahi:x:84:84:avahi:/:/bin/false
administrador:*:10001:10006:Administrador:/home/EJEMPLO/administrador:/bin/bash
guest:*:10002:10007:Guest:/home/EJEMPLO/guest:/bin/bash
krbtgt:*:10003:10006:krbtgt:/home/EJEMPLO/krbtgt:/bin/bash
test.user:*:10000:10006:Test User:/home/EJEMPLO/test.user:/bin/bash

```

Y para los grupos:

 `# getent group` 
```
root:x:0:root
bin:x:1:root,bin,daemon
daemon:x:2:root,bin,daemon
sys:x:3:root,bin
adm:x:4:root,daemon
tty:x:5:
disk:x:6:root
lp:x:7:daemon
mem:x:8:
kmem:x:9:
wheel:x:10:root
ftp:x:11:
mail:x:12:
uucp:x:14:
log:x:19:root
utmp:x:20:
locate:x:21:
rfkill:x:24:
smmsp:x:25:
http:x:33:
games:x:50:
network:x:90:
video:x:91:
audio:x:92:
optical:x:93:
floppy:x:94:
storage:x:95:
scanner:x:96:
power:x:98:
nobody:x:99:
users:x:100:
dbus:x:81:
ntp:x:87:
avahi:x:84:
domain computers:x:10008:
domain controllers:x:10009:
schema admins:x:10010:administrador
enterprise admins:x:10011:administrador
cert publishers:x:10012:
domain admins:x:10013:test.user,administrador
domain users:x:10006:
domain guests:x:10007:
group policy creator owners:x:10014:administrador
ras and ias servers:x:10015:
allowed rodc password replication group:x:10016:
denied rodc password replication group:x:10017:krbtgt
read-only domain controllers:x:10018:
enterprise read-only domain controllers:x:10019:
dnsadmins:x:10020:
dnsupdateproxy:x:10021:

```

### Comprobar comandos de Samba

Pruebe algunos comandos net para ver si Samba se puede comunicar con el AD:

 `# net ads info` 
```
[2012/02/05 20:21:36.473559,  0] param/loadparm.c:7599(lp_do_parameter)
  Ignoring unknown parameter "idmapd backend"
LDAP server: 192.168.1.2
LDAP server name: PDC.ejemplo.com
Realm: EJEMPLO.COM
Bind Path: dc=EJEMPLO,dc=COM
LDAP port: 389
Server time: Sun, 05 Feb 2012 20:21:33 CST
KDC server: 192.168.1.2
Server time offset: -3

```
 `# net ads lookup` 
```
[2012/02/05 20:22:39.298823,  0] param/loadparm.c:7599(lp_do_parameter)
  Ignoring unknown parameter "idmapd backend"
Information for Domain Controller: 192.168.1.2

Response Type: LOGON_SAM_LOGON_RESPONSE_EX
GUID: 2a098512-4c9f-4fe4-ac22-8f9231fabbad
Flags:
        Is a PDC:                                   yes
        Is a GC of the forest:                      yes
        Is an LDAP server:                          yes
        Supports DS:                                yes
        Is running a KDC:                           yes
        Is running time services:                   yes
        Is the closest DC:                          yes
        Is writable:                                yes
        Has a hardware clock:                       yes
        Is a non-domain NC serviced by LDAP server: no
        Is NT6 DC that has some secrets:            no
        Is NT6 DC that has all secrets:             yes
Forest:                 ejemplo.com
Domain:                 ejemplo.com
Domain Controller:      PDC.ejemplo.com
Pre-Win2k Domain:       EJEMPLO
Pre-Win2k Hostname:     PDC
Server Site Name :              Office
Client Site Name :              Office
NT Version: 5
LMNT Token: ffff
LM20 Token: ffff

```
 `# net ads status -U administrador%password | less` 
```
objectClass: top
objectClass: person
objectClass: organizationalPerson
objectClass: user
objectClass: computer
cn: myarchlinux
distinguishedName: CN=myarchlinux,CN=Computers,DC=leafscale,DC=inc
instanceType: 4
whenCreated: 20120206043413.0Z
whenChanged: 20120206043414.0Z
uSNCreated: 16556
uSNChanged: 16563
name: myarchlinux
objectGUID: 2c24029c-8422-42b2-83b3-a255b9cb41b3
userAccountControl: 69632
badPwdCount: 0
codePage: 0
countryCode: 0
badPasswordTime: 0
lastLogoff: 0
lastLogon: 129729780312632000
localPolicyFlags: 0
pwdLastSet: 129729764538848000
primaryGroupID: 515
objectSid: S-1-5-21-719106045-3766251393-3909931865-1105
...<snip>...

```

## Configurar PAM

Ahora cambiaremos varias reglas en PAM para permitir que los usuarios de Active Directory puedan utilizar el sistema para cosas como iniciar sesión y acceso sudo. Cuando se cambian estas reglas note que el orden de estos elementos y cualquier cosa que este marcado como **required** (requerido) o **sufficient** (suficiente) es crítico para que funcione como se espera. No debe desviarse de estas reglas a no haya ser que sepa como escribir reglas PAM.

En el caso de inicios de sesión primero PAM debe de preguntar por las cuentas AD y por las cuentas locales si no encuentra ninguna cuenta de AD. Por lo tanto añadiremos entradas para incluir `pam_winbind.so` en el proceso de autentificación.

La configuración PAM de Arch Linux mantiene el proceso central de autentificación en `/etc/pam.d/system-auth`. Iniciando con la configuración de stock de `pambase`, cambiela como prosigue:

### system-auth

#### Sección "auth"

Encuentre la línea:

```
auth required pam_unix.so ...

```

Elimínela y reemplacela con:

```
auth [success=1 default=ignore] pam_localuser.so
auth [success=2 default=die] pam_winbind.so
auth [success=1 default=die] pam_unix.so nullok
auth requisite pam_deny.so

```

#### Sección "account"

Encuentre la línea:

```
account required pam_unix.so

```

Mantenla y añada esto debajo:

```
account [success=1 default=ignore] pam_localuser.so
account required pam_winbind.so

```

#### Sección "password"

Encuentre la línea:

```
password required pam_unix.so ...

```

Elimínela y reemplacela con:

```
password [success=1 default=ignore] pam_localuser.so
password [success=2 default=die] pam_winbind.so
password [success=1 default=die] pam_unix.so sha512 shadow
password requisite pam_deny.so

```

#### Sección "session"

Encuentre la línea:

```
session required pam_unix.so

```

Mantenla y añada esta línea justo encima de ella:

```
session required pam_mkhomedir.so skel=/etc/skel/ umask=0022

```

Debajo de la línea pam_unix añada esto:

```
session [success=1 default=ignore] pam_localuser.so
session required pam_winbind.so

```

### passwd

#### Sección "password"

Para que los usuarios de Active Directory que han iniciado sesión puedan cambiar sus contraseñas con el comando 'passwd' el archivo `/etc/pam.d/passwd` tiene que incluir información de system-auth.

Encuentre la línea:

```
password required pam_unix.so sha512 shadow nullok

```

Elimínela y reemplacela con:

```
password include system-auth

```

### Comprobar inicio de sesión

Ahora inicie una nueva sesión con consola (o ssh) e intente iniciar sesión con las credenciales de AD. El nombre del dominio es opcional como se establece en la configuración de Winbind como 'default realm'. Por favor tenga en cuenta que en el caso de ssh necesitará modificar el archivo `/etc/ssh/sshd_config` para permitir la autentificación kerberos `(KerberosAuthentication yes)`.

```
test.user
EJEMPLO+test.user

```

Ambos comandos deben funcionar. Debe notar que `/home/example/test.user` se creará automáticamente. **Inicie sesión utilizando una cuenta de Linux. Compruebe si puede iniciar sesión como root - ¡pero tenga en cuenta que tiene que iniciar sesión como root en al menos una sesión!**

## Configurar recursos compartidos

Antes se omitió la configuración de recursos compartidos. Ahora que todo funciona vuelva a `/etc/samba/smb.conf` y añada los recursos del host que quiere que estén disponibles en la red de Windows.

 `/etc/samba/smb.conf` 
```
[MyShare]
  comment = Ejemplo de recurso compartido
  path = /srv/exports/myshare
  read only = no
  browseable = yes
  valid users = @NETWORK+"Domain Admins" NETWORK+test.user

```

En el ejemplo anterior la palabra **NETWORK** se tiene que utilizar. No lo sustituya erróneamente por su nombre de dominio. Para añadir grupos preceda el símbolo '@' del grupo. Note que `Domain Admins` está entre comillas para que Samba lo sustituya cuando lea el archivo de configuración.

## Añadir un ordenador al archivo keytab y activar ssh kerberizado sin contraseña al ordenador

Esto explica cómo generar un ordenador al archivo keytab por el cual puede necesitar, por ejemplo, activar ssh kerberizado sin contraseña a tu ordenador desde otros ordenadores del dominio. El escenario que se plantea es que tenga un grupo de sistemas en su dominio y solo añadió un servidor/espacio de trabajo utilizando la descripción de arriva a su dominio del cual muchos usuarios necesitan ssh para trabajar, por ejemplo, con un espacio de trabajo GPU o con un nodo computacional OpenMP, etc. En este caso puede que no quiera introducir la contraseña cada vez que entre al servidor. Por otra parte muchos usuarios utilizan la autentificación por llave, en este supuesto a lo mejor no puede darle las credenciales necesarias para montar recursos compartidos kerberizados NFSv4, por ejemplo. Esto le ayudará activar los accesos sin contraseña desde sus clientes a la maquina en cuestion utilizando seguimiento de ticket kerberos.

### Crear un archivo keytab del ordenador

Ejecute 'net ads keytab create -U administrador' como root para crear el archivo keytab del ordenador en /etc/krb5.keytab. Mostrará una advertencia de que necesita activar la autentificación keytab en su archivo de configuración, por tanto hágalo en el paso siguiente. En este caso específico hubo problemas cuando se creó el archivo keytab porque ya existía. En este caso el comando se queda sin responder. Para solucionarlo renombre el archivo /etc/krb5.keytab existente y ejecute el comando de nuevo, debería funcionar.

 `# net ads keytab create -U administrador` 

verifique el contenido de su keytab ejecutando:

 `# klist -k /etc/krb5.keytab` 
```
Keytab name: FILE:/etc/krb5.keytab
KVNO Principal
---- --------------------------------------------------------------------------
   4 host/myarchlinux.ejemplo.com@EJEMPLO.COM
   4 host/myarchlinux.ejemplo.com@EJEMPLO.COM
   4 host/myarchlinux.ejemplo.com@EJEMPLO.COM
   4 host/myarchlinux.ejemplo.com@EJEMPLO.COM
   4 host/myarchlinux.ejemplo.com@EJEMPLO.COM
   4 host/MYARCHLINUX@EJEMPLO.COM
   4 host/MYARCHLINUX@EJEMPLO.COM
   4 host/MYARCHLINUX@EJEMPLO.COM
   4 host/MYARCHLINUX@EJEMPLO.COM
   4 host/MYARCHLINUX@EJEMPLO.COM
   4 MYARCHLINUX$@EJEMPLO.COM
   4 MYARCHLINUX$@EJEMPLO.COM
   4 MYARCHLINUX$@EJEMPLO.COM
   4 MYARCHLINUX$@EJEMPLO.COM
   4 MYARCHLINUX$@EJEMPLO.COM

```

### Activar la autentificación keytab

Ahora necesita decirle a winbind que utilice el archivo añadiendo estas lineas a /etc/samba/smb.conf:

```
 kerberos method = secrets and keytab
 dedicated keytab file = /etc/krb5.keytab

```

Se verá algo parecido a esto:

 `/etc/samba/smb.conf` 
```
[Global]
  netbios name = MYARCHLINUX
  workgroup = EJEMPLO
  realm = EJEMPLO.COM
  server string = %h ArchLinux Host
  security = ads
  encrypt passwords = yes
  password server = pdc.ejemplo.com
  kerberos method = secrets and keytab
  dedicated keytab file = /etc/krb5.keytab

  idmap config * : backend = tdb
  idmap config * : range = 10000-20000

  winbind use default domain = Yes
  winbind enum users = Yes
  winbind enum groups = Yes
  winbind nested groups = Yes
  winbind separator = +
  winbind refresh tickets = yes

  template shell = /bin/bash
  template homedir = /home/%D/%U

  preferred master = no
  dns proxy = no
  wins server = pdc.ejemplo.com
  wins proxy = no

  inherit acls = Yes
  map acl inherit = Yes
  acl group control = yes

  load printers = no
  debug level = 3
  use sendfile = no

```

Reinicie el demonio winbind utilizando 'systemctl restart winbindd.service' con privilegios root.

 `# systemctl restart winbindd.service` 

Compruebe que todo funciona obteniendo un ticket del ordenador desde su sistema ejecutando

 `# kinit MYARCHLINUX$ -kt /etc/krb5.keytab` 

No debe de devolver ningún resultado pero ejecutando 'klist' debe mostrarse su sth así:

 `# klist` 
```
 Ticket cache: FILE:/tmp/krb5cc_0
 Default principal: MYARCHLINUX$@EJEMPLO.COM

 Valid starting    Expires           Service principal 
 02/04/12 21:27:47 02/05/12 07:27:42 krbtgt/EJEMPLO.COM@EJEMPLO.COM
         renew until 02/05/12 21:27:47

```

Algunos errores comunes aquí son

*   Olvidar los $ finales o
*   Ignorar la sensibilidad de mayúsculas que son necesarias para las entradas en el keytab (en general no puede haber muchos fallos con todas las mayúsculas).

### Preparar sshd en el servidor

Todo lo que necesita hacer es añadir algunas opciones a su configuración sshd_config y reiniciar sshd.service.

Edite /etc/ssh/sshd_config como sigue en los lugares adecuados:

 `# /etc/ssh/sshd_config` 
```

...

# Cámbiela a no para desactivar las contraseñas s/key
ChallengeResponseAuthentication no

# Opciones Kerberos
KerberosAuthentication yes
#KerberosOrLocalPasswd yes
KerberosTicketCleanup yes
KerberosGetAFSToken yes

# Opciones GSSAPI
GSSAPIAuthentication yes
GSSAPICleanupCredentials yes

...

```

Reinicie el sshd.service utilizando:

 `# systemctl restart sshd.service` 

### Añadir las opciones necesarias en el cliente

Primero necesita asegurarse que los tickets de su cliente se puede transferir. Esto normalmente es un estándar pero es mejor comprobarlo de todas formas. Tiene que mirar la opción transferible y establecerlo a 'true' en el archivo /etc/krb5.conf.

 `forwardable     =       true` 

Después añada las siguientes opciones

```
 GSSAPIAuthentication yes
 GSSAPIDelegateCredentials yes

```

a su archivo .ssh/config para decirle a ssh que utilice estas opciones. Alternativamente se puede invocar directamente con la opción -o en el comando ssh (vea 'man ssh' para más información).

### Comprobar la ejecución

En el cliente:

Asegúrese que tiene un ticket válido - si tiene dudas ejecute 'kinit'.

Después utilice ssh para conectarse a su ordenador.

 `ssh myarchlinux.ejemplo.com ` 

Debe comprobar que se conecta sin necesidad de introducir su contraseña.

Si tiene una llave de autentificación adicional debe realizar

 `ssh -v myarchlinux.ejemplo.com ` 

para ver cual método de autentificación utiliza actualmente.

Para depuración puede activar en el servidor DEBUG3 y mirar en el journal utilizando [journalctl](/index.php/Journalctl "Journalctl").

### Ajuste preciso para un manejo completo de kerberos sin contraseña.

En el caso de que sus clientes no estén utilizando cuentas de dominio en sus ordenadores locales (por cualquier razón) puede ser difícil decirle a kinit antes que a ssh el espacio de trabajo. Sin embargo una solución posible es la que se propone en el siguiente apartado.

## Generating user Keytabs which are accepted by AD

On a system let the user run:

```
ktutil
addent -password -p username@EXAMPLE.COM -k 1 -e RC4-HMAC
- enter password for username -
wkt username.keytab
q

```

Now test the file by invoking:

 `kinit username@EXAMPLE.COM -kt username.keytab` 

It should not promt you to give your password nor should it give any other feedback. If it worked you are basically done - just put the line above into your ~./bashrc - you can now get kerberos tickets without typing a password and with that you can connect to your workstation without typing a password while being completely kerberized and able to authenticate against NFSv4 and CIFS via tickets - pretty neat.

### Nice to know

The file 'username.keytab' is not machinespecific and can therefore be copied around. E.g. we created the files on a linux machine and copied them to our Mac clients as the commands on Macs are different ...

## See also

*   [Wikipedia - Active Directory](https://en.wikipedia.org/wiki/Active_Directory "wikipedia:Active Directory")
*   [Wikipedia - Samba](https://en.wikipedia.org/wiki/Samba_(software) "wikipedia:Samba (software)")
*   [Wikipedia - Kerberos](https://en.wikipedia.org/wiki/Kerberos_(protocol) "wikipedia:Kerberos (protocol)")
*   [Samba - Documentation](http://www.samba.org/samba/docs)
*   [Samba Wiki - Samba & Active Directory](http://wiki.samba.org/index.php/Samba_&_Active_Directory)
*   [`smb.conf(5)` manpage](http://www.samba.org/samba/docs/man/manpages-3/smb.conf.5.html)

### Commercial Solutions

*   Centrify
*   Likewise