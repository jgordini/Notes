## [Float your Boat](https://problems.tryapl.org/psets/2013.html?goto=P7_Float_Your_Boat)

**Problem:** Write a dfn which selects the floating point (non-integer) numbers from a numeric vector.

**Video:** https://youtu.be/w5LvImFVi2M
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/7.apl

**Example Solutions:**
```APL
F ← {⍵/⍨⍵≠⌊⍵} ⍝ Compare the number against it's rounded version. Same is int. Different is Float.  
Ft ← /⍨∘(≠∘⌊⍨)⍨ ⍝ Tacit Version - See Note
	```

**Note:**
<mark style="background: #FFF3A3A6;">Ft </mark> ← Tacit Derived Function - Composed of Operators
Beginning with the Parenthesis `(≠∘⌊⍨)`
1.  ⌊<mark style="background: #ADCCFFA6;">⍨</mark> ⍵ - Compare Argument with it's own Floor:  Selfie - ⍨
2.  ≠<mark style="background: #BBFABBA6;">∘</mark>⌊⍨ ⍵ - Preprocess the right argument with `≠` using the floor: Jot - ∘
3.   /<mark style="background: #ADCCFFA6;">⍨</mark><mark style="background: #BBFABBA6;">∘</mark>⍵⍵- Preprocess the parenthesis expression using Jot and then Swap
4.    <mark style="background: #FFB8EBA6;">⍺/ ⍵⍵ ⍨ ⍵</mark> - Filter result using initial array: Swap - ⍨

**Comment:** 
Swap - <mark style="background: #FFB8EBA6;">⍺ f ⍨ ⍵</mark>  is  <mark style="background: #FFB8EBA6;">⍵ f ⍺</mark>  
Selfie- <mark style="background: #ADCCFFA6;"> f ⍨ ⍵</mark>  is  <mark style="background: #ADCCFFA6;">⍵ f ⍵</mark>
<mark style="background: #BBFABBA6;">Jot </mark> - {R}←{X} f∘g Y - Preprocess the right argument. Then apply the left.

```APL

```

**Glyphs Used:**
[Floor](https://aplwiki.com/wiki/Floor) `⌊` - a [monadic](https://aplwiki.com/wiki/Monadic "Monadic") [scalar function](https://aplwiki.com/wiki/Scalar_function "Scalar function") that gives the [floor](https://en.wikipedia.org/wiki/floor_and_ceiling_functions "wikipedia:floor and ceiling functions") of a real number
[Equal to](https://aplwiki.com/wiki/Equal_to)  `=` - a [comparison function](https://aplwiki.com/wiki/Comparison_function "Comparison function") which tests whether argument elements are equal to each other.
[Not Equal to](https://aplwiki.com/wiki/Not_Equal_to) `≠` - a [comparison function](https://aplwiki.com/wiki/Comparison_function "Comparison function") which tests whether argument elements are unequal.
[Compress](https://aplwiki.com/wiki/Replicate) `/` - aka FIlter - requires the number of copies to be [Boolean](https://aplwiki.com/wiki/Boolean "Boolean"): each element is either retained (1 copy) or discarded (0 copies)
[Commute](https://aplwiki.com/wiki/Commute) `⍨` - aka Swap - used dyadically, the arguments are swapped. 



**Concepts Used:**
[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Comparison Tolerance](https://www.jsoftware.com/papers/satn23.htm) - The tolerance is controlled by the value of a system variable ⎕ct .
[Commute](https://aplwiki.com/wiki/Commute) `⍨` - can be used to emulate a monadic `f g h` [Fork](https://aplwiki.com/wiki/Fork "Fork") when combined with [Compose](https://aplwiki.com/wiki/Compose "Compose")
[Function Composition](http://help.dyalog.com/latest/index.htm#Language/Primitive%20Operators/Operator%20Syntax.htm#Function_Composition)
[Hook](https://aplwiki.com/wiki/Hook)
[Derived Function](https://aplwiki.com/wiki/Derived_function)




[Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.`
[Sort](https://xpqz.github.io/learnapl/manip.html?highlight=sort#grade-up-down) `data[⍋data]` 
[Overtake](https://aplwiki.com/wiki/Take#Overtaking) `↑` - A length larger than the argument length causes [fills](https://aplwiki.com/wiki/Fill_element "Fill element") to be inserted
[Fork](https://aplwiki.com/wiki/Train#3-trains)
