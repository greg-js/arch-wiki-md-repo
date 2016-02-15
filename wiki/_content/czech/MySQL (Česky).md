# Úvod

MySQL je populární, vícevláknový a víceuživatelský SQL databázový server. Více informací o vlastnostech naleznete na oficiální [domovské stránce](http://www.mysql.com/).

# Instalace

Nainstalujte balíček [mysql](https://aur.archlinux.org/packages/mysql/).

Po instalaci MySQL byste měli jako root spustit init skript:

```
# /etc/rc.d/mysqld start

```

Ten se postará o základní nastavení jako například přidání systémových uživatelů nebo vytvoření logovacích souborů. Můžete přidat `mysqld` do pole `DAEMONS` v `/etc/rc.conf`, aby MySQL startoval po spuštění systému:

```
DAEMONS=(... mysqld ...)

```

# Nastavení

Po spuštění MySQL serveru budete asi chtít vytvořit účet roota, abyste mohli spravovat MySQL uživatele a databáze. To uděláte jako root následovně:

```
# mysqladmin -u root password VASE_HESLO

```

Tento příkaz vytvoří účet roota s heslem VASE_HESLO. Následně je možné pokračovat v konfiguraci prostřednictvím vašeho oblíbeného rozhraní. Například můžete použít rozhraní příkazové řádky MySQL, abyste se jako root přihlásili k MySQL serveru:

```
$ mysql -p -u root

```