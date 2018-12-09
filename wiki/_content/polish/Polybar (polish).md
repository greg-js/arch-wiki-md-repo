[polybar](https://github.com/jaagr/polybar) jest szybkim i prostym do używania narzędziem do tworzenia paska statusu. Program ma na calu być łatwo dostosowywalnym, wykorzystującym wiele modułów, które umożliwiają szeroki zakres funkcji (edytowalnych), takich jak wyświetlanie obszarów roboczych, daty czy głośności systemowej. Polybar jest wyjątkowo przydatny dla [Window manager](/index.php/Window_manager "Window manager")ów które mają ograniczony panel lub wcale go nie mają jak np [awesome](/index.php/Awesome "Awesome") czy [i3](/index.php/I3 "I3"). Polybar również może byc używany na pełnych [środowiskach graficznych](/index.php/Desktop_environment "Desktop environment") jak [Plasma (Polski)](/index.php/Plasma_(Polski) "Plasma (Polski)").

## Contents

*   [1 Instalacja](#Instalacja)
*   [2 Konfiguracja](#Konfiguracja)
    *   [2.1 Uruchamianie Polybara](#Uruchamianie_Polybara)
    *   [2.2 Przykładowa konfiguracja](#Przykładowa_konfiguracja)
    *   [2.3 Uruchamianie korzystając z WM](#Uruchamianie_korzystając_z_WM)
        *   [2.3.1 bspwm](#bspwm)
        *   [2.3.2 i3](#i3)
*   [3 Zobacz również](#Zobacz_również)

## Instalacja

[Zainstaluj](/index.php/Zainstaluj "Zainstaluj") pakiet [polybar](https://aur.archlinux.org/packages/polybar/) lub [polybar-git](https://aur.archlinux.org/packages/polybar-git/) dla wersji rozwojowej.

## Konfiguracja

#### Uruchamianie Polybara

Polybar może być uruchomiony korzystając z:

```
Usage: polybar [OPTION]... BAR

  -h, --help               Display this help and exit
  -v, --version            Display build details and exit
  -l, --log=LEVEL          Set the logging verbosity (default: WARNING)
                           LEVEL is one of: error, warning, info, trace
  -q, --quiet              Be quiet (will override -l)
  -c, --config=FILE        Path to the configuration file
  -r, --reload             Reload when the configuration has been modified
  -d, --dump=PARAM         Print value of PARAM in bar section and exit
  -m, --list-monitors      Print list of available monitors and exit
  -w, --print-wmname       Print the generated WM_NAME and exit
  -s, --stdout             Output data to stdout instead of drawing it to the X window
  -p, --png=FILE           Save png snapshot to FILE after running for 3 seconds

```

Jednak prawdopodobnie będziesz chciał uruchomić Polybar za pomocą procedury bootstrap menedżera okien. Zobacz [#Uruchamianie korzystając z WM](#Uruchamianie_korzystając_z_WM)

#### Przykładowa konfiguracja

Bardzo podstawowa konfiguracja polybara może wyglądać mniej więcej tak:

```
[bar/mybar]
modules-right = date

[module/date]
type = internal/date
date = %Y-%m-%d%
```

Definiuje panel nazwany `mybar` z modułem `date`.

Domyślnie polybar zainstaluje również przykładową konfigurację z wieloma wstępnie skonfigurowanymi modułami w `/usr/share/doc/polybar/config`

**Note:** Przykładowa konfiguracja nie jest zaprojektowana do pracy out of the box dla wszystkich, musisz zmodyfikować ją, żeby polybar działał z twoim komputerem

#### Uruchamianie korzystając z WM

Stwórz [plik wykonywalny](/index.php/Help:Reading_(Polski)#Stwórz_plik_wykonywalnym "Help:Reading (Polski)") zawierający logikę uruchamiania, na przykład `$HOME/.config/polybar/launch.sh`:

```
#!/bin/bash

# Terminate already running bar instances
killall -q polybar

# Wait until the processes have been shut down
while pgrep -u $UID -x polybar >/dev/null; do sleep 1; done

# Launch Polybar, using default config location ~/.config/polybar/config
polybar mybar &

echo "Polybar launched..."

```

Ten skrypt oznacza, że ponowne uruchomienie WM spowoduje również ponowne uruchomienie Polybar.

###### bspwm

Jeżeli korzystasz z [bspwm](/index.php/Bspwm "Bspwm"), dodaj poniższą linie do swojej konfiguracji bspwm:

```
$HOME/.config/polybar/launch.sh

```

###### i3

Jeżeli korzystasz z [i3](/index.php/I3 "I3"), dodaj poniższą linie do swojej konfiguracji i3:

```
exec_always --no-startup-id $HOME/.config/polybar/launch.sh

```

## Zobacz również

*   [Wiki Polybara na GitHubie](https://github.com/jaagr/polybar/wiki/)