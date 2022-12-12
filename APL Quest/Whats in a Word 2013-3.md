## [Whats in a Word](https://problems.tryapl.org/psets/2013.html?goto=P3_What_Is_In_a_Word)

**Problem:** Write a dfn which returns the number of words in the given character scalar or vector.

**Video:** https://youtu.be/MgkM2qCPWas 
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/3.apl

**Example Solutions:**
```APL
	F ← ≢' '∘≠⊆, ⍝ Tacit - binding the space to the not equal to make monadic. 
	L ← {+/2</1,⍨' '=⍵} ⍝ fastest solution append a bit
```

**Examples:**

```APL
F ← ≢' '∘≠⊆, ⍝ Tacit - binding the space to the not equal to make monadic. 
```
1.  Split on sequences of spaces
2. `' '=s` [Equal To](https://aplwiki.com/wiki/Equal_to) compares arrays one [element](https://aplwiki.com/wiki/Element "Element") at a time. Returns a boolean vector of 1 for match and 0 for no-match. 
3. `⊆` [Partition](https://aplwiki.com/wiki/Partition)  splits on the 0s when the left argument is boolean.. So we use [Not equal to](https://aplwiki.com/wiki/Not_Equal_to) `≠⊆` to create runs of 1s. 
4. `⊆` [Partition](https://aplwiki.com/wiki/Partition) also requires an axis. So to use a [Comparison Function](https://aplwiki.com/wiki/Comparison_function) on a scaler we must [Ravel](https://aplwiki.com/wiki/Ravel)  `⊆,`first. 
5. `' '∘≠` We [Bind](https://aplwiki.com/wiki/Bind) the space to the [Not equal to](https://aplwiki.com/wiki/Not_Equal_to) to achieve a monadic function. 
6. `≢` Last we [Tally](https://aplwiki.com/wiki/Tally) to count the number of major cells or items. 

```APL
G ← ≢'[^ ]+'⎕S 3
```

1. Use [Regular Expressions](https://xpqz.github.io/cultivations/Regex.html)
2. `⎕S` [String Search](http://help.dyalog.com/18.0/index.htm#Language/System%20Functions/r.htm) 



**Comment:** 
```APL
t←'abc '[?1e6⍴4] ⍝ Interesting use of bracket index to generate random words array
```

**Glyphs Used:**
<mark style="background: #BBFABBA6;">Split on Sequence of Spaces</mark>
[Not equal to](https://aplwiki.com/wiki/Not_Equal_to)
<mark style="background: #BBFABBA6;">Partition Function</mark>
[Partition](https://aplwiki.com/wiki/Partition) - Uses ones to Partition
[Tally](https://aplwiki.com/wiki/Tally)
[Bind](https://aplwiki.com/wiki/Bind)
[String Search](http://help.dyalog.com/18.0/index.htm#Language/System%20Functions/r.htm) - ⎕S
[Verify Fixed Input](http://help.dyalog.com/18.0/index.htm#Language/System%20Functions/vfi.htm?Highlight=Verify%20and%20Fix%20Input) - ⎕VFI
[First](https://aplwiki.com/wiki/First)
<mark style="background: #BBFABBA6;">Compating Adjacent Elements</mark>
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