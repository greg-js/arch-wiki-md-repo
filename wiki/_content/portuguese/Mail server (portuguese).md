**Status de tradução:** Esse artigo é uma tradução de [Mail server](/index.php/Mail_server "Mail server"). Data da última tradução: 2019-04-16\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Mail_server&diff=0&oldid=568443) na versão em inglês.

Um servidor de e-mail consiste em vários componentes. Um [agente de transferência de e-mail](https://en.wikipedia.org/wiki/pt:Mail_transfer_agent "wikipedia:pt:Mail transfer agent") (MTA) recebe e envia e-mails via [SMTP](https://en.wikipedia.org/wiki/pt:Simple_Mail_Transfer_Protocol "wikipedia:pt:Simple Mail Transfer Protocol"). E-mails recebidos e aceitos são então passados para um [agente de entrega de e-mail](https://en.wikipedia.org/wiki/Mail_delivery_agent "wikipedia:Mail delivery agent") (MDA), que armazena o e-mail em uma caixa de correio (geralmente nos formatos [mbox](https://en.wikipedia.org/wiki/mbox "wikipedia:mbox") ou [Maildir](https://en.wikipedia.org/wiki/Maildir "wikipedia:Maildir")). Se você quiser que os usuários possam acessar remotamente seus e-mails usando [clientes de e-mail](/index.php/Email_client "Email client") (MUA), será necessário executar um servidor [POP3](https://en.wikipedia.org/wiki/pt:Post_Office_Protocol "wikipedia:pt:Post Office Protocol") e/ou [IMAP](https://en.wikipedia.org/wiki/pt:Internet_Message_Access_Protocol "wikipedia:pt:Internet Message Access Protocol").

```
+---------+  SMTP  +---+   +---+                     +------------------+
|Outro MTA| <----> |MTA| --|MDA|-> Armazenamento <-- |Servidor POP3/IMAP|
+---------+        +---+   +---+                     +------------------+
                     ^                                       ^
                     |     SMTP        +---+                 |
                     +-----------------|MUA|-----------------+
                                       +---+

```

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Software](#Software)
    *   [1.1 Servidores POP3/IMAP](#Servidores_POP3/IMAP)
    *   [1.2 MDAs autônomos](#MDAs_autônomos)
*   [2 Portas](#Portas)
*   [3 Registro MX](#Registro_MX)
*   [4 TLS](#TLS)
*   [5 Autenticação](#Autenticação)
    *   [5.1 Sender Policy Framework](#Sender_Policy_Framework)
    *   [5.2 Sender Rewriting Scheme](#Sender_Rewriting_Scheme)
    *   [5.3 DKIM](#DKIM)
*   [6 Sites de teste](#Sites_de_teste)
*   [7 Dicas e truques](#Dicas_e_truques)

## Software

Todos esses softwares, exceto o Sendmail, incluem um agente de entrega de e-mail.

*   **[Exim](/index.php/Exim "Exim")** — Um agente de transferência de e-mail altamente configurável.

	[https://exim.org/](https://exim.org/) || [exim](https://www.archlinux.org/packages/?name=exim)

*   **[OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD")** — Um agente de transferência de e-mail, parte do projeto OpenBSD.

	[https://opensmtpd.org/](https://opensmtpd.org/) || [opensmtpd](https://www.archlinux.org/packages/?name=opensmtpd)

*   **[Postfix](/index.php/Postfix "Postfix")** — Um agente de transferência de e-mail, destinado a ser rápido, fácil de administrar e seguro.

	[http://www.postfix.org/](http://www.postfix.org/) || [postfix](https://www.archlinux.org/packages/?name=postfix)

*   **[Sendmail](/index.php/Sendmail "Sendmail")** — Um agente de transferência de e-mail bem conhecido.

	[http://www.sendmail.org/](http://www.sendmail.org/) || [sendmail](https://aur.archlinux.org/packages/sendmail/)

### Servidores POP3/IMAP

*   **[Courier](/index.php/Courier "Courier")** — Um agente de transferência de e-mail, fornecendo serviços POP3, IMAP, webmail e lista de discussão como componentes individuais.

	[https://www.courier-mta.org/](https://www.courier-mta.org/) || [courier-mta](https://aur.archlinux.org/packages/courier-mta/)

*   **[Cyrus IMAP](https://en.wikipedia.org/wiki/pt:Cyrus_(IMAP) "wikipedia:pt:Cyrus (IMAP)")** — Um agente de transferência de e-mail com um formato de spool de email personalizado fornece serviços POP3 e IMAP.

	[https://www.cyrusimap.org/](https://www.cyrusimap.org/) || [cyrus-imapd](https://aur.archlinux.org/packages/cyrus-imapd/)

*   **[Dovecot](/index.php/Dovecot "Dovecot")** — Um servidor IMAP e POP3 escrito para ser seguro, rápido e simples de configurar.

	[https://dovecot.org/](https://dovecot.org/) || [dovecot](https://www.archlinux.org/packages/?name=dovecot)

*   **[UW IMAP](/index.php/UW_IMAP "UW IMAP")** — Um servidor IMAP/POP.

	[https://www.washington.edu/imap/](https://www.washington.edu/imap/) || [imap](https://www.archlinux.org/packages/?name=imap)

### MDAs autônomos

*   **[fdm](/index.php/Fdm "Fdm")** — Um programa simples para entregar e filtrar mensagens.

	[https://github.com/nicm/fdm](https://github.com/nicm/fdm) || [fdm](https://www.archlinux.org/packages/?name=fdm)

*   **[Procmail](/index.php/Procmail "Procmail")** — Um programa para filtrar, classificar e armazenar email (não-mantido).

	[http://www.procmail.org/](http://www.procmail.org/) || [procmail](https://www.archlinux.org/packages/?name=procmail)

*   **Maildrop** — Um agente de transferência de e-mail/filtro de e-mail usado pelo Courier Mail Server.

	[https://www.courier-mta.org/maildrop/](https://www.courier-mta.org/maildrop/) || [courier-maildrop](https://aur.archlinux.org/packages/courier-maildrop/)

Veja também [Wikipedia:Comparison of e-mail servers](https://en.wikipedia.org/wiki/Comparison_of_e-mail_servers "wikipedia:Comparison of e-mail servers").

## Portas

| Propósito | Porta | Protocolo | Criptografia |
| Aceitar e-mail de outros MTAs. | 25 | SMTP | STARTTLS |
| Aceitar submissões a partir de MUAs. | 587 | SMTP | STARTTLS |
| 465 | [SMTPS](https://en.wikipedia.org/wiki/SMTPS "wikipedia:SMTPS") | TLS implícito |
| Permitir que MUAs acessem e-mails. | 110 | POP3 | STARTTLS |
| 995 | POP3S | TLS implícito |
| 143 | IMAP | STARTTLS |
| 993 | IMAPS | TLS implícito |

**Nota:** O TLS implícito é mais seguro do que o [STARTTLS](https://en.wikipedia.org/wiki/Opportunistic_TLS "wikipedia:Opportunistic TLS"), porque o último é vulnerável a [ataques *man-in-the-middle*](https://en.wikipedia.org/wiki/pt:Ataque_man-in-the-middle "wikipedia:pt:Ataque man-in-the-middle"). Para mais informações, consulte [[1]](https://serverfault.com/questions/523804/is-starttls-less-safe-than-tls-ssl) e [RFC:8314](https://tools.ietf.org/html/rfc8314 "rfc:8314").

## Registro MX

Hospedar um servidor de e-mail requer um [nome de domínio](https://en.wikipedia.org/wiki/pt:Dom%C3%ADnio "wikipedia:pt:Domínio") com um [registro MX](https://en.wikipedia.org/wiki/pt:Mx_record "wikipedia:pt:Mx record") apontando para o nome de domínio do seu agente de transferência de e-mail. O nome de domínio usado como o valor do registro MX deve ser mapeado para pelo menos um [endereço de registro](https://en.wikipedia.org/wiki/A_record "wikipedia:A record") (A, AAAA) e não deve ter um [registro CNAME](https://en.wikipedia.org/wiki/CNAME_record "wikipedia:CNAME record") para estar em conformidade com [RFC 2181](https://tools.ietf.org/html/rfc2181#section-10.3 "rfc:2181"), do contrário você pode não receber mensagens de alguns servidores de e-mail. A configuração de registros DNS geralmente é feita a partir da interface de configuração do seu [registrador de nomes de domínio](https://en.wikipedia.org/wiki/pt:Registrar "wikipedia:pt:Registrar").

## TLS

**Atenção:** Se você implementar [TLS](https://en.wikipedia.org/wiki/pt:Transport_Layer_Security "wikipedia:pt:Transport Layer Security"), certifique-se de seguir [TLS do lado do servidor](/index.php/Server-side_TLS "Server-side TLS") para evitar vulnerabilidades.

Para obter um certificado, veja [OpenSSL#Usage](/index.php/OpenSSL#Usage "OpenSSL").

## Autenticação

Há várias técnicas [autenticação por e-mail](https://en.wikipedia.org/wiki/Email_authentication "wikipedia:Email authentication").

### Sender Policy Framework

Do [Wikipédia](https://en.wikipedia.org/wiki/Sender_Policy_Framework "wikipedia:Sender Policy Framework"):

	**Sender Policy Framework** (**SPF**) é um protocolo de validação de e-mail projetado para detectar e bloquear falsificação de e-mail, fornecendo um mecanismo para permitir o recebimento de troca de e-mails para verificar se o e-mail recebido de um domínio vem de um endereço IP autorizado pelos administradores do domínio.

Para permitir que outros trocadores de e-mail validem e-mails aparentemente enviados de seu domínio, você precisa definir um registro DNS TXT, conforme explicado no [artigo da Wikipédia](https://en.wikipedia.org/wiki/pt:Sender_Policy_Framework "wikipedia:pt:Sender Policy Framework") (há também [um assistente online](https://www.spfwizard.net/)). Para validar as mensagens recebidas usando o SPF, você precisa configurar seu agente de transferência de e-mail para usar uma implementação SPF. Existem várias [implementações SPF](http://www.openspf.org/Implementations) disponíveis, [libspf2](https://www.archlinux.org/packages/?name=libspf2), [perl-mail-spf](https://www.archlinux.org/packages/?name=perl-mail-spf) e [perl-mail-spf-query](https://www.archlinux.org/packages/?name=perl-mail-spf-query) podem ser encontradas no repositórios oficiais.

<caption>Suporte a validação de SPF</caption>
| [Courier](/index.php/Courier "Courier") | Sim, embutido |
| [Postfix](/index.php/Postfix "Postfix") | [Sim](/index.php/Postfix#Sender_Policy_Framework "Postfix") |
| [Sendmail](/index.php/Sendmail "Sendmail") | por meio do [Milter](https://en.wikipedia.org/wiki/Milter "wikipedia:Milter") e do [spfmilter-acme](https://aur.archlinux.org/packages/spfmilter-acme/) |
| [Exim](/index.php/Exim "Exim") | [experimental](https://github.com/Exim/exim/wiki/SPF), exibe [libspf2](https://www.archlinux.org/packages/?name=libspf2) |
| [OpenSMTPD](/index.php/OpenSMTPD "OpenSMTPD") | Não |
| [Cyrus IMAP](https://en.wikipedia.org/wiki/pt:Cyrus_(IMAP) | ? |

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
*   [SpamAssassin](/index.php/SpamAssassin "SpamAssassin") para identificar e filtrar spam
*   [Sieve](https://en.wikipedia.org/wiki/Sieve_(mail_filtering_language) – uma linguagem de programação para filtrar e-mail
*   [webmail](https://en.wikipedia.org/wiki/pt:Webmail "wikipedia:pt:Webmail") como o [Roundcube](/index.php/Roundcube "Roundcube") ou o [Squirrelmail](/index.php/Squirrelmail "Squirrelmail")