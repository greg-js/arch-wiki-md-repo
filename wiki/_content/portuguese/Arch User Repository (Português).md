O [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") (AUR), ou Repositório de Usuário do Arch, é um repositório dirigido pela comunidade para usuários do Arch. Ele contém descrições de pacotes (PKGBUILDs) que permitem a você compilar um pacote de um fonte com o [makepkg](/index.php/Makepkg "Makepkg") e depois instalar via [pacman](/index.php/Pacman "Pacman"). O AUR foi criado para organizar e compartilhar novos pacotes da comunidade e ajudar a acelerar a inclusão dos pacotes populares no repositório [[community]](#.5Bcommunity.5D). Este documento explica como usuários podem acessar e utilizar o AUR.

Um bom número de novos pacotes que entram para os repositórios oficiais iniciam no AUR. No AUR, usuários são capazes de contribuir com seus próprios pacotes (PKGBUILD e arquivos relacionados). A comunidade do AUR tem a capacidade de votar a favor ou contra os pacotes no AUR. Se um pacote se torna popular o bastante -- desde que tenha uma licença compatível e uma boa técnica de empacotamento -- ele pode ser colocado no repositório da [[community]](#.5Bcommunity.5D) (diretamente acessível pelo [pacman](/index.php/Pacman "Pacman") ou [abs](/index.php/ABS "ABS")).

## Contents

*   [1 Começando](#Come.C3.A7ando)
*   [2 História](#Hist.C3.B3ria)
*   [3 Pesquisando](#Pesquisando)
*   [4 Instalando pacotes](#Instalando_pacotes)
    *   [4.1 Pré-requisitos](#Pr.C3.A9-requisitos)
    *   [4.2 Obter arquivos para compilação](#Obter_arquivos_para_compila.C3.A7.C3.A3o)
    *   [4.3 Compile o pacote](#Compile_o_pacote)
    *   [4.4 Instalar o pacote](#Instalar_o_pacote)
*   [5 Feedback](#Feedback)
*   [6 Compartilhando e mantendo pacotes](#Compartilhando_e_mantendo_pacotes)
    *   [6.1 Enviando pacotes](#Enviando_pacotes)
    *   [6.2 Mantendo pacotes](#Mantendo_pacotes)
    *   [6.3 Outras requisições](#Outras_requisi.C3.A7.C3.B5es)
*   [7 [community]](#.5Bcommunity.5D)
*   [8 Repositório Git](#Reposit.C3.B3rio_Git)
*   [9 FAQ](#FAQ)
    *   [9.1 O que é o AUR?](#O_que_.C3.A9_o_AUR.3F)
    *   [9.2 Que tipo de pacotes é permitido no AUR?](#Que_tipo_de_pacotes_.C3.A9_permitido_no_AUR.3F)
    *   [9.3 Como posso votar em pacotes no AUR?](#Como_posso_votar_em_pacotes_no_AUR.3F)
    *   [9.4 O que é um TU?](#O_que_.C3.A9_um_TU.3F)
    *   [9.5 Qual é a diferença entre o Arch User Repository e [community]?](#Qual_.C3.A9_a_diferen.C3.A7a_entre_o_Arch_User_Repository_e_.5Bcommunity.5D.3F)
    *   [9.6 Quantos votos são necessários para que um PKGBUILD seja transferido para [community]?](#Quantos_votos_s.C3.A3o_necess.C3.A1rios_para_que_um_PKGBUILD_seja_transferido_para_.5Bcommunity.5D.3F)
    *   [9.7 Como é que eu faço um PKGBUILD?](#Como_.C3.A9_que_eu_fa.C3.A7o_um_PKGBUILD.3F)
    *   [9.8 Estou a tentar fazer "pacman -S foo"; não está funcionando mas eu sei que está em [community]](#Estou_a_tentar_fazer_.22pacman_-S_foo.22.3B_n.C3.A3o_est.C3.A1_funcionando_mas_eu_sei_que_est.C3.A1_em_.5Bcommunity.5D)
    *   [9.9 Foo no AUR está desatualizado; o que faço?](#Foo_no_AUR_est.C3.A1_desatualizado.3B_o_que_fa.C3.A7o.3F)
    *   [9.10 Eu tenho um PKGBUILD que queria enviar; alguém pode verificá-lo para ver se ele tem algum erro?](#Eu_tenho_um_PKGBUILD_que_queria_enviar.3B_algu.C3.A9m_pode_verific.C3.A1-lo_para_ver_se_ele_tem_algum_erro.3F)
    *   [9.11 Foo no AUR não compila quando eu executo makepkg; o que devo fazer?](#Foo_no_AUR_n.C3.A3o_compila_quando_eu_executo_makepkg.3B_o_que_devo_fazer.3F)
    *   [9.12 Como o posso agilizar processo de compilação repetitivos?](#Como_o_posso_agilizar_processo_de_compila.C3.A7.C3.A3o_repetitivos.3F)
    *   [9.13 Como é que eu tenho acesso a pacotes não-suportados?](#Como_.C3.A9_que_eu_tenho_acesso_a_pacotes_n.C3.A3o-suportados.3F)
    *   [9.14 Como é que eu faço upload para o AUR sem usar a interface web?](#Como_.C3.A9_que_eu_fa.C3.A7o_upload_para_o_AUR_sem_usar_a_interface_web.3F)

## Começando

Os usuários podem pesquisar e baixar os PKGBUILDs da [Interface Web do AUR](https://aur.archlinux.org). Esses PKGBUILDs podem ser construídos dentro dos pacotes instaláveis usando [makepkg](/index.php/Makepkg "Makepkg"), e depois instalados usando pacman.

*   Certifique-se de que o grupo de pacotes [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) está instalado (`pacman -S base-devel`).
*   Leia o restante deste artigo para mais informações e um pequeno tutoria sobre a instalação de pacotes do AUR
*   Visite a [Interface Web do AUR](https://aur.archlinux.org) para se informar sobre acontecimentos e atualizações. Lá você também encontrará estatísticas e uma lista atualizada dos mais novos pacotes disponíveis no AUR.
*   Veja o [#FAQ](#FAQ) para respostas das questões mais comuns.
*   Você pode querer ajustar `/etc/makepkg.conf` para melhor otimizar a prioridade do seu processador para a construção dos pacotes do AUR. Uma melhora significante nos tempos de compilação pode ser realizada nos sistemas com multi-processadores ao ajustar a variável MAKEFLAGS. Os usuários podem também habilitar otimizações específicas de hardware no GCC via a variável CFLAGS. Veja o [makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf") para mais informações.

## História

Os itens a seguir são listados por motivos históricos, somente. Eles foram substituídos pelo o AUR e não estão mais disponíveis.

No começo, havia `ftp://ftp.archlinux.org/incoming` e as pessoas contribuíam simplesmente enviando o PKGBUILD, os arquivos suplementares e o próprio pacote construído para o servidor. O pacote e os arquivos associados mantiveram-se até um [Mantenedor de pacotes](/index.php/Package_Maintainer "Package Maintainer") ver o programa e adotá-lo.

Em seguida, o Trusted User Repositories nasceu. Certos indivíduos na comunidade foram habilitados a hospedar seus próprios repositórios para qualquer um usar. O AUR expandiu nesta base, com o objetivo de ser mais flexível e usável. Na verdade, os mantenedores do AUR ainda são referidos como TUs (Trusted Users).

## Pesquisando

A Interface Web do AUR pode ser encontrada [aqui](https://aur.archlinux.org/) e uma interface adequada para acessar o AUR por meio de script (por exemplo) pode ser encontrada [aqui](https://aur.archlinux.org/rpc.php)

As consultas pesquisam por nomes de pacotes e descrições por meio de uma comparação tipo MySQL. Isto permite critérios de pesquisa mais flexíveis (ex.: tentar pesquisar por 'tool%like%grep' em vez de 'tool like grep'). Se você precisa pesquisar por uma descrição que contenha '%', use '\%' como caractere de escape.

## Instalando pacotes

A instalação de pacotes do AUR é um processo relativamente simples. Essencialmente:

1.  Adquira o tarball contendo o [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") e quaisquer outros arquivos necessários.
2.  Extraia o tarball (preferivelmente em uma pasta especificamente para compilações do AUR).
3.  Execute [makepkg](/index.php/Makepkg "Makepkg") no diretório onde os arquivos foram salvos ("makepkg -s" vai automaticamente resolver as dependências com o pacman)
4.  Instale o pacote resultante com o [pacman](/index.php/Pacman "Pacman"):

	 `# pacman -U /caminho/para/pkg.tar.xz` 

[AUR helpers](/index.php/AUR_helpers "AUR helpers") (Auxiliares do AUR) adicionam um acesso transparente ao AUR. Suas funcionalidades pode variar, mas eles podem facilitar a pesquisa, aquisição, compilação e instalação de PKGBUILDs encontrados no AUR. Todos esses scripts podem ser encontrados no AUR.

**Nota:** Não há e nunca haverá um mecanismo _oficial_ para instalação do material compilado do AUR. Todos os usuários devem estar familiarizados com o processo de compilação.

O que segue abaixo é um exemplo detalhado da instalação de um pacote chamado "foo".

### Pré-requisitos

Primeiro, certifique-se de que as ferramentas necessárias estão instaladas. O grupo do pacote [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) deve ser suficiente; ele inclui o [make](https://www.archlinux.org/packages/?name=make) e outras ferramentas necessárias para a compilação do fonte.

**Atenção:** Os pacotes do AUR presumem que o [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) está instalado e não listarão os membros deste grupo como dependências, mesmo se os pacotes não puderem ser compilador sem eles. Por favor, certifique-se de que este grupo está instalado antes de se queixar sobre problemas de compilação.

```
# pacman -S base-devel

```

Em seguida, escolha um diretório de compilação apropriado. Um diretório de compilação é simplesmente um diretório no qual o pacote será criado ou "compilado", podendo ser qualquer diretório. Exemplos dos diretórios mais comuns são:

```
~/builds

```

ou se estiver usando o ABS (o [Arch Build System](/index.php/Arch_Build_System "Arch Build System")):

```
/var/abs/local

```

Para mais informações sobre o ABS, leia o artigo [Arch Build System](/index.php/Arch_Build_System "Arch Build System"). O exemplo usará `~/builds` como o diretório de compilação.

### Obter arquivos para compilação

Encontre o pacote no AUR. Isso pode ser feito usando o recurso de pesquisa (o campo de texto no topo da [Página inicial do AUR](https://aur.archlinux.org/)). Ao clicar no nome do aplicativo na lista de resultados de pesquisa, será mostrada uma página de informações sobre o pacote. Leia atentamente a descrição para confirmar que esse é o pacote desejado, veja quando o pacote foi atualizado pela última vez e leia quaiquer comentários.

Baixe os arquivos necessários para compilação clicando no link "Baixar o tarball" em "Ações do Pacote", no canto direito da tela. Esse arquivo deve ser salvo no diretório de construção, ou copiado para esse diretório, depois do download. Neste exemplo, o arquivo é chamado "foo.tar.gz" (o formato padrão é "pkgname".tar.gz, se ele foi submetido do modo certo).

### Compile o pacote

Extraia o tarball. Mude o diretório para o de compilação, se já não estiver lá, e extraia os arquivos de compilação

```
$ cd ~/builds
$ tar -xvzf foo.tar.gz

```

Isto deve criar um novo diretório chamado "foo" no diretório de construção.

**Atenção:** **Verifique com atenção todos os arquivos.** Entre no diretório recém-criado, e procure cuidadosamente por comandos maliciosos no `PKGBUILD` e em qualquer arquivo `.install`. `PKGBUILD`s são scripts em bash contendo funções para serem executadas pelo `makepkg`: essas funções podem conter _qualquer_ comando válido ou sintaxe Bash válida. Então, é totalmente possível que um `PKGBUILD` contenha comandos perigosos por malícia ou por ignorância por parte do autor. Já que o `makepkg` usa fakeroot (e nunca deveria ser executado como root), ainda há um certo nível de proteção, mas você nunca deveria contar somente nisso. Em caso de dúvida, NÃO compile o pacote e procure ajuda nos fóruns ou na lista de discussão.

```
$ cd foo
$ nano PKGBUILD
$ nano foo.install

```

Crie o pacote. Depois de confirmar, manualmente, a integridade dos arquivos, execute [makepkg](/index.php/Makepkg "Makepkg") como usuário normal no diretório de compilação.

```
$ makepkg -s

```

A opção `-s` usará o [sudo](/index.php/Sudo "Sudo") para instalar qualquer dependência necessária. Se o uso do sudo for indesejável, instale antes as dependências você mesmo, e exclua a opção `-s` do comando acima.

### Instalar o pacote

Instale o pacote usando o pacman. Um tarball deve ter sido criado, chamado:

```
<_nome da aplicação_>-<_número da versão_>-<'architecture_>.pkg.tar.gz_

```

Este pacote pode ser instalado usando o comando de "upgrade" do pacman:

```
# pacman -U foo-0.1-1-i686.pkg.tar.xz   

```

Esses pacotes instalados manualmente são chamados de pacotes "foreign" (extrangeiros) — pacotes cuja origem não advém de qualquer repositório conhecido pelo pacman. Para listar todos os pacotes extrangeiros:

```
$ pacman -Qm 

```

**Nota:** O exemplo acima é apenas um breve resumo do processo de compilação de pacotes. Uma visita as páginas do [makepkg](/index.php/Makepkg "Makepkg") e do [ABS](/index.php/Arch_Build_System "Arch Build System") fornecerá mais detalhes e é altamente recomendado (principalmente para usuários de primeira viagem).

## Feedback

A [Interface Web do AUR](https://aur.archlinux.org) possui um espaço para comentários que permite aos usuários fornecer sugestões e feedback ao contribuidor do PKGBUILD. Evite colar patches ou PKGBUILDs na seção de comentários. Eles logo tornam-se obsoletos e terminam tomando muito espaço sem necessidade. Ao invés disso, envie por e-mail os arquivos ao mantenedor ou até mesmo use um [pastebin](/index.php/Pastebin_Clients "Pastebin Clients").

Uma das atividades mais fáceis para **todos** os usuários do Arch é navegar no AUR e **votar** em seus pacotes prediletos, usando a interface online. Todos os pacotes são elegíveis para serem adotados por um TU (Trusted User) para a inclusão no repositório [community], e a contagem de votos é uma das coisas levadas em conta nesse processo; votar é do interesse de todos!

## Compartilhando e mantendo pacotes

O usuário tem um papel essencial no AUR, que não pode desenvolver seu potencial sem o suporte, envolvimento e a contribuição da comunidade de usuários como um todo. O ciclio de vida de um pacote do AUR começa e termina com o usuário, e requer que o usuário contribua de várias formas.

Usuários podem **compartilhar** PKGBUILDs usando o Arch User Repository, o qual não contém pacote binário algum, mas permite aos usuários enviar PKGBUILDs, que podem ser baixados por outros. Esses PKGBUILDs são totalmente não-oficiais e não foram examinados completamente, então eles devem ser usados por sua conta e risco.

### Enviando pacotes

Depois de se conectar à interface web do AUR, o usuário pode [enviar](https://aur.archlinux.org/pkgsubmit.php) um tarball em gzip (`.tar.gz`) de um diretório contendo arquivos de compilação para um pacote. O diretório dentro do tarball deve conter um `PKGBUILD`, quaisquer arquivos `.install`, patches, etc. (_absolutamente_ nenhum binário). Exemplos do que um diretório deve conter pode ser visto dentro de `/var/abs` se [Arch Build System](/index.php/Arch_Build_System "Arch Build System") tiver sido instalado.

O tarball pode ser criado com o seguinte comando:

```
$ makepkg --source

```

Note que esse é um tarball em gzip; supondo que você está submetendo ao AUR um pacote chamado _libfoo_, quando você criar o arquivo, ele deve parecer com:

 `# Lista do conteúdo de um tarball.` 

```
 $ tar tf libfoo-0.1-1.src.tar.gz
 libfoo/
 libfoo/PKGBUILD
 libfoo/libfoo.install
```

Ao enviar um pacote, deve-se observar as seguintes regras:

*   Verifique [core], [extra], e [community] a procura do pacote. Se ele está dentro de um desses repositórios em ALGUMA forma, NÃO envie o pacote (se o pacote atual está quebrado ou sem algum ter incluído algum recurso, favor criar um relatório de bug no [FlySpray](https://bugs.archlinux.org/)).
*   Verifique no AUR pelo pacote. Se ele já tem um mantenedor, alterações podem ser submetidas em comentários para chamar atenção do mantenedor. Se o pacote não tem um mantenedor, o pacote pode ser adotado e atualizado como precisar.
*   Verifique atentamente se o pacote que você está enviando está correto. Todos contribuidores devem ler e aderir aos [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards") quando estiver escrevendo PKGBUILDs. Isso é essencial para o funcionamento suave e sucesso como um todo do AUR. Lembre-se que você não vai ganhar nenhuma ou respeito de seus próximos gastando o tempo deles com PKGBUILDs ruins.
*   Pacotes que contém binários ou que são mal escritos podem ser deletados sem aviso.
*   Se você não tem certeza sobre o processo de empacotamento (ou de compilação/envio) de alguma forma, envie o PKGBUILD para a Lista de Discussão do AUR ou para sessões de AUR no forum para uma revisão pública antes de adicionar ao AUR.
*   Tenha certeza que o pacote é útil. Alguém mais vai querer esse pacote? Ele é extremamente especializado? Se mais do que poucas pessoas pensariam nesse pacote como útil, então é apropriado para ser submetido.
*   Adquira alguma experiência antes de enviar pacotes. Compile alguns pacotes para aprender o processo e depois envie.
*   Se você submeter um `package.tar.gz` com uma arquivo chamado '`package`' nele, você vai receber uma mensagem de erro: 'Não foi possível alterar o diretório `/home/aur/unsupported/package/package`'. Para resolver isso, renomeie o arquivo '`package`' para alguma coisa diferente. Por exemplo, '`package.rc`'. Quando ele estiver instalado no diretório `pkg` você pode renomeá-lo de volta para '`package`'.

### Mantendo pacotes

*   Se você mantém um pacote e deseja atualizar o PKGBUILD do seu pacote, basta reenviá-lo.
*   Verifique os feedback e comentários de outros usuários e tente incorporar quaisquer melhorias que eles sugerirem; considere isso um processo de aprendizado!
*   Por favor, não simplesmente envie e depois esqueça dos pacotes! É trabalho do mantenedor manter o pacote, verificando atualizações e melhorando o PKGBUILD.
*   Se você não quer mais continuar mantendo o pacote por algum motivo, basta abandonar (`disown`) o pacote usando a interface web do AUR e/ou postar uma mensagem na Lista de Discussão do AUR.

### Outras requisições

*   Requisições para abandono e requisições para remoção de pacotes devem ser enviadas para a lista de discussão aur-general direcionada para os TUs e outros usuários, para que seja decida pelos TUs.
*   **Inclua o nome do pacote e a URL para a página do AUR**, preferivelmente com uma nota de rodapé [1].
*   Requisições de abandono ("Disownment Requests") serão concedidas somente duas semanas após o atual mantenedor tenha sido contactado por e-mail e não havendo resposta dele.
*   **Mesclagem de pacotes foi implementada**. Os usuários têm que reenviar um pacote sob um novo nome e, então, podem requisitar a mesclagem (**Merge Requests**)de comentários e votos do pacote antigo para a lista de discussão.
*   Requisições de remoção (**Removal Requests**) precisam das seguintes informações:
    *   Nome do pacote e a URL da página no AUR
    *   Motivo para exclusão, com pelo menos uma nota curta
        **Repare:** Um comentário em um pacote não necessariamente demonstra de suficiente o motivo do porquê um pacote deve ser excluído. Isso porque assim que um TU realiza a exclusão, o único lugar que vai manter a tal informação será o e-mail na lista de discussão do aur-general.
    *   Incluir detalhes de suporte, como, por exemplo, quando um pacote é fornecido por outro pacote, se você é o mantenedor do pacote, ele foi renomeado e o dono original concordou, etc.

Requisições de remoção podem ser negadas, caso em que você provavelmente será aconselhado a abandonar o pacote para a referência de um possível futuro mantenedor.

## [community]

O repositório [community], mantido pelos [Trusted Users](/index.php/Trusted_Users "Trusted Users"), contém a maioria dos pacotes populares do UNSUPPORTED. Ele é habilitado por padrão no `pacman.conf`. Se desabilitado/removido, ele pode ser habilitado descomentando/adicionando essas duas linhas:

```
/etc/pacman.conf

```

```
...
[community]
Include = /etc/pacman.d/mirrorlist
...

```

[community], ao contrário do UNSUPPORTED, contém pacotes binários que podem ser instalados diretamente com o [pacman](/index.php/Pacman "Pacman") e os arquivos de compilação também podem ser acessados com o [ABS](/index.php/Arch_Build_System "Arch Build System"). Alguns desses pacotes podem eventualmente serem movidos para os repositórios [core] ou [extra], caso os desenvolvedores considerem como crucial para a distribuição.

Usuários também podem acessar os arquivos de compilação do [community] editando o `/etc/abs.conf` e habilitando o repositório community no vetor `REPOS`.

## Repositório Git

Um repositório Git do AUR é mantido por Thomas Dziedzic, contendo a história dos pacotes junto com outras coisas. É atualizado pelo menos uma vez por dia. Para clonar o repositório (várias centenas de MB):

```
$ git clone git://pkgbuild.com/aur-mirror.git

```

Mais informações: [interface Web](http://pkgbuild.com/git/aur-mirror.git/), [readme](http://pkgbuild.com/~td123/readme), [tópico no fórum](https://bbs.archlinux.org/viewtopic.php?id=113099).

## FAQ

### O que é o AUR?

O AUR (Arch User Repository) é um sítio onde a comunidade do Arch Linux pode fazer upload de [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") de aplicações, bibliotecas, etc., e compartilhá-los com toda a comunidade. Outros usuários poderão então votar pelos seus favoritos para que sejam transferidos para o repositório [community] de forma a serem compartilhados com os usuários do Arch Linux em forma de binário.

### Que tipo de pacotes é permitido no AUR?

Os pacotes no AUR são meramente "scripts de compilação", isto é, receitas para a compilação de binários para o pacman. Na maioria dos casos, tudo é permitido, sujeito à utilidade mencionada acima e ao escopo das diretrizes, desde que o pacote esteja em conformidade com os termos de licenciamento do conteúdo. Para a maioria dos casos, onde é mencionado que "você não pode vincular" a downloads, por exemplo, conteúdos que não são redistribuíveis, você somente pode usar o nome do arquivo como fonte. Isso significa que e requer que os usuários já tenham o fonte restrito no diretório de compilação antes de compilar o pacote. Quando tiver dúvidas, pergunte.

### Como posso votar em pacotes no AUR?

Registe-se no [AUR website](https://aur.archlinux.org/) para obter uma opção "Vote neste pacote" enquanto navega nos pacotes.

### O que é um TU?

Um [TU (Trusted User)](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") é uma pessoa que é escolhida para supervisionar o AUR e o repositório [community]. Eles são os que mantêm PKGBUILDs populares no [community], marcam PKGBUILDs como seguros e ao todo mantêm o AUR a funcionar.

### Qual é a diferença entre o Arch User Repository e [community]?

O Arch User Repository é onde todos os PKGBUILDs que os utilizadores submetem são guardados, e têm que ser construídos manualmente com [makepkg](/index.php/Makepkg "Makepkg"). Quando os PKGBUILDs recebem votos suficientes, eles são transferidos para o repositório [community], onde os TUs mantêm pacotes binários que podem ser instalados com o [pacman](/index.php/Pacman "Pacman").

### Quantos votos são necessários para que um PKGBUILD seja transferido para [community]?

Normalmente, são necessários pelo menos 10 votos para que alguma coisa seja transferida para [community]. Contudo, se um TU quiser dar suporte a um pacote, então este frequentemente vai ser encontrado no repositório.

### Como é que eu faço um PKGBUILD?

O melhor recurso é [Creating packages](/index.php/Creating_packages "Creating packages"). Não se esqueça de ver no AUR antes de criar o PKGBUILD de forma a não duplicar esforços.

### Estou a tentar fazer "pacman -S foo"; não está funcionando mas eu sei que está em [community]

Você provavelmente não habilitou o [community] no seu `/etc/pacman.conf`. Basta descomentar as linhas relevantes. Se [community] já está habilitado no seu `/etc/pacman.conf`, tente executar `pacman -S -y` primeiro para sincronizar o cache de pacotes antes de tentar instalar seu pacote novamente.

### Foo no AUR está desatualizado; o que faço?

Para começar, você pode marcar pacotes como desatualizados. Se ele ficar desatualizado por um longo período de tempo, a melhor coisa a ser feita é você mesmo escrever um e-mail para o mantenedor. Se não houver resposta do mantenedor, você pode escrever um e-mail para a lista de discussão aur-general requisitando que um TU torne o pacote órfão ("Disownment Request"), se você estiver disposto a mantê-lo. Quando estivermos falando de um pacote que está marcado como desatualizado por mais de 3 meses e em geral não teve atualização por muito tempo, por favor adicione esta informação na sua requisição.

### Eu tenho um PKGBUILD que queria enviar; alguém pode verificá-lo para ver se ele tem algum erro?

Se quiser ter o seu PKGBUILD criticado, envie-o para a lista de discussão aur-general para receber feedback dos TUs e de outros membros do AUR. Você também pode conseguir ajuda do [Canal IRC](/index.php/ArchChannel "ArchChannel"), #archlinux em irc.freenode.net. Você também pode usar o [namcap](/index.php/Namcap "Namcap") para verificar erros no seu PKGBUILD e no pacote resultante.

### Foo no AUR não compila quando eu executo makepkg; o que devo fazer?

Provavelmente está deixando escapar alguma coisa trivial.

1.  Execute `pacman -Syyu` antes de compilar qualquer coisa com `makepkg`, pois o problema pode ser que o seu sistema não está atualizado.
2.  Certifique-se de que tem ambos os grupos "base" e "base-devel" instalados.
3.  Tente usar a opção "`-s`" com `makepkg` para verificar e instalar todas as dependências necessárias antes de começar o processo de compilação.

Certifique-se de primeiro ler o PKGBUILD e os comentários na página do AUR do pacote em questão. O motivo pode não ser trivial. CFLAGS, LDFLAGS e MAKEFLAGS personalizadas podem causar falhas. Também é possivel que o PKGBUILD esteja realmente incorreto para todos. Se não consegue descobrir por si mesmo, relate o problema ao mantenedor. Por exemplo, postar nos comentários da página do AUR os erros que você está recebendo.

### Como o posso agilizar processo de compilação repetitivos?

Se você frequentemente compila códigos que usam gcc - digamos, um pacote git ou SVN - você pode encontrar [ccache](/index.php/Ccache "Ccache"), que é o diminutivo para "compiler cache", útil.

### Como é que eu tenho acesso a pacotes não-suportados?

Veja [#Instalando pacotes](#Instalando_pacotes)

### Como é que eu faço upload para o AUR sem usar a interface web?

Você pode usar [burp](https://www.archlinux.org/packages/?name=burp), _aurploader_ ([python3-aur](https://aur.archlinux.org/packages/python3-aur/)) ou [aurup](https://aur.archlinux.org/packages/aurup/) — eles são programas de linah de comando.