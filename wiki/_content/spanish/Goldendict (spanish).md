**Estado de la traducción**
Este artículo es una traducción de [Goldendict](/index.php/Goldendict "Goldendict"), revisada por última vez el **2018-10-29**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Goldendict&diff=0&oldid=551959) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[goldendict](http://goldendict.org) es un programa de búsqueda de diccionarios con muchas funciones.

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") [goldendict](https://www.archlinux.org/packages/?name=goldendict) de los [repositorios oficiales](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)").

## Configuración

### Búsqueda de diccionario sin conexión con dictd

Primero `dictd` debe configurarse para alojar diccionarios sin conexión. Consulte [Hosting Offline Dictionaries](/index.php/Dictd#Hosting_Offline_Dictionaries "Dictd").

Una vez que se hayan instalado los diccionarios y se haya configurado `dictd`, se puede configurar `goldendict` para acceder a las bases de datos del diccionario `dictd` siguiendo estos pasos:

*   Presione F3 para abrir la ventana "Diccionarios".
*   Haga clic en la pestaña "Servidores DICT"
*   Haga clic en "Agregar ..."
*   Haga clic para poner una marca de verificación en "Habilitado"
*   Haga doble clic en "Dirección" y escriba: `dict://localhost`. Asegúrese de cambiar `localhost` si `dictd` se está ejecutando en otro servidor.
*   Finalmente haga clic en "Aceptar".