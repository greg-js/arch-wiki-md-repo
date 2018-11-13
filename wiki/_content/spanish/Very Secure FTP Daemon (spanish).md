**vsftpd** es el "**v**ery **s**ecure **ftp** **d**aemon" (demonio ftp muy seguro) , un pequeño pero eficiente servidor FTP.

Como puede correr con o sin [xinetd](https://es.wikipedia.org/wiki/Xinetd), serán explicados los dos métodos.

## Contents

*   [1 Sin xinetd (simple)](#Sin_xinetd_(simple))
*   [2 Usando xinetd](#Usando_xinetd)
*   [3 PAM with "virtual users"](#PAM_with_"virtual_users")
    *   [3.1 Para agregar carpetas privadas para los usuarios virtuales](#Para_agregar_carpetas_privadas_para_los_usuarios_virtuales)

## Sin xinetd (simple)

En primer lugar, instala el paquete necesario con pacman:

```
# pacman -S vsftpd

```

`/etc/vsftpd.conf` es un archivo de configuración muy bien documentado, pero estas son las cosas básicas para configurar (leer el resto del archivo):

```
listen=YES          # Permite a vsftpd actuar como un servidor independiente
anonymous_enable=NO # Si lo deseas, puedes acceder al servidor de forma anónima
local_enable=YES    # Esto permite a los usuarios acceso al servidor FTP local
write_enable=YES    # Sea muy cuidadoso usando anonymous_enable=YES

```

Luego anexar 'vsftpd: ALL' a tu archivo /etc/hosts.allow. Luego puedes iniciar el servidor con el comando /etc/rc.d/vsftpd start. Agregalo a su lista de DAEMONS en /etc/rc.conf si quieres que inice cuando el sistema operativo lo haga.

## Usando xinetd

Primero, instala con pacman los paquetes que vas a necesitar:

```
# pacman -S xinetd vsftpd

```

Los siguientes archivos de configuración necesitarán ser modificados:

/etc/xinetd.d/vsftpd:

```
service ftp
{
        socket_type             = stream
        wait                    = no
        user                    = root
        server                  = /usr/sbin/vsftpd
        log_on_success  += HOST DURATION
        log_on_failure  += HOST
        disable                 = no
}

```

/etc/vsftpd.conf es un archivo de configuracion muy bien documentado, pero hay cosas básicas que probablemente querras establecer:

```
anonymous_enable=NO      # Assuming you do not want anonymous ftp
local_enable=YES         # This lets local machine users log in
write_enable=YES    # Be really careful using this with anonymous_enable=YES
tcp_wrappers=YES    # Use tcp_wrappers to control connections. Then allow in hosts.allow
pam_service_name=vsftpd

```

/etc/hosts.allow - agrega las siguientes entradas (por razones de seguridad hosts.allow puede ser configurado de otra forma. /etc/hosts.deny and /etc/hosts.allow

```
vsftpd: ALL

```

Finalmente, agrega xinetd a tu lista de daemons o demonios en /etc/[rc.conf](/index.php/Rc.conf "Rc.conf"). No necesitas agregarvsftpd, ya que será llamado por xinetd siempre que sea necesario.

Si obtienes errores como

```
500 OOPS: cap_set_proc

```

cuando te conectes al servidor, necesitas agregar *capability* en la línea MODULES= en /etc/rc.conf.

Cuando actualizas a **version 2.1.0** podrías obtener un error como estecuando te estés conectando al servidor desde un cliente:

```
500 OOPS: could not bind listening IPv4 socket

```

En versiones anteriores ha sido suficiente con dejar comentadas las siguientes líneas:

```
# Use this to use vsftpd in standalone mode, otherwise it runs through (x)inetd
# listen=YES

```

En esta nueva versión, y probablemente en las futuras, es necesario configurarlo explícitamente para que *no* fncione en forma independiente, asi:

```
# Use this to use vsftpd in standalone mode, otherwise it runs through (x)inetd
listen=NO

```

## PAM with "virtual users"

Al usar usuarios virtuales está la ventaja de no requerir una sesion real del usuario en el sistema. Mantener el ambiente en un recipiente es, por supuesto, una opción mas segura.

Una base de datos de usuarios virtuales debe ser creada primero haciendo un simple archivo de texto como el siguiente:

```
user1
password1
user2
password2

```

Incluye el número de usuarios virtuales que desees de acuerdo con la estructura del ejemplo. Guárdalo como logins.txt; el nombre del archivo no tiene ningun significado. El siguiente paso depende del sistema de base de datos de Berkeley, que se incluye en el sistema base de Arch. Como root crea la actual base de datos con la ayuda del archivo logins .txt , o el nombre que haya elegido:

```
# db_load -T -t hash -f logins.txt /etc/vsftpd_login.db

```

Es recomendado restringir permisos al nuevo archivo creado vsftpd_login.db :

```
# chmod 600 /etc/vsftpd_login.db

```

**Advertencia:** Tenga en cuenta que guardar passwords en un archivo de texto plano no es seguro. No olvides borrar tu archivo temporal con `rm logins.txt`.

PAM debe ser ahora configurado para que use vsftpd_login.db. Para hacer que PAM compruebe la autenticación de usuarios crea un archivo llamado ftp en el directorio /etc/pam.d/ con la siguiente información:

```
auth required /lib/security/pam_userdb.so db=/etc/vsftpd_login crypt=hash 
account required /lib/security/pam_userdb.so db=/etc/vsftpd_login crypt=hash

```

Atención! Usamos /etc/vsftpd_login sin la extension .db en PAM-config! Ahora es la hora de crear un home para los usuarios virtuales. En el ejemplo /srv/ftp es usada para alojar datos para los usuarios virtuales, lo que refleja tambien la estructura de directorios por defecto de Arch. Primero crea el usuario virtual general y haz que su home sea /srv/ftp :

```
# useradd -d /srv/ftp virtual

```

Hacer vitual al propietario:

```
# chown virtual:virtual /srv/ftp

```

Configura vsftpd para usar el entorno creado editando /etc/vsftpd.conf. Estas son los ajustes necesarios para hacer que vsftpd restrinja el acceso a usuarios virtuales, a traves de usuario y contraseña, y restringir su acceso al area especificada /srv/ftp:

```
anonymous_enable=NO
local_enable=YES
chroot_local_user=YES
guest_enable=YES
guest_username=virtual
virtual_use_local_privs=YES

```

Si el método xinetd es usado, inicia el servicio ej: '/etc/rc.d/xinetd start'. Ahra deberías estar permitido de iniciar sesión a traves de un usuario y una contraseña de acuerdo con la base de datos creada.

### Para agregar carpetas privadas para los usuarios virtuales

Primero crea sus directorios

```
# mkdir /srv/ftp/usuario1
# mkdir /srv/ftp/usuario2
# chown virtual:virtual /srv/ftp/user?/

```

Nuevamente, en tu archivo vsftpd.conf , agrega lo siguiente.

```
local_root=/srv/ftp/$USER
user_sub_token=$USER

```