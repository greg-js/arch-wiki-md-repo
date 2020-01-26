**Estado de la traducción**
Este artículo es una traducción de [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"), revisada por última vez el **2018-09-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Arch_User_Repository&diff=0&oldid=544908) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [makepkg (Español)](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)")
*   [pacman (Español)](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)")
*   [PKGBUILD (Español)](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)")
*   [.SRCINFO](/index.php/.SRCINFO ".SRCINFO")
*   [Aurweb RPC interface](/index.php/Aurweb_RPC_interface "Aurweb RPC interface")
*   [AUR Trusted User Guidelines (Español)](/index.php/AUR_Trusted_User_Guidelines_(Espa%C3%B1ol) "AUR Trusted User Guidelines (Español)")
*   [Official repositories (Español)](/index.php/Official_repositories_(Espa%C3%B1ol) "Official repositories (Español)")
*   [Arch Build System (Español)](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")
*   [Creating packages (Español)](/index.php/Creating_packages_(Espa%C3%B1ol) "Creating packages (Español)")
*   [AUR helpers (Español)](/index.php/AUR_helpers_(Espa%C3%B1ol) "AUR helpers (Español)")

Arch User Repository (AUR) es un repositorio promovido por los usuarios de la comunidad de Arch. Este contiene descripciones de los paquetes ([PKGBUILD](/index.php/PKGBUILD "PKGBUILD")) que le permiten compilar un paquete desde el código fuente con [makepkg](/index.php/Makepkg "Makepkg") y luego instalarlo a través de [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)"). AUR fue creado para organizar y compartir paquetes nuevos de la comunidad y ayudar a acelerar la inclusión de los paquetes más populares en el [repositorio community](/index.php/Repositorio_community "Repositorio community"). Este documento explica cómo los usuarios pueden acceder y utilizar AUR.

Un buen número de paquetes nuevos que entran en los repositorios oficiales tienen su origen en AUR. En AUR, los usuarios pueden aportar sus propias compilaciones de paquetes (PKGBUILD y los archivos relacionados). La comunidad de AUR tiene la posibilidad de votar a favor o en contra de los paquetes de AUR. Si un paquete llega a ser lo suficientemente popular —siempre que tenga una licencia compatible y la técnica de un buen empaquetado— puede ser introducido en el repositorio *community* (directamente accesible por [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)") o [abs](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)")).

