Este manual foi traduzido com base no guia em inglês criado em 25/02/2012.

O guia que está sempre atualizado é mantido na página [Official_Installation_Guide](/index.php/Installation_guide "Installation guide").

Este guia é válido somente para a release 2010.05 ou superior. Comentários são bem-vindos na [lista de discussão](https://www.archlinux.org/mailman/listinfo/arch-releng).

## Contents

*   [1 Introdução](#Introdu.C3.A7.C3.A3o)
    *   [1.1 O que é Arch Linux?](#O_que_.C3.A9_Arch_Linux.3F)
    *   [1.2 Licença](#Licen.C3.A7a)
*   [2 Pre-Instalação](#Pre-Instala.C3.A7.C3.A3o)
    *   [2.1 Arquiteturas](#Arquiteturas)
    *   [2.2 Imagens Disponíveis](#Imagens_Dispon.C3.ADveis)
    *   [2.3 AIF, a instalação da ferramenta](#AIF.2C_a_instala.C3.A7.C3.A3o_da_ferramenta)
    *   [2.4 Obtendo Arch Linux](#Obtendo_Arch_Linux)
    *   [2.5 Preparando Media de Instalação](#Preparando_Media_de_Instala.C3.A7.C3.A3o)
*   [3 Instalando Arch Linux](#Instalando_Arch_Linux)
    *   [3.1 Utilizando a Media de Instalação](#Utilizando_a_Media_de_Instala.C3.A7.C3.A3o)
        *   [3.1.1 Pre-boot](#Pre-boot)
        *   [3.1.2 Pós-boot](#P.C3.B3s-boot)
    *   [3.2 Utilizando PXE (Network booting)](#Utilizando_PXE_.28Network_booting.29)
        *   [3.2.1 Servidor](#Servidor)
        *   [3.2.2 Cliente](#Cliente)
    *   [3.3 Executando a instalação](#Executando_a_instala.C3.A7.C3.A3o)
        *   [3.3.1 Procedimento de Instalação Interativo](#Procedimento_de_Instala.C3.A7.C3.A3o_Interativo)
            *   [3.3.1.1 Selecionando Fontes](#Selecionando_Fontes)
                *   [3.3.1.1.1 Opicional: somente quando estiver utilizando fontes de rede](#Opicional:_somente_quando_estiver_utilizando_fontes_de_rede)
                    *   [3.3.1.1.1.1 Configuração de Rede](#Configura.C3.A7.C3.A3o_de_Rede)
                    *   [3.3.1.1.1.2 Escolhendo as Fontes (Espelhos)](#Escolhendo_as_Fontes_.28Espelhos.29)
        *   [3.3.2 Definindo o Editor](#Definindo_o_Editor)
            *   [3.3.2.1 Definindo Horário](#Definindo_Hor.C3.A1rio)
            *   [3.3.2.2 Preparando Disco Rígido](#Preparando_Disco_R.C3.ADgido)
                *   [3.3.2.2.1 Auto-Preparação](#Auto-Prepara.C3.A7.C3.A3o)
                *   [3.3.2.2.2 Particionando manualmente o Disco Rígido](#Particionando_manualmente_o_Disco_R.C3.ADgido)
                *   [3.3.2.2.3 Configurando manualmente os blocos do dispostivio, sistema de arquivo e pontos de montagem](#Configurando_manualmente_os_blocos_do_dispostivio.2C_sistema_de_arquivo_e_pontos_de_montagem)
                *   [3.3.2.2.4 Rollbacks](#Rollbacks)
            *   [3.3.2.3 Selecionando Pacotes](#Selecionando_Pacotes)
            *   [3.3.2.4 Instalando Pacotes](#Instalando_Pacotes)
            *   [3.3.2.5 Configuração do Sistema](#Configura.C3.A7.C3.A3o_do_Sistema)
            *   [3.3.2.6 Instação do Bootloader](#Insta.C3.A7.C3.A3o_do_Bootloader)
            *   [3.3.2.7 Encerrando a Instalação](#Encerrando_a_Instala.C3.A7.C3.A3o)
        *   [3.3.3 Procedimento de Instalação Automática](#Procedimento_de_Instala.C3.A7.C3.A3o_Autom.C3.A1tica)
            *   [3.3.3.1 Sintaxe do Arquivo de Configuração](#Sintaxe_do_Arquivo_de_Configura.C3.A7.C3.A3o)
        *   [3.3.4 Personalização de Instalação](#Personaliza.C3.A7.C3.A3o_de_Instala.C3.A7.C3.A3o)
*   [4 Seu novo sistema](#Seu_novo_sistema)
*   [5 Maiores Informações](#Maiores_Informa.C3.A7.C3.B5es)
    *   [5.1 Gerenciamento de Pacotes](#Gerenciamento_de_Pacotes)
    *   [5.2 APENDICE](#APENDICE)

# Introdução

## O que é Arch Linux?

Arch Linux é desenvolvido de forma independente para i686 e x86_64 a distribuição otimizada que foi originalmente baseada em idéias de CRUX.
O desenvolvimento está focado em um equilíbrio de simplicidade, elegância e correção de código- para o software de borda.
O seu design leve e simples faz com que seja fácil de estender e moldar o sistema da forma que desejar.

## Licença

Arch Linux e os scripts possuem copyright

2002-2007 Judd Vinet

2007-2010 Aaron Griffin

e são licenciados sob a GNU General Public License (GPL).

# Pre-Instalação

## Arquiteturas

Arch Linux está otimizado para processadores i686 e x86_64, porém não será executado em gerações mais baixas ou gerações incompatíveis de processadores x86 (i386, i486 or i586).
Os processadores Pentium Pro, Pentium II or AMD Athlon (K7) ou superiores são necessários. Antes de instalar o Arch Linux, você deve escolher o método de instalação que gostaria de usar.

## Imagens Disponíveis

Arch Linux fornece isofiles que podem ser escritas em CD-ROMs ou discos e dispositivos USB

O Isolinux é carregado na inicialização do boot.

*   Na imagem do "core" existe um snapshot dos pacotes básicos.
    Estas imagens são mais adequados para as pessoas que têm uma ligação à Internet que é lento ou difícil de configurar.
*   Na imagem de "rede" não contêm todos os pacotes, e sempre irá utilizar a rede para instalar os pacotes.

Todas as imagens podem também ser usados ​​como ambientes de recuperação. As imagens correm como qualquer sistema instalado Arch Linux.
Na verdade, eles são exatamente o mesmo, apenas instalado em uma imagem de CD ou USB em vez de um disco rígido.
Eles incluem toda a "base" e conjunto de pacotes, bem como vários utilitários e drivers de rede.
Se há alguma que você precise em tempo de execução, é só pegar sua conexão com a Internet e instalá-lo usando pacman.
A referência de comando curta pacman está disponível no final deste documento.

Todas as imagens estão disponíveis em i686, x86_64 ou ambas. Este último contém e permite que você escolha uma arquitetura no boot.

## AIF, a instalação da ferramenta

Arch Linux usa AIF aka 'Arch Linux Installation Framework' para suas instalalções.
Essa ferrametna - escrita em bash - consistem num conjunto de bibliotecas para executar diversas funções (instalações de pacotes, configurações, etc) e procedimentos que utilizam estas biliotecas para fornecer de forma fácil as instalações ou tarefas relacionadas. Estes procedimentos são enviados por padrão:

*   interactive: Um procedimento de instalação interativa, que lhe pede algumas perguntas, orienta você através de uma instalação e ajuda você a configuração do sistema de destino alterando automaticamente algumas definições dependendo do que você fez anteriormente (por exemplo, configurações de rede)
    O sistema instalado terá inicialmente personalizável apenas uma parte do conjunto "base" de pacotes instalados alguns utilitários e os drivers que você precisa para ficar on-line.
    Em seguida, uma vez que inicializado com êxito o sistema instalado, você vai passar por um sistema de atualização e instalação de outros pacotes que você deseja. (alias como `/arch/setup` )
*   automatic: Um sistema automatizado, o processo de implantação 'deploy-tool-alike' projetada para a interatividade zero.
    Usa perfis para a configuração do sistema de destino. Veja /usr/share/FIA/examples/ para arquivos de perfil de exemplo. Os exemplos implementam cenários bastante genéricos, mas você é livre para alterá-los como você deseja instalar pacotes extras, fazer ajustes de configuração, etc.
*   base: básico, pouca interação na instalação com definições padrões.
    Este procedimento é herdado pela utilização de outros usuários e NÃO é um método muito recomendado.
*   partial-configure-network: apresenta a etapa de configuração de rede do procedimento interativo, para ajudá-lo a configurar a rede no ambiente ativo
*   partial-disks: Processa o subsistema carregado do disco ou realiza um rollback
*   partial-keymap: altera suas configurações de mapa de caracteres ou fonte do console. (apelido para `km`)

O beneficio dos procedimentos como partial-keymap e partial-configure-network, sobre a utilização de outras ferramentas, é que ao executa o procedimento interativo suas configurações podem ser fixadas no sistema que será instalado

Se você quiser ir além disso também pode:

*   escrever seus procedimentos ou substituir alguns partes dos procediemntos existentes
*   escreva suas bibliotecas, para fornecer novas funcionalidades

Para maiores informações, consulte o README do AIF.

## Obtendo Arch Linux

*   Você pode baixar o Arch Linux de diferentes fontes listadas na seguinte [download](https://www.archlinux.org/download/) página.

*   Você pode comprar um CD de instalação Archux, OSDisc ou LinuxCD e obter em qualquer lugar do mundo.

## Preparando Media de Instalação

*   Escolha e baixa a imagem torrent (preferencialmente) ou de sua fonte favorita.

*   Baixe o iso/<release>/sha1sums.txt

*   Verifique a integridade da imagem obtida usando sha1sum:

    sha1sum --check sha1sums.txt

    archlinux-XXX.iso: OK

*   Grave a imagem ISO em um CD-R ou CD-RW usando um programa de sua escolha, ou se utilizar um dispositivo de armazenamento USB mass, usando o binário dd ou um programa de escrita raw:

    dd if=archlinux-XXX.iso of=/dev/sdX

Certifique-se de usar o caminho do dispositivo e não da partição (/dev/sdX e NÃO /dev/sdX1).
Esse comando vai sobrescrever os arquivos existentes no dispositivo USB, utilize apenas se não houverem arquivos importantes no dispositivo.

# Instalando Arch Linux

## Utilizando a Media de Instalação

### Pre-boot

Certifique-se que a BIOS está configurada para iniciar por seu CD-ROM ou dispositivo USB. Reinicie seu computador com o CD de Instalação Arch Linux, por exemplo. Após inicialização da instalação, você irá ver a logo do Arch Linux e o menu do Isolinux aguardando você selecionar. Muito provavelmente você pode simplesmente pressionar enter neste momento.

### Pós-boot

Ao final do processo de boot, você deve estar em um prompt de login com algumas instruções simples na parte superior da tela.
Você deve logar como root. Neste ponto, você pode, opcionalmente, realizar preparações manuais e iniciar a instalação.

Se você prefere um keymap non-US ou consolefont específico, km tipo para mudar qualquer um destes.

*   Se você prefere uma configuração de mapa de caracteres que não seja US ou a fonte de caracteres especificada, utilize `km` para altera qualquer um desdes.
*   Se você precisa de acesso à rede antes de iniciar o instalador (o processo interativo permite que você configure a rede para NET instalações),
    você pode utilizar `aif -p partial-configure-network`

Para ambos os itens, para que as configurações alteradas devem ser lembradas, para que sejam aplicadas no sistema alvo, quando utilizado o processo interativo.

Há também um login `arch` que pode ser útil se você quer fazer as coisas como usuário não privilegiado.</br> Muitas pessoas não precisam.

Você irá descobrir que tudo que você precisa para realizar esta instalação pode ser encontada em /arch

## Utilizando PXE (Network booting)

### Servidor

Com outra máquina em funcionamento com Arch Linux (live ou normal), você precisa instalar e configurar um dhcp e daemon tftpd. Dnsmasq é uma boa escolha que pode fazer as duas coisas. Você também precisa de um nbd (network block devise) daemon então o cliente poderá carregar os arquivos necessários.

Você opde buscar maiores informações na seguinte wiki: [Community contributed documentation](/index.php/Archiso-as-pxe-server "Archiso-as-pxe-server")

### Cliente

Configure primeiramente seu sistema para realizar o boot pela rede (pxe).</br> Você irá obter um IP através do servidor e irá carregar automaticamente todos os arquivos necessários pela rede. Uma vez iniciado, você pode prosseguir normalmente.

## Executando a instalação

Você pode utilizar quaisquer procedimentos interativos ou um dos automáticos.
Veja na seção [2.3 AIF, a instalação da ferramenta](#AIF.2C_a_instala.C3.A7.C3.A3o_da_ferramenta) ou no readme do AIF para maiores informações.

### Procedimento de Instalação Interativo

Através do `/arch/setup` ou pelo `aif -p interactive -d -l` para iniciar.

Após a mensagem de boas-vindas e aviso você será apresentado com o menu principal de instalação. Você poderá utilizar as teclas de UP e DOWN para navegar nos menus. Utilize o TAB para alterar entre os botões e o ENTER para selecionar. A qualquer momento durante o processo de instalação, você pode mudar a sua sétima interface do console (com ALT-F7) para ver a saída dos comandos da instalação que está em execução. Utilize (ALT-F1) para voltar à primeira interface do console onde o instalador deve está sendo executado, e os demais F-[2..6] devem ser utilizados se desejar, por algum motivo, intervir nos processos em execução.

#### Selecionando Fontes

No primeiro passo que você deve escolher os repositórios de instalação do Arch Linux. Se você possui uma conexão rápida à Internet, você pode preferir habilitar as fontes para obter os pacotes mais recentes que os existentes na imagem utilizada no boot. Se você estiver utilizando uma imagem de instalação pela INTERNET você não tem muitas escolhas ;-). Você pode montar seus repositórios no sistema de arquivo manualmente. Se você estiver utilizando a imgem de "CORE" e não tem uma conexão rápida com a internet, você provavelmente irá utilizar os arquivos inclusos no 'core', a menos que esteja muito desatualizado. É requirido somente selecionar o repositorio do 'core'. Você pode combinar entre repositórios locais e remotos, mas faça isso somente se você souber o que está fazendo ;-). (combinar arquivos de core antigo com novos pacotes da internet podem resultar em pacotes quebrados - isso seria trágico)

##### Opicional: somente quando estiver utilizando fontes de rede

###### Configuração de Rede

As entradas de configuração de rede irão habilitar e configurar seus dispositivos de rede Se você estiver usando um dispositivo de rede sem fio, você vai precisar usar os utilitários habituais para configurá-lo manualmente. Uma lista de todos dispositivos de rede disponíveis para você. Se não tiver dispositivos ethernet disponíveis, ou o dispositivo que dejese utilizar não seja encontrado você pode mudar para outro consola e carregar o módulo manualmente. Se você não estiver podendo configurar seu dispositivo de rede, verifique se ele está corretamente instalado (fisicamente), e que é suportado pelo kernel do Linux.

Quando as correções do modulos forem carregadas e sua placa de rede for listada, você poderá selecionar o dispositivo que será configurado, assim como você poderar receber as configurações de rede por DHCP. Se sua rede usar DHCP, escolha YES e deixe o instalador trabalhar. Se você selecionar NO, você precisará entrar com as informações de rede manualmente. De qualquer forma, sua rede deve ser configurada com sucesso, e você poderá verificar a conectividade utilizando ferramentas como ping no console.

###### Escolhendo as Fontes (Espelhos)

Escolha da fonte será habilitada para você escolher as fontes de sua preferência que instalarão os pacotes de seu sistema Arch Linux. Você deve escolher uma fonte situada próxima a sua localidade, para que os arquivos sejam baixados com maior velocidade. Em outros momentos da instalação você poderá alterar a fonte padrão de download de suas fontes.

**Nota: ** ftp.archlinux.org é limitada a 50 KB/s.

As entradas no menu estão disponíveis apenas na escolha da instalação por FTP. Após a preparação bem sucedida, volte ao menu principal.

### Definindo o Editor

Você pode escolher nano e vi (pico/joe/vim se você instalar em um console separado). Você pode pular este menu, mas você será solicitado novamente quando necessário.

#### Definindo Horário

Defina a data e hora do relógio. Primeiro você deve informar o localtime ou fuso por UTC. UTC tem preferência, mas se você tem um SO instalado que não pode lidar com fusos UTC da BIOS corretamente, como o Windows, você terá que escolher localtime. No Próximo passo da instalação selecionar o continente/país (timezone), e habilitar a configuração de data e hora (você pode usar também [NTP](http://www.ntp.org/) se sua internet esteja ativa)

#### Preparando Disco Rígido

Na preparação do Disco Rígido você terá duas alteranativas: para preparar o driver de instalação e desfazer as alterações.

*   Auto-prepare: irá particionar automaticamente (e sobrescrever tudo) um disco de sua escolha. Ele cria um layout simples com /boot, swap, / e /home onde você pode escolher o sistema de arquivos e seus tamanhos.
*   Se você precisar de mais alterações, se deve particionar manualmente o(s) disco(s) e então especificar manualmente todas as configurações das partições. Você pode usar lvm e dm_crypt dessa forma.
*   O Rollback vai verificar quais sistemas de arquivos foram criados por esses métodos, desmontar as partições relevantes e destroir os volumes lvm e dm_crypt que você tenha criado. Você precisa dessa opção para desfazer ou refazer um determinado esquema.

Notas:

*   AIF pode lhe ajudar se você configurar um novo dm_crypt e lvm, mas não softraid.
*   AIF atualmente não ajuda na criação de grupos de volumes que abrangem múltiplos os volumes. (se precisar use: vgcreate)
*   AIF suporta a reutilização de sistemas de arquivos, mas pode encontrar blockdevice.

##### Auto-Preparação

Auto-Prepare will automatically partition a hard drive of your choice into a /boot, swap, a root partition, and a /home and then create filesystems on all four. These partitions will also be automatically mounted in the proper place. To be exact, this option will create:

*   32 MB ext2 /partição de boot
*   256 MB swap
*   7.5 GB partição principal
*   /home partição destinada ao usuário

Você será solicitado a alterar o tamanho dos volumes, o /home utilizará o espaço restante do disco. Pode também customizar o uso do sistema de arquivo para o /boot e para o root e /home.

**AUTO-REPARE APAGARÁ TODOS OS DADOS NO DISCO ESCOLHIDO**

##### Particionando manualmente o Disco Rígido

Aqui você pode selecionar os discos quer deseja particionar, e você será mandado para o programa cfdisk onde pode modificar livremente as informações de até que escreva [Write] e saia [Quit]. Você precisar ser root para continuar a instalação.

##### Configurando manualmente os blocos do dispostivio, sistema de arquivo e pontos de montagem

Nesse menu as partições encontradas serão listadas. No topo você pode criar o novo sistema de arquivos. Você deveria estar ciente dessas coisas:

*   Isso é apenas um modelo, tudo será definido somente após a confirmação.
*   Alguns sistemas de arquivos farão com que criem novos blockdevices. Esse é o caso para dm_crypt e lvm volumes. Você vai vê-los no modelo e você pode usá-los para colocar um outro sistema de arquivos em cima dele.
*   Quando perguntado sobre as opções de ferramentas mkfs, deve-se passar argumentos que irão literalmente ser adicionados ao chamar mkfs Por exemplo, para disabilitar o journal no sistema de arquivos ext:
    *   não faça: `^has_journal`
    *   mas sim: `-O ^has_journal`
*   Use 'dev' da forma mais simples para se referir a seus discos em arquivos de configuração, tais como o fstab e grub. Atualizações de Kernel provocam a renomeação de dispositivos, o que pode causar problemas. O 'uuid' é um hassle-free, forma concreta de se referir ao seu disco, 'label' vai usar labels do sistema de arquivo - no qual você pode escolher - e voltar para 'dev' se preciso for.

Quando o sistema de arquivo estiver completamente configurado, você pode selecionar 'Done'. Neste ponto uma verificação será executada o que irá dizer-lhe todos os erros críticos e/ou retornar alguma(s) advertência(s) que você pode ignorar (sem swap). Se nada for encontrado, você pode voltar para corrigir esses problemas ou continuar ao ponto em que tudo será configurado do jeito que lhe foi perguntado.

Por exemplo, se quiser configurar que usar LVM em cima do dm_crypt, seria:

*   tenha certeza que você tem 2 partições: uma pequena parte descriptografada para o boot (~ 100M) e uma com o restante criptografada para o sistema. (faça isso com "Manually partition hard drives")
*   em seu /dev/sdX1, faça um sistema de arquivo ext2 para o /boot
*   em seu /dev/sdX2, faça um volume dm_crypt, com label sdX2crypt (ou outra label que preferir)
*   /dev/mapper/sdX2crypt irá parecer. Coloque um partição física LVM nele
*   /dev/mapper/sdX2crypt+ irá aparecer. Essa é a representação para o volume físico. Coloque um volumegroup para ele, com a label cryptpool (ou outra label que preferir)
*   /dev/mapper/cryptpool irá aparecer. Com esse volumegroup você poderá colocar outros multiplos volumes logicos. Criar 2:
    *   uma com tamanho 5G: cryptroot (label)
    *   uma com tamanho 10G: crypthome (label)
*   2 novos volumes aparecerão:
    *   /dev/mapper/cryptpool-cryptroot: com esse blockdevice, você pode colocar seus sistemas de arquivo raiz (root), com ponto de montagem /.
    *   /dev/mapper/cryptpool-crypthome é o blockdevice no qual você pode colocar seu sistema de arquivo com ponto de montagem em /home.
*   Se você quiser um espaço para swap, crie um volume lógico para a swap e coloque um volume de swap volume nele.
*   Que é isso! Se você selecionar 'done' ele deveria processar esse modelo e criar seus discos com as configurações especificadas. O legal dessa parte é que você pode escolher valores relativamente pequenos para seus volumes iniciais, e se você precisar de mais espaço posteriormente você pode aumentar o volume lógico e o colocar o sistema de arquivo sobre ele.

##### Rollbacks

A função de rollback irá processar tudo que é necessário para "retornar" as configurações feitas pelo 'Manually configure block devices, filesystems and mountpoints' ou passo de 'Autoprepare', para pertmitir que refaça completamente suas configurações.

Ele vai:

*   desmontar os sistemas de arquivos destinados ao sistema
*   destroir/desfazer volumes lvm e dm_crypt.

Ele não irá:

*   voltar suas partições
*   remover 'simplesmente' sistemas de arquivos como o ext3, xfs, swap etc.

A razão para isso é bem simples: somente coisas que possam perturbar as tarefas subsequentes aos preparativos de disco rígido precisam ser desfeitas.

#### Selecionando Pacotes

Seleção de pacotes irá deixar você selecionar os pacotes que deseja instalar pelo CD, USB ou espelhos na NET. Primeiramente, você será solicitado a selecionar um pacote bootloader (o bootloader irá ser configurado após do estágio de "Install Bootloader"). Depois disso, você poderá escolher os grupos de pacotes a partir do qual você geralmente costuma instalar seus pacotes, então ajustar sua seleção de pacotes individuais a partir dos grupos que você escolheu. É recomendado que instale todos os pacotes "base", mas não qualquer coisa. A única exceção a essa regra é a instalação de pacotes que precise para se conectar a Internet.

Uma vez selecionados os pacotes que precise, saia da tela de seleção e continue ao próximo passo.

#### Instalando Pacotes

Pacotes de instalação irão agora instalar o sistema básico e quaisquer outros pacotes selecionados com dependências resolvidas, em seu disco rígido.

#### Configuração do Sistema

Configurando sistema para muitas coisas:

*   automaticamente vem pré-configurados alguns arquivos (por exemplo, do grub menu.lst mkinitcpio.conf HOOKS, as configurações de mapa de caracteres em rc.conf, espelhos para pacman, etc)
*   pré-configurar alguns arquivos de configuração depois de acordado. (por exemplo, configurações de rede)
*   permitem que você altere manualmente os arquivos de configuração importantes para o seu sistema de destino.
*   permitem que você defina a senha de root para o destino.
*   executar automaticamente algumas ferramentas que utilizam a configuração atualizada (localidades, mkinitcpio, configurações de tempo, etc)

**Arquivos de Configuração**

Estes são os principais arquivos de configuração do Arch Linux. Se você precisar de ajuda para configurar algum serviço em específico, favor ler a página no manual ou quaisquer referências de documentação online que precise. Em muitos casos, o Arch Linux [Wiki](https://wiki.archlinux.org/) e [forums](https://bbs.archlinux.org/) são uma rica fonte de ajuda também.

*   /etc/rc.conf
*   [/etc/fstab](/index.php/Fstab "Fstab")
*   /etc/mkinitcpio.conf
*   /etc/modprobe.d/modprobe.conf
*   /etc/resolv.conf
*   /etc/hosts
*   /etc/locale.gen
*   /etc/pacman.d/mirrorlist
*   /etc/pacman.conf
*   /etc/crypttab

**/etc/rc.conf**

Este é o arquivo de configuração principal do Arch Linux. Ele permite que você configure seu teclado, fuso horário, nome da máquina, rede, daemons para executar e modulos para carregar no boot, perfis de usuário e mais.

**LOCALE:** Este define suas configurações de linguagem, que sera usada por todos i18n-friendly aplicações e utilitários. Veja em locale.gen as opções disponíveis abaixo. Essa configuração padrão This setting's default é boa para usuários US English.

**HARDWARECLOCK:** UTC se o relógia da BIOS estiver definido para UTC, ou localtime se o relógio de sua BIOS estiver setado a sua hora local. Se você tem um S.O. instalado que não pode lidar com a hora UTC da BIOS corretamente, como Windows, escolha localtime aqui, caso contrário você deve preferir UTC, o que torna o horario de verão um problema.

**USEDIRECTISA:** If set to "yes" it tells hwclock to use explicit I/O instructions to access the hardware clock. Otherwise, hwclock will try to use the /dev/rtc device it assumes to be driven by the rtc device driver. This setting's default "no" is fine for people not using an ISA machine.

**TIMEZONE:** Specifies your time zone. Possible time zones are the relative path to a zoneinfo file starting from the directory /usr/share/zoneinfo. For example, a German timezone would be Europe/Berlin, which refers to the file /usr/share/zoneinfo/Europe/Berlin. If you don't know the exact name of your timezone file, worry about it later.

**KEYMAP:** Defines the keymap to load with the loadkeys program on bootup. Possible keymaps are found in /usr/share/kbd/keymaps. Please note that this setting is only valid for your TTYs, not any graphical window managers or X! Again, the default is fine for US users.

**CONSOLEFONT:** Defines the console font to load with the setfont program on bootup. Possible fonts are found in /usr/share/kbd/consolefonts.

**CONSOLEMAP:** Defines the console map to load with the setfont program on bootup. Possible maps are found in /usr/share/kbd/consoletrans. Set this to a map suitable for the appropriate locale (8859-1 for Latin1, for example) if you're using an UTF-8 locale above, and use programs that generate 8-bit output. If you're using X11 for everyday work, don't bother, as it only affects the output of Linux console applications.

**USECOLOR:** Enable (or disable) colorized status messages during boot-up.

**MOD_AUTOLOAD:** If set to "yes", udev will be allowed to load modules as necessary upon bootup. If set to "no", it will not.

**MODULES:** In this array you can list the names of modules you want to load during bootup without the need to bind them to a hardware device as in the modprobe.conf. Simply add the name of the module here, and put any options into modprobe.conf if need be. Prepending a module with a bang ('!') will blacklist the module, and not allow it to be loaded.

**USELVM:** Set to "yes" to run a vgchange during sysinit, thus activating any LVM groups

**HOSTNAME:** Set this to the hostname of the machine, without the domain part. This is totally your choice, as long as you stick to letters, digits and a few common special characters like the dash.

**INTERFACES:** Here you define the settings for your networking interfaces. The default lines and the included comments explain the setup well enough. If you use DHCP, 'eth0="dhcp"' should work for you. If you do not use DHCP just keep in mind that the value of the variable (whose name must be equal to the name of the device which is supposed to be configured) equals the line which would be appended to the ifconfig command if you were to configure the device manually in the shell.

**ROUTES:** You can define your own static network routes with arbitrary names here. Look at the example for a default gateway to get the idea. Basically the quoted part is identical to what you'd pass to a manual route add command, therefore reading man route is recommended or simply leave this alone.

**[/index.php/Network_Profiles NET_PROFILES]:** Enables certain network profiles at bootup. Network profiles provide a convenient way of managing multiple network configurations, and are intended to replace the standard INTERFACES/ROUTES setup that is still recommended for systems with only one network configuration. If your computer will be participating in various networks at various times (eg, a laptop) then you should take a look at the /etc/network-profiles/ directory to set up some profiles. There is a template file included there that can be used to create new profiles. This now requires the netcfg package.

**DAEMONS:** This array simply lists the names of those scripts contained in /etc/rc.d/ which are supposed to be started during the boot process. If a script name is prefixed with a bang (!), it is not executed. If a script is prefixed with an "at" symbol (@), then it will be executed in the background, ie. the startup sequence will not wait for successful completion before continuing. Usually you do not need to change the defaults to get a running system, but you are going to edit this array whenever you install system services like sshd, and want to start these automatically during bootup.

**[/etc/fstab](/index.php/Fstab "Fstab")**

Filesystem settings and mountpoints are configured here. The installer should have created the necessary entries. Ensure they are accurate and correct.

**/etc/mkinitcpio.conf**

This file allows you to fine-tune the initial ramdisk for your system. The ramdisk is a gzipped image that is read by the kernel during bootup. Its purpose is to bootstrap the system to the point where it can access the root filesystem. This means it has to load any modules that are required to "see" things like IDE, SCSI, or SATA drives (or USB/FW, if you are booting off a USB/FW drive). Once the ramdisk loads the proper modules, either manually or through udev, it passes control to the Arch system and your bootup continues. For this reason, the ramdisk only needs to contain the modules necessary to access the root filesystem. It does not need to contain every module you would ever want to use. The majority of your everyday modules will be loaded later on by udev, during the init process.

By default, mkinitcpio.conf is configured to autodetect all needed modules for IDE, SCSI, or SATA systems through so-called HOOKS. The installer should also have inserted hooks like crypt, lvm, keymap and usbinput if relevant. This means the default initrd should work for almost everybody. You can edit mkinitcpio.conf and remove the subsystem HOOKS (ie, IDE, SCSI, RAID, USB, etc) that you don't need. You can customize even further by specifying the exact modules you need in the MODULES array and remove even more of the hooks, but proceed with caution.

If you're using RAID on your root filesystem, the RAID settings near the bottom must be configured. See the wiki pages for RAID and mkinitcpio for more info. If you're using a non-US keyboard, you should also add the 'keymap' hook, as well as the 'usbinput' hook if you are using a USB keyboard.

**/etc/modprobe.d/modprobe.conf**

This tells the kernel which modules to load for system devices, and what options to set. For example, to have the kernel load the Realtek 8139 ethernet module when it starts the network (ie. tries to setup eth0), use this line:

```
 alias eth0 8139too

```

Most people will not need to edit this file.

**/etc/resolv.conf**

Use this file to manually setup your preferred nameserver(s). It should basically look like this:

```
 search domain.tld

 nameserver 192.168.0.1

 nameserver 192.168.0.2

```

Replace domain.tld and the ip addresses with your settings. The so-called search domain specifies the default domain that is appended to unqualified hostnames automatically. By setting this, a ping myhost will effectively become a ping myhost.domain.tld with the above values. These settings usually aren't mighty important, though, and most people should leave them alone for now. If you use DHCP, this file will be replaced with the correct values automatically when networking is started, meaning you can and should happily ignore this file.

**/etc/hosts**

This is where you stick hostname/ip associations of computers on your network. If a hostname isn't known to your DNS, you can add it here to allow proper resolving, or override DNS replies. You usually don't need to change anything here, but you might want to add the hostname and hostname + domain of the local machine to this file, resolving to the IP of your network interface. Some services, postfix for example, will bomb otherwise. If you don't know what you're doing, leave this file alone until you read man hosts.

**/etc/locale.gen**

This file contains a list of all supported locales and charsets available to you. When choosing a LOCALE in your /etc/rc.conf or when starting a program, it is required to uncomment the respective locale in this file, to make a "compiled" version available to the system, and run the locale-gen command as root to generate all uncommented locales and put them in their place afterwards. You should uncomment all locales you intend to use.

During the installation process, you do not need to run locale-gen manually, this will be taken care of automatically after saving your changes to this file. By default, all locales are enabled that would make sense by rc.conf's LOCALE= setting. To make your system work smoothly, you should edit this file and uncomment at least the one locale you're using in your rc.conf.

**/etc/pacman.d/mirrorlist**

This file contains a list of mirrors from which pacman will download packages for the official Arch Linux repositories. The mirrors are tried in the order in which they are listed. The $repo macro is automatically expanded by pacman depending on the repository (core, extra, community or testing).

If you are performing an FTP installation, the mirror you used to download the packages from will be added on top of the mirror list, in order to be used as the default mirror in your new Arch Linux system.

**/etc/pacman.conf**

Here you can customize pacman settings such as which repositories to use.

**/etc/crypttab**

If you use encryption on a device which is not used to bring up your root, (and hence is not enabled by the encrypt hook in mkinitcpio.conf), you should configure the volume in this file.

**Set Root Password**

At this step, you must set the root password for your system. Choose this password carefully, preferably as a mixture of alphanumeric and special characters, since this password allows you to modify critical parts of your system.

When you are done editing the configuration files choose Return to return to the main menu. The setup will regenerate the initial ramdisk to enable the changes you made in mkinitcpio.conf.

#### Instação do Bootloader

A Instalação do Bootloader irá lhe ajudar a configurar o bootloader que você selecionou no passo de "Select Packages" .

Um editor será aberto, permitindo que edite o arquivo de configuração do bootloader, que o instalador tem pré-preenchida. Você deve checar e modificar esse arquivo, se necessário.

**/boot/syslinux/syslinux.cfg** (Syslinux) After checking your bootloader configuration for correctness, you'll be asked to allow the installer to Set the Boot Flag and install the Syslinux MBR.

**/boot/grub/menu.lst** (Grub) After checking your bootloader configuration for correctness, you'll be prompted for a disk to install the loader to. You should install GRUB to the MBR of the installation disk.

#### Encerrando a Instalação

You will be shown a summary of the installation, listing the steps and whether they executed successfully or not. If all went well, exit the installer, type reboot at the command line, remove your installation media and cross your fingers!

### Procedimento de Instalação Automática

With the automatic installation procedure, you can do scripted/automatic installations. Veja em [2.3 AIF, a instalação da ferramenta](#AIF.2C_a_instala.C3.A7.C3.A3o_da_ferramenta) Em /usr/share/aif/examples você irá encontrar exemplos de profiles que terão pouca ou nenhuma alteração, para instalação do sistema:

*   generic-install-on-sda this file demonstrates some things you can do (adding custom packages, setting timezone, update config files etc) it sets up a simple installation (with a structure similar to what you get with Auto-prepare) on /dev/sda
*   fancy-install-on-sda very similar to generic-install-on-sda, but sets up a "filesystems on lvm on dm_crypt" system on /dev/sda

Note that these files are plain bash files, so if you want to define for example `SYNC_URL` it must be singlequoted to prevent bash expanding `$repo`

Invoke as `aif -p automatic -c /path/to/configfile` Obviously, don't forget to change the hard disk names unless you want to use /dev/sda.

#### Sintaxe do Arquivo de Configuração

O arquivo de configuração será carregado pelo bash, então ele precisa ter um código válido.

**PARTITIONS:** Permite definir partições dos disco, separando por espaço.

*   primeiro vem o arquivo de dispositivo para o disco rígido
*   em seguida, para cada partição que deseja o tamanho em MiB (ou '*' para o restando do espaço livre do disco), tipos de sistemas de arquivo e, opcionalmente, '+' para ligar flags de boot separadas por (':')

**BLOCKDATA:** Nesta variável de multiplas linhas você pode descrever para cada partição, como ela deve ser usado. Estude os exemplos para ver como ele funciona.

### Personalização de Instalação

You can also customize your installation experience by writing new procedures (possibly inheriting from current procedures) or config files for procedures that support it (eg automatic). You have all the aif libraries at your disposal and you can create new libraries. (see /usr/lib/aif) This is a moving target, so consult the AIF readme for more information.

# Seu novo sistema

Se deu tudo certo, você pode reiniciar o sistema (certifique-se de não iniciar novamente a partir do CD-ROM) e seu novo sistema vai iniciar

Você notará que no espaço do usuário os ganchos necessários para obter a sua raiz sistema de arquivos são executados. Você notará no início que no espaço do usuário (a parte que vem depois do bootloader) os 'hooks' (como definido na mkinitcpio.conf) necessários para obter a sua raiz sistema de arquivos são executados.
Se você possui lvm, o mesmo será executado no 'hook'. Se você usar criptografia, ele irá executar o mapa de caracteres e criptografar para que você possa entrar com sua senha para descriptografar o volume.

Uma vez que o sistema é inicializado, faça o login como root. Por padrão a senha é vazia mas você pode alterá-la

# Maiores Informações

## Gerenciamento de Pacotes

Pacman é o gerenciador de pacotes que acompanha o sistema instalado. Ele tem suporte as dependências e utilizar 'tar' ou 'gzip' como formato padrão de arquivo para os pacotes. Algumas tarefas comuns que você pode precisar usar Durante a instalação, são explicados abaixo com os seus respectivos comandos. Para explanar as opções adicionais do pacman, leia em 'man pacman' ou consulte a página do manual Arch Linux [Wiki](/index.php/Pacman "Pacman").

**Tarefas Comuns:**

*   Atualizar lista de repositório

    # pacman --sync --refresh

    # pacman -Sy

Este irá recuperar uma lista de pacotes dos repositórios definidos no arquivo /etc/pacman.conf e descompactá-lo para o banco de dados.

*   Busca de repositórios para o pacote

    # pacman --sync --search <regexp>

    # pacman -Ss <regexp>

Pesquisar por pacote nas bases de dados ou descrição que correspondam a 'regexp'.

*   Mostrar informações do pacote específico da base de banco do repositório

    # pacman --sync --info foo

    # pacman -Si foo

Displays information from the repository database on package foo (tamanho, data de criação, dependencias, conflitos, etc.)

*   Adiciona um pacote a partir do repositório

    # pacman --sync foo

    # pacman -S foo

Obter e instalar o pacote foo, com todas as dependências que ele requer. Antes de usar qualquer opção de sincronização, certifique-se que a lista de pacotes está atualizada.

*   Lista pacotes instalados

    # pacman --query

    # pacman -Q

Exibe uma lista de todos os pacotes instalados no sistema.

*   Verifica se o pacote especificado está instalado

    # pacman --query foo

    # pacman -Q foo

Este comando irá exibir o nome e versão do pacote foo se estiver instalado.

*   Exibir informações do pacote esperificado

    # pacman --query --info foo

    # pacman -Qi foo

Exibir informações do pacote foo (tamanho, data de instalação, data de criação, dependencias, conflitos, etc.)

*   Exibir lista de arquivos contidos no pacote

    # pacman --query --list foo

    # pacman -Ql foo

Lista todos os arquivos que pertencem ao 'foo'.

*   Descubra a qual pacote um arquivo específico pertence

    # pacman --query --owns /path/to/file

    # pacman -Qo /path/to/file

Esta consulta exibe o nome e versão dos pacotes contidos no arquivo referenciado pelo seu caminho.

## APENDICE

Veja [Official Arch Linux Install Guide Appendix](/index.php/Official_Arch_Linux_Install_Guide_Appendix "Official Arch Linux Install Guide Appendix") para acessar documentação não oficial, pode user muito útil para novos usuários.