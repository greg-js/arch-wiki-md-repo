*Secure Shell* ou SSH é um protocolo de internet que permite a troca de informações por meio de um canal seguro entre dois computadores. A encriptação proporciona sigilo e integridade da informação. SSH usa criptografia de chave-pública para autenticar no computador remoto e permitir que o computador remoto autentique o usuário, se necessário.

SSH é tipicamente utilizado para logar em um computador remoto e executar comandos, mas ele também pode ser usado para *tunneling*. Transferência de arquivos pode ser feita usando os protocolos SFTP ou SCP.

Um servidor de SSH, por padrão, roda na porta 22\. Um cliente SSH geralmente é usado para estabelecer conexões com um servidor de sshd configurado para aceitar conexões remotas. Ambos estão presentes na maior parte dos sistemas operacionais modernos, incluindo GNU/Linux, MacOS X, Solaris e OpenVMS. Existem versões pagas, grátis e de código aberto.

## Contents

*   [1 OpenSSH](#OpenSSH)
    *   [1.1 Instalando o OpenSSH](#Instalando_o_OpenSSH)
    *   [1.2 Configurando o SSH](#Configurando_o_SSH)
        *   [1.2.1 Cliente](#Cliente)
        *   [1.2.2 Daemon](#Daemon)
        *   [1.2.3 Permitindo outros entrarem](#Permitindo_outros_entrarem)
    *   [1.3 Gerenciando o Daemon SSHD](#Gerenciando_o_Daemon_SSHD)
    *   [1.4 Conectando ao servidor](#Conectando_ao_servidor)
*   [2 Dicas e Truques](#Dicas_e_Truques)
    *   [2.1 Túnel criptografado](#T.C3.BAnel_criptografado)
        *   [2.1.1 Primeiro Passo: Iniciar a Conexão](#Primeiro_Passo:_Iniciar_a_Conex.C3.A3o)
        *   [2.1.2 Segundo Passo: Configure seu Navegador ( e/ou outros programas )](#Segundo_Passo:_Configure_seu_Navegador_.28_e.2Fou_outros_programas_.29)
    *   [2.2 Encaminhamento X11](#Encaminhamento_X11)
    *   [2.3 Acelerando o SSH](#Acelerando_o_SSH)
        *   [2.3.1 Resolução de Problemas](#Resolu.C3.A7.C3.A3o_de_Problemas)
    *   [2.4 Montando um Sistema de Arquivos Remoto com SSHFS](#Montando_um_Sistema_de_Arquivos_Remoto_com_SSHFS)
    *   [2.5 Mantendo a Sessão Ativa](#Mantendo_a_Sess.C3.A3o_Ativa)
    *   [2.6 Salvar os dados da conexão em .ssh/config](#Salvar_os_dados_da_conex.C3.A3o_em_.ssh.2Fconfig)

# OpenSSH

O OpenSSH (OpenBSD Secure Shell) é um conjunto de programas de computador que provê sessões de comunicação criptografada sobre uma rede de computadores utilizando o protocolo ssh. Ele foi criado como alternativa de código aberto à suite de aplicativos proprietários de Shell Seguro ( do inglês: Secure Shell ) oferecida pela SSH Communications Security. o OpenSSH é desenvolvido como parte do projeto OpenBSD, o qual é liderado por Theo de Raadt.

O OpenSSH é ocasionalmente confundido com o OpenSSL devido aos nomes parecidos; embora os projetos tenham propósitos diferentes e sejam desenvolvidos por times diferentes, os nomes similares surgiram de objetivos similares.

## Instalando o OpenSSH

```
# pacman -S openssh

```

## Configurando o SSH

### Cliente

O arquivo de configuração do cliente SSH pode ser encontrado e editado em `/etc/ssh/ssh_config`.

Um exemplo de configuração:

 `/etc/ssh/ssh_config` 
```
#       $OpenBSD: ssh_config,v 1.25 2009/02/17 01:28:32 djm Exp $

# This is the ssh client system-wide configuration file.  See
# ssh_config(5) for more information.  This file provides defaults for
# users, and the values can be changed in per-user configuration files
# or on the command line.

# Configuration data is parsed as follows:
#  1\. command line options
#  2\. user-specific file
#  3\. system-wide file
# Any configuration value is only changed the first time it is set.
# Thus, host-specific definitions should be at the beginning of the
# configuration file, and defaults at the end.

# Site-wide defaults for some commonly used options.  For a comprehensive
# list of available options, their meanings and defaults, please see the
# ssh_config(5) man page.

Host *
#   ForwardAgent no
#   ForwardX11 no
#   RhostsRSAAuthentication no
#   RSAAuthentication yes
#   PasswordAuthentication yes
#   HostbasedAuthentication no
#   GSSAPIAuthentication no
#   GSSAPIDelegateCredentials no
#   BatchMode no
#   CheckHostIP yes
#   AddressFamily any
#   ConnectTimeout 0
#   StrictHostKeyChecking ask
#   IdentityFile ~/.ssh/identity
#   IdentityFile ~/.ssh/id_rsa
#   IdentityFile ~/.ssh/id_dsa
#   Port 22
#   Protocol 2,1
#   Cipher 3des
#   Ciphers aes128-ctr,aes192-ctr,aes256-ctr,arcfour256,arcfour128,aes128-cbc,3des-cbc
#   MACs hmac-md5,hmac-sha1,umac-64@openssh.com,hmac-ripemd160
#   EscapeChar ~
#   Tunnel no
#   TunnelDevice any:any
#   PermitLocalCommand no
#   VisualHostKey no
HashKnownHosts yes
StrictHostKeyChecking ask
```

É recomendado alterar a linha do Protocolo para:

```
Protocol 2

```

Dessa forma, apenas o protocolo 2 será utilizado, visto que a protocolo 1 é considerado inseguro.

### Daemon

O Arquivo de configuração do daemon SSH pode ser encontrado e editado em `/etc/ssh/ssh**d**_config`.

Um exemplo de configuração:

 `/etc/ssh/sshd_config` 
```
#	$OpenBSD: sshd_config,v 1.75 2007/03/19 01:01:29 djm Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options change a
# default value.

#Port 22
#Protocol 2,1
ListenAddress 0.0.0.0
#ListenAddress ::

# HostKey for protocol version 1
#HostKey /etc/ssh/ssh*host*key
# HostKeys for protocol version 2
#HostKey /etc/ssh/ssh*host*rsa_key
#HostKey /etc/ssh/ssh*host*dsa_key

# Lifetime and size of ephemeral version 1 server key
#KeyRegenerationInterval 1h
#ServerKeyBits 768

# Logging
#obsoletes ~QuietMode and ~FascistLogging
#SyslogFacility AUTH
#LogLevel INFO

# Authentication:

#LoginGraceTime 2m
#PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6

#RSAAuthentication yes
#PubkeyAuthentication yes
#AuthorizedKeysFile     .ssh/authorized_keys

# For this to work you will also need host keys in /etc/ssh/ssh*known*hosts
#RhostsRSAAuthentication no
# similar for protocol version 2
#HostbasedAuthentication no
# Change to yes if you don't trust ~/.ssh/known_hosts for
# RhostsRSAAuthentication and HostbasedAuthentication
#IgnoreUserKnownHosts no
# Don't read the user's ~/.rhosts and ~/.shosts files
#IgnoreRhosts yes

# To disable tunneled clear text passwords, change to no here!
#PasswordAuthentication yes
#PermitEmptyPasswords no

# Change to no to disable s/key passwords
#ChallengeResponseAuthentication yes

# Kerberos options
#KerberosAuthentication no
#KerberosOrLocalPasswd yes
#KerberosTicketCleanup yes
#KerberosGetAFSToken no

# GSSAPI options
#GSSAPIAuthentication no
#GSSAPICleanupCredentials yes

# Set this to 'yes' to enable PAM authentication, account processing,
# and session processing. If this is enabled, PAM authentication will
# be allowed through the ~ChallengeResponseAuthentication mechanism.
# Depending on your PAM configuration, this may bypass the setting of
# PasswordAuthentication, ~PermitEmptyPasswords, and
# "PermitRootLogin without-password". If you just want the PAM account and
# session checks to run without PAM authentication, then enable this but set
# ChallengeResponseAuthentication=no
#UsePAM no

#AllowTcpForwarding yes
#GatewayPorts no
#X11Forwarding no
#X11DisplayOffset 10
#X11UseLocalhost yes
#PrintMotd yes
#PrintLastLog yes
#TCPKeepAlive yes
#UseLogin no
#UsePrivilegeSeparation yes
#PermitUserEnvironment no
#Compression yes
#ClientAliveInterval 0
#ClientAliveCountMax 3
#UseDNS yes
#PidFile /var/run/sshd.pid
#MaxStartups 10

# no default banner path
#Banner /some/path

# override default of no subsystems
Subsystem       sftp    /usr/lib/ssh/sftp-server
```

Para permitir acesso apenas por alguns usuários, adicione a seguinte linha:

```
AllowUsers    user1 user2

```

Você deve querer mudar algumas linhas para que pareçam com as seguintes:

```
Protocol 2
.
.
.
LoginGraceTime 120
.
.
.
PermitRootLogin no # (put yes here if you want root login)

```

Você pode também descomentar a opção BANNER e editar `/etc/issue` para uma mensagem de boas vindas.

**Tip:** Você deve querer alterar a porta padrão de 22 para qualquer porta alta (veja em inglês [security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity")).

Mesmo que a porta utilizada pelo ssh possa ser detectada por um port-scanner como o nmap, alterando-a irá reduzir o número de entradas nos logs por tentativas automatizadas de acesso.pts.

**Tip:** Desativando inteiramente logins por senha pode melhorar sua segurança, desde que cada usuário com acesso ao servidor necessitará criar chaves ssh. (veja em inglês [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys")).
 `/etc/ssh/sshd_config` 
```
PasswordAuthentication no
ChallengeResponseAuthentication no
```

### Permitindo outros entrarem

**Note:** Você tem que ajustar esse arquivo para acessar sua maquina remotamente visto que ele se encontra vazio por padrão

Para permitir que outra pessoa conecte via ssh a sua maquina você precisa ajustar o arquivo `/etc/hosts.allow`, e adicionar o seguinte:

```
# Permite qualquer um conectar a você
sshd: ALL

# Ou, você pode restringir certos ips.
sshd: 192.168.0.1

# ou restringir uma rede de ips
sshd: 10.0.0.0/255.255.255.0

# ou restringir o ip por um padrão
sshd: 192.168.1.

```

Agora você deve checar o arquivo `/etc/hosts.deny` pela seguinte linha, e ter certeza que ela está dessa forma:

```
ALL: ALL

```

É isso. Você pode sair e outros devem conseguir entrar via ssh :).

Para utilizar as novas configurações, reinicie o daemon (as root):

```
# /etc/rc.d/sshd restart

```

## Gerenciando o Daemon SSHD

Apenas adicione sshd à seção "DAEMON" do seu arquivo `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`:

```
DAEMONS=(... ... **sshd** ... ...)

```

Para iniciar/reiniciar/parar o daemon, use o seguinte:

```
# /etc/rc.d/sshd {start|stop|restart}

```

## Conectando ao servidor

Para conectar ao servidor, execute:

```
$ ssh -p port user@server-address

```

# Dicas e Truques

## Túnel criptografado

Isso é muito útil para usuário de notebook conectado a várias redes inseguras. A única coisa que você precisa é um servidor ssh sendo executado em alguma localização segura, como sua casa ou trabalho. Pode ser util fazer uso de um serviço de DNS dinâmico como [DynDNS](http://www.dyndns.org/) assim você não precisa lembrar o seu endereço IP.

### Primeiro Passo: Iniciar a Conexão

Você tem apenas que executar esse único comando no seu terminal favorito para iniciar a conexão:

```
$ ssh -ND 4711 usuario@host

```

onde `"usuario"` é o seu usuário no servidor SSH executando em `"host"`. Ele irá pedir sua senha, e então você estará conectado! A opção `"N"` desabilita o "prompt" interativo, e a opção `"D"` especifica a porta local na qual ele ouvirá (você pode escolher qualquer numero de porta de sua preferência).

Uma forma de fazer isso mais facil é colocar um atalho no seu arquivo `~/.bashrc` da seguinte forma:

```
alias sshtunnel="ssh -ND 4711 -v user@host"

```

É interessante adicionar a opção de verbosidade `"-v"`, porque então você pode verificar que está realmente conectado pela saída. Agora você precisa executar apenas`"sshtunnel"`  :)

### Segundo Passo: Configure seu Navegador ( e/ou outros programas )

O passo acima é completamente inútil se você não configurar seu navegador ( ou outros programas) para usar o novo túnel. Desde que a versão atual do SSH suporta SOCKS4 e SOCKS5, você pode usar qualquer um deles.

*   Para o Firefox:*Editar → Preferências → Avançado → Rede → Configurar Conexão →*:

	Marque a opção *"Configuração manual de proxy"*, e digite "localhost" no campo*"SOCKS"*, e então o número da porta no campo seguinte (acima eu utilizei 4711).

*   Para o Chromium: você terá que configurar as variáveis de ambiente. Eu recomento adicionar as seguintes linhas ao seu .bashrc:

```
   function secure_chromium {
       port=4711
       export SOCKS_SERVER=localhost:$port
       export SOCKS_VERSION=5
       chromium &
       exit
   }

```

Agora abra um terminal e faça:

```
   $ secure_chromium

```

Aproveite o seu túnel seguro!

## Encaminhamento X11

Para executar aplicativos gráficos através de uma conexão SSH você pode habilitar o "X11 forwarding". Uma opção precisa ser definida nos arquivos de configuração do servidor e do cliente (aqui "cliente" quer dizer o seu computador onde o servidor X11 é executado, e você irá executar aplicativos X no "servidor").

Instalando xorg-xauth no servidor:

```
# pacman -S xorg-xauth

```

*   Habilite a opção **AllowTcpForwarding** no arquivo `sshd_config` no **server**.
*   Habilite a opção **X11Forwarding** no arquivo `sshd_config` no **server**.
*   Defina a opção **X11DisplayOffset** no arquivo `sshd_config` no **server** para 10.
*   Habilite a opção **X11UseLocalhost** no arquivo `sshd_config` no **server**.
*   Habilite a opção **ForwardX11** no arquivo `ssh_config` no **client**.

Para usar o encaminhamento, conecte no seu servidor pelo ssh:

```
# ssh -X -p port user@server-address

```

Se vocẽ receber erros ao tentar executar um aplicativo gráfico, tente usar o encaminhamento confiável então:

```
# ssh -Y -p port user@server-address

```

Agora você pode iniciar qualquer aplicativo X no servidor remoto, a saída será redirecionada para a sua sessão local:

```
# xclock

```

Se você receber erros "Cannot open display", tente o seguinte comando como root:

```
$ xhost +

```

o comando acima irá permitir que qualquer um encaminhe aplicativos X11\. Para restringir o encaminhamento a um determinado host:

```
$ xhost +hostname

```

onde hostname é o nome do host ao qual você quer encaminhar. Digite "man xhost" para mais detalhes.

Seja cuidadoso com alguns aplicativos que checam por uma instância na maquina local. O Firefox é um exemplo. Feche o Firefox ou use o seguinte parâmetro de inicialização para iniciar uma instância na maquina local:

```
$ firefox -no-remote

```

## Acelerando o SSH

Você pode fazer todas as sessões ao mesmo host utilizarem uma única conexão, o que irá acelerar muito os logins subsequentes, ao adicionar a seguinte linha abaixo do host apropriado em `/etc/ssh/ssh_config`:

```
ControlMaster auto
ControlPath ~/.ssh/socket-%r@%h:%p

```

Alterando as cifras utilizadas pelo SSH para aquelas que requerem menos processamento pode melhorar a velocidade. Nesse aspecto as melhores escolhas são arcfour e blowfish-cbc. **Por favor, não faça isso a menos que saiba o que estás fazendo;arcfour tem várias vulnerabilidades conhecidas**. Para usá-las, execute o ssh com a opção `"c"`, assim:

```
# ssh -c arcfour,blowfish-cbc user@server-address

```

Para usá-las permanentemente, adicione a seguinte linha abaixo do host apropriado em `/etc/ssh/ssh_config`:

```
Ciphers arcfour,blowfish-cbc

```

Outra opção para melhorar a velocidade é ativar a compressão com a opção `"C"`. Uma solução permanente para isso é adicionar a seguinte linha abaixo do host apropriado em `/etc/ssh/ssh_config`:

```
Compression yes

```

O tempo de login pode ser reduzido utilizando a opção `"4"`, que pula a pesquisa em IPv6. Isso pode ser feito permanentemente adicionando a seguinte linha abaixo do host apropriado em `/etc/ssh/ssh_config`:

```
AddressFamily inet

```

Outra forma de fazer essas mudanças permanentes é criar um atalho em `~/.bashrc`:

```
alias ssh='ssh -C4c arcfour,blowfish-cbc'

```

### Resolução de Problemas

Certifique-se de que a variável DISPLAY está corretamente configurada no servidor remoto:

```
ssh -X user@server-address
server$ echo $DISPLAY
localhost:10.0
server$ telnet localhost 6010
localhost/6010: lookup failure: Temporary failure in name resolution   

```

isso pode ser resolvido adicionando localhost ao arquivo `/etc/hosts`.

## Montando um Sistema de Arquivos Remoto com SSHFS

Instale o sshfs

```
# pacman -S sshfs

```

Carregue o módulo Fuse para a memória

```
# modprobe fuse

```

Adicione fuse à lista de módulos no arquivo `/etc/rc.conf` para carregá-lo na inicialização do sistema.

Monte o diretório remoto usando sshfs

```
# mkdir ~/remote_folder
# sshfs USER@remote_server:/tmp ~/remote_folder

```

O comando acima irá fazer com que a pasta /tmp no servidor remoto seja montada como ~/remote_folder na maquina local. Copiando qualquer arquivo para essa pasta irá em cópia transparente através da rede usando SFTP. O mesmo ocorre quanto a edição, criação ou remoção de arquivos.

Quando terminarmos de utilizar o sistema de arquivos remoto, podemos desmontar o diretório remoto fazendo:

```
# fusermount -u ~/remote_folder

```

Se trabalharmos nessa pasta numa base diária, ele irá sabiamente adicionar à table de sistemas de arquivo `/etc/fstab`. Desse forma ele pode ser automaticamente montado pelo sistema durante a inicialização ou manualmente (se a opção `noauto` for escolhida) sem a necessidade de especificar a localização remota a cada vez. Aqui uma entrada de exemplo da tabela:

```
sshfs#USER@remote_server:/tmp /full/path/to/directory fuse    defaults,auto,allow_other    0 0

```

## Mantendo a Sessão Ativa

Sua sessão ssh irá desconectar automaticamente se permanecer ociosa. Para manter a conexão ativa adicione a seguinte linha ao arquivo `~/.ssh/config` ou para `/etc/ssh/ssh_config` no cliente.

```
ServerAliveInterval 120

```

Isso irá enviar um sinal "keep alive" para o servidor a cada 120 segundos.

Reciprocamente, para manter conexões de entrada ativas, você pode definir

```
ClientAliveInterval 120

```

(ou algum outro número maior que 0) no arquivo `/etc/ssh/sshd_config` no servidor.

## Salvar os dados da conexão em .ssh/config

Sempre que você quer conectar a um servidor, você normalmente precisa digitar ao menos o endereço e o seu usuário. Para evitar o trabalho de digitar os servidores que você regularmente conecta, você pode utilizar o arquivo `$HOME/.ssh/config` como mostrado no exemplo:

 `$HOME/.ssh/config` 
```
Host myserver
    HostName 123.123.123.123
    Port 12345
    User bob
Host other_server
    HostName test.something.org
    User alice
    CheckHostIP no
    Cipher blowfish

```

Agora vocẽ pode simplesmente conectar ao servidor usando o nome que você especificou:

```
$ ssh myserver

```

Para ver uma lista completa de possíveis opções, cheque a pagina de manual do ssh_config no seu sistema ou a [Documentação do ssh_config](http://www.openbsd.org/cgi-bin/man.cgi?query=ssh_config) no site official em inglês.