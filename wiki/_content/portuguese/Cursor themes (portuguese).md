**Status de tradução:** Esse artigo é uma tradução de [Cursor themes](/index.php/Cursor_themes "Cursor themes"). Data da última tradução: 2020-01-25\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Cursor_themes&diff=0&oldid=589053) na versão em inglês.

O servidor de exibição é acompanhado por um *tema de cursor* padrão que ajuda em vários aspectos de navegação GUI e manipulação. Apesar disso, outros temas podem ser instalados e selecionados.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
    *   [1.1 Por pacotes](#Por_pacotes)
    *   [1.2 Manualmente](#Manualmente)
*   [2 Configuração](#Configuração)
    *   [2.1 Especificação XDG](#Especificação_XDG)
    *   [2.2 LXAppearance](#LXAppearance)
    *   [2.3 Ambientes de desktop](#Ambientes_de_desktop)
        *   [2.3.1 GNOME](#GNOME)
        *   [2.3.2 MATE](#MATE)
        *   [2.3.3 XFCE](#XFCE)
    *   [2.4 Recursos X](#Recursos_X)
    *   [2.5 Variáveis de ambiente](#Variáveis_de_ambiente)
    *   [2.6 Gerenciadores de login](#Gerenciadores_de_login)
        *   [2.6.1 GDM](#GDM)
*   [3 Solução de problemas](#Solução_de_problemas)
    *   [3.1 Crie links para cursores faltando](#Crie_links_para_cursores_faltando)
    *   [3.2 Suprindo cursores não achados](#Suprindo_cursores_não_achados)
        *   [3.2.1 rdesktop](#rdesktop)
    *   [3.3 Mude o cursor padrão com forma de X](#Mude_o_cursor_padrão_com_forma_de_X)
    *   [3.4 .Xdefaults](#.Xdefaults)
    *   [3.5 Tamanho do cursor não muda na inicialização](#Tamanho_do_cursor_não_muda_na_inicialização)
*   [4 Veja também](#Veja_também)

## Instalação

A instalação pode ser feita por pacotes, ou manualmente, fazendo o download e extração do tema no diretório apropriado.

### Por pacotes

Temas de cursores estão disponíveis em:

*   [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") — [pesquisar "xcursor-"](https://www.archlinux.org/packages/?sort=&q=xcursor-&maintainer=&last_update=&flagged=&limit=50).
*   [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") — [pesquisar "cursor"](https://aur.archlinux.org/packages.php?O=0&L=0&C=17&K=cursor&SeB=nd&SB=n&SO=a&PP=50&do_Search=Go).

### Manualmente

Se um tema de cursor não está disponível nos repositórios oficiais ou AUR, ele pode ser adicionado manualmente. Existem vários sites onde você pode baixá-los. Feito isto eles precisam ser colocados no diretório *icons* (cursores podem vir com temas de ícones).

Alguns sites que disponibilizam temas de cursores:

*   [GNOME Look](https://www.gnome-look.org/browse/cat/107/ord/latest/)
*   [Customize.org](http://www.customize.org/list/xcursors)
*   [Deviant Art](https://www.deviantart.com/browse/all/customization/skins/linuxutil/x11cursors/)
*   [Open Desktop](https://www.opendesktop.org/browse/cat/107/)

Para instalação *específica do usuário*, use o diretório `~/.local/share/icons/` ou `~/.icons/`. Extraia os temas com este comando, irá funcionar com a maioria dos arquivos tar:

```
$ tar xvf foobar-cursor-theme.tar.gz -C ~/.local/share/icons

```

A estrutura do diretório de temas de cursores é `nome-do-tema/cursors`, por exemplo: `~/.local/share/icons/*tema*/cursors/`; tenha certeza que os arquivos extraídos sigam esta estrutura.

**Nota:** Para instalação a *nível de sistema* o diretório `/usr/share/icons` é usado. Extrair diretamente para este diretório não é aconselhado pois o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") não tem controle e conhecimento sobre os arquivos extraídos desse jeito; é recomendado criar um [pacote](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para o tema de cursor.

Temas de cursores já instalados podem ser visualizados com o comando:

```
find /usr/share/icons ~/.local/share/icons ~/.icons -type d -name "cursors"

```

Se o tema possui o arquivo `index.theme`, verifique se tem uma linha "Inherits" dentro dele. Se sim, cheque se o tema herdado também existe no sistema (renomeia se necessário).

## Configuração

Existem várias maneiras de definir o tema de cursor.

### Especificação XDG

Este método se aplica tanto para temas de cursores para [X11](/index.php/X11_(Portugu%C3%AAs) "X11 (Português)") quanto para [Wayland](/index.php/Wayland_(Portugu%C3%AAs) "Wayland (Português)").

Para configuração *específica do usuário*, crie ou edite `~/.icons/default/index.theme`; para configuração a *nível de sistema*, você pode editar `/usr/share/icons/default/index.theme`.

A opção `Inherits` na seção `[icon theme]` deve ser definida para o nome do diretório, por exemplo `xcursor-breeze-snow`:

 `~/.icons/default/index.theme` 
```
[icon theme] 
Inherits=*xcursor-breeze-snow*
```

Você deve também editar `~/.config/gtk-3.0/settings.ini`, mudando `*nome_do_tema_de_cursor*` para o escolhido:

 `~/.config/gtk-3.0/settings.ini` 
```
[Settings]
gtk-cursor-theme-name=*nome_do_tema_de_cursor*
```

Faça login novamente para as mudanças serem aplicadas.

### LXAppearance

[LXAppearance](/index.php/LXDE#Cursors "LXDE") define o cursor padrão criando e modificando o arquivo `~/.icons/default/index.theme`: se você editou este arquivo manualmente, LXAppearance irá sobrescrever. Lembre-se também de editar manualmente `~/.config/gtk-3.0/settings.ini` como especificado em [#Especificação XDG](#Especificação_XDG), porque programas como o Firefox usam esta configuração.

### Ambientes de desktop

[Ambientes de desktop](/index.php/Ambientes_de_desktop "Ambientes de desktop") usam o [protocolo XSETTINGS](https://specifications.freedesktop.org/xsettings-spec/xsettings-latest.html), tipicamente implementado nas configurações de daemon. Isto permite rápida mudança de cursor, no entanto, o tema aplicado pode ser inconsistente em múltiplas aplicações. Veja [#Especificação XDG](#Especificação_XDG) para mudar o tema de cursor manualmente.

#### GNOME

Para mudar o tema no [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"), use [gnome-tweaks](https://www.archlinux.org/packages/?name=gnome-tweaks) ou defina a configuração diretamente com:

```
gsettings set org.gnome.desktop.interface cursor-theme *nome_do_tema_de_cursor*

```

Para mudar o tamanho do cursor (dependendo do tema, tamanhos são 24, 32, 48, 64):

```
gsettings set org.gnome.desktop.interface cursor-size *tamanho_do_cursor*

```

**Nota:** Por padrão, no Wayland, programas do GNOME não devem ser capazes de exibir temas de cursor localizados em `~/.local/share/icons`. Para resolver, você pode [modificar a variável de ambiente XCURSOR_PATH](#Variáveis_de_ambiente).

#### MATE

No MATE você pode usar o [mate-control-center](https://www.archlinux.org/packages/?name=mate-control-center) ou *gsettings*. Para mudar o tema de cursor:

```
gsettings set org.mate.peripherals-mouse cursor-theme *nome_do_tema_de_cursor*

```

Para mudar o tamanho:

```
gsettings set org.mate.peripherals-mouse *tamanho_do_cursor*

```

#### XFCE

Para mudar o tema, use:

```
xfconf-query --channel xsettings --property /Gtk/CursorThemeName --set *nome_do_tema_de_cursor*

```

Para mudar o tamanho:

```
xfconf-query --channel xsettings --property /Gtk/CursorThemeSize --set *tamanho_do_cursor*

```

### Recursos X

Para localmente definir um tema de cursor, adicione no arquivo `~/.Xresources`:

```
Xcursor.theme: nome-do-tema-de-cursor

```

O tema de cursor deve ser apropriadamente carregado pelo gerenciador de janelas; Se não, isto pode ser forçado ao colocar o seguinte comando no `~/.xinitrc` ou [.xprofile](/index.php/Xprofile_(Portugu%C3%AAs) "Xprofile (Português)") (depende da sua configuração pessoal):

```
$ xrdb ~/.Xresources

```

Opcionalmente, adicione esta linha para `~/.Xresources` se seu tema de cursor suporta diferentes tamanhos:

```
Xcursor.size: 16

```

**Dica:** 32, 48 ou 64 podem ser também uma boa escolha.

Se está em dúvida se isto é suportado, inicie o X sem esta configuração e deixe o tamanho do cursor ser escolhido automaticamente. (Procure por detalhes na documentação do seu gerenciador de janelas.)

### Variáveis de ambiente

Você pode usar uma [variável de ambiente](/index.php/Vari%C3%A1vel_de_ambiente "Variável de ambiente") para definir o tema em uma única aplicação, para testá-lo, exemplo:

```
$ XCURSOR_THEME=NomeDeAlgumTema xclock

```

XCURSOR_SIZE é opcional, e seu tema deve suportar diferentes tamanhos.

Se seus temas de cursor estão instalados em `~/.local/share/icons`, para evitar possíveis inconvenientes, adicione o caminho no XCURSOR_PATH. Por exemplo:

 `~/.bash_profile`  `export XCURSOR_PATH=${$XCURSOR_PATH}:~/.local/share/icons` 

### Gerenciadores de login

Um tema de cursor pode ser normalmente definido para gerenciadores de login, mas tenha em mente que isto pode não ser levado a sessão do usuário.

#### GDM

Veja [GDM (Português)#Alterando o tema do cursor](/index.php/GDM_(Portugu%C3%AAs)#Alterando_o_tema_do_cursor "GDM (Português)").

## Solução de problemas

### Crie links para cursores faltando

Programas podem continuar usando os cursores padrão quando tema não possui alguns cursores. Isto pode ser corrigido ao adicionar links para os cursores em falta. Por exemplo:

```
$ cd ~/.icons/*theme*/cursors/
$ ln -s right_ptr arrow
$ ln -s cross crosshair
$ ln -s right_ptr draft_large
$ ln -s right_ptr draft_small
$ ln -s cross plus
$ ln -s left_ptr top_left_arrow
$ ln -s cross tcross
$ ln -s hand hand1
$ ln -s hand hand2
$ ln -s left_side left_tee
$ ln -s left_ptr ul_angle
$ ln -s left_ptr ur_angle
$ ln -s left_ptr_watch 08e8e1c95fe2fc01f976f1e063a24ccd

```

Se isto não resolver o problema, procure em `/usr/share/icons/whiteglass/cursors` por cursores adicionais que podem estar faltando, e crie links para estes também.

**Dica:** Você pode também remover os cursores que não deseja, por exemplo o cursor "watch":
```
$ cd ~/.icons/*theme*/cursors/
$ rm watch left_ptr_watch
$ ln -s left_ptr watch
$ ln -s left_ptr left_ptr_watch

```

### Suprindo cursores não achados

Alguns programas podem definir seus próprios cursores em `~/.Xresources` que você pode querer sobrescrever. Um exemplo comum disto é rdesktop, que se conecta a um computador Microsoft Windows e usa os cursores obtidos da maquina remota, o que geralmente é difícil de ver devido a limitações do protocolo, levando a conversão de baixa qualidade.

Isto pode ser resolvido substituindo estes cursores com o mesmo tema(ou outro). Para fazer isto, o **hash** da imagem deve ser obtido. Isto é feito ao configurar a variável de ambiente `XCURSOR_DISCOVER` antes do lançamento do programa que define estes cursores:

```
$ XCURSOR_DISCOVER=1 rdesktop ...

```

Na primeira (e única) vez que o cursor é configurado, alguns detalhes irão ser mostrados, como:

```
Cursor image name: 24020000002800000528000084810000
...
Cursor image name: 7bf1cc07d310bf080118007e08fc30ff
...
Cursor hash 24020000002800000528000084810000 returns 0x0

```

Quando o Xcursor procura por cursores, o caminho da pesquisa inclui `~/.icons/default/cursors`, este caminho é onde uma imagem pode ser colocada para o Xcursor achar. Primeiro, crie este diretório se ele não existir:

```
$ mkdir -p ~/.icons/default/cursors

```

Então faça o link do hash para a imagem alvo. Aqui nós usamos a imagem `left_ptr` do tema de cursor `Vanilla-DMZ`:

```
$ ln -s /usr/share/icons/Vanilla-DMZ/cursors/left_ptr ~/.icons/default/cursors/24020000002800000528000084810000

```

A mudança irá ser visível quando a aplicação for reiniciada. Nenhum método especial é necessário.

#### rdesktop

Estes são alguns cursores comuns do Microsoft Windows que o rdesktop usa quando está se conectando a uma máquina Windows remotamente. Infelizmente, cursores animados são difíceis de sobrescrever já que eles são enviados frame por frame, então será necessário mapear cada um deles!

```
$ ln -s /usr/share/icons/$THEME/cursors/xterm          ~/.icons/default/cursors/00000000017e000002fc000000000000
$ ln -s /usr/share/icons/$THEME/cursors/right_ptr      ~/.icons/default/cursors/00000093000010860000631100006609
$ ln -s /usr/share/icons/$THEME/cursors/plus           ~/.icons/default/cursors/01e00000201c00004038000080300000
$ ln -s /usr/share/icons/$THEME/cursors/left_ptr       ~/.icons/default/cursors/24020000002800000528000084810000
$ ln -s /usr/share/icons/$THEME/cursors/left_ptr_watch ~/.icons/default/cursors/6ce0180090108e0005814700a0021400
$ ln -s /usr/share/icons/$THEME/cursors/hand           ~/.icons/default/cursors/d2201000a2c622004385440041308800
$ ln -s /usr/share/icons/$THEME/cursors/watch          ~/.icons/default/cursors/fc618c00da110f0034fd0e004e082400

```

### Mude o cursor padrão com forma de X

O cursor padrão com formato de X aparece em gerenciadores de janela que não definem o cursor padrão para left_ptr ou em gerenciadores de janelas que usam XCB (como, por exemplo, [awesome](/index.php/Awesome "Awesome")) ao invés da Xlib.

Para consertar isto, simplesmente adicione o seguinte para seu `~/.xinitrc` , xsession ou arquivos de configuração(ou iniciados automaticamente) do seu gerenciador de janelas se possível (por exemplo, o bspwmrc do bspwm).

```
$ xsetroot -cursor_name left_ptr

```

A lista de estilos de cursores está no [apêndice B](https://tronche.com/gui/x/xlib/appendix/b/) do protocolo X.

### .Xdefaults

Se você tem cursores que conflitam isto pode ter acontecido porquê um cursor diferente pode ter sido configurado no arquivo`~/.Xdefaults`.

### Tamanho do cursor não muda na inicialização

Se você está tentando mudar o tamanho do cursor pelo `~/.Xresources`ou em seu `~/.xinitrc` e não funciona, tenha certeza que o xrandr roda antes de carregar o `~/.Xresources`.

Tenha certeza que seu `~/.xinitrc` é similar ao seguinte:

 `~/.xinitrc` 
```
xrandr &&
...
xrdb -merge ~/.Xresources &&
exec wm
```

## Veja também

*   [Xcursor(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xcursor.3) — Para mais informações sobre cursores no Xorg (diretivas suportadas, formatos, compatibilidade, etc).