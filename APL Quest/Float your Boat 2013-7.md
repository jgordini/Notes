## [Float your Boat](https://problems.tryapl.org/psets/2013.html?goto=P7_Float_Your_Boat)

**Problem:** Write a dfn which selects the floating point (non-integer) numbers from a numeric vector.

**Video:** https://youtu.be/w5LvImFVi2M
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/7.apl

**Example Solutions:**
```APL
v ← ¯3.1 4 1.5 92.6 ¯5 ⍝ Test Data
A ← {⍵/⍨⍵≠⌊⍵} ⍝ Compare the number against it's rounded version. Same is int. Different is Float.  
B ← (/⍨)∘(≠∘⌊⍨)⍨ ⍝ {(⍵≠(⌊⍵))/⍵}
	```

A
1. `⍵≠⌊⍵` [Floor](https://aplwiki.com/wiki/Floor) `⌊` Rounds down to the nearest real number.
2. [Not Equal to](https://aplwiki.com/wiki/Not_Equal_to) `≠` a [comparison function](https://aplwiki.com/wiki/Comparison_function "Comparison function")  tests whether arguments are unequal. This returns a boolean array where 1 indicates the non-integers. 
3. `⍵/`  [Compress](https://mastering.dyalog.com/Some-Primitive-Functions.html?highlight=compress#replicate) filters the right argument using the boolean array on the left. 
4. [Commute](https://aplwiki.com/wiki/Commute) `⍨` aka Swap used to put the boolean array generated in Step 1 on the left of the Compress. 

B
1. `(≠∘⌊⍨)`  [Selfie](https://mastering.dyalog.com/Tacit-Programming.html?highlight=selfie#commute-selfie-and-constant) `⍨` - used monadically, the same argument gets used on both sides of the function. Thus, `F⍨y` is equivalent to - `y F y`.
2. `∘` Preprocess the right argument `≠` with Floor `⌊`
3. `(/⍨)∘` This time preprocess the right argument with Filter `/`  Using the original test data. 
4. The first Selfie flips the whole expression. 
5. See the comment for a Dfn version

Comparison Tolerance
```APL
T ← 1e¯13+⍳15 ⍝ Test Data using 13 decimals
14⍕w ⍝ Format using 14 decimals

C ← {⎕CT←0 ⋄ ⍵/⍨⍵≠⌊⍵} ⍝ Test Data
	```

C
1. [Comparison Tolerance](https://help.dyalog.com/latest/Content/Language/System%20Functions/ct.htm) `⎕CT` - determines the precision with which two numbers are judged to be equal. Can be set to zero.
2. Apply solution A 

Data Representation
```APL
D ← {⍵/⍨645=⎕DR¨⍵} ⍝ Test Data
x ← v,1e400 ⍝ Test Data 
E ← {⍵/⍨645 1287∊⍨⎕DR¨⍵} ⍝ Test Data
	```

D 
1. [Data Representation](https://help.dyalog.com/latest/Content/Language/System%20Functions/Data%20Representation%20Dyadic.htm) `⎕DR` - converts the data type of its argument Y according to the type specification X
2.  [Each](https://aplwiki.com/wiki/Each) `¨` - applies its [operand](https://aplwiki.com/wiki/Operand "Operand") to each [element](https://aplwiki.com/wiki/Element "Element") of the [arguments](https://aplwiki.com/wiki/Argument "Argument")
E
1. [Membership](https://aplwiki.com/wiki/Membership) `∊` - tests if each of the elements of the left [argument](https://aplwiki.com/wiki/Argument "Argument") appears as an element of the right argument

Print Precision
```APL
F ← {⍵/⍨'.'∊∘⍕¨⍵}
G ← {⎕PP←34 ⋄ ⍵/⍨'.'∊∘⍕¨⍵}
	```

F
1. [Format](https://aplwiki.com/wiki/Format) `⍕` - Dydactic column width and the number of decimal places for formatting [numeric](https://aplwiki.com/index.php?title=Numeric&action=edit&redlink=1 "Numeric (page does not exist)") arrays

G
1. [Print Precision](https://help.dyalog.com/latest/Content/Language/System%20Functions/pp.htm) `⎕PP` - number of significant digits in the display of numeric output

Signum
```APL
H ← {⍵/⍨×1|⍵}
I ← {⎕CT←0 ⋄ ⍵/⍨×1|⍵}
J ← {⍵/⍨×1⊤⍵}
	```

H
1. [Signum](https://aplwiki.com/wiki/Signum) `×` -  three poss ible results of Signum on a real argument are `0`, `1`, and `¯1` : Positive, Negative and Zero.
I
1. [Comparison Tolerance](https://help.dyalog.com/latest/Content/Language/System%20Functions/ct.htm) `⎕CT` - determines the precision with which two numbers are judged to be equal
J
1. [Encode](https://mastering.dyalog.com/Mathematical-Functions.html?highlight=encode#encode) `⊤` - `A⊤B`, turns `B` into a list(s) of digits in (mixed) base

Subtract
```APL
K ← {⍵/⍨0≠⍵-⌊⍵}
	```

K
1. 

Replicate and Error Guard
```APL
L ← ∊{0::⍵⋄⍵/⍬}¨
	```

L
1. [Error Guard](http://help.dyalog.com/18.0/index.htm#Language/Defined%20Functions%20and%20Operators/DynamicFunctions/Error%20Guards.htm) `::` vector of error numbers :: expression to be evaluated
2. [Replicate](https://aplwiki.com/wiki/Replicate) `/` - copies each [element](https://aplwiki.com/wiki/Element "Element") of the right [argument](https://aplwiki.com/wiki/Argument "Argument") a given number of times


**Glyphs Used:**
[Floor](https://aplwiki.com/wiki/Floor) `⌊` - a [monadic](https://aplwiki.com/wiki/Monadic "Monadic") [scalar function](https://aplwiki.com/wiki/Scalar_function "Scalar function") that gives the [floor](https://en.wikipedia.org/wiki/floor_and_ceiling_functions "wikipedia:floor and ceiling functions") of a real number
[Equal to](https://aplwiki.com/wiki/Equal_to)  `=` - a [comparison function](https://aplwiki.com/wiki/Comparison_function "Comparison function") which tests whether argument elements are equal to each other.
[Not Equal to](https://aplwiki.com/wiki/Not_Equal_to) `≠` - a [comparison function](https://aplwiki.com/wiki/Comparison_function "Comparison function") which tests whether argument elements are unequal.
[Compress](https://aplwiki.com/wiki/Replicate) `/` - aka FIlter - requires the number of copies to be [Boolean](https://aplwiki.com/wiki/Boolean "Boolean"): each element is either retained (1 copy) or discarded (0 copies)
[Commute](https://aplwiki.com/wiki/Commute) `⍨` - aka Swap - used dyadically, the arguments are swapped. 
[Selfie](https://mastering.dyalog.com/Tacit-Programming.html?highlight=selfie#commute-selfie-and-constant) `⍨` - used monadically, the same argument gets used on both sides of the function. Thus, `F⍨y` is equivalent to - `y F y`.
[Format](https://aplwiki.com/wiki/Format) `⍕` - Dydactic column width and the number of decimal places for formatting [numeric](https://aplwiki.com/index.php?title=Numeric&action=edit&redlink=1 "Numeric (page does not exist)") arrays
[Comparison Tolerance](https://help.dyalog.com/latest/Content/Language/System%20Functions/ct.htm) `⎕CT` - determines the precision with which two numbers are judged to be equal
[Data Representation](https://help.dyalog.com/latest/Content/Language/System%20Functions/Data%20Representation%20Dyadic.htm) `⎕DR` - converts the data type of its argument Y according to the type specification X
[Each](https://aplwiki.com/wiki/Each) `¨` - applies its [operand](https://aplwiki.com/wiki/Operand "Operand") to each [element](https://aplwiki.com/wiki/Element "Element") of the [arguments](https://aplwiki.com/wiki/Argument "Argument")
[Membership](https://aplwiki.com/wiki/Membership) `∊` - tests if each of the elements of the left [argument](https://aplwiki.com/wiki/Argument "Argument") appears as an element of the right argument
[Print Precision](https://help.dyalog.com/latest/Content/Language/System%20Functions/pp.htm) `⎕PP` - number of significant digits in the display of numeric output
[Residue](https://aplwiki.com/wiki/Residue) `|` - aka Modulo - gives the [remainder](https://en.wikipedia.org/wiki/Remainder "wikipedia:Remainder") of [division](https://aplwiki.com/wiki/Divide "Divide") between two real numbers.
[Signum](https://aplwiki.com/wiki/Signum) `×` -  three poss ible results of Signum on a real argument are `0`, `1`, and `¯1` : Positive, Negative and Zero
[Encode](https://mastering.dyalog.com/Mathematical-Functions.html?highlight=encode#encode) `⊤` - `A⊤B`, turns `B` into a list(s) of digits in (mixed) base
[Replicate](https://aplwiki.com/wiki/Replicate) `/` - copies each [element](https://aplwiki.com/wiki/Element "Element") of the right [argument](https://aplwiki.com/wiki/Argument "Argument") a given number of times
[Error Guard](http://help.dyalog.com/18.0/index.htm#Language/Defined%20Functions%20and%20Operators/DynamicFunctions/Error%20Guards.htm) `::` - vector of error numbers :: expression to be evaluated

**Concepts Used:**
[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Comparison Tolerance](https://www.jsoftware.com/papers/satn23.htm) 
[Function Composition](http://help.dyalog.com/latest/index.htm#Language/Primitive%20Operators/Operator%20Syntax.htm#Function_Composition)
[Hook](https://aplwiki.com/wiki/Hook)
[Derived Function](https://aplwiki.com/wiki/Derived_function)
[Modulo Operation](https://en.wikipedia.org/wiki/Modulo_operation)

**Note:**
<mark style="background: #FFF3A3A6;">Ft </mark> ← Tacit Derived Function - Composed of Operators
Beginning with the first Parenthesis `(≠∘⌊⍨)`
1.  ⌊<mark style="background: #ADCCFFA6;">⍨</mark> ⍵ - Compare Argument with it's own Floor:  Selfie - ⍨
2.  ≠<mark style="background: #BBFABBA6;">∘</mark>⌊⍨ ⍵ - Preprocess the right argument with `≠` using the floor: Jot - ∘
3.   <mark style="background: #FFB8EBA6;">/⍨</mark><mark style="background: #BBFABBA6;">∘</mark>⍺⍺- Preprocess the right parenthesis expression using Jot and then Swap
4.   <mark style="background: #ADCCFFA6;">⍺⍺/ ⍵ ⍨ ⍵</mark> - Filter initial array using result: Selfie - ⍨

**Comment:** 
Swap - <mark style="background: #FFB8EBA6;">⍺ f ⍨ ⍵</mark>  is  <mark style="background: #FFB8EBA6;">⍵ f ⍺</mark>  
Selfie- <mark style="background: #ADCCFFA6;"> f ⍨ ⍵</mark>  is  <mark style="background: #ADCCFFA6;">⍵ f ⍵</mark>
<mark style="background: #BBFABBA6;">Jot </mark> - {R}←{X} f∘g Y - Preprocess the right argument. Then apply the left.