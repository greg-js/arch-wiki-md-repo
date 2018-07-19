O [Wireshark](https://www.wireshark.org/) é um analisador de pacotes livre e de código aberto. Ele é usado para solucionar de problemas de rede, análise, desenvolvimento de software e protocolo de comunicação e educação.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Capturando como um usuário normal](#Capturando_como_um_usu.C3.A1rio_normal)
*   [3 Algumas técnicas de captura](#Algumas_t.C3.A9cnicas_de_captura)
    *   [3.1 Filtrando pacotes TCP](#Filtrando_pacotes_TCP)
    *   [3.2 Filtrando pacotes UDP](#Filtrando_pacotes_UDP)
    *   [3.3 Filtrar pacotes para um endereço IP específico](#Filtrar_pacotes_para_um_endere.C3.A7o_IP_espec.C3.ADfico)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt) para a GUI do Wireshark ou [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) para apenas a CLI `tshark`.

Para a interface GTK+ obsoleta, instale o pacote [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk). Note que esse pacote será removido no futuro (Wireshark 3.0).

## Capturando como um usuário normal

Não execute Wireshark como *root*, é inseguro. O Wireshark implementou a separação de privilégios.[[1]](https://wiki.wireshark.org/CaptureSetup/CapturePrivileges#Most_UNIXes)

O [script de instalação](/index.php/PKGBUILD_(Portugu%C3%AAs)#install "PKGBUILD (Português)") do [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) define as [capacidades](/index.php/Capabilities "Capabilities") de captura de pacotes no executável `/usr/bin/dumpcap`.

`/usr/bin/dumpcap` só pode ser executado como *root* e membros do grupo `wireshark`.

Então, para usar Wireshark como um usuário normal, você só precisa adicionar seu usuário ao [grupo](/index.php/Grupo "Grupo") `wireshark`:

```
 # gpasswd -a *nome-de-usuário* wireshark

```

Faça login novamente para aplicar a alteração. Você pode usar `newgrp wireshark` para abrir um shell com o novo grupo aplicado, mas ele só vai funcionar quando o Wireshark é lançado lá de dentro, até que você faça login novamente.

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