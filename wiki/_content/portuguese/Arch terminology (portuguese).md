**Status de tradução:** Esse artigo é uma tradução de [Arch terminology](/index.php/Arch_terminology "Arch terminology"). Data da última tradução: 2019-06-23\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Arch_terminology&diff=0&oldid=573999) na versão em inglês.

A intenção desta página é desmistificar os termos comumente usados pela comunidade do Arch Linux. Sinta-se à vontade para adicionar ou modificar quaisquer termos, mas por favor use a opção de editar da opção específica. Se você decidir adicionar algum termo, por favor adicione-o em ordem alfabética.

**Nota:** Ao traduzir este artigo, foram mantidos em inglês (original) os termos apresentados nos títulos das seções, para facilitar quem encontrou esses termos em algum tipo de conversa ou tópico de fórum em inglês e busca saber do que se trata. Porém, a tradução de cada termo é apresentada dentro da respectiva seção.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 ABS](#ABS)
*   [2 Arch Linux](#Arch_Linux)
*   [3 Arch Linux Archive](#Arch_Linux_Archive)
*   [4 AUR](#AUR)
*   [5 bbs](#bbs)
*   [6 community/[community]](#community/[community])
*   [7 core/[core]](#core/[core])
*   [8 custom/user repository](#custom/user_repository)
*   [9 Developer](#Developer)
*   [10 extra/[extra]](#extra/[extra])
*   [11 initramfs](#initramfs)
*   [12 initrd](#initrd)
*   [13 KISS](#KISS)
*   [14 makepkg](#makepkg)
*   [15 namcap](#namcap)
*   [16 package](#package)
*   [17 Package maintainer](#Package_maintainer)
*   [18 pacman](#pacman)
*   [19 PKGBUILD](#PKGBUILD)
*   [20 repository/repo](#repository/repo)
*   [21 RTFM](#RTFM)
*   [22 testing/[testing]](#testing/[testing])
*   [23 The Arch Way](#The_Arch_Way)
*   [24 TU, Trusted User](#TU,_Trusted_User)
*   [25 udev](#udev)
*   [26 wiki](#wiki)

## ABS

ABS é o acrônimo de [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)") ("Sistema de Compilação do Arch") e pode ser usado para:

*   Fazer novos pacotes para software que tem nenhum pacote disponível ainda
*   Personalizar/modificar pacotes existentes para ajustar suas necessidades:
    *   habilitar/desabilitar opções em tempo de compilação
    *   Aplicar alterações no código-fonte via patches
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

O [Arch Linux Archive](/index.php/Arch_Linux_Archive_(Portugu%C3%AAs) "Arch Linux Archive (Português)") (abreviado ALA), anteriormente conhecido Arch Linux Rollback Machine (a.k.a ARM), armazena *snapshots* de repositórios oficiais, imagens ISO e tarballs de *bootstrap* ao longo do tempo.

## AUR

O [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)") (AUR) é um repositório dirigido por uma comunidade de usuários do Arch. Ele contém descrições de pacotes ([PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)")) que permitem que você compile um pacote da fonte com o [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") e, então, instale-o via [pacman](/index.php/Pacman_(Portugu%C3%AAs)#Comandos_adicionais "Pacman (Português)"). O AUR foi criado e organizado para compartilhar novos pacotes da comunidade ajudando a acelerar a inclusão de pacotes populares para o [repositório community](/index.php?title=Reposit%C3%B3rio_community_(Portugu%C3%AAs)&action=edit&redlink=1 "Repositório community (Português) (page does not exist)").

Um bom número de novos pacotes que entram nos repositórios oficiais iniciam no AUR. No AUR, usuários são capazes de contribuir suas próprias compilações de pacote (PKGBUILD e arquivos relacionados). A comunidade do AUR possui a habilidade de votar a favor ou contra pacotes no AUR. Se um pacote se torna popular o suficiente — desde que tenha uma licença compatível e uma boa técnica de empacotamento — ele pode ser inserido no repositório *community* (diretamente acessível por [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") ou [abs](/index.php/Abs_(Portugu%C3%AAs) "Abs (Português)")).

Você pode acessar o repositório da comunidade de usuários do Arch Linux [aqui](https://aur.archlinux.org).

## bbs

*bbs* é o acrônimo para "Bulletin Board System"; no caso do Arch, é somente o fórum para suporte localizado [aqui](https://bbs.archlinux.org).

## community/[community]

O repositório *community* é onde pacotes pré-compilados são disponibilizados pelos [Trusted Users](/index.php/Trusted_Users_(Portugu%C3%AAs) "Trusted Users (Português)"). A maioria dos pacotes no *community* vem do [AUR](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)").

## core/[core]

O repositório *core* contém os pacotes básicos para um sistema do Arch Linux. O *core* tem tudo que é necessário ter um sistema funcional de linha de comando.

## custom/user repository

Trata-se de repositório personalizado, de usuário. Qualquer um pode criar um e disponibilizá-lo para outros usuários. Para criar um repositório, você precisa de um conjunto de pacotes e um arquivo de banco de dados compatível com o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") para seus pacotes. Hospede seus arquivos online e todo mundo poderá usar seu repositório adicionando-o como um repositório comum.

Veja [Repositório local personalizado](/index.php/Reposit%C3%B3rio_local_personalizado "Repositório local personalizado").

## Developer

Desenvolvedores são semideuses trabalhando para melhorar o Arch sem qualquer ganho financeiro. [Desenvolvedores](https://www.archlinux.org/people/developers/) são deixados para trás somente por seus deuses, Judd Vinet e Aaron Griffin, que, por sua vez, só é superado por tacos.

## extra/[extra]

Coleção oficial de pacotes do Arch é razoavelmente simples, mas suplementamos isso com um maior e mais completo do repositório *extra* que contém muitas das coisas que nunca entrou na coleção de pacotes centrais. Este repositório está constantemente aumentando com a ajuda de pacotes enviados da comunidade forte. É aqui onde os ambientes de trabalho, gerenciadores de janela e programas comuns são encontrados.

## initramfs

Veja [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio").

## initrd

Obsoleto. Hoje em dia é frequentemente usado como um sinônimo de initramfs.

## KISS

Acrônimo para *Keep It Simple, Stupid*, que em português seria algo como "mantenha isto simples, estúpido". [Simplicidade](/index.php/Arch_Linux_(Portugu%C3%AAs)#Simplicidade "Arch Linux (Português)") é um princípio central que o Arch Linux tenta atingir.

## makepkg

[makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") vai construir pacotes para você. O makepkg vai ler metadados necessários de um arquivo [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"). Tudo que ele precisa é uma plataforma Linux capaz de compilação, [curl](https://www.archlinux.org/packages/?name=curl) e alguns scripts de compilação. A vantagem a de compilar baseado em script é que você realmente faz o trabalho uma vez. Assim que você tiver o script de compilação para um pacote, tudo o que você precisará é executar makepkg e ele vai fazer o resto: baixa e balida os arquivos fontes, verifica as dependências, configura as configurações de tempo de compilação, compilação do pacote, instala o pacote em uma raiz temporária, faz personalizações, cria informações-meta e empacota toda a coisa para o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") usar.

## namcap

[namcap](/index.php/Namcap_(Portugu%C3%AAs) "Namcap (Português)") é um utilitário de análise de pacotes que procura por problemas com pacotes do Arch Linux ou em seus arquivos [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"). Ele pode aplicar regras à lista de arquivos, no próprios arquivos ou em arquivos PKGBUILD individuais.

As regras retornam listas de mensagens. Cada mensagem pode ser uma dos três tipos: erro, aviso ou informação (pense nelas como notas ou comentários). Erros (referidos por "E:" são coisas que o namcap tem muita certeza de que estão erradas e precisam ser corrigidas. Avisos (referidos por "W:") são coisas que o namcap pensa que deveriam ser alteradas, mas se você sabe o que você está fazendo, então você pode ignorá-las. Informações (referidas por "I:") são apenas mostradas quando você usar o argumento de informação. Mensagens informacionais dão informações que podem ser úteis, mas é nada que tenha que ser alterado.

## package

Pacote é um conjunto de arquivos que contém:

*   todos os arquivos (compilados) de um aplicativo
*   metadados sobre o aplicativo como nome, versão, dependências...
*   arquivos e diretrizes de instalação para o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")
*   (opcionalmente) arquivos extras para facilitar sua vida, como um script de start/stop

O [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), gerenciador de pacotes do arch, pode instalar, atualizar e remover esses pacotes. Usar um gerenciador de pacotes em vez de compilar e instalar programas manualmente tem vários benefícios:

*   fácil atualização: pacman vai atualizar os pacotes existentes, assim que as atualizações estiverem disponíveis
*   verificações de dependência: pacman lida com dependências para você, você só precisa especificar o programa e pacman instala-o junto com todos os outros programas necessários
*   remoção limpa: pacman tem uma lista de todos os arquivos em um pacote. Desta forma, nenhum arquivo será deixado para trás quando você decidir remover um pacote.

**Nota:** Distribuições GNU/Linux podem usar diferentes pacotes com seus respectivos gerenciadores, significa dizer que você não pode usar o pacman para instalar um pacote Debian no Arch.

## Package maintainer

Veja [Mantenedor de pacotes](/index.php/Mantenedor_de_pacotes "Mantenedor de pacotes").

## pacman

O [gerenciador de pacotes](https://en.wikipedia.org/wiki/pt:sistema_gestor_de_pacotes é um das características mais distintas do Arch Linux. Ele combina um formato de pacote binário simples com um [sistema de compilação](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)") fácil de usar. O objetivo do *pacman* é possibilitar gerenciar pacotes facilmente, sejam eles dos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") ou de compilações do próprio usuário.

*pacman* mantém o sistema atualizado sincronizando listas de pacotes com o servidor mestre. Esse modelo servidor/cliente também permite que o usuário baixe/instale pacotes com um comando simples e completo com todas as dependências necessários.

Note: Pacman foi escrito por Judd Vinet, o criador do Arch Linux. Ele é usado como uma ferramenta de gerenciamento de pacote por outras distribuições também, tal como FrugalWare, Rubix, UfficioZero (na Itália, baseado no Ubuntu) e, é claro, [distribuições baseadas no Arch](/index.php/Distribui%C3%A7%C3%B5es_baseadas_no_Arch "Distribuições baseadas no Arch"), tal como Archie e AEGIS.

## PKGBUILD

[PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") são pequenos scripts que são usados para compilar pacotes do Arch Linux. Veja [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes") para mais detalhes.

## repository/repo

Repositório contém pacotes pré-compilados de um ou (geralmente) mais [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"). [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") são divididos em diferentes partes para facilitar manutenção. O pacman usa esses repositórios para pesquisar por pacotes e instalá-los. Um repositório podem ser lcaol (i.e. em seu computador) ou remoto (i.e. os pacotes são baixados antes de serem instalados).

## [RTFM](https://en.wikipedia.org/wiki/pt:RTFM "wikipedia:pt:RTFM")

'"Read The Fine Manual"', que pode ser traduzido como "Leia este ótimo manual". Essa mensagem simples é respondida a muitos dos novos usuários Linux/Arch que perguntam sobre a funcionalidade de um programa quando ela está definida, de forma clara, no manual do programa.

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

Podendo ser traduzido como "A Forma do Arch" ou "O Jeito do Arch", é um termo extraoficial tradicionalmente usado para se referir aos mais importantes [princípios do Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs)#Princípios "Arch Linux (Português)").

## TU, Trusted User

Um *[trusted user](/index.php/Trusted_user_(Portugu%C3%AAs) "Trusted user (Português)")*, que pode ser traduzido como "usuário confiável", é alguém que mantém o AUR e o repositório [community]. Trusted Users podem mover um pacote para o repositório [community], se ele foi votado como particular. TUs são apontados pela votação da maioria dos TUs existentes.

Os Trusted Users seguem as [AUR Trusted User Guidelines (Português)](/index.php/AUR_Trusted_User_Guidelines_(Portugu%C3%AAs) "AUR Trusted User Guidelines (Português)") e [TU by-laws](https://aur.archlinux.org/trusted-user/TUbylaws.html).

## udev

[udev](/index.php/Udev "Udev") fornece um diretório dinâmico de dispositivos contendo apenas os arquivos para os dispositivos presentes no momento. Ele cria ou remove arquivos de nó de dispositivos no diretório `/dev` ou renomeia as interfaces de rede.

Geralmente o udev é executado como udevd(8) e recebe *uevents* diretamente do kernel se um dispositivo é adicionado/removido do sistema.

Se o udev recebe um evento de dispositivo, ele compara suas regras configuradas com os atributos do dispositivo disponível fornecidos no [sysfs](https://en.wikipedia.org/wiki/pt:sysfs "wikipedia:pt:sysfs") para identificar o dispositivo. Regras que corresponderem podem fornecer informações adicionais do dispositivo ou especificar um nome de nó de dispositivo e múltiplos nomes de *symlink* e instruir udev a executar programas adicionais como parte da manipulação de evento do dispositivo.

## [wiki](https://en.wikipedia.org/wiki/pt:Wiki "wikipedia:pt:Wiki")

[O próprio!](/index.php/P%C3%A1gina_principal "Página principal") Um lugar para encontrar documentação sobre o Arch Linux. Qualquer um pode adicionar e modificar a documentação.