**Status de tradução:** Esse artigo é uma tradução de [GDM](/index.php/GDM "GDM"). Data da última tradução: 2019-05-24\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=GDM&diff=0&oldid=573816) na versão em inglês.

Artigos relacionados

*   [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)")
*   [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição")

Do [GDM - GNOME Display Manager](https://wiki.gnome.org/Projects/GDM): "O Gerenciador de Exibição do GNOME (GDM) é um programa que gerencia servidores gráficos de exibição e lida com logins de usuários gráficos."

[Gerenciadores de exibição](/index.php/Gerenciadores_de_exibi%C3%A7%C3%A3o "Gerenciadores de exibição") fornecem a usuários de [X Window System](/index.php/X_Window_System_(Portugu%C3%AAs) "X Window System (Português)") e [Wayland](/index.php/Wayland "Wayland") com um prompt de login gráfico.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Inicialização](#Inicialização)
    *   [2.1 Inicializando aplicativos automaticamente](#Inicializando_aplicativos_automaticamente)
*   [3 Configuração](#Configuração)
    *   [3.1 Imagem de plano de fundo na tela de autenticação](#Imagem_de_plano_de_fundo_na_tela_de_autenticação)
    *   [3.2 Configuração no DConf](#Configuração_no_DConf)
        *   [3.2.1 Logo da tela de autenticação](#Logo_da_tela_de_autenticação)
        *   [3.2.2 Alterando o tema do cursor](#Alterando_o_tema_do_cursor)
        *   [3.2.3 Fonte maior para a tela de autenticação](#Fonte_maior_para_a_tela_de_autenticação)
        *   [3.2.4 Desligando o som](#Desligando_o_som)
        *   [3.2.5 Configurando o comportamento do botão de energia](#Configurando_o_comportamento_do_botão_de_energia)
        *   [3.2.6 Habilitando tap-to-click](#Habilitando_tap-to-click)
        *   [3.2.7 Desabilitar/Habilitar o menu de acessibilidade](#Desabilitar/Habilitar_o_menu_de_acessibilidade)
    *   [3.3 Layout do teclado](#Layout_do_teclado)
    *   [3.4 Alterar o idioma](#Alterar_o_idioma)
    *   [3.5 Usuários e autenticação](#Usuários_e_autenticação)
        *   [3.5.1 Autenticação automática](#Autenticação_automática)
        *   [3.5.2 Autenticação sem senha](#Autenticação_sem_senha)
        *   [3.5.3 Desligamento sem senha para várias sessões](#Desligamento_sem_senha_para_várias_sessões)
        *   [3.5.4 Habilitar autenticação como root no GDM](#Habilitar_autenticação_como_root_no_GDM)
        *   [3.5.5 Ocultar usuário da lista de login](#Ocultar_usuário_da_lista_de_login)
    *   [3.6 Definir as configurações de monitor padrão](#Definir_as_configurações_de_monitor_padrão)
    *   [3.7 Configurar permissão de acesso do servidor X](#Configurar_permissão_de_acesso_do_servidor_X)
*   [4 Solução de problemas](#Solução_de_problemas)
    *   [4.1 Wayland e o driver proprietário da NVIDIA](#Wayland_e_o_driver_proprietário_da_NVIDIA)
    *   [4.2 Falha no encerramento da sessão](#Falha_no_encerramento_da_sessão)
    *   [4.3 Xorg sem senha](#Xorg_sem_senha)
    *   [4.4 Usar backend do Xorg](#Usar_backend_do_Xorg)
    *   [4.5 GDM congela com o systemd](#GDM_congela_com_o_systemd)
    *   [4.6 Remoção incompleta do gdm](#Remoção_incompleta_do_gdm)
    *   [4.7 Suspensão automática do GDM (GNOME 3.28)](#Suspensão_automática_do_GDM_(GNOME_3.28))
    *   [4.8 GDM ignora Wayland e usa X.Org por padrão](#GDM_ignora_Wayland_e_usa_X.Org_por_padrão)
*   [5 Veja também](#Veja_também)

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
    <file>calendar-today.svg</file>
    <file>checkbox-focused.svg</file>
    <file>checkbox-off-focused.svg</file>
    <file>checkbox-off.svg</file>
    <file>checkbox.svg</file>
    <file>dash-placeholder.svg</file>
    <file>gnome-shell.css</file>
    <file>gnome-shell-high-contrast.css</file>
    <file>icons/message-indicator-symbolic.svg</file>
    <file>key-enter.svg</file>
    <file>key-hide.svg</file>
    <file>key-layout.svg</file>
    <file>key-shift-latched-uppercase.svg</file>
    <file>key-shift.svg</file>
    <file>key-shift-uppercase.svg</file>
    <file>noise-texture.png</file>
    <file>**nome-do-arquivo**</file>
    <file>no-events.svg</file>
    <file>no-notifications.svg</file>
    <file>pad-osd.css</file>
    <file>process-working.svg</file>
    <file>toggle-off-hc.svg</file>
    <file>toggle-off-intl.svg</file>
    <file>toggle-on-hc.svg</file>
    <file>toggle-on-intl.svg</file>
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

Algumas configurações do GDM são armazenadas em um banco de dados DConf. Eles podem ser configurados adicionando *arquivo-chaves* ao diretório `/etc/dconf/db/gdm.d` e, em seguida, recompilando o banco de dados do GDM executando `dconf update` como root ou fazendo login no usuário do GDM no sistema e alterando a configuração diretamente usando a ferramenta de linha de comando *gsettings*. Observe que, para a abordagem anterior, é necessário um arquivo de perfil do GDM - isso deve ser criado manualmente, pois não é mais enviado pelo desenvolvedor, veja abaixo:

 `/etc/dconf/profile/gdm` 
```
user-db:user
system-db:gdm
file-db:/usr/share/gdm/greeter-dconf-defaults
```

Para a última abordagem, você pode efetuar login no usuário do GDM com o comando abaixo:

```
# machinectl shell gdm@

```

#### Logo da tela de autenticação

Crie o seguinte arquivo-chave

 `/etc/dconf/db/gdm.d/02-logo` 
```
[org/gnome/login-screen]
logo='*/caminho/para/logo.png*'
```

e recompile o banco de dados do GDM ou, alternativamente, autentique-se ao usuário GDM e execute o seguinte:

```
$ gsettings set org.gnome.login-screen logo '*/caminho/para/logo.png*'

```

#### Alterando o tema do cursor

O GDM desconsidera as configurações do tema do cursor [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") e também ignora o conjunto de temas do cursor de acordo com a [especificação XDG](/index.php/Cursor_themes#XDG_specification "Cursor themes"). Para alterar o tema do cursor usado no GDM, crie o seguinte arquivo-chave

 `/etc/dconf/db/gdm.d/10-cursor-settings` 
```
[org/gnome/desktop/interface]
cursor-theme='*nome-tema'*

```

e recompile o banco de dados do GDM ou, alternativamente, autentique-se como o usuário GDM e execute o seguinte:

```
$ gsettings set org.gnome.desktop.interface cursor-theme '*nome-tema*'

```

#### Fonte maior para a tela de autenticação

Clique no ícone de acessibilidade no canto superior direito da tela (um círculo branco com a silhueta de uma pessoa no centro) e marque a opção *Texto grande*.

Para definir um fator de escala específico, você pode criar o seguinte arquivo-chave:

 `/etc/dconf/db/gdm.d/03-scaling` 
```
[org/gnome/desktop/interface]
text-scaling-factor='*1.25*'
```

e, em seguida, recompile o banco de dados do GDM ou, alternativamente, efetue login no usuário do GDM e execute o seguinte:

```
$ gsettings set org.gnome.desktop.interface text-scaling-factor '*1.25*'

```

#### Desligando o som

Este ajuste desativa o feedback audível ouvido quando o volume do sistema é ajustado (via teclado) na tela de login.

Crie o seguinte arquivo-chave:

 `/etc/dconf/db/gdm.d/04-sound` 
```
[org/gnome/desktop/sound]
event-sounds='false'
```

e recompile o banco de dados do GDM ou, alternativamente, efetue login no usuário do GDM e execute o seguinte:

```
$ gsettings set org.gnome.desktop.sound event-sounds 'false'

```

#### Configurando o comportamento do botão de energia

**Nota:**

*   As [configurações do logind](/index.php/Power_management#ACPI_events "Power management") para o botão de energia são substituídas pelo daemon de configurações do GNOME. [[2]](https://bugzilla.gnome.org/show_bug.cgi?id=755953#c4)
*   A partir do GDM 3.18, o botão de energia não pode ser ajustado para *interativo*. [[3]](https://bugzilla.gnome.org/show_bug.cgi?id=753713#c6)
*   Em alguns casos, essa configuração será ignorada e os padrões codificados serão usados. [[4]](https://bugzilla.gnome.org/show_bug.cgi?id=755953#c17)

**Atenção:** Observe que o daemon [acpid](/index.php/Acpid "Acpid") também lida com os eventos "botão liga/desliga" e "botão de hibernação". Executar os dois sistemas ao mesmo tempo pode levar a um comportamento inesperado.

Crie o seguinte arquivo-chave:

 `/etc/dconf/db/gdm.d/05-power` 
```
[org/gnome/settings-daemon/plugins/power]
power-button-action='*ação*'
```

e recompile o banco de dados do GDM ou, alternativamente, efetue login no usuário do GDM e execute o seguinte:

```
$ gsettings set org.gnome.settings-daemon.plugins.power power-button-action '*ação*'

```

sendo *ação* uma entre `nothing`, `suspend` ou `hibernate`.

#### Habilitando tap-to-click

Tap-to-click (em português, "tocar para clicar") está desabilitado no GDM (e no GNOME) por padrão, mas você pode facilmente habilitá-lo com uma configuração no dconf.

**Nota:** Se você quiser fazer isso no X, você precisa primeiro configurar as permissões corretas de acesso ao servidor X - veja [#Configurar permissão de acesso do servidor X](#Configurar_permissão_de_acesso_do_servidor_X).

Para habilitar tap-to-click diretamente, use:

 `# sudo -u gdm gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true` 

Se você preferir fazer isso com uma GUI, use:

 `# sudo -u gdm dconf-editor` 

Para verificar se ela está definida corretamente, use:

 `$ sudo -u gdm gsettings get org.gnome.desktop.peripherals.touchpad tap-to-click` 

Se você receber um erro `dconf-WARNING **: failed to commit changes to dconf: Error spawning command line`, certifique-se que dbus está em excecução:

 `$ sudo -u gdm dbus-launch gsettings set org.gnome.desktop.peripherals.touchpad tap-to-click true` 

#### Desabilitar/Habilitar o menu de acessibilidade

Para desabilitar ou habilitar o Menu de Acessibilidade, defina a seguinte chave no editor dconf:

```
# machinectl shell gdm@
# gsettings set org.gnome.desktop.interface toolkit-accessibility false
# exit
```

O menu é desabilitado quando a chave estiver em falso, habilitado quando estiver em verdadeiro.

### Layout do teclado

O layout do teclado do sistema será aplicado ao GDM. Veja [Keyboard configuration in Xorg#Using X configuration files](/index.php/Keyboard_configuration_in_Xorg#Using_X_configuration_files "Keyboard configuration in Xorg").

**Dica:** Veja [Wikipedia:ISO 3166-1](https://en.wikipedia.org/wiki/ISO_3166-1 "wikipedia:ISO 3166-1") para uma lista de *keymaps*.

Se um sistema tiver vários usuários, é possível especificar um layout de teclado para o GDM usar, o que é diferente do layout do teclado do sistema. Em primeiro lugar, certifique-se de que o pacote [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) esteja instalado. Então inicie o *gnome-control-center* e navegue até *Região & Idioma -> Fontes de entrada*. Na barra de cabeçalho, pressione o botão de alternância *Tela de início de sessão* e escolha um layout de teclado na lista. Observe que o botão *Tela de início de sessão* não estará visível na barra de cabeçalho, a menos que vários usuários estejam presentes no sistema [[5]](https://bugzilla.gnome.org/show_bug.cgi?id=741500).

Usuários do GDM 2.x (GDM legado) pode precisar editar `~/.dmrc` como mostrado abaixo:

 `~/.dmrc` 
```
[Desktop]
Language=de_DE.UTF-8   # altera seu idioma padrão
Layout=de   nodeadkeys # altera seu layout padrão
```

### Alterar o idioma

O idioma do sistema será aplicado ao GDM. Se um sistema tiver vários usuários, é possível definir um idioma para o GDM diferente do idioma do sistema. Neste caso, primeiro certifique-se de que [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) esteja instalado. Então, inicie o 'gnome-control-center' e escolha *Região & Idioma*. Na barra de cabeçalho, marque o botão de alternância *Tela de início de sessão*. Por fim, clique em *Idioma* e escolha seu idioma na lista. Você será solicitado a fornecer sua senha de root. Observe que o botão *Tela de início de sessão* não estará visível na barra de cabeçalho, a menos que vários usuários estejam presentes no sistema [[6]](https://bugzilla.gnome.org/show_bug.cgi?id=741500).

**Dica:** Ao adicionar dois idiomas de entrada diferentes, efetuando logout e selecionando seu idioma padrão, o GDM se lembrará de sua escolha assim que a segunda opção for removida.

### Usuários e autenticação

#### Autenticação automática

Para habilitar a autenticação automática com o GDM, adicione o seguinte a `/etc/gdm/custom.conf` (substitua *nome_de_usuário* por seu próprio):

 `/etc/gdm/custom.conf` 
```
# Habilita autenticação automática para o usuário
[daemon]
AutomaticLogin=*nome_de_usuário*
AutomaticLoginEnable=True
```

**Dica:** Se o GDM falhar após adicionar essas linhas, comente-as de um TTY.

ou para uma autenticação automática com um atraso:

 `/etc/gdm/custom.conf` 
```
[daemon]

TimedLoginEnable=true
TimedLogin=*nome_de_usuário*
TimedLoginDelay=1
```

Você pode definir a sessão usada para autenticação automática (substitua `gnome-xorg` pela sessão desejada):

 `/var/lib/AccountsService/users/*nome_de_usuário*`  `XSession=gnome-xorg` 

#### Autenticação sem senha

Se você quiser ignorar o prompt de senha no GDM, basta adicionar a seguinte linha na primeira linha de `/etc/pam.d/gdm-password`:

```
auth sufficient pam_succeed_if.so user ingroup nopasswdlogin

```

Em seguida, adicione o grupo `nopasswdlogin` ao seu sistema. Veja [Usuários e grupos#Gerenciamento de grupo](/index.php/Usu%C3%A1rios_e_grupos#Gerenciamento_de_grupo "Usuários e grupos") para descrições de grupos e comandos de gerenciamento de grupos.

Agora, adicione seu usuário ao grupo `nopasswdlogin` e você só terá que clicar no seu nome de usuário para se autenticar.

**Atenção:**

*   **Não** faça isso para a conta **root**.
*   Você não poderá mais alterar seu tipo de sessão na autenticação com o GDM. Se você quiser alterar o tipo de sessão padrão, primeiro precisará remover o usuário do grupo `nopasswdlogin`.

#### Desligamento sem senha para várias sessões

O GDM usa o polkit e o logind para obter permissões para o encerramento. Você pode desligar o sistema quando vários usuários estão autenticados, definindo:

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

Você pode encontrar todas as opções de logind disponíveis (por exemplo, reboot-multiple-sessions) [here](http://www.freedesktop.org/wiki/Software/systemd/logind#Security).

#### Habilitar autenticação como root no GDM

Não é aconselhável fazer login como root, mas, se necessário, você pode editar `/etc/pam.d/gdm-password` e adicionar a seguinte linha antes da linha `auth required pam_deny.so`:

`/etc/pam.d/gdm-password`

```
auth            sufficient      pam_succeed_if.so uid eq 0 quiet

```

O arquivo deve ser algo como isto:

`/etc/pam.d/gdm-password`

```
...
auth            sufficient      pam_succeed_if.so uid eq 0 quiet
auth            sufficient      pam_succeed_if.so uid >= 1000 quiet
auth            required        pam_deny.so
...

```

Você deve poder autenticar como root após reiniciar o GDM.

#### Ocultar usuário da lista de login

Os usuários da lista de usuários do gdm são reunidos por [AccountsService](https://www.freedesktop.org/wiki/Software/AccountsService/). Ele irá ocultar automaticamente os usuários do sistema (UID <1000). Para ocultar usuários comuns da lista de login, crie ou edite um arquivo com o nome do usuário para ocultar em `/var/lib/AccountsService/users/` para conter pelo menos:

 `/var/lib/AccountsService/users/*nome_de_usuário*` 
```
[User]
SystemAccount=true
```

### Definir as configurações de monitor padrão

Alguns [ambientes de desktop](/index.php/Ambientes_de_desktop "Ambientes de desktop") armazenam configurações de exibição em `~/.config/monitors.xml`. Os comandos *xrandr* são então gerados na base do conteúdo do arquivo. O GDM tem um arquivo semelhante armazenado em `/var/lib/gdm/.config/monitors.xml`.

Se você tiver a configuração de seus monitores como quiser (orientação, escala, primário e assim por diante) em `~/.config/monitors.xml` e quiser que o GDM honre essas configurações:

```
$ sudo cp ~/.config/monitors.xml /var/lib/gdm/.config/
$ sudo chown gdm:gdm /var/lib/gdm/.config/monitors.xml

```

As partes relevantes de `monitors.xml` para rotação e escala de tela são:

```
<monitors version="2">
  <configuration>
    <logicalmonitor>
      ...
      <scale>2</scale>
      ...
      <transform>
        <rotation>right</rotation>
        <flipped>no</flipped>
      </transform>
      ...
    </logicalmonitor>
  </configuration>
</monitors>

```

As alterações entrarão em vigor no encerramento da sessão. Isso é necessário porque o GDM não respeita `xorg.conf`.

**Nota:** Se você usa GDM sob o Wayland, você também deve usar um `monitors.xml` que foi criado sob Wayland. Veja [bug 224 do GDM](https://gitlab.gnome.org/GNOME/gdm/issues/224) para mais informações. Alternativamente, você pode forçar o GDM a [#Usar backend do Xorg](#Usar_backend_do_Xorg) e usar um `monitors.xml` que foi criado sob Xorg.

### Configurar permissão de acesso do servidor X

Você pode usar o comando `xhost` para configurar permissões de acesso ao servidor X.

Por exemplo, para conceder ao GDM o direito de acessar o servidor X, use o seguinte comando:

 `# xhost +SI:localuser:gdm` 

## Solução de problemas

### Wayland e o driver proprietário da NVIDIA

O GDM não funciona bem no modo Wayland com o driver proprietário [NVIDIA](/index.php/NVIDIA "NVIDIA"). Ao usar esse driver, o GDM usará o Xorg em vez disso. [[7]](https://gitlab.gnome.org/GNOME/gdm/merge_requests/46)

### Falha no encerramento da sessão

Se o GDM iniciar corretamente na inicialização, mas falhar após tentativas repetidas de encerramento de sessão, tente adicionar essa linha à seção do daemon do `/etc/gdm/custom.conf`:

```
GdmXserverTimeout=60

```

### Xorg sem senha

Veja [Xorg#Rootless Xorg](/index.php/Xorg#Rootless_Xorg "Xorg").

### Usar backend do Xorg

O backend [Wayland](/index.php/Wayland "Wayland") é usado por padrão e o backend [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") é usado somente se o backend de Wayland não puder ser iniciado. Como o backend Wayland foi [relatado](https://bugzilla.redhat.com/show_bug.cgi?id=1199890) para causar problemas para alguns usuários, o uso do backend do Xorg pode ser necessário. Para usar o backend do Xorg por padrão, edite o arquivo `/etc/gdm/custom.conf` e remova o comentário da seguinte linha:

```
#WaylandEnable=false

```

### GDM congela com o systemd

Se o GDM travar com `systemctl enable gdm`, e `systemctl start gdm` funciona conforme esperado, aplique a configuração com `systemctl edit gdm` conforme abaixo:

```
 [Service]
 Type=Idle

```

### Remoção incompleta do gdm

Após remover [gdm](https://www.archlinux.org/packages/?name=gdm), o [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") pode relatar o seguinte:

```
user 'gdm': directory '/var/lib/gdm' does not exist

```

Para remover esse aviso, autentique-se como root e exclua o usuário primário "gdm" e exclua o grupo "gdm":

```
# userdel gdm
# groupdel gdm

```

Verifique se gdm foi removido com sucesso via `pwck` e `grpck`. Para completar, você pode querer se certificar que não há arquivos [arquivos sem dono](/index.php/Pacman/Dicas_e_truques#Identificar_arquivos_que_pertençam_a_nenhum_pacote "Pacman/Dicas e truques") por restos do gdm.

### Suspensão automática do GDM (GNOME 3.28)

O GDM usa um banco de dados separado do dconf para controlar o gerenciamento de energia. Você pode fazer o GDM se comportar da mesma maneira que as sessões do usuário copiando as configurações do usuário para o banco de dados dconf do GDM.

```
$ IFS=$'
'; for x in $(sudo -u *nome_de_usuário* gsettings list-recursively org.gnome.settings-daemon.plugins.power); do eval "sudo -u gdm dbus-launch gsettings set $x"; done; unset IFS

```

sendo `*nome_de_usuário*` o nome do seu usuário.

Ou simplesmente desabilitar a suspensão automática (também execute o comando com `ac` substituído por `battery` para também desativá-lo durante a execução com bateria):

```
$ sudo -u gdm dbus-launch gsettings set org.gnome.settings-daemon.plugins.power sleep-inactive-ac-type 'nothing'

```

### GDM ignora Wayland e usa X.Org por padrão

Wayland requer Kernel Mode Setting (KMS) em execução para funcionar, e em algumas máquinas o processo GDM inicia mais cedo que KMS, resultando em GDM ser incapaz de ver Wayland e trabalhando apenas com X.Org, você pode resolver este problema [iniciando o KMS mais cedo](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting").

## Veja também

*   [Manual de referência do GDM](https://help.gnome.org/admin/gdm/stable/index.html.pt_BR)