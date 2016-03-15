## Contents

*   [1 Wstęp](#Wst.C4.99p)
*   [2 KDE 4](#KDE_4)
*   [3 KDE 5](#KDE_5)
*   [4 KDM](#KDM)
*   [5 Uruchamianie KDE 4 i 5 bez KDM](#Uruchamianie_KDE_4_i_5_bez_KDM)
*   [6 Informacje końcowe](#Informacje_ko.C5.84cowe)

## Wstęp

KDE to jedno z największych środowisk graficznych. Zostało napisane głównie przy użyciu biblioteki Qt. Ma stosunkowo duże wymagania sprzętowe, ale za to oferuje bogatą ilość opcji konfiguracyjnych, personalizacyjnych i programów narzędziowych przydatnych podczas normalnej pracy.

## KDE 4

KDE 4 (znany też jako KDE SC 4, KDE Software Compilation 4) to czwarta stabilna wersja środowiska graficznego KDE. Wersja ta to tak na prawdę zestaw aplikacji, w których znajduje się Plazma, "prawdziwe" środowisko graficzne KDE 4\. KDE 4 bazuje na Qt 4\. Flagowym stylem KDE 4 jest Oxygen.

Instalacja KDE 4 w najnowszym Archu:

Instalacja pełnego środowiska KDE, wraz ze wszystkimi aplikacjami i polskim językiem interfejsu. Niezalecane, ponieważ zajmuje bardzo dużo miejsca i instaluje dużo aplikacji których użytkownik może nawet nigdy nie używać:

```
# pacman -S kde kde-l10n-pl

```

Instalacja minimalnego środowiska KDE SC z Plazmą i kilkoma domyślnymi aplikacjami kolekcji programów KDE 4: Dolphin (menedżer plików), Konsole (konsola/terminal), Kate (edytor tekstu):

```
# pacman -S kdebase-workspace kdebase-konsole kdesdk-kate kde-l10n-pl

```

## KDE 5

KDE 5 to następna wersja KDE, następca KDE 4\. KDE 5, w przeciwieństwie do KDE SC 4 i poprzednich, został podzielony na 3 odrębne części które rozwijają się w swoim czasie: Szkielety/Biblioteki (Frameworks), Pulpit (Workspace) i Aplikacje (Apps). Domyślnym środowiskiem graficznym KDE 5 jest Plazma 5, znana także jako Plazma 2 i Plasma Next. Biblioteki, pulpit i aplikacje KDE 5 są nadal w trakcie tworzenia. Biblioteki i pulpit nie są jeszcze całkiem stabilne, a aplikacje nie są jeszcze użyteczne. Plazmę Next i Szkielety KDE 5 można zainstalować z repozytorium extra/. Zestaw KDE 5 bazowany jest na Qt 5\. Wprowadza on całkowicie nowy płaski styl aplikacji Breeze.

Instalacja **niestabilnych** szkieletów i pulpitu KDE 5 w najnowszym Archu:

```
# pacman -S plasma-next

```

Aplikacje z KDE 4 mogą być używane obok Plazmy 5\. Integracja aplikacji Qt 4 ze stylem Breeze może zostać uzyskana po zainstalowaniu pakietu breeze-kde4\. Styl Breeze dla GTK 2 i/lub 3 nie został jeszcze stworzone.

## KDM

KDM to menedżer logowania dla środowiska graficznego KDE 4\. Na czas dzisiejszy nie wspiera on KDE 5\. Został zaprojektowany jako prostsza w konfiguracji alternatywa dla domyślnego w Xorg menedżera XDM.

```
# pacman -S kdm

```

Aby uruchomić KDM używając Systemd, należy wydać komendę poniżej:

```
# systemctl start kdm

```

## Uruchamianie KDE 4 i 5 bez KDM

Możliwe jest uruchamianie środowisk graficznych KDE 4 i KDE 5 bez użycia KDM lub innych menedżerów sesji. Dzięki temu można uruchomić serwer graficzny Xorg bez uprawnień administratora (roota), dzięki czemu istnieje mniejsza szansa na wykorzystywanie luk w tym serwerze graficznym. Aby to zrobić, należy użyć programu Xinit:

```
# pacman -S xorg-xinit

```

Po instalacji programu, należy utworzyć plik .xinitrc w katalogu domowym i wypełnić go tą zawartością:

```
exec startkde

```

Teraz wystarczy zapisać plik, wyjść z edytora i uruchomić:

```
# startx

```

z konta użytkownika, u którego utworzono plik .xinitrc.

**Uwaga**: Konfiguracja systemowa programu Xinit może być przeprowadzona edytując plik /etc/X11/xinit/xinitrc lub edytując pliki w katalogu /etc/X11/xinit/xinitrc.d.

## Informacje końcowe

Aby dowiedzieć się więcej o tym środowisku, przejdź do angielskojęzycznego artykułu [KDE](/index.php/KDE "KDE").