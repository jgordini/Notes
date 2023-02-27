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
A ←{⍵ ⍵⍴1(-⍵)\1} ⍝ expand 1 into one 1 and n 0s
B ←(,⍨⍴1\⍨1,-) ⍝ tacit
C ←{(⍵,⍵)⍴((1,(-⍵))\1)} ⍝ tacit.help
```

1. [Expand](https://xpqz.github.io/cultivations/Functions7.html?#expand) `\` - copies each [element](https://aplwiki.com/wiki/Element "Element") of the right [argument](https://aplwiki.com/wiki/Argument "Argument") a given number of times. Positive numbers on the left also replicate like with `/` but negative numbers insert that many prototypical (spaces for characters and zeros for numbers) elements at that position. 
2. `1(-⍵)\1`  `-⍵` is the number of zeros. `\1` is the number to prepend with. `1(-⍵)` is the number of times to prepend with a 1. 
3. `⍵ ⍵⍴`  Reshape into a `⍵ ⍵` matrix. 


B
1. `,⍨⍴1` Self concatenation of the argument reshaped by 
2. `1\⍨1` 1 expanded by 1 (See A step 2)
3. `,-` followed by the negation of the argument (generates zeros)
4. See C for [Dfn](https://aplwiki.com/wiki/Dfn) form

Matrix - [Matrix Multiplication](https://en.wikipedia.org/wiki/Matrix_multiplication)

```APL
A ←{⌹⍨?⍵ ⍵⍴0} ⍝ M × I = M
B ←(⌹⍨⍤?,⍨⍴≡) ⍝ depth of simple scalar is 0
C ←{(?((⍵,⍵)⍴(≡⍵)))⌹(?((⍵,⍵)⍴(≡⍵)))} ⍝ tacit.help
```

A
1. Reshape a matrix of random numbers against it's inverse. 
2. `?⍵ ⍵⍴0` This gives us a matrix of random floats between zero and one. 
3. [Matrix Divide](https://aplwiki.com/wiki/Matrix_Divide) `⌹` Using [Selfie](https://mastering.dyalog.com/Tacit-Programming.html?highlight=selfie#commute-and-selfie) `⍨` we echo the right argument to its left. In this case the matrix generated in Step 2 is divided by itself.
4. This produces the identity matrix using [matrix multiplication](https://en.wikipedia.org/wiki/Matrix_multiplication)
B
1. Makes A a [Tacit Function]([Tacit Programming](https://aplwiki.com/wiki/Tacit_programming))
2. Can be read as Matrix division `⌹`, Selfie `⍨` , On `⍤`, random numbers `?` shaped `⍴` as the self concatentation `,⍨`(takes one input and makes it two) of [Depth](https://aplwiki.com/wiki/Depth) `≡` - returns an array's depth. On a scaler (our input) it reurns zero. 
3. See C for [Dfn](https://aplwiki.com/wiki/Dfn) form

Base conversion

```APL
A ← (⍴∘2⊤2*⊢-⍳) ⍝ powers of two are 1 0 0 …
B ← {(⍵⍴2)⊤(2*(⍵-(⍳⍵)))} ⍝ tacit.help
```

A
1.  Looking at our identiry matrix we can see that each column is a power of two spelled out in binary. 
2. `2*⊢-⍳` We can generate these numbers by subtracting the initial [Identity](https://aplwiki.com/wiki/Identity) `⊢` from the  [Index Generator](https://aplwiki.com/wiki/Index_Generator)`⍳` of the argument and raising the result to the [power of](https://aplwiki.com/wiki/Exponential) 2. 
3. We can then perform a base conversion. The left argument to [Encode](https://mastering.dyalog.com/Mathematical-Functions.html?highlight=encode#encode) `⊤` defines the number of digits in the new number system. In this case we are prefixing it with a 2.
4. We [Bind](https://aplwiki.com/wiki/Bind) `∘` -  the Encode `⊤` with [Reshape](https://aplwiki.com/wiki/Reshape) `⍴` creating a derived function and a tacit result. 
5. See B for [Dfn](https://aplwiki.com/wiki/Dfn) form

Overtake, Mix and Scan
```APL
A ← (-⍤⍳↑⍤0≢) ⍝ suffixes of 1
B ← (↑,⍨\⍤↑∘1) ⍝ cumulative reverse-concatenations
C ← {↑(({⍵,⍺}\)(⍵↑1))} ⍝ tacit.help
```

A
1. `-⍤⍳` Negation of the indices
2. Paired with the rank operator. Take using a length which is larger than the argument length causes [fills](https://aplwiki.com/wiki/Fill_element "Fill element") of 0's to be inserted.
3. Use tally to get a 1 allows function to be tacit. 
4. `{(-(⍳⍵))(↑⍤0)(≢⍵)}` is the Dfn version

B
1. `,⍨\` Swapped concatentation of scan returns the reversed prefixes of a vector
2. `↑∘1` Take binded with one. Overtakes one with the arguments number of zeros. In this case n=5
3. `⍤` Atop seperates the functions returns the right and then the left. 

Key Operator
```APL
A←(×⌽⍤↑⌸⍤⍳) ⍝ {×(({⌽(⍺↑⍵)}⌸)(⍳⍵))}
B←(⍸⍣¯1⍤⊢⌸⍳) ⍝ {({(⍸⍣¯1)⍵}⌸)(⍳⍵)}
```

A
1. Signum reversal atop of the the taking of the two arguments
2. `↑⌸⍤⍳`  We use the [Index Generator](https://aplwiki.com/wiki/Index_Generator) `⍳` to produce a list of numbers. [Key](https://aplwiki.com/wiki/Key)  `⌸`  groups each unique element as left argument, and the indices of that element in the data as right argument. We can then [Overtake](https://aplwiki.com/wiki/Take#Overtaking) `↑` with a length larger than the argument length causing  [fills](https://aplwiki.com/wiki/Fill_element "Fill element") of zeros to be inserted.
3. `×⌽` [Reverse](https://aplwiki.com/wiki/Reverse) `⌽` reorders the [elements](https://aplwiki.com/wiki/Elements "Elements") of the argument to go in the opposite direction along a specified [axis](https://aplwiki.com/wiki/Axis "Axis") We then use  [Signum](https://aplwiki.com/wiki/Signum) `×` to generate 1's, instead of the indices generated by Key in Step 2. 
4. `⍤` The [Atop](https://aplwiki.com/wiki/Atop_(operator)) operator `f⍤g Y` performs  performs f on the result of g on Y.  This allows the expression to be [Tacit](https://aplwiki.com/wiki/Tacit_programming). 
5. See Comment for the [Dfn](https://aplwiki.com/wiki/Dfn) version. 

B
1. Where inverse atop the right argument. Boolean vectors with 1 in each position. 
2.  `⊢⌸⍳`   Same as in A we use the [Index Generator](https://aplwiki.com/wiki/Index_Generator) `⍳` to produce a list of numbers. [Key](https://aplwiki.com/wiki/Key)  `⌸`  groups each unique element as left argument, and the indices of that element in the data as right argument. However we use [Identity](https://aplwiki.com/wiki/Identity) `⊢` to just return the indices. 
3. `⍸⍣¯1` [Power](https://aplwiki.com/wiki/Power_(operator)) `⍣¯1` is used to access function inverses. [Where](https://aplwiki.com/wiki/Indices) `⍸` returns the indices of a boolean array. So this will pad our indices with zeros. 
4. `⍤` The [Atop](https://aplwiki.com/wiki/Atop_(operator)) operator `f⍤g Y` performs  performs f on the result of g on Y.  This allows the expression to be [Tacit](https://aplwiki.com/wiki/Tacit_programming). 
5. See Comment for the [Dfn](https://aplwiki.com/wiki/Dfn) version. 

[Complex Numbers](https://aplwiki.com/wiki/Complex_number)

```APL
A ← {4=○÷12○⍵∘.+0j1×⍵}⍳ ⍝ π÷4 = arg(a+ai)
B ← {0=(2*÷2)||⍵∘.+0j1×⍵}⍳ ⍝ |a+ai| = 0 mod √2
```

A
1. `⍵∘.+0j1×⍵` Using [Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.+` of the real part plus the imaginary part `+0j1` and Multiplying the imaginary part `0j1×⍵` by the Index `⍳` to create a table.  
2. `○÷12○` The [Circular](https://aplwiki.com/wiki/Circular)  `12○` function is the [Phase](https://en.wikipedia.org/wiki/Phase_(waves)) of ⍵. This determines the magnitude and the direction fo a complex number.  
3. `4=○÷` The diagonal values will have Phase of 45 degrees or one quarter of pi (0.785398163 radians). Dividing by pi `○÷` returns 4 and we can then select all the 4's in the matrix. Returning 1's for true. 
B
1. `⍵∘.+0j1×⍵` Again using [Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.+` of the real part plus the imaginary part `+0j1` and Multiplying the imaginary part `0j1×⍵` by the Index `⍳` to create a table.  
2. When two complex numbers are added, they form the two sides of a right triangle in the complex plane, with the resulting complex number being the hypotenuse. The magnitude of the resulting complex number is equal to the length of the hypotenuse.
3. Becuase the horizontal and the vertical parts of this triangle are equal to each other( the same index is used on both sides of the outer product). The diagnals length is a multiple of the square root of 2. 
4. `(2*÷2)||` The first vertial bar takes the [Magnitude](https://aplwiki.com/wiki/Magnitude) `|` of the result of Step 1. The second bar calculates the remainder or [Residue](https://aplwiki.com/wiki/Residue) when the table is divided by the square root of two `(2*÷2)` 
5. `0=` Everywhere there is no remainder we are on the diagonal. 

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

welcome to this episode of the apl quest c apl wiki for details today's quest is generating an identity matrix of order n very simple task um but a lot of interesting ways we can do this and let's go get started with some serious solutions and then look at some more fun innovative solutions after that so the first thing we can do is that we have a number n let's for argument 6a that n is five and we want to make a matrix that is five by five so we can calculate n to itself giving us five by five next up we can generate all the indices of an array of shape five five and we can take these indices and look at where the horizontal and vertical index are the same by comparing each this gives us our identity matrix however we can do this in a simpler way we only need to generate the indices until n and then make an inequality table using the outer product and the selfie or commute operator to use the same indices on both sides of the quality and in fact this is our simplest solution so just the outer product selfie on the indices it isn't a very efficient solution however because we are comparing a lot of numbers in general that we have generated when we actually know where the ones are going to be in advance so what we can do is we can start off by creating an empty matrix of zeros so we take n and use that twice to reshape zero this gives us a big empty vector like this an empty matrix like this no it's not empty it has big zero matrix like this then we can use dyadic transpose which selects the um it can collapse dimensions so that we get diagonals we can illustrate this by saying 5 5 reshape iota 25 and then we can use the attic transpose mapping both dimensions to a single dimension and that gives us the compromise between them diagonal so now we can use this with a selective assignment we say one one transpose of s gates one and the one that gets distributed over the entire s and now s has been updated to become an identity matrix we can put this into a function as s gets omega omega reshape zero and then the diagonal of s gets one and then return that s and we can now give it the argument five fine and this is verbose but it works it doesn't have the best performance necessarily and it's a bit awkward because we have to have this middle statement where we update s before we then return s we can also use the add operator to do something similar we can start off by generating all the indices that need to be set to 1. how can we do this well if we start with uh with this iota n um in in our case then we know that it is the uh the elements of position one one two two three three four four and that need to be set to one so what we can do is we concatenate selfie concatenate to itself each one of them and these are the indices that we need to set to one and then there we can use this setting one at those indices in the array that is n and reshape zero and that will give us an identity matrix we could also use these indices in a different way and namely we could say give me a boolean matrix that has ones in those positions so where are all the ones in the boolean matrix is magnetic iota underbar and the inverse we can use power negative one on that and that gives us an identity matrix as well there are even more things that we could do along these lines instead of using a matrix we can use a vector and the way we can do that is by observing that this is kind of an encoding of in in a special radix so we want ones and then when we do things like that we we need to see set coordinator to zero otherwise it becomes too complicated so what we can do is we have the indices um iota n here and then we can multiply those by n and so this corresponds to um let's see number zero is this element and number five is this element and number ten is this element in revel order however we need to offset one for each one so if you take these indices and add them to this that gives us in revel order that diagonal we can actually see this if we say 5 5 reshape by yo to 25 we can see that 0 6 12 18 24 those are diagonals and once we have those we can then use the add operator as before so we can set the ones at that in a vector which is zero reshaped to the shape of n squared and this is our flattened identity matrix now we can take the proper shape and reshape it and we get our identity matrix let's change back to quarter one index origin one and then actually do some uh the best performing solutions and and that we can observe similar to what we've done now we can see that there are exactly n zeros onto the next one and then again n zeros to the next one so what we can do is we can begin with a one followed by n zeros and then we can reshape that cyclically into our full full shape we'll use n here and this is almost as good as it gets there's one problem for a very large n and we create a boolean vector of all zeros and then by inserting one at the beginning it gives us sub-optimal performance because we need to copy this entire array one step over shifting everything by one bit to insert that leading bit how can we avoid that well we can use overtake so if we say n take of one it pads with additional zeros at the end and the only thing we need to do here is really adding n plus one and this gives us the full row and now we can reshape into that shape so this is going to be the best it gets we can put this into a function as omega omega reshape omega plus one take one and we can also make this into a tested form and we can play some tricks there so let's split up the problem omega omega that is the self concatenation of the argument then we reshape that and then we want the argument plus one so we can tie or bind a 1 to plus making a magnetic function so that's an increment function and we use that to take from well we need a 1 here but we can't have 1 at the end of a tested function because it's a constant not a function we can transform it into a function using uh the constant operator so we can try this as well and that works and then for a little bit of uh of trickery we can actually avoid this construct of one constant by observing that the sine of five is one and the problem was that we needed on the right hand to have a function not a constant so this is a function applied to any number that's relevant and we get one if we want the zero by zero it doesn't matter that the sine of zero is zero it will still work because we it becomes an empty array so it doesn't matter that we are taking from 0 there so we can do this we can say i5 like this another possibility is observing that how many elements are there in a single number there's only one and that applies even to zero and so we can we can do that as well so this is a this is the fastest solution that we're going to get this is a proper solution whether you want to use a tested form or a defend it should be about the same performance now onto some more fun and innovative solutions that we could do and remember again that we needed a single one followed by n zeros and we can actually do that using expand so if we have uh if we have a one representing that we want um one one and then we have negative n representing n fill elements we can use that with the expand function on a single one to get the same thing and then we can reshape that to our identity matrix and we can write this um in a tested form and so this is again the self-concatenation reshapes one expanded by one followed by the negation and it works for zero as well what happens in the zero case is negation of zero is zero so we get one zero that means we expand one as a single one with no fill elements reshape that to zero zero and we have an empty numeric matrix so that works as well um here's one that almost always works like there is an astronomically small probability that it won't work but it is rather fun let's say we have a matrix of uh random numbers so with the zero as argument question mark gives us random floats between zero and one so they won't be zero they won't be one and it's exceedingly unlikely that we'll have duplicates here of course now if this is a matrix then there must exist a matrix such that m and multiplication here means matrix multiplication we can we can write that as cluster times um will give us but in traditional mathematics just at times will give us the matrix itself and that is the identity matrix now if we move things around around on the in this equation we'll find that dividing the matrix by itself should give us the identity matrix and indeed that is so so we can do m matrix divide with m and that gives us an identity matrix and we can write the whole thing as matrix division selfie on the random numbers of the self-concatenation of zero so here's a constant zero again you can try this and it works similar to what we did with sine and tally to get a 1 there's also a function which for a single number a scalar gives 0 and that is the depth function so the depth of a single number a scalar simple scalar is zero so we can go up and amend our function to this very obscure looking thing which works just fine and is very very inefficient because api will have to solve an equation system every time we generate an identity matrix but hey it's fun right here's another one which is very very inefficient let's think about this we've got the indices up to n um if we subtract these from n itself that gives us descending powers from four down to zero raised two to the power of that and we've got descending powers of two and now if we go up and look in our identity matrix then we can see that the first column is 16 spelled out in binary and the second column is 8 spelled out in binary and 4 and 2 and 1. so this means that if we represent all these numbers in a in base 2 then we we would get the identity matrix so we could do something like this which auto sizes but we already know that we want n bits so we can say n nreship2 encode on that and that works as well and then we can make the whole thing tacit by saying that it is the reshape of two so this is a magnetic function which reshapes two encodes 2 to the power of the argument minus iota on the argument so this works just fine but again very inefficient doing base conversions when we just want to create um an identity makes it but fun it's fun okay a little bit more and of fun we can um we can generate the negative indices and then we can overtake like we did before on a1 so each one of these will be used to take from a1 so it takes from the rear padding will zero us at the front oops that was too much missing in each there there we go and now we just need to stack them up on top of each other and there are various ways we could do that we can mix or we could use the rank operator so we want to pair these up we need to do take pair these up with one and then it mixes everything together so that works as well and now we can put all this together to create an um a tested function so we have the negation of iota take rank 0 on remember how to get a 1 without using literal one we could use tally for example so this should work as well and here's our density matrix in the rather roundabout way another thing we can use is scan so we can get normally prefixes of a vector like this if we instead of concatenate so this is a cumulative concatenation we do a cumulative swapped concatenation then we get these reversed prefixes instead okay so if we can have a way to get reverse prefixes and we have a way to get one followed by a bunch of zeros then these give us our rows and we just need to mix and so we can write this as an as a function the conclusion swapped scan and off the take of one so this is an end take one and then we mix that then we just need to put and a top here so we have two functions after each other and here we got our identity function in a very roundabout manner but lots of fun again and now let's move over to the key operator which we can also use for this so we can generate our our indices like this and then we can ask the key operator what are the indices so let's put it like this but now so this is saying index one is found or the number one is found at position one the number two is filter under position two only number three is found at position three that means the alpha here is one and omega is what f plus 2 omega is 2 and so on now we can use take here and that gives us these vectors and we can see how where we're going with this we can then reverse this and now we just have the problem of the sign so we can take the sign of all of this and we need to stack them on top of each other as well so we could mix it like this but there's a better way but not enclosing them we already get the mix for free and now we just need to get the sign here and then we can make this tacit because it fits very nicely it is the reversal on top of the taking of these two arguments and that gives us our identity matrix it's not quite a function yet but we can make it so by combining the key with the indices and now we have our identity matrix generator in a totally obscure way that nobody will be able to understand don't do this in production code let's make it worse let's start again with um with this construct and here we are only interested in the right argument so that gives us these vectors of um indices one by itself two beta three beta four by five by itself and remember we used the uh iota underbar the where inverse to generate a boolean array and that has ones in those positions there's only one position in each one but we can still do this so this gives us these vectors and yes you recognize this remove the enclosure and we've got our identity matrix and we can combine this we can make the operand test it simply by saying that it's this where inverse on top of the right argument we have to have that because there's a left argument as well and so this is our function and that works again don't do this in production code but it sure is fun to look at and then somebody asked during the live chat event if we can't use complex numbers for this and of course we can use complex numbers for this okay let's get started so we have these indices and let's make a table of complex numbers so we do the other product of the real part plus the imaginary part so we multiply the imaginary units with these indices oops there shouldn't be n here it should be that and that gives us a complex number table so this is 1 plus 1 i 2 plus and 1 plus 2 i 1 plus 3 i next row 2 plus 1 i and so on and now what we need to do is we want to find out the ones that are down the diagonal and both actually down the diagonal we can kind of see the angle of them but it also happens to be that in a complex plane these will have an um an angle or an also known as the argument which is 45 degrees or a a quarter of pi so we can ask for the argument of that and we can see that going down the diagonal they all have that 0.785 and so on now we can multiply that by or or rather sorry divide pi by that so the same thing as taking the reciprocal and multiplying by pi and then you can see that gives four and now we can say where is 4 equal to that and that gives us our identity matrix so this is our full function would be to we could either do iota omega here or we could just use omega and put iota outside that as in the top and we've got our identity matrix producing function here in a terrible way using complex numbers and as if that wasn't enough let's go in and modify this a bit so starting again from here with our table of complex numbers we can also ask what is the absolute value or the magnitude of these numbers and since they are on the 45 degree angle that means that the horizontal and vertical parts in this right angle triangle are equal to each other that means that the diagonal's length has to be a multiple of the square root of 2. so we can ask what is the divisional remainder when these numbers are divided by the square root of 2 and if there is no remainder then and we are at on the diagonal so we can compare this with zero and we get our identity matrix using complex numbers that's enough fun and what you should do of course is use the solution where we take the argument twice reshape with one plus the argument to take over of and of one or you can use the tested version where it's a self-concatenation of the reshape of the incremented number take off one or as a constant or you can use the sign or the tally if you really want to go there but these would be the industrial strength versions you can also go up and if you don't like parentheses like i personally don't do then you can swap the arguments of this take as well that's perfectly acceptable as well thank you for watching
