**PulseAudio** (antigo Polypaudio) é um servidor de som em rede multi-plataforma , comumente usado em sistemas baseados no Linux e FreeBSD. Ele pode ser usado como um substituo melhorado do Enlightened Sound Daemon (ESD).

PulseAudio roda em sistemas Microsoft Windows e POSIX-compliant, como o Linux e FreeBSD. PulseAudio é um software livre lançado sobre os termos da GNU Lesser General Public License.

**Fonte:** [Wikipédia](https://en.wikipedia.org/wiki/PulseAudio "wikipedia:PulseAudio")

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Executando](#Executando)
*   [3 Configuração dos Backends](#Configura.C3.A7.C3.A3o_dos_Backends)
    *   [3.1 ALSA](#ALSA)
    *   [3.2 OSS](#OSS)
        *   [3.2.1 osspd](#osspd)
        *   [3.2.2 padsp wrapper](#padsp_wrapper)
    *   [3.3 GStreamer](#GStreamer)
    *   [3.4 OpenAL](#OpenAL)
    *   [3.5 libao](#libao)
    *   [3.6 PortAudio](#PortAudio)
    *   [3.7 ESD](#ESD)
*   [4 Desktop Environments](#Desktop_Environments)
    *   [4.1 X11 bell](#X11_bell)
    *   [4.2 GNOME](#GNOME)
    *   [4.3 KDE 3](#KDE_3)
    *   [4.4 KDE 4 e Qt4](#KDE_4_e_Qt4)
*   [5 Aplicativos](#Aplicativos)
    *   [5.1 Audacious](#Audacious)
    *   [5.2 mpd](#mpd)
    *   [5.3 MPlayer](#MPlayer)
*   [6 Configurações alternativas](#Configura.C3.A7.C3.B5es_alternativas)
    *   [6.1 Sistemas surround](#Sistemas_surround)
        *   [6.1.1 Gravar de fonte monitora](#Gravar_de_fonte_monitora)
    *   [6.2 PulseAudio via rede](#PulseAudio_via_rede)
    *   [6.3 Suporte TCP (som via rede)](#Suporte_TCP_.28som_via_rede.29)
        *   [6.3.1 Publicação Zeroconf (Avahi)](#Publica.C3.A7.C3.A3o_Zeroconf_.28Avahi.29)
    *   [6.4 Trocando o servidor PulseAudio usado por clientes X locais](#Trocando_o_servidor_PulseAudio_usado_por_clientes_X_locais)
    *   [6.5 Pulseaudio via OSS](#Pulseaudio_via_OSS)
*   [7 Soluções de problemas](#Solu.C3.A7.C3.B5es_de_problemas)
    *   [7.1 Sem som depois da instalação](#Sem_som_depois_da_instala.C3.A7.C3.A3o)
        *   [7.1.1 Sem placa de som](#Sem_placa_de_som)
        *   [7.1.2 Dispositivo de som mudo](#Dispositivo_de_som_mudo)
    *   [7.2 Falha ao iniciar o daemon](#Falha_ao_iniciar_o_daemon)
    *   [7.3 padevchooser](#padevchooser)
    *   [7.4 Problemas e uso intenso da CPU a partir da versão 0.9.14](#Problemas_e_uso_intenso_da_CPU_a_partir_da_vers.C3.A3o_0.9.14)
    *   [7.5 Som intermitente](#Som_intermitente)
    *   [7.6 Ajuste de volume não funciona corretamente](#Ajuste_de_volume_n.C3.A3o_funciona_corretamente)
    *   [7.7 Realtime scheduling](#Realtime_scheduling)
*   [8 Veja também](#Veja_tamb.C3.A9m)
*   [9 Links externos](#Links_externos)

## Instalação

Para instalar o PulseAudio:

```
# pacman -S pulseaudio

```

Opcionalmente você pode instalar alguns frontends escritos em GTK:

```
# pacman -S paprefs pavucontrol

```

## Executando

O PulseAudio pode ser iniciado usando:

```
$ pulseaudio --start

```

Ou se você usa o X11:

```
$ start-pulseaudio-x11

```

Isso vai iniciar o PulseAudio com os plugins para o X11\.

No KDE você pode usar o comando:

```
$ start-pulseaudio-kde

```

Isso permite que você veja cada um dos dispositivos de áudio no *Configurações do sistema->Multimídia->Phonon*.

Você pode parar o PulseAudio usando:

```
$ pulseaudio --kill

```

Note que em alguns Desktops Environments como o KDE e o GNOME, o PulseAudio será iniciado durante o login.

## Configuração dos Backends

### ALSA

Para aplicativos que não suportam o PulseAudio mas suportam o ALSA é **recomendado** instalar o plugin do PulseAudio para o ALSA. O jeito mais simples de fazê-lo é instalando o pacote pulseaudio-alsa.

```
# pacman -S pulseaudio-alsa

```

Esse pacote inclui o `/etc/asound.conf` necessário para configurar o ALSA para usar o PulseAudio.

Se você usa o Arch x86_64 e quer ter som em programas 32-bits (como o Wine), lembre-se de instalar o lib32-libpulse e o lib32-alsa-plugins também.

Para evitar que aplicativos usem a emulação do OSS via ALSA e assim transpassando o PulseAudio (prevenindo outros aplicativos de tocar som), remova o módulo `snd_pcm_oss` executando:

```
# rmmod snd_pcm_oss

```

Depois, coloque o módulo na lista negra (blacklist) adicionando `!snd_pcm_oss` na parte MODULES do arquivo `/etc/rc.conf`.

### OSS

Existem várias maneiras de fazer programas que só funcionam com OSS rodarem no PulseAudio:

#### osspd

Esse é o jeito mais simples.

Instale o ossp e inicie-o digitando:

```
# /etc/rc.d/osspd start

```

Depois, adicione-o na linha DAEMONS do arquivo `/etc/rc.conf`.

#### padsp wrapper

Se você tem um programa que usa o OSS você pode fazê-lo funcionar com o PulseAudio iniciando-o com o padsp:

```
$ padsp OSSprogram

```

Alguns exemplos:

```
$ padsp aumix
$ padsp sox foo.wav -t ossdsp /dev/dsp

```

Se você preferir você pode renomear seu programa OSS e substituí-lo com um script como esse:

 `/usr/bin/OSSProgram` 
```
#!/bin/sh
if test -x /usr/bin/padsp; then
    exec /usr/bin/padsp /usr/bin/OSSprogram-bin "$@"
else
    exec /usr/bin/OSSprogram "$@"
fi

```

### GStreamer

Para fazer o [GStreamer](/index.php/GStreamer "GStreamer") usar o PulseAudio, execute `gstreamer-properties` (parte do pacote *gnome-media*) e selecione *Servidor de som PulseAudio* tanto na Saída como Entrada padrão. Alternativamente, isso pode ser feito setando as variáveis `/system/gstreamer/0.10/default/audiosink` para *pulsesink* e `/system/gstreamer/0.10/default/audiosrc` para *pulsesrc* no gconf2:

```
 $ gconftool-2 -t string --set /system/gstreamer/0.10/default/audiosink pulsesink
 $ gconftool-2 -t string --set /system/gstreamer/0.10/default/audiosrc pulsesrc

```

Algumas aplicações (como o Rhythmbox) ignoram a propriedade *audiosink*, usando a propriedade *musicaudiosink*, que não pode ser configurada usando o `gstreamer-properties` e precisa ser setada manualmente usando o `gconf-editor` ou `gconftool-2`:

```
 $ gconftool-2 -t string --set /system/gstreamer/0.10/default/musicaudiosink pulsesink

```

### OpenAL

OpenAL deve usar o PulseAudio por padrão, mas você pode configurar explicitamente para usá-lo em: `/etc/openal/alsoft.conf`  `drivers=pulse,alsa` 

### libao

Edite a seguinte linha no arquivo de configuração do libao:

 `/etc/libao.conf`  `default_driver=pulse` 

### PortAudio

A versão atual do PortAudio no repositório community não suporta o PulseAudio. Isso pode ser arrumado compilando o PortAudio do ABS e aplicando esse [patch](http://svn.mandriva.com/cgi-bin/viewvc.cgi/packages/cooker/portaudio/current/SOURCES/portaudio-19-alsa_pulse.patch?revision=313993) ao código.

### ESD

PulseAudio substitui o enlightened sound daemon (ESD). Enquanto o PulseAudio estiver rodando, clientes ESD devem ser capazes de usá-lo sem configurações adicionais.

## Desktop Environments

#### X11 bell

Para fazer o PulseAudio tocar um som quando um evento do X11 acontecer (ex.: fazer seu terminal fazer 'Ping!' ao invés de 'Beep!'), adicione o seguinte no arquivo `/etc/pulse/default.pa`:

```
load-sample-lazy x11-bell /usr/share/sounds/freedesktop/stereo/dialog-error.ogg
load-module module-x11-bell sample=x11-bell 

```

Você também pode usar outro som. `dialog-error.ogg` faz parte do pacote *sound-theme-freedesktop*.

### GNOME

Para obter integração completa do GNOME com o PulseAudio você deve instalar os seguintes pacotes:

*   gnome-media-pulse
*   gnome-settings-daemon-pulse
*   libcanberra-pulse

Eles fazem parte do grupo *pulseaudio-gnome*.

### KDE 3

PulseAudio *não* é um substituto para o aRts. Se você usa o KDE 3 não é possível usar o PulseAudio por enquanto.

### KDE 4 e Qt4

Se tudo ocorreu bem não é necessário fazer nenhuma configuração adicional no KDE 4.

## Aplicativos

### Audacious

Audacious tem suporte nativo ao PulseAudio. Para usá-lo você deve setar nas preferências do Audacious (Ctrl + P) -> Áudio -> Plugin de saída atual para 'PulseAudio Output Plugin'.

### mpd

Você vai precisar [configurar](http://mpd.wikia.com/wiki/PulseAudio) o mpd para usar o PulseAudio.

Se você roda o daemon no modo system-wide, você vai precisar adicionar o usuário *mpd* no grupo *pulse-access* para conseguir fazer o mpd se conectar ao daemon.

Num desktop, executar o mpd com o seu usuário e não com o *mpd* é preferível.

### MPlayer

O MPlayer tem suporte nativo ao PulseAudio usando a opção "-ao=pulse". Também é possível configurar o PulseAudio para ser a saída de áudio padrão, em `~/.mplayer/config` para cada usuário, ou `/etc/mplayer/mplayer.conf` para o sistema inteiro:

 `/etc/mplayer/mplayer.conf`  `ao=pulse` 

## Configurações alternativas

### Sistemas surround

Várias pessoas tem uma placa de som surround, mas só usam dois canais, então o PulseAudio não pode usar como padrão uma configuração surround. Para habilitar todos os canais, edite o arquivo `/etc/pulse/daemon.conf`: descomente a linha 'default-sample-channels' (remova o ponto-e-vírgula do início da linha) e sete o valor para **6** se você tiver um sistema 5.1 ou **8** se você tiver um sistema 7.1 e assim por diante.

```
# Padrão
default-sample-channels=2
# Para 5.1
default-sample-channels=6
# Para 7.1
default-sample-channels=8

```

Depois de fazer a mudança, você deve reiniciar o PulseAudio.

#### Gravar de fonte monitora

Para conseguir gravar a partir de uma fonte monitora (a.k.a. "O-que-você-ouve", "Stereo Mix"), use `pactl list` para achar o nome da fonte no PulseAudio (ex. `alsa_output.pci-0000_00_1b.0.analog-stereo.monitor`). Então adicione algo como o seguinte no `/etc/asound.conf` or `~/.asoundrc`:

```
pcm.pulse_monitor {
  type pulse
  device alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
}

ctl.pulse_monitor {
  type pulse
  device alsa_output.pci-0000_00_1b.0.analog-stereo.monitor
}

```

Agora você pode selecionar o `pulse_monitor` como uma fonte de gravação.

### PulseAudio via rede

Um dos recursos mais interessantes do PulseAudio é a possibilidade de fazer streams de áudio dos clientes via TCP até o servidor rodando o daemon do PulseAudio, permitindo que sons sejam transmitidos via LAN.

Para conseguir isso, é necessário ativar o module-native-protocol-tcp, e copiar o pulse-cookie nos clientes.

### Suporte TCP (som via rede)

Para ativar o módulo TCP, adicione isso (ou descomente, se já estiver aí) `/etc/pulse/default.pa`:

```
load-module module-native-protocol-tcp

```

Para permitir conexões remotas ao módulo TCP, você também tem que desbloquear o serviço em `/etc/hosts.allow` com a seguinte linha:

```
pulseaudio-native: ALL

```

#### Publicação Zeroconf (Avahi)

Para o servidor remoto do PulseAudio aparecer no PulseAudio Device Chooser (`padevchooser`), você também vai precisar adicionar o `avahi-daemon` na linha DAEMONS do seu rc.conf tanto no servidor quanto nos clientes.

### Trocando o servidor PulseAudio usado por clientes X locais

Para trocar entre servidores no cliente a partir do X, o comando `pax11publish` pode ser usado. Por exemplo, para trocar do servidor padrão para um servidor no hostname foo:

```
$ pax11publish -e -S foo

```

Ou para voltar ao servidor padrão:

```
$ pax11publish -e -r

```

Note que para a troca se efetive, os programas que usam o PulseAudio devem ser reiniciados.

### Pulseaudio via OSS

Adicione a seguinte linha no `/etc/pulse/default.pa`:

```
 load-module module-oss

```

Então inicie o PulseAudio como usual.

## Soluções de problemas

### Sem som depois da instalação

#### Sem placa de som

Se o PulseAudio inicie, rode `pacmd list`. Se nenhuma placa de som for reportada, confira se seus dispositivos ALSA não estão em uso:

```
$ fuser -v /dev/snd/*
$ fuser -v /dev/dsp

```

Tenha certeza que qualquer aplicativo usando pcm ou dsp está desligado antes de reiniciar o PulseAudio.

#### Dispositivo de som mudo

Se você não teve nenhum áudio enquanto usava o ALSA como seu dispositivo padrão, talvez você tenha que remover o mudo da sua placa de som. Para isso, você vai iniciar o alsamixer e checar se cada coluna tem uma verde com 00 abaixo dele (isso pode ser feito pressionando 'm')

```
$ alsamixer -c 0

```

Algumas vezes o módulo snd_pcsp conflita com o snd_hda_intel (para aqueles que usam placas da Intel) e nenhum som é conseguido. Para arrumar isso, você pode colocar na lista negra (blacklist) o módulo snd_pcsp na linha MODULES do arquivo `/etc/rc.conf` (inserindo `!snd_pcsp`)

### Falha ao iniciar o daemon

Tente recomeçar o PulseAudio. Para isso:

```
$ pulseaudio --kill
$ killall pulseaudio
$ killall -9 pulseaudio
$ rm -rf ~/.pulse*
$ rm -rf /tmp/pulse*

```

Depois disso, inicie o PulseAudio de novo.

### padevchooser

Se você não consegue iniciar o PulseAudio Device Chooser, primeiro (re)inicie o daemon do Avahi:

```
$ /etc/rc.d/avahi-daemon restart

```

### Problemas e uso intenso da CPU a partir da versão 0.9.14

O servidor de áudio PulseAudio foi reescrito para usar timer-based scheduling ao invés do tradicional interrupt-driven scheduling. Timer-based scheduling pode apresentar problemas em alguns drivers do ALSA. Para desligar o timer-based scheduling, substitua a linha:

```
load-module module-udev-detect 

```

no arquivo `/etc/pulse/default.pa` por:

```
load-module module-udev-detect tsched=0

```

### Som intermitente

Som intermitente no PulseAudio pode ser resultado de configurações erradas no sample rate do arquivo `/etc/pulse/ddaemon.conf`. Tente substituir a linha

```
; default-sample-rate = 44100

```

para

```
default-sample-rate = 48000

```

e reinicie o PulseAudio usando

```
pulseaudio --kill && pulseaudio --start

```

### Ajuste de volume não funciona corretamente

Você talvez queira checar:

```
/usr/share/pulseaudio/alsa-mixer/paths/analog-output.conf.common

```

### Realtime scheduling

Se o rtkit não funcionar, você pode setar manualmente seu sistema para rodar o PulseAudio com realtime scheduling, o que ajuda na performance. Para fazer isso, adicione as seguintes linhas no arquivo `/etc/security/limits.conf`:

```
@pulse-rt - rtprio 9
@pulse-rt - nice -11

```

Depois disso, você precisa adicionar seu usuário no grupo `pulse-rt`:

```
# gpasswd -a <user> pulse-rt

```

## Veja também

*   [Allow multiple programs to play sound at once](/index.php/Allow_multiple_programs_to_play_sound_at_once "Allow multiple programs to play sound at once")

## Links externos

*   [http://www.pulseaudio.org/wiki/PerfectSetup](http://www.pulseaudio.org/wiki/PerfectSetup) - Um bom guia para configurar o PulseAudio de forma perfeita (em inglês)
*   [http://www.alsa-project.org/main/index.php/Asoundrc](http://www.alsa-project.org/main/index.php/Asoundrc) - Alsa wiki sobre .asoundrc (em inglês)
*   [http://www.pulseaudio.org/](http://www.pulseaudio.org/) - Site oficial do PulseAudio (em inglês)
*   [http://www.pulseaudio.org/wiki/FAQ](http://www.pulseaudio.org/wiki/FAQ) - PulseAudio FAQ (em inglês)