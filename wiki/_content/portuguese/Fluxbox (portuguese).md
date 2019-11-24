Flubox é um gerenciador de janelas para X11\. É baseado no código do(agora descontinuado) Blackbox 0.61.1, porém com significantes melhoras e desenvolvimento contínuo. Fluxbox é bastante leve a nível de recursos e rápido, e ainda provê ferramentas interesantes para gerenciamento de janelas como abas e agrupamentos. Seus arquivos de configuração são fáceis de entender e editar e existem centenas de "estilos" de fluxbox para tornar a aparencia do seu desktop legal. ArchLinux com FluxBox pode tornar um velho Pentium 800 com apenas 256MB de RAM em um computador bastante usável.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Iniciando o Fluxbox](#Iniciando_o_Fluxbox)
    *   [2.1 Método 1: Gerenciadores de Login KDM/GDM/LightDM](#Método_1:_Gerenciadores_de_Login_KDM/GDM/LightDM)
    *   [2.2 Método 2: ~/.xinitrc](#Método_2:_~/.xinitrc)
    *   [2.3 Método 3: Gerenciador de login SLiM](#Método_3:_Gerenciador_de_login_SLiM)
*   [3 Configuração](#Configuração)
    *   [3.1 Gerenciamento do menu](#Gerenciamento_do_menu)
        *   [3.1.1 fluxbox-generate_menu](#fluxbox-generate_menu)
        *   [3.1.2 MenuMaker](#MenuMaker)
        *   [3.1.3 Arch Linux Xdg menu](#Arch_Linux_Xdg_menu)
        *   [3.1.4 Editar/Criar manualmente o menu](#Editar/Criar_manualmente_o_menu)
    *   [3.2 Init](#Init)
    *   [3.3 Teclas de atalho(Hotkeys)](#Teclas_de_atalho(Hotkeys))
    *   [3.4 Workspaces](#Workspaces)
    *   [3.5 Abas e Agrupamento](#Abas_e_Agrupamento)
    *   [3.6 Fundo (Wallpaper)](#Fundo_(Wallpaper))
        *   [3.6.1 Alterando diversos fundos facilmente](#Alterando_diversos_fundos_facilmente)
        *   [3.6.2 Utilizando o Feh com FluxBox](#Utilizando_o_Feh_com_FluxBox)
    *   [3.7 Temas](#Temas)
    *   [3.8 Iniciando automaticamente aplicativos](#Iniciando_automaticamente_aplicativos)
    *   [3.9 Outros menus](#Outros_menus)
    *   [3.10 Terminais transparentes rxvt-unicode](#Terminais_transparentes_rxvt-unicode)
    *   [3.11 Vida após "xorg.conf"](#Vida_após_"xorg.conf")
        *   [3.11.1 Configurando o seu layout de teclado](#Configurando_o_seu_layout_de_teclado)
        *   [3.11.2 Desabilitando economia de energia](#Desabilitando_economia_de_energia)
*   [4 Recursos Adicionais](#Recursos_Adicionais)

## Instalação

A instalação é tão fácil quanto:

1.  pacman -S fluxbox fluxconf

## Iniciando o Fluxbox

### Método 1: Gerenciadores de Login KDM/GDM/LightDM

Usuários do KDM, [GDM](/index.php/GDM_(Portugu%C3%AAs) "GDM (Português)") e LightDM deverão encontrar uma nova entrada referente ao fluxbox de forma automática na lista de sessões disponíveis. Apenas selecione o fluxbox quando logando.

### Método 2: ~/.xinitrc

Edite `~/.xinitrc` e adicione o seguinte código:

```
exec fluxbox

```

Se você prefere ter os dispositivos montados automaticamente(ex: no Thunar ou outros gerenciadores de arquivo), use o seguinte código:

```
exec startfluxbox

```

Veja [Xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)") para maiores detalhes. Utilize o comando "startx" de um terminal para lançar o X com o seu gerenciador de janelas.

### Método 3: Gerenciador de login SLiM

SLiM, the Simple Login Manager(o gerenciado de login simples) é o favorito para muitos usuários do Arch por conta de sua eficiência. O SLiM lê o arquivo ~/.xinitrc, portanto, se você tiver o .xinitrc configurado como o acima irá funcionar. Contudo, se você quer habilitar o SLiM para escolher entre diversos gerenciadores de janelas então edite a variavel de sessões no arquivo `/etc/slim.conf` para que os nomes sejam comparados com a declaração "case" no arquivo `~/.xinitrc` Veja [SLiM](/index.php/SLiM_(Portugu%C3%AAs) "SLiM (Português)") e [Xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)").

## Configuração

O arquivo de configuração global do Fluxbox reside em {{ic|/usr/share/fluxbox}, enquanto o arquivo de configuração específico do usuário em `~/.fluxbox`. Os arquivos de usuário são:

*   init: arquivo principal de configuração de recursos. Ver [Editando o arquivo init](http://fluxbox-wiki.org/index.php?title=Editing_the_init_file)
*   menu: configuração de menu do fluxbox. Ver abaixo e em [Editando o arquivo menu](http://fluxbox-wiki.org/index.php?title=Editing_the_menu)
*   keys: arquivo de atalhos de teclado(hotkeys) do fluxbox. Ver abaixo e [aqui](http://fluxbox-wiki.org/index.php?title=Keyboard_shortcuts)
*   startup: aplicações lançadas no iniciar, porém veja o .xinitrc e [aqui](http://fluxbox-wiki.org/index.php?title=Editing_the_startup_file)
*   overlay: arqivo de configuração para sobrescreves elementos de estilos. Ver [aqui](http://fluxbox-wiki.org/index.php?title=Style_overlay)
*   apps: arquivo de configuração para guardar configuração de janelas de aplicações especificas. Ver [aqui](http://fluxbox-wiki.org/index.php?title=Editing_the_apps_file)
*   windowmenu: arquivo de configuração para alterar o próprio Window Menu: [Leia-me](http://fluxbox-wiki.org/index.php?title=Editing_the_windowmenu)

Alguns arquivos de menor importancia existem neste diretório. Porém os principais são init, menu, keys e talvez o startup.

### Gerenciamento do menu

Na primeira instalação do fluxbox, uma lista básica de aplicativos será criado em ~/.fluxbox/menu. Você acessa o menu através do clique com o botão direito do mouse no desktop. Como qualquer outro gerenciador de janelas leve, o Fluxbox não atualiza o seu menu automaticamente ao instalar cada aplicativo novo. É recomendado que você instale a maioria dos aplicativos que deseja primeiro e então gere novamente ou edite o menu. Para aprimorar o menu e adicionar/editar itens, as quatro coisas básicas a se fazer são:

#### fluxbox-generate_menu

Existe um comando built-in com o fluxbox:

```
$ fluxbox-generate_menu

```

Este comando irá gerar automaticamente o `~/.fluxbox/menu/`, baseado em seus programas instalados. Porém, o menu gerado não será tão detalhado quanto um gerado pelo "menumaker" (imediatamente abaixo).

#### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net) é uma ferramenta poderosa que cria menus baseados em XML para uma variedade de gerenciadores de janela, incluindo o Fluxbox. O MenuMaker irá buscar em seu computador por programas executáveis e criará um menu baseado nos resultados. Pode ser configurado para excluir aplicações do X(legadas), GNOME, KDE ou Xfce se desejado.

Para instalar o MenuMaker:

```
# pacman -S menumaker

```

Uma vez instalado, um novo e completo menu pode ser gerado sobrescrevendo o padrão apenas executando:

```
$ mmaker -f FluxBox

```

Para verificar as opções do MenuMaker:

```
$ mmaker --help

```

#### Arch Linux Xdg menu

Requisito - [XdgMenu](/index.php/XdgMenu "XdgMenu") disponível via pacman:

```
# pacman -S archlinux-xdg-menu

```

Para criar o menu do Fluxbox:

```
$ xdg_menu --fullmenu --format fluxbox --root-menu /etc/xdg/menus/arch-applications.menu >~/.fluxbox/menu

```

Informações adicionais:

```
$ xdg_menu --help

```

#### Editar/Criar manualmente o menu

Use seu editor de texto favorito e edite o arquivo: "~/.fluxbox/menu" . A sintaxe básica para um item de menu é:

```
[exec] (nome) {comando} <caminho para o ícone>

```

...onde "nome" é o texto que aparecerá no item do menu e "comando" é a localização do binário. ex:

```
[exec] (Navegador Firefox) {/usr/bin/firefox} <caminho para o ícone do Firefox>

```

Se você deseja um submenu:

```
[submenu] (Nome)
...
...
[end]

```

Quando terminado de editar o arqivo, salve. Não há necessidade de reiniciar o fluxbox. Para maiores informações, ver [editando o menu do fluxbox](http://fluxbox-wiki.org/index.php?title=Editing_the_menu).

### Init

O arquivo ~/.fluxbox/init é o recurso primário de configuração do Fluxbox. Você pode alterar o funcionamento básico, janelas, toolbar, foco, etc. Algumas destas opções estão também disponíveis no menu de configuração do Fluxbox. Para maiores detalhes leia [editando o arquivo init](http://fluxbox-wiki.org/index.php?title=Editing_the_init_file).

### Teclas de atalho(Hotkeys)

O Fluxbox oferece uma funcionalidade básica de teclas de atalho. O arquivo que define tais hotkeys é o `~/.fluxbox/keys`. A tecla Control é representada por "COntrol". Mod1 corresponde a tecla Alt e Mod4 corresponte a Meta (não é uma tecla padrão, porém muitos usuários mapeiam-a como tecla "Win"). Logo após instalado, uma série de teclas de atalho já padronizadas lhe darão um ambiente confortável no Fluxbox. Você deve aprender a manipular o arquivo ~/.fluxbox/keys, para melhorar sua produtividade e experiência com o Fluxbox.

Exemplo: Forma rápida de controlar o volume principal(Master):

```
Control Mod1 Up :Exec amixer set Master,0 5%+
Control Mod1 Down :Exec amixer set Master,0 5%-

```

### Workspaces

O Fluxbox por padrão trabalha com quatro workspaces. Eles estão acessíveis através dos atalhos Ctrl+F1-F4, ou usando o clique esquerdo do mouse nas setas que residem na toolbar. Você pode também acessar uma workspace através de um clique com o botão do meio no desktop, que lhe tratá o menu dos Workspaces disponíveis.

### Abas e Agrupamento

Com no mínimo duas janelas visíveis no seu desktop, clique com o botão do meio do mouse na aba superior de uma das janelas e solte-a em outra janela aberta. As duas janelas serão agrupadas através de abas na barra superior da janela. Agora você pode executar operações na janela, e o grupo inteiro será afetado.

### Fundo (Wallpaper)

Configurar um plano de fundo(wallpaper) no Fluxbox é historicamente perturbador, especialmente quando transparência é um requisito. A Wiki do Fluxbox agora possui um artigo para [configuração de background](http://fluxbox-wiki.org/index.php?title=Howto_set_the_background) então, use com sabedoria.

A forma mais fácil de fazer isto no ArchLinux é primeiro verificar se você possui disponível uma configuração correta para a aplicação do fundo:

```
 $ fbsetbg -i

```

Se não, instale feh, esetroot ou wmsetbg utilizando o pacman. Então adicione esta linha do "fbsetbg" no seu arquivo ~/.xinitrc antes da entrada "exec". Exemplo:

```
 fbsetbg /path/to/my/image.image
 exec startfluxbox

```

#### Alterando diversos fundos facilmente

Adicione o seguinte submenu no seu menu do Fluxbox:

```
[submenu] (Backgrounds)
[wallpapers] (~/.fluxbox/backgrounds)
[wallpapers] (/usr/share/fluxbox/backgrounds)
[end]

```

Então, adicione suas imagens que serão utilizadas como plano de fundo em `~/.fluxbox/backgrounds` ou algum outro diretório de sua preferência(e altere acima obviamente), que eles aparecerão em uma seleção da mesma forma que os estilos do Fluxbox.

#### Utilizando o Feh com FluxBox

Instalando o feh:

```
# pacman -S feh

```

Você pode adicionar um submenu rapidamente no arquivo `~/.fluxbox/menu`, que lhe permitirá a troca de fundos "on-the-fly"

```
[submenu] (Backgrounds)
[backgrounds] (/path/to/your/backgrounds) {feh --bg-scale}
[end]

```

Para ter certeza que o fluxbox irá carregar o feh em background no momento do início:

**1.** Faça o arquivo `.fehbg` executável:

```
$ chmod 770 ~/.fehbg

```

**2.** Adicione(ou modifique) a seguinte linha em `~/.fluxbox/init`:

```
session.screen0.rootCommand:	~/.fehbg

```

**3.** Adicione(ou modifique) a seguinte linha em `~/.fluxbox/startup`:

```
~/.fehbg

```

### Temas

Para instalar um novo tema no fluxbox basta extrair o arquivo de tema ao diretório de estilos. Os diretórios padrões são:

*   global - `/usr/share/fluxbox/styles`
*   user only - `~/.fluxbox/styles`

O [AUR](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)") atualmente contém uma compilação de temas de fluxbox bastante bonitos, chamados de "fluxbox-stiles". Adquira-os [aqui](https://aur.archlinux.org/packages.php?ID=28743) e instale este pacote para uma maior gama de temas disponíveis. QUando instalado corretamente, eles aparecerão no Fluxbox, na sessão "Styles" do menu do Fluxbox.

Para criar seus próprios estilos no fluxbox, leia o artigo [Fluxbox Style Guide](/index.php/Fluxbox_Style_Guide "Fluxbox Style Guide") e este [guia de estilos](http://tenr.de/howto/style_fluxbox/style_fluxbox.html).

### Iniciando automaticamente aplicativos

O modo ArchLinux de iniciar aplicativos automaticamente é colocar todo o código dentro do `~/.xinitrc`. Veja [Xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)") para maiores detalhes. Contudo, fluxbox provê funcionalidades de iniciar automaticamente aplicativos de sua própria forma. O arquivo `~/.fluxbox/startup` é um script de "autostart" de programas, e de início do fluxbox mesmo. O símbolo # denota um comentário

Arquivo de exemplo:

```
fbsetbg -l # sets the last background set, very useful and recommended.
# In the below commands the ampersand symbol (&) is required on all applications that do not terminate immediately. 
# failure to provide them will cause fluxbox not to start.
idesk & 
xterm &
# exec is for starting fluxbox itself, do not put an ampersand (&) after this or fluxbox will exit immediately
exec /usr/bin/fluxbox
# or if you want to keep a log, uncomment the below command and comment out the above command:
# exec /usr/bin/fluxbox -log ~/.fluxbox/log

```

### Outros menus

Na seção "Gerenciamento do menu"(acima) nos discutimos sobre o menu de aplicações, chamdo de "Root" menu no fluxbox. O FluxBox também possui outros menus disponíveis para o usuário:

*   Workspaces Menu: Clique com o botão do meio no desktop.
*   Configuration Menu: Localizado na seção Fluxbox do "Root menu".
*   Window menu: Clique direito na barra de título de qualquer janela, ou se na barra de minimizada. Pode ser editado. Veja a página de manuais do fluxbox-menu(man fluxbox-menu).
*   Toolbar menu: Clique direito em uma toolbar vazia. Também pode ser encontrada como um submenu do menu de configurações(Configuration Menu).
*   Slit Menu: Sub-menu do menu de configurações.

### Terminais transparentes rxvt-unicode

Instale urxvt:

```
 # pacman -S rxvt-unicode

```

Execute o urxvt com os seguintes parametros:

```
 $ urxvt -depth 32 -bg rgba:0000/0000/0000/bbbb -tint grey

```

Ou você pode editar o arquivo ~/.Xdefaults e adicionar um equivalente do comando urxvt. Veja [Xdefaults](/index.php/Xdefaults "Xdefaults") para maiores informações.

### Vida após "xorg.conf"

O Xorg não requer mais o arquivo de configuração xorg.conf. Tradicionalmente este é o arquivo onde você deveria alterar layout de teclado e opções de gerenciamento de energia. Com sorte, existem soluções elegantes que não usam o xorg.conf.

#### Configurando o seu layout de teclado

Apenas adicione a seguinte linha ao arquivo `~/.fluxbox/startup`: setxkbmap us -variant intl & # Para teclados de layout americano(us), mas que tem acesso a acentuação(como éóíáú).

Ao invés de 'us" você pode passar diretamente a linguagem e sua variação(como por exemplo 'us_intl'). Veja os manuais de setxkbmap para mais opções.

Para ficar mais fácil, adicione no seu menu editando o arquivo `~/.fluxbox/menu`:

```
[submenu] (Keyboard)
      [exec] (normal) {setxkbmap us}
      [exec] (international) {setxkbmap us -variant intl}
[end]

```

#### Desabilitando economia de energia

Você sabe bem a raiva que dá quando a tela fica branca enquanto você assiste um filme? Pois é, o Xorg detectou que você não estava fazendo nada :). Se você não necessita tal funcionalidade, ela pode ser desativada. Basta que você lembre de desligar seu monitor na mão quando não estiver utilizando ele.

Apenas adicione a seguinte linha ao arquivo `~/.fluxbox/startup`:

```
xset s off -dpms &

```

## Recursos Adicionais

*   [Fluxbox Homepage](http://fluxbox.org/)
*   [Fluxbox Wiki](http://fluxbox-wiki.org/)
*   [Wiki do Gentoo sobre o Fluxbox](http://wiki.gentoo.org/wiki/Fluxbox)
*   [Temas para Fluxbox](http://box-look.org/)
*   [Guia de estilo para o Fluxbox](/index.php/Fluxbox_Style_Guide "Fluxbox Style Guide")
*   [Guia do Narada - Fluxbox](https://bbs.archlinux.org/viewtopic.php?id=77729)
*   Páginas de manual do fluxbox: fluxbox, fluxbox-menu, fluxbox-style, fluxbox-keys, fluxbox-apps, fluxbox-remote, fbsetroot, fbsetbg, fbrun, startfluxbox.
*   [Screenshots do Fluxbox no ArchLinux](https://bbs.archlinux.org/viewtopic.php?id=90260)