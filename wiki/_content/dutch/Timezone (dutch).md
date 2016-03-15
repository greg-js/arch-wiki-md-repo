**Tijdzones** zijn verschillende gebieden op aarde met elk een verschillende standaardtijd. U kunt uw computer zo instellen dat deze een bepaalde tijdzone gebruikt. Dit doet u door de variable `TIMEZONE` in `/etc/rc.conf` aan te passen. U kunt alle mogelijke waardes vinden in `/usr/share/zoneinfo`. Bijvoorbeeld:

```
TIMEZONE="Europe/Amsterdam"

```

of

```
TIMEZONE="Europe/Brussels"

```

of

```
TIMZONE="America/Paramaribo"

```

## UTC of localtime?

In `/etc/rc.conf` kunt u aangeven of u UTC of localtime wilt gebruiken. Als u alleen Linux draait, is het aan te raden om UTC te gebruiken. Draait u echter ook Windows op dezelfde PC, dan kunt u beter localtime gebruiken. Als u UTC gebruikt, verzet de computer automatisch de tijd een uur als de zomer- of wintertijd ingaat. U kunt dit instellen door middel van de variable `HARDWARECLOCK`:

```
HARDWARECLOCK="UTC"

```

of

```
HARDWARECLOCK="localtime"

```