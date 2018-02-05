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

Here is a list of useful information that should be mentioned in your bug report:

*   **Version of the package** being used. **Always specify package version**. Saying "the latest", "todays", or "the package in extra" have absolutely no meaning. Especially if the bug is not about to get fixed right away.

*   Version of the main libraries used by the package (available in the *depends* variable in the PKGBUILD), when they are involved in the problem. If you do not know exactly what information to provide then wait for a bug hunter to ask you for it...

*   Version of the kernel used if you are having hardware related problems.

*   Indicate whether or not **the functionality worked at one time or not**. If so, indicate since when it stopped working.

*   Indicate your **hardware brand** when you are having hardware related problems

*   Add **relevant log information** when any is available. This can be obtained in the following places depending on the problem:
    *   [systemd journal](/index.php/Systemd_journal "Systemd journal"). If using [syslog-ng](https://www.archlinux.org/packages/?name=syslog-ng), `/var/log/messages` contains logs related to kernel and hardware related issues.
    *   `~/.local/share/xorg/Xorg.0.log` or `/var/log/Xorg.0.log` or `/var/log/Xorg.2.log` or any Xorg like log files if video related problems (nvidia, ati, xorg...)
    *   Run your program in a **console** and use **verbose** and/or **debug** mode if available (see your program documentation), and copy the output in a file. When running an application in a terminal make sure relevant information will be displayed in **English** so that many people can understand it. This can be done by using `export LC_ALL="C"`. Example with a software named *foobar* from which you would like to have relevant information at runtime and provided that *foobar* has a `--verbose` option:

```
$ export LC_ALL="C"
$ foobar --verbose

```

This will affect only the current terminal and will stop taking effect when the terminal is closed.

If you have to paste a lot of text, like the output of dmesg, or a Xorg log, is it preferred to save it as a file on your computer and attach it to your bug report. Attaching a file rather than using a pastebin to present relevant information is preferable in general due to the fact that pastebined content may suffer by expired links or any other potential problems. **Attaching a file guarantees the provided information will always be available**.

*   **Indicate how to reproduce the bug**. This is very important, it will help people test the bug and potential patches on their own computer.

*   **The stack trace**. It is a list of calls made by the program during its execution, and helps in finding part of the program where the bug is located, especially if bug involves the program crashing. You can obtain a stack trace using [gdb](https://www.archlinux.org/packages/?name=gdb) (The GNU Debugger) as explained in [Debug - Getting Traces#Getting the trace](/index.php/Debug_-_Getting_Traces#Getting_the_trace "Debug - Getting Traces").

## Abrindo um relatório

When you are sure it is a bug or a feature and you gathered all useful information, then you are ready to open a bug report or feature request.

### Criando uma conta

You have to create an account on [Arch's bug tracker system](https://bugs.archlinux.org/). This is as easy as creating an account on a wiki or a forum and there is nothing particular to mention here.

### Projetos

Once you have determined your feature or bug is related to Arch and not an upstream issue, you will need to file your problem in the correct project. Select the project in the drop down list *to the left of the "Switch" button* in the top left corner of the bug report creation page (*not* to the right of "Category"). There are five projects:

*   **Arch Linux** - for packages in *testing*, *core*, or *extra*. It is also a place for documentation, websites (except AUR), and security issues.

*   **Arch User Repository (AUR)** - for the AUR website code and server issues. This does not include third party apps used to access the AUR or packages in *unsupported*.

*   **Community Packages** - for packages in *community*. It is not a place for packages in *unsupported*.

*   **Pacman** - for [pacman](/index.php/Pacman "Pacman") and the official scripts and tools associated with it. This includes things like makepkg and abs. It does not include community developed packages such as [AUR helpers](/index.php/AUR_helpers "AUR helpers").

*   **Release Engineering** - intended for all release related issues (isos, installer, etc)

There is no place for reporting problems with packages in *unsupported*. The AUR provides a way to add comments to a package in *unsupported*. You should use this to report bugs to the package maintainer.

### Resumo

Please write a concise and descriptive Summary.

Here is a list of recommendations:

*   **Do not** name your report "*pkgname* is broken after the last update" - it is non-descriptive and "after last update" has no meaning in Arch.
*   Start the Summary with package name enclosed in square brackets, e.g. "**[*pkgname*]** 3.0.5-1 breaks copy-paste feature". By naming reports this way you make it much easier for developers to sort reports by package names.
*   Do not write too much text in the Summary. Excessive text will not be visible in reports list.

### Severidade

Choosing a *critical* severity will not help to solve the bug faster. It will only make truly critical problems less visible and probably make the developer assigned to your bug a bit less open to fixing it.

Here is a general usage of severities:

*   **Critical** - System crash, severe boot failure that is likely to affect more than just you, or an exploitable security issue in either a core or outward-facing service package.
*   **High** - The main functionality of the application does not work, less critical security issues, etc.
*   **Medium** - A non-essential functionality does not work, UNIX standards not respected, etc.
*   **Low** - An optional functionality (plugin or compilation activated) does not work.
*   **Very Low** - Translation or documentation mistake. Something that really does not matter much but should be noticed for a future release.

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