**Status de tradução:** Esse artigo é uma tradução de [EFISTUB](/index.php/EFISTUB "EFISTUB"). Data da última tradução: 2019-09-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=EFISTUB&diff=0&oldid=580648) na versão em inglês.

Artigos relacionados

*   [Processo de inicialização do Arch](/index.php/Processo_de_inicializa%C3%A7%C3%A3o_do_Arch "Processo de inicialização do Arch")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

O kernel Linux suporta a inicialização EFISTUB, que permite que o firmware [EFI](/index.php/EFI "EFI") carregue o kernel como um executável EFI. A opção é ativada por padrão nos kernels do Arch Linux ou, se você estiver compilando o kernel, pode ativá-lo, definindo `CONFIG_EFI_STUB=y` na configuração do Kernel. Veja [The EFI Boot Stub](https://www.kernel.org/doc/Documentation/efi-stub.txt) para mais informações.

Com EFISTUB, um kernel pode ser inicializado diretamente por uma placa-mãe UEFI ou indiretamente usando um [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot"). Recomenda-se o uso de um gerenciador de boot se você tiver vários pares kernel/initramfs e o menu de inicialização UEFI da sua placa-mãe não for fácil de usar.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Preparando para EFISTUB](#Preparando_para_EFISTUB)
*   [2 Inicializando EFISTUB](#Inicializando_EFISTUB)
    *   [2.1 Usando um gerenciador de boot](#Usando_um_gerenciador_de_boot)
    *   [2.2 Usando UEFI Shell](#Usando_UEFI_Shell)
    *   [2.3 Usando UEFI diretamente](#Usando_UEFI_diretamente)
        *   [2.3.1 efibootmgr](#efibootmgr)
        *   [2.3.2 efibootmgr com arquivo .efi](#efibootmgr_com_arquivo_.efi)
        *   [2.3.3 UEFI Shell](#UEFI_Shell)
        *   [2.3.4 Mais ferramentas](#Mais_ferramentas)
        *   [2.3.5 Usando um script startup.nsh](#Usando_um_script_startup.nsh)
*   [3 Solução de problemas](#Solução_de_problemas)
    *   [3.1 Não foi possível criar uma entrada de inicialização com efibootmgr](#Não_foi_possível_criar_uma_entrada_de_inicialização_com_efibootmgr)
*   [4 Veja também](#Veja_também)

## Preparando para EFISTUB

Primeiro, você deve criar uma [partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") e escolher como ela é montada. Consulte [Partição de sistema EFI#Montar a partição](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI#Montar_a_partição "Partição de sistema EFI") para todas as opções de montagem ESP disponíveis.

**Dica:**

*   O [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") vai atualizar diretamente o kernel que o firmware EFI vai ler se você montar a ESP para `/boot`.
*   Você pode manter o kernel e o initramfs fora da ESP se você usar um gerenciador de inicialização que tenha um driver do sistema de arquivos para a partição onde eles residem, por exemplo, [rEFInd](/index.php/REFInd "REFInd").

## Inicializando EFISTUB

**Nota:** O caminho do initramfs do Linux Kernel EFISTUB deve ser relativo à raiz da Partição do Sistema EFI e deve usar barras invertidas (de acordo com os padrões EFI). Por exemplo, se o initramfs estiver localizado em `*esp*/EFI/arch/initramfs-linux.img`, a linha formatada com UEFI correspondente deverá ser `initrd=\EFI\arch\initramfs-linux.img`. Nos exemplos a seguir, vamos assumir que tudo está sob `*esp*/`.

### Usando um gerenciador de boot

Existem vários gerenciadores de boot UEFI que podem fornecer opções adicionais ou simplificar o processo de inicialização via UEFI - especialmente se você tiver vários kernels/sistemas operacionais. Veja [Processo de inicialização do Arch#Gerenciador de boot](/index.php/Processo_de_inicializa%C3%A7%C3%A3o_do_Arch#Gerenciador_de_boot "Processo de inicialização do Arch") para mais informações.

### Usando UEFI Shell

É possível iniciar um kernel EFISTUB a partir do UEFI Shell como se fosse um aplicativo UEFI normal. Neste caso, os parâmetros do kernel são passados como parâmetros normais para o arquivo de kernel EFISTUB lançado.

```
> fs0:
> \vmlinuz-linux root=PARTUUID=3518bb68-d01e-45c9-b973-0b5d918aae96 rw initrd=\initramfs-linux.img

```

Para evitar a necessidade de lembrar de todos os seus parâmetros do kernel, você pode salvar o comando executável em um script de shell como `archlinux.nsh` na sua partição de sistema UEFI e executá-lo com:

```
> fs0:
> archlinux

```

### Usando UEFI diretamente

O UEFI foi projetado para remover a necessidade de um bootloader intermediário, como o [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)"). Se a sua placa-mãe tiver uma boa implementação de UEFI, é possível embutir os parâmetros do kernel dentro de uma entrada de boot UEFI e para a placa-mãe inicializar o Arch diretamente. Você pode usar o [efibootmgr](/index.php/Efibootmgr "Efibootmgr") ou o UEFI Shell v2 para modificar as entradas de inicialização da sua placa-mãe.

#### efibootmgr

Para criar uma entrada de inicialização que carregue o kernel usando o *efibootmgr*, execute um comando similar a este:

```
# efibootmgr --disk */dev/sdX* --part *Y* --create --label "Arch Linux" --loader /vmlinuz-linux --unicode 'root=PARTUUID=*XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX* rw initrd=\initramfs-linux.img' --verbose

```

sendo `*/dev/sdX*` e `*Y*` a unidade e o número da partição onde a ESP está localizada. Altere o parâmetro `root=` para refletir sua partição raiz do Linux, consulte os [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel#Lista_de_parâmetros "Parâmetros do kernel") para formatos de nome de dispositivo suportados e [nomeação persistente de dispositivo de bloco](/index.php/Nomea%C3%A7%C3%A3o_persistente_de_dispositivo_de_bloco "Nomeação persistente de dispositivo de bloco") para obter o valor correspondente.

Note que o argumento `-u`/`--unicode` entre aspas é apenas a lista de [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel"), então você pode precisar adicionar parâmetros adicionais (por exemplo, para [suspender para o disco](/index.php/Suspend_and_hibernate#Required_kernel_parameters "Suspend and hibernate") ou [microcódigo](/index.php/Microcode "Microcode")).

Após adicionar a entrada de inicialização, você pode verificar que a entrada foi adiciona corretamente com:

```
# efibootmgr --verbose

```

Para definir a ordem de inicialização, execute:

```
# efibootmgr --bootorder *XXXX*,*XXXX* --verbose

```

sendo *XXXX* o número que aparece na saída do comando *efibootmgr* para cada entrada.

**Dica:** É conveniente salvar o comando para criar a entrada de inicialização em um script de shell, o que facilita a modificação, por exemplo, ao alterar os parâmetros do kernel.

**Dica:** A publicação de fórum com título [The linux kernel with build in bootloader?](https://bbs.archlinux.org/viewtopic.php?pid=1090040#p1090040) também pode ser de seu interesse.

#### efibootmgr com arquivo .efi

Se estiver usando [cryptboot](https://aur.archlinux.org/packages/cryptboot/) e [sbupdate-git](https://aur.archlinux.org/packages/sbupdate-git/) para gerar suas próprias chaves para [Secure Boot](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot") e assinar o initramfs e o kernel para, então, criar uma imagem *.efi* inicializável, o [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) pode ser usado diretamente para inicializar o arquivo *.efi*:

```
# efibootmgr --create --disk /dev/sdX --part *número_partição* --label "*rótulo*" --loader "EFI\*pasta*\*arquivo*.efi" --verbose

```

Consulte [efibootmgr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/efibootmgr.8) para uma explicação das opções.

#### UEFI Shell

Algumas implementações de UEFI dificultam a modificação do NVRAM usando o *efibootmgr*. Se o *efibootmgr* não conseguir criar uma entrada com êxito, você poderá usar o comando [bcfg](/index.php/UEFI#bcfg "UEFI") no UEFI Shell v2 (isto é, a partir da [iso live do Arch Linux](https://www.archlinux.org/download/)).

Primeiro, descubra o número do dispositivo onde sua [ESP](/index.php/ESP_(Portugu%C3%AAs) "ESP (Português)") reside usando:

```
Shell> map

```

Neste exemplo, `1` é usado como o número do dispositivo. Para listar o conteúdo da [ESP](/index.php/ESP_(Portugu%C3%AAs) "ESP (Português)"):

```
Shell> ls fs1:

```

Para ver as entradas de inicialização atuais:

```
Shell> bcfg boot dump

```

Para adicionar uma entrada para o seu kernel, use:

```
Shell> bcfg boot add *N* fs1:\vmlinuz-linux "Arch Linux"

```

sendo `*N*` o local onde a entrada será adicionada no menu de inicialização. 0 é o primeiro item de menu. Os itens de menu já existentes serão deslocados no menu sem serem descartados.

Para adicionar as opções de kernel necessárias, primeiro crie um arquivo na sua ESP:

```
Shell> edit fs1:\options.txt

```

No arquivo, adicione a linha de inicialização. Por exemplo:

```
root=/dev/sda2 ro initrd=\initramfs-linux.img

```

**Nota:** Adicione espaços extras no início da linha no arquivo. Existe uma [marca de ordem de byte](https://en.wikipedia.org/wiki/pt:Marca_de_ordem_de_byte "wikipedia:pt:Marca de ordem de byte") no início da linha que irá esmagar qualquer caractere próximo a ele, o que causará um erro ao inicializar.

Pressione `F2` para salvar e, então, `F3` para sair.

Para adicionar essas opções à sua entrada anterior, faça:

```
Shell> bcfg boot -opt *N* fs1:\options.txt

```

Repita este processo para quaisquer entradas adicionais.

Para remover um item adicionado anteriormente, faça:

```
Shell> bcfg boot rm *N*

```

#### Mais ferramentas

Algumas das ferramentas acima, e mais, são brevemente discutidas em [rEFInd#Tools](/index.php/REFInd#Tools "REFInd").

#### Usando um script startup.nsh

Algumas implementações de UEFI não mantêm variáveis EFI entre inicializações "a frio" (por exemplo, [VirtualBox](/index.php/VirtualBox_(Portugu%C3%AAs) "VirtualBox (Português)")) e qualquer coisa definida pela interface de firmware UEFI é perdida no desligamento.

O [UEFI Shell Specification 2.0](http://www.uefi.org/sites/default/files/resources/UEFI_Shell_Spec_2_0.pdf) estabelece que um script chamado `startup.nsh` na raiz da partição ESP sempre ser interpretado e pode conter instruções arbitrárias; entre aquelas que você pode definir uma linha de inicialização. Certifique-se de montar a partição ESP em `/boot` e crie um script `startup.nsh` que contenha uma linha de inicialização do kernel. Por exemplo:

```
vmlinuz-linux rw root=/dev/sd*X* [rootfs=*meufs*] [rootflags=*minhasopçõesraiz*] \
 [kernel.flag=*foo*] [*meumódulo*.flag=*bar*] \
 [initrd=\intel-ucode.img] initrd=\initramfs-linux.img

```

Este método funcionará com quase todas as versões de firmware UEFI que você pode encontrar em hardware real, você pode usá-lo como último recurso. **O script deve ser uma única linha longa.** As seções entre colchetes são opcionais e são fornecidas apenas como um guia. As quebras de linha estilo shell são apenas para esclarecimento visual. Os sistemas de arquivos FAT usam a barra invertida como separador de caminho e, nesse caso, a barra invertida declara que o initramfs está localizado na raiz da partição ESP. Apenas o microcódigo da Intel é carregado na linha de parâmetros de inicialização; O microcódigo da AMD é lido do disco posteriormente durante o processo de inicialização; isso é feito automaticamente pelo kernel.

## Solução de problemas

### Não foi possível criar uma entrada de inicialização com efibootmgr

Algumas combinações de versões do kernel e do *efibootmgr* podem se recusar a criar novas entradas de inicialização. Isso pode ser devido à falta de espaço livre na NVRAM. Você pode tentar excluir quaisquer arquivos de despejo EFI:

```
# rm /sys/firmware/efi/efivars/dump-*

```

Ou, como último recurso, inicialize com o parâmetro do kernel `efi_no_storage_paranoia`. Você também pode tentar [fazer downgrade](/index.php/Downgrade_(Portugu%C3%AAs) "Downgrade (Português)") de sua instalação do *efibootmgr* para a versão 0.11.0\. Esta versão funciona com o Linux versão 4.0.6\. Veja a discussão no relatório de erro [FS#34641](https://bugs.archlinux.org/task/34641), em particular o [comentário final](https://bugs.archlinux.org/task/34641#comment111365), para mais informações.

## Veja também

*   [Documentação do kernel Linux sobre EFISTUB](https://www.kernel.org/doc/Documentation/efi-stub.txt)
*   [Commit Git do EFISTUB no kernel Linux](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=commitdiff;h=291f36325f9f252bd76ef5f603995f37e453fc60;hp=55839d515495e766605d7aaabd9c2758370a8d27)
*   [Página do Rod Smith sobre EFISTUB](http://www.rodsbooks.com/efi-bootloaders/efistub.html)