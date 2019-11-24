**Status de tradução:** Esse artigo é uma tradução de [Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists"). Data da última tradução: 2019-11-20\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Access_Control_Lists&diff=0&oldid=589489) na versão em inglês.

[Lista de controle de acesso](https://en.wikipedia.org/wiki/pt:Lista_de_controle_de_acesso "wikipedia:pt:Lista de controle de acesso") (ACL, do inglês "Access Control List") fornece um mecanismo de permissão adicional e mais flexível para [sistemas de arquivos](/index.php/File_systems "File systems"). Ele foi projetado para ajudar com as permissões de arquivo UNIX. A ACL permite conceder permissões para qualquer usuário ou grupo a qualquer recurso de disco.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Configuração](#Configuração)
    *   [2.1 Habilitando ACL](#Habilitando_ACL)
    *   [2.2 Definindo ACL](#Definindo_ACL)
    *   [2.3 Mostrando ACL](#Mostrando_ACL)
*   [3 Exemplos](#Exemplos)
    *   [3.1 Saída do comando ls](#Saída_do_comando_ls)
*   [4 Concedendo permissões de execução para arquivos privados a um servidor web](#Concedendo_permissões_de_execução_para_arquivos_privados_a_um_servidor_web)
*   [5 Veja também](#Veja_também)

## Instalação

O pacote [acl](https://www.archlinux.org/packages/?name=acl) é uma dependência do [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"), e já deve estar instalado.

## Configuração

### Habilitando ACL

Para habilitar a ACL, o sistema de arquivos deve ser montado com a opção `acl`. Você pode usar [fstab](/index.php/Fstab "Fstab") para torná-lo permanente em seu sistema.

Existe a possibilidade de a opção `acl` já estar habilitada como opção de montagem padrão no sistema de arquivos. [Btrfs](/index.php/Btrfs "Btrfs") faz e os sistemas de arquivos Ext2/[3](/index.php/Ext3 "Ext3")/[4](/index.php/Ext4_(Portugu%C3%AAs) "Ext4 (Português)") também. Use o seguinte comando para verificar a opção de partições ext* formatadas:

 `# tune2fs -l /dev/sd*XY* | grep "Default mount options:"` 
```
Default mount options:    user_xattr acl

```

Verifique também se a opção de montagem padrão não está substituída; nesse caso, você verá `noacl` em `/proc/mounts` na linha relevante.

Você pode definir as opções de montagem padrão de um sistema de arquivos usando o comando `tune2fs -o *opção* *partição*`, por exemplo:

```
# tune2fs -o acl /dev/sd*XY*

```

Usar as opções de montagem padrão em vez de uma entrada em `/etc/fstab` é muito útil para unidades externas, essa partição será montada com a opção `acl` também em outras máquinas Linux. Não há necessidade de editar o `/etc/fstab` em todas as máquinas.

**Nota:**

*   `acl` é especificado como opção de montagem padrão ao criar um sistema de arquivos ext2/3/4\. Isso está configurado em `/etc/mke2fs.conf`.
*   As opções padrão de montagem não estão listadas em `/proc/mounts`.

### Definindo ACL

A ACL pode ser modificada usando o comando *setfacl*.

**Dica:** Você pode listar as alterações de permissão de arquivo/diretório sem modificar as permissões (ou seja, "dry-run") anexando a opção `--test`.

Para definir permissões para um usuário (`*usuário*` é o nome do usuário ou o ID):

```
# setfacl -m "u:*usuário:permissões*" <arquivo/diretório>

```

Para definir permissões para um grupo (`*grupo*` é o nome ou o ID do grupo):

```
# setfacl -m "g:*grupo:permissões*" <arquivo/diretório>

```

Para definir permissões para outras pessoas:

```
# setfacl -m "other:*permissões*" <arquivo/diretório>

```

Para permitir que todos os arquivos ou diretórios *recém-criados* herdem entradas do diretório pai (isso não afetará os arquivos que serão *copiados* para o diretório):

```
# setfacl -dm "*entrada*" <diretório>

```

Para remover uma entrada específica:

```
# setfacl -x "*entrada*" <arquivo/diretório>

```

Para remover as entradas padrão:

```
# setfacl -k <arquivo/diretório>

```

Para remover todas as entradas (as entradas do dono, grupo e outras são mantidas):

```
# setfacl -b <arquivo/diretório>

```

**Nota:** O comportamento padrão de *setfacl* é recalcular a entrada da máscara da ACL, a menos que uma entrada `--mask` tenha sido explicitamente fornecida. A entrada da máscara é definida para a união de todas as permissões do grupo proprietário e todas as entradas de usuário e grupo nomeadas (essas são exatamente as entradas afetadas pela entrada da máscara).

**Dica:** Para aplicar operações a todos os arquivos e diretórios recursivamente, acrescente o argumento `-R`.

### Mostrando ACL

Para mostrar permissões, use:

```
# getfacl <arquivo/diretório>

```

## Exemplos

Defina todas as permissões para o usuário `joao` no arquivo chamado `abc`:

```
# setfacl -m "u:joao:rwx" abc

```

Verifica permissões:

 `# getfacl abc` 
```
# file: abc
# owner: alguém
# group: alguém
user::rw-
user:joao:rwx
group::r--
mask::rwx
other::r--

```

Altera permissões para o usuário `joao`:

```
# setfacl -m "u:joao:r-x" abc

```

Verifica permissões:

 `# getfacl abc` 
```
# file: abc
# owner: alguém
# group: alguém
user::rw-
user:joao:r-x
group::r--
mask::r-x
other::r--

```

Remove todas as entradas estendidas ACL:

```
# setfacl -b abc

```

Verifica permissões:

 `# getfacl abc` 
```
# file: abc
# owner: alguém
# group: alguém
user::rw-
group::r--
other::r--

```

### Saída do comando ls

Você notará que há uma ACL para um determinado arquivo porque ele exibirá um `**+**` (sinal de mais) após as permissões do Unix na saída de `ls -l`.

 `$ ls -l /dev/audio` 
```
crw-rw----+ 1 root audio 14, 4 nov.   9 12:49 /dev/audio

```
 `$ getfacl /dev/audio` 
```
getfacl: Removing leading '/' from absolute path names
# file: dev/audio
# owner: root
# group: audio
user::rw-
user:solstice:rw-
group::rw-
mask::rw-
other::---

```

## Concedendo permissões de execução para arquivos privados a um servidor web

A técnica a seguir descreve como um processo como um [servidor web](/index.php/Web_server "Web server") pode receber acesso a arquivos que residem no diretório inicial de um usuário, sem comprometer a segurança, fornecendo acesso ao mundo inteiro.

A seguir, presumimos que o servidor web é executado como usuário `http` e concedemos acesso ao diretório "home" do `geoffrey` `/home/geoffrey`.

A primeira etapa é conceder permissões de execução para o usuário `http`:

```
# setfacl -m "u:http:--x" /home/geoffrey

```

**Nota:** Permissões de execução para um diretório são necessárias para um processo listar o conteúdo do diretório.

Como o usuário `http` agora pode acessar arquivos em `/home/geoffrey`, outros não precisam mais acessar:

```
# chmod o-rx /home/geoffrey

```

Use `getfacl` para verificar as alterações:

 `$ getfacl /home/geoffrey` 
```
getfacl: Removing leading '/' from absolute path names
# file: home/geoffrey
# owner: geoffrey
# group: geoffrey
user::rwx
user:http:--x
group::r-x
mask::r-x
other::---

```

Como mostra a saída acima, o `other` não tem mais permissões, mas o usuário `http` ainda pode acessar os arquivos, portanto, a segurança pode ser considerada aumentada.

**Nota:** Pode ser necessário conceder acesso de gravação para o usuário `http` em diretórios e/ou arquivos específicos:
```
# setfacl -dm "u:http:rwx" /home/geoffrey/project1/cache

```

## Veja também

*   [getfacl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getfacl.1)
*   [setfacl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfacl.1)
*   Um [guia](http://vanemery.net/Linux/ACL/linux-acl.html) antigo, mas ainda relevante (e completo) sobre ACL
*   [Como definir permissões de arquivo padrão para todas as pastas/arquivos em um diretório?](http://unix.stackexchange.com/questions/1314/how-to-set-default-file-permissions-for-all-folders-files-in-a-directory) *(inglês)*