**Status de tradução:** Esse artigo é uma tradução de [Dnscrypt-proxy](/index.php/Dnscrypt-proxy "Dnscrypt-proxy"). Data da última tradução: 2018-09-17\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Dnscrypt-proxy&diff=0&oldid=541854) na versão em inglês.

O [dnscrypt-proxy](https://github.com/jedisct1/dnscrypt-proxy) é um proxy DNS com suporte para os protocolos DNS criptografados [DNS sobre HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "wikipedia:DNS over HTTPS") e [DNSCrypt](https://dnscrypt.info/), que pode ser usado para prevenir ataques do tipo *man-in-the-middle* e espionagem. O *dnscrypt-proxy* também é compatível com [DNSSEC](/index.php/DNSSEC_(Portugu%C3%AAs) "DNSSEC (Português)").

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Configuração](#Configura.C3.A7.C3.A3o)
    *   [2.1 Inicialização](#Inicializa.C3.A7.C3.A3o)
    *   [2.2 Selecionar resolvedor](#Selecionar_resolvedor)
    *   [2.3 Desabilitar quaisquer serviços na porta 53](#Desabilitar_quaisquer_servi.C3.A7os_na_porta_53)
    *   [2.4 Modificar resolv.conf](#Modificar_resolv.conf)
    *   [2.5 Iniciar o serviço systemd](#Iniciar_o_servi.C3.A7o_systemd)
*   [3 Dicas e truques](#Dicas_e_truques)
    *   [3.1 Configuração de cache de DNS local](#Configura.C3.A7.C3.A3o_de_cache_de_DNS_local)
        *   [3.1.1 Alterar a porta](#Alterar_a_porta)
        *   [3.1.2 Exemplo de configurações de cache de DNS local](#Exemplo_de_configura.C3.A7.C3.B5es_de_cache_de_DNS_local)
            *   [3.1.2.1 Unbound](#Unbound)
            *   [3.1.2.2 dnsmasq](#dnsmasq)
            *   [3.1.2.3 pdnsd](#pdnsd)
    *   [3.2 Sandboxing](#Sandboxing)
    *   [3.3 Habilitar EDNS0](#Habilitar_EDNS0)
        *   [3.3.1 Testar EDNS0](#Testar_EDNS0)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy).

## Configuração

### Inicialização

O serviço pode ser iniciado de duas formas mutuamente exclusivas (ou seja, apenas um dos dois pode estar ativado):

*   Com o arquivo `.service`.

**Nota:** A opção `listen_addresses` deve ser configurado (p.ex., `listen_addresses = ['127.0.0.1:53', '[::1]:53']`) no arquivo de configuração quando estiver usando o arquivo `.service`.

*   Por meio de ativação de `.socket`.

**Nota:** Ao usar a ativação de soquete, a opção `listen_addresses` deve ser definida como vazia (p.ex., `listen_addresses = [ ]`) no arquivo de configuração, pois o systemd cuida da configuração do soquete.

### Selecionar resolvedor

Ao deixar `server_names` comentado no arquivo de configuração `/etc/dnscrypt-proxy/dnscrypt-proxy.toml`, o *dnscrypt-proxy* escolherá o servidor mais rápido a partir das fontes já configurado em `[sources]` [[1]](https://github.com/jedisct1/dnscrypt-proxy/wiki/Configuration#an-example-static-server-entry). As listas serão baixadas, verificadas e atualizadas automaticamente [[2]](https://github.com/jedisct1/dnscrypt-proxy/wiki/Configuration-Sources#what-is-the-point-of-these-lists). Assim, a configuração de um conjunto específico de servidores é opcional.

Para definir manualmente qual servidor é usado, edite `/etc/dnscrypt-proxy/dnscrypt-proxy.toml` e descomente a variável `server_names`, selecionando um ou mais dos servidores. Por exemplo, para usar os servidores da Cloudflare:

```
server_names = ['cloudflare', 'cloudflare-ipv6']

```

Uma lista completa de resolvedores está localizada na [página do upstream](https://download.dnscrypt.info/resolvers-list/v2/public-resolvers.md) ou no [Github](https://raw.githubusercontent.com/DNSCrypt/dnscrypt-resolvers/master/v2/public-resolvers.md). Se o *dnscrypt-proxy* já tiver sido executado com sucesso no sistema antes, `/var/cache/dnscrypt-proxy/public-resolvers.md` também conterá uma lista. Olhe a descrição dos servidores que validam [DNSSEC (Português)](/index.php/DNSSEC_(Portugu%C3%AAs) "DNSSEC (Português)"), não registram e não são censurados. Esses requisitos podem ser configurados globalmente com as opções `require_dnssec`, `require_nolog`, `require_nofilter`.

### Desabilitar quaisquer serviços na porta 53

**Dica:** Se estiver usando [#Unbound](#Unbound) como seu cache de DNS local, esta seção pode ser ignorada, pois *unbound* é executado na porta 53 por padrão.

Para ver se algum programa está usando a porta 53, execute:

```
 $ ss -lp 'sport = :domain'

```

Se a saída contiver mais do que a primeira linha de nomes de coluna, será necessário desabilitar qualquer serviço que esteja usando a porta 53\. Um culpado comum é `systemd-resolved.service`, mas outros gerentes de rede podem ter componentes análogos. Você está pronto para prosseguir, uma vez que o comando acima não produz nada além da seguinte linha:

```
 Netid               State                 Recv-Q                Send-Q                                 Local Address:Port                                   Peer Address:Port

```

### Modificar resolv.conf

Modifique o arquivo [resolv.conf](/index.php/Resolv.conf_(Portugu%C3%AAs) "Resolv.conf (Português)") e substitua o conjunto atual de endereços do resolvedor pelo endereço para *localhost* e opções [[3]](https://github.com/jedisct1/dnscrypt-proxy/wiki/Installation-linux#step-4-change-the-system-dns-settings):

```
nameserver 127.0.0.1
options edns0 single-request-reopen

```

Outros programas sobrescrevem essa configuração. Veja [resolv.conf (Português)#Sobrescrita do /etc/resolv.conf](/index.php/Resolv.conf_(Portugu%C3%AAs)#Sobrescrita_do_.2Fetc.2Fresolv.conf "Resolv.conf (Português)") para detalhes.

### Iniciar o serviço systemd

Finalmente, [inicie/habilite](/index.php/Inicie/habilite "Inicie/habilite") a unit `dnscrypt-proxy.service` ou `dnscrypt-proxy.socket`, dependendo de qual método você escolheu.

## Dicas e truques

### Configuração de cache de DNS local

**Dica:** *dnscrypt-proxy* pode armazenar entradas em cache sem depender de outro programa. Este recurso é habilitado por padrão com a linha `cache=true` no seu arquivo de configuração *dnscrypt-proxy*

É recomendado executar o *dnscrypt-proxy* como um encaminhador para um cache DNS local, se não estiver usando o recurso de cache *dnscrypt-proxy*; caso contrário, todas as consultas farão um retorno para o resolvedor upstream. Qualquer programa de cache DNS local deve funcionar. Além de configurar o *dnscrypt-proxy*, você deve configurar o seu programa de cache DNS local.

#### Alterar a porta

Para encaminhar consultas de um cache DNS local, o *dnscrypt-proxy* deve escutar em uma porta diferente do padrão `53`, já que o próprio cache DNS precisa escutar `53` e consultar *dnscrypt-proxy* em uma porta diferente. O número de porta `53000` é usado como um exemplo nesta seção. Neste exemplo, o número da porta é maior que 1024, portanto, o *dnscrypt-proxy* não precisa ser executado pelo root.

Existem dois métodos para alterar a porta padrão:

**Método do soquete**

[Edite](/index.php/Edite "Edite") `dnscrypt-proxy.socket` como o seguinte conteúdo:

```
[Socket]
ListenStream=
ListenDatagram=
ListenStream=127.0.0.1:53000
ListenStream=[::1]:53000
ListenDatagram=127.0.0.1:53000
ListenDatagram=[::1]:53000

```

Quando as consultas são encaminhadas do cache DNS local para `53000`, `dnscrypt-proxy.socket` vai iniciar `dnscrypt-proxy.service`.

**Método do serviço**

Edite a opção `listen_addresses` em `/etc/dnscrypt-proxy/dnscrypt-proxy.toml` com o seguinte:

```
listen_addresses = ['127.0.0.1:53000', '[::1]:53000']

```

#### Exemplo de configurações de cache de DNS local

As seguintes configurações devem funcionar com *dnscrypt-proxy* e assumir que ele está escutando na porta `53000`.

##### Unbound

Configure [Unbound](/index.php/Unbound "Unbound") ao seu gosto (em particular, veja [Unbound#Local DNS server](/index.php/Unbound#Local_DNS_server "Unbound")) e adicione as seguintes linhas ao final da seção `server` em `/etc/unbound/unbound.conf`:

```
  do-not-query-localhost: no
forward-zone:
  name: "."
  forward-addr: ::1@53000
  forward-addr: 127.0.0.1@53000

```

**Dica:** Se você estiver configurando um servidor, adicione `interface: 0.0.0.0@53` e `access-control: *sua-rede*/*máscara-de-sub-rede* allow` dentro a seção `server:` para que os outros computadores possam se conectar ao servidor. Um cliente deve ser configurado com `nameserver *endereço-de-seu-servidor*` em `/etc/resolv.conf`.

[Reinicie](/index.php/Reinicie "Reinicie") `unbound.service` para aplicar as alterações.

##### dnsmasq

Configure o dnsmasq como um [cache DNS local](/index.php/Dnsmasq#DNS_server "Dnsmasq"). A configuração básica para trabalhar com *dnscrypt-proxy*:

 `/etc/dnsmasq.conf` 
```
no-resolv
server=::1#53000
server=127.0.0.1#53000
listen-address=::1,127.0.0.1
```

Se você configurou o *dnscrypt-proxy* para usar um resolvedor com a validação [DNSSEC](/index.php/DNSSEC_(Portugu%C3%AAs) "DNSSEC (Português)") ativada, certifique-se de ativá-lo também no dnsmasq:

 `/etc/dnsmasq.conf` 
```
conf-file=/usr/share/dnsmasq/trust-anchors.conf
dnssec
dnssec-check-unsigned
```

Reinicie `dnsmasq.service` para aplicar as configurações.

##### pdnsd

Instale o [pdnsd](/index.php/Pdnsd "Pdnsd"). Uma configuração básica para trabalhar com o *dnscrypt-proxy* é:

 `/etc/pdnsd.conf` 
```
global {
    perm_cache = 1024;
    cache_dir = "/var/cache/pdnsd";
    run_as = "pdnsd";
    server_ip = 127.0.0.1;
    status_ctl = on;
    query_method = udp_tcp;
    min_ttl = 15m;       # Retain cached entries at least 15 minutes.
    max_ttl = 1w;        # One week.
    timeout = 10;        # Global timeout option (10 seconds).
    neg_domain_pol = on;
    udpbufsize = 1024;   # Upper limit on the size of UDP messages.
}

server {
    label = "dnscrypt-proxy";
    ip = 127.0.0.1;
    port = 53000;
    timeout = 4;
    proxy_only = on;
}

source {
    owner = localhost;
    file = "/etc/hosts";
}
```

Reinicie `pdnsd.service` para aplicar as configurações.

### Sandboxing

[Edite](/index.php/Edite "Edite") o `dnscrypt-proxy.service` para incluir as seguintes linhas:

```
[Service]
CapabilityBoundingSet=CAP_IPC_LOCK CAP_SETGID CAP_SETUID CAP_NET_BIND_SERVICE
ProtectSystem=strict
ProtectHome=true
ProtectKernelTunables=true
ProtectKernelModules=true
ProtectControlGroups=true
PrivateTmp=true
PrivateDevices=true
MemoryDenyWriteExecute=true
NoNewPrivileges=true
RestrictRealtime=true
RestrictAddressFamilies=AF_INET AF_INET6
SystemCallArchitectures=native
SystemCallFilter=~@clock @cpu-emulation @debug @keyring @ipc @module @mount @obsolete @raw-io

```

Veja [systemd.exec(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.exec.5) e [Systemd (Português)#Usando ambientes de aplicativos em sandbox](/index.php/Systemd_(Portugu%C3%AAs)#Usando_ambientes_de_aplicativos_em_sandbox "Systemd (Português)") para mais informações.

### Habilitar EDNS0

[Extension Mechanisms for DNS](https://en.wikipedia.org/wiki/Extension_mechanisms_for_DNS "wikipedia:Extension mechanisms for DNS") que, junto com outras coisas, permitem que um cliente especifique quão grande uma resposta por UDP pode ser.

Adicione a linha a seguir ao `/etc/resolv.conf`:

```
options edns0

```

Você também pode querer acrescentar o seguinte ao `/etc/dnscrypt-proxy.conf`:

```
EDNSPayloadSize *bytes*

```

sendo *bytes* um número de bytes, com valor padrão de **1252** e com valores máximos até **4096** bytes sendo supostamente seguros. Um valor abaixo ou igual a **512** bytes desativará este mecanismo, a menos que um cliente envie um pacote com uma seção OPT fornecendo um tamanho de carga útil.

#### Testar EDNS0

Use o [Servidor de teste de tamanho de resposta do DNS](https://www.dns-oarc.net/oarc/services/replysizetest), use a ferramenta de linha de comando *drill* para emitir uma consulta TXT para o nome *rs.dns-oarc.net*:

```
$ drill rs.dns-oarc.net TXT

```

Caso haja suporte a **EDNS0**, a "answer section" da saída deve ser parecer com isso:

```
rst.x3827.rs.dns-oarc.net.
rst.x4049.x3827.rs.dns-oarc.net.
rst.x4055.x4049.x3827.rs.dns-oarc.net.
"2a00:d880:3:1::a6c1:2e89 DNS reply size limit is at least 4055 bytes"
"2a00:d880:3:1::a6c1:2e89 sent EDNS buffer size 4096"

```