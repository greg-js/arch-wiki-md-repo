Este artigo deve servir como um guia para configurações mais avançadas do [ALSA](/index.php/ALSA_(Portugu%C3%AAs) "ALSA (Português)"). A configuração fica armazenada em `/etc/asound.conf` como mencionado no artigo principal. Nenhuma das configurações abaixo tem a garantia de funcionar.

**Note:** A maioria das coisas discutidas aqui são muito mais fácil de se fazer usando plugins do alsa como upmix, que são explicadas no artigo principal.

## Upmixagem de fontes stereo para 7.1 usando dmix enquanto fontes saturadas não fican upmixadas

```
# 2008-11-15
#
# Esse .asoundrc vai permitir o seguinte:
#
# - upmix com arquivos stereo para alto-falantes 7.1.
# - reproduzir sons em 7.1 real, em alto-falantes 7.1,
# - permitir a reprodução de ambas fontes stereo(upmixado) e surround(7.1) ao mesmo tempo
# - usar o 6º e 7º canal (alto-falantes laterais) como uma placa de som separada, i,e, para fones de ouvido
#   (Isso é chamado de saída "alternativa" ao longo deste arquivo, nomes de dispositivos prefixados com 'a')
# - reproduz fontes mono em stereo (como skype & ekiga) na saída alternativa
#
# Certifique-se de ter "8 Channels" e NÃO "6 Channels" selecionado no alsamixer!
#
# Por favor tente os seguintes comandos, para se certificar que tudo está funcionado como deveria.
#
# Testar upmix stereo:       speaker-test -c2 -Ddefault -twav
# Testar surround(5.1):      speaker-test -c6 -Dplug:dmix6 -twav
# Testar surround(7.1):      speaker-test -c6 -Dplug:dmix8 -twav
# Testar saída alternativa:  speaker-test -c2 -Daduplex -twav
# Testar upmix mono:         speaker-test -c1 -Dmonoduplex -twav
#
#
# Ele pode não funcionar sem uma configuração manual para todas as placas. Se não funcionar para você, leia
# os comentários ao longo deste arquivo.
# A base deste arquivo foi escrito por wishie de #alsa e, então, modificado com as informações de várias fontes
# por squisher. Svenstaro modificou-o para suporte a saída 7.1.

# Defina a placa de som para usar
pcm.snd_card {
    type hw
    card 0
    device 0
}

# dmix de 8 canal - saída de qualquer áudio, para todos os 8 alto-faltantes
pcm.dmix8 {
    type dmix
    ipc_key 1024
    ipc_key_add_uid false
    ipc_perm 0660
    slave {
        pcm "snd_card"
        rate 48000
        channels 8
        period_time 0
        period_size 1024
        buffer_time 0
        buffer_size 5120
    }

# Algumas placas, como as variantes "nforce" exigem que o seguinte seja descomentado.
# Ele roteia o áudio para os alto-falantes corretos.
#    bindings {
#        0 0
#        1 1
#        2 4
#        3 5
#        4 2
#        5 3
#        6 6
#        7 7
#    }
}

# upmixing - duplica dados stereo para todos os 8 canais
pcm.ch71dup {
    type route
    slave.pcm dmix8
    slave.channels 8
    ttable.0.0 1
    ttable.1.1 1
    ttable.0.2 1
    ttable.1.3 1
    ttable.0.4 0.5
    ttable.1.4 0.5
    ttable.0.5 0.5
    ttable.1.5 0.5
    ttable.0.6 1
    ttable.1.7 1
}

# isso cria uma placa de som de seis canais
# e emite para o oitavo canal
# i.e. para uso de mplayer, tive que definir em ~/.mplayer/config:
#   ao=alsa:device=dmix6
#   channels=6
pcm.dmix6 {
    type route
    slave.pcm dmix8
    slave.channels 8
    ttable.0.0 1
    ttable.1.1 1
    ttable.2.2 1
    ttable.3.3 1
    ttable.4.4 1
    ttable.5.5 1
    ttable.6.6 1
    ttable.7.7 1
}

# compartilha o microfone, i.e. porque virtualbox pega-o por padrão
pcm.microphone {
    type dsnoop
    ipc_key 1027
    slave {
        pcm "snd_card"
    }
}

# taxa de conversão, necessário para i.e. wine
pcm.2chplug {
    type plug
    slave.pcm "ch71dup"
}
pcm.a2chplug {
    type plug
    slave.pcm "dmix8"
}

# roteia o canal para a alternativa
# saída de 2 canais que se torna o 7º e 8º canal
# na placa de som real
#pcm.alt2ch {
#    type route
#    slave.pcm "a2chplug"
#    slave.channels 8
#    ttable.0.6    1
#    ttable.1.7    1
#}

# skype e ekiga são apenas mono, então roteia canal esquerdo para o canal direito
# nota: isso roteia 2 canais para a alternativa
pcm.mono_playback {
    type route
    slave.pcm "a2chplug"
    slave.channels 8
    # Envia canal 0 do Skype para os alto-falantes L e R no volume máximo
    #ttable.0.6    1
    #ttable.0.7    1
}

# dispositivo "full-duplex" para uso com aoss
pcm.duplex {
    type asym
    playback.pcm "2chplug"
    capture.pcm "microphone"
}

#pcm.aduplex {
#    type asym
#    playback.pcm "alt2ch"
#    capture.pcm "microphone"
#}

pcm.monoduplex {
    type asym
    playback.pcm "mono_playback"
    capture.pcm "microphone"
}

# para aoss
pcm.dsp0 "duplex"
ctl.mixer0 "duplex"

# softvol gerencia volume no alsa
# i.e. wine gosta disso
pcm.mainvol {
    type softvol
    slave.pcm "duplex"
    control {
        name "2ch-Upmix Master"
        card 0
    }
}

#pcm.!default "mainvol"

# define o dispositivo padrão de acordo com o ambiente
# variável ALSA_DEFAULT_PCM e padrão para mainvol
pcm.!default {
    @func refer
    name { @func concat 
           strings [ "pcm."
                     { @func getenv
                       vars [ ALSA_DEFAULT_PCM ]
                       default "mainvol"
                     }
           ]
         }
}

# descomente o seguinte se você deseja ser capaz de controlar
# o dispositivo mixador também por meio de variáveis de ambiente
#ctl.!default {
#    @func refer
#    name { @func concat 
#           strings [ "ctl."
#                     { @func getenv
#                       vars [ ALSA_DEFAULT_CTL
#                              ALSA_DEFAULT_PCM
#                       ]
#                       default "duplex"
#                     }
#           ]
#         }
#}

```

