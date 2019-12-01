**Status de tradução:** Esse artigo é uma tradução de [Wayland](/index.php/Wayland "Wayland"). Data da última tradução: 2019-11-25\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Wayland&diff=0&oldid=590154) na versão em inglês.

Artigos relacionados

*   [KMS](/index.php/KMS "KMS")
*   [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)")

[Wayland](https://wayland.freedesktop.org/) é um protocolo para um [gerenciador de janelas de composição](https://en.wikipedia.org/wiki/Compositing_window_manager and [KDE](/index.php/KDE_(Portugu%C3%AAs) "KDE (Português)"). Existe também uma implementação referência de compositor chamada [Weston](/index.php/Weston "Weston"). XWayland provê uma camada de compatibilidade para rodar programas [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") em Wayland.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Requerimentos](#Requerimentos)
*   [2 Compositores](#Compositores)
*   [3 Gerenciadores de login](#Gerenciadores_de_login)
*   [4 Bibliotecas GUI](#Bibliotecas_GUI)
    *   [4.1 GTK 3](#GTK_3)
    *   [4.2 Qt 5](#Qt_5)
    *   [4.3 Clutter](#Clutter)
    *   [4.4 SDL2](#SDL2)
    *   [4.5 GLFW](#GLFW)
    *   [4.6 GLEW](#GLEW)
    *   [4.7 EFL](#EFL)
*   [5 Solução de problemas](#Solução_de_problemas)
    *   [5.1 GDM e drivers proprietários da NVIDIA](#GDM_e_drivers_proprietários_da_NVIDIA)
    *   [5.2 Gama](#Gama)
    *   [5.3 Falha de afirmação LLVM](#Falha_de_afirmação_LLVM)
    *   [5.4 Tela lenta, glitches gráficos, e crashes](#Tela_lenta,_glitches_gráficos,_e_crashes)
    *   [5.5 Cannot open display: :0 com programas feitos em Electron](#Cannot_open_display:_:0_com_programas_feitos_em_Electron)
    *   [5.6 Gravar tela](#Gravar_tela)
    *   [5.7 Exibição remota](#Exibição_remota)
    *   [5.8 Captação de entradas nos jogos, desktop remoto e janelas VM](#Captação_de_entradas_nos_jogos,_desktop_remoto_e_janelas_VM)
        *   [5.8.1 Protocolo inibidor de entrada wlroots](#Protocolo_inibidor_de_entrada_wlroots)
*   [6 Veja também](#Veja_também)

## Requerimentos

A maioria do compositores Wayland somente funcionam em sistemas que usam [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). Wayland por si só não provê um ambiente gráfico; para isto você também precisa de um compositor como [Weston](/index.php/Weston "Weston") ou [Sway](/index.php/Sway_(Portugu%C3%AAs) "Sway (Português)"), ou um ambiente desktop que inclui um, como [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") ou [KDE](/index.php/KDE_(Portugu%C3%AAs) "KDE (Português)").

Para o driver GPU e o compositor Wayland serem compatíveis eles devem suportar a mesma buffer API. Existem duas principais APIs: [GBM](https://en.wikipedia.org/wiki/Generic_Buffer_Management "wikipedia:Generic Buffer Management") e [EGLStreams](https://www.phoronix.com/scan.php?page=news_item&px=XDC2016-Device-Memory-API).

| Buffer API | Suporte de driver GPU | Suporte de compositores Wayland |
| GBM | Todos exceto [NVIDIA](/index.php/NVIDIA "NVIDIA") | Todos |
| EGLStreams | [NVIDIA](/index.php/NVIDIA "NVIDIA") | [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"), [KDE](/index.php/KDE_(Portugu%C3%AAs) "KDE (Português)") |

## Compositores

| Nome | Tipo | Descrição |
| GNOME | Stacking | Veja [GNOME#Iniciando](/index.php/GNOME_(Portugu%C3%AAs)#Iniciando "GNOME (Português)"). |
| sway | Tiling | [Sway](/index.php/Sway_(Portugu%C3%AAs) "Sway (Português)") é um compositor e gerenciador de janelas compatível com o i3 para Wayland. [GitHub](https://github.com/SirCmpwn/sway). |
| Enlightenment | Stacking e tiling | [Mais informações sobre](https://www.enlightenment.org/about-wayland). |
| KDE Plasma | Stacking | Veja [KDE#Iniciando o Plasma](/index.php/KDE_(Portugu%C3%AAs)#Iniciando_o_Plasma "KDE (Português)"). |
| Orbment | Tiling | [orbment](https://github.com/Cloudef/orbment) (antiga loliwm) é um projeto abandonado de tiling WM para Wayland. |
| Velox | Tiling | [Velox](/index.php/Velox "Velox") é um gerenciador de janelas simples baseado no swc. É inspirado por [dwm](/index.php/Dwm "Dwm") e [xmonad](/index.php/Xmonad "Xmonad"). |
| Orbital | Stacking | [Orbital](https://github.com/giucam/orbital) é um compositor Wayland e shell(mais semelhante a uma WM do que DE) usando Qt5 e Weston. O objetivo do projeto é construir um simples mas flexível e bonito desktop Wayland. |
| Liri Shell | Stacking | [Liri Shell](https://github.com/lirios/shell) É um shell para [Liri](/index.php/Liri "Liri"), construído com QtQuick e QtCompositor como um compositor para Wayland. |
| Maynard | *(Incerto)* | [Maynard](https://github.com/raspberrypi/maynard) é um cliente shell desktop para Weston feito em GTK. Foi baseado no weston-gtk-shell, um projeto de Tiago Vignatti. Não está em desenvolvimento. [[1]](https://github.com/raspberrypi/maynard/issues/54#issuecomment-303422302)[[2]](https://github.com/raspberrypi/maynard/issues/55#issuecomment-373808518) |
| Motorcar | *(Incerto)* | [Motorcar](https://github.com/evil0sheep/motorcar) é um compositor Wayland para exploração de janelas 3D usando realidade virtual. |
| Way Cooler | Tiling | [Way Cooler](https://github.com/way-cooler/way-cooler) é um customizável (arquivos de configuração em Lua) compositor Wayland, escrito em Rust. Inspirado pelo i3 e awesome. |
| Maze Compositor | Flutuante 3D | [Maze Compositor](https://github.com/imbavirus/mazecompositor) é um compositor Wayland 3D feito em Qt. |
| Cage | Kiosk | [Cage](https://www.hjdskes.nl/projects/cage/) é um compositor Wayland que mostra somente um programa em tela cheia. |
| Greenfield | Stacking | [Greenfield](https://github.com/udevbe/greenfield) é um compositor Wayland que roda no navegador e pode mostrar aplicações remotamente. |
| Grefsen | Flutuante | [Grefsen](https://github.com/ec1oud/grefsen) é um compositor Qt/Wayland que oferece um desktop mínimo. |
| Waymonad | Tiling | [Waymonad](https://github.com/waymonad/waymonad) é um compositor Wayland inspirado e baseado nas ideias do xmonad. |
| wayfire | Stacking | [Wayfire](https://github.com/WayfireWM/wayfire) é um compositor de propósito geral. |
| Weston | Floating | [Weston](/index.php/Weston "Weston") é uma implementação referência de compositor Wayland. |

Alguns destes acima podem ser suportados por [gerenciadores de janela](/index.php/Gerenciadores_de_janela "Gerenciadores de janela"). Cheque `/usr/share/wayland-sessions/*compositor*.desktop` para saber como eles são iniciados.

## Gerenciadores de login

Abaixo estão listados gerenciadores de login que suportam rodar compositores Wayland. A coluna Tipo indica se o gerenciador de login suporta ou não ser executado em Wayland.

| Nome | Tipo | Descrição |
| GDM | Roda em Wayland | Gerenciador de login do [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"). |
| LightDM | Roda em X11 | Gerenciador de login TUI escrito em C |
| Ly | Roda no console | TUI display manager written in C |
| SDDM | Roda em X11 | Gerenciador de login feito em QML. |

## Bibliotecas GUI

Veja detalhes no [site oficial](https://wayland.freedesktop.org/toolkits.html).

### GTK 3

O pacote [gtk3](https://www.archlinux.org/packages/?name=gtk3) tem o backend Wayland já habilitado. GTK irá ser executado por padrão em Wayland, mas é possível sobrescrever isto para Xwayland ao modificar a variável de ambiente: `GDK_BACKEND=x11`.

### Qt 5

Para habilitar o suporte para Wayland no Qt 5, instale o pacote [qt5-wayland](https://www.archlinux.org/packages/?name=qt5-wayland).

Para rodar um programa Qt 5 com o plugin Wayland [[3]](https://wiki.qt.io/QtWayland#How_do_I_use_QtWayland.3F), use [variáveis de ambiente](/index.php/Vari%C3%A1veis_de_ambiente "Variáveis de ambiente") `-platform wayland` ou `QT_QPA_PLATFORM=wayland-egl`. Para forçar o uso do [X11](/index.php/X11_(Portugu%C3%AAs) "X11 (Português)") numa sessão Wayland, use `QT_QPA_PLATFORM=xcb`.

### Clutter

O toolkit Clutter suporta o backend Wayland e isto possibilita que ele rode como um cliente Wayland. O backend já é habilitado por padrão no pacote [clutter](https://www.archlinux.org/packages/?name=clutter).

Para rodar um programa Clutter em Wayland, defina: `CLUTTER_BACKEND=wayland`.

### SDL2

Para rodar um programa SDL2 no Wayland, defina `SDL_VIDEODRIVER=wayland`.

**Nota:** Muitos jogos proprietários vem com versões antigas do SDL, que não suportam Wayland e podem deixar de funcionar se você definir `SDL_VIDEODRIVER=wayland`. Para forçar o programa a rodar com Xwayland, defina `SDL_VIDEODRIVER=x11`.

### GLFW

Para usar GLFW com o backend Wayland, instale o pacote [glfw-wayland](https://www.archlinux.org/packages/?name=glfw-wayland) (ao invés do [glfw-x11](https://www.archlinux.org/packages/?name=glfw-x11)).

### GLEW

Para usar GLEW com o backend Wayland, instale o pacote [glew-wayland](https://www.archlinux.org/packages/?name=glew-wayland) (ao invés do [glew](https://www.archlinux.org/packages/?name=glew)).

### EFL

EFL tem suporte completo ao Wayland. Para rodar um programa EFL no Wayland, veja a [página do projeto](https://wayland.freedesktop.org/efl.html).

## Solução de problemas

### GDM e drivers proprietários da NVIDIA

Se você estiver usando o driver proprietário da [NVIDIA](/index.php/NVIDIA "NVIDIA"), o [GDM](/index.php/GDM_(Portugu%C3%AAs) "GDM (Português)") explicitamente [desabilita](https://bbs.archlinux.org/viewtopic.php?pid=1837424#p1837424) o suporte a Wayland. O [motivo](https://gitlab.gnome.org/GNOME/gdm/commit/5cd78602d3d4c8355869151875fc317e8bcd5f08) para esta decisão é que os aplicativos GLX atualmente não funcionam bem quando o driver proprietário da NVIDIA é usado com uma sessão de Wayland.

Para habilitar forçadamente o Wayland, desabilite a regra de [udev](/index.php/Udev "Udev") responsável por desabilitar o Wayland no GDM:

```
# ln -s /dev/null /etc/udev/rules.d/61-gdm.rules

```

### Gama

Enquanto [Redshift](/index.php/Redshift "Redshift") não suporta Wayland (sem um patch) é possível aplicar a temperatura desejada no [tty](/index.php/Tty "Tty") antes de iniciar o compositor. Por exemplo:

```
redshift -m drm -PO 3000

```

Apesar disso alguns compositores possuem essa funcionalidade enquanto rodam:

*   [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") possui funcionalidade como [Redshift](/index.php/Redshift "Redshift") e suporta o Wayland. Habilite [Luz noturna](/index.php/GNOME_(Portugu%C3%AAs)#Luz_noturna "GNOME (Português)") nas suas configurações de tela.
*   De mesmo modo, [KDE Plasma](/index.php/KDE_Plasma_(Portugu%C3%AAs) "KDE Plasma (Português)") também oferece *Cor Noturna*.
*   No Sway 1.0 e outros compositores baseados no wlroots, o [redshift-wlr-gamma-control-git](https://aur.archlinux.org/packages/redshift-wlr-gamma-control-git/) pode ser usado.
*   No Orbital, [redshift-wayland-git](https://aur.archlinux.org/packages/redshift-wayland-git/) pode ser usado.

### Falha de afirmação LLVM

Se você receber uma falha de afirmação LLVM (LLVM assertion failure), você precisa recompilar [mesa](https://www.archlinux.org/packages/?name=mesa) sem Gallium LLVM até que este problema seja consertado.

Isto pode implicar na desativação de alguns drivers que precisam do LLVM. Você pode também tentar exportar o seguinte, se tiver problemas com drivers de hardware:

```
$ export EGL_DRIVER=/usr/lib/egl/egl_gallium.so

```

### Tela lenta, glitches gráficos, e crashes

Usuários do gnome-shell podem sofrer problemas na tela quando eles mudam para Wayland do X. Uma das causas desse problema pode ser o `CLUTTER_PAINT=disable-clipped-redraws:disable-culling` definido para o gnome-shell baseado no Xorg. Tente remover isto do `/etc/environment` ou outros arquivos rc para ver se tudo volta ao normal.

### Cannot open display: :0 com programas feitos em Electron

Tenha certeza que você não definiu GDK_BACKEND=wayland. Definir isso globalmente irá quebrar programas Electron.

### Gravar tela

[green-recorder](https://aur.archlinux.org/packages/green-recorder/), [obs-gnome-screencast](https://aur.archlinux.org/packages/obs-gnome-screencast/) e [obs-xdg-portal-git](https://aur.archlinux.org/packages/obs-xdg-portal-git/) suportam gravar a tela no Wayland usando uma funcionalidade do GNOME.

[wf-recorder-git](https://aur.archlinux.org/packages/wf-recorder-git/) é um gravador de tela para compositores baseados no wlroots.

[wlrobs-hg](https://aur.archlinux.org/packages/wlrobs-hg/) é um plugin do [obs-studio](https://www.archlinux.org/packages/?name=obs-studio) que lhe permite capturar a tela em compositores baseados no wlroots.

### Exibição remota

*   (20190503) [wlroots](https://www.archlinux.org/packages/?name=wlroots) (usado por [Sway](/index.php/Sway_(Portugu%C3%AAs) "Sway (Português)")) oferece um backend RDP desde a versão 0.6[[4]](https://github.com/swaywm/wlroots/blob/master/docs/env_vars.md).
*   (20180401) [mutter](https://www.archlinux.org/packages/?name=mutter) tem agora desktop remoto habilitado no tempo de compilação, veja [[5]](https://wiki.gnome.org/Projects/Mutter/RemoteDesktop) e [gnome-remote-desktop](https://www.archlinux.org/packages/?name=gnome-remote-desktop) para detalhes.
*   Existe um merge do FreeRDP no Weston em 2013, habilitado com uma flag de compilação. O pacote [weston](https://www.archlinux.org/packages/?name=weston) vem com isso habilitado desde a versão 6.0.0.
*   [waypipe-git](https://aur.archlinux.org/packages/waypipe-git/) é um proxy transparente para programas Wayland, com um comando que roda via [SSH](/index.php/Secure_Shell_(Portugu%C3%AAs) "Secure Shell (Português)").

### Captação de entradas nos jogos, desktop remoto e janelas VM

Diferente do Xorg, Wayland não permite captação exclusiva de entrada, também conhecido como captação ativa ou explicita (exemplo [teclado](https://tronche.com/gui/x/xlib/input/XGrabKeyboard.html), [mouse](https://tronche.com/gui/x/xlib/input/XGrabPointer.html)), ao invés disso, depende do compositor Wayland para direcionar os atalhos do teclado e confinar o ponteiro para a janela do programa.

Esta mudança na captação de entrada quebra o atual comportamento dos programas:

*   Combinação de teclas e modificadores irão ser pegos pelo compositor e não serão enviados para o desktop remoto e janelas de máquina virtual.
*   O mouse não irá ser restrito a janela da aplicação, isto pode causar um efeito de paralaxe onde a localização do ponteiro dentro da janela da máquina virtual ou desktop remoto é mal interpretado do host.

Isto é resolvido adicionando extensões para o protocolo Wayland e XWayland. O suporte para estas extensões precisam ser adicionados para compositores Wayland. Os clientes nativos do Wayland, toolkits widget (exemplo GTK, QT) ou as próprias aplicações, se nenhum toolkit está sendo usado, também precisam suportar estas extensões. Programas Xorg não precisam de mudança devido a existência do XWayland.

Estas extensões já estão incluídas no [wayland-protocols](https://www.archlinux.org/packages/?name=wayland-protocols), e suportadas por [xorg-server-xwayland](https://www.archlinux.org/packages/?name=xorg-server-xwayland) 1.20.

Extensões relacionadas são:

*   [XWayland keyboard grabbing protocol](https://cgit.freedesktop.org/wayland/wayland-protocols/tree/unstable/xwayland-keyboard-grab/xwayland-keyboard-grab-unstable-v1.xml)
*   [Compositor shortcuts inhibit protocol](https://cgit.freedesktop.org/wayland/wayland-protocols/tree/unstable/keyboard-shortcuts-inhibit/keyboard-shortcuts-inhibit-unstable-v1.xml)
*   [Relative pointer protocol](https://cgit.freedesktop.org/wayland/wayland-protocols/tree/unstable/relative-pointer/relative-pointer-unstable-v1.xml)
*   [Pointer constraints protocol](https://cgit.freedesktop.org/wayland/wayland-protocols/tree/unstable/pointer-constraints/pointer-constraints-unstable-v1.xml)

Compositores Wayland que suportam:

*   Mutter, compositor do [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") [desde versão 3.28](https://bugzilla.gnome.org/show_bug.cgi?id=783342).

Toolkits widget que suportam:

*   GTK desde a versão 3.22.18.

#### Protocolo inibidor de entrada wlroots

[Inibidor de entrada](https://github.com/swaywm/wlr-protocols/blob/master/unstable/wlr-input-inhibitor-unstable-v1.xml) é um protocolo Wayland feito pelos desenvolvedores do Sway e wlroots que conflita com `Compositor shortcuts inhibit`.
Sway e wlroots não suportam os protocolos `Compositor shortcuts inhibit` e `XWayland keyboard grabbing`, aparentemente eles são contra adicionar suporte ao último [[6]](https://github.com/swaywm/wlroots/pull/635#issuecomment-366385856) [[7]](https://github.com/swaywm/wlroots/issues/624#issuecomment-367276476).
Não é conhecido nenhum toolkit widget ou programa que suporta este protocolo.

## Veja também

*   [Artigo sobre depuração de Wayland no Fedora Wiki](https://fedoraproject.org/wiki/How_to_debug_Wayland_problems)
*   [Temas de cursor](/index.php/Temas_de_cursor "Temas de cursor")
*   [Discussão no fórum do Arch Linux](https://bbs.archlinux.org/viewtopic.php?id=107499)
*   [Documentação online do Wayland](https://wayland.freedesktop.org/docs/html/)