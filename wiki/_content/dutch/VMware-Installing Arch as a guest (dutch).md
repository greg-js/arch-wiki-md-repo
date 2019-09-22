Related articles

*   [VMware](/index.php/VMware "VMware")
*   [Installing_VMWare_vCLI_(Nederlands)](/index.php/Installing_VMWare_vCLI_(Nederlands) "Installing VMWare vCLI (Nederlands)")

Dit artikel behandelt de installatie van Arch Linux in virtuele machine binnen een VMware omgeving zoals bijvoorbeeld VMware ESX, VMware Workstation/Fusion en VMware Player.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 VMware Tools versus Open-VM-Tools](#VMware_Tools_versus_Open-VM-Tools)
*   [2 Open-VM-Tools modules](#Open-VM-Tools_modules)
*   [3 Open-VM-Tools utilities](#Open-VM-Tools_utilities)
*   [4 Installatie Open-VM-Tools](#Installatie_Open-VM-Tools)
*   [5 Tijdsynchronisatie](#Tijdsynchronisatie)
*   [6 Xorg configuratie](#Xorg_configuratie)
*   [7 Paravirtual SCSI-Adapter](#Paravirtual_SCSI-Adapter)
*   [8 VMCI](#VMCI)
*   [9 DRAG AND DROP](#DRAG_AND_DROP)
*   [10 Shared Folders met de Host](#Shared_Folders_met_de_Host)
    *   [10.1 Prune mlocate DB](#Prune_mlocate_DB)

## VMware Tools versus Open-VM-Tools

De VMware Tools voor Linux zijn er in 2 verschillende vormen: de [officiele VMware Tools](http://packages.vmware.com/tools) en de Open-VM-Tools. Waarbij de VMware Tools zijn gebaseerd op een stable snapshot van de Open-VM-Tools. De Open-VM-Tools bevatten meer dan ook meer experimentele code en features. De officiele VMware Tools zijn niet beschikbaar voor Arch Linux.

Oorspronkelijk leverden de VMware Tools betere drivers voor netwerk en storage, aangevuld met functionaliteit voor o.a. tijd-synchronisatie. Echter sinds geruime tijd zijn de drivers voor de netwerk-adapter en de scsi-adapter standaard onderdeel van de Linux kernel, en zijn de tools alleen benodig voor de extra features en voor de “oude” vmxnet netwerkkaart.

## Open-VM-Tools modules

De open-vm-tools-modules package bevat de volgende modules:

*   vmblock: kernel filesystem module, maakt het mogelijk om in VMware Workstation/Fusion drag&drop van bestanden te doen tussen het host-systeem en de virtuele machine.
*   vmhgfs: kernel filesystem module, maakt het mogelijk om in VMware Workstation/Fusion directories te delen tussen het het host-systeem en de virtuele machine.
*   vmsync: experimentele filesystem sync driver, maakt het mogelijk om filesystem quiescing te doen bij het maken van backups en snapshots
*   vmci: virtual machine communication interface, high performance interface tussen virtuele machines op dezelfde host en tussen virtuele machines en de host.
*   vsocket: onderdeel van vmci
*   vmxnet: driver voor oude vmxnet netwerk-adapter

## Open-VM-Tools utilities

Bij de open-vm-tools worden de volgende utilities meegeleverd:

*   vmtoolsd: service verantwoordelijk voor virtual machine status report
*   vmware-check-vm: tool om te controleren of een utility op een fysieke of virtuele machine gestart is
*   vmware-xferlogs: Dump logging/debugging informatie naar de virtual machine logfile
*   vmware-toolbox-cmd: tool om virtuele machine informatie te krijgen van de host zoals bijv. statistieken.

## Installatie Open-VM-Tools

Installeer de `open-vm-tools` package van de [community repository](/index.php/Community_repository "Community repository"):

```
pacman -S open-vm-tools

```

en start deze met:

```
rc.d start open-vm-tools

```

Om de tools te starten tijdens het boot proces van Arch Linux, voeg deze dan toe aan de [DAEMONS](/index.php/DAEMONS "DAEMONS") area in het [rc.conf](/index.php/Rc.conf "Rc.conf") bestand.

```
DAEMONS = ( ... open-vm-tools ... )

```

De open-vm-tools lezen het bestand /etc/arch-release uit, die normaliter leeg is.

```
cat /proc/version > /etc/arch-release

```

## Tijdsynchronisatie

Tijdsynchronisatie configuratie is in een virtuele machine belangrijk: er kunnen sneller afwijkingen/ontwijkingen ontstaan in een virtuele machine dan in een fysieke machine. Dit komt in belangrijke mate doordat dat de cpu gedeeld wordt door meer dan 1 virtuele machine.

Er zijn 2 manieren om tijdsychronisatie te regelen: de host als bron of een externe [NTP](/index.php/NTP "NTP") server als bron.

Wanneer je de host als bron gebruikt (bijvoorbeeld de ESX server) dan kan dit met behulp van het commando:

```
vmware-toolbox-cmd timesync enable

```

## Xorg configuratie

**Note:** Om Xorg te gebruiken in een virtuele machine is minimaal 32MB VGA memory benodigd, en de VMware hardware versie moet > 8 zijn, versie 7 werkt niet meer.

Installeer de volgende benodigdheden:

```
pacman -S xf86-input-vmmouse xf86-video-vmware xf86-video-vesa svga-dri

```

Voeg de vmwgfx module toe aan de MODULES array in [rc.conf](/index.php/Rc.conf "Rc.conf").

```
MODULES = (... vmwgfx ...)

```

Maak het /etc/X11/xorg.conf.d/20-gpudriver.conf

```
Section "Device"
       Identifier "Card0"
       Driver     "vmware"
EndSection

```

Een reboot is hierna vereist.

## Paravirtual SCSI-Adapter

De paravirtual scsi-adapter kan, doordat er minder overhead is, in ESX een behoorlijke performance winst opleveren.

Je kunt deze als volgt gebruiken: open het [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") bestand en voeg in de MODULES array het volgende toe:

```
MODULES = (... vmw_pvscsi ...)

```

En voer dan het volgende commando uit:

```
mkinitcpio -p linux

```

Zet de virtuele machine uit en pas vervolgens het type scsi-adapter aan naar: “VMware Paravirtual”. De bijbehorende waarschuwing kun je veilig negeren.

## VMCI

De [VMCI interface](http://www.vmware.com/support/developer/vmci-sdk) is bij VMware Workstation en Fusion standaard enabled. Bij VMware ESX is de interface restricted, wat betekent dat er alleen communicatie tussen ESX en de virtuele machine mogelijk is, maar niet tussen de virtuele machines. Dit kan gewijzigd worden via de Virtual Machine settings, verkeer tussen de ESX en de Virtuele Machine kan niet gedisabled worden.

## DRAG AND DROP

Drag and Drop from files, from VMware Workstation/Fusion into the Virtual Machines, can be disabled by editing /etc/conf.d/open-vm-tools:

```
VM_DRAG_AND_DROP="no"

```

## Shared Folders met de Host

**Note:** Deze functionaliteit is alleen beschikbaar in VMware Workstation en Fusion

Maak een nieuwe Shared Folder door `VM` -> `Settings...` te selecteren in het VMware Workstation menu. Selecteer vervolgens de `Options` tab en dan `Shared Folder`. Enable de `Always enabled` optie en maak de nieuwe share. Voor Windows XP kun je een share maken met de naam `C` en de Host Path `C:\`.

Voeg vervolgens een regel toe aan het `/etc/fstab` bestand (uid/gid aanpassen indien nodig) voor elke shared folder:

```
.host:/shared_folder /mnt/shared vmhgfs defaults,user,ttl=5,uid=root,gid=root,fmask=0133,dmask=0022 0 0

```

Maak de mount directories en mount de Shared Folders:

```
mkdir /mnt/shared
mount /mnt/shared

```

Alleen tijdelijk mounten kan ook

```
mount -t -v -o rw .host:/shared_folder /mnt/shared

```

### Prune mlocate DB

Waneer je gebruik maakt van mlocate, dan is het nutteloos om de shared directories te laten indexeren in de `locate DB`. Voeg daarom de directories toe aan `PRUNEPATHS` in `/etc/updatedb`.