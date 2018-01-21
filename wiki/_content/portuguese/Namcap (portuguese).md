Namcap é uma ferramenta para verificar pacotes binários e PKGBUILDs fonte para erros comuns de empacotamento, que também pode ser habilitado automaticamente. Ele foi criado por [Jason Chu](https://www.archlinux.org/people/developer-fellows/#jason).

**Alterações**: O arquivo [NEWS](https://git.archlinux.org/namcap.git/tree/NEWS) no repositório Git contém as alterações em relação versões anteriores de forma concisa.

**Ramo de desenvolvimento**: [https://git.archlinux.org/namcap.git](https://git.archlinux.org/namcap.git)

Para fazer um **relato de erro** ou **requisição de recurso** para o namcap, preencha um relatório na seção *Packages:Extra* do [rastreador de erros](https://bugs.archlinux.org) do Arch Linux e defina a importância conforme o caso. Se você está relatando um erro, por favor forneça exemplos concretos de pacotes nos quais o problema ocorra e lembre-se de inserir o número de versão.

Se você tem um *patch* (corrigindo um erro ou adicionando um novo módulo para o namcap), você pode enviá-lo para a lista de discussão [arch-projects](mailto:arch-projects@archlinux.org). O desenvolvimento do namcap é gerenciado com git, então patches formatados em git são preferíveis.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Como usá-lo](#Como_us.C3.A1-lo)
*   [3 Entendendo a saída](#Entendendo_a_sa.C3.ADda)
*   [4 Tags](#Tags)
    *   [4.1 Links simbólicos](#Links_simb.C3.B3licos)
    *   [4.2 Depedências](#Deped.C3.AAncias)
    *   [4.3 Licenças](#Licen.C3.A7as)
    *   [4.4 Arquivos](#Arquivos)
    *   [4.5 Diversos](#Diversos)
    *   [4.6 PKGBUILDs](#PKGBUILDs)
    *   [4.7 Não lançadas](#N.C3.A3o_lan.C3.A7adas)
*   [5 Fazendo um módulo de namcap](#Fazendo_um_m.C3.B3dulo_de_namcap)
*   [6 Relatórios do namcap](#Relat.C3.B3rios_do_namcap)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [namcap](https://www.archlinux.org/packages/?name=namcap).

## Como usá-lo

Para executar o namcap em um arquivo, sendo *nome_de_arquivo* o `PKGBUILD` ou o nome de um binário `pkg.tar.xz`:

```
$ namcap *nome_de_arquivo*

```

Se você deseja ver mensagens informacionais extras, chame o namcap com a opção `-i`:

```
$ namcap -i *nome_de_arquivo*

```

Para mais informações sobre uso, veja a página man [namcap(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/namcap.1).

## Entendendo a saída

O namcap usa um sistema de **tags** para classificar a saída. Atualmente, as tags são de três tipos, *erros* (denotados por E), *avisos* (denotados por W) e *informativo* (denotado por I). Um erro é importante e deve ser corrigido imediatamente; principalmente se eles referem a segurança insuficiente, falta de licença ou problemas de permissão.

Normalmente, o namcap imprime uma explicação legível por humanos (às vezes com sugestões sobre como solucionar o problema). Se quiser saída que pode ser facilmente analisada por um programa, passe a opção -m (*legível para máquina*) para o namcap (esse recurso está atualmente no ramo de desenvolvimento).

## Tags

### Links simbólicos

*   **symlink-found** (*informacional*) Relata quaisquer **links simbólicos** presentes no pacote.
*   **hardlink-found** (*informacional*) Relata quaisquer **links absolutos** presentes no pacote.
*   **dangling-symlink** (*erro*) Relata ocorrências de links simbólicos que apontam para um arquivo que não está presente no pacote.
*   **dangling-hardlink** (*erro*) Relata ocorrências de links absolutos que apontam para um arquivo que não está presente no pacote.

### Depedências

*   **link-level-dependence** (*informacional*) Informa sobre uma biblioteca à qual um pacote está dinamicamente vinculado.
*   **dependency-is-testing-release** (*aviso*) A dependência do pacote listada está no repositório [testing]. Enquanto os pacotes estão sendo criados para os repositórios oficiais do Arch Linux (core, extra e community), eles **não devem ser compilados** contra pacotes do [testing]. Para os pacotes do [core] e [extra], os pacotes comilados contra [testing] devem ser colocados no repositório [testing].
*   **dependency-covered-by-link-dependence** (*informacional*) Dependência coberta por dependências da dependência de links. Portanto, esta é uma dependência redundante.
*   **dependency-detected-not-included** (*erro*) O arquivo referido tem uma dependência que não está listada no vetor depends. Ignore este erro se a dependência mencionada estiver listada na matriz optdepends.

*   **dependency-already-satisfied** (*aviso*) A dependência já está satisfeita (como a dependência de algum pacote já listado como uma dependência, por exemplo) e, portanto, é redundante. Você pode usar a ferramenta `pactree` de [pacman](https://www.archlinux.org/packages/?name=pacman) para ver a árvore de dependências do seu pacote.
*   **dependency-not-needed** (*aviso*) Essa dependência não é necessária por nenhum arquivo presente no programa (até onde o namcap pode deduzir). Isso ainda não funciona corretamente para scripts (como pacotes Python ou perl); lá, você terá que descobrir as dependências por conta própria.
*   **depends-by-namcap-sight** (*informacional*) Uma lista de dependências de acordo com o namcap.

### Licenças

*   **missing-license** (*erro*) Esse pacote carece de uma licença. Licenças devem ser colocadas no vetor `license=()` do PKGBUILD. Veja os [Padrões de empacotamento do Arch](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch") para mais informações. É **muito importante** corrigir esse erro assim que possível, já que não incluir uma lista uma licença é, em muitos casos, uma violação de copyright.
*   **missing-custom-license-dir** (*erro*) A licença especificada é *custom* (personalizada), mas nenhum diretório de licença foi encontrado sob */usr/share/licenses/*, conforme especificado nas diretrizes de empacotamento.
*   **missing-custom-license-file** (*erro*) A licença especificada é *custom*, mas nenhum arquivo de licença foi localizado em */usr/share/licenses/$pkgname*.
*   **not-a-common-license** (*erro*) A licença especificada **não** é *custom*, mas não está presente no pacote [licenses](https://www.archlinux.org/packages/?name=licenses) (contendo licenças comuns), fornecido na distribuição do Arch Linux.

### Arquivos

Esta seção descreve as tags que se relacionam com permissões incorretas de arquivos ou arquivos que não estão sendo instalados de acordo com as diretrizes do FHS.

*   **script-link-detected** (*informacional*) O arquivo a seguir é um script.
*   **file-in-non-standard-dir** (*aviso*) O arquivo a seguir está em um diretório fora do padrão, conforme definido nas [diretrizes do FHS](http://proton.pathname.com/fhs/pub/fhs-2.3.html). Os diretórios permitidos são: *bin/*, *etc/*, *usr/bin/*, *usr/sbin/*, *usr/lib*, *usr/include/*, *usr/share/*, *opt/*, *lib/*, *sbin/*, *srv/*, *var/lib/*, *var/opt/*, *var/spool/*, *var/lock/*, *var/state/*, *var/run/*, *var/log/*.
*   **elffile-not-in-allowed-dirs** (*erro*) Arquivos ELF devem estar somente nesses diretórios: */lib*, */bin*, */sbin*, */usr/bin*, */usr/sbin*, */lib*, */usr/lib*, */opt/$pkgname/*.
*   **empty-directory** (*aviso*) O diretório a seguir no pacote está vazio.
*   **non-fhs-man-page** (*erro*) O pacote instala páginas de manual em uma localização diferente de */usr/share/man*, que é o diretório para páginas de manual conforme as [diretrizes do FHS](http://www.pathname.com/fhs/pub/fhs-2.3.html#USRSHAREMANMANUALPAGES).
*   **potential-non-fhs-man-page** (*aviso*) Esse arquivo parece ser uma página de manual que não está instalada em */usr/share/man*, mas o namcap não tem certeza disso.
*   **non-fhs-info-page** (*erro*) O pacote instala páginas info em em uma localização diferente de */usr/share/info*, que é onde dados independentes de arquitetura devem ser instalados, conforme as [diretrizes do FHS](http://www.pathname.com/fhs/pub/fhs-2.3.html#USRSHAREARCHITECTUREINDEPENDENTDATA)
*   **potential-non-fhs-info-page** (*aviso*) Esse arquivo parece ser uma página info que não está instalada em */usr/share/info*, mas o namcap não tem certeza sobre isso.
*   **incorrect-permissions** (*erro*) Esse arquivo possui dono incorreto. O dono dos arquivos em pacotes binários deve ser `root/root`.
*   **file-not-world-readable** (*aviso*) O arquivo não é legível por todos; geralmente, isso não é o desejado.
*   **file-world-writable** (*aviso*) Qualquer pessoa pode escrever nesse arquivo; novamente, não é um caso comum.
*   **directory-not-world-executable** (*aviso*) O diretório não tem o bit de executável por todos definido. Isso impede o acesso ao diretório para programas que estejam sob privilégios de usuário.
*   **incorrect-library-permissions** (*aviso*) O arquivo de biblioteca estática (.a) não tem permissão 644 (legível e gravável pelo root, legível por qualquer pessoa).
*   **libtool-file-present** (*aviso*) Esse arquivo é um arquivo libtool (.la) e normalmente não deve estar presente. Pode-se usar a opção `!libtool` no vetor *options* do PKGBUILD para remover esses arquivos automaticamente.
*   **perllocal-pod-present** (*erro*) O arquivo perllocal.pod não deve estar presente em um pacote perl; veja as [diretrizes de pacote Perl](/index.php/Perl_package_guidelines "Perl package guidelines") para mais informações.
*   **scrollkeeper-dir-exists** (*erro*) Um diretório scrollkeeper foi localizado no pacote. scrollkeeper não deve ser executado até pós-{instalação,atualização,remoção}.
*   **info-dir-file-present** (*erro*) O arquivo de diretório info */usr/share/info/dir* estava presente no pacote. Esse arquivo não deve estar presente.
*   **gnome-mime-file** (*erro*) O arquivo é um arquivo MIME autogerado do GNOME e não deveria estar presente no pacote.

### Diversos

*   **insecure-rpath** (*erro*) Um RPATH (para um executável) está fora de */usr/lib*. Um RPATH para uma localização insegura é um risco de segurança em potencial. Veja [FS#14049](https://bugs.archlinux.org/task/14049) para uma discussão sobre isso.

### PKGBUILDs

Essas são tags relacionadas aos PKGBUILDs. Algumas dessas podem também se aplicar a pacotes binários.

*   **variable-not-array** (*aviso*) A variável deve ser um vetor de bash em vez de uma string. Essas são as variáveis que devem ser escritas em vetores: *arch*, *license*, *depends*, *makedepends*, *optdepends*, *provides*, *conflicts*, *replaces*, *backup*, *source*, *noextract*, *md5sums*
*   **backups-preceding-slashes** (*erro*) O arquivo mencionado no vetor backup inicia com uma barra ('/').
*   **package-name-in-uppercase** (*erro*) Não deve haver letras maiúsculas em nomes de pacotes.
*   **specific-host-type-used** (*aviso*) Em vez de usar um tipo de host específico (como i686 ou x86_64) use a variável genérica $CARCH variable.
*   **extra-var-begins-without-underscore** (*aviso*) A variável não é uma da variáveis padrões definidas no manual do PKGBUILD e, mesmo assim, não inicia com sublinhado.
*   **file-referred-in-startdir** (*erro*) Um arquivo foi referenciado em *$startdir* fora de *$startdir/pkg* e *$startdir/src*.
*   **missing-md5sums** (*erro*) MD5sums correspondentes aos arquivos fonte estão faltando. Esses podem ser adicionados ao PKGBUILD usando `updpkgsums`.
*   **not-enough-md5sums** (*erro*) Há mais arquivos fontes do que MD5sums fornecidos no PKGBUILD.
*   **too-many-md5sums** (*erro*) Há mais MD5sums do que arquivos fontes no PKGBUILD.
*   **improper-md5sum** (*erro*) Um MD5sum impróprio foi localizado. MD5sums são de 32 caracteres de tamanho.
*   **specific-sourceforge-mirror** (*aviso*) O PKGBUILD usa um espelho específico de servidor do sourceforge. [http://downloads.sourceforge.net](http://downloads.sourceforge.net) deve ser usado.
*   **using-dl-sourceforge** (*aviso*) O domínio obsoleto [http://dl.sourceforge.net](http://dl.sourceforge.net) está sendo usado no vetor fonte. [http://downloads.sourceforge.net](http://downloads.sourceforge.net) deve ser usado.
*   **missing-contributor** (*aviso*) A tag *contributor* está faltando.
*   **missing-maintainer** (*aviso*) A tag *maintainer* está faltando.
*   **missing-url** (*erro*) O pacote não tem uma página web de *upstream* definida. Use a variável `url` para isso.
*   **pkgname-in-description** (*aviso*) A descrição não deve conter o nome do pacote.
*   **recommend-use-pkgdir** (*informacional*) *$startdir/pkg* está obsoleto, use *$pkgdir*.
*   **recommend-use-srcdir** (*informacional*) *$startdir/src* está obsoleto, use *$srcdir*.

### Não lançadas

Não há novas tags na versão de desenvolvimento.

## Fazendo um módulo de namcap

Esta seção documenta as partes internas do namcap e especifica como criar um novo módulo namcap.

O programa principal do namcap, o namcap.py, toma como parâmetros o nome de arquivo de um pacote ou um PKGBUILD e faz um objeto pkginfo, o qual ele passa para uma lista de regras definidas em `__tarball__` e `__pkgbuild__`.

*   *__tarball__* define as regras que processam os pacotes binários.
*   *__pkgbuild__* define as regras que processam os PKGBUILDs

Uma vez que seu módulo esteja finalizado, lembre-se de adicioná-lo para o vetor apropriado (*__tarball__* ou *__pkgbuild__*) definido em *Namcap/__init__.py*

Um exemplo de módulo de namcap é assim:

 `namcap/url.py` 
```
  import pacman

  class package:
  	def short_name(self):
		return "url"
	def long_name(self):
		return "Verifies url is included in a PKGBUILD"
	def prereq(self):
		return ""
	def analyze(self, pkginfo, tar):
		ret = [[],[],[]]
		if not hasattr(pkginfo, 'url'):
			ret[0].append(("missing-url", ()))
		return ret
	def type(self):
		return "pkgbuild"

```

Em sua maioria, o código é autoexplicatório. A seguir segue a lista de métodos que cada módulo do namcap deve ter:

*   **short_name**(self) Retorna uma string contendo um nome curto do módulo. Geralmente, isso é o mesmo que o nome base do arquivo do módulo.
*   **long_name**(self) Retorna uma string contendo uma descrição concisa do módulo. Essa descrição é usada ao listar todas as regras usando `namcap -r list`.
*   **prereq**(self) Retorna uma string contendo os pré-requisitos necessários para o módulo funcionar corretamente. Geralmente "" para módulos processando PKGBUILDs e "tar" por módulos processando arquivos de pacote. "extract" deve ser especificado se o conteúdo do pacote deve ser extraído para um diretório temporário antes de processamento adicional.
*   **analyze**(self, pkginfo, tar) Deve retornar uma lista que inclua, por sua vez, três listas: de tags de erro, tags de aviso e tags de informações, respectivamente. Cada membro dessas listas de tags deve ser uma tupla consistindo de dois componentes: **a forma curta e hifenizada** da tag com os especificadores de formato apropriado (%s, etc). A primeira palavra desta string deve ser o nome da tag. A forma legível por humanos desta tag deve ser coloca no arquivo de tags. O formato do arquivo de tags é descrito abaixo; e **os parâmetros** que devem substituir os tokens especificadores de formato na saída final.
*   **type**(self) "pkgbuild" para um módulos processando PKGBUILDs, "tarball" para um módulo processando um arquivo de pacote binário.

O arquivo de tags consiste de linhas especificando a forma legível por humanos das tags hifenizadas usadas no código do namcap. Uma linha começando com um '#' é tratada como um comentário. Do contrário, o formato do arquivo é:

```
 machine-parseable-tag %s :: This is machine parseable tag %s

```

Note que uma dupla de caracteres de dois pontos (::) é usada para separar a tag hifenizada da descrição legível por humanos.

## Relatórios do namcap

**namcap-reports** é um relatório gerado automaticamente obtido após executar o namcap nas árvores dos repositórios core, extra e community.

Como ele funciona:

*   O namcap é executado em toda árvore do [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)") para criar `namcap.log`.
*   Os pacotes nos repositórios core, extra e community são colocados em arquivos com nomes core, extra e community, respectivamente (usando `pacman -Slq`).
*   `namcap-report.py` leva o código e prepara o relatório e feeds RSS, que é então copiado para o servidor web.