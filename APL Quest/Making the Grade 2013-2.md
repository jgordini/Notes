## [Making the Grade](https://problems.tryapl.org/psets/2013.html?goto=P2_Making_The_Grade)

**Problem:** Write a dfn which returns the percent (from 0 to 100) of passing (65 or higher) grades in a vector of grades.

**Video:** https://youtu.be/pxo2BtoMxP4
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/2.apl

**Example Solutions:**
2 Scaler functions and a reduction over a vectorized operation. 
```APL
F ← {100×(+/⍵≥65)÷≢⍵}
J ← 100×+.≥∘65÷≢ ⍝ Tacit
```

**Explanation:**
```APL
F ← {100×(+/⍵≥65)÷≢⍵}
```

1.  `(+/⍵≥65)` use [greater than or equal to](https://aplwiki.com/wiki/Greater_than_or_Equal_to) as a [Comparison Function](https://aplwiki.com/wiki/Comparison_function) return ing a boolean vector of 1 if true and 0 if false. Then [sum](https://aplwiki.com/wiki/Reduce) the result - `+/`. 
2. `÷≢⍵`  [Tally](https://aplwiki.com/wiki/Tally) the length of your argument and divde that by the result in step 1. 
3. Multiply this by 100 to get your percentage of passing grades. 

**Performance:**
```APL
F ← {100×(+/⍵≥65)÷≢⍵}
G ← {100×+/(⍵≥65)÷≢⍵}
H ← {+/100×(⍵≥65)÷≢⍵}
```
Note that it does not matter where we do the sum mathmatically. However there are siginificant performance penalties for summing after the division.

```APL
s←?1e6⍴100
'cmpx'⎕cy'dfns'
cmpx'F s' 'G s' 'H s'
```
We can evalute the performance of each function by importing the [CMPX](http://dfns.dyalog.com/n_cmpx.htm) function from the [DFNS](http://dfns.dyalog.com/n_contents.htm) library. 
1.  We [Roll](https://aplwiki.com/wiki/Roll)1 million `1e6` random numbers between 1 and 100
2.  We [copy](http://help.dyalog.com/latest/Content/Language/System%20Functions/cy.htm) `⎕cy` CMPX from the DFNS library into our workspace
3.  We use cmpx to evalute the performance of each function. With the first function as our baseline. 




**Quotes:**
*We are dealing with a scaler (65) and a vector (Scores). We should notice this pattern. We have a sum over a comparison of vectors. When we have that, we should think, Inner Product.*

*65 is a bound constant to the inner product.* 

**Comment:** 
```APL
0,⍳64 ⍝ Raveld with zero becuase ⎕IO←1
```

**Glyphs Used:**
[Roll](https://aplwiki.com/wiki/Roll)
[Reshape](https://aplwiki.com/wiki/Reshape)
[Tally](https://aplwiki.com/wiki/Tally)
[Greater than or Equal to](https://aplwiki.com/wiki/Greater_than_or_Equal_to)
[Scan](https://aplwiki.com/wiki/Scan) - Plus Scan
[Quad](https://aplwiki.com/wiki/Quad_name)
[Bind](https://aplwiki.com/wiki/Bind)
[Atop](https://aplwiki.com/wiki/Atop_(operator))
[Identity](https://aplwiki.com/wiki/Identity)
[Diamond](https://aplwiki.com/wiki/Statement_Separator)
[Ravel](https://aplwiki.com/wiki/Ravel)
[Iota](https://aplwiki.com/wiki/Index_Generator)
[Without](https://aplwiki.com/wiki/Without) aka not
[Over](https://aplwiki.com/wiki/Over)
[Indices](https://aplwiki.com/wiki/Indices) aka Where

**Concepts Used:**
[Comparison Function](https://aplwiki.com/wiki/Comparison_function)
[Dfn](https://aplwiki.com/wiki/Dfn)
[Dfns Workspace](https://aplwiki.com/wiki/Dfns_workspace)
[Scientific Notation](https://mastering.dyalog.com/Data-and-Variables.html#data-and-variables-representation-of-numbers)
[CMPX](http://dfns.dyalog.com/n_cmpx.htm)
[Scalar Function](https://aplwiki.com/wiki/Scalar_function)
[Reduction](https://aplwiki.com/wiki/Reduce)
[Inner Product](https://aplwiki.com/wiki/Inner_Product)
[Dot Product](https://en.wikipedia.org/wiki/Dot_product)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Function Atop Tack](https://mastering.dyalog.com/Tacit-Programming.html?highlight=atop#function-atop-tack)
[Default Left Arguments](https://aplwiki.com/wiki/Dfn#Default_left_arguments)
[Fork](https://aplwiki.com/wiki/Train#2-trains) - 2 Train
[Boolean Mask](https://aplwiki.com/wiki/Boolean)
[Code Reuse](https://en.wikipedia.org/wiki/Code_reuse)





