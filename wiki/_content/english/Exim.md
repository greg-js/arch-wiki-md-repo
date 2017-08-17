This article gives a quick overview on the configuration of an exim mail server.

[Exim](http://exim.org/) is a versatile [SMTP](https://en.wikipedia.org/wiki/SMTP "wikipedia:SMTP") server for Linux/UNIX-like systems. While the [exim wiki](https://github.com/Exim/exim/wiki/) provides some helpful how-to's on certain specific use cases, a [detailed description](https://exim.org/exim-html-current/doc/html/spec_html/index.html) of all configuration options is available as well.

## Contents

*   [1 Installation](#Installation)
*   [2 Basic configuration](#Basic_configuration)
    *   [2.1 Main parameters](#Main_parameters)
    *   [2.2 TLS, security & authentification](#TLS.2C_security_.26_authentification)
    *   [2.3 Routing, transport & retry](#Routing.2C_transport_.26_retry)
        *   [2.3.1 Use manualroute](#Use_manualroute)
    *   [2.4 ACL: Access Control Lists](#ACL:_Access_Control_Lists)
    *   [2.5 Hide machine name](#Hide_machine_name)
    *   [2.6 Startup](#Startup)
*   [3 Advanced ACL configuration](#Advanced_ACL_configuration)
*   [4 Dovecot LMTP delivery & SASL authentification](#Dovecot_LMTP_delivery_.26_SASL_authentification)
*   [5 DKIM & DNSSEC](#DKIM_.26_DNSSEC)
*   [6 Using Gmail as smarthost](#Using_Gmail_as_smarthost)
*   [7 Hardening](#Hardening)
    *   [7.1 Rate limits](#Rate_limits)
    *   [7.2 fail2ban](#fail2ban)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 451 Temporary local problem](#451_Temporary_local_problem)

## Installation

Install the [exim](https://www.archlinux.org/packages/?name=exim) package.

## Basic configuration

Exim comes with a bulky default configuration file which is located in `/etc/mail/exim.conf`. Many options in there aren't necessary in a regular use case. By default configuration is done in a single file containing several chapters. Below is a very basic configuration, which provides: local delivers to system users (Maildir format) and authorized relaying to MX hosts. The description is based on a domain "mydomain.tld" served on a host "hostname.mydomain.tld". It is highly recommended to consult the official documentation before using the given documentation below.

### Main parameters

Main parameters contain some basic options. Using solely those options would open ports for connections but still no mail would be accepted nor relayed anywhere.

```
# be the responsible mail host for hostname.mydomain.tld (@) & mydomain.tld
domainlist local_domains = @ : mydomain.tld

# we don't relay. Not for foreign domains nor for a single host
domainlist relay_to_domains =
hostlist relay_from_hosts = 

# serve the 2 ports 25 and 587; don't use 465 - it's not an official port
daemon_smtp_ports = 25 : 587

# do a reverse name lookup for all incoming connections
host_lookup = *

# Logging: log all events, add syslog to logging path & avoid double entries
log_selector = +all
log_file_path = : syslog
syslog_duplication = false

# undeliverables: discard bounce messages after 2d and all others after 7 d
ignore_bounce_errors_after = 2d
timeout_frozen_after = 7d

```

### TLS, security & authentification

The first part of the following options are still part of the first configuration section in exim. Starting with "begin authenticators" the first special section in exim configuration begins. There will be more such sections later. Below some very basic security related options are defined, TLS is set up & a plain text authentificatior using a user password lookup is introduced.

**Warning:** This example of an authentificator should not be used in production enviroment!

```
# actually not required: it's hard coded - anyway: no mail delivery to root
never_users = root

# don't show the exim version to everyone. Actually not even show the name.
smtp_banner = $smtp_active_hostname ESMTP $tod_full

# STARTTLS is offered to everyone
tls_advertise_hosts	= *
tls_certificate = /path/to/exim/only/fullchain.pem
tls_privatekey = /path/to/exim/only/privkey.pem

# use all ciphers on port 25, use only good ciphers on port 587
tls_require_ciphers = ${if =={$received_port}{25} \
				{DEFAULT} {HIGH:!MD5:!SHA1:!SHA2}}

# we don't use port 465, so we don't activate TLS on it
#tls_on_connect_ports = 465

# special sections always start with a "begin"
begin authenticators

	PLAIN:
		# authentification protocol is plain text
		driver = plaintext
		# authentification is offered as plain text
		public_name = PLAIN
		server_prompts = :
		# authentification is successful, if the password provided ($auth3) 
		# equals the password found in a lookup file for user ($auth2)
		server_condition = ${if eq{$auth3}{${lookup{$auth2}dbm{/etc/authpwd}}}}
		server_set_id = $auth2
		# only offer plain text authentification after TLS is been negotiated
		server_advertise_condition = ${if def:tls_in_cipher}

```

**Note:** Exim loads certificate files during mail processing with the low privilege user exim. While it is good to run an internet facing process with such a user, it is somewhat strange to give access to a private key to such user. If your server serves multiple purposes (e.g. http, imap, smtp) with multiple dns aliases (cname or several names pointing to a single ip) it may be wise to request multiple certificates. If the exim certificate gets lost, damage is limited to smtp.

### Routing, transport & retry

For each receipient of a message routing is performed as follows: routers are tested in their order given in the routing section. For each router, conditions may apply (e.g. `domains = ! +local_domains`). Only if all conditions apply, the message will be handed over to the defined transport (e.g. `transport = smtp`). If transport fails or not all conditions of a router are fulfilled, the next router is tested.

```
begin routers

	# that's the relay router
	dnslookup:
		# the router type
		driver = dnslookup
		# the domains served on this router: not the local domain
		domains = ! +local_domains
		# the transport to be used (see transport section below)
		transport = remote_delivery
		# localhost is to be ignored if dns gives such result
		ignore_target_hosts = <; 0.0.0.0 ; 127.0.0.0/8 ; ::1
		# a router list is processed until matched and successful transported.
		# if transport fails, we don't want the next router to be used
		no_more

	# local delivery
	localuser:
		# the transport type - we accept the mail locally
		driver = accept
		# this router serves only our domains
		domains	= +local_domains
		# use transport named local_delivery
		transport = local_delivery
		# in case local delivery fails
		cannot_route_message = Unknown local user

begin transports

	remote_delivery:
	 	driver = smtp

	local_delivery:
		#deliver to a local mailbox
		driver = appendfile
		file = /var/mail/$local_part

# if routing or transport fails, try again after this (default) ruleset
begin retry

	# Address or Domain    Error       Retries
	# -----------------    -----       -------
	*                      *           F,2h,15m; G,16h,1h,1.5; F,4d,6h

```

#### Use manualroute

If you wang to use manualroute instead, comment out the dnslookup block and add the smarthost block.

```
#dnslookup:
    # the router type
    # driver = dnslookup
    # the domains served on this router: not the local domain
    # domains = ! +local_domains
    # the transport to be used (see transport section below)
    # transport = remote_delivery
    # localhost is to be ignored if dns gives such result
    # ignore_target_hosts = <; 0.0.0.0 ; 127.0.0.0/8 ; ::1
    # a router list is processed until matched and successful transported.
    # if transport fails, we don't want the next router to be used
    # no_more

smarthost:
  driver = manualroute
  domains = !+local_domains
  transport = remote_delivery
  route_list = * smtp.myisp.com        # change to the desired smtp server
  ignore_target_hosts = <; 0.0.0.0 ; 127.0.0.0/8 ; ::1
```

### ACL: Access Control Lists

Access Control Lists are at the heart of exim. They are required for basic checks and may be used for sophisticated message processing. In general the overal message processing in exim is:

 `connection > (authentification >) ACL > routing > transport` 

With this it is important to note that messages coming from authenticated clients are treated (by default) by the same ACL as messages coming from other mail servers. Exim know a full set of [different ACL](https://www.exim.org/exim-html-current/doc/html/spec_html/ch-access_control_lists.html). Good knowledge of the SMTP protocol is required to choose the correct set of ACL.

 `acl_smtp_connect > acl_smtp_helo > ... > acl_smtp_rcpt > ... > acl_smtp_data > ...` 

For a basic setup two ACL are mandatory: acl_smtp_rcpt and acl_smtp_data. These are default to deny while all other default to accept. The example below just prevents being an open relay. This setup has multiple security flaws (e.g. all authentificated users may use any mail address). If added to an existing configuration, it must be added before any other special section (i.e. before any existing "begin").

**Warning:** Don't use the following example in a production example! It lacks several required checks!

```
# use this ACL after SMTP RCPT TO: is received
acl_smtp_rcpt = basic_acl_rcpt
# use this ACL after SMTP DATA is finished, i.e. all data has been received
acl_smtp_data = basic_acl_data

begin acl

	basic_acl_rcpt:

		# accept all messages for which I am the receiving mail host
		accept 	domains = +local_domains

		# accept all messages from authetificated clients
		accept	authenticated = *

		# deny all other messages (i.e. messages to be relayed from unauthorized
		# clients)
		deny	message = "we are not an open relay"

	basic_acl_data:

		# we have done all checks after RCPT already
		accept

```

### Hide machine name

If you have a laptop, or a machine in a smarthost configuration, where you do not want the name of the machine to appear in the outgoing email then you must enable exim's rewriting facilities.

In the Rewriting section you should have something like:

```
*@*machine*.*mydomain* $1@*mydomain*

```

where `*machine*` is the hostname of your laptop or PC and `*mydomain*` is the domain name of the machine and the outgoing mail. To rewrite only sender domain, add special flag (F) in the line end. See [upstream document](http://www.exim.org/exim-html-current/doc/html/spec_html/ch-address_rewriting.html) for detail

### Startup

[Start/enable](/index.php/Start/enable "Start/enable") the `exim.service`.

## Advanced ACL configuration

## Dovecot LMTP delivery & SASL authentification

In this section the integration of [Dovecot](/index.php/Dovecot "Dovecot") is described. It is assumed that Dovecot & Exim are already setup and configured. Dovecot will serve as SASL authentificator and local transport mechanism. For this purpose the Dovecot services will be setup as follows.

 `/etc/dovecot/conf.d/10-master.conf` 
```
service auth {
	unix_listener exim-auth {
		mode = 0600
		user = exim
		group = exim        
	}
	# Auth process is run as this user.
	user = $default_internal_user
}

service lmtp {
	# a unix socket is prefered of a local port communication
	unix_listener exim-lmtp {
		mode = 0600
		group = exim
		user = exim
	}
}

```

To use the dovecot SASL in a TLS protected enviroment, add the following authentificator to exim.

 `/etc/mail/exim.conf - authenticators section` 
```
	PLAIN:
		driver = dovecot
		public_name = PLAIN
		server_socket = /var/run/dovecot/exim-auth
		server_set_id = $auth1
		server_advertise_condition = ${if def:tls_in_cipher}

```

The existing router for local delivery can be reused. You may want to consider add a `dsn_lasthop` to the router definition. If [DSN](https://de.wikipedia.org/wiki/Delivery_Status_Notification) is used, exim will assume final delivery of the message at this point. In the transport section the transport for local delivery must be replaced by the following transport definition.

 `/etc/mai/exim.conf - transports section` 
```
	local_delivery:
		driver = lmtp
		socket = /var/run/dovecot/exim-lmtp
		batch_max = 200

```

**Note:** As of exim 4.88 there is a limitation with the lmtp driver: in an ACL `verify = recipient/callout=no_cache` won't work as expected, i.e. non-existent user accounts won't throw a failure. To accomplish a receipient check against Dovecot you must replace the driver above by a
```
driver = smtp
protocol = lmtp
host = 127.0.0.1
port = 2525
```

Furthermore your Dovecot lmtp service must be adjusted accordingly.

Since Dovecot is configured to provide a unix socket for the exim user, you may harden your security by adding the following line to the main configuration section.

 `/etc/mail/exim.conf - main section` 
```
# don't deliver being root, drop privileges to exim user
deliver_drop_privilege = true
```

## DKIM & DNSSEC

## Using Gmail as smarthost

In the beginning of the exim conf file, you must enable TLS using

 `tls_advertise_hosts = +local_network : *.gmail.com` 

or to advertise tls to all hosts

 `tls_advertise_hosts = *` 

More information about TLS can be found in the [exim documentation](http://www.exim.org/exim-html-current/doc/html/spec_html/ch-encrypted_smtp_connections_using_tlsssl.html).

**Note:** The following must be put in the appropriate sections of the configuration file, eg, after **begin authenticators**.

Add a router before or instead of the dnslookup router:

```
gmail_route:
  driver = manualroute
  transport = gmail_relay
  route_list = * smtp.gmail.com
```

Add a transport:

```
gmail_relay:
  driver = smtp
  port = 587
  tls_verify_certificates = /etc/ssl/certs/ca-certificates.crt
  # this forces host verification.
  tls_verify_hosts = smtp.gmail.com
  hosts_require_auth = <; $host_address
  hosts_require_tls = <; $host_address
```

Because of host verification, your exim log might contain

 `SSL verify error: certificate name mismatch: "/C=US/ST=California/L=Mountain View/O=Google Inc/CN=smtp.gmail.com"` 

But this has no effect on mail-delivery and can be ignored. Add an authenticator (replacing myaccount@gmail.com and mypassword with your own account details):

```
gmail_login:
  driver = plaintext
  public_name = LOGIN
  hide client_send = : myaccount@gmail.com : mypassword
```

`$host_address` is used for `hosts_require_auth` and `hosts_require_tls` instead of smtp.gmail.com to avoid occasional 530 5.5.1 Authentication Required errors. These are caused by the changing IP addresses in DNS queries for smtp.gmail.com. `$host_address` will expand to the particular IP address that was resolved by the `gmail_route` router.

For added security, use a per-application password. This works with Google Apps accounts as well.

## Hardening

### Rate limits

Security breaches happen. In case you don't have any service that submits local mail (receiving mail from localhost on a port is not considered local submission), completely disable local submission. Do so by adding `acl_not_smtp = acl_local` to the main section and add the following simple ACL to the acl section.

 `/etc/mail/exim.conf - acl section` 
```
	acl_local:

		deny	log_message = AL01: Local submission denied.

```

In local submission is required, consider imposing a rate limit to it. Do so by adding `acl_not_smtp = acl_local` to the main section and adding the following ACL to the acl section. It imposes 2 rate limits: 20 mails in a single minute and 30 mails in 10 minutes. With this a burst of local submitted alerts are possible while

 `/etc/mail/exim.conf - acl section` 
```
	acl_local:

		# apply a limit of 30 mails to the administrator for alerts submitted
		# by local services
		deny	ratelimit	= 30 / 1m / strict 
			recipients 	= admin@mydomain.tld : root@hostname.mydomain.tld
			log_message	= AL01: Sender rate limit for local submission \
					  exceeded: $sender_rate / $sender_rate_period.

		# apply a burst limit of 3 mails per minute to everyone else
		deny	ratelimit	= 3 / 1m / strict 
			!recipients 	= admin@mydomain.tld : root@hostname.mydomain.tld
			log_message 	= AL02: Sender rate limit for local submission \
					  exceeded: $sender_rate / $sender_rate_period.

		# apply a regular limit of 10 mails per 30 minutes to everyone else
		deny	ratelimit	= 10 / 30m / strict 
			!recipients 	= admin@mydomain.tld : root@hostname.mydomain.tld
			log_message 	= AL03: Sender rate limit for local submission \
					  exceeded: $sender_rate / $sender_rate_period.

		accept

```

### fail2ban

## Troubleshooting

### 451 Temporary local problem

If you are getting a "451 Temporary Local Problem" when testing SMTP, you are probably sending as root. By default Exim will not allow you to send as root.