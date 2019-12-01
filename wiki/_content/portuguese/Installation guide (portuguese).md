**Status de tradução:** Esse artigo é uma tradução de [Installation guide](/index.php/Installation_guide "Installation guide"). Data da última tradução: 2019-11-24\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Installation_guide&diff=0&oldid=589334) na versão em inglês.

Este documento irá guiá-lo no processo de instalação do [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)") usando o [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Antes de instalar, é recomendável ler rapidamente o [FAQ](/index.php/FAQ_(Portugu%C3%AAs) "FAQ (Português)"). Para convenções usadas neste documento, veja [Help:Leitura](/index.php/Help:Leitura "Help:Leitura"). Em especial, exemplos de código podem conter objetos reservados (formatados em `*italics*`) que devem ser substituídos manualmente.

Para instruções mais detalhadas, veja os respectivos artigos [ArchWiki](/index.php/ArchWiki_(Portugu%C3%AAs) "ArchWiki (Português)") ou as [páginas man](/index.php/P%C3%A1ginas_man "Páginas man") dos vários programas, ambos relacionados neste guia. Para uma ajuda interativa, o [canal IRC](/index.php/Canal_IRC "Canal IRC") e os [fóruns](https://bbs.archlinux.org/) também estão disponíveis.

Arch Linux deve funcionar em qualquer máquina compatível com [x86_64](https://en.wikipedia.org/wiki/pt:AMD64 "wikipedia:pt:AMD64") com um mínimo de 512 MB de RAM. Uma instalação básica deve ocupar menos de 800 MB de espaço em disco. Como o processo de instalação precisa obter pacotes de repositório remoto, esse guia presume que uma conexão com a Internet esteja disponível.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Pré-instalação](#Pré-instalação)
    *   [1.1 Verificar a assinatura](#Verificar_a_assinatura)
    *   [1.2 Inicializar o ambiente live](#Inicializar_o_ambiente_live)
    *   [1.3 Definir o layout do teclado](#Definir_o_layout_do_teclado)
    *   [1.4 Definir o idioma do ambiente live](#Definir_o_idioma_do_ambiente_live)
    *   [1.5 Verificar o modo de inicialização](#Verificar_o_modo_de_inicialização)
    *   [1.6 Conectar à internet](#Conectar_à_internet)
    *   [1.7 Atualizar o relógio do sistema](#Atualizar_o_relógio_do_sistema)
    *   [1.8 Partição dos discos](#Partição_dos_discos)
        *   [1.8.1 Exemplos de layouts](#Exemplos_de_layouts)
    *   [1.9 Formatar as partições](#Formatar_as_partições)
    *   [1.10 Montar os sistemas de arquivos](#Montar_os_sistemas_de_arquivos)
*   [2 Instalação](#Instalação)
    *   [2.1 Selecionar os espelhos](#Selecionar_os_espelhos)
    *   [2.2 Instalar os pacotes essenciais](#Instalar_os_pacotes_essenciais)
*   [3 Configurar o sistema](#Configurar_o_sistema)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Fuso horário](#Fuso_horário)
    *   [3.4 Localização](#Localização)
    *   [3.5 Configuração de rede](#Configuração_de_rede)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Senha do root](#Senha_do_root)
    *   [3.8 Gerenciador de boot](#Gerenciador_de_boot)
*   [4 Reiniciar](#Reiniciar)
*   [5 Pós-instalação](#Pós-instalação)

## Pré-instalação

A mídia de instalação e suas assinaturas [GnuPG](/index.php/GnuPG "GnuPG") podem ser obtidas a partir da página de [Download](https://archlinux.org/download/).

### Verificar a assinatura

É recomendável verificar a assinatura da imagem antes de usá-la, especialmente ao fazer o download de um *espelho HTTP*, no qual os downloads geralmente são propensos a serem interceptados para [servir imagens maliciosas](http://www.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html#explanation).

Em um sistema com [GnuPG](/index.php/GnuPG "GnuPG") instalado, faça isso baixando a *assinatura PGP* (sob *Checksums*) para o diretório da ISO e [verificando-a](/index.php/GnuPG#Verify_a_signature "GnuPG") com:

```
$ gpg --keyserver-options auto-key-retrieve --verify archlinux-*versão*-x86_64.iso.sig

```

Alternativamente, de uma instalação existente de Arch Linux, execute:

```
$ pacman-key -v archlinux-*versão*-x86_64.iso.sig

```

**Nota:**

*   A assinatura em si pode ser manipulada se for baixada de um site espelho, ao invés de [archlinux.org](https://archlinux.org/download/) como acima. Nesse caso, certifique-se de que a chave pública, que é usada para decodificar a assinatura, seja assinada por outra chave confiável. O comando `gpg` produzirá a impressão digital da chave pública.
*   Outro método para verificar a autenticidade da assinatura é garantir que a impressão digital da chave pública seja idêntica à impressão digital da chave do [desenvolvedor do Arch Linux](https://www.archlinux.org/people/developers/) que assinou o arquivo ISO. Veja [Wikipedia:pt:Criptografia de chave pública](https://en.wikipedia.org/wiki/pt:Criptografia_de_chave_p%C3%BAblica "wikipedia:pt:Criptografia de chave pública") para mais informações sobre o processo de chave pública para autenticar chaves.

### Inicializar o ambiente live

O ambiente *live* pode ser inicializado a partir de uma [unidade flash USB](/index.php/M%C3%ADdia_de_instala%C3%A7%C3%A3o_em_flash_USB "Mídia de instalação em flash USB"), um [disco óptico](/index.php/Optical_disc_drive#Burning "Optical disc drive") ou uma rede com [PXE](/index.php/PXE "PXE"). Para meios alternativos de instalação, consulte [Category:Installation process (Português)](/index.php/Category:Installation_process_(Portugu%C3%AAs) "Category:Installation process (Português)").

*   O apontamento do dispositivo de inicialização atual para uma unidade que contém a mídia de instalação do Arch normalmente pode ser alcançado pressionando-se uma tecla durante a fase [POST](https://en.wikipedia.org/wiki/pt:Power-on_self-test "wikipedia:pt:Power-on self-test"), conforme indicado na tela inicial. Consulte o manual da sua placa-mãe para obter detalhes.
*   Quando o menu do Arch aparecer, selecione *Boot Arch Linux* e pressione `Enter` para entrar no ambiente de instalação.
*   Consulte [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) para uma lista de [parâmetros de inicialização](/index.php/Par%C3%A2metros_do_kernel#Configuração "Parâmetros do kernel") e [packages.x86_64](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) para uma lista de pacotes incluídos.
*   Você será autenticado no primeiro [console virtual](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") como o usuário *root* sob um prompt de shell [Zsh](/index.php/Zsh "Zsh").

Para trocar para um console diferente — por exemplo, para ver esse guia com [ELinks](/index.php/ELinks "ELinks") junto com a instalação — use o [atalho](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*seta*`. Para [editar](/index.php/Edi%C3%A7%C3%A3o_de_texto "Edição de texto") arquivos de configuração, [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") e [vim](/index.php/Vim#Usage "Vim") estão disponíveis.

### Definir o layout do teclado

O [mapa de teclas de console](/index.php/Mapa_de_teclas_de_console "Mapa de teclas de console") padrão é [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Layouts disponíveis podem ser listados com:

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

Para modificar o layout, acrescente um nome de arquivo ao [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), omitindo caminho e extensão de arquivo. Por exemplo, para definir um layout de teclado [ABNT (brasileiro)](https://en.wikipedia.org/wiki/File:KB_Portuguese_Brazil.svg "wikipedia:File:KB Portuguese Brazil.svg"):

```
# loadkeys br-abnt2   

```

Ou para definir para um layout de teclado de português de Portugal:

```
# loadkeys pt-latin1 

```

[Fontes de console](/index.php/Fontes_de_console "Fontes de console") estão localizadas em `/usr/share/kbd/consolefonts/` e, de forma semelhante, podem ser definidas com [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Definir o idioma do ambiente live

**Nota:** Isso se aplica **apenas** ao ambiente live. A definição do idioma do sistema instalado é explicado em [#Localização](#Localização)

O ambiente *live* vem em inglês (locale `en_US.UTF-8`) por padrão, mas você pode alterá-lo para executar as etapas de instalação usando o idioma desejado.

Para português brasileiro, descomente `pt_BR.UTF-8 UTF-8` e qualquer outro locale desejado em `/etc/locale.gen` e gere-os com:

```
 # locale-gen

```

Então, exporte a variável `LANG` acrescentando o idioma e codificação desejados. Por exemplo, para português brasileiro seria:

```
 # export LANG=pt_BR.UTF-8

```

Para português de Portugal, use `pt_PT.UTF-8 UTF-8` em vez do "pt_BR".

### Verificar o modo de inicialização

Se o modo UEFI estiver disponível em uma placa-mãe [UEFI](/index.php/UEFI "UEFI"), [Archiso](/index.php/Archiso_(Portugu%C3%AAs) "Archiso (Português)") vai [inicializar](/index.php/Inicializar "Inicializar") o Arch Linux adequadamente via [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). Para verificar isso, liste o diretório [efivars](/index.php/UEFI#UEFI_variables "UEFI"):

```
# ls /sys/firmware/efi/efivars

```

Se o diretório não existir, o sistema pode ser inicializado no modo [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") ou CSM. Veja o manual da sua placa-mãe para detalhes.

### Conectar à internet

Para configurar uma conexão de rede, siga as etapas abaixo:

*   Certifique-se que sua [interface de rede](/index.php/Interface_de_rede "Interface de rede") esteja listada e ativada, por exemplo, com [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8): `# ip link` 
*   Conecte-se à rede. Conecte o cabo Ethernet ou [conecte a uma rede sem fio](/index.php/Configura%C3%A7%C3%A3o_de_rede_sem_fio "Configuração de rede sem fio").
*   Configure sua conexão de rede:
    *   [Endereço IP estático](/index.php/Configura%C3%A7%C3%A3o_de_rede#Endereço_IP_estático "Configuração de rede")
    *   Endereço IP dinâmico: use [DHCP](/index.php/DHCP "DHCP").

    **Nota:** A imagem de instalação habilita [dhcpcd](/index.php/Dhcpcd "Dhcpcd") (`dhcpcd@*interface*.service`) para [dispositivos de rede com fio](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) na inicialização.

*   A conexão pode ser verificada com [ping](https://en.wikipedia.org/wiki/pt:ping "wikipedia:pt:ping"): `# ping archlinux.org` 

### Atualizar o relógio do sistema

Use [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) para garantir que o relógio do sistema está certo:

```
# timedatectl set-ntp true

```

Para verificar o status do serviço, use `timedatectl status`.

### Partição dos discos

Quando reconhecido pelo sistema *live*, discos são atribuídos a um [dispositivo de bloco](/index.php/Dispositivo_de_bloco "Dispositivo de bloco") tal como `/dev/sda` ou `/dev/nvme0n1`.. Para identificar esses dispositivos, use [lsblk](/index.php/Lsblk_(Portugu%C3%AAs) "Lsblk (Português)") ou *fdisk*.

```
# fdisk -l

```

Resultados terminando em `rom`, `loop` ou `airoot` podem ser ignorados.

As seguintes [partições](/index.php/Partition "Partition") são **exigidas** para um dispositivo escolhido:

*   Uma partição para o diretório raiz `/`.
*   Se [UEFI](/index.php/UEFI "UEFI") estiver habilitado, uma [partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI").

Se você quiser criar algum dispositivo de bloco empilhado para [LVM](/index.php/LVM "LVM"), [criptografia de sistema](/index.php/Dm-crypt "Dm-crypt") ou [RAID](/index.php/RAID "RAID"), faça isso agora.

#### Exemplos de layouts

| BIOS com [MBR](/index.php/MBR "MBR") |
| Ponto de montagem | Partição | [Tipo de partição](https://en.wikipedia.org/wiki/pt:Tipo_de_parti%C3%A7%C3%A3o "wikipedia:pt:Tipo de partição") | Tamanho sugerido |
| `/mnt` | `/dev/sd*X*1` | Linux | Restante do dispositivo |
| [SWAP] | `/dev/sd*X*2` | Swap Linux | Mais que 512 MiB |
| UEFI com [GPT](/index.php/GPT "GPT") |
| Ponto de montagem | Partição | [Tipo de partição](https://en.wikipedia.org/wiki/pt:Tabela_de_Parti%C3%A7%C3%A3o_GUID#Tipos_de_parti.C3.A7.C3.A3o_GUID "wikipedia:pt:Tabela de Partição GUID") | Tamanho sugerido |
| `/mnt/boot` ou `/mnt/efi` | `/dev/sd*X*1` | [Partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") | 260–512 MiB |
| `/mnt` | `/dev/sd*X*2` | Linux x86-64 root (/) | Restante do dispositivo |
| [SWAP] | `/dev/sd*X*3` | Linux swap | Mais que 512 MiB |

Veja também [Partitioning#Example layouts](/index.php/Partitioning#Example_layouts "Partitioning").

**Nota:**

*   Use [fdisk](/index.php/Fdisk "Fdisk") ou [parted](/index.php/Parted "Parted") para modificar as tabelas de partição, por exemplo `fdisk /dev/sd*X*`.
*   Um espaço [swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)") pode ser definido em um [Arquivo swap](/index.php/Arquivo_swap "Arquivo swap") para sistemas de arquivos que possuem suporte a file systems supporting it.

### Formatar as partições

Assim que as partições tenham sido criadas, cada uma deve ser formatada com um [sistema de arquivos](/index.php/File_system "File system") adequado. Por exemplo, se a partição raiz está em `/dev/sd*X*1` e receberá o sistema de arquivos `*ext4*`, execute:

```
# mkfs.*ext4* /dev/sd*X1*

```

Se você criou uma partição para swap (por exemplo, `/dev/*sda3*`), inicialize-a com *mkswap*:

```
# mkswap /dev/sd*X2*
# swapon /dev/sd*X2*

```

Veja [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") para detalhes.

### Montar os sistemas de arquivos

[Monte](/index.php/Mount "Mount") o sistema de arquivos da partição raiz em `/mnt`, por exemplo:

```
# mount /dev/sd*X1* /mnt

```

Crie quaisquer pontos de montagem restantes (tal como `/mnt/efi`) e monte suas partições correspondentes.

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) vai detectar os sistemas de arquivos montados e espaços swap.

## Instalação

### Selecionar os espelhos

Pacotes a serem instalados devem ser baixados de [espelhos](/index.php/Espelhos "Espelhos") *(mirrors)*, que são definidos na `/etc/pacman.d/mirrorlist`. No sistema *live*, todos os espelhos estão habilitados e ordenados por seu status e velocidade de sincronização à época em que a imagem de instalação foi criada.

Quanto mais alto um espelho está posicionado na lista, mais prioritário ele será ao baixar um pacote. Você pode querer editar o arquivo e mover espelhos geograficamente mais pertos para o topo da lista, apesar de que outros critérios devem ser levados em consideração.

Esse arquivo será posteriormente copiado para o novo sistema por *pacstrap*, então é melhor fazer direito.

### Instalar os pacotes essenciais

Use o script [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) para instalar o pacote [base](https://www.archlinux.org/packages/?name=base), um [kernel](/index.php/Kernel_(Portugu%C3%AAs) "Kernel (Português)") Linux e um firmware para hardwares comuns:

```
# pacstrap /mnt base linux linux-firmware

```

**Dica:** Você pode substituir [linux](https://www.archlinux.org/packages/?name=linux) pelo pacote de [kernel](/index.php/Kernel_(Portugu%C3%AAs) "Kernel (Português)") de sua escolha. Você pode não instalar um kernel, se souber o que está fazendo.

O pacote [base](https://www.archlinux.org/packages/?name=base) não inclui todas as ferramentas da instalação *live*. Então a instalação de outros pacotes pode ser necessário para um sistema base completamente funcional. Em especial, considere instalar:

*   utilitários para acessar partições [RAID](/index.php/RAID "RAID") ou [LVM](/index.php/LVM "LVM"),
*   firmwares específicos para outros dispositivos não incluídos em [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware),
*   softwares necessários para [rede](/index.php/Rede "Rede"),
*   um editor de [editores de arquivos](/index.php/Text_editor "Text editor")
*   pacotes necessários para acessar documentação em páginas [man](/index.php/Man_(Portugu%C3%AAs) "Man (Português)") e [info](/index.php/Info_(Portugu%C3%AAs) "Info (Português)"): [man-db](https://www.archlinux.org/packages/?name=man-db), [man-pages](https://www.archlinux.org/packages/?name=man-pages) and [texinfo](https://www.archlinux.org/packages/?name=texinfo).

Para [instalar](/index.php/Instala "Instala") outros pacotes ou grupos de pacotes, acrescente os nomes ao comando *pacstrap* acima (separados por espaço) ou use o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") enquanto [estiver em chroot no novo sistema](#Chroot). Para uma comparação, pacotes disponíveis no sistema *live* podem ser encontrados em [packages.x86_64](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64).

## Configurar o sistema

### Fstab

Gerar um arquivo [fstab](/index.php/Fstab "Fstab") (use `-U` ou `-L` para definir por [UUID](/index.php/UUID_(Portugu%C3%AAs) "UUID (Português)") ou rótulos, respectivamente):

```
# genfstab -p /mnt >> /mnt/etc/fstab

```

Verifique o arquivo `/mnt/etc/fstab` resultante e edite-o caso haja erros.

### Chroot

[Mude a raiz](/index.php/Change_root_(Portugu%C3%AAs) "Change root (Português)") para novo sistema:

```
# arch-chroot /mnt

```

### Fuso horário

Defina o [fuso horário](/index.php/Time_zone "Time zone"):

```
# ln -sf /usr/share/zoneinfo/*Região*/*Cidade* /etc/localtime

```

Por exemplo, para definir para o fuso horário de Brasília (*BRT* ou *BRST*), execute:

```
# ln -sf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime

```

Execute [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) para gerar `/etc/adjtime`:

```
# hwclock --systohc

```

Esse comando presume que o relógio de hardware está definido para [UTC](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC"). Veja [System time#Time standard](/index.php/System_time#Time_standard "System time") para mais detalhes.

### Localização

Descomente `pt_BR.UTF-8 UTF-8` e qualquer outro [locale](/index.php/Locale_(Portugu%C3%AAs) "Locale (Português)") em `/etc/locale.gen`, e gere-os com:

```
# locale-gen

```

Crie o arquivo [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) e defina a [variável](/index.php/Vari%C3%A1vel "Variável") `LANG` adequadamente:

 `/etc/locale.conf`  `LANG=*pt_BR.UTF-8*` 

Se você [definir o layout do teclado](#Definir_o_layout_do_teclado), torne as alterações persistentes em [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*br-abnt2*` 

### Configuração de rede

Crie o arquivo [hostname](/index.php/Hostname_(Portugu%C3%AAs) "Hostname (Português)"):

 `/etc/hostname` 
```
*meuhostname*

```

Adicione entradas correspondentes ao [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost.localdomain	localhost
::1		localhost.localdomain	localhost
**127.0.1.1	*meuhostname*.localdomain	*meuhostname***

```

Se o sistema tem um endereço IP permanente, ele deve ser usado em vez de `127.0.1.1`.

Conclua a [configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede") para o ambiente recém-instalado, que inclua [instala](/index.php/Instala "Instala")ção de pacotes como [iputils](https://www.archlinux.org/packages/?name=iputils) e seu software [gerenciador de rede](/index.php/Gerenciador_de_rede "Gerenciador de rede") preferido.

### Initramfs

Criar um novo *initramfs* geralmente não é necessário, porque [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") foi executado na instalação do pacote de [kernel](/index.php/Kernel_(Portugu%C3%AAs) "Kernel (Português)") com *pacstrap*.

Para [LVM](/index.php/LVM#Configure_mkinitcpio "LVM"), [criptografia de sistema](/index.php/Dm-crypt "Dm-crypt") or [RAID](/index.php/RAID#Configure_mkinitcpio "RAID"), modifique o [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) e recrie a imagem initramfs:

```
# mkinitcpio -P

```

### Senha do root

Defina a [senha](/index.php/Senha "Senha") do *root* (também conhecido como "superusuário"):

```
# passwd

```

### Gerenciador de boot

Escolha e instale um [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") compatível com Linux. Se você tiver um CPU Intel ou AMD, habilite atualizações de [microcódigo](/index.php/Microcode "Microcode") também.

## Reiniciar

Saia de ambiente *chroot* digitando `exit` ou pressionando `Ctrl+D`.

Opcionalmente, desmonte todas as partições com `umount -R /mnt`: isso permite noticiar quaisquer partições "ocupadas" e localizar a causa com o [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Finalmente, reinicie a máquina digitando `reboot`: quaisquer partições que ainda estejam montadas serão desmontadas automaticamente por *systemd*. Lembre-se de remover a mídia de instalação e, então, se autenticando no novo sistema com a conta de root.

## Pós-instalação

Veja [Recomendações gerais](/index.php/Recomenda%C3%A7%C3%B5es_gerais "Recomendações gerais") por instruções de gerenciamento de sistema e tutoriais pós-instalação (como instalar uma interface gráfica de usuário, som ou um touchpad).

Para uma lista de aplicativos que podem ser de seu interesse, veja [Lista de aplicativos](/index.php/List_of_applications "List of applications").