**Status de tradução:** Esse artigo é uma tradução de [Core utilities](/index.php/Core_utilities "Core utilities"). Data da última tradução: 2019-10-20\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Core_utilities&diff=0&oldid=584948) na versão em inglês.

Artigos relacionados

*   [Shell de linha de comando](/index.php/Shell_de_linha_de_comando "Shell de linha de comando")
*   [Usuários e grupos](/index.php/Usu%C3%A1rios_e_grupos "Usuários e grupos")
*   [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)")
*   [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")
*   [Recomendações gerais](/index.php/Recomenda%C3%A7%C3%B5es_gerais "Recomendações gerais")

*Utilitários principais* (ou *Core utilities*) são as ferramentas básicas e fundamentais de um sistema [GNU](/index.php/GNU_(Portugu%C3%AAs) "GNU (Português)")/[Linux](/index.php/Linux_(Portugu%C3%AAs) "Linux (Português)"). Este artigo fornece uma visão geral incompleta deles, vincula sua documentação e descreve alternativas úteis. O escopo deste artigo inclui, mas não está limitado a, o [GNU coreutils](https://www.gnu.org/software/coreutils/coreutils.html). A maioria dos utilitários principais é ferramenta tradicional [Unix](https://en.wikipedia.org/wiki/pt:Unix "wikipedia:pt:Unix") (veja [Heirloom](/index.php/Heirloom "Heirloom")) e muitos foram padronizados pela [POSIX](https://en.wikipedia.org/wiki/pt:POSIX "wikipedia:pt:POSIX"), mas foram desenvolvidos para fornecer mais recursos.

A maioria das interfaces de linha de comando está principalmente documentada em [páginas man](/index.php/P%C3%A1ginas_man "Páginas man"), utilitários pelo [Projeto GNU](/index.php/Projeto_GNU "Projeto GNU") estão documentados em [manual info](/index.php/Manual_info "Manual info"), alguns [shells](/index.php/Shell_(Portugu%C3%AAs) "Shell (Português)") fornecem um `help` comando para comandos embutidos [shell](/index.php/Shell_(Portugu%C3%AAs) "Shell (Português)"). Além disso, a maioria dos utilitários imprime seu uso quando executado com o sinalizador `--help`.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Essenciais](#Essenciais)
    *   [1.1 Prevenindo perda de dados](#Prevenindo_perda_de_dados)
*   [2 Não essenciais](#Não_essenciais)
*   [3 Alternativas](#Alternativas)
    *   [3.1 Alternativas ao cp](#Alternativas_ao_cp)
    *   [3.2 ls alternatives](#ls_alternatives)
    *   [3.3 Alternativas ao find](#Alternativas_ao_find)
    *   [3.4 Alternativas ao diff](#Alternativas_ao_diff)
    *   [3.5 Alternativas ao grep](#Alternativas_ao_grep)
        *   [3.5.1 Pesquisadores de código](#Pesquisadores_de_código)
    *   [3.6 Filtros interativos](#Filtros_interativos)
*   [4 Veja também](#Veja_também)

## Essenciais

A tabela a seguir lista alguns utilitários importantes com os quais os usuários do Arch Linux devem estar familiarizados. Veja também [intro(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/intro.1).

| Pacote | Utilitário | Descrição | Documentação | Alternativas |
| embutido no shell | cd | muda o diretório | [cd(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cd.1p) |
| GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) | ls | lista o diretório | [ls(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ls.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/ls-invocation.html) | [exa](https://www.archlinux.org/packages/?name=exa), [lsd](https://www.archlinux.org/packages/?name=lsd), [tree](https://www.archlinux.org/packages/?name=tree) |
| cat | concatena para stdout | [cat(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cat.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/cat-invocation.html) | [tac(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tac.1), [bat](https://www.archlinux.org/packages/?name=bat) |
| mkdir | cria diretório | [mkdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkdir.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/mkdir-invocation.html) |
| rmdir | remove diretório vazio | [rmdir(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rmdir.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/rmdir-invocation.html) |
| rm | remove arquivos ou diretórios | [rm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rm.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/rm-invocation.html) | [shred](/index.php/Shred "Shred") |
| cp | copia arquivos ou diretórios | [cp(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cp.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/cp-invocation.html) |
| mv | move arquivos ou diretórios | [mv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mv.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/mv-invocation.html) |
| ln | cria links absolutos ou simbólicos | [ln(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ln.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/ln-invocation.html) |
| [chown](/index.php/Chown_(Portugu%C3%AAs) "Chown (Português)") | altera dono e grupo de arquivo | [chown(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chown.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/chown-invocation.html) | [chgrp(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chgrp.1) |
| [chmod](/index.php/Chmod_(Portugu%C3%AAs) "Chmod (Português)") | altera permissões de arquivo | [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/chmod-invocation.html) |
| [dd](/index.php/Dd_(Portugu%C3%AAs) "Dd (Português)") | converte e copia um arquivo | [dd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dd.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/dd-invocation.html) |
| df | relata uso de espaço em disco pelos sistemas de arquivos | [df(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/df.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/df-invocation.html) |
| GNU [tar](https://www.archlinux.org/packages/?name=tar) | [tar](/index.php/Tar_(Portugu%C3%AAs) "Tar (Português)") | arquivador tar | [tar(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tar.1), [info](https://www.gnu.org/software/tar/manual/html_chapter/index.html) | [arquivadores](/index.php/Arquivador "Arquivador") |
| GNU [less](https://www.archlinux.org/packages/?name=less) | less | paginador de terminal | [less(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/less.1) | [paginadores de terminal](/index.php/Terminal_pager "Terminal pager") |
| GNU [findutils](https://www.archlinux.org/packages/?name=findutils) | find | pesquisa por arquivos ou diretórios | [find(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/find.1), [info](https://www.gnu.org/software/findutils/manual/html_node/find_html/index.html), [GregsWiki](https://mywiki.wooledge.org/UsingFind "gregswiki:UsingFind") | [#Alternativas ao find](#Alternativas_ao_find) |
| GNU [diffutils](https://www.archlinux.org/packages/?name=diffutils) | diff | compara arquivos linha por linha | [diff(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/diff.1), [info](https://www.gnu.org/software/diffutils/manual/html_node/Invoking-diff.html) | [#Alternativas ao diff](#Alternativas_ao_diff) |
| GNU [grep](https://www.archlinux.org/packages/?name=grep) | grep | imprime linhas correspondendo a um padrão | [grep(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/grep.1), [info](https://www.gnu.org/software/grep/manual/html_node/index.html) | [#Alternativas ao grep](#Alternativas_ao_grep) |
| GNU [sed](https://www.archlinux.org/packages/?name=sed) | sed | editor de fluxo | [sed(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sed.1), [info](https://www.gnu.org/software/sed/manual/html_node/index.html), [uma linha](http://sed.sourceforge.net/sed1line_pt-BR.html) |
| GNU [gawk](https://www.archlinux.org/packages/?name=gawk) | awk | linguagem de varredura e processamento de padrão | [gawk(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gawk.1), [info](https://www.gnu.org/software/gawk/manual/html_node/index.html) | [nawk](https://www.archlinux.org/packages/?name=nawk), [mawk](https://aur.archlinux.org/packages/mawk/) |
| [util-linux](https://www.archlinux.org/packages/?name=util-linux) | [dmesg](https://en.wikipedia.org/wiki/pt:dmesg "wikipedia:pt:dmesg") | exibe ou controla o *ring buffer* do kernel | [dmesg(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dmesg.1) | [journal do systemd](/index.php/Journal_do_systemd "Journal do systemd") |
| [lsblk](/index.php/Lsblk_(Portugu%C3%AAs) "Lsblk (Português)") | lista dispositivos de bloco | [lsblk(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lsblk.8) |
| [mount](/index.php/Mount "Mount") | monta um sistema de arquivos | [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) |
| [umount](/index.php/Umount "Umount") | desmonta um sistema de arquivos | [umount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/umount.8) |
| [su](/index.php/Su "Su") | substitui o usuário | [su(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/su.1) | [sudo](/index.php/Sudo "Sudo") |
| kill | encerra um processo | [kill(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/kill.1) | [pkill(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pkill.1), [killall(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/killall.1) |
| [procps-ng](https://www.archlinux.org/packages/?name=procps-ng) | pgrep | procura por processos por nome ou atributos | [pgrep(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pgrep.1) | [pidof(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pidof.1) |
| ps | mostra informações sobre processos | [ps(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ps.1) | [top(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/top.1), [htop](https://www.archlinux.org/packages/?name=htop) |
| free | exibe a quantidade de memória livre e usada | [free(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/free.1) |

### Prevenindo perda de dados

Os redirecionamentos `rm`, `mv`, `cp` e shell excluem ou sobrescrevem arquivos sem perguntar. `rm`, `mv` e `cp` possuem suporte ao sinalizador `-i` para avisar o usuário antes de cada remoção/sobrescrita. Alguns usuários gostam de ativar o sinalizador `-i` por padrão usando [aliases](/index.php/Alias "Alias"). Depender dessas opções de shell pode ser perigoso porque você se acostuma a elas, resultando em perda de dados em potencial quando você usa outro sistema ou usuário que não as possui. A melhor maneira de evitar a perda de dados é criar [backups](/index.php/Backup_(Portugu%C3%AAs) "Backup (Português)").

## Não essenciais

Essa tabela lista utilitários principais que geralmente são úteis.

| Pacote | Utilitário | Descrição | Documentação | Alternativas |
| embutido no shell | alias | define ou exibe aliases | [alias(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/alias.1p) |
| type | imprime o tipo de um comando | [type(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/type.1p) | [which(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/which.1) |
| time | obtenha o tempo de um comando | [time(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/time.1p) |
| GNU [coreutils](https://www.archlinux.org/packages/?name=coreutils) | tee | lê a stdin e escreve para stdout e arquivos | [tee(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tee.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/tee-invocation.html) |
| mktemp | cria um arquivo ou diretório temporário | [mktemp(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mktemp.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/mktemp-invocation.html) |
| cut | imprime partes selecionadas de linhas | [cut(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cut.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/cut-invocation.html) |
| tr | traduz ou exclui caracteres | [tr(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tr.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/tr-invocation.html) |
| od | despeja arquivos em octal e outros formatos | [od(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/od.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/od-invocation.html) | [hexdump(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hexdump.1), [vim](/index.php/Vim "Vim")'s [xxd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xxd.1) |
| sort | ordena linhas | [sort(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sort.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/sort-invocation.html) |
| uniq | relata ou omite linhas repetidas | [uniq(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/uniq.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/uniq-invocation.html) |
| comm | compara dois arquivos ordenados linha por linha | [comm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/comm.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/comm-invocation.html) |
| head | imprime a parte inicial dos arquivos | [head(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/head.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/head-invocation.html) |
| tail | imprime a parte final dos arquivos, ou segue arquivos | [tail(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tail.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/tail-invocation.html) |
| wc | imprime contagem de nova linha, palavra e byte | [wc(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wc.1), [info](https://www.gnu.org/software/coreutils/manual/html_node/wc-invocation.html) |
| GNU [binutils](https://www.archlinux.org/packages/?name=binutils) | strings | emite caracteres imprimíveis em arquivos binários | [strings(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/strings.1), [info](https://sourceware.org/binutils/docs/binutils/strings.html) |
| GNU [glibc](https://www.archlinux.org/packages/?name=glibc) | iconv | converte codificações de caracteres | [iconv(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iconv.1) | [recode](https://www.archlinux.org/packages/?name=recode) |
| [file](https://www.archlinux.org/packages/?name=file) | file | advinha o tipo de arquivo | [file(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/file.1) |

O pacote [moreutils](https://www.archlinux.org/packages/?name=moreutils) fornece ferramentas úteis como o [sponge(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sponge.1) que não estão presentes no GNU coreutils.

## Alternativas

Utilitários principais alternativos são fornecidos por [BusyBox](/index.php/BusyBox "BusyBox"), o [Heirloom Toolchest](/index.php/Heirloom "Heirloom"), [9base](https://www.archlinux.org/packages/?name=9base), [sbase-git](https://aur.archlinux.org/packages/sbase-git/) e [ubase-git](https://aur.archlinux.org/packages/ubase-git/).

### Alternativas ao cp

O uso de [rsync como uma alternativa a cp/mv](/index.php/Rsync#As_cp/mv_alternative "Rsync") permite retomar uma transferência com falha, mostrar o status da transferência, pular arquivos já existentes e certificar-se da integridade dos arquivos de destino usando somas de verificação.

### ls alternatives

*   **lsd** — Um *ls* moderno com muitas cores bonitas e ícones legais. Escrito em Rust.

	[https://github.com/Peltoche/lsd](https://github.com/Peltoche/lsd) || [lsd](https://www.archlinux.org/packages/?name=lsd)

### Alternativas ao find

*   **fd** — Alternativa simples, rápida e amigável ao find. Ignora arquivos ocultos e inseridos em `.gitignore` por padrão.

	[https://github.com/sharkdp/fd](https://github.com/sharkdp/fd) || [fd](https://www.archlinux.org/packages/?name=fd)

*   **fuzzy-find** — Completação aproximada para localizar arquivos.

	[https://github.com/silentbicycle/ff](https://github.com/silentbicycle/ff) || [ff-git](https://aur.archlinux.org/packages/ff-git/)

*   **[mlocate](/index.php/Mlocate_(Portugu%C3%AAs) "Mlocate (Português)")** — Implementação de fusão entre locate e updatedb.

	[https://pagure.io/mlocate](https://pagure.io/mlocate) || [mlocate](https://www.archlinux.org/packages/?name=mlocate)

Para pesquisadores gráficos de arquivo, veja [List of applications/Utilities#File searching](/index.php/List_of_applications/Utilities#File_searching "List of applications/Utilities").

### Alternativas ao diff

Enquanto [diffutils](https://www.archlinux.org/packages/?name=diffutils) não oferece suporte a diferenciação por palavras, vários outros programas oferecem:

*   [git](/index.php/Git "Git") diff pode fazer um *diff* de palavras com `--color-words`, usando `--no-index` ele também pode ser usado para arquivos fora de árvores de trabalho Git.
*   **dwdiff** — Um front-end diferenciador de palavras para o programa dif; tem suporte a cores.

	[https://os.ghalkes.nl/dwdiff.html](https://os.ghalkes.nl/dwdiff.html) || [dwdiff](https://www.archlinux.org/packages/?name=dwdiff)

*   **GNU wdiff** — Uma implementação de diferenciação de palavras do GNU diff; não possui suporte a cores.

	[https://www.gnu.org/software/wdiff/](https://www.gnu.org/software/wdiff/) || [wdiff](https://www.archlinux.org/packages/?name=wdiff)

*   **cwdiff** — Um interfaceador do GNU wdiff que coloriza a saída.

	[https://github.com/junghans/cwdiff](https://github.com/junghans/cwdiff) || [cwdiff](https://aur.archlinux.org/packages/cwdiff/), [cwdiff-git](https://aur.archlinux.org/packages/cwdiff-git/)

*   **icdiff** — Uma ferramenta diff colorida escrita em Python. "Improved color diff" serve para complementar o uso normal do diff.

	[https://github.com/jeffkaufman/icdiff](https://github.com/jeffkaufman/icdiff) || [icdiff](https://aur.archlinux.org/packages/icdiff/),[icdiff-git](https://aur.archlinux.org/packages/icdiff-git/)

Veja também [List of applications/Utilities#Comparison, diff, merge](/index.php/List_of_applications/Utilities#Comparison,_diff,_merge "List of applications/Utilities").

### Alternativas ao grep

*   **mgrep** — Um grep multilinha.

	[https://sourceforge.net/projects/multiline-grep/](https://sourceforge.net/projects/multiline-grep/) || [mgrep](https://aur.archlinux.org/packages/mgrep/)

#### Pesquisadores de código

As três ferramentas a seguir visam substituir o grep na pesquisa de código. Elas fazem pesquisa recursiva por padrão, ignoram arquivos vinários e respeitam o `.gitignore`.

*   **ack** — Um substituto do grep baseado em Perl, tendo com alvo programadores com grandes árvores de código-fonte heretogêneo.

	[https://beyondgrep.com/](https://beyondgrep.com/) || [ack](https://www.archlinux.org/packages/?name=ack)

*   **ripgrep (rg)** — Uma ferramenta de pesquisa que combina a usabilidade do ag com a velocidade bruta do grep.

	[https://github.com/BurntSushi/ripgrep](https://github.com/BurntSushi/ripgrep) || [ripgrep](https://www.archlinux.org/packages/?name=ripgrep)

*   **The Silver Searcher (ag)** — Ferramenta de pesquisa de código similar ao Ack, porém mais rápido.

	[https://github.com/ggreer/the_silver_searcher](https://github.com/ggreer/the_silver_searcher) || [the_silver_searcher](https://www.archlinux.org/packages/?name=the_silver_searcher)

### Filtros interativos

*   **fzf** — Localizador aproximado de linha de comando de propósito geral, movido a find por padrão.

	[https://github.com/junegunn/fzf](https://github.com/junegunn/fzf) || [fzf](https://www.archlinux.org/packages/?name=fzf), [fzf-git](https://aur.archlinux.org/packages/fzf-git/)

*   **fzy** — Um seletor de texto aproximado rápido e simples com um algoritmo avançado de pontuação.

	[https://github.com/jhawthorn/fzy](https://github.com/jhawthorn/fzy) || [fzy](https://www.archlinux.org/packages/?name=fzy), [fzy-git](https://aur.archlinux.org/packages/fzy-git/)

*   **peco** — Ferramenta simplista de filtragem interativa.

	[https://github.com/peco/peco](https://github.com/peco/peco) || [peco](https://aur.archlinux.org/packages/peco/), [peco-git](https://aur.archlinux.org/packages/peco-git/)

*   **percol** — Adiciona o sabor da filtragem interativa ao conceito tradicional de pipe do shell do UNIX.

	[https://github.com/mooz/percol](https://github.com/mooz/percol) || [percol](https://www.archlinux.org/packages/?name=percol), [percol-git](https://aur.archlinux.org/packages/percol-git/)

## Veja também

*   [Documentação do GNU Coreutils](https://www.gnu.org/software/coreutils/manual/coreutils.html)
*   [Utilitários do POSIX](http://pubs.opengroup.org/onlinepubs/9699919799/idx/utilities.html)