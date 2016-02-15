Sudo (su "do") dovoluje systémovému administrátorovi předat určitým uživatelům (nebo jejich skupinám) oprávnění spouštět některé (případně všechny) příkazy jako root nebo jiný uživatel, přičemž poskytuje o těchto příkazech a jejich parametrech kontrolní záznamy. [[1]](http://www.gratisoft.us/sudo/)

## Contents

*   [1 Princip](#Princip)
*   [2 Instalace](#Instalace)
*   [3 Použití](#Pou.C5.BEit.C3.AD)
*   [4 Konfigurace](#Konfigurace)
    *   [4.1 Časový limit pro heslo](#.C4.8Casov.C3.BD_limit_pro_heslo)
*   [5 Tipy a triky](#Tipy_a_triky)
    *   [5.1 Urážky](#Ur.C3.A1.C5.BEky)
    *   [5.2 Heslo roota](#Heslo_roota)

## Princip

Sudo je bezpečná alternativa k tradičnímu příkazu [su](/index.php/Su "Su"). Uživatelé často používají su (**s**ubstitute **u**ser — nahradit uživatele) pro získání práv roota. Obecně je přihlašování pod rootem — superuživatelem — na delší dobu považováno za nerozumné. Uživatel root si užívá kompletní a absolutní kontroly nad celým systémem, což je riskantní. Malé přepsání snadno dovede uvést systém do nepoužitelného stavu a aplikace běžící pod tímto uživatelem mohou tento neomezený přístup šířit.

Spíše než to nabízí sudo _dočasné_ navýšení práv pro jednotlivé příkazy (ať už jako root nebo jiný uživatel); navracejíc se po jejich dokončení do neprivilegovaného stavu, čímž chrání systém před nechtěnými důsledky. Navíc sudo zaznamenává všechny příkazy a neúspěšné pokusy o přístup pro kontrolu těchto událostí.

## Instalace

Pro instalaci suda zadejte:

```
# pacman -S sudo

```

Ve výchozím nastavení uživatelům není dovoleno sudo spustit. Pro instrukce viz [#Konfigurace](#Konfigurace).

## Použití

S nainstalovaným a nakonfigurovaným sudem mohou uživatelé pro spuštění příkazů s oprávněními superuživatele (nebo jinými) před tyto příkazy psát `sudo`. Například:

```
$ sudo pacman -Syu

```

Viz [manuálová stránka suda (anglicky)](http://www.gratisoft.us/sudo/man/sudo.html) pro více informací.

## Konfigurace

Konfigurační soubor pro sudo je `/etc/sudoers`. **Tento soubor nemá být upravován přímo!** Místo toho musí uživatelé zadat jako root příkaz `visudo`, jenž v programu specifikovaném proměnnou prostředí _$EDITOR_ otevře dočasnou kopii konfiguračního souboru.

```
# visudo

```

Výchozí editor je _vi_. Pokud si s _vi_ nerozumíte, zadejte nejdříve tento příkaz:

```
# export EDITOR=nano

```

Nebo jej změňte natrvalo přídáním následujícího do souboru `/etc/sudoers`, kde "vim" je vámi upřednostňovaný textový editor:

```
# Specifikace Defaults
# Ve výchozím nastavení pročistit proměnné prostředí
Defaults      env_reset
# Nastavit výchozí editor na vim, nedovolit programu visudo použít EDITOR/VISUAL.
Defaults      editor=/usr/bin/vim, !env_editor

```

Poznámka: I když použijete jiný editor, stále musíte spouštět `visudo` jako root.

Když je soubor uložen, `visudo` jej před přepsáním existujícího souboru `/etc/sudoers` prověří na syntaktické chyby. Tento bezpečnostní prvek je zaveden kvůli tomu, že pokud konfigurační soubor obsahuje chyby, sudo bude uvedeno v nepoužitelnost.

Abyste určitému uživateli povolili získání oprávnění roota, když na začátek příkazu napíše "sudo", přidejte následující řádek:

```
UŽIVATELSKÉ_JMÉNO   ALL=(ALL) ALL

```

Povolení přístupu k sudu pouze z lokálního počítače:

```
UŽIVATELSKÉ_JMÉNO   HOSTNAME=(ALL) ALL

```

kde UŽIVATELSKÉ_JMÉNO je uživatelské jméno dotyčného uživatele.

Povolení členům [skupiny](/index.php?title=Groups_(%C4%8Cesky)&action=edit&redlink=1 "Groups (Česky) (page does not exist)") kolo použít sudo bez výzvy k zadání hesla:

```
%kolo      ALL=(ALL) NOPASSWD: ALL

```

Obšírnější příklad `sudoers` můžete nalézt [zde](http://www.gratisoft.us/sudo/sample.sudoers). Pro detailní informace si prohlédněte [manuál k sudoers (anglicky)](http://www.gratisoft.us/sudo/man/sudoers.html).

### Časový limit pro heslo

Uživatelé si mohou přát změnit výchozí časový limit před vypršením hesla. Toho docílíte přidáním následující řádky do `/etc/sudoers` (`visudo`). Například:

```
Defaults:UŽIVATELSKÉ_JMÉNO timestamp_timeout=20

```

Zde heslo pro uživatele UŽIVATELSKÉ_JMÉNO vyprší, pokud sudo nepoužije déle než 20 minut.

**Tip:** Pokud chcete, aby se sudo ptalo na heslo vždy, nastavte časový limit na nulu.

## Tipy a triky

### Urážky

Uživatelé mohou sudo nakonfigurovat tak, aby namísto výchozí zprávy "špatné heslo" zobrazovalo chytré urážky. Najděte řádek Defaults v souboru `/etc/sudoers` a přidejte za čárku ke stávajícím volbám "insults". Výsledek může vypadat nějak takto:

```
# Specifikace Defaults
Defaults insults

```

Pro otestování zadejte `sudo -K` pro ukončení současného sezení a nechce se suda dotázat na heslo.

### Heslo roota

Uživatelé mohou sudo nakonfigurovat tak, aby místo jejich vlastního uživatelského hesla chtělo heslo uživatele root. Toho lze docílit přidáním volby "rootpw" na řádek Defaults v souboru `/etc/sudoers`:

```
Defaults timestamp_timeout=0,rootpw

```