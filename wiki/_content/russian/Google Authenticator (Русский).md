Проект [Google Authenticator project](http://code.google.com/p/google-authenticator/) обеспечивает возможность двухфакторной аутентификации посредством одноразовых паролей ([OTP](http://ru.wikipedia.org/wiki/%D0%9E%D0%B4%D0%BD%D0%BE%D1%80%D0%B0%D0%B7%D0%BE%D0%B2%D1%8B%D0%B9_%D0%BF%D0%B0%D1%80%D0%BE%D0%BB%D1%8C)). Генератор OTP доступен для iOS, Android и Blackberry. Подобно [S/KEY_Authentication](/index.php/S/KEY_Authentication "S/KEY Authentication"), механизм аутентификации интегрируется в систему Linux PAM. Это руководство объясняет установку и настройку этого механизма.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка PAM](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_PAM)
*   [3 Генерация секретного файла ключа](#.D0.93.D0.B5.D0.BD.D0.B5.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D1.81.D0.B5.D0.BA.D1.80.D0.B5.D1.82.D0.BD.D0.BE.D0.B3.D0.BE_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.D0.BA.D0.BB.D1.8E.D1.87.D0.B0)
*   [4 Настройка генератора OTP](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B3.D0.B5.D0.BD.D0.B5.D1.80.D0.B0.D1.82.D0.BE.D1.80.D0.B0_OTP)
*   [5 Проверка](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0)

## Установка

Программа доступна через [AUR](/index.php/AUR "AUR") в виде пакета [google-authenticator-libpam-git](https://aur.archlinux.org/packages/google-authenticator-libpam-git/).

## Настройка PAM

**Важно:** Если вы конфигурируете через SSH - не закрывайте сессию, не проверив, что всё работает, иначе вы можете заблокировать себе доступ! Также: сгенерируйте файл ключа перед активацией PAM.

Обычно двухфакторная аутентификация нужна только для удалённого входа. Соответствующий файл конфигурации - `/etc/pam.d/sshd`. В случае, если Вы хотите использовать Google Authenticator глобально - необходимо изменить файл `/etc/pam.d/system-auth` - будьте внимательны, чтобы не лишить себя доступа. В этом руководстве мы будем менять файл `/etc/pam.d/sshd` в рамках локальной сессии, что более безопасно (хотя и не обязательно).

Для запроса unix-пароля и OTP добавьте `pam_google_authenticator.so` в `/etc/pam.d/system-auth`:

```
 auth            required        pam_google_authenticator.so
 auth            required        pam_unix.so
 auth            required        pam_env.so

```

В результате, будет запрашиваться сначала OTP, потом - Ваш unix-пароль. Изменение порядка модулей изменит и порядок запроса паролей.

**Важно:** Вход посредством ssh будет доступен только пользователям, сгенерировавшим файл ключа (см. ниже).

Чтобы разрешить вход с помощью OTP или unix-пароля, напишите следующее:

```
 auth            sufficient      pam_google_authenticator.so
 auth            sufficient      pam_unix.so
 auth            required        pam_env.so

```

Наконец, включите [аутентификацию "вызов-ответ"](http://ru.wikipedia.org/wiki/%D0%92%D1%8B%D0%B7%D0%BE%D0%B2-%D0%BE%D1%82%D0%B2%D0%B5%D1%82_%28%D0%B0%D1%83%D1%82%D0%B5%D0%BD%D1%82%D0%B8%D1%84%D0%B8%D0%BA%D0%B0%D1%86%D0%B8%D1%8F%29) в файле `/etc/ssh/sshd_config`:

```
 ChallengeResponseAuthentication yes

```

и перезагрузите конфигурацию `sshd`

```
 # systemctl reload sshd

```

## Генерация секретного файла ключа

Чтобы использовать двухфакторную аутентификацию - необходимо сгенерировать секретный ключ в домашней директории. Это легко можно сделать с помощью `google-authenticator` из пакета [google-authenticator-libpam-git](https://aur.archlinux.org/packages/google-authenticator-libpam-git/):

```
   $ google-authenticator
   Do you want authentication tokens to be time-based (y/n) _(Хотим ли мы, чтобы пароль был основан на временной отметке?)_ **y**

   [https://www.google.com/chart?chs=200x200&chld=M%7C0&cht=qr&chl=otpauth://totp/username@hostname%3Fsecret%3DZVZG5UZU4D7MY4DH](https://www.google.com/chart?chs=200x200&chld=M%7C0&cht=qr&chl=otpauth://totp/username@hostname%3Fsecret%3DZVZG5UZU4D7MY4DH)
   Your new secret key is _(секретный ключ для ввода в телефон)_: **ZVZG5UZU4D7MY4DH**

   Your verification code is 269371
   Your emergency scratch codes are _(резервные коды доступа)_:
     70058954
     97277505
     99684896
     56514332
     82717798

   Do you want me to update your "/home/username/.google_authenticator" file (y/n) _(обновить настройки в /home/username/.google_authenticator)?_ **y**

   Do you want to disallow multiple uses of the same authentication
   token? This restricts you to one login about every 30s, but it increases
   your chances to notice or even prevent man-in-the-middle attacks (y/n) 
   _(Запретить использование одного кода несколько раз? Помогает заметить или даже предотвратить атаку man-in-the-middle.)?_ **y**

   By default, tokens are good for 30 seconds and in order to compensate for
   possible time-skew between the client and the server, we allow an extra
   token before and after the current time. If you experience problems with poor
   time synchronization, you can increase the window from its default
   size of 1:30min to about 4min. Do you want to do so (y/n) _(Увеличить окно времени с приблизительно 1.5 минут до 4 минут?)_ **n**

   If the computer that you are logging into isn't hardened against brute-force
   login attempts, you can enable rate-limiting for the authentication module.
   By default, this limits attackers to no more than 3 login attempts every 30s.
   Do you want to enable rate-limiting (y/n) _( Ограничить число попыток логина за промежуток времени?)_ **y**

```

Рекомендуется **сохранить резервные коды доступа в безопасном месте** (например, распечатать и спрятать), потому что это единственный вариант входа по ssh, если вы потеряете свой мобильный телефон. Они также хранятся в `~/.google_authenticator`, так что вы сможете их подглядеть, после успешного логина, разумеется.

## Настройка генератора OTP

Установите OTP-генератор на свой мобильный телефон из магазина приложений или пройдя по ссылке [http://m.google.com/authenticator](http://m.google.com/authenticator). В меню приложения создайте новый аккаунт и отсканируйте QR-код, который сгенерировало приложение google-authenticator на компьютере, или вручную введите секретный ключ, выданный тем же приложением (в примере выше это 'ZVZG5UZU4D7MY4DH').

Теперь вы должны увидеть в телефоне новый пароль, который обновляется каждые 30 секунд.

## Проверка

Подключитесь по ssh с другой машины или окна терминала и проверьте, что всё работает:

```
 $ssh username@hostname
 login as: username
 Verification code:
 Password:
 $

```