**Status de tradução:** Esse artigo é uma tradução de [Device file](/index.php/Device_file "Device file"). Data da última tradução: 2018-09-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Device_file&diff=0&oldid=542013) na versão em inglês.

From [Wikipédia](https://en.wikipedia.org/wiki/pt:Arquivos_de_dispositivo "wikipedia:pt:Arquivos de dispositivo"):

	Em sistemas operacionais, um arquivo de dispositivo, ou arquivo especial, é uma interface para um driver de dispositivo que aparece em um sistema de arquivos como se fosse um arquivo comum.

No Linux, eles estão no diretório `/dev`, de acordo com [Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/pt:Filesystem_Hierarchy_Standard "wikipedia:pt:Filesystem Hierarchy Standard") (padrão para sistema de arquivos hierárquico).

No Arch Linux, os nós de dispositivo são gerenciados pelo [udev](/index.php/Udev "Udev").

## Contents

*   [1 Dispositivos de bloco](#Dispositivos_de_bloco)
    *   [1.1 lsblk](#lsblk)
    *   [1.2 wipefs](#wipefs)
*   [2 Pseudodispositivos](#Pseudodispositivos)
*   [3 Veja também](#Veja_também)

## Dispositivos de bloco

[Dispositivos de bloco](https://en.wikipedia.org/wiki/pt:Arquivo_de_dispositivo#Dispositivos_de_bloco "wikipedia:pt:Arquivo de dispositivo") fornecem acesso por buffer a dispositivos de hardware e permitem a leitura e escrita de qualquer tamanho e alinhamento.

O início do nome do dispositivo especifica o tipo de dispositivo de bloco. A maioria dos dispositivos de armazenamento modernos (por exemplo, discos rígidos, [SSDs](/index.php/SSD "SSD") e unidades flash USB) são reconhecidos como discos [SCSI](https://en.wikipedia.org/wiki/pt:SCSI "wikipedia:pt:SCSI") (`sd`). O tipo é seguido por uma letra minúscula a partir de `a` para o primeiro dispositivo (`sda`), `b` para o segundo dispositivo (`sdb`), e assim por diante. [Partições](/index.php/Partition "Partition") *existentes* em cada dispositivo serão listadas com um número a partir de `1` para a primeira partição (`sda1`), `2` para a segunda (`sda2`) e assim por diante. Outros tipos de dispositivos de bloco comuns incluem, por exemplo, `mmcblk` para cartões de memória e `nvme` para dispositivos [NVMe](/index.php/NVMe "NVMe").

Veja também [Nomenclatura dispositivo bloco persistente](/index.php/Persistent_block_device_naming "Persistent block device naming").

### lsblk

O pacote [util-linux](https://www.archlinux.org/packages/?name=util-linux) fornece o utilitário [lsblk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) para listar dispositivos de blocos, por exemplo:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1 vfat                 C4DA-2C4D                            /boot
├─sda2 swap                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 [SWAP]
└─sda3 ext4                 56adc99b-a61e-46af-aab7-a6d07e504652 /

```

No exemplo acima, apenas um dispositivo está disponível (`sda`), e esse dispositivo tem três partições (`sda1` para `sda3`), cada uma com um diferente [sistema de arquivos](/index.php/File_system "File system").

### wipefs

*wipefs* pode listar ou apagar [sistema de arquivo](/index.php/File_system "File system"), [RAID](/index.php/RAID "RAID") ou [tabela de partição](/index.php/Partition "Partition") assinaturas (strings mágicas) do dispositivo especificado para tornar as assinaturas invisíveis para [libblkid(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libblkid.3). Ele não apaga os sistemas de arquivos nem quaisquer outros dados do dispositivo.

Veja [wipefs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wipefs.8) para mais informação.

Por exemplo, para apagar todas as assinaturas do dispositivo `/dev/sdb` e criar um arquivo de backup de assinatura `~/wipefs-sdb-*offset*.bak` para cada assinatura:

```
# wipefs --all --backup /dev/sdb

```

## Pseudodispositivos

Nós de dispositivos que não têm um dispositivo físico.

*   [/dev/random](/index.php//dev/random "/dev/random"), veja [random(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/random.4)
*   [/dev/shm](/index.php//dev/shm "/dev/shm")
*   [/dev/null](https://en.wikipedia.org/wiki/pt:/dev/null "wikipedia:pt:/dev/null"), [/dev/zero](https://en.wikipedia.org/wiki/pt:/dev/zero "wikipedia:pt:/dev/zero"), veja [null(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/null.4)
*   [/dev/full](https://en.wikipedia.org/wiki/pt:/dev/full "wikipedia:pt:/dev/full"), veja [full(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/full.4)

## Veja também

*   [Linux allocated devices — The Linux Kernel documentation](https://www.kernel.org/doc/html/latest/admin-guide/devices.html)
*   [Gentoo:Device file](https://wiki.gentoo.org/wiki/Device_file "gentoo:Device file")