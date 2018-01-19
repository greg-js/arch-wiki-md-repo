**Atenção:** Auxiliadores do AUR não possuem suporte [oficial](https://bbs.archlinux.org/viewtopic.php?pid=828254#p828254) pelo Arch Linux. É recomendado se tornar familiar com o [processo manual de compilação](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#Instalando_pacotes "Arch User Repository (Português)") para estar preparado para diagnosticar e resolver problemas por conta própria.

Auxiliares do AUR são escritos para automatizar certas tarefas para o [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)").

## Contents

*   [1 Envio](#Envio)
*   [2 Compilar e pesquisa](#Compilar_e_pesquisa)
*   [3 Manutenção](#Manuten.C3.A7.C3.A3o)
*   [4 Bibliotecas](#Bibliotecas)
*   [5 Gráfico](#Gr.C3.A1fico)
*   [6 Tabela comparativa](#Tabela_comparativa)

## Envio

*   [aur4_import.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_import.sh) — Divide um pacote de um repositório git com múltiplos pacotes, adicionando/atualizando `.SRCINFO` para cada commit.
*   [aur4_make_submodule.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_make_submodule.sh) — Substitui um pacote em um repositório git maior com um submódulo do AUR 4, incluindo `.SRCINFO`.
*   [aurpublish](https://github.com/Edenhofer/abs/blob/master/aurpublish) — Gerencia pacotes do AUR como [subárvores git](https://raw.githubusercontent.com/git/git/master/contrib/subtree/git-subtree.txt). A [geração de arquivos `.SRCINFO`, verificação de `PKGBUILD`](https://github.com/Edenhofer/abs/blob/master/pre-commit.hook) e a [criação de um modelo de mensagem de commit por pacote](https://github.com/Edenhofer/abs/blob/master/prepare-commit-msg.hook) é deixada para os *hooks* git no mesmo [repositório](https://github.com/Edenhofer/abs/blob/master/README.md).

## Compilar e pesquisa

Esta é uma lista de utilitários auxiliares que pesquisam, baixam e/ou criam pacotes.

*   **aura** — Um gerenciador de pacotes para o Arch Linux escrito em Haskell. ([Página no fórum](https://bbs.archlinux.org/viewtopic.php?id=155778))

	[https://github.com/aurapm/aura](https://github.com/aurapm/aura) || [aura-bin](https://aur.archlinux.org/packages/aura-bin/)

*   **auracle** — Um cliente AUR escrito em C++.

	[https://github.com/falconindy/auracle](https://github.com/falconindy/auracle) || [auracle-git](https://aur.archlinux.org/packages/auracle-git/)

*   **aurel** — Pesquisa, vote e baixe pacotes do AUR a partir dor Emacs. ([Página no fórum](https://bbs.archlinux.org/viewtopic.php?id=177142))

	[https://github.com/alezost/aurel](https://github.com/alezost/aurel) || [aurel-git](https://aur.archlinux.org/packages/aurel-git/)

*   **aurget** — Interface semelhante ao pacman para o AUR, sem interfacear os comandos do pacman.

	[https://github.com/pbrisbin/aurget/](https://github.com/pbrisbin/aurget/) || [aurget](https://aur.archlinux.org/packages/aurget/)

*   **aurquery** — Wrapper com cache para a interface RPC do AUR usando a biblioteca python3-aur.

	[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

*   **aurutils** — Ferramentas auxiliares para o AUR. ([Página no fórum](https://bbs.archlinux.org/viewtopic.php?pid=1615428))

	[https://github.com/AladW/aurutils](https://github.com/AladW/aurutils) || [aurutils](https://aur.archlinux.org/packages/aurutils/)

*   **bauerbill** — Extensão do pacman/Powerpill com suporte para compilação de pacotes a partir do ABS e do AUR. ([Página no fórum](https://bbs.archlinux.org/viewtopic.php?id=205834))

	[http://xyne.archlinux.ca/projects/bauerbill](http://xyne.archlinux.ca/projects/bauerbill) || [bauerbill](https://aur.archlinux.org/packages/bauerbill/)

*   **burgaur** — Um front-end para cower escrito em Python.

	[https://github.com/m45t3r/burgaur](https://github.com/m45t3r/burgaur) || [burgaur](https://aur.archlinux.org/packages/burgaur/)

*   **cower** — Agente de pesquisa e download do AUR escrito em C, que também verifica por atualizações e dependências de pacotes. ([Página no fórum](https://bbs.archlinux.org/viewtopic.php?id=97137))

	[https://github.com/falconindy/cower](https://github.com/falconindy/cower) || [cower](https://aur.archlinux.org/packages/cower/)

*   **pacaur** — Um auxiliar do AUR que minimiza a interação do usuário. ([Página no fórum](https://bbs.archlinux.org/viewtopic.php?pid=937423))

	[https://github.com/rmarquis/pacaur](https://github.com/rmarquis/pacaur) || [pacaur](https://aur.archlinux.org/packages/pacaur/)

*   **pacget** — Um wrapper para o pacaur para simular o recurso de pesquisa do yaourt.

	[https://github.com/neurobin/pacget](https://github.com/neurobin/pacget) || [pacget](https://aur.archlinux.org/packages/pacget/)

*   **packer** — Wrapper para o pacman e o AUR. ([Página no fórum](https://bbs.archlinux.org/viewtopic.php?id=88115))

	[https://github.com/keenerd/packer](https://github.com/keenerd/packer) || [packer](https://aur.archlinux.org/packages/packer/)

*   **pbget** — Obtém arquivos fontes da interface web CVS e SVN do Arch, o AUR e o servidor rsync ABS.

	[http://xyne.archlinux.ca/projects/pbget](http://xyne.archlinux.ca/projects/pbget) || [pbget](https://aur.archlinux.org/packages/pbget/)

*   **PKGBUILDer** — Um auxiliar do AUR com suporte a dependência escrito em Python 3.

	[https://github.com/Kwpolska/pkgbuilder](https://github.com/Kwpolska/pkgbuilder) || [pkgbuilder](https://aur.archlinux.org/packages/pkgbuilder/)

*   **prm** — Um auxiliar do AUR e do ABS.

	[https://git.fleshless.org/prm/](https://git.fleshless.org/prm/) || [PKGBUILD](https://pkg.fleshless.org/prm/plain/PKGBUILD)

*   **repoctl** — Ferramenta para ajudar a gerenciar repositórios locais (com suporte ao AUR).

	[https://github.com/cassava/repoctl](https://github.com/cassava/repoctl) || [repoctl](https://aur.archlinux.org/packages/repoctl/)

*   **spinach** — Um auxiliar do AUR escrito em Bash

	[http://www.floft.net/code/spinach/](http://www.floft.net/code/spinach/) || [spinach](https://aur.archlinux.org/packages/spinach/)

*   **trizen** — Um wrapper para o AUR escrito em Perl.

	[https://github.com/trizen/trizen](https://github.com/trizen/trizen) || [trizen](https://aur.archlinux.org/packages/trizen/)

*   **wrapaur** — Um wrapper para o pacman e o AUR escrito em bash.

	|| [wrapaur](https://aur.archlinux.org/packages/wrapaur/)

*   **yaah** — Acrônimo para mais um auxiliar do AUR (*yet another AUR helper*)

	[https://bitbucket.org/the_metalgamer/yaah](https://bitbucket.org/the_metalgamer/yaah) || [yaah](https://aur.archlinux.org/packages/yaah/)

*   **yaourt** — Um wrapper para o AUR e pacotes comuns (repositórios oficiais).

	[https://archlinux.fr/yaourt-en](https://archlinux.fr/yaourt-en) || [yaourt](https://aur.archlinux.org/packages/yaourt/)

*   **yay** — Auxiliar do AUR escrito em Go.

	[https://github.com/Jguer/yay](https://github.com/Jguer/yay) || [yay](https://aur.archlinux.org/packages/yay/) ou [yay-bin](https://aur.archlinux.org/packages/yay-bin/) (binário)

## Manutenção

*   **pkgbuild-watch** — Procura por alterações nas páginas web dos *upstreams*

	[http://kmkeen.com/pkgbuild-watch](http://kmkeen.com/pkgbuild-watch) || [pkgbuild-watch](https://aur.archlinux.org/packages/pkgbuild-watch/)

*   **pkgbuildup** — Ajuda mantenedores de pacotes do AUR a atualizar automaticamente arquivos de PKGBUILD. Oferece suporta a uma sintaxe de variável de modelo.

	[https://github.com/fasheng/pkgbuildup](https://github.com/fasheng/pkgbuildup) || [pkgbuildup-git](https://aur.archlinux.org/packages/pkgbuildup-git/)

*   **pkgcheck** — Usa regras nos PKGBUILDs para analisar informações de versão no *upstream* ou procura por alterações analisando a soma de verificação da página web

	[https://bbs.archlinux.org/viewtopic.php?id=162816](https://bbs.archlinux.org/viewtopic.php?id=162816) || Repositório: [GitHub](https://github.com/onny/pkgcheck)

*   **pkgoutofdate** — Analisa a URL fonte dos PKGBUILDs e tenta localizar novas versões dos pacotes incrementando o número da versão e enviando requisições ao servidor web

	[https://github.com/anatol/pkgoutofdate](https://github.com/anatol/pkgoutofdate) || [pkgoutofdate-git](https://aur.archlinux.org/packages/pkgoutofdate-git/)

## Bibliotecas

*   **haskell-archlinux** — Biblioteca para acessar os metadados de pacotes e AURa partir da linguagem de programação Haskell

	[http://hackage.haskell.org/package/archlinux](http://hackage.haskell.org/package/archlinux) || [haskell-archlinux](https://aur.archlinux.org/packages/haskell-archlinux/)

*   **python3-aur** — Módulos Python 3 para acessar as informações de pacote do AUR e automatizar as interações do AUR.

	[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## Gráfico

*   **Aarchup** — Fork do archup. Possui as mesmas opções que o archup e também alguns outros recursos, para as diferenças entre ambos, favor verficiar o [changelog](https://bbs.archlinux.org/viewtopic.php?id=119129).

	[https://github.com/aericson/aarchup/](https://github.com/aericson/aarchup/) || [aarchup](https://aur.archlinux.org/packages/aarchup/)

*   **Argon** — Frontend gráfico para o pacaur, fornecendo instalação, remoção e atualização de pacotes; e atualiza notificações para pacotes dos repositórios oficiais e do AUR.

	[https://github.com/14mRh4X0r/arch-argon](https://github.com/14mRh4X0r/arch-argon) || [argon](https://aur.archlinux.org/packages/argon/)

*   **pamac** — Um daemon do DBus e frontend Gtk3 para o libalpm escrito em Vala.

	[https://github.com/manjaro/pamac/](https://github.com/manjaro/pamac/) || [pamac-aur](https://aur.archlinux.org/packages/pamac-aur/)

*   **PkgBrowser** — Aplicativo para pesquisar e navegar pelos pacotes do Arch, mostrando detalhes em pacotes selecionados.

	[https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home](https://bitbucket.org/kachelaqa/pkgbrowser/wiki/Home) || [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)

## Tabela comparativa

As colunas têm o seguinte significado:

*   *Seguro*: não [carrega](/index.php/Carrega "Carrega") o PKGBUILD por padrão, ou alerta o usuário e oferece a oportunidade de inspecionar o PKGBUILD manualmente antes dele ser carregado. Alguns auxiliares são conhecidos por carregar PKGBUILDs antes do usuário inspecioná-los, **permitindo códigos maliciosos serem executados**. *Opcional* significa que há uma opção de linha de comando ou opção de configuração para evitar o carregamento automático antes de visualizar.
*   *Compilação limpa*: não exporta novas variáveis que podem evitar um processo de compilação bem-sucedido.
*   *Analisador confiável*: habilidade de lidar com pacotes complexos usando os metadados fornecidos (RPC/.SRCINFO) em vez de [análise](https://en.wikipedia.org/wiki/pt:An%C3%A1lise_sint%C3%A1tica_(computa%C3%A7%C3%A3o)#Analisador_sint.C3.A1tico "w:pt:Análise sintática (computação)") do PKGBUILD, tal como [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/).
*   *Resolvedor confiável*: habilidade para resolver corretamente e compilar cadeias de dependência complexas, tal como [plasma-git-meta](https://aur.archlinux.org/packages/plasma-git-meta/).
*   *Pacotes divididos*: habilidade de compilar e instalar corretamente pacotes divididos (*split packages*) de forma independente, tal como [python-virtualfish](https://aur.archlinux.org/packages/python-virtualfish/) e [python2-virtualfish](https://aur.archlinux.org/packages/python2-virtualfish/).
*   *Git clone*: usa git-clones em vez de baixar tarballs (obsoleto desde o AUR 4).
*   *Sintaxe*: P significa tipo [Pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), E para específico.

| Nome | Escrito em | Seguro | Compilação limpa | Analisador confiável | Resolvedor confiável | Pacotes divididos | Git clone | Completação de shell | Sintaxe | Especificidade |
| aura | Haskell | Sim | Sim | Sim | Não | Não [[1]](https://github.com/aurapm/aura/issues/353) | Não | bash/zsh | P | Suporte a downgrade, [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)") e [powerpill](/index.php/Powerpill_(Portugu%C3%AAs) "Powerpill (Português)"), multilíngue, exibe [Unofficial user repositories/ArchHaskell](/index.php/Unofficial_user_repositories/ArchHaskell "Unofficial user repositories/ArchHaskell") |
| auracle | C++ | Sim | N/D | Sim | Sim | N/D | Não | N/D | E | Sem compilações automáticas |
| aurel | Emacs Lisp | Sim | N/D | Sim | N/D | N/D | Não | N/D | E | Integração com o Emacs, sem compilações automáticas |
| aurget | Bash | Opcional | Sim | Não | Não | Não [[2]](https://github.com/pbrisbin/aurget/issues/40) | Não | bash/zsh | P | ordena por votos |
| aurutils | Bash/C | Sim | Sim | Sim | Sim | Sim | Sim | zsh | E | [vifm](/index.php/Vifm "Vifm"), [PCRE](https://en.wikipedia.org/wiki/pt:PCRE "w:pt:PCRE"), [repositório local](/index.php/Reposit%C3%B3rio_local "Repositório local"), [assinatura de pacote](/index.php/Assinatura_de_pacote "Assinatura de pacote"), suporte a [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") |
| bauerbill | Python | Sim | Sim | Sim | Sim | Sim | Sim | bash/zsh | P/E | Gerenciamento de confiança, Suporte a ABS, estende Powerpill |
| burgaur | Python/C | Opcional, com [mc](/index.php/Mc "Mc") | Sim | Não | Não | Não | Não | Nenhum | P | Wrapper para *cower* |
| pacaur [*Precisando de mantenedor!*](https://bbs.archlinux.org/viewtopic.php?pid=1755144#p1755144) | Bash/C | Sim | Sim | Sim | Sim | Sim | Sim | bash/zsh | P/E | Minimiza interação de usuário, multilíngue, ordena por votos/popularidade |
| packer | Bash | Não | Sim | Não | Não | Não | Não | Nenhum | P | - |
| pbget | Python | Sim | N/D | Sim | N/D | N/D | Sim | Nenhum | E | Sem compilações automáticas |
| PKGBUILDer | Python | Opcional | Sim | Sim | Sim | Parcial [[3]](https://github.com/Kwpolska/pkgbuilder/issues/39) | Sim | Nenhum | P | Compilações automáticas por padrão, use `-F` para desabilitar; multilíngue |
| prm | Bash | Sim [[4]](https://git.fleshless.org/prm/commit/?id=e7252333b07975ea40f526269ce995e375e627bf) | N/D | Sim | N/D | N/D | Sim | Nenhum | E | Sem compilações automáticas, Suporte a ABS |
| repoctl | Go | Sim | N/D | Sim [[5]](https://github.com/goulash/pacman/blob/master/aur/aur.go) | N/D | N/D | Não | zsh | E | Sem compilações automáticas, suporte a repositório local |
| spinach | Bash | Sim [[6]](https://github.com/floft/spinach/commit/545574700812eb369b9537370f085ec9e5c3f01a) | Sim | Não | Não | Não | Não | Nenhum | E | - |
| trizen | Perl | Sim | Sim | Sim [[7]](https://github.com/trizen/trizen/commit/7ab7ee5f9f1f5d971b731d092fc8e1dd963add4b) | Sim | Sim [[8]](https://github.com/trizen/trizen/commit/3c94434c66ede793758f2bf7de84d68e3174e2ac) | Sim [[9]](https://github.com/trizen/trizen/commit/6fb0cc9e0ab66b8cca9493b0618ba4bab5fd2252) | bash/zsh | P | Comentários do AUR |
| wrapaur | Bash | Sim | Sim | Não | Não | Não | Sim | Nenhum | E | Atualiza espelhos (mirror), imprime notícias e comentários do AUR |
| yaah | Bash | Sim | N/D | Sim | N/D | N/D | Opcional | bash | E | Sem compilações automáticas |
| yaourt | Bash/C | Não (*yaourt -Si*) [[10]](https://github.com/archlinuxfr/yaourt/blob/f373121d23d87031a24135fee593115832d803ec/src/lib/aur.sh#L47) [[11]](https://github.com/archlinuxfr/yaourt/blob/d9790e29cd7194535c793f51d185b7130a396916/src/lib/pkgbuild.sh.in#L415-L438) | Não [[12]](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | Não | Não [[13]](https://github.com/archlinuxfr/yaourt/issues/186) | Não [[14]](https://github.com/archlinuxfr/yaourt/issues/85) | Opcional | bash/zsh/fish | P | Backup, Suporte a ABS, Comentários do AUR, multilíngue |
| yay | Go | Sim | Sim | Sim | Não | Parcial | Não | bash/zsh/fish | P | ordena por votos |

**Nota:** [Pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") 4.2\. introduziu campos específicos para arquitetura. [[15]](http://allanmcrae.com/2014/12/pacman-4-2-released/) Porém, desde 06 de abril de 2016, [AurJson](/index.php/AurJson_(Portugu%C3%AAs) "AurJson (Português)") combina todas as entradas em um único campo: [FS#48796](https://bugs.archlinux.org/task/48796). Auxiliares que dependam do RPC podem usar as soluções de contorno abaixo para obter dependências:

*   [bauerbill](https://aur.archlinux.org/packages/bauerbill/) [[16]](https://bbs.archlinux.org/viewtopic.php?pid=1617235#p1617235), [pkgbuilder](https://aur.archlinux.org/packages/pkgbuilder/) [[17]](https://github.com/Kwpolska/pkgbuilder/blob/65d9d74ef05f8996b81afb1cd005e3c337afa8b2/pkgbuilder/build.py#L198): Obter campos específicos do [.SRCINFO](/index.php/.SRCINFO_(Portugu%C3%AAs) ".SRCINFO (Português)")
*   [aurutils](https://aur.archlinux.org/packages/aurutils/) [[18]](https://github.com/AladW/aurutils/issues/80), [pacaur](https://aur.archlinux.org/packages/pacaur/) [[19]](https://github.com/rmarquis/pacaur/issues/465), [trizen](https://aur.archlinux.org/packages/trizen/) [[20]](https://github.com/trizen/trizen/commit/6a8ff9dc8cc83af783b8475dfbe89988dbc8a553): Remover o prefixo `lib32-` em sistemas `i686`