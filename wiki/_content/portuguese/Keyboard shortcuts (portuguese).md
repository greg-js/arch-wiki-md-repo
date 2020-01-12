**Status de tradução:** Esse artigo é uma tradução de [Keyboard shortcuts](/index.php/Keyboard_shortcuts "Keyboard shortcuts"). Data da última tradução: 2020-01-09\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Keyboard_shortcuts&diff=0&oldid=594274) na versão em inglês.

Este artigo visa fornecer uma lista (não tão popular) dos atalhos de teclado padrão e também fornece informações sobre sua personalização.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Atalhos padrão](#Atalhos_padrão)
    *   [1.1 Kernel](#Kernel)
    *   [1.2 Console virtual](#Console_virtual)
    *   [1.3 Xorg e Wayland](#Xorg_e_Wayland)
*   [2 Personalização](#Personalização)
    *   [2.1 Readline](#Readline)
    *   [2.2 Zsh](#Zsh)
    *   [2.3 Xorg](#Xorg)
        *   [2.3.1 sxhkd](#sxhkd)
        *   [2.3.2 actkbd](#actkbd)
        *   [2.3.3 xbindkeys](#xbindkeys)
    *   [2.4 Ambientes de desktop](#Ambientes_de_desktop)
    *   [2.5 Gerenciadores de janela](#Gerenciadores_de_janela)
    *   [2.6 Associação de teclas para X-selection-paste](#Associação_de_teclas_para_X-selection-paste)
        *   [2.6.1 XMonad Window Manager](#XMonad_Window_Manager)
*   [3 Dicas e truques](#Dicas_e_truques)
*   [4 Veja também](#Veja_também)

## Atalhos padrão

### Kernel

Existem certos atalhos de baixo nível implementados no kernel que podem ser usados para depuração e recuperação de um sistema instável ou travado. Sempre que possível, recomenda-se que estes atalhos sejam utilizados ao invés de fazer um desligamento forçado via hardware (segurando o botão de energia até desligar completamente o sistema).

Para utilizá-los, estes devem primeiro ser ativados com `sysctl kernel.sysrq=1` ou `echo "1" > /proc/sys/kernel/sysrq`. Valores maiores do que 1 podem ser usados para parcialmente ativar determinadas funções, veja a [documentação do Linux Kernel](https://www.kernel.org/doc/html/latest/admin-guide/sysrq.html) para detalhes.

Se desejar tê-las ativadas já durante o boot, adicione a configuração apropriada para a [configuração do sysctl](/index.php/Sysctl#Configuration "Sysctl"). Se quiser ter certeza de que elas serão ativadas mesmo antes das partições serem montadas e no initrd, então adicione `sysrq_always_enabled=1` nos [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel").

Uma linguagem comum para decorá-las é, do inglês, "**R**eboot **E**ven **I**f **S**ystem **U**tterly **B**roken" (ou simplesmente "REISUB"), que quer dizer, a grosso modo, "reinicie mesmo se o sistema estiver completamente quebrado". Outra maneira de se lembrar da sequência de teclas é pensar na palavra, "BUSIER" lida de trás para frente (também do inglês, que quer dizer algo como ocupado demais).

| Atalho | Descrição |
| `Alt+SysRq+r` Unraw | Toma o controle do teclado do servidor X, e assume. |
| `Alt+SysRq+e` Terminate | Envia o sinal SIGTERM a todos os processos, permitindo encerrá-los de maneira não arbitrária ou forçada. |
| `Alt+SysRq+i` Kill | Envia o sinal SIGKILL para todos os processos, forçando-os a se encerrarem imediatamente. |
| `Alt+SysRq+s` Sync | Grava os dados na unidade de disco rígido. |
| `Alt+SysRq+u` Unmount | Desmonta e remonta todos os sistemas de arquivos em modo somente leitura. |
| `Alt+SysRq+b` Reboot | Reinicia o sistema. |

**Dica:**

*   Se estiver usando um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição") e após `Alt+SysRq+e` você for levado à tela de login (ou à sua área de trabalho caso o login automático estiver ativado), então provavelmente a diretiva `Restart=always` no [arquivo *service*](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") é a responsável. Se necessário, [edite a unit](/index.php/Edite_a_unit "Edite a unit"), embora isto não deve evitar que a sequência "REISUB" funcione.
*   Caso todas as combinações acima funcionem, exceto `Alt+SysRq+b`, tente usar a tecla `Alt` do lado oposto do teclado.
*   Em laptops que usam a tecla `Fn` para diferenciar a função `SysRq` de `PrtScrn`, pode não ser necessário usar a tecla `Fn` (isto é, simplesmente pressionar `Alt+PrtSc+*letra*` pode ser o suficiente).
*   Em laptops Lenovo, `SysRq` é frequentemente configurada como `Fn+S`. Para usá-la, pressione e segure `Alt`, então pressione `Fn+s`, **solte** `Fn` e `s` e, ainda segurando `Alt` use a combinação de teclas acima.
*   Pode ser necessário pressionar `Ctrl` junto de `Alt`. Então, por exemplo, o atalho completo pode ser `Ctrl+Alt+SysRq+b`.

Veja [Wikipedia:Magic SysRq key](https://en.wikipedia.org/wiki/Magic_SysRq_key "wikipedia:Magic SysRq key") para mais detalhes.

### Console virtual

Veja [Console do Linux#Atalhos de teclado](/index.php/Console_do_Linux#Atalhos_de_teclado "Console do Linux").

### Xorg e Wayland

| Teclas de atalho | Descrição | Notas |
| `Ctrl+Alt+F1`, `F2`, `F3`, ... | Alterna para o *n*-ésimo console virtual | Se não funcionar, tente `Ctrl+Fn+Alt+F…` com as demais teclas de função. |
| `Shift+Insert`
`Mouse Button 2` | Cola texto do [PRIMARY buffer](/index.php/Clipboard "Clipboard") | Por padrão, o Qt mapeia `Shift+Insert` para a área de transferência ao invés do buffer PRIMARY (veja exemplo [[1]](http://doc.qt.io/qt-5/qlineedit.html#details)) enquanto `Ctrl+Shift+Insert` é mapeado para o buffer PRIMARY. |

## Personalização

### Readline

[Readline](/index.php/Readline "Readline") é uma biblioteca comumente usada para edição de linha; e é usada, por exemplo pelo [Bash](/index.php/Bash "Bash"), FTP, e muitos outros (veja detalhes do pacote [readline](https://www.archlinux.org/packages/?name=readline), na coluna "Required By" da tabela, para mais exemplos). É semelhante ao estilo de edição do [Emacs](/index.php/Emacs "Emacs") e do [vi](/index.php/Vi "Vi"), que podem ser personalizados com sequências de escape. Combinações padrão de teclas estão listadas em sua [documentação](https://tiswww.cwru.edu/php/chet/readline/rluserman.html).

### Zsh

[Zsh](/index.php/Zsh "Zsh") utiliza [ZLE](/index.php/Zsh#Key_bindings "Zsh") para ligar atalhos a widgets, scripts e comandos.

### Xorg

Veja [Xorg/Keyboard configuration#Frequently used XKB options](/index.php/Xorg/Keyboard_configuration#Frequently_used_XKB_options "Xorg/Keyboard configuration") alguns atalhos comuns, que são desativados por padrão.

Em um ambiente gráfico, podemos querer executar um comando quando certa combinação de teclas é pressionada (isto é, um comando ligado a uma *keysym*). Existem várias maneiras de se fazer isso:

*   A maneira mais prática é usando ferramentas de baixo nível , como uma daemon [acpid](/index.php/Acpid "Acpid"). Nem todas as teclas são suportadas, mas uma configuração de maneira bastante uniforme é possível para teclas, conexão com fontes de energia e até mesmo ao plugar/desplugar um conector de fone de ouvido. Também é difícil executar programas dentro de uma sessão do X corretamente.
*   A maneira universal é usando utilitários do [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") (por exemplo, [xbindkeys](/index.php/Xbindkeys "Xbindkeys")) e eventualmente as ferramentas de seu gerenciador de janelas ou ambiente de desktop.
*   A maneira mais rápida é através de programas de terceiros que façam tudo via interface gráfica, tais como a Central de Controle do GNOME.

#### sxhkd

Uma simplória daemon hotkey para o X com uma poderosa e compacta sintaxe de configuração. Veja [sxhkd](/index.php/Sxhkd "Sxhkd") para detalhes.

#### actkbd

Da [site do actkbd](http://users.softlab.ece.ntua.gr/~thkala/projects/actkbd/):

	[actkbd](https://aur.archlinux.org/packages/actkbd/) (disponível no [AUR](/index.php/AUR "AUR")) é uma simples daemon que interliga ações a eventos de teclado. É capaz de reconhecer combinações de tecla com suporte a eventos do tipo pressionar, repetir e soltar. Atualmente suporta somente a interface linux-2.6 evdev. Utiliza um arquivo de configuração em forma de planilha de texto que contém todas as vinculações de tecla.

Um modelo de configuração, bem como guia, estão disponíveis [aqui](http://users.softlab.ece.ntua.gr/~thkala/projects/actkbd/latest/README).

#### xbindkeys

[xbindkeys](/index.php/Xbindkeys "Xbindkeys") permite mapeamento avançado de teclas para ações independentemente do ambiente de desktop *(Desktop Environment)*.

**Dica:** Se você achar `xbindkeys` difícil de usar, experimente o gerenciador gráfico [xbindkeys_config-gtk2](https://aur.archlinux.org/packages/xbindkeys_config-gtk2/) disponível no [AUR](/index.php/AUR "AUR").

### Ambientes de desktop

*   [LXDE#Bindings](/index.php/LXDE#Bindings "LXDE")
*   [Xfce#Atalhos de teclado](/index.php/Xfce_(Portugu%C3%AAs)#Atalhos_de_teclado "Xfce (Português)")

### Gerenciadores de janela

*   [Fluxbox#Hotkeys](/index.php/Fluxbox#Hotkeys "Fluxbox")
*   [Openbox#Keybinds](/index.php/Openbox#Keybinds "Openbox")

### Associação de teclas para X-selection-paste

Usuários que preferem usar mais o teclado ao invés do mouse podem se beneficiar de um atalho de teclado para operação de colagem que até então é feita através do botão intermediário do mouse. Isto é especialmente útil em um ambiente baseado em utilização do teclado. Um exemplo de como seria este fluxo de trabalho vem a seguir:

1.  No Firefox, selecione (com o mouse) um texto que deseja pesquisar no google.
2.  Pressione `Ctrl+k` para abrir o campo de busca.
3.  Pressione `F9` para colar o texto, ao invés de ter que mover o ponteiro do mouse para dentro do campo de busca e usar o botão intermediário do mouse para colá-lo.

**Nota:** `Shift+Insert` tem uma funcionalidade parecida, mas diferente. Veja [#Xorg](#Xorg): `Shift+Insert` insere o buffer da área de transferência, e não o x-selection-buffer. Em algumas aplicações, ambos os buffers são espelhados.

O método sugerido aqui usa três pacotes::

*   [xsel](https://www.archlinux.org/packages/?name=xsel) para dar acesso ao conteúdo do x-selection-buffer.
*   [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") para vincular pressionamento de teclas a uma ação.
*   [xvkbd](https://aur.archlinux.org/packages/xvkbd/) para passar a string do buffer para a aplicação ao emular uma entrada de teclado.

Este exemplo vincula uma operação do x-selection-paste à tecla `F9`:

 `.xbindkeysrc` 
```
"xvkbd -no-jump-pointer -xsendevent -text "\D1`xsel`" 2>/dev/null"
    F9

```

O código `"\D1"` estabelece uma pause de 100 ms para inserir a seleção do buffer (veja a [site do xvkbd](http://t-sato.in.coocan.jp/xvkbd/)).

**Nota:** Dependendo da configuração do seu X, pode ser necessário descartar o argumento `-xsendevent` ao xvkbd.

Os códigos para outras teclas diferentes de `F9` podem ser determinados usando `xbindkeys -k`.

Referências (em inglês):

*   [Pasting X selection (not clipboard) contents with keyboard](http://unix.stackexchange.com/questions/11889/pasting-x-selection-not-clipboard-contents-with-keyboard)
*   [site do xvkbd](http://homepage3.nifty.com/tsato/xvkbd/)

#### XMonad Window Manager

No gerenciador de janela [xmonad](https://www.archlinux.org/packages/?name=xmonad) existe uma função embutida para colar o conteúdo do x-selection-buffer. De modo a vincular esta função a um pressionamento de teclas, (aqui, a tecla `Insert`), a seguinte configuração pode ser usada:

 `xmonad.hs` 
```
import XMonad.Util.Paste
...
  -- X-selection-paste buffer
  , ((0,                     xK_Insert), pasteSelection) ]

```

## Dicas e truques

*   Se você é adepto ao uso do computador primordialmente com teclado, você pode gostar de um [Gerenciadores de janela#Gerenciadores de janela de tiling](/index.php/Gerenciadores_de_janela#Gerenciadores_de_janela_de_tiling "Gerenciadores de janela").

## Veja também

*   [The Linux Magic System Request Key - Kernel documentation](https://www.kernel.org/doc/html/latest/admin-guide/sysrq.html)
*   [Linux Newbie Administrator Guide - Shortcuts and Commands](http://lnag.sourceforge.net/lnag_html/node5.html)
*   [The Linux keyboard and console HOWTO](http://tldp.org/HOWTO/Keyboard-and-Console-HOWTO.html)