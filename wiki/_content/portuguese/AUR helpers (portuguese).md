**Status de tradução:** Esse artigo é uma tradução de [AUR helpers](/index.php/AUR_helpers "AUR helpers"). Data da última tradução: 2018-10-25\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=AUR_helpers&diff=0&oldid=546605) na versão em inglês.

**Atenção:** Auxiliares do AUR **não possuem suporte** pelo Arch Linux. Você deve se familiarizar com o [processo manual de compilação](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#Instalando_pacotes "Arch User Repository (Português)") para estar preparado para diagnosticar e resolver problemas.

Os auxiliares do AUR automatizam certos usos do [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"). A maioria dos auxiliares do AUR pode pesquisar por pacotes no AUR e obter seus [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") - outros, adicionalmente, assistem com o processo de compilação e instalação.

[Pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") só lida com atualizações para pacotes pré-compilados em seus repositórios. Pacotes do AUR são redistribuídos na forma de [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") e precisam de um auxiliar do AUR para automatizar o processo de recompilação. No entanto, lembre-se de que uma recompilação de um pacote pode ser necessária quando as suas dependências de bibliotecas compartilhadas forem atualizadas, e não apenas o pacote em si é atualizado.

Como não há suporte aos auxiliares do AUR, eles não estão presentes nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais").

## Contents

*   [1 Legenda](#Legenda)
*   [2 Pesquisa e download](#Pesquisa_e_download)
*   [3 Download e compilação](#Download_e_compila.C3.A7.C3.A3o)
*   [4 Wrappers do pacman](#Wrappers_do_pacman)
*   [5 Gráficos](#Gr.C3.A1ficos)
    *   [5.1 Notificadores de atualização](#Notificadores_de_atualiza.C3.A7.C3.A3o)
*   [6 Bibliotecas](#Bibliotecas)
*   [7 Manutenção](#Manuten.C3.A7.C3.A3o)
*   [8 Envio](#Envio)

## Legenda

As colunas têm o seguinte significado:

*   *Revisão de arquivo*: não [carrega](/index.php/Carrega "Carrega") o PKGBUILD por padrão, ou alerta o usuário e oferece a oportunidade de inspecionar o PKGBUILD manualmente antes dele ser carregado. Alguns auxiliares são conhecidos por carregar PKGBUILDs antes do usuário inspecioná-los, **permitindo códigos maliciosos serem executados**. *Opcional* significa que há uma opção de linha de comando ou opção de configuração para evitar o carregamento automático antes de visualizar.
*   *Ver diff*: capacidade de visualizar as diferenças de pacote na inspeção. Além do PKGBUILD, isso inclui alterações em arquivos como `.install` ou `.patch`.
*   *Git clone*: usa [git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1) por padrão para obter os arquivos de compilação a partir do AUR.
*   *Analisador confiável*: capacidade de lidar com pacotes complexos usando os metadados fornecidos (RPC/.SRCINFO) em vez de [análise](https://en.wikipedia.org/wiki/pt:An%C3%A1lise_sint%C3%A1tica_(computa%C3%A7%C3%A3o)#Analisador_sint.C3.A1tico do PKGBUILD, tal como [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/).
*   *Resolvedor confiável*: capacidade para resolver corretamente e compilar cadeias de dependência complexas, tal como [ros-lunar-desktop](https://aur.archlinux.org/packages/ros-lunar-desktop/).
*   *Pacotes divididos*: relacionado aos chamados *split packages* (inglês), é a capacidade de compilar e instalar corretamente:

	– Vários pacotes do mesmo pacote base, sem recompilar ou reinstalar várias vezes, tal como [clion](https://aur.archlinux.org/packages/clion/)

	– Pacotes divididos que dependem de um pacote do mesmo pacote base, tal como [libc++](https://aur.archlinux.org/packages/libc%2B%2B/) e [libc++abi](https://aur.archlinux.org/packages/libc%2B%2Babi/).

	– Pacotes divididos de forma independente, tal como [python-pyalsaaudio](https://aur.archlinux.org/packages/python-pyalsaaudio/) e [python2-pyalsaaudio](https://aur.archlinux.org/packages/python2-pyalsaaudio/).

*   *Compilação limpa*: não exporta novas variáveis que podem evitar um processo de compilação bem-sucedido.
*   *Interação em lote*: capacidade de solicitar antes do processo de compilação, em particular para:

1.  Inspeção de arquivos do pacote ou suas diferenças;
2.  Resumo de atualizações de pacotes;
3.  Resolução de conflitos e instalações de pacotes.

	Um asterisco indica funcionalidade especificamente habilitada pelo usuário.

*   *Completação de shell*: [completação por Tab](https://en.wikipedia.org/wiki/Command-line_completion listados.

**Nota:**

*   As linhas da tabela estão ordenadas por valores das colunas, nas quais *Sim* ou *N/D* aparecem antes de *Parcial* ou *Opcional* e *Não*, ou alfabeticamente se os valores forem iguais.
*   *Opcional* significa que um recurso está disponível, mas apenas por meio de um argumento de linha de comando ou opção de configuração. *Parcial* significa que um recurso não está totalmente implementado, ou que ela parcialmente desvia do critério dado.

## Pesquisa e download

| Nome | Escrito em | Revisão de arquivo | Git clone | Analisador confiável | Resolvedor confiável | Completação de shell | Especificidade |
| [auracle-git](https://aur.archlinux.org/packages/auracle-git/) | C++ | Sim | [Sim](https://github.com/falconindy/auracle/commit/c73bbee) | Sim | Sim | Bash | imprime ordem de compilação |
| [pbget](https://aur.archlinux.org/packages/pbget/) | Python | Sim | Sim | Sim | – | – | – |
| [yaah](https://aur.archlinux.org/packages/yaah/) | Bash | Sim | Opcional | Sim | – | bash | – |
| [cower](https://aur.archlinux.org/packages/cower/) | C | Sim | Não | Sim | – | bash, zsh | suporte a expressão regular, ordem por votos/popularidade |
| [package-query](https://aur.archlinux.org/packages/package-query/) | C | Sim | – | [Não](https://github.com/archlinuxfr/package-query/issues/135) | – | – | apenas pesquisa |
| [repoctl](https://aur.archlinux.org/packages/repoctl/) | Go | Sim | Não | [Sim](https://github.com/goulash/pacman/blob/master/aur/aur.go) | – | zsh | suporte a repositório local |
| [aurel](https://aur.archlinux.org/packages/aurel/)
<small>([descontinuado](https://bbs.archlinux.org/viewtopic.php?pid=1522459#p1522459))</small> | Emacs Lisp | Sim | Não | Sim | – | – | Integração com Emacs |

## Download e compilação

| Nome | Escrito em | Revisão de arquivo | Ver diff | Git clone | Analisador confiável | Resolvedor confiável | Pacotes divididos | Compilação limpa | Interação em lote | Completação
de shell | Especificidade |
| [aurutils](https://aur.archlinux.org/packages/aurutils/) | Bash/C | Sim | Sim | Sim | Sim | Sim | Sim | Sim | 1 | zsh | suporte a [vifm](/index.php/Vifm "Vifm"), [repositório local](/index.php/Reposit%C3%B3rio_local "Repositório local"), [assinatura de pacote](/index.php/Assinatura_de_pacote "Assinatura de pacote"), [chroot limpo](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot"), ordena por votos/popularidade |
| [bauerbill](https://aur.archlinux.org/packages/bauerbill/) | Python | Sim | Não | Sim | Sim | Sim | Sim | Sim | 1 | bash, zsh | Gerenciamento de confiança, suporte a [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)"), estende o *powerpill*, `bb-wrapper` para interfacear o *pacman* |
| [PKGBUILDer](https://aur.archlinux.org/packages/PKGBUILDer/) | Python | Opcional | [Não](https://github.com/Kwpolska/pkgbuilder/issues/36) | Sim | Sim | Sim | [Parcial](https://github.com/Kwpolska/pkgbuilder/issues/39) | Sim | 1* | – | Compilações automáticas por padrão, use `-F` para desabilitar; multilíngue, `pb-wrapper` para interfacear o *pacman* |
| [naaman](https://aur.archlinux.org/packages/naaman/) | Python | Opcional | Não | Sim | Sim | [Parcial](https://github.com/enckse/naaman/issues/19) | [Parcial](https://github.com/enckse/naaman/issues/20) | Sim | 1* | bash | Compilações automáticas por padrão, use `--fetch` para desabilitar, use `-d` para habilitar o resolvedor |
| [repofish](https://aur.archlinux.org/packages/repofish/) | Bash | Opcional | Sim | Sim | Não | Não | Não | Sim | 1* | – | Compilações automáticas por padrão, use `check` ou `update` para desabilitar, suporte a [repositório local](/index.php/Reposit%C3%B3rio_local "Repositório local") |
| [aurget](https://aur.archlinux.org/packages/aurget/) | Bash | Opcional | [Não](https://github.com/pbrisbin/aurget/issues/41) | Não | Não | Não | [Não](https://github.com/pbrisbin/aurget/issues/40) | Sim | – | bash, zsh | ordena por votos |
| [spinach](https://aur.archlinux.org/packages/spinach/)
<small>([descontinuado](https://github.com/floft/spinach))</small> | Bash | [Sim](https://github.com/floft/spinach/commit/5455747) | Não | Não | Não | Não | Não | Sim | – | – | – |
| [burgaur](https://aur.archlinux.org/packages/burgaur/)
<small>([descontinuado](https://github.com/m45t3r/burgaur/issues/7#issuecomment-365599675))</small> | Python/C | Opcional | Não | Não | Não | Não | Não | Sim | – | – | Wrapper para *cower* |

## Wrappers do pacman

**Atenção:** Wrappers do [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) abstraem o trabalho do gerenciador de arquivos. Eles podem (opcionalmente ou por padrão) introduzir [opções inseguras](/index.php/Manuten%C3%A7%C3%A3o_do_sistema#Evite_certos_comandos_do_pacman "Manutenção do sistema") ou outros comportamentos inesperados levando a um sistema defeituoso.

| Nome | Escrito em | Revisão de arquivo | Ver diff | Git clone | Analisador confiável | Resolvedor confiável | Pacotes divididos | Compilação limpa | Opções inseguras | Interação em lote | Completação
de shell | Especificidade |
| [pakku](https://aur.archlinux.org/packages/pakku/) | Nim | Sim | [Sim](https://github.com/kitsunyan/pakku/commit/396e9f4) | Sim | Sim | Sim | Sim | [Sim](https://github.com/kitsunyan/pakku/commit/864cc03) | [-Sy](https://github.com/kitsunyan/pakku/wiki/Native-Pacman-Explanation) | 1 | bash, zsh | Suporte a [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)"), comentários do AUR, obtém chaves PGP |
| [pikaur](https://aur.archlinux.org/packages/pikaur/) | Python | Sim | Sim | Sim | Sim | Sim | [Sim](https://github.com/actionless/pikaur/commit/d409b95) | Sim | [-Sy](https://github.com/actionless/pikaur#pikaur) | 1, 2, 3 | bash, fish, zsh | [usuários dinâmicos](http://0pointer.net/blog/dynamic-users-with-systemd.html), [multilíngue](https://github.com/actionless/pikaur/tree/master/locale), ordena por votos/popularidade, emite notícias, [ignora erros](https://github.com/actionless/pikaur/commit/3688d828591d307c6864c3b5ad8c1f581396b865) |
| [yay](https://aur.archlinux.org/packages/yay/) | Go | Sim | [Sim](https://github.com/Jguer/yay/pull/447) | [Sim](https://github.com/Jguer/yay/pull/297) | Sim | Sim | Sim | Sim | [-Sy*](https://github.com/Jguer/yay/commit/3bdb534)
[--ask*](https://github.com/Jguer/yay/commit/ea5a94e) | 1, [2*](https://github.com/Jguer/yay/commit/3bdb534), [3*](https://github.com/Jguer/yay/commit/ea5a94e) | bash, fish, zsh | obtém chaves PGP, ordena por votos/popularidade, [arquitetura de prompt](https://github.com/Jguer/yay/commit/4bcd3a6) |
| [trizen](https://aur.archlinux.org/packages/trizen/) | Perl | Sim | Sim | [Sim](https://github.com/trizen/trizen/commit/6fb0cc9) | [Sim](https://github.com/trizen/trizen/commit/7ab7ee5f) | Sim | [Parcial](https://github.com/trizen/trizen/issues/46) | Sim | [-Ud*](https://github.com/trizen/trizen/commit/9e7b40e) | 1* | bash, fish, zsh | compilações automáticas por padrão, use `-G` para desabilitar, comentários do AUR |
| [aura](https://aur.archlinux.org/packages/aura/) | Haskell | Opcional | [Parcial](https://github.com/aurapm/aura/blob/89bf702/aura/src/Aura/Pkgbuild/Records.hs) | [Não](https://github.com/aurapm/aura/pull/346) | [Sim](https://github.com/aurapm/aura/commit/7848e983) | Não | [Não](https://github.com/aurapm/aura/issues/353) | Sim | – | 1* | bash, zsh | compilações automáticas por padrão, use `--dryrun` para desabilitar, suporte a [downgrade](/index.php/Downgrade_(Portugu%C3%AAs) "Downgrade (Português)"), multilíngue |
| [aurman](https://aur.archlinux.org/packages/aurman/)
<small>([sem suporte a usuário](https://github.com/polygamma/aurman#stopped-development-for-public-use))</small> | Python | Sim | Sim | Sim | Sim | [Sim](https://github.com/polygamma/aurman/wiki/Description-of-the-aurman-dependency-solving) | Sim | Sim | [-Sy*](https://github.com/polygamma/aurman/commit/6c02ba3)
[--ask*](https://github.com/polygamma/aurman#make-use-of-the-undocumented---ask-flag-of-pacman) | 1, [2*, 3*](https://github.com/polygamma/aurman#question-6) | bash, fish | obtém chaves PGP, ordena por votos/popularidade, emite notícias |
| [pacaur](https://aur.archlinux.org/packages/pacaur/)
<small>([descontinuado](https://bbs.archlinux.org/viewtopic.php?pid=1755144#p1755144))</small> | Bash/C | Sim | Sim | Sim | Sim | Sim | Sim | Sim | [-Ud](https://github.com/rmarquis/pacaur/commit/d8f4918)
[--ask](https://github.com/rmarquis/pacaur/commit/12707cc) | 1, 3 | bash, zsh | multilíngue, ordena por votos/popularidade |
| [wrapaur](https://aur.archlinux.org/packages/wrapaur/)
<small>(parado)</small> | Bash | Sim | Não | Sim | Não | Não | Não | Sim | – | – | – | atualizações de espelhos, emite notícias e comentários do AUR |
| [packer-aur](https://aur.archlinux.org/packages/packer-aur/)
<small>(parado)</small> | Bash | Não | Não | Não | Não | Não | Não | Sim | – | – | – | – |
| [yaourt](https://aur.archlinux.org/packages/yaourt/)
<small>(parado)</small> | Bash/C | [Não](https://github.com/archlinuxfr/yaourt/blob/34b5c0b/src/lib/aur.sh#L54-L72) | Opcional | Opcional | Não | [Não](https://github.com/archlinuxfr/yaourt/issues/186) | [Não](https://github.com/archlinuxfr/yaourt/issues/85) | [Não](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | [-Sy](https://github.com/archlinuxfr/yaourt/blob/d30823e/yaourt/yaourt#L1773) | 2 | bash, fish, zsh | suporte a ABS, emite comentários do AUR, multilíngue |

## Gráficos

**Atenção:**

*   Auxiliares gráficos do AUR são normalmente destinados a [distribuições baseadas no Arch](/index.php/Distribui%C3%A7%C3%B5es_baseadas_no_Arch "Distribuições baseadas no Arch"). Seu uso no [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)") pode levar a um sistema defeituoso, por exemplo, através de [atualizações parciais](/index.php/Atualiza%C3%A7%C3%B5es_parciais "Atualizações parciais") não assistidas.
*   Se um auxiliar *é conhecido* por apresentar comportamento problemático, está colorido com uma entrada vermelha.

| Nome | Escrito em | Toolkit gráfico | Notas |
| [argon](https://aur.archlinux.org/packages/argon/) | Python | GTK+ 3 | – |
| [cylon](https://aur.archlinux.org/packages/cylon/) | Bash | TUI | – |
| [pamac-aur](https://aur.archlinux.org/packages/pamac-aur/) | Vala | GTK+ 3 | usa [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3) em vez de [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) |
| [pakku-gui](https://aur.archlinux.org/packages/pakku-gui/) | Python | GTK+ 3 | – |
| [PkgBrowser](https://aur.archlinux.org/packages/PkgBrowser/) | Python | Qt 5 | navegador somente leitura para pacotes de repositórios e do AUR |
| [octopi](https://aur.archlinux.org/packages/octopi/) | C++ | Qt 5 | o serviço de notificação [habilitado no arquivo install](https://github.com/aarnt/octopi/blob/271c7e1/octopi.install) regularmente [realiza atualizações parciais](https://github.com/aarnt/octopi/issues/134#issuecomment-142099266) |

### Notificadores de atualização

| Nome | Pacote | Escrito em | Toolkit gráfico |
| aarchup | [aarchup](https://aur.archlinux.org/packages/aarchup/) | C | GTK+ 2 |
| arch-update | [gnome-shell-extension-arch-update](https://aur.archlinux.org/packages/gnome-shell-extension-arch-update/) | JavaScript | Clutter |
| kalu | [kalu](https://aur.archlinux.org/packages/kalu/) | C | GTK+ 3 |
| pactray | [pactray](https://aur.archlinux.org/packages/pactray/) | Python | GTK+ 3 |
| Arch Updater | [plasma5-applets-kde-arch-update-notifier-git](https://aur.archlinux.org/packages/plasma5-applets-kde-arch-update-notifier-git/) | C++/QML | Qt 5 |
| updatehint | [updatehint](https://aur.archlinux.org/packages/updatehint/) | Bash | GTK+ 3 |

## Bibliotecas

*   **haskell-archlinux** — Biblioteca para acessar os metadados de pacotes e AURa partir da linguagem de programação Haskell.

	[http://hackage.haskell.org/package/archlinux](http://hackage.haskell.org/package/archlinux) || [haskell-archlinux](https://aur.archlinux.org/packages/haskell-archlinux/)

*   **python3-aur** — Módulos Python 3 para acessar as informações de pacote do AUR e automatizar as interações do AUR.

	[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## Manutenção

*   **aur-out-of-date** — Usa APIs do hospedeiro para verificar pacotes do AUR por alterações no upstream.

	[https://github.com/simon04/aur-out-of-date](https://github.com/simon04/aur-out-of-date) || [aur-out-of-date](https://aur.archlinux.org/packages/aur-out-of-date/)

*   **pkgbuild-watch** — Procura por alterações nas páginas web dos *upstreams*.

	[http://kmkeen.com/pkgbuild-watch](http://kmkeen.com/pkgbuild-watch) || [pkgbuild-watch](https://aur.archlinux.org/packages/pkgbuild-watch/)

*   **pkgbuildup** — Ajuda mantenedores de pacotes do AUR a atualizar automaticamente arquivos de PKGBUILD. Oferece suporta a uma sintaxe de variável de modelo.

	[https://github.com/fasheng/pkgbuildup](https://github.com/fasheng/pkgbuildup) || [pkgbuildup-git](https://aur.archlinux.org/packages/pkgbuildup-git/)

*   **pkgoutofdate** — Analisa a URL fonte dos PKGBUILDs e tenta localizar novas versões dos pacotes incrementando o número da versão e enviando requisições ao servidor web.

	[https://github.com/anatol/pkgoutofdate](https://github.com/anatol/pkgoutofdate) || [pkgoutofdate-git](https://aur.archlinux.org/packages/pkgoutofdate-git/)

## Envio

*   [aur4_import.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_import.sh) — Divide um pacote de um repositório git com múltiplos pacotes, adicionando/atualizando `.SRCINFO` para cada commit
*   [aur4_make_submodule.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_make_submodule.sh) — Substitui um pacote em um repositório git maior com um submódulo do AUR 4, incluindo `.SRCINFO`
*   **aurpublish** — Scripts auxiliar para gerenciar e atualizar pacotes do AUR usando [git-subtree(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-subtree.1). Usa [githooks(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/githooks.5) para verificar a integridade do PKGBUILD, gera .SRCINFO automaticamente e cria um modelo de mensagem de commit.

	[https://github.com/eli-schwartz/aurpublish](https://github.com/eli-schwartz/aurpublish) || [aurpublish](https://www.archlinux.org/packages/?name=aurpublish)