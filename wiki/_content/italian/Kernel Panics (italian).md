In questa pagina si descrive come ritornare ad una versione precedente del kernel, nel caso in cui quella corrente abbia avuto qualche problema.

## Contents

*   [1 Avvio dal CD di installazione](#Avvio_dal_CD_di_installazione)
*   [2 Chroot nel proprio disco di root](#Chroot_nel_proprio_disco_di_root)
*   [3 Ritornare ad una versione precedente del kernel (rollback)](#Ritornare_ad_una_versione_precedente_del_kernel_(rollback))
*   [4 Reboot](#Reboot)

## Avvio dal CD di installazione

Il primo passo è l'avvio del CD di installazione. Una volta lanciato, digitare "arch", come se si volesse installare Arch Linux per la prima volta.

```
# arch

```

## Chroot nel proprio disco di root

Una volta avviato, avrete un ambiente Linux ridotto, ma perfettamente funzionale, completo di alcuni strumenti di base. Ora, bisogna montare il disco di root in /mnt.

```
# mount /dev/hdXY /mnt

```

Se si utilizza una partizione di boot, non dimenticare di montarla

```
# mount /dev/hdaXY /mnt/boot

```

I kernel più nuovi utilizzano una ramdisk iniziale per impostare l'ambiente del kernel. Quando si reinstalla un kernel, quella ramdisk iniziale va rigenerata con mkinitcpio. Una delle caratteristiche di mkinitcpio è l'autorilevamento dei moduli del kernel che sono necessari per avviare il proprio computer. Per far funzionare questo autorilevamento, è necessario che `/dev`, `/sys` e `/proc` siano montati nel proprio ambiente chroot:

```
# mount -t proc none /mnt/proc
# mount -t sysfs none /mnt/sys
# mount --bind /dev /mnt/dev

```

Ora, si dovrà eseguire un chroot in questo disco, in modo da poterlo utilizzare come si avviasse il proprio computer "normalmente". Molte funzionalità non saranno comunque disponibili.

```
# chroot /mnt

```

## Ritornare ad una versione precedente del kernel (rollback)

Se si mantengono i pacchetti scaricati con pacman nella sua cache, allora si può facilmente eseguire il rollback. Se invece non si è scelto di mantenerli, bisogna trovare un modo per ottenere una versione precedente del kernel nel proprio sistema.

Supponiamo che si è scelto di mantenere le precedenti versioni dei pacchetti. Si dovrà quindi installare l'ultima versione funzionante, per esempio con il seguente comando:

```
# pacman -U /var/cache/pacman/pkg/kernel26-2.6.16.13-1.pkg.tar.gz

```

Probabilmente si dovrà cambiare il numero di versione riportato appena sopra con quello dell'ultima versione funzionante.

## Reboot

A questo punto, se si è reinstallato il kernel funzionante, si può riavviare il proprio computer ed eseguire il boot come si fa usualmente. Non dimenticare di controllare la pagina delle news di Arch Linux, per capire che cosa è andato storto con l'ultima versione del kernel.