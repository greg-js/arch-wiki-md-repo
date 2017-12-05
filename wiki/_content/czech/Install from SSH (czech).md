Tento článek má ukázat uživatelům, jak nainstalovat Arch vzdáleně prostřednictvím připojení SSH. Zvažte tento přístup oproti standardnímu v scénářích, jako jsou následující:

*   HTPC bez náležitého monitoru (např. SDTV);
*   Počítač umístěný v jiném městě, státě, zemi (dům přítele, dům rodičů atd.);
*   PC, který byste raději nastavili vzdáleně, například z pohodlí vlastní pracovní stanice s možností kopírovat/vložit z ArchWiki.

## Na vzdáleném (cílovém) zařízení

**Note:** : Tyto kroky vyžadují fyzický přístup k zařízení. Je zřejmé, že je-li fyzicky umístěno jinde, budou muset být koordinovány s jinou osobou.

Nabootujte cílový počítač do živého prostředí Arch pomocí [Live CD/USB image](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch"): uživatel bude přihlášen jako root.

V tomto okamžiku nastavte síť na cílovém stroji, jak je například navrženo v [Installation guide#Connect to the Internet](/index.php/Installation_guide#Connect_to_the_Internet "Installation guide")

Zadruhé nastavte heslo pro root, které je potřebné pro připojení SSH, protože výchozí heslo pro root je prázdné:

```
# passwd

```

Nyní zkontrolujte, zda je v `/etc/ssh/sshd_config` přítomen (a nezakomentován) `PermitRootLogin yes`. Toto nastavení umožňuje přihlášení root s ověřením hesla na serveru SSH.

**Note:** Pokud je cílový počítač za směrovačem s NAT, je nutné, aby port SSH (ve výchozím nastavení 22) byl předán na IP adresu cílového zařízení. Použití přesměrování portů není v této příručce obsaženo.

Nakonec spusťte démon openssh pomocí služby `sshd.service`, který je na živém CD ve výchozím nastavení obsažen.

**Note:** Po instalaci se doporučuje v prvním kroku odstranění `PermitRootLogin yes` z `/etc/ssh/sshd_config`.

## Na místním počítači

Na místním počítači se připojíte k cílovému počítači přes SSH pomocí následujícího příkazu:

```
$ ssh root@*ip.adresa.cilovy.pocitac*

```

Odtud je prezentována uvítací zpráva živého prostředí a je možné spravovat cílový stroj, jako by na fyzické klávesnici. V tomto okamžiku, je-li záměrem jednoduše instalovat Arch z živého média, postupujte podle pokynů v [Installation guide](/index.php/Installation_guide "Installation guide"). Pokud je záměrem upravit stávající instalaci systému Linux, která byla porušena, postupujte podle článku [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux").