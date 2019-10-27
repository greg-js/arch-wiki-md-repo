**Status de tradução:** Esse artigo é uma tradução de [Arch Testing Team](/index.php/Arch_Testing_Team "Arch Testing Team"). Data da última tradução: 2019-10-20\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Arch_Testing_Team&diff=0&oldid=583812) na versão em inglês.

O Equipe de Teste do Arch é um grupo dentro da comunidade Arch responsável por garantir que os pacotes enviados para os repositórios [*testing*](/index.php/Testing_(Portugu%C3%AAs) "Testing (Português)") estejam funcionais. Isto inclui, certificar-se que o pacote é instalado corretamente, que não causa quebra com pacotes dos quais ele depende, entre outros.

Os Testadores do Arch [assinam](/index.php/DeveloperWiki:CoreSignoffs "DeveloperWiki:CoreSignoffs") pacotes após comprovar sua exatidão para que eles possam ser movidos dos repositórios de teste para os repositórios centrais, extras ou comunitários.

## Contribuindo

Você pode se candidatar a se tornar um testador oficial do Arch entrando em contato com [Florian Pritz](https://www.archlinux.org/people/developers/#bluewind) por [e-mail](mailto:bluewind@xinu.at) e requisitando uma [conta de testador](https://lists.archlinux.org/pipermail/arch-dev-public/2016-July/028191.html).

Se você receber uma conta do testador, poderá fazer login no [archweb](https://www.archlinux.org/devel) e ver uma aba de *signoffs*. A aba *signoffs* conterá uma lista de pacotes que estão atualmente nos repositórios de testes e precisam de pelo menos duas *assinaturas* (isto é, um carimbo confirmando a correção de um pacote).

Você pode então testar os pacotes listados localmente e assiná-los se estiverem corretos, clicando no botão *signoff* de cada pacote.

**Dica:** Você pode simplificar o processo assinando pacotes a partir da linha de comando com [signoff(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/signoff.1) do pacote [arch-signoff](https://www.archlinux.org/packages/?name=arch-signoff).

## Diretrizes

Para testar um pacote do Arch, lembre-se dos seguintes aspectos:

*   Se você está testando um kernel ou um pacote que depende dos módulos do kernel, você **deve reiniciar a máquina e garantir que ela inicialize corretamente**.
*   Embora o teste em software de virtualização não seja proibido, pode não ser tão útil quanto testar um pacote em uma instalação em um computador físico. Isso se aplica especialmente aos pacotes suscetíveis a diferentes tipos de hardware, como pacotes do kernel.
*   Se você estiver testando uma biblioteca, talvez queira executar um binário que use essa biblioteca. Certifique-se de que o arquivo de objeto compartilhado esteja carregado usando o *ldd*.
*   Da mesma forma, se houver um pacote que fornece pacotes executáveis, é recomendável testar sua funcionalidade básica.
*   Se você notar um erro ao testar um pacote, adicione um relatório de erro detalhado no [rastreador de erros](https://bugs.archlinux.org/) com:
    *   Nome do pacote, versão e pkgrel
    *   Qual componente do pacote apresentou o erro (por exemplo, um dos binários, ou um arquivo de configuração)
    *   Raiz do erro (por exemplo, durante a instalação ou uso, etc.)
    *   Quaisquer mensagens/logs de erro relevantes
    *   Certifique-se que o relatório de erro seja preenchido com a categoria *Packages: Testing*

## Coordenação

Você pode coordenar com outros testadores no canal IRC [#archlinux-testing](ircs://chat.freenode.net/archlinux-testing).

Você pode seguir atualizações por atividade de empacotador na lista de discussão [arch-commits](https://lists.archlinux.org/pipermail/arch-commits) (muito tráfego).