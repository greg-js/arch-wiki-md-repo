<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Protegendo a partição de boot não criptografada](#Protegendo_a_partição_de_boot_não_criptografada)
    *   [1.1 Inicializando de um dispositivo removível](#Inicializando_de_um_dispositivo_removível)
    *   [1.2 chkboot](#chkboot)
    *   [1.3 mkinitcpio-chkcryptoboot](#mkinitcpio-chkcryptoboot)
        *   [1.3.1 Instalação](#Instalação)
        *   [1.3.2 Visão geral técnica](#Visão_geral_técnica)
    *   [1.4 AIDE](#AIDE)
    *   [1.5 STARK](#STARK)
*   [2 Usando keyfiles criptografadas com GPG, LUKS ou OpenSSL](#Usando_keyfiles_criptografadas_com_GPG,_LUKS_ou_OpenSSL)
*   [3 Abrir remotamente a partição raiz (ou outra)](#Abrir_remotamente_a_partição_raiz_(ou_outra))
    *   [3.1 Abrir remotamente (hooks: systemd, systemd-tool)](#Abrir_remotamente_(hooks:_systemd,_systemd-tool))
    *   [3.2 Abrir remotamente (hooks: netconf, dropbear, tinyssh, ppp)](#Abrir_remotamente_(hooks:_netconf,_dropbear,_tinyssh,_ppp))
    *   [3.3 Abrir remotamente pelo wifi](#Abrir_remotamente_pelo_wifi)
        *   [3.3.1 Hook predefinido](#Hook_predefinido)
        *   [3.3.2 Faça o seu próprio](#Faça_o_seu_próprio)
*   [4 Suporte a discard/TRIM para unidades de estado sólido (SSD)](#Suporte_a_discard/TRIM_para_unidades_de_estado_sólido_(SSD))
*   [5 O hook encrypt e múltiplos discos](#O_hook_encrypt_e_múltiplos_discos)
    *   [5.1 Expandindo LVM em múltiplos discos](#Expandindo_LVM_em_múltiplos_discos)
        *   [5.1.1 Adicionando uma nova unidade de armazenamento](#Adicionando_uma_nova_unidade_de_armazenamento)
        *   [5.1.2 Extendendo o volume lógico](#Extendendo_o_volume_lógico)
    *   [5.2 Modificando o hook encrypt para múltiplas partições](#Modificando_o_hook_encrypt_para_múltiplas_partições)
        *   [5.2.1 sistema de arquivos principal expandido para múltiplas partições](#sistema_de_arquivos_principal_expandido_para_múltiplas_partições)
        *   [5.2.2 Múltiplas partições não raiz](#Múltiplas_partições_não_raiz)
*   [6 Sistema criptografado usando um cabeçalho LUKS desanexado](#Sistema_criptografado_usando_um_cabeçalho_LUKS_desanexado)
    *   [6.1 Usando o hook do systemd](#Usando_o_hook_do_systemd)
    *   [6.2 Modificando o hook encrypt](#Modificando_o_hook_encrypt)
*   [7 Encrypted /boot and a detached LUKS header on USB](#Encrypted_/boot_and_a_detached_LUKS_header_on_USB)
    *   [7.1 Preparing the disk devices](#Preparing_the_disk_devices)
        *   [7.1.1 Preparing the USB key](#Preparing_the_USB_key)
        *   [7.1.2 The main drive](#The_main_drive)
    *   [7.2 Installation procedure and custom encrypt hook](#Installation_procedure_and_custom_encrypt_hook)
        *   [7.2.1 Boot Loader](#Boot_Loader)
    *   [7.3 Changing the LUKS keyfile](#Changing_the_LUKS_keyfile)

## Protegendo a partição de boot não criptografada

A partição `/boot` e o [Master Boot Record](/index.php/Particionamento#Master_Boot_Record "Particionamento") são duas áreas do disco que não são criptografadas até mesmo com a [raiz criptografada](/index.php/Dm-crypt/Criptografando_todo_um_sistema "Dm-crypt/Criptografando todo um sistema"). Estes não podem ser usualmente criptografados porquê o [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") e BIOS (respectivamente) não são capazes de abrir o container do dm-crypt para continuar o processo de inicialização. Uma exceção é o [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)"), que tem a funcionalidade de abrir a partição `/boot` criptografada - veja [dm-crypt/Criptografando todo um sistema#Partição de boot criptografada (GRUB)](/index.php/Dm-crypt/Criptografando_todo_um_sistema#Partição_de_boot_criptografada_(GRUB) "Dm-crypt/Criptografando todo um sistema").

Esta seção descreve passos que podem ser feitos para fazer o processo de inicialização mais seguro.

**Atenção:** Note que proteger a partição `/boot` e MBR pode mitigar numerosos ataques que ocorrem no processo de inicialização, mas sistemas configurados desta maneira ainda podem estar vuneráveis a adulteração da BIOS/UEFI/firmware, keyloggers de hardware, ataques cold boot, e outras ameaças que estão fora do escopo deste artigo. Para uma visão geral da confiabilidade do sistema e como estes são relacionados a encriptação total de sistema, veja [[1]](http://www.youtube.com/watch?v=pKeiKYA03eE).

### Inicializando de um dispositivo removível

**Atenção:** O gerador do systemd versão 230 para o cryptsetup emite `RequiresMountsFor` para a keyfile. Quando o sistema de arquivos que possui este arquivo é desmontado, o serviço do cryptsetup também para. Este comportamento está correto porquê o sistema de arquivos e a chave criptografada são necessários somente quando o container criptografado é inicialmente aberto. Veja a [systemd issue 3816](https://github.com/systemd/systemd/issues/3816).

Usar um dispositivo separado para inicializar um sistema é um procedimento bastante simples, e oferece uma significante melhora na segunraça contra alguns tipos de ataques. Duas partes vulneráveis de um sistema com [raiz criptografada](/index.php/Dm-crypt/Criptografando_todo_um_sistema "Dm-crypt/Criptografando todo um sistema") são:

*   o [Master Boot Record](/index.php/Particionamento#Master_Boot_Record "Particionamento"), e
*   a partição `/boot`.

Estas devem ser guardadas em forma não criptografada para o sistema inicializar. Para protegê-las de adulteração, é recomendado usar uma unidade de armazenamento removível, como um pendrive, e inicializar por meio desta ao invês do disco interno. Enquanto você cuidar e guardar consigo a unidade de armazenamento removível, vai ter certeza que esta não foi adulterada, fazendo a autentificação muito mais segura quando abrir seu sistema.

É assumido que você já configurou seu sistema e tem um partição dedicada montada em `/boot`. Se não, siga os passos em [dm-crypt/Configuração do sistema#Gerenciador de boot](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Gerenciador_de_boot "Dm-crypt/Configuração do sistema"), substituindo a sua unidade de armazenamento por uma removível.

**Nota:** Você deve ter certeza que seu sistema suporta a inicialização por uma unidade de armazenamento removível, seja esta um pendrive, HD externo, cartão SD, ou qualquer outra coisa.

Prepare a unidade de armazenamento removível (`/dev/sdx`).

```
# gdisk /dev/sdx # formate se necessário. Pode usar também cgdisk, fdisk, cfdisk, gparted...
# mkfs.ext2 /dev/sdx1
# mount /dev/sdx1 /mnt

```

Copie o que tiver no `/boot` para o novo.

```
# cp -ai /boot/* /mnt/

```

Monte a nova partição. Não se esqueça de atualizar o [fstab](/index.php/Fstab "Fstab") de acordo.

```
# umount /boot
# umount /mnt
# mount /dev/sdx1 /boot
# genfstab -p -U / > /etc/fstab

```

Atualize o [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)"). `grub-mkconfig` deve detectar o novo UUID da partição automaticamente, mas entradas do menu customizadas precisam ser atualizadas manualmente.

```
# grub-mkconfig -o /boot/grub/grub.cfg
# grub-install /dev/sdx # instale para a unidade de armazenamento removível, não a unidade de armazenamento interna.

```

Reinicie e teste a nova configuração. Se lembre de definir a entrada do dispositivo de boot de acordo com sua BIOS ou [UEFI](/index.php/UEFI "UEFI"). Se o sistema falhar na inicialização, você deve ainda conseguir inicializar pelo disco rígido e então corrigir o problema.

### chkboot

**Atenção:** chkboot faz a partição `/boot` **tamper-evident** (adulterações evidentes), não **tamper-proof** (a prova de adulteração). Quando o script chkboot é executado, você já digitou a sua senha em um potencialmente compromissado gerenciador de boot, kernel ou initrd. Se seu sistema falhar o teste de integridade chkboot, nenhuma assunção pode ser feita sobre a segurança dos seus dados.

Fazendo referência ao artigo (em inglês) da ct-magazine (em inglês, issue 3/12, página 146, 01.16.2012, [[2]](http://www.heise.de/ct/inhalt/2012/03/6/)) o seguinte script checa por mudanças do SHA-1 hash, inode, e blocos ocupados no disco dos arquivos no `/boot`. Também checa o [Master Boot Record](/index.php/Particionamento#Master_Boot_Record "Particionamento"). O script não pode prevenir certos tipos de ataques, mas o fazem mais difíceis. Nenhuma configuração do script é guardada no `/boot` não criptografado. Com o sistema criptografado fechado/desligado, não é aparente que uma comparação automática da soma de verificação da partição é feita na inicialização, dificultando para os atacantes. No entanto, um atacante que antecipar estas precauções pode manipular o firmware para rodar seu próprio código em cima do kernel e interceptar acessos ao sistema de arquivos, exemplo para `/boot`, e apresentar os arquivos intocados. Geralmente, nenhuma medida de segurança abaixo do nível do firmware pode garantir confiança e evidência de adulteração.

O script com instruções de instalação está disponível [aqui](ftp://ftp.heise.de/pub/ct/listings/1203-146.zip) (Autor: Juergen Schmidt, ju na heisec.de; Licença: GPLv2). Existe também o pacote [chkboot](https://aur.archlinux.org/packages/chkboot/) para [instalar](/index.php/Instala "Instala").

Depois da instalação, adicione um arquivo de serviço (o pacote inclui um baseado no seguinte) e [habilite](/index.php/Habilite "Habilite")-o:

```
[Unit]
Description=Check that boot is what we want
Requires=basic.target
After=basic.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/chkboot.sh

[Install]
WantedBy=multi-user.target

```

Existe uma pequena ressalva para o systemd. No tempo de escrita, o script original provido, `chkboot.sh`, contém um espaço em branco no começo do `#!/bin/bash` que deve ser removido para o serviço começar com sucesso.

`/usr/local/bin/chkboot_user.sh` precisa ser executado depois do login, adicione-o para a [inicialização automática](/index.php/Inicializa%C3%A7%C3%A3o_autom%C3%A1tica "Inicialização automática") (exemplo, em inglês, no KDE -> *System Settings -> Startup and Shutdown -> Autostart*; GNOME 3: *gnome-session-properties*).

Com o Arch Linux, mudanças no `/boot` são frequentes, por exemplo atualizações do kernel. Assim, pode ser útil usar scripts com cada atualização total do sistema. Uma forma de fazer isso é:

```
#!/bin/bash
#
# Nota: Insira seu <usuário> e execute isto com sudo para pacman e chkboot para funcionar automagicamente
#
echo "Atualização [1] Checagem rápida antes dela" & 
sudo -u <usuário> /usr/local/bin/chkboot_user.sh		# insira seu <usuário> logado
/usr/local/bin/chkboot.sh
sudo -u <usuário> /usr/local/bin/chkboot_user.sh		# insira seu <usuário> logado
echo "Atualização [2] Sincronizando repositórios com o pacman" 
pacman -Syu
/usr/local/bin/chkboot.sh
sudo -u <usuário> /usr/local/bin/chkboot_user.sh		# insira seu <usuário> logado
echo "Atualização [3] Tudo feito, vamos continuar..."

```

### mkinitcpio-chkcryptoboot

**Atenção:** Este hook **não** criptografa o código núcleo do [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") ou EFI stub, nem protege contra situações onde um atacante pode modificar o comportamento do gerenciador de boot para comprometer o kernel e/ou initramfs durante a execução.

[mkinitcpio-chkcryptoboot](https://aur.archlinux.org/packages/mkinitcpio-chkcryptoboot/) é um hook do [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") que verifica a integridade durante o *** performs integrity checks during early-userspace e recomenda ao usuário não entrar com a senha da partição raiz criptografada se o sistema ter sido aparentemente comprometido. Segurança é conquistada atravês de uma [partição de boot criptografada](/index.php/Dm-crypt/Criptografando_todo_um_sistema#Partição_de_boot_criptografada_(GRUB) "Dm-crypt/Criptografando todo um sistema"), que é aberta usando o módulo `cryptodisk.mod` do [GRUB](/index.php/GRUB_(Portugu%C3%AAs)#/boot_criptografado "GRUB (Português)"), e a partição raiz criptografada tem uma senha diferente da anterior. Desta maneira, o [initramfs](/index.php/Initramfs "Initramfs") e o [kernel](/index.php/Kernel_(Portugu%C3%AAs) "Kernel (Português)") são protegidos contra adulterações offline, e a partição raiz pode permanecer segura até mesmo se a senha da partição `/boot` seja entrada em uma máquina comprometida (desde que o hook chkcryptoboot detecte modificações, e não seja comprometido durante a execução).

Este hook precisa do [grub](https://www.archlinux.org/packages/?name=grub) versão >= 2.00 para funcionar, e uma partição `/boot` criptografada com LUKS, com sua própria senha para ser segura.

#### Instalação

[Instale](/index.php/Instale "Instale") o [mkinitcpio-chkcryptoboot](https://aur.archlinux.org/packages/mkinitcpio-chkcryptoboot/) e edite `/etc/default/chkcryptoboot.conf`. Se você quer detectar se sua partição de boot foi modificada, edite as variáveis `CMDLINE_NAME` e `CMDLINE_VALUE`, com valores conhecidos somente por você. Você pode seguir o conselho de usar duas hash como é sugerido depois da instalação. Também, faça as mudanças apropriadas aos [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") em `/etc/default/grub`. Edite a linha `HOOKS=` em `/etc/mkinitcpio.conf`, e insira o hook `chkcryptoboot` **antes do** hook `encrypt`. Quando acabar, [gere novamente o initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

#### Visão geral técnica

[mkinitcpio-chkcryptoboot](https://aur.archlinux.org/packages/mkinitcpio-chkcryptoboot/) consiste de um install e run-time hook para o mkinitcpio. O install hook é executado toda vez que o initramfs é gerado, e faz hash do [EFI](/index.php/EFI "EFI") stub do GRUB (`$esp/EFI/grub_uefi/grubx64.efi`) (para sistemas [UEFI](/index.php/UEFI "UEFI")) ou os primeiros 446 bytes do disco que o grub está instalado (para sistemas BIOS), e guarda esta hash dentro do initramfs localizado na partição `/boot` criptografada. Quando o sistema é inicializado, GRUB pede a senha para a partição `/boot`, e então o run-time hook executa a mesma operação de hash e compara o hash resultante antes de solicitar a senha para a partição raiz. Se eles não forem iguais, vai ser mostrado um erro como esse:

```
CHKCRYPTOBOOT ALERT!
CHANGES HAVE BEEN DETECTED IN YOUR BOOT LOADER EFISTUB!
YOU ARE STRONGLY ADVISED NOT TO ENTER YOUR ROOT CONTAINER PASSWORD!
Please type uppercase yes to continue:

```

Em adição a fazer hash do gerenciador de boot, o hook também verifica os parâmetros do kernel em execução com os configurados em `/etc/default/chkcryptoboot.conf`. Esta verificação é feita durante e depois do processo de inicialização. Isto permite detectar se a configuração do GRUB foi adulterada durante a execução e depois para verificar se toda a partição `/boot` foi modificada.

Para sistemas BIOS, o hook cria um hash do primeiro estágio do gerenciador de boot GRUB (instalado nos primeiros 446 bytes do dispositivo de inicialização) para comparar depois no processo de inicialização. O principal segundo estágio `core.img` não é verificado.

### AIDE

Uma alternativa aos scripts acima, é a checagem de hash feita com [AIDE](/index.php/AIDE "AIDE") que tem um arquivo de configuração muito flexível.

### STARK

Enquanto um destes métodos devem servir para a maioria do usuários, eles não resolvem todos os problemas de segurança associados com o `/boot` não criptografado. Uma abordagem que se esforça para prover uma cadeia de inicialização totalmente autentificada foi publicada como POTTS, uma tese acadêmica de implementação do framework de autentificação [STARK](https://www1.informatik.uni-erlangen.de/stark).

O proof-of-concept (prova de conceito) POTTS usa Arch Linux como distribuição base e implementa um sistema de inicialização em cadeia com:

*   POTTS - um menu de inicialização com caixa de diálogo para autentificação única por meio de mensagem.
*   TrustedGrub - uma implementação do [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") que verifica o kernel e initramfs por meio de registradores PCR do [chip TPM](/index.php/Trusted_Platform_Module "Trusted Platform Module").
*   TRESOR - um patch do kernel que implementa AES, mas mantém a chave mestre nos registradores da CPU ao invês da RAM enquanto está em execução.

Como parte da tese, as instruções de [instalação](https://13.tc/p/potts/manual.html) baseadas no Arch Linux (ISO de 2013-01) foi publicada. Se você quiser tentar, tenha em mente que estas ferramentas não estão nos repositórios padrão e a solução vai consumir tempo para manter.

## Usando keyfiles criptografadas com GPG, LUKS ou OpenSSL

Os seguintes posts (em inglês) do fórum dão instruções para usar autentificação de dois fatores, keyfiles criptografadas com gpg ou openssl, ao invês de uma keyfile de texto puro descrita antes em [Criptografia de sistema usando LUKS com chaves criptografadas com GPG](https://bbs.archlinux.org/viewtopic.php?id=120243):

*   GnuPG: [Post sobre chaves criptografadas com GPG](https://bbs.archlinux.org/viewtopic.php?pid=943338#p943338). Possui instruções genéricas.
*   OpenSSL: [Post sobre chaves criptografadas com OpenSSL](https://bbs.archlinux.org/viewtopic.php?pid=947805#p947805). Tem somente os hooks `ssldec`.
*   OpenSSL: [Post sobre chaves criptografadas com OpenSSL (embaralhadas com bf-cbc)](https://bbs.archlinux.org/viewtopic.php?id=155393). Este post tem o hooks do initcpio install, `bfkf`, e script gerador de keyfile criptografada.
*   LUKS: [Post sobre chaves criptografadas com LUKS](https://bbs.archlinux.org/viewtopic.php?pid=1502651#p1502651) com um hook do initcpio `lukskey`. Ou [#/boot criptografado e um cabeçalho LUKS desanexado em um pendrive](#Encrypted_/boot_and_a_detached_LUKS_header_on_USB) abaixo com um hook encrypt customizado para o initcpio.

Note que:

*   Você pode seguir as instruções acima com somente duas partições, uma de boot (necessário devido a criptografia) e uma LVM. Dentro da partição com LVM, você pode ter quantos volumes lógicos quiser/precisar, exemplo, volumes lógicos para a raiz, swap e home. Com isto basta ter somente uma keyfile para abrir os volumes lógicos da LVM criptografada. Se você decidir fazer isso, dentre os hooks presentes no `/etc/mkinitcpio.conf` deve ter: `HOOKS=( ... usb usbinput (etwo ou ssldec) encrypt (se está usando openssl) lvm2 resume ... )` e você deve adicionar `resume=/dev/<GrupoDeVolumes>/<VolumeLogicoDaSwap>` para os do [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel").
*   Se você precisa temporariamente guardar a keyfile não criptografada em algum lugar, não a guarde em um disco não criptografado. É mais recomendado guardá-la na RAM, em `/dev/shm`.
*   Se você quer usar uma keyfile criptografada com GPG, vai precisar usar uma versão 1.4 do GnuPG compilada estaticamente ou editar os hooks e usar este pacote do AUR [gnupg1](https://aur.archlinux.org/packages/gnupg1/)
*   É possível que uma atualização do OpenSSL quebre o `ssldec` customizado mencionado no segundo post do forum.

## Abrir remotamente a partição raiz (ou outra)

Se você deseja ser capaz de reiniciar um sistema criptografado com LUKS remotamente, ou iniciá-lo com um serviço [Wake-on-LAN](/index.php/Wake-on-LAN "Wake-on-LAN"), você vai precisar de uma maneira de entrar a senha para a partição/container raiz na inicialização. Isto é alcançavél ao executar um hook do [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") que configura uma interface de rede. Alguns pacotes listados abaixo contribuem com vários ["mkinitcpio build hooks"](/index.php/Mkinitcpio#Build_hooks "Mkinitcpio") para facilitar a configuração.

**Nota:**

*   Usar nomes de dispositivos do kernel para interface de rede (exemplo, `eth0`) ao invês dos do [udev](/index.php/Udev "Udev") (exemplo, `enp1s0`), não vai funcionar.
*   Por padrão, nomes de interfaces de rede previsíveis são ativados e *mudam* nomes de dispositivos do kernel mais tarde durante a inicialização. Use dmesg e olhe o que seu módulo de rede do kernel faz para achar o nome original (exemplo, `eth0`)
*   Pode ser necessário adicionar o módulo para sua placa de rede [a cabo](/index.php/Network_configuration_(Portugu%C3%AAs)/Ethernet_(Portugu%C3%AAs)#Driver_de_dispositivo "Network configuration (Português)/Ethernet (Português)") ou [sem fio](/index.php/Network_configuration_(Portugu%C3%AAs)/Wireless_(Portugu%C3%AAs)#Driver_de_dispositivo "Network configuration (Português)/Wireless (Português)") para o arranjo [MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio").

### Abrir remotamente (hooks: systemd, systemd-tool)

O pacote do AUR [mkinitcpio-systemd-tool](https://aur.archlinux.org/packages/mkinitcpio-systemd-tool/) oferece um hook do mkinitcpio voltado no [systemd](https://www.archlinux.org/packages/?name=systemd) com o nome de *systemd-tool* que possui as seguintes funcionalidades para o initramfs do systemd:

| 

Funcionalidades principais incluídas no hook:

*   configuração unificada do systemd + mkinitcpio
*   automática provisão de binário e recursos de configuração
*   invocação em demanda de scripts e funções do mkinitcpio

 | 

Funcionalidades oferecidas pela unidades de serviço incluídas:

*   debug do initrd
*   configuração inicial de rede antecipada
*   shell interativo
*   acesso remoto ssh no initrd
*   cryptsetup + agente de senha personalizado

 |

O pacote [mkinitcpio-systemd-tool](https://aur.archlinux.org/packages/mkinitcpio-systemd-tool/) precisa do [hook do systemd](/index.php/Mkinitcpio#Common_hooks "Mkinitcpio"). Para mais informações leia o [README](https://github.com/random-archer/mkinitcpio-systemd-tool/blob/master/README.md) do projeto e também [arquivos unit de serviços do systemd](https://github.com/random-archer/mkinitcpio-systemd-tool) como uma introdução.

Os hooks recomendados são: `base autodetect modconf block filesystems keyboard fsck systemd systemd-tool`.

### Abrir remotamente (hooks: netconf, dropbear, tinyssh, ppp)

Outra combinação de pacotes que oferece login remoto para o initcpio é [mkinitcpio-netconf](https://www.archlinux.org/packages/?name=mkinitcpio-netconf) e/ou [mkinitcpio-ppp](https://aur.archlinux.org/packages/mkinitcpio-ppp/) (para abrir remotamente usando uma coneção [PPP](https://en.wikipedia.org/wiki/Point-to-Point_Protocol "wikipedia:Point-to-Point Protocol")) junto com um servidor [SSH](/index.php/Secure_Shell_(Portugu%C3%AAs) "Secure Shell (Português)"). Você tem a opção de usar o [mkinitcpio-dropbear](https://www.archlinux.org/packages/?name=mkinitcpio-dropbear) ou [mkinitcpio-tinyssh](https://www.archlinux.org/packages/?name=mkinitcpio-tinyssh). Estes hooks não instalam qualquer shell, então você pode precisar [instalar](/index.php/Instala "Instala") o pacote [mkinitcpio-utils](https://www.archlinux.org/packages/?name=mkinitcpio-utils). As instruções abaixo podem ser usadas em qualquer combinação dos pacotes acima. Será perceptível quando ações forem específicas para dada combinação de pacotes.

1.  Se você não tem um par de chaves do SSH ainda, [o gere](/index.php/SSH_keys#Generating_an_SSH_key_pair "SSH keys") no sistema cliente (o que vai ser usado para abrir remotamente a máquina).
    **Nota:** `tinyssh` somente suporta [Ed25519](/index.php/SSH_keys#Ed25519 "SSH keys") e tipos de chave [ECDSA](/index.php/SSH_keys#ECDSA "SSH keys"). Se você prefere usar [mkinitcpio-tinyssh](https://www.archlinux.org/packages/?name=mkinitcpio-tinyssh), você precisa criar/usar um destes.

    **Nota:** `mkinitcpio-dropbear` na versão 0.0.3-5 não é compativel com a atual implementação do dropbear que removeu dss. Veja a [issue 8](https://github.com/grazzolini/mkinitcpio-dropbear/issues/8) para detalhes e como corrigir.

2.  Insira sua chave pública do SSH (exemplo, a que você normalmente coloca nas máquinas acessadas sem uma senha, ou a que você criou e termina com *.pub*) no `/etc/dropbear/root_key` ou `/etc/tinyssh/root_key` da máquina remota.
    **Dica:** Este método pode ser usado mais tarde para adicionar outras chaves públicas se necessário; Caso copie o conteúdo do arquivo `~/.ssh/authorized_keys` da máquina remota, verifique se somente tem chaves que você planeja usar para abrir a máquina remotamente. Quando adicionar chaves, gere seu initrd também usando o `mkinitcpio`. Veja também [OpenSSH#Protection](/index.php/OpenSSH#Protection "OpenSSH").

3.  Adicione todos os três [hooks](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") `<netconf e/ou ppp> <dropbear ou tinyssh> encryptssh` antes de `filesystems` dentro do arranjo "HOOKS" no `/etc/mkinitcpio.conf` (o hook `encryptssh` substitue `encrypt`). Então [gere novamente o initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").
    **Nota:** O hook `net` provido pelo [mkinitcpio-nfs-utils](https://www.archlinux.org/packages/?name=mkinitcpio-nfs-utils) **não** é necessário.

    **Nota:** Se você receber o erro `libgcc_s.so.1 must be installed for pthread_cancel to work` quando tentar descriptografar, você precisa adicionar `/usr/lib/libgcc_s.so.1` para o arranjo "[BINARIES](/index.php/Mkinitcpio#BINARIES_and_FILES "Mkinitcpio")".

4.  Configure o [parâmetro](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Gerenciador_de_boot "Dm-crypt/Configuração do sistema") `cryptdevice=` e adicione o [o parâmetro do kernel](/index.php/Kernel_parameters "Kernel parameters") `ip=` para a configuração do seu gerenciador de boot com os argumentos apropriados. Por exemplo, se o servidor DHCP não atribuir um IP estático para seu sistema remoto, dificultando o acesso com SSH entre inicializações, você pode explicitamente declarar o endereço IP que você quer, usando: `ip=192.168.1.1:::::eth0:none` Alternativamente, você pode especificar também a máscara de subrede e gateway necessário para a rede: `ip=192.168.1.1::192.168.1.254:255.255.255.0::eth0:none` 
    **Nota:** Na versão 0.0.4 do [mkinitcpio-netconf](https://www.archlinux.org/packages/?name=mkinitcpio-netconf), você pode usar múltiplos `ip=` para configurar várias interfaces. você não pode misturar isto com `ip=dhcp` (`ip=:::::eth0:dhcp`) sozinho. Uma interface precisa ser especificada.
     `ip=ip=192.168.1.1:::::eth0:none:ip=172.16.1.1:::::eth1:none` Para uma descrição detalhada veja [essa seção do mkinitcpio](/index.php/Mkinitcpio#Using_net "Mkinitcpio"). Quando terminar, atualize a configuração do seu [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot").
5.  Finalmente, reinicie o sistema remoto e tente [usar o ssh](/index.php/OpenSSH#Client_usage "OpenSSH"), **explicitamente usando o nome de usuário "root"** (até mesmo se o superusuário root está desabilitado na máquina, este usuário root é usado somente no initrd para abrir o sistema remotamente). Se você está usando o pacote [mkinitcpio-dropbear](https://www.archlinux.org/packages/?name=mkinitcpio-dropbear) e também tem o pacote [openssh](https://www.archlinux.org/packages/?name=openssh) instalado, então provavelmente não vai receber nenhum aviso antes de logar, porquê o anterior converte e usa as mesmas chaves do ssh (exceto chaves Ed25519, já que o dropbear não suporta elas). Caso você está usando [mkinitcpio-tinyssh](https://www.archlinux.org/packages/?name=mkinitcpio-tinyssh), existe a opção de instalar [tinyssh-convert](https://www.archlinux.org/packages/?name=tinyssh-convert) ou [tinyssh-convert-git](https://aur.archlinux.org/packages/tinyssh-convert-git/) para que você possa usar as mesmas chaves da sua instalação do [openssh](https://www.archlinux.org/packages/?name=openssh) (atualmente, somente chaves Ed25519). De qualquer forma, você precisa rodar o [daemon do ssh](/index.php/OpenSSH#Daemon_management "OpenSSH") ao menos uma vez, usando as units providas do systemd, então as chaves podem ser geradas primeiro. Depois de reiniciar a máquina, deve ser solicitado a senha para abrir o dispositivo raiz. O sistema vai completar o processo de inicialização e você pode executar o ssh [normalmente](/index.php/OpenSSH#Client_usage "OpenSSH") (com o usuário remoto de sua escolha).

**Dica:** Se você deseja uma boa solução para montar outras partições criptografadas (tais como `/home`) remotamente, você pode quer ler [esta thread do forum](https://bbs.archlinux.org/viewtopic.php?pid=880484).

### Abrir remotamente pelo wifi

O hook net é normalmente usado com uma conexão com fio. Caso você queira configurar um computador sem fio, e abrí-lo por wifi, você pode usar um hook predefinido ou criar um hook customizado para se conectar a rede wifi antes que o hook net seja executado.

#### Hook predefinido

Você pode instalar um hook predefinido baseado no presente nesta wiki:

1.  Instale [mkinitcpio-wifi](https://aur.archlinux.org/packages/mkinitcpio-wifi/).
2.  Configure sua coneção wifi ao criar uma configuração do wpa_supplicant com as propriedades da sua rede: `wpa_passphrase "ESSID" "senha" > /etc/wpa_supplicant/initcpio.conf` 
3.  Adicione o hook `wifi` antes de `netconf` no seu `/etc/mkinitcpio.conf`. Seus módulos relacionados com wifi devem ser detectados automaticamente, se não: adicione eles em `MODULES`.
4.  Adicione `ip=:::::wlan0:dhcp` nos [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel").
5.  [Gere novamente o initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").
6.  Atualize a configuração do seu [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot").

#### Faça o seu próprio

Abaixo um exemplo mostrando uma configuração usando um adaptador usb, se conectando a uma rede wifi com WPA2-PSK. Caso você use, por exemplo, WEP ou outro gerenciador de boot, você pode precisar mudar algumas coisas.

1.  Modifique o `/etc/mkinitcpio.conf`:
    *   Adicione os módulos do kernel necessários para seu adaptador wifi.
    *   Inclua os binários do `wpa_passphrase` e `wpa_supplicant`.
    *   Adicione o hook `wifi` (ou um nome de sua escolha, este será o hook customizado que será criado) antes do hook `net`.
        ```
        MODULES=(*module*)
        BINARIES=(wpa_passphrase wpa_supplicant)
        HOOKS=(base udev autodetect ... **wifi** net ... dropbear encryptssh ...)
        ```

2.  Crie o hook `wifi` no `/etc/initcpio/hooks/wifi`:
    ```
    run_hook ()
    {
    	# espere alguns segundos para que wlan0 seja configurada pelo kernel
    	sleep 5

    	# set wlan0 to up
    	ip link set wlan0 up

    	# associe com a rede wifi
    	# 1\. salve o arquivo de configuração temporário
    	wpa_passphrase "*ESSID da rede*" "*senha*" > /tmp/wifi

    	# 2\. associe
    	wpa_supplicant -B -D nl80211,wext -i wlan0 -c /tmp/wifi

    	# espere alguns segundos para que wpa_supplicant termine de se conectar
    	sleep 5

    	# wlan0 deve agora estar conectada e pronta para receber um ip pelo hook net
    }

    run_cleanuphook ()
    {
    	# mate wpa_supplicant rodando em segundo plano
    	killall wpa_supplicant

    	# coloque a interface wlan0 como down
    	ip link set wlan0 down

    	# wlan0 deve agora esta totalmente desconectada da rede wifi
    }
    ```

3.  Crie o arquivo do hook de instalação no `/etc/initcpio/install/wifi`:
    ```
    build ()
    {
    	add_runscript
    }
    help ()
    {
    cat<<HELPEOF
    	Habilita o wifi na inicialização, para abrir o disco com dropbear (ssh).
    HELPEOF
    }
    ```

4.  Adicione `ip=:::::wlan0:dhcp` para os [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel"). Remova `ip=:::::eth0:dhcp` para evitar conflitos.
5.  Opcionalmente crie uma entrada de boot adicional com o parâmetro do kernel `ip=:::::eth0:dhcp`.
6.  [Gere novamente o initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").
7.  Atualize a configuração do seu [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot").

Uma vez que o sistema estiver totalmente inicializado, se lembre de configurar o [wifi](/index.php/Network_configuration_(Portugu%C3%AAs)/Wireless_(Portugu%C3%AAs) "Network configuration (Português)/Wireless (Português)"), para então você fazer login. Caso você não consiga se conectar a rede wifi, tente aumentar um pouco o tempo de espera.

## Suporte a discard/TRIM para unidades de estado sólido (SSD)

Usuários de [SSDs](/index.php/Solid_state_drive "Solid state drive") devem saber que, por padrão, comandos de TRIM não são habilitados pelo mapeador de dispositivos, dispositivos de bloco são montados sem a opção `discard` a menos que você sobrescreva o padrão.

Os mantenedores do mapeador de dispositivos deixaram claro que suporte a TRIM nunca será habilitado por padrão em dispositivos do dm-crypt devido a potenciais implicações de segurança.[[3]](http://www.saout.de/pipermail/dm-crypt/2011-September/002019.html)[[4]](http://www.saout.de/pipermail/dm-crypt/2012-April/002420.html) Um vazamento mínimo de dados em forma de informações de blocos liberadas, talvez o suficiente para determinar o sistema de arquivos em uso, pode ocorrer se o suporte a TRIM estiver habilitado. Ilustrações e discursão dos problemas resultantes estão disponíveis no [blog](http://asalor.blogspot.de/2011/08/trim-dm-crypt-problems.html) de um dos desenvolvedores do *cryptsetup*. Se você está preocupado com isso, tenha em mente que as ameaças podem crescer: por exemplo, se o dispositivo está ainda criptografado com a antiga cifra padrão (cryptsetup <=1.6.0) `--cipher aes-cbc-essiv`, mais informação pode ser vazada do setor que sofreu TRIM do que com o [padrão](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Opções_de_encriptação_para_o_modo_LUKS "Dm-crypt/Encriptação de dispositivo") atual.

Os seguintes casos podem ser distinguidos:

*   O dispositivo é criptografado com as opções padrão do modo LUKS do dm-crypt:
    *   Por padrão o cabeçalho do LUKS é guardado no início do dispositivo e usar TRIM é útil para proteger as modificações do cabeçalho. Se por exemplo uma senha comprometida do LUKS é revocada, sem TRIM o velho cabeçalho vai, geralmente, ainda estar disponível para leitura até que seja sobrescrevida por outra operação; se a unidade de armazenamento é roubada nesse periodo, os atacantes podem em teoria achar uma maneira de localizar o velho cabeçalho e usá-lo para descriptografar o dispositivo com a senha compromissada. Veja [FAQ do cryptsetup, seção 5.19 "What about SSDs, Flash and Hybrid Drives?"](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects) e [Encriptação total de disco em um ssd](https://www.reddit.com/r/archlinux/comments/2f370s/full_disk_encryption_on_an_ssd/ck5p5c5).
    *   TRIM pode continuar desabilitado se as preocupações de segurança mostradas no começo desta seção são consideradas uma ameaça pior que a acima.

	Veja também [Securely wipe disk#Flash memory](/index.php/Securely_wipe_disk#Flash_memory "Securely wipe disk").

*   O dispositivo é criptografado com o modo plain do dm-crypt, ou o cabeçalho do LUKS é guardado [separadamente](#Sistema_criptografado_usando_um_cabeçalho_LUKS_desanexado):
    *   Se negação plausível é desejada, TRIM **nunca** deve ser usado devido a considerações no começo dessa seção, ou o uso de encriptação vai ser revelado.
    *   Se negação plausível não é desejada, TRIM pode ser usado para ganhos de perfomance, já que problemas de segurança descritos no começo dessa seção não são uma preocupação.

**Atenção:** Antes de habilitar o TRIM na unidade de armazenamento, tenha certeza de que o dispositivo suporta totalmente comandos de TRIM, ou perda de dados podem ocorrer. Veja [Solid State Drives#TRIM](/index.php/Solid_State_Drives#TRIM "Solid State Drives").

No [linux](https://www.archlinux.org/packages/?name=linux) 3.1 e superior, habilitar o TRIM no dm-crypt pode ser alcançado na montagem com `dmsetup` ou na criação do dispositivo. Suporte para esta opção também existe no [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) versão >= 1.4.0\. Para adicionar suporte durante a inicialização, você precisa adicionar `:allow-discards` para a opção `cryptdevice`. A opção de TRIM pode parecer assim:

```
cryptdevice=/dev/sdaX:raiz:allow-discards

```

Para as configurações principais do `cryptdevice` antes de `allow-discards` veja [Dm-crypt/Configuração do sistema](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema "Dm-crypt/Configuração do sistema").

Se você usa um initrd baseado no systemd, você deve colocar:

```
rd.luks.options=discard

```

**Nota:** `rd.luks.options=discard` não tem efeito nos dispositivos incluidos no arquivo `/etc/crypttab` da imagem do initramfs (`/etc/crypttab.initramfs` na raiz do sistema). Você deve especificar a opção `discard` no `/etc/crypttab.initramfs`.

Além disso, também é necessário periodicamente rodar `fstrim` ou montar o sistema de arquivos (exemplo, `/dev/mapper/raiz` neste exemplo) com a opção `discard` no `/etc/fstab`. Para detalhes, veja a página do [TRIM](/index.php/TRIM "TRIM").

Para dispositivos LUKS abertos com `/etc/crypttab`, use a opção `discard`, exemplo:

 `/etc/crypttab`  `luks-123abcdef-etc UUID=123abcdef-etc none discard` 

Quando abrir manualmente os dispositivos no terminal use `--allow-discards`.

Com LUKS2 você pode definir `allow-discards` como uma flag padrão para um dispositivo ao abrí-lo uma vez com a opção `--persistent`:

```
# cryptsetup --allow-discards --persistent open /dev/sdaX root

```

Quando o dispositivo já estiver aberto, a ação `open` vai dar erro. Nestes casos você pode usar a opção `refresh`, exemplo:

```
# cryptsetup --allow-discards --persistent refresh /dev/sdaX

```

Você pode ter certeza que a flag está definida como persistente no cabeçalho do LUKS2 ao olhar a saída do `cryptsetup luksDump`:

 `# cryptsetup luksDump /dev/sdaX | grep Flags` 
```
Flags:          allow-discards

```

Em qualquer caso você pode ver se o dispositivo foi aberto com a flag ao inspecionar a saída do `dmsetup table`:

 `# dmsetup table` 
```
luks-123abcdef-etc: 0 1234567 crypt aes-xts-plain64 000etc000 0 8:2 4096 1 allow_discards

```

## O hook encrypt e múltiplos discos

**Dica:** o hook `sd-encrypt` suporta abrir múltiplos dispositivos. Eles podem ser especificados nos parâmetros do kernel ou no `/etc/crypttab.initramfs`. Veja [dm-crypt/Configuração do sistema#Usando o hook sd-encrypt](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Usando_o_hook_sd-encrypt "Dm-crypt/Configuração do sistema").

O hook `encrypt` somente permite uma **única** entrada `cryptdevice=` ([FS#23182](https://bugs.archlinux.org/task/23182)). Em um sistema com múltiplas unidades de armazenamentos isto pode ser limitante, devido ao *dm-crypt* não ter funcionalidade para usar algo além de dispositivos físicos. Por exemplo, use "LVM dentro do LUKS": Toda a LVM existe dentro de um dispositivo LUKS. Não há problema para sistema com uma unidade de armazenamento, desde que tem somente uma para criptografar. Mas o que acontece se você quer aumentar o tamanho da LVM? Você não pode, não sem modificar o hook `encrypt`.

As seções seguintes brevemente mostram alternativas para superar esta limitação. A primeira, demostra como expandir uma configuração [LUKS dentro do LVM](/index.php/Dm-crypt/Criptografando_todo_um_sistema#LUKS_dentro_do_LVM "Dm-crypt/Criptografando todo um sistema") para um novo disco. A segunda, em como modificar o hook `encrypt` para abrir múltiplos disco criptografados com LUKS sem LVM.

### Expandindo LVM em múltiplos discos

O gerenciamento de múltiplos discos é uma funcionalidade básica do [LVM](/index.php/LVM_(Portugu%C3%AAs) "LVM (Português)") e uma da razões por seu particionamento flexível. Pode ser usado com *dm-crypt*, mas somente se LVM é empregado como primeiro mapeador. Em uma configuração [LUKS dentro do LVM](/index.php/Dm-crypt/Criptografando_todo_um_sistema#LUKS_dentro_do_LVM "Dm-crypt/Criptografando todo um sistema"), os dispositivos criptografados são criados dentro de volumes lógicos (com uma senha/chave separada por volume). A seguir é mostrado como expandir para outro disco.

**Atenção:** Faça backup! Enquanto redimensionar sistema de arquivos pode ser o padrão, tenha em mente que operções **podem** dar errado e não serem aplicáveis para uma configuração específica. Geralmente, extender um sistema de arquivos para usar o espaço livre é menos problemático que reduzí-lo. Isto é particularmente verdade quando mapeadores são empilhados, o caso do seguinte exemplo.

#### Adicionando uma nova unidade de armazenamento

Primeiro, pode ser desejado preparar um novo disco de acordo com [dm-crypt/Preparando a unidade de armazenamento](/index.php/Dm-crypt/Preparando_a_unidade_de_armazenamento "Dm-crypt/Preparando a unidade de armazenamento"). Segundo, é particionado como um LVM, exemplo, todo o espaço é alocado para `/dev/sdY1` com o tipo de partição `8E00` (Linux LVM). Terceiro, o novo disco/partição é ligado a um grupo de volumes do LVM existente, exemplo:

```
# pvcreate /dev/sdY1
# vgextend MeuArmazenamento /dev/sdY1

```

#### Extendendo o volume lógico

Para o próximo passo, a alocação final do novo espaço do disco, o volume lógico que será extendido tem que estar desmontado. Isto pode ser feito pela partição raiz do `cryptdevice`, mas neste caso o procedimento vai ser feito com a ISO de instalação do Arch.

Neste exemplo, é assumido que o volume lógico para `/home` (`homevol` é nome do volume lógico) vai ser expandido para o novo espaço em disco:

```
# umount /home
# fsck /dev/mapper/home
# cryptsetup luksClose /dev/mapper/home
# lvextend -l +100%FREE MeuArmazenamento/homevol

```

Agora o volume lógico é extendido e o container LUKS vem depois:

```
# cryptsetup open /dev/MeuArmazenamento/homevol home
# umount /home      # como uma garantia, caso foi automaticamente montado
# cryptsetup --verbose resize home

```

Finalmente, o sistema de arquivos vai ser redimensionado:

```
# e2fsck -f /dev/mapper/home
# resize2fs /dev/mapper/home

```

Pronto! Se foi de acordo com o plano, `/home` pode ser remontado e agora inclui a extensão para o novo disco:

```
# mount /dev/mapper/home /home

```

Note que a ação `cryptsetup resize` não afeta as chaves de encriptação, e estas não mudaram.

### Modificando o hook encrypt para múltiplas partições

#### sistema de arquivos principal expandido para múltiplas partições

É possível modificar o hook encrypt para permitir que múltiplas unidades de armazenamento abram a raiz `/` na inicialização. Uma maneira é:

```
# cp /usr/lib/initcpio/install/encrypt /etc/initcpio/install/encrypt2
# cp /usr/lib/initcpio/hooks/encrypt  /etc/initcpio/hooks/encrypt2
# sed -i "s/cryptdevice/cryptdevice2/" /etc/initcpio/hooks/encrypt2
# sed -i "s/cryptkey/cryptkey2/" /etc/initcpio/hooks/encrypt2

```

Adicione `cryptdevice2=` para suas opções de boot (e `cryptkey2=` se necessário), e adicione o hook `encrypt2` para seu [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") antes de gerar o initramfs. Veja [dm-crypt/Configuração do sistema](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema "Dm-crypt/Configuração do sistema").

#### Múltiplas partições não raiz

Talvez você precisa usar o hook `encrypt` em uma partição não raiz. Arch não suporta isto nativamente, no entanto, você pode facilmente mudar os valores cryptdev e cryptname em `/lib/initcpio/hooks/encrypt` (o primeiro para sua partição `/dev/sd*`, a segunda para o nome que você quer o atribuir). Isto deve bastar.

A grande vantagem é que você pode ter tudo automatizado, configurar o `/etc/crypttab` com uma keyfile externa (a keyfile não está numa partição do disco rígido interno) pode ser chato - você precisa ter certeza que o dispositivo USB/FireWire/... é montado antes da partição criptografada, isto significa que você tem de mudar a ordem do `/etc/fstab` (ao menos).

Se o pacote [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) for atualizado, você terá que mudar este script denovo. Diferente do `/etc/crypttab`, somente uma partição é suportada, mas com alguns hacks é possível abrir múltiplas partições.

Se você quer fazer isto em uma partição RAID de software, existe mais uma coisa que você precisa fazer. Somente definir o dispositivo `/dev/mdX` em `/lib/initcpio/hooks/encrypt` não é o bastante; o hook `encrypt` não vai encontrar a chave por algum motivo, e a senha não vai ser solicitada. Aparentemente, dispositivos RAID não são descobertos antes do hook `encrypt` rodar. Você pode resolver isto ao botar o arranjo RAID em `/boot/grub/menu.lst`, como:

```
kernel /boot/vmlinuz-linux md=1,/dev/hda5,/dev/hdb5

```

Se você usar sua partição raiz como RAID, você vai notar similaridades com esta configuração. [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") pode de forma simples manusear definições de múltiplos arranjos:

```
kernel /boot/vmlinuz-linux root=/dev/md0 ro md=0,/dev/sda1,/dev/sdb1 md=1,/dev/sda5,/dev/sdb5,/dev/sdc5

```

## Sistema criptografado usando um cabeçalho LUKS desanexado

Este exemplo segue a mesma configuração do [dm-crypt/Criptografando todo um sistema#dm-crypt plain](/index.php/Dm-crypt/Criptografando_todo_um_sistema#dm-crypt_plain "Dm-crypt/Criptografando todo um sistema"), que deve ser lida antes de seguir este guia.

Ao usar um cabeçalho desanezado, o dispositivo de bloco criptografado somente possui os dados criptografados, o que leva à [criptografia negável](https://en.wikipedia.org/wiki/Deniable_encryption "wikipedia:Deniable encryption") enquanto a existência do cabeçalho é desconhecida pelos atacantes. É similar ao [dm-crypt plain](/index.php/Dm-crypt/Criptografando_todo_um_sistema#dm-crypt_plain "Dm-crypt/Criptografando todo um sistema"), mas com as vantagens do LUKS como múltiplas senhas para a chave mestre e derivação de chave. Além de oferecer uma forma de autentificação de dois fatores com uma configuração mais simples que [#Using GPG, LUKS, or OpenSSL Encrypted Keyfiles](#Using_GPG,_LUKS,_or_OpenSSL_Encrypted_Keyfiles), enquanto nativamente tem solicitação de senha para múltiplas tentativas. Veja [Criptografia de disco#Metadados criptográficos](/index.php/Criptografia_de_disco#Metadados_criptográficos "Criptografia de disco") para mais informações.

Veja [dm-crypt/Encriptação de dispositivo#Opções de encriptação para o modo LUKS](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Opções_de_encriptação_para_o_modo_LUKS "Dm-crypt/Encriptação de dispositivo") para opções de encriptação antes de executar o primeiro passo e criar o arquivo de cabeçalho para usar com `cryptsetup`:

```
# dd if=/dev/zero of=cabecalho.img bs=16M count=1
# cryptsetup luksFormat /dev/sdX --offset 32768 --header cabecalho.img

```

**Dica:** A opção `--offset` permite especificar o início dos dados criptografados no dispositivo. Ao reservar um espaço no começo do dispositivo você pode [recolocar o cabeçalho do LUKS](/index.php/Dm-crypt/Encripta%C3%A7%C3%A3o_de_dispositivo#Restauração_usando_o_cryptsetup "Dm-crypt/Encriptação de dispositivo"). O valor é especificado em setores de 512-bytes, veja [cryptsetup(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cryptsetup.8) para mais detalhes.

Abra o container:

```
# cryptsetup open --header cabecalho.img /dev/sdX enc

```

Agora siga a [configuração LVM dentro do LUKS](/index.php/Dm-crypt/Criptografando_todo_um_sistema#Preparando_partições_que_não_são_de_boot "Dm-crypt/Criptografando todo um sistema") para suas necessidades. O mesmo se aplica para [preparando a partição de boot](/index.php/Dm-crypt/Criptografando_todo_um_sistema#Preparando_a_partição_de_boot_4 "Dm-crypt/Criptografando todo um sistema") no dispositivo removível (se não, não há lógica em ter um cabeçalho separado para abrir o disco criptografado). Mova o `cabecalho.img` para ele:

```
# mv cabecalho.img /mnt/boot

```

Siga o procedimento de instalação até o passo do mkinitcpio (você deve ter executado `arch-chroot` no sistema criptografado).

**Dica:** Você vai notar que a partição do sistema tem somente dados "randômicos", não tem tabela de partição e também não tem um `UUID` ou `LABEL`. Mas você pode ainda ter um mapeamento persistente usando o [Nomeação persistente de dispositivo de bloco#by-id e by-path](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco#by-id_e_by-path "Nomeação persistente de dispositivo de bloco"). Exemplo, usando o id do disco pelo `/dev/disk/by-id/`.

No initramfs, existem duas opções que suportam o cabeçalho do LUKS desanexado.

### Usando o hook do systemd

Primeiro crie `/etc/crypttab.initramfs` e adicione o dipositivo cripotgrafado nele. A sintaxe está definida em [crypttab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/crypttab.5)

 `/etc/crypttab.initramfs`  `enc	/dev/disk/by-id/*id_do_seu_disco*	none	header=/boot/cabecalho.img` 

Modifique `/etc/mkinitcpio.conf` [para usar o systemd](/index.php/Mkinitcpio#Common_hooks "Mkinitcpio") e adicione o cabeçalho em `FILES`.

 `/etc/mkinitcpio.conf` 
```
...
FILES=(**/boot/cabecalho.img**)
...
HOOKS=(base **systemd** autodetect **keyboard** **sd-vconsole** modconf block **sd-encrypt** **sd-lvm2** filesystems fsck)
...
```

[Gere novamente o initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") e pronto.

**Nota:** Nenhum parâmetro do cryptsetup precisa ser passado para a linha de comando do kernel, desde que `/etc/crypttab.initramfs` será adicionado como `/etc/crypttab` no initramfs. Se você deseja especificá-los na linha de comando do kernel veja [dm-crypt/Configuração do sistema#Usando o hook sd-encrypt](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#Usando_o_hook_sd-encrypt "Dm-crypt/Configuração do sistema") para opções suportadas.

### Modificando o hook encrypt

Este método mostra como modificar o hook `encrypt` para usá-lo com um cabeçalho do LUKS desanexado. Agora o hook `encrypt` precisa ser modificado para deixar o `cryptsetup` usar o cabeçalho separado ([FS#42851](https://bugs.archlinux.org/task/42851)); A fonte base e ideia para estas mudanças foi [publicada no BBS](https://bbs.archlinux.org/viewtopic.php?pid=1076346#p1076346)). Faça uma cópia para que esta configuração não seja sobrescrevida em uma atualização do [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"):

```
# cp /usr/lib/initcpio/hooks/encrypt /etc/initcpio/hooks/encrypt2
# cp /usr/lib/initcpio/install/encrypt /etc/initcpio/install/encrypt2

```
 `/etc/initcpio/hooks/encrypt2 (around line 52)` 
```
warn_deprecated() {
    echo "The syntax 'root=${root}' where '${root}' is an encrypted volume is deprecated"
    echo "Use 'cryptdevice=${root}:root root=/dev/mapper/root' instead."
}

**local headerFlag=false**
for cryptopt in ${cryptoptions//,/ }; do
    case ${cryptopt} in
        allow-discards)
            cryptargs="${cryptargs} --allow-discards"
            ;;  
        **header)
            cryptargs="${cryptargs} --header /boot/cabecalho.img"
            headerFlag=true
            ;;**
        *)  
            echo "Encryption option '${cryptopt}' not known, ignoring." >&2 
            ;;  
    esac
done

if resolved=$(resolve_device "${cryptdev}" ${rootdelay}); then
    if **$headerFlag ||** cryptsetup isLuks ${resolved} >/dev/null 2>&1; then
        [ ${DEPRECATED_CRYPT} -eq 1 ] && warn_deprecated
        dopassphrase=1
```

Agora edite o [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") para adicionar os hooks `encrypt2` e `lvm2`, o `cabecalho.img` para `FILES` e o `loop` para `MODULES`, fora outras configurações que o sistema precisa:

 `/etc/mkinitcpio.conf` 
```
...
MODULES=(**loop**)
...
FILES=(**/boot/cabecalho.img**)
...
HOOKS=(base udev autodetect **keyboard** **keymap** consolefont modconf block **encrypt2** **lvm2** filesystems fsck)
...
```

Isto é necessário para que o cabeçalho do LUKS esteja disponível na inicialização, nos excluindo uma configuração mais complicada para montar um pendrive separado para acessar o cabeçalho. Depois disso, gere a imagem [initramfs](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio").

Depois, configure o [gerenciador de boot](/index.php/Dm-crypt/Criptografando_todo_um_sistema#Configurando_o_gerenciador_de_boot_4 "Dm-crypt/Criptografando todo um sistema") para especificar o `cryptdevice=` também passando a nova opção `header` para esta configuração:

```
cryptdevice=/dev/disk/by-id/*id_do_seu_disco*:enc:header

```

Para finalizar, é útil seguir [dm-crypt/Criptografando todo um sistema#Pós-instalação](/index.php/Dm-crypt/Criptografando_todo_um_sistema#Pós-instalação "Dm-crypt/Criptografando todo um sistema") com uma partição `/boot` no dispositivo USB.

## Encrypted /boot and a detached LUKS header on USB

Rather than embedding the `header.img` and keyfile into the [initramfs](/index.php/Initramfs "Initramfs") image, this setup will make your system depend entirely on the usb key rather than just the image to boot, and on the encrypted keyfile inside of the encrypted boot partition. Since the header and keyfile are not included in the [initramfs](/index.php/Initramfs "Initramfs") image and the custom encrypt hook is specifically for the usb's [by-id](/index.php/Persistent_block_device_naming#by-id_and_by-path "Persistent block device naming"), you will literally need the usb key to boot.

For the usb drive, since you are encrypting the drive and the keyfile inside, it is preferred to cascade the ciphers as to not use the same one twice. Whether a [meet-in-the-middle](https://en.wikipedia.org/wiki/Meet-in-the-middle_attack "wikipedia:Meet-in-the-middle attack") attack would actually be feasible is debatable. You can do twofish-serpent or serpent-twofish.

### Preparing the disk devices

`sdb` will be assumed to be the USB drive, `sda` will be assumed to be the main hard drive.

Prepare the devices according to [dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

#### Preparing the USB key

Use [gdisk](/index.php/Gdisk "Gdisk") to partition the disk according to the layout [shown here](/index.php/Dm-crypt/Encrypting_an_entire_system#Preparing_the_disk_5 "Dm-crypt/Encrypting an entire system"), with the exception that it should only include the first two partitions. So as follows:

 `# gdisk /dev/sdb` 
```
Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048         1050623   512.0 MiB   EF00  EFI System
   2         1050624         1460223   200.0 MiB   8300  Linux filesystem

```

Before running `cryptsetup`, look at the [Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") and [Ciphers and modes of operation](/index.php/Disk_encryption#Ciphers_and_modes_of_operation "Disk encryption") first to select your desired settings.

[Prepare the boot partition](/index.php/Dm-crypt/Encrypting_an_entire_system#Preparing_the_boot_partition_5 "Dm-crypt/Encrypting an entire system") but do not `mount` any partition yet and [Format the EFI system partition](/index.php/EFI_system_partition#Format_the_partition "EFI system partition").

```
# mount /dev/mapper/cryptboot /mnt
# dd if=/dev/urandom of=/mnt/key.img bs=*filesize* count=1
# cryptsetup luksFormat /mnt/key.img
# cryptsetup open /mnt/key.img lukskey

```

*filesize* is in bytes but can be followed by a suffix such as `M`. Having too small of a file will get you a nasty `Requested offset is beyond real size of device /dev/loop0` error. As a rough reference, creating a 4M file will encrypt it successfully. You should make the file larger than the space needed since the encrypted loop device will be a little smaller than the file's size.

With a big file, you can use `--keyfile-offset=*offset*` and `--keyfile-size=*size*` to navigate to the correct position. [[7]](https://wiki.gentoo.org/wiki/Custom_Initramfs#Encrypted_keyfile)

Now you should have `lukskey` opened in a loop device (underneath `/dev/loop1`), mapped as `/dev/mapper/lukskey`.

#### The main drive

```
# truncate -s 16M /mnt/header.img
# cryptsetup --key-file=/dev/mapper/lukskey --keyfile-offset=*offset* --keyfile-size=*size* luksFormat /dev/sda --offset 32768 --header /mnt/header.img

```

Pick an *offset* and *size* in bytes (8192 bytes is the maximum keyfile size for `cryptsetup`).

```
# cryptsetup open --header /mnt/header.img --key-file=/dev/mapper/lukskey --keyfile-offset=*offset* --keyfile-size=*size* /dev/sda enc 
# cryptsetup close lukskey
# umount /mnt

```

Follow [Preparing the logical volumes](/index.php/Dm-crypt/Encrypting_an_entire_system#Preparing_the_logical_volumes "Dm-crypt/Encrypting an entire system") to set up LVM on LUKS.

See [Particionamento#Partições discretas](/index.php/Particionamento#Partições_discretas "Particionamento") for recommendations on the size of your partitions.

Once your root partition is mounted, `mount` your encrypted boot partition as `/mnt/boot` and your EFI system partition as `/mnt/efi`.

### Installation procedure and custom encrypt hook

Follow the [installation guide](/index.php/Installation_guide "Installation guide") up to the `mkinitcpio` step but do not do it yet, and skip the partitioning, formatting, and mounting steps as they have already been done.

In order to get the encrypted setup to work, you need to build your own hook, which is thankfully easy to do and here is the code you need. You will have to follow [Persistent block device naming#by-id and by-path](/index.php/Persistent_block_device_naming#by-id_and_by-path "Persistent block device naming") to figure out your own `by-id` values for the usb and main hard drive (they are linked -> to `sda` or `sdb`).

You should be using the `by-id` instead of just `sda` or `sdb` because `sdX` can change and this ensures it is the correct device.

You can name `customencrypthook` anything you want, and custom build hooks can be placed in the `hooks` and `install` folders of `/etc/initcpio`. Keep a backup of both files (`cp` them over to the `/home` partition or your user's `/home` directory after you make one). `/usr/bin/ash` is not a typo.

 `/etc/initcpio/hooks/customencrypthook` 
```
#!/usr/bin/ash

run_hook() {
    modprobe -a -q dm-crypt >/dev/null 2>&1
    modprobe loop
    [ "${quiet}" = "y" ] && CSQUIET=">/dev/null"

    while [ ! -L '/dev/disk/by-id/*usbdrive*-part2' ]; do
     echo 'Waiting for USB'
     sleep 1
    done

    cryptsetup open /dev/disk/by-id/*usbdrive*-part2 cryptboot
    mkdir -p /mnt
    mount /dev/mapper/cryptboot /mnt
    cryptsetup open /mnt/key.img lukskey
    cryptsetup --header /mnt/header.img --key-file=/dev/mapper/lukskey --keyfile-offset=''offset'' --keyfile-size=''size'' open /dev/disk/by-id/*harddrive* enc
    cryptsetup close lukskey
    umount /mnt
}

```

`*usbdrive*` is your USB drive `by-id`, and `*harddrive*` is your main hard drive `by-id`.

**Tip:** You could also close `cryptboot` using `cryptsetup close`, but having it open makes it easier to mount for system updates using [Pacman](/index.php/Pacman "Pacman") and regenerating the initramfs with [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"). The `/boot` partition must be mounted for updates that affect the [kernel](/index.php/Kernel "Kernel") or [Initramfs](/index.php/Initramfs "Initramfs"), and the initramfs will be automatically regenerated after these updates.

```
# cp /usr/lib/initcpio/install/encrypt /etc/initcpio/install/customencrypthook

```

Now edit the copied file and remove the `help()` section as it is not necessary.

 `/etc/mkinitcpio.conf (edit this only do not replace it, these are just excerpts of the necessary parts)` 
```
MODULES=(loop)
...
HOOKS=(base udev autodetect modconf block customencrypthook lvm2 filesystems keyboard fsck)
```

The `files=()` and `binaries=()` arrays are empty, and you should not have to replace `HOOKS=(...)` array entirely just edit in `customencrypthook lvm2` after `block` and before `filesystems`, and make sure `systemd`, `sd-lvm2`, and `encrypt` are removed.

#### Boot Loader

Finish the [Installation Guide](/index.php/Installation_guide#Initramfs "Installation guide") from the `mkinitcpio` step. To boot you would need either [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") or [efibootmgr](/index.php/Efibootmgr "Efibootmgr"). Note you can use [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") to support the encrypted disks by [Configuring the boot loader](/index.php/Dm-crypt/Encrypting_an_entire_system#Configuring_the_boot_loader_6 "Dm-crypt/Encrypting an entire system") but editing the `GRUB_CMDLINE_LINUX` is not necessary for this set up.

Or use Direct UEFI Secure boot by generating keys with [cryptboot](https://aur.archlinux.org/packages/cryptboot/) then signing the initramfs and kernel and creating a bootable *.efi* file for your EFI system partition with [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/). Before using cryptboot or sbupdate note this excerpt from [Secure Boot#Using your own keys](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot"):

**Tip:** Note that [cryptboot](https://aur.archlinux.org/packages/cryptboot/) requires the encrypted boot partition to be specified in `/etc/crypttab` before it runs, and if you are using it in combination with [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/), sbupdate expects the `/boot/efikeys/db.*` files created by cryptboot to be capitalized like `DB.*` unless otherwise configured in `/etc/default/sbupdate`. Users who do not use systemd to handle encryption may not have anything in their `/etc/crypttab` file and would need to create an entry.

```
# efibootmgr -c -d /dev/*device* -p *partition_number* -L "Arch Linux Signed" -l "EFI\Arch\linux-signed.efi"

```

See [efibootmgr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/efibootmgr.8) for an explanation of the options.

Make sure the boot order puts `Arch Linux Signed` first. If not change it with `efibootmgr -o XXXX,YYYY,ZZZZ`.

### Changing the LUKS keyfile

```
# cryptsetup --header /boot/header.img --key-file=/dev/mapper/lukskey --keyfile-offset=*offset* --keyfile-size=*size* luksChangeKey /dev/mapper/enc /dev/mapper/lukskey2 --new-keyfile-size=*newsize* --new-keyfile-offset=*newoffset*

```

Afterwards, `cryptsetup close lukskey` and [shred](/index.php/Shred "Shred") or [dd](/index.php/Securely_wipe_disk#dd "Securely wipe disk") the old keyfile with random data before deleting it, then make sure that the new keyfile is renamed to the same name of the old one: `key.img` or other name.