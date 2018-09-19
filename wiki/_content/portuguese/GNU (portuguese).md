**Status de tradução:** Esse artigo é uma tradução de [GNU](/index.php/GNU "GNU"). Data da última tradução: 2018-09-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=GNU&diff=0&oldid=539208) na versão em inglês.

Artigos relacionados

*   [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)")
*   [Utilitários principais](/index.php/Utilit%C3%A1rios_principais "Utilitários principais")

Do [Wikipédia](https://en.wikipedia.org/wiki/GNU "wikipedia:GNU"):

	GNU é um sistema operacional e uma extensa coleção de softwares de computador. O GNU é composto inteiramente de software livre, a maioria dos quais é licenciada sob a Licença Pública Geral (GPL) do Projeto GNU. O GNU é um acrônimo recursivo para "GNU Não é Unix!".

Porque o kernel do GNU, [Hurd](https://www.gnu.org/s/hurd/hurd.html), não está pronto para produção [[1]](https://www.gnu.org/software/hurd/hurd/status.html), o GNU é normalmente usado com o kernel do Linux. O [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)") é uma distribuição GNU/Linux, usando software GNU como o shell [Bash](/index.php/Bash "Bash"), o GNU coreutils, o conjunto de ferramentas do GNU *(toolchain)* e vários outros utilitários e bibliotecas. Esta página não tenta listar todos os [quase 400](https://www.gnu.org/software/software.html#allgnupkgs) pacotes GNU e apenas destaca alguns.

## Contents

*   [1 Texinfo](#Texinfo)
*   [2 Sistema base](#Sistema_base)
*   [3 Conjunto de ferramentas](#Conjunto_de_ferramentas)
    *   [3.1 Sistema de compilação](#Sistema_de_compila.C3.A7.C3.A3o)
*   [4 Outros softwares](#Outros_softwares)
*   [5 Veja também](#Veja_tamb.C3.A9m)

## Texinfo

O software GNU é documentado usando a sintaxe de composição [Texinfo](https://en.wikipedia.org/wiki/pt:Texinfo "wikipedia:pt:Texinfo"). Você pode visualizar documentos de Informações usando o programa `info`, fornecido pelo pacote [texinfo](https://www.archlinux.org/packages/?name=texinfo), que faz parte do [base](https://www.archlinux.org/groups/x86_64/base/).

Embora a maioria dos softwares GNU também forneça [páginas man](/index.php/P%C3%A1ginas_man "Páginas man"), os documentos de Informações tendem a ser mais abrangentes.

## Sistema base

*   **[GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)")** — GRUB é um gerenciador de boot para o projeto GNU.

	[https://www.gnu.org/software/grub/](https://www.gnu.org/software/grub/) || [grub](https://www.archlinux.org/packages/?name=grub)

*   **[Bash](/index.php/Bash "Bash")** — É um shell compatível com sh que incorpora recursos úteis do Korn shell (ksh) e do C shell (csh).

	[https://www.gnu.org/software/bash/](https://www.gnu.org/software/bash/) || [bash](https://www.archlinux.org/packages/?name=bash)

*   **[Coreutils](/index.php/Coreutils_(Portugu%C3%AAs) "Coreutils (Português)")** — coreutils fornece os utilitários básicos de manipulação de arquivo, shell e texto do sistema operacional GNU.

	[https://www.gnu.org/software/coreutils/](https://www.gnu.org/software/coreutils/) || [coreutils](https://www.archlinux.org/packages/?name=coreutils)

*   **[gzip](https://en.wikipedia.org/wiki/pt:gzip "wikipedia:pt:gzip")** — gzip é tanto um formato de arquivo quanto um aplicativo de software para compressão e descompressão.

	[https://www.gnu.org/software/gzip/](https://www.gnu.org/software/gzip/) || [gzip](https://www.archlinux.org/packages/?name=gzip)

*   **[tar](/index.php/Tar_(Portugu%C3%AAs) "Tar (Português)")** — It provides the ability to create or decompress tar archives, as well as various other kinds of manipulation.

	[https://www.gnu.org/software/tar/](https://www.gnu.org/software/tar/) || [tar](https://www.archlinux.org/packages/?name=tar)

## Conjunto de ferramentas

A maioria das ferramentas do [conjunto de ferrtamentas do GNU](https://en.wikipedia.org/wiki/GNU_toolchain "wikipedia:GNU toolchain") *(toolchain)* estão no grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), exceto *glibc* que está no [base](https://www.archlinux.org/groups/x86_64/base/) e GDB que está em nenhum grupo.

*   **[GNU make](https://en.wikipedia.org/wiki/pt:Make "wikipedia:pt:Make")** — Utilitário GNU make para manter grupos de programas.

	[http://www.gnu.org/software/make](http://www.gnu.org/software/make) || [make](https://www.archlinux.org/packages/?name=make)

*   **[GCC](/index.php/GCC "GCC")** — O GNU Compiler Collection - frontends para C e C++.

	[https://gcc.gnu.org/](https://gcc.gnu.org/) || [gcc](https://www.archlinux.org/packages/?name=gcc)

*   **[glibc](https://en.wikipedia.org/wiki/pt:GNU_C_Library "wikipedia:pt:GNU C Library")** — a implementação do GNU da biblioteca C.

	[https://www.gnu.org/software/libc/](https://www.gnu.org/software/libc/) || [glibc](https://www.archlinux.org/packages/?name=glibc) (parte do [base](https://www.archlinux.org/groups/x86_64/base/))

*   **[GNU Binutils](https://en.wikipedia.org/wiki/GNU_Binutils "wikipedia:GNU Binutils")** — Um conjunto de programas para montar e manipular arquivos binários e arquivos objeto. Inclui [ld](https://en.wikipedia.org/wiki/GNU_linker "wikipedia:GNU linker").

	[https://www.gnu.org/software/binutils/](https://www.gnu.org/software/binutils/) || [binutils](https://www.archlinux.org/packages/?name=binutils)

*   **[GNU bison](https://en.wikipedia.org/wiki/GNU_bison "wikipedia:GNU bison")** — O gerador de analisador de propósito geral do GNU.

	[https://www.gnu.org/software/bison/bison.html](https://www.gnu.org/software/bison/bison.html) || [bison](https://www.archlinux.org/packages/?name=bison)

*   **[GNU m4](https://en.wikipedia.org/wiki/GNU_m4 "wikipedia:GNU m4")** — O processador de macros do GNU.

	[https://www.gnu.org/software/m4/](https://www.gnu.org/software/m4/) || [m4](https://www.archlinux.org/packages/?name=m4)

*   **[GDB](https://en.wikipedia.org/wiki/GNU_Debugger "wikipedia:GNU Debugger")** — O depurador do GNU.

	[https://www.gnu.org/software/gdb/](https://www.gnu.org/software/gdb/) || [gdb](https://www.archlinux.org/packages/?name=gdb)

### Sistema de compilação

Do [Wikipédia](https://en.wikipedia.org/wiki/GNU_build_system "wikipedia:GNU build system"):

	O sistema de compilação do GNU, também conhecido como Autotools, é um conjunto de ferramentas de programação para assistir no processo de criação de pacotes de código-fonte portáteis para muitos sistemas tipo Unix.

*   **[GNU Autoconf](https://en.wikipedia.org/wiki/pt:Autoconf "wikipedia:pt:Autoconf")** — Ferramenta para configurar automaticamente código-fonte.

	[http://www.gnu.org/software/autoconf](http://www.gnu.org/software/autoconf) || [autoconf](https://www.archlinux.org/packages/?name=autoconf)

*   **[GNU Automake](https://en.wikipedia.org/wiki/pt:Automake "wikipedia:pt:Automake")** — Ferramenta para criar automaticamente Makefiles.

	[http://www.gnu.org/software/automake](http://www.gnu.org/software/automake) || [automake](https://www.archlinux.org/packages/?name=automake)

*   **[GNU Libtool](https://en.wikipedia.org/wiki/GNU_Libtool "wikipedia:GNU Libtool")** — Um scripts de suporte genérico para bibliotecas.

	[http://www.gnu.org/software/libtool](http://www.gnu.org/software/libtool) || [libtool](https://www.archlinux.org/packages/?name=libtool)

## Outros softwares

Muitas outras ferramentas opcionais do GNU está disponíveis nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"):

*   [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"), um ambiente de desktop
*   [GIMP](/index.php/GIMP "GIMP"), um editor de imagens
*   [GTK+](/index.php/GTK%2B "GTK+"), um kit de ferramentas de widget
*   [Gnumeric](/index.php/Gnumeric "Gnumeric"), um software de planilhas
*   [GNU Parted](/index.php/GNU_Parted "GNU Parted"), um gerenciador de partição
*   [GNU Screen](/index.php/GNU_Screen "GNU Screen"), um multiplexador de terminal
*   [GNU nano](/index.php/GNU_nano "GNU nano"), um editor de texto de linha de comando
*   [GNU Emacs](/index.php/GNU_Emacs "GNU Emacs"), um editor de texto extensível, personalizável e autodocumentado
*   [GnuPG](/index.php/GnuPG "GnuPG"), uma implementação do OpenPGP
*   [GNU Octave](/index.php/GNU_Octave "GNU Octave"), uma linguagem de programação científica
*   [GNU Readline](/index.php/Readline "Readline"), uma biblioteca de edição de linha para interfaces de linha de comando

## Veja também

*   [https://www.gnu.org/](https://www.gnu.org/)
*   [O Manifesto GNU](https://www.gnu.org/gnu/manifesto)
*   [Lista de pacotes GNU no Wikipédia](https://en.wikipedia.org/wiki/List_of_GNU_packages "wikipedia:List of GNU packages")
*   O [Projeto Arch Hurd](https://archhurd.org/) visa portar o Arch Linux para o kernel Hurd.