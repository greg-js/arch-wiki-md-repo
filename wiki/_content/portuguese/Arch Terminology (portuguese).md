A intenção desta página é desmistificar os termos comumente usados pela comunidade do Arch Linux. Sinta-se à vontade para adicionar ou modificar quaisquer termos, mas por favor use a opção de editar da opção específica. Se você decidir adicionar algum termo, por favor adicione-o em ordem alfabética.

## Contents

*   [1 ABS](#ABS)
*   [2 Arch Linux](#Arch_Linux)
*   [3 Arch Linux Archive](#Arch_Linux_Archive)
*   [4 AUR](#AUR)
*   [5 bbs](#bbs)
*   [6 community/[community]](#community.2F.5Bcommunity.5D)
*   [7 core/[core]](#core.2F.5Bcore.5D)
*   [8 custom/user repository](#custom.2Fuser_repository)
*   [9 Developer](#Developer)
*   [10 extra/[extra]](#extra.2F.5Bextra.5D)
*   [11 initramfs](#initramfs)
*   [12 initrd](#initrd)
*   [13 KISS](#KISS)
*   [14 makepkg](#makepkg)
*   [15 namcap](#namcap)
*   [16 package](#package)
*   [17 Package maintainer](#Package_maintainer)
*   [18 pacman](#pacman)
*   [19 pacman.conf](#pacman.conf)
*   [20 PKGBUILD](#PKGBUILD)
*   [21 repository/repo](#repository.2Frepo)
*   [22 RTFM](#RTFM)
*   [23 testing/[testing]](#testing.2F.5Btesting.5D)
*   [24 The Arch Way](#The_Arch_Way)
*   [25 TU, Trusted User](#TU.2C_Trusted_User)
*   [26 udev](#udev)
*   [27 wiki](#wiki)

## ABS

Acrônimo de [Arch Build System](/index.php/Arch_Build_System "Arch Build System"), que pode ser traduzido como "Sistema de Compilação do Arch", é útil para:

*   Fazer novos pacotes de software para os quais nenhum pacote está disponível
*   Personalizar/modificar pacotes existentes para ajustar suas necessidades (habilitando ou desabilitando opções)
*   Recompilar seu sistema completo usando as flags do seu compilador, "a la Gentoo"
*   Fazer com que módulos do kernel funcionem no seu kernel personalizado

ABS não é necessário para se usar o Arch Linux, mas é muito útil.

## Arch Linux

Arch deve ser referenciado como:

*   **Arch Linux**
*   **Arch** (Linux implícito)
*   **archlinux** (nome UNIX)

Archlinux, ArchLinux, archLinux, aRcHlInUx, etc. são todos estranhas mutações.

Oficialmente, o 'Arch' de "Arch Linux" é pronunciado /ˈɑrtʃ/ como em "archer"/arqueiro, ou "arch-nemesis" ("arqui-inimigo") e não como em "ark" ou "archangel" ("arcanjo").

## Arch Linux Archive

O [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive") (abreviado ALA), anteriormente conhecido Arch Linux Rollback Machine (a.k.a ARM), armazena *snapshots* de repositórios oficiais, imagens ISO e tarballs de *bootstrap* ao longo do tempo.

## AUR

O [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") (AUR) é um repositório dirigido por uma comunidade de usuários do Arch. Ele contém descrições de pacotes ([PKGBUILDs](/index.php/PKGBUILD "PKGBUILD")) que permite que você compile um pacote do fonte com [makepkg](/index.php/Makepkg "Makepkg") e, então, instale-o via [pacman](/index.php/Pacman#Additional_commands "Pacman"). O AUR foi criado para organizado para compartilhar novos pacotes da comunidade para ajudar e acelerar inclusão de pacotes populares para o repositório [community](/index.php/Community "Community"). Esse documento explica como usuários podem acessar e utilizar o AUR.

Um bom número de novos pacotes que entram nos repositórios oficiais iniciam no AUR. No AUR, usuários são capazes de contribuir suas próprias compilações de pacote (PKGBUILD e arquivos relacionados). A comunidade do AUR possui a habilidade de votar por ou contra pacotes no AUR. Se um pacote se torna popular o suficiente — desde que tenha uma licença compatível e uma boa técnica de empacotamento — ele pode ser inserido no repositório *community* (diretamente acessível por [pacman](/index.php/Pacman "Pacman") ou [abs](/index.php/Abs "Abs")).

Você pode acessar o repositório da comunidade de usuários do Arch Linux [aqui](https://aur.archlinux.org).

## bbs

*bbs* é o acrônimo para "Bulletin Board System"; no caso do Arch, é somente o fórum para suporte localizado [aqui](https://bbs.archlinux.org).

## community/[community]

O repositório *community* é onde pacotes pré-compilados são disponibilizados pelos [Trusted Users](/index.php/Trusted_Users "Trusted Users"). A maioria dos pacotes no *community* vem do [AUR](/index.php?title=Arch_Terminology_(Portugu%C3%AAs)/Arch_User_Repository_(Portugu%C3%AAs)&action=edit&redlink=1 "Arch Terminology (Português)/Arch User Repository (Português) (page does not exist)").

## core/[core]

O repositório *core* contém os pacotes básicos para um sistema do Arch Linux. O *core* tem tudo que é necessário ter um sistema funcional de linha de comando.

## custom/user repository

Trata-se de repositório personalizado, de usuário. Qualquer um pode criar um e disponibilizá-lo para outros usuários. Para criar um repositório, você precisa de um conjunto de pacotes e um arquivo de banco de dados compatível com o [pacman](/index.php/Pacman "Pacman") para seus pacotes. Hospede seus arquivos online e todo mundo poderá usar seu repositório adicionando-o como um repositório comum.

Veja [Repositório local personalizado](/index.php/Custom_local_repository "Custom local repository").

## Developer

Desenvolvedores são semideuses trabalhando para melhorar o Arch sem qualquer ganho financeiro. [Desenvolvedores](https://www.archlinux.org/developers/) são deixados para trás somente por seus deuses, Judd Vinet e Aaron Griffin, os quais por sua vez são deixados para trás por tacos.

## extra/[extra]

Coleção oficial de pacotes do Arch é razoavelmente simples, mas suplementamos isso com um maior e mais completo do repositório *extra* que contém muitas das coisas que nunca entrou na coleção de pacotes centrais. Este repositório está constantemente aumentando com a ajuda de pacotes enviados da comunidade forte. É aqui onde os ambientes de trabalho, gerenciadores de janela e programas comuns são encontrados.

## initramfs

Veja [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio").

## initrd

Obsoleto. Hoje em dia é frequentemente usado como um sinônimo de initramfs.

## KISS

Acrônimo para *Keep It Simple, Stupid*, que em português seria algo como "mantenha isto simples, estúpido". [Simplicidade](/index.php/Arch_Linux#Simplicity "Arch Linux") é um princípio central que o Arch Linux tenta atingir.

## makepkg

[makepkg](/index.php/Makepkg "Makepkg") vai construir pacotes para você. O makepkg vai ler metadados necessários de um arquivo [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). Tudo que ele precisa é uma plataforma Linux capaz de compilação, [wget](https://www.archlinux.org/packages/?name=wget) e alguns scripts de compilação. A vantagem a de compilar baseado em script é que você realmente faz o trabalho uma vez. Assim que você tiver o script de compilação para um pacote, tudo o que você precisará é executar makepkg e ele vai fazer o resto: baixa e balida os arquivos fontes, verifica as dependências, configura as configurações de tempo de compilação, compilação do pacote, instala o pacote em uma raiz temporária, faz personalizações, cria informações-meta e empacota toda a coisa para o [pacman](/index.php/Pacman "Pacman") usar.

## namcap

[namcap](/index.php/Namcap "Namcap") é um utilitário de análise de pacotes que procura por problemas com pacotes do Arch Linux ou em seus arquivos [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). Ele pode aplicar regras à lista de arquivos, no próprios arquivos ou em arquivos PKGBUILD individuais.

As regras retornam listas de mensagens. Cada mensagem pode ser uma dos três tipos: erro, aviso ou informação (pense nelas como notas ou comentários). Erros (referidos por "E:" são coisas que o namcap tem muita certeza de que estão erradas e precisam ser corrigidas. Avisos (referidos por "W:") são coisas que o namcap pensa que deveriam ser alteradas, mas se você sabe o que você está fazendo, então você pode ignorá-las. Informações (referidas por "I:") são apenas mostradas quando você usar o argumento de informação. Mensagens informacionais dão informações que podem ser úteis, mas é nada que tenha que ser alterado.

## package

Pacote é um conjunto de arquivos que contém:

*   todos os arquivos (compilados) de um aplicativo
*   metadados sobre o aplicativo como nome, versão, dependências...
*   arquivos e diretrizes de instalação para o [pacman](/index.php/Pacman "Pacman")
*   (opcionalmente) arquivos extras para facilitar sua vida, como um script de start/stop

O [pacman](/index.php/Pacman "Pacman"), gerenciador de pacotes do arch, pode instalar, atualizar e remover esses pacotes. Usar um gerenciador de pacotes em vez de compilar e instalar programas manualmente tem vários benefícios:

*   fácil atualização: pacman vai atualizar os pacotes existentes, assim que as atualizações estiverem disponíveis
*   verificações de dependência: pacman lida com dependências para você, você só precisa especificar o programa e pacman instala-o junto com todos os outros programas necessários
*   remoção limpa: pacman tem uma lista de todos os arquivos em um pacote. Desta forma, nenhum arquivo será deixado para trás quando você decidir remover um pacote.

**Note:** Distribuições GNU/Linux podem usar diferentes pacotes com seus respectivos gerenciadores, significa dizer que você não pode usar o pacman para instalar um pacote Debian no Arch.

## Package maintainer

Mantenedor de pacote é o papel responsável por atualizar pacotes na medida em que novas versões são disponibilizadas pelo *upstream*, além de fornecer suporte em relatórios de erros sobre eles. O termo pode se aplicar a qualquer um dos seguintes:

*   Um desenvolvedor do Arch Linux que mantém um pacote de software em um dos repositórios oficiais (*core*, *extra* ou *testing*).
*   Um [Trusted User](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") da comunidade que mantém pacotes de software no repositório de comunidade extraoficiais/sem suporte.
*   Um usuário normal que mantém um [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") e arquivos fontes locais no [AUR](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)").

O mantenedor de um pacote é a pessoa atualmente responsável pelo pacote. Mantenedores anteriores deve ser listado como contribuidores no PKGBUILD junto com outros que contribuíram para o pacote.

## pacman

O [gerenciador de pacotes](https://en.wikipedia.org/wiki/Package_manager "wikipedia:Package manager") [pacman](/index.php/Pacman "Pacman") é um das características mais distintas do Arch Linux. Ele combina um formato de pacote binário simples com um [sistema de compilação](/index.php/Arch_Build_System "Arch Build System") fácil de usar. O objetivo do *pacman* é possibilitar gerenciar pacotes facilmente, sejam eles dos [repositórios oficiais](/index.php/Official_repositories "Official repositories") ou de compilações do próprio usuário.

*pacman* mantém o sistema atualizado sincronizando listas de pacotes com o servidor mestre. Esse modelo servidor/cliente também permite que o usuário baixe/instale pacotes com um comando simples e completo com todas as dependências necessários.

Note: Pacman foi escrito por Judd Vinet, o criador do Arch Linux. Ele é usado como uma ferramenta de gerenciamento de pacote por outras distribuições também, tal como FrugalWare, Rubix, UfficioZero (na Itália, baseado no Ubuntu) e, é claro, [distribuições baseada no Arch](/index.php/Arch_based_distributions "Arch based distributions"), tal como Archie e AEGIS.

## pacman.conf

Esse é o arquivo de configuração do [pacman](/index.php/Pacman "Pacman"). Ele está localizado no `/etc`. Para uma explicação completa de seus poderes, digite isso na linha de comando: `man pacman.conf`.

## PKGBUILD

[PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") são pequenos scripts que são usados para compilar pacotes do Arch Linux. Veja [Criando pacotes](/index.php/Creating_packages "Creating packages") para mais detalhes.

## repository/repo

Repositório contém pacotes pré-compilados de um ou (geralmente) mais [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD"). [Repositórios oficiais](/index.php/Official_repositories "Official repositories") são divididos em diferentes partes para facilitar manutenção. O pacman usa esses repositórios para pesquisar por pacotes e instalá-los. Um repositório podem ser lcaol (i.e. em seu computador) ou remoto (i.e. os pacotes são baixados antes de serem instalados).

## [RTFM](https://en.wikipedia.org/wiki/RTFM "wikipedia:RTFM")

'"Read The Fucking (ou Fine) Manual"', que pode ser traduzido como "Leia a porra desse manual". Essa mensagem simples é respondida a muitos dos novos usuários Linux/Arch que perguntam sobre a funcionalidade de um programa quando ela está definida, de forma clara, no manual do programa.

É geralmente usada quando um usuário falha em, ele mesmo, fazer qualquer tentativa de encontrar uma solução para o problema. Se alguém lhe disser isso, não está tentando lhe ofender; está apenas frustrado com sua falta de esforço.

A melhor coisa a se fazer se lhe falarem isso é ler a página do manual.

*   Para ler a página de manual de um programa em particular chamado de NOME-PROGRAMA, digite isso na linha de comando: `man NOME-PROGRAMA`.

Se você não localizar a resposta para sua pergunta no manual do programa, há mais formas de encontrar a resposta. Você pode:

*   pesquisar no [wiki](/index.php/Special:Search "Special:Search")
*   pesquisar no [fórum](https://bbs.archlinux.org)
*   Pesquisar nas [listas de discussão](https://www.google.com/#hl=en&q=arch+site:archlinux.org%2Fpipermail%2F)
*   Pesquisar na [web](https://www.google.com)

## testing/[testing]

Esse é o respositório no qual a maioria dos pacotes ou das atualizações de pacotes são mantidas antes de serem lançadas para os repositórios principais, de forma que eles podem ser testados e atualizações de problemas podem ser descobertas. É desabilitado por padrão, mas pode ser habilitado no `/etc/pacman.conf`

## The Arch Way

Podendo ser traduzido como "A Forma do Arch", é um termo extraoficial tradicionalmente usado para se referir aos mais importantes [princípios do Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs)#Princ.C3.ADpios "Arch Linux (Português)").

## TU, Trusted User

Um *[trusted user](/index.php/Trusted_user "Trusted user")*, que pode ser traduzido como "usuário confiável", é alguém que mantém o AUR e o repositório [community]. Trusted Users podem mover um pacote para o repositório [community], se ele foi votado como particular. TUs são apontados pela votação da maioria dos TUs existentes.

Os Trusted Users seguem as [AUR Trusted User Guidelines (Português)](/index.php/AUR_Trusted_User_Guidelines_(Portugu%C3%AAs) "AUR Trusted User Guidelines (Português)") e [TU by-laws](https://aur.archlinux.org/trusted-user/TUbylaws.html).

## udev

[udev](/index.php/Udev "Udev") fornece um diretório dinâmico de dispositivos contendo apenas os arquivos para os dispositivos presentes no momento. Ele cria ou remove arquivos de nó de dispositivos no diretório `/dev` ou renomeia as interfaces de rede.

Geralmente o udev é executado como udevd(8) e recebe *uevents* diretamente do kernel se um dispositivo é adicionado/removido do sistema.

Se o udev recebe um evento de dispositivo, ele compara suas regras configuradas com os atributos do dispositivo disponível fornecidos no sysfs para identificar o dispositivo. Regras que corresponderem podem fornecer informações adicionais do dispositivo ou especificar um nome de nó de dispositivo e múltiplos nomes de *symlink* e instruir udev a executar programas adicionais como parte da manipulação de evento do dispositivo.

## [wiki](https://en.wikipedia.org/wiki/Wiki "wikipedia:Wiki")

[O próprio!](/index.php/Main_page "Main page") Um lugar para encontrar documentação sobre o Arch Linux. Qualquer um pode adicionar e modificar a documentação.