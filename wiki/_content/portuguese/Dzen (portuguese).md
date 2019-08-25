[Dzen](http://robm.github.com/dzen/) é "um programa de propósito geral para notificações, menus e barras para o X11\. Ele foi feito para ser rápido, leve e programável em qualquer linguagem de programação e se integra bem com gerenciadores de janela como [dwm](/index.php/Dwm "Dwm"), [wmii](/index.php/Wmii "Wmii") e [xmonad](/index.php/Xmonad "Xmonad") apesar de que vai funcionar com qualquer gerenciador de janela."

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Uso](#Uso)
    *   [2.1 Opções](#Opções)
    *   [2.2 Criando um pop-up com dzen](#Criando_um_pop-up_com_dzen)
    *   [2.3 Fonte](#Fonte)
    *   [2.4 Eventos e Ações](#Eventos_e_Ações)
        *   [2.4.1 Sintaxe](#Sintaxe)
        *   [2.4.2 Exemplos](#Exemplos)
    *   [2.5 Formatação](#Formatação)
        *   [2.5.1 Cores](#Cores)
        *   [2.5.2 Gráfico](#Gráfico)
        *   [2.5.3 Posicionamento](#Posicionamento)
        *   [2.5.4 Interação](#Interação)
        *   [2.5.5 Exemplos](#Exemplos_2)
*   [3 Configuração](#Configuração)
*   [4 Dicas e truques](#Dicas_e_truques)
    *   [4.1 Dzen e Conky](#Dzen_e_Conky)
    *   [4.2 Gadgets](#Gadgets)
        *   [4.2.1 dbar](#dbar)
        *   [4.2.2 gdbar](#gdbar)
        *   [4.2.3 Outros](#Outros)
*   [5 Veja também](#Veja_também)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [dzen2](https://www.archlinux.org/packages/?name=dzen2) que inclui suporte a Xft, Xpm e Xinerama.

## Uso

O dzen recebe uma string por [pipe](https://en.wikipedia.org/wiki/pt:Encadeamento_(Unix) e imprime ela graficamente, esse fato faz com que o dzen seja programável em qualquer linguagem, pois você só precisa passar uma string para ele.

Exemplo:

```
$ echo "Olá Mundo" | dzen2 -p

```

### Opções

O dzen conta com varias opções para diversas finalidades, são elas:

*   `-fg` Cor de foreground.
*   `-bg` Cor de background.
*   `-fn` Fonte.
*   `-ta` Alinhar o conteúdo da "title window", **l**(eft), **c**(enter), **r**(ight).
*   `-tw` Largura da "title window".
*   `-sa` Alinhar o conteúdo da "slave window", Veja `-ta`.
*   `-l` Linhas das "slave window".
*   `-e` Eventos e ações.
*   `-m` Modo menu.
*   `-u` Atualiza o conteúdo do "title" e "slave" simultaneamante.
*   `-p` Persistente EOF (timeout opcional em segundos).
*   `-x` Posição X.
*   `-y` Posição Y.
*   `-h` Altura de linha (padrão: fontheight + 2 pixels).
*   `-w` Largura do janela.
*   `-v` Infomação da versão.

**Atenção:** Opção *-u* está descontinuada.

### Criando um pop-up com dzen

O seguinte código irá abrir uma janela do dzen no canto superior esquerdo da sua tela com uma largura de 100 pixels, uma altura de linha de 15 pixels, foreground preto e background branco (para fechar o dzen clique nele com o botão direito).

```
$ seq 1 3 | dzen2 -p -w '100' -h '15' -fg '#000000' -bg '#FFFFFF'

```

Veja que a janela está com o número *3* centralizado, agora tente adicionar a opção `-l` nele.

```
$ seq 1 3 | dzen2 -p -w '100' -h '15' -fg '#000000' -bg '#FFFFFF' -l '2'

```

Agora quando você passar o mouse por cima da janela ela irá abrir outra janela abaixo, parecida com um menu, mas diferente de um menu quando você clicar nada irá acontecer, para isso existe a opção `-m`.

```
$ seq 1 3 | dzen2 -p -w '100' -h '15' -fg '#000000' -bg '#FFFFFF' -l '2' -m

```

Agora quando você clicar nos itens do "menu" o dzen irá imprimir esses números no seu terminal. Essa opção é útil para fazer menus que abrem determinados programas com um click.

Mas digamos que você queira centralizar os números e colocar o título para o lado esquerdo, você usará as opções de alinhamento: `-ta`, `-sa`.

```
$ seq 1 3 | dzen2 -p -w '100' -h '15' -fg '#000000' -bg '#FFFFFF' -l '2' -m -ta 'l' -sa 'c'

```

Esse é o funcionamento das opções básico do dzen.

### Fonte

O [dzen2](https://www.archlinux.org/packages/?name=dzen2) aceita dois tipos descrição de fonte, são eles: [XLFD](/index.php/X_Logical_Font_Description "X Logical Font Description") e [Xft](/index.php/Font_configuration "Font configuration"). Elas são setadas da seguinte forma no dzen.

X Logical Font Description:

```
$ uname -r | dzen2 -p -fn '-*-fixed-*-*-*-*-*-*-*-*-*-*-*-*'

```

Xft

```
$ uname -r | dzen2 -p -fn 'Sans:size=10'

```

Veja o [manual do fonts-conf](https://www.freedesktop.org/software/fontconfig/fontconfig-user.html) para detalhes de como setar fontes com [fontconfig](https://www.archlinux.org/packages/?name=fontconfig).

### Eventos e Ações

O Dzen permite você associar ações a eventos por meio da opção `-e`. Abaixo uma lista das principais ações e eventos do dzen.

| Evento | Função |
| onstart | Executa uma ação logo após o inicio do dzen. |
| onexit | Executa uma ação antes de fechar o dzen. |
| button{1..7} | Executa ações com cliques dos botões do mouse. |
| entertitle | Executa uma ação ao entrar na "title window". |
| leavetitle | Executa uma ação ao sair da "title window". |
| enterslave | Executa uma ação ao entrar na "slave window". |
| leaveslave | Executa uma ação ao sair da "slave window". |

| Ação | Função |
| exec:comando1:..:n | Executa todas opções passados. |
| exit:retval | Fecha o dzen e retorna "retval" (status de saída). |
| print:str1:..:n | Imprime todas opções para o STDOUT. |
| collapse | Fecha a "slave window". |
| uncollapse | Abre a "slave window". |
| hide | Esconde a "title window". |
| unhide | Mostra a "title window". |

Para uma lista completa de eventos e ações veja [Dzen Wiki#Events and Actions](https://github.com/robm/dzen/wiki/Events-and-actions).

**Nota:** Se `-e` não for setado o dzen usará a seguinte string de eventos:
```
-e 'entertitle=uncollapse,grabkeys;
    enterslave=grabkeys;
    leaveslave=collapse,ungrabkeys;
    button1=menuexec;
    button2=togglestick;
    button3=exit:13;
    button4=scrollup;
    button5=scrolldown;
    key_Escape=ungrabkeys,exit'
```

#### Sintaxe

A opção `-e` do dzen usa a seguinte sintaxe para a associação de eventos:

```
-e 'button1=exec:xterm:firefox;entertitle=uncollapse,unhide;button3=exit'

```

`button1=exec:xterm:firefox;`

	No evento `button1` (clique do botão esquerdo mouse) o dzen irá executar o xterm e firefox. Note que xterm e firefox são opções da ação *exec*.

`entertitle=uncollapse,unhide;`

	No evento `entertitle` (quando o mouse entra na "title window") o dzen irá "uncollapse" a "slave window" e "unhide" a "title window". Veja [Criando um pop-up com dzen](#Criando_um_pop-up_com_dzen).

`button3=exit`

	No evento `button3` (clique do botão direto do mouse) o dzen irá simplesmente fechar.

#### Exemplos

Abaixo alguns exemplos de uso para os eventos e funções.

Exemplo 1:

```
$ echo "Menu 
 Item1 
 Item2 
 Item3" | dzen2 -p -l '3' -w '100' -h '30' -m -e 'button1=uncollapse,menuexec;leaveslave=collapse;button3=exit:0'

```

Exemplo 2:

 `~/volume.sh` 
```
#!/bin/sh

function get_vol() {
        amixer get Master | awk '/Left:/{gsub(/[[:punct:]]/,"");print $5}'
}

while :; do
        get_vol | gdbar -s 'v' -h '150' -sw '10'
        sleep 1
done | dzen2 -p -w '50' -h '200' -e 'button4=exec:amixer set Master 5%+;button5=exec:amixer set Master 5%-;button3=exit:0'

```

### Formatação

O Dzen tem uma formatação especial para sua string. Isso é usado para fazer botões, mudar o background ou foreground de partes especificas da string etc. Essa formatação é feita da seguinte maneira:

```
^bg(#00FF00) Olá ^bg() ^fg(#00FF00) Mundo ^fg().

```

Lista dos principais padrões de formatação do Dzen. Para uma lista completa veja o [README.dzen](https://github.com/robm/dzen).

#### Cores

	`^fg(cor)`

	Seta o foreground.

	`^fg()`

	Sem argumento, seta o foreground padrão.

	`^bg(cor)`

	Seta o background.

	`^bg()`

	Sem argumento, seta o background padrão.

#### Gráfico

	`^i(path)`

	Seta um icon especificado pelo path. Formatos suportados: XBM e XPM.

	`^r(LARGURAxALTURA)`

	Desenha um retângulo com as dimensões especificadas.

	`^ro(LARGURAxALTURA)`

	Desenha um contorno de retângulo.

	`^c(RAIO)`

	Desenha um círculo com o raio especificado.

	`^co(RAIO)`

	Desenha um contorno de círculo.

#### Posicionamento

	`^p(+-X)`

	Move X pixels para direita (+) ou esquerda (-) no eixo X.

	`^p(;+-Y)`

	Move Y pixels para cima (-) ou para baixo (+) no eixo Y.

	`^p(+-X;+-Y)`

	Move X pixels e Y pixels nos eixos X e Y.

	`^pa()`

	Faz o mesmo que as opções anteriores, mas usando posição absoluta.

#### Interação

	`^ca(BOT, CMD) ... ^ca()` Cria áreas clicáveis.

	`BOT`

	Será o botão do mouse (1=esquerdo, 2=direito, 3=scroll (clique), 4=scrollup, 5=scrolldown, etc.).

	`CMD`

	Será o comando que irá ser executado quando essa área for clicada.

	`...`

	Será o texto que aparecerá no dzen.

	`^ca()`

	Sem argumentos, indica o fim da área clicável.

#### Exemplos

Exemplo 1:

 `~/degrade.sh` 
```
#!/bin/sh

for x in {0..9} {a..f}; do
        for y in {0..9} {a..f}; do
                color+="^bg(#FF${x}${y}00) "
        done
done

echo ${color} | dzen2 -p -h '30'

```

Exemplo 2 (Olho):

```
$ echo "^ib(1)^c(50)^fg(black)^p(-28)^c(25)^fg()^c(50)^fg(black)^p(-28)^c(25)" | dzen2 -p -h '100' -w '300' -fg '#FFFFFF'

```

## Configuração

O Dzen consegue ler as configurações de fonte e cor do [X resources](/index.php/X_resources "X resources"). Por exemplo, você pode adicionar as seguintes linhas no seu `~/.Xresources`

```
dzen2.font: Sans:size=10
dzen2.foreground: #FFFFFF
dzen2.background: black

```

## Dicas e truques

### Dzen e Conky

O [Conky](/index.php/Conky "Conky") pode ser usado para passar a informação para o dzen criar uma barra de "status". Isso pode ser feito tanto com o Conky do repositório oficial quanto com o [conky-cli](https://aur.archlinux.org/packages/conky-cli/), uma versão [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") mais leve do Conky.

O seguinte exemplo mostra o [load average](https://en.wikipedia.org/wiki/pt:Load_average "wikipedia:pt:Load average") em vermelho e a data atual na cor de foreground padrão do dzen.

 `~/.conkyrc` 
```
conky.config = {
      background = false
    , out_to_console = true
    , out_to_x = false
    , update_interval = 1.0
    , total_run_times = 0
    , use_spacer = none
}

conky.text = [[^fg(\#ff0000)${loadavg 1 2 3} ^fg()${time %a %b %d %I:%M%P}]]

```

Criando um script em [shell script](https://en.wikipedia.org/wiki/pt:Shell_script "wikipedia:pt:Shell script") para o dzen.

 `~/dzconky` 
```
 #!/bin/sh

 FG='#aaaaaa'
 BG='#1a1a1a'
 FONT='Sans:size=10'
 conky | dzen2 -p -h '16' -w '600' -ta r -fg $FG -bg $BG -fn $FONT

```

Agora execute o script `~/dzconky`.

### Gadgets

O dzen2 possui alguns gadgets que podem ser usados para fazer uma boa customização. Segue abaixo alguns deles com uma breve explicação e exemplos.

#### dbar

O dbar recebe um [pipe](https://en.wikipedia.org/wiki/pt:Encadeamento_(Unix) de outro comando com um número qualquer e cria uma barra de progresso semi-gráfica com base nesse número, por padrão o valor máximo é *100*. Os valores máximo e mínimo podem ser alterados com as opções *-max*/*-min* repectivamente.

Exemplo de output:

```
50% [=============            ]

```

Exemplo de código:

 `~/teste` 
```
#!/bin/sh

amixer get Master | awk '{gsub(/[[:punct:]]/,"",$5)} /Left:/{left=$5} /Right:/{right=$5} END{print left ORS right}' | dbar -max 100 -min 0 -s '|' -l 'Vol'

```

Veja o [README](https://github.com/robm/dzen/blob/master/gadgets/README.dbar) do dbar para mais detalhes.

#### gdbar

O gdbar, assim como o [dbar](#dbar), cria uma barra de progresso a partir de um [pipe](https://en.wikipedia.org/wiki/pt:Encadeamento_(Unix) "wikipedia:pt:Encadeamento (Unix)"), mas aqui ela é totalmente gráfica. Ele tem as mesmas opções do dbar com algumas opções adicionais. Algumas dessas opções são:

*   *-fg* para foreground
*   *-bg* para background
*   *-w*/*-h* para width e height (altura e largura).

Exemplo de código:

 `~/teste` 
```
#!/bin/sh

(
amixer get Master | awk '{gsub(/[[:punct:]]/,"",$5)}
                          /Left:/{left=$5} /Right:/{right=$5}
                          END{print left ORS right}'
) | gdbar -max 100 -min 0 -l 'Vol ' -bg '#777777' -fg '#00ff00' -ss '2' | dzen2 -p -l '1' -w '150' -y '100' -x '100' -ta c -sa c -e 'onstartup=uncollapse;button3=exit'

```

Veja o [README](https://github.com/robm/dzen/blob/master/gadgets/README.gdbar) do gdbar para mais detalhes.

**Nota:** gdbar só é útil se estiver sendo usando com o dzen >= 0.7.0.

#### Outros

Informação sobre outros gadgets podem ser encontrado [aqui](https://github.com/robm/dzen/tree/master/gadgets).

## Veja também

*   [Site oficial](http://robm.github.com/dzen/)
*   [Dzen Wiki](https://github.com/robm/dzen/wiki/_pages)
*   [Código-fonte](https://github.com/robm/dzen)