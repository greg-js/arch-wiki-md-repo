**Status de tradução:** Esse artigo é uma tradução de [Dm-crypt](/index.php/Dm-crypt "Dm-crypt"). Data da última tradução: 2019-11-22\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Dm-crypt&diff=0&oldid=589414) na versão em inglês.

Related articles

*   [Disk encryption](/index.php/Disk_encryption "Disk encryption")
*   [Removing system encryption](/index.php/Removing_system_encryption "Removing system encryption")

dm-crypt é o [mapeador de dispositivos](https://en.wikipedia.org/wiki/pt:device_mapper "wikipedia:pt:device mapper") alvo de encriptação do kernel Linux. De acordo com o [Wikipédia](https://en.wikipedia.org/wiki/pt:dm-crypt "wikipedia:pt:dm-crypt"), ele é:

	Um subsistema de criptografia de disco transparente [no] kernel Linux... [É] implementado como um alvo do mapeador de dispositivos e pode ser empilhado sobre outras transformações do mapeador de dispositivos. Ele pode, assim, criptografar discos inteiros (incluindo mídia removível), partições, volumes RAID de software, volumes lógicos e arquivos. Ele aparece como um dispositivo de bloco, que pode ser usado para fazer backup de sistemas de arquivos, swap ou como um volume físico de LVM.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Cenários comuns](#Cenários_comuns)
*   [2 Preparando a unidade de armazenamento](#Preparando_a_unidade_de_armazenamento)
*   [3 Encriptação de dispositivo](#Encriptação_de_dispositivo)
*   [4 Configuração de sistema](#Configuração_de_sistema)
*   [5 Swap criptografada](#Swap_criptografada)
*   [6 Especificidades](#Especificidades)
*   [7 Veja também](#Veja_também)

## Cenários comuns

Esta parte introduz cenários comuns para uso do *dm-crypt* na encriptação de um sistema ou pontos de montagem individuais. Pode ser considerado como um ponto inicial de familiarização com diferentes procedimentos práticos de encriptação. Os cenários possuem links para outras subpáginas quando necessário.

Veja [/Criptografando um sistema de arquivos não raiz](/index.php/Dm-crypt_(Portugu%C3%AAs)/Criptografando_um_sistema_de_arquivos_n%C3%A3o_raiz "Dm-crypt (Português)/Criptografando um sistema de arquivos não raiz") se você precisa criptografar um dispositivo que não é usado na inicialização do seu sistema, como uma [partição](/index.php/Dm-crypt_(Portugu%C3%AAs)/Criptografando_um_sistema_de_arquivos_n%C3%A3o_raiz#Partição "Dm-crypt (Português)/Criptografando um sistema de arquivos não raiz") ou um [dispositivo de loop](/index.php/Dm-crypt_(Portugu%C3%AAs)/Criptografando_um_sistema_de_arquivos_n%C3%A3o_raiz#Dispositivo_de_loop "Dm-crypt (Português)/Criptografando um sistema de arquivos não raiz").

Veja [/Criptografando todo um sistema](/index.php/Dm-crypt_(Portugu%C3%AAs)/Criptografando_todo_um_sistema "Dm-crypt (Português)/Criptografando todo um sistema") se você quer criptografar todo um sistema, em particular a partição raiz. Alguns cenários são cobertos, incluindo o uso do *dm-crypt* com a extensão *LUKS*, modo de encriptação *plain* e *LVM* e encriptação.

## Preparando a unidade de armazenamento

[/Preparando a unidade de armazenamento](/index.php/Dm-crypt_(Portugu%C3%AAs)/Preparando_a_unidade_de_armazenamento "Dm-crypt (Português)/Preparando a unidade de armazenamento") lida com operações como [apagar o disco com segurança](/index.php/Dm-crypt_(Portugu%C3%AAs)/Preparando_a_unidade_de_armazenamento#Apagando_o_disco_com_segurança "Dm-crypt (Português)/Preparando a unidade de armazenamento") e pontos específicos do *dm-crypt* relacionados ao [particionamento](/index.php/Dm-crypt_(Portugu%C3%AAs)/Preparando_a_unidade_de_armazenamento#Particionamento "Dm-crypt (Português)/Preparando a unidade de armazenamento").

## Encriptação de dispositivo

[/Encriptação de dispositivo](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption") cobre como utilizar o dm-crypt para criptografar todo um sistema por meio do comando [cryptsetup](/index.php/Cryptsetup "Cryptsetup"). Possui exemplos de [Opções de encriptação com dm-crypt](/index.php/Dm-crypt/Device_encryption#Encryption_options_with_dm-crypt "Dm-crypt/Device encryption"), lida com a criação de [keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption"), comandos específicos do LUKS para [gerenciamento de chaves](/index.php/Dm-crypt/Device_encryption#Key_management "Dm-crypt/Device encryption") como também para [Backup e restauração](/index.php/Dm-crypt/Device_encryption#Backup_and_restore "Dm-crypt/Device encryption").

## Configuração de sistema

[/Configuração de sistema](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration") ilustra como configurar o [mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration"), o [gerenciador de boot](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") e o arquivo [crypttab](/index.php/Crypttab "Crypttab") quando você está criptografando um sistema.

## Swap criptografada

[/Swap criptografada](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") cobre como adicionar uma partição swap para um sistema criptografado, se necessário. A partição swap também deve ser criptografada para proteger qualquer informação colocada lá pelo sistema. Esta página detalha métodos [sem](/index.php/Dm-crypt/Swap_encryption#Without_suspend-to-disk_support "Dm-crypt/Swap encryption") e [com](/index.php/Dm-crypt/Swap_encryption#With_suspend-to-disk_support "Dm-crypt/Swap encryption") suporte a suspensão para o disco.

## Especificidades

[/Especificidades](/index.php/Dm-crypt/Specialties "Dm-crypt/Specialties") lida com operações especiais como [protegendo partições de boot não criptografadas](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties"), [usando keyfiles criptogradas GPG ou OpenSSL](/index.php/Dm-crypt/Specialties#Using_GPG,_LUKS,_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties"), um método para [ligar e desbloquear pela rede](/index.php/Dm-crypt/Specialties#Remote_unlocking_of_the_root_(or_other)_partition "Dm-crypt/Specialties"), outro para [configurando discard/TRIM para um SSD](/index.php/Dm-crypt/Specialties#Discard/TRIM_support_for_solid_state_drives_(SSD) "Dm-crypt/Specialties"), e seções que lidam com [múltiplos discos e hook de encriptação](/index.php/Dm-crypt/Specialties#The_encrypt_hook_and_multiple_disks "Dm-crypt/Specialties").

## Veja também

*   [dm-crypt](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt) - A página do projeto
*   [cryptsetup](https://gitlab.com/cryptsetup/cryptsetup) - A página do LUKS e [FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions) - a principal e recurso de maior ajuda.
*   [repositório do cryptsetup](https://git.kernel.org/cgit/utils/cryptsetup/cryptsetup.git/) e versões [release](https://www.kernel.org/pub/linux/utils/cryptsetup/).