**[Diretrizes de criação de pacotes](/index.php/Criando_pacotes "Criando pacotes")**

* * *

[CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") –[OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Este documento define um padrão proposto para empacotar programas [Java](/index.php/Java_(Portugu%C3%AAs) "Java (Português)") no Arch Linux. Os programas Java são notoriamente difíceis de serem empacotados de forma limpa sem dependências sobrepostas. Este documento descreve uma maneira de remediar esta situação. Essas diretrizes são flexíveis para cobrir os vários cenários diferentes que surgem ao lidar com aplicativos Java.

## Contents

*   [1 Introdução](#Introdu.C3.A7.C3.A3o)
*   [2 Estrutura de um aplicativo Java típico](#Estrutura_de_um_aplicativo_Java_t.C3.ADpico)
*   [3 Empacotamento de Java no Arch Linux](#Empacotamento_de_Java_no_Arch_Linux)
    *   [3.1 Múltiplas implementações de API](#M.C3.BAltiplas_implementa.C3.A7.C3.B5es_de_API)
    *   [3.2 Exemplo de estrutura de diretórios](#Exemplo_de_estrutura_de_diret.C3.B3rios)
    *   [3.3 Dependências](#Depend.C3.AAncias)

## Introdução

Os empacotadores do Arch Linux não parecem conseguir chegar em um acordo sobre como lidar com pacotes Java. Vários métodos são usados em [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") s nos repositórios oficiais e não oficiais e no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"). Essas soluções incluem colocar toda a bagunça em `/opt` com scripts de shell em `/usr/bin` ou perfis colocados em `/etc/profile`. Outros são colocados em diretórios em `/usr/share` com scripts colocados em `/usr/bin`. Muitos adicionam arquivos desnecessários a `CLASSPATH` e `PATH` do sistema.

## Estrutura de um aplicativo Java típico

A maioria dos aplicativos desktop em Java tem uma estrutura similar. Eles são instalados a partir de um instalador independente do sistema (mas dependente do pacote). Isso geralmente instala tudo em um único diretório com subdiretórios chamados `bin`, `lib`, `jar`, `conf`, etc. Geralmente, existe um arquivo jar principal contendo as classes principais de executáveis. Um script shell geralmente é fornecido para executar a classe principal para que os usuários não tenham que chamar o interpretador Java diretamente. Este script de shell geralmente é bastante complexo, pois é genérico em todas as distribuições e geralmente inclui casos especiais para diferentes sistemas (por exemplo, Cygwin).

O diretório `lib` geralmente contém arquivos jar agrupados que satisfazem as dependências do aplicativo Java. Isso torna simples para um usuário instalar o programa (todas as dependências incluídas), mas é o pesadelo de um desenvolvedor de pacotes. É um desperdício de espaço quando vários pacotes agrupam a mesma dependência. Este não foi um grande problema no passado, quando havia menos aplicativos e bibliotecas de desktop Java, e aqueles que existiam tendiam a ser muito grandes de qualquer maneira. As coisas são diferentes agora ...

Outros arquivos necessários para executar o programa geralmente são armazenados na mesma pasta que o arquivo jar principal, ou um subdiretório dele. Uma vez que os programas Java não sabem de onde suas classes foram carregadas, eles geralmente precisam ser executados a partir deste diretório (ou seja, o script de shell deve `cd` no diretório) ou uma variável de ambiente está configurada para indicar o localização do diretório.

## Empacotamento de Java no Arch Linux

O empacotamento de aplicativos Java no Arch vai levar um pouco mais de trabalho para empacotadores do que atualmente. O esforço valerá a pena, no entanto, resultando em um sistema de arquivos mais limpo e poucas dependências agrupadas (à medida que mais e mais bibliotecas Java são refatoradas em seus próprios pacotes, os empacotamentos serão mais fáceis). As seguintes diretrizes devem ser seguidas na criação de um pacote Java do Arch Linux:

*   Se uma biblioteca Java tiver um nome genérico, o nome do pacote deve ser precedido pelo título `java-` para ajudar a distingui-lo de outras bibliotecas. Isso não é necessário com pacotes nomeados de forma exclusiva (como JUnit), programas de usuários finais (como o Eclipse) ou bibliotecas que podem ser descritas de forma exclusiva com outro prefixo (como jakarta-commons-collections ou apache-ant).

*   Você não precisa compilar aplicativos Java do fonte. Muito pouca otimização entra no processo de compilação, como os binários criados no gcc. Se o pacote fonte fornecer uma maneira fácil de compilar a partir da fonte, vá em frente e usá-lo, mas se é mais fácil apenas pegar uma versão binária de um arquivo jar ou um instalador, você também pode usar isso.

*   Coloque todos os arquivos jar (e nenhum outro arquivo) distribuídos com o programa em um diretório `/usr/share/java/meuprograma`. Isso inclui todos os arquivos jar de dependências distribuídos com o aplicativo. No entanto, o esforço deve ser feito para colocar bibliotecas de dependências comuns ou grandes em seus próprios pacotes. Isso só pode acontecer se o programa não depende de uma versão específica de uma biblioteca de dependências.

	Esta regra possibilita refatorar iterativamente as dependências. Ou seja, o pacote e todas as suas dependências podem ser colocados em um diretório no primeiro momento. Depois disso, as principais dependências podem ser refatoradas uma a uma. Observe que alguns aplicativos incluem dependências agrupadas dentro do arquivo jar principal. Ou seja, eles desfazem o jar das dependências agrupadas e as incluem no jar principal. Tais dependências geralmente são muito pequenas e há pouco interesse em refaturá-las.

*   Se o programa deve ser executado pelo usuário, escreva um script de shell personalizado que executa o arquivo jar principal. Este script deve ser colocado em `/usr/bin`. As bibliotecas geralmente não requerem scripts de shell. Escreva o script do shell a partir do zero, em vez de usar um que esteja empacotado com o programa. Remova o código que testa para ambientes personalizados (como Cygwin) e o código que tenta determinar se `JAVA_HOME` foi configurado (Arch [não usa](/index.php/Java_(Portugu%C3%AAs)#Instala.C3.A7.C3.A3o "Java (Português)") `JAVA_HOME`, ele usa `archlinux-java` para definir o link simbólico `/usr/bin/java`).

	tal script deve se parecer com isso para arquivos jar:

```
#!/bin/sh
exec /usr/bin/java -jar '/usr/share/java/NOMEPROGRAMA/NOMEPROGRAMA.jar' "$@"
```

	e como isso para arquivos com uma única classe:

```
#!/bin/sh
exec /usr/bin/java '/usr/share/java/NOMEPROGRAMA/NOMECLASSEPROGRAMA' "$@"
```

*   Defina o `CLASSPATH` usando a opção `-cp` para o interpretador Java a menos que haja um motivo explícito para não fazer isso (por exemplo, o `CLASSPATH` é usado como um mecanismo de plugin). O `CLASSPATH` deve incluir todos os arquivos jar no diretório `/usr/share/java/meuprograma`, bem como arquivos jar que são de bibliotecas de dependências que foram refatoradas para outros diretórios. Você pode usar alguma coisa como o código a seguir:

```
for nome in /usr/share/java/meuprograma/*.jar ; do
  CP=$CP:$nome
done
CP=$CP:/usr/share/java/dep1/dep1.jar
java -cp $CP meuprograma.java.MainClass
```

*   Certifique-se de que o script shell é executável!

*   Outros arquivos distribuídos com o pacote devem ser armazenados em um diretório com o nome do pacote em `/usr/share`. Talvez seja necessário definir a localização deste diretório em uma variável como `MEUPROJETO_HOME` dentro do script shell. Esta diretriz pressupõe que o programa espera que todos os arquivos estejam no mesmo diretório (como é padrão com pacotes Java). Se parecer mais natural colocar um arquivo de configuração em outro lugar (por exemplo, logs em `/var/log`), então sinta-se à vontade para fazê-lo.

	Tenha em mente que `/usr` pode ser montado como somente leitura em alguns sistemas. Se houver arquivos no diretório compartilhado que precisam ser escritos pelo aplicativo, eles podem ter que ser transferidos para `/etc`, `/var` ou no diretório inicial do usuário.

*   Como é padrão com os pacotes do Arch Linux, se os padrões acima não puderem ser adotados sem uma quantidade séria de trabalho, o pacote deve ser instalado de maneira preferida, com o diretório resultante localizado em `/opt`. Isso é útil para programas que agrupam JREs ou incluem versões personalizadas de dependências, ou fazem outras tarefas estranhas ou dolorosas.

### Múltiplas implementações de API

Se o seu pacote distribui um implementação de API comumente usada (como o driver jdbc), você deve colocar a biblioteca em `/usr/share/java/*nomeapi*`. Então, os aplicativos que permitem ao usuário selecionar de várias implementações saberá onde procurá-las. Use esta localização apenas para pacotes de bibliotecas não tratadas. Se tal implementação for parte da distribuição do aplicativo, **não** coloque este arquivo jar em uma localização comum, mas use a estrutura do pacote comum.

### Exemplo de estrutura de diretórios

Para esclarecer, aqui está uma estrutura de diretório de exemplo para um programa hipotético chamado `foo`. Uma vez que `foo` é um nome comum, o pacote é chamado `java-foo`, mas observe que isso não está refletido na estrutura de diretório:

*   `/usr/share/java/foo/`
*   `/usr/share/java/foo/foo.jar`
*   `/usr/share/java/foo/bar.jar` (incluindo dependência de `java-foo`)
*   `/usr/share/foo/`
*   `/usr/share/foo/*.*` (alguns arquivos gerais exigidos por `java-foo`)
*   `/usr/bin/foo` (script shell executável)

### Dependências

Os pacotes Java podem especificar `java-runtime` ou `java-environment` como dependência, baseado no que eles precisam.

Para a maioria dos pacotes, `java-runtime` é o que é necessário para simplesmente executar software escrito em Java. `java-runtime` é uma dependência virtual fornecida por:

*   [jre9-openjdk](https://www.archlinux.org/packages/?name=jre9-openjdk) (livre)
*   [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) (livre)
*   [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) (livre)
*   [java-gcj-compat](https://aur.archlinux.org/packages/java-gcj-compat/) (livre)
*   [jre](https://aur.archlinux.org/packages/jre/) (não livre)

`java-environment` (ex.: JDK) é necessário por pacotes que vão precisar o código fonte Java em código de bytes. `java-environment` é uma dependência virtual fornecida por:

*   [jdk9-openjdk](https://www.archlinux.org/packages/?name=jdk9-openjdk) (livre)
*   [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) (livre)
*   [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) (livre)
*   [jdk](https://aur.archlinux.org/packages/jdk/) (não livre)