**Dica:** Esta é parte de um artigo multi-páginas do "The Beginners' Guide" ("O Guia para Iniciantes"). **[Clique aqui](/index.php/Beginners%27_Guide_(Portugu%C3%AAs) "Beginners' Guide (Português)")** se preferir ler o artigo completo.

## Contents

*   [1 Preparar a Instalação](#Preparar_a_Instala.C3.A7.C3.A3o)
    *   [1.1 Obtendo a última mídia de instalação](#Obtendo_a_.C3.BAltima_m.C3.ADdia_de_instala.C3.A7.C3.A3o)
        *   [1.1.1 Verificação de integridade da imagem ISO](#Verifica.C3.A7.C3.A3o_de_integridade_da_imagem_ISO)
        *   [1.1.2 Instalação através de mídia (CD/DVD) ou pendrive](#Instala.C3.A7.C3.A3o_atrav.C3.A9s_de_m.C3.ADdia_.28CD.2FDVD.29_ou_pendrive)
        *   [1.1.3 Instalação via Rede](#Instala.C3.A7.C3.A3o_via_Rede)
        *   [1.1.4 Instalação em Máquina Virtual](#Instala.C3.A7.C3.A3o_em_M.C3.A1quina_Virtual)
    *   [1.2 Inicializar o Instalador Arch Linux](#Inicializar_o_Instalador_Arch_Linux)
        *   [1.2.1 Testando se inicialização é do tipo UEFI](#Testando_se_inicializa.C3.A7.C3.A3o_.C3.A9_do_tipo_UEFI)
        *   [1.2.2 Verificando problemas de inicialização](#Verificando_problemas_de_inicializa.C3.A7.C3.A3o)

## Preparar a Instalação

**Nota:** Se você desejar instalar em outra partição a partir de uma distribuição GNU/Linux já existente ou o LiveCD, por favor veja [este artigo de wiki](/index.php/Install_from_Existing_Linux_(Portugu%C3%AAs) "Install from Existing Linux (Português)") para obter as etapas para fazer isso. Isso pode ser útil especialmente se você planeja instalar o Arch via VNC ou SSH remotamente. O seguinte artigo assume que a instalação ocorrerá por meios convencionais.

### Obtendo a última mídia de instalação

Você pode obter a mídia de instalação [aqui](https://www.archlinux.org/download/). No momento atual, a última versão disponível é a 2014.09.03 do qual este guia trata. Lançamentos antigos podem ser encontrados no [seguinte link](https://www.archlinux.org/releng/releases/) *(e estes não são mais oficialmente suportados)*.

#### Verificação de integridade da imagem ISO

A verificação da imagem ISO pode ser feita das seguintes formas:

```
 $ sha1sum --check arquivo_com_checksum_sha1.txt archlinux_versao.iso

```

ou

```
 $ md5sum --check arquivo_com_checksum_md5.txt archlinux_versao.iso

```

Os arquivos contendo as somas de verificação podem ser encontrados [aqui](https://www.archlinux.org/download/), na sessão *Checksums*. Atente-se apenas para baixar o arquivo de soma correspondente ao algorítmo utilizado (md5 ou sha1) e a versão do Arch Linux que você efetuou download.

#### Instalação através de mídia (CD/DVD) ou pendrive

*   Grave o arquivo de imagem .iso em um CD ou DVD utilizando um programa para gravar imagens ISO de sua preferência

**Nota:** A qualidade dos discos ópticos, bem como da mídia CD em si, variam muito. Geralmente usar uma velocidade lenta de gravação é recomendado para gravações confiáveis; Alguns usuários recomendam velocidades ***tão baixas como 4x ou 2x.*** Se você está tendo um comportamento inesperado do CD, tente gravar na velocidade mínima suportada pelo seu sistema.

*   Alternativamente, você pode gravar a imagem do Arch Linux em um dispositivo de memória flash (pendrive). Para instruções detalhadas acesse [Instalar a partir de um drive flash USB](/index.php/Install_from_a_USB_flash_drive_(Portugu%C3%AAs) "Install from a USB flash drive (Português)")

#### Instalação via Rede

Em vez de gravar o disco de boot em uma unidade USB ou disco, você poderá alternativamente inicializar a imagem .iso através da rede. Isso funciona bem quando você já tiver um servidor configurado. Por favor, veja [este artigo](/index.php/Install_Arch_from_network_(via_PXE) "Install Arch from network (via PXE)") para obter mais informações, e depois continue em [Inicializar o Instalador Arch Linux](#Inicializar_o_Instalador_Arch_Linux)

#### Instalação em Máquina Virtual

A instalação em uma é uma boa forma de familiarização com o Arch Linux e seu processo de instalação, sem correr os riscos de afetar seu sistema operacional atual, ou alterar o particionamento de seus discos. Também é uma forma eficiente de lhe manter acessível a este guia enquanto efetua a instalação. Alguns usuários acharão vantajoso ter uma instalação independente do Arch Linuxm em um drive virtual, para propósitos de testes.

Exemplos de softwares de virtualização: [VirtualBox](/index.php/VirtualBox "VirtualBox"), [VMware](/index.php/VMware "VMware"), [QEMU](/index.php/QEMU "QEMU"), [Xen](/index.php/Xen "Xen"), [Parallels](/index.php/Parallels "Parallels").

O procedimento exato de criação de uma máquina virtual depende do programa utilizado, porém, tal processo pode ser generalizado nos seguintes passos:

1.  Criação do disco de máquina virtual no sistema hospedeiro.
2.  Configuração dos parametros da máquina virtual.
3.  Configuração de boot através da ISO baixada, através de um drive de CD virtual.
4.  Continua em [#Inicializar o Instalador Arch Linux|Inicializar o Instalador Arch Linux]].

Alguns artigos que podem ser úteis:

*   [Arch Linux VirtualBox Guest](/index.php/Arch_Linux_VirtualBox_Guest "Arch Linux VirtualBox Guest")
*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [VirtualBox Arch Linux Guest On Physical Drive](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [Installing Arch Linux in VMware](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

### Inicializar o Instalador Arch Linux

Primeiramente, você deverá alterar a ordem de boot na BIOS de seu computador. Para executar tal tarefa, você terá que pressionar uma das seguintes teclas durante a fase de POST(Power On Self-Test): `Delete`, `F1`, `F2`, `F11` ou `F12`. Configurado o método de boot, selecione a opção "Boot Arch Linux" e pressione `Enter` para iniciar a instalação.

**Dica:** A memória requerida para uma instalação básica é de 64 MB de RAM.

**Dica:** Durante o processo, a protecção de tela automática pode surgir. Se isto ocorrer, pode-se pressionar a tecla Alt com segurança para retornar para a exibição normal.

**Nota:** Usuários que buscam realizar a instalação do Arch Linux remotamente através de uma conexão ssh são incentivados a fazer alguns ajustes neste momento para permitir conexões ssh diretamente para o ambiente CD ao vivo. Se estiver interessado, consulte o artigo [Instalar a partir de SSH](/index.php/Install_from_SSH_(Portugu%C3%AAs) "Install from SSH (Português)").

#### Testando se inicialização é do tipo UEFI

Caso você possua uma placa-mãe [UEFI](/index.php/UEFI "UEFI"), o CD/USB irá lançar uma Shell UEFI mostrando a mensagem que o script `startup.nsh` foi executado. Confie neste script e o execute. Então, para verificar se você inicializou no modo UEFI, carregue o módulo do kernel `efivars` (antes do chroot) e então verifique se existem arquivos em `/sys/firmware/efi/vars/`:

```
# modprobe efivars       # before chrooting
# ls -1 /sys/firmware/efi/vars/

```

**Nota:** O módulo do kernel `efivars` detecta e povoa as variáveis de execução da UEFI em `/sys/firmware/efi/vars`. Este módulo **não** é carregado automaticamente durante o processo de boot, e enquanto este módulo estiver carregado, e o kernel **não possuir** o parametro `noefi` configurado, o diretório `/sys/firmware/efi/vars` permanecerá vazio. Estar variáveis serão modificadas mais tarde pelo `efibootmgr` para adicionar ao bootloader entradas no menu de boot UEFI. No modo BIOS, o modprobe não exibirá erros sobre o módulo efivars. A forma correta de detectar um boot UEFI é verificar a existência de arquivos em `/sys/firmware/efi/vars` .

#### Verificando problemas de inicialização

*   Caso você utilize um dispositivo gráfico da Intel e a tela continua branca durante todo o processo de inicialização, há grandes chances de que o problema seja relacionado ao Kernel Mode Setting ([KMS](/index.php/KMS "KMS")). Uma possível solução de contorno pode ser reiniciar o computador pressionando `Tab` em cima da entrada do menu que você irá escolher(i686 or x86_64). A partir daqui, digite o parâmetro `nomodeset` e pressione `Enter`. Alternativamente, tente `video=SVIDEO-1:d` que, caso funcione, não irá desabilitar completamente o KMS. Veja o artigo [Intel](/index.php/Intel "Intel") para maiores informações.

*   Caso a tela *não* fique branca, porém o processo de inicialização permanece parado no momento da carga do Kernel, pressione `Tab` na entrada de menu como descrito acima, e adiciona `acpi=off` ao final da linha, e então pressione `Enter`.

**[Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide")**

* * *

[Prefácio](/index.php/Beginners%27_Guide/Preface_(Portugu%C3%AAs) "Beginners' Guide/Preface (Português)") >> **Preparar a Instalação** >> [Instalar o sistema base](/index.php/Beginners%27_Guide/Installation_(Portugu%C3%AAs) "Beginners' Guide/Installation (Português)") >> [Extras](/index.php/Beginners%27_Guide/Extra_(Portugu%C3%AAs) "Beginners' Guide/Extra (Português)")