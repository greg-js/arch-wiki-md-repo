Este guia é direcionado a qualquer um que deseja instalar o Arch Linux em outro Linux já existente - - seja através de um LiveCD ou de uma distribuição Linux diferente já existente.

É util para quem deseja:

*   Instalar o Arch Linux de forma remota
*   Criar uma nova distribuição ou LiveCD baseado no Arch Linux
*   Criar um ambiente de chroot
*   [rootfs-over-NFS para terminais burros](/index.php/Diskless_network_boot_NFS_root "Diskless network boot NFS root")

Este guia tem como pré-requisito a existência de um ambiente capaz de executar os programas compilados para a arquitetura escolhida no Arch Linux. Neste caso, um host x86_64 é capaz de utilizar o i686-pacman para construir um ambiente de chroot de 32-bits. Veja [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system"). Contudo, não é algo trivial criar um ambiente 64-bit quando o host em execução está utilizando programas 32-bit.

**Nota:** Se você já está utilizando o Arch, ao invés de seguir este guia apenas instale o pacote [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) dos repositórios oficiais e siga o [Guia de Instalação](/index.php/Installation_Guide_(Portugu%C3%AAs) "Installation Guide (Português)")

**Este guia adiciona passos ao [Guia de Instalação](/index.php/Installation_Guide_(Portugu%C3%AAs) "Installation Guide (Português)"). Os passos já descridos no guia de instalação devem ser seguidos sempre que necessários.**

## Contents

*   [1 Preparar o sistema](#Preparar_o_sistema)
*   [2 Configurar o ambiente do Pacman](#Configurar_o_ambiente_do_Pacman)
    *   [2.1 Método 1: Chroot em uma imagem LiveCD](#M.C3.A9todo_1:_Chroot_em_uma_imagem_LiveCD)
    *   [2.2 Método 2: Bootstrapping dos scripts de instalação(arch install scripts)](#M.C3.A9todo_2:_Bootstrapping_dos_scripts_de_instala.C3.A7.C3.A3o.28arch_install_scripts.29)
    *   [2.3 Método 3: Instalando o pacman nativamente em uma distribuição não-arch(avançado)](#M.C3.A9todo_3:_Instalando_o_pacman_nativamente_em_uma_distribui.C3.A7.C3.A3o_n.C3.A3o-arch.28avan.C3.A7ado.29)
        *   [2.3.1 Download dos fontes e pacotes do pacman](#Download_dos_fontes_e_pacotes_do_pacman)
    *   [2.4 Dependências de instalação](#Depend.C3.AAncias_de_instala.C3.A7.C3.A3o)
        *   [2.4.1 Compilação do pacman](#Compila.C3.A7.C3.A3o_do_pacman)
        *   [2.4.2 Preparação dos arquivos de configuração](#Prepara.C3.A7.C3.A3o_dos_arquivos_de_configura.C3.A7.C3.A3o)
*   [3 Corrigindo problemas de chaves de assinatura](#Corrigindo_problemas_de_chaves_de_assinatura)
*   [4 Configure o sistema alvo](#Configure_o_sistema_alvo)
    *   [4.1 Edite o arquivo FSTAB](#Edite_o_arquivo_FSTAB)
    *   [4.2 Finalizando a instalação](#Finalizando_a_instala.C3.A7.C3.A3o)
*   [5 Dicas](#Dicas)

## Preparar o sistema

Siga as instruções no [Guia de Instalação](/index.php/Installation_Guide_(Portugu%C3%AAs) "Installation Guide (Português)") até que você tenha ajustado partições, teclado e conexão com a internet.

## Configurar o ambiente do Pacman

Você precisa criar um ambiente onde o _pacman_ e os _arch istall scripts_ possam rodar em sua distribuição.(Se você escolher o método 1, apenas o pacman será necessário)

A princípio, existem dois métodos diferentes de preparar o ambiente: **instalando o pacman nativamente (método 4 abaixo)** em sua distribuição ou criando um **ambiente de chroot**. A segunda opção tende a ser a mais fácil, e será discutida em seguida:

Duas são as formas possíveis de se utilizar o método do _chroot_:

*   **Utilizando o chroot como um ambiente de instalação**: O ambiente de chroot Archlinux preparado será utilizado temporariamente para criar a instalação do Archlinux através do _arch-install-scripts_. O trabalho inicial pode ser mais demorado, porém, quando o ambiente estiver pronto, vários sistemas Archlinux podem ser criados com uma facilidade e rapidez imensa. Se você deseja fazer uma instalação única, este método pode parecer desperdício. Você configurará duas vezes o mesmo sistema, terá um grande tráfego de rede e utilizara muito mais RAM, por conta deste processo.

*   **Instalar o Archlinux diretamente/Bootstrapping direto**: Graças ao script _arch-bootstrap_ criado por tokland, este método é eficiente e muito rápido. Após uma simples linha de código, o sistema base inteiro do Archlinux estará instalado no disco. **Contudo**, se você deseja instalar o Archlinux em diversas máquinas este método será mais demorado, pois requer o re-download de todos os pacotes a cada nova instalação.

A melhor aplicação do **Bootstrapping direto** é em uma rede com um número reduzido de sistemas. Se você pretende instalar o Archlinux em muitos sistemas, a instalação via **ambiente chroot** ou mesmo o **pacman nativo** pode ser muito mais vantajoso.

### Método 1: Chroot em uma imagem LiveCD

Este é o método recomendado.

É possível montar a imagem da ultima mídia de instalação do Archlinux e então, entrar nela através de chroot. Este método possui a vantagem de dar a você um sistema com todos os requisitos necessários, sem que pacotes adicionais precisem ser instalados.

**Nota:** Antes de iniciar este procedimento, certifique de possuir a última versão do pacote [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools) no sistema em execução. Caso contrário, você poderá receber erros como: `FATAL ERROR aborting: uncompress_inode_table: failed to read block`.

*   Baixe a última imagem de instalação de [https://www.archlinux.org/download/](https://www.archlinux.org/download/)

*   Monte a imagem LiveCD

 `# mount -o loop archlinux-{date}-dual.iso /mnt` 

*   A raiz da imagem possui o [formato squashfs](https://en.wikipedia.org/wiki/Squashfs "wikipedia:Squashfs") dentro do CD. O squashfs não é editável então, você precisa utilizar o unsquash para ter acesso a imagem raiz para aí então, montá-la.

Para executar um unsquash da imagem de arquitetura x86_64 (ou i686 respectivamente) rode

 `# unsquashfs -d /squashfs-root /mnt/arch/x86_64/root-image.fs.sfs` 

*   Agora, você pode desmontar e remover a imagem iso

```
# umount /mnt
# rm archlinux-{date}-dual.iso

```

*   Monte a imagem raiz através da opção loop

 `# mount -o loop /squashfs-root/root-image.fs /arch` 

*   Antes de executar o [chrooting](/index.php/Change_root "Change root") para o interior da imagem, precisaremos configurar alguns pontos de montagem adicionais,

```
# mount -t proc none /arch/proc
# mount -t sysfs none /arch/sys
# mount -o bind /dev /arch/dev
# mount -o bind /dev/pts /arch/dev/pts # important for pacman (for signature check)

```

*   Agora tudo está preparado para que você dê um chroot no seu ambiente de instalação do Arch.

 `# chroot /arch bash` 

Este chroot está apto a executar os arch install scripts. As partições de destino do chroot deverão sempre ser montadas abaixo da estrutura de diretórios `/mnt`.

### Método 2: Bootstrapping dos scripts de instalação(arch install scripts)

Ao contrário dos outros métodos, **este é um método de um passo apenas**; você só precisará executar o script abaixo e pronto.

Este método pode ser considerado um híbrido entre os métodos 1 e 2\. Provê um ambiente de chroot onde os scripts de instalação serão executados(similar ao método 2), utilizando o script de bootstrapping(similar ao método 1).

O script abaixo criará um diretório chamado `archinstall-pkg` e efetuará o download dos pacotes necessários lá. Então os extrairá para dentro do diretório `archinstall-chroot`. Finalmente, irá preparar os pontos de montagem, configrará o pacman e entrará no chroot

**Nota:** Este é **apenas** um ambiente para executar os arch install scripts: **esta não é sua instalação final**.

Este chroot é capaz de executar os arch install scripts. **As partições destino deve estar montadas abaixo do diretório `/mnt` para este chroot**. Após esta configuração, vá para o próximo passo que é [#Corrigindo problemas de chaves de assinatura](#Corrigindo_problemas_de_chaves_de_assinatura).

 `archinstall-bootstrap.sh` 

```
#!/bin/bash
# This script is inspired on the archbootstrap script.

PACKAGES=(acl attr bzip2 curl expat glibc gpgme libarchive libassuan libgpg-error libssh2 openssl pacman xz zlib pacman-mirrorlist coreutils bash grep gawk file tar ncurses readline libcap util-linux pcre arch-install-scripts)
# Change the mirror as necessary
MIRROR='http://mirrors.kernel.org/archlinux' 
# You can set the ARCH variable to i686 or x86_64
ARCH=`uname -m`
LIST=`mktemp`
CHROOT_DIR=archinstall-chroot
DIR=archinstall-pkg
mkdir -p "$DIR"
mkdir -p "$CHROOT_DIR"
# Create a list with urls for the arch packages
for REPO in core community extra; do  
        wget -q -O- "$MIRROR/$REPO/os/$ARCH/" |sed  -n "s|.*href=\"\\([^\"]*\\).*|$MIRROR\\/$REPO\\/os\\/$ARCH\\/\\1|p"|grep -v 'sig$'|uniq >> $LIST  
done
# Download and extract each package.
for PACKAGE in ${PACKAGES[*]}; do
        URL=`grep "$PACKAGE-[0-9]" $LIST|head -n1`
        FILE=`echo $URL|sed 's/.*\/\([^\/][^\/]*\)$/\1/'`
        wget "$URL" -c -O "$DIR/$FILE" 
        xz -dc "$DIR/$FILE" | tar x -k -C "$CHROOT_DIR"
done
# Create mount points
mkdir -p "$CHROOT_DIR/dev" "$CHROOT_DIR/proc" "$CHROOT_DIR/sys" "$CHROOT_DIR/mnt"
mount -t proc proc "$CHROOT_DIR/proc/"
mount -t sysfs sys "$CHROOT_DIR/sys/"
mount -o bind /dev "$CHROOT_DIR/dev/"
mkdir -p "$CHROOT_DIR/dev/pts"
mount -t devpts pts "$CHROOT_DIR/dev/pts/"

# Hash for empty password  Created by doing: openssl passwd -1 -salt ihlrowCo and entering an empty password (just press enter)
echo 'root:$1$ihlrowCo$sF0HjA9E8up9DYs258uDQ0:10063:0:99999:7:::' > "$CHROOT_DIR/etc/shadow"
echo "root:x:0:0:root:/root:/bin/bash" > "$CHROOT_DIR/etc/passwd" 
touch "$CHROOT_DIR/etc/group"
echo "myhost" > "$CHROOT_DIR/etc/hostname"
test -e "$CHROOT_DIR/etc/mtab" || echo "rootfs / rootfs rw 0 0" > "$CHROOT_DIR/etc/mtab"
[ -f "/etc/resolv.conf" ] && cp "/etc/resolv.conf" "$CHROOT_DIR/etc/"
sed -ni '/^[ \t]*CheckSpace/ !p' "$CHROOT_DIR/etc/pacman.conf"
sed -i "s/^[ \t]*SigLevel[ \t].*/SigLevel = Never/" "$CHROOT_DIR/etc/pacman.conf"
echo "Server = $MIRROR/\$repo/os/$ARCH" >> "$CHROOT_DIR/etc/pacman.d/mirrorlist"

chroot $CHROOT_DIR /usr/bin/pacman -Sy 
chroot $CHROOT_DIR /bin/bash

```

### Método 3: Instalando o pacman nativamente em uma distribuição não-arch(avançado)

**Warning:** Este método é potencialmente difícil, e pode ter variações de distribuição para distribuição. Se você deseja apenas efetuar uma instalação do arch utilizando outra distro e não está interessado em ter o pacman como um programa dentro de tal distro, é melhor utilizar outro método de instalação

Este método abrange a instalação do pacman e os scripts de instalação do arch diretamente em outra distribuição, para que se tornem programas comuns na mesma.

Este método é bastante útil se você planeja utilizar outra distro regularmente para instalar o arch, ou fazer coisas mirabolantes como atualizar os pacotes do arch enquanto utiliza outra distribuição. Este é o único método que não requer a criação de um ambiente chroot para executar o pacman e scripts de instalação. (porém, como parte do processo de instalação inclui entrar em chroot, não existe escapatória)

#### Download dos fontes e pacotes do pacman

Visite a página inicial do pacman: [https://www.archlinux.org/pacman/#_releases](https://www.archlinux.org/pacman/#_releases) e baixe a última versão.

Agora, baixe os seguintes pacotes:

*   pacman-mirrorlist: [https://www.archlinux.org/packages/core/any/pacman-mirrorlist/download/](https://www.archlinux.org/packages/core/any/pacman-mirrorlist/download/)
*   arch-install-scripts: [https://www.archlinux.org/packages/extra/any/arch-install-scripts/download/](https://www.archlinux.org/packages/extra/any/arch-install-scripts/download/)
*   pacman (necessário para arquivos de configuração): [https://www.archlinux.org/packages/core/x86_64/pacman/download/](https://www.archlinux.org/packages/core/x86_64/pacman/download/) (altere para x86_64 se necessário)

### Dependências de instalação

Utilizando os mecanismos da sua distribuição, instale os seguintes pacotes que são necessários para o pacman e arch install scripts: libcurl, libarchive, fakeroot, xz, asciidoc, wget, e sed. Obviamente, gcc, make e as variantes "devel" de tais pacotes também são necessários.

#### Compilação do pacman

*   Extraia os fontes do pacman e entre no diretório.
*   Execute o configure, e adapte os caminhos se necessário: ` ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var --enable-doc` 

Caso ocorram erros, são grandes as changes de dependências em falta ou bibliotecas como libcurl, libarchive ou outras são muito antigas. Instale as dependências utilizando suas opções na distribuição em uso, e se estas forem muito antigas, compile-as.

*   Compile `make` 
*   Se não houver erros, instale com `make install` 
*   Chame manualmente `ldconfig` para garantir a detecção da libalpm.

#### Preparação dos arquivos de configuração

Agora é a hora de extrair os arquivos de configuração. Altere para x86_64 se necessário

*   Extraia os arquivos pacman.conf e makepkg.conf do pacote do pacman, e desabilite a verificação de assinaturas: `tar xJvf pacman-*-x86_64.pkg.tar.xz etc -C / ; sed -i 's/SigLevel.*/SigLevel = Never/g' /etc/pacman.conf` 
*   Extraia a lista de arquivos: `tar xJvf pacman-mirrorlist-*-any.pkg.tar.xz -C /` 
*   Habilite alguns espelhos no arquivo `/etc/pacman.d/mirrorlist`
*   Extraia o arch-install-scripts `tar xJvf arch-install-scripts-*-any.pkg.tar.xz -C /` 

Outra opção é utilizar a ferramenta `alien` para converter os pacotes `pacman-mirrorlist` e `arch-install-scripts` para o formato utilizado pela sua distribuição. Não converta o `pacman` em si.

## Corrigindo problemas de chaves de assinatura

É necessário inicializar o chaveiro do _pacman_ para a verificação das assinaturas.

Execute

```
# pacman-key --init # leia nota abaixo!
# pacman-key --populate archlinux

```

**Contudo**, quando conectado através de SSH você pode sofrer de falta de [entropia](http://pt.wikipedia.org/wiki/Entropia). Neste caso, tente algo similar a:

```
# cat /usr/bin/* > /dev/null &
# find / > /dev/null &

```

antes de executar `pacman-key --init`.

Pode levar um tempo. Caso estas opções acima não funcionem, instale o pacote [haveged](https://www.archlinux.org/packages/?name=haveged) e antes de efetuar a inicialização das chaves com `pacman-key --init`, execute:

```
# /usr/sbin/haveged -w 1024 -v 1

```

## Configure o sistema alvo

Neste ponto, apenas siga os passos do [Guia de Instalação](/index.php/Installation_Guide_(Portugu%C3%AAs) "Installation Guide (Português)"). Lembre de montar o sistema destino do chroot em `/mnt`.

```
# pacstrap /mnt base base-devel
# # ...

```

### Edite o arquivo FSTAB

Provavelmente o script `genfstab` não funcionará. Neste caso, você terá de editar o `/mnt/etc/fstab` na mão. Utilize o conteúdo do arquivo `/etc/mtab` como referência.

### Finalizando a instalação

Execute os outros passos normalmente.

## Dicas

*   Caso você queira substituir o sistema existente, mas por alguma razão não consegue utilizar um LiveCD devido a limitações físicas(acesso ao computador, ausência de driver de CD, etc) a seguinte dica pode ajudar: Libere ~500MB no seu disco e instale o archlinux lá. Reinicie nesta nova partição criada e execute um [rsync completo](/index.php/Full_system_backup_with_rsync#With_a_single_command "Full system backup with rsync") para a partição primária. Altere as configurações do bootloader e reinicie.