Artigos relacionados

*   [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")

Esta página é um guia para selecionar e configurar seus espelhos e uma lista dos espelhos disponíveis atualmente.

## Contents

*   [1 Espelhos oficiais](#Espelhos_oficiais)
    *   [1.1 Espelhos prontos para IPv6](#Espelhos_prontos_para_IPv6)
*   [2 Habilitando um espelho específico](#Habilitando_um_espelho_espec.C3.ADfico)
    *   [2.1 Forçar o pacman a renovar as listas de pacotes](#For.C3.A7ar_o_pacman_a_renovar_as_listas_de_pacotes)
*   [3 Ordenando espelhos](#Ordenando_espelhos)
    *   [3.1 Listar por velocidade](#Listar_por_velocidade)
    *   [3.2 Classificação do lado do servidor](#Classifica.C3.A7.C3.A3o_do_lado_do_servidor)
    *   [3.3 Listar espelhos apenas para um país específico](#Listar_espelhos_apenas_para_um_pa.C3.ADs_espec.C3.ADfico)
*   [4 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
*   [5 Espelhos não oficiais](#Espelhos_n.C3.A3o_oficiais)
    *   [5.1 Áustria](#.C3.81ustria)
    *   [5.2 Canadá](#Canad.C3.A1)
    *   [5.3 China](#China)
    *   [5.4 França](#Fran.C3.A7a)
    *   [5.5 Indonésia](#Indon.C3.A9sia)
    *   [5.6 Irã](#Ir.C3.A3)
    *   [5.7 Itália](#It.C3.A1lia)
    *   [5.8 Japão](#Jap.C3.A3o)
    *   [5.9 Malásia](#Mal.C3.A1sia)
    *   [5.10 Holanda](#Holanda)
    *   [5.11 Nova Zelândia](#Nova_Zel.C3.A2ndia)
    *   [5.12 Polônia](#Pol.C3.B4nia)
    *   [5.13 Rússia](#R.C3.BAssia)
    *   [5.14 África do Sul](#.C3.81frica_do_Sul)
    *   [5.15 Suécia](#Su.C3.A9cia)
    *   [5.16 Tailândia](#Tail.C3.A2ndia)
    *   [5.17 Turquia](#Turquia)
    *   [5.18 Estados Unidos](#Estados_Unidos)
    *   [5.19 Sourceforge (ISOs antigas)](#Sourceforge_.28ISOs_antigas.29)

## Espelhos oficiais

A lista de espelhos oficial do Arch Linux está disponível no pacote [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist). Para obter uma lista de espelhos mais atualizada, use a página [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) no site principal.

Verifique o status dos espelhos do Arch visitando a página [Mirror Status](https://www.archlinux.org/mirrors/status/). É recomendável usar apenas espelhos atualizados, ou seja, não fora de sincronia.

Se você quiser que o seu espelho seja adicionado à lista oficial, veja [DeveloperWiki:NewMirrors](/index.php/DeveloperWiki:NewMirrors "DeveloperWiki:NewMirrors"). Enquanto isso, adicione-o à lista [#Espelhos não oficiais](#Espelhos_n.C3.A3o_oficiais) no final desta página.

### Espelhos prontos para IPv6

O [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/?ip_version=6) também pode ser usado para localizar uma lista atual de espelhos IPv6.

## Habilitando um espelho específico

Para habilitar espelhos, edite `/etc/pacman.d/mirrorlist` e localize sua região geográfica. Descomente os espelhos que você gostaria de usar.

Exemplo:

```
# Any
# Server = ftp://mirrors.kernel.org/archlinux/$repo/os/$arch
**Server = http://mirrors.kernel.org/archlinux/$repo/os/$arch**

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
**Server = ftp://ftp.hosteurope.de/mirror/ftp.archlinux.org/core/os/$arch**
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

Passar dois sinalizadores `--refresh` ou `-y` força o pacman a atualizar todas as listas de pacotes, mesmo que sejam consideradas atualizadas. Emitir `pacman -Syyu` *sempre que mudar para um novo espelho* é uma boa prática e evitará possíveis problemas. Veja também [Is -Syy safe?](https://bbs.archlinux.org/viewtopic.php?id=163124) (-Syy é seguro?).

## Ordenando espelhos

Ao baixar os pacotes, o pacman usa os espelhos na ordem em que estão no `/etc/pacman.d/mirrorlist`. Para definir uma prioridade para os espelhos, o arquivo mirrorlist deve ser classificado manualmente ou usando um script.

Não é uma boa ideia usar apenas os espelhos mais rápidos, pois os espelhos mais rápidos podem estar fora de sincronia. Em vez disso, faça uma lista de espelhos classificados por sua [velocidade](#Listar_por_velocidade), depois remova da lista aqueles que estão fora de sincronia conforme seu [status](https://www.archlinux.org/mirrors/status/).

É recomendado repetir esse processo antes de toda atualização de sistema para manter o `/etc/pacman.d/mirrorlist` atualizado.

### Listar por velocidade

O pacote [pacman](https://www.archlinux.org/packages/?name=pacman) fornece um script Bash, `/usr/bin/rankmirrors`, que pode ser usado para classificar os espelhos de acordo com suas velocidades de conexão e abertura para aproveitar o uso do espelho local mais rápido.

Faça um *backup* do `/etc/pacman.d/mirrorlist` existente:

```
# cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup

```

Edite `/etc/pacman.d/mirrorlist.backup` e descomente espelhos para teste com `rankmirrors`.

Opcionalmente, execute a seguinte linha `sed` para descomentar todo os espelhos:

```
# sed -i 's/^#Server/Server/' /etc/pacman.d/mirrorlist.backup

```

Finalmente, classifique os espelhos. O operando `-n 6` significa emitir apenas os 6 espelhos mais rápidos:

```
# rankmirrors -n 6 /etc/pacman.d/mirrorlist.backup > /etc/pacman.d/mirrorlist

```

Execute `rankmirrors -h` para uma lista de todas as opções disponíveis.

### Classificação do lado do servidor

O [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) oficial fornece uma maneira fácil de obter uma lista ordenada de espelhos. Como toda a classificação é feita em um único servidor que leva vários fatores em consideração, a quantidade de carga nos espelhos e nos clientes é significativamente menor em comparação à classificação em cada cliente individual.

Existem vários scripts automatizando a atualização do mirrorlist do servidor de classificação:

*   **[Reflector](/index.php/Reflector "Reflector")** — Obtém o mirrorlist mais recente da página [MirrorStatus](https://www.archlinux.org/mirrors/status/), filtra os espelhos mais atualizados, ordena-os por velocidade e sobrescreve o `/etc/pacman.d/mirrorlist`

	[https://xyne.archlinux.ca/projects/reflector/](https://xyne.archlinux.ca/projects/reflector/) || [reflector](https://www.archlinux.org/packages/?name=reflector).

*   **armrr** — Baixa um mirrorlist classificado para países específicos do [Pacman Mirrorlist Generator](https://www.archlinux.org/mirrorlist/)

	[https://github.com/spurge/armrr](https://github.com/spurge/armrr) || nenhum pacote

### Listar espelhos apenas para um país específico

Pode ser útil para automatizar a atualização da lista de espelhos somente para países específicos, em vez de fazer um teste de velocidade a cada vez. Presumindo que existe `mirrorlist.pacnew`, o arquivo cria após a instalação da atualização [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist).

```
awk '/^## Brazil$/ {f=1} f==0 {next} /^$/ {exit} {print substr($0, 1)}' \
    /etc/pacman.d/mirrorlist.pacnew
```

## Solução de problemas

Na improvável situação de você estar sem espelhos configurados e `pacman-mirrorlist` não instalado, execute o seguinte comando:

```
# curl -o /etc/pacman.d/mirrorlist https://www.archlinux.org/mirrorlist/all/

```

Lembre-se de descomentar um espelho preferencial conforme descrito acima e então:

```
# pacman -Syu pacman-mirrorlist

```

## Espelhos não oficiais

Esses espelhos *não* estão listados no `/etc/pacman.d/mirrorlist`.

### Áustria

*   [http://gd.tuwien.ac.at/opsys/linux/archlinux/](http://gd.tuwien.ac.at/opsys/linux/archlinux/) - *Universidade Técnica de Viena*
*   [ftp://gd.tuwien.ac.at/opsys/linux/archlinux/](ftp://gd.tuwien.ac.at/opsys/linux/archlinux/)

### Canadá

*   [https://na.mirrors.coltondrg.com/archlinux/](https://na.mirrors.coltondrg.com/archlinux/)

### China

**Telecom**

*   [http://mirror.bit.edu.cn/archlinux/](http://mirror.bit.edu.cn/archlinux/) - *Beijing Institute of Technology*
*   [http://mirrors.aliyun.com/archlinux/](http://mirrors.aliyun.com/archlinux/) - *Alibaba*

**Unicom**

*   [http://mirrors.sohu.com/archlinux/](http://mirrors.sohu.com/archlinux/)
*   [http://mirrors.yun-idc.com/archlinux/](http://mirrors.yun-idc.com/archlinux/)

**Cernet**

*   [http://mirrors.geekpie.org/archlinux/](http://mirrors.geekpie.org/archlinux/) - *Geek Pie Association @ ShanghaiTech University*
*   [http://ftp.sjtu.edu.cn/archlinux/](http://ftp.sjtu.edu.cn/archlinux/) - *Shanghai Jiaotong University(Legacy)*
*   [https://mirrors.sjtug.org/archlinux/](https://mirrors.sjtug.org/archlinux/) - *Shanghai Jiaotong University Linux User Group*
*   [http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.4.tuna.tsinghua.edu.cn/archlinux/) *(ipv4 apenas)*
*   [http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/](http://mirrors.6.tuna.tsinghua.edu.cn/archlinux/) *(ipv6 apenas)*
*   [http://mirror.lzu.edu.cn/archlinux/](http://mirror.lzu.edu.cn/archlinux/) - *Lanzhou University*
*   [https://mirrors.nju.edu.cn/archlinux/](https://mirrors.nju.edu.cn/archlinux/) - *Nanjing University*

### França

*   [http://delta.archlinux.fr/](http://delta.archlinux.fr/) - *Com suporte a pacotes Delta. Precisa de [xdelta3](https://www.archlinux.org/packages/?name=xdelta3) para executar.*
*   [https://eu.mirrors.coltondrg.com/archlinux/](https://eu.mirrors.coltondrg.com/archlinux/)
*   [https://mirror.oldsql.cc/archlinux/](https://mirror.oldsql.cc/archlinux/)

### Indonésia

*   [http://kambing.ui.ac.id/archlinux/](http://kambing.ui.ac.id/archlinux/)

### Irã

*   [http://mirror.yazd.ac.ir/arch/](http://mirror.yazd.ac.ir/arch/)
*   [http://repo.sadjad.ac.ir/arch/](http://repo.sadjad.ac.ir/arch/)

### Itália

*   [http://mi.mirror.garr.it/mirrors/archlinux/](http://mi.mirror.garr.it/mirrors/archlinux/)

### Japão

*   [http://ftp.nara.wide.ad.jp/pub/Linux/archlinux/](http://ftp.nara.wide.ad.jp/pub/Linux/archlinux/) - *Nara Institute of Science and Technology*
*   [http://ftp.kddilabs.jp/Linux/packages/archlinux/](http://ftp.kddilabs.jp/Linux/packages/archlinux/)
*   [http://srv2.ftp.ne.jp/Linux/packages/archlinux/](http://srv2.ftp.ne.jp/Linux/packages/archlinux/)
*   [http://mirror.archlinuxjp.org/](http://mirror.archlinuxjp.org/)

### Malásia

*   [http://mirror.oscc.org.my/archlinux/](http://mirror.oscc.org.my/archlinux/)

### Holanda

*   [http://mirror.transip.net/archlinux/](http://mirror.transip.net/archlinux/) *TransIP B.V.*

### Nova Zelândia

*   [http://mirror.ece.auckland.ac.nz/archlinux/](http://mirror.ece.auckland.ac.nz/archlinux/) *NZ apenas*

### Polônia

*   [ftp://ftp.icm.edu.pl/pub/Linux/dist/archlinux/](ftp://ftp.icm.edu.pl/pub/Linux/dist/archlinux/) - ICM UW
*   [http://ftp.icm.edu.pl/pub/Linux/dist/archlinux/](http://ftp.icm.edu.pl/pub/Linux/dist/archlinux/) - ICM UW
*   [https://ftp.icm.edu.pl/pub/Linux/dist/archlinux/](https://ftp.icm.edu.pl/pub/Linux/dist/archlinux/) - ICM UW
*   rsync://ftp.icm.edu.pl/pub/Linux/dist/archlinux/ - ICM UW

### Rússia

*   [http://mirrors.krasinfo.ru/archlinux/](http://mirrors.krasinfo.ru/archlinux/) - *Krasnoyarsk, Classica-Service Ltd*

### África do Sul

*   [http://ftp.leg.uct.ac.za/pub/linux/arch/](http://ftp.leg.uct.ac.za/pub/linux/arch/) - *Universidade da Cidade do Cabo*
*   [ftp://ftp.leg.uct.ac.za/pub/linux/arch/](ftp://ftp.leg.uct.ac.za/pub/linux/arch/)
*   [http://mirror.ufs.ac.za/archlinux/](http://mirror.ufs.ac.za/archlinux/) - *University of the Free State*
*   [ftp://mirror.ufs.ac.za/os/linux/distros/archlinux/](ftp://mirror.ufs.ac.za/os/linux/distros/archlinux/)
*   [http://archlinux.mirror.ac.za](http://archlinux.mirror.ac.za) - *TENET - Tertiary Education and Research Network of South Africa*
*   [ftp://archlinux.mirror.ac.za](ftp://archlinux.mirror.ac.za)

### Suécia

*   [http://foss.dhyrule.se/linux/archlinux/](http://foss.dhyrule.se/linux/archlinux/)
*   [ftp://foss.dhyrule.se/linux/archlinux/](ftp://foss.dhyrule.se/linux/archlinux/)

### Tailândia

*   [http://mirror1.ku.ac.th/archlinux/](http://mirror1.ku.ac.th/archlinux/)

### Turquia

*   [http://mirror.veriteknik.net.tr/archlinux/](http://mirror.veriteknik.net.tr/archlinux/) *- VeriTeknik Data Center*

*   [http://ftp.linux.org.tr/archlinux/](http://ftp.linux.org.tr/archlinux/)

### Estados Unidos

*   [http://mirror.clarkson.edu/archlinux/](http://mirror.clarkson.edu/archlinux/)
*   [http://mirror.pointysoftware.net/archlinux/](http://mirror.pointysoftware.net/archlinux/)
*   [http://mirror.ziemer.bz/archlinux](http://mirror.ziemer.bz/archlinux)
*   [https://lug.mines.edu/mirrors/archlinux/](https://lug.mines.edu/mirrors/archlinux/)
*   [http://mirror.cs.umn.edu/arch/](http://mirror.cs.umn.edu/arch/)

### Sourceforge (ISOs antigas)

*   [http://sourceforge.net/projects/archlinux/files/](http://sourceforge.net/projects/archlinux/files/) - *Arquivos ISO apenas; Não tem nenhum lançamento desde 2006\. Use-o apenas para obter ISOs mais antigas.*