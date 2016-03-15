[Los módulos del núcleo](https://en.wikipedia.org/wiki/Loadable_kernel_module "wikipedia:Loadable kernel module") (también conocido por su nombre inglés, *kernel*) son ​​fragmentos de código que pueden ser cargados y eliminados del núcleo bajo demanda. Extienden la funcionalidad del núcleo sin necesidad de reiniciar el sistema.

## Contents

*   [1 Descripción](#Descripci.C3.B3n)
*   [2 Obtener información](#Obtener_informaci.C3.B3n)
*   [3 Configuración](#Configuraci.C3.B3n)
    *   [3.1 Cargar módulos](#Cargar_m.C3.B3dulos)
    *   [3.2 Configurar opciones de los módulos](#Configurar_opciones_de_los_m.C3.B3dulos)
        *   [3.2.1 Usar archivos en /etc/modprobe.d/](#Usar_archivos_en_.2Fetc.2Fmodprobe.d.2F)
        *   [3.2.2 Usar la línea de órdenes de arranque del núcleo](#Usar_la_l.C3.ADnea_de_.C3.B3rdenes_de_arranque_del_n.C3.BAcleo)
    *   [3.3 Alias](#Alias)
    *   [3.4 Lista negra](#Lista_negra)
        *   [3.4.1 Usar archivos en /etc/modprobe.d/](#Usar_archivos_en_.2Fetc.2Fmodprobe.d.2F_2)
        *   [3.4.2 Usar la línea de órdenes del núcleo](#Usar_la_l.C3.ADnea_de_.C3.B3rdenes_del_n.C3.BAcleo)
*   [4 Manejar módulos manualmente](#Manejar_m.C3.B3dulos_manualmente)
*   [5 Consejos y trucos](#Consejos_y_trucos)
    *   [5.1 Función de bash para listar los parámetros del módulo](#Funci.C3.B3n_de_bash_para_listar_los_par.C3.A1metros_del_m.C3.B3dulo)
*   [6 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Descripción

Para conocer cómo crear un módulo del núcleo, puede leer [esta guía](http://tldp.org/LDP/lkmpg/2.6/html/index.html). Un módulo puede ser configurado para ser compilable (incluso en el núcleo) o cargable (se puede cargar bajo demanda). Para cargar o eliminar dinámicamente un módulo, tiene que estar configurado como un módulo cargable en la configuración del núcleo (la línea relacionada con el módulo, por lo tanto, se mostrará con la letra `M`).

Los módulos se almacenan en `/lib/modules/*nombre_del_kernel*`. Use la orden `uname -r` para obtener su versión actual del núcleo.

**Nota:** Los nombres de los módulos suelen utilizar guiones bajos (`_`) o guiones (`-`), sin embargo, esos símbolos son intercambiables, tanto cuando se utiliza la orden `modprobe` como en los archivos de configuración del directorio `/etc/modprobe.d/`.

## Obtener información

Para mostrar los módulos del núcleo cargados actualmente:

```
 $ lsmod

```

Para mostrar información sobre un módulo:

```
 $ modinfo *nombre_del_módulo*

```

Para listar las opciones que se establecen para un módulo cargado:

```
 $ systool -v -m *nombre_del_módulo*

```

Para mostrar la configuración completa de todos los módulos:

```
 $ modprobe -c | less

```

Para mostrar la configuración de un módulo en particular:

```
 $ modprobe -c | grep *nombre_del_módulo*

```

Listar las dependencias de un módulo (o alias), incluido el propio módulo:

```
 $ modprobe --show-depends *nombre_del_módulo*

```

## Configuración

Hoy en día, todos los módulos que necesitan ser cargados, son manejados automáticamente por udev, por lo que si no quiere/necesita utilizar ningún módulo ajeno al núcleo, no hay necesidad de ponerlos en algún archivo de configuración para que se carguen en el arranque. Sin embargo, hay casos en que es posible que desee cargar un módulo específico adicional durante el proceso de arranque, o crear una lista negra de módulos (los cuales no se cargarán) para que el equipo funcione correctamente.

### Cargar módulos

Los módulos adicionales del *kernel* pueden ser cargados durante el arranque configurándolos como una lista estática en los archivos residentes en `/etc/modules-load.d/`. Cada archivo de configuración es nombrado siguiendo el formato: `/etc/modules-load.d/<programa>.conf`. Los archivos de configuración contienen simplemente una lista de los nombres de los módulos del núcleo a cargar, separadas por saltos de líneas. Las líneas vacías y las líneas cuyo primer carácter sea `#` o `;` serán ignoradas.

 `/etc/modules-load.d/virtio-net.conf` 
```
# Carga virtio-net.ko al arranque
virtio-net
```

Consulte `modules-load.d(5)` para obtener más información.

### Configurar opciones de los módulos

Para pasar un parámetro a un módulo puede usar un archivo de configuración en la carpeta modprobe o utilizar la línea de órdenes del núcleo.

#### Usar archivos en /etc/modprobe.d/

El directorio `/etc/modprobe.d/` se puede utilizar para pasar la configuración de los módulos a [udev](/index.php/Udev_(Espa%C3%B1ol) "Udev (Español)"), el cual utilizará `modprobe` para manejar la carga de los módulos durante el arranque del sistema. Puede crear un archivo de configuración con cualquier nombre en aquel directorio, siempre que acaben con la extensión `.conf`. La sintaxis es la siguiente:

 `/etc/modprobe.d/miarchivo.conf`  `options nombredelmódulo nombredelparámetro=valordelparámetro` 

Por ejemplo:

 `/etc/modprobe.d/thinkfan.conf` 
```
# Thinkpads on, ésto permite que el demonio thinkfan controle la velocidad del ventilador
options thinkpad_acpi fan_control=1
```

**Nota:** Si cualquiera de los módulos afectados se cargan durante el arranque (desde el ramdisk de inicio), entonces tendrá que añadir el correspondiente archivo `.conf` a FILES en [mkinitcpio.conf](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)"), o usar el [hook](/index.php/Mkinitcpio.conf#HOOKS "Mkinitcpio.conf") `modconf`, para que se incluya en el ramdisk.

#### Usar la línea de órdenes de arranque del núcleo

Si el módulo está integrado en el núcleo también puede pasar opciones al módulo a través de la línea de órdenes. Para todos los cargadores de arranque (*bootloader*) más comunes la sintaxis correcta es:

```
nombredelmódulo.nombredelparámetro=valordelparámetro

```

por ejemplo:

```
thinkpad_acpi.fan_control=1

```

Simplemente añada esto a la línea de órdenes del núcleo de su gestor de arranque como se describe en los [parámetros del núcleo](/index.php/Kernel_parameters#When_starting_the_kernel "Kernel parameters").

### Alias

Los alias son nombres alternativos para un módulo. Por ejemplo: `alias mi-mod nombre_de_módulo_muy_largo` significa que puede utilizar `modprobe mi-mod` en lugar de `modprobe nombre_de_módulo_muy_largo`. También puede utilizar comodines del estilo shell, por lo que `alias mi-mod* nombre_de_módulo_muy_largo` significa que `modprobe mi-mod-cualquier-cosa` tiene el mismo efecto. Crear un alias:

 `/etc/modprobe.d/mialias.conf`  `alias mimod nombre_de_módulo_muy_largo` 

Algunos módulos tienen alias que se utilizan para su carga automática cuando son solicitados por una aplicación. La desactivación de estos alias evitará que se cargue automáticamente, pero permitirá que se puedan cargar manualmente. Ejemplo:

 `/etc/modprobe.d/modprobe.conf` 
```
# Evita cargar automáticamente el módulo necesario para bluetooth
alias net-pf-31 off
```

### Lista negra

Incluir en la lista negra (*«blacklisting»*), en el contexto de los módulos del núcleo, es un mecanismo que evita que el núcleo cargue dicho módulo. Esto podría ser útil si, por ejemplo, el dispositivo de hardware asociado con el módulo no se utiliza y no desea que funcione, o porque la carga del módulo crea problemas: por ejemplo, puede darse la carga simultánea de dos módulos que intentan controlar el mismo dispositivo o componente del hardware, y cargándolos en conjunto se traduciría en un conflicto.

Algunos módulos se cargan como parte de [initramfs](/index.php/Initramfs "Initramfs"). `mkinitcpio -M` mostrará todos los módulos detectados automáticamente: para evitar que initramfs cargue algunos de estos módulos, se utiliza la lista negra (*«blacklist»*) en `/etc/modprobe.d/modprobe.conf`. La ejecución de `mkinitcpio -v` mostrará una lista de todos los módulos insertados en initramfs por los distintos hooks (por ejemplo, hook filesystem, hook SCSI, etc.) Recuerde reconstruir el initramfs una vez haya hecho la lista negra de los módulos y reiniciar el sistema después.

#### Usar archivos en /etc/modprobe.d/

Crear un archivo `.conf` dentro de `/etc/modprobe.d/` y añadir una línea para cada módulo que desee a la lista negra, usando la palabra clave `blacklist`. Por ejemplo, si desea evitar que el módulo `pcspkr` se cargue:

 `/etc/modprobe.d/nobeep.conf` 
```
# Esto evitará la carga del módulo pcspkr que controla el altavoz de la placa base
blacklist pcspkr
```

**Nota:** El uso de la opción `blacklist` respecto de un módulo hará que este no se cargue de forma automática, pero el módulo se puede cargar si otro módulo que no esté en la lista negra depende de él o si se carga de forma manual, con lo que iniciado este último se cargaría el primero, a pesar de estar incluido en la lista negra.

Sin embargo, hay una solución para este comportamiento, la orden `install` instruye a modprobe para ejecutar una orden personalizada, en lugar de insertar el módulo en la memoria, con lo que puede forzar que se impida la carga del módulo usando:

 `/etc/modprobe.d/blacklist.conf` 
```
...
install MODULE_NAME /bin/false
...
```
Esto hace efectivo la inclusión en la «lista negra» de ese módulo y de cualquier otro que dependa de él.

#### Usar la línea de órdenes del núcleo

**Sugerencia:** Esto es útil en casos de emergencia cuando un módulo falla evitando un inicio correcto del sistema.

También puede evitar la carga de módulos a través del gestor de arranque.

Agregue `modprobe.blacklist=modname1,modname2,modname3` en la línea de órdenes del núcleo de su gestor de arranque como se describe en los [parámetros del núcleo](/index.php/Kernel_parameters#When_starting_the_kernel "Kernel parameters").

**Nota:** Cuando están en lista negra más de un módulo, tenga en cuenta que los mismos deben estar separados por comas solamente. Los espacios o cualquier otra cosa presumiblemente podría romper la sintaxis.

## Manejar módulos manualmente

Los módulos del núcleo pueden ser manejados con las herramientas proporcionadas por el paquete [kmod](https://www.archlinux.org/packages/?name=kmod). Estas herramientas pueden ser utilizadas manualmente.

Para cargar un módulo:

```
# modprobe *nombre_del_módulo*

```

Para quitar/retirar un módulo:

```
# modprobe -r *nombre_del_módulo*

```

O, alternativamente:

```
# rmmod *nombre_del_módulo*

```

## Consejos y trucos

### Función de bash para listar los parámetros del módulo

Esta es una función de bash que debe ser ejecutada como root, que mostrará una lista de todos los módulos actualmente cargados y todos sus parámetros, incluido el valor actual del parámetro. Utilice `/proc/modules` para obtener una lista actualizada de los módulos cargados, a continuación, acceder al archivo del módulo directamente con modinfo para tomar una descripción del módulo y las descripciones para cada parámetro (si está disponible), y finalmente acceda al sistema de archivos sysfs para tomar los nombres de los parámetros reales y los valores cargados en ese momento .

```
function aa_mod_parameters () 
{ 
    N=/dev/null;
    C=`tput op` O=$(echo -en "
`tput setaf 2`>>> `tput op`");
    for mod in $(cat /proc/modules|cut -d" " -f1);
    do
        md=/sys/module/$mod/parameters;
        [[ ! -d $md ]] && continue;
        m=$mod;
        d=`modinfo -d $m 2>$N | tr "
" "\t"`;
        echo -en "$O$m$C";
        [[ ${#d} -gt 0 ]] && echo -n " - $d";
        echo;
        for mc in $(cd $md; echo *);
        do
            de=`modinfo -p $mod 2>$N | grep ^$mc 2>$N|sed "s/^$mc=//" 2>$N`;
            echo -en "\t$mc=`cat $md/$mc 2>$N`";
            [[ ${#de} -gt 1 ]] && echo -en " - $de";
            echo;
        done;
    done
}
```

Aquí está un ejemplo de salida.

 `# aa_mod_parameters` 
```
>>> ehci_hcd - USB 2.0 'Enhanced' Host Controller (EHCI) Driver
        hird=0 - hird:host initiated resume duration, +1 for each 75us (int)
        ignore_oc=N - ignore_oc:ignore bogus hardware overcurrent indications (bool)
        log2_irq_thresh=0 - log2_irq_thresh:log2 IRQ latency, 1-64 microframes (int)
        park=0 - park:park setting; 1-3 back-to-back async packets (uint)

>>> processor - ACPI Processor Driver
        ignore_ppc=-1 - ignore_ppc:If the frequency of your machine gets wronglylimited by BIOS, this should help (int)
        ignore_tpc=0 - ignore_tpc:Disable broken BIOS _TPC throttling support (int)
        latency_factor=2 - latency_factor: (uint)

>>> usb_storage - USB Mass Storage driver for Linux
        delay_use=1 - delay_use:seconds to delay before using a new device (uint)
        option_zero_cd=1 - option_zero_cd:ZeroCD mode (1=Force Modem (default), 2=Allow CD-Rom (uint)
        quirks= - quirks:supplemental list of device IDs and their quirks (string)
        swi_tru_install=1 - swi_tru_install:TRU-Install mode (1=Full Logic (def), 2=Force CD-Rom, 3=Force Modem) (uint)

>>> video - ACPI Video Driver
        allow_duplicates=N - allow_duplicates: (bool)
        brightness_switch_enabled=Y - brightness_switch_enabled: (bool)
        use_bios_initial_backlight=Y - use_bios_initial_backlight: (bool)
```

Lo que sigue es una variación de la función anterior, que incluye una descripción completa de cada parámetro. La salida tiene un formato ligeramente diferente y utiliza más colores.

```
function show_mod_parameter_info ()
{
  if tty -s <&1
  then
    green="\e[1;32m"
    yellow="\e[1;33m"
    cyan="\e[1;36m"
    reset="\e[0m"
  else
    green=
    yellow=
    cyan=
    reset=
  fi
  newline="
"

  while read mod
  do
    md=/sys/module/$mod/parameters
    [[ ! -d $md ]] && continue
    d="$(modinfo -d $mod 2>/dev/null | tr "
" "\t")"
    echo -en "$green$mod$reset"
    [[ ${#d} -gt 0 ]] && echo -n " - $d"
    echo
    pnames=()
    pdescs=()
    pvals=()
    pdesc=
    add_desc=false
    while IFS="$newline" read p
    do
      if [[ $p =~ ^[[:space:]] ]]
      then
        pdesc+="$newline    $p"
      else
        $add_desc && pdescs+=("$pdesc")
        pname="${p%%:*}"
        pnames+=("$pname")
        pdesc=("    ${p#*:}")
        pvals+=("$(cat $md/$pname 2>/dev/null)")
      fi
      add_desc=true
    done < <(modinfo -p $mod 2>/dev/null)
    $add_desc && pdescs+=("$pdesc")
    for ((i=0; i<${#pnames[@]}; i++))
    do
      printf "  $cyan%s$reset = $yellow%s$reset
%s
" \
        ${pnames[i]} \
        "${pvals[i]}" \
        "${pdescs[i]}"
    done
    echo

  done < <(cut -d' ' -f1 /proc/modules | sort)
}

```

## Véase también

*   [modprobe man page](http://linuxmanpages.com/man5/modprobe.conf.5.php)
*   [Disable PC Speaker Beep (Español)](/index.php/Disable_PC_Speaker_Beep_(Espa%C3%B1ol) "Disable PC Speaker Beep (Español)")