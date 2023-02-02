Translating into dyalog 
prints out a table of ordered pairs to graph y=sin(x)
```APL
∇a pairs b;x;y;z  
[1] x←a  
[2] y←1o x  
[3] z←dtor x  
[4] z;' ';x;' ';y  
[5] x←x+○1÷12  
[6] →(x≤b)/2  
[7] ∇```
To modern APL
Introduces divide by zero error
```APL
rtod ← (180÷○∘÷)N
```
z;' ';x;' ';y   is now z x y
dtor should be rtod
```APL
half←{180-2×rtod ⍺×○÷⍵}
```
Also looking for a solution that identifies the answer by quadrants

There is a math dyalog plugin for windows and linux
https://github.com/Dyalog/Math
```APL
(F G H x) K y → y K⍨ F G H x ⍝ Commute

((2*0.1)-1)÷0.1
0.1÷⍨(2*0.1)-1
0.1÷⍨1-⍨2*0.1
10×¯1+2*0.1 ⍝ Was trying to show ¯1+ and X× patterns for replacing - and ÷
```
