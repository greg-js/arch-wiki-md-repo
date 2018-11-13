Netboot atvaizdai tai ypač maži (<1MB) atvaizdai, kurie gali būti naudojami parsisiųsti naujausio leidimo Arch Linux, sistemos įkrovimo metu. Netboot atvaizdo atnaujinti nebūtina, naujausias leidimas bus prieinamas automatiškai. Netboot atvaizdus galima parsisiųsti iš [Arch Linux tinklalapio](https://www.archlinux.org/releng/netboot/).

## Contents

*   [1 BIOS](#BIOS)
    *   [1.1 ipxe.lkrn naudojimas](#ipxe.lkrn_naudojimas)
    *   [1.2 ipxe.pxe naudojimas](#ipxe.pxe_naudojimas)
*   [2 UEFI](#UEFI)
    *   [2.1 Įdiegimas su efibootmgr](#Įdiegimas_su_efibootmgr)

## BIOS

Norint netboot naudoti ant kompiuterio su BIOS, jums reikės ipxe.lkrn arba ipxe.pxe atvaizdo.

### ipxe.lkrn naudojimas

ipxe.lkrn atvaizdas gali būti užkraunamas kaip Linux branduolys. Bet kuris Linux įkroviklis (kaip Grub ar syslinux) gali būti panaudotas užkrauti jį iš kietojo disko, CD ar USB laikmenos.

Atvaizdą galima išbandyti su qemu naudojantis sekančia komanda:

```
   qemu-system-x86_64 -enable-kvm -m 1G -kernel ipxe.lkrn

```

### ipxe.pxe naudojimas

ipxe.pxe atvaizdas yra PXE atvaizdas. Jis gali būti grandiniškai užkrautas iš egzistuojančios PXE aplinkos. Tai leidžia sukonfigūruoti DHCP serverį taip kad kraunant iš tinklo visados bus užkraunama Arch Linux netboot.

## UEFI

ipxe.efi atvaizdas gali būti naudojamas paleisti Arch Linux netboot UEFI rėžimu. Pailaikoma tik 64 Bit'ų UEFI. ipxe.efi atvaizdas prie įkrovimo pasirinkimų gali būti pridėtas per efibootmgr, grandiniškai užkrautas per systemd-boot ar tiesiogiai paleistas per UEFI apvalkalą.

### Įdiegimas su efibootmgr

Pirmiausiai įdiekite [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) paketą, tada parsisiųskite [UEFI netboot atvaizdą](https://www.archlinux.org/releng/netboot/).

Darant prielaidą, kad jūsų [EFI sistemos particija](/index.php/EFI_system_partition "EFI system partition") (ESP) yra prijungta po `*esp*`, jūs turėtumėte ją perkelti kaip - kartu duodant ir draugišką vardą:

```
# mkdir *esp*/EFI/arch_netboot
# mv ipxe.*.efi *esp*/EFI/arch_netboot/arch_netboot.efi

```

Tuomet galite sukurti įkrovimo įrašą:

```
# efibootmgr --create --disk /dev/sda --part 1 --loader /EFI/arch_netboot/arch_netboot.efi --label "Arch Linux Netboot"

```