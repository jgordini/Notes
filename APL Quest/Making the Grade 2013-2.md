## [Making the Grade](https://problems.tryapl.org/psets/2013.html?goto=P2_Making_The_Grade)

**Video:** https://youtu.be/pxo2BtoMxP4
**Problem:** Write a dfn which returns the percent (from 0 to 100) of passing (65 or higher) grades in a vector of grades.
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/2.apl

**Example Solutions:**
2 Scaler functions and a reduction over a vectorized operation. 
```APL
F ← {100×(+/⍵≥65)÷≢⍵}
J ← 100×+.≥∘65÷≢ ⍝ Tacit
```

**Quotes:**
*We are dealing with a scaler (65) and a vector (Scores). We should notice this pattern. We have a sum over a comparison of vectors. When we have that, we should think, Inner Product.*

*65 is a bound constant to the inner product.* 

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


--
[Iota](https://aplwiki.com/wiki/Index_Generator)
[Commute](https://aplwiki.com/wiki/Commute) aka Selfie
[Indices](https://aplwiki.com/wiki/Indices) aka Where
[Residue](https://aplwiki.com/wiki/Residue) aka Modulus 
[Take](https://aplwiki.com/wiki/Take)
[Scan](https://aplwiki.com/wiki/Scan)
[Power](https://aplwiki.com/wiki/Power_(function))
[Branch](https://aplwiki.com/wiki/Branch)



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
[Parity - Modulous 2](https://xpqz.github.io/cultivations/Functions2.html#magnitude-residue)
[Fill Elements](https://aplwiki.com/wiki/Fill_element) - Padding with zeros
[Control Structure](https://aplwiki.com/wiki/Control_structure)
[Fork](https://aplwiki.com/wiki/Train#3-trains) - 3 Train





