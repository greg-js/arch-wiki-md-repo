Artigos relacionados

*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")
*   [Step-by-step debugging guide](/index.php/Step-by-step_debugging_guide "Step-by-step debugging guide")
*   [Depuração - Obtendo Rastros](/index.php/Depura%C3%A7%C3%A3o_-_Obtendo_Rastros "Depuração - Obtendo Rastros")

Abrir (e fechar) relatórios de erros no [Rastreador de erros do Arch Linux](https://bugs.archlinux.org/) (também conhecido como *Arch Linux Bugtracker*) é uma das muitas maneiras possíveis de [ajudar a comunidade](/index.php/Getting_involved_(Portugu%C3%AAs) "Getting involved (Português)"). No entanto, relatórios de erros mal formulados podem ser contraproducentes. Quando os erros são incorretamente relatados, os desenvolvedores perdem tempo investigando e fechando relatórios inválidos. Este documento irá guiar qualquer pessoa que deseje ajudar a comunidade informando eficientemente e buscando erros.

Veja também: [Como relatar erros de forma efetiva](https://www.chiark.greenend.org.uk/~sgtatham/bugs.html) (em inglês) por Simon Tatham

## Contents

*   [1 Antes de relatar](#Antes_de_relatar)
    *   [1.1 Pesquise por duplicados](#Pesquise_por_duplicados)
    *   [1.2 Upstream ou Arch?](#Upstream_ou_Arch.3F)
    *   [1.3 Erro ou recurso?](#Erro_ou_recurso.3F)
        *   [1.3.1 Motivos para não ser um erro](#Motivos_para_n.C3.A3o_ser_um_erro)
        *   [1.3.2 Motivos para não ser um recurso](#Motivos_para_n.C3.A3o_ser_um_recurso)
    *   [1.4 Colete informações úteis](#Colete_informa.C3.A7.C3.B5es_.C3.BAteis)
*   [2 Abrindo um relatório](#Abrindo_um_relat.C3.B3rio)
    *   [2.1 Criando uma conta](#Criando_uma_conta)
    *   [2.2 Projetos](#Projetos)
    *   [2.3 Resumo](#Resumo)
    *   [2.4 Severidade](#Severidade)
    *   [2.5 Incluindo informações relevantes](#Incluindo_informa.C3.A7.C3.B5es_relevantes)
*   [3 Acompanhando relatórios](#Acompanhando_relat.C3.B3rios)
    *   [3.1 Votando e monitorando](#Votando_e_monitorando)
    *   [3.2 Respondendo solicitações de informações adicionais](#Respondendo_solicita.C3.A7.C3.B5es_de_informa.C3.A7.C3.B5es_adicionais)
    *   [3.3 Atualizando o relatório de erro quando surgir uma nova versão do software relatado](#Atualizando_o_relat.C3.B3rio_de_erro_quando_surgir_uma_nova_vers.C3.A3o_do_software_relatado)
    *   [3.4 Fechando quando resolvido](#Fechando_quando_resolvido)
    *   [3.5 Mais sobre status de relatórios](#Mais_sobre_status_de_relat.C3.B3rios)

## Antes de relatar

Preparar um relatório de erros detalhado e bem formado não é difícil, mas requer um esforço do relatante. **O trabalho feito antes de relatar um erro é indiscutivelmente a parte mais útil do trabalho**. Infelizmente, poucas pessoas tomam o tempo para fazer isso funcionar corretamente.

Os passos a seguir vão lhe guiar na preparação de seu relatório de erro ou requisição de recurso.

### Pesquise por duplicados

Se você encontrar um problema ou desejar um novo recurso, existe uma grande probabilidade de que alguém já tenha esse problema ou ideia. Se assim for, um relatório de erro apropriado já pode existir. Nesse caso, não crie um relatório duplicado; veja [#Acompanhando relatórios](#Acompanhando_relat.C3.B3rios).

Pesquise detalhadamente as informações existentes, incluindo:

*   [Fóruns do Arch Linux](https://bbs.archlinux.org/): Os fóruns são muitas vezes a primeira parada para usuários que procuram ajuda ou compartilhar ideias. Ainda que não exista uma solução, informações detalhadas e discussão adicional podem orientá-lo na direção certa.

*   [Rastreador de Erros do Arch Linux](https://bugs.archlinux.org/): Seu problema talvez já tenha sido relatado aos desenvolvedores do Arch Linux. Relatórios de erros duplicados são inúteis e prontamente fechados. Pesquisa por tanto **[relatório de erros fechados recentemente](https://bugs.archlinux.org/index.php?string=&project=1&status%5B%5D=closed&closedfrom=-1+week)** como os relatórios abertos. Lembre-se de marcar "search details" (detalhes da pesquisa) e/ou "search comments" (pesquisar comentários) em Advanced, pois o título do relatório pode não conter o texto que você está procurando.

*   [Google](https://www.google.com) ou seu mecanismo de pesquisa favorito: Pesquise usando o nome do programa, versão e uma parte relevante da mensagem de erro, se houver.

*   Fórum, lista de discussão e rastreador de erro do **Upstream**: Se o Arch Linux não é responsável por um erro, ele deve ser relatado no upstream em vez do Rastreador de Erros do Arch Linux. Procure os erros recentemente fechados, bem como relatórios abertos. Erros podem já ter sido corrigidos na versão de desenvolvimento do programa.

*   **Fóruns de outras distribuições**: A comunidade de software livre é vasta; usuários do Arch não são os únicos usuários com ideias! Considere pesquisar nos [Fóruns do Gentoo](https://forums.gentoo.org/), [FedoraForum.org](http://forums.fedoraforum.org/) e [Fóruns do Ubuntu](https://ubuntuforums.org/), por exemplo.

### Upstream ou Arch?

Arch Linux é uma *distribuição* GNU/Linux. Desenvolvedores do Arch e Trusted Users são responsáveis por compilar, empacotar e distribuir software de uma ampla gama de fontes. **Upstream** refere-se àqueles *fontes* – os autores originais ou mantenedores do software que é distribuído no Arch Linux. Por exemplo, o popular navegador web Firefox é desenvolvido pelo Projeto Mozilla.

**Se o Arch não for responsável por um erro, o problema não será resolvido relatando o erro aos desenvolvedores do Arch.** A responsabilidade por um erro é dito ser do upstream quando não é causado pelos esforços de distribuição e integração da distribuição.

Ao relatar erros ao upstream, você não só ajudará os usuários e desenvolvedores do Arch, mas também ajudará outras pessoas na comunidade de software livre, pois a solução afetará todas as distribuições.

Assim que você relatar um erro no upstream ou encontrar outras informações relevantes do upstream, pode ser útil publicar isso no rastreador de erros do Arch, de modo que os desenvolvedores e os usuários do Arch sejam informados disso.

Então, pelo que o Arch Linux é responsável?

*   [Projetos do Arch Linux](https://projects.archlinux.org/): [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"), [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") e sites do Arch. Se você tiver dúvidas sobre se o projeto pertence ao Arch ou obtenha estas informações do pacote (`pacman -Qi *nome_pacote*` ou usando o site) e veja o URL do upstream.

*   **Empacotamento**: O empacotamento basicamente consiste em buscar o código fonte do upstream, compilando-o com as opções relevantes, certificando-se de que ele será instalado corretamente em um sistema Arch e verificando se a funcionalidade principal funciona. O empacotamento no Arch não consiste em adicionar novas funcionalidades ou patches para erros existentes; este é o trabalho do desenvolvedor upstream.

Se um erro/recurso não está sob a responsabilidade do Arch, relate-o ao upstream. Veja também [#Motivos para não ser um erro](#Motivos_para_n.C3.A3o_ser_um_erro).

### Erro ou recurso?

	erro *(bug)*

	alguma coisa que deve funcionar, mas não funciona, contrário às intenções dos desenvolvedores.

	recruso *(feature)*

	alguma coisa que o software faz ou faria se alguém o codificasse.

#### Motivos para não ser um erro

*   Algo que você gostaria que uma parte do software fizesse, o que não foi implementado pelos desenvolvedores upstream. Em resumo: **um novo recurso**.
*   Um erro já realtado no upstream.
*   Um erro já corrigido no upstream, mas não no Arch porque o pacote não está desatualizado.
*   **Um pacote que está atualizado**. Use o recurso **Flag Package Out-of-Date** no [site de pacotes do Arch](https://archlinux.org/packages/).
*   Um pacote que não usa patches do Fedora, Ubuntu ou outra comunidade. **Patches devem ser enviados para o *upstream***.
*   Um pacote que a **função não essencial** X ou a função Y não estejam ativados. Isso é uma requisição de recurso.
*   Um pacote que não inclui um **arquivo .desktop** ou **ícones** ou outra coisa do [freedesktop](https://www.freedesktop.org). Este não é um erro se tais arquivos não estiverem incluídos no tarball fonte, e isso deve ser solicitado como uma requisição de recurso no *upstream*. Se esses arquivos forem fornecidos pelo *upstream*, mas não utilizados na empacotamento, então isso é um erro.

#### Motivos para não ser um recurso

*   Quando é um erro...
*   Quando não estiver sob a responsabilidade do Arch implementar o recurso, ou seja, um **recurso do upstream**.
*   Um pacote não está atualizado. Use o recurso **Flag Package Out-of-Date** em [site de pacotes do Arch](https://archlinux.org/packages/).
*   Um pacote que não usa patch do Fedora, Ubuntu ou de alguma outra comunidade. **Os patches devem ser enviados para o *upstream***.

### Colete informações úteis

Aqui está uma lista de informações úteis que devem ser mencionadas no seu relatório de erros:

*   **Versão do pacote** sendo usado. **Sempre especifique a versão do pacote**. Dizer "a última", "atual" ou "o pacote no extra" não tem nenhuma sentido. Especialmente se o erro não está para ser corrigido imediatamente.

*   Versão das principais bibliotecas utilizadas pelo pacote (disponível na variável *depends* no PKGBUILD), quando estão envolvidas no problema. Se você não sabe exatamente quais informações fornecer, espere que um caçador de bugs peça a você...

*   Versão do kernel usada se você está tendo problemas relacionados ao hardware.

*   Indique se **a funcionalidade funcionou em algum momento** ou não. Se sim, indique desde quando parou de funcionar.

*   Indique a sua **marca de hardware** quando tiver problemas relacionados com hardware

*   Adicione **informações de log relevantes** quando estiver disponível. Isso pode ser obtido nos seguintes locais, dependendo do problema:
    *   [Journal do systemd](/index.php/Systemd_(Portugu%C3%AAs)#Journal "Systemd (Português)"). Se estiver usando [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng), `/var/log/messages` contém logs relacionados a kernel e problemas relacionados ao hardware.
    *   `~/.local/share/xorg/Xorg.0.log` ou `/var/log/Xorg.0.log` ou `/var/log/Xorg.2.log` ou a qualquer arquivo de log tipo Xorg se problemas relacionados a vídeo (nvidia, ati, xorg...)
    *   Execute seu programa em um **console** e use o modo **verboso** *(verbose)* e/ou **depuração** *(debug)* se disponível (veja a documentação do programa) e copie a saída em um arquivo. Ao executar um aplicativo em um terminal, certifique-se de que informações relevantes serão exibidas em **inglês**, de forma que mais pessoas possam entendê-la. Isso pode ser feito usando `export LC_ALL="C"`. Exemplifique com um software chamado *foobar* do qual você gostaria de ter informações relevantes em tempo de execução e considerando que *foobar* tem uma opção `--verbose`:

```
$ export LC_ALL="C"
$ foobar --verbose

```

Isso afetará apenas o terminal atual e parará de funcionar quando o terminal for fechado.

Se você tiver que colar muito texto, como a saída do dmesg, ou um log do Xorg, é preferível salvá-lo como um arquivo no seu computador e anexá-lo ao seu relatório de erros. Anexar um arquivo em vez de usar um pastebin para apresentar informações relevantes é preferível em geral, devido ao fato de que o conteúdo colocado em um pastebin pode ter seu link expirado ou quaisquer outros problemas potenciais. **Anexar um arquivo garante que as informações fornecidas estarão sempre disponíveis**.

*   **Indique como reproduzir o erro**. Isso é muito importante, ajudará as pessoas a testar o erro e possíveis patches em seu próprio computador.

*   **O rastro da pilha** *(stack trace)*. É uma lista de chamadas feitas pelo programa durante sua execução e ajuda a encontrar a parte do programa onde o erro está localizado, especialmente se o erro envolver o travamento do programa. Você pode obter um rastro de pilha usando [gdb](https://www.archlinux.org/packages/?name=gdb) (O GNU Debugger) como explicado em [Depuração - Obtendo Rastros#Obtendo o rastro](/index.php/Depura%C3%A7%C3%A3o_-_Obtendo_Rastros#Obtendo_o_rastro "Depuração - Obtendo Rastros").

## Abrindo um relatório

Quando tiver certeza de que é um erro ou um recurso e você coletou todas as informações úteis, então você está pronto para abrir um relatório de erro ou solicitação de recurso.

### Criando uma conta

Você tem que criar uma conta no [sistema de rastreamento de erros do Arch](https://bugs.archlinux.org/). Isso é tão fácil quanto criar uma conta em um wiki ou um fórum e não há nada de especial para mencionar aqui.

### Projetos

Depois de determinar que seu recurso ou bug está relacionado ao Arch e não a um problema de upstream, será necessário relatar seu problema no projeto correto. Selecione o projeto na lista suspensa *à esquerda do botão "Swtich"* no canto superior esquerdo da página de criação de relatórios de erros (*não* à direita de "Category"). Existem cinco projetos:

*   **Arch Linux** - para pacotes em *testing*, *core* ou *extra*. Também é um lugar para documentação, sites (exceto AUR) e problemas de segurança.

*   **Arch User Repository (AUR)** - para o código do site do AUR e problemas em seu servidor. Isso não inclui aplicativos de terceiros usados para acessar o AUR ou pacotes no *unsupported*.

*   **Community Packages** - para pacotes no *community*. Não é um lugar para pacotes no *unsupported*.

*   **Pacman** - para [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") e os scripts e ferramentas oficiais associadas a ele. Isso inclui coisas como o makepkg. Isso não inclui pacotes desenvolvidos pela comunidade, como os [auxiliares do AUR](/index.php/Auxiliares_do_AUR "Auxiliares do AUR").

*   **Release Engineering** - destinado a todos os problemas relacionados à lançamentos (isos, instalador etc.)

Não há lugar para relatar problemas com pacotes no *unsupported*. O AUR fornece uma maneira de adicionar comentários a um pacote no *unsupported*. Você deve usar isso para relatar erros ao mantenedor do pacote.

### Resumo

Por favor, escreva um resumo *(Summary)* conciso e descritivo.

Aqui está uma lista de recomendações:

*   **Não** nomeie seu relatório "*pkgname* is broken after the last update" - isso não é descritivo e "after the last update" não tem sentido no Arch.
*   Inicie o Summary com o nome do pacote envolto com colchetes, p. ex.. "**[*pkgname*]** 3.0.5-1 breaks copy-paste feature". Ao nomear relatórios dessa forma, você facilita para desenvolvedores a ordenarem relatórios por nomes de pacotes.
*   Não escreva muito texto no Summary. Texto excessivo não será visível na lista de relatórios.

### Severidade

Escolher uma severidade *crítica* (em inglês, *Severity*) não ajudará a resolver o erro mais rápido. Isso só tornará os problemas realmente críticos menos visíveis e provavelmente fará com que o desenvolvedor atribuído ao seu relatório fique menos aberto para corrigi-lo.

Aqui está um uso geral de severidades:

*   **Critical** - Queda do sistema, falha grave de inicialização que provavelmente afetará mais do que apenas você ou um problema de segurança explorável em um pacote de serviços principal ou externo.
*   **High** - A principal funcionalidade do aplicativo não funciona, menos problemas críticos de segurança, etc.
*   **Medium** - Uma funcionalidade não essencial não funciona, padrões UNIX não são respeitados, etc.
*   **Low** - Uma funcionalidade opcional (plug-in ou compilação ativado) não funciona.
*   **Very Low** - Erro de tradução ou documentação. Algo que realmente não importa muito, mas deve ser notado para uma versão futura.

### Incluindo informações relevantes

This is maybe one of the most difficult parts of bug reporting. You have to choose from the section [#Gather useful information](#Gather_useful_information) which information you will add to your bug report. This will depend on which your problem is. If you do not know what the relevant pieces of information are, do not be shy: **it is better to give more information than needed than not enough**.

A good tutorial on reporting bugs can be found at [[1]](https://www.chiark.greenend.org.uk/~sgtatham/bugs.html).

However, developers or bug hunters will ask you for more information if needed. Fortunately after a few bug reports you will know what information should be given.

Short information can be inlined in your bug report, whereas **long information (logs, screenshots...) should be attached**.

## Acompanhando relatórios

**Do not think the work is done once you have reported a bug**!

Developers or other users will probably ask you for more details and give you some potential fixes to try. Without continued feedback, bugs cannot be closed and the end result is both angry users and developers.

### Votando e monitorando

You can **vote** for your favourite bugs. The number of votes indicates to the developers how many people are impacted by the bug. However, this is not a very effective way of getting the bug solved. Much more important would be posting any additional information you know about the bug if you were not the original reporter.

**Watching** a bug is important - you will receive an email when new comments are added or the bug status has changed. If you opened a bug, verify that the "Notify me whenever this task changes" checkbox is activated in order to receive such emails.

### Respondendo solicitações de informações adicionais

People will take the time to look at your bug report and will try to help you. You need to continue to help them resolve your bug. Not answering to their questions will keep your bug unresolved and likely hamper enthusiasm to fix it.

**Please take the time to give people more information if requested and try the solutions proposed**.

Developers or bug hunters will close your bug if you do not answer questions after a few weeks or a month.

### Atualizando o relatório de erro quando surgir uma nova versão do software relatado

Sometimes a bug is related to a given package version and is fixed in a new version. If this is the case then indicate it in the bug report comments and request a closure.

### Fechando quando resolvido

Sometimes people report a bug but do not notify when they have solved it on their own, leaving people searching for a solution that has already been found. Please request a closure if you found a solution and give the solution in the bug report comments.

### Mais sobre status de relatórios

During its life a bug goes through several states:

*   **Unconfirmed** - This is the default state. You have just reported it and nobody managed to reproduce the problem or confirmed that it is actually a bug.

*   **New** - The bug is confirmed but it has not been assigned to the developer responsible for the related software. It is usually the case when more investigation is needed to determine which software is responsible for the bug.

*   **Assigned** - The bug has been assigned to a developer responsible for the software involved in the bug. It does not mean that the developer will be the one who will fix the bug. It does not even mean that the developer will work on a solution. It just means that the developer will take care of the life cycle of the bug, including reviewing patches if any, releasing a fix and closing the bug when required. There is no point in contacting a developer directly to have a bug fixed more quickly, he/she will certainly not like it...

*   **Researching** - Somebody is looking for a solution. This status is **rarely used at Arch** and it is better this way. The *researching* status could make people believe they do not need to get interested in the bug report. But usually we need more than one person to fix a bug: having several experienced people on a bug helps a lot.

*   **Waiting on Response** and **Requires testing** - The one who reported a bug is asked to provide more information or to try a proposed solution, but he/she did not give a feedback yet. Those status are **rarely used at Arch** and should be used more often. However it is important that you **watch the bug** (see the [#Voting and Watching](#Voting_and_Watching) section) as developers or bug hunters usually ask questions in the comments.

*   **A task closure has been requested** - This is not exactly a status, but you may find some bug reports with such a notification. This indicates that somebody requested a closure for the bug. A reason is added to the request most of the time. It is upon the assignee developer to decide whether he/she will accept the closure or not.

*   **Closed** - Either this is not a valid bug (see [#Reasons for not being a bug](#Reasons_for_not_being_a_bug)) or a solution has been found and released.

Some people (developers, TUs...) are responsible for dispatching the bugs and change their status.