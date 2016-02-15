Installazione e uso di Intel® C++ Composer XE (formerly Intel® C++ Compiler Professional Edition) per Linux sotto Arch.

## Contents

*   [1 Prima di iniziare](#Prima_di_iniziare)
*   [2 Creazione del pacchetto e installazione](#Creazione_del_pacchetto_e_installazione)
*   [3 Using icc with makepkg](#Using_icc_with_makepkg)
    *   [3.1 Metodo 1](#Metodo_1)
*   [4 icc CFLAGS](#icc_CFLAGS)
    *   [4.1 -xX](#-xX)
    *   [4.2 -Ox](#-Ox)
    *   [4.3 -w](#-w)
*   [5 Software compilato con Intel](#Software_compilato_con_Intel)

## Prima di iniziare

**Warning:** I pacchetti compilati con icc dipenderanno da **intel-openmp** per poter essere eseguiti. Mentre **intel-openmp** dipende da **intel-compiler-base**; gli utenti devono avere entrambi i panchetti installati!

## Creazione del pacchetto e installazione

[intel-parallel-studio-xe](https://aur.archlinux.org/packages/intel-parallel-studio-xe/) è disponibile su [AUR](/index.php/AUR "AUR"). Per poter costruire questo pacchetto è necessario ottenere una licenza per uso non commerciale direttamente dal sito di Intel [[registration](https://registrationcenter.intel.com/RegCenter/AutoGen.aspx?ProductID=1517&AccountID=&EmailID=&ProgramID=&RequestDt=&rm=NCOM&lang=)] che dovrà essere copiata nella $startdir prima di eseguire il makepkg. L'attuale PKGBUILD assembla 8 pachetti:

*   **intel-compiler-base** - Intel C/C++ compiler and base libs
*   **intel-fortran-compiler** - Intel fortran compiler and base libs (only Parallel Studio XE)
*   **intel-openmp** - Intel OpenMP Library
*   intel-idb- Intel C/C++ debugger
*   intel-ipp - Intel Integrated Performance Primitives
*   intel-mkl - Intel Math Kernel Library (Intel® MKL)
*   intel-sourcechecker - Intel Source Checker
*   intel-tbb - Intel Threading Building Blocks (TBB)

**Note:** Un ambiente di lavoro minino richiede i pachetti **intel-compiler-base** e **intel-openmp**; se si desidera pure il compilatore fortran si deve installare **intel-fortran-compiler**.

## Using icc with makepkg

**Note:** Non tutti i pacchetti si possono compilare coi compilatori intel senza aver prima modificato i sorgenti.

Attualmente non ci sono guide ufficiali per usare icc. Questa sezione è intesa per ricevere i suggerimenti degli utenti. Se lo ritieni necessario apri una nuova sottosezione in questa pagina o completa quelle esistenti.

### Metodo 1

Modifica `/etc/makepkg.conf` inserendo il seguente codice _sotto_ la linea esistente **CXXFLAGS** per attivare icc con makepkg. Non sono necessarie altre opzioni particolari per attivare icc con makepkg.

```
_CC=icc
if [ $_CC = "icc" ]; then
  export CFLAGS="-fast -pipe -gcc"
  export CXXFLAGS="${CFLAGS}"
  export CC="icc"
  export CXX="icpc"
  export HOSTCC="icc"
fi
```

**Note:** per passare da icc ad gcc o viceversa si deve commentare o decomentare la linea dove si definisce la variabile **_CC**.

**Note:** In alcuni casi le direttive in `/etc/makepkg.conf` vengono ignorate e la compilazione avviene con _gcc_, quindi dopo aver costruito il pachetto ti devi assicurare che questo sia stato effettivamente compilato con _icc_

Per verificare che un pacchetto sia stato effettivamente compilato con icc:

*   Dare il comando **ldd [your_app] | grep intel** Se l'applicativo usa un libreria dinamica che si trova nella directory **/opt/intel/lib/** significa che è stato effettivamente compilato con icc

*   Un altro metodo è quello di osservare l'output durante la costruzione del pacchetto e vedere se usa _icc_ o _icpc_ come comando.

*   L'ultimo metodo è quello di vedere se i warning sono nello stile di _icc_.

## icc CFLAGS

Generalmente, icc supporta una buona parte dei CFLAGS di gcc ed è piuttosto tollerante coi flags di gcc che non implementa. In moltissimi casi si possono ignorare senza problemi i warning. Per una lista completa delle opzioni si consiglia di consultare la man page di icc , o dando il comando:

```
icc --help

```

### -xX

Da usare per generare un codice ottimizzato sulla propria CPU. Se non si è sicuri di quali **flags** usare si deve andare a vedere la sezione _flags_ nel file `/proc/cpuinfo`. Nell'esempio sotto, **SSE4.1** è la scelta coretta:

```
$ cat /proc/cpuinfo  | grep -m 1 flags
flags: fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush 
dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx lm constant_tsc arch_perfmon pebs 
bts rep_good nopl aperfmperf pni dtes64 monitor ds_cpl vmx smx est tm2 ssse3 cx16 xtpr
pdcm sse4_1 lahf_lm dts tpr_shadow vnmi flexpriority
```

*   -xHost
*   -xSSE2
*   -xSSE3
*   -xSSSE3
*   -xSSE4.1
*   -xSSE4.2
*   -xAVX
*   -xCORE-AVX-I
*   -xSSSE3_ATOM

**Tip:** Se si usa l'opzione **-xHost** icc decide automaticamente quale è la configurazione ottimale per la CPU.

### -Ox

Come con gcc. x è una delle seguenti opzioni:

*   0 - disabilita ogni ottimizzazione
*   1 - Ottimizza per avere una massimizzazione della velocità, ma disabilita alcune opzioni che accrescono la dimensione del eseguibile.
*   2 - Ottimizza per avere una massimizzazione della velocità (DEFAULT)
*   3 - Ottimizza per avere una massimizzazione della velocità e abilita una serie di ottimizzazioni molto aggressive (raccomandato per applicazioni numeriche intensive)

### -w

Come con gcc:

*   -w - disabilita tutti i warnings (raccomandato per la compilazione dei pacchetti)
*   -Wbrief - stampa un warning di una linea
*   -Wall - abilita tutti i warning
*   -Werror - i warning vengono interpretati come errori.

## Software compilato con Intel

Qui sotto riporto una lista di applicativi che si è tentato di compilare con Intel compiler, la compilazione in genere va fatta usando i PKGBUILD presenti in ABS.

| Applicativo | Compilazione | Note |
| **Gimp 2.8** | OK | Funziona col [Metodo 1](/index.php/Intel_C%2B%2B_(Italiano)#Metodo_1 "Intel C++ (Italiano)") |
| **MySql** | OK | Funziona col [Metodo 1](/index.php/Intel_C%2B%2B_(Italiano)#Metodo_1 "Intel C++ (Italiano)") |
| **SqlLite** | OK | Funziona col [Metodo 1](/index.php/Intel_C%2B%2B_(Italiano)#Metodo_1 "Intel C++ (Italiano)") |
| **xaos** | OK | Funziona col [Metodo 1](/index.php/Intel_C%2B%2B_(Italiano)#Metodo_1 "Intel C++ (Italiano)") |
| **mplayer** | Fallita | Tipo di compilatore non riconosciuto |
| **VLC** | Non riuscita | Ci sono problemi con le opzioni di compilazione |
| **python-numpy** | OK | si deve modificare il PKGBUILD. [python-numpy-mkl](https://aur.archlinux.org/packages/python-numpy-mkl/) |
| **python-scipy** | OK | si deve modificare il PKGBUILD. [python-scipy-mkl](https://aur.archlinux.org/packages/python-scipy-mkl/) |

**Leggenda:**

| OK | La compilazione con ICC funziona senza intoppi |
| OK | La compilazione funziona ma sono necessari degli interventi sul PKGBUILD |
| Non riuscita | La compilazione potrebbe funzionare, ma si sono verificati degli errori durante la compilazione. |
| Non consigliata | La compilazione funziona, ma non è consigliabile usare ICC |
| Fallita | Non si riesce a compilare. |