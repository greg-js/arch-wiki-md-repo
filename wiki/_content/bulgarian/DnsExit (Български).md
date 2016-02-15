# Увод

Q. What services does DnsExit.com provide?

A. We provide domain name registration, dynamic / static DNS services, URL forwarding, Backup Mail service, Email Forwarding service, Email Redirection service. DnsExit.com provides a convenient single-location, integrated, web-based domain manager for configuring all of the services provided. Click here to learn more.

# Клиент на dnsExit

Клиента идва с разширения .deb, .rpm and .tar.gz. Макар, че е написа с Perl, трябва да се променят няколко неща за да работи с Arch Linux.

Get the tarball from [this address](http://www.dnsexit.com/Direct.sv?cmd=ipClients).

# Инсталация

Разархивирайте архива, влезте в папката и въведете:

```
# perl setup.pl

```

Инсталацияата е автоматизина. След това трябва да се пусне програмата за да създаде файла с разширение .pid, понеже не се създава по време на инсталацияата от setup.pl

```
# perl ipUpdate.pl

```

След това се копира програмата за да може да се ползва като daemon:

```
# cp ipUpdate.pl /usr/sbin/ipUpdate.pl

```

Също така трябва да се копира:

```
# cp Http_get.pm /usr/sbin/Http_get.pm

```

След това се създава самия файл за daemona. При мен липсваше.

```
# vim /etc/rc.d/ipUpdate

```