Artigos relacionados

*   [File systems](/index.php/File_systems "File systems")
*   [Ext3](/index.php/Ext3 "Ext3")

De [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4) (traduzido):

	Ext4 é a evolução do sistema de arquivos mais usado no Linux, o Ext3\. De diversas formas, o Ext4 é uma melhoria mais profunda sobre Ext3 do que o Ext3 foi sobre Ext2\. O Ext3 foi principalmente sobre adicionar *journaling* ao Ext2, mas o Ext4 modifica estruturas de dados importantes do sistema de arquivos como aqueles projetados para armazenar os dados de arquivos. O resultado é um sistema de arquivos com um desenho melhorado, melhor desempenho, confiabilidade e recursos

## Contents

*   [1 Criar um novo sistema de arquivos ext4](#Criar_um_novo_sistema_de_arquivos_ext4)
    *   [1.1 Proporção de bytes por inode](#Propor.C3.A7.C3.A3o_de_bytes_por_inode)
    *   [1.2 Blocos reservados](#Blocos_reservados)
*   [2 Migrando de ext2/ext3 para ext4](#Migrando_de_ext2.2Fext3_para_ext4)
    *   [2.1 Montando partições ext2/ext3 como ext4 sem conversão](#Montando_parti.C3.A7.C3.B5es_ext2.2Fext3_como_ext4_sem_convers.C3.A3o)
        *   [2.1.1 Motivo](#Motivo)
        *   [2.1.2 Procedimento](#Procedimento)
    *   [2.2 Convertendo partições ext2/ext3 para ext4](#Convertendo_parti.C3.A7.C3.B5es_ext2.2Fext3_para_ext4)
        *   [2.2.1 Motivo](#Motivo_2)
        *   [2.2.2 Procedimento](#Procedimento_2)
*   [3 Usando criptografia baseada em arquivos](#Usando_criptografia_baseada_em_arquivos)
*   [4 Melhorando performance](#Melhorando_performance)
    *   [4.1 E4rat](#E4rat)
    *   [4.2 Desabilitando atualização de tempo de acesso](#Desabilitando_atualiza.C3.A7.C3.A3o_de_tempo_de_acesso)
    *   [4.3 Aumentando o intervalo de commit](#Aumentando_o_intervalo_de_commit)
    *   [4.4 Desligando barreiras](#Desligando_barreiras)
    *   [4.5 Desabilitando journaling](#Desabilitando_journaling)
*   [5 Habilitando somas de verificação de metadados](#Habilitando_somas_de_verifica.C3.A7.C3.A3o_de_metadados)
    *   [5.1 Novo sistema de arquivos](#Novo_sistema_de_arquivos)
    *   [5.2 Sistema de arquivos existente](#Sistema_de_arquivos_existente)
    *   [5.3 Impacto na performance](#Impacto_na_performance)
*   [6 Veja também](#Veja_tamb.C3.A9m)

## Criar um novo sistema de arquivos ext4

Para formatar uma partição, faça:

```
# mkfs.ext4 /dev/*partição*

```

**Dica:** Veja [mke2fs(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) para mais opções; edite `/etc/mke2fs.conf` para ver/configurar as opções padrões.

### Proporção de bytes por inode

Traduzido de [mke2fs(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8):

	***mke2fs** cria um inode para todos os* bytes por inode *de espaço no disco. Quanto maior proporção de* bytes por inode*, menos inodes serão criados.*

A criação de um novo arquivo, diretório, link simbólico etc. exige pelo menos um [inode](https://en.wikipedia.org/wiki/pt:N%C3%B3-i "wikipedia:pt:Nó-i") livre. Se a contagem de inodes for pequena demais, nenhum arquivo pode ser criado no sistema de arquivos mesmo se ainda houver espaço restante nele.

Porque não é possível alterar a proporção de bytes por inode ou a contagem de inodes após o sistema de arquivos ser criado, o `mkfs.ext4` usa, por padrão, uma proporção relativamente baixa de um inode a cada 16384 bytes (16 KB) para evitar essa situação.

Porém, para partições com tamanho em centenas ou milhares de GB e tamanho de arquivo médio na faixa de megabytes, isso geralmente resulta em um número muito grande de inodes porque o número de arquivos criados nunca alcança o número de inodes.

Isso resulta em um desperdício de espaço em disco, porque todos arquivos inodes não usados ocupam até 256 bytes no sistema de arquivos (isso também é definido em `/etc/mke2fs.conf`, mas não deve ser alterado). 256 * vários milhões = alguns poucos gigabytes desperdiçados em inodes não usados.

Essa situação pode ser avaliada comparando as figuras `{I}Uso%` fornecidas pelo `df` e `df -i`:

 `$ df -h /home` 
```
Sist. Arq.              Tam.   Usado   Dispo.  **Uso%**  Montado em
/dev/mapper/lvm-home    115G    56G    59G    **49%**    /home
```
 `$ df -hi /home` 
```
Sist. Arq.              Inodes IUsado ILivre **IUso%**   Montado em
/dev/mapper/lvm-home    1.8M    1.1K   1.8M   **1%**     /home
```

Para especificar uma proporção de bytes por inode diferente, você pode usar a opção `-T *tipo-de-uso*` que sugere o uso esperado do sistema de arquivos usando tipos definidos em `/etc/mke2fs.conf`. Além daqueles tipos estão `largefile` e `largefile4` maiores, que oferecem proporções mais relevantes de um inode a cada 1 MB e 4 MB, respectivamente. Pode-se usar da seguinte forma:

```
# mkfs.ext4 -T largefile /dev/*dispositivo*

```

A proporção de bytes por inode também pode ser definida diretamente via a opção `-i`: *p.ex.:* use `-i 2097152` para uma proporção 2 MB e `-i 6291456` para uma proporção 6 MB.

**Dica:** Por outro lado, se você está configurando uma partição dedicada a hospedar milhões de arquivos pequenos, como emails e itens de newsgroups, você pode usar valores menores de *tipo-de-uso* como `news` (um inode para cada 4096 bytes) ou `small` (idem, somado a tamanhos de bloco e inode menores).

**Atenção:** Se você faz uso intenso de links simbólicos, certifique-se de manter a contagem de inodes alta o suficiente com uma proporção baixa de bytes por inode, porque, apesar de não usar muito espaço, todo novo link simbólico consume um novo inode e, portanto, o sistema de arquivos pode esgotá-los rapidamente.

### Blocos reservados

Por padrão, 5% dos blocos de sistema de arquivos serão reservados para o superusuário, para evitar fragmentação e "*permitir daemons do root continuarem a funcionar corretamente após processos sem privilégios serem impedidos de escrever no sistema de arquivos*" (traduzido de [mke2fs(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8)).

Para discos modernos de alta capacidade, isso é mais alto do que necessário se a partição for usada como um arquivo de longo prazo ou não crucial para operações do sistema (como `/home`). Veja [esse e-mail](http://www.redhat.com/archives/ext3-users/2009-January/msg00026.html) para a opinião do desenvolvedor do ext4 Ted Ts'o sobre blocos reservados.

Geralmente é seguro reduzir a percentagem de blocos reservados para liberar espaço de disco quando a partição é:

*   Grande demais (por exemplo > 50G); ou
*   Usado como arquivo de longo prazo, isto é, onde arquivos não serão excluídos e criados com muita frequência

A opção `-m` de utilitários relacionados ao ext4 permitem especificar a percentagem de blocos reservados.

Para impedir totalmente de reservar blocos na criação do sistema de arquivos, use:

```
# mkfs.ext4 -m 0 /dev/*dispositivo*

```

Para reduzi-lo para 1% posteriormente, use:

```
# tune2fs -m 1 /dev/*dispositivo*

```

Você pode usar [findmnt(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/findmnt.8) para localizar o nome do dispositivo:

```
$ findmnt */o/ponto/de/montagem*

```

## Migrando de ext2/ext3 para ext4

### Montando partições ext2/ext3 como ext4 sem conversão

#### Motivo

Um compromisso entre a conversão total para ext4 e simplesmente permanecer com ext2/ext3 é montar as partições como ext4.

**Vantagens:**

*   Compatibilidade (o sistema de arquivos pode continuar sendo montado como ext3) – Isso permite que os usuários ainda leiam o sistema de arquivos de outros sistemas operacionais sem suporte a ext4 (por exemplo, o Windows com drivers ext2/ext3)
*   Melhor desempenho (embora não tanto como uma partição ext4 totalmente convertida).[[1]](http://kernelnewbies.org/Ext4) [[2]](http://events.linuxfoundation.org/slides/2010/linuxcon_japan/linuxcon_jp2010_fujita.pdf)

**Desvantagens:**

*   Menos recursos do ext4 são usados (apenas aqueles que não alteram o formato do disco, como a alocação de múltiplos blocos e a alocação atrasada)

**Nota:** Exceto pela novidade relativa do ext4 (que pode ser visto como um risco), **não há nenhuma desvantagem importante para esta técnica**.

#### Procedimento

1.  Edite `/etc/fstab` e altere o 'type' de ext2/ext3 para ext4 para quaisquer partições você gostaria de montar como ext4.
2.  Monte novamente as partições afetadas.

### Convertendo partições ext2/ext3 para ext4

#### Motivo

Para experimentar os benefícios do ext4, um processo de conversão irreversível deve ser concluído.

**Vantagens:**

*   Desempenho melhorado e novos recursos.[[3]](http://kernelnewbies.org/Ext4) [[4]](http://events.linuxfoundation.org/slides/2010/linuxcon_japan/linuxcon_jp2010_fujita.pdf)

**Desvantagens:**

*   As partições que contêm principalmente arquivos estáticos, como uma partição `/boot`, podem não se beneficiar dos novos recursos. Além disso, adicionar um diário (que está implícito ao mover uma partição ext2 para ext3/4) sempre incorre em despesas gerais de desempenho.
*   Irreversível (as partições ext4 não podem ser "rebaixadas" para ext2/ext3\. No entanto, é compatível com versões anteriores até que a extensão e outras opções exclusivas estejam habilitadas)

#### Procedimento

These instructions were adapted from [Kernel documentation](http://ext4.wiki.kernel.org/index.php/Ext4_Howto) and an [BBS thread](https://bbs.archlinux.org/viewtopic.php?id=61602).

**Warning:**

*   If you convert the system's root filesystem, ensure that the 'fallback' initramfs is available at reboot. Alternatively, add `ext4` according to [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") and re-create the 'default' initial ramdisk with `mkinitcpio -p linux` before starting.
*   If you decide to convert a separate `/boot` partition, ensure the [bootloader](/index.php/Bootloader "Bootloader") supports booting from ext4.

In the following steps `/dev/sdxX` denotes the path to the partition to be converted, such as `/dev/sda1`.

1.  **[BACK-UP!](/index.php/Backup_programs "Backup programs")** Back-up all data on any ext3 partitions that are to be converted to ext4\. A useful package, especially for root partitions, is [Clonezilla](http://clonezilla.org).
2.  Edit `/etc/fstab` and change the 'type' from ext3 to ext4 for any partitions that are to be converted to ext4.
3.  Boot the live medium (if necessary). The conversion process with [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) must be done when the drive is not mounted. If converting a root partition, the simplest way to achieve this is to boot from some other live medium.
4.  Ensure the partition is **NOT** mounted
5.  If you want to convert a ext2 partition, the first conversion step is to add a [journal](/index.php/File_systems#Journaling "File systems") by running `tune2fs -j /dev/sdxX` as root; making it a ext3 partition.
6.  Run `tune2fs -O extent,uninit_bg,dir_index /dev/sdxX` as root. This command converts the ext3 filesystem to ext4 (irreversibly).
7.  Run `fsck -f /dev/sdxX` as root.
    *   The user **must *fsck*** the filesystem, or it **will be unreadable**! This *fsck* run is needed to return the filesystem to a consistent state. It **will** find checksum errors in the group descriptors - this **is** expected. The `-f` option asks *fsck* to force checking even if the file system seems clean. The `-p` option may be used on top to 'automatically repair' (otherwise, the user will be asked for input for each error).
8.  Recommended: mount the partition and run `e4defrag -c -v /dev/sdxX` as root.
    *   Even though the filesystem is now converted to ext4, all files that have been written before the conversion do not yet take advantage of the extent option of ext4, which will improve large file performance and reduce fragmentation and filesystem check time. In order to fully take advantage of ext4, all files would have to be rewritten on disk. Use *e4defrag* to take care of this problem.
9.  Reboot Arch Linux!

## Usando criptografia baseada em arquivos

**Note:** Ext4 forbids encrypting the root (`/`) directory and will produce an error on [kernel](/index.php/Kernel "Kernel") 4.13 and later [[5]](https://patchwork.kernel.org/patch/9787619/) [[6]](https://www.phoronix.com/scan.php?page=news_item&px=EXT4-Linux-4.13-Work).

ext4 supports file-based encryption. In a directory tree marked for encryption, file contents, filenames, and symbolic link targets are all encrypted. Encryption keys are stored in the kernel keyring. See also [Quarkslab's blog](http://blog.quarkslab.com/a-glimpse-of-ext4-filesystem-level-encryption.html) entry with a write-up of the feature, an overview of the implementation state, and practical test results with kernel 4.1.

The encryption relies on the kernel option `CONFIG_EXT4_ENCRYPTION`, which is enabled by default, as well as the *e4crypt* command from the [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) package.

A precondition is that your filesystem is using a supported block size for encryption:

 `# tune2fs -l /dev/*device* | grep 'Block size'` 
```
Block size:               4096

```
 `# getconf PAGE_SIZE` 
```
4096

```

If these values are not the same, then your filesystem will not support encryption, so **do not proceed further**.

**Warning:**

*   Once the encryption feature flag is enabled, kernels older than 4.1 will be unable to mount the filesystem.
*   If the `/boot/` directory is on the ext4 file system, check that the boot loader supports the ext4 encryption.

Next, enable the encryption feature flag on your filesystem:

```
# tune2fs -O encrypt /dev/*device*

```

**Tip:** The operation can be reverted with `debugfs -w -R "feature -encrypt" /dev/*device*`. Run [fsck](/index.php/Fsck "Fsck") before and after to ensure the integrity of the file system.

Next, make a directory to encrypt:

```
# mkdir */encrypted*

```

Note that encryption can only be applied to an empty directory. New files and subdirectories within an encrypted directory inherit its encryption policy. Encrypting already existing files is not yet supported.

Now generate and add a new key to your keyring. This step must be repeated every time you flush your keyring (i.e., reboot):

```
# e4crypt add_key
Enter passphrase (echo disabled): 
Added key with descriptor [f88747555a6115f5]

```

**Warning:** If you forget your passphrase, there will be no way to decrypt your files. It also is not yet possible to change a passphrase after it has been set.

**Note:** To help prevent [dictionary attacks](https://en.wikipedia.org/wiki/Dictionary_attack is automatically generated and stored in the ext4 filesystem superblock. Both the passphrase *and* the salt are used to derive the actual encryption key. As a consequence of this, if you have multiple ext4 filesystems with encryption enabled mounted, then `e4crypt add_key` will actually add multiple keys, one per filesystem. Although any key can be used on any filesystem, it would be wise to only use, on a given filesystem, keys using that filesystem's salt. Otherwise, you risk being unable to decrypt files on filesystem A if filesystem B is unmounted. Alternatively, you can use the `-S` option to `e4crypt add_key` to specify a salt yourself.

Now you know the descriptor for your key. Make sure the key is in your session keyring:

```
# keyctl show
Session Keyring
1021618178 --alswrv   1000  1000  keyring: _ses
 176349519 --alsw-v   1000  1000   \_ logon: ext4:f88747555a6115f5

```

Almost done. Now set an encryption policy on the directory (assign the key to it):

```
# e4crypt set_policy f88747555a6115f5 */encrypted*

```

This completes setting up encryption for a directory named `*/encrypted*`. If you try accessing the directory without adding the key into your keyring, filenames and their contents will be seen as encrypted gibberish.

**Warning:**

*   Some applications cannot open files in directories encrypted using this method. Try moving the file outside of the encrypted directory before assuming it is broken. In this case, you will often see a message about a missing key.
*   Logging in does automatically unlock home directories encrypted by this method when using GDM or console login.

**Note:** For security reasons, unencrypted files are not allowed to exist in an encrypted directory. As such, attempting to move (`mv`) unencrypted files into an encrypted directory will

*   fail, if both directories are on the same filesystem mount point. This happens because *mv* will only update the directory index to point to the new directory, but not the file's data inodes (which contain the crypto reference).
*   succeed, if both directories are on different filesystem mount points (new data inodes are created).

In both cases it is better to copy (`cp`) files instead, because that leaves the option to securely delete the unencrypted original with *shred* or a similar tool.

## Melhorando performance

### E4rat

[E4rat](/index.php/E4rat "E4rat") is a preload application designed for the ext4 filesystem. It monitors files opened during boot, optimizes their placement on the partition to improve access time, and preloads them at the very beginning of the boot process. "E4rat" does not offer improvements with [SSDs](/index.php/SSD "SSD"), whose access time is negligible compared to hard disks.

### Desabilitando atualização de tempo de acesso

The *ext4* file system records information about when a file was last accessed and there is a cost associated with recording it. With the `noatime` option, the access timestamps on the filesystem are not updated.

 `/etc/fstab`  `/dev/sda5    /    ext4    defaults,**noatime**    0    1` 

### Aumentando o intervalo de commit

The sync interval for data and metadata can be increased by providing a higher time delay to the `commit` option.

The default 5 sec means that if the power is lost, one will lose as much as the latest 5 seconds of work.

It forces a full sync of all data/journal to physical media every 5 seconds. The filesystem will not be damaged though, thanks to the journaling. The following fstab illustrates the use of `commit`:

 `/etc/fstab`  `/dev/sda5    /    ext4   defaults,noatime,**commit=999**    0    1` 

### Desligando barreiras

**Warning:** Disabling barriers for disks without battery-backed cache is not recommended and can lead to severe file system corruption and data loss.

*Ext4* enables write barriers by default. It ensures that file system metadata is correctly written and ordered on disk, even when write caches lose power. This goes with a performance cost especially for applications that use *fsync* heavily or create and delete many small files. For disks that have a write cache that is battery-backed in one way or another, disabling barriers may safely improve performance.

To turn barriers off, add the option `barrier=0` to the desired filesystem. For example:

 `/etc/fstab`  `/dev/sda5    /    ext4    noatime,**barrier=0**   0    1` 

### Desabilitando journaling

**Warning:** Using a filesystem without journaling can result in data loss in case of sudden dismount like power failure or kernel lockup.

Disabling the journal with *ext4* can be done with the following command on an unmounted disk:

1.  tune2fs -O ^has_journal /dev/sdXN

## Habilitando somas de verificação de metadados

In both cases of enabling metadata checksums for new and existing filesystems, you will need to load some kernel modules.

If your CPU supports SSE 4.2, make sure the `crc32c_intel` kernel module is loaded in order to enable the hardware accelerated CRC32C algorithm. If not you will need to load the `crc32c_generic` module.

After this, you are ready to enable support for metadata checksums as described in the following two sections. In both cases the file system must not be mounted.

More about metadata checksums can be read on the [ext4 wiki](https://ext4.wiki.kernel.org/index.php/Ext4_Metadata_Checksums).

### Novo sistema de arquivos

To enable support for ext4 metadata checksums on a new file system make sure that you have `e2fsprogs 1.43` or newer and run:

```
# mkfs.ext4 -O metadata_csum */dev/path/to/disk*

```

The `64bit` option is enabled by default.

The file-system can then be mounted as usual.

### Sistema de arquivos existente

To enable support on an existing ext4 file system do the following.

This needs to be done with the partition unmounted, so if you want to convert the root, you'll need to run off an USB live distro.

First the partition needs to be checked and optimized using:

```
# e2fsck -Df */dev/path/to/disk*  

```

Then the file-system needs to be converted to 64bit:

```
# resize2fs -b */dev/path/to/disk* 

```

Finally checksums can be added

```
# tune2fs -O metadata_csum */dev/path/to/disk*

```

The file-system can then be mounted as usual.

You can check whether the features were successfully enabled by running:

```
# dumpe2fs -h */dev/path/to/disk*

```

### Impacto na performance

Keep in mind that the intel module consistently performs 10x faster than the generic one, peaking at 20x faster as can be seen in [this benchmark](https://ext4.wiki.kernel.org/index.php/Ext4_Metadata_Checksums#Benchmarking).

## Veja também

*   [Official Ext4 wiki](https://ext4.wiki.kernel.org/)
*   [Ext4 Disk Layout](https://ext4.wiki.kernel.org/index.php/Ext4_Disk_Layout) described in its wiki
*   [Ext4 Encryption](http://lwn.net/Articles/639427/) LWN article
*   Kernel commits for ext4 encryption [[7]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=6162e4b0bedeb3dac2ba0a5e1b1f56db107d97ec) [[8]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=8663da2c0919896788321cd8a0016af08588c656)
*   [e2fsprogs Changelog](http://e2fsprogs.sourceforge.net/e2fsprogs-release.html)
*   [Ext4 Metadata Checksums](https://ext4.wiki.kernel.org/index.php/Ext4_Metadata_Checksums)