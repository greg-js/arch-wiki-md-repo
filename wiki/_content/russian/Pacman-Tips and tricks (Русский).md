## Contents

*   [1 Раскраска вывода Pacman'a](#.D0.A0.D0.B0.D1.81.D0.BA.D1.80.D0.B0.D1.81.D0.BA.D0.B0_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4.D0.B0_Pacman.27a)
    *   [1.1 Скрипты](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D1.8B)
    *   [1.2 Альтернатива](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.B0)
    *   [1.3 Использование 'acoc'](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.27acoc.27)
    *   [1.4 Альтернатива](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.B0_2)
*   [2 Custom local repository](#Custom_local_repository)

## Раскраска вывода Pacman'a

Кому и зачем это нужно? Менеджер пакетов [Gentoo](http://www.gentoo.org/) - 'portage' - широко использует эту возможность, что значительно повышает восприятие выводимой информации, наблюдать эффект можно здесь: [screenshot](http://gentoo-portage.com/up_img/1026.png)

#### Скрипты

Пользователи citral используют следующий скрипт в своём .bashrc:

```
alias pacs="pacsearch"
pacsearch () {
       echo -e "$(pacman -Ss $@ | sed \
       -e 's#core/.*#\\033[1;31m&\\033[0;37m#g' \
       -e 's#extra/.*#\\033[0;32m&\\033[0;37m#g' \
       -e 's#community/.*#\\033[1;35m&\\033[0;37m#g' \
       -e 's#^.*/.* [0-9].*#\\033[0;36m&\\033[0;37m#g' )"
}

```

Это проверенное решение. Впрочем, если вы решите использовать всесистемное решение, выполните **root**:

```
 touch /usr/bin/pacs && chmod 755 /usr/bin/pacs

```

и затем вставьте это в /usr/bin/pacs как root:

```
 #!/bin/bash
 echo -e "$(pacman -Ss $@ | sed \
 -e 's#core/.*#\\033[1;31m&\\033[0;37m#g' \
 -e 's#extra/.*#\\033[0;32m&\\033[0;37m#g' \
 -e 's#community/.*#\\033[1;35m&\\033[0;37m#g' \
 -e 's#^.*/.* [0-9].*#\\033[0;36m&\\033[0;37m#g' )"

```

You can substitute "pacs" in these lines for anything you like. You can also alias "pacs" to something else in your .bashrc, as done above.

Using these commands is straightforward; simply use your new command instead of 'pacman', the rest is still the same!

#### Альтернатива

Альтернативой является использование этого python-скрипта, который эмулирует вывод pacman -Ss (с цветом!), но получает список пакетов из интернета. Он ищет в официальных репозиториях и AUR (community и unsupported).

```
#!/usr/bin/python

import os
import re
import sys
import urllib2

OFFICIAL_QUERY = "[https://archlinux.org/packages/search/\?q=](https://archlinux.org/packages/search/\?q=)"
AUR_QUERY = "[https://aur.archlinux.org/packages.php?K=](https://aur.archlinux.org/packages.php?K=)"

# Repos and colors
repos = {"Core":'32',"Extra":'36',"Testing":'31',"community":'33',"unsupported":'35'}

def strip_html(buffer):
    buffer = re.sub('<[^>]*>','',buffer)
    buffer = re.sub('(?m)^[ \t]*','',buffer)
    return buffer

def cut_html(beg,end,buffer):
    buffer = re.sub('(?s).*' + beg,'',buffer)
    buffer = re.sub('(?s)' + end + '.*','',buffer)
    return buffer

class RepoSearch:
    def __init__(self,keyword):
        self.keyword = keyword
        self.results = ''
        for name in ['official','aur']:
            self.get_search_results(name)
            self.parse_results(name)
        self.colorize()

    def get_search_results(self,name):
        if name == "official":
            query = OFFICIAL_QUERY
        elif name == "aur":
            query = AUR_QUERY

        f = urllib2.urlopen( query + self.keyword )
        self.search_results = f.read()
        f.close()

    def preformat(self,header,a,b):
        self.buffer = cut_html('<table class=\"' + header + '\"[^>]*>','</table',self.search_results)
        self.buffer = strip_html(self.buffer)
        self.buffer = self.buffer.split('
')
        self.buffer = [line for line in self.buffer if line]
        del self.buffer[a:b]

    def parse_results(self,name):
        self.buffer = ''
        if name == 'official':
            if re.search('<table class=\"results\"',self.search_results):
                self.preformat('results',0,6)
            elif re.search('<div class=\"box\">',self.search_results):
                temp = re.search('<h2 class=\"title\">([^<]*)</h2>',self.search_results)
                temp = temp.group(1)
                temp = temp.split()
                self.preformat('listing',7,-1)
                for i in range(0,3): del self.buffer[i]
                for i in temp: self.buffer.insert(temp.index(i) + 2,i)

        elif name == 'aur':
            p = re.compile('<td class=.data[^>]*>')
            self.buffer = self.search_results.split('
')
            self.buffer = [strip_html(line) for line in self.buffer if p.search(line)]

        l = len(self.buffer)/6
        parsed_buf = ''

        for i in range(l):
            parsed_buf += self.buffer[i*6] + '/'
            parsed_buf += self.buffer[i*6+1] + ' '*(24-len(self.buffer[i*6] + self.buffer[i*6+1]))
            parsed_buf += self.buffer[i*6+2]
            if name == "official":
                parsed_buf += ' ' + self.buffer[i*6+3]
            parsed_buf += '
' + self.buffer[i*6+4] + '
'

        self.results += parsed_buf

    def colorize(self):
        for repo,repo_color in repos.iteritems():
            self.results = re.sub(repo + '/.*','\\033[1;' + repo_color + 'm' + '\g<0>' + '\\033[0;0m',self.results)

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print "Usage: " + sys.argv[0] + " <keyword>"
        sys.exit(2)
    reposearch = RepoSearch(sys.argv[1])
    sys.stdout.write(reposearch.results)

```

#### Использование 'acoc'

Это другой способ произвольного раскрашивания командного вывода. Вы можете загрузить небольшую [Ruby](http://www.ruby-lang.org/en/) утилиту [acoc](http://raa.ruby-lang.org/project/acoc/) ( её зависимости, [term-ansicolor](http://raa.ruby-lang.org/project/ansicolor/) и [tpty](http://raa.ruby-lang.org/cache/ruby-tpty/). ). tpty не является зависимостью, но некоторые приложения, например "ls", не будут работать с acoc (они должны быть запущены в терминале (или в псевдотерминале, в этом случае), иначе они ведут себя по-другому).

Установка сравнительно проста:

```
$ tar xvzf tpty-0.0.1.tar.gz
$ cd tpty-0.0.1
$ ruby extconf.rb
$ make
$ ruby ./test.rb
# make install

```

```
$ tar xvzf term-ansicolor-1.0.1.tar.gz
$ cd term-ansicolor-1.0.1
# ruby install.rb

```

А теперь acoc:

```
$ tar xvzf acoc-0.7.1.tar.gz
$ cd acoc-0.7.1
# make install

```

Теперь всего-лишь прочитайте раздел "Advanced Installation" в файле INSTALL и настраивайте acoc по своему усмотрению. Создайте ссылку для 'pacman' также, так как это, прежде всего то, для чего мы всё это делаем. Как только acoc запустится, вы можете добавить эти строки в acoc.conf:

```
[pacman -Si]
/^Name\s+:\s([\w.-]+)/                              bold
[pacman -Qi]
/^Name\s+:\s([\w.-]+)/                              bold
[pacman -Qi$]
/^([\w.-]+)\s([\w.-]+)/                 bold,clear
[pacman -Ss]
/^([\w.-]+)\/([\w.-]+)\s+([\w.-]+)/     clear,bold,clear
[pacman -Qs]
/^([\w.-]+)\/([\w.-]+)\s+([\w.-]+)/     clear,bold,clear
[pacman -Sl]
/^([\w.-]+)\s([\w.-]+)\s([\w.-]+)/              clear,bold,clear
[pacman -Qo]
/^([\w.-\/]+)\sis\sowned\sby\s([\w.-]+)\s([\w.-]+)/     clear,bold,clear
[pacman -Qe$]
/^([\w.-]+)\s([\w.-]+)/                 bold,clear
[pacman -Qg$]
/^([\w.-]+)\s([\w.-]+)/                 clear,bold

```

Вероятно, это не совершенство, и выглядит не очень красиво, но я нахожу это очень удобным. Строки, указанные выше, "заставляют" список пакетов pacman выводить жирным шрифтом, что помогает при выводе, например, "pacman -Ss xfce". Если вы хотите сделать вывод более цветным, всё в ваших руках :-). Прочтите документацию acoc, включаемую в пакет для большей информации.

#### Альтернатива

В AUR доступен [PKGBUILD](https://aur.archlinux.org/packages.php?do_Details=1&ID=11827) с патчем цветного вывода от Vogo.

## Custom local repository

В [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") 3 появился новый скрипт repo-add, который делает генерацию собственного локального репозитория еще проще. Используйте **repo-add --help** для больших подробностей по его использованию.

При помощи этого скрипта очень легко поддерживать состояние вашей базы данных в актуальном состоянии. Просто сохраните все пакеты, которые вы хотите положить в свой репозиторий, в одной папке, перейдите в эту папку, и запустите следующую команду:

```
repo-add /path/to/repo.db.tar.gz *.pkg.tar.xz

```

где 'repo' - это имя вашего собственного репозитория. Последний аргумент добавляет все pkg.tar.xz файлы к вашему репозиторию, так что будьте внимательны, если вы имеете несколько разных версий одного и того же пакета в вашей папке. Неизвестно какая версия попадет в репозиторий, но попадет только одна!

Для добавления нового пакета (и удаления старого, если он есть) просто запустите:

```
repo-add /path/to/repo.db.tar.gz packagetoadd-1.0-1-i686.pkg.tar.xz

```

Если есть пакет, который вы не хотите видеть в репозитории, читайте **repo-remove --help**.

При желании вы можете добавить репозиторий (директорию, содержащую пакеты и файл db.tar.gz) на ftp (или nfs) сервер машины.

Добавьте репозиторий в ваш **pacman.conf**. Именем репозитория должно быть имя файла db.tar.gz. Вы можете сослаться непосредственно на него, используя синтаксис **file://** или обратиться по ftp: **~[ftp://localhost/path/to/directory](ftp://localhost/path/to/directory)**

**Не забудьте добавить ваш собственный репозиторий в наш [список неофициальных пользовательских репозиториев](/index.php/Unofficial_user_repositories "Unofficial user repositories") для того чтобы другие пользователи могли найти и установить ваши пакеты!**