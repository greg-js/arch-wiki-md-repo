Lenovo ThinkPad X201 jest 2 rdzeniowym (4 wątkowym) subnotebookiem produkowanym przez Lenovo. Aby dowiedzieć się więcej na jego temat sprawdź: [Thinkwiki](http://www.thinkwiki.org/wiki/Category:X201)

Arch działa świetnie na tym laptopie, jednak w pewnych przypadkach (np. ze względu na różne podzespoły stosowane w tym modelu) wymaga kilku interwencji użytkownika.

## Contents

*   [1 Grafika](#Grafika)
*   [2 Hibernation](#Hibernation)
*   [3 Oszczędzanie Energii](#Oszcz.C4.99dzanie_Energii)
    *   [3.1 Zmiana częstotliwości pracy procesora](#Zmiana_cz.C4.99stotliwo.C5.9Bci_pracy_procesora)
    *   [3.2 Zmniejszanie napięcia procesora](#Zmniejszanie_napi.C4.99cia_procesora)
    *   [3.3 Modem 3G](#Modem_3G)

## Grafika

Ze względu na to, że laptop ten występuje tylko ze zintegrowanym układem graficznym firmy Intel, Xorg najczęściej sam ładuje właściwy sterownik, bez żadnej dodatkowej konfiguracji. Jednak w przypadku problemów z wyświetlaniem, w dziale [Intel](/index.php/Intel "Intel") znajdziesz wszystkie potrzebne do rozwiązania problemów informacje.

Od wydania Mesy 9.0, na mobilnych układach o nazwie kodowej "Iron Lake" czasami mogą wystąpić problemy z wyświetlaniem grafiki, bądź nagłym zawieszeniem pulpitu. Angielskie źródła mówią o zawieszaniu się systemów, które do odzyskania sprawności, mogą wymagać nawet restartu systemu. W przypadku X201 problem ten występuje po hibernacji i jedynie przy menadżerze logowania GDM. Zabicie procesu GDM z innego terminala przywraca poprawne działanie systemu.

## Hibernation

Po zainstalowaniu i konfiguracji pakietu [pm-utils](https://www.archlinux.org/packages/?name=pm-utils) hibernacja i usypianie odbywa się bezproblemowo.

## Oszczędzanie Energii

### Zmiana częstotliwości pracy procesora

Po zainstalowaniu [cpupower](https://www.archlinux.org/packages/?name=cpupower) i uruchomieniu usługi procesor sam dostosowuje częstotliwość pracy, TurboCore również działa prawidłowo.

### Zmniejszanie napięcia procesora

W procesorach serii Core ix nie jest możliwa programowa ingerencja w napięcie procesora.

### Modem 3G

**Warning:** Poniższe porady mogą nie zadziałać, jeżeli przed podjęciem próby zainstalowania sterownika modemu, nie zostanie umieszczona karta SIM!

Modem 3G jest jedyną właściwie rzeczą, która w X201 nie działa zaraz po instalacji. Większość dystrybucji ma duży problem z jego obsługą. W tym laptopie występuje oficjalnie tylko jeden model modemu 3G, jest nim Qualcomm Gobi 2000\. Przede wszystkim w tej chwili nie spotkałem się z działającą konfiguracją [wvdial](https://www.archlinux.org/packages/?name=wvdial), ale jest i dobra informacja, modem na Archu świetnie działa w trybie graficznym!

Do prawidłowego działania i wykrywania modemu potrzebujemy menadżer sieci [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) oraz [modemmanager](https://www.archlinux.org/packages/?name=modemmanager). Po zainstalowaniu oprogramowania z oficjalnego repozytorium wykonujemy:

 `systemctl enable NetworkManager modemmanager` 

Następnie pobieramy i instalujemy [gobi-loader](https://aur.archlinux.org/packages/gobi-loader/).
Kolejnym krokiem jest pobranie sterowników pod Windows 7 ze strony producenta: (([http://support.lenovo.com/us/en/downloads/migr-72938](http://support.lenovo.com/us/en/downloads/migr-72938)))
Najlepszą metodą jest zainstalowanie pakietu za pomocą [wine](https://www.archlinux.org/packages/?name=wine), ponieważ spowoduje to wypakowanie potrzebnych nam elementów
Teraz **Koniecznie** wchodzimy na konto root za pomocą **su** i tworzymy katalog:

 `mkdir /usr/lib/firmware/gobi` 

Będąc na koncie root musimy skopiować 3 pliki, modemy montowane w X201 nie są brandowane, potrzebujemy więc skopiować do utworzonego katalogu plik:

- **amss.mbn** i **apps.mbn** z katalogu `./.wine/drive_c/Program\ Files\ \(x86\)/QUALCOMM/Images/Lenovo/UMTS/` 
- **UQCN.mbn** z katalogu `./.wine/drive_c/Program\ Files\ \(x86\)/QUALCOMM/Images/Lenovo/2/` 
Następnie uruchamiamy komputer ponownie, zaraz po tym w NetworkManagerze modem powinien zostać bez większych problemów wykryty, jeżeli tak się nie stało, wykonaj `rmmod qcserial` 

a następnie

 `modprobe qcserial` 

i odczekaj chwile.