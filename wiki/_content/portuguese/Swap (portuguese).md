Artigos relacionados

*   [fstab](/index.php/Fstab "Fstab")
*   [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate")
*   [Zswap](/index.php/Zswap "Zswap")
*   [Swap on video ram](/index.php/Swap_on_video_ram "Swap on video ram")
*   [ZFS#Swap_volume](/index.php/ZFS#Swap_volume "ZFS")
*   [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption")

Essa página fornece uma introdução a [espaço swap e paginação](https://en.wikipedia.org/wiki/pt:Pagina%C3%A7%C3%A3o_de_mem%C3%B3ria "wikipedia:pt:Paginação de memória") no GNU/Linux. Ele cobre a criação e ativação de partições swap e arquivos swap.

Do [All about Linux swap space](http://www.linux.com/news/software/applications/8208-all-about-linux-swap-space):

	O Linux divide sua RAM física (memória de acesso aleatório) em pedaços de memória chamados páginas. *Swapping*, ou troca, é o processo pelo qual uma página de memória é copiada para o espaço pré-configurado no disco rígido, chamado espaço swap ou espaço de troca ou *swap space*, para liberar essa página de memória. Os tamanhos combinados da memória física e do espaço swap são a quantidade de memória virtual disponível.

Suporte para swap é fornecido pelo kernel Linux e utilitários de espaço de usuário do pacote [util-linux](https://www.archlinux.org/packages/?name=util-linux).

## Contents

*   [1 Espaço swap](#Espa.C3.A7o_swap)
*   [2 Partição swap](#Parti.C3.A7.C3.A3o_swap)
    *   [2.1 Ativação por systemd](#Ativa.C3.A7.C3.A3o_por_systemd)
    *   [2.2 Desabilitando swap](#Desabilitando_swap)
*   [3 Arquivo swap](#Arquivo_swap)
    *   [3.1 Manualmente](#Manualmente)
        *   [3.1.1 Criação de arquivo swap](#Cria.C3.A7.C3.A3o_de_arquivo_swap)
        *   [3.1.2 Remover arquivo swap](#Remover_arquivo_swap)
    *   [3.2 Automatizado](#Automatizado)
        *   [3.2.1 systemd-swap](#systemd-swap)
*   [4 Swap com dispositivo USB](#Swap_com_dispositivo_USB)
*   [5 Criptografia swap](#Criptografia_swap)
*   [6 Desempenho](#Desempenho)
    *   [6.1 Swappiness](#Swappiness)
    *   [6.2 Pressão de cache VFS](#Press.C3.A3o_de_cache_VFS)
    *   [6.3 Prioridade](#Prioridade)
    *   [6.4 Usando zswap ou zram](#Usando_zswap_ou_zram)
    *   [6.5 Distribuição](#Distribui.C3.A7.C3.A3o)

## Espaço swap

O espaço swap pode assumir a forma de uma partição de disco ou de um arquivo. Os usuários podem criar um espaço swap durante a instalação ou em qualquer momento posterior, conforme desejado. O espaço swap pode ser usado para duas finalidades, estender a memória virtual além da memória física instalada (RAM), também conhecido como "ativar swap", e também para suporte de suspensão para disco.

Se for benéfico ativar o swap, depende da quantidade de memória física instalada e da quantidade de memória necessária para executar todos os programas desejados. Se a quantidade de memória física for menor que a quantidade necessária, é benéfico ativar a troca. Isso evita [condições de falta de memória](https://en.wikipedia.org/wiki/Out_of_memory "wikipedia:Out of memory"), onde o mecanismo matador de OOM do kernel do Linux tentará automaticamente liberar memória matando processos. Para aumentar a quantidade de memória virtual para o valor necessário, adicione a diferença necessária como espaço swap. Por exemplo, se os seus programas precisarem de 7,5 GB de memória para serem executados e houver 4 GB de memória física instalada, adicione a diferença de 3,5 GB no espaço swap. Adicione mais espaço swap para atender aos requisitos futuros. É uma questão de preferência pessoal se você preferir que os programas sejam eliminados ao ativar swap. A maior desvantagem de ativar o swap é seu desempenho inferior, consulte a seção [#Desempenho](#Desempenho).

Para verificar o estado do swap, use:

```
$ swapon --show

```

Ou

```
$ free -h

```

*free* também indica se a memória está em falta, o que pode ser remediado habilitando swap ou aumentando swap.

**Nota:** Não há vantagem de desempenho para um arquivo de swap contíguo ou uma partição, ambos são tratados da mesma maneira.

## Partição swap

Uma partição swap pode ser criada com a maioria das [ferramentas de particionamento](/index.php/Partitioning_tools "Partitioning tools") do GNU/Linux. Partições swap são tipicamente designadas como tipo `82`. Mesmo que seja possível usar qualquer tipo de partição como swap, é recomendado usar o tipo `82` na maioria dos casos, já que o [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") detectará e montará automaticamente (veja abaixo).

Para configurar uma partição como área swap do Linux, o comando `mkswap` é usado. Por exemplo:

```
# mkswap /dev/sd*xy*

```

**Atenção:** todos os dados na partição especificada serão perdidos.

Para habilitar o dispositivo para paginação:

```
# swapon /dev/sd*xy*

```

Para habilitar essa partição swap na inicialização, adicione uma entrada ao [fstab](/index.php/Fstab "Fstab"):

```
UUID=<UUID> none swap defaults 0 0

```

sendo que <UUID> é obtido do comando:

```
lsblk -no UUID /dev/sd*xy*

```

**Dica:** UUIDs e LABELs devem ser favorecidos em relação ao uso dos nomes de dispositivos fornecidos pelo kernel, pois a ordem dos dispositivos pode mudar no futuro. Veja: [fstab](/index.php/Fstab "Fstab").

**Nota:**

*   A entrada fstab é opcional se a partição swap estiver localizada em um dispositivo usando o GPT. Veja a próxima subseção.
*   Se estiver usando um SSD com suporte a [TRIM](/index.php/TRIM "TRIM"), considere usar `defaults,discard` na linha de swap no [fstab](/index.php/Fstab "Fstab"). Se estiver ativando o swap manualmente com *swapon*, o parâmetro `-d`/`--discard` atinge o mesmo objetivo. Veja [swapon(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/swapon.8) para detalhes.

**Atenção:** Habilitar descarte em configurações de RAID usando mdadm vai causar um travamento do sistema na inicialização e durante o tempo de execução, se estiver usando swapon.

### Ativação por systemd

O [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") ativa partições swap com base em dois mecanismos diferentes. Ambos são executáveis em `/usr/lib/systemd/system-generators`. Os geradores são executados na inicialização e criam unidades systemd nativas para montagens. O primeiro, `systemd-fstab-generator`, lê o fstab para gerar unidades, incluindo uma unidade para swap. O segundo, `systemd-gpt-auto-generator` inspeciona o disco raiz para gerar unidades. Ele opera somente nos discos GPT e pode identificar as partições swap pelo tipo GUID, consulte [systemd (Português)#Automontagem de partição GPT](/index.php/Systemd_(Portugu%C3%AAs)#Automontagem_de_parti.C3.A7.C3.A3o_GPT "Systemd (Português)") para obter mais informações.

### Desabilitando swap

Para desabilitar um espaço swap específico:

```
# swapoff /dev/sd*xy*

```

Alternativamente, use a opção `-a` para desabilitar todos os espaços swap.

Como o swap é gerenciado pelo systemd, ele será ativado novamente na próxima inicialização do sistema. Para desabilitar a ativação automática do espaço de swap detectado permanentemente, execute `systemctl --type swap` para encontrar a unit responsável *.swap* e aplique [mask](/index.php/Mask_(Portugu%C3%AAs) "Mask (Português)").

## Arquivo swap

Como uma alternativa para criar uma partição inteira, um arquivo swap oferece a capacidade de variar seu tamanho em execução, e é mais facilmente removido completamente. Isto pode ser especialmente desejável se o espaço em disco for precioso (por exemplo, um SSD de tamanho modesto).

**Atenção:** [Btrfs](/index.php/Btrfs "Btrfs") não tem suporte a arquivos swap. Não seguir este aviso pode resultar em corrupção do sistema de arquivos. Enquanto um arquivo swap pode ser usado no Btrfs quando montado através de um dispositivo de loop, isso resultará em desempenho swap severamente degradado.

### Manualmente

#### Criação de arquivo swap

Como root, use `fallocate` para criar um arquivo swap com o tamanho de sua escolha (M = [Mebibytes](https://en.wikipedia.org/wiki/pt:Mebibyte "wikipedia:pt:Mebibyte"), G = [Gibibytes](https://en.wikipedia.org/wiki/pt:Gibibyte "wikipedia:pt:Gibibyte")). Por exemplo, para criar um arquivo swap de 512 MiB:

```
# fallocate -l 512M /swapfile

```

**Nota:** *fallocate* pode causar problemas com alguns sistemas de arquivos tal como [F2FS](/index.php/F2FS "F2FS") ou [XFS](/index.php/XFS "XFS").[[1]](https://bugzilla.redhat.com/show_bug.cgi?id=1129205#c3) Como uma alternativa, usar *dd* é mais confiável, mas mais lento: `# dd if=/dev/zero of=/swapfile bs=1M count=512` 

Defina as permissões certas (um arquivo swap legível por todos é uma imensa vulnerabilidade local)

```
# chmod 600 /swapfile

```

Após criar o arquivo no tamanho correto, formate-o para swap:

```
# mkswap /swapfile

```

Ative o arquivo swap:

```
# swapon /swapfile

```

Finalmente, edite o [fstab](/index.php/Fstab "Fstab") para adicionar uma entrada para o arquivo swap:

 `/etc/fstab`  `/swapfile none swap defaults 0 0` 

#### Remover arquivo swap

To remove a swap file, it must be turned off first and then can be removed:

```
# swapoff -a
# rm -f /swapfile

```

Finally remove the relevant entry from `/etc/fstab`.

### Automatizado

#### systemd-swap

[Install](/index.php/Install "Install") the [systemd-swap](https://www.archlinux.org/packages/?name=systemd-swap) package. Set `swapfc_enabled=1` in the *Swap File Chunked* section of `/etc/systemd/swap.conf`. [Start/enable](/index.php/Start/enable "Start/enable") the `systemd-swap` service. Visit the [authors GitHub](https://github.com/Nefelim4ag/systemd-swap) page for more information and setting up the [recommended configuration](https://github.com/Nefelim4ag/systemd-swap/blob/master/README.md#about-configuration).

**Note:** If the journal keeps showing the following warning `systemd-swap[..]: WARN: swapFC: ENOSPC` and no swap file is being created, you need to set `swapfc_force_preallocated=1` in `/etc/systemd/swap.conf`.

## Swap com dispositivo USB

Thanks to the modularity offered by Linux, we can have multiple swap partitions spread over different devices. If you have a very full hard disk, a USB device can be used as a swap partition temporarily. However, this method has some severe disadvantages:

*   A USB device is slower than a hard disk
*   Flash memory has a limited number of write cycles. Using it as a swap partition can kill it quickly

To add a USB device to swap, first take a USB flash drive and partition it for swap as described in [#Swap partition](#Swap_partition).

Next open `/etc/fstab` and add

```
pri=0

```

to the mount options of the *original* swap entry so that the USB swap partition will take priority over the old swap partition.

This guide will work for other memory such as SD cards, etc.

## Criptografia swap

See [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

## Desempenho

Swap operations are usually significantly slower than directly accessing data in RAM. Disabling swap entirely to improve performance can sometimes lead to a degradation, since it decreases the memory available for VFS caches, causing more frequent and costly disk I/O.

Swap values can be adjusted to help performance:

### Swappiness

The *swappiness* [sysctl](/index.php/Sysctl "Sysctl") parameter represents the kernel's preference (or avoidance) of swap space. Swappiness can have a value between 0 and 100, the default value is 60\. A low value causes the kernel to avoid swapping, a higher value causes the kernel to try to use swap space. Using a low value on sufficient memory is known to improve responsiveness on many systems.

To check the current swappiness value:

```
$ cat /sys/fs/cgroup/memory/memory.swappiness

```

or

```
$ cat /proc/sys/vm/swappiness

```

**Note:** As `/proc` is a lot less organized and is kept only for compatibility purposes, you are encouraged to use `/sys` instead.

To temporarily set the swappiness value:

```
# sysctl vm.swappiness=10

```

To set the swappiness value permanently, edit a *sysctl* configuration file

 `/etc/sysctl.d/99-sysctl.conf`  `vm.swappiness=10` 

To test and more on why this may work, take a look at [this article](http://rudd-o.com/en/linux-and-free-software/tales-from-responsivenessland-why-linux-feels-slow-and-how-to-fix-that).

### Pressão de cache VFS

Another *sysctl* parameter that affects swap performance is `vm.vfs_cache_pressure`, which controls the tendency of the kernel to reclaim the memory which is used for caching of VFS caches, versus pagecache and swap. Increasing this value increases the rate at which VFS caches are reclaimed[[2]](http://doc.opensuse.org/documentation/leap/tuning/html/book.sle.tuning/cha.tuning.memory.html#cha.tuning.memory.vm.reclaim). For more information, see the [Linux kernel documentation](https://www.kernel.org/doc/Documentation/sysctl/vm.txt).

### Prioridade

If you have more than one swap file or swap partition you should consider assigning a priority value (0 to 32767) for each swap area. The system will use swap areas of higher priority before using swap areas of lower priority. For example, if you have a faster disk (`/dev/sda`) and a slower disk (`/dev/sdb`), assign a higher priority to the swap area located on the fastest device. Priorities can be assigned in [fstab](/index.php/Fstab "Fstab") via the `pri` parameter:

```
/dev/sda1 none swap defaults,pri=100 0 0
/dev/sdb2 none swap defaults,pri=10  0 0

```

Or via the `--priority` parameter of swapon:

```
# swapon --priority 100 /dev/sda1

```

If two or more areas have the same priority, and it is the highest priority available, pages are allocated on a round-robin basis between them.

### Usando zswap ou zram

[Zswap](/index.php/Zswap "Zswap") is a Linux kernel feature providing a compressed write-back cache for swapped pages. This increases the performance and decreases the IO-Operations. [ZRAM](/index.php/ZRAM "ZRAM") creates a virtual compressed Swap-file in memory as alternative to a swapfile on disc.

### Distribuição

There is no necessity to use [RAID](/index.php/RAID "RAID") for swap performance reasons. The kernel itself can stripe swapping on several devices, if you just give them the same priority in the `/etc/fstab` file. Refer to [The Software-RAID HOWTO](http://unthought.net/Software-RAID.HOWTO/Software-RAID.HOWTO-2.html#ss2.3) for details.