**Status de tradução:** Esse artigo é uma tradução de [LVM](/index.php/LVM "LVM"). Data da última tradução: 2020-01-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=LVM&diff=0&oldid=595401) na versão em inglês.

Related articles

*   [Software RAID and LVM](/index.php/Software_RAID_and_LVM "Software RAID and LVM")
*   [LUKS dentro do LVM](/index.php/Dm-crypt_(Portugu%C3%AAs)/Encrypting_an_entire_system_(Portugu%C3%AAs)#LUKS_dentro_do_LVM "Dm-crypt (Português)/Encrypting an entire system (Português)")
*   [Resizing LVM-on-LUKS](/index.php/Resizing_LVM-on-LUKS "Resizing LVM-on-LUKS")
*   [Create root filesystem snapshots with LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM")

Da [Wikipedia:Logical Volume Manager (Linux)](https://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux) "wikipedia:Logical Volume Manager (Linux)"):

	LVM é um [gerenciador de volume lógico](https://en.wikipedia.org/wiki/logical_volume_management "wikipedia:logical volume management") para o [Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel "wikipedia:Linux kernel"); ele gerencia unidades de disco e dispositivos de armazenamento em massa ou similares.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Conceitos básicos](#Conceitos_básicos)
    *   [1.1 Construção em blocos do LVM](#Construção_em_blocos_do_LVM)
    *   [1.2 Vantagens](#Vantagens)
    *   [1.3 Desvantagens](#Desvantagens)
    *   [1.4 Introdução](#Introdução)
        *   [1.4.1 Configuração por interface gráfica](#Configuração_por_interface_gráfica)
*   [2 Instalando Arch Linux em LVM](#Instalando_Arch_Linux_em_LVM)
*   [3 Operações com volumes](#Operações_com_volumes)
    *   [3.1 Volumes físicos](#Volumes_físicos)
        *   [3.1.1 Aumentando](#Aumentando)
        *   [3.1.2 Diminuindo](#Diminuindo)
            *   [3.1.2.1 Mover extensões físicas](#Mover_extensões_físicas)
            *   [3.1.2.2 Redimensionar volumes físicos](#Redimensionar_volumes_físicos)
            *   [3.1.2.3 Redimensionar partição](#Redimensionar_partição)
    *   [3.2 Grupos de volumes](#Grupos_de_volumes)
        *   [3.2.1 Ativando um grupo de volume](#Ativando_um_grupo_de_volume)
        *   [3.2.2 Reparando um grupo de volumes](#Reparando_um_grupo_de_volumes)
        *   [3.2.3 Desativando um grupo de volumes](#Desativando_um_grupo_de_volumes)
        *   [3.2.4 Renomeando um grupo de volumes](#Renomeando_um_grupo_de_volumes)
        *   [3.2.5 Adicionar um volume físico a um grupo de volumes](#Adicionar_um_volume_físico_a_um_grupo_de_volumes)
        *   [3.2.6 Remover partições de um grupo de volumes](#Remover_partições_de_um_grupo_de_volumes)
    *   [3.3 Volumes lógicos](#Volumes_lógicos)
        *   [3.3.1 Renomeando um volume lógico](#Renomeando_um_volume_lógico)
        *   [3.3.2 Redimensionando volumes lógicos e sistemas de arquivos de uma só vez](#Redimensionando_volumes_lógicos_e_sistemas_de_arquivos_de_uma_só_vez)
        *   [3.3.3 Redimensionar volume lógico e sistema de arquivos separadamente](#Redimensionar_volume_lógico_e_sistema_de_arquivos_separadamente)
        *   [3.3.4 Removendo um volume lógico](#Removendo_um_volume_lógico)
*   [4 Tipos de volume lógico](#Tipos_de_volume_lógico)
    *   [4.1 Snapshots](#Snapshots)
        *   [4.1.1 Configuração](#Configuração)
    *   [4.2 Cache LVM](#Cache_LVM)
        *   [4.2.1 Criar cache](#Criar_cache)
        *   [4.2.2 Remover cache](#Remover_cache)
    *   [4.3 RAID](#RAID)
        *   [4.3.1 Configurando RAID](#Configurando_RAID)
        *   [4.3.2 Configurar mkinitcpio para RAID](#Configurar_mkinitcpio_para_RAID)
*   [5 Solução de problemas](#Solução_de_problemas)
    *   [5.1 Problemas de inicialização/desligamento causam a desativação de lvmetad](#Problemas_de_inicialização/desligamento_causam_a_desativação_de_lvmetad)
    *   [5.2 Comandos LVM não funcionam](#Comandos_LVM_não_funcionam)
    *   [5.3 Volumes lógicos não são exibidos](#Volumes_lógicos_não_são_exibidos)
    *   [5.4 LVM em mídia removível](#LVM_em_mídia_removível)
        *   [5.4.1 Suspensão/retorno com LVM e mídia removível](#Suspensão/retorno_com_LVM_e_mídia_removível)
    *   [5.5 O redimensionamento de um volume lógico falha](#O_redimensionamento_de_um_volume_lógico_falha)
    *   [5.6 Comando "grub-mkconfig" reporta o erro "unknown filesystem"](#Comando_"grub-mkconfig"_reporta_o_erro_"unknown_filesystem")
    *   [5.7 Tempo esgotado em volumes de dispositivos da raiz](#Tempo_esgotado_em_volumes_de_dispositivos_da_raiz)
    *   [5.8 Demora no desligamento](#Demora_no_desligamento)
*   [6 Veja também](#Veja_também)

## Conceitos básicos

### Construção em blocos do LVM

O gerenciador de volumes lógicos (LVM) utiliza um recurso do kernel chamado [device-mapper](http://sources.redhat.com/dm/) (mapeador de dispositivo) para fornecer um sistema de partições independente do leiaute subjacente do disco. Com o LVM, você abstrai seu dispositivo de armazenamento e passa a ter "partições virtuais", tornando a tarefa de [estender/diminuir](#Redimensionar_volume_lógico_e_sistema_de_arquivos_separadamente) volumes mais fácil (embora isto esteja sujeito a potenciais limitações do sistema de arquivos).

Partições virtuais permitem adição e remoção sem a preocupação de haver ou não espaço contíguo em um disco em particular, como por exemplo sendo impedido por fdisk fazendo uma varredura no disco (e imaginando se o kernel está usando a tabela de partições nova ou velha), ou ainda, tendo que mover eventuais partições próximas para outra região ao longo do disco.

Construção básico dos blocos do LVM:

	Volume físico (PV, do inglês *Phisical Volume*)

	um *node* de dispositivo em bloco Unix, usado para armazenamento pelo LVM. Exemplos: um disco rígido, uma [partição](/index.php/Parti%C3%A7%C3%A3o "Partição") MBR ou GPT, um arquivo de *loopback*, um mapeador de dispositivo (por exemplo, [dm-crypt](/index.php/Dm-crypt_(Portugu%C3%AAs) "Dm-crypt (Português)")). Ele grava um cabeçalho do LVM.

	Grupo de volume (VG, do inglês *Volume Group*)

	Grupo de PVs que servem como contêineres para LVs (volumes lógicos, de *Logical Volumes*). PEs (*Phisical Extents*, ou extensões físicas são alocadas de um VG para um LV.

	Volume lógico ou *Logical Volume* (LV)

	Uma partição virtual/lógica que reside em um VG e é composta de PEs. LVs são dispositivos de bloco Unix análogos a partições físicas, ou seja, podem ser diretamente formatadas com um [sistema de arquivos](/index.php/Sistema_de_arquivos "Sistema de arquivos").

	Extensão física ou *Physical Extent* (PE)

	A menor extensão física contígua (4 MiB, por padrão) em um PV que pode ser atribuída para um LV. Pense em PEs como sendo partes de PVs que possam ser alocadas para qualquer LV.

Exemplo:

```
Discos físicos

  Disco1 (/dev/sda):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partição1 50 GiB (Volume físico)    |Partição2 80 GiB (Volume físico)        |
    |/dev/sda1                           |/dev/sda2                               |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |

  Disco2 (/dev/sdb):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partição1 120 GiB (Volume físico)                    |
    |/dev/sdb1                                            |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|

```

```
Volumes lógicos do LVM

  Grupo de volumes1 (/dev/MeuGrupoDeVolumes/ = /dev/sda1 + /dev/sda2 + /dev/sdb1):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Volume lógico1 15 GiB          |Volume lógico2 35 GiB              |Volume lógico3 200 GiB           |
    |/dev/MeuGrupoDeVolumes/rootvol |/dev/MeuGrupoDeVolumes/homevol     |/dev/MeuGrupoDeVolumes/mediavol  |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _| _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|

```

### Vantagens

O LVM proporciona mais flexibilidade do que usar partições normais no disco rígido, pois permite:

*   Usar qualquer quantidade de discos como se fosse um único grande disco;
*   Ter volumes lógicos estendidos sobre vários discos;
*   Criar pequenos volumes lógicos e estendê-los "dinamicamente" à medida em que eles forem ficando cheios;
*   Redimensionar volumes lógicos independentemente da ordem que estão dispostos fisicamente no disco. Isto não depende da posição do LV dentro do VG, não havendo nem mesmo necessidade de liberar espaço disponível ao redor destes;
*   Redimensionar/criar/excluir volumes lógicos e físicos online. Os sistemas de arquivos neles ainda precisam ser redimensionados, mas alguns (como ext4) suportam redimensionamento online;
*   Migração de um LV em uso online/em tempo real por serviços de diferentes discos sem necessidade de reinicializar os serviços;
*   Criar *snapshots* que permitem backup completo do sistema de arquivos, minimizando o tempo de indisponibilidade dos serviços;
*   Usar vários alvos do mapeador de dispositivos incluindo criptografia transparente do sistema de arquivos e *cache* dados acessados frequentemente. Isto permite criar um sistema com (um ou mais) discos físicos (criptografados com LUKS) e [LVM por cima](/index.php/Dm-crypt_(Portugu%C3%AAs)/Encrypting_an_entire_system_(Portugu%C3%AAs)#LVM_dentro_do_LUKS "Dm-crypt (Português)/Encrypting an entire system (Português)") para permitir o fácil redimensionamento e gerenciamento de volumes separados (por exemplo, para `/`, `/home`, `/backup`, etc.) sem o incômodo de digitar uma senha várias vezes numa inicialização.

### Desvantagens

*   Etapas adicionais tornam o processo de configuração inicial do sistema mais complicado.
*   Em dual boot, note que o Windows não suporta LVM; o que impossibilita o acesso de quaisquer partições LVM à partir do Windows.

### Introdução

Certifique-se de ter [instalado](/index.php/Instalado "Instalado") o pacote [lvm2](https://www.archlinux.org/packages/?name=lvm2).

#### Configuração por interface gráfica

Não existe uma ferramenta "oficial" por interface gráfica para gerenciar volumes LVM, mas [system-config-lvm](https://aur.archlinux.org/packages/system-config-lvm/) cobre a maioria das operações comuns e fornece visualizações simples do estado do volume. Pode automaticamente redimensionar muitos tipos de sistemas de arquivos ao redimensionar volumes lógicos.

## Instalando Arch Linux em LVM

Veja [Instalando Arch Linux em LVM](/index.php/Installing_Arch_linux_on_LVM_(Portugu%C3%AAs) "Installing Arch linux on LVM (Português)")

## Operações com volumes

### Volumes físicos

Após estender ou antes de reduzir o tamanho de um dispositivo que possui um volume físico nele, você precisa aumentar ou diminuir o PV usando `pvresize`.

#### Aumentando

Para expandir o PV em `/dev/sda1` após aumentar a [partição](/index.php/Parti%C3%A7%C3%A3o "Partição"), execute:

```
# pvresize /dev/sda1

```

Isto irá automaticamente detectar o novo tamanho do dispositivo e estender o PV ao seu tamanho máximo.

**Nota:** Este comando pode ser feito enquanto o volume estiver online.

#### Diminuindo

Para diminuir um volume físico antes de reduzir seu dispositivo subjacente, adicione os parâmetros `--setphysicalvolumesize *tamanho*` ao comando, *exemplo*:

```
# pvresize --setphysicalvolumesize 40G /dev/sda1

```

O comando acima pode terminar com o seguinte erro:

```
 /dev/sda1: cannot resize to 25599 extents as later ones are allocated.
 0 physical volume(s) resized / 1 physical volume(s) not resized

```

De fato, `pvresize` irá se recusar a diminuir um PV se sua extensão física estiver *após* onde o seu novo final deveria estar. É preciso executar [pvmove](#Mover_extensões_físicas) antecipadamente para realocá-las em outro ponto do grupo de volumes onde houver espaço livre suficiente.

##### Mover extensões físicas

Antes de mover extensões físicas para o final do volume, é preciso executar `pvdisplay -v -m` para ver os segmentos de volume físico. No exemplo a seguir, existe um volume físico em `/dev/sdd1`, um grupo de volumes `vg1` e um volume lógico `backup`.

 `# pvdisplay -v -m` 
```
    Finding all volume groups.
    Using physical volume(s) on command line.
  --- Physical volume ---
  PV Name               /dev/sdd1
  VG Name               vg1
  PV Size               1.52 TiB / not usable 1.97 MiB
  Allocatable           yes 
  PE Size               4.00 MiB
  Total PE              399669
  Free PE               153600
  Allocated PE          246069
  PV UUID               MR9J0X-zQB4-wi3k-EnaV-5ksf-hN1P-Jkm5mW

  --- Physical Segments ---
  Physical extent 0 to 153600:
    FREE
  Physical extent 153601 to 307199:
    Logical volume	/dev/vg1/backup
    Logical extents	1 to 153599
  Physical extent 307200 to 307200:
    FREE
  Physical extent 307201 to 399668:
    Logical volume	/dev/vg1/backup
    Logical extents	153601 to 246068

```

Pode-se observar que o espaço livre está dividido pelo volume. Para diminuir o volume físico, precisamos primeiro mover todos os segmentos usados para o início.

Aqui, o primeiro segmento livre começa em 0 e vai até 153600 e nos deixa com 153601 de extensão livre. Podemos agora mover este número de segmento da última extensão física para a primeira extensão. O comando será assim:

 `# pvmove --alloc anywhere /dev/sdd1:307201-399668 /dev/sdd1:0-92467` 
```
/dev/sdd1: Moved: 0.1 %
/dev/sdd1: Moved: 0.2 %
...
/dev/sdd1: Moved: 99.9 %
/dev/sdd1: Moved: 100.0 %

```

**Note:**

*   este comando move 399668 - 307201 + 1 = 92468 PEs **do** último segmento **to** para o primeiro segmento. Isto é possível porque o primeiro segmento encerra 153600 PEs livres, cada qual contendo 92467 - 0 + 1 = 92468 PEs movidas.
*   a opção `--alloc anywhere` é usada pois queremos mover as PEs dentro da mesma partição. No caso de partições diferentes, o comando deveria ser algo como: `# pvmove /dev/sdb1:1000-1999 /dev/sdc1:0-999` 
*   este comando pode levar muito tempo (uma ou duas horas) no caso de volumes grandes. Pode ser uma boa idéia executar este comando em um [Tmux](/index.php/Tmux "Tmux") ou uma sessão [GNU Screen](/index.php/GNU_Screen "GNU Screen"). Qualquer parada indesejada no processo poderá ser fatal.
*   uma vez que a operação tenha terminado, execute [fsck](/index.php/Fsck_(Portugu%C3%AAs) "Fsck (Português)") para ter certeza de que seu sistema de arquivos é válido.

##### Redimensionar volumes físicos

Uma vez que todos os seus segmentos físicos estejam na última extensão física, execute `vgdisplay` e veja sua PE livre.

Você pode agora executar novamente o comando:

```
# pvresize --setphysicalvolumesize *tamanho* *PhysicalVolume*

```

Veja o resultado:

 `# pvs` 
```
  PV         VG   Fmt  Attr PSize    PFree 
  /dev/sdd1  vg1  lvm2 a--     1t     500g

```

##### Redimensionar partição

Finalmente, você deve diminuir a partição com sua [ferramenta de particionamento](/index.php/Partitioning_(Portugu%C3%AAs)#Ferramentas_de_particionamento "Partitioning (Português)") desejada.

### Grupos de volumes

#### Ativando um grupo de volume

**Nota:** Você pode restringir os volumes que serão ativados automaticamente definindo `auto_activation_volume_list` em `/etc/lvm/lvm.conf`. Em caso de dúvida, deixe esta opção comentada.

```
# vgchange -a y vg0

```

Isto irá reativar o grupo de volume. Se por exemplo você tiver uma falha em um dispositivo de espelhamento e tiver substituído a unidade, execute `pvcreate`, `vgextend` e `vgreduce --removemissing --force`.

#### Reparando um grupo de volumes

Para iniciar o procedimento de reconstrução de um espelhamento de uma matriz degrada nesse exemplo, você deveria executar:

```
# lvconvert --repair /dev/vg0/mirror

```

Você pode monitorar o processo de reconstrução (Cpy%Sync Column output) com:

```
# lvs -a -o +devices

```

#### Desativando um grupo de volumes

Apenas invoque

```
# vgchange -a n my_volume_group

```

Isto irá desativar o grupo de volumes e irá permitir que você desmonte o contêiner onde ele está armazenado.

#### Renomeando um grupo de volumes

Use o comando [vgrename(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vgrename.8) para renomear um grupo de volumes existente.

Qualquer um dos comandos a seguir é capaz de renomear um grupo de volumes existente `vg02` para `my_volume_group`

```
# vgrename /dev/vg02 /dev/my_volume_group

```

```
# vgrename vg02 my_volume_group

```

#### Adicionar um volume físico a um grupo de volumes

Você primeiro cria um novo volume físico no dispositivo que deseja usar, depois estende seu grupo de volumes:

```
# pvcreate /dev/sdb1
# vgextend VolGroup00 /dev/sdb1

```

Isto, é claro, irá aumentar o total de extensões físicas em seu grupo de volumes, podendo cada uma ser alocada por volumes lógicos como você achar melhor.

**Nota:** É uma boa prática ter uma [tabela de partição](/index.php/Partitioning_(Portugu%C3%AAs) "Partitioning (Português)") em sua mídia de armazenamento sob LVM. Use o código de tipo apropriado: `8e` para partições MBR, e `8e00` para partições GPT.

#### Remover partições de um grupo de volumes

Se você criou um volume lógico na partição, [remova-a](#Removendo_um_volume_lógico) primeiro.

Todos os dados na partição precisarão ser movidos para outra partição. Felizmente, o LVM torna isso fácil:

```
# pvmove /dev/sdb1

```

Se desejar ter os dados em um volume físico em particular, especifique-o como o segundo argumento para `pvmove`:

```
# pvmove /dev/sdb1 /dev/sdf1

```

Então o volume físico precisará ser removido do grupo de volumes:

```
# vgreduce myVg /dev/sdb1

```

Ou remover todos os volumes físicos vazios:

```
# vgreduce --all vg0

```

Por exemplo, se você tiver um disco ruim em um grupo que não pode ser encontrado por ter sido removido ou falhado:

```
# vgreduce --removemissing --force vg0

```

E finalmente, se desejar usar a partição para algo mais, e quiser prevenir que LVM considere que a partição é um volume físico:

```
# pvremove /dev/sdb1

```

### Volumes lógicos

**Nota:** [lvresize(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvresize.8) fornece mais ou menos as mesmas opções que os comandos especializados [lvextend(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvextend.8) e [lvreduce(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvreduce.8), enquanto permite fazer ambos os tipos de operação. Além disso, todos estes utilitários oferecem uma opção `-r`/`--resizefs` que permite redimensionar o sistema de arquivos juntamente com o LV usando [fsadm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsadm.8) (*ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS* e [XFS](/index.php/XFS "XFS") suportados). Portanto pode ser mais fácil apenas usar `lvresize` para ambas operações e usar `--resizefs` para simplificar um pouco as coisas, exceto se você tiver necessidades específicas ou quiser controle completo sobre o processo.

**Atenção:** Aumentar um sistema de arquivos é uma operação que muitas vezes pode ser feita online (isto é, enquanto estiver montado), mesmo para a partição raiz, já diminuir irá sempre requerer a desmontagem do sistema de arquivos para prevenir perda de dados. Certifique-se de que seu sistema de arquivos suporta o que estiver pretendendo fazer.

#### Renomeando um volume lógico

Para renomear um volume lógico existente, use o comando [lvrename(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvrename.8).

Qualquer um dos comandos a seguir irão renomear o volume lógico `lvold` no grupo de volumes de `vg02` para `lvnew`.

```
# lvrename /dev/vg02/lvold /dev/vg02/lvnew

```

```
# lvrename vg02 lvold lvnew

```

#### Redimensionando volumes lógicos e sistemas de arquivos de uma só vez

**Nota:** Somente os [sistemas de arquivos](/index.php/Sistemas_de_arquivos "Sistemas de arquivos") *ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS* e [XFS](/index.php/XFS "XFS") são suportados. Para diferentes tipos de sistemas de arquivos, veja [#Redimensionar volume lógico e sistema de arquivos separadamente](#Redimensionar_volume_lógico_e_sistema_de_arquivos_separadamente).

Estender o volume lógico `mediavol` em `MyVolGroup` por 10 GiB e redimensionar seu sistema de arquivos *tudo de uma vez*:

```
# lvresize -L +10G --resizefs MyVolGroup/mediavol

```

Definir o tamanho do volume lógico `mediavol` em `MyVolGroup` para 15 GiB e redimensionar seu sistema de arquivos *tudo de uma vez*:

```
# lvresize -L 15G --resizefs MyVolGroup/mediavol

```

Se desejar preencher todo o espaço livre em um grupo de volumes, use o seguinte comando:

```
# lvresize -l +100%FREE --resizefs MyVolGroup/mediavol

```

Veja [lvresize(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvresize.8) para opções mais detalhadas.

#### Redimensionar volume lógico e sistema de arquivos separadamente

Para sistemas de arquivos não suportados por [fsadm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsadm.8) será necessário usar um [utilitário apropriado](/index.php/File_systems_(Portugu%C3%AAs)#Tipos_de_sistemas_de_arquivos "File systems (Português)") para redimensionar o sistema de arquivos e diminuir o volume lógico, ou depois de expandí-lo.

Para estender o volume lógico `mediavol` contido no grupo de volumes `MyVolGroup` em 2 GiB *sem* tocar em seu sistema de arquivos:

```
# lvresize -L +2G MyVolGroup/mediavol

```

Agora, para expandir o sistema de arquivos ([ext4](/index.php/Ext4 "Ext4") neste exemplo) para o tamanho máximo do volume lógico subjacente:

```
# resize2fs /dev/MyVolGroup/mediavol

```

Para reduzir o tamanho do volume lógico `mediavol` contido em `MyVolGroup` em 500 MiB, primeiro calcule o tamanho do sistema de arquivos resultante, depois diminuir o sistema de arquivos ([ext4](/index.php/Ext4 "Ext4") neste exemplo) para o novo tamanho:

```
# resize2fs /dev/MyVolGroup/mediavol *NovoTamanho*

```

Quando o sistema de arquivos for diminuído, reduza o tamanho do volume lógico:

```
# lvresize -L -500M MyVolGroup/mediavol

```

Para calcular o tamanho exato do volume lógico para sistemas de arquivos *ext2*, [ext3](/index.php/Ext3 "Ext3") e [ext4](/index.php/Ext4 "Ext4"), use uma simples fórmula: `LVM_EXTENTS = FS_BLOCKS × FS_BLOCKSIZE ÷ LVM_EXTENTSIZE`.

 `# tune2fs -l /dev/MyVolGroup/mediavol | grep Block` 
```
Block count:              102400000
Block size:               4096
Blocks per group:         32768

```
 `# vgdisplay MyVolGroup | grep "PE Size"` 
```
PE Size               4.00 MiB

```

**Nota:** O tamanho do bloco no sistema de arquivos é dado em bytes. Certifique-se de usar a mesma unidade para ambos tamanho de bloco e extensão.

```
102400000 blocos × 4096 bytes/bloco ÷ 4 MiB/extensão = 100000 extensão total

```

Passando `--resizefs` irá confirmar que que está correto.

 `# lvreduce -l 100000 --resizefs /dev/MyVolGroup/mediavol` 
```
...
O sistema de arquivos tem atualmente 102400000 (4k) blocos. Nada a fazer!
...
O tamanho do volume lógico sysvg/root foi redimensionado com sucesso.

```

Veja [lvresize(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvresize.8) para opções mais detalhadas.

#### Removendo um volume lógico

**Atenção:** Antes de remover um volume lógico, certifique-se de mover todos os dados que desejar manter para outro lugar; caso contrário, serão perdidos!

Primeiro, encontre o nome do volume lógico que desejar remover. Pode-se obter a lista de volumes lógicos com:

```
# lvs

```

Depois, verifique o ponto de montagem do volume lógico escolhido:

```
$ lsblk

```

Então desmonte o sistema de arquivos do volume lógico:

```
# umount /<*ponto-de-montagem*>

```

Finalmente, remova o volume lógico:

```
# lvremove <*grupo_de_volumes*>/<*volume_logico*>

```

Por exemplo:

```
# lvremove VolGroup00/lvolhome

```

Confirme digitando `y`.

Atualize `/etc/fstab` conformece necessário.

Você poderá verificar a remoção do volume lógico digitando `lvs` como root novamente (veja o primeiro passo deste seção).

## Tipos de volume lógico

Além de volumes lógicos simples, LVM suporta snapshots, volumes lógicos de *cache*, volumes lógicos de provisionamento fino e RAID.

### Snapshots

O LVM permite tirar um *snapshot* de seu sistema de uma maneira muito mais eficiente do que um backup tradicional. Ele usa a técnica chamada COW (cópia em gravação, do inglês *copy-on-write*). O snapshot inicial tirado contém apontamentos aos *inodes* de seus dados atuais. Desde que seus dados permaneçam inalterados, o snapshot apenas irá conter ponteiros para seus *inodes* e não os dados propriamente ditos. Sempre que modificar um arquivo ou diretório para o qual o snapshot aponta, o LVM irá clonar os dados automaticamente, a cópia anterior será referenciada pelo snapshot, e a nova cópia referenciada pelo seu sistema ativo. Assim, você pode tirar snapshot de um sistema com 35 GiB de dados usando apenas 2 GiB de espaço livre desde que você modifique menos de 2 GiB (em ambos original e snapshot). Para que seja possível criar snapshots, será necessário ter espaço não alocado em seu grupo de volumes. Criar snapshots em qualquer outro irá ocupar espaço no respectivo grupo de volumes. Então, se planeja usar snapshots para backup de sua partição raiz, não aloque 100% de seu grupo de volumes para o volume lógico raiz.

#### Configuração

Você cria snapshot de volumes lógicos normalmente como se faz com quaisquer outros volumes normais.

```
# lvcreate --size 100M --snapshot --name snap01 /dev/vg0/lv

```

Com este volume, você pode modificar menos de 100 MiB de dados, antes de preencher todo o volume de snapshots.

Para reverter o volume lógico 'lv' modificado para o estado onde o snapshot 'snap01' foi criado pode ser feito com

```
# lvconvert --merge /dev/vg0/snap01

```

No caso do volume de origem estar ativo, a fusão ocorrerá na próxima reinicialização (esta fusão pode ser feita a partir de um LiveCD).

**Nota:** O snapshot deixará de existir após a fusão.

Múltiplos snapshots também podem ser criados e cada um fundido com seu respectivo volume lógico de origem.

O snapshot pode ser montado e salvo ter seu backup realizado com **dd** ou **tar**. O tamanho do arquivo de backup feito com **dd** terá o tamanho dos arquivos dentro do volume de snapshot. Para restaurá-lo, apenas crie um snapshot, monte-o, e grave ou extraia o backup para dentro dele. Então, mescle-o com a origem.

Snapshots são primariamente usados para fornecer uma cópia congelada do sistema de arquivos para se fazer backups; um backup levando duas horas fornece uma imagem do sistema de arquivos mais consistente do que realizar backup diretamente da partição.

Veja [Criar snapshots do sistema de arquivos raiz com LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM") para automatizar a criação de um sistema de arquivos raiz limpo durante a inicialização dos sistema para backup e restauração.

Veja [LVM dentro de LUKS](/index.php/Dm-crypt_(Portugu%C3%AAs)/Encrypting_an_entire_system_(Portugu%C3%AAs)#LVM_dentro_do_LUKS "Dm-crypt (Português)/Encrypting an entire system (Português)") e [LUKS dentro do LVM](/index.php/Dm-crypt_(Portugu%C3%AAs)/Encrypting_an_entire_system_(Portugu%C3%AAs)#LUKS_dentro_do_LVM "Dm-crypt (Português)/Encrypting an entire system (Português)").

Se tiver volumes LVM não ativados via [initramfs](/index.php/Initramfs "Initramfs"), [ative](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)") `lvm-monitoring.service`, fornecido pelo pacote [lvm2](https://www.archlinux.org/packages/?name=lvm2).

### Cache LVM

De [lvmcache(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmcache.7):

	O *cache* de volumes lógicos usa um LV pequeno e rápido para melhorar a performance de um LV grande e lento. Isto é feito armazenando os blocos usados frequentemente em um LV mais rápido. O LVM então refere-se ao LV pequeno e rápido como um LV de cache. O LV grande e lento é chamado de LV de origem. Devido às requisições do *dm-cache* (o driver do kernel), o LVM divide adicionalmente o LV de cache em dois dispositivos - um LV de cache de dados e um LV de cache de metadados. O LV de cache de dados é o local onde cópias dos blocos de dados são mantidos à partir do LV de origem para aumentar a velocidade. O LV de cache de metadados mantém informações que especificam onde os blocos de dados estão armazenados (por exemplo, no LV de origem ou no LV de cache de dados). Usuários devem familiarizar-se com esses LVs se desejarem criar volumes de cache melhores e mais robustos. Todos estes LVs associados devem residir no mesmo VG.

#### Criar cache

A maneira mais rápida é criar um PV (se necessário) no disco mais rápido e adicioná-lo ao grupo de volumes existente:

```
# vgextend dataVG /dev/sdx

```

Criar um cache automático com metadados em sdb, e converter o volume lógico existente (dataLV) para o volume que já contenha o cache, tudo em um único passo:

```
# lvcreate --type cache --cachemode writethrough -L 20G -n dataLV_cachepool dataVG/dataLV /dev/sdx

```

Obviamente, se desejar que seu cache seja maior, você pode aumentar o parâmetro `-L` para um tamanho diferente.

**Nota:** `--cachemode` tem duas possíveis opções:

*   `writethrough` garante que todos os dados gravados sejam armazenados no LV do conjunto de cache e no LV de origem. A perda de um dispositivo associado com o LV do conjunto de cache neste caso não implica nenhuma perda de dados;
*   `writeback` garante melhor performance, mas ao custo de maior risco de perda de dados em caso de falha de um dos dispositivos usados para cache.

Se um `--cachemode` específico não for indicado, o sistema irá assumir `writethrough` como padrão.

#### Remover cache

Se você precisar desfazer a operação de criação em uma etapa acima:

```
# lvconvert --uncache dataVG/dataLV

```

Isto confirmará qualquer gravação pendente em cache de volta ao LV de origem, e então excluirá o cache. Outras opções estão disponíveis e descritas em [lvmcache(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmcache.7).

### RAID

From [lvmraid(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmraid.7):

	[lvm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvm.8) RAID é uma maneira de criar um volume lógico (LV) que usa múltiplos dispositivos físicos para aumentar performance ou tolerar falhas em dispositivos. Em LVM, os dispositivos físicos são, na verdade, volumes físicos (PVs) em um único grupo de volumes (VG).

LVM RAID suporta RAID 0, RAID 1, RAID 4, RAID 5, RAID 6 e RAID 10\. Veja [Wikipedia:Standard RAID levels](https://en.wikipedia.org/wiki/Standard_RAID_levels "wikipedia:Standard RAID levels") para detalhes sobre cada nível.

#### Configurando RAID

Crie volumes físicos:

```
# pvcreate /dev/sda2 /dev/sdb2

```

Crie um grupo de volumes nos volumes físicos:

```
# vgcreate VolGroup00 /dev/sda2 /dev/sdb2

```

Crie volumes lógicos usando `lvcreate --type *nivel_RAID*`, veja [lvmraid(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmraid.7) e [lvcreate(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvcreate.8) para mais opções.

```
# lvcreate --type RaidLevel [OPTIONS] -n Name -L Size VG [PVs]

```

Por exemplo:

```
# lvcreate --type raid1 --mirrors 1 -L 20G -n myraid1vol VolGroup00 /dev/sda2 /dev/sdb2

```

irá criar um volume lógico espelhado de 20 GiB chamado "myraid1vol" no grupo VolGroup00 em `/dev/sda2` e `/dev/sdb2`.

#### Configurar mkinitcpio para RAID

Se seu sistema de arquivos raiz está em um LVM RAID adicionalmente aos hooks `lvm2` ou `sd-lvm2`, será necessário adicionar `dm-raid` e os módulos RAID apropriados (por exemplo, `raid0`, `raid1`, `raid10` e/ou `raid456`) para a matriz MODULES em `mkinitcpio.conf`.

Para initramfs baseada em busybox:

 `/etc/mkinitcpio.conf` 
```
MODULES=(**dm-raid raid0 raid1 raid10 raid456**)
HOOKS=(base **udev** ... block **lvm2** filesystems)
```

Para initramfs baseada em systemd:

 `/etc/mkinitcpio.conf` 
```
MODULES=(**dm-raid raid0 raid1 raid10 raid456**)
HOOKS=(base **systemd** ... block **sd-lvm2** filesystems)
```

## Solução de problemas

### Problemas de inicialização/desligamento causam a desativação de lvmetad

`use_lvmetad = 1` **deve** ser definido em `/etc/lvm/lvm.conf`. Este é o padrão agora - se você tiver um arquivo `lvm.conf.pacnew`, você deve mesclar todas as alterações.

### Comandos LVM não funcionam

*   Carregue o módulo apropriado:

```
# modprobe dm_mod

```

O módulo `dm_mod` deve ser automaticamente carregado. Caso não seja, você poderá tentar:

 `/etc/mkinitcpio.conf`  `MODULES=(dm_mod ...)` 

Será necessário [recriar a initramfs](/index.php/Recriar_a_initramfs "Recriar a initramfs") para confirmar as alterações feitas.

*   tente comandos precedendo *lvm*, como este:

```
# lvm pvdisplay

```

### Volumes lógicos não são exibidos

Se estiver tentando montar volumes lógicos existentes, mas eles não são exibidos em `lvscan`, você poderá usar os seguintes comandos para ativá-los:

```
# vgscan
# vgchange -ay

```

### LVM em mídia removível

Sintomas:

 `# vgscan` 
```
  Reading all physical volumes.  This may take a while...
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836585984: Input/output error
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836643328: Input/output error
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 0: Input/output error
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 4096: Input/output error
  Found volume group "backupdrive1" using metadata type lvm2
  Found volume group "networkdrive" using metadata type lvm2

```

Causa: remover uma unidade externa LVM sem antes desativar o(s) grupo(s) de volume(s). Antes de desconectá-lo, certifique-se:

```
# vgchange -an *nome do grupo de volumes*

```

Solução: assumindo que você já tentou ativar o grupo de volumes com `vgchange -ay *vg*`, e ainda está recebendo erros de *Input/output*:

```
# vgchange -an *nome do grupo de volumes*

```

Desconecte a unidade externa e aguarde alguns minutos:

```
# vgscan
# vgchange -ay *nome do grupo de volumes*

```

#### Suspensão/retorno com LVM e mídia removível

Para que o LVM funcione corretamente em mídia removível – como um dispositivo USB externo – o grupo de volumes do da unidade externa deverá ser desativada antes do sistema entrar em suspensão. Se isto não for feito, você poderá obter erros de *"buffer I/O errors"* no dispositivo (após retornar do modo de suspensão). Por esta razão, não é recomendável misturar dispositivos externos com dispositivos internos no mesmo grupo de volumes.

Para desativar automaticamente grupos de volumes com unidades USB externas, marque cada grupo de volumes com `sleep_umount` assim:

```
# vgchange --addtag sleep_umount *vg_external*

```

Uma vez que a *tag* for definida, use a seguinte *unit* para o systemd desativar corretamente volumes antes de entrar em modo de suspensão. Ao retornar do modo de suspensão, eles serão automaticamente ativados pelo LVM:

 `/etc/systemd/system/ext_usb_vg_deactivate.service` 
```
[Unit]
Description=Desativar grupos de volumes USB externos ao entrar em modo de suspensão
Before=sleep.target

[Service]
Type=oneshot
ExecStart=-/etc/systemd/system/deactivate_sleep_vgs.sh

[Install]
WantedBy=sleep.target
```

e este script:

 `/etc/systemd/system/deactivate_sleep_vgs.sh` 
```
#!/bin/sh

TAG=@sleep_umount
vgs=$(vgs --noheadings -o vg_name $TAG)

echo "Desativando grupos de volumes com a tag $TAG: $vgs"

# Desmonta volumes lógicos pertencentes a todos os gruops de volumes com a tag $TAG
for vg in $vgs; do
    for lv_dev_path in $(lvs --noheadings  -o lv_path -S lv_active=active,vg_name=$vg); do
        echo "Unmounting logical volume $lv_dev_path"
        umount $lv_dev_path
    done
done

# Desativa grupos de volumes marcados com sleep_umount
for vg in $vgs; do
    echo "Deactivating volume group $vg"
    vgchange -an $vg
done
```

Finalmente, [ative](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)") a unit.

### O redimensionamento de um volume lógico falha

Se estiver tentando extender um volume lógico e obtém o erro:

```
" Insufficient suitable contiguous allocatable extents for logical volume "

```

A causa é que o volume lógico foi criado com uma alocação explicitamente (opções `-C y` ou `--alloc contiguous`) e não há outra extensão contígua disponível (veja também a [referência](http://www.hostatic.ro/2010/02/15/lvm-inherit-and-contiguous-policies/)).

Para resolver isto, primeiro estenda o volume lógico, altere seu método de alocação com `lvchange --alloc inherit <volume_logico>`. Se for necessário manter o método de alocação contíguo, uma alternativa seria mover o volume para uma área do disco com espaço livre extensão suficiente (veja [[1]](http://superuser.com/questions/435075/how-to-align-logical-volumes-on-contiguous-physical-extents)).

### Comando "grub-mkconfig" reporta o erro "unknown filesystem"

Certifique-se de remover primeiro os volumes de snapshot antes de [gerar o grub.cfg](/index.php/GRUB_(Portugu%C3%AAs)#Gerar_o_arquivo_de_configuração_principal "GRUB (Português)").

### Tempo esgotado em volumes de dispositivos da raiz

Com uma grande quantidade de snapshots, `thin_check` executará por muito tempo, o que fará com que do dispositivos da raiz do sistema tenham seu tempo-limite esgotado. Para compensar isso, adicione o parâmetro na inicialização do kernel `rootdelay=60` na configuração do gerenciador de boot. Ou, faça `thin_check` pular a verificação de mapeamento de blocos (veja [[2]](https://www.redhat.com/archives/linux-lvm/2016-January/msg00010.html)) e [recriar a initramfs](/index.php/Recriar_a_initramfs "Recriar a initramfs"):

 `/etc/lvm/lvm.conf`  `thin_check_options = [ "-q", "--clear-needs-check-flag", "--skip-mappings" ]` 

### Demora no desligamento

Se estiver usando RAID, snapshots ou provisionamento poderão causar uma demora no desligamento, certifique-se de que o serviço `lvm2-monitor.service` está [iniciado](/index.php/Iniciado "Iniciado"). Veja [FS#50420](https://bugs.archlinux.org/task/50420).

## Veja também

*   [LVM2 Resource Page](http://sourceware.org/lvm2/) on SourceWare.org
*   [LVM](http://wiki.gentoo.org/wiki/LVM) article at Gentoo wiki
*   [Ubuntu LVM Guide Part 1](http://www.tutonics.com/2012/11/ubuntu-lvm-guide-part-1.html)[Part 2 detals snapshots](http://www.tutonics.com/2012/12/lvm-guide-part-2-snapshots.html)
*   [Red Hat: Logical Volume Manager Administration](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Logical_Volume_Manager_Administration/index.html)