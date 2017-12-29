Artigos relacionados

*   [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)")
*   [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)")
*   [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)")
*   [Mirrors](/index.php/Mirrors "Mirrors")
*   [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")
*   [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)")
*   [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories")

Um [repositório de software](https://en.wikipedia.org/wiki/pt:Reposit%C3%B3rio "wikipedia:pt:Repositório") é um local de armazenamento a partir do qual pacotes de software são obtidos para instalação.

**Repositórios oficiais** do Arch Linux contêm softwares essenciais e populares, prontamente acessíveis via [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"). Eles são mantidos por [mantenedores de pacote](/index.php/Arch_terminology_(Portugu%C3%AAs)#Package_maintainer "Arch terminology (Português)").

Pacotes nos repositórios oficiais são atualizados constantemente: quando um pacote é atualizado, sua versão antiga é removida do repositórios. Não há grandes lançamentos do Arch: cada pacote é atualizado na medida em que novas versões se tornam disponíveis a partir de fontes do *upstream*. Cada repositório está sempre coerente, isto é, os pacotes que ele hospeda sempre são versões reciprocamente compatíveis.

## Contents

*   [1 Repositórios](#Reposit.C3.B3rios)
    *   [1.1 core](#core)
    *   [1.2 extra](#extra)
    *   [1.3 community](#community)
    *   [1.4 multilib](#multilib)
    *   [1.5 testing](#testing)
        *   [1.5.1 community-testing](#community-testing)
        *   [1.5.2 multilib-testing](#multilib-testing)
        *   [1.5.3 gnome-unstable](#gnome-unstable)
        *   [1.5.4 kde-unstable](#kde-unstable)
        *   [1.5.5 Desabilitando repositórios de teste](#Desabilitando_reposit.C3.B3rios_de_teste)
*   [2 Revisão histórica](#Revis.C3.A3o_hist.C3.B3rica)

## Repositórios

### core

Esse repositório pode ser localizado em `.../core/os/` de seu [mirror](/index.php/Mirror "Mirror") favorito.

*core* contém pacotes para:

*   inicialização do Arch Linux
*   [conectar à Internet](/index.php/Network_configuration_(Portugu%C3%AAs) "Network configuration (Português)")
*   [compilação de pacotes](/index.php/Creating_packages_(Portugu%C3%AAs) "Creating packages (Português)")
*   gerenciamento e correção de [sistemas de arquivos](/index.php/File_systems "File systems") suportados
*   o processo de configuração do sistema (ex.: [openssh](https://www.archlinux.org/packages/?name=openssh))

assim como as dependências deles (não necessariamente [makedepends](/index.php/PKGBUILD_(Portugu%C3%AAs)#makedepends "PKGBUILD (Português)")).

*core* possui uma qualidade consideravelmente estrita de requisitos. Desenvolvedores/usuários precisam assinar (como uma confirmação) as atualizações de pacotes antes delas serem aceitas; Para pacotes com baixo uso, um motivo razoável é suficiente: informar pessoas sobre a atualização, requisitar assinaturas, manter no [#testing](#testing) por uma semana dependendo da severidade da alteração, falta de relatórios de erros relevantes, junto com o assinatura implícito do mantenedor do pacote.

**Nota:** Para criar um repositório local com pacotes do *core* (ou outros repositórios) sem uma conexão internet, veja [pacman/Dicas e truques#Instalando pacotes a partir de um CD/DVD ou pendrive](/index.php/Pacman/Dicas_e_truques#Instalando_pacotes_a_partir_de_um_CD.2FDVD_ou_pendrive "Pacman/Dicas e truques")

### extra

Esse repositório pode ser localizado em `.../extra/os/` de seu *mirror* favorito.

*extra* contém todos os pacotes que não foram para o *core*. Por exemplo: Xorg, gerenciadores de janela, navegadores web, reprodutores de mídia, ferramentas para trabalhar com linguagens como Python e Ruby, e muito mais.

### community

Esse repositório pode ser localizado em `.../comunidade/os/` de seu *mirror* favorito.

*community* contém pacotes que foram adotadores por [Trusted Users](/index.php/Trusted_Users_(Portugu%C3%AAs) "Trusted Users (Português)") do [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"). Alguns desses pacotes podem eventualmente serem movidos para os repositórios [core](#core) ou [extra](#extra) caso os desenvolvedores os considerem cruciais para a distribuição.

### multilib

Esse repositório pode ser localizado em `.../multilib/os/` de seu *mirror* favorito.

*multilib* contém softwares e bibliotecas 32 bits que podem ser usados para executar e compilar aplicativos 32 bits em instalações 64 bits (ex.: [wine](https://www.archlinux.org/packages/?name=wine), [steam](https://www.archlinux.org/packages/?name=steam), etc).

Para mais informações, veja [Multilib](/index.php/Multilib_(Portugu%C3%AAs) "Multilib (Português)").

### testing

**Atenção:** Cuidado ao ativar o repositório *testing*. Seu sistema pode não funcionar adequadamente ao realizar uma atualização. Apenas usuários experientes que sabem como lidar com falhas de sistema em potencial devem usá-lo.

Esse repositório pode ser localizado em `.../multilib/os/` de seu *mirror* favorito.

*testing* contém pacotes que são candidatos aos repositórios *core* ou *extra*.

Novos pacotes vão para o *testing* se:

*   Eles são destinados ao repositório *core*. Tudo no *core* deve passar pelo *testing*

*   Espera-se que eles quebrem alguma coisa ao atualizar e precisarem ser testados primeiro.

*testing* é o único repositório que pode ter colisões nos nomes com outros repositórios oficiais. Se ativo, ele tem de ser o primeiro repositório listado em seu arquivo `/etc/pacman.conf`.

**Nota:** *testing* não é para as versões de pacotes "mais novo do novo". Parte de seu propósito é segurar atualizações de pacotes que têm o potencial de quebrar o sistema, seja como parte da coleção de pacotes do *core*, seja como crítico de outras formas. Como tal, usuários do *testing* são incentivados a se inscreverem na [lista de discussão arch-dev-public](https://mailman.archlinux.org/mailman/listinfo/arch-dev-public), acompanhar o [fórum do repositório testing](https://bbs.archlinux.org/viewforum.php?id=49) e a [relatar todos os erros](/index.php/Reporting_bug_guidelines "Reporting bug guidelines").

**Atenção:** Se você habilitar *testing*, também deve habilitar *community-testing*. Se você habilitar qualquer outro repositório de teste listado nas subseções a seguir, você também deve habilitar ambos *testing* e *community-testing*.

#### community-testing

Esse repositório é similar ao repositório *testing*, mas para pacotes que são candidatos para o repositório *community*.

#### multilib-testing

Esse repositório é similar ao repositório *testing*, mas para pacotes que são candidatos ao repositório *multilib*.

#### gnome-unstable

Esse repositório contém a versão mais recente do ambiente gráfico do [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"), antes de ser movido para o repositório principal de teste *testing*.

Para habilitá-lo, adicione as seguintes linhas ao `/etc/pacman.conf`:

```
[gnome-unstable]
Include = /etc/pacman.d/mirrorlist

```

A entrada *gnome-unstable* deve estar primeiro na lista de repositórios (*i.e.*, acima da entrada *testing*).

Por favor, relate erros relacionados a empacotamento em nosso [rastreador de erro](https://bugs.archlinux.org/), enquanto o resto deve ser relatado para o *upstream* no [Bugzilla do GNOME](https://bugzilla.gnome.org/).

#### kde-unstable

Esse repositório contém o *beta* mais recente ou *Release Candidate* dos aplicativos e Plasma do [KDE](/index.php/KDE "KDE").

Para habilitá-lo, adicione as seguintes linhas ao `/etc/pacman.conf`:

```
[kde-unstable]
Include = /etc/pacman.d/mirrorlist

```

A entrada *kde-unstable* deve estar primeiro na lista de repositórios (*i.e.*, em cima da entrada *testing*).

Certifique-se de [fazer relatórios de erros](/index.php/Reporting_bug_guidelines "Reporting bug guidelines") se você descobrir algum problema.

#### Desabilitando repositórios de teste

Se você habilitou repositórios de teste, mas posteriormente decidir desabilitá-los, você deve:

1.  Remover (comentar) eles do `/etc/pacman.conf`
2.  Realizar um `# pacman -Syuu` para "retroceder" suas atualizações para esses repositórios.

O segundo item é opcional, mas tenha-o em mente que cas você tenha algum problema.

## Revisão histórica

A maioria das divisões de repositórios ocorreram por razões históricas. Originalmente, quando o Arch Linux tinha ainda muito poucos usuários, havia apenas um repositório conhecido como **official** (agora *core*). Na época, *official*, basicamente, continha os aplicativos favoritos do Judd Vinet. Estava desenhado de maneira a conter apenas um de cada "tipo" de programa -- um ambiente gráfico, um navegador, etc.

Naquela época, havia usuários que não gostavam da seleção do Judd. Então, já que o [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)") é tão fácil de usar, começaram a criar os seus próprios pacotes. Estes pacotes foram para um repositório chamado **unofficial** e eram mantidos por outros desenvolvedores, não o Judd. Eventualmente, os dois repositórios foram considerados pelos desenvolvedores igualmente com suporte, de forma que os nomes *official* e *unofficial* já não mais refletiam seu real propósito. Subsequentemente, estes foram renomeados para **current** e **extra**, por volta da versão 0.5.

Pouco depois do lançamento em 2007.08.1, *current* mudou para *core* para evitar confusões sobre o que ele realmente continha. Os repositórios estão agora mais ou menos iguais aos olhos da equipe e da comunidade, mas o *core* tem algumas diferenças. A distinção principal é que os pacotes usados para CDs de instalação e *snapshots* de lançamento são criados a partir do *core*, apenas. Este repositório ainda fornece um sistema Linux completo, mas pode não ser o sistema Linux que você deseja.

Por volta das versões 0.5 e 0.6, havia muitos pacotes que os desenvolvedores não queriam manter. [Jason Chu](https://www.archlinux.org/fellows/#jason) montou os "Trusted User Repositories" (que pode ser traduzido como "repositórios dos usuários confiados"), que eram repositórios não-oficiais que os usuários considerados confiados poderiam colocar pacotes que eles tinham criado. Havia um repositório **staging** no qual pacotes poderiam ser promovidos a repositórios oficiais por um dos desenvolvedores do Arch Linux, mas fora isso, os desenvolvedores e os usuários confiados eram mais ou menos diferentes.

Isso funcionou por algum tempo, mas não quando os tais usuários confiados estavam entediados com seus repositórios e quando usuários não-confiados queriam compartilhar seus próprios pacotes. Isso levou ao desenvolvimento do [AUR](https://aur.archlinux.org/). Os TUs foram conglomerados em um grupo bastante restrito denominado Trusted Users e hoje eles mantêm o repositório **community**. Os TUs ainda são um grupo separado dos desenvolvedores do Arch Linux e há muita comunicação entre eles. Porém, pacotes populares ainda são por vezes promovidos do *community* para *extra*. O [AUR](https://aur.archlinux.org/) também permite que os demais usuários (não-TUs)enviem seus PKGBUILDs.

Após um kernel no *core* [quebrar o sistema de muitos usuários](https://www.archlinux.org/news/please-avoid-kernel-261614-1/), a *"core signoff policy"* ("política de assinatura do core") foi introduzida. Desde então, todas as atualizações de pacotes para o *core* precisam passar pelo repositório *testing* primeiro e apenas após múltiplas assinaturas de outros desenvolvedores que, então, são permitidos mover. Ao longo do tempo, foi notado que vários pacotes do *core* tinham pouco uso, e signoffs de usuários ou até mesmo falta de relatórios de erros se tornaram informalmente aceitos como critério para aceitar tais pacotes.

No final de 2009 e o início de 2010, com o advento de novos sistemas de arquivos, o desejo de oferecer suporte durante a instalação e com a percepção de que o *core* nunca foi claramente definido (apenas "pacotes importantes, escolhido a mão pelos desenvolvedores"), o repositório recebeu uma descrição mais precisa.