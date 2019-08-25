**Status de tradução:** Esse artigo é uma tradução de [Display manager](/index.php/Display_manager "Display manager"). Data da última tradução: 2019-06-19\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Display_manager&diff=0&oldid=572750) na versão em inglês.

Artigos relacionados

*   [Iniciar X no login](/index.php/Iniciar_X_no_login "Iniciar X no login")

Um [gerenciador de exibição](https://en.wikipedia.org/wiki/X_display_manager_(program_type) "wikipedia:X display manager (program type)"), ou gerenciador de login, é tipicamente uma interface gráfica de usuário que é exibida no final do processo de inicialização no lugar do shell padrão. Há várias implementações de gerenciadores de exibição, assim como existem vários tipos de [gerenciadores de janela](/index.php/Gerenciadores_de_janela "Gerenciadores de janela") e [ambientes de desktop](/index.php/Ambientes_de_desktop "Ambientes de desktop"). Geralmente, há uma certa quantidade de personalização e mudança de tema disponível com cada um.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Lista de gerenciadores de exibição](#Lista_de_gerenciadores_de_exibição)
    *   [1.1 Console](#Console)
    *   [1.2 Gráficos](#Gráficos)
*   [2 Carregando o gerenciador de exibição](#Carregando_o_gerenciador_de_exibição)
    *   [2.1 Usando systemd-logind](#Usando_systemd-logind)
*   [3 Configuração de sessão](#Configuração_de_sessão)
    *   [3.1 Executar ~/.xinitrc como uma sessão](#Executar_~/.xinitrc_como_uma_sessão)
    *   [3.2 Iniciando aplicativos sem um gerenciador de janela](#Iniciando_aplicativos_sem_um_gerenciador_de_janela)
*   [4 Dicas e truques](#Dicas_e_truques)
    *   [4.1 Iniciando automaticamente](#Iniciando_automaticamente)
    *   [4.2 Definir o idioma para sessão de usuário](#Definir_o_idioma_para_sessão_de_usuário)

## Lista de gerenciadores de exibição

### Console

*   **[CDM](/index.php/CDM "CDM")** — ultra-minimalista, ainda gerenciador de login completo escrito em bash

	[https://github.com/ghost1227/cdm](https://github.com/ghost1227/cdm) || [cdm-git](https://aur.archlinux.org/packages/cdm-git/)

*   **[Console TDM](/index.php/Console_TDM "Console TDM")** — Extensão para *xinit* escrita em puro Bash.

	[https://github.com/dopsi/console-tdm](https://github.com/dopsi/console-tdm) || [console-tdm](https://aur.archlinux.org/packages/console-tdm/)

*   **[nodm](/index.php/Nodm "Nodm")** — Gerenciador de exibição minimalista para logins automáticos.

	[https://github.com/spanezz/nodm](https://github.com/spanezz/nodm) || [nodm](https://www.archlinux.org/packages/?name=nodm) – [sem mantenedor desde 2018-10](https://github.com/spanezz/nodm/issues/8)

*   **[Ly](/index.php/Ly "Ly")** — Gerenciador de exibição experimental para ncurses.

	[https://github.com/cylgom/ly](https://github.com/cylgom/ly) || [ly-git](https://aur.archlinux.org/packages/ly-git/)

*   **tbsm** — Uma sessão bash ou lançador de aplicativos, com suporte a sessões X e Wayland.

	[https://loh-tar.github.io/tbsm/](https://loh-tar.github.io/tbsm/) || [tbsm](https://aur.archlinux.org/packages/tbsm/)

### Gráficos

*   **[GDM](/index.php/GDM_(Portugu%C3%AAs) "GDM (Português)")** — Gerenciador de exibição do [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)").

	[https://wiki.gnome.org/Projects/GDM](https://wiki.gnome.org/Projects/GDM) || [gdm](https://www.archlinux.org/packages/?name=gdm)

*   **[LightDM](/index.php/LightDM "LightDM")** — Gerente de exibição para vários desktops, pode usar vários front-ends escritos em qualquer kit de ferramentas.

	[https://github.com/CanonicalLtd/lightdm/](https://github.com/CanonicalLtd/lightdm/) || [lightdm](https://www.archlinux.org/packages/?name=lightdm)

*   **[LXDM](/index.php/LXDM "LXDM")** — Gerenciador de exibição do [LXDE](/index.php/LXDE "LXDE"). Pode ser usado independentemente do ambiente de desktop LXDE.

	[https://sourceforge.net/projects/lxdm/](https://sourceforge.net/projects/lxdm/) || [lxdm](https://www.archlinux.org/packages/?name=lxdm)

*   **[SDDM](/index.php/SDDM "SDDM")** — Gerenciador de exibição baseado no QML e sucessor do KDM; recomendado para [Plasma](/index.php/Plasma_(Portugu%C3%AAs) "Plasma (Português)") e [LXQt](/index.php/LXQt "LXQt").

	[https://github.com/sddm/sddm](https://github.com/sddm/sddm) || [sddm](https://www.archlinux.org/packages/?name=sddm)

*   **[XDM](/index.php/XDM_(Portugu%C3%AAs) "XDM (Português)")** — Gerenciador de exibição X com suporte a XDMCP, seletor de host.

	[xdm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xdm.8) || [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm)

## Carregando o gerenciador de exibição

Para ativar o login gráfico, [habilite](/index.php/Habilite "Habilite") o serviço systemd apropriado. Por exemplo, para [SDDM](/index.php/SDDM "SDDM"), habilite `sddm.service`.

Isso deve funcionar sem configurações extras. Caso contrário, talvez seja necessário redefinir um link simbólico personalizado `default.target` para apontar para o `graphical.target` padrão. Veja [systemd (Português)#Alterar target padrão para inicializar](/index.php/Systemd_(Portugu%C3%AAs)#Alterar_target_padrão_para_inicializar "Systemd (Português)").

Depois de habilitar o [SDDM](/index.php/SDDM "SDDM"), um link simbólico `display-manager.service` deve ser configurado em `/etc/systemd/system/`. Você pode precisar usar `--force` para substituir os links simbólicos antigos.

 `$ file /etc/systemd/system/display-manager.service` 
```
/etc/systemd/system/display-manager.service: symbolic link to /usr/lib/systemd/system/sddm.service

```

### Usando systemd-logind

Para verificar o status da sua sessão de usuário, você pode usar o *loginctl*. Todas as ações do [polkit](/index.php/Polkit "Polkit"), como suspender o sistema ou montar unidades externas, funcionarão imediatamente.

```
$ loginctl show-session $XDG_SESSION_ID

```

## Configuração de sessão

Muitos gerenciadores de exibição leem sessões disponíveis do diretório `/usr/share/xsessions/`. Ele contém [arquivos de entrada de desktop](https://specifications.freedesktop.org/desktop-entry-spec/latest/) padrão para cada DM/WM.

Para adicionar/remover entradas à sua lista de sessões do gerenciador de exibição; crie/remova os arquivos *.desktop* em `/usr/share/xsessions/` conforme desejado. Um arquivo *.desktop* comum se parecerá com:

```
[Desktop Entry]
Name=Openbox
Comment=Log in using the Openbox window manager (without a session manager)
Exec=/usr/bin/openbox-session
TryExec=/usr/bin/openbox-session
Icon=openbox.png
Type=Application

```

### Executar ~/.xinitrc como uma sessão

Instalar [xinit-xsession](https://aur.archlinux.org/packages/xinit-xsession/) vai fornecer uma opção para executar seu [xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)") como uma sessão. Basta definir `xinitrc` como a sessão nas configurações do gerenciador de exibição e se certificar de que o arquivo `~/.xinitrc` é um executável.

### Iniciando aplicativos sem um gerenciador de janela

Você também pode iniciar um aplicativo sem qualquer gerenciamento de janela, área de trabalho ou de decoração. Por exemplo, para iniciar o [google-chrome](https://aur.archlinux.org/packages/google-chrome/) crie um arquivo `web-browser.desktop` em `/usr/share/xsessions/` desta forma:

```
[Desktop Entry]
Name=Web Browser
Comment=Use a web browser as your session
Exec=/usr/bin/google-chrome --auto-launch-at-startup
TryExec=/usr/bin/google-chrome --auto-launch-at-startup
Icon=google-chrome
Type=Application

```

Nesse caso, quando você fizer o login, o aplicativo configurado com `Exec` será iniciado imediatamente. Quando você fechar o aplicativo, você será levado de volta ao gerenciador de login (o mesmo que fazer logout de um DE/WM normal).

É importante lembrar que a maioria dos aplicativos gráficos não é destinada a ser iniciada dessa forma e você pode ter ajustes manuais para fazer ou limitações para viver com (não há gerenciador de janela, portanto, não espere conseguir mover ou redimensionar *qualquer* janela, incluindo diálogos; no entanto, você pode ser capaz de definir a geometria da janela nos arquivos de configuração do aplicativo).

Veja também [#Inicializando aplicativos sem um gerenciador de janela](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)").

## Dicas e truques

### Iniciando automaticamente

A maioria dos gerenciadores de exibição carregam `/etc/xprofile`, `~/.xprofile` e `/etc/X11/xinit/xinitrc.d/`. Para mais detalhes, veja [xprofile](/index.php/Xprofile_(Portugu%C3%AAs) "Xprofile (Português)").

### Definir o idioma para sessão de usuário

Para gerenciadores de exibição que usam [AccountsService](https://freedesktop.org/wiki/Software/AccountsService/) o [locale](/index.php/Locale_(Portugu%C3%AAs) "Locale (Português)") para a sessão de usuário pode ser definido editando: `/var/lib/AccountsService/users/$USER` 
```
[User]
Language=*seu_locale*
```

sendo *seu_locale* um valor como `pt_BR.UTF-8`.

Faça logout e, então, volte novamente para as alterações terem efeito.