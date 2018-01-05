Artículos relacionados

*   [AUR helpers](/index.php/AUR_helpers "AUR helpers")
*   [AurJson](/index.php/AurJson "AurJson")
*   [AUR Trusted User Guidelines](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines")
*   [PKGBUILD (Español)](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)")
*   [makepkg (Español)](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)")
*   [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")
*   [Official repositories (Español)](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)")
*   [Arch Build System (Español)](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")

Arch User Repository (AUR) es un repositorio promovido por los usuarios de la comunidad de Arch. Este contiene descripciones de los paquetes ([PKGBUILD](/index.php/PKGBUILD "PKGBUILD")) que le permiten compilar un paquete desde el código fuente con [makepkg](/index.php/Makepkg "Makepkg") y luego instalarlo a través de [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)"). AUR fue creado para organizar y compartir paquetes nuevos de la comunidad y ayudar a acelerar la inclusión de los paquetes más populares en el repositorio [[community]](#.5Bcommunity.5D). Este documento explica cómo los usuarios pueden acceder y utilizar AUR.

Un buen número de paquetes nuevos que entran en los repositorios oficiales tienen su origen en AUR. En AUR, los usuarios pueden aportar sus propias compilaciones de paquetes (PKGBUILD y los archivos relacionados). La comunidad de AUR tiene la posibilidad de votar a favor o en contra de los paquetes de AUR. Si un paquete llega a ser lo suficientemente popular —siempre que tenga una licencia compatible y la técnica de un buen empaquetado— puede ser introducido en el repositorio [community] (directamente accesible por [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") o [abs](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")).

## Contents

*   [1 Para empezar](#Para_empezar)
*   [2 Historia](#Historia)
*   [3 Buscar](#Buscar)
*   [4 Instalar paquetes](#Instalar_paquetes)
    *   [4.1 Prerrequisitos](#Prerrequisitos)
    *   [4.2 Adquirir archivos compilados](#Adquirir_archivos_compilados)
    *   [4.3 Compilar e instalar el paquete](#Compilar_e_instalar_el_paquete)
*   [5 Feedback](#Feedback)
*   [6 Compartir y mantener los paquetes](#Compartir_y_mantener_los_paquetes)
    *   [6.1 Enviar paquetes](#Enviar_paquetes)
        *   [6.1.1 Reglas de envio](#Reglas_de_envio)
        *   [6.1.2 Verificación](#Verificaci.C3.B3n)
        *   [6.1.3 Crear un paquete nuevo](#Crear_un_paquete_nuevo)
        *   [6.1.4 Subir paquetes](#Subir_paquetes)
    *   [6.2 Mantener los paquetes](#Mantener_los_paquetes)
    *   [6.3 Otras solicitudes](#Otras_solicitudes)
*   [7 [community]](#.5Bcommunity.5D)
*   [8 Repositorio Git](#Repositorio_Git)
*   [9 FAQ](#FAQ)
    *   [9.1 ¿Que es AUR?](#.C2.BFQue_es_AUR.3F)
    *   [9.2 ¿Qué tipo de paquetes se permiten en AUR?](#.C2.BFQu.C3.A9_tipo_de_paquetes_se_permiten_en_AUR.3F)
    *   [9.3 ¿Cómo puedo votar por los paquetes en AUR?](#.C2.BFC.C3.B3mo_puedo_votar_por_los_paquetes_en_AUR.3F)
    *   [9.4 ¿Qué es un TU?](#.C2.BFQu.C3.A9_es_un_TU.3F)
    *   [9.5 ¿Cuál es la diferencia entre Arch User Repository y [community]?](#.C2.BFCu.C3.A1l_es_la_diferencia_entre_Arch_User_Repository_y_.5Bcommunity.5D.3F)
    *   [9.6 ¿Cuántos votos necesita un PKGBUILD para llegar a [community]?](#.C2.BFCu.C3.A1ntos_votos_necesita_un_PKGBUILD_para_llegar_a_.5Bcommunity.5D.3F)
    *   [9.7 ¿Cómo hacer un PKGBUILD?](#.C2.BFC.C3.B3mo_hacer_un_PKGBUILD.3F)
    *   [9.8 No me funciona «pacman -S foo», aunque sé que el paquete «foo» está en [community]](#No_me_funciona_.C2.ABpacman_-S_foo.C2.BB.2C_aunque_s.C3.A9_que_el_paquete_.C2.ABfoo.C2.BB_est.C3.A1_en_.5Bcommunity.5D)
    *   [9.9 Un paquete en AUR está desactualizado, ¿qué hago?](#Un_paquete_en_AUR_est.C3.A1_desactualizado.2C_.C2.BFqu.C3.A9_hago.3F)
    *   [9.10 Quiero enviar un PKGBUILD ¿podría alguien comprobar antes si tiene errores?](#Quiero_enviar_un_PKGBUILD_.C2.BFpodr.C3.ADa_alguien_comprobar_antes_si_tiene_errores.3F)
    *   [9.11 Foo, que está en AUR, no me compila con makepkg, ¿qué hago?](#Foo.2C_que_est.C3.A1_en_AUR.2C_no_me_compila_con_makepkg.2C_.C2.BFqu.C3.A9_hago.3F)
    *   [9.12 ¿Cómo puedo acelerar los repetidos procesos de compilación?](#.C2.BFC.C3.B3mo_puedo_acelerar_los_repetidos_procesos_de_compilaci.C3.B3n.3F)
    *   [9.13 ¿Cómo accedo a paquetes de Unsupported?](#.C2.BFC.C3.B3mo_accedo_a_paquetes_de_Unsupported.3F)
    *   [9.14 ¿Puedo subir archivos a AUR sin usar la interfaz web?](#.C2.BFPuedo_subir_archivos_a_AUR_sin_usar_la_interfaz_web.3F)

## Para empezar

Los usuarios pueden buscar y descargar PKGBUILD desde la [Interfaz Web de AUR](https://aur.archlinux.org). Estos PKGBUILD se pueden compilar en paquetes instalables usando [makepkg](/index.php/Makepkg "Makepkg"), y luego instalarlos con pacman.

*   Asegúrese de que los paquetes del grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) están [instalados](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)").
*   Léase el resto de este artículo para obtener más información que funciona como un breve tutorial sobre la instalación de los paquetes de AUR.
*   Visite la [Interfaz Web de AUR](https://aur.archlinux.org) para obtener información sobre actualizaciones y otros eventos. Allí también encontrará estadísticas y una lista actualizada de los nuevos paquetes disponibles presentes en AUR.
*   Léase [#FAQ](#FAQ) para obtener respuestas a las preguntas más comunes.
*   Es posible mejorar la optimización ajustando `/etc/makepkg.conf` para el procesador antes de crear paquetes desde AUR. Se puede obtener una mejora significativa en los tiempos de compilación en sistemas con procesadores multi-core ajustando la variable MAKEFLAGS. También se pueden habilitar optimizaciones para hardware específico en GCC a través de la variable CFLAGS. Véase [makepkg.conf](/index.php/Makepkg.conf "Makepkg.conf") para obtener más información.

## Historia

Los siguientes instrumentos se listan con fines ilustrativos solamente. Desde entonces, han sido sustituidos por AUR y ya no están disponibles.

Al principio, existía `ftp://ftp.archlinux.org/incoming`, y se contribuía únicamente subiendo el PKGBUILD, los archivos adicionales necesarios y el mismo paquete compilado al servidor. El paquete y los archivos asociados se mantenían allí hasta que un [Package Maintainer](/index.php/Package_Maintainer "Package Maintainer") veía el programa y lo adoptaba.

Posteriormente, surgieron los Trusted User Repositories (*«repositorios de usuarios de confianza»*). A algunas personas de la comunidad se les permitía alojar sus propios repositorios para que cualquiera los utilizase. AUR se amplió sobre esta base, con el objetivo de hacerlo más flexible y usable. De hecho, a los responsables de AUR todavía se les conoce como TUs (Trusted Users -*«Usuarios de Confianza»*-).

## Buscar

La interfaz web de AUR puede ser encontrada [aquí](https://aur.archlinux.org/), y una interfaz para el acceso a AUR mediante un script (por ejemplo) puede ser encontrada [aquí](https://aur.archlinux.org/rpc.php).

Las consultas de búsqueda de los nombre y descripciones de los paquetes utilizan un método similar al de MySQL. Esto permite el uso de criterios de búsquedas más flexibles (por ejemplo, pruebe a burcar por «tool%like%grep», en lugar de «tool like grep»). Si tiene que buscar una descripción que contiene «%», use el carácter de escape «\%».

## Instalar paquetes

La instalación de paquetes desde AUR es un proceso relativamente simple. En esencia consiste en:

1.  Adquirir los archivos para la construcción, incluyendo el [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") y posiblemente otros archivos necesarios.
2.  Verificar que el [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") y los archivos acompañantes no son maliciosos.
3.  Ejecute `makepkg -si` en el directorio donde ha puesto los archivos. Este comando descarga la fuente, resuelve depedencias con [pacman](/index.php/Pacman "Pacman"), compila, empaca e instala el paquete.

Los [AUR helpers](/index.php/AUR_helpers "AUR helpers") añaden un acceso transparente para AUR. Los mismos varían en sus características, pero pueden facilitar la búsqueda, descarga, compilación e instalación de los PKGBUILD que se encuentran en AUR. Todos estos scripts se pueden encontrar en AUR.

**Advertencia:** Nunca habrá un mecanismo *oficial* para la instalación del material precompilado de AUR. Por tanto, **todos los usuarios deben estar familiarizados con el proceso de compilación.**

Lo que sigue es un ejemplo detallado de la instalación de un paquete llamado «foo».

### Prerrequisitos

Primero, asegúrese de que las herramientas necesarias estén instaladas. El grupo de paquetes [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) debe ser suficiente; incluye [make](https://www.archlinux.org/packages/?name=make) y otras herramientas necesarias para compilar desde el código fuente.

**Nota:** Los paquetes disponibles en AUR asumen que tiene [instalado](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalaci.C3.B3n_de_paquetes "Help:Reading (Español)") el grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), por lo que los paquetes de AUR no listan los elementos de este grupo como dependencias, incluso si el paquete no se puede compilar sin ellos. Por tanto, asegúrese que este grupo está instalado para prevenir que arroje errores sobre fallo al compilar.

```
# pacman -S base-devel

```

A continuación, elija un directorio de compilación apropiado. Un directorio de compilación es simplemente una carpeta en la que se construirá el paquete o «se compilará», y puede ser cualquier carpeta. En el ejemplo que se sigue, la carpeta `~/builds` será el directorio de compilación.

### Adquirir archivos compilados

Localice el paquete en AUR. Esto se realiza utilizando la función de búsqueda (esto es, el recuadro de texto de la parte superior de la [página principal de AUR](https://aur.archlinux.org/)). Al pulsar sobre el nombre de la aplicación en la lista de búsqueda, nos llevará a una página de información sobre el paquete. Lea la descripción para confirmar que este es el paquete deseado, observe si el paquete ha sido actualizado y lea los comentarios.

Existen diferentes métodos para adquirir los archivos de construcción:

*   Clone el repositorio [git](/index.php/Git "Git") que tiene el nombre "Git Clone URL" en los detalles del paquete:

```
$ git clone https://aur.archlinux.org/*package_name*.git

```

	Una ventaja de este método es la facilidad de actualizar el repositorio con el comando `git pull`.

*   Descargue los archivos necesarios de compilación. Desde la página de información del paquete, descargue los archivos de compilación pulsando el «tarball» que aparece en el lado izquierdo, cerca del final de los detalles del paquete. Este archivo debe ser guardado en el directorio de compilación o una copia del archivo en dicho directorio después de la descarga.

```
$ tar -xvf *package_name*.tar.gz

```

*   También se puede descargar el tarball desde la terminal (para luego extraerlo):

```
$ curl -L -O https://aur.archlinux.org/cgit/aur.git/snapshot/*package_name*.tar.gz

```

### Compilar e instalar el paquete

Si ha usado el método *git clone* solo es necesario cambiar a ese directorio `cd *package_name*`, y continue con la construcción de los archivos.

Extraiga el tarball. Para ello, cambie el archivo a la carpeta de compilación, si no está ya allí y, una vez en dicho directorio, extraiga los archivos de compilación:

```
$ cd ~/builds
$ tar -xvzf foo.tar.gz

```

Esto debería crear una nueva carpeta llamada «foo» en el directorio de compilación.

**Advertencia:** **Revise cuidadosamente todos los archivos.** Ejecute la orden `cd` para desplazarse a la carpeta (foo) recién creada y revise con cuidado el `PKGBUILD` y cualquier archivo `.install` para advertir órdenes maliciosas. Los `PKGBUILD` son scripts de bash que contienen funciones para ser ejecutadas por `makepkg`: estas funciones pueden contener *cualquier* orden válida o con la sintaxis que interpreta Bash, por lo que es totalmente posible que un `PKGBUILD` pueda contener órdenes peligrosas introducidas por malicia o ignorancia del autor. Use `makepkg` en un entorno fakeroot (y no lo ejecute nunca como root), lo cual le da un cierto nivel de protección, pero nunca se debe confiar del todo con ello. En caso de duda, no compile el paquete y consulte en los foros o listas de correo.

```
$ cd foo
$ nano PKGBUILD
$ nano foo.install

```

Construya el paquete. Después de confirmar manualmente la integridad de los archivos, ejecute [makepkg](/index.php/Makepkg "Makepkg") como un usuario normal en el directorio de compilación.

```
$ makepkg -si

```

*   `-s`/`--syncdeps` utilizará [sudo](/index.php/Sudo "Sudo") para instalar eventuales dependencias. Si no se desea utilizar sudo, se deberán instalar manualmente las dependencias de antemano y posteriormente ejecutar lar orden anterior, omitiendo la opción `-s`.
*   `-i`/`--install` installa el paquete si fue creado exitosamente.

Como una alternativa puede instalar el paquete con [pacman](/index.php/Pacman "Pacman"). Un tarball bien creado debería mostrar un nombre siguiendo este esquema:

```
<*application name*>-<*application version number*>-<*package revision number*>-<*architecture*>.pkg.tar.xz

```

Este paquete puede ser instalado usando la orden «upgrade» de pacman:

```
# pacman -U foo-0.1-1-i686.pkg.tar.xz   

```

Estos paquetes instalados manualmente se denominan paquetes foráneos (*«foreign packages»*) —es decir, aquellos paquetes que no se han originado desde cualquier repositorio conocido por pacman—. Para listar todos los paquetes foráneos, escriba:

```
$ pacman -Qm 

```

**Nota:** El ejemplo anterior es solo un breve resumen del proceso de compilación de un paquete. Es recomendable una visita a los artículos sobre [makepkg](/index.php/Makepkg "Makepkg") y [ABS](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)"). Estos artículos proporcionan más detalles y son muy útiles, sobre todo para los usuarios primerizos.

## Feedback

La [Interfaz Web de AUR](https://aur.archlinux.org) facilita hacer comentarios que permite a los usuarios proporcionar sugerencias y feedback para contribuir a mejorar el PKGBUILD. Evite pegar parches o PKGBUILD en la sección de comentarios: se vuelven rápidamente obsoletos y acaban ocupando innecesariamente mucho espacio. En su lugar, envie los archivos al mantenedor, o incluso utilice un [pastebin](/index.php/Pastebin_Clients "Pastebin Clients").

Una de las actividades más fáciles para **todos** los usuarios de Arch es navegar por AUR y **votar** por sus paquetes favoritos utilizando la interfaz web. Todos los paquetes son elegibles para ser adoptados por un TU para su inclusión en [community], y el recuento de votos es uno de los factores considerados en este proceso, ¡por lo que votar es un interés de todos!

## Compartir y mantener los paquetes

El usuario juega un papel esencial en AUR, por lo que no puede desplegar su potencial sin el apoyo, la participación y la contribución de la más amplia comunidad de usuarios. El ciclo de vida de un paquete de AUR comienza y termina con el usuario y requiere que el usuario contribuya de diversas maneras.

Los usuarios pueden **compartir** los PKGBUILD a través de Arch User Repository. Este no contiene los paquetes binarios, pero permite a los usuarios subir sus PKGBUILD que pueden ser descargados por otros. Estos PKGBUILD no tienen ningún apoyo oficial y, por tanto, no se han investigado a fondo, por lo que se deben utilizar con cautela bajo el propio riesgo del usuario.

### Enviar paquetes

Después de iniciar sesión en la interfaz web de AUR, un usuario puede [enviar](https://aur.archlinux.org/pkgsubmit.php) un archivo *.tar comprimido con gzip (`.tar.gz`) de un directorio que contiene archivos para compilar un paquete. El directorio, dentro del tarball, debe contener un [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), cualesquiera archivos `.install`, parches, etc., (**en ningún caso** archivos binarios). Ejemplos de cómo debe ser la estructura de dicho directorio pueden ser encontrados en los directorios incluidos en `/var/abs`, si [Arch Build System](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") se ha instalado.

El tarball se puede crear con la siguiente orden:

```
$ makepkg --source 

```

Tenga en cuenta que se trata de un archivo .tar comprimido con gzip, de modo que, suponiendo que está subiendo un paquete llamado *libfoo*, la creación del archivo comprimido debería dar como resultado algo similar a esto:

 `$ tar tf libfoo-0.1-1.src.tar.gz` 
```
libfoo/
libfoo/PKGBUILD
libfoo/libfoo.install
```

#### Reglas de envio

Al enviar un paquete, observe las siguientes reglas:

*   Marque la casilla [package database](https://www.archlinux.org/packages/) para el paquete. Si existe, **no** envie el paquete. Si el paquete actual está roto o falta alguna función incluida, es preferible enviar un [informe de errores](https://bugs.archlinux.org/).
*   Compruebe AUR para el paquete. Si es mantenido actualmente, los cambios se pueden enviar en un comentario para la atención del mantenedor. Si está desatendido, el paquete puede ser adoptado y actualizado, según sea necesario. No cree paquetes duplicados.
*   Verifique cuidadosamente que lo que se está cargando es correcto. Todos los participantes deben leer y seguir las [normas de empaquetado de Arch](/index.php/Arch_packaging_standards "Arch packaging standards") al escribir PKGBUILD. Esto es esencial para el buen funcionamiento y el éxito general de AUR. Recuerde que no va a ganar ningún crédito o respeto de sus compañeros por perder el tiempo con un PKGBUILD malo.
*   Los paquetes que contengan binarios o que estén mal escritos pueden ser borrados sin previo aviso.
*   Si no está seguro sobre el paquete (o el proceso de compilación/envío) de ninguna manera, presente el PKGBUILD a la [Lista de Correo de AUR](https://mailman.archlinux.org/mailman/listinfo/) o en las [Tablas de AUR](https://bbs.archlinux.org/viewforum.php?id=4) del fórum público para su revisión antes de añadirlo a AUR.
*   Asegúrese de que el paquete es útil. ¿Alguien más quiere utilizar este paquete? ¿Es sumamente especializado? Si no hay más que unas cuantas personas que encontrarán este paquete útil, no es apropiado para su presentación.
*   Los repositorios AUR y oficiales están diseñados para paquetes que instalan generalmente software y contenido relacionado con el software, incluyendo uno o más de los siguientes: archivo(s) ejecutable, archivo(s) de configuración, documentación en línea o fuera de línea para un software, en particular, o para la distribución Arch Linux, en general; archivos multimedia destinados a ser utilizados directamente por el software.
*   Obtenga un poco de experiencia antes de enviar los paquetes. Compile algunos paquetes para conocer el proceso y luego enviarlos.
*   Si se presenta un `package.tar.gz` con un archivo llamado «`package`» obtendrá el siguiente error: «Could not change to directory `/home/aur/unsupported/package/package`». Para resolver este problema, cambie el nombre del archivo llamado «`package`» con otro nombre, por ejemplo, «`package.rc`». Cuando se instale en el directorio `pkg` puede cambiar su nombre de nuevo a «`package`». Léase también [Arch packaging standards#Submitting packages to the AUR](/index.php/Arch_packaging_standards#Submitting_packages_to_the_AUR "Arch packaging standards").

#### Verificación

Para tener acceso de modificación en AUR se necesita tener [llaves de SSH](/index.php/SSH_keys_(Espa%C3%B1ol) "SSH keys (Español)"). El contenido de la llave pública debe ser copiado en la pagina del perfil en la sección *My Account*, y la llave privada correspondiente debe ser configurada para el servidor `aur.archlinux.org`. Por ejemplo:

 `~/.ssh/config` 
```
Host aur.archlinux.org
  IdentityFile ~/.ssh/aur
  User aur
```

En el escenario ideal se debe crear un [nuevo par de llaves](/index.php/SSH_keys_(Espa%C3%B1ol)#Generando_las_llaves_SSH "SSH keys (Español)") y no usar uno existente, así se pueden revocar selectiva mente en caso de que algo ocurra:

```
$ ssh-keygen -f ~/.ssh/aur

```

**Tip:** Se pueden agregar múltiples llaves en su perfil separandolas con una nueva linea.

#### Crear un paquete nuevo

Para crear un repositorio Git vació para un paquete, simplemente `git clone` el repositorio remoto con el nombre correspondiente. Si el paquete no existe en AUR, la siguiente advertencia será vista:

 `$ git clone ssh://aur@aur.archlinux.org/*package_name*.git` 
```
Cloning into '*package_name*'...
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
```

**Nota:** Cuando un paquete es borrado de AUR, el repositorio git no es borrado, asi que al clonar el repositorio puede que no este vació si alguien quiere crear un paquete con el mismo nombre.

Si hay un repositorio git existente, simplemente se crea un *remote* para el repositorio git de AUR y luego *fetch* en el repositorio:

```
$ git remote add *nombre_remoto* ssh://aur@aur.archlinux.org/*nombre_paquete*.git
$ git fetch *nombre_remoto*

```

Donde `*nombre_remoto*` es el nombre del *remote* a crear (*v.g.,* "origen"). Vea [Git#Using remotes](/index.php/Git#Using_remotes "Git") para mayor información.

El paquete aparecerá en AUR después del primer *push*. Desde ese momento se pueden agregar archivos con codigo fuente a la copia local del repositorio git. Vea [#Subir paquetes](#Subir_paquetes).

**Advertencia:** Sus AUR *commits* tendran como autor su usuario y correo electronico configurado en git, es muy dificil cambiar un *commit* despueś que ha sido subida (vea [FS#45425](https://bugs.archlinux.org/task/45425)). Si desea enviar paquetes con un autor/email diferente lo puede hacer con el comando `git config user.name [...]` y `git config user.email [...]`. Revise sus *commits* y documentos antes de subirlos!

#### Subir paquetes

El procedimiento para subir paquetes to AUR es el mismo para paquetes nuevos o para actualizaciones. Se necesita como mínimo un [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") y un [.SRCINFO](/index.php/.SRCINFO ".SRCINFO") en el directorio de trabajo para subir (*push*) su paquete a AUR.

**Nota:** se necesita generar el archivo `.SRCINFO` cada vez que se cambie la metainformación del `PKGBUILD`, por ejemplo al modificar [pkgver()](/index.php/PKGBUILD_(Espa%C3%B1ol)#Variables "PKGBUILD (Español)") en actualizaciones. De otra manera AUR web no va a mostrar las versiones actualizadas .

Para subir, añada el `PKGBUILD`, `.SRCINFO`, y cualquier otro archivo necesario (como arachivos `.install` o fuentes locales `.patch`) con `git add`, suba a su arbol local con un mensaje descriptivo `git commit`, y finalmente suba sus cambios a AUR con `git push`.

Ejemplo concreto:

```
$ makepkg --printsrcinfo > .SRCINFO
$ git add PKGBUILD .SRCINFO
$ git commit -m "*useful commit message*"
$ git push

```

**Tip:**

*   Si inicialmente se ha olvidado el archivo `.SRCINFO` y lo ha agregado en un *commit* después, AUR va a rechazar sus subidas porque el archivo `.SRCINFO` debe existir en *cada* subida (*push*). Para solucionar este problema puede usar el comando [git rebase](https://git-scm.com/docs/git-rebase) con la opción `--root` o el comando [git filter-branch](https://git-scm.com/docs/git-filter-branch) con la opción `--tree-filter`.
*   Para prevenir archivos sin rastrear en las subidas, y para mantener el directorio de trabajo tan limpio como sea posible, excluya todos los archivos no deseados con `.gitignore` y fuerce agregar manualmente cada archivo. Vea [dotfiles#Using gitignore](/index.php/Dotfiles#Using_gitignore "Dotfiles").

### Mantener los paquetes

*   Si se mantiene un paquete y desea actualizar el PKGBUILD para el mismo, basta con reenviarlo.
*   Compruebe si hay feedback y comentarios de otros usuarios y trate de incorporar las mejoras que le sugieren, ¡considere que es un proceso de aprendizaje!
*   Por favor, no presente un paquete, para luego olvidarse de él. El trabajo del mantenedor es mantener el paquete, buscando las actualizaciones y las mejoras del PKGBUILD.
*   Si no desea seguir manteniendo el paquete, por alguna razón, etiquete el paquete como `disown` a través de la interfaz web de AUR y/o envie un mensaje a la lista de correos de AUR.

### Otras solicitudes

*   La peticiones de abandono y de eliminación deben ir a la lista de correos general de aur, para que puedan tomar una decisión los TU y los demás usuarios.
*   **Incluya el nombre del paquete y la dirección URL a la página de AUR**, preferiblemente con una nota al pie [1].
*   Las solicitudes de abandono se concederán dos semanas después de que el mantenedor actual haya sido contactado por correo electrónico y no se haya obtenido respuesta.
*   **El renombre de paquetes no es ahora implementado**, los usuarios tienen ahora que reenviar el paquete con un nombre nuevo y solicitar el renombre de los comentarios de la versión antigua y de los votos a la lista de correos.
*   Las peticiones de eliminación requieren la siguiente información:
    *   Nombre del paquete y la dirección URL a la página AUR
    *   Razón para su eliminación, al menos una breve nota
        **Aviso:** Los comentarios de un paquete, no son razón suficiente para señalar un paquete para su eliminación. Porque tan pronto como TU toma medidas, el único lugar donde se puede obtener esa información es la lista de correo general de aur.
    *   Incluir detalles de información, como cuando un paquete es proporcionado por otro paquete, si es el mismo mantenedor, si se ha cambiado el nombre y el propietario original está de acuerdo, etc.

Las solicitudes de abandono pueden ser rechazadas, en cuyo caso es probable que se avise del abandono del paquete para referencias futuras del empaquetador.

## [community]

El repositorio [community], mantenido por los [Trusted Users](/index.php/Trusted_Users "Trusted Users"), contiene los paquetes más populares de AUR. Está habilitado de forma predeterminada en `/etc/pacman.conf`. Si [community] se ha deshabilitado o eliminado, se puede activar descomentándolo, o añadiendo estas dos líneas, respectivamente:

 `/etc/pacman.conf` 
```
...
[community]
Include = /etc/pacman.d/mirrorlist
...
```

Este depósito, a diferencia de AUR, contiene paquetes binarios que se pueden instalar directamente con [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") y a los archivos de compilación también se puede acceder con [ABS.](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") Algunos de estos paquetes pueden eventualmente pasar a los repositorios [core] o [extra], cuando los desarrolladores los consideran cruciales para la distribución.

Los usuarios también pueden acceder a los archivos de compilación de [community] editando `/etc/abs.conf` y habilitando al repositorio [community] en la matriz `REPOS`.

## Repositorio Git

Un repositorio git de AUR es mantenido por Thomas Dziedzic proporcionando paquete históricos, entre otras cosas. Se actualiza, al menos, una vez al día. Para clonar el repositorio (varios cientos de MB):

```
$ git clone git://pkgbuild.com/aur-mirror.git

```

Más información: [Interfaz Web](http://pkgbuild.com/git/aur-mirror.git/), [readme](http://pkgbuild.com/~td123/readme), [hilo del fórum](https://bbs.archlinux.org/viewtopic.php?id=113099).

## FAQ

### ¿Que es AUR?

AUR (Arch User Repository) es el lugar donde la comunidad de Arch Linux puede subir los [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") de las aplicaciones, bibliotecas, etc., y compartirlos con el resto de la comunidad. Los demás usuarios pueden votar para que sus favoritos entren en el repositorio [community] de modo que puedan ser instalados en Arch Linux en formato binario.

### ¿Qué tipo de paquetes se permiten en AUR?

Los paquetes en AUR no son más que «scripts de compilación», es decir, instrucciones para construir los binarios que pueden ser manejados por pacman. Para la mayor parte de los casos, no hay limitaciones, siempre y cuando se ajusten a las directrices de la utilidad antes mencionada y a los términos de licencia del contenido. En otros casos, cuando se menciona que «no se puede vincular» a las descargas, como cuando los contenidos no son redistribuibles, solo se podrá hacer uso del mismo nombre del archivo como la fuente. Esto significa y requiere que los usuarios deben tener ya la fuente en el directorio de compilación antes de iniciar el proceso de construcción del paquete. En caso de duda, pregunte.

### ¿Cómo puedo votar por los paquetes en AUR?

Inscríbase en el [sitio web de AUR](https://aur.archlinux.org/) para tener acceso a la opción "Vote for this package" («Vote por este paquete») mientras explora los paquetes.

### ¿Qué es un TU?

Un [TU (Trusted User)](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines") es una persona encargada de supervisar el repositorio AUR y el repositorio [community]. Ellos son los que colocan los paquetes más votados en el repositorio [community], marcan los PKGBUILDs como seguros y mantienen AUR.

### ¿Cuál es la diferencia entre Arch User Repository y [community]?

Arch User Repository contiene todos los PKGBUILD que los usuarios envían; para instalarlos tiene que construirlos manualmente con [makepkg](/index.php/Makepkg "Makepkg"). Cuando un PKGBUILD obtiene suficientes votos, pasa al repositorio [community], donde los TUs lo mantienen y puede instalarse como binario directamente con [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").

### ¿Cuántos votos necesita un PKGBUILD para llegar a [community]?

Por lo general, son necesarios, al menos, 10 votos para que algo se mueva al repositorio [community]. Sin embargo, si un TU quiere apoyar un paquete, se suele pasar dicho paquete al repositorio.

### ¿Cómo hacer un PKGBUILD?

Lo mejor es mirar [Creating packages](/index.php/Creating_packages "Creating packages"). Recuerde mirar en AUR antes de crear el PKGBUILD para no duplicar los esfuerzos.

### No me funciona «pacman -S foo», aunque sé que el paquete «foo» está en [community]

Probablemente no ha activado el repositorio [community] en el archivo `/etc/pacman.conf`. Basta con descomentar las líneas relevantes. Si el repositorio [community] está habilitado en `/etc/pacman.conf`, pruebe ejecutando primero `pacman -S -y` para sincronizar el pkgcache, antes de intentar de nuevo instalar el paquete.

### Un paquete en AUR está desactualizado, ¿qué hago?

Puede marcarlo como obsoleto. Si no se actualiza en un periodo de tiempo razonable, lo mejor es avisar a su mantenedor por email. Si el responsable no responde, puede comunicarlo a la lista de correo general de AUR, para que un TU (usuario de confianza) declare huérfano al PKGBUILD y pueda adoptarlo si desea mantenerlo él mismo. Cuando se trate de un paquete que lleva desactualizado más de 3 meses y, en general, no se actualiza desde hace mucho tiempo, por favor agregue esto en su solicitud de orfandad.

### Quiero enviar un PKGBUILD ¿podría alguien comprobar antes si tiene errores?

Si quisiera recibir comentarios a tu PKGBUILD, envíelo a la lista de correo de AUR para que los TU y los otros miembros de AUR puedan orientarle para mejorarlo. Otro lugar donde puede encontrar ayuda es el [canal IRC](/index.php/ArchChannel "ArchChannel"), #archlinux en irc.freenode.net. También puede usar [namcap](/index.php/Namcap "Namcap") para depurar su PKGUILD y el pkg.tar.gz.

### Foo, que está en AUR, no me compila con makepkg, ¿qué hago?

Probablemente está pasando por alto alguna cosa.

1.  Ejecute `pacman -Syyu` antes de compilar nada con `makepkg` dado que el problema puede ser que el sistema no está al día.
2.  Asegúrese de que tiene instalados tanto los grupos «base» como «base-devel».
3.  Pruebe usando la opción «`-s`» con `makepkg` para comprobar e instalar todas las dependencias necesarias antes de comenzar el proceso de compilación.

Asegúrese de leer primero el PKGBUILD y los comentarios en la página de AUR del paquete en cuestión. La razón puede no ser trivial después de todo. La personalización de CFLAGS, LDFLAGS y MAKEFLAGS puede causar fallos. También es posible que el PKGBUILD se rompe para todos. Si no puede resolverlo por su cuenta, simplemente informe al mantenedor, por ejemplo, mediante la publicación de los errores que está recibiendo en los comentarios de la página de AUR.

### ¿Cómo puedo acelerar los repetidos procesos de compilación?

Si suele compilar del código que utiliza gcc —como por ejemplo, un paquete git o SVN—, puede encontrar útil utilizar [ccache](/index.php/Ccache "Ccache"), abreviatura de «compiler cache».

### ¿Cómo accedo a paquetes de Unsupported?

Véase [#Installing packages](#Installing_packages)

### ¿Puedo subir archivos a AUR sin usar la interfaz web?

Puede usar [burp](https://www.archlinux.org/packages/?name=burp), *aurploader* ([python3-aur](https://aur.archlinux.org/packages/python3-aur/)) o [aurup](https://aur.archlinux.org/packages/aurup/) —se trata de programas de línea de órdenes—.