## Contents

*   [1 Instalace](#Instalace)
*   [2 Nastavení](#Nastaven.C3.AD)
    *   [2.1 Server](#Server)
        *   [2.1.1 Klíče](#Kl.C3.AD.C4.8De)
        *   [2.1.2 Startujeme server](#Startujeme_server)
    *   [2.2 Klient](#Klient)
        *   [2.2.1 Arch Linux](#Arch_Linux)
        *   [2.2.2 Windows](#Windows)
        *   [2.2.3 Konfigurace](#Konfigurace)
*   [3 Spouštění](#Spou.C5.A1t.C4.9Bn.C3.AD)
    *   [3.1 Klávesové zkratky](#Kl.C3.A1vesov.C3.A9_zkratky)
    *   [3.2 Opuštění celoobrazovkového módu](#Opu.C5.A1t.C4.9Bn.C3.AD_celoobrazovkov.C3.A9ho_m.C3.B3du)
    *   [3.3 Tipy pro obnovení](#Tipy_pro_obnoven.C3.AD)
    *   [3.4 Oprava nastavení DPI](#Oprava_nastaven.C3.AD_DPI)
*   [4 Setting up non-KDE or Gnome desktop managers](#Setting_up_non-KDE_or_Gnome_desktop_managers)
    *   [4.1 Alternative fix](#Alternative_fix)
*   [5 Problems](#Problems)
    *   [5.1 Debug problems](#Debug_problems)
    *   [5.2 Authentication OK, but connection fails](#Authentication_OK.2C_but_connection_fails)
    *   [5.3 Key changes](#Key_changes)
    *   [5.4 Xorg 7](#Xorg_7)
    *   [5.5 Wrong password / No connection possible](#Wrong_password_.2F_No_connection_possible)
        *   [5.5.1 NX Crashes on session startup](#NX_Crashes_on_session_startup)
    *   [5.6 NX logo then blank screen](#NX_logo_then_blank_screen)

## Instalace

balíček je rozdělen do 2 částí:

*   freenx (server)
*   nxclient (klient)

## Nastavení

### Server

Server je přítomen v balíčku jménem 'freenx'.

*   Pro povolení přihlašování prosím přidejte balíček 'sshd' do pole daemonů v souboru /etc/rc.conf

Hlavní konfigurační soubor je umístěn zde:

```
/opt/NX/etc/node.conf

```

Pokud jako desktopové prostředí používáte KDE nebo Gnome, nemusíte měnit tento soubor, v tomto případě funfuje vše ve výchozím nastavení. Pokud používáte jiného okenního manažera jako třeba Fluxbox/Openbox nebo Xfce, možná budete muset tento soubor trochu pozměnit (viz níže).

#### Klíče

Klíče jsou používány k autentizaci klienta se serverem. Jako výchozí je při instalaci generována dvojice náhodných klíčů, jeden pro server a jeden pro klienta. Je třeba zkopírovat klientský klíč do každého klienta, pomocí kterého se budete chtít připojovat k serveru (ve Windows i v Linuxu).

Klientský klíč naleznete zde"

```
/opt/NX/home/nx/.ssh/client.id_dsa.key

```

Případně můžete použít výchozí klíč, který je poskztován NoMachine se všemi klienty. V tomto případě není třeba kopírova náhodně generovaný klíč do každého klienta. Aby server přijímal výchozí klientské klíče, zadejte tento příkaz::

```
/opt/NX/bin/nxsetup --install --setup-nomachine-key --clean --purge

```

Znovuvytvoření náhodně generovaných klíčů:

*   /opt/NX/bin/nxsetup --install --clean --purge

Přenesení nx klíčů do jiných serverů:

*   /opt/NX/home/nx/.ssh obsahuje soubory s klíči

```
 -rw------- 1 nx root  697  9\. Okt 12:55 authorized_keys
 -rw------- 1 nx root  668  9\. Okt 11:48 client.id_dsa.key
 -rw------- 1 nx root  609  9\. Okt 12:55 server.id_dsa.pub.key

```

*   Ulož tyto soubory.
*   Přidej tyto soubory do tvého serveeru, je třeba udržet stejná oprávnění, jména, skupiny a adresáře!

```
 # cp authorized_keys client.id_dsa.key server.id_dsa.pub.key /opt/NX/home/nx/.ssh/
 # chmod 600 /opt/NX/home/nx/.ssh/*
 # chown nx /opt/NX/home/nx/.ssh/*
 # chgrp root /opt/NX/home/nx/.ssh/*

```

*   Znovuvytvoření souboru known_hosts:

```
 # echo -n 127.0.0.1 > /opt/NX/home/nx/.ssh/known_hosts
 # cat /etc/ssh/ssh_host_rsa_key.pub >> /opt/NX/home/nx/.ssh/known_hosts
 # chmod 633 /opt/NX/home/nx/.ssh/known_hosts
 # chown nx /opt/NX/home/nx/.ssh/known_hosts
 # chgrp root /opt/NX/home/nx/.ssh/known_hosts

```

#### Startujeme server

Jaklime server běží a je připraven, nemusíš již nic ručně nastavovat. Jediná věc, která musí být spuštěna aby ses mohl přihlásit je sshd daemon.

Když zkontroluješ seznam procesů (`ps aux`) neuvidíš žádný běžící nxserver, ikdyž je spuštěný. To je protože nxserver je spouštěn přihlášením se do sshd jako speciální uživatel 'nx'. Tento uživatel byl nastaven jako shell pro užití nxserverem asi tak jako má normální uživatel výchozí bash shell.

### Klient

#### Arch Linux

Pacmanem získáme klienta:

```
pacman -S nxclient

```

#### Windows

Získáme klienta z domovské stránky nomachine: [http://nomachine.com](http://nomachine.com)

Tip: Nomachine směřuje k odstraňování starých klientů z jejich domovské stránky, pokud s určitým klientem tvé nastavení funguje, uschovej ho na bezpečném místě ;)

#### Konfigurace

Jak již bylo zmíněno výše, klient musí obsahovat správný klíč pro připojení k serveru. Pokud používáš náhodné klíče generované během instalace, je třeba je zkopírovat na do následujících lokací:

*   Windows: `<yourinstalldironwindows>/share/keys/client.id_dsa.key`
*   Arch Linux: `/opt/NX/share/keys/client.id_dsa.key`

Po přesunutí klíčů možná budeš chtít použít grafické rozhraní nxclient pro importování nových klíčů. V konfiguračním dialogu zmáčkni tlačítko 'Klíč...' a importuj noý klientský klíč.

## Spouštění

### Klávesové zkratky

```
CTR+ALT+F          Přepíná mezi normálním a celoobrazovkovým módem
CTRL+ALT+T         Zobrazí ukončovací, pozastavovací dialog
CTRL+ALT+M         Maximalizuje nebo minimalizuje okno 
CTRL+ALT+Myš     Přesunuje zobrazovanou část, takže můžeš vidět rozdílné části plochy 
CTRL+ALT+Šipky Přesunuje zobrazovanou část po určitých částech 
CTRL+ALT+S         It will activate "screen-scraping" mode, so all the GetImage
                   originated by the clients will be forwarded to the real
                   display. This should make happy those who love taking
                   screenshots ;-). By pressing the sequence again, nxagent
                   will revert to the usual "fast" mode.
CTRL+ALT+E         líné kódování obrázků
CTRL+ALT+Shift+ESC Nouzový exit a kill-window

```

### Opuštění celoobrazovkového módu

V pravém horním rohu okna je umístěn magický pixel. Pravým klikem na něj minimalizuješ okno aplikace.

### Tipy pro obnovení

*   Obnovení je poněkud experimentální, občas se může objevit pád po obnovení sezení. Musíš zjistit, které aplikace obnovení mají rády a které ne ;).
*   Obnovení mezi Linuxovým a Windows sezením nefunguje.
*   Když obnovení selháže, nech mu dojít čas a nepoužívej tlačítko 'Storno', ostatní sezení zůstanou a budou konzumovat RAM na serveru. Pro ukončení takových sezení použij program pro administraci sezení.

### Oprava nastavení DPI

Pokud máš rád stejné velikosti fontů a DPI na všech tvých klientských sezení, nastav zdroj X "Xft.dpi". Pro ukázku, vložení tohoto řádku do užiivatelova "~/.XResources" udělá jeho plochu 100dpi: Xft.dpi: 100

## Setting up non-KDE or Gnome desktop managers

Before following anything in this part, make sure the server working setup and accepting connections. This section only deals with problems once NXClient has logged on.

It is quite simple (once the server is setup) to connect to Gnome and KDE sessions, however connecting to other window managers (fluxbox, xfce, whatever) is slightly different.

Choosing "custom" and using a command like startx of startfluxbox will either result in a blank screen after the !M logo or the Client to present an error complaining about lack of a X server. A way around this is open a session with the command "startx", and the another with the command to start your window-manager-of-choice.

If you do not want to do this, you can start X by [installing a login manager like SLIM or XDM](/index.php/Display_manager "Display manager"). I would recomend using SLiM because of it's small size.

(Authors note: This is how I got fluxbox, xfce and others to work on my arch installation- however, I have now removed slim from inittab and set the run level back to 3, and yet I can still login perfectly with NXClient. Possibly try this if you get your system working this way, if like me you have a low memory machine.)

#### Alternative fix

A simple fix without resorting to the above seems to involve a simple edit to the config file. This should work for fluxbox/openbox/xfce or any other window manager that uses the **.xinitrc** startup file in a call to **startx**.

Simply edit the config file (as root):

```
/opt/NX/etc/node.conf

```

and change

```
#USER_X_STARTUP_SCRIPT=.Xclients

```

to

```
USER_X_STARTUP_SCRIPT=.xinitrc

```

Remember to remove the # symbol from the start of the line.

Then in the client under configuration settings, choose **Custom** as the desktop, and click on settings:

*   In the first group select - **`Run the default X client Script on server`**
*   In the second group select - **`New virtual desktop`**

## Problems

### Debug problems

Edit the nxserver config file:

```
 vi /opt/NX/etc/node.conf

```

Change:

```
 #SESSION_LOG_CLEAN=1

```

to

```
 SESSION_LOG_CLEAN=0

```

Then you can look/debug the log files in:

```
 $HOME/.nx/T-C-<hostname>-<display>-<session-id>

```

For succesfull connections and:

```
 $HOME/.nx/F-C-<hostname>-<display>-<session-id>

```

For failed ones.

### Authentication OK, but connection fails

If you are trying to startkde

```
 vi /opt/NX/etc/node.conf

```

And search for:

```
 COMMAND_START_KDE=startkde

```

Replace for:

```
 COMMAND_START_KDE=/opt/kde/bin/startkde

```

### Key changes

Change the key in GUI setup to new generated key.

### Xorg 7

Be aware that you have to remove the /usr/X11R6 directory, else strange things can happen.

### Wrong password / No connection possible

*   If you get always wrong password or no connection after authentication was done and you are sure that you typed it correct, check that your server can connect to itself using localhost by ssh and that it is not blocked either by /etc/hosts.deny or not allowed by /etc/hosts.allow.

*   If you messed up your key files, create new ones or fix the old ones, it's probably caused by a wrong known_hosts file.

#### NX Crashes on session startup

If your NX Client shows the NX logo then disappears with a Connection Problem dialog afterwards.

Then it could be due to missing fonts. Mostly applies if you have installed Arch Linux base and then installed freenx after without the whole X11 set.

Solution until FreeNX Dependencies is fixed is to install xorg-fonts-misc on your NX Server (pacman -S xorg-fonts-misc) and your NX should work.

Note: This does not apply to freenx 0.6.1-3 and above, fix has been incorporated in it and following versions.

### NX logo then blank screen

If you see the NX logo (!M) then a blank screen.

This problem can be solved by running a login manager- The problem is that X11 is not started, and it appears that "startx" or similar do not work from the freenx client. Follow these instructions to setup a login manager and load it at startup: [Display manager](/index.php/Display_manager "Display manager")