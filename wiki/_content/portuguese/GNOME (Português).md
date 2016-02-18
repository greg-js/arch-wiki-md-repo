| **Summary**  |
| GNOME 3 provê um ambiente moderno, reescrito do zero, usando o GTK3+ toolkit. |
| **Overview** |
| The [Xorg](/index.php/Xorg "Xorg") project provides an open source implementation of the X Window System – the foundation for a graphical user interface. [Desktop environments](/index.php/Desktop_environment "Desktop environment") such as [Enlightenment](/index.php/Enlightenment "Enlightenment"), [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE"), and [Xfce](/index.php/Xfce "Xfce") provide a complete graphical environment. Various [window managers](/index.php/Window_manager "Window manager") offer alternative and novel environments, and may be used *standalone* to conserve system resources. [Display managers](/index.php/Display_manager "Display manager") provide a graphical login prompt. |

Para o GNOME 3, os desenvolvedores começaram do zero e criaram um novo complemento, um ambiente de trabalho moderno para os usuários e as tecnologias recentes. Algumas das características implementadas:

*   Novo tema e visual, bem como fontes modernas.
*   O modo de visualização das atividades fornece uma maneira mais fácil de acessar janelas e aplicativos.
*   Recurso de pesquisa rápida (entre configurações, programas e arquivos) junto à visualização de atividades.
*   Um novo aplicativo de Configuração do Sistema.
*   Sistema de notificação mais sutil e um painel mais discreto.
*   Serviço de mensagens integrado.
*   E muito mais recursos: window tiling (semelhante ao Aero Snap), gerenciador de arquivos Nautilus aperfeiçoado etc.

[mais detalhes no site do [GNOME 3](http://www.gnome3.org/)]

## Contents

*   [1 Introdução](#Introdu.C3.A7.C3.A3o)
*   [2 Atualização do GNOME 2.32 atual](#Atualiza.C3.A7.C3.A3o_do_GNOME_2.32_atual)
*   [3 Instalação do GNOME 3 como novo ambiente de trabalho](#Instala.C3.A7.C3.A3o_do_GNOME_3_como_novo_ambiente_de_trabalho)
    *   [3.1 Daemons e modulos necessários ao GNOME](#Daemons_e_modulos_necess.C3.A1rios_ao_GNOME)
    *   [3.2 Executando o GNOME](#Executando_o_GNOME)
*   [4 Usando o shell](#Usando_o_shell)
*   [5 Customizando](#Customizando)
    *   [5.1 Usando Gnome-tweak-tool](#Usando_Gnome-tweak-tool)
        *   [5.1.1 Wallpaper](#Wallpaper)
        *   [5.1.2 Desligar Som](#Desligar_Som)
        *   [5.1.3 Alterar o layout do teclado no GDM](#Alterar_o_layout_do_teclado_no_GDM)
    *   [5.2 Alterando o GTK3 usando o tema settings.ini](#Alterando_o_GTK3_usando_o_tema_settings.ini)
    *   [5.3 Redimensionar a barra de título Massive](#Redimensionar_a_barra_de_t.C3.ADtulo_Massive)
    *   [5.4 Configurando tema para o ícone](#Configurando_tema_para_o_.C3.ADcone)

## Introdução

O GNOME 3 vem com **duas** interfaces, **gnome-shell**, o novo layout padrão, e o modo **fallback**. *Gnome-session* detectará se o computador é capaz de rodar o *gnome-shell*, do contrário iniciará no modo *fallback*.

O modo **fallback** é muito similar ao layout do GNOME 2.x (enquanto usa o gnome-panel e metacity, alternativas ao gnome-shell e Mutter).

Caso esteja no modo fallback, pode-se escolher o gerenciamento de janelas preferido.

## Atualização do GNOME 2.32 atual

**Atenção:** A sessão pode falhar durante a atualização e recomendado que você execute o comando no outra sessão, de outra DE ou VM, ou tty.

```
# pacman -Syu 

```

**Importante**: Apenas o GNOME 3.x modo **falback** estará instalado neste momento. Para instalar o novo shell:

```
# pacman -S gnome-shell

```

## Instalação do GNOME 3 como novo ambiente de trabalho

GNOME 3 está no [extra]. Deve-se executar o seguinte comando para instalá-lo:

```
# pacman -Syu gnome

```

Para adquirir aplicações adicionais:

```
# pacman -Syu gnome-extra

```

### Daemons e modulos necessários ao GNOME

O desktop GNOME requer um daemon o **DBUS** para uma operação adequada.

Para iniciar o DBUS no daemon:

```
# /etc/rc.d/dbus start

```

Ou adicione o **DAEMONS** diretamente no diretório `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` irão iniciar no boot:

```
DAEMONS=(syslog-ng **dbus** network crond)

```

**GVFS** permite protocolos para acesso de arquivos remotos, como FTP ou SMB, para uso em aplicativos diversos como o gerenciandor de arquivos Nautilus. Isso é feito pelo **FUSE**: o espaço virtual no sistema de arquivos na camada de módulos do kernel.

Para carregar o módulo do kernel:

```
# modprobe fuse

```

Ou adicione o módulo em **MODULES** no diretório `/etc/rc.conf` para que sejam iniciado no boot, exemplo:

```
MODULES=(**fuse** usblp)

```

**Nota:** FUSE é um módulo do kernel, não um daemon.

### Executando o GNOME

Para o melhor integrar no desktop **GDM** é recomendado (mas outros gerenciadores de login, tais como SLiM também funcionam consulte a seleção Policykit).

```
# pacman -S gdm

```

Confira o [Display manager](/index.php/Display_manager "Display manager") para iniciá-lo corretamente.

Se você preferir iniciar pelo console, adicione a linha no seu diretório `~/.xinitrc`, certifique-se a última linha e inicia com *exec* (veja [xinitrc](/index.php/Xinitrc "Xinitrc")):

```
exec gnome-session

```

Agora o GNOME inciará quando digitar o comando:

```
$ startx

```

## Usando o shell

Veja [https://live.gnome.org/GnomeShell/CheatSheet](https://live.gnome.org/GnomeShell/CheatSheet)

## Customizando

### Usando Gnome-tweak-tool

```
# pacman -S gnome-tweak-tool

```

Este customização da fonte, themas, o botão minimizar e maximizar e algumas configurações como qual ação é tomada quando é fechado.

Uma boa customização o tutorial é [http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html](http://blog.fpmurphy.com/2011/03/customizing-the-gnome-3-shell.html) que explora a gsettings.

#### Wallpaper

```
$ GSETTINGS_BACKEND=dconf gsettings get org.gnome.desktop.background picture-uri
$ GSETTINGS_BACKEND=dconf gsettings set org.gnome.desktop.background picture-uri "file:///usr/share/backgrounds/gnome/SundownDunes.jpg"

```

Você preicisa apontar para um arquivo onde o usuário gdm para permissão de ler, e não em seu diretório home.

#### Desligar Som

```
$ GSETTINGS_BACKEND=dconf gsettings com org.gnome.desktop.sound event-sounds false

```

Insirá um "1" de volta /etc/shadow para desabilitar o login do usuário gdm.

#### Alterar o layout do teclado no GDM

Desde do GDM 3 a configuração do layout do teclado não importa o gnome, você tem que configurar no Xorg. Veja aqui: [Beginners' guide#Non-US_keyboard](/index.php/Beginners%27_guide#Non-US_keyboard "Beginners' guide")

### Alterando o GTK3 usando o tema settings.ini

Similar para `~/.gtkrc-2.0` GTK2+ é possível definir o GTK3 (Gnome 3) atrávez do tema `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini`. Por default `${XDG_CONFIG_HOME}` é interpretado como `~/.config`.

Apenas o tema Adwaita existe neste momento para gtk3 e é disponível no pacote **gnome-themes-standard**.

Exemplo:

```
 [Configurações]
 gtk-theme-name = Adwaita
 gtk-fallback-icon-theme = gnome
 # next option is applicable only if selected theme supports it
 gtk-application-prefer-dark-theme = true
 # set font name and dimension
 gtk-font-name = Sans 10

```

Pode ser necessário reiniciar o DE ou WM para aplicar as configurações.

**Nota:** Mais opções podem ser encontradas: [GtkSettings documentation](http://developer.gnome.org/gtk3/3.0/GtkSettings.html#GtkSettings.properties)

### Redimensionar a barra de título Massive

```
# sed -i "/title_vertical_pad/s/value=\"[0-9]\{1,2\}\"/value=\"0\"/g" /usr/share/themes/Adwaita/metacity-1/metacity-theme-3.xml

```

`Alt` + `F2` e *reiniciar* seguido de `Enter`

Isso vai alterar o title_vertical_pad para de 14 para 0 colocando mas elegância nas janelas.

Para restaurar as configurações originais:

```
sudo pacman -S gnome-themes-standard

```

### Configurando tema para o ícone

**Nota:** Com o gnome-tweak-tool na versão 3.0.3 e superior, você deve adicionar os temas dos ícones dentro de ~/.icons.

Útil, o Gnome 3 pode usar os ícones do Gnome 2, assim não fica preso no padrão definido. Para isso, você pode copiar o seu ícone preferido para ~/.icons. Exemplo:

```
$ cp -R /home/user/Desktop/my_new_icon_theme ~/.icons

```

The new icon theme 'my_new_icon_theme' will now be selectable using the gnome-tweak-tool (under 'Interface'), otherwise it can be set with no need of gnome-tweak-tool by adding the gtk-icon-theme-name entry inside ${XDG_CONFIG_HOME}/gtk-3.0/settings.ini.

 `${XDG_CONFIG_HOME}/gtk-3.0/settings.ini` 
```
.....
gtk-icon-theme-name = my_new_icon_theme
.....
```