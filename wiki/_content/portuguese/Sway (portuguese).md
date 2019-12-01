**Status de tradução:** Esse artigo é uma tradução de [Sway](/index.php/Sway "Sway"). Data da última tradução: 2019-11-16\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Sway&diff=0&oldid=588993) na versão em inglês.

*sway* é um compositor para [Wayland](/index.php/Wayland_(Portugu%C3%AAs) "Wayland (Português)") feito para ser totalmente compatível com [i3](/index.php/I3 "I3"). De acordo com [o site oficial](https://swaywm.org):

	Sway é um compositor dinâmico para Wayland e possui configuração compatível com o gerenciador de janelas i3 para X11\. Funciona com sua existente configuração do i3 e suporta a maioria de suas funcionalidades, alem de extras.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Iniciando](#Iniciando)
    *   [2.1 Pelo TTY](#Pelo_TTY)
    *   [2.2 Por um gerenciador de login](#Por_um_gerenciador_de_login)
*   [3 Configuração](#Configuração)
    *   [3.1 Teclado](#Teclado)
    *   [3.2 Barra de status](#Barra_de_status)
    *   [3.3 Papel de parede](#Papel_de_parede)
    *   [3.4 Dispositivos de entrada](#Dispositivos_de_entrada)
    *   [3.5 HiDPI](#HiDPI)
    *   [3.6 Atalhos customizados](#Atalhos_customizados)
    *   [3.7 Xresources](#Xresources)
    *   [3.8 Rode programas nativamente no Wayland (sem suporte do XWayland)](#Rode_programas_nativamente_no_Wayland_(sem_suporte_do_XWayland))
*   [4 Dicas e truques](#Dicas_e_truques)
    *   [4.1 Iniciar automaticamente após login](#Iniciar_automaticamente_após_login)
    *   [4.2 Alternar luz de fundo](#Alternar_luz_de_fundo)
    *   [4.3 Capturar tela](#Capturar_tela)
    *   [4.4 Controle swaynag com o teclado](#Controle_swaynag_com_o_teclado)
    *   [4.5 Mudar o tamanho e tema de cursor para programas XWayland](#Mudar_o_tamanho_e_tema_de_cursor_para_programas_XWayland)
*   [5 Solução de problemas](#Solução_de_problemas)
    *   [5.1 Lançadores de aplicativos](#Lançadores_de_aplicativos)
    *   [5.2 VirtualBox](#VirtualBox)
    *   [5.3 Sway socket não detectado](#Sway_socket_não_detectado)
    *   [5.4 Não foi possível pegar o caminho do socket](#Não_foi_possível_pegar_o_caminho_do_socket)
    *   [5.5 Atalhos e formato do teclado](#Atalhos_e_formato_do_teclado)
    *   [5.6 Programas java](#Programas_java)
*   [6 Veja também](#Veja_também)

## Instalação

*sway* pode ser [instalado](/index.php/Instala "Instala") com o pacote [sway](https://www.archlinux.org/packages/?name=sway). A versão de desenvolvimento pode ser instalada usando [wlroots-git](https://aur.archlinux.org/packages/wlroots-git/) e [sway-git](https://aur.archlinux.org/packages/sway-git/). É aconselhável sempre atualizar o *wlroots* quando você atualiza o *sway*, devido a forte dependência.

Você pode instalar também [swaylock](https://www.archlinux.org/packages/?name=swaylock) e [swayidle](https://www.archlinux.org/packages/?name=swayidle) para bloqueio de tela e gerenciador de inatividade.

## Iniciando

**Dica:** Veja [Wayland#Bibliotecas GUI](/index.php/Wayland_(Portugu%C3%AAs)#Bibliotecas_GUI "Wayland (Português)") para configurar bibliotecas de decoração de janela com variáveis de ambiente adequadas.

### Pelo TTY

Para iniciar o Sway, simplesmente digite "sway" no TTY.

### Por um gerenciador de login

**Nota:** Sway não suporta gerenciadores de login oficialmente.[[1]](https://github.com/swaywm/sway/pull/3634#issuecomment-462779163)

A sessão do sway está localizada em `/usr/share/wayland-sessions/sway.desktop`, ela é automaticamente reconhecida por qualquer gerenciador de login moderno como [GDM](/index.php/GDM_(Portugu%C3%AAs) "GDM (Português)") e [SDDM](/index.php/SDDM "SDDM").

É também possível rodar sway como um [serviço de usuário do systemd](https://github.com/swaywm/sway/wiki/Systemd-integration#running-sway-itself-as-a---user-service) através do gerenciador de login.

Você também pode usar gerenciador de login somente texto, veja [Gerenciadores de exibição#Console](/index.php/Gerenciadores_de_exibi%C3%A7%C3%A3o#Console "Gerenciadores de exibição").

## Configuração

Se você já usa o i3, então copie sua configuração para `~/.config/sway/config` e deve funcionar sem problemas. Caso contrário, copie o arquivo de exemplo da configuração para `~/.config/sway/config`. Ele está localizado em `/etc/sway/config`, a menos que a flag `DFALLBACK_CONFIG_DIR` tenha sido configurada. Veja [sway(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sway.5) para informações sobre a configuração.

### Teclado

Por padrão, sway inicia com o teclado US QWERTY. Para configuração por `input`:

 `~/.config/sway/config` 
```
 input * xkb_layout "us,de,ru"
 input * xkb_variant "colemak,,typewriter"
 input * xkb_options "grp:win_space_toggle"
 input "MANUFACTURER1 Keyboard" xkb_model "pc101"
 input "MANUFACTURER2 Keyboard" xkb_model "jp106"

```

Mais detalhes estão disponíveis em [xkeyboard-config(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xkeyboard-config.7) e [sway-input(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sway-input.5).

O teclado pode também ser configurado usando variáveis de ambiente (`XKB_DEFAULT_LAYOUT`, `XKB_DEFAULT_VARIANT`, etc.) quando inicializando o sway.

### Barra de status

Instalando o programa [i3status](https://www.archlinux.org/packages/?name=i3status) é uma maneira simples de conseguir uma pratica, padrão linha de status. Tudo que se tem a fazer é adicionar o seguinte trecho no final da sua configuração do sway:

 `~/.config/sway/config` 
```
 bar {
  status_command i3status
 }

```

Se você quer que o i3status tenha saída colorida, você pode ajustar da seguinte maneira a configuração dele:

 `~/.config/i3status/config` 
```
general {
        colors = true
        interval = 5
}

```

Em ambos os exemplos, os arquivos de configuração instalados a nível de sistema foram copiados para o diretório do usuário e então modificados.

**Dica:** [waybar](https://www.archlinux.org/packages/?name=waybar) é uma alternativa a barra de status incluída no sway (swaybar).

### Papel de parede

Desde a versão 1.1.1 o gerenciamento de papel de parede do projeto SwayWM foi movido para [swaybg](https://www.archlinux.org/packages/?name=swaybg), que é necessário para executar o comando `output`.

Esta linha, que pode ser adicionada ao final da sua configuração do sway, define o papel de parede em todas as telas (`output` seleciona todos com nome `"*"`):

 `~/.config/sway/config` 
```
 output "*" bg /home/onny/pictures/fredwang_norway.jpg fill

```

Você tem que mudar o nome do arquivo e caminho de acordo com seu papel de parede.

### Dispositivos de entrada

É possível realizar a configuração de específicos dispositivos de entrada. Por exemplo para habilitar toque-para-clicar e deslize natural para um touchpad, adicione um bloco de `input`:

 `~/.config/sway/config` 
```
input "2:14:ETPS/2_Elantech_Touchpad" {
    tap enabled
    natural_scroll enabled
}

```

O identificador do dispositivo pode ser consultado com:

```
$ swaymsg -t get_inputs

```

A saída do comando, algumas vezes tem um "\" para escapar símbolos como "/" (por exemplo, `"2:14:ETPS\/2_Elantech_Touchpad"`) e isto precisa ser removido.

Mais documentação e opções como perfis de aceleração podem ser encontradas em [sway-input(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sway-input.5).

### HiDPI

Configure o fator de escala das suas telas com o comando `output` em seu arquivo de configuração. O fator de escala pode ser fracionário, mas é normalmente 2 para telas HiDPI.

```
output <nome> scale <fator>

```

Você pode encontrar o nome da sua tela com o seguinte comando:

```
$ swaymsg -t get_outputs

```

### Atalhos customizados

[Teclas especiais](/index.php/Extra_keyboard_keys "Extra keyboard keys") no seu teclado podem ser usadas para executar comandos, por exemplo para controlar o seu volume, o brilho do seu monitor ou seu media player:

 `~/.config/sway/config` 
```
bindsym XF86AudioRaiseVolume exec pactl set-sink-volume @DEFAULT_SINK@ +5%
bindsym XF86AudioLowerVolume exec pactl set-sink-volume @DEFAULT_SINK@ -5%
bindsym XF86AudioMute exec pactl set-sink-mute @DEFAULT_SINK@ toggle
bindsym XF86AudioMicMute exec pactl set-source-mute @DEFAULT_SOURCE@ toggle
bindsym XF86MonBrightnessDown exec brightnessctl set 5%-
bindsym XF86MonBrightnessUp exec brightnessctl set +5%
bindsym XF86AudioPlay exec playerctl play-pause
bindsym XF86AudioNext exec playerctl next
bindsym XF86AudioPrev exec playerctl previous

```

Para controlar o brilho voce pode usar [brightnessctl](https://www.archlinux.org/packages/?name=brightnessctl) ou [light](https://www.archlinux.org/packages/?name=light). Para uma lista de utilitários que controlam o brilho e correção de cor veja [Luz de fundo](/index.php/Backlight "Backlight").

### Xresources

Copie `~/.Xresources` para `~/.Xdefaults` para usá-lo no Sway.

### Rode programas nativamente no Wayland (sem suporte do XWayland)

Primeiro, tenha certeza que o kit de ferramentas ou bibliotecas de todos os programas que estão e serão instalados [suportam Wayland](/index.php/Wayland_(Portugu%C3%AAs)#Bibliotecas_GUI "Wayland (Português)"). Então adicione a seguinte linha no seu arquivo de configuração do sway para desabilitar o suporte ao XWayland:

 `~/.config/sway/config` 
```
xwayland disable

```

**Nota:** Alguns programas, como [Firefox](/index.php/Firefox#Wayland "Firefox"), [bemenu](#Lançadores_de_aplicativos) ou programas baseados no [Qt5](/index.php/Wayland_(Portugu%C3%AAs)#Qt_5 "Wayland (Português)"), também precisam de especificas variáveis de ambiente configuradas para rodarem nativamente em wayland.

**Nota:** Numa recente instalação do Sway, você precisa mudar o menu e terminal padrão porquê eles dependem do XWayland.

## Dicas e truques

### Iniciar automaticamente após login

Para rodar sway no tty1 ao logar com teclado padrão US, edite:

 `~/.bash_profile` 
```
if [[ -z $DISPLAY ]] && [[ $(tty) = /dev/tty1 ]]; then
  XKB_DEFAULT_LAYOUT=us exec sway
fi

```

Para rodar sway no tty1 ao logar com teclado padrão BR, edite:

 `~/.bash_profile` 
```
if [[ -z $DISPLAY ]] && [[ $(tty) = /dev/tty1 ]]; then
  XKB_DEFAULT_LAYOUT=br exec sway
fi

```

### Alternar luz de fundo

Para desligar (e ligar) suas telas com uma tecla (exemplo `Pause`), crie um atalho na sua `config` do Sway para o seguinte script:

```
#!/bin/sh
read lcd < /tmp/lcd
    if [ "$lcd" -eq "0" ]; then
        swaymsg "output * dpms on"
        echo 1 > /tmp/lcd
    else
        swaymsg "output * dpms off"
        echo 0 > /tmp/lcd
    fi

```

### Capturar tela

Você pode fazer uso do [grim](https://www.archlinux.org/packages/?name=grim) or [swayshot](https://aur.archlinux.org/packages/swayshot/) para capturas de tela e [wf-recorder-git](https://aur.archlinux.org/packages/wf-recorder-git/) para vídeo. Opcionalmente, [slurp](https://www.archlinux.org/packages/?name=slurp) pode ser usado para selecionar parte da tela a ser capturada.

Tire uma captura de tela da tela toda:

```
$ grim captura-de-tela.png

```

Tire uma captura de tela de parte da tela:

```
$ grim -g "$(slurp)" captura-de-tela.png

```

Grave um vídeo de toda a tela:

```
$ wf-recorder -o gravação.mp4

```

Grave um vídeo de parte da tela:

```
$ wf-recorder -g "$(slurp)"

```

Exemplo de uso do [grim](https://www.archlinux.org/packages/?name=grim), [slurp](https://www.archlinux.org/packages/?name=slurp) e [wl-clipboard](https://www.archlinux.org/packages/?name=wl-clipboard), captura de tela diretamente tirada com tecla Print para a área de transferência.

 `~/.config/sway/config` 
```
bindsym --release Print exec grim -g \"$(slurp)" - | wl-copy

```

### Controle swaynag com o teclado

Swaynag, o programa de aviso/prompt padrão que vem no sway, somente suporta interação do usuário com o mouse. Um programa auxiliar como [swaynagmode](https://aur.archlinux.org/packages/swaynagmode/) pode ser usado para habilitar interação via atalhos do teclado.

Swaynagmode funciona lançando swaynag, e então escutando sinais que podem acionar ações como selecionar o próximo botão, fechar o prompt, ou aceitar o botão selecionado. Estes sinais são enviados ao lançar outra instância do script *swaynagmode* com controle de argumento, como `swaynagmode --select right` ou `swaynagmode --confirm`.

Swaynagmode por padrão aciona o modo do sway `nag` ao inicializar, seguido por `default` na saída. Isto facilita a definição de atalhos na sua configuração do sway:

 `~/.config/sway/config` 
```
set $nag exec swaynagmode
mode "nag" {
  bindsym {
    Ctrl+d    mode "default"

    Ctrl+c    $nag --exit
    q         $nag --exit
    Escape    $nag --exit

    Return    $nag --confirm

    Tab       $nag --select prev
    Shift+Tab $nag --select next

    Left      $nag --select next
    Right     $nag --select prev

    Up        $nag --select next
    Down      $nag --select prev
  }
}

```

Note que, a partir da versão do sway 1.2, diferencia-se maiúsculo/minúsculo em nomes de modos.

Você pode configurar o sway para usar swaynagmode com o comando de configuração `swaynag_command swaynagmode`.

### Mudar o tamanho e tema de cursor para programas XWayland

Para definir [temas de cursor](/index.php/Temas_de_cursor "Temas de cursor") e tamanho:

 `~/.config/sway/config` 
```
seat seat0 xcursor_theme *tema_do_cursor* *tamanho_do_cursor*

```

Onde `*my_cursor_theme*` pode ser definido ou trocado por um valor específico como `default`, `Adwaita` ou `Simple-and-Soft`, e `*my_cursor_size*` um valor como `48`.

Você pode inspecionar os seus valores com `echo $XCURSOR_SIZE` e `echo $XCURSOR_THEME`.

Note que você precisa reiniciar o programa XWayland para ver as mudanças.

## Solução de problemas

### Lançadores de aplicativos

i3-dmenu-desktop, [dmenu](https://www.archlinux.org/packages/?name=dmenu), e [rofi](https://www.archlinux.org/packages/?name=rofi) todos funcionam relativamente bem no Sway, no entanto, rodam sob XWayland e sofrem do mesmo problema, onde eles podem não responder se o cursor é movido para uma janela nativa do Wayland. O motivo para isso acontecer é que clientes/janelas do Wayland não tem acesso a dispositivos de entrada a menos que eles possuam foco na tela. O servidor XWayland é um cliente para o compositor Wayland, então um de seus clientes deve ter foco para ter acesso a entrada do usuario. No entanto, uma vez que um de seus clientes tem foco, pode captar as entradas e fazê-la disponível para todos os clientes XWayland através do protocolo X11\. Mover o cursor para uma janela XWayland e pressionar a tecla Escape deve resolver, algumas vezes rodar `pkill` resolve também.

[bemenu](https://www.archlinux.org/packages/?name=bemenu) é o substituto nativo do dmenu para Wayland que pode opcionalmente ser combinado com [j4-dmenu-desktop](https://aur.archlinux.org/packages/j4-dmenu-desktop/) para prover um lançador de arquivos desktop nativo do Wayland (como i3-dmenu-desktop faz):

```
j4-dmenu-desktop --dmenu='bemenu -i --nb "#3f3f3f" --nf "#dcdccc" --fn "pango:DejaVu Sans Mono 12"' --term='termite'

```

Você pode precisar configurar a variavel de ambiente `BEMENU_BACKEND` para "wayland" se você escolhe desabilitar o XWayland.

Você pode combinar seu terminal flutuante com fzf como discutido em uma [issue do GitHub](https://github.com/swaywm/sway/issues/1367).

### VirtualBox

Sway não funciona bem(ou de qualquer modo) sobre [VirtualBox](/index.php/VirtualBox_(Portugu%C3%AAs) "VirtualBox (Português)").

### Sway socket não detectado

Usando um argumento do `swaymsg`, como `swaymsg -t get_outputs`, irá algumas vezes retornar a mensagem:

```
sway socket not detected.
ERROR: Unable to connect to

```

Quando roda dentro de um terminal multiplex (como gnu screen ou tmux). Isto significa que `swaymsg` não pôde se conectar ao socket provido pelo `SWAYSOCK`.

Para ver qual o atual valor do `SWAYSOCK`, digite:

```
$ env | fgrep SWAYSOCK
SWAYSOCK=/run/user/1000/sway-ipc.1000.4981.sock

```

Para resolver este problema, você pode tentar definir o socket baseado no atual processo do sway:

```
$ export SWAYSOCK=/run/user/$(id -u)/sway-ipc.$(id -u).$(pgrep -x sway).sock

```

Para evitar este erro, rode o comando fora de um multiplex.

### Não foi possível pegar o caminho do socket

Solicitar mensagens do `swaymsg -t` no tty pode retornar a seguinte mensagem:

```
Unable to retrieve socket path

```

A variável de ambiente `SWAYSOCK` é configurada depois do lançamento do Sway, então uma resolução para este erro é solicitar `swaymsg -t [message]` dentro de um terminal no Sway.

### Atalhos e formato do teclado

Por padrão, se voce esta usando mais do que um formato de teclado, exemplo `input * xkb_layout "us,ru"`, atalhos podem se tornar quebrados quando você troca para um teclado secundário.

Graças ao [https://github.com/swaywm/sway/pull/3058](https://github.com/swaywm/sway/pull/3058), tudo que você precisa fazer é adicionar `--to-code` a linhas do `bindsym` como esta:

```
bindsym --to-code {
  $mod+$left focus left
  $mod+$down focus down
  $mod+$up focus up
  $mod+$right focus right
}

```

### Programas java

Alguns programas baseados no Java irão mostrar uma tela branca quando abertos, por exemplo qualquer editor Intellij. Para solucionar isto, o programa pode ser iniciado com a variável de ambiente `_JAVA_AWT_WM_NONREPARENTING` configurada para 1.

Se você rodar o programa por um lançador como [rofi](https://www.archlinux.org/packages/?name=rofi) ou [dmenu](https://www.archlinux.org/packages/?name=dmenu), você pode querer modificar a entrada desktop do aplicativo como descrito em [Entradas de desktop#Modificar variáveis de ambiente](/index.php/Entradas_de_desktop#Modificar_variáveis_de_ambiente "Entradas de desktop").

## Veja também

*   [Projeto no GitHub](https://github.com/swaywm/sway)
*   [Wiki oficial do Sway](https://github.com/swaywm/sway/wiki)
*   [Página git no sr.ht](https://git.sr.ht/~sircmpwn/sway)
*   [Site](https://swaywm.org)
*   [Anunciando o lançamento do sway 1.0](https://drewdevault.com/2019/03/11/Sway-1.0-released.html)