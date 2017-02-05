A Intel provém e suporta drivers de código aberto (open source), portanto as GPU Intel são plug-and-play.

Para uma lista abrangente dos modelos de GPU Intel e processadores, veja [this comparison on Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_Intel_graphics_processing_units "wikipedia:Comparison of Intel graphics processing units").

**Nota:** PowerVR-based graphics ([GMA 500](/index.php/Intel_GMA_500 "Intel GMA 500") and [GMA 3600](/index.php/Intel_GMA_3600 "Intel GMA 3600") series) não suportam os drivers open source.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Carregando](#Carregando)
    *   [2.1 Habilitando KMS mais cedo no boot](#Habilitando_KMS_mais_cedo_no_boot)
*   [3 Configuração do Xorg](#Configura.C3.A7.C3.A3o_do_Xorg)
*   [4 Opções de economia de energia](#Op.C3.A7.C3.B5es_de_economia_de_energia)
    *   [4.1 RC6 sleep modes (enable_rc6)](#RC6_sleep_modes_.28enable_rc6.29)
    *   [4.2 Compressão Framebuffer (enable_fbc)](#Compress.C3.A3o_Framebuffer_.28enable_fbc.29)
*   [5 Dicas e Truques](#Dicas_e_Truques)
    *   [5.1 Tear-free video (Video sem glitches)](#Tear-free_video_.28Video_sem_glitches.29)
    *   [5.2 Disable Vertical Synchronization (VSYNC)](#Disable_Vertical_Synchronization_.28VSYNC.29)
    *   [5.3 Selecionando o modo de scala (scaling mode)](#Selecionando_o_modo_de_scala_.28scaling_mode.29)
    *   [5.4 Problemas com o KMS: o console é limitado a uma área pequena](#Problemas_com_o_KMS:_o_console_.C3.A9_limitado_a_uma_.C3.A1rea_pequena)
    *   [5.5 Decodificação H.264 em GMA 4500](#Decodifica.C3.A7.C3.A3o_H.264_em_GMA_4500)
    *   [5.6 Definindo brilho e gama](#Definindo_brilho_e_gama)
*   [6 Resolução de Problemas](#Resolu.C3.A7.C3.A3o_de_Problemas)
    *   [6.1 Problemas com SNA](#Problemas_com_SNA)
    *   [6.2 Problemas com DRI3](#Problemas_com_DRI3)
    *   [6.3 Fontes e tela corrompidas em aplicações GTK+ (missing glyphs after suspend/resume)](#Fontes_e_tela_corrompidas_em_aplica.C3.A7.C3.B5es_GTK.2B_.28missing_glyphs_after_suspend.2Fresume.29)
    *   [6.4 Tela branca durante o boot, enquanto carrega os módulos](#Tela_branca_durante_o_boot.2C_enquanto_carrega_os_m.C3.B3dulos)
    *   [6.5 X trava com o driver intel](#X_trava_com_o_driver_intel)
    *   [6.6 Adicionando resoluções não detectadas](#Adicionando_resolu.C3.A7.C3.B5es_n.C3.A3o_detectadas)
    *   [6.7 Problema da escala da cor](#Problema_da_escala_da_cor)
    *   [6.8 O Brilho não está ajustando](#O_Brilho_n.C3.A3o_est.C3.A1_ajustando)
    *   [6.9 Desabilitando a compressão do frame buffer](#Desabilitando_a_compress.C3.A3o_do_frame_buffer)
    *   [6.10 Corrupção/Falta de Resposta no Chromium e Firefox](#Corrup.C3.A7.C3.A3o.2FFalta_de_Resposta_no_Chromium_e_Firefox)
    *   [6.11 Kernel crashing com kernels 4.0+ em placas Broadwell/Core-M](#Kernel_crashing_com_kernels_4.0.2B_em_placas_Broadwell.2FCore-M)
*   [7 = Suporte à Skylake](#.3D_Suporte_.C3.A0_Skylake)
    *   [7.1 Lag em convidados do Windows (Máquinas Virtuais)](#Lag_em_convidados_do_Windows_.28M.C3.A1quinas_Virtuais.29)
    *   [7.2 Tela piscando](#Tela_piscando)
*   [8 Veja também](#Veja_tamb.C3.A9m)

## Instalação

Instale o pacote [mesa](https://www.archlinux.org/packages/?name=mesa), que fornece o driver DRI para aceleração 3D.

*   Para o driver DDX (que fornecem a aceleração 2D no [Xorg](/index.php/Xorg "Xorg")), instale o pacote [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). (Alguns não recomendam a instalação do driver Intel, veja a nota abaixo)

*   Para o suporte OpenGL, instale [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl). Se você usa x86_64 e precisa de suporte 32-bits, instale também [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) do repositporio [multilib](/index.php/Multilib "Multilib").

*   Para o suporte ao [Vulkan]] (*Ivy Bridge* em diante), instale [vulkan-intel](https://www.archlinux.org/packages/?name=vulkan-intel).

Não se esqueça de checar [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

**Note:** Existe uma discussão ([Debian & Ubuntu](http://www.phoronix.com/scan.php?page=news_item&px=Ubuntu-Debian-Abandon-Intel-DDX), [Fedora](http://www.phoronix.com/scan.php?page=news_item&px=Fedora-Xorg-Intel-DDX-Switch), [KDE](https://community.kde.org/Plasma/5.9_Errata#Intel_GPUs)) em que alguns recomendam não se instalar o driver [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), deixando apenas o modesetting driver, que é o driver embutido no kernel. Veja [[1]](https://www.reddit.com/r/archlinux/comments/4cojj9/it_is_probably_time_to_ditch_xf86videointel/), [[2]](http://www.phoronix.com/scan.php?page=article&item=intel-modesetting-2017&num=1), [Xorg#Installation](/index.php/Xorg#Installation "Xorg"), and [modesetting(4)](http://linux.die.net/man/4/modesetting). Entretanto, o driver modesetting pode também causar alguns problemas [Chromium Issue 370022](https://bugs.chromium.org/p/chromium/issues/detail?id=370022).

## Carregando

O Intel kernel module carrega automaticamente na inicialização do sistema

Caso isso não aconteça, então:

*   Tenha certeza de que você não tem `nomodeset` ou {ic|1=vga=}} como um [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), visto que as GPU's Intel necessitam do kernel mode-setting.
*   Também, cheque se você não desabilitou o driver, utilizando algum modprobe blacklisting `/etc/modprobe.d/` ou `/usr/lib/modprobe.d/`.

### Habilitando KMS mais cedo no boot

O [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) é utilizado pelas placas Intel que usam o driver i915 DRM, sendo ativado como padrão.

Em [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") encontram-se instruções para se ativar o KMS o mais cedo o possível no processo de inicialização.

## Configuração do Xorg

Não é preciso nenhuma configuração para se rodar o [Xorg](/index.php/Xorg "Xorg").

**Note:** A geração Skylake/HD 530 pode necessitar de configurações adicionais, veja[#Skylake support](#Skylake_support)
!

No entanto, para tirar vantagem de algumas opções do driver, será necessário que se crie um arquivo de configuração do Xorg, similar ao que se encontra abaixo:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
EndSection
```

Opções adicionais devem ser adicionadas pelo usuário nas linhas abaixo de: `Driver`.

**Note:**

*   Talvez seja preciso indicar a `Option "AccelMethod"` ao se criar um arquivo de configuração, mesmo que seja para indicar o método padrão (`"sna"`); senão o X pode vir a travar.
*   Pode-se ser necessário adicionar mais seções de {{|Device}} do que a apresentada acima. Indicaremos quando necessário.

Para conhecer todas as opções que podem ser adicionadas ao driver, veja a [man page](/index.php/Man_page "Man page") para `intel`.

## Opções de economia de energia

O módulo do kernel `i915` permite configurações via [module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). Algumas delas modificam as opções de economia de energia.

Uma lista com todas as opções, suas descrições e valores padrão podem ser geradas com o seguinte comando:

```
$ modinfo -p i915

```

Para checar o que está ativado, digite:

```
# systool -m i915 -av

```

Muitas opções tomam por padrão a íntegra -1, que assume os padrões do hardware. Contudo, é possível configurar opções mais agressivas de economia de energia utilizando [module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). Também é possível desabilitar a economia de energia por completo.

**Warning:** Utilizar outras opções que não sejam as padrões dos chips é considerado experimental: [tainted](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=fc9740cebc3ab7c65f3c5f6ce0caf3e4969013ca).

As opções abaixo são consideradas seguras:

 `/etc/modprobe.d/i915.conf` 
```
options i915 enable_rc6=1 enable_fbc=1 semaphores=1

```

### RC6 sleep modes (enable_rc6)

Pode-se experimentas valores mais altos em `enable_rc6`, mas sua GPU pode não suportá-los: [[3]](https://wiki.archlinux.org/index.php?title=Talk:Intel_Graphics&oldid=327547#Kernel_Module_options).

Para confirmar o valor utilizado, olhe em sysfs:

```
# cat /sys/class/drm/card0/power/rc6_enable

```

... se o valor é mais baixo do que o esperado, o nível RC6 indicado é provavelmente não suportado. `drm.debug=0xe` adiciona informação de depuração DRM para o log do kernel - possivelmente incluirá uma linha como essa:

```
[drm:sanitize_rc6_option] Adjusting RC6 mask to 1 (requested 7, valid 1)

```

### Compressão Framebuffer (enable_fbc)

A compressão Framebuffer pode não estar disponível ou não ser confiável nas GPU's Intel de gerações anteriores à Sandy Bridge (6ª geração). Isso pode resultar em mensagens no log do system journal similares a esta:

```
kernel: drm: not enough stolen space for compressed buffer, disabling.

```

## Dicas e Truques

### Tear-free video (Video sem glitches)

A aceleração SNA causa tearing em alguns computadores. Para concertar isso,ative a opção `"TearFree"` no driver, adicionando a seguinte linha a em sua configuração do Xorg: [configuration file](#Xorg_configuration):

```
Option "TearFree" "true"

```

Veja [original bug report](https://bugs.freedesktop.org/show_bug.cgi?id=37686) para mais informação.

**Note:**

*   Esta opção pode não funcionar quando `SwapbuffersWait` é `false`.
*   Esta opção pode diminuir a performance e aumentar o consumo de memória. [[4]](https://bugs.freedesktop.org/show_bug.cgi?id=37686#c123)
*   Esta opção é problemática para algumas aplicações: [Super Meat Boy](https://en.wikipedia.org/wiki/Super_Meat_Boy "wikipedia:Super Meat Boy").
*   Esta opção não funciona para a aceleração UXA, somente para SNA.

### Disable Vertical Synchronization (VSYNC)

O driver intel [Triple Buffering](http://www.intel.com/support/graphics/sb/CS-004527.htm) para sincronização vertical, isso permite performance total e evita tearing. Para desligar o Vsync, use isso `.drirc` na sua pasta home:

 `~/.drirc` 
```
<device screen="0" driver="dri2">
	<application name="Default">
		<option name="vblank_mode" value="0"/>
	</application>
</device>
```

**Warning:**

*   Não use [driconf](https://www.archlinux.org/packages/?name=driconf) para criar esse arquivo. É bugado e vai selecionar o driver errado.
*   Para melhor performance pode-se também desligar o vsync, principalmente para jogos.

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

### Problemas com o KMS: o console é limitado a uma área pequena

Uma das portas de vídeo de baixa resolução pode ser ativada na inicialização, o que está fazendo com que o terminal utilize uma pequena área da tela. Para corrigir, desative explicitamente a porta com uma configuração de módulo i915 com `video=SVIDEO-1:d` no parâmetro da linha de comando do kernel no carregador de inicialização. Consulte [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") para mais informações.

Se isso não funcionar, tente desabilitar TV1 ou VGA1 ou invés de SVIDEO-1.

### Decodificação H.264 em GMA 4500

O pacote [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) fornece descodificação MPEG-2 somente para GPU's da série GMA 4500\. O suporte de decodificação H.264 é mantido em um ramo separado g45-h264, que pode ser usado ao instalar o pacote [libva-intel-driver-g45-h264](https://aur.archlinux.org/packages/libva-intel-driver-g45-h264/). Note-se, porém, que este suporte é experimental e seu desenvolvimento foi abandonado. Usar a VA-API com este driver em uma GPU GMA 4500 series irá descarregar a CPU, mas pode não resultar em uma reprodução tão suave quanto a reprodução não acelerada. Testes usando mplayer mostraram que usar o vaapi para reproduzir um vídeo 1080p codificado em H.264 reduziu para metade a carga da CPU (em comparação com a sobreposição XV), mas resultou em reprodução muito irregular, enquanto 720p funcionou razoavelmente bem [/viewtopic.php?id=150550](https://bbs.archlinux.org). Há também outras experiências [[5]](http://www.emmolution.org/?p=192&cpage=1#comment-12292). Definir o tamanho do canal de vídeo pré-alocado maior na bios resulta em uma reprodução de decodificada pelo hardware muito melhor. Mesmo 1080p h264 funciona bem se isso for feito.

### Definindo brilho e gama

Veja [Backlight](/index.php/Backlight "Backlight").

## Resolução de Problemas

### Problemas com SNA

*SNA* é o método padrão de aceleração do driver [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). Se você enfrenta problemas com o *SNA* (e.g. pixelated graphics (gráficos pixelados?), texto corrompido, etc.), ente usar *UXA*, o que pode ser feito ao adicionar a seguinte linha ao seu arquivo de configuração Xorg: [configuration file](#Xorg_configuration):

```
Option      "AccelMethod"  "uxa"

```

Veja `man 4 intel` sobre `Option "AccelMethod"`.

### Problemas com DRI3

*DRI3* é padrão em [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). Podem surgir alguns problemas em alguns sistemas, como: [this](https://bugs.chromium.org/p/chromium/issues/detail?id=370022). Para mudar para *DRI2* adicione a seguinte linha ao seu arquivo de configuração do Xorg: [configuration file](#Xorg_configuration):

```
Option "DRI" "2"

```

### Fontes e tela corrompidas em aplicações GTK+ (missing glyphs after suspend/resume)

Se você tiver missing font glyphs (glifos de fontes faltando ?) em aplicações GTK+, este método pode ajudar. Edite `/etc/environment` e a dicione a linha abaixo:

 `/etc/environment`  `COGL_ATLAS_DEFAULT_BLIT_MODE=framebuffer` 

Veja também [FreeDesktop bug 88584](https://bugs.freedesktop.org/show_bug.cgi?id=88584).

### Tela branca durante o boot, enquanto carrega os módulos

Se estiver carregando o KMS mais tarde no boot ("late start") KMS e a tela ficar branca enquanto carregar os módulos, pode ajudar se adicionar `i915` e `intel_agp` para o initramfs. Veja a sessão [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting").

Outra alternativa, seria adicionar o seguinte [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"):

```
video=SVIDEO-1:d

```

Se você precisa de saída para VGA, tente isso:

```
video=VGA-1:1280x800

```

### X trava com o driver intel

Alguns problemas com o X travando, o bloqueio da GPU ou problemas com o congelamento do X podem ser corrigidos desativando o uso da GPU com a opção `NoAccel` - adicione as seguintes linhas ao seu[configuration file](#Xorg_configuration):

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

**Note:** Aguns monitores/TVs suportam as duas escalas de cores. Nesse caso, uma opção frequentemente conhecida como *Black Level* pode precisar ser ajustada para fazê-los lidar com o sinal corretamente. Algumas TVs podem manipular o sinal somente em alcance limitado. Definir RGB de difusão para "Completo" fará um "Collor Clipping". Você pode precisar configurá-lo para "Limited 16: 235" manualmente para evitar o "Clipping".

Pode-se forçar o modo com: `xrandr --output <HDMI> --set "Broadcast RGB" "Full"` (substitua `<HDMI>` pelo dispositivo correto, rodando `xrandr`).

Infelizmente, o driver Intel não suporta a configuração do intervalo de cores através de um arquivo de configuração `xorg.conf.d`.

Um [bug report](https://bugzilla.kernel.org/show_bug.cgi?id=94921) foi postado e um patch pode ser encontrado em anexo.

Também existem outros problemas relacionados que podem ser corrigidos editando registros GPU. Mais informações podem ser encontradas em [[6]](http://lists.freedesktop.org/archives/intel-gfx/2012-April/016217.html) e [[7]](http://github.com/OpenELEC/OpenELEC.tv/commit/09109e9259eb051f34f771929b6a02635806404c).

### O Brilho não está ajustando

Se depois de retomar a suspensão, as teclas de atalho para alterar o brilho da tela não tiverem efeito, verifique sua configuração em relação ao artigo [Backlight](/index.php/Backlight "Backlight").

Se o problema persistir, tente um dos seguintes [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

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

Se você tiver alguma corrupção ou falta de resposta no Chromium e/ou no Firefox [set the AccelMethod to "uxa"](#SNA_issues).

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

Isso pode ser corrigido desabilitando o suporte a execlist que foi alterado para o padrão com o kernel 4.0\. Adicione o seguinte [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"):

```
i915.enable_execlists=0

```

Isso é conhecido por ser quebrado para pelo menos kernel 4.0.5.

## = Suporte à Skylake

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

**Note:** Se o sistema aparecer pendurado após "Loading Initial Ramdisk", certifique-se de que o tamanho de abertura IGD no BIOS seja inferior a 4GB.

### Lag em convidados do Windows (Máquinas Virtuais)

A saída de vídeo de um convidado do Windows (windows guest) no VirtualBox às vezes trava até que o host force uma atualização de tela (por exemplo, movendo o cursor do mouse). A remoção da opção `enable_fbc=1` corrige este problema.

### Tela piscando

Os seguintes recursos de economia de energia usados por intel iGPUs são conhecidos por causar cintilação em alguns casos. Uma solução temporária é desativar um deles usando a opção [kernel boot parameter](/index.php/Kernel_parameters "Kernel parameters") apropriada:

*   Rc6 sleep modes (ver [#RC6 sleep modes (enable_rc6)](#RC6_sleep_modes_.28enable_rc6.29)), pode ser desabilitado com `i915.enable_rc6=0`.

*   *Panel Self Refresh (PSR) [FS#49628](https://bugs.archlinux.org/task/49628) [FS#49371](https://bugs.archlinux.org/task/49371) [FS#50605](https://bugs.archlinux.org/task/50605), ativado por padrão desde o kernel mainline 4.6\. Para desativar esse recurso, use a opção `i915.enable_psr=0`.

## Veja também

*   [https://01.org/linuxgraphics/documentation](https://01.org/linuxgraphics/documentation) (lista dos hardwares suportados)