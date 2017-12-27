## Contents

*   [1 Introdução](#Introdu.C3.A7.C3.A3o)
*   [2 Boot através da midia](#Boot_atrav.C3.A9s_da_midia)
*   [3 Configure o SSH no ambiente Live](#Configure_o_SSH_no_ambiente_Live)
*   [4 Conectar ao PC destino através do ssh](#Conectar_ao_PC_destino_atrav.C3.A9s_do_ssh)
    *   [4.1 Notas](#Notas)
*   [5 Próximos Passos](#Pr.C3.B3ximos_Passos)

## Introdução

Este artigo possui o intuito de mostrar aos usuários como instalar o Arch através de uma conexão SSH. Considere esta forma de instalação a padrão nos seguintes cenários:

Instalando o Arch em um...

*   Home Theater Personal Computer(HTPC) sem um monitor conectado.
*   Um PC localizado em outra cidade, estado, país(casa do amigo, de um parente, etc.)
*   Um PC que pode ser tranquilamente instalado remoto, para que você possa desfrutar do conforto de sua Workstation com capacidades de copiar/colar coisas da Wiki do Arch.

**Nota:** Nas primeiras duas opções, o acesso físico a máquina é necessário. Obviamente, se estiver localizado em qualquer lugar longínquo, você deverá coordenar esforços com outra pessoa!

## Boot através da midia

Inicie um ambiente [Live CD/USB](/index.php/Beginners%27_guide_(Portugu%C3%AAs)#Obtendo_a_.C3.BAltima_m.C3.ADdia_de_Instala.C3.A7.C3.A3o "Beginners' guide (Português)") do Arch Linux

## Configure o SSH no ambiente Live

**Nota:** Os seguintes comandos devem ser executados com o usuário root, motivo pelo qual existe o **#** antes dos comandos.

Neste exato momento, você deve estar logado como root(pois este é o comportamento padrão do livecd)

Configure então, a rede da máquina em questão.

Supondo que a conexão é através de uma rede cabeada, um `dhclient` ou `dhcpcd` é o suficiente para obter um lease. Para maiores informações, visite [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede").

Se estiver em uma rede sem fio, os artigos [configuração de rede sem fio](/index.php/Wireless_Setup "Wireless Setup") e [Wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant") dão maiores detalhes de como estabelecer uma conexão com o seu access point.

Logo após, execute o daemont do ssh

Em um livecd que utiliza o systemd: (2012.10.06 ou posterior)

```
# systemctl start sshd

```

Em um livecd que utiliza os initscripts: (pre-2012.10.06)

```
# rc.d start sshd

```

Finalmente, configure uma senha para o usuário root, necessária para a conexão; a senha padrão do Arch para o usuário root é a senha vazia.

## Conectar ao PC destino através do ssh

Conecte a máquina destino através do seguinte comando:

```
$ ssh root@endereço.ip.do.destino

```

A partir daqui, a mensagem de bemvindo do ambiente live será exibida, e você será capaz de administrar a máquina como se estivesse sentado em frente ao teclado físico.

```
ssh root@10.1.10.105
root@10.1.10.105's password: 
Last login: Thu Dec 23 08:33:02 2010 from 10.1.10.200
[root@archiso ~]#
```

### Notas

*   Se o computador destino está atrás de algum firewall/roteador, a porta 22(ssh) deverá ser obviamente encaminhada para o IP LAN da máquina em questão. O assunto de encaminhamento de portas não está no escopo deste guia.
*   Você pode editar o `/etc/ssh/sshd_config` no ambiente live para alterar a porta padrão de escuta do daemon do ssh se você desejar

## Próximos Passos

O céu é o limite. Se você pretende apenas instalar o Arch, siga o [guia de instalação](/index.php/Installation_guide_(Portugu%C3%AAs) "Installation guide (Português)"). Já se o objetivo é editar/manipular uma instalação Linux que está com problemas, siga o artigo [Instalando em um Linux já configurado](/index.php/Install_from_existing_Linux "Install from existing Linux").

Deseja que o [grub2](/index.php/Grub2 "Grub2") utilize disco rígido [GPT](/index.php/GPT "GPT")?

*   Particione manualmente o dispositivo utilizando o utilitário **gdisk**, instalado através do comando *pacman -S gdisk* antes de iniciar a instalação do Arch Linux
*   Instalar o grub2 é trivial a partir deste momento. Apenas execute o chroot no seu Arch recém-instalado e instale o grub2 assim:

```
cd /mnt
rm console ; mknod -m 600 console c 5 1
rm null ; mknod -m 666 null c 1 3
rm zero ; mknod -m 666 zero c 1 5
mount -t proc proc /mnt/proc
mount -t sysfs sys /mnt/sys
mount -o bind /dev /mnt/dev
chroot /mnt /bin/bash

```

Agora, de dentro do chroot:

```
pacman -S grub2
grep -v rootfs /proc/mounts > /etc/mtab

```

Edite od `/etc/default/grub` de acordo com suas necessidades. Instale o grub, e gere o grub.cfg

```
grub-install /dev/sdX --no-floppy
grub-mkconfig -o /boot/grub/grub.cfg

```

**Nota:** O procedimento acima assume que você deseja dar boot em um disco GPT, e que o usuário entende previamente os conceitos expostos nos artigos desta wiki, e mais, que a partição de 1M ef02 para o grub2 foi criada.

Quando estiver pronto para reiniciar no Arch, saia do chroot e desmonte as partições antes de efetuar o processo de reboot.

```
exit
umount /mnt/boot   # if mounted this or any other separate partitions
umount /mnt/{proc,sys,dev}
umount /mnt

```