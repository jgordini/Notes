## [Whats in a Word](https://problems.tryapl.org/psets/2013.html?goto=P3_What_Is_In_a_Word)

**Problem:** Write a dfn which returns the number of words in the given character scalar or vector.
**Video:**https://youtu.be/MgkM2qCPWas 
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/3.apl

**Example Solutions:**
2 Scaler functions and a reduction over a vectorized operation. 
```APL
F ← {100×(+/⍵≥65)÷≢⍵}
J ← 100×+.≥∘65÷≢ ⍝ Tacit
```

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






