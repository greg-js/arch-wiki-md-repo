**Estado de la traducción**
Este artículo es una traducción de [Maple](/index.php/Maple "Maple"), revisada por última vez el **2018-11-04**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Maple&diff=0&oldid=553066) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Octave](/index.php/Octave "Octave")
*   [Sage-mathematics](/index.php/Sage-mathematics "Sage-mathematics")
*   [Mathematica](/index.php/Mathematica "Mathematica")
*   [Matlab](/index.php/Matlab "Matlab")

De su [página web oficial](http://www.maplesoft.com/products/maple/):

	Maple es un lenguaje de alto nivel y un entorno interactivo para computación numérica, visualización y programación. Con Maple, puede analizar datos, desarrollar algoritmos y crear modelos y aplicaciones. El lenguaje, las herramientas y las funciones matemáticas integradas le permiten explorar múltiples enfoques y alcanzar una solución más rápido que con hojas de cálculo o lenguajes de programación tradicionales, como C/C++ o Java.

Maple es un software propietario producido por Maplesoft y requiere una licencia para obtener, instalar y activar. Arch no tiene soporte oficial, pero el instalador provisto por Maplesoft puede funcionar en algunos casos.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Solución de problemas](#Soluci.C3.B3n_de_problemas)
    *   [2.1 Error al determinar el ID de host del servidor de licencias](#Error_al_determinar_el_ID_de_host_del_servidor_de_licencias)
    *   [2.2 Ventana principal en blanco con gestores de ventanas de mosaico](#Ventana_principal_en_blanco_con_gestores_de_ventanas_de_mosaico)
    *   [2.3 Los diagramas 3D fallan](#Los_diagramas_3D_fallan)
    *   [2.4 Activación offline](#Activaci.C3.B3n_offline)

## Instalación

Maplesoft proporciona un script de instalación que puede funcionar en algunas instalaciones de Arch Linux. La versión 18 es compatible con [maple18](https://aur.archlinux.org/packages/maple18/). Asegúrese de tener una instalación [Java](/index.php/Java_(Espa%C3%B1ol) "Java (Español)") en funcionamiento antes de comenzar.

Después de comprar su licencia, [descargue](http://www.maplesoft.com/support/downloads/) el paquete de Maple correspondiente y desempaquételo en la ubicación que elija. Abra un terminal, cambie al directorio en el que desempaquetó los archivos y ejecute el script de instalación como usuario normal. Por defecto, la instalación de los archivos del programa se hará dentro del directorio de inicio del usuario, y permite eliminar fácilmente todos los componentes en un momento posterior.

Una vez que el paquete está instalado, deberá proporcionar un código de activación de licencia. Esto debería haber sido incluido en su archivo de instalación.

## Solución de problemas

### Error al determinar el ID de host del servidor de licencias

Para que Maple acepte su código de activación, es posible que deba [instalar](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [ld-lsb](https://www.archlinux.org/packages/?name=ld-lsb). Esto falsificará un runtime básico estándar de Linux y convencerá al servidor de autenticación para que acepte su código de activación válido. El paquete [lsb-release](https://www.archlinux.org/packages/?name=lsb-release) no resuelve este problema, como [la página de soporte de instalación de MapleSoft](http://www.maplesoft.com/support/Faqs/detail.aspx?sid=32610) puede llevar a uno a creer.

### Ventana principal en blanco con gestores de ventanas de mosaico

Véase [Java#Non-reparenting window managers / Grey window / Programs not drawing properly](/index.php/Java#Non-reparenting_window_managers_.2F_Grey_window_.2F_Programs_not_drawing_properly "Java")

### Los diagramas 3D fallan

Maple se expide con su propio runtime de C++, que parece causar problemas con el renderizado 3D (plot3d, implicitplot3d, ...).

En cambio, vincular el libstdc++ del sistema parece solucionar el problema, por ejemplo, para Maple 2016 en sistemas x64, vaya a

```
   maple2016/bin.X86_64_LINUX/system

```

y vincule libstdc++.so.6.0.20 y libstdc++.so.6 a la versión de su sistema:

```
   libstdc++.so.6 -> /usr/lib64/libstdc++.so.6
   libstdc++.so.6.0.20 -> /usr/lib64/libstdc++.so.6.0.22

```

### Activación offline

Si la activación por clave de licencia no funciona, puede probar la [activación sin conexión](https://www.maplesoft.com/contact/webforms/offlineactivation/index.aspx).

Ingrese su clave de licencia en el campo *Purchase Code* y seleccione o bien *Host ID* o *Disk Serial Number* como método de activación de hardware.

Para obtener su ID de host, ejecute el siguiente comando:

```
   ip address show | grep link/ether | awk '{ print $2; }' | sed 's/://g'

```

y use una de las IDs resultantes.

Ingrese su dirección de correo electrónico (o use una desechable), luego copie los contenidos a `*maplehome*/license/license.dat`.

Esto debería activar Maple en el próximo arranque.