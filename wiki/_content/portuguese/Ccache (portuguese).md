**Status de tradução:** Esse artigo é uma tradução de [Ccache](/index.php/Ccache "Ccache"). Data da última tradução: 2018-09-21\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Ccache&diff=0&oldid=542513) na versão em inglês.

Artigos relacionados

*   [Makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)")
*   [Distcc](/index.php/Distcc "Distcc")

[ccache](http://ccache.samba.org/) é uma ferramenta para o compilador gcc usada para compilar o mesmo programa repetidas vezes com pouco tempo de inatividade. Enquanto pode levar alguns segundos mais para compilar um programa na primeira vez com o *ccache*, compilações subsequentes serão muito, muito mais rápidos.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Configuração](#Configura.C3.A7.C3.A3o)
    *   [2.1 Habilitar ccache para makepkg](#Habilitar_ccache_para_makepkg)
    *   [2.2 Habilitar para linha de comando](#Habilitar_para_linha_de_comando)
    *   [2.3 Habilitar com colorgcc](#Habilitar_com_colorgcc)
*   [3 Diversos](#Diversos)
    *   [3.1 Alterar o diretório do cache](#Alterar_o_diret.C3.B3rio_do_cache)
    *   [3.2 Configurar o tamanho máximo do cache](#Configurar_o_tamanho_m.C3.A1ximo_do_cache)
    *   [3.3 Desabilitar o cacho via ambiente](#Desabilitar_o_cacho_via_ambiente)
    *   [3.4 CLI](#CLI)
    *   [3.5 makechrootpkg](#makechrootpkg)
*   [4 Advertência](#Advert.C3.AAncia)
*   [5 Veja também](#Veja_tamb.C3.A9m)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [ccache](https://www.archlinux.org/packages/?name=ccache).

## Configuração

O comportamento padrão pode ser sobrescrito pelos arquivos de configuração. Prioridade das configurações é a seguinte (sendo 1 o mais alto):

1.  Variáveis de ambiente
2.  Arquivo de configuração específico do cache (`$HOME/.ccache/ccache.conf`)
3.  Arquivo de configuração para todo sistema (`/etc/ccache.conf`)

Veja [ccache(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ccache.1) para detalhes.

### Habilitar ccache para makepkg

Para habilitar o *ccache* ao usar [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"), edite `/etc/makepkg.conf`. Em `BUILDENV`, descomente `ccache` (remova a marca de exclamação) para habilitar cache. Por exemplo:

 `/etc/makepkg.conf`  `BUILDENV=(fakeroot !distcc color **ccache** check !sign)` 

### Habilitar para linha de comando

Se você está compilando seu código a partir da linha de comando, e não compilando pacotes, então você ainda desejará usar *ccache* para ajudar a acelerar as coisas.

Para isso, você precisará alterar seu `$PATH` para incluir os binários do *ccache* antes do caminho de seu compilador:

```
$ export PATH="/usr/lib/ccache/bin/:$PATH"

```

Você pode querer definir essa linha como [variável de ambiente](/index.php/Vari%C3%A1vel_de_ambiente "Variável de ambiente") para uso regular.

**Nota:** Isso inevitavelmente habilitará *ccache* para *makepkg* da mesma forma que se fosse chamado com esse PATH.

### Habilitar com colorgcc

Já que [colorgcc](https://www.archlinux.org/packages/?name=colorgcc) também um *wrapper* de compilador, precisa-se ter alguns cuidados para garantir que cada wrapper é chamado na sequência correta.

```
export PATH="/usr/lib/colorgcc/bin/:$PATH"    # De acordo com a instalação usual de colorgcc, deixe inalterado (não adicione ccache)
export CCACHE_PATH="/usr/bin"                 # Fale para o ccache usar apenas compiladores aqui

```

Então, o *colorgcc* precisa ser informado para chamar *ccache* em vez do compilador real. Edite `/etc/colorgcc/colorgccrc` e altere os caminhos de `/usr/bin` para `/usr/lib/ccache/bin` para todos os compiladores em `/usr/lib/ccache/bin`:

 `/etc/colorgcc/colorgccrc` 
```
g++: /usr/lib/ccache/bin/g++
gcc: /usr/lib/ccache/bin/gcc
c++: /usr/lib/ccache/bin/g++
cc: /usr/lib/ccache/bin/cc
g77:/usr/bin/g77
f77:/usr/bin/g77
gcj:/usr/bin/gcj

```

## Diversos

### Alterar o diretório do cache

Você pode querer mover o diretório cache para uma localização mais rápida do que o diretório `~/.ccache` padrão, como um SSD ou um [ramdisk](/index.php/Ramdisk "Ramdisk").

Para alterar a localização do cacho apenas no shell atual:

```
$ export CCACHE_DIR=/ramdisk/ccache

```

Ou para alterar a localização por padrão:

 `/home/*user*/.ccache/ccache.conf`  `cache_dir = /ramdisk/ccache` 

### Configurar o tamanho máximo do cache

O valor padrão é 5 gigabyte, porém é possível usar um valor menor ou até mesmo mais alto:

```
$ ccache --set-config=max_size=2.0G

```

### Desabilitar o cacho via ambiente

Se você deseja desabilitar o *ccache* apenas no shell atual:

```
$ export CCACHE_DISABLE=1

```

### CLI

Você pode usar o utilitário de linha de comando *ccache* para mostrar um resumo de estatística:

```
$ ccache -s

```

ou limpar o cache completamente:

```
$ ccache -C

```

### makechrootpkg

Também é possível usar o *ccache* com *makechrootpkg* do pacote [devtools](https://www.archlinux.org/packages/?name=devtools). Para reter o cache quando o chroot é limpado pelo *makechrootpkg*, a opção `-d` pode ser usada para vincular o diretório do cache do sistema regular para o chroot, ex.:

```
$ mkdir /path/of/chroot/ccache
$ makechrootpkg -d /caminho/para/cache/:/ccache -r /caminho/do/chroot -- CCACHE_DIR=/ccache

```

Então, *ccache* pode ser configurado para o chroot na mesma forma como explicado acima para o sistema comum.

## Advertência

*ccache* é efetivo **somente** quando compilar fontes **exatamente idênticas**. (mais especificamente, fontes pré-processadas.)

Na comunidade Gentoo Linux, uma distro baseada em fontes, *ccache* tem sido notório por seu efeito placebo, falha de compilação (devido a objetos indesejados), etc. O Gentoo exige que seja desligado o *ccache* antes de relatar falha de compilação. Veja a [seção ccache](https://wiki.gentoo.org/wiki/Handbook:Parts/Working/Features#Caching_compilation_objects) no Manual do Gentoo Linux, e [a publicação de blog](https://flameeyes.blog/2008/06/21/debunking-ccache-myths/) intitulado "Debunking ccache myths" por Diego Pettenò, um ex-desenvolvedor Gentoo.

## Veja também

*   [manual do ccache](http://ccache.samba.org/manual.html)