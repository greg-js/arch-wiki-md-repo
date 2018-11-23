**Estado de la traducción**
Este artículo es una traducción de [Sony Vaio Z21V9E](/index.php/Sony_Vaio_Z21V9E "Sony Vaio Z21V9E"), revisada por última vez el **2018-11-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Sony_Vaio_Z21V9E&diff=0&oldid=349264) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

## Instalación

El único obstáculo real para instalar Arch Linux es la configuración RAID. Hay distintas alternativas con varias ventajas y desventajas. Lo más fácil es dejar el raid habilitado según la configuración de fábrica y tratar la partición resultante como una sola unidad.

 `lsblk` 
```
$ lsblk
NAME        MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
sda           8:0    0 119.2G  0 disk  
└─md126       9:126  0 238.5G  0 raid0 
  ├─md126p1 259:0    0  15.6G  0 md    /
  └─md126p2 259:1    0 221.9G  0 md    /home
sdb           8:16   0 119.2G  0 disk  
└─md126       9:126  0 238.5G  0 raid0 
  ├─md126p1 259:0    0  15.6G  0 md    /
  └─md126p2 259:1    0 221.9G  0 md    /home

```

Como puede ver, el sistema contiene dos unidades separadas que se han utilizado para crear una única partición RAID, raid0\. Cuando prepare su unidad de almacenamiento durante la instalación, tratará esa partición raid0 como la unidad en la que se hará la instalación.

 `cfdisk /dev/md126` 
```
                    Disk: /dev/md126
                                                             Size: 238.5 GiB, 256066453504 bytes, 500129792 sectors
                                                                       Label: dos, identifier: 0x000932f6

    Device                     Boot                                 Start                     End                 Sectors                Size              Id Type
    /dev/md126p1               *                                     2048                32770047                32768000               15.6G              83 Linux
    /dev/md126p2                                                 32770048               498081791               465311744              221.9G              83 Linux
>>  Free space                                                  498081792               500129791                 2048000               1000M                      

```

Alternativamente, simplemente desactive el IRST y trate las dos unidades SSD por separado.