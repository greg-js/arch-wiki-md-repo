# Arch is the best

The **Arch is the best** project is a very sophisticated and exquisite, ego-boosting and mind-blowing (albeit perhaps a bit over-engineered) project which gives proof of Arch's superiority.

## Contents

*   [1 History](#History)
*   [2 Installation](#Installation)
*   [3 The code](#The_code)
*   [4 Translations](#Translations)
*   [5 Encodings](#Encodings)

## History

The visionary project was originally devised in April 2008 by long time Arch community member [lucke](https://bbs.archlinux.org/profile.php?id=2529) as a simple shell script which provided irrefutable proof that "Arch is the best". It was announced to the world with a [forum post](https://bbs.archlinux.org/viewtopic.php?id=47306), thus illuminating other people's minds, who immediately started porting it to multiple different languages, both programming and verbal, so that every human being on the planet could fully appreciate and benefit from this revolutionary discovery.

## Installation

A sample PKGBUILD called [archbest-mod1](https://aur.archlinux.org/packages/archbest-mod1/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/archbest-mod1)]</sup> has been uploaded to [AUR](/index.php/AUR "AUR").

## The code

The "Arch is the best" project is ported to many programming languages.

NaN

```
Предупреждение("Arch is the best!");

```

NaN

```
with Ada.Text_IO;
use Ada.Text_IO;
procedure ArchIsTheBest is
begin
   Put_Line("Arch is the best!");
end HelloWorld;

```

NaN

```
'Arch is the best!'

```

NaN

```
implement main () = println! "Arch is the best!"

```

NaN

```
BEGIN {
   print "Arch is the best!"
}

```

NaN

```
<v"Arch is the best!"0
 <,_@#:

```

NaN

```
print "Arch is the best!"

```

NaN

```
#!/bin/sh
echo "Arch is the best!"

```

NaN

```
#!/bin/sh
yes Arch is the best!

```

NaN

```
 #!/bin/bash
 wget http://wiki.archlinux.org/index.php/Arch_is_the_best -qO-| sed -n ':b;n;s/id="Translations"//;Tb;:d;n;s/id="Encodings"//;t;p;bd'|sed '/<i>.*<\/i>/d;s/<[^>]*>//g'|sed 'N;s/\n/: /;N;N;s/\n//g'

```

NaN

```
 #!/bin/bash
 curl -s "https://wiki.archlinux.org/index.php?title=Arch_is_the_best&action=raw" | sed -n '/==Translations==/,$p' | sed "s/^\(.*\)$/* \1:/;t;s/^[^=]/  &/"

```

NaN

```
++>++++++>+++++<+[>[->+<]<->++++++++++<]>>.<[-]>[-<++>]
<----------------.---------------.+++++.<+++[-<++++++++++>]<.
>>+.++++++++++.<<.>>+.------------.---.<<.>>---.
+++.++++++++++++++.+.<<+.[-]++++++++++.

```

NaN

```
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
   puts("Arch is the best!");
   return EXIT_SUCCESS;
}

```

NaN

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

NaN

```
#include <iostream>
#include <cstdlib>
int main ()
{
   std::cout << "Arch is the best!" << std::endl;
   return EXIT_SUCCESS;
}

```

NaN

```
    IDENTIFICATION DIVISION.
    PROGRAM-ID.  TheBest.

    PROCEDURE DIVISION.
        DISPLAY "Arch is the best!".
        STOP RUN.

```

NaN

```
alert 'Arch is the best!'

```

NaN

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

NaN

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

NaN

```
(prn "Arch is the best!")

```

NaN

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

NaN

```
(princ "Arch is the best!")

```

NaN

```
 import std.stdio : writeln;
 void main()
 {
     writeln("Arch is the best");
 }

```

NaN

```
 main(){
   print('Arch is the best');
 }

```

NaN

```
 console.loge with '                So Arch'
 console.loge with '     Much Good'
 console.loge with '                          Wow'

```

NaN

```
 (message "Arch is the best!")

```

NaN

```
-module(arch).
-export([is_the_best/0]).
   is_the_best() -> io:fwrite("Arch is the best!\n").

```

NaN

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

NaN

```
printfn "Arch is the best!"

```

NaN

```
"Arch is the best" print

```

NaN

```
Dear Princess Celestia: Letter About Arch Linux.
Today I learned:
    I wrote "Arch is the best!".
Your faithful student, Twilight Sparkle

```

NaN

```
." Arch is the best" cr -- kiss way

```

NaN

```
program arch
   print *,"Arch is the best!"
end program arch

```

NaN

```
init
 print "Arch is the best"

```

NaN

```
#!/usr/bin/env gjs
print ('Arch is the best');

```

NaN

```
package main

import "fmt"

func main() {
 fmt.Println("Arch is the best!")
}

```

NaN

```
println 'Arch is the best!' 

```

NaN

```
main = putStrLn "Arch is the best!"

```

NaN

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

NaN

```
"Arch is the best!" println

```

NaN

```
public class ArchIsTheBest {
   public static void main(String[] args) {
       System.out.println("Arch is the best!");
   }
}

```

NaN

```
console.log('Arch is the best!');

```

NaN

```
alert('Arch is the best!');

```

NaN

```
println("Arch is the best!")

```

NaN

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

NaN

```
HAI
CAN HAS STDIO?
VISIBLE "ARCH IS TEH PWNZ LOL!"
KTHXBYE

```

NaN

```
print "Arch is the best!"

```

NaN

```
 bCBA@?>=<;:9876543210/.-,+*)('&%$#"!~}|{zyxwvutsrqponmlkjihgfedcba`_^]
 \[ZYXWVUTSRQPONMLKJIHGFEDCBA@?>=<;:9y16543210/.-,+*)('&}C#"!~}|{zyxwvu
 tsrqponmlkjihgfedcba`_^]\[ZYXWVUTSRQPONMLK-CgGFEDCBA@?>=<;:98x6543210/
 .-,+*)('&%$#"!~}|u;yxwpun4rqpRhmf,jihgIe^$ba`_^]\[ZYXQVUTMqQPONMFjJI+A
 eEDC%A:^>=<|:981U54t21*/.-&Jk)('&}C#"!aw={z\xwvun4lqpi/mlkjiKaf_%p

```

NaN

```
writeln("Arch is the best!");

```

NaN

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

NaN

```
echo "Arch is the best!"

```

NaN

```
console.log('Arch is the best!');

```

NaN

```
NSLog(@"Arch is the best!");

```

NaN

```
print_endline "Arch is the best!"

```

NaN

```
printf("Arch is the best!\n")

```

NaN

```
Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook. Ook. Ook! Ook? Ook. Ook? Ook! Ook? Ook! Ook! Ook. Ook? Ook. Ook. Ook? Ook. Ook? Ook! Ook? Ook. Ook! Ook! Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook. Ook? Ook! Ook. Ook? Ook. Ook? Ook! Ook. Ook? Ook. Ook! Ook? Ook! Ook! Ook? Ook! Ook. Ook? Ook! Ook? Ook! Ook! Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook? Ook! Ook? Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook? Ook! Ook! Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook? Ook! Ook? Ook. Ook! Ook. Ook. Ook? Ook. Ook? Ook. Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook? Ook. Ook? Ook. Ook! Ook. Ook. Ook? Ook. Ook? Ook. Ook. Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook? Ook. Ook? Ook. Ook! Ook. Ook. Ook? Ook. Ook? Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook. Ook. Ook! Ook. Ook? Ook. Ook? Ook. Ook. Ook. Ook! Ook. Ook! Ook? Ook! Ook! Ook? Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook.

```

NaN

```
program ArchIsTheBest;
begin
  writeln('Arch is the best!');
end.

```

NaN

```
#!/usr/bin/perl
print "Arch is the best!\n";

```

NaN

```
<?php
   echo "Arch is the best!\n";
?>

```

NaN

```
print("Arch is the best!",0,0,#1897D1)
frame

```

NaN

```
actor Main
  new create(env: Env) =>
    env.out.print("Arch is the best!")

```

NaN

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

NaN

```
println("Arch is the best!");

```

NaN

```
format('Arch is the best~n',[]).

```

NaN

```
#!/usr/bin/env python3
print('Arch is the best!')

```

NaN

```
PRINT "Arch is the best!"

```

NaN

```
archIsBest <- function() { cat("Arch is the best!\n") }
archIsBest()

```

NaN

```
#!/usr/bin/ruby -w
puts 'Arch is the best!'

```

NaN

```
fn main() {
    println!("Arch is the best!");
}

```

NaN

```
 object ArchIsBest extends App {
     println("Arch is the best!")
 }

```

NaN

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

NaN

```
#!/usr/bin/env seed
print ('Arch is the best');

```

NaN

```
Shoes.app :width => 135, :height => 30 do
    para "Arch is the Best!"
end

```

NaN

```
SELECT 'Arch is the best!';
SELECT 'Arch is the best!' from dual; -- for Oracle DB

```

NaN

```
print "Arch is the best!\n"

```

NaN

```
#!/usr/bin/env tclsh
puts "Arch is the best!"

```

NaN

```
#include <Uefi.h>
EFI_STATUS EFIAPI
ArchIsTheBest (
              IN EFI_HANDLE        ImageHandle,
              IN EFI_SYSTEM_TABLE  *SystemTable
              )
{
   SystemTable -> ConOut-> OutputString(SystemTable->ConOut, L"Arch is the best!\n"); 
   return EFI_SUCCESS;
}

```

NaN

```
void main(string[] args) {
stdout.printf("\nArch is the best!\n\n");
}

```

NaN

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

NaN

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

## Translations

NaN

```
阿祺，盡善矣。

```

NaN

```
Ἡ Ἀψίς ἄριστην ἐστί!

```

NaN

```
ارتش هو الأفضل

```

NaN

```
Arch is fair dinkum, mate!

```

NaN

```
Arch terbaik!

```

NaN

```
Arch onena da!

```

NaN

```
Арч - самы лепшы!

```

NaN

```
আর্চ সবচেয়ে ভালো!

```

NaN

```
Arch is simply spiffing.

```

NaN

```
Арч е най-добрият!

```

NaN

```
Arch és el millor!

```

NaN

```
Arch 最棒了！

```

NaN

```
Arch 好棒棒！

```

NaN

```
Arch，好评哦，亲！

```

NaN

```
Arch je nejlepší!

```

NaN

```
Arch je najbolji!

```

NaN

```
Arch er bedst!

```

NaN

```
So Arch, Much Good, Wow

```

NaN

```
Arch is de beste!

```

NaN

```
Arch plejbonas!

```

NaN

```
Arch on parim!

```

NaN

```
Firch Arkon fir äkon fist bäkon

```

NaN

```
Mabuhay ang Arch!

```

NaN

```
Arch on paras!

```

NaN

```
Arch est le meilleur!

```

NaN

```
Arch é o mellor!

```

NaN

```
Arch ist das Beste!

```

NaN

```
Το Αρτς είναι το καλύτερο!

```

NaN

```
Arch se meye bagay!

```

NaN

```
Arch je nejbetélnější!

```

NaN

```
ארצ' זה הכי אחי!

```

NaN

```
आर्च सर्वोत्तम है ।

```

NaN

```
Az Arch a legjobb!

```

NaN

```
Arch é is fearr!

```

NaN

```
Arch è il migliore!

```

NaN

```
Archが一番ですよ！

```

NaN

```
Арч - ең жақсы!

```

NaN

```
Arch'pu'ta"a'

```

NaN

```
아치가 최고입니다!

```

NaN

```
Arch optimus est!

```

NaN

```
Arch ir labākais!

```

NaN

```
4rch 15 7h3 b357!

```

NaN

```
Arch yra geriausias!

```

NaN

```
la .artc. xagrai

```

NaN

```
ARCH IZ TEH BEST!

```

NaN

```
ആർച് ആണ് ഏറ്റവും നല്ലത്

```

NaN

writting system: Unificado

```
Doy kümei Arch

```

writting system: Raguileo

```
Zoy kvmey Arc

```

writting system: Azümchefe (Used in Windows XP)

```
Zoi kümei Arch

```

writting system: Nhewenh

```
Zoi kvmei Arch

```

writting system: Wirizüŋun

```
Zoy kümey Arch _or_ Zoy kvmey Arch

```

NaN

```
आर्च सगळ्यात भारी आहे!

```

NaN

```
आर्च सबैभन्दा राम्रो हो!

```

NaN

```
Arch er best!

```

NaN

```
Arch biþ betst!

```

NaN

```
آرچ بهترین است

```

NaN

```
Archway isway ethay estbay!

```

NaN

```
Arch jest najlepszy!

```

NaN

```
Arch é o melhor!

```

NaN

```
Arch est le plus meilleure du monde!

```

NaN

```
Аrch e cel mai bun!

```

NaN

```
Арч:лучший!

```

NaN

```
Arch je najbolji!

```

NaN

```
Arch the best lah!

```

NaN

```
Arch je najboljši!

```

NaN

```
¡Arch es el mejor!

```

NaN

```
Arch es una mazza!!

```

NaN

```
Arch es bacán

```

NaN

```
Arch es la raja

```

NaN

(written in IPA because standard Spanish doesn't have these sounds)

```
ˈæɹʃ ɛːʰ tɜ.rˈiː.u.lɛ la rˈa.χa ʃʊ.ɹʊ

```

NaN

```
Arch la rompe!

```

NaN

```
Arch är bäst!

```

NaN

```
Arch en iyisidir!

```

NaN

```
ஆர்ச்சே சிறந்தது!

```

NaN

```
ఆర్చ్ ఉత్తమమైనది!

```

NaN

```
อาค์ชเทพเมพขิงขิง

```

NaN

```
Arch li pona mute!

```

NaN

```
Arch:найкращий!

```

NaN

```
آرچ سب سے بہتر ہے!

```

NaN

```
Arch là tốt nhất!

```

NaN

Emphasis on Arch:

```
Arch sydd yr orau un!
Arch sydd y gorau un!

```

Emphasis on being the best (one):

```
Yr orau un yw Arch!
Y gorau un yw Arch!

```

## Encodings

NaN

```
                   _       _       _   _            _               _   _
    /\            | |     (_)     | | | |          | |             | | | |
   /  \   _ __ ___| |__    _ ___  | |_| |__   ___  | |__   ___  ___| |_| |
  / /\ \ | '__/ __| '_ \  | / __| | __| '_ \ / _ \ | '_ \ / _ \/ __| __| |
 / ____ \| | | (__| | | | | \__ \ | |_| | | |  __/ | |_) |  __/\__ \ |_|_|
/_/    \_\_|  \___|_| |_| |_|___/  \__|_| |_|\___| |_.__/ \___||___/\__(_)

```

NaN

```
QXJjaCBpcyB0aGUgYmVzdCEK

```

NaN

```
0100000101110010011000110110100000100000011010010111001100100000011101000110100001100101001000000110001001100101011100110111010000100001

```

NaN

```
⠁⠗⠉⠓⠀⠊⠎⠀⠮⠀⠃⠑⠎⠞⠲

```

NaN

```
!tseb eht si hcrA

```

NaN

```
4rch 15 7h3 b357!

```

NaN

```
4172636820697320746865206265737421

```

NaN

```
2d9092e089d77a8e23f47ba3dfe77027

```

NaN

```
.- .-. -.-. ....   .. ...   - .... .   -... . ... -

```

NaN

```
Nepu vf gur orfg!

```

NaN

```
7f6ed0bf29abbd7e796ca1311c84a7a21a68a656

```

NaN

```
af15cd556676d37f916a35e2cf74f04cf7b1805b3244ec418c3927d8

```

NaN

```
107139d6b9a15fd97acf743e5806823c8ff868fde8b7c28cfcc2c9184df644ae

```

NaN

```
769ec295d876483aa6cec7ff7997296c8ff2236630b0e48b059576143b60ab30adefec9321d8acc2a133219dfb302bc5

```

NaN

```
b0917f66d05278106808d25f51001b038856fa7171b935d450b4bcbf1e8b82ed6a5a2f49d99734e1efc7ad3d1b8a33519008635d4e1aa3e65a5e70c4de649aad

```

NaN

```
¡ʇsǝq ǝɥʇ s! ɥɔɹ∀

```

NaN

```
Arch%20is%20the%20best!

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Arch_is_the_best&oldid=412617](https://wiki.archlinux.org/index.php?title=Arch_is_the_best&oldid=412617)"