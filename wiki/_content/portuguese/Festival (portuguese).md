[Festival](http://www.cstr.ed.ac.uk/projects/festival/) é um sistema geral de síntese de fala multilíngue desenvolvido no CSTR ([Centre for Speech Technology Research](http://www.cstr.ed.ac.uk/)).

O Festival oferece uma estrutura geral para a construção de sistemas de síntese de voz, incluindo exemplos de vários módulos. Como um todo, ele oferece texto completo para fala por meio de um número de APIs: do nível de shell, embora um interpretador de comandos Scheme, como uma biblioteca C ++, de Java e uma interface Emacs. O festival é multilíngue (atualmente inglês britânico, inglês americano, italiano, tcheco e espanhol, com outros idiomas disponíveis em protótipo).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
    *   [1.1 Usando a extensão de IMS alemão para festival com mbrola](#Usando_a_extensão_de_IMS_alemão_para_festival_com_mbrola)
*   [2 Configuração](#Configuração)
    *   [2.1 Uso com um servidor de som](#Uso_com_um_servidor_de_som)
    *   [2.2 Voz](#Voz)
        *   [2.2.1 Patches de compatibilidade com HTS](#Patches_de_compatibilidade_com_HTS)
        *   [2.2.2 Instalação manual de voz](#Instalação_manual_de_voz)
*   [3 Uso](#Uso)
    *   [3.1 Modo interativo (testar voz etc.)](#Modo_interativo_(testar_voz_etc.))
    *   [3.2 Exemplo de script](#Exemplo_de_script)
*   [4 Solução de problemas](#Solução_de_problemas)
    *   [4.1 Não é possível abrir /dev/dsp](#Não_é_possível_abrir_/dev/dsp)
    *   [4.2 Alsa playing at wrong speed](#Alsa_playing_at_wrong_speed)
    *   [4.3 O comando aplay não funciona](#O_comando_aplay_não_funciona)
*   [5 Veja também](#Veja_também)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [festival](https://www.archlinux.org/packages/?name=festival). Você precisa de um pacote de voz como [festival-english](https://www.archlinux.org/packages/?name=festival-english) ou [festival-us](https://www.archlinux.org/packages/?name=festival-us).

Teste festival:

```
$ echo "This is an example. Arch is the best." | festival --tts

```

Se você ouvir todo o texto do exemplo, você instalou com sucesso um sistema TTS.

Se você não ouvir nada, consulte a seção [Solução de problemas](#Solução_de_problemas). Se você tiver um sistema desktop, você quase certamente receberá uma mensagem sobre `/dev/dsp` e precisará seguir essas instruções.

### Usando a extensão de IMS alemão para festival com mbrola

Você pode usar o pacote [festival-ims](https://aur.archlinux.org/packages/festival-ims/) com os patches do IMS Stuttgart.

O [Instituto de Processamento de Linguagem Natural (IMS) da Universidade de Stuttgart](http://www.ims.uni-stuttgart.de) desenvolveu uma extensão ao festival especialmente para o idioma alemão. Ela usa vozes alemãs com [mbrola](https://aur.archlinux.org/packages/mbrola/). Para instalá-la, a extensão precisa ser baixada dos servidores da universidade (siga as instruções [aqui](http://www.ims.uni-stuttgart.de/institut/arbeitsgruppen/phonetik/synthesis/festival_opensource.html)) e o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") precisa ser modificado.

Adicione esses dois arquivos baixados do IMS (NÃO use o terceiro arquivo, `ims_german_1.3-os.fix.tgz`)

```
 ims_german_1.3-os.tgz
 bomp_full.corr.tgz

```

com seus md5sums para a variável *source* e coloque-os na mesma pasta que o PKGBUILD. Na seção `prepare()`, inclua as seguintes linhas (no final da seção):

```
   # add ims config
   sed -i 's/ALSO_INCLUDE +=$/# IMS module for German
ALSO_INCLUDE += ims_german_text/' "$srcdir/festival/config/config.in"
   cat<<EOF >> "$srcdir/festival/lib/sitevars.scm"
 (set! mbrola-path "/usr/share/mbrola/")
 (set! mbrola_progname "/usr/bin/mbrola -e")
 EOF
   echo "(require 'ims_german_opensource)" >> "$srcdir/festival/lib/siteinit.scm"

```

Isso deve instalar o suporte para as vozes alemãs `de1` até `de4`. Instale pelo menos uma dessas vozes, p.ex., [mbrola-voices-de2](https://aur.archlinux.org/packages/mbrola-voices-de2/), e depois usá-lo no festival, selecionando a voz via

```
 (voice_german_de2_os)
 (SayText "Hallo Welt.")

```

no prompt ou use-o em *text2wave* via

```
 text2wave -o spoken.wav -eval '(voice_german_de2_os)' *entrada*.txt

```

sendo `*entrada*.txt` o nome do arquivo contendo o texto a ser processado.

## Configuração

Não existe um arquivo de configuração global `/etc`, mas você pode configurar o festival com o seu arquivo `~/.festivalrc` ou editando diretamente `/usr/share/festival/festival.scm`. Ambos são arquivos de esquema, usam sintaxe de esquema e são executados toda vez que o festival é executado.

### Uso com um servidor de som

Para PulseAudio, adicione essas linhas ao final de seu arquivo `~/.festivalrc` ou a `/usr/share/festival/festival.scm`:

```
(Parameter.set 'Audio_Required_Format 'aiff)
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "paplay $FILE --client-name=Festival --stream-name=Speech")

```

Para ALSA, use essas linhas ([fonte](http://ubuntuforums.org/showpost.php?p=4058268&postcount=16)):

```
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "aplay -q -c 1 -t raw -f s16 -r $SR $FILE")

```

### Voz

Arch splits the set of official voices into [festival-english](https://www.archlinux.org/packages/?name=festival-english) and [festival-us](https://www.archlinux.org/packages/?name=festival-us). [The AUR](https://aur.archlinux.org/packages/?K=festival) has some others, in various states of maintenance which may or may not be currently working.

To see what voices you currently have installed and what your default is, go into the Festival shell (which is a scheme REPL) and type the following (some space added for clarity):

```
   $ festival

   Festival Speech Synthesis System 2.1:release November 2010
   Copyright (C) University of Edinburgh, 1996-2010\. All rights reserved.

   clunits: Copyright (C) University of Edinburgh and CMU 1997-2010
   clustergen_engine: Copyright (C) CMU 2005-2010
   hts_engine: 
   The HMM-based speech synthesis system (HTS)
   hts_engine API version 1.04 ([http://hts-engine.sourceforge.net/](http://hts-engine.sourceforge.net/))
   Copyright (C) 2001-2010  Nagoya Institute of Technology
                 2001-2008  Tokyo Institute of Technology
   All rights reserved.
   For details type `(festival_warranty)'

   festival> voice_default 
   voice_cmu_us_slt_arctic_hts          ;;<-- THIS IS THE VOICE FESTIVAL SPEAKS WITH

   festival> default-voice-priority-list 
   (kal_diphone                         ;;<-- THIS IS THE HARD-CODED LIST OF VOICES FESTIVAL CAME PRE-AWARE OF
    cmu_us_bdl_arctic_hts
    cmu_us_jmk_arctic_hts
    cmu_us_slt_arctic_hts
    cmu_us_awb_arctic_hts
    ked_diphone
    don_diphone
    rab_diphone
    en1_mbrola
    us1_mbrola
    us2_mbrola
    us3_mbrola
    gsw_diphone
    el_diphone)

   festival> (voice_                    ;;<-- PRESS TAB HERE TO SEE WHAT VOICES FESTIVAL HAS AVAILABLE
   voice_cmu_us_slt_arctic_hts     voice_kal_diphone               voice_nitech_us_slt_arctic_hts  voice_reset
   voice_default                   voice_nitech_us_clb_arctic_hts  voice_rab_diphone

   festival> (voice_cmu_us_slt_arctic_hts) 
   cmu_us_slt_arctic_hts

   festival> (SayText "Arch makes me happy")
   #<Utterance 0x7fb5b8c423b0>

   festival> 

```

To permanently change the default voice you can add a line like this to the end of `~/.festivalrc`:

```
(set! voice_default voice_cmu_us_slt_arctic_hts)

```

You cannot set the voice with festival.scm; to set voices globally, set order of searched voices in `/usr/share/festival/voices.scm`.

#### Patches de compatibilidade com HTS

Some say that HTS voices for Festival are the best ones freely available. Sadly they are not compatible with Festival >2.1 without patching it (and the new voice versions are not made available for downloading).

You can install the patched version from [AUR](/index.php/AUR "AUR"): [festival-patched-hts](https://aur.archlinux.org/packages/festival-patched-hts/) and [festival-hts-voices-patched](https://aur.archlinux.org/packages/festival-hts-voices-patched/)

#### Instalação manual de voz

You can also get voices straight from [festvox.org](http://festvox.org/festival/downloads.html). In their downloads, the files named "festvox_*.tgz" each contain a different voice, as built by the festival team. They do work, but you will need to manually unzip and move the folder containing the voice to the appropriate place. On a recent Arch, the appropriate place is /usr/share/festival/voices/english/ and the way to tell what folder contains the voice is to look for a 'festvox/' subfolder inside of it.

You can then test that your new voices are found by loading up the festival prompt again.

## Uso

Read a text file:

```
$ festival --tts /path/to/letter.txt

```

Be obnoxious while demonstrating piping

```
$ (echo "Get ready for some pain"; sudo cat /var/log/messages.log) | festival --tts

```

Convert a text file to mp3:

```
$ cat letter.txt | text2wave | lame - file.mp3 && mplayer file.mp3

```

### Modo interativo (testar voz etc.)

festival has an interactive prompt you can use for testing. Some examples (with sample output):

```
$ festival 
[...]
festival> 

```

List available voices:

```
festival> (voice.list)
(cstr_us_awb_arctic_multisyn kal_diphone don_diphone)

```

Set voice:

```
festival> (voice_cstr_us_awb_arctic_multisyn)
#<voice 0x1545b90>

```

Speak:

```
festival> (SayText '"test this is a test oh no a test bla test")
inserting pause after: t.
Inserting pause
[...]
id _63 ; name t ; 
id _65 ; name # ; 
#<Utterance 0x7f7c0c144810>

```

More:

```
festival> help 
"The Festival Speech Synthesizer System: Help

```

Quit: ctrl+d or

```
festival> (quit)

```

### Exemplo de script

One classic app that can make use of this is ping. Use this script to constantly ping a host, and return ping if success, fail if not:

```
#!/bin/bash
while :; do
    ping -c 1 $1 && (echo "Ping" | festival --tts) || (echo "Fail" | festival --tts)
done

```

Note that this does not really work on multisynth voices, as they take a while to prepare before playing.

## Solução de problemas

### Não é possível abrir /dev/dsp

If festival returns the following error message:

```
Linux: can't open /dev/dsp

```

See [#Uso com um servidor de som](#Uso_com_um_servidor_de_som) above.

### Alsa playing at wrong speed

If the solution above gives you a squeaky voice, you might want to try changing your aplay options:

```
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "aplay -Dplug:default -f S16_LE -r $SR $FILE")

```

### O comando aplay não funciona

Install [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils).

## Veja também

*   [Festival manual](http://www.cstr.ed.ac.uk/projects/festival/manual/)