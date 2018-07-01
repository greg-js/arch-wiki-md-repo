**Atenção:**

*   Auxiliares do AUR **não** [possuem suporte](https://bbs.archlinux.org/viewtopic.php?pid=828254#p828254) pelo Arch Linux. É recomendado se tornar familiar com o [processo manual de compilação](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#Instalando_pacotes "Arch User Repository (Português)") para estar preparado para diagnosticar e resolver problemas por conta própria.
*   Auxiliares do AUR podem replicar o uso do [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8) para os [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"), tais como `pacman -Syu`. Esse uso pode desviar do *pacman* em várias formas; portanto, **não** há suporte nem é recomendado.

Auxiliares do AUR são escritos para automatizar certas tarefas para o [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)").

## Contents

*   [1 Compilação e pesquisa](#Compila.C3.A7.C3.A3o_e_pesquisa)
    *   [1.1 Ativos](#Ativos)
    *   [1.2 Pesquisa apenas](#Pesquisa_apenas)
    *   [1.3 Inativos](#Inativos)
*   [2 Bibliotecas](#Bibliotecas)
*   [3 Manutenção](#Manuten.C3.A7.C3.A3o)
*   [4 Envio](#Envio)

## Compilação e pesquisa

As colunas têm o seguinte significado:

*   *Seguro*: não [carrega](/index.php/Carrega "Carrega") o PKGBUILD por padrão, ou alerta o usuário e oferece a oportunidade de inspecionar o PKGBUILD manualmente antes dele ser carregado. Alguns auxiliares são conhecidos por carregar PKGBUILDs antes do usuário inspecioná-los, **permitindo códigos maliciosos serem executados**. *Opcional* significa que há uma opção de linha de comando ou opção de configuração para evitar o carregamento automático antes de visualizar.
*   *Compilação limpa*: não exporta novas variáveis que podem evitar um processo de compilação bem-sucedido.
*   *Analisador confiável*: habilidade de lidar com pacotes complexos usando os metadados fornecidos (RPC/.SRCINFO) em vez de [análise](https://en.wikipedia.org/wiki/pt:An%C3%A1lise_sint%C3%A1tica_(computa%C3%A7%C3%A3o)#Analisador_sint.C3.A1tico "w:pt:Análise sintática (computação)") do PKGBUILD, tal como [aws-cli-git](https://aur.archlinux.org/packages/aws-cli-git/).
*   *Resolvedor confiável*: habilidade para resolver corretamente e compilar cadeias de dependência complexas, tal como [ros-lunar-desktop](https://aur.archlinux.org/packages/ros-lunar-desktop/).
*   *Pacotes divididos*: relacionado aos chamados, em inglês, *split packages*, é a habilidade de compilar e instalar corretamente:

	– Vários pacotes do mesmo pacote base, sem recompilar ou reinstalar várias vezes, tal como [clion](https://aur.archlinux.org/packages/clion/)

	– Pacotes divididos que dependem de um pacote do mesmo pacote base, tal como [libc++](https://aur.archlinux.org/packages/libc%2B%2B/) e [libc++abi](https://aur.archlinux.org/packages/libc%2B%2Babi/).

	– Pacotes divididos de forma independente, tal como [python-pyalsaaudio](https://aur.archlinux.org/packages/python-pyalsaaudio/) e [python2-pyalsaaudio](https://aur.archlinux.org/packages/python2-pyalsaaudio/).

*   *Git clone*: usa [git-clone(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/git-clone.1) por padrão para obter os arquivos de compilação a partir do AUR.
*   *Pacman nativo*: quando usado como substituto para comandos do [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8), tal como`pacman -Syu`, os a seguir são obedecidos *por padrão*:

	– não separa comandos; por exemplo, `pacman -Syu` não é divido em `pacman -Sy` e `pacman -S *pacotes*`;

	– usa *pacman* diretamente, em vez de manipulação e uso de banco de dados manual do [libalpm(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/libalpm.3).

	Além disso, comandos sem suporte, como o `pacman -Ud`, `pacman -Rdd` ou `pacman --force` **não** são usados.

*   *Completação de shell*: [completação por tab](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion") está disponível para os [shells](/index.php/Shell_(Portugu%C3%AAs) "Shell (Português)") listados.

**Nota:**

*   As linhas da tabela estão ordenadas por valores das colunas, nas quais *Sim* ou *N/D* aparecem antes de *Parcial* ou *Opcional* e *Não*, ou alfabeticamente se os valores forem iguais.
*   *Opcional* significa que um recurso está disponível, mas apenas por meio de um argumento de linha de comando ou opção de configuração. *Parcial* significa que um recurso não está totalmente implementado, ou que ela desvia do critério dado de uma forma pequena.

### Ativos

| Nome | Escrito em | Seguro | Compilação limpa | Analisador confiável | Resolvedor confiável | Pacotes divididos | Git clone | Pacman nativo | Completação de shell | Especificidade |
| [aurman](https://aur.archlinux.org/packages/aurman/) | Python | Sim | Sim | Sim | Sim | Sim | Sim | Sim | bash, fish | interação em lote, obtém chaves pgp, ordena por popularidade, [pesquisa profunda](https://github.com/polygamma/aurman/wiki/Description-of-the-aurman-dependency-solving) |
| [aurutils](https://aur.archlinux.org/packages/aurutils/) | Bash/C | Sim | Sim | Sim | Sim | Sim | Sim | N/D | zsh | suporte a [vifm](/index.php/Vifm "Vifm"), [PCRE](https://en.wikipedia.org/wiki/pt:PCRE "w:pt:PCRE"), [repositório local](/index.php/Reposit%C3%B3rio_local "Repositório local"), [assinatura de pacote](/index.php/Assinatura_de_pacote "Assinatura de pacote"), [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn"), ordena por votos/popularidade |
| [bauerbill](https://aur.archlinux.org/packages/bauerbill/) | Python | Sim | Sim | Sim | Sim | Sim | Sim | Sim | bash, zsh | Gerenciamento de confiança, Suporte a ABS, estende o Powerpill |
| [pakku](https://aur.archlinux.org/packages/pakku/) | Nim | Sim | Sim [[1]](https://github.com/kitsunyan/pakku/commit/864cc0373fd6095295f68cc44d1657bd17269732) | Sim | Sim | Sim | Sim | Parcial [[2]](https://github.com/kitsunyan/pakku/wiki/Pacman-Wrap-Explanation) | bash | Comentários do AUR, interação em lote, obtém chaves PGP |
| [pikaur](https://aur.archlinux.org/packages/pikaur/) | Python | Sim | Sim | Sim | Sim | Sim [[3]](https://github.com/actionless/pikaur/commit/d409b958b4ff403d4fda06681231061854d32b3c) | Sim | Parcial [[4]](https://github.com/actionless/pikaur/issues/81) | bash, fish, zsh | [usuários dinâmicos](http://0pointer.net/blog/dynamic-users-with-systemd.html), multilíngue, ordena por votos/popularidade, interação em lote |
| [yay](https://aur.archlinux.org/packages/yay/) | Go | Sim | Sim | Sim | Sim | Sim | Sim [[5]](https://github.com/Jguer/yay/pull/297) | Parcial [[6]](https://github.com/Jguer/yay/commit/98ea801004fc63b5a294f46392910e85286ffd98) | bash, zsh, fish | ordena por votos, interação em lote, obtém chaves PGP, [arquitetura de prompt](https://github.com/Jguer/yay/pull/260) |
| [PKGBUILDer](https://aur.archlinux.org/packages/PKGBUILDer/) | Python | Opcional | Sim | Sim | Sim | Parcial [[7]](https://github.com/Kwpolska/pkgbuilder/issues/39) | Sim | Sim [[8]](https://github.com/Kwpolska/pkgbuilder/blob/master/docs/wrapper.rst) | Nenhum | Compilações automáticas por padrão, use `-F` para desabilitar; multilíngue |
| [trizen](https://aur.archlinux.org/packages/trizen/) | Perl | Sim | Sim | Sim [[9]](https://github.com/trizen/trizen/commit/7ab7ee5f9f1f5d971b731d092fc8e1dd963add4b) | Sim | Sim [[10]](https://github.com/trizen/trizen/commit/3c94434c66ede793758f2bf7de84d68e3174e2ac) | Sim [[11]](https://github.com/trizen/trizen/commit/6fb0cc9e0ab66b8cca9493b0618ba4bab5fd2252) | Não [[12]](https://github.com/trizen/trizen/commit/ba687bc3c3e306e6f3942e95f825ed6a55d3ad69) | bash, zsh,fish | Comentários do AUR |
| [naaman](https://aur.archlinux.org/packages/naaman/) | Python | Opcional | Sim | Sim | Não | Não | Sim | N/D | bash | Compilações automáticas por padrão, use `--fetch` para desabilitar |
| [aura](https://aur.archlinux.org/packages/aura/) | Haskell | Sim | Sim | Sim [[13]](https://github.com/aurapm/aura/commit/7848e9830cd880215f1d12a1c0294992428ea778) | Não | Não [[14]](https://github.com/aurapm/aura/issues/353) | Não [[15]](https://github.com/aurapm/aura/pull/346) | Sim [[16]](https://github.com/aurapm/aura/blob/master/aura/src/Aura/Pacman.hs) | bash, zsh | Suporte a downgrade, [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)"), [powerpill](/index.php/Powerpill_(Portugu%C3%AAs) "Powerpill (Português)"), multilíngue, requer [ArchHaskell](/index.php/ArchHaskell "ArchHaskell") |

### Pesquisa apenas

| Nome | Escrito em | Seguro | Analisador confiável | Resolvedor confiável | Git clone | Completação
de shell | Especificidade |
| [pbget](https://aur.archlinux.org/packages/pbget/) | Python | Sim | Sim | N/D | Sim | Nenhuma | - |
| [yaah](https://aur.archlinux.org/packages/yaah/) | Bash | Sim | Sim | N/D | Opcional | bash | - |
| [auracle-git](https://aur.archlinux.org/packages/auracle-git/) | C++ | Sim | Sim | Sim | Não | N/D | Imprime ordem de compilação |
| [cower](https://aur.archlinux.org/packages/cower/) | C | Sim | Sim | N/D | Não | bash/zsh | suporte a expressão regular, ordem por votos/popularidade |
| [package-query](https://aur.archlinux.org/packages/package-query/) | C | Sim | Não [[17]](https://github.com/archlinuxfr/package-query/issues/135) | N/D | N/D | Nenhuma | - |
| [repoctl](https://aur.archlinux.org/packages/repoctl/) | Go | Sim | Sim [[18]](https://github.com/goulash/pacman/blob/master/aur/aur.go) | N/D | Não | zsh | suporte a repositório local |

### Inativos

Um projeto é considerado *inativo* se ele foi descontinuado pelo autor ou se problemas de segurança e de compilação limpa foram ignorados por pelo menos 6 meses.

| Nome | Escrito em | Seguro | Compilação limpa | Analisador confiável | Resolvedor confiável | Pacotes divididos | Git clone | Pacman nativo | Completação de shell | Especificidade |
| [aurel-git](https://aur.archlinux.org/packages/aurel-git/) [[19]](https://bbs.archlinux.org/viewtopic.php?pid=1522459#p1522459) | Emacs Lisp | Sim | N/D | Sim | N/D | N/D | Não | N/D | N/D | Integração com Emacs, sem compilações automáticas |
| [pacaur](https://aur.archlinux.org/packages/pacaur/) [[20]](https://bbs.archlinux.org/viewtopic.php?pid=1755144#p1755144) | Bash/C | Sim | Sim | Sim | Sim | Sim | Sim | Não [[21]](https://github.com/rmarquis/pacaur/commit/d8f49188452785fb28afc017baadd01d9e24ba21) | bash, zsh | multilíngue, ordena por votos/popularidade, interação em lote |
| [wrapaur](https://aur.archlinux.org/packages/wrapaur/) | Bash | Sim | Sim | Não | Não | Não | Sim | Sim | Nenhum | Atualizações de espelhos, emite notícias e comentários do AUR |
| [spinach](https://aur.archlinux.org/packages/spinach/) | Bash | Sim [[22]](https://github.com/floft/spinach/commit/545574700812eb369b9537370f085ec9e5c3f01a) | Sim | Não | Não | Não | Não | N/D | Nenhum | - |
| [aurget](https://aur.archlinux.org/packages/aurget/) | Bash | Opcional | Sim | Não | Não | Não [[23]](https://github.com/pbrisbin/aurget/issues/40) | Não | N/D | bash, zsh | ordena por votos |
| [burgaur](https://aur.archlinux.org/packages/burgaur/) [[24]](https://github.com/m45t3r/burgaur/issues/7#issuecomment-365599675) | Python/C | Opcional | Sim | Não | Não | Não | Não | N/D | Nenhum | Wrapper para *cower* |
| [packer](https://aur.archlinux.org/packages/packer/) | Bash | Não | Sim | Não | Não | Não | Não | Sim | Nenhum | - |
| [yaourt](https://aur.archlinux.org/packages/yaourt/) | Bash/C | Não [[25]](https://github.com/archlinuxfr/yaourt/blob/f373121d23d87031a24135fee593115832d803ec/src/lib/aur.sh#L47) [[26]](https://github.com/archlinuxfr/yaourt/blob/d9790e29cd7194535c793f51d185b7130a396916/src/lib/pkgbuild.sh.in#L415-L438) | Não [[27]](https://lists.archlinux.org/pipermail/aur-general/2015-August/031314.html) | Não | Não [[28]](https://github.com/archlinuxfr/yaourt/issues/186) | Não [[29]](https://github.com/archlinuxfr/yaourt/issues/85) | Opcional | Não | bash, zsh, fish | Backup, Suporte a ABS, comentários do AUR, multilíngue |

## Bibliotecas

*   **haskell-archlinux** — Biblioteca para acessar os metadados de pacotes e AURa partir da linguagem de programação Haskell

	[http://hackage.haskell.org/package/archlinux](http://hackage.haskell.org/package/archlinux) || [haskell-archlinux](https://aur.archlinux.org/packages/haskell-archlinux/)

*   **python3-aur** — Módulos Python 3 para acessar as informações de pacote do AUR e automatizar as interações do AUR.

	[http://xyne.archlinux.ca/projects/python3-aur](http://xyne.archlinux.ca/projects/python3-aur) || [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## Manutenção

*   **aur-out-of-date** — Usa APIs do hospedeiro para verificar pacotes do AUR por alterações no upstream

	[https://github.com/simon04/aur-out-of-date](https://github.com/simon04/aur-out-of-date) || [aur-out-of-date](https://aur.archlinux.org/packages/aur-out-of-date/)

*   **pkgbuild-watch** — Procura por alterações nas páginas web dos *upstreams*

	[http://kmkeen.com/pkgbuild-watch](http://kmkeen.com/pkgbuild-watch) || [pkgbuild-watch](https://aur.archlinux.org/packages/pkgbuild-watch/)

*   **pkgbuildup** — Ajuda mantenedores de pacotes do AUR a atualizar automaticamente arquivos de PKGBUILD. Oferece suporta a uma sintaxe de variável de modelo.

	[https://github.com/fasheng/pkgbuildup](https://github.com/fasheng/pkgbuildup) || [pkgbuildup-git](https://aur.archlinux.org/packages/pkgbuildup-git/)

*   **pkgoutofdate** — Analisa a URL fonte dos PKGBUILDs e tenta localizar novas versões dos pacotes incrementando o número da versão e enviando requisições ao servidor web

	[https://github.com/anatol/pkgoutofdate](https://github.com/anatol/pkgoutofdate) || [pkgoutofdate-git](https://aur.archlinux.org/packages/pkgoutofdate-git/)

## Envio

*   [aur4_import.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_import.sh) — Divide um pacote de um repositório git com múltiplos pacotes, adicionando/atualizando `.SRCINFO` para cada commit.
*   [aur4_make_submodule.sh](https://github.com/JonnyJD/PKGBUILDs/blob/master/_bin/aur4_make_submodule.sh) — Substitui um pacote em um repositório git maior com um submódulo do AUR 4, incluindo `.SRCINFO`.
*   [aurpublish](https://github.com/Edenhofer/abs/blob/master/aurpublish) — Gerencia pacotes do AUR como [subárvores git](https://raw.githubusercontent.com/git/git/master/contrib/subtree/git-subtree.txt). A [geração de arquivos `.SRCINFO`, verificação de `PKGBUILD`](https://github.com/Edenhofer/abs/blob/master/pre-commit.hook) e a [criação de um modelo de mensagem de commit por pacote](https://github.com/Edenhofer/abs/blob/master/prepare-commit-msg.hook) é deixada para os *hooks* git no mesmo [repositório](https://github.com/Edenhofer/abs/blob/master/README.md).