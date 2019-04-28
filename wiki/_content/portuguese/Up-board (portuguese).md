**Status de tradução:** Esse artigo é uma tradução de [Up-board](/index.php/Up-board "Up-board"). Data da última tradução: 2019-04-27\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Up-board&diff=0&oldid=572029) na versão em inglês.

A [UP Board](http://up-board.org) é um dispositivo SOC baseado em Intel da Aaeon. Existe um dispositivo complementar, o UP Core, que usa o mesmo chipset e dispositivos. A instalação do Arch não é diferente, exceto se você não tem o barramento GPIO para ativar.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 GPIO](#GPIO)
*   [3 Reiniciando](#Reiniciando)
*   [4 Som](#Som)
    *   [4.1 Compilação](#Compilação)
        *   [4.1.1 Manual](#Manual)
        *   [4.1.2 Arch Build System](#Arch_Build_System)
*   [5 Veja Também](#Veja_Também)

## Instalação

A UP Board apresenta uma configuração somente [UEFI](/index.php/UEFI "UEFI") (sem emulação de BIOS). O processo de instalação padrão do UEFI pode ser seguido. [systemd-boot](/index.php/Systemd-boot "Systemd-boot") funciona bem como um simples gerenciador de inicialização.

**Nota:** O disco de instalação para a UP Board é `/dev/mmcblk0`. O tipo de partição recomendado é [GPT](/index.php/GPT "GPT").

## GPIO

Os pinos GPIO na UP Board são roteados por meio de um CPLD que requer um driver personalizado. Este driver ainda não foi adicionado ao kernel principal, mas há patches disponíveis que adicionam a funcionalidade. O pacote [linux-up](https://aur.archlinux.org/packages/linux-up/) do AUR fornece o kernel principal com o driver corrigido e ativado.

## Reiniciando

Devido a um possível erro, discutido [aqui](https://forum.up-community.org/discussion/comment/8980#Comment_8980) e relatado [aqui](https://bugs.freedesktop.org/show_bug.cgi?id=106721)

Reiniciando a placa várias vezes sem desconectar a energia, já que o que poderia acontecer se fosse usado como um servidor, poderia falhar com o kernel panic.

Para tornar a reinicialização da placa mais confiável, tente adicionar o seguinte à sua configuração em `/etc/default/grub`.

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX_DEFAULT="reboot=efi,cold fsck.mode=force fsck.repair=yes"` 

## Som

A partir de agosto de 2016, o kernel da linha principal não suporta som através de HDMI para dispositivos baseados em trilhas como o UP Board. Existem planos para adicionar suporte ao kernel da linha principal, conforme observado [aqui](https://bugzilla.kernel.org/show_bug.cgi?id=113971#c6), mas nesse meio tempo, se você deseja ter som, precisará patchear manualmente seu kernel. Atualmente, não há pacote AUR incluindo esses patches.

### Compilação

Sem quaisquer otimizações, a compilação na UP Board leva de 5 a 6 horas. Configurar o seu `MAKEFLAGS` de antemão irá melhorar drasticamente o tempo de compilação. Se você estiver usando o ABS, a página [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") contém informações sobre como definir a variável lá.

#### Manual

*   Faça o download de uma cópia do kernel corrigido de [aqui](https://github.com/plbossart/sound/archive/byt-cht-hdmi-v4.7.tar.gz) e as fontes de kernel mais recentes em [http://www.kernel.org](http://www.kernel.org).

*   Depois de extrair o arquivo, você precisará remover a referência em linha em um dos arquivos de cabeçalho. Você pode fazer isso com `sed` assim:

```
$ sed -i 's/inline//g' sound-byt-cht-hdmi-v4.7/sound/hdmi_audio/intel_mid_hdmi_audio.h

```

*   Em seguida, você precisará criar um patch para as duas pastas que foram alteradas, `sound/` e `drivers/gpu/drm/i915`:

```
$ diff -ENwbur {linux-4.7.2,sound-byt-cht-hdmi-v4.7}/drivers/gpu/drm/i915 >> cherry.patch
$ diff -ENwbur {linux-4.7.2,sound-byt-cht-hdmi-v4.7}/sound >> cherry.patch

```

*   Uma vez que o patch foi criado, você pode movê-lo para o diretório de fontes do kernel e executar:

```
$ patch -p1 < cherry.patch

```

*   Por fim, você precisará garantir que a opção `CONFIG_SUPPORT_HDMI=y` esteja na `.config`.

#### Arch Build System

Se você deseja construir o kernel usando o ABS, siga os passos fornecidos em [Kernels/Arch Build System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System"). Lembre-se de adicionar o patch à função prepare e executar *updpkgsums* para atualizar a soma de verificação do arquivo de configuração alterado.

## Veja Também

*   [Up-squared (Português)](/index.php/Up-squared_(Portugu%C3%AAs) "Up-squared (Português)")
*   [Página Inicial](https://www.up-board.org)