Poclbm (Python OpenCL Bitcoin miner) is a python program/script made by m0mchil on Github ([https://github.com/m0mchil/poclbm](https://github.com/m0mchil/poclbm)), it mines Bitcoins using an OpenCL capable device. Here's how to install and use it as a systemd service.

## Contents

*   [1 Introduction](#Introduction)
*   [2 Installation](#Installation)
*   [3 Execute the miner](#Execute_the_miner)
*   [4 Running as systemd service](#Running_as_systemd_service)

## Introduction

Mining Bitcoins is a process that uses your computer hardware i.e. GPU/CPU to generate "blocks" which are used to verify transactions in the Bitcoin network. Currently a generated block will give you 50 BTC. However it will drop to 25 BTC by the end of November 2012.

As more blocks get generated difficulty increases, and today (as of November 2012) the estimated time to generate a block on an average gaming computer is over 2 years. Therefore it's not really worth the electricity trying to generate a block. Also note that it's random and sometimes you may get lucky and still (despite the difficulty and stuff) generate a block using your standard gaming computer. However it is very unlikely and not worth the risk of waiting months. you'll probably end up stopping it and paying your enormous electricity bill without having generated anything. But there is a solution to that which is called **Pool Mining**.

A pool is a network of computers mining together to generate a block, and the total reward is shared between all the people that contributed to generate the block, so when using a pool you'll get smaller but regular incomes and using the appropriate hardware (see below) it may be actually a profitable business.

When mining, the CPU isn't ideal and even a low-end graphics card will beat your high-end CPU so we're only using the GPU for mining, so with a correct configuration the machine used for mining can be used for something else, for example a web server, and if you're only mining then you may want to use a low-end single-core CPU and a low-end motherboard, and RAM isn't used either so 2GB of RAM is more than enough.

**Note:** NVIDIA cards aren't ideal for mining and you'll waste more money (on electricity) than you'll generate, even when using a pool, so unless you do it for experimentation/fun, or if you use your computer as a heat source (i use mine in my bedroom and it's producing more heat than my usual electric heater) it's not worth it.

**Note:** ATI/AMD cards are the best choice for this, they have a lower price and use less electricity while having extreme performance (for mining) compared to NVIDIA cards (a single ATI card is more powerful than my 3x NVIDIA GTX580), so if you're doing this for profit you need ATI cards.

Also, there is a bug on some drivers (both ATI and NVIDIA) that makes the miner use 100% CPU on 2 cores (even if mining on the GPU), i'm not sure what causes that but it seems to also affect Windows systems so you'll have to try it yourself.

## Installation

Install [poclbm-git](https://aur.archlinux.org/packages/poclbm-git/) from the [AUR](/index.php/AUR "AUR").

## Execute the miner

Use the command below to start the miner on all OpenCL devices. If you receive the following error then check you configuration and ensure that all required packages and drivers are present:

**Tip:** Be sure to have your pool login and password available. You can obtain this if you register with [https://mining.bitcoin.cz](https://mining.bitcoin.cz)

```
$ poclbm _username:password@server:port_

```

The miner has started and will display a hash rate (x MH/s). To exit use the `Ctrl+C` to exit. If you just want to run the miner manually then that's all you need to do.

## Running as systemd service

Create the service file:

 `/etc/systemd/system/poclbm.service` 

```
[Unit]
Description=Python OpenCL Bitcoin miner
After=network.target

[Service]
ExecStart=/usr/bin/poclbm --verbose _<user-specific arguments>_

[Install]
WantedBy=multi-user.target
```

The user-specific arguments need to be adapted as described in [#Execute the miner](#Execute_the_miner). Then [start](/index.php/Start "Start") the service using _systemctl_.