Related articles

*   [Diretrizes de pacotes Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java")
*   [Fontes do Java Runtime Environment](/index.php/Java_Runtime_Environment_Fonts "Java Runtime Environment Fonts")

Do [artigo do Wikipédia](https://en.wikipedia.org/wiki/pt:Java_(linguagem_de_programa%C3%A7%C3%A3o) "wikipedia:pt:Java (linguagem de programação)"):

	Java é uma linguagem de programação interpretada orientada a objetos desenvolvida na década de 90 por uma equipe de programadores chefiada por James Gosling, na empresa Sun Microsystems. Diferente das linguagens de programação convencionais, que são compiladas para código nativo, a linguagem Java é compilada para um bytecode que é interpretado por uma máquina virtual (Java Virtual Machine, mais conhecida pela sua abreviação JVM). A linguagem de programação Java é a linguagem convencional da Plataforma Java, mas não é a sua única linguagem.

Arch Linux oferece suporte oficial às versões de código aberto OpenJDK 7, 8 e 9\. Todas essas JVM podem ser instaladas sem conflito e alternadas entre si usando o script auxiliar `archlinux-java`. Vários outros ambientes Java estão disponíveis no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), sem suporte oficial.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Marcando pacotes como desatualizados](#Marcando_pacotes_como_desatualizados)
*   [3 Alternando entre JVM](#Alternando_entre_JVM)
    *   [3.1 Listar ambientes Java compatíveis instalados](#Listar_ambientes_Java_compat.C3.ADveis_instalados)
    *   [3.2 Alterar o ambiente Java padrão](#Alterar_o_ambiente_Java_padr.C3.A3o)
    *   [3.3 Desconfigurar o ambiente Java padrão](#Desconfigurar_o_ambiente_Java_padr.C3.A3o)
    *   [3.4 Corrigir o ambiente Java padrão](#Corrigir_o_ambiente_Java_padr.C3.A3o)
    *   [3.5 Iniciar um aplicativo com uma versão Java não padrão](#Iniciar_um_aplicativo_com_uma_vers.C3.A3o_Java_n.C3.A3o_padr.C3.A3o)
*   [4 Pré-requisitos de pacote para ter suporte a archlinux-java](#Pr.C3.A9-requisitos_de_pacote_para_ter_suporte_a_archlinux-java)
*   [5 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [5.1 MySQL](#MySQL)
    *   [5.2 Personificar outro gerenciador de janela](#Personificar_outro_gerenciador_de_janela)
    *   [5.3 Fontes ilegíveis](#Fontes_ileg.C3.ADveis)
    *   [5.4 Faltando texto em alguns aplicativos](#Faltando_texto_em_alguns_aplicativos)
    *   [5.5 Aplicações sem redimensionamento com o WM, menus fechando imediatamente](#Aplica.C3.A7.C3.B5es_sem_redimensionamento_com_o_WM.2C_menus_fechando_imediatamente)
    *   [5.6 Sistema congela ao depurar aplicativos JavaFX](#Sistema_congela_ao_depurar_aplicativos_JavaFX)
*   [6 Dicas e truques](#Dicas_e_truques)
    *   [6.1 Melhor renderização de fonte](#Melhor_renderiza.C3.A7.C3.A3o_de_fonte)
    *   [6.2 Silenciar mensagem 'Picked up _JAVA_OPTIONS' na linha de comando](#Silenciar_mensagem_.27Picked_up_JAVA_OPTIONS.27_na_linha_de_comando)
    *   [6.3 Visual GTK](#Visual_GTK)
    *   [6.4 Melhor desempenho 2D](#Melhor_desempenho_2D)
    *   [6.5 Gerenciadores de janela non-reparenting / Janela cinza / Programas não estão sendo desenhados corretamente](#Gerenciadores_de_janela_non-reparenting_.2F_Janela_cinza_.2F_Programas_n.C3.A3o_est.C3.A3o_sendo_desenhados_corretamente)
*   [7 Veja também](#Veja_tamb.C3.A9m)

## Instalação

**Nota:**

*   A instalação de um JDK vai trazer automaticamente suas dependência em JRE.
*   Após a instalação, o ambiente Java precisará se reconhecido pelo shell (variável `$PATH`). Isso pode ser feito [carregando](/index.php/Carrega "Carrega") `/etc/profile` pela linha de comando ou saindo e entrando novamente em um ambiente de desktop.

Os pacotes *common* são trazidos respectivamente como dependência, chamados de [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) (contendo arquivos comuns para Java Runtime Environments) e [java-environment-common](https://www.archlinux.org/packages/?name=java-environment-common) (contendo arquivos comuns para Java Development Kits). O arquivo de ambiente fornecido `/etc/profile.d/jre.sh` aponta para um link simbólico `/usr/lib/jvm/default/bin`, definido pelo script auxiliar `archlinux-java`. Os links `/usr/lib/jvm/default` e `/usr/lib/jvm/default-runtime` devem **sempre** ser editados com `archlinux-java`. Ele é usado para exibir e apontar para uma ambiente Java padrão em `/usr/lib/jvm/java-${VERSÃO_MAIOR_JAVA}-${NOME_FORNECEDOR}` ou um runtime do Java em `/usr/lib/jvm/java-${VERSÃO_MAIOR_JAVA}-${NOME_FORNECEDOR}/jre`.

A maioria dos executáveis da instalação do Java são fornecidos por linsk diretos em `/usr/bin`, enquanto outros estão disponíveis em `$PATH`.

**Atenção:** O arquivo `/etc/profile.d/jdk.sh` não é mais fornecido por nenhum pacote.

Os pacotes a seguir estão disponíveis:

**OpenJDK 7** — A implementação código aberto da sétima edição do Java SE.

	[http://openjdk.java.net/projects/jdk7/](http://openjdk.java.net/projects/jdk7/) || [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) [openjdk7-doc](https://www.archlinux.org/packages/?name=openjdk7-doc) [openjdk7-src](https://www.archlinux.org/packages/?name=openjdk7-src)

**IBM J9 7** — Implementação da IBM da sétima edição do JRE.

	[https://developer.ibm.com/javasdk/downloads/sdk7/](https://developer.ibm.com/javasdk/downloads/sdk7/) || [jdk7-j9-bin](https://aur.archlinux.org/packages/jdk7-j9-bin/) [jdk7r1-j9-bin](https://aur.archlinux.org/packages/jdk7r1-j9-bin/)

**OpenJDK 8** — A implementação código aberto da oitava edição do Java SE.

	[http://openjdk.java.net/projects/jdk8/](http://openjdk.java.net/projects/jdk8/) || [jre8-openjdk-headless](https://www.archlinux.org/packages/?name=jre8-openjdk-headless) [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc) [openjdk8-src](https://www.archlinux.org/packages/?name=openjdk8-src)

**OpenJFX 8** — A implementação código aberto do JavaFX. Você [não precisa](https://wiki.openjdk.java.net/display/OpenJFX/Repositories+and+Releases) instalar esse pacote se você está fazendo uso do Java SE (a implementação da Oracle do JRE e JDK, descritos abaixo). Esse pacote só interessa usuários da implementação código aberto de Java (projeto OpenJDK).

	[http://openjdk.java.net/projects/openjfx/](http://openjdk.java.net/projects/openjfx/) || [java-openjfx](https://www.archlinux.org/packages/?name=java-openjfx) [java-openjfx-doc](https://www.archlinux.org/packages/?name=java-openjfx-doc) [java-openjfx-src](https://www.archlinux.org/packages/?name=java-openjfx-src)

**IBM J9 8** — Implementação da IBM da oitava edição do JRE.

	[https://developer.ibm.com/javasdk/downloads/sdk8/](https://developer.ibm.com/javasdk/downloads/sdk8/) || [jdk8-j9-bin](https://aur.archlinux.org/packages/jdk8-j9-bin/)

**OpenJDK 9** — A implementação código aberto da nona edição do Java SE.

	[http://openjdk.java.net/projects/jdk9/](http://openjdk.java.net/projects/jdk9/) || [jre9-openjdk-headless](https://www.archlinux.org/packages/?name=jre9-openjdk-headless) [jre9-openjdk](https://www.archlinux.org/packages/?name=jre9-openjdk) [jdk9-openjdk](https://www.archlinux.org/packages/?name=jdk9-openjdk) [openjdk9-doc](https://www.archlinux.org/packages/?name=openjdk9-doc) [openjdk9-src](https://www.archlinux.org/packages/?name=openjdk9-src)

**OpenJ9** — Implementação do Eclipse de JRE, contribuído pela IBM.

	[https://www.eclipse.org/openj9/](https://www.eclipse.org/openj9/) || [jdk8-openj9-bin](https://aur.archlinux.org/packages/jdk8-openj9-bin/) [jdk9-openj9-bin](https://aur.archlinux.org/packages/jdk9-openj9-bin/)

**Java SE** — Implementação da Oracle de JRE e JDK.

	[http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html) || [jre](https://aur.archlinux.org/packages/jre/) [jre6](https://aur.archlinux.org/packages/jre6/) [jre7](https://aur.archlinux.org/packages/jre7/) [jre8](https://aur.archlinux.org/packages/jre8/) [jre-devel](https://aur.archlinux.org/packages/jre-devel/) [jdk](https://aur.archlinux.org/packages/jdk/) [jdk5](https://aur.archlinux.org/packages/jdk5/) [jdk6](https://aur.archlinux.org/packages/jdk6/) [jdk7](https://aur.archlinux.org/packages/jdk7/) [jdk8](https://aur.archlinux.org/packages/jdk8/) [jdk-devel](https://aur.archlinux.org/packages/jdk-devel/)

**Parrot VM** — Uma VM com suporte experimental para Java [[1]](http://trac.parrot.org/parrot/wiki/Languages) por meio de dois métodos diferentes: como um [tradutor de um *bytecode* de Java VM](http://code.google.com/p/parrot-jvm/) ou como um [compilador Java visando o Parrot VM](https://github.com/chrisdolan/perk).

	[http://www.parrot.org/](http://www.parrot.org/) || [parrot](https://aur.archlinux.org/packages/parrot/)

**Nota:** Versões de 32 bits do Java SE podem ser localizados prefixando `bin32-`, (por exemplo, [bin32-jre](https://aur.archlinux.org/packages/bin32-jre/) e [bin32-jdk](https://aur.archlinux.org/packages/bin32-jdk/)). Elas usam [java32-runtime-common](https://aur.archlinux.org/packages/java32-runtime-common/), que funciona como [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) acrescentando `32` ao final (por exemplo, `java32`). A mesma analogia se aplica a [java32-environment-common](https://aur.archlinux.org/packages/java32-environment-common/), que é usado somente por pacotes de JDK de 32 bits.

## Marcando pacotes como desatualizados

Embora os lançamentos do pacote Arch Linux possam conter uma referência às versões proprietárias nas quais os pacotes se baseiam, o projeto código aberto possui seu próprio esquema de versão:

*   [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk), [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) e [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) devem ser marcados como desatualizados com base na [versão do *IcedTea*](http://icedtea.wildebeest.org/download/source) (ex.: `2.4.3`), em vez da versão de referência da Oracle (ex. `u45` no lançamento `7.u45_2.4.3-1`).
*   [icedtea-web](https://www.archlinux.org/packages/?name=icedtea-web) deve ser marcado como desatualizado com base na [versão do *IcedTea Web*](http://icedtea.wildebeest.org/download/source) (ex.: `1.4.1`). Ele é independente da versão do *IcedTea*.

## Alternando entre JVM

O script auxiliar `archlinux-java` fornece tais funcionalidades:

```
archlinux-java <COMANDO>

COMANDO:
	status		Lista ambientes Java instalados e um habilitado
	get		Retorna o nome curto do ambiente Java definido como padrão
	set <JAVA_ENV>	Força <JAVA_ENV> como padrão
	unset		Desconfigura o ambiente Java padrão atual
	fix		Corrige uma configuração inválida/quebrada de ambiente Java padrão

```

### Listar ambientes Java compatíveis instalados

```
$ archlinux-java status

```

Exemplo:

```
$ archlinux-java status
Available Java environments:
  java-7-openjdk (default)
  java-8-openjdk/jre

```

Note o "*(default)*" denotando que o `java-7-openjdk` está atualmente definido como padrão. Chamar `java` e outros binários vai depender dessa instalação do Java. Também note na saída anterior que somente a parte *JRE* do OpenJDK 8 está instalada aqui.

### Alterar o ambiente Java padrão

```
# archlinux-java set <JAVA_ENV>

```

Exemplo:

```
# archlinux-java set java-8-openjdk/jre

```

**Dica:** Para ver nomes possíveis de `<JAVA_ENV>`, use `archlinux-java status`.

Note que o `archlinux-java` não vai deixar você definir um ambiente Java inválido. No exemplo anterior, [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) está instalado, mas [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) **não** está, então a tentativa de definir `java-8-openjdk` vai falhar:

```
# archlinux-java set java-8-openjdk
'/usr/lib/jvm/java-8-openjdk' is not a valid Java environment path

```

### Desconfigurar o ambiente Java padrão

Não há necessidade de remover a definição de um ambiente Java, pois os pacotes que os fornecem devem cuidar disso. Ainda assim, caso você queira fazê-lo, basta usar o comando `unset`:

```
# archlinux-java unset

```

### Corrigir o ambiente Java padrão

Se um link inválido de ambiente Java estiver definido, executar o comando `archlinux-java fix` tenta corrigi-lo. Note também que, se nenhum ambiente Java padrão estiver configurado, isso fará com que busque outros válidos e tentará configurá-lo para você. Os pacotes oficialmente suportados "OpenJDK 7" e "OpenJDK 8" serão considerados primeiro nesta ordem, então, pacotes não oficiais do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)").

```
# archlinux-java fix

```

### Iniciar um aplicativo com uma versão Java não padrão

Se você quiser iniciar um aplicativo com outra versão do java do que o padrão (por exemplo, se você tiver as versões jre7 e jre8 instaladas no seu sistema), você pode chamar seu aplicativo em um pequeno script bash para alternar localmente o PATH padrão de Java. Por exemplo, se a versão padrão for jre7 e você quiser usar jre8:

```
#!/bin/sh 

export PATH=/usr/lib/jvm/java-8-openjdk/jre/bin/:$PATH
exec /path/to/application "$@"

```

## Pré-requisitos de pacote para ter suporte a `archlinux-java`

**Nota:** As informações abaixo também se aplicam a `archlinux32-java` para pacotes Java de 32 bits, com devidos acréscimos de `32` aos nome des pacote ou de executável, onde aplicável.

Esta seção é direcionada ao empacotador disposto a fornecer pacotes no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") para uma JVM alternativa e que possa se integrar ao esquema JVM do Arch Linux para usar o `archlinux-java`. Para fazer isso, os pacotes devem:

*   Colocar todos os arquivos sob `/usr/lib/jvm/java-${VERSÃO_MAIOR_JAVA}-${NOME_FORNECEDOR}`
*   Certifique-se de que todos os executáveis para os quais [java-runtime-common](https://www.archlinux.org/packages/extra/any/java-runtime-common/files/) e [java-environment-common](https://www.archlinux.org/packages/extra/any/java-environment-common/files/) fornecem links estejam disponíveis no pacote correspondente
*   Forneça links de `/usr/bin` para os executáveis somente se esses links não já pertencerem a [java-runtime-common](https://www.archlinux.org/packages/extra/any/java-runtime-common/files/) e [java-environment-common](https://www.archlinux.org/packages/extra/any/java-environment-common/files/)
*   Acrescente ao final das páginas man `-${NOME_FORNECEDOR}${VERSÃO_MAIOR_JAVA}` para evitar conflitos (veja a [lista de arquivos do jre8-openjdk](https://www.archlinux.org/packages/extra/x86_64/jre8-openjdk/files/) no qual as páginas man recebem, ao final de seu nome, `-openjdk8`)
*   Não declare qualquer [conflicts](/index.php/PKGBUILD_(Portugu%C3%AAs)#conflicts "PKGBUILD (Português)") ou [replaces](/index.php/PKGBUILD_(Portugu%C3%AAs)#replaces "PKGBUILD (Português)") com outras JDKs, `java-runtime`, `java-runtime-headless` ou `java-environment`
*   Use o script `archlinux-java` em *funções do .install* para configurar o ambiente Java como padrão **Se nenhum outro ambiente Java válido estiver definido** (ie: o pacote não deve **forçar** a instalação como padrão). Veja [fontes de pacote de ambiente Java suportadas oficialmente](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/java7-openjdk) para exemplos

Note também que:

*   Pacotes que precisam de **qualquer** ambiente Java devem declarar a dependência a `java-runtime`, `java-runtime-headless` ou `java-environment`
*   Pacotes que precisam de um **fornecedor Java específico** devem declarar a dependência no pacote correspondente
*   Pacotes OpenJDK agora declaram `provides="java-runtime-openjdk=${pkgver}"` etc. Isso permite que um pacote de terceiro declare dependência em um OpenJDK sem especificar uma versão

## Solução de problemas

### MySQL

Devido ao fato de que os drivers JDBC costumam usar a porta no URL para estabelecer uma conexão com o banco de dados, ele é considerado "remoto" (ou seja, o MySQL não escuta a porta de acordo com suas configurações padrão), apesar do fato de que eles estão possivelmente executando no mesmo host. Assim, para usar JDBC e MySQL, você deve habilitar o acesso remoto ao MySQL, seguindo as instruções em [MySQL#Grant Remote Access](/index.php/MySQL#Grant_Remote_Access "MySQL").

### Personificar outro gerenciador de janela

Você pode usar o [wmname](https://www.archlinux.org/packages/?name=wmname) do [suckless.org](http://tools.suckless.org/x/wmname) para fazer a JVM acreditar que você está executando em um gerenciador de janela diferente. Isso pode resolver um problema de renderização das GUIs Java ocorrendo em gerenciadores de janela, como o [Awesome](/index.php/Awesome "Awesome"), [Dwm](/index.php/Dwm "Dwm") ou [Ratpoison](/index.php/Ratpoison "Ratpoison").

```
$ wmname LG3D

```

Você deve reiniciar o aplicativo em questão após executar o comando wmname.

Isso funciona porque a JVM contém uma lista codificada de gerenciadores de janela *non-re-parenting* (que não registram novas janelas como de topo de nível) conhecidos. Para a máxima ironia, alguns usuários preferem personificar `LG3D`, o gerenciador de janela *non-re-parenting* [escrito pela Sun, em Java](https://en.wikipedia.org/wiki/Project_Looking_Glass "wikipedia:Project Looking Glass").

### Fontes ilegíveis

Além das sugestões mencionadas abaixo em [#Melhor renderização de fonte](#Melhor_renderiza.C3.A7.C3.A3o_de_fonte), algumas fontes ainda pode não estar legíveis depois. Se esse for o caso, há uma grande chance das fontes da Microsoft estarem sendo usadas. Instale [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)").

### Faltando texto em alguns aplicativos

Se alguns aplicativos estão faltando textos completos, pode ajudar a usar as opções em [#Dicas e truques](#Dicas_e_truques) como sugerido em [FS#40871](https://bugs.archlinux.org/task/40871).

### Aplicações sem redimensionamento com o WM, menus fechando imediatamente

O kit de ferramentas padrão de GUI do Java possui uma lista codificada de gerenciadores de janela "*não-reparenting*". Se estiver usando um que não esteja nessa lista, pode haver alguns problemas com a execução de alguns aplicativos Java. Um dos problemas mais comuns é "blobs cinzas", quando o aplicativo Java se renderiza como uma caixa cinzenta simples em vez de renderizar a interface gráfica esperada. Outro pode ser menus respondendo ao seu clique, mas fechando imediatamente.

Há várias coisas que podem ajudar:

*   Para [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) ou [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk), acrescente a linha `export _JAVA_AWT_WM_NONREPARENTING=1` em `/etc/profile.d/jre.sh`. Então, [carregue](/index.php/Carrega "Carrega") o arquivo `/etc/profile.d/jre.sh` ou encerre a sessão e incie-a novamente.
*   Para JRE/JDK da Oracle, use [SetWMName](https://wiki.haskell.org/Xmonad/Frequently_asked_questions#Using_SetWMName). Porém, seu efeito pode ser cancelado ao usar também `XMonad.Hooks.EwmhDesktops`. Neste caso, acrescentar

```
>> setWMName "LG3D"

```

ao `LogHook` pode ajudar.

Veja [[2]](http://wiki.haskell.org/Xmonad/Frequently_asked_questions#Problems_with_Java_applications.2C_Applet_java_console) para mais informações.

### Sistema congela ao depurar aplicativos JavaFX

Se o seu sistema congela durante a depuração de um aplicativo JavaFX, você pode tentar fornecer a opção JVM `-Dsun.awt.disablegrab=true`.

Veja [http://bugs.java.com/view_bug.do?bug_id=6714678](http://bugs.java.com/view_bug.do?bug_id=6714678)

## Dicas e truques

**Nota:** As sugestões nesta seção são aplicáveis a todos os aplicativos, usando o *runtime* do Java instalado explicitamente (externo). Alguns aplicativos são agrupados com *runtime* próprio (privado) ou usam mecanismos próprios para GUI, renderização de fontes, etc., portanto, nenhum dos itens escritos abaixo é garantido de funcionar.

O comportamento da maioria dos aplicativos Java pode ser controlado fornecendo variáveis pré-definidas para o tempo de execução Java. Desta [publicação do fórum](https://bbs.archlinux.org/viewtopic.php?id=72892), uma maneira de fazê-lo consiste em adicionar a seguinte linha no seu `~/.bashrc` (ou `/etc/profile.d/jre.sh` para afetar programas que não são executados [carregando](/index.php/Carrega "Carrega") `~/.bashrc`, por exemplo, ao iniciar um programa a partir da visão de aplicativos do GNOME):

```
export _JAVA_OPTIONS="-D**<opção 1>** -D**<opção 2>**..."

```

Por exemplo, para usar fontes *anti-alias* do sistema e fazer o *swing* usar a aparência do GTK:

```
export _JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=on -Dswing.aatext=true -Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel'

```

### Melhor renderização de fonte

As implementações de código fechado e de código aberto de Java são conhecidas por implementar incorretamente o *anti-aliasing* de fontes. Isso pode ser corrigido com as seguintes opções: `-Dawt.useSystemAAFontSettings=on`, `-Dswing.aatext=true`

Veja [Fontes do Java Runtime Environment](/index.php/Java_Runtime_Environment_fonts "Java Runtime Environment fonts") para informações mais detalhadas.

### Silenciar mensagem 'Picked up _JAVA_OPTIONS' na linha de comando

Definir as variáveis de ambiente _JAVA_OPTIONS faz com que java (openjdk) escreva para *stderr* as mensagens da forma: 'Picked up _JAVA_OPTIONS = ...'. Para suprimir essas mensagens em seu terminal, você pode desmarcar a variável de ambiente nos arquivos de inicialização de shell e fazer um alias do java para passar as mesmas opções como argumentos de linha de comando:

```
_SILENT_JAVA_OPTIONS="$_JAVA_OPTIONS"
unset _JAVA_OPTIONS
alias java='java "$_SILENT_JAVA_OPTIONS"'

```

### Visual GTK

Se seus programas Java estão com aparência ruim, você pode querer configurar a aparência padrão para componentes *swing*:

`swing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel`.

Alguns programas Java insistem em usar a aparência multiplataforma Metal. Em alguns casos você pode forçar esses aplicativos a usar o visual do GTK definindo a propriedade a seguir:

`swing.crossplatformlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel`.

**Nota:** Forçar o Java a usar o GTK pode quebrar alguns aplicativos. O JRE/JDK está vinculado ao GTK2 enquanto muitas aplicações de desktop usam o GTK3\. Se um aplicativo GTK3 tiver plugins Java com GUI, é provável que o aplicativo falhe ao abrir a GUI Java, já que não há suporte à mistura de GTK2 e GTK3\. O Libreoffice 5.0 é um exemplo disso.

### Melhor desempenho 2D

Alternar para o pipeline de aceleração de hardware baseado em OpenGL melhorará o desempenho em 2D

```
export _JAVA_OPTIONS='-Dsun.java2d.opengl=true'

```

### Gerenciadores de janela non-reparenting / Janela cinza / Programas não estão sendo desenhados corretamente

Usuários de gerenciadores de janela *non-reparenting* devem configurar a seguinte variável em seu `.xinitrc`

```
export _JAVA_AWT_WM_NONREPARENTING=1

```

Não configurar isso pode resultar em programa javas não serem desenhados corretamente.

## Veja também

*   [Introdução à Programação Usando o Java](http://math.hws.edu/javanotes/)