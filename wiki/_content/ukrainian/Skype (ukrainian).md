## Contents

*   [1 Skype](#Skype)
    *   [1.1 Встановлення Skype](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_Skype)
        *   [1.1.1 Інсталяція на 64-бітних системах](#.D0.86.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D1.8F.D1.86.D1.96.D1.8F_.D0.BD.D0.B0_64-.D0.B1.D1.96.D1.82.D0.BD.D0.B8.D1.85_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B0.D1.85)
    *   [1.2 Звук в Skype](#.D0.97.D0.B2.D1.83.D0.BA_.D0.B2_Skype)
        *   [1.2.1 Skype ALSA Sound (2.0+)](#Skype_ALSA_Sound_.282.0.2B.29)

## Skype

Skype - безкоштовне програмне забезпечення з закритим кодом, що забезпечує шифрований голосовий зв'язок через Інтернет між комп'ютерами (VoIP), а також платні послуги для зв'язку з абонентами звичайної телефонної мережі. Можлива організація конференц-зв'язку (до 25 абонентів, включаючи ініціатора), передача текстових повідомлень і файлів, а також відеозв'язок.

### Встановлення Skype

Для інсталювання Skype ви повинні в файлі /etc/pacman.conf додати репозиторій [community]:

```
[community]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist

```

Тепер можна інсталювати Skype:

```
# pacman -S skype

```

#### Інсталяція на 64-бітних системах

Skype пропонується тільки в якості пакета для 32-бітних систем, і тому не існує пакетів в офіціальних репозиторіях для x86_64\. Попри це, Ви можете інсталювати 32-bit Skype з AUR, або Ви можете інсталювати його вручну, виконавши наступні команды: Спочатку, створюємо робочую директорію:

```
$ cd ~ && mkdir temp-skype-install

```

Видаляемо всі попередні версії Skype:

```
$ sudo rm -rf /usr/share/skype/ && sudo rm -rf /usr/bin/skype

```

Потім, скачуємо Skype:

```
$ wget [http://www.skype.com/go/getskype-linux-beta-static](http://www.skype.com/go/getskype-linux-beta-static) 
$ tar xvf skype_static-2.1.0.81.tar.bz2 && cd skype_static-2.1.0.81 

```

**Note:** Користувачі **Kopete**, хто хоче використовувати Skype API повинні отримати динамічно зв’язані пакети.

Інсталюємо Skype:

```
$ sudo mkdir /usr/share/skype/ 
$ sudo mv avatars/ /usr/share/skype/ 
$ sudo mv icons/ /usr/share/skype/ 
$ sudo mv lang/ /usr/share/skype/ 
$ sudo mv sounds/ /usr/share/skype/ 
$ sudo mv skype /usr/bin/ 

```

Та видаляемо робочу директорію:

```
$ cd ~ && rm -rf temp-skype-install

```

**Note:** Ви можете використати сценарій, котрий робить усе вище описане автоматично: $ wget [http://tinyurl.com/arch-skype-install](http://tinyurl.com/arch-skype-install) -O-

**Note:** Також Вам необхідні 32-bit бібліотеки, які можна отримати: # pacman -S lib32

### Звук в Skype

Останні версії Skype (2,0 +) мають вбудовану підтримку ALSA, більш ранні версії підтримують тільки застарілі OSS.

#### Skype ALSA Sound (2.0+)

В ідеалі, звук повинен працювати "з коробки", якщо ви не можете вибрати звуковий пристрій для використання в Skype або якщо Ви маєте проблеми зі Skype: він блокує звуковий пристрій, то Вам потрібно тільки додадти наступні строки в Ваш ~/.asoundrc :і

```
  pcm.dmixout {
  # Just pass this on to the system dmix
  type plug
  slave {
     pcm "dmix"
    }
  }

```

Після цього Вы можете запустити Skype, піти в опції аудіо та оберіть dmixout в якості оратора і ringing device.