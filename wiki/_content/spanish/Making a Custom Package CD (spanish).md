Si desea copiar algunos paquetes de una computadora con Arch Linux a otra (si tiene por ejemplo, una conexión a Internet lenta) utilizando un CD personalizado, haga lo siguiente:

*   Cree un repositorio de paquetes utilizando gensync [Custom local repository with ABS and gensync](/index.php/Custom_local_repository_with_ABS_and_gensync "Custom local repository with ABS and gensync"). Copie los paquetes de `/var/cache/pacman/pkg` al sistema con Arch Linux actualizado.

*   Cree una imagen iso del repositorio en un CD-R o en un CD-RW

*   Monte el CD en la segunda computadora con Arch Linux

*   Añada un repositorio personalizado a `/etc/pacman.conf`:

```
 [mycd]
 Server = file:///mnt/cd/pkg

```

Otra opción es simplemente copiar los archivos del CD en el directorio `/var/cache/pacman/pkg` del segundo ordenador. Pacman obtendrá los paquetes desde allí en vez de desde la red si los archivos están actualizados.

Otra opción más es crear un CD de instalación personalizado

1\. Copiar los archivos de /var/cache/pacman/pkg en un CD

2\. Crear en la pc un archivo repositorios

```
  #mkdir   /home/repositorios

```

3\. Copiar los archivos del CD a /home/repositorios

4\. Ejecutar el comando:

```
 #repo-add /home/repositorios/repositorios.db.tar.gz  /home/repositorios/*

```

5\. Editar el archivo /etc/pacman.conf Comentar todas las líneas de los repositorios current, community y extra

6\. Añadir:

```
[repositorios]
Server=file:///home/repositorios

```

7\. Actualizar pacman

```
 #pacman -S pacman

```

8\. Actualizar todo

```
 #pacman -Syu

```