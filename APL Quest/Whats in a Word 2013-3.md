## [Whats in a Word](https://problems.tryapl.org/psets/2013.html?goto=P3_What_Is_In_a_Word)

**Problem:** Write a dfn which returns the number of words in the given character scalar or vector.

**Video:** https://youtu.be/MgkM2qCPWas 
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/3.apl

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

1. Use [Regular Expressions](https://xpqz.github.io/cultivations/Regex.html) You can use [regexr.com](https://regexr.com/) to evaluate.
2. `⎕S` [String Search](http://help.dyalog.com/18.0/index.htm#Language/System%20Functions/r.htm) -regex enclosed in single quotes
3. `[^ ]+` Matches anything that is not a space
4. [Transformation Codes](http://help.dyalog.com/18.0/index.htm#Language/System%20Functions/r.htm) for each match in the input document, a numeric scalar or vector of the same shape as the transformation codes is created.
5. `3`  - Pattern number which matched the input document, origin Zero
6.  [Tally](https://aplwiki.com/wiki/Tally) to count the number of patterns

```APL
H ← ≢∘⊃⎕VFI
```
1. `⎕VFI` - [Verify and Fix Input](https://xpqz.github.io/cultivations/Constants.html?highlight=fix%20input#verify-and-fix-input-vfi) - takes a string and returns two lists. It cuts the string into space separated fields. Then it attempts to convert each field to a number.
2. `⊃` - Monadic [Pick](https://xpqz.github.io/learnapl/indexing.html?highlight=first#pick) picks the first element. In this case the first vector.
3. `≢∘⊃` - [Bind](https://mastering.dyalog.com/Tacit-Programming.html?highlight=bind#binding) When we use the operator _bind_, we create a single derived function that is monadic.  That way we can give it a name. 

```APL
I ← {+/2</' '≠' ',⍵}
J ← {+/2</0,' '≠⍵}
K ← {(⊃m)++/2</m←' '≠,⍵}
L ← {+/2</1,⍨' '=⍵}
```

1. `' '≠` -  [Boolean Mask](https://aplwiki.com/wiki/Boolean) showing a 1 (true) when we don't have a space. 
2. `2</` - N wise [Reduce](https://aplwiki.com/wiki/Reduce) comparing adjacent elements in pairs of two. Only true when 0 on left and 1 on right. 
3. `' ',` - Inserting a space at the beginning using [Catenate](https://xpqz.github.io/cultivations/Functions7.html#catenate)
4. `+/` - Plus [Reduction](https://aplwiki.com/wiki/Reduce) on the result of Step 3 returns the number of words. 
5. `0,` - In J for performance instead of adding a space at the begining we are adding a zero to the result of the comparison. 
6. `(⊃m)` - In K we are taking the [First Element](https://aplwiki.com/wiki/first) ⊃ of the mask and adding that to the sum. Avoiding re-writing the array for a performance benefit. If `m` is 0 there are leading spaces if `m` is 1 there is a word. 
7. `1,⍨' '=⍵` - In L we are appending a 1 instead of prepending for performance. `' '=⍵`  here a 1 indicates a space and going from 0 to 1 is the end of a word.  We are doing a flipped concatination using [Swap](https://aplwiki.com/wiki/Commute) to add a 1 to the end instead of the beginning. 

```APL
t←'abc '[?1e6⍴4] ⍝ Interesting use of bracket index to generate random words array
'cmpx'⎕cy'dfns'
cmpx'F t' 'G t' 'H t' 'I t'
```

We can evalute the performance of each function by importing the [CMPX](http://dfns.dyalog.com/n_cmpx.htm) function from the [DFNS](http://dfns.dyalog.com/n_contents.htm) library. 

1.  Using the 4 characters `'abc '` abc and space.  
2. We use [Bracket Indexing](https://xpqz.github.io/learnapl/indexing.html#bracket-indexing) `[]` to randomly `?` pick one of the 4 characters a million `1e6` times. 
3.  [Reshape](https://aplwiki.com/wiki/Reshape) ⍴ is being used to limit the index to 4. 
4.  We can then [copy](http://help.dyalog.com/latest/Content/Language/System%20Functions/cy.htm) `⎕cy` CMPX from the DFNS library into our workspace
5.  We use cmpx to evalute the performance of each function. With the first function as our baseline. 

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
[Commute](https://aplwiki.com/wiki/Commute) aka Swap
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