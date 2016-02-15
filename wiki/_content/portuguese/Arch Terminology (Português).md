A intenção desta página é desmistificar os termos comumente usados pela comunidade do Arch Linux. Sinta-se à vontade para adicionar ou modificar quaisquer termos, mas por favor use a opção de editar da opção específica. Se você decidir adicionar algum termo, por favor adicione-o em ordem alfabética.

**Note:** Alguns itens estão fora da ordem alfabética enquanto falta terminar a tradução, mas serão reorganizados posteriormente

## Contents

*   [1 Arch Linux](#Arch_Linux)
*   [2 ABS](#ABS)
*   [3 ARM](#ARM)
*   [4 AUR](#AUR)
*   [5 PKGBUILD](#PKGBUILD)
*   [6 TU, Trusted User](#TU.2C_Trusted_User)
*   [7 bbs](#bbs)
*   [8 community/[community]](#community.2F.5Bcommunity.5D)
*   [9 core/[core]](#core.2F.5Bcore.5D)
*   [10 repositório do usuário/personalizado](#reposit.C3.B3rio_do_usu.C3.A1rio.2Fpersonalizado)
*   [11 Desenvolvedor](#Desenvolvedor)
*   [12 extra/[extra]](#extra.2F.5Bextra.5D)
*   [13 hwd](#hwd)
*   [14 hwdetect](#hwdetect)
*   [15 initramfs](#initramfs)
*   [16 initrd](#initrd)
*   [17 makepkg](#makepkg)
*   [18 namcap](#namcap)
*   [19 package](#package)
*   [20 Package maintainer](#Package_maintainer)
*   [21 pacman](#pacman)
*   [22 pacman.conf](#pacman.conf)
*   [23 repository/repo](#repository.2Frepo)
*   [24 RTFM](#RTFM)
*   [25 taurball](#taurball)
*   [26 testing/[testing]](#testing.2F.5Btesting.5D)
*   [27 udev](#udev)
*   [28 wiki](#wiki)

## Arch Linux

Arch deve ser referenciado como:

*   **Arch Linux**
*   **Arch** (Linux implícito)
*   **archlinux** (nome UNIX)

Archlinux, ArchLinux, archLinux, aRcHlInUx, etc. são todos estranhas mutações.

Oficialmente, o 'Arch' de "Arch Linux" é pronunciado /ˈɑrtʃ/ como em "archer"/arqueiro, ou "arch-nemesis" ("arqui-inimigo") e não como em "ark" ou "archangel" ("arcanjo").

## ABS

O [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), ou ABS, ("Sistema de Compilação do Arch") é útil para:

*   Fazer novos pacotes de software para os quais nenhum pacote está disponível
*   Personalizar/modificar pacotes existentes para ajustar suas necessidades (habilitando ou desabilitando opções)
*   Reconstruir seu sistema completo usando as flags do seu compilador, "a la Gentoo"
*   Fazer com que módulos do kernel funcionem no seu kernel personalizado

ABS não é necessário para se usar o Arch Linux, mas é muito útil.

## ARM

**Note:** Arch Rollback Machine fechou em 2013-08-18 [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1313360#p1313360)

O [Arch Rollback Machine](/index.php/Downgrading_packages#Arch_Rollback_Machine "Downgrading packages") é um espelho que não remove versões antigas dos pacotes e é, portanto, muito útil se você precisa fazer downgrade do seu sistema.

## AUR

O [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") (AUR) é um repositório dirigido por uma comunidade de usuários do Arch. O AUR foi inicialmente concebido para organizar o compartilhamento de [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") por toda comunidade e para expedir a inclusão de pacotes populares contribuídos por usuários para os repositórios do [core] e [extra] via repositório [community] do AUR.

O AUR é o local de nascimento de novos pacotes do Arch. Os usuários contribuem com seus pacotes para o AUR. A comunidade do AUR vota em seus pacotes favoritos e eventualmente, assim que um pacote receber pacotes suficientes, um Trusted User do AUR pode levar esse pacote para o repositório [community], o qual está acessível via [pacman](/index.php/Pacman "Pacman") e [ABS](/index.php/Arch_Build_System "Arch Build System").

Você pode acessar o repositório da comunidade de usuários do Arch Linux [aqui](https://aur.archlinux.org).

## PKGBUILD

Os [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") são pequenos scripts que constroem pacotes para o Arch Linux. Veja [Creating packages](/index.php/Creating_packages "Creating packages") para maiores detalhes.

## TU, Trusted User

Um [trusted user](/index.php/Trusted_Users "Trusted Users") ("usuário confiável"), é alguém que mantém o AUR e o repositório [community]. Trusted Users podem mover um pacote para o repositório [community], se ele foi votado como particular. TUs são apontados pela votação da maioria dos TUs existentes.

Os Trusted users seguem as [AUR Trusted User Guidelines (Português)](/index.php/AUR_Trusted_User_Guidelines_(Portugu%C3%AAs) "AUR Trusted User Guidelines (Português)") e [TU by-laws](https://aur.archlinux.org/trusted-user/TUbylaws.html)

## bbs

_bbs_ é o acrônimo para "bulletin board system", mas no caso do Arch, é somente o fórum para suporte localizado [aqui](https://bbs.archlinux.org).

## community/[community]

O repositório [community] é onde pacotes pré-compilados são disponibilizado pelos [Trusted Users](/index.php/Trusted_Users "Trusted Users"). A maioria dos pacotes no [community] vem do [AUR](/index.php/Arch_User_Repository "Arch User Repository").

Para acessar o repositório [community], descomente-o no `/etc/pacman.conf`.

## core/[core]

O repositório [core] contém os pacotes básicos para um sistema do Arch Linux. O [core] tem tudo necessário para ter um sistema de linha de comando funcionando.

## repositório do usuário/personalizado

Em inglês "custom/user repository", qualquer usuário pode criar um e disponibilizá-lo para outros usuários. Para criar um repositório, você precisa de um conjunto de pacotes e um arquivo de banco de dados compatível com o [pacman](/index.php/Pacman "Pacman") para seus pacotes. Hospede seus arquivos online e todo mundo poderá usar seu repositório adicionando-o como um repositório comum.

Veja [Custom local repository](/index.php/Custom_local_repository "Custom local repository").

## Desenvolvedor

Em inglês "developer", são semi-deuses trabalhando para melhorar o Arch por nenhum ganho financeiro. [Desenvolvedores](https://www.archlinux.org/developers/) são deixados para trás somente por seus deuses, Judd Vinet e Aaron Griffin, os quais por sua vez são deixados para trás por tacos.

## extra/[extra]

Coleção oficial de pacotes do Arch é razoalmente simples, mas suplementamos isso com um maior e mais completo do repositório "extra" que contém muitas das coisas que nunca entrou na coleção de pacotes centrais. Este repositório está constantemente aumentando com a ajuda de pacotes enviados da comunidade forte. É aqui onde os ambientes de trabalho, gerenciadores de janela e programas comuns são encontrados.

## hwd

[hwd](https://aur.archlinux.org/packages/hwd/) é uma ferramenta de detecção de hardware e gerador de `xorg.conf` para o Arch Linux. Em vez de executar um script de configuração automática que poderia ser esperado, hwd não altera a configuração existente. Ele detecta hardwares e módulos e fornece informação sobre como fazer alterações manualmente. Isso permite que o usuário tenha controle sobre seu próprio sistema, que é a filosofia básica do Arch Linux

## hwdetect

[hwdetect](/index.php/Hwdetect "Hwdetect") é uma script de detecção de hardware primariamente usado para carregar ou listar módulos para ser usado no `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` ou `/etc/[mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf")`. O script faz uso da informação exportada pelo subsistema de sysfs empregado pelo kernel do Linux.

## initramfs

Veja [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio").

## initrd

O arquivo especial `/dev/initrd` é um dispositivo de bloco somente leitura. O dispositivo `/dev/initrd` é um disco RAM que é inicializado (ex.: carregado) pelo carregador (bootloader) antes do kernel ser iniciado. O kernle, então, usa o conteúdo do dispositivo de bloco `/dev/initrd` para a segunda fase da inicialização do sistema.

Na primeira fase da inicialização, o kernel inicializa e monta uma sistema de arquivos raiz inicial do conteúdo do `/dev/initrd` (ex.: disco RAM inicializado peloe carregador (bootloader). Na segunda fase, drivers adicionais e outros módulos são carregados do conteúdo inicial raiz do dispositivo. Após carregar os módulos adicionais, um novo sistema de arquivos raiz (i.e. o sistema de arquivo raiz normal) é montado de um dispositivo diferente.

## makepkg

[makepkg](/index.php/Makepkg "Makepkg") vai construir pacotes para você. O makepkg vai ler metadados necessários de um arquivo [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). Tudo que ele precisa é uma plataforma Linux capaz de compilação, [wget](https://www.archlinux.org/packages/?name=wget) e alguns scripts de compilação. A vantagem a de compilar baseado em script é que você realmente faz o trabalho uma vez. Assim que você tiver o script de compilação para um pacote, tudo o que você precisará é executar makepkg e ele vai fazer o resto: baixa e balida os arquivos fontes, verifica as dependências, configura as configurações de tempo de compilação, compilação do pacote, instala o pacote em uma raiz temporária, faz personalizações, cria informações-meta e empacota toda a coisa para o [pacman](/index.php/Pacman "Pacman") usar.

## namcap

[namcap](/index.php/Namcap "Namcap") é um utilitário de análise de pacotes que procura por problemas com pacotes do Arch Linux ou em seus arquivos [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). Ele pode aplicar regras à lista de arquivos, no próprios arquivos ou em arquivos PKGBUILD individuais.

As regras retornam listas de mensagens. Cada mensagem pode ser uma dos três tipos: erro, aviso ou informação (pense nelas como notas ou comentários). Erros (referidos por "E:" são coisas que o namcap tem muita certeza de que estão erradas e precisam ser corrigidas. Avisos (referidos por "W:") são coisas que o namcap pensa que deveriam ser alteradas, mas se você sabe o que você está fazendo, então você pode ignorá-las. Informações (referidas por "I:") são apenas mostradas quando você usar o argumento de informação. Mensagens informacionais dão informações que podem ser úteis, mas é nada que tenha que ser alterado.

## package

Um package("pacote") é um conjunto de arquivos que contém:

*   Todos os arquivos (compilados) de um aplicativo
*   Metadados sobre o aplicativo como nome, versão, dependências...
*   Arquivos de instalação e diretrizes para o [pacman](/index.php/Pacman "Pacman")
*   (Opcionalmente) arquivos extras para facilitar sua vida, como um script de start/stop

O [pacman](/index.php/Pacman "Pacman"), gerenciador de pacotes do arch, pode instalar, atualizar e remover esses pacotes. Usar um gerenciador de pacotes em vez de compilar e instalar programas manualmente tem vários benefícios:

*   Fácil atualização: pacman irá atualizar os pacotes existentes, logo que as atualizações estejam disponíveis
*   Checagem de dependências: pacman lida com dependências para você, você só precisa especificar o programa e pacman instala-o junto com todos os outros programas necessários
*   Remoção limpa: pacman tem uma lista de todos os arquivos em um pacote. Desta forma, nenhum arquivo será deixado para trás quando você decidir remover um pacote.

**Note:** Distribuições GNU/Linux podem usar diferentes pacotes com seus respectivos gerenciadores, significa dizer que você não pode usar o pacman para instalar um pacote Debian no Arch.

## Package maintainer

The role of the package maintainer is to update packages as new versions become available upstream and to field support questions relating to bugs in said packages. The term may be applied to any of the following:

A core Arch Linux developer who maintains a software package in one of the official repositories (core, extra, or testing).

A [Trusted User](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") of the community who maintains software packages in the unsupported/unofficial community repository.

A normal user who maintains a [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and local source files in the [AUR](/index.php/AUR "AUR").

The maintainer of a package is the person currently responsible for the package. Previous maintainers should be listed as contributors in the PKGBUILD along with others who have contributed to the package.

## pacman

The [pacman](/index.php/Pacman "Pacman") package manager is one of the great highlights of Arch Linux. It combines a simple binary package format with an easy-to-use build system (see [ABS](/index.php/Arch_Build_System "Arch Build System")). Pacman makes it possible to easily manage and customize packages, whether they be from the official Arch repositories or the user's own creations. The repository system allows users to build and maintain their own custom package repositories, which encourages community growth and contribution (see [AUR](/index.php/Arch_User_Repository "Arch User Repository")).

Pacman can keep a system up to date by synchronizing package lists with the master server, making it a breeze for the security-conscious system administrator to maintain. This server/client model also allows you to download/install packages with a simple command, complete with all required dependencies (similar to Debian's apt-get).

NB: Pacman was written by Judd Vinet, the creator of Arch Linux. It is used as a package management tool by other distributions as well, such as FrugalWare, Rubix, UfficioZero (in Italian, based on Ubuntu), and, of course, [Arch based distributions](/index.php/Arch_based_distributions_(active) "Arch based distributions (active)") such as Archie and AEGIS.

## pacman.conf

This is the configuration file of [pacman](/index.php/Pacman "Pacman"). It is located in `/etc`. For a full explanation of its powers, type this at the command line:

```
man pacman.conf

```

## repository/repo

The repository has the pre-compiled packages of one or (usually) more [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD"). Official repositories are

*   [core]: containing the latest version of packages required for a full CLI system
*   [extra]: containing the latest version of packages not needed for a working system but are needed for an enjoyable system ;)
*   [community]: containing packages that came from [AUR](/index.php/Arch_User_Repository "Arch User Repository") and got enough user votes

Pacman uses these repositories to search for packages and install them. A repository can be local (i.e. on your own computer) or remote (i.e. the packages are downloaded before they are installed).

## [RTFM](https://en.wikipedia.org/wiki/RTFM "wikipedia:RTFM")

"Read The Fucking (or Fine) Manual". This simple message is replied to a lot of new Linux/Arch users who ask about the functionality of a program when it is clearly defined in the program's manual.

It is often used when a user fails to make any attempt to find a solution to the problem themselves. If someone tells you this, they are not trying to offend you; they are just frustrated with your lack of effort.

The best thing to do if you are told to do this is to read the manual page.

*   To read the program manual page for a particular program, type this at the command line:

```
man PROGRAM-NAME

```

where PROGRAM-NAME is the name of the program you need more information about.

If you do not find the answer to your question in the program manual, there are more ways to find the answer. You can:

*   search the [wiki](/index.php/Special:Search "Special:Search")
*   search the [forum](https://bbs.archlinux.org)
*   search the [mailing lists](https://www.google.com/#hl=en&q=arch+site:archlinux.org%2Fpipermail%2F)
*   search the [web](https://www.google.com)

## taurball

The tarballed [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") and local source files that are required by makepkg to create an installable binary package. The name is derived from the practice of uploading such tarballs to the [AUR](/index.php/Arch_User_Repository "Arch User Repository"), hence "tAURball".

## testing/[testing]

This is the repository where major packages/updates to packages are kept prior to release into the main repositories, so they can be bug tested and upgrade issues can be found. It is disabled by default but can be enabled in `/etc/pacman.conf`

## udev

[udev](/index.php/Udev "Udev") provides a dynamic device directory containing only the files for actually present devices. It creates or removes device node files in the `/dev` directory, or it renames network interfaces.

Usually udev runs as udevd(8) and receives uevents directly from the kernel if a device is added/removed to/from the system.

If udev receives a device event, it matches its configured rules against the available device attributes provided in sysfs to identify the device. Rules that match may provide additional device information or specify a device node name and multiple symlink names and instruct udev to run additional programs as part of the device event handling.

## [wiki](https://en.wikipedia.org/wiki/Wiki "wikipedia:Wiki")

[This!](/index.php/Main_page "Main page") A place to find documentation about Arch Linux. Anyone can add and modify the documentation.