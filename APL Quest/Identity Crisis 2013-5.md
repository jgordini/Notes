## [Identity Crisis](https://problems.tryapl.org/psets/2013.html?goto=P5_Identity_Crisis)

**Problem:** An [Identity Matrix](https://en.wikipedia.org/wiki/Identity_matrix) is a square matrix (table) of 0 with 1’s in the main diagonal. Write an APL dfn which produces an n×n identity matrix.

**Video:** https://youtu.be/vVaZ3wEdmpQ
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/5.apl

**Example Solutions:**

**A**
```APL
n←5
A←(=/¨⍤⍳,⍨) ⍝ equality of x and y in all indices
```

1. [Catenate](https://aplwiki.com/wiki/Catenate) `,` **n** to [Itself](https://aplwiki.com/wiki/Commute) `⍨` we get a vector of 5 5
2. We can take that vector and use it as an input for the [Index Generator](https://aplwiki.com/wiki/Index_Generator). `⍳` this generates an array of shape 5 5 where the elements are the indices for each element.
3. [Equality](https://aplwiki.com/wiki/Comparison_function) [Reduction](https://aplwiki.com/wiki/Reduce) of [Each](https://aplwiki.com/wiki/Each) pair `=/¨` we can see where the horizontal and vertical indexes are equal.  This forms our identity matrix. 
4. `⍤` The [Atop](https://aplwiki.com/wiki/Atop_(operator)) operator `f⍤g Y` performs  performs f on the result of g on Y.  This allows the expression to be [Tacit](https://aplwiki.com/wiki/Tacit_programming). 

```APL
{({(=/)⍵}¨)(⍳(⍵,⍵))} ⍝ The expression as a Dfn from tacit.help
```

**B** - Equailty Table using same indeces for both sides
```APL
B←(∘.=⍨⍳) ⍝ equality table for one dimensional indices
```

1. `∘.` [Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.` generates a table from the input vector
2. `⍨⍳` Same input vector on both sides. Uses [Index Generator](https://aplwiki.com/wiki/Index_Generator) `⍳` to create the values. 
3. `=` [Comparison Function](https://aplwiki.com/wiki/Comparison_function) = checks for eqality beween the elements. 
4. This forms our identity matrix. 

**C** - Assign to diagonal
```APL
{s←⍵ ⍵⍴0 ⋄ (1 1⍉s)←1 ⋄ s} ⍝ assign to diagonal
```

1. `⍵ ⍵⍴0` Reshape 0 to a 5 by 5 matrix and assign it to s
2. `(1 1⍉s)←1` Giving 1 1 to [dyadic transpose ](https://xpqz.github.io/learnapl/dyadictrn.html?highlight=assignment#dyadic-transpose-ab)returns the leading diagonal. 1 replaces those values becuase dyadic transpose allows for modified assignment. 
3. `s` returns the new identity matrix. Diamond is the statement seperator. 

D - amend at (i,i)
```APL
{1@(,⍨¨⍳⍵)⊢⍵ ⍵⍴0} ⍝ amend at (i,i)
```
1. `,⍨¨⍳⍵` By using the Index Generator `⍳`  and [catenating](https://aplwiki.com/wiki/Catenate) `,` [each](https://aplwiki.com/wiki/Each) `¨`  value to [itself](https://aplwiki.com/wiki/Commute) `⍨` we can generate all the indices that need to be set to 1.  (1 1) (2 2) (3 3) (4 4) (5 5)
2. `1@` Sets 1 [At](https://xpqz.github.io/cultivations/Operators.html#at) each location.
3. `⊢⍵ ⍵⍴0` [Identity](https://aplwiki.com/wiki/Identity) `⊢` returns the  [Reshaped](https://aplwiki.com/wiki/Reshape) `⍴` array of ⍵ ⍵ filled with zeros. 

E - 1s at (i,i)
```APL
⍸⍣¯1,⍨¨⍳ ⍝ 1s at (i,i)
```
1. `,⍨¨⍳` Step 1 of D (1 1) (2 2) (3 3) (4 4) (5 5)
2.  `⍸⍣¯1`  [Where](https://aplwiki.com/wiki/Indices) `⍸` returns the [indices](https://aplwiki.com/wiki/Index "Index") of all ones in a [Boolean](https://aplwiki.com/wiki/Boolean "Boolean") array. The [Power Operator](https://aplwiki.com/wiki/Power_(operator))  with `¯1` returns the inverse of the Where function. Given the indices in Step 1 it returns a boolean vector with ones at each position. The [inverse of indices](https://aplwiki.com/wiki/Indices#Inverse). 
3. This generates our identity matrix. 

F
```APL
{⎕IO←0 ⋄ d←i+⍵×i←⍳⍵ ⋄ ⍵ ⍵⍴1@d⊢0↑⍨⍵*2} ⍝ amend at (i,i)ₙ
```
1. `⎕IO←0` Sets [Index Origin](https://aplwiki.com/wiki/Index_origin)  to 0
2. `d←i+⍵×i←⍳⍵` Taking the indices `⍳⍵` we can multiply by their length `w` we get the indices for the [leading axis](https://aplwiki.com/wiki/Leading_axis_theory) in [ravel order](https://aplwiki.com/wiki/Ravel_order) (0 5 10 15 20 25), adding the indices `⍳⍵` returns the diagonal (0 6 12 18 24). This is then assigned to `d` which we use in the next step. 
4. `1@d` We then set 1s [At](https://xpqz.github.io/cultivations/Operators.html#at) `1@d` these indices in a vector `⊢` of 0s with length of `⍵*2` using [Overtake](https://aplwiki.com/wiki/Take#Overtaking)  `↑` 
5. `⍵ ⍵⍴` The result is shaped into a matrix using [Reshape](https://aplwiki.com/wiki/Reshape) `⍴`

I - Industrial Versions
```APL
A ←{⍵ ⍵⍴1,⍵↑0} ⍝ insert 1 before n 0s
B ←{⍵ ⍵⍴(⍵+1)↑1} ⍝ overtake
C ←(,⍨⍴+∘1↑1⍨) ⍝ tacit form
D ←(,⍨⍴+∘1↑×) ⍝ sign gives 1 (or 0 for 0)
E ←(,⍨⍴+∘1↑≢) ⍝ tally of scalar is 1
```

A 
1. There are n zeros to the next 1. (1 0 0 0 0 0 1) ex. n=5
2. `1,⍵↑0` [Overtake](https://aplwiki.com/wiki/Take#Overtaking) `↑` A length larger than the argument length causes [fills](https://aplwiki.com/wiki/Fill_element "Fill element") to be inserted. In this case we use it to pad zero with `⍵-1` additional zeros. `1,` [Catenate](https://aplwiki.com/wiki/Catenate) a 1 to the result. 
3.  [Reshape](https://aplwiki.com/wiki/Reshape) `⍴` repeats an argument of any length, singleton or otherwise. We prefix it with `⍵ ⍵` to indicate the desired final shape.  A 5x5 matrix using the example in Step 1. 

B
1.  Using the concept of Overtake we saw in Step 1 of A we can pad 1 with `⍵+1`  zeros and then reshape the result. Obtaining the same matrix. 

C - Tacit
1.  `,⍨⍴` Ravel the argument against itself and use it to reshape
2. `+∘1` Bind + to 1 making it monadic. Add one to the argument. 
3. `↑1⍨` Use step 2 to Overtake 1. The Selfie `⍨` is used as a [Constant](https://aplwiki.com/wiki/Constant). 

D  - Signum
1.  [Signum](https://aplwiki.com/wiki/Signum) `×A` - Sign of number  - on a real argument are `0`, `1`, and `¯1` (zero, positive and negative)

E - Tally
1.  [Tally](https://aplwiki.com/wiki/Tally) `≢` The tally of a Scalar is 1

Expand
```APL
⍵ ⍵⍴1(-⍵)\1 ⍝ expand 1 into one 1 and n 0s
,⍨⍴1\⍨1,- ⍝ tacit
{(⍵,⍵)⍴((1,(-⍵))\1)} ⍝ tacit.help
```

1. [Expand](https://xpqz.github.io/cultivations/Functions7.html?#expand) `\` - copies each [element](https://aplwiki.com/wiki/Element "Element") of the right [argument](https://aplwiki.com/wiki/Argument "Argument") a given number of times. Positive numbers on the left also replicate like with `/` but negative numbers insert that many prototypical elements at that position.
2. 

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
