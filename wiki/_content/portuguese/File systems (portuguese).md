Artigos relacionados

*   [Particionamento](/index.php/Particionamento "Particionamento")
*   [Arquivo de dispositivo#lsblk](/index.php/Arquivo_de_dispositivo#lsblk "Arquivo de dispositivo")
*   [Permissões e atributos de arquivo](/index.php/Permiss%C3%B5es_e_atributos_de_arquivo "Permissões e atributos de arquivo")
*   [fsck](/index.php/Fsck "Fsck")
*   [fstab](/index.php/Fstab "Fstab")
*   [List of applications#Mount tools](/index.php/List_of_applications#Mount_tools "List of applications")
*   [QEMU#Mounting a partition inside a raw disk image](/index.php/QEMU#Mounting_a_partition_inside_a_raw_disk_image "QEMU")
*   [udev](/index.php/Udev "Udev")
*   [udisks](/index.php/Udisks "Udisks")
*   [umask](/index.php/Umask "Umask")
*   [USB storage devices](/index.php/USB_storage_devices "USB storage devices")

Do [Wikipédia](https://en.wikipedia.org/wiki/File_system "wikipedia:File system"):

	Na computação, um sistema de arquivos (em inglês, "file system" or "filesystem") controla como os dados são armazenados e recuperados. Sem um sistema de arquivos, as informações colocadas em uma mídia de armazenamento seriam um grande corpo de dados, sem nenhuma maneira de saber onde uma informação é interrompida e a próxima começa. Ao separar os dados em partes e dar um nome a cada parte, as informações são facilmente isoladas e identificadas. Tomando seu nome da maneira como os sistemas de informação em papel são nomeados, cada grupo de dados é chamado de "arquivo". A estrutura e as regras lógicas usadas para gerenciar os grupos de informações e seus nomes são chamadas de "sistema de arquivos".

Partições de unidades individuais podem ser configuradas usando um dos muitos sistemas de arquivos disponíveis diferentes. Cada um tem suas próprias vantagens, desvantagens e idiossincrasias únicas. Uma breve visão geral dos sistemas de arquivos suportados segue; os links são para páginas da Wikipédia que fornecem muito mais informações.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Tipos de sistemas de arquivos](#Tipos_de_sistemas_de_arquivos)
    *   [1.1 Journaling](#Journaling)
    *   [1.2 Sistema de arquivos baseados em FUSE](#Sistema_de_arquivos_baseados_em_FUSE)
    *   [1.3 Sistemas de arquivos empilháveis](#Sistemas_de_arquivos_empilháveis)
    *   [1.4 Sistema de arquivos somente leitura](#Sistema_de_arquivos_somente_leitura)
    *   [1.5 Sistemas de arquivos em cluster](#Sistemas_de_arquivos_em_cluster)
*   [2 Identificando sistemas de arquivos existentes](#Identificando_sistemas_de_arquivos_existentes)
*   [3 Criar um sistema de arquivos](#Criar_um_sistema_de_arquivos)
*   [4 Montar um sistema de arquivos](#Montar_um_sistema_de_arquivos)
    *   [4.1 Listar sistemas de arquivos montados](#Listar_sistemas_de_arquivos_montados)
    *   [4.2 Desmontar um sistema de arquivos](#Desmontar_um_sistema_de_arquivos)
*   [5 Veja também](#Veja_também)

## Tipos de sistemas de arquivos

Veja [filesystems(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/filesystems.5) para uma visão geral e [Wikipedia:Comparison of file systems](https://en.wikipedia.org/wiki/Comparison_of_file_systems "wikipedia:Comparison of file systems") para uma comparação detalhada das funcionalidades. Sistemas de arquivos suportados pelo kernel estão listados em `/proc/filesystems`.

<caption>Sistemas de arquivos FUSE e inclusos no kernel</caption>
| Sistema de arquivos | Comando de criação | Utilitários do userspace | [Archiso](/index.php/Archiso_(Portugu%C3%AAs) "Archiso (Português)") [[1]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) | Documentação do kernel [[2]](https://www.kernel.org/doc/Documentation/filesystems/) | Notas |
| [Btrfs](/index.php/Btrfs "Btrfs") | [mkfs.btrfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.btrfs.8) | [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) | Sim | [btrfs.txt](https://www.kernel.org/doc/Documentation/filesystems/btrfs.txt) | [status de estabilidade](https://btrfs.wiki.kernel.org/index.php/Status) |
| [VFAT](/index.php/VFAT "VFAT") | [mkfs.fat(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.fat.8) | [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) | Sim | [vfat.txt](https://www.kernel.org/doc/Documentation/filesystems/vfat.txt) |
| [exFAT](https://en.wikipedia.org/wiki/exFAT "wikipedia:exFAT") | [mkexfatfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkexfatfs.8) | [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils) | Sim | N/A (baseado no FUSE) |
| [F2FS](/index.php/F2FS "F2FS") | [mkfs.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.f2fs.8) | [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) | Sim | [f2fs.txt](https://www.kernel.org/doc/Documentation/filesystems/f2fs.txt) | Dispositivos baseados no Flash |
| [ext3](/index.php/Ext3 "Ext3") | [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Sim | [ext3.txt](https://www.kernel.org/doc/Documentation/filesystems/ext3.txt) |
| [ext4](/index.php/Ext4_(Portugu%C3%AAs) "Ext4 (Português)") | [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Sim | [ext4.txt](https://www.kernel.org/doc/Documentation/filesystems/ext4.txt) |
| [HFS](https://en.wikipedia.org/wiki/Hierarchical_File_System "wikipedia:Hierarchical File System") | mkfs.hfsplus(8) | [hfsprogs](https://aur.archlinux.org/packages/hfsprogs/) | Não | [hfs.txt](https://www.kernel.org/doc/Documentation/filesystems/hfs.txt) | sistema de arquivos do [Mac OS Clássico](https://en.wikipedia.org/wiki/pt:Mac_OS_Classic "wikipedia:pt:Mac OS Classic") |
| [HFS+](https://en.wikipedia.org/wiki/HFS_Plus "wikipedia:HFS Plus") | mkfs.hfsplus(8) | [hfsprogs](https://aur.archlinux.org/packages/hfsprogs/) | Não | [hfsplus.txt](https://www.kernel.org/doc/Documentation/filesystems/hfsplus.txt) | sistema de arquivos do [macOS](https://en.wikipedia.org/wiki/pt:macOS "wikipedia:pt:macOS") |
| [JFS](/index.php/JFS "JFS") | [mkfs.jfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.jfs.8) | [jfsutils](https://www.archlinux.org/packages/?name=jfsutils) | Sim | [jfs.txt](https://www.kernel.org/doc/Documentation/filesystems/jfs.txt) |
| [NILFS2](https://en.wikipedia.org/wiki/NILFS "wikipedia:NILFS") | [mkfs.nilfs2(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.nilfs2.8) | [nilfs-utils](https://www.archlinux.org/packages/?name=nilfs-utils) | Sim | [nilfs2.txt](https://www.kernel.org/doc/Documentation/filesystems/nilfs2.txt) |
| [NTFS](/index.php/NTFS "NTFS") | [mkfs.ntfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.ntfs.8) | [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) | Sim | N/A (baseado no FUSE) | sistema de arquivos do [Windows](https://en.wikipedia.org/wiki/Microsoft_Windows "wikipedia:Microsoft Windows") |
| [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "wikipedia:ReiserFS") | [mkfs.reiserfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.reiserfs.8) | [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs) | Sim |
| [UDF](https://en.wikipedia.org/wiki/Universal_Disk_Format "wikipedia:Universal Disk Format") | [mkfs.udf(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.udf.8) | [udftools](https://www.archlinux.org/packages/?name=udftools) | opcional | [udf.txt](https://www.kernel.org/doc/Documentation/filesystems/udf.txt) |
| [XFS](/index.php/XFS "XFS") | [mkfs.xfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.xfs.8) | [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) | Sim | 

[xfs.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs.txt)
[xfs-delayed-logging-design.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs-delayed-logging-design.txt)
[xfs-self-describing-metadata.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs-self-describing-metadata.txt)

 |

**Nota:** O kernel tem sua própria implementação do driver do NTFS (veja [ntfs.txt](https://www.kernel.org/doc/Documentation/filesystems/ntfs.txt)), mas tem suporte limitado a escrever arquivos.

<caption>Sistemas de arquivos não inclusos no kernel</caption>
| Sistema de arquivos | Comando de criação | Conjunto de patches para o kernel | Utilitários do userspace | Notas |
| [APFS](https://en.wikipedia.org/wiki/Apple_File_System "wikipedia:Apple File System") | mkapfs(8) | [linux-apfs-dkms-git](https://aur.archlinux.org/packages/linux-apfs-dkms-git/) | [apfsprogs-git](https://aur.archlinux.org/packages/apfsprogs-git/) | sistema de arquivos do [macOS](https://en.wikipedia.org/wiki/pt:macOS "wikipedia:pt:macOS") (10.13 e posterior). Somente leitura, experimental. |
| [Bcachefs](/index.php/Bcachefs "Bcachefs") | bcachefs(8) | [linux-bcachefs-git](https://aur.archlinux.org/packages/linux-bcachefs-git/) | [bcachefs-tools-git](https://aur.archlinux.org/packages/bcachefs-tools-git/) |
| [Reiser4](/index.php/Reiser4 "Reiser4") | mkfs.reiser4(8) | [linux-ck-reiser4](https://aur.archlinux.org/packages/linux-ck-reiser4/) | [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/) |
| [ZFS](/index.php/ZFS "ZFS") | [zfs-linux](https://aur.archlinux.org/packages/zfs-linux/), [zfs-dkms](https://aur.archlinux.org/packages/zfs-dkms/) | [zfs-utils](https://aur.archlinux.org/packages/zfs-utils/) | porte, [OpenZFS](https://en.wikipedia.org/wiki/OpenZFS "wikipedia:OpenZFS") |

### Journaling

All the above filesystems with the exception of ext2, FAT16/32, Reiser4 (optional), Btrfs and ZFS, use [journaling](https://en.wikipedia.org/wiki/Journaling_file_system "wikipedia:Journaling file system"). Journaling provides fault-resilience by logging changes before they are committed to the filesystem. In the event of a system crash or power failure, such file systems are faster to bring back online and less likely to become corrupted. The logging takes place in a dedicated area of the filesystem.

Not all journaling techniques are the same. Ext3 and ext4 offer data-mode journaling, which logs both data and meta-data, as well as possibility to journal only meta-data changes. Data-mode journaling comes with a speed penalty and is not enabled by default. In the same vein, [Reiser4](/index.php/Reiser4 "Reiser4") offers so-called ["transaction models"](https://reiser4.wiki.kernel.org/index.php/Reiser4_transaction_models) which not only change the features it provides, but in its journaling mode. It uses a different journaling techniques: a special model called [wandering logs](https://reiser4.wiki.kernel.org/index.php/V4#Wandering_Logs) which eliminates the need to write to the disk twice, **write-anywhere**—a pure copy-on-write approach (mostly equivalent to btrfs' default but with a fundamentally different "tree" design) and a combined approach called **hybrid** which heuristically alternates between the two former.

**Note:** Reiser4 does provide an almost equivalent to ext4's default journaling behavior (meta-data only) with the use of the **node41** plugin which also features meta-data and inline checksums, optionally combined with the wandering logs behaviour it provides depending on what transaction model is chosen at mount time.

The other filesystems provide ordered-mode journaling, which only logs meta-data. While all journaling will return a filesystem to a valid state after a crash, data-mode journaling offers the greatest protection against corruption and data loss. There is a compromise in system performance, however, because data-mode journaling does two write operations: first to the journal and then to the disk (which Reiser4 avoids with its "wandering logs" feature. The trade-off between system speed and data safety should be considered when choosing the filesystem type. Reiser4 is the only filesystem that by design operates on full atomicity and also provides checksums for both meta-data and inline data (operations entirely occur, or they entirely do not and does not corrupt or destroy data due to operations half-occurring) and by design is therefor much less prone to data loss than other file systems like [Btrfs](/index.php/Btrfs "Btrfs").

Filesystems based on copy-on-write (also known as write-anywhere), such as Reiser4, Btrfs and ZFS, have no need to use traditional journal to protect metadata, because they are never updated in-place. Although Btrfs still has a journal-like log tree, it is only used to speed-up fdatasync/fsync.

### Sistema de arquivos baseados em FUSE

Veja [FUSE](/index.php/FUSE "FUSE").

### Sistemas de arquivos empilháveis

*   **aufs** — Advanced Multi-layered Unification Filesystem, a FUSE based union filesystem, a complete rewrite of Unionfs, was rejected from Linux mainline and instead OverlayFS was merged into the Linux Kernel.

	[http://aufs.sourceforge.net](http://aufs.sourceforge.net) || [aufs](https://aur.archlinux.org/packages/aufs/)

*   **[eCryptfs](/index.php/ECryptfs "ECryptfs")** — The Enterprise Cryptographic Filesystem is a package of disk encryption software for Linux. It is implemented as a POSIX-compliant filesystem-level encryption layer, aiming to offer functionality similar to that of GnuPG at the operating system level.

	[http://ecryptfs.org](http://ecryptfs.org) || [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils)

*   **mergerfs** — a FUSE based union filesystem.

	[https://github.com/trapexit/mergerfs](https://github.com/trapexit/mergerfs) || [mergerfs](https://aur.archlinux.org/packages/mergerfs/)

*   **mhddfs** — Multi-HDD FUSE filesystem, a FUSE based union filesystem.

	[http://mhddfs.uvw.ru](http://mhddfs.uvw.ru) || [mhddfs](https://aur.archlinux.org/packages/mhddfs/)

*   **[overlayfs](/index.php/Overlayfs "Overlayfs")** — OverlayFS is a filesystem service for Linux which implements a union mount for other file systems.

	[https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt](https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt) || [linux](https://www.archlinux.org/packages/?name=linux)

*   **Unionfs** — Unionfs is a filesystem service for Linux, FreeBSD and NetBSD which implements a union mount for other file systems.

	[http://unionfs.filesystems.org/](http://unionfs.filesystems.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **unionfs-fuse** — A user space Unionfs implementation.

	[https://github.com/rpodgorny/unionfs-fuse](https://github.com/rpodgorny/unionfs-fuse) || [unionfs-fuse](https://www.archlinux.org/packages/?name=unionfs-fuse)

### Sistema de arquivos somente leitura

*   **[SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS")** — SquashFS is a compressed read only filesystem. SquashFS compresses files, inodes and directories, and supports block sizes up to 1 MB for greater compression.

	[http://squashfs.sourceforge.net/](http://squashfs.sourceforge.net/) || [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools)

### Sistemas de arquivos em cluster

*   **[Ceph](/index.php/Ceph "Ceph")** — Unified, distributed storage system designed for excellent performance, reliability and scalability.

	[https://ceph.com/](https://ceph.com/) || [ceph](https://www.archlinux.org/packages/?name=ceph)

*   **[Glusterfs](/index.php/Glusterfs "Glusterfs")** — Cluster file system capable of scaling to several peta-bytes.

	[https://www.gluster.org/](https://www.gluster.org/) || [glusterfs](https://www.archlinux.org/packages/?name=glusterfs)

*   **[IPFS](/index.php/IPFS "IPFS")** — A peer-to-peer hypermedia protocol to make the web faster, safer, and more open. IPFS aims replace HTTP and build a better web for all of us. Uses blocks to store parts of a file, each network node stores only content it is interested, provides deduplication, distribution, scalable system limited only by users. (currently in aplha)

	[https://ipfs.io/](https://ipfs.io/) || [go-ipfs](https://www.archlinux.org/packages/?name=go-ipfs)

*   **[MooseFS](https://en.wikipedia.org/wiki/MooseFS "wikipedia:MooseFS")** — MooseFS is a fault tolerant, highly available and high performance scale-out network distributed file system.

	[https://moosefs.com](https://moosefs.com) || [moosefs](https://www.archlinux.org/packages/?name=moosefs)

*   **[OpenAFS](/index.php/OpenAFS "OpenAFS")** — Open source implementation of the AFS distributed file system

	[http://www.openafs.org](http://www.openafs.org) || [openafs](https://aur.archlinux.org/packages/openafs/)

*   **[OrangeFS](https://en.wikipedia.org/wiki/OrangeFS "wikipedia:OrangeFS")** — OrangeFS is a scale-out network file system designed for transparently accessing multi-server-based disk storage, in parallel. Has optimized MPI-IO support for parallel and distributed applications. Simplifies the use of parallel storage not only for Linux clients, but also for Windows, Hadoop, and WebDAV. POSIX-compatible. Part of Linux kernel since version 4.6.

	[http://www.orangefs.org/](http://www.orangefs.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **Sheepdog** — Distributed object storage system for volume and container services and manages the disks and nodes intelligently.

	[https://sheepdog.github.io/sheepdog/](https://sheepdog.github.io/sheepdog/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Tahoe-LAFS](https://en.wikipedia.org/wiki/Tahoe-LAFS "wikipedia:Tahoe-LAFS")** — Tahoe Least-Authority Filesystem is a free and open, secure, decentralized, fault-tolerant, peer-to-peer distributed data store and distributed file system.

	[https://tahoe-lafs.org/](https://tahoe-lafs.org/) || [tahoe-lafs](https://aur.archlinux.org/packages/tahoe-lafs/)

## Identificando sistemas de arquivos existentes

Para identificar sistemas de arquivos existentes, você pode usar o [lsblk](/index.php/Device_file_(Portugu%C3%AAs)#lsblk "Device file (Português)"):

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL     UUID                                 MOUNTPOINT
sdb
└─sdb1 vfat   Transcend 4A3C-A9E9
```

Um sistema de arquivos existente, se presente, vai ser mostrado na coluna `FSTYPE`. Se [montado](/index.php/Monta "Monta"), vai aparecer na coluna `MOUNTPOINT`.

## Criar um sistema de arquivos

Sistemas de arquivo são normalmente criados em uma [partição](/index.php/Parti%C3%A7%C3%A3o "Partição"), dentro de containers lógicos como [LVM](/index.php/LVM "LVM"), [RAID](/index.php/RAID "RAID") e [dm-crypt](/index.php/Dm-crypt_(Portugu%C3%AAs) "Dm-crypt (Português)"), ou em um arquivo normal (veja [Wikipedia:Loop device](https://en.wikipedia.org/wiki/Loop_device "wikipedia:Loop device")). Esta seção descreve o caso da partição.

**Nota:** Sistemas de arquivos podem ser escritos diretamente para o disco, isto é conhecido como *superfloppy* ou [disco sem partição](/index.php/Particionamento#Disco_sem_partição "Particionamento"). Existem certas limitações neste método, particularmente se [inicializar](/index.php/Processo_de_inicializa%C3%A7%C3%A3o_do_Arch "Processo de inicialização do Arch") por tal unidade de armazenamento. Veja [Btrfs#Partitionless Btrfs disk](/index.php/Btrfs#Partitionless_Btrfs_disk "Btrfs") para um exemplo.

**Atenção:**

*   Depois de criar o novo sistema de arquivos, dados antes presentes nesta partição podem não ser mais recuperados. **faça um backup de quaisquer dados que você deseja manter**.
*   O propósito de dada partição pode restringir a escolha do sistema de arquivos. Por exemplo, uma [partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") deve ter um sistema de arquivos [FAT32](/index.php/FAT32 "FAT32"), e o sistema de arquivo do diretório `/boot` deve ser suportado pelo [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot").

Antes de continuar, [identifique o dispositivo](/index.php/Device_file_(Portugu%C3%AAs)#lsblk "Device file (Português)") onde o sistema de arquivos vai ser criado e se ele está ou não montado. Por exemplo:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1                      C4DA-2C4D
├─sda2 ext4                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 /mnt
└─sda3                      56adc99b-a61e-46af-aab7-a6d07e504652

```

Sistemas de arquivos montados **devem** ser [desmontados](#Desmontar_um_sistema_de_arquivos) antes de proceder. No exemplo acima um sistema de arquivo existente no `/dev/sda2` está montado em `/mnt`. Este deve ser desmontado com:

```
# umount /dev/sda2

```

Para achar somente os sistemas de arquivos montados, veja [#Listar sistemas de arquivos montados](#Listar_sistemas_de_arquivos_montados).

Para criar um novo sistema de arquivos, use o [mkfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.8). Veja [#Tipos de sistemas de arquivos](#Tipos_de_sistemas_de_arquivos) para o exato tipo, e também os utilitários do userspace que você pode instalar para um sistema de arquivos particular.

Por exemplo, para criar um novo sistema de arquivos do tipo [ext4](/index.php/Ext4_(Portugu%C3%AAs) "Ext4 (Português)") (comum para partições de dados no Linux) no `/dev/sda1`, rode:

```
# mkfs.ext4 /dev/sda1

```

**Dica:**

*   Use a opção `-L` do *mkfs.ext4* para especificar um [rotúlo (label) sistema de arquivos](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco#by-label "Nomeação persistente de dispositivo de bloco"). *e2label* pode ser usado para mudar o rotúlo de um sistema de arquivos existente.
*   Sistemas de arquivos podem ser *redimensionados* depois da criação, no entanto, podem existir com certas limitações. Por exemplo, o tamanho do sistema de arquivos [XFS](/index.php/XFS "XFS") pode ser aumentado, mas não reduzido. Veja [Wikipedia:Comparison of file systems#Resize capabilities](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Resize_capabilities "wikipedia:Comparison of file systems") e a documentação do respectivo sistema de arquivos para detalhes.

O novo sistema de arquivos pode ser montado para um diretório de escolha.

## Montar um sistema de arquivos

Para manualmente montar um sistema de arquivos localizado em um dispositivo (exemplo, uma partição) para um diretório, use [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8). Este exemplo monta `/dev/sda1` no `/mnt`.

```
# mount /dev/sda1 /mnt

```

Isto liga o sistema de arquivos em `/dev/sda1` para o diretório `/mnt`, fazendo seu conteúdo visível. Quaisquer dados que existiam no `/mnt` antes desta ação ficam invisíveis até que o dispositivo seja desmontado.

O [fstab](/index.php/Fstab "Fstab") contém informações de como dispositivos devem ser automaticamente montados, se presentes. Veja o artigo do [fstab](/index.php/Fstab "Fstab") para mais informações de como modificar este comportamento.

Se um dispositivo é especificado no `/etc/fstab` e somente o dispositivo ou ponto de montagem é dado na linha de comando, a informação presente no fstab vai ser usada para a montagem. Por exemplo, se o `/etc/fstab` contém uma linha indicando que `/dev/sda1` deveria ser montado para `/mnt`, então o seguinte vai automaticamente montar o dispositivo para este diretório:

```
# mount /dev/sda1

```

Ou

```
# mount /mnt

```

*mount* contém algumas opções, muitas destas dependem do sistema de arquivos especificado. As opções podem ser mudadas, ao:

*   usar opções na linha de comando com *mount*
*   editando o [fstab](/index.php/Fstab "Fstab")
*   criando regras do [udev](/index.php/Udev "Udev")
*   [compilando o kernel você mesmo](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)")
*   ou usando scripts para montagem de um sistema de arquivos específico (localizado em `/usr/bin/mount.*`).

Veja estes artigos relacionados e o artigo do sistema de arquivos de interesse para mais informações.

**Dica:** Sistemas de arquivos também podem ser montados com *systemd-mount* ao invês do *mount*. Se o ponto de montagem não é especificado, o sistema de arquivos vai ser montado automaticamente em `/run/media/system/*identificador_do_dispositivo*/`. Isto permite facilmente montar um sistema de arquivos sem ter de decidir onde montá-lo. Veja [systemd-mount(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-mount.1) para modo de uso e mais detalhes.

### Listar sistemas de arquivos montados

Para listar todos os sistemas de arquivos montados, use [findmnt(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/findmnt.8):

```
$ findmnt

```

*findmnt* recebe uma variedade de argumentos que podem filtrar a saída e mostra informações adicionais. Por exemplo, é possível receber um dispositivo ou ponto de montagem como um argumento para somente mostrar informações sobre ele:

```
$ findmnt /dev/sda1

```

*findmnt* coleta informações do `/etc/fstab`, `/etc/mtab`, e `/proc/self/mounts`.

### Desmontar um sistema de arquivos

Para desmontar um sistema de arquivos, use [umount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/umount.8). O dispositivo que contém o sistema de arquivos (exemplo, `/dev/sda1`) ou o ponto de montagem (exemplo, `/mnt`) deve ser especificado:

```
# umount /dev/sda1

```

ou

```
# umount /mnt

```

## Veja também

*   [filesystems(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/filesystems.5)
*   [systemd-mount(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-mount.1)
*   [Documentation of file systems supported by linux](https://www.kernel.org/doc/Documentation/filesystems/)
*   [Wikipedia:File systems](https://en.wikipedia.org/wiki/File_systems "wikipedia:File systems")
*   [Wikipedia:Mount (Unix)](https://en.wikipedia.org/wiki/Mount_(Unix) "wikipedia:Mount (Unix)")