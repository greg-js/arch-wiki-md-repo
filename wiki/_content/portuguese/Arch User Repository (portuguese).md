**Status de tradução:** Esse artigo é uma tradução de [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Data da última tradução: 2019-08-09\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Arch_User_Repository&diff=0&oldid=577636) na versão em inglês.

Artigos relacionados

*   [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)")
*   [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")
*   [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)")
*   [.SRCINFO](/index.php/.SRCINFO_(Portugu%C3%AAs) ".SRCINFO (Português)")
*   [Interface RPC do Aurweb](/index.php/Interface_RPC_do_Aurweb "Interface RPC do Aurweb")
*   [Diretrizes de envio ao AUR](/index.php/Diretrizes_de_envio_ao_AUR "Diretrizes de envio ao AUR")
*   [Diretrizes de Trusted User do AUR](/index.php/Diretrizes_de_Trusted_User_do_AUR "Diretrizes de Trusted User do AUR")
*   [Repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais")
*   [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)")
*   [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes")
*   [Auxiliares do AUR](/index.php/Auxiliares_do_AUR "Auxiliares do AUR")

O Arch User Repository (AUR) ou, em português, Repositório de Usuário do Arch é um repositório dirigido pela comunidade para usuários do Arch. Ele contém descrições de pacotes ([PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)")) que permitem a você compilar um pacote de um fonte com o [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") e depois instalar via [pacman](/index.php/Pacman_(Portugu%C3%AAs)#Comandos_adicionais "Pacman (Português)"). O AUR foi criado para organizar e compartilhar novos pacotes da comunidade e ajudar a acelerar a inclusão dos pacotes populares no [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community"). Este documento explica como usuários podem acessar e utilizar o AUR.

Um bom número de novos pacotes que entram para os repositórios oficiais iniciam no AUR. No AUR, usuários são capazes de contribuir com seus próprios pacotes (`PKGBUILD` e arquivos relacionados). A comunidade do AUR tem a capacidade de votar a favor os pacotes no AUR. Se um pacote se torna popular o bastante -- desde que tenha uma licença compatível e uma boa técnica de empacotamento -- ele pode ser colocado no repositório *community* (diretamente acessível pelo *pacman* ou [abs](/index.php/Abs_(Portugu%C3%AAs) "Abs (Português)")).

**Atenção:** Os pacotes do AUR são conteúdo produzido por usuário. Qualquer uso dos arquivos fornecidos está por sua própria conta e risco.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Começando](#Começando)
*   [2 História](#História)
    *   [2.1 Repositórios Git para pacotes AUR3](#Repositórios_Git_para_pacotes_AUR3)
*   [3 Instalando pacotes](#Instalando_pacotes)
    *   [3.1 Pré-requisitos](#Pré-requisitos)
    *   [3.2 Obtendo arquivos de compilação](#Obtendo_arquivos_de_compilação)
    *   [3.3 Compilando e instalando o pacote](#Compilando_e_instalando_o_pacote)
*   [4 Feedback](#Feedback)
*   [5 Enviando pacotes](#Enviando_pacotes)
*   [6 Tradução da interface web](#Tradução_da_interface_web)
*   [7 Sintaxe de comentário](#Sintaxe_de_comentário)
*   [8 FAQ](#FAQ)
    *   [8.1 O que é o AUR?](#O_que_é_o_AUR?)
    *   [8.2 Que tipo de pacote é permitido no AUR?](#Que_tipo_de_pacote_é_permitido_no_AUR?)
    *   [8.3 Como posso votar em pacotes no AUR?](#Como_posso_votar_em_pacotes_no_AUR?)
    *   [8.4 O que é um Trusted User / TU?](#O_que_é_um_Trusted_User_/_TU?)
    *   [8.5 Qual é a diferença entre o Arch User Repository e repositório [community]?](#Qual_é_a_diferença_entre_o_Arch_User_Repository_e_repositório_[community]?)
    *   [8.6 Foo no AUR está desatualizado; o que devo fazer?](#Foo_no_AUR_está_desatualizado;_o_que_devo_fazer?)
    *   [8.7 Foo no AUR não compila quando eu executo makepkg; o que devo fazer?](#Foo_no_AUR_não_compila_quando_eu_executo_makepkg;_o_que_devo_fazer?)
    *   [8.8 ERRO: Uma ou mais assinaturas PGP não puderam ser verificadas!; o que eu devo fazer?](#ERRO:_Uma_ou_mais_assinaturas_PGP_não_puderam_ser_verificadas!;_o_que_eu_devo_fazer?)
    *   [8.9 Como eu crio um PKGBUILD?](#Como_eu_crio_um_PKGBUILD?)
    *   [8.10 Eu tenho um PKGBUILD que queria enviar; alguém pode verificá-lo para ver se ele tem algum erro?](#Eu_tenho_um_PKGBUILD_que_queria_enviar;_alguém_pode_verificá-lo_para_ver_se_ele_tem_algum_erro?)
    *   [8.11 Como que faz para um PKGBUILD ir para o repositório *community*?](#Como_que_faz_para_um_PKGBUILD_ir_para_o_repositório_community?)
    *   [8.12 Como o posso agilizar processo de repetidas compilações?](#Como_o_posso_agilizar_processo_de_repetidas_compilações?)
    *   [8.13 Qual é a diferença entre pacotes foo e foo-git](#Qual_é_a_diferença_entre_pacotes_foo_e_foo-git)
    *   [8.14 Por que foo desapareceu do AUR?](#Por_que_foo_desapareceu_do_AUR?)
    *   [8.15 Como eu descubro se algum dos meus pacotes instalados desapareceu do AUR?](#Como_eu_descubro_se_algum_dos_meus_pacotes_instalados_desapareceu_do_AUR?)
    *   [8.16 Como eu posso obter uma lista de todos os pacotes do AUR?](#Como_eu_posso_obter_uma_lista_de_todos_os_pacotes_do_AUR?)
*   [9 Veja também](#Veja_também)

## Começando

Os usuários podem pesquisar e baixar os [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") da [Interface Web do AUR](https://aur.archlinux.org). Esses `PKGBUILD`s podem ser construídos dentro dos pacotes instaláveis usando *makepkg*, e depois instalados usando *pacman*.

*   Certifique-se de que o grupo de pacotes [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) está todo instalado (`pacman -S --needed base-devel`).
*   Veja o [#FAQ](#FAQ) para respostas das questões mais comuns.
*   Você pode querer ajustar `/etc/makepkg.conf` para melhor otimizar a prioridade do seu processador para a construção dos pacotes do AUR. Uma melhora significante nos tempos de compilação pode ser realizada nos sistemas com processadores multi-cores ao ajustar a variável `MAKEFLAGS`. Os usuários também podem habilitar otimizações específicas de hardware no [GCC](/index.php/GCC_(Portugu%C3%AAs) "GCC (Português)") por meio da variável `CFLAGS`. Veja [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") para mais informações.

Também é possível interagir com o AUR por meio de SSH: digite `ssh aur@aur.archlinux.org help` para uma lista de comandos disponíveis.

## História

No começo, havia `ftp://ftp.archlinux.org/incoming` e as pessoas contribuíam simplesmente enviando o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"), os arquivos suplementares e o próprio pacote construído para o servidor. O pacote e os arquivos associados mantiveram-se até um [Mantenedor de pacote](/index.php/Arch_terminology_(Portugu%C3%AAs)#Package_maintainer "Arch terminology (Português)") ver o programa e adotá-lo.

Em seguida, os Trusted User Repositories nasceram. Certos indivíduos na comunidade foram habilitados a hospedar seus próprios repositórios para qualquer um usar. O AUR expandiu nesta base, com o objetivo de ser mais flexível e usável. Na verdade, os mantenedores do AUR ainda são referidos como TUs (Trusted Users).

Entre 2015-06-08 e 2015-08-08, o AUR mudou da versão 3.5.1 para 4.0.0, introduzindo o uso de repositórios Git para publicação dos `PKGBUILD`s. Os pacotes existentes foram descartados, a menos que migrados manualmente para a nova infraestrutura por seus mantenedores.

### Repositórios Git para pacotes AUR3

O [Arquivo do AUR](https://github.com/aur-archive) no GitHub possui um repositório para cada repositório que estava no AUR 3 durante a migração para o AUR 4 em Agosto de 2015. Alternativamente, há o repositório [aur3-mirror](https://github.com/felixonmars/aur3-mirror/) que fornece o mesmo conteúdo.

## Instalando pacotes

A instalação de pacotes do AUR é um processo relativamente simples. Essencialmente:

1.  Obtenha os arquivos de compilação, incluindo o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") e possivelmente outros arquivos necessários, como unidades [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") e patches (geralmente não o código em si).
2.  Certifique-se de que o `PKGBUILD` e os arquivos que o acompanham não são maliciosos ou duvidosos.
3.  Execute `makepkg -si` no diretório onde os arquivos foram salvos. Isso vai baixar o código, resolver as dependências com o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"), compilá-lo, empacotá-lo e instalar o pacote.

**Nota:** Não há suporte aos pacotes do AUR, então qualquer pacote que você instalar é *sua responsabilidade* atualizar, e não do pacman. Se o pacote nos repositórios oficiais são atualizados, você precisa recompilar quaisquer pacotes do AUR que dependam daquelas bibliotecas.

### Pré-requisitos

Primeiro, certifique-se de que as ferramentas necessárias estão instaladas, [instalando](/index.php/Instale "Instale") todo o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), o qual inclui [make](https://www.archlinux.org/packages/?name=make) e outras ferramentas necessárias para a compilação do código-fonte.

**Dica:** Use a opção `--needed` ao instalar o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) para ignorar pacotes que você já tem instalados, em vez de reinstalá-los.

**Nota:** Os pacotes do AUR presumem que o grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) está instalado, isto é, eles não listarão explicitamente os membros deste grupo como dependências

Em seguida, escolha o diretório de compilação adequado. Um diretório de compilação é apenas um diretório no qual o pacote será feito ou "compilado" e pode ser em qualquer diretório. Os exemplos nas seguintes seções usarão `~/builds` como o diretório de compilação.

### Obtendo arquivos de compilação

Localize o pacote no AUR. Isso pode ser feito usando o campo de pesquisa no topo da [página inicial do AUR](https://aur.archlinux.org/). Ao clicar no nome do aplicativo na lista de resultados de pesquisa, será mostrada uma página de informações sobre o pacote. Leia atentamente a descrição para confirmar que esse é o pacote desejado, veja quando o pacote foi atualizado pela última vez e leia quaisquer comentários.

Há vários métodos para adquirir os arquivos de compilação:

*   Clonar o repositório [git](/index.php/Git "Git") que está rotulado como o "Git Clone URL" em "Detalhes do pacote". Esse é o método preferível.

```
$ git clone https://aur.archlinux.org/*nome_pacote*.git

```

	Uma vantagem deste método é que você pode facilmente obter atualizações para o pacote vi `git pull`.

*   Baixar os arquivos de compilação com seu navegadores web clicando no link "Baixar snapshot" sob "Ações do Pacote", no canto direito da tela. Isso vai baixar um arquivo compactado, que deve ser extraído (preferivelmente em um diretório definido a parte para compilações do AUR)

```
$ tar -xvf *nome_pacote*.tar.gz

```

*   Similarmente, você pode baixar um tarball do terminal (e extraí-lo):

```
$ curl -L -O https://aur.archlinux.org/cgit/aur.git/snapshot/*nome_pacote*.tar.gz

```

### Compilando e instalando o pacote

Mude diretórios para o diretório contendo o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") do pacote.

```
$ cd *nome_pacote*

```

**Atenção:** Verifique cuidadosamente o `PKGBUILD`, qualquer arquivo *.install* e quaisquer outros arquivos no repositório git do pacote para comandos maliciosos ou perigosos. Em caso de dúvida, não crie o pacote e nem [peça conselho](/index.php/General_troubleshooting#Additional_support "General troubleshooting") no fórum ou na lista de discussão. Código malicioso foi encontrado em pacotes antes. [[1]](https://lists.archlinux.org/pipermail/aur-general/2018-July/034151.html)

Veja o conteúdo de todos os arquivos fornecidos. Por exemplo, para usar o paginador *less* para ver `PKGBUILD`:

```
$ less PKGBUILD

```

**Dica:** Se você está atualizando um pacote, você pode querer olhar as mudanças desde o último commit.

*   Para ver as mudanças desde o último commit, você pode usar `git show`.
*   Para ver mudanças desde o último commit usando *vimdiff*, execute `git difftool @~..@ vimdiff`. A vantagem do *vimdiff* é que você vê todo o conteúdo de cada arquivo junto com os indicadores do que foi alterado.

Crie o pacote. Depois de confirmar, manualmente, o conteúdo dos arquivos, execute [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") como usuário normal no diretório de compilação.

```
$ makepkg -si

```

*   `-s`/`--syncdeps` resolve automaticamente e instala quaisquer dependências com o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") antes de compilar. Se o pacote depende de outros pacotes do AUR, você precisará instalá-los manualmente primeiro.
*   `-i`/`--install` instala o pacote se ele foi compilado com sucesso. Alternativamente, o pacote compilado pode ser instalado com `pacman -U *nome_pacote*.pkg.tar.xz`.

Outras flags úteis são

*   `-r`/`--rmdeps` remove dependências de tempo de compilação após a compilação, já que elas não mais são necessárias. Porém, essas dependências pode precisar serem reinstaladas da próxima vez que o pacote for atualizado.
*   `-c`/`--clean` limpa os arquivos temporários de compilação após a compilação, já que eles não mais são necessários. Esses arquivos geralmente são necessários apenas ao depurar o processo de compilação.

**Nota:** O exemplo acima é apenas um resumo breve do processo de compilação. É **altamente** recomendado ler os artigos [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") e [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)") para mais detalhes.

## Feedback

A [Interface Web do AUR](https://aur.archlinux.org) possui um recurso de comentários que permite aos usuários fornecer sugestões e feedback sobre melhorias para o colaborador [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"). Evite colar patches ou `PKGBUILD` na seção de comentários: eles rapidamente se tornam obsoletos e acabam desnecessariamente ocupando muito espaço. Em vez disso, envie esses arquivos por e-mail para o mantenedor, ou até mesmo use um [pastebin](/index.php/Pastebin "Pastebin").

Uma das atividades mais fáceis para **todos** os usuários do Arch é navegar no AUR e **votar** nos seus pacotes favoritos usando a interface online. Todos os pacotes são elegíveis para adoção por uma TU para inclusão no [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community"), e a contagem de votos é uma das considerações nesse processo; é do interesse de todos votar!

## Enviando pacotes

Os usuários podem compartilhar [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") usando o Arch User Repository. Ele não contém nenhum pacote binário, mas permite que os usuários carreguem `PKGBUILD` s que podem ser baixados por outras pessoas. Estes `PKGBUILD` s são completamente não oficiais e não foram cuidadosamente verificados, por isso devem ser usados por sua conta e risco. Veja [Diretrizes de envio ao AUR](/index.php/Diretrizes_de_envio_ao_AUR "Diretrizes de envio ao AUR") para mais detalhes.

## Tradução da interface web

Veja [i18n.txt](https://projects.archlinux.org/aurweb.git/tree/doc/i18n.txt) na área de fontes do AUR para informações sobre criação e manutenção da [Interface Web do AUR](https://aur.archlinux.org).

## Sintaxe de comentário

Há suporte à sintaxe do [Python-Markdown](https://python-markdown.github.io/) nos comentários. Ela fornece a sintaxe básica [Markdown](https://en.wikipedia.org/wiki/pt:Markdown são convertidos em links automaticamente. Comentários longos são recolhidos e podem ser expandidos sob demanda.

## FAQ

### O que é o AUR?

O AUR (Arch User Repository) é um lugar para onde a comunidade do Arch Linux pode enviar [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") de aplicativos, bibliotecas, etc., e compartilhá-los com toda a comunidade. Outros usuários poderão então votar pelos seus favoritos para que sejam transferidos para o [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community") de forma a serem compartilhados com os usuários do Arch Linux em forma de binário.

### Que tipo de pacote é permitido no AUR?

Os pacotes no AUR são apenas "scripts de compilação", ou seja, receitas para construir binários para [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"). Na maioria dos casos, tudo é permitido, sujeito a [utilidade e diretrizes de escopo](/index.php/Diretrizes_de_envio_ao_AUR#Regras_de_envio "Diretrizes de envio ao AUR"), desde que você esteja em conformidade com os termos de licenciamento do conteúdo. Para outros casos, onde é mencionado que "você não pode vincular" a downloads, ou seja, conteúdos que não são redistribuíveis, você pode usar apenas o nome do arquivo como fonte. Isso significa e exige que os usuários já tenham a fonte restrita no diretório de compilação antes de criar o pacote. Em caso de dúvida, pergunte.

### Como posso votar em pacotes no AUR?

Inscreva-se no [site do AUR](https://aur.archlinux.org/) para obter uma opção "Votar neste pacote" enquanto navega nos pacotes. Depois de se inscrever, também é possível votar na linha de comando com [aurvote](https://aur.archlinux.org/packages/aurvote/), [aurvote-git](https://aur.archlinux.org/packages/aurvote-git/) ou [aur-auto-vote-git](https://aur.archlinux.org/packages/aur-auto-vote-git/).

Como alternativa, se você tiver configurado as [autenticação via ssh](/index.php/Diretrizes_de_envio_ao_AUR#Autenticação "Diretrizes de envio ao AUR"), poderá votar diretamente na linha de comando usando a chave ssh. Isso significa que você não precisará salvar ou digitar sua senha do AUR.

```
$ ssh aur@aur.archlinux.org vote *nome_do_pacote*

```

### O que é um Trusted User / TU?

Um [(Trusted User)](/index.php/AUR_Trusted_User_Guidelines_(Portugu%C3%AAs) "AUR Trusted User Guidelines (Português)"), abreviado como TU, é uma pessoa que é escolhida para supervisionar o AUR e o [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community"). Eles são os que mantêm [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") populares no *community* e de forma geral mantêm o AUR funcionando.

### Qual é a diferença entre o Arch User Repository e repositório [community]?

O Arch User Repository é onde todos os [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") enviados pelos usuários são armazenados e devem ser criados manualmente com [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"). Quando `PKGBUILD`s recebem bastante interesse da comunidade e o suporte de uma TU, eles são movidos para o [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community") (mantido pelos TUs), onde os pacotes binários podem ser instalados com [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)").

### Foo no AUR está desatualizado; o que devo fazer?

Primeiro, você deve sinalizar o pacote como *desatualizado* indicando detalhes sobre o motivo pelo qual o pacote está desatualizado, de preferência incluindo links para o anúncio de lançamento ou a nova versão [tarball](/index.php/Arquivamento_e_compress%C3%A3o#Arquivamento_apenas "Arquivamento e compressão"). Você também deve tentar entrar em contato com o mantenedor diretamente por e-mail. Se não houver resposta do mantenedor após *duas semanas*, você pode preencher uma requisição para *tornar órfão*. Isso significa que você pede a um [Trusted User](/index.php/Trusted_User_(Portugu%C3%AAs) "Trusted User (Português)") para retirar o mantenedor daquele pacote base. Isso deve ser feito apenas se o pacote exigir ação do mantenedor, se ele não estiver respondendo e se você já tentou contatá-lo anteriormente.

Neste meio tempo, você pode tentar atualizar o pacote você mesmo editando o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") localmente. Ás vezes, atualizações não exigem qualquer alteração para o processo de compilação ou empacotamento, caso em que apenas atualizar o vetor `pkgver` ou `source` é suficiente.

**Nota:** [Pacotes VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") não são considerados desatualizados quando o pkgver muda, então não sinalize-os, pois o mantenedor vai simplesmente desmarcar sinalização e ignorar você. Mantenedores do AUR não deve fazer commit para meras atualizações de pkgver.

### Foo no AUR não compila quando eu executo makepkg; o que devo fazer?

Provavelmente está deixando escapar alguma coisa trivial.

1.  [Atualize o sistema](/index.php/Pacman_(Portugu%C3%AAs)#Atualizando_pacotes "Pacman (Português)") antes de compilar qualquer coisa com [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"), pois o problema pode ser que seu sistema não esteja atualizado.
2.  Certifique-se de ter ambos os grupos [base](https://www.archlinux.org/groups/x86_64/base/) e [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) instalados.
3.  Tente usar a opção `-s` com `makepkg` para verificar e instalar todas as dependências necessárias antes de iniciar o processo de compilação.

Certifique-se de ler primeiro o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") e os comentários na página AUR do pacote em questão. A razão pode não ser trivial afinal. `CFLAGS`, `LDFLAGS` e `MAKEFLAGS` personalizados podem causar falhas. Também é possível que o `PKGBUILD` esteja quebrado para todos. Se você não conseguir descobrir sozinho, basta relatá-lo ao responsável, por exemplo, publicando os erros que você está recebendo nos comentários na página do AUR.

Para verificar se o `PKGBUILD` está quebrado, ou seu sistema está desconfigurado, considere compilar em um chroot limpo. Ele compilará seu pacote em um ambiente limpo do Arch Linux, com apenas dependências (de compilação) instaladas e sem personalização do usuário. Para fazer isso [instale](/index.php/Instale "Instale") o [devtools](https://www.archlinux.org/packages/?name=devtools) e execute *extra-x86_64-build* ao invés de *makepkg*. Para pacotes [multilib](/index.php/Multilib_(Portugu%C3%AAs) "Multilib (Português)"), execute *multilib-build* Veja [DeveloperWiki:Building in a clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot") para mais informações. Se o processo de compilação ainda falhar em um chroot limpo, o problema provavelmente está no `PKGBUILD`.

### ERRO: Uma ou mais assinaturas PGP não puderam ser verificadas!; o que eu devo fazer?

É muito provável que você não tenha as chaves públicas necessárias no seu chaveiro pessoal para verificar os arquivos baixados. Veja [Makepkg (Português)#Verificação de assinatura](/index.php/Makepkg_(Portugu%C3%AAs)#Verificação_de_assinatura "Makepkg (Português)") para detalhes.

### Como eu crio um PKGBUILD?

O melhor recurso é a página wiki [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes"). Lembre-se de procurar no AUR antes de criar o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") para não duplicar esforços.

### Eu tenho um PKGBUILD que queria enviar; alguém pode verificá-lo para ver se ele tem algum erro?

Se você gostaria de ter seu [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") revisado, poste-o na [lista de discussão aur-general](https://mailman.archlinux.org/mailman/listinfo/aur-general) para obter feedback dos TUs e colegas membros do AUR. Você também pode obter ajuda no [canal IRC](/index.php/Canal_IRC "Canal IRC"), #archlinux-aur no irc.freenode.net. Você também pode usar [namcap](/index.php/Namcap_(Portugu%C3%AAs) "Namcap (Português)") para verificar seu `PKGBUILD` e o pacote resultante por erros.

### Como que faz para um PKGBUILD ir para o repositório *community*?

Normalmente, pelo menos 10 votos são necessários para que algo se mova para [community](/index.php/Reposit%C3%B3rio_community "Repositório community"). No entanto, se um [TU](/index.php/TU_(Portugu%C3%AAs) "TU (Português)") quiser dar suporte a um pacote, ele geralmente será encontrado no repositório.

Alcançar o mínimo exigido de votos não é o único requisito, tem que haver um TU disposto a manter o pacote. Os TUs não são obrigados a mover um pacote para o repositório *community*, mesmo que ele tenha milhares de votos.

Normalmente, quando um pacote muito popular fica no AUR, é porque:

*   Arch Linux já tem outra versão de um pacote nos repositórios
*   Sua licença proíbe redistribuição
*   Isso ajuda a obter [PKGBUILDs](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") fornecidos por usuário. [Auxiliares do AUR](/index.php/Auxiliares_do_AUR "Auxiliares do AUR"), por definição, [não possuem suporte](https://bbs.archlinux.org/viewtopic.php?pid=828310#p828310).

Veja também [[Diretrizes de Trusted User do AUR#Regras para a Entrada de Pacotes no Repositório [community]|Regras para a Entrada de Pacotes no Repositório community]].

### Como o posso agilizar processo de repetidas compilações?

Veja [Makepkg (Português)#Melhorando os tempos de compilação](/index.php/Makepkg_(Portugu%C3%AAs)#Melhorando_os_tempos_de_compilação "Makepkg (Português)").

### Qual é a diferença entre pacotes foo e foo-git

Muitos pacotes AUR são apresentados em versões comuns ("estáveis") e de desenvolvimento ("instáveis"). Um pacote de desenvolvimento geralmente têm um sufixo como `-cvs`, `-svn`, `-git`, `-hg`, `-bzr` ou `-darcs`. Enquanto pacotes de desenvolvimento não se destinam ao uso comum, eles podem oferecer novos recursos ou correções de erros. Como esses pacotes fazem o download da última fonte disponível quando você executa o [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)"), um versão do pacote para rastrear possíveis atualizações não está diretamente disponível para eles. Da mesma forma, esses pacotes não podem realizar uma soma de verificação de autenticidade, em vez disso dependendo do mantenedor do repositório [Git](/index.php/Git "Git").

Veja também [Manutenção do sistema#Use pacotes de software aprovados](/index.php/Manuten%C3%A7%C3%A3o_do_sistema#Use_pacotes_de_software_aprovados "Manutenção do sistema").

### Por que foo desapareceu do AUR?

É possível que o pacote tenha sido adotado por um [TU](/index.php/TU_(Portugu%C3%AAs) "TU (Português)") e agora esteja no [repositório community](/index.php/Reposit%C3%B3rio_community "Repositório community").

Pacotes podem ter sido excluídos, se eles não preencherem as [regras de envio](/index.php/Diretrizes_de_envio_ao_AUR#Regras_de_envio "Diretrizes de envio ao AUR"). Veja os [histórico do aur-requests](https://lists.archlinux.org/pipermail/aur-requests/) pelo motivo da exclusão.

Se o pacote costumava existir no AUR3, ele pode não ter sido [migrado para o AUR4](https://lists.archlinux.org/pipermail/aur-general/2015-August/031322.html). Veja os [#Repositórios Git para pacotes AUR3](#Repositórios_Git_para_pacotes_AUR3) nos quais eles foram preservados.

### Como eu descubro se algum dos meus pacotes instalados desapareceu do AUR?

A forma mais simples é verificar o status HTTP da página AUR do pacote:

```
$ comm -23 <(pacman -Qqm | sort) <(curl [https://aur.archlinux.org/packages.gz](https://aur.archlinux.org/packages.gz) | gzip -cd | sort)

```

### Como eu posso obter uma lista de todos os pacotes do AUR?

*   [https://aur.archlinux.org/packages.gz](https://aur.archlinux.org/packages.gz)
*   Use `aurpkglist` do [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## Veja também

*   [Interface Web do AUR](https://aur.archlinux.org)
*   [Lista de Discussão do AUR](https://lists.archlinux.org/listinfo/aur-general)
*   [DeveloperWiki:AUR Cleanup Day](/index.php/DeveloperWiki:AUR_Cleanup_Day "DeveloperWiki:AUR Cleanup Day")