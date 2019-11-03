**Status de tradução:** Esse artigo é uma tradução de [Linux console](/index.php/Linux_console "Linux console"). Data da última tradução: 2019-08-17\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Linux_console&diff=0&oldid=579208) na versão em inglês.

Artigos relacionados

*   [/Configuração de teclado](/index.php/Console_do_Linux/Configura%C3%A7%C3%A3o_de_teclado "Console do Linux/Configuração de teclado")
*   [Screen capture#Virtual console](/index.php/Screen_capture#Virtual_console "Screen capture")
*   [Color output in console](/index.php/Color_output_in_console "Color output in console")
*   [getty](/index.php/Getty "Getty")

De acordo com [Wikipédia](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console"):

	O **console Linux** é um console do sistema interno ao [kernel Linux](/index.php/Kernel_Linux_(Portugu%C3%AAs) "Kernel Linux (Português)"). O console Linux fornece uma maneira de o kernel e outros processos enviarem a saída de texto ao usuário e receberem entrada de texto do usuário. O usuário normalmente insere texto com um teclado de computador e lê o texto de saída em um monitor de computador. O kernel Linux tem suporte a consoles virtuais - consoles que são logicamente separados, mas que acessam o mesmo teclado físico e tela.

Este artigo descreve os conceitos básicos do console do Linux e como configurar a exibição da fonte. A configuração do teclado é descrita na subpágina [/Configuração de teclado](/index.php/Console_do_Linux/Configura%C3%A7%C3%A3o_de_teclado "Console do Linux/Configuração de teclado").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Implementação](#Implementação)
    *   [1.1 Consoles virtuais](#Consoles_virtuais)
    *   [1.2 Modo de texto](#Modo_de_texto)
    *   [1.3 Console framebuffer](#Console_framebuffer)
*   [2 Atalhos de teclado](#Atalhos_de_teclado)
*   [3 Fontes](#Fontes)
    *   [3.1 Visualizar alterações e alterações temporárias](#Visualizar_alterações_e_alterações_temporárias)
    *   [3.2 Configuração persistente](#Configuração_persistente)
    *   [3.3 HiDPI](#HiDPI)
*   [4 Veja também](#Veja_também)

## Implementação

O console, diferentemente da maioria dos serviços que interagem diretamente com os usuários, é implementado no kernel. Isso contrasta com o software de emulação de terminal, como o [Xterm](/index.php/Xterm "Xterm"), que é implementado no espaço do usuário como um aplicativo normal. O console sempre fez parte dos kernels Linux lançados, mas sofreu mudanças em sua história, mais notavelmente a transição para o uso do [framebuffer](https://en.wikipedia.org/wiki/pt:Framebuffer_(Linux) e suporte a [Unicode](https://en.wikipedia.org/wiki/pt:Unicode "wikipedia:pt:Unicode").

Apesar de muitos aprimoramentos no console, sua total retrocompatibilidade com o hardware legado significa que ele é limitado em comparação com um emulador de terminal gráfico.

### Consoles virtuais

O console é apresentado ao usuário como uma série de [consoles virtuais](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console"). Estes dão a impressão de que vários terminais independentes estão sendo executados simultaneamente; cada console virtual pode ser conectado com diferentes usuários, executar seu próprio shell e ter suas próprias configurações de fonte. Os consoles virtuais usam um dispositivo `/dev/ttyX`, e você pode alternar entre eles pressionando `Alt+F*x*` (onde `*x*` é igual ao número do console virtual, começando com 1) . O dispositivo `/dev/console` é automaticamente mapeado para o console virtual ativo.

Veja também [chvt(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chvt.1), [openvt(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/openvt.1) e [deallocvt(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/deallocvt.1).

### Modo de texto

Como o Linux começou originalmente como um kernel para hardware de PC, o console foi desenvolvido usando gráficos [CGA/EGA/VGA](https://en.wikipedia.org/wiki/VGA "wikipedia:VGA") padrão da IBM, que todos os PCs suportavam na época. Os gráficos operaram no modo de texto VGA, que fornece um display simples de 80x25 caracteres com 16 cores. Este modo legado é semelhante aos recursos dos terminais de texto dedicados, como a série [DEC VT100](https://en.wikipedia.org/wiki/VT100 "wikipedia:VT100"). Ainda é possível inicializar no modo texto se o hardware do sistema suportar, mas quase todas as distribuições modernas (incluindo o Arch Linux) usam o console framebuffer.

### Console framebuffer

Como o Linux foi portado para outras arquiteturas não-PC, foi necessária uma solução melhor, uma vez que outras arquiteturas não usam adaptadores gráficos compatíveis com VGA e podem não suportar modos de texto. O console framebuffer foi implementado para fornecer um console padrão em todas as plataformas e, portanto, apresenta a mesma interface no estilo VGA, independentemente do hardware gráfico subjacente. Como tal, o console do Linux não é um emulador de terminal, mas um terminal por si só. Ele usa o tipo de terminal `linux` e é amplamente compatível com o VT100.

## Atalhos de teclado

| Atalho de teclado | Descrição |
| `Ctrl+Alt+Del` | Reinicia o computador (especificado pelo link simbólico `/usr/lib/systemd/system/ctrl-alt-del.target`) |
| `Alt+F1`, `F2`, `F3`, ... | Alterna para o *n*º console virtual |
| `Alt+ ←` | Alterna para o console virtual anterior |
| `Alt+ →` | Alterna para o próximo console virtual |
| `Scroll Lock` | Quando Scroll Lock está ativado, entrada/saída está travada |
| `Shift+PgUp`/`PgDown` | Rola o buffer de console para cima/para baixo |
| `Ctrl+c` | Encerra a tarefa atual |
| `Ctrl+d` | Insere um EOF (fim de arquivo) |
| `Ctrl+z` | Pausa a tarefa atual |

Veja também [console_codes(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/console_codes.4).

## Fontes

**Nota:** Esta seção é sobre o [console do Linux](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console"). Para soluções de console alternativas que oferecem mais recursos (fontes Unicode completas, adaptadores gráficos modernos, etc.), consulte [fbterm](/index.php/Fbterm "Fbterm"), [KMSCON](/index.php/KMSCON "KMSCON") ou projetos semelhantes.

Por padrão, o [console virtual](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") usa a fonte embutida no kernel com um conjunto de caracteres [CP437](https://en.wikipedia.org/wiki/CP437 "wikipedia:CP437"), mas isso pode ser alterado facilmente.

O [console do Linux](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console") usa a codificação UTF-8 por padrão, mas como o framebuffer padrão compatível com VGA é usado, uma fonte do console é limitada a um padrão 256 ou 512 glifos. Se a fonte tiver mais de 256 glifos, o número de cores será reduzido de 16 para 8\. Para atribuir o símbolo correto a ser exibido ao valor Unicode fornecido, é necessário um mapa de tradução especial, geralmente chamado de *unimap*. Atualmente, a maioria das fontes do console tem o *unimap* embutido; historicamente, tinha que ser carregado separadamente.

O pacote [kbd](https://www.archlinux.org/packages/?name=kbd) fornece ferramentas para alterar a fonte do console virtual e o mapeamento de fontes. As fontes disponíveis são salvas no diretório `/usr/share/kbd/consolefonts/`, aquelas que terminam com *.psfu* ou *.psfu.gz* possuem um mapa de tradução Unicode embutido.

Os keymaps (mapas de teclado), a conexão entre a tecla pressionada e o caractere usado pelo computador, são encontrados nos subdiretórios de `/usr/share/kbd/keymaps/`, veja [/Configuração de teclado](/index.php/Console_do_Linux/Configura%C3%A7%C3%A3o_de_teclado "Console do Linux/Configuração de teclado") para detalhes.

**Nota:** Substituir a fonte pode causar problemas com programas que esperam uma fonte de estilo VGA padrão, como aqueles que usam gráficos de desenho de linha.

**Dica:** Para idiomas baseados na Europa escritos em letras latinas/gregas, você pode usar a fonte `eurlatgr`, que inclui uma ampla gama de variações de letras latinas/gregas, bem como caracteres especiais [[2]](https://lists.altlinux.org/pipermail/kbd/2014-February/000439.html).

### Visualizar alterações e alterações temporárias

**Dica:** Uma biblioteca organizada de imagens para visualização está disponível: [Linux console fonts screenshots](http://alexandre.deverteuil.net/pages/consolefonts/).

```
$ showconsolefont

```

mostra uma tabela de glifos ou letras de uma fonte.

`setfont` altera temporariamente a fonte se passado um nome de fonte (em `/usr/share/kbd/consolefonts/`) tal como

```
$ setfont lat2-16 -m 8859-2

```

Os nomes das fontes diferenciam maiúsculo de minúsculo. Com nenhum parâmetro, `setfont` retorna o console para a fonte padrão.

Então, para ter uma fonte **8x8 pequena**, com aquela fonte instalada como visto abaixo, use, por exemplo:

```
$ setfont -h8 /usr/share/kbd/consolefonts/drdos8x8.psfu.gz

```

Para ter uma fonte **maior**, a fonte Terminus ([terminus-font](https://www.archlinux.org/packages/?name=terminus-font)) está disponível em muitos tamanhos, tal como `ter-132n` que é maior.

**Dica:** Todos os comandos alteradores de fonte podem ser digitados as "cegas".

**Nota:** *setfont* só funciona no console atualmente em uso. Quaisquer outros consoles, ativos ou inativos, não são afetados.

### Configuração persistente

A variável `FONT` em `/etc/vconsole.conf` é usado para definir a fonte na inicialização, de forma persistente para todos consoles. Veja [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) para detalhes.

Para exibir caracteres tais como *Č, ž, đ, š* or *Ł, ę, ą, ś* usando a fonte `lat2-16.psfu.gz`:

 `/etc/vconsole.conf` 
```
...
FONT=lat2-16
FONT_MAP=8859-2
```

Isso significa que a segunda parte dos caracteres ISO/IEC 8859 é usada com tamanho 16\. Você pode alterar o tamanho da fonte usando outros valores (por exemplo, `lat2-08`). Para as regiões determinadas pela especificação 8859, veja [Wikipedia:ISO/IEC 8859#The parts of ISO/IEC 8859](https://en.wikipedia.org/wiki/ISO/IEC_8859#The_parts_of_ISO.2FIEC_8859 "wikipedia:ISO/IEC 8859").

Para usar a fonte especificada no espaço do usuário, use o gancho `consolefont` em `/etc/mkinitcpio.conf`. Veja [Mkinitcpio#HOOKS](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") para mais informações.

Se as fontes parecerem não mudar na inicialização, ou mudarem apenas temporariamente, é mais provável que tenham sido reiniciadas quando o driver gráfico foi inicializado e o console foi mudado para o framebuffer. Para evitar isso, carregue seu driver de gráficos anteriormente. Veja por exemplo [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting"), [[3]](https://bbs.archlinux.org/viewtopic.php?id=145765) ou outras maneiras de configurar seu framebuffer antes de `/etc/vconsole.conf` é aplicado.

### HiDPI

Veja [HiDPI#Linux console](/index.php/HiDPI#Linux_console "HiDPI").

## Veja também

*   [General troubleshooting#Scrollback](/index.php/General_troubleshooting#Scrollback "General troubleshooting")
*   [The TTY demystified – Linus Åkesson](https://www.linusakesson.net/programming/tty/)