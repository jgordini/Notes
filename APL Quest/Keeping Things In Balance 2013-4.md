## [ Keeping Things In Balance](https://problems.tryapl.org/psets/2013.html?goto=P4_Keeping_Things_In_Balance)

**Problem:** Write an APL dfn which returns a 1 if the opening and closing parentheses in a character vector are balanced, or a zero otherwise.

**Video:** https://youtu.be/El0_RB4TTPA
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/4.apl

**Example Solutions:**
```APL
	Di ← {1 ¯1 0['()'⍳⍵]} ⍝ Indexing into an array, 1 is left paren, ¯1 is Right and 0 is all other characters. 
	Df ← '('∘= - =∘')' ⍝ Tacit, subtracts the comparisons to get the depth changes. 
	Bn ← (¯1∊+\)⍱0≠+/ ⍝ checks for no ¯1 and no 0 in scan
	F ← (¯1∘∊⍱0≠⊢/)'('∘=+\⍤-=∘')' ⍝ Moves scan to be atop on comparisons +\⍤ 
	```

**Parenthesis depth changes**
Examples:
```APL
Di ← {⍵ ↑⍤,⍥⊂ 1 ¯1 0['()'⍳⍵]} ⍝ Convert the data to norrmalized form. 
Do ← -⌿'()'∘.=⊢
Df ← '('∘= - =∘')'
```
**Di**
1. `['()'⍳⍵]` - [Index of](https://aplwiki.com/wiki/Index_Of) `⍳` shows a 1 if left paren, 2 if right paren, and 3 if not found. 
2. `1 ¯1 0` - map the result of step 1  to (1 left,  -1 right, 0 not found)
3. `↑⍤,⍥⊂` -  [Enclose](https://aplwiki.com/wiki/Enclose) `⊂`  - Create a nested scaler  [Over](https://aplwiki.com/wiki/Over)  `⍥` -  Preprocess the right argument  [Merge Axis](https://aplwiki.com/wiki/Rank_(operator)#Merge_axes) -  `⍤,` concatenate the two axis  [Mix](https://aplwiki.com/wiki/Mix)  `↑` - trades one level of [depth](https://aplwiki.com/wiki/Depth) (nesting) into one level of [rank](https://aplwiki.com/wiki/Rank). 

**Do**
1. `'()'∘.=⊢` Applying an [Outer Product](https://mastering.dyalog.com/Operators.html?highlight=outer%20product#outer-product) using a comparison `=` Because this is a tacit function [Right Tack](https://aplwiki.com/wiki/Identity) acts as omega `⍵` and just returns the function it is pointing to. 
2. `'()'∘.=⊢` The `'()'` is the comparison that the outer product is applying against the identity. This creates a table. 
3. The first row a [Boolean Mask](https://aplwiki.com/wiki/Boolean) of 1's (true) where the left parenthesis is found and 0 (false) where is it not found. 
4. The second row is 1's where the right parenthesis is found. 
5. The result of step 2 is already a matrix. So we can use [Table](https://xpqz.github.io/cultivations/Functions7.html#table) `⍪`  - to ravel the major cells of the array and make each one of them into a row with the identity on top. This is just explanatory. 
6. -⌿ Subtracting the bottom row from step 2 from the top row in step 2 using a vertical minus [Reduction](https://aplwiki.com/wiki/Reduce) gives us the  depth changes.  

**Df**
1. We can do the two [Comparison Functions](https://aplwiki.com/wiki/Comparison_function) independently
2. `'('∘=` Making a boolean mask of the left parenthesis. 
3. `=∘')'` Making a boolean mask of the right parenthesis.
4. After subtracting the two results to give us the depth changes we can turn this into a [Tacit Function](https://aplwiki.com/wiki/Tacit_programming) 
5.   [Bind](https://aplwiki.com/wiki/Bind) `∘` is used to create a derived function with a single constant argument for each comparison. 
6. This creates a [3-train Fork](https://aplwiki.com/wiki/Train#3-trains) where the two outer functions are applied first, and their results are used as arguments to the middle function in this case subtract `-`. 

**Performance**
Examples:
```APL
'turtle' 'joy' 'cmpx'⎕cy'dfns'
(y n)←(⊢⍴⍨100×⍴)⍤⎕VR¨'turtle' 'joy'
cmpx'D',¨'iof',¨⊂' y'
```

We can evalute the performance of each function by importing the [CMPX](http://dfns.dyalog.com/n_cmpx.htm) function from the [DFNS](http://dfns.dyalog.com/n_contents.htm) library. 

1.  We can  [copy](http://help.dyalog.com/latest/Content/Language/System%20Functions/cy.htm) `⎕cy` CMPX  along with TURTLE and JOY from the DFNS library into our workspace.
2. We know that Turtle has matched parenthesis and Joy has unmatched parenthesis so we can use these two functions as our test cases. 
3. In the next line we are taking the [Vector Representation](https://xpqz.github.io/cultivations/CodeManagement.html?highlight=vr#visual-representation-vr) - ⎕VR of [Each](https://aplwiki.com/wiki/Each) `¨` function.
4. [Rank](https://aplwiki.com/wiki/Rank_(operator)) `⍤` - applies its left [operand](. https://aplwiki.com/wiki/Operand "Operand") function to [cells](https://aplwiki.com/wiki/Cells "Cells") of its arguments specified by its right operand array.
5. `⊢⍴⍨100×⍴` Using [Commute](https://aplwiki.com/wiki/Commute) `⍨`  - we first take the [Shape](https://aplwiki.com/wiki/Shape) of the idenitity `⊢⍴` and and then  [Reshape](https://aplwiki.com/wiki/Reshape) `100×⍴` it using 100 times it's current shape. 
6.  In the next line we are doing some meta programming to use cmpx to evalute the performance of each function. 
7. Every function begins with a D. We [Concatenate](https://aplwiki.com/wiki/Catenate)  [Each](https://aplwiki.com/wiki/Each) `,¨` of the suffixes 'iof' and then  [Concatenate](https://aplwiki.com/wiki/Catenate)  [Each](https://aplwiki.com/wiki/Each) `,¨` to the entire function ' y' using [Enclose](https://aplwiki.com/wiki/Enclose) `⊂` - An enclosed array is a [scalar](https://aplwiki.com/wiki/Scalar "Scalar"), which is subject to [scalar extension](https://aplwiki.com/wiki/Scalar_extension "Scalar extension").

**Balanced?**
Comment:
```
We are checking if two condtions are realized. 
1. Our final parenthesis level needs to be zero. 
2. As our function proceeds our parenthesis level should not drop below zero. 
3. Both expressions are then evaluted for performance using simlar steps to above
```
Examples:
```APL
Ba ← (∧/0≤+\)∧0=+/
Bn ← (¯1∊+\)⍱0≠+/
```
BA
1. `∧/` [And](https://aplwiki.com/wiki/And) [Reduction](https://aplwiki.com/wiki/Reduction "Reduction")  tests if it is true for ALL that the parenthesis depth is greater than or equal to zero. 
2.  `0≤+\` Plus [Scan](https://aplwiki.com/wiki/Scan) `+\` gives us the parenthesis depth. The [Comparison Function](https://aplwiki.com/wiki/Comparison_function) `0≤` checks if zero is less than or equal to the running sum. 
3. `∧0=+/` [And](https://aplwiki.com/wiki/And)  also checking if it is true that zero = the full sum `0=+/`. 
4. Both conditions must be true for BA to return 1 (for true).

BN 
1. `¯1∊+\` Checks if -1 is a [member](https://aplwiki.com/wiki/Membership) `∊` of the running sum or [Scan](https://aplwiki.com/wiki/Scan) `+\`. 
2.  `0≠+/` Checks if zero is not equal to the total. 
3. `⍱` [Nor](https://aplwiki.com/wiki/Nor) tests if neither argument (Step 1 or 2) is true: it returns 1 if both are false (0) and 0 if at least one is true (1)

**Find and Replace**
Comment:
```APL
Regular Expressions
```

**Quotes:**

If an element isn't found a lookup array. Then we get the next index. 
Applying a function to a scaler doesn't change the function and will let APL evaluate it. 

**Comment:** 
```APL

⊢/ ⍝ Last element
```

**Glyphs Used:**
[Index of](https://aplwiki.com/wiki/Index_Of) `⍳`
[Bracket Indexing](https://xpqz.github.io/learnapl/indexing.html#bracket-indexing)  [ ]  - Mapping 
[Mix](https://aplwiki.com/wiki/Mix)  `↑`
[Merge Axis](https://aplwiki.com/wiki/Rank_(operator)#Merge_axes)  ,⍤
[Over](https://aplwiki.com/wiki/Over)  `⍥`
[Enclose](https://aplwiki.com/wiki/Enclose) `⊂` - creates a nested scalar by wrapping its argument under one level of nesting

[Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.`  - using a comparison `∘.=`
[Laminate](https://aplwiki.com/wiki/Catenate)  `⍪` Catenate First - Add a line to a matrix
[Reduce](https://aplwiki.com/wiki/Reduce) `⌿` Vertical Minus Reduction
[Bind](https://aplwiki.com/wiki/Bind) `∘`

[Vector Representation](https://xpqz.github.io/cultivations/CodeManagement.html?highlight=vr#visual-representation-vr) - ⎕VR`
[Rank](https://aplwiki.com/wiki/Rank_(operator))  `⍤` - applies its left operand function to cells of its arguments specified by its right operand array. 
[Identity](https://aplwiki.com/wiki/Identity) `⊢`
[Reshape](https://aplwiki.com/wiki/Reshape) `⍴`
[Commute](https://aplwiki.com/wiki/Commute) `⍨`  - aka Selfie or Swap
[Tally](https://aplwiki.com/wiki/Tally) `≢`
[Each](https://aplwiki.com/wiki/Each) `¨`
[Scan](https://aplwiki.com/wiki/Scan) `+\`  - Plus Scan
[Sum](https://aplwiki.com/wiki/Add#Reduction) `+/` - [Reduction](https://aplwiki.com/wiki/Reduction "Reduction") with Add gives the sum of the whole list.
[And](https://aplwiki.com/wiki/And) `∧` - tests if both arguments are true: it returns 1 if both are true (1) and 0 if one or both are false (0)
[Nor](https://aplwiki.com/wiki/Nor) `⍱` - tests if neither argument is true: it returns 1 if both are false (0) and 0 if at least one is true (1)
[Enlist](https://aplwiki.com/wiki/Enlist)  `∊` - Enlist flattens over all layers of nesting
[Intersection](https://aplwiki.com/wiki/Intersection)  `∩`
[Match](https://aplwiki.com/wiki/match) `≡`
[Power Match](https://aplwiki.com/wiki/Power_(operator))  `⍣≡` - Iterating until a fixed point is reached.
[Atop](https://aplwiki.com/wiki/Atop_(operator)) `⍤` - takes two (monadic) functions and glues them together.  Uses the left operand to process the right
<mark style="background: #BBFABBA6;">Regular Expressions</mark>
[Variant](https://aplwiki.com/wiki/Variant) `⍠` - Switch Regex to plain text
[Find](https://aplwiki.com/wiki/find) `⍷`
[Rotate](https://aplwiki.com/wiki/rotate) `⌽`
[Or](https://aplwiki.com/wiki/or) `∨`
[Compress](https://aplwiki.com/wiki/Replicate) `/` -  Outside of APL, [filter](https://en.wikipedia.org/wiki/filter_(higher-order_function) "wikipedia:filter (higher-order function)") typically provides the functionality of Compress
[Execute](https://aplwiki.com/wiki/execute) ⍎
[Diamond](https://aplwiki.com/wiki/Statement_separator) ⋄ - Statement Seperator
[Format](https://aplwiki.com/wiki/format) ⍕ - Flatten
[First](https://aplwiki.com/wiki/first) ⊃

**Concepts Used:**
[Comparison Function](https://aplwiki.com/wiki/Comparison_function)
[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Boolean Mask](https://aplwiki.com/wiki/Boolean)
[Reduction](https://aplwiki.com/wiki/Reduce)
[Fork](https://aplwiki.com/wiki/Train#3-trains)
[Dfns Workspace](https://aplwiki.com/wiki/Dfns_workspace)
[Boolean Functions](https://aplwiki.com/wiki/Boolean#Boolean_functions)
[Logical Conjunction](https://en.wikipedia.org/wiki/Logical_conjunction)
[Logical Nor](https://en.wikipedia.org/wiki/Logical_NOR)
[Fork and Atop Problem](https://aplwiki.com/wiki/Train#Problems_caused_by_function-operator_overloading)
[Regular Expressions](https://xpqz.github.io/cultivations/Regex.html)
[Intersection](https://en.wikipedia.org/wiki/Intersection_(set_theory))
[Error Guard](https://aplwiki.com/wiki/Dfn#Error-guards) `::`
[Performance](https://aplwiki.com/wiki/Performance#Performant_usage)
[CMPX](http://dfns.dyalog.com/n_cmpx.htm)


**Reference:**
[Sixteen APL Amuse-Bouches](http://archive.vector.org.uk/art10501480) - #5
[Learn Regular Expressions](https://www.regular-expressions.info/)