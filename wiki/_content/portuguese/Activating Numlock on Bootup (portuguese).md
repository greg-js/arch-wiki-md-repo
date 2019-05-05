**Status de tradução:** Esse artigo é uma tradução de [Activating Numlock on Bootup](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup"). Data da última tradução: 2019-04-28\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Activating_Numlock_on_Bootup&diff=0&oldid=572120) na versão em inglês.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Console](#Console)
    *   [1.1 Usando um serviço separado](#Usando_um_serviço_separado)
    *   [1.2 Extendendo getty@.service](#Extendendo_getty@.service)
    *   [1.3 Alternativa Bash](#Alternativa_Bash)
*   [2 X.org](#X.org)
    *   [2.1 startx](#startx)
    *   [2.2 MATE](#MATE)
    *   [2.3 Usuários de KDE Plasma](#Usuários_de_KDE_Plasma)
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

Então crie e habilite um serviço systemd:

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

### Extendendo getty@.service

Isso é mais simples do que usar um serviço separado e não codifica o número de VTs em um script. Crie um [drop-in snippet](/index.php/Drop-in_snippet "Drop-in snippet") para `getty@.service` que são aplicados no topo da unidade original:

 `/etc/systemd/system/getty@.service.d/activate-numlock.conf` 
```
[Service]
ExecStartPre=/bin/sh -c 'setleds -D +num < /dev/%I'
```

**Nota:** Se você tiver algum problema, tente substituir `ExecStartPre` por `ExecStartPost` e/ou desabilitar a dica como descrito abaixo.

Para desativar a sugestão de ativação num-lock exibida na tela de login, edite `getty@tty1.service` e adicione `--nohints` às opções *agetty*:

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

### Usuários de KDE Plasma

Vá para Configurações do Sistema, no item Hardware/Dispositivos de Entrada/Teclado, você encontrará uma opção para selecionar o comportamento do NumLock.

### GDM

**Nota:** O GDM não executa mais scripts em `/etc/gdm/Init`.

Certifique-se de ter [numlockx](https://www.archlinux.org/packages/?name=numlockx) instalado e adicione o seguinte código ao [~/.xprofile](/index.php/Xprofile "Xprofile"):

```
if [ -x /usr/bin/numlockx ]; then
      /usr/bin/numlockx on
fi

```

### GNOME

Quando não estiver usando o gerenciador de login do GDM, o numlockx pode ser adicionado aos aplicativos de inicialização do GNOME.

Instale o pacote [numlockx](https://www.archlinux.org/packages/?name=numlockx). Em seguida, adicione um comando de inicialização para iniciar `numlockx`.

```
$ gnome-session-properties

```

O comando acima abre o applet **Startup Applications Preferences**. Clique em ***Add*** e digite o seguinte:

| Name: | *Numlockx* |
| Command: | */usr/bin/numlockx on* |
| Comment: | *Turns on numlock.* |

**Nota:** Esta não é uma alteração de todo o sistema, repita essas etapas para cada usuário que deseja ativar o NumLock após efetuar login.

### Xfce

No arquivo `~/.config/xfce4/xfconf/xfce-perchannel-xml/keyboards.xml`, certifique-se de os seguintes valores estão configurados como 'true':

```
<property name="Numlock" type="bool" value="true"/>
<property name="RestoreNumlock" type="bool" value="true"/>

```

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