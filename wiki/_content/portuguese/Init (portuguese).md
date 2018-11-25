**Status de tradução:** Esse artigo é uma tradução de [Init](/index.php/Init "Init"). Data da última tradução: 2018-10-25\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Init&diff=0&oldid=551065) na versão em inglês.

Artigos relacionados

*   [Processo de inicialização do Arch](/index.php/Processo_de_inicializa%C3%A7%C3%A3o_do_Arch "Processo de inicialização do Arch")
*   [ConsoleKit](/index.php/ConsoleKit "ConsoleKit")

**Atenção:** O Arch Linux só tem suporte oficial para [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"). [[1]](https://lists.archlinux.org/pipermail/arch-general/2015-July/039460.html) Ao usar um sistema init diferente, por favor, mencione isso em solicitações de suporte.

[Init](https://en.wikipedia.org/wiki/pt:Init "wikipedia:pt:Init") é o primeiro processo iniciado durante a inicialização do sistema. É um processo daemon que continua em execução até que o sistema seja encerrado. Init é o ancestral direto ou indireto de todos os outros processos e adota automaticamente todos os processos órfãos. É iniciado pelo kernel usando um nome de arquivo embutido; Se o kernel não puder iniciá-lo, haverá um pânico. Normalmente, a inicialização é atribuída a [identificador de processo](https://en.wikipedia.org/wiki/pt:identificador_de_processo "wikipedia:pt:identificador de processo") 1.

Os *init scripts* (ou *rc*) são iniciados pelo processo init para garantir a funcionalidade básica no início e no encerramento do sistema. Isso inclui (des)montagem de [sistema de arquivos](/index.php/File_system "File system") e inicialização de [daemons](/index.php/Daemons "Daemons"). Um *gerenciador de serviços* dá um passo além, fornecendo controle ativo sobre processos iniciados, ou [supervisão de processos](https://en.wikipedia.org/wiki/Process_Supervision "wikipedia:Process Supervision"). Um exemplo é monitorar falhas e reiniciar processos de acordo.

Esses componentes combinam-se com o *sistema* init. Algumas entradas incluem o gerenciador de serviços no processo de inicialização ou possuem scripts de inicialização em relação próxima. Estes inits são abaixo referidos como *integrados*, embora as entradas em diferentes categorias possam depender explicitamente umas das outras.

## Contents

*   [1 Inits (integrados)](#Inits_(integrados))
*   [2 Inits](#Inits)
*   [3 Init scripts](#Init_scripts)
*   [4 Gerenciadores de serviços](#Gerenciadores_de_serviços)
*   [5 Configuração](#Configuração)
    *   [5.1 Migrar serviços em execução](#Migrar_serviços_em_execução)
    *   [5.2 logind](#logind)
    *   [5.3 Tarefas agendadas](#Tarefas_agendadas)
    *   [5.4 Dbus](#Dbus)
*   [6 Dicas e truques](#Dicas_e_truques)
    *   [6.1 systemd-nspawn](#systemd-nspawn)
    *   [6.2 Substituindo udev](#Substituindo_udev)
*   [7 Veja também](#Veja_também)

## Inits (integrados)

*   **anopa** — Sistema de inicialização construído em torno do conjunto de supervisão s6.

	[https://jjacky.com/anopa/](https://jjacky.com/anopa/) || [anopa](https://aur.archlinux.org/packages/anopa/)

*   **GNU Shepherd** — Sistema de inicialização escrito em [Guile](https://www.gnu.org/software/guile/).

	[https://www.gnu.org/software/shepherd/](https://www.gnu.org/software/shepherd/) || [shepherd](https://aur.archlinux.org/packages/shepherd/)

*   **[OpenRC](/index.php/OpenRC "OpenRC")** — Sistema de inicialização baseado em dependência.

	[http://www.gentoo.org/proj/en/base/openrc/](http://www.gentoo.org/proj/en/base/openrc/) || [openrc](https://aur.archlinux.org/packages/openrc/) [openrc-arch-services-git](https://aur.archlinux.org/packages/openrc-arch-services-git/)

*   **[systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)")** — Sistema de inicialização baseado em dependência com paralelização agressiva, supervisão de processo usando cgroups e a capacidade de depender de um ponto de montagem dado ou um serviço dbus.

	[http://freedesktop.org/wiki/Software/systemd/](http://freedesktop.org/wiki/Software/systemd/) || [systemd](https://www.archlinux.org/packages/?name=systemd)

## Inits

*   **[BusyBox](/index.php/BusyBox "BusyBox")** — Utilitários para sistemas de recuperação e embarcados.

	[http://busybox.net/](http://busybox.net/) || [busybox](https://www.archlinux.org/packages/?name=busybox)

*   **ninit** — Fork do [minit](http://www.fefe.de/minit/)

	[http://riemann.fmi.uni-sofia.bg/ninit/](http://riemann.fmi.uni-sofia.bg/ninit/) || [ninit](https://aur.archlinux.org/packages/ninit/)

*   **sinit** — Inicialização simples inicialmente baseada no init mínimo de Rich Felker.

	[http://core.suckless.org/sinit](http://core.suckless.org/sinit) || [sinit](https://aur.archlinux.org/packages/sinit/)

*   **[SysVinit](/index.php/SysVinit "SysVinit")** — Init tradicional do System V.

	[http://savannah.nongnu.org/projects/sysvinit](http://savannah.nongnu.org/projects/sysvinit) || [sysvinit](https://aur.archlinux.org/packages/sysvinit/)

## Init scripts

*   **initscripts-fork** — Fork mantido dos scripts SysVinit no Arch Linux.

	[https://bitbucket.org/TZ86/initscripts-fork/overview](https://bitbucket.org/TZ86/initscripts-fork/overview) || [initscripts-fork](https://aur.archlinux.org/packages/initscripts-fork/)

*   **minirc** — Script init mínimo projetado para BusyBox.

	[https://github.com/hut/minirc/](https://github.com/hut/minirc/) || [minirc-git](https://aur.archlinux.org/packages/minirc-git/)

*   **spark-rc** — Um script rc simples para iniciar seu sistema.

	[https://gitlab.com/fbt/spark-rc](https://gitlab.com/fbt/spark-rc) || [spark-rc](https://aur.archlinux.org/packages/spark-rc/)

## Gerenciadores de serviços

*   **daemontools** — Coleção de ferramentas para gerenciar serviços UNIX.

	[http://cr.yp.to/daemontools.html](http://cr.yp.to/daemontools.html) || [daemontools](https://aur.archlinux.org/packages/daemontools/)

*   **[Monit](/index.php/Monit "Monit")** — Monit é uma ferramenta de supervisão de processos para Unix e Linux. Com o monit, o status do sistema pode ser visualizado diretamente a partir da linha de comando ou através do servidor da Web HTTP(S) nativo.

	[http://mmonit.com/monit/](http://mmonit.com/monit/) || [monit](https://www.archlinux.org/packages/?name=monit)

*   **perp** — Supervisor de processo persistente (serviço) e estrutura de gerenciamento para UNIX.

	[http://b0llix.net/perp/](http://b0llix.net/perp/) || [perp](https://aur.archlinux.org/packages/perp/)

*   **[runit](/index.php/Runit "Runit")** — Esquema de inicialização do UNIX com supervisão de serviço, uma substituição para o SysVinit e outros esquemas de inicialização.

	[http://smarden.org/runit/](http://smarden.org/runit/) || [runit](https://aur.archlinux.org/packages/runit/)

*   **s6** — Pequeno conjunto de programas para UNIX, projetado para permitir a supervisão de serviço na linha de daemontools e runit.

	[http://skarnet.org/software/s6/](http://skarnet.org/software/s6/) || [s6](https://aur.archlinux.org/packages/s6/)

## Configuração

### Migrar serviços em execução

Para executar daemons sob o novo init, salve uma lista de daemons em execução:

```
$ systemctl list-units --state=running "*.service" > daemons.list

```

e configure os [#Init scripts](#Init_scripts) adequadamente. Veja também [[2]](http://unix.stackexchange.com/questions/175380/how-to-list-all-running-daemons).

**Nota:** [systemd-tmpfiles(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-tmpfiles.8), [módulos de kernel](/index.php/Kernel_modules "Kernel modules") e [sysctl](/index.php/Sysctl "Sysctl") também podem precisar de configuração.

### logind

[logind](http://www.freedesktop.org/wiki/Software/systemd/logind/) exige *systemd* para ser o processo init. [[3]](http://www.freedesktop.org/wiki/Software/systemd/InterfacePortabilityAndStabilityChart/) Portanto, [sessões locais](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") e outras funcionalidades não estão disponíveis.

**Dica:** Uma versão autônoma do *logind* está disponível como [elogind-git](https://aur.archlinux.org/packages/elogind-git/) [[4]](https://lists.gnu.org/archive/html/guix-devel/2015-04/msg00352.html)

	Permissões de dispositivo

Adicione usuários aos respectivos [grupos de usuários](/index.php/Grupos_de_usu%C3%A1rios "Grupos de usuários") para acesso ao dispositivo e reinicialize. A associação atual ao grupo deve primeiro ser verificada com `id *usuário*`.

```
# usermod -a -G video,audio,power,disk,storage,optical,lp,scanner *usuário*

```

Veja também [Usuários e grupos#Grupos pré-systemd](/index.php/Usu%C3%A1rios_e_grupos#Grupos_pré-systemd "Usuários e grupos"). Para criar regras de grupo para usar com [Polkit](/index.php/Polkit "Polkit"), veja [Polkit#Bypass password prompt](/index.php/Polkit#Bypass_password_prompt "Polkit").

	X sem root (1.16)

Como `Xorg.wrap` não verifica se logind está ativo [[5]](https://bugs.freedesktop.org/show_bug.cgi?id=86975#c5), [permissões de root para Xorg](/index.php/Xorg#Rootless_Xorg "Xorg") precisam se habilitadas manualmente:

 `/etc/X11/Xwrapper.config`  `needs_root_rights = yes` 

	Gerenciamento de energia

Veja [pm-utils](https://aur.archlinux.org/packages/pm-utils/) e [acpid](/index.php/Acpid "Acpid") para substituir [gerenciamento de energia por systemd](/index.php/Power_management#Power_management_with_systemd "Power management").

### Tarefas agendadas

Arch usa arquivos [timer](/index.php/Systemd_(Portugu%C3%AAs)#Timers "Systemd (Português)") em vez do [cron](/index.php/Cron "Cron"), por padrão. Veja [archlinux-cronjobs](https://github.com/notfoss/archlinux-cronjobs) para trabalhos de cron básicos.

### Dbus

As instâncias de usuário do *dbus-daemon* são iniciadas pelo [systemd/User](/index.php/Systemd/User "Systemd/User") [[6]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/). Ao solicitar IPC entre aplicativos de desktop, restaure `30-dbus.sh`:

 `/etc/X11/xinit/xinitrc.d/30-dbus.sh` 
```
#!/bin/bash

# inicia uma instância de sessão dbus
if [ -z "${DBUS_SESSION_BUS_ADDRESS-}" ] && type dbus-launch >/dev/null; then
  eval $(dbus-launch --sh-syntax --exit-with-session)
fi
```

## Dicas e truques

### systemd-nspawn

[systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") é uma ferramenta para sistemas systemd. Desde o Linux 2.6.19, no entanto, é possível executar o systemd em um sistema não-systemd usando o espaço de nome de PID. Para isso, o kernel precisa ser configurado com `CONFIG_PID_NS` e `CONFIG_NAMESPACES`).

O espaço de nome de PID cria uma nova hierarquia de processos que começam com o PID 1\. Além disso, o systemd exige que um sistema de arquivos raiz "chrootado" seja montado. Portanto, você precisa pelo menos fazer uma montagem de ligação, porque senão alguns serviços falharão com

```
"Failed at step NAMESPACE spawning" due to "Invalid operation" 

```

pois o systemd tenta remontar a raiz com a opção `private`.

Para configurar um chroot com um novo namespace PID, você pode usar o jchroot [[7]](http://vincent.bernat.im/en/blog/2011-jchroot-isolation.html) [[8]](https://github.com/vincentbernat/jchroot). Certifique-se de não montar `/proc` dentro da nova raiz antes de fazer o chroot, caso contrário, o systemd detectará o ambiente chroot. Você pode montá-lo depois que o systemd estiver em execução.

### Substituindo udev

**Atenção:** Substituir o udev não é necessário, já que *systemd-udev* é funcional sem *systemd* como PID 1\. Algumas substituições como *eudev* também não podem coexistir com [systemd](https://www.archlinux.org/packages/?name=systemd) – garanta um init alternativo está inicializado **antes** em sua instalação.

*   **eudev** — O eudev é um fork do udev iniciado pelo projeto Gentoo. É principalmente projetado e testado com OpenRC.

	[https://wiki.gentoo.org/wiki/Eudev](https://wiki.gentoo.org/wiki/Eudev) || [eudev](https://aur.archlinux.org/packages/eudev/) [eudev-git](https://aur.archlinux.org/packages/eudev-git/)

*   **mdev** — Gerenciador de dispositivos para uso em sistemas embarcados.

	[https://git.busybox.net/busybox/plain/docs/mdev.txt](https://git.busybox.net/busybox/plain/docs/mdev.txt) || [busybox](https://www.archlinux.org/packages/?name=busybox)

*   **vdev** — Um gerenciador de dispositivos virtuais para unix.

	[https://github.com/jcnelson/vdev.git](https://github.com/jcnelson/vdev.git) || [vdev-git](https://aur.archlinux.org/packages/vdev-git/)

*   **smdev** — O smdev é um programa simples para gerenciar nós de dispositivos. É principalmente compatível com o mdev, mas não possui todos os seus recursos.

	[http://git.suckless.org/smdev/](http://git.suckless.org/smdev/) || [smdev-git](https://aur.archlinux.org/packages/smdev-git/)

## Veja também

*   [Debate sobre o sistema de inicialização do Debian](https://wiki.debian.org/Debate/initsystem)
*   [Como executar o s6-svscan como processo 1](http://skarnet.org/software/s6/s6-svscan-1.html)
*   [Substitua o systemd com busybox + minirc](https://bbs.archlinux.org/viewtopic.php?id=162606&p=1)
*   [Experimentos do Manjaro](http://www.troubleshooters.com/linux/init/manjaro_experiments.htm)
*   [Init vs. runsv](https://busybox.net/~vda/init_vs_runsv.html)
*   [Desmistificando o sistema init](https://felipec.wordpress.com/2013/11/04/init/)
*   [Uma história de sistemas init modernos (1992-2015)](http://blog.darknedgy.net/technology/2015/09/05/0/)
*   [Comparação de sistemas init (gentoo wiki)](https://wiki.gentoo.org/wiki/Comparison_of_init_systems)