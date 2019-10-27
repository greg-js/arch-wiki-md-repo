**Status de tradução:** Esse artigo é uma tradução de [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"). Data da última tradução: 2019-10-21\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Persistent_block_device_naming&diff=0&oldid=586896) na versão em inglês.

Artigos relacionados

*   [fstab](/index.php/Fstab "Fstab")
*   [udev](/index.php/Udev "Udev")
*   [LVM](/index.php/LVM "LVM")

Este artigo descreve como usar nomes persistentes para seus [dispositivos de bloco](/index.php/Dispositivos_de_bloco "Dispositivos de bloco"). Isso foi possível com a introdução do [udev](/index.php/Udev "Udev") e tem algumas vantagens sobre a nomeação baseada em barramento. Se sua máquina tiver mais de um controlador de disco SATA, SCSI ou IDE, a ordem na qual os nós de dispositivos correspondentes são adicionados é arbitrária. Isso pode resultar em nomes de dispositivos como `/dev/**sda**` e `/dev/**sdb**` alternando em cada inicialização, culminando em uma inicialização não-inicializável sistema, pânico do kernel ou um dispositivo de bloco desaparecendo. A nomeação persistente resolve esses problemas.

**Nota:**

*   A nomeação persistente possui limites que estão fora do escopo neste artigo. Por exemplo, enquanto [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") pode ter suporte a um método, o systemd pode impor seus próprios limites (por exemplo, [FS#42884](https://bugs.archlinux.org/task/42884)) na nomeação de nomes que ele pode processar durante a inicialização.
*   Esse artigo não é relevante para volumes lógicos de [LVM](/index.php/LVM "LVM"), pois os caminhos de dispositivo `/dev/*NomeGrupoVolume*/*NomeVolumeLógico*` são persistentes.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Métodos de nomeação persistente](#Métodos_de_nomeação_persistente)
    *   [1.1 by-label](#by-label)
    *   [1.2 by-uuid](#by-uuid)
    *   [1.3 by-id e by-path](#by-id_e_by-path)
    *   [1.4 by-partlabel](#by-partlabel)
    *   [1.5 by-partuuid](#by-partuuid)
    *   [1.6 Nomes estáticos de dispositivos com udev](#Nomes_estáticos_de_dispositivos_com_udev)
*   [2 Usando nomeação persistente](#Usando_nomeação_persistente)
    *   [2.1 fstab](#fstab)
    *   [2.2 Parâmetros de kernel](#Parâmetros_de_kernel)

## Métodos de nomeação persistente

Há quatro esquemas diferentes para nomeação persistente: [by-label](#by-label), [by-uuid](#by-uuid), [by-id e by-path](#by-id_e_by-path). Para os que usam discos com [Tabela de Partição GUID (GPT)](/index.php/GUID_Partition_Table "GUID Partition Table"), dois esquemas adicionais podem ser usados: [by-partlabel](#by-partlabel) e [by-partuuid](#by-partuuid). Você também pode usar [nomes estáticos de dispositivos com udev](#Nomes_estáticos_de_dispositivos_com_udev).

Os diretórios em `/dev/disk/` são criados e destruídos dinamicamente, dependendo se há dispositivos neles ou não.

**Nota:** Cuidado que [Clonagem de disco](/index.php/Clonagem_de_disco "Clonagem de disco") cria dois discos diferentes com o mesmo nome.

As seções a seguir descrevem quais são os diferentes métodos de nomenclatura persistente e como são usados.

O comando [lsblk](/index.php/Lsblk_(Portugu%C3%AAs) "Lsblk (Português)") pode ser usado para visualizar graficamente os primeiros esquemas persistentes:

 `$ lsblk -f` 
```
NAME        FSTYPE LABEL      UUID                                 MOUNTPOINT
sda                                                       
├─sda1      vfat              CBB6-24F2                            /boot
├─sda2      ext4   Arch Linux 0a3407de-014b-458b-b5c1-848e92a327a3 /
├─sda3      ext4   Data       b411dc99-f0a0-4c87-9e05-184977be8539 /home
└─sda4      swap              f9fe0b69-a280-415d-a03a-a32752370dee [SWAP]
mmcblk0
└─mmcblk0p1 vfat              F4CA-5D75

```

Para aqueles que usam [GPT](/index.php/GPT "GPT"), use o comando `blkid`. Este comando é mais conveniente para scripts, mas mais difícil de ler.

 `# blkid` 
```
/dev/sda1: UUID="CBB6-24F2" TYPE="vfat" PARTLABEL="EFI system partition" PARTUUID="d0d0d110-0a71-4ed6-936a-304969ea36af" 
/dev/sda2: LABEL="Arch Linux" UUID="0a3407de-014b-458b-b5c1-848e92a327a3" TYPE="ext4" PARTLABEL="GNU/Linux" PARTUUID="98a81274-10f7-40db-872a-03df048df366" 
/dev/sda3: LABEL="Data" UUID="b411dc99-f0a0-4c87-9e05-184977be8539" TYPE="ext4" PARTLABEL="Home" PARTUUID="7280201c-fc5d-40f2-a9b2-466611d3d49e" 
/dev/sda4: UUID="f9fe0b69-a280-415d-a03a-a32752370dee" TYPE="swap" PARTLABEL="Swap" PARTUUID="039b6c1c-7553-4455-9537-1befbc9fbc5b"
/dev/mmcblk0: PTUUID="0003e1e5" PTTYPE="dos"
/dev/mmcblk0p1: UUID="F4CA-5D75" TYPE="vfat" PARTUUID="0003e1e5-01"
```

### by-label

Quase todo [tipo de sistema de arquivos](/index.php/File_systems#Types_of_file_systems "File systems") pode ter um rótulo ("label", em inglês). Todos os seus volumes que têm um são listados no diretório `/dev/disk/by-label`.

 `$ ls -l /dev/disk/by-label` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 Data -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 Arch\x20Linux -> ../../sda2

```

A maioria dos sistemas de arquivos possui suporte à configuração do rótulo na criação do sistema de arquivos, consulte a [página man](/index.php/P%C3%A1gina_man "Página man") do utilitário relevante `mkfs.*`. Para alguns sistemas de arquivos, também é possível alterar os rótulos. A seguir, são apresentados alguns métodos para alterar rótulos em sistemas de arquivos comuns:

	swap 

	`swaplabel -L "*novo rótulo*" /dev/*XXX*` usando [util-linux](https://www.archlinux.org/packages/?name=util-linux)

	ext2/3/4 

	`e2label /dev/*XXX* "*novo rótulo*"` usando [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)

	btrfs 

	`btrfs filesystem label /dev/*XXX* "*novo rótulo*"` usando [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)

	reiserfs 

	`reiserfstune -l "*novo rótulo*" /dev/*XXX*` usando [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs)

	jfs 

	`jfs_tune -L "*novo rótulo*" /dev/*XXX*` usando [jfsutils](https://www.archlinux.org/packages/?name=jfsutils)

	xfs 

	`xfs_admin -L "*novo rótulo*" /dev/*XXX*` usando [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs)

	fat/vfat 

	`fatlabel /dev/*XXX* "*novo rótulo*"` usando [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)

	`mlabel -i /dev/*XXX* ::"*novo rótulo*"` usando [mtools](https://www.archlinux.org/packages/?name=mtools)

	exfat 

	`exfatlabel /dev/*XXX* "*novo rótulo*"` usando [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils)

	ntfs 

	`ntfslabel /dev/*XXX* "*novo rótulo*"` usando [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)

	udf 

	`udflabel /dev/*XXX* "*novo rótulo*"` usando [udftools](https://www.archlinux.org/packages/?name=udftools)

	crypto_LUKS (LUKS2 apenas) 

	`cryptsetup config --label="*novo rótulo*" /dev/*XXX*` usando [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup)

O rótulo de um dispositivo pode ser obtido com *lsblk*:

 `$ lsblk -dno LABEL /dev/sda2` 
```
Arch Linux

```

Ou com *blkid*:

 `# blkid -s LABEL -o value /dev/sda2` 
```
Arch Linux

```

**Nota:**

*   O sistema de arquivos não deve ser montado para alterar seu rótulo. Para o sistema de arquivos raiz, isso pode ser feito inicializando a partir de outro volume.
*   Os rótulos devem ser inequívocos para evitar possíveis conflitos.
*   As rótulos podem ter até 16 caracteres.
*   Como o rótulo é uma propriedade do sistema de arquivos, não é adequado para endereçar persistentemente um único dispositivo RAID.
*   Ao usar contêineres criptografados com [dm-crypt](/index.php/Dm-crypt "Dm-crypt"), os rótulos dos sistemas de arquivos dentro dos contêineres não estarão disponíveis enquanto o contêiner estiver bloqueado/criptografado.

### by-uuid

[UUID](https://en.wikipedia.org/wiki/pt:UUID "wikipedia:pt:UUID") é um mecanismo para fornecer a cada [sistema de arquivos](/index.php/Filesystem "Filesystem") um identificador exclusivo. Esses identificadores são gerados pelos utilitários do sistema de arquivos (por exemplo, `mkfs.*`) quando o dispositivo é formatado e projetado para que as colisões sejam improváveis. Todos os sistemas de arquivos GNU/Linux (incluindo cabeçalhos swap e LUKS de dispositivos criptografados não processados) possuem suporte a UUID. Os sistemas de arquivos FAT, exFAT e NTFS não suportam UUID, mas ainda estão listados em `/dev/disk/by-uuid/` com um UID mais curto (identificador exclusivo):

 `$ ls -l /dev/disk/by-uuid/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 0a3407de-014b-458b-b5c1-848e92a327a3 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 b411dc99-f0a0-4c87-9e05-184977be8539 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 CBB6-24F2 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 f9fe0b69-a280-415d-a03a-a32752370dee -> ../../sda4
lrwxrwxrwx 1 root root 10 May 27 23:31 F4CA-5D75 -> ../../mmcblk0p1

```

O UUID de um dispositivo pode ser obtido com *lsblk*:

 `$ lsblk -dno UUID /dev/sda1` 
```
CBB6-24F2

```

Ou com *blkid*:

 `# blkid -s UUID -o value /dev/sda1` 
```
CBB6-24F2

```

A vantagem de usar o método UUID é que é muito menos provável que ocorram colisões de nomes do que com rótulos. Além disso, é gerado automaticamente na criação do sistema de arquivos. Por exemplo, ele permanecerá único, mesmo que o dispositivo esteja conectado a outro sistema (que talvez tenha um dispositivo com a mesma etiqueta).

A desvantagem é que os UUIDs dificultam a leitura e quebram as linhas de código em muitos arquivos de configuração (por exemplo, [fstab](/index.php/Fstab "Fstab") ou [crypttab](/index.php/Crypttab "Crypttab")). Além disso, toda vez que um volume é reformatado, um novo UUID é gerado e os arquivos de configuração precisam ser ajustados manualmente.

**Dica:** Caso sua swap não tenha um UUID atribuído, você precisará redefini-la usando o utilitário [mkswap](/index.php/Swap_(Portugu%C3%AAs)#Partição_swap "Swap (Português)").

### by-id e by-path

`by-id` cria um nome exclusivo, dependendo do número de série do hardware, e `by-path`, dependendo do caminho físico mais curto (de acordo com o sysfs). Ambos contêm strings para indicar a qual subsistema eles pertencem (por exemplo, `pci-` para `by-path` e `ata-` para `by-id` ), para que estejam vinculados ao hardware que controla o dispositivo. Isso implica em diferentes níveis de persistência: o `by-path` já será alterado quando o dispositivo estiver conectado a uma porta diferente do controlador, o `by-id` será alterado quando o dispositivo estiver conectado em uma porta de um controlador de hardware sujeito a outro subsistema. [[1]](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/persistent_naming.html) Portanto, ambos não são adequados para obter nomes persistentes e tolerantes a alterações de hardware.

No entanto, ambos fornecem informações importantes para encontrar um dispositivo específico em uma grande infraestrutura de hardware. Por exemplo, se você não atribuir manualmente rótulos persistentes (`by-label` ou `by-partlabel`) e manter um diretório com uso de porta de hardware, `by-id` e `by-path` podem ser usados para encontrar um dispositivo específico.[[2]](http://linuxshellaccount.blogspot.in/2008/09/how-to-easily-find-wwns-of-qlogic-hba.html) [[3]](http://www.linuxquestions.org/questions/linux-server-73/how-to-find-wwn-for-dev-sdc-917269/)

O `by-id` também cria links [World Wide Name](https://en.wikipedia.org/wiki/World_Wide_Name "wikipedia:World Wide Name") de dispositivos de armazenamento que possuem suporte a ele. Diferente de outros links `by-id`, os WWNs são totalmente persistentes e não serão alterados dependendo do subsistema usado.

 `$ ls -l /dev/disk/by-id/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470 -> ../../sda
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part1 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part2 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part3 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part4 -> ../../sda4
lrwxrwxrwx 1 root root 10 May 27 23:31 mmc-SD32G_0x0040006d -> ../../mmcblk0
lrwxrwxrwx 1 root root 10 May 27 23:31 mmc-SD32G_0x0040006d-part1 -> ../../mmcblk0p1
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f -> ../../sda
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f-part1 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f-part2 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f-part3 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f-part4 -> ../../sda4

```
 `$ ls -l /dev/disk/by-path/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1 -> ../../sda
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1-part1 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1-part2 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1-part3 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1-part4 -> ../../sda4
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:07:00.0-platform-rtsx_pci_sdmmc.0 -> ../../mmcblk0
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:07:00.0-platform-rtsx_pci_sdmmc.0-part1 -> ../../mmcblk0p1

```

### by-partlabel

**Nota:** Este método refere-se apenas a discos com [Tabela de Partição GUID (GPT)](/index.php/GUID_Partition_Table "GUID Partition Table").

Os rótulos de partição GPT podem ser definidos no cabeçalho da [entrada de partição](https://en.wikipedia.org/wiki/pt:Tabela_de_Parti%C3%A7%C3%A3o_GUID#Entradas_de_parti.C3.A7.C3.A3o_.28LBA_2.E2.80.9333.29 "wikipedia:pt:Tabela de Partição GUID") nos discos GPT.

Esse método é muito semelhante aos [rótulos de sistema de arquivos](#by-label), exceto que os rótulos da partição não serão afetados se o sistema de arquivos na partição for alterado.

Todas as partições que possuem rótulos de partição estão listadas no diretório `/dev/disk/by-partlabel`.

 `ls -l /dev/disk/by-partlabel/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 EFI\x20system\x20partition -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 GNU\x2fLinux -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 Home -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 Swap -> ../../sda4

```

O rótulo da partição de um dispositivo pode ser obtido com *lsblk*:

 `$ lsblk -dno PARTLABEL /dev/sda1` 
```
EFI system partition

```

Ou com *blkid*:

 `# blkid -s PARTLABEL -o value /dev/sda1` 
```
EFI system partition

```

**Nota:**

*   Os rótulos das partições GPT também precisam ser diferentes para evitar conflitos. Para alterar o rótulo da sua partição, você pode usar [gdisk](/index.php/Gdisk "Gdisk") ou a versão baseada em ncurses [cgdisk](/index.php/Cgdisk "Cgdisk"). Ambos estão disponíveis no pacote [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk). Veja [Partitioning#Partitioning tools](/index.php/Partitioning#Partitioning_tools "Partitioning").
*   De acordo com a especificação, os rótulos das partições GPT podem ter até 72 caracteres.

### by-partuuid

Da mesma forma que [rótulos de partição GPT](#by-partlabel), os UUIDs da partição GPT são definidos em [entrada de partição](https://en.wikipedia.org/wiki/pt:Tabela_de_Parti%C3%A7%C3%A3o_GUID#Entradas_de_parti.C3.A7.C3.A3o_.28LBA_2.E2.80.9333.29 "wikipedia:pt:Tabela de Partição GUID") nos discos GPT.

O MBR não possui suporte a UUIDs de partição, mas o Linux[[4]](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=d33b98fc82b0908e91fb05ae081acaed7323f9d2) e softwares usando libblkid[[5]](https://git.kernel.org/pub/scm/utils/util-linux/util-linux.git/commit/?id=d67cc2889a0527b26d7bb8c76f2acac46751d673) (por exemplo, udev[[6]](https://github.com/systemd/systemd/pull/3293)) são capazes de gerar pseudo-PARTUUIDs para partições MBR. O formato é `*SSSSSSSS*-*PP*`, sendo `*SSSSSSSS*` uma [assinatura de disco MBR](https://en.wikipedia.org/wiki/Master_boot_record#Disk_identity "wikipedia:Master boot record") de 32 bits preenchida com zeros e `*PP*` é um número de partição preenchido com zeros em formato hexadecimal. Ao contrário do PARTUUID regular de uma partição GPT, o pseudo-PARTUUID do MBR pode mudar se o número da partição for alterado.

O diretório dinâmico é semelhante a outros métodos e, como [UUIDs de sistema de arquivos](#by-uuid), o uso de UUIDs é preferível aos rótulos.

 `ls -l /dev/disk/by-partuuid/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 0003e1e5-01 -> ../../mmcblk0p1
lrwxrwxrwx 1 root root 10 May 27 23:31 039b6c1c-7553-4455-9537-1befbc9fbc5b -> ../../sda4
lrwxrwxrwx 1 root root 10 May 27 23:31 7280201c-fc5d-40f2-a9b2-466611d3d49e -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 98a81274-10f7-40db-872a-03df048df366 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 d0d0d110-0a71-4ed6-936a-304969ea36af -> ../../sda1

```

O UUID da partição de um dispositivo pode ser obtido com *lsblk*:

 `$ lsblk -dno PARTUUID /dev/sda1` 
```
d0d0d110-0a71-4ed6-936a-304969ea36af

```

Ou com *blkid*:

 `# blkid -s PARTUUID -o value /dev/sda1` 
```
d0d0d110-0a71-4ed6-936a-304969ea36af

```

### Nomes estáticos de dispositivos com udev

Veja [udev#Setting static device names](/index.php/Udev#Setting_static_device_names "Udev").

## Usando nomeação persistente

Há vários aplicativos que podem ser configurados usando nomes persistentes. A seguir, alguns exemplos de como configurá-los.

### fstab

Veja o artigo principal: [fstab#Identifying filesystems](/index.php/Fstab#Identifying_filesystems "Fstab").

### Parâmetros de kernel

Para usar nomes persistentes em [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel"), os seguintes pré-requisitos devem ser atendidos. Em uma instalação padrão, seguindo o guia de instalação, os dois pré-requisitos são atendidos:

*   Você esteja usando uma imagem de disco de RAM inicial do [mkinitcpio](/index.php/Mkinitcpio#Configuration "Mkinitcpio")
*   Você tenha um gancho de udev ou systemd habilitado no `/etc/mkinitcpio.conf`

O local do sistema de arquivos raiz é fornecido pelo parâmetro `root` na linha de comando do kernel. A linha de comando do kernel é configurada a partir do [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot"), consulte [Parâmetros do kernel#Configuração](/index.php/Par%C3%A2metros_do_kernel#Configuração "Parâmetros do kernel"). Para alterar para nomeação persistente de dispositivo, altere apenas os parâmetros que especificam dispositivos de bloco, por exemplo `root` e `resume`, deixando outros parâmetros como estão. Há suporte a vários esquemas de nomeação:

Nomeação persistente de dispositivo [usando o rótulo](#by-label) e o formato `LABEL=`; neste exemplo, `Arch Linux` é o LABEL do sistema de arquivos raiz.

```
root="LABEL=Arch Linux"

```

A nomeação persistente de dispositivo [usando o UUID](#by-uuid) e o formato `UUID=`; neste exemplo `0a3407de-014b-458b-b5c1-848e92a327a3`, é o UUID de o sistema de arquivos raiz.

```
root=UUID=0a3407de-014b-458b-b5c1-848e92a327a3

```

Nomeação persistente de dispositivo [usando o ID do disco](#by-id_e_by-path) e o formato do caminho `/dev`; neste exemplo `wwn-0x60015ee0000b237f-part2` é o ID da partição raiz.

```
root=/dev/disk/by-id/wwn-0x60015ee0000b237f-part2

```

A nomeação persistente de dispositivo [usando o UUID da partição GPT](#by-partuuid) e o formato `PARTUUID=`; neste exemplo `98a81274-10f7-40db-872a-03df048df366`, é o PARTUUID da partição raiz.

```
root=PARTUUID=98a81274-10f7-40db-872a-03df048df366

```

Nomeação persistente de dispositivo [usando o rótulo da partição GPT](#by-partlabel) e o formato `PARTLABEL=`; neste exemplo `GNU/Linux` é o PARTLABEL da partição raiz.

```
root="PARTLABEL=GNU/Linux"

```