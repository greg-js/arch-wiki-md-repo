Na vysvětlenou: "locales" jsou soubory definující pravidla pro zobrazování znaků různých abeced a jazyků. Jsou základem správně nastaveného systému. Pokud máte nesprávně nastavené locales, bude mít pravděpodobně problémy také vaše grafické prostředí jako celek nebo i jednotlivé aplikace (např. OpenOffice.org). Budete mít také problém se psaním českých písmen.

Nastavení locales (přidání a odebrání) je snadné. Jako superuživatel root upravte soubor `/etc/locale.gen`: odkomentujte (tzn. odstraňte znak # na začátku řádku) požadované locales. Potom spusťte jako root `locale-gen`. Pokud následně spustíte `locale -a`, měli byste vidět locales, které jste nastavili.

```
$ locale -a
C
cs_CZ.utf8
POSIX

```

Aby mělo vaše locale efekt, musíte jej nastavit v souboru <tt>/etc/rc.conf</tt>. Vyberte si požadované locale, které jste viděli ve výpise <tt>locale -a</tt>, a vložte jej jako parametr proměnné:

```
LOCALE="cs_CZ.utf8"

```

Toto nastavení je platné pro celý systém, takže pokud je ve vašem systému více uživatelů, kteří upřednostňují jiné locale, mohou si ho nastavit např. v přihlašovacím profilu, tj. souboru <tt>.bashrc</tt> v domovském adresáři. Stačí do něj přidat (příklad pro němčinu)

```
export LANG="de_DE@euro"

```

Správné nastavení locale znamená, že terminály jako např. xterm správně zobrazí národní znaky (háčky, čárky, přehlásky a další). Pokud potřebujete podporu pro jazyky, jako je arabština nebo hebrejština, zvažte použití programu [mlterm](/index.php/Mlterm "Mlterm").