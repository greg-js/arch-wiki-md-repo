Related articles

*   [Sistemas de arquivos](/index.php/Sistemas_de_arquivos "Sistemas de arquivos")
*   [fdisk](/index.php/Fdisk "Fdisk")
*   [gdisk](/index.php/Gdisk "Gdisk")
*   [parted](/index.php/Parted "Parted")
*   [fstab](/index.php/Fstab "Fstab")
*   [LVM](/index.php/LVM "LVM")
*   [Swap](/index.php/Swap "Swap")
*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

O [particionamento](https://en.wikipedia.org/wiki/Particionamento_de_disco ou para separar dados de maneira lógica como arquivos de áudio e vídeo.

As informações necessárias são gravadas em um esquema de [tabela de partições](#Tabela_de_partições) que pode ser MBR ou GPT.

Tabelas de partições são criadas e modificadas usando uma de diversas ferramentas, a qual deve ser compatível com o esquema da tabela de partição escolhido. Ferramentas disponíveis estão listadas na seção [#Ferramentas de particionamento](#Ferramentas_de_particionamento).

Uma vez criada, uma partição deve ser formatada com um [sistema de arquivos](/index.php/Sistema_de_arquivos "Sistema de arquivos") apropriado antes que arquivos possam ser gravados nela.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Tabela de partições](#Tabela_de_partições)
    *   [1.1 Master Boot Record](#Master_Boot_Record)
        *   [1.1.1 Master Boot Record (código de inicialização)](#Master_Boot_Record_(código_de_inicialização))
        *   [1.1.2 Master Boot Record (tabela de partição)](#Master_Boot_Record_(tabela_de_partição))
    *   [1.2 GUID Partition Table](#GUID_Partition_Table)
    *   [1.3 Escolhendo entre MBR e GPT](#Escolhendo_entre_MBR_e_GPT)
    *   [1.4 Disco sem partição](#Disco_sem_partição)
        *   [1.4.1 Particionamento Btrfs](#Particionamento_Btrfs)
*   [2 Esquema de partição](#Esquema_de_partição)
    *   [2.1 Partição raiz simples](#Partição_raiz_simples)
    *   [2.2 Partições discretas](#Partições_discretas)
        *   [2.2.1 /](#/)
        *   [2.2.2 /boot](#/boot)
        *   [2.2.3 /home](#/home)
        *   [2.2.4 /var](#/var)
        *   [2.2.5 /data](#/data)
        *   [2.2.6 Swap](#Swap)
    *   [2.3 Exemplos de leiaute](#Exemplos_de_leiaute)
        *   [2.3.1 Leiaute de exemplo UEFI/GPT](#Leiaute_de_exemplo_UEFI/GPT)
        *   [2.3.2 Leiaute de exemplo BIOS/MBR](#Leiaute_de_exemplo_BIOS/MBR)
        *   [2.3.3 Leiaute de exemplo BIOS/GPT](#Leiaute_de_exemplo_BIOS/GPT)
*   [3 Ferramentas](#Ferramentas)
    *   [3.1 Ferramentas de particionamento](#Ferramentas_de_particionamento)
        *   [3.1.1 fdisk](#fdisk)
        *   [3.1.2 GPT fdisk](#GPT_fdisk)
        *   [3.1.3 GNU Parted](#GNU_Parted)
    *   [3.2 Backup](#Backup)
    *   [3.3 Recuperação](#Recuperação)
*   [4 Alinhamento de partição](#Alinhamento_de_partição)
*   [5 Suporte à GPT do kernel](#Suporte_à_GPT_do_kernel)
*   [6 Truque para BIOS antigos inicializarem a partir de GPT](#Truque_para_BIOS_antigos_inicializarem_a_partir_de_GPT)
*   [7 Veja também](#Veja_também)

## Tabela de partições

**Dica:** Para imprimir/listar tabelas existentes (de um dispositivo específico), execute `parted */dev/sda* print` ou `fdisk -l */dev/sda*`, onde `*/dev/sda*` é um nome de [dispositivo de bloco](/index.php/Dispositivo_de_bloco "Dispositivo de bloco").

Há dois principais tipos de tabelas de partição disponíveis. Eles são descritos abaixo nas seções [#Master Boot Record](#Master_Boot_Record) (MBR) e [#GUID Partition Table](#GUID_Partition_Table) (GPT) juntos com uma discussão sobre como escolher um deles. Uma terceira alternativa, a menos comum, é usar um disco sem nenhuma partição, a qual também está discutida.

### Master Boot Record

O [Master Boot Record](https://en.wikipedia.org/wiki/Master_boot_record em sistemas [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS"). Veja [Wikipedia:Master boot record#Disk partitioning](https://en.wikipedia.org/wiki/Master_boot_record#Disk_partitioning "wikipedia:Master boot record") para conhecer a estrutura do MBR.

**Nota:**

*   O MBR não fica localizado dentro de uma partição; mas sim no primeiro setor do dispositivo (fisicamente a trilha 0), antes da primeira partição.
*   O setor de boot presente em um dispositivo sem partição ou com uma partição individual é chamado de [volume boot record (VBR)](https://en.wikipedia.org/wiki/Volume_boot_record "wikipedia:Volume boot record"), ao invés de MBR.

#### Master Boot Record (código de inicialização)

Os primeiros 440 bytes do MBR são a **área do codigo de inicialização**. Em sistemas BIOS, ela usualmente contém o primeiro estágio do carregador de inicialização. Este código pode ser armazenado em backup, restaurado ou apagado [usando dd](/index.php/Dd_(Portugu%C3%AAs)#Fazer_backup_e_restaurar_MBR "Dd (Português)").

#### Master Boot Record (tabela de partição)

Na tabela de partição MBR (também conhecida como tabela de partição MS-DOS) há três tipos de partições:

*   Partição primária
*   Partição extendida
    *   Unidade lógica

**Partições primárias** podem ser inicializadas e são limitadas a quatro por disco ou volume RAID. Se a tabela de partição MBR requerer mais do que quatro partições, então uma das partições primárias deve ser substituída por uma **partição extendida** contendo uma **unidade lógica** ou mais dentro dela.

Partições extendidas podem ser pensadas como contêineres para unidades lógicas. Um disco rígido não pode conter mais do que uma partição extendida. A partição extendida também é contada como uma partição primária, então se um disco possuir uma partição extendida, somente outras três partições primárias serão possíveis (isto é, três partições primárias e uma partição extendida). O número de unidades lógicas residentes dentro de uma partição extendida é ilimitado. Um sistema executado em dual-boot com Windows irá necessitar que o Windows esteja dentro de uma partição primária.

Um esquema bem comum é criar partições primárias de *sda1* até *sda3* seguidas por uma partição extendida *sda4*. As unidades lógicas em *sda4* são numeradas como *sda5*, *sda6*, etc.

**Dica:** Ao particionar um disco MBR, considere deixar ao menos 33 setores de 512 bytes cada (16.5 KiB) de espaço livre sem particionamento no final do disco para caso você decida [convertê-lo posteriormente para GPT](/index.php/Gdisk#Convert_between_MBR_and_GPT "Gdisk"). Este espaço adicional será necessário para guardar o cabeçalho da GPT.

### GUID Partition Table

[GUID Partition Table](https://en.wikipedia.org/wiki/GUID_Partition_Table "wikipedia:GUID Partition Table") (GPT) é um esquema de particionamento que é parte da especificação [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface"); utiliza [globally unique identifiers](https://en.wikipedia.org/wiki/Globally_unique_identifier "wikipedia:Globally unique identifier") (GUIDs), ou UUIDs no universo Linux, para definir partições e [tipos de partição](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table"). Foi desenvolvido para suceder o esquema de particionamento [Master Boot Record](#Master_Boot_Record).

No início de uma tabela de partição GPT no disco, há um [protetor do registro-mestre de inicialização](https://en.wikipedia.org/wiki/GUID_Partition_Table#Protective_MBR_.28LBA_0.29 a qual pode ser usada para inicializar sistemas usando esquemas BIOS/GPT em bootloaders que suportarem.

### Escolhendo entre MBR e GPT

GUID Partition Table (GPT) é uma alternativa moderna de método de particionamento criada para substituir o antigo sistema de registro-mestre de inicialização (MBR). GPT possui algumas vantagens sobre o MBR, o qual data de tempos do MS-DOS. Com os recentes desenvolvimentos de ferramentas de formatação, é fácil obter performance e confiabilidade iguais tanto para GPT como para MBR.

**Nota:** Para que o GRUB possa inicializar a partir de um disco particionado no esquema GPT em um sistema baseado em BIOS, uma [partição de inicialização BIOS](/index.php/GRUB_(Portugu%C3%AAs)#Instruções_específicas_de_Tabela_de_Partição_GUID_(GPT) "GRUB (Português)") é necessária.

Alguns pontos a serem considerar na escolha:

*   Para dual-boot com Windows (ambos 32-bit e 64-bit) usando um sistema BIOS, será necessário escolher o esquema MBR.
*   Para dual-boot com Windows 64-bit usando o modo [UEFI](/index.php/UEFI "UEFI") ao invés de BIOS, será necessário usar o esquema GPT.
*   Se estiver instalando em hardware antigo, especialmente em laptops antigos, considere escolher MBR seu BIOS pode não suportar (mas [veja abaixo](/index.php/Partitioning_(Portugu%C3%AAs)#Truque_para_BIOS_antigos_inicializarem_a_partir_de_GPT "Partitioning (Português)") como contornar isso).
*   Se estiver particionando um disco de 2 TiB ou mais, será necessário usar o esquema GPT.
*   É recomendável sempre usar GPT para incializar sistemas [UEFI](/index.php/UEFI "UEFI"), já que algumas implementações UEFI não suportam inicializar MBR.
*   Se nenhuma das condições acima se aplicarem, será possível escolher livremente entre GPT e MBR. Uma vez que GPT é mais moderno, é recomendável usá-lo neste caso.

Algumas vantagens do GPT sobre o MBR são:

*   Fornece GUID de disco e GUID de partição ([PARTUUID](/index.php/Persistent_block_device_naming_(Portugu%C3%AAs)#by-partuuid "Persistent block device naming (Português)")) exclusivos para cada partição - uma boa prática de referenciar partições e discos para o sistema de arquivos.
*   Fornece um nome de partição independente do sistema de arquivos ([PARTLABEL](/index.php/Persistent_block_device_naming_(Portugu%C3%AAs)#by-partlabel "Persistent block device naming (Português)")).
*   Número arbitrário de partições - depende do espaço alocado para a tabela de partições - Não necessita de partições extendidas e unidades lógicas. Por padrão, a tabela de partições GPT contém espaço para difinir até 128 partições. Entretanto, se for desejável definir mais partições, é possível alocar mais espaço para a tabela de partições (atualmente apenas *gdisk* é reconhecido por suportar esse recurso).
*   Utiliza LBA de 64-bits para armazenar números de setores - permite endereçar discos de até 2 ZiB. O MBR é limitado a endereçar até 2 TiB de espaço por dispositivo.
*   Armazena um cabeçalho de backup e uma tabela de partição no fim do disco que auxiliam na [recuperação](/index.php/Gdisk#Recover_GPT_header "Gdisk") no caso destas serem danificadas.
*   Recurso CRC32 checksums para detectar erros e corrompimento do cabeçalho e da tabela de partições.

A seção de [#Ferramentas de particionamento](#Ferramentas_de_particionamento) contém uma tabela indicando quais ferramentas estão disponívels para criar e modificar tabelas GPT e MBR.

**Dica:** É possível converter entre MBR e GPT. Veja [gdisk#Convert between MBR and GPT](/index.php/Gdisk#Convert_between_MBR_and_GPT "Gdisk").

### Disco sem partição

Um disco sem partição, também conhecido como [superfloppy](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/windows-and-gpt-faq#what-is-a-superfloppy) refere-se a um dispositivo de armazenamento sem uma tabela de partição, tendo um sistema de arquivos ocupando o dispositivo de armazenamento inteiro. O setor de boot presente em um disco sem partição é chamado de [volume boot record (VBR)](https://en.wikipedia.org/wiki/Volume_boot_record "wikipedia:Volume boot record").

#### Particionamento Btrfs

[Btrfs](/index.php/Btrfs "Btrfs") pode ocupar um dispositivo de armazenamento inteiro e substituir os esquemas de particionamento [MBR](#Master_Boot_Record) ou [GPT](#GUID_Partition_Table). Veja as instruções em [Btrfs#File system on a single device](/index.php/Btrfs#File_system_on_a_single_device "Btrfs") para detalhes.

## Esquema de partição

Não há regras estritas para particionar um disco rígido, embora o guia geral a seguir possa ser seguido. Um esquema de particionamento de disco é determinado por várioas razões como flexibilidade desejada, velocidade, segurança, bem como limitações impostas pelo espaço em disco disponível. É essencialmente uma preferência pessoal. Se pretende fazer dual-boot com Arch Linux e um sistema operacional Windows, veja [Dual boot com Windows](/index.php/Dual_boot_com_Windows "Dual boot com Windows").

**Nota:**

*   Sistemas [UEFI](/index.php/UEFI "UEFI") requerem uma ESP, ou [partição de sistema EFI](/index.php/EFI_system_partition_(Portugu%C3%AAs) "EFI system partition (Português)").
*   Sistemas BIOS que são particionados com [GPT](#GUID_Partition_Table) requerem uma [partição de inicialização BIOS](/index.php/GRUB_(Portugu%C3%AAs)#Instruções_específicas_de_Tabela_de_Partição_GUID_(GPT) "GRUB (Português)") se [GRUB](/index.php/GRUB "GRUB") for o bootloader usado.

**Dica:** Se estiver usando [Btrfs](/index.php/Btrfs "Btrfs"), subvolumes podem ser usados para imitar partições. Veja a seção [Btrfs#Mounting subvolumes](/index.php/Btrfs#Mounting_subvolumes "Btrfs").

### Partição raiz simples

Este esquema é o mais simples e deve ser suficiente para a maioria dos casos. Um [arquivo swap](/index.php/Arquivo_swap "Arquivo swap") pode ser criado e facilmente redimensionado conforme necessário. Isto usualmente faz sentido de ser feito considerando uma partição `/` simples e posteriormente se desejar separar outras em casos específicos como RAID, encriptação, uma partição de mídia compartilhada, etc.

### Partições discretas

Separar um diretório como uma partição permite selecionar diferentes sistemas de arquivos e opções de montagem. Em casos como o de partições de mídia, elas tambem podem ser compartilhados entre sistemas operacionais.

A seguir, há alguns exemplos de esquemas que podem ser usados ao fazer um particionamento, e as subseções seguintes detalham um pouco diretorios os quais podem ter sua própria partição separada e seu ponto de montagem relativo a `/`. Veja [file-hierarchy(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file-hierarchy.7) para uma descrição completa do conteúdo destes diretórios.

#### /

O diretório-raiz é o topo da hierarquia, o ponto onde o principal sistema de arquivos é montado e de cada outro sistema de arquivos reside. Todos os arquivos e diretórios aparecem sob o diretório-raiz `/`, mesmo se estiverem armazenados em outros dispositivos físicos. O conteúdo do sistema de arquivos raiz deve ser adequado para inicializar, restaurar, recuperar e/ou reparar o sistema. Portanto, alguns diretórios sob `/` não são cadidatos para partições separadas.

A partição `/` ou partição-raiz é necessária e também a mais importante. As demais partições podem ser substituídas por ela.

**Atenção:** Diretórios essenciais para inicialização (exceto para `/boot`) **devem** estar na mesma partição de `/` ou montados no mesmo espaço de usuário inicial da [initramfs](/index.php/Initramfs "Initramfs"). Estes diretórios essenciais são: `/etc` e `/usr` [[1]](https://freedesktop.org/wiki/Software/systemd/separate-usr-is-broken).

`/` tradicionalmente contém o diretório `/usr`, o qual pode crescer significativamente à medida em que novo software for instalado. 15–20 GiB devem ser suficientes para a maioria dos usuários com modernos discos rígidos. Se planejar armazenar um arquivo de swap aqui, precisará de um tamanho de partição maior.

#### /boot

O diretório `/boot` contém as imagens do kernel e ramdisk, bem como o arquivo de configuração do bootloader. Também armazena os dados que são usados antes mesmo de o kernel começar a executar programas no espaço de usuário. `/boot` não é necessário na execução normal do sistema, apenas durante o processo de inicialização e durante atualização do kernel (quando as imagens do randisk precisam ser recriadas).

**Nota:**

*   Uma partição `/boot` separada é somente necessária se o seu bootloader não for capaz de acessar o diretório `/boot` que reside dentro de `/`. Por exemplo, se o bootloader não suportar o sistema de arquivos ou se seu diretório `/` estiver em um dispositivo de bloco empilhado (por exemplo, [RAID](/index.php/RAID "RAID") via software, um [volume criptografado](/index.php/Dm-crypt "Dm-crypt") ou um [LVM](/index.php/LVM "LVM")) e se o bootloader não tiver drivers que suportem. Veja [Arch boot process (Português)#Gerenciador de boot](/index.php/Arch_boot_process_(Portugu%C3%AAs)#Gerenciador_de_boot "Arch boot process (Português)") para mais informações sobre pré-requisitos e capacidades de bootloaders.
*   Se estiver inicializando um [boot loader](/index.php/Arch_boot_process_(Portugu%C3%AAs)#Gerenciador_de_boot "Arch boot process (Português)") UEFI que não possuir drivers para outros sistemas de arquivos, é recomendável montar a [partição de sistema EFI](/index.php/EFI_system_partition_(Portugu%C3%AAs) "EFI system partition (Português)") em `/boot`. Veja [EFI system partition (Português)#Montar a partição](/index.php/EFI_system_partition_(Portugu%C3%AAs)#Montar_a_partição "EFI system partition (Português)") para mais informações.

Um tamanho sugerido para `/boot` é 200 MiB a menos que esteja usando uma [partição de sistema EFI](/index.php/EFI_system_partition_(Portugu%C3%AAs) "EFI system partition (Português)") como `/boot`, neste caso, no mímimo 260 MiB são recomendados.

#### /home

O diretório `/home` contém arquivos de configuração, caches, dados de aplicativos e arquivos de mídia específicos do usuário.

Separar `/home` permite que `/` seja reparticionada separadamente, mas note que será possível reinstalar Arch com `/home` intocada mesmo se não estiver separada - basta que os diretórios de outros níveis sejam removidos, e então pacstrap poderá ser executado.

Não se deve compartilhar diretórios de usuários entre diferentes distribuições, porque elas usam versões de software incompatíveis entre si. Invés disso, considere compartilhar uma partição de mídia ou ao menos usar diferentes diretórios dentro da partição `/home`. O tamanho desta artição varia.

#### /var

O diretório `/var` armazena dados de spool em diretórios e arquivos, dados administrativos e de acesso, cache do [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), etc. É usada, por exemplo, para cache e registro, e portanto é frequentemente alvo de operações de leitura e escrita. Mantendo-a em uma partição separada evita esgotar o espaço disponível devido a logs enormes.

Ela existe para que seja possível montar `/usr` como somente-leitura. Tudo que, historicamente, foi gravado dentro de `/usr` e que é escrito durante a operação do sistema (com exceção de instalação e manutenção de software) deve residir em `/var`.

**Nota:** `/var` contém muitos arquivos pequenos. A escolha de um tipo de sistema de arquivos deve considerar isso se uma partição exclusiva for usada.

`/var` irá conter, entre outros dados, o cache do [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"). Manter estes pacotes é útil no caso de alguma atualização causar instabilidade, exigindo um [downgrade](/index.php/Downgrading_packages_(Portugu%C3%AAs) "Downgrading packages (Português)") para um pacote mais antigo arquivado. O cache do pacman irá aumentar à medida em que o sistema crescer e for atualizado, mas pode seguramente ser limpo se espaço se tornar um problema. 8–12 GiB em um sistema desktop deve ser suficiente para `/var`, dependendo da quantidade de software instalado.

#### /data

Pode-se considerar montar uma partição `/data` para armazenar diversos dados compartilhados entre usuários. Usar a partição `/home` para este propósito também é válido. O tamanho desta partição pode variar.

#### Swap

Uma partição [swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)") fornece uma memória que pode ser usada como memória RAM virtual. Um [arquivo swap](/index.php/Arquivo_swap "Arquivo swap") deve ser uma opção considerada também, como eles não tem nenhuma sobrecarga de performance em relação a manter uma partição separada com este propósito, mas são muito mais fáceis de redimensionar. Uma partição swap pode *potencialmente* ser compartilhada entre sistemas operacionais, desde que a hibernação não seja utilizada.

Historicamente, a regra geral para o tamanho da partição swap era alocar duas vezes a quantidade de memória física (RAM) instalada. Como os computadores tem ganhado cada vez maiores capacidades de memória, esta regra está defasada. Por exemplo, um desktop médio com até 512 MiB de RAM, a regra de 2× é usualmente adequada; se uma quantidade de memória RAM suficiente (mais de 1024 MiB) está disponível, é possível ter uma partição ou arquivo swap de menor tamanho.

Para usar hibernação (também referida como suspensão ao disco) é recomendado que seja criada uma partição ou arquivo swap com o tamanho da RAM. Apesar do kernel tentar compactar a imagem de suspensão ao discopara preencher o tamanho do espaço reservado para swap, não há garantia de que será bem-sucedido caso o espaço de swap for significativamente menor do que o tamanho da RAM. Veja [Power management/Suspend and hibernate#Hibernation](/index.php/Power_management/Suspend_and_hibernate#Hibernation "Power management/Suspend and hibernate") para mais informações.

### Exemplos de leiaute

Os exemplos a seguir usam `/dev/sda` como exemplo de disco com `/dev/sda1` como sua primeira partição. O esquema de nomeamento do dispositivo de bloco poderá ser diferente se estiver particionando um disco [NVMe](/index.php/NVMe "NVMe") (por exemplo, `/dev/nvme0n1` com partições iniciando em `/dev/nvme0n1p1`), um catão SD ou disco eMMC (por exemplo `/dev/mmcblk0` com partições começando em `/dev/mmcblk0p1`). Veja [Device file (Português)#Nomes de dispositivos de bloco](/index.php/Device_file_(Portugu%C3%AAs)#Nomes_de_dispositivos_de_bloco "Device file (Português)") para mais informações.

**Nota:** Inicialização em UEFI não envolve qualquer bandeira "boot", este método de inicialização depende somente das entradas na NVRAM. [Parted](/index.php/Parted "Parted") e ferramentas similares de interface gráfica usam uma bandeira "boot" em GPT para indicar que esta partição é uma partição de sistema EFI.

#### Leiaute de exemplo UEFI/GPT

| Ponto de montagem no sistema instalado | Partição | [GUID e tipo de partição](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") | [Atributos da partição](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_entries_.28LBA_2.E2.80.9333.29 "wikipedia:GUID Partition Table") | Tamanho sugerido |
| `/boot` ou `/efi` | `/dev/sda1` | `C12A7328-F81F-11D2-BA4B-00A0C93EC93B`: [Partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") | 260 MiB |
| `/` | `/dev/sda2` | `4F68BCE3-E8CD-4DB1-96E7-FBCAF984B709`: Linux x86-64 root (/) | 23–32 GiB |
| `[SWAP]` | `/dev/sda3` | `0657FD6D-A4AB-43C4-84E5-0933C84B4F4F`: Linux [swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)") | Mais de 512 MiB |
| `/home` | `/dev/sda4` | `933AC7E1-2EB4-4F13-B844-0E14E2AEF915`: Linux /home | Restante do dispositivo |

#### Leiaute de exemplo BIOS/MBR

| Ponto de montagem no sistema instalado | Partição | [ID e tipo de partição](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") | [Bandeira de boot](https://en.wikipedia.org/wiki/Boot_flag "wikipedia:Boot flag") | Tamanho sugerido |
| `/` | `/dev/sda1` | `83`: Linux | Sim | 23–32 GiB |
| `[SWAP]` | `/dev/sda2` | `82`: Linux [swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)") | Não | Mais de 512 MiB |
| `/home` | `/dev/sda3` | `83`: Linux | Não | Restante do dispositivo |

#### Leiaute de exemplo BIOS/GPT

| Ponto de montagem no sistema instalado | Partição | [GUID e tipo de partição](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") | [Atributos da partição](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_entries_.28LBA_2.E2.80.9333.29 "wikipedia:GUID Partition Table") | Tamanho sugerido |
| Nenhum | `/dev/sda1` | `21686148-6449-6E6F-744E-656564454649`: [Partição de inicialização BIOS](/index.php/GRUB_(Portugu%C3%AAs)#Instruções_específicas_de_Master_Boot_Record_(MBR) "GRUB (Português)") | 1 MiB |
| `/` | `/dev/sda2` | `4F68BCE3-E8CD-4DB1-96E7-FBCAF984B709`: Linux x86-64 root (/) | `2`: BIOS inicializável | 23–32 GiB |
| `[SWAP]` | `/dev/sda3` | `0657FD6D-A4AB-43C4-84E5-0933C84B4F4F`: Linux [swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)") | Mais de 512 MiB |
| `/home` | `/dev/sda4` | `933AC7E1-2EB4-4F13-B844-0E14E2AEF915`: Linux /home | Restante do dispositivo |

1.  Uma partição de inicialização BIOS somente é necessária ao usar [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") para inicializar um disco GPT em um sistema BIOS. Esta partição não tem qualquer relação com `/boot`, e sequer deve ser formatada com um sistema de arquivos, nem mesmo montada.

## Ferramentas

### Ferramentas de particionamento

Os programas a seguir são usados para criar e/ou manipular tabelas de partições de dispositivos e partições. Veja os artigos nos links para os comandos exatos a serem usados.

Esta tabela irá ser útil para escolher o utilitário de sua necessidade:

 MBR | GPT |
| Scripts de diálogo | fdisk
parted | fdisk
gdisk
parted |
| Modo texto interativo | cfdisk | cfdisk
cgdisk |
| Não interativo | sfdisk
parted | sfdisk
sgdisk
parted |
| Gráfico | GParted
gnome-disk-utility
partitionmanager | GParted
gnome-disk-utility
partitionmanager |

**Atenção:** Para particionar dispositivos, use uma ferramenta de particionamento compatível com o tipo de tabela de partição (GPT ou MBR) escolhido. O uso de ferramentas incompatíveis pode resultar em destruição da tabela junto com suas partições ou dados existentes.

#### fdisk

*fdisk* e seus utilitários estão descritos no artigo [fdisk](/index.php/Fdisk "Fdisk").

*   [fdisk](/index.php/Fdisk "Fdisk") ([util-linux](https://www.archlinux.org/packages/?name=util-linux))
    *   [fdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fdisk.8) – Programa guiado por diálogo para criação e manipulação de tabelas de partição.
    *   [cfdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cfdisk.8) – Variante do fdisk baseada na biblioteca [Curses](https://en.wikipedia.org/wiki/curses_(programming_library) "wikipedia:curses (programming library)").
    *   [sfdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sfdisk.8) – Variante do fdisk.

#### GPT fdisk

*gdisk* e seus utilitários estão descritos no artigo [gdisk](/index.php/Gdisk "Gdisk").

*   [GPT fdisk](/index.php/GPT_fdisk "GPT fdisk") ([gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk))
    *   [gdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gdisk.8) – Manipulador de [Tabela de partições GUID (GPT)](#GUID_Partition_Table) interativo.
    *   [cgdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cgdisk.8) – Variante do gdisk baseada na biblioteca Curses.
    *   [sgdisk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sgdisk.8) – Variante do gdisk.

#### GNU Parted

Este grupo de ferramentas está descrito no artigo [GNU Parted](/index.php/GNU_Parted "GNU Parted").

*   **[GNU Parted](/index.php/GNU_Parted "GNU Parted")** — Ferramenta de particionamento via terminal.

	[https://www.gnu.org/software/parted/parted.html](https://www.gnu.org/software/parted/parted.html) || [parted](https://www.archlinux.org/packages/?name=parted)

*   **GNOME Disks** — Utilitário de gerenciamento de discos para GNOME.

	[https://wiki.gnome.org/Apps/Disks](https://wiki.gnome.org/Apps/Disks) || [gnome-disk-utility](https://www.archlinux.org/packages/?name=gnome-disk-utility)

*   **[GParted](/index.php/GParted "GParted")** — Editor de partições GTK para gerenciar graficamente suas partições de disco.

	[https://gparted.sourceforge.io/](https://gparted.sourceforge.io/) || [gparted](https://www.archlinux.org/packages/?name=gparted)

*   **KDE Partition Manager** — Programa utilitário do KDE para gerenciar dispositivos de disco, partições e sistemas de arquivos.

	[https://www.kde.org/applications/system/kdepartitionmanager/](https://www.kde.org/applications/system/kdepartitionmanager/) || [partitionmanager](https://www.archlinux.org/packages/?name=partitionmanager)

### Backup

*   [fdisk](/index.php/Fdisk "Fdisk") pode criar um backup da tabela de partições. Veja [fdisk#Backup and restore partition table](/index.php/Fdisk#Backup_and_restore_partition_table "Fdisk").
*   [GPT fdisk](/index.php/GPT_fdisk "GPT fdisk") pode criar um backup binário contendo o MBR protetivo, o cabeçalho principal da GPT e uma cópia da tabela de partições. Veja [GPT fdisk#Backup and restore partition table](/index.php/GPT_fdisk#Backup_and_restore_partition_table "GPT fdisk").

### Recuperação

*   **[gpart](https://en.wikipedia.org/wiki/gpart "wikipedia:gpart")** — Um utilitário que descobre o conteúdo de uma tabela de partições MBR destruída. Sua utilização está explicada no manual do [gpart(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gpart.8).

	[https://github.com/baruch/gpart](https://github.com/baruch/gpart) || [gpart](https://www.archlinux.org/packages/?name=gpart)

*   **[GPT fdisk](/index.php/GPT_fdisk#Recover_GPT_header "GPT fdisk")** — Uma ferramenta de particionamento que pode restaurar o cabeçalho primário da GPT (localizada no início do disco) a partir do cabeçalho secundário da GPT (localizado no fim do disco) ou vice-versa.

	[https://www.rodsbooks.com/gdisk/](https://www.rodsbooks.com/gdisk/) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **[TestDisk](/index.php/File_recovery#Testdisk_and_PhotoRec "File recovery")** — Um utilitário que suporta recuperação de partições perdidas em ambos MBR e GPT.

	[https://www.cgsecurity.org/index.html?testdisk.html](https://www.cgsecurity.org/index.html?testdisk.html) || [testdisk](https://www.archlinux.org/packages/?name=testdisk)

## Alinhamento de partição

[fdisk](/index.php/Fdisk "Fdisk"), [gdisk](/index.php/Gdisk "Gdisk") e [parted](/index.php/Parted#Alignment "Parted") lidam com alinhamento automaticamente. Veja [GNU Parted#Check alignment](/index.php/GNU_Parted#Check_alignment "GNU Parted") caso deseje verificar o alinhamento após o particionamento.

Para certas unidades, o [formato avançado](/index.php/Advanced_Format "Advanced Format") pode ser capaz de fornecer melhor desempenho de alinhamento.

## Suporte à GPT do kernel

A opção `CONFIG_EFI_PARTITION` na configuração do kernel ativa o suporte a GPT (apesar do nome, EFI PARTITION). Esta opção deve ser compilada no kernel e não compilada como um módulo carregável. É necessária mesmo em discos GPT que são utilizados para armazenamento de dados e não para inicialização do sistema. É ativada por padrão em todos [kernel oficialmente suportados](/index.php/Kernel_(Portugu%C3%AAs)#Kernels_com_suporte_oficial "Kernel (Português)") pelo Arch. No caso de um kernel personalizado, ative esta opção com o parâmetro `CONFIG_EFI_PARTITION=y`.

## Truque para BIOS antigos inicializarem a partir de GPT

Alguns sistemas baseados em BIOS antigos (produzidos antes de 2010) tentam processar o setor de inicialização e recusam-no se ele não contiver uma partição inicializável MBR. Isto é um problema se for necessário usar GPT neste disco, porque do ponto de vista do BIOS, ele contém somente uma partição MBR não inicializável do tipo `ee` (isto é, uma partição MBR protetiva). É possível marcar a partição protetiva MBR como inicializável usando `fdisk -t mbr /dev/sda`, e isto irá funcionar em alguns sitemas BIOS. Entretanto, a especificação UEFI proíbe a partição protetiva MBR de ser inicializável, e sistemas baseados em UEFI irão interferir nisso, mesmo quando configuradas no modo legado de inicialização. Então, isso importa caso deseje criar um flash drive USB baseado em GPT que deveria inicializar tanto em sistemas UEFI como sistemas BIOS antigos que insistem em procurar uma partição MBR inicializável. Não é possível solucionar este problema usando ferramentas como [fdisk](/index.php/Fdisk "Fdisk") ou [gdisk](/index.php/Gdisk "Gdisk"), mas é possível criar uma partição MBR falsa com uma adequada entrada para ambos os tipos de BIOS manualmente, com uma sequência correta de bytes.

O comando a seguir irá sobrepor a segunda partição MBR e adicionar uma partição inicializável do tipo 0 (isto é, como espaço não utilizado), cobrindo somente o primeiro setor do dispositivo. Isto não vai interferir com a GPT ou com a primeira entrada partição MBR que normalmente contém uma partição MBR protetiva.

```
# printf '\200\0\0\0\0\0\0\0\0\0\0\0\001\0\0\0' | dd of=/dev/sda bs=1 seek=462

```

O resultado final será algo como:

 `# fdisk -t mbr -l /dev/sda` 
```
Disk /dev/sda: 232.9 GiB, 250059350016 bytes, 488397168 sectors
Disk model: ST3250820AS     
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00000000

Device     Boot Start       End   Sectors   Size Id Type
/dev/sda1           1 488397167 488397167 232.9G ee GPT
/dev/sda2  *        0         0         1   512B  0 Empty

Partition table entries are not in disk order.
```

## Veja também

*   [Wikipedia:Disk partitioning](https://en.wikipedia.org/wiki/Disk_partitioning "wikipedia:Disk partitioning")
*   [Wikipedia:Binary prefix](https://en.wikipedia.org/wiki/Binary_prefix "wikipedia:Binary prefix")
*   [Understanding Disk Drive Terminology](https://thestarman.pcministry.com/asm/mbr/DiskTerms.htm)
*   [What is a Master Boot Record (MBR)?](https://kb.iu.edu/d/aijw)
*   Rod Smith's page on [What's a GPT?](https://www.rodsbooks.com/gdisk/whatsgpt.html) and [Booting OSes from GPT](https://rodsbooks.com/gdisk/booting.html)
*   [Make the most of large drives with GPT and Linux - IBM Developer](https://developer.ibm.com/tutorials/l-gpt/)
*   [Microsoft's Windows and GPT FAQ](https://docs.microsoft.com/en-us/windows-hardware/manufacture/desktop/windows-and-gpt-faq)
*   [Partition Alignment](https://www.thomas-krenn.com/en/wiki/Partition_Alignment) (with examples)