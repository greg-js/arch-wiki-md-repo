Artigos relacionados

*   [Improving performance/Boot process](/index.php/Improving_performance/Boot_process "Improving performance/Boot process")
*   [Pacman/Dicas e truques#Desempenho](/index.php/Pacman/Dicas_e_truques#Desempenho "Pacman/Dicas e truques")
*   [OpenSSH#Speeding up SSH](/index.php/OpenSSH#Speeding_up_SSH "OpenSSH")
*   [Openoffice#Speed up OpenOffice](/index.php/Openoffice#Speed_up_OpenOffice "Openoffice")
*   [Laptop](/index.php/Laptop "Laptop")
*   [Preload](/index.php/Preload "Preload")

Este artigo oferece informação sobre diagnósticos básicos do sistema relacionados com desempenho e também passos que podem ser tomados para reduzir o consumo de recursos ou otimizar o sistema com o objetivo final de melhorias perceptíveis ou documentadas.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 O básico](#O_básico)
    *   [1.1 Conheça o seu sistema](#Conheça_o_seu_sistema)
    *   [1.2 Fazer benchmark](#Fazer_benchmark)
*   [2 Dispositivos de armazenamento](#Dispositivos_de_armazenamento)
    *   [2.1 Múltiplas conexões de hardware](#Múltiplas_conexões_de_hardware)
    *   [2.2 Particionamento](#Particionamento)
        *   [2.2.1 Múltiplas unidades de armazenamento](#Múltiplas_unidades_de_armazenamento)
        *   [2.2.2 Particionamento em HDDs](#Particionamento_em_HDDs)
    *   [2.3 Escolhendo e aumentando o desempenho do seu sistema de arquivos](#Escolhendo_e_aumentando_o_desempenho_do_seu_sistema_de_arquivos)
        *   [2.3.1 Opções de montagem](#Opções_de_montagem)
            *   [2.3.1.1 Reiserfs](#Reiserfs)
    *   [2.4 Parâmetros do kernel que melhoram o desempenho](#Parâmetros_do_kernel_que_melhoram_o_desempenho)
    *   [2.5 Escalonador de input/output](#Escalonador_de_input/output)
        *   [2.5.1 Informações básicas](#Informações_básicas)
        *   [2.5.2 The scheduling algorithms](#The_scheduling_algorithms)
        *   [2.5.3 Kernel's I/O schedulers](#Kernel's_I/O_schedulers)
        *   [2.5.4 Changing I/O scheduler](#Changing_I/O_scheduler)
        *   [2.5.5 Tuning I/O scheduler](#Tuning_I/O_scheduler)
    *   [2.6 Configuração de gerenciamento de energia](#Configuração_de_gerenciamento_de_energia)
    *   [2.7 Reduzir leituras/escritas no disco](#Reduzir_leituras/escritas_no_disco)
        *   [2.7.1 Mostrar escritas no disco](#Mostrar_escritas_no_disco)
        *   [2.7.2 Realocar arquivos para tmpfs](#Realocar_arquivos_para_tmpfs)
        *   [2.7.3 Sistema de arquivos](#Sistema_de_arquivos)
        *   [2.7.4 Espaço swap](#Espaço_swap)
        *   [2.7.5 Intervalo de writeback e tamanho do buffer](#Intervalo_de_writeback_e_tamanho_do_buffer)
    *   [2.8 Agendando tarefas I/O com ionice](#Agendando_tarefas_I/O_com_ionice)
*   [3 CPU](#CPU)
    *   [3.1 Overclocking](#Overclocking)
    *   [3.2 Escala de frequência](#Escala_de_frequência)
    *   [3.3 Escalonadores alternativos da CPU](#Escalonadores_alternativos_da_CPU)
    *   [3.4 Real-time kernel](#Real-time_kernel)
    *   [3.5 Ajustando as prioridades dos processos](#Ajustando_as_prioridades_dos_processos)
        *   [3.5.1 Ananicy](#Ananicy)
        *   [3.5.2 cgroups](#cgroups)
        *   [3.5.3 Cpulimit](#Cpulimit)
    *   [3.6 irqbalance](#irqbalance)
    *   [3.7 Desligar as mitigações das falhas da CPU](#Desligar_as_mitigações_das_falhas_da_CPU)
*   [4 Gráficos](#Gráficos)
    *   [4.1 Configuração do Xorg](#Configuração_do_Xorg)
    *   [4.2 Configuração do Mesa](#Configuração_do_Mesa)
    *   [4.3 Overclocking](#Overclocking_2)
*   [5 RAM and swap](#RAM_and_swap)
    *   [5.1 Clock frequency and timings](#Clock_frequency_and_timings)
    *   [5.2 Root on RAM overlay](#Root_on_RAM_overlay)
    *   [5.3 Zram or zswap](#Zram_or_zswap)
        *   [5.3.1 Swap na zRAM usando uma regra do udev](#Swap_na_zRAM_usando_uma_regra_do_udev)
    *   [5.4 Usando a RAM da placa de vídeo](#Usando_a_RAM_da_placa_de_vídeo)
*   [6 Rede](#Rede)
*   [7 Watchdogs](#Watchdogs)
*   [8 Veja também](#Veja_também)

## O básico

### Conheça o seu sistema

A melhor maneira de aprimorar um sistema é ter como alvo os gargalos, ou subsistemas que limitam o desempenho médio. As especificações do sistema podem ajudar a identificá-las.

*   Se o computador se torna lento quando aplicações grandes (como LibreOffice e Firefox) rodam ao mesmo tempo, verifique se a quantidade de RAM é suficiente. Use o seguinte comando e verifique a coluna "available" (ou "disponível" em português):

```
$ free -h

```

*   Se a inicialização é lenta, e programas demoram muito tempo para carregar na primeira vez (apenas) que são executados, então possivelmente é culpa do disco rígido. A velocidade dele pode ser mensurada com o comando `hdparm`:

**Nota:** [hdparm](https://www.archlinux.org/packages/?name=hdparm) indica somente a velocidade de escrita e leitura pura de um disco rígido, e não é um benchmark válido. Um valor maior que 40MB/s (enquanto ocioso) é aceitável em um sistema mediano.

```
# hdparm -t /dev/sdX

```

*   Se o carregamento da CPU é consistemente alto até mesmo com bastante RAM disponível, tente diminuir o uso da CPU ao desabilitar [daemons](/index.php/Daemons "Daemons") que estão rodando e/ou processos. Isto pode ser monitorado de algumas formas, por exemplo com [htop](https://www.archlinux.org/packages/?name=htop), `pstree` ou qualquer outra ferramenta de [monitoração do sistema](/index.php/List_of_applications#System_monitors "List of applications"):

```
$ htop

```

*   Se aplicações usam renderização direta estão lentas (exemplo, estas que usam a GPU, tais como players de vídeo, jogos, ou até mesmo um [gerenciador de janelas](/index.php/Window_manager "Window manager")), então melhorar o desempenho da GPU deve ajudar. O primeiro passo é verificar se a renderização direta está habilitada. Isto é indicado pelo comando `glxinfo`, parte do pacote [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos):

 `$ glxinfo | grep "direct rendering"` 
```
direct rendering: Yes

```

*   Ao usar um [ambiente de desktop](/index.php/Ambientes_de_desktop "Ambientes de desktop"), desabilitar efeitos visuais (não usados) pode reduzir o uso da GPU. Use um ambiente mais leve ou crie um [personalizado](/index.php/Ambientes_de_desktop#Ambientes_personalizados "Ambientes de desktop"), se o atual não é compatível com seu hardware e/ou preferências pessoais.

### Fazer benchmark

Os efeitos de otimização são normalmente dificieis de julgar. No entanto estes podem ser mensurados por ferramentas de [benchmark](/index.php/Benchmarking "Benchmarking").

## Dispositivos de armazenamento

### Múltiplas conexões de hardware

Um caminho interno do hardware é como o dispositivo de armazenamento é conectado para sua placa-mãe. Existem diferentes maneiras de se conectar a ela como: TCP/IP atravês de uma NIC, plugado diretamente com PCIe/PCI, Fireware, Raid Card, USB, etc. Ao espalhar seus dispositivos de armazenamento por estes múltiplos pontos de conexão, você maximiza as capacidades de sua placa-mãe, por exemplo 6 discos rígidos conectados por USB devem ser bem mais lentos que 3 pelo USB e 3 pelo Firewire. O motivo disso é que cada conexão de entrada na placa-mãe é como um tubo, e existe um limite de quanto você pode transmitir por vez. A boa notícia é que ela normalmente tem vários tubos.

Mais exemplos

1.  Diretamente na placa-mãe usando PCI/PCIe/ATA
2.  Usando uma capa externa para guardar o disco por USB/Firewire
3.  Jogar o dispositivo no dispositivo de armazenamento da rede ao conectar com TCP/IP

Note também que se você tem duas portas USB na frente da sua máquina, e 4 portas USB atrás, e possui 4 discos, deve ser mais rápido/eficiente colocar 2 na frente e 2 atrás do que 3 atrás e 1 na frente. Devido a portas da frente provavelmente possuírem um Hub USB separado, significando que você pode enviar duas vezes mais dados do que somente usar 1\. Use os seguintes comandos para determinar as várias conexões de hardware de sua máquina.

 `USB Device Tree`  `$ lsusb -t`  `PCI Device Tree`  `$ lspci -tv` 

### Particionamento

Garanta que suas partições estão [apropriadamente alinhadas](/index.php/Particionamento#Alinhamento_de_partição "Particionamento").

#### Múltiplas unidades de armazenamento

Se você têm múltiplos discos disponíveis, você pode configurar um [RAID](/index.php/RAID "RAID") de software para sérias melhorias na velocidade.

Criar uma [swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)") em um disco separado pode ajudar, especialmente se sua máquina envia dados frequentemente para a swap.

#### Particionamento em HDDs

Se você está usando o tradicional HDD rotacional, seu particionamento pode influenciar a performance do sistema. Setores no começo do disco (mais próximos de fora do disco) são mais rápidos que estes no fim. Também, uma menor partição precisa de menos movimentos da cabeça da unidade de armazenamento, e consequentemente acelera as operações no disco. É recomendado criar partições menores (10GB, mais ou menos dependendo de suas necessidades) somente para seu sistema, tão próximo do começo do disco quanto possível. Outros dados (imagens, vídeos) devem ser mantidos em uma partição separada, isto normalmente é feito ao separar o diretório home (`/home/*usuário*`) do sistema (`/`).

### Escolhendo e aumentando o desempenho do seu sistema de arquivos

Escolher o melhor sistema de arquivos para seu sistema específico é muito importante, pois cada um tem suas especificidades. Os artigos dos [sistemas de arquivos](/index.php/Sistemas_de_arquivos "Sistemas de arquivos") oferecem um pequeno sumário dos mais populares. Você pode também encontrar artigos relevantes em [Category:File systems (Português)](/index.php/Category:File_systems_(Portugu%C3%AAs) "Category:File systems (Português)").

#### Opções de montagem

A opção [noatime](/index.php/Fstab#atime_options "Fstab") é conhecida por melhorar o desempenho de sistemas de arquivos.

Outras opções são específicas para cada sistema de arquivos, então veja os artigos relevantes de cada um deles: mount options are filesystem specific, therefore see the relevant articles for the filesystems:

*   [Ext3](/index.php/Ext3 "Ext3")
*   [Ext4#Melhorando o desempenho](/index.php/Ext4_(Portugu%C3%AAs)#Melhorando_o_desempenho "Ext4 (Português)")
*   [JFS Filesystem#Optimizations](/index.php/JFS_Filesystem#Optimizations "JFS Filesystem")
*   [XFS#Performance](/index.php/XFS#Performance "XFS")
*   [Btrfs#Defragmentation](/index.php/Btrfs#Defragmentation "Btrfs"), [Btrfs#Compression](/index.php/Btrfs#Compression "Btrfs"), e [btrfs(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/btrfs.5)
*   [ZFS#Tuning](/index.php/ZFS#Tuning "ZFS")

##### Reiserfs

A opção de montagem `data=writeback` melhora a velocidade, mas pode corromper dados durante uma queda de energia. A opção de montagem `notail` aumenta o espaço usado pelo sistema de arquivos por volta de 5%, mas melhora o desempenho geral. Você pode reduzir o carregamento do disco ao colocar o journal e dados em unidades de armazenamento separadas. Isto é feito ao criar o sistema de arquivos:

```
# mkreiserfs –j /dev/sd**a1** /dev/sd**b1**

```

Substitua o `/dev/sd**a1**` com a partição reservada para o journal, e `/dev/sd**b1**` com a partição para dados. Você pode aprender mais sobre reiserfs com este [artigo](http://www.funtoo.org/Funtoo_Filesystem_Guide,_Part_2).

### Parâmetros do kernel que melhoram o desempenho

Existem algumas chaves habilitáveis que afetam positivamente o desempenho de dispositivos de bloco, veja [sysctl#Virtual memory](/index.php/Sysctl#Virtual_memory "Sysctl") para mais informações.

### Escalonador de input/output

#### Informações básicas

O escalonador (scheduler) de input/output *(I/O)* é o componente do kernel que decide em que ordem as operações de bloco I/O são submetidas para dispositivos de armazenamento. É útil se lembrar de algumas especificações dos dois principais tipos de unidades de armazenamento devido ao objetivo do escalonador I/O, que é otimizar a maneira de lidar com os pedidos de leitura:

*   Um HDD tem discos giratórios e uma cabeça que se move fisicamente para a localização solicitada. Latência randômica é muito alta estando entre 3 e 12ms (não importando se é um dispositivo de armazenamento de um servidor de última geração ou de notebook e ignorando o buffer de escrita controlador do disco) enquanto o acesso sequencial oferece uma taxa de transferência muito maior. O HDD típico faz em torno de 200 operações I/O por segundo *(IOPS)*.

*   Um SSD não tem partes móveis, acesso randômico é tão rápido quanto sequencial, tipicamente abaixo de 0.1ms, e pode manusear múltiplas solicitações concorrentes. A velocidade de saída do SSD típico é maior que 10,000 IOPS, que é mais do que o necessário para situações comuns de grande trabalho.

Se existem muitos processos fazendo solicitações I/O para diferentes partes do armazenamento, milhares de IOPS podem ser gerados enquanto o HDD típico pode manusear em torno de somente 200 IOPS. Existe uma fila de solicitações que terão de esperar para acessar o disco. Esta situação é onde escalonadores I/O entram com a tarefa de otimização.

#### The scheduling algorithms

One way to improve throughput is to linearize access: by ordering waiting requests by their logical address and grouping the closest ones. Historically this was the first Linux I/O scheduler called [elevator](https://en.wikipedia.org/wiki/Elevator_algorithm "w:Elevator algorithm").

One issue with the elevator algorithm is that it is not optimal for a process doing sequential access: reading a block of data, processing it for several microseconds then reading next block and so on. The elevator scheduler does not know that the process is about to read another block nearby and, thus, moves to another request by another process at some other location. The [anticipatory](https://en.wikipedia.org/wiki/Anticipatory_scheduling "w:Anticipatory scheduling") I/O scheduler overcomes the problem: it pauses for a few milliseconds in anticipation of another close-by read operation before dealing with another request.

While these schedulers try to improve total throughput, they might leave some unlucky requests waiting for a very long time. As an example, imagine the majority of processes make requests at the beginning of the storage space while an unlucky process makes a request at the other end of storage. This potentially infinite postponement of the process is called starvation. To improve fairness, the [deadline](https://en.wikipedia.org/wiki/Deadline_scheduler "w:Deadline scheduler") algorithm was developed. It has a queue ordered by address, similar to the elevator, but if some request sits in this queue for too long then it moves to an "expired" queue ordered by expire time. The scheduler checks the expire queue first and processes requests from there and only then moves to the elevator queue. Note that this fairness has a negative impact on overall throughput.

The [Completely Fair Queuing *(CFQ)*](https://en.wikipedia.org/wiki/CFQ "w:CFQ") approaches the problem differently by allocating a timeslice and a number of allowed requests by queue depending on the priority of the process submitting them. It supports [cgroup](/index.php/Cgroup "Cgroup") that allows to reserve some amount of I/O to a specific collection of processes. It is in particular useful for shared and cloud hosting: users who paid for some IOPS want to get their share whenever needed. Also, it idles at the end of synchronous I/O waiting for other nearby operations, taking over this feature from the *anticipatory* scheduler and bringing some enhancements. Both the *anticipatory* and the *elevator* schedulers were decommissioned from the Linux kernel replaced by the more advanced alternatives presented above.

The [Budget Fair Queuing *(BFQ)*](https://algo.ing.unimo.it/people/paolo/disk_sched/) is based on CFQ code and brings some enhancements. It does not grant the disk to each process for a fixed time-slice but assigns a "budget" measured in number of sectors to the process and uses heuristics. It is a relatively complex scheduler, it may be more adapted to rotational drives and slow SSDs because its high per-operation overhead, especially if associated with a slow CPU, can slow down fast devices. The objective of BFQ on personal systems is that for interactive tasks, the storage device is virtually as responsive as if it was idle. In its default configuration it focuses on delivering the lowest latency rather than achieving the maximum throughput.

[Kyber](https://lwn.net/Articles/720675/) is a recent scheduler inspired by active queue management techniques used for network routing. The implementation is based on "tokens" that serve as a mechanism for limiting requests. A queuing token is required to allocate a request, this is used to prevent starvation of requests. A dispatch token is also needed and limits the operations of a certain priority on a given device. Finally, a target read latency is defined and the scheduler tunes itself to reach this latency goal. The implementation of the algorithm is relatively simple and it is deemed efficient for fast devices.

#### Kernel's I/O schedulers

While some of the early algorithms have now been decommissioned, the official Linux kernel supports a number of I/O schedulers which can be split into two categories:

*   The **multi-queue schedulers** are available by default with the kernel. The [Multi-Queue Block I/O Queuing Mechanism *(blk-mq)*](https://www.thomas-krenn.com/en/wiki/Linux_Multi-Queue_Block_IO_Queueing_Mechanism_(blk-mq)) maps I/O queries to multiple queues, the tasks are distributed across threads and therefore CPU cores. Within this framework the following schedulers are available:
    *   *None*, no queuing algorithm is applied.
    *   *mq-deadline* is the adaptation of the deadline scheduler to multi-threading.
    *   *Kyber*
    *   *BFQ*

*   The **single-queue schedulers** are legacy schedulers, they can be activated at boot time as described in [#Changing I/O scheduler](#Changing_I/O_scheduler):
    *   [NOOP](https://en.wikipedia.org/wiki/NOOP_scheduler "w:NOOP scheduler") is the simplest scheduler, it inserts all incoming I/O requests into a simple FIFO queue and implements request merging. In this algorithm, there is no re-ordering of the request based on the sector number. Therefore it can be used if the ordering is dealt with at another layer, at the device level for example, or if it does not matter, for SSDs for instance.
    *   *Deadline*
    *   *CFQ*

**Note:** Single-queue schedulers [were removed from kernel since Linux 5.0](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=f382fb0bcef4c37dc049e9f6963e3baf204d815c).

#### Changing I/O scheduler

**Note:**

*   The block multi-queue *(blk-mq)* mode must be disabled at boot time to be able to access the legacy *CFQ* and *Deadline* schedulers. This is done by adding `scsi_mod.use_blk_mq=0` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). The multi-queue schedulers are no longer available once in this mode.
*   The best choice of scheduler depends on both the device and the exact nature of the workload. Also, the throughput in MB/s is not the only measure of performance: deadline or fairness deteriorate the overall throughput but may improve system responsiveness. [Benchmarking](/index.php/Benchmarking "Benchmarking") may be useful to indicate each I/O scheduler performance.

To list the available schedulers for a device and the active scheduler (in brackets):

 `$ cat /sys/block/***sda***/queue/scheduler`  `mq-deadline kyber [bfq] none` 

To list the available schedulers for all devices:

 `$ cat /sys/block/*****/queue/scheduler` 
```
none
[mq-deadline] kyber bfq none
mq-deadline kyber [bfq] none
```

To change the active I/O scheduler to *bfq* for device *sda*, use:

```
# echo ***bfq*** > /sys/block/***sda***/queue/scheduler

```

The process to change I/O scheduler, depending on whether the disk is rotating or not can be automated and persist across reboots. For example the [udev](/index.php/Udev "Udev") rule below sets the scheduler to *none* for [NVMe](/index.php/NVMe "NVMe"), *mq-deadline* for [SSD](/index.php/SSD "SSD")/eMMC, and *bfq* for rotational drives:

 `/etc/udev/rules.d/60-ioschedulers.rules` 
```
# set scheduler for NVMe
ACTION=="add|change", KERNEL=="nvme[0-9]*", ATTR{queue/scheduler}="none"
# set scheduler for SSD and eMMC
ACTION=="add|change", KERNEL=="sd[a-z]|mmcblk[0-9]*", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="mq-deadline"
# set scheduler for rotating disks
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="1", ATTR{queue/scheduler}="bfq"
```

Reboot or force [udev#Loading new rules](/index.php/Udev#Loading_new_rules "Udev").

#### Tuning I/O scheduler

Each of the kernel's I/O scheduler has its own tunables, such as the latency time, the expiry time or the FIFO parameters. They are helpful in adjusting the algorithm to a particular combination of device and workload. This is typically to achieve a higher throughput or a lower latency for a given utilization. The tunables and their description can be found within the [kernel documentation files](https://www.kernel.org/doc/Documentation/block/).

To list the available tunables for a device, in the example below *sdb* which is using *deadline*, use:

 `$ ls /sys/block/***sdb***/queue/iosched`  `fifo_batch  front_merges  read_expire  write_expire  writes_starved` 

To improve *deadline'*s throughput at the cost of latency, one can increase `fifo_batch` with the command:

 `# echo *32* > /sys/block/***sdb***/queue/iosched/**fifo_batch**` 

### Configuração de gerenciamento de energia

Ao lidar com discos rotacionais tradicionais (HDDs) você pode querer [diminuir ou desabilitar funcionalidades de economia de energia](/index.php/Hdparm#Power_management_configuration "Hdparm") completamente.

### Reduzir leituras/escritas no disco

Evitar acessos desnecessários em unidades de armazenamento lentas é bom para a performance e também aumenta a vida útil dos dispositivos, apesar que em hardware moderno a diferença é normalmente insignificante.

**Nota:** Um SSD de 32GB com um fator medíocre de amplificação de escrita em 10 vezes, um padrão de 10000 ciclos de escrever/apagar, e **10GB de dados escritos por dia**, deve lhe dar uma **espectativa de vida útil de 8 anos**. Isto melhora com SSDs maiores e controladores modernos com menos amplificação de escrita. Também compare [[1]](http://techreport.com/review/25889/the-ssd-endurance-experiment-500tb-update) ao considerar se qualquer estratégia particular para limitar escritas no disco é, de verdade, necessária.

#### Mostrar escritas no disco

O pacote [iotop](https://www.archlinux.org/packages/?name=iotop) pode ordenar programas por escritas no disco, e mostrar quanto e quão frequentemente estes estão escrevendo no disco. Veja [iotop(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iotop.8) para detalhes.

#### Realocar arquivos para tmpfs

Realocar arquivos, tais como perfil do navegador, para um sistema de arquivos [tmpfs](/index.php/Tmpfs "Tmpfs"), melhora a responsividade do programa já que todos os arquivo estão guardados na RAM:

*   Veja [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon") para sincronizar perfis do navegador. Certos navegadores podem precisar de atenção especial, veja por exemplo [Firefox on RAM](/index.php/Firefox_on_RAM "Firefox on RAM").
*   Veja [Anything-sync-daemon](/index.php/Anything-sync-daemon "Anything-sync-daemon") para sincronizar qualquer diretório específico.
*   Veja [Makepkg#Melhorando os tempos de compilação](/index.php/Makepkg_(Portugu%C3%AAs)#Melhorando_os_tempos_de_compilação "Makepkg (Português)") para melhorar tempo de compilação ao compilar pacotes no tmpfs.

#### Sistema de arquivos

Veja a página correspondente do seu [sistema de arquivos](/index.php/Sistema_de_arquivos "Sistema de arquivos") para possíveis instruções que melhoram a performance, exemplo [ext4#Melhorando o desempenho](/index.php/Ext4_(Portugu%C3%AAs)#Melhorando_o_desempenho "Ext4 (Português)") e [XFS#Performance](/index.php/XFS#Performance "XFS").

#### Espaço swap

Veja [swap#Desempenho](/index.php/Swap_(Portugu%C3%AAs)#Desempenho "Swap (Português)").

#### Intervalo de writeback e tamanho do buffer

Veja [Sysctl#Virtual memory](/index.php/Sysctl#Virtual_memory "Sysctl") para detalhes.

### Agendando tarefas I/O com ionice

Muitas tarefas como backup não dependem de um pequeno atraso I/O ou uma grande banda de armazenamento I/O para seu objetivo, eles podem ser classificados como tarefas de segundo plano. O I/O rápido é necessário para boa responsibilidade da interface do usuário no desktop. Então é benefíco reduzir a quantidade de banda de armazenamento disponível para tarefas de segundo plano, enquanto outras precisam de prioridade. Isto pode ser alcançado ao fazer uso do escalonador I/O CFQ do linux, que permite configurar diferentes prioridades para os processos.

A prioridade I/O de um processo de segundo plano pode ser reduzida para o nível "idle" (ocioso) com o comando:

```
# ionice -c 3 *seu_comando_aqui*

```

Veja [ionice(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ionice.1) e [[2]](https://www.cyberciti.biz/tips/linux-set-io-scheduling-class-priority.html) para mais informação.

## CPU

### Overclocking

[Overclocking](https://en.wikipedia.org/wiki/Overclocking "wikipedia:Overclocking") melhora a performance computacional da CPU ao aumentar o pico da frequência do clock. A habilidade para fazer overclock depende da combinação do modelo da CPU e placa-mãe. É mais frequentemente feito atravês da BIOS. Fazer overclock também tem desvantagens e riscos, não é nem recomendado nem desencorajado aqui.

Muitos chips da Intel não vão reportar corretamente a frequência do clock para acpi_cpufreq e a maioria dos utilitários. Isto resulta em excessivas mensagens no dmesg, que podem ser evitados ao descarregar ou colocar o módulo do kernel `apcu_cpufreq` na blacklist. Para ler a velocidade do seu clock, use *i7z* do pacote [i7z](https://www.archlinux.org/packages/?name=i7z). Para verificar se a CPU com overclock está operando corretamente, é recomendado fazer um [teste de estresse](/index.php/Stress_testing "Stress testing").

### Escala de frequência

Veja [Escala de frequência do CPU](/index.php/Escala_de_frequ%C3%AAncia_do_CPU "Escala de frequência do CPU").

### Escalonadores alternativos da CPU

O escalonador padrão da CPU que está na mainline do kernel Linux é o [CFS](https://en.wikipedia.org/wiki/Completely_Fair_Scheduler "wikipedia:Completely Fair Scheduler"). Existem alternativas.

Um escalonador alternativo focado na interatividade e responsibilidade é o [MuQSS](http://ck.kolivas.org/patches/muqss/sched-MuQSS.txt), desenvolvido por [Con Kolivas](http://users.tpg.com.au/ckolivas/kernel/). MuQSS está incluído no pacote do kernel [linux-zen](https://www.archlinux.org/packages/?name=linux-zen). Está também disponível como um patch independente ou como parte do conjunto de patches **-ck**. Veja [Linux-ck](/index.php/Linux-ck "Linux-ck") and [Linux-pf](/index.php/Linux-pf "Linux-pf") para mais informações sobre.

### Real-time kernel

Algumas aplicações como usar uma placa sintonizadora de televisão na resolução FULL HD (1080p) podem se beneficiar do uso do [realtime kernel](/index.php/Realtime_kernel "Realtime kernel").

### Ajustando as prioridades dos processos

Veja também [nice(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nice.1) e [renice(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/renice.1).

#### Ananicy

[Ananicy](https://github.com/Nefelim4ag/Ananicy) é um daemon, disponível no pacote [ananicy-git](https://aur.archlinux.org/packages/ananicy-git/), para auto ajustar o nível nice dos executáveis. Os níveis nice representam a prioridade dos executáveis quando alocam recursos da CPU.

#### cgroups

Veja [cgroups](/index.php/Cgroups "Cgroups").

#### Cpulimit

[Cpulimit](https://github.com/opsengine/cpulimit) é um programa que limita o uso da CPU de um processo específico. Depois de instalar [cpulimit](https://www.archlinux.org/packages/?name=cpulimit), você pode limitar o PID de um processo usando uma escala de 0 a 100 vezes o número de núcleos da CPU que o computador têm. Por exemplo, com oito núcleos a porcentagem vai ser de 0 a 800\. Uso:

```
$ cpulimit -l 50 -p 5081

```

### irqbalance

A proposta do [irqbalance](https://www.archlinux.org/packages/?name=irqbalance) é distribuir interrupção de hardware entre processadores em um sistema com múltiplos processadores para aumentar o desempenho. Pode ser [controlado](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)") com `irqbalance.service`.

### Desligar as mitigações das falhas da CPU

**Atenção:** Não aplique esta configuração sem considerar as vulnerabilidades que isto causa. Veja [isto](https://phoronix.com/scan.php?page=news_item&px=Linux-Improve-CPU-Spec-Switches) e [isto](https://linuxreviews.org/HOWTO_make_Linux_run_blazing_fast_(again)_on_Intel_CPUs) para mais informações.

Desligar as mitigações de falhas da CPU melhoram a performance (algumas vezes mais de 50%). Use o [parâmetro do kernel](/index.php/Par%C3%A2metro_do_kernel "Parâmetro do kernel") abaixo para desabilitá-los:

```
mitigations=off

```

A explicação de todos os switches que são passados está no [kernel.org](https://www.kernel.org/doc/html/latest/admin-guide/kernel-parameters.html). Você pode usar [spectre-meltdown-checker](https://aur.archlinux.org/packages/spectre-meltdown-checker/) para checar vulnerabilidade.

## Gráficos

### Configuração do Xorg

O desempenho gráfico pode depender da configurações presentes no [xorg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5); veja os artigos da [NVIDIA](/index.php/NVIDIA "NVIDIA"), [ATI](/index.php/ATI "ATI"), [AMDGPU](/index.php/AMDGPU "AMDGPU") e [Intel](/index.php/Intel "Intel"). Configurações erradas podem fazer o Xorg deixar de funcionar, tome cuidado.

### Configuração do Mesa

O desempenho dos drivers Mesa pode ser configurado com [drirc](https://dri.freedesktop.org/wiki/ConfigurationInfrastructure/). As seguintes ferramentas gráficas estão disponíveis:

*   **adriconf (Advanced DRI Configurator)** — Ferramenta gráfica para configurar os drivers Mesa ao definir opções e escrevê-las para o arquivo drirc padrão.

	[https://github.com/jlHertel/adriconf/](https://github.com/jlHertel/adriconf/) || [adriconf](https://www.archlinux.org/packages/?name=adriconf)

*   **DRIconf** — Applet de configuração para Direct Rendering Infrastructure, DRI (Inflaestrutura de Renderização Direta, em português). Permite customizar o desempenho e configurações da qualidade visual dos drivers OpenGL em um nível por unidade de armazenamento, por tela e/ou por aplicação.

	[https://dri.freedesktop.org/wiki/DriConf/](https://dri.freedesktop.org/wiki/DriConf/) || [driconf](https://aur.archlinux.org/packages/driconf/)

### Overclocking

Assim como acontece com CPUs, overclocking pode diretamente melhorar o desempenho, mas geralmente não é recomendado. Existem pacotes no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), tais como [amdoverdrivectrl](https://aur.archlinux.org/packages/amdoverdrivectrl/) (placas antigas AMD/ATI), [rocm-smi](https://aur.archlinux.org/packages/rocm-smi/) (placas recentes AMD ), [nvclock](https://aur.archlinux.org/packages/nvclock/) (placas NVIDIA antigas - até o Geforce 9), e [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) para placas recentes da NVIDIA.

Veja [AMDGPU#Overclocking](/index.php/AMDGPU#Overclocking "AMDGPU") ou [NVIDIA/Tips and tricks#Enabling overclocking](/index.php/NVIDIA/Tips_and_tricks#Enabling_overclocking "NVIDIA/Tips and tricks").

## RAM and swap

### Clock frequency and timings

RAM can run at different clock frequencies and timings, which can be configured in the BIOS. Memory performance depends on both values. Selecting the highest preset presented by the BIOS usually improves the performance over the default setting. Note that increasing the frequency to values not supported by both motherboard and RAM vendor is overclocking, and similar risks and disadvantages apply, see [#Overclocking](#Overclocking).

### Root on RAM overlay

If running off a slow writing medium (USB, spinning HDDs) and storage requirements are low, the root may be run on a RAM overlay ontop of read only root (on disk). This can vastly improve performance at the cost of a limited writable space to root. See [liveroot](https://aur.archlinux.org/packages/liveroot/).

### Zram or zswap

The [zram](https://www.kernel.org/doc/Documentation/blockdev/zram.txt) kernel module (previously called **compcache**) provides a compressed block device in RAM. If you use it as swap device, the RAM can hold much more information but uses more CPU. Still, it is much quicker than swapping to a hard drive. If a system often falls back to swap, this could improve responsiveness. Using zram is also a good way to reduce disk read/write cycles due to swap on SSDs.

Similar benefits (at similar costs) can be achieved using [zswap](/index.php/Zswap "Zswap") rather than zram. The two are generally similar in intent although not operation: zswap operates as a compressed RAM cache and neither requires (nor permits) extensive userspace configuration.

Example: To set up one lz4 compressed zram device with 32GiB capacity and a higher-than-normal priority (only for the current session):

```
# modprobe zram
# echo lz4 > /sys/block/zram0/comp_algorithm
# echo 32G > /sys/block/zram0/disksize
# mkswap --label zram0 /dev/zram0
# swapon --priority 100 /dev/zram0

```

To disable it again, either reboot or run

```
# swapoff /dev/zram0
# rmmod zram

```

A detailed explanation of all steps, options and potential problems is provided in the official documentation of the module [here](https://www.kernel.org/doc/Documentation/blockdev/zram.txt).

The [systemd-swap](https://www.archlinux.org/packages/?name=systemd-swap) package provides a `systemd-swap.service` unit to automatically initialize zram devices. Configuration is possible in `/etc/systemd/swap.conf`.

The package [zramswap](https://aur.archlinux.org/packages/zramswap/) provides an automated script for setting up such swap devices with optimal settings for your system (such as RAM size and CPU core number). The script creates one zram device per CPU core with a total space equivalent to the RAM available, so you will have a compressed swap with higher priority than regular swap, which will utilize multiple CPU cores for compressing data. To do this automatically on every boot, [enable](/index.php/Enable "Enable") `zramswap.service`.

#### Swap na zRAM usando uma regra do udev

O exemplo abaixo descreve como configurar swap na zRAM automaticamente na inicialização com uma única regra do udev. Nenhum pacote precisa ser instalado.

Primeiro, habilite o módulo:

 `/etc/modules-load.d/zram.conf` 
```
zram

```

Configure o número de células da /dev/zram que você precisa.

 `/etc/modprobe.d/zram.conf` 
```
options zram num_devices=2

```

Crie a regra do udev como mostrado no exemplo.

 `/etc/udev/rules.d/99-zram.rules` 
```
KERNEL=="zram0", ATTR{disksize}="512M" RUN="/usr/bin/mkswap /dev/zram0", TAG+="systemd"
KERNEL=="zram1", ATTR{disksize}="512M" RUN="/usr/bin/mkswap /dev/zram1", TAG+="systemd"

```

Adicione /dev/zram para seu fstab.

 `/etc/fstab` 
```
/dev/zram0 none swap defaults 0 0
/dev/zram1 none swap defaults 0 0

```

### Usando a RAM da placa de vídeo

No cenário pouco provável onde você tem pouca RAM e excedente memória de vídeo, você pode usar a última como swap. Veja [Swap on video RAM](/index.php/Swap_on_video_RAM "Swap on video RAM").

## Rede

*   Gerenciador de rede do Kernel: veja [Sysctl#Improving performance](/index.php/Sysctl#Improving_performance "Sysctl")
*   NIC: veja [Configuração de rede#Definindo o MTU do dispositivo e o tamanho da fila](/index.php/Configura%C3%A7%C3%A3o_de_rede#Definindo_o_MTU_do_dispositivo_e_o_tamanho_da_fila "Configuração de rede")
*   DNS: considere usar um servidor de cache do resolvedor DNS, veja [Resolução de nome de domínio#Servidores DNS](/index.php/Resolu%C3%A7%C3%A3o_de_nome_de_dom%C3%ADnio#Servidores_DNS "Resolução de nome de domínio")
*   Samba: veja [Samba#Improve throughput](/index.php/Samba#Improve_throughput "Samba")

## Watchdogs

De acordo com [wikipedia:Watchdog_timer](https://en.wikipedia.org/wiki/Watchdog_timer "wikipedia:Watchdog timer") (traduzido):

	Um watchdog timer [...] é um temporizador eletrônico que é usado para detectar e recuperar o computador de malfuncionamento. Durante a operação normal, o computador regularmente reseta o watchdog timer [...]. Se, [...], o computador falha para resetar o watchdog, o temporizador vai decorrer e gerar um sinal de timeout [...] usado parar iniciar ações corretivas [...] tipicamente incluindo colocar o sistema do computador em um estado seguro e restaurar a sua operação normal.

Muitos usuários precisam desta funcionalidade devido a cargos críticos do sistema (exemplo, servidores), ou devido a falta de of power reset (exemplo, dispositivos embarcados). Nessas situações, esta funcionalidade é necessária para uma boa operação do sistema. No entanto, usuários normais (exemplo, desktop e notebooks) não precisam disso e podem desabilitá-la.

Para desabilitar temporizadores watchdog (ambos em software e hardware), adicione `nowatchdog` para seus parâmetros de inicialização.

Para verificar a nova configuração, execute:

```
# cat /proc/sys/kernel/watchdog

```

ou use:

```
# wdctl

```

Depois que você desabilitou os watchdogs, você pode *opcionalmente* evitar o carregamento do módulo responsável pelo watchdog de hardware, também. Faã isso ao [blacklisting](/index.php/Blacklisting "Blacklisting") do módulo relacionado, exemplo `iTCO_wdt`.

**Nota:** Alguns usuários [reportaram](https://bbs.archlinux.org/viewtopic.php?id=221239) que o parâmetro `nowatchdog` não funciona como esperado mas eles desabilitaram com sucesso (ao menos o de hardware) ao colocar o módulo citado acima no blacklist.

Qualquer ação vai aumentar a acelerar a inicialização e desligar a máquina, devido a ser um módulo a menos carregado. Também, desabilitar temporizadores do watchdog aumenta a performance e [abaixa o consumo de energia](/index.php/Power_management#Disabling_NMI_watchdog "Power management").

Veja [[3]](https://bbs.archlinux.org/viewtopic.php?id=163768), [[4]](https://bbs.archlinux.org/viewtopic.php?id=165834), [[5]](http://0pointer.de/blog/projects/watchdog.html), e [[6]](https://www.kernel.org/doc/Documentation/watchdog/watchdog-parameters.txt) para mais informações.

## Veja também

*   [Red Hat Performance Tuning Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Performance_Tuning_Guide/index.html)
*   [Linux Performance Measurements using vmstat](https://www.thomas-krenn.com/en/wiki/Linux_Performance_Measurements_using_vmstat)