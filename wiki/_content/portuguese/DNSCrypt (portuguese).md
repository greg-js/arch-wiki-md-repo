[DNSCrypt](http://dnscrypt.org/) é um software que criptografa o tráfico DNS entre o usuário e o provedor DNS reverso e previne ataques de espionagem, falsificação ou *man-in-the-middle*.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Configução](#Configu.C3.A7.C3.A3o)
    *   [2.1 Escolher resolvedor DNS](#Escolher_resolvedor_DNS)
    *   [2.2 Modificando o resolv.conf](#Modificando_o_resolv.conf)
    *   [2.3 Iniciando o serviço Systemd](#Iniciando_o_servi.C3.A7o_Systemd)
*   [3 Dicas](#Dicas)
    *   [3.1 DNSCrypt com cache DNS local](#DNSCrypt_com_cache_DNS_local)
        *   [3.1.1 Configuração para Unbound](#Configura.C3.A7.C3.A3o_para_Unbound)
        *   [3.1.2 Configuração para dnsmasq](#Configura.C3.A7.C3.A3o_para_dnsmasq)
    *   [3.2 Enable EDNS0](#Enable_EDNS0)
        *   [3.2.1 Teste EDNS0](#Teste_EDNS0)

## Instalação

Instale [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy) dos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais").

**Dica:** [dnscrypt-proxy-gui](https://aur.archlinux.org/packages/dnscrypt-proxy-gui/) fornece uma GUI escrita em QT para configurar o servidor DNS usado pelo DNSCrypt

## Configução

**Dica:** Um exemplo de arquivo de configuração, `/etc/dnscrypt-proxy.conf.example` é fornecido, mas note que o systemd substitui a opção `LocalAddress` por um arquivo socket.

Para configurar o dnscrypt-proxy, execute as seguintes etapas:

### Escolher resolvedor DNS

Escolha um resolvedor DNS no arquivo `/usr/share/dnscrypt-proxy/dnscrypt-resolvers.csv` e edit `/etc/dnscrypt-proxy.conf`, usando o nome curto da primeira coluna do arquivo csv, `Name`. Por exemplo, para selecionar *dnscrypt.eu-nl* como resolvedor DNS:

```
ResolverName dnscrypt.eu-nl

```

**Dica:**

*   Uma lista mais potencialmente mais atualizada está disponível diretamente na [página oficial](https://github.com/jedisct1/dnscrypt-proxy/blob/master/dnscrypt-resolvers.csv).
*   Nesta fase, você também pode adicionar um usuário não privilegiado para executar o dnscrypt. Veja [#dnscrypt runs with root privileges](#dnscrypt_runs_with_root_privileges).

### Modificando o resolv.conf

Depois de selecionar um resolvedor DNS do dnscrypt, modifique o arquivo [resolv.conf](/index.php/Resolv.conf_(Portugu%C3%AAs) "Resolv.conf (Português)") e substitua o conjunto atual de endereços para o endereço do *localhost*:

```
nameserver 127.0.0.1

```

outros programas podem substituir esta configuração. Veja [resolv.conf#Preserve DNS settings](/index.php/Resolv.conf#Preserve_DNS_settings "Resolv.conf") para mais detalhes.

### Iniciando o serviço Systemd

Finalmente, [inicie e habilite](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)") o `dnscrypt-proxy.service`

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

[Extension Mechanisms for DNS](https://en.wikipedia.org/wiki/Extension_mechanisms_for_DNS "wikipedia:Extension mechanisms for DNS") (*inglês*) que, dentre outras coisas, permite a um cliente especificar o tamanho de um pacote de resposta sobre UDP.

Adicione o que se segue ao seu arquivo `/etc/resolv.conf`:

```
options edns0

```

Você talvez deseje adicionar o seguinte argumento a *dnscrypt-proxy*:

```
--edns-payload-size=<bytes>

```

O tamanho padrão seria **1252** bytes, com valores até **4096** bytes com suposta segurança.. Um valor inferior ou igual a **512** bytes desabilita este mecanismo ao menos que o cliente envie um pacote com um seção OPT especificando o tamanho do pacote.

#### Teste EDNS0

Faça uso da ferramenta [*DNS Reply Size Test Server*](https://www.dns-oarc.net/oarc/services/replysizetest%7C), use *dig*, uma ferramenta de linha de comando disponível com o pacote [dnsutils](https://www.archlinux.org/packages/?name=dnsutils) dos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"), para emitir uma consulta TXT para o nome *rs.dns-oarc.net*:

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