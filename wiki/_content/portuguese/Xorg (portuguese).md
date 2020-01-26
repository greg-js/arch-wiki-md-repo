**Status de tradução:** Esse artigo é uma tradução de [Xorg](/index.php/Xorg "Xorg"). Data da última tradução: 2020-01-20\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Xorg&diff=0&oldid=594367) na versão em inglês.

Artigos relacionados

*   [Inicialização automática](/index.php/Inicializa%C3%A7%C3%A3o_autom%C3%A1tica "Inicialização automática")
*   [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição")
*   [Gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela")
*   [Configuração de fontes](/index.php/Font_configuration "Font configuration")
*   [Temas de cursor](/index.php/Temas_de_cursor "Temas de cursor")
*   [Ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop")
*   [Wayland](/index.php/Wayland_(Portugu%C3%AAs) "Wayland (Português)")
*   [xinit](/index.php/Xinit_(Portugu%C3%AAs) "Xinit (Português)")
*   [xrandr](/index.php/Xrandr "Xrandr")

Da [https://www.x.org/wiki/](https://www.x.org/wiki/):

	O projeto X.Org oferece uma implementação de código aberto do [Sistema de janelas X](https://en.wikipedia.org/wiki/pt:X_Window_System "wikipedia:pt:X Window System"). O desenvolvimento é realizado em conjunto com a comunidade freedesktop.org. X.org é uma corporação educacional sem fins lucrativos, liderada pelo conselho e membros do projeto.

**Xorg** (normalmente chamado de **X**) é o servidor de exibição mais popular entre os usuários do Linux. Sua onipresença lhe fez um pré-requisito para programas GUI, Isto resultou em uma massiva adoção na maioria das distribuições Linux. Veja a página do Wikipédia [Xorg](https://en.wikipedia.org/wiki/pt:X.Org_Server "wikipedia:pt:X.Org Server") ou visite o [site do Xorg](https://www.x.org/wiki/) para mais informações.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
    *   [1.1 Instalação de driver](#Instalação_de_driver)
    *   [1.2 AMD](#AMD)
*   [2 Iniciando](#Iniciando)
*   [3 Configuração](#Configuração)
    *   [3.1 Usando arquivos .conf](#Usando_arquivos_.conf)
    *   [3.2 Usando xorg.conf](#Usando_xorg.conf)
*   [4 Dispositivos de entrada](#Dispositivos_de_entrada)
    *   [4.1 Identificação de entrada](#Identificação_de_entrada)
    *   [4.2 Aceleração do mouse](#Aceleração_do_mouse)
    *   [4.3 Botões adicionais do mouse](#Botões_adicionais_do_mouse)
    *   [4.4 Touchpad](#Touchpad)
    *   [4.5 Toque de tela](#Toque_de_tela)
    *   [4.6 Configurações do teclado](#Configurações_do_teclado)
*   [5 Configurações do monitor](#Configurações_do_monitor)
    *   [5.1 Configuração manual](#Configuração_manual)
    *   [5.2 Múltiplos monitores](#Múltiplos_monitores)
        *   [5.2.1 Mais de uma placa de vídeo](#Mais_de_uma_placa_de_vídeo)
    *   [5.3 Tamanho da tela e DPI](#Tamanho_da_tela_e_DPI)
        *   [5.3.1 Definindo o DPI manualmente](#Definindo_o_DPI_manualmente)
            *   [5.3.1.1 Driver proprietário NVIDIA](#Driver_proprietário_NVIDIA)
            *   [5.3.1.2 Correção manual do DPI](#Correção_manual_do_DPI)
    *   [5.4 Gerenciamento de energia do monitor](#Gerenciamento_de_energia_do_monitor)
*   [6 Composição](#Composição)
    *   [6.1 Lista de gerenciadores de composição](#Lista_de_gerenciadores_de_composição)
*   [7 Dicas e truques](#Dicas_e_truques)
    *   [7.1 Automação](#Automação)
    *   [7.2 Sessão X aninhada](#Sessão_X_aninhada)
    *   [7.3 Iniciando programas GUI remotamente](#Iniciando_programas_GUI_remotamente)
    *   [7.4 Habilitando e desabilitando em demanda dispositivos de entrada](#Habilitando_e_desabilitando_em_demanda_dispositivos_de_entrada)
    *   [7.5 Atalho para matar um programa](#Atalho_para_matar_um_programa)
    *   [7.6 Impeça acesso ao TTY](#Impeça_acesso_ao_TTY)
    *   [7.7 Impeça um usuário de matar o X](#Impeça_um_usuário_de_matar_o_X)
*   [8 Solução de problemas](#Solução_de_problemas)
    *   [8.1 Geral](#Geral)
    *   [8.2 Tela preta, nenhum protocolo especificado.., recurso temporariamente não disponível para todos ou alguns usuários](#Tela_preta,_nenhum_protocolo_especificado..,_recurso_temporariamente_não_disponível_para_todos_ou_alguns_usuários)
    *   [8.3 DRI com placas Matrox parou de funcionar](#DRI_com_placas_Matrox_parou_de_funcionar)
    *   [8.4 Problemas no modo renderizador de quadros (framebuffer mode)](#Problemas_no_modo_renderizador_de_quadros_(framebuffer_mode))
    *   [8.5 Programa requer "font '(null)'"](#Programa_requer_"font_'(null)'")
    *   [8.6 Recuperação: Desabilitar o Xorg antes do login GUI](#Recuperação:_Desabilitar_o_Xorg_antes_do_login_GUI)
    *   [8.7 Cliente X começando com falha "su"](#Cliente_X_começando_com_falha_"su")
    *   [8.8 X falhou para iniciar: Inicialização do teclado falhou](#X_falhou_para_iniciar:_Inicialização_do_teclado_falhou)
    *   [8.9 Xorg sem superusuário](#Xorg_sem_superusuário)
        *   [8.9.1 Redirecionamento quebrado](#Redirecionamento_quebrado)
    *   [8.10 Tela verde toda vez que tenta ver um vídeo](#Tela_verde_toda_vez_que_tenta_ver_um_vídeo)
    *   [8.11 Erro SocketCreateListener](#Erro_SocketCreateListener)
    *   [8.12 Chave inválida MIT-MAGIC-COOKIE-1 enquanto tenta executar um programa como root](#Chave_inválida_MIT-MAGIC-COOKIE-1_enquanto_tenta_executar_um_programa_como_root)
    *   [8.13 Xorg-server Fatal server error: (EE) AddScreen/ScreenInit](#Xorg-server_Fatal_server_error:_(EE)_AddScreen/ScreenInit)
*   [9 Veja também](#Veja_também)

## Instalação

Xorg pode ser [instalado](/index.php/Instala "Instala") com o pacote [xorg-server](https://www.archlinux.org/packages/?name=xorg-server).

Alguns pacotes do grupo [xorg-apps](https://www.archlinux.org/groups/x86_64/xorg-apps/) são necessários para certas tarefas de configuração, eles serão destacados nas seções relevantes.

O grupo [xorg](https://www.archlinux.org/groups/x86_64/xorg/) também é uma opção, ele oferece pacotes do servidor Xorg, pacotes do grupo [xorg-apps](https://www.archlinux.org/groups/x86_64/xorg-apps/) e fontes.

**Dica:** Você irá normalmente instalar um [gerenciador de janelas](/index.php/Gerenciador_de_janela "Gerenciador de janela") ou um [ambiente desktop](/index.php/Ambientes_de_desktop "Ambientes de desktop") para suplementar o X.

### Instalação de driver

O kernel Linux inclui drivers de vídeo de código aberto e suporta aceleração de hardware para framebuffers. No entanto, é necessário suporte para OpenGL e aceleração 2D no X11.

Primeiro, identifique sua placa:

```
$ lspci | grep -e VGA -e 3D

```

Então, instale o driver apropriado. Você pode procurar por uma lista completa de drivers de vídeo com:

```
$ pacman -Ss xf86-video

```

Xorg procura por drivers de vídeo instalados automaticamente:

*   Se ele não achar o driver específico instalado (listados abaixo), ele primeiro procura por *fbdev* ([xf86-video-fbdev](https://www.archlinux.org/packages/?name=xf86-video-fbdev)).
*   Se não for achado, ele procura por *vesa* ([xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa)), o driver genérico, que manuseia um grande número de chipsets mas não inclui nenhuma aceleração 2D e 3D.
*   Se *vesa* não é encontrado, Xorg irá fazer uso do [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"), que inclui aceleração GLAMOR (veja [modesetting(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/modesetting.4)).

Para aceleração de vídeo funcionar, e geralmente para usar todos os modos configuráveis da GPU, é necessário o driver apropriado:

| Marca | Tipo | Driver | OpenGL | OpenGL ([multilib](/index.php/Multilib_(Portugu%C3%AAs) "Multilib (Português)")) | Documentação |
| AMD / ATI | Código aberto | [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [AMDGPU](/index.php/AMDGPU "AMDGPU") |
| [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [ATI](/index.php/ATI "ATI") |
| Intel | Código aberto | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Gráficos Intel](/index.php/Gr%C3%A1ficos_Intel "Gráficos Intel") |
| NVIDIA | Código aberto | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Nouveau](/index.php/Nouveau "Nouveau") |
| Proprietário | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) | [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) | [NVIDIA](/index.php/NVIDIA "NVIDIA") |
| [nvidia-390xx](https://www.archlinux.org/packages/?name=nvidia-390xx) | [nvidia-390xx-utils](https://www.archlinux.org/packages/?name=nvidia-390xx-utils) | [lib32-nvidia-390xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-390xx-utils) |

**Nota:**

*   Para habilitar NVIDIA Optimus que usa uma placa de vídeo integrada com uma placa GPU dedicada, Veja [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus").
*   Para gráficos Intel da quarta geração e maior, veja [Gráficos Intel#Instalação](/index.php/Gr%C3%A1ficos_Intel#Instalação "Gráficos Intel") para drivers disponíveis.

Outros drivers de vídeo podem ser encontrados no grupo [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/).

Xorg deve rodar suavemente sem drivers de código fechado, que são tipicamente necessários somente para características avançadas como rápida renderização 3D para jogos. As exceções para esta regra são GPUs recentes (especialmente GPUs da NVIDIA), que não são suportadas por drivers de código aberto.

### AMD

| Arquitetura da GPU | Placas Radeon | Driver de código aberto | Driver proprietário |
| GCN 4
e recentes | [vários](https://en.wikipedia.org/wiki/List_of_AMD_graphics_processing_units "wikipedia:List of AMD graphics processing units") | [AMDGPU](/index.php/AMDGPU "AMDGPU") | [AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") |
| GCN 3 | [AMDGPU](/index.php/AMDGPU "AMDGPU") | [Catalyst](/index.php/Catalyst "Catalyst") /
[AMDGPU PRO](/index.php/AMDGPU_PRO "AMDGPU PRO") |
| GCN 2 | [AMDGPU](/index.php/AMDGPU "AMDGPU")* / [ATI](/index.php/ATI "ATI") | [Catalyst](/index.php/Catalyst "Catalyst") |
| GCN 1 | [AMDGPU](/index.php/AMDGPU "AMDGPU")* / [ATI](/index.php/ATI "ATI") | [Catalyst](/index.php/Catalyst "Catalyst") |
| TeraScale 2&3 | HD 5000 - HD 6000 | [ATI](/index.php/ATI "ATI") | [Catalyst](/index.php/Catalyst "Catalyst") |
| TeraScale 1 | HD 2000 - HD 4000 | antigo [Catalyst](/index.php/Catalyst "Catalyst") |
| Mais antigo | X1000 e antigo | *não disponível* |

	*: Experimental

## Iniciando

O comando [Xorg(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xorg.1) não é normalmente iniciado diretamente, ao invés disso o servidor X é iniciado por um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição") ou [xinit](/index.php/Xinit_(Portugu%C3%AAs) "Xinit (Português)").

## Configuração

**Nota:** Arch supre os arquivos de configuração padrão em `/usr/share/X11/xorg.conf.d/`, nenhuma configuração extra é necessária para a maioria dos casos.

Xorg usa o arquivo de configuração `xorg.conf` e arquivos terminando com o sufixo `.conf` para sua inicialização: a lista completa das pastas onde estes arquivos são procurados podem ser encontrados em [xorg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5), juntamente com explicações detalhadas de todas as opções disponíveis.

### Usando arquivos .conf

O diretório `/etc/X11/xorg.conf.d/` guarda configurações específicas do usuário. Você é livre para adicionar arquivos de configuração, mas eles deve ter o sufixo `.conf`: os arquivos são lidos na ordem ASCII, e por convenção seus nomes começam com `*XX*-` (dois dígitos e um hífen, e por exemplo, 10 é lido antes de 20). Estes arquivos são analisados pelo servidor X e são tratados como parte do arquivo de configuração tradicional `xorg.conf`. Note que em caso de configuração conflitante, o arquivo lido por *último* será processado. Por esta razão os arquivos de configuração genéricos devem ser ordenados primeiro por nome. As configurações no arquivo `xorg.conf` são processadas no final.

Para opções de configuração, veja também a página da [wiki do Fedora](https://fedoraproject.org/wiki/Input_device_configuration#xorg.conf.d).

### Usando xorg.conf

Xorg pode ser configurado modificando `/etc/X11/xorg.conf` ou `/etc/xorg.conf`. Você também pode gerar um esqueleto do para `xorg.conf` com:

```
# Xorg :0 -configure

```

Isto deve criar um arquivo `xorg.conf.new` em `/root/` que você pode copiar para `/etc/X11/xorg.conf`.

**Dica:** Se você já está rodando um servidor X, use uma exibição *(display)* diferente. Por exemplo, `Xorg :2 -configure`.

Alternativamente, seu driver proprietário pode vir com uma ferramenta para automaticamente configurar o Xorg: veja o artigo do seu driver de vídeo, [NVIDIA](/index.php/NVIDIA "NVIDIA") ou [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst"), para mais detalhes.

**Nota:** Palavras-chave de arquivo de configuração não diferenciam maiúsculas/minúsculas, e caracteres "_" são ignorados. A maioria das palavras (incluindo nomes de opções) também não diferenciam maiúsculas/minúsculas, o mesmo acontece com os caracteres de espaço e "_".

## Dispositivos de entrada

Para dispositivos de entrada o servidor X usa o driver libinput ([xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput)), mas [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) e drivers relacionados estão disponíveis como alternativa.[[1]](https://www.archlinux.org/news/xorg-server-1191-is-now-in-extra/)

[Udev](/index.php/Udev "Udev"), oferecido como dependência do systemd, irá detectar o hardware e ambos os drivers irão agir dinamicamente como driver de entrada para quase todos dispositivos, como definido nos arquivos de configuração padrão `10-quirks.conf` e `40-libinput.conf` no diretório `/usr/share/X11/xorg.conf.d/`.

Depois de iniciar o servidor X, o arquivo de log irá mostrar que driver foi selecionado para dado dispositivo (note que o nome do arquivo de log mais recente pode variar):

```
$ grep -e "Using input driver " Xorg.0.log

```

Se ambos não suportam um dispositivo particular, instale o driver necessário do grupo [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/). O mesmo se aplica, se você quiser usar outro driver.

Para influenciar a troca dinâmica entre os drivers, Veja [#Configuração](#Configuração).

Para instruções específicas, veja também o artigo [libinput](/index.php/Libinput "Libinput"), as seguintes páginas abaixo, ou a [wiki do Fedora](https://fedoraproject.org/wiki/Input_device_configuration) para mais exemplos.

### Identificação de entrada

Veja [Keyboard input#Identifying keycodes in Xorg](/index.php/Keyboard_input#Identifying_keycodes_in_Xorg "Keyboard input").

### Aceleração do mouse

Veja [Mouse acceleration](/index.php/Mouse_acceleration "Mouse acceleration").

### Botões adicionais do mouse

Veja [Mouse buttons](/index.php/Mouse_buttons "Mouse buttons").

### Touchpad

Veja [libinput](/index.php/Libinput "Libinput") or [Synaptics](/index.php/Synaptics "Synaptics").

### Toque de tela

Veja [Touchscreen](/index.php/Touchscreen "Touchscreen").

### Configurações do teclado

Veja [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg").

## Configurações do monitor

### Configuração manual

**Nota:**

*   Novas versões do Xorg são automaticamente configuráveis, então configurações manuais não devem ser necessárias.
*   Se Xorg não é capaz de detectar qualquer monitor ou para evitar automaticamente configuração, um arquivo de configuração pode ser usado. Um exemplo de uso, é em um servidor, que liga sem um monitor e inicia o Xorg automaticamente, com [console virtual](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console") no [login](/index.php/Xinit_(Portugu%C3%AAs)#Inicializar_automaticamente_o_X_no_login "Xinit (Português)"), ou por um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição")

Para configuração headless o driver [xf86-video-dummy](https://www.archlinux.org/packages/?name=xf86-video-dummy) é necessário; [instale](/index.php/Instale "Instale") e crie um arquivo de configuração, como o seguinte:

 `/etc/X11/xorg.conf.d/10-headless.conf` 
```
Section "Monitor"
        Identifier "dummy_monitor"
        HorizSync 28.0-80.0
        VertRefresh 48.0-75.0
        Modeline "1920x1080" 172.80 1920 2040 2248 2576 1080 1081 1084 1118
EndSection

Section "Device"
        Identifier "dummy_card"
        VideoRam 256000
        Driver "dummy"
EndSection

Section "Screen"
        Identifier "dummy_screen"
        Device "dummy_card"
        Monitor "dummy_monitor"
        SubSection "Display"
        EndSubSection
EndSection

```

### Múltiplos monitores

Veja o artigo [Múltiplos monitores](/index.php/Multihead "Multihead") para informações gerais.

Veja também as instruções específicas da GPU:

*   [NVIDIA#Múltiplos monitores](/index.php/NVIDIA#Multiple_monitors "NVIDIA")
*   [Nouveau#Dois monitores](/index.php/Nouveau#Dual_head "Nouveau")
*   [AMD Catalyst#Duas telas (Dois monitores / Duas telas / Xinerama)](/index.php/AMD_Catalyst#Double_Screen_(Dual_Head_/_Dual_Screen_/_Xinerama) "AMD Catalyst")
*   [ATI#Configuração múltiplos monitores](/index.php/ATI#Multihead_setup "ATI")

#### Mais de uma placa de vídeo

Você deve definir o driver correto a ser usado e botar o bus ID de sua placa de vídeo.

```
Section "Device"
    Identifier             "Screen0"
    Driver                 "nouveau"
    BusID                  "PCI:0:12:0"
EndSection

Section "Device"
    Identifier             "Screen1"
    Driver                 "radeon"
    BusID                  "PCI:1:0:0"
EndSection

```

Para descobrir o bus ID você pode executar:

 `$ lspci | grep VGA` 
```
01:00.0 VGA compatible controller: nVidia Corporation G96 [GeForce 9600M GT] (rev a1)

```

O bus ID desse exemplo é 1:0:0.

### Tamanho da tela e DPI

O DPI do servidor X é determinado da seguinte maneira:

1.  A opção da linha de comando `-dpi` tem a maior prioridade.
2.  Se ela não é usada, a configuração `DisplaySize` no arquivo de configuração do X é usada para entregar o DPI, dado o tamanho de resolução da tela.
3.  Se nenhum `DisplaySize` é dado, os valores de tamanho do monitor da [DDC](https://en.wikipedia.org/wiki/Display_Data_Channel "wikipedia:Display Data Channel") são usados para definir o DPI, dado a resolução de tela.
4.  Se DDC não especifica um tamanho, é usado por padrão 75 DPI.

Para conseguir pontos por polegada (DPI) correto, o tamanho da tela deve ser reconhecido ou configurado. Ter o DPI correto é um requisito quando detalhes finos são necessários (como renderização de fontes). Antigamente, fabricantes tentaram criar um padrão para 96 DPI (um monitor de 10.3" deveria ser 800X600, um monitor de 13.2" deveria ser 1024X768). Atualmente, DPIs variam e podem não ser iguais horizontalmente e verticalmente. Por exemplo, uma tela panorâmica LCD de 19" 1440X900 poderia ter um DPI de 89X87\. Para configurar o DPI, o servidor Xorg tenta a auto detecção do tamanho de tela físico através da placa gráfica com DDC. ~~Quando o servidor Xorg sabe o tamanho físico da tela, ele será capaz de configurar o DPI corretamente baseado no tamanho da resolução.~~

Para ver se o tamanho da sua tela e DPI são detectados/calculados corretamente:

```
$ xdpyinfo | grep -B2 resolution

```

Verifique se as dimensões correspondem ao tamanho da sua tela. Se o servidor Xorg não é capaz de corretamente calcular o tamanho de tela, o DPI será definido como 75X75 e você terá que calcular isto você mesmo.

Se você tem especificações do tamanho físico da tela, pode colocá-los no arquivo de configuração do Xorg para então o DPI apropriado ser calculado (ajuste o *Identifier* de acordo com a saída do `xrandr`):

```
Section "Monitor"
    Identifier             "DVI-D-0"
    DisplaySize             286 179    # Em milímetros
EndSection

```

Se você somente quer colocar sua especificação de monitor **sem** criar um novo arquivo xorg.conf. Por exemplo (`/etc/X11/xorg.conf.d/90-monitor.conf`):

```
Section "Monitor"
    Identifier             "<monitor padrão>"
    DisplaySize            286 179    # Em milímetros
EndSection

```

Se você não tem as especificações físicas de altura e largura da tela, (a maioria das especificações atualmente somente listam o tamanho diagonal) você pode usar a nativa resolução do monitor (ou aspecto de proporção) e comprimento diagonal para calcular a dimensão horizontal e vertical física. Usando o Teorema de Pitágoras em uma tela diagonal de 13.3" com uma resolução nativa de 1280X800 (ou aspecto de proporção 16:10):

```
$ echo 'scale=5;sqrt(1280^2+800^2)' | bc  # 1509.43698

```

Isto dará o comprimento do pixel diagonal e com este valor você pode descobrir o comprimento horizontal e vertical físico (e converter eles para milímetros):

```
$ echo 'scale=5;(13.3/1509)*1280*25.4' | bc  # 286.43072
$ echo 'scale=5;(13.3/1509)*800*25.4'  | bc  # 179.01920

```

**Nota:** Este cálculo funciona para monitores com pixels quadrados; no entanto, raramente um monitor pode comprimir o aspecto de proporção (exemplo aspecto de resolução 16:10 para um 16:9). Se este for o caso, você deve mensurar o tamanho de sua tela manualmente.

#### Definindo o DPI manualmente

**Nota:** Embora você possa definir qualquer dpi que desejar e os aplicativos que usam Qt e GTK serão redimensionados de acordo, é recomendável defini-lo como 96, 120 (25% a mais), 144 (50% a mais), 168 (75% a mais), 192 (100% a mais) etc., para reduzir dimensionamento de artefatos à GUI que usam bitmaps. Reduzi-lo abaixo de 96 dpi pode não reduzir o tamanho dos elementos gráficos da GUI, pois normalmente o dpi mais baixo para o qual os ícones são criados é 96.

Para drivers compatíveis com RandR (por exemplo, o driver ATI de código aberto), você pode configurá-lo da seguinte maneira:

```
$ xrandr --dpi 144

```

**Nota:** Os aplicativos que estão em conformidade com a configuração não serão alterados imediatamente. Você precisa iniciá-los novamente.

Para torná-lo permanente, consulte [Inicialização automática#Na inicialização de Xorg](/index.php/Inicializa%C3%A7%C3%A3o_autom%C3%A1tica#Na_inicialização_de_Xorg "Inicialização automática").

##### Driver proprietário NVIDIA

O DPI pode ser configurado manualmente se você deseja usar somente uma resolução ([calculadora de DPI](https://www.pxcalc.com/)):

```
Section "Monitor"
    Identifier             "Monitor0"
    Option                 "DPI" "96 x 96"
EndSection

```

Você pode configurar manualmente o DPI adicionando as opções abaixo no arquivo `/etc/X11/xorg.conf.d/20-nvidia.conf` (dentro da seção **Device**):

```
Option              "UseEdidDpi" "False"
Option              "DPI" "96 x 96"

```

##### Correção manual do DPI

GTK frequentemente sobrescreve o DPI do servidor com o Xresource opcional `Xft.dpi`. Para descobrir se isto está acontecendo com você, verifique:

```
$ xrdb -query | grep dpi

```

A partir da versão 3.16 do GTK quando esta variável não é explicitamente definida, GTK define como 96\. Para os programas GTK obedecerem o DPI do servidor você deve explicitamente definir Xft.dpi. O recurso Xft.dpi é o metodo pelo qual alguns ambientes desktop opcionalmente forçam o DPI para um valor específico. Dentre estes [KDE](/index.php/KDE_(Portugu%C3%AAs) "KDE (Português)") e [TDE](/index.php/TDE "TDE").

### Gerenciamento de energia do monitor

[DPMS](/index.php/DPMS "DPMS") (Gerenciamento de energia do monitor baseado em sinalização) é uma tecnologia que habilita o modo de economia de energia para monitores quando o computador não está em uso. Isto permite que os monitores vão para o modo standby automaticamente depois de determinado período de tempo.

## Composição

A extensão de Composição para X gera uma completa subárvore hierárquica de janelas a serem renderizadas para um buffer off-screen (renderização fora da tela). Programas então pegam o conteúdo desse buffer e fazem o que quiser com ele. O buffer off-screen pode ser automaticamente fundido com a janela pai ou com programas externos, chamados gerenciadores de composição. Veja o seguinte artigo para mais informações: [gerenciador de janelas compositor](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager")

Alguns gerenciadores de janela (por exemplo: [compiz](/index.php/Compiz "Compiz"), [Enlightenment](/index.php/Enlightenment "Enlightenment"), KWin, Marco, Metacity, Muffin, Mutter, [Xfwm](/index.php/Xfwm "Xfwm")) fazem composição. Para outros gerenciadores de janela, um gerenciador de composição pode ser usado.

### Lista de gerenciadores de composição

*   **[Picom](/index.php/Picom "Picom")** — Compositor (um fork do Compton)

	[https://github.com/yshui/picom](https://github.com/yshui/picom) || [picom](https://www.archlinux.org/packages/?name=picom)

*   **[Xcompmgr](/index.php/Xcompmgr "Xcompmgr")** — Gerenciador de efeitos de janela de composição

	[https://cgit.freedesktop.org/xorg/app/xcompmgr/](https://cgit.freedesktop.org/xorg/app/xcompmgr/) || [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr)

*   **Unagi** — Um modular gerenciador de composição escrito em C baseado no XCB

	[https://projects.mini-dweeb.org/projects/unagi](https://projects.mini-dweeb.org/projects/unagi) || [unagi](https://aur.archlinux.org/packages/unagi/)

## Dicas e truques

### Automação

Esta seção lista utilitários para automatizar a entrada do teclado ou mouse e operações de janela (como mover, redimensionar e iniciar).

| Ferramenta | Pacote | Manual | Entrada
[Keysym](/index.php/Keysym "Keysym") | Operações de
janela | Nota |
| xautomation | [xautomation](https://www.archlinux.org/packages/?name=xautomation) | [xte(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xte.1) | Sim | Não | Também contém ferramentas de [screen scraping](https://en.wikipedia.org/wiki/pt:Raspagem_de_dados#Screen_scraping "wikipedia:pt:Raspagem de dados"). Não pode simular F13+. |
| xdo | [xdo-git](https://aur.archlinux.org/packages/xdo-git/) | [xdo(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdo.1) | Não | Sim | Pequena ferramenta do X para ações elementárias em janelas. |
| xdotool | [xdotool](https://www.archlinux.org/packages/?name=xdotool) | [xdotool(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdotool.1) | Sim | Sim | [Muitos bugs](https://github.com/jordansissel/xdotool/issues) e não está em desenvolvimento ativo, exemplo: tem parseamento da linha de comando quebrado.[[2]](https://github.com/jordansissel/xdotool/issues/14#issuecomment-327968132)[[3]](https://github.com/jordansissel/xdotool/issues/71) |
| xvkbd | [xvkbd](https://aur.archlinux.org/packages/xvkbd/) | [xvkbd(1)](http://t-sato.in.coocan.jp/xvkbd/#option) | Sim | Não | Teclado virtual para Xorg, também tem a opção `-text` para envio de caracteres. |

Veja também [Clipboard#Tools](/index.php/Clipboard#Tools "Clipboard") e [uma visão geral de ferramentas de automação do X](https://venam.nixers.net/blog/unix/2019/01/07/win-automation.html) (em inglês).

### Sessão X aninhada

Para executar uma sessão aninhada de outro ambiente de desktop:

```
$ /usr/bin/Xnest :1 -geometry 1024x768+0+0 -ac -name Windowmaker & wmaker -display :1

```

Isso vai iniciar uma sessão de Window Maker em uma janela 1024 por 768 dentro de sua sessão X atual.

Isso precisa do pacote [xorg-server-xnest](https://www.archlinux.org/packages/?name=xorg-server-xnest) para ser instalado.

### Iniciando programas GUI remotamente

Veja o artigo principal: [OpenSSH#X11 forwarding](/index.php/OpenSSH#X11_forwarding "OpenSSH").

### Habilitando e desabilitando em demanda dispositivos de entrada

Com a ajuda de *xinput* você pode temporariamente desabilitar ou habilitar dispositivos de entrada. Isto pode ser útil, por exemplo, em sistemas que tem mais de um mouse, como os ThinkPads, e você prefere usar somente um para evitar clicks indesejados.

[Instale](/index.php/Instale "Instale") o pacote [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput).

Encontre o nome ou ID do dispositivo que você quer desabilitar:

```
$ xinput

```

Por exemplo, em um Lenovo ThinkPad T500, a saída parece com isto:

 `$ xinput` 
```
⎡ Virtual core pointer                          id=2    [master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer                id=4    [slave  pointer  (2)]
⎜   ↳ TPPS/2 IBM TrackPoint                     id=11   [slave  pointer  (2)]
⎜   ↳ SynPS/2 Synaptics TouchPad                id=10   [slave  pointer  (2)]
⎣ Virtual core keyboard                         id=3    [master keyboard (2)]
    ↳ Virtual core XTEST keyboard               id=5    [slave  keyboard (3)]
    ↳ Power Button                              id=6    [slave  keyboard (3)]
    ↳ Video Bus                                 id=7    [slave  keyboard (3)]
    ↳ Sleep Button                              id=8    [slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard              id=9    [slave  keyboard (3)]
    ↳ ThinkPad Extra Buttons                    id=12   [slave  keyboard (3)]

```

Desabilite o dispositivo com `xinput --disable *dispositivo*`, onde o *dispositivo* é o ID ou nome do dispositivo que você quer desabilitar. Neste exemplo nós iremos desabilitar o *Synaptics Touchpad*, com o ID 10:

```
$ xinput --disable 10

```

Para habilitar novamente o dispositivo, execute o comando:

```
$ xinput --enable 10

```

Alternatively using the device name, the command to disable the touchpad would be:

Alternativamente, usando o nome do dispositivo, o comando para desabilitar o touchpad seria:

```
$ xinput --disable "SynPS/2 Synaptics TouchPad"

```

### Atalho para matar um programa

Faça um atalho com o seguinte script:

```
#!/bin/bash
windowFocus=$(xdotool getwindowfocus);
pid=$(xprop -id $windowFocus | grep PID);
kill -9 $pid

```

Dependências: [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop), [xdotool](https://www.archlinux.org/packages/?name=xdotool).

### Impeça acesso ao TTY

Para impedir o acesso ao TTY no X, adicione no [xorg.conf](#Configuração):

```
Section "ServerFlags"
    Option "DontVTSwitch" "True"
EndSection

```

### Impeça um usuário de matar o X

Para prevenir um usuário de matar uma sessão X quando ela está rodando, adicione o seguinte no [xorg.conf](#Configuração):

```
Section "ServerFlags"
    Option "DontZap"      "True"
EndSection

```

## Solução de problemas

### Geral

Se um problema acontecer, veja o log armazenado em `/var/log/` ou, se executa o servidor X como usuário comum (possível desde v1.16), em `~/.local/share/xorg/`. Usuários do [GDM](/index.php/GDM_(Portugu%C3%AAs) "GDM (Português)") devem verificar os [registros do systemd](/index.php/Systemd_(Portugu%C3%AAs)/Journal_(Portugu%C3%AAs) "Systemd (Português)/Journal (Português)"). [[4]](https://bbs.archlinux.org/viewtopic.php?id=184639)

Os arquivos de log estão na forma de `Xorg.n.log` com `n` sendo o número de exibição(`$DISPLAY`). Para uma maquina de único usuário com configuração padrão, o arquivo de log é frequentemente `Xorg.0.log`, mas isto pode variar. Para ter certeza de qual é o arquivo certo você pode olhar o log da inicialização da sessão X e de qual console ele foi iniciado. Por exemplo:

 `$ grep -e Log -e tty Xorg.0.log` 
```
[    40.623] (==) Log file: "/home/archuser/.local/share/xorg/Xorg.0.log", Time: Thu Aug 28 12:36:44 2014
[    40.704] (--) controlling tty is VT number 1, auto-enabling KeepTty
```

*   No arquivo de log você pode procurar por qualquer linhas começando com `(EE)`, que representam erros, e também `(WW)`, que são avisos que podem indicar outros problemas.
*   Se o arquivo `xinitrc` estiver *vazio* em seu `$HOME`, exclua ou edite ele para o X iniciar apropriadamente. Se você não fizer isto X irá mostrar uma tela vazio sem erros aparentes no seu `Xorg.0.log`. Ao exclui-lo a próxima vez que for iniciado o X será executado com o ambiente X padrão.
*   Se a tela ficar preta, você pode ainda tentar trocar para um diferente console virtual (por exemplo, `Ctrl+Alt+F6`), e entrar como root. Você pode fazer isto ao digitar `root` (pressionando `Enter` depois) e entrar com a senha do usuário root (denovo, pressione `Enter` depois).

	Você pode querer matar o servidor X com:

	 `# pkill -x X` 

	Se isto não funcionar, pode reiniciar cegamente com:

	 `# reboot` 

*   Veja páginas específicas na [Categoria:Dispositivos de entrada](/index.php/Category:Input_devices_(Portugu%C3%AAs) "Category:Input devices (Português)") se você tiver problemas com o teclado, mouse, Touchpad e etc, considere verificar a pagina em [inglês](/index.php/Category:Input_devices "Category:Input devices") se não achar o que procura.
*   Procure por problemas comuns nos artigos da [ATI](/index.php/ATI "ATI"), [Intel](/index.php/Intel "Intel") e [NVIDIA](/index.php/NVIDIA "NVIDIA").

### Tela preta, nenhum protocolo especificado.., recurso temporariamente não disponível para todos ou alguns usuários

X cria configuração e arquivos temporários no diretório do usuário ($HOME). Tenha certeza que existe espaço de disco disponível na partição utilizada. Infelizmente, o servidor X não informa isso de maneira óbvia.

### DRI com placas Matrox parou de funcionar

Se você usa um cartão Matrox e DRI parou de funcionar depois de atualizar o Xorg, tente adicionar a seguinte linha:

```
Option "OldDmaInit" "On"

```

Na seção `Device` que referência a placa de vídeo em `xorg.conf`.

### Problemas no modo renderizador de quadros (framebuffer mode)

Se X falha para iniciar com a seguinte messagem de log:

```
(WW) Falling back to old probe method for fbdev
(II) Loading sub module "fbdevhw"
(II) LoadModule: "fbdevhw"
(II) Loading /usr/lib/xorg/modules/linux//libfbdevhw.so
(II) Module fbdevhw: vendor="X.Org Foundation"
       compiled for 1.6.1, module version=0.0.2
       ABI class: X.Org Video Driver, version 5.0
(II) FBDEV(1): using default device

Fatal server error:
Cannot run in framebuffer mode. Please specify busIDs for all framebuffer devices

```

[Desinstale](/index.php/Pacman_(Portugu%C3%AAs)#Removendo_pacotes "Pacman (Português)") o pacote [xf86-video-fbdev](https://www.archlinux.org/packages/?name=xf86-video-fbdev).

### Programa requer "font '(null)'"

Messagem de erro: `unable to load font `(null)'`.

Alguns programas somente funcionam com fontes bitmap. Os dois maiores pacotes com fontes bipmap disponíveis são [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) e [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi). Você não precisa de ambos, um deve ser o bastante. Para descobrir qual o mais apropriado para sua situação, tente `xdpyinfo`, do pacote [xorg-xdpyinfo](https://www.archlinux.org/packages/?name=xorg-xdpyinfo), desse jeito:

```
$ xdpyinfo | grep resolution

```

Use o que for mais próximo do valor mostrado.

### Recuperação: Desabilitar o Xorg antes do login GUI

Se o Xorg está configurado para iniciar automaticamente e por alguma razão você precisa evitar isto antes de iniciar o login/gerenciador de exibição Aparecerem (e o sistema está mal configurado e o Xorg não reconhece o mouse ou teclado, por exemplo), você pode fazer isto com dois métodos.

*   Mude o alvo padrão para rescue.target. Veja [Systemd#Alterar target padrão para inicializar](/index.php/Systemd_(Portugu%C3%AAs)#Alterar_target_padrão_para_inicializar "Systemd (Português)").
*   Se você além de ter um sistema com falhas que fazem o Xorg não usável, tem o menu do GRUB sem tempo de espera, e não pode usar o GRUB para prevenir o Xorg de iniciar. Você pode usar um live CD do Arch Linux. Veja no [guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação") sobre como montar e chroot o sistema Arch Linux instalado.Você também pode tentar trocar para outro [tty](/index.php/Tty "Tty") com `Ctrl+Alt` + a tecla de função (normalmente do `F1` para `F7`, use um que não está sendo usado pelo X), logue como root e siga os passos abaixo.

Dependendo da configuração, você vai precisar fazer um ou mais desses passos:

*   [Desabilite](/index.php/Desabilite "Desabilite") o [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição").
*   Desabilite o [Inicio automático do X no login](/index.php/Xinit_(Portugu%C3%AAs)#Inicializar_automaticamente_o_X_no_login "Xinit (Português)").
*   Renomeie o `~/.xinitrc` ou comente a linha que contém `exec` dentro dele.

### Cliente X começando com falha "su"

Se você está ecebendo "Client is not authorized to connect to server", tente adicionar essa linha:

```
session        optional        pam_xauth.so

```

Em `/etc/pam.d/su` e `/etc/pam.d/su-l`. `pam_xauth` irá então apropriadamente definir as variáveis de ambiente e cuidar das chaves `xauth`.

### X falhou para iniciar: Inicialização do teclado falhou

Se o sistema de arquivos, especificamente se `/tmp` está cheio, `startx` irá falhar. `/var/log/Xorg.0.log` irá terminar com:

```
(EE) Error compiling keymap (server-0)
(EE) XKB: Could not compile keymap
(EE) XKB: Failed to load keymap. Loading default keymap instead.
(EE) Error compiling keymap (server-0)
(EE) XKB: Could not compile keymap
XKB: Failed to compile keymap
Keyboard initialization failed. This could be a missing or incorrect setup of xkeyboard-config.
Fatal server error:
Failed to activate core devices.
Please consult the The X.Org Foundation support at http://wiki.x.org
for help.
Please also check the log file at "/var/log/Xorg.0.log" for additional information.
(II) AIGLX: Suspending AIGLX clients for VT switch

```

Libere espaço no sistema de arquivos e X irá iniciar.

### Xorg sem superusuário

Xorg pode rodar sem a necessidade de privilégios especiais com a ajuda de [systemd-logind(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-logind.8), veja [[5]](https://fedoraproject.org/wiki/Changes/XorgWithoutRootRights) e [FS#41257](https://bugs.archlinux.org/task/41257). Para isso é necessário:

*   Iniciar o X via [xinit](/index.php/Xinit_(Portugu%C3%AAs) "Xinit (Português)"); gerenciadores de exibição não são suportados.
*   [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"); implementações em drivers proprietários falham na [autodetecção](https://cgit.freedesktop.org/xorg/xserver/tree/hw/xfree86/xorg-wrapper.c#n222), e é necessário definir `needs_root_rights = no` em `/etc/X11/Xwrapper.config`.

Se não for possível, habilite novamente o uso de poderes de superusuário em `/etc/X11/Xwrapper.config`:

 `/etc/X11/Xwrapper.config`  `needs_root_rights = *yes*` 

Veja também [Xorg.wrap(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xorg.wrap.1) e [Xorg como um serviço de usuário do systemd](/index.php/Systemd/User#Xorg_as_a_systemd_user_service "Systemd/User") (inglês).

[GDM](/index.php/GDM_(Portugu%C3%AAs) "GDM (Português)") também roda o Xorg sem poderes de superusuário por padrão quando [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") é usado.

#### Redirecionamento quebrado

Enquanto os logs do xorg quando executado com o usuário são armazenados em `~/.local/share/xorg/Xorg.log`, eles não incluem a saída da sessão X. Para habilitar o redirecionamento, inicie o X com a opção `-keeptty`:

```
exec startx -- -keeptty > ~/.xorg.log 2>&1

```

Ou copie `/etc/X11/xinit/xserverrc` para `~/.xserverrc`, e adicione `-keeptty`. Veja [[6]](https://bbs.archlinux.org/viewtopic.php?pid=1446402#p1446402).

### Tela verde toda vez que tenta ver um vídeo

Sua profundidade de cor está errada. Pode ser 24 ao invés de 16, por exemplo.

### Erro SocketCreateListener

Se X termina com a mensagem de erro "SocketCreateListener() failed", você pode precisar deletar os arquivos de socket em `/tmp/.X11-unix`. Isto pode acontecer se você antes tenha rodado o Xorg como superusuário (Por exemplo, para gerar uma `xorg.conf`).

### Chave inválida MIT-MAGIC-COOKIE-1 enquanto tenta executar um programa como root

Este erro significa que somente o atual usuário tem acesso ao servidor X. Para resolver, dê acesso ao superusuário:

```
$ xhost +si:localuser:root

```

Esta linha também pode dar acesso a outros usuários.

### Xorg-server Fatal server error: (EE) AddScreen/ScreenInit

Se o servidor do Xorg estiver apresentando um problema intermitente e no log do Xorg você vê:

```
systemd-logind: failed to take device /dev/dri/card0: Operation not permitted
...
AddScreen/ScreenInit failed for driver 0

```

Então este problema pode ser causado pelo [issue 13943 do systemd](https://github.com/systemd/systemd/issues/13943). Configure um [início antecipado de KMS](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting").

## Veja também

*   [Xplain](https://magcius.github.io/xplain/article/) - Explicação detalhada do sistema de janelas X.
*   [Xorg(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xorg.1) - Página manual do Xorg.
*   [Gentoo/Xorg#Configuration](https://wiki.gentoo.org/wiki/Xorg/Guide/en#Configuration) - Página de configuração do Xorg da Wiki do Gentoo.