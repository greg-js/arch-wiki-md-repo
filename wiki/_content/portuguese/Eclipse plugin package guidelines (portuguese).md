**[Diretrizes de criação de pacotes](/index.php/Criando_pacotes "Criando pacotes")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Há muitas maneiras de instalar os plugins do [Eclipse](/index.php/Eclipse "Eclipse"), especialmente desde a introdução do diretório *dropins* no Eclipse 3.4, mas alguns deles são confusos, e ter uma maneira padronizada e consistente de empacotamento é muito importante levar a uma estrutura de sistema limpa. Não é fácil, no entanto, conseguir isso sem que o empacotador saiba todos os detalhes sobre como os plug-ins do Eclipse funcionam. Esta página tem como objetivo definir uma estrutura padrão e simples para [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") de plugins do Eclipse, para que a estrutura do sistema de arquivos permaneça consistente entre todos os plugins sem que o empacotador seja iniciado novamente para cada novo pacote.

## Contents

*   [1 Estrutura e instalação de plugins do Eclipse](#Estrutura_e_instala.C3.A7.C3.A3o_de_plugins_do_Eclipse)
*   [2 Empacotamento](#Empacotamento)
    *   [2.1 Exemplo de PKGBUILD](#Exemplo_de_PKGBUILD)
    *   [2.2 Como personalizar a compilação](#Como_personalizar_a_compila.C3.A7.C3.A3o)
    *   [2.3 Revisão aprofundada do PKGBUILD](#Revis.C3.A3o_aprofundada_do_PKGBUILD)
        *   [2.3.1 Nomenclatura de pacote](#Nomenclatura_de_pacote)
        *   [2.3.2 Arquivos](#Arquivos)
            *   [2.3.2.1 Extração](#Extra.C3.A7.C3.A3o)
            *   [2.3.2.2 Localizações](#Localiza.C3.A7.C3.B5es)
        *   [2.3.3 A função build()](#A_fun.C3.A7.C3.A3o_build.28.29)
*   [3 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)

## Estrutura e instalação de plugins do Eclipse

O plug-in típico do Eclipse contém dois diretórios, `features` e `plugins` e, desde o Eclipse 3.3, eles podem ser colocados apenas em `/usr/lib/eclipse/`. O conteúdo desses dois diretórios pode ser mesclado com o de outros plugins, e criou uma confusão e tornou a estrutura difícil de gerenciar. Também foi muito difícil dizer rapidamente qual pacote continha qual arquivo.

Ainda há suporte a esse método de instalação no Eclipse 3.4, mas o preferido agora está usando o diretório `/usr/lib/eclipse/dropins/`. Dentro deste diretório pode-se viver um número ilimitado de subdiretórios, cada um contendo seus próprios subdiretórios `features` e `plugins`. Isso permite manter uma estrutura limpa e arrumada e deve ser o modo de empacotamento padrão.

## Empacotamento

### Exemplo de PKGBUILD

Arquivo está um exemplo, nós vamos detalhar como personalizá-lo.

 `PKGBUILD-eclipse.proto` 
```
pkgname=eclipse-mylyn
pkgver=3.0.3
pkgrel=1
pkgdesc="A task-focused interface for Eclipse"
arch=('any')
url="https://eclipse.org/mylyn/"
license=('EPL')
depends=('eclipse')
optdepends=('bugzilla: ticketing support')
source=(https://download.eclipse.org/tools/mylyn/update/mylyn-${pkgver}-e3.4.zip)
sha512sums=('aa6289046df4c254567010b30706cc9cb0a1355e9634adcb2052127030d2640f399caf20fce10e8b4fab5885da29057ab9117af42472bcc1645dcf9881f84236')

prepare() {
  # remove features and plug-ins containing sources
  rm -f features/*.source_*
  rm -f plugins/*.source_*
  # remove gz files
  rm -f plugins/*.pack.gz
}

package() {
  _dest="${pkgdir}/usr/lib/eclipse/dropins/${pkgname/eclipse-}/eclipse"

  # Features
  find features -type f | while read -r _feature ; do
    if [[ "${_feature}" =~ (.*\.jar$) ]] ; then
      install -dm755 "${_dest}/${_feature%*.jar}"
      cd "${_dest}/${_feature/.jar}"
      # extract features (otherwise they are not visible in about dialog)
      jar xf "${srcdir}/${_feature}" || return 1
    else
      install -Dm644 "${_feature}" "${_dest}/${_feature}"
    fi
  done

  # Plugins
  find plugins -type f | while read -r _plugin ; do
    install -Dm644 "${_plugin}" "${_dest}/${_plugin}"
  done
}

```

### Como personalizar a compilação

A variável principal que precisa ser personalizada é o `pkgname`. Se você estiver empacotando um plug-in típico, essa é a única coisa que você precisa fazer: a maioria dos plug-ins é distribuída em arquivos zip que contêm apenas os dois subdiretórios `features` e `plugins`. Portanto, se você estiver empacotando o plug-in `foo` e o arquivo de origem contiver apenas `features` e `plugins`, você só precisará alterar `pkgname` para `eclipse-foo` e você está pronto.

Continue lendo para ir aos componentes internos do PKGBUILD, que ajudam a entender como configurar a compilação para todos os outros casos.

### Revisão aprofundada do PKGBUILD

#### Nomenclatura de pacote

Os pacotes devem ser denominados `eclipse-*nomeplugin*`, para que sejam reconhecidos como pacotes relacionados ao Eclipse e seja fácil extrair o nome do plug-in com uma substituição de shell simples como `${pkgname/eclipse-}`, não tendo que recorrer a uma variável desnecessária `${_realname}`. O nome do plugin é necessário para arrumar tudo durante a instalação e evitar conflitos.

#### Arquivos

##### Extração

Alguns plugins precisam que os recursos sejam extraídos dos arquivos jar. O utilitário `jar`, já incluído no JRE, é usado para fazer isso. No entanto, `jar` não pode extrair para diretórios diferentes do atual: isso significa que, após cada criação de diretório, é necessário `cd` dentro dele antes de extrair. A variável `${_dest}` é usada neste contexto para melhorar a legibilidade e a limpeza do PKGBUILD.

##### Localizações

Como dissemos, os archives de origem fornecem dois diretórios, `features` e `plugins`, cada um com arquivos jar. A estrutura de dropins preferida deve ficar assim:

```
/usr/lib/eclipse/dropins/pluginname/eclipse/features/recurso1/...
/usr/lib/eclipse/dropins/pluginname/eclipse/features/recurso2/...
/usr/lib/eclipse/dropins/pluginname/eclipse/plugins/plugin1.jar
/usr/lib/eclipse/dropins/pluginname/eclipse/plugins/plugin2.jar

```

Esta estrutura permite misturar diferentes versões de bibliotecas que podem ser necessárias por diferentes plugins, sendo claro sobre qual pacote possui o quê. Ele também evitará conflitos caso pacotes diferentes forneçam a mesma biblioteca. A única alternativa seria dividir cada pacote de suas bibliotecas, com toda a confusão extra que requer, e nem mesmo seria garantido que funcionasse por causa dos pacotes que precisavam de versões de bibliotecas mais antigas.

Os recursos devem ser descompactados do arquivo *jar*, pois o Eclipse não os detectará de outra forma, e toda a instalação do plug-in não funcionará. Isso acontece porque o Eclipse trata os sites de atualização e as instalações locais de forma diferente (não pergunte por que, apenas faz).

#### A função build()

A primeira coisa a ser notada é o comando `cd ${srcdir}`. Geralmente os arquivos fonte extraem as pastas `features` e `plugins` diretamente sob `${srcdir}`, mas nem sempre é esse o caso. De qualquer forma, para a maioria dos plugins não padrão *(de fato)*, esta é a única linha que precisa ser alterada.

Alguns recursos lançados incluem suas fontes também. Para uma versão normal, essas fontes não são necessárias e podem ser removidas. Além disso, os mesmos recursos incluem arquivos `*.pack.gz`, que contêm os mesmos arquivos em comparação com os arquivos jar. Então, esses arquivos podem ser removidos também.

A próxima é a seção `features`. Ele cria os diretórios necessários, um para cada arquivo jar, e extrai o jar no diretório correspondente. Da mesma forma, a seção `plugins` instala os arquivos jar em seus diretórios. Um ciclo de tempo é usado para evitar arquivos de nome engraçado.

## Solução de problemas

*   Algumas vezes, a limpeza do Eclipse ajuda a corrigir alguns problemas: `$ eclipse -clean` 
*   Se novos plug-ins instalados não aparecerem no Eclipse, tente com um diretório limpo `~/.eclipse`, por exemplo, renomeando o existente. Esteja ciente de que isso, é claro, tornará todos os plugins instalados pelo usuário via Marketplace indisponíveis.