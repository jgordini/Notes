## [Float your Boat](https://problems.tryapl.org/psets/2013.html?goto=P7_Float_Your_Boat)

**Problem:** Write a dfn which selects the floating point (non-integer) numbers from a numeric vector.

**Video:** https://youtu.be/w5LvImFVi2M
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/7.apl

**Example Solutions:**
```APL
	```

**Quotes:**


**Comment:** 
```APL
```

**Glyphs Used:**
[Maximum Reduce](https://aplwiki.com/wiki/Maximum) `⌈/` - returns the largest element of a [vector](https://aplwiki.com/wiki/Vector "Vector")
[Minimum Reduce](https://aplwiki.com/wiki/Minimum) `⌊/` - returns the smallest element of a [vector](https://aplwiki.com/wiki/Vector "Vector")
[Ravel](https://aplwiki.com/wiki/Ravel) `,` - an array's ravel is the [vector](https://aplwiki.com/wiki/Vector "Vector") containing all its [elements](https://aplwiki.com/wiki/Elements "Elements") in [ravel order](https://aplwiki.com/wiki/Ravel_order "Ravel order").
[Over](https://aplwiki.com/wiki/over) `⍥` - both arguments are pre-processed using the right operand
[Commute](https://aplwiki.com/wiki/Commute) `⍨`  - aka Selfie or Swap
[Membership](https://aplwiki.com/wiki/Membership) `∊` - tests if each of the elements of the left [argument](https://aplwiki.com/wiki/Argument "Argument") appears as an element of the right argument.
[Shape](https://aplwiki.com/wiki/Shape) `⍴` - returns the _shape_ of its argument array
[Guards](https://aplwiki.com/wiki/Dfn#Guards) : - Return result
[Diamond](https://aplwiki.com/wiki/Statement_separator) ⋄ - Statement Seperator
[Each](https://aplwiki.com/wiki/Each) `¨` - Apply to each element
[Grade ](https://aplwiki.com/wiki/Grade) `⍋ ⍒`  - Grade returns a [permutation](https://aplwiki.com/index.php?title=Permutation&action=edit&redlink=1 "Permutation (page does not exist)") [vector](https://aplwiki.com/wiki/Vector "Vector") whose length equals the number of [major cells](https://aplwiki.com/wiki/Major_cell "Major cell") - See sort below.
[Pick](https://mastering.dyalog.com/Nested-Arrays-Continued.html?highlight=pick#pick) `⊃` - Left argument is path, right argument is data. 
[Atop](https://aplwiki.com/wiki/Atop_(operator)) `⍤` - Uses the left argument to process the result of the right. 
[Tally](https://aplwiki.com/wiki/Tally) `≢` - Length of the array
[Take](https://aplwiki.com/wiki/Take) `↑` - used to get the first few, or last few, elements of a vector
[Identity ](https://aplwiki.com/wiki/Identity)`⊢` functions and operators rather than names are used to direct the flow of arguments
[Replicate](https://xpqz.github.io/cultivations/Functions7.html?#replicate) `/` - copies each [element](https://aplwiki.com/wiki/Element "Element") of the right [argument](https://aplwiki.com/wiki/Argument "Argument") a given number of times
[Catenate](https://aplwiki.com/wiki/Catenate) `,` - combines two arrays along a shared [axis](https://aplwiki.com/wiki/Axis "Axis"), left to right
[Intersection](https://aplwiki.com/wiki/Intersection) `∩` - removes elements from the left which are not present in the right. Duplicates in the right do not matter.
[Enlist](https://aplwiki.com/wiki/enlist) `∊` - Flattens over all levels of nesting
[Match](https://aplwiki.com/wiki/match) `≡` - indicates whether the left and right [argument](https://aplwiki.com/wiki/Argument "Argument") arrays are identical

**Concepts Used:**
[Ravel Order](https://aplwiki.com/wiki/Ravel_order)
[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.`
[Sort](https://xpqz.github.io/learnapl/manip.html?highlight=sort#grade-up-down) `data[⍋data]` 
[Overtake](https://aplwiki.com/wiki/Take#Overtaking) `↑` - A length larger than the argument length causes [fills](https://aplwiki.com/wiki/Fill_element "Fill element") to be inserted
[Fork](https://aplwiki.com/wiki/Train#3-trains)
