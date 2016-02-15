[VirtualBox](http://www.virtualbox.org) é um poderoso emulador de PC virtual x86 e AMD64/Intel64 assim como [VMware](/index.php/VMware "VMware"). É ativamente desenvolvido com lançamentos frequentes e tem uma lista sempre crescente de funcionalidades, sistemas operacionais convidados e plataformas onde pode ser executado.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
    *   [1.1 Extension Pack](#Extension_Pack)
*   [2 Configuração](#Configura.C3.A7.C3.A3o)
    *   [2.1 Adicionar usuário ao grupo vboxusers](#Adicionar_usu.C3.A1rio_ao_grupo_vboxusers)
    *   [2.2 Habilitando a interface de rede _Host-Only_](#Habilitando_a_interface_de_rede_Host-Only)
    *   [2.3 Adicionais para convidado](#Adicionais_para_convidado)
    *   [2.4 Iniciando máquinas virtuais como serviço](#Iniciando_m.C3.A1quinas_virtuais_como_servi.C3.A7o)
*   [3 Máquinas Virtuais](#M.C3.A1quinas_Virtuais)
    *   [3.1 Instalando o Arch Linux em uma máquina virtual](#Instalando_o_Arch_Linux_em_uma_m.C3.A1quina_virtual)
        *   [3.1.1 Adicionais para Convidado](#Adicionais_para_Convidado_2)
        *   [3.1.2 Iniciando serviços compartilhados](#Iniciando_servi.C3.A7os_compartilhados)
        *   [3.1.3 Usando Microfone/WebCam USB](#Usando_Microfone.2FWebCam_USB)
        *   [3.1.4 Sincronizando a data da máquina virtual com a máquina real](#Sincronizando_a_data_da_m.C3.A1quina_virtual_com_a_m.C3.A1quina_real)
        *   [3.1.5 Habilitando pastas compartilhadas](#Habilitando_pastas_compartilhadas)
*   [4 Iniciar o VirtualBox](#Iniciar_o_VirtualBox)
*   [5 Solução de Problemas](#Solu.C3.A7.C3.A3o_de_Problemas)
    *   [5.1 modprobe Exec format error](#modprobe_Exec_format_error)
    *   [5.2 VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)](#VBOX_E_INVALID_OBJECT_STATE_.280x80BB0007.29)
    *   [5.3 Could not load the Host USB Proxy service: VERR_NOT_FOUND](#Could_not_load_the_Host_USB_Proxy_service:_VERR_NOT_FOUND)
    *   [5.4 Failed to create the host-only network interface](#Failed_to_create_the_host-only_network_interface)
    *   [5.5 WinXP: Bit-depth cannot be greater than 16](#WinXP:_Bit-depth_cannot_be_greater_than_16)
    *   [5.6 Montando imagens .VDI](#Montando_imagens_.VDI)

## Instalação

O VirtualBox, lincenciado sob GPL, pode ser [instalado](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") com o pacote [virtualbox](https://www.archlinux.org/packages/?name=virtualbox), encontrado nos [repositórios oficiais](/index.php/Official_Repositories_(Portugu%C3%AAs) "Official Repositories (Português)"). O pacote [virtualbox-host-modules](https://www.archlinux.org/packages/?name=virtualbox-host-modules), que contém os módulos pré-compilados para o kernel Arch Linux estoque, deve ser instalado com ele. Se você estiver usando kernel [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) deve também instalar [virtualbox-host-modules-lts](https://www.archlinux.org/packages/?name=virtualbox-host-modules-lts). Para utilizar a interface gráfica, baseada em [Qt](/index.php/Qt "Qt"), você também precisará instalar o pacote [qt4](https://www.archlinux.org/packages/?name=qt4).

```
# pacman -S virtualbox

```

### Extension Pack

Para fornecer suporte a RDP, USB e PXE para boot em placas de rede Intel, além de outras funcionalidades, o VirtualBox precisa do _Extension Pack_, que pode ser baixado neste link: [VirtualBox Downloads](https://www.virtualbox.org/wiki/Downloads). Este pacote de expansão, com licença PUEL, é livre para uso pessoal.

Para instalar o Extension Pack, baixe e salve-o em seu disco rígido e, em seguida, abra o VirtualBox. Vá em **Arquivo → Preferências → Extensões** e clique no ícone "Acrescentar extensões", em seguida abra a pasta que contém a extensão e selecione-a para instalar.

**Dica:** Caso você receba algum erro ao tentar instalar o Extension Pack no VirtualBox, tente iniciá-lo como superusuário e refaça os passos.

Além disso você pode instalar o pacote de extensão através do terminal usando o VBoxManage:

```
VBoxManage extpack install <tarball> |
                   uninstall [--force] <name> |
                   cleanup

```

Como alternativa você pode utilizar o pacote [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/) do [AUR](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)").

## Configuração

### Adicionar usuário ao grupo vboxusers

Adicione os usuários desejados ao grupo **vboxusers**. O novo grupo não se aplica automaticamente as sessões existentes, o usuário tem que logar novamente ou iniciar um novo ambiente.

```
# gpasswd -a $USER vboxusers

```

**Nota:** Terá que reiniciar a sua sessão (Log-Out/Log-In) para que as alterações tenham efeito

_=== Carregando os módulos ===_

Após a instalação você poderá gerenciar suas máquinas virtuais, porém não poderá iniciá-las até carregar o módulo **vboxdrv**. Para carregar o módulo manualmente (como root):

```
# modprobe vboxdrv

```

Para carregar os módulos do VirtualBox automaticamente na inicialização do Arch Linux, crie um arquivo `*.conf` (e.g. `virtualbox.conf`) em `/etc/[modules-load.d](/index.php/Kernel_modules#Loading "Kernel modules")`, que conterá todos os módulos que deverão ser carregados.

 `/etc/modules-load.d/virtualbox.conf`  `vboxdrv` 
**Nota:** Se ao rodar o comando `modprobe -a vboxdrv` (ou qualquer outro módulo do virtualbox) você se deparar com a mensagem "_modprobe: WARNING: Module vboxdrv not found._" ou "_no such file or directory_" será preciso atualizar a base de dados dos módulos rodando o comando `depmod -a`.

**Nota:** Este módulo costumava ser adicionado à matriz `MODULES` em `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`, que agora está obsoleto.

### Habilitando a interface de rede _Host-Only_

Pra que seja possível utilizar a opção Host-Only na interface de rede do VirtualBox, é preciso carregar os módulos **vboxnetadp** e **vboxnetflt** ou acrescentá-los ao arquivo `virtualbox.conf` em `/etc/[modules-load.d](/index.php/Kernel_modules#Loading "Kernel modules")` para que sejam carregados automaticamente na inicialização do Arch Linux:

 `/etc/modules-load.d/virtualbox.conf` 

```
vboxdrv
**vboxnetadp**
**vboxnetflt**
```

Para carregar os módulos manualmente, utilize o seguinte comando como root:

```
# modprobe -a vboxnetadp vboxnetflt

```

Feito isso, abra a interface gráfica do VirtualBox e vá até **Arquivo → Preferências → Rede** e acrescente uma nova interface de rede _host-only_ antes de poder habilitá-la em sua máquina virtual.

**Nota:** Estes módulos costumavam ser adicionados à matriz `MODULES` em `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`, que agora está obsoleto.

### Adicionais para convidado

O VirtualBox sugere a instalação do [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) no host Arch Linux rodando VirtualBox. É uma imagem de disco utilizada para instalação dos adicionais para convidado nas máquinas virtuais, tornando disponível clicando em **Dispositivos → Instalar adicionais para convidado**.

```
# pacman -S virtualbox-guest-iso

```

### Iniciando máquinas virtuais como serviço

Para iniciar máquinas virtuais como serviço no Arch Linux você deve criar o arquivo `vboxvmservice@.service` em `/etc/[systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)")/system` da seguinte forma:

 `/etc/systemd/system/vboxvmservice@.service` 

```
[Unit]
Description=VBox Virtual Machine %i Service
Requires=systemd-modules-load.service
After=systemd-modules-load.service

[Service]
User=USUARIO
Group=vboxusers
ExecStart=/usr/bin/VBoxHeadless -s %i
ExecStop=/usr/bin/VBoxManage controlvm %i savestate

[Install]
WantedBy=multi-user.target

```

**Nota:**

*   Cada máquina virtual tem seu próprio serviço. Substitua USUARIO com um usuário que seja membro do grupo **vboxusers**:

```
# systemctl enable vboxvmservice@_nome_da_maquina_virtual_
# systemctl start vboxvmservice@_nome_da_maquina_virtual_

```

*   Certifique-se de que o campo **USUARIO** é preenchido com o mesmo usuário que está criando/importando as máquinas virtuais, se não o usuário não irá vê-las.

## Máquinas Virtuais

### Instalando o Arch Linux em uma máquina virtual

A instalação do Arch Linux em uma máquina virtual é tão simples quanto instalar qualquer outro sistema convidado no VirtualBox, mas as adições devem ser instaladas através do [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") (Seguindo as instruções abaixo), e não através do item "Instalar Adicionais para Convidado" no menu do VirtualBox nem de uma ISO montada.

*   Clique no botão "**Novo**" para criar uma nova máquina virtual.
*   Nomeie a máquina como desejar
*   Selecione a distribuição e a arquitetura (Se você nomeá-la como Arch Linux o VirtualBox automaticamente irá selecionar a distribuição do Arch, mas você deverá escolher a arquitetura)
*   Selecione a quantidade de memória a ser utilizada pela máquina virtual (Lembre-se que a máquina virtual irá utilizar a memória do seu sistema real e que você deve colocar, no mínimo, 512 MB para que a maioria dos sistemas funcione de forma satisfatória)
*   Após criar a sua máquina virtual, selecione-a e clique em **Configurações → Armazenamento → Controladora IDE → Vazio** e, em **Drive de CD/DVD**, selecione a imagem ISO do seu Arch Linux.
*   Inicie a máquina virtual e siga as instruções de instalação do [Guia do Iniciante](/index.php/Guia_do_Iniciante(Portugu%C3%AAs_do_Brasil) "Guia do Iniciante(Português do Brasil)")

#### Adicionais para Convidado

Instale o pacote [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) em sua máquina virtual Arch Linux e carregue os módulos manualmente com:

```
# modprobe -a vboxguest vboxsf vboxvideo

```

Ou crie um arquivo `*.conf` em (e.g. `virtualbox.conf`) em `/etc/modules-load.d/` para que o Arch carregue os módulos automaticamente na inicialização do sistema com as seguintes linhas:

 `/etc/modules-load.d/virtualbox.conf` 

```
vboxguest
vboxsf
vboxvideo
```

adicione a seguinte linha para o topo de `~/.xinitrc` acima de quaisquer opções `exec`. (crie um novo arquivo se este não existir):

 `~/.xinitrc`  `/usr/bin/VBoxClient-all` 
**Nota:** Se você está criando um novo arquivo `~/.xinitrc` você _deve_ também incluir um [Gerenciador de Janelas (Documentação em Inglês)](/index.php/Window_manager "Window manager") ou [Ambiente de Trabalho (Documentação em Inglês)](/index.php/Desktop_environment "Desktop environment").

#### Iniciando serviços compartilhados

Após instalar o [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) acima, você deve iniciar o `VBoxClient-all` para iniciar os serviços de compartilhamento da área de transferência, redimensionamento da tela, etc.

*   Se você estiver executando algo que inicia `/etc/xdg/autostart/vboxclient.desktop`, como GNOME ou KDE, então nada precisa ser feito.
*   Se você utiliza `.xinitrc` para lançar coisas em vez disso, você deve adicionar o seguinte em seu `.xinitrc` antes de iniciar sua máquina virtual:

```
# VBoxClient-all &

```

#### Usando Microfone/WebCam USB

**Nota:** Você deve ter instalado o [VirtualBox Extension Pack](#Extension_Pack) antes de seguir os passos abaixo.

*   Certifique-se de que a máquina virtual não está sendo executada e seu microfone/webcam não está sendo utilizado;
*   Abra a janela do VirtualBox, selecione a máquina virtual do Arch Linux e clique em _Configurações_, em seguida selecione a seção _USB_;
*   Marque a caixa _Habilitar controladora USB_ e também _Habilitar controladora USB 2.0 (EHCI)_;
*   Clique no botão _Adicionar filtro do dispositivo_ (O cabo com sinal de +);
*   Selecione o seu dispositivo de webcam/microfone na lista;
*   Inicie sua máquina virtual Arch.

#### Sincronizando a data da máquina virtual com a máquina real

Para sincronizar hora e data, tenha certeza de ter instalado o pacote [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) em sua máquina real. Então execute o comando:

```
# systemctl start vboxservice.service 

```

Para habilitar o serviço na inicialização do sistema execute:

```
# systemctl enable vboxservice.service

```

Você também deve utilizar este daemon afim de usar o recurso de pastas compartilhadas descrito abaixo.

#### Habilitando pastas compartilhadas

Pastas compartilhadas são gerenciadas através do programa VirtualBox na máquina real. Elas podem ser adicionadas, automontadas e feita somente leitura.

Se a _automontagem_ está habilitada e o _vboxservice_ está habilitado, criando uma pasta compartilhada do programa VirtualBox com a máquina real, irá montar esta pasta em `/media/sf_NOMEDAPASTACOMPARTILHADA` na máquina virtual. Para ter esta pasta criada na máquina virtual Arch, após instalar os [adicionais para convidado](#Adicionais_para_Convidado_2), você precisa adicionar seu nome de usuário ao grupo `vboxsf`.

```
# groupadd vboxsf
# gpasswd -a $USER vboxsf

```

**Nota:** Para que a **automontagem** funcione, você deve habilitar o serviço **vboxservice**.

Se você quer uma pasta compartilhada (e.g `/media/sd_Dropbox`) a ser simbolicamente linkada para outra pasta em seu diretório pessoal, para facilitar o acesso, você pode digitar no cliente:

```
$ ln -s /media/sf_Dropbox/* ~/dropbox

```

O script `VBoxLinuxAdditions.run` fornecido na ISO dos adicionais para convidado faz isso para você, porém o Arch não recomenda usá-lo.

Se as pastas compartilhadas não forem montadas automaticamente, tente montar manualmente. Para evitar problemas de inicialização quando estiver usando o [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") você deve adicionar `comment=systemd.automount` ao seu `/etc/fstab`. Dessa forma, eles serão montados apenas quando você acessar esses pontos de montagem e não durante a inicialização. Caso contrário, o sistema pode se tornar inutilizável após uma atualização do kernel (se você adicionar suas adições para convidado manualmente).

```
desktop   /media/desktop    vboxsf  uid=user,gid=group,rw,dmode=700,fmode=600,comment=systemd.automount 0 0

```

Não desperdice seu tempo para tentar o opção `nofail`. O `mount.vboxsf` não é capaz de lidar com isso (2012-08-20).

```
desktop   /media/desktop    vboxsf  uid=user,gid=group,rw,dmode=700,fmode=600,nofail 0 0

```

## Iniciar o VirtualBox

Para iniciar a interface gráfica do Virtualbox:

```
$ VirtualBox

```

## Solução de Problemas

### modprobe Exec format error

Atualize o seu sistema:

```
# pacman -Syu

```

### VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)

Isso pode ocorrer quando a máquina virtual é fechada inesperadamente. Para contornar o problema:

```
# VBoxManage controlvm nArch poweroff

```

### Could not load the Host USB Proxy service: VERR_NOT_FOUND

Às vezes, o subsistema USB não é detectado automaticamente ou um drive USB não é visível no host, mesmo quando o usuário está no grupo vboxusers. Adicione a seguinte linha ao seu `~/.bashrc`:

 `~/.bashrc`  `VBOX_USB=usbfs` 

Reinicie o seu sistema e abra uma nova instância do terminal. Também tenha certeza de que o usuário é membro do grupo **storage**.

### Failed to create the host-only network interface

Antes de tudo, tenha certeza de que você tem o pactoe [net-tools](https://www.archlinux.org/packages/?name=net-tools) instalado em seu sistema e em seguida faça os passos descritos em: [habilitando interface de rede Host-Only](#Habilitando_a_interface_de_rede_Host-Only).

### WinXP: Bit-depth cannot be greater than 16

Se você estiver executando em profundidade de cor de 16-bit, então os ícones parecerão distorcidos. No entanto, ao tentar mudar a profundidade da cor para uma resolução mais alta o sistema pode restringí-lo a uma resolução mais baixa ou, simplesmente não permitirá que você altere a resolução. Para corrigir isto, abra o `regedit` e adicione a seguinte chave ao registro da máquina virtual Windows XP:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services]
"ColorDepth"=dword:00000004

```

Em seguida, atualize a profundidade de cor na janela de propriedades do desktop. Se nada acontecer, force a tela para redesenhar (Ex. `host + f` para redesenhar a tela em Full Screen).

### Montando imagens .VDI

Só funciona com imagens VDi de tamanho estático (tamanho dinâmico não será fácil para montar). Precisamos obter uma informação de sua imagem VDI:

```
$ VBoxManage internalcommands dumphdinfo Arch_64min.vdi |grep offData
Header: offBlocks=4096 offData=69632

```

Agora, acrescente ao seu _offData_ **32256** (Ex.: `32256 + 69632 = 101888`) Monte a sua imagem VDI:

```
# mount -t ext4 -o rw,noatime,noexec,loop,offset=101888 Arch_64min.vdi /mnt/

```