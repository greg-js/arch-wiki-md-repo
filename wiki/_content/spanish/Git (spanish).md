Artículos relacionados

*   [Gitweb](/index.php/Gitweb "Gitweb")
*   [Cgit](/index.php/Cgit "Cgit")
*   [HTTP tunneling#Tunneling Git](/index.php/HTTP_tunneling#Tunneling_Git "HTTP tunneling")
*   [Subversion](/index.php/Subversion "Subversion")
*   [Concurrent Versions System](/index.php/Concurrent_Versions_System "Concurrent Versions System")

> He conocido personas que piensan que git es la interfaz de Github, están equivocados, git es la interfaz de AUR.
> — Linus Torvalds

[Git](https://en.wikipedia.org/wiki/es:Git_(software) es un software de control de versiones diseñado y desarrollado por Linus Torvalds, el creador del kernel de Linux. Git es usado para mantener los paquetes en [AUR](/index.php/AUR_(Espa%C3%B1ol) "AUR (Español)"), y en bastantes proyectos, incluidas las fuentes para el kernel de Linux.

## Contents

*   [1 Instalación](#Instalación)
    *   [1.1 Programas Gráficos](#Programas_Gráficos)
*   [2 Configuración](#Configuración)
*   [3 Uso](#Uso)
    *   [3.1 Repositorio local](#Repositorio_local)
        *   [3.1.1 Preparación](#Preparación)
        *   [3.1.2 Confirmar cambios](#Confirmar_cambios)
        *   [3.1.3 Ver cambios](#Ver_cambios)
        *   [3.1.4 Ramas en un repositorio](#Ramas_en_un_repositorio)
    *   [3.2 Colaboración](#Colaboración)
        *   [3.2.1 Adoptando una buena etiqueta](#Adoptando_una_buena_etiqueta)
        *   [3.2.2 Clonar un repositorio](#Clonar_un_repositorio)
        *   [3.2.3 Solicitud de cambio](#Solicitud_de_cambio)
        *   [3.2.4 Usando remotos](#Usando_remotos)
        *   [3.2.5 Publicar en un repositorio](#Publicar_en_un_repositorio)
        *   [3.2.6 Trabajando con fusiones](#Trabajando_con_fusiones)
        *   [3.2.7 Enviar un parche a una lista de correo](#Enviar_un_parche_a_una_lista_de_correo)
    *   [3.3 Histórico y revisiones](#Histórico_y_revisiones)
        *   [3.3.1 Buscar en el histórico](#Buscar_en_el_histórico)
        *   [3.3.2 Revisiones para lanzamientos](#Revisiones_para_lanzamientos)
        *   [3.3.3 Organizando confirmaciones](#Organizando_confirmaciones)
*   [4 Trucos y consejos](#Trucos_y_consejos)
    *   [4.1 Usar git-config](#Usar_git-config)
    *   [4.2 Acelerar verificación](#Acelerar_verificación)
    *   [4.3 Valores por defecto del protocolo](#Valores_por_defecto_del_protocolo)
*   [5 Servidor Git](#Servidor_Git)
    *   [5.1 SSH](#SSH)

## Instalación

[Instale](/index.php/Help:Reading_(Espa%C3%B1ol)#Instalación_de_paquetes "Help:Reading (Español)") el paquete [git](https://www.archlinux.org/packages/?name=git). Para la versión en desarrollo instale el paquete [git-git](https://aur.archlinux.org/packages/git-git/). Verifique los requerimientos opcionales al usar *git svn*, *git gui* and *gitk*.

### Programas Gráficos

Véase también [Clientes gráficos de Git](https://git-scm.com/download/gui/linux).

*   **Giggle** — Cliente gráfico de git basado en GTK+.

	[https://wiki.gnome.org/Apps/giggle/](https://wiki.gnome.org/Apps/giggle/) || [giggle](https://www.archlinux.org/packages/?name=giggle)

*   **Git Cola** — Elegante y poderosa interfaz de usuario escrita en Python.

	[https://git-cola.github.io/](https://git-cola.github.io/) || [git-cola](https://aur.archlinux.org/packages/git-cola/)

*   **Git Extensions** — Interfaz de usuario para git sin necesidad de usar la terminal.

	[https://gitextensions.github.io/](https://gitextensions.github.io/) || [gitextensions](https://aur.archlinux.org/packages/gitextensions/)

*   **gitg** — Interfaz de GNOME para ver repositorios git.

	[https://wiki.gnome.org/Apps/Gitg](https://wiki.gnome.org/Apps/Gitg) || [gitg](https://www.archlinux.org/packages/?name=gitg)

*   **git-gui** — Interfaz gráfica de usuario basada en Tcl/Tk.

	[https://git-scm.com/docs/git-gui](https://git-scm.com/docs/git-gui) || [git](https://www.archlinux.org/packages/?name=git) + [tk](https://www.archlinux.org/packages/?name=tk)

**Nota:** Para activar corrección de lenguaje en *git-gui*, el paquete [aspell](https://www.archlinux.org/packages/?name=aspell) es necesario, asi como el diccionario correspondiente con la [variable de entorno](/index.php/Environment_variables_(Espa%C3%B1ol) "Environment variables (Español)") `LC_MESSAGES`. Vea [FS#28181](https://bugs.archlinux.org/task/28181) y el articulo [aspell](/index.php/Aspell_(Espa%C3%B1ol) "Aspell (Español)").

*   **gitk** — Navegador de repositorios git basada en Tcl/Tk.

	[https://git-scm.com/docs/gitk](https://git-scm.com/docs/gitk) || [git](https://www.archlinux.org/packages/?name=git) + [tk](https://www.archlinux.org/packages/?name=tk)

*   **QGit** — Interfaz gráfica de usuario para navegar revisiones, historia, parches y cambios en archivos.

	[https://github.com/tibirna/qgit](https://github.com/tibirna/qgit) || [qgit](https://www.archlinux.org/packages/?name=qgit)

*   **[RabbitVCS](https://en.wikipedia.org/wiki/RabbitVCS "wikipedia:RabbitVCS")** — Grupo de herramientas gráficas hechas para proporcionar acceso simple a su sistema de control de versiones.

	[http://rabbitvcs.org/](http://rabbitvcs.org/) || [rabbitvcs](https://aur.archlinux.org/packages/rabbitvcs/)

*   **Tig** — Interfaz para git basada en ncurses.

	[https://jonas.github.io/tig/](https://jonas.github.io/tig/) || [tig](https://www.archlinux.org/packages/?name=tig)

*   **ungit** — Proporciona facilidad en git para el usuario sin sacrificar la versatilidad.

	[https://github.com/FredrikNoren/ungit](https://github.com/FredrikNoren/ungit) || [nodejs-ungit](https://aur.archlinux.org/packages/nodejs-ungit/)

*   **GitHub Desktop** — Iterfaz gráfica de usuario basada en Electron, escrita por Github.

	[https://github.com/desktop/desktop](https://github.com/desktop/desktop) || [github-desktop](https://aur.archlinux.org/packages/github-desktop/)

## Configuración

Para usar Git es necesario usar un usuario y correo electrónico:

```
$ git config --global user.name  "*Pablo Perez*"
$ git config --global user.email "*pabloperez@ejemplo.com*"

```

Vea [#Trucos y consejos](#Trucos_y_consejos) para mas configuraciones.

## Uso

Este tutorial muestra como usar Git para controlar y revisar de manera básica distribuida un proyecto.

Git es un sistema de control de versiones, lo cual quiere decir que la historia completa de los cambios hechos a un repositorio es guardada localmente, en una carpeta llamada `./.git` en el directorio del proyecto. Los archivos del proyecto que son visibles al usuario constituyen el *árbol de trabajo*. Estos archivos pueden ser actualizados para coincidir con las revisiones guardadas en `./.git` usando los comandos de `git` (v.g. `git checkout`), nuevas revisiones pueden ser creadas al modificar estos archivos y ejecutar el comando de `git` apropiado (e.g. `git commit`).

Vea [gitglossary(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/gitglossary.7) para una definicion mas completa de los terminos usados en este tutorial.

El proceso de trabajo típico con Git es:

1.  Cree un proyecto nuevo o clone un proyecto remoto.
2.  Cree una rama para implementar cambios, y confirme (`git commit`) esos cambios.
3.  Consolide sus cambios para una mejor organización y entendimiento.
4.  Incorpore (`git merge`) sus cambios en la rama principal.
5.  (Opcional) Suba (`git push`) los cambios a un servidor remoto.

### Repositorio local

#### Preparación

**Inicializar** un nuevo repositorio. Esto creara e iniciará `./.git`:

```
$ cd (su proyecto)/
$ git init

```

Para guardar cambios en archivos del repositorio, estos tiene que ser agregados al *index* o *área de preparación*, esta operación también es conocida como *preparar*. Cuando se confirman los cambios usando `git commit`, son los archivos contenidos en el index los que se confirman en la rama actual, y no el contenido del árbol de trabajo.

**Nota:** El index es de hecho un archivo binario `.git/index`, el cual puede ser consultado con `git ls-files --stage`.

Para **agregar** archivos al index del árbol de trabajo:

```
$ git add *archivo1* *archivo2*

```

Esto guarda el estado actual de los archivos. Si los archivos son modificados, se puede ejecutar `git add` de nuevo para "agregar" la nueva versión al index.

**Agregar todos** los archivos:

```
$ git add .

```

**Sugerencia:** Para **ignorar** algunos archivos del comando `git add .`, cree un archivo llamado `.gitignore`: `.gitignore` 
```
# Archivo que posiblemente borrare
test-script

# Ignore todos los archivos .html, excepto 'importante.html'
*.html
!important.html

# Ignore todos los archivos recursiva mente en el directorio 'NoIncluir'
NoIncluir/**

```

Vea [gitignore(5)](http://git-scm.com/docs/gitignore) para más detalles.

**Remueva** un archivo de la área de trabajo (`--cached` preserva el estado actual de los archivos):

```
$ git rm *(--cached)* *archivo*

```

**Remueva todos** los archivos:

```
$ git rm --cached -r .

```

O también:

```
$ git reset HEAD -- .

```

En este caso, `HEAD` es una "referencia simbólica" a la revisión actual.

**Renombrar** un archivo:

```
$ git mv *archivo1* *archivo2*

```

**Nota:** `git mv` es un comando conveniente, es casi equivalente a `mv archivo1 archivo2` seguido por `git rm archivo1` y `git add archivo2`. La deteción de re-nombramiento durante la incorporación esta basada en la similitud del contenido, se ignora el método usado para el re-nombramiento del archivo. La razón de esto, que diferencia a Git de sistemas basados en parches como [Darcs](/index.php/Darcs "Darcs"), puede ser vista [aquí](http://permalink.gmane.org/gmane.comp.version-control.git/217).

**Listado** de archivos:

```
$ git ls-files

```

Por defecto, este comando muestra los archivos en la área de trabajo, archivos `--cached`.

#### Confirmar cambios

Una vez el contenido a ser guardado esta *preparado*, *confirme* ejecutando:

```
$ git commit -m "*Primera confirmación.*"

```

El parámetro `-m (*--message)*` es para un mensaje corto, si se omite el editor pre seleccionado abrirá para permitir un mensaje más extenso.

**Sugerencia:**

*   Siempre confirme cambios pequenos con mensajes significativos.
*   Para **agregar** todos los archivos modificados al index **y confirmarlos** en un solo comando, use el parametro `-a (*--all*)`, "todo"):

```
$ git commit -am "*Primera confirmación.*"

```

**Modifique** el mensaje de confirmación para la ultima confirmación. Esto también alterara la confirmación con los archivos que se *preparado*:

```
$ git commit --amend -m "*Mensaje.*"

```

Algunos de los comandos en este articulo toman confirmaciones como argumentos. Una confirmación puede ser identificada por uno de los siguientes métodos:

*   El resumen criptográfico de 40 dígitos SHA-1 (usualmente los primeros 7 dígitos son suficientes para identificar la confirmación de manera única)
*   La etiqueta de la confirmación, ya sea la el nombre de la rama o la marca (tag)
*   La etiqueta del `HEAD` siempre se refiere la rama en la cual se encuentre actualmente (generalmente la ultima modificación de la rama, a menos que se haya usado *git checkout* para revisar una versión anterior)
*   Cualquier caso anterior más `~` para referirse a una confirmación anterior. Por ejemplo, `HEAD~` se refiere a una confirmación antes de `HEAD`, y `HEAD~5` se refiere a cinco confirmaciones antes de `HEAD`.

#### Ver cambios

**Mostrar diferencias** entre confirmaciones:

```
$ git diff HEAD HEAD~3

```

o diferencias entre área de preparación y el árbol de trabajo:

```
$ git diff

```

**Obtenga** un **resumen** general de los cambios:

```
$ git status

```

**Ver historico** de cambios (donde "*-N*" es el numero de confirmaciones anteriores):

```
$ git log -p *(-N)*

```

#### Ramas en un repositorio

Modificaciones y nuevas características son usualmente examinadas en ramas. Cuando los cambios son satisfactorios se pueden incorporar en la rama principal (master).

**Crear** una rama, cuyo nombre refleja su propósito:

```
$ git branch *agregar-seccion-ayuda*

```

**Listado** de ramas:

```
$ git branch

```

**Cambiar** de rama:

```
$ git checkout *rama*

```

**Crear y cambian**:

```
$ git checkout -b *rama*

```

**Incorporar** una rama a la rama principal:

```
$ git checkout master
$ git merge *rama*

```

Los cambios serán incorporados si no hay conflictos. En caso de haberlos, Git mostrara un mensaje de error, y anotara los archivos en el árbol de trabajo grabando los conflictos. Las anotaciones pueden ser vistas con `git diff`. Conflictos son resueltos modificando los archivos,removiendo las anotaciones y confirmando la versión final. Vea [#Trabajando con fusiones](#Trabajando_con_fusiones) en la parte de abajo.

Cuando se haya terminado el trabajo en una rama, **bórrela** con:

```
$ git branch -d *branch*

```

### Colaboración

#### Adoptando una buena etiqueta

*   Cuando se considere contribuir a un proyecto existente, lea y entienda su licencia, ya que esta puede limitar excesivamente la habilidad para modificar el código. Algunas licencias pueden generar disputas sobre la autoría del código.
*   Piense sobre la comunidad del proyecto y que tan bien se puede encajar allí. Para tener un sentimiento del rumbo del proyecto, lea la documentación e incluso el [histórico](#Histórico_y_revisiones) del repositorio.
*   Cuando se solicite incluir (pull) una confirmación, o se suba un parche, mantenga el cambio pequeño, conciso y documentado; esto ayudara a los mantenedores a entender sus cambios y decidir si los incorporan, o para preguntar por una corrección.
*   Si una contribución es rechazada, no se desanime, el proyecto es de ellos. Si es importante, discuta las razones para la contribución tan clara y pacientemente como sea posible: con este procedimiento una solución puede que eventualmente sea posible.

#### Clonar un repositorio

Para comenzar a contribuir a un proyecto, **clone** el repositorio de este:

```
$ git clone *lugar* *directorio*

```

`*lugar*` puede ser una ruta o dirección de Internet. Cuando la clonación haya terminado, el lugar sera guardado y solo se necesitara un `git pull` para actualizar el repositorio.

#### Solicitud de cambio

Después de hacer algunos cambios, un contribuidor puede preguntarle al autor original de incorporar dichos cambios. Esto se denomina una solicitud de cambio (*pull request*).

Para **obtener (pull)**:

```
$ git pull *lugar* master

```

El comando *pull* combina los comandos recuperar (fetch) y fusionar (merge). Si hay conflictos (v.g. cuando el autor original hizo cambios la mismo tiempo), sera necesario solucionarlos manualmente.

Alternativamente, el autor original puede **seleccionar** los **cambios** que quiere incorporar. Usando la opción *fetch* (y la opción *log* con un símbolo `FETCH_HEAD` especial), el contenido de la solicitud puede ser visto antes de ser incorporado:

```
$ git fetch *lugar* master
$ git log -p HEAD..FETCH_HEAD
$ git merge *lugar* master

```

#### Usando remotos

Remotos son apodos para rastrear repositorios remotos. Una *etiqueta* es creada definiendo el lugar. Estas etiquetas son usadas para identificar repositorios de frecuente acceso.

**Crear** un remoto:

```
$ git remote add *etiqueta* *lugar*

```

**Recupere (fetch)** un remoto:

```
$ git fetch *etiqueta*

```

**Mostrar diferencias** entre la rama principal y la rama principal del remoto:

```
$ git log -p master..*etiqueta*/master

```

**Ver** remotos del repositorio actual:

```
$ git remote -v

```

Cuando se define un remoto que es el predecesor de una bifurcación (lideres del proyecto), se define como *upstream* (versión original).

#### Publicar en un repositorio

Después de tener acceso para modificar el repositorio, dado por los autores originales, **publique** (push) sus cambios con:

```
$ git push *lugar* *rama*

```

Cuando se ejecute *git clone*, se guarda el lugar original y se le da el nombre remoto de `origin`.

Asi, que lo que **típicamente** se ejecuta es:

```
$ git push origin master

```

Si se usa el parámetro `-u (--set-upstream-to)`, el lugar va a ser guardado y la próxima vez simplemente `git push` es necesario.

#### Trabajando con fusiones

Vea [Procedimiento para fusionar](https://git-scm.com/book/es/v2/Ramificaciones-en-Git-Procedimientos-B%C3%A1sicos-para-Ramificar-y-Fusionar) el el libro de Git para una explicación más extensa para solucionar conflictos en fusiones. Fusiones son generalmente reversibles. Si se desea cancelar una fusión, se puede usar el parámetro `--abort` (v.g. `git merge --abort` o `git pull --abort`).

#### Enviar un parche a una lista de correo

Si desea enviar parches directamente a una lista de correo, necesita instalar los siguientes paquetes: [perl-authen-sasl](https://www.archlinux.org/packages/?name=perl-authen-sasl), [perl-net-smtp-ssl](https://www.archlinux.org/packages/?name=perl-net-smtp-ssl) y [perl-mime-tools](https://www.archlinux.org/packages/?name=perl-mime-tools).

Asegúrese de tener su usuario y correo electrónica configurado, vea[#Configuración](#Configuración).

**Modifique** la configuración de su **e-mail**:

```
$ git config --global sendemail.smtpserver *smtp.gmail.com*
$ git config --global sendemail.smtpserverport *587*
$ git config --global sendemail.smtpencryption *tls*
$ git config --global sendemail.smtpuser *foobar@gmail.com*

```

Ahora debe ser posible **enviar** el **parche** a la lista de correo:

```
$ git add *nombre-archivo*
$ git commit -s
$ git send-email --to=*nombre-lista@servidorlista.org* --confirm=always -M -1

```

### Histórico y revisiones

#### Buscar en el histórico

`git log` mostrará el histórico con confirmaciones, resumen criptográfico, autor, fecha y el mensaje corto. El *resumen-criptográfico* es el "nombre del objeto" de una confirmación, típicamente 40 digitos SHA-1.

Para el **histórico** con el **mensaje extenso** (el "*resumen-criptográfico*" puede ser truncado, mientras que se mantenga único):

```
$ git show (*resumen-criptográfico*)

```

**Buscar** por un *modelo* en los archivos que están siendo rastreados:

```
$ git grep *modelo*

```

**Buscar** en archivos terminados con **`.c`** y **`.h`**:

```
$ git grep *modelo* -- '*.[ch]'

```

#### Revisiones para lanzamientos

**Etiqueta** (tag) de confirmaciones para revisiones:

```
$ git tag 2.14 *resumen-criptográfico*

```

*Etiquetar* se efectúa generalmente para [lanzamientos/revisiones](https://git-scm.com/book/es/v2/Fundamentos-de-Git-Etiquetado) pero puede ser cualquier cadena de caracteres. Generalmente etiquetas anotadas son usadas, porque estas se agregan a la base de datos de Git.

**Etiquete** la confirmación **actual** con:

```
$ git tag -a 2.14 -m "Versión 2.14"

```

**Listado** de etiquetas:

```
$ git tag -l

```

**Borrar** una etiqueta:

```
$ git tag -d 2.08

```

**Actualizar etiqueta** remota:

```
$ git push --tags

```

#### Organizando confirmaciones

Antes de solicitar cambios en un repositorio, es deseable **consolidar/reorganizar** las confirmaciones. Esto se puede hacer con *git rebase* y el parámetro `--interactive`:

```
$ git rebase -i *resumen-criptográfico*

```

Este comando abrirá un editor de texto con un resumen de todas las confirmaciones en el rango especificado; en el caso del comando anterior, incluyendo la confirmación mas reciente (`HEAD`) y hasta, pero excluyendo la confirmación `*resumen-criptográfico*`. Es posible usar notación de numérica, use por ejemplo `HEAD~3`, el cual incluirá las ultimas tres confirmaciones:

```
pick d146cc7 Test punto de montaje.
pick 4f47712 Explicación parámetro -o en el readme.
pick 8a4d479 Re nombrado de la documentación.

```

Modificando la acción en la primera columna dictara como se hará la reorganización. Las opciones son:

*   `pick` — Use esta confirmación como esta (por defecto).
*   `edit` — Edite archivos y/o mensaje de confirmación.
*   `reword` — Edite mensaje de confirmación.
*   `squash` — Fusión/envuelva con la confirmación anterior.
*   `fixup` — Fusión/envuelva con la confirmación anterior descartando su mensaje.

Las confirmaciones pueden ser re ordenadas o borradas del histórico (pero sea muy cuidadoso). Después de modificar un archivo, Git ejecutara la acción especificada; si se le pregunta resolver problemas, solucionelos y continue con `git rebase --continue` o cancele la reorganización con el comando `git rebase --abort`.

**Nota:** La opción *Squash* en las confirmaciones, solo es usado en confirmaciones locales, creara problemas en repositorios compartidos con mas usuarios.

## Trucos y consejos

### Usar git-config

Git lee su configuración de unos pocos archivos de configuración:

*   Cada repositorio contiene un archivo `.git/config` para configuracion especifica.
*   Cada usuario tiene un archivo `$HOME/.gitconfig` para configuraciones por defecto.
*   `/etc/gitconfig` es usado para configuraciones por defecto a nivel del sistema.

Estos archivos pueden ser modificados directamente, pero la manera recomendada para hacerlo es con `git config`, como se muestra en el siguiente ejemplo:

Listado de las siguientes variables establecidas:

```
$ git config {--local,--global,--system} --list

```

Establezca el editor de texto por defecto a [vim](/index.php/Vim_(Espa%C3%B1ol) "Vim (Español)") o [nano](/index.php/Nano_(Espa%C3%B1ol) "Nano (Español)"):

```
$ git config --global core.editor "nano -w"

```

Establezca la acción de publicar por defecto:

```
$ git config --global push.default simple

```

Establezca una herramienta diferente para *git difftool* (*meld* por defecto):

```
$ git config --global diff.tool vimdiff

```

Vea [git-config(1)](https://www.kernel.org/pub/software/scm/git/docs/git-config.html) y [Configuración de Git](https://git-scm.com/book/es/v2/Personalizaci%C3%B3n-de-Git-Configuraci%C3%B3n-de-Git) para más información.

### Acelerar verificación

Es deseable evitar tener que iniciar sesión interactiva mente en cada publicación al servidor Git.

*   Si se esta usando verificación con llaves SSH, use el [agente de SSH](/index.php/SSH_keys_(Espa%C3%B1ol)#Agentes_de_SSH "SSH keys (Español)"). Vea tambien [SSH#Acelerando SSh](/index.php/Secure_Shell_(Espa%C3%B1ol)#Acelerando_SSH "Secure Shell (Español)") y [SSH#Mantener la sesión activa](/index.php/Secure_Shell_(Espa%C3%B1ol)#Mantener_la_sesi.C3.B3n_activa "Secure Shell (Español)").
*   Si se esta usando verificación con usuario y contrasena, cambie a [llaves de SSH](/index.php/SSH_keys_(Espa%C3%B1ol) "SSH keys (Español)") si el servidor es compatible con SSH. De otra manera intente con [git-credential-cache](https://git-scm.com/docs/git-credential-cache) o [git-credential-store](https://git-scm.com/docs/git-credential-store).

### Valores por defecto del protocolo

Si se esta usando una conexión multiplexada, Git por SSH puede ser más rápido que por HTTPS. Algunos servidores (como AUR), solo admiten publicar con SSH. Por ejemplo, la siguiente configuración establecerá Git sobre SSH para cualquier repositorio alojado en AUR.

 `~/.gitconfig` 
```
[url "ssh://aur@aur.archlinux.org/"]
	insteadOf = https://aur.archlinux.org/
	insteadOf = http://aur.archlinux.org/
	insteadOf = git://aur.archlinux.org/

```

## Servidor Git

Como configurar la conexión a diferentes repositorios dependiendo en el protocolo usado.

### SSH

Para usar el protocolo SSH, primero genere una llave publica; para ello siga la guía en [llaves SSH](/index.php/SSH_keys_(Espa%C3%B1ol)#Generando_las_llaves_SSH "SSH keys (Español)"). Para montar un servidor SSH, siga la guie en [SSH](/index.php/Secure_Shell_(Espa%C3%B1ol) "Secure Shell (Español)").

Con un servidor SSH funcional y llaves generadas, copie el contenido de `~/.ssh/id_rsa.pub` a `~/.ssh/authorized_keys` (asegúrese que sea una sola linea). Ahora puede acceder al repositorio Git ejecutando:

```
$ git clone *usuario*@*ejemplo.com*:*mi_repositorio*.git

```

Ahora SSH le hará una pregunta de si/no, si se tiene la configuración `StrictHostKeyChecking` (por d efecto). Teclee `yes` seguido de `Intro`. Ahora se debe tener acceso al repositorio. Gracias a que la configuración es con SSH también debe tener derecho para hacer confirmaciones.

Para modificar un repositorio existente para usar SSH, el lugar remoto debe ser re-definido:

```
$ git remote set-url origin git@localhost:*mi_repositorio*.git

```

Conexiones en un puerto diferente al 22 pueden ser configuradas en base a cada servidor, en `/etc/ssh/ssh_config` o `~/.ssh/config`. Para configurar puertos para un repositorio (en este ejemplo 443):

 `.git/config` 
```
[remote "origin"]
    url = ssh://*usuario*@*ejemplo*.com:443/~*mi_repositorio*/repo.git
```

Es posible proteger incluso más la cuenta de SSH del usuario, aceptando solo comandos de descarga (pull) o de publicación (push) para ese usuario. Esto se hace reemplazando la shell de inicio de sesión por defecto con git-shell. Descripción en [Git en el servidor](https://git-scm.com/book/es/v2/Git-en-el-Servidor-Configurando-el-servidor).