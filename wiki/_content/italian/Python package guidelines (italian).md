## Contents

*   [1 Nomenclatura del pacchetto](#Nomenclatura_del_pacchetto)
*   [2 Posizionamento dei file](#Posizionamento_dei_file)
*   [3 Note](#Note)
*   [4 Esempio](#Esempio)

## Nomenclatura del pacchetto

Per le librerie, utilizzare `python-*modulename*`. Per le applicazioni, usare il nome del programma. In ogni caso, il nome del pacchetto dovrà essere scritto completamente in minuscolo.

Le librerie scritte in Python 2 devono essere nominate `python2-*modulename*`.

## Posizionamento dei file

Molti pacchetti python sono installati tramite il sistema [distutils](http://docs.python.org/library/distutils.html) utilizzando **setup.py**, che installa i file nella directory `/usr/lib/python*<python version>*/site-packages/*pkgname*`.

## Note

Il parametro `--optimize=1` compila i `.pyo` in modo tale da poter essere tracciati da [pacman](/index.php/Pacman "Pacman").

Nella maggior parte dei casi, è necessario inserire `any` nell' array `arch` poichè molti pacchetti Python non dipendono dall' architettura.

Non installare in una directory chiamata `tests`, in quanto può facilmente andare in conflitto con altri pacchetti Python (ad esempio: `/usr/lib/python2.7/site-packages/tests/`).

## Esempio

Un esempio di PKGBUILD si può trovare in `/usr/share/pacman/PKGBUILD-python.proto`, contenuto nel pacchetto [abs](https://www.archlinux.org/packages/?name=abs)