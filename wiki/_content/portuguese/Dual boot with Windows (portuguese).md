Este artigo detalha diferentes formas de se instalar Arch com Windows.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Informação importante](#Informação_importante)
    *   [1.1 Limitações do Windows em UEFI versus BIOS](#Limitações_do_Windows_em_UEFI_versus_BIOS)
    *   [1.2 Limitações da mídia de instalação](#Limitações_da_mídia_de_instalação)
    *   [1.3 Gerenciador de boot UEFI versus limitações do BIOS](#Gerenciador_de_boot_UEFI_versus_limitações_do_BIOS)
    *   [1.4 UEFI Secure Boot](#UEFI_Secure_Boot)
    *   [1.5 Inicialização rápida](#Inicialização_rápida)
    *   [1.6 Limitações de nomes de arquivo no Windows](#Limitações_de_nomes_de_arquivo_no_Windows)
*   [2 Instalação](#Instalação)
    *   [2.1 Windows antes do Linux](#Windows_antes_do_Linux)
        *   [2.1.1 Sistemas BIOS](#Sistemas_BIOS)
            *   [2.1.1.1 Usando um gerenciador de boot para Linux](#Usando_um_gerenciador_de_boot_para_Linux)
            *   [2.1.1.2 Usando o gerenciador de boot do Windows](#Usando_o_gerenciador_de_boot_do_Windows)
                *   [2.1.1.2.1 Gerenciador de boot do Windows Vista/7/8/8.1](#Gerenciador_de_boot_do_Windows_Vista/7/8/8.1)
        *   [2.1.2 Sistemas UEFI](#Sistemas_UEFI)
    *   [2.2 Linux antes do Windows](#Linux_antes_do_Windows)
        *   [2.2.1 Firmware UEFI](#Firmware_UEFI)
    *   [2.3 Solução de problemas](#Solução_de_problemas)
        *   [2.3.1 Não é possível criar uma nova partição ou localizar uma existente](#Não_é_possível_criar_uma_nova_partição_ou_localizar_uma_existente)
        *   [2.3.2 Não é possível inicializar Linux após a instalação do Windows](#Não_é_possível_inicializar_Linux_após_a_instalação_do_Windows)
        *   [2.3.3 Restaurando um registro de inicialização do Windows](#Restaurando_um_registro_de_inicialização_do_Windows)
*   [3 Padrões de fuso horário](#Padrões_de_fuso_horário)
*   [4 Veja também](#Veja_também)

## Informação importante

### Limitações do Windows em UEFI versus BIOS

A Microsoft impõe limitações em que o método de carregamento do sistema irá depender da circunstância em que cada tipo de firmware e esquema de particionamento podem ser suportados de acordo com a versão utilizada do Windows:

*   Versões do **Windows XP**, ambos **x86 32-bit** e **x86_64** (também chamado de x64) (RTM e todos os Service Packs) não suportam inicialização em modo [UEFI](/index.php/UEFI "UEFI") (IA32 ou x86_64) de qualquer disco ([MBR](/index.php/MBR "MBR") ou [GPT](/index.php/GPT "GPT")), OU em mdoo BIOS a partir de um disco GPT. Estas versões somente suportam inicialização no modo BIOS à partir de um disco MBR.
*   Versões do **Windows Vista** ou **7** **x86 32-bit** (RTM e todos os Service Packs) somente suportam inicialização em modo BIOS à partir de discos MBR, não à partir de discos GPT. Elas não suportam inicializar pelo modo UEFI x86_64 ou UEFI IA32 (x86 32-bit). Somente suportam inicialização no modo BIOS e somente por discos MBR.
*   Versões do **Windows Vista RTM x86_64** (e somente RTM) suportam inicializar em modo BIOS somente por discos MBR, não por discos GPT. Não suportam inicializar pelo modo UEFI x86_64 UEFI ou UEFI IA32 (x86 32-bit). Suporta somente inicializar no modo BIOS por discos MBR.
*   Versões do **Windows Vista** (SP1 ou acima, não RTM) e **Windows 7** **x86_64** suportam inicialização no modo UEFI x86_64 UEFI por discos GPT; OU em modo BIOS por discos MBR. Não suportam o modo UEFI IA32 (x86 32-bit) por discos GPT/MBR, UEFI x86_64 por discos MBR nem modo BIOS por discos GPT.
*   Versões do **Windows 8/8.1 x86 32-bit** suportam somente inicializar pelo modo UEFI IA32 (32-bit) por discos GPT; OU em modo BIOS por discos MBR. Não suportam UEFI x86_64 por discos GPT/MBR, UEFI x86_64 por discos MBR, nem modo BIOS por discos GPT. No mercado, os únicos sistemas conhecidos por suportar UEFI IA32 (32-bit) são alguns Macs Intel antigos (anteriores à 2010) e tablets Windows com Intel Atom (Clover trail e Bay Trail). São casos em que inicializam SOMENTE no modo UEFI IA32 (32-bit) e SOMENTE por discos GPT.
*   Versões do **Windows 8/8.1** **x86_64** suportam inicializar no modo UEFI x86_64 somente por discos GPT; OU somente em modo BIOS por discos MBR. Não suportam UEFI IA32, UEFI x86_64 por discos MBR, nem inicializar em modo BIOS à partir de discos GPT.

Para o caso de sistemas pré-instalados:

*   Todos os sistemas pré-instalados com Windows XP, Vista ou 7 32-bit, independentemente do Service Pack, edição (SKU) ou presença de suporte ao UEFI via firmware, inicializam no modo BIOS em discos MBR por padrão.
*   A maioria dos sistemas pré-instalados com Windows 7 x86_64, independentemente do Service Pack ou edição (SKU), usam BIOS em discos MBR por padrão. Sistemas mais recentes com Windows 7 pré-instaladossão conhecidos por inicializarem em modo UEFI x86_64 UEFI em discos GPT por padrão.
*   TODOS os sistemas com Windows 8/8.1 pré-instalado inicializam em modo UEFI com disco GPT. A arquitetura do firmware (32 ou 64 bits) corresponde com a do Windows, isto é, Windows 8/8.1 x86_64 inicializa em modo UEFI x86_64 e Windows 8/8.1 32-bit inicializa em modo UEFI IA32 (32-bit).

A melhor maneira de detectar o modo em que o Windows está inicializando é a seguinte[[1]](http://www.eightforums.com/tutorials/29504-bios-mode-see-if-windows-boot-uefi-legacy-mode.html):

*   Inicialize o Windows;
*   Pressione `Win+R` para abrir a caixa de diálogo "Executar";
*   Nela, digite `msinfo32.exe` e pressione Enter;
*   Na janela **Informações do Sistema**, selecione *Resumo do Sistema* no lado esquerdo e veja o valor que está no item **Modo da BIOS**, no lado direito;
*   Se o valor é `UEFI`, então o Windows está inicializando em modo UEFI/GPT. Se o valor é `Legado`, então o Windows está inicializando em modo BIOS/MBR.

Em geral, o Windows força o esquema de particionamento (GPT ou MBR) dependendo do modo de firmware usado (UEFI ou BIOS), isto é, se o Windows está no modo UEFI, ele só pode estar em um disco GPT; se o Windows está no modo BIOS, só pode estar num disco MBR. Esta é uma limitação imposta pelo instalador do Windows, e desde abril de 2014 não há oficialmente (por parte da Microsoft) suporte à instalação do Windows nas combinações UEFI/MBR ou BIOS/GPT. Portanto, o Windows suporta apenas as combinações UEFI/GPT ou BIOS/MBR.

**Dica:** O Windows 10 versão 1703 e versões mais recentes suportam converter de BIOS/MBR para UEFI/GPT usando [MBR2GPT.EXE](https://docs.microsoft.com/en-us/windows/deployment/mbr-to-gpt).

Esta limitação não é imposta pelo Linux kernel, mas depende somente de cada [gerenciador de boot](/index.php/Arch_boot_process_(Portugu%C3%AAs)#Gerenciador_de_boot "Arch boot process (Português)") usado e/ou como ele está configurado. A limitação do Windows deve ser considerada caso o usuário deseje inicializar ambos Windows e Linux pelo mesmo disco, haja vista que os procedimentos de instalação do gerenciador de boot dependem do tipo de firmware do sistema (BIOS ou UEFI) e da configuração de [particionamento](/index.php/Particionamento "Particionamento"). Nos casos onde Windows e Linux inicializam pelo mesmo disco, é recomandável seguir o método usado pelo Windows, ou seja, escolher entre UEFI/GPT ou BIOS/MBR. Veja [http://support.microsoft.com/kb/2581408](http://support.microsoft.com/kb/2581408) para mais informações.

### Limitações da mídia de instalação

Os tablets Intel Atom System-on-Chip (Clover trail e Bay Trail) fornecem apenas UEFI IA32 (32-bit) sem suporte ao Legacy BIOS (CSM) (diferente da maioria dos sistemas com UEFI x86_64), devido ao *Microsoft Connected Standby Guidelines para OEMs*. Com a falta do suporte ao Legacy BIOS nesses sistemas e a falta do suporte ao UEFI 32-bit na ISO oficial do Arch ([FS#53182](https://bugs.archlinux.org/task/53182)), a mídia oficial de instalação não pode inicializar esses sistemas. Veja [Unified Extensible Firmware Interface#UEFI firmware bitness](/index.php/Unified_Extensible_Firmware_Interface#UEFI_firmware_bitness "Unified Extensible Firmware Interface") para mais informações e possíveis soluções.

### Gerenciador de boot UEFI versus limitações do BIOS

A maioria dos gerenciadores de boot para linux instalados para um tipo de firmware não podem lançar ou carregar em cadeia gerenciadores de boot para outros tipos de firmware. Isto quer dizer que, se o Arch está instalado em modo UEFI/GPT ou UEFI/MBR em um disco e Windows está instalado em modo BIOS/MBR em outro disco, o gerenciador de boot UEFI usado pelo Arch não poderá carregar, em cadeia, o gerenciador em BIOS do Windows que está no outro disco. Da mesma forma, se o Arch está instalado em modo BIOS/MBR ou BIOS/GPT em um disco e o Windows está instalado em modo UEFI/GPT em outro disco, o gerenciador de boot que está em BIOS usado pelo Arch Arch não será capaz de carregar, em cadeia, o Windows em modo UEFI do outro disco.

As únicas exceções para isto são [GRUB](/index.php/GRUB "GRUB") em Macs da Apple, em que GRUB no modo UEFI pode inicializar um sistema operacional instalado em modo BIOS via comando `appleloader` (que não funciona em sistemas que não sejam Apple), e [rEFInd](/index.php/REFInd "REFInd") que tecnicamente suporta inicializar um sistema operacional em legacy BIOS em sistemas UEFI, mas [nem sempre legacy BIOS funciona em sistemas que não sejam Apple UEFI](http://rodsbooks.com/refind/using.html#), de acordo com seu autor Rod Smith.

Contudo, se o Arch está instalado em modo BIOS/GPT em um disco e o Windows está instalado em modo BIOS/MBR em outro disco, então o gerenciador de boot em BIOS usado pelo Arch **pode** inicializar o Windows em outro disco, se o gerenciador de boot usado suportar o carregamento à partir de outro disco.

**Nota:** Se o Arch e o Windows estão em dual-boot no mesmo disco, então o Arch deve seguir a mesma combinação de modo de firmware e esquema de particionamento usado pelo instalador do Windows no disco.

### UEFI Secure Boot

Todos os sistemas com versões pré-instaladas do Windows 8/8.1 por padrão inicializam em modo UEFI/GPT e tem UEFI Secure Boot ativado por padrão. Isto é obrigatório pela Microsoft em todos os sistemas OEM pré-instalados.

A mídia de instalação do Arch Linux não suporta *Secure Boot*. Veja [Secure Boot#Booting an install media](/index.php/Secure_Boot#Booting_an_install_media "Secure Boot").

É recomendável desativar o *UEFI Secure Boot* na configuração do firmware da placa-mãe manualmente antes de tentar inicializar o Arch Linux. O Windows 8/8.1 DEVE continuar a inicializar normalmente mesmo com o *Secure boot* desativado. O único problema a respeito de desativar o *UEFI Secure Boot* é que ele requer acesso físico ao sistema para desativá-lo através da configuração do firmware, já que a Microsoft explicitamente proibiu a existência de qualquer outro método remoto ou programável (de dentro do sistema operacional) de desativá-lo em todos os sistemas com Windows 8/8.1 pré-instalado.

### Inicialização rápida

A inicialização rápida é um recurso presente no Windows 8 e mais recentes versões que hiberna o computadorao invés de realmente desligá-lo para acelerar o tempo de inicialização. Seu sistema pode perder dados se o Windows hibernar e você inicializar outro sistema operacional e fazer alterações em arquivos. Mesmo se você não tiver intenção de compartilhar sistemas de arquivos, a partição de sistema EFI provavelmente será danificada em um sistema EFI. Portanto, você deve desativar a inicialização rápida, como descrito [aqui para Windows 8](http://www.eightforums.com/tutorials/6320-fast-startup-turn-off-windows-8-a.html) e [aqui para Windows 10](http://www.tenforums.com/tutorials/4189-fast-startup-turn-off-windows-10-a.html) antes de instalar o Linux em qualquer computador que tenha Windows 8 ou mais recente.

[ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) adicionou uma [maneira segura](http://sourceforge.net/p/ntfs-3g/ntfs-3g/ci/559270a8f67c77a7ce51246c23d2b2837bcff0c9/) de prevenir de montar uma unidade hibernada ao impedir que seja feita em modo de escrita, mas o driver NTFS presente no Linux kernel não tem essa segurança.

### Limitações de nomes de arquivo no Windows

O Windows está limitado em ter caminhos de arquivo menores do que [260 caracteres](http://blogs.msdn.com/b/bclteam/archive/2007/02/13/long-paths-in-net-part-1-of-3-kim-hamilton.aspx).

O Windows também impõe limitações no uso de [certos caracteres](http://msdn.microsoft.com/en-us/library/aa365247(VS.85).aspx#naming_conventions) em nomes de arquivo por razões vem desde o DOS:

*   `<` (menor que)
*   `>` (maior que)
*   `:` (dois pontos)
*   `"` (aspas)
*   `/` (barra)
*   `\` (barra invertida)
*   `|` (barra vertical ou pipe)
*   `?` (interrogação)
*   `*` (asterisco)

Estas são limitações do Windows e não do NTFS: qualquer outro sistema operacional usando partições NTFS poderá funcionar normalmente. O Windows irá falhar em detectar estes arquivos e executar `chkdsk` irá provavelmente acarretar sua remoção, o que significa uma potencial perda de dados.

[NTFS-3G](/index.php/NTFS-3G "NTFS-3G") aplica as restrições do Windows a novos arquivos através da opção [windows_names](http://www.tuxera.com/community/ntfs-3g-manual/#4) (veja [fstab](/index.php/Fstab "Fstab")).

## Instalação

A maneira recomendada de instalar um sistema em dual-boot com Linux e Windows é instalar primeiro Windows, usando apenas parte do disco para suas partições. Ao terminar a instalação do Windows, inicialize o ambiente de instalação do Linux onde você poderá criar e redimensionar partições para Linux enquanto mantém as partições existentes do Windows intocadas. A instalação do Windows irá criar a [partição de sistema EFI](/index.php/EFI_system_partition_(Portugu%C3%AAs) "EFI system partition (Português)") a qual poderá ser usada pelo seu gerenciador de boot no Linux [gerenciador de boot](/index.php/Arch_boot_process_(Portugu%C3%AAs)#Gerenciador_de_boot "Arch boot process (Português)").

### Windows antes do Linux

#### Sistemas BIOS

##### Usando um gerenciador de boot para Linux

Poderão ser utilizados quaisquer [gerenciadores de boot](/index.php/Arch_boot_process_(Portugu%C3%AAs)#Gerenciador_de_boot "Arch boot process (Português)") que suportem inicialização múltipla e BIOS.

##### Usando o gerenciador de boot do Windows

Com esta configuração, o gerenciador de boot do Windows carrega o GRUB, o qual inicializa o Arch.

###### Gerenciador de boot do Windows Vista/7/8/8.1

A seguinte seção contém trechos de [http://www.iceflatline.com/2009/09/how-to-dual-boot-windows-7-and-linux-using-bcdedit/](http://www.iceflatline.com/2009/09/how-to-dual-boot-windows-7-and-linux-using-bcdedit/).

De modo a garantir que o gerenciador de boot do Windows detecte a partição Linux, uma das partições linux criadas precisarão ser FAT32 (neste caso, `/dev/sda3`). O restante da instalação é similar a uma instalação típica. Algumas documentação alegam que a partição que será inicializada pelo Windows deverá ser uma partição primária, mas eu não tive problemas em fazê-lo com uma partição extendida.

*   Ao instalar o gerenciador de boot GRUB, instale-o em sua partição `/boot` ao invés de no MBR.
    **Nota:** Por exemplo, minha partição `/boot` é `/dev/sda5`. Então, eu instalei GRUB em `/dev/sda5` ao invés de `/dev/sda`. Para ajuda ao fazer isso, veja [GRUB/Tips and tricks#Install to partition or partitionless disk](/index.php/GRUB/Tips_and_tricks#Install_to_partition_or_partitionless_disk "GRUB/Tips and tricks").

*   De dentro do Linux, faça uma cópia das informações de boot com os seguintes comandos no terminal:

```
my_windows_part=/dev/sda3
my_boot_part=/dev/sda5
mkdir /media/win
mount $my_windows_part /media/win
dd if=$my_boot_part of=/media/win/linux.bin bs=512 count=1

```

*   Inicialize o Windows e você poderá ver o arquivo linux.bin em `C:\`. Agora, execute **cmd** com privilégios de administrador (vá em *Iniciar > Todos os programas > Acessórios*, clique com o botão direito em *Prompt de comando* e selecione *Executar como administrador*):

```
bcdedit /create /d "Linux" /application BOOTSECTOR

```

*   O BCDEdit irá retornar uma [UUID](https://en.wikipedia.org/wiki/Universally_unique_identifier "wikipedia:Universally unique identifier") que nos passos a seguir irei me referir a ela como apenas {ID}. Você vai precisar substituir a {ID} pelo número retornado. Um exemplo de {ID} é {d7294d4e-9837-11de-99ac-f3f3a79e3e93}.

```
bcdedit /set {ID} device partition=c:
bcdedit /set {ID}  path \linux.bin
bcdedit /displayorder {ID} /addlast
bcdedit /timeout 30

```

Reincie e aproveite. No meu caso, estou usando o gerenciador de boot do Windows, para que eu possa mapear o segundo botão do meu Dell Precision M4500 para inicializar Linux ao invés de Windows.

#### Sistemas UEFI

Se você já tiver o Windows instalado, então ele já criou algumas partições e preparou o disco no esquema [GPT](/index.php/Partitioning_(Portugu%C3%AAs)#GUID_Partition_Table "Partitioning (Português)"):

*   Uma partição contendo o [Windows Recovery Environment](https://en.wikipedia.org/wiki/Windows_Recovery_Environment "wikipedia:Windows Recovery Environment"), geralmente com 499 MiB de tamanho, contendo os arquivos necessários para inicializar o Windows (isto é, equivalente a `/boot` no Linux),
*   uma [partição de sistema EFI](/index.php/EFI_system_partition_(Portugu%C3%AAs) "EFI system partition (Português)") com o sistema de arquivos [FAT32](/index.php/FAT32 "FAT32"),
*   uma partição [Microsoft Reserved](https://en.wikipedia.org/wiki/Microsoft_Reserved_Partition "wikipedia:Microsoft Reserved Partition"), geralmente com 128 MiB de tamanho,
*   uma partição Microsoft com dados básicos de sistema e um sistema de arquivos NTFS, a qual corresponde a `C:`,
*   potencialmente um sistema de recuperação e backup e/ou dados secundários (que frequentemente corresponde a `D:` ou letras alfabéticas seguintes).

Usando o utilitário *Gerenciamento de disco do Windows*, veja como as partições estão nomeadas e que tipo está sendo reportado. Iso irá ajudar a compreender quais partições são essenciais ao Windows, e quais você poderá utilizar para outros propósitos.

**Atenção:** As 4 primeiras partições na lista acima são essenciais, não as remova.

Você poderá prosseguir com o [particionamento](/index.php/Partitioning_(Portugu%C3%AAs) "Partitioning (Português)"), de acordo com suas necessidades. Tenha em mente que uma partição de sistema EFI (muitas vezes referida simplesmente como ESP) não deverá ser criada, o que poderá [impedir a inicialização do Windows](https://support.microsoft.com/en-us/help/2879602/unable-to-boot-if-more-than-one-efi-system-partition-is-present). Simplesmente [monte a partição existente](/index.php/EFI_system_partition_(Portugu%C3%AAs)#Montar_a_partição "EFI system partition (Português)").

Deverá ser escolhido um gerenciador de boot capaz de inicializar em cadeia outras aplicações EFI para que o dual-boot entre Windows/Linux seja possível.

**Dica:** [rEFInd](/index.php/REFInd "REFInd") e [systemd-boot](/index.php/Systemd-boot "Systemd-boot") irão detectar automaticamente *Windows Boot Manager* (`\EFI\Microsoft\Boot\bootmgfw.efi`) e exibí-lo em seu menu de boot automaticamente. Para o [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)"), siga [GRUB (Português)#Windows instalado em modo UEFI/GPT](/index.php/GRUB_(Portugu%C3%AAs)#Windows_instalado_em_modo_UEFI/GPT "GRUB (Português)") para adicionar manualmente as entradas ao menu de boot ou [GRUB (Português)#Detectando outros sistemas operacionais](/index.php/GRUB_(Portugu%C3%AAs)#Detectando_outros_sistemas_operacionais "GRUB (Português)") para um arquivo de configuração gerado automaticamente.

Computadores que vem com versões mais novas do Windows costumam ter [Secure Boot](/index.php/Secure_Boot "Secure Boot") ativado. Você poderá ter de seguir alguns passos extras para desativar Secure Boot ou para criar sua mídia de instalação compatível com secure boot (veja o link para a página acima).

### Linux antes do Windows

Mesmo sendo uma forma recomendada de criar um dual-boot entre Linux/Windows instalar primeiro o Windows, isto poderá ser feito de forma diferente. Em contraste a instalar Windows antes do Linux, você precisará reservar uma partição para Windows, digamos de 40GB de tamanho ou mais, antecipadamente. Ou ter algum espaço em disco não-particionado, ou criar e redimensionar partições para Windows de dentro da instalação do Linux, antes de executar a instalação do Windows.

#### Firmware UEFI

O Windows irá usar a [partição de sistema EFI](/index.php/EFI_system_partition_(Portugu%C3%AAs) "EFI system partition (Português)") existente. Em contraste com o [afirmado anteriormente](#UEFI_systems), não está muito claro se uma simples partição para Windows, sem as partições com *Windows Recovery Environment* e sem a partição *Microsoft Reserved*, não irá funcionar.

Seguindo um esboço, assumindo que [Secure Boot](/index.php/Secure_Boot "Secure Boot") está desativado no firmware:

1.  Inicialize a instalação do Windows. Tome o cuidado de deixar apenas a partição pretendida, ou caso contrário deixe que ela faça seu trabalho como se não fosse instalar o Linux.
2.  Siga a seção [#Inicialização rápida](#Inicialização_rápida).
3.  Corrija a capacidade de carregar Linux na inicialização, talvez seguindo [#Não é possível inicializar Linux após a instalação do Windows](#Não_é_possível_inicializar_Linux_após_a_instalação_do_Windows). Já foi mencionado em [#Sistemas UEFI](#Sistemas_UEFI) que alguns gerenciadores de boot para Linux irão detectar automaticamente *Windows Boot Manager*. Ainda que novas instalações do Windows tenham uma opção de reinicialização avançada das quais você poderá inicializar o Linux, é aconselhável ter outras maneiras de inicializar o Linux, como por exemplo a mídia de instalação do Arch ou outro live CD.

### Solução de problemas

#### Não é possível criar uma nova partição ou localizar uma existente

Veja [#Limitações do Windows em UEFI versus BIOS](#Limitações_do_Windows_em_UEFI_versus_BIOS).

#### Não é possível inicializar Linux após a instalação do Windows

Veja [Unified Extensible Firmware Interface#Windows changes boot order](/index.php/Unified_Extensible_Firmware_Interface#Windows_changes_boot_order "Unified Extensible Firmware Interface").

#### Restaurando um registro de inicialização do Windows

Convencionalmente (e para facilidade de instalação), o Windows é comumente instalado na primeira partição e instala sua tabela de partições bem como sua referência ao gerenciador de boot no primeiro setor dessa partição. Caso você tenha acidentalmente instalado um gerenciador de boot como GRUB na partição do Windows ou danificado seu registro de inicialização de outra forma, você precisará de um utilitário para repará-la. A Microsoft inclui um utilitário de correção do setor de inicialização `FIXBOOT` e um utilitário de correção do MBR chamado `FIXMBR` em seus discos de recuperação, ou às vezes em seus discos de instalação. Através deste método, você pdoerá corrigir a referência ao setor de inicialização da primeira partição ao arquivo de configuração do gerenciador de boot e corrigir a referência do MBR para a primeira partição, respectivamente. Depois de fazer isto, você terá que [reinstalar o GRUB](/index.php/GRUB_(Portugu%C3%AAs)#Instalação "GRUB (Português)") no MBR como foi feito originalmente (isto é, o gerenciador de boot GRUB pode ser definido para carregar em cadeia o gerenciador de boot do Windows).

Se desejar reverter para utilização do Windows, você pode usar o comando `FIXBOOT` que liga do MBR ao setor de boot da primeira partição para voltar ao normal, neste caso, o carregamento automático do sistema operacional Windows.

É importante notar que existe um utilitário para Linux chamado `ms-sys` (pacote [ms-sys](https://aur.archlinux.org/packages/ms-sys/) no AUR) que pode instalar MBRs. No entento, este utilitário só é capaz de escrever novos MBRs (em todos os sistemas operacionais e sistemas de arquivos suportados) e setores de boot (também conhecidos como registro de boot; equivalente a usar `FIXBOOT`) para sistemas de arquivo FAT. A maioria dos Live CDs não possuem este utilitário por padrão, então ele precisará ser instalado primeiro, ou você poderá checar algum CD de recuperação que o possui, como o [Parted Magic](http://partedmagic.com/).

Primeiro, grave a informação da partição (tabela) novamente, usando:

```
# ms-sys --partition /dev/sda1

```

Depois, grave um MBR para Windows 2000/XP/2003:

```
# ms-sys --mbr /dev/sda  # Leia opções para versões diferentes

```

Então, grave o novo setor de boot (registro de boot):

```
# ms-sys -(1-6)          # Leia opções para descobrir o tipo adequado de gravação em FAT

```

`ms-sys` também pode gravar MBRs para Windows 98, ME, Vista, e 7, veja `ms-sys -h`.

## Padrões de fuso horário

*   Recomendado: configure ambos Arch Linux e Windows para usarem UTC, seguindo [System time#UTC in Windows](/index.php/System_time#UTC_in_Windows "System time"). Algumas versões do Windows revertem o relógio de hardware de volta para *localtime* caso estejam ajustados para sincronização online. Aparentemente este problema foi resolvido no Windows 10.
*   Não recomendado: Ajuste Arch Linux para *localtime* e desativo todas as [daemons de sincronização de fuso horário](/index.php/System_time#Time_synchronization "System time"). Isto irá deixar o Windows cuidar das correções de fuso horário e relógio de hardware e você precisará lembrar de inicializar o Windows ao menos duas vezes por ano quando [DST](https://en.wikipedia.org/wiki/Daylight_saving_time "wikipedia:Daylight saving time") (horário de verão) entrar. Por favor, não pergunte nos fóruns porque o seu relógio está atrasado ou adiantado em uma hora se você passou esse período sem acessar o Windows.

## Veja também

*   [Booting Windows from a desktop shortcut](https://bbs.archlinux.org/viewtopic.php?id=140049)
*   [One-time boot into Windows partition from desktop shortcut](https://github.com/kaipee/grub-reboot2win)
*   [Windows 7/8/8.1/10 ISO to Flash Drive burning utility for Linux (MBR/GPT, BIOS/UEFI, FAT32/NTFS)](https://github.com/ValdikSS/windows2usb)