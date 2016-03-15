Démon je program, který běží v pozadí, čeká na události, které nastanou, reaguje na ně a poskytuje služby. Ukázkovým příkladem může být třeba webový server, který čeká na požadavek na sestavení stránky, nebo SSH server, který čeká, až se někdo vzdáleně přihlásí. To jsou příklady programů s mnoha vlastnostmi, ne všechny démony se ale viditelně projevují - démon, který zaznamenává činnost systému (např. syslog, metalog), démon, který sníží frekvenci procesoru, pokud systém nemá nic na práci.

## Contents

*   [1 Spouštění po startu](#Spou.C5.A1t.C4.9Bn.C3.AD_po_startu)
*   [2 Ruční spouštění a zastavování](#Ru.C4.8Dn.C3.AD_spou.C5.A1t.C4.9Bn.C3.AD_a_zastavov.C3.A1n.C3.AD)
*   [3 Základy](#Z.C3.A1klady)
*   [4 Spouštění démonů v pozadí](#Spou.C5.A1t.C4.9Bn.C3.AD_d.C3.A9mon.C5.AF_v_pozad.C3.AD)

## Spouštění po startu

Běžná instalace Arch Linuxu po startu spouští jen velmi málo démonů či služeb. Služby můžete snadno přidat či odstranit editováním souboru [rc.conf](/index.php/Rc.conf "Rc.conf"). Najděte řádek, který v nové instalaci vypadá zhruba takto:

```
DAEMONS=(syslog-ng network netfs crond)

```

Služby (démony) se při startu spouštějí v pořadí, v jakém jsou uvedeny na tomto řádku. Můžete jejich automatické spouštění zakázat tak, že před název umístíte vykřičník (!). Můžete je také spustit na pozadí - přidejte před název zavináč (@).

## Ruční spouštění a zastavování

Skripty určené ke spouštění služeb se nacházejí v adresáři /etc/rc.d/. Služby můžete ručně spouštět, zastavovat nebo restartovat příkazem

```
/etc/rc.d/*nameofservice* {start|stop|restart}

```

Skripty mohou mít ještě další příkazy - najdete je v dokumentaci. Obvykle je také vypíše samotný skript, pokud jej spustíte bez parametrů.

## Základy

Služby přidávejte pouze tehdy, pokud je potřebujete. Typický uživatel si asi spustí služby [CUPS](/index.php/CUPS "CUPS"), [HAL](/index.php/HAL "HAL") a [ALSA](/index.php/ALSA "ALSA"). Uvědomte si, že některé služby spouštějí další služby. Například HAL automaticky spouští [D-Bus](/index.php/D-Bus_(%C4%8Cesky) "D-Bus (Česky)") a [Acpid](/index.php/Acpid "Acpid"). Pamatujte také na to, že pokud do systému nainstalujete novou službu, musíte jí ručně přidat do [rc.conf](/index.php/Rc.conf "Rc.conf"), pokud ji tedy chcete spouštět při startu systému.

## Spouštění démonů v pozadí

Je to praktické pro případ, kdy potřebujete, aby se druhá služba spustila dříve, než první skončí. Které služby (démony) spouštět v pozadí, záleží na vašich potřebách - nespouštějte tímto způsobem hned všechno. Zde je příklad:

```
DAEMONS=(syslog-ng gensplash network netfs hal @avahi-daemon @samba @crond @alsa @openntpd @cupsd @mpd)

```