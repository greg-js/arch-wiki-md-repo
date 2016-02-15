[DNSCrypt](http://dnscrypt.org/) é um software que criptografa o tráfico DNS entre o usuário e o provedor DNS reverso e previne ataques de espionagem, falsificação ou _man-in-the-middle_.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Configução](#Configu.C3.A7.C3.A3o)
*   [3 Iniciando](#Iniciando)
*   [4 Dicas](#Dicas)
    *   [4.1 DNSCrypt com cache DNS local](#DNSCrypt_com_cache_DNS_local)
        *   [4.1.1 Configuração para Unbound](#Configura.C3.A7.C3.A3o_para_Unbound)
        *   [4.1.2 Configuração para dnsmasq](#Configura.C3.A7.C3.A3o_para_dnsmasq)
    *   [4.2 Enable EDNS0](#Enable_EDNS0)
        *   [4.2.1 Teste EDNS0](#Teste_EDNS0)

## Instalação

Instale [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy) dos [repositórios oficiais](/index.php/Official_repositories "Official repositories").

## Configução

**Dica:** Para configurar e escolher um provedor DNS reverso automaticamente use [dnscrypt-autoinstall](https://aur.archlinux.org/packages/dnscrypt-autoinstall/) do [AUR](/index.php/Arch_User_Repository_(Portugu%C3%AAs) "Arch User Repository (Português)").

Por padrão, _dnscrypt-proxy_ é pré-configurado em `/etc/conf.d/dnscrypt-proxy` e serve de parâmetro de configuração para `dnscrypt-proxy.service` para aceitar requisições em `127.0.0.1` para um servidor [OpenDNS](https://opendns.com). Veja esta [lista de servidores DNS reverso](https://github.com/jedisct1/dnscrypt-proxy/blob/master/dnscrypt-resolvers.csv) para alternativas.

Com esta configuração será necessário alterar seu arquivo `resolv.conf` e alterar sua atual lista de DNS reverso por _localhost_:

```
nameserver 127.0.0.1

```

Você deve prevenir que outros programas reescrevam-no, veja [resolv.conf#Preserve DNS settings](/index.php/Resolv.conf#Preserve_DNS_settings "Resolv.conf") (_em inglês_) para detalhes.

## Iniciando

Disponível como um serviço [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"): `dnscrypt-proxy.service`

## Dicas

### DNSCrypt com cache DNS local

É recomendado executar DNSCrypt com cache DNS, caso contrário cada requisição será enviada ao servidor DNS reverso. Importante observar que se o Domínio mudar de endereço durante o tempo de vida do cache o registro local estará desatualizado. Abaixo temos dois exemplos de configuração para [Unbound](/index.php/Unbound "Unbound") e [dnsmasq](/index.php/Dnsmasq_(Portugu%C3%AAs) "Dnsmasq (Português)").

#### Configuração para Unbound

Configure [Unbound](/index.php/Unbound "Unbound") e adicione as seguintes linhas no fim da seção `server` em `/etc/unbound/unbound.conf`:

**Dica:** Observe que `/etc/resolv.conf` deve estar configurado com `nameserver 127.0.0.1`, mais informações para [configurar /etc/resolv.conf para usar servidor DNS local](/index.php/Unbound#Set_.2Fetc.2Fresolv.conf_to_use_the_local_DNS_server "Unbound")

```
do-not-query-localhost: no
forward-zone:
  name: "."
  forward-addr: 127.0.0.1@2053

```

Inicie o serviço [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") `unbound.service`. Então configure DNSCrypt para combinar o novo IP e porta `forward-zone` do Unbound em `/etc/conf.d/dnscrypt-proxy`:

```
DNSCRYPT_LOCALIP=127.0.0.1
DNSCRYPT_LOCALPORT=2053

```

**Nota:** DNSCrypt precisa ser reiniciado primeiro que Unbound, então inclua `unbound.service` numa linha `Before=` na seção `[Unit]` de `dnscrypt-proxy.service`

Reinicie `dnscrypt-proxy.service` e `unbound.service` para que as modificações tenham efeito.

#### Configuração para dnsmasq

Configure dnsmasq como [cache local DNS](/index.php/Dnsmasq_(Portugu%C3%AAs)#Configura.C3.A7.C3.A3o_do_cache_DNS "Dnsmasq (Português)"). Segue configuração básica:

 `/etc/dnsmasq.conf` 

```
no-resolv
server=127.0.0.2#2053
listen-address=127.0.0.1
```

Se você configurou DNSCrypt para usar DNS reverso com validação DNSSEC habilitada, certifique de habilitar, também, em dnsmasq:

 `/etc/dnsmasq.conf`  `proxy-dnssec` 

Configure DNSCrypt `DNSCRYPT_LOCALIP` apontando para o servidor dnsmasq `127.0.0.2` e `DNSCRYPT_LOCALPORT` para sua respectiva porta (também no servidor dnsmasq) `#2053`:

 `/etc/conf.d/dnscrypt-proxy` 

```
DNSCRYPT_LOCALIP=127.0.0.2
DNSCRYPT_LOCALPORT=2053
```

Reinicie `dnscrypt-proxy.service` e `dnsmasq.service` para que as modificações tenham efeito.

### Enable EDNS0

[Extension Mechanisms for DNS](https://en.wikipedia.org/wiki/Extension_mechanisms_for_DNS "wikipedia:Extension mechanisms for DNS") (_inglês_) que, dentre outras coisas, permite a um cliente especificar o tamanho de um pacote de resposta sobre UDP.

Adicione o que se segue ao seu arquivo `/etc/resolv.conf`:

```
options edns0

```

Você talvez deseje adicionar o seguinte argumento a _dnscrypt-proxy_:

```
--edns-payload-size=<bytes>

```

O tamanho padrão seria **1252** bytes, com valores até **4096** bytes com suposta segurança.. Um valor inferior ou igual a **512** bytes desabilita este mecanismo ao menos que o cliente envie um pacote com um seção OPT especificando o tamanho do pacote.

#### Teste EDNS0

Faça uso da ferramenta [_DNS Reply Size Test Server_](https://www.dns-oarc.net/oarc/services/replysizetest%7C), use _dig_, uma ferramenta de linha de comando disponível com o pacote [dnsutils](https://www.archlinux.org/packages/?name=dnsutils) dos [repositórios oficiais](/index.php/Official_repositories "Official repositories"), para emitir uma consulta TXT para o nome _rs.dns-oarc.net_:

```
$ dig +short rs.dns-oarc.net txt

```

Com suporte ao **EDNS0**, a saída seria similar a isto:

```
rst.x3827.rs.dns-oarc.net.
rst.x4049.x3827.rs.dns-oarc.net.
rst.x4055.x4049.x3827.rs.dns-oarc.net.
"2a00:d880:3:1::a6c1:2e89 DNS reply size limit is at least 4055 bytes"
"2a00:d880:3:1::a6c1:2e89 sent EDNS buffer size 4096"

```