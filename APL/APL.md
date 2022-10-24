-------------------------------------------------------------------------------

### [APL Books](https://drive.google.com/drive/folders/1By9dnSi53_ov9gYjbiboCoQwaP6zZsvu?usp=sharing)

### [APL Links](https://keep.google.com/u/0/#label/APL)


I wrote this to be the book I would have wanted to read when I started to learn APL. An introduction to APL for an experienced practitioner from a different programming language or two. We all learn in different ways, and I prefer the fundamental concepts laid bare first, and then learn by example.

I came to APL after discovering a file of [solutions](https://github.com/KxSystems/kdb/blob/master/ad.k) to the [Advent of Code](https://adventofcode.com/) 2015 challenge in [K](https://en.wikipedia.org/wiki/K_(programming_language)), an APL derivative. That’s around 100 lines of actual code, and whilst I didn’t understand any of it, I kept looking at it, trying to figure out which of the 50 problems (well, 49) this was a solution to. Each of my Python solutions typically ran to 50-100 lines+ for the bulk of the problems.

Turns out it was the whole lot. That blew my mind.,

Clipped from [Introduction — Learning APL](https://xpqz.github.io/learnapl/intro.html) at 2022-10-24.> ,

Clipped from [](https://www.jstor.org/stable/pdf/27961549.pdf) at 2022-10-24.> ,

Clipped from [](https://www.jstor.org/stable/pdf/27961549.pdf) at 2022-10-24.

Mathematics is a language for formal communication among scientists and engi neers and can be taught effectively via a formal language. A Programming Language (abbreviated APL) is a relatively new multipurpose programming language now available on both minicomputers and large time-sharing systems, with major appli cations in business, scientific research, and education. Originally conceived as a notation for describing algorithms (Iverson 1962), APL is a particularly appropriate language for teaching mathematics. APL provides the user with many symbols for forming concise and unambiguous mathematical expressions. Its syntax is simple, uniform, and easily learned by students. 

The design of APL affords even greater rewards because of its consistency, generality, and elegance?qualities that have been admired by mathematicians and teachers of mathematics alike. APL is further attractive as an interactive language implemented on computers because it provides an active learning environment?one in which the student may engage directly in problem solving and, in a sense, "do" mathematics. APL gives power to the educational process by relegating computational tedium to the machine?leaving the student free to study important concepts and leaving the teacher free to provide guidance and motivation. This is the unique contribution of the computer: not just to transmit knowledge (as in conventional computer-assisted instruction), but to allow the student to experience mathematics directly and to be creative in studying it. Because its roots are in math. 

![[Function Defs.png]]


```
⊆⍨~' '=m  
m←⎕CSV⍠'Separator' 'x'⊢'/Users/optopi/Desktop/input2.txt'⍬ 4  
⍋⊢+⌿m  
j[⍋j]
```


> **J** is a high-level, general-purpose programming language that is particularly suited to the mathematical, statistical, and logical analysis of data. It is a powerful tool for developing algorithms and exploring problems that are not already well understood.

J is written in portable C and is available for Windows, Linux, Mac, iOS, Android and Raspberry Pi. J can be installed and distributed for free. The [source](https://github.com/jsoftware/jsource) is provided under both commercial and GPL 3 licenses.

J is easy to install, has a small footprint, and has direct access to tutorials and documentation.

The latest release is J903 with several new language features and performance improvements, available from Dec 2021. See [J903 Release Notes](https://code.jsoftware.com/wiki/System/ReleaseNotes/J903).

A [J904 beta](https://code.jsoftware.com/wiki/System/ReleaseNotes/J904) is available from April 2022.

**Jd** ( J database) is a high-performance columnar RDBMS writt,

Clipped from [Overview](https://www.jsoftware.com/#/README) at 2022-10-24.

> APL Exercises  
  
**Roger K.W. Hui**  
 

These exercises are designed to introduce APL to a high school senior adept in mathematics.

⎕io←0 throughout.,

Clipped from [APL Exercises](https://www.jsoftware.com/papers/APL_exercises/intro.htm) at 2022-10-24.> APL Exercises 2  
Recursion  
 

⎕io←0 throughout.  
 

**2.0 Factorial**

Write a function to compute the factorial function on integer ⍵ , ⍵≥0 .


```  fac¨ 5 6 7 8
120 720 5040 40320

   n←1+?20
   (fac n) = n×fac n-1
1
   fac 0
1,
 ```
 
Clipped from [APL Exercises](https://www.jsoftware.com/papers/APL_exercises/ex2.htm) at 2022-10-24.> **2.8 Tower of Hanoi**

![](https://www.jsoftware.com/papers/APL_exercises/img/Tower_of_Hanoi_4.gif)

The Tower of Hanoi problem is to move a set of n different-sized disks from one peg to another, moving one disk at a time, using an intermediate peg if necessary. At all times no larger disk may sit on top of a smaller disk.

Write a function Hanoi ⍵ to solve the problem of moving ⍵ disks from peg 0 to peg 2. Since it’s always the disk which is at the top of a peg which is moved, the solution can be stated as a 2-column matrix with column 0 indicating the source peg and column 1 the destination peg.,
