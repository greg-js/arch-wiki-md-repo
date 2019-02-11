**Estado de la traducción**
Este artículo es una traducción de [Arch Linux AMIs for Amazon Web Services](/index.php/Arch_Linux_AMIs_for_Amazon_Web_Services "Arch Linux AMIs for Amazon Web Services"), revisada por última vez el **2019-02-09**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Arch_Linux_AMIs_for_Amazon_Web_Services&diff=0&oldid=557054) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Ejecutar AMIs públicas de Arch](#Ejecutar_AMIs_públicas_de_Arch)
    *   [1.1 Imágenes AMI de Uplink Labs](#Imágenes_AMI_de_Uplink_Labs)
    *   [1.2 Otras AMIs](#Otras_AMIs)
*   [2 Compilar AMIs de Arch](#Compilar_AMIs_de_Arch)

## Ejecutar AMIs públicas de Arch

### Imágenes AMI de Uplink Labs

Uplink Labs crea nuevas imágenes aproximadamente dos veces al mes. Las imágenes se compilan para varias regiones y cubren las siguientes configuraciones:

*   ebs hvm x86_64 lts
*   s3 hvm x86_64 lts
*   ebs hvm x86_64 stable
*   s3 hvm x86_64 stable

Los enlaces de las AMIs y más información se encuentra disponible en [https://www.uplinklabs.net/projects/arch-linux-on-ec2/](https://www.uplinklabs.net/projects/arch-linux-on-ec2/).

### Otras AMIs

Las AMIs públicas, en funcionamiento y verificadas de arch linux se encuentran a continuación

```
AMI          Store Build   Release     Kernel Last verified
ami-07be766e  EBS  64 bit  2011-04-15  3.0+   2012-01-14    
ami-19be7670  EBS  64 bit  2011-11-18  3.0+   2012-01-14    
ami-26e8144f  EBS  32 bit  2011-04-15  2.6    2012-01-14    
ami-38e81451  EBS  32 bit  2011-04-15  2.6    2012-01-14    

```

Estas AMIs se expiden con kernels de Arch linux que se arrancan mediante PV-GRUB.

(2012-01-14) Las AMIs de 64 bits fallaron sistemáticamente en el arranque en las instancias Micro en us-east-1a y us-east-1d. En us-east-1b y us-east-1c, las AMIs ocasionalmente no arrancan. Detenga e inicie la instancia para reasignarle una máquina aleatoria en estos casos.

Esto puede ser un problema asociado a que Amazon ejecuta diferentes versiones de Xen en diferentes máquinas / zonas de disponibilidad más antiguas.

## Compilar AMIs de Arch

[linux-ec2](https://aur.archlinux.org/packages/linux-ec2/) disponible en [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)") compila el kernel de Arch linux para AWS con los módulos Xen habilitados y el parche XSAVE aplicado.

La página web de Uplink Labs mencionada anteriormente también contiene un manual sobre el proceso de compilación.