## [Go Forth and Multiply](https://problems.tryapl.org/psets/2013.html?goto=P8_Go_Forth_And_Multiply)

**Problem:** Write a dfn which produces a multiplication table.

**Video:** https://youtu.be/O_l-nJYmDrs 
**Code:** https://github.com/abrudz/apl_quest/blob/main/2013/8.apl

**Example Solutions:**
```APL

	```

**Note:**

**Comment:** 


**Glyphs Used:**





[Floor](https://aplwiki.com/wiki/Floor) `⌊` - a [monadic](https://aplwiki.com/wiki/Monadic "Monadic") [scalar function](https://aplwiki.com/wiki/Scalar_function "Scalar function") that gives the [floor](https://en.wikipedia.org/wiki/floor_and_ceiling_functions "wikipedia:floor and ceiling functions") of a real number
[Equal to](https://aplwiki.com/wiki/Equal_to)  `=` - a [comparison function](https://aplwiki.com/wiki/Comparison_function "Comparison function") which tests whether argument elements are equal to each other.


**Concepts Used:**




[Dfn](https://aplwiki.com/wiki/Dfn)
[Tacit Programming](https://aplwiki.com/wiki/Tacit_programming)
[Comparison Tolerance](https://www.jsoftware.com/papers/satn23.htm) 
[Function Composition](http://help.dyalog.com/latest/index.htm#Language/Primitive%20Operators/Operator%20Syntax.htm#Function_Composition)
[Hook](https://aplwiki.com/wiki/Hook)
[Derived Function](https://aplwiki.com/wiki/Derived_function)
[Modulo Operation](https://en.wikipedia.org/wiki/Modulo_operation)

Hi and welcome to the APL quest (see APL wiki for details). Today's quest is the ninth problem from the 2013 round of the FPL problem solving competition. The problem is to find the average over a sub-period of a year's worth of data of numbers.

Starting off with some data, these are some cells. The obvious approach here is to use n-wise reduction, and maybe the simplest, at least for simple data, way to visualize n-wise reduction is using the additive reduction using concatenation. So, we have the sales and then we can say, for example, a three-wise reduction of the sales using concatenation, where that just concatenates together groups of three elements moving over one step each time. You can see we get these little windows, and now what we want is the average of each one of those.

So, we can use the very idiomatic APL expression for an average, which is the sum divided by the length, and apply it to each one of those, and that gives us the solution where the left argument is three and the right argument is sales. However, we should really package this as a proper function, so we can do that. These are two function applications. There's the comma slash using the 3s left argument, and we should probably use slash bars to make this more general for a higher rank in general arrays. And then there is the post-processing, which is the average function on each one.

So, the three can go outside here, and then we have on the top the n-wise reduction is applied between these arguments, between three and sales, and then the average each is applied to the result of that. So, this is a basic solution, but by far not the best solution, and this is because we can actually go in and apply something directly to each one. Because what we do when we do n-wise reduction, what we do here when we compute the average, is again and again we take something of length three, sum it together, and then divide count its length, which is always three, of course, and then divide the sum by the length.

Instead, what we could do is we could just do the n-wise reductions, and then all of those could be divided by three. That would give us the same, and we can express this as a little define. So, what we want is the left argument, which is the size that n-wise reduction over the right argument, and then we divide that by the left argument. That gives us the result, and this is a much better way to do it and certainly much more efficient.

We can even express this as a tacit function because it comes out very nicely that we have a function applied diatically between the left argument and the right argument and a middle function and then a selection of the left or right, which can be expressed in terms of function application as the left function applied between the left and right argument, and that is a fork. So, we can simply get rid of all these mentions of the argument and get this beautiful solution, and that is as good as it gets for the specific way that this problem has been stated.

However, there's an interesting edge case which the testing framework, if you look on problems.trypl.com, does not include, but we could say that the n, the window size, is larger than a year. So, for 12, we get the entire year averaged. For 13, we get no averages. And for 14, we get an error. So, how do we handle things that are so window sizes that are more than one step larger than the entire data that we've got?

There are many different ways we could go about this. I will have a look at some of them. For this particular problem, an obvious approach would be to go back here and simply clamp the argument. So, we have the left argument, but under no circumstances should it be larger than 13. If it's larger than 13, then we just want it to be 13. So, we take the smallest value of the left argument and 13 and replace it with that, and this works like normal as long as the left argument is small, and it works fine with 13, and it works fine with greater values as well.

Now, you could observe, of course, that when we're dividing by a number, if ever the left argument is 13 or greater, then that means that what's on the left of the division sign is an empty vector. In which case, it doesn't matter at all we divide by. There are no divisions going on, so we can remove this clamping from the right, and it will still work.

We can also generalize this, of course, so that it works on any number of elements in cells, and we would do that by simply adding one to the length of the cells. So, this is a more general purpose solution.

We could also use our original formulation and using the little train that we had before, we simply used the clamping size on the left and then the fork which was the n-wise reduction divided by left and then the data on the right, and this will work as well. And it works for these values that we have been using as well.

We can, if we want, get rid of this parenthesis by moving things around. So, we can put this plane argument on over here, and we can put this formula on the right, and then we could swap here, and this would work. However, since the only thing that's inside this train is a take right or left and another function, we can also move this over on and on this function and simply turn the take around to be on the right, and that will still work.

We can also unroll the whole thing because we can see that what's actually happening here is that the n-wise reduction where this is the n, and then over this, and finally we divide by the left argument, so we don't even need a train here inside the stephen. Then we can go ahead and make this tacit if we want, and there are various different ways we can do that. But here we can say we want the tally of the right argument, and this is the left argument. We want the n-wise reduction over the right argument, and then here's division by the left argument, and this would be the tacit equivalent. It's not necessarily better, but it's possible to write it like this.

Then there is a code golf trick for those that want to make the code as short as possible, and that is when we add one to the length, then we could actually get that out here, where we are anyway applying the function tally atop the selection of the right argument. We can include this one plus by concatenating the arguments. Since the left argument here is always going to be a single number, concatenating it to the right argument gives something that's not meaningful but it has the right length, namely one longer than the original right argument, and so we can save a little bit of code here by doing it this way. But it's obscure, and it's not efficient either because we are inserting an element at the beginning of potentially a larger amount of data. If short code is what you strive for and you want people to not understand what it is you've written, then this is the way to go.

A whole different approach to dealing with this problem of the length error is to simply try it and then catch the error when things go wrong. So we can again write our formula as we did before where we say that we divide by the left argument and then we have this n-wise reduction on the right argument, and that works fine, but when we do something that gets too big, then we get a length error.

Now length error is error number five, and so we can say we set up an error guard. Whenever any error number five happens, return the empty vector, and then it will return the empty vector. But you might also wish for a specialized operator and one that allows you to choose what happens when an error happens. How should we react to that?

Here we had an explicit guard, but we could also use a function that can't handle the error and instead combine it together with some kind of error handling function for an overall function that does handle an error. This exists, for example, in the J language where it's called "adverse." We can actually use APL to find a definition for "adverse," and we find this definition. I won't go into exactly what it is, but we can just give it a name "adverse." Now we can use it with any definition that we had from before. So we can say we want the sum divided by the left argument, but if anything goes wrong, then instead we apply a function which returns the empty vector. And so this works as before as long as no error happens, and when an error happens, then we apply the empty vector function and we get an empty vector result.

However, I prefer when I do APL to not rely on catching an error and continuing. Rather, I test my input and make sure that everything is okay with it. So I would do that in this case by writing an assumption that if the left argument is greater than the length of the right argument, then return the empty vector. Otherwise, we can do whatever we've been doing before, and that works as well. No error handling involved here.

Finally, there's an issue here if the input has higher rank. We're already using slash bar instead of slash in order to handle higher rank things, but if the length doesn't fit, is too large, and we end up with this guard, the results from the guard then the result isn't actually correct. Yes, it has to be empty, but not the empty vector. Say that we have the sales in a matrix with a single column, and then we're doing this with this n-wise average down the columns. That means we are reducing the number of rows in the table, but the table is still a one column table. This means if the left argument is too large, we should be getting a zero row table but not an empty list.

If instead, we redefined our function such that it can be larger than one because we know that when it's one larger than, then the n-wise reduction still works. 

If we define the function to only go into the special guard when it is more than one with the left argument is more than one larger than the length of the right argument, then we can observe here that we get notice there's no blank line, a zero row one column table and that this function doesn't work for the problem. 

The problem is of course that we universally just return the empty vector if the left argument exceeds the length of the right argument. What we really should do is preserve the entire shape of the argument only compressing the height of the table to have no rows if it's a two-dimensional table, or if it's a larger array we want to compress the first axis to have no content. The way we can do that is instead of returning this empty vector blanket, we use zero to compress along the first axis the leading axis and the right argument. Then we will see that it now works even for large arguments. This is the ultimate industrial solution. 

Thank you for watching.
