**Status de tradução:** Esse artigo é uma tradução de [Improving performance](/index.php/Improving_performance "Improving performance"). Data da última tradução: 2020-01-26\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Improving_performance&diff=0&oldid=596231) na versão em inglês.

Artigos relacionados

*   [Improving performance/Boot process](/index.php/Improving_performance/Boot_process "Improving performance/Boot process")
*   [Pacman/Dicas e truques#Desempenho](/index.php/Pacman/Dicas_e_truques#Desempenho "Pacman/Dicas e truques")
*   [OpenSSH#Speeding up SSH](/index.php/OpenSSH#Speeding_up_SSH "OpenSSH")
*   [Openoffice#Speed up OpenOffice](/index.php/Openoffice#Speed_up_OpenOffice "Openoffice")
*   [Laptop](/index.php/Laptop "Laptop")
*   [Preload](/index.php/Preload_(Portugu%C3%AAs) "Preload (Português)")

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
    *   [2.5 Escalonador de entrada/saída](#Escalonador_de_entrada/saída)
        *   [2.5.1 Informações básicas](#Informações_básicas)
        *   [2.5.2 Os algoritmos de escalonamento de processos](#Os_algoritmos_de_escalonamento_de_processos)
        *   [2.5.3 Escalonadores de E/S do kernel](#Escalonadores_de_E/S_do_kernel)
        *   [2.5.4 Mudando o escalonador de E/S](#Mudando_o_escalonador_de_E/S)
        *   [2.5.5 Otimizando o escalonador de E/S](#Otimizando_o_escalonador_de_E/S)
    *   [2.6 Configuração de gerenciamento de energia](#Configuração_de_gerenciamento_de_energia)
    *   [2.7 Reduzir leituras/escritas no disco](#Reduzir_leituras/escritas_no_disco)
        *   [2.7.1 Mostrar escritas no disco](#Mostrar_escritas_no_disco)
        *   [2.7.2 Realocar arquivos para tmpfs](#Realocar_arquivos_para_tmpfs)
        *   [2.7.3 Sistema de arquivos](#Sistema_de_arquivos)
        *   [2.7.4 Espaço swap](#Espaço_swap)
        *   [2.7.5 Intervalo de writeback e tamanho do buffer](#Intervalo_de_writeback_e_tamanho_do_buffer)
    *   [2.8 Agendando tarefas de E/S com ionice](#Agendando_tarefas_de_E/S_com_ionice)
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
*   [5 RAM e swap](#RAM_e_swap)
    *   [5.1 Tempos e frequência de clock](#Tempos_e_frequência_de_clock)
    *   [5.2 Raiz na RAM](#Raiz_na_RAM)
    *   [5.3 Zram ou zswap](#Zram_ou_zswap)
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

*   Se o carregamento da CPU é consistemente alto até mesmo com bastante RAM disponível, tente diminuir o uso da CPU ao desabilitar [daemons](/index.php/Daemons_(Portugu%C3%AAs) "Daemons (Português)") que estão rodando e/ou processos. Isto pode ser monitorado de algumas formas, por exemplo com [htop](https://www.archlinux.org/packages/?name=htop), `pstree` ou qualquer outra ferramenta de [monitoração do sistema](/index.php/List_of_applications#System_monitors "List of applications"):

```
$ htop

```

*   Se aplicações usam renderização direta estão lentas (exemplo, estas que usam a GPU, tais como players de vídeo, jogos, ou até mesmo um [gerenciador de janelas](/index.php/Gerenciador_de_janela "Gerenciador de janela")), então melhorar o desempenho da GPU deve ajudar. O primeiro passo é verificar se a renderização direta está habilitada. Isto é indicado pelo comando `glxinfo`, parte do pacote [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos):

 `$ glxinfo | grep "direct rendering"` 
```
direct rendering: Yes

```

*   Ao usar um [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop"), desabilitar efeitos visuais (não usados) pode reduzir o uso da GPU. Use um ambiente mais leve ou crie um [personalizado](/index.php/Ambientes_de_desktop#Ambientes_personalizados "Ambientes de desktop"), se o atual não é compatível com seu hardware e/ou preferências pessoais.

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

### Escalonador de entrada/saída

#### Informações básicas

O escalonador (*scheduler*) de entrada/saída *(E/S)* (*input/output* ou *I/O*, em inglês) é o componente do kernel que decide em que ordem as operações de bloco de E/S são submetidas para dispositivos de armazenamento. É útil se lembrar de algumas especificações dos dois principais tipos de unidades de armazenamento devido ao objetivo do escalonador de E/S, que é otimizar a maneira de lidar com os pedidos de leitura:

*   Um HDD tem discos giratórios e uma cabeça que se move fisicamente para a localização solicitada. Latência randômica é muito alta estando entre 3 e 12ms (não importando se é um dispositivo de armazenamento de um servidor de última geração ou de notebook e ignorando o buffer de escrita controlador do disco) enquanto o acesso sequencial oferece uma taxa de transferência muito maior. O HDD típico faz em torno de 200 operações de E/S por segundo (*IOPS*, I/O operations per second).

*   Um SSD não tem partes móveis, acesso randômico é tão rápido quanto sequencial, tipicamente abaixo de 0.1ms, e pode manusear múltiplas solicitações concorrentes. A velocidade de saída do SSD típico é maior que 10.000 IOPS, que é mais do que o necessário para situações comuns de grande trabalho.

Se existem muitos processos fazendo solicitações de E/S para diferentes partes do armazenamento, milhares de IOPS podem ser gerados enquanto o HDD típico pode manusear em torno de somente 200 IOPS. Existe uma fila de solicitações que terão de esperar para acessar o disco. Esta situação é onde escalonadores de E/S entram com a tarefa de otimização.

#### Os algoritmos de escalonamento de processos

Uma maneira de melhorar a taxa de transferência é linearizar o acesso: ao ordenar as solicitações ociosas por seu endereço lógico e agrupar os mais próximos. Historicamente isto foi o primeiro escalonador de E/S chamado [elevator](https://en.wikipedia.org/wiki/Elevator_algorithm "wikipedia:Elevator algorithm") (elevador).

Um problema com o algoritmo *elevator* é sua falta de otimização para processos que fazem acessos sequenciais: lê um bloco de dados, o processa por alguns microssegundos, e então vai para o próximo. O *elevator* não sabe que o processo vai ler outro bloco próximo e, então, vai para a próxima solicitação de outro processo em outra localização. O escalonador de E/S [anticipatory](https://en.wikipedia.org/wiki/Anticipatory_scheduling "wikipedia:Anticipatory scheduling") (antecipatório) supera este problema: pausa por alguns milissegundos em antecipação de outra operação de leitura próxima antes de lidar com outras solicitações.

Enquanto estes escalonadores tentam melhorar a taxa de transferência total, eles podem deixar algumas solicitações sem sorte em espera por um longo período de tempo. Por exemplo, imagine que a maioria do processos fazem solicitações no começo do espaço de armazenamento enquanto um processo sem sorte faz um no final do espaço. O processo pode potencialmente ser adiado infinitamente, isto é chamado de inanição ou "starvation", em inglês. Pensando nesse problema, o algoritmo de [deadline](https://en.wikipedia.org/wiki/Deadline_scheduler "wikipedia:Deadline scheduler") foi desenvolvido. Existe uma fila ordenada por endereço, similar ao *elevator*, mas se a solicitação fica em espera por muito tempo, ela é movida para a fila "expired", ordenada pelo tempo de expiração. O escalonador verifica a fila "expired" primeiro e processa os seus pedidos e somente então vai para a fila *elevator*. Note que isto tem um efeito negativo na taxa de transferência geral.

O [Completely Fair Queuing *(CFQ)*](https://en.wikipedia.org/wiki/CFQ "wikipedia:CFQ") (fila completamente justa) aborda o problema diferentemente ao alocar um período fixo de tempo e um número de solicitações permitidas por vez dependendo da prioridade do processo submetendo elas. Suporta o [cgroup](/index.php/Cgroup "Cgroup") que permite a reserva de alguma quantidade de E/S para um grupo específico de processos. É particularmente útil para hosting compartilhado e nuvem: usuários que pagam por alguns IOPS querem sua parte quando necessários. Além disso, ele fica ocioso no final da E/S síncrona, aguardando outras operações próximas, assumindo esse recurso do escalonador *anticipatory* e trazendo algumas melhorias. Ambos, *anticipatory* e *elevator* foram descomissionados do kernel Linux e substituídos pelas alternativas mais avançadas apresentadas nesta seção.

O [Budget Fair Queuing *(BFQ)*](https://algo.ing.unimo.it/people/paolo/disk_sched/) (carteira de fila justa) é baseado no código do CFQ e trás algumas melhorias. Não garante o disco para cada processo por um período fixo de tempo mas uma "budget" (carteira) mensurada no número de setores para os processos e usa heurísticas. É relativamente complexo, pode ser mais adaptado a unidades de armazenamento rotacionais e SSDs lentos por causa de seu alto uso de recursos por operação, especialmente se associado com uma CPU lenta, pode diminuir o desempenho de dispositivos rápidos. O objetivo do BFQ em sistemas pessoais é esse, em tarefas interativas, o dispositivo de armazenamento é virtualmente tão responsivo quanto se estivesse ocioso. Na configuração padrão se foca em entregar a latência mais baixa do que a taxa de transferência máxima.

[Kyber](https://lwn.net/Articles/720675/) é um escalonador recente inspirado pelas técnicas de gerenciamento ativo de fila usado para roteamento de rede. A implementação é baseada em "tokens" que servem como um mecanismo para limitar solicitações. Um token de fila é necessário para alocar uma solicitação, para prevenir a inanição de solicitações. Um token de despacho é também necessário e limita as operações de certa prioridade para dado dispositivo. Finalmente, uma latência alvo de leitura é definida e o escalonador se otimiza para chegar nela. A implementação do algoritmo é relativamente simples e é considerada eficiente para dispositivos rápidos.

#### Escalonadores de E/S do kernel

Enquanto alguns algoritmos iniciais já foram descomissionados, o kernel oficial do Linux suporta um número de escalonadores de E/S que podem ser divididos em duas categorias:

*   Os **multi-queue schedulers** (escalonadores de filas múltiplas) estão disponíveis por padrão no kernel. O [Multi-Queue Block I/O Queuing Mechanism *(blk-mq)*](https://www.thomas-krenn.com/en/wiki/Linux_Multi-Queue_Block_IO_Queueing_Mechanism_(blk-mq)), em português mecanismo de empilhamento de blocos de E/S de várias filas, mapeia solicitações de E/S para múltiplas filas, as tarefas são distribuídas pelas threads, e consequentemente, núcleos da CPU. Os seguintes escalonadores estão disponíveis:

*   *   *None*, nenhum algoritmo de fila é aplicado.
    *   *mq-deadline* é o algoritmo do escalonador "deadline" para multithreads.
    *   *Kyber*
    *   *BFQ*

*   Os **single-queue schedulers** (escalonadores de única fila) são datados, eles podem ser ativados na inicialização como descritos em [#Mudando o escalonador de E/S](#Mudando_o_escalonador_de_E/S):
    *   [NOOP](https://en.wikipedia.org/wiki/NOOP_scheduler "wikipedia:NOOP scheduler") é o escalonador mais simples, ele insere todas as solicitações que chegam em uma simples fila FIFO e implementa a sua execução. Neste algoritmo, não existe reordenação da solicitação baseada no número do setor. Ela pode ser feita em outra camada, por exemplo no nível do dispositivo, ou se isto não importa, ignorada como em SSDs.
    *   *Deadline*
    *   *CFQ*

**Nota:** escalonadores de fila única [foram removidos do kernel desde o Linux 5.0](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=f382fb0bcef4c37dc049e9f6963e3baf204d815c).

#### Mudando o escalonador de E/S

**Nota:**

*   O modo do bloco de filas múltiplas *(blk-mq)* deve ser desabilitado na inicialização para ser possível usar os escalonadores datados *CFQ* e *Deadline*. Isto é feito ao adicionar `scsi_mod.use_blk_mq=0` nos [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel"). Os escalonadores de múltiplas filas não estão mais disponíveis neste modo.
*   A melhor escolha de qual escalonador usar depende de ambos, o dispositivo e o que vai ser utilizado. Também, a taxa de transferência em MB/s não é o único fator para mensurar o desempenho: tempo limite ou igualdade para processos pioram a taxa de transferência geral mas podem melhorar a responsividade do sistema. Fazer [benchmark](/index.php/Benchmarking "Benchmarking") pode ser útil para indicar o desempenho de cada escalonador de E/S.

Para listar os escalonadores disponíveis para um dispositivo e o atualmente ativo (em colchetes):

 `$ cat /sys/block/***sda***/queue/scheduler` 
```
mq-deadline kyber [bfq] none

```

Para listar os escalonadores disponíveis para todos os dispositivos:

 `$ cat /sys/block/*****/queue/scheduler` 
```
none
[mq-deadline] kyber bfq none
mq-deadline kyber [bfq] none

```

Para mudar o escalonador ativo para *bfq* no dispositivo *sda*, execute:

```
# echo ***bfq*** > /sys/block/***sda***/queue/scheduler

```

O processo para mudar o escalonador de E/S, dependendo se o disco é rotativo ou não, pode ser automatizado e persistir entre reinicializações. Por exemplo a regra do [udev](/index.php/Udev "Udev") abaixo define o escalonador como *none* para [NVMe](/index.php/NVMe "NVMe"), *mq-deadline* para [SSD](/index.php/SSD "SSD")/eMMC, e *bfq* para unidades de armazenamento rotativas:

 `/etc/udev/rules.d/60-ioschedulers.rules` 
```
# define o escalonador para NVMe
ACTION=="add|change", KERNEL=="nvme[0-9]*", ATTR{queue/scheduler}="none"
# define o escalonador para SSD e eMMC
ACTION=="add|change", KERNEL=="sd[a-z]|mmcblk[0-9]*", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="mq-deadline"
# define o escalonador para discos rotativos
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="1", ATTR{queue/scheduler}="bfq"
```

Reinicie ou force o udev a [carregar as novas regras](/index.php/Udev#Loading_new_rules "Udev").

#### Otimizando o escalonador de E/S

Cada um dos escalonadores de E/S do kernel tem suas próprias variáveis modificáveis, tais como tempo de latência, tempo de expiração ou parâmetros FIFO. Eles ajudam a ajustar o algoritmo para uma combinação particular do dispositivo e carga de trabalho. Isto é tipicamente usado para conseguir uma maior taxa de transferência ou diminuir a latência.

As variáveis modificáveis e suas descrições podem ser encontradas dentro dos [arquivos da documentação do kernel](https://www.kernel.org/doc/Documentation/block/).

Para listar as váriaveis modificáveis para um dispositivo, no exemplo abaixo é usado o *sdb* que está usando o *deadline*, execute:

 `$ ls /sys/block/***sdb***/queue/iosched` 
```
fifo_batch  front_merges  read_expire  write_expire  writes_starved

```

Para melhorar a taxa de transferência do *deadline* ao custo de latência, você pode aumentar o `fifo_batch` com o comando:

 `# echo *32* > /sys/block/***sdb***/queue/iosched/**fifo_batch**` 

### Configuração de gerenciamento de energia

Ao lidar com discos rotacionais tradicionais (HDDs) você pode querer [diminuir ou desabilitar funcionalidades de economia de energia](/index.php/Hdparm#Power_management_configuration "Hdparm") completamente.

### Reduzir leituras/escritas no disco

Evitar acessos desnecessários em unidades de armazenamento lentas é bom para a performance e também aumenta a vida útil dos dispositivos, apesar que em hardware moderno a diferença é normalmente insignificante.

**Nota:** Um SSD de 32GB com um fator medíocre de amplificação de escrita em 10 vezes, um padrão de 10000 ciclos de escrever/apagar, e **10GB de dados escritos por dia**, deve lhe dar uma **expectativa de vida útil de 8 anos**. Isto melhora com SSDs maiores e controladores modernos com menos amplificação de escrita. Também compare [[1]](http://techreport.com/review/25889/the-ssd-endurance-experiment-500tb-update) ao considerar se qualquer estratégia particular para limitar escritas no disco é, de verdade, necessária.

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

### Agendando tarefas de E/S com ionice

Muitas tarefas como backup não dependem de um pequeno atraso de E/S ou uma grande banda de armazenamento de E/S para seu objetivo, eles podem ser classificados como tarefas de segundo plano. O E/S rápido é necessário para boa responsividade da interface do usuário no desktop. Então, é benéfico reduzir a quantidade de banda de armazenamento disponível para tarefas de segundo plano, enquanto outras precisam de prioridade. Isto pode ser alcançado ao fazer uso do escalonador de E/S CFQ do linux, que permite configurar diferentes prioridades para os processos.

A prioridade de E/S de um processo de segundo plano pode ser reduzida para o nível "idle" (ocioso) com o comando:

```
# ionice -c 3 *seu_comando_aqui*

```

Veja [ionice(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ionice.1) e [[2]](https://www.cyberciti.biz/tips/linux-set-io-scheduling-class-priority.html) para mais informação.

## CPU

### Overclocking

[Overclocking](https://en.wikipedia.org/wiki/Overclocking "wikipedia:Overclocking") melhora a performance computacional da CPU ao aumentar o pico da frequência do clock. A habilidade para fazer overclock depende da combinação do modelo da CPU e placa-mãe. É mais frequentemente feito através da BIOS. Fazer overclock também tem desvantagens e riscos, não é nem recomendado nem desencorajado aqui.

Muitos chips da Intel não vão reportar corretamente a frequência do clock para acpi_cpufreq e a maioria dos utilitários. Isto resulta em excessivas mensagens no dmesg, que podem ser evitados ao descarregar ou colocar o módulo do kernel `apcu_cpufreq` na blacklist. Para ler a velocidade do seu clock, use *i7z* do pacote [i7z](https://www.archlinux.org/packages/?name=i7z). Para verificar se a CPU com overclock está operando corretamente, é recomendado fazer um [teste de estresse](/index.php/Stress_testing "Stress testing").

### Escala de frequência

Veja [Escala de frequência do CPU](/index.php/Escala_de_frequ%C3%AAncia_do_CPU "Escala de frequência do CPU").

### Escalonadores alternativos da CPU

O escalonador padrão da CPU que está na mainline do kernel Linux é o [CFS](https://en.wikipedia.org/wiki/Completely_Fair_Scheduler "wikipedia:Completely Fair Scheduler"). Existem alternativas.

Um escalonador alternativo focado na interatividade e responsividade é o [MuQSS](http://ck.kolivas.org/patches/muqss/sched-MuQSS.txt), desenvolvido por [Con Kolivas](http://users.tpg.com.au/ckolivas/kernel/). MuQSS está incluído no pacote do kernel [linux-zen](https://www.archlinux.org/packages/?name=linux-zen). Está também disponível como um patch independente ou como parte do conjunto de patches **-ck**. Veja [Linux-ck](/index.php/Linux-ck "Linux-ck") and [Linux-pf](/index.php/Linux-pf "Linux-pf") para mais informações sobre.

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

Desligar as mitigações de falhas da CPU melhoram o desempenho (algumas vezes mais de 50%). Use o [parâmetro do kernel](/index.php/Par%C3%A2metro_do_kernel "Parâmetro do kernel") abaixo para desabilitá-las:

```
mitigations=off

```

A explicação de todos os switches que são passados está no [kernel.org](https://www.kernel.org/doc/html/latest/admin-guide/kernel-parameters.html). Você pode usar [spectre-meltdown-checker](https://aur.archlinux.org/packages/spectre-meltdown-checker/) para checar vulnerabilidade.

## Gráficos

### Configuração do Xorg

O desempenho gráfico pode depender das configurações presentes no [xorg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5); veja os artigos da [NVIDIA](/index.php/NVIDIA "NVIDIA"), [ATI](/index.php/ATI "ATI"), [AMDGPU](/index.php/AMDGPU "AMDGPU") e [Intel](/index.php/Intel "Intel"). Configurações erradas podem fazer o Xorg deixar de funcionar, tome cuidado.

### Configuração do Mesa

O desempenho dos drivers Mesa pode ser configurado com [drirc](https://dri.freedesktop.org/wiki/ConfigurationInfrastructure/). As seguintes ferramentas gráficas estão disponíveis:

*   **adriconf (Advanced DRI Configurator)** — Ferramenta gráfica para configurar os drivers Mesa ao definir opções e escrevê-las para o arquivo drirc padrão.

	[https://github.com/jlHertel/adriconf/](https://github.com/jlHertel/adriconf/) || [adriconf](https://www.archlinux.org/packages/?name=adriconf)

*   **DRIconf** — Applet de configuração para Direct Rendering Infrastructure, DRI (Inflaestrutura de Renderização Direta, em português). Permite customizar o desempenho e configurações da qualidade visual dos drivers OpenGL em um nível por unidade de armazenamento, por tela e/ou por aplicação.

	[https://dri.freedesktop.org/wiki/DriConf/](https://dri.freedesktop.org/wiki/DriConf/) || [driconf](https://aur.archlinux.org/packages/driconf/)

### Overclocking

Assim como acontece com CPUs, overclocking pode diretamente melhorar o desempenho, mas geralmente não é recomendado. Existem pacotes no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), tais como [amdoverdrivectrl](https://aur.archlinux.org/packages/amdoverdrivectrl/) (placas antigas da AMD/ATI), [rocm-smi](https://aur.archlinux.org/packages/rocm-smi/) (placas recentes da AMD), [nvclock](https://aur.archlinux.org/packages/nvclock/) (placas antigas da NVIDIA - até o Geforce 9), e [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) para placas recentes da NVIDIA.

Veja [AMDGPU#Overclocking](/index.php/AMDGPU#Overclocking "AMDGPU") ou [NVIDIA/Tips and tricks#Enabling overclocking](/index.php/NVIDIA/Tips_and_tricks#Enabling_overclocking "NVIDIA/Tips and tricks").

## RAM e swap

### Tempos e frequência de clock

A RAM pode rodar em diferentes tempos e clock, isto pode ser configurado na BIOS. O desempenho da memória depende de ambos os valores. Selecionar o valor mais alto presente na BIOS normalmente melhora o desempenho em comparação com o valor padrão. Note que aumentar a frequência para valores maiores que os suportados pelos fabricantes da placa-mãe e RAM é overclocking, riscos e desvantagens similares se aplicam nesse caso, veja [#Overclocking](#Overclocking).

### Raiz na RAM

Se está usando um dispositivo com lenta capacidade de escrita (USB, HDDs rotativos) e os requerimentos de armazenamento são baixos, a raiz pode rodar na RAM em cima de uma raiz somente leitura (no disco). Isto pode aumentar significamente o desempenho ao custo de um limitado espaço modificável na raiz do sistema. Veja [liveroot](https://aur.archlinux.org/packages/liveroot/).

### Zram ou zswap

O módulo [zram](https://www.kernel.org/doc/Documentation/blockdev/zram.txt) do kernel (antigamente chamado de **compcache**) oferece um dispositivo de bloco comprimido na RAM. Se você usa isto como um dispositivo swap, A RAM pode guardar muito mais informações mas usa mais CPU. Apesar disso, é muito mais rápido que usar um disco rígido. Se um sistema regularmente recorre a swap, isto pode aumentar a responsibilidade. Usar zram é também uma boa maneira de reduzir ciclos de leitura/escrita no disco que ocorrem por causa da swap em SSDs.

Benefícios similares (em custos similares) podem ser alcançados usando [zswap](/index.php/Zswap "Zswap"). Os dois são geralmente similares em intenção mas não em implementação: zswap opera como um cache da RAM comprimida e nem precisa (nem permite) extensiva configuração no userspace.

Exemplo: Para definir um dispositivo zram com capacidade de 32GiB, comprimido com lz4 e prioridade maior que o normal (somente para a atual sessão):

```
# modprobe zram
# echo lz4 > /sys/block/zram0/comp_algorithm
# echo 32G > /sys/block/zram0/disksize
# mkswap --label zram0 /dev/zram0
# swapon --priority 100 /dev/zram0

```

Para desabilitá-lo, reinicie o sistema ou execute:

```
# swapoff /dev/zram0
# rmmod zram

```

Uma explicação detalhada de todos os passos, opções e potenciais problemas pode ser encontrada na documentação oficial do [módulo](https://www.kernel.org/doc/Documentation/blockdev/zram.txt).

O pacote [systemd-swap](https://www.archlinux.org/packages/?name=systemd-swap) oferece a unit `systemd-swap.service` para automaticamente inicializar dispositivos zram. É possível configurar em `/etc/systemd/swap.conf`.

O pacote [zramswap](https://aur.archlinux.org/packages/zramswap/) oferece um script automatizado para configurar tais dispositivos swap com configurações ideais para seu sistema (tais como tamanho da RAM e número de núcleos da CPU). O script cria um dispositivo zram por núcleo da CPU com um espaço total equivalente a RAM disponível, então você vai ter uma swap comprimida com uma prioridade maior que a swap normal, que vai utilizar múltiplos núcleos da CPU para os dados comprimidos. Para fazer isto automaticamente em toda inicialização, [habilite](/index.php/Habilite "Habilite") o `zramswap.service`.

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

De acordo com [Wikipedia:Watchdog timer](https://en.wikipedia.org/wiki/Watchdog_timer "wikipedia:Watchdog timer") (traduzido):

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

Depois que você desabilitou os watchdogs, você pode *opcionalmente* evitar o carregamento do módulo responsável pelo watchdog de hardware, também. Faça isso com o módulo relacionado [adicionando-o em lista-negra](/index.php/Kernel_module_(Portugu%C3%AAs)#Adicionar_um_módulo_em_uma_lista-negra_(Blacklisting) "Kernel module (Português)"), exemplo `iTCO_wdt`.

**Nota:** Alguns usuários [reportaram](https://bbs.archlinux.org/viewtopic.php?id=221239) que o parâmetro `nowatchdog` não funciona como esperado mas eles desabilitaram com sucesso (ao menos o de hardware) ao colocar o módulo citado acima no blacklist.

Qualquer ação vai aumentar a acelerar a inicialização e desligar a máquina, devido a ser um módulo a menos carregado. Também, desabilitar temporizadores do watchdog aumenta a performance e [abaixa o consumo de energia](/index.php/Power_management#Disabling_NMI_watchdog "Power management").

Veja [[3]](https://bbs.archlinux.org/viewtopic.php?id=163768), [[4]](https://bbs.archlinux.org/viewtopic.php?id=165834), [[5]](http://0pointer.de/blog/projects/watchdog.html), e [[6]](https://www.kernel.org/doc/Documentation/watchdog/watchdog-parameters.txt) para mais informações.

## Veja também

*   [Red Hat Performance Tuning Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Performance_Tuning_Guide/index.html)
*   [Linux Performance Measurements using vmstat](https://www.thomas-krenn.com/en/wiki/Linux_Performance_Measurements_using_vmstat)