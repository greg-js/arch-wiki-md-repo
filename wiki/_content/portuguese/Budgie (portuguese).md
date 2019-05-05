Artigos relacionados

*   [Desktop environment (Português)](/index.php/Desktop_environment_(Portugu%C3%AAs) "Desktop environment (Português)")
*   [Display manager (Português)](/index.php/Display_manager_(Portugu%C3%AAs) "Display manager (Português)")
*   [Window manager (Português)](/index.php/Window_manager_(Portugu%C3%AAs) "Window manager (Português)")
*   [GTK+ (Português)](/index.php/GTK%2B_(Portugu%C3%AAs) "GTK+ (Português)")

**Status de tradução:** Esse artigo é uma tradução de [Budgie](/index.php/Budgie "Budgie"). Data da última tradução: 2019-05-02\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Budgie&diff=0&oldid=572246) na versão em inglês.

O Budgie é o desktop padrão do Solus Operating System, escrito do zero. Além de um design mais moderno, o Budgie pode emular a aparência da área de trabalho do GNOME 2.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Iniciando](#Iniciando)
*   [3 Uso](#Uso)
*   [4 Configuração](#Configuração)
    *   [4.1 Mudando o botão de layout](#Mudando_o_botão_de_layout)
    *   [4.2 Use um window manager diferente](#Use_um_window_manager_diferente)
*   [5 Veja Também](#Veja_Também)

## Instalação

[Instale](/index.php/Install "Install") o pacote [budgie-desktop](https://www.archlinux.org/packages/?name=budgie-desktop) para a versão estável ou [budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/) para a versão de desenvolvimento. É recomendado instalar suas dependências opcionais também para obter um ambiente de desktop mais completo. É recomendado também instalar o grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/), que contém os aplicativos necessários para a experiência padrão do GNOME.

## Iniciando

Escolha a sessão *Budgie Desktop* de um [gerenciador de exibição](/index.php/Display_manager_(Portugu%C3%AAs) "Display manager (Português)") de sua escolha, ou modifique [xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)") para incluir o Budgie Desktop:

 `~/.xinitrc` 
```
export XDG_CURRENT_DESKTOP=Budgie:GNOME
exec budgie-desktop

```

## Uso

Você pode ver as mensagens de notificação, definir o volume e modificar a aparência da área de trabalho com a barra lateral chamada "Raven". Ele pode ser acessado com a tecla `Super + N` ou clicando no applet Indicador de status.

## Configuração

A configuração do Budgie Desktop é feita através da barra lateral e as alterações nas configurações do sistema são feitas através do [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center)

### Mudando o botão de layout

O layout do botão da janela pode ser alterado usando [dconf](https://www.archlinux.org/packages/?name=dconf), [dconf-editor](https://www.archlinux.org/packages/?name=dconf-editor) ou gsettings.

Por exemplo:

```
gsettings set com.solus-project.budgie-wm button-layout 'close,minimize,maximize:appmenu'
gsettings set com.solus-project.budgie-helper.workarounds fix-button-layout 'close,minimize,maximize:menu'

```

### Use um window manager diferente

É possível usar um [window manager](/index.php/Window_manager_(Portugu%C3%AAs) "Window manager (Português)") alternativo com o Budgie. Defina um [Sessão GNOME personalizada](/index.php/GNOME/Tips_and_tricks#Custom_GNOME_sessions "GNOME/Tips and tricks") que substitua *budgie-wm* por outro window manager ou [autostart](/index.php/GNOME_(Portugu%C3%AAs)#Inicialização_automática "GNOME (Português)") `*my -wm* --replace` onde *my-wm* é o nome do executável do gerenciador de janelas que você deseja usar.

## Veja Também

*   [Wikipedia:Budgie (desktop environment)](https://en.wikipedia.org/wiki/Budgie_(desktop_environment) "wikipedia:Budgie (desktop environment)")
*   [Site oficial do Budgie Desktop](https://budgie-desktop.org/)
*   [Repositório git oficial para o desenvolvimento do Solus](https://git.solus-project.com/)
*   [Status dos projetos do Solus](https://build.solus-project.com/)