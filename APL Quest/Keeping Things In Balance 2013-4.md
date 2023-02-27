## [ Keeping Things In Balance](https://problems.tryapl.org/psets/2013.html?goto=P4_Keeping_Things_In_Balance)

**Problem:** Write an APL dfn which returns a 1 if the opening and closing parentheses in a character vector are balanced, or a zero otherwise.

**Video:** https://youtu.be/El0_RB4TTPA
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/4.apl

**Example Solutions:**
```APL
	Di ← {1 ¯1 0['()'⍳⍵]} ⍝ Indexing into an array, 1 is left paren, ¯1 is Right and 0 is all other characters. 
	Df ← '('∘= - =∘')' ⍝ Tacit, subtracts the comparisons to get the depth changes. 
	Bn ← (¯1∊+\)⍱0≠+/ ⍝ checks for no ¯1 and no 0 in scan
	F ← (¯1∘∊⍱0≠⊢/)'('∘=+\⍤-=∘')' ⍝ Moves scan to be atop on comparisons +\⍤ 
	```

**Parenthesis depth changes**
Examples:
```APL
Di ← {⍵ ↑⍤,⍥⊂ 1 ¯1 0['()'⍳⍵]} ⍝ Convert the data to norrmalized form. 
Do ← -⌿'()'∘.=⊢
Df ← '('∘= - =∘')'
```
**Di**
1. `['()'⍳⍵]` - [Index of](https://aplwiki.com/wiki/Index_Of) `⍳` shows a 1 if left paren, 2 if right paren, and 3 if not found. 
2. `1 ¯1 0` - map the result of step 1  to (1 left,  -1 right, 0 not found)
3. `↑⍤,⍥⊂` -  [Enclose](https://aplwiki.com/wiki/Enclose) `⊂`  - Create a nested scaler  [Over](https://aplwiki.com/wiki/Over)  `⍥` -  Preprocess the right argument  [Merge Axis](https://aplwiki.com/wiki/Rank_(operator)#Merge_axes) -  `⍤,` concatenate the two axis  [Mix](https://aplwiki.com/wiki/Mix)  `↑` - trades one level of [depth](https://aplwiki.com/wiki/Depth) (nesting) into one level of [rank](https://aplwiki.com/wiki/Rank). 

**Do**
1. `'()'∘.=⊢` Applying an [Outer Product](https://mastering.dyalog.com/Operators.html?highlight=outer%20product#outer-product) using a comparison `=` Because this is a tacit function [Right Tack](https://aplwiki.com/wiki/Identity) acts as omega `⍵` and just returns the function it is pointing to. 
2. `'()'∘.=⊢` The `'()'` is the comparison that the outer product is applying against the identity. This creates a table. 
3. The first row a [Boolean Mask](https://aplwiki.com/wiki/Boolean) of 1's (true) where the left parenthesis is found and 0 (false) where is it not found. 
4. The second row is 1's where the right parenthesis is found. 
5. The result of step 2 is already a matrix. So we can use [Table](https://xpqz.github.io/cultivations/Functions7.html#table) `⍪`  - to ravel the major cells of the array and make each one of them into a row with the identity on top. This is just explanatory. 
6. -⌿ Subtracting the bottom row from step 2 from the top row in step 2 using a vertical minus [Reduction](https://aplwiki.com/wiki/Reduce) gives us the  depth changes.  

**Df**
1. We can do the two [Comparison Functions](https://aplwiki.com/wiki/Comparison_function) independently
2. `'('∘=` Making a boolean mask of the left parenthesis. 
3. `=∘')'` Making a boolean mask of the right parenthesis.
4. After subtracting the two results to give us the depth changes we can turn this into a [Tacit Function](https://aplwiki.com/wiki/Tacit_programming) 
5.   [Bind](https://aplwiki.com/wiki/Bind) `∘` is used to create a derived function with a single constant argument for each comparison. 
6. This creates a [3-train Fork](https://aplwiki.com/wiki/Train#3-trains) where the two outer functions are applied first, and their results are used as arguments to the middle function in this case subtract `-`. 

**Performance**
Examples:
```APL
'turtle' 'joy' 'cmpx'⎕cy'dfns'
(y n)←(⊢⍴⍨100×⍴)⍤⎕VR¨'turtle' 'joy'
cmpx'D',¨'iof',¨⊂' y'
```

We can evalute the performance of each function by importing the [CMPX](http://dfns.dyalog.com/n_cmpx.htm) function from the [DFNS](http://dfns.dyalog.com/n_contents.htm) library. 

1.  We can  [copy](http://help.dyalog.com/latest/Content/Language/System%20Functions/cy.htm) `⎕cy` CMPX  along with TURTLE and JOY from the DFNS library into our workspace.
2. We know that Turtle has matched parenthesis and Joy has unmatched parenthesis so we can use these two functions as our test cases. 
3. In the next line we are taking the [Vector Representation](https://xpqz.github.io/cultivations/CodeManagement.html?highlight=vr#visual-representation-vr) - ⎕VR of [Each](https://aplwiki.com/wiki/Each) `¨` function.
4. [Rank](https://aplwiki.com/wiki/Rank_(operator)) `⍤` - applies its left [operand](. https://aplwiki.com/wiki/Operand "Operand") function to [cells](https://aplwiki.com/wiki/Cells "Cells") of its arguments specified by its right operand array.
5. `⊢⍴⍨100×⍴` Using [Commute](https://aplwiki.com/wiki/Commute) `⍨`  - we first take the [Shape](https://aplwiki.com/wiki/Shape) of the idenitity `⊢⍴` and and then  [Reshape](https://aplwiki.com/wiki/Reshape) `100×⍴` it using 100 times it's current shape. 
6.  In the next line we are doing some meta programming to use cmpx to evalute the performance of each function. 
7. Every function begins with a D. We [Concatenate](https://aplwiki.com/wiki/Catenate)  [Each](https://aplwiki.com/wiki/Each) `,¨` of the suffixes 'iof' and then  [Concatenate](https://aplwiki.com/wiki/Catenate)  [Each](https://aplwiki.com/wiki/Each) `,¨` to the entire function ' y' using [Enclose](https://aplwiki.com/wiki/Enclose) `⊂` - An enclosed array is a [scalar](https://aplwiki.com/wiki/Scalar "Scalar"), which is subject to [scalar extension](https://aplwiki.com/wiki/Scalar_extension "Scalar extension").

**Balanced?**
Comment:
```
We are checking if two condtions are realized. 
1. Our final parenthesis level needs to be zero. 
2. As our function proceeds our parenthesis level should not drop below zero. 
3. Both expressions are then evaluted for performance using simlar steps to above
```
Examples:
```APL
Ba ← (∧/0≤+\)∧0=+/
Bn ← (¯1∊+\)⍱0≠+/
Bns ← (¯1∘∊⍱0≠⊢/)+\
F ← (¯1∘∊⍱0≠⊢/)'('∘=+\⍤-=∘')'
```
BA
1. `∧/` [And](https://aplwiki.com/wiki/And) [Reduction](https://aplwiki.com/wiki/Reduction "Reduction")  tests if it is true for ALL that the parenthesis depth is greater than or equal to zero. 
2.  `0≤+\` Plus [Scan](https://aplwiki.com/wiki/Scan) `+\` gives us the parenthesis depth. The [Comparison Function](https://aplwiki.com/wiki/Comparison_function) `0≤` checks if zero is less than or equal to the running sum. 
3. `∧0=+/` [And](https://aplwiki.com/wiki/And)  also checking if it is true that zero = the full sum `0=+/`. 
4. Both conditions must be true for BA to return 1 (for true).

BN 
1. `¯1∊+\` Checks if -1 is a [member](https://aplwiki.com/wiki/Membership) `∊` of the running sum or [Scan](https://aplwiki.com/wiki/Scan) `+\`. 
2.  `0≠+/` Checks if zero is not equal to the total. 
3. `⍱` [Nor](https://aplwiki.com/wiki/Nor) tests if neither argument (Step 1 or 2) is true: it returns 1 if both are false (0) and 0 if at least one is true (1)

BNS
1. Move the Scan to outside the parenthesis
2. `∘` [Bind](https://aplwiki.com/wiki/Bind) the enclose to the scaler. Tacit so the identity element is implied. 
3. `⊢/` Right Reduction picks the last element of the Scan we moved in step 1. 
4. Evaluate for performance. 

F
1. Take our BNS solution which is an [Atop](https://aplwiki.com/wiki/Train#2-trains) or 2-train. The left function is applied [monadically](https://aplwiki.com/wiki/Monadic_function "Monadic function") on the result of the right function.
2. Take our Df Solution which is a [Fork](https://aplwiki.com/wiki/Train#3-trains) or 3-Train. The two outer functions are applied first, and their results are used as arguments to the middle function.
3. `+\⍤-` To combine these solutions we use an [Atop](https://aplwiki.com/wiki/Atop_(operator)) `⍤` operator  on Df to post process the result of the subtraction using a scan `+\`. 
4.  The depth change in Step 3 is then passed to BNS. 

**Find and Replace** - Regular Expressions
Comment:
```
Find all the parenthesis and eliminate pairs of parenthesis until none are found. 
If we have an empty set Parenthesis are matched.
Any parenthesis that are left means they are unbalanced.
```

Examples:
```APL
t←'(1 2)×(3+(3÷4))×(1+2)÷8'
Re ← ''≡'\(\)'⎕R''⍣≡⍤∩∘'()'
Re0 ← ''≡'()'⎕R''⍠'Regex'0⍣≡⍤∩∘'()'
Fi ← ''≡(⊢(/⍨)¯1(⊢⍱⌽)'()'∘⍷)⍣≡⍤∩∘'()'
```

RE
1.  `∩∘'()'` [Intersection](https://aplwiki.com/wiki/Intersection) `∩` removes elements from the left which are not present in the right. In this case we remove everything but the parenthesis. 
2. `'\(\)'⎕R''` [Regular Expression](https://xpqz.github.io/cultivations/Regex.html?highlight=regular%20expressions) using `⎕R` to find parenthesis and replace with an empty string. Each parenthesis is escaped using `\` Performs this operation one time. 
3. `''≡` [Match](https://aplwiki.com/wiki/match) `≡` is checking if the result matches an empty string. 
4. `⍣≡`  [Power Match](https://xpqz.github.io/cultivations/ConditionControlledLoops.html?highlight=power)  `⍣≡` - Iterating until a fixed point is reached. In this case when no more parens are found. 
5. `⍤` [Atop Operator](https://aplwiki.com/wiki/Atop_(operator)) takes the two monadic functions and glues them together. 

RE0
1. [Variant](https://aplwiki.com/wiki/Variant) `⍠` - Switch Regex to plain text using `'Regex'0`
2. This allows us to use `⎕R` to search and replace parenthesis without escaping them
3. The same function is then applied. 

FI
1. `⍣≡⍤∩∘'()'` Step 1,4,5 from RE
2. `'()'∘⍷` Using the [Find](https://aplwiki.com/wiki/find) `⍷` function returns a boolean mask where 1 indicates the start of an set of open and closed parens. 
3. `¯1(⊢⍱⌽)`  Takes the [mask]([Boolean Mask](https://aplwiki.com/wiki/Boolean)) generated in Step 2 `⊢` and [Rotates](https://mastering.dyalog.com/Working-on-Data-Shape.html?highlight=rotate#rotate-vectors) `⌽` it one step `¯1`.  This indicates where the closed parens are.  We want to remove parens with the mask so we are using  [Nor](https://aplwiki.com/wiki/Nor) `⍱`. To retain parens we would use [Or](https://aplwiki.com/wiki/Or)  
6.  `⊢(/⍨)`  Use the result of Step 3 to [Filter](https://en.wikipedia.org/wiki/filter_(higher-order_function) "wikipedia:filter (higher-order function)")  the string **t** using [Compress](https://aplwiki.com/wiki/Replicate) `/` We use [Commute](https://aplwiki.com/wiki/Commute) `⍨`  and the [Identity](https://aplwiki.com/wiki/Identity) `⊢` to maintain right to left evaluation becuase this expression is [Tacit](https://aplwiki.com/wiki/Tacit_programming).  This will be more clear if we look at the Dfn version generated by [tacit.help](https://tacit.help/)

```APL
Fi ← {''≡(({(('()'⍷⍵)⍱(¯1⌽('()'⍷⍵)))/⍵}⍣≡)(⍵∩'()'))}
```

7. `''≡`  Step 3 from RE

**Abusing APL's Parser** 
Comment:
```
The APL interpreter can parse paired and unpaired parenthesis and braces and will return an error if unpaired. We can use this in our expressions.  
```

Examples
```APL
t←'(1 2)×(3+(3÷4))×(1+2)÷8'
Nd ← {0::0 ⋄ (⍎'{} '['()'⍳⍵])/1}
Np ← {0::0 ⋄ ⊃∊⍎⍕1,1,¨⍵∩'()'}
```

ND
1. `⍎'{} '['()'⍳t]`  This is the same process as Step 1 of Di. We are getting the [Index of](https://aplwiki.com/wiki/Index_Of) `⍳` our string **t** and then [Mapping](https://xpqz.github.io/learnapl/indexing.html#bracket-indexing)  the result to open and closed brace `{}` and a blank space.  We then [Execute](https://aplwiki.com/wiki/execute) ⍎ this function.
2. `/1`  [Reduction](https://aplwiki.com/wiki/Reduction "Reduction") `/` over a scaler. Applying a function to a scaler doesn't change the function and will let APL evaluate it. It will return the 1 if it does not error. 
3. `0::0⋄`  [Error Guard](https://help.dyalog.com/latest/#Language/Defined%20Functions%20and%20Operators/DynamicFunctions/Error%20Guards.htm#ErrorGuards) `::` Error numbers 0 and 1000 are catch-alls for synchronous errors and interrupts respectively. [Diamond](https://aplwiki.com/wiki/Statement_separator) `⋄` is a statement Seperator. If the expression from Step 1 and 2 generates an error, its immediately preceding: `0::0` catches it and returns 0.
4. Evaluted on the [Vector Representation](https://xpqz.github.io/cultivations/CodeManagement.html?highlight=vr#visual-representation-vr) - ⎕VR of two Dfns 'turtle' and 'joy'. 

NP
1. `1,1,¨t∩'()'` We evaulate the set [Intersection](https://aplwiki.com/wiki/Intersection)  `∩` of our string against open and closed parens `()` Then we [Concatenate](https://aplwiki.com/wiki/Catenate) a 1 in front of  [Each](https://aplwiki.com/wiki/Each) `1,¨` character. Then we concatenate a 1 in front of the entire expression.  `1,` 
2. `⊃∊⍎⍕` We then [Format](https://mastering.dyalog.com/Execute-and-Format-Control.html#the-format-primitive) ⍕  the result into a character array. Numeric and nested arrays are converted into vectors or matrices of characters and [Execute](https://aplwiki.com/wiki/execute) ⍎ it. [Flattening](https://xpqz.github.io/learnapl/manip.html?highlight=enlist#ravel-catenate-enlist-member) `∊` any nested arrays and [Picking](https://aplwiki.com/wiki/first) ⊃ the first element which should be the 1 we concatenated to the front in Step 1. 
3. `0::0⋄` we use the same Error Guard as in Step 3 of ND to check for unpaired parenthesis. 

**Glyphs Used:**
[Index of](https://aplwiki.com/wiki/Index_Of) `⍳`
[Bracket Indexing](https://xpqz.github.io/learnapl/indexing.html#bracket-indexing)  [ ]  - Mapping 
[Mix](https://aplwiki.com/wiki/Mix)  `↑`
[Merge Axis](https://aplwiki.com/wiki/Rank_(operator)#Merge_axes)  ,⍤
[Over](https://aplwiki.com/wiki/Over)  `⍥`
[Enclose](https://aplwiki.com/wiki/Enclose) `⊂` - creates a nested scalar by wrapping its argument under one level of nesting
[Outer Product](https://aplwiki.com/wiki/Outer_Product) `∘.`  - using a comparison `∘.=`
[Laminate](https://aplwiki.com/wiki/Catenate)  `⍪` Catenate First - Add a line to a matrix
[Reduce](https://aplwiki.com/wiki/Reduce) `⌿` Vertical Minus Reduction
[Bind](https://aplwiki.com/wiki/Bind) `∘`
[Vector Representation](https://xpqz.github.io/cultivations/CodeManagement.html?highlight=vr#visual-representation-vr) - ⎕VR`
[Rank](https://aplwiki.com/wiki/Rank_(operator))  `⍤` - applies its left operand function to cells of its arguments specified by its right operand array. 
[Identity](https://aplwiki.com/wiki/Identity) `⊢`
[Reshape](https://aplwiki.com/wiki/Reshape) `⍴`
[Commute](https://aplwiki.com/wiki/Commute) `⍨`  - aka Selfie or Swap
[Tally](https://aplwiki.com/wiki/Tally) `≢`
[Each](https://aplwiki.com/wiki/Each) `¨`
[Scan](https://aplwiki.com/wiki/Scan) `+\`  - Plus Scan
[Sum](https://aplwiki.com/wiki/Add#Reduction) `+/` - [Reduction](https://aplwiki.com/wiki/Reduction "Reduction") with Add gives the sum of the whole list.
[And](https://aplwiki.com/wiki/And) `∧` - tests if both arguments are true: it returns 1 if both are true (1) and 0 if one or both are false (0)
[Nor](https://aplwiki.com/wiki/Nor) `⍱` - tests if neither argument is true: it returns 1 if both are false (0) and 0 if at least one is true (1)
[Enlist](https://aplwiki.com/wiki/Enlist)  `∊` - Enlist flattens over all layers of nesting
[Intersection](https://aplwiki.com/wiki/Intersection)  `∩`
[Match](https://aplwiki.com/wiki/match) `≡`
[Power Match](https://aplwiki.com/wiki/Power_(operator))  `⍣≡` - Iterating until a fixed point is reached.
[Atop](https://aplwiki.com/wiki/Atop_(operator)) `⍤` - takes two (monadic) functions and glues them together.  Uses the left operand to process the right

<mark style="background: #BBFABBA6;">Regular Expressions</mark>
[Variant](https://aplwiki.com/wiki/Variant) `⍠` - Switch Regex to plain text
[Find](https://aplwiki.com/wiki/find) `⍷`
[Rotate](https://aplwiki.com/wiki/rotate) `⌽`
[Or](https://aplwiki.com/wiki/or) `∨`
[Compress](https://aplwiki.com/wiki/Replicate) `/` -  Outside of APL, [filter](https://en.wikipedia.org/wiki/filter_(higher-order_function) "wikipedia:filter (higher-order function)") typically provides the functionality of Compress
[Execute](https://aplwiki.com/wiki/execute) ⍎
[Diamond](https://aplwiki.com/wiki/Statement_separator) ⋄ - Statement Seperator
[Format](https://aplwiki.com/wiki/format) ⍕ - Flatten
[First](https://aplwiki.com/wiki/first) ⊃

**Concepts Used:**
[Comparison Function](https://aplwiki.com/wiki/Comparison_function)
[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Boolean Mask](https://aplwiki.com/wiki/Boolean)
[Reduction](https://aplwiki.com/wiki/Reduce)
[Fork](https://aplwiki.com/wiki/Train#3-trains)
[Dfns Workspace](https://aplwiki.com/wiki/Dfns_workspace)
[Boolean Functions](https://aplwiki.com/wiki/Boolean#Boolean_functions)
[Logical Conjunction](https://en.wikipedia.org/wiki/Logical_conjunction)
[Logical Nor](https://en.wikipedia.org/wiki/Logical_NOR)
[Fork and Atop Problem](https://aplwiki.com/wiki/Train#Problems_caused_by_function-operator_overloading)
[Regular Expressions](https://xpqz.github.io/cultivations/Regex.html)
[Intersection](https://en.wikipedia.org/wiki/Intersection_(set_theory))
[Error Guard](https://aplwiki.com/wiki/Dfn#Error-guards) `::`
[Performance](https://aplwiki.com/wiki/Performance#Performant_usage)
[CMPX](http://dfns.dyalog.com/n_cmpx.htm)

**Reference:**
[Sixteen APL Amuse-Bouches](http://archive.vector.org.uk/art10501480) - #5
[Learn Regular Expressions](https://www.regular-expressions.info/)


hello and welcome to this fourth apl quest check apl wiki for details today's quest is called keeping things in balance here we take a character vector and it has parenthesis in it we need to check whether the parentheses are balanced so it looks like a normal mathematical expression or whether things are wrong say we begin with closing parentheses that aren't there or we end with some open parenthesis let's get started let's start by having a test data just to see how this works so we create a character vector and let's put in some expression there for example something like this okay this is a balanced one and the approach we're going to start off with today is that we're going to find out where the depth of the parenthesis nesting changes and there are a few different ways we can do that then later we'll move on to actually finding out whether or not the parentheses are balanced or not a very simple approach and a classic one in apl is to convert the input into a normalized form so we can look up every character in this test case the indices of its characters in the open plan and closed paren and apl does this that if an element isn't found in a lookup array then we get the next index so one and two are the open and close and three is any character which wasn't found now we need to map these to indicate when the parenthesis level changes so and we use this to index into a vector and we say when we have open parenthesis then we increase the parenthesis level when we have a closing pan then we decrease the parenthesis level and any other character we map to zero as it doesn't affect the level let's stack this together with original input so we're going to mix the concatenation of the enclosures with the original and we can see how when we have open parenthesis the parenthesis level increases closing parenthesis decreases and any other character leaves the parenthesis level unaffected so we can make this into a function let's call this the parenthesis depth changes using indexing and so it's going to take this formula but there are other ways that we could do that you do this we can in a similar manner but instead of lookup we can do a comparison so if we take the character vector consisting of these parentheses and do an outer product with the characters here we get a table and we can do the same trick as before to stack up on top oops oh it's a yeah that's not what i should have done i increased the rank which is just sticking up it's already a matrix there we go and we can see here that the first row of this boolean matrix indicates whenever the parenthesis level increases and the second row indicates when it decreases and then the other row is of course zero and then we can do this clever thing that we can subtract the top row from the uh subtract the bottom row from the top row so the top row minus the bottom row that's a vertical minus reduction and that gives us the same thing now we need to stack them on top of each other there you go all right now we get the same thing as before so this is a different way of doing it and we can call this the parentheses depth changes uh using the outer product over out of product um so we can we can even do this as a as a tested function because it's so simple and the argument is just the identity right there okay but there are more ways we can do this we can also do the two comparisons each by themselves so let's say we take the comparison to the left parenthesis and the comparison with the right parenthesis and put them next to each other that gives us these two vectors we could of course stack them on top of each other and then we get just like the other product but since we're going to subtract them from each other we can just put the minus in between and that gives us the parenthesis depth changes right away we can give this a name and we can again make it into a tested function because it's really simple so we can and it looks very nice as well symmetric like this so we can bind this to equal making equal equals and left parenthesis in a magnetic function and subtract the same thing we can we can put the because equal is computed so we can put the argument on either side i'd like to put it like this because it looks really cool so this is the depth uh using a fork um with the two outer tines equality to the two parenthesis and then subtracting the the two from each each other um now this is on a tiny little test case let's get some real data that we can try this on and then let's do some performance comparison before we move on to the second part of the problem because we haven't solved the whole thing yet we need to find out are they balanced or not so for that i'm going to copy in some functions from the defense workspace and we're not going to use these functions other than just their source as example data so there's a turtle function there's a joy programming language interpreter and then we need the comparison and performance comparison as well we copy those from defense right and they are large functions these turtle enjoy but not really large enough so let's create some data we have some data i know that uh turtle has parentheses that are well balanced and joy has parenthesis that are not well balanced i looked that up before um so this gives us these two test cases let's call it yes and no and whether or not they are balanced um i'm going to take the source code of each one so the vector representation of each of turtle turtle and joy and then i'm going to make them a little bit bigger so we're going to take that source code and reshape it using 100 times its current shape and this gives us some large test data we can see here that y is a bit a bit of a million and um n is a couple of million so now we can compare them but instead of typing out the expressions with these three different functions let's use an apl expression to generate the expressions that we're going to time a little bit of meter programming here so every function begins with a d and we concatenate that to each of these suffixes i o and f and then we concatenate each of those to the entire argument y so this gives us these three expressions and we can run cmpx on those and we can see that the df the one that just that is the fork just compares it to one parenthesis and the other parenthesis and subtracting them is by far the fastest one for these cases and what if we do it on something that isn't balanced and again um interestingly enough here the i and the o are approximately the same speed but df still wins out so this is the first part of the problem determining when the parenthesis level changes goes up and down next we're going to use this to compute whether or not they're actually balanced or not so we can use df that was the fastest one on our test case that gives us these ones and zeros and now we have to think about what does it mean that it's balanced so there really two things to it one is that when the whole input is finished when we reach the end we have to reach down to parenthesis level zero and when we go along we're never allowed to dip below zero because that would mean that we have closed more parenthesis than we have opened so we want the running total the the of the parenthesis depth that's very simple we can do that with a with a scan and this is then the parenthesis parentheses depth and and we also want to know what is the um what is the left element whether or not it is zero that would be the sum of them and that's zero so now we can just put together these two conditions the first condition being that it is always true it's true for all that they are greater than or equal to zero in the running sum and also it has to be true that 0 equals the full sum let's give this a name and we'll call it ba because we're using this and condition both this condition has to be true and this condition has to be true but we can also do it a different way a little bit more succinct at least the first part if we're saying it has to be all true that's the end reduction that all of the elements have to be greater than or equal to zero now the parenthesis level can only change by one step at a time there's no double open parenthesis there's only single open parenthesis and they can only go down one level so the first condition which is to check that we never reach a negative level it would have to pass negative one in order to become negative it might continue further on but it's a sufficient check to see whether or not we have any negative ones so we can say negative one is a member of the running sum means it's invalid and the second and then so now we're doing it in reverse we're using a negative conditions and similarly we have to say that 0 is different from the sum so these are things that are not allowed to be to be present and therefore if neither of them are present then our expression is well balanced so instead of having an and we have to use a nor so we can call this balanced using nor let's compare the performance of these two and similarly we can create the expressions that we want so we start off with uh ba and bn we could we can just spell it out since the only two of them bn um and each one of them concatenated to the entire yd here uh so we have we haven't assigned this yet we should go up and assign this so this is the depth for y and we should do the depth fun for n as well and then we can get these two expressions and cmpx on that and yeah it's about the same you can do the same thing for the nose and that's a bit faster and we can probably reason our way for that because in ba we did the comparison of everything in the running sum and then we check whether they're all true whereas in bn we're not doing any comparisons and for we're not doing comparisons for all of the elements we just start looking for negative one and as soon as we hit any negative one we're done so the membership function will just terminate right there it doesn't have to look through the entire array so in some cases that can be faster and so here bn in some cases can be faster than ba and that means we can potentially put together a whole solution here based on these so we take df from before and we supply its results to bn and that should give us the answer and so we can do f on each of y and n should give it one and zero and that worked we can we can also spell it out um so but we'll come back to that because there's one more step we can do let's go back for a moment and think about what we're doing the running sum and the full sum you can then observe since we're adding the elements from left to right that means that the last element of the running sum is equal to the the full sum and so we're actually doing a little bit of unnecessary work we're summing twice one once we're summing a cumulative sum and the other one we're summing everything again so the last step of the cumulative sum is the same thing as doing the entire sum it might drown in the mass of the cumulative sum but still it could be a little bit of performance gain so being that we found that bn was the fastest let's rewrite that and so to say break out the scan and just pick out the right element from this scan the cumulative sum instead of using a new reduction so let's break out the scan here um and we do that put the scan outside and that means that the um this scan is already just the identity but since we now have just a single argument with a dyadic function we can just glue those together with a bind operator and then we have zero is different from and this is the last element so the last element of the of the scan we can also just write that as a right reduction so this is bns and now we can try to compare them so we can say we're looking at bn and bns each one concatenated to the yd and we got a bit of a speed up there and we can try it again with nd as well and we got a bit of a speed up there again so while it's not all about performance this was fairly easy to to go from one solution to another and you got better and better performance so we can put all of this together and a final solution we define f and then we take the definition from b and s here and then we also want the parenthesis comparison like this this was the df now there's one problem we want to apply this function which is a fork and then we want to apply this function which is at a top and this gives us sort of say three parts it becomes would be a fork and we would call this the adequately the scan that's not what you want but we can fix this by taking the scan and moving it to be in the top on top of the um of the subtraction and now we have a fork as the right part where we have uh the two comparisons and then the scan of the subtraction as the middle time so the scan post processes the result of the subtraction and then we feed that over to where we extract the nest element so we can check that it's in non-zero and then we can and also we look whether or not there are any negative ones in that and then we do the nor at the end and that is our solution so this is a really good apl solution to the problem and that's what i would use now that that's done let's look at some alternative solutions that are not going to have good performance but they're interesting to look at nonetheless something that would be nearer to many people especially if they come from other programming languages and especially if they come from pearl is to use regular expressions and we can do that as well so let's go back to our test case here and observe it we're only interested in the parenthesis so we can do the set intersection with parenthesis just to get the structure that's the only thing we're interested in and now we can go in and remove pairs of parentheses so here's a set of parentheses with nothing in them here's a set of parentheses or nothing in them here's another one and then repeat the process until we are done and if there's nothing left that means that they've been balanced if anything is left any parenthesis is left hanging whether it's opening at the at the end or closing at the beginning then it's unbalanced and that means if the result of this repeated transformation is the empty character vector that means it's balanced okay how can we define this so we start off by applying the function of intersection with the parenthesis and then we can write a regular expression now we have to escape the parenthesis and replace with nothing so we can apply this on our test case and then we can see it removed the first parenthesis and the last parenthesis and the inner of the middle parenthesis and then we just need to do it again and check whether or not it is the empty character vector we don't know how many times we're going to do it therefore we have to say that we are doing it until nothing more changes also known as power match so applying it until there are no more changes and that allows us to do we can try this and but it's probably a bit much to do it on the large case well we can try it oh that worked okay and we can do it on the uh on the last case of the no as well and you can see that that worked so let's call this regular expressions and we can just put it up here that's our regular expression solution this is not going to be performant for a apl but well oh i missed missing the right argument that is because oh yeah of course this is because this is a magnetic function we want to apply to our argument and this is a magnetic function we want to apply to our argument we need to glue them together to become a top right there but regular expressions are very expensive we have to spin up an entire regular expression engine and possibly transform our input to a format you can understand and get the result back collect the information extract information from there we can actually use quad r it's a fairly new feature that was added to use quad r it's for replacements of plane text from this character vector to this character vector as well and we do that by applying the variant operator where we switch regex off and now we don't need to escape the parentheses anymore because now it's just plain text replace from these two parentheses to nothing so let's call this well it's not really regular expressions anymore it's replace but well no regex i guess however keeping this method in mind we can also try implementing it in apl and that might give even better performance so now we have to think a bit we have to find places where we have an open paren and close brand and then remove those well let's look at our test case we can easily use the find function to find a oh find we need to remove the all the characters that are not paranthesis first so let's take this and compare with this you can see how it matches every place where we find open brand close brand we get a one bit indicating so however our problem is that we want to find to to remove those parts so we need to indicate also where the closing parenthesis corresponding closing parenthesis is let's space this out a little bit for readability and what we can do here is we can do a rotate so we can do both this mask that we just computed and or when it's rotated one step and this indicates both the opening paren and the closing paren but we don't actually want to preserve those we want to get rid of those the way we do that is just by flipping the the or to a nor and this gives us a mask indicating just the characters that we want to keep so now we can say we want this just the the text that has the characters from an open print close paren and then we glue this together so we have a function here and then negative one and that puts it all together and we then we can filter it using that so that gives us this now it's not useful to look at the original anymore and then we just need to repeat this process over and over but we don't need to repeat removing the parentheses everything that's not parenthesis we just need to repeat this squeezing of away open paren close paren so we can do the same thing with power match again and then we can compare to the empty character vector like that so we can put all this together here we've got we can actually put it atop and glue this together again and this is using find so we can try uh find on each of y and n and it gives us one and zero so now we basically implemented the same transformation that we used regular expressions and then the quad r just for text replacement and we've now implemented that same transformation in raw apl we can do a comparison of the performance of these so we have re and re0 and fi and we're comparing them to y so and we can see that the regular expression engine it takes is very heavy weight it's much faster to do it either with replace without regex or implementing it ourselves and we can do it on end as well and a similar thing so it's probably easiest to implement it just with the text replacement that's built in but if you implement it yourself you can get a little bit more performance right there and finally uh some kind of joke uh solutions that we can kind of circumvent the problem because this kind of parenthesis matching is already happening in well in mathematics in most programming languages as well when apl evaluates an expression it has to do this kind of thing as well um such an expression as this can of course be evaluated as apl if our parentheses don't match then april will tell us that there is unpaired parenthesis that means the apl interpret itself somehow has this same functionality built in and we can leverage that and the same thing happens we if we use braces that are not in in defense that are not paired up correctly then ap let's tell that they're unpaired braces let's see how we can abuse this we can start off using the braces and doing the same mapping as we did way in the beginning mapping to 1 negative 1 and 0 and here we'll map the input to braces instead so we look up the in open and close parenthesis and then we use that to index into open and close phrase and a blank so this gives us an expression which doesn't do anything useful it won't be able to actually run but apl's parser will protest if it doesn't look right how in order to force apl to actually use this function we have to execute it and that returns a function with a strange display form that's not very interesting the only thing we want to see is whether or not this errors are not now if it does error then we can catch that error if it doesn't error we need to apply this function in a way that won't error and how can we apply a function that's completely meaningless and doesn't do anything it will just result in the value error well we can take this function and reuse it to reduce over a scalar or one element vector reducing over a scalar doesn't change that scalar at all so apl will never actually use the function it just registers that it's there and will error if the function doesn't work so this should work fine and if we try to do it with an expression that doesn't work like what we did before then we should get an error so the only thing that's left here is to transform this into a function we wrap it in a in a defend put in an error guard if we get any error then it's not balanced and otherwise uh we it's going to reduce over the one and reducing one doesn't change the one so that's the one that we want for result so this uses nesting depth of defense we can try try this but i think we'll run into a problem that the test case is just too big for the parser to to deal with yeah this isn't working why isn't this working given giving the wrong result oh yeah of course um i know why it's not working because the test is cases are in fact too big so let's just try it on the vector representation of turtle and joy okay now it's working um the the reason is giving it a zero is because the error guard is catching the air condition that the expression is too complex for apl to parse so this is working um and here's another approach using stranding of parentheses so let's say we take we start off the same way by extracting just our parentheses and then we concatenate a one in front of each character and we also concatenate a one in front of everything just in case the expression is empty and now we should be able to to run this we can we can execute this in apl it gives some nested array but this will force apl to check whether the parenthesis level is uh working so we just need to we can format it to flatten it um and then we can we can try executing it and then we just need to see whether or not that will work so if we hit any error return a zero otherwise we ask for the first element of this which is of course going to be one because uh we should maybe flatten it as well just in case it's nested because it's all once everywhere and this is using nesting depth of parenthesis to parse this and we can try it and what we had before so this is for joy and it's okay and for turtle oh this is not right this is not working so see here oh of course we put a t here instead of putting an omega was silly me okay turtle and uh joy yeah so those you give the correct result and of course the performance of this is going to absolutely hurt i'm not going to bother you with this these are just some fun solutions of abusing the system thank you very much for watching
