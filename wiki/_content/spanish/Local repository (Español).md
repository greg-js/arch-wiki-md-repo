## Como hacer un repositorio local (1 forma)

Este documento es una de las muchas maneras de compartir paquetes de ArchLinux en una LAN. una mejor manera de hacer esto es con [Repositorio local con ABS y gensync](/index.php?title=Repositorio_local_con_ABS_y_gensync&action=edit&redlink=1 "Repositorio local con ABS y gensync (page does not exist)") y hacer el repositorio disponible LAN usando NFS ó FTP. Este documento es una traducción exacta del Wiki en ingles:

```
To share all your downloaded packages in your lan
Pros  save bandwith, diskspace and time.
"pacman -Sy"  will sync against our local repository
"pacman -S pkgname" try to download and install pkg from localserver if pkg not exist it download
from the next server in the list /etc/pacman.conf and save pkg on localserver.
"alsync" will update localserver db against ftp.archlinux.org

ex. for my network
serverip=192.168.14.3
network=192.168.14.0/255.255.255.0
adjust to yours

1\. serverside
on your server create an nfs share readwrite for all pc on your lan

if you run archlinux on the server you can
pacman -S portmap
pacman -S nfs-utils

edit /etc/exports
add line
/var/cache/pacman/pkg  192.168.14.0/255.255.255.0(rw,no''root''squash,sync)
add portmap, nfslock and nfsd to DAEMONS in /etc/rc.conf

run  /etc/rc.d/portmap start
run  /etc/rc.d/nfslock start
run  /etc/rc.d/nfsd start
to check the nfsshare run "exportfs" on server.

1.1 Check hosts.allow and hosts.deny

to work (very simple):

hosts.deny
ALL: ALL: DENY

hosts.allow
ALL: 192.168.14.

Explanation: 

hosts.deny deny all connection that doesnt exist on hosts.allow.
hosts.allow allow connection from local network 192.168.14.0/255.255.255.0

2\. on all clients
rename  /var/cache/pacman/pkg  to /var/cache/pacman/pkgorg
create a new /var/cache/pacman/pkg and mount the nfs share there

run "mount -o rw,nolock 192.168.14.3:/var/cache/pacman/pkg /var/cache/pacman/pkg"
or if you want it automount on client reboot
add this line in /etc/fstab
192.168.14.3:/var/cache/pacman/pkg /var/cache/pacman/pkg    nfs    rw,nolock
run "mount -a"
run "df" to check mount

move all your already fetched pkg from your clients
/var/cache/pacman/pkgorg to /var/cache/pacman/pkg

edit /etc/pacman.conf and add this lines directly after the line

{current}
Server = file:///var/cache/pacman/pkg

     '''''' and after ''''''
{extra}
Server = file:///var/cache/pacman/pkg

3\. to sync your local repository v.s. archlinux
"alsync" connects, login, and update your packages database on the local nfsserver
pacman -S openssl
pacman -S wget

create a file called /bin/alsync and put in this lines
''''''''''''''' content of alsync '''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''
cd /var/cache/pacman/pkg
wget -N ftp://ftp.archlinux.org/current/'''.db.'''
wget -N ftp://ftp.archlinux.org/extra/'''.db.'''
''''''''''''''''''''''''''' end '''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''''*

chmod 777 /bin/alsync
copy this file to your clients

to try run as root on first client
alsync
pacman -Sy
pacman -S new-pkgname

move to next client and run
pacman -Sy
pacman -S new-pkgname

```

## Como hacer un repositorio local (2 forma)

El siguiente script sincroniza (mediante rsync) un repositorio de Arch con un directorio en nuestro PC. Compartiendo este directorio mediante NFS, Samba, FTP o lo que sea podremos actualizar todas las máquinas de nuestra LAN sin que cada una de ellas deba bajarse las actualizaciones de Internet.

El ejemplo siguente almacena en /repositorio el contenido de current, extra y community para arquitectura i686\. En total no llega a 7GB. Si queremos también unstable y testing debemos eliminar las lineas que los excluyen. Lo mismo para las ISOs o para los repositorios de x86_64:

```
#!/bin/bash
# Sincroniza el repositorio de Arch del servidor ‘distro.ibiblio.org’
# con el directorio /repositorio

# Definición de los parámetros usados:
#
# a, –archive –> archive mode; same as -rlptgoD (no -H)
# v, –verbose –> increase verbosity
# r, –recursive –> recurse into directories

rsync -arv \
–delete-after \
–exclude=0.7.2 \
–exclude=iso \
–exclude=x86_64 \
–exclude=images \
–exclude=other \
–exclude=release \
–exclude=unstable \
–exclude=testing \
distro.ibiblio.org::distros/archlinux/ \
/repositorio/

```

Esto puede cambiar según el repositorio fuente usado. En el que uso como ejemplo no se almacenan versiones anteriores a la 0.7.2 por lo que no hace falta excluirlas.

El parámetro –delete-after es muy importante, sirve para eliminar los paquetes del destino (nuestro PC) cuando ya no están en el origen (por ejemplo, eliminar foo-1.tar.gz si hay disponible foo-2.tar.gz). El resto de parámetros creo que ya están bien explicados en el propio script, para más información: man rsync

El siguente paso es decirle a pacman que no busque los paquetes en Internet sino en /repositorio. Esto es realmente fácil, sólo hay que modificar el fichero /etc/pacman.conf de la siguiente forma:

```
[current]
Server = file:///repositorio/current/os/i686

[extra]
Server = file:///repositorio/extra/os/i686

[community]
Server = file:///repositorio/community/os/i686

```

Ahora el siguiente paso es usar cron para automatizar la sincronización, pero esto os lo dejo a vosotros.