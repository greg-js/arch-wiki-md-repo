Из [Википедии](https://ru.wikipedia.org/wiki/VNC):

	*Virtual Network Computing (VNC) — система удалённого доступа к рабочему столу компьютера, использующая протокол RFB (англ. Remote FrameBuffer, удалённый кадровый буфер). Управление осуществляется путём передачи нажатий клавиш на клавиатуре и движений мыши с одного компьютера на другой и ретрансляции содержимого экрана через компьютерную сеть.*

Для повышения безопасности VNC может быть передан через [SSH](/index.php/SSH_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SSH (Русский)") (Secure Shell).

Имеется несколько серверов VNC, доступных в том числе в Arch:

*   [TigerVNC](/index.php/TigerVNC "TigerVNC")

*   [TightVNC](/index.php/TightVNC "TightVNC")

*   [x11vnc](/index.php/X11vnc "X11vnc")

*   [vino](/index.php/Vino "Vino")

*   vinagre

Клиенты:

*   [Remmina](/index.php/Remmina "Remmina")

*   [TightVNC](/index.php/TightVNC "TightVNC")

Для получения всего списка связанных с VNC программ наберите:

```
$ pacman -Ss vnc

```

## See also

*   [xrdp](/index.php/Xrdp "Xrdp"), демон, запускающий интерфейс RDP