**Status de tradução:** Esse artigo é uma tradução de [Desktop environment](/index.php/Desktop_environment "Desktop environment"). Data da última tradução: 2018-10-01\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Desktop_environment&diff=0&oldid=544591) na versão em inglês.

Artigos relacionados

*   [Comparação entre ambientes de desktop](/index.php/Compara%C3%A7%C3%A3o_entre_ambientes_de_desktop "Comparação entre ambientes de desktop")
*   [Category:Freedesktop.org (Português)](/index.php/Category:Freedesktop.org_(Portugu%C3%AAs) "Category:Freedesktop.org (Português)")

Um [ambiente de desktop](https://en.wikipedia.org/wiki/pt:Ambiente_de_desktop "wikipedia:pt:Ambiente de desktop") ou ambiente de trabalho (em inglês, *desktop environment* ou **DE**) é uma implementação da [metáfora de escritório](https://en.wikipedia.org/wiki/pt:Met%C3%A1fora_de_escrit%C3%B3rio "wikipedia:pt:Metáfora de escritório") feita por um conjunto de programas, que compartilham uma interface gráfica de usuário (GUI) comum.

## Contents

*   [1 Visão geral](#Vis.C3.A3o_geral)
*   [2 Lista de ambientes de desktop](#Lista_de_ambientes_de_desktop)
    *   [2.1 Com suporte oficial](#Com_suporte_oficial)
    *   [2.2 Sem suporte oficial](#Sem_suporte_oficial)
*   [3 Ambientes personalizados](#Ambientes_personalizados)
    *   [3.1 Usar um gerenciador de janela diferente](#Usar_um_gerenciador_de_janela_diferente)

## Visão geral

Um ambiente de desktop reúne uma variedade de componentes para fornecer elementos comuns de interface gráfica do usuário, como ícones, barras de ferramentas, papéis de parede e widgets da área de trabalho. Além disso, a maioria dos ambientes de desktop inclui um conjunto de aplicativos e utilitários integrados. Mais importante ainda, os ambientes de desktop fornecem seu próprio [gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela"), que normalmente pode ser substituído por outro compatível.

O usuário é livre para configurar seu ambiente de GUI de várias maneiras. Ambientes de desktop simplesmente fornecem um meio completo e conveniente de realizar essa tarefa. Observe que os usuários estão livres para misturar e combinar aplicativos de vários ambientes de desktop. Por exemplo, um usuário do [KDE](/index.php/KDE "KDE") pode instalar e executar aplicativos do [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") como o navegador [Epiphany](/index.php/Epiphany "Epiphany"), caso ele/ela prefira este ao navegador web Konqueror do KDE. Uma desvantagem dessa abordagem é que muitos aplicativos fornecidos por projetos de ambiente de desktop dependem muito das respectivas bibliotecas subjacentes do DE. Como resultado, a instalação de aplicativos de uma variedade de ambientes de desktop exigirá a instalação de um maior número de dependências. Os usuários que buscam economizar espaço em disco geralmente evitam esses ambientes mistos ou escolhem alternativas que dependem apenas de algumas bibliotecas externas.

Além disso, os aplicativos fornecidos por DE tendem a se integrar melhor com seus ambientes nativos. Superficialmente, a mistura de ambientes com kits de ferramentas *(toolkits)* de widgets diferentes resultará em discrepâncias visuais (ou seja, as interfaces usarão ícones e estilos de widgets diferentes). Em termos de usabilidade, os ambientes mistos podem não se comportar de maneira semelhante (por exemplo, clique único versus ícones de clique duplo; funcionalidade arrastar e soltar), potencialmente causando confusão ou comportamento inesperado.

Antes de instalar um ambiente de desktop, é necessária uma instalação funcional do servidor X. Veja [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") para informações detalhadas. Alguns ambientes de desktop também podem oferecer suporte ao [Wayland](/index.php/Wayland "Wayland") como uma alternativa ao X, mas a maioria deles ainda é experimental.

## Lista de ambientes de desktop

### Com suporte oficial

*   **[Budgie](/index.php/Budgie "Budgie")** — Budgie é um ambiente de desktop projetado com o usuário moderno em mente, ele se concentra na simplicidade e elegância.

	[https://budgie-desktop.org/](https://budgie-desktop.org/) || [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop)

*   **[Cinnamon](/index.php/Cinnamon "Cinnamon")** — O Cinnamon se esforça para fornecer uma experiência de usuário tradicional. Cinnamon é um fork do GNOME 3.

	[http://developer.linuxmint.com/projects/cinnamon-projects.html](http://developer.linuxmint.com/projects/cinnamon-projects.html) || [cinnamon](https://www.archlinux.org/packages/?name=cinnamon)

*   **[Deepin](/index.php/Deepin "Deepin")** — A interface e os aplicativos de desktop do Deepin apresentam um design intuitivo e elegante. Movimentar-se, compartilhar e pesquisar etc. tornou-se simplesmente uma experiência divertida.

	[https://www.deepin.org/](https://www.deepin.org/) || [deepin](https://www.archlinux.org/groups/x86_64/deepin/)

*   **[Enlightenment](/index.php/Enlightenment "Enlightenment")** — O shell de desktop Enlightenment fornece um eficiente gerenciador de janelas baseado nas Bibliotecas Fundamentais do Enlightenment *(Enlightenment Foundation Libraries)* juntamente com outros componentes essenciais da área de trabalho, como um gerenciador de arquivos, ícones da área de trabalho e widgets. Possui suporte a temas, enquanto ainda é capaz de executar em hardwares mais antigos ou dispositivos embarcados.

	[https://www.enlightenment.org/](https://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)")** — O ambiente de desktop GNOME é um desktop atrativo e intuitivo com tanto uma sessão moderna (*GNOME*) e uma clássica (*GNOME Clássico*).

	[https://www.gnome.org/gnome-3/](https://www.gnome.org/gnome-3/) || [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

*   **[GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")** — GNOME Flashback é um shell para o GNOME 3 que foi inicialmente chamado de modo flashback do GNOME. O layout de desktop e a tecnologia subjacente é similar a do GNOME 2.

	[https://wiki.gnome.org/Projects/GnomeFlashback](https://wiki.gnome.org/Projects/GnomeFlashback) || [gnome-flashback](https://www.archlinux.org/packages/?name=gnome-flashback)

*   **[KDE Plasma](/index.php/KDE_Plasma "KDE Plasma")** — O ambiente de desktop Plasma do KDE é um ambiente de trabalho familiar. O Plasma oferece todas as ferramentas necessárias para uma experiência de computação moderna, para que você possa ser produtivo desde o início.

	[https://www.kde.org/plasma-desktop](https://www.kde.org/plasma-desktop) || [plasma](https://www.archlinux.org/groups/x86_64/plasma/)

*   **[LXDE](/index.php/LXDE "LXDE")** — O Lightweight X11 Desktop Environment (ambiente de desktop X11 leve) é um ambiente de desktop rápido e que economiza energia. Ele vem com uma interface moderna, suporte a vários idiomas, atalhos de teclado padrão e recursos adicionais, como a navegação por arquivos com guias. Fundamentalmente projetado para ser leve, o LXDE se esforça para ter menos CPU e RAM do que outros ambientes.

	[https://lxde.org/](https://lxde.org/) || GTK+ 2: [lxde](https://www.archlinux.org/groups/x86_64/lxde/), GTK+ 3: [lxde-gtk3](https://www.archlinux.org/groups/x86_64/lxde-gtk3/)

*   **[LXQt](/index.php/LXQt "LXQt")** — O LXQt é o *port* do Qt e a próxima versão do LXDE, o Lightweight Desktop Environment. É o produto da fusão entre os projetos LXDE-Qt e Razor-qt: Um ambiente de desktop leve, modular, extremamente rápido e fácil de usar.

	[http://lxqt.org/](http://lxqt.org/) || [lxqt](https://www.archlinux.org/groups/x86_64/lxqt/)

*   **[MATE](/index.php/MATE "MATE")** — O Mate fornece um ambiente de desktop intuitivo e atraente para usuários de Linux que usam metáforas tradicionais. O MATE começou como um fork do GNOME 2, mas agora usa o GTK+ 3.

	[https://mate-desktop.org/](https://mate-desktop.org/) || [mate](https://www.archlinux.org/groups/x86_64/mate/)

*   **[Sugar](/index.php/Sugar "Sugar")** — A Sugar Learning Platform (plataforma de aprendizagem Sugar) é um ambiente computacional composto por Atividades projetadas para ajudar crianças de 5 a 12 anos de idade a aprenderem juntas por meio de expressão de mídia rica. O Sugar é o principal componente de um esforço mundial para oferecer a todas as crianças a oportunidade de uma educação de qualidade – atualmente é usado por quase um milhão de crianças em todo o mundo, falando 25 idiomas em mais de 40 países. Sugar fornece os meios para ajudar as pessoas a levarem vidas completas através do acesso a uma educação de qualidade que atualmente é desperdiçada por muitos.

	[https://sugarlabs.org/](https://sugarlabs.org/) || [sugar](https://www.archlinux.org/packages/?name=sugar) + [sugar-fructose](https://www.archlinux.org/groups/x86_64/sugar-fructose/)

*   **[Xfce](/index.php/Xfce "Xfce")** — O Xfce incorpora a tradicional [filosofia Unix](https://en.wikipedia.org/wiki/pt:Filosofia_Unix "wikipedia:pt:Filosofia Unix") de modularidade e reutilização. Ele consiste em vários componentes que fornecem a funcionalidade completa que se pode esperar de um ambiente de desktop moderno, mantendo-se relativamente leve. Eles são empacotados separadamente e você pode escolher entre os pacotes disponíveis para criar o melhor ambiente de trabalho pessoal.

	[https://xfce.org/](https://xfce.org/) || [xfce4](https://www.archlinux.org/groups/x86_64/xfce4/)

### Sem suporte oficial

*   **[EDE](/index.php/Equinox_Desktop_Environment "Equinox Desktop Environment")** — O "Equinox Desktop Environment" é um ambiente de desktop projetado para ser simples, extremamente leve e rápido.

	[https://edeproject.org/](https://edeproject.org/) || [ede](https://aur.archlinux.org/packages/ede/)

*   **[Liri](/index.php/Liri "Liri")** — O Liri é um ambiente de desktop com design e recursos modernos. Liri é a fusão entre [Hawaii](http://hawaiios.org/), [Papyros](http://papyros.io/) e o [Projeto Liri](https://github.com/liri-project). Altamente experimental.

	[https://liri.io/](https://liri.io/) || [liri-shell-git](https://aur.archlinux.org/packages/liri-shell-git/)

*   **[Lumina](/index.php/Lumina "Lumina")** — Lumina é um ambiente de desktop leve escrito em Qt 5 para o FreeBSD que usa o Fluxbox para gerenciamento de janelas.

	[https://lumina-desktop.org/](https://lumina-desktop.org/) || [lumina-desktop](https://aur.archlinux.org/packages/lumina-desktop/)

*   **[Moksha](/index.php/Moksha "Moksha")** — Fork do Enlightenment atualmente usado como ambiente de desktop padrão no Bodhi Linux baseado em Ubuntu.

	[http://www.bodhilinux.com/moksha-desktop/](http://www.bodhilinux.com/moksha-desktop/) || [moksha](https://aur.archlinux.org/packages/moksha/)

*   **[Pantheon](/index.php/Pantheon "Pantheon")** — O Pantheon é o ambiente de desktop padrão originalmente criado para a distribuição de SO elementar. Ele é escrito do zero usando Vala e o kit de ferramentas GTK3\. Com relação à usabilidade e aparência, o desktop tem algumas semelhanças com o GNOME Shell e o macOS.

	[https://elementary.io/](https://elementary.io/) || [pantheon-session-git](https://aur.archlinux.org/packages/pantheon-session-git/)

*   **theShell** — theShell é um ambiente de desktop que tenta ser o mais transparente possível. Ele usa o Qt 5 como seu kit de ferramentas de widgets e o KWin como seu gerenciador de janelas. Também incorpora um assistente pessoal. Ele também incorpora um assistente pessoal.

	[https://vicr123.com/theshell](https://vicr123.com/theshell) || [theshell](https://aur.archlinux.org/packages/theshell/)

*   **[Trinity](/index.php/Trinity "Trinity")** — O projeto Trinity Desktop Environment (TDE) é um ambiente de desktop do computador para sistemas operacionais tipo Unix com o objetivo principal de manter o estilo de computação geral do KDE 3.5.

	[http://www.trinitydesktop.org/](http://www.trinitydesktop.org/) || Veja [Trinity](/index.php/Trinity "Trinity")

## Ambientes personalizados

Os ambientes de desktop representam o meio mais simples de instalar um ambiente gráfico *completo*. No entanto, os usuários são livres para criar e personalizar seu ambiente gráfico de várias maneiras, se nenhum dos ambientes populares de desktop atender aos seus requisitos. Geralmente, a criação de um ambiente personalizado envolve a seleção de um [gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela"), uma [barra de tarefas](/index.php/List_of_applications#Taskbars "List of applications") e um número de aplicativos (uma seleção minimalista geralmente inclui um [emulador de terminal](/index.php/Terminal_emulator "Terminal emulator"), [gerenciador de arquivos](/index.php/List_of_applications#File_managers "List of applications") e [editor de texto](/index.php/Text_editor "Text editor")).

Outros componentes geralmente fornecidos por ambientes de área de trabalho são:

*   Iniciador de aplicativo: [List of applications#Application launchers](/index.php/List_of_applications#Application_launchers "List of applications")
*   Controle de volume de áudio: [List of applications#Volume control](/index.php/List_of_applications#Volume_control "List of applications")
*   [Gerenciador de área de transferência](/index.php/Clipboard_manager "Clipboard manager")
*   Compositor de desktop: [Xorg#Composite](/index.php/Xorg#Composite "Xorg")
*   Definidor de papel de parede e ícone da área de trabalho: [List of applications#Wallpaper setters](/index.php/List_of_applications#Wallpaper_setters "List of applications") e [Openbox#Desktop icons and wallpapers](/index.php/Openbox#Desktop_icons_and_wallpapers "Openbox")
*   Gerenciador de exibição: [Gerenciadores de exibição#Lista de gerenciadores de exibição](/index.php/Gerenciadores_de_exibi%C3%A7%C3%A3o#Lista_de_gerenciadores_de_exibi.C3.A7.C3.A3o "Gerenciadores de exibição")
*   Configurações de tela de economia de energia: [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling")
*   Diálogo de *logout*: [Oblogout](/index.php/Oblogout "Oblogout")
*   Ferramenta de montagem: [List of applications#Mount tools](/index.php/List_of_applications#Mount_tools "List of applications")
*   Daemon de notificação: [Desktop notifications](/index.php/Desktop_notifications "Desktop notifications")
*   Agente de autenticação de Polkit: [Polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit")
*   Bloqueador de tela: [List of applications#Screen lockers](/index.php/List_of_applications#Screen_lockers "List of applications")
*   Aplicativos padrão: [XDG MIME Applications#mimeapps.list](/index.php/XDG_MIME_Applications#mimeapps.list "XDG MIME Applications")

### Usar um gerenciador de janela diferente

Se o ambiente de desktop tem um artigo, veja sua seção *Usar um gerenciador de janela diferente* (ou, no artigo original, *Use a diferent window manager*), do contrário consulte a documentação oficial.

*   [Budgie#Use a different window manager](/index.php/Budgie#Use_a_different_window_manager "Budgie")
*   [Cinnamon#Use a different window manager](/index.php/Cinnamon#Use_a_different_window_manager "Cinnamon")
*   [GNOME (Português)#Usar um gerenciador de janela diferente](/index.php/GNOME_(Portugu%C3%AAs)#Usar_um_gerenciador_de_janela_diferente "GNOME (Português)")
*   [KDE#Use a different window manager](/index.php/KDE#Use_a_different_window_manager "KDE")
*   [LXDE#Use a different window manager](/index.php/LXDE#Use_a_different_window_manager "LXDE")
*   [LXQt#Use a different window manager](/index.php/LXQt#Use_a_different_window_manager "LXQt")
*   [MATE#Use a different window manager](/index.php/MATE#Use_a_different_window_manager "MATE")
*   [Xfce#Use a different window manager](/index.php/Xfce#Use_a_different_window_manager "Xfce")