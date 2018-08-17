**Status de tradução:** Esse artigo é uma tradução de [Users and groups](/index.php/Users_and_groups "Users and groups"). Data da última tradução: 2018-08-13\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Users_and_groups&diff=0&oldid=531655) na versão em inglês.

Artigos relacionados

*   [DeveloperWiki:UID / GID Database](/index.php/DeveloperWiki:UID_/_GID_Database "DeveloperWiki:UID / GID Database")
*   [Sudo](/index.php/Sudo "Sudo")
*   [Polkit](/index.php/Polkit "Polkit")
*   [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes")

Usuários e grupos são usados no GNU/Linux para [controle de acesso](https://en.wikipedia.org/wiki/pt:Controle_de_acesso#Na_seguran.C3.A7a_da_informa.C3.A7.C3.A3o "wikipedia:pt:Controle de acesso") — isto é, para controlar o acesso aos arquivos, diretórios e periféricos do sistema. O Linux oferece mecanismos de controle de acesso relativamente simples/grosseiros por padrão. Para opções mais avançadas, veja [ACL](/index.php/ACL "ACL") e [PAM#Configuration How-Tos](/index.php/PAM#Configuration_How-Tos "PAM").

## Contents

*   [1 Visão geral](#Vis.C3.A3o_geral)
*   [2 Permissões e propriedade](#Permiss.C3.B5es_e_propriedade)
*   [3 Lista de arquivos](#Lista_de_arquivos)
*   [4 Gerenciamento de usuário](#Gerenciamento_de_usu.C3.A1rio)
    *   [4.1 Exemplo de adicionar um usuário](#Exemplo_de_adicionar_um_usu.C3.A1rio)
    *   [4.2 Exemplo de adicionar um usuário do sistema](#Exemplo_de_adicionar_um_usu.C3.A1rio_do_sistema)
    *   [4.3 Alterar um nome de login ou diretório home do usuário](#Alterar_um_nome_de_login_ou_diret.C3.B3rio_home_do_usu.C3.A1rio)
    *   [4.4 Outros exemplos de gerenciamento de usuário](#Outros_exemplos_de_gerenciamento_de_usu.C3.A1rio)
*   [5 Base de dados de usuários](#Base_de_dados_de_usu.C3.A1rios)
*   [6 Gerenciamento de grupo](#Gerenciamento_de_grupo)
*   [7 Lista de grupos](#Lista_de_grupos)
    *   [7.1 Grupos de usuário](#Grupos_de_usu.C3.A1rio)
    *   [7.2 Grupos de sistema](#Grupos_de_sistema)
    *   [7.3 Grupos pré-systemd](#Grupos_pr.C3.A9-systemd)
    *   [7.4 Grupos sem uso](#Grupos_sem_uso)

## Visão geral

	*"root" redireciona aqui. Para o diretório raiz (root), veja [Partitioning#/](/index.php/Partitioning#.2F "Partitioning").*

Um *usuário* é qualquer pessoa que use um computador. Nesse caso, estamos descrevendo os nomes que representam esses usuários. Pode ser Maria ou Guilherme, e eles podem usar os nomes SraDragao ou Pirata no lugar de seu nome real. Tudo o que importa é que o computador possui um nome para cada conta que ele cria, e é esse o nome pelo qual uma pessoa ganha acesso para usar o computador. Alguns serviços do sistema também são executados usando contas de usuários restritas ou privilegiadas.

O gerenciamento de usuários é feito com a finalidade de segurança, limitando o acesso de determinadas formas específicas. O [superusuário](https://en.wikipedia.org/wiki/pt:Superusu%C3%A1rio "wikipedia:pt:Superusuário") (*root*) possui acesso completo ao sistema operacional e sua configuração; destina-se apenas a uso administrativo. Usuários não privilegiados podem usar os programas [su](/index.php/Su "Su") e [sudo](/index.php/Sudo "Sudo") para a escalação de privilégios controlados.

Qualquer indivíduo pode ter mais de uma conta, desde que eles usem um nome diferente para cada conta que eles criem. Além disso, existem alguns nomes reservados que não podem ser usados como "root".

Os usuários podem ser agrupados em um "grupo", e os usuários podem ser adicionados a um grupo existente para utilizar o acesso privilegiado que ele concede.

**Nota:** Iniciante deve usar essas ferramentas com cuidado e deve ficar longe de ter qualquer coisa a ver com qualquer outra conta de usuário "existente", diferente da sua.

## Permissões e propriedade

De [In UNIX Everything is a File](https://web.archive.org/web/20150110114929/http://ph7spot.com:80/musings/in-unix-everything-is-a-file):

	O sistema operacional UNIX cristaliza um par de ideias e conceitos unificadores que moldaram seu design, interface do usuário, cultura e evolução. Um dos mais importantes é provavelmente o mantra: "tudo é um arquivo", amplamente considerado como um dos pontos de definição do UNIX.

	Este princípio chave de design consiste em fornecer um paradigma unificado para acessar uma ampla gama de recursos de entrada/saída: documentos, diretórios, discos rígidos, CD-ROM, modems, teclados, impressoras, monitores, terminais e até mesmo interprocessos e redes comunicações. O truque é fornecer uma abstração comum para todos esses recursos, cada um dos quais os pais do UNIX chamaram de "arquivo". Como cada "arquivo" é exposto através da mesma API, você pode usar o mesmo conjunto de comandos básicos para ler/escrever em um disco, teclado, documento ou dispositivo de rede.

De [Extending UNIX File Abstraction for General-Purpose Networking](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.597.4699&rep=rep1&type=pdf):

	Uma abstração fundamental e muito poderosa e consistente fornecida no UNIX e sistemas operacionais compatíveis é a abstração do arquivo. Muitos serviços de sistema operacional e interfaces de dispositivos são implementados para fornecer uma metáfora de arquivo ou sistema de arquivos para aplicativos. Isso permite novos usos para, e aumenta consideravelmente o poder de, aplicações existentes — ferramentas simples projetadas com usos específicos em mente podem, com abstrações de arquivos do UNIX, serem usadas de maneiras inovadoras. Uma ferramenta simples, como o *cat*, projetada para ler um ou mais arquivos e produzir os conteúdos para a saída padrão, pode ser usada para ler a partir de dispositivos de E/S através de arquivos de dispositivos especiais, tipicamente encontrados no diretório `/dev`. Em muitos sistemas, a gravação e reprodução de áudio podem ser feitas simplesmente com os comandos "`cat /dev/audio > meu_arquivo`" e "`cat meu_arquivo > /dev/audio`", respectivamente.

Todo arquivo em um sistema GNU/Linux pertence a um usuário e a um grupo. Além disso, existem três tipos de permissões de acesso: ler, escrever e executar. Permissões de acesso diferentes podem ser aplicadas ao usuário dono de um arquivo, grupo dono e outros (aqueles que não são usuários nem do grupo dono). Pode-se determinar os donos e permissões de um arquivo ao visualizar o formato de listagem longa do comando [ls](/index.php/Ls_(Portugu%C3%AAs) "Ls (Português)"):

 `$ ls -l /boot/` 
```
total 13740
drwxr-xr-x 2 root root    4096 Jan 12 00:33 grub
-rw-r--r-- 1 root root 8570335 Jan 12 00:33 initramfs-linux-fallback.img
-rw-r--r-- 1 root root 1821573 Jan 12 00:31 initramfs-linux.img
-rw-r--r-- 1 root root 1457315 Jan  8 08:19 System.map26
-rw-r--r-- 1 root root 2209920 Jan  8 08:19 vmlinuz-linux

```

A primeira coluna exibe as permissões do arquivo (por exemplo, o arquivo `initramfs-linux.img` possui permissões `-rw-r-r--`). As terceira e quarta colunas exibem o usuário e o grupo que possuem o arquivo, respectivamente. Neste exemplo, todos os arquivos pertencem ao usuário *root* e do grupo *root*.

 `$ ls -l /media/` 
```
total 16
drwxrwx--- 1 root vboxsf 16384 Jan 29 11:02 sf_Shared

```

Neste exemplo, o diretório `sf_Shared` pertence ao usuário *root* e do grupo *vboxsf*. Também é possível determinar os donos e as permissões do arquivo usando o comando *stat*:

Usuário dono:

 `$ stat -c %U /media/sf_Shared/` 
```
root

```

Grupo dono:

 `$ stat -c %G /media/sf_Shared/` 
```
vboxsf

```

Direitos de acesso:

 `$ stat -c %A /media/sf_Shared/` 
```
drwxrwx---

```

As permissões de acesso são exibidas em três grupos de caracteres, representando as permissões do usuário dono, grupo dono e outros, respectivamente. Por exemplo, os caracteres `-rw-r-r--` indicam que o dono do arquivo tem permissão de leitura e gravação, mas não de execução (`rw-`), enquanto os usuários pertencem ao grupo dono e outros usuários só têm permissão de leitura (`r--` e `r--`). Enquanto isso, os caracteres `drwxrwx---` indicam que o dono do arquivo e os usuários pertencentes ao grupo dono possuem permissões de leitura, gravação e execução (`rwx` e `rwx`), enquanto outros usuários têm acesso negado (`---`). O primeiro caractere representa o tipo do arquivo.

Liste arquivos que pertencem a um usuário ou grupo com o utilitário *find*:

```
# find / -group *grupo*

```

```
# find / -user *usuário*

```

O usuário e o grupo donos de um arquivo podem ser alterados com o comando [chown](/index.php?title=Chown_(Portugu%C3%AAs)&action=edit&redlink=1 "Chown (Português) (page does not exist)") (*change owner* ou mudar o dono). As permissões de acesso a um arquivo podem ser alteradas com o comando [chmod](/index.php/Chmod "Chmod") (*change mode* ou mudar o modo).

Veja [chown(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chown.1), [chmod(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1) e [Permissões de acesso a arquivos e diretórios](http://www.guiafoca.org/cgs/guia/inic_interm/ch-perm.html) para detalhes adicionais.

## Lista de arquivos

**Atenção:** Não edite esses arquivos na mão. Há utilitários que lidam corretamente com a trava e evitam invalidar o formato da base de dados. Veja [#Gerenciamento de usuário](#Gerenciamento_de_usu.C3.A1rio) e [#Gerenciamento de grupo](#Gerenciamento_de_grupo) para uma visão geral.

| Arquivo | Propósito |
| `/etc/shadow` | Informações da conta do usuário seguras |
| `/etc/passwd` | Informações da conta do usuário |
| `/etc/gshadow` | Contém a "sombra" da informação para contas de grupo |
| `/etc/group` | Define os grupos para aos quais os usuários pertencem |
| `/etc/sudoers` | Lista de quem pode executar o que com sudo |
| `/home/*` | Diretórios *home* |

## Gerenciamento de usuário

Para listar os usuários conectados no sistema, o comando *who* pode ser usado. Para listar todas as contas de usuários existentes, incluindo suas propriedades armazenadas na base de dados de [usuário](#Base_de_dados_de_usu.C3.A1rios), execute `passwd -Sa` como root. Veja [passwd(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/passwd.1) para a descrição do formato de saída.

Para adicionar um novo usuário, use o comando *useradd*:

```
# useradd -m -g *grupo_inicial* -G *grupos_adicionais* -s *shell_de_login* *nome_de_usuário*

```

	`-m`/`--create-home`

	cria o diretório pessoal do usuário como `/home/*nome_de_usuário*`. Dentro de seu diretório pessoal, um usuário que não seja root pode escrever arquivos, exclui-los, instalar programas e por aí vai.

	`-g`/`--gid`

	define o nome ou número de grupo do grupo inicial do usuário. Se especificado, o nome de grupo deve existir; se um número de grupo for fornecido, ele deve se referir a um grupo já existente. Se não especificado, o comportamento de *useradd* vai depender da variável `USERGROUPS_ENAB` contida em `/etc/login.defs`. O comportamento padrão (`USERGROUPS_ENAB yes`) é criar um grupo com o nome igual ao nome de usuário, com `GID` igual a `UID`.

	`-G`/`--groups`

	introduz uma lista de grupos suplementares dos quais o usuários também é membro. Cada grupo é separado do próximo por uma vírgula, com nenhuma no meio. O padrão é para o usuário pertencer a apenas o grupo inicial.

	`-s`/`--shell`

	define o caminho e o nome do arquivo do shell de login padrão do usuário. Após o processo de inicialização ter concluído, o shell de login padrão é o especificado aqui. Assegure-se de que o pacote do shell escolhido está instalado se escolher algo diferente do [Bash](/index.php/Bash "Bash").

**Atenção:** Para ser capaz de se autenticar, o shell de login deve ser um dos listados em `/etc/shells`, do contrário o módulo [PAM](/index.php/PAM "PAM")`pam_shell` vai negar a requisição de login. Em especial, não use o caminho `/usr/bin/bash` em vez de `/bin/bash`, a menos que propriamente configurado em `/etc/shells`.

**Nota:** A senha para o usuário recém criado deve então ser definido, usando *passwd* conforme mostrado em [#Exemplo de adicionar um usuário](#Exemplo_de_adicionar_um_usu.C3.A1rio).

Quando o shell de login destina-se a ser não funcional, por exemplo quando a conta de usuário é criada para um serviço específico, `/usr/bin/nologin` pode ser especificado no lugar de uma shell comum para educadamente recusar um login (veja [nologin(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nologin.8)).

### Exemplo de adicionar um usuário

Para adicionar um novo usuário chamado `archie`, crar seu diretório pessoal e, do contrário, usando todos os padrões nos termos de grupos, nomes de pastas, shell usado e vários outros parâmetros:

```
# useradd --create-home archie

```

**Dica:** O valor padrão usado para o shell de login da nova conta pode ser exibida usando `useradd ---default`. O padrão é Bash, um shell diferente pode ser especificado com a opção `-s`/`--shell`.

Apesar de ser obrigatório proteger o recém criado usuário `archie` com uma senha, é altamente recomendado fazê-lo:

```
# passwd archie

```

O comando *useradd* acima pode também criar automaticamente um grupo chamado `archie` com o mesmo GID que o UID do usuário `archie` e torna este o grupo padrão para `archie` no login. Fazer com que cada usuário tenha seu próprio grupo (com o nome do grupo igual ao nome do usuário e GID, o mesmo que o UID) é a maneira preferida de adicionar usuários.

Você poderia fazer o grupo padrão alguma outra coisa usando a opção `-g`, mas note que, em sistemas multiusuários, o uso de um único grupo padrão (por exemplo, `users`) para cada usuário não é recomendado. A razão é que, tipicamente, o método para facilitar o acesso de gravação compartilhada para grupos específicos de usuários é definir o valor [umask](/index.php/Umask_(Portugu%C3%AAs) "Umask (Português)") do usuário para `002`, o que significa que o grupo padrão sempre terá, por padrão, acesso de gravação a qualquer arquivo que você crie. Veja também [User Private Groups](https://security.ias.edu/how-and-why-user-private-groups-unix). Se um usuário deve ser um membro de um grupo específico, especifique aquele grupo como um grupo suplementar ao criar o usuário.

No cenário recomendado, onde o grupo padrão tem o mesmo nome que o nome do usuário, todos os arquivos são somente graváveis para o usuário que os criou. Para permitir o acesso de gravação a um grupo específico, os arquivos/pastas compartilhados podem ser gravados por padrão para todos neste grupo e o grupo dono pode ser fixado automaticamente no grupo que possui o diretório pai configurando o bit *setgid* neste diretório:

```
# chmod g+s *nosso_diretório_compartilhado*

```

Caso contrário, o grupo padrão do criador do arquivo (geralmente o mesmo que o nome do usuário) é usado.

Se uma mudança de GID for necessária temporariamente, você também pode usar o comando *newgrp* para alterar o GID padrão do usuário para outro GID em tempo de execução. Por exemplo, depois de executar `newgrp *nomegrupo*`, os arquivos criados pelo usuário serão associados ao GID `*nomegrupo*`, sem requerer um novo login. Para voltar ao GID padrão, execute *newgrp* sem um nome de grupo.

### Exemplo de adicionar um usuário do sistema

Os usuários do sistema podem ser usados para executar processos/daemons em um usuário diferente, protegendo (por exemplo, com [chown](/index.php/Chown "Chown")) arquivos e/ou diretórios e mais exemplos de *hardening* do computador.

Com o seguinte comando, um usuário do sistema sem acesso ao shell e sem um diretório `home` é criado (opcionalmente, anexe o parâmetro `-U` para criar um grupo com o mesmo nome que o usuário e adicione o usuário para este grupo):

```
# useradd -r -s /usr/bin/nologin *nome_de_usuário*

```

### Alterar um nome de login ou diretório home do usuário

Para alterar o diretório *home* do usuário:

```
# usermod -d /meu/novo/home -m *nome_de_usuário*

```

A opção `-m` também cria automaticamente o novo diretório e move o conteúdo para lá.

**Dica:** Você pode criar um link do antigo diretório inicial do usuário para o novo. Isso permitirá que os programas encontrem arquivos que tenham caminhos codificados.
```
# ln -s /meu/novo/home/ /meu/antigo/home

```

Certifique-se de que **não** haja `/` ao final de `/meu/novo/home`.

Para alterar o nome de login de um usuário:

```
# usermod -l *novo_nome* *antigo_nome*

```

**Atenção:** Certifique-se de que você não está autenticado como o usuário cujo nome você está prestes a mudar. Abra um novo tty (`Ctrl+Alt+F1`) e se autentique como *root* ou como outro usuário e su para *root*. O *usermod* deve evitar que você faça isso por engano.

Alterar um nome de usuário é seguro e fácil quando feito corretamente, basta usar o comando [usermod](#Outros_exemplos_de_gerenciamento_de_usu.C3.A1rio). Se o usuário estiver associado a um grupo com o mesmo nome, você pode renomear isso com o comando [groupmod](#Gerenciamento_de_grupo).

Alternativamente, o arquivo `/etc/passwd` pode ser editado diretamente, veja [#Base de dados de usuários](#Base_de_dados_de_usu.C3.A1rios) para uma introdução ao seu formato.

Também tenha em mente as notas a seguir:

*   Se você estiver usando [sudo](/index.php/Sudo "Sudo"), certifique-se de atualizar o `/etc/sudoers` para refletir o(s) novo(s) usuário(s) (via o comando *visudo* como root).
*   Os [crontabs](/index.php/Cron#Crontab_format "Cron") pessoais precisam ser ajustados renomeando o arquivo do usuário em `/var/spool/cron` do nome antigo para o novo, e depois abrindo com `crontab -e` para alterar os caminhos relevantes e fazê-lo ajustar as permissões do arquivo.
*   O conteúdo das pastas e dos arquivos pessoais do [wine](/index.php/Wine "Wine") em `~/.wine/drive_c/users`, `~/.local/share/applications/wine/Programs` e possivelmente mais, precisam ser renomeados/editados manualmente.
*   Certos complementos do Thunderbird, como o [Enigmail](https://www.enigmail.net/index.php/en/), podem precisar ser reinstalados.
*   Qualquer coisa no seu sistema (atalhos da área de trabalho, scripts de shell, etc.) que usa um caminho absoluto para seu diretório *home* (ou seja, `/home/antigo_nome`) precisará ser alterado para refletir seu novo nome. Para evitar esses problemas em scripts de shell, use as variáveis `~` ou `$HOME` para diretórios *home*.
*   Além disso, não se esqueça de editar adequadamente os arquivos de configuração em `/etc` que dependem de seu caminho absoluto (ou seja, Samba, CUPS, etc.). Uma boa maneira de aprender quais arquivos você precisa atualizar envolve o uso do comando grep desta maneira: `grep -r {antigo_usuário} *`

### Outros exemplos de gerenciamento de usuário

Para adicionar um usuário a outros grupos, use (`*grupos_adicionais*` é uma lista separada por vírgula):

```
# usermod -aG *grupos_adicionais* *nome_de_usuário*

```

**Atenção:** Se a opção `-a` for omitida no comando *usermod* acima, o usuário é removido de todos os outros grupos não listados em `*grupos_adicionais*` (i.e. o usuário será membro apenas daqueles grupos em `*grupos_adicionais*`).

Alternativamente, *gpasswd* pode ser usado, embora o nome de usuário só possa ser adicionado (ou removido) de um grupo por vez:

```
# gpasswd --add *nome_de_usuário* *grupo*

```

Para inserir informações do usuário para o comentário [GECOS](#Base_de_dados_de_usu.C3.A1rios) (ex. o nome completo do usuário), digite:

```
# chfn *nome_de_usuário*

```

(dessa forma, *chfn* é executado em modo interativo).

Alternativamente, o comentário GECOS pode ser definido mais livremente com:

```
# usermod -c "Comentário" *nome_de_usuário*

```

Para marcar a senha de um usuário como expirada, exigindo que ele crie uma nova senha na primeira vez que fizerem login, digite:

```
# chage -d 0 *nome_de_usuário*

```

Contas de usuário podem ser excluídas com o comando *userdel*:

```
# userdel -r *nome_de_usuário*

```

A opção `-r` especifica que o diretório *home* do usuário e o *spool* de correios também devem ser excluídos.

Para alterar o shell de login do usuário:

```
# usermod -s */bin/bash* *nome_de_usuário*

```

**Dica:** O script [adduser](https://aur.archlinux.org/packages/adduser/) permite realizar os trabalhos de *useradd*, *chfn* e *passwd* interativamente. Veja também [FS#32893](https://bugs.archlinux.org/task/32893).

## Base de dados de usuários

As informações do usuário local são armazenadas no arquivo de texto simples `/etc/passwd`: cada uma das suas linhas representa uma conta de usuário e tem sete campos delimitados por caracteres de dois pontos.

```
*conta:senha:UID:GID:GECOS:diretório:shell*

```

Sendo que:

*   `*conta*` é o nome de usuário. Esse campo não pode estar vazio. Padrão regras de nomeação *NIX aplicam-se.
*   `*senha*` é a senha do usuário.
    **Atenção:** O arquivo `passwd` é legível por todos, então armazenar senhas (em hash ou de outra forma) neste arquivo é inseguro. Em vez disso, o Arch Linux usa [senhas em *shadow*](/index.php/Security#Password_hashes "Security"): o campo `senha` conterá um caractere reservado (`x`) indicando que a senha em hash está salva no arquivo de acesso restrito `/etc/shadow`. Por esse motivo, é recomendado sempre alterar senhas usando o comando **passwd**.

*   `*UID*` é a identificação numérica de usuário. No Arch, o nome do primeiro login (após o *root*) tem UID 1000, por padrão; entradas subsequentes de UID para usuários devem ser maiores que 1000.
*   `*GID*` é a identificação numérica de grupo primário para o usuário. Valores numéricos para GIDs são listados em [/etc/group](#Gerenciamento_de_grupo).
*   `*GECOS*` é um campo opcional com propósitos informacionais; geralmente, ele contém o nome completo do usuário, mas também pode ser usado por serviços, como o *finger*, e gerenciado com o comando [chfn](#Outros_exemplos_de_gerenciamento_de_usu.C3.A1rio). Esse campo é opcional e pode ser deixado em branco.
*   `*diretório*` é usado pelo comando de login para definir a variável de ambiente `$HOME`. Vários serviços com seus próprios usuários usam `/`, mas os usuários normais costumam definir uma pasta em `/home`.
*   `*shell*` é o caminho para o [shell de comandos](/index.php/Shell_de_comandos "Shell de comandos") padrão do usuário. Esse campo é opcional e tem como padrão `/bin/bash`.

Exemplo:

```
joao:x:1001:100:João da Silva,algum comentário aqui,,:/home/joao:/bin/bash

```

Expandindo, isso significa: usuário `joao`, cuja senha está em `/etc/shadow`, cujo UID é 1001 e cujo grupo primário é 100\. João da Silva é o nome completo dele e existe um comentário associado a sua conta; Seu diretório inicial é `/home/joao` e ele está usando [Bash](/index.php/Bash "Bash").

O comando *pwck* pode ser usado para verificar a integridade da base de dados de usuário. Ele pode ordenar a lista de usuários por GID ao mesmo tempo, o que pode ser útil para comparação:

```
# pwck -s

```

**Nota:** Os padrões do Arch Linux dos arquivos são criados como arquivos *.pacnew* pelas novas versões do pacote [filesystem](https://www.archlinux.org/packages/?name=filesystem). A menos que o *pacman* emita mensagens relacionadas para ação, esses arquivos *.pacnew* podem, e devem, ser desconsiderados/removidos. Novos usuários e grupos padrão obrigatórios são adicionados ou re-adicionados conforme necessário por [systemd-sysusers(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sysusers.8).

## Gerenciamento de grupo

`/etc/group` é o arquivo que define os grupos no sistema (veja [group(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/group.5) para detalhes).

Mostre associação a grupos com o comando `groups`:

```
$ groups *usuário*

```

Se `*usuário*` for omitido, os nomes de grupos do usuário atual são exibidos.

O comando `id` fornece detalhes adicionais, tal como o UID do usuário e GIDs associados:

```
$ id *usuário*

```

Para listar todos os grupos no sistema:

```
$ cat /etc/group

```

Crie novos grupos com o comando `groupadd`:

```
# groupadd *grupo*

```

Adicione usuários a um grupo com o comando `gpasswd`:

```
# gpasswd -a *usuário* *grupo*

```

Modifique um grupo existente com `groupmod`; por exemplo, para renomear o grupo `antigo_grupo` para `novo_grupo` enquanto preserva o gid (todos os arquivos previamente pertencentes ao `antigo_grupo` serão do `novo_grupo`):

```
# groupmod -n *novo_grupo* *antigo_grupo*

```

**Nota:** Isso vai alterar um nome de grupo, mas não o GID numérico do grupo.

Para excluir grupos existentes:

```
# groupdel *grupo*

```

Para remover usuários de um grupo antigo:

```
# gpasswd -d *usuário* *grupo*

```

Se o usuário estiver atualmente autenticado, ele deve encerrar a sessão e entrar novamente para que a alteração tenha efeito.

O comando *grpck* pode ser usado para verificar a integridade dos arquivos de grupo do sistema.

Atualizações ao pacote [filesystem](https://www.archlinux.org/packages/?name=filesystem) criam arquivos *.pacnew*. Ao contrário dos arquivos *.pacnew* para o [#Gerenciamento de usuário](#Gerenciamento_de_usu.C3.A1rio), essas alterações podem ser ignoradas/removidas, porque o script de instalação adiciona quaisquer novos grupos exigidos.

## Lista de grupos

Essa seção explica o propósito dos grupos essenciais do pacote [core/filesystem](https://git.archlinux.org/svntogit/packages.git/tree/trunk/group?h=packages/filesystem). Há muitos outros grupos, que serão criados com o [GID correto](/index.php/DeveloperWiki:UID_/_GID_Database "DeveloperWiki:UID / GID Database") quando o pacote relevante for instalado. Veja a página principal do software para detalhe.

**Nota:** Uma remoção posterior de um pacote não remove o usuário/grupo (UID/GID) criado automaticamente. Isto é intencional porque qualquer arquivo criado durante a sua utilização seria deixado órfão como um potencial risco de segurança.

### Grupos de usuário

Usuários não *root* de estação de trabalho ou desktop frequentemente precisam ser adicionados a alguns dos grupos a seguir para permitir acesso a periféricos de hardware e facilitar administração de sistema:

| Grupo | Arquivos afetados | Propósito |
| adm | Grupo administrativo, similar ao `wheel`. |
| ftp | `/srv/ftp/` | Acesso a arquivos servidos por servidores [FTP](https://en.wikipedia.org/wiki/pt:FTP "wikipedia:pt:FTP"). |
| games | `/var/games` | Acesso a alguns softwares de jogos. |
| http | `/srv/http/` | Acesso a arquivos servidos por servidores [HTTP](https://en.wikipedia.org/wiki/pt:HTTP "wikipedia:pt:HTTP"). |
| log | Acesso a arquivos de registros de log em `/var/log/` criados pelo [syslog-ng](/index.php/Syslog-ng "Syslog-ng"). |
| rfkill | `/dev/rfkill` | Direito para controlar estado de energia de dispositivos sem fio (usado pelo *rfkill*). |
| sys | Direito para administrar impressoras no [CUPS](/index.php/CUPS "CUPS"). |
| systemd-journal | `/var/log/journal/*` | Pode ser usado para fornecer acesso somente leitura aos logs do systemd, como uma alternativa ao `adm` e ao `wheel` [[1]](https://cgit.freedesktop.org/systemd/systemd/tree/README?id=fdbbf0eeda929451e2aaf34937a72f03a225e315#n190). Do contrário, apenas mensagens geradas pelo usuário são exibidas. |
| users | Grupo padrão de usuários. |
| uucp | `/dev/ttyS[0-9]+`, `/dev/tts/[0-9]+`, `/dev/ttyUSB[0-9]+`, `/dev/ttyACM[0-9]+`, `/dev/rfcomm[0-9]+` | Portas seriais RS-232 e dispositivos conectados a elas. |
| wheel | Grupo administrativo, comumente usado para dar acesso aos utilitários [sudo](/index.php/Sudo "Sudo") e [su](/index.php/Su "Su") (nenhum deles usa-o por padrão, sendo configurável em `/etc/pam.d/su` e `/etc/pam.d/su-l`). Também pode ser usado para ganhar acesso total de leitura aos arquivos de [journal](/index.php/Systemd_(Portugu%C3%AAs)#Journal "Systemd (Português)"). |

### Grupos de sistema

Os seguintes grupos são usados para propósitos de sistema, uma atriubuição para usuários é necessária apenas para propósitos dedicados:

| Grupo | Arquivos afetados | Propósito |
| dbus | Usado internamente pelo [dbus](https://www.archlinux.org/packages/?name=dbus) |
| kmem | `/dev/port`, `/dev/mem`, `/dev/kmem` |
| locate | `/usr/bin/locate`, `/var/lib/locate`, `/var/lib/mlocate`, `/var/lib/slocate` | Veja [locate](/index.php/Locate_(Portugu%C3%AAs) "Locate (Português)"). |
| lp | `/dev/lp[0-9]*`, `/dev/parport[0-9]*` | Acesso a dispositivos de porta paralela (impressoras e outros). |
| mail | `/usr/bin/mail` |
| nobody | Grupo sem privilégios. |
| proc | `/proc/*pid*/` | Um grupo autorizado a aprender informação de processo que, do contrário, seria proibido pela opção de montagem `hidepid=` do [sistema de arquivos proc](https://www.kernel.org/doc/Documentation/filesystems/proc.txt). O grupo deve ser definido explicitamente com a opção de montagem `gid=`. |
| root | `/*` | Administração e controle total do sistema (root, admin). |
| smmsp | Grupo do [sendmail](/index.php/Sendmail "Sendmail"). |
| tty | `/dev/tty`, `/dev/vcc`, `/dev/vc`, `/dev/ptmx` |
| utmp | `/run/utmp`, `/var/log/btmp`, `/var/log/wtmp` |

### Grupos pré-systemd

Antes do Arch migrar para o [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"), os usuários tinham que ser adicionados manualmente a esses grupos para poder acessar os dispositivos correspondentes. Essa forma se tornou obsoleta em favor do [udev](/index.php/Udev "Udev") marcar os dispositivos com uma [etiqueta](https://github.com/systemd/systemd/blob/master/src/login/70-uaccess.rules) `uaccess` e *logind* atribuindo as permissões aos usuários de forma dinâmica via [ACLs](/index.php/ACL "ACL") de acordo com qual sessão está atualmente ativa. Observe que a sessão não deve ser quebrada para que isso funcione (consulte [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting")).

Existem algumas exceções notáveis que exigem a adição de um usuário a alguns desses grupos: por exemplo, se você quiser permitir que os usuários acessem o dispositivo mesmo quando não estiverem logados. No entanto, observe que adicionar usuários aos grupos pode até fazer alguma funcionalidade quebrar (por exemplo, o grupo `audio` irá quebrar a troca rápida de usuários e permite que os aplicativos bloqueiem o mixer de software).

| Grupo | Arquivos afetados | Propósito |
| audio | `/dev/audio`, `/dev/snd/*`, `/dev/rtc0` | Acesso direto ao hardware de som, para todas as sessões. Ainda é necessário fazer [ALSA (Português)](/index.php/ALSA_(Portugu%C3%AAs) "ALSA (Português)") e [OSS](/index.php/OSS "OSS") funcionar nas sessões remotas, veja [ALSA#User privileges](/index.php/ALSA#User_privileges "ALSA"). Também é usado no [JACK](/index.php/JACK "JACK") para fornecer aos usuários permissões de processamento em tempo real. |
| disk | `/dev/sd[a-z][1-9]` | Acesso para bloquear dispositivos não afetados por outros grupos, como `optical`, `floppy` e `storage`. |
| floppy | `/dev/fd[0-9]` | Acesso a unidades de disquete. |
| input | `/dev/input/event[0-9]*`, `/dev/input/mouse[0-9]*` | Acesso a dispositivos de entrada. Introduzido no systemd 215 [[2]](http://lists.freedesktop.org/archives/systemd-commits/2014-June/006343.html). |
| kvm | `/dev/kvm` | Aceso a máquinas virtuais usando [KVM](/index.php/KVM "KVM"). |
| optical | `/dev/sr[0-9]`, `/dev/sg[0-9]` | Acesso a dispositivos óticos, como unidades de CD e DVD. |
| scanner | `/var/lock/sane` | Acesso a hardware de scanner. |
| storage | Acesso a unidades removíveis, como as unidades de HD externo USB, pendrives, MP3 players; permite ao usuário montar dispositivos de armazenamento. |
| video | `/dev/fb/0`, `/dev/misc/agpgart` | Acesso a dispositivos de captura de vídeo, aceleração hardware 2D/3D, framebuffer ([X](/index.php/Xorg_(Portugu%C3%AAs) "Xorg (Português)") pode ser usado *sem* pertencer a este grupo). |

### Grupos sem uso

Os seguintes grupos estão atualmente sem uso para qualquer propósito:

| Grupo | Arquivos afetados | Propósito |
| bin | nenhum | Histórico |
| daemon |
| lock | Usado para acesso a arquivo de trava. Necessário para, por exemplo, [gnokii](https://www.archlinux.org/packages/?name=gnokii). |
| mem |
| network | Sem uso por padrão. Pode ser usado, por exemplo, para conceder acesso ao NetworkManager (veja [NetworkManager#Set up PolicyKit permissions](/index.php/NetworkManager#Set_up_PolicyKit_permissions "NetworkManager")). |
| power |
| uuidd |