Pokud chcete změnit Vaší MAC adresu síťové karty (a to už z různých důvodů) je zde návod. Dejme tomu, že Vaše síťová karta je `ethX`. Pro zjištění MAC adresy zadáme příkaz:

```
# ip link show eth0

```

Číslo, které hledáme je 6 bytové v hexadecimální formě. Je to něco podobného tomuto:

```
link/ether 00:1d:98:5a:d1:3a

```

Změna MAC adresy je velmi jednoduchá. Napřed vypneme síťové rozhraní u kterého chceme změnit MAC adresu. Potom zadáme příkaz pro změnu MAC adresy a znovu nastartujeme síťové rozhraní. Vše musíme dělat standardně pod superuživatelem root:

```
# ip link set dev eth0 down
# ip link set dev eth0 address XX:XX:XX:XX:XX:XX
# ip link set dev eth0 up

```

kde `FF:FF:FF:FF:FF:FF` je Vaše nová MAC adresa.