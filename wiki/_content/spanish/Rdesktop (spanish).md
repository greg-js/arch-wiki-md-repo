**Estado de la traducción**
Este artículo es una traducción de [Rdesktop](/index.php/Rdesktop "Rdesktop"), revisada por última vez el **2018-11-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Rdesktop&diff=0&oldid=555859) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [xrdp](/index.php/Xrdp "Xrdp")
*   [Remmina](/index.php/Remmina "Remmina")

[rdesktop](http://www.rdesktop.org/) es un cliente para el protocolo propietario RDP de Microsoft libre y de código abierto publicado bajo la licencia GNU General Public License. Use rdesktop para administrar remotamente servidores RDP de Windows 2000/XP/Vista/Win7/Win10.

Desde julio de 2008, rdesktop implementa un gran conjunto de acciones para el protocolo RDP5, entre las que se encuentran:

*   Caché de bitmap (bitmap caching).
*   Redirección de sistema de ficheros, audio, puerto serie y puerto de impresora
*   Mapeo para la mayoría de teclados internacionales
*   Stream compression y encriptado
*   Autenticación automática
*   Soporte para smartcard
*   Aplicaciones remotas como por ejemplo el soporte modo "seamless" vía SeamlessRDP

Aún sin implementar se encuentran:

*   Peticiones de asistencia remota
*   Redirección de dispositivos USB

Soporte para funcionalidades adicionales disponibles en RDP 5.1 y RDP 6 (incluyendo pantalla multi-head spanning y composición multiventana) aún no han sido implementadas.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Utilización](#Utilización)
*   [3 Trucos y consejos](#Trucos_y_consejos)
    *   [3.1 Escalado automático de geometría de pantalla](#Escalado_automático_de_geometría_de_pantalla)
    *   [3.2 Escritorio remoto usando nombres NetBIOS en lugar de direcciones IP](#Escritorio_remoto_usando_nombres_NetBIOS_en_lugar_de_direcciones_IP)
    *   [3.3 Obteniendo cursores perdidos](#Obteniendo_cursores_perdidos)
*   [4 Véase también](#Véase_también)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [rdesktop](https://www.archlinux.org/packages/?name=rdesktop) desde los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

## Utilización

Para una lista completa de opciones véase [rdesktop(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rdesktop.1). Aquí puede ver una sentencia típica:

```
$ rdesktop -g 1440x900 -P -z -x l -r sound:off -u windowsuser 98.180.102.33:3389

```

Leyendo de izquierda a derecha:

| `-g 1440x900` | Establece la resolución de la pantalla a 1440x900 |
| `-P` | Establece bitmap caching/aceleración xfers. |
| `-z` | Establece la compresión del streaming de datos RDP |
| `-x l` | Establece nivel de experiencia de calidad "LAN". Revisa la página del man para opciones adicionales |
| `-r sound:off` | Redirige el sonido generado en el servidor a null |
| `-u windowsuser` | Define el usuario a usar para iniciar sesión en la máquina Windows |
| `98.180.102.33:3389` | Indica la dirección IP y el puerto de la máquina objetivo |

## Trucos y consejos

### Escalado automático de geometría de pantalla

Para escalar automáticamente la geometría de la pantalla para coincidir con el monitor actual, pasa los parámetros

```
-g $(xrandr -q | awk '/Screen 0/ {print int($8/1.28) $9 int($10/1.2)}' | sed 's/,//g')

```

a la orden rdesktop.

Otra opción es usar la directiva -g

```
 $ rdesktop -g 100% -P -z 98.180.102.33:3389

```

### Escritorio remoto usando nombres NetBIOS en lugar de direcciones IP

Si no conoce la dirección IP de la máquina Windows, tiene que activar wins support. Para ello, debe instalar [samba](/index.php/Samba "Samba"). Activar wins en samba es sorprendentemente fácil: solo edite el fichero `/etc/samba/smb.conf` y añada la siguiente línea al mismo, o descoméntela si ya existiera:

```
wins support = yes

```

Ahora debe instalar winbind, entonces edite el fichero `/etc/nsswitch.conf` y añada "wins" a la lista de hosts.

Reinicie los servicios `smbd` y `nmbd` y compruebe que tiene conexión realizando ping a un host Windows NetBIOS.

### Obteniendo cursores perdidos

Revise [Cursor themes (Español)#Configurando temas de cursor](/index.php/Cursor_themes_(Espa%C3%B1ol)#Configurando_temas_de_cursor "Cursor themes (Español)").

## Véase también

*   [Web oficial de Rdesktop](http://www.rdesktop.org/)
*   [freerdp](https://www.archlinux.org/packages/?name=freerdp) Un fork de rdesktop que soporta funcionalidades de RDP 7.1 incluyendo autenticación de nivel de red (NLA). Véase también [[1]](http://askubuntu.com/a/97932/217269).