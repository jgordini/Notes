## [Slices of Pi](https://problems.tryapl.org/psets/2017.html?goto=P4_Slices_of_Pies)

**Problem:** Write a function that calculates and returns the areas of 0 or more pie slices. The left argument is 0 or more angles (in degrees). The right argument is 0 or more pie diameters. If the number of angles and diameters are not equal to each other (and neither is a single number), a `LENGTH ERROR` should be generated.

**Video:** https://youtu.be/XLrh6HwUbP8 
**Code:** https://github.com/abrudz/apl_quest/blob/main/2017/4.apl

**Example Solutions:**
```APL
v ← ¯3.1 4 1.5 92.6 ¯5 ⍝ Test Data
A ← {⍵/⍨⍵≠⌊⍵} ⍝ Compare the number against it's rounded version. Same is int. Different is Float.  
B ← (/⍨)∘(≠∘⌊⍨)⍨ ⍝ {(⍵≠(⌊⍵))/⍵}
	```

A
1. `⍵≠⌊⍵` [Floor](https://aplwiki.com/wiki/Floor) `⌊` Rounds down to the nearest real number.
2. [Not Equal to](https://aplwiki.com/wiki/Not_Equal_to) `≠` a [comparison function](https://aplwiki.com/wiki/Comparison_function "Comparison function")  tests whether arguments are unequal. This returns a boolean array where 1 indicates the non-integers. 
3. `⍵/`  [Compress](https://mastering.dyalog.com/Some-Primitive-Functions.html?highlight=compress#replicate) filters the right argument using the boolean array on the left. 
4. [Commute](https://aplwiki.com/wiki/Commute) `⍨` aka Swap used to put the boolean array generated in Step 1 on the left of the Compress. 



**Glyphs Used:**
[Floor](https://aplwiki.com/wiki/Floor) `⌊` - a [monadic](https://aplwiki.com/wiki/Monadic "Monadic") [scalar function](https://aplwiki.com/wiki/Scalar_function "Scalar function") that gives the [floor](https://en.wikipedia.org/wiki/floor_and_ceiling_functions "wikipedia:floor and ceiling functions") of a real number
[Equal to](https://aplwiki.com/wiki/Equal_to)  `=` - a [comparison function](https://aplwiki.com/wiki/Comparison_function "Comparison function") which tests whether argument elements are equal to each other.
[Not Equal to](https://aplwiki.com/wiki/Not_Equal_to) `≠` - a [comparison function](https://aplwiki.com/wiki/Comparison_function "Comparison function") which tests whether argument elements are unequal.
[Compress](https://aplwiki.com/wiki/Replicate) `/` - aka FIlter - requires the number of copies to be [Boolean](https://aplwiki.com/wiki/Boolean "Boolean"): each element is either retained (1 copy) or discarded (0 copies)
[Commute](https://aplwiki.com/wiki/Commute) `⍨` - aka Swap - used dyadically, the arguments are swapped. 
[Selfie](https://mastering.dyalog.com/Tacit-Programming.html?highlight=selfie#commute-selfie-and-constant) `⍨` - used monadically, the same argument gets used on both sides of the function. Thus, `F⍨y` is equivalent to - `y F y`.
[Format](https://aplwiki.com/wiki/Format) `⍕` - Dydactic column width and the number of decimal places for formatting [numeric](https://aplwiki.com/index.php?title=Numeric&action=edit&redlink=1 "Numeric (page does not exist)") arrays
[Comparison Tolerance](https://help.dyalog.com/latest/Content/Language/System%20Functions/ct.htm) `⎕CT` - determines the precision with which two numbers are judged to be equal
[Data Representation](https://help.dyalog.com/latest/Content/Language/System%20Functions/Data%20Representation%20Dyadic.htm) `⎕DR` - converts the data type of its argument Y according to the type specification X
[Each](https://aplwiki.com/wiki/Each) `¨` - applies its [operand](https://aplwiki.com/wiki/Operand "Operand") to each [element](https://aplwiki.com/wiki/Element "Element") of the [arguments](https://aplwiki.com/wiki/Argument "Argument")
[Membership](https://aplwiki.com/wiki/Membership) `∊` - tests if each of the elements of the left [argument](https://aplwiki.com/wiki/Argument "Argument") appears as an element of the right argument
[Print Precision](https://help.dyalog.com/latest/Content/Language/System%20Functions/pp.htm) `⎕PP` - number of significant digits in the display of numeric output
[Residue](https://aplwiki.com/wiki/Residue) `|` - aka Modulo - gives the [remainder](https://en.wikipedia.org/wiki/Remainder "wikipedia:Remainder") of [division](https://aplwiki.com/wiki/Divide "Divide") between two real numbers.
[Signum](https://aplwiki.com/wiki/Signum) `×` -  three poss ible results of Signum on a real argument are `0`, `1`, and `¯1` : Positive, Negative and Zero
[Encode](https://mastering.dyalog.com/Mathematical-Functions.html?highlight=encode#encode) `⊤` - `A⊤B`, turns `B` into a list(s) of digits in (mixed) base
[Replicate](https://aplwiki.com/wiki/Replicate) `/` - copies each [element](https://aplwiki.com/wiki/Element "Element") of the right [argument](https://aplwiki.com/wiki/Argument "Argument") a given number of times
[Error Guard](http://help.dyalog.com/18.0/index.htm#Language/Defined%20Functions%20and%20Operators/DynamicFunctions/Error%20Guards.htm) `::` - vector of error numbers :: expression to be evaluated

**Concepts Used:**
[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Comparison Tolerance](https://www.jsoftware.com/papers/satn23.htm) 
[Function Composition](http://help.dyalog.com/latest/index.htm#Language/Primitive%20Operators/Operator%20Syntax.htm#Function_Composition)
[Hook](https://aplwiki.com/wiki/Hook)
[Derived Function](https://aplwiki.com/wiki/Derived_function)
[Modulo Operation](https://en.wikipedia.org/wiki/Modulo_operation)

**Note:**
<mark style="background: #FFF3A3A6;">Ft </mark> ← Tacit Derived Function - Composed of Operators
Beginning with the first Parenthesis `(≠∘⌊⍨)`
1.  ⌊<mark style="background: #ADCCFFA6;">⍨</mark> ⍵ - Compare Argument with it's own Floor:  Selfie - ⍨
2.  ≠<mark style="background: #BBFABBA6;">∘</mark>⌊⍨ ⍵ - Preprocess the right argument with `≠` using the floor: Jot - ∘
3.   <mark style="background: #FFB8EBA6;">/⍨</mark><mark style="background: #BBFABBA6;">∘</mark>⍺⍺- Preprocess the right parenthesis expression using Jot and then Swap
4.   <mark style="background: #ADCCFFA6;">⍺⍺/ ⍵ ⍨ ⍵</mark> - Filter initial array using result: Selfie - ⍨

**Comment:** 
Swap - <mark style="background: #FFB8EBA6;">⍺ f ⍨ ⍵</mark>  is  <mark style="background: #FFB8EBA6;">⍵ f ⍺</mark>  
Selfie- <mark style="background: #ADCCFFA6;"> f ⍨ ⍵</mark>  is  <mark style="background: #ADCCFFA6;">⍵ f ⍵</mark>
<mark style="background: #BBFABBA6;">Jot </mark> - {R}←{X} f∘g Y - Preprocess the right argument. Then apply the left.

**Transcript:**
Hi, let's compute areas of circle sectors. And when we're doing so, we'll be using APL as the mathematical notation when reasoning about and simplifying the mathematical formula. Okay, to get started, the area of a circle. One way to think about the area of a circle is that you sort of say unroll the circle into its slices, these pie slices or sectors. Infinitely thin ones put them next to each other, we get a rectangle. The long sides of the rectangle are then contributed by the circumference and the short size of the rectangle is the radius. Well, the radius is equal to compute from the diameter, that's just half of it, but the long sides, well, we know that diameter times pi gives us the circumference, and we know that this circumference that has to contribute to long sides, being that there are two, that means half of that would be one of the long sides. So we can compute the area of the rectangle as the short side times the long side. If it's pi times half of the diameter, that's pi times the radius, so it's pi times the radius times the radius that gives us the area of the circle, and we can express this in the APL quite easily.

We don't have a symbol for pi directly, but almost always when we're using pi in mathematics, it's because we want to multiply by pi. APL does have a function to multiply by pi and appropriately is denoted by a circle. Circle R means pi times R where R is the radius and we want to multiply that by r of course. We haven't defined what R is and we are going to take as right argument the diameter not the radius, the right argument that's omega as the rightmost letter of the Greek alphabet and we can divide that by two and assign it into r. The result of an assignment is the value that was being assigned so this sets are to half of the argument diameter and returns that same value which we then multiply by pi times R and we can try it. APL automatically maps arithmetic operations so it doesn't matter that we have three values here, it will just work. These are the areas of circles where the diameters 9, 12, and 15.

We are multiplying Pi Pi with r and then we keep multiplying and it doesn't matter which order we do the multiplication in so we can remove the parenthesis over here and now it's very clear that we have I term R times r, or R times itself. Instead of using the dyadic function multiplication with one argument on each side, we can mention that the argument only once and use the commute operator or higher order function to change the multiplication from a diadic function infix that takes its arguments on the side to become a prefix function and it uses then the same argument on both sides of the multiplication. The symbol for this self thing as in self-multiplication is a bit like a selfie face, but now of course we're only using R here in the assignment and never reusing it so we might as well just use the Omega divided by 2 directly. This gives us the areas of these circles, but we don't want the full circle. We want a fraction of a circle, a sector, and specifically, we want it given in degrees. So how big a part of the full circle is it that we're dealing with? Well, let's say we have 60 degrees, so we want a fraction of the full circle. How much out of the full 360 degrees is it that we are having? So it's the left argument Alpha on the leftmost letter of the Greek alphabet and divided by 360. That's how big a part of the circle it is, and we multiply that by the area of the full circle. So we can see that 60 degrees out of a full 360, that's a sixth of the full value, we get the area of a 60 degree slice or sector of a circle. This is a solution to the problem, but let's try simplifying and condensing this a bit.

The first thing I'm going to do is undo this selfie that we did before and we do that since we have a fraction here. It's Omega divided by 2, then we can say Omega times Omega that's the square of that divided by 2 and divided by 2 again that is divided by two times two. How does this work out because APL functions have long right scope that is this division symbol sees everything on its right as its right argument, so this becomes Omega divided by 4 and then times Omega again so this is also Omega squared divided by 2 squared. You can see we get the same values right there. Okay, it's all multiplication division stuff, and we know that everything we multiply together on the right, that's what we divide by, and everything on the left and that's that which is being divided, so we are dividing by 360 over here on the left, and we can move that over on the right just by adding another 360 to the terms on the right, and then of course we can compute two times two times 360 is 1440.

Okay, this is already looking better, and this is about as dense as we can get it while still mentioning the arguments explicitly. However, there is a different style of APL functions, and they're commonly called tacit functions, and specifically, we're going to use a type of tacit function called a train. Tacit functions, the reason they're called tacit, we don't mention the arguments; we only mentioned functions, and that means the whole function, the overall function, is defined in terms of function applications to the argument or in this case of arguments.

Since we have two arguments, then all the functions are being applied to arguments are going to be applied to both of those arguments, and this function, the pi times function, we just want as a multiplication factor. We don't actually need it to be applied to any arguments at all, and therefore we're going to move it over to the very end. It will be a type of post-processing step. Right then, let's look at what we've got in terms of the arguments. Well, over here, I spot the left argument times the regular argument. Again, we're actually doing a multiplication by everything on the right, but that doesn't matter because it's all multiplications we are talking about, so let's parenthesize this, of course, that will still work. Um, and this is now a sub-expression defined in terms of a function application on both arguments.

This one is a bit more problematic because we don't need the left argument at all. We only want the right argument. So how can we express this in terms of a function application to the two arguments? To both of them, we need a function that ignores the left argument but does take the right argument and returns it as is. That's an identity function, specifically a right identity function. Now, for that, we have something called the right tack symbol or the functions could actually just be called right, and if we give it a left argument, it completely ignores that. You can kind of see it as a symbol that stops on the left and points at the right, so it will return just the right argument like this. We can try it. It gives the same result, and finally, another problem, this isn't the function at all. This is a constant, but we need it to be a function. We need it to be something that we apply to the arguments, but we don't want the left argument. We don't want the right argument at all. We just want the constant. This calls for a constant function. Obviously, APL doesn't have a built-in constant function that just takes an argument or arguments and returns 1440. However, we do have a higher-order function which takes an operand just like we had this selfie symbol which took a function that took two arguments and made it into a function that took a single argument using the same argument twice.

We also have a higher-order function that doesn't take a function but takes a value, in this case, 1440, and turns it into a function that always returns that value no matter which arguments you give it. Happens to be it's the same symbol. There is no contradiction or ambiguity here because this symbol, this operator always takes a single thing on its left in order to derive a new function. If the thing on its left is a function, then it does that which we said before of moving arguments around, and if it is a value, then it derives a constant function. So we can give this function arguments on one of both sides. Here we don't need to parenthesize this last part because remember APL functions have long right scope, and so the division sees everything to its right as its right argument, and this will then create a constant function, 1440 constant function, apply it to these arguments, and return 1440.

This is, of course, very verbose and unnecessary, but now we can switch from explicit to tacit, and we do that simply by eliminating all mention of the arguments, and we don't even need our curly braces anymore. We do need a pair of outer parentheses, though. Here's an argument. Let's get rid of that. That's another argument we're getting ready. Um, over there, then there are these two arguments that we're getting rid of, and these arguments over here we want to get rid of, and look, we get the same result. The last step is then removing all the redundant parentheses.

And there we go, a tacit function to compute circle sector areas. Thank you for watching.