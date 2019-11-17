**Status de tradução:** Esse artigo é uma tradução de [Dnsmasq](/index.php/Dnsmasq "Dnsmasq"). Data da última tradução: 2019-11-11\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Dnsmasq&diff=0&oldid=587307) na versão em inglês.

Artigos relacionados

*   [Resolução de nome de domínio](/index.php/Resolu%C3%A7%C3%A3o_de_nome_de_dom%C3%ADnio "Resolução de nome de domínio")

[dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html) fornece um [servidor DNS](https://en.wikipedia.org/wiki/Name_server "wikipedia:Name server"), um [servidor DHCP](https://en.wikipedia.org/wiki/pt:Dynamic_Host_Configuration_Protocol "wikipedia:pt:Dynamic Host Configuration Protocol") com suporte a [DHCPv6](https://en.wikipedia.org/wiki/DHCPv6 "wikipedia:DHCPv6") e [PXE](https://en.wikipedia.org/wiki/Preboot_Execution_Environment "wikipedia:Preboot Execution Environment"), e um [servidor TFTP](https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol "wikipedia:Trivial File Transfer Protocol"). Ele é projetado para ser leve e ter um tamanho reduzido, adequado para roteadores e firewalls com recursos restritos. O dnsmasq também pode ser configurado para armazenar em cache as consultas DNS para melhorar as velocidades de pesquisa de DNS nos sites visitados anteriormente.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Iniciar o daemon](#Iniciar_o_daemon)
*   [3 Configuração](#Configuração)
    *   [3.1 Servidor DNS](#Servidor_DNS)
        *   [3.1.1 Arquivo de endereços DNS e encaminhamento](#Arquivo_de_endereços_DNS_e_encaminhamento)
            *   [3.1.1.1 openresolv](#openresolv)
            *   [3.1.1.2 Encaminhamento manual](#Encaminhamento_manual)
        *   [3.1.2 Adicionando um domínio personalizado](#Adicionando_um_domínio_personalizado)
        *   [3.1.3 Testar](#Testar)
    *   [3.2 Servidor DHCP](#Servidor_DHCP)
        *   [3.2.1 Testar](#Testar_2)
    *   [3.3 Servidor TFTP](#Servidor_TFTP)
    *   [3.4 Servidor PXE](#Servidor_PXE)
*   [4 Dicas e truques](#Dicas_e_truques)
    *   [4.1 Evitar que o OpenDNS redirecione as consultas do Google](#Evitar_que_o_OpenDNS_redirecione_as_consultas_do_Google)
    *   [4.2 Substituir endereços](#Substituir_endereços)
    *   [4.3 Mais de uma instância](#Mais_de_uma_instância)
        *   [4.3.1 Estático](#Estático)
        *   [4.3.2 Dinâmico](#Dinâmico)
    *   [4.4 Colocar domínios em lista negra](#Colocar_domínios_em_lista_negra)
*   [5 Veja também](#Veja_também)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq).

## Iniciar o daemon

[Inicie/habilite](/index.php/Inicie/habilite "Inicie/habilite") `dnsmasq.service`.

Para ver se o dnsmasq iniciou adequadamente, verifique o journal do sistema:

```
$ journalctl -u dnsmasq.service

```

A rede também precisará ser reiniciada de forma que o cliente DHCP possa criar um novo `/etc/resolv.conf`.

## Configuração

Para configurar o dnsmasq, edite `/etc/dnsmasq.conf`. O arquivo contém comentários explicando as opções. Para todas as opções disponíveis, veja [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8).

**Atenção:** A configuração padrão do dnsmasq habilita seus servidores DNS. Se você não quiser este serviço, você precisa desabilitá-lo explicitamente definindo a porta DNS para `0`: `port=0` 

**Dica:** Para verificar a sintaxe do(s) arquivo(s) de configuração, execute:
```
$ dnsmasq --test

```

### Servidor DNS

Para configurar o dnsmasq como um daemon de cache DNS em um único computador, especifique uma diretiva `listen-address`, adicionando o endereço IP do host local:

```
listen-address=::1,127.0.0.1

```

Para usar este computador para ouvir em seu endereço IP da LAN para outros computadores na rede. Recomenda-se que você use um IP de LAN estático neste caso. Por exemplo:

```
listen-address=::1,127.0.0.1,192.168.1.1

```

Defina o número de nomes de domínios em cache com `cache-size=*tamanho*` (o padrão é `150`):

```
cache-size=1000

```

Para validar o [DNSSEC](/index.php/DNSSEC_(Portugu%C3%AAs) "DNSSEC (Português)") carregue as âncoras de confiança DNSSEC fornecidas pelo pacote [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) e defina a opção `dnssec`:

```
conf-file=/usr/share/dnsmasq/trust-anchors.conf
dnssec

```

Veja o [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) para mais opções que você pode querer usar.

#### Arquivo de endereços DNS e encaminhamento

Depois de configurar o dnsmasq, você precisa adicionar os endereços de host local como os únicos servidores de nomes em `/etc/resolv.conf`. Isso faz com que todas as consultas sejam enviadas para o dnsmasq.

Como o dnsmasq é um *stub resolver*, isto é, não é um servidor DNS recursivo, você deve configurar o encaminhamento para um servidor DNS externo. Isso pode ser feito automaticamente usando [openresolv](/index.php/Openresolv_(Portugu%C3%AAs) "Openresolv (Português)") ou especificando manualmente o endereço do servidor DNS na configuração do dnsmasq.

##### openresolv

Se seu gerenciador de rede tiver suporte a *resolvconf*, em vez de alterar diretamente o `/etc/resolv.conf`, você pode usar o [openresolv](/index.php/Openresolv_(Portugu%C3%AAs) "Openresolv (Português)") para gerenciar arquivos de configuração para o dnsmasq. [[1]](https://roy.marples.name/projects/openresolv/config)

Edite `/etc/resolvconf.conf` e adicione os endereços de loopback como servidores de nomes e configure o openresolv para escrever a configuração do dnsmasq:

 `/etc/resolvconf.conf` 
```
# Usa o servidor de nomes local
name_servers="::1 127.0.0.1"

# Escreve os arquivos resolv e de configuração estendida do dnsmasq
dnsmasq_conf=/etc/dnsmasq-openresolv.conf
dnsmasq_resolv=/etc/dnsmasq-resolv.conf
```

Executa `resolvconf -u` de forma que os arquivos de configuração sejam criados. Se os arquivos não existirem, `dnsmasq.service` vai falhar ao iniciar.

Edite o arquivo de configuração do dnsmasq para usar a configuração gerada do openresolv:

```
# Leia a configuração gerada pelo openresolv
conf-file=/etc/dnsmasq-openresolv.conf
resolv-file=/etc/dnsmasq-resolv.conf

```

##### Encaminhamento manual

Primeiro, você deve definir endereços de localhost como os únicos servidores de nomes no `/etc/resolv.conf`:

 `/etc/resolv.conf` 
```
nameserver ::1
nameserver 127.0.0.1

```

Certifique-se de proteger `/etc/resolv.conf` de modificações conforme descrito em [Resolução de nome de domínio#Sobrescrita do /etc/resolv.conf](/index.php/Resolu%C3%A7%C3%A3o_de_nome_de_dom%C3%ADnio#Sobrescrita_do_/etc/resolv.conf "Resolução de nome de domínio").

Os endereços de servidor DNS upstream devem então ser especificados no arquivo de configuração do dnsmasq como `server=*endereço_servidor*`. Também adicione `no-resolv` para que o dnsmasq não leia desnecessariamente `/etc/resolv.conf` que contém apenas os endereços de host local de si mesmo.

```
no-resolv

# Servidores do Google, por exemplo
server=8.8.8.8
server=8.8.4.4
```

Agora, as consultas de DNS serão resolvidas com dnsmasq, verificando somente os servidores externos se não puder responder à consulta de seu cache.

#### Adicionando um domínio personalizado

É possível adicionar um domínio personalizado a hosts em sua rede (local):

```
local=/lan/
domain=lan

```

Neste exemplo é possível pingar um host/dispositivo (p.ex., definido em seu arquivo `/etc/hosts`) como `*hostname*.lan`.

Descomente `expand-hosts` para adicionar um domínio personalizado a entradas de host:

```
expand-hosts

```

Sem essa configuração, você terá que adicionar o domínio às entradas de `/etc/hosts`.

#### Testar

Para fazer um teste de velocidade de pesquisa, escolha um site que não tenha sido visitado desde que o dnsmasq foi iniciado (o *drill* faz parte do pacote [ldns](https://www.archlinux.org/packages/?name=ldns)):

```
$ drill archlinux.org | grep "Query time"

```

Executar o comando novamente usará o IP do DNS em cache e resultará em um tempo de pesquisa mais rápido se o dnsmasq estiver configurado corretamente:

 `$ drill archlinux.org | grep "Query time"` 
```
;; Query time: 18 msec

```
 `$ drill archlinux.org | grep "Query time"` 
```
;; Query time: 2 msec

```

Para testar se a validação do DNSSEC está funcionando, veja [DNSSEC (Português)#Testando](/index.php/DNSSEC_(Portugu%C3%AAs)#Testando "DNSSEC (Português)").

### Servidor DHCP

Por padrão, o dnsmasq tem a funcionalidade de DHCP desativada, se você quiser usá-la, deve ativá-la. Aqui estão as configurações importantes:

```
# Ouve apenas à placa de rede 'LAN-NIC' dos roteadores. Fazer isso abre
# a porta 53 tcp/udp para o localhost e a porta 67 udp para o mundo:
interface=<LAN-NIC>

# O dnsmasq vai abrir a porta 53 tcp/udp e porta 67 udp para o mundo
# para ajudar com interfaces dinâmicas (atribuição de IPs dinâmicos).
# O dnsmasq vai descartar requisições do mundo a elas, mas os paranoicos
# podem querer fechá-las e deixar o kernel lidar com elas:
bind-interfaces

# Opcionalmente, defina um nome de domínio
domain=example.com

# Defina o gateway padrão
dhcp-option=3,0.0.0.0

# Defina os servidores DNS para anunciar
dhcp-option=6,0.0.0.0

# Se seu servidor dnsmasq também fizer o roteamento de sua rede,
# você pode usar a opção 121 para aplicar uma rota estática.
# x.x.x.x é a LAN de destino, yy pe a notação CIDR (geralmente /24), 
# e z.z.z.z é o host que vai fazer o roteamento.
dhcp-option=121,x.x.x.x/yy,z.z.z.z

# Intervalo dinâmico de IPs para disponibilizar ao computador e o tempo
# de concessão. Idealmente, defina o tempo de concessão para 5m apenas
# no começo para testar se tudo funciona bem antes de você definir
# registros duradouros:
dhcp-range=192.168.111.50,192.168.111.100,12h

# Fornece concessões IPv6 de DHCP por meio de Router Advertisements (RAs)
# para a sub-rede aaaa:bbbb:cccc:dddd::/64
dhcp-range=aaaa:bbbb:cccc:dddd::,ra-only,infinite

# Se você quiser ter o dnsmasq atribuindo IPs estáticos para alguns
# clientes, vincule os endereços MAC da placa de rede dos computadores:
dhcp-host=aa:bb:cc:dd:ee:ff,192.168.111.50
dhcp-host=aa:bb:cc:ff:dd:ee,192.168.111.51

```

Veja [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) para mais opções.

#### Testar

A partir de um computador conectado ao dnsmasq, configure-o para usar o DHCP para atribuição automática de endereço IP e, em seguida, tente efetuar login na rede normalmente.

Se você inspecionar o arquivo `/var/lib/misc/dnsmasq.leases` no servidor, poderá ver a concessão.

### Servidor TFTP

O dnsmasq tem um servidor [TFTP](/index.php/TFTP_(Portugu%C3%AAs) "TFTP (Português)") embutido.

Para usá-lo, crie um diretório para a raiz do TFTP (p.ex., `/srv/tftp`) para colocar arquivos transferíveis nele.

Para aumentar a segurança, é aconselhável usar o modo seguro de TFTP do dnsmasq. No modo seguro, apenas os arquivos pertencentes ao usuário `dnsmasq` serão atendidos pelo TFTP. Você precisará fazer [chown](/index.php/Chown_(Portugu%C3%AAs) "Chown (Português)") na raiz do TFTP e todos os arquivos nele para o usuário `dnsmasq` usar este recurso.

Habilite o TFTP:

```
enable-tftp
tftp-root=/srv/tftp
tftp-secure

```

Veja [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) para mais opções.

### Servidor PXE

O PXE requer servidores DHCP e TFTP, ambas as funções podem ser fornecidas pelo dnsmasq.

**Dica:** O dnsmasq pode ser executado no modo "proxy-DHCP" e adicionar opções de inicialização PXE a uma rede com um servidor DHCP já em execução:
```
interface=*enp0s0*
bind-dynamic
dhcp-range=*192.168.0.1*,proxy
```

1.  defina [#Servidor TFTP](#Servidor_TFTP) e [#Servidor DHCP](#Servidor_DHCP)
2.  copie e configure um gerenciador de boot compatível com PXE (p.ex., [PXELINUX](/index.php/PXELINUX "PXELINUX")) na raiz do TFTP
3.  habilite PXE no `/etc/dnsmasq.conf`:

**Nota:**

*   caminhos de arquivos são relativos à raiz do TFTP
*   se o arquivo tem um sufixo `.0`, você deve excluir o sufixo nas opções `pxe-service`

Para apenas enviar um arquivo:

```
dhcp-boot=lpxelinux.0

```

Para enviar um arquivo dependente da arquitetura do cliente:

```
pxe-service=x86PC, "PXELINUX (BIOS)", "bios/lpxelinux"
pxe-service=X86-64_EFI, "PXELINUX (EFI)", "efi64/syslinux.efi"

```

**Nota:** No caso de `pxe-service` não funcionar (especialmente para clientes baseados em UEFI), a combinação de `dhcp-match` e `dhcp-boot` pode ser usada. Veja [RFC4578](https://tools.ietf.org/html/rfc4578#section-2.1) para mais números de `client-arch` para usar com o protocolo de inicialização de dhcp.

```
dhcp-match=set:efi-x86_64,option:client-arch,7
dhcp-match=set:efi-x86_64,option:client-arch,9
dhcp-match=set:efi-x86,option:client-arch,6
dhcp-match=set:bios,option:client-arch,0
dhcp-boot=tag:efi-x86_64,"efi64/syslinux.efi"
dhcp-boot=tag:efi-x86,"efi32/syslinux.efi"
dhcp-boot=tag:bios,"bios/lpxelinux.0"

```

Veja [dnsmasq(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dnsmasq.8) para mais opções.

O resto é por conta do [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot").

## Dicas e truques

### Evitar que o OpenDNS redirecione as consultas do Google

Para evitar que o OpenDNS redirecione todas as consultas do Google para seu próprio servidor de pesquisa, adicione ao `/etc/dnsmasq.conf`:

 `server=/www.google.com/<IP do DNS do provedor>` 

### Substituir endereços

Em alguns casos, como ao operar um portal cativo, pode ser útil resolver nomes de domínios específicos para um conjunto de endereços codificados. Isso é feito com a configuração `address`:

```
address=/example.com/1.2.3.4

```

Além disso, é possível retornar um endereço específico para todos os nomes de domínio que não são respondidos de `/etc/hosts` ou DHCP usando um curinga especial:

```
address=/#/1.2.3.4

```

### Mais de uma instância

Se quisermos que dois ou mais servidores dnsmasq funcionem por interface(s).

#### Estático

Para fazer isso de forma estática, servidor por interface, use as opções `interface` e `bind-interface`. Esta execução inicial segundo dnsmasq.

#### Dinâmico

Neste caso, podemos excluir por interface e vincular quaisquer outras:

```
except-interface=lo
bind-dynamic

```

**Nota:** Esse é o padrão no [libvirt](/index.php/Libvirt "Libvirt").

### Colocar domínios em lista negra

Para fazer um *blacklist* em domínios, ou seja, as respostas a consultas para eles com NXDOMAIN, use a opção `address` sem especificar o endereço IP:

```
address=/blacklisted.example/
address=/another.blacklisted.example/

```

Para facilitar o uso, coloque a lista negra em um arquivo separado, como, por exemplo, `/etc/dnsmasq.d/blacklist.conf`, e carregue-o a partir de `/etc/dnsmasq.conf` com `conf-file=/etc/dnsmasq.d/blacklist.conf` ou `conf-dir=conf-dir=/etc/dnsmasq.d/,*.conf`.

**Dica:** Uma lista de fontes potenciais para a lista negra pode ser encontrada no [README do pacote de bloqueador de propagandas do OpenWrt](https://github.com/openwrt/packages/blob/master/net/adblock/files/README.md).

## Veja também

*   [Fazendo cache de servidor de nome usando dnsmasq e algumas outras dicas e truques.](http://www.g-loaded.eu/2010/09/18/caching-nameserver-using-dnsmasq/)