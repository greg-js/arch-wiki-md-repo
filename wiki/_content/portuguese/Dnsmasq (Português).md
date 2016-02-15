**dnsmasq** proporciona serviços como cache DNS e servidor DHCP. Como um Sistema de Nomes de Domínio (DNS), pode armazenar em cache as consultas DNS para melhorar a velocidade de conexão para sites previamente visitados. E como um servidor DHCP, _dnsmasq_ pode ser usado para prover endereços IP internos e roteamento para computadores em uma LAN. Ambos serviços podem ser implementados. _dnsmasq_ é considerado leve e de fácil configuração; é próprio para o uso pessoal como também para uma rede com até 50 computadores. Ainda oferece suporte a servidor [PXE](/index.php/PXE "PXE").

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Configuração do cache DNS](#Configura.C3.A7.C3.A3o_do_cache_DNS)
    *   [2.1 Arquivo de endereços DNS](#Arquivo_de_endere.C3.A7os_DNS)
        *   [2.1.1 resolv.conf](#resolv.conf)
            *   [2.1.1.1 Mais de três nameservers](#Mais_de_tr.C3.AAs_nameservers)
        *   [2.1.2 dhcpcd](#dhcpcd)
        *   [2.1.3 dhclient](#dhclient)
    *   [2.2 NetworkManager](#NetworkManager)
        *   [2.2.1 Outros Métodos](#Outros_M.C3.A9todos)
*   [3 Configuração servidor DHCP](#Configura.C3.A7.C3.A3o_servidor_DHCP)
*   [4 Iniciar o _daemon_](#Iniciar_o_daemon)
*   [5 Teste](#Teste)
    *   [5.1 Cache DNS](#Cache_DNS)
    *   [5.2 Servidor DHCP](#Servidor_DHCP)
*   [6 Dicas e Sugestões](#Dicas_e_Sugest.C3.B5es)
    *   [6.1 Previna OpenDNS redirecione Consultas do Google](#Previna_OpenDNS_redirecione_Consultas_do_Google)
    *   [6.2 Visualizar leases](#Visualizar_leases)
    *   [6.3 Adicionar um domínio personalizado](#Adicionar_um_dom.C3.ADnio_personalizado)

## Instalação

[Instale](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) pelo [repositório oficial](/index.php/Official_repositories "Official repositories").

## Configuração do cache DNS

Para configurar _dnsmasq_ como um _daemon_ de armazenamento DNS em um único computador edite `/etc/dnsmasq.conf` e descomente a diretiva `listen-address`, adicionando o endereço de IP _localhost_:

```
listen-address=127.0.0.1

```

Para usar este computador para que outros computadores conectados a mesma rede possam consultar com seu endereço IP na LAN:

```
listen-address=192.168.1.1    # Exemplo de endereço de IP

```

Neste caso é recomendável que você tenha um endereço de IP estático em sua LAN.

### Arquivo de endereços DNS

Depois de configurar _dnsmasq_ o cliente DHCP necessitará ser reconfigurado para que o endereço _localhost_ preceda os endereços DNS conhecidos em `/etc/resolv.conf`. Isso faz com que todas as consultas sejam enviadas para _dnsmasq_ antes que sejam resolvidas com um DNS externo. Depois que o cliente DHCP esteja configurado a rede precisa ser reiniciada para que as mudanças tenham efeitos.

#### resolv.conf

Uma opção seria a simples configuração de `resolv.conf`. Para fazer isso basta que o primeiro _nameserver_ em `/etc/resolv.conf` aponte para _localhost_:

 `/etc/resolv.conf` 

```
nameserver 127.0.0.1
# nameservers externos
...

```

Agora as consultas DNS serão resolvidas primeiro com _dnsmaq_, somente checando servidores externos se _dnsmasq_ não puder resolver a consulta. Observe que [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) tende a modificar `/etc/resolve.con` por padrão, então se você usa DHCP seria uma boa ideia proteger `/etc/resolv.conf`. Para fazer isso adicione `nohook resolv.conf` ao arquivo de configuração dhcpcd.conf:

 `/etc/dhcpcd.conf` 

```
...
nohook resolv.conf
```

Seria possível também proteger contra escrita seu resolv.conf:

```
# chattr +i /etc/resolv.conf

```

Caso queira desfazer a proteção contra escrita execute:

```
# chattr -i /etc/resolve.conf

```

##### Mais de três nameservers

Uma limitação na forma como Linux maneja consultas DNS é que só podem haver um máximo de três _nameservers_ usados em `resolv.conf`. Uma solução alternativa seria fazer _localhost_ como único nameserver em `resolv.conf`, e depois criar um `resolv-file` separado para seu _nameserver_ externo. Primeiro crie um novo arquivo _resolv_ para _dnsmasq_:

 `/etc/resolv.dnsmasq.conf` 

```
# Neste caso Google DNS
nameserver 8.8.8.8
nameserver 8.8.4.4

```

Depois edite `/etc/dnsmasq.conf` para usar seu novo arquivo _resolv_:

 `/etc/dnsmasq.conf` 

```
...
resolv-file=/etc/resolv.dnsmasq.conf
...

```

#### dhcpcd

[dhcpcd](/index.php/Dhcpcd "Dhcpcd") tem a habilidade de antepor ou adicionar _nameservers_ a `/etc/resolv.com` criando ou editando os arquivos `/etc/resolv.con.head` e `/etc/resolv.conf.tail`, respectivamente: `server=/example1.com/exemple2.com/xx.xxx.xxx.x`

```
echo "nameserver 127.0.0.1" > /etc/resolv.conf.head

```

#### dhclient

Para [dhclient](https://www.archlinux.org/packages/?name=dhclient), descomente em `/etc/dhclient.conf`:

```
prepend domain-name-servers 127.0.0.1;

```

### NetworkManager

[NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") tem a habilidade de iniciar _dnsmasq_ pelo seu arquivo de configuração. Adicione a opção `dns=dnsmasq` a `NetworkManager.conf` na seção `[main]` depois desabilite o `dnsmasq.service` para que não seja iniciado pelo [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)").

 `/etc/NetworkManager/NetworkManager.conf` 

```
[main]
plugins=keyfile
dns=dnsmasq

```

Configurações personalizadas podem ser criadas para _dnsmasq_ criando um arquivo de configuração em `/etc/NetworkManager/dnsmasq.d/`. Por exemplo, para mudar o tamanho do cache DNS (que é armazenado na memória RAM):

 `/etc/NetworkManager/dnsmasq.d/cache`  `cache-size=1000` 

Quando _dnsmasq_ é iniciado por `NetworkManager` arquivo de configuração em seu diretório é usado no lugar do arquivo de configuração padrão.

**Dica:** Este método permite habilitar configurações personalizadas de DNS em domínios privados. Por exemplo: `server=/exemplo1.com/exemplo2.com/xx.xxx.xxx.xx` muda o primeiro endereço DNS para `xx.xxx.xxx.xx` enquanto navega somente os seguintes web sites `exemplo1.com, exemplo2.com`. Este método é preferível para uma configuração global de DNS enquanto usa _nameservers_ de DNS que careçam de velocidade, estabilidade, privacidade e segurança.

#### Outros Métodos

Outra opção está nas configurações do NetworkManager onde se pode listar as conexões e manualmente configurá-las. Veja [NetworkManager](/index.php/NetworkManager "NetworkManager") para mais informações (inglês).

## Configuração servidor DHCP

Por padrão _dnsmasq_ tem a funcionalidade DHCP desativada, case dejese utiliza-la deve acivar em `/etc/dnsmasq.con`. Aqui estão configurações importantes:

```
# Only listen to routers' LAN NIC.  Doing so opens up tcp/udp port 53 to
# localhost and udp port 67 to world:
interface=<LAN-NIC>

# dnsmasq will open tcp/udp port 53 and udp port 67 to world to help with
# dynamic interfaces (assigning dynamic ips). Dnsmasq will discard world
# requests to them, but the paranoid might like to close them and let the 
# kernel handle them:
bind-interfaces

# Dynamic range of IPs to make available to LAN pc
dhcp-range=192.168.111.50,192.168.111.100,12h

# If you’d like to have dnsmasq assign static IPs, bind the LAN computer's
# NIC MAC address:
dhcp-host=aa:bb:cc:dd:ee:ff,192.168.111.50

```

## Iniciar o _daemon_

Para iniciar _dnsmasq_ com o sistema:

 `# systemctl enable dnsmasq` 

Para iniciar _dnsmasq_ imediatamente:

 `# systemctl start dnsmasq` 

Para verificar se _dnsmasq_ iniciou adequadamente verifique o _journal_ do sistema:

 `# journalctl -u dnsmasq` 

A rede precisa ser reiniciada para que o cliente DHCP execute as novas configurações em `/etc/resolv.conf`

## Teste

### Cache DNS

Para fazer um teste de velocidade escolha um web site que **não** foi visitado desde que _dnsmasq_ foi iniciado.

**Dica:** O comando _dig_ é parte do pacote [dnsutils](https://www.archlinux.org/packages/?name=dnsutils)

```
$ dig archlinux.org | grep "Query time"

```

Ao executar o comando novamente será usado o endereço DNS em cache resultando em uma resolução rápida caso _dnsmasq_ esteja corretamente configurado

 `$ dig archlinux.org | grep "Query time"` 

```
;; Query time: 18 msec

```

 `$ dig archlinux.org | grep "Query time"` 

```
;; Query time: 2 msec

```

### Servidor DHCP

De um computador conectado a outro por meio do _dnsmasq_, configure-o para usar DHCP para atribuição automática de endereço de IP, então faça login na rede normalmente.

## Dicas e Sugestões

### Previna OpenDNS redirecione Consultas do Google

Para prevenir que OpenDns redirecione todas as consultas do Google para seus proprios servidores adicione a `/etc/dnsmasq.conf`:

 `server=/www.google.com/<ISP DNS IP>` 

### Visualizar leases

 `$ cat /var/lib/misc/dnsmasq.leases` 

### Adicionar um domínio personalizado

É possível adicionar domínios personalizados na sua rede local:

```
local=/home.lan/
domain=home.lan

```

Neste exemplo é possível enviar _ping_ a um host/device, por exemplo, definido no seu arquivo _hosts_ como `hostname.home.lan`.

Descomente `expand-hosts` para adicionar um domínio personalizado as entradas de _hosts_:

```
expand-hosts

```

Sem esses ajuste você terá que adicionar o domínio as entradas de `/etc/hosts`.