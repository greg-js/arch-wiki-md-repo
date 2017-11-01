Artigos relacionados

*   [Color output in console#man](/index.php/Color_output_in_console#man "Color output in console")

**Páginas man** — abreviação para "páginas de manual" — são a forma de documentação que está disponível na maioria dos sistemas operacionais tipo UNIX, incluindo o Arch Linux. O comando usado para exibi-los é `man`.

Apesar de seu escopo, páginas man são projetadas para serem documentos autocontidos, consequentemente limitando-as a fazer referência a outras páginas man ao discutir assuntos relatados. Esse é um contraste nítido com os arquivos info compatíveis com hiperlinks, a tentativa do GNU de substituir o formato tradicional de página man.

[man-db](https://www.archlinux.org/packages/?name=man-db) implementa *man* no Arch Linux, e o [less](/index.php/Core_utilities#less "Core utilities") é o paginador padrão usado com *man*.

## Contents

*   [1 Acessando páginas man](#Acessando_p.C3.A1ginas_man)
*   [2 Formato](#Formato)
*   [3 Pesquisando por manuais](#Pesquisando_por_manuais)
*   [4 Largura de página](#Largura_de_p.C3.A1gina)
*   [5 Lendo páginas man locais](#Lendo_p.C3.A1ginas_man_locais)
    *   [5.1 Convertendo para HTML legível com navegador](#Convertendo_para_HTML_leg.C3.ADvel_com_navegador)
        *   [5.1.1 mdocml](#mdocml)
        *   [5.1.2 man2html](#man2html)
        *   [5.1.3 man -H](#man_-H)
        *   [5.1.4 roffit](#roffit)
    *   [5.2 Convertendo para PDF](#Convertendo_para_PDF)
*   [6 Páginas man online](#P.C3.A1ginas_man_online)
*   [7 Páginas man notáveis](#P.C3.A1ginas_man_not.C3.A1veis)
*   [8 Veja também](#Veja_tamb.C3.A9m)

## Acessando páginas man

Para ler uma página man, basta digitar:

```
$ man *page_name*

```

Manuais são ordenados em diversas seções. Para uma listagem completa, veja a seção intitulada "Sections of the manual pages" no [man-pages(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/man-pages.7).

Páginas man geralmente são referenciadas por seu nome, seguido do número de sua seção em parênteses. Geralmente há múltiplas páginas man com o mesmo nome, tal como [man(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/man.1) e [man(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/man.7). Neste caso, forneça ao man o número da seção seguido pelo nome da página man. Por exemplo:

```
$ man 5 passwd

```

para ler a página man sobre `/etc/passwd`, em vez do utilitário `passwd`.

Descrições de uma linha podem ser exibidas usando o comando `whatis`. Por exemplo, para uma descrição breve das seções de página man sobre `ls`, digite:

 `$ whatis ls` 
```
ls (1p)              - list directory contents
ls (1)               - list directory contents

```

## Formato

Todas as páginas man seguem um formato razoavelmente padronizado, o que ajuda a navegá-las. Veja a seção intitulada "Sections within a manual page" em [man-pages(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/man-pages.7).

## Pesquisando por manuais

Apesar do utilitário `man` permitir que usuários exibam páginas man, e pesquisem seu conteúdo via *less*, um problema surge quando não se sabe o nome exato da página de manual desejada em primeiro lugar! Por sorte, as opções `-k` ou `--apropos` podem ser usadas para pesquisar pelas descrições de página de manual por ocorrências de uma palavra-chave dada.

O recurso de pesquisa é fornecido por um cache dedicado. Por padrão, você não pode ter qualquer cache compilado e todas suas pesquisa lhe darão *nenhum resultado apropriado*. Você pode gerar o cache ou atualizá-lo executando

```
# mandb

```

Você deve executá-lo toda vez que uma nova página man é instalada.

Agora, você pode começar sua pesquisa. Por exemplo, para pesquisar por páginas man relacionadas a "password":

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

*   Usuários do [KDE](/index.php/KDE "KDE") podem ler páginas man com
    *   Konqueror usando `man:<nome>`.
    *   KHelpCenter ([khelpcenter](https://www.archlinux.org/packages/?name=khelpcenter)) em "UNIX manual pages" ou executando `khelpcenter man:<nome>`.
*   [xorg-xman](https://www.archlinux.org/packages/?name=xorg-xman) fornece uma visão categorizada em páginas man no [X](/index.php/X "X").
*   [yelp](https://www.archlinux.org/packages/?name=yelp), o navegador de ajuda do [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"), pode ser usado via `yelp man:<nome>`.

### Convertendo para HTML legível com navegador

#### mdocml

Instale [mdocml](https://aur.archlinux.org/packages/mdocml/) do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"). Para converter uma página, por exemplo `free(1)`:

```
$ gunzip -c /usr/share/man/man1/free.1.gz | mandoc -Thtml -Ostyle=style.css 1> free.html

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

Isso vai ler sua [variável de ambiente](/index.php/Environment_variable "Environment variable") `BROWSER` para determinar o navegador. Você pode sobrepor isso passando o executável para a opção `-H`.

#### roffit

Primeiro, instale [roffit](https://aur.archlinux.org/packages/roffit/) do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)").

Para converter uma página man:

```
$ gunzip -c /usr/share/man/man1/free.1.gz | roffit > free.html

```

### Convertendo para PDF

Páginas man sempre foram imprimíveis: elas são escritas em troff, que é fundamentalmente uma linguagem de formatação de texto. Se você tiver o ghostscript instalado, a conversão de uma página man para PDF é realmente bem fácil: `man -t <manpage> | ps2pdf - <pdf>`. [Essa pesquisa de imagens no Google](https://www.google.com.br/search?q=manpage+pdf+troff&source=lnms&tbm=isch) deve lhe dar uma ideia do que o resultado se parece com; pode não ser do gosto de todas as pessoas.

Ressalvas: Fontes são geralmente limitadas a Times em tamanhos fixos. Não há hyperlinks. Algumas páginas man foram projetadas especificamente para ver no terminal e não ficarão bem na forma de PS ou PDF.

## Páginas man online

Há vários bancos de dado online de páginas man, incluindo:

*   [Man7.org.](http://man7.org/linux/man-pages/index.html) Upstream do [man-pages](https://www.archlinux.org/packages/?name=man-pages) do Arch Linux.
*   [*Páginas man do Arch Linux*](https://manned.org/pkg/arch)
*   [*Páginas man do Debian GNU/Linux*](http://manpages.debian.net/)
*   [*Páginas man do DragonFlyBSD*](http://leaf.dragonflybsd.org/cgi/web-man)
*   [*Páginas man hypertext do FreeBSD*](http://www.freebsd.org/cgi/man.cgi)
*   [*Páginas man do Linux e Solaris 10*](http://www.manpages.spotlynx.com/)
*   [*Páginas man do Linux no die.net*](http://linux.die.net/man/)
*   [*Páginas man do NetBSD*](http://netbsd.gw.com/cgi-bin/man-cgi)
*   [*Páginas man do Mac OS X*](http://developer.apple.com/documentation/Darwin/Reference/ManPages/index.html)
*   [*Páginas man online do UNIX*](http://unixhelp.ed.ac.uk/alphabetical/index.html)
*   [*Páginas de manual do OpenBSD*](http://www.openbsd.org/cgi-bin/man.cgi)
*   [*Manual do Plan 9 — Volume 1*](http://man.cat-v.org/plan_9/)
*   [*Manual do Inferno — Volume 1*](http://man.cat-v.org/inferno/)
*   [*Páginas man do Storage Foundation*](http://sfdoccentral.symantec.com/sf/5.0MP3/linux/manpages/index.html)
*   [*O repositório de páginas man do UNIX and Linux Forums*](http://www.unix.com/man-page/OpenSolaris/1/man/)
*   [*Repositório de páginas man do Ubuntu*](http://manpages.ubuntu.com/)

**Atenção:** Algumas distribuições fornecem páginas man alteradas ou desatualizadas que se diferem daquelas fornecidas pelo Arch. Exercite o cuidado ao usar páginas man online.

## Páginas man notáveis

Aqui está uma lista não exaustiva de páginas dignas de nota que podem lhe ajudar a entender muitas coisas em profundidade. Alguns deles podem servir como uma boa referência (como a tabela ASCII).

*   [ascii(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ascii.7)
*   [boot(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/boot.7)
*   [charsets(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/charsets.7)
*   [chmod(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1)
*   [credentials(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/credentials.7)
*   [fstab(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/fstab.5)
*   [hier(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/hier.7)
*   [systemd(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.1)
*   [locale(1p)](http://jlk.fjfi.cvut.cz/arch/manpages/man/locale.1p), [locale(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/locale.5), [locale(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/locale.7)
*   [printf(3)](http://jlk.fjfi.cvut.cz/arch/manpages/man/printf.3)
*   [proc(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/proc.5)
*   [regex(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/regex.7)
*   [signal(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/signal.7)
*   [term(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/term.5), [term(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/term.7)
*   [termcap(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/termcap.5)
*   [terminfo(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/terminfo.5)
*   [utf-8(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/utf-8.7)

De forma mais geral, dê uma olhada nas páginas de categoria 7:

```
$ man -s 7 -k ".*" 

```

Páginas específicas do Arch Linux:

*   [archlinux(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/archlinux.7)
*   [mkinitcpio(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.8)
*   [pacman(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8)
*   [pacman-key(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman-key.8)
*   [pacman.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.conf.5)

## Veja também

*   [man page - artigo wiki do Gentoo](https://wiki.gentoo.org/wiki/Man_page)
*   [Escrevendo o bom manual com pod2man](https://linuxtidbits.wordpress.com/2013/08/21/wtfm-write-the-fine-manual-with-pod2man-text-converter/)