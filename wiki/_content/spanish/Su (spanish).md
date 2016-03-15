La orden **su** (**s**ubstitute **u**ser) se utiliza para asumir la identidad de otro usuario en el sistema, normalmente root. Esto ahorra tener que cerrar la sesión en curso y volver a iniciarla después como usuario normal. En su lugar, puede iniciar sesión como otro usuario **durante** su sesión, iniciando una especie de «subsesión», y, luego, cerrar esta última sesión, para volver a la anterior, cuando haya terminado.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Utilización](#Utilizaci.C3.B3n)
*   [3 Seguridad](#Seguridad)
*   [4 Consejos y trucos](#Consejos_y_trucos)
    *   [4.1 Shell de inicio de sesión](#Shell_de_inicio_de_sesi.C3.B3n)
    *   [4.2 su y wheel](#su_y_wheel)

## Instalación

su es parte del paquete [util-linux](https://www.archlinux.org/packages/?name=util-linux), que se instala por defecto en Arch como miembro del grupo [base](https://www.archlinux.org/groups/x86_64/base/).

## Utilización

Para asumir el inicio de sesión de otro usuario, pase el nombre de usuario que desea convertir a su, como sigue:

```
# su nombre_usuario

```

Se le pedirá la contraseña del usuario al que está invocando.

Si no se pasa ningún nombre de usuario, su asume que el usuario es root y la contraseña por la que se le preguntará será la de root.

## Seguridad

Desde una perspectiva de seguridad, podría decirse que es mejor establecer y utilizar [sudo](/index.php/Sudo_(Espa%C3%B1ol) "Sudo (Español)") en lugar de su. El sistema sudo le mostrará un prompt que tiene su propia contraseña –o ninguna, si está configurado así– en lugar de la del usuario de destino (la cuenta del usuario que está intentando utilizar). De esta manera no tiene que compartir contraseñas entre los usuarios, y si alguna vez necesita evitar que un usuario tenga acceso como root (o el acceso a cualquier otra cuenta, para el caso), no tendrá que cambiar la contraseña de root, que es una molestia que afecta a los demás usuarios; bastará con revocar el acceso a sudo de ese usuario.

Si sudo se ha configurado para permitir al usuario ejecutar la shell de root, el usuario puede ejecutar `sudo -s` o `sudo -i` para imitar `su` o `su -`, respectivamente, y proporcionando su propia contraseña o sin contraseña, en lugar de la contraseña de root. Del mismo modo, `sudo -u john -i` imita a `su - john` si tiene permitido ejecutar la shell de john.

## Consejos y trucos

### Shell de inicio de sesión

El comportamiento predeterminado de su es permanecer dentro del directorio vigente y de mantener las variables del entorno del usuario original (en lugar de cambiar a los del nuevo usuario).

Consideraciones importantes a tener en cuenta:

*   A veces puede ser ventajoso para un administrador del sistema utilizar la cuenta shell de un usuario normal y no la suya propia. En particular, a veces, la manera más eficiente para resolver el problema de un usuario, es iniciar sesión en la cuenta de ese usuario a fin de reproducir o depurar el problema.

*   Sin embargo, en muchas situaciones no es deseable, o incluso puede ser peligroso para el usuario root, estar operando desde la cuenta de la shell de un usuario normal y con las variables del entorno de esa cuenta, más que desde las suyas propias. Podría darse el caso de que, sin intención, desde la cuenta shell de un usuario normal, root instalara un programa o hiciera cambios en el sistema que no tendrían el mismo resultado que si se hicieran durante el uso de la cuenta de root. Por ejemplo, podría instalar un programa de modo que el mismo le diera al usuario normal el poder para dañar accidentalmente el sistema u obtener acceso no autorizado a determinados datos.

Por lo tanto, es aconsejable que los usuarios administradores, así como cualquier otro usuario que está autorizado a utilizar su (y se sugiere que sean pocos, si los hay) adquieran el hábito de utilizar la orden su con un espacio y un guión. El guión tiene dos efectos:

1.  Cambiar desde el directorio en curso al directorio home del nuevo usuario (por ejemplo, a `/root` en el caso de que el usuario destinatario sea root) para *acceder* como ese usuario.
2.  Cambiar las variables del entorno a las del nuevo usuario según lo indicado en su propio archivo `~/.bashrc`. Es decir, si el primer argumento que se pasa a su es un guión, el directorio y el entorno en curso cambiarán a los que se obtendrían si el nuevo usuario hubiera iniciado su propia sesión en realidad (en lugar de hacerse cargo de la sesión ya existente).

Por lo tanto, los administradores, generalmente, deben utilizar su de la siguiente manera :

```
$ su -

```

Un resultado idéntico se produce añadiendo el nombre de usuario root:

```
$ su - root

```

Del mismo modo, lo anterior se puede hacer con cualquier otro usuario (por ejemplo, para un usuario llamado archie):

```
# su - archie

```

Es posible que desee añadir un alias en `~/.bashrc` como sigue:

```
alias su='su -'

```

### su y wheel

su de BSD permite únicamente a los miembros del [grupo](/index.php/Users_and_Groups_(Espa%C3%B1ol) "Users and Groups (Español)") «wheel» asumir la identidad de root por defecto. Este no es el comportamiento por defecto de su en GNU, pero dicho comportamiento puede ser imitado usando PAM. Descomente la línea apropiada en `/etc/pam.d/su`:

```
auth required pam_wheel.so use_uid

```