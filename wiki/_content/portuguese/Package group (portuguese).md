**Status de tradução:** Esse artigo é uma tradução de [Package group](/index.php/Package_group "Package group"). Data da última tradução: 2019-01-02\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Package_group&diff=0&oldid=561245) na versão em inglês.

Um **grupo de pacotes** é um conjunto de pacotes relacionados, definidos pelo [empacotador](/index.php/Empacotador "Empacotador"), que podem ser instalados ou desinstalados simultaneamente usando o nome do grupo como um substituto para cada nome de pacote individual. Embora um grupo não seja um pacote, ele pode ser instalado de maneira semelhante a um pacote, consulte [Pacman (Português)#Instalando grupos de pacotes](/index.php/Pacman_(Portugu%C3%AAs)#Instalando_grupos_de_pacotes "Pacman (Português)") e [PKGBUILD (Português)#groups](/index.php/PKGBUILD_(Portugu%C3%AAs)#groups "PKGBUILD (Português)").

## Contents

*   [1 Grupos](#Grupos)
    *   [1.1 base](#base)
    *   [1.2 base-devel](#base-devel)
*   [2 Diferença para um pacote meta](#Diferença_para_um_pacote_meta)
*   [3 Veja também](#Veja_também)

## Grupos

Os grupos de pacotes mais importantes são:

### base

O grupo [base](https://www.archlinux.org/groups/x86_64/base/) contém:

*   softwares essenciais, como o [kernel](/index.php/Kernel "Kernel"), [Bash](/index.php/Bash "Bash"), os [utilitários principais](/index.php/Utilit%C3%A1rios_principais "Utilitários principais") e [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")
*   softwares não essenciais, como [dhcpcd](/index.php/Dhcpcd "Dhcpcd"), [netctl](/index.php/Netctl "Netctl"), [nano](/index.php/Nano "Nano") e [vi](/index.php/Vi "Vi").

### base-devel

O grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) contém ferramentas necessárias para compilar muitos pacotes como o [GCC](/index.php/GCC "GCC") e o [make](/index.php/GNU_make "GNU make"). Veja também [makepkg (Português)#Uso](/index.php/Makepkg_(Portugu%C3%AAs)#Uso "Makepkg (Português)").

## Diferença para um pacote meta

Um *pacote meta*, muitas vezes (embora nem sempre) intitulado com o sufixo "-meta", fornece funcionalidade semelhante a um grupo de pacotes, pois permite que vários pacotes relacionados sejam instalados ou desinstalados simultaneamente. Pacotes Meta podem ser instalados como qualquer outro pacote (veja [Pacman (Português)#Instalando pacotes específicos](/index.php/Pacman_(Portugu%C3%AAs)#Instalando_pacotes_específicos "Pacman (Português)")). A única diferença entre um pacote meta e um pacote regular é que um pacote meta é vazio e existe apenas para vincular pacotes relacionados por meio de dependências.

A vantagem de um pacote meta, comparado a um grupo, é que quaisquer novos pacotes membro serão instalados quando o pacote meta for atualizado com um novo conjunto de dependências. Isso está em contraste com um grupo no qual os novos membros do grupo não serão instalados automaticamente. A desvantagem de um pacote meta é que ele não é tão flexível quanto um grupo; você pode escolher quais membros do grupo você deseja instalar, mas você não pode escolher quais dependências do pacote meta você deseja instalar. Da mesma forma, você pode desinstalar membros do grupo sem precisar remover o grupo inteiro. No entanto, você não pode remover as dependências do pacote meta sem ter que desinstalar o próprio pacote meta.

## Veja também

*   [Lista de todos os grupos de pacotes](https://www.archlinux.org/groups/)
*   Exemplos:
    *   [GNOME (Português)#Instalação](/index.php/GNOME_(Portugu%C3%AAs)#Instalação "GNOME (Português)")
    *   [KDE#Installation](/index.php/KDE#Installation "KDE")
    *   [i3#Installation](/index.php/I3#Installation "I3")