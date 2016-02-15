Para compartir paquetes entre computadoras, simplemente comparte _/var/cache/pacman/_ usando cualquier protocolo de compartición que permita el montaje de archivos; por ejemplo [Samba](/index.php/Samba "Samba") ó [NFS](/index.php/NFS "NFS"). También puedes usar sshfs el cual es mas seguro pero un poco lento. Esta guía muestra como usar shfs ó sshfs para compartir la cache de paquetes y los directorios de librerías entre varias computadoras en la misma red.

## Contents

*   [1 Usando compartición de la caché](#Usando_compartici.C3.B3n_de_la_cach.C3.A9)
    *   [1.1 Usando sshfs](#Usando_sshfs)
        *   [1.1.1 sshfs vs. shfs](#sshfs_vs._shfs)
    *   [1.2 Usando nfs](#Usando_nfs)

## Usando compartición de la caché

Primero, instala cualquier compartición de red - sshfs, shfs, ftpfs, smbfs, nfs etc.

### Usando sshfs

```
pacman -S sshfs

```

Entonces monta `/var/cache/pacman/pkg` de tu servidor a `/var/cache/pacman/pkg` en cada máquina del cliente.

```
mount sshfs#root@alpha:/var/cache/pacman/pkg/ /var/cache/pacman/pkg

```

¡Eso es todo! Ahora tienes una caché compartida.

Si también quieres compartir la base de datos de la máquina, necesitas montar `/var/lib/pacman/{current,extra,testing,community,unstable}` de la misma manera.

**Advertencia:** ¡No montar `/var/lib/pacman/local`!

Puedes modificar tu `/etc/fstab` como esto:

```
sshfs#root@alpha:/var/cache/pacman/pkg/ /var/cache/pacman/pkg fuse rw,reconnect 0 0
sshfs#root@alpha:/var/lib/pacman/testing/ /var/lib/pacman/testing fuse rw,reconnect 0 0
sshfs#root@alpha:/var/lib/pacman/current/ /var/lib/pacman/current fuse rw,reconnect 0 0
sshfs#root@alpha:/var/lib/pacman/extra/ /var/lib/pacman/extra fuse rw,reconnect 0 0
sshfs#root@alpha:/var/lib/pacman/community/ /var/lib/pacman/community fuse rw,reconnect 0 0

```

ó así:

```
root@alpha:/var/cache/pacman/pkg/ /var/cache/pacman/pkg shfs rw,preserve,persistent 0 0
root@alpha:/var/lib/pacman/testing/ /var/lib/pacman/testing shfs rw,preserve,persistent 0 0
root@alpha:/var/lib/pacman/current/ /var/lib/pacman/current shfs rw,preserve,persistent 0 0
root@alpha:/var/lib/pacman/extra/ /var/lib/pacman/extra shfs rw,preserve,persistent 0 0
root@alpha:/var/lib/pacman/community/ /var/lib/pacman/community shfs rw,preserve,persistent 0 0

```

**Nota:** usar base de datos compartida puede ser lento, dependiendo del sistema de archivos de red y la carga de la LAN.

**Tip:** Si quieres usar sshfs ó shfs deberías leer [SSH - Uso de claves](/index.php?title=SSH_-_Uso_de_claves&action=edit&redlink=1 "SSH - Uso de claves (page does not exist)").

#### sshfs vs. shfs

*   sshfs es un sistema de archivos, shfs es un módulo del kernel.
*   Existen algunos problemas con shfs.

### Usando nfs

```
 pacman -S nfs-utils

```

NFS puede ser rápido para redes locales, ya que no hay cifrado. Sin embargo, la configuración es mas compleja.

*   En el "servidor"
    *   Agrega portmap, nfslock, y nfsd a la lista de DAEMONS en rc.conf (e iniciarlos) en este orden.
    *   En /etc/exports, agregar:

```
 #List machines allowed to mount this share.
 # See 'man exports' for details
 #A single machine on the network
 /var/cache/pacman/pkg/ 192.168.1.199(rw,sync,subtree_check)
 #The entire local network
 /var/cache/pacman/pkg/ 192.168.1.199(rw,sync,subtree_check)

```

*   *   Agregar los clientes que se conectarán a /etc/hosts.allow

Si es una sola máquina:

```
 ALL : 192.168.1.199 : ALLOW

```

Para varias:

```
 portmap : 192.168.1.199 : ALLOW
 lockd : 192.168.1.199 : ALLOW
 mountd : 192.168.1.199 : ALLOW
 rquoted : 192.168.1.199 : ALLOW
 statd : 192.168.1.199 : ALLOW

```

*   En los "cliente(s)"
    *   Agrega portmap a la lista de DAEMONS en rc.conf (e iniciarlo).
    *   Agrega una entrada en /etc/fstab:

```
 # mount the shared cache on 192.168.1.25 (our server)
 192.168.1.25:/var/cache/pacman/pkg/ /var/cache/pacman/pkg/ nfs rw 0 0

```