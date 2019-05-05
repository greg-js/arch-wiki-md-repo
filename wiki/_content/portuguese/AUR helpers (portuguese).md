**Status de tradução:** Esse artigo é uma tradução de [AUR helpers](/index.php/AUR_helpers "AUR helpers"). Data da última tradução: 2019-05-02\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=AUR_helpers&diff=0&oldid=572323) na versão em inglês.

**Atenção:** Auxiliares do AUR **não possuem suporte** pelo Arch Linux. Você deve se familiarizar com o [processo manual de compilação](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#Instalando_pacotes "Arch User Repository (Português)") para estar preparado para diagnosticar e resolver problemas.

**Nota:** Por favor, use a página de discussão para sugerir edições a este artigo: [Talk:AUR helpers](/index.php/Talk:AUR_helpers "Talk:AUR helpers").

Os auxiliares do AUR automatizam certos usos do [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"). A maioria dos auxiliares do AUR pode pesquisar por pacotes no AUR e obter seus [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") - outros, adicionalmente, assistem com o processo de compilação e instalação.

[Pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") só lida com atualizações para pacotes pré-compilados em seus repositórios. Pacotes do AUR são redistribuídos na forma de [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") e precisam de um auxiliar do AUR para automatizar o processo de recompilação. No entanto, lembre-se de que uma recompilação de um pacote pode ser necessária quando as suas dependências de bibliotecas compartilhadas forem atualizadas, e não apenas o pacote em si é atualizado.

Como não há suporte aos auxiliares do AUR, eles não estão presentes nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais").

## Legenda

As colunas da [#Tabela de comparação](#Tabela_de_comparação) têm o seguinte significado:

	Revisão de arquivo

	Não [carrega](/index.php/Carrega "Carrega") o PKGBUILD *por padrão*, ou alerta o usuário e oferece a oportunidade de inspecionar o PKGBUILD manualmente antes dele ser carregado. Alguns auxiliares são conhecidos por carregar PKGBUILDs antes do usuário inspecioná-los, **permitindo códigos maliciosos serem executados**.

	Ver diff

	Capacidade de visualizar as diferenças de pacote na inspeção. Além do PKGBUILD, isso inclui alterações em arquivos como os arquivos `.install` ou `.patch`.

	Git clone

	Usa [git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1) por padrão para obter os arquivos de compilação a partir do AUR.

	Analisador confiável

	Capacidade de tratar de pacotes complexos usando os metadados fornecidos ([RPC](/index.php/Interface_RPC_do_Aurweb "Interface RPC do Aurweb")/.SRCINFO) em vez de [análise](https://en.wikipedia.org/wiki/pt:An%C3%A1lise_sint%C3%A1tica_(computa%C3%A7%C3%A3o)#Analisador_sint.C3.A1tico do PKGBUILD, tal como [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/).

	Resolvedor confiável

	Capacidade de resolver e compilar corretamente cadeias de dependência complexas, tal como [ros-lunar-desktop](https://aur.archlinux.org/packages/ros-lunar-desktop/).

	Pacotes divididos

	Relacionado aos chamados *split packages* (inglês), é a capacidade de compilar e instalar corretamente:

*   Vários pacotes do mesmo pacote base, sem recompilar ou reinstalar várias vezes, tal como [clion](https://aur.archlinux.org/packages/clion/)
*   Pacotes divididos que dependem de um pacote do mesmo pacote base, tal como [libc++](https://aur.archlinux.org/packages/libc%2B%2B/) e [libc++abi](https://aur.archlinux.org/packages/libc%2B%2Babi/).
*   Pacotes divididos de forma independente, tal como [python-pyalsaaudio](https://aur.archlinux.org/packages/python-pyalsaaudio/) e [python2-pyalsaaudio](https://aur.archlinux.org/packages/python2-pyalsaaudio/).

	Interação em lote

	Capacidade de perguntar antes do processo de compilação e transações de pacote, em particular para:

1.  Resumo combinado de atualizações de repositório e de pacote do AUR;
2.  Resolução de conflitos e escolha de provedores.

	Completação de shell

	[Completação por Tab](https://en.wikipedia.org/wiki/Command-line_completion listados.

**Nota:** *Opcional* significa que um recurso está disponível, mas apenas por meio de um argumento de linha de comando ou opção de configuração. *Parcial* significa que um recurso não está totalmente implementado, ou que ela parcialmente desvia do critério dado.

## Tabela de comparação

### Pesquisa e download

| Nome | Escrito em | Git clone | Analisador confiável | Resolvedor confiável | Completação de shell | Especificidade |
| [auracle-git](https://aur.archlinux.org/packages/auracle-git/) | C++ | [Sim](https://github.com/falconindy/auracle/commit/c73bbee) | Sim | Sim | Bash | imprime ordem de compilação |
| [pbget](https://aur.archlinux.org/packages/pbget/) | Python | Sim | Sim | – | – | – |
| [repoctl](https://aur.archlinux.org/packages/repoctl/) | Go | Não | [Sim](https://github.com/goulash/pacman/blob/master/aur/aur.go) | – | zsh | [repositório local](/index.php/Reposit%C3%B3rio_local "Repositório local") |
| [yaah](https://aur.archlinux.org/packages/yaah/) | Bash | Opcional | Sim | – | bash | – |
| [aurel](https://aur.archlinux.org/packages/aurel/)
<small>([descontinuado](https://bbs.archlinux.org/viewtopic.php?pid=1522459#p1522459))</small> | Emacs Lisp | Não | Sim | – | – | Integração com [emacs](/index.php/Emacs "Emacs") |

### Pesquisa e compilação

| Nome | Escrito em | Revisão de arquivo | Ver diff | Git clone | Analisador confiável | Resolvedor confiável | Pacotes divididos | Completação
de shell | Especificidade |
| [aurget](https://aur.archlinux.org/packages/aurget/) | Bash | Não | [Não](https://github.com/pbrisbin/aurget/issues/41) | Não | Não | Não | [Não](https://github.com/pbrisbin/aurget/issues/40) | bash, zsh | – |
| [aurutils](https://aur.archlinux.org/packages/aurutils/) | Bash/C | Sim | Sim | Sim | Sim | Sim | Sim | bash, zsh | [modular](https://en.wikipedia.org/wiki/Modular_programming "w:Modular programming"), [repositório local](/index.php/Reposit%C3%B3rio_local "Repositório local"), [assinatura de pacote](/index.php/Assinatura_de_pacote "Assinatura de pacote"), [chroot limpo](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot") |
| [bauerbill](https://aur.archlinux.org/packages/bauerbill/) | Python | Sim | Não | Sim | Sim | Sim | Sim | bash, zsh | `bb-wrapper` para interfacear o *pacman*, gerenciamento de confiança |
| [PKGBUILDer](https://aur.archlinux.org/packages/PKGBUILDer/) | Python | Não | [Não](https://github.com/Kwpolska/pkgbuilder/issues/36) | Sim | Sim | Sim | [Parcial](https://github.com/Kwpolska/pkgbuilder/issues/39) | – | `pb` para interfacear o *pacman* |
| [repofish](https://aur.archlinux.org/packages/repofish/) | Bash | Não | Sim | Sim | Não | Não | Não | – | [repositório local](/index.php/Reposit%C3%B3rio_local "Repositório local") |
| [rua](https://aur.archlinux.org/packages/rua/) | Rust | Sim | [Não](https://github.com/vn971/rua/issues/1) | Sim | [Sim](https://github.com/vn971/rua/commit/fc8c2f3) | Sim | [Não](https://github.com/vn971/rua/issues/21) | bash, zsh, fish | [bubblewrap](/index.php/Bubblewrap "Bubblewrap"), inspeção de `.pkg.tar`, [somente compilação](https://github.com/vn971/rua/issues/13) |
| [spinach](https://aur.archlinux.org/packages/spinach/)
<small>([descontinuado](https://github.com/floft/spinach))</small> | Bash | [Sim](https://github.com/floft/spinach/commit/5455747) | Não | Não | Não | Não | Não | – | – |

### Wrappers do pacman

**Atenção:** Wrappers do [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) abstraem o trabalho do gerenciador de arquivos. Eles podem (opcionalmente ou por padrão) introduzir [opções inseguras](/index.php/Manuten%C3%A7%C3%A3o_do_sistema#Evite_certos_comandos_do_pacman "Manutenção do sistema") ou outros comportamentos inesperados levando a um sistema defeituoso.

| Nome | Escrito em | Revisão de arquivo | Ver diff | Git clone | Analisador confiável | Resolvedor confiável | Pacotes divididos | Opções inseguras | Completação
de shell | Especificidade |
| [aura](https://aur.archlinux.org/packages/aura/) | Haskell | Não | [Parcial](https://github.com/aurapm/aura/blob/89bf702/aura/src/Aura/Pkgbuild/Records.hs) | [Não](https://github.com/aurapm/aura/pull/346) | [Sim](https://github.com/aurapm/aura/commit/7848e983) | Não | [Não](https://github.com/aurapm/aura/issues/353) | – | bash, zsh | – |
| [pacaur](https://aur.archlinux.org/packages/pacaur/) | Bash/C | Sim | Sim | Sim | Sim | Sim | Sim | [--ask](https://github.com/rmarquis/pacaur/commit/12707cc) | bash, zsh | interação em lote 2 |
| [packer-aur-git](https://aur.archlinux.org/packages/packer-aur-git/) | Bash | Não | Não | Não | Não | Não | Não | – | – | – |
| [pakku](https://aur.archlinux.org/packages/pakku/) | Nim | Sim | [Sim](https://github.com/kitsunyan/pakku/commit/396e9f4) | Sim | Sim | Sim | Sim | [-Sy](https://github.com/kitsunyan/pakku/wiki/Native-Pacman-Explanation) | bash, zsh | obtém chaves PGP |
| [pikaur](https://aur.archlinux.org/packages/pikaur/) | Python | Sim | Sim | Sim | Sim | Sim | Sim | [-Sy](https://github.com/actionless/pikaur#pikaur) | bash, fish, zsh | interação em lote 1/2, [usuários dinâmicos](http://0pointer.net/blog/dynamic-users-with-systemd.html) |
| [trizen](https://aur.archlinux.org/packages/trizen/) | Perl | Sim | Sim | [Sim](https://github.com/trizen/trizen/commit/6fb0cc9) | [Sim](https://github.com/trizen/trizen/commit/7ab7ee5f) | Sim | [Parcial](https://github.com/trizen/trizen/issues/46) | [-Ud*](https://github.com/trizen/trizen/commit/9e7b40e)}} | bash, fish, zsh | – |
| [yay](https://aur.archlinux.org/packages/yay/) | Go | Sim | [Sim](https://github.com/Jguer/yay/pull/447) | [Sim](https://github.com/Jguer/yay/pull/297) | Sim | [Sim](https://github.com/Jguer/yay/pull/866) | Sim | [-Sy*](https://github.com/Jguer/yay/commit/3bdb534)
[--ask*](https://github.com/Jguer/yay/commit/ea5a94e) | bash, fish, zsh | interação em lote 1/2, obtém chaves PGP |
| [aurman](https://aur.archlinux.org/packages/aurman/)
<small>([descontinuado](https://github.com/polygamma/aurman#stopped-development-for-public-use))</small> | Python | Sim | Sim | Sim | Sim | [Não](https://github.com/polygamma/aurman/issues/259) | Sim | [-Sy*](https://github.com/polygamma/aurman/commit/6c02ba3)
[--ask*](https://github.com/polygamma/aurman#make-use-of-the-undocumented---ask-flag-of-pacman) | bash, fish | interação em lote 1/2, obtém chaves PGP |

## Gráficos

**Atenção:** O uso de auxiliares do AUR gráficos podem levar a um sistema defeituoso, por exemplo, através de [atualizações parciais](/index.php/Atualiza%C3%A7%C3%B5es_parciais "Atualizações parciais") não assistidas.

*   **Argon** — Wrapper do pacman em GTK+3 escrito em Python.

	[https://github.com/14mRh4X0r/arch-argon](https://github.com/14mRh4X0r/arch-argon) || [argon](https://aur.archlinux.org/packages/argon/)

*   **Cylon** — Wrapper do pacman em TUI escrito em Bash.

	[https://github.com/gavinlyonsrepo/cylon](https://github.com/gavinlyonsrepo/cylon) || [cylon](https://aur.archlinux.org/packages/cylon/)

*   **Pamac** — Gerenciador de pacotes autônomo em GTK+3 usando [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3) escrito em Vala.

	[https://gitlab.manjaro.org/applications/pamac](https://gitlab.manjaro.org/applications/pamac) || [pamac-aur](https://aur.archlinux.org/packages/pamac-aur/)

*   **Pakku GUI** — Frontend GTK+3 para o pakku escrito em Python.

	[https://gitlab.com/mrvik/pakku-gui](https://gitlab.com/mrvik/pakku-gui) || [pakku-gui](https://aur.archlinux.org/packages/pakku-gui/)

*   **PkgBrowser** — Navegador somente leitura Qt 5 para pacotes de repositórios e AUR escrito em Python.

	[https://bitbucket.org/kachelaqa/pkgbrowser](https://bitbucket.org/kachelaqa/pkgbrowser) || [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)

*   **Octopi** — Wrapper do pacman em Qt 5 escrito em C++. Pode levar a um sistema defeituoso, pois um noificação de serviço [habilitado na instalação](https://github.com/aarnt/octopi/blob/271c7e1/octopi.install) [realiza regularmente](https://github.com/aarnt/octopi/issues/134#issuecomment-142099266) [atualizações parciais](/index.php/Atualiza%C3%A7%C3%B5es_parciais "Atualizações parciais").

	[https://octopiproject.wordpress.com/](https://octopiproject.wordpress.com/) || [octopi](https://aur.archlinux.org/packages/octopi/)

## Manutenção

*   **aur-out-of-date** — Usa APIs do hospedeiro para verificar pacotes do AUR por alterações no upstream.

	[https://github.com/simon04/aur-out-of-date](https://github.com/simon04/aur-out-of-date) || [aur-out-of-date](https://aur.archlinux.org/packages/aur-out-of-date/)

*   **aurpublish** — Script auxiliar para gerenciar e fazer upload de pacotes do AUR usando [git-subtree(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-subtree.1). Usa [githooks(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/githooks.5) para verificar a integridade do PKGBUILD, gerar .SRCINFO automaticamente e criar um modelo de mensagem de commit.

	[https://github.com/eli-schwartz/aurpublish](https://github.com/eli-schwartz/aurpublish) || [aurpublish](https://www.archlinux.org/packages/?name=aurpublish)

*   **[devtools](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot")** — Compila pacotes em um ambiente limpo (contêiner de [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")) para garantir sua correção. Envolto por [aurutils](https://aur.archlinux.org/packages/aurutils/) e [clean-chroot-manager](https://aur.archlinux.org/packages/clean-chroot-manager/).

	[https://git.archlinux.org/devtools.git/](https://git.archlinux.org/devtools.git/) || [devtools](https://www.archlinux.org/packages/?name=devtools)

*   **pkgbuild-watch** — Procura por alterações nas páginas web dos *upstreams*.

	[http://kmkeen.com/pkgbuild-watch](http://kmkeen.com/pkgbuild-watch) || [pkgbuild-watch](https://aur.archlinux.org/packages/pkgbuild-watch/)

*   **pkgbuildup** — Ajuda mantenedores de pacotes do AUR a atualizar automaticamente arquivos de PKGBUILD. Oferece suporta a uma sintaxe de variável de modelo.

	[https://github.com/fasheng/pkgbuildup](https://github.com/fasheng/pkgbuildup) || [pkgbuildup-git](https://aur.archlinux.org/packages/pkgbuildup-git/)

*   **pkgoutofdate** — Analisa a URL fonte dos PKGBUILDs e tenta localizar novas versões dos pacotes incrementando o número da versão e enviando requisições ao servidor web.

	[https://github.com/anatol/pkgoutofdate](https://github.com/anatol/pkgoutofdate) || [pkgoutofdate-git](https://aur.archlinux.org/packages/pkgoutofdate-git/)

## Outros

*   **aur.rs** — Biblioteca em Rust para acessar [interface RPC do Aurweb](/index.php/Interface_RPC_do_Aurweb "Interface RPC do Aurweb")

	[https://github.com/zeyla/aur.rs](https://github.com/zeyla/aur.rs) ||

*   **aur-talk** — Buscar e exibir comentários AUR.

	[https://github.com/GermainZ/aur-talk](https://github.com/GermainZ/aur-talk) || [aur-talk-git](https://aur.archlinux.org/packages/aur-talk-git/)

*   **aurvote-utils** — Um conjunto de utilitários para gerenciar os votos do AUR.

	[https://github.com/jadenPete/aurvote-utils](https://github.com/jadenPete/aurvote-utils) || [aurvote-utils](https://aur.archlinux.org/packages/aurvote-utils/)

*   **haskell-aur** — Biblioteca Haskell para acessar a interface RPC do Aurweb

	[https://hackage.haskell.org/package/aur](https://hackage.haskell.org/package/aur) || [haskell-aur](https://aur.archlinux.org/packages/haskell-aur/)

*   **package-query** — Ferramenta para consultar [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3) e o AUR.

	[https://github.com/archlinuxfr/package-query](https://github.com/archlinuxfr/package-query) || [package-query](https://aur.archlinux.org/packages/package-query/)

*   **python3-aur** — Módulos Python 3 e utilitários auxiliares para acessar as informações de pacote do AUR e automatizar as interações do AUR.

	[https://xyne.archlinux.ca/projects/python3-aur](https://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)