**Status de tradução:** Esse artigo é uma tradução de [Category:Boot loaders](/index.php/Category:Boot_loaders "Category:Boot loaders"). Data da última tradução: 2018-09-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Category:Boot_loaders&diff=0&oldid=541260) na versão em inglês.

Para inicializar o Arch Linux, você deve instalar um [*boot loader*](https://en.wikipedia.org/wiki/pt:Boot#Sistema_de_inicia.C3.A7.C3.A3o_ou_carregador "w:pt:Boot"), ou sistema de inicialização, com capacidade para Linux no [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") ou [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table"). O boot loader é a primeira peça de software iniciada pela [BIOS](https://en.wikipedia.org/wiki/pt:BIOS "w:pt:BIOS") ou [UEFI](https://en.wikipedia.org/wiki/pt:UEFI "w:pt:UEFI"). É responsável por carregar o kernel com os [parâmetros do kernel](/index.php/Kernel_parameters "Kernel parameters") desejados e [disco de RAM inicial](/index.php/Mkinitcpio "Mkinitcpio") antes de iniciar o [processo de inicialização](/index.php/Boot_process "Boot process"). Veja abaixo os boot loaders disponíveis.

**Nota:** Carregar atualizações de [Microcode](/index.php/Microcode "Microcode") exigem ajustes na configuração do boot loader. [[1]](https://www.archlinux.org/news/changes-to-intel-microcodeupdates/)

## Comparação de recursos

**Nota:**

*   Boot loaders só precisam oferecer suporte ao sistema de arquivos no qual o kernel e o initramfs residem (o sistema de arquivos no qual `/boot` está localizado).
*   Como o GPT é parte da especificação UEFI, todos os boot loaders UEFI oferecem suporte a discos GPT. O GPT nos sistemas BIOS é possível, usando *hybrid booting* com [Hybrid MBR](https://www.rodsbooks.com/gdisk/hybrid.html) ("inicialização híbrida") ou o novo protocolo [somente GPT](http://repo.or.cz/syslinux.git/blob/HEAD:/doc/gpt.txt). Porém, esse protocolo pode causar problemas com certas implementações de BIOS; veja [rodsbooks](http://www.rodsbooks.com/gdisk/bios.html#bios) para mais detalhes.
*   A criptografia mencionada no suporte a sistema de arquivos é uma [criptografia a nível de sistema de arquivos](https://en.wikipedia.org/wiki/Filesystem-level_encryption "wikipedia:Filesystem-level encryption"), não influenciando [criptografia a nível de bloco](/index.php/Dm-crypt "Dm-crypt").

| Nome | Firmware | Multiboot | [Sistema de arquivos](/index.php/File_systems "File systems") | Notas |
| BIOS | [UEFI](/index.php/UEFI "UEFI") | [Btrfs](/index.php/Btrfs "Btrfs") | [ext4](/index.php/Ext4_(Portugu%C3%AAs) "Ext4 (Português)") | ReiserFS v3 | [VFAT](/index.php/VFAT "VFAT") | [XFS](/index.php/XFS "XFS") |
| [EFISTUB](/index.php/EFISTUB "EFISTUB") | – | Sim | – | – | – | – | somente ESP | – | O kernel se tornou em um executável EFI para ser carregado diretamente do firmware [UEFI](/index.php/UEFI "UEFI") ou de outro bootloader. |
| [Clover](/index.php/Clover "Clover") | emula UEFI | Sim | Sim | Não | sem criptografia | Não | Sim | Não | Fork do rEFIt modificado para funcionar em [macOS em hardware que não seja da Apple](https://en.wikipedia.org/wiki/pt:Hackintosh "wikipedia:pt:Hackintosh"). |
| [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") | Sim | Sim | Sim | Sem compressão zstd | Sim | Sim | Sim | Sim | No BIOS/GPT, configuração requer uma [partição de boot BIOS](/index.php/BIOS_boot_partition "BIOS boot partition").
Possui suporte a RAID, LUKS1 e LVM (mas não volumes de provisionamento fino). |
| [rEFInd](/index.php/REFInd "REFInd") | Não | Sim | Sim | sem: criptografia, compressão zstd | sem criptografia | sem recurso de *tail-packing* | Sim | Não | Possui suporte a autodetecção de kernels e parâmetros sem configuração explícita. |
| [Syslinux](/index.php/Syslinux "Syslinux") | Sim | [Parcial](/index.php/Syslinux#Limitations_of_UEFI_Syslinux "Syslinux") | [Parcial](/index.php/Syslinux#Chainloading "Syslinux") | sem: volumes de vários dispositivos, compressão, criptografia | sem criptografia | Não | Sim | v4 somente na [MBR](/index.php/MBR "MBR") | Sem suporte a certos recursos de [sistema de arquivos](/index.php/File_system "File system") [[2]](http://www.syslinux.org/wiki/index.php?title=Filesystem) |
| [systemd-boot](/index.php/Systemd-boot "Systemd-boot") | Não | Sim | Sim | Não | Não | Não | somente ESP | Não | Não é possível iniciar binários de outras partições além de [ESP](/index.php/ESP "ESP"). |
| [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") | sem GPT | Não | Sim | Não | Não | Sim | Sim | somente v4 | [Descontinuado](https://www.gnu.org/software/grub/grub-legacy.html) em favor do [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)"). |
| [LILO](/index.php/LILO "LILO") | sem GPT | Não | Sim | Não | sem criptografia | Sim | Sim | Somente MBR [[3]](http://xfs.org/index.php/XFS_FAQ#Q:_Does_LILO_work_with_XFS.3F) | [Descontinuado](http://web.archive.org/web/20180323163248/http://lilo.alioth.debian.org/) em razão de limitações (p.ex., com Btrfs, GPT, RAID). |

## Veja também

*   [Rod Smith - Gerenciando Boot Loaders EFI para Linux](http://www.rodsbooks.com/efi-bootloaders/)
*   [Wikipedia:Comparison of boot loaders](https://en.wikipedia.org/wiki/Comparison_of_boot_loaders "wikipedia:Comparison of boot loaders")