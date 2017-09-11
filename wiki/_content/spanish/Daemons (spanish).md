Un [demonio](https://en.wikipedia.org/wiki/es:Demonio_(inform%C3%A1tica) es un programa que se ejecuta en segundo plano, esperando a que ocurran determinados eventos y ofreciendo servicios. Un buen ejemplo de ello es un servidor web que espera una solicitud para entregar una página o un servidor ssh esperando a alguien tratando de conectarse. Si bien estas son aplicaciones con una amplia funcionalidad, hay demonios cuyo trabajo no es tan visible. Los demonios sirven para tareas como escribir mensajes en un archivo de registro (por ejemplo, `syslog`, `metalog`) o mantener la hora precisa del sistema (por ejemplo [`ntpd`](/index.php/Network_Time_Protocol_daemon_(Espa%C3%B1ol) "Network Time Protocol daemon (Español)")). Para obtener más información consulte [daemon(7)](http://jlk.fjfi.cvut.cz/arch/manpages/man/daemon.7).

**Nota:** El término demonio es, a veces, utilizado para una clase de programas que se inician en el arranque, pero que no son procesos que permanecen en la memoria. Se les llama demonios simplemente porque utilizan la misma estructura de arranque/parada (por ejemplo, archivos de servicios de systemd como *Type oneshot*) usada para iniciar los demonios tradicionales. Por ejemplo, los archivos de servicio `alsa-store` y `alsa-restore` proporcionan apoyo para una configuración permanente, pero no inician procesos adicionales en segundo plano a las solicitudes del servicio ni responden a eventos.

Desde la perspectiva del usuario, la distinción no suele ser significativa, a menos que el usuario trata de buscar el «demonio» en una lista de procesos.

## Gestionar los demonios

En Arch Linux, los demonios son administrados por [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)"). La orden [systemctl](/index.php/Systemd_(Espa%C3%B1ol)#Uso_b.C3.A1sico_de_systemctl "Systemd (Español)") es la interfaz de usuario que se utiliza para su gestión. Los archivos se leen como *<nombre_servicio>*.service que contienen información acerca de cómo y cuándo iniciar el demonio asociado. Los archivos de servicios se guardan en `/{etc,usr/lib,run}/systemd/system`. Véase [systemd (Español)#Usar las unidades](/index.php/Systemd_(Espa%C3%B1ol)#Usar_las_unidades "Systemd (Español)") para obtener información completa acerca del uso systemctl para gestionar los demonios.

## Lista de demonios

Véase la [lista de demonios](/index.php/Daemons_List_(Espa%C3%B1ol) "Daemons List (Español)") para conocer una lista de demonios con relación al nombre del servicio y el antiguo script rc.d.

## Véase también

*   [systemd](/index.php/Systemd_(Espa%C3%B1ol) "Systemd (Español)")