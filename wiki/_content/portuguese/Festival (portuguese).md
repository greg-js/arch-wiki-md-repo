**Status de tradução:** Esse artigo é uma tradução de [Festival](/index.php/Festival "Festival"). Data da última tradução: 2019-11-09\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Festival&diff=0&oldid=588366) na versão em inglês.

[Festival](http://www.cstr.ed.ac.uk/projects/festival/) é um sistema geral de síntese de fala multilíngue desenvolvido no CSTR ([Centre for Speech Technology Research](http://www.cstr.ed.ac.uk/)).

O Festival oferece uma estrutura geral para a construção de sistemas de síntese de voz, incluindo exemplos de vários módulos. Como um todo, ele oferece texto completo para fala por meio de um número de APIs: do nível de shell, embora um interpretador de comandos Scheme, como uma biblioteca C ++, de Java e uma interface Emacs. O festival é multilíngue (atualmente inglês britânico, inglês americano, italiano, tcheco e espanhol, com outros idiomas disponíveis em protótipo).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
    *   [1.1 Usando a extensão de IMS alemão para festival com mbrola](#Usando_a_extensão_de_IMS_alemão_para_festival_com_mbrola)
*   [2 Configuração](#Configuração)
    *   [2.1 Uso com um servidor de som](#Uso_com_um_servidor_de_som)
    *   [2.2 Vozes](#Vozes)
        *   [2.2.1 Patches de compatibilidade com HTS](#Patches_de_compatibilidade_com_HTS)
        *   [2.2.2 Instalação manual de voz](#Instalação_manual_de_voz)
*   [3 Uso](#Uso)
    *   [3.1 Modo interativo (testar voz etc.)](#Modo_interativo_(testar_voz_etc.))
    *   [3.2 Exemplo de script](#Exemplo_de_script)
*   [4 Solução de problemas](#Solução_de_problemas)
    *   [4.1 Não é possível abrir /dev/dsp](#Não_é_possível_abrir_/dev/dsp)
    *   [4.2 Alsa reproduzindo na velocidade errada](#Alsa_reproduzindo_na_velocidade_errada)
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

### Vozes

Arch divide o conjunto de vozes oficiais em [festival-english](https://www.archlinux.org/packages/?name=festival-english) e [festival-us](https://www.archlinux.org/packages/?name=festival-us). [O AUR](https://aur.archlinux.org/packages/?K=festival) possui alguns outros, em vários estados de manutenção que podem ou não estar funcionando no momento.

Para ver quais vozes você instalou e qual é o seu padrão, acesse o shell do Festival (que é um esquema REPL) e digite o seguinte (algum espaço adicionado para maior clareza):

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
   voice_cmu_us_slt_arctic_hts          ;;<-- ESTA É A VOZ COM A QUAL FESTIVAL FALA

   festival> default-voice-priority-list 
   (kal_diphone                         ;;<-- ESTA É A LISTA CODIFICADA DE VOZES DE FESTIVAL VÊM COM SUPORTE
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

   festival> (voice_                    ;;<-- PRESSIONE TAB AQUI PARA VER QUE VOZES FESTIVAL TEM DISPONÍVEL
   voice_cmu_us_slt_arctic_hts     voice_kal_diphone               voice_nitech_us_slt_arctic_hts  voice_reset
   voice_default                   voice_nitech_us_clb_arctic_hts  voice_rab_diphone

   festival> (voice_cmu_us_slt_arctic_hts) 
   cmu_us_slt_arctic_hts

   festival> (SayText "Arch makes me happy")
   #<Utterance 0x7fb5b8c423b0>

   festival> 

```

Para alterar permanentemente a voz padrão, você pode adicionar uma linha como esta ao final de `~/.festivalrc`:

```
 (set! voice_default voice_cmu_us_slt_arctic_hts)

```

Você não pode definir a voz com festival.scm; para definir vozes globalmente, defina a ordem das vozes pesquisadas em `/usr/share/festival/voices.scm`.

#### Patches de compatibilidade com HTS

Alguns dizem que as vozes HTS para o Festival são as melhores disponíveis gratuitamente. Infelizmente, eles não são compatíveis com o Festival> 2.1 sem corrigi-lo (e as novas versões de voz não são disponibilizadas para download).

Você pode instalar a versão corrigida em [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"): [festival-patched-hts](https://aur.archlinux.org/packages/festival-patched-hts/) e [festival-hts-voices-patched](https://aur.archlinux.org/packages/festival-hts-voices-patched/)

#### Instalação manual de voz

Você também pode obter vozes diretamente em [festvox.org](http://festvox.org/festival/downloads.html). Nos downloads, os arquivos denominados `festvox_*.tgz` contêm uma voz diferente, criada pela equipe do festival. Eles funcionam, mas você precisará descompactar manualmente e mover a pasta que contém a voz para o local apropriado. Em um arco recente, o local apropriado é `/usr/share/festival/voices/english/` e a maneira de saber qual pasta contém a voz é procurar uma subpasta `festvox/` dentro dela.

Você pode testar se suas novas vozes foram encontradas carregando o prompt do festival novamente.

## Uso

Ler um arquivo texto:

```
$ festival --tts /caminho/para/carta.txt

```

Ser desagradável ao demonstrar a encadeamento

```
$ (echo "Get ready for some pain"; sudo cat /var/log/messages.log) | festival --tts

```

Converter um arquivo de texto para mp3:

```
$ cat carta.txt | text2wave | lame - arquivo.mp3 && mplayer arquivo.mp3

```

### Modo interativo (testar voz etc.)

O festival tem um prompt interativo que você pode usar para testar. Alguns exemplos (com saída de amostra):

```
$ festival 
[...]
festival> 

```

Lista vozes disponíveis:

```
festival> (voice.list)
(cstr_us_awb_arctic_multisyn kal_diphone don_diphone)

```

Define a voz:

```
festival> (voice_cstr_us_awb_arctic_multisyn)
#<voice 0x1545b90>

```

Fala:

```
festival> (SayText '"test this is a test oh no a test bla test")
inserting pause after: t.
Inserting pause
[...]
id _63 ; name t ; 
id _65 ; name # ; 
#<Utterance 0x7f7c0c144810>

```

Mais:

```
festival> help 
"The Festival Speech Synthesizer System: Help

```

Sair: Ctrl+d ou

```
festival> (quit)

```

### Exemplo de script

Um aplicativo clássico que pode fazer uso disso é o *ping*. Use este script para executar *ping* constantemente em um host e retorna "Ping" se for bem-sucedido; do contrário, "Falha":

```
#!/bin/bash
while :; do
    ping -c 1 $1 && (echo "Ping" | festival --tts) || (echo "Fail" | festival --tts)
done

```

Observe que isso realmente não funciona em vozes multissintéticas, pois elas demoram um pouco para serem preparadas antes da reprodução.

## Solução de problemas

### Não é possível abrir /dev/dsp

Se o festival retornar a seguinte mensagem de erro:

```
Linux: can't open /dev/dsp

```

Veja [#Uso com um servidor de som](#Uso_com_um_servidor_de_som) acima.

### Alsa reproduzindo na velocidade errada

Se a solução acima lhe der uma voz estridente, convém alterar suas opções de jogo:

```
(Parameter.set 'Audio_Method 'Audio_Command)
(Parameter.set 'Audio_Command "aplay -Dplug:default -f S16_LE -r $SR $FILE")

```

### O comando aplay não funciona

[Instale](/index.php/Instale "Instale") [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils).

## Veja também

*   [Manual do Festival](http://www.cstr.ed.ac.uk/projects/festival/manual/)