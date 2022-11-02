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