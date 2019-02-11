**Status de tradução:** Esse artigo é uma tradução de [IPv6 tunnel broker setup](/index.php/IPv6_tunnel_broker_setup "IPv6 tunnel broker setup"). Data da última tradução: 2019-01-25\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=IPv6_tunnel_broker_setup&diff=0&oldid=564696) na versão em inglês.

A Hurricane Electric oferece um serviço gratuito de [tunnel broker](http://tunnelbroker.net/) que é relativamente fácil de usar sob o Arch se você deseja adicionar conectividade IPv6 a um host somente IPv4.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Registrando por um tunnel](#Registrando_por_um_tunnel)
*   [2 Configurando um túnel Hurricane Electric](#Configurando_um_túnel_Hurricane_Electric)
*   [3 systemd-networkd](#systemd-networkd)
*   [4 Usando tunelamento com IP IPv4 dinâmico](#Usando_tunelamento_com_IP_IPv4_dinâmico)

## Registrando por um tunnel

Não é tão difícil de fazer. Sinta-se à vontade para preencher as instruções aqui se algo parecer complicado, mas, caso contrário, basta ir ao site do *tunnel broker* e completar o registro.

## Configurando um túnel Hurricane Electric

Crie a seguinte unidade systemd, substituindo o texto em negrito pelos endereços IP que você obteve do HE:

**Nota:** Se você está por traz de um NAT (configuração típica de roteador residencial), use seu endereço IPv4 *local* para `**endereço_IPv4_cliente**`, p.ex., `192.168.0.2`.
 `/etc/systemd/system/he-ipv6.service` 
```
[Unit]
Description=he.net IPv6 tunnel
After=network.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/bin/ip tunnel add he-ipv6 mode sit remote **endereço_IPv4_servidor** local **endereço_IPv4_cliente** ttl 255
ExecStart=/usr/bin/ip link set he-ipv6 up mtu 1480
ExecStart=/usr/bin/ip addr add **endereço_IPv6_cliente** dev he-ipv6
ExecStart=/usr/bin/ip -6 route add ::/0 dev he-ipv6
ExecStop=/usr/bin/ip -6 route del ::/0 dev he-ipv6
ExecStop=/usr/bin/ip link set he-ipv6 down
ExecStop=/usr/bin/ip tunnel del he-ipv6

[Install]
WantedBy=multi-user.target
```

Então, [inicie/habilite](/index.php/Inicie/habilite "Inicie/habilite") `he-ipv6.service`.

## systemd-networkd

Se [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") lida suas conexões de rede, é provavelmente uma idea melhor para deixá-lo lidar com *tunnel broker* também (em vez de usar um arquivo `.service`).

 `/etc/systemd/network/he-tunnel.netdev` 
```
[Match]

[NetDev]
Name=he-ipv6
Kind=sit
MTUBytes=1480

[Tunnel]
Local=<IPv4 local>
Remote=<outro lado do túnel>
TTL=255

```
 `/etc/systemd/network/he-tunnel.network` 
```
[Match]
Name=he-ipv6

[Network]
Address=<IPv6 local>
Gateway=<gateway IPv6>
DNS=2001:4860:4860::8888
DNS=2001:4860:4860::8844

```

e adicione essa linha à seção `[Network]` de seu arquivo `.network` padrão de conexão internet:

```
Tunnel=he-ipv6

```

## Usando tunelamento com IP IPv4 dinâmico

A maneira mais simples de usar o tunelamento com um IP IPv4 dinâmico é configurar um cronjob que atualizará periodicamente seu endereço atual. O URL de exemplo e uma *Chave de atualização* podem ser encontrados na aba *Avançado* da página *Detalhes do túnel*.

Para verificar se a atualização funciona, execute o seguinte comando (substitua `*USERNAME*`, `*UPDATEKEY*` e `*TUNNELID*` pelo detalhes de sua conta e túnel):

```
$ wget -O - https://*USERNAME*:*UPDATEKEY*@ipv4.tunnelbroker.net/nic/update?hostname=*TUNNELID*

```

Se funcionar, crie um cronjob abrindo `crontab -e` e adicionando uma nova linha:

```
*/10 * * * * wget -q -O /dev/null https://*USERNAME*:*UPDATEKEY*@ipv4.tunnelbroker.net/nic/update?hostname=*TUNNELID*

```