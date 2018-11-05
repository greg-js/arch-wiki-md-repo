**Estado de la traducción**
Este artículo es una traducción de [Ethereum](/index.php/Ethereum "Ethereum"), revisada por última vez el **2018-10-31**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Ethereum&diff=0&oldid=552192) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

El [Proyecto Ethereum](https://ethereum.org/) proporciona una plataforma de código abierto, distribuida y basada en blockchain para los llamados [contratos inteligentes](https://en.wikipedia.org/wiki/es:Contrato_inteligente "wikipedia:es:Contrato inteligente").

## Contents

*   [1 Clientes](#Clientes)
    *   [1.1 Go Ethereum](#Go_Ethereum)
        *   [1.1.1 Minería GPU con geth](#Miner.C3.ADa_GPU_con_geth)
    *   [1.2 Ethereum Wallet](#Ethereum_Wallet)

## Clientes

### Go Ethereum

[Go Ethereum](https://geth.ethereum.org/), la implementación oficial de Go del protocolo Ethereum, está disponible como el paquete [go-ethereum](https://www.archlinux.org/packages/?name=go-ethereum).

Cree una cuenta con `geth account new`.

El cliente puede iniciarse con `geth`, y procederá a descargar varios gigabytes de datos blockchain. Esto llevará mucho tiempo. Este tiempo se puede acortar con

```
$ geth --fast --cache=1024

```

Aparentemente, tener un valor de caché más alto parece acelerar el proceso[[1]](https://ethereum.stackexchange.com/questions/603/help-with-very-slow-mist-sync#3805).

Opcionalmente, inicie el cliente con `geth console` para obtener una consola de JavaScript para una interacción más significativa. Esta consola se puede adjuntar desde otro terminal o de forma remota con `geth attach [hostname:port defaults to localhost]`.

Para verificar los saldos en la consola o en los modos adjuntos, use `web3.fromWei(eth.getBalance(eth.coinbase), "ether")`.

Para iniciar la minería de CPU, use `geth --mine`. Esto es mucho menos eficiente que la minería de GPU, y ethereum.org no lo recomienda.

#### Minería GPU con geth

La minería de GPU con geth ha sido descontinuada.

### Ethereum Wallet

Puede instalar Ethereum Wallet a través del paquete [mist](https://aur.archlinux.org/packages/mist/) o de [los lanzamientos](https://github.com/ethereum/mist/releases) de GitHub. Mist se conectará a una instancia geth en ejecución o iniciará la suya propia si no enuentra ninguna.

Si usa la versión de GitHub, descargue la más reciente para Linux con extensión zip: `Ethereum-Wallet-linux64-*version*.zip`; descomprima el archivo y ejecute `./ethereumwallet`.

Si la aplicación no se inicia con `error while loading shared libraries: libgtk-x11-2.0.so: cannot open shared object file: No such file or directory`, instale la librería [GTK+ 2](/index.php/GTK%2B_(Espa%C3%B1ol) "GTK+ (Español)") .

Wallet también implementa un nodo Ethereum.