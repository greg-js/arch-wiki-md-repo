**Status de tradução:** Esse artigo é uma tradução de [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key"). Data da última tradução: 2019-01-27\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Installing_Arch_Linux_on_a_USB_key&diff=0&oldid=564449) na versão em inglês.

Artigos relacionados

*   [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação")
*   [Recomendações gerais](/index.php/Recomenda%C3%A7%C3%B5es_gerais "Recomendações gerais")
*   [Solução de problemas gerais](/index.php/General_troubleshooting "General troubleshooting")

Esta página explica como realizar uma instalação normal do Arch em um pendrive (também conhecido como "unidade flash" ou, em inglês, de *USB key*). Em contraste com o fato de ter um LiveUSB coberto em [Mídia de instalação em flash USB](/index.php/M%C3%ADdia_de_instala%C3%A7%C3%A3o_em_flash_USB "Mídia de instalação em flash USB"), o resultado será uma instalação persistente idêntica à instalação normal em HDD, mas em uma unidade flash USB.

## Contents

*   [1 Instalação](#Instalação)
    *   [1.1 Ajustes na instalação](#Ajustes_na_instalação)
*   [2 Configuração](#Configuração)
    *   [2.1 GRUB legado](#GRUB_legado)
    *   [2.2 GRUB](#GRUB)
    *   [2.3 Syslinux](#Syslinux)
*   [3 Dicas](#Dicas)
    *   [3.1 Usando sua instalação USB em múltiplas máquinas](#Usando_sua_instalação_USB_em_múltiplas_máquinas)
        *   [3.1.1 Drivers de entrada](#Drivers_de_entrada)
        *   [3.1.2 Drivers de vídeo](#Drivers_de_vídeo)
        *   [3.1.3 Nomenclatura de dispositivos de bloco persistentes](#Nomenclatura_de_dispositivos_de_bloco_persistentes)
        *   [3.1.4 Parâmetros do kernel](#Parâmetros_do_kernel)
        *   [3.1.5 Inicializando de mídia USB 3.0](#Inicializando_de_mídia_USB_3.0)
    *   [3.2 Compatibilidade](#Compatibilidade)
    *   [3.3 Minimizando o acesso a disco](#Minimizando_o_acesso_a_disco)
*   [4 Veja também](#Veja_também)

## Instalação

**Nota:** Recomenda-se pelo menos 2 GB de espaço de armazenamento. Um conjunto modesto de pacotes vai caber, deixando um pouco de espaço livre para armazenamento.

Existem várias maneiras de instalar o Arch em um pendrive, dependendo do sistema operacional disponível:

*   Se você tem outro computador Linux disponível (não precisa ser o Arch), você pode seguir as instruções em [Instalar a partir de um Linux existente](/index.php/Instalar_a_partir_de_um_Linux_existente "Instalar a partir de um Linux existente").
*   Um Arch Linux CD/USB pode ser usado para instalar o Arch no pendrive, através da inicialização do CD/USB e seguindo o [guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação"). Se for inicializar de um Live USB, a instalação terá que ser feita em um pendrive diferente.
*   Se você usar Windows ou OS X, faça o download do VirtualBox, instale as VirtualBox Extensions, adicione a unidade USB a uma máquina virtual executando o Arch (por exemplo, executando a partir de uma ISO), aponte a instalação para a unidade USB enquanto usa as instruções no [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação").

### Ajustes na instalação

*   Antes de [criar o disco de RAM inicial](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio"), em `/etc/mkinitcpio.conf` mova os hooks `block` e `keyboard` antes do hook `autodetect`. Isso é necessário para permitir a inicialização em vários sistemas. cada um exigindo módulos diferentes no espaço do usuário anterior.
*   É altamente recomendável revisar o artigo wiki sobre [redução leitura/escrita de disco](/index.php/Improving_performance#Reduce_disk_reads/writes "Improving performance") antes de selecionar um sistema de arquivos. Resumindo, [ext4 sem um jornal](http://fenidik.blogspot.com/2010/03/ext4-disable-journal.html) está bom, o qual pode ser criado com `# mkfs.ext4 -O "^has_journal" /dev/sdXX`. A desvantagem óbvia de usar um sistema de arquivos com o *journaling* desativado é a perda de dados como resultado de uma desmontagem desajeitada. Reconheça que o flash tem um número limitado de gravações, e um sistema de arquivos com *journaling* levará alguns deles à medida que o journal for atualizado. Por esse mesmo motivo, é melhor nem pensar a partição swap. Observe que isso não afeta a instalação em um disco rígido USB.
*   Se você quiser continuar a usar o dispositivo UFD como uma unidade removível multiplataforma, isso pode ser feito criando uma partição que hospede um sistema de arquivos apropriado (provavelmente NTFS ou exFAT). Observe que a partição de dados pode precisar ser a primeira partição no dispositivo, pois o Windows pressupõe que só pode haver uma partição em um dispositivo removível e, de outra forma, terá uma montagem automática de uma partição do sistema EFI. Lembre-se de instalar [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) e [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g). Algumas ferramentas estão disponíveis on-line que podem permitir que você mude o bit de mídia removível em seu dispositivo UFD. Isso faria com que os sistemas operacionais tratassem seu dispositivo UFD como um disco rígido externo e permitisse que você usasse qualquer esquema de particionamento escolhido.

**Atenção:** Não é possível mudar o bit de mídia removível em todos os dispositivos UFD e tentar usar software incompatível com o dispositivo pode danificá-lo. A tentativa de mudar o bit de mídia removível **não** é recomendada.

## Configuração

*   Certifique-se de que `/etc/fstab` inclua as informações de partição corretas para `/` e para quaisquer outras partições no pendrive. Se o pendrive for inicializado em várias máquinas, é bem provável que os dispositivos e o número de discos rígidos disponíveis variem. Por isso, é aconselhável usar o UUID ou o rótulo.

Para obter os UUIDs adequados para sua partição, emita **blkid**

**Nota:**

*   Quando o GRUB é instalado no pendrive, o pendrive sempre será `hd0,0`.
*   Parece que as versões atuais do GRUB serão automaticamente padronizadas para usar o uuid. As instruções a seguir são para GRUB legado.

### GRUB legado

`menu.lst`, o arquivo de configuração do GRUB legado, deve ser editado para (mais ou menos) corresponder às configurações a seguir.

Quando estiver usando rótulo, seu menu.lst deve se parecer com isso:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-label/**Arch** rw
initrd /boot/initramfs-linux.img

```

E para UUID, deve se parecer com isso:

```
root (hd0,0)
kernel /boot/vmlinuz-linux root=/dev/disk/by-uuid/3a9f8929-627b-4667-9db4-388c4eaaf9fa rw
initrd /boot/initramfs-linux.img

```

### GRUB

Na GPT com instalações UEFI, certifique-se de seguir as instruções em [GRUB#UEFI systems](/index.php/GRUB#UEFI_systems "GRUB") e incluir a opção `--removable`, pois isso pode interromper as instalações do GRUB existentes, como no comando abaixo:

```
# grub-install --target=x86_64-efi --efi-directory=*esp* **--removable** --recheck

```

### Syslinux

Usando seu UUID:

```
LABEL Arch
        MENU LABEL Arch Linux
        LINUX ../vmlinuz-linux
        APPEND root=UUID=3a9f8929-627b-4667-9db4-388c4eaaf9fa rw
        INITRD ../initramfs-linux.img

```

## Dicas

### Usando sua instalação USB em múltiplas máquinas

#### Drivers de entrada

Para o uso de laptop (ou use com uma tela tátil) você precisará do pacote [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) para o touchpad/touchscreen funcionar.

Para obter instruções sobre ajuste fino ou solução de problemas do touchpad, consulte o artigo [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

#### Drivers de vídeo

**Nota:** O uso de drivers de vídeo proprietários **não** é recomendado para este tipo de instalação.

Para obter suporte às GPUs mais comuns, instale [xf86-video-vesa](https://www.archlinux.org/packages/?name=xf86-video-vesa), [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati), [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) e [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau).

#### Nomenclatura de dispositivos de bloco persistentes

Recomenda-se usar o [UUID](/index.php/UUID "UUID") tanto na configuração do [fstab](/index.php/Fstab "Fstab") quanto na do gerenciador de inicialização. Veja [Nomenclatura de dispositivo de bloco persistente](/index.php/Persistent_block_device_naming "Persistent block device naming") para detalhes.

Alternativamente, você pode criar a regra do udev para criar um link simbólico personalizado para seu pendrive. Em seguida, use este link simbólico na configuração do fstab e do gerenciador de inicialização. Veja [udev#Setting static device names](/index.php/Udev#Setting_static_device_names "Udev") para detalhes.

#### Parâmetros do kernel

Você pode desabilitar KMS por vários motivos, como obter uma tela em branco ou um erro de "sem sinal" no visor, ao usar algumas placas de vídeo Intel, etc. Para desabilitar o KMS, adicione `nomodeset` como um parâmetro do kernel. Veja [Parâmetros do kernel](/index.php/Kernel_parameters "Kernel parameters") para mais informações.

**Atenção:** Alguns drivers [Xorg](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") não funcionam com o KMS desabilitado. Veja a página wiki em seu driver específico para detalhes. O Nouveau, em particular, precisa do KMS para determinar a resolução de exibição correta. Se você adicionar `nomodeset` como um parâmetro do kernel como uma medida preventiva, pode ser necessário ajustar a resolução de exibição manualmente ao usar máquinas com placas de vídeo Nvidia. Veja [Xrandr](/index.php/Xrandr "Xrandr") para mais informações.

#### Inicializando de mídia USB 3.0

Veja [[1]](http://www.wyae.de/docs/boot-usb3/).

### Compatibilidade

A imagem alternativa deve ser usada para compatibilidade máxima.

### Minimizando o acesso a disco

*   Você pode querer configurar o [journal do systemd](/index.php/Journal_do_systemd "Journal do systemd") para armazenar seus journals na RAM, por exemplo, criando um arquivo de configuração personalizado:

 `/etc/systemd/journald.conf.d/usbstick.conf` 
```
[Journal]
Storage=volatile
RuntimeMaxUse=30M
```

*   Para desabilitar `fsync` e chamadas de sistema relacionadas em navegadores web e outros aplicativos que não escrevem dados essenciais, use o comando *eatmydata* do [libeatmydata](https://aur.archlinux.org/packages/libeatmydata/) para evitar tais chamadas de sistema:

```
$ eatmydata firefox

```

## Veja também

*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives")