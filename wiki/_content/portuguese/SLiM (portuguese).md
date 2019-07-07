Artigos relacionados

*   [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição")

[SLiM](http://slim.berlios.de/) é um acrônimo para Gerenciador de Login Simples (Simple Login Manager). SLiM é simples, leve e fácil de ser configurado. SLiM é usado por alguns porque não requer dependências do [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") ou [KDE](/index.php/KDE "KDE") e pode ajudar a criar um sistema leve para usuários que gostam de usar desktops leve como [Xfce](/index.php/Xfce "Xfce"), [Openbox](/index.php/Openbox "Openbox"), e [Fluxbox](/index.php/Fluxbox_(Portugu%C3%AAs) "Fluxbox (Português)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Configuração](#Configuração)
    *   [2.1 Habilitando o SLIM](#Habilitando_o_SLIM)
    *   [2.2 Único ambiente gráfico](#Único_ambiente_gráfico)
    *   [2.3 Login automático](#Login_automático)
    *   [2.4 Múltiplos ambientes gráficos](#Múltiplos_ambientes_gráficos)
    *   [2.5 Temas](#Temas)
        *   [2.5.1 Configuração em tela dupla](#Configuração_em_tela_dupla)
*   [3 Outras opções](#Outras_opções)
    *   [3.1 Modificando o Cursor](#Modificando_o_Cursor)
    *   [3.2 Compartilhando o papel de parede do SLiM e da Área de trabalho](#Compartilhando_o_papel_de_parede_do_SLiM_e_da_Área_de_trabalho)
    *   [3.3 Desligar, reiniciar, suspender, sair, executar um terminal no SLiM](#Desligar,_reiniciar,_suspender,_sair,_executar_um_terminal_no_SLiM)
    *   [3.4 Erro de inicialização do SLiM com o daemon rc.d](#Erro_de_inicialização_do_SLiM_com_o_daemon_rc.d)
    *   [3.5 Erro de Desligar com Splashy](#Erro_de_Desligar_com_Splashy)
    *   [3.6 Informações de login com o SLiM](#Informações_de_login_com_o_SLiM)
    *   [3.7 SLiM e o Keyring do Gnome](#SLiM_e_o_Keyring_do_Gnome)
    *   [3.8 Configurando o DPI com o SLiM](#Configurando_o_DPI_com_o_SLiM)
    *   [3.9 Usando um tema aleatório](#Usando_um_tema_aleatório)
*   [4 Todas as opções do SLIM](#Todas_as_opções_do_SLIM)
*   [5 Fontes](#Fontes)

## Instalação

Instale o SLIM do repositório **extra**:

```
# pacman -S slim

```

## Configuração

### Habilitando o SLIM

O SLiM pode ser carregado na inicialização adicionando sua entrada no daemons em `rc.conf` ou modificando o arquivo `inittab`. Veja a página [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição") para obter instruções detalhadas.

### Único ambiente gráfico

Para configurar o SLiM para carregar um ambiente em particular, edite seu [~/.xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)") para carregar seu ambiente de desktop:

```
#!/bin/sh

#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

exec [comando-da-seção]

```

Substitua `[comando-da-seção]` com o comando de seção apropriado. Veja alguns exemplos de diferentes comandos de inicialização de desktops:

```
exec awesome
exec dwm
exec fluxbox
exec fvwm2
exec gnome-session
exec openbox-session
exec startkde
exec startlxde
exec startxfce4
exec enlightenment_start

```

Se o seu ambiente não estiver listado aqui, consulte a página do Wiki apropriada.

### Login automático

Para fazer com que o SLiM faça login automaticamente como um usuário em especifico (sem ter que digitar uma senha). as seguintes linhas em /etc/slim.conf devem ser modificadas.

```
# default_user        simone

```

Remova o comentário dessa linha, e altere "simone" para o nome do usuário que irá fazer login automaticamente:

```
# auto_login          no

```

Remova o comentário dessa linha e altere 'no' para 'yes' ('sim' para 'não'). Isto irá habilitar o recurso de login automático.

### Múltiplos ambientes gráficos

Para ter a possibilidade de escolher múltiplos ambientes gráficos, o SLiM pode ser configurado para fazer login em qualquer ambiente gráfico que você deseja escolher.

Coloque uma declaração similar a este em seu arquivo `~/.xinitrc` e edite a variável sessions em `/etc/slim.conf` para corresponder com os nomes que liga essa declaração. Você pode escolher a seção no momento do login pressionando F1\. Note que este recurso é experimental.

```
# As seguintes variáveis definem a seção que será inicializada se o usuário explicitamente não selecionar uma seção
# Fonte: http://svn.berlios.de/svnroot/repos/slim/trunk/xinitrc.sample

DEFAULT_SESSION=twm

case $1 in
kde)
	exec startkde
	;;
xfce4)
	exec startxfce4
	;;
icewm)
	icewmbg &
	icewmtray &
	exec icewm
	;;
wmaker)
	exec wmaker
	;;
blackbox)
	exec blackbox
	;;
*)
	exec $DEFAULT_SESSION
	;;
esac

```

### Temas

Instale o pacote de temas [slim-themes](https://www.archlinux.org/packages/?name=slim-themes):

```
# pacman -S slim-themes archlinux-themes-slim

```

Os pacotes [archlinux-themes-slim](https://www.archlinux.org/packages/?name=archlinux-themes-slim) contem diferentes temas diversos. Veja o diretório `/usr/share/slim/themes` para acessar os temas disponíveis. Digite o nome do tema na linha 'current_theme' no arquivo `/etc/slim.conf`:

```
#current_theme       default
current_theme       archlinux-simplyblack

```

Para visualizar o tema, execute o seguinte quando uma instância do servidor Xorg estiver em execução:

```
$ slim -p /usr/share/slim/themes/<nome do tema>

```

Para fechar, digite "exit" na linha Login e pressione Enter.

Pacotes de temas adicionais podem ser encontrados no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)").

#### Configuração em tela dupla

Você pode personalizar o tema do slim em /usr/share/slim/themes/<seu tema>/slim.theme para transformar esses valores em porcentagem. Esta caixa possui as dimensões de 450 px por 250 px:

```
input_panel_x           50%
input_panel_y           50%

```

em valores de pixels:

```
# Estas configurações colocam o painel do tema "archlinux-simplyblack" no centro de uma tela de 1440x900:
input_panel_x           495
input_panel_y           325

```

```
# Estas configurações colocam o painel do tema "archlinux-simplyblack" no centro de uma tela de 1680x1050:
input_panel_x           615
input_panel_y           400

```

Se o seu tema possui uma imagem de fundo, você precisa usar a configuração background_style ('stretch', 'tile', 'center' ou 'color') para exibir a imagem corretamente. Dê uma olhada na [documentação oficial que é muito simples e clara sobre os temas do slim](http://slim.berlios.de/themes_howto.php) para maiores detalhes.

## Outras opções

Algumas coisas que você poderia gostar de tentar.

### Modificando o Cursor

Se você deseja modificar o cursor padrão do X para um novo estilo, o pacote [slim-cursor](https://aur.archlinux.org/packages/slim-cursor/) está disponível.

Após a instalação, edite o arquivo `/etc/slim.conf` e comente a linha:

```
cursor   left_ptr

```

Ao invés disso isso irá lhe dar uma seta normal. Esta configuração está após `xsetroot -cursor_name`. Você pode verificar os possíveis nomes de cursor [aqui](http://cvsweb.xfree86.org/cvsweb/*checkout*/xc/lib/X11/cursorfont.h?rev=HEAD&content-type=text/plain) ou em `/usr/share/icons/<your-cursor-theme>/cursors/`.

Para modificar o tema do cursor que será usado na tela de login, crie um arquivo chamado index.theme em `/usr/share/icons/default/index.theme` com este conteúdo:

```
[Icon Theme]
Inherits=<o-tema-do-seu-cursor>

```

Substitua <o-tema-do-seu-cursor> com o nome do tema do cursor que você deseja usar (ex: whiteglass).

### Compartilhando o papel de parede do SLiM e da Área de trabalho

Para compartilhar o papal de parede do SLiM e de sua área de trabalho, modifique o nome do papel de parede do tema, e então crie um link do arquivo de papel de parede de sua área de trabalho para o tema padrão do SLiM:

```
# mv /usr/share/slim/themes/default/background.jpg{,.bck}
# ln -s /path/to/mywallpaper.jpg /usr/share/slim/themes/default/background.jpg

```

### Desligar, reiniciar, suspender, sair, executar um terminal no SLiM

Talvez você queira desligar, reiniciar, suspender, sair ou até mesmo executar um terminal na tela de login do SLiM. Para fazer isso, use os valores no campo username e a senha root no campo password:

*   Para executar um terminal, digite **console** como um nome de usuário (padrões para o xterm podem ser instaladas separadamente... edite `/etc/slim.conf` para modificar as preferências do terminal)
*   Para desligar, digite **halt** como um nome de usuário
*   Para reiniciar, digite **reboot** como um nome de usuário
*   Para sair para o bash, digite **exit** como um nome de usuário
*   Para suspender, digite **suspend** como um nome de usuário (suspender está desabilitado por padrão, edite o arquivo `/etc/slim.conf` como root para remover o comentário da linha `suspend_cmd`, e se for necessário você pode modificar o comando suspend (ex. altere `/usr/sbin/suspend` para `sudo /usr/sbin/pm-suspend`))

### Erro de inicialização do SLiM com o daemon rc.d

Se você inicializa o SLiM com o arquivo `/etc/rc.conf` usando a entrada DAEMONS e ele falha para inicializar, é provável que seja um problema em um arquivo lock. O SLiM cria um arquivo lock em `/var/lock` em cada inicialização, porém, na maioria dos casos o diretório lock em /var não existe, prevenindo que o SLiM inicialize. Verifique para ter certeza se `/var/lock` existe, se não existir, você pode criá-lo digitando o seguinte:

```
# mkdir /var/lock/

```

### Erro de Desligar com Splashy

Se você usa o Splashy e o SLiM, algumas vezes você não consegue desligar ou reiniciar pelo menu do GNOME, Xfce, LXDE ou outros. Verifique seu `/etc/slim.conf` e `/etc/splash.conf`; Defina DEFAULT_TTY=7 o mesmo como xserver_arguments vt07.

### Informações de login com o SLiM

Por padrão, o SLiM falha em registrar logins (quem, último, etc.) para utmp e wtmp, relatando de forma incorreta as informações de login. Para resolver isso, edite seu `slim.conf` como a seguir:

```
 sessionstart_cmd    /usr/bin/sessreg -a -l $DISPLAY %user
 sessionstop_cmd     /usr/bin/sessreg -d -l $DISPLAY %user

```

### SLiM e o Keyring do Gnome

Se você está usando o SLiM para executar uma seção do Gnome e está tendo problemas para acessar seu keyring, por exemplo, não ser automaticamente autenticado no login, adicione as seguintes linhas para o seu /etc/pam.d/slim (como discutido [aqui](https://bugs.archlinux.org/task/18637)).

```
auth		optional	pam_gnome_keyring.so
session		optional	pam_gnome_keyring.so	auto_start

```

Porém, essa solução não funciona com o Gnome 2.30\. Uma alternativa para contornar o problema está descrito [aqui](https://bugs.archlinux.org/task/18930). Modificando a linha login_cmd em /etc/slim.conf:

```
login_cmd exec /bin/bash -login ~/.xinitrc %session >~/.xsession-errors 2>&1

```

### Configurando o DPI com o SLiM

O servidor Xorg geralmente carrega o DPI, mas se não funcionar para você, você pode especificar para o SLiM. Se você definir o DPI com o argumento -dpi 96 em `/etc/X11/xinit/xserverrc` não irá funcionar com o SLiM. Para resolver isso, edite seu `slim.conf` de:

```
 xserver_arguments   -nolisten tcp vt07 

```

para

```
 xserver_arguments   -nolisten tcp vt07 -dpi 96

```

### Usando um tema aleatório

Use a variável current_theme como uma lista separada por vírgulas para especificar um conjunto de temas para ser aleatoriamente escolhido.

## Todas as opções do SLIM

Esta é uma lista de todas as opções de configuração do slim e os seus valores padrões.

**Nota:** welcome_msg permite 2 variáveis **%host** e **%domain**
sessionstart_cmd allows **%user** *(execd right before login_cmd)* e também é permitido em sessionstop_cmd
login_cmd permite **%session** e **%theme**

| Nome da Opção | Valor padrão |
| default_path | <tt>/bin:/usr/bin:/usr/local/bin</tt> |
| default_xserver | <tt>/usr/bin/X</tt> |
| xserver_arguments | <tt>vt07 -auth /var/run/slim.auth</tt> |
| numlock |
| daemon | <tt>yes</tt> |
| xauth_path | <tt>/usr/bin/xauth</tt> |
| login_cmd | <tt>exec /bin/bash -login ~/.xinitrc %session</tt> |
| halt_cmd | <tt>/sbin/shutdown -h now</tt> |
| reboot_cmd | <tt>/sbin/shutdown -r now</tt> |
| suspend_cmd |
| sessionstart_cmd |
| sessionstop_cmd |
| console_cmd | <tt>/usr/bin/xterm -C -fg white -bg black +sb -g %dx%d+%d+%d -fn %dx%d -T</tt> |
| screenshot_cmd | <tt>import -window root /slim.png</tt> |
| welcome_msg | <tt>Welcome to %host</tt> |
| session_msg | <tt>Session:</tt> |
| default_user |
| focus_password | <tt>no</tt> |
| auto_login | <tt>no</tt> |
| current_theme | <tt>default</tt> |
| lockfile | <tt>/var/run/slim.lock</tt> |
| logfile | <tt>/var/log/slim.log</tt> |
| authfile | <tt>/var/run/slim.auth</tt> |
| shutdown_msg | <tt>The system is halting...</tt> |
| reboot_msg | <tt>The system is rebooting...</tt> |
| sessions | <tt>wmaker,blackbox,icewm</tt> |
| sessiondir |
| hidecursor | <tt>false</tt> |
| input_panel_x | <tt>50%</tt> |
| input_panel_y | <tt>40%</tt> |
| input_name_x | <tt>200</tt> |
| input_name_y | <tt>154</tt> |
| input_pass_x | <tt>-1</tt> |
| input_pass_y | <tt>-1</tt> |
| input_font | <tt>Verdana:size=11</tt> |
| input_color | <tt>#000000</tt> |
| input_cursor_height | <tt>20</tt> |
| input_maxlength_name | <tt>20</tt> |
| input_maxlength_passwd | <tt>20</tt> |
| input_shadow_xoffset | <tt>0</tt> |
| input_shadow_yoffset | <tt>0</tt> |
| input_shadow_color | <tt>#FFFFFF</tt> |
| welcome_font | <tt>Verdana:size=14</tt> |
| welcome_color | <tt>#FFFFFF</tt> |
| welcome_x | <tt>-1</tt> |
| welcome_y | <tt>-1</tt> |
| welcome_shadow_xoffset | <tt>0</tt> |
| welcome_shadow_yoffset | <tt>0</tt> |
| welcome_shadow_color | <tt>#FFFFFF</tt> |
| intro_msg |
| intro_font | <tt>Verdana:size=14</tt> |
| intro_color | <tt>#FFFFFF</tt> |
| intro_x | <tt>-1</tt> |
| intro_y | <tt>-1</tt> |
| background_style | <tt>stretch</tt> |
| background_color | <tt>#CCCCCC</tt> |
| username_font | <tt>Verdana:size=12</tt> |
| username_color | <tt>#FFFFFF</tt> |
| username_x | <tt>-1</tt> |
| username_y | <tt>-1</tt> |
| username_msg | <tt>Please enter your username</tt> |
| username_shadow_xoffset | <tt>0</tt> |
| username_shadow_yoffset | <tt>0</tt> |
| username_shadow_color | <tt>#FFFFFF</tt> |
| password_x | <tt>-1</tt> |
| password_y | <tt>-1</tt> |
| password_msg | <tt>Please enter your password</tt> |
| msg_color | <tt>#FFFFFF</tt> |
| msg_font | <tt>Verdana:size=16:bold</tt> |
| msg_x | <tt>40</tt> |
| msg_y | <tt>40</tt> |
| msg_shadow_xoffset | <tt>0</tt> |
| msg_shadow_yoffset | <tt>0</tt> |
| msg_shadow_color | <tt>#FFFFFF</tt> |
| session_color | <tt>#FFFFFF</tt> |
| session_font | <tt>Verdana:size=16:bold</tt> |
| session_x | <tt>50%</tt> |
| session_y | <tt>90%</tt> |
| session_shadow_xoffset | <tt>0</tt> |
| session_shadow_yoffset | <tt>0</tt> |
| session_shadow_color | <tt>#FFFFFF</tt> |

## Fontes

*   [Página do SLiM](http://slim.berlios.de/)
*   [Documentação do SLiM](http://slim.berlios.de/manual.php)