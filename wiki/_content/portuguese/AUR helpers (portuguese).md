**Status de tradução:** Esse artigo é uma tradução de [AUR helpers](/index.php/AUR_helpers "AUR helpers"). Data da última tradução: 2018-08-15\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=AUR_helpers&diff=0&oldid=534929) na versão em inglês.

**Atenção:** Auxiliares do AUR **não** [possuem suporte](https://bbs.archlinux.org/viewtopic.php?pid=828310#p828310) pelo Arch Linux. Você deve se familiarizar com o [processo manual de compilação](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#Instalando_pacotes "Arch User Repository (Português)") para estar preparado para diagnosticar e resolver problemas.

Os auxiliares do AUR automatizam certas tarefas para usar o [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"). A maioria dos auxiliares automatiza o processo de obtenção de um pacote [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") do AUR e a compilação do pacote. Na maioria dos casos, os pacotes instalados a partir do AUR não são verificados quanto a atualizações por [pacman (Português)](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"); Assim, alguns auxiliares verificam o AUR em busca de atualizações e automatizam o processo de recompilação. No entanto, lembre-se de que uma recompilação de um pacote do AUR, ou qualquer outro pacote criado e instalado localmente, pode ser necessária quando as bibliotecas compartilhadas forem atualizadas, e não apenas quando o pacote for atualizado.

Como não há suporte aos auxiliares do AUR, eles não estão presentes nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais").

## Contents

*   [1 Compilação e pesquisa](#Compila.C3.A7.C3.A3o_e_pesquisa)
    *   [1.1 Ativos](#Ativos)
    *   [1.2 Pesquisa apenas](#Pesquisa_apenas)
    *   [1.3 Descontinuados ou problemáticos](#Descontinuados_ou_problem.C3.A1ticos)
*   [2 Gráficos](#Gr.C3.A1ficos)
*   [3 Bibliotecas](#Bibliotecas)
*   [4 Manutenção](#Manuten.C3.A7.C3.A3o)
*   [5 Envio](#Envio)

## Compilação e pesquisa

As colunas têm o seguinte significado:

*   *Revisão de arquivo*: não [carrega](/index.php/Carrega "Carrega") o PKGBUILD por padrão, ou alerta o usuário e oferece a oportunidade de inspecionar o PKGBUILD manualmente antes dele ser carregado. Alguns auxiliares são conhecidos por carregar PKGBUILDs antes do usuário inspecioná-los, **permitindo códigos maliciosos serem executados**. *Opcional* significa que há uma opção de linha de comando ou opção de configuração para evitar o carregamento automático antes de visualizar.
*   *Compilação limpa*: não exporta novas variáveis que podem evitar um processo de compilação bem-sucedido.
*   *Wrapper do pacman*: quando usado como substituto para comandos do [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8), tal como `pacman -Syu`, o seguinte deve ser obedecido *por padrão*: [[1]](https://wiki.archlinux.org/index.php?title=Talk:AUR_helpers&oldid=515160#Add_.22pacman_wrap.22_column)

	– não separa comandos; por exemplo, `pacman -Syu` não é divido em `pacman -Sy` e `pacman -S *pacotes*`;

	– usa *pacman* diretamente, em vez de manipulação e uso de banco de dados manual do [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3).

	Além disso, [comandos potencialmente perigosos](/index.php/Manuten%C3%A7%C3%A3o_do_sistema#Evite_certos_comandos_do_pacman "Manutenção do sistema"), como o `pacman -Ud`, `pacman -Rdd`, `pacman --ask` ou `pacman --force` **não** são usados.

**Atenção:** Não obstante esses critérios, os auxiliares do AUR podem se desviar de [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) de várias maneiras, em particular para a instalação de pacotes nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"). Tal uso, portanto, **não** oferece suporte ou **não** é recomendado.

*   *Analisador confiável*: capacidade de lidar com pacotes complexos usando os metadados fornecidos (RPC/.SRCINFO) em vez de [análise](https://en.wikipedia.org/wiki/pt:An%C3%A1lise_sint%C3%A1tica_(computa%C3%A7%C3%A3o)#Analisador_sint.C3.A1tico do PKGBUILD, tal como [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/).
*   *Resolvedor confiável*: capacidade para resolver corretamente e compilar cadeias de dependência complexas, tal como [ros-lunar-desktop](https://aur.archlinux.org/packages/ros-lunar-desktop/).
*   *Pacotes divididos*: relacionado aos chamados *split packages* (inglês), é a capacidade de compilar e instalar corretamente:

	– Vários pacotes do mesmo pacote base, sem recompilar ou reinstalar várias vezes, tal como [clion](https://aur.archlinux.org/packages/clion/)

	– Pacotes divididos que dependem de um pacote do mesmo pacote base, tal como [libc++](https://aur.archlinux.org/packages/libc%2B%2B/) e [libc++abi](https://aur.archlinux.org/packages/libc%2B%2Babi/).

	– Pacotes divididos de forma independente, tal como [python-pyalsaaudio](https://aur.archlinux.org/packages/python-pyalsaaudio/) e [python2-pyalsaaudio](https://aur.archlinux.org/packages/python2-pyalsaaudio/).

*   *Git clone*: usa [git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1) por padrão para obter os arquivos de compilação a partir do AUR.
*   *Ver diff*: capacidade de visualizar as diferenças de pacote na inspeção. Além do PKGBUILD, isso inclui alterações em arquivos como `.install` ou `.patch`.
*   *Interação em lote*: capacidade de solicitar em sucessão direta, em particular para:

1.  Inspeção de PKGBUILDs;
2.  Resumo de atualizações de pacotes;
3.  Resolução de conflitos e instalações de pacotes.

	Um asterisco indica funcionalidade especificamente habilitada pelo usuário.

*   *Completação de shell*: [completação por Tab](https://en.wikipedia.org/wiki/Command-line_completion listados.

**Nota:**

*   As linhas da tabela estão ordenadas por valores das colunas, nas quais *Sim* ou *N/D* aparecem antes de *Parcial* ou *Opcional* e *Não*, ou alfabeticamente se os valores forem iguais.
*   *Opcional* significa que um recurso está disponível, mas apenas por meio de um argumento de linha de comando ou opção de configuração. *Parcial* significa que um recurso não está totalmente implementado, ou que ela parcialmente desvia do critério dado.

### Ativos

| Nome | Escrito em | Wrapper do pacman | Revisão de arquivo | Compilação limpa | Analisador confiável | Resolvedor confiável | Pacotes divididos | Git clone | Ver diff | Interação em lote | Completação de shell | Especificidade |
| [aurman](https://aur.archlinux.org/packages/aurman/) | Python | Sim | Sim | Sim | Sim | [Sim](https://github.com/polygamma/aurman/wiki/Description-of-the-aurman-dependency-solving) | Sim | Sim | Sim | 1, [2*, 3*](https://github.com/polygamma/aurman#question-6) | bash, fish | obtém chaves pgp, ordena por votos/popularidade, emite notícias |
| [aurutils](https://aur.archlinux.org/packages/aurutils/) | Bash/C | – | Sim | Sim | Sim | Sim | Sim | Sim | Sim | 1 | zsh | suporte a [vifm](/index.php/Vifm "Vifm"), [repositório local](/index.php/Reposit%C3%B3rio_local "Repositório local"), [assinatura de pacote](/index.php/Assinatura_de_pacote "Assinatura de pacote"), [chroot limpo](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot"), ordena por votos/popularidade |
| [yay](https://aur.archlinux.org/packages/yay/) | Go | Sim | Sim | Sim | Sim | Sim | Sim | [Sim](https://github.com/Jguer/yay/pull/297) | [Sim](https://github.com/Jguer/yay/pull/447) | 1, [2*](https://github.com/Jguer/yay/commit/3bdb5343218d99d40f8a449b887348611f6bdbfc), [3*](https://github.com/Jguer/yay/commit/ea5a94e0f8bb5f76879099e6d319c0c0102231c2) | bash, fish, zsh | obtém chaves PGP, ordena por votos/popularidade, [arquitetura de prompt](https://github.com/Jguer/yay/commit/4bcd3a6297052714e91e3f886602ce5c12d15786) |
| [pakku](https://aur.archlinux.org/packages/pakku/) | Nim | [divide](https://github.com/kitsunyan/pakku/wiki/Native-Pacman-Explanation) `-Syu` | Sim | [Sim](https://github.com/kitsunyan/pakku/commit/864cc0373fd6095295f68cc44d1657bd17269732) | Sim | Sim | Sim | Sim | [Sim](https://github.com/kitsunyan/pakku/commit/396e9f44c4f5a79c7b9238835599387f6ff418fe) | 1 | bash, zsh | Suporte a [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)"), comentários do AUR, obtém chaves PGP |
| [pikaur](https://aur.archlinux.org/packages/pikaur/) | Python | [divide](https://github.com/actionless/pikaur#pikaur) `-Syu` | Sim | Sim | Sim | Sim | [Sim](https://github.com/actionless/pikaur/commit/d409b958b4ff403d4fda06681231061854d32b3c) | Sim | Sim | 1, 2, 3 | bash, fish, zsh | [usuários dinâmicos](http://0pointer.net/blog/dynamic-users-with-systemd.html), [multilíngue](https://github.com/actionless/pikaur/tree/master/locale), ordena por votos/popularidade, emite notícias, [ignora erros](https://github.com/actionless/pikaur/commit/3688d828591d307c6864c3b5ad8c1f581396b865) |
| [trizen](https://aur.archlinux.org/packages/trizen/) | Perl | [Sim](https://github.com/trizen/trizen/commit/9e7b40e110175ea5bc7a0fa002ffadbf1106704b) | Sim | Sim | [Sim](https://github.com/trizen/trizen/commit/7ab7ee5f9f1f5d971b731d092fc8e1dd963add4b) | Sim | [Parcial](https://github.com/trizen/trizen/issues/46) | [Sim](https://github.com/trizen/trizen/commit/6fb0cc9e0ab66b8cca9493b0618ba4bab5fd2252) | Sim | 1* | bash, zsh, fish | Compilações automáticas por padrão, use `-G` para desabilitar, comentários do AUR |
| [bauerbill](https://aur.archlinux.org/packages/bauerbill/) | Python | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Não | 1 | bash, zsh | Gerenciamento de confiança, suporte a [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)"), estende o Powerpill |
| [PKGBUILDer](https://aur.archlinux.org/packages/PKGBUILDer/) | Python | [Sim](https://github.com/Kwpolska/pkgbuilder/blob/master/docs/wrapper.rst) | Opcional | Sim | Sim | Sim | [Parcial](https://github.com/Kwpolska/pkgbuilder/issues/39) | Sim | [Não](https://github.com/Kwpolska/pkgbuilder/issues/36) | 1* | – | Compilações automáticas por padrão, use `-F` para desabilitar; multilíngue |
| [naaman](https://aur.archlinux.org/packages/naaman/) | Python | – | Opcional | Sim | Sim | [Parcial](https://github.com/enckse/naaman/issues/19) | [Parcial](https://github.com/enckse/naaman/issues/20) | Sim | Não | 1* | bash | Compilações automáticas por padrão, use `--fetch` para desabilitar, use `-d` para habilitar o resolvedor |
| [aura](https://aur.archlinux.org/packages/aura/) | Haskell | [Sim](https://github.com/aurapm/aura/blob/master/aura/src/Aura/Pacman.hs) | Opcional | Sim | [Sim](https://github.com/aurapm/aura/commit/7848e9830cd880215f1d12a1c0294992428ea778) | Não | [Não](https://github.com/aurapm/aura/issues/353) | [Não](https://github.com/aurapm/aura/pull/346) | [Parcial](https://github.com/aurapm/aura/blob/89bf702bd0539fa757265c4c54ea2192155f85ed/aura/src/Aura/Pkgbuild/Records.hs) | 1* | bash, zsh | Compilações automáticas por padrão, use `--dryrun` para desabilitar, suporte a [downgrade](/index.php/Downgrade_(Portugu%C3%AAs) "Downgrade (Português)"), multilíngue |
| [repofish](https://aur.archlinux.org/packages/repofish/) | Bash | – | Opcional | Sim | Não | Não | Não | Sim | Sim | 1* | – | Compilações automáticas por padrão, use `check` ou `update` para desabilitar, suporte a [repositório local](/index.php/Reposit%C3%B3rio_local "Repositório local") |
| [aurget](https://aur.archlinux.org/packages/aurget/) | Bash | – | Opcional | Sim | Não | Não | [Não](https://github.com/pbrisbin/aurget/issues/40) | Não | [Não](https://github.com/pbrisbin/aurget/issues/41) | – | bash, zsh | ordena por votos |

### Pesquisa apenas

| Nome | Escrito em | Revisão de arquivo | Analisador confiável | Resolvedor confiável | Git clone | Completação
de shell | Especificidade |
| [pbget](https://aur.archlinux.org/packages/pbget/) | Python | Sim | Sim | – | Sim | – | – |
| [yaah](https://aur.archlinux.org/packages/yaah/) | Bash | Sim | Sim | – | Opcional | bash | – |
| [auracle-git](https://aur.archlinux.org/packages/auracle-git/) | C++ | Sim | Sim | Sim | Não | – | Imprime ordem de compilação |
| [cower](https://aur.archlinux.org/packages/cower/) | C | Sim | Sim | – | Não | bash, zsh | suporte a expressão regular, ordem por votos/popularidade |
| [package-query](https://aur.archlinux.org/packages/package-query/) | C | Sim | Não [[2]](https://github.com/archlinuxfr/package-query/issues/135) | – | – | – | – |
| [repoctl](https://aur.archlinux.org/packages/repoctl/) | Go | Sim | Sim [[3]](https://github.com/goulash/pacman/blob/master/aur/aur.go) | – | Não | zsh | Suporte a repositório local |

### Descontinuados ou problemáticos

Esta tabela descreve os projetos que foram descontinuados por seus autores ou que possuem problemas de *Segurança*, *Compilação limpa* ou *Pacman nativo* (consulte [#Compilação e pesquisa](#Compila.C3.A7.C3.A3o_e_pesquisa)) não tratados nos últimos 6 meses.

| Nome | Escrito em | Wrapper do pacman | Revisão de arquivo | Compilação limpa | Analisador confiável | Resolvedor confiável | Pacotes divididos | Git clone | Ver diff | Interação em lote | Completação de shell | Especificidade |
| [aurel](https://aur.archlinux.org/packages/aurel/) [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1522459#p1522459) | Emacs Lisp | – | Sim | – | – | – | – | Não | – | – | – | Integração com Emacs, sem compilações automáticas |
| [pacaur](https://aur.archlinux.org/packages/pacaur/) [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1755144#p1755144) | Bash/C | [usa](https://github.com/rmarquis/pacaur/commit/d8f49188452785fb28afc017baadd01d9e24ba21) `-Ud` | Sim | Sim | Sim | Sim | Sim | Sim | Sim | 1, 3 | bash, zsh | multilíngue, ordena por votos/popularidade |
| [wrapaur](https://aur.archlinux.org/packages/wrapaur/) | Bash | Sim | Sim | Sim | Não | Não | Não | Sim | Não | – | – | Atualizações de espelhos, emite notícias e comentários do AUR |
| [spinach](https://aur.archlinux.org/packages/spinach/) [[6]](https://github.com/floft/spinach) | Bash | – | [Sim](https://github.com/floft/spinach/commit/545574700812eb369b9537370f085ec9e5c3f01a) | Sim | Não | Não | Não | Não | Não | – | – | – |
| [burgaur](https://aur.archlinux.org/packages/burgaur/) [[7]](https://github.com/m45t3r/burgaur/issues/7#issuecomment-365599675) | Python/C | – | Opcional | Sim | Não | Não | Não | Não | Não | – | – | Wrapper para *cower* |
| [packer-aur-git](https://aur.archlinux.org/packages/packer-aur-git/) | Bash | Sim | Não | Sim | Não | Não | Não | Não | Não | – | – | – |
| [yaourt](https://aur.archlinux.org/packages/yaourt/) | Bash/C | divide `-Syu` | Não [[8]](https://github.com/archlinuxfr/yaourt/blob/f373121d23d87031a24135fee593115832d803ec/src/lib/aur.sh#L47) [[9]](https://github.com/archlinuxfr/yaourt/blob/d9790e29cd7194535c793f51d185b7130a396916/src/lib/pkgbuild.sh.in#L415-L438) | [Não](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | Não | [Não](https://github.com/archlinuxfr/yaourt/issues/186) | [Não](https://github.com/archlinuxfr/yaourt/issues/85) | Opcional | Opcional | 2 | bash, zsh, fish | Backup ([modifica o banco de dados do pacman!](https://github.com/archlinuxfr/yaourt/blob/5a82dfe/src/lib/alpm_backup.sh#L38)), suporte a ABS, emite comentários do AUR, multilíngue |

## Gráficos

**Atenção:**

*   Auxiliares gráficos do AUR são normalmente destinados a [distribuições baseadas no Arch](/index.php/Distribui%C3%A7%C3%B5es_baseadas_no_Arch "Distribuições baseadas no Arch"). Seu uso no [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)") pode levar a um sistema defeituoso, por exemplo, através de [atualizações parciais](/index.php/Atualiza%C3%A7%C3%B5es_parciais "Atualizações parciais") não assistidas.
*   Se um auxiliar *é conhecido* por apresentar comportamento problemático, está colorido com uma entrada vermelha.

| Nome | Escrito em | Toolkit gráfico | Auxiliar em backend | Notas |
| [aarchup](https://aur.archlinux.org/packages/aarchup/) | C | GTK+ 2 | auracle | – |
| [argon](https://aur.archlinux.org/packages/argon/) | Python | GTK+ 3 | auracle, pacaur | – |
| [cylon](https://aur.archlinux.org/packages/cylon/) | Bash | TUI | auracle, trizen | – |
| [kalu](https://aur.archlinux.org/packages/kalu/) | C | GTK+ 3 | – | – |
| [pactray](https://aur.archlinux.org/packages/pactray/) | Python | GTK+3 | auracle | – |
| [pamac-aur](https://aur.archlinux.org/packages/pamac-aur/) | Vala | GTK+ 3 | – | Usa [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3) em vez de [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) |
| [pakku-gui](https://aur.archlinux.org/packages/pakku-gui/) | Python | GTK+ 3 | pakku | – |
| [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/) | Python | Qt 5 | – | – |
| [updatehint](https://aur.archlinux.org/packages/updatehint/) | Bash | GTK+ 3 | auracle | – |
| [octopi](https://aur.archlinux.org/packages/octopi/) | C++ | Qt 5 | trizen, pacaur, yaourt | o serviço de notificação [habilitado no arquivo install](https://github.com/aarnt/octopi/blob/271c7e1/octopi.install) regularmente [realiza atualizações parciais](https://github.com/aarnt/octopi/issues/134#issuecomment-142099266) |

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