Estas son las instrucciones para instalar el controlador de la impresora Epson TX125.

Primero, instale [cups](https://www.archlinux.org/packages/?name=cups) de los repositorios oficiales y [epson-inkjet-printer-n10-nx127](https://aur.archlinux.org/packages/epson-inkjet-printer-n10-nx127/) del AUR.

Cree una nueva regla de udev, `/etc/udev/rules.d/10-usbprinter.rules`, con el contiendo siguiente.

```
ATTR{idVendor}=="04b8", ATTR{idProduct}=="085c", MODE:="0666", GROUP:={"lp"}, E$

```

`idVendor` e `idProduct` lo obtengo con `# lsusb -v`.