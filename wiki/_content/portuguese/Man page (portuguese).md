**Status de tradução:** Esse artigo é uma tradução de [Man page](/index.php/Man_page "Man page"). Data da última tradução: 2019-10-06\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Man_page&diff=0&oldid=587126) na versão em inglês.

Artigos relacionados

*   [Color output in console#man](/index.php/Color_output_in_console#man "Color output in console")

[man pages](https://en.wikipedia.org/wiki/Man_page "wikipedia:Man page") — abreviação para "páginas de manual" — são a forma de documentação que está disponível na maioria dos sistemas operacionais tipo UNIX, incluindo o Arch Linux. O comando usado para exibi-los é `man`.

Apesar de seu escopo, páginas man são projetadas para serem documentos autocontidos, consequentemente limitando-as a fazer referência a outras páginas man ao discutir assuntos relatados. Esse é um contraste nítido com os [documentos info](/index.php/Manual_info "Manual info") compatíveis com hiperlinks, a tentativa do GNU de substituir o formato tradicional de página man.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Acessando páginas man](#Acessando_páginas_man)
*   [3 Formato](#Formato)
*   [4 Pesquisando por manuais](#Pesquisando_por_manuais)
    *   [4.1 Compilando o cache de manuais com mandb](#Compilando_o_cache_de_manuais_com_mandb)
    *   [4.2 Pesquisando por expressões nos manuais](#Pesquisando_por_expressões_nos_manuais)
*   [5 Obtendo descrições de uma linha com whatis](#Obtendo_descrições_de_uma_linha_com_whatis)
*   [6 Largura de página](#Largura_de_página)
*   [7 Lendo páginas man locais](#Lendo_páginas_man_locais)
    *   [7.1 Aplicativos de visualização](#Aplicativos_de_visualização)
    *   [7.2 Conversão para HTML](#Conversão_para_HTML)
        *   [7.2.1 mandoc](#mandoc)
        *   [7.2.2 man2html](#man2html)
        *   [7.2.3 man -H](#man_-H)
        *   [7.2.4 roffit](#roffit)
    *   [7.3 Conversão para PDF](#Conversão_para_PDF)
*   [8 Páginas man online](#Páginas_man_online)
*   [9 Páginas man notáveis](#Páginas_man_notáveis)
*   [10 Veja também](#Veja_também)

## Instalação

[man-db](https://www.archlinux.org/packages/?name=man-db) implementa *man* no Arch Linux, e o [less](/index.php/Utilit%C3%A1rios_principais#Essenciais "Utilitários principais") é o paginador padrão usado com *man*.

[man-pages](https://www.archlinux.org/packages/?name=man-pages) fornece as páginas man do Linux.

## Acessando páginas man

Para ler uma página man, basta digitar:

```
$ man *nome_página*

```

Manuais são ordenados em diversas [seções](https://en.wikipedia.org/wiki/Man_page#Manual_sections "wikipedia:Man page"). Para uma listagem completa, veja a seção intitulada "Sections of the manual pages" no [man-pages(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/man-pages.7).

Páginas man geralmente são referenciadas por seu nome, seguido do número de sua seção em parênteses. Geralmente há múltiplas páginas man com o mesmo nome, tal como [man(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/man.1) e [man(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/man.7). Neste caso, forneça ao man o número da seção seguido pelo nome da página man. Por exemplo:

```
$ man 5 passwd

```

para ler a página man sobre `/etc/passwd`, em vez do utilitário `passwd`.

## Formato

Todas as páginas man seguem um formato razoavelmente padronizado, o que ajuda a navegá-las. Veja a seção intitulada "Sections within a manual page" em [man-pages(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/man-pages.7).

## Pesquisando por manuais

Apesar do utilitário `man` permitir que usuários exibam páginas man, e pesquisem seu conteúdo via *less*, um problema surge quando não se sabe o nome exato da página de manual desejada em primeiro lugar! Por sorte, as opções `-k` ou `--apropos` podem ser usadas para pesquisar pelas descrições de página de manual por ocorrências de uma palavra-chave dada.

### Compilando o cache de manuais com mandb

O recurso de pesquisa é fornecido por um cache dedicado, do contrário todas as pesquisa retornariam resultado *nada apropriado*. Por padrão, manutenção daquele cache é lidado por `man-db.service`, o qual periodicamente é ativado por `man-db.timer`. Você pode manualmente (re)gerar o cache ou atualizá-lo executando:

```
# mandb

```

### Pesquisando por expressões nos manuais

Por exemplo, para pesquisar por páginas man relacionadas a "password":

```
$ man -k password

```

ou:

```
$ man --apropos password

```

Isso é equivalente a chamar o comando `apropos`:

```
$ apropos password

```

A palavra-chave dada é interpretada como uma expressão regular por padrão.

Se você deseja fazer uma pesquisa mais profunda correspondendo palavras-chave encontradas em todos os artigos, você pode usar a opção `-K`:

```
$ man -K password

```

## Obtendo descrições de uma linha com whatis

Descrições de uma linha podem ser exibidas usando o comando `whatis`. Por exemplo, para uma descrição breve das seções de página man sobre `ls`, digite:

 `$ whatis ls` 
```
ls (1p)              - list directory contents
ls (1)               - list directory contents

```

## Largura de página

A largura de páginas man é controlada pela variável de ambiente `MANWIDTH`.

Se o número de colunas no terminal é pequeno demais (ex.: a largura da janela é estreita), as quebras de linha ficarão erradas. Isso pode ser bem incômodo para ler. Você pode corrigir isso definindo MANWIDTH na invocação de `man`. Com `Bash`, isso seria:

 `~/.bashrc` 
```
man() {
    local width=$(tput cols)
    [ $width -gt $MANWIDTH ] && width=$MANWIDTH
    env MANWIDTH=$width \
    man "$@"
}

```

## Lendo páginas man locais

Em vez da interface padrão, o uso de navegadores como [lynx](https://www.archlinux.org/packages/?name=lynx) e [Firefox](/index.php/Firefox "Firefox") para visualizar páginas man permite que os usuários colham o principal benefício de texto hiperlink das páginas info. As alternativas incluem o seguinte:

### Aplicativos de visualização

*   **GNOME Help** — Visualização de ajuda para o [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"). Ele pode mostrar páginas man via `yelp man:<nome>` ou a combinação de teclas não documentada `CTRL+L` a partir de uma janela existente.

	[https://wiki.gnome.org/Apps/Yelp](https://wiki.gnome.org/Apps/Yelp) || [yelp](https://www.archlinux.org/packages/?name=yelp)

*   **KHelpCenter** — Aplicativo para mostrar documentação dos aplicativos do [KDE](/index.php/KDE_(Portugu%C3%AAs) "KDE (Português)"). Páginas man estão em *Páginas de manual do UNIX* ou executando `khelpcenter man:<nome>`.

	[https://userbase.kde.org/KHelpCenter](https://userbase.kde.org/KHelpCenter) || [khelpcenter](https://www.archlinux.org/packages/?name=khelpcenter)

*   **[Konqueror](https://en.wikipedia.org/wiki/pt:Konqueror "wikipedia:pt:Konqueror")** — Gerenciador de arquivos e navegador web do KDE. Ele pode mostrar páginas man via `man:<nome>`.

	[https://konqueror.org/](https://konqueror.org/) || [konqueror](https://www.archlinux.org/packages/?name=konqueror)

*   **xman** — Fornece um visual categorizado em páginas man.

	[https://xorg.freedesktop.org/](https://xorg.freedesktop.org/) || [xorg-xman](https://www.archlinux.org/packages/?name=xorg-xman)

### Conversão para HTML

#### mandoc

Instale o pacote [mandoc](https://aur.archlinux.org/packages/mandoc/). Para converter uma página, por exemplo `free(1)`:

```
$ mandoc -Thtml -Ostyle=style.css /usr/share/man/man1/free.1.gz > free.html

```

Agora, abra o arquivo chamado `free.html` em seu navegador favorito.

#### man2html

Primeiro, instale [man2html](https://www.archlinux.org/packages/?name=man2html) dos repositórios oficiais.

Agora, converta uma página man:

```
$ man free | man2html -compress -cgiurl man$section/$title.$section$subsection.html > ~/man/free.html

```

Outro uso para `man2html` é exportar para texto não tratado, no formato de impressão:

```
$ man free | man2html -bare > ~/free.txt

```

#### man -H

A implementação GNU do man nos repositórios Arch também possuem a habilidade de fazer isso por conta própria:

```
$ man -H free

```

Isso vai ler sua [variável de ambiente](/index.php/Vari%C3%A1vel_de_ambiente "Variável de ambiente") `BROWSER` para determinar o navegador. Você pode sobrepor isso passando o executável para a opção `-H`.

#### roffit

Primeiro, instale [roffit](https://aur.archlinux.org/packages/roffit/) do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)").

Para converter uma página man:

```
$ gunzip -c /usr/share/man/man1/free.1.gz | roffit > free.html

```

### Conversão para PDF

Páginas man sempre foram imprimíveis: elas são escritas em troff, que é fundamentalmente uma linguagem de formatação de texto. Se você tiver o [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) instalado, você pode converter uma página man para PDF usando `man -t <página-man> | ps2pdf - <pdf>`.

Ressalvas: Fontes são geralmente limitadas a Times em tamanhos fixos. Não há hyperlinks. Algumas páginas man foram projetadas especificamente para ver no terminal e não ficarão bem na forma de PS ou PDF.

## Páginas man online

Há vários bancos de dado online de páginas man, incluindo:

*   [man7.org](http://man7.org/linux/man-pages/index.html). Upstream do [man-pages](https://www.archlinux.org/packages/?name=man-pages) do Arch Linux.
*   [Páginas man do Arch Linux](https://jlk.fjfi.cvut.cz/arch/manpages/). Usado para links do wiki.
*   [manned.org](https://manned.org/) — coleção de várias distribuições Linux, BSD, etc. com múltiplas versões de pacotes
*   [linux.die.net](https://linux.die.net/man/)
*   [man.cx](https://man.cx/)
*   [Páginas man do Debian](https://manpages.debian.org/)
*   [Páginas man do Ubuntu](http://manpages.ubuntu.com/)
*   [Páginas man do DragonFlyBSD](https://leaf.dragonflybsd.org/cgi/web-man)
*   [Páginas man do FreeBSD](https://www.freebsd.org/cgi/man.cgi)
*   [Páginas man do NetBSD](http://netbsd.gw.com/cgi-bin/man-cgi)
*   [Páginas man do OpenBSD](https://man.openbsd.org)
*   [Páginas man do Mac OS X](https://developer.apple.com/documentation/Darwin/Reference/ManPages/index.html)
*   [Manual do Plan 9 — Volume 1](http://man.cat-v.org/plan_9/)
*   [Manual do Inferno — Volume 1](http://man.cat-v.org/inferno/)
*   [Páginas man do Storage Foundation](http://sfdoccentral.symantec.com/sf/5.0MP3/linux/manpages/index.html)
*   [Repositório de páginas man do UNIX and Linux Forums](https://www.unix.com/man-page/OpenSolaris/1/man/)

**Dica:** Você pode usar o [!Bang](https://duckduckgo.com/bang.html) `!archman` do DuckDuckGo para pesquisar pelas [páginas man do Arch Linux](https://jlk.fjfi.cvut.cz/arch/manpages/) diretamente

**Atenção:** Algumas distribuições fornecem páginas man alteradas ou desatualizadas que se diferem daquelas fornecidas pelo Arch. Exercite o cuidado ao usar páginas man online.

## Páginas man notáveis

Aqui está uma lista não exaustiva de páginas dignas de nota que podem lhe ajudar a entender muitas coisas em profundidade. Alguns deles podem servir como uma boa referência (como a tabela ASCII).

*   [ascii(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ascii.7)
*   [boot(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/boot.7)
*   [charsets(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/charsets.7)
*   [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1)
*   [credentials(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/credentials.7)
*   [fstab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fstab.5)
*   [hier(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hier.7)
*   [systemd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.1)
*   [locale(1p)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.1p), [locale(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.5), [locale(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.7)
*   [printf(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/printf.3)
*   [proc(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/proc.5)
*   [regex(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/regex.7)
*   [signal(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/signal.7)
*   [term(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/term.5), [term(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/term.7)
*   [termcap(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/termcap.5)
*   [terminfo(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/terminfo.5)
*   [utf-8(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/utf-8.7)

De forma mais geral, dê uma olhada nas [páginas de categoria 7 (miscelânea)](http://man7.org/linux/man-pages/dir_section_7.html):

```
$ man -s 7 -k ".*" 

```

Páginas específicas do Arch Linux:

*   [archlinux(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/archlinux.7)
*   [mkinitcpio(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.8)
*   [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8)
*   [pacman-key(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman-key.8)
*   [pacman.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.conf.5)

## Veja também

*   [man page - artigo wiki do Gentoo](https://wiki.gentoo.org/wiki/Man_page)
*   [Escrevendo o bom manual com pod2man](https://linuxtidbits.wordpress.com/2013/08/21/wtfm-write-the-fine-manual-with-pod2man-text-converter/)