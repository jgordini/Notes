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

Hello and welcome to this APL quest episode. See APL wiki for details. Today's quest is the last problem from the 2013 round of the APL problem-solving competition. We are simply given a set of linear equations and the values that those equations add up to, and then we are to find the solution for the variables.

Let's start by creating this equation system, so we'll have a simple example of just three equations with three variables. This is saying: 4x + 1y + z = 2, 2x + 2y + 2z = 6, and so on. A solution to that is if x is -1, y is 3, and z is 1, and we can check this.

So, the problem here is that we don't know this result, which is -1 3 1. We want to compute it. What we do know are these values: 2, 6, and 4. So, in other words, we want to find a v and such that m plus dot times this value gives 2 6 and the missing right it gives 2 6 4.

Luckily, we can write this up, so we can say we want to apply this negative one time to get this value. This is a power negative one, applying a function in reverse. Applying it negative one times really asks this question: what argument, in this case, right argument, we're giving it the left argument over here, what right argument can we give to m plus that times such that we get r and that solves the problem?

Now, in the problem specification and r go is the left argument and m is the right argument. So we can type up our solution as plus the times operator negative one commute just swap the two arguments like that, and then the matrix goes on the right and the vector goes on the left, and that's a proper solution.

However, this matrix multiplication in reverse is actually the same as multiplying by the inverse, and the inverse of a matrix we have in APL as a primitive. We can then state this instead as multiplying by the inverse. The dyadic form of this character, which is often nicknamed domino and looks like a one one domino, is actually exactly that. So, the entire solution can just be that.

In other words, this problem has a one-character solution in APL.

Now, that's of course a lot of fun, but it would be nice to see how we could really solve this without APL just doing all the work for us. There are a couple of ways to do this. There's a really clever way to do it called the Hoteling-Buddhic scheme, if I pronounce that correctly. It states that we can do an iterative approach to approximate better and better the correct solution to an inverse of a matrix. And as we had before, if we have the inverse, then the problem is basically solved.

The formula looks like this: the next iteration is the previous iteration matrix multiplied by two times the identity matrix minus the grand matrix that the original matrix has been multiplied by the previous iteration. We can rearrange this formula a little bit and take this vi here and multiply it into the parenthesis. So that gives us 2vi minus vi plus dot times (which is the matrix multiplication) and vi times a, which is the original matrix, times vi again.

We can then state this in APL. The way we would write that is: 2 times vi minus vi plus dot times a plus times vi. We can break this and avoid the parenthesis simply by having two vi's here. It'll be the same thing as multiplying it by two.

Now we can make this a function of the original matrix on one side. So we have a and then we make a function and we have the previous iteration as the right argument. We'll do it as a test function, so we start from the right here and build it up first. We want the matrix multiplication of them plus the times, and then we want to multiply by vi again, so vi is the right argument, plus that times that. Then we want to subtract this from vi (that's the right argument minus that), and then we add another one of the right arguments. We can write it up like this.

So here's a tested way to compute this, and this is one iteration of it. However, we actually want to keep doing this until it becomes stable. The way we would then write that is we could take it as a function where the right argument function of the original matrix here called a, so that becomes fed into our inner function as a left argument, and then we keep iterating with the power operator until two consecutive iterations are the same.

So, we just need to apply this whole thing on our initial guess, and that's the next problem. The problem is, it's kind of hard to find an initial guess which will work out for us, but recently someone named Solemani came up with a surefire way to determine an initial guess. What he stated was that the transpose of the array divided by the trace of the matrix times its transpose is a good starting guess that will always come up. Again, see his paper if you want the details of how exactly that works out.

So, we again take the trace of the matrix times its transpose, and then we divide the transpose by that. First, we do the trace of the matrix times its transpose. We can have this matrix m, and we can transpose it, and then we can do matrix multiplication with itself. Then we want the trace. The trace is the sum of the major diagonal from top left to bottom right, and that we can do as a 1 1 transpose. Then we sum that up. For our matrix m here, that magic value that we want to divide by is 84. Then we would go ahead and divide the transpose of m by 84, and that would be a good starting value.

Now, this can be simplified a little bit, and for that, we need to observe some characteristics of doing exactly this, the trace of the matrix multiplied by its transpose. So what we're going to do is we'll start with a matrix that is easy to recognize where the bits and pieces are going, and instead of doing an actual multiplication with itself, we are going to take and model the plus and the times as functions that are just saying what they would do rather than actually doing them.

This will show us that we give great little boxes showing us what's going on, and we need to multiply it with itself with the right argument to the matrix multiplication being transposed. Here we can see all the results that we're getting, but we're only interested in the diagonal.

