**Status de tradução:** Esse artigo é uma tradução de [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux"). Data da última tradução: 2019-08-01\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Install_from_existing_Linux&diff=0&oldid=577222) na versão em inglês.

Artigos relacionados

*   [Instalar a partir de SSH](/index.php/Instalar_a_partir_de_SSH "Instalar a partir de SSH")

Este documento descreve o processo de inicialização necessário para instalar o Arch Linux a partir de um sistema host Linux em execução. Após o bootstrapping, a instalação prossegue conforme descrito no [guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação").

Instalar o Arch Linux de um Linux existente é útil para:

*   instalar remotamente o Arch Linux, p.ex. um servidor raiz (virtual)
*   substituir um Linux existente sem um LiveCD (ver [#Substituindo o sistema existente sem um LiveCD](#Substituindo_o_sistema_existente_sem_um_LiveCD))
*   criar uma nova distribuição ou [LiveMedia baseada no Arch Linux](/index.php/Distribui%C3%A7%C3%B5es_baseadas_no_Arch "Distribuições baseadas no Arch")
*   criar um ambiente de chroot do Arch Linux, p.ex.: contêiner base de Docker
*   [rootfs-over-NFS para terminais burros](/index.php/Diskless_network_boot_NFS_root "Diskless network boot NFS root")

O objetivo do procedimento de inicialização é configurar um ambiente a partir do qual os scripts do [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) (como o `pacstrap` e `arch-chroot`) podem ser executados.

Se o sistema hospedeiro funciona no Arch Linux, isso pode ser conseguido simplesmente instalando [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts). Se o sistema hospedeiro executar outra distribuição Linux, primeiro você precisará configurar um chroot baseado no Arch Linux.

**Nota:** Este guia exige que o sistema hospedeiro existente seja capaz de executar os novos programas de arquitetura do Arch Linux alvo. Isso significa que tem que ser uma máquina x86_64.

**Atenção:** Certifique-se de compreender cada passo antes de prosseguir. É fácil destruir seu sistema ou perder dados críticos, e seu provedor de serviços provavelmente cobrará muito para ajudá-lo a recuperar.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Backup e preparação](#Backup_e_preparação)
*   [2 De um host executando o Arch Linux](#De_um_host_executando_o_Arch_Linux)
    *   [2.1 Criar uma nova instalação do Arch](#Criar_uma_nova_instalação_do_Arch)
    *   [2.2 Criar uma cópia exata de uma instalação do Arch existente](#Criar_uma_cópia_exata_de_uma_instalação_do_Arch_existente)
*   [3 De um host executando outra distribuição Linux](#De_um_host_executando_outra_distribuição_Linux)
    *   [3.1 Usando pacman do sistema hospedeiro](#Usando_pacman_do_sistema_hospedeiro)
    *   [3.2 Criando um chroot](#Criando_um_chroot)
        *   [3.2.1 Método A: Usando a imagem do bootstrap (recomendado)](#Método_A:_Usando_a_imagem_do_bootstrap_(recomendado))
        *   [3.2.2 Método B: Usando a imagem LiveCD](#Método_B:_Usando_a_imagem_LiveCD)
    *   [3.3 Usando um ambiente chroot](#Usando_um_ambiente_chroot)
        *   [3.3.1 Inicializando o chaveiro do pacman](#Inicializando_o_chaveiro_do_pacman)
        *   [3.3.2 Selecionando um espelho e baixando ferramentas básicas](#Selecionando_um_espelho_e_baixando_ferramentas_básicas)
    *   [3.4 Dicas de instalação](#Dicas_de_instalação)
        *   [3.4.1 Host baseado no debian](#Host_baseado_no_debian)
            *   [3.4.1.1 /dev/shm](#/dev/shm)
            *   [3.4.1.2 /dev/pts](#/dev/pts)
            *   [3.4.1.3 lvmetad](#lvmetad)
        *   [3.4.2 Host baseado no Fedora](#Host_baseado_no_Fedora)
*   [4 Coisas para verificar antes de reiniciar](#Coisas_para_verificar_antes_de_reiniciar)
*   [5 Substituindo o sistema existente sem um LiveCD](#Substituindo_o_sistema_existente_sem_um_LiveCD)
    *   [5.1 Defina a partição antiga de swap como nova partição raiz](#Defina_a_partição_antiga_de_swap_como_nova_partição_raiz)
    *   [5.2 Instalação](#Instalação)

## Backup e preparação

Faça backup de todos os seus dados, incluindo correios, servidores web, etc. Tenha todas as informações ao seu alcance. Preserve todas as configurações do seu servidor, hsotnames, etc.

Aqui está uma lista de dados que você provavelmente precisará:

*   Endereço IP
*   hostname(s), (nota: servidores raiz são principalmente também parte do domínio dos provedores, verifique ou salve seu `/etc/hosts` antes de excluir)
*   Servidor DNS (verifique `/etc/resolv.conf`)
*   Chaves SSH (se outras pessoas trabalham no seu servidor, elas terão de aceitar novas chaves, caso contrário. Isso inclui chaves do seu Apache, seus servidores de e-mail, seu servidor SSH e outros.)
*   Informações de hardware (placa de rede, etc. Consulte o seu `/etc/modules.conf` pré-instalado)
*   Arquivos de configuração Grub.

Em geral, é uma boa ideia ter uma cópia local do diretório original `/etc` no seu disco rígido local.

## De um host executando o Arch Linux

Instale o pacote [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts).

Siga [Guia de instalação#Montar os sistemas de arquivos](/index.php/Guia_de_instala%C3%A7%C3%A3o#Montar_os_sistemas_de_arquivos "Guia de instalação") para montar o sistema de arquivos e todos os pontos de montagem necessários. Se você já usa o diretório `/mnt` para alguma outra coisa, basta criar outro diretório como `/mnt/install` e usá-lo como a base de pontos de montagem.

### Criar uma nova instalação do Arch

Siga [Guia de instalação#Instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o#Instalação "Guia de instalação").

No procedimento, [Guia de instalação#Selecionar os espelhos](/index.php/Guia_de_instala%C3%A7%C3%A3o#Selecionar_os_espelhos "Guia de instalação") pode ser pulado, já que o host já deve ter a lista de espelhos correta.

**Dica:** Para evitar baixar novamente todos os pacotes, considere seguir [Pacman/Dicas e truques#Cache do pacman compartilhado na rede](/index.php/Pacman/Dicas_e_truques#Cache_do_pacman_compartilhado_na_rede "Pacman/Dicas e truques") ou usara opção `-c` do *pacstrap*.

**Dica:** Quando o gerenciador de boot Grub é usado, o comando `grub-mkconfig` pode detectar dispositivos incorretamente. Isso resultará em `Erro:nenhuma partição` ao tentar inicializar a partir do pendrive. Para resolver este problema, a partir do host executando o Arch Linux, monte as partições recém-instaladas, use `arch-chroot` na nova partição, depois instale e configure o grub. A última etapa pode requerer a desativação de `lvmetad` do `/etc/lvm/lvm.conf` configurando `use_lvmetad=0`.

### Criar uma cópia exata de uma instalação do Arch existente

É possível replicar uma instalação existente do Arch Linux copiando o sistema de arquivos do host para a nova partição e fazer alguns ajustes nela para torná-la inicializável e única.

O primeiro passo é copiar os arquivos do host para a nova partição montada, para isso, considere o uso da abordagem exibida em [rsync#Full system backup](/index.php/Rsync#Full_system_backup "Rsync").

Em seguida, siga o procedimento descrito em [Guia de instalação#Configurar o sistema](/index.php/Guia_de_instala%C3%A7%C3%A3o#Configurar_o_sistema "Guia de instalação") com algumas advertências e etapas adicionais:

*   [Guia de instalação#Fuso horário](/index.php/Guia_de_instala%C3%A7%C3%A3o#Fuso_horário "Guia de instalação"), [Guia de instalação#Localização](/index.php/Guia_de_instala%C3%A7%C3%A3o#Localização "Guia de instalação") e [Guia de instalação#Senha do root](/index.php/Guia_de_instala%C3%A7%C3%A3o#Senha_do_root "Guia de instalação") podem ser ignorados
*   [Guia de instalação#Initramfs](/index.php/Guia_de_instala%C3%A7%C3%A3o#Initramfs "Guia de instalação") pode ser necessário especialmente se estiver alterando o sistema de arquivos, por exemplo, para [ext4](/index.php/Ext4_(Portugu%C3%AAs) "Ext4 (Português)") para [Btrfs](/index.php/Btrfs "Btrfs")
*   Sobre [Guia de instalação#Gerenciador de boot](/index.php/Guia_de_instala%C3%A7%C3%A3o#Gerenciador_de_boot "Guia de instalação"), é necessário reinstalar o gerenciador de boot
*   Exclua `/etc/machine-id` de forma que um novo, único, seja gerado na próxima inicialização

Se a instalação espelhada do Arch puder ser usada em uma configuração diferente ou com outro hardware, considere as seguintes operações adicionais:

*   Use a atualização do [microcódigo](/index.php/Microcode "Microcode") da CPU adaptada para o sistema alvo durante o passo [Guia de instalação#Gerenciador de boot](/index.php/Guia_de_instala%C3%A7%C3%A3o#Gerenciador_de_boot "Guia de instalação")
*   Se algum [Xorg#Configuration](/index.php/Xorg#Configuration "Xorg") específico foi apresentado no host e pode estar incompleto com o sistema alvo, siga [Movendo uma instalação existente para dentro (ou fora) de uma máquina virtual#Desabilitar quaisquer arquivos relacionados a Xorg](/index.php/Movendo_uma_instala%C3%A7%C3%A3o_existente_para_dentro_(ou_fora)_de_uma_m%C3%A1quina_virtual#Desabilitar_quaisquer_arquivos_relacionados_a_Xorg "Movendo uma instalação existente para dentro (ou fora) de uma máquina virtual")
*   Faça qualquer outro ajuste apropriado para o sistema de destino, como reconfigurar a rede ou o áudio.

## De um host executando outra distribuição Linux

Existem várias ferramentas que automatizam uma grande parte das etapas descritas nas subseções a seguir. Consulte as respectivas páginas para obter instruções detalhadas.

*   [arch-bootstrap](https://github.com/tokland/arch-bootstrap) (Bash)
*   [archcx](https://github.com/m4rienf/ArchCX) (Bash, do Hetzner CX Rescue System)
*   [digitalocean-debian-to-arch](https://github.com/gh2o/digitalocean-debian-to-arch) (disco de repartição, específico para DigitalOCean)
*   [image-bootstrap](https://github.com/hartwork/image-bootstrap) (Python)
*   [vps2arch](https://gitlab.com/drizzt/vps2arch) (Bash)

A maneira manual é apresentada nas seguintes subseções. A ideia é fazer o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") funcionar diretamente no sistema hospedeiro ou executar um sistema Arch dentro do sistema host, com a instalação real sendo executada a partir do sistema Arch. O sistema aninhado está contido dentro de um chroot.

### Usando pacman do sistema hospedeiro

O [Pacman](https://git.archlinux.org/pacman.git/) pode ser compilado na maioria das distribuições Linux e usado diretamente no sistema hospedeiro para inicializar o Arch Linux. O [arch-install-scripts](https://git.archlinux.org/arch-install-scripts.git/about/) deve ser executado sem problemas diretamente dos fontes baixados em qualquer distribuição recente.

Algumas distribuições fornecem um pacote para o *pacman* e/ou *arch-install-scripts* em seus repositórios oficiais, que podem ser usados para essa finalidade. Até fevereiro de 2019, o Gentoo é conhecido por fornecer o pacote *pacman*, e o Alpine Linux e o Fedora são conhecidos por fornecer *pacman* e *arch-install-scripts*.

### Criando um chroot

Dois métodos para configurar e entrar no chroot são apresentados abaixo, do mais fácil ao mais complicado. Selecione apenas um dos dois métodos. Então, continue em [#Usando um ambiente chroot](#Usando_um_ambiente_chroot).

#### Método A: Usando a imagem do bootstrap (recomendado)

Baixe a imagem *bootstrap* de um [espelho](https://www.archlinux.org/download) (*mirror*) em `/tmp`.

Você também pode baixar a assinatura (mesma URL com `.sig` adicionado) e [verificá-la com GnuPG](/index.php/GnuPG#Verify_a_signature "GnuPG").

Extraia o tarball:

```
# tar xzf <caminho-para-imagem-bootstrap>/archlinux-bootstrap-*-x86_64.tar.gz

```

Selecione um servidor de repositório editando `/tmp/root.x86_64/etc/pacman.d/mirrorlist`.

Entre no *chroot*

*   Se bash 4 ou posterior estiver instalado, e unshare tiver suporte às opções --fork e --pid:

```
# /tmp/root.x86_64/bin/arch-chroot /tmp/root.x86_64/

```

*   Do contrário, execute os seguintes comandos:

```
# mount --bind /tmp/root.x86_64 /tmp/root.x86_64
# cd /tmp/root.x86_64
# cp /etc/resolv.conf etc
# mount -t proc /proc proc
# mount --make-rslave --rbind /sys sys
# mount --make-rslave --rbind /dev dev
# mount --make-rslave --rbind /run run    # (presumindo que /run existe no sistema)
# chroot /tmp/root.x86_64 /bin/bash

```

#### Método B: Usando a imagem LiveCD

É possível montar a imagem raiz da mídia mais recente de instalação do Arch Linux e, em seguida, fazer *chroot* nela. Este método tem a vantagem de fornecer uma instalação funcional do Arch Linux no direito do sistema host sem a necessidade de prepará-lo instalando pacotes específicos.

**Nota:** Antes de prosseguir, verifique se a versão mais recente de [squashfs](http://squashfs.sourceforge.net/) está instalada no sistema host. Caso contrário, esperam-se erros como os a seguir: `FATAL ERROR aborting: uncompress_inode_table: failed to read block`.

*   A imagem raiz pode ser encontrada em um dos [espelhos](https://www.archlinux.org/download) em `arch/x86_64/`. O formato squashfs não é editável, portanto, desfazemos o "squash" na imagem raiz e a montamos.

*   Para fazer um "unsquash" na imagem raiz, execute

 `# unsquashfs airootfs.sfs` 

*   Antes de fazer [chroot](/index.php/Chroot_(Portugu%C3%AAs) "Chroot (Português)") para ela, precisamos configurar alguns pontos de montagem e copiar o resolv.conf para conectividade.

```
# mount --bind squashfs-root squashfs-root
# mount -t proc none squashfs-root/proc
# mount -t sysfs none squashfs-root/sys
# mount -o bind /dev squashfs-root/dev
# mount -o bind /dev/pts squashfs-root/dev/pts  ## importante para o pacman (para verificação de assinatura)
# cp -L /etc/resolv.conf squashfs-root/etc  ## Isso é necessário para usar conectividade com o chroot

```

*   Agora, tudo está preparado para fazer chroot para dentro do ambiente Arch recém-instalado

 `# chroot squashfs-root bash` 

### Usando um ambiente chroot

O ambiente *bootstrap* é realmente minimalista (sem `nano`, sem `ping`, sem `cryptsetup`, sem `lvm`). Portanto, precisamos configurar o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") para baixar o resto da `base` e, se necessário, `base-devel`.

#### Inicializando o chaveiro do pacman

Antes de iniciar a instalação, as chaves do pacman precisam ser configuradas. Antes de executar os dois comandos a seguir, leia [pacman-key (Português)#Inicializando o chaveiro](/index.php/Pacman-key_(Portugu%C3%AAs)#Inicializando_o_chaveiro "Pacman-key (Português)") para entender os requisitos de entropia:

```
# pacman-key --init
# pacman-key --populate archlinux

```

**Dica:** A instalação e execução [haveged](https://www.archlinux.org/packages/?name=haveged) deve ser feito no sistema hospedeiro, já que não é possível instalar pacotes antes de inicializar o chaveiro do pacman e porque *systemd* vai detectar que está sendo executado em um *chroot* e [vai ignorar requisição de ativação](https://superuser.com/questions/688733/start-a-systemd-service-inside-chroot). Se você for executar `ls -Ra /` em outro console (TTY, terminal, sessão SSH...), não tenha medo de executá-lo em um loop algumas vezes: cinco ou seis execuções do hospedeiro provou ser suficiente para gerar entropia suficiente em um servidor burro remoto.

#### Selecionando um espelho e baixando ferramentas básicas

Após [selecionar um espelho](/index.php/Espelhos#Habilitando_um_espelho_específico "Espelhos"), [renove as listas de pacotes](/index.php/Espelhos#Forçar_o_pacman_a_renovar_as_listas_de_pacotes "Espelhos") e [instale](/index.php/Instale "Instale") o que você precisa: [base](https://www.archlinux.org/groups/x86_64/base/), [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), [parted](https://www.archlinux.org/packages/?name=parted) etc.

**Nota:**

*   Como ainda não há nenhum editor de texto, você precisa sair do arch-chroot e editar a mirrorlist usando o editor de texto do host.
*   Quando você tentar instalar pacotes com o pacman, você pode obter `*erro: não foi possível determinar o ponto de montagem do cachedir: /var/cache/pacman/pkg*`. Para contornar isso, você pode usar `mount --bind <diretório-para-livecd-ou-bootstrap> <diretório-para-livecd-ou-bootstrap>` antes de fazer chroot. Veja [FS#46169](https://bugs.archlinux.org/task/46169).

### Dicas de instalação

Você pode prosseguir agora para [Guia de instalação#Partição dos discos](/index.php/Guia_de_instala%C3%A7%C3%A3o#Partição_dos_discos "Guia de instalação") e seguir o resto do [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação").

Alguns sistemas hospedeiros ou configurações podem exigir determinadas etapas adicionais. Veja as seções abaixo para obter dicas.

##### Host baseado no debian

###### /dev/shm

Em alguns sistemas baseados no Debian, `pacstrap` pode produzir o seguinte erro:

 `# pacstrap /mnt base` 
```
==> Creating install root at /mnt
mount: mount point /mnt/dev/shm is a symbolic link to nowhere
==> ERROR: failed to setup API filesystems in new root

```

Isso porque em algumas versões do Debian, `/dev/shm` aponta para `/run/shm` enquanto no chroot baseado no Arch, `/run/shm` não existe e o link está quebrado. Para corrigir esse erro, cria um diretório `/run/shm`:

```
# mkdir /run/shm

```

###### /dev/pts

Ao instalar `archlinux-2015.07.01-x86_64` a partir de um host Debian 7, o seguinte erro impediu [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) e [arch-chroot](/index.php/Chroot_(Portugu%C3%AAs)#Usando_arch-chroot "Chroot (Português)") de funcionar:

 `# pacstrap -i /mnt` 
```
mount: mount point /mnt/dev/pts does not exist
==> ERROR: failed to setup chroot /mnt

```

Aparentemente, é porque esses dois scripts usam uma função em comum. `chroot_setup()`[[1]](https://projects.archlinux.org/arch-install-scripts.git/tree/common#n76) depende em novos recursos do [util-linux](https://www.archlinux.org/packages/?name=util-linux), que são incompatíveis com Debian 7 *userland* (veja [FS#45737](https://bugs.archlinux.org/task/45737)).

A solução para *pacstrap* é executar manualmente seus [várias tarefas](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in#n77), mas use o [procedimento regular](/index.php/Chroot_(Portugu%C3%AAs)#Usando_chroot "Chroot (Português)") para montaros sistemas de arquivos do kernel no diretório alvo (`"$newroot"`):

```
# newroot=/mnt
# mkdir -m 0755 -p "$newroot"/var/{cache/pacman/pkg,lib/pacman,log} "$newroot"/{dev,run,etc}
# mkdir -m 1777 -p "$newroot"/tmp
# mkdir -m 0555 -p "$newroot"/{sys,proc}
# mount --bind "$newroot" "$newroot"
# mount -t proc /proc "$newroot/proc"
# mount --rbind /sys "$newroot/sys"
# mount --rbind /run "$newroot/run"
# mount --rbind /dev "$newroot/dev"
# pacman -r "$newroot" --cachedir="$newroot/var/cache/pacman/pkg" -Sy base base-devel ... ## adicione os pacotes que quiser
# cp -a /etc/pacman.d/gnupg "$newroot/etc/pacman.d/"       ## copiar chaveiro
# cp -a /etc/pacman.d/mirrorlist "$newroot/etc/pacman.d/"  ## copiar lista de espelhos
```

Em vez de usar `arch-chroot` para [Guia de instalação#Chroot](/index.php/Guia_de_instala%C3%A7%C3%A3o#Chroot "Guia de instalação"), basta usar `chroot "$newroot"`.

###### lvmetad

A tentativa de criar [volumes lógicos](/index.php/LVM#Logical_volumes "LVM") [LVM](/index.php/LVM "LVM") de um ambiente `archlinux-bootstrap-2015.07.01-x86_64` em um host Debian 7 resultaram no seguinte erro:

 `# lvcreate -L 20G lvm -n root` 
```
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /dev/lvm/root: not found: device not cleared
  Aborting. Failed to wipe start of new LV.
```

(A criação de volume físico e grupo de volumes funcionaram apesar de `/run/lvm/lvmetad.socket: connect failed: No such file or directory` estar sendo exibido.)

Isso poderia ser facilmente contornado criando os volumes lógicos fora do chroot (do host Debian). Eles estão disponíveis uma vez que executados chroot novamente.

Também, se o sistema que você está usando tiver lvm, você pode ter a seguinte saída:

 `# grub-install --target=i386-pc --recheck /dev/main/archroot` 
```
Installing for i386-pc platform.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
  /run/lvm/lvmetad.socket: connect failed: No such file or directory
  WARNING: Failed to connect to lvmetad. Falling back to internal scanning.
```

Isso porque o Debian não usa lvmetad por padrão. Você precisa editar `/etc/lvm/lvm.conf` e definir `use_lvmetad` para `0`:

```
use_lvmetad = 0

```

Isto irá desencadear mais tarde um erro na inicialização no estágio initrd. Portanto, você deve alterá-lo depois da geração grub. Em um software RAID + LVM, as etapas seriam as seguintes:

*   Após instalar o sistema, verifique seu [Mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") e as configurações do gerenciador de inicialização *(boot loader)*. Veja [Processo de inicialização do Arch#Gerenciador de boot](/index.php/Processo_de_inicializa%C3%A7%C3%A3o_do_Arch#Gerenciador_de_boot "Processo de inicialização do Arch") para uma lista de gerenciadores de inicialização.
*   Você pode precisar alterar seu `/etc/mdadm.conf` para refletir suas configurações de [RAID](/index.php/RAID "RAID") (se aplicável).
*   Você pode precisar alterar seu`HOOKS` e `MODULES` de acordo com seus requisitos de [LVM](/index.php/LVM "LVM") e [RAID](/index.php/RAID "RAID"): `MODULES="dm_mod" HOOKS="base udev **mdadm_udev** ... block **lvm2** filesystems ..."`
*   Você provavelmente vai precisar gerar novas imagens initrd com mkinitcpio. Veja [Mkinitcpio#Image creation and activation](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio").
*   Defina `use_lvmetad = 0` em `/etc/lvm/lvm.conf`.
*   Atualize as configurações de seu gerenciador de inicialização. Veja a página wiki de seu gerenciador de inicialização para detalhes.
*   Defina `use_lvmetad = 1` em `/etc/lvm/lvm.conf`.

##### Host baseado no Fedora

On Fedora based hosts and live USBs you may encounter problems when using `genfstab` to generate your [fstab](/index.php/Fstab "Fstab"). Remove duplicate entries and the "seclabel" option where it appears, as this is Fedora-specific and will keep your system from booting normally.

## Coisas para verificar antes de reiniciar

Antes de reiniciar, faça um *chroot* no sistema recém-instalado.

Certifique-se de criar um usuário com senha, para que você possa fazer o login via ssh. O login de root está desabilitado por padrão desde o OpenSSH-7.1p2.

Defina uma senha de root para que você possa alternar para root por meio do su mais tarde:

```
# passwd

```

Instale o [ssh](/index.php/Ssh_(Portugu%C3%AAs) "Ssh (Português)") e [habilite](/index.php/Habilite "Habilite")-o para iniciar automaticamente na inicialização.

Configure a conexão de [rede](/index.php/Rede "Rede") para iniciar automaticamente na inicialização.

Configure um [gerenciador de inicialização](/index.php/Gerenciador_de_inicializa%C3%A7%C3%A3o "Gerenciador de inicialização") e configure-o para usar a partição swap que você apropriou anteriormente como a partição raiz. Você pode querer configurar seu gerenciador de inicialização para poder inicializar em seu sistema antigo; é útil reutilizar a partição /boot existente do servidor no novo sistema para este propósito.

## Substituindo o sistema existente sem um LiveCD

Encontre ~700 MB de espaço livre em algum lugar do disco, p.ex. particionando uma partição swap. Você pode desativar a partição swap e configurar o seu sistema lá.

### Defina a partição antiga de swap como nova partição raiz

Verifique `cfdisk`, `/proc/swaps` ou `/etc/fstab` para localizar sua partição swap. Presumindo que seu disco rígido esteja localizado em sdaX (X será um número).

Faça o seguinte:

Desabilite o espaço swap:

```
# swapoff /dev/sdaX

```

Crie um sistema de arquivos nele

```
# fdisk /dev/sda
(defina o campo de ID do /dev/sdaX para "Linux" - Hex 83)
# mke2fs -j /dev/sdaX

```

Crie um diretório para montá-lo nele

```
# mkdir /mnt/novosis

```

Finalmente, monte o novo diretório para instalar um sistema intermediário.

```
# mount -t ext4 /dev/sdaX /mnt/novosis

```

### Instalação

Se estiver disponível menos de 700 MB, examine os pacotes na base do grupo e selecione apenas aqueles necessários para que um sistema com conexão à Internet seja executado e executado na partição temporária. Isso significará especificamente especificar pacotes individuais para pacstrap, bem como passá-lo a opção -c, para obter pacotes baixados para o sistema host para evitar o preenchimento de espaço valioso.

Uma vez que o novo sistema Arch Linux esteja instalado, reinicie no sistema recém-criado e faça um [rsync de todo o sistema](/index.php/Rsync#Full_system_backup "Rsync") para a partição primária. Corrija a configuração do gerenciador de inicialização antes de reiniciar.