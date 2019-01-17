**Estado de la traducción**
Este artículo es una traducción de [Omnikey Cardman 5321](/index.php/Omnikey_Cardman_5321 "Omnikey Cardman 5321"), revisada por última vez el **2019-01-16**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Omnikey_Cardman_5321&diff=0&oldid=563467) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Este artículo explica cómo hacer funcionar el lector de tarjetas *Omnikey Cardman 5321 SmartCard Reader* en Archlinux. Esta guía también podría funcionar para otros modelos, pero aún no se ha probado.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") los paquetes [pcsclite](https://www.archlinux.org/packages/?name=pcsclite), [pcsc-tools](https://www.archlinux.org/packages/?name=pcsc-tools) y [omnikey_cardman_5x2x](https://aur.archlinux.org/packages/omnikey_cardman_5x2x/).

[Inicie](/index.php/Systemd_(Espa%C3%B1ol)#Utilizar_las_unidades "Systemd (Español)") pcscd con `pcscd.service`.

## Prueba con pcsc_scan

Puede probar la instalación ejecutando `pcsc_scan`. Si todo funciona correctamente, debería obtener algo así:

```
PC/SC device scanner
V 1.4.16 (c) 2001-2009, Ludovic Rousseau <ludovic.rousseau@free.fr>
Compiled with PC/SC lite version: 1.5.5
Scanning present readers...
0: OMNIKEY CardMan 5x21 00 00
1: OMNIKEY CardMan 5x21 00 01

Sun Feb 21 18:21:05 2010
 Reader 0: OMNIKEY CardMan 5x21 00 00
  Card state: Card removed, 

Sun Feb 21 18:21:05 2010
 Reader 1: OMNIKEY CardMan 5x21 00 01
  Card state: Card removed, 

Sun Feb 21 18:21:11 2010
 Reader 1: OMNIKEY CardMan 5x21 00 01
  Card state: Card inserted, 
  ATR: 3B 89 80 01 4A 43 4F 50 34 31 56 32 32 4D

ATR: 3B 89 80 01 4A 43 4F 50 34 31 56 32 32 4D
+ TS = 3B --> Direct Convention
+ T0 = 89, Y(1): 1000, K: 9 (historical bytes)
  TD(1) = 80 --> Y(i+1) = 1000, Protocol T = 0 
-----
  TD(2) = 01 --> Y(i+1) = 0000, Protocol T = 1 
-----
+ Historical bytes: 4A 43 4F 50 34 31 56 32 32
  Category indicator byte: 4A (proprietary format)
+ TCK = 4D (correct checksum)

Possibly identified card (using /usr/share/pcsc/smartcard_list.txt):
3B 89 80 01 4A 43 4F 50 34 31 56 32 32 4D
	New Zealand e-Passport

```