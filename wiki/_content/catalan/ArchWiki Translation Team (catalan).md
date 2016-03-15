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
| [0\. Intro](/index.php/Installation_Guide_(Catal%C3%A0)#Installation "Installation Guide (Català)") | jsoler | v0.1b | Repassar gramàtica i millorar |
| [1\. Download](/index.php/Installation_Guide_(Catal%C3%A0)#Download "Installation Guide (Català)") | jsoler | v0.01 | Completar |
| [2.1 Keyboard layout](/index.php/Installation_Guide_(Catal%C3%A0)#Keyboard_layout "Installation Guide (Català)") | v0.0 |
| [2.2 Partition disks](/index.php/Installation_Guide_(Catal%C3%A0)#Partition_disks "Installation Guide (Català)") | v0.0 |
| [2.3 Format the partitions](/index.php/Installation_Guide_(Catal%C3%A0)#Format_the_partitions "Installation Guide (Català)") | v0.0 |
| [2.4 Mount_the_partitions](/index.php/Installation_Guide_(Catal%C3%A0)#Mount_the_partitions "Installation Guide (Català)") | v0.0 |
| [2.5 Connect to the internet](/index.php/Installation_Guide_(Catal%C3%A0)#Connect_to_the_internet "Installation Guide (Català)") | v0.0 |
| [2.5.1 Wireless](/index.php/Installation_Guide_(Catal%C3%A0)#Wireless "Installation Guide (Català)") | v0.0 |
| [2.6 Install the base system](/index.php/Installation_Guide_(Catal%C3%A0)#Install_the_base_system "Installation Guide (Català)") | v0.0 |
| [2.7 Configure the system](/index.php/Installation_Guide_(Catal%C3%A0)#Configure_the_system "Installation Guide (Català)") | v0.0 |
| [2.8 Install and configure a boot loader](/index.php/Installation_Guide_(Catal%C3%A0)#Install_and_configure_a_boot_loader "Installation Guide (Català)") | v0.0 |
| [2.9 Unmount and reboot](/index.php/Installation_Guide_(Catal%C3%A0)#Unmount_and_reboot "Installation Guide (Català)") | v0.0 |
| [3.0 Post-installation](/index.php/Installation_Guide_(Catal%C3%A0)#Post-installation "Installation Guide (Català)") | v0.0 |
| [3.1 User management](/index.php/Installation_Guide_(Catal%C3%A0)#User_management "Installation Guide (Català)") | v0.0 |
| [3.2 Package management](/index.php/Installation_Guide_(Catal%C3%A0)#Package_management "Installation Guide (Català)") | v0.0 |
| [3.3 Service management](/index.php/Installation_Guide_(Catal%C3%A0)#Service_management "Installation Guide (Català)") | v0.0 |
| [3.4 Sound](/index.php/Installation_Guide_(Catal%C3%A0)#Sound "Installation Guide (Català)") | v0.0 |
| [3.5 Display server](/index.php/Installation_Guide_(Catal%C3%A0)#Display_server "Installation Guide (Català)") | v0.0 |
| [3.6 Fonts](/index.php/Installation_Guide_(Catal%C3%A0)#Fonts "Installation Guide (Català)") | v0.0 |
| [4.Appendix](/index.php/Installation_Guide_(Catal%C3%A0)#Appendix "Installation Guide (Català)") | v0.0 |

# Articles solts

| Secció | Autor | Versió | Revisat i aprovat | Comentaris |
| [OpenVPN](/index.php/OpenVPN "OpenVPN") | v0.0 |
| [Seguretat](/index.php/Security "Security") | v0.0 |