Artigos relacionados

*   [Módulos de kernel](/index.php/Kernel_modules "Kernel modules")
*   [Compilar módulo de kernel](/index.php/Compile_kernel_module "Compile kernel module")
*   [Kernel Panics](/index.php/Kernel_Panics "Kernel Panics")
*   [sysctl](/index.php/Sysctl "Sysctl")

De acordo com o Wikipédia:

	O [kernel Linux](https://en.wikipedia.org/wiki/pt:Linux_(n%C3%BAcleo) (ou núcleo Linux) é um [kernel para sistemas operacionais](https://en.wikipedia.org/wiki/pt:N%C3%BAcleo_(sistema_operacional) tipo UNIX, monolítico e de código aberto.

[Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)") é baseado no kernel do Linux. Existem vários kernels Linux disponíveis para o Arch Linux, além do kernel estável mais recente. Este artigo lista algumas das opções disponíveis nos repositórios com uma breve descrição de cada uma. Há também uma descrição dos patches que podem ser aplicados ao kernel do sistema. O artigo termina com uma visão geral da compilação personalizada do kernel com links para vários métodos.

Os pacotes de kernel são [instalados](/index.php/Instala "Instala") no sistema de arquivos em `/boot/`. Para poder inicializar no kernels, o [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") deve ser configurado adequadamente.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Kernels com suporte oficial](#Kernels_com_suporte_oficial)
*   [2 Compilação](#Compilação)
*   [3 Kernels do kernel.org](#Kernels_do_kernel.org)
*   [4 Patches e patchsets](#Patches_e_patchsets)
    *   [4.1 Patchsets principais](#Patchsets_principais)
    *   [4.2 Outros patchsets](#Outros_patchsets)
*   [5 Veja também](#Veja_também)

## Kernels com suporte oficial

*   **Stable** — Kernel e módulos Vanilla Linux, com alguns patches aplicados.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux](https://www.archlinux.org/packages/?name=linux)

*   **Hardened** — Um kernel Linux focado na segurança que aplica um conjunto de patches rígidos para mitigar as explorações do kernel e do espaço do usuário. Ele também permite mais recursos de fortalecimento do kernel upstream do que [linux](https://www.archlinux.org/packages/?name=linux).

	[https://github.com/anthraxx/linux-hardened](https://github.com/anthraxx/linux-hardened) || [linux-hardened](https://www.archlinux.org/packages/?name=linux-hardened)

*   **Longterm** — Kernel e módulos Linux de suporte a longo prazo (LTS).

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)

*   **Zen Kernel** — Resultado de um esforço colaborativo de hackers do kernel para fornecer o melhor kernel Linux possível para os sistemas do dia a dia. Mais detalhes podem ser encontrados em [https://liquorix.net](https://liquorix.net) (que fornece binários de kernel baseados no Zen for Debian).

	[https://github.com/zen-kernel/zen-kernel](https://github.com/zen-kernel/zen-kernel) || [linux-zen](https://www.archlinux.org/packages/?name=linux-zen)

## Compilação

O Arch Linux fornece dois métodos para compilar seu próprio kernel.

	[/Arch Build System](/index.php/Kernel/Arch_Build_System "Kernel/Arch Build System")

	Aproveita a alta qualidade do [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") existente do [linux](https://www.archlinux.org/packages/?name=linux) e os benefícios de [gerenciamento de pacote](https://en.wikipedia.org/wiki/pt:Sistema_gestor_de_pacotes "wikipedia:pt:Sistema gestor de pacotes").

	[/Compilação tradicional](/index.php/Kernel/Traditional_compilation "Kernel/Traditional compilation")

	Envolve o download manual de um tarball de origem e a compilação no diretório inicial como um usuário normal.

## Kernels do kernel.org

*   **Git** — Kernel e módulos Linux compilados usando fontes do repositório Git de Linus Torvalds

	[https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git) || [linux-git](https://aur.archlinux.org/packages/linux-git/)

*   **Mainline** — Kernels onde todos os novos recursos são introduzidos, lançados a cada 2-3 meses.

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)

*   **Next** — Kernels mais recentes com recursos pendentes para serem mesclados na próxima versão da linha principal.

	[https://www.kernel.org/doc/man-pages/linux-next.html](https://www.kernel.org/doc/man-pages/linux-next.html) || [linux-next-git](https://aur.archlinux.org/packages/linux-next-git/)

*   **Longterm 3.16** — Kernel e módulos Linux 3.16 de suporte a longo prazo (LTS).

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts316](https://aur.archlinux.org/packages/linux-lts316/)

*   **Longterm 4.4** — Kernel e módulos Linux 4.4 de suporte a longo prazo (LTS).

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts44](https://aur.archlinux.org/packages/linux-lts44/)

*   **Longterm 4.9** — Kernel e módulos Linux 4.9 de suporte a longo prazo (LTS).

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts49](https://aur.archlinux.org/packages/linux-lts49/)

*   **Longterm 4.14** — Kernel e módulos Linux 4.14 de suporte a longo prazo (LTS).

	[https://www.kernel.org/](https://www.kernel.org/) || [linux-lts414](https://aur.archlinux.org/packages/linux-lts414/)

## Patches e patchsets

There are lots of reasons to patch your kernel, the major ones are for performance or support for non-mainline features such as [reiser4](/index.php/Reiser4 "Reiser4") file system support. Other reasons might include fun and to see how it is done and what the improvements are.

However, it is important to note that the best way to increase the speed of your system is to first tailor your kernel to your system, especially the architecture and processor type. For this reason using pre-packaged versions of custom kernels with generic architecture settings is not recommended or really worth it. A further benefit is that you can reduce the size of your kernel (and therefore build time) by not including support for things you do not have or use. For example, you might start with the stock kernel config when a new kernel version is released and remove support for things like bluetooth, video4linux, 1000Mbit ethernet, etc.; functionality you know you will not require for your specific machine. Although this page is not about customizing your kernel config, it is recommended as a first step--before moving on to using a patchset once you have grasped the fundamentals involved.

The config files for the Arch kernel packages can be used as a starting point. They are in the Arch package source files, for example [[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux) linked from [linux](https://www.archlinux.org/packages/?name=linux). The config file of your currently running kernel may also be available in your file system at `/proc/config.gz` if the `CONFIG_IKCONFIG_PROC` kernel option is enabled.

If you have not actually patched or customized a kernel before it is not that hard and there are many PKGBUILDs on the forum for individual patchsets. However, you are advised to start from scratch with a bit of research on the benefits of each patchset, rather than just arbitrarily picking one. This way you will learn much more about what you are doing rather than just choosing a kernel at startup and then be left wondering what it actually does.

**Warning:** Patchsets are developed by a variety of people. Some of these people are actually involved in the production of the linux kernel and others are hobbyists, which may reflect its level of reliability and stability.

### Patchsets principais

*   **[Linux-ck](/index.php/Linux-ck "Linux-ck")** — Contains patches by Con Kolivas designed to improve system responsiveness with specific emphasis on the desktop, but suitable to any workload.

	[http://ck.kolivas.org/](http://ck.kolivas.org/) || [linux-ck](https://aur.archlinux.org/packages/linux-ck/)

*   **pf-kernel** — Provides you with a handful of awesome features not merged into mainline. It is based on neither existing Linux fork nor patchset, although some unofficial ports may be used if required patches have not been released officially. The most prominent patches of linux-pf are PDS CPU scheduler and UKSM.

	[https://gitlab.com/post-factum/pf-kernel/wikis/README](https://gitlab.com/post-factum/pf-kernel/wikis/README) || Packages:

*   [Repository](/index.php/Unofficial_user_repositories#post-factum_kernels "Unofficial user repositories") by pf-kernel developer, [post-factum](https://aur.archlinux.org/account/post-factum)
*   [Repository](/index.php/Unofficial_user_repositories#home-thaodan "Unofficial user repositories"), [linux-pf](https://aur.archlinux.org/packages/linux-pf/), [linux-pf-preset-default](https://aur.archlinux.org/packages/linux-pf-preset-default/), [linux-pf-lts](https://aur.archlinux.org/packages/linux-pf-lts/) by pf-kernel fork developer, [Thaodan](https://aur.archlinux.org/account/Thaodan)

*   **[Realtime kernel](/index.php/Realtime_kernel "Realtime kernel")** — Maintained by a small group of core developers, led by Ingo Molnar. This patch allows nearly all of the kernel to be preempted, with the exception of a few very small regions of code ("raw_spinlock critical regions"). This is done by replacing most kernel spinlocks with mutexes that support priority inheritance, as well as moving all interrupt and software interrupts to kernel threads.

	[https://wiki.linuxfoundation.org/realtime/start](https://wiki.linuxfoundation.org/realtime/start) || [linux-rt](https://aur.archlinux.org/packages/linux-rt/), [linux-rt-lts](https://aur.archlinux.org/packages/linux-rt-lts/)

### Outros patchsets

Some of the listed packages may also be available as binary packages via [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories").

*   **[AppArmor](/index.php/AppArmor "AppArmor")** — The [Mandatory Access Control](https://en.wikipedia.org/wiki/Mandatory_access_control "wikipedia:Mandatory access control") (MAC) system, implemented upon the [Linux Security Modules](https://en.wikipedia.org/wiki/Linux_Security_Modules "wikipedia:Linux Security Modules") (LSM). While [linux](https://www.archlinux.org/packages/?name=linux) supports apparmor this kernel has the required [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") enabled by default.

	[https://gitlab.com/apparmor/apparmor/wikis/About](https://gitlab.com/apparmor/apparmor/wikis/About) || [linux-apparmor](https://aur.archlinux.org/packages/linux-apparmor/)

*   **Aufs** — The aufs-compatible linux kernel and modules, useful when using [docker](/index.php/Docker "Docker").

	[http://aufs.sourceforge.net/](http://aufs.sourceforge.net/) || [linux-aufs](https://aur.archlinux.org/packages/linux-aufs/)

*   **Clear** — Patches from Intel's Clear Linux project. Provides performance and security optimizations; [WireGuard](/index.php/WireGuard "WireGuard") module.

	[https://github.com/clearlinux-pkgs/linux](https://github.com/clearlinux-pkgs/linux) || [linux-clear](https://aur.archlinux.org/packages/linux-clear/)

*   **Libre** — The Linux Kernels without "binary blobs".

	[https://www.fsfla.org/ikiwiki/selibre/linux-libre/](https://www.fsfla.org/ikiwiki/selibre/linux-libre/) || [linux-libre](https://aur.archlinux.org/packages/linux-libre/)

*   **Liquorix** — Kernel replacement built using Debian-targeted configuration and the Zen kernel sources. Designed for desktop, multimedia, and gaming workloads, it is often used as a Debian Linux performance replacement kernel. Damentz, the maintainer of the Liquorix patchset, is a developer for the Zen patchset as well.

	[https://liquorix.net](https://liquorix.net) || [linux-lqx](https://aur.archlinux.org/packages/linux-lqx/)

*   **MultiPath TCP** — The Linux Kernel and modules with Multipath TCP support.

	[https://multipath-tcp.org/](https://multipath-tcp.org/) || [linux-mptcp](https://aur.archlinux.org/packages/linux-mptcp/)

*   **[Reiser4](/index.php/Reiser4 "Reiser4")** — Successor filesystem for ReiserFS, developed from scratch by Namesys and Hans Reiser.

	[https://sourceforge.net/projects/reiser4/files/](https://sourceforge.net/projects/reiser4/files/) || [linux-ck-reiser4](https://aur.archlinux.org/packages/linux-ck-reiser4/)

*   **VFIO** — The Linux kernel and a few patches written by Alex Williamson (acs override and i915) to enable the ability to do PCI Passthrough with KVM on some machines.

	[https://lwn.net/Articles/499240/](https://lwn.net/Articles/499240/) || [linux-vfio](https://aur.archlinux.org/packages/linux-vfio/), [linux-vfio-lts](https://aur.archlinux.org/packages/linux-vfio-lts/)

*   **XanMod** — Aiming to take full advantage in high-performance workstations, gaming desktops, media centers and others and built to provide a more rock-solid, responsive and smooth desktop experience. This kernel uses the BFS scheduler, BFQ I/O scheduler, UKSM realtime memory data deduplication, YeAH TCP congestion control, x86_64 advanced instruction set support, and other default changes.

	[https://xanmod.org/](https://xanmod.org/) || [linux-xanmod](https://aur.archlinux.org/packages/linux-xanmod/)

## Veja também

*   [O'Reilly - Linux Kernel in a Nutshell](http://www.kroah.com/lkn/) (free ebook)
*   [What stable kernel should I use?](http://kroah.com/log/blog/2018/08/24/what-stable-kernel-should-i-use/) by Greg Kroah-Hartman