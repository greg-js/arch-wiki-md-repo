**Status de tradução:** Esse artigo é uma tradução de [Device file](/index.php/Device_file "Device file"). Data da última tradução: 2019-10-12\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Device_file&diff=0&oldid=581847) na versão em inglês.

Artigos relacionados

*   [Nomeação persistente de dispositivo de bloco](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco "Nomeação persistente de dispositivo de bloco")

From [Wikipédia](https://en.wikipedia.org/wiki/pt:Arquivos_de_dispositivo "wikipedia:pt:Arquivos de dispositivo"):

	Em sistemas operacionais, um arquivo de dispositivo, ou arquivo especial, é uma interface para um driver de dispositivo que aparece em um sistema de arquivos como se fosse um arquivo comum.

No Linux, eles estão no diretório `/dev`, de acordo com [Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/pt:Filesystem_Hierarchy_Standard "wikipedia:pt:Filesystem Hierarchy Standard") (padrão para sistema de arquivos hierárquico).

No Arch Linux, os nós de dispositivo são gerenciados pelo [udev](/index.php/Udev "Udev").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Dispositivos de bloco](#Dispositivos_de_bloco)
    *   [1.1 Nomes de dispositivos de bloco](#Nomes_de_dispositivos_de_bloco)
        *   [1.1.1 SCSI](#SCSI)
        *   [1.1.2 NVMe](#NVMe)
        *   [1.1.3 MMC](#MMC)
        *   [1.1.4 Unidade de disco óptico SCSI](#Unidade_de_disco_óptico_SCSI)
    *   [1.2 Utilitários](#Utilitários)
        *   [1.2.1 lsblk](#lsblk)
        *   [1.2.2 wipefs](#wipefs)
*   [2 Pseudodispositivos](#Pseudodispositivos)
*   [3 Veja também](#Veja_também)

## Dispositivos de bloco

[Dispositivos de bloco](https://en.wikipedia.org/wiki/pt:Arquivo_de_dispositivo#Dispositivos_de_bloco "wikipedia:pt:Arquivo de dispositivo") fornecem acesso por buffer a dispositivos de hardware e permitem a leitura e escrita de qualquer tamanho e alinhamento.

### Nomes de dispositivos de bloco

O início do nome do dispositivo especifica o subsistema de driver usado do kernel para operar o dispositivo de bloco.

**Atenção:** Os descritores de nomes do kernel para dispositivos de bloco não são [persistentes](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco "Nomeação persistente de dispositivo de bloco") e podem alterar cada inicialização, eles não devem ser usados em arquivos de configuração.

#### SCSI

Dispositivos de armazenamento, como discos rígidos, [SSDs](/index.php/SSD "SSD") e unidades flash, que possuem suporte a conexões de [comando SCSI](https://en.wikipedia.org/wiki/SCSI_command "wikipedia:SCSI command") ([SCSI](https://en.wikipedia.org/wiki/pt:SCSI "wikipedia:pt:SCSI"), [SAS](https://en.wikipedia.org/wiki/pt:Serial_Attached_SCSI "wikipedia:pt:Serial Attached SCSI"), [UASP](https://en.wikipedia.org/wiki/USB_Attached_SCSI "wikipedia:USB Attached SCSI")), ATA ([PATA](https://en.wikipedia.org/wiki/pt:Parallel_ATA "wikipedia:pt:Parallel ATA"), [SATA](https://en.wikipedia.org/wiki/pt:Serial_ATA "wikipedia:pt:Serial ATA")) ou [armazenamento em unidade USB](https://en.wikipedia.org/wiki/USB_mass_storage_device_class "wikipedia:USB mass storage device class") são tratadas pelo subsistema de driver SCSI do kernel. Todas elas compartilham o mesmo esquema de nome.

O nome desses dispositivos começa com `sd`. Ele é então seguido por uma letra minúscula começando de `a` para o primeiro dispositivo descoberto (`sda`), `b` para o segundo dispositivo descoberto (`sdb`) e assim por diante. As [partições](/index.php/Parti%C3%A7%C3%B5es "Partições") existentes em cada dispositivo serão listadas com o número que lhes é atribuído na tabela de partições, por exemplo, `sda1` para a partição `1`, `sda2` para partição `2` e assim por diante.

Resumo:

*   `/dev/sda` - dispositivo `a`, o primeiro dispositivo descoberto.
*   `/dev/sda1` - partição `1` no dispositivo `a`.
*   `/dev/sde` - dispositivo `e`, o quinto dispositivo descoberto.
*   `/dev/sde7` - partition `7` on device `e`.

#### NVMe

O nome dos dispositivos de armazenamento, como [SSDs](/index.php/SSD "SSD"), que estão conectados via [NVM Express](/index.php/NVM_Express "NVM Express") (NVMe) começa com `nvme`. É então seguido por um número iniciando em `0` para o controlador do dispositivo, `nvme0` para o primeiro controlador NVMe descoberto, `nvme1` para o segundo, e assim por diante. A próxima é a letra "n" e um número iniciando em `1` expressando o dispositivo em um controlador, ou seja, `nvme0n1` para o primeiro dispositivo descoberto no primeiro controlador descoberto, `nvme0n2` para o segundo dispositivo descoberto no primeiro controlador descoberto e assim por diante. As [partições](/index.php/Parti%C3%A7%C3%B5es "Partições") existentes em cada dispositivo serão listadas com a letra "p" e o número que lhes é atribuído na tabela de partições. Por exemplo, `nvme0n1p` para a partição com o número `1` no primeiro dispositivo descoberto no primeiro controlador descoberto, `nvme0n1p2` para a partição `2`, e assim por diante.

Resumo:

*   `/dev/nvme0n1` - dispositivo `1` no controlador `0`, o primeiro dispositivo descoberto no primeiro controlador descoberto.
*   `/dev/nvme0n1p1` - partição `1` no dispositivo `1` no controlador `0`.
*   `/dev/nvme2n5` - dispositivo `5` no controlador `2`, o quinto dispositivo descoberto no terceiro controlador descoberto.
*   `/dev/nvme2n5p7` - partição `7` no dispositivo `5` no controlador `2`.

#### MMC

[Cartões SD](https://en.wikipedia.org/wiki/pt:Cart%C3%A3o_SD "wikipedia:pt:Cartão SD"), [cartões MMC](https://en.wikipedia.org/wiki/pt:MultiMediaCard "wikipedia:pt:MultiMediaCard") e [dispositivos de armazenamento eMMC](https://en.wikipedia.org/wiki/pt:MultiMediaCard#eMMC "wikipedia:pt:MultiMediaCard") são manipulados pelo driver `mmc` do kernel e o nome desses dispositivos começa com `mmcblk`. É então seguido por um número iniciando em `0` para o dispositivo, ou seja, `mmcblk0` para o primeiro dispositivo descoberto, `mmcblk1` para o segundo dispositivo descoberto e assim por diante. As [partições](/index.php/Parti%C3%A7%C3%B5es "Partições") existentes em cada dispositivo serão listadas com a letra "p" e o número que lhes é atribuído na tabela de partições. A partição com o número `1` na tabela de partições seria `mmcblk0p1`, a partição com o número `2` seria `mmcblk0p2`, e assim por diante.

Resumo:

*   `/dev/mmcblk0` - dispositivo `0`, o primeiro dispositivo descoberto.
*   `/dev/mmcblk0p1` - partição `1` no dispositivo `0`.
*   `/dev/mmcblk4` - dispositivo `4`, o quinto dispositivo descoberto.
*   `/dev/mmcblk4p7` - partição `7` no dispositivo `4`.

#### Unidade de disco óptico SCSI

O nome de [unidades de disco óptico](/index.php/Optical_disc_drive "Optical disc drive") (ODDs), que estão conectadas usando uma das interfaces suportadas pelo subsistema de driver [SCSI](#SCSI), começa com `sr`. O nome é então seguido por um número iniciando em `0` para o dispositivo, isto é, `sr0` para o primeiro dispositivo descoberto, `sr1` para o segundo dispositivo descoberto e assim por diante.

[Udev](/index.php/Udev "Udev") também fornece `/dev/cdrom` que é um link simbólico para `/dev/sr0`. O nome sempre será `cdrom` independentemente do tipo de disco suportado ou a mídia inserida.

Resumo:

*   `/dev/sr0` - unidade de disco óptico `0`, a primeira unidade de disco óptico descoberta.
*   `/dev/sr4` - unidade de disco óptico `4`, a quinta unidade de disco óptico descoberta.
*   `/dev/cdrom` - um link simbólico para `/dev/sr0`.

### Utilitários

#### lsblk

O pacote [util-linux](https://www.archlinux.org/packages/?name=util-linux) fornece o utilitário [lsblk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) para listar dispositivos de blocos, por exemplo:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1 vfat                 C4DA-2C4D                            /boot
├─sda2 swap                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 [SWAP]
└─sda3 ext4                 56adc99b-a61e-46af-aab7-a6d07e504652 /

```

No exemplo acima, apenas um dispositivo está disponível (`sda`), e esse dispositivo tem três partições (`sda1` para `sda3`), cada uma com um diferente [sistema de arquivos](/index.php/Sistema_de_arquivos "Sistema de arquivos").

#### wipefs

*wipefs* pode listar ou apagar assinaturas (strings mágicas) de [sistema de arquivos](/index.php/Sistema_de_arquivos "Sistema de arquivos"), [RAID](/index.php/RAID "RAID") ou [tabela de partição](/index.php/Parti%C3%A7%C3%A3o "Partição") do dispositivo especificado para tornar as assinaturas invisíveis para [libblkid(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libblkid.3). Ele não apaga os sistemas de arquivos nem quaisquer outros dados do dispositivo.

Veja [wipefs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wipefs.8) para mais informação.

Por exemplo, para apagar todas as assinaturas do dispositivo `/dev/sdb` e criar um arquivo de assinatura backup `~/wipefs-sdb-*posição*.bak` para cada assinatura:

```
# wipefs --all --backup /dev/sdb

```

## Pseudodispositivos

Nós de dispositivos que não têm um dispositivo físico.

*   [/dev/random](/index.php//dev/random "/dev/random"), veja [random(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/random.4)
*   [/dev/shm](/index.php//dev/shm "/dev/shm")
*   [/dev/null](https://en.wikipedia.org/wiki/pt:/dev/null "wikipedia:pt:/dev/null"), [/dev/zero](https://en.wikipedia.org/wiki/pt:/dev/zero "wikipedia:pt:/dev/zero"), veja [null(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/null.4)
*   [/dev/full](https://en.wikipedia.org/wiki/pt:/dev/full "wikipedia:pt:/dev/full"), veja [full(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/full.4)
*   [/dev/ttyX](/index.php//dev/ttyX_(Portugu%C3%AAs) "/dev/ttyX (Português)"), sendo que X é um número

## Veja também

*   [Linux allocated devices — The Linux Kernel documentation](https://www.kernel.org/doc/html/latest/admin-guide/devices.html)
*   [Gentoo:Device file](https://wiki.gentoo.org/wiki/Device_file "gentoo:Device file")