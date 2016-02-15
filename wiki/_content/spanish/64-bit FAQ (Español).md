## Contents

*   [1 ¿Cómo determino si mi procesador es compatible con x86_64?](#.C2.BFC.C3.B3mo_determino_si_mi_procesador_es_compatible_con_x86_64.3F)
*   [2 ¿Cuál versión de Arch debería usar: 32 o 64 bit?](#.C2.BFCu.C3.A1l_versi.C3.B3n_de_Arch_deber.C3.ADa_usar:_32_o_64_bit.3F)
*   [3 ¿Cómo puedo instalar Arch64?](#.C2.BFC.C3.B3mo_puedo_instalar_Arch64.3F)
*   [4 ¿Qué tan completo es el port? ¿tendré todos los paquetes que uso en Arch32?](#.C2.BFQu.C3.A9_tan_completo_es_el_port.3F_.C2.BFtendr.C3.A9_todos_los_paquetes_que_uso_en_Arch32.3F)
*   [5 ¿El uso de los 64 bits significa un gran aumento de rendimiento?](#.C2.BFEl_uso_de_los_64_bits_significa_un_gran_aumento_de_rendimiento.3F)
*   [6 ¡Atención si actualizas glibc en una versión anterior a la 2.4!](#.C2.A1Atenci.C3.B3n_si_actualizas_glibc_en_una_versi.C3.B3n_anterior_a_la_2.4.21)
*   [7 ¿Cómo puedo reportar bugs?](#.C2.BFC.C3.B3mo_puedo_reportar_bugs.3F)
*   [8 ¿Tienen una lista de correo?](#.C2.BFTienen_una_lista_de_correo.3F)
*   [9 ¿Qué repositorios debería agregar para pacman?](#.C2.BFQu.C3.A9_repositorios_deber.C3.ADa_agregar_para_pacman.3F)
*   [10 ¿Cómo puedo conseguir los PKGBUILDs para Arch64?](#.C2.BFC.C3.B3mo_puedo_conseguir_los_PKGBUILDs_para_Arch64.3F)
*   [11 ¿Cómo puedo crear paquetes para Arch64 usando PKGBUILDs para 32-bit?](#.C2.BFC.C3.B3mo_puedo_crear_paquetes_para_Arch64_usando_PKGBUILDs_para_32-bit.3F)
*   [12 ¿Como puedo parchar PKGBUILDs existentes para usar con Arch64?](#.C2.BFComo_puedo_parchar_PKGBUILDs_existentes_para_usar_con_Arch64.3F)
*   [13 ¿Qué perderé con Arch64?](#.C2.BFQu.C3.A9_perder.C3.A9_con_Arch64.3F)
*   [14 ¿Puedo compilar paquetes de 32-bit para i686 dentro de Arch64?](#.C2.BFPuedo_compilar_paquetes_de_32-bit_para_i686_dentro_de_Arch64.3F)
*   [15 ¿Puedo usar aplicaciones de 32-bit en Arch64?](#.C2.BFPuedo_usar_aplicaciones_de_32-bit_en_Arch64.3F)
*   [16 ¿Puedo actualizar/cambiar mi sistema de i686 a x86_64 sin reinstalar?](#.C2.BFPuedo_actualizar.2Fcambiar_mi_sistema_de_i686_a_x86_64_sin_reinstalar.3F)

## ¿Cómo determino si mi procesador es compatible con x86_64?

Ejecute la siguiente instrucción:

```
$ less /proc/cpuinfo

```

Busque la entrada "flags". Si ve la bandera "lm" entonces su procesador es compatible con x86_64.

O puede ejecutar esta instrucción:

```
$ grep "^flags.*\blm\b" /proc/cpuinfo

```

## ¿Cuál versión de Arch debería usar: 32 o 64 bit?

Si su procesador es compatible con [x86_64](http://es.wikipedia.org/wiki/X86-64), debería usar Arch64 a menos que piense usar programas [sin soporte](#.C2.BFQu.C3.A9_perder.C3.A9_con_Arch64.3F). Es importante notar que Arch32 por defecto no soporta más de 3GB de RAM: tiene que usar Arch64 si tiene más de 3GB de RAM.

## ¿Cómo puedo instalar Arch64?

Solo usa la [ISO Oficial (x86_64)](https://www.archlinux.org/download/).

## ¿Qué tan completo es el port? ¿tendré todos los paquetes que uso en Arch32?

Los repositorios Core y Extra son portados y casi todo está actualizado, solo unas horas (o unos pocos días como mucho) atrás que Arch Linux i686\. Los Usuarios Confiables están tratando de portar el repositorio comunitario ahora.

El port está listo para equipos de escritorio y servidores.

## ¿El uso de los 64 bits significa un gran aumento de rendimiento?

Es así en la mayoría de las aplicaciones que usan los registros de 64-bit (como las aplicaciones para grandes bases de datos). Algunas aplicaciones multimedia funcionarán notoriamente más rápido. Si conoces una aplicación que funcione más rápido en SSE3 puedes recompilar el paquete por ti mismo. Arch64 _solamente_ es compilado con soporte para SSE2 y con optimizaciones -O2. Para más información, lea [http://forums.gentoo.org/viewtopic.php?t=221045](http://forums.gentoo.org/viewtopic.php?t=221045) o [http://www.thejemreport.com/mambo/content/view/74/74/](http://www.thejemreport.com/mambo/content/view/74/74/) (Inglés).

Para el resto del sistema: No hace ninguna diferencia notable.

## ¡Atención si actualizas glibc en una versión anterior a la 2.4!

Es importante si actualizas glibc desde una versión inferior a la 2.4 que lo hagas desde un paso separado. Solo haz `pacman -Sy glibc` y si salió bien haz `pacman -Su`. Si no, las librerías no se moverán correctamente y deberás usar pacman.static para arreglarlo.

## ¿Cómo puedo reportar bugs?

Repórtalo normalmente, pero asegúrate de aclarar que es x86_64 si crees que es un problema del port.

## ¿Tienen una lista de correo?

Sí, hay [una lista de correo](https://archlinux.org/mailman/listinfo/arch-ports) para los ports de Arch.

## ¿Qué repositorios debería agregar para pacman?

El port soporta todos los repositorios.

## ¿Cómo puedo conseguir los PKGBUILDs para Arch64?

Tenemos _**ABS**_ como en el Arch de 32-bit. Se recomienda mirar _/var/abs_. _abs_ busca todas las entradas CVS de archlinux.org que contengan la etiqueta "CURRENT-64".

## ¿Cómo puedo crear paquetes para Arch64 usando PKGBUILDs para 32-bit?

Tenemos PKGBUILDs en común con Arch32\. Puedes obtener PKGBUILDs todavía no portados, para 32-bit desde el CVS: [https://www.archlinux.org/cvs/](https://www.archlinux.org/cvs/)

## ¿Como puedo parchar PKGBUILDs existentes para usar con Arch64?

Añadimos esta variable a todos los paquetes portados:

```
arch=('i686' 'x86_64') 

```

Añade parches directamente al código fuente y cambia los md5sums:

```
[ "$CARCH" = "x86_64" ] && source=(${source[@]} 'otro código fuente')
[ "$CARCH" = "x86_64" ] && md5sums=(${md5sums[@]} 'otro md5sum')

```

Para un arreglo pequeño usa esto y compila:

```
[ "$CARCH" = "x86_64" ] && (patch -Np0 -i ../foo_x86_64.patch || return 1)

```

O, cuando necesitas más cambios:

```
if [ "$CARCH" = "x86_64" ]; then
    configure/patch/sed      # para x86_64
  else configure/patch/sed   # para i686
fi

```

Para los desarrolladores:

```
cvs commit -m "x86_64 updated/fixed o lo que sea"
cvs tag -cFR CURRENT-64 foo-package-directory (incluso para extra, community, unstable y testing)

```

## ¿Qué perderé con Arch64?

Nada en realidad. Casi todas las aplicaciones ahora son compatibles con 64 bits o se encuentran en la transición para hacer posible esta compatibilidad.

El mayor problema son los paquetes que son de **código cerrado** o bien contienen ensamblados específicos para x86 que son realmente incómodos para portar (típico de los emuladores).

Estas aplicaciones tuvieron conflictos en el pasado, sin embargo ahora están disponibles en [AUR](/index.php/AUR "AUR") y trabajan bien:

*   Acrobat Reader no se encuentra disponible en 64 bits, pero se puede ejecutar la versión de 32 bits en modo de compatibilidad. También hay muchas otras alternativas de código abierto que pueden ser utilizadas para leer archivos PDF.

Todo lo demas deberia funcionar perfectamente. No obstante si necesitas un paquete de Arch32 que no se haya portado aun, y sabes que se puede compilar en x86_64 sin usar multilibs, puedes hablar con los desarrolladores.

## ¿Puedo compilar paquetes de 32-bit para i686 dentro de Arch64?

Si. Necesitas un chroot de i686 en funcionamiento (recomendada la instalación rápida de la ISO i686 para tenerlo rápidamente en Arch64). Instala el paquete "linux32" para lograr que chroot se comporte como un sistema i686\. Luego usa este script para logearte dentro de chroot como root:

```
#!/bin/bash
mount --bind /dev /dirección-de-tu-chroot/dev
mount --bind /dev/pts /dirección-de-tu-chroot/dev/pts
mount --bind /dev/shm /dirección-de-tu-chroot/dev/shm
mount -t proc none /dirección-de-tu-chroot/proc
mount -t sysfs none /dirección-de-tu-chroot/sys
linux32 chroot /dirección-de-tu-chroot

```

Si tienes el código del programa en el host x86_64 puedes añadir

```
"mount --bind /dirección-a-las-fuentes /dirección-de-tu-chroot/dirección-a-las-fuentes" 

```

para compartir el código entre el host y el sistema chroot.

## ¿Puedo usar aplicaciones de 32-bit en Arch64?

¡Sí!

**PERO: ¡Nuestra meta es ser la distribución más actualizada! los 32-bit están pasados de moda. Queremos que Arch64 sea moderna y puramente de 64-bit. Así que no tenemos un sistema "Multilib". No añadiremos ningún paquete que requiera compatibilidad con 32-bit. Puede que los dejemos en AUR o en el repositorio comunitario.** _**¡No esperes obtener ningún soporte por parte de los desarrolladores para tener aplicaciones de 32-bit ejecutándose en Arch64!**_

*   Puedes instalar todas las librerías lib32-* desde el repositorio multilib. Para usar este repositorio debes agregar las siguientes líneas a tu pacman.conf:

```
 [multilib]
 Include = /etc/pacman.d/mirrorlist

```

*   O puedes crear una jaula chroot con un sistema de 32bit. Inicia en Arch64, startx, abre una terminal.

```
$ xhost +local:
$ su
# mount /dev/sda1 /mnt/arch32
# mount --bind /proc /mnt/arch32/proc
# chroot /mnt/arch32
$ su your32bitusername
# /usr/bin/orden-que-quieres-correr  # ejemplo: /opt/mozilla/bin/firefox

```

Algunas aplicaciones de 32-bit (como OpenOffice) pueden requerir configuraciones adicionales. Las siguientes líneas se pueden agregar al rc.local para asegurarse de tener todo lo necesario para 32-bit.

(Asumiendo que /mnt/arch32 está montado en fstab):

```
mount --bind /dev /mnt/arch32/dev
mount --bind /dev/pts /mnt/arch32/dev/pts
mount --bind /dev/shm /mnt/arch32/dev/shm
mount --bind /proc /mnt/arch32/proc
mount --bind /proc/bus/usb /mnt/arch32/proc/bus/usb
mount --bind /sys /mnt/arch32/sys
mount --bind /tmp /mnt/arch32/tmp
# comenta la siguiente línea si no usas el mismo directorio "home"
mount --bind /home /mnt/arch32/home

```

Luego, en una terminal, puedes hacer:

```
$ xhost +localhost
$ sudo chroot /mnt/arch32 su tu_usuario_en_32bit /opt/openoffice/program/soffice

```

## ¿Puedo actualizar/cambiar mi sistema de i686 a x86_64 sin reinstalar?

No. De todas maneras, puedes inicia desde el CD de Arch64, montar el disco, y borrar todo, excepto lo que quieras conservar, siempre y cuando no sea un binario de 32-bit y luego instalar.