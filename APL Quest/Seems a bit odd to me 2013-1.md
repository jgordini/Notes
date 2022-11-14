## [Seems a Bit Odd To Me](https://problems.tryapl.org/psets/2013.html?goto=P1_Seems_a_Bit_Odd_To_Me)

**Video:** https://youtu.be/Mj4wyLKrBho
**Problem:** Write a dfn to produce a vector of the first n odd numbers.
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/1.apl

**Example Solutions:**
```APL
F←{1-⍨2×⍳⍵}
F←(⍳+⍳-≢) ⍝ Tacit
F←{⍸2|⍳2×⍵} ⍝ Any ⎕IO
```

**Glyphs Used:**
[Iota](https://aplwiki.com/wiki/Index_Generator)
[Commute](https://aplwiki.com/wiki/Commute) aka Selfie
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
[Index Origin](https://aplwiki.com/wiki/Index_origin) - Generating Functions with that work with 0 or 1 origin
[Zero based Numbering](https://en.wikipedia.org/wiki/Zero-based_numbering)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Boolean Mask](https://aplwiki.com/wiki/Boolean)
[Parity - Modulous 2](https://xpqz.github.io/cultivations/Functions2.html#magnitude-residue)
[Fill Elements](https://aplwiki.com/wiki/Fill_element) - Padding with zeros
[Control Structure](https://aplwiki.com/wiki/Control_structure)
[Fork](https://aplwiki.com/wiki/Train#3-trains) - 3 Train





