Artigos relacionados

*   [dotfiles](/index.php/Dotfiles_(Portugu%C3%AAs) "Dotfiles (Português)")

Do [Wikipédia](https://en.wikipedia.org/wiki/pt:Shell_do_Unix "wikipedia:pt:Shell do Unix"):

	Um shell do Unix é um interpretador de linha de comando ou shell que fornece uma interface semelhante ao Unix tradicional. Os usuários indicam a operação do computador pela entrada de comandos como texto para um interpretador de linha de comando executar, ou criando scripts de texto de um ou mais de tais comandos.

## Contents

*   [1 Lista de shells](#Lista_de_shells)
*   [2 Alterando seu shell padrão](#Alterando_seu_shell_padr.C3.A3o)
*   [3 Arquivos de configuração](#Arquivos_de_configura.C3.A7.C3.A3o)
    *   [3.1 /etc/profile](#.2Fetc.2Fprofile)
*   [4 Veja também](#Veja_tamb.C3.A9m)

## Lista de shells

*   **[Bash](/index.php/Bash "Bash")** — Bash é um shell compatível com sh que incorpora recursos úteis do shell Korn (ksh) e do C shell (csh). Ele se destina a se ajustar ao padrão de shells e ferramentas do IEEE POSIX P1003.2/ISO 9945.2\. Ele oferece melhorias funcionais em relação ao sh para programação e uso interativo. Além disso, a maioria dos scripts sh podem ser executados pelo Bash sem modificações.

	[https://www.gnu.org/software/bash/](https://www.gnu.org/software/bash/) || [bash](https://www.archlinux.org/packages/?name=bash)

*   **[C shell](https://en.wikipedia.org/wiki/C_shell "wikipedia:C shell")** — Interpretador de linguagem de comando utilizável tanto como um shell de login interativo e um processador de comando de script de shell. Inclui um editor de linha de comando, completação de palavra programável, correção ortográfica, mecanismo de histórico, controle de trabalho e uma sintaxe tipo C.

	[http://www.tcsh.org](http://www.tcsh.org) || [tcsh](https://www.archlinux.org/packages/?name=tcsh)

*   **[DASH](/index.php/Dash "Dash")** — Implementação compatível com POSIX de `/bin/sh` que pretende ser tão pequena quanto possível. Ele faz isso sem sacrificar a velocidade, quando possível. Na verdade, é significativamente mais rápido que Bash (o GNU Bourne-Again SHell) para a maioria das tarefas.

	[http://gondor.apana.org.au/~herbert/dash/](http://gondor.apana.org.au/~herbert/dash/) || [dash](https://www.archlinux.org/packages/?name=dash)

*   **Elvish** — Elvish é um shell moderno e expressivo, que pode carregar valores internos estruturados por meio de *pipelines*. Esse recurso torna possível evitar um monte de código complexo de processamento de texto. Isso permite uma linguagem de programação mais efetiva, com recursos como exceções, espaço de nome e funções anônimas. Ele também possui um readline poderoso que verifica a sintaxe enquanto digita, e realce de sintaxe por padrão.

	[https://elvish.io](https://elvish.io) || [elvish](https://aur.archlinux.org/packages/elvish/)

*   **[fish](/index.php/Fish "Fish")** — Shell de linha de comando inteligente e amigável. O *fish* executa o realce da sintaxe da linha de comando em cores, bem como o realce e a completação dos comandos e dos argumentos, da existência do arquivo e do histórico. Ele oferece suporte à completação na medida em que você escreve para o histórico e os comandos. O fish é capaz de analisar as páginas man do sistema para determinar argumentos válidos para comandos, permitindo que ele realce e complete os comandos. Uma revisão fácil do último comando pode ser feita usando Alt-Up. O daemon de fish (fishd) facilita ter um histórico sincronizado em todas as instâncias do fish, bem como variáveis de ambiente universais e persistentes.

	[http://fishshell.com/](http://fishshell.com/) || [fish](https://www.archlinux.org/packages/?name=fish)

*   **[Korn shell](/index.php/Korn_shell "Korn shell")** — O KornShell possui uma linguagem de programação completa, poderosa e de alto nível para escrever aplicativos, muitas vezes mais fácil e rápido do que com outras linguagens de alto nível. Isso o torna especialmente adequado para prototipagem. O ksh tem as melhores características do Bourne shell e do C shell, além de muitos novos recursos próprios. Assim, o ksh pode fazer muito para melhorar sua produtividade e a qualidade do seu trabalho, tanto na interação com o sistema quanto na programação. Os programas ksh são mais fáceis de escrever e são mais concisos e legíveis do que os programas escritos em linguagem de nível inferior, como C.

	[http://www.kornshell.com](http://www.kornshell.com) || Veja [esse artigo](/index.php/Ksh#Installation "Ksh")

*   **[Nash](/index.php/Nash "Nash")** — Nash é um shell do sistema, inspirado pelo rc do plan9, que facilita a criação de scripts confiáveis e seguros, aproveitando os namespaces dos sistemas operacionais (no linux e no plan9) de forma idiomática.

	[https://github.com/NeowayLabs/nash](https://github.com/NeowayLabs/nash) || [nash-git](https://aur.archlinux.org/packages/nash-git/)

*   **Oh** — Shell de Unix escrito em Go. É semelhante em espírito, mas diferente em detalhes de outros shells de Unix. *Oh*, estende os recursos da linguagem de programação do shell sem sacrificar os recursos interativos do shell.

	[https://github.com/michaelmacinnis/oh](https://github.com/michaelmacinnis/oh) || [oh-git](https://aur.archlinux.org/packages/oh-git/)

*   **[powerShell](https://en.wikipedia.org/wiki/pt:PowerShell "wikipedia:pt:PowerShell")** — O PowerShell é uma linguagem de programação orientada a objetos e um shell de linha de comando interativo, originalmente escrito para e exclusivo para o Windows. Mais tarde, foi aberto e portado para Mac OS X e Linux.

	[https://github.com/PowerShell/PowerShell](https://github.com/PowerShell/PowerShell) || [powershell](https://aur.archlinux.org/packages/powershell/)

*   **[rc](https://en.wikipedia.org/wiki/rc "wikipedia:rc")** — Interpretador de comando para o Plan9 que fornece recursos semelhantes ao Bourne shell do UNIX, com algumas pequenas adições e menos sintaxe idiossincrática.

	[http://plan9.bell-labs.com/sys/doc/rc.html](http://plan9.bell-labs.com/sys/doc/rc.html) || [9base-git](https://aur.archlinux.org/packages/9base-git/)

*   **xonsh** — AUm shell retrocompatível com base no interpretador python.

	[http://xon.sh/](http://xon.sh/) || [xonsh](https://aur.archlinux.org/packages/xonsh/)

*   **[Zsh](/index.php/Zsh "Zsh")** — Shell projetado para uso interativo, embora também seja uma poderosa linguagem de script. Muitos dos recursos úteis de Bash, ksh e tcsh foram incorporados no Zsh; vários recursos originais foram adicionados. O [documento introdutório](http://zsh.sourceforge.net/Intro/intro_toc.html) detalha alguns dos recursos exclusivos do Zsh.

	[http://www.zsh.org/](http://www.zsh.org/) || [zsh](https://www.archlinux.org/packages/?name=zsh)

## Alterando seu shell padrão

Depois de instalar um dos shells acima, você pode executar esse shell dentro do seu shell atual, apenas executando o executável. Se você quiser ser servido nesse shell quando você fizer login no entanto, você precisará alterar seu shell padrão.

Para listar todos os shells instalados, execute:

```
$ chsh -l

```

E para definir um como padrão para seu usuário, faça:

```
$ chsh -s *caminho-completo-do-shell*

```

sendo *caminho-completo-do-shell* é o caminho completo como fornecido em `chsh -l`.

Se você agora você encerrar a sessão e iniciá-la novamente, você será saudado pelo outro shell.

## Arquivos de configuração

Para iniciar automaticamente programas no console ou no login, você pode usar os arquivos/diretórios de inicialização do shell. Leia a documentação do seu shell, ou seu artigo do ArchWiki, p. ex., [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") ou [Zsh#Startup/Shutdown files](/index.php/Zsh#Startup.2FShutdown_files "Zsh").

Veja também [Wikipedia:pt:Shell do Unix#Arquivos de configuração](https://en.wikipedia.org/wiki/pt:Shell_do_Unix#Arquivos_de_configura.C3.A7.C3.A3o "wikipedia:pt:Shell do Unix").

### /etc/profile

Após o login, todas os shells compatíveis com Bourne usam `/etc/profile`, o que, por sua vez, origina qualquer arquivo `*.sh` legível em `/etc/profile.d/`: estes scripts não requerem uma diretiva de interpretador, nem precisam ser executáveis. Eles são usados para configurar um ambiente e definir configurações específicas do aplicativo.

## Veja também

*   [Evolução de shells no Linux](http://www.ibm.com/developerworks/linux/library/l-linux-shells/index.html) no IBM developerWorks
*   [terminal.sexy](https://terminal.sexy/) — Designer de esquema de cores de terminal
*   [Hyperpolyglot](http://hyperpolyglot.org/unix-shells) — Comparação lado a lado das sintaxes do shell
*   [UNIX Power Tools](http://docstore.mik.ua/orelly/unix/upt/index.htm) — Uso geral da ferramenta de linha de comando
*   [commandlinefu.com](https://www.commandlinefu.com/commands/browse) — Compartilhamento de trechos de linha de comando
*   [List of applications#Terminal emulators](/index.php/List_of_applications#Terminal_emulators "List of applications")