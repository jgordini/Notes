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

1. `⍳-≢` - [Indices](https://aplwiki.com/wiki/Indices)  of argument, subtracted from the [Tally](https://aplwiki.com/wiki/Tally) of the argument (1 item)  *ex*  1-⍨⍳5 (0 1 2 3 4)
2. `⍳+⍳-≢` -  [Indices](https://aplwiki.com/wiki/Indices)  of argument added to the result from step 1. 
*ex* `(⍳5)+(⍳5)-1` (1 3 5 7 9)

**Glyphs Used:**
[Index](https://aplwiki.com/wiki/Index_Generator) - aka Iota - The notation `⍳N` where `N` is a natural number, describes a vector of the first `N` natural numbers. Starting from 0 or 1 depending on the [Index Origin](https://aplwiki.com/wiki/Index_origin) 

**Concepts Used:**
[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
https://tacit.help/
[Boolean Mask](https://aplwiki.com/wiki/Boolean)
[Parity - Modulous 2](https://xpqz.github.io/cultivations/Functions2.html#magnitude-residue)
[Fill Elements](https://aplwiki.com/wiki/Fill_element) - Padding with zeros
[Fork](https://aplwiki.com/wiki/Train#3-trains) - 3 Train

Notes
Hello and welcome to this very first episode of The apl Quest, where we go through one problem every week from a past apl problem solving competitions. Phase One have a look at apl wiki for the details. Today's problem is the first problem from 2013, where we are asked to write a definite odd numbers.

Let's talk about generating some numbers. Let's say we want to generate the first ten numbers. Problem here is that these are all the adjacent integers.

So we multiply by two, getting us every other number. And then we can offset it by one. For example, we can take a one and subtract it.

So we're swapping the arguments on the minus. There are other alternatives. We could as well add negative one to this, or we could parenthesize it.

And for this we can build our defense that's the argument name omega, and we can try it. And there we go. Now, as you can see, by default, apl starts counting from one.

A lot of people, computer scientists especially some mathematicians, prefer starting counting from zero instead. And apl allows you to choose that. So we can set the index origin to zero.

And now we count from zero instead. This has upsides and downsides. Upside, of course, is you can choose whatever fits your problem and your comfort.

downside is that if you share code with others, you need to make sure you get the right index origin. You might need to set it yourself. And so it's a classic problem to try to write code that works with any index origin.

We can see that if we now try to apply a function, it gives an entirely wrong result. So that's no good. The corresponding function for index origin zero instead of subtracting one would be to add one.

There are other ways of generating this. Yes, the problem asks for a defen, but we can also write tested functions in apl. So here's another approach.

Let's start by writing the framework for a tested function. So we put some parentheses here, and then we can do two times, and not the name of the argument, but rather the identity of the argument. So it's an identity function and we can get 20 there.

Then we can use this to reshape a bunch of zeros and ones. So this is zero one reshape. We swapped the arguments on the reshapes.

It's a shape on the right and the content on the left. And now the only thing we miss is asking for the indices where we have the true who values or the ones. So the where function.

And there we go. This was index origin zero. Now let's switch back to index origin one.

And of course this won't work anymore. Rather, we just have to flip the ones and the zeros. And there we go.

Okay, that's all very nice, but how about if we wanted to write a function that could work with either setting of quad I o the index origin. And there are various approaches to that. Here are some cool ones that came up in the live event.

Let's say we start by multiplying the argument by two and then generating those integers. And now we take the parity of that. So that's the two residue, or modulars two of that.

And now we ask for where we have the ones. Okay, that's good. Now, what happens if we change to quaterio zero? Okay, so this part up here starts off differently, and then when we ask for the parity, we get the opposite.

But that's exactly what we want when we're using quadrant zero. Which means if we ask where are the ones, we get the right result. So we can see that this function works with either origin.

Let's give it a name. Argument goes here. And really what's happening is the Iota, the index generator and the Iota underbar the where function are canceling each other out.

So quad io gets one and this works, and quad io gets zero and it still works. So it's a really clever solution for writing it in a way that doesn't matter which index origin you're using. Now, the reason we're bumping into this is because we're dealing with indices at all.

We have the index generator, we have the where function, which is the indices of the true values. But we could also go about this in a very different way, in a mathematical way. So if we observe that we start with a one and then we increase with two every time, that's an interesting property.

So let's say like this. Let's take overtake here. We're taking the first ten elements of a one.

Now there aren't ten elements in the one, so apo will pad with appropriate fill elements which are zeros. We can subtract this from two. And notice here that we have the beginning element, the one, and then the offset to the next number over and over.

Which means if we ask for the cumulative sum or the plus scan of that, we get all the odd numbers. And since we didn't use any index related functionality, then there is no influence from the index origin. So we can put this into a function as well.

Argument goes here and we can try it. F ten and quarter one. F ten.

There we go. Now, let's say we wanted to go back to our original formulation where we started off with two times the integers indices. So in one case we wanted to subtract one.

That's when quad io is one. And in the other case we want to add one. That's in the case when quad io is zero.

So how could we adjust this? Of course, both the subtraction and addition can be seen as an addition. You just need to either add negative one or you need to add one. So that means if quad io is one, then we want to subtract one and if quad io is zero, then we need to add one and we can map this in a mathematical way.

So we have either a zero or a one. And if we take negative one and we raise it to the power of those two, then for the zero we get one, and for one we get negative one, which is exactly what we want. So now we can write our function as negative one raised to the power of the quad io.

And this will just take whatever global quad I O is currently in effect and we add that to twice the indices. So now we can try this was quad io one and quad io zero. And it still works.

Let me show you another very clever solution. It is as follows iota plus Iota minus the tally. This is a tested function.

We can apply it and we can see that indeed it works. Let's see what the structure looks like. It is a fork where the right tie in of the fork is itself a fork.

We start off by subtracting the tally from the indices. Now, what is the telly? That's how many major cells there are in the argument. A symbol number is just one.

So this is a clever way of subtracting one from the indices. So let's try that. We have the indices and we're subtracting one.

And then we're using that as right argument for plus. And the left argument is Iota applied on the argument. So the indices again.

Now, if we add these up, then well, you cannot probably see this already that we get exactly what we want. And so the way we can write all this together is the indices plus the indices minus the tally. And we can give this a name and apply it like that.

And that's all for today. Thank you for following along.



