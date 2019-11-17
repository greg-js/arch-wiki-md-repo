**Status de tradução:** Esse artigo é uma tradução de [incron](/index.php/Incron "Incron"). Data da última tradução: 2019-11-10\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Incron&diff=0&oldid=588452) na versão em inglês.

[incron](http://inotify.aiken.cz/?section=incron&page=about&lang=en) é um daemon que monitora [eventos de sistemas de arquivos](/index.php/Inicializa%C3%A7%C3%A3o_autom%C3%A1tica#Em_eventos_de_sistemas_de_arquivos "Inicialização automática") e executa comandos definidos nas tabelas do sistema e do usuário.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Ativação e inicialização automática](#Ativação_e_inicialização_automática)
*   [3 Configuração](#Configuração)
    *   [3.1 Usando incrontab](#Usando_incrontab)
    *   [3.2 Formato de incrontab](#Formato_de_incrontab)
        *   [3.2.1 Tipos de máscaras](#Tipos_de_máscaras)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [incron](https://www.archlinux.org/packages/?name=incron).

## Ativação e inicialização automática

Após a instalação, o daemon não será ativado por padrão. Ele pode ser habilitado usando [systemctl](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)").

## Configuração

Os incrontabs nunca devem ser editados diretamente; em vez disso, os usuários devem usar o programa *incrontab* para trabalhar com seus incrontabs.

### Usando incrontab

Para visualizar seus incrontabs, os usuários devem emitir o comando:

```
$ incrontab -l

```

Para editar suas incrontabs, eles devem usar:

```
$ incrontab -e

```

Para remover as incrontabs, eles podem usar:

```
$ incrontab -r

```

Para recarregar *incrond*, use:

```
$ incrontab -d

```

Para editar a incrontab de outro usuário, execute o seguinte comando como root:

```
$ incrontab -u *usuário*

```

### Formato de incrontab

Cada linha em um arquivo incrontab é uma tabela que o dameon executa quando um evento acontece em um determinado diretório ou arquivo.

O formato básico para um incrontab é:

```
*caminho* *máscara* *comando*

```

*   *caminho* é o diretório ou arquivo que *incrond* vai monitorar por alterações.
*   *máscara* é o tipo de evento de sistema de arquivos que icrond vai monitorar. Esse parâmetro pode ser separado por vígulas.
*   *comando* é o comando a ser executado após ocorrer(em) o(s) evento(s) de sistema de arquivos especificado(s).

#### Tipos de máscaras

O *incrontab* usa tipos de máscara para especificar qual evento do sistema de arquivos monitorar. Para mais opções, consulte [inotify(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/inotify.7)

Para acionar um comando se um arquivo for acessado ou lido:

```
**IN_ACCESS**

```

Para acionar um comando se os metadados de um arquivo forem alterados (por exemplo, *carimbos de data/hora*, *permissões*):

```
**IN_ATTRIB**

```

Para acionar um comando se um arquivo aberto para gravação estiver fechado:

```
**IN_CLOSE_WRITE**

```

Para acionar um comando se um arquivo ou diretório não aberto para gravação estiver fechado:

```
**IN_CLOSE_NOWRITE**

```

Para acionar um comando se um arquivo ou diretório for criado em um diretório monitorado:

```
**IN_CREATE**

```

Para acionar um comando se um arquivo ou diretório for excluído de um diretório monitorado:

```
**IN_DELETE**

```

Para acionar um comando se um arquivo ou diretório monitorado for excluído (ou movido para um sistema de arquivos diferente):

```
**IN_DELETE_SELF**

```

Para acionar um comando se um arquivo foi modificado:

```
**IN_MODIFY**

```

Para acionar um comando se um arquivo ou diretório monitorado for movido dentro do sistema de arquivos:

```
**IN_MOVE_SELF**

```

Para acionar um comando se um arquivo ou diretório for movido para fora do diretório monitorado:

```
**IN_MOVED_FROM**

```

Para acionar um comando se um arquivo ou diretório for movido para o diretório monitorado:

```
**IN_MOVED_TO**

```

Para acionar um comando se um arquivo ou diretório monitorado for aberto:

```
**IN_OPEN**

```