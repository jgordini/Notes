## [Home on the range](https://problems.tryapl.org/psets/2013.html?goto=P6_Home_On_The_Range)

**Problem:** Write a dfn which returns the magnitude of the range (i.e. the difference between the lowest and highest values) of a numeric array.

**Video:** https://youtu.be/36HlHsEjUIQ
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/6.apl

**Example Solutions:**

Non empty Vectors
```APL
	V ←¯1 4 1 5 9 2 6
	A ← (⌈/-⌊/), ⍝ Tacit - ravel the array and the take the difference of the max and min {(⌈/,⍵)-(⌊/,⍵)}
	
	B ← (⌈/∘,∘.-⍨) ⍝ {(⌈/)(,(⍵(∘.-)⍵))}
```

A
1. `,` We [Ravel](https://aplwiki.com/wiki/Ravel) `,` the array first to convert it into a [vector](https://aplwiki.com/wiki/Vector)  so that it works on a [Matrix](https://aplwiki.com/wiki/Rank), a two dimensional array.  
2. Then we apply a [fork](https://aplwiki.com/wiki/Train#3-trains) The two outer functions are applied first, and their results are used as arguments to the middle function.
3. `⌈/-⌊/` The two outer arguments are [Maximum Reduce](https://aplwiki.com/wiki/Maximum) `⌈/`  returns the largest element of a vector and [Minimum Reduce](https://aplwiki.com/wiki/Minimum) `⌊/` returns the smallest element of a vector. 
4. `-` The middle function is [Subtract](https://aplwiki.com/wiki/Subtract). 

B
1.  `∘.-` Using our vector we create a Subtraction Table ([Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.`). This will give us all the possible differences between values.
2. `⌈/,⍵∘.-⍵` We then ravel this and [Maximum Reduce](https://aplwiki.com/wiki/Maximum) `⌈/,` returning the largest value in our table. 
3. To make this [Tacit](https://aplwiki.com/wiki/Tacit_programming) we [Bind](https://aplwiki.com/wiki/Bind) `∘` the Maximum Reduce with the Ravel `⌈∘,` and use [Commute](https://aplwiki.com/wiki/Commute) `∘.-⍨`  to put our argument on either side of the Outer Product. 

Empty Arrays
```APL
⌈/⍬ ⍝ Maximum of empty vector is smallest representable number. Minimum reduction produces the opposite value.
C ←{0∊⍴⍵:0 ⋄ (⌈/-⌊/),⍵} ⍝ If zero is a member of the shape of the array return zero. Otherwise find the range.
D ←(⊃⍤⌽-⊃){⍵[⍋⍵]}⍤, ⍝ {(⊃(⌽⍵))-(⊃⍵)}
E ←((⌈/-⌊/)⊢↑⍨1⌈≢),
```

C
1.  [Membership](https://aplwiki.com/wiki/Membership) `∊` - tests if each of the elements of the left [argument](https://aplwiki.com/wiki/Argument "Argument") appears as an element of the right argument. 
2. [Shape](https://aplwiki.com/wiki/Shape) `⍴` - returns the _shape_ of its argument array
3. `0∊⍴⍵` So we are testing if 0 is a member of the shape of the array `⍵`. 
4. The [Guard](https://aplwiki.com/wiki/Dfn#Guards) :  Returns 0 if the left argument is true. 
5.  [Diamond](https://aplwiki.com/wiki/Statement_separator) ⋄ - Statement Seperator divides the two statements. The left one (with the guard) is evaluated first. 
6. `(⌈/-⌊/),⍵` Once we have confirmed that the vector is not an empty array we then move on to Solution A. It's details are above. 

D
1. `⍵[⍋⍵]` Uses [Grade Up](https://aplwiki.com/wiki/Grade) `⍋` to generate an index from lowest to highest. We can then [Sort](https://xpqz.github.io/learnapl/manip.html?highlight=sort#grade-up-down) `data[⍋data]` the array using that [index](https://xpqz.github.io/learnapl/indexing.html#bracket-indexing). 
2. `(⊃⍤⌽-⊃)` Now that it's been sorted we can subtract the first element from the last. Here we use [First](https://aplwiki.com/wiki/First) `⊃`  to grab the first element. We then use [Atop](https://aplwiki.com/wiki/Atop_(operator)) `⍤`  to apply [First](https://aplwiki.com/wiki/First) `⊃` to the result of the [Rotate](https://aplwiki.com/wiki/Rotate) `⌽`  See the [Dfn](https://aplwiki.com/wiki/Dfn) in the comment for more details. 
E


**Comment:** 
```APL
⌈/⍬ ⍝ Maximum of empty vector is smallest representable number. Minimum reduction produces the opposite value.
⊃⍤⌽ ⍝ Choose the last element of a vector
1⌈≢ ⍝ is the length larger than one. Using this as a check to make sure it is not an empty array. Taking this result returns the entire array or zero if empty. 
,, ⍝ Catenate the ravel

	I←(⌈/-⌊/), ⍝ Tacit - ravel the array and the take the difference of the max and min
	J←{0∊⍴⍵:0 ⋄ (⌈/-⌊/),⍵} ⍝ If zero is a member of the shape of the array return zero. Otherwise find the range. 
	K←(⌈/-⌊/),,42/⍨0∊⍴ ⍝ If zero is a member of the shape of the array return 42. Otherwise return nothing. Catenate the result with the ravel of the array (See I). Take the difference of the max and min.  

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
[Grade ](https://aplwiki.com/wiki/Grade) `⍋ ⍒`  - ⍋ 'foo' 'bar' 'baz'  - **Example** resulting in 2 3 1 means( the second item is first, The 3rd item is second, The first item is third.) This can then be used to index into the array and alphabeticlaly Sort it. 
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
