## [Go Forth and Multiply](https://problems.tryapl.org/psets/2013.html?goto=P8_Go_Forth_And_Multiply)
**Problem:** Write a dfn which produces a multiplication table.

**Video:** https://youtu.be/O_l-nJYmDrs 
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/8.apl

**Outer Product**
```APL
A ← ∘.×⍨⍳
	```

**Without Outer Product**
```APL
B ← {×/¨⍳⍵ ⍵}
C ← ×⍤0 1⍨⍳
D ← {+⍀⍵ ⍵⍴⍳⍵}
E ← +⍀,⍨⍴⍳
F ← +⍀,⍨⍴+⍀⍤⍴∘1
G ← +⍀,⍨+\⍤⍴≢
	```

**Without Operators**
```APL
H ← {⍵ ⍵⍴(⍵/⍳⍵)×(⍵×⍵)⍴⍳⍵}
I ← {t×⍉t←⍵ ⍵⍴⍳⍵}
J ← {↑(⍳⍵)×⊂⍳⍵}
K ← ↑⍳×(⊂⍳)
L ← (↑⊢×⊂)⍳
	```

**Without Arithmetic**
```APL
M ← {≢¨,¨⍳¨⍳⍵ ⍵}
N ← ≢⍤,⍤⍳¨⍳⍤,⍨
O ← ∘.{≢⍺/⍵/#}⍨⍳
P ← ≢⍤⍸¨⍳∘./⍳
Q ← ∘.{≢#,⍣⍺⍣⍵⊢⍬}⍨⍳
	```

**Note:**


**Comment:** 


**Glyphs Used:**
[Floor](https://aplwiki.com/wiki/Floor) `⌊` - a [monadic](https://aplwiki.com/wiki/Monadic "Monadic") [scalar function](https://aplwiki.com/wiki/Scalar_function "Scalar function") that gives the [floor](https://en.wikipedia.org/wiki/floor_and_ceiling_functions "wikipedia:floor and ceiling functions") of a real number
[Equal to](https://aplwiki.com/wiki/Equal_to)  `=` - a [comparison function](https://aplwiki.com/wiki/Comparison_function "Comparison function") which tests whether argument elements are equal to each other.


**Concepts Used:**
[Ravel Order](https://aplwiki.com/wiki/Ravel_order)
[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.`
[Sort](https://xpqz.github.io/learnapl/manip.html?highlight=sort#grade-up-down) `data[⍋data]` 
[Overtake](https://aplwiki.com/wiki/Take#Overtaking) `↑` - A length larger than the argument length causes [fills](https://aplwiki.com/wiki/Fill_element "Fill element") to be inserted
[Fork](https://aplwiki.com/wiki/Train#3-trains)

