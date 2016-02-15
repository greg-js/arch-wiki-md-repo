Щоб вимкнути комп'ютер кнопкою Power потрібно:

Встановити пакунок **acpid**.
Додайте **acpid** в список демонів (DAEMONS) в _/etc/rc.conf_.
Створіть в _/etc/acpi/events/_ файл **power** з таким змістом:

```
# /etc/acpi/events/power
# This is called when the user presses the power button

event=button/power (PWR.||PBTN)
action=/sbin/poweroff

```

Тепер запустіть демон **acpid** (виконайте _/etc/rc.d/acpid start_)

Тепер після легкого натиснення на кнопку Power (не кілька секунд) система повинна вимкнутися. Зауважте, якщо у вас налаштований і працює **hibernate**, ви можете змінити останній рядок на

```
action=/sbin/hibernate

```

Однак, якщо ви використовуєте більш складний віконний менеджер (WM), краще використати його метод вимикання системи для збереження сесій, тощо.

Для KDE достатньо змінити _action_ на

```
/opt/kde/bin/dcop --all-users --all-sessions ksmserver ksmserver logout 0 2 0

```

Для XFCE змініть _action_ на

```
echo POWEROFF | /usr/lib/xfce4/xfsm-shutdown-helper 

```