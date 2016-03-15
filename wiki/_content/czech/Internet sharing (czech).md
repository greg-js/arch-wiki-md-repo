## Předmluva

Předpokládejme, že máte připojení k internetu a chcete sdílet. Existují dva hlavní způsoby, jak to udělat.

```
   internet                           pc1
1\. ----> |router| ---> |switch| --->-<
                                      pc2 ..atd

   internet
2\. ------> |pc1 (router)| --> pc2..atd

```

## Návod

Vysvětlím vám druhý způsob.

1.  Nainstalujte druhou síťovou kartu do PC1.
2.  Propojte PC pomocí kříženého kabelu.
3.  Předpokládejme že první karta (s internetem) je ***eth0*** a druhá je ***eth1***. (If those two keep switching at every boot read [this](/index.php/Udev#Mixed_Up_Devices.2C_Sound.2FNetwork_Cards_Changing_Order_Each_Boot "Udev") ).
4.  Konfigurace druhé síťové karty s:

    	**IP:** 192.168.0.1

    	**Netmask:** 255.255.255.0

    nebo zadejte v konzoli (jako root)
    ```
    ifconfig eth1 192.168.0.1 netmask 255.255.255.0
    ifconfig eth1 up
    ```

5.  Zadejte stejné informace v souboru **/etc/rc.conf** so that this card is set up correctly earch time your computer starts. **Poznámka**: pokuď používáte **Wicd**, nemusíte to udělat.
    ```
    eth1="eth1 192.168.0.1 netmask 255.255.255.0"
    INTERFACES=(lo eth0 eth1)
    ```

6.  Povolení předávání paketů. `echo 1 > /proc/sys/net/ipv4/ip_forward` 
7.  Editujte `/etc/sysctl.d/30-ipforward.conf` nastavte 1 u net.ipv4.ip_forward (**net.ipv4.ip_forward=1**). To umožní uchování změny po restartu.
8.  Nainstalujte iptables(Pokuď ještě nemáte) a nastavte pravidlo pro přesměrování internetu do PC2 a uložte. iptables.
    ```
    pacman -S iptables
    iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
    /etc/rc.d/iptables save
    ```

9.  Editujte **/etc/conf.d/iptables** a zapněte forwarding (IPTABLES_FORWARD=1).
10.  Start démona iptables: `/etc/rc.d/iptables start` 
11.  Přidejte iptables do pole DAEMONS v souboru /etc/rc.conf, aby byl spuštěn po zapnutí pc.
12.  V PC2 nastavte:

    	**IP:** 192.168.0.2

    	**Netmask:** 255.255.255.0

    	**Gateway:** 192.168.0.1

    	**DNS:** stejný jako v PC1

```
ifconfig eth0 192.168.0.2 netmask 255.255.255.0
ifconfig eth0 up
route add default gw 192.168.0.1 eth0
echo "nameserver <adresa nameserveru>" >> /etc/resolv.conf

```

Adresu nameserveru můžete zjistit v /etc/resolv.conf na PC1.

Hotovo

**Note:** Of course, this also works with a mobile broadband connection (usually called ppp0 on PC1)

## Viz také

*   [Sharing ppp connection with wlan interface](/index.php/Sharing_ppp_connection_with_wlan_interface "Sharing ppp connection with wlan interface")
*   [Simple stateful firewall](/index.php/Simple_stateful_firewall "Simple stateful firewall")
*   [Router](/index.php/Router "Router")
*   [USB 3G Modem](/index.php/USB_3G_Modem "USB 3G Modem")

* * *

pozn.překladatele: Omlouvám se za kvalitu. Překládal jsem pomocí překladače a hned to i nastavoval, takže můžu potvrdit funkčnost. Jestli to umíte přeložit lépe, jako že vás bude jistě spousta, s chutí do toho.