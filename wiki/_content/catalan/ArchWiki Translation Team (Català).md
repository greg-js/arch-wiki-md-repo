Benvingut a la comunitat de traducció al català de la documentació de ArchLinux. Ens podeu trobar al canal #archlinux-ca al servidor irc.freenode.net. Des d'aquí volem fer l'esforç de traducció de les pàgines wiki de ArchLinux.

A mida d'anar traduïnt la documentació en anglés s'anirà revisant si el pot ampliar aquesta.

**Dilluns 3 de Març HACKATON a [F53Hack](https://n-1.cc/g/hackerspace_garrotxa_f53hack) d'olot** Normes del HackaTon:

*   Cada participat pot escollir un total de 4 seccions.
*   S'escull a l'altzar:
    *   Quin ordinador farà servir cadascú.
    *   Qui començarà a escollir secció. Primer un després els altre participant, per a cada 4 seccions.
*   Les traduccions s'han de fer el local i només modificar la wiki en el moment que estigui acabada la traducció de l'article.

Good Hacking guys!!!

Repartim feina (codi a millorar per no repetir seccions)

```
#/bin/bash

# Vint seccions a traduir
# Usuaris 3
p1="jimics"
p2="N0rd"
p3="jsoler"
jugador=0
seccio=0
i=1
# Selecció de usuari 3 a 1.

while [ $i -lt 21 ]; do
	jugador=$((RANDOM%3+1))
	seccio=$((RANDOM%20+1))
	echo "Jugador: $jugador Seccio: $seccio"
	let i=i+1
done

```

<--! * Traducció al Pad de Marsupi: [ArchCat-Marsupi](http://pad.marsupi.org/ArchCat) -->

# Instal·lació

| Secció | Autor | Versió | Revisat i aprovat | Comentaris |
| [0\. Intro](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Installation) | jsoler | v0.1b | Repassar gramàtica i millorar |
| [1\. Download](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Download) | jsoler | v0.01 | Completar |
| [2.1 Keyboard layout](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Keyboard_layout) | v0.0 |
| [2.2 Partition disks](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Partition_disks) | v0.0 |
| [2.3 Format the partitions](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Format_the_partitions) | v0.0 |
| [2.4 Mount_the_partitions](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Mount_the_partitions) | v0.0 |
| [2.5 Connect to the internet](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Connect_to_the_internet) | v0.0 |
| [2.5.1 Wireless](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Wireless) | v0.0 |
| [2.6 Install the base system](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Install_the_base_system) | v0.0 |
| [2.7 Configure the system](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Configure_the_system) | v0.0 |
| [2.8 Install and configure a boot loader](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Install_and_configure_a_boot_loader) | v0.0 |
| [2.9 Unmount and reboot](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Unmount_and_reboot) | v0.0 |
| [3.0 Post-installation](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Post-installation) | v0.0 |
| [3.1 User management](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#User_management) | v0.0 |
| [3.2 Package management](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Package_management) | v0.0 |
| [3.3 Service management](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Service_management) | v0.0 |
| [3.4 Sound](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Sound) | v0.0 |
| [3.5 Display server](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Display_server) | v0.0 |
| [3.6 Fonts](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Fonts) | v0.0 |
| [4.Appendix](https://wiki.archlinux.org/index.php/Installation_Guide_(Catal%C3%A0)#Appendix) | v0.0 |

# Articles solts

| Secció | Autor | Versió | Revisat i aprovat | Comentaris |
| [OpenVPN](https://wiki.archlinux.org/index.php/Openvpn) | v0.0 |
| [Seguretat](https://wiki.archlinux.org/index.php/Security) | v0.0 |