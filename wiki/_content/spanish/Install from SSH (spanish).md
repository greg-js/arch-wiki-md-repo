**Estado de la traducción**
Este artículo es una traducción de [Install from SSH](/index.php/Install_from_SSH "Install from SSH"), revisada por última vez el **2019-11-13**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Install_from_SSH&diff=0&oldid=584702) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Este artículo está destinado a mostrar a los usuarios cómo instalar Arch de forma remota a través de una conexión [SSH](/index.php/SSH "SSH"). Considere este enfoque cuando el servidor se encuentra en un lugar remoto o si desea utilizar la capacidad de copiar/pegar de un cliente SSH para realizar la instalación de Arch.

## En la máquina remota (destino)

**Nota:** estos pasos requieren acceso físico a la máquina. Si el equipo se encuentra físicamente en otro lugar, es posible que esto deba coordinarse con otra persona.

Arranque la máquina de destino en un entorno live de Arch a través de una [imagen USB/CD Live](/index.php/Getting_and_installing_Arch_(Espa%C3%B1ol) "Getting and installing Arch (Español)"): esto registrará al usuario como root.

En este punto, configure la red en la máquina de destino como, por ejemplo, se sugiere en [Installation guide (Español)#Conectarse a Internet](/index.php/Installation_guide_(Espa%C3%B1ol)#Conectarse_a_Internet "Installation guide (Español)").

En segundo lugar, configure una contraseña de root necesaria para una conexión SSH, ya que la contraseña de Arch predeterminada para root está vacía:

```
# passwd

```

Ahora compruebe que `PermitRootLogin yes` está presente (y sin comentar) en `/etc/ssh/sshd_config`. Esta configuración permite el inicio de sesión como root con autenticación de contraseña en el servidor SSH.

Finalmente, [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") el demonio openssh con `sshd.service`, que se incluye por defecto en el CD live.

**Nota:** a menos que se requiera, se recomienda, después de la instalación, eliminar `PermitRootLogin yes` de `/etc/ssh/sshd_config`.

**Sugerencia:** si la máquina de destino está detrás de un enrutador NAT, y necesita acceso externo, el puerto SSH (22 por defecto) deberá reenviarse a la dirección IP de la LAN de la máquina de destino.

## En la máquina local

En la máquina local, conéctese a la máquina de destino a través de SSH con la siguiente orden:

```
$ ssh root@*ip.address.of.target*

```

A partir de aquí se le presentará el mensaje de bienvenida del entorno live y podrá administrar la máquina de destino como si estuviera sentado frente a su teclado físico. En este punto, si la intención es simplemente instalar Arch desde el soporte live, siga la [Installation guide (Español)](/index.php/Installation_guide_(Espa%C3%B1ol) "Installation guide (Español)"). Si la intención es editar una instalación de Linux existente con problemas, siga el artículo de la wiki [Install from existing Linux (Español)](/index.php/Install_from_existing_Linux_(Espa%C3%B1ol) "Install from existing Linux (Español)").

**Sugerencia:** considere instalar un [multiplexor de terminal](/index.php/List_of_applications#Terminal_multiplexers "List of applications") en el sistema live de la máquina de destino (en la memoria), de modo que si se desconecta pueda reengancharse a la sesión de su multiplexor.