**Nota:** En proceso de traducción

Artículos relacionados

*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System")
*   [pacman](/index.php/Pacman "Pacman")
*   [Arch Rollback Machine](/index.php/Arch_Rollback_Machine "Arch Rollback Machine")

Antes de desactualizar uno o varios paquetes, considere por qué desea hacerlo. Si se debe a un error, busque en [rastreador de errores](https://bugs.archlinux.org/) las tareas existentes. Si no hay ninguna, agregue un nueva tarea; es mejor corregir los errores, o al menos advertir a otros usuarios de posibles problemas.

**Advertencia:**

*   La desactualización de un paquete puede requerir que sus dependencias también sean desactualizadas. Cuando el número de paquetes a desactualizar es grande, considere usar una instantánea. Ver [Cómo restaurar todos los paquetes a una fecha específica.](/index.php/Arch_Linux_Archive#How_to_restore_all_packages_to_a_specific_date "Arch Linux Archive").
*   Tenga cuidado con los cambios en los archivos de configuración y scripts. Por ahora, pacman se encargará de esto por nosotros, siempre y cuando no eludamos sus medidas de seguridad.
*   Si la desactualización implica un cambio de nombre, toda dependencia puede necesitar ser desactualizada o también [reconstruida](/index.php/Frequently_asked_questions_(Espa%C3%B1ol)#.C2.BFQu.C3.A9_pasa_si_ejecuto_una_actualizaci.C3.B3n_completa_del_sistema_y_hay_una_actualizaci.C3.B3n_de_una_biblioteca_compartida.2C_pero_no_para_las_aplicaciones_que_dependen_de_ella.3F "Frequently asked questions (Español)") .

## Contents

*   [1 Volver a una versión anterior del paquete](#Volver_a_una_versi.C3.B3n_anterior_del_paquete)
    *   [1.1 Usando la caché de pacman](#Usando_la_cach.C3.A9_de_pacman)
    *   [1.2 Desactualizando el kernel](#Desactualizando_el_kernel)
    *   [1.3 Archivo Arch Linux](#Archivo_Arch_Linux)
    *   [1.4 Reconstrucción del paquete](#Reconstrucci.C3.B3n_del_paquete)
    *   [1.5 Automatización](#Automatizaci.C3.B3n)
*   [2 Volver de [testing]](#Volver_de_.5Btesting.5D)

## Volver a una versión anterior del paquete

### Usando la caché de pacman

### Desactualizando el kernel

### Archivo Arch Linux

### Reconstrucción del paquete

### Automatización

## Volver de [testing]