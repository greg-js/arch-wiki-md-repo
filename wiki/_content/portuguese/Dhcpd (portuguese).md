Artigos relacionados

*   [dhcpcd](/index.php/Dhcpcd "Dhcpcd")

O *dhcpd* é o servidor DHCP da [Internet Systems Consortium](http://www.isc.org/downloads/dhcp/). Ele é útil, por exemplo, em uma máquina agindo como um roteador em uma rede local.

**Nota:** *dhcpd* (DHCP **(server)** daemon) não é o mesmo que [dhcpcd](/index.php/Dhcpcd "Dhcpcd") (DHCP **cliente** daemon).

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Uso](#Uso)
*   [3 Configuração](#Configura.C3.A7.C3.A3o)
    *   [3.1 Ouvindo apenas em uma interface](#Ouvindo_apenas_em_uma_interface)
        *   [3.1.1 Configurando dhcpd](#Configurando_dhcpd)
        *   [3.1.2 Arquivo de serviço](#Arquivo_de_servi.C3.A7o)
    *   [3.2 Usar para PXE](#Usar_para_PXE)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [dhcp](https://www.archlinux.org/packages/?name=dhcp), disponível nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais").

## Uso

*dhcpd* inclui um arquivo unit `dhcpd4.service`, que pode ser usado para [controlar](/index.php/Habilite "Habilite") o daemon. Ele inicia o daemon para *todas* as [interfaces de rede](/index.php/Interfaces_de_rede "Interfaces de rede"). Veja [#Ouvindo apenas em uma interface](#Ouvindo_apenas_em_uma_interface) para uma alternativa.

## Configuração

Atribua um endereço IPv4 estático para a interface que você deseja usar (em nossos exemplos, usaremos `eth0`). Os 3 primeiros bytes deste endereço não podem ser exatamente o mesmo que os de outra interface.

```
# ip link set up dev eth0
# ip addr add 139.96.30.100/24 dev eth0 # endereço arbitrário

```

**Dica:** Geralmente, uma das três sub-redes são usadas para redes privadas, que são especialmente reservadas e não conflitarão com nenhum host na Internet:

*   `192.168/16` (sub-rede `192.168.0.0`, máscara de rede `255.255.0.0`)
*   `172.16/12` (sub-rede `172.16.0.0`, máscara de rede `255.240.0.0`)
*   `10/8` (para redes grandes; sub-rede `10.0.0.0`, máscara de rede `255.0.0.0`)

Veja também [RFC 1918](http://www.ietf.org/rfc/rfc1918.txt).

Para ter seu IP estático atribuído na inicialização, veja [Configuração de rede#Endereço IP estático](/index.php/Configura%C3%A7%C3%A3o_de_rede#Endere.C3.A7o_IP_est.C3.A1tico "Configuração de rede").

O `dhcpd.conf` padrão contém muitos exemplos descomentados, então mude-o:

```
# mv /etc/dhcpd.conf /etc/dhcpd.conf.example

```

O arquivo de configuração mínimo pode se parecer com:

 `/etc/dhcpd.conf` 
```
option domain-name-servers 8.8.8.8, 8.8.4.4;
option subnet-mask 255.255.255.0;
option routers 139.96.30.100;
subnet 139.96.30.0 netmask 255.255.255.0 {
  range 139.96.30.150 139.96.30.250;
}

```

Se você precisar fornecer um endereço IP fixo para um dispositivo único específico, você pode usar a seguinte sintaxe:

 `/etc/dhcpd.conf` 
```
option domain-name-servers 8.8.8.8, 8.8.4.4;
option subnet-mask 255.255.255.0;
option routers 139.96.30.100;
subnet 139.96.30.0 netmask 255.255.255.0 {
  range 139.96.30.150 139.96.30.250;

  host macbookpro{
   hardware ethernet 70:56:81:22:33:44;
   fixed-address 139.96.30.199;
  }
}

```

A opção `domain-name-servers` contém endereços de servidores DNS que são fornecidos aos clientes. No nosso exemplo, estamos usando os servidores DNS públicos do Google. Se você conhece um servidor DNS local (por exemplo, fornecido pelo seu provedor de internet), você deve usá-lo. Se você configurou seu próprio DNS em uma máquina local, use seu endereço em sua sub-rede (por exemplo, g. `139.96.30.100` em nosso exemplo).

`subnet-mask` e `routers` define uma máscara de sub-rede e uma lista de roteadores disponíveis na sub-rede. Na maioria dos casos, para pequenas redes, você pode usar `255.255.255.0` como uma máscara e especificar um endereço IP da máquina em que você está configurando o servidor DHCP como roteador.

`subnet` define opções para sub-redes separadas, que são mapeadas para as interfaces de rede nas quais *dhcpd* está sendo executado. No nosso exemplo, esta é uma sub-rede `139.96.30.0/24` para interface única `eth0`, para a qual definimos o intervalo de endereços IP disponíveis. Os endereços desse intervalo serão atribuídos aos clientes conectados.

### Ouvindo apenas em uma interface

Se o seu computador já faz parte de uma ou várias redes, pode ser um problema se seu computador começar a dar endereços IP para máquinas das outras redes. Isso pode ser feito configurando dhcpd ou iniciando como um daemon com [systemctl](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)").

#### Configurando dhcpd

Para excluir uma interface, você deve criar uma declaração vazia para a sub-rede que será configurada nessa interface.

Isso é feito editando o arquivo de configuração (por exemplo):

 `/etc/dhcpd.conf` 
```
# Nenhum serviço DHCP na rede DMZ (192.168.2.0/24)
subnet 192.168.2.0 netmask 255.255.255.0 {
}

```

#### Arquivo de serviço

Não há arquivos *.service* fornecidos por padrão para usar *dhcpd* apenas em uma interface, então você precisa criar um:

 `/etc/systemd/system/dhcpd4@.service` 
```
[Unit]
Description=IPv4 DHCP server on %I
Wants=network.target
After=network.target

[Service]
Type=forking
PIDFile=/run/dhcpd4.pid
ExecStart=/usr/bin/dhcpd -4 -q -pf /run/dhcpd4.pid %I
KillSignal=SIGINT

[Install]
WantedBy=multi-user.target

```

Esse é um modelo de unit, que vincula-o a uma interface específica, por exemplo `dhcpd4@*eth0*.service`, sendo*eth0* uma interface mostrada com `ip link`.

Às vezes, queremos esperar que a rede seja configurada, neste caso, a solução é fazer o serviço aguardar a network-online.target em vez de network.target:

 `/etc/systemd/system/dhcpd4@.service` 
```
[Unit]
Wants=network-online.target
After=network-online.target

```

Para que isso funcione, devemos habilitar outro serviço para que funcione:

```
# systemctl enable systemd-networkd-wait-online

```

### Usar para PXE

A configuração de PXE é feita com as duas opções a seguir:

 `/etc/dhcpd.conf` 
```
next-server 192.168.0.2;
filename "/pxelinux.0";

```

Essa seção pode tanto ser uma `subnet` inteira ou apenas uma definição de `host`. `next-server` é o IP do servidor TFTP e `filename` é o nome de arquivo da imagem para inicializar. Para mais informações, veja [PXE](/index.php/PXE "PXE").