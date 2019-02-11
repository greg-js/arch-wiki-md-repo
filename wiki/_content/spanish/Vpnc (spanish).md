**Estado de la traducción**
Este artículo es una traducción de [Vpnc](/index.php/Vpnc "Vpnc"), revisada por última vez el **2018-10-05**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Vpnc&diff=0&oldid=541096) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[vpnc](https://www.unix-ag.uni-kl.de/~massar/vpnc/) es un cliente VPN para los redes privadas virtules del hardware de Cisco.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Configuración](#Configuración)
*   [3 Inicio](#Inicio)
*   [4 Solución de problemas](#Solución_de_problemas)

## Instalación

[Instale](/index.php/Install "Install") el paquete [vpnc](https://www.archlinux.org/packages/?name=vpnc).

## Configuración

Los archivos de configuración vpnc están en `/etc/vpnc`. Contiene un archivo `default.conf` que puede copiar y modificar para la configuración.

La ejecución de `vpnc --long-help` proporcionará los nombres y descripciones de las diversas opciones de configuración. Por ejemplo, en esa salida verá:

```
 --gateway <ip/hostname>
     IP/name of your IPSec gateway
 conf-variable: IPSec gateway<ip/hostname>

```

que se traduce en una línea como esta en su archivo de configuración:

```
IPSec gateway gateway.example.com

```

## Inicio

El paquete `vpnc` viene con una unidad de [systemd](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") `vpnc @ .service`. Si desea utilizar el archivo de configuración `/etc/vpnc/client.conf`, debería iniciarlo con `systemctl start vpnc@client`.

## Solución de problemas

En caso de que el cliente vpnc se bloquee con:

```
   May 15 09:11:38 ntrp-mimacom systemd-coredump[5858]: Process 5814 (vpnc) of user 0 dumped core.

                                                        Stack trace of thread 5814:
                                                        #0  0x00007f835cba3a10 raise (libc.so.6)
                                                        #1  0x00007f835cba513a abort (libc.so.6)
                                                        #2  0x00007f835cb9c607 __assert_fail_base (libc.so.6)
                                                        #3  0x00007f835cb9c6b2 __assert_fail (libc.so.6)
                                                        #4  0x000000000040e48c n/a (vpnc)
                                                        #5  0x0000000000412348 n/a (vpnc)
                                                        #6  0x0000000000404f72 n/a (vpnc)
                                                        #7  0x00007f835cb90511 __libc_start_main (libc.so.6)
                                                        #8  0x000000000040596a n/a (vpnc)

```

tendrá que aplicar el parche al software porque una afirmación está fallando con las últimas actualizaciones.

Descargue las fuentes de [http://svn.unix-ag.uni-kl.de/vpnc/trunk/](http://svn.unix-ag.uni-kl.de/vpnc/trunk/) y corrija el archivo vpnc.c con lo siguiente:

```
   Índice: vpnc.c
   ===================================================================
   --- vpnc.c      (revision 550)
   +++ vpnc.c      (working copy)
   @@ -1206,7 +1206,7 @@
           assert(a->af == isakmp_attr_16);
           assert(a->u.attr_16 == IKE_LIFE_TYPE_SECONDS || a->u.attr_16 == IKE_LIFE_TYPE_K);
           assert(a->next != NULL);
   -       assert(a->next->type == IKE_ATTRIB_LIFE_DURATION);
   +       /* assert(a->next->type == IKE_ATTRIB_LIFE_DURATION); */

           if (a->next->af == isakmp_attr_16)
                   value = a->next->u.attr_16;

```

La solución temporal se encuentra aquí: [https://bbs.archlinux.org/viewtopic.php?id=225556](https://bbs.archlinux.org/viewtopic.php?id=225556)

Recuerde cambiar PREFIX a /usr en lugar de /usr/local para que sobrescriba el binario roto.