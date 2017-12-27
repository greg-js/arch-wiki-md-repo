O repositório *multilib* é um [repositório oficial](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") que permite ao usuário executar a compilar aplicativos 32 bits em instalações 64 bits do Arch Linux.

## Contents

*   [1 Estrutura de diretórios](#Estrutura_de_diret.C3.B3rios)
*   [2 Habilitando](#Habilitando)
*   [3 Desabilitando](#Desabilitando)
*   [4 Veja também](#Veja_tamb.C3.A9m)

## Estrutura de diretórios

Com o repositório multilib habilitado, as bibliotecas compatíveis com 32 bits estão localizadas sob `/usr/lib32/`.

## Habilitando

Para usar o repositório [multilib](/index.php/Reposit%C3%B3rios_oficiais#multilib "Repositórios oficiais"), descomente a seção `[multilib]` em `/etc/pacman.conf` (Por favor, certifique-se de descomentar ambas as linhas):

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

Então, [atualize](/index.php/Atualize "Atualize") o sistema e instale os pacotes multilib desejados.

**Dica:** Execute `pacman -Sl multilib` para listar todos os pacotes multilib no repositório *multilib*. Nomes de pacotes de biblioteca 32 bits começam com `lib32-`.

## Desabilitando

Para reverter para um sistema 64 bits puro:

Execute o seguinte comando para remover todos os pacotes que foram instalados do *multilib*:

```
# pacman -R $(paclist multilib | cut -f1 -d' ')

```

Se você tiver conflitos com gcc-libs, reinstale o pacote [gcc-libs](https://www.archlinux.org/packages/?name=gcc-libs) e o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/).

Comente a seção `[multilib]` no `/etc/pacman.conf`:

```
#[multilib]
#Include = /etc/pacman.d/mirrorlist

```

Então, [atualize](/index.php/Atualize "Atualize") o sistema.

## Veja também

*   [Makepkg (Português)#Compilar pacotes 32 bits em um sistema 64 bits](/index.php/Makepkg_(Portugu%C3%AAs)#Compilar_pacotes_32_bits_em_um_sistema_64_bits "Makepkg (Português)")
*   [FAQ (Português)#64 bit](/index.php/FAQ_(Portugu%C3%AAs)#64_bit "FAQ (Português)")
*   Lista de discussão [arch-multilib](//mailman.archlinux.org/mailman/listinfo/arch-multilib)