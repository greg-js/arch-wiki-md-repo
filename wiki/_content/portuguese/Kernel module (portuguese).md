**Status de tradução:** Esse artigo é uma tradução de [Kernel module](/index.php/Kernel_module "Kernel module"). Data da última tradução: 2020-01-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Kernel_module&diff=0&oldid=595461) na versão em inglês.

Artigos relacionados

*   [Boot debugging](/index.php/Boot_debugging "Boot debugging")
*   [Kernel](/index.php/Kernel_(Portugu%C3%AAs) "Kernel (Português)")
*   [Parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel")
*   [Compile kernel module](/index.php/Compile_kernel_module "Compile kernel module")

[Módulos de Kernel](https://en.wikipedia.org/wiki/Loadable_kernel_module "wikipedia:Loadable kernel module") são peças de código que podem ser carregadas e descarregadas no kernel de acordo com a demanda. Elas estendem a funcionalidade do kernel sem a necessidade de reinicialização do sistema.

Para criar um módulo de kernel, você pode ler (em inglês) [The Linux Kernel Module Programming Guide](http://tldp.org/LDP/lkmpg/2.6/html/index.html). Um módulo pode ser configurado como para executar de modo embutido ao kernel ou ser carregado separadamente. Para carregar ou remover um módulo dinamicamente, ele deve ser configurado como em mmódulo carregável na configuração do kernel (a linha relacionada ao módulo sexibirá a letra `M`).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Obtendo informações](#Obtendo_informações)
*   [2 Carregamento automático de módulos com systemd](#Carregamento_automático_de_módulos_com_systemd)
*   [3 Manuseio de módulos de kernel](#Manuseio_de_módulos_de_kernel)
*   [4 Opções de configuração de módulos](#Opções_de_configuração_de_módulos)
    *   [4.1 Carregá-lo manualmente usando modprobe](#Carregá-lo_manualmente_usando_modprobe)
    *   [4.2 Usando arquivos em /etc/modprobe.d/](#Usando_arquivos_em_/etc/modprobe.d/)
    *   [4.3 Usando a linha de comando do kernel](#Usando_a_linha_de_comando_do_kernel)
*   [5 Aliasing](#Aliasing)
*   [6 Adicionar um módulo em uma lista negra (Blacklisting)](#Adicionar_um_módulo_em_uma_lista_negra_(Blacklisting))
    *   [6.1 Usando arquivos em /etc/modprobe.d/](#Usando_arquivos_em_/etc/modprobe.d/_2)
    *   [6.2 Usando a linha de comando do kernel](#Usando_a_linha_de_comando_do_kernel_2)
*   [7 Solução de problemas](#Solução_de_problemas)
    *   [7.1 Módulos não podem ser carregados](#Módulos_não_podem_ser_carregados)
*   [8 Veja também](#Veja_também)

## Obtendo informações

Módulos são gravados em `/usr/lib/modules/*versão_do_kernel*`. O comando `uname -r` pode ser usado para obter a atual versão do kernel em execução.

**Nota:** Nomes de módulo costumam usar *underlines* (`_`) ou traços (`-`); entretanto, esses símbolos são permutáveis ao usar o comando `modprobe` e nos arquivos de configuração em `/etc/modprobe.d/`.

Para exibir quais módulos do kernel estão atualmente carregados:

```
$ lsmod

```

Para exibir informação sobre um módulo:

```
$ modinfo *nome_do_modulo*

```

Para listar opções que estão definidas para um módulo carregado:

```
$ systool -v -m *nome_do_modulo*

```

Para mostrar a configuração de modo mais compreensível de todos os módulos:

```
$ modprobe -c | less

```

Para exibir a configuração de um módulo em particular:

```
$ modprobe -c | grep *nome_do_modulo*

```

Listar as dependências de um módulo (ou *alias*), incluindo o módulo em si:

```
$ modprobe --show-depends *nome_do_modulo*

```

## Carregamento automático de módulos com systemd

Hoje, todos os módulos necessários ao funcionamento do sistema são automaticamente gerenciados por [udev](/index.php/Udev "Udev"), então se não houver necessidade de usar quaisquer módulos de kernel adicionais, não há necessidade de acrescentar módulos que deverão ser carregados na inicialização do sistema em qualquer arquivo de configuração. Entretanto, existem casos onde você pode querer adicionar um módulo extra durante o processo de inicialização do sistema, ou acrescentá-lo numa lista negra (blacklist) para que seu computador funcione adequadamente.

Módulos de kernel podem ser explicitamente listados em arquivos dentro de `/etc/modules-load.d/` para que o systemd os carregue durante a inicialização do sistema. Cada arquivo de configuração é nomeado no estilo de `/etc/modules-load.d/<programa>.conf`. Arquivos de configuração simplesmente contém uma lista de módulos de kernel a serem carregados, separados linha a linha. Linhas vazias e linhas cujo primeiro caractere sem espaço em branco seja `#` ou `;` são ignoradas.

 `/etc/modules-load.d/virtio-net.conf` 
```
# Carrega virtio_net.ko na inicialização
virtio_net
```

Veja [modules-load.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/modules-load.d.5) para mais detalhes.

## Manuseio de módulos de kernel

Módulos de kernel são manuseados por ferramentas fornecidas pelo pacote [kmod](https://www.archlinux.org/packages/?name=kmod). Você pode usar essas ferramentas manualmente.

**Nota:** Caso tenha atualizado seu kernel mas ainda não tenha reiniciado o sistema, *modprobe* irá falhar com ou sem mensagem de erro e irá fechar com código 1, porque o caminho `/usr/lib/modules/$(uname -r)/` não existirá mais neste cenário. Verifique manualmente se o caminho existe quando *modprobe* falhar, para determinar se este é o caso.

Para carregar um módulo:

```
# modprobe *nome_do_modulo*

```

Para carregar um módulo pelo seu nome de arquivo (isto é, algum que não esteja instalado em `/usr/lib/modules/$(uname -r)/`):

```
# insmod filename [args]

```

Para descarregar um módulo:

```
# modprobe -r *nome_do_modulo*

```

Ou alternativamente:

```
# rmmod *nome_do_modulo*

```

## Opções de configuração de módulos

Para passar um parâmetro para um módulo de kernel, você passa-o manualmente com modprobe ou assegura certos parâmetros que sempre serão aplicados usando um arquivo de configuração do modprobe, ou ainda usando a linha de comando do kernel.

### Carregá-lo manualmente usando modprobe

A mais básica forma de passar parâmetros para um módulo é através do comando modprobe. Parâmetros são especificados em linha de comando usando simples valores `*key=value*`:

```
# modprobe *nome_do_modulo nome_do_parametro=valor_do_parametro*

```

### Usando arquivos em /etc/modprobe.d/

Arquivos no diretório `/etc/modprobe.d/` podem ser usados para passar configurações do módulo ao [udev](/index.php/Udev "Udev"), o qual usará `modprobe` para gerenciar o carregamento de módulos durante a inicialização do sistema. Arquivos de configuração neste diretório podem ter qualquer nome, desde termine com a extensão `.conf`. A sintaxe é:

 `/etc/modprobe.d/myfilename.conf`  `options *nome_do_modulo nome_do_parametro=valor_do_parametro*` 

Por exemplo:

 `/etc/modprobe.d/thinkfan.conf` 
```
# Em ThinkPads, a daemon 'thinkfan' permite controlar a velocidade da ventoinha
options thinkpad_acpi fan_control=1
```

**Nota:** Se qualquer dos módulos afetados estão carregados pela initramfs, então será necessário adicionar o arquivo `.conf` apropriado a `FILES` em [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") ou usar o [hook](/index.php/Mkinitcpio.conf#HOOKS "Mkinitcpio.conf") `modconf`, para que então ele seja incluído na initramfs. Para ver o conteúdo de uma initramfs padrão, use `lsinitcpio /boot/initramfs-linux.img`.

### Usando a linha de comando do kernel

Se o módulo estiver embutido dentro do kernel, você pode também passar opções ao módulo usando a linha de comando do kernel. Para todos os gerenciadores de boot comuns, a seguinte sintaxe está correta:

```
*nome_do_modulo.nome_do_parametro=valor_do_parametro*

```

Por exemplo:

```
thinkpad_acpi.fan_control=1

```

Simplesmente adicione isto à linha de comando do kernel através do seu gerenciador de boot, como descrito em [Parâmetros do Kernel](/index.php/Kernel_parameters_(Portugu%C3%AAs) "Kernel parameters (Português)").

## Aliasing

*Aliasing* é atribuir apelido (alias) a um módulo de kernel. Por exemplo: `alias my-mod really_long_modulename` significa que você pode usar `modprobe my-mod` ao invés de `modprobe really_long_modulename`. Você pode ainda usar caracteres-curinga no estilo do shell, então `alias my-mod* really_long_modulename` significa que `modprobe my-mod-something` tem o mesmo efeito. Criar um alias:

 `/etc/modprobe.d/myalias.conf`  `alias mymod really_long_module_name` 

Alguns módulos tem aliases que são automaticamente carregadas quando são necessárias por uma aplicação. Desativar estes *aliases* pode evitar que que o módulo seja carregado automaticamente, mas o mesmo ainda poderá ser carregado manualmente.

 `/etc/modprobe.d/modprobe.conf` 
```
# Evita o carregamento automático do Bluetooth
alias net-pf-31 off
```

## Adicionar um módulo em uma lista negra (Blacklisting)

Blacklisting, no contexto de módulos de kernel, é um mecanismo de evitar que módulos de kernel sejam carregados. Isto pode ser útil se, por exemplo, o hardware associado a ele não seja usado, ou se carregar seu módulo cause problemas: por exemplo, pode haver dois módulos de kernel tentando controlar a mesma parte do hardware, e carregá-los juntos resulta em conflito.

Alguns módulos são parte da [initramfs](/index.php/Arch_boot_process_(Portugu%C3%AAs)#initramfs "Arch boot process (Português)"). `mkinitcpio -M` irá mostrar todos os módulos automaticamente detectados: para evitar que initramfs carregue alguns deste módulos, adicione-os a uma lista negra com um arquivo *.conf* dentro de `/etc/modprobe.d` e ela deverá ser adicionada pelo hook `modconf` durante a criação da imagem. Executar `mkinitcpio -v` irá listar todos os módulos puxados por diversos hooks (por exemplo, hook `filesystems`, hook `block`, etc.). Lembre de adicionar este arquivo *.conf* à matriz `FILES` em `/etc/mkinitcpio.conf`, caso você não tenha o hook `modconf` em sua matriz `HOOKS` (por exemplo, se você não usa a configuração padrão), e uma vez que você adicionar estes módulos à lista negra, [recrie a initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") e reinicie o sistema em seguida.

### Usando arquivos em /etc/modprobe.d/

Crie um arquivo `.conf` dentro de `/etc/modprobe.d/` e acrescente uma linha para cada módulo que desejar colocá-lo em lista negra, usando a palavra-chave `blacklist`. Se por exemplo desejar evitar que o módulo `pcspkr` seja carregado:

 `/etc/modprobe.d/nobeep.conf` 
```
# Não carregar o módulo 'pcspkr' durante a inicialização.
blacklist pcspkr
```

**Nota:** O comando `blacklist` irá colocar em lista negra um módulo para que ele não seja carregado automaticamente, mas ainda assim ele poderá ser carregado se outro módulo (que não esteja na lista negra) depender dele ou se for carregado manualmente.

Contudo, há uma solução para este comportamento; o comando `install` instrui modprobe a executar um comando personalizado ao invés de normalmente inserir o módulo no kernel, então é possível forçar o módulo a sempre falhar no seu carregamento, com:

 `/etc/modprobe.d/blacklist.conf` 
```
...
install *nome_do_modulo* /bin/true
...
```
Isto irá efetivamente colocar o módulo em lista negra e qualquer outro que dependa dele.

### Usando a linha de comando do kernel

**Dica:** Isto pode ser muito útil caso um módulo quebrado impossibilite a inicialização do sistema.

Você pode também adicionar módulos à lista negra a partir do gerenciador de boot.

Simplesmente adicione `module_blacklist=modulo1,modulo2,modulo3` para a linha de comando do kernel em seu gerenciador de boot, como descrito em [Parâmetros do Kernel](/index.php/Kernel_parameters_(Portugu%C3%AAs) "Kernel parameters (Português)").

**Nota:** Ao adicionar mais do que um módulo na lista negra, perceba que eles deverão ser separados apenas por vírgulas. Espaços ou qualquer outra coisa além disso irá presumivelmente quebrar a sintaxe.

## Solução de problemas

### Módulos não podem ser carregados

No caso de algum módulo específico não ser carregado e o log de inicialização (acessível com `journalctl -b`) dizer que o módulo está em lista negra (blacklisted), mas o diretório `/etc/modprobe.d/` não exibir uma entrada correspondente, procure em outro diretório-fonte do modprobe `/usr/lib/modprobe.d/` por entradas de *blacklist*.

Um módulo não será carregado se a *string* "vermagic" contida dentro do módulo não corresponder com o valor do kernel em execução. Se houver conhecimento de que tal módulo seja compatível com o kernel em execução, a verificação "vermagic" poderá ser ignorada com `modprobe --force-vermagic`.

**Atenção:** Ignorar verificações de versão poderá causar instabilidade no kernel e o sistema apresentará comportamento inesperado devido à incompatibilidade. Use `--force-vermagic` sempre com extrema cautela.

## Veja também

*   [Disable PC speaker beep](/index.php/Disable_PC_speaker_beep "Disable PC speaker beep")
*   [Writing a WMI driver](https://lwn.net/Articles/391230/) - an LWM introduction