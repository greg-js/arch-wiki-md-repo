**Status de tradução:** Esse artigo é uma tradução de [Accessibility](/index.php/Accessibility "Accessibility"). Data da última tradução: 2019-07-30\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Accessibility&diff=0&oldid=578378) na versão em inglês.

Artigos relacionados

*   [TalkingArch](/index.php/TalkingArch_(Portugu%C3%AAs) "TalkingArch (Português)")

Existem muitos métodos diferentes de fornecer acessibilidade a usuários com deficiência física ou visual. No entanto, a menos que um [ambiente de desktop](/index.php/Ambiente_de_desktop "Ambiente de desktop") seja usado, a configuração pode exigir alguns ajustes até que fique certo.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Ambiente de desktop](#Ambiente_de_desktop)
*   [2 Independente a ambientes desktop específicos](#Independente_a_ambientes_desktop_específicos)
    *   [2.1 Operando o teclado](#Operando_o_teclado)
        *   [2.1.1 Teclas de aderência com systemd](#Teclas_de_aderência_com_systemd)
        *   [2.1.2 Teclas de aderência com xserverrc](#Teclas_de_aderência_com_xserverrc)
    *   [2.2 Operando o mouse](#Operando_o_mouse)
        *   [2.2.1 Mapeamento de botão](#Mapeamento_de_botão)
        *   [2.2.2 Teclas de mouse](#Teclas_de_mouse)
    *   [2.3 Assistência visual](#Assistência_visual)
        *   [2.3.1 Reconhecimento de voz](#Reconhecimento_de_voz)
        *   [2.3.2 Emuladores de terminal virtual e consoles](#Emuladores_de_terminal_virtual_e_consoles)
*   [3 Problemas conhecidos](#Problemas_conhecidos)
*   [4 Veja também](#Veja_também)

## Ambiente de desktop

A maioria dos ambientes de desktop modernos é fornecida com um amplo conjunto de recursos, entre os quais se pode encontrar uma ferramenta para configurar as opções de acessibilidade. Geralmente, essas opções podem ser encontradas listadas sob as de "acessibilidade" ou sob as do dispositivo de entrada correspondente (por exemplo, "teclado" e "mouse"). Por exemplo, com [GNOME](https://help.gnome.org/users/gnome-help/stable/a11y.html.pt_BR) e [KDE](https://userbase.kde.org/Applications/Accessibility/pt-br).

**Nota:** Ao usar as ferramentas de configuração de um ambiente de desktop, esteja ciente de possíveis conflitos com as configurações de ferramentas independentes do ambiente de desktop.

## Independente a ambientes desktop específicos

O servidor [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") possui recursos (accessx) para assistência física, configurando parâmetros via [X keyboard extension](/index.php/X_keyboard_extension "X keyboard extension"). Esta seção cobre exemplos.

Para reconhecimento de fala, consulte também [Texto para fala](/index.php/Text_to_speech "Text to speech").

### Operando o teclado

Para Braille, veja [Arch Linux para os cegos](/index.php/Arch_Linux_para_os_cegos "Arch Linux para os cegos").

#### Teclas de aderência com systemd

Para habilitar as teclas de aderência em um TTY, você precisa saber os códigos exatos das teclas a serem usadas. Eles podem ser encontrados por uma ferramenta como [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev) ou [xkeycaps](https://www.archlinux.org/packages/?name=xkeycaps). Como alternativa, você pode inspecionar a saída de *dumpkeys*, desde que o mapa de teclado atual esteja correto.

Por exemplo, um Logitech Ultra-X fornecerá os seguintes códigos de teclas para as teclas modificadoras:

```
LCtrl = 29
LShift = 42
LAlt = 56
RShift = 54
RCtrl = 97

```

Em seguida, use *dumpkeys* para determinar o intervalo dos códigos de teclas:

```
# dumpkeys | head -1
keymaps 0-63

```

Continue criando um novo arquivo com um nome adequado, por exemplo "teclasDeAderência", e use seu editor favorito para combinar as informações encontradas anteriormente com a função de tecla desejada.

No caso dos códigos de teclas encontrados anteriormente, você obteria:

```
keymaps 0-63
keycode 29 = SCtrl
keycode 42 = SShift
keycode 56 = SAlt
keycode 54 = SShift
keycode 97 = SCtrl

```

Aqui, a letra "S" na frente de uma tecla modificadora indica que queremos a versão de aderência desta tecla.

**Nota:** A etapa a seguir mudará seu mapeamento de chave em todos os TTYs. Garanta a correção dos seus códigos de teclas ou você poderá perder a capacidade de usar certas chaves importantes.

Carregue seu novo mapeamento executando o seguinte comando:

```
# loadkeys ./teclasDeAderência

```

Se você estiver satisfeito com os resultados, mova o arquivo para um diretório adequado. Para ter isso [habilitado](/index.php/Habilita "Habilita") seja inicializado, veja a seguinte unit systemd:

 `/etc/systemd/system/loadkeys.service` 
```
[Unit]
Description="Carrega mapeamento de teclas personalizado (teclas de aderência)"

[Service]
Type=oneshot
ExecStart=/usr/bin/loadkeys /caminho/para/teclasDeAderência
StandardInput=tty
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target emergency.target rescue.target
```

#### Teclas de aderência com xserverrc

Um método para habilitar a função de acessibilidade independente de ambiente de desktop é passá-lo pelo X, já que ele é construído com suporte a XKB. Isso pode ser feito definindo parâmetros para o servidor X, conforme especificado em sua página man:

```
[+-]accessx [ timeout [ timeout_mask [ feedback [ options_mask ] ] ] ]
              enables(+) or disables(-) AccessX key sequences (Sticky Keys).

-ardelay milliseconds
              sets the autorepeat delay (length of time in milliseconds  that
              a key must be depressed before autorepeat starts).

-arinterval milliseconds
              sets  the  autorepeat  interval (length of time in milliseconds
              that should elapse between autorepeat-generated keystrokes).

```

Estes parâmetros devem ser colocados no arquivo `~/.xserverrc`, que você pode precisar criar.

Por exemplo, para ativar as teclas de aderência sem tempo limite e sem feedback audível ou visível, é possível usar o seguinte:

```
if [ -z "$XDG_VTNR" ]; then
  exec /usr/bin/X -nolisten tcp "$@" +accessx 0 0x1e 0 0xcef
else
  exec /usr/bin/X -nolisten tcp "$@" vt$XDG_VTNR +accessx 0 0x1e 0 0xcef
fi

```

Note que uma vez que o X tenha iniciado, por ex. Ao executar `startx`, ainda é necessário pressionar a tecla Shift 5 vezes para ativar as teclas de aderência. Infelizmente, isso é necessário toda vez que o X inicia. Como alternativa, um script pode ser usado para automatizar esse processo.

Semelhante à maioria das implementações, as teclas de aderência podem ser desativadas pressionando uma tecla modificadora e qualquer outra tecla ao mesmo tempo.

### Operando o mouse

#### Mapeamento de botão

Usando o *xmodmap*, você pode mapear funções para botões do mouse, independentemente do seu ambiente gráfico. Para isso, você precisa saber qual botão físico do mouse é lido como o número, que pode ser encontrado por uma ferramenta como [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev). Geralmente, os botões físicos da esquerda, do meio e da direita são lidos como o primeiro, o segundo e o terceiro botão, respectivamente.

Depois de adquiri-los, continue criando um arquivo de configuração em um local adequado, por exemplo, `~/.mouseconfig`. Em seguida, abra o arquivo com seu editor favorito e escreva a palavra-chave `pointer=` seguida de uma enumeração do número de botões do mouse encontrado anteriormente.

Por exemplo, um mouse de três botões com uma roda de rolagem é capaz de fornecer cinco ações físicas: esquerda, central e direita, bem como rolar para cima e rolar para baixo. Isso pode ser mapeado para as mesmas funções usando a seguinte linha no arquivo de configuração:

```
pointer = 1 2 3 4 5

```

Aqui, o local informará a ação necessária para executar uma função interna do botão do mouse. Por exemplo, um mapeamento para pessoas canhotas (botão esquerdo e direito comutado) pode parecer

```
pointer = 3 2 1 4 5

```

Quando terminar, você poderá testar e inspecionar seu mapeamento executando `xmodmap`:

```
$ xmodmap ~/.mouseconfig
$ xmodmap -pp

```

Uma vez satisfeito, você pode ativá-lo no começo colocando a primeira linha em `~/.xinitrc`.

#### Teclas de mouse

[Teclas de mouse](https://en.wikipedia.org/wiki/Mouse_keys "wikipedia:Mouse keys") (em inglês, *mouse keys*) é um recurso do Xorg (como teclas de aderência) para usar o teclado (especialmente um teclado numérico) como um dispositivo apontador. Pode substituir um mouse ou trabalhar ao lado dele. É desativado por padrão. Você pode usar

```
$ xset q | grep "Mouse Keys"

```

para ver o estado. Para ativá-lo para uma sessão:

```
$ setxkbmap -option keypad:pointerkeys

```

Se você usa uma configuração com [xmodmap](/index.php/Xmodmap "Xmodmap"), esteja ciente que *setxkbmap* o redefine.

**Dica:** Alguns layouts de teclado de terceiros, por exemplo, o [layout Neo alemão](https://wiki.neo-layout.org), podem usar maneiras diferentes de ativar as teclas de mouse.

Para ativar as teclas de mouse permanentemente, adicione

```
Option "XkbOptions" "keypad:pointerkeys" 

```

Para o arquivo de configuração do teclado. Isso fará o atalhos `Shift+NumLock` ativar ou desativar teclas de mouse.

Para mais, veja [Keyboard configuration in Xorg#Using X configuration files](/index.php/Keyboard_configuration_in_Xorg#Using_X_configuration_files "Keyboard configuration in Xorg") e [X keyboard extension#Mouse control](/index.php/X_keyboard_extension#Mouse_control "X keyboard extension") para configuração avançada.

### Assistência visual

Como tal, a maioria dos ambientes de desktop modernos é fornecida com um amplo conjunto de recursos para ajustar os aspectos visuais de seu sistema. Geralmente, essas opções são listadas sob as de "acessibilidade" ou "assistência visual". Como alternativa, opções úteis podem ser encontradas nas configurações dos aplicativos individuais.

#### Reconhecimento de voz

Veja [Speech recognition](/index.php/Speech_recognition "Speech recognition").

#### Emuladores de terminal virtual e consoles

*   Edite `/etc/vconsole.conf`.
*   Edite `~/.Xresources`.

## Problemas conhecidos

*   A configuração de dispositivos de entrada não é reconhecida por softwares que contornam a camada de software, por exemplo, [wine](/index.php/Wine "Wine"), [VirtualBox](/index.php/VirtualBox_(Portugu%C3%AAs) "VirtualBox (Português)") e [QEMU](/index.php/QEMU "QEMU").

## Veja também

*   Aplicativos de acessibilidade avançada do [KDE](https://userbase.kde.org/Applications/Accessibility).