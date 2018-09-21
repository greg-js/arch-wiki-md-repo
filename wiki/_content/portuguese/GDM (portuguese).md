**Status de tradução:** Esse artigo é uma tradução de [GDM](/index.php/GDM "GDM"). Data da última tradução: 2018-09-20\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=GDM&diff=0&oldid=540366) na versão em inglês.

Artigos relacionados

*   [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)")
*   [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição")

Do [GDM - GNOME Display Manager](https://wiki.gnome.org/Projects/GDM): "O GNOME Display Manager (GDM) é um programa que gerencia servidores gráficos de exibição e lida com logins de usuários gráficos."

[Gerenciadores de exibição](/index.php/Gerenciadores_de_exibi%C3%A7%C3%A3o "Gerenciadores de exibição") fornecem a usuários de [X Window System](/index.php/X_Window_System_(Portugu%C3%AAs) "X Window System (Português)") e [Wayland](/index.php/Wayland "Wayland") com um prompt de login gráfico.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Inicialização](#Inicializa.C3.A7.C3.A3o)
    *   [2.1 Inicializando aplicativos automaticamente](#Inicializando_aplicativos_automaticamente)
*   [3 Configuração](#Configura.C3.A7.C3.A3o)
    *   [3.1 Imagem de plano de fundo na tela de autenticação](#Imagem_de_plano_de_fundo_na_tela_de_autentica.C3.A7.C3.A3o)
    *   [3.2 Configuração no DConf](#Configura.C3.A7.C3.A3o_no_DConf)
        *   [3.2.1 Logo da tela de autenticação](#Logo_da_tela_de_autentica.C3.A7.C3.A3o)
        *   [3.2.2 Alterando o tema do cursor](#Alterando_o_tema_do_cursor)
        *   [3.2.3 Fonte maior para a tela de autenticação](#Fonte_maior_para_a_tela_de_autentica.C3.A7.C3.A3o)
        *   [3.2.4 Desligando o som](#Desligando_o_som)
        *   [3.2.5 Configurando o comportamento do botão de energia](#Configurando_o_comportamento_do_bot.C3.A3o_de_energia)
        *   [3.2.6 Habilitando tap-to-click](#Habilitando_tap-to-click)
        *   [3.2.7 Desabilitar/Habilitar o menu de acessibilidade](#Desabilitar.2FHabilitar_o_menu_de_acessibilidade)
    *   [3.3 Layout do teclado](#Layout_do_teclado)
    *   [3.4 Alterar o idioma](#Alterar_o_idioma)
    *   [3.5 Usuários e autenticação](#Usu.C3.A1rios_e_autentica.C3.A7.C3.A3o)
        *   [3.5.1 Autenticação automática](#Autentica.C3.A7.C3.A3o_autom.C3.A1tica)
        *   [3.5.2 Autenticação sem senha](#Autentica.C3.A7.C3.A3o_sem_senha)
        *   [3.5.3 Desligamento sem senha para várias sessões](#Desligamento_sem_senha_para_v.C3.A1rias_sess.C3.B5es)
        *   [3.5.4 Habilitar autenticação como root no GDM](#Habilitar_autentica.C3.A7.C3.A3o_como_root_no_GDM)
        *   [3.5.5 Ocultar usuário da lista de login](#Ocultar_usu.C3.A1rio_da_lista_de_login)
    *   [3.6 Definir as configurações de monitor padrão](#Definir_as_configura.C3.A7.C3.B5es_de_monitor_padr.C3.A3o)
    *   [3.7 Configurar permissão de acesso do servidor X](#Configurar_permiss.C3.A3o_de_acesso_do_servidor_X)
*   [4 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [4.1 Falha ao usar driver proprietários da NVIDIA](#Falha_ao_usar_driver_propriet.C3.A1rios_da_NVIDIA)
    *   [4.2 Falha no encerramento da sessão](#Falha_no_encerramento_da_sess.C3.A3o)
    *   [4.3 Xorg sem senha](#Xorg_sem_senha)
    *   [4.4 Usar backend do Xorg](#Usar_backend_do_Xorg)
    *   [4.5 Remoção incompleta do gdm](#Remo.C3.A7.C3.A3o_incompleta_do_gdm)
    *   [4.6 Suspensão automática do GDM (GNOME 3.28)](#Suspens.C3.A3o_autom.C3.A1tica_do_GDM_.28GNOME_3.28.29)
*   [5 Veja também](#Veja_tamb.C3.A9m)

## Instalação

GDM pode ser [instalado](/index.php/Instala "Instala") com o pacote [gdm](https://www.archlinux.org/packages/?name=gdm) e é instalado como parte do grupo [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

Se você preferir usar o GDM legado que foi usado no GNOME 2 e possui seu próprio utilitário de configuração, instale o pacote [gdm-old](https://aur.archlinux.org/packages/gdm-old/). Observe que o restante deste artigo discute o GDM atual, não o GDM legado, a menos que indicado de outra forma.

Você também pode querer instalar o seguinte:

*   **gdm3setup** — Uma interface para configurar GDM3, opções de autologin e alterar o tema de Shell

	[https://github.com/Nano77/gdm3setup](https://github.com/Nano77/gdm3setup) || [gdm3setup-utils](https://aur.archlinux.org/packages/gdm3setup-utils/)

## Inicialização

Para iniciar o GDM na inicialização do sistema, [habilite](/index.php/Habilite "Habilite") `gdm.service`.

### Inicializando aplicativos automaticamente

Pode-se querer iniciar automaticamente certos comandos, como *xrandr*, por exemplo, quanto da auttenticaçaõ. Isso pode ser obtido adicionando um comando ou script a um local originado pelo gerenciador de exibição. Consulte [Gerenciador de exibição#Iniciando automaticamente](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o#Iniciando_automaticamente "Gerenciador de exibição") para uma lista de locais suportados.

**Nota:** O diretório `/etc/gdm/Init` não é mais uma localização válida, veja [[1]](https://bugzilla.gnome.org/show_bug.cgi?id=751602#c2).

## Configuração

### Imagem de plano de fundo na tela de autenticação

**Nota:**

*   Desde o GNOME 3.16, temas do GNOME Shell estão sendo armazenados como arquivos binários (gresource).
*   Essa alteração será substituída em atualizações subsequentes do [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell).

Em primeiro lugar, você precisa extrair o tema existente do GNOME Shell para uma pasta em seu diretório pessoal. Você pode fazer isso usando o seguinte script:

 `extractgst.sh` 
```
#!/bin/sh
gst=/usr/share/gnome-shell/gnome-shell-theme.gresource
workdir=${HOME}/shell-theme

for r in `gresource list $gst`; do
	r=${r#\/org\/gnome\/shell/}
	if [ ! -d $workdir/${r%/*} ]; then
	  mkdir -p $workdir/${r%/*}
	fi
done

for r in `gresource list $gst`; do
        gresource extract $gst $r >$workdir/${r#\/org\/gnome\/shell/}
done
```

Navegue até o diretório criado. Você deve descobrir que os arquivos de tema foram extraídos para ele. Agora copie sua imagem de fundo preferida para este diretório.

Em seguida, você precisa criar um arquivo no diretório com o seguinte conteúdo:

 `gnome-shell-theme.gresource.xml` 
```
<?xml version="1.0" encoding="UTF-8"?>
<gresources>
  <gresource prefix="/org/gnome/shell/theme">
    <file>calendar-arrow-left.svg</file>
    <file>calendar-arrow-right.svg</file>
    <file>calendar-today.svg</file>
    <file>checkbox.svg</file>
    <file>checkbox-focused.svg</file>
    <file>checkbox-off.svg</file>
    <file>checkbox-off-focused.svg</file>
    <file>close-window.svg</file>
    <file>close-window-active.svg</file>
    <file>close-window-hover.svg</file>
    <file>corner-ripple-ltr.png</file>
    <file>corner-ripple-rtl.png</file>
    <file>dash-placeholder.svg</file>
    <file>gnome-shell.css</file>
    <file>gnome-shell-high-contrast.css</file>
    <file>icons/message-indicator-symbolic.svg</file>
    <file>key-enter.svg</file>
    <file>key-hide.svg</file>
    <file>key-layout.svg</file>
    <file>key-shift.svg</file>
    <file>key-shift-latched-uppercase.svg</file>
    <file>key-shift-uppercase.svg</file>
    <file>noise-texture.png</file>
    <file>**nome-do-arquivo**</file>
    <file>no-events.svg</file>
    <file>no-notifications.svg</file>
    <file>pad-osd.css</file>
    <file>page-indicator-active.svg</file>
    <file>page-indicator-checked.svg</file>
    <file>page-indicator-hover.svg</file>
    <file>page-indicator-inactive.svg</file>
    <file>process-working.svg</file>
    <file>toggle-off-hc.svg</file>
    <file>toggle-off-intl.svg</file>
    <file>toggle-off-us.svg</file>
    <file>toggle-on-hc.svg</file>
    <file>toggle-on-intl.svg</file>
    <file>toggle-on-us.svg</file>
  </gresource>
</gresources>
```

Substitua **nome-do-arquivo** com o nome do arquivo de sua imagem de plano de fundo.

Agora, abra o arquivo `gnome-shell.css` no diretório e alterar a definição `#lockDialogGroup` da seguinte forma:

```
#lockDialogGroup {
  background: #2e3436 url(**nome-do-arquivo**);
  background-size: **[ALTURA]**px **[LARGURA]**px;
  background-repeat: no-repeat;
}

```

Defina `background-size` para a resolução que o GDM usa, que pode não necessariamente ser a resolução da imagem. Para uma lista de resoluções de tela, veja [Display resolution](https://en.wikipedia.org/wiki/Display_resolution#Computer_monitors "wikipedia:Display resolution"). Novamente, defina **nome-de-arquivo** para ser o nome da imagem de fundo.

Finalmente, compile o tema usando o seguinte comando:

```
$ glib-compile-resources gnome-shell-theme.gresource.xml

```

Então, copie o arquivo resultante `gnome-shell-theme.gresource` para o diretório `/usr/share/gnome-shell`.

Então, reinicie `gdm.service` (note que só encerrar a sessão não é suficiente) e você deve descobrir que ele está usando sua imagem de plano de fundo.

Para mais informações, veja o seguinte [tópico no forum](https://bbs.archlinux.org/viewtopic.php?id=197036).

### Configuração no DConf

Some GDM settings are stored in a DConf database. They can be configured either by adding *keyfiles* to the `/etc/dconf/db/gdm.d` directory and then recompiling the GDM database by running `dconf update` as root or by logging into the GDM user on the system and changing the setting directly using the *gsettings* command line tool. Note that for the former approach, a GDM profile file is required - this must be created manually as it is no longer shipped upstream, see below:

 `/etc/dconf/profile/gdm` 
```
user-db:user
system-db:gdm
file-db:/usr/share/gdm/greeter-dconf-defaults
```

For the latter approach, you can log into the GDM user with the command below:

```
# machinectl shell gdm@

```

#### Logo da tela de autenticação

Either create the following keyfile

 `/etc/dconf/db/gdm.d/02-logo` 
```
[org/gnome/login-screen]
logo='*/path/to/logo.png*'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.login-screen logo '*/path/to/logo.png*'

```

#### Alterando o tema do cursor

GDM disregards [GNOME](/index.php/GNOME "GNOME") cursor theme settings and it also ignores the cursor theme set according to the [XDG specification](/index.php/Cursor_themes#XDG_specification "Cursor themes"). To change the cursor theme used in GDM, either create the following keyfile

 `/etc/dconf/db/gdm.d/10-cursor-settings` 
```
[org/gnome/desktop/interface]
cursor-theme='*theme-name'*

```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.desktop.interface cursor-theme '*theme-name*'

```

#### Fonte maior para a tela de autenticação

Click on the accessibility icon at the top right of the screen (a white circle with the silhouette of a person in the centre) and check the *Large Text* option.

To set a specific scaling factor, you can create the following keyfile:

 `/etc/dconf/db/gdm.d/03-scaling` 
```
[org/gnome/desktop/interface]
text-scaling-factor='*1.25*'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.desktop.interface text-scaling-factor '*1.25*'

```

#### Desligando o som

This tweak disables the audible feedback heard when the system volume is adjusted (via keyboard) on the login screen.

Either create the following keyfile:

 `/etc/dconf/db/gdm.d/04-sound` 
```
[org/gnome/desktop/sound]
event-sounds='false'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.desktop.sound event-sounds 'false'

```

#### Configurando o comportamento do botão de energia

**Note:**

*   The [logind settings](/index.php/Power_management#ACPI_events "Power management") for the power button are overriden by GNOME Settings Daemon. [[2]](https://bugzilla.gnome.org/show_bug.cgi?id=755953#c4)
*   As of GDM 3.18, the power button cannot be set to *interactive*. [[3]](https://bugzilla.gnome.org/show_bug.cgi?id=753713#c6)
*   In some cases, this setting will be ignored and hardcoded defaults will be used. [[4]](https://bugzilla.gnome.org/show_bug.cgi?id=755953#c17)

**Warning:** Please note that the [acpid](/index.php/Acpid "Acpid") daemon also handles the "power button" and "hibernate button" events. Running both systems at the same time may lead to unexpected behaviour.

Either create the following keyfile:

 `/etc/dconf/db/gdm.d/05-power` 
```
[org/gnome/settings-daemon/plugins/power]
power-button-action='*action*'
```

and then recompile the GDM database or alternatively log in to the GDM user and execute the following:

```
$ gsettings set org.gnome.settings-daemon.plugins.power power-button-action '*action*'

```

where *action* can be one of `nothing`, `suspend` or `hibernate`.

#### Habilitando tap-to-click

Tap-to-click is disabled in GDM (and GNOME) by default, but you can easily enable it with a dconf setting.

**Note:** If you want to do this under X, you have to first set up correct X server access permissions - see [#Configure X server access permission](#Configure_X_server_access_permission).

To directly enable tap-to-click, use:

 `# sudo -u gdm gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true` 

If you prefer to do this with a GUI, use:

 `# sudo -u gdm dconf-editor` 

To check the if it was set correctly, use:

 `$ sudo -u gdm gsettings get org.gnome.desktop.peripherals.touchpad tap-to-click` 

If you get the error `dconf-WARNING **: failed to commit changes to dconf: Error spawning command line`, make sure dbus is running:

 `$ sudo -u gdm dbus-launch gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true` 

#### Desabilitar/Habilitar o menu de acessibilidade

To disable or enable the Accessibility Menu, set the following key in dconf editor:

```
# machinectl shell gdm@
# gsettings set org.gnome.desktop.interface toolkit-accessibility false
# exit
```

The menu is disabled when the key is false, enabled when it is true.

### Layout do teclado

The system keyboard layout will be applied to GDM. See [Keyboard configuration in Xorg#Using X configuration files](/index.php/Keyboard_configuration_in_Xorg#Using_X_configuration_files "Keyboard configuration in Xorg").

**Tip:** See [Wikipedia:ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1 "wikipedia:ISO 3166-1") for a list of keymaps.

If a system has multiple users, it is possible to specify a keyboard layout for GDM to use which is different from the system keyboard layout. Firstly, ensure the package [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) is installed. Then start *gnome-control-center* and navigate to *Region & Language -> Input Sources*. In the header bar, hit the *Login Screen* toggle button and then choose a keyboard layout from the list. Note that the *Login Screen* button will not be visible in the header bar unless multiple users are present on the system [[5]](https://bugzilla.gnome.org/show_bug.cgi?id=741500).

Users of GDM 2.x (legacy GDM) may need to edit `~/.dmrc` as shown below:

 `~/.dmrc` 
```
[Desktop]
Language=de_DE.UTF-8   # change to your default lang
Layout=de   nodeadkeys # change to your keyboard layout
```

### Alterar o idioma

The system language will be applied to GDM. If a system has multiple users, it is possible to set a language for GDM different to the system language. In this case, firstly ensure that [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) is installed. Then, start *gnome-control-center* and choose *Region & Language*. In the header bar, check the *Login Screen* toggle button. Finally, click on *Language* and choose your language from the list. You will be prompted for your root password. Note that the *Login Screen* button will not be visible in the header bar unless multiple users are present on the system [[6]](https://bugzilla.gnome.org/show_bug.cgi?id=741500).

**Tip:** By adding 2 different input languages, logging out then selecting your default language GDM will remember your choice once the second option is removed.

### Usuários e autenticação

#### Autenticação automática

To enable automatic login with GDM, add the following to `/etc/gdm/custom.conf` (replace *username* with your own):

 `/etc/gdm/custom.conf` 
```
# Enable automatic login for user
[daemon]
AutomaticLogin=*username*
AutomaticLoginEnable=True
```

**Tip:** If GDM fails after adding these lines, comment them out from a TTY.

or for an automatic login with a delay:

 `/etc/gdm/custom.conf` 
```
[daemon]

TimedLoginEnable=true
TimedLogin=*username*
TimedLoginDelay=1
```

You can set the session used for automatic login (replace `gnome-xorg` with desired session):

 `/var/lib/AccountsService/users/*username*`  `XSession=gnome-xorg` 

#### Autenticação sem senha

If you want to bypass the password prompt in GDM then simply add the following line on the first line of `/etc/pam.d/gdm-password`:

```
auth sufficient pam_succeed_if.so user ingroup nopasswdlogin

```

Then, add the group `nopasswdlogin` to your system. See [Groups](/index.php/Groups "Groups") for group descriptions and group management commands.

Now, add your user to the `nopasswdlogin` group and you will only have to click on your username to login.

**Warning:**

*   Do **not** do this for a **root** account.
*   You won't be able to change your session type at login with GDM anymore. If you want to change your default session type, you will first need to remove your user from the `nopasswdlogin` group.

#### Desligamento sem senha para várias sessões

GDM uses polkit and logind to gain permissions for shutdown. You can shutdown the system when multiple users are logged in by setting:

 `/etc/polkit-1/localauthority.conf.d/org.freedesktop.logind.policy` 
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE policyconfig PUBLIC
 "-//freedesktop//DTD PolicyKit Policy Configuration 1.0//EN"
 "[http://www.freedesktop.org/standards/PolicyKit/1.0/policyconfig.dtd](http://www.freedesktop.org/standards/PolicyKit/1.0/policyconfig.dtd)">

<policyconfig>

  <action id="org.freedesktop.login1.power-off-multiple-sessions">
    <description>Shutdown the system when multiple users are logged in</description>
    <message>System policy prevents shutting down the system when other users are logged in</message>
    <defaults>
      <allow_inactive>yes</allow_inactive>
      <allow_active>yes</allow_active>
    </defaults>
  </action>

</policyconfig>
```

You can find all available logind options (e.g. reboot-multiple-sessions) [here](http://www.freedesktop.org/wiki/Software/systemd/logind#Security).

#### Habilitar autenticação como root no GDM

It is not advised to login as root, but if necessary you can edit `/etc/pam.d/gdm-password` and add the following line before the line `auth required pam_deny.so`:

`/etc/pam.d/gdm-password`

```
auth            sufficient      pam_succeed_if.so uid eq 0 quiet

```

The file should look something like this:

`/etc/pam.d/gdm-password`

```
...
auth            sufficient      pam_succeed_if.so uid eq 0 quiet
auth            sufficient      pam_succeed_if.so uid >= 1000 quiet
auth            required        pam_deny.so
...

```

You should be able to login as root after restarting GDM.

#### Ocultar usuário da lista de login

The users for the gdm user list are gathered by [AccountsService](https://www.freedesktop.org/wiki/Software/AccountsService/). It will automatically hide system users (UID < 1000). To hide ordinary users from the login list create or edit a file named after the user to hide in `/var/lib/AccountsService/users/` to contain at least:

 `/var/lib/AccountsService/users/<username>` 
```
[User]
SystemAccount=true
```

### Definir as configurações de monitor padrão

Some [desktop environments](/index.php/Desktop_environments "Desktop environments") store display settings in `~/.config/monitors.xml`. *xrandr* commands are then generated on the base of the file content. GDM has a similar file stored in `/var/lib/gdm/.config/monitors.xml`.

If you have your monitors setup as you like (orientation, primary and so on) in `~/.config/monitors.xml` and want GDM to honor those settings:

```
# cp ~/.config/monitors.xml /var/lib/gdm/.config/monitors.xml

```

Changes will take effect on logout. This is necessary because GDM does not respect `xorg.conf`.

**Note:** If you use GDM under Wayland, you must also use a `monitors.xml` that was created under Wayland. See [GNOME bug 748098](https://bugzilla.gnome.org/show_bug.cgi?id=748098) for more info. Alternatively, you can force GDM to [#Use Xorg backend](#Use_Xorg_backend), and use a `monitors.xml` that was created under Xorg.

### Configurar permissão de acesso do servidor X

You can use the `xhost` command to configure X server access permissions.

For instance, to grant GDM the right to access the X server, use the following command:

 `# xhost +SI:localuser:gdm` 

## Solução de problemas

### Falha ao usar driver proprietários da NVIDIA

GDM uses the [Wayland](/index.php/Wayland "Wayland") backend by default which conflicts with NVIDIA driver. Turning off the Wayland backend could enable proprietary NVIDIA driver.

### Falha no encerramento da sessão

If GDM starts up properly on boot, but fails after repeated attempts on logout, try adding this line to the daemon section of `/etc/gdm/custom.conf`:

```
GdmXserverTimeout=60

```

### Xorg sem senha

See [Xorg#Rootless Xorg](/index.php/Xorg#Rootless_Xorg "Xorg").

### Usar backend do Xorg

The [Wayland](/index.php/Wayland "Wayland") backend is used by default and the [Xorg](/index.php/Xorg "Xorg") backend is used only if the Wayland backend cannot be started. As the Wayland backend has been [reported](https://bugzilla.redhat.com/show_bug.cgi?id=1199890) to cause problems for some users, use of the Xorg backend may be necessary. To use the Xorg backend by default, edit the `/etc/gdm/custom.conf` file and uncomment the following line:

```
#WaylandEnable=false

```

### Remoção incompleta do gdm

After removing [gdm](https://www.archlinux.org/packages/?name=gdm), [systemd](/index.php/Systemd "Systemd") may report the following:

```
user 'gdm': directory '/var/lib/gdm' does not exist

```

To remove this warning, login as root and delete the primary user "gdm" and then delete the group "gdm":

```
# userdel gdm
# groupdel gdm

```

Verify that gdm is successfully removed via `pwck` and `grpck`. To round it off, you may want to double-check no [unowned files](/index.php/Pacman/Tips_and_tricks#Identify_files_not_owned_by_any_package "Pacman/Tips and tricks") for gdm remain.

### Suspensão automática do GDM (GNOME 3.28)

GDM uses a separate dconf database to control power management. You can make GDM behave the same way as user sessions by copying the user settings to GDM's dconf database.

```
$ IFS=$'
'; for x in $(sudo -u YOUR_USER gsettings list-recursively org.gnome.settings-daemon.plugins.power); do eval "sudo -u gdm dbus-launch gsettings set $x"; done; unset IFS

```

Or to simply disable auto-suspend (also run the command with `ac` replaced with `battery` to also disable it while running on battery):

```
$ sudo -u gdm dbus-launch gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type 'nothing'

```

## Veja também

*   [GDM Reference Manual](https://help.gnome.org/admin/gdm/stable/index.html.en)