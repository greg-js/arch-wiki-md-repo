**Estado de la traducción**
Este artículo es una traducción de [Wireshark](/index.php/Wireshark "Wireshark"), revisada por última vez el **2019-10-06**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Wireshark&diff=0&oldid=584509) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[Wireshark](https://www.wireshark.org/) es un analizador de paquetes gratuito y de código abierto. Se utiliza para la resolución de problemas de red, análisis, desarrollo de software y protocolo de comunicaciones, y con fines educativos.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Capturar privilegios](#Capturar_privilegios)
*   [3 Algunas técnicas de captura](#Algunas_técnicas_de_captura)
    *   [3.1 Filtrar paquetes TCP](#Filtrar_paquetes_TCP)
    *   [3.2 Filtrar paquetes UDP](#Filtrar_paquetes_UDP)
    *   [3.3 Filtrar paquetes a una dirección IP específica](#Filtrar_paquetes_a_una_dirección_IP_específica)
    *   [3.4 Excluir paquetes de una dirección IP específica](#Excluir_paquetes_de_una_dirección_IP_específica)
    *   [3.5 Filtrar paquetes a la LAN](#Filtrar_paquetes_a_la_LAN)
    *   [3.6 Filtrar paquetes por puerto](#Filtrar_paquetes_por_puerto)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt) para la interfaz gráfica de Wireshark o [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) para usar solo la [CLI](https://en.wikipedia.org/wiki/es:Interfaz_de_l%C3%ADnea_de_comandos "wikipedia:es:Interfaz de línea de comandos") `tshark`.

**Nota:** la interfaz GTK en desuso se ha eliminado en Wireshark 3.0

## Capturar privilegios

No ejecute Wireshark como root, es inseguro. Wireshark ha implementado la separación de privilegios [[1]](https://wiki.wireshark.org/CaptureSetup/CapturePrivileges#Most_UNIXes).

El [script de instalación](/index.php/PKGBUILD#install "PKGBUILD") [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) establece la captura de paquetes [capabilities](/index.php/Capabilities "Capabilities") en el ejecutable `/usr/bin/dumpcap`.

`/usr/bin/dumpcap` solo puede ser ejecutado por root y miembros del grupo `wireshark`, por lo tanto, para usar Wireshark como usuario normal, debe agregar su usuario al [grupo del usuario](/index.php/User_group "User group") `wireshark` (consulte [Users and groups (Español)#Administración de grupos](/index.php/Users_and_groups_(Espa%C3%B1ol)#Administración_de_grupos "Users and groups (Español)")).

## Algunas técnicas de captura

Hay varias maneras diferentes de capturar exactamente lo que está buscando en Wireshark, aplicando [filtros de captura](https://wiki.wireshark.org/CaptureFilters) o [filtros de visualización](https://wiki.wireshark.org/DisplayFilters).

**Nota:** para conocer la sintaxis del filtro de captura, consulte [pcap-filter(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pcap-filter.7). Para ver los filtros de visualización, consulte [wireshark-filter(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wireshark-filter.4).

### Filtrar paquetes TCP

Si desea ver todos los paquetes TCP actuales, escriba `tcp` en la barra «Filter» o en la CLI, introduzca:

```
$ tshark -f "tcp"

```

### Filtrar paquetes UDP

Si desea ver todos los paquetes TCP actuales, escriba `udp` en la barra «Filter» o en la CLI, introduzca:

```
$ tshark -f "udp"

```

### Filtrar paquetes a una dirección IP específica

*   Si desea ver todo el tráfico que va a una dirección específica, introduzca el filtro de visualización `ip.dst == 1.2.3.4`, reemplazando `1.2.3.4` con la dirección IP a la que se está enviando al tráfico saliente.
*   Si desea ver todo el tráfico entrante para una dirección específica, introduzca el filtro de visualización `ip.src == 1.2.3.4`, reemplazando `1.2.3.4` con la dirección IP a la que se está enviando al tráfico entrante.
*   Si desea ver todo el tráfico entrante y saliente para una dirección específica, introduzca el filtro de visualización `ip.addr == 1.2.3.4`, reemplazando `1.2.3.4` con la dirección IP relevante.

### Excluir paquetes de una dirección IP específica

```
ip.addr != 1.2.3.4

```

### Filtrar paquetes a la LAN

Para ver solo el tráfico LAN, sin el tráfico de Internet, ejecute:

```
ip.src==192.168.0.0/16 and ip.dst==192.168.0.0/16

```

### Filtrar paquetes por puerto

Vea todo el tráfico en dos puertos o más:

```
tcp.port==80||tcp.port==3306
tcp.port==80||tcp.port==3306||tcp.port==443

```