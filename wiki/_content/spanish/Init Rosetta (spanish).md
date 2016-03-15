Este artículo muestra el paralelismo existente entre el antiguo [SysVinit](/index.php/SysVinit_(Espa%C3%B1ol) "SysVinit (Español)") y la inicialización actual de [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)").

Advierta que siempre puede omitir las extensiones `.service` y `.target`, especialmente si está editando temporalmente los [parámetros del kernel](/index.php/Kernel_parameters "Kernel parameters") cuando visualiza el menú del gestor de arranque. Esto también lo hace más fácil de recordar.

### Órdenes

| SysVinit | systemd | Información |
|  rc.d {start | stop | restart} daemon  |  systemctl {start | stop | restart} daemon.service  | Cambia el estado del servicio (iniciar, parar, reiniciar). |
|  rc.d list  |  systemctl list-unit-files --type=service  | Lista los servicios. |
|  chkconfig daemon {on | off}  |  systemctl {enable | disable} daemon.service  | Activa/desactiva el servicio. |
|  chkconfig daemon --add  |  systemctl daemon-reload  | Se usa para recargar cuando se crean o modifican configuraciones/scripts. |

### Tabla de Targets

| Runlevel de SysV | Target de systemd | Notas |
| 0 | runlevel0.target, poweroff.target | Detiene el sistema. |
| 1, s, single | runlevel1.target, rescue.target | Modalidad de usuario único. |
| 2, 4 | runlevel2.target, runlevel4.target, multi-user.target | Definidos por el usuario. Preconfigurados a 3. |
| 3 | runlevel3.target, multi-user.target | Multiusuario, no gráfica. Los usuarios, por lo general, pueden acceder al sistema a través de múltiples consolas o a través de la red. |
| 5 | runlevel5.target, graphical.target | Multiusuario y gráfica. Por lo general, cuenta con todos los servicios del nivel de ejecución 3, además de un inicio de sesión gráfica. |
| 6 | runlevel6.target, reboot.target | Reinicia el sistema. |
| emergency | emergency.target | Consola de emergencia. |