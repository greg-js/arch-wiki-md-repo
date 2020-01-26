**Status de tradução:** Esse artigo é uma tradução de [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). Data da última tradução: 2020-01-25\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Arch_Build_System&diff=0&oldid=596073) na versão em inglês.

Artigos relacionados

*   [Padrões de empacotamento do Arch](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")
*   [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)")
*   [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes")
*   [Compilação de kernel com ABS](/index.php/Kernel_Compilation_with_ABS "Kernel Compilation with ABS")
*   [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)")
*   [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais")
*   [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")
*   [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)")
*   [Aplicação de patch no ABS](/index.php/Aplica%C3%A7%C3%A3o_de_patch_no_ABS "Aplicação de patch no ABS")

O sistema de compilação do Arch *(Arch build system)* é um sistema *tipo portação* para compilar e empacotar software a partir do código-fonte. Enquanto o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") é a ferramenta especializada do Arch para gerenciamento de pacote binário (incluindo pacotes compilados com o ABS), ABS é uma coleção de ferramentas para compilar o fonte em pacotes `.pkg.tar.xz` instaláveis.

*Ports* é um sistema usado por *BSD para automatizar o processo de compilação de software a partir do código-fonte. O sistema usa um *port* para baixar, descompactar, patch, compilar e instalar o software dado. Um *port* é meramente um pequeno diretório no computador do usuário, nomeado pelo software correspondente para ser instalado, que contém uns poucos arquivos com as instruções para compilar e instalar o software a partir dos fontes. Isso torna a instalação de softwares tão simples quanto digitar `make` ou `make install clean` dentro de diretório de portação.

ABS é um conceito similar. Uma parte do ABS é um repositório SVN e um repositório Git equivalente. O repositório contém um diretório correspondente a cada pacote disponível no Arch Linux. Os diretórios do repositório contêm um arquivo [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") (e às vezes outros arquivos) e não contêm a fonte do software nem o binário. Ao emitir [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") dentro de um diretório, as fontes do software são baixadas, o software é compilado e empacotado no diretório de compilação. Então, você pode usar [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") para instalar o pacote.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Visão geral](#Visão_geral)
    *   [1.1 Árvore de repositório](#Árvore_de_repositório)
*   [2 Casos de uso](#Casos_de_uso)
*   [3 Uso](#Uso)
    *   [3.1 Obtendo fonte de PKGBUILD](#Obtendo_fonte_de_PKGBUILD)
        *   [3.1.1 Obtebdo fonte de PKGBUILD usando SVN](#Obtebdo_fonte_de_PKGBUILD_usando_SVN)
            *   [3.1.1.1 Pré-requisitos](#Pré-requisitos)
            *   [3.1.1.2 Checkout não-recursivo](#Checkout_não-recursivo)
            *   [3.1.1.3 Fazer checkout de um pacote](#Fazer_checkout_de_um_pacote)
        *   [3.1.2 Obtendo fonte de PKGBUILD usando Git](#Obtendo_fonte_de_PKGBUILD_usando_Git)
    *   [3.2 Compilar pacote](#Compilar_pacote)
*   [4 Dicas e truques](#Dicas_e_truques)
    *   [4.1 Preserve pacotes modificados](#Preserve_pacotes_modificados)
    *   [4.2 Faça checkout de uma versão anterior de um pacote](#Faça_checkout_de_uma_versão_anterior_de_um_pacote)
*   [5 Outras ferramentas](#Outras_ferramentas)

## Visão geral

"ABS" pode ser usado como um termo guarda-chuva já que ele inclui e depende de vários outros componentes; portanto, apesar de tecnicamente impreciso, "ABS" pode ser referir às seguintes ferramentas como um kit de ferramentas completos:

	Árvore do repositório

	A estrutura de diretório contendo arquivos necessários para compilar todos os pacotes oficiais, mas não os pacotes em si nem os arquivos fontes do software. Ela está disponível nos repositórios [svn](https://www.archlinux.org/svn/) e [git](https://projects.archlinux.org/svntogit/packages.git/).

Consulte a seção [#Árvore de repositório](#Árvore_de_repositório) para mais informações.

	[PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)")

	Um script [Bash](/index.php/Bash "Bash") que contém a URL do código-fonte junto com as instruções de compilação e empacotamento.

	[makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)")

	Ferramenta de comando shell que lê os PKGBUILDs, baixa automaticamente e compila os fontes e cria um `.pkg.tar*` de acordo com o vetor `PKGEXT` no `makepkg.conf`. Você também pode usar makepkg para fazer seus próprios pacotes personalizados do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") ou fontes de terceiros. Veja [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes") para mais informações.

	[pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")

	pacman é completamente separado, mas é necessariamente invocado pelo makepkg ou manualmente, para instalar e remover os pacotes compilados e para obter dependências.

	[AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)")

	O Arch User Repository é separado do ABS, mas PKGBUILDs do AUR (sem suporte) são compilados usando makepkg para compilar e empacotar software. Em contraste com a árvore do ABS em sua máquina local, o AUR existe como uma interface do website. Ele contém muitos milhares de PKGBUILDs contribuídos por usuários para software que está indisponível como um pacote oficial do Arch. Se você precisar compilar um pacote fora da árvore oficial do Arch, as chances são de que esteja no AUR.

**Atenção:** PKGBUILDs oficiais presumem que pacotes são [compilados em um *chroot* limpo](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot"). Compilação de software em um sistema de compilação *sujo* pode falhar ou causar comportamentos inesperados em tempo de execução, porque se o sistema de compilação detecta dependências dinamicamente, o resultado depende de quais pacotes estão disponíveis no sistema de compilação.

### Árvore de repositório

Os [repositórios](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") *core*, *extra* e *testing* estão no repositório *packages* para *[checkout](#Checkout_não-recursivo)*. Os repositórios *community* e *multilib* estão no repositório *community*.

Cada pacote possui seu próprio subdiretório. Dentro dele há diretórios `repos` e `trunk`. `repos` é expandido por nome de repositório (ex.: *core*) e arquitetura. PKGBUILDs e arquivos localizados em `repos` são usados em compilações oficiais. Arquivos localizados no `trunk` são usados pelos desenvolvedores na preparação antes de serem copiados para `repos`.

Por exemplo, a árvore para [acl](https://www.archlinux.org/packages/?name=acl) se parece com isso:

```
acl
acl/repos
acl/repos/core-i686
acl/repos/core-i686/PKGBUILD
acl/repos/core-x86_64
acl/repos/core-x86_64/PKGBUILD
acl/trunk
acl/trunk/PKGBUILD

```

O código-fonte do pacote não está presente no diretório ABS. Em vez disso, o `PKGBUILD` contém uma URL que vai baixar o código-fonte quando o pacote é compilado.

## Casos de uso

Casos de uso do ABS são:

*   Em qualquer caso que você queria compilar ou recompilar um pacote
*   *Make* e instalar novos pacotes de fontes de software para os quais nenhum pacote está instalado ainda (veja [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes"))
*   Personalizar pacotes existentes para atender suas necessidades (por exemplo, habilitar ou desabilitar opções, *patching*)
*   Recompilar todo o seu sistema usando suas *flags* de compilador, "à la FreeBSD" (ex.: com [pacman-src-git](https://aur.archlinux.org/packages/pacman-src-git/)))
*   Compilar e instalar, sem interferências, seu próprio kernel personalizado (veja [Compilação de kernel](/index.php/Kernels_(Portugu%C3%AAs)#Compilação "Kernels (Português)"))
*   Fazer com que módulos de kernel funcionem com um kernel personalizado
*   Compilar e instalar facilmente uma versão mais nova, antiga, beta ou de desenvolvimento de um pacote do Arch editando o número de versão no PKGBUILD

O ABS automatiza determinadas tarefas relacionadas à compilação a partir do código-fonte. Como alternativa ao uso do ABS, você pode executar essas tarefas manualmente.

## Uso

Para obter o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") necessário para compilar um certo pacote a partir do fonte, você pode usar uma abordagem baseada em [SVN](/index.php/SVN "SVN") ou [Git](/index.php/Git "Git") usando o pacote [asp](https://www.archlinux.org/packages/?name=asp) que é uma interface para os repositórios svntogit. A seguir, o método baseado em svn, bem como o [método baseado em git](#Obtendo_fonte_de_PKGBUILD_usando_Git), são descritos.

### Obtendo fonte de PKGBUILD

#### Obtebdo fonte de PKGBUILD usando SVN

##### Pré-requisitos

[Instale](/index.php/Instale "Instale") o pacote [subversion](https://www.archlinux.org/packages/?name=subversion).

##### Checkout não-recursivo

**Atenção:** Não baixe todo o repositório; siga apenas as instruções abaixo. O repositório SVN todo é gigantesco. Não apenas vai gastar uma quantidade absurda de espaço em disco, mas também vai ocupar o servidor do archlinux.org para você baixá-lo. Se você abusar desse serviço, seu endereço pode ser bloqueado. Nunca use o SVN público para qualquer tipo de *scripting*.

Para fazer *checkout* dos [repositórios](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") *core*, *extra* e *testing*:

```
$ svn checkout --depth=empty svn://svn.archlinux.org/packages

```

Para fazer *checkout* dos repositórios *community* e *multilib*

```
$ svn checkout --depth=empty svn://svn.archlinux.org/community

```

Em ambos casos, ele cria um diretório vazio, mas ele sabe que é um *checkout* de svn.

##### Fazer checkout de um pacote

No diretório contendo o repositório svn que você fez checkout (isto é, *packages* ou *community*), faça:

```
$ svn update *nome-pacote*

```

Isso vai obter o pacote que você requisitou em seu checkout. Daqui para frente, toda vez que você executar *svn update* no nível superior, esse também será atualizado.

Se você especifica um pacote que não existe, svn não vai avisar você. Ele só vai mostrar algo como "At revision 115847", sem criar quaisquer arquivos. Se isso acontecer:

*   verifique se o nome do pacote está escrito corretamente
*   verifique se o pacote não foi movido para outro repositório (ex. do repositório *community* para o repositório principal)
*   acesse [https://www.archlinux.org/packages](https://www.archlinux.org/packages) para ver se o pacote é compilado a partir de outro pacote base (por exemplo, [python-tensorflow](https://www.archlinux.org/packages/?name=python-tensorflow) é compilado no PKGBUILD do [tensorflow](https://www.archlinux.org/packages/?name=tensorflow))

**Dica:** Para fazer *checkout* uma versão mais antiga de um pacote, veja [#Faça checkout de uma versão anterior de um pacote](#Faça_checkout_de_uma_versão_anterior_de_um_pacote).

Você deve atualizar periodicamente todos os pacotes baixados se você deseja realizar recompilações em revisões mais recentes dos repositórios. Para fazer isso, execute:

```
$ svn update

```

#### Obtendo fonte de PKGBUILD usando Git

Como pré-condição, [instale](/index.php/Instale "Instale") o pacote [asp](https://www.archlinux.org/packages/?name=asp). [Asp](https://github.com/falconindy/asp) é uma ferramenta para gerenciar os arquivos-fontes de compilação usados para criar pacotes do Arch Linux. Usa a interface git, que oferece fontes mais atualizadas. Consulte também o tópico do fórum do Arch Linux BBS [[1]](https://bbs.archlinux.org/viewtopic.php?id=185075).

Para clonar o repositório svntogit para um pacote específico, use:

```
$ asp checkout *nome-pacote*

```

Isso vai clonar o repositório git para o pacote dado em um diretório com o nome do pacote.

Para atualizar o repositório git clonado, execute `asp update` seguido por `git pull` dentro do repositório git.

Em seguida, você pode usar todos os comandos git para realizar o *checkout* de uma versão antiga do pacote ou rastrear alterações personalizadas. Para mais informações sobre o uso de git, veja a página [git](/index.php/Git "Git").

Se você só deseja copiar um snapshot do [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para um pacote específico, use:

```
$ asp export *nome-pacote*

```

### Compilar pacote

Configure o *makepkg* para compilar pacotes dos [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") que você fez *checkout*, como dado em [makepkg (Português)#Configuração](/index.php/Makepkg_(Portugu%C3%AAs)#Configuração "Makepkg (Português)").

Em seguida, copie o diretório contendo o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") que você deseja modificar para uma nova localização.

Então, faça as modificações desejadas e use *makepkg*, como descrito em [makepkg (Português)#Uso](/index.php/Makepkg_(Portugu%C3%AAs)#Uso "Makepkg (Português)"), para criar e instalar o novo pacote.

## Dicas e truques

### Preserve pacotes modificados

Atualizar o sistema com o pacman vai substituir um pacote modificado pelo ABS com o pacote de menos nome dos repositórios oficiais. Veja as instruções a seguir para como evitar isso.

Insira um vetor de grupo no PKGBUILD, e adicione o pacote para um grupo chamado `modified`.

 `PKGBUILD`  `groups=('modified')` 

Adicione esse grupo à seção `IgnoreGroup` no `/etc/pacman.conf`.

 `/etc/pacman.conf`  `IgnoreGroup = modified` 

Se novas versões estiverem disponíveis nos repositórios oficiais durante uma atualização de sistema, pacman emite uma nota de que ele está ignorando essa atualização porque ele está na seção IgnoreGroup. Neste ponto, o pacote modificado deve ser recompilado a partir do ABS para evitar atualizações parciais.

### Faça checkout de uma versão anterior de um pacote

Dentro do repositório svn que você faz checkout como descrito em [#Checkout não-recursivo](#Checkout_não-recursivo) (isto é, "packages" ou "community"), primeiro examine o log:

```
$ svn log *nome-pacote*

```

Descrita a revisão que você deseja examinando o histórico e especifique a revisão que você deseja fazer *checkout*. Por exemplo, para fazer *checkout* da revisão `r1729`, você faria:

```
$ svn update -r1729 *nome-pacote*

```

Isso vai atualizar uma cópia de trabalho existente de *nome-pacote* para a revisão escolhida.

Você também pode especificar uma data. Se nenhuma revisão naquele dia existir, svn vai pegar o pacote mais recente antes daquele tempo. O seguinte exemplo faz checkout da revisão de 2009-03-03:

```
 $ svn update -r'{20090303}' *nome-pacote*

```

Também é possível fazer *checkout* de pacotes nas versões antes de eles terem sido movidos para um outro repositório; veja os logs pela data que eles foram movidos ou o número da última revisão.

## Outras ferramentas

*   [pbget](http://xyne.archlinux.ca/projects/pbget/) - obtém PKGBUILDs de pacotes individuais diretamente da interface web. Inclui suporte ao AUR.