**Status de tradução:** Esse artigo é uma tradução de [AUR submission guidelines](/index.php/AUR_submission_guidelines "AUR submission guidelines"). Data da última tradução: 2019-10-13\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=AUR_submission_guidelines&diff=0&oldid=582292) na versão em inglês.

Artigos relacionados

*   [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)")
*   [Padrões de empacotamento do Arch](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")
*   [Diretrizes de Trusted User do AUR](/index.php/Diretrizes_de_Trusted_User_do_AUR "Diretrizes de Trusted User do AUR")

Os usuários podem **compartilhar** PKGBUILDs usando o [Arch User Repository](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)"). Ele não contém nenhum pacote binário, mas permite que os usuários carreguem PKGBUILDs que podem ser baixados por outras pessoas. Estes PKGBUILDs são completamente não oficiais e não foram cuidadosamente avaliados, por isso devem ser usados por sua conta e risco.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Enviando pacotes](#Enviando_pacotes)
    *   [1.1 Regras de envio](#Regras_de_envio)
    *   [1.2 Autenticação](#Autenticação)
    *   [1.3 Criando repositórios de pacote](#Criando_repositórios_de_pacote)
    *   [1.4 Publicando novo conteúdo de pacote](#Publicando_novo_conteúdo_de_pacote)
*   [2 Mantendo pacotes](#Mantendo_pacotes)
*   [3 Requisições](#Requisições)

## Enviando pacotes

**Atenção:** Antes de tentar enviar um pacote, espera-se que você esteja familiarizado com os [Arch Packaging Standards](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch") (*padrões de empacotamento do Arch*) e todos os artigos sob "Artigos relacionados". Verifique cuidadosamente se o que você está enviando está correto. Pacotes que violam as regras podem ser excluídos sem qualquer aviso.

Se você de alguma forma esta incerto sobre um pacote ou o processo de compilação/envio mesmo após ler essa seção duas vezes, envie o PKGBUILD à [lista de discussão do AUR](https://mailman.archlinux.org/mailman/listinfo/aur-general), o [fórum do AUR](https://bbs.archlinux.org/viewforum.php?id=4) nos fóruns do Arch ou peça em nosso [canal IRC](/index.php/Canal_IRC "Canal IRC") por uma revisão pública antes de adicioná-lo ao AUR.

### Regras de envio

Ao enviar um pacote para o AUR, observe as seguintes regras:

Os PKGBUILDs enviados não devem compilar aplicativos **já presentes em qualquer um** dos **repositórios oficiais** binários sob nenhuma circunstância. Verifique a [base de dados de pacotes oficial](https://www.archlinux.org/packages/) pelo pacote. Se qualquer versão dele existir, **não** envie o pacote. Se o pacote oficial estiver desatualizado, sinalize-o como tal. Se o pacote oficial está quebrado ou faltando algum recurso, por favor, envie um [relatório de erros](https://bugs.archlinux.org/).

	**Exceção** a esta regra estrita pode ser apenas pacotes que tenham **recursos extras** habilitados e/ou **patches** em comparação com os oficiais. Nesta ocasião, o `pkgname` deve ser diferente para expressar isso. Por exemplo, um pacote para o GNU Screen contendo o patch da barra lateral poderia ser chamado de `screen-sidebar`. Além disso, o array `provides=('screen')` deve ser usado para evitar conflitos com o pacote oficial.

*   **Verifique no AUR** se o pacote **já existe**. Se ela estiver atualmente atualizada, as alterações podem ser enviadas em um comentário para a atenção do mantenedor. Se não for mantido ou o mantenedor não responder, o pacote poderá ser adotado e atualizado conforme necessário. Não crie pacotes duplicados.

*   Certifique-se de que o pacote que você deseja enviar é **útil**. Alguém mais vai querer usar este pacote? É extremamente especializado? Se mais do que algumas pessoas acham este pacote útil, é apropriado para envio.

	Os repositórios AUR e oficiais são destinados a pacotes que instalam geralmente conteúdo relacionado a software e software, incluindo um ou mais dos seguintes: executável(is); arquivo(s) de configuração; documentação online ou offline para software específico ou a distribuição do Arch Linux como um todo; mídia destinada a ser usada diretamente pelo software.

*   Não use `replaces` em um PKGBUILD no AUR a menos que o pacote seja renomeado, por exemplo, quando *Ethereal* se tornou *Wireshark*. Se o pacote for uma versão **alternativa de um pacote já existente**, use `conflicts` (e `provides` se esse pacote for requerido por outras pessoas). A principal diferença é: após a sincronização (-Sy), o pacman imediatamente deseja substituir um pacote 'ofensivo' instalado ao encontrar um pacote com o `replaces` correspondente em qualquer lugar em seus repositórios; o `conflicts`, por outro lado, só é avaliado na instalação do pacote, que geralmente é o comportamento desejado, porque é menos invasivo.

*   Pacotes que usam [deliverables](https://en.wikipedia.org/wiki/Deliverables "wikipedia:Deliverables") **pré-compilados** quando os fontes estão disponíveis, devem usar o sufixo `-bin`. Uma exceção a isso com [Java](/index.php/Diretrizes_de_pacotes_Java#Empacotamento_de_Java_no_Arch_Linux "Diretrizes de pacotes Java"). O AUR não deve conter o tarball binário criado pelo makepkg, nem deve conter a lista de arquivos.

*   Por favor, adicione uma **linha de comentário** no topo do arquivo `PKGBUILD` contendo informações sobre os atuais **mantenedores** e **contribuidores** anteriores, respeitando o seguinte formato. Lembre-se de disfarçar o seu e-mail para proteger contra spam. Linhas adicionais ou desnecessárias são facultativas.

	Se você está assumindo o papel de mantenedor para um PKGBUILD existente, adicione seu nome ao topo desta forma

```
# Maintainer: Seu Nome <endereço at domínio dot tld>

```

	Se houver mantenedores antigos, liste-os como contribuidores. O mesmo se aplica para quem enviou o pacote, se não foi você. Se você é um comantenedor, adicione os nome de outros mantenedores atuais também.

```
# Maintainer: Seu Nome <endereço at domínio dot tld>
# Maintainer: Nome do Outro Mantenedor <endereço at domínio dot tld>
# Contributor: Nome do Mantenedor Anterior <endereço at domínio dot tld>
# Contributor: Nome do Criador do Pacote <endereço at domínio dot tld>

```

### Autenticação

Para acesso de escrita para o AUR, você precisar ter um [par de chaves SSH](/index.php/SSH_keys "SSH keys"). O conteúdo da chave pública precisa ser copiada para seu perfil em *Minha conta* e a chave privada correspondente configurada para o endereço `aur.archlinux.org`. Por exemplo:

 `~/.ssh/config` 
```
Host aur.archlinux.org
  IdentityFile ~/.ssh/aur
  User aur
```

Você deve [criar um novo par de chaves](/index.php/SSH_keys#Generating_an_SSH_key_pair "SSH keys") em vez de usar um existente, de forma que você possa seletivamente revogar as chaves caso algo aconteça:

```
$ ssh-keygen -f ~/.ssh/aur

```

**Dica:** Você pode adicionar múltiplas chaves públicas ao seu perfil separando-as com uma nova linha no campo de entrada.

### Criando repositórios de pacote

Se você está [criando um novo pacote](/index.php/Criando_pacotes "Criando pacotes") do zero, estabeleça um repositório Git local e um remoto no AUR [clonando](/index.php/Git#Getting_a_Git_repository "Git") o [pkgbase](/index.php/PKGBUILD_(Portugu%C3%AAs)#pkgbase "PKGBUILD (Português)") desejado. Se o pacote ainda não existir, o seguinte aviso é esperado:

 `$ git clone ssh://aur@aur.archlinux.org/*pkgbase*.git` 
```
Cloning into '*pkgbase*'...
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
```

**Nota:** O repositório não estará vazio, se `*pkgbase*` corresponde a um pacote [excluído](#Requisições).

Se você já tem um pacote, [inicialize-o](/index.php/Git#Getting_a_Git_repository "Git") como um repositório Git, se ainda não for um, e adicione um remoto do AUR:

```
$ git remote add *rótulo* ssh://aur@aur.archlinux.org/*pkgbase*.git

```

Então, faça um [fetch](/index.php/Git#Using_remotes "Git") deste remoto para inicializá-lo no AUR.

**Nota:** Use [pull e rebase](https://git-scm.com/docs/git-pull#git-pull---rebasefalsetruemergespreserveinteractive) para resolver conflitos se o `*pkgbase*` corresponder a um pacote excluído.

### Publicando novo conteúdo de pacote

**Atenção:** Seus commits terão como autor seu [nome e endereço de e-mail Git globais](/index.php/Git#Configuration "Git"). É muito difícil de alterar commits após você realizar o *push* ([FS#45425](https://bugs.archlinux.org/task/45425)). Se você deseja fazer o push para o AUR sob credenciais diferentes, você pode alterá-los por pacote com `git config user.name "..."` e `git config user.email "..."`.

Ao lançar uma nova versão do software empacotado, atualize as variáveis [pkgver](/index.php/PKGBUILD_(Portugu%C3%AAs)#pkgver "PKGBUILD (Português)") ou [pkgrel](/index.php/PKGBUILD_(Portugu%C3%AAs)#pkgrel "PKGBUILD (Português)") para notificar todos os usuários que uma atualização é necessária. Não atualize esses valores se apenas pequenas alterações no [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)"), como a correção de um erro de digitação, estiverem sendo publicadas.

Lembre-se de gerar [.SRCINFO](/index.php/.SRCINFO_(Portugu%C3%AAs) ".SRCINFO (Português)") sempre que os metadados do `PKGBUILD` forem alterados, como as atualizações do `pkgver()`; caso contrário, o AUR não mostrará números de versão atualizados.

Para enviar ou atualizar um pacote, [adicione](/index.php/Git#Staging_changes "Git") *pelo menos* o `PKGBUILD` e `.SRCINFO`, e quaisquer arquivos auxiliares novos ou modificados (tal como arquivos [.install](/index.php/PKGBUILD_(Portugu%C3%AAs)#install "PKGBUILD (Português)") ou [arquivos fontes locais](/index.php/PKGBUILD_(Portugu%C3%AAs)#source "PKGBUILD (Português)"), como [patches](/index.php/Aplica%C3%A7%C3%A3o_de_patch_em_pacotes "Aplicação de patch em pacotes"); [Faça commit](/index.php/Git#Committing_changes "Git") deles com uma mensagem de commit significativa e, finalmente, faça um [push](/index.php/Git#Push_to_a_repository "Git") das alterações para o AUR.

Por exemplo:

```
$ makepkg --printsrcinfo > .SRCINFO
$ git add PKGBUILD .SRCINFO
$ git commit -m "*mensagem útil de commit*"
$ git push

```

**Nota:** Se o `.SRCINFO` não foi adicionado antes do seu primeiro commit, adicione-o realizando o [rebase com --root](https://git-scm.com/docs/git-rebase#git-rebase---root) ou [filtrando a árvore](https://git-scm.com/docs/git-filter-branch#git-filter-branch---tree-filterltcommandgt), de forma que o AUR permita seu push inicial.

**Dica:** Para manter o diretório de trabalho e os commits o mais limpo possível, crie um [gitignore(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gitignore.5) que exclua todos os arquivos e adicione forçadamente os arquivos conforme necessário.

## Mantendo pacotes

*   Verifique os feedback e comentários de outros usuários e tente incorporar quaisquer melhorias que eles sugerirem; considere isso um processo de aprendizado!
*   Por favor, não envie um comentário contendo a versão toda vez que você atualizar o pacote. Isso deixa a seção de comentário usável para o conteúdo valioso mencionado acima.
*   Por favor, não apenas envie e depois esqueça dos pacotes! É trabalho do mantenedor manter o pacote, verificando atualizações e melhorando o PKGBUILD.
*   Se você não deseja continuar mantendo o pacote por algum motivo, basta `tornar órfão` o pacote usando a interface web AUR e/ou publique uma mensagem na Lista de Discussão do AUR. Se todos os mantenedores de um pacote AUR o abandonarem, ele se tornará um pacote ["órfão"](https://aur.archlinux.org/packages/?SB=n&do_Orphans=Orphans).

## Requisições

As requisições de tornar órfão, de exclusão e de mesclagem podem ser criadas clicando no link "Enviar requisições" em "Ações do pacote" no lado direito. Isso envia automaticamente um e-mail de notificação para o mantenedor do pacote atual e para a [lista de discussão aur-requests](https://mailman.archlinux.org/mailman/listinfo/aur-requests) para discussão. Os [Trusted Users](/index.php/Trusted_Users_(Portugu%C3%AAs) "Trusted Users (Português)") aceitarão ou rejeitarão a requisição.

*   Requisições de tornar órfão serão concedidas após duas semanas se o mantenedor atual não reagir.
*   Requisições de mesclagem servem para excluir o pacote base e transferir seus votos e comentários para outro pacote base. O nome do pacote base a ser mesclado é obrigatório. Observe que isso não tem nada a ver com 'git merge' ou as *merge requests* do GitLab.
*   Requisições de exclusão exibem as informações a seguir:
    *   Uma breve nota explicando o motivo da exclusão. Observe que os comentários de um pacote não apontam suficientemente as razões pelas quais um pacote está pronto para ser excluído. Porque assim que um TU entra em ação, o único lugar onde tal informação pode ser obtida é a lista de discussão do aur-requests.
    *   Detalhes de suporte, como quando um pacote é fornecido por outro pacote, se você for o mantenedor, ele é renomeado e o proprietário original concordou, etc.
    *   Após um pacote ser excluído, seu repositório Git permanece disponível no AUR.