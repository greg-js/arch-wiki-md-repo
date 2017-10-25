The [Ethereum Project](https://ethereum.org/) provides an open-source, distributed, blockchain-based platform for so-called [wikipedia:Smart contracts](https://en.wikipedia.org/wiki/Smart_contracts "wikipedia:Smart contracts").

## Contents

*   [1 Clients](#Clients)
    *   [1.1 Ethereum-Go](#Ethereum-Go)
        *   [1.1.1 GPU Mining with geth](#GPU_Mining_with_geth)
    *   [1.2 Ethereum Wallet](#Ethereum_Wallet)

## Clients

### Ethereum-Go

The Ethereum [geth](https://www.archlinux.org/packages/?name=geth) package is Ethereum.org's Golang implementation of their node, client, and optionally CPU Miner.

Create an account with `geth account new`.

The client can be started with `geth`, and it will proceed to download several gigabytes of blockchain data.

Optionally, start the client with `geth console` to get a JavaScript console for more meaningful interaction. This console can then be attached-to from another terminal or remotely with `geth attach [hostname:port` .

To check balances in the console or attach modes, use `web3.fromWei(eth.getBalance(eth.coinbase), "ether")`.

To start CPU mining, use `geth --mine`. This is far less efficient than GPU mining, and ethereum.org does not recommend it.

#### GPU Mining with geth

### Ethereum Wallet

You can install the Ethereum Wallet via the [mist](https://aur.archlinux.org/packages/mist/) package or the GitHub [releases](https://github.com/ethereum/mist/releases).

If you use a GitHub release, download the most recent Linux one with the zip extension: `Ethereum-Wallet-linux64-*version*.zip`; unzip the file and run `./ethereumwallet`.

If the application fails to start with `error while loading shared libraries: libgtk-x11-2.0.so: cannot open shared object file: No such file or directory`, install the [GTK+ 2](/index.php/GTK%2B "GTK+") library.

The wallet also implements an Ethereum node.