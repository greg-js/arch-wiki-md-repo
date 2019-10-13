## DISTCC

Installa distcc ( pacman -S distcc ). Edita /etc/conf.d/distccd in questo modo:

```
lord=`nslookup gally.dyndns.org | tail -n2 | grep Address | cut -d ' ' -f2`
dani=`nslookup danimoth.homelinux.net | tail -n2 | grep Address | cut -d ' ' -f2`
zmax=`nslookup zmax.homelinux.org | tail -n2 | grep Address | cut -d ' ' -f2`
lele85=`nslookup lele85.dyndns.biz | tail -n2 | grep Address | cut -d ' ' -f2`
ech0s7=`nslookup ech0s7.serveftp.org | tail -n2 | grep Address | cut -d ' ' -f2`
cagnulein=`nslookup cagnulein.no-ip.info | tail -n2 | grep Address | cut -d ' ' -f2`
DISTCC_ARGS="--user nobody --allow ${lord} --allow ${dani} --allow ${zmax} --allow ${lele85} --allow ${ech0s7} --allow ${cagnulein} -N 19"

```

-N 19 dice semplicemente che il processo di compilazione verra' eseguito con un nice 19, in modo da limitare l'impatto sull'uso del PC.

Se vuoi aggiungerti, prima di DISTCC_ARGS metti una riga del tipo

```
vostro_nome=`nslookup vostro_dns_dinamico | tail -n2 | grep Address | cut -d ' ' -f2`

```

e in DISTCC_ARGS aggiungi ${vostro_nome}. Ricordate poi di aggiornare questa pagina!

Ricorda! Il proprio host non va messo. Qundi Danimoth, ad esempio, avra':

```
DISTCC_ARGS="--user nobody --allow ${lord} --allow ${zmax} --allow ${lele85} --allow ${ech0s7} --allow ${cagnulein} --allow 127.0.0.1"

```

## makepkg

apri /etc/makepkg.conf

edita

```
MAKEFLAGS="-j14"
BUILDENV=(fakeroot distcc color !ccache !xdelta)

```

e aggiungi, prima di DISTCCHOST:

```
lord=`nslookup gally.dyndns.org | tail -n2 | grep Address | cut -d ' ' -f2`
dani=`nslookup danimoth.homelinux.net | tail -n2 | grep Address | cut -d ' ' -f2`
zmax=`nslookup zmax.homelinux.org | tail -n2 | grep Address | cut -d ' ' -f2`
lele85=`nslookup lele85.dyndns.biz | tail -n2 | grep Address | cut -d ' ' -f2`
ech0s7=`nslookup ech0s7.serveftp.org | tail -n2 | grep Address | cut -d ' ' -f2`
cagnulein=`nslookup cagnulein.no-ip.info | tail -n2 | grep Address | cut -d ' ' -f2`
DISTCC_HOSTS="localhost/1 ${lord}:6112/2,lzo ${dani}:6610/1,lzo ${zmax}:3632/1,lzo ${lele85}:3632/2,lzo ${ech0s7}:3632/1,lzo ${cagnulein}:3632/2,lzo"

```

Ricorda! il proprio host non va messo. Ad esempio, danimoth avra':

```
DISTCC_HOSTS="localhost/1 ${lord}:6112/2,lzo ${zmax}:3632/1,lzo ${lele85}:3632/2,lzo ${ech0s7}:3632/1,lzo ${cagnulein}:3632/2,lzo"

```

Per aggiungerti, fai come prima, metti il tuo nome sia come variabile sia nell'array. E riportalo qui, mi raccomando!

Spiegazione veloce dei termini: ${nome} e' l'host, /NUMERO sta per il limite di job da spedire contemporanemente, e ,lzo serve per attivare la compressione dei dati, che a noi e' obbligatoria altrimenti andremmo ad aspettare di piu' tra trasmissione e ricezione che non compilandocelo da solo. Alcuni benchmark fatti dall'impareggiabile danimoth dimostrano che la cosa migliore e' assegnare 2 a chi ha un dual core e 1 per chi ha il processore singolo, come limite massimo. Cosi' si raggiunge un discreto rapporto qualita/prestazioni che rendono (spero) conveniente usare distcc.