**Advertencia:** Los paquetes contenidos en AUR son producidos por el usuario. Cualquier uso de los archivos proporcionados lo es bajo el propio riesgo del usuario.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Para empezar](#Para_empezar)
*   [2 Historia](#Historia)
    *   [2.1 Repositorios Git para paquetes AUR3](#Repositorios_Git_para_paquetes_AUR3)
*   [3 Instalar paquetes](#Instalar_paquetes)
    *   [3.1 Requisitos previos](#Requisitos_previos)
    *   [3.2 Obtener los archivos de compilación](#Obtener_los_archivos_de_compilación)
    *   [3.3 Compilar e instalar el paquete](#Compilar_e_instalar_el_paquete)
*   [4 Feedback](#Feedback)
*   [5 Compartir y mantener los paquetes](#Compartir_y_mantener_los_paquetes)
    *   [5.1 Enviar paquetes](#Enviar_paquetes)
        *   [5.1.1 Reglas de envío](#Reglas_de_envío)
        *   [5.1.2 Verificación](#Verificación)
        *   [5.1.3 Crear un paquete nuevo](#Crear_un_paquete_nuevo)
        *   [5.1.4 Subir paquetes](#Subir_paquetes)
    *   [5.2 Mantener los paquetes](#Mantener_los_paquetes)
    *   [5.3 Otras solicitudes](#Otras_solicitudes)
*   [6 Traducir la interfaz web](#Traducir_la_interfaz_web)
*   [7 Sintaxis de comentario](#Sintaxis_de_comentario)
*   [8 FAQ](#FAQ)
    *   [8.1 ¿Que es AUR?](#¿Que_es_AUR?)
    *   [8.2 ¿Qué tipo de paquetes se permiten en AUR?](#¿Qué_tipo_de_paquetes_se_permiten_en_AUR?)
    *   [8.3 ¿Cómo puedo votar por los paquetes en AUR?](#¿Cómo_puedo_votar_por_los_paquetes_en_AUR?)
    *   [8.4 ¿Qué es un usuario de confianza / Trusted Users (TU)?](#¿Qué_es_un_usuario_de_confianza_/_Trusted_Users_(TU)?)
    *   [8.5 ¿Cuál es la diferencia entre Arch User Repository y el repositorio community?](#¿Cuál_es_la_diferencia_entre_Arch_User_Repository_y_el_repositorio_community?)
    *   [8.6 Un paquete en AUR está desactualizado, ¿qué hago?](#Un_paquete_en_AUR_está_desactualizado,_¿qué_hago?)
    *   [8.7 Foo, que está en AUR, no me compila con makepkg, ¿qué hago?](#Foo,_que_está_en_AUR,_no_me_compila_con_makepkg,_¿qué_hago?)
    *   [8.8 ERROR: One or more PGP signatures could not be verified!; ¿qué debería hacer?](#ERROR:_One_or_more_PGP_signatures_could_not_be_verified!;_¿qué_debería_hacer?)
    *   [8.9 ¿Cómo hacer un PKGBUILD?](#¿Cómo_hacer_un_PKGBUILD?)
    *   [8.10 Quiero enviar un PKGBUILD ¿podría alguien comprobar antes si tiene errores?](#Quiero_enviar_un_PKGBUILD_¿podría_alguien_comprobar_antes_si_tiene_errores?)
    *   [8.11 ¿Qué hacer para que un PKGBUILD pase al repositorio community?](#¿Qué_hacer_para_que_un_PKGBUILD_pase_al_repositorio_community?)
    *   [8.12 ¿Cómo puedo acelerar los repetidos procesos de compilación?](#¿Cómo_puedo_acelerar_los_repetidos_procesos_de_compilación?)
    *   [8.13 ¿Cuál es la diferencia entre los paquetes foo y foo-git?](#¿Cuál_es_la_diferencia_entre_los_paquetes_foo_y_foo-git?)
    *   [8.14 ¿Por qué foo desapareció de AUR?](#¿Por_qué_foo_desapareció_de_AUR?)
    *   [8.15 ¿Cómo puedo averiguar si alguno de los paquetes instalados desapareció de AUR?](#¿Cómo_puedo_averiguar_si_alguno_de_los_paquetes_instalados_desapareció_de_AUR?)
    *   [8.16 ¿Cómo puedo obtener una lista de todos los paquetes de AUR?](#¿Cómo_puedo_obtener_una_lista_de_todos_los_paquetes_de_AUR?)
*   [9 Véase también](#Véase_también)

## Para empezar

Los usuarios pueden buscar y descargar PKGBUILD desde la [interfaz Web de AUR](https://aur.archlinux.org). Estos PKGBUILD se pueden compilar en paquetes instalables usando [makepkg](/index.php/Makepkg "Makepkg"), y luego instalarlos con pacman.

*   Asegúrese de que los paquetes del grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) están [instalados](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)").
*   Léase [#FAQ](#FAQ) para obtener respuestas a las preguntas más comunes.
*   Es posible mejorar la optimización ajustando `/etc/makepkg.conf` para el procesador (del equipo) antes de crear paquetes desde AUR. Se puede obtener una mejora significativa en los tiempos de compilación en sistemas con procesadores multicore ajustando la variable MAKEFLAGS. También se pueden habilitar optimizaciones para hardware específico en GCC a través de la variable CFLAGS. Véase [makepkg](/index.php/Makepkg "Makepkg") para obtener más información.

También es posible interactuar con AUR a través de SSH: escriba `ssh aur@aur.archlinux.org help` para obtener una lista de las órdenes disponibles.

## Historia

En un principio, existía `ftp://ftp.archlinux.org/incoming`, y se contribuía únicamente subiendo el PKGBUILD, los archivos adicionales necesarios y el mismo paquete compilado al servidor. El paquete y los archivos asociados se mantenían allí hasta que un [mantenedor de paquetes](/index.php/Package_Maintainer "Package Maintainer") veía el programa y lo adoptaba.

Posteriormente, surgieron los Trusted User Repositories (*«repositorios de usuarios de confianza»*). A algunas personas de la comunidad se les permitía alojar sus propios repositorios para que cualquiera los utilizase. AUR se amplió sobre esta base, con el objetivo de hacerlo más flexible y manejable. De hecho, a los responsables de AUR todavía se les conoce como TU (Trusted Users -*«usuarios de confianza»*-).

Entre 2015-06-08 y 2015-08-08, AUR hizo la transición de la versión 3.5.1 a la 4.0.0, introduciendo el uso de repositorios Git para publicar los PKGBUILD. Los paquetes existentes se descartaron, salvo aquellos que sus mantenedores migraron manualmente a la nueva infraestructura.

### Repositorios Git para paquetes AUR3

El [AUR Archive](https://github.com/aur-archive) en GitHub tiene un repositorio para cada paquete que estaba en AUR 3 en el momento de la migración. Por otro lado, existe el repositorio [aur3-mirror](https://github.com/felixonmars/aur3-mirror/) que proporciona lo mismo.

## Instalar paquetes

La instalación de paquetes desde AUR es un proceso relativamente simple. En esencia consiste en:

1.  Obtener los archivos para la compilación, incluyendo el [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") y posiblemente otros archivos necesarios.
2.  Verificar que el [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") y los archivos acompañantes no son maliciosos.
3.  Ejecutar `makepkg -si` en el directorio donde se han colocado los archivos. Esta orden descarga la fuente, resuelve depedencias con [pacman](/index.php/Pacman "Pacman"), compila, empaca e instala el paquete.

**Nota:** AUR no tiene soporte, por lo que cualquier paquete que instale es *responsabilidad del usuario* actualizarlo, no de pacman. Si se actualizan paquetes en los repositorios oficiales, deberá reconstruir cualquier paquete de AUR que dependa de esas bibliotecas.

### Requisitos previos

Primero, asegúrese de que las herramientas necesarias estén instaladas. El grupo de paquetes [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) debe ser suficiente; incluye [make](https://www.archlinux.org/packages/?name=make) y otras herramientas necesarias para compilar desde el código fuente.

**Nota:** Los paquetes disponibles en AUR asumen que tiene instalado el grupo [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), es decir, no enumeran los miembros del grupo como dependencias explícitamente.

A continuación, elija un directorio de compilación apropiado. Un directorio de compilación es simplemente una carpeta en la que se construirá el paquete o «se compilará», y puede ser cualquier carpeta. En el ejemplo que se sigue, la carpeta `~/builds` será el directorio de compilación.

### Obtener los archivos de compilación

Localice el paquete en AUR. Esto se realiza utilizando la función de búsqueda (esto es, el recuadro de texto de la parte superior de la [página principal de AUR](https://aur.archlinux.org/)). Al pulsar sobre el nombre de la aplicación en la lista de búsqueda, nos llevará a una página de información sobre el paquete. Lea la descripción para confirmar que este es el paquete deseado, observe si el paquete ha sido actualizado y lea los comentarios.

Existen diferentes métodos para adquirir los archivos de compilación:

*   Clonar el repositorio [git](/index.php/Git "Git") que tiene el nombre «Git Clone URL» en los detalles del paquete:

```
$ git clone https://aur.archlinux.org/*package_name*.git

```

	Una ventaja de este método es la facilidad de actualizar el repositorio con la orden `git pull`.

*   Descargar los archivos necesarios de compilación. Desde la página de información del paquete, descargue los archivos de compilación pulsando el «tarball» que aparece en el lado izquierdo, cerca del final de los detalles del paquete. Este archivo debe ser guardado en el directorio de compilación o una copia del archivo en dicho directorio después de la descarga.

```
$ tar -xvf *package_name*.tar.gz

```

*   También se puede descargar el tarball desde la terminal (para luego extraerlo):

```
$ curl -L -O https://aur.archlinux.org/cgit/aur.git/snapshot/*package_name*.tar.gz

```

### Compilar e instalar el paquete

Cambie los directorios al directorio que contiene el [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") del paquete.

```
$ cd *nombre_del_paquete*

```

**Advertencia:** Verifique cuidadosamente el [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), cualquier archivo *.install* y cualquier otro archivo presente en el repositorio git del paquete, en busca de secuencia de órdenes maliciosas o peligrosas. Si tiene dudas, no compile el paquete, y [dé el aviso](/index.php/General_troubleshooting#Additional_support "General troubleshooting") en los foros o en la lista de correos. Ya se ha encontrado antes código malicioso en paquetes. [[1]](https://lists.archlinux.org/pipermail/aur-general/2018-July/034151.html)

Vea los contenidos de todos los archivos proporcionados. Por ejemplo, para usar el paginador *less* para ver `PKGBUILD` haga:

```
$ less PKGBUILD

```

**Sugerencia:** Si está actualizando un paquete, es posible que desee ver los cambios desde el último envío.

*   Para ver los cambios desde el último envío utilice `git show`.
*   Para ver los cambios desde el último envío utilizando *vimdiff*, haga `git difftool @~..@ vimdiff`. La ventaja de *vimdiff* es que puede ver todo el contenido de cada archivo junto con los indicadores de lo que ha cambiado.

Construya el paquete. Después de confirmar manualmente el contenido de los archivos, ejecute [makepkg](/index.php/Makepkg "Makepkg") como un usuario normal:

```
$ makepkg -si

```

*   `-s`/`--syncdeps` resuelve e instala automáticamente cualquier dependencia con [pacman](/index.php/Pacman "Pacman") antes de compilar. Si el paquete depende de otros paquetes de AUR, deberá primero instalarlos manualmente.
*   `-i`/`--install` instala el paquete si está compilado correctamente. En otro caso, el paquete compilado se puede instalar con `pacman -U *package*.pkg.tar.xz`.

Otros indicadores útiles son:

*   `-r`/`--rmdeps` elimina las dependencias de compilación después de la compilación, ya que las mismas no serán necesarias. Sin embargo, es posible que estas dependencias tengan que reinstalarse la próxima vez que se actualice el paquete.
*   `-c`/`--clean` limpia los archivos de compilación temporales después de la compilación, ya que no serán necesarios. Estos archivos generalmente solo se necesitan al depurar el proceso de compilación.

**Nota:** El ejemplo anterior es solo un breve resumen del proceso de compilación. Se recomienda *encarecidamente* que lea los artículos [makepkg (Español)](/index.php/Makepkg_(Espa%C3%B1ol) "Makepkg (Español)") y [ABS (Español)](/index.php/Arch_Build_System_(Espa%C3%B1ol) "Arch Build System (Español)") para obtener más información.

## Feedback

La [interfaz Web de AUR](https://aur.archlinux.org) facilita hacer comentarios que permite a los usuarios proporcionar sugerencias y feedback para contribuir a mejorar el PKGBUILD. Evite pegar parches o PKGBUILD en la sección de comentarios: se vuelven rápidamente obsoletos y acaban ocupando innecesariamente mucho espacio. En su lugar, envíe los archivos al mantenedor, o incluso utilice un [cliente pastebin](/index.php/Pastebin_Clients "Pastebin Clients").

Una de las actividades más fáciles para **todos** los usuarios de Arch es navegar por AUR y **votar** por sus paquetes favoritos utilizando la interfaz web. Todos los paquetes son elegibles para ser adoptados por un TU (Trusted Users —*«usuarios de confianza»*—) para su inclusión en el [repositorio community](/index.php/Repositorio_community "Repositorio community"), y el recuento de votos es uno de los factores considerados en este proceso, ¡por lo que votar es un interés de todos!

## Compartir y mantener los paquetes

**Note:** Consulte [Talk:Arch User Repository#Scope of the AUR4 section](https://wiki.archlinux.org/index.php?title=Talk:Arch_User_Repository&oldid=484964#Scope_of_the_AUR4_section) antes de realizar cambios en esta sección.

Los usuarios pueden **compartir** los PKGBUILD a través de Arch User Repository. Este no contiene los paquetes binarios, pero permite a los usuarios subir sus PKGBUILD que pueden ser descargados por otros. Estos PKGBUILD no tienen ningún apoyo oficial y, por tanto, no se han investigado a fondo, por lo que se deben utilizar con cautela y bajo su propio riesgo por el usuario final.

### Enviar paquetes

**Advertencia:** Antes de intentar enviar un paquete, se espera que se familiarice con [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards") y todos los artículos indicados en «Artículos relacionados». **Verifique cuidadosamente** que lo que está cargando es correcto. Los paquetes que infrinjan las reglas podrán **eliminarse** sin previo aviso.

Si no está seguro de ningún modo sobre el paquete o el proceso de compilación/envío, incluso después de haber leído varias veces esta sección, envíe el PKGBUILD a la [lista de correo de AUR](https://mailman.archlinux.org/mailman/listinfo/aur-general), el [foro de AUR](https://bbs.archlinux.org/viewforum.php?id=4) en los foros de Arch, o pregunte en nuestro [IRC channel](/index.php/IRC_channel "IRC channel") para su revisión pública antes de agregarlo a AUR.

#### Reglas de envío

Al enviar un paquete, observe las siguientes reglas:

*   Los PKGBUILD enviados no deben compilar aplicaciones **ya disponibles en cualquiera** de los **repositorios oficiales** con binarios bajo ninguna circunstancia. Compruebe la [base de datos de paquetes oficiales](https://www.archlinux.org/packages/) para ver el paquete. Si existe alguna versión de la misma, **no** envíe el paquete. Si el paquete oficial está desactualizado, márquelo como tal. Si el paquete oficial está roto o carece de un recurso, entonces presente un [informe de error](https://bugs.archlinux.org/).

	**Excepción** a esta regla estricta solo lo pueden ser aquellos paquetes que tengan **características adicionales** habilitadas y/o **parches** en comparación con las oficiales. En tal caso, `pkgname` debería ser diferente para expresar esa diferencia. Por ejemplo, un paquete para la GNU screen que contiene el parche de la barra lateral se podría llamar `screen-sidebar`. Además, el vector `provides=('screen')` se debe utilizar para evitar conflictos con el paquete oficial.

*   **Verifique en AUR** si el paquete **ya existe**. Si ya tiene un mantenedor, los cambios se pueden enviar en un comentario a la atención del mantenedor. Si no hay mantenedor o el mantenedor no responde, el paquete se puede adoptar y actualizar según sea necesario. No cree paquetes duplicados.

*   Asegúrese de que el paquete que desea cargar es **útil**. ¿Alguien más quiere usar este paquete? ¿Es muy especializado? Si unas cuantas personas encuentran este paquete útil, es apropiado para la presentación.

	AUR y los repositorios oficiales están destinados a paquetes que instalan generalmente software y contenido relacionado con software, incluidos uno o más de los siguientes: ejecutables; archivo(s) de configuración; documentación en línea o fuera de línea para un software específico o para la distribución de Arch Linux en su conjunto; medios destinados a ser utilizados directamente por el software.

*   No utilice `replaces` en un PKGBUILD de AUR a menos que se cambie el nombre del paquete, por ejemplo cuando *Ethereal* se convirtió en *Wireshark*. Si el paquete es una **versión alternativa de un paquete ya existente**, utilice `conflicts` (y ​​`provides` si ese paquete es requerido por otros). La principal diferencia es que después de la sincronización (-Sy), pacman inmediatamente quiere reemplazar un paquete 'ofensivo' instalado al encontrar un paquete con la coincidencia `replaces` en sus repositorios; `conflicts`, por otro lado, solo se evalúa al instalar el paquete, que generalmente es el comportamiento deseado porque es menos invasivo.

*   El envío de **binarios** debe **evitarse** si las fuentes están disponibles. AUR no debe contener el tarball binario creado por makepkg, ni debe contener la lista de archivos.

Agregue una **línea de comentario** a la parte superior del archivo `PKGBUILD` que contenga información sobre los **mantenedores** actuales y los **contribuidores** anteriores, respetando el siguiente formato. Recuerde disfrazar su correo electrónico para protegerse contra el correo no deseado. Las líneas adicionales o innecesarias son facultativas.

	Si asume la función de mantenedor de un PKGBUILD existente, agregue su nombre a la parte superior de este modo

```
# Maintainer: su nombre <dirección at dominio dot tld>

```

	Si hubo mantenedores anteriores, colóquelos como contribuyentes. Lo mismo se aplica para el remitente original si este no fue usted. Si existe un conjunto de mantenedores, agregue los nombres de los otros mantenedores actuales también.

```
# Maintainer: su nombre <dirección at dominio dot tld>
# Maintainer: nombre de otros mantenedores <dirección at dominio dot tld>
# Contributor:  nombre de los mantenedores anteriores <dirección at dominio dot tld>
# Contributor: nombre del remitente original <dirección at dominio dot tld>

```

#### Verificación

Para tener acceso de modificación en AUR necesita disponer de [emparejamiento de claves SSH](/index.php/SSH_keys_(Espa%C3%B1ol) "SSH keys (Español)"). El contenido de la llave pública debe ser copiado en la página del perfil en la sección *My Account*, y la llave privada correspondiente debe ser configurada para el servidor `aur.archlinux.org`. Por ejemplo:

 `~/.ssh/config` 
```
Host aur.archlinux.org
  IdentityFile ~/.ssh/aur
  User aur
```

En el escenario ideal se debe [crear un nuevo par de llaves](/index.php/SSH_keys_(Espa%C3%B1ol)#Generando_las_llaves_SSH "SSH keys (Español)") y no usar un par existente, así se pueden revocar selectivamente en caso de que algo ocurra:

```
$ ssh-keygen -f ~/.ssh/aur

```

**Sugerencia:** Se pueden agregar múltiples llaves en su perfil separándolas con una nueva línea.

#### Crear un paquete nuevo

Para crear un repositorio Git vacío para un paquete, simplemente `git clone` el repositorio remoto con el nombre correspondiente. Si el paquete no existe en AUR, aparecerá la siguiente advertencia:

 `$ git clone ssh://aur@aur.archlinux.org/*package_name*.git` 
```
Cloning into '*package_name*'...
warning: You appear to have cloned an empty repository.
Checking connectivity... done.
```

**Nota:** Cuando un paquete es borrado de AUR, el repositorio git no es borrado, así que al clonar el repositorio puede que no este vació si alguien quiere crear un paquete con el mismo nombre.

Si hay un repositorio git existente, simplemente se crea un *remote* para el repositorio git de AUR y luego *fetch* en el repositorio:

```
$ git remote add *nombre_remoto* ssh://aur@aur.archlinux.org/*nombre_paquete*.git
$ git fetch *nombre_remoto*

```

Donde `*nombre_remoto*` es el nombre del *remote* a crear (*v.g.,* "origen"). Vea [Git#Using remotes](/index.php/Git#Using_remotes "Git") para mayor información.

El paquete aparecerá en AUR después del primer *push*. Desde ese momento se pueden agregar archivos con código fuente a la copia local del repositorio git. Vea [#Subir paquetes](#Subir_paquetes).

**Advertencia:** Sus AUR *commits* tendrán como autor su usuario y correo electrónico configurado en git. Es muy difícil cambiar un *commit* después que ha sido subido (vea [FS#45425](https://bugs.archlinux.org/task/45425)). Si desea enviar paquetes con un autor/email diferente, lo puede hacer con la orden `git config user.name [...]` y `git config user.email [...]`. ¡Revise sus *commits* y documentos antes de subirlos!

#### Subir paquetes

El procedimiento para subir paquetes a AUR es el mismo que para crear paquetes nuevos o para actualizaciones. Se necesita como mínimo un [PKGBUILD](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)") y un [.SRCINFO](/index.php/.SRCINFO ".SRCINFO") en el directorio de trabajo para subir (*push*) su paquete a AUR.

**Nota:** se necesita generar el archivo `.SRCINFO` cada vez que se cambie la metainformación del `PKGBUILD`. Por ejemplo, al modificar [pkgver()](/index.php/PKGBUILD_(Espa%C3%B1ol)#Variables "PKGBUILD (Español)") en actualizaciones. De otra manera, la web de AUR no va a mostrar las versiones actualizadas .

Para subir, añada el `PKGBUILD`, `.SRCINFO` y cualquier otro archivo necesario (como archivos `.install` o fuentes locales `.patch`) con `git add`, suba a su árbol local con un mensaje descriptivo `git commit`, y finalmente suba sus cambios a AUR con `git push`.

Ejemplo concreto:

```
$ makepkg --printsrcinfo > .SRCINFO
$ git add PKGBUILD .SRCINFO
$ git commit -m "*useful commit message*"
$ git push

```

**Sugerencia:**

*   Si inicialmente se ha olvidado el archivo `.SRCINFO` y lo ha agregado en un *commit* después, AUR va a rechazar sus subidas porque el archivo `.SRCINFO` debe existir en *cada* subida (*push*). Para solucionar este problema puede usar la orden [git rebase](https://git-scm.com/docs/git-rebase) con la opción `--root` o la orden [git filter-branch](https://git-scm.com/docs/git-filter-branch) con la opción `--tree-filter`.
*   Para prevenir archivos sin rastrear en las subidas, y para mantener el directorio de trabajo tan limpio como sea posible, excluya todos los archivos no deseados con `.gitignore` y fuerce agregar manualmente cada archivo. Vea [dotfiles#Using gitignore](/index.php/Dotfiles#Using_gitignore "Dotfiles").

### Mantener los paquetes

*   Si se mantiene un paquete y desea actualizar el PKGBUILD para el mismo, basta con reenviarlo.
*   Compruebe si hay feedback y comentarios de otros usuarios y trate de incorporar las mejoras que le sugieren, ¡considere que es un proceso de aprendizaje!
*   Por favor, no presente un paquete, para luego olvidarse de él. El trabajo del mantenedor es mantener el paquete, buscando las actualizaciones y las mejoras del PKGBUILD.
*   Si no desea seguir manteniendo el paquete, por alguna razón, etiquete el paquete como `disown` a través de la interfaz web de AUR y/o envíe un mensaje a la lista de correos de AUR. Si todos los mantenedores de un paquete AUR lo rechazan, se convertirá en un paquete [«huérfano»](https://aur.archlinux.org/packages/?SB=n&do_Orphans=Orphans).

### Otras solicitudes

Las solicitudes de orfandad, eliminación o fusión se pueden crear haciendo clic en el enlace «Submit Request» bajo el enlace «Package Actions» en el lado derecho. Esto envía automáticamente un correo electrónico de notificación al actual mantenedor del paquete y a la [aur-requests lista de correo](https://mailman.archlinux.org/mailman/listinfo/aur-requests) para su discusión. El [Trusted Users](/index.php/Trusted_Users "Trusted Users") aceptará o rechazará la solicitud.

*   Las solicitudes de orfandad se otorgarán después de dos semanas, si el mantenedor actual no reaccionó.
*   Las solicitudes de fusión son para eliminar la base del paquete y transferir sus votos y comentarios a otra base de paquetes. Se requiere el nombre de base del paquete para fusionar. Tenga en cuenta que esto no tiene nada que ver con 'git merge' o las solicitudes de fusión de GitLab.
*   Las solicitudes de eliminación requieren la siguiente información:
    *   Una breve nota que explique el motivo de la eliminación. Tenga en cuenta que los comentarios de un paquete no indican suficientemente las razones por las cuales un paquete está listo para su eliminación. Porque tan pronto como una TU toma medidas, el único lugar donde se puede obtener dicha información es la lista de correo.
    *   Detalles del soporte, como cuando un paquete es proporcionado por otro paquete, si uno mismo es el mantenedor, si es renombrado y si el propietario original acepta, etc.
    *   Las solicitudes de eliminación pueden rechazarse, en cuyo caso, si usted es el mantenedor del paquete, es probable que se le aconseje que no lo reconozca, para permitir la adopción por parte de otro empaquetador.

## Traducir la interfaz web

Consulte [i18n.txt](https://projects.archlinux.org/aurweb.git/tree/doc/i18n.txt) en el árbol fuente de AUR para obtener información sobre cómo crear y mantener la traducción de la interfaz web de AUR.

## Sintaxis de comentario

La sintaxis de [Python-Markdown](https://python-markdown.github.io/) es compatible con los comentarios. Proporciona la sintaxis básica de [Markdown](https://en.wikipedia.org/wiki/Markdown "wikipedia:Markdown") para dar formato a los comentarios. Tenga en cuenta que esta implementación tiene algunas [diferencias](https://python-markdown.github.io/#differences) ocasionales con respecto a las [reglas de sintaxis](https://daringfireball.net/projects/markdown/syntax) oficiales. Confirme el hash para el repositorio Git del paquete y las referencias a los tickets para Flyspray se convertirán en enlaces automáticamente. Los comentarios largos se contraen y se pueden expandir bajo demanda.

## FAQ

### ¿Que es AUR?

AUR (Arch User Repository) es el lugar donde la comunidad de Arch Linux puede subir los [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") de las aplicaciones, bibliotecas, etc., y compartirlos con el resto de la comunidad. Los demás usuarios pueden votar para que sus favoritos entren en el [repositorio community](/index.php/Repositorio_community "Repositorio community") de modo que puedan ser instalados en Arch Linux en formato binario.

### ¿Qué tipo de paquetes se permiten en AUR?

Los paquetes en AUR no son más que «scripts de compilación», es decir, instrucciones para construir los binarios que pueden ser manejados por pacman. Para la mayor parte de los casos, no hay limitaciones, siempre y cuando se ajusten a [las directrices](#Reglas_de_envío) de la utilidad antes mencionada y a los términos de licencia del contenido. En otros casos, cuando se menciona que «no se puede vincular» a las descargas, como cuando los contenidos no son redistribuibles, solo se podrá hacer uso del mismo nombre del archivo como la fuente. Esto significa y requiere que los usuarios deben tener ya la fuente en el directorio de compilación antes de iniciar el proceso de construcción del paquete. En caso de duda, pregunte.

### ¿Cómo puedo votar por los paquetes en AUR?

Inscríbase en el [sitio web de AUR](https://aur.archlinux.org/) para tener acceso a la opción "Vote for this package" («Vote por este paquete») mientras explora los paquetes. Después de registrarse, también es posible votar desde la línea de órdenes con [aurvote](https://aur.archlinux.org/packages/aurvote/), [aurvote-git](https://aur.archlinux.org/packages/aurvote-git/) o [aur-auto-vote-git](https://aur.archlinux.org/packages/aur-auto-vote-git/).

Alternativamente, si ha configurado [autenticación ssh](#Verificación) como se indicó anteriormente, puede votar directamente desde la línea de órdenes usando su clave ssh. Esto significa que no necesitará guardar o escribir su contraseña AUR.

```
ssh aur@aur.archlinux.org vote <PACKAGE_NAME>

```

### ¿Qué es un usuario de confianza / Trusted Users (TU)?

Un [Trusted Users (*«usuarios de confianza»*)](/index.php/AUR_Trusted_User_Guidelines "AUR Trusted User Guidelines"), siglas en inglés TU, es una persona encargada de supervisar el repositorio AUR y el [repositorio community](/index.php/Repositorio_community "Repositorio community"). Ellos son los que colocan los paquetes más votados en el repositorio *community*, marcan los PKGBUILDs como seguros y mantienen AUR.

### ¿Cuál es la diferencia entre Arch User Repository y el repositorio community?

Arch User Repository contiene todos los PKGBUILD que los usuarios envían; para instalarlos tiene que construirlos manualmente con [makepkg](/index.php/Makepkg "Makepkg"). Cuando un PKGBUILD obtiene suficientes votos, pasa al [repositorio community](/index.php/Repositorio_community "Repositorio community") (mantenido por los usuarios de confianza), donde los paquetes binarios pueden instalarse directamente con [pacman](/index.php/Pacman_(Espa%C3%B1ol) "Pacman (Español)").

### Un paquete en AUR está desactualizado, ¿qué hago?

Puede marcarlo como obsoleto. Si no se actualiza en un periodo de tiempo razonable, lo mejor es avisar a su mantenedor por email. Si el responsable no responde, puede comunicarlo a la lista de correo general de AUR, para que un TU (Trusted Users —*«usuarios de confianza»*—) declare huérfano al PKGBUILD y pueda adoptarlo si desea mantenerlo él mismo. Cuando se trate de un paquete que lleva desactualizado más de 3 meses y, en general, no se actualiza desde hace mucho tiempo, por favor agregue esto en su solicitud de orfandad.

Mientras tanto, puede intentar actualizar el paquete editando el PKGBUILD localmente. A veces, las actualizaciones no requieren cambios en el proceso de compilación o paquete, en cuyo caso basta con actualizar la matriz `pkgver` o `source`.

**Nota:** Los [paquetes VCS](/index.php/VCS_package_guidelines "VCS package guidelines") no se consideran obsoletos cuando el pkgver cambia, no los marque ya que el mantenedor simplemente desmarca el paquete y lo ignora. Los mantenedores de AUR no deberían cometer errores de pkgver.

### Foo, que está en AUR, no me compila con makepkg, ¿qué hago?

Probablemente está pasando por alto alguna cosa.

1.  Ejecute `pacman -Syyu` antes de compilar nada con `makepkg` dado que el problema puede ser que el sistema no está al día.
2.  Asegúrese de que tiene instalados tanto los grupos «base» como «base-devel».
3.  Pruebe usando la opción «`-s`» con `makepkg` para comprobar e instalar todas las dependencias necesarias antes de comenzar el proceso de compilación.

Asegúrese de leer primero el PKGBUILD y los comentarios en la página de AUR del paquete en cuestión. La razón puede no ser trivial después de todo. La personalización de CFLAGS, LDFLAGS y MAKEFLAGS puede causar fallos. También es posible que el PKGBUILD se rompe para todos. Si no puede resolverlo por su cuenta, simplemente informe al mantenedor, por ejemplo, mediante la publicación de los errores que está recibiendo en los comentarios de la página de AUR.

Para verificar si el PKGBUILD está roto, o si su sistema está mal configurado, considere compilar en un entorno chroot limpio. Construirá su paquete en un entorno limpio de Arch Linux, con solo dependencias (de compilación) instaladas y sin personalización del usuario. Para hacer esto [instale](/index.php/Install "Install") [devtools](https://www.archlinux.org/packages/?name=devtools) y ejecute `extra-x86_64-build` en lugar de `makepkg`. Para paquetes [multilib](/index.php/Multilib "Multilib"), ejecute `multilib-build`. Consulte [DeveloperWiki:Building in a clean chroot](/index.php/DeveloperWiki:Building_in_a_clean_chroot "DeveloperWiki:Building in a clean chroot") para más información. Si el proceso de compilación aún falla en un entorno chroot limpio, el problema probablemente esté en el PKGBUILD.

### ERROR: One or more PGP signatures could not be verified!; ¿qué debería hacer?

Lo más probable es que no tenga las claves públicas requeridas en su depósito de claves personal para verificar los archivos descargados. Si uno o más archivos .sig se descargan al compilar el paquete, [makepkg verificará automáticamente los archivos correspondientes con la clave pública de su firmante](/index.php/Makepkg#Signature_checking "Makepkg"). Si no tiene la clave requerida en su depósito de claves personal, *makepkg* no hará la verificación.

La forma recomendada de tratar este problema es importar la clave pública requerida, ya sea [manualmente](/index.php/GnuPG#Import_a_public_key "GnuPG") o [desde un servidor de claves](/index.php/GnuPG#Use_a_keyserver "GnuPG"). A menudo, simplemente puede encontrar la huella digital de las claves públicas necesarias en la sección [validpgpkeys](/index.php/PKGBUILD#validpgpkeys "PKGBUILD") del [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

### ¿Cómo hacer un PKGBUILD?

Lo mejor es mirar [Creating packages (Español)](/index.php/Creating_packages_(Espa%C3%B1ol) "Creating packages (Español)"). Recuerde mirar en AUR antes de crear el PKGBUILD para no duplicar los esfuerzos.

### Quiero enviar un PKGBUILD ¿podría alguien comprobar antes si tiene errores?

Si quisiera recibir comentarios a tu PKGBUILD, envíelo a la lista de correo de AUR para que los TU (Trusted Users —*«usuarios de confianza»*—) y los otros miembros de AUR puedan orientarle para mejorarlo. Otro lugar donde puede encontrar ayuda es el [canal IRC](/index.php/ArchChannel "ArchChannel"), #archlinux en irc.freenode.net. También puede usar [namcap](/index.php/Namcap "Namcap") para depurar errores de su PKGUILD y del paquete resultante.

### ¿Qué hacer para que un PKGBUILD pase al repositorio community?

Por lo general, son necesarios, al menos, 10 votos para que algo se mueva al [repositorio community](/index.php/Repositorio_community "Repositorio community"). Sin embargo, si un TU (Trusted Users —*«usuarios de confianza»*—) quiere apoyar un paquete, se suele pasar dicho paquete al repositorio.

Llegar al mínimo requerido de votos no es el único requisito, tiene que haber un TU (Trusted Users —*«usuarios de confianza»*—) dispuesto a mantener el paquete. Los TU (Trusted Users —*«usuarios de confianza»*—) no están obligados a mover un paquete al repositorio *community*, incluso si tiene miles de votos.

Por lo general, cuando un paquete muy popular permanece en AUR es porque:

*   Arch Linux ya tiene otra versión de un paquete en los repositorios
*   Su licencia prohíbe la redistribución
*   Ayuda a recuperar PKGBUILDs enviados por el usuario. Los [AUR helpers](/index.php/AUR_helpers "AUR helpers") están por definición [sin soporte](https://bbs.archlinux.org/viewtopic.php?pid=828310#p828310).

Véase también [Reglas para paquetes que ingresan en el repositorio community](/index.php/AUR_Trusted_User_Guidelines#Rules_for_Packages_Entering_the_.5Bcommunity.5D_Repo "AUR Trusted User Guidelines").

### ¿Cómo puedo acelerar los repetidos procesos de compilación?

Consulte [Makepkg#Improving compile times](/index.php/Makepkg#Improving_compile_times "Makepkg").

### ¿Cuál es la diferencia entre los paquetes foo y foo-git?

Muchos paquetes de AUR se presentan en versiones regulares ("estables") y de desarrollo ("inestables"). Un paquete de desarrollo generalmente tiene un sufijo como `-cvs`, `-svn`, `-git`, `-hg`, `-bzr` o `-darcs`. Si bien los paquetes de desarrollo no están destinados para uso regular, pueden ofrecer nuevas características o correcciones de errores. Debido a que estos paquetes descargan la última fuente disponible cuando ejecuta `makepkg`, no está directamente disponible para estos una versión del paquete para rastrear posibles actualizaciones. Del mismo modo, estos paquetes no pueden realizar una suma de comprobación de autenticidad, sino que debemos fiarnos de los mantenedores del repositorio Git.

Véase también [System maintenance#Use proven software packages](/index.php/System_maintenance#Use_proven_software_packages "System maintenance").

### ¿Por qué foo desapareció de AUR?

Es posible que el paquete haya sido adoptado por un TU (Trusted Users —*«usuarios de confianza»*—) y ahora esté en el [repositorio community](/index.php/Repositorio_community "Repositorio community").

Los paquetes pueden eliminarse si no cumplen con las [#Reglas de envío](#Reglas_de_envío). Consulte los [aur-requests archivos](https://lists.archlinux.org/pipermail/aur-requests/) para conocer el motivo de la eliminación.

Si el paquete estaba presente en AUR3, podría no haber sido [migrado a AUR4](https://lists.archlinux.org/pipermail/aur-general/2015-August/031322.html). Consulte los [#Repositorios Git para paquetes AUR3](#Repositorios_Git_para_paquetes_AUR3) donde se conservará.

### ¿Cómo puedo averiguar si alguno de los paquetes instalados desapareció de AUR?

La forma más sencilla es verificar el estado HTTP de la página AUR del paquete:

```
$ comm -23 <(pacman -Qqm | sort) <(curl [https://aur.archlinux.org/packages.gz](https://aur.archlinux.org/packages.gz) | gzip -cd | sort)

```

Si utiliza un [AUR helper](/index.php/AUR_helper "AUR helper"), puede acortar este script reemplazando la orden curl con cualquier orden que consulte AUR para un paquete.

### ¿Cómo puedo obtener una lista de todos los paquetes de AUR?

*   [https://aur.archlinux.org/packages.gz](https://aur.archlinux.org/packages.gz)
*   Utilice `aurpkglist` de [python3-aur](https://aur.archlinux.org/packages/python3-aur/)

## Véase también

*   [AUR Web Interface](https://aur.archlinux.org)
*   [AUR Mailing List](https://lists.archlinux.org/listinfo/aur-general)
*   [DeveloperWiki:AUR Cleanup Day](/index.php/DeveloperWiki:AUR_Cleanup_Day "DeveloperWiki:AUR Cleanup Day")