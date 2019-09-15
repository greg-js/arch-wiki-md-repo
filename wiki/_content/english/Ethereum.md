The [Ethereum Project](https://ethereum.org/) provides an open-source, distributed, blockchain-based platform for so-called [wikipedia:Smart contracts](https://en.wikipedia.org/wiki/Smart_contracts "wikipedia:Smart contracts").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Clients](#Clients)
    *   [1.1 Go Ethereum](#Go_Ethereum)
        *   [1.1.1 GPU Mining with geth](#GPU_Mining_with_geth)
    *   [1.2 Ethereum Wallet](#Ethereum_Wallet)

## Clients

### Go Ethereum

[Go Ethereum](https://geth.ethereum.org/), the official Go implementation of the Ethereum protocol, is available as the [go-ethereum](https://www.archlinux.org/packages/?name=go-ethereum) package.

Create an account with `geth account new`.

The client can be started with `geth`, and it will proceed to download several gigabytes of blockchain data. This will take a very long time. This time can be shortened with

```
$ geth --fast --cache=1024

```

Higher cache values appear to speed up the process more[[1]](https://ethereum.stackexchange.com/questions/603/help-with-very-slow-mist-sync#3805).

Optionally, start the client with `geth console` to get a JavaScript console for more meaningful interaction. This console can then be attached-to from another terminal or remotely with `geth attach [hostname:port defaults to localhost]`.

To check balances in the console or attach modes, use `web3.fromWei(eth.getBalance(eth.coinbase), "ether")`.

To start CPU mining, use `geth --mine`. This is far less efficient than GPU mining, and ethereum.org does not recommend it.

#### GPU Mining with geth

GPU mining with geth has been discontinued.

### Ethereum Wallet

You can install the Ethereum Wallet via the [mycrypto-bin](https://aur.archlinux.org/packages/mycrypto-bin/) package. The old [mist](https://aur.archlinux.org/packages/mist/) wallet is deprecated. See the [announcement](https://medium.com/@avsa/sunsetting-mist-da21c8e943d2) and view the [migration guide](https://medium.com/@omgwtfmarc/mist-migration-patterns-6bcf066ac383).