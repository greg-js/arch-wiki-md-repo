Além do ponteiro preto padrão, há vários esquemas de ponteiros (cursor) disponíveis para o Sistema de Janelas X11\. Este guia irá guiá-lo em como obter, instalar e configurar esses ponteiros.

## Contents

*   [1 Obtendo Temas para o Ponteiro do Mouse](#Obtendo_Temas_para_o_Ponteiro_do_Mouse)
*   [2 Instalando os Temas para o Ponteiro do Mouse](#Instalando_os_Temas_para_o_Ponteiro_do_Mouse)
*   [3 Configurando o Tema do Ponteiro](#Configurando_o_Tema_do_Ponteiro)
*   [4 Maiores informações](#Maiores_informa.C3.A7.C3.B5es)

## Obtendo Temas para o Ponteiro do Mouse

Aqui são alguns links onde você pode baixar ponteiros:

*   [KDE Look](http://kde-look.org/index.php?xcontentmode=36)
*   [Freshmeat](http://themes.freshmeat.net/browse/982/)
*   [Customize.org](http://www.customize.org/list/xcursors)

Alguns temas também estão disponíveis no [AUR](https://aur.archlinux.org/packages.php?O=0&L=0&C=17&K=cursor&SeB=nd&SB=n&SO=a&PP=50&do_Search=Go)

**Nota:** O X já vem com os temas 'redglass' e 'whiteglass' em `/usr/X11R6/lib/icons ou /usr/share/icons.`

## Instalando os Temas para o Ponteiro do Mouse

**Extraia o pacote do tema:**

```
$ tar -zxvf foobar-cursor-theme-package-foo.tar.gz

```

ou

```
$ tar -jxvf foobar-cursor-theme-package-foo.tar.bz2

```

**Crie um diretório para o tema:**

*Exemplo:* FooBar-AweSoMe-Cursors-v2.98beta

Instalação na pasta do Usuário (pessoal):

```
$ mkdir -p ~/.icons/foobar/cursors

```

Instalação na pasta do Sistema (global):

```
# mkdir -p /usr/share/icons/foobar/cursors

```

**Nota:** Para simplificar o nome do tema, o nome inicial usado ao criar os diretório(s) acima é 'foobar' ao invés de 'FooBar-AweSoMe-Cursors-v2.98beta'.

**Copiando os arquivos do ponteiro para um diretório apropriado:**

Instalação na pasta do Usuário (pessoal):

```
$ cp -a FooBar-AweSoMe-Cursors-v2.98beta/cursors/* ~/.icons/foobar/cursors/

```

Instalação na pasta do Sistema (global):

```
# cp -a FooBar-AweSoMe-Cursors-v2.98beta/cursors/* /usr/share/icons/foobar/cursors/

```

Se o pacote incluir o arquivo index.theme, verifique se existe uma linha "Inherits" no arquivo. Se sim, verifique qualquer tema herdado que também existe sob esse nome em seu sistema (renomeie se for necessário).

**Copiando o index.theme do ponteiro para um diretório apropriado:**

Instalação na pasta do Usuário (pessoal):

```
$ cp -a FooBar-AweSoMe-Cursors-v2.98beta/index.theme ~/.icons/foobar/index.theme

```

Instalação na pasta do Sistema (global):

```
# cp -a FooBar-AweSoMe-Cursors-v2.98beta/index.theme /usr/share/icons/foobar/index.theme

```

Se o pacote não tem o arquivo index.theme ou se ele não inclui uma linha "Inherits", você não precisa copiar esse arquivo.

**Criando links para ponteiros ausentes:**

Os aplicativos podem continuar usando os ponteiros padrões do X11 quando algum tema falta alguns ponteiros. Se você experienciar isso, ele pode ser corrigido adicionado links para os ponteiros ausentes. Por exemplo:

```
$ cd ~/.icons/foobar/cursors/
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

Se os links acima não resolver o problema, veja em `/usr/share/icons/whiteglass/cursors` por ponteiros adicionais do tema que estejam ausentes, e então crie links para eles também.

## Configurando o Tema do Ponteiro

Para nomear um tema localmente, adicione para o seu `~/.Xdefaults`:

```
Xcursor.theme: foobar

```

Para fazer com que o tema seja carregado corretamente, ele precisa ser chamado pelo seu gerenciador de janela. Se não for o seu caso, você pode forçar seu gerenciador de janela para carregar o tema, colocando o seguinte comando em [xprofile](/index.php/Xprofile_(Portugu%C3%AAs) "Xprofile (Português)"):

```
xrdb ~/.Xdefaults

```

Consulte a documentação do seu gerenciador de janela para maiores detalhes.

Alternativamente, você pode criar um link simbólico "default" (padrão) em `~/.icons`, que aponta para a instalação do seu tema de ponteiro:

```
$ ln -s /usr/share/icons/foobar/ ~/.icons/default

```

Se você prefere que o ponteiro seja mudado globalmente (ex: usado por gerenciadores de login como kdm, gdm, ...), ou se você experienciar problemas com os métodos acima (por exemplo no Firefox), crie o diretório `/usr/share/icons/default/` **(apenas se for necessário)**:

```
# mkdir -p /usr/share/icons/default  **(apenas se for necessário)**

```

Edite ou crie o arquivo `/usr/share/icons/default/index.theme` e adicione o seguinte:

```
 [icon theme] 
Inherits=foobar

```

Ou se você tem/queira apenas os temas de ponteiro em `~/.icons`. Crie o diretório `~/.icons/default/`:

```
$ mkdir -p ~/.icons/default

```

E crie o arquivo `~/.icons/default/index.theme` com o mesmo conteúdo acima `/usr/share/icons/default/index.theme`.

Se o seu ponteiro suporta múltiplos tamanhos. você pode opcionalmente adicionar essa linha para `~/.Xdefaults`:

```
Xcursor.size:  16       !  32, 48 ou 64 também pode ser bons valores

```

Se você não conhece os tamanhos de ponteiro suportado, apenas inicie o X sem essa configuração e deixe que ele escolha o tamanho do ponteiro automaticamente.

## Maiores informações

Para maiores informações sobre os ponteiros no X (diretórios suportado, formatos, compatibilidade, etc.) consulte a página do man:

```
$ man Xcursor

```

**Nota:** Se as animações estão piscando em sua placa nvidia, adicione a seguinte linha dentro da seção nvidia device em seu arquivo `/etc/X11/xorg.conf` para resolver esse problema:

```
Option "HWCursor" "off"

```