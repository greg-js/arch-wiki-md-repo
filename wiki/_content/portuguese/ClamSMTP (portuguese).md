**Status de tradução:** Esse artigo é uma tradução de [ClamSMTP](/index.php/ClamSMTP "ClamSMTP"). Data da última tradução: 2018-10-31\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=ClamSMTP&diff=0&oldid=549013) na versão em inglês.

[ClamSMTP](http://thewalter.net/stef/software/clamsmtp/) é uma ferramenta de filtragem de vírus muito simples para qualquer servidor SMTP. É muito útil com o MTA do Postfix, portanto, o artigo a seguir se aplica a isso e fornece um exemplo de uma configuração simples.

Os requisitos básicos são uma instalação do [Postfix](/index.php/Postfix "Postfix") de trabalho com usuários configurados e um daemon [ClamAV](/index.php/ClamAV_(Portugu%C3%AAs) "ClamAV (Português)") em funcionamento, portanto, certifique-se de tê-los instalado e configurado corretamente.

## Contents

*   [1 Instalação](#Instalação)
*   [2 Configuração](#Configuração)
    *   [2.1 CLAMSMTP](#CLAMSMTP)
    *   [2.2 CLAMAV](#CLAMAV)
    *   [2.3 POSTFIX](#POSTFIX)
*   [3 Teste](#Teste)
*   [4 Veja também](#Veja_também)

## Instalação

Antes de instalar o Clamsmtp, instale e configure o Postfix, crie usuários para o seu servidor SMTP e teste se ele está funcionando. Instale o Clamav e teste-o também.

Se as duas ferramentas funcionarem bem, [instale](/index.php/Instale "Instale") o [clamsmtp](https://aur.archlinux.org/packages/clamsmtp/).

## Configuração

### CLAMSMTP

Vamos ver `/etc/conf.d/clamsmtp`. Primeiro, altere a linha:

```
START_CLAMSMTP="no" 

```

para

```
START_CLAMSMTP="yes"

```

Agora, vamos configurar o daemon, editando `/etc/clamav/clamsmtpd.conf`. Você pode apagar o arquivo original ou simplesmente fazer um backup dele. Crie um novo arquivo com esse conteúdo:

```
# Um arquivo de configuração clamsmtpd simples

OutAddress: 10025 
Listen: 127.0.0.1:10026 
TempDirectory: /var/spool/clamsmtp
User: clamav

```

O Clamsmtp funciona como um daemon. O fluxo de trabalho é simples, ele escuta em uma porta especificada em seu arquivo de configuração, pega os e-mails, os escaneia via Clamav e, em seguida, os envia de volta para o Postfix por meio de outra porta.Aqui, o daemon escutará na porta 10026, depois escaneia os e-mails como usuário clamav e os envia de volta para o Postfix na porta 10025.

Em seguida, criamos o cache para clamsmtp por:

```
mkdir /var/spool/clamsmtp
chown clamav:clamav /var/spool/clamsmtp

```

(Por algum motivo, o TempDirectory padrão: `/tmp` retorna erros de permissão )

### CLAMAV

verifique seu `/etc/clamav/clamd.conf` e descomente a linha (normalmente, isso já foi feito):

```
#ScanMail yes

```

para

```
ScanMail yes

```

### POSTFIX

Agora, temos que configurar o Postfix para trabalhar em conjunto com o Clamsmtp. Edite `/etc/postfix/main.cf` e adicione estas duas linhas ao final do arquivo:

```
content_filter = scan:127.0.0.1:10026 
receive_override_options = no_address_mappings 

```

Postfix enviará e-mails para localhost na porta 10026.

Edite `/etc/postfix/master.cf`:

```
scan      unix  -       -       n       -       16      smtp 
        -o smtp_send_xforward_command=yes 
# For injecting mail back into postfix from the filter 
127.0.0.1:10025 inet  n -       n       -       16      smtpd 
       -o content_filter= 
       -o receive_override_options=no_unknown_recipient_checks,no_header_body_checks
       -o smtpd_helo_restrictions= 
       -o smtpd_client_restrictions= 
       -o smtpd_sender_restrictions= 
       -o smtpd_recipient_restrictions=permit_mynetworks,reject 
       -o mynetworks_style=host 
       -o smtpd_authorized_xforward_hosts=127.0.0.0/8 

```

As duas primeiras linhas criam o serviço “scan”, as outras se encarregam de aceitar o correio já escaneado do Clamsmtp da porta 10025 e de entregá-lo aos destinatários.

## Teste

Agora, teste seu servidor, [reiniciando](/index.php/Reinicia "Reinicia") os serviços `clamav`, `postfix` e `clamsmtp`.

Envie um e-mail para você mesmo, sem quaisquer vírus

Se nenhum e-mail chegar, verifique `/var/log/mail.log` por erros

Então, baixe um vírus de teste

```
wget [http://eicar.org/download/eicar_com.zip](http://eicar.org/download/eicar_com.zip)

```

e envie-o como um anexo.

Verifique o arquivo de log de seu servidor novamente, você deve obter alguma coisa similar a isso:

```
May 23 00:04:08 servername postfix/smtp[2415]: A9B941F911: to=<user@your.postfix.server>, relay=127.0.0.1[127.0.0.1]:10026, delay=0.13, delays=0.08/0/0.04/0, dsn=2.0.0, status=sent (250 Virus Detected; Discarded Email)

```

## Veja também

*   [http://memberwebs.com/stef/software/clamsmtp/](http://memberwebs.com/stef/software/clamsmtp/)
*   [http://www.postfix.org/](http://www.postfix.org/)