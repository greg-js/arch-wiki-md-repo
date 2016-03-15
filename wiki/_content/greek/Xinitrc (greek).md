## Περίληψη

Πως να χρησιμοποιήσετε την εντολή **startx**,για να εκκινήσετε το αγαπημένο σας γραφικό περιβάλλον καθώς και τον x-server.

## Εκκινήστε το αρχείο, **~/.xinitrc**

Ξεκινάμε το γραφικό περιβάλλον από το αρχείο **/home/yourname/.xinitrc** Βγάλτε το σύμβολο (#) και επιλέξετε το αγαπημένο σας, π.χ Gnome

```
#!/bin/sh
#
# ~~/.xinitrc
#
# Executed by startx (run your window manager from here)
#
# exec ion
# exec wmaker
# exec startkde
# exec icewm
# exec blackbox
exec gnome-session
# exec startfluxbox
# exec startxfce4
# exec openbox
# exec startlxde

```

Μικρή παρατήρηση: αν το .xinitrc λειτουργεί, αλλά θέλετε να δοκιμάσετε και άλλα περιβάλλοντα εργασίας ή windows managers τρέξτε το xinit από ένα τερματικό όπως παρακάτω

 `xinit /full/path/to/window-manager` 

Ολόκληρο το path (τοποθεσία) **χρειάζεται**. Προαιρετικά μπορείτε να προσθέσετε επιλογές στον X server μετά τα -- Παράδειγμα:

 `xinit /usr/bin/enlightenment -- -br +bs -dpi 96`