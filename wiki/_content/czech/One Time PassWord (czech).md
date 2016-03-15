**One Time PassWord** (**OTPW**) je PAM modul, který zprostředkuje použití hesel "na jedno použití" k přihlášení do systému. Tohle se hodí zejména v kontextu Secure shell, a to umožnění přihlášení z veřejných nebo sdílených počítačů, za pomoci jednorázových hesel, které nebudou nikdy fungovat znova.

Instrukce pro instalaci OTPW a konfiguraci SSH používat OTPW k přihlášení jsou níže.

## Contents

*   [1 Instalace](#Instalace)
*   [2 Konfigurace pro ssh přihlášení](#Konfigurace_pro_ssh_p.C5.99ihl.C3.A1.C5.A1en.C3.AD)
    *   [2.1 PAM Konfigurace](#PAM_Konfigurace)
    *   [2.2 sshd Configuration](#sshd_Configuration)

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

### sshd Configuration

OTPW používá interaktivní přihlášení pro SHH připojení, které je povoleno přidáním těchto řádek do `/etc/ssh/sshd_config`:

```
UsePAM yes
UsePrivilegeSeparation yes
ChallengeResponseAuthentication yes

```

**Note:** Ujistěte se, že nepřidáte nadbytečnou nebo konfliktní řádky konfigurace do `/etc/ssh/sshd_config`! Například buďte si jistí že tam nejsou dva řádky s UsePAM directivou,atp.

Pokud si přejete používat také statická hesla, ujistěte se, že obsahuje řádek jako tento: