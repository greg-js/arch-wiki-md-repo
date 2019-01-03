Related articles

*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Docker](/index.php/Docker "Docker")
*   [Lxc-systemd](/index.php/Lxc-systemd "Lxc-systemd")

**LinuX Containers** (**LXC**) é um método de virtualização em nível de sistema operacional para executar vários sistemas Linux isolados (contêineres) em um único host de controle (LXC host).

LXC não fornecer uma máquina virtual, mas fornece um ambiente virtual que tem sua própria CPU, memória, bloco I/O, rede, etc espaço. Este é fornecido por [cgroups](/index.php/Cgroups "Cgroups") recursos no kernel do Linux no host LXC. É semelhante a um chroot, mas oferece muito mais isolamento.

Este documento destina-se como uma visão geral sobre a configuração e implantação de contêineres. Uma certa quantidade de conhecimentos e habilidades pré-requisito é exigido (rede de instalação, executar comandos como root, instalar pacotes do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), configuração do kernel, sistema de arquivos de montagem, etc.)