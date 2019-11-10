**Status de tradução:** Esse artigo é uma tradução de [Meta package and package group](/index.php/Meta_package_and_package_group "Meta package and package group"). Data da última tradução: 2019-11-06\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Meta_package_and_package_group&diff=0&oldid=587700) na versão em inglês.

Um **metapacote** e **grupo de pacotes** podem ser definidos pelo [empacotador](/index.php/Empacotador "Empacotador") para denotar um conjunto de pacotes relacionados. Ambos podem permitir instalar ou desinstalar este conjunto de pacotes simultaneamente usando o metapacote ou o nome do grupo como um substituto para cada nome de pacote individual. Embora um grupo não seja um pacote, ele pode ser instalado de maneira semelhante a um pacote, consulte [pacman (Português)#Instalando grupos de pacotes](/index.php/Pacman_(Portugu%C3%AAs)#Instalando_grupos_de_pacotes "Pacman (Português)") e [PKGBUILD (Português)#groups](/index.php/PKGBUILD_(Portugu%C3%AAs)#groups "PKGBUILD (Português)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Diferença entre um metapacote e um grupo de pacotes](#Diferença_entre_um_metapacote_e_um_grupo_de_pacotes)
*   [2 Metapacotes](#Metapacotes)
*   [3 Grupos](#Grupos)
*   [4 Veja também](#Veja_também)

## Diferença entre um metapacote e um grupo de pacotes

A diferença entre um metapacote e um pacote comum é que um metapacote é vazio e existe apenas para vincular pacotes relacionados por meio de dependências. Um *metapacote*, muitas vezes (embora nem sempre) intitulado com o sufixo "-meta", fornece funcionalidade semelhante a um grupo de pacotes, pois permite que vários pacotes relacionados sejam instalados ou desinstalados simultaneamente.

Cada solução possui vantagens e desvantagens:

*metapacote*:

*   Os metapacotes podem ser instalados como qualquer outro pacote (consulte [pacman (Português)#Instalando pacotes específicos](/index.php/Pacman_(Portugu%C3%AAs)#Instalando_pacotes_específicos "Pacman (Português)")).
*   Os metapacotes podem ser removidos como qualquer outro pacote (veja [pacman (Português)#Removendo pacotes](/index.php/Pacman_(Portugu%C3%AAs)#Removendo_pacotes "Pacman (Português)")).
*   Quaisquer novos pacotes-membro serão instalados quando o metapacote é atualizado com um novo conjunto de dependências.
*   Os usuários não podem escolher quais dependências de metapacotes que desejam instalar.
*   Os usuários não podem remover as dependências do metapacote sem precisar desinstalar o próprio pacote.

*grupo*:

*   Os grupos de pacotes solicitarão aos usuários que selecionem os pacotes do grupo que desejam instalar (consulte [pacman (Português)#Instalando grupos de pacotes](/index.php/Pacman_(Portugu%C3%AAs)#Instalando_grupos_de_pacotes "Pacman (Português)")).
*   Os usuários não podem desinstalar um grupo, porque instalaram uma lista de pacotes.
*   Novos membros do grupo não serão instalados automaticamente.
*   Os usuários podem escolher quais membros do grupo eles desejam instalar.
*   Os usuários podem desinstalar membros do grupo sem precisar remover o grupo inteiro.

## Metapacotes

O metapacote mais importante é o [base](https://www.archlinux.org/packages/?name=base). Ele contém um conjunto mínimo de pacotes que define uma instalação básica do Arch Linux. Ele inclui:

*   básico como [glibc](https://www.archlinux.org/packages/?name=glibc) e [bash](/index.php/Bash "Bash"),
*   coisas relacionadas à distribuição como [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") e [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)")
*   ferramentas POSIX como [utilitários principais](/index.php/Utilit%C3%A1rios_principais "Utilitários principais"), utilitários de processo, arquivo e compressão de arquivo
*   ferramentas de rede como [iproute2](https://www.archlinux.org/packages/?name=iproute2)

O [kernel](/index.php/Kernel_(Portugu%C3%AAs) "Kernel (Português)") é uma dependência opcional. Veja [o anúncio quando ele foi introduzido](https://www.archlinux.org/news/base-group-replaced-by-mandatory-base-package-manual-intervention-required/) e [os motivos para o base ser um metapacote](https://lists.archlinux.org/pipermail/arch-dev-public/2019-January/029435.html).

## Grupos

O grupo de pacotes mais importante é o [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/). Ele contém ferramentas necessárias para compilar muitos pacotes como o [GCC](/index.php/GCC_(Portugu%C3%AAs) "GCC (Português)") e o [make](/index.php/GNU_make "GNU make"). Veja também [makepkg (Português)#Uso](/index.php/Makepkg_(Portugu%C3%AAs)#Uso "Makepkg (Português)").

## Veja também

*   [Lista de todos os grupos de pacotes](https://www.archlinux.org/groups/)
*   Exemplos:
    *   [GNOME (Português)#Instalação](/index.php/GNOME_(Portugu%C3%AAs)#Instalação "GNOME (Português)")
    *   [KDE (Português)#Instalação](/index.php/KDE_(Portugu%C3%AAs)#Instalação "KDE (Português)")
    *   [i3#Installation](/index.php/I3#Installation "I3")