**Status de tradução:** Esse artigo é uma tradução de [Advanced Linux Sound Architecture](/index.php/Advanced_Linux_Sound_Architecture "Advanced Linux Sound Architecture"). Data da última tradução: 2017-12-24\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Advanced_Linux_Sound_Architecture&diff=0&oldid=13292) na versão em inglês.

Artigos relacionados

*   [Advanced Linux Sound Architecture/Exemplo de configurações](/index.php/Advanced_Linux_Sound_Architecture/Exemplo_de_configura%C3%A7%C3%B5es "Advanced Linux Sound Architecture/Exemplo de configurações")
*   [Advanced Linux Sound Architecture/Troubleshooting](/index.php/Advanced_Linux_Sound_Architecture/Troubleshooting "Advanced Linux Sound Architecture/Troubleshooting")
*   [Sistema de som](/index.php/Sistema_de_som "Sistema de som")
*   [Disable PC Speaker Beep](/index.php/Disable_PC_Speaker_Beep "Disable PC Speaker Beep")
*   [PulseAudio (Português)](/index.php/PulseAudio_(Portugu%C3%AAs) "PulseAudio (Português)")
*   [Open Sound System](/index.php/Open_Sound_System "Open Sound System")

## Contents

*   [1 Sobre este documento](#Sobre_este_documento)
*   [2 Instalação](#Instalação)
    *   [2.1 Kernel drivers](#Kernel_drivers)
        *   [2.1.1 Kernel 2.4](#Kernel_2.4)
        *   [2.1.2 Kernel 2.6](#Kernel_2.6)
    *   [2.2 Userspace utilities](#Userspace_utilities)
*   [3 Configuração](#Configuração)
    *   [3.1 Certificando-se que os modulos do som estão carregados](#Certificando-se_que_os_modulos_do_som_estão_carregados)
    *   [3.2 Habilitando canais e testando a placa de som](#Habilitando_canais_e_testando_a_placa_de_som)
    *   [3.3 Configurando as permissões](#Configurando_as_permissões)
    *   [3.4 Restaurando as configurações do mixer durante a inicialização](#Restaurando_as_configurações_do_mixer_durante_a_inicialização)
    *   [3.5 Obtendo a saída SPDIF](#Obtendo_a_saída_SPDIF)
*   [4 Continua sem som?](#Continua_sem_som?)
*   [5 Configurando o KDE](#Configurando_o_KDE)

## Sobre este documento

Esta é uma tradução feita por [Hugo Dória](/index.php/User:Nozey "User:Nozey") do how to **[Alsa Setup](/index.php/ALSA "ALSA")**. Quaisquer dúvidas quanto à **tradução do documento**, por favor, entrar em contato com o tradutor, e não com o autor do documento original.

Este documento mostra como configurar o alsa tanto com a série 2.4 do kernel, quanto com a 2.6\. Veja, também, [como permitir que os programas toquem som ao mesmo tempo](/index.php/Allow_multiple_programs_to_play_sound_at_once "Allow multiple programs to play sound at once")

## Instalação

### Kernel drivers

#### Kernel 2.4

Se você usa um kernel da série 2.4, você terá que instalar os drivers do alsa. Se o seu kernel foi instalado com o pacote pré-compilado **kernel24** ou **kernel24-scsi**, você pode usar o pacote **alsa-driver**:

```
# pacman -S alsa-driver
# depmod -a

```

Se você compilou o seu próprio kernel, você deve compilar um novo pacote do 'alsa-driver' com o ABS e instalá-lo.

#### Kernel 2.6

O Alsa foi incluído no kernel 2.6 e em todos os pacotes **kernel26*** do Arch. Se você compilar o seu próprio kernel, não esqueça de ativar o driver do alsa correto.

**NOTA SOBRE A AUTO DETECÇÃO DO UDEV**: Instalações antigas do Arch ou instalações feitas a partir do cd da versão 0.7.1 (recentes instalações via FTP **não** foram afetadas) terão uma **configuração padrão antiga no arquivo /etc/modprobe.d/modprobe.conf** que **IRÁ QUEBRAR A AUTO DETECÇÃO DO SOM**. Se seus modulos de som não forem carregados automaticamente após a instalação ou atualização do udev, por favor, **REMOVA AS SEGUINTES LINHAS DO ARQUIVO /etc/modprobe.d/modprobe.conf**:

```
# OSS Compatibility
install snd-pcm modprobe -i snd-pcm ; modprobe snd-pcm-oss ; true
install snd-seq modprobe -i snd-seq ; modprobe snd-seq-oss ; true

```

Depois de **REMOVER** estas linhas, o som deverá ser auto detectado corretamente durante a (re)inicialização do sistema. Outra coisa. **NUNCA** use o alsaconf se você possui uma placa de som PCI ou ISAPNP, pois a configuração que o alsaconf adiciona ao arquivo modprobe.conf poderá ter um efeito parecido sobre a auto detecção do udev.

### Userspace utilities

*   Necessário para os programas alsa nativos e administração:

```
# pacman -S alsa-lib alsa-utils

```

*   Recomendado caso você deseja usar aplicações com suporte a OSS em combinação com o dmix:

```
# pacman -S alsa-oss

```

Quase todos os programas terão o pacote alsa-lib como dependência.

## Configuração

### Certificando-se que os modulos do som estão carregados

Você pode supor que o udev (ou o hotplug para a série 2.4 do kernel) irá auto detectar o som corretamente, incluíndo os modulos para a compatibilidade com o OSS. Você pode verificar isto com o comando:

```
$ lsmod|grep ^snd
snd_usb_audio          69696  0 
snd_usb_lib            13504  1 snd_usb_audio
snd_rawmidi            20064  1 snd_usb_lib
snd_hwdep               7044  1 snd_usb_audio
snd_seq_oss            29412  0 
snd_seq_midi_event      6080  1 snd_seq_oss
snd_seq                46220  4 snd_seq_oss,snd_seq_midi_event
snd_seq_device          6796  3 snd_rawmidi,snd_seq_oss,snd_seq
snd_pcm_oss            45216  0 
snd_mixer_oss          15232  1 snd_pcm_oss
snd_intel8x0           27932  0 
snd_ac97_codec         87648  1 snd_intel8x0
snd_ac97_bus            1792  1 snd_ac97_codec
snd_pcm                76296  4 snd_usb_audio,snd_pcm_oss,snd_intel8x0,snd_ac97_codec
snd_timer              19780  2 snd_seq,snd_pcm
snd                    43776  12 snd_usb_audio,snd_rawmidi,snd_hwdep,snd_seq_oss,snd_seq,snd_seq_device,snd_pcm_oss,snd_mixer_oss,snd_intel8x0,snd_ac97_codec,snd_pcm,snd_timer
snd_page_alloc          7944  2 snd_intel8x0,snd_pcm

```

Se a saída do comando acima for parecida, seus drivers de som foram auto detectados com sucesso. Você pode, também, checar o diretório **/dev/snd** para os arquivos de dispositivos corretos (somente kernel 2.6 e udev).

```
$ ls -l /dev/snd/
total 0
crw-rw----  1 root audio 116,  0 Apr  8 14:17 controlC0
crw-rw----  1 root audio 116, 32 Apr  8 14:17 controlC1
crw-rw----  1 root audio 116, 24 Apr  8 14:17 pcmC0D0c
crw-rw----  1 root audio 116, 16 Apr  8 14:17 pcmC0D0p
crw-rw----  1 root audio 116, 25 Apr  8 14:17 pcmC0D1c
crw-rw----  1 root audio 116, 56 Apr  8 14:17 pcmC1D0c
crw-rw----  1 root audio 116, 48 Apr  8 14:17 pcmC1D0p
crw-rw----  1 root audio 116,  1 Apr  8 14:17 seq
crw-rw----  1 root audio 116, 33 Apr  8 14:17 timer

```

Se você tiver, pelo menos, os dispositivos **controlC0** e **pcmC0D0p** ou parecidos, então seus modulos de som foram detectados e carregados corretamente.

Se este não for o caso, você terá que carregar os modulos manualmente.

*   Procure o modulo da sua placa de som: [http://www.alsa-project.org/alsa-doc/](http://www.alsa-project.org/alsa-doc/) O modulo terá o préfixo 'snd-' (por exemplo: 'snd-via82xx').

*   Carregue o modulo:

```
 # modprobe snd-NOME-DO-MODULO
 # modprobe snd-pcm-oss

```

*   Verifique os arquivos de dispositivos no diretório **/dev/snd** (veja acima) e/ou rode o **alsamixer** ou o **amixer** e veja se eles mostram uma saída correta.

*   Adicione **snd-pcm-oss** e **snd-NOME-DO-MODULO** para a lista de MODULOS em **/etc/rc.conf** para garantir que eles serão carregados da próxima vez.

### Habilitando canais e testando a placa de som

*   Habilitando o som (tirando do mudo):

```
 # amixer set Master 75 unmute
 # amixer set PCM 75 unmute

```

Você também pode fazer isto graficamente utilizando o 'alsamixer'.

**OBS:** Quando usar o alsamixer, **tire o canal do mudo** (apertando M) e aumente o volume (com os direcionais do teclado).

*   Tente tocar um arquivo no formato wav:

```
 # aplay meuarquivo.wav

```

*   [Allow multiple programs to play sound at once](/index.php/Allow_multiple_programs_to_play_sound_at_once "Allow multiple programs to play sound at once")

### Configurando as permissões

Para poder usar a placa de som como um usuário comum, siga os seguintes passos:

*   Adicione o seu usuário ao grupo 'audio':

```
# gpasswd -a NOME-DO-USUARIO audio

```

*   Dê logoff e logue-se novamente para ter certeza que o grupo audio foi carregado.

### Restaurando as configurações do mixer durante a inicialização

*   Rode 'alsactl' uma vez para que o arquivo '/etc/asound.state' seja criado

```
alsactl store

```

*   Edite o arquivo '/etc/rc.conf' e adicione 'alsa' na lista de DAEMONS a serem rodados durante o boot. Isto vai fazer com que as configurações do mixer sejam salvas sempre que o computador for desligado e restauradas a cada boot.

### Obtendo a saída SPDIF

*   No Controle de Volume do Gnome, na aba Options, mude de IEC958 para PCM. Esta opção pode ser ativada nas preferências.

*   Caso você não tenha o Controle de Volume do Gnome,
    *   Edite o arquivo /etc/asound.state. É neste arquivo que as configurações do mixer são salvas.
    *   Encontre uma linha que diz: 'IEC958 Playback Switch'. Próxima a ela, você encontrará uma linha dizendo **value:false**. Mude para **value:true**
    *   Agora encontre esta linha: 'IEC958 Playback AC97-SPSA' e mude o seu valor para 0.
    *   Reinicie o alsa.

Método alternativo para ativar a saída SPDIF automaticamente durante o login (testado na SoundBlaster Audigy)

*   Adicione as seguintes linhas ao arquivo /etc/rc.local:

```
 # Use COAX-digital output
 amixer set 'IEC958 Optical' 100 unmute
 amixer set 'Audigy Analog/Digital Output Jack' on

```

Você pode ver o nome da daída digital da sua placa som:

```
 amixer scontrols

```

## Continua sem som?

Mesmo que os drivers estejam instalados corretamente e que o volume esteja alto (sem nada mudo), você pode não escutar nada! Adicionar a linha abaixo ao arquivo '/etc/modprobe.d/modprobe.conf' pode consertar o problema (com o driver 'via82xx', pelo menos)

```
options snd-NAME-OF-MODULE ac97_quirk=0

```

Verifique também, através do alsamixer, se as barras de volume não estão marcadas com "MM", pois isso significa que aquele dispositivo está mudo. Para mudar isso selecione a barra de volume do dispositivo que deseja (importante se não sai som de seu headphone) e pressione "M".

## Configurando o KDE

*   Inicialize o KDE:

```
# startx

```

*   Configure o volume como deseja para este usuário (cada usuário tem suas próprias configurações):

```
# alsamixer

```

*   **KDE 3.3** Vá em K Menu > Multimedia > KMix
    *   Selecione Settings > Configure KMix...
    *   Desmarque a opção "Restore volumes on logon"
    *   Pressione OK. Pronto. Agora seus volumes serão os mesmo na linha de comando e dentro do KDE.