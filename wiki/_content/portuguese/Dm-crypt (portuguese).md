**Status de tradução:** Esse artigo é uma tradução de [Dm-crypt](/index.php/Dm-crypt "Dm-crypt"). Data da última tradução: 2019-11-27\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Dm-crypt&diff=0&oldid=589414) na versão em inglês.

Artigos relacionados

*   [Criptografia de disco](/index.php/Criptografia_de_disco "Criptografia de disco")
*   [Removing system encryption](/index.php/Removing_system_encryption "Removing system encryption")

dm-crypt é o [mapeador de dispositivos](https://en.wikipedia.org/wiki/pt:device_mapper "wikipedia:pt:device mapper") alvo de encriptação do kernel Linux. De acordo com o [Wikipédia](https://en.wikipedia.org/wiki/pt:dm-crypt "wikipedia:pt:dm-crypt"), ele é:

	Um subsistema de criptografia de disco transparente [no] kernel Linux... [É] implementado como um alvo do mapeador de dispositivos e pode ser empilhado sobre outras transformações do mapeador de dispositivos. Ele pode, assim, criptografar discos inteiros (incluindo mídia removível), partições, volumes RAID de software, volumes lógicos e arquivos. Ele aparece como um dispositivo de bloco, que pode ser usado para fazer backup de sistemas de arquivos, swap ou como um volume físico de LVM.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Cenários comuns](#Cenários_comuns)
*   [2 Preparando a unidade de armazenamento](#Preparando_a_unidade_de_armazenamento)
*   [3 Encriptação de dispositivo](#Encriptação_de_dispositivo)
*   [4 Configuração do sistema](#Configuração_do_sistema)
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

[/Encriptação de dispositivo](/index.php/Dm-crypt_(Portugu%C3%AAs)/Encripta%C3%A7%C3%A3o_de_dispositivo "Dm-crypt (Português)/Encriptação de dispositivo") mostra como utilizar o dm-crypt para criptografar todo um sistema por meio do comando [cryptsetup](/index.php/Cryptsetup "Cryptsetup"). Possui exemplos de [Opções de encriptação com dm-crypt](/index.php/Dm-crypt_(Portugu%C3%AAs)/Encripta%C3%A7%C3%A3o_de_dispositivo#Opções_de_encriptação_com_dm-crypt "Dm-crypt (Português)/Encriptação de dispositivo"), lida com a criação de [keyfiles](/index.php/Dm-crypt_(Portugu%C3%AAs)/Encripta%C3%A7%C3%A3o_de_dispositivo#Keyfiles "Dm-crypt (Português)/Encriptação de dispositivo"), comandos específicos do LUKS para [gerenciamento de chaves](/index.php/Dm-crypt_(Portugu%C3%AAs)/Encripta%C3%A7%C3%A3o_de_dispositivo#Gerenciamento_de_chaves "Dm-crypt (Português)/Encriptação de dispositivo") como também para [Backup e restauração](/index.php/Dm-crypt_(Portugu%C3%AAs)/Encripta%C3%A7%C3%A3o_de_dispositivo#Backup_e_restauração "Dm-crypt (Português)/Encriptação de dispositivo").

## Configuração do sistema

[/Configuração do sistema](/index.php/Dm-crypt_(Portugu%C3%AAs)/Configura%C3%A7%C3%A3o_do_sistema "Dm-crypt (Português)/Configuração do sistema") mostra como configurar o [mkinitcpio](/index.php/Dm-crypt_(Portugu%C3%AAs)/Configura%C3%A7%C3%A3o_do_sistema#mkinitcpio "Dm-crypt (Português)/Configuração do sistema"), o [gerenciador de boot](/index.php/Dm-crypt_(Portugu%C3%AAs)/Configura%C3%A7%C3%A3o_do_sistema#Gerenciador_de_boot "Dm-crypt (Português)/Configuração do sistema") e o arquivo [crypttab](/index.php/Dm-crypt_(Portugu%C3%AAs)/Configura%C3%A7%C3%A3o_do_sistema#crypttab "Dm-crypt (Português)/Configuração do sistema") quando você está criptografando um sistema.

## Swap criptografada

[/Swap criptografada](/index.php/Dm-crypt_(Portugu%C3%AAs)/Swap_criptografada "Dm-crypt (Português)/Swap criptografada") mostra como adicionar uma partição swap para um sistema criptografado, se necessário. A partição swap também deve ser criptografada para proteger qualquer informação colocada lá pelo sistema. Esta página detalha métodos [sem](/index.php/Dm-crypt_(Portugu%C3%AAs)/Swap_criptografada#Sem_suporte_a_suspender_para_o_disco "Dm-crypt (Português)/Swap criptografada") e [com](/index.php/Dm-crypt_(Portugu%C3%AAs)/Swap_criptografada#Com_suporte_a_suspender_para_o_disco "Dm-crypt (Português)/Swap criptografada") suporte a suspensão para o disco.

## Especificidades

[/Especificidades](/index.php/Dm-crypt_(Portugu%C3%AAs)/Especificidades "Dm-crypt (Português)/Especificidades") lida com operações especiais como [protegendo partições de boot não criptografadas](/index.php/Dm-crypt_(Portugu%C3%AAs)/Especificidades#Securing_the_unencrypted_boot_partition "Dm-crypt (Português)/Especificidades"), [usando keyfiles criptogradas GPG, LUKS ou OpenSSL](/index.php/Dm-crypt_(Portugu%C3%AAs)/Especificidades#Usando_keyfiles_criptografadas_com_GPG,_LUKS_ou_OpenSSL "Dm-crypt (Português)/Especificidades"), um método para [abrir remotamente a partição raiz](/index.php/Dm-crypt_(Portugu%C3%AAs)/Especificidades#Abrir_remotamente_a_partição_raiz_(ou_outra) "Dm-crypt (Português)/Especificidades"), outro para [configurar discard/TRIM para um SSD](/index.php/Dm-crypt_(Portugu%C3%AAs)/Especificidades#Suporte_a_discard/TRIM_para_unidades_de_estado_sólido_(SSD) "Dm-crypt (Português)/Especificidades"), e seções que lidam com [o hook encrypt e múltiplos discos](/index.php/Dm-crypt_(Portugu%C3%AAs)/Especificidades#O_hook_encrypt_e_múltiplos_discos "Dm-crypt (Português)/Especificidades").

## Veja também

*   [dm-crypt](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt) - A página do projeto
*   [cryptsetup](https://gitlab.com/cryptsetup/cryptsetup) - A página do LUKS e [FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions) - a principal e recurso de maior ajuda.
*   [repositório do cryptsetup](https://git.kernel.org/cgit/utils/cryptsetup/cryptsetup.git/) e versões [release](https://www.kernel.org/pub/linux/utils/cryptsetup/).