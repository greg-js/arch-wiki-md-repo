O **Trusted User (TU)** ("Usuário confiável") é um membro da comunidade encarregado de manter o AUR funcionando. Ele/Ela mantém pacotes populares ([comunicando com o *upstream* e enviando-o patches quando necessário](https://mailman.archlinux.org/pipermail/aur-general/2010-September/010649.html)) e vota em assuntos administrativos. Um TU é eleito de membros ativos da comunidade pelos atuais TUs em um processo democrático. TUs são os únicos membros que têm a última palavra na direção do AUR.

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
3.  Certificar-se de que os detalhes da sua conta no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") estejam atualizados e que seu patrocinador tenha lhe concedido o status de TU.
4.  Adicionar a si próprio à página de [Trusted Users](/index.php/Trusted_Users "Trusted Users").
5.  Se inscrever na lista de discussão pública de desenvolvimento do Arch Linux, [arch-dev-public](https://lists.archlinux.org/listinfo/arch-dev-public).
6.  Lembrar um [administrador do BBS](https://bbs.archlinux.org/userlist.php?username=&show_group=1&sort_by=username&sort_dir=ASC&search=Submit) de alterar sua conta nos fóruns.
7.  Perguntar a algum TU pela chave do #archlinux-tu@freenode e aparecer no canal. Você não tem que fazer isso, mas seria interessante já que é lá que a maioria dos segredos ocultos são apresentados e onde muitas novas ideias são concebidas.
8.  Criar uma chave PGP para [assinatura de pacotes](/index.php/Package_signing "Package signing") ou use sua chave PGP existente. Certifique-se de que a chave também contém uma subchave criptográfica de forma você possa receber tokens de verificação criptografados.
9.  Enviar ao Ionuț Bîru (ibiru@archlinux.org) oru ao Florian Pritz (bluewind@xinu.at) um e-mail com todas as informações baseadas neste [modelo](https://www.archlinux.org/trustedusers/) para ter acesso à interface de desenvolvimento (archweb).
10.  Enviar um e-mail assinado para o Florian:
    *   Anexe uma chave pública SSH. Se você não possuir uma, use `ssh-keygen` para gerar uma. Verifique na página wiki [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys") para mais informações sobre chaves SSH.
    *   Solicitar que ele lhe dê permissão à arch-dev-public.
    *   Façar para ele se você deseja um e-mail @archlinux.org.
11.  Pedir a seu patrocinador (*sponsor*):
    *   para lhe conceder o status de TU no AUR.
    *   para abrir uma nova tarefa no projeto "Keyring" do rastreador de erro seguindo as sintruções [nesta mensagem](https://lists.archlinux.org/pipermail/arch-dev-public/2013-September/025456.html) na ordem de ter sua chave PGP assinado pelos três detentores de chave mestre.
12.  Instale o pacote [devtools](https://www.archlinux.org/packages/?name=devtools).
13.  [Configurar sua chave privada ssh](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#Autentica.C3.A7.C3.A3o "Arch User Repository (Português)") para os servidores `orion.archlinux.org` e `repos.archlinux.org`.
14.  Teste a conexão SSH para seunome@orion.archlinux.org (assim que você tiver permissões).
15.  Se você não for acrescentado a um grupo de Trusted User no rastreador de erro em dois dias, relate isso como um bug para arch-dev-public.
16.  Começar a contribuir!

## O TU e o [unsupported]

Os TUs deveriam também fazer um esforço para verificar o envio de pacotes no UNSUPPORTED por códigos maliciosos e o correto seguimento dos padrões dos PKGBUILD. Em cerca de 80% dos casos, os PKGBUILDs no UNSUPPORTED são muito simples e podem ter rapidamente verificadas a sanidade e os códigos maliciosos pela equipe de TUs.

Os TUs devem também verificar os PKGBUILDs por pequenos erros, sugerir correções e melhoras. O TU deve se tentar certificar-se de que todos os pacotes sigam Arch Packaging Guidelines/Standards (Diretrizes/Padrões de Empacotamento do Arch) e ao fazer isso, compartilhar suas habilidades com outros criadores de pacotes em um esforço em criar um padrão de criação de pacotes por toda a distribuição.

Os TUs também estão em uma posição de documentar práticas recomendadas.

## O TU e [community], Diretrizes para Manutenção de Pacotes

### Regras para a Entrada de Pacotes no Repositório [community]

*   Um pacote não pode já existir em qualquer um dos repositórios do Arch Linux. você deve tomar os cuidados necessários para se certificar que nenhum outro empacotador está no processo de promoção do mesmo pacote. Veja os comentários do pacote do AUR, leia os últimos títulos de assuntos no [aur-general](https://mailman.archlinux.org/mailman/listinfo/aur-general), pesquise [todos os projetos no rastreador de erro](https://bugs.archlinux.org/index.php?project=0&do=index&switch=1), use [grep](https://en.wikipedia.org/wiki/Grep "wikipedia:Grep") no [log do Subversion](http://svnbook.red-bean.com/en/1.7/svn.ref.svn.c.log.html) e envie uma mensagem rápida para o [canal IRC](/index.php/IRC_Channel "IRC Channel") privado de TUs.

*   Somente pacotes "populares" podem entrar no repositório, sendo definido pelo 1% de uso no [pkgstats](https://www.archlinux.de/?page=PackageStatistics) ou 10 votos no AUR.

*   Exceções automáticas a esta regra são:
    *   pacotes de internacionalização (i18n)
    *   pacotes de acessibilidade
    *   drivers
    *   dependências de pacotes que satisfazem a definição de populares, incluindo **makedeps** e **optdeps**
    *   pacotes que são parte de uma coleção e têm a intenção de ser distribuídos juntos, fornecendo uma parte da coleção satisfaz a definição de popular

*   Quaisquer adições não cobertas por nenhum dos critérios acima devem ser propostas na lista de discussão aur-general, explicando o motivo para a dispensa (ex.: pacote renomeado, novo pacote). O acordo de três outros TUs é necessário para que o pacote seja aceito na [community]. Adições propostas por TUs com grande número de pacotes "não-populares" provavelmente serão rejeitadas.

*   Os TUs são incentivados a mover os pacotes mantidos do [community], se eles tiverem baixo uso. Nenhuma aplicação será necessária, apesar de que a renúncia de pacotes de TUs pode ser filtrada antes que ocorra adoção.

*   É uma boa prática sempre incrementar o **pkgrel** em *1* (em outras palavras, defina o para *n + 1*) ao promover um pacote do AUR. Isso é para facilitar atualizações automáticas para aqueles que já têm o pacote instalado, de forma que eles podem continuar a receber atualizações a partir do canal oficial. Um outro efeito positivo disto é que usuários não são avisados que sua cópia local é mais nova, como é o caso se um empacotador redefinir o **pkgrel** para *1*.

### Acessando e Atualizando o Repositório

O repositório [community] agora usa **devtools**, que é o mesmo sistema usado para enviar pacotes para o [core] e [extra], apesar de usar outro servidor `nymeria.archlinux.org` ao invés de `gerolde.archlinux.org`. Por isso, a maioria das instruções no [Guia do Empacotador](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager") funciona sem qualquer outro comentário. Informações que são específicas para o repositório [community] (como URLs alteradas) foram inseridas aqui. O devtools exige que os empacotadores [definam a variável PACKAGER](/index.php/Makepkg#Packager_information "Makepkg") no `makepkg.conf`.

Inicialmente, você deve fazer um **checkout não-recursivo** do repositório [community]: svn checkout -N svn+ssh://svn-community@repos.archlinux.org/srv/repos/svn-community/svn svn-community

Isso cria um diretório chamado "svn-community" contendo nada, além de uma pasta ".svn".

Para realizar **checkout**, **atualizar** todos os pacotes ou **adicionar** um pacote, veja o [Guia do Empacotador](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager").

Para **remover** um pacote:

```
ssh orion.archlinux.org /community/db-remove community arch pkgname

```

Aqui e no texto seguinte, *arch* pode ser *i686* ou *x86_64*, que são as duas arquiteturas às quais o Arch Linux oferece suporte.

**Note:** Se você está editando pacotes da arquitetura *any*, você pode executar os scripts x64 que também vão funcionar.

Quando você tiver finalizado a edição do PKGBUILD, etc, você deve fazer um **commit** das alterações (`svn commit`).

Compile o pacote com `mkarchroot` ou os scripts auxiliares `extra-i686-build` e `extra-x86_64-build`. Se você deseja enviar para *testing*, você também precisará compilar com os scripts de teste `testing-i686-build` e `testing-x86_64-build`.

Assine o pacote com `gpg --detach-sign *.pkg.tar.xz`. Se você está usando uma chave PGP diferente para assinatura de pacote, você pode adicioná-la ao `~/.makepkg.conf` com `GPGKEY=<identifier>`.

Quando você quiser publicar (**release**) um pacote, primeiro copie o pacote junto com sua assinatura para o diretório *staging/community* no *orion.archlinux.org* usando `scp` e, então, marque (**tag**) o pacote no diretório *pkgname/trunk* e chamando `archrelease community-arch`. Isso faz uma cópia svn das entradas do trunk em um diretório chamado *community-i686* ou *community-x86_64* indicando que este pacote está no repositório *community* para aquela arquitetura. Note que o diretório *staging* é diferente do repositório *staging* e todo pacote precisa ser enviado para o diretório *staging*. Esse processo pode ser automatizado com o script `communitypkg`. Veja o resumo abaixo.

***Nota:** Em alguns casos, especialmente para pacotes do [community], um TU de x86_64 pode incrementar o pkgrel por .1 (e não por +1). Isso indica que a alteração do PKGBUILD é especificamente de x86_64 e mantenedores de i686 **não devem** recompilar o pacote para i686\. Quando o TU decide incrementar o pkgrel, isso deveria ser feito com o acréscimo normal de +1\. Porém, um pkgrel=2.1 anterior não deve se tornar pkgrel=3.1 quando incrementado pelo TU e deve ser pkgrel=3\. Em resumo, mantenha os lançamentos com ponto (.) exclusivamente para TUs de x86_64 para evitar confusão.*

'**Resumo da atualização de pacote:**

*   **Atualizar** o diretório de pacote (`svn update algum-pacote`)
*   **Mudar** para o diretório trunk do pacote (`cd algum-pacote/trunk`)
*   **Editar** o PKGBUILD, fazer alterações necessárias, atualizar o checksums com `updpkgsums`.
*   **Compilar** o pacote: com `makechrootpkg` ou `extra-i686-build` e `extra-x86_64-build`. É **obrigatório** compilar em um [*chroot* limpo](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot").
*   **[Namcap](/index.php/Namcap "Namcap")** no PKGBUILD e no binário `pkg.tar.gz`.
*   **Commit**, **Copiar** e **Tag** o pacote usando `communitypkg "mensagem de commit"`. Isso automatiza o seguinte:
    *   Fazer **commit** das alterações no trunk: `svn commit`.
    *   **Assinar** o pacote: `gpg --detach-sign *.pkg.tar.xz`.
    *   **Copiar** o pacote e sua assinatura para *orion.archlinux.org*: `scp *.pkg.tar.xz *.pkg.tar.xz.sig orion.archlinux.org:staging/community/`.
    *   Aplicar um **tag** do pacote: `archrelease community-{i686,x86_64`}.
*   **Atualizar** o repositório: `ssh orion.archlinux.org /community/db-update`.

Veja também a seção de *Miscelânia* no [Guia do Empacotador](/index.php/DeveloperWiki:HOWTO_Be_A_Packager "DeveloperWiki:HOWTO Be A Packager") and [SSH keys#ssh-agent](/index.php/SSH_keys#ssh-agent "SSH keys"). Para a seção *Avoid having to enter your password all the time* ("evite de precisar digitar sua senha toda vez"), use *orion.archlinux.org* em vez do *gerolde.archlinux.org*.

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

Não há sentido em remover pacotes-modelos, porque eles serão recriados na tentativa de atender dependências. Se alguém enviar um pacote real, então todos os dependentes irão apontar para o local correto.

### Veja também

*   [Diretrizes de Empacotamento](/index.php/DeveloperWiki#Packaging_Guidelines "DeveloperWiki")