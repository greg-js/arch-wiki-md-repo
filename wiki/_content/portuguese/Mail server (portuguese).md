Um **servidor de e-mail** ou [agente de transferência de e-mail](https://en.wikipedia.org/wiki/pt:Mail_transfer_agent "wikipedia:pt:Mail transfer agent") (MTA) recebe e envia e-mails via [SMTP](https://en.wikipedia.org/wiki/pt:Simple_Mail_Transfer_Protocol "wikipedia:pt:Simple Mail Transfer Protocol"). E-mails recebidos e aceitos são então passados para um [agente de entrega de e-mail](https://en.wikipedia.org/wiki/Mail_delivery_agent "wikipedia:Mail delivery agent") (MDA), que armazena o e-mail em uma caixa de correio (geralmente nos formatos [mbox](https://en.wikipedia.org/wiki/mbox "wikipedia:mbox") ou [Maildir](https://en.wikipedia.org/wiki/Maildir "wikipedia:Maildir")). Se você quiser que os usuários possam acessar remotamente seus e-mails usando [clientes de e-mail](/index.php/Email_client "Email client") ou [agentes de recuperação de e-mail](/index.php/Category:Mail_retrieval_agents "Category:Mail retrieval agents"), será necessário executar um servidor [POP3](https://en.wikipedia.org/wiki/pt:Post_Office_Protocol "wikipedia:pt:Post Office Protocol") e/ou [IMAP](https://en.wikipedia.org/wiki/pt:Internet_Message_Access_Protocol "wikipedia:pt:Internet Message Access Protocol").

| Software | Pacote | [MTA](https://en.wikipedia.org/wiki/pt:MTA "wikipedia:pt:MTA") | [MDA](https://en.wikipedia.org/wiki/Mail_delivery_agent "wikipedia:Mail delivery agent") | [POP3](https://en.wikipedia.org/wiki/pt:Post_Office_Protocol "wikipedia:pt:Post Office Protocol") | [IMAP](https://en.wikipedia.org/wiki/pt:Internet_Message_Access_Protocol "wikipedia:pt:Internet Message Access Protocol") | [SPF](#Sender_Policy_Framework) |
| [Sendmail](/index.php/Sendmail "Sendmail") | [sendmail](https://aur.archlinux.org/packages/sendmail/) | Sim | Não | Não | Não | por meio do [Milter](https://en.wikipedia.org/wiki/Milter "wikipedia:Milter") |
| [Exim](/index.php/Exim "Exim") | [exim](https://www.archlinux.org/packages/?name=exim) | Sim | Sim | Não | Não | experimental[[1]](https://github.com/Exim/exim/wiki/SPF) |
| [OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD") | [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd) | Sim | Sim | Não | Não | Não |
| [Postfix](/index.php/Postfix "Postfix") | [postfix](https://www.archlinux.org/packages/?name=postfix) | Sim | Sim | Não | Não | Sim |
| [Courier](/index.php/Courier_Mail_Server "Courier Mail Server") | [courier-mta](https://aur.archlinux.org/packages/courier-mta/) | Sim | Sim | Sim | Sim | Sim |
| [Cyrus IMAP](https://en.wikipedia.org/wiki/pt:Cyrus_(IMAP) | [cyrus-imapd](https://aur.archlinux.org/packages/cyrus-imapd/) | Sim | Sim | Sim | Sim |  ? |
| [Dovecot](/index.php/Dovecot "Dovecot") | [dovecot](https://www.archlinux.org/packages/?name=dovecot) | Não | Sim | Sim | Sim |
| [UW IMAP](https://en.wikipedia.org/wiki/UW_IMAP "wikipedia:UW IMAP") | [imap](https://www.archlinux.org/packages/?name=imap) | Não | Sim | Sim | Sim |
| [fdm](/index.php/Fdm "Fdm") | [fdm](https://www.archlinux.org/packages/?name=fdm) | Não | Sim | Não | Não |
| [Procmail](/index.php/Procmail "Procmail") | [procmail](https://www.archlinux.org/packages/?name=procmail) | Não | Sim | Não | Não |

Veja também [Wikipedia:Comparison of e-mail servers](https://en.wikipedia.org/wiki/Comparison_of_e-mail_servers "wikipedia:Comparison of e-mail servers").

## Contents

*   [1 Registro MX](#Registro_MX)
*   [2 TLS](#TLS)
*   [3 Autenticação](#Autentica.C3.A7.C3.A3o)
    *   [3.1 Sender Policy Framework](#Sender_Policy_Framework)
    *   [3.2 Sender Rewriting Scheme](#Sender_Rewriting_Scheme)
    *   [3.3 DKIM](#DKIM)
*   [4 Sites de teste](#Sites_de_teste)
*   [5 Dicas e truques](#Dicas_e_truques)

## Registro MX

Se você quiser receber e-mails, precisará definir um [registro MX](https://en.wikipedia.org/wiki/pt:MX_record "wikipedia:pt:MX record"), ou *MX record*, do seu nome de domínio para apontar para o seu servidor de e-mail. Geralmente isso é feito a partir da interface de configuração do seu provedor de domínio.

Um registro de troca de e-mails (registro MX) é um tipo de registro de recurso no Sistema de Nomes de Domínio (DNS) que especifica um servidor de e-mails responsável por aceitar mensagens de email em nome do domínio de um destinatário.

Quando uma mensagem de e-mail é enviada pela Internet, o agente de transferência de e-mail de envio consulta o Sistema de Nome de Domínio para registros MX do nome de domínio de cada destinatário. Essa consulta retorna uma lista de nomes de host de servidores de troca de mensagens que aceitam emails de entrada para esse domínio e suas preferências. O agente de envio, em seguida, tenta estabelecer uma conexão SMTP com um desses servidores, começando com aquele com o menor número de preferência, entregando a mensagem ao primeiro servidor com o qual uma conexão pode ser feita.

**Nota:** Alguns servidores de e-mail não entregarão e-mails para você se seu registro MX apontar para um CNAME. Para obter melhores resultados, sempre aponte um registro MX para uma definição de registro. Para mais informações, veja, por exemplo, a [lista do Wikipédia com tipos de registros DNS](https://en.wikipedia.org/wiki/List_of_DNS_record_types "wikipedia:List of DNS record types").

## TLS

**Atenção:** Se você implementar [TLS](https://en.wikipedia.org/wiki/pt:Transport_Layer_Security "wikipedia:pt:Transport Layer Security"), certifique-se de seguir [TLS do lado do servidor](/index.php/Server-side_TLS "Server-side TLS") para evitar vulnerabilidades.

Para obter um certificado, veja [OpenSSL#Certificates](/index.php/OpenSSL#Certificates "OpenSSL").

## Autenticação

Há várias técnicas [autenticação por e-mail](https://en.wikipedia.org/wiki/Email_authentication "wikipedia:Email authentication").

### Sender Policy Framework

Do [Wikipédia](https://en.wikipedia.org/wiki/Sender_Policy_Framework "wikipedia:Sender Policy Framework"):

	**Sender Policy Framework** (**SPF**) é um protocolo de validação de e-mail projetado para detectar e bloquear falsificação de e-mail, fornecendo um mecanismo para permitir o recebimento de troca de e-mails para verificar se o e-mail recebido de um domínio vem de um endereço IP autorizado pelos administradores do domínio.

Para permitir que outros trocadores de e-mail validem e-mails aparentemente enviados de seu domínio, você precisa definir um registro DNS TXT, conforme explicado no [artigo da Wikipédia](https://en.wikipedia.org/wiki/pt:Sender_Policy_Framework "wikipedia:pt:Sender Policy Framework"). Para validar as mensagens recebidas usando o SPF, você precisa configurar seu servidor de e-mail para usar uma implementação SPF. Existem várias [implementações SPF](http://www.openspf.org/Implementations) disponíveis, [perl-mail-spf](https://www.archlinux.org/packages/?name=perl-mail-spf) e [perl-mail-spf-query](https://www.archlinux.org/packages/?name=perl-mail-spf-query) podem ser encontradas no repositórios oficiais.

*   Para [Sendmail](/index.php/Sendmail "Sendmail") [spfmilter-acme](https://aur.archlinux.org/packages/spfmilter-acme/) pode ser usado.
*   Para [Postfix](/index.php/Postfix "Postfix"), veja [Postfix#Sender Policy Framework](/index.php/Postfix#Sender_Policy_Framework "Postfix").
*   [Courier Mail Server](/index.php/Courier_Mail_Server "Courier Mail Server") oferece suporte nativamente a SPF.

Os seguintes sites permitem você validar seu registro SPF:

*   [SPF Record Checker](http://www.kitterman.com/spf/validate.html)
*   [SPF Email test](http://www.appmaildev.com/en/spf)

**Dica:** O SPF pode até ser útil para domínios não usados para enviar email. Publicar uma política como `v=spf1-all` faz com que qualquer servidor de email imponha e-mails de rejeição SPF do seu nome de domínio, evitando assim o uso indevido.

### Sender Rewriting Scheme

O [Sender Rewriting Scheme](https://en.wikipedia.org/wiki/Sender_Rewriting_Scheme "wikipedia:Sender Rewriting Scheme") (SRS) é um esquema seguro para permitir retornos encaminháveis para e-mails encaminhados no servidor sem quebrar a [Sender Policy Framework](#Sender_Policy_Framework).

Para [Postfix](/index.php/Postfix "Postfix"), veja [Postfix#Sender Rewriting Scheme](/index.php/Postfix#Sender_Rewriting_Scheme "Postfix").

### DKIM

[DomainKeys Identified Mail](https://en.wikipedia.org/wiki/DomainKeys_Identified_Mail "wikipedia:DomainKeys Identified Mail") (DKIM) é um método de autenticação de e-mail no nível do domínio projetado para detectar falsificação de e-mail.

A implementações DKIM disponíveis são [OpenDKIM](/index.php/OpenDKIM "OpenDKIM") e [dkimproxy](https://www.archlinux.org/packages/?name=dkimproxy).

## Sites de teste

Existem vários sites úteis que podem ajudá-lo a testar os registros DNS, a capacidade de entrega e o suporte à criptografia.

*   [https://mxtoolbox.com/](https://mxtoolbox.com/)
*   [http://ismyemailworking.com/](http://ismyemailworking.com/)
*   [https://www.mail-tester.com/](https://www.mail-tester.com/)
*   [https://www.checktls.com/](https://www.checktls.com/)
*   [https://pingability.com/zoneinfo.jsp](https://pingability.com/zoneinfo.jsp)

## Dicas e truques

A maioria dos servidores de e-mail pode ser configurada para remover os endereços IP dos usuários e os [agentes de usuário](https://en.wikipedia.org/wiki/User_agent "wikipedia:User agent") do e-mail de saída.

Extras disponíveis que geralmente podem ser integrados são:

*   [ClamAV](/index.php/ClamAV_(Portugu%C3%AAs) "ClamAV (Português)") para verificação de e-mails por vírus
*   [spamassassin](https://www.archlinux.org/packages/?name=spamassassin) para identificar e filtrar spam
*   [Sieve](https://en.wikipedia.org/wiki/Sieve_(mail_filtering_language) – uma linguagem de programação para filtrar e-mail
*   [webmail](https://en.wikipedia.org/wiki/pt:Webmail "wikipedia:pt:Webmail") como o [Roundcube](/index.php/Roundcube "Roundcube") ou o [Squirrelmail](/index.php/Squirrelmail "Squirrelmail")