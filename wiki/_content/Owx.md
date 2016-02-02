# Owx

[owx](http://owx.chmurka.net) (open wouxun) is a CLI utility used to program KG669V radios by means of a CSV spreadsheet.

## Installation

[Install](/index.php/Install "Install") the [owx](https://aur.archlinux.org/packages/owx/) package.

## Tips and Tricks

Frequency lists; replace `CH` with the desired channel number.

U.S. [NOAA Weather Radio](http://en.wikipedia.org/wiki/NOAA_Weather_Radio):

```
"CH","NWR1","162.40000","162.40000","","","narrow","high","no","no"
"CH","NWR2","162.42500","162.42500","","","narrow","high","no","no"
"CH","NWR3","162.45000","162.45000","","","narrow","high","no","no"
"CH","NWR4","162.47500","162.47500","","","narrow","high","no","no"
"CH","NWR5","162.50000","162.50000","","","narrow","high","no","no"
"CH","NWR6","162.52500","162.52500","","","narrow","high","no","no"
"CH","NWR7","162.55000","162.55000","","","narrow","high","no","no"
```

U.S. [Family Radio Service (FRS)](http://en.wikipedia.org/wiki/Family_Radio_Service):

```
"CH","FRS1","462.56250","462.56250","","","narrow","high","yes","no"
"CH","FRS2","462.58750","462.58750","","","narrow","high","yes","no"
"CH","FRS3","462.61250","462.61250","","","narrow","high","yes","no"
"CH","FRS4","462.63750","462.63750","","","narrow","high","yes","no"
"CH","FRS5","462.66250","462.66250","","","narrow","high","yes","no"
"CH","FRS6","462.68750","462.68750","","","narrow","high","yes","no"
"CH","FRS7","462.71250","462.71250","","","narrow","high","yes","no"
"CH","FRS8","467.56250","467.56250","","","narrow","high","yes","no"
"CH","FRS9","467.58750","467.58750","","","narrow","high","yes","no"
"CH","FRS10","467.61250","467.61250","","","narrow","high","yes","no"
"CH","FRS11","467.63750","467.63750","","","narrow","high","yes","no"
"CH","FRS12","467.66250","467.66250","","","narrow","high","yes","no"
"CH","FRS13","467.68750","467.68750","","","narrow","high","yes","no"
"CH","FRS14","467.71250","467.71250","","","narrow","high","yes","no"
```

U.S. [General Mobile Radio Service (GMRS)](http://en.wikipedia.org/wiki/GMRS), exclusive of interstitial frequencies shared by FRS, and using simplex operation:

```
"CH","GMRS1","462.55000","462.55000","","","narrow","high","yes","no"
"CH","GMRS2","462.57500","462.57500","","","narrow","high","yes","no"
"CH","GMRS3","462.60000","462.60000","","","narrow","high","yes","no"
"CH","GMRS4","462.62500","462.62500","","","narrow","high","yes","no"
"CH","GMRS5","462.65000","462.65000","","","narrow","high","yes","no"
"CH","GMRS6","462.67500","462.67500","","","narrow","high","yes","no"
"CH","GMRS7","462.70000","462.70000","","","narrow","high","yes","no"
"CH","GMRS8","462.72500","462.72500","","","narrow","high","yes","no"
```

U.S. [Multi-Use Radio Service (MURS)](http://en.wikipedia.org/wiki/Multi-Use_Radio_Service):

```
"CH","MURS1","151.82000","151.82000","","","narrow","high","yes","no"
"CH","MURS2","151.88000","151.88000","","","narrow","high","yes","no"
"CH","MURS3","151.94000","151.94000","","","narrow","high","yes","no"
"CH","MURS4","154.57000","154.57000","","","narrow","high","yes","no"
"CH","MURS5","154.60000","154.60000","","","narrow","high","yes","no"
```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Owx&oldid=389415](https://wiki.archlinux.org/index.php?title=Owx&oldid=389415)"