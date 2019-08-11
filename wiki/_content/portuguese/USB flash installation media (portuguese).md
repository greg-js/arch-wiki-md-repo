**Status de tradução:** Esse artigo é uma tradução de [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media"). Data da última tradução: 2019-08-10\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=USB_flash_installation_media&diff=0&oldid=579165) na versão em inglês.

Artigos relacionados

*   [CD Burning](/index.php/CD_Burning "CD Burning")
*   [Archiso](/index.php/Archiso_(Portugu%C3%AAs) "Archiso (Português)")
*   [Multiboot USB drive](/index.php/Multiboot_USB_drive "Multiboot USB drive")

Esta página discute vários métodos multiplataforma sobre como criar uma unidade USB do instalador do Arch Linux (também conhecida como *"unidade flash", "pendrive", "USB stick", "flash drive", "USB key"* etc.) para inicializar na BIOS e sistemas UEFI. O resultado será um sistema LiveUSB (similar a LiveCD) que pode ser usado para instalar o Arch Linux, manutenção do sistema ou para fins de recuperação, e que, por causa da natureza do [SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS"), descartará todas as alterações quando o computador for desligado.

Se você deseja executar uma instalação completa do Arch Linux a partir de uma unidade USB (por exemplo, com configurações persistentes), consulte [Instalando Arch Linux em um pendrive](/index.php/Instalando_Arch_Linux_em_um_pendrive "Instalando Arch Linux em um pendrive"). Se você gostaria de usar seu pendrive inicializável com Arch Linux como um sistema de recuperação, veja [chroot](/index.php/Change_root_(Portugu%C3%AAs) "Change root (Português)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 USB inicializável com BIOS e UEFI](#USB_inicializável_com_BIOS_e_UEFI)
    *   [1.1 Usando ferramentas automáticas](#Usando_ferramentas_automáticas)
        *   [1.1.1 No GNU/Linux](#No_GNU/Linux)
            *   [1.1.1.1 Usando dd](#Usando_dd)
            *   [1.1.1.2 Usando etcher](#Usando_etcher)
            *   [1.1.1.3 Usando Kindd](#Usando_Kindd)
        *   [1.1.2 No Windows](#No_Windows)
            *   [1.1.2.1 Usando Rufus](#Usando_Rufus)
            *   [1.1.2.2 Usando USBwriter](#Usando_USBwriter)
            *   [1.1.2.3 Usando win32diskimager](#Usando_win32diskimager)
            *   [1.1.2.4 Usando Cygwin](#Usando_Cygwin)
            *   [1.1.2.5 dd para Windows](#dd_para_Windows)
        *   [1.1.3 No macOS](#No_macOS)
        *   [1.1.4 No Android](#No_Android)
            *   [1.1.4.1 EtchDroid](#EtchDroid)
    *   [1.2 Usando formatação manual](#Usando_formatação_manual)
        *   [1.2.1 No GNU/Linux](#No_GNU/Linux_2)
        *   [1.2.2 No Windows](#No_Windows_2)
*   [2 Outros métodos para sistemas BIOS](#Outros_métodos_para_sistemas_BIOS)
    *   [2.1 No GNU/Linux](#No_GNU/Linux_3)
        *   [2.1.1 Usando uma unidade USB multiboot](#Usando_uma_unidade_USB_multiboot)
        *   [2.1.2 Usando o utilitário de disco do GNOME](#Usando_o_utilitário_de_disco_do_GNOME)
        *   [2.1.3 Fazendo uma unidade USB-ZIP](#Fazendo_uma_unidade_USB-ZIP)
        *   [2.1.4 Usando UNetbootin](#Usando_UNetbootin)
    *   [2.2 No Windows](#No_Windows_3)
        *   [2.2.1 A forma Flashnul](#A_forma_Flashnul)
        *   [2.2.2 Carregar a mídia de instalação da RAM](#Carregar_a_mídia_de_instalação_da_RAM)
            *   [2.2.2.1 Preparar a unidade flash USB](#Preparar_a_unidade_flash_USB)
            *   [2.2.2.2 Copiar os arquivos necessários à unidade flash USB](#Copiar_os_arquivos_necessários_à_unidade_flash_USB)
            *   [2.2.2.3 Criar o arquivo de configuração](#Criar_o_arquivo_de_configuração)
            *   [2.2.2.4 Etapas finais](#Etapas_finais)
*   [3 Solução de problemas](#Solução_de_problemas)
*   [4 Veja também](#Veja_também)

## USB inicializável com BIOS e UEFI

### Usando ferramentas automáticas

#### No GNU/Linux

##### Usando dd

**Nota:** Este método é recomendado devido à sua simplicidade. Se não funcionar, mude para o método alternativo [#Usando formatação manual](#Usando_formatação_manual) abaixo.

**Atenção:** Isso destruirá irrevogavelmente todos os dados em `/dev/**sdx**`. Para restaurar a unidade USB como um dispositivo de armazenamento utilizável vazio após usar a imagem ISO do Arch, a assinatura do sistema de arquivos ISO 9660 precisa ser removida executando `wipefs --all /dev/**sdx**` como root, antes de [reparticionar](/index.php/Repartition "Repartition") e [reformatar](/index.php/Reformat "Reformat") a unidade USB.

**Dica:** Descubra o nome do sua unidade USB com `lsblk`. Certifique-se de que ela **não** esteja montada.

Execute o seguinte comando, substituindo `/dev/**sdx**` pela sua unidade, por exemplo `/dev/sdb`. (**não** anexe um número de partição, de forma a **não** usar algo como `/dev/sdb**1**`)

```
# dd bs=4M if=path/to/archlinux.iso of=/dev/**sdx** status=progress oflag=sync

```

Veja [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1) para mais informações sobre [dd](/index.php/Dd_(Portugu%C3%AAs) "Dd (Português)"). Veja [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1#DESCRIPTION) para mais informações sobre `oflag=sync`.

##### Usando etcher

[Etcher](https://etcher.io/) é um aplicador de imagem do sistema operacional criado com node.js e Electron, capaz que o *flashing* de um cartão SD ou unidade USB seja uma experiência agradável e segura. Ele protege você de gravar acidentalmente em seus discos rígidos e garante que todos os bytes de dados foram escritos corretamente e muito mais. Há 6 pacotes relacionados no AUR.

##### Usando Kindd

[Kindd](https://github.com/LinArcX/Kindd) é um frontend gráfico baseado no Qt para dd. Está disponível como [kindd-git](https://aur.archlinux.org/packages/kindd-git/).

#### No Windows

##### Usando Rufus

[Rufus](https://rufus.akeo.ie/) é um escritor multiuso de ISO em USB. Ele fornece uma interface gráfica do usuário e não se importa se a unidade está formatada corretamente ou não.

Basta selecionar a ISO do Arch Linux, a unidade USB na qual você deseja criar o Arch Linux inicializável e clicar em *Iniciar*.

**Nota:** Se a unidade USB não inicializar adequadamente usando o modo padrão da imagem ISO, o **modo Imagem DD** deve ser usado.

*   Para Rufus versão ≥ 3.0, selecione *GPT* a partir do menu suspenso *Esquema de partição*. Ao clicar em *Iniciar*, você verá o diálogo de seleção de modo, selecione o *modo Imagem DD*.
*   Para Rufus versão < 3.0,selecione o modo *Imagem DD* a partir do menu suspenso na parte inferior.

**Dica:** Para adicionar [uma partição adicional a um armazenamento persistente](https://github.com/pbatard/rufus/issues/691) use o controle deslizante para escolher o tamanho da partição persistente. Ao usar o recurso de partição persistente, certifique-se de selecionar *MBR* no menu suspenso *Esquema de partição* e *BIOS ou UEFI* em *Sistema de sestino*, caso contrário a unidade não será utilizável para inicialização de BIOS e UEFI.

##### Usando USBwriter

Esse método não requer nenhuma solução alternativa e é tão simples quanto `dd` no Linux. Basta baixar o ISO do Arch Linux e, com permissões de administrador local, use o utilitário [USBwriter](https://sourceforge.net/p/usbwriter/wiki/Documentation/) para gravar na memória flash USB.

##### Usando win32diskimager

[win32diskimager](https://sourceforge.net/projects/win32diskimager/) é outra ferramenta gráfica de gravação de ISO para Windows. Basta selecionar sua imagem ISO e a letra da unidade USB de destino (talvez seja necessário formatá-la primeiro para atribuir uma letra de unidade) e clicar em Write.

##### Usando Cygwin

Certifique-se que sua instalação de [Cygwin](https://www.cygwin.com/) contém o pacote `dd`.

**Dica:** Se você não quiser instalar o Cygwin, você pode fazer o download do `dd` para Windows em [http://www.chrysocome.net/dd](http://www.chrysocome.net/dd) aqui. Veja a próxima seção para mais informações.

Coloque seu arquivo de imagem em seu diretório *home*:

```
C:\cygwin\home\joao\

```

Execute o cygwin como administrador (necessário para o cygwin acessar o hardware). Para escrever na sua unidade USB, use o seguinte comando:

```
dd if=*imagem.iso* of=\\.\**x**: bs=4M

```

sendo *imagem.iso* o caminho para o arquivo de imagem iso dentro do diretório `cygwin` e `\\.\**x**:` é a sua unidade flash USB onde `**x**` é a letra designada pelo Windows, por exemplo `\\.\d:`.

No Cygwin 6.0, descubra a partição correta com:

```
cat /proc/partitions

```

e escreva a imagem ISO com as informações da saída. Exemplo:

**Atenção:** Isso excluirá irrevogavelmente todos os arquivos da sua unidade flash USB. Portanto, certifique-se de não ter arquivos importantes na unidade flash antes de fazer isso.

```
dd if=imagem.iso of=/dev/sdb bs=4M

```

##### dd para Windows

Uma versão do *dd* licenciada sob GPL para Windows está disponível em [http://www.chrysocome.net/dd](http://www.chrysocome.net/dd). A vantagem dela sobre o Cygwin é um download menor. Use-a como mostrado nas instruções do Cygwin acima.

Para começar, baixe a última versão do dd para Windows. Uma vez baixado, extraia o conteúdo do arquivo em Downloads ou em outro lugar.

Agora, inicie seu `prompt de comando` como administrador. Em seguida, mude o diretório (`cd`) para o diretório Downloads.

Se a sua ISO do Arch Linux estiver em outro lugar, você pode precisar declarar o caminho completo, por conveniência, você pode querer colocar o ISO do Arch Linux na mesma pasta que o executável dd. O formato básico do comando será semelhante a este:

```
# dd if=*archlinux-*versão*-x86_64.iso* od=\\.\*x*: bs=4M

```

**Nota:** As letras da unidade do Windows estão vinculadas a uma partição. Para permitir a seleção de todo o disco, o *dd para Windows* fornece o parâmetro `od`, que é usado nos comandos acima. Note, entretanto, que este parâmetro é específico para *dd para Windows* e não pode ser encontrado em outras implementações de *dd*.

**Atenção:** Porque o `od` é usado, todas as partições no disco selecionado serão destruídas. Esteja absolutamente certo de que você está direcionando dd para a unidade correta antes de executar.

Simplesmente substitua os vários pontos nulos (indicados por um "x") com a data correta e letra de unidade correta. Aqui está um exemplo completo. Por exemplo:

```
# dd if=ISOs\archlinux-*versão*-x86_64.iso od=\\.\d: bs=4M

```

**Nota:** Alternativamente, substitua a letra da unidade com `\\.\PhysicalDrive*X*`, sendo `*X*` o número da unidade física (inicia do 0). Por exemplo: `# dd if=ISOs\archlinux-*versão*-x86_64.iso of=\\.\PhysicalDrive1 bs=4M` 

Você pode descobrir o número da unidade física digitando `wmic diskdrive list brief` no prompt de comando ou com `dd --list`

Qualquer janela do Explorer deve ser fechada ou o dd informará um erro.

#### No macOS

Primeiro, você precisa identificar o dispositivo USB. Abra `/Applications/Utilities/Terminal` e liste todos os dispositivos de armazenamento com o comando:

```
$ diskutil list

```

Seu dispositivo USB aparecerá como algo como `/dev/disk2 (external, physical)`. Verifique se esse é o dispositivo que você deseja apagar verificando seu nome e tamanho e, em seguida, use seu identificador para os comandos abaixo, em vez de /dev/disk*X*.

Um dispositivo USB é normalmente automontado no macOS e você pode ter que desmontá-lo (não ejetar) antes de escrever blocos nele com `dd`. No Terminal, execute:

```
$ diskutil unmountDisk /dev/disk*X*

```

Agora, copie o arquivo de imagem ISO para o dispositivo. O comando `dd` é similar à sua contraparte Linux, mas note o 'r' antes do modo 'disk' para modo *raw*, que torna a transferência muito mais rápida:

```
# dd if=caminho/para/arch.iso of=/dev/**r**disk*X* bs=1M

```

Esse comando será executado sem qualquer mensagem de saída. Para ver o progresso, envie SIGINFO pressionando `Ctrl+t`. Note que `disk*X*` aqui não deve incluir o sufixo `s1` ou, do contrário, o dispositivo USB só será inicializável no modo UEFI e não no legado. Após a conclusão, o macOS reclamar "O disco que você inseriu não podia ser lido por este computador". Selecione 'Ignorar'. O dispositivo USB será inicializável.

#### No Android

##### EtchDroid

[EtchDroid](https://etchdroid.depau.eu/) é um instalador de imagem de sistema operacional para o Android. Ele funciona sem permissões de root no Android 5 até o Android 8\. De acordo com relatórios de erros, nem sempre funciona no Android 9 e Android 4.4.

Para criar um instalador do Arch Linux, baixe o arquivo de imagem ISO no seu dispositivo Android. Conecte a unidade USB ao seu dispositivo, usando um adaptador USB-OTG, se necessário. Abra o EtchDroid, selecione "Flash raw image", selecione o seu Arch ISO e selecione o seu drive USB. Conceda a permissão da API USB e confirme.

Mantenha seu telefone em uma mesa enquanto está gravando a imagem: muitos adaptadores USB-OTG são um pouco instáveis e você pode desconectá-lo por engano.

### Usando formatação manual

#### No GNU/Linux

Esse método é mais complicado do que gravar a imagem diretamente com `dd`, mas mantém a unidade flash utilizável para armazenamento de dados (ou seja, o ISO é instalado em uma partição específica dentro de um [dispositivo já particionado](/index.php/Partitioning "Partitioning") sem alterar outras partições).

**Nota:** Aqui, denotaremos a partição de destino como `/dev/sd**Xn**`. Em qualquer um dos seguintes comandos, ajuste **X** e **n** de acordo com o seu sistema.

*   Se ainda não tiver feito, crie uma [tabela de partição](/index.php/Partition_table "Partition table") em `/dev/sd**X**`.
*   Se ainda não tiver feito, crie uma partição no dispositivo. A partição `/dev/sd**Xn**` deve ser formatada para [FAT32](/index.php/FAT32 "FAT32").
*   Monte a imagem ISO, monte o sistema de arquivos FAT32 localizado no dispositivo flash USB e copie o conteúdo da imagem ISO para ele. Em seguida, desmonte a imagem ISO, mas mantenha a partição FAT32 montada (isso pode usado em etapas subsequentes). Por exemplo:

```
# mkdir -p /mnt/{iso,usb}
# mount -o loop archlinux-*versão*-x86_64.iso /mnt/iso
# mount /dev/sd**Xn** /mnt/usb
# cp -a /mnt/iso/* /mnt/usb
# sync
# umount /mnt/iso

```

Para inicializar um rótulo ou um [UUID](/index.php/UUID "UUID") para selecionar, é necessário informar a partição a ser inicializada. Por padrão, o rótulo `ARCH_*AAAAMM*` (com o ano e mês de lançamento apropriado) é usado. Assim, o [rótulo do sistema de arquivos](/index.php/Persistent_block_device_naming#by-label "Persistent block device naming") precisa ser definido de acordo, por exemplo, usando *gparted*. Alternativamente, você pode mudar este comportamento alterando as linhas terminadas por `archisolabel=ARCH_*AAAAMM*` no arquivo `/mnt/usb/arch/boot/syslinux/archiso_sys.cfg` (para inicialização de BIOS), e em `/mnt/usb/loader/entries/archiso-x86_64.conf` (para inicialização com UEFI). Para usar um UUID, substitua as porções de linhas com `archiso*dispositivo*=/dev/disk/by-uuid/**SEU-UUID**`. O UUID pode ser recuperado com `blkid -o *valor* -s UUID /dev/sd**Xn**`.

**Atenção:** A incompatibilidade de rótulos ou o UUID errado impede a inicialização da mídia criada.

Os arquivos de inicialização legada do Syslinux são estão pré-instalados em `/mnt/usb/arch/boot/syslinux`. Se você quiser ser capaz de inicializar seu pendrive USB no modo legado, instale o pacote [syslinux](https://www.archlinux.org/packages/?name=syslinux) e siga as instruções em [Syslinux#Manual install](/index.php/Syslinux#Manual_install "Syslinux").

#### No Windows

**Nota:**

*   Para formatação manual, não use nenhum utilitário **criador de USB inicializável** para criar o USB UEFI inicializável. Para formatação manual, não use *dd para Windows* para inserir o ISO na unidade USB.
*   Nos comandos abaixo, **X:** é considerado como sendo a unidade flash USB no Windows.
*   Windows usa barra invertida `\` como separador de caminho, então o mesmo é usado nos comandos abaixo.
*   Todos os comandos devem ser executados no prompt de comandos do Windows **como administrador**.
*   `>` denota o prompt de comando do Windows.

*   Particione e formate o drive USB usando o [particionador de USB Rufus](https://rufus.akeo.ie/). Selecione a opção de esquema de partição como **MBR para BIOS e UEFI** e sistema de arquivos como **FAT32**. Desmarque a opção "Criar um disco inicializável usando imagem ISO" e "Criar arquivos estendidos de rótulo e ícone".
*   Altere o **Rótulo do Volume** da unidade flash USB `X:` para corresponder ao LABEL mencionado na parte `archisolabel=` em `<ISO>\loader\entries\archiso-x86_64.conf`. Esta etapa é necessária para o ISO oficial ([Archiso](/index.php/Archiso_(Portugu%C3%AAs) "Archiso (Português)")). Esta etapa também pode ser executada usando o Rufus, durante a etapa anterior de "particionamento e formatação".
*   Extraia a ISO (similar a extrair o arquivo ZIP) para a unidade flash USB usando [7-Zip](https://www.7-zip.org/).
*   Baixe os binários oficiais Syslinux 6.xx (arquivo zip) de [https://www.kernel.org/pub/linux/utils/boot/syslinux/](https://www.kernel.org/pub/linux/utils/boot/syslinux/) e extrai-a. A versão do Syslinux deve ser a mesma versão usada na imagem ISO.

*   Execute o comando a seguir (no prompt de comando do Windows, como admin):

```
> cd bios\
> for /r %Y in (*.c32) do copy "%Y" "X:\arch\boot\syslinux\" /y
> copy mbr\*.bin X:\arch\boot\syslinux\ /y

```

*   Instale Syslinux no USB executando (use `win64\syslinux64.exe` para Windows x64):

```
> cd bios\
> win32\syslinux.exe -d /arch/boot/syslinux -i -a -m X:

```

**Nota:**

*   A etapa acima instala o `ldlinux.sys` do Syslinux no VBR da partição USB, define a partição como "active/boot" na tabela de partições MBR e grava o código de inicialização do MBR no primeiro código de inicialização de 440 bytes região do USB.
*   O opção `-d` espera um caminho com separador de caminho de barra como nos sistemas * unix.

## Outros métodos para sistemas BIOS

### No GNU/Linux

#### Usando uma unidade USB multiboot

Isso permite inicializar vários ISOs de um único dispositivo USB, incluindo o archiso. Atualizar uma unidade USB existente para uma ISO mais recente é mais simples do que na maioria dos outros métodos. Veja [Unidade USB de inicialização múltipla](/index.php/Multiboot_USB_drive "Multiboot USB drive").

#### Usando o utilitário de disco do GNOME

As distribuições Linux que usam o GNOME podem facilmente criar um live CD através do [nautilus](https://www.archlinux.org/packages/?name=nautilus) e do [gnome-disk-utility](https://www.archlinux.org/packages/?name=gnome-disk-utility). Basta clicar com o botão direito no arquivo *.iso* e selecionar *Abrir com Gravador de imagem de disco*. Quando o Utilitário de disco do GNOME abrir, especifique a unidade flash no menu suspenso *Destino* e clique em *Iniciar Restauração*.

#### Fazendo uma unidade USB-ZIP

Para alguns sistemas BIOS antigos, somente a inicialização de unidades USB-ZIP é suportada. Este método permite que você ainda inicialize a partir de uma unidade USB-HDD.

**Atenção:** Isso destruirá todas as informações da sua unidade flash USB!

*   Baixe [syslinux](https://www.archlinux.org/packages/?name=syslinux) e [mtools](https://www.archlinux.org/packages/?name=mtools) de repositórios oficiais.
*   Localize sua unidade usb com `lsblk`.
*   Digite `mkdiskimage -4 /dev/sd**x** 0 64 32` (substitua x com a letra de sua unidade). Isso vai levar um tempo.

A partir daqui, continue com o método de formatação manual. A partição será `/dev/sd**x**4` por causa da forma que unidades ZIP funcionam.

**Nota:** Não formate a unidade como FAT32; mantenha-o como FAT16.

#### Usando UNetbootin

O UNetbootin pode ser usado em qualquer distribuição Linux ou no Windows para copiar seu ISO para um dispositivo USB. No entanto, o Unetbootin sobrescreve o `syslinux.cfg`, portanto, ele cria um dispositivo USB que não inicializa corretamente. Por esse motivo, **Unetbootin não é recomendado** -- use `dd` ou um dos outros métodos discutidos neste tópico.

**Atenção:** O UNetbootin escreve sobre o `syslinux.cfg` padrão; isso deve ser restaurado antes que o dispositivo USB seja inicializado corretamente.

Edite `syslinux.cfg`:

 `sysconfig.cfg` 
```
default menu.c32
prompt 0
menu title Archlinux Installer
timeout 100

label unetbootindefault
menu label Archlinux_x86_64
kernel /arch/boot/x86_64/vmlinuz
append initrd=/arch/boot/x86_64/archiso.img archisodevice=/dev/sd**x1** ../../
```

Em `/dev/sd**x1**` você deve substituir **x** pela primeira letra livre após a última letra em uso no sistema onde você está instalando o Arch Linux (p.ex., Se você tiver dois discos rígidos, use `c`. Você pode fazer essa alteração durante a primeira fase de inicialização pressionando `Tab` quando o menu é exibido.

### No Windows

#### A forma Flashnul

[flashnul](https://translate.google.com/translate?hl=&sl=ru&tl=en&u=http%3A%2F%2Fshounen.ru%2Fsoft%2Fflashnul%2Freadme.rus.html&sandbox=1) é um utilitário para verificar a funcionalidade e manutenção da memória Flash (Flash USB, IDE-Flash, SecureDigital, MMC, MemoryStick, SmartMedia, XD, CompactFlash etc).

Em um prompt de comando, chame flashnul com `-p` e determine qual índice de dispositivo é seu drive USB, por exemplo:

 `C:\>flashnul -p` 
```
Available physical drives:
Available logical disks:
C:\
D:\
E:\

```

Depois de determinar qual é o dispositivo correto, você pode gravar a imagem em sua unidade, chamando flashnul com o índice do dispositivo, `-L` e o caminho para sua imagem, por exemplo:

```
C:\>flashnul **E:** -L *caminho\para\arch.iso*

```

Contanto que você tenha certeza de que deseja gravar os dados, digite yes e espere um pouco para que eles sejam gravados. Se você receber um erro de acesso negado, feche todas as janelas do Explorer abertas.

Se sob o Vista ou o Win7, você deve abrir o console como administrador, senão o flashnul não conseguirá abrir o pendrive como um dispositivo de bloco e só poderá gravar através dos meios fornecidos pelo Windows.

**Nota:** Confirmado que você precisa usar letra de unidade em oposição ao número. flashnul 1rc1, Windows 7 x64.

#### Carregar a mídia de instalação da RAM

Este método usa [Syslinux](/index.php/Syslinux "Syslinux") e um [Ramdisk](/index.php/Ramdisk "Ramdisk") ([MEMDISK](https://wiki.syslinux.org/wiki/index.php/MEMDISK)) para carregar toda a imagem ISO do Arch Linux na RAM. Como isso será executado inteiramente a partir da memória do sistema, você precisará certificar-se de que o sistema em que você estará instalando tenha uma quantidade adequada. Uma quantidade mínima de RAM entre 500 MB e 1 GB deve ser suficiente para uma instalação do Arch Linux baseada em MEMDISK.

Para obter mais informações sobre os requisitos do sistema Arch Linux, bem como sobre os do MEMDISK, consulte o [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação") e [aqui](http://www.etherboot.org/wiki/bootingmemdisk#preliminaries). Para referência, aqui está o [tópico do fórum anterior](https://bbs.archlinux.org/viewtopic.php?id=135266).

**Dica:** Uma vez que o instalador tenha concluído o carregamento, você pode simplesmente remover o pendrive e até mesmo usá-lo em uma máquina diferente para iniciar o processo novamente. A utilização do MEMDISK também permite inicializar e instalar o Arch Linux de e para a mesma unidade flash USB.

##### Preparar a unidade flash USB

Comece formatando a unidade flash USB como **FAT32**. Em seguida, crie as seguintes pastas na unidade recém-formatada.

*   `Boot`
    *   `Boot/ISOs`
    *   `Boot/Settings`

##### Copiar os arquivos necessários à unidade flash USB

Em seguida copie o ISO que você gostaria de inicializar na pasta `Boot/ISOs`. Depois disso, extraia os seguintes arquivos da última versão do [syslinux](https://www.archlinux.org/packages/?name=syslinux) do site [aqui](https://www.kernel.org/pub/linux/utils/boot/syslinux/) e copie-os para o seguinte pastas.

*   `./win32/syslinux.exe` para a pasta `Área de trabalho` ou `Downloads` em seu sistema.
*   `./memdisk/memdisk` para a pasta `Settings` em seu dispositivo flash USB.

##### Criar o arquivo de configuração

Depois de copiar os arquivos necessários, navegue até a unidade flash USB, /boot/Settings e crie um arquivo `syslinux.cfg`.

**Atenção:** Na linha `INITRD`, certifique-se de usar o nome do arquivo ISO que você copiou para a sua pasta `ISOs`.
 `/Boot/Settings/syslinux.cfg` 
```
DEFAULT arch_iso

LABEL arch_iso
        MENU LABEL Arch Setup
        LINUX memdisk
        INITRD /Boot/ISOs/archlinux-*versão*-x86_64.iso
        APPEND iso
```

Para mais informações sobre o Syslinux veja o [artigo do Arch Wiki](/index.php/Syslinux "Syslinux").

##### Etapas finais

Finalmente, crie um arquivo `*.bat` onde `syslinux.exe` está localizado e execute-o ("Executar como administrador" se você estiver no Vista ou no Windows 7):

 `C:\Documents and Settings\usuário\Área de trabalho\install.bat` 
```
@echo off
syslinux.exe -m -a -d /Boot/Settings X:

```

## Solução de problemas

*   Se você receber o erro "device did not show up after 30 seconds" devido à não montagem do `/dev/disk/by-label/ARCH_*AAAAMM*`, tente renomear sua mídia USB para `ARCH_*AAAAMM*` (por exemplo, `ARCH_201501`).
*   Se você receber erros, tente usar outro dispositivo USB. Existem casos em que resolveu todos os problemas.

## Veja também

*   [Gentoo wiki - LiveUSB/HOWTO](https://wiki.gentoo.org/wiki/LiveUSB/HOWTO)
*   [Fedora wiki - How to create and use Live USB](https://fedoraproject.org/wiki/How_to_create_and_use_Live_USB)
*   [openSUSE wiki - SDB:Live USB stick](https://en.opensuse.org/SDB:Live_USB_stick)