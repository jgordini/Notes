## [Identity Crisis](https://problems.tryapl.org/psets/2013.html?goto=P5_Identity_Crisis)

**Problem:** An identity matrix is a square matrix (table) of 0 with 1’s in the main diagonal. Write an APL dfn which produces an n×n identity matrix.

**Video:** https://youtu.be/vVaZ3wEdmpQ
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/5.apl

**Example Solutions:**
```APL
	I←∘.=⍨⍳ ⍝ equality table for one dimensional indices
	J←{⍵ ⍵⍴(⍵+1)↑1} ⍝ overtake to insert 1 before n 0s
	```

**Quotes:**


**Comment:** 
```APL
=/¨  ⍝ Compare Each
∘.=⍨ ⍝ Equailty Table using same indeces for both sides
1 1⍉s ⍝ Selects the diagonal of s
,⍨¨ ⍝ Catenate each to itself
```

**Glyphs Used:**
[Catenate](https://aplwiki.com/wiki/Catenate) `,`
[Index of](https://aplwiki.com/wiki/Index_Of) `⍳`
[Comparison Function](https://aplwiki.com/wiki/Comparison_function) =
[Compress](https://aplwiki.com/wiki/Replicate) `/` - filters the right argument `=/¨` compare each
[Each](https://aplwiki.com/wiki/Each) `¨`
[Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.` 
[Commute](https://aplwiki.com/wiki/Commute) `⍨`  - aka Selfie or Swap
[Dyadic Transpose](https://xpqz.github.io/learnapl/dyadictrn.html?#dyadic-transpose-ab) ``x⍉y`` - allows you to select diagonals by giving one or more dimensions equal mapping
[Reshape](https://aplwiki.com/wiki/Reshape) `⍴`
[At](https://xpqz.github.io/cultivations/Operators.html#at) `@` - What’s on its left gets done at the position indicated by its right operand. 
[Identity](https://aplwiki.com/wiki/Identity) `⊢`
[Where](https://aplwiki.com/wiki/Indices) `⍸` - returns the indices of a boolean array - mondadic
[Power](https://aplwiki.com/wiki/Power_(operator)) `⍣¯1` - used to access function inverses
[Power(Function)](https://aplwiki.com/wiki/Power_(function)) `*` -  `X*Y` is `X` raised to the power `Y`
[Overtake](https://aplwiki.com/wiki/Take#Overtaking) `↑` - A length larger than the argument length causes [fills](https://aplwiki.com/wiki/Fill_element "Fill element") to be inserted
[Bind](https://aplwiki.com/wiki/Bind) `∘`
[Constant](https://xpqz.github.io/cultivations/Operators.html#constant-a) `A⍨` - always returns the operator array
[Signum](https://aplwiki.com/wiki/Signum) `×A` - Sign of number  - on a real argument are `0`, `1`, and `¯1` (zero, positive and negative)
[Tally](https://aplwiki.com/wiki/Tally) `≢`
[Expand](https://xpqz.github.io/cultivations/Functions7.html?#expand) `\` - copies each [element](https://aplwiki.com/wiki/Element "Element") of the right [argument](https://aplwiki.com/wiki/Argument "Argument") a given number of times
[Roll](https://aplwiki.com/wiki/Roll) `?0` - When zero Roll chooses a floating-point number between 0 and 1



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
[Diamond](https://aplwiki.com/wiki/Statement_separator) ⋄ - Statement Seperator
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
[Identity Matrix](https://en.wikipedia.org/wiki/Identity_matrix)
[Dfn](https://aplwiki.com/wiki/Dfn)
[Radix](https://en.wikipedia.org/wiki/Radix)
[Index Origin](https://aplwiki.com/wiki/Index_origin) - Generating Functions with that work with 0 or 1 origin
[Ravel Order](https://aplwiki.com/wiki/Ravel_order)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)




[Dfn](https://aplwiki.com/wiki/Dfn)
[Boolean Mask](https://aplwiki.com/wiki/Boolean)
[Reduction](https://aplwiki.com/wiki/Reduce)
[Fork](https://aplwiki.com/wiki/Train#3-trains)
[Dfns Workspace](https://aplwiki.com/wiki/Dfns_workspace)
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