**Status de tradução:** Esse artigo é uma tradução de [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine"). Data da última tradução: 2019-12-15\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Moving_an_existing_install_into_(or_out_of)_a_virtual_machine&diff=0&oldid=590842) na versão em inglês.

Artigos relacionados

*   [VirtualBox](/index.php/VirtualBox_(Portugu%C3%AAs) "VirtualBox (Português)")
*   [VMware](/index.php/VMware "VMware")
*   [QEMU](/index.php/QEMU "QEMU")
*   [Migrar instalação para novo hardware](/index.php/Migrate_installation_to_new_hardware "Migrate installation to new hardware")

Este artigo descreve como transferir sua instalação atual do Arch Linux para dentro ou fora de um ambiente virtual (por exemplo, QEMU, VirtualBox, VMware). Uma máquina virtual ("VM", abreviadamente) usa hardware diferente, que precisa ser endereçado regenerando a imagem initramfs e possivelmente ajustando o fstab - especialmente se for um [SSD](/index.php/SSD "SSD").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Movendo para fora da uma VM](#Movendo_para_fora_da_uma_VM)
    *   [1.1 Configurar uma pasta compartilhada](#Configurar_uma_pasta_compartilhada)
    *   [1.2 Transferir o sistema](#Transferir_o_sistema)
    *   [1.3 Entrar em chroot e reinstalar o gerenciador de boot](#Entrar_em_chroot_e_reinstalar_o_gerenciador_de_boot)
    *   [1.4 Ajustar o fstab](#Ajustar_o_fstab)
    *   [1.5 Gerar novamente a imagem initramfs](#Gerar_novamente_a_imagem_initramfs)
*   [2 Movendo para dentro de uma VM](#Movendo_para_dentro_de_uma_VM)
    *   [2.1 Criar o contêiner](#Criar_o_contêiner)
    *   [2.2 Transferir o sistema](#Transferir_o_sistema_2)
    *   [2.3 Converter o contêiner para um formato compatível](#Converter_o_contêiner_para_um_formato_compatível)
    *   [2.4 Entrar em chroot e reinstalar o gerenciador de boot](#Entrar_em_chroot_e_reinstalar_o_gerenciador_de_boot_2)
    *   [2.5 Ajustar o fstab](#Ajustar_o_fstab_2)
    *   [2.6 Desabilitar quaisquer arquivos relacionados a Xorg](#Desabilitar_quaisquer_arquivos_relacionados_a_Xorg)
    *   [2.7 Gerar novamente a imagem initramfs](#Gerar_novamente_a_imagem_initramfs_2)
*   [3 Solução de problemas](#Solução_de_problemas)
    *   [3.1 "mount: o dispositivo especial /dev/loop5p1 não existe"](#"mount:_o_dispositivo_especial_/dev/loop5p1_não_existe")
    *   [3.2 "Waiting 10 seconds for device /dev/sda1; ERROR: Unable to find root device '/dev/sda1'"](#"Waiting_10_seconds_for_device_/dev/sda1;_ERROR:_Unable_to_find_root_device_'/dev/sda1'")
    *   [3.3 "Missing operating system. FATAL: INT18: BOOT FAILURE"](#"Missing_operating_system._FATAL:_INT18:_BOOT_FAILURE")
    *   [3.4 Me pede a senha de root, para manutenção](#Me_pede_a_senha_de_root,_para_manutenção)

## Movendo para fora da uma VM

Mover para fora de um ambiente virtual é relativamente fácil.

### Configurar uma pasta compartilhada

A configuração de uma pasta compartilhada entre a máquina virtual convidada e o host depende do hipervisor usado. Por favor, refira-se à sua página wiki ou manual específico.

Se você ainda não possui uma partição ext4, veja [Sistemas de arquivos](/index.php/Sistemas_de_arquivos "Sistemas de arquivos").

Se você estiver no Windows, instale [Ext2Fsd](http://www.ext2fsd.com/) para poder montar volumes ext.

### Transferir o sistema

Na máquina virtual, abra um terminal e [transfira](/index.php/Rsync "Rsync") o sistema:

```
# rsync -aAXv /* /path/to/shared/folder --exclude={/dev/*,/proc/*,/sys/*,/tmp/*,/run/*,/mnt/*,/media/*,/lost+found,/home/*/.gvfs}

```

### Entrar em chroot e reinstalar o gerenciador de boot

Inicialize uma distribuição GNU/Linux "live", monte a partição root e faça [chroot](/index.php/Chroot_(Portugu%C3%AAs) "Chroot (Português)") nela.

Reinstale seu gerenciador de boot: [Syslinux](/index.php/Syslinux "Syslinux"), [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") ou [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). Não se esqueça de atualizar o arquivo de configuração: `syslinux.cfg` para o Syslinux, `grub.cfg` para o Grub ou as entradas de inicialização do systemd-boot localizadas em `/boot/loader/entries/`.

### Ajustar o fstab

Como toda a sua árvore raiz foi transferida para uma única partição, edite o arquivo [fstab](/index.php/Fstab "Fstab") para refletir a(s) partição(ões) correta(s).

Verifique com o comando `blkid`, já que `lsblk` não é muito útil dentro de um chroot.

### Gerar novamente a imagem initramfs

Como o hardware mudou, enquanto você ainda está no chroot, gere novamente a imagem do initramfs:

```
# mkinitcpio -p linux 

```

E é basicamente isso.

É provável que você precise configurar a rede, já que a máquina virtual provavelmente estava usando as configurações de rede do sistema operacional do host. Veja [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede").

## Movendo para dentro de uma VM

Mover para *dentro* de um ambiente virtual exige um pouco mais de esforço.

### Criar o contêiner

Isso criará uma imagem bruta de 10 GB:

```
# dd if=/dev/zero of=/media/Backup/backup.img bs=1024 count=10482381

```

**Dica:** Usar `fallocate` é muito mais rápido:
```
# fallocate -l 10GiB -o 1024 /media/Backup/backup.img

```

Se você quiser criar um com o tamanho exato de sua partição raiz, execute `fdisk -l` e use o valor da coluna `Blocos` para o parâmetro `count=`. Note que você irá transferir toda a sua árvore raiz, de modo que inclua as pastas `/boot` e `/home`. Se você tiver partições separadas para essas, precisará considerá-las ao criar o contêiner.

Agora carregue o módulo necessário e monte-o como um dispositivo de loopback, em `/dev/loop5` (por exemplo):

```
# modprobe loop
# losetup /dev/loop5 /media/Backup/backup.img

```

Em seguida, particione o dispositivo `/dev/loop5` executando sua ferramenta de [particionamento favorita](/index.php/Particionamento#Ferramentas_de_particionamento "Particionamento"). Crie uma tabela de partição nela (por exemplo, `msdos`), escolha o [esquema de partição](/index.php/Esquema_de_parti%C3%A7%C3%A3o "Esquema de partição") e crie as partições. Em seguida, crie um [sistema de arquivos](/index.php/Sistema_de_arquivos "Sistema de arquivos") nas partições, que aparecerão como `/dev/loop5p1`, `/dev/loop5p2`, etc.

### Transferir o sistema

Monte o dispositivo de loopback e [transfira](/index.php/Rsync "Rsync") o sistema:

**Nota:** Se o contêiner foi salvo em algum lugar diferente de `/mnt` ou `/media`, não se esqueça de adicioná-lo à lista de exclusões.

```
# mkdir /mnt/Virtual
# mount /dev/loop5p1 /mnt/Virtual
# rsync -aAXv /* /mnt/Virtual --exclude={/dev/*,/proc/*,/sys/*,/tmp/*,/run/*,/mnt/*,/media/*,/lost+found,/home/*/.gvfs}

```

### Converter o contêiner para um formato compatível

Escolha o comando apropriado, dependendo da máquina virtual desejada.

Para converter em um contêiner de **KVM**, use [qemu](https://www.archlinux.org/packages/?name=qemu) com a seguinte linha de comando:

```
$ qemu-img convert -c -f raw -O qcow /media/backup.img /media/backup.qcow2

```

Para converter em um contêiner do **VirtualBox**, use o [virtualbox](https://www.archlinux.org/packages/?name=virtualbox) com a seguinte linha de comando:

```
$ VBoxManage convertfromraw --format VDI /media/backup.img /media/backup.vdi

```

Para converter em um contêiner do **VMware**, use o *virtualbox* com a seguinte linha de comando:

```
$ VBoxManage convertfromraw --format VMDK /media/backup.img /media/backup.vmdk

```

### Entrar em chroot e reinstalar o gerenciador de boot

Conecte o contêiner à VM, juntamente com um LiveCD do Linux (por exemplo, o ISO do Arch Linux mais recente) no CD-ROM virtual da VM, em seguida, inicie a VM e faça [chroot](/index.php/Chroot_(Portugu%C3%AAs) "Chroot (Português)") nela:

```
# mount /dev/sda1 /mnt
# arch-chroot /mnt /bin/bash

```

Reinstale o [Syslinux](/index.php/Syslinux "Syslinux") ou o [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)"). Não esqueça de atualizar seu arquivo de configuração:

*   Para o Syslinux, deve ser `APPEND root=/dev/sda1 ro` no `syslinux.cfg`.

*   Para o GRUB, é recomendado que você gere de novo automaticamente um `grub.cfg`.

### Ajustar o fstab

Como toda a sua árvore raiz foi transferida para uma única partição, edite o arquivo [fstab](/index.php/Fstab "Fstab"). Você pode usar o UUID ou o rótulo, se quiser, mas eles são mais úteis em configurações de várias unidades e várias unidades (para evitar confusões). Por enquanto, `/dev/sda1` para todo o seu sistema está ótimo.

 `/etc/fstab` 
```
tmpfs                    /tmp      tmpfs     nodev,nosuid          0   0
/dev/sda1                /         ext4      defaults,noatime      0   1
```

### Desabilitar quaisquer arquivos relacionados a Xorg

Ter uma entrada `nvidia`, `nouveau`, `radeon`, `intel`, etc. na seção `Device` de uma dos arquivos de configuração do Xorg evitará que ele seja iniciado, já que você estará usando hardware *emulado* (incluindo a placa de vídeo). Portanto, é recomendável mover/renomear ou excluir o seguinte:

```
# mv /etc/X11/xorg.conf /etc/X11/xorg.conf.bak
# mv /etc/X11/xorg.conf.d/10-monitor /etc/X11/xorg.conf.d/10-monitor.bak

```

### Gerar novamente a imagem initramfs

Como o hardware mudou, enquanto você ainda está no chroot, gere novamente a imagem do initramfs e faça um desligamento adequado:

```
# mkinitcpio -p linux
# exit
# umount -R /mnt
# poweroff

```

Por fim, retire o LiveCD (o arquivo ISO), para que você não inicialize novamente nele e inicie a máquina virtual.

Aproveite o seu novo ambiente virtual.

## Solução de problemas

### "mount: o dispositivo especial /dev/loop5p1 não existe"

Use `losetup --partscan`, por exemplo:

```
# losetup --partscan /dev/loop5 /media/Backup/backup.img

```

Isso deve criar nós de dispositivo para cada partição que você criou dentro do dispositivo de loop.

### "Waiting 10 seconds for device /dev/sda1; ERROR: Unable to find root device '/dev/sda1'"

```
Waiting 10 seconds for device /dev/sda1 ...
ERROR: Unable to find root device '/dev/sda1'.
You are being dropped to a recovery shell
    Type 'exit' to try and continue booting
sh: cannot access tty; job control turned off
[rootfs /]# _

```

Isso provavelmente significa que você não executou `poweroff` como *você foi orientado* e fechou a VM com o botão "Fechar", que é o equivalente a uma queda de energia. Agora você precisa gerar novamente sua imagem de initramfs. Para fazer isso, você pode iniciar a VM usando a entrada reserva. Se você não tiver uma entrada reserva, pressione `Tab` (para Syslinux) ou `e` (para GRUB) e renomeie-a para `initramfs-linux-fallback.img`. Depois de inicializar, abra um terminal e execute:

```
# mkinitcpio -p linux
# poweroff

```

### "Missing operating system. FATAL: INT18: BOOT FAILURE"

*   Você precisa instalar ou reinstalar um gerenciador de boot. Veja [Processo de inicialização do Arch#Gerenciador de boot](/index.php/Processo_de_inicializa%C3%A7%C3%A3o_do_Arch#Gerenciador_de_boot "Processo de inicialização do Arch").

*   Você está usando um sistema de arquivos [Btrfs](/index.php/Btrfs "Btrfs") com compressão para `/boot`, do qual o [Syslinux](/index.php/Syslinux "Syslinux") atualmente não consegue inicializar.

*   A ordem de inicialização do BIOS ou das configurações da VM não está configurada corretamente. Certifique-se de que a unidade que contém o gerenciador de boot seja a primeira a ser inicializada.

### Me pede a senha de root, para manutenção

```
:: Checking Filesystems                        [BUSY]
fsck.ext4: Unable to resolve '...'

```

Isso significa que você esqueceu de adicionar o UUID da unidade, o rótulo ou o nome do dispositivo em `/etc/fstab`. O UUID é diferente toda vez que você o formata (ou, neste caso, cria um do zero), e eles provavelmente não coincidem. Verifique com `blkid`.