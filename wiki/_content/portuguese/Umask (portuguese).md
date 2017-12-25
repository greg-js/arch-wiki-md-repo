Artigos relacionados

*   [File permissions and attributes](/index.php/File_permissions_and_attributes "File permissions and attributes")

O utilitário *umask* é usado para controlar a máscara de modo de criação de arquivo, o qual determinar o valor inicial dos bits de permissão de arquivo para arquivos recém-criados. O seguinte comportamento deste utilitário é padronizado pelo [POSIX](https://en.wikipedia.org/wiki/pt:POSIX "wikipedia:pt:POSIX") e descrito no [Manual do Programador POSIX](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/umask.html). Porque o *umask* afeta o ambiente de execução do shell atual, é geralmente implementado como um comando incorporado de um shell.

## Contents

*   [1 Significado da máscara de modo](#Significado_da_m.C3.A1scara_de_modo)
*   [2 Exibir o valor atual da máscara](#Exibir_o_valor_atual_da_m.C3.A1scara)
*   [3 Definir o valor da máscara](#Definir_o_valor_da_m.C3.A1scara)
*   [4 Veja também](#Veja_tamb.C3.A9m)

## Significado da máscara de modo

A máscara de modo contém os bits de permissão que **não** devem ser definidos em um arquivo recém-criado e, portanto, é uma [negação](https://en.wikipedia.org/wiki/pt:Nega%C3%A7%C3%A3o "wikipedia:pt:Negação") (também chamado, em inglês, de [*logical complement*](https://en.wikipedia.org/wiki/Logical_complement "wikipedia:Logical complement")) dos bits de permissão definidos em um arquivo recém-criado. Se algum bit na máscara estiver configurado para `1`, a permissão correspondente para o arquivo recém-criado será desabilitada. Assim, a máscara atua como um filtro para retirar os bits de permissão e ajuda na configuração do acesso padrão aos arquivos.

O valor resultante para os bits de permissão a serem configurados em um arquivo recém-criado é calculado usando a **negação de [condicional ou implicação material](https://en.wikipedia.org/wiki/pt:Condicional_material "wikipedia:pt:Condicional material")** (também chamada, em inglês, de [*material nonimplication* ou *abjunction*](https://en.wikipedia.org/wiki/Material_nonimplication "wikipedia:Material nonimplication"), que pode ser expressa em notação lógica:

```
R: (D & (~M))

```

Isso é, as permissões resultantes `R` são o resultado da [conjunção binário (AND)](https://en.wikipedia.org/wiki/pt:Conjun%C3%A7%C3%A3o_l%C3%B3gica "wikipedia:pt:Conjunção lógica") de permissões padrão `D` e a [negação binária (NOT)](https://en.wikipedia.org/wiki/pt:L%C3%B3gica_bin%C3%A1ria#NOT "wikipedia:pt:Lógica binária") da máscara de modo de criação de arquivo `M`.

**Nota:**

*   O Linux não permite que um arquivo seja criado com permissões de execução – de fato, as permissões de criação padrão são `777` para diretórios, mas apenas `666` para arquivos.
*   No Linux, apenas os bits de permissão do arquivo da máscara são usados – veja [umask(2)](http://jlk.fjfi.cvut.cz/arch/manpages/man/umask.2). Os bits *suid*, *sgid* e *sticky* da máscara são ignorados.

Por exemplo, suponha que a máscara do modo de criação de arquivos seja 027\. Aqui, a representação bit a bit de cada dígito representa:

*   `0` significa não definido para os bits de permissão de *usuário* em um arquivo recém-criado
*   `2` significa não definido para os bits de permissão de *grupo* em um arquivo recém-criado
*   `7` significa não definido para os bits de permissão de *outro* em um arquivo recém-criado

Com as informações fornecidas pela tabela abaixo, isso significa que para um arquivo recém-criado, por exemplo, pertencente ao usuário `Usuario1` e o grupo `Grupo1`, o `Usuario1` tem todas as permissões possíveis (valor octal `7`) para o arquivo recém-criado, outros usuários do grupo `Grupo1` não possuem permissões de escrita (valor octal `5`) e qualquer outro usuário não possui quaisquer permissões (valor octal `0`) sobre o arquivo recém-criado. Então, com a máscara `027` deste exemplo, os arquivos serão criados com permissões `750`.

<caption></caption>
| Octal | Binário | Singinificado |
| `0` | `000` | sem permissão |
| `1` | `001` | somente execução |
| `2` | `010` | somente escrita |
| `3` | `011` | somente escrita e execução |
| `4` | `100` | somente leitura |
| `5` | `101` | leitura e execução |
| `6` | `110` | leitura e escrita |
| `7` | `111` | leitura, escrita e execução |

## Exibir o valor atual da máscara

Para exibir a máscara atual, basta executar `umask` sem especificar nenhum argumento. O estilo de saída padrão depende da implementação, mas geralmente é octal:

 `$umask` 
```
0027

```

Quando a opção `-S`, padronizada pelo POSIX, é usada, a máscara será exibida usando a notação simbólica. No entanto, o valor da notação simbólica **sempre será a negação binária do valor octal**, isto é, os bits de permissão a serem definidos no arquivo recém-criado:

 `$ umask -S`  `u=rwx,g=rx,o=` 

## Definir o valor da máscara

**Nota:** Os valores umask podem ser definidos caso a caso. Por exemplo, os usuários de desktop achar as permissões restritas em sua pasta *home* (`chmod 700`, conforme aplicado por `useradd -m`) suficiente, pois elas tornam todos os arquivos inacessíveis para outros usuários. Isso não seria prático (por exemplo, ao usar o [Apache](/index.php/Apache "Apache")) e os arquivos públicos são armazenados entre os particulares, então, em vez disso, considere restringir o umask.

Você pode definir o valor de umask através do comando *umask*. A string que especifica a máscara de modo segue as mesmas regras sintáticas que o argumento de modo de [chmod](/index.php/Chmod "Chmod") (consulte o [Manual do Programador POSIX](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/chmod.html#tag_20_17_13) para mais detalhes).

O valor de umask do sistema pode ser definido em `/etc/profile` ou nos arquivos de configuração padrão do [shell](/index.php/Shell_(Portugu%C3%AAs) "Shell (Português)"), por exemplo, `/etc/bash.bashrc`. A maioria das distribuições Linux, incluindo o Arch [[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/profile?h=packages/filesystem) definem um valor padrão de `022`. Você também pode configurar umask com `pam_umask.so`, mas este pode ser substituído por `/etc/profile` ou similar.

Se você precisa definir um valor diferente, você pode editar diretamente esse arquivo, afetando todos os usuários, ou executar `umask` a partir do arquivo de configuração do usuário do seu shell (ex.: `~/.bashrc`) para alterar apenas seu umask, porém essas mudanças só terão efeito após o próximo login. Para alterar seu umask apenas durante a sessão atual, basta executar `umask` e digitar o valor desejado. Por exemplo, executar `umask 077` lhe dará permissões de leitura e escrita para novos arquivos e permissões de leitura, escrita e execução para novas pastas.

## Veja também

*   Manual do Programador POSIX:
    *   [umask](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/umask.html) (também disponível como [umask(1p)](http://jlk.fjfi.cvut.cz/arch/manpages/man/umask.1p))
    *   [chmod (descrição estendida)](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/chmod.html#tag_20_17_13) (também disponível como [chmod(1p)](http://jlk.fjfi.cvut.cz/arch/manpages/man/chmod.1p))
*   [wikipedia:pt:umask](https://en.wikipedia.org/wiki/pt:umask "wikipedia:pt:umask")
*   [027 umask: um meio-termo entre segurança e simplicidade](https://blogs.gentoo.org/mgorny/2011/10/18/027-umask-a-compromise-between-security-and-simplicity/)