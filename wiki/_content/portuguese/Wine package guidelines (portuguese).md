**[Diretrizes de criação de pacotes](/index.php/Criando_pacotes "Criando pacotes")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Muitos programas do Windows ainda podem ser úteis no Linux e, portanto, podemos querer ter um pacote para eles. As diferenças entre os dois sistemas operacionais tornam essa tarefa um pouco complexa. Nesta diretriz, falaremos sobre binários do Win32, já que os projetos em que a origem está disponível geralmente são portados para o Linux.

## Contents

*   [1 Coisas para verificar imediatamente](#Coisas_para_verificar_imediatamente)
    *   [1.1 Licença](#Licen.C3.A7a)
    *   [1.2 Installador](#Installador)
    *   [1.3 Portabilidade e limpeza](#Portabilidade_e_limpeza)
*   [2 A diretriz em resumo](#A_diretriz_em_resumo)
    *   [2.1 Instalando](#Instalando)
    *   [2.2 O script /usr/bin](#O_script_.2Fusr.2Fbin)
    *   [2.3 UnionFsFuse](#UnionFsFuse)
*   [3 Um exemplo](#Um_exemplo)
*   [4 Gecko e Mono](#Gecko_e_Mono)

## Coisas para verificar imediatamente

*   Licença: a licença permite que o programa seja reempacotada?
*   Instalador: é possível instalar o programa silenciosamente? Melhor ainda, existe uma versão sem instalador?
*   Portabilidade e limpeza: é o programa portátil? É limpo?

Aqui dizemos que um programa é portátil se *nunca* escreve no registro ou fora de seu diretório; dizemos que um programa é limpo se nunca escreve em seu diretório, mas pode gravar suas configurações na pasta do usuário. Um programa também pode ser ambos (por exemplo, nunca escreve configurações) ou nem (por exemplo, ele escreve em seu diretório, escreve em volta, escreve no registro ...)

### Licença

Geralmente, as licenças estão em um arquivo de texto no diretório de instalação. Se você não conseguir encontrá-los, tente seguir as telas durante a instalação. Se nada for dito sobre reempacotamento, vá em frente. O autor não se importa. Caso contrário, a licença geralmente não permite a remoção de arquivos ou não permite a reempacotamento. No primeiro caso, apenas tenha cuidado para que o processo [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") não perca nenhum arquivo, você pode excluir arquivos desnecessários (por exemplo, desinstaladores) na fase `post_install`; no último caso, todo o processo de instalação deve ser feito na fase `post_install`. A fase `build` será apenas para copiar os arquivos de instalação.

### Installador

É muito mais fácil trabalhar com arquivos compactados como `.zip` do que com instaladores do Windows. Se você não tiver escolha, pois o autor insiste em distribuir seu programa com um instalador, pesquise na Internet se é possível instalar silenciosamente o software. [MSFN](http://unattended.msfn.org/unattended.xp/page/list/switch/) geralmente é um bom lugar para pesquisar. Se não conseguir encontrar uma maneira, tente abrir o instalador com diferentes [utilitários de desempacotamento](/index.php/Nonfree_applications_package_guidelines#Unpacking "Nonfree applications package guidelines"); pode funcionar.

### Portabilidade e limpeza

Um programa portátil não precisa de seu próprio sistema de arquivos em [Wine](/index.php/Wine "Wine"), portanto, verifique em [Portable Freeware](http://www.portablefreeware.com) se o programa que você está empacotando é portátil.

## A diretriz em resumo

A ideia por trás do empacotamento de um programa do Windows é usar os arquivos do programa como meros dados que o Wine interpretará, assim como o bytecode da JVM e do Java.

Então vamos instalar o programa em `/usr/share/"$pkgname"` e o programa irá escrever tudo o que precisa em `"$HOME"/."$pkgname"`. Tudo será preparado por um pequeno script salvo em `/usr/bin/"$pkgname"` que irá criar a pasta, prepará-la, se necessário, e finalmente iniciar o programa.

Nas próximas seções, nós vamos falar sobre cada etapa.

Desta forma, cada usuário terá suas próprias configurações e suas decisões não incomodarão outros usuários.

### Instalando

Se o programa não tiver instalador, a instalação é uma mera descompactação de um arquivo; descompacte-o em `"$pkgdir"/usr/share/$pkgname`, certificando-se de que as permissões estejam corretas. Esses comandos servirão:

```
$ find "$pkgdir"/usr/share -type f -exec chmod 644 "{}" \;
$ find "$pkgdir"/usr/share -type d -exec chmod 755 "{}" \;

```

Se o programa não puder ser instalado da maneira mais fácil, você precisará criar um ambiente Wine:

```
$ install -m755 -d "$srcdir"/tmp "$srcdir"/tmp/env "$srcdir"/tmp/local
$ export WINEPREFIX="$srcdir"/tmp/env
$ export XDG_DATA_HOME="$srcdir"/tmp/local
$ wine "$srcdir"/installer.exe /silentoptions

```

Nós ainda não discutimos a portabilidade, mas se o seu programa não precisa das chaves de registro que ele modificou, você pode simplesmente copiar o diretório do:

```
"$srcdir"/tmp/env/drive_c/Program\ Files/nomeprograma

```

Caso contrário, você precisará copiar todos os arquivos de registro também e, eventualmente, os arquivos instalados pelo programa. O `"$srcdir"/tmp/local` conterá ícones de menu e arquivos da área de trabalho, você pode querer copiá-los no pacote. Se não existe uma maneira de instalar o programa silenciosamente ... Talvez você possa criar um arquivo `.tar.gz` e enviá-lo para algum lugar? Se nada for possível, force o usuário a seguir o instalador e espere que ele não estrague a instalação, faça algumas verificações antes de copiar cegamente uma pasta que pode não existir (por exemplo, o usuário pressionou 'Cancelar').

### O script /usr/bin

Este script prepara a pasta de configurações e inicia o programa. Se o seu programa for portátil, ficará assim:

```
#!/bin/bash
unset WINEPREFIX
if [ ! -d "$HOME"/.nomeprograma ] ; then
   mkdir -p "$HOME"/.nomeprograma
   #prepare o ambiente aqui
fi
WINEDEBUG=-all wine "$HOME"/.nomeprograma/nomeprograma "$@"

```

Se for limpo, ele vai se parecer com isso:

```
#!/bin/bash
export WINEPREFIX="$HOME"/.nomeprograma/wine
if [ ! -d "$HOME"/.nomeprograma ] ; then
   mkdir -p "$HOME"/.nomeprograma/wine
   wineboot -u
   #copie o arquivo de registro se necessário
fi
WINEDEBUG=-all wine /usr/share/nomeprograma "$@"

```

Como você pode ver, no segundo caso não há preparação do ambiente. Na verdade, um aplicativo limpo será iniciado diretamente de `/usr/share`, pois não precisará gravar em sua pasta, portanto, suas configurações serão gravadas em algum lugar no sistema de arquivos emulado.

Se o aplicativo não for nem limpo nem portátil, as duas ideias devem ser combinadas.

Se o aplicativo não gravar configurações, ignore o `if` e inicie-o em `/usr/share`.

A tarefa de preparar o ambiente pode diferir muito entre os aplicativos, mas siga estas regras práticas: Se o programa:

*   só precisa ler um arquivo, faça um link simbólico para ele.
*   precisa escrever em um arquivo, copie-o.
*   não usa um arquivo, ignore-o.

É claro, o mínimo é só iniciar `WINEDEBUG=-all wine /usr/share/nomeprograma "$@"`.

Geralmente, o ambiente será feito por link simbólico entre o diretório `"$HOME"/.*nomeprograma*` e os arquivos `/usr/share/*nomeprograma*`. Mas já que alguns programas do Windows são muito inconstantes em relação aos seus caminhos, você pode precisar vincular diretamente no diretório `"$HOME"/.*nomeprograma*/wine/drive_c/Program\ Files/*nomeprograma*`.

Claro que essas são apenas ideias para integrar aplicativos Win32 no ambiente Linux, não esqueça sua inteligência e bom senso.

Como exemplo, [μTorrent](https://en.wikipedia.org/wiki/pt:%CE%BCTorrent "wikipedia:pt:μTorrent") é por padrão um aplicativo limpo, mas com uma etapa fácil pode ser usado como um arquivo portátil. Já que é um único arquivo e é bem pequeno criando seu ambiente do Wine (aproximadamente 5MB) é provavelmente um exagero. É melhor criar um link simbólico para o executável, criar o **settings.dat** vazio para poder usá-lo no diretório `$HOME/.utorrent`. Com a vantagem de apenas visitar a pasta `.utorrent`, um usuário pode ver uma cópia dos arquivos `.torrent` que baixou.

### UnionFsFuse

Você pode considerar o uso do programa [UnionFsFuse](http://podgorny.cz/moin/UnionFsFuse) disponível nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") como [unionfs-fuse](https://www.archlinux.org/packages/?name=unionfs-fuse)). UnionFsFuse permite manter o diretório base no `/usr/share` e colocar uma cópia dos arquivos do aplicativo necessários para escrever dentro de `$HOME/.nomeprograma` quase automaticamente.

Usar UnionFsFuse significa uma dependência adicional e requer o módulo fuse, o que nem todos os usuários podem carregar. No entanto, pode valer a pena se o aplicativo precisar de muitos links simbólicos ou se não estiver claro exatamente o que precisa ser escrito. Apenas certifique-se de montar e desmontar os UnionFs corretamente.

## Um exemplo

Vamos fazer um pacote para o [eMule](http://www.emule-project.net/). De acordo com [Portable Freeware](http://www.portablefreeware.com/?q=emule), eMule não é completamente portátil, pois ele escreve algumas chaves (inúteis) no registro.

Por outro lado, ele também não é limpo já que ele escreve seus arquivos de configuração e coloca seus downloads em sua pasta de instalação.

Por sorte, há uma [versão sem instalador disponível](http://prdownloads.sourceforge.net/emule/eMule0.49b.zip).

Então, nós fazemos nosso [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"); a única dependência é o [wine](https://www.archlinux.org/packages/?name=wine). O `md5sums` deve ser adicionado.

```
# Maintainer: Você <seuemail>
pkgname=emule
pkgver=0.49b
pkgrel=1
pkgdesc="One of the biggest and most reliable peer-to-peer file sharing
clients around the world."
arch=(i686 x86_64)
url="http://www.emule-project.net"
license=('GPL')
depends=()
depends=(wine)
makedepends=(unzip)
source=(emule http://prdownloads.sourceforge.net/emule/eMule$pkgver.zip)
noextract=()
options=(!strip)

build() {
  rm -f src/eMule"$pkgver"/license* #It is GPL

  install -d -m755 pkg/usr/share/emule
  cp -ra src/eMule"$pkgver"/* pkg/usr/share/emule
  find pkg/usr/share/emule -type d -exec chmod 755 "{}" \;
  find pkg/usr/share/emule -type f -exec chmod 644 "{}" \;

  install -d -m755 pkg/usr/bin
  install -m755 emule pkg/usr/bin 
}

```

Agora, nós fazemos nosso arquivo **emule**, que, de com o `build`, será copiado e tornado executável em `/usr/bin`.

```
#!/bin/bash
export WINEARCH=win32 WINEPREFIX="$HOME/.emule/wine"

if [ ! -d "$HOME"/.emule ] ; then
  mkdir -p "$HOME"/.emule/wine || exit 1
  #Cada usuário terá suas config, nós copiamos o arquivo padrão
  #já que o emule precisa escrevê-lo.
  cp -r /usr/share/emule/config "$HOME"/.emule || exit 1
  #Nós criamos links simbólicos para os arquivos que o emule precisa ler para funcionar
  ln -s /usr/share/emule/emule.exe "$HOME"/.emule/emule || exit 1
  ln -s -T /usr/share/emule/lang "$HOME"/.emule/lang || exit 1
  ln -s -T /usr/share/emule/webserver "$HOME"/.emule/webserver || exit 1
fi

wine "$HOME"/.emule/emule "$@"

```

Se você quiser ser mais preciso, você pode adicionar uma mensagem no arquivo `.install` dizendo ao usuário que ele deve desabilitar o histórico de busca, já que o wine bagunça aquele menu. Você pode até fornecer um arquivo de configuração padrão com as melhores configurações. E é isso ... execute `$ makepkg`, verifique a pasta do pacote para ter certeza e instale-o.

## Gecko e Mono

A menos que você saiba com certeza que o software requer o navegador do tempo de execução do .NET (pacotes [wine_gecko](https://www.archlinux.org/packages/?name=wine_gecko) e [wine-mono](https://www.archlinux.org/packages/?name=wine-mono) nos repositórios oficiais), os prompts padrão de instalação do wine para Gecko/Mono são indesejáveis.

Para desabilitar renderização HTML, suporte a bytecode e diálogos, você precisa usar um dlloverride em seu script. Para Gecko:

```
export WINEDLLOVERRIDES="mshtml="

```

Para Mono:

```
export WINEDLLOVERRIDES="mscoree="

```

Para ambos:

```
export WINEDLLOVERRIDES="mscoree,mshtml="

```

Você também pode desabilitá-los via `winecfg`: basta definir mscoree/mshtml para desabilitar.