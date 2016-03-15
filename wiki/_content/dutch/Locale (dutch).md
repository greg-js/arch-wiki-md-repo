## Nederlands / Nederland

Het is eenvoudig om Nederlands als standaardtaal te installeren. Bewerk als root `/etc/locale.gen`. Haal het hekje weg voor `nl_NL.UTF-8`. Draai nu

```
 # locale-gen

```

Als je nu

```
 $ locale -a

```

draait, ziet u als het goed is `nl_NL.UTF-8` er tussen staan.

Om nu Nederlands in te stellen, moeten we `/etc/rc.conf` bewerken. Vervang de regel `LOCALE="en_US.UTF-8"` door `LOCALE="nl_NL.UTF-8"`.

De volgende keer dat de computer wordt opgestart, is alles (wat vertaald is) in het Nederlands.

## Nederlands / België

Bewerk als root `/etc/locale.gen`. Haal het hekje weg voor `nl_BE.UTF-8`. Draai nu

```
 # locale-gen

```

Als je nu

```
 $ locale -a

```

draait, ziet u als het goed is `nl_BE.UTF-8` er tussen staan.

Om nu Nederlands in te stellen, moeten we `/etc/rc.conf` bewerken. Vervang de regel `LOCALE="en_US.UTF-8"` door `LOCALE="nl_BE.UTF-8"`.

De volgende keer dat de computer wordt opgestart, is alles (wat vertaald is) in het Nederlands.