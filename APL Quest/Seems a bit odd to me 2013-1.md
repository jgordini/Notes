## [Seems a Bit Odd To Me](https://problems.tryapl.org/psets/2013.html?goto=P1_Seems_a_Bit_Odd_To_Me)

**Problem:** Write a dfn to produce a vector of the first n odd numbers.

**Video:** https://youtu.be/Mj4wyLKrBho
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/1.apl

**Example Solutions:**
```APL
F←{1-⍨2×⍳⍵}
G←(⍸1 0⍴⍨2×⊢) ⍝ Tacit
H←{⍸2|⍳2×⍵} ⍝ Any ⎕IO
I←(⍳+⍳-≢) ⍝ Tacit
```

**Explanation:**
```APL
F←{1-⍨2×⍳⍵}
```
1. `⍳⍵` - Use [Iota](https://aplwiki.com/wiki/Index_Generator) to generate the first `⍵` natural numbers (1, 2, 3, 4 etc.)
2.  `1-⍨2×` - [Swap](https://xpqz.github.io/learnapl/manip.html?#selfie-commute-constant)  ⍨ - Preserves the right to left order. - parsed as `(2×⍳5)-1`  
3. Multiply the values by 2
4. Subtract one from each of the array values.

```APL
G←(⍸1 0⍴⍨2×⊢)
```
1.  `(2×⊢)`- parses as (2×⍵) -  [Identity](https://aplwiki.com/wiki/Identity) replaces `⍵` - () indicates tacit
2. `1 0⍴⍨2×⊢` [Swap](https://xpqz.github.io/learnapl/manip.html?#selfie-commute-constant)  ⍨ - parses as `((2×⍵)⍴1 0)` 
3. `1 0⍴` [Reshape](https://aplwiki.com/wiki/Reshape)  see above -  returns the argument as boolean vector of ones and zeros
4. `⍸` [Where](https://aplwiki.com/wiki/Identity)  gives the indices of ones in a Boolean [vector](https://aplwiki.com/wiki/Vector "Vector")


```APL
H←{⍸2|⍳2×⍵} ⍝ Either Index Origin
```

1. `⍳2×⍵` - multiplys the argument by two and returns the [Index](https://aplwiki.com/wiki/Index_Generator) 
2. `2|` -  [Modulus](https://aplwiki.com/wiki/Residue)  2  - returns 0 (even) and 1 (odd) see Parity
3.  `⍸` [Where](https://aplwiki.com/wiki/Identity)  gives the indices of ones(true values) in a Boolean [vector](https://aplwiki.com/wiki/Vector "Vector")

**Comment:**
[Parity](https://mathworld.wolfram.com/Parity.html) of an integer is being even or odd. 
[Modulus](https://aplwiki.com/wiki/Residue) gives the [remainder](https://en.wikipedia.org/wiki/Remainder "wikipedia:Remainder") of [division](https://aplwiki.com/wiki/Divide "Divide") between two real numbers. 
[Index Origin](https://aplwiki.com/wiki/Index_origin)  `⎕IO` - Generating Functions with that work with 0 or 1 origin see [Zero based Numbering](https://en.wikipedia.org/wiki/Zero-based_numbering)

```APL
I←{+\2-⍵↑1} ⍝ Works with ⎕IO←0 or 1
```

1. `⍵↑1` - [Overtake](https://xpqz.github.io/cultivations/Functions4.html?highlight=overtaking#take) 1 adds zeros to pad the array starting with 1 *ex* `5↑1` is 1 0 0 0 0
2. subtract the result from 2 (1 2 2 2 2)
3. `+\` - [Plus Scan](https://mastering.dyalog.com/Operators.html?highlight=scan#scan) returns the running sums from the vector in step two. (1 3 5 7 9)

```APL
I←(⍳+⍳-≢) ⍝ {(⍳⍵)+((⍳⍵)-(≢⍵))}
```

1. `⍳-≢` - [Indices](https://aplwiki.com/wiki/Indices)  of argument, subtracted from the [Tally](https://aplwiki.com/wiki/Tally) of the argument `((⍳⍵)-(≢⍵))` *ex*  1-⍨⍳5 (0 1 2 3 4)
2. `⍳+⍳-≢` -  [Indices](https://aplwiki.com/wiki/Indices)  of argument added to the result from step 1. 

**Glyphs Used:**
[Index](https://aplwiki.com/wiki/Index_Generator) - aka Iota - The notation `⍳N` where `N` is a natural number, describes a vector of the first `N` natural numbers. Starting from 0 or 1 depending on the [Index Origin](https://aplwiki.com/wiki/Index_origin) 

[Commute](https://aplwiki.com/wiki/Commute) aka Swap
[Quad](https://aplwiki.com/wiki/Quad_name)
[Identity](https://aplwiki.com/wiki/Identity)
[Reshape](https://aplwiki.com/wiki/Reshape)
[Indices](https://aplwiki.com/wiki/Indices) aka Where
[Residue](https://aplwiki.com/wiki/Residue) aka Modulus 
[Take](https://aplwiki.com/wiki/Take)
[Scan](https://aplwiki.com/wiki/Scan)
[Power](https://aplwiki.com/wiki/Power_(function))
[Branch](https://aplwiki.com/wiki/Branch)
[Tally](https://aplwiki.com/wiki/Tally)


**Concepts Used:**
[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Boolean Mask](https://aplwiki.com/wiki/Boolean)
[Parity - Modulous 2](https://xpqz.github.io/cultivations/Functions2.html#magnitude-residue)
[Fill Elements](https://aplwiki.com/wiki/Fill_element) - Padding with zeros
[Control Structure](https://aplwiki.com/wiki/Control_structure)
[Fork](https://aplwiki.com/wiki/Train#3-trains) - 3 Train





