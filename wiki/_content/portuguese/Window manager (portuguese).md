**Status de tradução:** Esse artigo é uma tradução de [Window manager](/index.php/Window_manager "Window manager"). Data da última tradução: 2019-11-11\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Window_manager&diff=0&oldid=578212) na versão em inglês.

Artigos relacionados

*   [Xdg-menu](/index.php/Xdg-menu "Xdg-menu")
*   [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)")
*   [xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)")
*   [Iniciar X no login](/index.php/Iniciar_X_no_login "Iniciar X no login")

Um [gerenciador de janela](https://en.wikipedia.org/wiki/pt:Gerenciador_de_janela "wikipedia:pt:Gerenciador de janela"), ou *window manager* (WM), é um software de sistema que controla o posicionamento e aparência de janelas dentro de um sistema de janelas em uma interface gráfica de usuário (GUI). Ele pode ser parte de um [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop") (DE) ou ser usado de forma independente.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Visão geral](#Visão_geral)
    *   [1.1 Tipos](#Tipos)
*   [2 Lista de gerenciadores de janela](#Lista_de_gerenciadores_de_janela)
    *   [2.1 Gerenciadores de janela de empilhamento](#Gerenciadores_de_janela_de_empilhamento)
    *   [2.2 Gerenciadores de janela de tiling](#Gerenciadores_de_janela_de_tiling)
    *   [2.3 Gerenciadores de janela dinâmicos](#Gerenciadores_de_janela_dinâmicos)
*   [3 Veja também](#Veja_também)

## Visão geral

Os gerenciadores de janela são clientes X que controlam a aparência e o comportamento dos quadros ("janelas"), onde os vários aplicativos gráficos são desenhados. Eles determinam a borda, a barra do título, o tamanho e a capacidade de redimensionar as janelas, e muitas vezes fornecem outras funcionalidades, como áreas reservadas para aderir [dockapps](http://windowmaker.org/dockapps/) como o [Window Maker](/index.php/Window_Maker "Window Maker"), ou a capacidade para separar janelas como o [Fluxbox](/index.php/Fluxbox "Fluxbox"). Alguns gerenciadores de janela são empacotados com utilitários simples, como menus para iniciar programas ou para configurar o próprio WM.

A especificação [Dicas estendidas de Gerenciador de janela](https://specifications.freedesktop.org/wm-spec/wm-spec-latest.html) (inglês) é usada para permitir que os gerenciadores de janela interajam de maneira padrão com o servidor e os outros clientes.

Alguns gerenciadores de janela são desenvolvidos como parte de um [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop") mais completo, geralmente permitindo que os outros aplicativos fornecidos interajam melhor uns com os outros, dando uma experiência mais consistente ao usuário, com recursos como ícones de área de trabalho, fontes, barras de ferramentas, papéis de parede ou widgets.

Outros gerenciadores de janela são, em vez disso, projetados para serem usados como "autônomos", dando ao usuário liberdade completa sobre a escolha dos outros aplicativos a serem usados. Isso permite ao usuário criar um ambiente mais leve e personalizado, adaptado às suas próprias necessidades específicas. "Extras", como ícones de área de trabalho, barras de ferramentas, papéis de parede ou widgets, se necessário, terão que ser adicionados com aplicativos dedicados adicionais.

Alguns WMs autônomos também podem ser usados para substituir o WM padrão de um DE, assim como alguns WMs orientados a DE podem ser usados autônomo também.

Antes de instalar um gerenciador de janela, é necessária uma instalação funcional do servidor X. Veja [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") para obter informações detalhadas.

### Tipos

*   [Empilhamento](#Gerenciadores_de_janela_de_empilhamento) – os gerenciadores de janela, neste caso também conhecidos como *flutuantes*, fornecem a metáfora tradicional de desktop usado em sistemas operacionais comerciais como Windows e OS X. As janelas agem como folhas de papéis em uma mesa e pode ser empilhada uma sobre a outra. Para páginas disponíveis no Arch Wiki, veja [Category:Stacking WMs (Português)](/index.php/Category:Stacking_WMs_(Portugu%C3%AAs) "Category:Stacking WMs (Português)").
*   [Tiling](#Gerenciadores_de_janela_de_tiling) – os gerenciadores de janela "colam" (*tile*) as janelas lado a lado, de forma que nenhuma se sobreponha a outra. Eles geralmente fazem grande uso de atalhos de teclados e menos (ou nenhuma) dependência do mouse. Os gerenciadores de janela de *tiling* podem ser manuais, oferecendo layouts pré-definidos ou ambos. Para páginas disponíveis no Arch Wiki, veja [Category:Tiling WMs](/index.php/Category:Tiling_WMs "Category:Tiling WMs").
*   [Dinâmico](#Gerenciadores_de_janela_dinâmicos) – os gerenciadores de janela podem trocar dinamicamente entre a disposição de janelas *tiling* ou flutuante. Para páginas disponíveis no Arch Wiki, veja [Category:Dynamic WMs](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs").

Veja [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers") e [Wikipedia:Comparison of X window managers](https://en.wikipedia.org/wiki/Comparison_of_X_window_managers "wikipedia:Comparison of X window managers") para uma comparação entre gerenciadores de janelas.

## Lista de gerenciadores de janela

### Gerenciadores de janela de empilhamento

*   **[2bwm](/index.php/2bwm "2bwm")** — Gerenciador de janela flutuante rápido, com a particularidade de ter 2 bordas, escritas sobre a biblioteca XCB e derivadas de mcwm escritas por Michael Cardell. Em 2bwm tudo é acessível a partir do teclado, mas um dispositivo de apontamento pode ser usado para mover, redimensionar e aumentar/diminuir. O nome mudou recentemente de mcwm-beast para 2bwm.

	[https://github.com/venam/2bwm](https://github.com/venam/2bwm) || [2bwm](https://aur.archlinux.org/packages/2bwm/)

*   **aewm** — Gerenciador de janela moderno e minimalista para o X11\. Ele é controlado inteiramente com o mouse, mas não contém nenhuma interface do usuário visível além dos quadros de janela. O conjunto de comandos é como o vi: projetado no início dos tempos (1997) para extrair velocidade de máquinas com pouca memória, totalmente não-intuitivo e hostil ao usuário, mas rápido e elegante à sua própria maneira.

	[http://www.red-bean.com/decklin/aewm/](http://www.red-bean.com/decklin/aewm/) || [aewm](https://aur.archlinux.org/packages/aewm/)

*   **[AfterStep](https://en.wikipedia.org/wiki/AfterStep "wikipedia:AfterStep")** — Gerenciador de janela para o sistema Unix X Window. Originalmente baseado na aparência da interface NeXTStep, ele fornece aos usuários finais uma área de trabalho consistente, limpa e elegante. O objetivo do desenvolvimento do AfterStep é fornecer flexibilidade na configuração da área de trabalho, melhorando a estética e o uso eficiente dos recursos do sistema.

	[http://www.afterstep.org/](http://www.afterstep.org/) || [afterstep-git](https://aur.archlinux.org/packages/afterstep-git/)

*   **[Blackbox](/index.php/Blackbox "Blackbox")** — Gerenciador de janela rápido e leve para o X Window System, sem todas as dependências irritantes da biblioteca. O Blackbox é construído com C++ e contém código completamente original (mesmo que a implementação gráfica seja semelhante à do WindowMaker).

	[http://blackboxwm.sourceforge.net/](http://blackboxwm.sourceforge.net/) || [blackbox](https://www.archlinux.org/packages/?name=blackbox)

*   **[Compiz](/index.php/Compiz "Compiz")** — Gerenciador de composição OpenGL que usa GLX_EXT_texture_from_pixmap para vincular janelas de nível superior redirecionadas a objetos de textura. Ele tem um sistema de plug-in flexível e foi projetado para funcionar bem na maioria dos hardwares gráficos.

	[https://launchpad.net/compiz](https://launchpad.net/compiz) || [compiz](https://aur.archlinux.org/packages/compiz/), [compiz-core](https://aur.archlinux.org/packages/compiz-core/)

*   **[cwm](/index.php/Cwm "Cwm")** — Originalmente derivado do evilwm, mas depois reescrito do zero. O cwm tem como objetivo ser simples e oferece recursos úteis, como procurar por janelas.

	[https://github.com/chneukirchen/cwm](https://github.com/chneukirchen/cwm) || [cwm](https://aur.archlinux.org/packages/cwm/)

*   **eggwm** — Um gerenciador de janela leve em QT4/QT5

	[eggwm-qt5](https://aur.archlinux.org/packages/eggwm-qt5/) || [eggwm](https://aur.archlinux.org/packages/eggwm/)

*   **[Enlightenment](/index.php/Enlightenment "Enlightenment")** — O Enlightenment não é apenas um gerenciador de janela para Linux/X11 e outros, mas também um conjunto completo de bibliotecas para ajudá-lo a criar lindas interfaces com muito menos trabalho do que fazê-lo à moda antiga e lutar com ferramentas tradicionais, sem mencionar um tradicional gerenciador de janela.

	[http://www.enlightenment.org/](http://www.enlightenment.org/) || [enlightenment](https://www.archlinux.org/packages/?name=enlightenment)

*   **[evilwm](/index.php/Evilwm "Evilwm")** — Gerenciador de janela minimalista para o X Window System. 'Minimalista' aqui não significa que esteja muito vazio para ser usado - significa apenas que omite muitas das coisas que tornam os outros gerentes de janela *in*utilizáveis.

	[http://www.6809.org.uk/evilwm/](http://www.6809.org.uk/evilwm/) || [evilwm](https://aur.archlinux.org/packages/evilwm/)

*   **[Fluxbox](/index.php/Fluxbox "Fluxbox")** — Gerenciador de janela para X que foi baseado no código do Blackbox 0.61.1\. É muito leve em recursos e fácil de manusear, mas ainda repleta de recursos para criar uma experiência de área de trabalho fácil e extremamente rápida. É construído usando C++ e licenciado sob a licença MIT.

	[https://github.com/fluxbox/fluxbox](https://github.com/fluxbox/fluxbox) || [fluxbox](https://www.archlinux.org/packages/?name=fluxbox)

*   **[Flwm](https://en.wikipedia.org/wiki/FLWM "wikipedia:FLWM")** — Tente combinar as melhores ideias em vários gerenciadores de janela. A principal influência e base de código é de wm2 por Chris Cannam.

	[http://flwm.sourceforge.net/](http://flwm.sourceforge.net/) || [flwm](https://aur.archlinux.org/packages/flwm/)

*   **[FVWM](/index.php/FVWM "FVWM")** — Extremamente poderoso gerenciador de janela de múltiplas áreas virtuais compatível com ICCCM para o sistema X Window. O desenvolvimento está ativo e o suporte é excelente.

	[http://www.fvwm.org/](http://www.fvwm.org/) || [fvwm](https://www.archlinux.org/packages/?name=fvwm)

*   **[Gala](http://elementaryos.org/journal/meet-gala-window-manager)** — Um belo gerenciador de janela do elementaryos, parte do [Pantheon](/index.php/Pantheon "Pantheon"). Também como gerenciador de composição, baseado no libmutter.

	[https://launchpad.net/gala](https://launchpad.net/gala) || [gala](https://aur.archlinux.org/packages/gala/), [gala-git](https://aur.archlinux.org/packages/gala-git/)

*   **Goomwwm** — Gerenciador de janela X11 implementado em C como um projeto de software de sala limpa. Ele gerencia janelas em um layout flutuante mínimo, enquanto fornece controles orientados por teclado flexíveis para troca de janela, dimensionamento, movimentação, marcação e colocação. Também é rápido, leve, sem modelagem, compatível com Xinerama e compatível com EWMH sempre que possível.

	[https://github.com/seanpringle/goomwwm](https://github.com/seanpringle/goomwwm) || [goomwwm](https://aur.archlinux.org/packages/goomwwm/)

*   **[IceWM](/index.php/IceWM "IceWM")** — Gerenciador de janela para o sistema X Window. O objetivo do IceWM é a velocidade, simplicidade e não ficar no caminho do usuário.

	[https://ice-wm.org/](https://ice-wm.org/) || [icewm](https://www.archlinux.org/packages/?name=icewm)

*   **jbwm** — O jbwm é um gerenciador de janela baseado no evilwm, com um tamanho mínimo de configuração de aproximadamente 16kb, focado no pequeno tamanho binário e na usabilidade, incorporando barras de título opcionais e renderização de fonte de barra de título XFT como opções de tempo de compilação. O jbwm também é mais fácil de usar keybindings do que o evilwm.

	[https://github.com/jefbed/jbwm](https://github.com/jefbed/jbwm) || [jbwm](https://aur.archlinux.org/packages/jbwm/)

*   **[JWM](/index.php/JWM "JWM")** — Gerenciador de janela para o sistema de janelas X11\. O JWM é escrito em C e usa apenas o Xlib no mínimo.

	[https://joewing.net/projects/jwm/index.shtml](https://joewing.net/projects/jwm/index.shtml) || [jwm](https://www.archlinux.org/packages/?name=jwm)

*   **Karmen** — Gerenciador de janela para X, escrito por Johan Veenhuizen. Ele é projetado para "apenas trabalhar". Não há arquivo de configuração nem dependências de bibliotecas além do Xlib. O modelo de foco de entrada é o clicar para focar. Karmen visa o cumprimento do ICCCM e do EWMH.

	[http://karmen.sourceforge.net/](http://karmen.sourceforge.net/) || [karmen](https://aur.archlinux.org/packages/karmen/)

*   **[KWin](https://en.wikipedia.org/wiki/KWin "wikipedia:KWin")** — O gerenciador de janela padrão do KDE, desde o KDE 4.0, vem com a primeira versão do suporte integrado para composição, tornando-o também um gerenciador de composição. Isso permite que a KWin forneça efeitos gráficos avançados, semelhantes ao Compiz, além de fornecer todos os recursos das versões anteriores do KDE (como uma integração muito boa com o KDE, capacidade de configuração avançada, prevenção contra furto de foco, gerenciador de janela bem testado e robusto). manuseio de aplicativos/kits de ferramentas que se comportam mal etc.). Também serve como compositor para [Wayland](/index.php/Wayland_(Portugu%C3%AAs) "Wayland (Português)").

	[https://techbase.kde.org/Projects/KWin](https://techbase.kde.org/Projects/KWin) || [kwin](https://www.archlinux.org/packages/?name=kwin)

*   **lwm** — Gerenciador de janela para o X que tenta se manter fora do seu rosto. Não há ícones, sem barras de botões, sem docks de ícones, sem menus raiz, sem nada: se você quer tudo isso, outros programas podem fornecê-lo. Também não há configurabilidade: se você quiser, você quer um gerenciador de janela diferente; um que ajude o seu sistema operacional em sua conquista maligna de seu espaço de disco e sua anexação de sua memória física.

	[http://www.jfc.org.uk/software/lwm.html](http://www.jfc.org.uk/software/lwm.html) || [lwm](https://www.archlinux.org/packages/?name=lwm)

*   **Marco** — O gerenciador de janela MATE, fork do Metacity.

	[https://github.com/mate-desktop/marco](https://github.com/mate-desktop/marco) || [marco](https://www.archlinux.org/packages/?name=marco)

*   **[Metacity](https://en.wikipedia.org/wiki/Metacity "wikipedia:Metacity")** — Este gerenciador de janela se esforça para ser silencioso, pequeno, estável, continuar com seu trabalho e ficar fora de sua atenção. Ele é usado pelas sessões legadas de flashback do GNOME 2 e do GNOME, e substituído pelo Mutter.

	[https://blogs.gnome.org/metacity/](https://blogs.gnome.org/metacity/) || [metacity](https://www.archlinux.org/packages/?name=metacity)

*   **[Muffin](https://en.wikipedia.org/wiki/Mutter_(software)#Muffin "wikipedia:Mutter (software)")** — O gerenciador de janela e composição do Cinnamon, fork do Mutter, baseado no Clutter, usa o OpenGL. Não pode ser usado fora de canela.

	[https://github.com/linuxmint/muffin/](https://github.com/linuxmint/muffin/) || [muffin](https://www.archlinux.org/packages/?name=muffin)

*   **[Mutter](https://en.wikipedia.org/wiki/Mutter_(window_manager) "wikipedia:Mutter (window manager)")** — O gerenciador de janela e composição do GNOME, baseado no Clutter, usa o OpenGL. Também serve um compositor de Wayland.

	[https://gitlab.gnome.org/GNOME/mutter/](https://gitlab.gnome.org/GNOME/mutter/) || [mutter](https://www.archlinux.org/packages/?name=mutter)

*   **[MWM](https://en.wikipedia.org/wiki/Motif_Window_Manager "wikipedia:Motif Window Manager")** — O Motif Window Manager (MWM) é um gerenciador de janela X baseado no kit de ferramentas Motif.

	[http://sourceforge.net/projects/motif/](http://sourceforge.net/projects/motif/) || [openmotif](https://www.archlinux.org/packages/?name=openmotif)

*   **[Openbox](/index.php/Openbox "Openbox")** — Gerenciador de janela da próxima geração e altamente configurável, com amplo suporte a padrões. O estilo visual *box é bem conhecido por sua aparência minimalista. O Openbox usa o estilo visual *box, enquanto fornece um maior número de opções para desenvolvedores de temas do que implementações anteriores de *box. A documentação do tema descreve a gama completa de opções encontradas nos temas do Openbox.

	[http://openbox.org/](http://openbox.org/) || [openbox](https://www.archlinux.org/packages/?name=openbox)

*   **[pawm](/index.php/Pawm "Pawm")** — Gerenciador de janela para o sistema X Window. Portanto, não é um 'desktop' e não oferece uma enorme pilha de opções inúteis, apenas as facilidades necessárias para executar seus aplicativos X e ao mesmo tempo ter uma interface amigável e fácil de usar.

	[http://www.pleyades.net/pawm/](http://www.pleyades.net/pawm/) || [pawm](https://aur.archlinux.org/packages/pawm/)

*   **[PekWM](/index.php/PekWM "PekWM")** — O gerenciador de janela que antigamente era baseado no gerenciador de janela aewm++, mas evoluiu o suficiente para não mais se assemelhar ao aew++. Ele tem um conjunto de recursos muito expandido, incluindo agrupamento de janelas (semelhante ao Ion, PWM ou Fluxbox), propriedades automáticas, Xinerama, keygrabber que suporta keychains e muito mais.

	[https://www.pekwm.org/](https://www.pekwm.org/) || [pekwm](https://www.archlinux.org/packages/?name=pekwm)

*   **[Sawfish](/index.php/Sawfish "Sawfish")** — Gerenciador de janela extensível usando uma linguagem de script baseada em Lisp. Sua política é muito mínima em comparação com a maioria dos gerenciadores de janelas. Seu objetivo é simplesmente gerenciar janelas da maneira mais flexível e atraente possível. Todas as funções WM de alto nível são implementadas em Lisp para futura extensibilidade ou redefinição.

	[http://sawfish.wikia.com/wiki/Main_Page](http://sawfish.wikia.com/wiki/Main_Page) || [sawfish](https://aur.archlinux.org/packages/sawfish/)

*   **TinyWM** — Gerenciador de janela minúsculo criado como um exercício de minimalismo. Pode ser útil aprender algumas das noções básicas de como criar um gerenciador de janela. É composto de aproximadamente 50 linhas de C. Há também uma versão do Python usando python-xlib.

	[http://incise.org/tinywm.html](http://incise.org/tinywm.html) || [tinywm](https://aur.archlinux.org/packages/tinywm/) [tinywm-git](https://aur.archlinux.org/packages/tinywm-git/)

*   **[twm](/index.php/Twm "Twm")** — Gerenciador de janela para o sistema X Window. Ele fornece barras de título, janelas de forma, várias formas de gerenciamento de ícone, funções de macro definidas pelo usuário, foco no teclado de clique para tipo e ponteiro e ligações de botão de ponteiro e tecla especificada pelo usuário.

	[https://cgit.freedesktop.org/xorg/app/twm/](https://cgit.freedesktop.org/xorg/app/twm/) || [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm)

*   **[UWM](https://en.wikipedia.org/wiki/UDE "wikipedia:UDE")** — O gerenciador de janela final para a UDE.

	[http://udeproject.sourceforge.net/](http://udeproject.sourceforge.net/) || [ude](https://aur.archlinux.org/packages/ude/)

*   **WindowLab** — Gerenciador de janela pequeno e simples com design inovador. Ele tem uma política de clique para focar, mas não para aumentar o foco, um mecanismo de redimensionamento de janela que permite que uma ou várias bordas de uma janela sejam alteradas em uma ação e uma barra de menu inovadora que compartilhe a mesma parte da tela. a barra de tarefas. As barras de título da janela são impedidas de sair da borda da tela restringindo o ponteiro do mouse e, quando apropriado, o ponteiro também é restringido à barra de tarefas/barra de menu para facilitar a execução dos itens de menu de destino.

	[https://github.com/nickgravgaard/windowlab](https://github.com/nickgravgaard/windowlab) || [windowlab](https://aur.archlinux.org/packages/windowlab/)

*   **[Window Maker](/index.php/Window_Maker "Window Maker")** — Gerenciador de janela X11 originalmente projetado para fornecer suporte de integração para o GNUstep Desktop Environment. De todas as formas possíveis, reproduz a aparência elegante da interface de usuário NEXTSTEP. É rápido, rico em recursos, fácil de configurar e fácil de usar. Também é software livre, com contribuições feitas por programadores de todo o mundo.

	[https://windowmaker.org/](https://windowmaker.org/) || [windowmaker](https://aur.archlinux.org/packages/windowmaker/)

*   **WM2** — Gerenciador de janela para X. Ele oferece um estilo incomum de decoração de janelas e pouca funcionalidade com a qual seu autor se sente confortável em um gerenciador de janela. wm2 não é configurável, exceto por editar o fonte e recompilar o código, e é realmente destinado a pessoas que não querem particularmente que seu gerenciador de janela seja muito amigável.

	[http://www.all-day-breakfast.com/wm2/](http://www.all-day-breakfast.com/wm2/) || [wm2](https://aur.archlinux.org/packages/wm2/)

*   **[Xfwm](/index.php/Xfwm "Xfwm")** — O gerenciador de janela [Xfce](/index.php/Xfce_(Portugu%C3%AAs) "Xfce (Português)") gerencia a colocação de janelas de aplicativos na tela, fornece belas decorações de janelas, gerencia espaços de trabalho ou desktops virtuais e suporta nativamente o modo de várias telas. Ele fornece seu próprio gerenciador de composição (da extensão X.Org Composite) para transparência e sombras verdadeiras. O gerenciador de janela do Xfce também inclui um editor de atalhos de teclado para comandos específicos do usuário e manipulações básicas do Windows e fornece um diálogo de preferências para ajustes avançados.

	[https://docs.xfce.org/xfce/xfwm4/start](https://docs.xfce.org/xfce/xfwm4/start) || [xfwm4](https://www.archlinux.org/packages/?name=xfwm4)

### Gerenciadores de janela de tiling

*   **[Bspwm](/index.php/Bspwm "Bspwm")** — bspwm is a tiling window manager that represents windows as the leaves of a full binary tree. It has support for EWMH and multiple monitors, and is configured and controlled through messages.

	[https://github.com/baskerville/bspwm](https://github.com/baskerville/bspwm) || [bspwm](https://www.archlinux.org/packages/?name=bspwm)

*   **[EXWM](/index.php/EXWM "EXWM")** — EXWM (Emacs X Window Manager) is a full-featured tiling X window manager for Emacs built on top of XELB. It features fully keyboard-driven operations, hybrid layout modes (tiling & stacking), dynamic workspace support, ICCCM/EWMH compliance, RandR (multi-monitor) support, and a built-in system tray.

	[https://github.com/ch11ng/exwm](https://github.com/ch11ng/exwm) || [emacs-exwm-git](https://aur.archlinux.org/packages/emacs-exwm-git/)

*   **[Herbstluftwm](/index.php/Herbstluftwm "Herbstluftwm")** — Manual tiling window manager for X11 using Xlib and Glib. The layout is based on splitting frames into subframes which can be split again or can be filled with windows (similar to i3/ musca). Tags (or workspaces or virtual desktops or …) can be added/removed at runtime. Each tag contains its own layout. Exactly one tag is viewed on each monitor. The tags are monitor independent (similar to xmonad). It is configured at runtime via ipc calls from herbstclient. So the configuration file is just a script which is run on startup. (similar to wmii/musca).

	[https://herbstluftwm.org](https://herbstluftwm.org) || [herbstluftwm](https://www.archlinux.org/packages/?name=herbstluftwm)

*   **howm** — A lightweight, tiling X11 window manager that mimics vi by offering operators, motions and modes. Configuration is done through the included `config.h` file.

	[https://github.com/HarveyHunt/howm](https://github.com/HarveyHunt/howm) || [howm-x11](https://aur.archlinux.org/packages/howm-x11/)

*   **[i3](/index.php/I3 "I3")** — Tiling window manager, completely written from scratch. i3 was created because wmii, our favorite window manager at the time, did not provide some features we wanted (multi-monitor done right, for example), had some bugs, did not progress for quite some time, and was not easy to hack at all (source code comments/documentation completely lacking). Notable differences are in the areas of multi-monitor support and the tree metaphor. For speed the Plan 9 interface of wmii is not implemented.

	[https://i3wm.org/](https://i3wm.org/) || [i3-wm](https://www.archlinux.org/packages/?name=i3-wm)

*   **[Ion3](/index.php/Ion3 "Ion3")** — Tiling tabbed X11 window manager designed with keyboard users in mind. It was one of the first of the “new wave" of tiling windowing environments (the other being LarsWM, with quite a different approach) and has since spawned an entire category of tiling window managers for X11 – none of which really manage to reproduce the feel and functionality of Ion. It uses Lua as an embedded interpreter which handles all of the configuration.

	[http://tuomov.iki.fi/software](http://tuomov.iki.fi/software) || [ion3](https://aur.archlinux.org/packages/ion3/)

*   **[Notion](/index.php/Notion "Notion")** — Tiling, tabbed window manager for the X window system that utilizes 'tiles' and 'tabbed' windows.
    *   Tiling: you divide the screen into non-overlapping 'tiles'. Every window occupies one tile, and is maximized to it
    *   Tabbing: a tile may contain multiple windows - they will be 'tabbed'.
    *   Static: most tiled window managers are 'dynamic', meaning they automatically resize and move around tiles as windows appear and disappear. Notion, by contrast, does not automatically change the tiling.

	Notion is a fork of Ion3.

	[http://notion.sf.net/](http://notion.sf.net/) || [notion](https://www.archlinux.org/packages/?name=notion)

*   **[Ratpoison](/index.php/Ratpoison "Ratpoison")** — Simple Window Manager with no fat library dependencies, no fancy graphics, no window decorations, and no rodent dependence. It is largely modeled after GNU Screen which has done wonders in the virtual terminal market. Ratpoison is configured with a simple text file. The information bar in Ratpoison is somewhat different, as it shows only when needed. It serves as both an application launcher as well as a notification bar. Ratpoison does not include a system tray.

	[http://www.nongnu.org/ratpoison/](http://www.nongnu.org/ratpoison/) || [ratpoison](https://www.archlinux.org/packages/?name=ratpoison)

*   **[Stumpwm](/index.php/Stumpwm "Stumpwm")** — Tiling, keyboard driven X11 Window Manager written entirely in Common Lisp. Stumpwm attempts to be customizable yet visually minimal. It does have various hooks to attach your personal customizations, and variables to tweak, and can be reconfigured and reloaded while running. There are no window decorations, no icons, no buttons, and no system tray. Its information bar can be set to show constantly or only when needed.

	[https://stumpwm.github.io/](https://stumpwm.github.io/) || [stumpwm-git](https://aur.archlinux.org/packages/stumpwm-git/)

*   **[subtle](/index.php/Subtle "Subtle")** — Manual tiling window manager with a rather uncommon approach of tiling: Per default there is no typical layout enforcement, windows are placed on a position (gravity) in a custom grid. The user can change the gravity of each window either directly per grabs or with rules defined by tags in the config. It has workspace tags and automatic client tagging, mouse and keyboard control as well as an extendable statusbar.

	[http://subforge.org/projects/subtle](http://subforge.org/projects/subtle) || [subtle-git](https://aur.archlinux.org/packages/subtle-git/)

*   **[sway](/index.php/Sway_(Portugu%C3%AAs) "Sway (Português)")** — Sway is a drop-in replacement for the i3 window manager, but for Wayland instead of X11\. It works with your existing i3 configuration and supports most of i3's features, and a few extras.

	[http://swaywm.org/](http://swaywm.org/) || [sway](https://www.archlinux.org/packages/?name=sway)

*   **way-cooler** — Way Cooler is a tiling Wayland window manager, written in Rust, configurable using Lua, and extendable with D-Bus.

	[http://way-cooler.org/](http://way-cooler.org/) || [way-cooler](https://aur.archlinux.org/packages/way-cooler/)

*   **[WMFS](/index.php/WMFS "WMFS")** — Window Manager From Scratch is a lightweight and highly configurable tiling window manager for X. It can be configured with a configuration file, supports Xft (FreeType) fonts and is compliant with the Extended Window Manager Hints (EWMH) specifications, Xinerama and Xrandr. WMFS can be driven with Vi based commands (ViWMFS).

	[https://github.com/xorg62/wmfs](https://github.com/xorg62/wmfs) || [wmfs](https://aur.archlinux.org/packages/wmfs/)

*   **[WMFS2](/index.php/WMFS2 "WMFS2")** — Incompatible successor of WMFS. It's even more minimalistic and brings some new stuff.

	[https://github.com/xorg62/wmfs](https://github.com/xorg62/wmfs) || [wmfs2-git](https://aur.archlinux.org/packages/wmfs2-git/)

### Gerenciadores de janela dinâmicos

*   **[awesome](/index.php/Awesome "Awesome")** — Highly configurable, next generation framework window manager for X. It is very fast, extensible and licensed under the GNU GPLv2 license. Configured in Lua, it has a system tray, information bar, and launcher built in. There are extensions available to it written in Lua. Awesome uses XCB as opposed to Xlib, which may result in a speed increase. Awesome has other features as well, such as an early replacement for notification-daemon, a right-click menu similar to that of the *box window managers, and many other things.

	[https://awesomewm.org/](https://awesomewm.org/) || [awesome](https://www.archlinux.org/packages/?name=awesome)

*   **[catwm](/index.php/Catwm "Catwm")** — Small window manager, even simpler than dwm, written in C. Configuration is done by modifying the config.h file and recompiling.

	[https://github.com/pyknite/catwm](https://github.com/pyknite/catwm) || [catwm-git](https://aur.archlinux.org/packages/catwm-git/)

*   **[dwm](/index.php/Dwm "Dwm")** — Dynamic window manager for X. It manages windows in tiled, monocle and floating layouts. All of the layouts can be applied dynamically, optimising the environment for the application in use and the task performed. does not include a tray app or automatic launcher, although dmenu integrates well with it, as they are from the same author. It has no text configuration file. Configuration is done entirely by modifying the C source code, and it must be recompiled and restarted each time it is changed.

	[http://dwm.suckless.org/](http://dwm.suckless.org/) || [dwm](https://aur.archlinux.org/packages/dwm/)

*   **[echinus](/index.php/Echinus "Echinus")** — Simple and lightweight tiling and floating window manager for X11\. Started as a dwm fork with easier configuration, echinus became full-featured re-parenting window manager with EWMH support. It has an EWMH-compatible panel/taskbar, called [ourico](https://aur.archlinux.org/packages/ourico/).

	[http://plhk.ru](http://plhk.ru) || [echinus](https://aur.archlinux.org/packages/echinus/)

*   **[FrankenWM](/index.php/FrankenWM "FrankenWM")** — Basically monsterwm with floating done right. Features that are added on top of basic mwm include: more layouts (fibonacci, equal stack, dual stack), gaps (and borders) are adjustable on the fly, minimize/maximize single windows, hide/show all windows, resizing master and stack individually, invert stack.

	[https://github.com/sulami/FrankenWM](https://github.com/sulami/FrankenWM) || [frankenwm-git](https://aur.archlinux.org/packages/frankenwm-git/)

*   **[spectrwm](/index.php/Spectrwm "Spectrwm")** — Small dynamic tiling window manager for X11, largely inspired by xmonad and dwm. It tries to stay out of the way so that valuable screen real estate can be used for much more important stuff. It has sane defaults and is configured with a text file. It was written by hackers for hackers and it strives to be small, compact and fast. It has a built-in status bar fed from a user-defined script.

	[https://github.com/conformal/spectrwm/](https://github.com/conformal/spectrwm/) || [spectrwm](https://www.archlinux.org/packages/?name=spectrwm)

*   **[Qtile](/index.php/Qtile "Qtile")** — Full-featured, hackable tiling window manager written in Python. Qtile is simple, small, and extensible. It's easy to write your own layouts, widgets, and built-in commands.It is written and configured entirely in Python, which means you can leverage the full power and flexibility of the language to make it fit your needs.

	[https://github.com/qtile/qtile](https://github.com/qtile/qtile) || [qtile](https://www.archlinux.org/packages/?name=qtile)

*   **[wmii](/index.php/Wmii "Wmii")** — Small, dynamic window manager for X11\. It is scriptable, has a 9P filesystem interface and supports classic and tiling (Acme-like) window management. It aims to maintain a small and clean (read hackable and beautiful) codebase. The default configuration is in bash and [rc (the Plan 9 shell)](http://rc.cat-v.org), but programs exist written in ruby, and any program that can work with text can configure it. It has a status bar and launcher built in, and also an optional system tray (`witray`).

	[http://wmii.suckless.org/](http://wmii.suckless.org/) || [wmii](https://aur.archlinux.org/packages/wmii/)

*   **[xmonad](/index.php/Xmonad "Xmonad")** — Dynamically tiling X11 window manager that is written and configured in Haskell. In a normal WM, you spend half your time aligning and searching for windows. Xmonad makes work easier, by automating this. XMonad is configured in Haskell. For all configuration changes, xmonad must be recompiled, so the Haskell compiler (over 100MB) must be installed. A large library called [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) provides many additional features

	[http://xmonad.org/](http://xmonad.org/) || [xmonad](https://www.archlinux.org/packages/?name=xmonad)

## Veja também

*   [http://www.gilesorr.com/wm/](http://www.gilesorr.com/wm/)
*   [http://www.slant.co/topics/390/~what-are-the-best-window-managers-for-linux/](http://www.slant.co/topics/390/~what-are-the-best-window-managers-for-linux/)
*   [https://l3net.wordpress.com/2013/03/17/a-memory-comparison-of-light-linux-desktops/](https://l3net.wordpress.com/2013/03/17/a-memory-comparison-of-light-linux-desktops/)
*   [http://www.xwinman.org/others.php](http://www.xwinman.org/others.php)