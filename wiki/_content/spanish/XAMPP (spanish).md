<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduction](#Introduction)
*   [2 Como instalar](#Como_instalar)
    *   [2.1 AUR](#AUR)
    *   [2.2 Manual](#Manual)
*   [3 Compartiendo sus propios archivos](#Compartiendo_sus_propios_archivos)
*   [4 Vínculos](#Vínculos)

# Introduction

XAMPP es una distribución de Apache fácil de instalar que contiene MySQL, PHP y Perl. Contiene: Apache, MySQL, PHP & PEAR, Perl, ProFTPD, phpMyAdmin, OpenSSL, GD, Freetype2, libjpeg, libpng, gdbm, zlib, expat, Sablotron, libxml, Ming, Webalizer, pdf class, ncurses, mod_perl, FreeTDS, gettext, mcrypt, mhash, eAccelerator, SQLite y IMAP C-Client.

# Como instalar

## AUR

*   Paquete [xampp](https://aur.archlinux.org/packages/xampp/) en el [AUR](/index.php/AUR "AUR")

## Manual

1.  Baje la última versión de [aquí](http://www.apachefriends.org/en/xampp-linux.html#374).
2.  En la terminal corra lo siguiente en la carpeta hacia donde el archivo fue bajado: `sudo tar xvfz xampp-linux-1.7.tar.gz -C /opt` 
3.  Use los siguientes comandos para controlar XAMPP: `sudo /opt/lampp/lampp {start,stop,restart}` 

**NOTA:** Si está corriendo una 64-bit arch, debe instalar <tt>lib32-glibc</tt> y <tt>lib32-gcc-libs</tt>.

 `sudo pacman -S lib32-glibc lib32-gcc-libs` 

# Compartiendo sus propios archivos

El directorio raíz web está ubicado en <tt>/opt/lampp/htdocs/</tt>. Puede o poner sus archivos ahí o hacer un link simbólico (symlink) a una carpeta.

# Vínculos

*   [Sitio XAMPP](http://www.apachefriends.org/es/xampp.html)