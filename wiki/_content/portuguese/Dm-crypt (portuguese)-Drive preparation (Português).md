Artigos relacionados

*   [Criptografia de disco#Preparando o disco](/index.php/Criptografia_de_disco#Preparando_o_disco "Criptografia de disco")
*   [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk")

**Status de tradução:** Esse artigo é uma tradução de [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation"). Data da última tradução: 2019-12-24\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Dm-crypt/Drive_preparation&diff=0&oldid=591581) na versão em inglês.

Antes de criptografar uma unidade de armazenamento, é recomendado apaga-la com segurança, a sobrescrevendo com dados aleatórios. Isto é realizado para prevenir ataques criptográficos ou indesejada [recuperação de arquivos](/index.php/File_recovery "File recovery"), estes dados não são disceníveis dos dados depois de escritos pelo dm-crypt. Para uma compreensiva discursão veja [Criptografia de disco#Preparando o disco](/index.php/Criptografia_de_disco#Preparando_o_disco "Criptografia de disco").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Apagando o disco com segurança](#Apagando_o_disco_com_segurança)
    *   [1.1 Métodos genéricos](#Métodos_genéricos)
    *   [1.2 Métodos específicos do dm-crypt](#Métodos_específicos_do_dm-crypt)
        *   [1.2.1 dm-crypt limpa o disco vazio ou partição](#dm-crypt_limpa_o_disco_vazio_ou_partição)
        *   [1.2.2 Apagando o espaço livre depois da instalação com dm-crypt](#Apagando_o_espaço_livre_depois_da_instalação_com_dm-crypt)
        *   [1.2.3 Apagar o cabeçalho do LUKS](#Apagar_o_cabeçalho_do_LUKS)
*   [2 Particionamento](#Particionamento)
    *   [2.1 Partições físicas](#Partições_físicas)
    *   [2.2 Dispositivos de blocos empilhados](#Dispositivos_de_blocos_empilhados)
    *   [2.3 Subvolumes do btrfs](#Subvolumes_do_btrfs)
    *   [2.4 Partição de boot (GRUB)](#Partição_de_boot_(GRUB))

## Apagando o disco com segurança

Quando estiver decidindo qual método usar para apagar o disco com segurança, se lembre que só precisa executar somente uma vez enquanto o disco está criptografado.

**Atenção:** Faça o backup de dados importantes antes de começar!

**Nota:** Quando estiver apagando uma grande quantidade de dados, o processo pode demorar algumas horas ou dias para terminar.

**Dica:**

*   Este processo pode demorar mais de um dia para terminar em disco com vários terabyte. Para usar a máquina durante a operação, pode ser desejado usar um sistema já instalado em outro disco, ao invés do sistema live de instalação do Arch.
*   Para [SSDs](/index.php/SSD "SSD"), como um esforço de minimizar artefatos de cache da [memória flash](/index.php/Securely_wipe_disk#Flash_memory "Securely wipe disk"), considere fazer *prioritariamente* [limpa de células de memória do SSD](/index.php/SSD_memory_cell_clearing "SSD memory cell clearing") do que as instruções abaixo.

### Métodos genéricos

Para instruções detalhadas de como apagar e preparar o disco consulte [Limpar o disco com segurança](/index.php/Securely_wipe_disk "Securely wipe disk").

### Métodos específicos do dm-crypt

Os três métodos a seguir são específicos do dm-crypt e são mencionados porque eles são muito rápidos e também podem ser executados depois que uma partição for configurada.

O [FAQ do cryptsetup](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup) (item 2.19 "*How can I wipe a device with crypto-grade randomness?*") menciona um procedimento muito simples para usar um dm-crypt-volume existente para apagar todo o espaço não usado no dispositivo de bloco com dados aleatórios, com este agindo como um simples gerador de números. Também clama proteger contra a divulgação de padrões de uso. Por causa disso os dados criptografados são praticamente não disceníveis dos aleatórios.

#### dm-crypt limpa o disco vazio ou partição

Primeiro, crie um container criptografado temporário na partição (usando a forma `sdXY`) ou disco (usando a forma `sdX`) a ser criptografado:

```
# cryptsetup open --type plain -d /dev/urandom /dev/*dispositivo_de_bloco* a_ser_apagado

```

Você pode verificar se ela existe:

 `# lsblk` 
```
NAME             MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINT
sda                8:0    0  1.8T  0 disk
└─a_ser_apagado  252:0    0  1.8T  0 crypt

```

Apague o container com zeros. O uso do `if=/dev/urandom` não é necessário, já que a cifra criptografada é usada para aleatoriedade.

 `# dd if=/dev/zero of=/dev/mapper/a_ser_apagado status=progress`  `dd: writing to ‘/dev/mapper/a_ser_apagado’: No space left on device` 
**Dica:**

*   *dd* com a opção `bs=`, exemplo `bs=1M`, é frequentemente usado para aumentar a taxa de transferência da operação.
*   Para checar a operação, zere a partição antes de limpar o container. Depois o comando para apagar `blockdev --getsize64 */dev/mapper/<container>*` pode ser usado para adquirir o tamanho exato do container como root. Agora *od* pode ser usado para verificar se os setores zerados foram sobrescrevido, exemplo `od -j *containersize - blocksize*` para visualizar a limpeza concluída até o final.

Finalmente feche o container temporário:

```
# cryptsetup close a_ser_apagado

```

Quando criptografar o sistema todo, o próximo passo é [#Particionamento](#Particionamento). Se está somente criptografando uma partição, continue em [dm-crypt/Criptografando um sistema de arquivos não raiz#Partição](/index.php/Dm-crypt/Criptografando_um_sistema_de_arquivos_n%C3%A3o_raiz#Partição "Dm-crypt/Criptografando um sistema de arquivos não raiz").

#### Apagando o espaço livre depois da instalação com dm-crypt

Usuários que não têm tempo para apagar com segurança antes da [instalação](/index.php/Dm-crypt/Criptografando_todo_um_sistema "Dm-crypt/Criptografando todo um sistema"), podem conseguir um efeito similar uma vez que o sistema criptografado está ligado e montado. No entanto, considere que o sistema de arquivos pode ter reservado espaço, por exemplo para, o usuário root ou outro mecanismo de [cota de disco](/index.php/Disk_quota "Disk quota"), que podem limitar esse procedimento mesmo quando feito com o usuário root: Algumas partes do disco podem não ser sobrescritas de forma alguma.

Para fazer isso, dentro de um container criptografado, crie um arquivo temporário com todo o espaço livre da partição :

 `# dd if=/dev/zero of=/arquivo/no/container status=progress`  `dd: writing to ‘/arquivo/no/container ’: No space left on device` 

Sincronize o cache de disco e então delete esse arquivo para recuperar o espaço anteriormente usado.

```
# sync
# rm /arquivo/no/container

```

Isto deve ser repetido para todas as partições criadas e que possuem sistema de arquivos. Por exemplo, ao optar por [LVM dentro do LUKS](/index.php/Dm-crypt/Criptografando_todo_um_sistema#LVM_dentro_do_LUKS "Dm-crypt/Criptografando todo um sistema"), esse procedimento tem que ser feito em todos os volumes lógicos.

#### Apagar o cabeçalho do LUKS

As partições formatadas com dm-crypt/LUKS contém um cabeçalho com cifras e opções criptográficas usadas, que é referido como `dm-mod` quando abrindo o dispositivo de bloco. Depois do cabeçalho os dados aleatórios da partição começam. Consequentemente, quando reinstalando em um disco que já possui esses dados, ou recondicionando um (exemplo, venda do PC, troca de discos, etc.), *pode* ser suficiente somente apagar o cabeçalho da partição, ao invés de sobrescrever o disco todo - que pode ser algo demorado.

Apagar o cabeçalho do LUKS deletará a chave mestre PBKDF2-encrypted (AES), sais(salts) e assim em diante.

**Nota:** É crucial escrever para partição criptografada LUKS (`/dev/sdX**1**` neste exemplo) e não diretamente nos discos. Configurações com encriptação como uma camada do dispositivo mapeador em cima dos outros, exemplo LVM dentro do LUKS no RAID, deve então escrever para o RAID respectivamente.

Um cabeçalho do LUKS1, com chave padrão de 256 bit, ocupa 1024KiB. É recomendado também sobrescrever os primeiros 4 KiB escritos pelo dm-crypt, então 1028 KiB têm que ser apagados. Isto é `1052672` Bytes.

Para isso faça:

```
# head -c 1052672 /dev/urandom > */dev/sdX1*; sync

```

Para chaves com tamanho de 512 bit (exemplo, aes-xts-plain com chave de 512 bit) o cabeçalho é 2 MiB. O cabeçalho do LUKS2 é 4 MiB, se criado com [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) < 2.1 ou 16 MiB, se criado com [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) > 2.1

Em caso de dúvida, seja generoso e sobrescreva os primeiros 20 MiB. Por exemplo, usando o dd:

```
# dd if=/dev/urandom of=*/dev/sdX1* bs=512 count=40960

```

Ou use [shred](/index.php/Shred "Shred"). Para sobrescrever 20 vezes os primeiros 20 MiB:

```
# shred -v -z -s 20MiB -n 20 */dev/sdX1*

```

**Nota:** Com uma cópia de backup do cabeçalho, os dados podem ser recuperados mas o sistema de arquivos foi provavelmente danificado, já que os primeiros setores criptografados foram sobrescritos. Veja outras seções sobre como fazer o backup de blocos de cabeçalho cruciais.

Quando se apaga um cabeçalho com dados aleatórios tudo deixado no dispositivo são arquivos criptografados. Uma exceção pode acontecer para SSDs devido aos blocos de cache empregados. Em teoria o cabeçalho pode ter sido salvo em algum momento anterior e uma cópia, consequentemente, ainda estará disponível depois de apagar o cabeçalho original. Se possui forte preocupação com segurança, apague o [ATA](https://en.wikipedia.org/wiki/pt:ATA "wikipedia:pt:ATA") com segurança (para prosseguir veja o [FAQ 5.19](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects)) do cryptsetup.)

## Particionamento

Esta seção somente se aplica a um sistema criptografado. Depois que o disco foi sobrescrito com segurança, um particionamento apropriado tem que ser escolhido, levando em conta os requisitos do dm-crypt e efeitos que as várias escolhas terão na manutenção do sistema resultante.

É importante notar que em [quase](#Partição_de_boot_(GRUB)) todo caso é necessário uma partição separada para `/boot` que deve se manter não criptografada, porquê o gerenciador de boot precisa acessar o diretório}} para carregar o initramfs/módulos de encriptação necessários para o resto do sistema (veja [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") para detalhes). Se preocupado com a segurança, veja [dm-crypt/Especificidades#Protegendo a partição de boot não criptografada](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties").

Outro fator importante a se levar em conta é como o swap e o sistema de suspensão serão tratados, veja [dm-crypt/Swap criptografado](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

### Partições físicas

No caso mais simples, as camadas criptografadas podem ser diretamente colocadas em partições físicas; veja [Particionamento](/index.php/Particionamento "Particionamento") para métodos de como criá-las. Assim como em um sistema não criptografado, a partição root é suficiente, exceto outra para `/boot`, como falado acima. Este método permite decidir quais partições criptografar e quais não, e funciona do mesmo jeito não importando a quantidade de discos envolvidos. Também é possível adicionar ou remover partições no futuro, mas redimensionar vai ficar limitado ao tamanho do disco utilizado. Finalmente, note que senhas separadas ou chaves são necessárias para abrir cada partição criptografada, apesar que isto pode ser automatizado durante a inicialização usando o arquivo `crypttab`, veja [Dm-crypt/Configuração do sistema#crypttab](/index.php/Dm-crypt/Configura%C3%A7%C3%A3o_do_sistema#crypttab "Dm-crypt/Configuração do sistema").

### Dispositivos de blocos empilhados

Se mais flexibilidade é necessária, dm-crypt pode coexistir com outros dispositivos de blocos empilhadores como [LVM](/index.php/LVM "LVM") e [RAID](/index.php/RAID "RAID"). Os containers criptografados podem residir abaixo ou em cima de outros:

*   Se os dispositivos LVM/RAID são criados em cima da camada criptografada, será possível adicionar, remover ou redimensionar os sistemas de arquivos da mesma partição criptografada deliberadamente, e somente uma chave ou senha será necessária para todos. Desde que a camada criptografada reside na partição física não será possível se aproveitar da habilidade do LVM e RAID para expandir para múltiplos discos.
*   Se a camada criptografada é criada em cima do LVM/RAID, ainda será possível reorganizar os sistemas de arquivos no futuro, mas com a complexidade adicionada, as camadas criptografadas terão que ser adaptadas de acordo. adicionalmente, senhas e chaves separadas serão necessárias para abrir cada dispositivo criptografado. Esta, no entanto, é a única escolha para sistemas que precisam criptografar sistemas de arquivos para múltiplos discos.

### Subvolumes do btrfs

[Btrfs](/index.php/Btrfs "Btrfs") tem uma [funcionalidade de subvolumes](/index.php/Btrfs#Subvolumes "Btrfs") que podem ser usados com dm-crypt, tirando a necessidade de usar LVM se nenhum outro sistema de arquivos for usado. No entanto, note que arquivos swap não são [suportados](https://btrfs.wiki.kernel.org/index.php/FAQ#Does_btrfs_support_swap_files.3F) pelo brtrfs antes do Linux 5.0, então uma partição [swap criptografada](/index.php/Encrypted_swap "Encrypted swap") necessária se quer usar [swap](/index.php/Swap_(Portugu%C3%AAs) "Swap (Português)") no Linux <5.0 (exemplo [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)). Veja também [dm-crypt/Criptografando todo um sistema#Subvolumes do Btrfs com swap](/index.php/Dm-crypt/Criptografando_todo_um_sistema#Subvolumes_do_Btrfs_com_swap "Dm-crypt/Criptografando todo um sistema").

### Partição de boot (GRUB)

Veja [dm-crypt/Criptografando todo um sistema#Partição de boot criptografada (GRUB)](/index.php/Dm-crypt/Criptografando_todo_um_sistema#Partição_de_boot_criptografada_(GRUB) "Dm-crypt/Criptografando todo um sistema").