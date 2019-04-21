**Status de tradução:** Esse artigo é uma tradução de [Wireshark](/index.php/Wireshark "Wireshark"). Data da última tradução: 2019-04-17\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Wireshark&diff=0&oldid=570364) na versão em inglês.

O [Wireshark](https://www.wireshark.org/) é um analisador de pacotes livre e de código aberto. Ele é usado para solucionar de problemas de rede, análise, desenvolvimento de software e protocolo de comunicação e educação.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Capturando como um usuário normal](#Capturando_como_um_usuário_normal)
*   [3 Algumas técnicas de captura](#Algumas_técnicas_de_captura)
    *   [3.1 Filtrando pacotes TCP](#Filtrando_pacotes_TCP)
    *   [3.2 Filtrando pacotes UDP](#Filtrando_pacotes_UDP)
    *   [3.3 Filtrar pacotes para um endereço IP específico](#Filtrar_pacotes_para_um_endereço_IP_específico)
    *   [3.4 Excluir pacotes de um endereço IP específico](#Excluir_pacotes_de_um_endereço_IP_específico)
    *   [3.5 Filtrar pacotes para LAN](#Filtrar_pacotes_para_LAN)
    *   [3.6 Filtrar pacotes por porta](#Filtrar_pacotes_por_porta)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt) para a GUI do Wireshark ou [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) para apenas a CLI `tshark`.

**Nota:** A interface GTK+ obsoleta foi removida no Wireshark 3.0.

## Capturando como um usuário normal

Não execute Wireshark como *root*, é inseguro. O Wireshark implementou a separação de privilégios.[[1]](https://wiki.wireshark.org/CaptureSetup/CapturePrivileges#Most_UNIXes)

O [script de instalação](/index.php/PKGBUILD_(Portugu%C3%AAs)#install "PKGBUILD (Português)") do [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) define as [capacidades](/index.php/Capabilities "Capabilities") de captura de pacotes no executável `/usr/bin/dumpcap`.

`/usr/bin/dumpcap` só pode ser executado como *root* e membros do grupo `wireshark`.

Então, para usar Wireshark como um usuário normal, você só precisa adicionar seu usuário ao [grupo de usuários](/index.php/Grupo_de_usu%C3%A1rios "Grupo de usuários") `wireshark`:

```
 # gpasswd -a *nome-de-usuário* wireshark

```

Faça login novamente para aplicar a alteração.

## Algumas técnicas de captura

Existem várias maneiras de capturar exatamente o que você está procurando no Wireshark, aplicando [filtros de captura](https://wiki.wireshark.org/CaptureFilters) ou [filtros de exibição](https://wiki.wireshark.org/DisplayFilters).

**Nota:** Para aprender a sintaxe do filtro de captura, veja o man [pcap-filter(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pcap-filter.7). Para os filtros de exibição, veja o man [wireshark-filter(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wireshark-filter.4).

### Filtrando pacotes TCP

Se quiser ver todos os pacotes TCP atuais, digite `tcp` na barra "Filter" ou na CLI, digite:

```
$ tshark -f "tcp"

```

### Filtrando pacotes UDP

Se quiser ver todos os pacotes UDP atuais, digite `udp` na barra "Filter" ou na CLI, digite:

```
$ tshark -f "udp"

```

### Filtrar pacotes para um endereço IP específico

*   Se você quiser ver todo o tráfego indo para um endereço específico, digite o filtro de exibição `ip.dst == 1.2.3.4`, substituindo `1.2.3.4` pelo endereço IP ao qual o tráfego de saída está sendo enviado.
*   Se você quiser ver todo o tráfego de entrada para um endereço específico, digite o filtro de exibição `ip.src == 1.2.3.4`, substituindo `1.2.3.4` pelo endereço IP ao qual o tráfego de entrada está sendo enviado.
*   Se você quiser ver todo o tráfego de entrada ou saída para um endereço específico, digite o filtro de exibição `ip.addr == 1.2.3.4`, substituindo `1.2.3.4` pelo endereço IP relevante.

### Excluir pacotes de um endereço IP específico

```
ip.addr != 1.2.3.4

```

### Filtrar pacotes para LAN

Para ver apenas tráfego de LAN, nenhum tráfego de internet, execute

```
ip.src==192.168.0.0/16 and ip.dst==192.168.0.0/16

```

### Filtrar pacotes por porta

Veja todo tráfego em 2 portas ou mais:

```
tcp.port==80||tcp.port==3306
tcp.port==80||tcp.port==3306||tcp.port==443

```