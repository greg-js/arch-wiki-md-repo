O **Trusted User (TU)** ("Usuário confiável") é um membro da comunidade encarregado de manter o AUR funcionando. Ele/Ela mantém pacotes populares ([comunicando com o upstream e enviando-o patches quando necessário](https://mailman.archlinux.org/pipermail/aur-general/2010-September/010649.html)) e vota em assuntos administrativos. Um TU é eleito de membros ativos da comunidade pelos atuais TUs em um processo democrático. TUs são os únicos membros que têm a última palavra na direção do AUR.

Os TUs são governados usando as [TU bylaws](https://aur.archlinux.org/trusted-user/TUbylaws.html) ("Estatuto dos TUs")

## Contents

*   [1 Lista de tarefas para novos Trusted Users](#Lista_de_tarefas_para_novos_Trusted_Users)
*   [2 O TU e o [unsupported]](#O_TU_e_o_.5Bunsupported.5D)
*   [3 O TU e [community], Diretrizes para Manutenção de Pacotes](#O_TU_e_.5Bcommunity.5D.2C_Diretrizes_para_Manuten.C3.A7.C3.A3o_de_Pacotes)
    *   [3.1 Regras para a Entrada de Pacotes no Repositório [community]](#Regras_para_a_Entrada_de_Pacotes_no_Reposit.C3.B3rio_.5Bcommunity.5D)
    *   [3.2 Acessando e Atualizando o Repositório](#Acessando_e_Atualizando_o_Reposit.C3.B3rio)
    *   [3.3 Abandonando pacotes](#Abandonando_pacotes)
    *   [3.4 Movendo pacotes do unsupported para [community]](#Movendo_pacotes_do_unsupported_para_.5Bcommunity.5D)
    *   [3.5 Movendo pacotes do [community] para unsupported](#Movendo_pacotes_do_.5Bcommunity.5D_para_unsupported)
    *   [3.6 Movendo pacotes do [community-testing] para [community]](#Movendo_pacotes_do_.5Bcommunity-testing.5D_para_.5Bcommunity.5D)
    *   [3.7 Excluindo pacotes do unsupported](#Excluindo_pacotes_do_unsupported)
    *   [3.8 Veja também](#Veja_tamb.C3.A9m)

## Lista de tarefas para novos Trusted Users

1.  Ler este artigo de wiki por completo.
2.  Ler as [TU Bylaws](https://aur.archlinux.org/trusted-user/TUbylaws.html).
3.  Certificar-se de que os detalhes da sua conta no [AUR](/index.php/AUR "AUR") estão atualizados e que seu patrocinador tenha lhe concedido o status de TU.
4.  Adicionar a si próprio à página de [Trusted Users](/index.php/Trusted_Users "Trusted Users").
5.  Relembrar Allan/Andrea de alterar sua conta nos fóruns.
6.  Perguntar a algum TU pela chave do #archlinux-tu@freenode e aparecer no canal. Você não tem que fazer isso, mas seria interessante já que é lá que a maioria dos segredos ocultos são apresentados e onde muitas novas ideias são concebidas.
7.  Se você ainda não fizer parte do grupo de Trusted User no bug tracker em dois dias, relate isso como um bug para Andrea Scarpino (andrea@archlinux.org).
8.  Envie ao Ionuț Bîru (ibiru@archlinux.org) todas as informações baseadas neste [modelo](https://www.archlinux.org/trustedusers/) para ter acesso à interface de desenvolvimento.
9.  Instalar o pacote [devtools](https://www.archlinux.org/packages/?name=devtools).
10.  Enviar um e-mail para o Lukas Fleischer contendo uma chave pública de SSH em anexo. Se você não tiver uma, use `ssh-keygen` para criar uma. Verifique na página wiki [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys") para mais informações sobre chaves SSH.
11.  Criar uma chave PGP para [assinatura de pacotes](/index.php/Package_signing "Package signing").
12.  Enviar um e-mail assinado digitalmente para todos os [donos de Chaves Mestras](https://www.archlinux.org/master-keys/) incluindo sua chave PGP e a impressão digital da chave completa relacionada. Sua chave precisa estar assinada por pelo menos três dos cinco titulares de chaves mestras.
13.  Criar os diretórios `~/staging/community` e `~/staging/community-testing` (e `~/staging/multilib`, se você está interessado em manter pacotes multilib) no sigurd.archlinux.org. Essa etapa é **importante**, pois os scripts do devtools usam este diretório para processar a chegada de pacotes.
14.  Começar a contribuir!

## O TU e o [unsupported]

Os TUs deveriam também fazer um esforço para verificar o envio de pacotes no UNSUPPORTED por códigos maliciosos e o correto seguimento dos padrões dos PKGBUILD. Em cerca de 80% dos casos, os PKGBUILDs no UNSUPPORTED são muito simples e podem ter rapidamente verificadas a sanidade e os códigos maliciosos pela equipe de TUs.

Os TUs devem também verificar os PKGBUILDs por pequenos erros, sugerir correções e melhoras. O TU deve se tentar certificar-se de que todos os pacotes sigam Arch Packaging Guidelines/Standards (Diretrizes/Padrões de Empacotamento do Arch) e ao fazer isso, compartilhar suas habilidades com outros criadores de pacotes em um esforço em criar um padrão de criação de pacotes por toda a distribuição.

Os TUs também estão em uma posição de documentar práticas recomendadas.

## O TU e [community], Diretrizes para Manutenção de Pacotes

### Regras para a Entrada de Pacotes no Repositório [community]

*   Somente pacotes "populares" podem entrar no repositório, sendo definido pelo 1% de uso no [pkgstats](https://www.archlinux.de/?page=PackageStatistics) ou 10 votos no AUR.

*   Exceções automáticas a esta regra são:
    *   pacotes i18n
    *   pacotes de acessibilidade
    *   drivers
    *   dependências de pacotes que satisfazem a definição de populares, incluindo makedeps e optdeps
    *   pacotes que são parte de uma coleção e têm a intenção de ser distribuidos juintos, fornecendo uma parte da coleção satisfaz a definição de popular

*   Quaisquer adições não cobertas por nenhum dos critérios acima devem ser propostas na lista de discussão aur-general, explicando o motivo para a dispensa (ex.: pacote renomeado, novo pacote). O acordo de três outros TUs é necessário para que o pacote seja aceito na [community]. Adições propostas por TUs com grande número de pacotes "não-populares" provavelmente serão rejeitadas.

*   Os TUs são fortemente encorajados a mover os pacotes mantidos do [community], se eles tem baixo uso. Nenhuma aplicação será necessária, apesar de que a renúncia de pacotes de TUs podem ser filtrados antes que ocorra adoção.

### Acessando e Atualizando o Repositório

O repositório [community] agora usa **devtools**, que é o mesmo sistema usado para enviar pacotes para o [core] e [extra], apesar de usar outro servidor `nymeria.archlinux.org` ao invés de `gerolde.archlinux.org`. Por isso, a maioria das instruções no [Guia do Empacotador](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager") funciona sem qualquer outro comentário. Informações que são específicas para o repositório [community] (como URLs alteradas) foram inseridas aqui. O devtools exige dos empacotadores a [definição da variável PACKAGER](/index.php/Arch_Build_System#Set_the_PACKAGER_variable_in_.2Fetc.2Fmakepkg.conf "Arch Build System"). Isso é feito no `/usr/share/devtools/makepkg-{i686,x86_64}.conf` já que o arquivo de configuração padrão não é colocado em um chroot do zero.

Inicialmente, você deveria fazer um **checkout não-recursivo** do repositório [community]:

```
svn checkout -N svn+[ssh://svn-community@nymeria.archlinux.org/srv/repos/svn-community/svn](ssh://svn-community@nymeria.archlinux.org/srv/repos/svn-community/svn)

```

Isso cria um diretório chamado "svn-packages", o qual contém nada. Ele, na verdade, sabe que é um checkout de svn.

Para realizar **checkout**, **update** em todos pacotes ou **add** de um pacote, veja o [Guia do empacotador](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager").

Para realizar **remove** de um pacote:

```
ssh nymeria.archlinux.org /community/db-remove community arch pkgname

```

Aqui e no texto seguinte, a arquitetura pode ser i686 ou x86_64, as quais são as duas arquiteturas suportadas pelo Arch Linux. (E sobre "any"?)

Quando você tiver finalizado a edição do PKGBUILD, etc, você deveria fazer um **commit** das alterações (`svn commit`).

Quando você quiser enviar (**release**) um pacote, primeiro copie o pacote para o diretório _staging/community_ no nymeria.archlinux.org usando scp e, então, marque (**tag**) o pacote no diretório _pkgname/trunk_ e informando a `archrelease community-arch`. Isso faz uma cópia svn das entradas do trunk em um diretório chamado _community-i686_ ou _community-x86_64_. indicando que este pacote está no repositório [community] para aquela arquitetura.

_**Nota:** Em alguns casos, especialmente para pacotes do [community], um TU de x86_64 podem subir o pkgrel por .1 (e não por +1). Isso indica que a alteração do PKGBUILD é especificamente de x86_64 e mantenedores de i686 **não deveriam** recompilar o pacote para i686\. Quando o TU decide subir o pkgrel, isso deveria ser feito com o acréscimo normal de +1\. Porém, um pkgrel=2.1 anterior não deve se tornar pkgrel=3.1 quando o TU subir o pkgrel, ao invés disso deve ser pkgrel=3\. Em resumo, mantenha os lançamentos com ponto (.) exclusivamente para TUs de x86_64 para evitar confusão._

Deste modo, o **processo** de atualização de pacotes pode ser resumida em:

*   **Atualizar** o diretório de pacote (`svn update algum-pacote`)
*   **Mudar** para o diretório trunk do pacote (`cd algum-pacote/trunk`)
*   **Editar** o PKGBUILD, fazer alterações necessárias e `makepkg`. Isso é recomendado para compilar em um [chroot limpo](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot").
*   **[Namcap](/index.php/Namcap "Namcap")** no PKGBUILD e no binário pkg.tar.gz.
*   **Commit**, **Copiar** e **Tag** o pacote usando `communitypkg "mensagem de commit"`. Isso automatiza o seguinte:
    *   **Commit** das alterações no trunk (`svn commit`)
    *   **Copiar** o pacote para o nymeria.archlinux.org (`scp pkgname-ver-rel-arch.pkg.tar.xz* nymeria.archlinux.org:staging/community/`)
    *   **Tag** do pacote (`archrelease community-{i686,x86_64`})
*   **Atualizar** o repositório (`ssh nymeria.archlinux.org /community/db-update`)

Veja também a seção de _Miscelânia_ no [Guia do Empacotador](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager"). Para a seção _Avoid having to enter your password all the time_ ("evite de precisar digitar sua senha toda vez") uso nymeria.archlinux.org ao invés do gerolde.archlinux.org.

### Abandonando pacotes

Se um TU não pode ou não quer mais manter um pacote, um aviso deve ser postado na Lista de Discussão do AUR, para que outro TU possa mantê-lo. Um pacote pode ainda ser abandonado mesmo se nenhum outro TU quiser mantê-lo, mas os TUs devem evitar de deixar muitos pacotes soltos (eles não deveriam manter mais do que possam dar conta). Se um pacote se tornou obsoleto ou não é mais usado, ele também pode ser completamente removido.

Se um pacote foi removido completamente, o mesmo pode ser enviado novamente (do zero) para o UNSUPPORTED, onde um usuário normal pode manter o pacote ao invés de um TU.

### Movendo pacotes do unsupported para [community]

Siga os procedimentos normais para adição de um pacote ao [community], mas lembre-se de remover o pacote correspondente do unsupported!

### Movendo pacotes do [community] para unsupported

Remova o pacote usando as instruções acima e envie o seu tarball fonte para o AUR.

### Movendo pacotes do [community-testing] para [community]

```
ssh nymeria.archlinux.org /arch/db-move community-testing community package

```

### Excluindo pacotes do unsupported

Não há sentido em remover pacotes-modelos porque eles serão recriados na tentativa de atender dependências. Se alguém enviar um pacote real, então todos os dependentes irão apontar para o local correto.

### Veja também

*   [Diretrizes de Empacotamento](/index.php/DeveloperWiki#Packaging_Guidelines "DeveloperWiki")