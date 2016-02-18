## Contents

*   [1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Основы](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D1.8B)
    *   [2.1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [2.2 Монтирование](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [2.3 Применение](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [2.4 Удаление](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [2.5 Backup](#Backup)
*   [3 Advanced](#Advanced)
    *   [3.1 PAM Mount](#PAM_Mount)

# Введение

В статье описывается базовое использование [eCryptfs](https://launchpad.net/ecryptfs). Статья проведёт вас через процесс установки зашифрованной домашней директории, в которой вы можете хранить личные/секретные данные. Если вы не уверены, нужно ли вам шифрование, прочтите сначала [dm-crypt](/index.php/System_Encryption_with_LUKS_for_dm-crypt "System Encryption with LUKS for dm-crypt").

Реализация eCryptfs отличается от реализации dm-crypt, которая шифрует блочное устройство полностью, а eCryptfs шифрует вайловую систему - тоесть каждый файл поотдельности. О сравнении двух методов шифрования можно прочитать на [[1]](http://ecryptfs.sourceforge.net/ecryptfs-faq.html#compare).

Если коротко, то eCryptfs не нуждается в резервировании места на диске(создание специального раздела). eCryptfs может быть смонтирован в любую директорию и шифровать её содержимое(например домашняя директория! пользователя или любая директория в сети). Все метаданные для расшифровки хранятся в заголовках файлов, поэтому зашифрованые файлы можно перемещать, копировать, делать резервные копии. Есть и другие плюсы данного метода, как и минусы. Самый большой минус - eCryptfs не может шифровать весь раздел/жёсткий диск. По этому eCryptfs не может зашифровать раздел swap(но вы можете комбинировать eCryptfs и dm-crypt).

# Основы

eCryptfs входит в ядро с версии 2.6.19, но для работы с ней, вам нужны дополнительные инструменты: [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils) и [keyutils](https://www.archlinux.org/packages/?name=keyutils).

После установки загрузите модуль ядра:

```
# modprobe ecryptfs

```

Пакет ecryptfs-utils нужен для управления ключами для доступа к зашифрованым данным. Некоторые скрипы из этого пакета помогут автоматизировать весь процесс (*ecryptfs-setup-private*) или помут в комбинировании eCryptfs и dm-crypt для шифрования раздела swap. Мы не будем использовать эти скрипты, а сделаем всё в ручном режиме для лучшего понимания принципа работы данного метода.

Прежде чем мы начнём, я советую вам прочитать документацию по eCryptfs(man).

## Установка

Для начала создайте директории, которые вы хотите зашифровать. В этом примере мы назовём директорию - Private.

```
$ su -
# mkdir -m 700 /home/username/.Private
# mkdir -m 500 /home/username/Private
# chown username:username /home/username/{.Private,Private}

```

В сумме получается:

*   Зашифрованые данные будут храниться в ~/.Private
*   Когда эта директория смонтированна, данные будут доступны в ~/Private
    *   Когда директория не смонтированна, данные в неё не могут быть записаны
    *   Когда директория смонтированна, права доступа к ней такие-же как и у ~/.Private

eCryptfs может быть смонтированны поверх ~/Private.

```
# mount -t ecryptfs /home/username/.Private /home/username/Private

```

Вам нужно будет ввести пароль и выбрать некоторые опции с которыми директория будет монтироватся в будущем. Так-же вы можете задать несколько различных ключей для шифрования различных данных(об этом ниже). Для краткости мы опишем процесс с одним ключём. Пример:

```
Key type: passphrase
Passphrase: ThisIsAVeryWeakPassphrase
Cypher: aes
Key byte: 16
Plaintext passtrough: no
Filename encryption: no
Add signature to cache: yes 

```

В сумме получается:

*   Ваш ключ это ваша так называемая **mount passphrase** хранится в виде хэша+соль.
    *   По теминологии eCryptfs этот ключ называется "file encryption key, encryption key", или **fekek**.
*   eCryptfs поддерживает несколько методов шифрования AES, blowfish, twofish...

*   Plaintext passtrough разрешает сохранять и работать с **не зашифрованными данными** внутри ~/.Private.
*   Шифрование файловой ситемы доступно с версии ядра 2.6.29.
    *   По теминологии eCryptfs этот ключ, который служит для шифрования имён файлов называется "filename encryption key" или **fnek**
*   Сигнатура ключа(ей) хранится в `/root/.ecryptfs/sig-cache.txt`.

Т.к. мы хотим монтировать директории без прав супер-пользователя, нам нужно переместить директорию с конфигурацией eCryptfs в нашу домашнюю директорию и сделать нас её владельцем:

```
# mv /root/.ecryptfs /home/username
# chown username:username /home/username/.ecryptfs

```

Установка на этом законченна и директория смонтирована. Вы можете размещать любые файлы в ~/Private и они будут прозрачно зашифрованы. Теперь отмонтируйте директорию и если вы попробуете прочитать содетжимое файлов, вы увидете, что они зашифрованы. Как получить к ним доступ? Смотрите следующий шаг.

## Монтирование

Когда вам снова понадобятся ваши файлы, вы можете повторить процедуру монтирования описанную выше ислпользую тот-же ключ и опции.

Каждый раз проделывать эти операции может быть утомительно. Вариант номер один: передать все опции команде монтирования кроме ключа.

```
$ sudo mount -t ecryptfs /home/username/.Private /home/username/Private -o ecryptfs_cipher=aes,ecryptfs_key_bytes=16,key=passphrase

```

Вариант номер два(рекомендован): добавить строку в **`/etc/fstab`**:

```
# eCryptfs mount points
/home/username/.Private /home/username/Private ecryptfs rw,user,noauto,ecryptfs_sig=XY,ecryptfs_cipher=aes,ecryptfs_key_bytes=16,ecrypfs_unlink_sigs 0 0

```

ПРИМЕЧАНИЕ:

*   Параметр **user** позволяет монтирование с ограничеными правами
*   В параметре **ecryptfs_sig** замените строку *XY* значением сигнатуры (можно взять из **mtab** или `sig-cache.txt`)
*   Если было разрешено шифрование имён файлов, то нужно поставить дополнительный параметр монтирования **ecryptfs_fnek_sig**=*XY*, где *XY* тоже значение сигнатуры, что и в параметре **ecryptfs_sig**
*   Последний параметр **ecrypfs_unlink_sigs** говорит о том, что при размонтировании ключ из брелка будет удалён

Поскольку в процессе размонтирования ключ удаляется из брелка ядра, то для последующего монтировании там необходимо заново создать ключ. Для этого используется утилиты **ecryptfs-add-passphrase** или **ecryptfs-manager**:

После ввода пароля шифрования можно произвести монтирование:

```
$ ecryptfs-add-passphrase
  Passphrase: ThisIsAVeryWeakPassphrase
$ mount -i /home/username/Private

```

Обратите внимание на параметр **`-i`**. Он предотвращает вызов помощника монтирования. Это означает, что при использовании параметра `-i` по умолчанию при монтировании будут применены параметры **nosuid, noexec** and **nodev**. Если в шифрованой папке необходимо иметь также и исполняемые файлы, то можно добавить параметр **exec** в файле fstab в строке команды.

Не лишне также будет вспомнить об утилите **keyctl**, входящую в состав пакета *keyutils*, установленного ранее. Она может быть использована для более продвинутого управления ключами. Нижеследующий пример демонстрирует команду для отображения списка имеющихся ключей и команду для очистки этого списка:

```
$ keyctl list @u
$ keyctl clear @u

```

## Применение

Помимо использования шифрованой папки для хранения критичных файлов и прочих данных не для чужих глаз, можно так же хранить и данные приложений. К примеру *Firefox* имеет не только встроеный менеждер паролей, но и историю посещений и кэш страниц, что может представлять уязвимость. Меры защиты очень просты:

```
 $ mv ~/.mozilla ~/Private/mozilla
 $ ln -s ~/Private/mozilla ~/.mozilla

```

## Удаление

Удаление зашифрованой папки производится после её размонтирования. Если содержащиеся в ней файлы нужно сохранить, то это делается перед её размонтированием.

## Backup

Setup explained here separates the directory with encrypted data from the mount point, so the encrypted data is available for backup at any time. With an overlay mount (i.e. *~/Secret* mounted over *~/Secret*) the lower, encrypted, data is harder to get to. Today when cronjobs and other automation software do automatic backups the risk of leaking your sensitive data is higher.

We explained earlier that all cryptographic metadata is stored in the headers of files. You can easily do backups, or incremental backups, of your **~/.Private** directory, treating it like any other directory.

# Advanced

This wiki article covers only the basic setup of a private encrypted directory. There is however another article about eCryptfs on Arch Linux, which covers encryption of your entire $HOME and encrypting swap space without breaking hibernation (suspend to disk).

That article includes many more steps (i.e. using PAM modules and automatic mounting) and the author was opposed to replicating it here, because there is just no single "right" way to do it. The author proposes some solutions and discusses the security implications, but they are his solutions and as such might not be the best nor are they endorsed by the eCryptfs project in any way.

```
Article: [eCryptfs and $HOME](http://sysphere.org/~anrxc/j/articles/ecryptfs/index.html) by Adrian C. (anrxc).

```

## PAM Mount

The above "*eCryptfs and $HOME*" article uses a shell init file to mount the home directory. The same can be done using [pam_mount](https://www.archlinux.org/packages/?name=pam_mount) with the added benefit that home is un-mounted when all sessions are logged out. As eCryptfs needs the `-i` switch, the *lclmount* setting will need to be changed. I use the following in `/etc/security/pam_mount.conf.xml`:

```
<lclmount>mount -i %(VOLUME) "%(before=\"-o\" OPTIONS)"</lclmount>

```

Remember to also set the volume definition (preferably to `~/.pam_mount.conf.xml` and uncomment luserconf).

```
<pam_mount>
<volume noroot="1" fstype="ecryptfs" path="/home/user/.Private" mountpoint="/home/user"/>
</pam_mount>

```

*noroot* is needed (at least in my configuration) because the encryption key will be added to the user's keyring.

To avoid wasting time needlessly unwrapping the passphrase you can create a script that will check *pmvarrun* to see the number of open sessions:

```
#!/bin/sh
#
#    /usr/local/bin/doecryptfs

exit $(/usr/sbin/pmvarrun -u$PAM_USER -o0)

```

With the following line added before the eCryptfs unwrap module in your PAM stack:

```
auth    [success=ignore default=1]    pam_exec.so     quiet /usr/local/bin/doecryptfs
auth    required                      pam_ecryptfs.so unwrap

```

The article suggests adding these to `/etc/pam.d/login`, but the changes will need to be added to all other places you login, such as `/etc/pam.d/kde`.