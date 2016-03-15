## Contents

*   [1 Wstęp](#Wst.C4.99p)
*   [2 Instalacja](#Instalacja)
*   [3 Konfiguracja](#Konfiguracja)
*   [4 Obconf](#Obconf)
*   [5 Obmenu](#Obmenu)
*   [6 LXAppearance](#LXAppearance)
*   [7 Nitrogen](#Nitrogen)
*   [8 Informacje końcowe](#Informacje_ko.C5.84cowe)
*   [9 Zobacz również](#Zobacz_r.C3.B3wnie.C5.BC)

## Wstęp

Openbox jest minimalistycznym, bardzo konfigurowalnym menadżerem okien. Dzięki swej lekkości może być używany na starszych komputerach. Openbox został oparty na kodzie Blackbox 0.65.0, jednakże został całkowicie przepisany w języku programowania C i wersja 3.0 nie posiada już nic z kodu Blackboksa.

Najważniejsze cechy:

*   Szybszy i wydajniejszy od swoich konkurentów;
*   Do działania potrzebuje mniej niż 5 MB pamięci RAM;
*   Pliki konfiguracyjne w formacie XML;
*   Wysoko konfigurowalne akcje myszy i klawiatury;
*   Może być zamiennikiem innych menedżerów okien takich jak Kwin czy Metacity.

## Instalacja

Openbox dostępny jest w oficjalnych repozytoriach, zatem wystarczy wpisać poniższe polecenie:

```
# pacman -Sy openbox

```

Możemy również od razu ściągnąć pakiet z tematami graficznymi:

```
# pacman -S openbox-themes

```

## Konfiguracja

Po zainstalowaniu Openboksa tworzymy lub modyfikujemy plik `~/.xinitrc` dodając do niego poniższy wpis (wszystkie inne linie komentujemy):

 `~/.xinitrc`  `exec openbox-session` 

Najprostszą metodą dokonania podstawowej konfiguracji jest skopiowanie przykładowych plików do katalogu `~/.config/openbox/`, a następnie dostosowanie ich do swoich potrzeb (jako zwykły użytkownik):

```
$ mkdir -p ~/.config/openbox/
$ cp /etc/xdg/openbox/rc.xml ~/.config/openbox/rc.xml
$ cp /etc/xdg/openbox/menu.xml ~/.config/openbox/menu.xml

```

Jeżeli chcemy, aby dany program uruchamiał się wraz z systemem, musimy dodać odpowiedni wpis do pliku `~/.config/openbox/autostart`.

## Obconf

Pakiet `obconf` służy do graficznej edycji pliku `~/.config/openbox/rc.xml`.

```
# pacman -S obconf

```

## Obmenu

Pakiet `obmenu` służy zaś do graficznej edycji `~/.config/openbox/menu.xml`.

```
# pacman -S obmenu

```

## LXAppearance

LXAppearance pomoże nam w zarządzaniu motywami GTK2/GTK+:

```
# pacman -S lxappearance

```

## Nitrogen

Nitrogen służy do ustawienia tapety pulpitu.

```
# pacman -S nitrogen

```

Następnie wybieramy odpowiednią tapetę:

```
$ nitrogen /ścieżka/do/katalogu/z/tapetami

```

Wybieramy tapetę, zapisujemy i dodajemy poniższą linijkę do pliku `~/.config/openbox/autostart.sh`:

```
nitrogen --restore &

```

## Informacje końcowe

Aby dowiedzieć się więcej o tym menedżerze, przejdź do angielskojęzycznego artykułu [Openbox](/index.php/Openbox "Openbox").

## Zobacz również

*   [Strona projektu](http://icculus.org/openbox/)
*   [Zbiór motywów graficznych](http://www.box-look.org/)