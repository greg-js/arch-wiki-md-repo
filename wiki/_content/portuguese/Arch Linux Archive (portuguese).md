Artigos relacionados

*   [Fazendo downgrade de pacotes](/index.php/Fazendo_downgrade_de_pacotes "Fazendo downgrade de pacotes")

O **Arch Linux Archive** (também conhecido como **ALA**), antigamente conhecido como **Arch Linux Rollback Machine** (ou **ARM**), armazena *snapshots de repositórios oficiais*, *imagens iso* e *traballs de bootstrap* ao longo do tempo.

**Você pode usá-lo para**

*   Fazer downgrade para uma versão anterior de um pacote (última versão está quebrada, desejo usar a anterior)
*   Restaurar todos seus pacotes para um momento específico (meu sistema está quebrado, desejo voltar para 2 meses atrás)
*   Localizar uma versão anterior de uma imagem ISO

## Contents

*   [1 Localização](#Localiza.C3.A7.C3.A3o)
*   [2 Diretórios](#Diret.C3.B3rios)
    *   [2.1 /repos](#.2Frepos)
    *   [2.2 /packages](#.2Fpackages)
    *   [2.3 /iso](#.2Fiso)
*   [3 FAQ](#FAQ)
    *   [3.1 Como fazer downgrade de um pacote](#Como_fazer_downgrade_de_um_pacote)
    *   [3.2 Como restaurar todos os pacotes para uma data específica](#Como_restaurar_todos_os_pacotes_para_uma_data_espec.C3.ADfica)
*   [4 História](#Hist.C3.B3ria)

## Localização

O Arch Linux Archive está disponível em [https://archive.archlinux.org/](https://archive.archlinux.org/).

O [código fonte](https://github.com/seblu/archivetools) também está disponível para configurar seu próprio espelho.

## Diretórios

O **Archive** é dividido em 3 diretórios principais detalhados abaixo.

```
├── iso
├── packages
└── repos

```

### /repos

O diretório [repos](https://archive.archlinux.org/repos) contém snapshots diários de espelho oficial organizado por data como o exemplo a seguir.

```
repos
├── 2013
│   ├── 08
│   │   └── 31
│   │       ├── community
│   │       ├── community-staging
│   │       ├── community-testing
│   │       ├── core
│   │       ├── extra
│   │       ├── gnome-unstable
│   │       ├── kde-unstable
│   │       ├── lastsync
│   │       ├── multilib
│   │       ├── multilib-staging
│   │       ├── multilib-testing
│   │       ├── pool
│   │       ├── staging
│   │       └── testing
│   ├── 09
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │   ├── 21
│   │   └── 22
│   ├── 10
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │
│   ├── 11
│   └── 12
├── 2014
│   ├── 01
│   │   ├── 01
│   │   ├── 02
│   │   ├── ...
│   │
│   ├── 02
│   ├── 03
│   ├── ...
│   └── 09
│       ├── 01
│       ├── ...
│       └── 28
├── last
├── month
└── week

```

Nota: Os últimos 3 diretórios especiais (**last**, **week** and **month**) vinculam respectivamente ao último repositório sincronizado, para a última segunda-feira e para a primeira do mês atual.

### /packages

O diretório [packages](https://archive.archlinux.org/packages) contém todas as versões de cada pacote com suas assinaturas. Um diretório por pacote e diretórios de pacotes são agrupadas pela sua primeira letra.

```
├── packages
│   ├── a
│   │   ├── awesome
│   │   │   ├── awesome-3.5.0-1-i686.pkg.tar.xz
│   │   │   ├── awesome-3.5.0-1-i686.pkg.tar.xz.sig
│   │   │   ├── awesome-3.5.0-1-x86_64.pkg.tar.xz
│   │   │   ├── awesome-3.5.0-1-x86_64.pkg.tar.xz.sig
│   │   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz
│   │   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz.sig
│   │   │   ├── ...
│   │   │ 
│   │   ├── ...
│   │   ├── awstats
│   │   └── axel
│   │   
│   ├── b
│   ├── ...
│   └── z

```

Você pode usar o subdiretório mágico [.all](https://archive.archlinux.org/packages/.all) para acessar todos os pacotes pelo nome deles. Ele atua como um diretório plano contendo todas as versões de cada pacote.

```
├── packages
│   ├── .all
│   │   ├── awesome-3.5.1-1-i686.pkg.tar.xz
│   │   ├── ...
│   │   ├── zsh-5.0.2-3-i686.pkg.tar.xz
│   │   ├── zsh-5.0.2-4-i686.pkg.tar.xz
│   │   └── ...

```

Você pode baixar a lista de pacotes completos (existem mais de cem mil pacotes) como um índice compactado: [index.0.xz](https://archive.archlinux.org/packages/.all/index.0.xz).

 `$ curl https://archive.archlinux.org/packages/.all/index.0.xz | unxz` 
```
0ad-a14-1-i686
0ad-a14-1-x86_64
0ad-a14-2-i686
...
zziplib-0.13.62-1-x86_64
zziplib-0.13.62-2-i686
zziplib-0.13.62-2-x86_64
```

### /iso

O diretório [iso](https://archive.archlinux.org/iso) contém imagens ISO oficiais e tarballs bootstrap ordenados por data de lançamento.

```
├── 2014.09.03
├── 2014.10.01
├── 2014.11.01
├── 2014.12.01
├── 2015.07.01
├── 2015.08.01
├── 2015.09.01
└── 2017.04.01
    ├── arch
    ├── archlinux-2017.04.01-x86_64.iso
    ├── archlinux-2017.04.01-x86_64.iso.sig
    ├── archlinux-2017.04.01-x86_64.iso.torrent
    ├── archlinux-bootstrap-2017.04.01-x86_64.tar.gz
    ├── archlinux-bootstrap-2017.04.01-x86_64.tar.gz.sig
    ├── md5sums.txt
    └── sha1sums.txt

```

## FAQ

### Como fazer downgrade de um pacote

Encontre o pacote que deseja em [/packages](#.2Fpackages) e deixe o pacman buscá-lo para instalação. Por exemplo

```
# pacman -U https://archive.archlinux.org/packages/ ... *nomepacote*.pkg.tar.xz

```

Deixar o pacman buscá-lo irá baixar automaticamente o arquivo *.sig* separado do pacote e verificá-lo de acordo com as configurações `/etc/pacman.conf`.

Alternativamente, baixe e instale o pacote manualmente usando `pacman -U`.

Veja também [Fazendo downgrade de pacotes#Automação](/index.php/Fazendo_downgrade_de_pacotes#Automa.C3.A7.C3.A3o "Fazendo downgrade de pacotes") para as ferramentas que simplificam o processo.

### Como restaurar todos os pacotes para uma data específica

Para restaurar todos os pacotes em sua versão em uma data específica, digamos, 30 de março de 2014, você deve direcionar o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") para essa data, editando seu `/etc/pacman.conf` e use o seguinte diretiva do servidor:

```
[core]
SigLevel = PackageRequired
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

[extra]
SigLevel = PackageRequired
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

[community]
SigLevel = PackageRequired
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

```

ou substituindo seu `/etc/pacman.d/mirrorlist` com o seguinte conteúdo:

```
##                                                                              
## Arch Linux repository mirrorlist                                             
## Generated on 2042-01-01                                                      
##
Server=https://archive.archlinux.org/repos/2014/03/30/$repo/os/$arch

```

Então, atualize sua base de dados e force o downgrade:

```
# pacman -Syyuu

```

**Nota:** [Não é seguro](/index.php/Atualiza%C3%A7%C3%B5es_parciais "Atualizações parciais") misturar os espelhos Archive e os atualizados. No caso de uma falha de download, você acabará ficando com um pacote de *upstream* e você terá pacotes não da mesma época do resto do sistema.

## História

*   O ARM (*Archlinux Rollback Machine*) original foi fechado em 2013-08-18.[[1]](https://bbs.archlinux.org/viewtopic.php?pid=1313360#p1313360)
*   O novo está hospedado em [seblu.net](http://seblu.net) desde 2013-08-31.
*   Nova URL e fechamento a hierarquia antiga do ARM em 2015-10-13\. Um novo software, [agetpkg-git](https://aur.archlinux.org/packages/agetpkg-git/), foi introduzido.
*   Movido para [archive.archlinux.org](https://archive.archlinux.org) em 2015-12-19.[[2]](https://lists.archlinux.org/pipermail/arch-dev-public/2015-December/027635.html)