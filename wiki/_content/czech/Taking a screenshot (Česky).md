_poznamka_ Pouzivam xfce, takze se omlouvam za odlisnosti (jsou-li) v jinem desctopovem prostredi.

# pomoci apletu na panelu

Moznost pridat si aplet na panel je velmy jednoducha a dobre se pouziva, avsak nepouzitelna, chceme-li udelat screenshot v okamziku, ze mame spusteny program na celou obrazovku, takze je aplet skryty. aplet pridame kliknutim pravym tlacitke mysi na panel -> pridat nove polozky (ci pridat aplet) pak uz jen staci na nej kliknout v okamziku, kdy chceme obrazovku vyfotit. Program se nas zepta kam a pod jakym nazvem chceme snimek ulozit.

# nastaveni klavesnicove zkratky

menu->nastaveni->klavesnice->klavesnicove zkratky zadame prikaz a klasevu, ci kombinaci klaves, ktere kdyz stiskneme, tak se prikaz vykona.

jedna moznost je zadat prikaz

```
# import -window root obrazek.png

```

kde _obrazek_ je smeno souboru pod jakym se screenshot ulozi a _png_ format. Pri teto variante se screenshot ulozi do vaseho domovskeho adresare. Chcemeli ho jinam, tak staci zadat cestu.

```
# import -window root /home/jirka/screenshot/obrazek.png

```

Nyni se mi sreenshot ulozi do adresare ~/screenshot

Tato varianta je ovsem neprakticka, protoze zadavame jmeno souboru, tudiz kdykoli udelam dalsi screenshot, tak se predchozi soubor prepise. (Pokud jsme ho neprejmenovali) Tedy pro nastaveni klavesnicove zkratky je lepsi jiny prikaz, ale na ten si musime nainstalovat program **scrot**

tedy

```
# pacman -S scrot

```

a zadame prikaz

```
# scrot -e 'mv $f ~/screenshot'

```