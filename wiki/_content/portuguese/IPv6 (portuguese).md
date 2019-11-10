**Status de tradução:** Esse artigo é uma tradução de [IPv6](/index.php/IPv6 "IPv6"). Data da última tradução: 2019-11-06\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=IPv6&diff=0&oldid=587192) na versão em inglês.

Artigos relacionados

*   [Configuração de tunnel broker IPv6](/index.php/Configura%C3%A7%C3%A3o_de_tunnel_broker_IPv6 "Configuração de tunnel broker IPv6")

No Arch Linux, IPv6 está habilitado por padrão.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Descoberta de vizinhança](#Descoberta_de_vizinhança)
*   [2 Autoconfiguração sem estado (SLAAC)](#Autoconfiguração_sem_estado_(SLAAC))
    *   [2.1 Para clientes](#Para_clientes)
    *   [2.2 Para gateways](#Para_gateways)
*   [3 Extensões de privacidade](#Extensões_de_privacidade)
    *   [3.1 dhcpcd](#dhcpcd)
    *   [3.2 NetworkManager](#NetworkManager)
    *   [3.3 systemd-networkd](#systemd-networkd)
    *   [3.4 connman](#connman)
*   [4 Endereços privados estáveis](#Endereços_privados_estáveis)
    *   [4.1 NetworkManager](#NetworkManager_2)
*   [5 Endereço estático](#Endereço_estático)
*   [6 IPv6 e PPPoE](#IPv6_e_PPPoE)
*   [7 Delegação de prefixo (DHCPv6-PD)](#Delegação_de_prefixo_(DHCPv6-PD))
    *   [7.1 Com dibbler](#Com_dibbler)
    *   [7.2 Com dhcpcd](#Com_dhcpcd)
    *   [7.3 Com WIDE-DHCPv6](#Com_WIDE-DHCPv6)
    *   [7.4 systemd-networkd](#systemd-networkd_2)
    *   [7.5 Outros clientes](#Outros_clientes)
*   [8 Desabilitar IPv6](#Desabilitar_IPv6)
    *   [8.1 Desabilitar funcionalidade](#Desabilitar_funcionalidade)
    *   [8.2 Outros programas](#Outros_programas)
        *   [8.2.1 dhcpcd](#dhcpcd_2)
        *   [8.2.2 NetworkManager](#NetworkManager_3)
        *   [8.2.3 ntpd](#ntpd)
    *   [8.3 systemd-networkd](#systemd-networkd_3)
*   [9 Preferir IPv4 a IPv6](#Preferir_IPv4_a_IPv6)
*   [10 Veja também](#Veja_também)

## Descoberta de vizinhança

Pingar o endereço multicast `ff02::1` resulta em todos os hosts no escopo link-local responderem. Uma interface tem que ser especificada:

```
$ ping ff02::1%eth0

```

Após isso, você pode obter uma lista de todos os vizinhos na rede local com:

```
$ ip -6 neigh

```

Com um ping para o endereço multicast `ff02::2` apenas roteadores vão responderem.

Se você adicionar uma opção `-I *seu-ipv6-global*`, hosts link-local vão responder com seus endereços de escopo link-global. A interface pode ser omitida neste caso:

```
$ ping -I 2001:4f8:fff6::21 ff02::1

```

## Autoconfiguração sem estado (SLAAC)

A maneira mais fácil de adquirir um endereço IPv6, desde que sua rede esteja configurada, é através de *Stateless address autoconfiguration* (abreviado para SLAAC, que poderia ser traduzido para português como "Autoconfiguração de endereço sem estado"). O endereço é inferido automaticamente do prefixo que o seu roteador anuncia e não requer nenhuma configuração adicional nem software especializado, como um cliente DHCP.

### Para clientes

Se você está usando o [netctl](/index.php/Netctl "Netctl"), você só precisa adicionar a seguinte linha para sua configuração Ethernet ou sem fio.

```
IP6=stateless

```

Se você está usando o [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)"), então endereços IP são habilitados automaticamente se houver anúncios para eles na rede.

Observe que a autoconfiguração sem estado funciona com a condição de que pacotes icmp IPv6 sejam permitidos em toda a rede. Portanto, para o lado do cliente, os pacotes `ipv6-icmp` devem ser aceitos. Se você estiver usando um [Firewall stateful simples](/index.php/Simple_stateful_firewall "Simple stateful firewall") ou o [iptables](/index.php/Iptables "Iptables"), você só precisa adicionar:

```
-A INPUT -p ipv6-icmp -j ACCEPT

```

Se você estiver usando um outro front-end de firewall (ufw, shorewall, etc), consulte sua documentação sobre como habilitar os pacotes `ipv6-icmp`.

Se a sua solução de gerenciamento de rede escolhida não ter suporte a configuração do resolvedor DNS com IPv6 sem estado (por exemplo, netctl), será possível usar [rdnssd(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/rdnssd.8) do pacote [ndisc6](https://www.archlinux.org/packages/?name=ndisc6) para isso.

### Para gateways

Para distribuir corretamente os IPv6s aos clientes da rede, precisaremos usar um daemon de anúncio. A ferramenta padrão para este trabalho é [radvd](https://www.archlinux.org/packages/?name=radvd) e está disponível em [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"). Configuração do radvd é bastante simples. Edite `/etc/radvd.conf` para incluir:

```
# substitua LAN com sua interface de LAN
interface LAN {
  AdvSendAdvert on;
  MinRtrAdvInterval 3;
  MaxRtrAdvInterval 10;
  prefix ::/64 {
    AdvOnLink on;
    AdvAutonomous on;
    AdvRouterAddr on;
  };
};

```

A configuração acima dirá aos clientes para se autoconfigurarem usando endereços do bloco /64 anunciado. Observe que a configuração acima anuncia "todos os prefixos disponíveis" atribuídos à interface de LAN. Se você quiser limitar os prefixos anunciados em vez de `::/64` use o prefixo desejado, por exemplo, `2001:DB8::/64`. O bloco `prefix` pode ser repetido várias vezes para mais prefixos.

Para anunciar servidores DNS para seus clientes LAN, você pode usar o recurso RDNSS. Por exemplo, adicione as seguintes linhas a `/etc/radvd.conf` para anunciar os servidores DNS v6 do Google:

```
RDNSS 2001:4860:4860::8888 2001:4860:4860::8844 {
};

```

O gateway também deve permitir o tráfego de pacotes `ipv6-icmp` em todas as cadeias básicas. Para um [Firewall stateful simples](/index.php/Simple_stateful_firewall "Simple stateful firewall") ou o [iptables](/index.php/Iptables "Iptables"), adicione:

```
-A INPUT -p ipv6-icmp -j ACCEPT
-A OUTPUT -p ipv6-icmp -j ACCEPT
-A FORWARD -p ipv6-icmp -j ACCEPT

```

Ajuste de acordo com outros front-ends de firewall e não se esqueça de habilitar `radvd.service`.

## Extensões de privacidade

Quando um cliente adquire um endereço através do SLAAC, seu endereço IPv6 é derivado do prefixo anunciado e do endereço MAC da interface de rede do cliente. Isso pode aumentar as preocupações de segurança, pois o endereço MAC do computador pode ser facilmente derivado pelo endereço IPv6\. Para resolver este problema, o padrão *IPv6 Privacy Extensions* ([RFC 4941](https://tools.ietf.org/html/rfc4941)) foi desenvolvido. Com as extensões de privacidade, o kernel gera um endereço *temporário* que é destacado do endereço original configurado automaticamente. Os endereços privados são preferidos ao se conectar a um servidor remoto, portanto, o endereço original fica oculto. Para ativar as extensões de privacidade, reproduza as seguintes etapas:

Adicione essas linhas a `/etc/sysctl.d/40-ipv6.conf`:

```
# Habilita IPv6 Privacy Extensions
net.ipv6.conf.all.use_tempaddr = 2
net.ipv6.conf.default.use_tempaddr = 2
net.ipv6.conf.*nic0*.use_tempaddr = 2
...
net.ipv6.conf.*nicN*.use_tempaddr = 2

```

Sendo que `nic0` a `nicN` são suas placas de rede (***N**etwork **I**nterface **C**ards*). Você pode encontrar seus nomes usando as instruções em [Configuração de rede#Listando interfaces de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede#Listando_interfaces_de_rede "Configuração de rede"). Os parâmetros `all.use_tempaddr` ou `default.use_tempaddr` não são aplicados nas *NIC*s que já existem quando as configurações de [sysctl](/index.php/Sysctl "Sysctl") são executadas.

Após uma reinicialização, no final, Privacy Extensions devem estar habilitadas.

### dhcpcd

[dhcpcd](/index.php/Dhcpcd "Dhcpcd") inclui em seu arquivo de configuração padrão desde a versão 6.4.0 a opção `slaac private`, que ativa "Endereços IPv6 privados estáveis ao invés de baseados em hardware", implementando [RFC 7217](https://tools.ietf.org/html/rfc7217) ([commit](http://roy.marples.name/projects/dhcpcd/info/8aa9dab00dc72c453aeccbde885ecce27a3d81ff)). Portanto, não é necessário alterar nada, exceto se for desejado alterar o endereço IPv6 com mais frequência do que a cada vez que o sistema for conectado a uma nova rede. Defina para `slaac hwaddr` para um endereço estável.

### NetworkManager

NetworkManager não honra as configurações colocadas em `/etc/sysctl.d/40-ipv6.conf`. Isso pode ser verificado executando `$ ip -6 addr show *interface*` após reiniciar: nenhum endereço `scope global **temporary**` aparece além do regular.

Para habilitar IPv6 Privacy Extensions por padrão, adicione essas linhas a `/etc/NetworkManager/NetworkManager.conf`

 `/etc/NetworkManager/NetworkManager.conf` 
```
...
**[connection]**
**ipv6.ip6-privacy=2**
```

Para habilitar as IPv6 Privacy Extensions para conexões gerenciadas pelo NetworkManager, edite o arquivo de conexão desejado em `/etc/NetworkManager/system-connections/` e acrescente à sua seção `[ipv6]` o par de valores-chave `ip6-privacy=2`:

 `/etc/NetworkManager/system-connections/*conexao-exemplo*` 
```
...
[ipv6]
method=auto
**ip6-privacy=2**
```

**Nota:** Embora possa parecer que o endereço IPv6 `scope global temporary` criado ao ativar as Privacy Extensions nunca é renovado (nunca muda para o status `deprecated` no termo de sua vida útil `valid_lft`), deve ser verificado durante um período de tempo mais longo que esse endereço **realmente** muda.

### systemd-networkd

Systemd-networkd também não honra as configurações `net.ipv6.conf.xxx.use_tempaddr` colocadas em `/etc/sysctl.d/40-ipv6.conf` a menos que a opção `IPv6PrivacyExtensions` esteja definida com o valor `kernel` no(s) arquivo(s) .network.

Outras opções para as IPv6 Privacy Extensions como:

```
net.ipv6.conf.xxx.temp_prefered_lft
net.ipv6.conf.xxx.temp_valid_lft

```

são honradas.

**Nota:** `temp_prefered_lft` é o nome da variável, *preferred* tem que ser escrito errado mesmo.

Veja [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") e [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5) para detalhes.

### connman

Adicione a `/var/lib/connman/settings` sob a seção global:

```
[global]
IPv6.privacy=preferred

```

## Endereços privados estáveis

Outra opção é um endereço IP privado estável ([RFC 7217](https://tools.ietf.org/html/rfc7217)). Isso permite que os IPs sejam estáveis dentro de uma rede sem expor o endereço MAC da interface.

Para que o kernel gere uma chave (por `wlan0`, por exemplo) podemos definir:

```
sysctl net.ipv6.conf.wlan0.addr_gen_mode=3

```

Desative a interface e ative-a novamente e você deverá ver `stable-privacy` ao lado de cada endereço IPv6 depois de executar `ip addr show dev wlan0`. O kernel gerou um segredo de 128 bits para gerar endereços IP para esta interface, para vê-lo rodar `sysctl net.ipv6.conf.wlan0.stable_secret`. Vamos persistir esse valor, então adicione as seguintes linhas ao `/etc/sysctl.d/40-ipv6.conf`:

```
# Habilita modo de privacidade estável de IPv6
net.ipv6.conf.wlan0.stable_secret = <saída do comando anterior>
net.ipv6.conf.wlan0.addr_gen_mode = 2

```

### NetworkManager

As configurações acima não são respeitadas pelo NetworkManager, mas o NetworkManager usa endereços privados estáveis por padrão.

## Endereço estático

Às vezes, usar um endereço estático pode melhorar a segurança. Por exemplo, se o seu roteador local usa Neighbor Discovery ou radvd ([RFC 2461](http://www.apps.ietf.org/rfc/rfc2461.html)), sua interface receberá automaticamente um endereço baseado em seu endereço MAC (usando a configuração automática sem estado do IPv6). Isso pode ser menos do que ideal para segurança, pois permite que um sistema seja rastreado mesmo que a parte da rede do endereço IP seja alterada.

Para atribuir um endereço IP estático usando [netctl](/index.php/Netctl "Netctl"), veja no exemplo de perfil em `/etc/netctl/examples/ethernet-static`. As seguintes linhas são importantes:

```
...
# Para configuração de endereço IPv6 estático
IP6=static
Address6=('1234:5678:9abc:def::1/64' '1234:3456::123/96')
Routes6=('abcd::1234')
Gateway6='1234:0:123::abcd'

```

**Nota:** Se você estiver conectado somente a IPv6, precisará determinar seu servidor DNS IPv6\. Por exemplo:
```
DNS=('6666:6666::1' '6666:6666::2')

```
Se o seu provedor não forneceu DNS IPv6 e você não está executando o seu próprio, você pode escolher o artigo [resolv.conf](/index.php/Resolv.conf_(Portugu%C3%AAs) "Resolv.conf (Português)").

## IPv6 e PPPoE

A ferramenta padrão para o PPPoE, `pppd`, fornece suporte a IPv6 sob PPPoE desde que seu provedor de internet e seu modem tenham suporte a isso. Basta adicionar ao seguinte a `/etc/ppp/options`

```
+ipv6

```

Se você estiver usando [netctl](/index.php/Netctl "Netctl") para PPPoE, basta adicionar o seguinte a sua configuração de netctl

```
PPPoEIP6=yes

```

## Delegação de prefixo (DHCPv6-PD)

**Nota:** Esta seção é direcionada para a configuração de gateway personalizada, não para máquinas clientes. Para roteadores de mercado padrão, consulte a documentação do seu roteador sobre como habilitar a delegação de prefixo.

A delegação de prefixo é uma técnica comum de implementação de IPv6 usada por muitos ISPs. É um método de atribuição de um prefixo de rede a um site do usuário (por exemplo, rede local). Um roteador pode ser configurado para atribuir diferentes prefixos de rede a várias sub-redes. O ISP distribui um prefixo de rede usando DHCPv6 (geralmente um `/56` ou `/64`) e um cliente dhcp atribui os prefixos à rede local. Para um simples gateway de duas interfaces, ele praticamente atribui um prefixo IPv6 à interface conectada à rede local a partir de um endereço adquirido através da interface conectada à WAN (ou uma pseudo-interface como ppp).

### Com dibbler

[Dibbler](http://klub.com.pl/dhcpv6/) é um cliente e servidor DHCPv6 portátil que pode ser usado para delegação de prefixo. Pode ser [instalado](/index.php/Instala "Instala") com o pacote [dibbler](https://aur.archlinux.org/packages/dibbler/).

Se você está usando `dibbler`, edite `/etc/dibbler/client.conf`

```
log-mode short
log-level 7
# use a interface conectada a sua WAN
iface "WAN" {
  ia
  pd
}

```

**Dica:** Leia dibbler-client(8) para mais informações.

### Com dhcpcd

O [dhcpcd](/index.php/Dhcpcd "Dhcpcd") além do suporte a dhcp IPv4 também fornece uma implementação bastante completa do padrão de cliente DHCPv6 que inclui o DHCPv6-PD. Se você estiver usando `dhcpcd` edite `/etc/dhcpcd.conf`. Você pode já estar usando o dhcpcd para IPv4, portanto, basta atualizar sua configuração existente.

```
duid
noipv6rs
waitip 6
# Descomente esta linha se você está usando dhcpcd para apenas IPv6.
#ipv6only

# usa a interface conectada a WAN
interface WAN
ipv6rs
iaid 1
# use a interface conectada a sua LAN
ia_pd 1 LAN
#ia_pd 1/::/64 LAN/0/64

```

Essa configuração solicitará um prefixo da interface WAN (`WAN`) e a delegará para a interface interna (`LAN`). No caso de um intervalo `/64` ser emitido, você precisará usar a segunda `ia_pd instruction` comentada em seu lugar. Ele também desativará as solicitações do roteador em todas as interfaces, exceto na interface WAN (`WAN`).

**Dica:** Leia também [dhcpcd(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.8) e [dhcpcd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.conf.5).

### Com WIDE-DHCPv6

[WIDE-DHCPv6](http://wide-dhcpv6.sourceforge.net/) é uma implementação de código aberto do Protocolo de Configuração de Host Dinâmico para IPv6 (DHCPv6) originalmente desenvolvido pelo projeto KAME. Pode ser [instalado](/index.php/Instala "Instala") com o pacote [wide-dhcpv6](https://aur.archlinux.org/packages/wide-dhcpv6/).

Se você está usando `wide-dhcpv6`, edite `/etc/wide-dhcpv6/dhcp6c.conf`

```
# use a interface conectada a sua WAN
interface WAN {
  send ia-pd 0;
};

id-assoc pd 0 {
  # use a interface conectada a sua LAN
  prefix-interface LAN {
    sla-id 1;
    sla-len 8;
  };
};

```

**Nota:** `sla-len` deve ser definido de forma que `(WAN-prefix) + (sla-len) = 64`. Neste caso, é configurado para um `/56` prefix 56+8=64\. Para um prefixo `/64`, `sla-len` deve ser `0`.

O cliente wide-dhcpv6 pode ser [iniciado/habilitado](/index.php/Iniciado/habilitado "Iniciado/habilitado") usando o arquivo unit systemd `dhcp6c@*interface*.service`, sendo que `*interface*` é o nome da interface no arquivo de configuração. Por exemplo, para um nome de interface "WAN", use `dhcp6c@WAN.service`.

**Dica:** Leia dhcp6c(8) e dhcp6c.conf(5) para mais informações.

### systemd-networkd

 `/etc/systemd/network/lan.network` 
```
[Network]
Address=192.168.1.1
IPv6PrefixDelegation=dhcpv6
```
 `/etc/systemd/network/wan.network` 
```
[Network]
DHCP=yes
IPForward=yes
IPv6Token=::1
IPv6AcceptRouterAdvertisements=2
IPv6AcceptRA=yes
IPv6DuplicateAddressDetection=1
IPv6PrivacyExtensions=kernel
```

### Outros clientes

[dhclient](/index.php/Dhclient_(Portugu%C3%AAs) "Dhclient (Português)") também pode solicitar um prefixo, mas atribuir esse prefixo ou partes desse prefixo a interfaces deve ser feito usando um script de saída do dhclient. Por exemplo: [https://github.com/jaymzh/v6-gw-scripts/blob/master/dhclient-ipv6](https://github.com/jaymzh/v6-gw-scripts/blob/master/dhclient-ipv6).

## Desabilitar IPv6

**Nota:** O Arch kernel tem suporte a IPv6 compilado diretamente e, portanto, um módulo não pode ser inserido na lista negra.

### Desabilitar funcionalidade

**Atenção:** Desabilitar a pilha IPv6 pode quebrar certos programas que esperam que ela seja ativada. [FS#46297](https://bugs.archlinux.org/task/46297)

Adicionar `ipv6.disable=1` à linha do kernel desabilita toda a pilha IPv6, o que é provável o que você deseja se estiver tendo problemas. Veja [Parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") para mais informações.

Como alternativa, adicionar `ipv6.disable_ipv6=1` manterá a pilha do IPv6 funcional, mas não atribuirá endereços IPv6 a nenhum de seus dispositivos de rede.

Também é possível evitar a atribuição de endereços IPv6 a interfaces de rede específicas, adicionando a seguinte configuração de sysctl a `/etc/sysctl.d/40-ipv6.conf`:

```
# Desabilita IPv6
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.*nic0*.disable_ipv6 = 1
...
net.ipv6.conf.*nicN*.disable_ipv6 = 1

```

Observe que você deve listar explicitamente todas as interfaces de destino, pois a desabilitação de `all.disable_ipv6` não se aplica a interfaces que já estão "up" quando as configurações de sysctl são aplicadas.

Outra observação: se desabilitar o IPv6 por sysctl, você deve comentar os hosts IPv6 em seu `/etc/hosts`:

```
#<endereço-ip> <hostnam.domínio.org> <hostname>
127.0.0.1 localhost.localdomain localhost
#::1 localhost.localdomain localhost

```

caso contrário, pode haver alguns erros de conexão, pois os hosts são resolvidos para o endereço IPv6, que não pode ser acessado.

### Outros programas

Desabilitar a funcionalidade do IPv6 no kernel não impede que outros programas tentem usar o IPv6\. Na maioria dos casos, isso é completamente inofensivo, mas se você tiver problemas com esse programa, consulte as páginas de manual do programa para obter uma maneira de desabilitar essa funcionalidade.

#### dhcpcd

*dhcpcd* vai continuar sem prejuízo tentar realizar uma solicitação IPv6 ao roteador. Para desabilitar isso, conforme documentado na [página man](/index.php/P%C3%A1gina_man "Página man") [dhcpcd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.conf.5), adicione o seguinte ao `/etc/dhcpcd.conf`:

```
noipv6rs
noipv6

```

#### NetworkManager

Para desabilitar IPv6 no NetworkManager, clique com o botão direito no ícone de status de rede, e selecione *Editar conexões > Cabeada >* Nome da rede *> Editar > Configurações IPv6 > Método > Ignorado/Desabilitado*

Então, clique em "Salvar".

#### ntpd

Seguindo o conselho em [systemd (Português)#Arquivos drop-in](/index.php/Systemd_(Portugu%C3%AAs)#Arquivos_drop-in "Systemd (Português)"), [edite](/index.php/Edite "Edite") `ntpd.service` para definir como o systemd o inicia.

Isso criará um trecho drop-in que será executado em vez do padrão `ntpd.service`. O sinalizador `-4` impede que o IPv6 seja usado pelo daemon ntp. Coloque o seguinte no trecho drop-in:

```
[Service]
ExecStart=
ExecStart=/usr/bin/ntpd -4 -g -u ntp:ntp

```

que primeiro limpa o `ExecStart` anterior e, em seguida, o substitui por um que inclua o sinalizador `-4`.

### systemd-networkd

O networkd possui suporte a desabilitação do IPv6 por interface. Quando a seção `[Network]` de uma unidade de rede possui `LinkLocalAddressing=ipv4` ou `LinkLocalAddressing=no`, o networkd não tentará configurar o IPv6 na correspondência interfaces.

No entanto, observe que, mesmo ao usar a opção acima, o networkd ainda esperará receber anúncios do roteador se o IPv6 não estiver desabilitado globalmente. Se o tráfego IPv6 não estiver sendo recebido pela interface (por exemplo, devido a configurações sysctl ou ip6tables), ele permanecerá no estado de configuração e poderá causar tempos limites para os serviços aguardando a configuração completa da rede. Para evitar isso, a opção `IPv6AcceptRA=no` também deve ser definida na seção `[Network]`.

## Preferir IPv4 a IPv6

Descomente a seguinte linha no `/etc/gai.conf`:

```
#
#    Para sites que preferem conexões IPv4, mude a última linha para
#
precedence ::ffff:0:0/96  100

```

## Veja também

*   [IPv6](https://www.kernel.org/doc/Documentation/networking/ipv6.txt) - documentação do kernel.org
*   [Endereços temporários IPv6](http://www.ipsidixit.net/2012/08/09/ipv6-temporary-addresses-and-privacy-extensions/) - um resumo sobre endereços temporários e extensões de privacidade
*   [IPv6 prefixes](http://tldp.org/HOWTO/Linux+IPv6-HOWTO/ch03s02.html) - um resumo de tipos de prefixo
*   [net.ipv6 options](http://tldp.org/HOWTO/Linux+IPv6-HOWTO/ch11s02.html) - documentação de parâmetros do kernel