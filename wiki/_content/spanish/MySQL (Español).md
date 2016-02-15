MySQL es una gran base de datos SQL multi-hilo y multi-usuario. Para mas información, mira [su página oficial](http://www.mysql.com/).

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
*   [3 Habilitar acceso remoto](#Habilitar_acceso_remoto)
*   [4 Habilitar autocompletado](#Habilitar_autocompletado)
*   [5 Como resetear la contraseña del Root](#Como_resetear_la_contrase.C3.B1a_del_Root)

## Instalación

[Instala](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") el paquete [mysql](https://aur.archlinux.org/packages/mysql/).

Despues de la instalación es necesario ejecutar el servicio de mysqld para poder proseguir:

Si estas usando systemd:

```
# systemctl start mysqld.service 

```

Si estas en initscripts

```
# rc.d start mysqld

```

Para configurar la contraseña del root, deberemos correr el script de instalación, este tambien nos permitira configurar algunas otras cosas como los usuarios anonimos, deshabilitar el login remote, y remover las bases de datos de prueba:

```
# mysql_secure_installation

```

Al finalizar el script simplemente nos permitira recargar los privilegios de las tablas y con esto tendremos configurado Mysql.

## Configuración

Una vez iniciado el servidor MySQL, podras utilizarlo con tu interfaz preferida, por ejemplo:

```
$ mysql -p -u root

```

Para iniciar MySQL al arranque:

Si usas systemd:

```
#systemctl enable mysqld.service

```

Si usas initscripts agrega `mysqld` a la lista de demonios en `/etc/rc.conf`

```
DAEMONS=(....mysqld)

```

## Habilitar acceso remoto

El servidor MySQL no escucha en el puerto TCP 3306 por defecto. Para permitir conexiones (remotas) TCP, comenta la línea que contiene `skip-networking` en `/etc/mysql/my.cnf`.

## Habilitar autocompletado

El autocompletado en MySQL esta deshabilitado por defecto, para habilitarlo edite el archivo `/etc/mysql/my.cnf` y rempace la linea que dice `no-auto-rehash` por `auto-rehash`, el cambio se notara la proxima vez que inicie MySQL.

## Como resetear la contraseña del Root

Deten el demonio mysqld

Si estas en systemd

```
#systemctl stop mysqld.service
# mysqld_safe --skip-grant-tables &

```

Si estas en initscripts

```
# rc.d stop mysqld
# mysqld_safe --skip-grant-tables &

```

Conectar al servidor mysql

```
# mysql -u root mysql

```

Cambia la contraseña del root:

```
 mysql> UPDATE user SET password=PASSWORD("NEW_PASSWORD") WHERE User='root';
 mysql> FLUSH PRIVILEGES;
 mysql> exit

```

Entonces Inicia el demonio: Si estas en systemd

```
#systemctl start mysqld.service

```

Si estas en initscripts

```
# rc.d start mysqld

```

Listo.