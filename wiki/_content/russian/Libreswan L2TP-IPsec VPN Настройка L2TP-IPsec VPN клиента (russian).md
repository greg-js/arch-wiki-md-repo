Данная статья описывает установку клиента VPN L2TP/IPsec для последующей настройки соединения через интерфейс NetworkManager.

## Установка

Установите следующие пакеты:

xl2tpd [xl2tpd](https://www.archlinux.org/packages/?name=xl2tpd) libreswan [libreswan](https://aur.archlinux.org/packages/libreswan/) networkmanager-l2tp [networkmanager-l2tp](https://aur.archlinux.org/packages/networkmanager-l2tp/)

В настоящий момент (август 2018) есть проблема с PGP подписью для пакета networkmanager-l2tp - надо либо имортировать ключи или ставить вручную через makepkg --skippgpcheck -sri

Далее перезапускаем NetworkManager **sudo systemctl restart NetworkManager** и выбираем добавить новое L2TP соединение, настраиваем, как того требует сервер. Обычно, это указание логина и пароля для L2TP и IPsec-settings -> pre-shared key.