**Status de tradução:** Esse artigo é uma tradução de [Silent boot](/index.php/Silent_boot "Silent boot"). Data da última tradução: 2019-11-06\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Silent_boot&diff=0&oldid=585788) na versão em inglês.

Artigos relacionados

*   [Plymouth](/index.php/Plymouth_(Portugu%C3%AAs) "Plymouth (Português)")

Esta página é para aqueles que preferem limitar a verbosidade de seu sistema a um mínimo estrito, seja por estética ou por outros motivos. Seguir este guia removerá todo o texto do processo de inicialização. [Demonstração em vídeo](http://www.youtube.com/watch?v=tuqhsqrhXk0)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Parâmetros do kernel](#Parâmetros_do_kernel)
*   [2 Remover o cursor piscando do console](#Remover_o_cursor_piscando_do_console)
*   [3 sysctl](#sysctl)
*   [4 agetty](#agetty)
*   [5 startx](#startx)
*   [6 fsck](#fsck)
*   [7 Silenciar o GRUB](#Silenciar_o_GRUB)
*   [8 Retendo ou desabilitando o logotipo do fornecedor do BIOS](#Retendo_ou_desabilitando_o_logotipo_do_fornecedor_do_BIOS)
    *   [8.1 Desabilitando o controle obtido](#Desabilitando_o_controle_obtido)

## Parâmetros do kernel

Altere os [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") usando as opções de configuração do seu gerenciador de inicialização, para incluir os seguintes parâmetros:

```
quiet vga=current

```

`vga=current` é o argumento do kernel para evitar comportamentos estranhos, como [FS#32309](https://bugs.archlinux.org/task/32309).

Se você ainda estiver recebendo mensagens impressas para o console, pode ser que o dmesg envie a você o que acha que são mensagens importantes. Você pode alterar o nível em que essas mensagens serão impressas usando `quiet loglevel=<nível>`, sendo `<nível>` qualquer número entre 0 e 7, em que 0 é o mais crítico e 7 é o nível de depuração da impressão.

```
quiet loglevel=3 vga=current

```

Note que isto parece funcionar apenas se `quiet` e `loglevel=<nível>` forem usados, e eles devem estar nessa ordem (quiet primeiro). O parâmetro de loglevel só alterará o que é impresso no console, os níveis do próprio dmesg não serão afetados e ainda estarão disponíveis através do diário, bem como do comando `dmesg`. Para obter mais informações, consulte o arquivo `Documentation/kernel-parameters.txt` do pacote [linux-docs](https://www.archlinux.org/packages/?name=linux-docs).

Se você também quiser impedir o systemd de imprimir seu número de versão ao inicializar, você também deve anexar `udev.log_priority=3` à sua linha de comando do kernel ([fonte](http://www.freedesktop.org/software/systemd/man/systemd-udevd.service.html#Kernel%20command%20line)). Se systemd for usado em um [initramfs](/index.php/Initramfs_(Portugu%C3%AAs) "Initramfs (Português)"), anexe `rd.udev.log_priority=3`.

Se você estiver usando o hook `systemd` no [initramfs](/index.php/Initramfs_(Portugu%C3%AAs) "Initramfs (Português)"), você poderá receber mensagens systemd durante a inicialização do initramfs. Você pode passar `rd.systemd.show_status=false` para desativá-los, ou `rd.systemd.show_status=auto` para suprimir somente mensagens bem-sucedidas (portanto, em caso de erros você ainda pode vê-los). Na verdade, `auto` já foi passado para `systemd.show_status=auto` quando `quiet` é usado, no entanto por algum motivo algumas vezes systemd dentro do initramfs não entende isso. Abaixo estão os parâmetros que você precisa passar para o seu kernel para obter uma inicialização completamente limpa com o systemd em seu [initramfs](/index.php/Initramfs_(Portugu%C3%AAs) "Initramfs (Português)"):

```
 quiet loglevel=3 rd.systemd.show_status=auto rd.udev.log_priority=3

```

Também `touch ~/.hushlogin` para remover a última mensagem de login.

## Remover o cursor piscando do console

O cursor do console na inicialização continua piscando se você seguir estas instruções. Isto pode ser resolvido passando `vt.global_cursor_default=0` ao kernel [[1]](http://www.friendlyarm.net/forum/topic/2998).

Para recuperar o cursor no TTY, execute:

```
# setterm -cursor on >> /etc/issue

```

## sysctl

Para ocultar quaisquer mensagens do kernel do console, adicione ou modifique a linha `kernel.printk` de acordo com [[2]](http://unix.stackexchange.com/a/45525/27433):

 `/etc/sysctl.d/20-quiet-printk.conf`  `kernel.printk = 3 3 3 3` 

## agetty

Para ocultar o problema de agetty exibido e a linha de prompt "login:" do console[[3]](https://github.com/karelzak/util-linux/commit/933956cb499e12d0d0e5228b6de34ffa5c9a9e08), crie um [trecho drop-in](/index.php/Trecho_drop-in "Trecho drop-in") para `getty@tty1.service`.

 `/etc/systemd/system/getty@tty1.service.d/skip-prompt.conf` 
```
[Service]
ExecStart=
ExecStart=-/usr/bin/agetty **--skip-login** --nonewline --noissue --autologin *nome_de_usuário* --noclear %I  $TERM
```

## startx

Para ocultar mensagens do `startx`, você pode redirecionar sua saída para `/dev/null`, em seu [.bash_profile](https://github.com/kaihendry/Kai-s--HOME/blob/master/.bash_profile), como:

**Nota:** Redirecionamento está quebrado com login sem root. Veja [Xorg#Redirecionamento quebrado](/index.php/Xorg_(Portugu%C3%AAs)#Redirecionamento_quebrado "Xorg (Português)").

```
$ [[ $(fgconsole 2>/dev/null) == 1 ]] && exec startx -- vt1 &> /dev/null

```

## fsck

Para ocultar as mensagens do fsck durante a inicialização, deixe o systemd verificar o sistema de arquivos raiz. Para isso, substitua o hook *udev* com *systemd*:

```
HOOKS=( base systemd fsck ...) 

```

em `/etc/mkinitcpio.conf` e, então, execute:

```
mkinitcpio -p linux

```

Agora, edite `systemd-fsck-root.service` e `systemd-fsck@.service`:

```
# systemctl edit --full systemd-fsck-root.service
# systemctl edit --full systemd-fsck@.service

```

Configurando *StandardOutput* e *StandardError* assim:

```
(...)

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/lib/systemd/systemd-fsck
StandardOutput=null
StandardError=journal+console
TimeoutSec=0

```

Veja [isso](http://www.freedesktop.org/software/systemd/man/systemd-fsck@.service.html) para mais informações sobre as opções que você pode passar para `systemd-fsck` - você pode alterar com qual frequência o serviço vai verificar (ou não) seus sistemas de arquivos.

## Silenciar o GRUB

Para ocultar as mensagens de boas-vindas e de inicialização do GRUB, você pode instalar o pacote não oficial [grub-silent](https://aur.archlinux.org/packages/grub-silent/).

Após a instalação, é necessário reinstalar o [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") na partição necessária primeiro.

Então, pegue um exemplo, como `/etc/default/grub.silent`, e faça as alterações necessárias para `/etc/default/grub`.

As três linhas abaixo são necessárias:

```
GRUB_DEFAULT=0
GRUB_TIMEOUT=0
GRUB_RECORDFAIL_TIMEOUT=$GRUB_TIMEOUT

```

**Nota:** Se você definir `GRUB_TIMEOUT=0` e `GRUB_HIDDEN_TIMEOUT=1` (ou qualquer valor positivo), defina `GRUB_RECORDFAIL_TIMEOUT=$GRUB_HIDDEN_TIMEOUT` em vez de `GRUB_RECORDFAIL_TIMEOUT=$GRUB_TIMEOUT`. Do contrário, pressionar `Esc` na inicialização para mostrar o menu do GRUB não vai funcionar.

Finalmente, gere novamente o arquivo `grub.cfg`.

## Retendo ou desabilitando o logotipo do fornecedor do BIOS

Os modernos sistemas UEFI exibem um logotipo de fornecedor na inicialização até entregar o controle ao gerenciador de boot; por exemplo, Os laptops da Lenovo exibem um logotipo vermelho brilhante da Lenovo. Esse logotipo de fornecedor é normalmente apagado pelo gerenciador de boot (se o GRUB padrão for usado) ou pelo kernel.

Para evitar que o kernel apague o logotipo de fornecedor, o Linux 4.19 introduziu uma nova opção de configuração `FRAMEBUFFER_CONSOLE_DEFERRED_TAKEOVER` que retém o conteúdo do framebuffer até que o texto precise ser impresso no console framebuffer. A partir de novembro de 2018 (Linux 4.19.1), os kernels oficiais do Arch Linux são compilados com `CONFIG_FRAMEBUFFER_CONSOLE_DEFERRED_TAKEOVER = y`.

Quando combinado com um nível de log baixo (para impedir que o texto seja impresso), o logotipo do fornecedor pode ser mantido enquanto o sistema é inicializado. Observe que o GRUB na configuração padrão substitui a tela; considere usar a inicialização [EFISTUB](/index.php/EFISTUB_(Portugu%C3%AAs) "EFISTUB (Português)") para inicializar diretamente no kernel e, assim, alavancar o controle diferido.

[Demonstração em vídeo](https://www.youtube.com/watch?v=5DW2JgJmsuY)

A linha de comando do kernel deve usar `loglevel=3` ou `rd.udev.log_priority=3` como mencionado acima. Observe que, se você costuma receber mensagens de `Core temperature above threshold, cpu clock throttled` no log do kernel, você precisa usar o nível de log 2 para silenciá-las no momento da inicialização. Alternativamente, se você compilar seu próprio kernel, ajuste o nível de log da mensagem em `arch/x86/kernel/cpu/mcheck/therm_throt.c`.

Se você usar [Intel graphics](/index.php/Intel_graphics "Intel graphics"), defina `i915.fastboot=1` na linha de comando do kernel para evitar configurações desnecessárias de modos (e de supressão de tela) na inicialização.

Leia mais sobre isso em:

*   [Phoronix: Linux 4.19 Adds Deferred Console Takeover Support For FBDEV - Cleaner Boot Process](https://www.phoronix.com/scan.php?page=news_item&px=Linux-4.19-FBDEV-Defer-Console)
*   [Hans de Goede: Adding deferred fbcon console takeover to the Fedora kernels](https://lists.fedoraproject.org/archives/list/kernel@lists.fedoraproject.org/thread/3MWCKJ2DVJPC4INXPKB4ECFZLA7X5RTI/)

### Desabilitando o controle obtido

Se o novo comportamento causar problema, você pode desabilitar o controle obtido por meio do [parâmetro do kernel](/index.php/Par%C3%A2metro_do_kernel "Parâmetro do kernel") `fbcon=nodefer`.