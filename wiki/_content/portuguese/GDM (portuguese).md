Artigos relacionados

*   [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)")
*   [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback")
*   [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição")
*   [LightDM](/index.php/LightDM "LightDM")
*   [LXDM](/index.php/LXDM "LXDM")

Dá página do [GDM - GNOME Display Manager](http://projects.gnome.org/gdm/about.html):

	*GDM é sigla para GNOME Display Manager (Gerenciador de Display do GNOME, numa tradução para o português). É um o pequeno programa que roda em segundo plano, carrega suas sessões do X, se apresenta a você como uma tela de login e lhe impede o acesso caso tenha esquecido sua senha. Ele faz praticamente tudo que você gostaria de ver no xdm, mas sem os problemas do mesmo. O GDM não utiliza nenhum código do XDM. Suporta o XDMCP e na verdade, estende-o um pouco a lugares que faltavam no xdm(mas ainda compatível com o XDMCP do xdm).*

[Display managers](/index.php/Display_manager_(Portugu%C3%AAs) "Display manager (Português)") (ou gerenciadores de exibição) fornecem [X Window System](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") para usuários no login no prompt.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Configuração](#Configura.C3.A7.C3.A3o)
    *   [2.1 Login automático](#Login_autom.C3.A1tico)
    *   [2.2 Login sem senha](#Login_sem_senha)
    *   [2.3 GDM legacy](#GDM_legacy)
*   [3 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [3.1 Falha de Login no GDM](#Falha_de_Login_no_GDM)
    *   [3.2 gconf-sanity-check-2 saiu com status 256](#gconf-sanity-check-2_saiu_com_status_256)
    *   [3.3 Login de root no GDM](#Login_de_root_no_GDM)
    *   [3.4 GDM sempre usa teclado padrão US-keyboard](#GDM_sempre_usa_teclado_padr.C3.A3o_US-keyboard)

## Instalação

Para instalar o [GDM](http://www.gnome.org/projects/gdm/) (parte do Gnome-Extra), digite no prompt:

 `# pacman -S gdm` 

Para criar o login gráfico o metódo tradicional de logar no sistema, edite seu arquivo `/etc/inittab` (recomendado). Pode adicionar como alternativa o gdm na sua lista de daemons em `/etc/rc.conf`. Estes procedimentos estão detalhados na página do [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição").

Se está acostumado a usar o arquivo `~/.xinitrc` para passar o argumento do servidor X quando é iniciado, por exemplo **xmodmap** ou **xsetroot**, você pode observar que pode adicionar o comando para [xprofile](/index.php/Xprofile_(Portugu%C3%AAs) "Xprofile (Português)"). Exemplo:

 `~/.xprofile` 
```
#!/bin/sh

#
# ~/.xprofile
#
# Executed by gdm at login
#

xmodmap -e "pointer=1 2 3 6 7 4 5" # conjunto de botões do mouse
xsetroot -solid black              # define o background

```

## Configuração

Você não pode mais usar o comando gdmsetup para configuração do GDM na versão 2.28\. O comando foi removido, e o GDM foi padronizado e integrado com o restante do GNOME.

Você pode instalar o gdm2setup que está no AUR para configuração do GDM, ou acompanhe a instrução:

Permitir acesso para configurar servidor X

 `# xhost +SI:localuser:gdm` 

Para configurar o tema para GDM, use o comando:

 `# -u gdm gnome-appearance-properties` 

Para mais opções de configuração, use este comando:

 `# -u gdm gconf-editor` 

E segue a modificação de hierarquia:

```
/apps/gdm/simple-greeter
/desktop/gnome/interface
/desktop/gnome/background

```

Se este comando falhar com o erro "Não pode abrir o display" quando iniciar GDM, você pode abrir duas janelas no login automático no GDM. Primeiro crie o comando (como root):

 `# cp -t /usr/share/gdm/autostart/LoginWindow/ /usr/share/applications/gnome-appearance-properties.desktop /usr/share/applications/gconf-editor.desktop` 

Então saia do usuário e volte ao GDM. Depois da janela de login, aparecerá duas outras janelas. Configure o GDM como deseja, e feche a janela e volte a logar. Quando estiver feito e se quiser não mas abrir com o GDM, execute o comando (como root):

 `# rm /usr/share/gdm/autostart/LoginWindow/gnome-appearance-properties.desktop /usr/share/gdm/autostart/LoginWindow/gconf-editor.desktop` 
**Nota:** Apesar que os seguintos comandos podem usar o sudo, você precisa de executar como root! ("su -" trabalhando)

Para mais informações e as configurações avançadas leia [aqui](http://library.gnome.org/admin/gdm/2.28/configuration.html.en).

Nota-se que está com a versão 1.6.1 do xorg-server `Ctrl`+`Alt`+`Backspace` não reinicia mais o gdm. A instrução para re-habilitar este procedimento, veja [Keyboard configuration in Xorg#Terminating Xorg with Ctrl+Alt+Backspace](/index.php/Keyboard_configuration_in_Xorg#Terminating_Xorg_with_Ctrl.2BAlt.2BBackspace "Keyboard configuration in Xorg").

### Login automático

Para habilitar o login automático com GDM, adicione o seguinte na /etc/gdm/custom.conf (substituição do usuário que vai auto-logar):

 `/etc/gdm/custom.conf` 
```
# Enable automatic login for user
[daemon]
AutomaticLogin=username
AutomaticLoginEnable=True

```

Ou atraso no login automática:

 `/etc/gdm/custom.conf` 
```
[daemon]
# for login with delay
TimedLoginEnable=true
TimedLogin=username
TimedLoginDelay=1

```

### Login sem senha

Se deseja ignorar a senha no GDM adicione a seguinte linha `/etc/pam.d/gdm` :

```
auth sufficient pam_succeed_if.so user ingroup nopasswdlogin

```

**Verifique** se a linha vai ficar no lado direito contendo "pam_unix.so".

Depois, adicione o grupo **nopasswdlogin** no seu sistema. Você pode realizar pelo gráfico também, em Sistemas > Administração > Usuários e Grupos. Veja em [Grupo](/index.php/Grupo "Grupo") a descrição e os comandos de gerenciamento de grupo.

Agora, quando acessar em Sitemas > Administração > Usuários e Grupos (como root) e definir seu usuário para "Senha: não pediu no login" (você criou a opção "Nâo perguntar mas a senha de login"), seu usuário adicionou automaticamente no grupo "nopasswdlogin", agora simplesmente terá que clicar no seu nome de usuário e registrará a senha que vai ser ignorada totalmente!

**Atenção:** <u>NÃO FAÇA</u> COM A CONTA DE ***ROOT***!

### GDM legacy

Se você deseja voltar para o antigo GDM, possui uma ferramenta para as configurações, para compilar e instalar no AUR [gdm-old](https://aur.archlinux.org/packages.php?ID=31165).

## Solução de problemas

### Falha de Login no GDM

Se o GDM iniciar adequadamente no boot, mais não com várias tentantivas de login, adicione esta linha do daemon `/etc/gdm/custom.conf`:

```
GdmXserverTimeout=60

```

### gconf-sanity-check-2 saiu com status 256

Se o GDM aparecer um erro sobre gconf-sanity-check-2, você pode verificar a permissão na /home e /etc/gconf/gconfig.xml.system (deve ser 755). Se aparecer a mensagem no GDM, apague os aquivos na home. Como root:

```
rm -rf /var/lib/gdm/.*

```

### Login de root no GDM

Não é aconselhavel realizar login como root, se for necessário edite `/etc/gdm/custom.conf` e adicione:

```
[security]
AllowRoot=true

```

Você deve fazer o login como root após reiniciar o GDM.

### GDM sempre usa teclado padrão US-keyboard

Problema: O layout do teclado é sempre para US; o layout é redefinido quando o teclado é plugado.

Solução: Edite ~/.dmrc

```
[Desktop]
Language=de_DE.UTF-8   # Padrão da linguagem
Layout=de   nodeadkeys # Layout do teclado

```