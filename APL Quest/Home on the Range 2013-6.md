## [Home on the range](https://problems.tryapl.org/psets/2013.html?goto=P6_Home_On_The_Range)

**Problem:** Write a dfn which returns the magnitude of the range (i.e. the difference between the lowest and highest values) of a numeric array.

**Video:** https://youtu.be/36HlHsEjUIQ
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/6.apl

**Example Solutions:**
```APL
	I←(⌈/-⌊/), ⍝ Tacit - ravel the array and the take the difference of the max and min
	J←{0∊⍴⍵:0 ⋄ (⌈/-⌊/),⍵} ⍝ If zero is a member of the shape of the array return zero. Otherwise find the range. 
	```

**Quotes:**


**Comment:** 
```APL
⌈/⍬ ⍝ Maximum of empty vector is smallest representable number. Minimum reduction produces the opposite value.
⊃⍤⌽ ⍝ Choose the last element of a vector

```

**Glyphs Used:**
[Maximum Reduce](https://aplwiki.com/wiki/Maximum) `⌈/` - returns the largest element of a [vector](https://aplwiki.com/wiki/Vector "Vector")
[Minimum Reduce](https://aplwiki.com/wiki/Minimum) `⌊/` - returns the smallest element of a [vector](https://aplwiki.com/wiki/Vector "Vector")
[Ravel](https://aplwiki.com/wiki/Ravel) `,` - an array's ravel is the [vector](https://aplwiki.com/wiki/Vector "Vector") containing all its [elements](https://aplwiki.com/wiki/Elements "Elements") in [ravel order](https://aplwiki.com/wiki/Ravel_order "Ravel order").
[Over](https://aplwiki.com/wiki/over) `⍥` - both arguments are pre-processed using the right operand
[Commute](https://aplwiki.com/wiki/Commute) `⍨`  - aka Selfie or Swap
[Membership](https://aplwiki.com/wiki/Membership) `∊` - tests if each of the elements of the left [argument](https://aplwiki.com/wiki/Argument "Argument") appears as an element of the right argument.
[Shape](https://aplwiki.com/wiki/Shape) `⍴` - returns the _shape_ of its argument array
[Guards](https://aplwiki.com/wiki/Dfn#Guards) : - Return result
[Diamond](https://aplwiki.com/wiki/Statement_separator) ⋄ - Statement Seperator
[Each](https://aplwiki.com/wiki/Each) `¨` 
[Grade ](https://aplwiki.com/wiki/Grade) `⍋ ⍒`  - Grade returns a [permutation](https://aplwiki.com/index.php?title=Permutation&action=edit&redlink=1 "Permutation (page does not exist)") [vector](https://aplwiki.com/wiki/Vector "Vector") whose length equals the number of [major cells](https://aplwiki.com/wiki/Major_cell "Major cell") - See sort below.
[Pick](https://mastering.dyalog.com/Nested-Arrays-Continued.html?highlight=pick#pick) `⊃` - Left argument is path, right argument is data. 
[Atop](https://aplwiki.com/wiki/Atop_(operator)) `⍤` - Uses the left argument to process the result of the right. 


[Catenate](https://aplwiki.com/wiki/Catenate) `,`
[Index of](https://aplwiki.com/wiki/Index_Of) `⍳`
[Comparison Function](https://aplwiki.com/wiki/Comparison_function) =
[Compress](https://aplwiki.com/wiki/Replicate) `/` - filters the right argument `=/¨` compare each
[Each](https://aplwiki.com/wiki/Each) `¨` 
[Commute](https://aplwiki.com/wiki/Commute) `⍨`  - aka Selfie or Swap
[Dyadic Transpose](https://xpqz.github.io/learnapl/dyadictrn.html?#dyadic-transpose-ab) ``x⍉y`` - allows you to select diagonals by giving one or more dimensions equal mapping
[Reshape](https://aplwiki.com/wiki/Reshape) `⍴`
[At](https://xpqz.github.io/cultivations/Operators.html#at) `@` - What’s on its left gets done at the position indicated by its right operand. 
[Identity](https://aplwiki.com/wiki/Identity) `⊢`
[Where](https://aplwiki.com/wiki/Indices) `⍸` - returns the indices of a boolean array - mondadic
[Power](https://aplwiki.com/wiki/Power_(operator)) `⍣¯1` - used to access function inverses
[Power(Function)](https://aplwiki.com/wiki/Power_(function)) `*` -  `X*Y` is `X` raised to the power `Y`
[Overtake](https://aplwiki.com/wiki/Take#Overtaking) `↑` - A length larger than the argument length causes [fills](https://aplwiki.com/wiki/Fill_element "Fill element") to be inserted
[Bind](https://aplwiki.com/wiki/Bind) `∘` -  used to create a derived function with a single constant argument
[Constant](https://xpqz.github.io/cultivations/Operators.html#constant-a) `A⍨` - always returns the operator array
[Signum](https://aplwiki.com/wiki/Signum) `×A` - Sign of number  - on a real argument are `0`, `1`, and `¯1` (zero, positive and negative)
[Tally](https://aplwiki.com/wiki/Tally) `≢`
[Expand](https://xpqz.github.io/cultivations/Functions7.html?#expand) `\` - copies each [element](https://aplwiki.com/wiki/Element "Element") of the right [argument](https://aplwiki.com/wiki/Argument "Argument") a given number of times
[Roll](https://aplwiki.com/wiki/Roll) `?0` - When zero Roll chooses a floating-point number between 0 and 1
[Matrix Divide](https://aplwiki.com/wiki/Matrix_Divide) `⌹`
[Rank](https://aplwiki.com/wiki/Rank_(operator)) `⍤` - applies its left [operand](. https://aplwiki.com/wiki/Operand "Operand") function to [cells](https://aplwiki.com/wiki/Cells "Cells") of its arguments specified by its right operand array.
[Depth](https://aplwiki.com/wiki/Depth) `≡` - returns an array's depth
[Decode](https://aplwiki.com/wiki/Decode) `⊥` - aka base
[Encode](https://aplwiki.com/wiki/Encode) `⊤` - aka antibase
[Bind](https://aplwiki.com/wiki/Bind) `∘` - used to create a derived function with a single constant argument
[Key](https://aplwiki.com/wiki/Key)  `⌸` - groups [major cells](https://aplwiki.com/wiki/Major_cell "Major cell") and applies the [function](https://aplwiki.com/wiki/Function "Function") for each cell
[Enclose](https://aplwiki.com/wiki/Enclose) `⊂` - An enclosed array is a [scalar](https://aplwiki.com/wiki/Scalar "Scalar"), which is subject to [scalar extension](https://aplwiki.com/wiki/Scalar_extension "Scalar extension").
[Reverse](https://aplwiki.com/wiki/Reverse) `⌽` - reorders [elements](https://aplwiki.com/wiki/Elements "Elements") of the argument to go in the opposite direction along a specified [axis](https://aplwiki.com/wiki/Axis "Axis").
[Circular](https://aplwiki.com/wiki/Circular)  12○ - Phase of ⍵ (omega)
[Pi Times](https://aplwiki.com/wiki/Pi_Times) ○ 
[Magnitude](https://aplwiki.com/wiki/Magnitude) `|` aka absolute value
[Residue](https://aplwiki.com/wiki/Residue) `|` aka remainder

**Concepts Used:**
[Ravel Order](https://aplwiki.com/wiki/Ravel_order)
[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.`
[Sort](https://xpqz.github.io/learnapl/manip.html?highlight=sort#grade-up-down) `data[⍋data]` 



[Identity Matrix](https://en.wikipedia.org/wiki/Identity_matrix)

[Radix](https://en.wikipedia.org/wiki/Radix)
[Index Origin](https://aplwiki.com/wiki/Index_origin) - Generating Functions with that work with 0 or 1 origin

[Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.`

[Matrix Multiplication](https://en.wikipedia.org/wiki/Matrix_multiplication)
[Vector Prefix](https://aplwiki.com/wiki/Prefix)
[Boolean Mask](https://aplwiki.com/wiki/Boolean)
[Complex Numbers](https://aplwiki.com/wiki/Complex_number)
[Phase](https://en.wikipedia.org/wiki/Phase_(waves))
