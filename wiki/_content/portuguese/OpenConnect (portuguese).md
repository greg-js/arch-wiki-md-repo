**Status de tradução:** Esse artigo é uma tradução de [OpenConnect](/index.php/OpenConnect "OpenConnect"). Data da última tradução: 2019-03-20\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=OpenConnect&diff=0&oldid=569293) na versão em inglês.

[OpenConnect](http://www.infradead.org/openconnect/) é um cliente para o [AnyConnect SSL VPN](https://www.cisco.com/go/asm) da Cisco e o [Pulse Connect Secure](/index.php/Pulse_Connect_Secure "Pulse Connect Secure") da Pulse Secure.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Uso](#Uso)
    *   [2.1 Cliente Juniper Pulse](#Cliente_Juniper_Pulse)
    *   [2.2 Roteamento dividido](#Roteamento_dividido)
*   [3 Integração](#Integração)
    *   [3.1 NetworkManager](#NetworkManager)
    *   [3.2 netctl](#netctl)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [openconnect](https://www.archlinux.org/packages/?name=openconnect).

## Uso

Veja [openconnect(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/openconnect.8). Basta executar *openconnect* como root e inserir seu nome de usuário e senha quando solicitado:

```
# openconnect *vpnserver*

```

Invocação mais avançada com nome de usuário e senha. Insira a senha após executar o comando.

```
# openconnect -u *user* --passwd-on-stdin *vpnserver*

```

Muitas vezes, o provedor de VPN oferece diferentes grupos de autenticação para diferentes configurações de acesso, como, por exemplo, para um túnel completo ou uma conexão de túnel dividida. Para mostrar os diferentes grupos de autenticação oferecidos e obter mais informações sobre a conexão com o servidor em geral, use:

```
# openconnect --authenticate *servidorvpn*

```

#### Cliente Juniper Pulse

Para conectar a um servidor [Pulse Connect Secure](/index.php/Pulse_Connect_Secure "Pulse Connect Secure"), você precisa saber a SHA-1 de seu certificado.

```
# openconnect --servercert=sha1:<HASH> --authgroup="single-Factor Pulse Clients" --protocol=nc <ENDEREÇO_SERVIDOR_VPN>/dana-na/auth/url_6/welcome.cgi --pid-file="/var/run/work-vpn.pid" --user=<NOME_DE_USUÁRIO>

```

#### Roteamento dividido

O roteamento dividido pode ser obtido usando-se [vpn-slice-git](https://aur.archlinux.org/packages/vpn-slice-git/) no lugar do *vpnc-script*, para que você possa acessar seletivamente os hosts através da VPN, mas permanecer em sua própria LAN. Exemplo:

```
   sh
   $ sudo openconnect gateway.bigcorp.com -u user1234 \
       -s 'vpn-slice 192.168.1.0/24 hostname1 alias2=alias2.bigcorp.com=192.168.1.43'
   $ cat /etc/hosts
   ...
   192.168.1.1 dns0.tun0					# vpn-slice-tun0 AUTOCREATED
   192.168.1.2 dns1.tun0					# vpn-slice-tun0 AUTOCREATED
   192.168.1.57 hostname1 hostname1.bigcorp.com		# vpn-slice-tun0 AUTOCREATED
   192.168.1.43 alias2 alias2.bigcorp.com		# vpn-slice-tun0 AUTOCREATED

```

## Integração

### NetworkManager

[Instale](/index.php/Instale "Instale") o pacote [networkmanager-openconnect](https://www.archlinux.org/packages/?name=networkmanager-openconnect). Então, configure e conecte com o *nm-applet* (utilitário de área de notificação do NetworkManager de [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet)) ou utilitário similar. Após a instalação, [reinicie](/index.php/Reinicie "Reinicie") o `NetworkManager.service`.

Veja [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") para detalhes.

### netctl

Um [netctl.profile(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.profile.5) simples de `tuntap` pode ser usado para integrar o OpenConnect no fluxo de trabalho normal do [Netctl](/index.php/Netctl "Netctl"). Por exemplo:

 `/etc/netctl/vpn` 
```
Description='VPN'
Interface=vpn
Connection=tuntap
Mode=tun
#User=root
#Group=root

BindsToInterfaces=(enp0s25 wlp2s0)
IP=no

PIDFILE=/run/openconnect_${Interface}.pid
SERVER=vpn.example.net
AUTHGROUP='<GRUPO_DE_AUTH>'
LOCAL_USERNAME=<NOME_DE_USUÁRIO_LOCAL>
REMOTE_USERNAME=<NOME_DE_USUÁRIO_VPN>
# Assuming the use of pass(1): 
PASSWORD_CMD="su ${LOCAL_USERNAME} -c \"pass ${REMOTE_USERNAME} | head -n 1\""

ExecUpPost="${PASSWORD_CMD} | /usr/bin/openconnect --background --pid-file=${PIDFILE} --interface='${Interface}' --authgroup='${AUTHGROUP}' --user='${REMOTE_USERNAME}' --passwd-on-stdin ${SERVER}"
ExecDownPre="kill -INT $(cat ${PIDFILE}) ; resolvconf -d ${Interface} ; ip link delete ${Interface}"

```

Isso permite uma execução como:

```
$ netctl start vpn
$ netctl restart vpn
$ netctl stop vpn

```

Observe que isso depende de `LOCAL_USERNAME` ter um [gpg-agent](/index.php/GnuPG#gpg-agent "GnuPG") em execução, com a senha para a chave PGP já em cache.

Se uma consulta interativa do [pass](/index.php/Pass "Pass") for desejado, use a seguinte linha para `PASSWORD_CMD`:

```
DISPLAY=":0"
PASSWORD_CMD="su ${LOCAL_USERNAME} -c \"DISPLAY=${DISPLAY} pass ${REMOTE_USERNAME} | head -n 1\""

```

Ajuste a variável `DISPLAY` conforme necessário.