We're taking the 1 1 transpose of that, and now we can observe exactly what's going on. Remember, the trace is the sum of these, so really what will happen is we're going to add all these together, all these little boxes. Notice that 1 1 is multiplied by each other, and 2 2, 3 3, and so on. That means every element of the entire matrix gets multiplied by itself squared, and then we just sum all these squares together, which means we can state this much easier. We can just revel the matrix, square it, and sum it. Or we could, of course, square it first, revel at the summit, and use many different ways of doing that. We can also combine this summing and the multiplication into an inner product. And that means that if we're going to write in the training, we want this as short as possible. Then we can write the revel cluster times the revel of the matrix, and that gives us that.

Now we just need to take the transpose of the matrix and divide by that. So we can take the transpose, divide by this, and that gives us our starting value, which isn't very interesting to look at. But let's put all of this together. So what we let's go up in and get it from up here, we had this formula right here, and we stick it in here. This is then the inverse that we get. We can compare this with the inverse primitive and see we got the exact same value.

Now, remember how we solve this with v? We can go in and say v plus that times this inverse, or instead, and this is a solution, but we want to glue these two things together to be a single function. So this right part here is the inversion of the matrix, and the left part is the matrix multiplication. We multiply with the inverse, and that gives us our solution. 

We can, and remember, this is an iterative thing. So inside here is the power match, which just runs over and over again until two consecutive things match each other. It would actually be neat to see how this would look. We can do that by doing each iteration separately. Now I happen to know that we only need to go through 11 iterations, so for every one of the numbers from 1 to 11, we're going to apply it that many times. And then we can see the progression of better and better values for x, y, and z to solve this system until we're done and it becomes stable.

This is a modern computational approach to this. The traditional way that you might have learned in school is the Gauss-Jordan method, and you can find it in the defense workspace. Here is an adapted version of what you can find there. I'll try to explain it a little bit. What it's doing here, if you learned in school, you would have learned that there are these various actions you can take on your matrix together with the result values to slowly build up diagonal matrix, and then you have the solution. When we're running it as computer code, then we can't go by a feeling of what's easier. Instead, we just go through all the steps every time.

So what we're building up here at the bottom is our equation system. These are the final values that we're putting next to it, and then these are the reversed indices because reduction runs from the right to left. That's what this comment is trying to say. This is what we're going to reduce over, so we just eliminate here, eliminate here, eliminate here, in this order. And every time we eliminate, we choose, for precision reasons, the row that has the largest magnitude. This gives us a specific column, and we start. Because we don't go down diagonals, we first start with the first column, and then we get rid of the first few elements that have already been taken care of. Of course, with the first one, that means we're dropping zero. Notice that the index origin is zero up here.

Then we look at the magnitudes and choose the largest one, and that's what we call our pivot row. And then we swap things around, so where we're up to in the nth row and the pivot row, we're taking those and just flipping them. There are just two of them, so then reverse just swaps the two around. Now we've got a matrix that's modified by having these two swapped around. And then we want to normalize such that in that corner, or should we say, of the sub-matrix missing rows and columns that is on the intersection of the nth column and the negan's row. That's why we have alpha semicolon alpha here, and we divide that. We divide all the other values there so that we get a 1.

Finally, we have the step of adding or subtracting, and the way it's been implemented here is that we are adding or subtracting not just for that single row but for the entire matrix. So, it's built up using masks, essentially. When we add or subtract 0, then nothing happens, and we're using a mask. This 2 right here represents all the indices for all the rows, and then we have a specific row number here, which gets subtracted wherever it's different from. We get zeros, and that means we only get one on this single row. Then we pick out from that column there and create a matrix with all the values that are in this particular row. And then that effectively means we have a bunch of zeros, and we subtract the right values in the right place.

Once that's done, since we've done a reduction, we have enclosed, so we open that up. We're not interested in the entire matrix with result values. Rather, we can chop those away, so that's what this is doing. And then just in case they were all identical, we used a single value. We just reshape it to have the right shape. And that's how the Gauss Jordan method works. We can try that. It solves the whole thing immediately and like this in exactly the same way.

I happened to look up an old paper on APL 360, and it was actually interesting. It brought us an example of code and this function, which is an inversion of a matrix but implemented in old style APL. I'm not going to go through and explain this. You can do it on your own. It's really very much the same, but in a you know old style without using any of the new operators. I've altered one slight thing. You can see a capital A in there, and that was an original function in APL 360. They had some functions called alpha and omega, which were prefix and suffix vectors, so alpha or which I've changed to an A here because alpha is now meaning something else. You can define it like this in our case here where the left argument is the length of the vector, and the right argument is the number of leading ones in that boolean vector. In our case, it could just be a take, but I suppose overtake, meaning you can take more elements than there are in the array, wasn't supported yet at that time. So, you can actually replace these A's just with an up arrow, and this gives us our inverted matrix.

As we can see from before, it's the same thing as the primitive. And that means that we could do the same thing here with multiplying the result of the inversion with our desired result values. That gives us our values for x, y, and z in the very oldest of fashions. So, this concludes the first year of APL problem-solving competitions, and we're now going to continue next time with the problems from 2014. Thank you for watching.
