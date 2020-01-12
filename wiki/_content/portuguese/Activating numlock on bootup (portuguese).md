**Status de tradução:** Esse artigo é uma tradução de [Activating numlock on bootup](/index.php/Activating_numlock_on_bootup "Activating numlock on bootup"). Data da última tradução: 2020-01-10\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Activating_numlock_on_bootup&diff=0&oldid=593041) na versão em inglês.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Console](#Console)
    *   [1.1 Usando um serviço separado](#Usando_um_serviço_separado)
    *   [1.2 Estendendo getty@.service](#Estendendo_getty@.service)
    *   [1.3 Alternativa Bash](#Alternativa_Bash)
*   [2 X.org](#X.org)
    *   [2.1 startx](#startx)
    *   [2.2 MATE](#MATE)
    *   [2.3 KDE Plasma](#KDE_Plasma)
    *   [2.4 GDM](#GDM)
    *   [2.5 GNOME](#GNOME)
    *   [2.6 Xfce](#Xfce)
    *   [2.7 SDDM](#SDDM)
    *   [2.8 SLiM](#SLiM)
    *   [2.9 OpenBox](#OpenBox)
    *   [2.10 LightDM](#LightDM)
    *   [2.11 LXDM](#LXDM)
    *   [2.12 LXQt](#LXQt)

## Console

### Usando um serviço separado

**Dica:** Estes passos podem ser automatizados através da instalação do pacote [systemd-numlockontty](https://aur.archlinux.org/packages/systemd-numlockontty/) e habilitando o serviço `numLockOnTty`.

Primeiro crie um script para configurar o numlock em TTYs relevantes:

 `/usr/local/bin/numlock` 
```
#!/bin/bash

for tty in /dev/tty{1..6}
do
    /usr/bin/setleds -D +num < "$tty";
done

```

Uma vez que o script é criado, você precisará torná-lo [executável](/index.php/Execut%C3%A1vel "Executável"). Do contrário, o script não ser executado.

Então, crie e [habilite](/index.php/Habilite "Habilite") um serviço systemd:

 `/etc/systemd/system/numlock.service` 
```
[Unit]
Description=numlock

[Service]
ExecStart=/usr/local/bin/numlock
StandardInput=tty
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

### Estendendo getty@.service

Isso é mais simples do que usar um serviço separado e não codifica o número de VTs em um script. Crie um [trecho drop-in](/index.php/Trecho_drop-in "Trecho drop-in") para `getty@.service` que são aplicados no topo da unidade original:

 `/etc/systemd/system/getty@.service.d/activate-numlock.conf` 
```
[Service]
ExecStartPre=/bin/sh -c 'setleds -D +num < /dev/%I'
```

**Nota:** Se você tiver algum problema, tente substituir `ExecStartPre` por `ExecStartPost` e/ou desabilitar a dica como descrito abaixo.

Para desativar a sugestão de ativação numlock exibida na tela de login, edite `getty@tty1.service` e adicione `--nohints` às opções *agetty*:

```
[Service]
ExecStart=
ExecStart=-/sbin/agetty '-p -- \\u' --nohints --noclear %I $TERM

```

### Alternativa Bash

Adicione `setleds -D +num` para `~/.bash_profile`. Observe que, diferentemente dos outros métodos, isso não terá efeito até que você efetue o login.

## X.org

Vários métodos estão disponíveis.

### startx

Instale o pacote [numlockx](https://www.archlinux.org/packages/?name=numlockx) e adicione isso para o arquivo `~/.xinitrc` antes de `exec`:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

numlockx &

exec window_manager

```

### MATE

Por padrão, o MATE salva o último estado no logout e o restaura durante o próximo login. Para habilitar o Numlock em cada login, você deve alterar os seguintes valores DCONF:

```
dconf write org.mate.peripherals-keyboard remember-numlock-state false
dconf write org.mate.peripherals-keyboard numlock-state 'on'

```

### KDE Plasma

Vá em *Configurações do sistema > Dispositivos de entrada > Teclado*, na aba *Hardware*, na seção *Numlock ao iniciar o Plasma*, escolha o comportamento desejado para o NumLock.

### GDM

**Nota:** O GDM não executa mais scripts em `/etc/gdm/Init`.

Certifique-se de ter [numlockx](https://www.archlinux.org/packages/?name=numlockx) instalado e adicione o seguinte código ao [~/.xprofile](/index.php/Xprofile_(Portugu%C3%AAs) "Xprofile (Português)"):

```
if [ -x /usr/bin/numlockx ]; then
      /usr/bin/numlockx on
fi

```

### GNOME

Execute o seguinte comando:

```
 $ gsettings set org.gnome.desktop.peripherals.keyboard numlock-state true

```

Para lembrar o último estado da tecla numlock (desabilitado ou habilitado), use:

```
  $ gsettings set org.gnome.desktop.peripherals.keyboard remember-numlock-state true

```

**Nota:** A chave `numlock-state` foi movida de `org.gnome.settings-daemon.peripherals.keyboard` desde o GNOME 3.34[[1]](https://gitlab.gnome.org/GNOME/gnome-settings-daemon/merge_requests/107)

Alternativamente, você pode adicionar `numlockx on` (de [numlockx](https://www.archlinux.org/packages/?name=numlockx) para um script de inicialização, como `~/.bashrc` (se estiver usando [Bash](/index.php/Bash "Bash")) ou `~/.profile`.

### Xfce

No arquivo `~/.config/xfce4/xfconf/xfce-perchannel-xml/keyboards.xml`, certifique-se de os seguintes valores estão configurados como 'true':

```
<property name="Numlock" type="bool" value="true"/>
<property name="RestoreNumlock" type="bool" value="true"/>

```

**Nota:** Se o arquivo não existir, abra *Configurações > Teclado*, marque e desmarque o *Restaurar o estado da tecla Num Lock ao iniciar*. Isso criará o arquivo `keyboards.xml`.

### SDDM

No arquivo `/etc/sddm.conf`, na seção `[General]`, defina o valor *Numlock* como *on*:

```
[General]
...
Numlock=on

```

### SLiM

No arquivo `/etc/slim.conf` encontre a linha e descomente-a (remova o `#`):

```
#numlock             on

```

### OpenBox

No arquivo `~/.config/openbox/autostart` adicione a linha:

```
numlockx &

```

E salve o arquivo.

### LightDM

Veja [LightDM#NumLock on by default](/index.php/LightDM#NumLock_on_by_default "LightDM").

### LXDM

Configure a opção em `/etc/lxdm/lxdm.conf`:

```
numlock=1

```

### LXQt

Configure a opção em `~/.config/lxqt/session.conf`:

```
[Keyboard]
numlock=true

```