[Adminer](http://www.adminer.org/) je nástroj pro jednoduchou správu databází [MySQL](/index.php/MySQL_(%C4%8Cesky) "MySQL (Česky)"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), [Sqlite](/index.php/Sqlite "Sqlite"), MS SQL a [Oracle](/index.php/Oracle "Oracle"). Je to jednodušší alternativa k [PhpMyAdminu](/index.php/PhpMyAdmin_(%C4%8Cesky) "PhpMyAdmin (Česky)"). Více informací o projektu lze nalézt na jeho [oficiálních stránkách](http://www.adminer.org/cs/) nebo [wikipedii](https://en.wikipedia.org/wiki/Adminer "wikipedia:Adminer").

## Instalace pod Apache

*   Před instalací se ještě ujistěte, že v počítači nemáte žádnou starší kopii Admineru:

```
$ rm -r /srv/http/adminer

```

*   Instalace z [AURu](/index.php/AUR_(%C4%8Cesky) "AUR (Česky)") se poté provede programem [yaourt](/index.php/Yaourt_(%C4%8Cesky) "Yaourt (Česky)") jednoduše spuštěním:

```
$ yaourt -S adminer

```

*   Po instalaci je nutné do souboru `/etc/httpd/conf/httpd.conf` přidat řádek:

```
Include conf/extra/httpd-adminer.conf

```

To lze udělat pomocí příkazu:

```
$ echo "Include conf/extra/httpd-adminer.conf" >> /etc/httpd/conf/httpd.conf

```

*   Následně už pouze stačí restartovat vašeho [Apache](/index.php/LAMP_(%C4%8Cesky) "LAMP (Česky)") daemona:

```
$ /etc/rc.d/httpd restart

```

**Note:** K Adminerovi pak můžete přistupovat pomocí svého prohlížeče na adrese [http://localhost/adminer](http://localhost/adminer).

## Externí odkazy

*   [Oficiální stránka Admineru](http://www.adminer.org/cs/)
*   [Adminer na AURu](https://aur.archlinux.org/packages.php?ID=41492)
*   [Weblog autora projektu](http://php.vrana.cz/)
*   [Adminer na Wikipedii](http://cs.wikipedia.org/wiki/Adminer)