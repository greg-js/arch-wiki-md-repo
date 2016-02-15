## Contents

*   [1 Condivisione connessione internet](#Condivisione_connessione_internet)
    *   [1.1 Schema connessioni](#Schema_connessioni)
    *   [1.2 Impostazioni generali](#Impostazioni_generali)
    *   [1.3 Impostazioni PC1](#Impostazioni_PC1)

# Condivisione connessione internet

## Schema connessioni

Assumiamo che la rete sia cosi' connessa:

```
--> internet <--> pc 1  <--> pc 2

```

i computer dovranno essere connessi tra loro tramite un cavo [crossover](http://it.wikipedia.org/wiki/Cavo_ethernet_incrociato) o uno switch

il _pc1_ dovra' possedere due schede di rete: una connessa ad internet (in questo esempio **eth0**) e una connessa al _pc2_ (in questo esempio **eth1**)

## Impostazioni generali

*   impostiamo gli indirizzi ip della rete interna in questo modo:

*   pc1:

	_IP_: 192.168.0.1

*   pc2:

	_IP_: 192.168.0.2

	_Gateway_: 192.168.0.1

	_DNS_: lo stesso del _pc1_

	si puo' utilizzare il semplice comando:

	 ` ifconfig eth1 192.168.0.2 up ` 

	e modificare il file **rc.conf** per impostare il gateway corretto

## Impostazioni PC1

1.  abilitiamo il _forwarding_ dei pacchetti: `echo 1 > /proc/sys/net/ipv4/ip_forward ` 
2.  installiamo _iptables_ e configuriamolo in questo modo nel _pc1_:

    ```
    iptables -A FORWARD -i eth0 -o eth1 -j ACCEPT
    iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
    iptables -t nat -A POSTROUTING -o eth1 -j MASQUERADE
    ```

ora il _pc2_ potra' accedere ad internet esattamente nello stesso modo in cui lo fa il _pc1_