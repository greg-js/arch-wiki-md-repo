**Status de tradução:** Esse artigo é uma tradução de [Mirrors](/index.php/Mirrors "Mirrors"). Data da última tradução: 2019-06-30\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Mirrors&diff=0&oldid=576138) na versão em inglês.

Artigos relacionados

*   [Espelhos não oficiais](/index.php/Espelhos_n%C3%A3o_oficiais "Espelhos não oficiais")
*   [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")

Esta página é um guia para selecionar e configurar seus espelhos e uma lista dos espelhos disponíveis atualmente.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Espelhos oficiais](#Espelhos_oficiais)
    *   [1.1 Espelhos prontos para IPv6](#Espelhos_prontos_para_IPv6)
*   [2 Habilitando um espelho específico](#Habilitando_um_espelho_específico)
    *   [2.1 Forçar o pacman a renovar as listas de pacotes](#Forçar_o_pacman_a_renovar_as_listas_de_pacotes)
*   [3 Ordenando espelhos](#Ordenando_espelhos)
    *   [3.1 Listar por velocidade](#Listar_por_velocidade)
        *   [3.1.1 Classificando uma lista de espelhos existente](#Classificando_uma_lista_de_espelhos_existente)
        *   [3.1.2 Obtendo e classificando uma lista de espelho live](#Obtendo_e_classificando_uma_lista_de_espelho_live)
    *   [3.2 Classificação do lado do servidor](#Classificação_do_lado_do_servidor)
*   [4 Solução de problemas](#Solução_de_problemas)
*   [5 Veja também](#Veja_também)

## Espelhos oficiais

A lista de espelhos oficial do Arch Linux está disponível no pacote [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist). Para obter uma lista de espelhos mais atualizada, use a página [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) no site principal.

Verifique o status dos espelhos do Arch visitando a página [Mirror Status](https://www.archlinux.org/mirrors/status/). É recomendável usar apenas espelhos atualizados, ou seja, não fora de sincronia.

Se você quiser que o seu espelho seja adicionado à lista oficial, veja [DeveloperWiki:NewMirrors](/index.php/DeveloperWiki:NewMirrors "DeveloperWiki:NewMirrors"). Enquanto isso, adicione-o ao artigo [Espelhos não oficiais](/index.php/Espelhos_n%C3%A3o_oficiais "Espelhos não oficiais").

### Espelhos prontos para IPv6

O [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/?ip_version=6) também pode ser usado para localizar uma lista atual de espelhos IPv6.

## Habilitando um espelho específico

Para habilitar espelhos, edite `/etc/pacman.d/mirrorlist` e localize sua região geográfica. Descomente os espelhos que você gostaria de usar.

Exemplo:

```
# Any
# Server = http://mirrors.kernel.org/archlinux/$repo/os/$arch
**Server = https://mirrors.kernel.org/archlinux/$repo/os/$arch**

```

Veja [#Ordenando espelhos](#Ordenando_espelhos) para ferramentas que ajudam a escolher espelhos.

**Dica:**

*   Descomente 5 espelhos favoritos e coloque-os no topo do arquivo mirrorlist. Dessa forma, é fácil encontrá-los e movê-los se o primeiro espelho da lista tiver problemas. Também facilita a atualização de atualizações de lista espelhada.
*   Os espelhos HTTP são mais rápidos que o FTP devido a [conexão HTTP persistente](https://en.wikipedia.org/wiki/HTTP_persistent_connection "wikipedia:HTTP persistent connection"): com o FTP, uma nova conexão ao servidor deve ser estabelecida toda vez que *pacman* solicita o download de um pacote, em uma breve pausa.

Também é possível especificar espelhos em `/etc/pacman.conf`. Para o repositório *[core]*, a configuração padrão é:

```
[core]
Include = /etc/pacman.d/mirrorlist

```

Para usar o espelho *HostEurope* como espelho padrão, adicione-o antes da linha `Include`:

```
[core]
**Server = http://ftp.hosteurope.de/mirror/ftp.archlinux.org/core/os/$arch**
Include = /etc/pacman.d/mirrorlist

```

O pacman agora tentará se conectar a esse espelho primeiro. Prossiga para fazer o mesmo para *[testing]* , *[extra]* e *[community]*, se aplicável.

**Nota:** Se os espelhos foram declarados diretamente em `pacman.conf`, lembre-se de usar o mesmo espelho para todos os repositórios. Caso contrário, pacotes que são incompatíveis entre si podem ser instalados, como o linux de *[core]* e um módulo de kernel antigo de *[extra]*.

### Forçar o pacman a renovar as listas de pacotes

Os espelhos podem estar fora de sincronia e a lista de pacotes do espelho antigo pode não corresponder à lista de pacotes do novo espelho, mesmo que as datas das listas possam sugerir isso.

Após criar/editar o `/etc/pacman.d/mirrorlist`, execute o seguinte comando:

```
# pacman -Syyu

```

Passar dois sinalizadores `--refresh`/`-y` força o pacman a atualizar todas as listas de pacotes, mesmo que sejam consideradas atualizadas. Emitir `pacman -Syyu` é um gasto desnecessário de largura de banda na maioria dos casos, mas algumas vezes pode corrigir problemas ao trocar entre um espelho defeituoso para um funcional. Veja também [Is -Syy safe?](https://bbs.archlinux.org/viewtopic.php?id=163124) (-Syy é seguro?).

**Atenção:** Na maioria dos casos, se você forçar a atualização do banco de dados do pacman, será necessário forçar o downgrade de qualquer pacote potencialmente novo demais para corresponder às versões oferecidas pelo novo espelho. Isso evita problemas nos quais os pacotes são atualizados de forma inconsistente, levando a uma atualização parcial.
```
# pacman -Syyuu

```

Isso não é necessário ao usar carimbos de hora *(timestamps)* para garantir que os espelhos apenas estejam atualizados.

## Ordenando espelhos

Ao baixar os pacotes, o pacman usa os espelhos na ordem em que estão listados no `/etc/pacman.d/mirrorlist`. A ordem que os servidores aparecem na lista define sua prioridade.

Não é ideal classificar apenas com base nos espelhos na velocidade, pois os servidores mais rápidos podem estar fora de sincronia. Em vez disso, faça uma lista de espelhos classificados por sua [velocidade](#Listar_por_velocidade), depois remova da lista aqueles que estão fora de sincronia conforme seu [status](https://www.archlinux.org/mirrors/status/).

É recomendado repetir esse processo antes de toda atualização de sistema para manter a lista de espelhos atualizada.

### Listar por velocidade

#### Classificando uma lista de espelhos existente

O pacote [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) fornece um script Bash, `/usr/bin/rankmirrors`, que pode ser usado para classificar os espelhos de acordo com suas velocidades de conexão e abertura para aproveitar o uso do espelho local mais rápido.

Faça um *backup* do `/etc/pacman.d/mirrorlist` existente:

```
# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup

```

Para preparar `mirrorlist.backup` para classificar com *rankmirrors*, as seguintes ações podem ser executadas:

Edite `mirrorlist.backup` e descomente os servidores a serem testados

*   Se os servidores no arquivo estiverem agrupados por país, pode-se extrair os servidores de um país específico por uso: `$ awk '/^## *Nome do país*$/{f=1}f==0{next}/^$/{exit}{print substr($0, 2)}' /etc/pacman.d/mirrorlist.backup` 

*   Para descomentar todo o espelho, execute a seguinte linha `sed`: `# sed -i 's/^#Server/Server/' /etc/pacman.d/mirrorlist.backup` 

Finalmente, classifique os espelhos, aqui com o operando `-n 6` para emitir apenas os 6 espelhos mais rápidos:

```
# rankmirrors -n 6 /etc/pacman.d/mirrorlist.backup > /etc/pacman.d/mirrorlist

```

#### Obtendo e classificando uma lista de espelho live

Para iniciar com uma lista curta de espelhos atualizados baseada em alguns países e fornecê-la ao *rankmirrors*, pode-se obter a lista do *Pacman Mirrorlist Generator*. O comando abaixo pega os espelhos atualizados na *França* ou no *Reino Unido*, que possuem suporte ao protocolo *https*, ele descomenta os servidores na lista e então os classifica e retorna os 5 mais rápidos.

```
$ curl -s "[https://www.archlinux.org/mirrorlist/?country=FR&country=GB&protocol=https&use_mirror_status=on](https://www.archlinux.org/mirrorlist/?country=FR&country=GB&protocol=https&use_mirror_status=on)" | sed -e 's/^#Server/Server/' -e '/^#/d' | rankmirrors -n 5 -

```

**Dica:** Esse procedimento pode ser feito interativamente navegando para `[https://www.archlinux.org/mirrorlist](https://www.archlinux.org/mirrorlist)` com qualquer navegador baseado em texto como, por exemplo, o [elinks(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/elinks.1).

### Classificação do lado do servidor

O [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) oficial fornece uma maneira fácil de obter uma lista ordenada de espelhos. Como toda a classificação é feita em um único servidor que leva vários fatores em consideração, a quantidade de carga nos espelhos e nos clientes é significativamente menor em comparação à classificação em cada cliente individual.

Outra alternativa popular é a ferramenta a seguir:

**[Reflector](/index.php/Reflector "Reflector")** — Obtém o último mirrorlist da página [MirrorStatus](https://www.archlinux.org/mirrors/status/), filtra e ordena-os por velocidade e sobrescreve `/etc/pacman.d/mirrorlist`

	[https://xyne.archlinux.ca/projects/reflector/](https://xyne.archlinux.ca/projects/reflector/) || [reflector](https://www.archlinux.org/packages/?name=reflector)

## Solução de problemas

Se você encontrar o seguinte erro:

```
erro: arquivo de configuração /etc/pacman.d/mirrorlist não pôde ser lido: Arquivo ou diretório inexistente

```

Obtenha o mirrorlist do site:

```
# curl -o /etc/pacman.d/mirrorlist https://www.archlinux.org/mirrorlist/all/

```

Lembre-se de descomentar um espelho preferencial conforme descrito acima e então:

```
# pacman -Syu pacman-mirrorlist

```

## Veja também

*   [mirrorlist.py no GitHub do archweb](https://github.com/archlinux/archweb/blob/master/mirrors/views/mirrorlist.py) - código fonte do gerador de mirrorlist do archweb