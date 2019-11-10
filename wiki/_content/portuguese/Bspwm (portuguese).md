**Status de tradução:** Esse artigo é uma tradução de [bspwm](/index.php/Bspwm "Bspwm"). Data da última tradução: 2019-11-06\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Bspwm&diff=0&oldid=587896) na versão em inglês.

Related articles

*   [Gerenciador de janela](/index.php/Gerenciador_de_janela "Gerenciador de janela")
*   [Comparação de gerenciadores de janela tiling](/index.php/Compara%C3%A7%C3%A3o_de_gerenciadores_de_janela_tiling "Comparação de gerenciadores de janela tiling")

[bspwm](https://github.com/baskerville/bspwm) é um gerenciador de janelas leve, lado a lado, e minimalista escrito em C que organiza janelas em árvore binária completa. O bspwm tem suporte a vérios monitores e é configurado e controlado por meio de mensagens. Há suporte parcial a [EWMH](https://standards.freedesktop.org/wm-spec/wm-spec-latest.html).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Iniciando](#Iniciando)
*   [3 Configuração](#Configuração)
    *   [3.1 Nota para múltiplos monitores](#Nota_para_múltiplos_monitores)
    *   [3.2 Regras](#Regras)
    *   [3.3 Painéis](#Painéis)
        *   [3.3.1 Usando lemonbar](#Usando_lemonbar)
        *   [3.3.2 Usando yabar](#Usando_yabar)
        *   [3.3.3 Usando polybar](#Usando_polybar)
    *   [3.4 Scratchpad](#Scratchpad)
    *   [3.5 Configurações diferentes de monitores para diferentes máquinas](#Configurações_diferentes_de_monitores_para_diferentes_máquinas)
    *   [3.6 Configurar um desktop onde todas as janelas estão flutuando](#Configurar_um_desktop_onde_todas_as_janelas_estão_flutuando)
    *   [3.7 Teclado](#Teclado)
*   [4 Solução de problemas](#Solução_de_problemas)
    *   [4.1 Tela em branco e atalhos de teclado não funcionam](#Tela_em_branco_e_atalhos_de_teclado_não_funcionam)
    *   [4.2 Temas de cursor funcionam no desktop](#Temas_de_cursor_funcionam_no_desktop)
    *   [4.3 Caixa de janela maior que o aplicativo](#Caixa_de_janela_maior_que_o_aplicativo)
    *   [4.4 Problemas com aplicativos java](#Problemas_com_aplicativos_java)
    *   [4.5 Problemas com atalhos de teclado usando fish](#Problemas_com_atalhos_de_teclado_usando_fish)
    *   [4.6 Mensagens de erro "Não foi possível pegar a chave 43 com modfield 68" no início](#Mensagens_de_erro_"Não_foi_possível_pegar_a_chave_43_com_modfield_68"_no_início)
    *   [4.7 Menu de contexto do Firefox seleciona automaticamente a primeira opção no clique de botão direito](#Menu_de_contexto_do_Firefox_seleciona_automaticamente_a_primeira_opção_no_clique_de_botão_direito)
*   [5 Veja também](#Veja_também)

## Instalação

[Instale](/index.php/Instale "Instale") [bspwm](https://www.archlinux.org/packages/?name=bspwm), ou [bspwm-git](https://aur.archlinux.org/packages/bspwm-git/) versão de desenvolvimento.

## Iniciando

Execute `bspwm` usando [xinit](/index.php/Xinit_(Portugu%C3%AAs) "Xinit (Português)").

## Configuração

**Importante:** Certifique-se de que sua variável de ambiente $XDG_CONFIG_HOME esteja configurada ou seu bspwmrc não será encontrado. Isso pode ser feito digitando `XDG_CONFIG_HOME="$HOME/.config"` e `export XDG_CONFIG_HOME` para `~/.profile`.

Exemplos de configuração podem ser encontrados em `/usr/share/doc/bspwm/examples/`.

Copie `bspwmrc` de lá para `~/.config/bspwm/` e `sxhkdrc` para `~/.config/sxhkd/`.

Esses dois arquivos são onde você vai definir as configurações e associações de teclas do wm, respectivamente.

Veja os manuais [bspwm(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/bspwm.1) e [sxhkd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sxhkd.1) para a documentação detalhada.

#### Nota para múltiplos monitores

O exemplo do bspwmrc configura dez áreas de trabalho para um só monitor:

```
bspc monitor -d I II III IV V VI VII VIII IX X

```

Você vai precisar alterar essa linha ou adicionar um para cada monitor, similar a isso:

```
bspc monitor DVI-I-1 -d I II III IV
bspc monitor DVI-I-2 -d V VI VII
bspc monitor DP-1 -d VIII IX X

```

Você pode usar `xrandr -q` ou `bspc query -M` para saber os nomes dos monitores.

O número total de áreas de trabalho foi mantido em dez no exemplo acima. Isso é para que cada área de trabalho ainda possa ser endereçada com `super + {1-9,0}` no sxhkdrc.

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

Se uma determinada janela não estiver se comportando de acordo com suas regras, verifique o nome da classe do programa. Isso pode ser feito executando `xprop | grep WM_CLASS` para ter certeza de que você está usando a string apropriada, o que requer o pacote [xorg-xprop](https://www.archlinux.org/packages/?name=xorg-xprop).

### Painéis

#### Usando lemonbar

Um exemplo de painel para [lemonbar-git](https://aur.archlinux.org/packages/lemonbar-git/) é fornecido na página de exemplos no GitHub. Você também pode encontrar mais exemplos na página wiki [lemonbar](/index.php/Lemonbar "Lemonbar"). O painel será executado adicionando `panel &` na sua bspwmrc. Verifique os [optdepends](/index.php/Optdepends "Optdepends") no pacote [bspwm](https://www.archlinux.org/packages/?name=bspwm) por dependências que pode, ser necessárias.

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

Em seguida, é só verificar se já está invocado e redirecionado para `$PANEL_FIFO`:

```
while true; do
echo "S" "$(panel_volume) $(panel_clock)" > "$PANEL_FIFO"
        sleep 1s
done &

```

#### Usando yabar

O uso do painel de exemplo usando lemonbar requer que você defina seu ambiente (.profile) e verifique se os scripts do painel estão no seu caminho. O painel mais fácil de configurar é o [yabar](https://aur.archlinux.org/packages/yabar/), que possui apenas um arquivo de configuração.

#### Usando polybar

[Polybar](/index.php/Polybar "Polybar") pode ser usada adicionando `polybar *exemplo* &` ao seu arquivo de configuração bspwmrc, sendo `*example*` o nome da barra.

### Scratchpad

Voce pode emular um terminal suspenso (como o recurso de rascunho do i3 se voce colocar um terminal nele) usando as flags da janela do bspwm. Anexe o seguinte ao final do arquivo de configuração do bspwm (adapte-o ao seu próprio emulador de terminal):

```
bspc rule -a scratchpad sticky=on state=floating hidden=on
st -c scratchpad -e ~/bin/scratch &

```

Essa opção `sticky` garante que a janela esteja sempre presente na área de trabalho atual. E `~/bin/scratch` é:

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

Para um script de scratchpad mais sofisticado que tenha suporte a muitos terminais prontos para usar e tenha opções para fazer coisas como iniciar opcionalmente uma sessão tmuxinator/tmux, transformar qualquer janela em um scratchpad imediatamente e redimensionar automaticamente um scratchpad para ajustar-se ao monitor atual, instale [tdrop-git](https://aur.archlinux.org/packages/tdrop-git/).

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

Coloque este script em algum lugar em seu `$PATH` e chame-o no arquivo `.xinitrc` ou similar (com um & no final):

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

([fonte](https://github.com/baskerville/bspwm/issues/428#issuecomment-199985423))

### Teclado

Bspwm não lida com qualquer entrada de teclado e, em vez disso, fornece o programa *bspc* como sua interface.

Para atalhos de teclado, você terá que configurar um serviço de hotkey como [sxhkd](https://www.archlinux.org/packages/?name=sxhkd) ([sxhkd-git](https://aur.archlinux.org/packages/sxhkd-git/) para a versão de desenvolvimento).

## Solução de problemas

### Tela em branco e atalhos de teclado não funcionam

*   Certifique-se de estar iniciando o sxhkd (em segundo plano, pois bloquear o console).
*   Certifique-se de que `~/.config/bspwm/bspwmrc` está executável.

### Temas de cursor funcionam no desktop

Veja [Temas de cursor#Mude o cursor padrão com forma de X](/index.php/Temas_de_cursor#Mude_o_cursor_padrão_com_forma_de_X "Temas de cursor")

### Caixa de janela maior que o aplicativo

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

(fonte: [Tópico sobre Bspwm no fórum](https://bbs.archlinux.org/viewtopic.php?pid=1404973#p1404973))

### Problemas com aplicativos java

Se você tiver problemas com o aplicações Java, tal como a janela não está redimensionando ou os menus fecham imediatamente após o clique, consulte [Java (Português)#Janela cinza, aplicações sem redimensionamento com o WM, menus fechando imediatamente](/index.php/Java_(Portugu%C3%AAs)#Janela_cinza,_aplicações_sem_redimensionamento_com_o_WM,_menus_fechando_imediatamente "Java (Português)").

### Problemas com atalhos de teclado usando fish

Se Você usa [fish](/index.php/Fish "Fish"), descobrirá que não é possível alternar as áreas de trabalho. Isso ocorre porque o uso do caractere ^ pelo bspc é incompatível com o fish. Você pode consertar isso explicitamente dizendo ao sxhkd para usar o bash para executar comandos:

```
$ set -U SXHKD_SHELL /usr/bin/bash

```

Alternativamente, o caractere ^ pode ser escapado com uma barra invertida no seu arquivo sxhkdrc.

### Mensagens de erro "Não foi possível pegar a chave 43 com modfield 68" no início

Se já tentou usar a mesma chave por duas vezes ou também o sxhkd. Verifique o bspwmrc, `~/.profile` ou `~/.bash_profile` e certifique-se que o sxhkd não está sendo iniciado mais de uma vez.

### Menu de contexto do Firefox seleciona automaticamente a primeira opção no clique de botão direito

Adicione a seguinte linha ao arquivo `userChrome.css` do perfil do Firefox:

```
#contentAreaContextMenu{ margin: 5px 0 0 5px }

```

O arquivo deve estar localizado em `~/.mozilla/firefox/*alguma-coisa*.default/chrome/` (ele precisará ser criado se você ainda não tiver um). Além disso, no Firefox, você terá que acessar a página `about:config` e ativar a opção `toolkit.legacyUserProfileCustomizations.stylesheets`; caso contrário, o Firefox ignorará o arquivo userChrome.css.

## Veja também

*   Lista de discussão: bspwm *at* librelist.com.
*   `#bspwm` - Canal IRC no irc.freenode.net
*   [https://bbs.archlinux.org/viewtopic.php?id=149444](https://bbs.archlinux.org/viewtopic.php?id=149444) - Tópico no fórum do Arch
*   [https://github.com/baskerville/bspwm](https://github.com/baskerville/bspwm) - no Projeto GitHub
*   [https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies](https://github.com/windelicato/dotfiles/wiki/bspwm-for-dummies) - earsplit's "bspwm for dummies"