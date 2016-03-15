## Contents

*   [1 Aclaración](#Aclaraci.C3.B3n)
*   [2 Primero](#Primero)
*   [3 Instalación](#Instalaci.C3.B3n)
*   [4 Para que funcione Xorg](#Para_que_funcione_Xorg)
    *   [4.1 Teclado en X](#Teclado_en_X)
*   [5 Sobre las interfaces de red](#Sobre_las_interfaces_de_red)
*   [6 Evitar la degradacion del disco rigido](#Evitar_la_degradacion_del_disco_rigido)
*   [7 Si quieren velocidad](#Si_quieren_velocidad)
    *   [7.1 Entorno gráfico](#Entorno_gr.C3.A1fico)
    *   [7.2 Gestor de redes](#Gestor_de_redes)
    *   [7.3 Navegador web](#Navegador_web)
    *   [7.4 Optimizaciones](#Optimizaciones)
    *   [7.5 Kernel personalizado](#Kernel_personalizado)
    *   [7.6 Make CFlags para compilar](#Make_CFlags_para_compilar)
*   [8 Software ligero](#Software_ligero)

## Aclaración

Esta es una guía diferencial para instalar ArchLinux en una Netbook HP mini note 110-1020.

Es como yo instale en la mia, un modelo 1020LA (con teclado en español) y les indica solo las particularidades, para el proceso general se deben referir al correspondiente artículo [Guía para principiantes](/index.php/Gu%C3%ADa_para_Principiantes "Guía para Principiantes").

## Primero

Cuando booteen por primera vez, tengan en cuenta que deben editar la linea del kernel en el grub, agregando:

"acpi=off" ó bien, "noacpi" (sin las comillas"). De no hacerlo, se quedarán clavados en el inicio de ACPI o UDEV (desconozco la razón) pero luego de la instalación no es necesario para arrancar.

[agosto 2010]Con la nueva imagen Dual Boot no tuve ese problema.

## Instalación

La instalación la hacen normalmente y reinician con el sistema andando. Pero les recomiendo editar el **rc.conf** en la siguiente forma:

de un plumazo pongan en la lista negra el módulo de broadcom (placa wireless) "b43" y el de "ssb" aún no funcionan, a pesar que estan repotados de hacerlo con kernel 2.6.32+, con el 2.6.34 aún no resulta en mi caso. Espero que pronto lo haga, para no depender del driver privativo. Sin embargo, hasta la fecha de esta actualización (junio 2010) necesitamos instalar dicho driver, en AUR tenemos un paquete para ello: [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) y lo agregan a la lista de módulos como les indica al terminar de instalar el paquete.

[Agosto 2010] Desde el kernel 2.6.35 el módulo B43 funciona bien y es más estable que el de Broadcom. Sin embargo, el procedimiento para comenzar la conexion/desconexion es notablemente más largo. Eso es especialmente molesto a la hora de suspender la computadora ya que demora varios segundos para hacerlo.

Por el resto, desde el kernel 2.6.33 que solo funciona el driver intel con KMS, y realmente es una maravilla, por fin dejé de tener problemas de video, para pasar a una estabilidad ideal. Para activar KMS tienen el siguiente artículo en la wiki: [Intel (ver KMS)](/index.php/Intel "Intel").

Para futuras referencias el teclado responde a la distribución latinoamericana en el caso del modelo 1020LA, cuando editan /etc/rc.conf en la sección KEYMAP ponen "la-latin1" y todo va sobre ruedas en los inicios subsiguientes

## Para que funcione Xorg

El driver de video es xf86-video-intel, el del touchpad es xf86-input-synaptics, no dejen de instalar xf86-input-evdev y xf86-input-keyboard y xf86-input-mouse (para cuando usen un mouse usb). Pueden instalar el grupo completo con "pacman -S xf86-input-drivers".

**NO se olviden de agregar "hal" a la seccion de DAEMONS del /etc/rc.conf !!!**.

### Teclado en X

La configuración indicada es la "Latinoamericana" y la eligen desde la una terminal con

```
setxkbmap latam

```

pueden agregar otros idiomas para cuando conecten un teclado externo, poder elegirlos de la lista:

```
setxkbmap latam,es,us

```

[Agosto 2010] Desde Xorg 1.8 Hal no es más necesario para tener uso de teclado y mouse en X. Aunque Xfce 4.6 aún lo necesita para automontado de unidades extraíbles.

## Sobre las interfaces de red

Artículo a leer: [Broadcom BCM4312](/index.php/Broadcom_BCM4312 "Broadcom BCM4312") especialmente la sección sobre como evitar que intercambien las interfaces sus nombres: eth0 <==> eth1

les sugiero que el archivo /etc/udev/rules.d/10-network.rules lo dejen así:

```
SUBSYSTEM=="net", ATTRS{address}=="00:26:XX:XX:XX:XX", NAME="eth0"
SUBSYSTEM=="net", ATTRS{address}=="00:26:XX:XX:XX:XX", NAME="wlan0"

```

Así pueden diferenciar facilmente la interface inalambrica de la cableada. Allí mismo tienen todas las actualizaciones sobre los drivers para la placa.

## Evitar la degradacion del disco rigido

Un problema bien conocido sobre el elevado conteo de ciclos de carga (load cycle count) de los discos rígidos de las portátiles con linux durante la presencia de las baterias, se soluciona cambiando los parametros con hdparm. Lo instalan con

```
#pacman -S hdparm

```

y agregan al rc.local

```
hdparm -B 254 /dev/sda

```

si quieren comprobar cuantos ciclos de carga lleva el disco, instalen smartmontools

```
#pacman -S smartmontools

```

y usan:

```
smartctl -a /dev/sda | grep Load_Cycle_Count

```

La salida es algo así:

```
193 Load_Cycle_Count        0x0032   097   097   000    Old_age   Always       -       31633

```

El ultimo numero es la cuenta. Tengan a consideracion que la vida util de los discos rigidos es de entre 300.000 y 600.000

## Si quieren velocidad

### Entorno gráfico

Mi recomendación: [Xfce](/index.php/Xfce "Xfce") o [LXDE](/index.php/LXDE "LXDE"); ambos son muy buenos, ligeros y rápidos. Mi elección: XFCE, es más facilmente configurable sobretodo a la hora de usar atajos de teclado, y tiene muchos plugins interesantes.

### Gestor de redes

Casi obligado es usar [WICD](/index.php/Wicd "Wicd"), rápido, ligero y siempre anda. No tiene dependencias pesadas y anda perfectamente con cualquiera de los dos escritorios arriba nombrados.

### Navegador web

Hoy: Chromium, le pasa el trapo al resto, anda casi perfecto y 10 veces más rápido. Ya esta en los repositorios oficiales y lo instalan con pacman.

Tengan en cuenta que Chromium no se lleva bien con los proxy, asi que si van a navegar en una red que los pone detras de uno, se van a llevar una mala sorpresa, para esos casos yo uso el tan querido Firefox, tambien disponible en los repositorios de nuestra distro en cuestión.

### Optimizaciones

Hay varias, aqui van a encontrar las más comunes y recomendadas: [Acelerar el arranque](/index.php/Speedup_boot "Speedup boot"); aunque yo solo recomiendo alterar la secuencia de carga de los daemons en el rc.conf para manejar el tiempo de arranque, poniendo una "@" delante de todos, menos hal y los daemons de red como "network" ó "wicd".

### Kernel personalizado

Infaltable, reduce sus tiempos de arranque y su sistema corre mucho mejor, especialmente porque elegimos el tipo de procesador "ATOM" que viene con nuestra netbook y se optimiza todo para el mismo. Quitamos todo lo que no necesitamos (soporte para AMD, IDE, RAID y demás) y nos queda un kernel con todo lo necesario y los módulos de lo que podemos llegar a usar.

Cuando termine de armar el paquete para AUR que funcione bien incluiré aquí la referencia, por lo pronto, el que quira, me envía un mensaje y le puedo facilitar el ".config" que uso en la compilación del último kernel.

### Make CFlags para compilar

Editen el [makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf") para que compile con las optimizaciones para su procesador específico.

## Software ligero

No dejen de leer este artículo: [Aplicaciones Ligeras](/index.php/Lightweight_Applications "Lightweight Applications")

Parte del soft que elegí con mucho esmero para mi netbook es el que listo aquí:

[DeadBeef](https://aur.archlinux.org/packages.php?ID=29502) : reproductor de audio de alta calidad.

Leafpad: Editor de textos simple (sin dependencias).

Abiword: Procesador de textos.

Gnumeric: Hoja de cálculo.

Xarchiver: Interface gráfica para utilitarios de compresión.

Thunar: Administrador de archivos y escritorio con papelera.

RXVT-unicode: terminal, aún mas ligera que xterm y muy estable.

[localepurge](https://aur.archlinux.org/packages/localepurge/): eliminar archivos de localización innecesarios.

ePDFViewer: visor de PDF.

Mplayer: reproductor multimedia.

UFW: firewall sin complicaciones.

GUFW: interface gtk para UFW.

WiCD: administrador de conexiones de red.

gpicview: Visor de imágenes.

galculator: calculadora.

truecrypt: encriptar información o particiones.

Eso es todo, Salu2