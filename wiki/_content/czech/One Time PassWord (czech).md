Related articles

*   [Secure Shell](/index.php/Secure_Shell "Secure Shell")
*   [S/KEY Authentication](/index.php/S/KEY_Authentication "S/KEY Authentication")
*   [Pam abl](/index.php/Pam_abl "Pam abl")
*   [Google Authenticator](/index.php/Google_Authenticator "Google Authenticator")

**One Time PassWord** (**OTPW**) je PAM modul, který zprostředkuje použití hesel "na jedno použití" k přihlášení do systému. Tohle se hodí zejména v kontextu Secure shell, a to umožnění přihlášení z veřejných nebo sdílených počítačů, za pomoci jednorázových hesel, které nebudou nikdy fungovat znova.

Instrukce pro instalaci OTPW a konfiguraci SSH používat OTPW k přihlášení jsou níže.

## Contents

*   [1 Instalace](#Instalace)
*   [2 Konfigurace pro ssh přihlášení](#Konfigurace_pro_ssh_p.C5.99ihl.C3.A1.C5.A1en.C3.AD)
    *   [2.1 PAM Konfigurace](#PAM_Konfigurace)
    *   [2.2 Konfigurace sshd](#Konfigurace_sshd)
    *   [2.3 Konfigurace OTPW](#Konfigurace_OTPW)
*   [3 Použití](#Pou.C5.BEit.C3.AD)

## Instalace

Instalujte [otpw](https://aur.archlinux.org/packages/otpw/) balíček z AUR.

## Konfigurace pro ssh přihlášení

### PAM Konfigurace

Vytvořte PAM konfigurační soubor pro otpw:

 `/etc/pam.d/ssh-otpw` 
```
auth sufficient pam_otpw.so
session optional pam_otpw.so

```

Dále upravte PAM kofigurační soubor pro ssh aby zahrnul otpw. Pokud chcete zakázat statické heslo zakomentujte druhý tučný řádek.Zde je upravená verze `/etc/pam.d/sshd` jako vzor:

 `/etc/pam.d/sshd` 
```
#%PAM-1.0
#auth     required  pam_securetty.so     #zakázat vzdálený root

**auth      include   ssh-otpw**
**#auth      include   system-remote-login #POZNÁMKA:Toto musí být zneplatněno pro zakázání přihlášní heslem.**
account   include   system-remote-login
password  include   system-remote-login
session   include   system-remote-login

```

### Konfigurace sshd

OTPW používá interaktivní přihlášení pro SHH připojení, které je povoleno přidáním těchto řádek do `/etc/ssh/sshd_config`:

```
UsePAM yes
UsePrivilegeSeparation yes
ChallengeResponseAuthentication yes

```

**Note:** Ujistěte se, že nepřidáte nadbytečnou nebo konfliktní řádky konfigurace do `/etc/ssh/sshd_config`! Například buďte si jistí že tam nejsou dva řádky s UsePAM directivou,atp.

Chcete-li povolit také přihlašování statickými hesly, zajistěte, aby {{ic|/etc/ssh/sshd_config} obsahoval následující řádek:

```
PasswordAuthentication yes

```

V opačném případě jej nastavte na **no**. Viz výše uvedené informace o úpravě souboru `/etc/pam.d/sshd`, abyste úplně deaktivovali autorizaci statickým heslem, neboť PAM jinak povolí statické heslo, pokud OTPW selže (např. Když uživatel vyčerpá hesla).

Pokud povolíte ověření pomocí hesla, pak po selhání jedné metody ověření se klienti ssh vrátí zpět do druhé. Všimněte si, že ve výchozím nastavení ssh umožňuje tři pokusy o heslo na přihlašovací metodu.

### Konfigurace OTPW

OTPW je nakonfigurován nezávisle pro každý uživatelský účet. Pokud daný účet nemá OTPW nakonfigurován, bude tento účet jednoduše používat statické heslo jako obvykle. Chcete-li nakonfigurovat protokol OTPW pro účet, spusťte jej jako:

```
$ otpw-gen > ~/otpw_passwords

```

`otpw-gen` požádá o předponu hesla, která musí být zadána na začátku všech otpw hesel. Tímto způsobem zajistíte, že pokud někdo jiný dostane váš seznam OTPW, nemůže ho použít k přihlášení k vašemu účtu, dokud nebude vědět i vaší předponu.

Po spuštění výše uvedeného příkazu by měl být v domovském adresáři uživatele soubor `otpw_passwords`, který obsahuje všechna uživatelská hesla OTPW. Bude také obsahovat soubor `~/.otpw`, který obsahuje hashe hesel. `otpw_passwords` lze při přihlášení tisknout a odkazovat.

## Použití

Po dokončení výše uvedené konfigurace by měl ssh automaticky používat OTPW pro uživatele, kteří jej nakonfigurovali. Příkaz k přihlášení OTPW vypadá takto:

```
Password 041:

```

Chcete-li se přihlásit, jednoduše vyhledejte heslo 41 v seznamu {{Ic|otpw_passwords}, například:

```
041 lYr0 g7QR

```

A zadejte předponu, po které následují obě poloviny hesla. Mezery jsou zde pro čitelnost a mohou nebo nemusí být zahrnuty do zadaného hesla. Nezadávejte mezeru mezi předčíslí a heslo.

Chcete-li zadat klientovi ssh, který způsob přihlášení chcete použít, přidejte `-o PreferredAuthentication=keyboard-interactive` pro použití OTPW nebo `-o PreferredAuthentication=password` statického hesla. Tyto volby mohou být také uvedeny v `~/.ssh/config` per-server.