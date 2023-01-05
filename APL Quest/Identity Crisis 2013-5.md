## [Identity Crisis](https://problems.tryapl.org/psets/2013.html?goto=P5_Identity_Crisis)

**Problem:** An [Identity Matrix](https://en.wikipedia.org/wiki/Identity_matrix) is a square matrix (table) of 0 with 1’s in the main diagonal. Write an APL dfn which produces an n×n identity matrix.

**Video:** https://youtu.be/vVaZ3wEdmpQ
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/5.apl

**Example Solutions:**
```APL
n←5
A←(=/¨⍤⍳,⍨) ⍝ equality of x and y in all indices
B←(∘.=⍨⍳) ⍝ equality table for one dimensional indices
```

A
1. [Catenate](https://aplwiki.com/wiki/Catenate) `,` **n** to [Itself](https://aplwiki.com/wiki/Commute) `⍨` we get a vector of 5 5
2. We can take that vector and use it as an input for the [Index Generator](https://aplwiki.com/wiki/Index_Generator). `⍳` this generates an array of shape 5 5 where the elements are the indices for each element.
3. [Equality](https://aplwiki.com/wiki/Comparison_function) Reduction of Each pair `=/¨` we can see where the horizontal and vertical indexes are equal.  This forms our identity matrix. 
4. `⍤` The [Atop](https://aplwiki.com/wiki/Atop_(operator)) operator `f⍤g Y` performs  performs f on the result of g on Y.  This allows the expression to be [Tacit](https://aplwiki.com/wiki/Tacit_programming). 

```APL
{({(=/)⍵}¨)(⍳(⍵,⍵))} ⍝ The expression as a Dfn from tacit.help
```

B
1. 

**Quotes:**
Use tally to get one without using 1

**Comment:** 
```APL
J←{⍵ ⍵⍴(⍵+1)↑1} ⍝ overtake to insert 1 before n 0s
=/¨  ⍝ Compare Each
∘.=⍨ ⍝ Equailty Table using same indeces for both sides
1 1⍉s ⍝ Selects the diagonal of s
,⍨¨ ⍝ Catenate each to itself
x+.×y ⍝ matrix multiplication
,\ ⍝ prefix of a vector
```

**Glyphs Used:**
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
[Identity Matrix](https://en.wikipedia.org/wiki/Identity_matrix)
[Dfn](https://aplwiki.com/wiki/Dfn)
[Radix](https://en.wikipedia.org/wiki/Radix)
[Index Origin](https://aplwiki.com/wiki/Index_origin) - Generating Functions with that work with 0 or 1 origin
[Ravel Order](https://aplwiki.com/wiki/Ravel_order)
[Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.`
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Matrix Multiplication](https://en.wikipedia.org/wiki/Matrix_multiplication)
[Vector Prefix](https://aplwiki.com/wiki/Prefix)
[Boolean Mask](https://aplwiki.com/wiki/Boolean)
[Complex Numbers](https://aplwiki.com/wiki/Complex_number)
[Phase](https://en.wikipedia.org/wiki/Phase_(waves))
