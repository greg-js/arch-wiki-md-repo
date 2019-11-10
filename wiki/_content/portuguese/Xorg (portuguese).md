Related articles

*   [Autostarting](/index.php/Autostarting "Autostarting")
*   [Display manager](/index.php/Display_manager "Display manager")
*   [Window manager](/index.php/Window_manager "Window manager")
*   [Font configuration](/index.php/Font_configuration "Font configuration")
*   [Cursor themes](/index.php/Cursor_themes "Cursor themes")
*   [Desktop environment](/index.php/Desktop_environment "Desktop environment")
*   [Wayland](/index.php/Wayland "Wayland")
*   [xinit](/index.php/Xinit "Xinit")
*   [xrandr](/index.php/Xrandr "Xrandr")

Da [https://www.x.org/wiki/](https://www.x.org/wiki/):

	O projeto X.Org oferece uma implementação de código aberto do [Sistema de janelas X](https://en.wikipedia.org/wiki/pt:X_Window_System "wikipedia:pt:X Window System"). O desenvolvimento é realizado em conjunto com a comunidade freedesktop.org. X.org é uma corporação educacional sem fins lucrativos, liderada pelo conselho e membros do projeto.

**Xorg** (normalmente chamado de **X**) é o servidor de exibição mais popular entre os usuários do Linux. Sua onipresença lhe fez um pré-requisito para programas GUI, Isto resultou em uma massiva adoção na maioria das distribuições Linux. Veja a página do Wikipedia [Xorg](https://en.wikipedia.org/wiki/pt:X.Org_Server "wikipedia:pt:X.Org Server") ou visite o [site do Xorg](https://www.x.org/wiki/) para mais informações.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
    *   [1.1 Instalação de Driver](#Instalação_de_Driver)
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
        *   [5.3.1 Setting DPI manually](#Setting_DPI_manually)
            *   [5.3.1.1 Proprietary NVIDIA driver](#Proprietary_NVIDIA_driver)
            *   [5.3.1.2 Manual DPI Setting Caveat](#Manual_DPI_Setting_Caveat)
    *   [5.4 Display Power Management](#Display_Power_Management)
*   [6 Composite](#Composite)
    *   [6.1 List of composite managers](#List_of_composite_managers)
*   [7 Tips and tricks](#Tips_and_tricks)
    *   [7.1 Automation](#Automation)
    *   [7.2 Nested X session](#Nested_X_session)
    *   [7.3 Starting GUI programs remotely](#Starting_GUI_programs_remotely)
    *   [7.4 On-demand disabling and enabling of input sources](#On-demand_disabling_and_enabling_of_input_sources)
    *   [7.5 Killing application with hotkey](#Killing_application_with_hotkey)
    *   [7.6 Block TTY access](#Block_TTY_access)
    *   [7.7 Prevent a user from killing X](#Prevent_a_user_from_killing_X)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 General](#General)
    *   [8.2 Black screen, No protocol specified.., Resource temporarily unavailable for all or some users](#Black_screen,_No_protocol_specified..,_Resource_temporarily_unavailable_for_all_or_some_users)
    *   [8.3 DRI with Matrox cards stopped working](#DRI_with_Matrox_cards_stopped_working)
    *   [8.4 Frame-buffer mode problems](#Frame-buffer_mode_problems)
    *   [8.5 Program requests "font '(null)'"](#Program_requests_"font_'(null)'")
    *   [8.6 Recovery: disabling Xorg before GUI login](#Recovery:_disabling_Xorg_before_GUI_login)
    *   [8.7 X clients started with "su" fail](#X_clients_started_with_"su"_fail)
    *   [8.8 X failed to start: Keyboard initialization failed](#X_failed_to_start:_Keyboard_initialization_failed)
    *   [8.9 Rootless Xorg](#Rootless_Xorg)
        *   [8.9.1 Broken redirection](#Broken_redirection)
    *   [8.10 A green screen whenever trying to watch a video](#A_green_screen_whenever_trying_to_watch_a_video)
    *   [8.11 SocketCreateListener error](#SocketCreateListener_error)
    *   [8.12 Invalid MIT-MAGIC-COOKIE-1 key when trying to run a program as root](#Invalid_MIT-MAGIC-COOKIE-1_key_when_trying_to_run_a_program_as_root)
*   [9 See also](#See_also)

## Instalação

Xorg pode ser [instalado](/index.php/Instala "Instala") com o pacote [xorg-server](https://www.archlinux.org/packages/?name=xorg-server).

Alguns pacotes do grupo [xorg-apps](https://www.archlinux.org/groups/x86_64/xorg-apps/) são necessários para certas tarefas de configuração, eles serão destacados nas seções relevantes.

O grupo [xorg](https://www.archlinux.org/groups/x86_64/xorg/) também é uma opção, ele oferece pacotes do servidor Xorg, pacotes do grupo [xorg-apps](https://www.archlinux.org/groups/x86_64/xorg-apps/) e fontes.

**Dica:** Você irá normalmente instalar um [gerenciador de janelas](/index.php/Gerenciador_de_janela "Gerenciador de janela") ou um [ambiente desktop](/index.php/Ambientes_de_desktop "Ambientes de desktop") para suplementar o X.

### Instalação de Driver

O kernel Linux inclui drivers de vídeo de código aberto e suporta aceleração de hardware para framebuffers. No entanto, é necessário suporte para OpenGL e aceleração 2D no X11\. The Linux kernel includes open-source video drivers and support for hardware accelerated framebuffers. However, userland support is required for OpenGL and 2D acceleration in X11.

Primeiro, identifique sua placa:

```
$ lspci | grep -e VGA -e 3D

```

Então instale o driver apropriado. Você pode procurar por uma lista completa de drivers de vídeo com:

```
$ pacman -Ss xf86-video

```

Xorg procura por drivers de vídeo instalados automaticamente:

*   Se ele não achar o driver especifíco instalado (listados abaixo), ele primeiro procura por *fbdev* ([xf86-video-fbdev](https://www.archlinux.org/packages/?name=xf86-video-fbdev)).
*   Se não for achado, ele procura por *vesa* ([xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa)), o driver genérico, que manuseia um grande número de chipsets mas não inclui nenhuma aceleração 2D e 3D.
*   Se *vesa* não é encontrado, Xorg irá fazer uso do [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"), que inclui aceleração GLAMOR (veja [modesetting(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/modesetting.4)).

Para aceleração de vídeo funcionar, e geralmente para usar todos os modos configuráveis da GPU, é necessário o driver apropriado:

| Marca | Tipo | Driver | OpenGL | OpenGL ([multilib](/index.php/Multilib "Multilib")) | Documentação |
| AMD / ATI | Código aberto | [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [AMDGPU](/index.php/AMDGPU "AMDGPU") |
| [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [ATI](/index.php/ATI "ATI") |
| Intel | Código aberto | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Gráficos Intel](/index.php/Intel_graphics_(Portugu%C3%AAs) "Intel graphics (Português)") |
| NVIDIA | Código aberto | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [mesa](https://www.archlinux.org/packages/?name=mesa) | [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) | [Nouveau](/index.php/Nouveau "Nouveau") |
| Proprietário | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [nvidia-utils](https://www.archlinux.org/packages/?name=nvidia-utils) | [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) | [NVIDIA](/index.php/NVIDIA "NVIDIA") |
| [nvidia-390xx](https://www.archlinux.org/packages/?name=nvidia-390xx) | [nvidia-390xx-utils](https://www.archlinux.org/packages/?name=nvidia-390xx-utils) | [lib32-nvidia-390xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-390xx-utils) |

**Nota:**

*   Para habilitar NVIDIA Optimus que usa uma placa de vídeo integrada com uma placa GPU dedicada, Veja [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") ou [Bumblebee](/index.php/Bumblebee "Bumblebee").
*   Para gráficos Intel da quarta generação e maior, veja [Gráficos Intel#Instalação](/index.php/Intel_graphics_(Portugu%C3%AAs)#Instalação "Intel graphics (Português)") para drivers disponíveis.

Outros drivers de vídeo podem ser encontrados no grupo [xorg-drivers](https://www.archlinux.org/groups/x86_64/xorg-drivers/).

Xorg deve rodar suavemente sem drivers de código fechado, que são tipicamente necessários somente para características avançadas como rápida renderização 3D para jogos. As exceções para esta regra são GPUs recentes (especialmente GPUs NVIDIA), que não são suportadas por drivers de código aberto.

### AMD

| Arquitetura da GPU | Placas Radeon | driver de código aberto | driver Proprietário |
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

O comando [Xorg(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xorg.1) não é normalmente iniciado diretamente, ao invês disso o servidor X é iniciado por um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição") ou [xinit](/index.php/Xinit_(Portugu%C3%AAs) "Xinit (Português)").

## Configuração

**Nota:** Arch supre os arquivos de configuração padrão em `/usr/share/X11/xorg.conf.d/`, nenhuma configuração extra é necessária para a maioria dos casos.

Xorg usa o arquivo de configuração `xorg.conf` e arquivos terminando com o sufixo `.conf` para sua inicialização: a lista completa das pastas onde estes arquivos são procurados podem ser encontrados em [xorg.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xorg.conf.5), juntamente com explicações detalhadas de todas as opções disponíveis.

### Usando arquivos .conf

O diretório `/etc/X11/xorg.conf.d/` guarda configurações específicas do usuário. Você é livre para adiconar arquivos de configuração, mas eles deve ter o sufixo `.conf`: os arquivos são lidos na ordem ASCII, e por convenção seus nomes começam com `*XX*-` (dois digitos e um hípen, e por exemplo, 10 é lido antes de 20). Estes arquivos são parseados pelo servidor X e são tratados como parte do arquivo de configuração tradicional `xorg.conf`. Note que em caso de configuração conflitante, o arquivo lido por *último* será processado. Por esta razão os arquivos de configuração genéricos devem ser ordenados primeiro por nome. As configurações no arquivo `xorg.conf` são processadas no final.

Para opções de configuração, veja também a página da [wiki do Fedora](https://fedoraproject.org/wiki/Input_device_configuration#xorg.conf.d).

### Usando xorg.conf

Xorg pode ser configurado modificando `/etc/X11/xorg.conf` ou `/etc/xorg.conf`. Você também pode gerar um esqueleto do para `xorg.conf` com:

```
# Xorg :0 -configure

```

Isto deve criar um arquivo `xorg.conf.new` em `/root/` que você pode copiar para `/etc/X11/xorg.conf`.

**Dica:** Se você já está rodando um servidor X, use uma exibição(display) diferente, por exemplo `Xorg :2 -configure`.

Alternativamente, seu driver proprietário pode vir com uma ferramenta para automaticamente configurar o Xorg: veja o artigo do seu driver de vídeo, [NVIDIA](/index.php/NVIDIA "NVIDIA") ou [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst"), para mais detalhes.

**Nota:** palavras chave de arquivo de configuração não diferenciam maiúsculas/minúsculas, e caracteres "_" são ignorados. A maioria das palavras (incluindo nomes de opções) também não diferenciam maiúsculas/minúsculas, o mesmo acontece com os caracteres de espaço e "_".

## Dispositivos de entrada

Para dispositivos de entrada o servidor X usa o driver libinput ([xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput)), mas [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev) e drivers relacionados estão disponíveis como alternativa.[[1]](https://www.archlinux.org/news/xorg-server-1191-is-now-in-extra/)

[Udev](/index.php/Udev "Udev"), oferecido como dependência do systemd, irá detectar o hardware e ambos os drivers irão agir dinâmicamente como driver de entrada para quase todos dispositivos, como definido nos arquivos de configuração padrão `10-quirks.conf` e `40-libinput.conf` no dirétorio `/usr/share/X11/xorg.conf.d/`.

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

*   Novas versões do Xorg são auto configuráveis, então configurações manuais não devem ser necessárias.
*   Se Xorg não é capaz de detectar qualquer monitor ou para evitar auto configuração, um arquivo de configuração pode ser usado. Um exemplo de uso, é em um servidor, que liga sem um monitor e inicia o Xorg automaticamente, com [console virtual](/index.php/Automatic_login_to_virtual_console "Automatic login to virtual console") no [login](/index.php/Xinit_(Portugu%C3%AAs)#Inicializar_automaticamente_o_X_no_login "Xinit (Português)"), ou por um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição")

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
2.  se ela não é usada, a configuração `DisplaySize` no arquivo de configuração do X é usada para entregar o DPI, dado o tamanho de resolução da tela.
3.  Se nenhum `DisplaySize` é dado, os valores de tamanho do monitor da [DDC](https://en.wikipedia.org/wiki/Display_Data_Channel "wikipedia:Display Data Channel") são usados para definir o DPI, dado a resolução de tela.
4.  Se DDC não especifica um tamanho, é usado por padrão 75 DPI.

Para conseguir os corretos pontos por polegada(DPI), o tamanho da tela deve ser reconhecido ou configurado. Ter o correto DPI é é um requesito quando detalhes finos são necessários (como renderização de fontes). Antigamente, fabricantes tentaram criar um padrão para 96 DPI (um monitor de 10.3" deveria ser 800X600, um monitor de 13.2" deveria ser 1024X768). Atualmente, DPIs variam e podem não ser iguais horizontalmente e verticalmente. Por exemplo, um eclã panorâmico LCD de 19" 1440X900 poderia ter um DPI de 89X87\. Para configurar o DPI, o servidor Xorg tenta a auto detecção do tamanho de tela físico através da placa gráfica com DDC. ~~Quando o servidor Xorg sabe o tamanho físico da tela, ele será capaz de configurar o DPI corretamente baseado no tamanho da resolução.~~

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
    Identifier             "<default monitor>"
    DisplaySize            286 179    # Em milímetros
EndSection

```

Se você não tem as especificações físicas de altura e largura da tela, (a maioria das especificações atualmente somente listam o tamanho diagonal) você pode usar a nativa resolução do monitor (ou aspecto de proporção) e comprimento diagonal para calcular a dimensão horizontal e vertical física. Usando o teorema de pitágoras em uma tela diagonal de 13.3" com uma resolução nativa de 1280X800 (ou aspecto de proporção 16:10):

```
$ echo 'scale=5;sqrt(1280^2+800^2)' | bc  # 1509.43698

```

Isto dará o comprimento do pixel diagonal e com este valor você pode descobrir o comprimento horizontal e vertical físico (e converter eles para milímetros):

```
$ echo 'scale=5;(13.3/1509)*1280*25.4' | bc  # 286.43072
$ echo 'scale=5;(13.3/1509)*800*25.4'  | bc  # 179.01920

```

**Nota:** Este cálculo funciona para monitores com pixels quadrados; no entanto, raramente um monitor pode comprimir o aspecto de proporção (exemplo aspecto de resolução 16:10 para um 16:9). Se este for o caso, você deve mensurar o tamanho de sua tela manualmente.

#### Setting DPI manually

**Note:** While you can set any dpi you like and applications using Qt and GTK will scale accordingly, it's recommended to set it to 96, 120 (25% higher), 144 (50% higher), 168 (75% higher), 192 (100% higher) etc., to reduce scaling artifacts to GUI that use bitmaps. Reducing it below 96 dpi may not reduce size of graphical elements of GUI as typically the lowest dpi the icons are made for is 96.

For RandR compliant drivers (for example the open source ATI driver), you can set it by:

```
$ xrandr --dpi 144

```

**Note:** Applications that comply with the setting will not change immediately. You have to start them anew.

See [Execute commands after X start](/index.php/Execute_commands_after_X_start "Execute commands after X start") to make it permanent.

##### Proprietary NVIDIA driver

DPI can be set manually if you only plan to use one resolution ([DPI calculator](https://www.pxcalc.com/)):

```
Section "Monitor"
    Identifier             "Monitor0"
    Option                 "DPI" "96 x 96"
EndSection

```

You can manually set the DPI adding the options below on `/etc/X11/xorg.conf.d/20-nvidia.conf` (inside **Device** section):

```
Option              "UseEdidDpi" "False"
Option              "DPI" "96 x 96"

```

##### Manual DPI Setting Caveat

GTK very often overrides the server's DPI via the optional Xresource `Xft.dpi`. To find out whether this is happening to you, check with:

```
$ xrdb -query | grep dpi

```

With GTK library versions since 3.16, when this variable is not otherwise explicitly set, GTK sets it to 96\. To have GTK apps obey the server DPI you may need to explictly set Xft.dpi to the same value as the server. The Xft.dpi resource is the method by which some desktop environments optionally force DPI to a particular value in personal settings. Among these are [KDE](/index.php/KDE "KDE") and [TDE](/index.php/TDE "TDE").

### Display Power Management

[DPMS](/index.php/DPMS "DPMS") (Display Power Management Signaling) is a technology that allows power saving behaviour of monitors when the computer is not in use. This will allow you to have your monitors automatically go into standby after a predefined period of time.

## Composite

The Composite extension for X causes an entire sub-tree of the window hierarchy to be rendered to an off-screen buffer. Applications can then take the contents of that buffer and do whatever they like. The off-screen buffer can be automatically merged into the parent window or merged by external programs, called compositing managers. See the following article for more information: [compositing window manager](https://en.wikipedia.org/wiki/Compositing_window_manager "wikipedia:Compositing window manager")

Some window managers (e.g. [Compiz](/index.php/Compiz "Compiz"), [Enlightenment](/index.php/Enlightenment "Enlightenment"), KWin, Marco, Metacity, Muffin, Mutter, [Xfwm](/index.php/Xfwm "Xfwm")) do compositing on their own. For other window managers, a standalone composite manager can be used.

### List of composite managers

*   **[Compton](/index.php/Compton "Compton")** — Compositor (a fork of xcompmgr-dana)

	[https://github.com/yshui/compton](https://github.com/yshui/compton) || [compton](https://www.archlinux.org/packages/?name=compton)

*   **[Xcompmgr](/index.php/Xcompmgr "Xcompmgr")** — Composite window-effects manager

	[https://cgit.freedesktop.org/xorg/app/xcompmgr/](https://cgit.freedesktop.org/xorg/app/xcompmgr/) || [xcompmgr](https://www.archlinux.org/packages/?name=xcompmgr)

*   **Unagi** — Modular compositing manager which aims written in C and based on XCB

	[https://projects.mini-dweeb.org/projects/unagi](https://projects.mini-dweeb.org/projects/unagi) || [unagi](https://aur.archlinux.org/packages/unagi/)

## Tips and tricks

### Automation

This section lists utilities for automating keyboard / mouse input and window operations (like moving, resizing or raising).

| Tool | Package | Manual | [Keysym](/index.php/Keysym "Keysym")
input | Window
operations | Note |
| xautomation | [xautomation](https://www.archlinux.org/packages/?name=xautomation) | [xte(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xte.1) | Yes | No | Also contains screen scraping tools. Cannot simulate F13+. |
| xdo | [xdo-git](https://aur.archlinux.org/packages/xdo-git/) | [xdo(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdo.1) | No | Yes | Small X utility to perform elementary actions on windows. |
| xdotool | [xdotool](https://www.archlinux.org/packages/?name=xdotool) | [xdotool(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdotool.1) | Yes | Yes | [Very buggy](https://github.com/jordansissel/xdotool/issues) and not in active development, e.g: has broken CLI parsing.[[2]](https://github.com/jordansissel/xdotool/issues/14#issuecomment-327968132)[[3]](https://github.com/jordansissel/xdotool/issues/71) |
| xvkbd | [xvkbd](https://aur.archlinux.org/packages/xvkbd/) | [xvkbd(1)](http://t-sato.in.coocan.jp/xvkbd/#option) | Yes | No | Virtual keyboard for Xorg, also has the `-text` option for sending characters. |

See also [Clipboard#Tools](/index.php/Clipboard#Tools "Clipboard") and [an overview of X automation tools](https://venam.nixers.net/blog/unix/2019/01/07/win-automation.html).

### Nested X session

To run a nested session of another desktop environment:

```
$ /usr/bin/Xnest :1 -geometry 1024x768+0+0 -ac -name Windowmaker & wmaker -display :1

```

This will launch a Window Maker session in a 1024 by 768 window within your current X session.

This needs the package [xorg-server-xnest](https://www.archlinux.org/packages/?name=xorg-server-xnest) to be installed.

### Starting GUI programs remotely

See main article: [OpenSSH#X11 forwarding](/index.php/OpenSSH#X11_forwarding "OpenSSH").

### On-demand disabling and enabling of input sources

With the help of *xinput* you can temporarily disable or enable input sources. This might be useful, for example, on systems that have more than one mouse, such as the ThinkPads and you would rather use just one to avoid unwanted mouse clicks.

[Install](/index.php/Install "Install") the [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) package.

Find the name or ID of the device you want to disable:

```
$ xinput

```

For example in a Lenovo ThinkPad T500, the output looks like this:

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

Disable the device with `xinput --disable *device*`, where *device* is the device ID or name of the device you want to disable. In this example we will disable the Synaptics Touchpad, with the ID 10:

```
$ xinput --disable 10

```

To re-enable the device, just issue the opposite command:

```
$ xinput --enable 10

```

Alternatively using the device name, the command to disable the touchpad would be:

```
$ xinput --disable "SynPS/2 Synaptics TouchPad"

```

### Killing application with hotkey

Run script on hotkey:

```
#!/bin/bash
windowFocus=$(xdotool getwindowfocus);
pid=$(xprop -id $windowFocus | grep PID);
kill -9 $pid

```

Deps: [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop), [xdotool](https://www.archlinux.org/packages/?name=xdotool)

### Block TTY access

To block tty access when in an X add the following to [xorg.conf](#Configuration):

```
Section "ServerFlags"
    Option "DontVTSwitch" "True"
EndSection

```

### Prevent a user from killing X

To prevent a user from killing when it is running add the following to [xorg.conf](#Configuration):

```
Section "ServerFlags"
    Option "DontZap"      "True"
EndSection

```

## Troubleshooting

### General

If a problem occurs, view the log stored in either `/var/log/` or, for the rootless X default since v1.16, in `~/.local/share/xorg/`. [GDM](/index.php/GDM "GDM") users should check the [systemd journal](/index.php/Systemd_journal "Systemd journal"). [[4]](https://bbs.archlinux.org/viewtopic.php?id=184639)

The logfiles are of the form `Xorg.n.log` with `n` being the display number. For a single user machine with default configuration the applicable log is frequently `Xorg.0.log`, but otherwise it may vary. To make sure to pick the right file it may help to look at the timestamp of the X server session start and from which console it was started. For example:

 `$ grep -e Log -e tty Xorg.0.log` 
```
[    40.623] (==) Log file: "/home/archuser/.local/share/xorg/Xorg.0.log", Time: Thu Aug 28 12:36:44 2014
[    40.704] (--) controlling tty is VT number 1, auto-enabling KeepTty
```

*   In the logfile then be on the lookout for any lines beginning with `(EE)`, which represent errors, and also `(WW)`, which are warnings that could indicate other issues.
*   If there is an *empty* `.xinitrc` file in your `$HOME`, either delete or edit it in order for X to start properly. If you do not do this X will show a blank screen with what appears to be no errors in your `Xorg.0.log`. Simply deleting it will get it running with a default X environment.
*   If the screen goes black, you may still attempt to switch to a different virtual console (e.g. `Ctrl+Alt+F6`), and blindly log in as root. You can do this by typing `root` (press `Enter` after typing it) and entering the root password (again, press `Enter` after typing it).

	You may also attempt to kill the X server with:

	 `# pkill -x X` 

	If this does not work, reboot blindly with:

	 `# reboot` 

*   Check specific pages in [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices") if you have issues with keyboard, mouse, touchpad etc.
*   Search for common problems in [ATI](/index.php/ATI "ATI"), [Intel](/index.php/Intel "Intel") and [NVIDIA](/index.php/NVIDIA "NVIDIA") articles.

### Black screen, No protocol specified.., Resource temporarily unavailable for all or some users

X creates configuration and temporary files in current user's home directory. Make sure there is free disk space available on the partition your home directory resides in. Unfortunately, X server does not provide any more obvious information about lack of disk space in this case.

### DRI with Matrox cards stopped working

If you use a Matrox card and DRI stopped working after upgrading to Xorg, try adding the line:

```
Option "OldDmaInit" "On"

```

to the Device section that references the video card in `xorg.conf`.

### Frame-buffer mode problems

If X fails to start with the following log messages,

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

[Uninstall](/index.php/Uninstall "Uninstall") the [xf86-video-fbdev](https://www.archlinux.org/packages/?name=xf86-video-fbdev) package.

### Program requests "font '(null)'"

Error message: `unable to load font `(null)'`.

Some programs only work with bitmap fonts. Two major packages with bitmap fonts are available, [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) and [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi). You do not need both; one should be enough. To find out which one would be better in your case, try `xdpyinfo` from [xorg-xdpyinfo](https://www.archlinux.org/packages/?name=xorg-xdpyinfo), like this:

```
$ xdpyinfo | grep resolution

```

and use what is closer to the shown value.

### Recovery: disabling Xorg before GUI login

If Xorg is set to boot up automatically and for some reason you need to prevent it from starting up before the login/display manager appears (if the system is wrongly configured and Xorg does not recognize your mouse or keyboard input, for instance), you can accomplish this task with two methods.

*   Change default target to rescue.target. See [systemd#Change default target to boot into](/index.php/Systemd#Change_default_target_to_boot_into "Systemd").
*   If you have not only a faulty system that makes Xorg unusable, but you have also set the GRUB menu wait time to zero, or cannot otherwise use GRUB to prevent Xorg from booting, you can use the Arch Linux live CD. Follow the [installation guide](/index.php/Installation_guide#Format_the_partitions "Installation guide") about how to mount and chroot into the installed Arch Linux. Alternatively try to switch into another [tty](/index.php/Tty "Tty") with `Ctrl+Alt` + function key (usually from `F1` to `F7` depending on which is not used by X), login as root and follow steps below.

Depending on setup, you will need to do one or more of these steps:

*   [Disable](/index.php/Disable "Disable") the [display manager](/index.php/Display_manager "Display manager").
*   Disable the [automatic start of the X](/index.php/Start_X_at_login "Start X at login").
*   Rename the `~/.xinitrc` or comment out the `exec` line in it.

### X clients started with "su" fail

If you are getting "Client is not authorized to connect to server", try adding the line:

```
session        optional        pam_xauth.so

```

to `/etc/pam.d/su` and `/etc/pam.d/su-l`. `pam_xauth` will then properly set environment variables and handle `xauth` keys.

### X failed to start: Keyboard initialization failed

If the filesystem (specifically `/tmp`) is full, `startx` will fail. `/var/log/Xorg.0.log` will end with:

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

Make some free space on the relevant filesystem and X will start.

### Rootless Xorg

Xorg may run with standard user privileges with the help of [systemd-logind(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-logind.8), see [[5]](https://fedoraproject.org/wiki/Changes/XorgWithoutRootRights) and [FS#41257](https://bugs.archlinux.org/task/41257). The requirements for this are:

*   Starting X via [xinit](/index.php/Xinit "Xinit"); display managers are not supported
*   [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"); implementations in proprietary display drivers fail [auto-detection](https://cgit.freedesktop.org/xorg/xserver/tree/hw/xfree86/xorg-wrapper.c#n222) and require manually setting `needs_root_rights = no` in `/etc/X11/Xwrapper.config`.

If you do not fit these requirements, re-enable root rights in `/etc/X11/Xwrapper.config`:

 `/etc/X11/Xwrapper.config`  `needs_root_rights = *yes*` 

See also [Xorg.wrap(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xorg.wrap.1) and [Systemd/User#Xorg as a systemd user service](/index.php/Systemd/User#Xorg_as_a_systemd_user_service "Systemd/User").

[GDM](/index.php/GDM "GDM") also runs Xorg without root privileges by default when [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") is used.

#### Broken redirection

While user Xorg logs are stored in `~/.local/share/xorg/Xorg.log`, they do not include the output from the X session. To re-enable redirection, start X with the `-keeptty` flag:

```
exec startx -- -keeptty > ~/.xorg.log 2>&1

```

Or copy `/etc/X11/xinit/xserverrc` to `~/.xserverrc`, and append `-keeptty`. See [[6]](https://bbs.archlinux.org/viewtopic.php?pid=1446402#p1446402).

### A green screen whenever trying to watch a video

Your color depth is set wrong. It may need to be 24 instead of 16, for example.

### SocketCreateListener error

If X terminates with error message "SocketCreateListener() failed", you may need to delete socket files in `/tmp/.X11-unix`. This may happen if you have previously run Xorg as root (e.g. to generate an `xorg.conf`).

### Invalid MIT-MAGIC-COOKIE-1 key when trying to run a program as root

That error means that only the current user has access to the X server. The solution is to give access to root:

```
$ xhost +si:localuser:root

```

That line can also be used to give access to X to a different user than root.

## See also

*   [Xplain](https://magcius.github.io/xplain/article/) - In-depth explanation of the X Window System
*   [Xorg(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xorg.1) - Xorg's Manual Page
*   [Gentoo/Xorg#Configuration](https://wiki.gentoo.org/wiki/Xorg/Guide/en#Configuration) - Gentoo Wiki's Xorg Configuration page