## Surround51 incl. stereo de upmix & dmix, troca L/R, alto-falante em posição ruim na sala

Prática ruim, mas funciona bem para a quase tudo sem personalização adicional per-programa/arquivo:

```
pcm.!default {
    type route
## encaminha para mixer pcm definido abaixo
    slave.pcm dmix51
    slave.channels 6

## "Canais Nativos" stereo, troca esquerda/direita
    ttable.0.1 1
    ttable.1.0 1
## esquerda/direita original comentada
#    ttable.0.0 1
#    ttable.1.1 1

## rota "surround nativo" de forma que ele ainda funcione, mas com sinal
## mais fraco (+ troca RL/RF), porque meus alto-falantes traseiros são
## mais aleatórios do que realmente atrás de mim
    ttable.2.3 0.7
    ttable.3.2 0.7
    ttable.4.4 0.7
    ttable.5.5 0.7

## stereo => "upmix" de quatro alto-falantes para alto-falantes "traseiros" + troca L/R
    ttable.0.3 1
    ttable.1.2 1

## stereo L+R => junta ao Centro & Subwoofer 50%/50%
    ttable.0.4 0.5
    ttable.1.4 0.5
    ttable.0.5 0.5
    ttable.1.5 0.5
## para testar: "$ speaker-test -c6 -twav" e: "$ speaker-test -c2 -twav"
}

pcm.dmix51 {
	type dmix
	ipc_key 1024
# deixe múltiplos usuários compartilhar
	ipc_key_add_uid false 
# permissões IPC (octal, padrão 0600)
# acho que alterar isso corrigiu algo - mas não tenho certeza do quê.
	ipc_perm 0660 # 
	slave {
## isso é específico para meu hda_intel. Geralmente hd:0 já está bom; Para localizar: $ aplay -L 
		pcm surround51 
# essa taxa faz minha placa de som crepitar
#		rate 44100
# essa taxa evita flash o firefox de reproduzir som, mas eu não preciso disso
       rate 48000
       channels 6
## Quaisquer outros valores nas 4 linhas abaixo parecem fazer minha placa de som crepitar também
       period_time 0
       period_size 1024
       buffer_time 0
       buffer_size 4096
	}
}

```