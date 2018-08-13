Artigos relacionados

*   [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)")
*   [Utilitários principais](/index.php/Utilit%C3%A1rios_principais "Utilitários principais")

Do [https://www.gnu.org/](https://www.gnu.org/):

	O Projeto GNU foi lançado em 1984 para desenvolver o sistema operacional GNU, um sistema operacional completo semelhante ao Unix, que é software livre – software que respeita a sua liberdade. Os sistemas operacionais semelhantes a Unix são criados a partir de uma coleção de aplicativos, bibliotecas e ferramentas para desenvolvedores – além de um programa para alocar recursos e conversar com o hardware, conhecido como kernel. [...] A combinação de GNU e Linux é o sistema operacional GNU/Linux, agora usado por milhões e algumas vezes incorretamente chamado apenas de “Linux”. O nome “GNU” é um acrônimo recursivo para “GNU's Not Unix!” ou, em português, “GNU Não é Unix!”.

O objetivo do Projeto GNU é produzir um sistema operacional totalmente livre. Enquanto o kernel do GNU não atingiu uma versão estável, o projeto resultou na criação de muitas ferramentas que alimentam a maioria das distribuições de sistemas operacionais semelhantes a Unix. O [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)") é uma distribuição desse tipo, usando o software GNU, como o gerenciador de boot [GRUB](/index.php/GRUB "GRUB"), o shell [Bash](/index.php/Bash "Bash") e vários outros utilitários e bibliotecas.

## Contents

*   [1 O sistema base](#O_sistema_base)
    *   [1.1 Kernel](#Kernel)
    *   [1.2 Coleção de softwares](#Cole.C3.A7.C3.A3o_de_softwares)
*   [2 Ferramentas de desenvolvimento](#Ferramentas_de_desenvolvimento)
*   [3 Outras ferramentas](#Outras_ferramentas)
*   [4 Veja também](#Veja_tamb.C3.A9m)

## O sistema base

No final do processo de instalação, um sistema Arch é nada mais do que o Kernel Linux, a cadeia de ferramentas do GNU e algumas ferramentas de linha de comando. A instalação mínima normalmente contém todo o grupo [base](https://www.archlinux.org/groups/x86_64/base/).

### Kernel

Enquanto o [Hurd](https://www.gnu.org/s/hurd/hurd.html), o kernel do GNU, está em desenvolvimento ativo, ainda não existe uma versão estável. Por esse motivo, o Arch e a maioria dos outros sistemas baseados em GNU usam o Kernel Linux. O [Projeto Arch Hurd](/index.php/Arch_Hurd_Project "Arch Hurd Project") visa portar o Arch Linux para o kernel Hurd.

### Coleção de softwares

*   **[GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)")** — GRUB é um gerenciador de boot para o projeto GNU.

	[https://www.gnu.org/software/grub/](https://www.gnu.org/software/grub/) || [grub](https://www.archlinux.org/packages/?name=grub)

*   **[glibc](https://en.wikipedia.org/wiki/pt:glibc "wikipedia:pt:glibc")** — glibc é a implementação do GNU da biblioteca C. Apesar de seu nome, ela também oferece suporte a C++ e outras linguagens indiretamente. Ela define as chamadas de sistema e outros recurso básicos como open, malloc, printf, exit.

	[https://www.gnu.org/software/libc/](https://www.gnu.org/software/libc/) || [glibc](https://www.archlinux.org/packages/?name=glibc)

*   **[binutils](https://en.wikipedia.org/wiki/binutils "wikipedia:binutils")** — É uma coleção de ferramentas de binárias.

	[https://www.gnu.org/software/binutils/](https://www.gnu.org/software/binutils/) || [binutils](https://www.archlinux.org/packages/?name=binutils)

*   **[bash](/index.php/Bash "Bash")** — É um shell compatível com sh que incorpora recursos úteis do Korn shell (ksh) e do C shell (csh).

	[https://www.gnu.org/software/bash/](https://www.gnu.org/software/bash/) || [bash](https://www.archlinux.org/packages/?name=bash)

*   **[coreutils](/index.php/Coreutils_(Portugu%C3%AAs) "Coreutils (Português)")** — coreutils fornece os utilitários básicos de manipulação de arquivo, shell e texto do sistema operacional GNU.

	[https://www.gnu.org/software/coreutils/](https://www.gnu.org/software/coreutils/) || [coreutils](https://www.archlinux.org/packages/?name=coreutils)

*   **[gzip](https://en.wikipedia.org/wiki/pt:gzip "wikipedia:pt:gzip")** — gzip é tanto um formato de arquivo quanto um aplicativo de software para compressão e descompressão.

	[https://www.gnu.org/software/gzip/](https://www.gnu.org/software/gzip/) || [gzip](https://www.archlinux.org/packages/?name=gzip)

*   **[tar](/index.php/Tar_(Portugu%C3%AAs) "Tar (Português)")** — It provides the ability to create or decompress tar archives, as well as various other kinds of manipulation.

	[https://www.gnu.org/software/tar/](https://www.gnu.org/software/tar/) || [tar](https://www.archlinux.org/packages/?name=tar)

## Ferramentas de desenvolvimento

Embora não seja necessário, os usuários têm a opção de instalar o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) para algumas ferramentas de desenvolvimento de software. Este grupo é um requisito para a compilação de pacotes a partir do [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)").

Entre **base-devel** estão vários membros do [Conjunto de Ferramentas GNU](https://en.wikipedia.org/wiki/pt:GNU_toolchain "wikipedia:pt:GNU toolchain"), um *"conjunto de ferramentas usadas de forma serial [...] para desenvolver aplicativos e sistemas operacionais "*. Os principais componentes deste conjunto de ferramenta são:

**compilação e construção:** [make](https://www.archlinux.org/packages/?name=make)

**conjunto de compiladores:** [gcc](https://www.archlinux.org/packages/?name=gcc)

**vinculador, montador e outras ferramentas:** [binutils](https://www.archlinux.org/packages/?name=binutils)

	[w:gold (linker)](https://en.wikipedia.org/wiki/gold_(linker) "w:gold (linker)"), [w:GNU Binutils](https://en.wikipedia.org/wiki/GNU_Binutils "w:GNU Binutils"), [w:GNU linker](https://en.wikipedia.org/wiki/GNU_linker "w:GNU linker")

**gerador de analisador:** [bison](https://www.archlinux.org/packages/?name=bison)

**processador de macro:** [m4](https://www.archlinux.org/packages/?name=m4)

[Sistema de Compilação GNU](https://en.wikipedia.org/wiki/GNU_build_system "wikipedia:GNU build system") (autotools):

	**configurar o código-fonte automaticamente:** [autoconf](https://www.archlinux.org/packages/?name=autoconf)

	**criar automaticamente Makefiles:** [automake](https://www.archlinux.org/packages/?name=automake)

	**scripts de suporte a bibliotecas:** [libtool](https://www.archlinux.org/packages/?name=libtool)

## Outras ferramentas

Muitas outras ferramentas opcionais do GNU está disponíveis nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"):

**Ambiente desktop:** [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)")

**Gerenciador de janelas em tela cheia:** [GNU Screen](/index.php/GNU_Screen "GNU Screen")

**Gerenciador de partição:** [GNU Parted](/index.php/GNU_Parted "GNU Parted")

**Editor de imagens:** [GIMP](/index.php/GIMP "GIMP")

**Planilhas:** [Gnumeric](/index.php/Gnumeric "Gnumeric")

**Kit de ferramentas de widget:** [GTK+](/index.php/GTK%2B "GTK+")

## Veja também

*   [Todos os pacotes GNU](https://www.gnu.org/software/software.html#allgnupkgs) - Atuais projetos do GNU
*   [O Manifesto GNU](https://www.gnu.org/gnu/manifesto)
*   [Lista de pacotes GNU no Wikipédia](https://en.wikipedia.org/wiki/List_of_GNU_packages "wikipedia:List of GNU packages")