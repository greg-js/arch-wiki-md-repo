Mathematica è un programma commerciale usato in campo scientifico, matematico e ingegneristico. Qui viene spiegato come installarlo.

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Mathematica 6](#Mathematica_6)
        *   [1.1.1 Montare l'iso](#Montare_l.27iso)
        *   [1.1.2 Eseguire l'installer](#Eseguire_l.27installer)
        *   [1.1.3 Font](#Font)
        *   [1.1.4 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [1.2 Mathematica 7](#Mathematica_7)
    *   [1.3 Mathematica 8](#Mathematica_8)
        *   [1.3.1 Mathematica 8.0.1](#Mathematica_8.0.1)
*   [2 Altre risorse](#Altre_risorse)

## Installazione

### Mathematica 6

#### Montare l'iso

Un modo per montare l'iso di Mathematica è creare **/media/iso** e aggiungere la seguente riga a fstab:

```
/<location/of/mathematica.iso> /media/iso iso9660 exec,ro,user,noauto,loop=/dev/loop0   0 0

```

Ora è pssibile montarla con:

```
mount /media/iso

```

#### Eseguire l'installer

È possibile avviare l'installer andando in:

```
/Unix/Installer

```

Eseguire ./MathInstaller con:

```
sh ./MathInstaller

```

**Nota:** Se non si piazza **sh** davanti, poi si otterrà un errore riguardo a un cattivo interprete

#### Font

Aggiungere le cartelle contenenti i font Type1 e BDF alla propria FontPath.

#### Risoluzione dei problemi

Se si hanno problemi di resa dei font nei quali certi simboli non vengono mostrati (es. "/" appare come un rettangolo), provare a disinstallare il pacchetto "mathematica-fonts".

### Mathematica 7

Mathematica 7 è più facile da installare.

```
tar xf Mathematica-7.0.1.tar.gz
cd Unix/Installer
./MathInstaller

```

Seguire le istruzioni.

Per gli utenti KDE l'icona di Mathematica può apparire nella categoria Oggetti smarriti. Per risolvere eseguire il seguente comando da amministratore:

```
sudo ln -s /etc/xdg/menus/applications-merged /etc/xdg/menus/kde-applications-merged

```

### Mathematica 8

#### Mathematica 8.0.1

C'è un pacchetto in [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") per Mathematica 8.0.1-2 reperibile [qui](https://aur.archlinux.org/packages.php?ID=47077). Lo script per l'installazione Mathematica_8.0.1_LINUX.sh è richiesto.

## Altre risorse

*   [Sito ufficiale (en)](http://www.wolfram.com/mathematica/)
*   [Supporto ufficiale (en)](http://www.wolfram.com/support/)