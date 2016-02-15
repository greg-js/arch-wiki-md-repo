| **Summary**  |
| Installatie en configuratie van TGT als iSCSI target |
| **Related** |
| [ISCSI_Target](/index.php/ISCSI_Target "ISCSI Target") |
| [iSCSI Boot](/index.php/ISCSI_Boot "ISCSI Boot") |

Het [TGT SCSI framework](http://stgt.sourceforge.net) kan gebruikt worden voor meerdere storage protocollen. Dit document beschrijft het gebruik van TGT als iSCSI target.

## Contents

*   [1 Waarom TGT](#Waarom_TGT)
*   [2 Installatie](#Installatie)
*   [3 Configuratie](#Configuratie)
*   [4 Voorbeeld configuratie](#Voorbeeld_configuratie)
*   [5 Van start](#Van_start)

## Waarom TGT

Er zijn verschillende iSCSI targets voor Linux beschikbaar, die qua performance elkaar niet heel veel ontlopen. TGT biedt de volgende voordelen:

*   wordt actief door-ontwikkeld
*   enige iSCSI target die op dit moment geschikt is voor vSphere omgevingen

## Installatie

De [tgt](https://aur.archlinux.org/packages/tgt/) software moet vanaf [AUR](/index.php/AUR "AUR") geinstalleerd worden. Wanneer je gebruik wilt maken van direct-store moet ook sg3_utils uit de [extra] repository geinstalleerd worden. Bij een direct-store worden eigenschappen van het fysieke device benaderbaar voor initiator en target.

Ander aandachtspunt: wanneer je gebruik maakt van een [Firewall](/index.php/Firewall "Firewall") dan moet tcp port 3260 geopend worden.

## Configuratie

Configuratie kan op twee manieren:

*   Met behulp van de `tgtadm` utility, waarna met `tgt-admin --dump` de configuratie bewaard kan worden.
    Deze methode wordt beschreven in de [Scsi-target-utils Quickstart Guide](http://fedoraproject.org/wiki/Scsi-target-utils_Quickstart_Guide) die ook gelinkt wordt vanaf de [TGT website](http://stgt.sourceforge.net). Het nadeel van deze methode is dat sommige parameters niet bewaard worden.
*   Het bewerken van /etc/tgt/targets.conf

## Voorbeeld configuratie

```
<target iqn.2004-01.nl.xtg:iscsi-server1>
 direct-store /dev/sdb
 write-cache on
 initiator-address ALL
 incominguser gebruiker wachtwoord
 scsi_id 00010001
 vendor_id XTG
 lun 12
</target>

```

```
MaxRecvDataSegmentLength 131072
MaxXmitDataSegmentLength 131072
MaxBurstLength 262144
FirstBurstLength 262144
TargetRecvDataSegmentLength=262144
InitiatorRecvDataSegmentLength=262144
MaxOutstandingUnexpectedPDUs=0
MaxOutstandingR2T=1
MaxCommands=128

```

Het eerste gedeelte van de voorbeeld configuratie biedt /dev/sdb als lun 12 aan en wordt er gebruik gemaakt van chap authenticatie. In het tweede gedeelte staan er een aantal [iSCSI advanced parameters](http://www.ietf.org/rfc/rfc3720.txt)

## Van start

Als de configuratie correct is, kan TGT gestart worden:

```
sudo rc.d start tgt

```

Om TGT te starten tijdens het boot proces van Arch Linux, voeg deze dan toe aan de [DAEMONS](/index.php/DAEMONS "DAEMONS") area in het [rc.conf](/index.php/Rc.conf "Rc.conf") bestand.

```
DAEMONS = ( ... network tgt ... )

```

Controleren of dit ook daadwerkelijk gelukt is kan met:

```
tgt-admin -s

```