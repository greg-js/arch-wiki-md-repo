Wine je aplikace sloužící ke spuštění programů pro Windows pod prostředím Gnu/Linuxu (a jiných POSIX systémech). Wine je často chybně označováno za emulátor, ikdyž se proti této chybě bráni již v názvu - wine je totiž zkratka, celé jméno zní Wine Is Not Emulator

## Contents

*   [1 Instalace](#Instalace)
*   [2 Konfigurace](#Konfigurace)
*   [3 Spuštění aplikace](#Spu.C5.A1t.C4.9Bn.C3.AD_aplikace)
*   [4 Odkazy](#Odkazy)

### Instalace

```
pacman -S wine

```

### Konfigurace

Konfiguraci wine spustíte pomocí příkazu

```
winecfg

```

Při prvním spuštění nějakého programu přes wine se vytvoří i adresář ~/.wine kam i se standardně instalují programy - adresář ~/.wine/drive_c v aplikacích spuštěných přez wine představuje disk C - C:\>

Pokud vám ve wine špatně fungují písma, nejspíše je to tím že nemáte balík ttf-ms-fonts

```
pacman -S ttf-ms-fonts

```

### Spuštění aplikace

```
wine apliakce.exe

```

Při problémech s DirectX spustit s parametrem -opengl

## Odkazy

*   [Oficiální web wine](http://www.winehq.com/)
*   [Databáze aplikací fungujících přes wine](http://appdb.winehq.org/)