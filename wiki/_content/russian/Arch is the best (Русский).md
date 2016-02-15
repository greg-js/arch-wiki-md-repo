"Арч — лучший!" — амбициозный и поражающий своей оригинальностью и изысканностью, одновременно возбуждающий и шокирующий (хотя, возможно, несколько переусложненный) проект, однозначно доказывающий неоспоримое превосходство Arch.

## Contents

*   [1 Немного истории](#.D0.9D.D0.B5.D0.BC.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B8.D1.81.D1.82.D0.BE.D1.80.D0.B8.D0.B8)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Код](#.D0.9A.D0.BE.D0.B4)
*   [4 Переводы](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B2.D0.BE.D0.B4.D1.8B)
*   [5 В разных кодировках](#.D0.92_.D1.80.D0.B0.D0.B7.D0.BD.D1.8B.D1.85_.D0.BA.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0.D1.85)

## Немного истории

Начало проекту было положено в далеком апреле 2008 года участником сообщества Arch Linux [lucke](https://bbs.archlinux.org/profile.php?id=2529) в виде обычного скрипта для командной оболочки, который уже тогда смог предоставить неопровержимое доказательство того, что "Арч — лучший!". Он был представлен миру в [этом посте на форуме](https://bbs.archlinux.org/viewtopic.php?id=47306), восхитив умы множества людей, которые незамедлительно приступили к портированию его на самые разные языки, как программирования, так и естественные, так что каждое человеческое существо на планете могло бы полностью оценить всю пользу от сего революционного открытия.

## Установка

Проект представлен двумя пакетами: [archbest-mod1](https://aur.archlinux.org/packages/archbest-mod1/) и [archisthebest](https://aur.archlinux.org/packages/archisthebest/).

## Код

Проект "Арч — лучший!" ("Arch is the best") портирован на самые разные языки программирования.

**1С:Предприятие 7.7/8/8.1/8.2** — язык программирования, который используется в семействе программ "1С:Предприятие".

```
Предупреждение("Арч - лучший!");

```

**Ada** — язык программирования для критичных и отказоустойчивых систем.

```
with Ada.Text_IO;
use Ada.Text_IO;
procedure ArchIsTheBest is
begin
   Put_Line("Arch is the best!");
end HelloWorld;

```

**APL** — "A Programming Language".

```
'Arch is the best!'

```

**ATS** — функциональный язык программирования, использующий зависимые типы для повышения надежности программ.

```
implement main () = println! "Arch is the best!"

```

**Awk** — интерпретируемый скриптовый Си-подобный язык построчного разбора и обработки входного потока (например, текстового файла) по заданным шаблонам.

```
BEGIN {
   print "Arch is the best!"
}

```

**Befunge** — эзотерический стековый язык, считающийся двумерным. Заявлен как язык общего назначения (в том плане, что "вы вероятно сможете даже написать Hunt the Wumpus на нем").

```
<v"Arch is the best!"0
 <,_@#:

```

**Boo** — объектно-ориентированный, статически-строго-типизированный язык программирования для платформы .NET.

```
print "Arch is the best!"

```

**Bourne shell** — оригинальная программа; должна быть совместима с любой командной оболочкой.

```
#!/bin/sh
echo "Arch is the best!"

```

**Bourne shell (Alternate)** — перенаправьте вывод этой программы в ваш клиент IRC/email/IM. Должно работать в любой оболочке.

```
#!/bin/sh
yes Arch is the best!

```

**Bourne shell (навороченная версия)**

```
 #!/bin/bash
 wget http://wiki.archlinux.org/index.php/Arch_is_the_best -qO-| sed -n ':b;n;s/id="Translations"//;Tb;:d;n;s/id="Encodings"//;t;p;bd'|sed '/<i>.*<\/i>/d;s/<[^>]*>//g'|sed 'N;s/\n/: /;N;N;s/\n//g'

```

или

```
 #!/bin/bash
 curl -s "https://wiki.archlinux.org/index.php?title=Arch_is_the_best&action=raw" | sed -n '/==Translations==/,$p' | sed "s/^'''\(.*\)'''$/* \1:/;t;s/^[^=]/  &/"

```

**brainfuck** — разве имени языка недостаточно для его описания? Ладно, попробуйте понять код.

```
++>++++++>+++++<+[>[->+<]<->++++++++++<]>>.<[-]>[-<++>]
<----------------.---------------.+++++.<+++[-<++++++++++>]<.
>>+.++++++++++.<<.>>+.------------.---.<<.>>---.
+++.++++++++++++++.+.<<+.[-]++++++++++.

```

**C** — обратите внимание на три пробела, используемых для отступа в этом коде! Возможно, в этом есть тайный смысл.

```
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
   puts("Arch is the best!");
   return EXIT_SUCCESS;
}

```

**C#** — объектно-ориентированный язык общего назначения. Разработан для того, чтобы быть простым и современным.

```
using System;
public class ArchIsTheBest
{
   static public void Main ()
   {
      Console.WriteLine ("Arch is the best!");
   }
}

```

**C++** — Arch == Linux++

```
#include <iostream>
#include <cstdlib>
int main ()
{
   std::cout << "Arch is the best!" << std::endl;
   return EXIT_SUCCESS;
}

```

**COBOL** — простой, легковесный язык программирования для домохозяек.

```
    IDENTIFICATION DIVISION.
    PROGRAM-ID.  TheBest.

    PROCEDURE DIVISION.
        DISPLAY "Arch is the best!".
        STOP RUN.

```

**CoffeeScript** — скриптовый язык, который транслируется в JavaScript.

```
alert 'Arch is the best!'

```

**Clojure** — диалект Lisp, который запускается на JVM.

```
(def translations {"english" "Arch is the best!",
                   "german" "Arch ist das Beste!",
                   "australian" "Arch is fair dinkum, mate!",
                   "h4x0r" "arhc 51 7he be57!",
                   "spanish" "¡Arch es el mejor!"})

(defn read-choice []
  (println "\nAvailable languages: ")
  (doall (map #(println (key %)) translations))
  (print "Enter language or Ctrl-c: ") (flush)
  (translations (read-line) :badinput))

(defn arch-is-the-best []
  (loop [choice (read-choice)]
    (case choice
      :badinput (do (print "\nBad input!\n")
                    (recur (read-choice)))
      (do (print "\n" choice "\n")
          (recur (read-choice))))))

```

или

```
(def translations {"english" "Arch is the best!",
                   "german" "Arch ist das Beste!",
                   "australian" "Arch is fair dinkum, mate!",
                   "h4x0r" "arhc 51 7he be57!",
                   "spanish" "¡Arch es el mejor!"
                   "street" "Arch iz da shizzle ma nizzle"})
(while 1
  (println "\nPick a language:\n" (map #(key %) translations) "\n language: ")
  (println (translations (read-line) "Not a valid language")))

```

или

```
(prn "Arch is the best!")

```

**Common Lisp** — протестировано на SBCL. Помощь в интернационализации приветствуется.

```
#!/usr/bin/sbcl --script
(defparameter *best-list* '((English "Arch is the best!")
            (Chinese "Arch, 她出类拔萃!")
          (German "Arch ist das Beste!")
          (Greek "Το Arch είναι το καλύτερο!")))
(defun aitb ()
  (format t "Available languages: ~{~{~@(~a~)~*~}~^, ~}.~%" *best-list*)
  (loop for input = (progn (format t "~&Input the desired language, (or 'quit'): ~%")
                           (force-output)
                           (read-line))
     if (string-equal input "quit")
     do (loop-finish)
     else
     do (let ((language-def
               (assoc input *best-list*
                      :key (lambda (lang) (symbol-name lang))
                      :test #'string-equal)))
          (if language-def
              (format t "~&~A~%" (second language-def))
              (format t "~&Invalid language.~%"))))
  (format t "~&May the Arch be with you!~%"))
(aitb)

```

**Common Lisp (Alternate)** — должен работать с любой реализацией (Clisp, Allegro, SBCL...).

```
(princ "Arch is the best!")

```

**D** — Си-подобный язык с более современным подходом.

```
 import std.stdio : writeln;
 void main()
 {
     writeln("Arch is the best");
 }

```

**Dart** — убийца JavaScript от Google.

```
 main(){
   print('Arch is the best');
 }

```

**Emacs Lisp** — диалект Lisp, используемый текстовыми редакторами GNU Emacs и XEmacs.

```
 (message "Arch is the best!")

```

**Erlang** — многопоточный язык с уборкой мусора и рантайм-средой.

```
-module(arch).
-export([is_the_best/0]).
   is_the_best() -> io:fwrite("Arch is the best!\n").

```

или используя сообщение, передаваемое между процессами

```
 -module(arch).
 -export([ultimate_question/0,the_answer/0]).
 the_answer() ->
     receive
         {Client,who_is_the_best} ->
             Client ! {self(),"Arch is the best!"};
         {Client,_} ->
             Client ! {self(),"Taco Taco Taco!"}
     end,
     the_answer().
 ultimate_question() ->
     Pid = spawn(arch,the_answer,[]),
     Pid ! {self(),who_is_the_best},
     receive
         {Pid,Response} -> io:format("~s~n",[Response])
     end.

```

**F#** — строго-типизированный, функциональный язык, который позволяет писать простой код для решения сложных проблем (и сложный для решения простых).

```
printfn "Arch is the best!"

```

**Factor** — высокоуровневый стековый язык.

```
"Arch is the best" print

```

**FIM++** — интуитивно понятный язык для любителей пони.

```
Dear Princess Celestia: Letter About Arch Linux.
Today I learned:
    I wrote "Arch is the best!".
Your faithful student, Twilight Sparkle

```

**Forth** — стековый язык программирования.

```
." Arch is the best" cr -- kiss way

```

**Fortran95**

```
program arch
   print *,"Arch is the best!"
end program arch

```

**Genie** — современный высокоуровневый язык программирования общего назначения.

```
init
 print "Arch is the best"

```

**Gjs** — Javascript для GNOME, основанный на движке Spidermonkey и фреймворке GObject.

```
#!/usr/bin/env gjs
print ('Arch is the best');

```

**Go** — еще один язык от Гугла, помесь C, C++ и Python.

```
package main

import "fmt"

func main() {
 fmt.Println("Arch is the best!")
}

```

**Haskell** — один из языков, где ввод-вывод прост и неприхотлив.

```
main = putStrLn "Arch is the best!"

```

**HTML** — язык разметки веб-страниц.

```
<!DOCTYPE html>
<html lang='en'>
   <head>
      <title>Arch is the best!</title>
   </head>
   <body>
       <p>Arch is the best!</p>
   </body>
</html>

```

**Io** — чистый объектно-ориентированный язык программирования, вдохновленный Smalltalk, Self, Lua, Lisp, Act1, и NewtonScript.

```
"Arch is the best!" println

```

**Java** — исключительно переносимый язык, который работает практически везде — даже на вашем тостере!

```
public class ArchIsTheBest {
   public static void main(String[] args) {
       System.out.println("Arch is the best!");
   }
}

```

**JavaScript** — также известный как ECMAScript, объектно-ориентированный на основе прототипов скриптовый язык программирования.

```
console.log('Arch is the best!');

```

**JavaScript (в веб-браузере)**

```
alert('Arch is the best!');

```

**LilyPond** — нотный редактор с приятным LaTeX-подобным языком.

```
\version "2.12.3"
\include "english.ly"
\header { title = "Arch is the best!" }
\score
{
   <<
      \relative c' { c4 e g c \bar "||" }
      \addlyrics   { Arch is the best! }
   >>
}

```

**LOLCODE** — почему бы и нет?

```
HAI
CAN HAS STDIO?
VISIBLE "ARCH IS TEH PWNZ LOL!"
KTHXBYE

```

**Lua** — легковесный, расширяемый язык программирования.

```
print "Arch is the best!"

```

**Morpho** — мультипарадигменный язык программирования, поддерживающий процедурный, объектно-ориентированный и функциональный подходы.

```
writeln("Arch is the best!");

```

**Nasm(x86_64) (или yasm)** — обратите внимание, что строка размещена в секции .text, в чем проявляется особое превосходство!

```
;nasm -f elf64 arch.asm
;ld -o arch arch.o
;./arch

section .text
global _start
_start:
mov edx,len
mov ecx,msg
mov ebx,1
mov eax,4
int 0x80
xor ebx,ebx
mov eax,1
int 0x80
msg: db "Arch is the best!",10
len equ $-msg

```

**Nimrod** — портируемый легковесный язык программирования.

```
echo "Arch is the best!"

```

**node.js** — платформа, работающая на движке JavaScript из Chrome для быстрой разработки быстрых и масштабируемых сетевых приложений.

```
console.log('Arch is the best!');

```

**Objective-C** — объектно-ориентированный язык общего назначения, который добавляет сообщения в стиле Smalltalk в Си-подобный язык программирования.

```
NSLog(@"Arch is the best!");

```

**OCaml** — основная реализация языка программирования Caml.

```
print_endline "Arch is the best!"

```

**Octave** — высокоуровневый интерпретируемый язык, предназначенный в основном для математических вычислений.

```
printf("Arch is the best!\n")

```

**Ook!** — brainfuck, переведенный на орангутангский.

```
Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook! Ook? Ook. Ook? Ook! Ook? Ook! Ook! Ook. Ook? Ook. Ook. Ook? Ook. Ook? Ook! Ook? Ook. Ook! Ook! Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook? Ook! Ook. Ook? Ook. Ook? Ook! Ook. Ook? Ook. Ook! Ook? Ook! Ook! Ook? Ook! Ook. Ook? Ook! Ook? Ook! Ook! Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook? Ook! Ook? Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook? Ook! Ook! Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook? Ook! Ook? Ook. Ook! Ook. Ook. Ook? Ook. Ook? Ook. Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook? Ook. Ook? Ook. Ook! Ook. Ook. Ook? Ook. Ook? Ook. Ook. Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook? Ook. Ook? Ook. Ook! Ook. Ook. Ook? Ook. Ook? Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook. Ook. Ook! Ook. Ook? Ook. Ook? Ook. Ook. Ook. Ook! Ook. Ook! Ook? Ook! Ook! Ook? Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook.

```

**Pascal** — влиятельный императивный и процедурный язык программирования.

```
program ArchIsTheBest;
begin
  writeln('Arch is the best!');
end.

```

**Perl** — высокоуровневый, интерпретированный, динамический язык общего назначения.

```
#!/usr/bin/perl
print "Arch is the best!\n";

```

**PHP** — скриптовый язык общего назначения.

```
<?php
   echo "Arch is the best!\n";
?>

```

**Pixilang** — пиксели!

```
print("Arch is the best!",0,0,#1897D1)
frame

```

**Portable GNU assembler** — as -o arch.o arch.s && ld -o arch -O0 arch.o

```
   .section .data
archIsBest:
   .ascii  "Arch is the best!\n"
archIsBest_len:
   .long   . - archIsBest
   .section .text
   .globl _start
_start:
   xorl %ebx, %ebx
   movl $4, %eax
   xorl %ebx, %ebx
   incl %ebx
   leal archIsBest, %ecx
   movl archIsBest_len, %edx
   int $0x80
   xorl %eax, %eax
   incl %eax
   xorl %ebx, %ebx
   int $0x80

```

**Processing** — язык программирования и среда разработки с открытым исходным кодом.

```
println("Arch is the best!");

```

**Prolog** — логический язык программирования общего назначения, связанный с искусственным интеллектом и компьютерной лингвистикой.

```
format('Arch is the best~n',[]).

```

**Python** — высокоуровневый язык общего назначения.

```
#!/usr/bin/env python3
print('Arch is the best!')

```

**QBASIC** — интерпретатор BASIC-подобного языка программирования, основанного на QuickBASIC.

```
PRINT "Arch is the best!"

```

**R** — язык для статистических вычислений (и многого другого!).

```
archIsBest <- function() { cat("Arch is the best!\n") }
archIsBest()

```

**Ruby** — динамический, рефлективный, интерпретируемый высокоуровневый язык программирования для быстрого и удобного объектно-ориентированного программирования.

```
#!/usr/bin/ruby -w
puts 'Arch is the best!'

```

**Rust** — мультипарадигмальный компилируемый язык программирования общего назначения, разрабатываемый Mozilla Research, поддерживающий функциональное программирование, модель акторов, процедурное программирование и объектно-ориентированное программирование.

```
fn main() {
    println!("Arch is the best!");
}

```

**Scala** — мультипарадигменный язык, который работает на JVM.

```
 object ArchIsBest extends App {
     println("Arch is the best!")
 }

```

**Scheme** — диалект Lisp.

```
(display "Arch is the best!\n")

```

or in XunDu style

```
#!/usr/bin/guile1.8 -s
!#
(define 节 or)
(define 哀 #t)
(define (xi) (display "Arch is the best!\n"))
(节 (xi) 哀 (wen) 顺 (le) 变 (jian) )

```

**Seed** — библиотека и интерпретатор, динамически связывающий, движок JavaScriptCore из WebKit с платформой GNOME.

```
#!/usr/bin/env seed
print ('Arch is the best');

```

**Shoes** — версия Ruby, использующая Shoes для GUI.

```
Shoes.app :width => 135, :height => 30 do
    para "Arch is the Best!"
end

```

**SQL** — структурированный язык запросов для реляционных баз данных.

```
SELECT 'Arch is the best!';
SELECT 'Arch is the best!' FROM dual; -- для Оракула

```

**Standard ML** — модульный функциональный язык программирования общего назначения.

```
print "Arch is the best!\n"

```

**Tcl/Tk** — скриптовый язык, используемый для прототипирования, скриптов, графических интерфейсов и тестирования.

```
#!/usr/bin/env tclsh
puts "Arch is the best!"

```

**Vala** — язык программирования, предназначенный для прикладного и системного программирования на основе библиотек GLib Object System (GObject) рабочей среды GNOME/GTK+

```
void main(string[] args) {
stdout.printf("\nArch is the best!\n\n");
}

```

**Wiring (Arduino)** — собранный на Processing, открытый язык программирования, разработанный в стенах МТИ (MIT).

```
void setup()
{
   Serial.begin(9600);
}
void loop()
{
   Serial.print("Arch is the best!");
}

```

**X11** — X11 является кроссплатформенной средой для разработки графических интерфейсов.

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#include <X11/Xlib.h>

int main()
{
       Display *d;
       Window w;
       XEvent e;
       int s;

       if (!(d = XOpenDisplay(NULL))) {
               fprintf(stderr, "Couldn't open display, but Arch is the best!\n");
               exit(1);
       }

       s = DefaultScreen(d);
       w = XCreateSimpleWindow(d, RootWindow(d,s), 0, 0, 110, 20, 0,
                               0, WhitePixel(d,s));
       XSelectInput(d, w, ExposureMask | KeyPressMask);
       XMapWindow(d,w);

       while (1) {
               XNextEvent(d, &e);
               if (e.type == Expose) {
                       XDrawString(d, w, DefaultGC(d, s), 5, 15, "Arch is the best!", 17);
               }
       }

       XCloseDisplay(d);
       return 0;
}

```

## Переводы

**Австралийский**

```
Arch is fair dinkum, mate!

```

**Арабский**

```
ارتش هو الأفضل

```

**Баскский**

```
Arch onena da!

```

**Белорусский**

```
Арч — самы лепшы!

```

**Бенгальский**

```
আর্চ সবচেয়ে ভালো!

```

**Болгарский**

```
Арч е най-добрият!

```

**Британский**

```
Arch is simply spiffing.

```

**Брненский сленг**

```
Arch je nejbetélnější!

```

**Валлийский**

```
Arch sydd yr orau un!

```

**Венгерский**

```
Az Arch a legjobb!

```

**Вьетнамский**

```
Arch là tốt nhất!

```

**Гаитянский креольский**

```
Arch se meye bagay!

```

**Галисийский**

```
Arch é o mellor!

```

**Греческий (современный)**

```
Το Αρτς είναι το καλύτερο!

```

**Датский**

```
Arch er bedst!

```

**Древнегреческий**

```
Ἡ Ἀψίς ἄριστην ἐστί!

```

**Древнекитайский**

```
阿祺，盡善矣。

```

**Иврит**

```
ארצ' זה הכי אחי!

```

**Индонезийский**

```
Arch terbaik!

```

**Ирландский**

```
Arch é is fearr!

```

**Испанский (Аргентина)**

```
Arch es una mazza!!

```

**Испанский (обычный)**

```
¡Arch es el mejor!

```

**Испанский (Уругвай)**

```
Arch la rompe!

```

**Испанский (Чили)**

```
Arch es bacán

```

**Испанский (Чили, еще один вариант)**

```
Arch es la raja

```

**Испанский (Чили, маргинальный)**

```
(написан в IPA, потому что в нормальном испанском просто нет таких звуков) ˈæɹʃ ɛːʰ tɜ.rˈiː.u.lɛ la rˈa.χa ʃʊ.ɹʊ

```

**Итальянский**

```
Arch è il migliore!

```

**Казахский**

```
Арч — ең жақсы!

```

**Каталанский**

```
Arch és el millor!

```

**Квебекский французский**

```
Arch est le plus meilleure du monde!

```

**Китайский (в стиле Taobao — 淘宝体)**

```
Arch，好评哦，亲！

```

**Китайский (традиционный)**

```
Arch 好棒棒！

```

**Китайский (упрощенный)**

```
Arch 最棒了！

```

**Клингонский**

```
Arch'pu'ta' 'a'

```

**Латвийский**

```
Arch ir labākais!

```

**Латинский**

```
Arch optimus est!

```

**Литовский**

```
Arch yra geriausias!

```

**Ложбан**

```
la .artc. xagrai

```

**Малаялам**

```
ആർച് ആണ് ഏറ്റവും നല്ലത്

```

**Маратхи**

```
आर्च सगळ्यात भारी आहे!

```

**Немецкий**

```
Arch ist das Beste!

```

**Непальский**

```
आर्च सबैभन्दा राम्रो हो!

```

**Нидерландский**

```
Arch is de beste!

```

**Норвежский**

```
Arch er best!

```

**Персидский**

```
آرچ بهترین است

```

**Польский**

```
Arch jest najlepszy!

```

**Поросячья латынь**

```
Archway isway ethay estbay!

```

**Португальский**

```
Arch é o melhor!

```

**Руменский**

```
Аrch e cel mai bun!

```

**Русский**

```
Арч — лучший!

```

**Сербский**

```
Arch je najbolji!

```

**Сингапурский**

```
Arch the best lah!

```

**Словенский**

```
Arch je najboljši!

```

**Староанглийский**

```
Arch biþ betst!

```

**Тамильский язык**

```
ஆர்ச்சே சிறந்தது!

```

**Телуг**

```
ఆర్చ్ ఉత్తమమైనది!

```

**Токипона**

```
Arch li pona mute!

```

**Турецкий**

```
Arch en iyisidir!

```

**Украинский**

```
Arch — найкращий!

```

**Урду**

```
آرچ سب سے بہتر ہے!

```

**Филиппинский**

```
Mabuhay ang Arch!

```

**Финский**

```
Arch on paras!

```

**Французский**

```
Arch est le meilleur!

```

**Хинди**

```
आर्च सर्वोत्तम है ।

```

**Хорватский**

```
Arch je najbolji!

```

**Чешский**

```
Arch je nejlepší!

```

**Шведский (образный)**

```
Firch Arkon fir äkon fist bäkon

```

**Шведский**

```
Arch är bäst!

```

**Эсперанто**

```
Arch plejbonas!

```

**Эстонский**

```
Arch on parim!

```

**Японский**

```
Archが一番ですよ！

```

## В разных кодировках

**ASCII-art**

```
                   _       _       _   _            _               _   _
    /\            | |     (_)     | | | |          | |             | | | |
   /  \   _ __ ___| |__    _ ___  | |_| |__   ___  | |__   ___  ___| |_| |
  / /\ \ | '__/ __| '_ \  | / __| | __| '_ \ / _ \ | '_ \ / _ \/ __| __| |
 / ____ \| | | (__| | | | | \__ \ | |_| | | |  __/ | |_) |  __/\__ \ |_|_|
/_/    \_\_|  \___|_| |_| |_|___/  \__|_| |_|\___| |_.__/ \___||___/\__(_)

```

**Base64**

```
QXJjaCBpcyB0aGUgYmVzdCEK

```

**Бинарный ASCII**

```
0100000101110010011000110110100000100000011010010111001100100000011101000110100001100101001000000110001001100101011100110111010000100001

```

**Шрифт Брайля**

```
⠁⠗⠉⠓⠀⠊⠎⠀⠮⠀⠃⠑⠎⠞⠲

```

**Яисревер (Реверсия)**

```
!tseb eht si hcrA

```

**h4x0r**

```
4rch 15 7h3 b357!

```

**Шестнадцатеричный ASCII**

```
4172636820697320746865206265737421

```

**md5sum**

```
2d9092e089d77a8e23f47ba3dfe77027

```

**Код Морзе**

```
.- .-. -.-. ....   .. ...   - .... .   -... . ... -

```

**ROT13**

```
Nepu vf gur orfg!

```

**Вверх ногами**

```
¡ʇsǝq ǝɥʇ s! ɥɔɹ∀

```

**URL Encoded**

```
Arch%20is%20the%20best!

```