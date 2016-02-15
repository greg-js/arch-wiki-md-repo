| **Streszczenie**  |
| Objaśnienie grup pakietów i meta-pakietów w KDE. |
| **Podobne artykuły** |
| [KDE](/index.php/KDE "KDE") |

Od wersji KDE SC 4.3, dla każdej aplikacji dostarczane są oddzielne pakiety. W artykule opisano koncepcję grup i meta-pakietów.

## Contents

*   [1 Terminologia](#Terminologia)
*   [2 Korzystanie z grup pakietów](#Korzystanie_z_grup_pakiet.C3.B3w)
    *   [2.1 Dlaczego warto korzystać z grup?](#Dlaczego_warto_korzysta.C4.87_z_grup.3F)
        *   [2.1.1 Zalety](#Zalety)
        *   [2.1.2 Wady](#Wady)
    *   [2.2 Kto powinien korzystać z grup?](#Kto_powinien_korzysta.C4.87_z_grup.3F)
*   [3 Korzystanie z meta-pakietów](#Korzystanie_z_meta-pakiet.C3.B3w)
    *   [3.1 Dlaczego warto korzystać z meta-pakietów?](#Dlaczego_warto_korzysta.C4.87_z_meta-pakiet.C3.B3w.3F)
        *   [3.1.1 Zalety](#Zalety_2)
        *   [3.1.2 Wady](#Wady_2)
    *   [3.2 Kto powinien korzystać z meta-pakietów?](#Kto_powinien_korzysta.C4.87_z_meta-pakiet.C3.B3w.3F)
*   [4 Listy pakietów członkowskich.](#Listy_pakiet.C3.B3w_cz.C5.82onkowskich.)

## Terminologia

	**moduł**

	Kod źródłowy kompilacji oprogramowania KDE podzielony jest na kilka kategorii, zwanych modułami. Są nimi np. kdebase, kdeutils itp. Projekt KDE wydaje jedno archiwum źródłowe na moduł. Szczegóły patrz [Coordinator List](http://techbase.kde.org/Projects/Release_Team#Coordinator_List).

	**grupa pakietów**

	Jest to po prostu grupa pakietów. [Pacman](/index.php/Pacman "Pacman") umożliwia wybór wielu pakietów według podziału na grupy podczas procesu ich instalacji bądź usuwania.

	**meta-pakiety**

	meta-pakiet jest pustym pakietem, który tylko łączy kilka pakietów używając zależności.

## Korzystanie z grup pakietów

Istnieją grupy dla każdego modułu KDE jak np. **kdebase**, **kdeutils** itp. Instalując grupę pakietów zostaną zainstalowane wszystkie pakiety należące do danego modułu na czas danej instalacji. Na przykład, aby zainstalować wszystkie pakiety, które są częścią modułu jak np. **kdebase** lub **kdeutils** w aktualnym wydaniu wprowadź:

```
# pacman -S kdebase kdeutils ...

```

Poza tym istnieje grupa **kde** , w skład której wchodzą wszystkie inne grupy KDE. Instalacja grupy pakietów **kde** spowoduje instalację aktualnej kompilacji w całości:

```
# pacman -S kde

```

### Dlaczego warto korzystać z grup?

#### Zalety

*   Wykorzystanie grup umożliwia łatwiejszą instalację lub usunięcie zestawu pakietów. Pozwala to na użycie tylko jednego polecenia (jak powyżej) do instalacji bądź usunięcia wszystkich pakietów w module.
*   Nie istnieją twarde zależności pomiędzy grupą i jej pakietami. Oznacza to, że nie ma potrzeby zachowywania wszystkich pakietów należących do zainstalowanej grupy. Można swobodnie usuwać pakiety członkowskie bez wpływania na inne pakiety członkowskie należące do tej samej grupy.

#### Wady

*   [Pacman](/index.php/Pacman "Pacman") nie zainstaluje żadnych nowych pakietów, które zostaną dodane do grupy w późniejszym terminie. Na przykład, jeśli następne wydanie kompilacji oprogramowania KDE będzie zawierało nowe aplikacje w jednym lub więcej modułach, to te nowe aplikacje nie zostaną automatycznie zainstalowane podczas aktualizacji systemu. Należy wtedy ręcznie zainstalować te nowe pakiety. Aby temu zaradzić, można skorzystać z meta-pakietów (patrz następna sekcja).

### Kto powinien korzystać z grup?

Instalujmy grupy pakietów, jeśli chcemy wykorzystywać tylko niektóre moduły z aktualnej kompilacji oprogramowania KDE. Grupy okażą się przydatne dla tych użytkowników, którzy chcą zachować tylko niektóre pakiety z grupy decydując się na usunięcie pozostałych.

## Korzystanie z meta-pakietów

Podobnie jak w przypadku grup istnieją meta-pakiety dla każdego modułu KDE, jak **kde-meta-kdebase**, **kde-meta-kdeutils** itp. Instalacja meta-pakietów zapewni tak instalację jak i aktualizację wszystkich pakietów należących do modułu. Jeśli w następnych wersjach zostaną dodane nowe aplikacje do modułu, będą one automatycznie instalowane przy aktualizacji systemu. Aby zainstalować konkretny moduł jak np. **kdebase** lub **kdeutils** wykorzystując meta-pakiety wprowadź:

```
# pacman -S kde-meta-kdebase kde-meta-kdeutils ...

```

Oprócz tego istnieje grupa **kde-meta** która obejmuje wszystkie meta-pakiety KDE. Instalacja grupy **kde-meta** spowoduje zainstalowanie całej kompilacji oprogramowania KDE:

```
# pacman -S kde-meta

```

### Dlaczego warto korzystać z meta-pakietów?

#### Zalety

*   Podobnie jak grupy, meta-pakiety ułatwiają instalację i utrzymanie pakietów. Pozwala to na wykorzystanie jednego polecenia (jak powyżej) do instalacji wszystkich pakietów z modułu.
*   Wykorzystanie meta-pakietów zapewni automatyczną instalację wszystkich nowych pakietów członkowskich [pacman](/index.php/Pacman "Pacman") podczas aktualizacji systemu. Emuluje to zachowanie wcześniej używanego monolitycznego zestawu pakietów poprzedzających wersję KDE SC 4.3.

#### Wady

*   Meta-pakiety utrzymują twarde zależności pomiędzy wszystkimi pakietami będącymi ich częściami. Oznacza to, że nie da się swobodnie usunąć pakietów, które są częściami meta-pakietu bez uprzedniego usunięcia najpierw jego samego. Jeśli np. zainstalowaliśmy kde-meta-kdebase a następnie chcemy usunąć pakiet członkowski taki jak **kdebase-kwrite**, musimy najpierw usunąć meta-pakiet zanim będziemy w stanie usunąć pakiet członkowski:

```
# pacman -R kde-meta-kdebase
# pacman -R kdebase-kwrite

```

Czyniąc tak nie usuniemy innych pakietów członkowskich z meta-pakietu **kde-meta-kdebase**, jednak pozbawiamy się w ten sposób możliwości automatycznego dodawania nowych pakietów w danym module (co może się zdarzyć w następnych wydaniach) przy uaktualnianiu systemu poleceniem pacman -Syu. Niemniej reinstalacja meta-pakietu **kde-meta-kdebase** w dowolnym momencie przywraca z powrotem jego monolityczne zachowanie.

Jeśli mamy zainstalowany pakiet kde-meta, możemy usunąć naraz wszystkie meta-pakiety używając polecenia:

```
# pacman -R kde-meta

```

Usuniemy w ten sposób tylko meta-pakiety, bez pakietów członkowskich.

### Kto powinien korzystać z meta-pakietów?

Skorzystajmy z meta-pakietów, jeśli mamy zamiar zainstalować całą kompilację oprogramowania KDE, a także gdy instalujemy jeden lub więcej modułów w całości. Zapewni to nam płynną aktualizację poprzez automatyczne dodawanie nowo podzielonych pakietów z kolejnych wydań.

## Listy pakietów członkowskich.

Aby otrzymać pełną listę aplikacji KDE wprowadź polecenie:

```
pacman -Sg kde

```

Otrzymywanie pełnej listy meta-pakietów:

```
pacman -Sg kde-meta

```

Otrzymywanie listy wszystkich grup modułów KDE:

```
for i in $(pacman -Sqg kde-meta); do echo ${i#kde-meta-};done

```

Otrzymywanie listy wszystkich pakietów KDE wraz z ich grupami modułów:

```
for i in $(pacman -Sqg kde-meta); do pacman -Sg ${i#kde-meta-};done

```

Możemy także skorzystać z interfejsu sieciowego pod adresem [archlinux.de](https://www.archlinux.de/?page=Packages;group=5) do przeglądania grup pakietów.