**Status de tradução:** Esse artigo é uma tradução de [Intel graphics](/index.php/Intel_graphics "Intel graphics"). Data da última tradução: 2017-02-03\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Intel_graphics&diff=0&oldid=467287) na versão em inglês.

Artigos relacionados

*   [Intel GMA 3600](/index.php/Intel_GMA_3600 "Intel GMA 3600")
*   [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)")
*   [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting")
*   [Xrandr](/index.php/Xrandr "Xrandr")
*   [Hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics")
*   [Vulkan](/index.php/Vulkan "Vulkan")

A Intel provém e suporta drivers de código aberto (open source), portanto as GPU Intel são plug-and-play.

Para uma lista abrangente dos modelos de GPU Intel e processadores, veja [Wikipedia:List of Intel graphics processing units](https://en.wikipedia.org/wiki/List_of_Intel_graphics_processing_units "wikipedia:List of Intel graphics processing units").

**Nota:** PowerVR-based graphics ([GMA 3600](/index.php/Intel_GMA_3600 "Intel GMA 3600") series) não suportam os drivers open source.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Carregando](#Carregando)
    *   [2.1 Habilitando KMS mais cedo no boot](#Habilitando_KMS_mais_cedo_no_boot)
    *   [2.2 Ativar carregamento do firmware GuC / HuC](#Ativar_carregamento_do_firmware_GuC_/_HuC)
*   [3 Configuração do Xorg](#Configuração_do_Xorg)
*   [4 Opções baseadas em módulo](#Opções_baseadas_em_módulo)
    *   [4.1 Compressão Framebuffer (enable_fbc)](#Compressão_Framebuffer_(enable_fbc))
    *   [4.2 Fastboot](#Fastboot)
    *   [4.3 Suporte de virtualização de gráficos Intel GVT-g](#Suporte_de_virtualização_de_gráficos_Intel_GVT-g)
*   [5 Dicas e Truques](#Dicas_e_Truques)
    *   [5.1 Selecionando o modo de scala (scaling mode)](#Selecionando_o_modo_de_scala_(scaling_mode))
    *   [5.2 Aceleração por hardware e Decodificação H.264 em GMA 4500](#Aceleração_por_hardware_e_Decodificação_H.264_em_GMA_4500)
    *   [5.3 Definindo brilho e gama](#Definindo_brilho_e_gama)
*   [6 Resolução de Problemas](#Resolução_de_Problemas)
    *   [6.1 Problemas com SNA](#Problemas_com_SNA)
    *   [6.2 Problemas com DRI3](#Problemas_com_DRI3)
    *   [6.3 Fontes e tela corrompidas em aplicações GTK+ (missing glyphs after suspend/resume)](#Fontes_e_tela_corrompidas_em_aplicações_GTK+_(missing_glyphs_after_suspend/resume))
    *   [6.4 Tela branca durante o boot, enquanto carrega os módulos](#Tela_branca_durante_o_boot,_enquanto_carrega_os_módulos)
    *   [6.5 X trava com o driver intel](#X_trava_com_o_driver_intel)
    *   [6.6 Adicionando resoluções não detectadas](#Adicionando_resoluções_não_detectadas)
    *   [6.7 Problema da escala da cor](#Problema_da_escala_da_cor)
    *   [6.8 O Brilho não está ajustando](#O_Brilho_não_está_ajustando)
    *   [6.9 Desabilitando a compressão do frame buffer](#Desabilitando_a_compressão_do_frame_buffer)
    *   [6.10 Corrupção/Falta de Resposta no Chromium e Firefox](#Corrupção/Falta_de_Resposta_no_Chromium_e_Firefox)
    *   [6.11 Kernel crashing com kernels 4.0+ em placas Broadwell/Core-M](#Kernel_crashing_com_kernels_4.0+_em_placas_Broadwell/Core-M)
    *   [6.12 Suporte à Skylake](#Suporte_à_Skylake)
    *   [6.13 Lag em convidados do Windows (Máquinas Virtuais)](#Lag_em_convidados_do_Windows_(Máquinas_Virtuais))
    *   [6.14 Tela piscando](#Tela_piscando)
*   [7 Veja também](#Veja_também)

## Instalação

Instale o pacote [mesa](https://www.archlinux.org/packages/?name=mesa), que fornece o driver DRI para aceleração 3D.

*   Para suporte a aplicações 32-bit, pode-se instalar o pacote [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) do repositório [multilib](/index.php/Multilib_(Portugu%C3%AAs) "Multilib (Português)").

*   Para o driver DDX (que fornecem a aceleração 2D no [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)")), instale o pacote [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). (Alguns não recomendam a instalação do driver Intel, veja a nota abaixo)

*   Para o suporte OpenGL, instale [mesa](https://www.archlinux.org/packages/?name=mesa). Se você usa x86_64 e precisa de suporte 32-bits, instale também [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) do repositório [multilib](/index.php/Multilib_(Portugu%C3%AAs) "Multilib (Português)").

*   Para o suporte ao [Vulkan](/index.php/Vulkan "Vulkan") (*Ivy Bridge* em diante), instale [vulkan-intel](https://www.archlinux.org/packages/?name=vulkan-intel).

Não se esqueça de checar [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

**Nota:** Existe uma discussão ([Debian & Ubuntu](http://www.phoronix.com/scan.php?page=news_item&px=Ubuntu-Debian-Abandon-Intel-DDX), [Fedora](http://www.phoronix.com/scan.php?page=news_item&px=Fedora-Xorg-Intel-DDX-Switch), [KDE](https://community.kde.org/Plasma/5.9_Errata#Intel_GPUs)) em que alguns não recomendam instalar o driver [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), deixando apenas o modesetting driver para a quarta geração em diante das GPUs. Veja [[1]](https://www.reddit.com/r/archlinux/comments/4cojj9/it_is_probably_time_to_ditch_xf86videointel/), [[2]](http://www.phoronix.com/scan.php?page=article&item=intel-modesetting-2017&num=1), [Xorg#Instalação](/index.php/Xorg_(Portugu%C3%AAs)#Instalação "Xorg (Português)"), e [modesetting(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/modesetting.4). Entretanto, o driver modesetting pode também causar alguns problemas [Chromium Issue 370022](https://bugs.chromium.org/p/chromium/issues/detail?id=370022). Além disso, o driver modesetting não será beneficiado pelo firmware Intel GuC / HuC / DMC.

## Carregando

O Intel kernel module carrega automaticamente na inicialização do sistema

Caso isso não aconteça, então:

*   Tenha certeza de que você não tem `nomodeset` ou {ic|1=vga=}} como um [parâmetro do kernel](/index.php/Par%C3%A2metro_do_kernel "Parâmetro do kernel"), visto que as GPU's Intel necessitam do kernel mode-setting.
*   Também, cheque se você não desabilitou o driver, utilizando algum modprobe blacklisting `/etc/modprobe.d/` ou `/usr/lib/modprobe.d/`.

### Habilitando KMS mais cedo no boot

O [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) é utilizado pelas placas Intel que usam o driver i915 DRM, sendo ativado como padrão.

Em [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") encontram-se instruções para se ativar o KMS o mais cedo o possível no processo de inicialização.

### Ativar carregamento do firmware GuC / HuC

Para o Skylake e os processadores mais recentes, alguns recursos de vídeo (por exemplo, controle de taxa CBR no modo de codificação de baixa energia SKL) podem exigir o uso de um firmware de GPU atualizado, que atualmente (a partir de 4.16) não está habilitado por padrão. Ativar o carregamento do firmware GuC / HuC pode causar problemas em alguns sistemas; desative-o se tiver congelamento (por exemplo, após sair da hibernação).

**Nota:** Veja [Gentoo:Intel#Feature support](https://wiki.gentoo.org/wiki/Intel#Feature_support "gentoo:Intel") para uma visão geral das gerações de processadores Intel.

Para esses processadores, é necessário adicionar `i915.enable_guc=2` aos [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") para ativar o carregamento do firmware. Alternativamente, se o [initramfs](/index.php/Initramfs_(Portugu%C3%AAs) "Initramfs (Português)") já inclui o módulo `i915` (veja [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting")), você pode definir estas opções através de um arquivo em `/etc/modprobe.d/`, por exemplo:

 `/etc/modprobe.d/i915.conf`  `options i915 enable_guc=2` 

É possível habilitar o carregamento do firmware GuC / HuC e o envio de GuC usando o parâmetro do módulo `enable_guc=3`, embora isso geralmente seja desencorajado e possa afetar negativamente a estabilidade do sistema.

Você pode verificar se ambos estão ativados usando [dmesg](/index.php/Dmesg_(Portugu%C3%AAs) "Dmesg (Português)"):

 `$ dmesg` 
```
[drm] HuC: Loaded firmware i915/kbl_huc_ver02_00_1810.bin (version 2.0)
[drm] GuC: Loaded firmware i915/kbl_guc_ver9_39.bin (version 9.39)
i915 0000:00:02.0: GuC firmware version 9.39
i915 0000:00:02.0: GuC submission enabled
i915 0000:00:02.0: HuC enabled
```

Alternativamente, verifique usando:

```
# cat /sys/kernel/debug/dri/0/i915_huc_load_status
# cat /sys/kernel/debug/dri/0/i915_guc_load_status

```

**Atenção:** Usando [GVT-g graphics virtualization](/index.php/Intel_GVT-g "Intel GVT-g") definindo `enable_gvt=1` não é suportado a partir do linux 4.20.11 quando o GuC/HuC também está ativado. O módulo i915 falharia ao inicializar conforme mostrado no system journal. `$ journalctl` 
```
... kernel: [drm:intel_gvt_init [i915]] *ERROR* i915 GVT-g loading failed due to Graphics virtualization is not yet supported with GuC submission
... kernel: i915 0000:00:02.0: [drm:i915_driver_load [i915]] Device initialization failed (-5)
... kernel: i915: probe of 0000:00:02.0 failed with error -5
... kernel: snd_hda_intel 0000:00:1f.3: failed to add i915 component master (-19)

```

## Configuração do Xorg

Pode não haver necessidade de qualquer configuração para executar o [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)").

No entanto, se o [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") não iniciar, para tirar proveito de algumas opções do driver, você poderá criar um arquivo de configuração do Xorg similar ao que se encontra abaixo:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
EndSection
```

Opções adicionais devem ser adicionadas pelo usuário nas linhas abaixo de: `Driver`. Para conhecer todas as opções que podem ser adicionadas ao driver, veja a man page [intel(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/intel.4).

**Nota:**

*   Talvez seja preciso indicar a `Option "AccelMethod"` ao se criar um arquivo de configuração, mesmo que seja para indicar o método padrão (`"sna"`); senão o X pode vir a travar.
*   Pode-se ser necessário adicionar mais seções de {{|Device}} do que a apresentada acima. Indicaremos quando necessário.

## Opções baseadas em módulo

O módulo do kernel `i915` permite configurações via [opções de módulos](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). Algumas delas modificam as opções de economia de energia.

Uma lista com todas as opções, suas descrições e valores padrão podem ser geradas com o seguinte comando:

```
$ modinfo -p i915

```

Para checar o que está ativado, digite:

```
# systool -m i915 -av

```

Muitas opções tomam por padrão a íntegra -1, que assume os padrões do hardware. Contudo, é possível configurar opções mais agressivas de economia de energia utilizando [opções de módulo](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). Também é possível desabilitar a economia de energia por completo.

**Atenção:** Utilizar outras opções que não sejam as padrões dos chips é considerado experimental: [tainted](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=fc9740cebc3ab7c65f3c5f6ce0caf3e4969013ca).

### Compressão Framebuffer (enable_fbc)

O uso da compressão Framebuffer (FBC) pode reduzir o consumo de energia e, ao mesmo tempo, reduzir a largura de banda de memória necessária para as atualizações de tela.

Para ativar o FBC, use `i915.enable_fbc=1` como [parâmetro do kernel](/index.php/Par%C3%A2metro_do_kernel "Parâmetro do kernel") ou defina em `/etc/modprobe.d/i915.conf`:

 `/etc/modprobe.d/i915.conf`  `options i915 enable_fbc=1` 
**Nota:** A compressão do framebuffer pode não ser confiável ou não estar disponível nas gerações da GPU Intel antes do Sandy Bridge (geração 6). Isso resulta em mensagens registradas no diário do sistema semelhante a esta:
```
kernel: drm: not enough stolen space for compressed buffer, disabling.

```

A ativação da compressão do buffer de quadros em CPUs anteriores ao Sandy Bridge resulta em mensagens de erro infinitas:

 `$ dmesg` 
```
[ 2360.475430] [drm] not enough stolen space for compressed buffer (need 4325376 bytes), disabling
[ 2360.475437] [drm] hint: you may be able to increase stolen memory size in the BIOS to avoid this

```
A solução é desabilitar a compactação do buffer de quadros, o que aumentará imperceptivelmente o consumo de energia (em torno de 0,06 W). Para desabilitá-lo, adicione `i915.enable_fbc=0` aos parâmetros da linha do kernel. Mais informações sobre os resultados da compressão desativada podem ser encontradas [aqui](http://kernel.ubuntu.com/~cking/power-benchmarking/background-colour-and-framebuffer-compression/).

### Fastboot

O objetivo do Intel Fastboot é preservar o buffer de quadros como configurado pelo BIOS ou [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") para evitar qualquer oscilação até que o [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") tenha iniciado [[3]](https://www.phoronix.com/scan.php?page=news_item&px=MTEwNzc).

Para habilitar o fastboot, defina `i915.fastboot=1` como um [parâmetro do kernel](/index.php/Par%C3%A2metro_do_kernel "Parâmetro do kernel") ou defina em `/etc/modprobe.d/i915.conf`:

 `/etc/modprobe.d/i915.conf`  `options i915 fastboot=1` 
**Atenção:** Esse parâmetro não é habilitado por padrão e pode causar problemas em alguns sistemas antigos (pré-Skylake).[[4]](https://www.phoronix.com/scan.php?page=news_item&px=Intel-Fastboot-Default-2019-Try)

### Suporte de virtualização de gráficos Intel GVT-g

Veja [Intel GVT-g](/index.php/Intel_GVT-g "Intel GVT-g") para detalhes.

## Dicas e Truques

### Selecionando o modo de scala (scaling mode)

Isso pode ser útil para algumas aplicações de tela inteira:

```
$ xrandr --output LVDS1 --set PANEL_FITTING *param*

```

Onde `*param*` pode ser:

*   `center`: A resolução vai ser mantida, nenhum método de escala será ativado.
*   `full`: Escala a resolução para se adequar à tela inteira.
*   `full_aspect`: Escala a resolução para o maior valor possível que mantenha a proporção.

Se não funcionar, tente:

```
$ xrandr --output LVDS1 --set "scaling mode" *param*

```

onde `*param*` é um entre: `"Full"`, `"Center"` or `"Full aspect"`.

**Nota:** Essa opcão atualmente não funciona para displays externos (exemplos: VGA, DVI, HDMI, DP). [[5]](https://bugs.freedesktop.org/show_bug.cgi?id=90989)

### Aceleração por hardware e Decodificação H.264 em GMA 4500

O pacote [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) fornece apenas descodificação MPEG-2 para GPU's da série GMA 4500\. O suporte de decodificação H.264 é mantido em um ramo separado g45-h264, que pode ser usado ao instalar o pacote [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/). Note-se, porém, que este suporte é experimental e seu desenvolvimento foi abandonado. Usar a VA-API com este driver em uma GPU GMA 4500 series irá descarregar a CPU, mas pode não resultar em uma reprodução tão suave quanto a reprodução não acelerada. Testes usando mplayer mostraram que usar o vaapi para reproduzir um vídeo 1080p codificado em H.264 reduziu para metade a carga da CPU (em comparação com a sobreposição XV), mas resultou em reprodução muito irregular, enquanto 720p funcionou razoavelmente bem [[6]](https://bbs.archlinux.org/viewtopic.php?id=150550). Há também outras experiências [[7]](http://www.emmolution.org/?p=192&cpage=1#comment-12292). Definir o tamanho do canal de vídeo pré-alocado maior na bios resulta em uma reprodução de decodificada pelo hardware muito melhor. Mesmo 1080p h264 funciona bem se isso for feito. A reprodução suave (1080p / 720p) também funciona com [mpv-git](https://aur.archlinux.org/packages/mpv-git/) em combinação com [ffmpeg-git](https://aur.archlinux.org/packages/ffmpeg-git/) e [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/). Com o MPV e o plug-in do Firefox "Watch with MPV" [[8]](https://addons.mozilla.org/de/firefox/addon/watch-with-mpv/), é possível assistir vídeos do YouTube acelerados por hardware.

### Definindo brilho e gama

Veja [Backlight](/index.php/Backlight "Backlight").

## Resolução de Problemas

### Problemas com SNA

*SNA* é o método padrão de aceleração do driver [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). Se você enfrenta problemas com o *SNA* (e.g. pixelated graphics (gráficos pixelados?), texto corrompido, etc.), ente usar *UXA*, o que pode ser feito ao adicionar a seguinte linha ao seu arquivo de configuração Xorg: [arquivo de configuração](#Configuração_do_Xorg):

```
Option      "AccelMethod"  "uxa"

```

Veja [intel(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/intel.4) sobre `Option "AccelMethod"`.

### Problemas com DRI3

*DRI3* é padrão em [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). Podem surgir alguns problemas em alguns sistemas, como: [this](https://bugs.chromium.org/p/chromium/issues/detail?id=370022). Para mudar para *DRI2* adicione a seguinte linha ao seu arquivo de configuração do Xorg: [arquivo de configuração](#Configuração_do_Xorg):

```
Option "DRI" "2"

```

### Fontes e tela corrompidas em aplicações GTK+ (missing glyphs after suspend/resume)

Se você tiver missing font glyphs (glifos de fontes faltando ?) em aplicações GTK+, este método pode ajudar. Edite `/etc/environment` e a dicione a linha abaixo:

 `/etc/environment`  `COGL_ATLAS_DEFAULT_BLIT_MODE=framebuffer` 

Veja também [FreeDesktop bug 88584](https://bugs.freedesktop.org/show_bug.cgi?id=88584).

### Tela branca durante o boot, enquanto carrega os módulos

Se estiver carregando o KMS mais tarde no boot ("late start") KMS e a tela ficar branca enquanto carregar os módulos, pode ajudar se adicionar `i915` e `intel_agp` para o initramfs. Veja a sessão [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting").

Outra alternativa, seria adicionar o seguinte [parâmetro do kernel](/index.php/Par%C3%A2metro_do_kernel "Parâmetro do kernel"):

```
video=SVIDEO-1:d

```

Se você precisa de saída para VGA, tente isso:

```
video=VGA-1:1280x800

```

### X trava com o driver intel

Alguns problemas com o X travando, o bloqueio da GPU ou problemas com o congelamento do X podem ser corrigidos desativando o uso da GPU com a opção `NoAccel` - adicione as seguintes linhas ao seu[arquivo de configuração](#Configuração_do_Xorg):

```
  Option "NoAccel" "True"

```

Alternativamente, tente desabolitar a aceleração 3D com a opção `DRI`:

```
  Option "DRI" "False"

```

Se o seu sistema travar e tiver

```
Option "TearFree" "true"
Option "AccelMethod" "sna"

```

no seu arquivo de configuração, na maioria dos casos isso pode ser corrigido ao se adicionar

```
i915.semaphores=1

```

aos seus parâmetros de boot.

Se você estiver usando o kernel 4.0.X ou superior na arquitetura Baytrail e o sistema travar frequentemente (especialmente ao assistir a vídeo ou usando GFX intensivamente), você deve tentar adicionar a seguinte opção do kernel como uma solução alternativa, até [https: // bugzilla. Kernel.org/show_bug.cgi?id=109051 este bug] ser corrigido permanentemente.

```
 intel_idle.max_cstate=1

```

### Adicionando resoluções não detectadas

Este problema está coberto em: [Xrandr](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr").

### Problema da escala da cor

O Kernel 3.9 [contém](http://lists.freedesktop.org/archives/dri-devel/2013-January/033576.html) um novo modo "Automático" padrão para a propriedade "Broadcast RGB" no driver Intel. É quase equivalente a "Limited 16: 235" (em vez do antigo padrão "Full") sempre que uma saída HDMI / DP está em um [modo CEA](http://raspberrypi.stackexchange.com/questions/7332/what-is-the-difference-between-cea-and-dmt). Se um monitor não suporta o sinal em uma faixa de cores limitada, ele causará problemas nas cores.

**Nota:** Aguns monitores/TVs suportam as duas escalas de cores. Nesse caso, uma opção frequentemente conhecida como *Black Level* pode precisar ser ajustada para fazê-los lidar com o sinal corretamente. Algumas TVs podem manipular o sinal somente em alcance limitado. Definir RGB de difusão para "Completo" fará um "Collor Clipping". Você pode precisar configurá-lo para "Limited 16: 235" manualmente para evitar o "Clipping".

Pode-se forçar o modo com: `xrandr --output <HDMI> --set "Broadcast RGB" "Full"` (substitua `<HDMI>` pelo dispositivo correto, rodando `xrandr`).

Infelizmente, o driver Intel não suporta a configuração do intervalo de cores através de um arquivo de configuração `xorg.conf.d`.

Um [bug report](https://bugzilla.kernel.org/show_bug.cgi?id=94921) foi postado e um patch pode ser encontrado em anexo.

Também existem outros problemas relacionados que podem ser corrigidos editando registros GPU. Mais informações podem ser encontradas em [[9]](http://lists.freedesktop.org/archives/intel-gfx/2012-April/016217.html) e [[10]](http://github.com/OpenELEC/OpenELEC.tv/commit/09109e9259eb051f34f771929b6a02635806404c).

### O Brilho não está ajustando

Se depois de retomar a suspensão, as teclas de atalho para alterar o brilho da tela não tiverem efeito, verifique sua configuração em relação ao artigo [Backlight](/index.php/Backlight "Backlight").

Se o problema persistir, tente um dos seguintes [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel"):

```
acpi_osi=Linux
acpi_osi="!Windows 2012"
acpi_osi=

```

### Desabilitando a compressão do frame buffer

Habilitando a compressão do frame buffer em CPUs pré Sandy Bridge resulta em incontáveis mensagens de erro:

```
$ dmesg |tail 
[ 2360.475430] [drm] not enough stolen space for compressed buffer (need 4325376 bytes), disabling
[ 2360.475437] [drm] hint: you may be able to increase stolen memory size in the BIOS to avoid this

```

The solution is to disable frame buffer compression which will imperceptibly increase power consumption (around 0.06 W). In order to disable it add `i915.enable_fbc=0` to the kernel line parameters. More information on the results of disabled compression can be found [here](http://kernel.ubuntu.com/~cking/power-benchmarking/background-colour-and-framebuffer-compression/).

### Corrupção/Falta de Resposta no Chromium e Firefox

Se você tiver alguma corrupção ou falta de resposta no Chromium e/ou no Firefox [configure o AccelMethod para "uxa"](#Problemas_com_SNA).

### Kernel crashing com kernels 4.0+ em placas Broadwell/Core-M

Alguns segundos após o X/Wayland carregar, o sistema trava e o journalctl apresenta um log como o seguinte:

```
Jun 16 17:54:03 hostname kernel: BUG: unable to handle kernel NULL pointer dereference at           (null)
Jun 16 17:54:03 hostname kernel: IP: [<          (null)>]           (null)
...
Jun 16 17:54:03 hostname kernel: CPU: 0 PID: 733 Comm: gnome-shell Tainted: G     U     O    4.0.5-1-ARCH #1
...
Jun 16 17:54:03 hostname kernel: Call Trace:
Jun 16 17:54:03 hostname kernel:  [<ffffffffa055cc27>] ? i915_gem_object_sync+0xe7/0x190 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa0579634>] intel_execlists_submission+0x294/0x4c0 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa05539fc>] i915_gem_do_execbuffer.isra.12+0xabc/0x1230 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa055d349>] ? i915_gem_object_set_to_cpu_domain+0xa9/0x1f0 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffff811ba2ae>] ? __kmalloc+0x2e/0x2a0
Jun 16 17:54:03 hostname kernel:  [<ffffffffa0555471>] i915_gem_execbuffer2+0x141/0x2b0 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa042fcab>] drm_ioctl+0x1db/0x640 [drm]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa0555330>] ? i915_gem_execbuffer+0x450/0x450 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffff8122339b>] ? eventfd_ctx_read+0x16b/0x200
Jun 16 17:54:03 hostname kernel:  [<ffffffff811ebc36>] do_vfs_ioctl+0x2c6/0x4d0
Jun 16 17:54:03 hostname kernel:  [<ffffffff811f6452>] ? __fget+0x72/0xb0
Jun 16 17:54:03 hostname kernel:  [<ffffffff811ebec1>] SyS_ioctl+0x81/0xa0
Jun 16 17:54:03 hostname kernel:  [<ffffffff8157a589>] system_call_fastpath+0x12/0x17
Jun 16 17:54:03 hostname kernel: Code:  Bad RIP value.
Jun 16 17:54:03 hostname kernel: RIP  [<          (null)>]           (null)

```

Isso pode ser corrigido desabilitando o suporte a execlist que foi alterado para o padrão com o kernel 4.0\. Adicione o seguinte [parâmetro do kernel](/index.php/Par%C3%A2metro_do_kernel "Parâmetro do kernel"):

```
i915.enable_execlists=0

```

Isso é conhecido por ser quebrado para pelo menos kernel 4.0.5.

### Suporte à Skylake

The i915 DRM driver is known to cause various GPU hangs, crashes and even full system freezes. It might be necessary to disable hardware acceleration to workaround these issues. One solution is to use the following Xorg configuration.

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
	Identifier  "Intel Graphics"
	Driver      "intel"
	Option	    "DRI"	"false"
EndSection

```

Aplicativos específicos, como os navegadores Chromium e Firefox, podem ser instruídos a desativar a renderização de hardware diretamente.

Outra opção que parece funcionar para alguns usuários é adicionar o parâmetro de inicialização do kernel `i915.enable_rc6=0`, o que fará com que a CPU / GPU permaneça em modos de alta potência, mas parece resolver a maioria Casos de GPU trava e sistema congela.

**Nota:** Se o sistema aparecer pendurado após "Loading Initial Ramdisk", certifique-se de que o tamanho de abertura IGD no BIOS seja inferior a 4GB.

### Lag em convidados do Windows (Máquinas Virtuais)

A saída de vídeo de um convidado do Windows (windows guest) no VirtualBox às vezes trava até que o host force uma atualização de tela (por exemplo, movendo o cursor do mouse). A remoção da opção `enable_fbc=1` corrige este problema.

### Tela piscando

Os seguintes recursos de economia de energia usados por intel iGPUs são conhecidos por causar cintilação em alguns casos. Uma solução temporária é desativar um deles usando a opção [kernel boot parameter](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") apropriada:

*   Rc6 sleep modes (ver [#RC6 sleep modes (enable_rc6)](#RC6_sleep_modes_(enable_rc6))), pode ser desabilitado com `i915.enable_rc6=0`.

*   *Panel Self Refresh (PSR) [FS#49628](https://bugs.archlinux.org/task/49628) [FS#49371](https://bugs.archlinux.org/task/49371) [FS#50605](https://bugs.archlinux.org/task/50605), ativado por padrão desde o kernel mainline 4.6\. Para desativar esse recurso, use a opção `i915.enable_psr=0`.

## Veja também

*   [https://01.org/linuxgraphics/documentation](https://01.org/linuxgraphics/documentation) (lista dos hardwares suportados)