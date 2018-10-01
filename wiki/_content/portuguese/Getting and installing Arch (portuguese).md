**Status de tradução:** Esse artigo é uma tradução de [Getting and installing Arch](/index.php/Getting_and_installing_Arch "Getting and installing Arch"). Data da última tradução: 2018-10-01\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Getting_and_installing_Arch&diff=0&oldid=544275) na versão em inglês.

A mídia de instalação e suas assinaturas [GnuPG](/index.php/GnuPG "GnuPG") podem ser obtidas a partir da página de [Download](https://archlinux.org/download/).

## Verificar assinatura

É recomendável verificar a assinatura da imagem antes de usá-la, especialmente ao fazer o download de um *espelho HTTP*, no qual os downloads geralmente são propensos a serem interceptados para [servir imagens maliciosas](http://www.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html#explanation).

Em um sistema com [GnuPG](/index.php/GnuPG "GnuPG") instalado, faça isso baixando a *assinatura PGP* (em *Checksums*) para o diretório ISO, e [verificando](/index.php/GnuPG#Verify_a_signature "GnuPG") com `gpg --keyserver pgp.mit.edu --keyserver-options auto-key-retrieve --verify archlinux-<versão>-x86_64.iso.sig`.

Alternativamente, execute `pacman-key -v archlinux-<versão>-x86_64.iso.sig` de uma instalação existente do Arch Linux como root.

**Nota:**

*   A assinatura em si pode ser manipulada se for baixada de um site espelho, em vez de [archlinux.org](https://archlinux.org/download/) como acima. Nesse caso, assegure-se de que a chave pública, que é usada para decodificar a assinatura, seja assinada por outra chave confiável. O comando `gpg` produzirá a impressão digital da chave pública.
*   Outro método para verificar a autenticidade da assinatura é garantir que a impressão digital da chave pública seja idêntica à impressão digital da chave do [desenvolvedor do Arch Linux](https://www.archlinux.org/people/developers/) que assinou o arquivo ISO. Veja [Wikipedia:pt:Criptografia de chave pública](https://en.wikipedia.org/wiki/pt:Criptografia_de_chave_p%C3%BAblica "wikipedia:pt:Criptografia de chave pública") para mais informações sobre o processo de chave pública para autenticar chaves.

## Métodos de instalação

A tabela abaixo oferece uma visão geral das maneiras comuns de inicializar a mídia de instalação. Como o processo de instalação recupera pacotes de um repositório remoto, esses métodos exigem uma conexão com a Internet; veja [Instalação offline de pacotes](/index.php/Offline_installation_of_packages "Offline installation of packages") e [Archiso#Installation without Internet access](/index.php/Archiso#Installation_without_Internet_access "Archiso") quando nenhum estiver disponível.

**Nota:**

*   Apontar o dispositivo de inicialização atual para uma unidade que contém a mídia de instalação do Arch normalmente é obtido pressionando-se uma tecla durante a fase [POST](https://en.wikipedia.org/wiki/pt:POST "wikipedia:pt:POST"), conforme indicado na tela inicial. Consulte o manual da sua placa-mãe para obter detalhes.
*   Quando o menu do Arch aparecer, selecione *Boot Arch Linux* e pressione `Enter` para entrar no ambiente de instalação.
*   Veja [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) para uma lista de [parâmetros de inicialização](/index.php/Kernel_parameters#Configuration "Kernel parameters") e [packages.x86_64](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) para uma lista de pacotes inclusos.

| Método | Artigos | Condições |
| Escrever a imagem em mídia flash ou disco ótico e, em seguida, inicializar a partir dela. | 

*   [Mídia de instalação em flash USB](/index.php/M%C3%ADdia_de_instala%C3%A7%C3%A3o_em_flash_USB "Mídia de instalação em flash USB")
*   [Optical disc drive#Burning](/index.php/Optical_disc_drive#Burning "Optical disc drive")

 | 

*   Instalação em um ou poucas máquinas no máximo
*   Obtenção de um sistema inicialização diretamente

 |
| Montar a imagem em uma máquina servidora e fazer com que os clientes a inicializem pela rede. | 

*   [PXE](/index.php/PXE "PXE")
*   [Sistema sem disco](/index.php/Diskless_system "Diskless system")

 | 

*   Modelo cliente-servidor
*   Conexão de rede cabeada (1Gbit+)

 |
| Montar a imagem em um sistema Linux em execução e instalar o Arch a partir de um ambiente chroot. | 

*   [Instalar a partir de um Linux existente](/index.php/Instalar_a_partir_de_um_Linux_existente "Instalar a partir de um Linux existente")
*   [Instalar a partir de SSH](/index.php/Instalar_a_partir_de_SSH "Instalar a partir de SSH")

 | 

*   Substituir um sistema existente com tempo de inatividade reduzido
*   Instalar na máquina local, ou um remoto via [VNC](/index.php/VNC "VNC") ou [SSH](/index.php/SSH "SSH")

 |
| Configurar uma máquina virtual e instale o Arch como um sistema convidado. | 

*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [Movendo uma instalação existente para dentro (ou fora) de uma máquina virtual](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

 | 

*   Sistema operacional compatível com software de virtualização
*   Obter um sistema isolado para aprender, testar ou depurar

 |
| Instalar Arch ao lado de uma instalação do Windows. | 

*   [Dual boot com Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows")

 | 

*   Máquina compartilhada com usuários do Windows
*   Permitir a redefinição com padrões de fábrica de um dispositivo pré-instalado no Windows

 |

## Veja também

*   [README.transfer](https://projects.archlinux.org/archiso.git/tree/docs/README.transfer)
*   [README.altbootmethods](https://projects.archlinux.org/archiso.git/tree/docs/README.altbootmethods)