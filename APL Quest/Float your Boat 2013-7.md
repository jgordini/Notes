## [Float your Boat](https://problems.tryapl.org/psets/2013.html?goto=P7_Float_Your_Boat)

**Problem:** Write a dfn which selects the floating point (non-integer) numbers from a numeric vector.

**Video:** https://youtu.be/w5LvImFVi2M
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/7.apl

**Example Solutions:**
```APL
F ← {⍵/⍨⍵≠⌊⍵} ⍝ Compare the number against it's rounded version. Same is int. Different is Float.  
Ft ← /⍨∘(≠∘⌊⍨)⍨ ⍝ Tacit Version
	```

**Quotes:**


**Comment:** 
```APL
```

**Glyphs Used:**
[Floor](https://aplwiki.com/wiki/Floor) `⌊` - a [monadic](https://aplwiki.com/wiki/Monadic "Monadic") [scalar function](https://aplwiki.com/wiki/Scalar_function "Scalar function") that gives the [floor](https://en.wikipedia.org/wiki/floor_and_ceiling_functions "wikipedia:floor and ceiling functions") of a real number
[Equal to](https://aplwiki.com/wiki/Equal_to)  `=` - a [comparison function](https://aplwiki.com/wiki/Comparison_function "Comparison function") which tests whether argument elements are equal to each other.
[Not Equal to](https://aplwiki.com/wiki/Not_Equal_to) `≠` - a [comparison function](https://aplwiki.com/wiki/Comparison_function "Comparison function") which tests whether argument elements are unequal.



**Concepts Used:**
[Comparison Tolerance](https://www.jsoftware.com/papers/satn23.htm) - The tolerance is controlled by the value of a system variable ⎕ct .



[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.`
[Sort](https://xpqz.github.io/learnapl/manip.html?highlight=sort#grade-up-down) `data[⍋data]` 
[Overtake](https://aplwiki.com/wiki/Take#Overtaking) `↑` - A length larger than the argument length causes [fills](https://aplwiki.com/wiki/Fill_element "Fill element") to be inserted
[Fork](https://aplwiki.com/wiki/Train#3-trains)
