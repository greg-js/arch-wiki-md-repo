**Status de tradução:** Esse artigo é uma tradução de [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). Data da última tradução: 2019-08-15\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Kernel_parameters&diff=0&oldid=573634) na versão em inglês.

Existem três maneiras de passar opções para o kernel e, assim, controlar seu comportamento:

1.  Ao compilar o kernel. Veja [Kernel (Português)#Compilação](/index.php/Kernel_(Portugu%C3%AAs)#Compilação "Kernel (Português)") para detalhes.
2.  Ao iniciar o kernel (geralmente, quando chamado por um gerenciador de boot).
3.  Em tempo real (através de arquivos no `/proc` e no `/sys`). Veja [sysctl](/index.php/Sysctl "Sysctl") para detalhes.

Esta página explica mais detalhadamente o segundo método e mostra uma lista dos parâmetros do kernel mais usados no Arch Linux.

Nem todos os parâmetros estão sempre disponíveis. A maioria está associada a subsistemas e funciona apenas se o kernel estiver configurado com esses subsistemas integrados. Eles também dependem da presença do hardware ao qual estão associados.

Parâmetros têm o formato `parâmetro` ou `parâmetro=valor`.

**Nota:** Todos os parâmetros do kernel diferenciam maiúsculo de minúsculo.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuração](#Configuração)
    *   [1.1 Syslinux](#Syslinux)
    *   [1.2 systemd-boot](#systemd-boot)
    *   [1.3 GRUB](#GRUB)
    *   [1.4 GRUB Legacy](#GRUB_Legacy)
    *   [1.5 LILO](#LILO)
    *   [1.6 rEFInd](#rEFInd)
    *   [1.7 EFISTUB](#EFISTUB)
    *   [1.8 Sobrepondo cmdline](#Sobrepondo_cmdline)
*   [2 Lista de parâmetros](#Lista_de_parâmetros)
*   [3 Veja também](#Veja_também)

## Configuração

**Nota:**

*   Você pode verificar os parâmetros com que seu sistema foi inicializado executando `cat /proc/cmdline` e veja se ele inclui suas alterações.
*   A [mídia de instalação](https://www.archlinux.org/download/) do Arch Linux usa [Syslinux](/index.php/Syslinux "Syslinux") para sistemas [BIOS](https://en.wikipedia.org/wiki/pt:BIOS "wikipedia:pt:BIOS") e [systemd-boot](/index.php/Systemd-boot "Systemd-boot") para sistemas [UEFI](/index.php/UEFI "UEFI").

Os parâmetros do kernel podem ser definidos temporariamente, editando a entrada de inicialização no menu de seleção de inicialização do gerenciador de boot ou modificando seu arquivo de configuração.

Os exemplos a seguir adicionam os parâmetros `quiet` e `splash` a [Syslinux](/index.php/Syslinux "Syslinux"), [systemd-boot](/index.php/Systemd-boot "Systemd-boot"), [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)"), [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"), [LILO](/index.php/LILO "LILO") e [rEFInd](/index.php/REFInd "REFInd").

### Syslinux

*   Pressione `Tab` quando o menu é exibido e adicione-os ao final da string:

	 `linux /boot/vmlinuz-linux root=/dev/sda3 initrd=/boot/initramfs-linux.img *quiet splash*` 

	Pressione `Enter` para inicializar com esses parâmetros.

*   Para tornar persistentes as alterações após a reinicialização, edite `/boot/syslinux/syslinux.cfg` e adicione-os à linha `APPEND`:

	 `APPEND root=/dev/sda3 *quiet splash*` 

Para mais informações sobre configurar o Syslinux, veja o artigo [Syslinux](/index.php/Syslinux "Syslinux").

### systemd-boot

*   Pressione `e` quando o menu aparecer e adicione os parâmetros ao final da string:

	 `initrd=\initramfs-linux.img root=/dev/sda2 *quiet splash*` 

	Pressione `Enter` para inicializar com esses parâmetros.

**Nota:**

*   Se você não tiver definido um valor para o tempo limite do menu, será necessário manter `Espaço` pressionado durante a inicialização para que o menu do systemd-boot apareça.
*   Se você não conseguir editar os parâmetros no menu de inicialização, você pode precisar editar o `/boot/loader/loader.conf` e adicionar o `editor 1` para habilitar a edição.

*   Para tornar persistentes as alterações após a reinicialização, edite `/boot/loader/entries/arch.conf` (presumindo que você configurou sua [partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI")) e adicionou-as à linha `options`:

	 `options root=/dev/sda2 *quiet splash*` 

Para mais informações sobre configurar o systemd-boot, veja o artigo [systemd-boot](/index.php/Systemd-boot "Systemd-boot").

### GRUB

*   Pressione `e` quando o menu é exibido e adicione-os à linha `linux`:

	 `linux /boot/vmlinuz-linux root=UUID=978e3e81-8048-4ae1-8a06-aa727458e8ff *quiet splash*` 

	Pressione `Ctrl+x` para inicializar com esses parâmetros.

*   Para tornar persistentes as alterações após a reinicialização, você *poderia* editar manualmente `/boot/grub/grub.cfg` com exatamente a linha acima, mas a melhor prática é:

	Editar `/etc/default/grub` e anexar suas opções de kernel à linha `GRUB_CMDLINE_LINUX_DEFAULT`:

	 `GRUB_CMDLINE_LINUX_DEFAULT="*quiet splash*"` 

	E, então, gerar novamente automaticamente o arquivo `grub.cfg` com:

	 `# grub-mkconfig -o /boot/grub/grub.cfg` 

Para mais informações sobre configurar o GRUB, veja o artigo [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)").

### GRUB Legacy

*   Pressione `e` quando o menu é exibido e adicione-os à linha `kernel`:

	 `kernel /boot/vmlinuz-linux root=/dev/sda3 *quiet splash*` 

	Pressione `b` para inicializar com esses parâmetros.

*   Para tornar persistentes as alterações após a reinicialização, edite `/boot/grub/menu.lst` e adicione-os à linha `kernel`, exatamente como acima.

Para mais informações sobre configurar o GRUB Legacy, veja o artigo [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy").

### LILO

*   Adicione-os a `/etc/lilo.conf`:

```
image=/boot/vmlinuz-linux
        ...
        *quiet splash*
```

Para mais informações sobre configurar o LILO, veja o artigo [LILO](/index.php/LILO "LILO").

### rEFInd

*   Pressione `+`, `F2` ou `Insert` na entrada do menu desejada e pressione-a novamente na entrada do submenu. Adicione os parâmetros do kernel ao final da string:

	 `root=PARTUUID=978e3e81-8048-4ae1-8a06-aa727458e8ff rw initrd=\boot\initramfs-linux.img *quiet splash*` 

	Pressione `Enter` para inicializar com esses parâmetros.

*   Para tornar persistentes as alterações após a reinicialização, edite `/boot/refind_linux.conf` e anexe-os a todas as linhas, ou apenas às necessárias, por exemplo

	 `"Boot using default options"   "root=PARTUUID=978e3e81-8048-4ae1-8a06-aa727458e8ff rw *quiet splash*"` 

*   Se você desativou a detecção automática de sistemas operacionais em rEFInd e está definindo sub-rotinas do sistema operacional em vez de `*esp*/EFI/refind/refind.conf` para carregar seus sistemas operacionais, é possível editá-lo como:

```
menuentry "Arch Linux" {
	...
	options  "root=PARTUUID=978e3e81-8048-4ae1-8a06-aa727458e8ff rw *quiet splash*"
	...
}

```

Para mais informações sobre configurar o rEFInd, veja o artigo [rEFInd](/index.php/REFInd "REFInd").

### EFISTUB

Veja [EFISTUB (Português)#Usando UEFI diretamente](/index.php/EFISTUB_(Portugu%C3%AAs)#Usando_UEFI_diretamente "EFISTUB (Português)").

### Sobrepondo cmdline

Mesmo sem acesso ao seu gerenciador de boot, é possível alterar os parâmetros do kernel para habilitar a depuração (se você tiver acesso root). Isso pode ser feito sobrescrevendo `/proc/cmdline`, que armazena os parâmetros do kernel. No entanto, `/proc/cmdline` não é gravável, mesmo como root, portanto, esse *hack* é realizado usando uma montagem de ligação para mascarar o caminho.

Primeiro crie um arquivo contendo os parâmetros desejados do kernel

 `/root/cmdline`  `root=/dev/disk/by-label/ROOT ro console=tty1 logo.nologo debug` 

Em seguida, use uma montagem de "bind" para sobrescrever os parâmetros

```
# mount -n --bind -o ro /root/cmdline /proc/cmdline

```

A opção `-n` pula a adição da montagem a `/etc/mtab`, portanto, funcionará mesmo se a raiz estiver montada como somente leitura. Você pode `cat /proc/cmdline` para confirmar que sua alteração foi bem-sucedida.

## Lista de parâmetros

Esta lista não é exaustiva. Para obter uma lista completa de todas as opções, consulte a [documentação do kernel](https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.txt)

| parâmetro | Descrição |
| root= | Sistema de arquivo raiz. Consulte [init/do_mounts.c](https://github.com/torvalds/linux/blob/f49aa1de98363b6c5fba4637678d6b0ba3d18065/init/do_mounts.c#L191-L219) por formatos de nome de dispositivos compatíveis. |
| rootflags= | Opções de montagem do sistema de arquivos raiz |
| ro | Monta o dispositivo raiz como somente leitura na inicialização (padrão). |
| rw | Monta o dispositivo raiz como leitura e gravação na inicialização. |
| initrd= | Especifica o local do ramdisk inicial. |
| init= | Executa o binário especificado em vez de `/sbin/init` como processo init. O pacote [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) cria links simbólicos `/sbin/init` para `/usr/lib/systemd/systemd` para usar o [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"). |
| init=/bin/sh | Inicializa para o shell. |
| systemd.unit= | Inicializa para um [target especificado](/index.php/Systemd_(Portugu%C3%AAs)#Targets "Systemd (Português)"). |
| resume= | Especifica um dispositivo swap para usar ao acordar de [hibernation](/index.php/Hibernation "Hibernation"). |
| nomodeset | Desabilita [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting"). |
| zswap.enabled | Habilita [Zswap](/index.php/Zswap "Zswap"). |
| panic= | Tempo antes de reiniciar automaticamente ao ocorrer "kernel panic". |
| debug | Habilita depuração de kernel (nível de log de eventos). |
| mem= | Força o uso de uma quantidade específica de memória a ser usada. |
| maxcpus= | Número máximo de processadores que um kernel SMP vai usar durante a inicialização. |
| selinux= | Desabilita ou habilita o SELinux em tempo de inicialização. |
| netdev= | Parâmetros de dispositivos de rede. |
| video= | Sobrepõe configurações padrão do vídeo framebuffer. |

 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") usa `ro` como valor padrão quando `rw` nem `ro` é definido pelo [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot"). Gerenciadores de boot podem definir o valor a ser usado. Por exemplo, o GRUB usa `rw` por padrão (veja [FS#36275](https://bugs.archlinux.org/task/36275) como referência).

## Veja também

*   [Documentação "Kernel Parameters" do Linux](https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.txt)
*   [Power saving#Kernel parameters](/index.php/Power_saving#Kernel_parameters "Power saving")
*   [Lista de parâmetros do kernel com mais explicações e agrupados por opções semelhantes](http://files.kroah.com/lkn/lkn_pdf/ch09.pdf)