Related articles

*   [Window manager](/index.php/Window_manager "Window manager")
*   [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers")

[bspwm](https://github.com/baskerville/bspwm) é um gerenciador de janelas leve, lado a lado, e minimalista escrito em C que organiza janelas em [árvore binária](https://pt.wikipedia.org/wiki/%C3%81rvore_bin%C3%A1ria) completa. Seu tamanho instalado é menor que 600KB. O bspwm tem suporte para [EWMH](https://standards.freedesktop.org/wm-spec/wm-spec-latest.html) e múltiplos monitores. Ele responde apenas a eventos e mensagens X que recebe em um soquete dedicado de um programa incluído em seu pacote, o bspc.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Iniciando](#Iniciando)
*   [3 Configuração](#Configura.C3.A7.C3.A3o)
    *   [3.1 Para múltiplos monitores](#Para_m.C3.BAltiplos_monitores)
    *   [3.2 Regras](#Regras)
    *   [3.3 Painéis](#Pain.C3.A9is)
        *   [3.3.1 Usando lemonbar](#Usando_lemonbar)
        *   [3.3.2 Usando polybar](#Usando_polybar)
    *   [3.4 Scratchpad](#Scratchpad)
    *   [3.5 Configurações diferentes de monitores para diferentes máquinas](#Configura.C3.A7.C3.B5es_diferentes_de_monitores_para_diferentes_m.C3.A1quinas)
    *   [3.6 Configurar um desktop onde todas as janelas estão flutuando](#Configurar_um_desktop_onde_todas_as_janelas_est.C3.A3o_flutuando)
*   [4 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [4.1 Tela em branco e atalhos de teclado não funcionam](#Tela_em_branco_e_atalhos_de_teclado_n.C3.A3o_funcionam)
    *   [4.2 Caixa de janela maior que a aplicação real](#Caixa_de_janela_maior_que_a_aplica.C3.A7.C3.A3o_real)
    *   [4.3 Problemas com aplicações java](#Problemas_com_aplica.C3.A7.C3.B5es_java)
    *   [4.4 Problemas com atalhos de teclado usando fish](#Problemas_com_atalhos_de_teclado_usando_fish)
    *   [4.5 Mensagens de erro "Não foi possível pegar a chave 43 com modfield 68" no início](#Mensagens_de_erro_.22N.C3.A3o_foi_poss.C3.ADvel_pegar_a_chave_43_com_modfield_68.22_no_in.C3.ADcio)
*   [5 Veja também](#Veja_tamb.C3.A9m)

## Instalação

[Instale](/index.php/Instale "Instale") [bspwm](https://www.archlinux.org/packages/?name=bspwm), ou [bspwm-git](https://aur.archlinux.org/packages/bspwm-git/) versão de desenvolvimento. Bspwm não manipula nenhuma entrada de teclado e, em vez disso, fornece o programa `bspc` como interface. Para atalhos de teclado, você terá que configurar um daemon de hotkey [sxhkd](https://www.archlinux.org/packages/?name=sxhkd) ([sxhkd-git](https://aur.archlinux.org/packages/sxhkd-git/) versão de desenvolvimento).

## Iniciando

Para começar o bspwm ao iniciar sessão, adicione ao arquivo `~/.xinitrc` ou `~/.xprofile` (dependendo de como escolheu iniciar o X [Xorg (Português)#Running Xorg](/index.php/Xorg_(Portugu%C3%AAs)#Running_Xorg "Xorg (Português)")):

```
sxhkd &
exec bspwm

```

## Configuração

Importante: Certifique-se de que sua variável de ambiente $ XDG_CONFIG_HOME esteja configurada ou seu bspwmrc não será encontrado. Isso pode ser feito digitando `XDG_CONFIG_HOME="$HOME/.config"` e `export XDG_CONFIG_HOME` para `~/.profile`.

Exemplos de configuração podem ser encontrados em `/usr/share/doc/bspwm/examples/` e [GitHub](https://github.com/baskerville/bspwm/blob/master/examples/).

Crie os diretórios `~ / .config / bspwm /` e `~ / .config / sxhkd /` e copie `/ usr / share / doc / bspwm / examples / bspwmrc` para `~ / .config / bspwm /` e `/ usr / share / doc / bspwm / examples / sxhkdrc` para `~ / .config / sxhkd /`. Nestes dois arquivos, as configurações e combinações de teclas serão definidas, respectivamente. Finalmente, torne o arquivo bspwmrc executável, com `chmod + x ~ / .config / bspwm / bspwmrc`.

As opções de configuração para cada arquivo são listadas e descritas em [1 bspwm( 1 )](https://jlk.fjfi.cvut.cz/arch/manpages/man/bspwm.) e [1 sxhkd( 1 )](https://jlk.fjfi.cvut.cz/arch/manpages/man/sxhkd.).

#### Para múltiplos monitores

Exemplo de configuração do bspwmrc para dez áreas de trabalho para um só monitor:

```
bspc monitor -d I II III IV V VI VII VIII IX X

```

Para mais de um monitor, um exemplo com 3 seria semelhante a esse:

```
bspc monitor DVI-I-1 -d I II III IV
bspc monitor DVI-I-2 -d V VI VII
bspc monitor DP-1 -d VIII IX X

```

Use `xrandr -q` ou `bspc query -M` para saber os nomes dos monitores que deseja.

O número total de área de trabalho foi mantido em dez no exemplo acima. Isso é para que cada área de trabalho ainda possa ser endereçada com `super + {1-9,0`} no sxhkdrc.

### Regras

Há duas maneiras de definir regras de comportamento para as janelas (a partir de [cd97a32](https://github.com/baskerville/bspwm/commit/cd97a3290aa8d36346deb706fa307f5f8faa2f34)).

A primeira é usando o comando de regra interno, conforme mostrado no exemplo bspwmrc:

```
bspc rule -a Gimp desktop=^8 follow=on state=floating
bspc rule -a Chromium desktop=^2
bspc rule -a mplayer2 state=floating
bspc rule -a Kupfer.py focus=on
bspc rule -a Screenkey manage=off

```

A segunda opção é usar um comando de regra externa. Isso é mais complexo, mas pode permitir que você crie regras de janelas mais específicas. Veja [estes exemplos](https://github.com/baskerville/bspwm/tree/master/examples/external_rules) para um comando de regra de amostra.

Se uma determinada janela não estiver se comportando de acordo com suas regras, verifique o nome da classe do programa. Isso pode ser feito executando `xprop | grep WM_CLASS` para ter certeza de que você está usando a string apropriada(pra isso precisa ter [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop) instalado).

### Painéis

#### Usando lemonbar

Um exemplo para [lemonbar-git](https://aur.archlinux.org/packages/lemonbar-git/) é fornecido na página do GitHub. Você também pode encontar mais exemplos na nossa wiki [lemonbar](/index.php/Lemonbar "Lemonbar"). O painel será executado adicionando `panel &` na sua bspwmrc. Verifique as dependências para as opções desejadas.

Para exibir informações do sistema na sua barra de status, você pode usar várias chamadas do sistema. Este exemplo mostra como editar seu `panel` para exibir o estado de volume no mesmo:

```
panel_volume()
{
        volStatus=$(amixer get Master | tail -n 1 | cut -d '[' -f 4 | sed 's/].*//g')
        volLevel=$(amixer get Master | tail -n 1 | cut -d '[' -f 2 | sed 's/%.*//g')
        # is alsa muted or not muted?
        if [ "$volStatus" == "on" ]
        then
                echo "%{Fyellowgreen} $volLevel %{F-}"
        else
                # If it is muted, make the font red
                echo "%{Findianred} $volLevel %{F-}"
        fi
}
```

Em seguida, é só verirficar se já está invocado e redirecionado para `$PANEL_FIFO`:

```
while true; do
echo "S" "$(panel_volume) $(panel_clock)" > "$PANEL_FIFO"
        sleep 1s
done &

```

#### Usando polybar

Polybar é uma ferramenta rápida e fácil de usar para criar barra de status; e também é altamente personalizável. Polybar possui um módulo para bspwm que permite gerenciar as áreas de trabalho e exibe informações da mesma semelhante ao i3status no [i3](https://www.archlinux.org/groups/x86_64/i3/). Polybar pode ser instalado pelo [bspwm](https://www.archlinux.org/packages/?name=bspwm) e [bspwm-git](https://aur.archlinux.org/packages/bspwm-git/). Então crie o diretório `~/.config/polybar` e copie para o mesmo o arquivo `/usr/share/doc/polybar/config`. Agora é só adicionar no seu bspwmrc:

```
polybar example &

```

Note que "example" é o nome da sua barra no arquivo de configuração.

### Scratchpad

Voce pode emular um terminal suspenso (como o recurso de rascunho do i3 se voce colocar um terminal nele) usando as flags da janela do bspwm. Anexe o seguinte ao final do arquivo de configuração do bspwm (adapte-o ao seu próprio emulador de terminal):

```
bspc rule -a scratchpad sticky=on state=floating hidden=on
st -c scratchpad -e ~/bin/scratch &

```

Esse sticky flag garante que a janela esteja sempre presente na área de trabalho atual. E `~/bin/scratch` é:

```
#!/usr/bin/sh
bspc query -N -n .floating > /tmp/scratchid
$SHELL

```

A tecla de atalho para alternar o scratchpad deve estar vinculada a:

```
id=$(cat /tmp/scratchid);\
bspc node $id --flag hidden;bspc node -f $id

```

Para um scratchpad que possa usar qualquer tipo de janela sem regras predefinidas, consulte [[1]](https://www.reddit.com/r/bspwm/comments/3xnwdf/i3_like_scratch_for_any_window_possible/cy6i585)

Para um script de rascunho mais sofisticado que suporte muitos terminais prontos para usar e tenha flags para fazer coisas como iniciar opcionalmente uma sessão tmuxinator / tmux, transformar qualquer janela em um scratchpad imediatamente e redimensionar automaticamente um scratchpad para ajustar-se ao monitor atual, instale [tdrop-git](https://aur.archlinux.org/packages/tdrop-git/).

### Configurações diferentes de monitores para diferentes máquinas

Visto que `bspwmrc` seja um shell script, este permite que se faça coisas semelhantes a essa:

```
#! /bin/sh

 if [[ $(hostname) == 'myhost' ]]; then
     bspc monitor eDP1 -d I II III IV V VI VII VIII IX X
 elif [[ $(hostname) == 'otherhost' ]]; then
     bspc monitor VGA-0 -d I II III IV V
     bspc monitor VGA-1 -d VI VII VIII IX X
 elif [[ $(hostname) == 'yetanotherhost' ]]; then
     bspc monitor DVI-I-3 -d VI VII VIII IX X
     bspc monitor DVI-I-2 -d I II III IV V
 fi

```

### Configurar um desktop onde todas as janelas estão flutuando

Aqui está como configurar a área de trabalho 3 para ter apenas janelas flutuantes. Pode ser útil para o Gimp ou outros aplicativos com várias janelas.

```
#!/bin/bash

 # change the desktop number here
 FLOATING_DESKTOP_ID=$(bspc query -D -d '^3')

 bspc subscribe node_manage | while read -a msg ; do
    desk_id=${msg[2]}
    wid=${msg[3]}
    [ "$FLOATING_DESKTOP_ID" = "$desk_id" ] && bspc node "$wid" -t floating
 done

```

Coloque este script em algum lugar em seu $ PATH e chame-o no arquivo .xinitrc ou similar (com um & no final):([source](https://github.com/baskerville/bspwm/issues/428#issuecomment-199985423))

## Solução de problemas

### Tela em branco e atalhos de teclado não funcionam

*   Certifique-se de estar inicinando o sxhkd em segundo plano no arquivo `~/.xinitrc` ou outro.
*   Confira se o arquivo `~/.config/bspwm/bspwmrc` está executável.

### Caixa de janela maior que a aplicação real

Isso pode acontecer se você estiver usando aplicativos GTK3 e, geralmente, para janelas de diálogo. A correção é criar ou adicionar o seguinte a um arquivo de tema gtk3 (`~/.config/gtk-3.0/gtk.css`):

```
.window-frame, .window-frame:backdrop {
  box-shadow: 0 0 0 black;
  border-style: none;
  margin: 0;
  border-radius: 0;
}

.titlebar {
  border-radius: 0;
}

```

(source: [Bspwm forum thread](https://bbs.archlinux.org/viewtopic.php?pid=1404973#p1404973))

### Problemas com aplicações java

Se você tiver problemas com o aplicações Java, tal como a janela não está redimensionando ou os menus fecham imediatamente após o clique, consulte [Java (Português)#Aplicações sem redimensionamento com o WM, menus fechando imediatamente](/index.php/Java_(Portugu%C3%AAs)#Aplica.C3.A7.C3.B5es_sem_redimensionamento_com_o_WM.2C_menus_fechando_imediatamente "Java (Português)").

### Problemas com atalhos de teclado usando fish

Se Você usa [fish](/index.php/Fish "Fish"), descobrirá que não é possível alternar as áreas de trabalho. Isso ocorre porque o uso do caractere ^ pelo bspc é incompatível com o fish. Você pode consertar isso explicitamente dizendo ao sxhkd para usar o bash para executar comandos:

```
$ set -U SXHKD_SHELL /usr/bin/bash

```

Alternativamente, o caractere ^ pode ser escapado com uma barra invertida no seu arquivo sxhkdrc.

### Mensagens de erro "Não foi possível pegar a chave 43 com modfield 68" no início

Se já tentou usar a mesma chave por duas vezes ou também o sxhkd. Verifique o bspwmrc, `~/.profile` ou `~/.bash_profile` e certifique-se que o sxhkd não está sendo iniciado mais de uma vez.

## Veja também

*   Mailing List: bspwm *at* librelist.com.
*   `#bspwm` - IRC channel at irc.freenode.net
*   [https://bbs.archlinux.org/viewtopic.php?id=149444](https://bbs.archlinux.org/viewtopic.php?id=149444) - Arch BBS thread
*   [https://github.com/baskerville/bspwm](https://github.com/baskerville/bspwm) - GitHub project
*   [https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies](https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies) - earsplit's "bspwm for dummies"