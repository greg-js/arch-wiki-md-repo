**Status de tradução:** Esse artigo é uma tradução de [GRUB](/index.php/GRUB "GRUB"). Data da última tradução: 2019-10-20\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=GRUB&diff=0&oldid=585138) na versão em inglês.

Artigos relacionados

*   [Processo de inicialização do Arch](/index.php/Processo_de_inicializa%C3%A7%C3%A3o_do_Arch "Processo de inicialização do Arch")
*   [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")
*   [Tabela de Partição GUID](/index.php/GUID_Partition_Table "GUID Partition Table")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")
*   [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy")
*   [GRUB/Exemplos de EFI](/index.php/GRUB/EFI_examples "GRUB/EFI examples")
*   [GRUB/Dicas e truques](/index.php/GRUB/Tips_and_tricks "GRUB/Tips and tricks")
*   [Multiboot USB drive](/index.php/Multiboot_USB_drive "Multiboot USB drive")

[GRUB](https://www.gnu.org/software/grub/) (GRand Unified Bootloader) é um [gerenciador de multi-boot](/index.php/Gerenciador_de_boot "Gerenciador de boot"). É derivado do [PUPA](http://www.nongnu.org/pupa/), que foi um projeto de pesquisa para desenvolver a substituição do que é agora conhecido como [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"). Este último tornou-se muito difícil de manter e o GRUB foi reescrito do zero com o objetivo de fornecer modularidade e portabilidade [[1]](https://www.gnu.org/software/grub/grub-faq.html#q1). O GRUB atual também é referido como GRUB 2, enquanto o GRUB Legacy corresponde às versões 0.9x.

**Nota:** Em todo este artigo `*esp*` denota o ponto de montagem da [partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI"), comumente abreviada como ESP.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Sistemas BIOS](#Sistemas_BIOS)
    *   [1.1 Instruções específicas de Tabela de Partição GUID (GPT)](#Instruções_específicas_de_Tabela_de_Partição_GUID_(GPT))
    *   [1.2 Instruções específicas de Master Boot Record (MBR)](#Instruções_específicas_de_Master_Boot_Record_(MBR))
    *   [1.3 Instalação](#Instalação)
*   [2 Sistemas UEFI](#Sistemas_UEFI)
    *   [2.1 Instalação](#Instalação_2)
*   [3 Configuração](#Configuração)
    *   [3.1 grub.cfg gerado](#grub.cfg_gerado)
        *   [3.1.1 Gerar o arquivo de configuração principal](#Gerar_o_arquivo_de_configuração_principal)
        *   [3.1.2 Detectando outros sistemas operacionais](#Detectando_outros_sistemas_operacionais)
            *   [3.1.2.1 MS Windows](#MS_Windows)
        *   [3.1.3 Argumentos adicionais](#Argumentos_adicionais)
        *   [3.1.4 LVM](#LVM)
        *   [3.1.5 RAID](#RAID)
        *   [3.1.6 /boot criptografado](#/boot_criptografado)
    *   [3.2 grub.cfg personalizado](#grub.cfg_personalizado)
        *   [3.2.1 Exemplos de entrada de menu de boot](#Exemplos_de_entrada_de_menu_de_boot)
            *   [3.2.1.1 Comandos do GRUB](#Comandos_do_GRUB)
                *   [3.2.1.1.1 Entrada de menu "Desligar"](#Entrada_de_menu_"Desligar")
                *   [3.2.1.1.2 Entrada de menu "Reiniciar"](#Entrada_de_menu_"Reiniciar")
                *   [3.2.1.1.3 Entrada de menu "Configuração do firmware" (UEFI apenas)](#Entrada_de_menu_"Configuração_do_firmware"_(UEFI_apenas))
            *   [3.2.1.2 Binarios de EFI](#Binarios_de_EFI)
                *   [3.2.1.2.1 Shell de UEFI](#Shell_de_UEFI)
                *   [3.2.1.2.2 gdisk](#gdisk)
                *   [3.2.1.2.3 Carregando um arquivo .efi do Arch Linux](#Carregando_um_arquivo_.efi_do_Arch_Linux)
            *   [3.2.1.3 Dual boot](#Dual_boot)
                *   [3.2.1.3.1 GNU/Linux](#GNU/Linux)
                *   [3.2.1.3.2 Windows instalado em modo UEFI/GPT](#Windows_instalado_em_modo_UEFI/GPT)
                *   [3.2.1.3.3 Windows instalado em modo BIOS/MBR](#Windows_instalado_em_modo_BIOS/MBR)
*   [4 Usando o shell de comandos](#Usando_o_shell_de_comandos)
    *   [4.1 Suporte a paginador](#Suporte_a_paginador)
    *   [4.2 Usando o ambiente shell de comandos para iniciar sistemas operacionais](#Usando_o_ambiente_shell_de_comandos_para_iniciar_sistemas_operacionais)
        *   [4.2.1 Carregando o VBR de uma partição](#Carregando_o_VBR_de_uma_partição)
        *   [4.2.2 Carregando o MBR de um disco ou o VBR de um disco sem partição](#Carregando_o_MBR_de_um_disco_ou_o_VBR_de_um_disco_sem_partição)
        *   [4.2.3 Carregando Windows/Linux instalado em modo UEFI](#Carregando_Windows/Linux_instalado_em_modo_UEFI)
        *   [4.2.4 Carregamento normal](#Carregamento_normal)
    *   [4.3 Usando o console de recuperação](#Usando_o_console_de_recuperação)
*   [5 Remoção do GRUB](#Remoção_do_GRUB)
*   [6 Solução de problemas](#Solução_de_problemas)
    *   [6.1 F2FS e outros sistemas de arquivos sem suporte](#F2FS_e_outros_sistemas_de_arquivos_sem_suporte)
    *   [6.2 BIOS da Intel não está inicialização GPT](#BIOS_da_Intel_não_está_inicialização_GPT)
    *   [6.3 Habilitar mensagens de depuração](#Habilitar_mensagens_de_depuração)
    *   [6.4 Erro "No suitable mode found"](#Erro_"No_suitable_mode_found")
    *   [6.5 Mensagem de erro sobre estilo msdos](#Mensagem_de_erro_sobre_estilo_msdos)
    *   [6.6 UEFI](#UEFI)
        *   [6.6.1 Erros comuns de instalação](#Erros_comuns_de_instalação)
        *   [6.6.2 Descartar o shell de recuperação](#Descartar_o_shell_de_recuperação)
        *   [6.6.3 UEFI do GRUB não carregado](#UEFI_do_GRUB_não_carregado)
        *   [6.6.4 Caminho de inicialização padrão/reserva](#Caminho_de_inicialização_padrão/reserva)
    *   [6.7 Assinatura inválida](#Assinatura_inválida)
    *   [6.8 Inicialização congelando](#Inicialização_congelando)
    *   [6.9 Arch não encontrado por outros sistemas operacionais](#Arch_não_encontrado_por_outros_sistemas_operacionais)
    *   [6.10 Aviso ao instalar em chroot](#Aviso_ao_instalar_em_chroot)
    *   [6.11 GRUB carrega lentamente](#GRUB_carrega_lentamente)
    *   [6.12 erro: sistema de arquivos desconhecido](#erro:_sistema_de_arquivos_desconhecido)
    *   [6.13 grub-reboot não está redefinido](#grub-reboot_não_está_redefinido)
    *   [6.14 BTRFS antigo impede a instalação](#BTRFS_antigo_impede_a_instalação)
    *   [6.15 Windows 8/10 não encontrado](#Windows_8/10_não_encontrado)
    *   [6.16 Modo EFI no VirtualBox](#Modo_EFI_no_VirtualBox)
    *   [6.17 Device /dev/xxx not initialized in udev database even after waiting 10000000 microseconds](#Device_/dev/xxx_not_initialized_in_udev_database_even_after_waiting_10000000_microseconds)
    *   [6.18 Recuperação do GRUB e /boot criptografado](#Recuperação_do_GRUB_e_/boot_criptografado)
*   [7 Veja também](#Veja_também)

## Sistemas BIOS

### Instruções específicas de Tabela de Partição GUID (GPT)

Em uma configuração de BIOS/[GPT](/index.php/GPT "GPT"), é necessária uma [partição de inicialização de BIOS](https://www.gnu.org/software/grub/manual/grub/html_node/BIOS-installation.html#BIOS-installation). O GRUB incorpora seu `core.img` nessa partição.

**Nota:**

*   Antes de tentar este método, lembre-se de que nem todos os sistemas poderão ter suporte a este esquema de particionamento. Leia mais sobre [Partitioning#GUID Partition Table](/index.php/Partitioning#GUID_Partition_Table "Partitioning").
*   A partição de inicialização de BIOS é necessária apenas pelo GRUB em uma configuração de BIOS/GPT. Em uma configuração de BIOS/MBR, o GRUB usa a lacuna pós-MBR para a incorporação do `core.img`. No GPT, no entanto, não há espaço não utilizado garantido antes da primeira partição.
*   Para sistemas [UEFI](/index.php/UEFI "UEFI"), essa partição extra não é necessária, pois não há incorporação de setores de inicialização nesse caso. No entanto, os sistemas UEFI ainda requerem uma [partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI").

Crie uma partição de mebibyte (`+1M` com *fdisk* ou *gdisk*) no disco sem sistema de arquivos e com o tipo de partição GUID `21686148-6449-6E6F-744E-656564454649`.

*   Selecione o tipo de partição `BIOS inicialização` para [fdisk](/index.php/Fdisk "Fdisk").
*   Selecione o código de tipo de partição `ef02` para [gdisk](/index.php/Gdisk "Gdisk").
*   Para o [parted](/index.php/Parted "Parted") defina/ative a opção `bios_grub` a partição.

Esta partição pode estar em qualquer ordem de posição, mas deve estar nos primeiros 2 TiB do disco. Esta partição precisa ser criada antes da instalação do GRUB. Quando a partição estiver pronta, instale o gerenciador de boot conforme as instruções abaixo.

O espaço antes da primeira partição também pode ser usado como partição de inicialização de BIOS, embora esteja fora da especificação de alinhamento da GPT. Como a partição não será acessada regularmente, problemas de desempenho podem ser desconsiderados, embora alguns utilitários de disco exibam um aviso sobre isso. Em *fdisk* ou *gdisk* crie uma nova partição a partir do setor 34 e abrangendo até 2047 e defina o tipo. Para que as partições visualizáveis comecem na base, considere adicionar essa partição por último.

### Instruções específicas de Master Boot Record (MBR)

Normalmente, o intervalo pós-MBR (após a região de 512 bytes [MBR](/index.php/MBR "MBR") e antes do início da primeira partição) em muitos sistemas particionados MBR é de 31 KiB quando os problemas de alinhamento do cilindro de compatibilidade do DOS são atendidos na tabela de partições. No entanto, uma lacuna pós-MBR de cerca de 1 a 2 MiB é recomendada para fornecer espaço suficiente para incorporar o `core.img` do GRUB ([FS#24103](https://bugs.archlinux.org/task/24103)). É aconselhável usar uma ferramenta de particionamento que suporte [alinhamento de partições](/index.php/Partitioning#Partition_alignment "Partitioning") de 1 MiB para obter este espaço, bem como para satisfazer outros problemas de setor não-512-byte (que não estão relacionados à incorporação de `core.img`).

### Instalação

[Instale](/index.php/Instale "Instale") o pacote [grub](https://www.archlinux.org/packages/?name=grub). (Ele vai substituir o [grub-legacy](https://aur.archlinux.org/packages/grub-legacy/) se este ainda estiver instalado.) Então, execute:

```
# grub-install --target=i386-pc /dev/sd*X*

```

sendo `/dev/sd*X*` o disco no qual o GRUB deve ser instalado (por exemplo, o disco `/dev/sda` e **não** partição `/dev/sda1`).

Agora, você deve [gerar o arquivo de configuração principal](#Gerar_o_arquivo_de_configuração_principal).

Se você usa [LVM](/index.php/LVM "LVM") para seu `/boot`, você pode instalar o GRUB em vários discos físicos.

**Dica:** Veja [GRUB/Tips and tricks#Alternative installation methods](/index.php/GRUB/Tips_and_tricks#Alternative_installation_methods "GRUB/Tips and tricks") para outras formas de instalar o GRUB, tal como um pendrive USB.

Veja [grub-install(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/grub-install.8) e o [manual do GRUB](https://www.gnu.org/software/grub/manual/grub/html_node/BIOS-installation.html#BIOS-installation) para mais detalhes no comando `grub-install`.

## Sistemas UEFI

**Nota:**

*   É recomendável ler e entender as páginas [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface"), [Partitioning#GUID Partition Table](/index.php/Partitioning#GUID_Partition_Table "Partitioning") e [Processo de inicialização do Arch#No UEFI](/index.php/Processo_de_inicializa%C3%A7%C3%A3o_do_Arch#No_UEFI "Processo de inicialização do Arch").
*   Ao instalar o UEFI, é importante inicializar a mídia de instalação no modo UEFI, caso contrário o *efibootmgr* não poderá adicionar a entrada de inicialização GRUB UEFI. A instalação no [caminho de inicialização reserva](#Caminho_de_inicialização_padrão/reserva) continuará funcionando mesmo no modo BIOS, já que ele não toca na NVRAM.
*   Para inicializar a partir de um disco usando UEFI, é necessária uma partição de sistema EFI. Siga [Partição de sistema EFI#Verificar uma partição existente](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI#Verificar_uma_partição_existente "Partição de sistema EFI") para descobrir se você já tem uma, caso contrário você precisa criá-la.

### Instalação

**Nota:**

*   Os firmwares da UEFI não são implementados de forma consistente entre os fabricantes. O procedimento descrito abaixo destina-se a funcionar em uma ampla variedade de sistemas UEFI, mas os que enfrentam problemas, apesar de aplicarem esse método, são encorajados a compartilhar informações detalhadas e, se possível, as soluções alternativas encontradas para o caso específico do hardware. Um artigo [GRUB/Exemplos de EFI](/index.php/GRUB/EFI_examples "GRUB/EFI examples") foi fornecido para esses casos.
*   A seção supõe que você esteja instalando o GRUB para sistemas x86_64\. Para sistemas UEFI IA32 (32 bits) (não confundir com CPUs de 32 bits), substitua `x86_64-efi` por `i386-efi` onde apropriado.

Primeiro, [instale](/index.php/Instale "Instale") os pacotes [grub](https://www.archlinux.org/packages/?name=grub) e [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr): *GRUB* é o gerenciador de boot, enquanto *efibootmgr* é usado pelo script de instalação do GRUB para escrever entradas de inicialização para NVRAM.

Então, siga os seguintes passos para instalar o GRUB:

1.  [Monte a partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI#Montar_a_partição "Partição de sistema EFI") e, no restante da sessão, substitua `*esp*` com seu ponto de montagem.
2.  Escolha um identificador de gerenciador de boot, aqui chamado `GRUB`. Um diretório com esse nome será criado em `*esp*/EFI/` para armazenar o binário EFI e esse é o nome que aparecerá no menu de inicialização UEFI para identificar a entrada de inicialização do GRUB.
3.  Execute o seguinte comando para instalar o aplicativo EFI do GRUB `grubx64.efi` em `*esp*/EFI/GRUB/` e instalar seus módulos para `/boot/grub/x86_64-efi/`.

```
# grub-install --target=x86_64-efi --efi-directory=*esp* --bootloader-id=GRUB

```

Após a instalação acima, o diretório principal do GRUB está localizado em `/boot/grub/`. Note que o `grub-install` também tenta [criar uma entrada no gerenciador de boot do firmware](/index.php/GRUB/Tips_and_tricks#Create_a_GRUB_entry_in_the_firmware_boot_manager "GRUB/Tips and tricks"), chamado `GRUB` no exemplo acima.

Lembre-se de [gerar o arquivo de configuração principal](#Gerar_o_arquivo_de_configuração_principal) após finalizar a configuração.

**Dica:** Se você usar a opção `--removable`, o GRUB será instalado em `*esp*/EFI/BOOT/BOOTX64.EFI` (ou `*esp*/EFI/BOOT/BOOTIA32.EFI` para o alvo `i386-efi` e você terá a capacidade adicional de poder inicializar a partir da unidade caso as variáveis EFI sejam reiniciadas ou você mover a unidade para outro computador. Normalmente, você pode fazer isso selecionando a unidade em si de forma semelhante ao uso da BIOS. Se estiver usando dual boot com o Windows, esteja ciente de que o Windows geralmente coloca um executável EFI lá, mas sua única finalidade é recriar a entrada de inicialização do UEFI para o Windows.

**Nota:**

*   `--efi-directory` e `--bootloader-id` são específicos para UEFI do GRUB, `--efi-directory` substitui `--root-directory` que está obsoleto.
*   Você pode notar a ausência de uma opção *caminho_dispositivo* (por exemplo: `/dev/sda`) no comando `grub-install`. Na verdade, qualquer *caminho_dispositivo* fornecido será ignorado pelo script de instalação do GRUB UEFI. De fato, os gerenciadores de boot de UEFI não usam um código de inicialização da MBR ou um setor de inicialização de partição.
*   Certifique-se de executar o comando `grub-install` do sistema no qual o GRUB será instalado como o gerenciador de boot. Isso significa que se você estiver inicializando a partir do ambiente de instalação *live*, você precisa estar dentro do chroot quando estiver executando `grub-install`. Se por algum motivo for necessário executar `grub-install` de fora do sistema instalado, anexe a opção `--boot-directory=` com o caminho para o `/boot`, por exemplo, `--boot-directory=/mnt/boot`.

Veja a [solução de problemas do UEFI](#UEFI) caso tenha problemas. Além disso, veja [GRUB/Tips and tricks#UEFI further reading](/index.php/GRUB/Tips_and_tricks#UEFI_further_reading "GRUB/Tips and tricks").

## Configuração

Em um sistema instalado, o GRUB carrega o arquivo de configuração `/boot/grub/grub.cfg` em cada inicialização. Você pode seguir [#grub.cfg gerado](#grub.cfg_gerado) para usar uma ferramenta ou [#grub.cfg personalizado](#grub.cfg_personalizado) para uma criação manual.

### grub.cfg gerado

Esta seção cobre apenas a edição do arquivo de configuração `/etc/default/grub`. Veja [GRUB/Tips and tricks](/index.php/GRUB/Tips_and_tricks "GRUB/Tips and tricks") para mais informações.

Lembre-se de sempre [gerar o arquivo de configuração principal](#Gerar_o_arquivo_de_configuração_principal) após fazer de alterações para `/etc/default/grub` e/ou arquivos em `/etc/grub.d/`.

#### Gerar o arquivo de configuração principal

Após a instalação, o arquivo de configuração principal `/boot/grub/grub.cfg` precisa ser gerado. O processo de geração pode ser influenciado por uma variedade de opções em `/etc/default/grub` e scripts em `/etc/grub.d/`.

Se você não tiver feito configurações adicionais, a geração automática determinará o sistema de arquivos raiz do sistema para inicializar o arquivo de configuração. Para que isso seja bem sucedido, é importante que o sistema seja inicializado ou "chrooted".

**Nota:**

*   Lembre-se que `/boot/grub/grub.cfg` tem que se gerado novamente após qualquer alteração a `/etc/default/grub` ou arquivos em `/etc/grub.d/`.
*   O caminho do arquivo padrão é `/boot/grub/grub.cfg`, não `/boot/grub/i386-pc/grub.cfg`.
*   Se você está tentando executar o *grub-mkconfig* em um chroot ou em um contêiner *systemd-nspawn*, você pode notar que ele não funciona, reclamando que *grub-probe* não consegue "obter o arquivo de configuração a partir de /dev/sdaX". Neste caso, tente usar *arch-chroot* como descrito nesta [publicação no BBS](https://bbs.archlinux.org/viewtopic.php?pid=1225067#p1225067).
*   Se você estiver instalando o GRUB no ambiente chroot usando o LVM e o `grub-mkconfig` travar indefinidamente, consulte [#Device /dev/xxx not initialized in udev database even after waiting 10000000 microseconds](#Device_/dev/xxx_not_initialized_in_udev_database_even_after_waiting_10000000_microseconds).

Use a ferramenta *grub-mkconfig* para gerar `/boot/grub/grub.cfg`:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Por padrão, os scripts de geração adicionam automaticamente entradas de menu para todos os [kernels](/index.php/Kernel_(Portugu%C3%AAs) "Kernel (Português)") do Arch Linux instalados na configuração gerada.

**Dica:**

*   Depois de instalar ou remover um [kernel](/index.php/Kernel_(Portugu%C3%AAs) "Kernel (Português)"), você só precisa executar novamente o comando acima, o *grub-mkconfig*.
*   Para obter dicas sobre o gerenciamento de várias entradas do GRUB, por exemplo, ao usar os kernels [linux](https://www.archlinux.org/packages/?name=linux) e [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), consulte [GRUB/Tips and tricks#Multiple entries](/index.php/GRUB/Tips_and_tricks#Multiple_entries "GRUB/Tips and tricks").

Para adicionar automaticamente entradas para outros sistemas operacionais instalados, consulte [#Detectando outros sistemas operacionais](#Detectando_outros_sistemas_operacionais).

Você pode adicionar entradas adicionais ao menu editando `/etc/grub.d/40_custom` e regerando `/boot/grub/grub.cfg`. Ou você pode criar `/boot/grub/custom.cfg` e adicioná-las lá. Alterações no `/boot/grub/custom.cfg` não requerem reexecução do *grub-mkconfig*, já que `/etc/grub.d/41_custom` adiciona a declaração `source` para o arquivo de configuração gerado.

**Dica:** `/etc/grub.d/40_custom` pode ser usado como um modelo para criar `/etc/grub.d/*nn*_custom`, sendo que `*nn*` define a precedência, indicando a ordem em que o script é executado. Os scripts de ordem são executados e determinam o posicionamento no menu de inicialização do GRUB. `*nn*` deve ser maior que `06` para garantir que os scripts necessários sejam executados primeiro.

Veja [#Exemplos de entrada de menu de boot](#Exemplos_de_entrada_de_menu_de_boot) para mais exemplos de entradas de menu personalizadas.

#### Detectando outros sistemas operacionais

Para fazer com que o *grub-mkconfig* procure por outros sistemas instalados e adicioná-los automaticamente ao menu, [instale](/index.php/Instale "Instale") o pacote [os-prober](https://www.archlinux.org/packages/?name=os-prober) e [monte](/index.php/Mount "Mount") as partições que contêm as outras sistemas. Então, execute novamente o *grub-mkconfig*.

##### MS Windows

Frequentemente, as partições contendo o Windows serão descobertas automaticamente pelo [os-prober](https://www.archlinux.org/packages/?name=os-prober). No entanto, as partições NTFS nem sempre podem ser detectadas quando montadas com os drivers Linux padrão. Se o GRUB não estiver detectando-a, tente instalar o [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) e remontá-la.

Partições encriptadas do Windows podem precisar ser descriptografadas antes da montagem. Para o BitLocker, isso pode ser feito com [dislocker](https://aur.archlinux.org/packages/dislocker/). Isso deve ser suficiente para o [os-prober](https://www.archlinux.org/packages/?name=os-prober) adicionar a entrada correta.

#### Argumentos adicionais

Para passar argumentos adicionais personalizados para a imagem do Linux, você pode definir as variáveis `GRUB_CMDLINE_LINUX` e `GRUB_CMDLINE_LINUX_DEFAULT` em `/etc/default/grub`. As duas são anexadas uma à outra e passadas ao kernel ao gerar entradas de inicialização comuns. Para a entrada de inicialização de *recuperação*, apenas `GRUB_CMDLINE_LINUX` é usado na geração.

Não é necessário usar ambos, mas pode ser útil. Por exemplo, você poderia usar `GRUB_CMDLINE_LINUX_DEFAULT="resume=UUID=*uuid-da-partição-swap* quiet"`, sendo `*uuid-da-partição-swap*` o [UUID](/index.php/UUID_(Portugu%C3%AAs) "UUID (Português)") da sua partição swap para permitir a continuação após [hibernação](/index.php/Hibernation "Hibernation"). Isso geraria uma entrada de inicialização de recuperação sem o resumo e sem `quiet` para suprimir mensagens do kernel durante uma inicialização a partir dessa entrada de menu. Porém, as outras entradas de menu (comuns) os teriam como opções.

Por padrão, o *grub-mkconfig* determina o [UUID](/index.php/UUID_(Portugu%C3%AAs) "UUID (Português)") do sistema de arquivos raiz para a configuração. Para desabilitar isso, descomente `GRUB_DISABLE_LINUX_UUID=true`.

Para gerar a entrada de recuperação do GRUB, você precisa garantir que `GRUB_DISABLE_RECOVERY` não esteja definido como `true` em `/etc/default/grub`.

Veja [Parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") para mais informações.

#### LVM

**Atenção:** O GRUB não possui suporte a volumes lógicos *thin-provisioned*.

Se você usa [LVM](/index.php/LVM "LVM") para sua partição `/boot` ou `/`, certifique-se de que o módulo `lvm` esteja pré-carregado:

 `/etc/default/grub`  `GRUB_PRELOAD_MODULES="... lvm"` 

#### RAID

O GRUB fornece um manuseio conveniente de volumes [RAID](/index.php/RAID "RAID"). Você precisa carregar os módulos GRUB `mdraid09` ou `mdraid1x` para permitir que você aborde o volume nativamente:

 `/etc/default/grub`  `GRUB_PRELOAD_MODULES="... mdraid09 mdraid1x"` 

Por exemplo, `/dev/md0` se torna:

```
set root=(md/0)

```

sendo que um volume RAID particionado (p.ex., `/dev/md0p1`) se torna:

```
set root=(md/0,1)

```

Para instalar o grub ao usar o RAID1 como partição `/boot` (ou usando `/boot` alojado em uma partição raiz RAID1), nos sistemas BIOS, simplesmente execute o *grub-install* em ambas as unidades, como:

```
# grub-install --target=i386-pc --debug /dev/sda
# grub-install --target=i386-pc --debug /dev/sdb

```

sendo que o vetor RAID 1 contendo `/boot` está contido em ambos `/dev/sda` e `/dev/sdb`.

**Nota:** GRUB possui suporte a inicializar de RAID 0/1/10 com [Btrfs](/index.php/Btrfs "Btrfs"), mas *não* RAID 5/6\. Você pode usar [mdadm](/index.php/Mdadm "Mdadm") para RAID 5/6, o qual possui suporte no GRUB.

#### /boot criptografado

O GRUB também tem suporte especial para inicializar com um `/boot` criptografado. Isto é feito desbloqueando um dispositivo de bloco [LUKS](/index.php/LUKS_(Portugu%C3%AAs) "LUKS (Português)") para ler sua configuração e carregar qualquer [initramfs](/index.php/Initramfs_(Portugu%C3%AAs) "Initramfs (Português)") e [kernel](/index.php/Kernel_(Portugu%C3%AAs) "Kernel (Português)") dele. Esta opção tenta resolver o problema de ter uma [partição de inicialização não criptografada](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties").

**Nota:** `/boot` **não** precisa obrigatoriamente ser mantido em uma partição separada; ele também pode ficar sob a árvore de diretórios `/` da raiz do sistema.

**Atenção:** O GRUB não possui suporte a cabeçalhos LUKS2; veja [bug #55093 do GRUB](https://savannah.gnu.org/bugs/?55093). Certifique-se de especificar `--type luks1` ao criar a partição criptografada usando `cryptsetup luksFormat`.

Para ativar este recurso, criptografe a partição com `/boot` que reside nela usando [LUKS](/index.php/LUKS_(Portugu%C3%AAs) "LUKS (Português)") normalmente. Em seguida, adicione a seguinte opção para `/etc/default/grub`:

 `/etc/default/grub`  `GRUB_ENABLE_CRYPTODISK=y` 

Esta opção é usada pelo grub-install para gerar o grub `core.img`, então certifique-se de [instalar o grub](#Instalação) depois de modificar esta opção.

Sem mais alterações, você será solicitado duas vezes a informar um código de acesso: o primeiro para o GRUB desbloquear o ponto de montagem `/boot` na incialização, o segundo para desbloquear o sistema de arquivos raiz como implementado pelo initramfs. Você pode usar um [initramfs](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption") para evitar isso.

**Atenção:**

*   Se você quiser [gerar o arquivo de configuração principal](#Gerar_o_arquivo_de_configuração_principal), certifique-se de que `/boot` esteja montado.
*   Para realizar atualizações do sistema envolvendo o ponto de montagem `/boot`, certifique-se de que o `/boot` criptografado esteja desbloqueado e montado antes de executar uma atualização. Com uma partição `/boot` separada, isso pode ser feito automaticamente na inicialização usando [crypttab](/index.php/Crypttab "Crypttab") com um [arquivo chave](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption").

**Nota:**

*   Se você usar um mapa de teclado especial, uma instalação padrão do GRUB não o saberá. Isso é relevante para saber como inserir a frase secreta para desbloquear o dispositivo de bloco LUKS.
*   Se você tiver problemas para obter a solicitação de uma senha (erros relacionados a cryptouuid, cryptodisk ou "dispositivo não encontrado"), tente reinstalar o GRUB e acrescentar `--modules="part_gpt part_msdos"` ao final do seu comando `grub-install`.

**Dica:** Você pode usar [hooks do pacman](https://bbs.archlinux.org/viewtopic.php?id=234607) para montar automaticamente o seu `/boot` quando as atualizações precisarem acessar arquivos relacionados.

### grub.cfg personalizado

Esta seção descreve a criação manual de entradas de inicialização do GRUB em `/boot/grub/grub.cfg` em vez de confiar em *grub-mkconfig*.

Um arquivo de configuração básico do GRUB usa as seguintes opções:

*   `(hd*X*,*Y*)` é a partição *Y* no disco *X*, números de partição iniciando em 1, números de disco iniciando em 0
*   `set default=*N*` é a entrada de inicialização padrão que é escolhida após atingido um tempo limite para ação do usuário
*   `set timeout=*M*` é o tempo *M* para aguardar em segundos para uma seleção de usuário antes da padrão ser inicializada
*   `menuentry "título" {opções desta entrada}` é uma entrada padrão chamada `título`
*   `set root=(hd*X*,*Y*)` define a partição de inicialização, onde os módulos de kernel e GRUB estão armazenados (o boot não precisa estar em uma partição separada e pode simplesmente ser um diretório sob a partição "root" (`/`)

#### Exemplos de entrada de menu de boot

**Dica:** Essas entradas de inicialização também podem ser usadas ao usar um `/boot/grub/grub.cfg` gerado pelo "grub-mkconfig". Adicione-os a `/etc/grub.d/40_custom` e [gere novamente o arquivo de configuração principal](#Gerar_o_arquivo_de_configuração_principal) ou adicione-os a `/boot/grub/custom.cfg`.

Para obter dicas sobre o gerenciamento de várias entradas do GRUB, por exemplo, ao usar os kernels [linux](https://www.archlinux.org/packages/?name=linux) e [linux-lts](https://www.archlinux.org/packages/?name=linux-lts), consulte [GRUB/Tips and tricks#Multiple entries](/index.php/GRUB/Tips_and_tricks#Multiple_entries "GRUB/Tips and tricks").

Para entradas de menu de inicialização de [Archiso](/index.php/Archiso_(Portugu%C3%AAs) "Archiso (Português)") e [Archboot](/index.php/Archboot "Archboot"), veja [Multiboot USB drive#Boot entries](/index.php/Multiboot_USB_drive#Boot_entries "Multiboot USB drive").

##### Comandos do GRUB

###### Entrada de menu "Desligar"

```
menuentry "Desligamento do sistema" {
	echo "Desligando o sistema..."
	halt
}

```

###### Entrada de menu "Reiniciar"

```
menuentry "Reinicialização do sistema" {
	echo "Reinicializando o sistema..."
	reboot
}

```

###### Entrada de menu "Configuração do firmware" (UEFI apenas)

```
if [ ${grub_platform} == "efi" ]; then
	menuentry "Configuração do firmware" {
		fwsetup
	}
fi
```

##### Binarios de EFI

Ao iniciar o modo UEFI, o GRUB pode carregar outros binários EFI.

**Dica:** Para mostrar essas entradas de menu somente quando o GRUB é iniciado no modo UEFI, coloque-as na seguinte instrução `if`:
```
if [ ${grub_platform} == "efi" ]; then
	*coloque apenas entradas de menu UEFI aqui*
fi
```

###### Shell de UEFI

Você pode iniciar o [UEFI Shell](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface") colocando-a na raiz da [partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") e adicionando esta entrada de menu:

```
menuentry "UEFI Shell" {
	insmod fat
	insmod chain
	search --no-floppy --set=root --file /shellx64.efi
	chainloader /shellx64.efi
}
```

###### gdisk

Baixe o [aplicativo EFI gdisk](/index.php/Gdisk#gdisk_EFI_application "Gdisk") e copie `gdisk_x64.efi` para `*esp*/EFI/tools/`.

```
menuentry "gdisk" {
	insmod fat
	insmod chain
	search --no-floppy --set=root --file /EFI/tools/gdisk_x64.efi
	chainloader /EFI/tools/gdisk_x64.efi
}
```

###### Carregando um arquivo .efi do Arch Linux

Se você tiver um arquivo *.efi* gerado a partir de [Secure Boot](/index.php/Secure_Boot "Secure Boot") ou outro meio, você pode adicioná-lo ao menu de inicialização. Por exemplo:

```
menuentry "Arch Linux .efi" {
	insmod fat
	insmod chain
	search --no-floppy --set=root --fs-uuid *UUID_SISTEMA_DE_ARQUIVOS*
	chainloader /EFI/arch/vmlinuz.efi
}
```

##### Dual boot

###### GNU/Linux

Presumindo que outra distribuição esteja na partição `sda2`:

```
menuentry "Outro Linux" {
	set root=(hd0,2)
	linux /boot/vmlinuz (adicione outras opções aqui conforme necessário)
	initrd /boot/initrd.img (se outro kernel usa/precisa de um)
}
```

Alternativamente, permita o GRUB pesquisar a partição correta pelo *UUID* ou *label*:

```
menuentry "Outro Linux" {
        # presumindo que o UUID seja 763A-9CB6
	search --no-floppy --set=root --fs-uuid 763A-9CB6

        # pesquise pelo rótulo OUTRO_LINUX (certifique-se que o rótulo da partição não seja ambígua)
        #search --no-floppy --set=root --label OUTRO_LINUX

	linux /boot/vmlinuz (adicione aqui outras opções necessárias, por exemplo: root=UUID=763A-9CB6)
	initrd /boot/initrd.img (se outro kernel usa/precisa de um)
}
```

###### Windows instalado em modo UEFI/GPT

Este modo determina onde o carregador de boot do Windows reside e carrega-o após o GRUB quando a entrada do menu é selecionada. A principal tarefa aqui é encontrar a partição do sistema EFI e executar o carregador de boot a partir dela.

**Nota:** Este entrada de menu funcionará apenas no modo de inicialização UEFI e somente se o *bitness* do Windows corresponder ao *bitstream* do UEFI. Não funcionará no GRUB instalado na BIOS. Veja [Dual boot with Windows#Windows UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Windows_UEFI_vs_BIOS_limitations "Dual boot with Windows") e [Dual boot with Windows#Bootloader UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Bootloader_UEFI_vs_BIOS_limitations "Dual boot with Windows") para mais informações.

```
if [ "${grub_platform}" == "efi" ]; then
	menuentry "Microsoft Windows Vista/7/8/8.1 UEFI/GPT" {
		insmod part_gpt
		insmod fat
		insmod chain
		search --no-floppy --fs-uuid --set=root $hints_string $fs_uuid
		chainloader /EFI/Microsoft/Boot/bootmgfw.efi
	}
fi
```

sendo que `$hints_string` e `$fs_uuid` são obtidas com os dois comandos abaixo.

O comando `$fs_uuid` determina o UUID da partição de sistema EFI:

 `# grub-probe --target=fs_uuid *esp*/EFI/Microsoft/Boot/bootmgfw.efi`  `1ce5-7f28` 

Como alternativa, é possível executar `blkid` (como root) e ler o UUID da partição do sistema EFI a partir dele.

O comando `$hints_string` determinará a localização da partição do sistema EFI, neste caso o disco rígido 0:

 `# grub-probe --target=hints_string *esp*/EFI/Microsoft/Boot/bootmgfw.efi`  `--hint-bios=hd0,gpt1 --hint-efi=hd0,gpt1 --hint-baremetal=ahci0,gpt1` 

Estes dois comandos presumem o uso da ESP do Windows montada em `*esp*`. Pode haver diferenças entre maiúsculas e minúsculas no caminho para o arquivo EFI do Windows, com o Windows e tudo mais.

###### Windows instalado em modo BIOS/MBR

**Nota:** O GRUB possui suporte a inicializar `bootmgr` diretamente e fazer carregamento em cadeia ([*chainloading*](https://www.gnu.org/software/grub/manual/grub.html#Chain_002dloading)) do setor de inicialização da partição não é mais necessário para inicializar Windows em uma configuração de BIOS/MBR.

**Atenção:** É a **partição do sistema** que tem `/bootmgr`, não sua partição Windows "real" (geralmente `C:`). O [rótulo do sistema de arquivos](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco#by-label "Nomeação persistente de dispositivo de bloco") da partição do sistema é `Sistema Reservado` ou `SISTEMA` e a partição tem por volta de 100 para 549 MiB em tamanho. Veja [Wikipedia:System partition and boot partition](https://en.wikipedia.org/wiki/System_partition_and_boot_partition "wikipedia:System partition and boot partition") para mais informações.

Ao longo desta seção, presume-se que sua partição do Windows é `/dev/sda1`. Uma partição diferente mudará todas as instâncias de `hd0,msdos1`.

**Nota:** Este entrada de menu funcionará apenas no modo de inicialização BIOS. Não funcionará no GRUB instalado na UEFI. Veja [Dual boot with Windows#Windows UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Windows_UEFI_vs_BIOS_limitations "Dual boot with Windows") e [Dual boot with Windows#Bootloader UEFI vs BIOS limitations](/index.php/Dual_boot_with_Windows#Bootloader_UEFI_vs_BIOS_limitations "Dual boot with Windows") .

Em ambos exemplos `*XXXXXXXXXXXXXXXX*` é o UUID do sistema de arquivos que pode ser encontrado com o comando `lsblk --fs`.

Para Windows Vista/7/8/8.1/10:

```
if [ "${grub_platform}" == "pc" ]; then
	menuentry "Microsoft Windows Vista/7/8/8.1/10 BIOS/MBR" {
		insmod part_msdos
		insmod ntfs
		insmod ntldr
		search --no-floppy --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 *XXXXXXXXXXXXXXXX*
		ntldr /bootmgr
	}
fi
```

Para Windows XP:

```
if [ "${grub_platform}" == "pc" ]; then
	menuentry "Microsoft Windows XP" {
		insmod part_msdos
		insmod ntfs
		insmod ntldr     
		search --no-floppy --fs-uuid --set=root --hint-bios=hd0,msdos1 --hint-efi=hd0,msdos1 --hint-baremetal=ahci0,msdos1 *XXXXXXXXXXXXXXXX*
		ntldr /ntldr
	}
fi
```

**Nota:** Em alguns casos, o GRUB pode ser instalado sem um Windows 8 limpo, caso em que você não consegue inicializar o Windows sem ter um erro com `\boot\bcd` (código de erro `0xc000000f`). Você pode consertá-lo indo até o Console de Recuperação do Windows (`cmd.exe` do disco de instalação) e executando:
```
X:\> bootrec.exe /fixboot
X:\> bootrec.exe /RebuildBcd

```

**Não** use `bootrec.exe /Fixmbr` porque ele apagará o GRUB. Ou você pode usar a função "Reparo de inicialização" no menu "Solução de problemas" - isso não eliminará o GRUB, mas consertará a maioria dos erros. Além disso, é melhor você ficar conectado tanto no disco rígido de destino quanto no dispositivo inicializável **SOMENTE**. O Windows geralmente não conserta as informações de inicialização se algum outro dispositivo estiver conectado.

## Usando o shell de comandos

Como o MBR é muito pequeno para armazenar todos os módulos do GRUB, apenas o menu e alguns comandos básicos residem nele. A maior parte da funcionalidade do GRUB permanece nos módulos em `/boot/grub/`, que são inseridos conforme necessário. Em condições de erro (por exemplo, se o layout da partição for alterado), o GRUB poderá falhar na inicialização. Quando isso acontece, um shell de comando pode aparecer.

O GRUB oferece vários shells/prompts. Se houver um problema ao ler o menu, mas o gerenciador de inicialização conseguir localizar o disco, você provavelmente será descartado no shell "normal":

```
grub>

```

Se houver um problema mais sério (por exemplo, o GRUB não conseguir localizar os arquivos necessários), você poderá ser direcionado para o shell "rescue":

```
grub rescue>

```

O shell de recuperação é um subconjunto restrito do shell normal, oferecendo muito menos funcionalidade. Se for jogado no shell de recuperação, primeiro tente inserir o módulo "normal" e, em seguida, inicie o shell "normal":

```
grub rescue> set prefix=(hdX,Y)/boot/grub
grub rescue> insmod (hdX,Y)/boot/grub/i386-pc/normal.mod
rescue:grub> normal

```

### Suporte a paginador

O GRUB possui suporte a paginador para ler comandos que fornecem saída longa (como o comando `help`). Isso funciona apenas no modo shell normal e não no modo de recuperação. Para digitar o paginador, digite no shell de comando do GRUB:

```
sh:grub> set pager=1

```

### Usando o ambiente shell de comandos para iniciar sistemas operacionais

```
grub>

```

O ambiente de shell de comando do GRUB pode ser usado para inicializar sistemas operacionais. Um cenário comum pode ser inicializar o Windows/Linux armazenado em uma unidade/partição via **carregamento em cadeia** (*chainloading*).

*Chainloading* significa carregar outro carregador de boot a partir do atual, isto é, carregamento em cadeia.

O outro gerenciador de boot pode ser incorporado no início de um disco particionado (MBR), no início de uma partição ou em um disco sem partição (VBR) ou como um binário EFI no caso de UEFI.

#### Carregando o VBR de uma partição

```
set root=(hdX,Y)
chainloader +1
boot

```

X=0,1,2... Y=1,2,3...

Por exemplo, para carregar o Windows armazenado na primeira partição do primeiro disco rígido,

```
set root=(hd0,1)
chainloader +1
boot

```

Da mesma forma, o GRUB instalado em uma partição pode ser carregado em cadeia.

#### Carregando o MBR de um disco ou o VBR de um disco sem partição

```
set root=hdX
chainloader +1
boot

```

#### Carregando Windows/Linux instalado em modo UEFI

```
insmod fat
set root=(hd0,gpt4)
chainloader (${root})/EFI/Microsoft/Boot/bootmgfw.efi
boot

```

`insmod fat` é usado para carregar o módulo do sistema de arquivos FAT para acessar o gerenciador de boot do Windows na partição do sistema EFI. `(hd0,gpt4)` ou `/dev/sda4` é a partição do sistema EFI neste exemplo. A entrada na linha `chainloader` especifica o caminho do arquivo *.efi* a ser carregado em cadeia.

#### Carregamento normal

Veja os exemplos em [#Usando o console de recuperação](#Usando_o_console_de_recuperação)

### Usando o console de recuperação

Veja [#Usando o shell de comandos](#Usando_o_shell_de_comandos) primeiro. Se não for possível ativar o shell padrão, uma solução possível é inicializar usando um live CD ou algum outro disco de recuperação para corrigir erros de configuração e reinstalar o GRUB. No entanto, esse disco de inicialização nem sempre está disponível (nem necessário); o console de recuperação é surpreendentemente robusto.

Os comandos disponíveis na recuperação do GRUB incluem `insmod`, `ls`, `set` e `unset`. Este exemplo usa `set` e `insmod`. `set` modifica variáveis e `insmod` insere novos módulos para adicionar funcionalidade.

Antes de iniciar, o usuário deve saber a localização de sua partição `/boot` (seja uma partição separada ou um subdiretório sob sua raiz):

```
grub rescue> set prefix=(hd*X*,*Y*)/boot/grub

```

sendo `*X*` o número da unidade física e `*Y*` o número da partição.

**Nota:** Com uma partição de inicialização separada, omita `/boot` do caminho (por exemplo, digite `set prefix=(hd*X*,*Y*)/grub`).

Para expandir as capacidades do console, insira o módulo `linux`:

```
grub rescue> insmod i386-pc/linux.mod

```

ou simplesmente

```
grub rescue> insmod linux

```

Isso introduz os comandos `linux` e `initrd`, que devem ser familiares.

Um exemplo, inicializando o Arch Linux:

```
set root=(hd0,5)
linux /boot/vmlinuz-linux root=/dev/sda5
initrd /boot/initramfs-linux.img
boot

```

Com uma partição de inicialização separada (por exemplo, ao usar UEFI), altere as linhas novamente:

**Note:** Como a inicialização é uma partição separada e não faz parte da sua partição raiz, você deve endereçar a partição de inicialização manualmente, da mesma maneira que a variável de prefixo.

```
set root=(hd0,5)
linux (hd*X*,*Y*)/vmlinuz-linux root=/dev/sda6
initrd (hd*X*,*Y*)/initramfs-linux.img
boot

```

**Nota:** Se você obteve a mensagem o `error: fim prematuro do arquivo /NOME_DO_SEU_KERNEL` durante a execução do comando `linux`, você pode tentar `linux16`.

Após inicializar com êxito a instalação do Arch Linux, os usuários podem corrigir o `grub.cfg` conforme necessário e reinstalar o GRUB.

Para reinstalar o GRUB e corrigir o problema completamente, altere `/dev/sda`, se necessário. Veja [#Instalação](#Instalação) para detalhes.

## Remoção do GRUB

Após migrar para o GPT/UEFI, pode-se querer remover o [código de inicialização de MBR](/index.php/Partitioning#Master_Boot_Record_(bootstrap_code) "Partitioning") [usando dd](/index.php/Dd_(Portugu%C3%AAs)#Remover_o_gerenciador_de_boot "Dd (Português)"):

```
# dd if=/dev/zero of=/dev/sd*X* bs=440 count=1

```

## Solução de problemas

### F2FS e outros sistemas de arquivos sem suporte

O GRUB não possui suporte ao sistema de arquivos [F2FS](/index.php/F2FS "F2FS"). Caso a partição raiz esteja em um sistema de arquivos incompatível, uma partição alternativa `/boot` com um sistema de arquivos compatível deve ser criada. Em alguns casos, a versão de desenvolvimento do GRUB [grub-git](https://aur.archlinux.org/packages/grub-git/) pode ter suporte nativo para o sistema de arquivos.

Se o GRUB é usado com um sistema de arquivos incompatível, ele não é capaz de extrair o [UUID](/index.php/UUID_(Portugu%C3%AAs) "UUID (Português)") da sua unidade, então ele usa nomes clássicos não-persistentes `/dev/*sdXx*`. Nesse caso, você pode ter que editar manualmente `/boot/grub/grub.cfg` e substituir `root=/dev/*sdXx*` com `root=UUID=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX*`. Você pode usar o comando `blkid` para obter o UUID do seu dispositivo, consulte [Nomeação persistente de dispositivo de bloco](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco "Nomeação persistente de dispositivo de bloco").

### BIOS da Intel não está inicialização GPT

Alguns BIOS da Intel exigem que pelo menos uma partição MBR inicializável esteja presente na inicialização, fazendo com que as configurações de inicialização particionadas por GPT não sejam iniciadas.

Isto pode ser contornado usando, por exemplo, fdisk para marcar uma das partições GPT (preferencialmente a partição 1007 KiB que você criou para o GRUB já) inicializável no MBR. Isto pode ser conseguido, usando fdisk, pelos seguintes comandos: Inicie o fdisk no disco que você está instalando, por exemplo `fdisk/dev/sda`, então pressione `a` e selecione a partição que você Para marcar como inicializável (provavelmente #1) pressionando o número correspondente, finalmente pressione `w` para escrever as alterações no MBR.

**Nota:** A marcação inicializável deve ser feita em `fdisk` ou similar, não no GParted ou em outros, pois eles não configurarão o sinalizador de inicialização no MBR.

Com o cfdisk, as etapas são semelhantes, apenas `cfdisk/dev/sda`, escolha inicializável (à esquerda) no disco rígido desejado e saia do salvamento.

Com a versão recente do parted, você pode usar a opção `disk_toggle pmbr_boot`. Em seguida, verifique se as "Opções de disco" mostram pmbr_boot.

```
# parted /dev/sd*x* disk_toggle pmbr_boot
# parted /dev/sd*x* print

```

Mais informações estão disponíveis [aqui](http://www.rodsbooks.com/gdisk/bios.html).

### Habilitar mensagens de depuração

**Nota:** Essas mudanças são sobrescritas ao [#Gerar o arquivo de configuração principal](#Gerar_o_arquivo_de_configuração_principal).

Adicionar:

```
set pager=1
set debug=all

```

para `grub.cfg`.

### Erro "No suitable mode found"

Se você receber este erro ao inicializar qualquer entrada de menu:

```
error: no suitable mode found
Booting however

```

Então, você precisa inicializar o terminal gráfico do GRUB (`gfxterm`) com o modo de vídeo apropriado (`gfxmode`) no GRUB. Este modo de vídeo é passado pelo GRUB para o kernel do Linux via "gfxpayload". No caso de sistemas UEFI, se o modo de vídeo GRUB não for inicializado, nenhuma mensagem de inicialização do kernel será mostrada no terminal (pelo menos até o KMS entrar em ação).

Copie `/usr/share/grub/unicode.pf2` para `${GRUB_PREFIX_DIR` (`/boot/grub/` no caso de sistemas BIOS e UEFI). Se GRUB UEFI foi instalado com `--boot-directory=*esp*/EFI` definido, então o diretório é `*esp*/EFI/grub/`:

```
# cp /usr/share/grub/unicode.pf2 ${GRUB_PREFIX_DIR}

```

Se `/usr/share/grub/unicode.pf2` não existe, instale [bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont), crie o arquivo `unifont.pf2` e, então, copie-o para `${GRUB_PREFIX_DIR}`:

```
# grub-mkfont -o unicode.pf2 /usr/share/fonts/misc/unifont.bdf

```

Em seguida, no arquivo `grub.cfg`, adicione as seguintes linhas para permitir que o GRUB passe o modo de vídeo corretamente para o kernel, sem o qual você só obterá uma tela preta (sem saída), mas reiniciando prossegue com sucesso sem nenhum travamento do sistema.

Depois disso, adicione o seguinte código (comum ao BIOS e ao UEFI):

```
loadfont "unicode"
set gfxmode=auto
set gfxpayload=keep
insmod all_video
insmod gfxterm
terminal_output gfxterm
```

### Mensagem de erro sobre estilo msdos

```
grub-setup: warn: Este rótulo de partição estilo msdos não tem espaço vago pós-MBR; não será possível embuti-lo!
grub-setup: warn: Incorporação não permitida. O GRUB só pode ser instalado neste setup usando blocklists.
            Porém. blocklists são INSTÁVEIS e seu uso não é aconselhado.
grub-setup: error: If you really want blocklists, use --force.

```

Este erro pode ocorrer quando você tenta instalar o GRUB em um contêiner VMware. Leia mais sobre isso [aqui](https://bbs.archlinux.org/viewtopic.php?pid=581760#p581760). Isso acontece quando a primeira partição começa logo após o MBR (bloco 63), sem o espaço usual de 1 MiB (2048 blocos) antes da primeira partição. Leia [#Instruções específicas de Master Boot Record (MBR)](#Instruções_específicas_de_Master_Boot_Record_(MBR)).

### UEFI

#### Erros comuns de instalação

*   Se você tiver um problema ao executar o *grub-install* com *sysfs* ou *procfs* e ele disser que você deve executar `modprobe efivarfs`, tente [Unified Extensible Firmware Interface#Mount efivarfs](/index.php/Unified_Extensible_Firmware_Interface#Mount_efivarfs "Unified Extensible Firmware Interface").
*   Sem a opção `--target` ou `--directory`, o grub-install não pode determinar qual firmware deve ser instalado. Em tais casos, `grub-install` irá imprimir `source_dir não existe. Por favor, especifique --target ou --diretório`.
*   Se, depois de executar o grub-install, for informado que sua partição não se parece com uma partição EFI, a partição provavelmente não é `Fat32`.

#### Descartar o shell de recuperação

Se o GRUB for carregado, mas cair no shell de recuperação sem erros, pode ser devido a um destes dois motivos:

*   Pode ser por causa de um `grub.cfg` ausente ou extraviado. Isso acontecerá se o UEFI do GRUB tiver sido instalado com `--boot-directory` e `grub.cfg` estiver faltando,
*   Isso também acontece se a partição de inicialização, que é codificada no arquivo `grubx64.efi`, for alterada.

#### UEFI do GRUB não carregado

Um exemplo de um UEFI funcional:

 `# efibootmgr -v` 
```
BootCurrent: 0000
Timeout: 3 seconds
BootOrder: 0000,0001,0002
Boot0000* GRUB HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\EFI\GRUB\grubx64.efi)
Boot0001* Shell HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\shellx64.efi)
Boot0002* Festplatte BIOS(2,0,00)P0: SAMSUNG HD204UI

```

Se a tela ficar preta por um segundo e a próxima opção de inicialização for tentada posteriormente, de acordo com [esta publicação](https://bbs.archlinux.org/viewtopic.php?pid=981560#p981560), mova o GRUB para a raiz da partição pode ajudar. A opção de inicialização deve ser excluída e recriada posteriormente. A entrada para o GRUB deve ficar assim:

```
Boot0000* GRUB HD(1,800,32000,23532fbb-1bfa-4e46-851a-b494bfe9478c)File(\grubx64.efi)

```

#### Caminho de inicialização padrão/reserva

Alguns firmwares UEFI exigem um arquivo inicializável em um local conhecido antes de mostrar as entradas de inicialização da UEFI NVRAM. Se este for o caso, `grub-install` irá reivindicar que `efibootmgr` adicionou uma entrada para inicializar o GRUB, no entanto a entrada não será mostrada no seletor de ordem de inicialização do VisualBIOS. A solução é instalar o GRUB no caminho de inicialização padrão/reserva:

```
# grub-install --target=x86_64-efi --efi-directory=*esp* **--removable**

```

Alternativamente, você pode mover um executável do GRUB EFI já instalado para o caminho padrão/reserva:

```
# mv *esp*/EFI/grub *esp*/EFI/BOOT
# mv *esp*/EFI/BOOT/grubx64.efi *esp*/EFI/BOOT/BOOTX64.EFI

```

### Assinatura inválida

Se tentar inicializar o Windows, resulta em um erro de "assinatura inválida", por exemplo, depois de reconfigurar partições ou adicionar discos rígidos adicionais, (re)mova a configuração do dispositivo do GRUB e reconfigure:

```
# mv /boot/grub/device.map /boot/grub/device.map-old
# grub-mkconfig -o /boot/grub/grub.cfg

```

`grub-mkconfig` agora deve mencionar todas as opções de inicialização encontradas, incluindo o Windows. Se funcionar, remova `/boot/grub/device.map-old`.

### Inicialização congelando

Se a inicialização for travada sem nenhuma mensagem de erro após o GRUB carregar o kernel e o disco em memória inicial, tente remover o parâmetro do kernel `add_efi_memmap`.

### Arch não encontrado por outros sistemas operacionais

Algumas pessoas relataram que outras distribuições podem ter problemas para encontrar o Arch Linux automaticamente com `os-prober`. Se esse problema ocorrer, foi relatado que a detecção pode ser melhorada com a presença de `/etc/lsb-release`. Esta ferramenta de arquivo e atualização está disponível com o pacote [lsb-release](https://www.archlinux.org/packages/?name=lsb-release).

### Aviso ao instalar em chroot

Ao instalar o GRUB em um sistema LVM em um ambiente chroot (por exemplo, durante a instalação do sistema), você pode receber avisos como

```
/run/lvm/lvmetad.socket: connect failed: No such file or directory

```

ou

```
WARNING: failed to connect to lvmetad: No such file or directory. Falling back to internal scanning.

```

Isto é porque `/run` não está disponível dentro do chroot. Esses avisos não impedem o sistema de inicializar, desde que tudo tenha sido feito corretamente, assim você pode continuar com a instalação.

### GRUB carrega lentamente

O GRUB pode levar muito tempo para carregar quando o espaço em disco está baixo. Verifique se você tem espaço livre em disco suficiente em sua partição `/boot` ou `/` quando tiver problemas.

### erro: sistema de arquivos desconhecido

O GRUB pode emitir `erro: sistema de arquivos desconhecido` e se recusar a inicializar por alguns motivos. Se você tem certeza de que todos os [UUIDs](/index.php/UUID_(Portugu%C3%AAs) "UUID (Português)") estão corretos e todos os sistemas de arquivos são válidos e compatíveis, pode ser que sua [partição de inicialização de BIOS](#Instruções_específicas_de_Tabela_de_Partição_GUID_(GPT)) esteja localizada fora dos primeiros 2 TiB da unidade [[2]](https://bbs.archlinux.org/viewtopic.php?id=195948). Use uma ferramenta de particionamento de sua escolha para garantir que essa partição esteja totalmente localizada nos primeiros 2 TiB, depois reinstale e reconfigure o GRUB.

Esse erro também pode ser causado por um sistema de arquivos [ext4](/index.php/Ext4_(Portugu%C3%AAs) "Ext4 (Português)") com os recursos `large_dir` ou `metadata_csum_seed` definidos.

### grub-reboot não está redefinido

O GRUB parece não conseguir gravar em partições BTRFS de raiz [[3]](https://bbs.archlinux.org/viewtopic.php?id=166131). Se você usar o grub-reboot para inicializar em outra entrada, será incapaz de atualizar seu ambiente em disco. Execute o grub-reboot a partir da outra entrada (por exemplo, ao alternar entre várias distribuições) ou considere um sistema de arquivos diferente. Você pode redefinir uma entrada "sticky" executando `grub-editenv create` e configurando `GRUB_DEFAULT=0` no `/etc/default/grub` (não esqueça `grub-mkconfig -o /boot/grub/grub.cfg`).

### BTRFS antigo impede a instalação

Se uma unidade estiver formatada com o BTRFS sem criar uma tabela de partição (por exemplo, `/dev/sdx`), mais tarde será gravada a tabela de partições, existindo partes do formato BTRFS que persistem. A maioria dos utilitários e sistemas operacionais não vê isso, mas o GRUB se recusará a instalar, mesmo com `--force`.

```
# grub-install: warning: Attempting to install GRUB to a disk with multiple partition labels. This is not supported yet.
# grub-install: error: filesystem `btrfs' does not support blocklists.

```

Você pode zerar a unidade, mas a solução fácil que deixa seus dados sozinhos é apagar o superbloco BTRFS com `wipefs -o 0x10040 /dev/sdx`.

### Windows 8/10 não encontrado

Uma configuração no Windows 8/10 chamada "Hiberboot", "Hybrid Boot" or "Fast Boot" (inicialização rápida pode impedir que a partição do Windows seja montada, portanto, o `grub-mkconfig` não localizará uma instalação do Windows. Desativar o Hiberboot no Windows permitirá que ele seja adicionado ao menu GRUB.

### Modo EFI no VirtualBox

Instal o GRUB para o [caminho de inicialização padrão/reserva](#Caminho_de_inicialização_padrão/reserva).

Veja também [VirtualBox (Português)#Instalação no modo EFI](/index.php/VirtualBox_(Portugu%C3%AAs)#Instalação_no_modo_EFI "VirtualBox (Português)").

### Device /dev/xxx not initialized in udev database even after waiting 10000000 microseconds

Se o *grub-mkconfig* travar e exibir a mensagem de erro: `WARNING: Device /dev/*xxx* not initialized in udev database even after waiting 10000000 microseconds`, você pode precisar fornecer o acesso a `/run/lvm/` para o ambiente de chroot usando:

```
# mkdir /mnt/hostlvm
# mount --bind /run/lvm /mnt/hostlvm
# arch-chroot /mnt
# ln -s /hostlvm /run/lvm

```

Veja o [FS#61040](https://bugs.archlinux.org/task/61040) e [solução de contorno](https://bbs.archlinux.org/viewtopic.php?pid=1820949#p1820949).

### Recuperação do GRUB e /boot criptografado

Ao usar um [/boot criptografado](#/boot_criptografado) e você não conseguir inserir uma senha correta, você será jogado no prompt de recuperação do GRUB.

Este prompt de recuperação do grub tem capacidades limitadas. Use os seguintes comandos para completar a inicialização:

```
grub rescue> cryptomount <partição>
grub rescue> insmod normal
grub rescue> normal

```

Veja [esta publicação de blog](https://blog.stigok.com/2017/12/30/decrypt-and-mount-luks-disk-from-grub-rescue-mode.html) para uma descrição melhor.

## Veja também

*   [Wikipedia:GNU GRUB](https://en.wikipedia.org/wiki/GNU_GRUB "wikipedia:GNU GRUB")
*   [Manual oficial do GRUB](https://www.gnu.org/software/grub/manual/grub.html)
*   [Página wiki do Ubuntu sobre GRUB](https://help.ubuntu.com/community/Grub2)
*   [Página wiki sobre GRUB descrevendo passos para compilar para sistemas UEFI](https://help.ubuntu.com/community/UEFIBooting)
*   [Wikipedia:BIOS Boot partition](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
*   [Como configurar o GRUB](http://web.archive.org/web/20160424042444/http://members.iinet.net/~herman546/p20/GRUB2%20Configuration%20File%20Commands.html#Editing_etcgrub.d05_debian_theme)
*   [Inicializar com GRUB](http://www.linuxjournal.com/article/4622)
*   [Detectando arquivos efi e iniciando-os a partir do grub](https://forum.manjaro.org/t/detecting-efi-files-and-booting-them-from-grub/38083)