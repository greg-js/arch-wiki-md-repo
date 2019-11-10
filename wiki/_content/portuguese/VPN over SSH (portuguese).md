**Status de tradução:** Esse artigo é uma tradução de [VPN over SSH](/index.php/VPN_over_SSH "VPN over SSH"). Data da última tradução: 2019-1-06\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=VPN_over_SSH&diff=0&oldid=586491) na versão em inglês.

Existem várias maneiras de configurar uma rede privada virtual por meio do SSH. Note que, embora isso possa ser útil de tempos em tempos, pode não ser uma substituição completa para uma VPN regular. Veja por exemplo [[1]](http://sites.inka.de/bigred/devel/tcp-tcp.html).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Usando tun2socks do badvpn](#Usando_tun2socks_do_badvpn)
    *   [1.1 Iniciar proxy SOCKS dinâmico de SSH](#Iniciar_proxy_SOCKS_dinâmico_de_SSH)
    *   [1.2 Configurar interface de tunelamento e badvpn](#Configurar_interface_de_tunelamento_e_badvpn)
    *   [1.3 Fazer o tráfego passar por um túnel](#Fazer_o_tráfego_passar_por_um_túnel)
*   [2 Tunelamento incorporado do OpenSSH](#Tunelamento_incorporado_do_OpenSSH)
    *   [2.1 Criar interfaces tun usando systemd-networkd](#Criar_interfaces_tun_usando_systemd-networkd)
        *   [2.1.1 Criando interfaces em comando SSH](#Criando_interfaces_em_comando_SSH)
    *   [2.2 Iniciar SSH](#Iniciar_SSH)
    *   [2.3 Solução de problemas](#Solução_de_problemas)
*   [3 Usando PPP por SSH](#Usando_PPP_por_SSH)
    *   [3.1 Script auxiliar](#Script_auxiliar)
*   [4 Veja também](#Veja_também)

## Usando tun2socks do badvpn

[badvpn](https://www.archlinux.org/packages/?name=badvpn) é uma coleção de utilitários para vários casos de uso relacionados à VPN.

### Iniciar proxy SOCKS dinâmico de SSH

Primeiro, vamos configurar um proxy socks dinâmico de SSH normal como de costume:

```
$ ssh -TND 4711 <seu_usuário>@<servidor_SSH>

```

### Configurar interface de tunelamento e badvpn

Depois, podemos prosseguir com a configuração do TUN.

```
# ip tuntap add dev tun0 mode tun user <seu_usuário_local>
# ip addr replace 10.0.0.1/24 dev tun0
# badvpn-tun2socks --tundev tun0 --netif-ipaddr 10.0.0.2 --netif-netmask 255.255.255.0 --socks-server-addr localhost:4711

```

Agora você tem uma interface local `tun0` funcionando que encaminha todo o tráfego que entra nele através do proxy SOCKS que você configurou anteriormente.

### Fazer o tráfego passar por um túnel

Tudo o que resta a fazer agora é configurar uma rota local para obter algum tráfego para ela. Vamos configurar uma rota que direcione todo o tráfego para ela. Vamos precisar de três rotas:

1.  Rota que vai para o servidor SSH que usamos para o túnel com uma baixa métrica.
2.  Rota para o servidor DNS (porque o tun2socks não faz o UDP que é necessário para o DNS) com uma baixa métrica.
3.  Rota padrão para todos os outros tráfegos com uma métrica mais alta que as outras rotas.

A ideia por trás da definição específica das métricas é que precisamos garantir que a rota escolhida para o servidor SSH seja sempre direta, caso contrário, ela retornaria ao túnel SSH, o que causaria um loop e, como resultado, perderíamos a conexão SSH. Além disso, precisamos definir uma rota DNS explícita, pois o tun2socks não faz o encapsulamento do UDP (necessário para o DNS). Também precisamos de uma nova rota padrão com uma métrica menor do que a sua rota padrão antiga para que o tráfego entre no túnel. Com tudo isso dito, vamos começar a trabalhar:

```
# ip route add <IP_do_servidor_SSH> via <IP_do_gateway_original> metric 5
# ip route add <IP_do_servidor_DNS> via <IP_do_gateway_original> metric 5
# ip route add default via 10.0.0.2 metric 6

```

Agora todo o tráfego (exceto o DNS e o próprio servidor SSH) deve passar `tun0`.

## Tunelamento incorporado do OpenSSH

O OpenSSH tem suporte a TUN/TAP integrado usando `-w<número-tun-local>:<número-tun-remoto>`. Aqui, um túnel de camada 3/ponto-a-ponto/TUN é descrito. Também é possível criar um túnel de camada 2/ethernet/TAP.

### Criar interfaces tun usando systemd-networkd

 `/etc/systemd/network/vpn.netdev` 
```
[NetDev]
Name=tun5
Kind=tun

[Tun]
User=vpn
Group=network
```
 `/etc/systemd/network/vpn.network` 
```
[Match]
Name=tun5

[Address]
Address=192.168.200.2/24
```

Assim que esses arquivos são criados, habilite-os [reiniciando](/index.php/Reinicia "Reinicia") `systemd-networkd.service`.

Também, você pode gerenciar as interfaces tun com o comando `ip tunnel`.

#### Criando interfaces em comando SSH

O SSH pode criar as duas interfaces automaticamente, mas você deve configurar o IP e o roteamento após a conexão ser estabelecida.

```
ssh \
  -o PermitLocalCommand=yes \
  -o LocalCommand="sudo ifconfig tun5 192.168.244.2 pointopoint 192.168.244.1 netmask 255.255.255.0" \
  -o ServerAliveInterval=60 \
  -w 5:5 vpn@example.com \
  'sudo ifconfig tun5 192.168.244.1 pointopoint 192.168.244.2 netmask 255.255.255.0; echo tun0 ready'
```

### Iniciar SSH

```
ssh -f -w5:5 vpn@example.com -i ~/.ssh/key "sleep 1000000000"

```

ou você pode adicionar opções keep-alive se estiver atrás de um NAT.

```
ssh -f -w5:5 vpn@example.com \
        -o ServerAliveInterval=30 \
        -o ServerAliveCountMax=5 \
        -o TCPKeepAlive=yes \
        -i ~/.ssh/key "sleep 1000000000"
```

### Solução de problemas

*   ssh deve ter direitos de acesso à interface do tun ou permissões para criá-lo. Verifique o proprietário da interface tun e/ou /dev/net/tun.
*   Obviamente, se você deseja acessar uma rede em vez de uma única máquina, você deve configurar corretamente o encaminhamento de pacotes IP, roteamento e talvez um netfilter em ambos os lados.

## Usando PPP por SSH

[pppd](/index.php/Pppd "Pppd") pode ser facilmente usado para criar um túnel por meio de um servidor SSH:

```
# pppd updetach noauth silent nodeflate pty "/usr/bin/ssh root@remote-gw /usr/sbin/pppd nodetach notty noauth" ipparam vpn 10.0.8.1:10.0.8.2

```

Quando a VPN é estabelecida, você pode rotear o tráfego através dela. Para obter acesso a uma rede interna:

```
# ip route add 192.168.0.0/16 via 10.0.8.2

```

Para rotear todo o tráfego da Internet através do túnel, por exemplo, para proteger sua comunicação em uma rede não criptografada, primeiro adicione uma rota ao servidor SSH através de seu gateway regular:

```
# ip route add <gw-remoto> via <gateway_padrão_atual>

```

Em seguida, substitua a rota padrão pelo túnel

```
# ip route replace default via 10.0.8.2

```

### Script auxiliar

[pvpn](https://github.com/halhen/pvpn) (pacote [pvpn](https://aur.archlinux.org/packages/pvpn/)) é um script wrapper de `pppd` por SSH.

## Veja também

*   [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede")
*   [Roteador](/index.php/Router "Router")
*   [OpenSSH](/index.php/OpenSSH "OpenSSH")
*   [sshuttle](https://www.archlinux.org/packages/?name=sshuttle), um túnel [python](/index.php/Python "Python")