[Eclipse](https://eclipse.org) é um projeto comunitário de código aberto, que visa fornecer uma plataforma de desenvolvimento universal. O projeto Eclipse é mais conhecido por seu IDE (ambiente de desenvolvimento integrado) multiplataforma. Os pacotes do Arch Linux (e este guia) estão relacionados especificamente ao IDE.

O Eclipse IDE é amplamente escrito em Java, mas pode ser usado para desenvolver aplicativos em várias linguagens, incluindo Java, C / C ++, PHP, Perl e Python. O IDE também pode fornecer suporte ao subversion e gerenciamento de tarefas.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Plugins](#Plugins)
    *   [2.1 Adicione o site de atualização padrão](#Adicione_o_site_de_atualização_padrão)
    *   [2.2 Eclipse Marketplace](#Eclipse_Marketplace)
    *   [2.3 Gerenciador de Plugin](#Gerenciador_de_Plugin)
        *   [2.3.1 Atualizações via gerenciador de plugins](#Atualizações_via_gerenciador_de_plugins)
    *   [2.4 Lista de plugins](#Lista_de_plugins)
*   [3 Ativar integração javadoc](#Ativar_integração_javadoc)
    *   [3.1 Versão online](#Versão_online)
    *   [3.2 Versão offline](#Versão_offline)
*   [4 Solução de problemas](#Solução_de_problemas)
    *   [4.1 Ctrl+X fecha Eclipse](#Ctrl+X_fecha_Eclipse)
    *   [4.2 Tema escuro](#Tema_escuro)
    *   [4.3 Alterar tamanho da fonte do título da janela padrão](#Alterar_tamanho_da_fonte_do_título_da_janela_padrão)
    *   [4.4 Desativar GTK 3](#Desativar_GTK_3)
    *   [4.5 Freshplayerplugin](#Freshplayerplugin)
    *   [4.6 Eclipse 4.6 não pode abrir a propriedade marketplace](#Eclipse_4.6_não_pode_abrir_a_propriedade_marketplace)
    *   [4.7 Mostrar no System Explorer não funciona](#Mostrar_no_System_Explorer_não_funciona)
    *   [4.8 Exibir problemas em Wayland](#Exibir_problemas_em_Wayland)
*   [5 Veja também](#Veja_também)

## Instalação

[Instalar](/index.php/Instalar "Instalar") um dos seguintes pacotes:

*   [eclipse-jee](https://www.archlinux.org/packages/?name=eclipse-jee) for Java EE Developers
*   [eclipse-java](https://www.archlinux.org/packages/?name=eclipse-java) for Java Developers
*   [eclipse-cpp](https://www.archlinux.org/packages/?name=eclipse-cpp) for C/C++ Developers
*   [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php) for PHP Developers
*   [eclipse-javascript](https://www.archlinux.org/packages/?name=eclipse-javascript) for JavaScript and Web Developers
*   [eclipse-rust](https://www.archlinux.org/packages/?name=eclipse-rust) for Rust Developers

Você não pode instalar vários deles ao mesmo tempo, pois eles conflitam, consulte [FS#45577](https://bugs.archlinux.org/task/45577): escolha o pacote acima do qual atenda imediatamente às suas necessidades e adicione suporte para os idiomas adicionais necessários através [#Plugins](#Plugins).

## Plugins

Muitos plugins são facilmente instalados usando **pacman** (veja [Eclipse plugin package guidelines](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") para mais informações). Isso também os manterá atualizados. Como alternativa, você pode escolher o [Eclipse Marketplace](#Eclipse_Marketplace) ou o interno [plugin manager](#Plugin_manager).

### Adicione o site de atualização padrão

Certifique-se de verificar se o site de atualização padrão para sua versão do Eclipse está configurado para que as dependências do plug-in possam ser instaladas automaticamente. A versão mais atual do Eclipse é o Photon e o site de atualização padrão é: [http://download.eclipse.org/releases/photon](http://download.eclipse.org/releases/photon). Vá para Ajuda> Instalar novo software> Adicionar, preencha o nome para identificar facilmente o site de atualização posteriormente - por exemplo, Photon Software Repository - e preencha o local com o URL.

### Eclipse Marketplace

**Nota:** certifique-se de ter seguido a seção [Add the default update site](#Adicione_o_site_de_atualização_padrão).

Para usar o Eclipse Marketplace, instale primeiro: vá para Help > Install new software > Switch to the default update site > General Purpose Tools > Marketplace Client. Reinicie o Eclipse e ele estará disponível em Help > Eclipse Marketplace.

### Gerenciador de Plugin

**Nota:** certifique-se de ter seguido a seção [Add the default update site](#Adicione_o_site_de_atualização_padrão).

Use o gerenciador de plugins do Eclipse para baixar e instalar plugins de seus repositórios originais: nesse caso, você precisa encontrar o repositório necessário no site do plug-in e, em seguida, vá para *Help > Install New Software...*, insira o repositório no campo *Work with*, selecione o plug-in para instalar na lista abaixo e siga as instruções.

**Nota:**

*   Se você instalar plug-ins com o gerenciador de plug-ins do Eclipse, é recomendável iniciar o Eclipse como root: dessa maneira, os plug-ins serão instalados em `/usr/lib/eclipse/plugins/`; se você os instalasse como usuário normal, eles seriam armazenados em uma pasta dependente da versão dentro `~/.eclipse/`, e, após o upgrade do Eclipse, eles não seriam mais reconhecidos.
*   Não use o Eclipse como root para o seu trabalho diário.

#### Atualizações via gerenciador de plugins

Abra o Eclipse e vá em *Help > Check for Updates*. Se você os instalou como root, conforme recomendado na seção acima, precisará executar o Eclipse como root.

Para que os plug-ins sejam atualizados, verifique se os repositórios de atualização estão ativados em *Window > Preferences > Install/Update > Available Software Sites*: você pode encontrar os repositórios de cada plug-in no respectivo site do projeto. Para adicionar, editar, remover ... repositórios, basta usar os botões à direita do painel *Sites de software disponíveis*. Para o Eclipse 4.5 (Mars), verifique se você ativou este repositório:

```
[http://download.eclipse.org/releases/mars](http://download.eclipse.org/releases/mars)

```

Para receber notificações de atualização, vá para *Window > Preferences > Install/Update > Automatic Updates*. Se você deseja receber notificações para plug-ins instalados como root, execute o Eclipse como root, vá para *Window > Preferences > Install/Update > Available Software Sites*, selecione os repositórios relacionados aos plugins instalados e *Export(Exporte)* eles, execute o Eclipse como usuário normal e *Import(Importe)* eles no mesmo painel.

### Lista de plugins

*   **AVR** — AVR microcontroller plugin.

	[http://avr-eclipse.sourceforge.net/wiki/index.php/The_AVR_Eclipse_Plugin](http://avr-eclipse.sourceforge.net/wiki/index.php/The_AVR_Eclipse_Plugin) || [eclipse-avr](https://aur.archlinux.org/packages/eclipse-avr/)

*   **Aptana** — HTML5/CSS3/JavaScript/Ruby/Rails/PHP/Pydev/Django support. Also available as standalone application.

	[http://www.aptana.com/](http://www.aptana.com/) || [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)

*   **IvyDE** — IvyDE dependency Manager.

	[https://ant.apache.org/ivy/ivyde/](https://ant.apache.org/ivy/ivyde/) || [eclipse-ivyde](https://aur.archlinux.org/packages/eclipse-ivyde/)

*   **Markdown** — Markdown editor plugin for Eclipse.

	[http://www.winterwell.com/software/markdown-editor.php](http://www.winterwell.com/software/markdown-editor.php) || [eclipse-markdown](https://aur.archlinux.org/packages/eclipse-markdown/)

*   **PyDev** — [Python](/index.php/Python "Python") support.

	[http://pydev.org/](http://pydev.org/) || [eclipse-pydev](https://aur.archlinux.org/packages/eclipse-pydev/)

*   **Subclipse** — [Subversion](/index.php/Subversion "Subversion") support.

	[https://github.com/subclipse/subclipse](https://github.com/subclipse/subclipse) || [eclipse-subclipse](https://aur.archlinux.org/packages/eclipse-subclipse/)

*   **Subversive** — Alternative Subversion support.

	[https://www.eclipse.org/subversive/](https://www.eclipse.org/subversive/) || [eclipse-subversive](https://aur.archlinux.org/packages/eclipse-subversive/)

*   **TestNG** — TestNG support.

	[http://testng.org/doc/eclipse.html](http://testng.org/doc/eclipse.html) || [eclipse-testng](https://aur.archlinux.org/packages/eclipse-testng/)

*   **TeXlipse** — [LaTeX](/index.php/LaTeX "LaTeX") support.

	[http://texlipse.sourceforge.net/](http://texlipse.sourceforge.net/) || [eclipse-texlipse](https://aur.archlinux.org/packages/eclipse-texlipse/)

*   **Checkstyle** — Eclipse Checkstyle support.

	[http://eclipse-cs.sourceforge.net/](http://eclipse-cs.sourceforge.net/) || [eclipse-checkstyle](https://aur.archlinux.org/packages/eclipse-checkstyle/)

## Ativar integração javadoc

Deseja ver as entradas da API ao passar o mouse sobre os métodos Java padrão?

### Versão online

Se você tiver acesso constante à Internet em sua máquina, poderá usar a documentação on-line:

1.  Vá para *Window > Preferences*, então vá para *Java > Installed JREs*.
2.  Deve haver um chamado "java" com o tipo "Standard VM". Selecione e clique em *Edit*.
3.  Selecione o item em {{ic|/usr/lib/jvm/java-8-openjdka/jre/lib/rt.jar} "JRE system libraries:", e clique *Javadoc Location...*.
4.  Digite "[https://docs.oracle.com/javase/8/docs/api/](https://docs.oracle.com/javase/8/docs/api/)" no campo de texto "Javadoc location path:".

### Versão offline

Você pode armazenar a documentação localmente instalando o pacote [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc). O Eclipse pode encontrar os javadocs automaticamente. Se isso não funcionar, configure o local do Javadoc para rt.jar para `file:/usr/share/doc/java8-openjdk/api`.

## Solução de problemas

### Ctrl+X fecha Eclipse

Parte do [this](https://bugs.eclipse.org/bugs/show_bug.cgi?id=318177) bug. Basta procurar em `~/workspace/.metadata/.plugins/org.eclipse.e4.workbench/workbench.xmi` e excluir a combinação `Ctrl+X` errada. Geralmente é o primeiro.

### Tema escuro

O Eclipse fornece um tema Escuro que pode ser ativado em Window > Preferences > General > Appearance e selecione o tema 'Dark'.

O tema escuro usa suas próprias cores, e não as cores do tema GTK, se você preferir respeitar totalmente as configurações de cores GTK, remova ou mova para a subpasta de backup todos os arquivos .css de`/usr/lib/eclipse/plugins/org.eclipse.ui.themes_x.x.xxx.vxxxxxxxx-xxxx/css/`.

### Alterar tamanho da fonte do título da janela padrão

Não é possível alterar o tamanho da fonte do título da janela usando as preferências do Eclipse; você deve editar os arquivos .css do tema real. Observe que você precisará refazer isso ao atualizar o eclipse. Eles estão localizados em

```
/usr/share/eclipse/plugins/org.eclipse.platform_4.3.<your version number>/css

```

Abra o arquivo apropriado com o seu editor de texto, ou seja, e4_default_gtk.css se você estiver usando o "Tema GTK". Procure por .MPartStack e altere o tamanho da fonte para o tamanho desejado

```
.MPartStack {
       font-size: 9;
       swt-simple: false;
       swt-mru-visible: false;
}

```

### Desativar GTK 3

Quando a interface do usuário do SWT GTK 3 é com erros e às vezes inutilizável, você pode tentar desativar o uso do GTK 3 com o SWT_GTK3 = 0 [variável de ambiente](/index.php/Vari%C3%A1vel_de_ambiente "Variável de ambiente") ao iniciar o eclipse:

```
SWT_GTK3=0 eclipse

```

Outra opção para obter o mesmo efeito é adicionar o seguinte a `/usr/lib/eclipse/eclipse.ini`.

```
--launcher.GTK_version
2

```

Essas duas linhas devem ser adicionadas **antes**:

```
--launcher.appendVmargs

```

### Freshplayerplugin

Eclipse não é compatível com [freshplayerplugin](https://aur.archlinux.org/packages/freshplayerplugin/). Veja [https://github.com/i-rinat/freshplayerplugin/issues/298](https://github.com/i-rinat/freshplayerplugin/issues/298).

### Eclipse 4.6 não pode abrir a propriedade marketplace

Veja [this](https://bugs.eclipse.org/bugs/show_bug.cgi?id=497729) bug. Você pode seguir duas etapas para corrigi-lo:

```
eclipse -consoleLog -application org.eclipse.equinox.p2.director -uninstallIU org.apache.httpcomponents.httpclient/4.3.6.v201411290715
cd /usr/lib/eclipse/ && sudo rm plugins/org.apache.httpcomponents.httpclient_4.3.6.v201411290715.jar

```

### Mostrar no System Explorer não funciona

Vejá esse guia [this](http://help.eclipse.org/luna/index.jsp?topic=%2Forg.eclipse.platform.doc.user%2Freference%2Fref-9.htm&cp=0_4_1_52). Vá para **Window** > **Preferences** > **General** > **Workspace** e altere o comando ativando o system explorer. Como usuário do Xfce, você pode alterá-lo para `thunar ${selected_resource_uri}` para abrir a pasta selecionada com thunar.

### Exibir problemas em Wayland

Ao executar o Eclipse em Wayland, você pode encontrar problemas de renderização, como tempo de resposta lento a eventos do mouse ou janelas de diálogo cortadas (Bug report [[1]](https://bugs.eclipse.org/bugs/show_bug.cgi?id=483545)). Uma solução possível para esse problema é forçar o Eclipse a executar no XWayland.

Com o superusuário, abra o arquivo `/usr/bin/eclipse` e anexe esta linha antes da linha `exec` :

```
   export GDK_BACKEND=x11

```

Isso forçará a execução do Eclipse no XWayland.

## Veja também

*   [Como usar o Subversion com o Eclipse](https://www.ibm.com/developerworks/library/os-ecl-subversion/)