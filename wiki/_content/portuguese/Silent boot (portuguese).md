Esta página é para aqueles que preferem limitar a verbosidade de seu sistema a um mínimo estrito, seja por estética ou por outros motivos. Seguir este guia removerá todo o texto do processo de inicialização. [Demonstração de vídeo](http://www.youtube.com/watch?v=tuqhsqrhXk0)

## Contents

*   [1 Parâmetros do kernel](#Par.C3.A2metros_do_kernel)
*   [2 sysctl](#sysctl)
*   [3 startx](#startx)
*   [4 fsck](#fsck)
*   [5 Remover o cursor piscando do console](#Remover_o_cursor_piscando_do_console)
*   [6 Silenciar o GRUB](#Silenciar_o_GRUB)

## Parâmetros do kernel

Altere os [parâmetros do kernel](/index.php/Kernel_parameters "Kernel parameters") usando as opções de configuração do seu gerenciador de inicialização, para incluir os seguintes parâmetros:

```
quiet vga=current

```

`vga=current` é o argumento do kernel para evitar comportamentos estranhos, como [FS#32309](https://bugs.archlinux.org/task/32309).

Se você ainda estiver recebendo mensagens impressas para o console, pode ser que o dmesg envie a você o que acha que são mensagens importantes. Você pode alterar o nível em que essas mensagens serão impressas usando `quiet loglevel=<nível>`, sendo `<nível>` qualquer número entre 0 e 7, em que 0 é o mais crítico e 7 é o nível de depuração da impressão.

```
quiet loglevel=3 vga=current

```

Note que isto parece funcionar apenas se `quiet` e `loglevel=<nível>` forem usados, e eles devem estar nessa ordem (quiet primeiro). O parâmetro de loglevel só alterará o que é impresso no console, os níveis do próprio dmesg não serão afetados e ainda estarão disponíveis através do diário, bem como do comando `dmesg`. Para obter mais informações, consulte o arquivo `Documentation/kernel-parameters.txt` do pacote [linux-docs](https://www.archlinux.org/packages/?name=linux-docs).

Se você também quiser impedir o systemd de imprimir seu número de versão ao inicializar, você também deve anexar `udev.log_priority=3` à sua linha de comando do kernel ([fonte](http://www.freedesktop.org/software/systemd/man/systemd-udevd.service.html#Kernel%20command%20line)). Se systemd for usado em um [initramfs](/index.php/Initramfs "Initramfs"), anexe `rd.udev.log_priority=3`.

Se você estiver usando o hook `systemd` no [initramfs](/index.php/Initramfs "Initramfs"), você poderá receber mensagens systemd durante a inicialização do initramfs. Você pode passar `rd.systemd.show_status=false` para desativá-los, ou `rd.systemd.show_status=auto` para suprimir somente mensagens bem-sucedidas (portanto, em caso de erros você ainda pode vê-los). Na verdade, `auto` já foi passado para `systemd.show_status=auto` quando `quiet` é usado, no entanto por algum motivo algumas vezes systemd dentro do initramfs não entende isso. Abaixo estão os parâmetros que você precisa passar para o seu kernel para obter uma inicialização completamente limpa com o systemd em seu [initramfs](/index.php/Initramfs "Initramfs"):

```
 quiet loglevel=3 rd.systemd.show_status=auto rd.udev.log_priority=3

```

Também `touch ~/.hushlogin` para remover a última mensagem de login.

## sysctl

Para ocultar quaisquer mensagens do kernel do console, adicione ou modifique a linha `kernel.printk` de acordo com [[1]](http://unix.stackexchange.com/a/45525/27433):

 `/etc/sysctl.d/20-quiet-printk.conf`  `kernel.printk = 3 3 3 3` 

## startx

Para ocultar mensagens do `startx`, você pode redirecionar sua saída para `/dev/null`, em seu [.bash_profile](https://github.com/kaihendry/Kai-s--HOME/blob/master/.bash_profile), como:

**Nota:** Redirecionamento está quebrado com login sem root. Veja [Xorg#Broken redirection](/index.php/Xorg#Broken_redirection "Xorg").

```
$ [[ $(fgconsole 2>/dev/null) == 1 ]] && exec startx -- vt1 &> /dev/null

```

## fsck

Para ocultar as mensagens do fsck durante a inicialização, deixe o systemd verificar o sistema de arquivos raiz. Para isso, remova *fsck* de:

```
HOOKS=(...) 

```

em `/etc/mkinitcpio.conf` e, então, execute:

```
mkinitcpio -p linux

```

Agora, copie os arquivos `systemd-fsck-root.service` e `systemd-fsck@.service` localizados em `/usr/lib/systemd/system/` para `/etc/systemd/system/` e edite-os, configurando *StandardOutput* e *StandardError* assim:

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

## Remover o cursor piscando do console

O cursor do console na inicialização continua piscando se você seguir estas instruções. Isto pode ser resolvido passando `vt.global_cursor_default=0` ao kernel [[2]](http://www.friendlyarm.net/forum/topic/2998).

Para recuperar o cursor no TTY, execute:

```
# setterm -cursor on >> /etc/issue

```

## Silenciar o GRUB

Para ocultar as mensagens de boas-vindas e de inicialização do GRUB, você pode instalar o pacote não oficial [grub-silent](https://aur.archlinux.org/packages/grub-silent/).

Após a instalação, é necessário reinstalar o [GRUB](/index.php/GRUB "GRUB") na partição necessária primeiro.

Então, pegue um exemplo, como `/etc/default/grub.silent`, e faça as alterações necessárias para `/etc/default/grub`.

As três linhas abaixo são necessárias:

```
GRUB_DEFAULT=0
GRUB_TIMEOUT=0
GRUB_RECORDFAIL_TIMEOUT=$GRUB_TIMEOUT

```

**Nota:** Se você definir `GRUB_TIMEOUT=0` e `GRUB_HIDDEN_TIMEOUT=1` (ou qualquer valor positivo), defina `GRUB_RECORDFAIL_TIMEOUT=$GRUB_HIDDEN_TIMEOUT` em vez de `GRUB_RECORDFAIL_TIMEOUT=$GRUB_TIMEOUT`. Do contrário, pressionar `Esc` na inicialização para mostrar o menu do GRUB não vai funcionar.

Finalmente, gere novamente o arquivo `grub.cfg`.