**Status de tradução:** Esse artigo é uma tradução de [Swap](/index.php/Swap "Swap"). Data da última tradução: 2019-01-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Swap&diff=0&oldid=561612) na versão em inglês.

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

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Espaço swap](#Espaço_swap)
*   [2 Partição swap](#Partição_swap)
    *   [2.1 Ativação por systemd](#Ativação_por_systemd)
    *   [2.2 Desabilitando swap](#Desabilitando_swap)
*   [3 Arquivo swap](#Arquivo_swap)
    *   [3.1 Manualmente](#Manualmente)
        *   [3.1.1 Criação de arquivo swap](#Criação_de_arquivo_swap)
        *   [3.1.2 Remover arquivo swap](#Remover_arquivo_swap)
    *   [3.2 Automatizado](#Automatizado)
        *   [3.2.1 systemd-swap](#systemd-swap)
*   [4 Swap com dispositivo USB](#Swap_com_dispositivo_USB)
*   [5 Criptografia swap](#Criptografia_swap)
*   [6 Desempenho](#Desempenho)
    *   [6.1 Swappiness](#Swappiness)
    *   [6.2 Pressão de cache VFS](#Pressão_de_cache_VFS)
    *   [6.3 Prioridade](#Prioridade)
    *   [6.4 Usando zswap ou zram](#Usando_zswap_ou_zram)
    *   [6.5 Distribuição](#Distribuição)

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

O [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") ativa partições swap com base em dois mecanismos diferentes. Ambos são executáveis em `/usr/lib/systemd/system-generators`. Os geradores são executados na inicialização e criam unidades systemd nativas para montagens. O primeiro, `systemd-fstab-generator`, lê o fstab para gerar unidades, incluindo uma unidade para swap. O segundo, `systemd-gpt-auto-generator` inspeciona o disco raiz para gerar unidades. Ele opera somente nos discos GPT e pode identificar as partições swap pelo tipo GUID, consulte [systemd (Português)#Automontagem de partição GPT](/index.php/Systemd_(Portugu%C3%AAs)#Automontagem_de_partição_GPT "Systemd (Português)") para obter mais informações.

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

**Nota:** *fallocate* pode causar problemas com alguns sistemas de arquivos tal como [F2FS](/index.php/F2FS "F2FS") ou [XFS](/index.php/XFS "XFS").[[1]](https://bugzilla.redhat.com/show_bug.cgi?id=1129205#c3) Como uma alternativa, usar *dd* é mais confiável, mas mais lento: `# dd if=/dev/zero of=/swapfile bs=1M count=512 status=progress` 

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

 `/etc/fstab` 
```
/swapfile none swap defaults 0 0

```

**Nota:** O arquivo swap deve ser especificado por sua localização no sistema de arquivos, e não por seu UUID ou LABEL.

#### Remover arquivo swap

Para remover um arquivo swap, ele deve primeiro ser desligado:

```
# swapoff -a
# rm -f /swapfile

```

Por fim, remova a entrada relevante do `/etc/fstab`.

### Automatizado

#### systemd-swap

[Instale](/index.php/Instale "Instale") o pacote [systemd-swap](https://www.archlinux.org/packages/?name=systemd-swap). Defina `swapfc_enabled=1` NA seção *Swap File Chunked* do `/etc/systemd/swap.conf`. [Inicie/habilite](/index.php/Inicie/habilite "Inicie/habilite") o serviço `systemd-swap`. Visite a página do [autor no GitHub](https://github.com/Nefelim4ag/systemd-swap) para mais informações e instalação da [configuração recomendada](https://github.com/Nefelim4ag/systemd-swap/blob/master/README.md#about-configuration).

**Nota:** Se o journal fica mostrando o aviso a seguir `systemd-swap[..]: WARN: swapFC: ENOSPC` e nenhum arquivo swap está sendo criado, você precisa definir `swapfc_force_preallocated=1` no `/etc/systemd/swap.conf`.

## Swap com dispositivo USB

Graças à modularidade oferecida pelo Linux, podemos ter várias partições de troca espalhadas por diferentes dispositivos. Se você tiver um disco rígido muito completo, um dispositivo USB pode ser usado temporariamente como partição de troca. No entanto, esse método tem algumas desvantagens severas:

*   Um dispositivo USB possivelmente é mais lento que um disco rígido
*   A memória flash possui um número limitado de ciclos de gravação. Usá-lo como uma partição swap pode matá-lo rapidamente

Para adicionar um dispositivo USB à swap, primeiro pegue uma unidade flash USB e particione-a para a swap, conforme descrito em [#Partição swap](#Partição_swap).

Em seguida, abra `/etc/fstab` e adicione

```
pri=0

```

para as opções de montagem da entrada de swap *original* para que a partição swap USB tenha prioridade sobre a partição swap antiga.

Esse guia vai funcionar para outras memórias tal como cartões SD, etc.

## Criptografia swap

Veja [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

## Desempenho

As operações de swap geralmente são significativamente mais lentas do que acessar diretamente os dados na RAM. A desativação total da swap para melhorar o desempenho pode levar a uma degradação, pois diminui a memória disponível para caches VFS, causando E/S de disco mais frequente e dispendiosa.

Os valores de swap podem ser ajustados para ajudar no desempenho:

### Swappiness

O parâmetro de [sysctl](/index.php/Sysctl "Sysctl") para *swappiness* (isto é, a capacidade de realizar swap) representa a preferência (ou evitação) do kernel a cerca do espaço de swap. Swappiness pode ter um valor entre 0 e 100, o valor padrão é 60\. Um valor baixo faz com que o kernel evite swap, um valor mais alto faz com que o kernel tente usar o espaço de swap. Sabe-se que usar um valor baixo em memória suficiente melhora a capacidade de resposta em muitos sistemas.

Para verificar o valor atual de swappiness:

```
$ cat /sys/fs/cgroup/memory/memory.swappiness

```

ou

```
$ cat /proc/sys/vm/swappiness

```

**Nota:** Como `/proc` é muito menos organizado e é mantido apenas para propósitos de compatibilidade, você é encorajado a usar `/sys`.

Para definir temporariamente o valor do swappiness:

```
# sysctl vm.swappiness=10

```

Para definir permanentemente o valor de swappiness, edite um arquivo de configuração *sysctl*

 `/etc/sysctl.d/99-sysctl.conf`  `vm.swappiness=10` 

Para testar e mais sobre por que isso pode funcionar, dê uma olhada [neste artigo](http://rudd-o.com/en/linux-and-free-software/tales-from-responsivenessland-why-linux-feels-slow-and-how-to-fix-that).

### Pressão de cache VFS

Outro parâmetro *sysctl* que afeta o desempenho da swap é `vm.vfs_cache_pressure`, que controla a tendência do kernel para recuperar a memória que é usada para armazenamento em cache de caches VFS, versus cache de páginas e swap. Aumentar esse valor aumenta a taxa na qual os caches VFS são recuperados [[2]](http://doc.opensuse.org/documentation/leap/tuning/html/book.sle.tuning/cha.tuning.memory.html#cha.tuning.memory.vm.reclaim). Para mais informações, consulte a [documentação do kernel Linux](https://www.kernel.org/doc/Documentation/sysctl/vm.txt).

### Prioridade

Se você tiver mais de um arquivo de swap ou partição de swap, considere atribuir um valor de prioridade (0 a 32767) para cada área de swap. O sistema usará áreas de swap de prioridade mais alta antes de usar áreas de swap de menor prioridade. Por exemplo, se você tiver um disco mais rápido (`/dev/sda`) e um disco mais lento (`/dev/sdb`), atribua uma prioridade mais alta à área de troca localizada no mais rápido dispositivo. Prioridades podem ser atribuídas em [fstab](/index.php/Fstab "Fstab") através do parâmetro `pri`:

```
/dev/sda1 none swap defaults,pri=100 0 0
/dev/sdb2 none swap defaults,pri=10  0 0

```

Ou por meio do parâmetro `--priority` de *swapon*:

```
# swapon --priority 100 /dev/sda1

```

Se duas ou mais áreas tiverem a mesma prioridade e for a prioridade mais alta disponível, as páginas serão alocadas em uma base round-robin entre elas.

### Usando zswap ou zram

O [zswap](/index.php/Zswap "Zswap") é um recurso de kernel do Linux que fornece um cache de write-back compactado para páginas do swap. Isso aumenta o desempenho e diminui o operações de E/S. [ZRAM](/index.php/ZRAM "ZRAM") cria um arquivo swap compactado virtual na memória como alternativa a um arquivo swap no disco.

### Distribuição

Não há necessidade de usar [RAID](/index.php/RAID "RAID") por motivos de desempenho de swap. O kernel em si pode distribuir a troca em vários dispositivos, se você apenas der a mesma prioridade no arquivo `/etc/fstab`. Consulte o [The Software-RAID HOWTO](http://unthought.net/Software-RAID.HOWTO/Software-RAID.HOWTO-2.html#ss2.3) para obter detalhes.