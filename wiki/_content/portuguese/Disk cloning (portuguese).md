**Status de tradução:** Esse artigo é uma tradução de [Disk cloning](/index.php/Disk_cloning "Disk cloning"). Data da última tradução: 2019-10-13\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Disk_cloning&diff=0&oldid=585150) na versão em inglês.

Artigos relacionados

*   [Programas de sincronização e backup](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")
*   [Manutenção do sistema#Backup](/index.php/Manuten%C3%A7%C3%A3o_do_sistema#Backup "Manutenção do sistema")
*   [Backup do sistema](/index.php/Backup_do_sistema "Backup do sistema")

A clonagem de disco é o processo de criar uma imagem de uma partição ou de um disco rígido inteiro. Isso pode ser útil para copiar a unidade para outros computadores e para fins de [backup](/index.php/Backup_(Portugu%C3%AAs) "Backup (Português)") e [recuperação](/index.php/File_recovery "File recovery").

**Dica:** Ao longo do tempo, [sistemas de arquivos](/index.php/Sistemas_de_arquivos "Sistemas de arquivos") obtém novos recursos e utilitários de [mkfs](/index.php/Mkfs_(Portugu%C3%AAs) "Mkfs (Português)") alteram seus padrões, mas nem todos os novos recursos podem ser habilitados sem reformatação. Então, ao mover dados para uma nova unidade, em vez de clonar os dispositivos de bloco ou sistemas de arquivos, considere criar um novo sistema de arquivos ou apenas copiar os arquivos (e seus atributos, ACLs, atributos estendidos, etc.) com, por exemplo, [rsync](/index.php/Rsync#Full_system_backup "Rsync").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Usando dd](#Usando_dd)
*   [2 Usando ddrescue](#Usando_ddrescue)
*   [3 Clonagem de sistema de arquivos](#Clonagem_de_sistema_de_arquivos)
    *   [3.1 Usando e2image](#Usando_e2image)
*   [4 Softwares de clonagem de disco](#Softwares_de_clonagem_de_disco)
    *   [4.1 Derivados do dd](#Derivados_do_dd)
*   [5 Veja também](#Veja_também)

## Usando dd

Veja [dd (Português)#Clonagem e restauração de disco](/index.php/Dd_(Portugu%C3%AAs)#Clonagem_e_restauração_de_disco "Dd (Português)").

## Usando ddrescue

[ddrescue](https://www.archlinux.org/packages/?name=ddrescue) é uma ferramenta projetada para clonagem e recuperação de dados. Ele copia dados de um arquivo ou dispositivo de bloco (disco rígido, cdrom, etc) para outro, tentando resgatar as partes boas primeiro em caso de erros de leitura, para maximizar os dados recuperados.

Para clonar uma unidade defeituosa ou prestes a morrer, execute *ddrescue* duas vezes. Primeiro round, copie todos os blocos sem erro de leitura e registre os erros em `rescue.log`.

```
# ddrescue -f -n /dev/sd*X* /dev/sd*Y* rescue.log

```

sendo `*X*` e `*Y*` as letras das partições desejadas dos [dispositivos de bloco](/index.php/Dispositivos_de_bloco "Dispositivos de bloco").

Segunda rodada, copie apenas os blocos ruins e tente 3 vezes para ler a fonte antes de desistir.

```
# ddrescue -d -f -r3 /dev/sd*X* /dev/sd*Y* rescue.log

```

Agora você pode verificar o sistema de arquivos por corrupção e montar a nova unidade.

```
# fsck -f /dev/sd*Y*

```

## Clonagem de sistema de arquivos

### Usando e2image

*e2image* é uma ferramenta incluída em [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) para fins de depuração. Ele pode ser usado para copiar partições ext2, ext3 e ext4 eficientemente apenas copiando os blocos usados. Observe que isso funciona apenas para sistemas de arquivos ext2, ext3 e ext4, e os blocos não utilizados não são copiados, portanto, essa pode não ser uma ferramenta útil se você estiver esperando recuperar arquivos excluídos.

Para clonar uma partição do disco físico `/dev/sda`, partição 1, para o disco físico `/dev/sdb`, partição 1 com e2image, execute:

```
# e2image -ra -p /dev/sda1 /dev/sdb1

```

**Dica:** [GParted](/index.php/GParted "GParted") usa *e2image* para copiar de forma eficiente partições ext2/3/4.

## Softwares de clonagem de disco

Estes aplicativos permite criação fácil de backup de sistemas de arquivos inteiros e recuperação em caso de falha, geralmente na forma de um Live CD ou unidade USB. Eles contêm imagens completas do sistema de um ou mais pontos específicos no tempo e são frequentemente usados para registrar boas configurações conhecidas. Veja [Wikipedia:Comparison of disk cloning software](https://en.wikipedia.org/wiki/Comparison_of_disk_cloning_software "wikipedia:Comparison of disk cloning software") para sua comparação.

Veja também [Programas de sincronização e backup](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs") para outros aplicativos que podem fazer snapshots completos do sistema, além de outras funcionalidades.

*   **Arch Backup** — Um script trivial de backup com configuração simples.
    *   Método de compressão configurável.
    *   Vários alvos de backup.

	[https://github.com/p5n/archlinux-stuff/tree/master/arch-backup/](https://github.com/p5n/archlinux-stuff/tree/master/arch-backup/) || [arch-backup](https://aur.archlinux.org/packages/arch-backup/)

*   **[Clonezilla](https://en.wikipedia.org/wiki/pt:Clonezilla "wikipedia:pt:Clonezilla")** — Uma solução de recuperação de desastre, clonagem de disco, criação e aplicação de imagem.
    *   Inicia de live CD, unidade flash USB ou servidor PXE.
    *   Suporte a ext2, ext3, ext4, reiserfs, reiser4, xfs, jfs, btrfs, FAT32, NTFS, HFS+ e outros.
    *   Usa Partclone (padrão), Partimage (opcional), ntfsclone (opcional) ou dd para fazer imagem ou clonar uma partição.
    *   Servidor multicast para restaurar várias máquinas de uma só vez.
    *   Incluído na mídia de instalação do Arch Linux.

	[http://clonezilla.org/](http://clonezilla.org/) || [clonezilla](https://www.archlinux.org/packages/?name=clonezilla)

*   **Deepin Clone** — Ferramenta do Deepin para fazer backup e restaurar. Possui suporte a clonagem, backup e restauração de disco ou partição.

	[https://www.deepin.org/en/original/deepin-clone/](https://www.deepin.org/en/original/deepin-clone/) || [deepin-clone](https://www.archlinux.org/packages/?name=deepin-clone)

*   **FSArchiver** — Uma ferramenta segura e flexível de backup e aplicação de sistema de arquivos
    *   Suporte a atributos básicos de arquivos (permissões, dono, ...).
    *   Suporte a vários sistemas de arquivos por arquivo.
    *   Suporte a atributos estendidos (eles são usados por SELinux).
    *   Suporte a atributos básicos de sistema de arquivos (label, uuid, block-size) para todos os sistemas de arquivos do Linux.
    *   Suporte a [sistema de arquivos NTFS](http://www.fsarchiver.org/Cloning-ntfs) (capacidade de criar clones flexíveis de partições do Windows).
    *   Uso de soma de verificação para tudo que é gravado nos arquivos (cabeçalhos, blocos de dados, arquivos completos).
    *   Capacidade de restaurar um arquivo que está corrompido (ele vai ignorar o arquivo atual).
    *   Compressão em "multi-thread" de lzo, gzip, bzip2, lzma.
    *   Suporte a divisão de arquivos grandes em vários arquivos com um tamanho máximo fixado.
    *   Criptografia do arquivo usando uma senha. Baseada em blowfish de libcrypto de [OpenSSL](/index.php/OpenSSL "OpenSSL").
    *   Suporte a backup de um sistema de arquivos raiz montado (opção `-A`).
    *   Pode ser encontrado no [System Rescue CD](http://www.sysresccd.org/Main_Page).

	[http://www.fsarchiver.org/](http://www.fsarchiver.org/) || [fsarchiver](https://www.archlinux.org/packages/?name=fsarchiver)

*   **[Mondo Rescue](https://en.wikipedia.org/wiki/Mondo_Rescue "wikipedia:Mondo Rescue")** — Uma solução de recuperação de desastres para criar mídia de backup que pode ser usada para reaplicar o sistema danificado.
    *   Backups baseados em imagem, com suporte a Linux/Windows.
    *   A taxa de compressão é ajustável.
    *   Pode fazer backup de sistemas ao vivo (sem ter que desligá-lo).
    *   Pode dividir imagem por vários arquivos.
    *   Suporte a inicialização em um Live CD para realizar uma restauração completa.
    *   Pode fazer backup/restaurar por NFS, de CDs, unidades de fita e outras mídias.
    *   Pode verificar backups.

	[http://www.mondorescue.org/](http://www.mondorescue.org/) || [mondo](https://aur.archlinux.org/packages/mondo/)

*   **[Partclone](/index.php/Partclone "Partclone")** — Uma ferramenta que pode ser usada para fazer backup e restaurar uma partição, considerando somente blocos usados.
    *   Suporte a ext2, ext3, ext4, hfs+, reiserfs, reiser4, btrfs, vmfs3, vmfs5, xfs, jfs, ufs, ntfs, fat(12/16/32), exfat.
    *   Suporte a compressão.
    *   Opcionalmente, uma interface *ncurses* pode ser usada.

	[http://partclone.org/](http://partclone.org/) || [partclone](https://www.archlinux.org/packages/?name=partclone)

*   **[Partimage](https://en.wikipedia.org/wiki/Partimage "wikipedia:Partimage")** — Um utilitário de clonagem de disco por *ncurses* para ambientes Linux/UNIX.
    *   Possui um Live CD.
    *   Possui suporte aos sistemas de arquivos mais populares no Linux, Windows e Mac OS.
    *   Compressão.
    *   Salva em vários CDs ou DVDs ou entre uma rede usando Samba/NFS.
    *   Desenvolvimento cessado em favor do FSArchiver.

	[http://www.partimage.org](http://www.partimage.org) || [partimage](https://www.archlinux.org/packages/?name=partimage)

*   **J7Z** — Uma interface gráfica em java para Linux que tenta simplificar a compressão e o backup de dados. Cria arquivos 7z, BZip2, Zip, GZip, Tar.
    *   Atualiza arquivos existentes rapidamente.
    *   Faz backup de várias pastas para um local de armazenamento.
    *   Cria e extra arquivos protegidos.
    *   Diminui o esforço usando perfis de arquivamento e listas.

	[http://j7z.xavion.name/](http://j7z.xavion.name/) || [j7z](https://aur.archlinux.org/packages/j7z/)

*   **[Redo Backup and Recovery](https://en.wikipedia.org/wiki/Redo_Backup_and_Recovery "wikipedia:Redo Backup and Recovery")** — Um aplicativo de backup e recuperação de desastre que executa de uma imagem de CD inicializável com Linux.
    *   É capaz de backup e recuperação "bare-metal" de partições de disco.
    *   Usa [xPUD](http://www.xpud.org/) e [Partclone](/index.php/Partclone "Partclone") como backend.

	[http://www.redobackup.org/](http://www.redobackup.org/) ||

*   **System Tar & Restore** — Fazer backup e restauração do seu sistema usando tar ou transfira-o com rsync
    *   Interfaces gráfica e de linha de comando (GUI e CLI)
    *   Cria arquivos *.tar.gz*, *.tar.bz2*, *.tar.xz* ou *.tar*
    *   Suporte a criptografia openssl / gpg
    *   Usa rsync para transferir um sistema em execução
    *   Possui suporte a Grub2, Syslinux, EFISTUB/efibootmgr e Systemd/bootctl

	[https://github.com/tritonas00/system-tar-and-restore](https://github.com/tritonas00/system-tar-and-restore) || [system-tar-and-restore](https://aur.archlinux.org/packages/system-tar-and-restore/)

### Derivados do dd

	dcfldd 

	[dcfldd](https://www.archlinux.org/packages/?name=dcfldd) é uma substituição do dd com a capacidade de hashing durante seu uso, ajudando a garantir a integridade. Aceita a maioria dos parâmetros do dd e inclui saída de status. Uma versão estável de *dcfldd* foi [lançado pela última vez em 2006](http://dcfldd.sourceforge.net/).

	ddrescue 

	GNU [ddrescue](https://www.archlinux.org/packages/?name=ddrescue) é uma ferramenta de recuperação de dados capaz de ignorar erros de leitura. *ddrescue* não está relacionado ao dd, exceto que ambos podem ser usados para copiar dados de um dispositivo para outro. A principal diferença é que o *ddrescue* usa um algoritmo sofisticado para copiar dados de unidades defeituosas, causando-lhes o menor dano possível. Consulte o [manual do ddrescue](http://www.gnu.org/software/ddrescue/manual/ddrescue_manual.html) para detalhes.

## Veja também

*   [Wikipedia:List of disk cloning software](https://en.wikipedia.org/wiki/List_of_disk_cloning_software "wikipedia:List of disk cloning software")
*   [Tópico no fórum do Arch Linux](https://bbs.archlinux.org/viewtopic.php?id=4329)