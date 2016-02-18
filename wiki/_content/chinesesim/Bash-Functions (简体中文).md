从笔记 (note taker) 得到启发，一个小的 todo 脚本

```
todo() {
   test -f $HOME/.todo || touch $HOME/.todo
   if test $# = 0
   then 
           cat $HOME/.todo
   elif test $1 = -l
   then
           cat -n $HOME/.todo
   elif test $1 = -c
   then
           > $HOME/.todo
   elif test $1 = -r
   then
           cat -n $HOME/.todo
           echo -ne "----------------------------
Type a number to remove: "
           read NUMBER
           sed -ie ${NUMBER}d $HOME/.todo
   else
           echo $@ >> $HOME/.todo
   fi
}

```

一个小的笔记(note taker)

```
note ()
{
       #if file doesn't exist, create it
       [ -f $HOME/.notes ] || touch $HOME/.notes
       #no arguments, print file
       if [ $# = 0 ]
       then
               cat $HOME/.notes
       #clear file
       elif [ $1 = -c ]
       then
               > $HOME/.notes
       #add all arguments to file
       else
               echo "$@" >> $HOME/.notes
       fi
}

```

解压缩函数，另外你也可以使用 atool (在 [community] 仓库中)

```
extract() {
 local e=0 i c
 for i; do
   if [ -f $i && -r $i ]; then
       c=
       case $i in
         *.tar.bz2) c='tar xjf'    ;;
         *.tar.gz)  c='tar xzf'    ;;
         *.bz2)     c='bunzip2'    ;;
         *.gz)      c='gunzip'     ;;
         *.tar)     c='tar xf'     ;;
         *.tbz2)    c='tar xjf'    ;;
         *.tgz)     c='tar xzf'    ;;
         *.7z)      c='7z x'       ;;
         *.Z)       c='uncompress' ;;
         *.exe)     c='cabextract' ;;
         *.rar)     c='unrar x'    ;;
         *.xz)      c='unxz'       ;;
         *.zip)     c='unzip'      ;;
         *)     echo "$0: cannot extract \`$i': Unrecognized file extension" >&2; e=1 ;;
       esac
       [ $c ] && command $c "$i"
   else
       echo "$0: cannot extract \`$i': File is unreadable" >&2; e=2
   fi
 done
 return $e
}

```

```
docview ()
{
  if [ -f $1 ] ; then
      case $1 in
          *.pdf)       xpdf $1    ;;
          *.ps)        oowriter $1    ;;
          *.odt)       oowriter $1     ;;
          *.txt)       leafpad $1       ;;
          *.doc)       oowriter $1      ;;
          *)           echo "don't know how to extract '$1'..." ;;
      esac
  else
      echo "'$1' is not a valid file!"
  fi
}

```

计算器

```
calc() { echo "scale=3;$@" | bc -l ; }

```

Kingbash - 菜单驱动的自动完成 (参见 [https://bbs.archlinux.org/viewtopic.php?id=101010](https://bbs.archlinux.org/viewtopic.php?id=101010))

从[AUR](/index.php/AUR "AUR")安装[kingbash](https://aur.archlinux.org/packages/kingbash/) 然后插入下面的代码到 .bashrc

```
function kingbash.fn() {
  echo -n "KingBash> $READLINE_LINE" #Where "KingBash> " looks best if it resembles your PS1, at least in length.
  OUTPUT=`/usr/bin/kingbash "$(compgen -ab -A function)"`
  READLINE_POINT=`echo "$OUTPUT" | tail -n 1`
  READLINE_LINE=`echo "$OUTPUT" | head -n -1`
  echo -ne "\r\e[2K"; }
bind -x '"\t":kingbash.fn'

```