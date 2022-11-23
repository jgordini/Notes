## [Home on the range](https://problems.tryapl.org/psets/2013.html?goto=P6_Home_On_The_Range)

**Problem:** Write a dfn which returns the magnitude of the range (i.e. the difference between the lowest and highest values) of a numeric array.

**Video:** https://youtu.be/36HlHsEjUIQ
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/6.apl

**Example Solutions:**
```APL
	I←(⌈/-⌊/), ⍝ Tacit - ravel the array and the take the difference of the max and min
	J←{0∊⍴⍵:0 ⋄ (⌈/-⌊/),⍵} ⍝ If zero is a member of the shape of the array return zero. Otherwise find the range. 
	```

**Quotes:**


**Comment:** 
```APL
⌈/⍬ ⍝ Maximum of empty vector is smallest representable number. Minimum reduction produces the opposite value.
⊃⍤⌽ ⍝ Choose the last element of a vector
1⌈≢ ⍝ is the length larger than one. Using this as a check to make sure it is not an empty array. Taking this result returns the entire array or zero if empty. 
,, ⍝ Catenate the ravel

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
[Replicate](https://aplwiki.com/wiki/Replicate) `/` - copies each [element](https://aplwiki.com/wiki/Element "Element") of the right [argument](https://aplwiki.com/wiki/Argument "Argument") a given number of times
[Catenate](https://aplwiki.com/wiki/Catenate) `,` - combines two arrays along a shared [axis](https://aplwiki.com/wiki/Axis "Axis"), left to right



**Concepts Used:**
[Ravel Order](https://aplwiki.com/wiki/Ravel_order)
[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.`
[Sort](https://xpqz.github.io/learnapl/manip.html?highlight=sort#grade-up-down) `data[⍋data]` 
[Overtake](https://aplwiki.com/wiki/Take#Overtaking) `↑` - A length larger than the argument length causes [fills](https://aplwiki.com/wiki/Fill_element "Fill element") to be inserted
[Fork](https://aplwiki.com/wiki/Train#3-trains)



[Radix](https://en.wikipedia.org/wiki/Radix)
[Index Origin](https://aplwiki.com/wiki/Index_origin) - Generating Functions with that work with 0 or 1 origin
[Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.`
[Matrix Multiplication](https://en.wikipedia.org/wiki/Matrix_multiplication)
[Vector Prefix](https://aplwiki.com/wiki/Prefix)
[Boolean Mask](https://aplwiki.com/wiki/Boolean)
[Complex Numbers](https://aplwiki.com/wiki/Complex_number)
[Phase](https://en.wikipedia.org/wiki/Phase_(waves))
