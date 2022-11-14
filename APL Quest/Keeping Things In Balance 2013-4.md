## [ Keeping Things In Balance](https://problems.tryapl.org/psets/2013.html?goto=P4_Keeping_Things_In_Balance)

**Problem:** Write an APL dfn which returns a 1 if the opening and closing parentheses in a character vector are balanced, or a zero otherwise.
**Video:** https://youtu.be/El0_RB4TTPA
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/4.apl

**Example Solutions:**
```APL
	Di ← {1 ¯1 0['()'⍳⍵]} ⍝ Indexing into an array, 1 is left paren, ¯1 is Right and 0 is all other characters. 
	
	L ← {+/2</1,⍨' '=⍵} ⍝ fastest solution append a bit
```

**Quotes:**
Convert input into a normalized form. 
If an element isn't found a lookup array. Then we get the next index. 

**Comment:** 
```APL
↑⍤,⍥⊂ ⍝ concatenate enclosure over the original, (mix)Increase the rank - used for vector - Laminate for Matrix
```

**Glyphs Used:**
[Index of](https://aplwiki.com/wiki/Index_Of)
[Bracket Indexing](https://xpqz.github.io/learnapl/indexing.html#bracket-indexing)  - Mapping 
[Mix](https://aplwiki.com/wiki/Mix)
[Rank](https://aplwiki.com/wiki/Rank_(operator))
[Concatenation](https://aplwiki.com/wiki/Catenate)
[Over](https://aplwiki.com/wiki/Over)
[Enclose](https://aplwiki.com/wiki/Enclose)
[Outer Product](https://aplwiki.com/wiki/Outer_Product) using a comparison =
[Laminate](https://aplwiki.com/wiki/Catenate) - Catenate First - Add a line to a matrix
[Reduce](https://aplwiki.com/wiki/Reduce) - Vertical Minus Reduction



[Not equal to](https://aplwiki.com/wiki/Not_Equal_to)
[Partition](https://aplwiki.com/wiki/Partition) - Uses ones to Partition
[Tally](https://aplwiki.com/wiki/Tally)
[Bind](https://aplwiki.com/wiki/Bind)
[String Search](http://help.dyalog.com/18.0/index.htm#Language/System%20Functions/r.htm) - ⎕S
[Verify Fixed Input](http://help.dyalog.com/18.0/index.htm#Language/System%20Functions/vfi.htm?Highlight=Verify%20and%20Fix%20Input) - ⎕VFI
[First](https://aplwiki.com/wiki/First)
[Reduce](https://aplwiki.com/wiki/Reduce) - Pair wise and plus reduction
[Ravel](https://aplwiki.com/wiki/Ravel) - adding a space or a 1
[Commute](https://aplwiki.com/wiki/Commute) aka Selfie
[Bracket Indexing](https://xpqz.github.io/learnapl/indexing.html#bracket-indexing) - Generating Random string using roll and reshape
[Roll](https://aplwiki.com/wiki/Roll)
[Reshape](https://aplwiki.com/wiki/Reshape)

**Concepts Used:**
[Comparison Function](https://aplwiki.com/wiki/Comparison_function)
[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Boolean Mask](https://aplwiki.com/wiki/Boolean)
[Reduction](https://aplwiki.com/wiki/Reduce)
[Regular Expressions](https://xpqz.github.io/cultivations/Regex.html)
[Windowed Reduce](https://aplwiki.com/wiki/Windowed_Reduce) - N-wise Reduction (pair-wise with left argument of 2)
[Performance](https://aplwiki.com/wiki/Performance#Performant_usage)
[Dfns Workspace](https://aplwiki.com/wiki/Dfns_workspace)
[CMPX](http://dfns.dyalog.com/n_cmpx.htm)