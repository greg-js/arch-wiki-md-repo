**Status de tradução:** Esse artigo é uma tradução de [GNOME package guidelines](/index.php/GNOME_package_guidelines "GNOME package guidelines"). Data da última tradução: 2018-11-23\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=GNOME_package_guidelines&diff=0&oldid=554280) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Os pacotes do [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)") no Arch Linux segue, um certo esquema.

## Contents

*   [1 URL fonte](#URL_fonte)
    *   [1.1 Usando tarball de lançamento](#Usando_tarball_de_lançamento)
    *   [1.2 Usando um commit do repositório Git](#Usando_um_commit_do_repositório_Git)
*   [2 Compilando com meson](#Compilando_com_meson)
*   [3 GConf schemas](#GConf_schemas)
*   [4 GSettings schemas](#GSettings_schemas)
*   [5 Documentação do Scrollkeeper](#Documentação_do_Scrollkeeper)
*   [6 Cache de ícones do GTK](#Cache_de_ícones_do_GTK)
*   [7 Arquivos .desktop](#Arquivos_.desktop)
*   [8 Arquivos .install](#Arquivos_.install)

## URL fonte

Esse tópico contém as URLs fonte mais comumente usadas pelos pacotes GNOME nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais") e no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"). Para exemplos, pesquise por pacotes GNOME nos repositórios oficiais[[1]](https://www.archlinux.org/packages/?q=gnome) e no AUR[[2]](https://aur.archlinux.org/packages/?K=gnome)

### Usando tarball de lançamento

Ao baixar um tarball de lançamento, você pode obtê-lo de [https://download.gnome.org](https://download.gnome.org) usando o seguinte vetor fonte:

```
source=("https://download.gnome.org/sources/$pkgname/${pkgver%.*}/$pkgname-$pkgver.tar.xz")

```

sendo que *${pkgver%.*}* retorna a versão de pacote *maior*.*menor*, removendo o sufixo do `pkgver` (que é a versão de pacote *micro*). Por exemplo, se *pkgver=3.28.0*, então *${pkgver%.*}* retornaria *3.28*.

### Usando um commit do repositório Git

Uma outra prática comum é usar como fonte um commit específico de um repositório git de código fonte do software GNOME. Isso não se classifica como pacote VCS porque o recurso do Pacman de definir um commit específico[[3]](https://www.archlinux.org/pacman/PKGBUILD.5.html#_using_vcs_sources_a_id_vcs_a) faz o PKGBUILD não seguir os últimos commits de desenvolvimento nem atualizar o campo `pkgver`, em vez disso, usando o fonte do hash de commit especificado.

Veja um modelo abaixo:

 `PKGBUILD` 
```
makedepends=(git)
commit=*hash_de_um_commit* 
source=("git+https://gitlab.gnome.org/GNOME/$pkgname.git#commit=$_commit")
md5sums=('SKIP')

pkgver() {
  cd $pkgname
  git describe --tags | sed 's/-/+/g'
}
```

Substitua *hash_de_um_commit* com a hash do commit Git desejado.

Note que já que o fonte é baixado com *git*, então [git](https://www.archlinux.org/packages/?name=git) deve estar no `makedepends` e somas de verificação devem ser definidas para *SKIP*, assim como ocorreria com qualquer outro pacote VCS. O uso da função `pkgver()` é altamente recomendado, de forma que defina o `pkgver` adequadamente para o hash de commit fornecido.

**Note:** GNOME já usou [https://git.gnome.org](https://git.gnome.org), mas então migrou para o [https://gitlab.gnome.org](https://gitlab.gnome.org)[[4]](https://www.gnome.org/news/2018/05/gnome-moves-to-gitlab-2/). Links antigos devem ser redirecionados automaticamente para o novo domínio gitlab.gnome.org, mas pode ser interessante atualizar manualmente a URL do seu fonte.

## Compilando com meson

Muitos softwares do GNOME migraram o sistema de compilação para o [Meson](https://mesonbuild.com/), consequentemente descartando o suporte a [GNU Autotools](/index.php/Sistema_de_Compila%C3%A7%C3%A3o_do_GNU "Sistema de Compilação do GNU"). Isso significa que você usará *./configure* e *make* neste caso.

Para compilar usando o Meson, adicione o pacote [meson](https://www.archlinux.org/packages/?name=meson) para [makedepends](/index.php/Makedepends_(Portugu%C3%AAs) "Makedepends (Português)") e execute seu comando *meson*, incluindo opcionalmente todas as opções desejadas suportadas pelo software alvo. O pacote [ninja](https://www.archlinux.org/packages/?name=ninja) também será usado neste sistema de compilação, mas é uma dependência do [meson](https://www.archlinux.org/packages/?name=meson), então você não precisa incluí-lo no vetor *makedepends*.

As funções [build()](/index.php/Criando_pacotes#build() "Criando pacotes"), [check()](/index.php/Criando_pacotes#check() "Criando pacotes") e [package()](/index.php/Criando_pacotes#package() "Criando pacotes") devem ser parecer com:

 `PKGBUILD` 
```
makedepends=(meson)

build() {
  meson --prefix /usr --buildtype=plain *fonte* *build*
  ninja -C *build*
}

check() {
  ninja -C *build* check
}

package() {
  DESTDIR="$pkgdir" ninja -C *build* install
}
```

sendo que

*   *fonte* é o diretório contendo o código-fonte extraído como, por exemplo, *$pkgname* ou *$pkgname-$pkgver*; e
*   *build* é o diretório que conterá os arquivos binários a serem instalados. Normalmente o nome de diretório "build" é usado, então você pode querer mantê-lo para padronização, mas você pode renomeá-lo para o que mais lhe agradar.

**Nota:**

*   Alguns softwares não suportam a chamada de *meson* de fora do diretório raiz do código-fonte. Se este for o seu caso, adapte o bloco de código acima simplesmente adicionando `cd *fonte*` ao início das três funções acima, e também alterando a linha de comando *meson* acima para `meson . *build*`.
*   Se o software não tiver regras de teste definidas (caso em que o bloco de código acima falharia para construir o pacote), remova/comente a toda a função *check()*.

**Dica:** Para alternar uma opção de compilação no *meson*, anexe os sinalizadores `-D*opção=valor*` à linha de comando do *meson*, em que *opção* é uma opção suportada para o software de destino que você está compilando, e *valor* é um valor válido para a *opção* fornecida. Então, por exemplo, se o software tem uma opção *gtk_doc* como *false* por padrão e você quer habilitá-la, acrescente `-Dgtk_doc=true` à linha de comando do *meson*. Leia os arquivos `meson.build` e `meson_options.txt` no diretório-raiz do código-fonte para encontrar as opções disponíveis.

## GConf schemas

Alguns pacotes do GNOME instalam [schemas do GConf](https://en.wikipedia.org/wiki/pt:GConf#Schemas "wikipedia:pt:GConf"), apesar de muitos outros já terem migrados para GSettings. Aqueles pacotes devem depender de [gconf](https://www.archlinux.org/packages/?name=gconf).

Schemas do Gconf são instalados na base de dados GConf do sistema, que deve ser evitado. Alguns pacotes fornecem uma opção `--disable-schemas-install` para o **./configure**, que dificilmente funciona. Porém, gconftool-2 tem uma variável chamada `GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL` a qual você pode definir para dizer ao gconftool-2 para não atualizar qualquer base de dados.

Ao criar pacotes que instalam arquivos schemas de GConf, use

 `make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR=${pkgdir} install` 

para a etapa de instalação do pacote no PKGBUILD.

Não chame `gconfpkg` no arquivo .install, pois schemas do GConf são automaticamente instalados/removidos (na instalação/remoção de um pacote GNOME) via [hooks do *pacman*](/index.php/Pacman_(Portugu%C3%AAs)#Hooks "Pacman (Português)") desde o [gconf](https://www.archlinux.org/packages/?name=gconf)=3.2.6-4

## GSettings schemas

Os schemas de Gconf foram migrados para schemas do GSettings, então muitos aplicativos pode ser encontrados usando esse novo arquivo de schema. GSettings usa o dconf como backend, então todos os pacotes que contêm schemas de GSettings exigem [dconf](https://www.archlinux.org/packages/?name=dconf) como dependência. Quando um novo schema de GSettings é instalado no sistema, a base de dados do GSettings tem que ser recompilada, mas não durante o empacotamento.

Para evitar recompilação da base de dados do GSettings no empacotamento, use a opção `--disable-schemas-compile` para o **./configure**.

Não chame `glib-compile-schemas` no arquivo .install, pois as bases de dados de schemas do GSettings são recompilados automaticamente via [hooks do pacman](/index.php/Pacman_(Portugu%C3%AAs)#Hooks "Pacman (Português)") desde [glib2](https://www.archlinux.org/packages/?name=glib2)=2.48.0-2.

## Documentação do Scrollkeeper

A partir do GNOME 2.20, não há mais necessidade de lidar com scrollkeeper, pois [rarian](https://www.archlinux.org/packages/?name=rarian) lê seus arquivos OMF diretamente. Scrollkeeper-update é um link dos dias atuais. A única coisa que é necessário agora é acrescentar [gnome-doc-utils](https://www.archlinux.org/packages/?name=gnome-doc-utils)>=0.11.2 ao vetor `makedepends`.

Ele pode ser desabilitado usando a opção `--disable-scrollkeeper` no **./configure**.

## Cache de ícones do GTK

Alguns ícones de instalação de pacotes no tema do ícone do hicolor.

Não chame `gtk-update-icon-cache` no arquivo .install, pois o cache de ícone é atualizado via [hooks do pacman](/index.php/Pacman_(Portugu%C3%AAs)#Hooks "Pacman (Português)") desde [gtk-update-icon-cache](https://www.archlinux.org/packages/?name=gtk-update-icon-cache)=3.20.3-2\. Tais pacotes *não* devem depender de [gtk-update-icon-cache](https://www.archlinux.org/packages/?name=gtk-update-icon-cache), pois qualquer aplicativo que faz uso de caches de ícones gtk vai instalar o pacote com o hook e fará uma atualização de banco de dados completa e retroativa.

## Arquivos .desktop

Muitos pacotes instalam arquivos `.desktop` compatíveis com Freedesktop.org e registram entradas tipo MIME neles.

Não chame `update-desktop-database` no arquivo .install, pois a base de dados é atualizada automaticamente via [hooks do pacman](/index.php/Pacman_(Portugu%C3%AAs)#Hooks "Pacman (Português)") desde [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils)=0.22-2\. Tais pacotes *não* devem depender de [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils), pois qualquer desktop que faz uso de arquivos de desktop vai instalar o pacote com o hook e fará uma atualização de banco de dados completa e retroativa.

## Arquivos .install

Anteriormente, a maioria dos pacotes GNOME tinham um arquivo .install chamando comandos como `glib-compile-schemas`, `gtk-update-icon-cache` e `update-desktop-database` para instalar/atualizar cache local ou base de dados. Isso está obsoleto desde o pacman 5.0, que trouxe a implementação de [hooks](/index.php/Pacman_(Portugu%C3%AAs)#Hooks "Pacman (Português)") que chamam aqueles comandos automaticamente ao instalar o pacote.

Para evitar ser chamado duas vezes, os comandos supramencionados devem ser removidos do arquivo .install.